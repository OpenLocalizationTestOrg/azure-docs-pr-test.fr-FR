---
title: "environnement d’heure série Insights aaaSend événements tooAzure | Documents Microsoft"
description: "Ce didacticiel décrit l’environnement de temps série Insights hello étapes toopush événements tooyour"
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
ms.openlocfilehash: dbccc23f61351a0033cd48c1a02fb3841b45d560
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="send-events-tooa-time-series-insights-environment-using-event-hub"></a><span data-ttu-id="d774d-103">Environnement d’heure série Insights tooa événements à l’aide de concentrateur d’événements d’envoi</span><span class="sxs-lookup"><span data-stu-id="d774d-103">Send events tooa Time Series Insights environment using event hub</span></span>

<span data-ttu-id="d774d-104">Ce didacticiel explique comment toocreate et configurer le concentrateur d’événements et exécuter un toopush d’application exemple d’événement.</span><span class="sxs-lookup"><span data-stu-id="d774d-104">This tutorial explains how toocreate and configure event hub and run a sample application toopush events.</span></span> <span data-ttu-id="d774d-105">Si vous disposez d’un concentrateur d’événements existant qui a déjà des événements au format JSON, ignorez ce didacticiel et affichez votre environnement dans [time series insights](https://insights.timeseries.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d774d-105">If you have an existing event hub with events in JSON format, skip this tutorial and view your environment in [time series insights](https://insights.timeseries.azure.com).</span></span>

## <a name="configure-an-event-hub"></a><span data-ttu-id="d774d-106">Configurer un concentrateur d’événements</span><span class="sxs-lookup"><span data-stu-id="d774d-106">Configure an event hub</span></span>
1. <span data-ttu-id="d774d-107">toocreate un concentrateur d’événements, suivez les instructions de hello concentrateur d’événements [documentation](https://docs.microsoft.com/azure/event-hubs/event-hubs-create).</span><span class="sxs-lookup"><span data-stu-id="d774d-107">toocreate an event hub, follow instructions from hello Event Hub [documentation](https://docs.microsoft.com/azure/event-hubs/event-hubs-create).</span></span>

2. <span data-ttu-id="d774d-108">Veillez à créer un groupe de consommateurs qui sera utilisé exclusivement par votre source d’événement Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="d774d-108">Make sure you create a consumer group that is used exclusively by your Time Series Insights event source.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="d774d-109">Assurez-vous que ce groupe de consommateurs n’est pas utilisé par un autre service (par exemple, une tâche Stream Analytics ou un autre environnement Time Series Insights).</span><span class="sxs-lookup"><span data-stu-id="d774d-109">Make sure this consumer group is not used by any other service (such as Stream Analytics job or another Time Series Insights environment).</span></span> <span data-ttu-id="d774d-110">Si le groupe de consommateurs est utilisé par d’autres services, lisez opération affectée pour cet environnement et hello d’autres services.</span><span class="sxs-lookup"><span data-stu-id="d774d-110">If consumer group is used by other services, read operation is negatively affected for this environment and hello other services.</span></span> <span data-ttu-id="d774d-111">Si vous utilisez « $Default » en tant que groupe de consommateurs hello, il risque de réutilisation de toopotential par les autres lecteurs.</span><span class="sxs-lookup"><span data-stu-id="d774d-111">If you are using “$Default” as hello consumer group, it could lead toopotential reuse by other readers.</span></span>

  ![Sélectionnez le groupe de consommateurs du concentrateur d’événements](media/send-events/consumer-group.png)

3. <span data-ttu-id="d774d-113">Créer des « MySendPolicy » sur le concentrateur d’événements hello, c'est-à-dire les événements de toosend utilisés dans hello, exemple csharp.</span><span class="sxs-lookup"><span data-stu-id="d774d-113">On hello event hub, create “MySendPolicy” that is used toosend events in hello csharp sample.</span></span>

  ![Sélectionnez des stratégies d’accès partagé et cliquez sur le bouton Ajouter](media/send-events/shared-access-policy.png)  

  ![Ajoutez une stratégie d’accès partagé](media/send-events/shared-access-policy-2.png)  

## <a name="create-time-series-insights-event-source"></a><span data-ttu-id="d774d-116">Créer la source d’événement Time Series Insights</span><span class="sxs-lookup"><span data-stu-id="d774d-116">Create Time Series Insights event source</span></span>
1. <span data-ttu-id="d774d-117">Si vous n’avez pas créé une source d’événements, procédez comme [ces instructions](time-series-insights-add-event-source.md) toocreate une source d’événement.</span><span class="sxs-lookup"><span data-stu-id="d774d-117">If you haven't created an event source, follow [these instructions](time-series-insights-add-event-source.md) toocreate an event source.</span></span>

2. <span data-ttu-id="d774d-118">Spécifiez « deviceTimestamp » comme nom de la propriété timestamp hello : cette propriété est utilisée comme hello horodatage réelle dans hello, exemple csharp.</span><span class="sxs-lookup"><span data-stu-id="d774d-118">Specify “deviceTimestamp” as hello timestamp property name – this property is used as hello actual timestamp in hello csharp sample.</span></span> <span data-ttu-id="d774d-119">nom de la propriété timestamp Hello respecte la casse et les valeurs doivent suivre le format de hello __AAAA-MM-JJThh. FFFFFFFK__ lors de l’envoi comme concentrateur tooevent JSON.</span><span class="sxs-lookup"><span data-stu-id="d774d-119">hello timestamp property name is case-sensitive and values must follow hello format __yyyy-MM-ddTHH:mm:ss.FFFFFFFK__ when sent as JSON tooevent hub.</span></span> <span data-ttu-id="d774d-120">Si la propriété de hello n’existe pas dans les événements hello, puis hello heure de l’événement hub en file d’attente est utilisé.</span><span class="sxs-lookup"><span data-stu-id="d774d-120">If hello property does not exist in hello event, then hello event hub enqueued time is used.</span></span>

  ![Créez la source d’événement](media/send-events/event-source-1.png)

## <a name="sample-code-toopush-events"></a><span data-ttu-id="d774d-122">Exemples d’événements toopush code</span><span class="sxs-lookup"><span data-stu-id="d774d-122">Sample code toopush events</span></span>
1. <span data-ttu-id="d774d-123">Accédez de stratégie de concentrateur d’événements toohello « MySendPolicy » et copier la chaîne de connexion hello avec la clé de stratégie hello.</span><span class="sxs-lookup"><span data-stu-id="d774d-123">Go toohello event hub policy “MySendPolicy” and copy hello connection string with hello policy key.</span></span>

  ![Copiez la chaîne de connexion MySendPolicy](media/send-events/sample-code-connection-string.png)

2. <span data-ttu-id="d774d-125">Exécutez hello après le code que les événements par chacun des périphériques de hello trois toosend 600.</span><span class="sxs-lookup"><span data-stu-id="d774d-125">Run hello following code that toosend 600 events per each of hello three devices.</span></span> <span data-ttu-id="d774d-126">Mettez à jour `eventHubConnectionString` avec votre chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="d774d-126">Update `eventHubConnectionString` with your connection string.</span></span>

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

                // Send JSON tooevent hub.
                EventData eventData = new EventData(ms);
                eventHubClient.Send(eventData);
            }
        }
    }
}

