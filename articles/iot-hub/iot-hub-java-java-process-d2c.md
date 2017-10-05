---
title: "Traiter les messages appareil-à-cloud d’Azure IoT Hub (Java) | Microsoft Docs"
description: "Comment traiter des messages appareil-à-cloud IoT Hub en utilisant les règles de routage et les points de terminaison personnalisés pour distribuer les messages vers d’autres services principaux."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: bd9af5f9-a740-4780-a2a6-8c0e2752cf48
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: dobett
ms.openlocfilehash: d1aca8f39e305105d4ec9f63fbe7bee95487e294
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="process-iot-hub-device-to-cloud-messages-java"></a><span data-ttu-id="62772-103">Traitement des messages appareil-à-cloud IoT Hub (Java)</span><span class="sxs-lookup"><span data-stu-id="62772-103">Process IoT Hub device-to-cloud messages (Java)</span></span>

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

<span data-ttu-id="62772-104">Azure IoT Hub est un service entièrement géré qui permet des communications bidirectionnelles fiables et sécurisées entre des millions d’appareils et un serveur principal de solution.</span><span class="sxs-lookup"><span data-stu-id="62772-104">Azure IoT Hub is a fully managed service that enables reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="62772-105">Les autres didacticiels ([Prise en main d’IoT Hub] et [Envoyer des messages du cloud vers des appareils avec IoT Hub][lnk-c2d]) vous expliquent comment utiliser la fonctionnalité de base de la messagerie « appareil vers cloud » et « cloud vers appareil » offerte par IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="62772-105">Other tutorials ([Get started with IoT Hub] and [Send cloud-to-device messages with IoT Hub][lnk-c2d]) show you how to use the basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span>

<span data-ttu-id="62772-106">Ce didacticiel s’appuie sur le code indiqué dans le didacticiel [Prise en main d’IoT Hub] et explique comment utiliser une méthode de configuration d’itinéraire pour traiter des messages appareil-à-cloud de façon évolutive.</span><span class="sxs-lookup"><span data-stu-id="62772-106">This tutorial builds on the code shown in the [Get started with IoT Hub] tutorial, and shows you how to use message routing to process device-to-cloud messages in a scalable way.</span></span> <span data-ttu-id="62772-107">Ce didacticiel vous indique comment traiter les messages qui nécessitent une action immédiate du serveur principal de la solution.</span><span class="sxs-lookup"><span data-stu-id="62772-107">The tutorial illustrates how to process messages that require immediate action from the solution back end.</span></span> <span data-ttu-id="62772-108">Par exemple, un appareil peut envoyer un message d’alerte qui déclenche l’insertion d’un ticket dans un système CRM.</span><span class="sxs-lookup"><span data-stu-id="62772-108">For example, a device might send an alarm message that triggers inserting a ticket into a CRM system.</span></span> <span data-ttu-id="62772-109">Par opposition, les messages de point de données sont simplement chargés dans un moteur d’analyse.</span><span class="sxs-lookup"><span data-stu-id="62772-109">By contrast, data-point messages simply feed into an analytics engine.</span></span> <span data-ttu-id="62772-110">Par exemple, les données de télémétrie de température d’un appareil qui doivent être enregistrées pour analyse ultérieure constituent un message de point de données.</span><span class="sxs-lookup"><span data-stu-id="62772-110">For example, temperature telemetry from a device that is to be stored for later analysis is a data-point message.</span></span>

<span data-ttu-id="62772-111">À la fin de ce didacticiel, vous exécutez trois applications de console Java :</span><span class="sxs-lookup"><span data-stu-id="62772-111">At the end of this tutorial, you run three Java console apps:</span></span>

