---
title: "aaaProcess les messages appareil-à-cloud Azure IoT Hub (Java) | Documents Microsoft"
description: "Comment tooprocess les messages appareil-à-cloud IoT Hub à l’aide des règles de routage et les points de terminaison personnalisés toodispatch messages tooother les services principaux."
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
ms.openlocfilehash: 084e84e721ca4297c4d7d6cb06a43b0bed9bce85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="process-iot-hub-device-to-cloud-messages-java"></a><span data-ttu-id="79139-103">Traitement des messages appareil-à-cloud IoT Hub (Java)</span><span class="sxs-lookup"><span data-stu-id="79139-103">Process IoT Hub device-to-cloud messages (Java)</span></span>

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

<span data-ttu-id="79139-104">Azure IoT Hub est un service entièrement géré qui permet des communications bidirectionnelles fiables et sécurisées entre des millions d’appareils et un serveur principal de solution.</span><span class="sxs-lookup"><span data-stu-id="79139-104">Azure IoT Hub is a fully managed service that enables reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="79139-105">Autres didacticiels ([prise en main IoT Hub] et [envoyer des messages cloud-à-appareil avec IoT Hub][lnk-c2d]) vous indiquent comment toouse hello base appareil-à-cloud et cloud-à-appareil fonctionnalités de messagerie de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="79139-105">Other tutorials ([Get started with IoT Hub] and [Send cloud-to-device messages with IoT Hub][lnk-c2d]) show you how toouse hello basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span>

<span data-ttu-id="79139-106">Ce didacticiel s’appuie sur le code hello illustré hello [prise en main IoT Hub] (didacticiel) et vous montre comment toouse message routage des messages appareil-à-cloud tooprocess de façon évolutive.</span><span class="sxs-lookup"><span data-stu-id="79139-106">This tutorial builds on hello code shown in hello [Get started with IoT Hub] tutorial, and shows you how toouse message routing tooprocess device-to-cloud messages in a scalable way.</span></span> <span data-ttu-id="79139-107">didacticiel de Hello illustre la façon dont les messages tooprocess qui nécessitent une action immédiate à partir de la solution de hello back-end.</span><span class="sxs-lookup"><span data-stu-id="79139-107">hello tutorial illustrates how tooprocess messages that require immediate action from hello solution back end.</span></span> <span data-ttu-id="79139-108">Par exemple, un appareil peut envoyer un message d’alerte qui déclenche l’insertion d’un ticket dans un système CRM.</span><span class="sxs-lookup"><span data-stu-id="79139-108">For example, a device might send an alarm message that triggers inserting a ticket into a CRM system.</span></span> <span data-ttu-id="79139-109">Par opposition, les messages de point de données sont simplement chargés dans un moteur d’analyse.</span><span class="sxs-lookup"><span data-stu-id="79139-109">By contrast, data-point messages simply feed into an analytics engine.</span></span> <span data-ttu-id="79139-110">Par exemple, la télémétrie de température d’un appareil qui est toobe stockée pour une analyse ultérieure est un message de point de données.</span><span class="sxs-lookup"><span data-stu-id="79139-110">For example, temperature telemetry from a device that is toobe stored for later analysis is a data-point message.</span></span>

<span data-ttu-id="79139-111">À la fin de hello de ce didacticiel, vous exécutez trois applications de console Java :</span><span class="sxs-lookup"><span data-stu-id="79139-111">At hello end of this tutorial, you run three Java console apps:</span></span>

