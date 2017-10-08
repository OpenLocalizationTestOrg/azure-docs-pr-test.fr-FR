---
title: "aaaAssign et gérer des stratégies de ressources Azure | Documents Microsoft"
description: "Décrit comment tooapply stratégies toosubscriptions et ressources groupes de ressources Azure et comment les stratégies de ressources tooview."
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
ms.date: 07/26/2017
ms.author: tomfitz
ms.openlocfilehash: b6999b43bbcc80d2fde9911352fd4352fa453443
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-and-manage-resource-policies"></a>Attribuer et gérer les stratégies de ressources

tooimplement une stratégie, vous devez effectuer ces étapes :

1. Vérifiez toosee (y compris les stratégies intégrées fournies par Azure) de définitions de stratégie s’il en existe déjà dans votre abonnement qui répond à vos besoins.
2. S’il en existe une, obtenez son nom.
3. S’il n’existe pas, définir la règle de stratégie hello avec JSON et l’ajouter en tant qu’une définition de stratégie dans votre abonnement. Cette étape rend les stratégie hello disponibles pour l’attribution, mais ne s’applique pas d’abonnement de tooyour règles hello.
4. Dans les deux cas, affecter l’étendue de tooa hello stratégie (par exemple, un groupe d’abonnement ou une ressource). les règles de stratégie de hello Hello sont désormais appliquées.

Cet article se concentre sur hello étapes toocreate une définition de stratégie et assigner cette étendue de tooa définition via l’API REST, PowerShell ou CLI d’Azure. Si vous préférez des stratégies de portail tooassign toouse hello, consultez [tooassign de portail utilisez Azure et de gérer les stratégies de ressources](resource-manager-policy-portal.md). Cet article n’aborde pas sur la syntaxe hello pour la création de définition de stratégie hello. Pour plus d’informations sur la syntaxe des stratégies, consultez la page [Vue d’ensemble des stratégies de ressources](resource-manager-policy.md).

## <a name="rest-api"></a>API REST

### <a name="create-policy-definition"></a>Créer une définition de stratégie

Vous pouvez créer une stratégie avec hello [API REST pour les définitions de stratégie](/rest/api/resources/policydefinitions). Hello API REST vous toocreate et supprimer des définitions de stratégie et obtenir des informations sur les définitions existantes.

toocreate une définition de la stratégie, exécutez :

```HTTP
PUT https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.authorization/policydefinitions/{policyDefinitionName}?api-version={api-version}
```

Inclure un toohello similaire de corps de demande l’exemple suivant :

```json
{
  "properties": {
    "parameters": {
      "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "hello list of locations that can be specified when deploying resources",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
      }
    },
    "displayName": "Allowed locations",
    "description": "This policy enables you toorestrict hello locations your organization can specify when deploying resources.",
    "policyRule": {
      "if": {
        "not": {
          "field": "location",
          "in": "[parameters('allowedLocations')]"
        }
      },
      "then": {
        "effect": "deny"
      }
    }
  }
}
```

### <a name="assign-policy"></a>Attribuer la stratégie

Vous pouvez appliquer la définition de la stratégie au niveau de portée hello souhaité via hello hello [API REST pour les attributions de stratégies](/rest/api/resources/policyassignments). Hello API REST vous toocreate et supprimer les attributions de stratégies et obtenir des informations sur les affectations existantes.

toocreate une attribution de stratégie, exécutez :

```HTTP
PUT https://management.azure.com /subscriptions/{subscription-id}/providers/Microsoft.authorization/policyassignments/{policyAssignmentName}?api-version={api-version}
```

Hello {affectation de stratégie} est le nom hello de l’attribution de stratégie hello.

Inclure un toohello similaire de corps de demande l’exemple suivant :

```json
{
  "properties":{
    "displayName":"West US only policy assignment on hello subscription ",
    "description":"Resources can only be provisioned in West US regions",
    "parameters": {
      "allowedLocations": { "value": ["northeurope", "westus"] }
     },
    "policyDefinitionId":"/subscriptions/{subscription-id}/providers/Microsoft.Authorization/policyDefinitions/{definition-name}",
      "scope":"/subscriptions/{subscription-id}"
  },
}
```

