---
title: "Mettre automatiquement à l’échelle les unités de débit Azure Event Hubs | Microsoft Docs"
description: "Activer la majoration automatique sur un espace de noms pour mettre automatiquement à l’échelle les unités de débit"
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
ms.openlocfilehash: b085091ea7bfd601efb0eee84144ddd091422d6e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="automatically-scale-up-azure-event-hubs-throughput-units"></a><span data-ttu-id="a16fb-103">Mettre automatiquement à l’échelle les unités de débit Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="a16fb-103">Automatically scale up Azure Event Hubs throughput units</span></span>

## <a name="overview"></a><span data-ttu-id="a16fb-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="a16fb-104">Overview</span></span>

<span data-ttu-id="a16fb-105">Azure Event Hubs est une plateforme hautement évolutive de diffusion de données en continu.</span><span class="sxs-lookup"><span data-stu-id="a16fb-105">Azure Event Hubs is a highly scalable data streaming platform.</span></span> <span data-ttu-id="a16fb-106">Par conséquent, les clients Event Hubs augmentent souvent leur utilisation après leur intégration au service.</span><span class="sxs-lookup"><span data-stu-id="a16fb-106">As such, Event Hubs customers often increase their usage after onboarding to the service.</span></span> <span data-ttu-id="a16fb-107">Cette augmentation de l’utilisation requiert la hausse des unités de débit (TU) prédéterminées pour mettre à l’échelle Event Hubs et gérer des débits de transfert plus importants.</span><span class="sxs-lookup"><span data-stu-id="a16fb-107">Such increases require increasing the predetermined throughput units (TUs) to scale Event Hubs and handle larger transfer rates.</span></span> <span data-ttu-id="a16fb-108">La fonctionnalité de *majoration automatique* (Auto-inflate) d’Event Hubs met automatiquement à l’échelle le nombre d’unités de débit pour répondre aux besoins d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="a16fb-108">The *Auto-inflate* feature of Event Hubs automatically scales up the number of TUs to meet usage needs.</span></span> <span data-ttu-id="a16fb-109">L’augmentation du nombre d’unités de débit vous empêche d’être confronté à des scénarios de limitation, dans lesquels :</span><span class="sxs-lookup"><span data-stu-id="a16fb-109">Increasing TUs prevents throttling scenarios, in which:</span></span>

* <span data-ttu-id="a16fb-110">Les taux d’entrée des données sont supérieurs aux unités de débit définies.</span><span class="sxs-lookup"><span data-stu-id="a16fb-110">Data ingress rates exceed set TUs.</span></span>
* <span data-ttu-id="a16fb-111">Les taux de demande de sortie des données sont supérieurs aux unités de débit définies.</span><span class="sxs-lookup"><span data-stu-id="a16fb-111">Data egress request rates exceed set TUs.</span></span>

## <a name="how-auto-inflate-works"></a><span data-ttu-id="a16fb-112">Fonctionnement de la majoration automatique</span><span class="sxs-lookup"><span data-stu-id="a16fb-112">How Auto-inflate works</span></span>

<span data-ttu-id="a16fb-113">Le trafic Event Hubs est contrôlé par les unités de débit.</span><span class="sxs-lookup"><span data-stu-id="a16fb-113">Event Hubs traffic is controlled by throughput units.</span></span> <span data-ttu-id="a16fb-114">Une unité de débit autorise 1 Mo par seconde d’entrée et deux fois cette quantité de sortie.</span><span class="sxs-lookup"><span data-stu-id="a16fb-114">A single TU allows 1 MB per second of ingress and twice that amount of egress.</span></span> <span data-ttu-id="a16fb-115">Les concentrateurs d’événements Standard peuvent être configurés avec un nombre d’unités de débit compris entre 1 et 20.</span><span class="sxs-lookup"><span data-stu-id="a16fb-115">Standard Event Hubs can be configured with 1-20 throughput units.</span></span> <span data-ttu-id="a16fb-116">La majoration automatique vous permet de démarrer avec le nombre d’unités de débit minimal requis.</span><span class="sxs-lookup"><span data-stu-id="a16fb-116">Auto-inflate enables you to start small with the minimum required throughput units.</span></span> <span data-ttu-id="a16fb-117">Ensuite, la fonctionnalité met automatiquement à l’échelle le nombre d’unités de débit dont vous avez besoin sur la limite maximale, selon l’augmentation de votre trafic.</span><span class="sxs-lookup"><span data-stu-id="a16fb-117">The feature then scales automatically to the maximum limit of throughput units you need, depending on the increase in your traffic.</span></span> <span data-ttu-id="a16fb-118">La majoration automatique vous permet de bénéficier des avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="a16fb-118">Auto-inflate provides the following benefits:</span></span>

