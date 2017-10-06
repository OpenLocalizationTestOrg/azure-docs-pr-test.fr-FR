---
title: "surveillance des opérations IoT Hub aaaAzure | Documents Microsoft"
description: "Comment les opérations de Azure IoT Hub toouse analyse toomonitor hello état des opérations sur votre IoT hub en temps réel."
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: a299f3a5-b14d-4586-9c3b-44aea14ed013
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.openlocfilehash: a0b233ef2d9bd0827e19fa30fdbdd49b2b61b813
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="iot-hub-operations-monitoring"></a>Surveillance des opérations IoT Hub

Surveillance des opérations IoT Hub vous permet d’état de hello toomonitor des opérations sur votre IoT hub en temps réel. IoT Hub effectue le suivi des événements entre différentes catégories d’opérations. Vous pouvez choisir d’envoyer des événements à partir d’une ou plusieurs catégories tooan point de terminaison de votre hub IoT pour le traitement. Vous pouvez analyser les données hello pour les erreurs ou configurer un traitement plus complexe basé sur des modèles de données.

IoT Hub surveille six catégories d’événements :

* Opérations d’identité des appareils
* Télémétrie d’appareil
* Messages Cloud à appareil
* Connexions
* Chargements de fichiers
* Routage de messages

## <a name="how-tooenable-operations-monitoring"></a>La surveillance des opérations tooenable

1. Créez un hub IoT. Vous trouverez des instructions sur la façon de toocreate un hub IoT Bonjour [prise en main] [ lnk-get-started] guide.

1. Ouvrez le panneau hello de votre hub IoT. De là, cliquez sur **Surveillance des opérations**.

    ![Opérations d’accès hello portail d’analyse][1]

1. Hello Sélectionnez analyse des catégories que vous souhaitez toomonitor, puis cliquez sur **enregistrer**. Hello événements sont disponibles pour la lecture à partir du point de terminaison hello compatible concentrateur d’événements répertoriée dans **paramètres d’analyse**. Hello point de terminaison IoT Hub est appelée `messages/operationsmonitoringevents`.

    ![Configurer la surveillance des opérations sur votre IoT Hub][2]

> [!NOTE]
> En sélectionnant **Verbose** analyse pour hello **connexions** catégorie provoque IoT Hub toogenerate les messages de diagnostic supplémentaires. Pour toutes les autres catégories, hello **Verbose** inclut les modifications apportées au paramètre quantité hello d’informations IoT Hub dans chaque message d’erreur.

## <a name="event-categories-and-how-toouse-them"></a>Catégories d’événements et comment toouse les

Chaque catégorie de surveillance d’opérations assure le suivi d’un type spécifique d’interaction avec IoT Hub et a un schéma qui définit la façon dont sont structurés les événements qu’elle comporte.

### <a name="device-identity-operations"></a>Opérations d’identité des appareils

catégorie d’opérations Hello appareils identité effectue le suivi des erreurs qui se produisent lorsque vous essayez de toocreate, mettre à jour ou supprimer une entrée dans le Registre des identités de votre hub IoT. Le suivi de cette catégorie est utile pour les scénarios d’approvisionnement.

```json
{
    "time": "UTC timestamp",
        "operationName": "create",
        "category": "DeviceIdentityOperations",
        "level": "Error",
        "statusCode": 4XX,
        "statusDescription": "MessageDescription",
        "deviceId": "device-ID",
        "durationMs": 1234,
        "userAgent": "userAgent",
        "sharedAccessPolicy": "accessPolicy"
}
```

### <a name="device-telemetry"></a>Télémétrie d’appareil

catégorie de télémétrie de périphérique Hello effectue le suivi des erreurs qui se produisent au hub IoT de hello et sont le pipeline de télémétrie toohello connexes. Cette catégorie inclut notamment les erreurs concernant l’envoi d’événements de télémétrie (par exemple, une limitation) et la réception des événements de télémétrie (par exemple, un lecteur non autorisé). Cette catégorie ne peut pas intercepter des erreurs provoquées par le code en cours d’exécution sur l’appareil hello lui-même.

```json
{
        "messageSizeInBytes": 1234,
        "batching": 0,
        "protocol": "Amqp",
        "authType": "{\"scope\":\"device\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
        "time": "UTC timestamp",
        "operationName": "ingress",
        "category": "DeviceTelemetry",
        "level": "Error",
        "statusCode": 4XX,
        "statusType": 4XX001,
        "statusDescription": "MessageDescription",
        "deviceId": "device-ID",
        "EventProcessedUtcTime": "UTC timestamp",
        "PartitionId": 1,
        "EventEnqueuedUtcTime": "UTC timestamp"
}
```

### <a name="cloud-to-device-commands"></a>Commandes cloud-à-appareil

