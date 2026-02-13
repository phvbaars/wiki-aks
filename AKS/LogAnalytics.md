## Log Analytics

### Flow

Pod stdout/stderr
     ↓
Container runtime (containerd)
     ↓
Azure Monitor Agent (DaemonSet in kube-system)
     ↓
Data Collection Rule (DCR)
     ↓
ConnectLog Analytics Workspace
     ↓
Tables: ContainerLogV2, KubePodInventory, KubeNodeInventory, etc


### Setup

In AKS/Insights menu → Enable Container Insights → choose Log Analytics workspace

Azure CLI:
```
az aks enable-addons \
  --resource-group rg-prod \
  --name aks-prod \
  --addons monitoring \
  --workspace-resource-id /subscriptions/<sub>/resourceGroups/<rg>/providers/Microsoft.OperationalInsights/workspaces/<law>

```
Azure will automatically:
- Deploy Azure Monitor Agent to cluster
- Create a Data Collection Rule
- Connect workspace

### Query Logs

Use Kusto Query Language (KQL) in Log Analytics to search logs:

```kusto
ContainerLogV2
| where PodName == "your-pod"
| project TimeGenerated, LogMessage
| order by TimeGenerated desc
```

Let op: ContainerLogV2 is de nieuwe tabel voor container logs. De oude tabel ContainerLog is deprecated.

### AKS Diagnostic Settings

AKS Monitor Diagnostic Settings gebruik je dus niet meer voor container logs. Je kunt deze nog wel gebruiken voor control plane logs, maar dat is niet per se nodig. Control plane logs zijn ook beschikbaar in Log Analytics via de Azure Monitor Agent. Je hoeft dus niet per se een aparte Diagnostic Setting te maken om control plane logs naar Log Analytics te sturen. 

| Category                | What it is           |
| ----------------------- | -------------------- |
| kube-apiserver          | API calls            |
| kube-audit              | audit logs           |
| kube-controller-manager | scheduling events    |
| kube-scheduler          | scheduling decisions |
| cluster-autoscaler      | scaling activity     |

Tables:
- AzureDiagnostics
- AKSAudit
- AKSControlPlane

### Best Practices

- Use namespaces and labels for filtering and cut costs



