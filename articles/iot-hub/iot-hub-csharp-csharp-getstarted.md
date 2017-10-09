---
title: "aaaGet démarré avec Azure IoT Hub (.NET) | Documents Microsoft"
description: "Découvrez comment toosend appareil-à-cloud messages tooAzure IoT Hub à l’aide de kits de développement logiciel IoT pour .NET. Créer appareil simulé et tooregister des applications de service de votre appareil, envoyer des messages et lire les messages de hub IoT."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: f40604ff-8fd6-4969-9e99-8574fbcf036c
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 56cf14687411898ea0fa4ebb1782e18b3930809c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-tooyour-iot-hub-using-net"></a>Connectez votre concentrateur de IoT tooyour périphérique à l’aide de .NET

[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

À la fin de hello de ce didacticiel, vous avez trois applications de console .NET :

* **CreateDeviceIdentity**, ce qui crée une identité d’appareil et clé de sécurité associés tooconnect votre application.
* **ReadDeviceToCloudMessages**, qui affiche la télémétrie hello envoyée par votre application.
* **SimulatedDevice**, qui se connecte tooyour IoT hub avec l’identité de l’appareil hello créée précédemment et envoie un message de télémétrie à chaque seconde à l’aide du protocole MQTT hello.

Vous pouvez télécharger ou cloner la solution Visual Studio hello, qui contient les trois applications de hello à partir de Github.

```bash
git clone https://github.com/Azure-Samples/iot-hub-dotnet-simulated-device-client-app.git
```

> [!NOTE]
> Pour plus d’informations sur hello kits de développement logiciel Azure IoT que vous pouvez utiliser toobuild toorun d’applications sur les appareils et à votre solution back-end, consultez [kits de développement logiciel Azure IoT][lnk-hub-sdks].

toocomplete ce didacticiel, vous devez hello suivant :

* Visual Studio 2015 ou Visual Studio 2017.
* Un compte Azure actif. (Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

Vous avez créé votre hub IoT, et vous avez le nom d’hôte hello et chaîne de connexion de IoT Hub que vous devez le reste de hello toocomplete de ce didacticiel.

<a id="DeviceIdentity_csharp"></a>
[!INCLUDE [iot-hub-get-started-create-device-identity-csharp](../../includes/iot-hub-get-started-create-device-identity-csharp.md)]

<a id="D2C_csharp"></a>
## <a name="receive-device-to-cloud-messages"></a>Recevoir des messages appareil-à-cloud
Dans cette section, vous allez créer une application console .NET qui lit les messages des appareils vers le cloud dans l’IoT Hub. Un hub IoT expose un [Azure Event Hubs][lnk-event-hubs-overview]-point de terminaison compatible tooenable vous tooread les messages appareil-à-cloud. tookeep les choses simples, ce didacticiel crée un lecteur de base qui n’est pas approprié pour un déploiement d’un débit élevé. toolearn comment les messages tooprocess appareil-à-cloud à grande échelle, consultez hello [traiter les messages appareil-à-cloud] [ lnk-process-d2c-tutorial] didacticiel. Pour plus d’informations sur la tooprocess des messages à partir de concentrateurs d’événements, consultez hello [prise en main les concentrateurs d’événements] [ lnk-eventhubs-tutorial] didacticiel. (Ce didacticiel est applicable toohello Hub IoT Hub événement compatible avec points de terminaison).

> [!NOTE]
> Hello point de terminaison de Hub d’événements compatibles pour la lecture des messages appareil-à-cloud toujours utilise le protocole AMQP hello.

1. Dans Visual Studio, ajouter une solution d’actuel toohello de projet Visual c# bureau classique de Windows, à l’aide de hello **l’application Console (.NET Framework)** modèle de projet. Assurez-vous que la version du .NET Framework hello est 4.5.1 ou version ultérieure. Projet de hello nom **ReadDeviceToCloudMessages**.

    ![Nouveau projet Visual C# Bureau classique Windows][10a]

2. Dans l’Explorateur de solutions, cliquez sur hello **ReadDeviceToCloudMessages** de projet, puis cliquez sur **gérer les Packages NuGet**.

3. Bonjour **Gestionnaire de Package NuGet** fenêtre, recherchez **WindowsAzure.ServiceBus**, sélectionnez **installer**et acceptez les conditions d’utilisation de hello. Cette procédure télécharge, installe et ajoute une référence trop[Azure Service Bus][lnk-servicebus-nuget], avec toutes ses dépendances. Ce package permet hello application tooconnect toohello concentrateur d’événements compatibles point de terminaison sur votre hub IoT.

4. Ajoutez hello suivant `using` instructions haut hello hello **Program.cs** fichier :

    ```csharp
    using Microsoft.ServiceBus.Messaging;
    using System.Threading;
    ```

5. Ajouter hello suivant champs toohello **programme** classe. Remplacer la valeur d’espace réservé hello avec hello chaîne de connexion de IoT Hub hub hello que vous avez créé dans hello section « Créer un hub IoT » de.

    ```csharp
    static string connectionString = "{iothub connection string}";
    static string iotHubD2cEndpoint = "messages/events";
    static EventHubClient eventHubClient;
    ```

6. Ajouter hello suivant de méthode toohello **programme** classe :

    ```csharp
    private static async Task ReceiveMessagesFromDeviceAsync(string partition, CancellationToken ct)
    {
        var eventHubReceiver = eventHubClient.GetDefaultConsumerGroup().CreateReceiver(partition, DateTime.UtcNow);
        while (true)
        {
            if (ct.IsCancellationRequested) break;
            EventData eventData = await eventHubReceiver.ReceiveAsync();
            if (eventData == null) continue;

            string data = Encoding.UTF8.GetString(eventData.GetBytes());
            Console.WriteLine("Message received. Partition: {0} Data: '{1}'", partition, data);
        }
    }
    ```

    Cette méthode utilise un **EventHubReceiver** tooreceive les messages d’instance à partir de tous les hello IoT hub appareil-à-cloud reçoivent des partitions. Notez la façon dont vous passez un `DateTime.Now` paramètre lorsque vous créez hello **EventHubReceiver** de l’objet, afin qu’elle reçoive uniquement les messages envoyés après son démarrage. Ce filtre est utile dans un environnement de test afin de voir l’ensemble actuel de hello de messages. Dans un environnement de production, votre code doit Assurez-vous qu’elle traite tous les messages de type hello. Pour plus d’informations, consultez le didacticiel de hello [comment tooprocess les messages appareil-à-cloud IoT Hub][lnk-process-d2c-tutorial].

7. Enfin, ajoutez hello suivant lignes toohello **Main** méthode :

    ```csharp
    Console.WriteLine("Receive messages. Ctrl-C tooexit.\n");
    eventHubClient = EventHubClient.CreateFromConnectionString(connectionString, iotHubD2cEndpoint);

    var d2cPartitions = eventHubClient.GetRuntimeInformation().PartitionIds;

    CancellationTokenSource cts = new CancellationTokenSource();

    System.Console.CancelKeyPress += (s, e) =>
    {
        e.Cancel = true;
        cts.Cancel();
        Console.WriteLine("Exiting...");
    };

    var tasks = new List<Task>();
    foreach (string partition in d2cPartitions)
    {
        tasks.Add(ReceiveMessagesFromDeviceAsync(partition, cts.Token));
    }  
    Task.WaitAll(tasks.ToArray());
    ```

## <a name="create-a-device-app"></a>Créer une application d’appareil

Dans cette section, vous créez une application console .NET qui simule un appareil qui envoie l’IoT hub tooan de messages appareil-à-cloud.

1. Dans Visual Studio, ajouter une solution d’actuel toohello de projet Visual c# bureau classique de Windows, à l’aide de hello **l’application Console (.NET Framework)** modèle de projet. Assurez-vous que la version du .NET Framework hello est 4.5.1 ou version ultérieure. Projet de hello nom **SimulatedDevice**.

    ![Nouveau projet Visual C# Bureau classique Windows][10b]

2. Dans l’Explorateur de solutions, cliquez sur hello **SimulatedDevice** de projet, puis cliquez sur **gérer les Packages NuGet**.

3. Bonjour **Gestionnaire de Package NuGet** fenêtre, sélectionnez **Parcourir**, recherchez **Microsoft.Azure.Devices.Client**, sélectionnez **installer** tooinstall hello **Microsoft.Azure.Devices.Client** empaqueter et accepter les conditions d’utilisation de hello. Cette procédure télécharge, installe et ajoute une référence toohello [package NuGet du Kit de développement logiciel de périphérique Azure IoT] [ lnk-device-nuget] et ses dépendances.

4. Ajoutez hello suivant `using` instruction début hello Hello **Program.cs** fichier :

    ```csharp
    using Microsoft.Azure.Devices.Client;
    using Newtonsoft.Json;
    ```

5. Ajouter hello suivant champs toohello **programme** classe. Substitution `{iot hub hostname}` avec le nom d’hôte hello IoT hub récupéré à la section « Créer un hub IoT » de hello. Substitution `{device key}` par clé hello d’appareil que vous avez récupéré dans la section « Créer une identité d’appareil » de hello.

    ```csharp
    static DeviceClient deviceClient;
    static string iotHubUri = "{iot hub hostname}";
    static string deviceKey = "{device key}";
    ```

6. Ajouter hello suivant de méthode toohello **programme** classe :

    ```csharp
    private static async void SendDeviceToCloudMessagesAsync()
    {
        double minTemperature = 20;
        double minHumidity = 60;
        int messageId = 1;
        Random rand = new Random();

        while (true)
        {
            double currentTemperature = minTemperature + rand.NextDouble() * 15;
            double currentHumidity = minHumidity + rand.NextDouble() * 20;

            var telemetryDataPoint = new
            {
                messageId = messageId++,
                deviceId = "myFirstDevice",
                temperature = currentTemperature,
                humidity = currentHumidity
            };
            var messageString = JsonConvert.SerializeObject(telemetryDataPoint);
            var message = new Message(Encoding.ASCII.GetBytes(messageString));
            message.Properties.Add("temperatureAlert", (currentTemperature > 30) ? "true" : "false");

            await deviceClient.SendEventAsync(message);
            Console.WriteLine("{0} > Sending message: {1}", DateTime.Now, messageString);

            await Task.Delay(1000);
        }
    }
    ```

    Cette méthode envoie un nouveau message Appareil vers cloud toutes les secondes. message de salutation contient un objet sérialisé en JSON, avec l’ID de périphérique hello et généré de façon aléatoire les numéros toosimulate un capteur de température et un capteur humidité.

7. Enfin, ajoutez hello suivant lignes toohello **Main** méthode :

    ```csharp
    Console.WriteLine("Simulated device\n");
    deviceClient = DeviceClient.Create(iotHubUri, new DeviceAuthenticationWithRegistrySymmetricKey ("myFirstDevice", deviceKey), TransportType.Mqtt);

    SendDeviceToCloudMessagesAsync();
    Console.ReadLine();
    ```

    Par défaut, hello **créer** méthode dans une application .NET Framework crée un **DeviceClient** instance qui utilise toocommunicate de protocole AMQP hello avec IoT Hub. toouse hello protocole MQTT ou HTTP, utilisez le remplacement hello Hello **créer** méthode qui vous permet de protocole de hello toospecify. Par défaut, les clients UWP et PCL utilisent le protocole HTTP hello. Si vous utilisez le protocole de hello HTTP, vous devez également ajouter hello **Microsoft.AspNet.WebApi.Client** hello de NuGet package tooyour projet tooinclude **System.Net.Http.Formatting** espace de noms.

Ce didacticiel vous guide de hello étapes toocreate un IoT Hub application d’appareil. Vous pouvez également utiliser hello [Service connecté pour Azure IoT Hub] [ lnk-connected-service] Visual Studio extension tooadd hello code nécessaire tooyour application.

> [!NOTE]
> tookeep les choses simples, ce didacticiel n’implémente pas de toute stratégie de nouvelle tentative. Dans le code de production, vous devez implémenter des stratégies de nouvelle tentative (par exemple, une interruption exponentielle), comme indiqué dans l’article hello [gestion des pannes temporaires][lnk-transient-faults].

## <a name="run-hello-apps"></a>Exécuter des applications de hello

Vous êtes maintenant prêt toorun hello applications.

1. Dans Visual Studio, dans l’explorateur de solutions, cliquez avec le bouton droit sur votre solution, puis sur **Définir les projets de démarrage**. Sélectionnez **plusieurs projets de démarrage**, puis sélectionnez **Démarrer** en tant qu’action hello pour les deux hello **ReadDeviceToCloudMessages** et **SimulatedDevice** projets.

    ![Propriétés de démarrage de projet][41]

2. Appuyez sur **F5** toostart les deux applications en cours d’exécution. Hello de sortie de la console à partir de hello **SimulatedDevice** application d’afficher les messages hello votre application envoie tooyour IoT hub. Hello de sortie de la console à partir de hello **ReadDeviceToCloudMessages** application affiche des messages hello qui reçoit de votre hub IoT.

    ![Sortie de console à partir d’applications][42]

3. Hello **utilisation** vignette Bonjour [portail Azure] [ lnk-portal] affiche hello le nombre de messages envoyés toohello IoT hub :

    ![Vignette Utilisation du portail Azure][43]

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous configuré un hub IoT Bonjour portail Azure et ensuite créé une identité d’appareil dans le Registre des identités de hello IoT hub. Vous avez utilisé ce périphérique identité tooenable hello appareil application toosend messages appareil-à-cloud toohello hub IoT. Vous avez créé également une application qui affiche les messages hello reçus par IoT hub de hello.

toocontinue mise en route avec IoT Hub et tooexplore autres scénarios IoT, consultez :

* [Connexion de votre appareil][lnk-connect-device]
* [Prise en main de la gestion d’appareils][lnk-device-management]
* [Bien démarrer avec IoT Edge][lnk-iot-edge]

toolearn tooextend vos messages IoT solution et des processus de périphérique dans le cloud à grande échelle, voir hello [traiter les messages appareil-à-cloud] [ lnk-process-d2c-tutorial] didacticiel.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

<!-- Images. -->
[41]: ./media/iot-hub-csharp-csharp-getstarted/run-apps1.png
[42]: ./media/iot-hub-csharp-csharp-getstarted/run-apps2.png
[43]: ./media/iot-hub-csharp-csharp-getstarted/usage.png
[10a]: ./media/iot-hub-csharp-csharp-getstarted/create-receive-csharp1.png
[10b]: ./media/iot-hub-csharp-csharp-getstarted/create-device-csharp1.png


<!-- Links -->
[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-servicebus-nuget]: https://www.nuget.org/packages/WindowsAzure.ServiceBus
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md

[lnk-device-nuget]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-connected-service]: https://visualstudiogallery.msdn.microsoft.com/e254a3a5-d72e-488e-9bd3-8fee8e0cd1d6
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