* <span data-ttu-id="79139-112">**APPAREIL simulé**, une version modifiée de l’application hello créée Bonjour [prise en main IoT Hub] didacticiel, envoie des messages de périphérique dans le cloud de point de données par seconde et interactif appareil-à-cloud messages toutes les 10 secondes.</span><span class="sxs-lookup"><span data-stu-id="79139-112">**simulated-device**, a modified version of hello app created in hello [Get started with IoT Hub] tutorial, sends data-point device-to-cloud messages every second, and interactive device-to-cloud messages every 10 seconds.</span></span> <span data-ttu-id="79139-113">Cette application utilise toocommunicate de protocole AMQP hello avec IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="79139-113">This app uses hello AMQP protocol toocommunicate with IoT Hub.</span></span>
* <span data-ttu-id="79139-114">**en lecture-d2c-messages** affiche télémétrie hello envoyée par votre application.</span><span class="sxs-lookup"><span data-stu-id="79139-114">**read-d2c-messages** displays hello telemetry sent by your device app.</span></span>
* <span data-ttu-id="79139-115">**en lecture critique-file d’attente** sort file d’attente de messages critiques hello de hello Bus de Service file d’attente attaché toohello IoT hub.</span><span class="sxs-lookup"><span data-stu-id="79139-115">**read-critical-queue** de-queues hello critical messages from hello Service Bus queue attached toohello IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="79139-116">IoT Hub offre la prise en charge de Kit de développement logiciel (SDK) de plusieurs plateformes d’appareils et de plusieurs langages (notamment C, Java et JavaScript).</span><span class="sxs-lookup"><span data-stu-id="79139-116">IoT Hub has SDK support for many device platforms and languages, including C, Java, and JavaScript.</span></span> <span data-ttu-id="79139-117">Pour plus d’informations sur comment tooreplace hello périphérique dans ce didacticiel avec un périphérique physique, et comment tooconnect périphériques tooan IoT Hub, consultez hello [centre de développement Azure IoT].</span><span class="sxs-lookup"><span data-stu-id="79139-117">For instructions on how tooreplace hello device in this tutorial with a physical device, and how tooconnect devices tooan IoT Hub, see hello [Azure IoT Developer Center].</span></span>

<span data-ttu-id="79139-118">toocomplete ce didacticiel, vous devez hello suivant :</span><span class="sxs-lookup"><span data-stu-id="79139-118">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="79139-119">Une version complète de travail de hello [prise en main IoT Hub] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="79139-119">A complete working version of hello [Get started with IoT Hub] tutorial.</span></span>
* <span data-ttu-id="79139-120">Hello dernières [8 de Kit de développement Java SE](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="79139-120">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="79139-121">Maven 3</span><span class="sxs-lookup"><span data-stu-id="79139-121">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="79139-122">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="79139-122">An active Azure account.</span></span> <span data-ttu-id="79139-123">(Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit] [lnk-free-trial] en quelques minutes.)</span><span class="sxs-lookup"><span data-stu-id="79139-123">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="79139-124">Vous devez avoir une connaissance de base de [Stockage Azure] et d’[Azure Service Bus].</span><span class="sxs-lookup"><span data-stu-id="79139-124">You should have some basic knowledge of [Azure Storage] and [Azure Service Bus].</span></span>

## <a name="send-interactive-messages-from-a-device-app"></a><span data-ttu-id="79139-125">Envoyer des messages interactifs à partir d’une application pour appareils</span><span class="sxs-lookup"><span data-stu-id="79139-125">Send interactive messages from a device app</span></span>
<span data-ttu-id="79139-126">Dans cette section, vous modifiez l’application d’appareil hello vous avez créé dans hello [prise en main IoT Hub] toooccasionally didacticiel envoyer des messages qui nécessitent un traitement immédiat.</span><span class="sxs-lookup"><span data-stu-id="79139-126">In this section, you modify hello device app you created in hello [Get started with IoT Hub] tutorial toooccasionally send messages that require immediate processing.</span></span>

1. <span data-ttu-id="79139-127">Utiliser un fichier de texte éditeur tooopen hello simulated-device\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="79139-127">Use a text editor tooopen hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span> <span data-ttu-id="79139-128">Ce fichier contient le code hello pour hello **appareil simulé** application que vous avez créé dans hello [prise en main IoT Hub] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="79139-128">This file contains hello code for hello **simulated-device** app you created in hello [Get started with IoT Hub] tutorial.</span></span>

