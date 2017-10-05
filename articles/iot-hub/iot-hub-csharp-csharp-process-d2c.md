---
title: "Traiter les messages appareil-à-cloud Azure IoT Hub en utilisant les itinéraires (.Net) | Microsoft Docs"
description: "Comment traiter des messages appareil-à-cloud IoT Hub en utilisant les règles de routage et les points de terminaison personnalisés pour distribuer les messages vers d’autres services principaux."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 5177bac9-722f-47ef-8a14-b201142ba4bc
ms.service: iot-hub
ms.devlang: csharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 1d2b52ea005ab520bf294efa603512c00a92ee63
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="process-iot-hub-device-to-cloud-messages-using-routes-net"></a><span data-ttu-id="1ab91-103">Traiter les messages appareil-à-cloud IoT Hub en utilisant les itinéraires (.NET)</span><span class="sxs-lookup"><span data-stu-id="1ab91-103">Process IoT Hub device-to-cloud messages using routes (.NET)</span></span>

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

<span data-ttu-id="1ab91-104">Ce didacticiel s’appuie sur celui relatif à la [prise en main du IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="1ab91-104">This tutorial builds on the [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="1ab91-105">Le didacticiel :</span><span class="sxs-lookup"><span data-stu-id="1ab91-105">The tutorial:</span></span>

* <span data-ttu-id="1ab91-106">Explique comment utiliser les règles de routage pour dispatcher les messages de l’appareil au cloud suivant une configuration facile.</span><span class="sxs-lookup"><span data-stu-id="1ab91-106">Shows you how to use routing rules to dispatch device-to-cloud messages in an easy, configuration-based way.</span></span>
* <span data-ttu-id="1ab91-107">Indique comment isoler les messages interactifs qui nécessitent une action immédiate du serveur principal de la solution pour un traitement ultérieur.</span><span class="sxs-lookup"><span data-stu-id="1ab91-107">Illustrates how to isolate interactive messages that require immediate action from the solution back end for further processing.</span></span> <span data-ttu-id="1ab91-108">Par exemple, un appareil peut envoyer un message d’alerte qui déclenche l’insertion d’un ticket dans un système CRM.</span><span class="sxs-lookup"><span data-stu-id="1ab91-108">For example, a device might send an alarm message that triggers inserting a ticket into a CRM system.</span></span> <span data-ttu-id="1ab91-109">Par opposition, les messages de point de données tels que la télémétrie de température sont chargés dans un moteur d’analyse.</span><span class="sxs-lookup"><span data-stu-id="1ab91-109">In contrast, data-point messages, such as temperature telemetry, feed into an analytics engine.</span></span>

<span data-ttu-id="1ab91-110">À la fin de ce didacticiel, vous exécutez trois applications console .NET :</span><span class="sxs-lookup"><span data-stu-id="1ab91-110">At the end of this tutorial, you run three .NET console apps:</span></span>

* <span data-ttu-id="1ab91-111">**SimulatedDevice**, une version modifiée de l’application créée dans le didacticiel [prise en main du IoT Hub] qui envoie des messages de point de données des appareils vers le cloud chaque seconde et des messages interactifs des appareils vers le cloud toutes les 10 secondes.</span><span class="sxs-lookup"><span data-stu-id="1ab91-111">**SimulatedDevice**, a modified version of the app created in the [Get started with IoT Hub] tutorial sends data-point device-to-cloud messages every second, and interactive device-to-cloud messages every 10 seconds.</span></span>
* <span data-ttu-id="1ab91-112">**ReadDeviceToCloudMessages**, qui affiche les données non critiques de télémétrie envoyées par votre application d’appareil.</span><span class="sxs-lookup"><span data-stu-id="1ab91-112">**ReadDeviceToCloudMessages** that displays the non-critical telemetry sent by your device app.</span></span>
* <span data-ttu-id="1ab91-113">**ReadCriticalQueue** enlève de la file d’attente Service Bus les messages critiques envoyés par votre application d’appareil.</span><span class="sxs-lookup"><span data-stu-id="1ab91-113">**ReadCriticalQueue** de-queues the critical messages sent by your device app from a Service Bus queue.</span></span> <span data-ttu-id="1ab91-114">Cette file d’attente est attachée à IoT hub.</span><span class="sxs-lookup"><span data-stu-id="1ab91-114">This queue is attached to the IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="1ab91-115">IoT Hub offre la prise en charge de Kit de développement logiciel (SDK) de plusieurs plateformes d’appareils et de plusieurs langages (notamment C, Java et JavaScript).</span><span class="sxs-lookup"><span data-stu-id="1ab91-115">IoT Hub has SDK support for many device platforms and languages, including C, Java, and JavaScript.</span></span> <span data-ttu-id="1ab91-116">Pour savoir comment remplacer l’appareil simulé de ce didacticiel par un appareil physique, voir le [Centre de développement Azure IoT].</span><span class="sxs-lookup"><span data-stu-id="1ab91-116">To learn how to replace the simulated device in this tutorial with a physical device, see the [Azure IoT Developer Center].</span></span>

<span data-ttu-id="1ab91-117">Pour réaliser ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="1ab91-117">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="1ab91-118">Visual Studio 2015 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="1ab91-118">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="1ab91-119">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="1ab91-119">An active Azure account.</span></span> <br/><span data-ttu-id="1ab91-120">Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit](https://azure.microsoft.com/free/) en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="1ab91-120">If you don't have an account, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

<span data-ttu-id="1ab91-121">Vous devez avoir une connaissance de base de [Stockage Azure] et d’[Azure Service Bus].</span><span class="sxs-lookup"><span data-stu-id="1ab91-121">You should have some basic knowledge of [Azure Storage] and [Azure Service Bus].</span></span>

## <a name="send-interactive-messages"></a><span data-ttu-id="1ab91-122">Envoyer des messages interactifs</span><span class="sxs-lookup"><span data-stu-id="1ab91-122">Send interactive messages</span></span>

<span data-ttu-id="1ab91-123">Modifiez l’application d’appareil créée dans le didacticiel [prise en main du IoT Hub] de façon à envoyer occasionnellement des messages interactifs.</span><span class="sxs-lookup"><span data-stu-id="1ab91-123">Modify the device app you created in the [Get started with IoT Hub] tutorial to occasionally send interactive messages.</span></span>

<span data-ttu-id="1ab91-124">Dans Visual Studio, dans le projet **SimulatedDevice**, remplacez la méthode `SendDeviceToCloudMessagesAsync` par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="1ab91-124">In Visual Studio, in the **SimulatedDevice** project, replace the `SendDeviceToCloudMessagesAsync` method with the following code:</span></span>

```csharp
private static async void SendDeviceToCloudMessagesAsync()
{
    double minTemperature = 20;
    double minHumidity = 60;
    Random rand = new Random();

    while (true)
    {
        double currentTemperature = minTemperature + rand.NextDouble() * 15;
        double currentHumidity = minHumidity + rand.NextDouble() * 20;

        var telemetryDataPoint = new
        {
            deviceId = "myFirstDevice",
            temperature = currentTemperature,
            humidity = currentHumidity
        };
        var messageString = JsonConvert.SerializeObject(telemetryDataPoint);
        string levelValue;

        if (rand.NextDouble() > 0.7)
        {
            messageString = "This is a critical message";
            levelValue = "critical";
        }
        else
        {
            levelValue = "normal";
        }
        
        var message = new Message(Encoding.ASCII.GetBytes(messageString));
        message.Properties.Add("level", levelValue);
        
        await deviceClient.SendEventAsync(message);
        Console.WriteLine("{0} > Sent message: {1}", DateTime.Now, messageString);

        await Task.Delay(1000);
    }
}
```

<span data-ttu-id="1ab91-125">Cela ajoute au hasard la propriété `"level": "critical"` aux messages envoyés par l’appareil, ce qui simule un message qui requiert une action immédiate du serveur principal de la solution.</span><span class="sxs-lookup"><span data-stu-id="1ab91-125">This method randomly adds the property `"level": "critical"` to messages sent by the device, which simulates a message that requires immediate action by the solution back-end.</span></span> <span data-ttu-id="1ab91-126">L’application d’appareil transmet ces informations dans les propriétés du message, plutôt que dans le corps du message, afin que IoT Hub puisse acheminer le message vers la destination adéquate.</span><span class="sxs-lookup"><span data-stu-id="1ab91-126">The device app passes this information in the message properties, instead of in the message body, so that IoT Hub can route the message to the proper message destination.</span></span>

> [!NOTE]
> <span data-ttu-id="1ab91-127">Vous pouvez utiliser les propriétés de message pour acheminer les messages pour de nombreux scénarios, tels que le traitement de chemin d’accès à froid, en plus de l’exemple de chemin d’accès à chaud présenté ici.</span><span class="sxs-lookup"><span data-stu-id="1ab91-127">You can use message properties to route messages for various scenarios including cold-path processing, in addition to the hot-path example shown here.</span></span>

> [!NOTE]
> <span data-ttu-id="1ab91-128">Par souci de simplicité, ce didacticiel n’implémente aucune stratégie de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="1ab91-128">For the sake of simplicity, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="1ab91-129">Dans le code de production, vous devez mettre en œuvre des stratégies de nouvelle tentative (par exemple, une interruption exponentielle), comme indiqué dans l’article MSDN [Transient Fault Handling](Gestion des erreurs temporaires).</span><span class="sxs-lookup"><span data-stu-id="1ab91-129">In production code, you should implement a retry policy such as exponential backoff, as suggested in the MSDN article [Transient Fault Handling].</span></span>

## <a name="route-messages-to-a-queue-in-your-iot-hub"></a><span data-ttu-id="1ab91-130">Router les messages vers une file d’attente dans votre IoT hub</span><span class="sxs-lookup"><span data-stu-id="1ab91-130">Route messages to a queue in your IoT hub</span></span>

<span data-ttu-id="1ab91-131">Dans cette section, vous allez :</span><span class="sxs-lookup"><span data-stu-id="1ab91-131">In this section, you:</span></span>

* <span data-ttu-id="1ab91-132">créer une file d’attente Service Bus ;</span><span class="sxs-lookup"><span data-stu-id="1ab91-132">Create a Service Bus queue.</span></span>
* <span data-ttu-id="1ab91-133">la connecter à votre IoT Hub ;</span><span class="sxs-lookup"><span data-stu-id="1ab91-133">Connect it to your IoT hub.</span></span>
* <span data-ttu-id="1ab91-134">configurer votre IoT Hub pour envoyer des messages à la file d’attente, en fonction de la présence d’une propriété dans le message.</span><span class="sxs-lookup"><span data-stu-id="1ab91-134">Configure your IoT hub to send messages to the queue based on the presence of a property on the message.</span></span>

<span data-ttu-id="1ab91-135">Pour plus d’informations sur la façon de traiter les messages des files d’attente Service Bus, consultez [Prise en main des files d’attente][Service Bus queue].</span><span class="sxs-lookup"><span data-stu-id="1ab91-135">For more information about how to process messages from Service Bus queues, see [Get started with queues][Service Bus queue].</span></span>

1. <span data-ttu-id="1ab91-136">Créez une file d’attente Service Bus, comme décrit dans [Prise en main des files d’attente][Service Bus queue].</span><span class="sxs-lookup"><span data-stu-id="1ab91-136">Create a Service Bus queue as described in [Get started with queues][Service Bus queue].</span></span> <span data-ttu-id="1ab91-137">La file d’attente doit être située dans les mêmes région et abonnement que votre IoT hub.</span><span class="sxs-lookup"><span data-stu-id="1ab91-137">The queue must be in the same subscription and region as your IoT hub.</span></span> <span data-ttu-id="1ab91-138">Prenez note de l’espace de noms et de la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="1ab91-138">Make a note of the namespace and queue name.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1ab91-139">Les options **Sessions** ou **Détection des doublons** ne doivent pas être activées pour les files d’attente et rubriques Service Bus utilisées comme points de terminaison IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1ab91-139">Service Bus queues and topics used as IoT Hub endpoints must not have **Sessions** or **Duplicate Detection** enabled.</span></span> <span data-ttu-id="1ab91-140">Si l’une de ces options est activée, le point de terminaison s’affiche comme **Inaccessible** dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1ab91-140">If either of those options are enabled, the endpoint appears as **Unreachable** in the Azure portal.</span></span>

2. <span data-ttu-id="1ab91-141">Dans le portail Azure, ouvrez votre IoT Hub, puis cliquez sur **Points de terminaison**.</span><span class="sxs-lookup"><span data-stu-id="1ab91-141">In the Azure portal, open your IoT hub and click **Endpoints**.</span></span>
    
    ![Points de terminaison dans IoT hub][30]

3. <span data-ttu-id="1ab91-143">En haut du panneau **Points de terminaison**, cliquez sur **Ajouter** pour ajouter votre file d’attente à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1ab91-143">In the **Endpoints** blade, click **Add** at the top to add your queue to your IoT hub.</span></span> <span data-ttu-id="1ab91-144">Nommez le point de terminaison **CriticalQueue**, puis utilisez les listes déroulantes pour sélectionner **File d’attente Service Bus**, l’espace de noms Service Bus dans lequel réside votre file d’attente, ainsi que le nom de votre file d’attente.</span><span class="sxs-lookup"><span data-stu-id="1ab91-144">Name the endpoint **CriticalQueue** and use the drop-downs to select **Service Bus queue**, the Service Bus namespace in which your queue resides, and the name of your queue.</span></span> <span data-ttu-id="1ab91-145">Lorsque vous avez terminé, cliquez sur **Enregistrer** en bas.</span><span class="sxs-lookup"><span data-stu-id="1ab91-145">When you are done, click **Save** at the bottom.</span></span>
    
    ![Ajout d’un point de terminaison][31]
    
4. <span data-ttu-id="1ab91-147">À présent, cliquez sur **Itinéraires** dans votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1ab91-147">Now click **Routes** in your IoT Hub.</span></span> <span data-ttu-id="1ab91-148">En haut du panneau, cliquez sur **Ajouter** afin de créer une règle qui achemine les messages vers la file d’attente que vous venez d’ajouter.</span><span class="sxs-lookup"><span data-stu-id="1ab91-148">Click **Add** at the top of the blade to create a routing rule that routes messages to the queue you just added.</span></span> <span data-ttu-id="1ab91-149">Sélectionnez **DeviceTelemetry** comme source de données.</span><span class="sxs-lookup"><span data-stu-id="1ab91-149">Select **DeviceTelemetry** as the source of data.</span></span> <span data-ttu-id="1ab91-150">Saisissez `level="critical"` comme condition, puis sélectionnez la file d’attente que vous venez d’ajouter comme point de terminaison personnalisé en tant que point de terminaison de la règle de routage.</span><span class="sxs-lookup"><span data-stu-id="1ab91-150">Enter `level="critical"` as the condition, and choose the queue you just added as a custom endpoint as the routing rule endpoint.</span></span> <span data-ttu-id="1ab91-151">Lorsque vous avez terminé, cliquez sur **Enregistrer** en bas.</span><span class="sxs-lookup"><span data-stu-id="1ab91-151">When you are done, click **Save** at the bottom.</span></span>
    
    ![Ajout d’un itinéraire][32]
    
    <span data-ttu-id="1ab91-153">Assurez-vous que l’itinéraire de secours est défini sur **ACTIVÉ**.</span><span class="sxs-lookup"><span data-stu-id="1ab91-153">Make sure the fallback route is set to **ON**.</span></span> <span data-ttu-id="1ab91-154">Il s’agit de la configuration par défaut d’une instance IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1ab91-154">This value is the default configuration for an IoT hub.</span></span>
    
    ![Itinéraire de secours][33]

## <a name="read-from-the-queue-endpoint"></a><span data-ttu-id="1ab91-156">Lecture à partir du point de terminaison de la file d’attente</span><span class="sxs-lookup"><span data-stu-id="1ab91-156">Read from the queue endpoint</span></span>

<span data-ttu-id="1ab91-157">Dans cette section, vous allez lire les messages à partir du point de terminaison de la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="1ab91-157">In this section, you read the messages from the queue endpoint.</span></span>

1. <span data-ttu-id="1ab91-158">Dans Visual Studio, ajoutez un projet Visual C# Bureau classique Windows à la solution actuelle en utilisant le modèle de projet **Application console (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="1ab91-158">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution, by using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="1ab91-159">Nommez le projet **ReadCriticalQueue**.</span><span class="sxs-lookup"><span data-stu-id="1ab91-159">Name the project **ReadCriticalQueue**.</span></span>

2. <span data-ttu-id="1ab91-160">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur le projet **ReadCriticalQueue**, puis cliquez sur **Gérer les packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="1ab91-160">In Solution Explorer, right-click the **ReadCriticalQueue** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="1ab91-161">Cela affiche la fenêtre **Gestionnaire de packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="1ab91-161">This operation displays the **NuGet Package Manager** window.</span></span>

3. <span data-ttu-id="1ab91-162">Recherchez **WindowsAzure.ServiceBus**, cliquez sur **Installer**, puis acceptez les conditions d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="1ab91-162">Search for **WindowsAzure.ServiceBus**, click **Install**, and accept the terms of use.</span></span> <span data-ttu-id="1ab91-163">Cette opération lance le téléchargement, l’installation et ajoute une référence à Azure Service Bus avec toutes ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="1ab91-163">This operation downloads, installs, and adds a reference to the Azure Service Bus, with all its dependencies.</span></span>

4. <span data-ttu-id="1ab91-164">Ajoutez les instructions **using** suivantes au début du fichier **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="1ab91-164">Add the following **using** statements at the top of the **Program.cs** file:</span></span>
   
    ```csharp
    using System.IO;
    using Microsoft.ServiceBus.Messaging;
    ```

5. <span data-ttu-id="1ab91-165">Enfin, ajoutez les lignes suivantes à la méthode **Main** .</span><span class="sxs-lookup"><span data-stu-id="1ab91-165">Finally, add the following lines to the **Main** method.</span></span> <span data-ttu-id="1ab91-166">Remplacez la chaîne de connexion par des autorisations **Listen** pour la file d’attente :</span><span class="sxs-lookup"><span data-stu-id="1ab91-166">Substitute the connection string with **Listen** permissions for the queue:</span></span>
   
    ```csharp
    Console.WriteLine("Receive critical messages. Ctrl-C to exit.\n");
    var connectionString = "{service bus listen string}";
    var queueName = "{queue name}";
    
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);

    client.OnMessage(message =>
        {
            Stream stream = message.GetBody<Stream>();
            StreamReader reader = new StreamReader(stream, Encoding.ASCII);
            string s = reader.ReadToEnd();
            Console.WriteLine(String.Format("Message body: {0}", s));
        });
        
    Console.ReadLine();
    ```

## <a name="run-the-applications"></a><span data-ttu-id="1ab91-167">Exécution des applications</span><span class="sxs-lookup"><span data-stu-id="1ab91-167">Run the applications</span></span>
<span data-ttu-id="1ab91-168">Vous êtes maintenant prêt à exécuter les applications.</span><span class="sxs-lookup"><span data-stu-id="1ab91-168">Now you are ready to run the applications.</span></span>

1. <span data-ttu-id="1ab91-169">Dans Visual Studio, dans l’Explorateur de solutions, cliquez avec le bouton droit sur votre solution, puis sélectionnez **Définir les projets de démarrage**.</span><span class="sxs-lookup"><span data-stu-id="1ab91-169">In Visual Studio, in Solution Explorer, right-click your solution and select **Set StartUp Projects**.</span></span> <span data-ttu-id="1ab91-170">Sélectionnez **Plusieurs projets de démarrage**, puis sélectionnez **Démarrer** en tant qu’action pour les projets **ReadDeviceToCloudMessages**, **SimulatedDevice** et **ReadCriticalQueue**.</span><span class="sxs-lookup"><span data-stu-id="1ab91-170">Select **Multiple startup projects**, then select **Start** as the action for the **ReadDeviceToCloudMessages**, **SimulatedDevice**, and **ReadCriticalQueue** projects.</span></span>
2. <span data-ttu-id="1ab91-171">Appuyez sur **F5** pour lancer les trois applications de console.</span><span class="sxs-lookup"><span data-stu-id="1ab91-171">Press **F5** to start the three console apps.</span></span> <span data-ttu-id="1ab91-172">L’application **ReadDeviceToCloudMessages** reçoit uniquement les messages non critiques provenant de l’application **SimulatedDevice**, tandis que l’application **ReadCriticalQueue** reçoit uniquement les messages critiques.</span><span class="sxs-lookup"><span data-stu-id="1ab91-172">The **ReadDeviceToCloudMessages** app has only non-critical messages sent from the **SimulatedDevice** application, and the **ReadCriticalQueue** app has only critical messages.</span></span>
   
   ![Trois applications de console][50]

## <a name="next-steps"></a><span data-ttu-id="1ab91-174">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1ab91-174">Next steps</span></span>
<span data-ttu-id="1ab91-175">Dans ce didacticiel, vous avez appris à répartir de façon fiable des messages appareil-à-cloud à l’aide de la fonctionnalité d’acheminement de messages d’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1ab91-175">In this tutorial, you learned how to reliably dispatch device-to-cloud messages by using the message routing functionality of IoT Hub.</span></span>

<span data-ttu-id="1ab91-176">Le didacticiel [Envoi de messages cloud-à-appareil avec IoT Hub][lnk-c2d] vous montre comment envoyer des messages à vos appareils à partir de votre serveur principal de solution.</span><span class="sxs-lookup"><span data-stu-id="1ab91-176">The [How to send cloud-to-device messages with IoT Hub][lnk-c2d] shows you how to send messages to your devices from your solution back end.</span></span>

<span data-ttu-id="1ab91-177">Pour des exemples de solutions de bout en bout qui utilisent IoT Hub, voir [Azure IoT Suite][lnk-suite].</span><span class="sxs-lookup"><span data-stu-id="1ab91-177">To see examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite][lnk-suite].</span></span>

<span data-ttu-id="1ab91-178">Pour en savoir plus sur le développement de solutions avec IoT Hub, consultez le [Guide du développeur IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="1ab91-178">To learn more about developing solutions with IoT Hub, see the [IoT Hub developer guide].</span></span>

<span data-ttu-id="1ab91-179">Pour en savoir plus sur le routage des messages dans IoT Hub, consultez [Envoyer et recevoir des messages avec IoT Hub][lnk-devguide-messaging].</span><span class="sxs-lookup"><span data-stu-id="1ab91-179">To learn more about message routing in IoT Hub, see [Send and receive messages with IoT Hub][lnk-devguide-messaging].</span></span>

<!-- Images. -->
[50]: ./media/iot-hub-csharp-csharp-process-d2c/run1.png
[30]: ./media/iot-hub-csharp-csharp-process-d2c/click-endpoints.png
[31]: ./media/iot-hub-csharp-csharp-process-d2c/endpoint-creation.png
[32]: ./media/iot-hub-csharp-csharp-process-d2c/route-creation.png
[33]: ./media/iot-hub-csharp-csharp-process-d2c/fallback-route.png

<!-- Links -->
[Service Bus queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
<span data-ttu-id="1ab91-180">[Stockage Azure]: https://azure.microsoft.com/documentation/services/storage/</span><span class="sxs-lookup"><span data-stu-id="1ab91-180">[Azure Storage]: https://azure.microsoft.com/documentation/services/storage/</span></span>
<span data-ttu-id="1ab91-181">[Azure Service Bus]: https://azure.microsoft.com/documentation/services/service-bus/</span><span class="sxs-lookup"><span data-stu-id="1ab91-181">[Azure Service Bus]: https://azure.microsoft.com/documentation/services/service-bus/</span></span>
<span data-ttu-id="1ab91-182">[Guide du développeur IoT Hub]: iot-hub-devguide.md</span><span class="sxs-lookup"><span data-stu-id="1ab91-182">[IoT Hub developer guide]: iot-hub-devguide.md</span></span>
<span data-ttu-id="1ab91-183">[prise en main du IoT Hub]: iot-hub-csharp-csharp-getstarted.md</span><span class="sxs-lookup"><span data-stu-id="1ab91-183">[Get started with IoT Hub]: iot-hub-csharp-csharp-getstarted.md</span></span>
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
<span data-ttu-id="1ab91-184">[Centre de développement Azure IoT]: https://azure.microsoft.com/develop/iot</span><span class="sxs-lookup"><span data-stu-id="1ab91-184">[Azure IoT Developer Center]: https://azure.microsoft.com/develop/iot</span></span>
<span data-ttu-id="1ab91-185">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span><span class="sxs-lookup"><span data-stu-id="1ab91-185">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span></span>
[lnk-c2d]: iot-hub-csharp-csharp-process-d2c.md
[lnk-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