### <a name="view-policy"></a>Afficher la stratégie
tooget une stratégie, utilisez hello [obtenir la définition de la stratégie](https://docs.microsoft.com/rest/api/resources/policydefinitions#PolicyDefinitions_Get) opération.

### <a name="get-aliases"></a>Obtenir les alias
Vous pouvez récupérer des alias via hello API REST :

```HTTP
GET /subscriptions/{id}/providers?$expand=resourceTypes/aliases&api-version=2015-11-01
```

Bonjour à l’exemple suivant montre une définition d’un alias. Comme vous pouvez le voir, un alias définit des chemins dans différentes versions d'API, même en cas de changement de nom de propriété. 

```json
"aliases": [
    {
      "name": "Microsoft.Storage/storageAccounts/sku.name",
      "paths": [
        {
          "path": "properties.accountType",
          "apiVersions": [
            "2015-06-15",
            "2015-05-01-preview"
          ]
        },
        {
          "path": "sku.name",
          "apiVersions": [
            "2016-01-01"
          ]
        }
      ]
    }
]
```

## <a name="powershell"></a>PowerShell

Avant de procéder à des exemples de PowerShell hello, assurez-vous que vous avez [installé la version la plus récente hello](/powershell/azure/install-azurerm-ps) d’Azure PowerShell. Les paramètres de stratégie ont été ajoutés dans la version 3.6.0. Si vous avez une version antérieure, les exemples hello renvoient de qu'un erreur indiquant le paramètre hello est introuvable.

### <a name="view-policy-definitions"></a>Afficher les définitions de stratégie
toosee toutes les définitions de stratégie dans votre abonnement, hello utilisation suivant de commandes :

```powershell
Get-AzureRmPolicyDefinition
```

Elle renvoie toutes les définitions de stratégie disponibles, y compris les stratégies intégrées. Chaque stratégie est retourné dans hello suivant le format :

```powershell
Name               : e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceId         : /providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceName       : e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceType       : Microsoft.Authorization/policyDefinitions
Properties         : @{displayName=Allowed locations; policyType=BuiltIn; description=This policy enables you to
                     restrict hello locations your organization can specify when deploying resources. Use tooenforce
                     your geo-compliance requirements.; parameters=; policyRule=}
PolicyDefinitionId : /providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c
```

Avant de continuer toocreate une définition de stratégie, examinez les stratégies intégrées hello. Si vous trouvez une stratégie intégrée qui applique des limites de hello que vous avez besoin, vous pouvez ignorer la création d’une définition de stratégie. Au lieu de cela, affectez toohello souhaité étendue de la stratégie intégrée hello.

### <a name="create-policy-definition"></a>Créer une définition de stratégie
Vous pouvez créer une définition de stratégie à l’aide de hello `New-AzureRmPolicyDefinition` applet de commande.

```powershell
$definition = New-AzureRmPolicyDefinition -Name coolAccessTier -Description "Policy toospecify access tier." -Policy '{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "field": "kind",
        "equals": "BlobStorage"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/accessTier",
          "equals": "cool"
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}'
```            

sortie de Hello est stockée dans un `$definition` objet, qui est utilisé lors de l’affectation de stratégie. 

Plutôt que de spécifier hello JSON en tant que paramètre, vous pouvez fournir hello chemin d’accès tooa .json fichier contenant la règle de stratégie hello.

```powershell
$definition = New-AzureRmPolicyDefinition -Name coolAccessTier -Description "Policy toospecify access tier." -Policy "c:\policies\coolAccessTier.json"
```

Hello exemple suivant crée une définition de stratégie qui inclut des paramètres :

```powershell
$policy = '{
    "if": {
        "allOf": [
            {
                "field": "type",
                "equals": "Microsoft.Storage/storageAccounts"
            },
            {
                "not": {
                    "field": "location",
                    "in": "[parameters(''allowedLocations'')]"
                }
            }
        ]
    },
    "then": {
        "effect": "Deny"
    }
}'

$parameters = '{
    "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "hello list of locations that can be specified when deploying storage accounts.",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
    }
}' 

$definition = New-AzureRmPolicyDefinition -Name storageLocations -Description "Policy toospecify locations for storage accounts." -Policy $policy -Parameter $parameters 
```

### <a name="assign-policy"></a>Attribuer la stratégie

Vous appliquez la stratégie de hello étendue hello souhaité à l’aide de hello `New-AzureRmPolicyAssignment` applet de commande. Hello l’exemple suivant affecte le groupe de ressources tooa hello stratégie.

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
New-AzureRMPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId -PolicyDefinition $definition
```

tooassign une stratégie qui requiert des paramètres, créer et de l’objet avec ces valeurs. Hello exemple suivant récupère une stratégie intégrée et transmet les valeurs de paramètres :

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
$definition = Get-AzureRmPolicyDefinition -Id /providers/Microsoft.Authorization/policyDefinitions/e5662a6-4747-49cd-b67b-bf8b01975c4c
$array = @("West US", "West US 2")
$param = @{"listOfAllowedLocations"=$array}
New-AzureRMPolicyAssignment -Name locationAssignment -Scope $rg.ResourceId -PolicyDefinition $definition -PolicyParameterObject $param
```

### <a name="view-policy-assignment"></a>Afficher l’attribution de stratégie

tooget une attribution de stratégie spécifique, utilisez :

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
(Get-AzureRmPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId
```

règle de stratégie tooview hello pour une définition de stratégie, utilisez :

```powershell
(Get-AzureRmPolicyDefinition -Name coolAccessTier).Properties.policyRule | ConvertTo-Json
```

### <a name="remove-policy-assignment"></a>Supprimer l’attribution de stratégie 

tooremove une attribution de stratégie, utilisez :

```powershell
Remove-AzureRmPolicyAssignment -Name regionPolicyAssignment -Scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="azure-cli"></a>Interface de ligne de commande Azure

### <a name="view-policy-definitions"></a>Afficher les définitions de stratégie
toosee toutes les définitions de stratégie dans votre abonnement, hello utilisation suivant de commandes :

```azurecli
az policy definition list
```

Elle renvoie toutes les définitions de stratégie disponibles, y compris les stratégies intégrées. Chaque stratégie est retourné dans hello suivant le format :

```azurecli
{                                                            
  "description": "This policy enables you toorestrict hello locations your organization can specify when deploying resources. Use tooenforce your geo-compliance requirements.",                      
  "displayName": "Allowed locations",
  "id": "/providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c",
  "name": "e56962a6-4747-49cd-b67b-bf8b01975c4c",
  "policyRule": {
    "if": {
      "not": {
        "field": "location",
        "in": "[parameters('listOfAllowedLocations')]"
      }
    },
    "then": {
      "effect": "Deny"
    }
  },
  "policyType": "BuiltIn"
}
```

Avant de continuer toocreate une définition de stratégie, examinez les stratégies intégrées hello. Si vous trouvez une stratégie intégrée qui applique des limites de hello que vous avez besoin, vous pouvez ignorer la création d’une définition de stratégie. Au lieu de cela, affectez toohello souhaité étendue de la stratégie intégrée hello.

### <a name="create-policy-definition"></a>Créer une définition de stratégie

Vous pouvez créer une définition de stratégie à l’aide de CLI d’Azure avec la commande de définition de stratégie hello.

```azurecli
az policy definition create --name coolAccessTier --description "Policy toospecify access tier." --rules '{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "field": "kind",
        "equals": "BlobStorage"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/accessTier",
          "equals": "cool"
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}'    
```

### <a name="assign-policy"></a>Attribuer la stratégie

Vous pouvez appliquer étendue de hello stratégie toohello souhaité à l’aide de commande de l’attribution de stratégie hello. Hello l’exemple suivant affecte à un groupe de ressources de stratégie tooa.

```azurecli
az policy assignment create --name coolAccessTierAssignment --policy coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

### <a name="view-policy-assignment"></a>Afficher l’attribution de stratégie

tooview une attribution de stratégie, fournir le nom de l’attribution de stratégie hello et l’étendue de hello :

```azurecli
az policy assignment show --name coolAccessTierAssignment --scope "/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}"
```

### <a name="remove-policy-assignment"></a>Supprimer l’attribution de stratégie 

tooremove une attribution de stratégie, utilisez :

```azurecli
az policy assignment delete --name coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="next-steps"></a>Étapes suivantes
* Pour obtenir des conseils comment les entreprises peuvent utiliser le Gestionnaire de ressources tooeffectively gérer les abonnements, consultez [une vue de structure Azure enterprise - gouvernance de l’abonnement normative](resource-manager-subscription-governance.md).