2. <span data-ttu-id="79139-129">Remplacez hello **MessageSender** classe avec hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="79139-129">Replace hello **MessageSender** class with hello following code:</span></span>

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
   
    <span data-ttu-id="79139-130">Cette méthode ajoute au hasard les propriété hello `"level": "critical"` toomessages envoyés par périphérique hello, qui simule un message qui requiert une action immédiate par hello application back-end.</span><span class="sxs-lookup"><span data-stu-id="79139-130">This method randomly adds hello property `"level": "critical"` toomessages sent by hello device, which simulates a message that requires immediate action by hello application back-end.</span></span> <span data-ttu-id="79139-131">application Hello transmet ces informations dans les propriétés de message hello, au lieu de dans le corps du message hello, afin que IoT Hub peut acheminer la destination du message approprié hello message toohello.</span><span class="sxs-lookup"><span data-stu-id="79139-131">hello application passes this information in hello message properties, instead of in hello message body, so that IoT Hub can route hello message toohello proper message destination.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="79139-132">Vous pouvez utiliser des messages de tooroute de propriétés pour différents scénarios, y compris à froid-chemin d’accès de traitement, en outre des exemple de chemin réactif toohello ci-après.</span><span class="sxs-lookup"><span data-stu-id="79139-132">You can use message properties tooroute messages for various scenarios including cold-path processing, in addition toohello hot path example shown here.</span></span>

2. <span data-ttu-id="79139-133">Enregistrez et fermez le fichier de simulated-device\src\main\java\com\mycompany\app\App.java hello.</span><span class="sxs-lookup"><span data-stu-id="79139-133">Save and close hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

    > [!NOTE]
    > <span data-ttu-id="79139-134">Pour des raisons de hello de simplicité, ce didacticiel n’implémente pas de toute stratégie de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="79139-134">For hello sake of simplicity, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="79139-135">Dans le code de production, vous devez implémenter une stratégie de nouvelle tentative comme une interruption exponentielle, comme indiqué dans l’article hello [gestion des pannes temporaires].</span><span class="sxs-lookup"><span data-stu-id="79139-135">In production code, you should implement a retry policy such as exponential backoff, as suggested in hello MSDN article [Transient Fault Handling].</span></span>

3. <span data-ttu-id="79139-136">toobuild hello **appareil simulé** application à l’aide de Maven, exécutez hello commande à l’invite de commandes hello dans le dossier d’appareil simulé hello suivante :</span><span class="sxs-lookup"><span data-stu-id="79139-136">toobuild hello **simulated-device** app using Maven, execute hello following command at hello command prompt in hello simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="add-a-queue-tooyour-iot-hub-and-route-messages-tooit"></a><span data-ttu-id="79139-137">Ajouter un tooit de messages file d’attente tooyour IoT hub et d’itinéraire</span><span class="sxs-lookup"><span data-stu-id="79139-137">Add a queue tooyour IoT hub and route messages tooit</span></span>

<span data-ttu-id="79139-138">Dans cette section, vous créez une file d’attente Service Bus connectez tooyour IoT hub et configurez votre IoT hub toosend toohello file d’attente messages en fonction de la présence de hello d’une propriété de message de type hello.</span><span class="sxs-lookup"><span data-stu-id="79139-138">In this section, you create a Service Bus queue, connect it tooyour IoT hub, and configure your IoT hub toosend messages toohello queue based on hello presence of a property on hello message.</span></span> <span data-ttu-id="79139-139">Pour plus d’informations sur la tooprocess des messages des files d’attente Service Bus, consultez [prise en main les files d’attente][lnk-sb-queues-java].</span><span class="sxs-lookup"><span data-stu-id="79139-139">For more information about how tooprocess messages from Service Bus queues, see [Get started with queues][lnk-sb-queues-java].</span></span>

1. <span data-ttu-id="79139-140">Créez une file d’attente Service Bus, comme décrit dans [Prise en main des files d’attente][lnk-sb-queues-java].</span><span class="sxs-lookup"><span data-stu-id="79139-140">Create a Service Bus queue as described in [Get started with queues][lnk-sb-queues-java].</span></span> <span data-ttu-id="79139-141">Prenez note du nom d’espace de noms et de file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="79139-141">Make a note of hello namespace and queue name.</span></span>

2. <span data-ttu-id="79139-142">Dans hello portail Azure, ouvrez votre IoT hub, cliquez sur **points de terminaison**.</span><span class="sxs-lookup"><span data-stu-id="79139-142">In hello Azure portal, open your IoT hub and click **Endpoints**.</span></span>

    ![Points de terminaison dans IoT hub][30]