catégorie de commandes de cloud-à-appareil Hello effectue le suivi des erreurs qui se produisent au hub IoT de hello et sont le pipeline de message du cloud-à-appareil toohello connexes. Cette catégorie inclut notamment les erreurs concernant l’envoi de messages cloud-à-appareil (telles qu’un expéditeur non autorisé), la réception des messages cloud-à-appareil (telles que le dépassement du nombre de remises) et la réception des commentaires de message cloud-à-appareil (telles que des commentaires arrivés à expiration). Cette catégorie n’intercepte pas d’erreurs à partir d’un périphérique qui gère correctement un message cloud-à-appareil si le message de salutation cloud sur l’appareil a été remis avec succès.

```json
{
    "messageSizeInBytes": 1234,
    "authType": "{\"scope\":\"hub\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
    "deliveryAcknowledgement": 0,
    "protocol": "Amqp",
    "time": " UTC timestamp",
    "operationName": "ingress",
    "category": "C2DCommands",
    "level": "Error",
    "statusCode": 4XX,
    "statusType": 4XX001,
    "statusDescription": "MessageDescription",
    "deviceId": "device-ID",
    "EventProcessedUtcTime": "UTC timestamp",
    "PartitionId": 1,
    "EventEnqueuedUtcTime": “UTC timestamp"
}
```

### <a name="connections"></a>Connexions

catégorie de connexions Hello effectue le suivi des erreurs qui se produisent lorsque les appareils se connecteront ou se déconnecter d’un hub IoT. Le suivi de cette catégorie est utile pour identifier les tentatives de connexion non autorisées et pour repérer les moments auxquels une connexion est perdue pour les appareils qui se trouvent dans des zones bénéficiant d’une connectivité médiocre.

```json
{
    "durationMs": 1234,
    "authType": "{\"scope\":\"hub\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
    "protocol": "Amqp",
    "time": " UTC timestamp",
    "operationName": "deviceConnect",
    "category": "Connections",
    "level": "Error",
    "statusCode": 4XX,
    "statusType": 4XX001,
    "statusDescription": "MessageDescription",
    "deviceId": "device-ID"
}
```

### <a name="file-uploads"></a>Chargements de fichiers

catégorie de téléchargement de fichier Hello effectue le suivi des erreurs qui se produisent au hub IoT de hello et sont une fonctionnalité de téléchargement toofile connexes. Cette catégorie inclut :

* Erreurs qui se produisent avec hello SAS URI, par exemple lorsqu’il expire avant un périphérique notifie hub hello d’un téléchargement terminé.
* Échec de téléchargements signalées par le périphérique de hello.
* Erreurs qui se produisent lorsqu’un fichier est introuvable dans le stockage lors de la création du message de notification IoT Hub.

Cette catégorie ne peut pas intercepter les erreurs qui directement se produisent lors de l’appareil de hello transfère un toostorage de fichier.

```json
{
    "authType": "{\"scope\":\"hub\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
    "protocol": "HTTP",
    "time": " UTC timestamp",
    "operationName": "ingress",
    "category": "fileUpload",
    "level": "Error",
    "statusCode": 4XX,
    "statusType": 4XX001,
    "statusDescription": "MessageDescription",
    "deviceId": "device-ID",
    "blobUri": "http//bloburi.com",
    "durationMs": 1234
}
```

### <a name="message-routing"></a>Routage de messages

catégorie du routage des messages Hello effectue le suivi des erreurs qui se produisent pendant l’évaluation de routage de message et de contrôle d’intégrité du point de terminaison perçue par IoT Hub. Cette catégorie inclut des événements tels que lorsqu’une règle prend trop « indéfini », lorsque IoT Hub la marque un point de terminaison en tant que de lettres mortes et les autres erreurs reçues à partir d’un point de terminaison. Cette catégorie n’inclut pas les erreurs spécifiques sur les messages hello eux-mêmes (par exemple, le périphérique erreurs de limitation), qui sont signalées sous la catégorie de « télémétrie de l’appareil » hello.

```json
{
    "messageSizeInBytes": 1234,
    "time": "UTC timestamp",
    "operationName": "ingress",
    "category": "routes",
    "level": "Error",
    "deviceId": "device-ID",
    "messageId": "ID of message",
    "routeName": "myroute",
    "endpointName": "myendpoint",
    "details": "ExternalEndpointDisabled"
}
```

## <a name="view-events"></a>Visualiser les événements

Vous pouvez utiliser hello *iothub-explorer* tooquickly de l’outil de test que votre hub IoT génère des événements de contrôle. tooinstall hello outil, consultez les instructions hello Bonjour [iothub-explorer] [ lnk-iothub-explorer] référentiel GitHub.

1. Vérifiez que hello **connexions** analyse catégorie est défini trop**Verbose** dans le portail de hello.

1. À une invite de commandes, exécutez hello suivant commande tooread hello surveillance de point de terminaison :

    ```
    iothub-explorer monitor-ops --login {your iothubowner connection string}
    ```

1. Dans l’invite de commandes une autre, exécutez hello suivant commande toosimulate un périphérique d’envoi de messages de l’appareil-à-cloud :

    ```
    iothub-explorer simulate-device {your device name} --send "My test message" --login {your iothubowner connection string}
    ```

