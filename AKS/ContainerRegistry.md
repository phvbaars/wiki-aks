# Azure Container Registry Integration with AKS

## Create Azure Container Registry

```bash
# Create a resource group (if needed)
az group create --name <resource-group> --location <location>

# Create Azure Container Registry
az acr create --resource-group <resource-group> --name <acr-name> --sku Basic
```

## Connect ACR to AKS Cluster

```bash
# Attach ACR to existing AKS cluster
az aks update --name <aks-cluster-name> --resource-group <resource-group> --attach-acr <acr-name>
```

## Import Existing Image into ACR

```bash
# Import nginx image from Docker Hub into your ACR
az acr import --name <acr-name> --source docker.io/library/nginx:latest --image nginx:v1
```

## References

- [Create a new ACR - Microsoft Docs](https://learn.microsoft.com/en-us/azure/aks/cluster-container-registry-integration?tabs=azure-cli#create-a-new-acr)