* <span data-ttu-id="62772-112">**simulated-device**, une version modifiée de l’application créée dans le didacticiel [Prise en main d’IoT Hub] qui envoie des messages de point de données des appareils vers le cloud chaque seconde et des messages interactifs des appareils vers le cloud toutes les 10 secondes.</span><span class="sxs-lookup"><span data-stu-id="62772-112">**simulated-device**, a modified version of the app created in the [Get started with IoT Hub] tutorial, sends data-point device-to-cloud messages every second, and interactive device-to-cloud messages every 10 seconds.</span></span> <span data-ttu-id="62772-113">Cette application utilise le protocole AMQPS pour communiquer avec IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="62772-113">This app uses the AMQP protocol to communicate with IoT Hub.</span></span>
* <span data-ttu-id="62772-114">**read-d2c-messages** affiche les données de télémétrie envoyées par votre application pour appareils.</span><span class="sxs-lookup"><span data-stu-id="62772-114">**read-d2c-messages** displays the telemetry sent by your device app.</span></span>
* <span data-ttu-id="62772-115">**read-critical-queue** enlève les messages critiques de la file d’attente Service Bus attachée au hub IoT.</span><span class="sxs-lookup"><span data-stu-id="62772-115">**read-critical-queue** de-queues the critical messages from the Service Bus queue attached to the IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="62772-116">IoT Hub offre la prise en charge de Kit de développement logiciel (SDK) de plusieurs plateformes d’appareils et de plusieurs langages (notamment C, Java et JavaScript).</span><span class="sxs-lookup"><span data-stu-id="62772-116">IoT Hub has SDK support for many device platforms and languages, including C, Java, and JavaScript.</span></span> <span data-ttu-id="62772-117">Pour obtenir des instructions expliquant comment remplacer l’appareil de ce didacticiel par un appareil physique et comment connecter vos appareils à un hub IoT, consultez le [Centre de développement Azure IoT].</span><span class="sxs-lookup"><span data-stu-id="62772-117">For instructions on how to replace the device in this tutorial with a physical device, and how to connect devices to an IoT Hub, see the [Azure IoT Developer Center].</span></span>

<span data-ttu-id="62772-118">Pour réaliser ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="62772-118">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="62772-119">Une version d’utilisation complète du didacticiel [Prise en main d’IoT Hub] .</span><span class="sxs-lookup"><span data-stu-id="62772-119">A complete working version of the [Get started with IoT Hub] tutorial.</span></span>
* <span data-ttu-id="62772-120">La version la plus récente de [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="62772-120">The latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="62772-121">Maven 3</span><span class="sxs-lookup"><span data-stu-id="62772-121">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="62772-122">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="62772-122">An active Azure account.</span></span> <span data-ttu-id="62772-123">(Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit] [lnk-free-trial] en quelques minutes.)</span><span class="sxs-lookup"><span data-stu-id="62772-123">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="62772-124">Vous devez avoir une connaissance de base de [Stockage Azure] et d’[Azure Service Bus].</span><span class="sxs-lookup"><span data-stu-id="62772-124">You should have some basic knowledge of [Azure Storage] and [Azure Service Bus].</span></span>

## <a name="send-interactive-messages-from-a-device-app"></a><span data-ttu-id="62772-125">Envoyer des messages interactifs à partir d’une application pour appareils</span><span class="sxs-lookup"><span data-stu-id="62772-125">Send interactive messages from a device app</span></span>
<span data-ttu-id="62772-126">Dans cette section, vous allez modifier l’application pour appareils que vous avez créée dans le didacticiel [Prise en main d’IoT Hub] de façon à envoyer occasionnellement des messages nécessitant un traitement immédiat.</span><span class="sxs-lookup"><span data-stu-id="62772-126">In this section, you modify the device app you created in the [Get started with IoT Hub] tutorial to occasionally send messages that require immediate processing.</span></span>

1. <span data-ttu-id="62772-127">À l’aide d’un éditeur de texte, ouvrez le fichier simulated-device\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="62772-127">Use a text editor to open the simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span> <span data-ttu-id="62772-128">Ce fichier contient le code pour l’application **simulated-device** que vous avez créée dans le didacticiel [Prise en main d’IoT Hub] .</span><span class="sxs-lookup"><span data-stu-id="62772-128">This file contains the code for the **simulated-device** app you created in the [Get started with IoT Hub] tutorial.</span></span>

