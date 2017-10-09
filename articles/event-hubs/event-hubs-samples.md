---
title: "exemples de concentrateurs d’événements aaaAzure | Documents Microsoft"
description: Exemples Azure Event Hubs
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: f01f52e6c13f9e885999a6726143440bbc70446d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-samples"></a><span data-ttu-id="768e5-103">Exemples de hubs d’événements</span><span class="sxs-lookup"><span data-stu-id="768e5-103">Event Hubs samples</span></span> 

<span data-ttu-id="768e5-104">ensemble d’exemples de concentrateurs d’événements Azure Hello illustre les fonctionnalités clés dans [Azure Event Hubs](/azure/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="768e5-104">hello set of Azure Event Hubs samples demonstrates key features in [Azure Event Hubs](/azure/event-hubs/).</span></span> <span data-ttu-id="768e5-105">Cet article de la catégorie et décrit les exemples hello disponibles, avec des liens tooeach.</span><span class="sxs-lookup"><span data-stu-id="768e5-105">This article categorizes and describes hello samples available, with links tooeach.</span></span>

<span data-ttu-id="768e5-106">Au moment de hello de rédaction de cet article, les exemples de concentrateurs d’événements se trouvent à différents endroits :</span><span class="sxs-lookup"><span data-stu-id="768e5-106">At hello time of this writing, Event Hubs samples are located in several different places:</span></span>

- [<span data-ttu-id="768e5-107">Exemples de code développeur MSDN</span><span class="sxs-lookup"><span data-stu-id="768e5-107">MSDN developer code samples</span></span>](https://code.msdn.microsoft.com/site/search?query=event%20hubs&f%5B0%5D.Value=event%20hubs&f%5B0%5D.Type=SearchText&ac=5)
- [<span data-ttu-id="768e5-108">GitHub</span><span class="sxs-lookup"><span data-stu-id="768e5-108">GitHub</span></span>](https://github.com/Azure/azure-event-hubs/tree/master/samples)

<span data-ttu-id="768e5-109">Pour plus d’informations sur les différentes versions de hello .NET Framework, consultez [infrastructures et cibles](/dotnet/articles/standard/frameworks).</span><span class="sxs-lookup"><span data-stu-id="768e5-109">For more information about different versions of hello .NET Framework, see [Frameworks and Targets](/dotnet/articles/standard/frameworks).</span></span>

<span data-ttu-id="768e5-110">D’autres exemples vont être ajoutés au fil du temps, alors consultez régulièrement cette page pour vérifier les mises à jour.</span><span class="sxs-lookup"><span data-stu-id="768e5-110">More samples will be added over time, so check back here frequently for updates.</span></span>

## <a name="net-standard"></a><span data-ttu-id="768e5-111">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="768e5-111">.NET Standard</span></span>

<span data-ttu-id="768e5-112">Hello exemples suivants montrent comment toosend et recevoir des événements à l’aide de hello [client de concentrateurs d’événements](https://github.com/Azure/azure-event-hubs-dotnet/blob/master/readme.md) pour hello [bibliothèque .NET Standard](/dotnet/articles/standard/library).</span><span class="sxs-lookup"><span data-stu-id="768e5-112">hello following samples demonstrate how toosend and receive events using hello [Event Hubs client](https://github.com/Azure/azure-event-hubs-dotnet/blob/master/readme.md) for hello [.NET Standard library](/dotnet/articles/standard/library).</span></span>

### <a name="send-events"></a><span data-ttu-id="768e5-113">Envoyer des événements</span><span class="sxs-lookup"><span data-stu-id="768e5-113">Send events</span></span> 

<span data-ttu-id="768e5-114">Hello [prise en main envoi](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) montre comment toowrite un .NET Core console application qui envoie le concentrateur d’événements événements tooan.</span><span class="sxs-lookup"><span data-stu-id="768e5-114">hello [Get started sending](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) sample shows how toowrite a .NET Core console application that sends events tooan event hub.</span></span>

### <a name="receive-events"></a><span data-ttu-id="768e5-115">Recevoir des événements</span><span class="sxs-lookup"><span data-stu-id="768e5-115">Receive events</span></span> 

<span data-ttu-id="768e5-116">Hello [prise en main de réception avec hello processeur d’événements hôte](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) exemple est une application console .NET Core qui reçoit des messages à partir d’un concentrateur d’événements à l’aide de hello processeur d’événements hôte.</span><span class="sxs-lookup"><span data-stu-id="768e5-116">hello [Get started receiving with hello Event Processor Host](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) sample is a .NET Core console application that receives messages from an event hub using hello Event Processor Host.</span></span>

## <a name="net-framework"></a><span data-ttu-id="768e5-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="768e5-117">.NET Framework</span></span>   

<span data-ttu-id="768e5-118">Ces exemples illustrent diverses fonctionnalités de Azure Event Hubs, ciblage hello [bibliothèque .NET Framework](/dotnet/framework/index).</span><span class="sxs-lookup"><span data-stu-id="768e5-118">These samples demonstrate various other features of Azure Event Hubs, targeting hello [.NET Framework library](/dotnet/framework/index).</span></span>
 
### <a name="notify-users-of-events-received"></a><span data-ttu-id="768e5-119">Avertir les utilisateurs de la réception d’événements</span><span class="sxs-lookup"><span data-stu-id="768e5-119">Notify users of events received</span></span>

<span data-ttu-id="768e5-120">Hello [AppToNotifyUsers](https://github.com/Azure-Samples/event-hubs-dotnet-user-notifications) exemple informe les utilisateurs de données provenant des capteurs ou d’autres systèmes.</span><span class="sxs-lookup"><span data-stu-id="768e5-120">hello [AppToNotifyUsers](https://github.com/Azure-Samples/event-hubs-dotnet-user-notifications) sample notifies users of data received from sensors or other systems.</span></span>

### <a name="get-started-with-event-hubs"></a><span data-ttu-id="768e5-121">Prise en main des hubs d’événements</span><span class="sxs-lookup"><span data-stu-id="768e5-121">Get started with Event Hubs</span></span> 

<span data-ttu-id="768e5-122">Hello [événement concentrateurs mise en route](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097) exemple illustre les fonctionnalités de base hello des concentrateurs d’événements, telles que comment envoyer le concentrateur d’événements événements tooan toocreate un concentrateur d’événements et consommer des événements à l’aide de hello [processeur d’événements hôte](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span><span class="sxs-lookup"><span data-stu-id="768e5-122">hello [Event Hubs Getting Started](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097) sample demonstrates hello basic capabilities of Event Hubs, such as how toocreate an event hub, send events tooan event hub, and consume events using hello [Event Processor Host](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span></span>

### <a name="scale-out-event-processing"></a><span data-ttu-id="768e5-123">Traitement d’événement mis à l’échelle</span><span class="sxs-lookup"><span data-stu-id="768e5-123">Scale out event processing</span></span> 

<span data-ttu-id="768e5-124">Hello [montée en charge le traitement des événements](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3) exemple illustre comment toouse hello [processeur d’événements hôte](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) la charge de travail hello toodistribute de consommation de flux de concentrateurs d’événements.</span><span class="sxs-lookup"><span data-stu-id="768e5-124">hello [Scale out event processing](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3) sample demonstrates how toouse hello [Event Processor Host](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) toodistribute hello workload of Event Hubs stream consumption.</span></span> <span data-ttu-id="768e5-125">Il montre comment tooimplement hello **EventProcessor** et **EventProcessorFactory** flux d’événements objets toomanage hello.</span><span class="sxs-lookup"><span data-stu-id="768e5-125">It shows how tooimplement hello **EventProcessor** and **EventProcessorFactory** objects toomanage hello event stream.</span></span> 

###  <a name="pull-data-from-sql-into-an-event-hub"></a><span data-ttu-id="768e5-126">Extraire des données de SQL dans Event Hub</span><span class="sxs-lookup"><span data-stu-id="768e5-126">Pull data from SQL into an event hub</span></span>

<span data-ttu-id="768e5-127">Hello [de données SQL d’extraction](https://github.com/Azure-Samples/event-hubs-dotnet-import-from-sql) exemple montre comment les données toopull à partir d’un SQL de table et poussez-le tooan toouse en tant qu’entrée dans les applications analytiques en aval, concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="768e5-127">hello [Pulling SQL data](https://github.com/Azure-Samples/event-hubs-dotnet-import-from-sql) sample shows how toopull data from a SQL table and push it tooan event hub, toouse as an input in downstream analytical applications.</span></span>

### <a name="pull-web-data-into-an-event-hub"></a><span data-ttu-id="768e5-128">Extraire des données web dans un Event Hub</span><span class="sxs-lookup"><span data-stu-id="768e5-128">Pull web data into an event hub</span></span> 

<span data-ttu-id="768e5-129">Hello [importer des données à partir du web de hello](https://github.com/Azure-Samples/event-hubs-dotnet-importfromweb) montre comment les données de toopull public (par exemple, informations sur le trafic du service de transport flux de hello) de flux et poussez-le tooan concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="768e5-129">hello [Import data from hello web](https://github.com/Azure-Samples/event-hubs-dotnet-importfromweb) sample shows how toopull data from public feeds (such as hello Department of Transportation's traffic information feed) and push it tooan event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="768e5-130">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="768e5-130">Next steps</span></span>

<span data-ttu-id="768e5-131">En savoir plus sur les versions du .NET Framework en visitant hello suivant liens :</span><span class="sxs-lookup"><span data-stu-id="768e5-131">Learn more about .NET Framework versions by visiting hello following links:</span></span>

- [<span data-ttu-id="768e5-132">Infrastructures et cibles</span><span class="sxs-lookup"><span data-stu-id="768e5-132">Frameworks and targets</span></span>](/dotnet/articles/standard/frameworks)
- [<span data-ttu-id="768e5-133">.NET Framework 4.6 et 4.5</span><span class="sxs-lookup"><span data-stu-id="768e5-133">.NET Framework 4.6 and 4.5</span></span>](/dotnet/framework/index)

<span data-ttu-id="768e5-134">Vous plus d’informations sur les concentrateurs d’événements Bonjour suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="768e5-134">You can learn more about Event Hubs in hello following articles:</span></span>

- [<span data-ttu-id="768e5-135">Vue d’ensemble des hubs d’événements</span><span class="sxs-lookup"><span data-stu-id="768e5-135">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
- [<span data-ttu-id="768e5-136">Créer un concentrateur d’événements</span><span class="sxs-lookup"><span data-stu-id="768e5-136">Create an event hub</span></span>](event-hubs-create.md)
- [<span data-ttu-id="768e5-137">FAQ sur les hubs d'événements</span><span class="sxs-lookup"><span data-stu-id="768e5-137">Event Hubs FAQ</span></span>](event-hubs-faq.md)