1. Hello première ligne de commande affiche les événements de surveillance de hello comme tooyour IoT hub connecte l’appareil simulé de hello.

## <a name="connect-toohello-monitoring-endpoint"></a>Se connecter toohello surveillance de point de terminaison

Hello surveillance de point de terminaison sur votre hub IoT est un point de terminaison de Hub d’événements compatibles. Vous pouvez utiliser n’importe quel mécanisme qui fonctionne avec les concentrateurs d’événements tooread analyse les messages à partir de ce point de terminaison. Hello exemple suivant crée un lecteur de base qui n’est pas approprié pour un déploiement d’un débit élevé. Pour plus d’informations sur la tooprocess des messages à partir de concentrateurs d’événements, consultez hello [prise en main les concentrateurs d’événements] [ lnk-eventhubs-tutorial] didacticiel.

point de terminaison analyse tooconnect toohello, vous devez un nom de point de terminaison hello et de chaîne de connexion. Hello suit vous montrent comment toofind hello les valeurs nécessaires dans le portail de hello :

1. Dans le portail de hello, accédez tooyour panneau des ressources IoT Hub.

1. Choisissez **surveillance des opérations**et prenez note de hello **nom du concentrateur d’événements compatibles** et **point de terminaison de Hub d’événements compatibles** valeurs :

    ![Valeurs du point de terminaison compatible Event Hub][img-endpoints]

1. Sélectionnez **Stratégies d’accès partagé**, puis **service**. Prenez note de hello **clé primaire** valeur :

    ![Clé primaire de la stratégie d’accès partagé du service][img-service-key]

exemple de code c# suivant Hello est effectuée à partir de Visual Studio **de bureau Windows classique** application de console c#. projet de Hello a hello **WindowsAzure.ServiceBus** package NuGet installé.

* Remplacez l’espace réservé chaîne de connexion hello avec une chaîne de connexion qui utilise hello **point de terminaison de Hub d’événements compatibles** et le service **clé primaire** valeurs notées précédemment, comme indiqué dans les éléments suivants de hello exemple :

    ```cs
    "Endpoint={your Event Hub-compatible endpoint};SharedAccessKeyName=service;SharedAccessKey={your service primary key value}"
    ```

* Remplacez hello analyse l’espace réservé de nom de point de terminaison avec hello **nom du concentrateur d’événements compatibles** valeur que vous avez notée précédemment.

```cs
class Program
{
    static string connectionString = "{your monitoring endpoint connection string}";
    static string monitoringEndpointName = "{your monitoring endpoint name}";
    static EventHubClient eventHubClient;

    static void Main(string[] args)
    {
        Console.WriteLine("Monitoring. Press Enter key tooexit.\n");

        eventHubClient = EventHubClient.CreateFromConnectionString(connectionString, monitoringEndpointName);
        var d2cPartitions = eventHubClient.GetRuntimeInformation().PartitionIds;
        CancellationTokenSource cts = new CancellationTokenSource();
        var tasks = new List<Task>();

        foreach (string partition in d2cPartitions)
        {
            tasks.Add(ReceiveMessagesFromDeviceAsync(partition, cts.Token));
        }

        Console.ReadLine();
        Console.WriteLine("Exiting...");
        cts.Cancel();
        Task.WaitAll(tasks.ToArray());
    }

    private static async Task ReceiveMessagesFromDeviceAsync(string partition, CancellationToken ct)
    {
        var eventHubReceiver = eventHubClient.GetDefaultConsumerGroup().CreateReceiver(partition, DateTime.UtcNow);
        while (true)
        {
            if (ct.IsCancellationRequested)
            {
                await eventHubReceiver.CloseAsync();
                break;
            }

            EventData eventData = await eventHubReceiver.ReceiveAsync(new TimeSpan(0,0,10));

            if (eventData != null)
            {
                string data = Encoding.UTF8.GetString(eventData.GetBytes());
                Console.WriteLine("Message received. Partition: {0} Data: '{1}'", partition, data);
            }
        }
    }
}
```

## <a name="next-steps"></a>Étapes suivantes
toofurther Explorez les fonctionnalités de hello d’IoT Hub, consultez :

* [Guide du développeur IoT Hub][lnk-devguide]
* [Simulation d’un appareil avec Azure IoT Edge][lnk-iotedge]

<!-- Links and images -->
[1]: media/iot-hub-operations-monitoring/enable-OM-1.png
[2]: media/iot-hub-operations-monitoring/enable-OM-2.png
[img-endpoints]: media/iot-hub-operations-monitoring/monitoring-endpoint.png
[img-service-key]: media/iot-hub-operations-monitoring/service-key.png

[lnk-get-started]: iot-hub-csharp-csharp-getstarted.md
[lnk-diagnostic-metrics]: iot-hub-metrics.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-dr]: iot-hub-ha-dr.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-iothub-explorer]: https://github.com/azure/iothub-explorer
[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md