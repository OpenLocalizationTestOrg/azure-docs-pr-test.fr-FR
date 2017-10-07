---
title: "sécurité aaaEnforce avec des stratégies sur les machines virtuelles Linux dans Azure | Documents Microsoft"
description: "Comment tooapply un tooan stratégie une Machine virtuelle Linux Azure Resource Manager"
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 06778ab4-f8ff-4eed-ae10-26a276fc3faa
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: singhkay
ms.openlocfilehash: 5abd0c937578aba7e72b62c65b4eef9a9737aa2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="apply-policies-toolinux-vms-with-azure-resource-manager"></a><span data-ttu-id="63fdf-103">Appliquer des stratégies tooLinux machines virtuelles avec le Gestionnaire de ressources Azure</span><span class="sxs-lookup"><span data-stu-id="63fdf-103">Apply policies tooLinux VMs with Azure Resource Manager</span></span>
<span data-ttu-id="63fdf-104">À l’aide de stratégies, une organisation peut appliquer différentes conventions et les règles dans toute entreprise de hello.</span><span class="sxs-lookup"><span data-stu-id="63fdf-104">By using policies, an organization can enforce various conventions and rules throughout hello enterprise.</span></span> <span data-ttu-id="63fdf-105">Mise en œuvre du comportement de hello souhaitée peut atténuer les risques tout en contribuant réussite toohello d’organisation de hello.</span><span class="sxs-lookup"><span data-stu-id="63fdf-105">Enforcement of hello desired behavior can help mitigate risk while contributing toohello success of hello organization.</span></span> <span data-ttu-id="63fdf-106">Dans cet article, nous décrivons comment vous pouvez utiliser le comportement de Azure Resource Manager stratégies toodefine hello souhaité pour les ordinateurs virtuels de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="63fdf-106">In this article, we describe how you can use Azure Resource Manager policies toodefine hello desired behavior for your organization's Virtual Machines.</span></span>