```
## <a name="supported-json-shapes"></a><span data-ttu-id="d774d-127">Structures JSON prises en charge</span><span class="sxs-lookup"><span data-stu-id="d774d-127">Supported JSON shapes</span></span>
### <a name="sample-1"></a><span data-ttu-id="d774d-128">Exemple 1</span><span class="sxs-lookup"><span data-stu-id="d774d-128">Sample 1</span></span>

#### <a name="input"></a><span data-ttu-id="d774d-129">Entrée</span><span class="sxs-lookup"><span data-stu-id="d774d-129">Input</span></span>

<span data-ttu-id="d774d-130">Un objet JSON simple.</span><span class="sxs-lookup"><span data-stu-id="d774d-130">A simple JSON object.</span></span>

```json
{
    "id":"device1",
    "timestamp":"2016-01-08T01:08:00Z"
}
```
#### <a name="output---1-event"></a><span data-ttu-id="d774d-131">Sortie - 1 événement</span><span class="sxs-lookup"><span data-stu-id="d774d-131">Output - 1 event</span></span>

|<span data-ttu-id="d774d-132">id</span><span class="sxs-lookup"><span data-stu-id="d774d-132">id</span></span>|<span data-ttu-id="d774d-133">timestamp</span><span class="sxs-lookup"><span data-stu-id="d774d-133">timestamp</span></span>|
|--------|---------------|
|<span data-ttu-id="d774d-134">device1</span><span class="sxs-lookup"><span data-stu-id="d774d-134">device1</span></span>|<span data-ttu-id="d774d-135">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="d774d-135">2016-01-08T01:08:00Z</span></span>|

### <a name="sample-2"></a><span data-ttu-id="d774d-136">Exemple 2</span><span class="sxs-lookup"><span data-stu-id="d774d-136">Sample 2</span></span>

#### <a name="input"></a><span data-ttu-id="d774d-137">Entrée</span><span class="sxs-lookup"><span data-stu-id="d774d-137">Input</span></span>
<span data-ttu-id="d774d-138">Un tableau JSON avec deux objets JSON.</span><span class="sxs-lookup"><span data-stu-id="d774d-138">A JSON array with two JSON objects.</span></span> <span data-ttu-id="d774d-139">Chaque objet JSON sera convertie tooan événement.</span><span class="sxs-lookup"><span data-stu-id="d774d-139">Each JSON object will be converted tooan event.</span></span>
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
#### <a name="output---2-events"></a><span data-ttu-id="d774d-140">Sortie - 2 événements</span><span class="sxs-lookup"><span data-stu-id="d774d-140">Output - 2 Events</span></span>

|<span data-ttu-id="d774d-141">id</span><span class="sxs-lookup"><span data-stu-id="d774d-141">id</span></span>|<span data-ttu-id="d774d-142">timestamp</span><span class="sxs-lookup"><span data-stu-id="d774d-142">timestamp</span></span>|
|--------|---------------|
|<span data-ttu-id="d774d-143">device1</span><span class="sxs-lookup"><span data-stu-id="d774d-143">device1</span></span>|<span data-ttu-id="d774d-144">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="d774d-144">2016-01-08T01:08:00Z</span></span>|
|<span data-ttu-id="d774d-145">device2</span><span class="sxs-lookup"><span data-stu-id="d774d-145">device2</span></span>|<span data-ttu-id="d774d-146">2016-01-08T01:17:00Z</span><span class="sxs-lookup"><span data-stu-id="d774d-146">2016-01-08T01:17:00Z</span></span>|
### <a name="sample-3"></a><span data-ttu-id="d774d-147">Exemple 3</span><span class="sxs-lookup"><span data-stu-id="d774d-147">Sample 3</span></span>

#### <a name="input"></a><span data-ttu-id="d774d-148">Entrée</span><span class="sxs-lookup"><span data-stu-id="d774d-148">Input</span></span>

<span data-ttu-id="d774d-149">Un objet JSON avec un tableau JSON imbriqué contenant deux objets JSON.</span><span class="sxs-lookup"><span data-stu-id="d774d-149">A JSON object with a nested JSON array containing two JSON objects.</span></span>
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
#### <a name="output---2-events"></a><span data-ttu-id="d774d-150">Sortie - 2 événements</span><span class="sxs-lookup"><span data-stu-id="d774d-150">Output - 2 Events</span></span>
<span data-ttu-id="d774d-151">Notez que la propriété de hello « location » est copiée via tooeach d’événement de hello.</span><span class="sxs-lookup"><span data-stu-id="d774d-151">Note that hello property "location" is copied over tooeach of hello event.</span></span>

|<span data-ttu-id="d774d-152">location</span><span class="sxs-lookup"><span data-stu-id="d774d-152">location</span></span>|<span data-ttu-id="d774d-153">events.id</span><span class="sxs-lookup"><span data-stu-id="d774d-153">events.id</span></span>|<span data-ttu-id="d774d-154">events.timestamp</span><span class="sxs-lookup"><span data-stu-id="d774d-154">events.timestamp</span></span>|
|--------|---------------|----------------------|
|<span data-ttu-id="d774d-155">WestUs</span><span class="sxs-lookup"><span data-stu-id="d774d-155">WestUs</span></span>|<span data-ttu-id="d774d-156">device1</span><span class="sxs-lookup"><span data-stu-id="d774d-156">device1</span></span>|<span data-ttu-id="d774d-157">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="d774d-157">2016-01-08T01:08:00Z</span></span>|
|<span data-ttu-id="d774d-158">WestUs</span><span class="sxs-lookup"><span data-stu-id="d774d-158">WestUs</span></span>|<span data-ttu-id="d774d-159">device2</span><span class="sxs-lookup"><span data-stu-id="d774d-159">device2</span></span>|<span data-ttu-id="d774d-160">2016-01-08T01:17:00Z</span><span class="sxs-lookup"><span data-stu-id="d774d-160">2016-01-08T01:17:00Z</span></span>|

### <a name="sample-4"></a><span data-ttu-id="d774d-161">Exemple 4</span><span class="sxs-lookup"><span data-stu-id="d774d-161">Sample 4</span></span>

#### <a name="input"></a><span data-ttu-id="d774d-162">Entrée</span><span class="sxs-lookup"><span data-stu-id="d774d-162">Input</span></span>

<span data-ttu-id="d774d-163">Un objet JSON avec un tableau JSON imbriqué contenant deux objets JSON.</span><span class="sxs-lookup"><span data-stu-id="d774d-163">A JSON object with a nested JSON array containing two JSON objects.</span></span> <span data-ttu-id="d774d-164">Cette entrée montre que les propriétés globales de hello peuvent être représentées par l’objet JSON complexe de hello.</span><span class="sxs-lookup"><span data-stu-id="d774d-164">This input demonstrates that hello global properties may be represented by hello complex JSON object.</span></span>

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
#### <a name="output---2-events"></a><span data-ttu-id="d774d-165">Sortie - 2 événements</span><span class="sxs-lookup"><span data-stu-id="d774d-165">Output - 2 Events</span></span>

|<span data-ttu-id="d774d-166">location</span><span class="sxs-lookup"><span data-stu-id="d774d-166">location</span></span>|<span data-ttu-id="d774d-167">manufacturer.name</span><span class="sxs-lookup"><span data-stu-id="d774d-167">manufacturer.name</span></span>|<span data-ttu-id="d774d-168">manufacturer.location</span><span class="sxs-lookup"><span data-stu-id="d774d-168">manufacturer.location</span></span>|<span data-ttu-id="d774d-169">events.id</span><span class="sxs-lookup"><span data-stu-id="d774d-169">events.id</span></span>|<span data-ttu-id="d774d-170">events.timestamp</span><span class="sxs-lookup"><span data-stu-id="d774d-170">events.timestamp</span></span>|<span data-ttu-id="d774d-171">events.data.type</span><span class="sxs-lookup"><span data-stu-id="d774d-171">events.data.type</span></span>|<span data-ttu-id="d774d-172">events.data.units</span><span class="sxs-lookup"><span data-stu-id="d774d-172">events.data.units</span></span>|<span data-ttu-id="d774d-173">events.data.value</span><span class="sxs-lookup"><span data-stu-id="d774d-173">events.data.value</span></span>|
|---|---|---|---|---|---|---|---|
|<span data-ttu-id="d774d-174">WestUs</span><span class="sxs-lookup"><span data-stu-id="d774d-174">WestUs</span></span>|<span data-ttu-id="d774d-175">manufacturer1</span><span class="sxs-lookup"><span data-stu-id="d774d-175">manufacturer1</span></span>|<span data-ttu-id="d774d-176">EastUs</span><span class="sxs-lookup"><span data-stu-id="d774d-176">EastUs</span></span>|<span data-ttu-id="d774d-177">device1</span><span class="sxs-lookup"><span data-stu-id="d774d-177">device1</span></span>|<span data-ttu-id="d774d-178">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="d774d-178">2016-01-08T01:08:00Z</span></span>|<span data-ttu-id="d774d-179">pressure</span><span class="sxs-lookup"><span data-stu-id="d774d-179">pressure</span></span>|<span data-ttu-id="d774d-180">psi</span><span class="sxs-lookup"><span data-stu-id="d774d-180">psi</span></span>|<span data-ttu-id="d774d-181">108.09</span><span class="sxs-lookup"><span data-stu-id="d774d-181">108.09</span></span>|
|<span data-ttu-id="d774d-182">WestUs</span><span class="sxs-lookup"><span data-stu-id="d774d-182">WestUs</span></span>|<span data-ttu-id="d774d-183">manufacturer1</span><span class="sxs-lookup"><span data-stu-id="d774d-183">manufacturer1</span></span>|<span data-ttu-id="d774d-184">EastUs</span><span class="sxs-lookup"><span data-stu-id="d774d-184">EastUs</span></span>|<span data-ttu-id="d774d-185">device2</span><span class="sxs-lookup"><span data-stu-id="d774d-185">device2</span></span>|<span data-ttu-id="d774d-186">2016-01-08T01:17:00Z</span><span class="sxs-lookup"><span data-stu-id="d774d-186">2016-01-08T01:17:00Z</span></span>|<span data-ttu-id="d774d-187">vibration</span><span class="sxs-lookup"><span data-stu-id="d774d-187">vibration</span></span>|<span data-ttu-id="d774d-188">abs G</span><span class="sxs-lookup"><span data-stu-id="d774d-188">abs G</span></span>|<span data-ttu-id="d774d-189">217.09</span><span class="sxs-lookup"><span data-stu-id="d774d-189">217.09</span></span>|

## <a name="next-steps"></a><span data-ttu-id="d774d-190">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d774d-190">Next steps</span></span>

* <span data-ttu-id="d774d-191">Afficher votre environnement dans le [Portail Time Series Insights](https://insights.timeseries.azure.com)</span><span class="sxs-lookup"><span data-stu-id="d774d-191">View your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
