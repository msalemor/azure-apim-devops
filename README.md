# azure-apim-devops

A DevOps guide for Azure API Management

## ARM Templates

- Microsoft's infrastructure as code

### ARM Template basics

- json file
- Three sections
  - parameters: can be overriden
  - variables: used during the execution
  - resources: the services to be deployed in Azure
  - Outputs
  - Functions

### Sample ARM template

> **Note:** This is a sample ARM template to create a storage account. Here we can see how parameters, variables, resources and outputs are used.

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storagePrefix": {
      "type": "string",
      "minLength": 3,
      "maxLength": 11
    },
    "storageSKU": {
      "type": "string",
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_RAGRS",
        "Standard_ZRS",
        "Premium_LRS",
        "Premium_ZRS",
        "Standard_GZRS",
        "Standard_RAGZRS"
      ]
    },
    "location": {
      "type": "string",
      "defaultValue": "[resourceGroup().location]"
    }
  },
  "variables": {
    "uniqueStorageName": "[concat(parameters('storagePrefix'), uniqueString(resourceGroup().id))]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2019-04-01",
      "name": "[variables('uniqueStorageName')]",
      "location": "[parameters('location')]",
      "sku": {
        "name": "[parameters('storageSKU')]"
      },
      "kind": "StorageV2",
      "properties": {
        "supportsHttpsTrafficOnly": true
      }
    }]
}
```
## APIM DevOps Toolkit

- Reference: https://github.com/Azure/azure-api-management-devops-resource-kit
- Releases: https://github.com/Azure/azure-api-management-devops-resource-kit/releases

### APIM Extraction Tool

## ARM Template YAML pipeline

