---
title: "Stratégies de ressources Azure pour les comptes de stockage | Microsoft Docs"
description: "Décrit les stratégies d’Azure Resource Manager pour gérer le déploiement de comptes de stockage."
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
ms.date: 07/05/2017
ms.author: tomfitz
ms.openlocfilehash: 6612ee61f5c50e743241b92030660cea7ae7094d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="apply-resource-policies-to-storage-accounts"></a><span data-ttu-id="704cd-103">Appliquer des stratégies de ressources à des comptes de stockage</span><span class="sxs-lookup"><span data-stu-id="704cd-103">Apply resource policies to storage accounts</span></span>
<span data-ttu-id="704cd-104">Cette rubrique montre plusieurs [stratégies de ressources](resource-manager-policy.md) que vous pouvez appliquer aux comptes de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="704cd-104">This topic shows several [resource policies](resource-manager-policy.md) you can apply to Azure storage accounts.</span></span> <span data-ttu-id="704cd-105">Ces stratégies garantissent la cohérence entre les comptes de stockage déployés dans votre organisation.</span><span class="sxs-lookup"><span data-stu-id="704cd-105">These policies ensure consistency for the storage accounts deployed in your organization.</span></span> 

## <a name="define-permitted-storage-account-types"></a><span data-ttu-id="704cd-106">Définir les types de compte de stockage autorisés</span><span class="sxs-lookup"><span data-stu-id="704cd-106">Define permitted storage account types</span></span>

<span data-ttu-id="704cd-107">La stratégie suivante restreint les [types de compte de stockage](../storage/common/storage-redundancy.md) qu’il est possible de déployer :</span><span class="sxs-lookup"><span data-stu-id="704cd-107">The following policy restricts which [storage account types](../storage/common/storage-redundancy.md) can be deployed:</span></span>

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/sku.name",
          "in": [
            "Standard_LRS",
            "Standard_GRS"
          ]
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

<span data-ttu-id="704cd-108">Une règle de stratégie similaire avec un paramètre permettant d’accepter les références SKU autorisées est disponible sous la forme d’une définition de stratégie prédéfinie.</span><span class="sxs-lookup"><span data-stu-id="704cd-108">A similar policy rule with a parameter for accepting the allowed SKUs is available as a built-in policy definition.</span></span> <span data-ttu-id="704cd-109">La stratégie prédéfinie possède l’ID de ressource `/providers/Microsoft.Authorization/policyDefinitions/7433c107-6db4-4ad1-b57a-a76dce0154a1`.</span><span class="sxs-lookup"><span data-stu-id="704cd-109">The built-in policy has the resource ID of `/providers/Microsoft.Authorization/policyDefinitions/7433c107-6db4-4ad1-b57a-a76dce0154a1`.</span></span> 

## <a name="define-permitted-access-tier"></a><span data-ttu-id="704cd-110">Définir le niveau d’accès autorisé</span><span class="sxs-lookup"><span data-stu-id="704cd-110">Define permitted access tier</span></span>

<span data-ttu-id="704cd-111">La stratégie suivante spécifie le type de [niveau d’accès](../storage/blobs/storage-blob-storage-tiers.md) qu’il est possible de spécifier pour les comptes de stockage :</span><span class="sxs-lookup"><span data-stu-id="704cd-111">The following policy specifies the type of [access tier](../storage/blobs/storage-blob-storage-tiers.md) that can be specified for storage accounts:</span></span>

```json
{
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
}
```

## <a name="ensure-encryption-is-enabled"></a><span data-ttu-id="704cd-112">Vérifier que le chiffrement est activé</span><span class="sxs-lookup"><span data-stu-id="704cd-112">Ensure encryption is enabled</span></span>

<span data-ttu-id="704cd-113">La stratégie suivante requiert que tous les comptes de stockage activent le [chiffrement des services de stockage](../storage/common/storage-service-encryption.md) :</span><span class="sxs-lookup"><span data-stu-id="704cd-113">The following policy requires all storage accounts to enable [Storage service encryption](../storage/common/storage-service-encryption.md):</span></span>

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/enableBlobEncryption",
          "equals": "true"
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

<span data-ttu-id="704cd-114">Cette règle de stratégie est également disponible sous forme de définition de stratégie prédéfinie avec l’ID de ressource `/providers/Microsoft.Authorization/policyDefinitions/7c5a74bf-ae94-4a74-8fcf-644d1e0e6e6f`.</span><span class="sxs-lookup"><span data-stu-id="704cd-114">This policy rule is also available as a built-in policy definition with the resource ID of `/providers/Microsoft.Authorization/policyDefinitions/7c5a74bf-ae94-4a74-8fcf-644d1e0e6e6f`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="704cd-115">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="704cd-115">Next steps</span></span>
* <span data-ttu-id="704cd-116">Après avoir défini une règle de stratégie (comme le montrent les exemples précédents), vous devez créer la définition de stratégie et l’attribuer à une étendue.</span><span class="sxs-lookup"><span data-stu-id="704cd-116">After defining a policy rule (as shown in the preceding examples), you need to create the policy definition and assign it to a scope.</span></span> <span data-ttu-id="704cd-117">L’étendue peut être un abonnement, un groupe de ressources ou une ressource.</span><span class="sxs-lookup"><span data-stu-id="704cd-117">The scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="704cd-118">Pour affecter des stratégies via le portail, consultez [Utiliser le portail Azure pour affecter et gérer les stratégies de ressources](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="704cd-118">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="704cd-119">Pour affecter des stratégies via l’API REST, PowerShell ou Azure CLI, consultez [Affecter et gérer des stratégies via un script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="704cd-119">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="704cd-120">Pour obtenir des conseils sur l’utilisation de Resource Manager par les entreprises pour gérer efficacement les abonnements, voir [Structure d’Azure Enterprise - Gouvernance normative de l’abonnement](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="704cd-120">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

