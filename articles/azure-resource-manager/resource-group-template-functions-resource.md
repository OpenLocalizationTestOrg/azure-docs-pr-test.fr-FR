---
title: "fonctions de modèle de gestionnaire de ressources aaaAzure - ressources | Documents Microsoft"
description: "Décrit toouse de fonctions hello dans des valeurs de tooretrieve modèles Azure Resource Manager sur les ressources."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/09/2017
ms.author: tomfitz
ms.openlocfilehash: c9d524b338b8b7ea6d8c9e0135d48e4fb8f167c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="resource-functions-for-azure-resource-manager-templates"></a>Fonctions de ressources pour les modèles Azure Resource Manager

Gestionnaire de ressources fournit hello suivant des fonctions pour obtenir des valeurs de ressource :

* [listKeys and list{Value}](#listkeys)
* [fournisseurs](#providers)
* [reference](#reference)
* [resourceGroup](#resourcegroup)
* [resourceId](#resourceid)
* [abonnement](#subscription)

tooget les valeurs de paramètres, variables ou hello en cours de déploiement, consultez [fonctions déploiement](resource-group-template-functions-deployment.md).

<a id="listkeys" />
<a id="list" />

## <a name="listkeys-and-listvalue"></a>listKeys and list{Value}
`listKeys(resourceName or resourceIdentifier, apiVersion)`

`list{Value}(resourceName or resourceIdentifier, apiVersion)`

Retourne hello des valeurs pour n’importe quel type de ressource qui prend en charge d’opération de liste hello. est de l’utilisation la plus courante Hello `listKeys`. 

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| nom_ressource ou identificateur_ressource |Oui |string |Identificateur unique pour la ressource de hello. |
| apiVersion |Oui |string |Version d'API de l'état d'exécution des ressources. En règle générale, dans le format de hello, **aaaa-mm-jj**. |

### <a name="return-value"></a>Valeur de retour

Hello a renvoyé un objet de listKeys aura hello suivant le format :

```json
{
  "keys": [
    {
      "keyName": "key1",
      "permissions": "Full",
      "value": "{value}"
    },
    {
      "keyName": "key2",
      "permissions": "Full",
      "value": "{value}"
    }
  ]
}
```

D’autres fonctions de liste ont différents formats de retour. format de hello toosee d’une fonction, incluez-le dans la section des sorties hello comme indiqué dans l’exemple de modèle de hello. 

### <a name="remarks"></a>Remarques

Toute opération qui commence par **list** peut être utilisée en tant que fonction dans votre modèle. les opérations disponibles Hello incluent non seulement le listKeys, mais également des opérations telles que `list`, `listAdminKeys`, et `listStatus`. Toutefois, vous ne pouvez pas utiliser **liste** les opérations qui requièrent des valeurs Bonjour corps de la demande. Par exemple, hello [liste compte SAP](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS) opération nécessite des paramètres de corps de la demande, tels que *signedExpiry*, vous ne pouvez pas l’utiliser dans un modèle.

toodetermine les types de ressources dont une opération de liste, vous avez hello options suivantes :

* Hello de vue [opérations d’API REST](/rest/api/) pour un fournisseur de ressources et recherchez les opérations de liste. Par exemple, comptes de stockage se hello [listKeys opération](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys).
* Hello d’utilisation [Get-AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation) applet de commande PowerShell. Hello exemple ci-dessous obtient toutes les opérations de liste pour les comptes de stockage :

  ```powershell
  Get-AzureRmProviderOperation -OperationSearchString "Microsoft.Storage/*" | where {$_.Operation -like "*list*"} | FT Operation
  ```
* Utilisez hello commande CLI d’Azure toofilter hello uniquement les opérations de la liste suivante :

  ```azurecli
  az provider operation show --namespace Microsoft.Storage --query "resourceTypes[?name=='storageAccounts'].operations[].name | [?contains(@, 'list')]"
  ```

Spécifier les ressources hello à l’aide soit hello [fonction resourceId](#resourceid), ou le format de hello `{providerNamespace}/{resourceType}/{resourceName}`.


### <a name="example"></a>Exemple

Hello suivant montre comment tooreturn hello secondaire les clés primaires et à partir d’un compte de stockage Bonjour génère la section.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountId": {
            "type": "string"
        }
    },
    "resources": [],
    "outputs": {
        "storageKeysOutput": {
            "value": "[listKeys(parameters('storageAccountId'), '2016-01-01')]",
            "type" : "object"
        }
    }
}
``` 

<a id="providers" />

## <a name="providers"></a>fournisseurs
`providers(providerNamespace, [resourceType])`

Renvoie des informations sur un fournisseur de ressources et les types de ressources qu’il prend en charge. Si vous ne fournissez pas un type de ressource, la fonction hello retourne tous les types hello pris en charge pour le fournisseur de ressources hello.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| espacedenoms_fournisseur |Oui |string |Namespace du fournisseur de hello |
| resourceType |Non |string |type Hello de ressource dans hello spécifié l’espace de noms. |

### <a name="return-value"></a>Valeur de retour

Chaque type pris en charge est retourné dans hello suivant le format : 

```json
{
    "resourceType": "{name of resource type}",
    "locations": [ all supported locations ],
    "apiVersions": [ all supported API versions ]
}
```

Tableau classement Hello retourné de valeurs n’est pas garantie.

### <a name="example"></a>Exemple

Bonjour à l’exemple suivant montre comment toouse hello fonction du fournisseur :

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "providerOutput": {
            "value": "[providers('Microsoft.Web', 'sites')]",
            "type" : "object"
        }
    }
}
```

Hello exemple précédent retourne un objet Bonjour suivant le format :

```json
{
  "resourceType": "sites",
  "locations": [
    "South Central US",
    "North Europe",
    "West Europe",
    "Southeast Asia",
    ...
  ],
  "apiVersions": [
    "2016-08-01",
    "2016-03-01",
    "2015-08-01-preview",
    "2015-08-01",
    ...
  ]
}
```

<a id="reference" />

## <a name="reference"></a>reference
`reference(resourceName or resourceIdentifier, [apiVersion])`

Renvoie un objet représentant l’état d’exécution d’une ressource.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| nom_ressource ou identificateur_ressource |Oui |string |Nom ou identificateur unique d’une ressource. |
| apiVersion |Non |string |Version de l’API de hello la ressource spécifiée. Incluez ce paramètre lors de la ressource de hello n’est pas configuré dans le même modèle. En règle générale, dans le format de hello, **aaaa-mm-jj**. |

### <a name="return-value"></a>Valeur de retour

Chaque type de ressource retourne des propriétés différentes pour la fonction de référence hello. fonction Hello ne retourne pas un format unique, prédéfini. propriétés de hello toosee pour un type de ressource, retourner objet hello Bonjour génère section comme indiqué dans l’exemple de hello.

### <a name="remarks"></a>Remarques

référence de fonction Hello dérive sa valeur à partir d’un état d’exécution et ne peut donc pas être utilisé dans la section des variables hello. Elle peut être utilisée dans la section outputs d'un modèle. 

À l’aide de référence de fonction hello, vous déclarez implicitement qu’une ressource dépend d’une autre ressource, si les ressources hello référencé sont configuré au sein du même modèle. Vous n’avez pas besoin de la propriété : dependsOn de tooalso utiliser hello. Hello fonction n’est pas été évaluée jusqu'à hello ressource référencée fin de déploiement.

toosee hello noms et valeurs pour un type de ressource, créez un modèle qui retourne un objet de hello dans la section des sorties hello. Si vous disposez d’une ressource de ce type, votre modèle retourne les objet hello sans déployer toutes les nouvelles ressources. 

En général, vous utilisez hello **référence** tooreturn une valeur particulière d’un objet, tel que du point de terminaison hello blob URI ou le nom de domaine complet de la fonction.

```json
"outputs": {
    "BlobUri": {
        "value": "[reference(concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName')), '2016-01-01').primaryEndpoints.blob]",
        "type" : "string"
    },
    "FQDN": {
        "value": "[reference(concat('Microsoft.Network/publicIPAddresses/', parameters('ipAddressName')), '2016-03-30').dnsSettings.fqdn]",
        "type" : "string"
    }
}
```

### <a name="example"></a>Exemple

Guide de référence et toodeploy ressource hello Bonjour même modèle, utilisez :

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
      "storageAccountName": { 
          "type": "string"
      }
  },
  "resources": [
    {
      "name": "[parameters('storageAccountName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-12-01",
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {
      }
    }
  ],
  "outputs": {
      "referenceOutput": {
          "type": "object",
          "value": "[reference(parameters('storageAccountName'))]"
      }
    }
}
``` 

Hello exemple précédent retourne un objet Bonjour suivant le format :

```json
{
   "creationTime": "2017-06-13T21:24:46.618364Z",
   "primaryEndpoints": {
     "blob": "https://examplestorage.blob.core.windows.net/",
     "file": "https://examplestorage.file.core.windows.net/",
     "queue": "https://examplestorage.queue.core.windows.net/",
     "table": "https://examplestorage.table.core.windows.net/"
   },
   "primaryLocation": "southcentralus",
   "provisioningState": "Succeeded",
   "statusOfPrimary": "available",
   "supportsHttpsTrafficOnly": false
}
```

Hello exemple suivant fait référence à un compte de stockage qui n’est pas déployé dans ce modèle. Hello compte de stockage existe déjà dans hello même groupe de ressources.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountName": {
            "type": "string"
        }
    },
    "resources": [],
    "outputs": {
        "ExistingStorage": {
            "value": "[reference(concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName')), '2016-01-01')]",
            "type" : "object"
        }
    }
}
```

<a id="resourcegroup" />

## <a name="resourcegroup"></a>resourceGroup
`resourceGroup()`

Retourne un objet qui représente le groupe de ressources actuel hello. 

### <a name="return-value"></a>Valeur de retour

Hello retournée objet est Bonjour suivant le format :

```json
{
  "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}",
  "name": "{resourceGroupName}",
  "location": "{resourceGroupLocation}",
  "tags": {
  },
  "properties": {
    "provisioningState": "{status}"
  }
}
```

### <a name="remarks"></a>Remarques

Une utilisation courante de la fonction du groupe de ressources hello est ressources toocreate Bonjour même emplacement que le groupe de ressources hello. Hello exemple suivant utilise hello ressource groupe emplacement tooassign hello emplacement pour un site web.

```json
"resources": [
   {
      "apiVersion": "2016-08-01",
      "type": "Microsoft.Web/sites",
      "name": "[parameters('siteName')]",
      "location": "[resourceGroup().location]",
      ...
   }
]
```

### <a name="example"></a>Exemple

Hello modèle suivant retourne les propriétés hello hello du groupe de ressources.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[resourceGroup()]",
            "type" : "object"
        }
    }
}
```

Hello exemple précédent retourne un objet Bonjour suivant le format :

```json
{
  "id": "/subscriptions/{subscription-id}/resourceGroups/examplegroup",
  "name": "examplegroup",
  "location": "southcentralus",
  "properties": {
    "provisioningState": "Succeeded"
  }
}
```

<a id="resourceid" />

## <a name="resourceid"></a>resourceId
`resourceId([subscriptionId], [resourceGroupName], resourceType, resourceName1, [resourceName2]...)`

Retourne hello identificateur unique d’une ressource. Vous utilisez cette fonction lorsque le nom de la ressource hello est ambigu ou non configuré dans hello même modèle. 

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| subscriptionId |Non |string (au format GUID) |Valeur par défaut est un abonnement hello. Spécifiez cette valeur lorsque vous avez besoin de tooretrieve une ressource dans un autre abonnement. |
| resourceGroupName |Non |string |La valeur par défaut est le groupe de ressources actuel. Spécifiez cette valeur lorsque vous avez besoin de tooretrieve une ressource dans un autre groupe de ressources. |
| resourceType |Oui |string |Type de ressource, y compris l'espace de noms du fournisseur de ressources. |
| nom_ressource1 |Oui |string |Nom de la ressource. |
| nom_ressource2 |Non |string |Segment de nom de ressource suivant si la ressource est imbriquée. |

### <a name="return-value"></a>Valeur de retour

identificateur de Hello est retourné dans hello suivant le format :

```json
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{resourceType}/{resourceName}
```

### <a name="remarks"></a>Remarques

Hello des valeurs de paramètre que vous spécifiez dépendent de la ressource de hello Bonjour même groupe d’abonnement et de ressources en tant que déploiement hello en cours.

ID de ressource de hello tooget pour un compte de stockage Bonjour même abonnement et le groupe de ressources, utilisez :

```json
"[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]"
```

ID de ressource tooget hello pour un compte de stockage dans hello même abonnement, mais d’un autre groupe de ressources, utilisez :

```json
"[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

