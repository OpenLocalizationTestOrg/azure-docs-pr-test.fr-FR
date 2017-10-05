---
title: "Attribuer et gérer les stratégies de ressources Azure | Microsoft Docs"
description: "Décrit comment appliquer des stratégies de ressources Azure à des abonnements et des groupes de ressources et comment afficher les stratégies de ressources."
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
ms.openlocfilehash: b204cffa8fab0ad27a9f78a81c04f0a0225d95f5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="assign-and-manage-resource-policies"></a><span data-ttu-id="d898c-103">Attribuer et gérer les stratégies de ressources</span><span class="sxs-lookup"><span data-stu-id="d898c-103">Assign and manage resource policies</span></span>

<span data-ttu-id="d898c-104">Pour implémenter une stratégie, vous devez suivre ces étapes :</span><span class="sxs-lookup"><span data-stu-id="d898c-104">To implement a policy, you must perform these steps:</span></span>

1. <span data-ttu-id="d898c-105">Vérifiez les définitions de stratégie (y compris les stratégies intégrées fournies par Azure) pour voir s’il en existe déjà une dans votre abonnement qui répond à vos besoins.</span><span class="sxs-lookup"><span data-stu-id="d898c-105">Check policy definitions (including built-in policies provided by Azure) to see if one already exists in your subscription that fulfills your requirements.</span></span>
2. <span data-ttu-id="d898c-106">S’il en existe une, obtenez son nom.</span><span class="sxs-lookup"><span data-stu-id="d898c-106">If one exists, get its name.</span></span>
3. <span data-ttu-id="d898c-107">S’il n’en existe pas, définissez la règle de stratégie avec JSON et ajoutez-la en tant que définition de stratégie dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="d898c-107">If one does not exist, define the policy rule with JSON, and add it as a policy definition in your subscription.</span></span> <span data-ttu-id="d898c-108">Cette opération rend la stratégie attribuable mais n’applique pas les règles à votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="d898c-108">This step makes the policy available for assignment but does not apply the rules to your subscription.</span></span>
4. <span data-ttu-id="d898c-109">Dans les deux cas, attribuez la stratégie à une étendue (par exemple, un groupe de ressources ou un abonnement).</span><span class="sxs-lookup"><span data-stu-id="d898c-109">For either case, assign the policy to a scope (such as a subscription or resource group).</span></span> <span data-ttu-id="d898c-110">Les règles de la stratégie sont à présent appliquées.</span><span class="sxs-lookup"><span data-stu-id="d898c-110">The rules of the policy are now enforced.</span></span>