3. <span data-ttu-id="79139-144">Bonjour **points de terminaison** panneau, cliquez sur **ajouter** à hello tooadd supérieur votre concentrateur de IoT tooyour file d’attente.</span><span class="sxs-lookup"><span data-stu-id="79139-144">In hello **Endpoints** blade, click **Add** at hello top tooadd your queue tooyour IoT hub.</span></span> <span data-ttu-id="79139-145">Point de terminaison nom hello **CriticalQueue** et utiliser hello déroulantes tooselect **file d’attente Service Bus**hello dans lequel réside votre file d’attente de l’espace de noms de Bus de Service et hello du nom de votre file d’attente.</span><span class="sxs-lookup"><span data-stu-id="79139-145">Name hello endpoint **CriticalQueue** and use hello drop-downs tooselect **Service Bus queue**, hello Service Bus namespace in which your queue resides, and hello name of your queue.</span></span> <span data-ttu-id="79139-146">Lorsque vous avez terminé, cliquez sur **enregistrer** bas hello.</span><span class="sxs-lookup"><span data-stu-id="79139-146">When you are done, click **Save** at hello bottom.</span></span>

    ![Ajout d’un point de terminaison][31]

4. <span data-ttu-id="79139-148">À présent, cliquez sur **Itinéraires** dans votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="79139-148">Now click **Routes** in your IoT Hub.</span></span> <span data-ttu-id="79139-149">Cliquez sur **ajouter** haut hello hello panneau toocreate est une règle de routage qui achemine les messages toohello de file d’attente vous simplement ajoutée.</span><span class="sxs-lookup"><span data-stu-id="79139-149">Click **Add** at hello top of hello blade toocreate a routing rule that routes messages toohello queue you just added.</span></span> <span data-ttu-id="79139-150">Sélectionnez **DeviceTelemetry** comme source de hello de données.</span><span class="sxs-lookup"><span data-stu-id="79139-150">Select **DeviceTelemetry** as hello source of data.</span></span> <span data-ttu-id="79139-151">Entrez `level="critical"` en tant que condition de hello, choisissez la file d’attente hello vous venez d’ajouter en tant qu’un point de terminaison personnalisé en tant que point de terminaison de règle de routage de hello.</span><span class="sxs-lookup"><span data-stu-id="79139-151">Enter `level="critical"` as hello condition, and choose hello queue you just added as a custom endpoint as hello routing rule endpoint.</span></span> <span data-ttu-id="79139-152">Lorsque vous avez terminé, cliquez sur **enregistrer** bas hello.</span><span class="sxs-lookup"><span data-stu-id="79139-152">When you are done, click **Save** at hello bottom.</span></span>

    ![Ajout d’un itinéraire][32]

    <span data-ttu-id="79139-154">Assurez-vous que l’itinéraire de secours hello est défini trop**ON**.</span><span class="sxs-lookup"><span data-stu-id="79139-154">Make sure hello fallback route is set too**ON**.</span></span> <span data-ttu-id="79139-155">Ce paramètre est la configuration par défaut de hello d’un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="79139-155">This setting is hello default configuration of an IoT hub.</span></span>

    ![Itinéraire de secours][33]

## <a name="optional-read-from-hello-queue-endpoint"></a><span data-ttu-id="79139-157">(Facultatif) Lire à partir du point de terminaison de file d’attente hello</span><span class="sxs-lookup"><span data-stu-id="79139-157">(Optional) Read from hello queue endpoint</span></span>

<span data-ttu-id="79139-158">Vous pouvez éventuellement lire messages hello du point de terminaison de file d’attente hello en suivant les instructions de hello dans [prise en main les files d’attente][lnk-sb-queues-java].</span><span class="sxs-lookup"><span data-stu-id="79139-158">You can optionally read hello messages from hello queue endpoint by following hello instructions in [Get started with queues][lnk-sb-queues-java].</span></span> <span data-ttu-id="79139-159">Nom hello application **en lecture critique-file d’attente**.</span><span class="sxs-lookup"><span data-stu-id="79139-159">Name hello app **read-critical-queue**.</span></span>

