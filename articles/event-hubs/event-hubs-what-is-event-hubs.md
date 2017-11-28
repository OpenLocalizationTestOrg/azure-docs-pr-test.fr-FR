---
title: aaaWhat est Azure Event Hubs et pourquoi utiliser | Documents Microsoft
description: "Vue d’ensemble et introduction tooAzure concentrateurs d’événements - ingestion de télémétrie de l’échelle du Cloud à partir de sites Web, des applications et des périphériques"
services: event-hubs
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: sethm; babanisa
ms.openlocfilehash: f6199a2e5bee8506f529b6f561234d79f9c8d465
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-event-hubs"></a><span data-ttu-id="6745b-103">Qu’est-ce qu’Event Hubs ?</span><span class="sxs-lookup"><span data-stu-id="6745b-103">What is Event Hubs?</span></span>

<span data-ttu-id="6745b-104">Azure Event Hubs est une plateforme de diffusion de données hautement évolutive et de service d’ingestion d’événement capable de recevoir et de traiter des millions d’événements par seconde.</span><span class="sxs-lookup"><span data-stu-id="6745b-104">Azure Event Hubs is a highly scalable data streaming platform and event ingestion service capable of receiving and processing millions of events per second.</span></span> <span data-ttu-id="6745b-105">Les concentrateurs d’événements peuvent traiter et stocker des événements, des données ou la télémétrie produits par des logiciels et appareils distribués.</span><span class="sxs-lookup"><span data-stu-id="6745b-105">Event Hubs can process and store events, data, or telemetry produced by distributed software and devices.</span></span> <span data-ttu-id="6745b-106">Les données envoyées tooan concentrateur d’événements peut être transformé et stockés à l’aide de n’importe quel fournisseur de l’analytique en temps réel ou les cartes de traitement par lot/stockage.</span><span class="sxs-lookup"><span data-stu-id="6745b-106">Data sent tooan event hub can be transformed and stored using any real-time analytics provider or batching/storage adapters.</span></span> <span data-ttu-id="6745b-107">Avec hello capacité tooprovide [fonctionnalités de publication / abonnement](https://msdn.microsoft.com/library/aa560414.aspx) avec une faible latence et à très grande échelle, les concentrateurs d’événements sert hello « sur le démarrage » pour les données volumineuses.</span><span class="sxs-lookup"><span data-stu-id="6745b-107">With hello ability tooprovide [publish-subscribe capabilities](https://msdn.microsoft.com/library/aa560414.aspx) with low latency and at massive scale, Event Hubs serves as hello "on ramp" for Big Data.</span></span>

## <a name="why-use-event-hubs"></a><span data-ttu-id="6745b-108">Pourquoi utiliser Azure Event Hubs ?</span><span class="sxs-lookup"><span data-stu-id="6745b-108">Why use Event Hubs?</span></span>

<span data-ttu-id="6745b-109">Les fonctionnalités de traitement des événements et données de télémétrie de cette solution sont particulièrement adaptées pour les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="6745b-109">Event Hubs event and telemetry handling capabilities make it especially useful for:</span></span>

* <span data-ttu-id="6745b-110">L’instrumentation de l'application</span><span class="sxs-lookup"><span data-stu-id="6745b-110">Application instrumentation</span></span>
* <span data-ttu-id="6745b-111">L’expérience de l'utilisateur ou le traitement du flux de travail</span><span class="sxs-lookup"><span data-stu-id="6745b-111">User experience or workflow processing</span></span>
* <span data-ttu-id="6745b-112">Des scénarios Internet des objets (IoT)</span><span class="sxs-lookup"><span data-stu-id="6745b-112">Internet of Things (IoT) scenarios</span></span>

<span data-ttu-id="6745b-113">Par exemple, les concentrateurs d’événements inclut une fonction de suivi du comportement dans les applications mobiles, des informations sur le trafic provenant de batteries de serveurs web, de capture d’événements de jeu dans les jeux de console ou des données de télémétrie collectées sur des machines industrielles, des véhicules connectés ou d’autres appareils.</span><span class="sxs-lookup"><span data-stu-id="6745b-113">For example, Event Hubs enables behavior tracking in mobile apps, traffic information from web farms, in-game event capture in console games, or telemetry collected from industrial machines, connected vehicles, or other devices.</span></span>

## <a name="azure-event-hubs-overview"></a><span data-ttu-id="6745b-114">Vue d'ensemble des hubs d'événements Azure</span><span class="sxs-lookup"><span data-stu-id="6745b-114">Azure Event Hubs overview</span></span>

<span data-ttu-id="6745b-115">rôle courant que les concentrateurs d’événements lit dans les architectures de solution Hello est hello « porte d’entrée » pour un pipeline d’événements, souvent appelé un *ingesteur d’événements*.</span><span class="sxs-lookup"><span data-stu-id="6745b-115">hello common role that Event Hubs plays in solution architectures is hello "front door" for an event pipeline, often called an *event ingestor*.</span></span> <span data-ttu-id="6745b-116">Un ingesteur d’événements est un composant ou service qui se trouve entre les éditeurs d’événements et de production de hello de toodecouple des consommateurs d’événements d’un flux d’événements à partir de la consommation de ces événements hello.</span><span class="sxs-lookup"><span data-stu-id="6745b-116">An event ingestor is a component or service that sits between event publishers and event consumers toodecouple hello production of an event stream from hello consumption of those events.</span></span> <span data-ttu-id="6745b-117">Hello figure suivante illustre cette architecture :</span><span class="sxs-lookup"><span data-stu-id="6745b-117">hello following figure depicts this architecture:</span></span>

![Event Hubs](./media/event-hubs-what-is-event-hubs/event_hubs_full_pipeline.png)

<span data-ttu-id="6745b-119">Cette solution fournit une fonctionnalité de gestion du flux de messages mais présente des caractéristiques différentes de la messagerie d’entreprise traditionnelle.</span><span class="sxs-lookup"><span data-stu-id="6745b-119">Event Hubs provides message stream handling capability but has characteristics that are different from traditional enterprise messaging.</span></span> <span data-ttu-id="6745b-120">Ses fonctionnalités reposent sur des scénarios de traitement des événements et un débit élevé.</span><span class="sxs-lookup"><span data-stu-id="6745b-120">Event Hubs capabilities are built around high throughput and event processing scenarios.</span></span> <span data-ttu-id="6745b-121">Par conséquent, les concentrateurs d’événements est différent de [Azure Service Bus](https://azure.microsoft.com/services/service-bus/) de messagerie et n’implémente pas certaines des fonctionnalités hello qui sont disponibles pour [messagerie Service Bus](/azure/service-bus-messaging/) entités, telles que des rubriques.</span><span class="sxs-lookup"><span data-stu-id="6745b-121">As such, Event Hubs is different from [Azure Service Bus](https://azure.microsoft.com/services/service-bus/) messaging, and does not implement some of hello capabilities that are available for [Service Bus messaging](/azure/service-bus-messaging/) entities, such as topics.</span></span>

## <a name="event-hubs-features"></a><span data-ttu-id="6745b-122">Fonctionnalités des concentrateurs d’événements</span><span class="sxs-lookup"><span data-stu-id="6745b-122">Event Hubs features</span></span>

<span data-ttu-id="6745b-123">Concentrateurs d’événements contient hello suit les éléments clés :</span><span class="sxs-lookup"><span data-stu-id="6745b-123">Event Hubs contains hello following key elements:</span></span>

- <span data-ttu-id="6745b-124">[**Les éditeurs/producteurs d’événements**](event-hubs-features.md#event-publishers): une entité qui envoie le concentrateur d’événements de tooan de données.</span><span class="sxs-lookup"><span data-stu-id="6745b-124">[**Event producers/publishers**](event-hubs-features.md#event-publishers): An entity that sends data tooan event hub.</span></span> <span data-ttu-id="6745b-125">Un événement est publié via AMQP 1.0 ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="6745b-125">An event is published via AMQP 1.0 or HTTPS.</span></span>
- <span data-ttu-id="6745b-126">[**Capturer**](event-hubs-features.md#capture): vous permet de toocapture les concentrateurs d’événements de diffusion en continu de données et les stocker dans un compte de stockage d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="6745b-126">[**Capture**](event-hubs-features.md#capture): Enables you toocapture Event Hubs streaming data and store it in an Azure Blob storage account.</span></span>
- <span data-ttu-id="6745b-127">[**Partitions**](event-hubs-features.md#partitions): permet à chaque tooonly consommateur lire un sous-ensemble spécifique, ou une partition, de hello flux d’événements.</span><span class="sxs-lookup"><span data-stu-id="6745b-127">[**Partitions**](event-hubs-features.md#partitions): Enables each consumer tooonly read a specific subset, or partition, of hello event stream.</span></span>
- <span data-ttu-id="6745b-128">[**Jetons SAP**](event-hubs-features.md#sas-tokens): identifie et authentifie l’éditeur d’événements hello.</span><span class="sxs-lookup"><span data-stu-id="6745b-128">[**SAS tokens**](event-hubs-features.md#sas-tokens): Identifies and authenticates hello event publisher.</span></span>
- <span data-ttu-id="6745b-129">[**Consommateurs d’événements**](event-hubs-features.md#event-consumers) : entité qui lit des données d’événement à partir d’un concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="6745b-129">[**Event consumers**](event-hubs-features.md#event-consumers): An entity that reads event data from an event hub.</span></span> <span data-ttu-id="6745b-130">Les consommateurs d’événements se connectent via AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="6745b-130">Event consumers connect via AMQP 1.0.</span></span> 
- <span data-ttu-id="6745b-131">[**Groupes de consommateurs**](event-hubs-features.md#consumer-groups): fournit chaque multiple consommation d’application avec une vue distincte du flux d’événements hello, l’activation de ces tooact consommateurs indépendamment.</span><span class="sxs-lookup"><span data-stu-id="6745b-131">[**Consumer groups**](event-hubs-features.md#consumer-groups): Provides each multiple consuming application with a separate view of hello event stream, enabling those consumers tooact independently.</span></span>
- <span data-ttu-id="6745b-132">[**Unités de débit**](event-hubs-features.md#capacity) : unités de capacité achetées préalablement.</span><span class="sxs-lookup"><span data-stu-id="6745b-132">[**Throughput units**](event-hubs-features.md#capacity): Pre-purchased units of capacity.</span></span> <span data-ttu-id="6745b-133">Une partition unique a une échelle maximale d’1 unité de débit.</span><span class="sxs-lookup"><span data-stu-id="6745b-133">A single partition has a maximum scale of 1 throughput unit.</span></span>

<span data-ttu-id="6745b-134">Pour obtenir des détails techniques sur d’autres fonctionnalités de concentrateurs d’événements, consultez hello [vue d’ensemble des fonctionnalités de concentrateurs d’événements](event-hubs-features.md).</span><span class="sxs-lookup"><span data-stu-id="6745b-134">For technical details about these and other Event Hubs features, see hello [Event Hubs features overview](event-hubs-features.md).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="6745b-135">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6745b-135">Next steps</span></span>

<span data-ttu-id="6745b-136">Pour obtenir des informations de tarification détaillées des concentrateurs d’événements, consultez [Tarification des concentrateurs d’événements](https://azure.microsoft.com/pricing/details/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="6745b-136">For detailed Event Hubs pricing information, see [Event Hubs Pricing](https://azure.microsoft.com/pricing/details/event-hubs/).</span></span>

<span data-ttu-id="6745b-137">Pour plus d’informations sur les concentrateurs d’événements, consultez hello suivant liens :</span><span class="sxs-lookup"><span data-stu-id="6745b-137">For more information about Event Hubs, visit hello following links:</span></span>

* <span data-ttu-id="6745b-138">Prise en main avec un [didacticiel des concentrateurs d’événements](event-hubs-dotnet-standard-getstarted-send.md)</span><span class="sxs-lookup"><span data-stu-id="6745b-138">Get started with an [Event Hubs tutorial](event-hubs-dotnet-standard-getstarted-send.md)</span></span>
* [<span data-ttu-id="6745b-139">FAQ sur les hubs d'événements</span><span class="sxs-lookup"><span data-stu-id="6745b-139">Event Hubs FAQ</span></span>](event-hubs-faq.md)
* [<span data-ttu-id="6745b-140">Exemples d’applications qui utilisent des Event Hubs</span><span class="sxs-lookup"><span data-stu-id="6745b-140">Sample applications that use Event Hubs</span></span>](https://github.com/Azure/azure-event-hubs/tree/master/samples)
 
 