ID de ressource tooget hello pour un compte de stockage dans un autre abonnement et le groupe de ressources, utilisez :

```json
"[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

ID de ressource tooget hello pour une base de données dans un autre groupe de ressources, utilisez :

```json
"[resourceId('otherResourceGroup', 'Microsoft.SQL/servers/databases', parameters('serverName'), parameters('databaseName'))]"
```

Vous devez souvent toouse cette fonction lorsque vous utilisez un compte de stockage ou d’un réseau virtuel dans un groupe de ressources différent. Hello exemple suivant montre comment une ressource à partir d’un groupe de ressources externes peut facilement être utilisée :

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
      "virtualNetworkName": {
          "type": "string"
      },
      "virtualNetworkResourceGroup": {
          "type": "string"
      },
      "subnet1Name": {
          "type": "string"
      },
      "nicName": {
          "type": "string"
      }
  },
  "variables": {
      "vnetID": "[resourceId(parameters('virtualNetworkResourceGroup'), 'Microsoft.Network/virtualNetworks', parameters('virtualNetworkName'))]",
      "subnet1Ref": "[concat(variables('vnetID'),'/subnets/', parameters('subnet1Name'))]"
  },
  "resources": [
  {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[parameters('nicName')]",
      "location": "[parameters('location')]",
      "properties": {
          "ipConfigurations": [{
              "name": "ipconfig1",
              "properties": {
                  "privateIPAllocationMethod": "Dynamic",
                  "subnet": {
                      "id": "[variables('subnet1Ref')]"
                  }
              }
          }]
       }
  }]
}
```

