---
title: "aaaAzure des stratégies de ressources pour les ressources réseau | Documents Microsoft"
description: "Décrit les stratégies Azure Resource Manager pour gérer le déploiement hello des ressources réseau."
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
ms.openlocfilehash: a6072c1c30db0a4e4a1cae04efc7828d14069709
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-toonetwork-resources"></a><span data-ttu-id="2dc15-103">Appliquer des ressources de toonetwork de stratégies de ressources</span><span class="sxs-lookup"><span data-stu-id="2dc15-103">Apply resource policies toonetwork resources</span></span>
<span data-ttu-id="2dc15-104">Cet article présente un exemple [stratégie de ressources](resource-manager-policy.md) vous pouvez appliquer des passerelles de réseau virtuel tooAzure.</span><span class="sxs-lookup"><span data-stu-id="2dc15-104">This article shows an example [resource policy](resource-manager-policy.md) you can apply tooAzure virtual network gateways.</span></span> <span data-ttu-id="2dc15-105">Cette stratégie garantit la cohérence pour les passerelles déployées dans votre organisation.</span><span class="sxs-lookup"><span data-stu-id="2dc15-105">This policy ensures consistency for gateways deployed in your organization.</span></span> 

## <a name="define-permitted-virtual-network-gateway-sku"></a><span data-ttu-id="2dc15-106">Définir la référence (SKU) de la passerelle de réseau virtuel autorisée</span><span class="sxs-lookup"><span data-stu-id="2dc15-106">Define permitted virtual network gateway SKU</span></span>

<span data-ttu-id="2dc15-107">Hello suivant stratégie restreint les références (SKU) peut être déployé pour les passerelles de réseau virtuel :</span><span class="sxs-lookup"><span data-stu-id="2dc15-107">hello following policy restricts which SKUs can be deployed for virtual network gateways:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="2dc15-108">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2dc15-108">Next steps</span></span>
* <span data-ttu-id="2dc15-109">Après avoir défini une règle de stratégie (comme indiqué dans hello précédents exemples), vous devez la définition de la stratégie toocreate hello et affectez tooa étendue.</span><span class="sxs-lookup"><span data-stu-id="2dc15-109">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="2dc15-110">étendue de Hello peut être un abonnement, le groupe de ressources ou la ressource.</span><span class="sxs-lookup"><span data-stu-id="2dc15-110">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="2dc15-111">stratégies tooassign via le portail de hello, voir [tooassign de portail utilisez Azure et de gérer les stratégies de ressources](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2dc15-111">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="2dc15-112">stratégies tooassign via l’API REST, PowerShell ou CLI d’Azure, consultez [affecter et gérer des stratégies dans le script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="2dc15-112">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="2dc15-113">Pour obtenir des conseils comment les entreprises peuvent utiliser le Gestionnaire de ressources tooeffectively gérer les abonnements, consultez [une vue de structure Azure enterprise - gouvernance de l’abonnement normative](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="2dc15-113">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

