---
title: "messages de périphérique dans le cloud Azure IoT Hub aaaProcess à l’aide d’itinéraires (.Net) | Documents Microsoft"
description: "Comment tooprocess les messages appareil-à-cloud IoT Hub à l’aide des règles de routage et les points de terminaison personnalisés toodispatch messages tooother les services principaux."
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
ms.openlocfilehash: c1dd5be04ca30c65af2be466ba6c8c1858333154
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="process-iot-hub-device-to-cloud-messages-using-routes-net"></a><span data-ttu-id="5a333-103">Traiter les messages appareil-à-cloud IoT Hub en utilisant les itinéraires (.NET)</span><span class="sxs-lookup"><span data-stu-id="5a333-103">Process IoT Hub device-to-cloud messages using routes (.NET)</span></span>

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

<span data-ttu-id="5a333-104">Ce didacticiel s’appuie sur hello [prise en main IoT Hub] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="5a333-104">This tutorial builds on hello [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="5a333-105">didacticiel de Hello :</span><span class="sxs-lookup"><span data-stu-id="5a333-105">hello tutorial:</span></span>

* <span data-ttu-id="5a333-106">Montre comment toouse règles de routage toodispatch les messages appareil-à-cloud dans un moyen simple et basée sur la configuration.</span><span class="sxs-lookup"><span data-stu-id="5a333-106">Shows you how toouse routing rules toodispatch device-to-cloud messages in an easy, configuration-based way.</span></span>
* <span data-ttu-id="5a333-107">Illustre comment les messages interactif tooisolate qui nécessitent une action immédiate à partir de la solution de hello back-end pour un traitement ultérieur.</span><span class="sxs-lookup"><span data-stu-id="5a333-107">Illustrates how tooisolate interactive messages that require immediate action from hello solution back end for further processing.</span></span> <span data-ttu-id="5a333-108">Par exemple, un appareil peut envoyer un message d’alerte qui déclenche l’insertion d’un ticket dans un système CRM.</span><span class="sxs-lookup"><span data-stu-id="5a333-108">For example, a device might send an alarm message that triggers inserting a ticket into a CRM system.</span></span> <span data-ttu-id="5a333-109">Par opposition, les messages de point de données tels que la télémétrie de température sont chargés dans un moteur d’analyse.</span><span class="sxs-lookup"><span data-stu-id="5a333-109">In contrast, data-point messages, such as temperature telemetry, feed into an analytics engine.</span></span>

<span data-ttu-id="5a333-110">À la fin de hello de ce didacticiel, vous exécutez trois applications de console .NET :</span><span class="sxs-lookup"><span data-stu-id="5a333-110">At hello end of this tutorial, you run three .NET console apps:</span></span>

* <span data-ttu-id="5a333-111">**SimulatedDevice**, une version modifiée de l’application hello créée Bonjour [prise en main IoT Hub] didacticiel envoie des messages de périphérique dans le cloud de point de données par seconde et toutes les 10 des messages interactif appareil-à-cloud secondes.</span><span class="sxs-lookup"><span data-stu-id="5a333-111">**SimulatedDevice**, a modified version of hello app created in hello [Get started with IoT Hub] tutorial sends data-point device-to-cloud messages every second, and interactive device-to-cloud messages every 10 seconds.</span></span>
* <span data-ttu-id="5a333-112">**ReadDeviceToCloudMessages** qu’affiche hello non critiques télémétrie envoyé par votre application.</span><span class="sxs-lookup"><span data-stu-id="5a333-112">**ReadDeviceToCloudMessages** that displays hello non-critical telemetry sent by your device app.</span></span>
* <span data-ttu-id="5a333-113">**ReadCriticalQueue** sort file d’attente de messages critiques de hello envoyées par votre application à partir d’une file d’attente Service Bus.</span><span class="sxs-lookup"><span data-stu-id="5a333-113">**ReadCriticalQueue** de-queues hello critical messages sent by your device app from a Service Bus queue.</span></span> <span data-ttu-id="5a333-114">Cette file d’attente est attaché toohello IoT hub.</span><span class="sxs-lookup"><span data-stu-id="5a333-114">This queue is attached toohello IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="5a333-115">IoT Hub offre la prise en charge de Kit de développement logiciel (SDK) de plusieurs plateformes d’appareils et de plusieurs langages (notamment C, Java et JavaScript).</span><span class="sxs-lookup"><span data-stu-id="5a333-115">IoT Hub has SDK support for many device platforms and languages, including C, Java, and JavaScript.</span></span> <span data-ttu-id="5a333-116">toolearn tooreplace hello appareil simulé dans ce didacticiel avec un périphérique physique, voir hello [centre de développement Azure IoT].</span><span class="sxs-lookup"><span data-stu-id="5a333-116">toolearn how tooreplace hello simulated device in this tutorial with a physical device, see hello [Azure IoT Developer Center].</span></span>

<span data-ttu-id="5a333-117">toocomplete ce didacticiel, vous devez hello suivant :</span><span class="sxs-lookup"><span data-stu-id="5a333-117">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="5a333-118">Visual Studio 2015 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="5a333-118">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="5a333-119">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="5a333-119">An active Azure account.</span></span> <br/><span data-ttu-id="5a333-120">Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit](https://azure.microsoft.com/free/) en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="5a333-120">If you don't have an account, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

<span data-ttu-id="5a333-121">Vous devez avoir une connaissance de base de [Stockage Azure] et d’[Azure Service Bus].</span><span class="sxs-lookup"><span data-stu-id="5a333-121">You should have some basic knowledge of [Azure Storage] and [Azure Service Bus].</span></span>

## <a name="send-interactive-messages"></a><span data-ttu-id="5a333-122">Envoyer des messages interactifs</span><span class="sxs-lookup"><span data-stu-id="5a333-122">Send interactive messages</span></span>

<span data-ttu-id="5a333-123">Modifier l’application d’appareil hello vous avez créé dans hello [prise en main IoT Hub] toooccasionally didacticiel envoyer des messages interactifs.</span><span class="sxs-lookup"><span data-stu-id="5a333-123">Modify hello device app you created in hello [Get started with IoT Hub] tutorial toooccasionally send interactive messages.</span></span>

<span data-ttu-id="5a333-124">Dans Visual Studio, Bonjour **SimulatedDevice** de projet, remplacez hello `SendDeviceToCloudMessagesAsync` méthode avec hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="5a333-124">In Visual Studio, in hello **SimulatedDevice** project, replace hello `SendDeviceToCloudMessagesAsync` method with hello following code:</span></span>

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

<span data-ttu-id="5a333-125">Cette méthode ajoute au hasard les propriété hello `"level": "critical"` toomessages envoyés par périphérique hello, qui simule un message qui requiert une action immédiate par hello solution back-end.</span><span class="sxs-lookup"><span data-stu-id="5a333-125">This method randomly adds hello property `"level": "critical"` toomessages sent by hello device, which simulates a message that requires immediate action by hello solution back-end.</span></span> <span data-ttu-id="5a333-126">application d’appareil Hello transmet ces informations dans les propriétés de message hello, au lieu de dans le corps du message hello, afin que IoT Hub peut acheminer la destination du message approprié hello message toohello.</span><span class="sxs-lookup"><span data-stu-id="5a333-126">hello device app passes this information in hello message properties, instead of in hello message body, so that IoT Hub can route hello message toohello proper message destination.</span></span>

> [!NOTE]
> <span data-ttu-id="5a333-127">Vous pouvez utiliser les messages de tooroute de propriétés de message pour différents scénarios, y compris à froid-chemin d’accès de traitement, en outre des exemple de chemin d’accès à chaud toohello ci-après.</span><span class="sxs-lookup"><span data-stu-id="5a333-127">You can use message properties tooroute messages for various scenarios including cold-path processing, in addition toohello hot-path example shown here.</span></span>

> [!NOTE]
> <span data-ttu-id="5a333-128">Pour des raisons de hello de simplicité, ce didacticiel n’implémente pas de toute stratégie de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="5a333-128">For hello sake of simplicity, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="5a333-129">Dans le code de production, vous devez implémenter une stratégie de nouvelle tentative comme une interruption exponentielle, comme indiqué dans l’article hello [gestion des pannes temporaires].</span><span class="sxs-lookup"><span data-stu-id="5a333-129">In production code, you should implement a retry policy such as exponential backoff, as suggested in hello MSDN article [Transient Fault Handling].</span></span>

## <a name="route-messages-tooa-queue-in-your-iot-hub"></a><span data-ttu-id="5a333-130">Itinéraire messages tooa file d’attente dans votre IoT hub</span><span class="sxs-lookup"><span data-stu-id="5a333-130">Route messages tooa queue in your IoT hub</span></span>

<span data-ttu-id="5a333-131">Dans cette section, vous allez :</span><span class="sxs-lookup"><span data-stu-id="5a333-131">In this section, you:</span></span>

* <span data-ttu-id="5a333-132">créer une file d’attente Service Bus ;</span><span class="sxs-lookup"><span data-stu-id="5a333-132">Create a Service Bus queue.</span></span>
* <span data-ttu-id="5a333-133">Connecter tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="5a333-133">Connect it tooyour IoT hub.</span></span>
* <span data-ttu-id="5a333-134">Configurez votre IoT hub toosend toohello file d’attente messages en fonction de la présence de hello d’une propriété de message de type hello.</span><span class="sxs-lookup"><span data-stu-id="5a333-134">Configure your IoT hub toosend messages toohello queue based on hello presence of a property on hello message.</span></span>

<span data-ttu-id="5a333-135">Pour plus d’informations sur la tooprocess des messages des files d’attente Service Bus, consultez [prise en main les files d’attente][Service Bus queue].</span><span class="sxs-lookup"><span data-stu-id="5a333-135">For more information about how tooprocess messages from Service Bus queues, see [Get started with queues][Service Bus queue].</span></span>

1. <span data-ttu-id="5a333-136">Créez une file d’attente Service Bus, comme décrit dans [Prise en main des files d’attente][Service Bus queue].</span><span class="sxs-lookup"><span data-stu-id="5a333-136">Create a Service Bus queue as described in [Get started with queues][Service Bus queue].</span></span> <span data-ttu-id="5a333-137">file d’attente Hello doit être Bonjour même abonnement et région que votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5a333-137">hello queue must be in hello same subscription and region as your IoT hub.</span></span> <span data-ttu-id="5a333-138">Prenez note du nom d’espace de noms et de file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="5a333-138">Make a note of hello namespace and queue name.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5a333-139">Les options **Sessions** ou **Détection des doublons** ne doivent pas être activées pour les files d’attente et rubriques Service Bus utilisées comme points de terminaison IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5a333-139">Service Bus queues and topics used as IoT Hub endpoints must not have **Sessions** or **Duplicate Detection** enabled.</span></span> <span data-ttu-id="5a333-140">Si une de ces options sont activée, le point de terminaison hello s’affiche en tant que **inaccessible** Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5a333-140">If either of those options are enabled, hello endpoint appears as **Unreachable** in hello Azure portal.</span></span>

2. <span data-ttu-id="5a333-141">Dans hello portail Azure, ouvrez votre IoT hub, cliquez sur **points de terminaison**.</span><span class="sxs-lookup"><span data-stu-id="5a333-141">In hello Azure portal, open your IoT hub and click **Endpoints**.</span></span>
    
    ![Points de terminaison dans IoT hub][30]

3. <span data-ttu-id="5a333-143">Bonjour **points de terminaison** panneau, cliquez sur **ajouter** à hello tooadd supérieur votre concentrateur de IoT tooyour file d’attente.</span><span class="sxs-lookup"><span data-stu-id="5a333-143">In hello **Endpoints** blade, click **Add** at hello top tooadd your queue tooyour IoT hub.</span></span> <span data-ttu-id="5a333-144">Point de terminaison nom hello **CriticalQueue** et utiliser hello déroulantes tooselect **file d’attente Service Bus**hello dans lequel réside votre file d’attente de l’espace de noms de Bus de Service et hello du nom de votre file d’attente.</span><span class="sxs-lookup"><span data-stu-id="5a333-144">Name hello endpoint **CriticalQueue** and use hello drop-downs tooselect **Service Bus queue**, hello Service Bus namespace in which your queue resides, and hello name of your queue.</span></span> <span data-ttu-id="5a333-145">Lorsque vous avez terminé, cliquez sur **enregistrer** bas hello.</span><span class="sxs-lookup"><span data-stu-id="5a333-145">When you are done, click **Save** at hello bottom.</span></span>
    
    ![Ajout d’un point de terminaison][31]
    
4. <span data-ttu-id="5a333-147">À présent, cliquez sur **Itinéraires** dans votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5a333-147">Now click **Routes** in your IoT Hub.</span></span> <span data-ttu-id="5a333-148">Cliquez sur **ajouter** haut hello hello panneau toocreate est une règle de routage qui achemine les messages toohello de file d’attente vous simplement ajoutée.</span><span class="sxs-lookup"><span data-stu-id="5a333-148">Click **Add** at hello top of hello blade toocreate a routing rule that routes messages toohello queue you just added.</span></span> <span data-ttu-id="5a333-149">Sélectionnez **DeviceTelemetry** comme source de hello de données.</span><span class="sxs-lookup"><span data-stu-id="5a333-149">Select **DeviceTelemetry** as hello source of data.</span></span> <span data-ttu-id="5a333-150">Entrez `level="critical"` en tant que condition de hello, choisissez la file d’attente hello vous venez d’ajouter en tant qu’un point de terminaison personnalisé en tant que point de terminaison de règle de routage de hello.</span><span class="sxs-lookup"><span data-stu-id="5a333-150">Enter `level="critical"` as hello condition, and choose hello queue you just added as a custom endpoint as hello routing rule endpoint.</span></span> <span data-ttu-id="5a333-151">Lorsque vous avez terminé, cliquez sur **enregistrer** bas hello.</span><span class="sxs-lookup"><span data-stu-id="5a333-151">When you are done, click **Save** at hello bottom.</span></span>
    
    ![Ajout d’un itinéraire][32]
    
    <span data-ttu-id="5a333-153">Assurez-vous que l’itinéraire de secours hello est défini trop**ON**.</span><span class="sxs-lookup"><span data-stu-id="5a333-153">Make sure hello fallback route is set too**ON**.</span></span> <span data-ttu-id="5a333-154">Cette valeur est la configuration par défaut de hello pour un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5a333-154">This value is hello default configuration for an IoT hub.</span></span>
    
    ![Itinéraire de secours][33]

## <a name="read-from-hello-queue-endpoint"></a><span data-ttu-id="5a333-156">Lire à partir du point de terminaison de file d’attente hello</span><span class="sxs-lookup"><span data-stu-id="5a333-156">Read from hello queue endpoint</span></span>

<span data-ttu-id="5a333-157">Dans cette section, vous lisez les messages de hello à partir du point de terminaison de file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="5a333-157">In this section, you read hello messages from hello queue endpoint.</span></span>

1. <span data-ttu-id="5a333-158">Dans Visual Studio, ajouter une solution d’actuel toohello de projet Visual c# bureau classique de Windows, à l’aide de hello **l’application Console (.NET Framework)** modèle de projet.</span><span class="sxs-lookup"><span data-stu-id="5a333-158">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution, by using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="5a333-159">Projet de hello nom **ReadCriticalQueue**.</span><span class="sxs-lookup"><span data-stu-id="5a333-159">Name hello project **ReadCriticalQueue**.</span></span>

2. <span data-ttu-id="5a333-160">Dans l’Explorateur de solutions, cliquez sur hello **ReadCriticalQueue** de projet, puis cliquez sur **gérer les Packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="5a333-160">In Solution Explorer, right-click hello **ReadCriticalQueue** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="5a333-161">Cette opération affiche hello **Gestionnaire de Package NuGet** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="5a333-161">This operation displays hello **NuGet Package Manager** window.</span></span>

3. <span data-ttu-id="5a333-162">Recherchez **WindowsAzure.ServiceBus**, cliquez sur **installer**et acceptez les conditions d’utilisation de hello.</span><span class="sxs-lookup"><span data-stu-id="5a333-162">Search for **WindowsAzure.ServiceBus**, click **Install**, and accept hello terms of use.</span></span> <span data-ttu-id="5a333-163">Cette opération télécharge, installe et ajoute une référence de toohello Azure Service Bus, avec toutes ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="5a333-163">This operation downloads, installs, and adds a reference toohello Azure Service Bus, with all its dependencies.</span></span>

4. <span data-ttu-id="5a333-164">Ajoutez hello suivant **à l’aide de** instructions haut hello hello **Program.cs** fichier :</span><span class="sxs-lookup"><span data-stu-id="5a333-164">Add hello following **using** statements at hello top of hello **Program.cs** file:</span></span>
   
    ```csharp
    using System.IO;
    using Microsoft.ServiceBus.Messaging;
    ```

5. <span data-ttu-id="5a333-165">Enfin, ajoutez hello suivant lignes toohello **Main** (méthode).</span><span class="sxs-lookup"><span data-stu-id="5a333-165">Finally, add hello following lines toohello **Main** method.</span></span> <span data-ttu-id="5a333-166">Remplacez par la chaîne de connexion hello **écouter** autorisations pour la file d’attente hello :</span><span class="sxs-lookup"><span data-stu-id="5a333-166">Substitute hello connection string with **Listen** permissions for hello queue:</span></span>
   
    ```csharp
    Console.WriteLine("Receive critical messages. Ctrl-C tooexit.\n");
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

## <a name="run-hello-applications"></a><span data-ttu-id="5a333-167">Exécuter des applications de hello</span><span class="sxs-lookup"><span data-stu-id="5a333-167">Run hello applications</span></span>
<span data-ttu-id="5a333-168">Vous êtes maintenant prêt toorun les applications hello.</span><span class="sxs-lookup"><span data-stu-id="5a333-168">Now you are ready toorun hello applications.</span></span>

1. <span data-ttu-id="5a333-169">Dans Visual Studio, dans l’Explorateur de solutions, cliquez avec le bouton droit sur votre solution, puis sélectionnez **Définir les projets de démarrage**.</span><span class="sxs-lookup"><span data-stu-id="5a333-169">In Visual Studio, in Solution Explorer, right-click your solution and select **Set StartUp Projects**.</span></span> <span data-ttu-id="5a333-170">Sélectionnez **plusieurs projets de démarrage**, puis sélectionnez **Démarrer** en tant qu’action hello pour hello **ReadDeviceToCloudMessages**, **SimulatedDevice**, et **ReadCriticalQueue** projets.</span><span class="sxs-lookup"><span data-stu-id="5a333-170">Select **Multiple startup projects**, then select **Start** as hello action for hello **ReadDeviceToCloudMessages**, **SimulatedDevice**, and **ReadCriticalQueue** projects.</span></span>
2. <span data-ttu-id="5a333-171">Appuyez sur **F5** toostart hello trois applications console.</span><span class="sxs-lookup"><span data-stu-id="5a333-171">Press **F5** toostart hello three console apps.</span></span> <span data-ttu-id="5a333-172">Hello **ReadDeviceToCloudMessages** application a uniquement les messages non critiques sont envoyés à partir de hello **SimulatedDevice** application et hello **ReadCriticalQueue** application a uniquement messages critiques.</span><span class="sxs-lookup"><span data-stu-id="5a333-172">hello **ReadDeviceToCloudMessages** app has only non-critical messages sent from hello **SimulatedDevice** application, and hello **ReadCriticalQueue** app has only critical messages.</span></span>
   
   ![Trois applications de console][50]

## <a name="next-steps"></a><span data-ttu-id="5a333-174">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5a333-174">Next steps</span></span>
<span data-ttu-id="5a333-175">Dans ce didacticiel, vous avez appris comment tooreliably distribuer des messages de l’appareil-à-cloud en utilisant la fonctionnalité de routage de messages hello du IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5a333-175">In this tutorial, you learned how tooreliably dispatch device-to-cloud messages by using hello message routing functionality of IoT Hub.</span></span>

<span data-ttu-id="5a333-176">Hello [comment les messages toosend cloud-à-appareil avec IoT Hub] [ lnk-c2d] vous montre comment les messages toosend tooyour des périphériques à partir de votre serveur principal de solution.</span><span class="sxs-lookup"><span data-stu-id="5a333-176">hello [How toosend cloud-to-device messages with IoT Hub][lnk-c2d] shows you how toosend messages tooyour devices from your solution back end.</span></span>

<span data-ttu-id="5a333-177">exemples de toosee des solutions de bout en bout complets qui utilisent l’IoT Hub, consultez [Azure IoT Suite][lnk-suite].</span><span class="sxs-lookup"><span data-stu-id="5a333-177">toosee examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite][lnk-suite].</span></span>

<span data-ttu-id="5a333-178">toolearn savoir plus sur le développement de solutions avec IoT Hub, consultez hello [guide du développeur IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="5a333-178">toolearn more about developing solutions with IoT Hub, see hello [IoT Hub developer guide].</span></span>

<span data-ttu-id="5a333-179">toolearn en savoir plus sur le routage des messages dans IoT Hub, consultez [envoyer et recevoir des messages avec IoT Hub][lnk-devguide-messaging].</span><span class="sxs-lookup"><span data-stu-id="5a333-179">toolearn more about message routing in IoT Hub, see [Send and receive messages with IoT Hub][lnk-devguide-messaging].</span></span>

<!-- Images. -->
[50]: ./media/iot-hub-csharp-csharp-process-d2c/run1.png
[30]: ./media/iot-hub-csharp-csharp-process-d2c/click-endpoints.png
[31]: ./media/iot-hub-csharp-csharp-process-d2c/endpoint-creation.png
[32]: ./media/iot-hub-csharp-csharp-process-d2c/route-creation.png
[33]: ./media/iot-hub-csharp-csharp-process-d2c/fallback-route.png

<!-- Links -->
[Service Bus queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[Stockage Azure]: https://azure.microsoft.com/documentation/services/storage/
[Azure Service Bus]: https://azure.microsoft.com/documentation/services/service-bus/
[guide du développeur IoT Hub]: iot-hub-devguide.md
[prise en main IoT Hub]: iot-hub-csharp-csharp-getstarted.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
[centre de développement Azure IoT]: https://azure.microsoft.com/develop/iot
[gestion des pannes temporaires]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-c2d]: iot-hub-csharp-csharp-process-d2c.md
[lnk-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
