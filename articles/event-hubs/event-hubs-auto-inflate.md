---
title: "échelle aaaAutomatically unités de débit Azure Event Hubs | Documents Microsoft"
description: "Activer augmentation automatique sur une échelle de tooautomatically d’espace de noms des unités de débit"
services: event-hubs
documentationcenter: na
author: ShubhaVijayasarathy
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: shvija;sethm
ms.openlocfilehash: 0f5216bcd619ccddc1fd4063a2f0131bfa36c7d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-scale-up-azure-event-hubs-throughput-units"></a>Mettre automatiquement à l’échelle les unités de débit Azure Event Hubs

## <a name="overview"></a>Vue d'ensemble

Azure Event Hubs est une plateforme hautement évolutive de diffusion de données en continu. Par conséquent, les clients de concentrateurs d’événements augmentent souvent leur utilisation après l’intégration toohello service. Ces augmente besoin croissant hello prédéterminé débit unités (état) tooscale concentrateurs d’événements et gérer des débits de transfert plus grandes. Hello *Auto-valeur de l’augmentation* s’ajuste automatiquement la fonctionnalité du service Event Hubs numéro hello besoins en matière d’utilisation de toomeet up. L’augmentation du nombre d’unités de débit vous empêche d’être confronté à des scénarios de limitation, dans lesquels :

* Les taux d’entrée des données sont supérieurs aux unités de débit définies.
* Les taux de demande de sortie des données sont supérieurs aux unités de débit définies.

## <a name="how-auto-inflate-works"></a>Fonctionnement de la majoration automatique

Le trafic Event Hubs est contrôlé par les unités de débit. Une unité de débit autorise 1 Mo par seconde d’entrée et deux fois cette quantité de sortie. Les concentrateurs d’événements Standard peuvent être configurés avec un nombre d’unités de débit compris entre 1 et 20. Augmentation automatique vous permet de toostart avec des unités de débit requis minimal hello. fonctionnalité de Hello puis met à l’échelle automatiquement toohello le nombre maximal d’unités de débit que vous avez besoin, en fonction de votre trafic augmentation hello. Valeur de l’augmentation automatique fournit hello avantages suivants :

- Un toostart mécanisme mise à l’échelle efficace petite et la montée en puissance en tant que vous augmentent en taille.
- Redimensionner automatiquement la limite supérieure de toohello spécifié sans problème de limitation.
- Plus de contrôle sur la mise à l’échelle, que vous contrôlez l’et la quantité tooscale.

## <a name="enable-auto-inflate-on-a-namespace"></a>Activer la majoration automatique sur un espace de noms

Vous pouvez activer ou désactiver la valeur de l’augmentation automatique sur un espace de noms à l’aide d’une des méthodes suivantes de hello :

1. Hello [portail Azure](https://portal.azure.com).
2. Un modèle Azure Resource Manager.

### <a name="enable-auto-inflate-through-hello-portal"></a>Activer augmentation automatique via le portail de hello

Vous pouvez activer la fonctionnalité de Auto-valeur de l’augmentation de hello sur un espace de noms lors de la création d’un espace de noms de concentrateurs d’événements :
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate1.png)

Une fois cette option activée, vous pouvez commencer par utiliser le nombre minimal d’unités de débit, puis monter en puissance à mesure que vos besoins d’utilisation augmentent. Hello limite supérieure de complications n’affecte pas la tarification, qui varie selon le nombre hello d’état utilisé par heure.

Vous pouvez également activer la valeur de l’augmentation automatique à l’aide de hello **échelle** option sur le panneau des paramètres dans le portail de hello hello :
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate2.png)

### <a name="enable-auto-inflate-using-an-azure-resource-manager-template"></a>Activer la majoration automatique à l’aide d’un modèle Azure Resource Manager

Vous pouvez activer la majoration automatique durant le déploiement d’un modèle Azure Resource Manager. Par exemple, set hello `isAutoInflateEnabled` propriété trop**true** et `maximumThroughputUnits` too10.

```json
"resources": [
        {
            "apiVersion": "2017-04-01",
            "name": "[parameters('namespaceName')]",
            "type": "Microsoft.EventHub/Namespaces",
            "location": "[variables('location')]",
            "sku": {
                "name": "Standard",
                "tier": "Standard"
            },
            "properties": {
                "isAutoInflateEnabled": true,
                "maximumThroughputUnits": 10
            },
            "resources": [
                {
                    "apiVersion": "2017-04-01",
                    "name": "[parameters('eventHubName')]",
                    "type": "EventHubs",
                    "dependsOn": [
                        "[concat('Microsoft.EventHub/namespaces/', parameters('namespaceName'))]"
                    ],
                    "properties": {},
                    "resources": [
                        {
                            "apiVersion": "2017-04-01",
                            "name": "[parameters('consumerGroupName')]",
                            "type": "ConsumerGroups",
                            "dependsOn": [
                                "[parameters('eventHubName')]"
                            ],
                            "properties": {}
                        }
                    ]
                }
            ]
        }
    ]
```

Pour le modèle complète de hello, consultez hello [espace de noms de créer des concentrateurs d’événements et activez la valeur de l’augmentation](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate) modèle sur GitHub.

## <a name="next-steps"></a>Étapes suivantes

Vous pouvez plus d’informations sur les concentrateurs d’événements en visitant hello suivant liens :

* [Vue d’ensemble des hubs d’événements](event-hubs-what-is-event-hubs.md)
* [Créer un concentrateur d’événements](event-hubs-create.md)
