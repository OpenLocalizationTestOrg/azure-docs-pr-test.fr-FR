---
title: "Prise en main d’Azure IoT Hub (.NET) | Microsoft Docs"
description: "Découvrez comment envoyer des messages appareil-vers-cloud à Azure IoT Hub à l’aide des kits SDK Azure IoT pour .NET. Créez un appareil simulé et des applications de service pour inscrire votre appareil, envoyer des messages et lire des messages d’IoT Hub."
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
ms.openlocfilehash: 69296eb9ac2a74a97b632d27733a6a06500b4abd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="connect-your-device-to-your-iot-hub-using-net"></a><span data-ttu-id="c3750-104">Connecter votre appareil à votre IoT Hub à l’aide de .NET</span><span class="sxs-lookup"><span data-stu-id="c3750-104">Connect your device to your IoT hub using .NET</span></span>

[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="c3750-105">À la fin de ce didacticiel, vous disposerez de trois applications console .NET :</span><span class="sxs-lookup"><span data-stu-id="c3750-105">At the end of this tutorial, you have three .NET console apps:</span></span>

* <span data-ttu-id="c3750-106">**CreateDeviceIdentity**, qui crée une identité d’appareil et une clé de sécurité associée pour connecter votre application d’appareil.</span><span class="sxs-lookup"><span data-stu-id="c3750-106">**CreateDeviceIdentity**, which creates a device identity and associated security key to connect your device app.</span></span>
* <span data-ttu-id="c3750-107">**ReadDeviceToCloudMessages**, qui affiche les données de télémétrie envoyées par votre application d’appareil.</span><span class="sxs-lookup"><span data-stu-id="c3750-107">**ReadDeviceToCloudMessages**, which displays the telemetry sent by your device app.</span></span>
* <span data-ttu-id="c3750-108">**SimulatedDevice**, qui se connecte à votre IoT hub avec l’identité d’appareil créée précédemment et envoie un message de télémétrie chaque seconde en utilisant le protocole MQTT.</span><span class="sxs-lookup"><span data-stu-id="c3750-108">**SimulatedDevice**, which connects to your IoT hub with the device identity created earlier, and sends a telemetry message every second by using the MQTT protocol.</span></span>

<span data-ttu-id="c3750-109">Vous pouvez télécharger ou cloner la solution Visual Studio, qui contient les trois applications, à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="c3750-109">You can download or clone the Visual Studio solution, which contains the three apps from Github.</span></span>

```bash
git clone https://github.com/Azure-Samples/iot-hub-dotnet-simulated-device-client-app.git
```

> [!NOTE]
> <span data-ttu-id="c3750-110">Pour plus d’informations sur les kits de développement logiciel Azure IoT que vous pouvez utiliser pour générer les deux applications qui s’exécutent sur les appareils et sur le serveur de solution principal, voir l’article [Kits de développement logiciel (SDK) Azure IoT][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="c3750-110">For information about the Azure IoT SDKs that you can use to build both applications to run on devices, and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="c3750-111">Pour réaliser ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="c3750-111">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="c3750-112">Visual Studio 2015 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="c3750-112">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="c3750-113">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="c3750-113">An active Azure account.</span></span> <span data-ttu-id="c3750-114">(Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)</span><span class="sxs-lookup"><span data-stu-id="c3750-114">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="c3750-115">Votre IoT Hub est maintenant créé et vous connaissez le nom d’hôte et la chaîne de connexion à IoT Hub dont vous avez besoin pour terminer ce qu’il reste du didacticiel.</span><span class="sxs-lookup"><span data-stu-id="c3750-115">You have now created your IoT hub, and you have the host name and IoT Hub connection string that you need to complete the rest of this tutorial.</span></span>

<a id="DeviceIdentity_csharp"></a>
[!INCLUDE [iot-hub-get-started-create-device-identity-csharp](../../includes/iot-hub-get-started-create-device-identity-csharp.md)]

<a id="D2C_csharp"></a>
## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="c3750-116">Recevoir des messages appareil-à-cloud</span><span class="sxs-lookup"><span data-stu-id="c3750-116">Receive device-to-cloud messages</span></span>
<span data-ttu-id="c3750-117">Dans cette section, vous allez créer une application console .NET qui lit les messages des appareils vers le cloud dans l’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c3750-117">In this section, you create a .NET console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="c3750-118">Un IoT Hub expose un point de terminaison compatible avec [Azure Event Hubs][lnk-event-hubs-overview] pour vous permettre de lire les messages appareil-à-cloud.</span><span class="sxs-lookup"><span data-stu-id="c3750-118">An IoT hub exposes an [Azure Event Hubs][lnk-event-hubs-overview]-compatible endpoint to enable you to read device-to-cloud messages.</span></span> <span data-ttu-id="c3750-119">Pour simplifier les choses, ce didacticiel crée un lecteur de base qui ne convient pas dans le cas d’un déploiement à débit élevé.</span><span class="sxs-lookup"><span data-stu-id="c3750-119">To keep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="c3750-120">Pour découvrir comment traiter les messages appareil-à-cloud à grande échelle, reportez-vous au didacticiel [Traitement des messages appareil-à-cloud][lnk-process-d2c-tutorial].</span><span class="sxs-lookup"><span data-stu-id="c3750-120">To learn how to process device-to-cloud messages at scale, see the [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span> <span data-ttu-id="c3750-121">Pour plus d’informations sur la façon de traiter les messages à partir des concentrateurs d’événements, reportez-vous au didacticiel [Prise en main des concentrateurs d’événements][lnk-eventhubs-tutorial].</span><span class="sxs-lookup"><span data-stu-id="c3750-121">For more information about how to process messages from Event Hubs, see the [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial.</span></span> <span data-ttu-id="c3750-122">(Ce didacticiel s’applique aux points de terminaison compatibles Event Hub IoT Hub).</span><span class="sxs-lookup"><span data-stu-id="c3750-122">(This tutorial is applicable to the IoT Hub Event Hub-compatible endpoints.)</span></span>

> [!NOTE]
> <span data-ttu-id="c3750-123">Le point de terminaison compatible Event Hub pour lire des messages de l’appareil vers le cloud utilise toujours le protocole AMQP.</span><span class="sxs-lookup"><span data-stu-id="c3750-123">The Event Hub-compatible endpoint for reading device-to-cloud messages always uses the AMQP protocol.</span></span>

1. <span data-ttu-id="c3750-124">Dans Visual Studio, ajoutez un projet Visual C# Bureau classique Windows à la solution actuelle en utilisant le modèle de projet **Application console (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="c3750-124">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution, by using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="c3750-125">Assurez-vous que la version du .NET Framework est définie sur 4.5.1 ou supérieur.</span><span class="sxs-lookup"><span data-stu-id="c3750-125">Make sure the .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="c3750-126">Nommez le projet **ReadDeviceToCloudMessages**.</span><span class="sxs-lookup"><span data-stu-id="c3750-126">Name the project **ReadDeviceToCloudMessages**.</span></span>

    ![Nouveau projet Visual C# Bureau classique Windows][10a]

2. <span data-ttu-id="c3750-128">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur le projet **ReadDeviceToCloudMessages**, puis cliquez sur **Gérer les packages Nuget**.</span><span class="sxs-lookup"><span data-stu-id="c3750-128">In Solution Explorer, right-click the **ReadDeviceToCloudMessages** project, and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="c3750-129">Dans la fenêtre **Gestionnaire de package Nuget**, recherchez **WindowsAzure.ServiceBus**, cliquez sur **Installer** et acceptez les conditions d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="c3750-129">In the **NuGet Package Manager** window, search for **WindowsAzure.ServiceBus**, select **Install**, and accept the terms of use.</span></span> <span data-ttu-id="c3750-130">Cette procédure lance le téléchargement, l’installation et ajoute une référence à [Azure Service Bus][lnk-servicebus-nuget] avec toutes ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="c3750-130">This procedure downloads, installs, and adds a reference to [Azure Service Bus][lnk-servicebus-nuget], with all its dependencies.</span></span> <span data-ttu-id="c3750-131">Ce package permet à l'application de se connecter au point de terminaison compatible Event Hubs sur votre IoT hub.</span><span class="sxs-lookup"><span data-stu-id="c3750-131">This package enables the application to connect to the Event Hub-compatible endpoint on your IoT hub.</span></span>

4. <span data-ttu-id="c3750-132">Ajoutez les instructions `using` suivantes en haut du fichier **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="c3750-132">Add the following `using` statements at the top of the **Program.cs** file:</span></span>

    ```csharp
    using Microsoft.ServiceBus.Messaging;
    using System.Threading;
    ```

5. <span data-ttu-id="c3750-133">Ajoutez les champs suivants à la classe **Program** .</span><span class="sxs-lookup"><span data-stu-id="c3750-133">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="c3750-134">Remplacez la valeur d’espace réservé par la chaîne de connexion IoT Hub pour le hub créé dans la section Créer un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="c3750-134">Replace the placeholder value with the IoT Hub connection string for the hub you created in the "Create an IoT hub" section.</span></span>

    ```csharp
    static string connectionString = "{iothub connection string}";
    static string iotHubD2cEndpoint = "messages/events";
    static EventHubClient eventHubClient;
    ```

6. <span data-ttu-id="c3750-135">Ajoutez la méthode suivante à la classe **Program** :</span><span class="sxs-lookup"><span data-stu-id="c3750-135">Add the following method to the **Program** class:</span></span>

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

    <span data-ttu-id="c3750-136">Cette méthode utilise une instance **EventHubReceiver** pour recevoir des messages à partir de toutes les partitions de réception Appareil vers cloud IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c3750-136">This method uses an **EventHubReceiver** instance to receive messages from all the IoT hub device-to-cloud receive partitions.</span></span> <span data-ttu-id="c3750-137">Notez la manière dont vous transmettez un paramètre `DateTime.Now` lorsque vous créez l’objet **EventHubReceiver** pour qu’il reçoive uniquement les messages envoyés après son démarrage.</span><span class="sxs-lookup"><span data-stu-id="c3750-137">Notice how you pass a `DateTime.Now` parameter when you create the **EventHubReceiver** object, so that it only receives messages sent after it starts.</span></span> <span data-ttu-id="c3750-138">Dans un environnement de test, ce filtre permet de voir l’ensemble des messages en cours.</span><span class="sxs-lookup"><span data-stu-id="c3750-138">This filter is useful in a test environment so you can see the current set of messages.</span></span> <span data-ttu-id="c3750-139">Dans un environnement de production, votre code doit faire en sorte de traiter tous les messages.</span><span class="sxs-lookup"><span data-stu-id="c3750-139">In a production environment, your code should make sure that it processes all the messages.</span></span> <span data-ttu-id="c3750-140">Pour plus d’informations, voir le didacticiel [Traiter les messages appareil-à-cloud IoT Hub en utilisant les itinéraires (.NET)][lnk-process-d2c-tutorial].</span><span class="sxs-lookup"><span data-stu-id="c3750-140">For more information, see the tutorial [How to process IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial].</span></span>

7. <span data-ttu-id="c3750-141">Enfin, ajoutez les lignes suivantes à la méthode **Main** :</span><span class="sxs-lookup"><span data-stu-id="c3750-141">Finally, add the following lines to the **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Receive messages. Ctrl-C to exit.\n");
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

## <a name="create-a-device-app"></a><span data-ttu-id="c3750-142">Créer une application d’appareil</span><span class="sxs-lookup"><span data-stu-id="c3750-142">Create a device app</span></span>

<span data-ttu-id="c3750-143">Dans cette section, vous allez créer une application console .NET qui simule un appareil envoyant des messages des appareils vers le cloud à un IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c3750-143">In this section, you create a .NET console app that simulates a device that sends device-to-cloud messages to an IoT hub.</span></span>

1. <span data-ttu-id="c3750-144">Dans Visual Studio, ajoutez un projet Visual C# Bureau classique Windows à la solution actuelle en utilisant le modèle de projet **Application console (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="c3750-144">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution, by using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="c3750-145">Assurez-vous que la version du .NET Framework est définie sur 4.5.1 ou supérieur.</span><span class="sxs-lookup"><span data-stu-id="c3750-145">Make sure the .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="c3750-146">Nommez le projet **SimulatedDevice**.</span><span class="sxs-lookup"><span data-stu-id="c3750-146">Name the project **SimulatedDevice**.</span></span>

    ![Nouveau projet Visual C# Bureau classique Windows][10b]

2. <span data-ttu-id="c3750-148">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur le projet **SimulatedDevice**, puis cliquez sur **Gérer les packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="c3750-148">In Solution Explorer, right-click the **SimulatedDevice** project, and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="c3750-149">Dans la fenêtre **Gestionnaire de package NuGet**, cliquez sur **Parcourir**, puis recherchez **Microsoft.Azure.Devices.Client**. Cliquez ensuite sur **Installer** pour installer le package **Microsoft.Azure.Devices.Client**, puis acceptez les conditions d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="c3750-149">In the **NuGet Package Manager** window, select **Browse**, search for **Microsoft.Azure.Devices.Client**, select **Install** to install the **Microsoft.Azure.Devices.Client** package, and accept the terms of use.</span></span> <span data-ttu-id="c3750-150">Cette procédure lance le téléchargement et l’installation et ajoute une référence au [package Azure IoT Device SDK NuGet][lnk-device-nuget] et ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="c3750-150">This procedure downloads, installs, and adds a reference to the [Azure IoT device SDK NuGet package][lnk-device-nuget] and its dependencies.</span></span>

4. <span data-ttu-id="c3750-151">Ajoutez l'instruction `using` suivante en haut du fichier **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="c3750-151">Add the following `using` statement at the top of the **Program.cs** file:</span></span>

    ```csharp
    using Microsoft.Azure.Devices.Client;
    using Newtonsoft.Json;
    ```

5. <span data-ttu-id="c3750-152">Ajoutez les champs suivants à la classe **Program** .</span><span class="sxs-lookup"><span data-stu-id="c3750-152">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="c3750-153">Remplacez `{iot hub hostname}` par le nom d’hôte IoT Hub que vous avez récupéré dans le cadre de la section « Créer un hub IoT ».</span><span class="sxs-lookup"><span data-stu-id="c3750-153">Substitute `{iot hub hostname}` with the IoT hub host name you retrieved in the "Create an IoT hub" section.</span></span> <span data-ttu-id="c3750-154">Remplacez `{device key}` par la clé d’appareil que vous avez récupérée au cours de la section « Création d’une identité d’appareil ».</span><span class="sxs-lookup"><span data-stu-id="c3750-154">Substitute `{device key}` with the device key you retrieved in the "Create a device identity" section.</span></span>

    ```csharp
    static DeviceClient deviceClient;
    static string iotHubUri = "{iot hub hostname}";
    static string deviceKey = "{device key}";
    ```

6. <span data-ttu-id="c3750-155">Ajoutez la méthode suivante à la classe **Program** :</span><span class="sxs-lookup"><span data-stu-id="c3750-155">Add the following method to the **Program** class:</span></span>

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

    <span data-ttu-id="c3750-156">Cette méthode envoie un nouveau message Appareil vers cloud toutes les secondes.</span><span class="sxs-lookup"><span data-stu-id="c3750-156">This method sends a new device-to-cloud message every second.</span></span> <span data-ttu-id="c3750-157">Ce message contient un objet JSON sérialisé avec l’ID de l’appareil et des nombres générés de manière aléatoire pour simuler un thermomètre et un capteur d’humidité.</span><span class="sxs-lookup"><span data-stu-id="c3750-157">The message contains a JSON-serialized object, with the device ID and randomly generated numbers to simulate a temperature sensor, and a humidity sensor.</span></span>

7. <span data-ttu-id="c3750-158">Enfin, ajoutez les lignes suivantes à la méthode **Main** :</span><span class="sxs-lookup"><span data-stu-id="c3750-158">Finally, add the following lines to the **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Simulated device\n");
    deviceClient = DeviceClient.Create(iotHubUri, new DeviceAuthenticationWithRegistrySymmetricKey ("myFirstDevice", deviceKey), TransportType.Mqtt);

    SendDeviceToCloudMessagesAsync();
    Console.ReadLine();
    ```

    <span data-ttu-id="c3750-159">Par défaut, la méthode de création **Create** d’une application .NET Framework crée une instance **DeviceClient** qui utilise le protocole AMQP pour communiquer avec IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c3750-159">By default, the **Create** method in a .NET Framework app creates a **DeviceClient** instance that uses the AMQP protocol to communicate with IoT Hub.</span></span> <span data-ttu-id="c3750-160">Pour utiliser le protocole MQTT ou HTTP, remplacez la méthode **Create** afin de pouvoir spécifier le protocole.</span><span class="sxs-lookup"><span data-stu-id="c3750-160">To use the MQTT or HTTP protocol, use the override of the **Create** method that enables you to specify the protocol.</span></span> <span data-ttu-id="c3750-161">Les clients UWP et PCL utilisent le protocole HTTP par défaut.</span><span class="sxs-lookup"><span data-stu-id="c3750-161">UWP and PCL clients use the HTTP protocol by default.</span></span> <span data-ttu-id="c3750-162">Si vous utilisez le protocole HTTP, vous devez également ajouter le package NuGet **Microsoft.AspNet.WebApi.Client** à votre projet de manière à inclure l’espace de noms **System.Net.Http.Formatting**.</span><span class="sxs-lookup"><span data-stu-id="c3750-162">If you use the HTTP protocol, you should also add the **Microsoft.AspNet.WebApi.Client** NuGet package to your project to include the **System.Net.Http.Formatting** namespace.</span></span>

<span data-ttu-id="c3750-163">Ce didacticiel vous accompagne tout au long des étapes de création d’une application d’appareil IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c3750-163">This tutorial takes you through the steps to create an IoT Hub device app.</span></span> <span data-ttu-id="c3750-164">Vous pouvez également utiliser l’extension [Connected Service for Azure IoT Hub][lnk-connected-service] de Visual Studio pour ajouter le code nécessaire à votre application d’appareil.</span><span class="sxs-lookup"><span data-stu-id="c3750-164">You can also use the [Connected Service for Azure IoT Hub][lnk-connected-service] Visual Studio extension to add the necessary code to your device app.</span></span>

> [!NOTE]
> <span data-ttu-id="c3750-165">Pour simplifier les choses, ce didacticiel n’implémente aucune stratégie de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="c3750-165">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="c3750-166">Dans le code de production, vous devez mettre en œuvre des stratégies de nouvelle tentative (par exemple, une interruption exponentielle), comme indiqué dans l’article MSDN [Gestion des erreurs temporaires][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="c3750-166">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="run-the-apps"></a><span data-ttu-id="c3750-167">Exécuter les applications</span><span class="sxs-lookup"><span data-stu-id="c3750-167">Run the apps</span></span>

<span data-ttu-id="c3750-168">Vous êtes maintenant prêt à exécuter les applications.</span><span class="sxs-lookup"><span data-stu-id="c3750-168">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="c3750-169">Dans Visual Studio, dans l’explorateur de solutions, cliquez avec le bouton droit sur votre solution, puis sur **Définir les projets de démarrage**.</span><span class="sxs-lookup"><span data-stu-id="c3750-169">In Visual Studio, in Solution Explorer, right-click your solution, and then click **Set StartUp projects**.</span></span> <span data-ttu-id="c3750-170">Sélectionnez **Plusieurs projets de démarrage**, puis **Démarrer** en tant qu’action pour les projets **ReadDeviceToCloudMessages** et **SimulatedDevice**.</span><span class="sxs-lookup"><span data-stu-id="c3750-170">Select **Multiple startup projects**, and then select **Start** as the action for both the **ReadDeviceToCloudMessages** and **SimulatedDevice** projects.</span></span>

    ![Propriétés de démarrage de projet][41]

2. <span data-ttu-id="c3750-172">Appuyez sur **F5** pour démarrer les deux applications.</span><span class="sxs-lookup"><span data-stu-id="c3750-172">Press **F5** to start both apps running.</span></span> <span data-ttu-id="c3750-173">La sortie de console à partir de l’application **SimulatedDevice** affiche les messages envoyés par votre application d’appareil à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c3750-173">The console output from the **SimulatedDevice** app shows the messages your device app sends to your IoT hub.</span></span> <span data-ttu-id="c3750-174">La sortie de console à partir de l’application **ProcessDeviceToCloudMessages** affiche les messages reçus par votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c3750-174">The console output from the **ReadDeviceToCloudMessages** app shows the messages that your IoT hub receives.</span></span>

    ![Sortie de console à partir d’applications][42]

3. <span data-ttu-id="c3750-176">La vignette **Utilisation** du [portail Azure][lnk-portal] indique le nombre de messages envoyés au IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="c3750-176">The **Usage** tile in the [Azure portal][lnk-portal] shows the number of messages sent to the IoT hub:</span></span>

    ![Vignette Utilisation du portail Azure][43]

## <a name="next-steps"></a><span data-ttu-id="c3750-178">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c3750-178">Next steps</span></span>

<span data-ttu-id="c3750-179">Dans ce didacticiel, vous avez configuré un IoT Hub dans le portail Azure, puis créé une identité d’appareil dans le registre d’identités de l’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c3750-179">In this tutorial, you configured an IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="c3750-180">Vous avez utilisé cette identité d’appareil pour permettre à l’application d’appareil d’envoyer des messages appareil-à-cloud à l’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c3750-180">You used this device identity to enable the device app to send device-to-cloud messages to the IoT hub.</span></span> <span data-ttu-id="c3750-181">Vous avez également créé une application qui affiche les messages reçus par l’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c3750-181">You also created an app that displays the messages received by the IoT hub.</span></span>

<span data-ttu-id="c3750-182">Pour continuer la prise en main de IoT Hub et explorer les autres scénarios IoT, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="c3750-182">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="c3750-183">[Connexion de votre appareil][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="c3750-183">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="c3750-184">[Prise en main de la gestion d’appareils][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="c3750-184">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="c3750-185">[Bien démarrer avec IoT Edge][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="c3750-185">[Getting started with IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="c3750-186">Pour découvrir comment étendre votre solution IoT et traiter les messages appareil-à-cloud à grande échelle, consultez le didacticiel [Traitement des messages appareil-à-cloud][lnk-process-d2c-tutorial].</span><span class="sxs-lookup"><span data-stu-id="c3750-186">To learn how to extend your IoT solution and process device-to-cloud messages at scale, see the [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>

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