2. <span data-ttu-id="62772-129">Remplacez la classe **MessageSender** par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="62772-129">Replace the **MessageSender** class with the following code:</span></span>

    ```java
    private static class MessageSender implements Runnable {

        public void run()  {
            try {
                double minTemperature = 20;
                double minHumidity = 60;
                Random rand = new Random();

                while (true) {
                    String msgStr;
                    Message msg;
                    if (new Random().nextDouble() > 0.7) {
                        msgStr = "This is a critical message.";
                        msg = new Message(msgStr);
                        msg.setProperty("level", "critical");
                    } else {
                        double currentTemperature = minTemperature + rand.nextDouble() * 15;
                        double currentHumidity = minHumidity + rand.nextDouble() * 20; 
                        TelemetryDataPoint telemetryDataPoint = new TelemetryDataPoint();
                        telemetryDataPoint.deviceId = deviceId;
                        telemetryDataPoint.temperature = currentTemperature;
                        telemetryDataPoint.humidity = currentHumidity;

                        msgStr = telemetryDataPoint.serialize();
                        msg = new Message(msgStr);
                    }
                    
                    System.out.println("Sending: " + msgStr);

                    Object lockobj = new Object();
                    EventCallback callback = new EventCallback();
                    client.sendEventAsync(msg, callback, lockobj);

                    synchronized (lockobj) {
                        lockobj.wait();
                    }
                    Thread.sleep(1000);
                }
            } catch (InterruptedException e) {
                System.out.println("Finished.");
            }
        }
    }
    ```
   
    <span data-ttu-id="62772-130">Cela ajoute au hasard la propriété `"level": "critical"` aux messages envoyés par l’appareil, ce qui simule un message qui requiert une action immédiate du serveur principal de l’application.</span><span class="sxs-lookup"><span data-stu-id="62772-130">This method randomly adds the property `"level": "critical"` to messages sent by the device, which simulates a message that requires immediate action by the application back-end.</span></span> <span data-ttu-id="62772-131">L’application transmet ces informations dans les propriétés du message, plutôt que dans le corps du message, afin que IoT Hub puisse acheminer le message vers la destination adéquate.</span><span class="sxs-lookup"><span data-stu-id="62772-131">The application passes this information in the message properties, instead of in the message body, so that IoT Hub can route the message to the proper message destination.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="62772-132">Vous pouvez utiliser les propriétés de message pour acheminer les messages pour de nombreux scénarios, tels que le traitement de chemin d’accès à froid, en plus de l’exemple de chemin d’accès à chaud présenté ici.</span><span class="sxs-lookup"><span data-stu-id="62772-132">You can use message properties to route messages for various scenarios including cold-path processing, in addition to the hot path example shown here.</span></span>

2. <span data-ttu-id="62772-133">Enregistrez et fermez le fichier simulated-device\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="62772-133">Save and close the simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

    > [!NOTE]
    > <span data-ttu-id="62772-134">Par souci de simplicité, ce didacticiel n’implémente aucune stratégie de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="62772-134">For the sake of simplicity, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="62772-135">Dans le code de production, vous devez mettre en œuvre des stratégies de nouvelle tentative (par exemple, une interruption exponentielle), comme indiqué dans l’article MSDN [Transient Fault Handling](Gestion des erreurs temporaires).</span><span class="sxs-lookup"><span data-stu-id="62772-135">In production code, you should implement a retry policy such as exponential backoff, as suggested in the MSDN article [Transient Fault Handling].</span></span>

3. <span data-ttu-id="62772-136">Pour générer l’application **simulated-device** à l’aide de Maven, exécutez la commande suivante à l’invite de commandes dans le dossier simulated-device :</span><span class="sxs-lookup"><span data-stu-id="62772-136">To build the **simulated-device** app using Maven, execute the following command at the command prompt in the simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="add-a-queue-to-your-iot-hub-and-route-messages-to-it"></a><span data-ttu-id="62772-137">Ajouter une file d’attente à votre IoT Hub et y acheminer des messages</span><span class="sxs-lookup"><span data-stu-id="62772-137">Add a queue to your IoT hub and route messages to it</span></span>

