---
title: aaaGet en main Azure IoT Hub (Java) | Documents Microsoft
description: "Découvrez comment toosend appareil-à-cloud messages tooAzure IoT Hub à l’aide de kits de développement logiciel IoT pour Java. Créer appareil simulé et tooregister des applications de service de votre appareil, envoyer des messages et lire les messages de hub IoT."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 70dae4a8-0e98-4c53-b5a5-9d6963abb245
ms.service: iot-hub
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ac954f0522b46ed2a5b4a819bc611c13be0b9a9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-tooyour-iot-hub-using-java"></a>Connectez votre concentrateur de IoT tooyour périphérique à l’aide de Java
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

À la fin de hello de ce didacticiel, vous avez trois applications de console Java :

* **identité du périphérique créer**, ce qui crée une identité d’appareil et clé de sécurité associés tooconnect votre application.
* **en lecture-d2c-messages**, qui affiche la télémétrie hello envoyée par votre application.
* **APPAREIL simulé**, qui se connecte tooyour IoT hub avec l’identité de l’appareil hello créée précédemment et envoie un message de télémétrie chaque seconde à l’aide de hello le protocole MQTT.

> [!NOTE]
> article de Hello [kits de développement logiciel Azure IoT] [ lnk-hub-sdks] fournit des informations sur hello kits de développement logiciel Azure IoT que vous pouvez utiliser toobuild toorun de deux applications sur les périphériques et votre principal de la solution.

toocomplete ce didacticiel, vous devez hello suivant :

