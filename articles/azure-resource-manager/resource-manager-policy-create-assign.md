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
# <a name="assign-and-manage-resource-policies"></a><span data-ttu-id="bf865-103">Attribuer et gérer les stratégies de ressources</span><span class="sxs-lookup"><span data-stu-id="bf865-103">Assign and manage resource policies</span></span>

<span data-ttu-id="bf865-104">tooimplement une stratégie, vous devez effectuer ces étapes :</span><span class="sxs-lookup"><span data-stu-id="bf865-104">tooimplement a policy, you must perform these steps:</span></span>

1. <span data-ttu-id="bf865-105">Vérifiez toosee (y compris les stratégies intégrées fournies par Azure) de définitions de stratégie s’il en existe déjà dans votre abonnement qui répond à vos besoins.</span><span class="sxs-lookup"><span data-stu-id="bf865-105">Check policy definitions (including built-in policies provided by Azure) toosee if one already exists in your subscription that fulfills your requirements.</span></span>
2. <span data-ttu-id="bf865-106">S’il en existe une, obtenez son nom.</span><span class="sxs-lookup"><span data-stu-id="bf865-106">If one exists, get its name.</span></span>
3. <span data-ttu-id="bf865-107">S’il n’existe pas, définir la règle de stratégie hello avec JSON et l’ajouter en tant qu’une définition de stratégie dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="bf865-107">If one does not exist, define hello policy rule with JSON, and add it as a policy definition in your subscription.</span></span> <span data-ttu-id="bf865-108">Cette étape rend les stratégie hello disponibles pour l’attribution, mais ne s’applique pas d’abonnement de tooyour règles hello.</span><span class="sxs-lookup"><span data-stu-id="bf865-108">This step makes hello policy available for assignment but does not apply hello rules tooyour subscription.</span></span>
4. <span data-ttu-id="bf865-109">Dans les deux cas, affecter l’étendue de tooa hello stratégie (par exemple, un groupe d’abonnement ou une ressource).</span><span class="sxs-lookup"><span data-stu-id="bf865-109">For either case, assign hello policy tooa scope (such as a subscription or resource group).</span></span> <span data-ttu-id="bf865-110">les règles de stratégie de hello Hello sont désormais appliquées.</span><span class="sxs-lookup"><span data-stu-id="bf865-110">hello rules of hello policy are now enforced.</span></span>