<span data-ttu-id="d898c-111">Cet article est centré sur les étapes de création d’une définition de stratégie et d’attribution de cette définition à une étendue via l’API REST, PowerShell ou Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="d898c-111">This article focuses on the steps to create a policy definition and assign that definition to a scope through REST API, PowerShell, or Azure CLI.</span></span> <span data-ttu-id="d898c-112">Si vous préférez utiliser le portail pour affecter des stratégies, consultez [Utiliser le portail Azure pour affecter et gérer les stratégies de ressources](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d898c-112">If you prefer to use the portal to assign policies, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="d898c-113">Il n’aborde pas la syntaxe de création de la définition de stratégie.</span><span class="sxs-lookup"><span data-stu-id="d898c-113">This article does not focus on the syntax for creating the policy definition.</span></span> <span data-ttu-id="d898c-114">Pour plus d’informations sur la syntaxe des stratégies, consultez la page [Vue d’ensemble des stratégies de ressources](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="d898c-114">For information about policy syntax, see [Resource policy overview](resource-manager-policy.md).</span></span>

## <a name="rest-api"></a><span data-ttu-id="d898c-115">API REST</span><span class="sxs-lookup"><span data-stu-id="d898c-115">REST API</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="d898c-116">Créer une définition de stratégie</span><span class="sxs-lookup"><span data-stu-id="d898c-116">Create policy definition</span></span>

<span data-ttu-id="d898c-117">Vous pouvez créer une stratégie avec l’ [API REST pour les définitions de stratégies](/rest/api/resources/policydefinitions).</span><span class="sxs-lookup"><span data-stu-id="d898c-117">You can create a policy with the [REST API for Policy Definitions](/rest/api/resources/policydefinitions).</span></span> <span data-ttu-id="d898c-118">L’API REST vous permet de créer et de supprimer des définitions de stratégies, ainsi que d’obtenir des informations sur les définitions existantes.</span><span class="sxs-lookup"><span data-stu-id="d898c-118">The REST API enables you to create and delete policy definitions, and get information about existing definitions.</span></span>

<span data-ttu-id="d898c-119">Pour créer une définition de stratégie, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d898c-119">To create a policy definition, run:</span></span>

```HTTP
PUT https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.authorization/policydefinitions/{policyDefinitionName}?api-version={api-version}
```

<span data-ttu-id="d898c-120">Incluez un texte de demande semblable à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="d898c-120">Include a request body similar to the following example:</span></span>

```json
{
  "properties": {
    "parameters": {
      "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "The list of locations that can be specified when deploying resources",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
      }
    },
    "displayName": "Allowed locations",
    "description": "This policy enables you to restrict the locations your organization can specify when deploying resources.",
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

### <a name="assign-policy"></a><span data-ttu-id="d898c-121">Attribuer la stratégie</span><span class="sxs-lookup"><span data-stu-id="d898c-121">Assign policy</span></span>

<span data-ttu-id="d898c-122">Vous pouvez appliquer la définition de stratégie à l’étendue souhaitée via l’ [API REST pour les affectations de stratégies](/rest/api/resources/policyassignments).</span><span class="sxs-lookup"><span data-stu-id="d898c-122">You can apply the policy definition at the desired scope through the [REST API for policy assignments](/rest/api/resources/policyassignments).</span></span> <span data-ttu-id="d898c-123">L’API REST vous permet de créer et de supprimer des affectations de stratégies, ainsi que d’obtenir des informations sur les affectations existantes.</span><span class="sxs-lookup"><span data-stu-id="d898c-123">The REST API enables you to create and delete policy assignments, and get information about existing assignments.</span></span>

<span data-ttu-id="d898c-124">Pour créer une affectation de stratégie, exécutez :</span><span class="sxs-lookup"><span data-stu-id="d898c-124">To create a policy assignment, run:</span></span>

```HTTP
PUT https://management.azure.com /subscriptions/{subscription-id}/providers/Microsoft.authorization/policyassignments/{policyAssignmentName}?api-version={api-version}
```

<span data-ttu-id="d898c-125">{policyAssignmentName} correspond au nom de l’affectation de stratégie.</span><span class="sxs-lookup"><span data-stu-id="d898c-125">The {policy-assignment} is the name of the policy assignment.</span></span>

<span data-ttu-id="d898c-126">Incluez un texte de demande semblable à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="d898c-126">Include a request body similar to the following example:</span></span>

```json
{
  "properties":{
    "displayName":"West US only policy assignment on the subscription ",
    "description":"Resources can only be provisioned in West US regions",
    "parameters": {
      "allowedLocations": { "value": ["northeurope", "westus"] }
     },
    "policyDefinitionId":"/subscriptions/{subscription-id}/providers/Microsoft.Authorization/policyDefinitions/{definition-name}",
      "scope":"/subscriptions/{subscription-id}"
  },
}
```

### <a name="view-policy"></a><span data-ttu-id="d898c-127">Afficher la stratégie</span><span class="sxs-lookup"><span data-stu-id="d898c-127">View policy</span></span>
<span data-ttu-id="d898c-128">Pour obtenir une stratégie, utilisez l’opération [Obtenir la définition de stratégie](https://docs.microsoft.com/rest/api/resources/policydefinitions#PolicyDefinitions_Get).</span><span class="sxs-lookup"><span data-stu-id="d898c-128">To get a policy, use the [Get policy definition](https://docs.microsoft.com/rest/api/resources/policydefinitions#PolicyDefinitions_Get) operation.</span></span>

### <a name="get-aliases"></a><span data-ttu-id="d898c-129">Obtenir les alias</span><span class="sxs-lookup"><span data-stu-id="d898c-129">Get aliases</span></span>
<span data-ttu-id="d898c-130">Vous pouvez récupérer les alias avec l’API REST :</span><span class="sxs-lookup"><span data-stu-id="d898c-130">You can retrieve aliases through the REST API:</span></span>

```HTTP
GET /subscriptions/{id}/providers?$expand=resourceTypes/aliases&api-version=2015-11-01
```

<span data-ttu-id="d898c-131">L'exemple suivant montre une définition d’alias :</span><span class="sxs-lookup"><span data-stu-id="d898c-131">The following example shows a definition of an alias.</span></span> <span data-ttu-id="d898c-132">Comme vous pouvez le voir, un alias définit des chemins dans différentes versions d'API, même en cas de changement de nom de propriété.</span><span class="sxs-lookup"><span data-stu-id="d898c-132">As you can see, an alias defines paths in different API versions, even when there is a property name change.</span></span> 

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

## <a name="powershell"></a><span data-ttu-id="d898c-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d898c-133">PowerShell</span></span>

<span data-ttu-id="d898c-134">Avant de passer aux exemples PowerShell, assurez-vous que vous avez [installé la dernière version](/powershell/azure/install-azurerm-ps) d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d898c-134">Before proceeding with the PowerShell examples, make sure you have [installed the latest version](/powershell/azure/install-azurerm-ps) of Azure PowerShell.</span></span> <span data-ttu-id="d898c-135">Les paramètres de stratégie ont été ajoutés dans la version 3.6.0.</span><span class="sxs-lookup"><span data-stu-id="d898c-135">Policy parameters were added in version 3.6.0.</span></span> <span data-ttu-id="d898c-136">Si vous utilisez une version antérieure, les exemples renvoient une erreur indiquant que le paramètre est introuvable.</span><span class="sxs-lookup"><span data-stu-id="d898c-136">If you have an earlier version, the examples return an error indicating the parameter cannot be found.</span></span>

### <a name="view-policy-definitions"></a><span data-ttu-id="d898c-137">Afficher les définitions de stratégie</span><span class="sxs-lookup"><span data-stu-id="d898c-137">View policy definitions</span></span>
<span data-ttu-id="d898c-138">Pour afficher toutes les définitions de stratégie dans votre abonnement, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d898c-138">To see all policy definitions in your subscription, use the following command:</span></span>

```powershell
Get-AzureRmPolicyDefinition
```

<span data-ttu-id="d898c-139">Elle renvoie toutes les définitions de stratégie disponibles, y compris les stratégies intégrées.</span><span class="sxs-lookup"><span data-stu-id="d898c-139">It returns all available policy definitions, including built-in policies.</span></span> <span data-ttu-id="d898c-140">Chaque stratégie est renvoyée au format suivant :</span><span class="sxs-lookup"><span data-stu-id="d898c-140">Each policy is returned in the following format:</span></span>

```powershell
Name               : e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceId         : /providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceName       : e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceType       : Microsoft.Authorization/policyDefinitions
Properties         : @{displayName=Allowed locations; policyType=BuiltIn; description=This policy enables you to
                     restrict the locations your organization can specify when deploying resources. Use to enforce
                     your geo-compliance requirements.; parameters=; policyRule=}
PolicyDefinitionId : /providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c
```

<span data-ttu-id="d898c-141">Avant de passer à la création d’une définition de stratégie, examinez les stratégies intégrées.</span><span class="sxs-lookup"><span data-stu-id="d898c-141">Before proceeding to create a policy definition, look at the built-in policies.</span></span> <span data-ttu-id="d898c-142">Si vous trouvez une stratégie intégrée qui applique les limites dont vous avez besoin, vous pouvez ignorer la création d’une définition de stratégie.</span><span class="sxs-lookup"><span data-stu-id="d898c-142">If you find a built-in policy that applies the limits you need, you can skip creating a policy definition.</span></span> <span data-ttu-id="d898c-143">À la place, assignez la stratégie intégrée à l’étendue souhaitée.</span><span class="sxs-lookup"><span data-stu-id="d898c-143">Instead, assign the built-in policy to the desired scope.</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="d898c-144">Créer une définition de stratégie</span><span class="sxs-lookup"><span data-stu-id="d898c-144">Create policy definition</span></span>
<span data-ttu-id="d898c-145">Vous pouvez créer une définition de stratégie en utilisant l’applet de commande `New-AzureRmPolicyDefinition`.</span><span class="sxs-lookup"><span data-stu-id="d898c-145">You can create a policy definition using the `New-AzureRmPolicyDefinition` cmdlet.</span></span>

```powershell
$definition = New-AzureRmPolicyDefinition -Name coolAccessTier -Description "Policy to specify access tier." -Policy '{
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

<span data-ttu-id="d898c-146">Le résultat est stocké dans un objet `$definition` utilisé lors de l’attribution de la stratégie.</span><span class="sxs-lookup"><span data-stu-id="d898c-146">The output is stored in a `$definition` object, which is used during policy assignment.</span></span> 

<span data-ttu-id="d898c-147">Au lieu de spécifier le JSON comme paramètre, vous pouvez fournir le chemin d’accès à un fichier .json contenant la règle de stratégie.</span><span class="sxs-lookup"><span data-stu-id="d898c-147">Rather than specifying the JSON as a parameter, you can provide the path to a .json file containing the policy rule.</span></span>

```powershell
$definition = New-AzureRmPolicyDefinition -Name coolAccessTier -Description "Policy to specify access tier." -Policy "c:\policies\coolAccessTier.json"
```

<span data-ttu-id="d898c-148">L’exemple suivant crée une définition de stratégie qui inclut des paramètres :</span><span class="sxs-lookup"><span data-stu-id="d898c-148">The following example creates a policy definition that includes parameters:</span></span>

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
          "description": "The list of locations that can be specified when deploying storage accounts.",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
    }
}' 

