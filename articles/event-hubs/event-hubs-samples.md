---
title: Exemples Azure Event Hubs | Microsoft Docs
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
ms.openlocfilehash: ae9fbd97a1747d8f14c561f247a0973bb11fd039
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="event-hubs-samples"></a><span data-ttu-id="b634e-103">Exemples de hubs d’événements</span><span class="sxs-lookup"><span data-stu-id="b634e-103">Event Hubs samples</span></span> 

<span data-ttu-id="b634e-104">Les exemples Azure Event Hubs présentent des fonctionnalités clés de [Azure Event Hubs](/azure/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="b634e-104">The set of Azure Event Hubs samples demonstrates key features in [Azure Event Hubs](/azure/event-hubs/).</span></span> <span data-ttu-id="b634e-105">Cette article attribue une catégorie et décrit les exemples disponibles, avec des liens vers chacun d’eux.</span><span class="sxs-lookup"><span data-stu-id="b634e-105">This article categorizes and describes the samples available, with links to each.</span></span>

<span data-ttu-id="b634e-106">Au moment de la rédaction de cet article, les exemples de hubs d’événements se trouvent dans différents emplacements :</span><span class="sxs-lookup"><span data-stu-id="b634e-106">At the time of this writing, Event Hubs samples are located in several different places:</span></span>

- [<span data-ttu-id="b634e-107">Exemples de code développeur MSDN</span><span class="sxs-lookup"><span data-stu-id="b634e-107">MSDN developer code samples</span></span>](https://code.msdn.microsoft.com/site/search?query=event%20hubs&f%5B0%5D.Value=event%20hubs&f%5B0%5D.Type=SearchText&ac=5)
- [<span data-ttu-id="b634e-108">GitHub</span><span class="sxs-lookup"><span data-stu-id="b634e-108">GitHub</span></span>](https://github.com/Azure/azure-event-hubs/tree/master/samples)

<span data-ttu-id="b634e-109">Pour plus d’informations sur les différentes versions de .NET Framework, consultez [Infrastructures et cibles](/dotnet/articles/standard/frameworks).</span><span class="sxs-lookup"><span data-stu-id="b634e-109">For more information about different versions of the .NET Framework, see [Frameworks and Targets](/dotnet/articles/standard/frameworks).</span></span>

<span data-ttu-id="b634e-110">D’autres exemples vont être ajoutés au fil du temps, alors consultez régulièrement cette page pour vérifier les mises à jour.</span><span class="sxs-lookup"><span data-stu-id="b634e-110">More samples will be added over time, so check back here frequently for updates.</span></span>

## <a name="net-standard"></a><span data-ttu-id="b634e-111">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="b634e-111">.NET Standard</span></span>

<span data-ttu-id="b634e-112">Les exemples suivants montrent comment envoyer et recevoir des événements à l’aide du [client Event Hubs](https://github.com/Azure/azure-event-hubs-dotnet/blob/master/readme.md) pour la [bibliothèque .NET Standard](/dotnet/articles/standard/library).</span><span class="sxs-lookup"><span data-stu-id="b634e-112">The following samples demonstrate how to send and receive events using the [Event Hubs client](https://github.com/Azure/azure-event-hubs-dotnet/blob/master/readme.md) for the [.NET Standard library](/dotnet/articles/standard/library).</span></span>

### <a name="send-events"></a><span data-ttu-id="b634e-113">Envoyer des événements</span><span class="sxs-lookup"><span data-stu-id="b634e-113">Send events</span></span> 

<span data-ttu-id="b634e-114">L’exemple de [prise en main de l’envoi](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) montre comment écrire une application console .NET Core qui envoie des événements vers un Event Hub.</span><span class="sxs-lookup"><span data-stu-id="b634e-114">The [Get started sending](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) sample shows how to write a .NET Core console application that sends events to an event hub.</span></span>

### <a name="receive-events"></a><span data-ttu-id="b634e-115">Recevoir des événements</span><span class="sxs-lookup"><span data-stu-id="b634e-115">Receive events</span></span> 

<span data-ttu-id="b634e-116">L’exemple de [prise en main de la réception avec l’hôte du processeur d’événements](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) est une application console .NET Core qui reçoit des messages à partir d’un concentrateur d’événements à l’aide de l’hôte du processeur d’événements.</span><span class="sxs-lookup"><span data-stu-id="b634e-116">The [Get started receiving with the Event Processor Host](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) sample is a .NET Core console application that receives messages from an event hub using the Event Processor Host.</span></span>

## <a name="net-framework"></a><span data-ttu-id="b634e-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="b634e-117">.NET Framework</span></span>   

<span data-ttu-id="b634e-118">Ces exemples présentent d’autres fonctionnalités d’Azure Event Hubs, ciblant la [bibliothèque .NET Framework](/dotnet/framework/index).</span><span class="sxs-lookup"><span data-stu-id="b634e-118">These samples demonstrate various other features of Azure Event Hubs, targeting the [.NET Framework library](/dotnet/framework/index).</span></span>
 
### <a name="notify-users-of-events-received"></a><span data-ttu-id="b634e-119">Avertir les utilisateurs de la réception d’événements</span><span class="sxs-lookup"><span data-stu-id="b634e-119">Notify users of events received</span></span>

<span data-ttu-id="b634e-120">L’exemple [AppToNotifyUsers](https://github.com/Azure-Samples/event-hubs-dotnet-user-notifications) avertit les utilisateurs de données reçues à partir des capteurs ou d’autres systèmes.</span><span class="sxs-lookup"><span data-stu-id="b634e-120">The [AppToNotifyUsers](https://github.com/Azure-Samples/event-hubs-dotnet-user-notifications) sample notifies users of data received from sensors or other systems.</span></span>

### <a name="get-started-with-event-hubs"></a><span data-ttu-id="b634e-121">Prise en main des hubs d’événements</span><span class="sxs-lookup"><span data-stu-id="b634e-121">Get started with Event Hubs</span></span> 

<span data-ttu-id="b634e-122">L’exemple de [prise en main des Event Hub](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097) montre les capacités de base des hubs d’événements, telles que la création d’un hub d’événements, l’envoi d’événements vers un Event Hub et la consommation d’événements à l’aide de [l’hôte du processeur d’événements](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span><span class="sxs-lookup"><span data-stu-id="b634e-122">The [Event Hubs Getting Started](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097) sample demonstrates the basic capabilities of Event Hubs, such as how to create an event hub, send events to an event hub, and consume events using the [Event Processor Host](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span></span>

### <a name="scale-out-event-processing"></a><span data-ttu-id="b634e-123">Traitement d’événement mis à l’échelle</span><span class="sxs-lookup"><span data-stu-id="b634e-123">Scale out event processing</span></span> 

<span data-ttu-id="b634e-124">L’exemple de [traitement d’événement mis à l’échelle](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3) montre comment utiliser [l’hôte du processeur d’événements](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) pour distribuer la charge de travail de la consommation de flux de hubs d’événements.</span><span class="sxs-lookup"><span data-stu-id="b634e-124">The [Scale out event processing](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3) sample demonstrates how to use the [Event Processor Host](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) to distribute the workload of Event Hubs stream consumption.</span></span> <span data-ttu-id="b634e-125">Il montre comment implémenter les objets **EventProcessor** et **EventProcessorFactory** pour gérer le flux d’événements.</span><span class="sxs-lookup"><span data-stu-id="b634e-125">It shows how to implement the **EventProcessor** and **EventProcessorFactory** objects to manage the event stream.</span></span> 

###  <a name="pull-data-from-sql-into-an-event-hub"></a><span data-ttu-id="b634e-126">Extraire des données de SQL dans Event Hub</span><span class="sxs-lookup"><span data-stu-id="b634e-126">Pull data from SQL into an event hub</span></span>

<span data-ttu-id="b634e-127">L’exemple [d’extraction de données SQL](https://github.com/Azure-Samples/event-hubs-dotnet-import-from-sql) montre comment extraire des données d’une table SQL et les distribuer vers un Event Hub pour les utiliser comme entrée de vos applications analytiques en aval.</span><span class="sxs-lookup"><span data-stu-id="b634e-127">The [Pulling SQL data](https://github.com/Azure-Samples/event-hubs-dotnet-import-from-sql) sample shows how to pull data from a SQL table and push it to an event hub, to use as an input in downstream analytical applications.</span></span>

### <a name="pull-web-data-into-an-event-hub"></a><span data-ttu-id="b634e-128">Extraire des données web dans un Event Hub</span><span class="sxs-lookup"><span data-stu-id="b634e-128">Pull web data into an event hub</span></span> 

<span data-ttu-id="b634e-129">L’exemple [d’importation des données à partir du web](https://github.com/Azure-Samples/event-hubs-dotnet-importfromweb) montre comment extraire des données à partir de flux publics (par exemple, le flux d’informations sur la circulation du Ministère des transports) et les distribuer vers un Event Hub.</span><span class="sxs-lookup"><span data-stu-id="b634e-129">The [Import data from the web](https://github.com/Azure-Samples/event-hubs-dotnet-importfromweb) sample shows how to pull data from public feeds (such as the Department of Transportation's traffic information feed) and push it to an event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b634e-130">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b634e-130">Next steps</span></span>

<span data-ttu-id="b634e-131">Pour en savoir plus sur les versions de .NET Framework, visitez les liens suivants :</span><span class="sxs-lookup"><span data-stu-id="b634e-131">Learn more about .NET Framework versions by visiting the following links:</span></span>

- [<span data-ttu-id="b634e-132">Infrastructures et cibles</span><span class="sxs-lookup"><span data-stu-id="b634e-132">Frameworks and targets</span></span>](/dotnet/articles/standard/frameworks)
- [<span data-ttu-id="b634e-133">.NET Framework 4.6 et 4.5</span><span class="sxs-lookup"><span data-stu-id="b634e-133">.NET Framework 4.6 and 4.5</span></span>](/dotnet/framework/index)

<span data-ttu-id="b634e-134">Pour plus d’informations sur les hubs d’événements, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="b634e-134">You can learn more about Event Hubs in the following articles:</span></span>

- [<span data-ttu-id="b634e-135">Vue d’ensemble des hubs d’événements</span><span class="sxs-lookup"><span data-stu-id="b634e-135">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
- [<span data-ttu-id="b634e-136">Créer un concentrateur d’événements</span><span class="sxs-lookup"><span data-stu-id="b634e-136">Create an event hub</span></span>](event-hubs-create.md)
- [<span data-ttu-id="b634e-137">FAQ sur les hubs d'événements</span><span class="sxs-lookup"><span data-stu-id="b634e-137">Event Hubs FAQ</span></span>](event-hubs-faq.md)