<span data-ttu-id="63fdf-107">Pour une introduction toopolicies, consultez [ressources toomanage de stratégie d’utilisation et de contrôler l’accès](../../azure-resource-manager/resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="63fdf-107">For an introduction toopolicies, see [Use Policy toomanage resources and control access](../../azure-resource-manager/resource-manager-policy.md).</span></span>

## <a name="permitted-virtual-machines"></a><span data-ttu-id="63fdf-108">Machines virtuelles autorisées</span><span class="sxs-lookup"><span data-stu-id="63fdf-108">Permitted Virtual Machines</span></span>
<span data-ttu-id="63fdf-109">tooensure que les ordinateurs virtuels de votre organisation sont compatibles avec une application, vous pouvez limiter hello autorisé des systèmes d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="63fdf-109">tooensure that virtual machines for your organization are compatible with an application, you can restrict hello permitted operating systems.</span></span> <span data-ttu-id="63fdf-110">Bonjour stratégie l’exemple suivant, vous autorisez uniquement Ubuntu 14.04.2-LTS virtuels toobe créé.</span><span class="sxs-lookup"><span data-stu-id="63fdf-110">In hello following policy example, you allow only Ubuntu 14.04.2-LTS Virtual Machines toobe created.</span></span>

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "in": [
          "Microsoft.Compute/disks",
          "Microsoft.Compute/virtualMachines",
          "Microsoft.Compute/VirtualMachineScaleSets"
        ]
      },
      {
        "not": {
          "allOf": [
            {
              "field": "Microsoft.Compute/imagePublisher",
              "in": [
                "Canonical"
              ]
            },
            {
              "field": "Microsoft.Compute/imageOffer",
              "in": [
                "UbuntuServer"
              ]
            },
            {
              "field": "Microsoft.Compute/imageSku",
              "in": [
                "14.04.2-LTS"
              ]
            },
            {
              "field": "Microsoft.Compute/imageVersion",
              "in": [
                "latest"
              ]
            }
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

<span data-ttu-id="63fdf-111">Utilisez un Bonjour de toomodify génériques précédant stratégie tooallow toute image Ubuntu LTS :</span><span class="sxs-lookup"><span data-stu-id="63fdf-111">Use a wild card toomodify hello preceding policy tooallow any Ubuntu LTS image:</span></span> 

```json
{
  "field": "Microsoft.Compute/virtualMachines/imageSku",
  "like": "*LTS"
}
```

<span data-ttu-id="63fdf-112">Pour plus d’informations sur les champs de la stratégie, consultez les [alias de stratégie](../../azure-resource-manager/resource-manager-policy.md#aliases).</span><span class="sxs-lookup"><span data-stu-id="63fdf-112">For information about policy fields, see [Policy aliases](../../azure-resource-manager/resource-manager-policy.md#aliases).</span></span>

## <a name="managed-disks"></a><span data-ttu-id="63fdf-113">Disques gérés</span><span class="sxs-lookup"><span data-stu-id="63fdf-113">Managed disks</span></span>

<span data-ttu-id="63fdf-114">toorequire hello utilisation des disques gérés, hello utilisation après la stratégie :</span><span class="sxs-lookup"><span data-stu-id="63fdf-114">toorequire hello use of managed disks, use hello following policy:</span></span>

```json
{
  "if": {
    "anyOf": [
      {
        "allOf": [
          {
            "field": "type",
            "equals": "Microsoft.Compute/virtualMachines"
          },
          {
            "field": "Microsoft.Compute/virtualMachines/osDisk.uri",
            "exists": true
          }
        ]
      },
      {
        "allOf": [
          {
            "field": "type",
            "equals": "Microsoft.Compute/VirtualMachineScaleSets"
          },
          {
            "anyOf": [
              {
                "field": "Microsoft.Compute/VirtualMachineScaleSets/osDisk.vhdContainers",
                "exists": true
              },
              {
                "field": "Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl",
                "exists": true
              }
            ]
          }
        ]
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="images-for-virtual-machines"></a><span data-ttu-id="63fdf-115">Images de machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="63fdf-115">Images for Virtual Machines</span></span>

<span data-ttu-id="63fdf-116">Pour des raisons de sécurité, vous pouvez exiger que seules les images personnalisées approuvées soient déployées dans votre environnement.</span><span class="sxs-lookup"><span data-stu-id="63fdf-116">For security reasons, you can require that only approved custom images are deployed in your environment.</span></span> <span data-ttu-id="63fdf-117">Vous pouvez spécifier soit groupe de ressources hello qui contient des images de hello approuvée ou des images d’approuvés spécifiques hello.</span><span class="sxs-lookup"><span data-stu-id="63fdf-117">You can specify either hello resource group that contains hello approved images, or hello specific approved images.</span></span>

<span data-ttu-id="63fdf-118">Hello, l’exemple suivant nécessite des images à partir d’un groupe de ressources approuvées :</span><span class="sxs-lookup"><span data-stu-id="63fdf-118">hello following example requires images from an approved resource group:</span></span>

```json
{
    "if": {
        "allOf": [
            {
                "field": "type",
                "in": [
                    "Microsoft.Compute/virtualMachines",
                    "Microsoft.Compute/VirtualMachineScaleSets"
                ]
            },
            {
                "not": {
                    "field": "Microsoft.Compute/imageId",
                    "contains": "resourceGroups/CustomImage"
                }
            }
        ]
    },
    "then": {
        "effect": "deny"
    }
} 
```

<span data-ttu-id="63fdf-119">Hello exemple suivant spécifie l’image hello approuvé ID :</span><span class="sxs-lookup"><span data-stu-id="63fdf-119">hello following example specifies hello approved image IDs:</span></span>

```json
{
    "field": "Microsoft.Compute/imageId",
    "in": ["{imageId1}","{imageId2}"]
}
```

## <a name="virtual-machine-extensions"></a><span data-ttu-id="63fdf-120">Extensions de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="63fdf-120">Virtual Machine extensions</span></span>

<span data-ttu-id="63fdf-121">Vous souhaiterez peut-être utilisation tooforbid de certains types d’extensions.</span><span class="sxs-lookup"><span data-stu-id="63fdf-121">You may want tooforbid usage of certain types of extensions.</span></span> <span data-ttu-id="63fdf-122">Par exemple, une extension peut ne pas être compatible avec certaines images de machines virtuelles personnalisées.</span><span class="sxs-lookup"><span data-stu-id="63fdf-122">For example, an extension may not be compatible with certain custom virtual machine images.</span></span> <span data-ttu-id="63fdf-123">Hello suivant montre l’exemple de comment tooblock une extension spécifique.</span><span class="sxs-lookup"><span data-stu-id="63fdf-123">hello following example shows how tooblock a specific extension.</span></span> <span data-ttu-id="63fdf-124">Il utilise toodetermine de serveur de publication et le type qui tooblock d’extension.</span><span class="sxs-lookup"><span data-stu-id="63fdf-124">It uses publisher and type toodetermine which extension tooblock.</span></span>

```json
{
    "if": {
        "allOf": [
            {
                "field": "type",
                "equals": "Microsoft.Compute/virtualMachines/extensions"
            },
            {
                "field": "Microsoft.Compute/virtualMachines/extensions/publisher",
                "equals": "Microsoft.Compute"
            },
            {
                "field": "Microsoft.Compute/virtualMachines/extensions/type",
                "equals": "{extension-type}"

      }
        ]
    },
    "then": {
        "effect": "deny"
    }
}
```


## <a name="next-steps"></a><span data-ttu-id="63fdf-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="63fdf-125">Next steps</span></span>
* <span data-ttu-id="63fdf-126">Après avoir défini une règle de stratégie (comme indiqué dans hello précédents exemples), vous devez la définition de la stratégie toocreate hello et affectez tooa étendue.</span><span class="sxs-lookup"><span data-stu-id="63fdf-126">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="63fdf-127">étendue de Hello peut être un abonnement, le groupe de ressources ou la ressource.</span><span class="sxs-lookup"><span data-stu-id="63fdf-127">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="63fdf-128">stratégies tooassign via le portail de hello, voir [tooassign de portail utilisez Azure et de gérer les stratégies de ressources](../../azure-resource-manager/resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="63fdf-128">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](../../azure-resource-manager/resource-manager-policy-portal.md).</span></span> <span data-ttu-id="63fdf-129">stratégies tooassign via l’API REST, PowerShell ou CLI d’Azure, consultez [affecter et gérer des stratégies dans le script](../../azure-resource-manager/resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="63fdf-129">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](../../azure-resource-manager/resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="63fdf-130">Pour un tooresource des stratégies de présentation, consultez [vue d’ensemble des stratégies de ressources](../../azure-resource-manager/resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="63fdf-130">For an introduction tooresource policies, see [Resource policy overview](../../azure-resource-manager/resource-manager-policy.md).</span></span>
* <span data-ttu-id="63fdf-131">Pour obtenir des conseils comment les entreprises peuvent utiliser le Gestionnaire de ressources tooeffectively gérer les abonnements, consultez [une vue de structure Azure enterprise - gouvernance de l’abonnement normative](../../azure-resource-manager/resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="63fdf-131">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](../../azure-resource-manager/resource-manager-subscription-governance.md).</span></span>
