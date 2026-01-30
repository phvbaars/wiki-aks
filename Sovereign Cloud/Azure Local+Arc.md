# Azure Local + Arc

## Overview

Azure Local is Microsoft's on-premises cloud platform that **requires Azure Arc to function**. They are tightly connected—Arc is not an add-on, it's the control plane that makes Azure Local operate.

Azure Arc is the Control Plane
Azure Arc enables you to manage your AKS cluster from Azure. Without Arc:
- You cannot deploy AKS on Azure Local
- You cannot use Azure Monitor, Policy, or Defender
- The system becomes unsupported by Microsoft

## Azure Local Sovereignty Model

### Designed For

| Capability | Description |
|------------|-------------|
| Data residency | Data stays on-premises |
| Operational sovereignty | You run the hardware |
| Network sovereignty | You control the perimeter |
| Regulatory compliance | Meet local compliance requirements |

### Not Designed For

- Full offline operation
- Independence from Azure
- Running without Arc
- Running without Entra ID
- Running without Azure billing/updates

## Arc Requirements

Arc requires persistent connectivity and integration with Azure:

- Persistent outbound connectivity
- Registration of resources in Azure
- Telemetry and health signals
- Policy and configuration sync
- Billing and metering
- Identity integration with Entra ID

> **Important:** This means the environment is **not isolated** and **not independent**.

## Sovereignty Classification

| Type | Azure Local + Arc |
|------|-------------------|
| Hybrid sovereignty | ✅ Supported |
| Absolute sovereignty | ❌ Not supported |

Azure Local supports **sovereignty within the Azure ecosystem**, not sovereignty *from* Azure.

## Full Technological Independence

Azure Arc does **not** offer full technological independence. That would require:

- No dependency on a public cloud
- No outbound connections
- No reliance on Azure control plane
- No Microsoft-managed identity, policy, or billing
- Ability to run fully offline indefinitely

## Alternative: Azure Stack Hub

**Azure Stack Hub** is the only Microsoft platform that meets full technological independence requirements:

- Can run fully disconnected
- No Arc dependency
- No Azure control plane
- Used by defense, intelligence, and isolated environments