- <span data-ttu-id="a16fb-119">Un mécanisme de mise à l’échelle efficace pour démarrer avec la valeur minimale et monter en puissance à mesure de la croissance de votre activité.</span><span class="sxs-lookup"><span data-stu-id="a16fb-119">An efficient scaling mechanism to start small and scale up as you grow.</span></span>
- <span data-ttu-id="a16fb-120">Mise à l’échelle automatique sur à la limite supérieure spécifiée sans problèmes de limitation.</span><span class="sxs-lookup"><span data-stu-id="a16fb-120">Automatically scale to the specified upper limit without throttling issues.</span></span>
- <span data-ttu-id="a16fb-121">Contrôle amélioré de la mise à l’échelle, car vous contrôlez le moment et la quantité de la mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="a16fb-121">More control over scaling, as you control when and how much to scale.</span></span>

## <a name="enable-auto-inflate-on-a-namespace"></a><span data-ttu-id="a16fb-122">Activer la majoration automatique sur un espace de noms</span><span class="sxs-lookup"><span data-stu-id="a16fb-122">Enable Auto-inflate on a namespace</span></span>

<span data-ttu-id="a16fb-123">Vous pouvez activer ou désactiver la majoration automatique sur un espace de noms avec l’une des méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="a16fb-123">You can enable or disable Auto-inflate on a namespace using either of the following methods:</span></span>

1. <span data-ttu-id="a16fb-124">Le [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a16fb-124">The [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a16fb-125">Un modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a16fb-125">An Azure Resource Manager template.</span></span>

### <a name="enable-auto-inflate-through-the-portal"></a><span data-ttu-id="a16fb-126">Activer la majoration automatique via le portail</span><span class="sxs-lookup"><span data-stu-id="a16fb-126">Enable Auto-inflate through the portal</span></span>

<span data-ttu-id="a16fb-127">Vous pouvez activer la fonctionnalité de majoration automatique sur un espace de noms lors de la création d’un espace de noms Event Hubs :</span><span class="sxs-lookup"><span data-stu-id="a16fb-127">You can enable the Auto-inflate feature on a namespace when creating an Event Hubs namespace:</span></span>
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate1.png)

<span data-ttu-id="a16fb-128">Une fois cette option activée, vous pouvez commencer par utiliser le nombre minimal d’unités de débit, puis monter en puissance à mesure que vos besoins d’utilisation augmentent.</span><span class="sxs-lookup"><span data-stu-id="a16fb-128">With this option enabled, you can start small on your throughput units and scale up as your usage needs increase.</span></span> <span data-ttu-id="a16fb-129">La limite supérieure de la majoration n’affecte pas les prix, qui dépendent du nombre d’unités de débit utilisées par heure.</span><span class="sxs-lookup"><span data-stu-id="a16fb-129">The upper limit for inflation does not affect pricing, which depends on the number of TUs used per hour.</span></span>

<span data-ttu-id="a16fb-130">Vous pouvez également activer la majoration automatique à l’aide de l’option **Mettre à l’échelle** dans le panneau des paramètres du portail :</span><span class="sxs-lookup"><span data-stu-id="a16fb-130">You can also enable Auto-inflate using the **Scale** option on the settings blade in the portal:</span></span>
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate2.png)

### <a name="enable-auto-inflate-using-an-azure-resource-manager-template"></a><span data-ttu-id="a16fb-131">Activer la majoration automatique à l’aide d’un modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a16fb-131">Enable Auto-Inflate using an Azure Resource Manager template</span></span>

<span data-ttu-id="a16fb-132">Vous pouvez activer la majoration automatique durant le déploiement d’un modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a16fb-132">You can enable Auto-inflate during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="a16fb-133">Par exemple, définissez la propriété `isAutoInflateEnabled` sur **true** et définissez `maximumThroughputUnits` sur 10.</span><span class="sxs-lookup"><span data-stu-id="a16fb-133">For example, set the `isAutoInflateEnabled` property to **true** and set `maximumThroughputUnits` to 10.</span></span>

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

<span data-ttu-id="a16fb-134">Pour accéder au modèle complet, consultez le modèle [Create Event Hubs namespace and enable inflate](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate) (Créer un espace de noms Event Hubs et activer la majoration) sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="a16fb-134">For the complete template, see the [Create Event Hubs namespace and enable inflate](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate) template on GitHub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a16fb-135">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a16fb-135">Next steps</span></span>

<span data-ttu-id="a16fb-136">Vous pouvez en apprendre plus sur Event Hubs en consultant les liens suivants :</span><span class="sxs-lookup"><span data-stu-id="a16fb-136">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="a16fb-137">Vue d’ensemble des hubs d’événements</span><span class="sxs-lookup"><span data-stu-id="a16fb-137">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="a16fb-138">Créer un concentrateur d’événements</span><span class="sxs-lookup"><span data-stu-id="a16fb-138">Create an Event Hub</span></span>](event-hubs-create.md)