<span data-ttu-id="bf865-111">Cet article se concentre sur hello étapes toocreate une définition de stratégie et assigner cette étendue de tooa définition via l’API REST, PowerShell ou CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="bf865-111">This article focuses on hello steps toocreate a policy definition and assign that definition tooa scope through REST API, PowerShell, or Azure CLI.</span></span> <span data-ttu-id="bf865-112">Si vous préférez des stratégies de portail tooassign toouse hello, consultez [tooassign de portail utilisez Azure et de gérer les stratégies de ressources](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="bf865-112">If you prefer toouse hello portal tooassign policies, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="bf865-113">Cet article n’aborde pas sur la syntaxe hello pour la création de définition de stratégie hello.</span><span class="sxs-lookup"><span data-stu-id="bf865-113">This article does not focus on hello syntax for creating hello policy definition.</span></span> <span data-ttu-id="bf865-114">Pour plus d’informations sur la syntaxe des stratégies, consultez la page [Vue d’ensemble des stratégies de ressources](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="bf865-114">For information about policy syntax, see [Resource policy overview](resource-manager-policy.md).</span></span>

## <a name="rest-api"></a><span data-ttu-id="bf865-115">API REST</span><span class="sxs-lookup"><span data-stu-id="bf865-115">REST API</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="bf865-116">Créer une définition de stratégie</span><span class="sxs-lookup"><span data-stu-id="bf865-116">Create policy definition</span></span>

<span data-ttu-id="bf865-117">Vous pouvez créer une stratégie avec hello [API REST pour les définitions de stratégie](/rest/api/resources/policydefinitions).</span><span class="sxs-lookup"><span data-stu-id="bf865-117">You can create a policy with hello [REST API for Policy Definitions](/rest/api/resources/policydefinitions).</span></span> <span data-ttu-id="bf865-118">Hello API REST vous toocreate et supprimer des définitions de stratégie et obtenir des informations sur les définitions existantes.</span><span class="sxs-lookup"><span data-stu-id="bf865-118">hello REST API enables you toocreate and delete policy definitions, and get information about existing definitions.</span></span>

<span data-ttu-id="bf865-119">toocreate une définition de la stratégie, exécutez :</span><span class="sxs-lookup"><span data-stu-id="bf865-119">toocreate a policy definition, run:</span></span>

```HTTP
PUT https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.authorization/policydefinitions/{policyDefinitionName}?api-version={api-version}
```

<span data-ttu-id="bf865-120">Inclure un toohello similaire de corps de demande l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="bf865-120">Include a request body similar toohello following example:</span></span>

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

### <a name="assign-policy"></a><span data-ttu-id="bf865-121">Attribuer la stratégie</span><span class="sxs-lookup"><span data-stu-id="bf865-121">Assign policy</span></span>

<span data-ttu-id="bf865-122">Vous pouvez appliquer la définition de la stratégie au niveau de portée hello souhaité via hello hello [API REST pour les attributions de stratégies](/rest/api/resources/policyassignments).</span><span class="sxs-lookup"><span data-stu-id="bf865-122">You can apply hello policy definition at hello desired scope through hello [REST API for policy assignments](/rest/api/resources/policyassignments).</span></span> <span data-ttu-id="bf865-123">Hello API REST vous toocreate et supprimer les attributions de stratégies et obtenir des informations sur les affectations existantes.</span><span class="sxs-lookup"><span data-stu-id="bf865-123">hello REST API enables you toocreate and delete policy assignments, and get information about existing assignments.</span></span>

<span data-ttu-id="bf865-124">toocreate une attribution de stratégie, exécutez :</span><span class="sxs-lookup"><span data-stu-id="bf865-124">toocreate a policy assignment, run:</span></span>

```HTTP
PUT https://management.azure.com /subscriptions/{subscription-id}/providers/Microsoft.authorization/policyassignments/{policyAssignmentName}?api-version={api-version}
```

<span data-ttu-id="bf865-125">Hello {affectation de stratégie} est le nom hello de l’attribution de stratégie hello.</span><span class="sxs-lookup"><span data-stu-id="bf865-125">hello {policy-assignment} is hello name of hello policy assignment.</span></span>

<span data-ttu-id="bf865-126">Inclure un toohello similaire de corps de demande l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="bf865-126">Include a request body similar toohello following example:</span></span>

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

### <a name="view-policy"></a><span data-ttu-id="bf865-127">Afficher la stratégie</span><span class="sxs-lookup"><span data-stu-id="bf865-127">View policy</span></span>
<span data-ttu-id="bf865-128">tooget une stratégie, utilisez hello [obtenir la définition de la stratégie](https://docs.microsoft.com/rest/api/resources/policydefinitions#PolicyDefinitions_Get) opération.</span><span class="sxs-lookup"><span data-stu-id="bf865-128">tooget a policy, use hello [Get policy definition](https://docs.microsoft.com/rest/api/resources/policydefinitions#PolicyDefinitions_Get) operation.</span></span>

### <a name="get-aliases"></a><span data-ttu-id="bf865-129">Obtenir les alias</span><span class="sxs-lookup"><span data-stu-id="bf865-129">Get aliases</span></span>
<span data-ttu-id="bf865-130">Vous pouvez récupérer des alias via hello API REST :</span><span class="sxs-lookup"><span data-stu-id="bf865-130">You can retrieve aliases through hello REST API:</span></span>

```HTTP
GET /subscriptions/{id}/providers?$expand=resourceTypes/aliases&api-version=2015-11-01
```

<span data-ttu-id="bf865-131">Bonjour à l’exemple suivant montre une définition d’un alias.</span><span class="sxs-lookup"><span data-stu-id="bf865-131">hello following example shows a definition of an alias.</span></span> <span data-ttu-id="bf865-132">Comme vous pouvez le voir, un alias définit des chemins dans différentes versions d'API, même en cas de changement de nom de propriété.</span><span class="sxs-lookup"><span data-stu-id="bf865-132">As you can see, an alias defines paths in different API versions, even when there is a property name change.</span></span> 

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

## <a name="powershell"></a><span data-ttu-id="bf865-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bf865-133">PowerShell</span></span>

<span data-ttu-id="bf865-134">Avant de procéder à des exemples de PowerShell hello, assurez-vous que vous avez [installé la version la plus récente hello](/powershell/azure/install-azurerm-ps) d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bf865-134">Before proceeding with hello PowerShell examples, make sure you have [installed hello latest version](/powershell/azure/install-azurerm-ps) of Azure PowerShell.</span></span> <span data-ttu-id="bf865-135">Les paramètres de stratégie ont été ajoutés dans la version 3.6.0.</span><span class="sxs-lookup"><span data-stu-id="bf865-135">Policy parameters were added in version 3.6.0.</span></span> <span data-ttu-id="bf865-136">Si vous avez une version antérieure, les exemples hello renvoient de qu'un erreur indiquant le paramètre hello est introuvable.</span><span class="sxs-lookup"><span data-stu-id="bf865-136">If you have an earlier version, hello examples return an error indicating hello parameter cannot be found.</span></span>

### <a name="view-policy-definitions"></a><span data-ttu-id="bf865-137">Afficher les définitions de stratégie</span><span class="sxs-lookup"><span data-stu-id="bf865-137">View policy definitions</span></span>
<span data-ttu-id="bf865-138">toosee toutes les définitions de stratégie dans votre abonnement, hello utilisation suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="bf865-138">toosee all policy definitions in your subscription, use hello following command:</span></span>

```powershell
Get-AzureRmPolicyDefinition
```

<span data-ttu-id="bf865-139">Elle renvoie toutes les définitions de stratégie disponibles, y compris les stratégies intégrées.</span><span class="sxs-lookup"><span data-stu-id="bf865-139">It returns all available policy definitions, including built-in policies.</span></span> <span data-ttu-id="bf865-140">Chaque stratégie est retourné dans hello suivant le format :</span><span class="sxs-lookup"><span data-stu-id="bf865-140">Each policy is returned in hello following format:</span></span>

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

<span data-ttu-id="bf865-141">Avant de continuer toocreate une définition de stratégie, examinez les stratégies intégrées hello.</span><span class="sxs-lookup"><span data-stu-id="bf865-141">Before proceeding toocreate a policy definition, look at hello built-in policies.</span></span> <span data-ttu-id="bf865-142">Si vous trouvez une stratégie intégrée qui applique des limites de hello que vous avez besoin, vous pouvez ignorer la création d’une définition de stratégie.</span><span class="sxs-lookup"><span data-stu-id="bf865-142">If you find a built-in policy that applies hello limits you need, you can skip creating a policy definition.</span></span> <span data-ttu-id="bf865-143">Au lieu de cela, affectez toohello souhaité étendue de la stratégie intégrée hello.</span><span class="sxs-lookup"><span data-stu-id="bf865-143">Instead, assign hello built-in policy toohello desired scope.</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="bf865-144">Créer une définition de stratégie</span><span class="sxs-lookup"><span data-stu-id="bf865-144">Create policy definition</span></span>
<span data-ttu-id="bf865-145">Vous pouvez créer une définition de stratégie à l’aide de hello `New-AzureRmPolicyDefinition` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="bf865-145">You can create a policy definition using hello `New-AzureRmPolicyDefinition` cmdlet.</span></span>

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

<span data-ttu-id="bf865-146">sortie de Hello est stockée dans un `$definition` objet, qui est utilisé lors de l’affectation de stratégie.</span><span class="sxs-lookup"><span data-stu-id="bf865-146">hello output is stored in a `$definition` object, which is used during policy assignment.</span></span> 

<span data-ttu-id="bf865-147">Plutôt que de spécifier hello JSON en tant que paramètre, vous pouvez fournir hello chemin d’accès tooa .json fichier contenant la règle de stratégie hello.</span><span class="sxs-lookup"><span data-stu-id="bf865-147">Rather than specifying hello JSON as a parameter, you can provide hello path tooa .json file containing hello policy rule.</span></span>

```powershell
$definition = New-AzureRmPolicyDefinition -Name coolAccessTier -Description "Policy toospecify access tier." -Policy "c:\policies\coolAccessTier.json"
```

<span data-ttu-id="bf865-148">Hello exemple suivant crée une définition de stratégie qui inclut des paramètres :</span><span class="sxs-lookup"><span data-stu-id="bf865-148">hello following example creates a policy definition that includes parameters:</span></span>

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

### <a name="assign-policy"></a><span data-ttu-id="bf865-149">Attribuer la stratégie</span><span class="sxs-lookup"><span data-stu-id="bf865-149">Assign policy</span></span>

<span data-ttu-id="bf865-150">Vous appliquez la stratégie de hello étendue hello souhaité à l’aide de hello `New-AzureRmPolicyAssignment` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="bf865-150">You apply hello policy at hello desired scope by using hello `New-AzureRmPolicyAssignment` cmdlet.</span></span> <span data-ttu-id="bf865-151">Hello l’exemple suivant affecte le groupe de ressources tooa hello stratégie.</span><span class="sxs-lookup"><span data-stu-id="bf865-151">hello following example assigns hello policy tooa resource group.</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
New-AzureRMPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId -PolicyDefinition $definition
```

<span data-ttu-id="bf865-152">tooassign une stratégie qui requiert des paramètres, créer et de l’objet avec ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="bf865-152">tooassign a policy that requires parameters, create and object with those values.</span></span> <span data-ttu-id="bf865-153">Hello exemple suivant récupère une stratégie intégrée et transmet les valeurs de paramètres :</span><span class="sxs-lookup"><span data-stu-id="bf865-153">hello following example retrieves a built-in policy and passes in parameters values:</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
$definition = Get-AzureRmPolicyDefinition -Id /providers/Microsoft.Authorization/policyDefinitions/e5662a6-4747-49cd-b67b-bf8b01975c4c
$array = @("West US", "West US 2")
$param = @{"listOfAllowedLocations"=$array}
New-AzureRMPolicyAssignment -Name locationAssignment -Scope $rg.ResourceId -PolicyDefinition $definition -PolicyParameterObject $param
```

### <a name="view-policy-assignment"></a><span data-ttu-id="bf865-154">Afficher l’attribution de stratégie</span><span class="sxs-lookup"><span data-stu-id="bf865-154">View policy assignment</span></span>

<span data-ttu-id="bf865-155">tooget une attribution de stratégie spécifique, utilisez :</span><span class="sxs-lookup"><span data-stu-id="bf865-155">tooget a specific policy assignment, use:</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
(Get-AzureRmPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId
```

<span data-ttu-id="bf865-156">règle de stratégie tooview hello pour une définition de stratégie, utilisez :</span><span class="sxs-lookup"><span data-stu-id="bf865-156">tooview hello policy rule for a policy definition, use:</span></span>

```powershell
(Get-AzureRmPolicyDefinition -Name coolAccessTier).Properties.policyRule | ConvertTo-Json
```

### <a name="remove-policy-assignment"></a><span data-ttu-id="bf865-157">Supprimer l’attribution de stratégie</span><span class="sxs-lookup"><span data-stu-id="bf865-157">Remove policy assignment</span></span> 

<span data-ttu-id="bf865-158">tooremove une attribution de stratégie, utilisez :</span><span class="sxs-lookup"><span data-stu-id="bf865-158">tooremove a policy assignment, use:</span></span>

```powershell
Remove-AzureRmPolicyAssignment -Name regionPolicyAssignment -Scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="azure-cli"></a><span data-ttu-id="bf865-159">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="bf865-159">Azure CLI</span></span>

### <a name="view-policy-definitions"></a><span data-ttu-id="bf865-160">Afficher les définitions de stratégie</span><span class="sxs-lookup"><span data-stu-id="bf865-160">View policy definitions</span></span>
<span data-ttu-id="bf865-161">toosee toutes les définitions de stratégie dans votre abonnement, hello utilisation suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="bf865-161">toosee all policy definitions in your subscription, use hello following command:</span></span>

```azurecli
az policy definition list
```

<span data-ttu-id="bf865-162">Elle renvoie toutes les définitions de stratégie disponibles, y compris les stratégies intégrées.</span><span class="sxs-lookup"><span data-stu-id="bf865-162">It returns all available policy definitions, including built-in policies.</span></span> <span data-ttu-id="bf865-163">Chaque stratégie est retourné dans hello suivant le format :</span><span class="sxs-lookup"><span data-stu-id="bf865-163">Each policy is returned in hello following format:</span></span>

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

<span data-ttu-id="bf865-164">Avant de continuer toocreate une définition de stratégie, examinez les stratégies intégrées hello.</span><span class="sxs-lookup"><span data-stu-id="bf865-164">Before proceeding toocreate a policy definition, look at hello built-in policies.</span></span> <span data-ttu-id="bf865-165">Si vous trouvez une stratégie intégrée qui applique des limites de hello que vous avez besoin, vous pouvez ignorer la création d’une définition de stratégie.</span><span class="sxs-lookup"><span data-stu-id="bf865-165">If you find a built-in policy that applies hello limits you need, you can skip creating a policy definition.</span></span> <span data-ttu-id="bf865-166">Au lieu de cela, affectez toohello souhaité étendue de la stratégie intégrée hello.</span><span class="sxs-lookup"><span data-stu-id="bf865-166">Instead, assign hello built-in policy toohello desired scope.</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="bf865-167">Créer une définition de stratégie</span><span class="sxs-lookup"><span data-stu-id="bf865-167">Create policy definition</span></span>

<span data-ttu-id="bf865-168">Vous pouvez créer une définition de stratégie à l’aide de CLI d’Azure avec la commande de définition de stratégie hello.</span><span class="sxs-lookup"><span data-stu-id="bf865-168">You can create a policy definition using Azure CLI with hello policy definition command.</span></span>

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

### <a name="assign-policy"></a><span data-ttu-id="bf865-169">Attribuer la stratégie</span><span class="sxs-lookup"><span data-stu-id="bf865-169">Assign policy</span></span>

<span data-ttu-id="bf865-170">Vous pouvez appliquer étendue de hello stratégie toohello souhaité à l’aide de commande de l’attribution de stratégie hello.</span><span class="sxs-lookup"><span data-stu-id="bf865-170">You can apply hello policy toohello desired scope by using hello policy assignment command.</span></span> <span data-ttu-id="bf865-171">Hello l’exemple suivant affecte à un groupe de ressources de stratégie tooa.</span><span class="sxs-lookup"><span data-stu-id="bf865-171">hello following example assigns a policy tooa resource group.</span></span>

```azurecli
az policy assignment create --name coolAccessTierAssignment --policy coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

### <a name="view-policy-assignment"></a><span data-ttu-id="bf865-172">Afficher l’attribution de stratégie</span><span class="sxs-lookup"><span data-stu-id="bf865-172">View policy assignment</span></span>

<span data-ttu-id="bf865-173">tooview une attribution de stratégie, fournir le nom de l’attribution de stratégie hello et l’étendue de hello :</span><span class="sxs-lookup"><span data-stu-id="bf865-173">tooview a policy assignment, provide hello policy assignment name and hello scope:</span></span>

```azurecli
az policy assignment show --name coolAccessTierAssignment --scope "/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}"
```

### <a name="remove-policy-assignment"></a><span data-ttu-id="bf865-174">Supprimer l’attribution de stratégie</span><span class="sxs-lookup"><span data-stu-id="bf865-174">Remove policy assignment</span></span> 

<span data-ttu-id="bf865-175">tooremove une attribution de stratégie, utilisez :</span><span class="sxs-lookup"><span data-stu-id="bf865-175">tooremove a policy assignment, use:</span></span>

```azurecli
az policy assignment delete --name coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="next-steps"></a><span data-ttu-id="bf865-176">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bf865-176">Next steps</span></span>
* <span data-ttu-id="bf865-177">Pour obtenir des conseils comment les entreprises peuvent utiliser le Gestionnaire de ressources tooeffectively gérer les abonnements, consultez [une vue de structure Azure enterprise - gouvernance de l’abonnement normative](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="bf865-177">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

