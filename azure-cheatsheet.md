# Azure CLI Cheatsheet

> The Azure CLI provisions, configures, and monitors Microsoft Azure resources from the terminal.

## Table of Contents
- [Login & Account](#login--account)
- [Resource Groups](#resource-groups)
- [Virtual Machines](#virtual-machines)
- [Storage](#storage)
- [AKS](#aks)
- [Networking](#networking)
- [App Service](#app-service)
- [Microsoft Entra ID](#microsoft-entra-id)
- [Key Vault](#key-vault)
- [Monitor](#monitor)

## Login & Account

| Command | Description |
| --- | --- |
| `az login` | Sign in interactively to Azure. |
| `az login --use-device-code` | Sign in with a device code flow. |
| `az account show` | Display the active subscription and tenant. |
| `az account list --output table` | List subscriptions available to the signed-in identity. |
| `az account set --subscription "Production"` | Set the active subscription. |
| `az logout` | Sign out of Azure CLI sessions. |

## Resource Groups

| Command | Description |
| --- | --- |
| `az group list --output table` | List resource groups in the active subscription. |
| `az group create --name rg-app --location eastus` | Create a resource group. |
| `az group show --name rg-app` | Display a resource group's properties. |
| `az group exists --name rg-app` | Check whether a resource group exists. |
| `az group delete --name rg-app --yes --no-wait` | Delete a resource group without prompting. |
| `az resource list --resource-group rg-app --output table` | List resources in a resource group. |

## Virtual Machines

| Command | Description |
| --- | --- |
| `az vm list --output table` | List virtual machines. |
| `az vm create --resource-group rg-app --name vm-app --image Ubuntu2204 --admin-username azureuser --generate-ssh-keys` | Create a Linux virtual machine. |
| `az vm start --resource-group rg-app --name vm-app` | Start a stopped virtual machine. |
| `az vm stop --resource-group rg-app --name vm-app` | Stop a running virtual machine. |
| `az vm deallocate --resource-group rg-app --name vm-app` | Deallocate a VM to stop compute billing. |
| `az vm run-command invoke --resource-group rg-app --name vm-app --command-id RunShellScript --scripts "uname -a"` | Run a shell command on a Linux VM. |

## Storage

| Command | Description |
| --- | --- |
| `az storage account list --output table` | List storage accounts. |
| `az storage account create --name appstorage123 --resource-group rg-app --location eastus --sku Standard_LRS` | Create a storage account. |
| `az storage container create --account-name appstorage123 --name uploads --auth-mode login` | Create a blob container using Entra authentication. |
| `az storage blob upload --account-name appstorage123 --container-name uploads --name file.txt --file file.txt --auth-mode login` | Upload a blob from a local file. |
| `az storage blob list --account-name appstorage123 --container-name uploads --auth-mode login --output table` | List blobs in a container. |
| `az storage blob download --account-name appstorage123 --container-name uploads --name file.txt --file ./file.txt --auth-mode login` | Download a blob to a local path. |

## AKS

| Command | Description |
| --- | --- |
| `az aks list --output table` | List AKS clusters. |
| `az aks create --resource-group rg-app --name aks-app --node-count 2 --generate-ssh-keys` | Create an AKS cluster. |
| `az aks show --resource-group rg-app --name aks-app` | Display AKS cluster configuration. |
| `az aks get-credentials --resource-group rg-app --name aks-app` | Merge AKS credentials into kubeconfig. |
| `az aks scale --resource-group rg-app --name aks-app --node-count 3` | Scale the default AKS node pool. |
| `az aks upgrade --resource-group rg-app --name aks-app --kubernetes-version 1.30.0` | Upgrade an AKS cluster Kubernetes version. |

## Networking

| Command | Description |
| --- | --- |
| `az network vnet list --output table` | List virtual networks. |
| `az network vnet create --resource-group rg-app --name vnet-app --address-prefixes 10.0.0.0/16 --subnet-name app --subnet-prefixes 10.0.1.0/24` | Create a virtual network and subnet. |
| `az network vnet subnet list --resource-group rg-app --vnet-name vnet-app --output table` | List subnets in a virtual network. |
| `az network nsg create --resource-group rg-app --name nsg-web` | Create a network security group. |
| `az network nsg rule create --resource-group rg-app --nsg-name nsg-web --name AllowHttps --priority 100 --direction Inbound --access Allow --protocol Tcp --destination-port-ranges 443` | Create an inbound NSG rule. |
| `az network public-ip list --resource-group rg-app --output table` | List public IP addresses in a resource group. |

## App Service

| Command | Description |
| --- | --- |
| `az appservice plan create --name plan-app --resource-group rg-app --sku B1 --is-linux` | Create a Linux App Service plan. |
| `az webapp create --resource-group rg-app --plan plan-app --name app-example-123 --runtime "NODE:20-lts"` | Create a web app with a runtime stack. |
| `az webapp list --resource-group rg-app --output table` | List web apps in a resource group. |
| `az webapp config appsettings set --resource-group rg-app --name app-example-123 --settings NODE_ENV=production` | Set application settings on a web app. |
| `az webapp restart --resource-group rg-app --name app-example-123` | Restart a web app. |
| `az webapp log tail --resource-group rg-app --name app-example-123` | Stream web app logs. |

## Microsoft Entra ID

| Command | Description |
| --- | --- |
| `az ad user list --output table` | List Microsoft Entra users. |
| `az ad user show --id user@example.com` | Display a user's directory properties. |
| `az ad group list --output table` | List Microsoft Entra groups. |
| `az ad group member list --group platform-team --output table` | List members of a directory group. |
| `az ad sp list --display-name ci-deployer` | List service principals by display name. |
| `az ad sp create-for-rbac --name ci-deployer --role Contributor --scopes /subscriptions/SUBSCRIPTION_ID` | Create a service principal with an Azure role assignment. |

## Key Vault

| Command | Description |
| --- | --- |
| `az keyvault list --output table` | List accessible Key Vaults. |
| `az keyvault create --name kv-app-123 --resource-group rg-app --location eastus` | Create a Key Vault. |
| `az keyvault secret set --vault-name kv-app-123 --name DbPassword --value "secret-value"` | Create or update a Key Vault secret. |
| `az keyvault secret show --vault-name kv-app-123 --name DbPassword` | Retrieve a secret's metadata and value. |
| `az keyvault secret list --vault-name kv-app-123 --output table` | List secret metadata in a vault. |
| `az keyvault key list --vault-name kv-app-123 --output table` | List keys in a vault. |

## Monitor

| Command | Description |
| --- | --- |
| `az monitor metrics list-definitions --resource RESOURCE_ID --output table` | List metrics available for a resource. |
| `az monitor metrics list --resource RESOURCE_ID --metric "Percentage CPU"` | Retrieve a resource metric time series. |
| `az monitor log-analytics workspace list --output table` | List Log Analytics workspaces. |
| `az monitor log-analytics query --workspace WORKSPACE_ID --analytics-query "AzureActivity | take 10"` | Run a Kusto query against a workspace. |
| `az monitor activity-log list --resource-group rg-app --max-events 20` | Show recent activity log events for a resource group. |
| `az monitor diagnostic-settings list --resource RESOURCE_ID` | List diagnostic settings on a resource. |
