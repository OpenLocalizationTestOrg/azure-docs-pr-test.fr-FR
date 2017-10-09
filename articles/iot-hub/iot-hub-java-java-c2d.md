---
title: "messages aaaCloud sur l’appareil avec Azure IoT Hub (Java) | Documents Microsoft"
description: "Comment toosend cloud-à-appareil messages appareil tooa à partir d’un hub IoT d’Azure à l’aide de kits de développement IoT hello Azure pour Java. Modifier une application appareil simulé tooreceive les messages cloud-à-appareil et de modifier une application de serveur principal toosend hello cloud-à-appareil les messages."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 7f785ea8-e7c2-40c5-87ef-96525e9b9e1e
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: dobett
ms.openlocfilehash: 8721f18428c849ed9a04aa2e45c65605c3e38101
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-to-device-messages-with-iot-hub-java"></a>Envoi de messages cloud à appareil avec IoT Hub (Java)
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

Azure IoT Hub est un service entièrement géré qui permet d’autoriser des communications bidirectionnelles fiables et sécurisées entre des millions d’appareils et un serveur principal de solution. Hello [prise en main IoT Hub] didacticiel montre comment toocreate un IoT hub, configurer une identité d’appareil qu’il contient et code d’une application d’appareil simulé qui envoie des messages de l’appareil-à-cloud.

Ce didacticiel s’appuie sur l’article [prise en main IoT Hub]. Cette rubrique vous explique les procédures suivantes :

* À partir de votre solution back-end, envoyer des messages cloud-à-appareil tooa seule unité via IoT Hub.
* Recevez des messages cloud-à-appareil sur un appareil.
* À partir de votre solution back-end demande l’accusé de réception (*commentaires*) pour tooa appareil les messages envoyés à partir de IoT Hub.

Vous trouverez plus d’informations sur les messages cloud-à-appareil Bonjour [guide du développeur IoT Hub][IoT Hub developer guide - C2D].

À la fin de hello de ce didacticiel, vous exécutez deux applications de console Java :

* **APPAREIL simulé**, une version modifiée de l’application hello créée dans [prise en main IoT Hub], qui se connecte tooyour IoT hub et reçoit des messages cloud-à-appareil.
* **envoi de messages de c2d**, qui envoie une application d’appareil simulé toohello cloud-à-appareil message via IoT Hub et reçoit ensuite son accusé de réception.

> [!NOTE]
> IoT Hub offre la prise en charge de plusieurs plateformes d’appareils et plusieurs langages (notamment C, Java et Javascript) par le biais des Kits de développement logiciel (SDK) d’appareils Azure IoT. Pour obtenir des instructions sur tooconnect du votre appareil toothis didacticiel code et généralement tooAzure IoT Hub, voir hello [centre de développement Azure IoT].

toocomplete ce didacticiel, vous devez hello suivant :

