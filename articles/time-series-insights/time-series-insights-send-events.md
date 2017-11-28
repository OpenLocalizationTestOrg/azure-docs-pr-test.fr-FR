---
title: "Envoyer des événements à votre environnement Azure Time Series Insights | Microsoft Docs"
description: "Ce didacticiel décrit les étapes à suivre pour envoyer des événements à votre environnement Time Series Insights"
keywords: 
services: tsi
documentationcenter: 
author: venkatgct
manager: jhubbard
editor: 
ms.assetid: 
ms.service: tsi
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/21/2017
ms.author: venkatja
ms.openlocfilehash: b4ef96a045393f28b3cd750068fe82a5a8411afa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="send-events-to-a-time-series-insights-environment-using-event-hub"></a><span data-ttu-id="f8ab1-103">Envoyer des événements à un environnement Time Series Insights à l’aide d’un concentrateur d’événements</span><span class="sxs-lookup"><span data-stu-id="f8ab1-103">Send events to a Time Series Insights environment using event hub</span></span>

<span data-ttu-id="f8ab1-104">Ce didacticiel explique comment créer et configurer le concentrateur d’événements et exécuter un exemple d’application pour envoyer des événements.</span><span class="sxs-lookup"><span data-stu-id="f8ab1-104">This tutorial explains how to create and configure event hub and run a sample application to push events.</span></span> <span data-ttu-id="f8ab1-105">Si vous disposez d’un concentrateur d’événements existant qui a déjà des événements au format JSON, ignorez ce didacticiel et affichez votre environnement dans [time series insights](https://insights.timeseries.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f8ab1-105">If you have an existing event hub with events in JSON format, skip this tutorial and view your environment in [time series insights](https://insights.timeseries.azure.com).</span></span>

## <a name="configure-an-event-hub"></a><span data-ttu-id="f8ab1-106">Configurer un concentrateur d’événements</span><span class="sxs-lookup"><span data-stu-id="f8ab1-106">Configure an event hub</span></span>
1. <span data-ttu-id="f8ab1-107">Pour créer un concentrateur d’événements, suivez les instructions de la [documentation](https://docs.microsoft.com/azure/event-hubs/event-hubs-create) relative aux concentrateurs d’événements.</span><span class="sxs-lookup"><span data-stu-id="f8ab1-107">To create an event hub, follow instructions from the Event Hub [documentation](https://docs.microsoft.com/azure/event-hubs/event-hubs-create).</span></span>

2. <span data-ttu-id="f8ab1-108">Veillez à créer un groupe de consommateurs qui sera utilisé exclusivement par votre source d’événement Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="f8ab1-108">Make sure you create a consumer group that is used exclusively by your Time Series Insights event source.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="f8ab1-109">Assurez-vous que ce groupe de consommateurs n’est pas utilisé par un autre service (par exemple, une tâche Stream Analytics ou un autre environnement Time Series Insights).</span><span class="sxs-lookup"><span data-stu-id="f8ab1-109">Make sure this consumer group is not used by any other service (such as Stream Analytics job or another Time Series Insights environment).</span></span> <span data-ttu-id="f8ab1-110">Si le groupe de consommateurs est utilisé par d’autres services, l’opération de lecture est affectée pour cet environnement et les autres services.</span><span class="sxs-lookup"><span data-stu-id="f8ab1-110">If consumer group is used by other services, read operation is negatively affected for this environment and the other services.</span></span> <span data-ttu-id="f8ab1-111">Si vous utilisez le groupe de consommateurs « $Default », ceci peut entraîner une réutilisation potentielle par d’autres lecteurs.</span><span class="sxs-lookup"><span data-stu-id="f8ab1-111">If you are using “$Default” as the consumer group, it could lead to potential reuse by other readers.</span></span>

  ![Sélectionnez le groupe de consommateurs du concentrateur d’événements](media/send-events/consumer-group.png)

3. <span data-ttu-id="f8ab1-113">Dans le concentrateur d’événements, créez la stratégie « MySendPolicy » utilisée pour envoyer des événements dans l’exemple csharp.</span><span class="sxs-lookup"><span data-stu-id="f8ab1-113">On the event hub, create “MySendPolicy” that is used to send events in the csharp sample.</span></span>

  ![Sélectionnez des stratégies d’accès partagé et cliquez sur le bouton Ajouter](media/send-events/shared-access-policy.png)  

  ![Ajoutez une stratégie d’accès partagé](media/send-events/shared-access-policy-2.png)  

## <a name="create-time-series-insights-event-source"></a><span data-ttu-id="f8ab1-116">Créer la source d’événement Time Series Insights</span><span class="sxs-lookup"><span data-stu-id="f8ab1-116">Create Time Series Insights event source</span></span>
1. <span data-ttu-id="f8ab1-117">Si vous n’avez créé aucune source d’événement, suivez [ces instructions](time-series-insights-add-event-source.md) pour créer une source d’événement.</span><span class="sxs-lookup"><span data-stu-id="f8ab1-117">If you haven't created an event source, follow [these instructions](time-series-insights-add-event-source.md) to create an event source.</span></span>

2. <span data-ttu-id="f8ab1-118">Spécifiez « deviceTimestamp » comme nom de la propriété timestamp. Cette propriété définit l’horodatage réel dans l’exemple csharp.</span><span class="sxs-lookup"><span data-stu-id="f8ab1-118">Specify “deviceTimestamp” as the timestamp property name – this property is used as the actual timestamp in the csharp sample.</span></span> <span data-ttu-id="f8ab1-119">Le nom de la propriété timestamp est sensible à la casse et les valeurs doivent être au format __aaaa-MM-jjTHH:mm:ss.FFFFFFFK__ lors de l’envoi au format JSON au concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="f8ab1-119">The timestamp property name is case-sensitive and values must follow the format __yyyy-MM-ddTHH:mm:ss.FFFFFFFK__ when sent as JSON to event hub.</span></span> <span data-ttu-id="f8ab1-120">Si la propriété n’existe pas dans l’événement, le système utilise l’heure à laquelle l’événement a été placé dans la file d’attente du concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="f8ab1-120">If the property does not exist in the event, then the event hub enqueued time is used.</span></span>

  ![Créez la source d’événement](media/send-events/event-source-1.png)

## <a name="sample-code-to-push-events"></a><span data-ttu-id="f8ab1-122">Exemple de code pour envoyer des événements</span><span class="sxs-lookup"><span data-stu-id="f8ab1-122">Sample code to push events</span></span>
1. <span data-ttu-id="f8ab1-123">Accédez à la stratégie de concentrateur d’événements « MySendPolicy » et copiez la chaîne de connexion avec la clé de stratégie.</span><span class="sxs-lookup"><span data-stu-id="f8ab1-123">Go to the event hub policy “MySendPolicy” and copy the connection string with the policy key.</span></span>

  ![Copiez la chaîne de connexion MySendPolicy](media/send-events/sample-code-connection-string.png)

2. <span data-ttu-id="f8ab1-125">Exécutez le code suivant qui envoie 600 événements pour chacun des trois appareils.</span><span class="sxs-lookup"><span data-stu-id="f8ab1-125">Run the following code that to send 600 events per each of the three devices.</span></span> <span data-ttu-id="f8ab1-126">Mettez à jour `eventHubConnectionString` avec votre chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="f8ab1-126">Update `eventHubConnectionString` with your connection string.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Globalization;
using System.IO;
using Microsoft.ServiceBus.Messaging;

namespace Microsoft.Rdx.DataGenerator
{
    internal class Program
    {
        private static void Main(string[] args)
        {
            var from = new DateTime(2017, 4, 20, 15, 0, 0, DateTimeKind.Utc);
            Random r = new Random();
            const int numberOfEvents = 600;

            var deviceIds = new[] { "device1", "device2", "device3" };

            var events = new List<string>();
            for (int i = 0; i < numberOfEvents; ++i)
            {
                for (int device = 0; device < deviceIds.Length; ++device)
                {
                    // Generate event and serialize as JSON object:
                    // { "deviceTimestamp": "utc timestamp", "deviceId": "guid", "value": 123.456 }
                    events.Add(
                        String.Format(
                            CultureInfo.InvariantCulture,
                            @"{{ ""deviceTimestamp"": ""{0}"", ""deviceId"": ""{1}"", ""value"": {2} }}",
                            (from + TimeSpan.FromSeconds(i * 30)).ToString("o"),
                            deviceIds[device],
                            r.NextDouble()));
                }
            }

            // Create event hub connection.
            var eventHubConnectionString = @"Endpoint=sb://...";
            var eventHubClient = EventHubClient.CreateFromConnectionString(eventHubConnectionString);

            using (var ms = new MemoryStream())
            using (var sw = new StreamWriter(ms))
            {
                // Wrap events into JSON array:
                sw.Write("[");
                for (int i = 0; i < events.Count; ++i)
                {
                    if (i > 0)
                    {
                        sw.Write(',');
                    }
                    sw.Write(events[i]);
                }
                sw.Write("]");

                sw.Flush();
                ms.Position = 0;

                // Send JSON to event hub.
                EventData eventData = new EventData(ms);
                eventHubClient.Send(eventData);
            }
        }
    }
}

```
## <a name="supported-json-shapes"></a><span data-ttu-id="f8ab1-127">Structures JSON prises en charge</span><span class="sxs-lookup"><span data-stu-id="f8ab1-127">Supported JSON shapes</span></span>
### <a name="sample-1"></a><span data-ttu-id="f8ab1-128">Exemple 1</span><span class="sxs-lookup"><span data-stu-id="f8ab1-128">Sample 1</span></span>

#### <a name="input"></a><span data-ttu-id="f8ab1-129">Entrée</span><span class="sxs-lookup"><span data-stu-id="f8ab1-129">Input</span></span>

<span data-ttu-id="f8ab1-130">Un objet JSON simple.</span><span class="sxs-lookup"><span data-stu-id="f8ab1-130">A simple JSON object.</span></span>

```json
{
    "id":"device1",
    "timestamp":"2016-01-08T01:08:00Z"
}
```
#### <a name="output---1-event"></a><span data-ttu-id="f8ab1-131">Sortie - 1 événement</span><span class="sxs-lookup"><span data-stu-id="f8ab1-131">Output - 1 event</span></span>

|<span data-ttu-id="f8ab1-132">id</span><span class="sxs-lookup"><span data-stu-id="f8ab1-132">id</span></span>|<span data-ttu-id="f8ab1-133">timestamp</span><span class="sxs-lookup"><span data-stu-id="f8ab1-133">timestamp</span></span>|
|--------|---------------|
|<span data-ttu-id="f8ab1-134">device1</span><span class="sxs-lookup"><span data-stu-id="f8ab1-134">device1</span></span>|<span data-ttu-id="f8ab1-135">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="f8ab1-135">2016-01-08T01:08:00Z</span></span>|

### <a name="sample-2"></a><span data-ttu-id="f8ab1-136">Exemple 2</span><span class="sxs-lookup"><span data-stu-id="f8ab1-136">Sample 2</span></span>

#### <a name="input"></a><span data-ttu-id="f8ab1-137">Entrée</span><span class="sxs-lookup"><span data-stu-id="f8ab1-137">Input</span></span>
<span data-ttu-id="f8ab1-138">Un tableau JSON avec deux objets JSON.</span><span class="sxs-lookup"><span data-stu-id="f8ab1-138">A JSON array with two JSON objects.</span></span> <span data-ttu-id="f8ab1-139">Chaque objet JSON sera converti en un événement.</span><span class="sxs-lookup"><span data-stu-id="f8ab1-139">Each JSON object will be converted to an event.</span></span>
```json
[
    {
        "id":"device1",
        "timestamp":"2016-01-08T01:08:00Z"
    },
    {
        "id":"device2",
        "timestamp":"2016-01-17T01:17:00Z"
    }
]
```
#### <a name="output---2-events"></a><span data-ttu-id="f8ab1-140">Sortie - 2 événements</span><span class="sxs-lookup"><span data-stu-id="f8ab1-140">Output - 2 Events</span></span>

|<span data-ttu-id="f8ab1-141">id</span><span class="sxs-lookup"><span data-stu-id="f8ab1-141">id</span></span>|<span data-ttu-id="f8ab1-142">timestamp</span><span class="sxs-lookup"><span data-stu-id="f8ab1-142">timestamp</span></span>|
|--------|---------------|
|<span data-ttu-id="f8ab1-143">device1</span><span class="sxs-lookup"><span data-stu-id="f8ab1-143">device1</span></span>|<span data-ttu-id="f8ab1-144">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="f8ab1-144">2016-01-08T01:08:00Z</span></span>|
|<span data-ttu-id="f8ab1-145">device2</span><span class="sxs-lookup"><span data-stu-id="f8ab1-145">device2</span></span>|<span data-ttu-id="f8ab1-146">2016-01-08T01:17:00Z</span><span class="sxs-lookup"><span data-stu-id="f8ab1-146">2016-01-08T01:17:00Z</span></span>|
### <a name="sample-3"></a><span data-ttu-id="f8ab1-147">Exemple 3</span><span class="sxs-lookup"><span data-stu-id="f8ab1-147">Sample 3</span></span>

#### <a name="input"></a><span data-ttu-id="f8ab1-148">Entrée</span><span class="sxs-lookup"><span data-stu-id="f8ab1-148">Input</span></span>

<span data-ttu-id="f8ab1-149">Un objet JSON avec un tableau JSON imbriqué contenant deux objets JSON.</span><span class="sxs-lookup"><span data-stu-id="f8ab1-149">A JSON object with a nested JSON array containing two JSON objects.</span></span>
```json
{
    "location":"WestUs",
    "events":[
        {
            "id":"device1",
            "timestamp":"2016-01-08T01:08:00Z"
        },
        {
            "id":"device2",
            "timestamp":"2016-01-17T01:17:00Z"
        }
    ]
}

```
#### <a name="output---2-events"></a><span data-ttu-id="f8ab1-150">Sortie - 2 événements</span><span class="sxs-lookup"><span data-stu-id="f8ab1-150">Output - 2 Events</span></span>
<span data-ttu-id="f8ab1-151">Notez que la propriété « location » est copiée dans chacun des événements.</span><span class="sxs-lookup"><span data-stu-id="f8ab1-151">Note that the property "location" is copied over to each of the event.</span></span>

|<span data-ttu-id="f8ab1-152">location</span><span class="sxs-lookup"><span data-stu-id="f8ab1-152">location</span></span>|<span data-ttu-id="f8ab1-153">events.id</span><span class="sxs-lookup"><span data-stu-id="f8ab1-153">events.id</span></span>|<span data-ttu-id="f8ab1-154">events.timestamp</span><span class="sxs-lookup"><span data-stu-id="f8ab1-154">events.timestamp</span></span>|
|--------|---------------|----------------------|
|<span data-ttu-id="f8ab1-155">WestUs</span><span class="sxs-lookup"><span data-stu-id="f8ab1-155">WestUs</span></span>|<span data-ttu-id="f8ab1-156">device1</span><span class="sxs-lookup"><span data-stu-id="f8ab1-156">device1</span></span>|<span data-ttu-id="f8ab1-157">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="f8ab1-157">2016-01-08T01:08:00Z</span></span>|
|<span data-ttu-id="f8ab1-158">WestUs</span><span class="sxs-lookup"><span data-stu-id="f8ab1-158">WestUs</span></span>|<span data-ttu-id="f8ab1-159">device2</span><span class="sxs-lookup"><span data-stu-id="f8ab1-159">device2</span></span>|<span data-ttu-id="f8ab1-160">2016-01-08T01:17:00Z</span><span class="sxs-lookup"><span data-stu-id="f8ab1-160">2016-01-08T01:17:00Z</span></span>|

### <a name="sample-4"></a><span data-ttu-id="f8ab1-161">Exemple 4</span><span class="sxs-lookup"><span data-stu-id="f8ab1-161">Sample 4</span></span>

#### <a name="input"></a><span data-ttu-id="f8ab1-162">Entrée</span><span class="sxs-lookup"><span data-stu-id="f8ab1-162">Input</span></span>

<span data-ttu-id="f8ab1-163">Un objet JSON avec un tableau JSON imbriqué contenant deux objets JSON.</span><span class="sxs-lookup"><span data-stu-id="f8ab1-163">A JSON object with a nested JSON array containing two JSON objects.</span></span> <span data-ttu-id="f8ab1-164">Cette entrée montre que les propriétés globales peuvent être représentées par l’objet JSON complexe.</span><span class="sxs-lookup"><span data-stu-id="f8ab1-164">This input demonstrates that the global properties may be represented by the complex JSON object.</span></span>

```json
{
    "location":"WestUs",
    "manufacturer":{
        "name":"manufacturer1",
        "location":"EastUs"
    },
    "events":[
        {
            "id":"device1",
            "timestamp":"2016-01-08T01:08:00Z",
            "data":{
                "type":"pressure",
                "units":"psi",
                "value":108.09
            }
        },
        {
            "id":"device2",
            "timestamp":"2016-01-17T01:17:00Z",
            "data":{
                "type":"vibration",
                "units":"abs G",
                "value":217.09
            }
        }
    ]
}
```
#### <a name="output---2-events"></a><span data-ttu-id="f8ab1-165">Sortie - 2 événements</span><span class="sxs-lookup"><span data-stu-id="f8ab1-165">Output - 2 Events</span></span>

|<span data-ttu-id="f8ab1-166">location</span><span class="sxs-lookup"><span data-stu-id="f8ab1-166">location</span></span>|<span data-ttu-id="f8ab1-167">manufacturer.name</span><span class="sxs-lookup"><span data-stu-id="f8ab1-167">manufacturer.name</span></span>|<span data-ttu-id="f8ab1-168">manufacturer.location</span><span class="sxs-lookup"><span data-stu-id="f8ab1-168">manufacturer.location</span></span>|<span data-ttu-id="f8ab1-169">events.id</span><span class="sxs-lookup"><span data-stu-id="f8ab1-169">events.id</span></span>|<span data-ttu-id="f8ab1-170">events.timestamp</span><span class="sxs-lookup"><span data-stu-id="f8ab1-170">events.timestamp</span></span>|<span data-ttu-id="f8ab1-171">events.data.type</span><span class="sxs-lookup"><span data-stu-id="f8ab1-171">events.data.type</span></span>|<span data-ttu-id="f8ab1-172">events.data.units</span><span class="sxs-lookup"><span data-stu-id="f8ab1-172">events.data.units</span></span>|<span data-ttu-id="f8ab1-173">events.data.value</span><span class="sxs-lookup"><span data-stu-id="f8ab1-173">events.data.value</span></span>|
|---|---|---|---|---|---|---|---|
|<span data-ttu-id="f8ab1-174">WestUs</span><span class="sxs-lookup"><span data-stu-id="f8ab1-174">WestUs</span></span>|<span data-ttu-id="f8ab1-175">manufacturer1</span><span class="sxs-lookup"><span data-stu-id="f8ab1-175">manufacturer1</span></span>|<span data-ttu-id="f8ab1-176">EastUs</span><span class="sxs-lookup"><span data-stu-id="f8ab1-176">EastUs</span></span>|<span data-ttu-id="f8ab1-177">device1</span><span class="sxs-lookup"><span data-stu-id="f8ab1-177">device1</span></span>|<span data-ttu-id="f8ab1-178">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="f8ab1-178">2016-01-08T01:08:00Z</span></span>|<span data-ttu-id="f8ab1-179">pressure</span><span class="sxs-lookup"><span data-stu-id="f8ab1-179">pressure</span></span>|<span data-ttu-id="f8ab1-180">psi</span><span class="sxs-lookup"><span data-stu-id="f8ab1-180">psi</span></span>|<span data-ttu-id="f8ab1-181">108.09</span><span class="sxs-lookup"><span data-stu-id="f8ab1-181">108.09</span></span>|
|<span data-ttu-id="f8ab1-182">WestUs</span><span class="sxs-lookup"><span data-stu-id="f8ab1-182">WestUs</span></span>|<span data-ttu-id="f8ab1-183">manufacturer1</span><span class="sxs-lookup"><span data-stu-id="f8ab1-183">manufacturer1</span></span>|<span data-ttu-id="f8ab1-184">EastUs</span><span class="sxs-lookup"><span data-stu-id="f8ab1-184">EastUs</span></span>|<span data-ttu-id="f8ab1-185">device2</span><span class="sxs-lookup"><span data-stu-id="f8ab1-185">device2</span></span>|<span data-ttu-id="f8ab1-186">2016-01-08T01:17:00Z</span><span class="sxs-lookup"><span data-stu-id="f8ab1-186">2016-01-08T01:17:00Z</span></span>|<span data-ttu-id="f8ab1-187">vibration</span><span class="sxs-lookup"><span data-stu-id="f8ab1-187">vibration</span></span>|<span data-ttu-id="f8ab1-188">abs G</span><span class="sxs-lookup"><span data-stu-id="f8ab1-188">abs G</span></span>|<span data-ttu-id="f8ab1-189">217.09</span><span class="sxs-lookup"><span data-stu-id="f8ab1-189">217.09</span></span>|

## <a name="next-steps"></a><span data-ttu-id="f8ab1-190">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f8ab1-190">Next steps</span></span>

* <span data-ttu-id="f8ab1-191">Afficher votre environnement dans le [Portail Time Series Insights](https://insights.timeseries.azure.com)</span><span class="sxs-lookup"><span data-stu-id="f8ab1-191">View your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