## <a name="run-hello-applications"></a><span data-ttu-id="79139-160">Exécuter des applications de hello</span><span class="sxs-lookup"><span data-stu-id="79139-160">Run hello applications</span></span>

<span data-ttu-id="79139-161">Vous êtes maintenant trois applications de prêt toorun hello.</span><span class="sxs-lookup"><span data-stu-id="79139-161">Now you are ready toorun hello three applications.</span></span>

1. <span data-ttu-id="79139-162">toorun hello **en lecture-d2c-messages** application, dans une invite de commandes ou d’un interpréteur de commandes accédez toohello en lecture-d2c dossier et exécuter hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="79139-162">toorun hello **read-d2c-messages** application, in a command prompt or shell navigate toohello read-d2c folder and execute hello following command:</span></span>

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```

   ![Exécution de read-d2c-messages][readd2c]

2. <span data-ttu-id="79139-164">toorun hello **en lecture critique-file d’attente** application, dans une invite de commandes ou d’un shell accédez toohello en lecture-critique-dossier file d’attente et d’exécuter hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="79139-164">toorun hello **read-critical-queue** application, in a command prompt or shell navigate toohello read-critical-queue folder and execute hello following command:</span></span>

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![Exécution de read-critical-messages][readqueue]

3. <span data-ttu-id="79139-166">toorun hello **appareil simulé** app, dans une invite de commandes ou d’un interpréteur de commandes exploration du dossier d’appareil simulé toohello et exécuter hello commande suivante :</span><span class="sxs-lookup"><span data-stu-id="79139-166">toorun hello **simulated-device** app, in a command prompt or shell navigate toohello simulated-device folder and execute hello following command:</span></span>

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![Exécuter simulated-device][simulateddevice]

## <a name="next-steps"></a><span data-ttu-id="79139-168">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="79139-168">Next steps</span></span>

<span data-ttu-id="79139-169">Dans ce didacticiel, vous avez appris comment tooreliably distribuer des messages de l’appareil-à-cloud en utilisant la fonctionnalité de routage de messages hello du IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="79139-169">In this tutorial, you learned how tooreliably dispatch device-to-cloud messages by using hello message routing functionality of IoT Hub.</span></span>

<span data-ttu-id="79139-170">Hello [comment les messages toosend cloud-à-appareil avec IoT Hub] [ lnk-c2d] vous montre comment les messages toosend tooyour des périphériques à partir de votre serveur principal de solution.</span><span class="sxs-lookup"><span data-stu-id="79139-170">hello [How toosend cloud-to-device messages with IoT Hub][lnk-c2d] shows you how toosend messages tooyour devices from your solution back end.</span></span>

<span data-ttu-id="79139-171">exemples de toosee des solutions de bout en bout complets qui utilisent l’IoT Hub, consultez [Azure IoT Suite][lnk-suite].</span><span class="sxs-lookup"><span data-stu-id="79139-171">toosee examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite][lnk-suite].</span></span>

<span data-ttu-id="79139-172">toolearn savoir plus sur le développement de solutions avec IoT Hub, consultez hello [guide du développeur IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="79139-172">toolearn more about developing solutions with IoT Hub, see hello [IoT Hub developer guide].</span></span>

<span data-ttu-id="79139-173">toolearn en savoir plus sur le routage des messages dans IoT Hub, consultez [envoyer et recevoir des messages avec IoT Hub][lnk-devguide-messaging].</span><span class="sxs-lookup"><span data-stu-id="79139-173">toolearn more about message routing in IoT Hub, see [Send and receive messages with IoT Hub][lnk-devguide-messaging].</span></span>

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

[Stockage Azure]: https://azure.microsoft.com/documentation/services/storage/
[Azure Service Bus]: https://azure.microsoft.com/documentation/services/service-bus/

[guide du développeur IoT Hub]: iot-hub-devguide.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
[prise en main IoT Hub]: iot-hub-java-java-getstarted.md
[centre de développement Azure IoT]: https://azure.microsoft.com/develop/iot
[gestion des pannes temporaires]: https://msdn.microsoft.com/library/hh675232.aspx

<!-- Links -->
[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-c2d]: iot-hub-java-java-c2d.md
[lnk-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