<span data-ttu-id="62772-138">Dans cette section, vous allez créer une file d’attente Service Bus, la connecter à votre IoT Hub et configurer votre IoT hub pour envoyer des messages à la file d’attente en fonction de la présence d’une propriété sur le message.</span><span class="sxs-lookup"><span data-stu-id="62772-138">In this section, you create a Service Bus queue, connect it to your IoT hub, and configure your IoT hub to send messages to the queue based on the presence of a property on the message.</span></span> <span data-ttu-id="62772-139">Pour plus d’informations sur la façon de traiter les messages des files d’attente Service Bus, consultez [Prise en main des files d’attente][lnk-sb-queues-java].</span><span class="sxs-lookup"><span data-stu-id="62772-139">For more information about how to process messages from Service Bus queues, see [Get started with queues][lnk-sb-queues-java].</span></span>

1. <span data-ttu-id="62772-140">Créez une file d’attente Service Bus, comme décrit dans [Prise en main des files d’attente][lnk-sb-queues-java].</span><span class="sxs-lookup"><span data-stu-id="62772-140">Create a Service Bus queue as described in [Get started with queues][lnk-sb-queues-java].</span></span> <span data-ttu-id="62772-141">Prenez note de l’espace de noms et de la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="62772-141">Make a note of the namespace and queue name.</span></span>

2. <span data-ttu-id="62772-142">Dans le portail Azure, ouvrez votre IoT Hub, puis cliquez sur **Points de terminaison**.</span><span class="sxs-lookup"><span data-stu-id="62772-142">In the Azure portal, open your IoT hub and click **Endpoints**.</span></span>

    ![Points de terminaison dans IoT hub][30]

3. <span data-ttu-id="62772-144">En haut du panneau **Points de terminaison**, cliquez sur **Ajouter** pour ajouter votre file d’attente à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="62772-144">In the **Endpoints** blade, click **Add** at the top to add your queue to your IoT hub.</span></span> <span data-ttu-id="62772-145">Nommez le point de terminaison **CriticalQueue**, puis utilisez les listes déroulantes pour sélectionner **File d’attente Service Bus**, l’espace de noms Service Bus dans lequel réside votre file d’attente, ainsi que le nom de votre file d’attente.</span><span class="sxs-lookup"><span data-stu-id="62772-145">Name the endpoint **CriticalQueue** and use the drop-downs to select **Service Bus queue**, the Service Bus namespace in which your queue resides, and the name of your queue.</span></span> <span data-ttu-id="62772-146">Lorsque vous avez terminé, cliquez sur **Enregistrer** en bas.</span><span class="sxs-lookup"><span data-stu-id="62772-146">When you are done, click **Save** at the bottom.</span></span>

    ![Ajout d’un point de terminaison][31]