$definition = New-AzureRmPolicyDefinition -Name storageLocations -Description "Policy to specify locations for storage accounts." -Policy $policy -Parameter $parameters 
```

### <a name="assign-policy"></a><span data-ttu-id="d898c-149">Attribuer la stratégie</span><span class="sxs-lookup"><span data-stu-id="d898c-149">Assign policy</span></span>

<span data-ttu-id="d898c-150">Appliquez la stratégie à l’étendue souhaitée à l’aide de la cmdlet `New-AzureRmPolicyAssignment`.</span><span class="sxs-lookup"><span data-stu-id="d898c-150">You apply the policy at the desired scope by using the `New-AzureRmPolicyAssignment` cmdlet.</span></span> <span data-ttu-id="d898c-151">L’exemple suivant assigne la stratégie à un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="d898c-151">The following example assigns the policy to a resource group.</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
New-AzureRMPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId -PolicyDefinition $definition
```

<span data-ttu-id="d898c-152">Pour assigner une stratégie qui requiert des paramètres, créez un objet avec ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="d898c-152">To assign a policy that requires parameters, create and object with those values.</span></span> <span data-ttu-id="d898c-153">L’exemple suivant récupère une stratégie intégrée et transmet les valeurs de paramètres :</span><span class="sxs-lookup"><span data-stu-id="d898c-153">The following example retrieves a built-in policy and passes in parameters values:</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
$definition = Get-AzureRmPolicyDefinition -Id /providers/Microsoft.Authorization/policyDefinitions/e5662a6-4747-49cd-b67b-bf8b01975c4c
$array = @("West US", "West US 2")
$param = @{"listOfAllowedLocations"=$array}
New-AzureRMPolicyAssignment -Name locationAssignment -Scope $rg.ResourceId -PolicyDefinition $definition -PolicyParameterObject $param
```

### <a name="view-policy-assignment"></a><span data-ttu-id="d898c-154">Afficher l’attribution de stratégie</span><span class="sxs-lookup"><span data-stu-id="d898c-154">View policy assignment</span></span>

<span data-ttu-id="d898c-155">Pour obtenir une affectation de stratégie spécifique, utilisez :</span><span class="sxs-lookup"><span data-stu-id="d898c-155">To get a specific policy assignment, use:</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
(Get-AzureRmPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId
```

