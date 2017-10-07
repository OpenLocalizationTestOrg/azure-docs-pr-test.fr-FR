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
# <a name="automatically-scale-up-azure-event-hubs-throughput-units"></a><span data-ttu-id="62cc2-103">Mettre automatiquement à l’échelle les unités de débit Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="62cc2-103">Automatically scale up Azure Event Hubs throughput units</span></span>

## <a name="overview"></a><span data-ttu-id="62cc2-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="62cc2-104">Overview</span></span>

<span data-ttu-id="62cc2-105">Azure Event Hubs est une plateforme hautement évolutive de diffusion de données en continu.</span><span class="sxs-lookup"><span data-stu-id="62cc2-105">Azure Event Hubs is a highly scalable data streaming platform.</span></span> <span data-ttu-id="62cc2-106">Par conséquent, les clients de concentrateurs d’événements augmentent souvent leur utilisation après l’intégration toohello service.</span><span class="sxs-lookup"><span data-stu-id="62cc2-106">As such, Event Hubs customers often increase their usage after onboarding toohello service.</span></span> <span data-ttu-id="62cc2-107">Ces augmente besoin croissant hello prédéterminé débit unités (état) tooscale concentrateurs d’événements et gérer des débits de transfert plus grandes.</span><span class="sxs-lookup"><span data-stu-id="62cc2-107">Such increases require increasing hello predetermined throughput units (TUs) tooscale Event Hubs and handle larger transfer rates.</span></span> <span data-ttu-id="62cc2-108">Hello *Auto-valeur de l’augmentation* s’ajuste automatiquement la fonctionnalité du service Event Hubs numéro hello besoins en matière d’utilisation de toomeet up.</span><span class="sxs-lookup"><span data-stu-id="62cc2-108">hello *Auto-inflate* feature of Event Hubs automatically scales up hello number of TUs toomeet usage needs.</span></span> <span data-ttu-id="62cc2-109">L’augmentation du nombre d’unités de débit vous empêche d’être confronté à des scénarios de limitation, dans lesquels :</span><span class="sxs-lookup"><span data-stu-id="62cc2-109">Increasing TUs prevents throttling scenarios, in which:</span></span>

* <span data-ttu-id="62cc2-110">Les taux d’entrée des données sont supérieurs aux unités de débit définies.</span><span class="sxs-lookup"><span data-stu-id="62cc2-110">Data ingress rates exceed set TUs.</span></span>
* <span data-ttu-id="62cc2-111">Les taux de demande de sortie des données sont supérieurs aux unités de débit définies.</span><span class="sxs-lookup"><span data-stu-id="62cc2-111">Data egress request rates exceed set TUs.</span></span>

## <a name="how-auto-inflate-works"></a><span data-ttu-id="62cc2-112">Fonctionnement de la majoration automatique</span><span class="sxs-lookup"><span data-stu-id="62cc2-112">How Auto-inflate works</span></span>

<span data-ttu-id="62cc2-113">Le trafic Event Hubs est contrôlé par les unités de débit.</span><span class="sxs-lookup"><span data-stu-id="62cc2-113">Event Hubs traffic is controlled by throughput units.</span></span> <span data-ttu-id="62cc2-114">Une unité de débit autorise 1 Mo par seconde d’entrée et deux fois cette quantité de sortie.</span><span class="sxs-lookup"><span data-stu-id="62cc2-114">A single TU allows 1 MB per second of ingress and twice that amount of egress.</span></span> <span data-ttu-id="62cc2-115">Les concentrateurs d’événements Standard peuvent être configurés avec un nombre d’unités de débit compris entre 1 et 20.</span><span class="sxs-lookup"><span data-stu-id="62cc2-115">Standard Event Hubs can be configured with 1-20 throughput units.</span></span> <span data-ttu-id="62cc2-116">Augmentation automatique vous permet de toostart avec des unités de débit requis minimal hello.</span><span class="sxs-lookup"><span data-stu-id="62cc2-116">Auto-inflate enables you toostart small with hello minimum required throughput units.</span></span> <span data-ttu-id="62cc2-117">fonctionnalité de Hello puis met à l’échelle automatiquement toohello le nombre maximal d’unités de débit que vous avez besoin, en fonction de votre trafic augmentation hello.</span><span class="sxs-lookup"><span data-stu-id="62cc2-117">hello feature then scales automatically toohello maximum limit of throughput units you need, depending on hello increase in your traffic.</span></span> <span data-ttu-id="62cc2-118">Valeur de l’augmentation automatique fournit hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="62cc2-118">Auto-inflate provides hello following benefits:</span></span>