4. <span data-ttu-id="62772-148">À présent, cliquez sur **Itinéraires** dans votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="62772-148">Now click **Routes** in your IoT Hub.</span></span> <span data-ttu-id="62772-149">En haut du panneau, cliquez sur **Ajouter** afin de créer une règle qui achemine les messages vers la file d’attente que vous venez d’ajouter.</span><span class="sxs-lookup"><span data-stu-id="62772-149">Click **Add** at the top of the blade to create a routing rule that routes messages to the queue you just added.</span></span> <span data-ttu-id="62772-150">Sélectionnez **DeviceTelemetry** comme source de données.</span><span class="sxs-lookup"><span data-stu-id="62772-150">Select **DeviceTelemetry** as the source of data.</span></span> <span data-ttu-id="62772-151">Saisissez `level="critical"` comme condition, puis sélectionnez la file d’attente que vous venez d’ajouter comme point de terminaison personnalisé en tant que point de terminaison de la règle de routage.</span><span class="sxs-lookup"><span data-stu-id="62772-151">Enter `level="critical"` as the condition, and choose the queue you just added as a custom endpoint as the routing rule endpoint.</span></span> <span data-ttu-id="62772-152">Lorsque vous avez terminé, cliquez sur **Enregistrer** en bas.</span><span class="sxs-lookup"><span data-stu-id="62772-152">When you are done, click **Save** at the bottom.</span></span>

    ![Ajout d’un itinéraire][32]

    <span data-ttu-id="62772-154">Assurez-vous que l’itinéraire de secours est défini sur **ACTIVÉ**.</span><span class="sxs-lookup"><span data-stu-id="62772-154">Make sure the fallback route is set to **ON**.</span></span> <span data-ttu-id="62772-155">Ce paramètre correspond à la configuration par défaut d’un IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="62772-155">This setting is the default configuration of an IoT hub.</span></span>

    ![Itinéraire de secours][33]

## <a name="optional-read-from-the-queue-endpoint"></a><span data-ttu-id="62772-157">(Facultatif) Lecture à partir du point de terminaison de la file d’attente</span><span class="sxs-lookup"><span data-stu-id="62772-157">(Optional) Read from the queue endpoint</span></span>

<span data-ttu-id="62772-158">Vous pouvez éventuellement lire les messages à partir du point de terminaison de la file d’attente en suivant les instructions fournies dans [Prise en main des files d’attente][lnk-sb-queues-java].</span><span class="sxs-lookup"><span data-stu-id="62772-158">You can optionally read the messages from the queue endpoint by following the instructions in [Get started with queues][lnk-sb-queues-java].</span></span> <span data-ttu-id="62772-159">Nommez l’application **read-critical-queue**.</span><span class="sxs-lookup"><span data-stu-id="62772-159">Name the app **read-critical-queue**.</span></span>

## <a name="run-the-applications"></a><span data-ttu-id="62772-160">Exécution des applications</span><span class="sxs-lookup"><span data-stu-id="62772-160">Run the applications</span></span>

<span data-ttu-id="62772-161">Vous êtes maintenant prêt à exécuter les trois applications.</span><span class="sxs-lookup"><span data-stu-id="62772-161">Now you are ready to run the three applications.</span></span>