<span data-ttu-id="d898c-156">Pour afficher la règle de stratégie pour une définition de stratégie, utilisez :</span><span class="sxs-lookup"><span data-stu-id="d898c-156">To view the policy rule for a policy definition, use:</span></span>

```powershell
(Get-AzureRmPolicyDefinition -Name coolAccessTier).Properties.policyRule | ConvertTo-Json
```

### <a name="remove-policy-assignment"></a><span data-ttu-id="d898c-157">Supprimer l’attribution de stratégie</span><span class="sxs-lookup"><span data-stu-id="d898c-157">Remove policy assignment</span></span> 

<span data-ttu-id="d898c-158">Pour supprimer une affectation de stratégie, utilisez :</span><span class="sxs-lookup"><span data-stu-id="d898c-158">To remove a policy assignment, use:</span></span>

```powershell
Remove-AzureRmPolicyAssignment -Name regionPolicyAssignment -Scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="azure-cli"></a><span data-ttu-id="d898c-159">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="d898c-159">Azure CLI</span></span>

### <a name="view-policy-definitions"></a><span data-ttu-id="d898c-160">Afficher les définitions de stratégie</span><span class="sxs-lookup"><span data-stu-id="d898c-160">View policy definitions</span></span>
<span data-ttu-id="d898c-161">Pour afficher toutes les définitions de stratégie dans votre abonnement, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d898c-161">To see all policy definitions in your subscription, use the following command:</span></span>

```azurecli
az policy definition list
```

<span data-ttu-id="d898c-162">Elle renvoie toutes les définitions de stratégie disponibles, y compris les stratégies intégrées.</span><span class="sxs-lookup"><span data-stu-id="d898c-162">It returns all available policy definitions, including built-in policies.</span></span> <span data-ttu-id="d898c-163">Chaque stratégie est renvoyée au format suivant :</span><span class="sxs-lookup"><span data-stu-id="d898c-163">Each policy is returned in the following format:</span></span>

```azurecli
{                                                            
  "description": "This policy enables you to restrict the locations your organization can specify when deploying resources. Use to enforce your geo-compliance requirements.",                      
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

<span data-ttu-id="d898c-164">Avant de passer à la création d’une définition de stratégie, examinez les stratégies intégrées.</span><span class="sxs-lookup"><span data-stu-id="d898c-164">Before proceeding to create a policy definition, look at the built-in policies.</span></span> <span data-ttu-id="d898c-165">Si vous trouvez une stratégie intégrée qui applique les limites dont vous avez besoin, vous pouvez ignorer la création d’une définition de stratégie.</span><span class="sxs-lookup"><span data-stu-id="d898c-165">If you find a built-in policy that applies the limits you need, you can skip creating a policy definition.</span></span> <span data-ttu-id="d898c-166">À la place, assignez la stratégie intégrée à l’étendue souhaitée.</span><span class="sxs-lookup"><span data-stu-id="d898c-166">Instead, assign the built-in policy to the desired scope.</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="d898c-167">Créer une définition de stratégie</span><span class="sxs-lookup"><span data-stu-id="d898c-167">Create policy definition</span></span>

<span data-ttu-id="d898c-168">Vous pouvez créer une définition de stratégie à l’aide d’Azure CLI avec la commande de définition de stratégie.</span><span class="sxs-lookup"><span data-stu-id="d898c-168">You can create a policy definition using Azure CLI with the policy definition command.</span></span>

```azurecli
az policy definition create --name coolAccessTier --description "Policy to specify access tier." --rules '{
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

### <a name="assign-policy"></a><span data-ttu-id="d898c-169">Attribuer la stratégie</span><span class="sxs-lookup"><span data-stu-id="d898c-169">Assign policy</span></span>

<span data-ttu-id="d898c-170">Vous pouvez appliquer la stratégie selon l’étendue de votre choix à l’aide de la commande d’affectation de stratégie.</span><span class="sxs-lookup"><span data-stu-id="d898c-170">You can apply the policy to the desired scope by using the policy assignment command.</span></span> <span data-ttu-id="d898c-171">L’exemple suivant assigne une stratégie à un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="d898c-171">The following example assigns a policy to a resource group.</span></span>

```azurecli
az policy assignment create --name coolAccessTierAssignment --policy coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

### <a name="view-policy-assignment"></a><span data-ttu-id="d898c-172">Afficher l’attribution de stratégie</span><span class="sxs-lookup"><span data-stu-id="d898c-172">View policy assignment</span></span>

<span data-ttu-id="d898c-173">Pour afficher une attribution de stratégie, fournissez le nom de l’attribution de stratégie et l’étendue :</span><span class="sxs-lookup"><span data-stu-id="d898c-173">To view a policy assignment, provide the policy assignment name and the scope:</span></span>

```azurecli
az policy assignment show --name coolAccessTierAssignment --scope "/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}"
```

### <a name="remove-policy-assignment"></a><span data-ttu-id="d898c-174">Supprimer l’attribution de stratégie</span><span class="sxs-lookup"><span data-stu-id="d898c-174">Remove policy assignment</span></span> 

<span data-ttu-id="d898c-175">Pour supprimer une affectation de stratégie, utilisez :</span><span class="sxs-lookup"><span data-stu-id="d898c-175">To remove a policy assignment, use:</span></span>

```azurecli
az policy assignment delete --name coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="next-steps"></a><span data-ttu-id="d898c-176">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d898c-176">Next steps</span></span>
* <span data-ttu-id="d898c-177">Pour obtenir des conseils sur l’utilisation de Resource Manager par les entreprises pour gérer efficacement les abonnements, voir [Structure d’Azure Enterprise - Gouvernance normative de l’abonnement](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="d898c-177">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