- <span data-ttu-id="62cc2-119">Un toostart mécanisme mise à l’échelle efficace petite et la montée en puissance en tant que vous augmentent en taille.</span><span class="sxs-lookup"><span data-stu-id="62cc2-119">An efficient scaling mechanism toostart small and scale up as you grow.</span></span>
- <span data-ttu-id="62cc2-120">Redimensionner automatiquement la limite supérieure de toohello spécifié sans problème de limitation.</span><span class="sxs-lookup"><span data-stu-id="62cc2-120">Automatically scale toohello specified upper limit without throttling issues.</span></span>
- <span data-ttu-id="62cc2-121">Plus de contrôle sur la mise à l’échelle, que vous contrôlez l’et la quantité tooscale.</span><span class="sxs-lookup"><span data-stu-id="62cc2-121">More control over scaling, as you control when and how much tooscale.</span></span>

## <a name="enable-auto-inflate-on-a-namespace"></a><span data-ttu-id="62cc2-122">Activer la majoration automatique sur un espace de noms</span><span class="sxs-lookup"><span data-stu-id="62cc2-122">Enable Auto-inflate on a namespace</span></span>

<span data-ttu-id="62cc2-123">Vous pouvez activer ou désactiver la valeur de l’augmentation automatique sur un espace de noms à l’aide d’une des méthodes suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="62cc2-123">You can enable or disable Auto-inflate on a namespace using either of hello following methods:</span></span>

1. <span data-ttu-id="62cc2-124">Hello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="62cc2-124">hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="62cc2-125">Un modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="62cc2-125">An Azure Resource Manager template.</span></span>

### <a name="enable-auto-inflate-through-hello-portal"></a><span data-ttu-id="62cc2-126">Activer augmentation automatique via le portail de hello</span><span class="sxs-lookup"><span data-stu-id="62cc2-126">Enable Auto-inflate through hello portal</span></span>

<span data-ttu-id="62cc2-127">Vous pouvez activer la fonctionnalité de Auto-valeur de l’augmentation de hello sur un espace de noms lors de la création d’un espace de noms de concentrateurs d’événements :</span><span class="sxs-lookup"><span data-stu-id="62cc2-127">You can enable hello Auto-inflate feature on a namespace when creating an Event Hubs namespace:</span></span>
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate1.png)

<span data-ttu-id="62cc2-128">Une fois cette option activée, vous pouvez commencer par utiliser le nombre minimal d’unités de débit, puis monter en puissance à mesure que vos besoins d’utilisation augmentent.</span><span class="sxs-lookup"><span data-stu-id="62cc2-128">With this option enabled, you can start small on your throughput units and scale up as your usage needs increase.</span></span> <span data-ttu-id="62cc2-129">Hello limite supérieure de complications n’affecte pas la tarification, qui varie selon le nombre hello d’état utilisé par heure.</span><span class="sxs-lookup"><span data-stu-id="62cc2-129">hello upper limit for inflation does not affect pricing, which depends on hello number of TUs used per hour.</span></span>

<span data-ttu-id="62cc2-130">Vous pouvez également activer la valeur de l’augmentation automatique à l’aide de hello **échelle** option sur le panneau des paramètres dans le portail de hello hello :</span><span class="sxs-lookup"><span data-stu-id="62cc2-130">You can also enable Auto-inflate using hello **Scale** option on hello settings blade in hello portal:</span></span>
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate2.png)

### <a name="enable-auto-inflate-using-an-azure-resource-manager-template"></a><span data-ttu-id="62cc2-131">Activer la majoration automatique à l’aide d’un modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="62cc2-131">Enable Auto-Inflate using an Azure Resource Manager template</span></span>

<span data-ttu-id="62cc2-132">Vous pouvez activer la majoration automatique durant le déploiement d’un modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="62cc2-132">You can enable Auto-inflate during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="62cc2-133">Par exemple, set hello `isAutoInflateEnabled` propriété trop**true** et `maximumThroughputUnits` too10.</span><span class="sxs-lookup"><span data-stu-id="62cc2-133">For example, set hello `isAutoInflateEnabled` property too**true** and set `maximumThroughputUnits` too10.</span></span>

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

<span data-ttu-id="62cc2-134">Pour le modèle complète de hello, consultez hello [espace de noms de créer des concentrateurs d’événements et activez la valeur de l’augmentation](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate) modèle sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="62cc2-134">For hello complete template, see hello [Create Event Hubs namespace and enable inflate](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate) template on GitHub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="62cc2-135">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="62cc2-135">Next steps</span></span>

<span data-ttu-id="62cc2-136">Vous pouvez plus d’informations sur les concentrateurs d’événements en visitant hello suivant liens :</span><span class="sxs-lookup"><span data-stu-id="62cc2-136">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="62cc2-137">Vue d’ensemble des hubs d’événements</span><span class="sxs-lookup"><span data-stu-id="62cc2-137">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="62cc2-138">Créer un concentrateur d’événements</span><span class="sxs-lookup"><span data-stu-id="62cc2-138">Create an Event Hub</span></span>](event-hubs-create.md)
