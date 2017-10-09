---
title: "stratégies de ressources aaaAzure pour les comptes de stockage | Documents Microsoft"
description: "Décrit les stratégies Azure Resource Manager pour gérer le déploiement hello de comptes de stockage."
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
ms.openlocfilehash: d37fc4bcf7cdec71b0e14f6231fc138bfb6a7893
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-toostorage-accounts"></a><span data-ttu-id="2ea77-103">Appliquer des comptes de toostorage de stratégies de ressources</span><span class="sxs-lookup"><span data-stu-id="2ea77-103">Apply resource policies toostorage accounts</span></span>
<span data-ttu-id="2ea77-104">Cette rubrique montre plusieurs [stratégies de ressources](resource-manager-policy.md) vous pouvez appliquer des comptes de stockage tooAzure.</span><span class="sxs-lookup"><span data-stu-id="2ea77-104">This topic shows several [resource policies](resource-manager-policy.md) you can apply tooAzure storage accounts.</span></span> <span data-ttu-id="2ea77-105">Ces stratégies garantissent la cohérence pour les comptes de stockage hello déployé dans votre organisation.</span><span class="sxs-lookup"><span data-stu-id="2ea77-105">These policies ensure consistency for hello storage accounts deployed in your organization.</span></span> 

## <a name="define-permitted-storage-account-types"></a><span data-ttu-id="2ea77-106">Définir les types de compte de stockage autorisés</span><span class="sxs-lookup"><span data-stu-id="2ea77-106">Define permitted storage account types</span></span>

<span data-ttu-id="2ea77-107">Hello stratégie suivante restreint qui [les types de compte de stockage](../storage/common/storage-redundancy.md) peut être déployé :</span><span class="sxs-lookup"><span data-stu-id="2ea77-107">hello following policy restricts which [storage account types](../storage/common/storage-redundancy.md) can be deployed:</span></span>

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

<span data-ttu-id="2ea77-108">Une règle de stratégie similaire avec un paramètre pour l’acceptation de hello autorisé des références (SKU) est disponible en tant qu’une définition de stratégie intégré.</span><span class="sxs-lookup"><span data-stu-id="2ea77-108">A similar policy rule with a parameter for accepting hello allowed SKUs is available as a built-in policy definition.</span></span> <span data-ttu-id="2ea77-109">stratégie intégrée de Hello a hello les ID de ressource de `/providers/Microsoft.Authorization/policyDefinitions/7433c107-6db4-4ad1-b57a-a76dce0154a1`.</span><span class="sxs-lookup"><span data-stu-id="2ea77-109">hello built-in policy has hello resource ID of `/providers/Microsoft.Authorization/policyDefinitions/7433c107-6db4-4ad1-b57a-a76dce0154a1`.</span></span> 

## <a name="define-permitted-access-tier"></a><span data-ttu-id="2ea77-110">Définir le niveau d’accès autorisé</span><span class="sxs-lookup"><span data-stu-id="2ea77-110">Define permitted access tier</span></span>

<span data-ttu-id="2ea77-111">Hello stratégie suivante spécifie type hello de [couche d’accès aux](../storage/blobs/storage-blob-storage-tiers.md) qui peut être spécifiée pour les comptes de stockage :</span><span class="sxs-lookup"><span data-stu-id="2ea77-111">hello following policy specifies hello type of [access tier](../storage/blobs/storage-blob-storage-tiers.md) that can be specified for storage accounts:</span></span>

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

## <a name="ensure-encryption-is-enabled"></a><span data-ttu-id="2ea77-112">Vérifier que le chiffrement est activé</span><span class="sxs-lookup"><span data-stu-id="2ea77-112">Ensure encryption is enabled</span></span>

<span data-ttu-id="2ea77-113">Hello suivant stratégie nécessite que tous les tooenable de comptes de stockage [chiffrement de service de stockage](../storage/common/storage-service-encryption.md):</span><span class="sxs-lookup"><span data-stu-id="2ea77-113">hello following policy requires all storage accounts tooenable [Storage service encryption](../storage/common/storage-service-encryption.md):</span></span>

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

<span data-ttu-id="2ea77-114">Cette règle de stratégie est également disponible sous une définition de stratégie intégrée avec l’ID de ressource hello de `/providers/Microsoft.Authorization/policyDefinitions/7c5a74bf-ae94-4a74-8fcf-644d1e0e6e6f`.</span><span class="sxs-lookup"><span data-stu-id="2ea77-114">This policy rule is also available as a built-in policy definition with hello resource ID of `/providers/Microsoft.Authorization/policyDefinitions/7c5a74bf-ae94-4a74-8fcf-644d1e0e6e6f`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2ea77-115">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2ea77-115">Next steps</span></span>
* <span data-ttu-id="2ea77-116">Après avoir défini une règle de stratégie (comme indiqué dans hello précédents exemples), vous devez la définition de la stratégie toocreate hello et affectez tooa étendue.</span><span class="sxs-lookup"><span data-stu-id="2ea77-116">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="2ea77-117">étendue de Hello peut être un abonnement, le groupe de ressources ou la ressource.</span><span class="sxs-lookup"><span data-stu-id="2ea77-117">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="2ea77-118">stratégies tooassign via le portail de hello, voir [tooassign de portail utilisez Azure et de gérer les stratégies de ressources](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2ea77-118">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="2ea77-119">stratégies tooassign via l’API REST, PowerShell ou CLI d’Azure, consultez [affecter et gérer des stratégies dans le script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="2ea77-119">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="2ea77-120">Pour obtenir des conseils comment les entreprises peuvent utiliser le Gestionnaire de ressources tooeffectively gérer les abonnements, consultez [une vue de structure Azure enterprise - gouvernance de l’abonnement normative](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="2ea77-120">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

