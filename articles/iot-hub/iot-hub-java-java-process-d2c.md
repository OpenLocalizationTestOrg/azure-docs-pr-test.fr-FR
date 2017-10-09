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
# <a name="process-iot-hub-device-to-cloud-messages-java"></a>Traitement des messages appareil-à-cloud IoT Hub (Java)

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

Azure IoT Hub est un service entièrement géré qui permet des communications bidirectionnelles fiables et sécurisées entre des millions d’appareils et un serveur principal de solution. Autres didacticiels ([prise en main IoT Hub] et [envoyer des messages cloud-à-appareil avec IoT Hub][lnk-c2d]) vous indiquent comment toouse hello base appareil-à-cloud et cloud-à-appareil fonctionnalités de messagerie de IoT Hub.

Ce didacticiel s’appuie sur le code hello illustré hello [prise en main IoT Hub] (didacticiel) et vous montre comment toouse message routage des messages appareil-à-cloud tooprocess de façon évolutive. didacticiel de Hello illustre la façon dont les messages tooprocess qui nécessitent une action immédiate à partir de la solution de hello back-end. Par exemple, un appareil peut envoyer un message d’alerte qui déclenche l’insertion d’un ticket dans un système CRM. Par opposition, les messages de point de données sont simplement chargés dans un moteur d’analyse. Par exemple, la télémétrie de température d’un appareil qui est toobe stockée pour une analyse ultérieure est un message de point de données.

À la fin de hello de ce didacticiel, vous exécutez trois applications de console Java :

* **APPAREIL simulé**, une version modifiée de l’application hello créée Bonjour [prise en main IoT Hub] didacticiel, envoie des messages de périphérique dans le cloud de point de données par seconde et interactif appareil-à-cloud messages toutes les 10 secondes. Cette application utilise toocommunicate de protocole AMQP hello avec IoT Hub.
* **en lecture-d2c-messages** affiche télémétrie hello envoyée par votre application.
* **en lecture critique-file d’attente** sort file d’attente de messages critiques hello de hello Bus de Service file d’attente attaché toohello IoT hub.

> [!NOTE]
> IoT Hub offre la prise en charge de Kit de développement logiciel (SDK) de plusieurs plateformes d’appareils et de plusieurs langages (notamment C, Java et JavaScript). Pour plus d’informations sur comment tooreplace hello périphérique dans ce didacticiel avec un périphérique physique, et comment tooconnect périphériques tooan IoT Hub, consultez hello [centre de développement Azure IoT].

toocomplete ce didacticiel, vous devez hello suivant :

* Une version complète de travail de hello [prise en main IoT Hub] didacticiel.
* Hello dernières [8 de Kit de développement Java SE](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Maven 3](https://maven.apache.org/install.html)
* Un compte Azure actif. (Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit] [lnk-free-trial] en quelques minutes.)

Vous devez avoir une connaissance de base de [Stockage Azure] et d’[Azure Service Bus].

## <a name="send-interactive-messages-from-a-device-app"></a>Envoyer des messages interactifs à partir d’une application pour appareils
Dans cette section, vous modifiez l’application d’appareil hello vous avez créé dans hello [prise en main IoT Hub] toooccasionally didacticiel envoyer des messages qui nécessitent un traitement immédiat.

1. Utiliser un fichier de texte éditeur tooopen hello simulated-device\src\main\java\com\mycompany\app\App.java. Ce fichier contient le code hello pour hello **appareil simulé** application que vous avez créé dans hello [prise en main IoT Hub] didacticiel.

2. Remplacez hello **MessageSender** classe avec hello suivant de code :

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
   
    Cette méthode ajoute au hasard les propriété hello `"level": "critical"` toomessages envoyés par périphérique hello, qui simule un message qui requiert une action immédiate par hello application back-end. application Hello transmet ces informations dans les propriétés de message hello, au lieu de dans le corps du message hello, afin que IoT Hub peut acheminer la destination du message approprié hello message toohello.
   
   > [!NOTE]
   > Vous pouvez utiliser des messages de tooroute de propriétés pour différents scénarios, y compris à froid-chemin d’accès de traitement, en outre des exemple de chemin réactif toohello ci-après.

2. Enregistrez et fermez le fichier de simulated-device\src\main\java\com\mycompany\app\App.java hello.

    > [!NOTE]
    > Pour des raisons de hello de simplicité, ce didacticiel n’implémente pas de toute stratégie de nouvelle tentative. Dans le code de production, vous devez implémenter une stratégie de nouvelle tentative comme une interruption exponentielle, comme indiqué dans l’article hello [gestion des pannes temporaires].

