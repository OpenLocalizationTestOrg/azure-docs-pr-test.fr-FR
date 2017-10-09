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
# <a name="send-events-tooa-time-series-insights-environment-using-event-hub"></a>Environnement d’heure série Insights tooa événements à l’aide de concentrateur d’événements d’envoi

Ce didacticiel explique comment toocreate et configurer le concentrateur d’événements et exécuter un toopush d’application exemple d’événement. Si vous disposez d’un concentrateur d’événements existant qui a déjà des événements au format JSON, ignorez ce didacticiel et affichez votre environnement dans [time series insights](https://insights.timeseries.azure.com).

## <a name="configure-an-event-hub"></a>Configurer un concentrateur d’événements
1. toocreate un concentrateur d’événements, suivez les instructions de hello concentrateur d’événements [documentation](https://docs.microsoft.com/azure/event-hubs/event-hubs-create).

2. Veillez à créer un groupe de consommateurs qui sera utilisé exclusivement par votre source d’événement Time Series Insights.

  > [!IMPORTANT]
  > Assurez-vous que ce groupe de consommateurs n’est pas utilisé par un autre service (par exemple, une tâche Stream Analytics ou un autre environnement Time Series Insights). Si le groupe de consommateurs est utilisé par d’autres services, lisez opération affectée pour cet environnement et hello d’autres services. Si vous utilisez « $Default » en tant que groupe de consommateurs hello, il risque de réutilisation de toopotential par les autres lecteurs.

  ![Sélectionnez le groupe de consommateurs du concentrateur d’événements](media/send-events/consumer-group.png)

3. Créer des « MySendPolicy » sur le concentrateur d’événements hello, c'est-à-dire les événements de toosend utilisés dans hello, exemple csharp.

  ![Sélectionnez des stratégies d’accès partagé et cliquez sur le bouton Ajouter](media/send-events/shared-access-policy.png)  

  ![Ajoutez une stratégie d’accès partagé](media/send-events/shared-access-policy-2.png)  

## <a name="create-time-series-insights-event-source"></a>Créer la source d’événement Time Series Insights
1. Si vous n’avez pas créé une source d’événements, procédez comme [ces instructions](time-series-insights-add-event-source.md) toocreate une source d’événement.

2. Spécifiez « deviceTimestamp » comme nom de la propriété timestamp hello : cette propriété est utilisée comme hello horodatage réelle dans hello, exemple csharp. nom de la propriété timestamp Hello respecte la casse et les valeurs doivent suivre le format de hello __AAAA-MM-JJThh. FFFFFFFK__ lors de l’envoi comme concentrateur tooevent JSON. Si la propriété de hello n’existe pas dans les événements hello, puis hello heure de l’événement hub en file d’attente est utilisé.

  ![Créez la source d’événement](media/send-events/event-source-1.png)

## <a name="sample-code-toopush-events"></a>Exemples d’événements toopush code
1. Accédez de stratégie de concentrateur d’événements toohello « MySendPolicy » et copier la chaîne de connexion hello avec la clé de stratégie hello.

  ![Copiez la chaîne de connexion MySendPolicy](media/send-events/sample-code-connection-string.png)

2. Exécutez hello après le code que les événements par chacun des périphériques de hello trois toosend 600. Mettez à jour `eventHubConnectionString` avec votre chaîne de connexion.

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
## <a name="supported-json-shapes"></a>Structures JSON prises en charge
### <a name="sample-1"></a>Exemple 1

#### <a name="input"></a>Entrée

Un objet JSON simple.

```json
{
    "id":"device1",
    "timestamp":"2016-01-08T01:08:00Z"
}
```
#### <a name="output---1-event"></a>Sortie - 1 événement

|id|timestamp|
|--------|---------------|
|device1|2016-01-08T01:08:00Z|

### <a name="sample-2"></a>Exemple 2

#### <a name="input"></a>Entrée
Un tableau JSON avec deux objets JSON. Chaque objet JSON sera convertie tooan événement.
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
#### <a name="output---2-events"></a>Sortie - 2 événements

|id|timestamp|
|--------|---------------|
|device1|2016-01-08T01:08:00Z|
|device2|2016-01-08T01:17:00Z|
### <a name="sample-3"></a>Exemple 3

#### <a name="input"></a>Entrée

Un objet JSON avec un tableau JSON imbriqué contenant deux objets JSON.
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
#### <a name="output---2-events"></a>Sortie - 2 événements
Notez que la propriété de hello « location » est copiée via tooeach d’événement de hello.

|location|events.id|events.timestamp|
|--------|---------------|----------------------|
|WestUs|device1|2016-01-08T01:08:00Z|
|WestUs|device2|2016-01-08T01:17:00Z|

### <a name="sample-4"></a>Exemple 4

#### <a name="input"></a>Entrée

Un objet JSON avec un tableau JSON imbriqué contenant deux objets JSON. Cette entrée montre que les propriétés globales de hello peuvent être représentées par l’objet JSON complexe de hello.

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
#### <a name="output---2-events"></a>Sortie - 2 événements

|location|manufacturer.name|manufacturer.location|events.id|events.timestamp|events.data.type|events.data.units|events.data.value|
|---|---|---|---|---|---|---|---|
|WestUs|manufacturer1|EastUs|device1|2016-01-08T01:08:00Z|pressure|psi|108.09|
|WestUs|manufacturer1|EastUs|device2|2016-01-08T01:17:00Z|vibration|abs G|217.09|

## <a name="next-steps"></a>Étapes suivantes

* Afficher votre environnement dans le [Portail Time Series Insights](https://insights.timeseries.azure.com)