* Une version complète de travail de hello [prise en main IoT Hub](iot-hub-java-java-getstarted.md) ou [les messages appareil-à-cloud processus IoT Hub](iot-hub-java-java-process-d2c.md) didacticiel.
* Hello dernières [8 de Kit de développement Java SE](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Maven 3](https://maven.apache.org/install.html)
* Un compte Azure actif. (Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)

## <a name="receive-messages-in-hello-simulated-device-app"></a>Recevoir des messages dans une application d’appareil simulé hello

Dans cette section, vous modifiez l’application d’appareil simulé hello vous avez créé dans [prise en main IoT Hub] tooreceive les messages cloud-à-appareil à partir du hub IoT de hello.

1. À l’aide d’un éditeur de texte, d’ouvrir le fichier de simulated-device\src\main\java\com\mycompany\app\App.java hello.

2. Ajoutez hello suivant **MessageCallback** classe comme une classe imbriquée dans hello **application** classe. Hello **exécuter** méthode est appelée lors de l’appareil de hello reçoit un message d’IoT Hub. Dans cet exemple, les appareils hello notifie toujours hub IoT de hello qu’il a complété le message de type hello :

    ```java
    private static class AppMessageCallback implements MessageCallback {
      public IotHubMessageResult execute(Message msg, Object context) {
        System.out.println("Received message from hub: "
          + new String(msg.getBytes(), Message.DEFAULT_IOTHUB_MESSAGE_CHARSET));
    
        return IotHubMessageResult.COMPLETE;
      }
    }
    ```
3. Modifier hello **principal** méthode toocreate une **AppMessageCallback** hello instance et appelez **setMessageCallback** méthode avant d’ouvrir les client hello comme suit :

    ```java
    client = new DeviceClient(connString, protocol);
   
    MessageCallback callback = new AppMessageCallback();
    client.setMessageCallback(callback, null);
    client.open();
    ```

    > [!NOTE]
    > Si vous utilisez HTTP au lieu de MQTT ou AMQP comme couche de transport hello, hello **DeviceClient** instance vérifie les messages à partir du IoT Hub rarement (inférieur à 25 minutes). Pour plus d’informations sur les différences de hello entre la prise en charge MQTT, AMQP et HTTP et de limitation IoT Hub, consultez hello [guide du développeur IoT Hub][IoT Hub developer guide - C2D].

4. toobuild hello **appareil simulé** application à l’aide de Maven, exécutez hello commande à l’invite de commandes hello dans le dossier d’appareil simulé hello suivante :

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="send-a-cloud-to-device-message"></a>Envoi d’un message cloud vers appareil

Dans cette section, vous créez une application console Java qui envoie des messages cloud-à-appareil toohello appareil simulé application. Vous devez hello ID de périphérique périphérique hello vous avez ajouté dans hello [prise en main IoT Hub] didacticiel. Vous devez également hello chaîne de connexion IoT Hub pour votre concentrateur que vous pouvez trouver Bonjour [portail Azure].

1. Créez un projet Maven appelé **-c2d-envoyer des messages** à l’aide de hello, la commande suivante à l’invite suivante. Il s’agit d’une commande unique et longue :

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=send-c2d-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. À l’invite de commandes, accédez toohello nouveau dossier d’envoi de messages de c2d.

3. À l’aide d’un éditeur de texte, ouvrez le fichier de pom.xml de hello dans le dossier d’envoi-c2d-messages hello et ajouter hello suivant dépendance toohello **dépendances** nœud. Ajout de la dépendance de hello vous permet de toouse hello **iothub-java-service-client** package dans toocommunicate de votre application avec votre service de hub IoT :

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > Vous pouvez vérifier pour la version la plus récente de hello **iot-service-client** à l’aide de [recherche de Maven][lnk-maven-service-search].

4. Enregistrez et fermez le fichier de pom.xml hello.

5. À l’aide d’un éditeur de texte, d’ouvrir le fichier de send-c2d-messages\src\main\java\com\mycompany\app\App.java hello.

6. Ajoutez hello suivant **importer** fichier de toohello instructions :

    ```java
    import com.microsoft.azure.sdk.iot.service.*;
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```

7. Ajouter hello suivant des variables de niveau classe toohello **application** classe, en remplaçant **{yourhubconnectionstring}** et **{yourdeviceid}** avec hello des valeurs votre indiqués précédemment :

    ```java
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "{yourdeviceid}";
    private static final IotHubServiceClientProtocol protocol = IotHubServiceClientProtocol.AMQPS;
    ```

8. Remplacez hello **principal** méthode avec hello suivant de code. Ce code connecte tooyour IoT hub, envoie un périphérique tooyour de message et attend un accusé de réception que message hello reçus et traités d’appareil hello :
   
    ```java
    public static void main(String[] args) throws IOException,
        URISyntaxException, Exception {
      ServiceClient serviceClient = ServiceClient.createFromConnectionString(
        connectionString, protocol);
   
      if (serviceClient != null) {
        serviceClient.open();
        FeedbackReceiver feedbackReceiver = serviceClient
          .getFeedbackReceiver();
        if (feedbackReceiver != null) feedbackReceiver.open();
   
        Message messageToSend = new Message("Cloud toodevice message.");
        messageToSend.setDeliveryAcknowledgement(DeliveryAcknowledgement.Full);
   
        serviceClient.send(deviceId, messageToSend);
        System.out.println("Message sent toodevice");
   
        FeedbackBatch feedbackBatch = feedbackReceiver.receive(10000);
        if (feedbackBatch != null) {
          System.out.println("Message feedback received, feedback time: "
            + feedbackBatch.getEnqueuedTimeUtc().toString());
        }
   
        if (feedbackReceiver != null) feedbackReceiver.close();
        serviceClient.close();
      }
    }
    ```

    > [!NOTE]
    > Par souci de simplicité, ce didacticiel n’implémente aucune stratégie de nouvelle tentative. Dans le code de production, vous devez implémenter des stratégies de nouvelle tentative (par exemple, d’interruption exponentielle), comme indiqué dans l’article hello [gestion des pannes temporaires].


9. toobuild hello **appareil simulé** application à l’aide de Maven, exécutez hello commande à l’invite de commandes hello dans le dossier d’appareil simulé hello suivante :

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="run-hello-applications"></a>Exécuter des applications de hello

Vous êtes maintenant prêt toorun les applications hello.

1. À une invite de commandes dans le dossier d’appareil simulé hello, exécutez hello suivant toobegin commande envoi IoT hub tooyour de télémétrie et toolisten pour les messages cloud-à-appareil envoyés à partir de votre hub :

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```

    ![Exécutez l’application d’appareil simulé hello][img-simulated-device]

2. À une invite de commandes dans le dossier d’envoi-c2d-messages hello, exécutez hello suivant commande toosend un message du cloud sur l’appareil et l’attendre un accusé de réception de commentaires :

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

    ![Exécuter le message de salutation commande toosend hello cloud-à-appareil][img-send-command]

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous avez appris comment toosend et recevoir des messages cloud-à-appareil. 

exemples de toosee des solutions de bout en bout complets qui utilisent l’IoT Hub, consultez [Azure IoT Suite].

toolearn savoir plus sur le développement de solutions avec IoT Hub, consultez hello [guide du développeur IoT Hub].

<!-- Images -->
[img-simulated-device]: media/iot-hub-java-java-c2d/receivec2d.png
[img-send-command]:  media/iot-hub-java-java-c2d/sendc2d.png
<!-- Links -->

[prise en main IoT Hub]: iot-hub-java-java-getstarted.md
[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md
[guide du développeur IoT Hub]: iot-hub-devguide.md
[centre de développement Azure IoT]: http://www.azure.com/develop/iot
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-java
[gestion des pannes temporaires]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[portail Azure]: https://portal.azure.com
[Azure IoT Suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22