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
# <a name="connect-your-device-tooyour-iot-hub-using-net"></a><span data-ttu-id="ff71b-104">Connectez votre concentrateur de IoT tooyour périphérique à l’aide de .NET</span><span class="sxs-lookup"><span data-stu-id="ff71b-104">Connect your device tooyour IoT hub using .NET</span></span>

[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="ff71b-105">À la fin de hello de ce didacticiel, vous avez trois applications de console .NET :</span><span class="sxs-lookup"><span data-stu-id="ff71b-105">At hello end of this tutorial, you have three .NET console apps:</span></span>

* <span data-ttu-id="ff71b-106">**CreateDeviceIdentity**, ce qui crée une identité d’appareil et clé de sécurité associés tooconnect votre application.</span><span class="sxs-lookup"><span data-stu-id="ff71b-106">**CreateDeviceIdentity**, which creates a device identity and associated security key tooconnect your device app.</span></span>
* <span data-ttu-id="ff71b-107">**ReadDeviceToCloudMessages**, qui affiche la télémétrie hello envoyée par votre application.</span><span class="sxs-lookup"><span data-stu-id="ff71b-107">**ReadDeviceToCloudMessages**, which displays hello telemetry sent by your device app.</span></span>
* <span data-ttu-id="ff71b-108">**SimulatedDevice**, qui se connecte tooyour IoT hub avec l’identité de l’appareil hello créée précédemment et envoie un message de télémétrie à chaque seconde à l’aide du protocole MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="ff71b-108">**SimulatedDevice**, which connects tooyour IoT hub with hello device identity created earlier, and sends a telemetry message every second by using hello MQTT protocol.</span></span>

<span data-ttu-id="ff71b-109">Vous pouvez télécharger ou cloner la solution Visual Studio hello, qui contient les trois applications de hello à partir de Github.</span><span class="sxs-lookup"><span data-stu-id="ff71b-109">You can download or clone hello Visual Studio solution, which contains hello three apps from Github.</span></span>

```bash
git clone https://github.com/Azure-Samples/iot-hub-dotnet-simulated-device-client-app.git
```

> [!NOTE]
> <span data-ttu-id="ff71b-110">Pour plus d’informations sur hello kits de développement logiciel Azure IoT que vous pouvez utiliser toobuild toorun d’applications sur les appareils et à votre solution back-end, consultez [kits de développement logiciel Azure IoT][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="ff71b-110">For information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices, and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="ff71b-111">toocomplete ce didacticiel, vous devez hello suivant :</span><span class="sxs-lookup"><span data-stu-id="ff71b-111">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="ff71b-112">Visual Studio 2015 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="ff71b-112">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="ff71b-113">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="ff71b-113">An active Azure account.</span></span> <span data-ttu-id="ff71b-114">(Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)</span><span class="sxs-lookup"><span data-stu-id="ff71b-114">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="ff71b-115">Vous avez créé votre hub IoT, et vous avez le nom d’hôte hello et chaîne de connexion de IoT Hub que vous devez le reste de hello toocomplete de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="ff71b-115">You have now created your IoT hub, and you have hello host name and IoT Hub connection string that you need toocomplete hello rest of this tutorial.</span></span>

<a id="DeviceIdentity_csharp"></a>
[!INCLUDE [iot-hub-get-started-create-device-identity-csharp](../../includes/iot-hub-get-started-create-device-identity-csharp.md)]

<a id="D2C_csharp"></a>
## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="ff71b-116">Recevoir des messages appareil-à-cloud</span><span class="sxs-lookup"><span data-stu-id="ff71b-116">Receive device-to-cloud messages</span></span>
<span data-ttu-id="ff71b-117">Dans cette section, vous allez créer une application console .NET qui lit les messages des appareils vers le cloud dans l’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ff71b-117">In this section, you create a .NET console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="ff71b-118">Un hub IoT expose un [Azure Event Hubs][lnk-event-hubs-overview]-point de terminaison compatible tooenable vous tooread les messages appareil-à-cloud.</span><span class="sxs-lookup"><span data-stu-id="ff71b-118">An IoT hub exposes an [Azure Event Hubs][lnk-event-hubs-overview]-compatible endpoint tooenable you tooread device-to-cloud messages.</span></span> <span data-ttu-id="ff71b-119">tookeep les choses simples, ce didacticiel crée un lecteur de base qui n’est pas approprié pour un déploiement d’un débit élevé.</span><span class="sxs-lookup"><span data-stu-id="ff71b-119">tookeep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="ff71b-120">toolearn comment les messages tooprocess appareil-à-cloud à grande échelle, consultez hello [traiter les messages appareil-à-cloud] [ lnk-process-d2c-tutorial] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="ff71b-120">toolearn how tooprocess device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span> <span data-ttu-id="ff71b-121">Pour plus d’informations sur la tooprocess des messages à partir de concentrateurs d’événements, consultez hello [prise en main les concentrateurs d’événements] [ lnk-eventhubs-tutorial] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="ff71b-121">For more information about how tooprocess messages from Event Hubs, see hello [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial.</span></span> <span data-ttu-id="ff71b-122">(Ce didacticiel est applicable toohello Hub IoT Hub événement compatible avec points de terminaison).</span><span class="sxs-lookup"><span data-stu-id="ff71b-122">(This tutorial is applicable toohello IoT Hub Event Hub-compatible endpoints.)</span></span>

> [!NOTE]
> <span data-ttu-id="ff71b-123">Hello point de terminaison de Hub d’événements compatibles pour la lecture des messages appareil-à-cloud toujours utilise le protocole AMQP hello.</span><span class="sxs-lookup"><span data-stu-id="ff71b-123">hello Event Hub-compatible endpoint for reading device-to-cloud messages always uses hello AMQP protocol.</span></span>

1. <span data-ttu-id="ff71b-124">Dans Visual Studio, ajouter une solution d’actuel toohello de projet Visual c# bureau classique de Windows, à l’aide de hello **l’application Console (.NET Framework)** modèle de projet.</span><span class="sxs-lookup"><span data-stu-id="ff71b-124">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution, by using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="ff71b-125">Assurez-vous que la version du .NET Framework hello est 4.5.1 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="ff71b-125">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="ff71b-126">Projet de hello nom **ReadDeviceToCloudMessages**.</span><span class="sxs-lookup"><span data-stu-id="ff71b-126">Name hello project **ReadDeviceToCloudMessages**.</span></span>

    ![Nouveau projet Visual C# Bureau classique Windows][10a]

2. <span data-ttu-id="ff71b-128">Dans l’Explorateur de solutions, cliquez sur hello **ReadDeviceToCloudMessages** de projet, puis cliquez sur **gérer les Packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="ff71b-128">In Solution Explorer, right-click hello **ReadDeviceToCloudMessages** project, and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="ff71b-129">Bonjour **Gestionnaire de Package NuGet** fenêtre, recherchez **WindowsAzure.ServiceBus**, sélectionnez **installer**et acceptez les conditions d’utilisation de hello.</span><span class="sxs-lookup"><span data-stu-id="ff71b-129">In hello **NuGet Package Manager** window, search for **WindowsAzure.ServiceBus**, select **Install**, and accept hello terms of use.</span></span> <span data-ttu-id="ff71b-130">Cette procédure télécharge, installe et ajoute une référence trop[Azure Service Bus][lnk-servicebus-nuget], avec toutes ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="ff71b-130">This procedure downloads, installs, and adds a reference too[Azure Service Bus][lnk-servicebus-nuget], with all its dependencies.</span></span> <span data-ttu-id="ff71b-131">Ce package permet hello application tooconnect toohello concentrateur d’événements compatibles point de terminaison sur votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="ff71b-131">This package enables hello application tooconnect toohello Event Hub-compatible endpoint on your IoT hub.</span></span>

4. <span data-ttu-id="ff71b-132">Ajoutez hello suivant `using` instructions haut hello hello **Program.cs** fichier :</span><span class="sxs-lookup"><span data-stu-id="ff71b-132">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>

    ```csharp
    using Microsoft.ServiceBus.Messaging;
    using System.Threading;
    ```

5. <span data-ttu-id="ff71b-133">Ajouter hello suivant champs toohello **programme** classe.</span><span class="sxs-lookup"><span data-stu-id="ff71b-133">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="ff71b-134">Remplacer la valeur d’espace réservé hello avec hello chaîne de connexion de IoT Hub hub hello que vous avez créé dans hello section « Créer un hub IoT » de.</span><span class="sxs-lookup"><span data-stu-id="ff71b-134">Replace hello placeholder value with hello IoT Hub connection string for hello hub you created in hello "Create an IoT hub" section.</span></span>

    ```csharp
    static string connectionString = "{iothub connection string}";
    static string iotHubD2cEndpoint = "messages/events";
    static EventHubClient eventHubClient;
    ```

6. <span data-ttu-id="ff71b-135">Ajouter hello suivant de méthode toohello **programme** classe :</span><span class="sxs-lookup"><span data-stu-id="ff71b-135">Add hello following method toohello **Program** class:</span></span>

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

    <span data-ttu-id="ff71b-136">Cette méthode utilise un **EventHubReceiver** tooreceive les messages d’instance à partir de tous les hello IoT hub appareil-à-cloud reçoivent des partitions.</span><span class="sxs-lookup"><span data-stu-id="ff71b-136">This method uses an **EventHubReceiver** instance tooreceive messages from all hello IoT hub device-to-cloud receive partitions.</span></span> <span data-ttu-id="ff71b-137">Notez la façon dont vous passez un `DateTime.Now` paramètre lorsque vous créez hello **EventHubReceiver** de l’objet, afin qu’elle reçoive uniquement les messages envoyés après son démarrage.</span><span class="sxs-lookup"><span data-stu-id="ff71b-137">Notice how you pass a `DateTime.Now` parameter when you create hello **EventHubReceiver** object, so that it only receives messages sent after it starts.</span></span> <span data-ttu-id="ff71b-138">Ce filtre est utile dans un environnement de test afin de voir l’ensemble actuel de hello de messages.</span><span class="sxs-lookup"><span data-stu-id="ff71b-138">This filter is useful in a test environment so you can see hello current set of messages.</span></span> <span data-ttu-id="ff71b-139">Dans un environnement de production, votre code doit Assurez-vous qu’elle traite tous les messages de type hello.</span><span class="sxs-lookup"><span data-stu-id="ff71b-139">In a production environment, your code should make sure that it processes all hello messages.</span></span> <span data-ttu-id="ff71b-140">Pour plus d’informations, consultez le didacticiel de hello [comment tooprocess les messages appareil-à-cloud IoT Hub][lnk-process-d2c-tutorial].</span><span class="sxs-lookup"><span data-stu-id="ff71b-140">For more information, see hello tutorial [How tooprocess IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial].</span></span>

7. <span data-ttu-id="ff71b-141">Enfin, ajoutez hello suivant lignes toohello **Main** méthode :</span><span class="sxs-lookup"><span data-stu-id="ff71b-141">Finally, add hello following lines toohello **Main** method:</span></span>

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

## <a name="create-a-device-app"></a><span data-ttu-id="ff71b-142">Créer une application d’appareil</span><span class="sxs-lookup"><span data-stu-id="ff71b-142">Create a device app</span></span>

<span data-ttu-id="ff71b-143">Dans cette section, vous créez une application console .NET qui simule un appareil qui envoie l’IoT hub tooan de messages appareil-à-cloud.</span><span class="sxs-lookup"><span data-stu-id="ff71b-143">In this section, you create a .NET console app that simulates a device that sends device-to-cloud messages tooan IoT hub.</span></span>

1. <span data-ttu-id="ff71b-144">Dans Visual Studio, ajouter une solution d’actuel toohello de projet Visual c# bureau classique de Windows, à l’aide de hello **l’application Console (.NET Framework)** modèle de projet.</span><span class="sxs-lookup"><span data-stu-id="ff71b-144">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution, by using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="ff71b-145">Assurez-vous que la version du .NET Framework hello est 4.5.1 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="ff71b-145">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="ff71b-146">Projet de hello nom **SimulatedDevice**.</span><span class="sxs-lookup"><span data-stu-id="ff71b-146">Name hello project **SimulatedDevice**.</span></span>

    ![Nouveau projet Visual C# Bureau classique Windows][10b]

2. <span data-ttu-id="ff71b-148">Dans l’Explorateur de solutions, cliquez sur hello **SimulatedDevice** de projet, puis cliquez sur **gérer les Packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="ff71b-148">In Solution Explorer, right-click hello **SimulatedDevice** project, and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="ff71b-149">Bonjour **Gestionnaire de Package NuGet** fenêtre, sélectionnez **Parcourir**, recherchez **Microsoft.Azure.Devices.Client**, sélectionnez **installer** tooinstall hello **Microsoft.Azure.Devices.Client** empaqueter et accepter les conditions d’utilisation de hello.</span><span class="sxs-lookup"><span data-stu-id="ff71b-149">In hello **NuGet Package Manager** window, select **Browse**, search for **Microsoft.Azure.Devices.Client**, select **Install** tooinstall hello **Microsoft.Azure.Devices.Client** package, and accept hello terms of use.</span></span> <span data-ttu-id="ff71b-150">Cette procédure télécharge, installe et ajoute une référence toohello [package NuGet du Kit de développement logiciel de périphérique Azure IoT] [ lnk-device-nuget] et ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="ff71b-150">This procedure downloads, installs, and adds a reference toohello [Azure IoT device SDK NuGet package][lnk-device-nuget] and its dependencies.</span></span>

4. <span data-ttu-id="ff71b-151">Ajoutez hello suivant `using` instruction début hello Hello **Program.cs** fichier :</span><span class="sxs-lookup"><span data-stu-id="ff71b-151">Add hello following `using` statement at hello top of hello **Program.cs** file:</span></span>

    ```csharp
    using Microsoft.Azure.Devices.Client;
    using Newtonsoft.Json;
    ```

5. <span data-ttu-id="ff71b-152">Ajouter hello suivant champs toohello **programme** classe.</span><span class="sxs-lookup"><span data-stu-id="ff71b-152">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="ff71b-153">Substitution `{iot hub hostname}` avec le nom d’hôte hello IoT hub récupéré à la section « Créer un hub IoT » de hello.</span><span class="sxs-lookup"><span data-stu-id="ff71b-153">Substitute `{iot hub hostname}` with hello IoT hub host name you retrieved in hello "Create an IoT hub" section.</span></span> <span data-ttu-id="ff71b-154">Substitution `{device key}` par clé hello d’appareil que vous avez récupéré dans la section « Créer une identité d’appareil » de hello.</span><span class="sxs-lookup"><span data-stu-id="ff71b-154">Substitute `{device key}` with hello device key you retrieved in hello "Create a device identity" section.</span></span>

    ```csharp
    static DeviceClient deviceClient;
    static string iotHubUri = "{iot hub hostname}";
    static string deviceKey = "{device key}";
    ```

6. <span data-ttu-id="ff71b-155">Ajouter hello suivant de méthode toohello **programme** classe :</span><span class="sxs-lookup"><span data-stu-id="ff71b-155">Add hello following method toohello **Program** class:</span></span>

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

    <span data-ttu-id="ff71b-156">Cette méthode envoie un nouveau message Appareil vers cloud toutes les secondes.</span><span class="sxs-lookup"><span data-stu-id="ff71b-156">This method sends a new device-to-cloud message every second.</span></span> <span data-ttu-id="ff71b-157">message de salutation contient un objet sérialisé en JSON, avec l’ID de périphérique hello et généré de façon aléatoire les numéros toosimulate un capteur de température et un capteur humidité.</span><span class="sxs-lookup"><span data-stu-id="ff71b-157">hello message contains a JSON-serialized object, with hello device ID and randomly generated numbers toosimulate a temperature sensor, and a humidity sensor.</span></span>

7. <span data-ttu-id="ff71b-158">Enfin, ajoutez hello suivant lignes toohello **Main** méthode :</span><span class="sxs-lookup"><span data-stu-id="ff71b-158">Finally, add hello following lines toohello **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Simulated device\n");
    deviceClient = DeviceClient.Create(iotHubUri, new DeviceAuthenticationWithRegistrySymmetricKey ("myFirstDevice", deviceKey), TransportType.Mqtt);

    SendDeviceToCloudMessagesAsync();
    Console.ReadLine();
    ```

    <span data-ttu-id="ff71b-159">Par défaut, hello **créer** méthode dans une application .NET Framework crée un **DeviceClient** instance qui utilise toocommunicate de protocole AMQP hello avec IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ff71b-159">By default, hello **Create** method in a .NET Framework app creates a **DeviceClient** instance that uses hello AMQP protocol toocommunicate with IoT Hub.</span></span> <span data-ttu-id="ff71b-160">toouse hello protocole MQTT ou HTTP, utilisez le remplacement hello Hello **créer** méthode qui vous permet de protocole de hello toospecify.</span><span class="sxs-lookup"><span data-stu-id="ff71b-160">toouse hello MQTT or HTTP protocol, use hello override of hello **Create** method that enables you toospecify hello protocol.</span></span> <span data-ttu-id="ff71b-161">Par défaut, les clients UWP et PCL utilisent le protocole HTTP hello.</span><span class="sxs-lookup"><span data-stu-id="ff71b-161">UWP and PCL clients use hello HTTP protocol by default.</span></span> <span data-ttu-id="ff71b-162">Si vous utilisez le protocole de hello HTTP, vous devez également ajouter hello **Microsoft.AspNet.WebApi.Client** hello de NuGet package tooyour projet tooinclude **System.Net.Http.Formatting** espace de noms.</span><span class="sxs-lookup"><span data-stu-id="ff71b-162">If you use hello HTTP protocol, you should also add hello **Microsoft.AspNet.WebApi.Client** NuGet package tooyour project tooinclude hello **System.Net.Http.Formatting** namespace.</span></span>

<span data-ttu-id="ff71b-163">Ce didacticiel vous guide de hello étapes toocreate un IoT Hub application d’appareil.</span><span class="sxs-lookup"><span data-stu-id="ff71b-163">This tutorial takes you through hello steps toocreate an IoT Hub device app.</span></span> <span data-ttu-id="ff71b-164">Vous pouvez également utiliser hello [Service connecté pour Azure IoT Hub] [ lnk-connected-service] Visual Studio extension tooadd hello code nécessaire tooyour application.</span><span class="sxs-lookup"><span data-stu-id="ff71b-164">You can also use hello [Connected Service for Azure IoT Hub][lnk-connected-service] Visual Studio extension tooadd hello necessary code tooyour device app.</span></span>

> [!NOTE]
> <span data-ttu-id="ff71b-165">tookeep les choses simples, ce didacticiel n’implémente pas de toute stratégie de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="ff71b-165">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="ff71b-166">Dans le code de production, vous devez implémenter des stratégies de nouvelle tentative (par exemple, une interruption exponentielle), comme indiqué dans l’article hello [gestion des pannes temporaires][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="ff71b-166">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="run-hello-apps"></a><span data-ttu-id="ff71b-167">Exécuter des applications de hello</span><span class="sxs-lookup"><span data-stu-id="ff71b-167">Run hello apps</span></span>

<span data-ttu-id="ff71b-168">Vous êtes maintenant prêt toorun hello applications.</span><span class="sxs-lookup"><span data-stu-id="ff71b-168">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="ff71b-169">Dans Visual Studio, dans l’explorateur de solutions, cliquez avec le bouton droit sur votre solution, puis sur **Définir les projets de démarrage**.</span><span class="sxs-lookup"><span data-stu-id="ff71b-169">In Visual Studio, in Solution Explorer, right-click your solution, and then click **Set StartUp projects**.</span></span> <span data-ttu-id="ff71b-170">Sélectionnez **plusieurs projets de démarrage**, puis sélectionnez **Démarrer** en tant qu’action hello pour les deux hello **ReadDeviceToCloudMessages** et **SimulatedDevice** projets.</span><span class="sxs-lookup"><span data-stu-id="ff71b-170">Select **Multiple startup projects**, and then select **Start** as hello action for both hello **ReadDeviceToCloudMessages** and **SimulatedDevice** projects.</span></span>

    ![Propriétés de démarrage de projet][41]

2. <span data-ttu-id="ff71b-172">Appuyez sur **F5** toostart les deux applications en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="ff71b-172">Press **F5** toostart both apps running.</span></span> <span data-ttu-id="ff71b-173">Hello de sortie de la console à partir de hello **SimulatedDevice** application d’afficher les messages hello votre application envoie tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="ff71b-173">hello console output from hello **SimulatedDevice** app shows hello messages your device app sends tooyour IoT hub.</span></span> <span data-ttu-id="ff71b-174">Hello de sortie de la console à partir de hello **ReadDeviceToCloudMessages** application affiche des messages hello qui reçoit de votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="ff71b-174">hello console output from hello **ReadDeviceToCloudMessages** app shows hello messages that your IoT hub receives.</span></span>

    ![Sortie de console à partir d’applications][42]

3. <span data-ttu-id="ff71b-176">Hello **utilisation** vignette Bonjour [portail Azure] [ lnk-portal] affiche hello le nombre de messages envoyés toohello IoT hub :</span><span class="sxs-lookup"><span data-stu-id="ff71b-176">hello **Usage** tile in hello [Azure portal][lnk-portal] shows hello number of messages sent toohello IoT hub:</span></span>

    ![Vignette Utilisation du portail Azure][43]

## <a name="next-steps"></a><span data-ttu-id="ff71b-178">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ff71b-178">Next steps</span></span>

<span data-ttu-id="ff71b-179">Dans ce didacticiel, vous configuré un hub IoT Bonjour portail Azure et ensuite créé une identité d’appareil dans le Registre des identités de hello IoT hub.</span><span class="sxs-lookup"><span data-stu-id="ff71b-179">In this tutorial, you configured an IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="ff71b-180">Vous avez utilisé ce périphérique identité tooenable hello appareil application toosend messages appareil-à-cloud toohello hub IoT.</span><span class="sxs-lookup"><span data-stu-id="ff71b-180">You used this device identity tooenable hello device app toosend device-to-cloud messages toohello IoT hub.</span></span> <span data-ttu-id="ff71b-181">Vous avez créé également une application qui affiche les messages hello reçus par IoT hub de hello.</span><span class="sxs-lookup"><span data-stu-id="ff71b-181">You also created an app that displays hello messages received by hello IoT hub.</span></span>

<span data-ttu-id="ff71b-182">toocontinue mise en route avec IoT Hub et tooexplore autres scénarios IoT, consultez :</span><span class="sxs-lookup"><span data-stu-id="ff71b-182">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="ff71b-183">[Connexion de votre appareil][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="ff71b-183">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="ff71b-184">[Prise en main de la gestion d’appareils][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="ff71b-184">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="ff71b-185">[Bien démarrer avec IoT Edge][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="ff71b-185">[Getting started with IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="ff71b-186">toolearn tooextend vos messages IoT solution et des processus de périphérique dans le cloud à grande échelle, voir hello [traiter les messages appareil-à-cloud] [ lnk-process-d2c-tutorial] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="ff71b-186">toolearn how tooextend your IoT solution and process device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>

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
