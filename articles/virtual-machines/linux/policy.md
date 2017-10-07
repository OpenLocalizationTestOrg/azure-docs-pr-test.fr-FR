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
# <a name="apply-policies-toolinux-vms-with-azure-resource-manager"></a>Appliquer des stratégies tooLinux machines virtuelles avec le Gestionnaire de ressources Azure
À l’aide de stratégies, une organisation peut appliquer différentes conventions et les règles dans toute entreprise de hello. Mise en œuvre du comportement de hello souhaitée peut atténuer les risques tout en contribuant réussite toohello d’organisation de hello. Dans cet article, nous décrivons comment vous pouvez utiliser le comportement de Azure Resource Manager stratégies toodefine hello souhaité pour les ordinateurs virtuels de votre organisation.

Pour une introduction toopolicies, consultez [ressources toomanage de stratégie d’utilisation et de contrôler l’accès](../../azure-resource-manager/resource-manager-policy.md).

## <a name="permitted-virtual-machines"></a>Machines virtuelles autorisées
tooensure que les ordinateurs virtuels de votre organisation sont compatibles avec une application, vous pouvez limiter hello autorisé des systèmes d’exploitation. Bonjour stratégie l’exemple suivant, vous autorisez uniquement Ubuntu 14.04.2-LTS virtuels toobe créé.

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

Utilisez un Bonjour de toomodify génériques précédant stratégie tooallow toute image Ubuntu LTS : 

```json
{
  "field": "Microsoft.Compute/virtualMachines/imageSku",
  "like": "*LTS"
}
```

Pour plus d’informations sur les champs de la stratégie, consultez les [alias de stratégie](../../azure-resource-manager/resource-manager-policy.md#aliases).

## <a name="managed-disks"></a>Disques gérés

toorequire hello utilisation des disques gérés, hello utilisation après la stratégie :

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

## <a name="images-for-virtual-machines"></a>Images de machines virtuelles

Pour des raisons de sécurité, vous pouvez exiger que seules les images personnalisées approuvées soient déployées dans votre environnement. Vous pouvez spécifier soit groupe de ressources hello qui contient des images de hello approuvée ou des images d’approuvés spécifiques hello.

Hello, l’exemple suivant nécessite des images à partir d’un groupe de ressources approuvées :

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

Hello exemple suivant spécifie l’image hello approuvé ID :

```json
{
    "field": "Microsoft.Compute/imageId",
    "in": ["{imageId1}","{imageId2}"]
}
```

## <a name="virtual-machine-extensions"></a>Extensions de machine virtuelle

Vous souhaiterez peut-être utilisation tooforbid de certains types d’extensions. Par exemple, une extension peut ne pas être compatible avec certaines images de machines virtuelles personnalisées. Hello suivant montre l’exemple de comment tooblock une extension spécifique. Il utilise toodetermine de serveur de publication et le type qui tooblock d’extension.

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


## <a name="next-steps"></a>Étapes suivantes
* Après avoir défini une règle de stratégie (comme indiqué dans hello précédents exemples), vous devez la définition de la stratégie toocreate hello et affectez tooa étendue. étendue de Hello peut être un abonnement, le groupe de ressources ou la ressource. stratégies tooassign via le portail de hello, voir [tooassign de portail utilisez Azure et de gérer les stratégies de ressources](../../azure-resource-manager/resource-manager-policy-portal.md). stratégies tooassign via l’API REST, PowerShell ou CLI d’Azure, consultez [affecter et gérer des stratégies dans le script](../../azure-resource-manager/resource-manager-policy-create-assign.md).
* Pour un tooresource des stratégies de présentation, consultez [vue d’ensemble des stratégies de ressources](../../azure-resource-manager/resource-manager-policy.md).
* Pour obtenir des conseils comment les entreprises peuvent utiliser le Gestionnaire de ressources tooeffectively gérer les abonnements, consultez [une vue de structure Azure enterprise - gouvernance de l’abonnement normative](../../azure-resource-manager/resource-manager-subscription-governance.md).