* Hello dernières [8 de Kit de développement Java SE](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) 
* [Maven 3](https://maven.apache.org/install.html) 
* Un compte Azure actif. (Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

Dans la dernière étape, prenez note de hello **clé primaire** valeur. Puis cliquez sur **points de terminaison** et hello **événements** intégré. Sur hello **propriétés** panneau, notez hello **nom du concentrateur d’événements compatibles** et hello **point de terminaison de Hub d’événements compatibles** adresse. Ces trois valeurs sont nécessaires pour créer votre application **read-d2c-messages**.

![Panneau de messagerie IoT Hub du portail Azure][6]

Votre IoT Hub est maintenant créé. Vous avez hello nom d’hôte IoT Hub, chaîne de connexion de IoT Hub, IoT Hub Primary Key, nom du concentrateur d’événements compatibles et le point de terminaison de Hub d’événements compatibles vous devez toocomplete ce didacticiel.

## <a name="create-a-device-identity"></a>Création d’une identité d’appareil
Dans cette section, vous créez une application de console Java qui crée une identité d’appareil dans le Registre des identités hello dans votre hub IoT. Un appareil ne peut pas se connecter à tooIoT concentrateur sauf si elle possède une entrée dans le Registre des identités hello. Pour plus d’informations, consultez hello **Registre des identités** section Hello [guide du développeur IoT Hub][lnk-devguide-identity]. Lorsque vous exécutez cette application console, il génère un ID d’appareil unique et clé que votre appareil peut utiliser tooidentify lui-même lorsqu’il envoie l’appareil-à-cloud messages tooIoT Hub.

1. Créez un dossier vide appelé iot-java-get-started. Dans le dossier d’iot-java-get-started hello, créez un projet de Maven appelé **identité du périphérique créer** à l’aide de hello, la commande suivante à l’invite suivante. Il s’agit d’une commande unique et longue :

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=create-device-identity -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. Votre invite de commandes, accédez à dossier d’identité du périphérique créer toohello.

3. À l’aide d’un éditeur de texte, ouvrez le fichier de pom.xml de hello dans le dossier d’identité du périphérique créer hello et ajouter hello suivant dépendance toohello **dépendances** nœud. Cette dépendance permet de vous toouse hello iot-service-package du client dans votre application :

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

5. À l’aide d’un éditeur de texte, d’ouvrir le fichier de create-device-identity\src\main\java\com\mycompany\app\App.java hello.

6. Ajoutez hello suivant **importer** fichier de toohello instructions :

    ```java
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;
    import com.microsoft.azure.sdk.iot.service.Device;
    import com.microsoft.azure.sdk.iot.service.RegistryManager;
   
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```

7. Ajouter hello suivant des variables de niveau classe toohello **application** classe, en remplaçant **{yourhubconnectionstring}** avec hello valeur votre indiqués précédemment :

    ```java
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "myFirstJavaDevice";
    ```
[!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

8. Modifier la signature hello Hello **principal** méthode tooinclude hello exceptions comme suit :

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException, Exception
    ```

9. Ajouter hello après le code en tant que corps hello Hello **principal** (méthode). Si ce n’est déjà fait, ce code crée un appareil appelé *javadevice* dans votre registre d’identités IoT Hub. Il affiche ensuite l’ID de périphérique hello et la clé dont vous avez besoin ultérieurement :

    ```java
    RegistryManager registryManager = RegistryManager.createFromConnectionString(connectionString);
RegistryManager registryManager = RegistryManager.createFromConnectionString(connectionString);

    // Create a device that's enabled by default, 
    // with an autogenerated key.
    Device device = Device.createFromId(deviceId, null, null);
    try {
      device = registryManager.addDevice(device);
    } catch (IotHubException iote) {
      // If hello device already exists.
      try {
        device = registryManager.getDevice(deviceId);
      } catch (IotHubException iotf) {
        iotf.printStackTrace();
      }
    }

    // Display information about the
    // device you created.
    System.out.println("Device Id: " + device.getDeviceId());
    System.out.println("Device key: " + device.getPrimaryKey());
    // Create a device that's enabled by default, 
    // with an autogenerated key.
    Device device = Device.createFromId(deviceId, null, null);
    try {
      device = registryManager.addDevice(device);
    } catch (IotHubException iote) {
      // If hello device already exists.
      try {
        device = registryManager.getDevice(deviceId);
      } catch (IotHubException iotf) {
        iotf.printStackTrace();
      }
    }

    // Display information about the
    // device you created.
    System.out.println("Device Id: " + device.getDeviceId());
    System.out.println("Device key: " + device.getPrimaryKey());
    ```

10. Enregistrez et fermez le fichier de App.java hello.

11. toobuild hello **identité du périphérique créer** application à l’aide de Maven, exécutez hello commande à l’invite de commandes hello dans le dossier d’identité du périphérique créer hello suivante :

    ```cmd/sh
    mvn clean package -DskipTests
    ```

12. toorun hello **identité du périphérique créer** application à l’aide de Maven, exécutez hello commande à l’invite de commandes hello dans le dossier d’identité du périphérique créer hello suivante :

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

13. Prenez note de hello **ID de périphérique** et **clé de périphérique**. Vous avez besoin de ces valeurs lorsque vous créez une application qui se connecte tooIoT Hub en tant que périphérique.

> [!NOTE]
> Hello Registre des identités IoT Hub stocke uniquement toohello IoT hub de périphérique identités tooenable un accès sécurisé. Il stocke toouse ID et les clés de périphérique en tant qu’informations d’identification de sécurité et d’un indicateur activée/désactivée que vous pouvez utiliser l’accès toodisable pour un périphérique. Si votre application doit toostore autres métadonnées spécifiques au périphérique, elle doit utiliser un magasin spécifique à l’application. Pour plus d’informations, consultez hello [guide du développeur IoT Hub][lnk-devguide-identity].

## <a name="receive-device-to-cloud-messages"></a>Recevoir des messages appareil-à-cloud

Dans cette section, vous allez créer une application console Java qui lit les messages des appareils vers le cloud dans l’IoT Hub. Un hub IoT expose un [concentrateur d’événements][lnk-event-hubs-overview]-point de terminaison compatible tooenable vous tooread les messages appareil-à-cloud. tookeep les choses simples, ce didacticiel crée un lecteur de base qui n’est pas approprié pour un déploiement d’un débit élevé. Hello [traiter les messages appareil-à-cloud] [ lnk-process-d2c-tutorial] didacticiel vous montre comment les messages tooprocess appareil-à-cloud à grande échelle. Hello [prise en main les concentrateurs d’événements] [ lnk-eventhubs-tutorial] didacticiel fournit des informations supplémentaires sur le tooprocess des messages à partir de concentrateurs d’événements et est applicable toohello points de terminaison de Hub IoT Hub événement compatible.

> [!NOTE]
> Hello point de terminaison de Hub d’événements compatibles pour la lecture des messages appareil-à-cloud toujours utilise le protocole AMQP hello.

1. Dans le dossier d’iot-java-get-started hello que vous avez créé dans hello *créer une identité d’appareil* section, créez un projet Maven appelé **en lecture-d2c-messages** à l’aide de hello, la commande suivante à l’invite suivante. Il s’agit d’une commande unique et longue :

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=read-d2c-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. Votre invite de commandes, accédez à dossier en lecture-d2c-messages de toohello.

3. À l’aide d’un éditeur de texte, ouvrir le fichier de pom.xml hello dans le dossier de lecture-d2c-messages hello et ajouter hello suivant dépendance toohello **dépendances** nœud. Cette dépendance permet toouse du package eventhubs-client hello dans tooread de votre application à partir du point de terminaison de Hub d’événements compatibles hello :

    ```xml
    <dependency> 
        <groupId>com.microsoft.azure</groupId> 
        <artifactId>azure-eventhubs</artifactId> 
        <version>0.13.0</version> 
    </dependency>
    ```

4. Enregistrez et fermez le fichier de pom.xml hello.

5. À l’aide d’un éditeur de texte, d’ouvrir le fichier de read-d2c-messages\src\main\java\com\mycompany\app\App.java hello.

6. Ajoutez hello suivant **importer** fichier de toohello instructions :

    ```java
    import java.io.IOException;
    import com.microsoft.azure.eventhubs.*;
    import com.microsoft.azure.servicebus.*;

    import java.nio.charset.Charset;
    import java.time.*;
    import java.util.function.*;
    ```

7. Ajouter hello suivant toohello de variable de niveau classe **application** classe. Remplacez **{youriothubkey}**, **{youreventhubcompatibleendpoint}**, et **{youreventhubcompatiblename}** avec les valeurs hello notées précédemment :

    ```java
    private static String connStr = "Endpoint={youreventhubcompatibleendpoint};EntityPath={youreventhubcompatiblename};SharedAccessKeyName=iothubowner;SharedAccessKey={youriothubkey}";
    ```

8. Ajoutez hello suivant **receiveMessages** méthode toohello **application** classe. Cette méthode crée un **EventHubClient** tooconnect toohello compatible concentrateur d’événements point de terminaison d’instance et puis crée de façon asynchrone un **PartitionReceiver** tooread d’instance à partir d’un concentrateur d’événements partition. Il en continu et imprime les détails du message hello jusqu'à l’arrêt de l’application hello.

    ```java
    // Create a receiver on a partition.
    private static EventHubClient receiveMessages(final String partitionId) {
      EventHubClient client = null;
      try {
        client = EventHubClient.createFromConnectionStringSync(connStr);
      } catch (Exception e) {
        System.out.println("Failed toocreate client: " + e.getMessage());
        System.exit(1);
      }
      try {
        // Create a receiver using the
        // default Event Hubs consumer group
        // that listens for messages from now on.
        client.createReceiver(EventHubClient.DEFAULT_CONSUMER_GROUP_NAME, partitionId, Instant.now())
          .thenAccept(new Consumer<PartitionReceiver>() {
            public void accept(PartitionReceiver receiver) {
              System.out.println("** Created receiver on partition " + partitionId);
              try {
                while (true) {
                  Iterable<EventData> receivedEvents = receiver.receive(100).get();
                  int batchSize = 0;
                  if (receivedEvents != null) {
                    System.out.println("Got some evenst");
                    for (EventData receivedEvent : receivedEvents) {
                      System.out.println(String.format("Offset: %s, SeqNo: %s, EnqueueTime: %s",
                        receivedEvent.getSystemProperties().getOffset(),
                        receivedEvent.getSystemProperties().getSequenceNumber(),
                        receivedEvent.getSystemProperties().getEnqueuedTime()));
                      System.out.println(String.format("| Device ID: %s",
                        receivedEvent.getSystemProperties().get("iothub-connection-device-id")));
                      System.out.println(String.format("| Message Payload: %s",
                        new String(receivedEvent.getBytes(), Charset.defaultCharset())));
                      batchSize++;
                    }
                  }
                  System.out.println(String.format("Partition: %s, ReceivedBatch Size: %s", partitionId, batchSize));
                }
              } catch (Exception e) {
                System.out.println("Failed tooreceive messages: " + e.getMessage());
              }
            }
          });
        } catch (Exception e) {
          System.out.println("Failed toocreate receiver: " + e.getMessage());
      }
      return client;
    }
    ```

   > [!NOTE]
   > Cette méthode utilise un filtre lorsqu’il crée le récepteur de hello afin que hello récepteur lit uniquement les messages envoyés tooIoT Hub après que le récepteur de hello commence à s’exécuter. Cette technique est utile dans un environnement de test afin de voir l’ensemble actuel de hello de messages. Dans un environnement de production, votre code doit vous assurer qu’elle traite tous les messages hello - pour plus d’informations, consultez hello [comment tooprocess les messages appareil-à-cloud IoT Hub] [ lnk-process-d2c-tutorial] didacticiel.

9. Modifier la signature hello Hello **principal** méthode tooinclude hello exception comme suit :

    ```java
    public static void main( String[] args ) throws IOException
    ```

10. Ajouter hello suivant code toohello **principal** méthode Bonjour **application** classe. Ce code crée deux de hello **EventHubClient** et **PartitionReceiver** instances et vous permet de tooclose hello application lorsque vous avez terminé le traitement des messages :

    ```java
    // Create receivers for partitions 0 and 1.
    EventHubClient client0 = receiveMessages("0");
    EventHubClient client1 = receiveMessages("1");
    System.out.println("Press ENTER tooexit.");
    System.in.read();
    try {
      client0.closeSync();
      client1.closeSync();
      System.exit(0);
    } catch (ServiceBusException sbe) {
      System.exit(1);
    }
    ```

    > [!NOTE]
    > Ce code suppose que vous avez créé votre hub IoT dans la couche de hello F1 (gratuit). Un IoT Hub gratuit comporte deux partitions nommées « 0 » et « 1 ».

11. Enregistrez et fermez le fichier de App.java hello.

12. toobuild hello **en lecture-d2c-messages** application à l’aide de Maven, exécutez hello commande à l’invite de commandes hello dans le dossier de lecture-d2c-messages hello suivante :

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="create-a-device-app"></a>Créer une application d’appareil
Dans cette section, vous créez une application console Java qui simule un appareil qui envoie l’IoT hub tooan de messages appareil-à-cloud.

1. Dans le dossier d’iot-java-get-started hello que vous avez créé dans hello *créer une identité d’appareil* section, créez un projet Maven appelé **appareil simulé** à l’aide de hello, la commande suivante à l’invite suivante. Il s’agit d’une commande unique et longue :

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. Votre invite de commandes, accédez à dossier d’appareil simulé toohello.

3. À l’aide d’un éditeur de texte, ouvrir le fichier de pom.xml hello dans le dossier d’appareil simulé hello et ajouter hello suivant dépendances toohello **dépendances** nœud. Cette dépendance permet de vous toouse hello iothub-java-package client dans votre toocommunicate d’application avec votre IoT hub et la tooserialize tooJSON d’objets Java :

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    <dependency>
      <groupId>com.google.code.gson</groupId>
      <artifactId>gson</artifactId>
      <version>2.3.1</version>
    </dependency>
    ```

    > [!NOTE]
    > Vous pouvez vérifier pour la version la plus récente de hello **client de périphérique iot** à l’aide de [recherche de Maven][lnk-maven-device-search].

4. Enregistrez et fermez le fichier de pom.xml hello.

5. À l’aide d’un éditeur de texte, d’ouvrir le fichier de simulated-device\src\main\java\com\mycompany\app\App.java hello.

6. Ajoutez hello suivant **importer** fichier de toohello instructions :

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.google.gson.Gson;

    import java.io.*;
    import java.net.URISyntaxException;
    import java.util.Random;
    import java.util.concurrent.Executors;
    import java.util.concurrent.ExecutorService;
    ```

7. Ajouter hello suivant des variables de niveau classe toohello **application** classe. En remplaçant **{youriothubname}** avec votre nom de hub IoT, et **{yourdevicekey}** avec la valeur de clé de périphérique hello générées dans hello *créer une identité d’appareil* section :

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myFirstJavaDevice;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myFirstJavaDevice";
    private static DeviceClient client;
    ```
   
    Cet exemple d’application utilise hello **protocole** variable lorsqu’il instancie une **DeviceClient** objet. Vous pouvez utiliser soit toocommunicate de protocole hello MQTT, AMQP ou HTTP avec IoT Hub.

8. Ajoutez suit hello imbriqués **TelemetryDataPoint** classe à l’intérieur de hello **application** classe les données de télémétrie hello toospecify votre appareil envoie tooyour IoT hub :

    ```java
    private static class TelemetryDataPoint {
      public String deviceId;
      public double temperature;
      public double humidity;
   
      public String serialize() {
        Gson gson = new Gson();
        return gson.toJson(this);
      }
    }
    ```
9. Ajoutez suit hello imbriqués **EventCallback** classe à l’intérieur de hello **application** état classe toodisplay hello accusé de réception qui hello IoT hub retourne lorsqu’il traite un message à partir de l’application hello. Cette méthode signale également thread principal de hello dans l’application hello hello message a été traité :
   
    ```java
    private static class EventCallback implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toomessage with status: " + status.name());
   
        if (context != null) {
          synchronized (context) {
            context.notify();
          }
        }
      }
    }
    ```

10. Ajoutez suit hello imbriqués **MessageSender** classe à l’intérieur de hello **application** classe. Hello **exécuter** méthode dans cette classe génère tooyour IoT hub pour exemple télémétrie données toosend et attend un accusé de réception avant d’envoyer le message de type hello suivant :

    ```java
    private static class MessageSender implements Runnable {
      public void run()  {
        try {
          double minTemperature = 20;
          double minHumidity = 60;
          Random rand = new Random();
    
          while (true) {
            double currentTemperature = minTemperature + rand.nextDouble() * 15;
            double currentHumidity = minHumidity + rand.nextDouble() * 20;
            TelemetryDataPoint telemetryDataPoint = new TelemetryDataPoint();
            telemetryDataPoint.deviceId = deviceId;
            telemetryDataPoint.temperature = currentTemperature;
            telemetryDataPoint.humidity = currentHumidity;
    
            String msgStr = telemetryDataPoint.serialize();
            Message msg = new Message(msgStr);
            msg.setProperty("temperatureAlert", (currentTemperature > 30) ? "true" : "false");
            msg.setMessageId(java.util.UUID.randomUUID().toString()); 
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

    Cette méthode envoie un nouveau message de l’appareil-à-cloud une seconde après que le précédent message de type hello accuse réception de hub IoT de hello. message de salutation contient un objet JSON sérialisé avec hello deviceId et généré de façon aléatoire les numéros toosimulate un capteur de température et un capteur humidité.

11. Remplacez hello **principal** méthode avec hello suivant le code qui crée un hub IoT de tooyour thread toosend messages appareil-à-cloud :

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException {
      client = new DeviceClient(connString, protocol);
      client.open();
    
      MessageSender sender = new MessageSender();
    
      ExecutorService executor = Executors.newFixedThreadPool(1);
      executor.execute(sender);
    
      System.out.println("Press ENTER tooexit.");
      System.in.read();
      executor.shutdownNow();
      client.closeNow();
    }
    ```

12. Enregistrez et fermez le fichier de App.java hello.

13. toobuild hello **appareil simulé** application à l’aide de Maven, exécutez hello commande à l’invite de commandes hello dans le dossier d’appareil simulé hello suivante :

    ```cmd/sh
    mvn clean package -DskipTests
    ```

> [!NOTE]
> tookeep les choses simples, ce didacticiel n’implémente pas de toute stratégie de nouvelle tentative. Dans le code de production, vous devez implémenter des stratégies de nouvelle tentative (par exemple, une interruption exponentielle), comme indiqué dans l’article hello [gestion des pannes temporaires][lnk-transient-faults].

## <a name="run-hello-apps"></a>Exécuter des applications de hello

Vous êtes maintenant prêt toorun hello applications.

1. À une invite de commandes dans le dossier en lecture-d2c de hello, exécutez hello suivant toobegin commande analyse la première partition de hello dans votre IoT hub :

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

    ![Messages appareil-à-cloud toomonitor d’application du service Java IoT Hub][7]

2. À une invite de commandes dans le dossier d’appareil simulé hello, exécutez hello suivant toobegin commande envoi tooyour IoT hub de télémétrie des données :

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```

    ![Messages appareil-à-cloud toosend Java IoT Hub appareil application][8]

3. Hello **utilisation** vignette Bonjour [portail Azure] [ lnk-portal] affiche hello le nombre de messages envoyés toohello IoT hub :

    ![Azure portail d’utilisation vignette affichage du nombre de messages envoyés tooIoT Hub][43]

## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, vous configuré un IoT hub Bonjour portail Azure et ensuite créé une identité d’appareil dans le Registre des identités de hello IoT hub. Vous avez utilisé ce périphérique identité tooenable hello appareil application toosend messages appareil-à-cloud toohello hub IoT. Vous avez créé également une application qui affiche les messages hello reçus par IoT hub de hello.

toocontinue mise en route avec IoT Hub et tooexplore autres scénarios IoT, consultez :

* [Connexion de votre appareil][lnk-connect-device]
* [Prise en main de la gestion d’appareils][lnk-device-management]
* [Explore Azure IoT Edge architecture on Linux][lnk-iot-edge] (Découvrir l’architecture Azure IoT Edge sur Linux)

toolearn tooextend vos messages IoT solution et des processus de périphérique dans le cloud à grande échelle, voir hello [traiter les messages appareil-à-cloud] [ lnk-process-d2c-tutorial] didacticiel.
[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

<!-- Images. -->
[6]: ./media/iot-hub-java-java-getstarted/create-iot-hub6.png
[7]: ./media/iot-hub-java-java-getstarted/runapp1.png
[8]: ./media/iot-hub-java-java-getstarted/runapp2.png
[43]: ./media/iot-hub-java-java-getstarted/usage.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-devguide-identity]: iot-hub-devguide-identity-registry.md
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md
[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-device-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-eventhubs-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22