3. toobuild hello **appareil simulé** application à l’aide de Maven, exécutez hello commande à l’invite de commandes hello dans le dossier d’appareil simulé hello suivante :

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="add-a-queue-tooyour-iot-hub-and-route-messages-tooit"></a>Ajouter un tooit de messages file d’attente tooyour IoT hub et d’itinéraire

Dans cette section, vous créez une file d’attente Service Bus connectez tooyour IoT hub et configurez votre IoT hub toosend toohello file d’attente messages en fonction de la présence de hello d’une propriété de message de type hello. Pour plus d’informations sur la tooprocess des messages des files d’attente Service Bus, consultez [prise en main les files d’attente][lnk-sb-queues-java].

1. Créez une file d’attente Service Bus, comme décrit dans [Prise en main des files d’attente][lnk-sb-queues-java]. Prenez note du nom d’espace de noms et de file d’attente hello.

2. Dans hello portail Azure, ouvrez votre IoT hub, cliquez sur **points de terminaison**.

    ![Points de terminaison dans IoT hub][30]

3. Bonjour **points de terminaison** panneau, cliquez sur **ajouter** à hello tooadd supérieur votre concentrateur de IoT tooyour file d’attente. Point de terminaison nom hello **CriticalQueue** et utiliser hello déroulantes tooselect **file d’attente Service Bus**hello dans lequel réside votre file d’attente de l’espace de noms de Bus de Service et hello du nom de votre file d’attente. Lorsque vous avez terminé, cliquez sur **enregistrer** bas hello.

    ![Ajout d’un point de terminaison][31]

4. À présent, cliquez sur **Itinéraires** dans votre IoT Hub. Cliquez sur **ajouter** haut hello hello panneau toocreate est une règle de routage qui achemine les messages toohello de file d’attente vous simplement ajoutée. Sélectionnez **DeviceTelemetry** comme source de hello de données. Entrez `level="critical"` en tant que condition de hello, choisissez la file d’attente hello vous venez d’ajouter en tant qu’un point de terminaison personnalisé en tant que point de terminaison de règle de routage de hello. Lorsque vous avez terminé, cliquez sur **enregistrer** bas hello.

    ![Ajout d’un itinéraire][32]

    Assurez-vous que l’itinéraire de secours hello est défini trop**ON**. Ce paramètre est la configuration par défaut de hello d’un hub IoT.

    ![Itinéraire de secours][33]

## <a name="optional-read-from-hello-queue-endpoint"></a>(Facultatif) Lire à partir du point de terminaison de file d’attente hello

Vous pouvez éventuellement lire messages hello du point de terminaison de file d’attente hello en suivant les instructions de hello dans [prise en main les files d’attente][lnk-sb-queues-java]. Nom hello application **en lecture critique-file d’attente**.

## <a name="run-hello-applications"></a>Exécuter des applications de hello

Vous êtes maintenant trois applications de prêt toorun hello.

1. toorun hello **en lecture-d2c-messages** application, dans une invite de commandes ou d’un interpréteur de commandes accédez toohello en lecture-d2c dossier et exécuter hello de commande suivante :

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```

   ![Exécution de read-d2c-messages][readd2c]

2. toorun hello **en lecture critique-file d’attente** application, dans une invite de commandes ou d’un shell accédez toohello en lecture-critique-dossier file d’attente et d’exécuter hello de commande suivante :

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![Exécution de read-critical-messages][readqueue]

3. toorun hello **appareil simulé** app, dans une invite de commandes ou d’un interpréteur de commandes exploration du dossier d’appareil simulé toohello et exécuter hello commande suivante :

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![Exécuter simulated-device][simulateddevice]

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous avez appris comment tooreliably distribuer des messages de l’appareil-à-cloud en utilisant la fonctionnalité de routage de messages hello du IoT Hub.

Hello [comment les messages toosend cloud-à-appareil avec IoT Hub] [ lnk-c2d] vous montre comment les messages toosend tooyour des périphériques à partir de votre serveur principal de solution.

exemples de toosee des solutions de bout en bout complets qui utilisent l’IoT Hub, consultez [Azure IoT Suite][lnk-suite].

toolearn savoir plus sur le développement de solutions avec IoT Hub, consultez hello [guide du développeur IoT Hub].

toolearn en savoir plus sur le routage des messages dans IoT Hub, consultez [envoyer et recevoir des messages avec IoT Hub][lnk-devguide-messaging].

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