1. <span data-ttu-id="62772-162">Pour exécuter l’application **read-d2c-messages**, dans l’invite de commandes ou l’interpréteur de commandes, accédez au dossier read-d2c et exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="62772-162">To run the **read-d2c-messages** application, in a command prompt or shell navigate to the read-d2c folder and execute the following command:</span></span>

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```

   ![Exécution de read-d2c-messages][readd2c]

2. <span data-ttu-id="62772-164">Pour exécuter l’application **read-critical-queue**, dans l’invite de commandes ou l’interpréteur de commandes, accédez au dossier read-critical-queue et exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="62772-164">To run the **read-critical-queue** application, in a command prompt or shell navigate to the read-critical-queue folder and execute the following command:</span></span>

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![Exécution de read-critical-messages][readqueue]

3. <span data-ttu-id="62772-166">Pour exécuter l’application **simulated-device**, dans l’invite de commandes ou l’interpréteur de commandes, accédez au dossier simulated-device, puis exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="62772-166">To run the **simulated-device** app, in a command prompt or shell navigate to the simulated-device folder and execute the following command:</span></span>

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![Exécuter simulated-device][simulateddevice]

## <a name="next-steps"></a><span data-ttu-id="62772-168">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="62772-168">Next steps</span></span>

<span data-ttu-id="62772-169">Dans ce didacticiel, vous avez appris à répartir de façon fiable des messages appareil-à-cloud à l’aide de la fonctionnalité d’acheminement de messages d’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="62772-169">In this tutorial, you learned how to reliably dispatch device-to-cloud messages by using the message routing functionality of IoT Hub.</span></span>

<span data-ttu-id="62772-170">Le didacticiel [Envoi de messages cloud-à-appareil avec IoT Hub][lnk-c2d] vous montre comment envoyer des messages à vos appareils à partir de votre serveur principal de solution.</span><span class="sxs-lookup"><span data-stu-id="62772-170">The [How to send cloud-to-device messages with IoT Hub][lnk-c2d] shows you how to send messages to your devices from your solution back end.</span></span>

<span data-ttu-id="62772-171">Pour des exemples de solutions de bout en bout qui utilisent IoT Hub, voir [Azure IoT Suite][lnk-suite].</span><span class="sxs-lookup"><span data-stu-id="62772-171">To see examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite][lnk-suite].</span></span>

<span data-ttu-id="62772-172">Pour en savoir plus sur le développement de solutions avec IoT Hub, consultez le [Guide du développeur IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="62772-172">To learn more about developing solutions with IoT Hub, see the [IoT Hub developer guide].</span></span>

<span data-ttu-id="62772-173">Pour en savoir plus sur le routage des messages dans IoT Hub, consultez [Envoyer et recevoir des messages avec IoT Hub][lnk-devguide-messaging].</span><span class="sxs-lookup"><span data-stu-id="62772-173">To learn more about message routing in IoT Hub, see [Send and receive messages with IoT Hub][lnk-devguide-messaging].</span></span>

<!-- Images. -->
<!-- TODO: UPDATE PICTURES -->
[simulateddevice]: ./media/iot-hub-java-java-process-d2c/runsimulateddevice.png
[readd2c]: ./media/iot-hub-java-java-process-d2c/runprocessinteractive.png
[readqueue]: ./media/iot-hub-java-java-process-d2c/runprocessd2c.png

[30]: ./media/iot-hub-java-java-process-d2c/click-endpoints.png
[31]: ./media/iot-hub-java-java-process-d2c/endpoint-creation.png
[32]: ./media/iot-hub-java-java-process-d2c/route-creation.png
[33]: ./media/iot-hub-java-java-process-d2c/fallback-route.png

<!-- Links -->

[lnk-sb-queues-java]: ../service-bus-messaging/service-bus-java-how-to-use-queues.md

<span data-ttu-id="62772-174">[Stockage Azure]: https://azure.microsoft.com/documentation/services/storage/</span><span class="sxs-lookup"><span data-stu-id="62772-174">[Azure Storage]: https://azure.microsoft.com/documentation/services/storage/</span></span>
<span data-ttu-id="62772-175">[Azure Service Bus]: https://azure.microsoft.com/documentation/services/service-bus/</span><span class="sxs-lookup"><span data-stu-id="62772-175">[Azure Service Bus]: https://azure.microsoft.com/documentation/services/service-bus/</span></span>

<span data-ttu-id="62772-176">[Guide du développeur IoT Hub]: iot-hub-devguide.md</span><span class="sxs-lookup"><span data-stu-id="62772-176">[IoT Hub developer guide]: iot-hub-devguide.md</span></span>
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
<span data-ttu-id="62772-177">[Prise en main d’IoT Hub]: iot-hub-java-java-getstarted.md</span><span class="sxs-lookup"><span data-stu-id="62772-177">[Get started with IoT Hub]: iot-hub-java-java-getstarted.md</span></span>
<span data-ttu-id="62772-178">[Centre de développement Azure IoT]: https://azure.microsoft.com/develop/iot</span><span class="sxs-lookup"><span data-stu-id="62772-178">[Azure IoT Developer Center]: https://azure.microsoft.com/develop/iot</span></span>
<span data-ttu-id="62772-179">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh675232.aspx</span><span class="sxs-lookup"><span data-stu-id="62772-179">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh675232.aspx</span></span>

<!-- Links -->
<span data-ttu-id="62772-180">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span><span class="sxs-lookup"><span data-stu-id="62772-180">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span></span>

[lnk-c2d]: iot-hub-java-java-c2d.md
[lnk-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
