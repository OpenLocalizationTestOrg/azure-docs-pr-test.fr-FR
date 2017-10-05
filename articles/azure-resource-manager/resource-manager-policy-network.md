---
title: "Stratégies de ressources Azure pour les ressources réseau | Microsoft Docs"
description: "Décrit les stratégies d’Azure Resource Manager pour gérer le déploiement des ressources réseau."
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
ms.openlocfilehash: bca66bbdd9da9b3e4099d0d961f42c9368a17f5e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="apply-resource-policies-to-network-resources"></a><span data-ttu-id="f6a2d-103">Appliquer des stratégies de ressources à des ressources réseau</span><span class="sxs-lookup"><span data-stu-id="f6a2d-103">Apply resource policies to network resources</span></span>
<span data-ttu-id="f6a2d-104">Cet article présente un exemple de [stratégie de ressources](resource-manager-policy.md) que vous pouvez appliquer aux passerelles de réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="f6a2d-104">This article shows an example [resource policy](resource-manager-policy.md) you can apply to Azure virtual network gateways.</span></span> <span data-ttu-id="f6a2d-105">Cette stratégie garantit la cohérence pour les passerelles déployées dans votre organisation.</span><span class="sxs-lookup"><span data-stu-id="f6a2d-105">This policy ensures consistency for gateways deployed in your organization.</span></span> 

## <a name="define-permitted-virtual-network-gateway-sku"></a><span data-ttu-id="f6a2d-106">Définir la référence (SKU) de la passerelle de réseau virtuel autorisée</span><span class="sxs-lookup"><span data-stu-id="f6a2d-106">Define permitted virtual network gateway SKU</span></span>

<span data-ttu-id="f6a2d-107">La stratégie suivante restreint les références (SKU) qui peuvent être déployées pour les passerelles de réseau virtuel :</span><span class="sxs-lookup"><span data-stu-id="f6a2d-107">The following policy restricts which SKUs can be deployed for virtual network gateways:</span></span>

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Network/virtualNetworkGateways"
      },
      {
        "not": {
          "field": "Microsoft.Network/virtualNetworkGateways/sku.name",
          "in": [
            "Basic",
            "VpnGw1"
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

## <a name="next-steps"></a><span data-ttu-id="f6a2d-108">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f6a2d-108">Next steps</span></span>
* <span data-ttu-id="f6a2d-109">Après avoir défini une règle de stratégie (comme le montrent les exemples précédents), vous devez créer la définition de stratégie et l’attribuer à une étendue.</span><span class="sxs-lookup"><span data-stu-id="f6a2d-109">After defining a policy rule (as shown in the preceding examples), you need to create the policy definition and assign it to a scope.</span></span> <span data-ttu-id="f6a2d-110">L’étendue peut être un abonnement, un groupe de ressources ou une ressource.</span><span class="sxs-lookup"><span data-stu-id="f6a2d-110">The scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="f6a2d-111">Pour affecter des stratégies via le portail, consultez [Utiliser le portail Azure pour affecter et gérer les stratégies de ressources](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f6a2d-111">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="f6a2d-112">Pour affecter des stratégies via l’API REST, PowerShell ou Azure CLI, consultez [Affecter et gérer des stratégies via un script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="f6a2d-112">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="f6a2d-113">Pour obtenir des conseils sur l’utilisation de Resource Manager par les entreprises pour gérer efficacement les abonnements, voir [Structure d’Azure Enterprise - Gouvernance normative de l’abonnement](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="f6a2d-113">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