### <a name="example"></a>Exemple

Hello exemple suivant renvoie les ID de ressource hello pour un compte de stockage dans le groupe de ressources hello :

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "sameRGOutput": {
            "value": "[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "differentRGOutput": {
            "value": "[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "differentSubOutput": {
            "value": "[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "nestedResourceOutput": {
            "value": "[resourceId('Microsoft.SQL/servers/databases', 'serverName', 'databaseName')]",
            "type" : "string"
        }
    }
}
```

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| sameRGOutput | String | /subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageAccounts/examplestorage |
| differentRGOutput | String | /subscriptions/{current-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage |
| differentSubOutput | String | /subscriptions/{different-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage |
| nestedResourceOutput | String | /subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.SQL/servers/serverName/databases/databaseName |

<a id="subscription" />

## <a name="subscription"></a>abonnement
`subscription()`

Retourne le plus d’informations sur l’abonnement hello pour le déploiement en cours de hello. 

### <a name="return-value"></a>Valeur de retour

fonction Hello renvoie hello suivant le format :

```json
{
    "id": "/subscriptions/{subscription-id}",
    "subscriptionId": "{subscription-id}",
    "tenantId": "{tenant-id}",
    "displayName": "{name-of-subscription}"
}
```

### <a name="example"></a>Exemple

Hello exemple suivant illustre hello abonnement fonction est appelée dans la section des sorties hello. 

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[subscription()]",
            "type" : "object"
        }
    }
}
```

## <a name="next-steps"></a>Étapes suivantes
* Pour obtenir une description des sections de hello dans un modèle Azure Resource Manager, consultez [les modèles de programmation Azure Resource Manager](resource-group-authoring-templates.md).
* consultez de plusieurs modèles toomerge [à l’aide de modèles liés avec Azure Resource Manager](resource-group-linked-templates.md).
* tooiterate un nombre spécifié de fois lors de la création d’un type de ressource, consultez [créer plusieurs instances de ressources dans Azure Resource Manager](resource-group-create-multiple.md).
* toosee modèle de hello toodeploy que vous avez créé, voir [déployer une application avec le modèle Azure Resource Manager](resource-group-template-deploy.md).

