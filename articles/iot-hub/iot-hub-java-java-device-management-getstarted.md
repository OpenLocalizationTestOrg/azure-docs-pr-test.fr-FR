---
title: "aaaGet a démarré avec la gestion des appareils Azure IoT Hub (Java) | Documents Microsoft"
description: "Comment toouse Azure IoT Hub device management tooinitiate un appareil distant redémarrer. Vous utilisez du SDK de périphérique Azure IoT hello pour Java tooimplement une application d’appareil simulé qui inclut une méthode directe et la hello Azure IoT service SDK pour Java tooimplement une application de service qui appelle la méthode directe hello."
services: iot-hub
documentationcenter: .java
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 7aaeda9d4ff7002e5c66adfd61e2dfd5bcea964f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-management-java"></a>Prise en main de la gestion d’appareils (Java)

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

Ce didacticiel vous explique les procédures suivantes :

* Utilisez hello toocreate portail Azure un IoT Hub et créer une identité d’appareil dans votre hub IoT.
* Créer une application d’appareil simulé qui implémente un périphérique de hello tooreboot méthode directe. Méthodes directes sont appelés à partir du cloud de hello.
* Créer une application qui appelle la méthode directe de redémarrage hello dans l’application d’appareil simulé hello via votre hub IoT. Cette application, les analyses hello propriétés signalées de hello appareil toosee lorsque l’opération de redémarrage hello est terminée.

À la fin de hello de ce didacticiel, vous avez deux applications de console Java :

**simulated-device**. Cette application :

* Se connecte à tooyour IoT hub avec l’identité de l’appareil hello créée précédemment.
* reçoit un appel de méthode directe de redémarrage ;
* simule un redémarrage physique ;
* Indique le temps hello du dernier redémarrage de hello via une propriété signalée.

**trigger-reboot**. Cette application :

* Appelle une méthode directe dans l’application d’appareil simulé hello.
* Affiche l’appel de méthode directe hello réponse toohello envoyé par appareil simulé de hello
* Hello affiche mis à jour a signalé des propriétés.

> [!NOTE]
> Pour plus d’informations sur les kits de développement logiciel de hello que vous pouvez utiliser toobuild applications toorun sur les périphériques et votre principal de la solution, consultez [kits de développement logiciel Azure IoT][lnk-hub-sdks].

toocomplete ce didacticiel, vous devez :

* Java SE 8. <br/> [Préparer votre environnement de développement] [ lnk-dev-setup] décrit comment tooinstall Java pour ce didacticiel sur Windows ou Linux.
* Maven 3.  <br/> [Préparer votre environnement de développement] [ lnk-dev-setup] décrit comment tooinstall [Maven] [ lnk-maven] pour ce didacticiel sur Windows ou Linux.
* [Node.js version 0.10.0 ou supérieure](http://nodejs.org).

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a>Déclencher un arrêt à distance sur l’appareil hello à l’aide d’une méthode directe

Dans cette section, vous allez créer une application console Java qui :

1. Appelle la méthode directe de redémarrage hello dans l’application d’appareil simulé hello.
1. Affiche la réponse de hello.
1. Hello de sondages signalé propriétés envoyées à partir de toodetermine de périphérique hello lorsque hello redémarrage soit terminé.

Cette application console connecte tooyour IoT Hub méthode directe de tooinvoke hello et lecture hello signalé des propriétés.

1. Créez un dossier vide appelé dm-get-started.

1. Dans le dossier d’exploration de données-get-started hello, créez un projet de Maven appelé **déclencheur-redémarrage** à l’aide de hello, la commande suivante à l’invite suivante. Hello Voici une commande unique longue :

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=trigger-reboot -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. À l’invite de commandes, accédez toohello déclencheur-redémarrage dossier.

1. À l’aide d’un éditeur de texte, ouvrir le fichier de pom.xml hello dans le dossier de redémarrage de déclencheur hello et ajouter hello suivant dépendance toohello **dépendances** nœud. Cette dépendance permet de vous toouse hello iot-service-package client dans votre toocommunicate d’application avec votre IoT hub :

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > Vous pouvez vérifier pour la version la plus récente de hello **iot-service-client** à l’aide de [recherche de Maven][lnk-maven-service-search].

1. Ajoutez hello suivant **générer** nœud après hello **dépendances** nœud. Cette configuration indique d’application hello toobuild 1,8 Maven toouse Java :

    ```xml
    <build>
      <plugins>
        <plugin>
          <groupId>org.apache.maven.plugins</groupId>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.3</version>
          <configuration>
            <source>1.8</source>
            <target>1.8</target>
          </configuration>
        </plugin>
      </plugins>
    </build>
    ```

1. Enregistrez et fermez le fichier de pom.xml hello.

1. À l’aide d’un éditeur de texte, d’ouvrir le fichier de source de trigger-reboot\src\main\java\com\mycompany\app\App.java hello.

1. Ajoutez hello suivant **importer** fichier de toohello instructions :

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceMethod;
    import com.microsoft.azure.sdk.iot.service.devicetwin.MethodResult;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceTwin;
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceTwinDevice;

    import java.io.IOException;
    import java.util.concurrent.TimeUnit;
    import java.util.concurrent.Executors;
    import java.util.concurrent.ExecutorService;
    ```

1. Ajouter hello suivant des variables de niveau classe toohello **application** classe. Remplacez `{youriothubconnectionstring}` avec votre chaîne de connexion de hub IoT noté dans hello *créez un IoT Hub* section :

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    private static final String methodName = "reboot";
    private static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    private static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    ```

1. tooimplement un thread qui lit hello a signalé des propriétés à partir du double du périphérique hello toutes les 10 secondes, ajoutez des éléments suivants de hello imbriqués classe toohello **application** classe :

    ```java
    private static class ShowReportedProperties implements Runnable {
      public void run() {
        try {
          DeviceTwin deviceTwins = DeviceTwin.createFromConnectionString(iotHubConnectionString);
          DeviceTwinDevice twinDevice = new DeviceTwinDevice(deviceId);
          while (true) {
            System.out.println("Get reported properties from device twin");
            deviceTwins.getTwin(twinDevice);
            System.out.println(twinDevice.reportedPropertiesToString());
            Thread.sleep(10000);
          }
        } catch (Exception ex) {
          System.out.println("Exception reading reported properties: " + ex.getMessage());
        }
      }
    }
    ```

1. méthode directe de redémarrage hello tooinvoke sur l’appareil simulé de hello, ajouter hello suivant code toohello **principal** méthode :

    ```java
    System.out.println("Starting sample...");
    DeviceMethod methodClient = DeviceMethod.createFromConnectionString(iotHubConnectionString);

    try
    {
      System.out.println("Invoke reboot direct method");
      MethodResult result = methodClient.invoke(deviceId, methodName, responseTimeout, connectTimeout, null);

      if(result == null)
      {
        throw new IOException("Invoke direct method reboot returns null");
      }
      System.out.println("Invoked reboot on device");
      System.out.println("Status for device:   " + result.getStatus());
      System.out.println("Message from device: " + result.getPayload());
    }
    catch (IotHubException e)
    {
        System.out.println(e.getMessage());
    }
    ```

1. toostart hello thread toopoll hello propriétés signalées à partir de l’appareil simulé de hello, ajoutez des hello suivant code toohello **principal** méthode :

    ```java
    ShowReportedProperties showReportedProperties = new ShowReportedProperties();
    ExecutorService executor = Executors.newFixedThreadPool(1);
    executor.execute(showReportedProperties);
    ```

1. tooenable vous toostop hello application Ajouter hello suivant code toohello **principal** méthode :

    ```java
    System.out.println("Press ENTER tooexit.");
    System.in.read();
    executor.shutdownNow();
    System.out.println("Shutting down sample...");
    ```

1. Enregistrez et fermez le fichier de trigger-reboot\src\main\java\com\mycompany\app\App.java hello.

1. Build hello **déclencheur-redémarrage** applications principal et corriger les erreurs éventuelles. Votre invite de commandes, accédez à toohello déclencheur-redémarrage dossier et exécution hello commande suivante :

    `mvn clean package -DskipTests`

## <a name="create-a-simulated-device-app"></a>Création d’une application de périphérique simulé

Dans cette section, vous créez une application console Java qui simule un appareil. application Hello écoute les appels de méthode directe hello redémarrage à partir de votre hub IoT et répond immédiatement toothat appel. Hello application puis se met en veille pendant un certain temps toosimulate le processus de redémarrage hello avant d’utiliser un Bonjour toonotify de propriété signalé **déclencheur-redémarrage** application principaux qui hello redémarrage est terminée.

1. Dans le dossier d’exploration de données-get-started hello, créez un projet de Maven appelé **appareil simulé** à l’aide de hello, la commande suivante à l’invite suivante. Hello Voici une commande unique longue :

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. Votre invite de commandes, accédez à dossier d’appareil simulé toohello.

1. À l’aide d’un éditeur de texte, ouvrir le fichier de pom.xml hello dans le dossier d’appareil simulé hello et ajouter hello suivant dépendance toohello **dépendances** nœud. Cette dépendance permet de vous toouse hello iot-service-package client dans votre toocommunicate d’application avec votre IoT hub :

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > Vous pouvez vérifier pour la version la plus récente de hello **client de périphérique iot** à l’aide de [recherche de Maven][lnk-maven-device-search].

1. Ajoutez hello suivant **générer** nœud après hello **dépendances** nœud. Cette configuration indique d’application hello toobuild 1,8 Maven toouse Java :

    ```xml
    <build>
      <plugins>
        <plugin>
          <groupId>org.apache.maven.plugins</groupId>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.3</version>
          <configuration>
            <source>1.8</source>
            <target>1.8</target>
          </configuration>
        </plugin>
      </plugins>
    </build>
    ```

1. Enregistrez et fermez le fichier de pom.xml hello.

1. À l’aide d’un éditeur de texte, d’ouvrir le fichier de source de simulated-device\src\main\java\com\mycompany\app\App.java hello.

1. Ajoutez hello suivant **importer** fichier de toohello instructions :

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.time.LocalDateTime;
    import java.util.Scanner;
    import java.util.Set;
    import java.util.HashSet;
    ```

1. Ajouter hello suivant des variables de niveau classe toohello **application** classe. Remplacez `{yourdeviceconnectionstring}` avec chaîne de connexion de périphérique hello noté Bonjour *créer une identité d’appareil* section :

    ```java
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;

    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String connString = "{yourdeviceconnectionstring}";
    private static DeviceClient client;
    ```

1. tooimplement un gestionnaire de rappel pour les événements d’état de méthode directe, ajoutez des éléments suivants de hello imbriqués classe toohello **application** classe :

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded toodevice method operation with status " + status.name());
      }
    }
    ```

1. tooimplement un gestionnaire de rappel pour les événements d’état de périphérique double, ajoutez des éléments suivants de hello imbriqués classe toohello **application** classe :

    ```java
    protected static class DeviceTwinStatusCallback implements IotHubEventCallback
    {
        public void execute(IotHubStatusCode status, Object context)
        {
            System.out.println("IoT Hub responded toodevice twin operation with status " + status.name());
        }
    }
    ```

1. tooimplement un gestionnaire de rappel pour les événements de propriété, ajoutez des éléments suivants de hello imbriqués classe toohello **application** classe :

    ```java
    protected static class PropertyCallback implements PropertyCallBack<String, String>
    {
      public void PropertyCall(String propertyKey, String propertyValue, Object context)
      {
        System.out.println("PropertyKey:     " + propertyKey);
        System.out.println("PropertyKvalue:  " + propertyKey);
      }
    }
    ```

1. tooimplement un thread toosimulate hello redémarrage de l’appareil, ajoutez des éléments suivants de hello imbriqués classe toohello **application** classe. thread de Hello se met en veille pendant cinq secondes et qu’il définit ensuite hello **lastReboot** a signalé de propriété :

    ```java
    protected static class RebootDeviceThread implements Runnable {
      public void run() {
        try {
          System.out.println("Rebooting...");
          Thread.sleep(5000);
          Property property = new Property("lastReboot", LocalDateTime.now());
          Set<Property> properties = new HashSet<Property>();
          properties.add(property);
          client.sendReportedProperties(properties);
          System.out.println("Rebooted");
        }
        catch (Exception ex) {
          System.out.println("Exception in reboot thread: " + ex.getMessage());
        }
      }
    }
    ```

1. méthode directe de tooimplement hello sur le périphérique de hello, ajoutez des éléments suivants de hello imbriqués classe toohello **application** classe. Lorsque application simulé hello reçoit un appel toohello **redémarrer** méthode directe, il retourne un appelant de toohello d’accusé de réception et démarre un Bonjour tooprocess de thread redémarrez :

    ```java
    protected static class DirectMethodCallback implements com.microsoft.azure.sdk.iot.device.DeviceTwin.DeviceMethodCallback
    {
      @Override
      public DeviceMethodData call(String methodName, Object methodData, Object context)
      {
        DeviceMethodData deviceMethodData;
        switch (methodName)
        {
          case "reboot" :
          {
            int status = METHOD_SUCCESS;
            System.out.println("Received reboot request");
            deviceMethodData = new DeviceMethodData(status, "Started reboot");
            RebootDeviceThread rebootThread = new RebootDeviceThread();
            Thread t = new Thread(rebootThread);
            t.start();
            break;
          }
          default:
          {
            int status = METHOD_NOT_DEFINED;
            deviceMethodData = new DeviceMethodData(status, "Not defined direct method " + methodName);
          }
        }
        return deviceMethodData;
      }
    }
    ```

1. Modifier la signature hello Hello **principal** hello toothrow de méthode suivant des exceptions :

    ```java
    public static void main(String[] args) throws IOException, URISyntaxException
    ```

1. tooinstantiate un **DeviceClient**, ajouter hello suivant code toohello **principal** méthode :

    ```java
    System.out.println("Starting device client sample...");
    client = new DeviceClient(connString, protocol);
    ```

1. toostart l’écoute des appels de méthode directe, ajouter hello suivant code toohello **principal** méthode :

    ```java
    try
    {
      client.open();
      client.subscribeToDeviceMethod(new DirectMethodCallback(), null, new DirectMethodStatusCallback(), null);
      client.startDeviceTwin(new DeviceTwinStatusCallback(), null, new PropertyCallback(), null);
      System.out.println("Subscribed toodirect methods and polling for reported properties. Waiting...");
    }
    catch (Exception e)
    {
      System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" +  e.getMessage());
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. tooshut vers le bas de simulateur d’appareil hello, ajouter hello suivant code toohello **principal** méthode :

    ```java
    System.out.println("Press any key tooexit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    scanner.close();
    client.close();
    System.out.println("Shutting down...");
    ```

1. Enregistrez et fermez le fichier de simulated-device\src\main\java\com\mycompany\app\App.java hello.

1. Build hello **appareil simulé** applications principal et corriger les erreurs éventuelles. Votre invite de commandes, accédez à dossier d’appareil simulé toohello et exécution hello commande suivante :

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a>Exécuter des applications de hello

Vous êtes maintenant prêt toorun hello applications.

1. À une invite de commandes dans le dossier d’appareil simulé hello, exécutez hello suivant toobegin commande écoute les appels de méthode de redémarrage à partir de votre hub IoT :

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IoT Hub simulée toolisten d’application de périphérique pour les appels de méthode directe de redémarrage][1]

1. À une invite de commandes dans le dossier de redémarrage de déclencheur hello, exécutez hello suivant de méthode de redémarrage de la commande toocall hello sur votre appareil simulé à partir de votre hub IoT :

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Hello de toocall application Java IoT Hub service redémarrer méthode directe][2]

1. APPAREIL simulé de Hello répond appel de méthode directe toohello redémarrage :

    ![Application d’appareil simulé Java IoT Hub répond l’appel de méthode directe toohello][3]

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[1]: ./media/iot-hub-java-java-device-management-getstarted/launchsimulator.png
[2]: ./media/iot-hub-java-java-device-management-getstarted/triggerreboot.png
[3]: ./media/iot-hub-java-java-device-management-getstarted/respondtoreboot.png
<!-- Links -->

[lnk-maven]: https://maven.apache.org/what-is-maven.html

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-java/blob/master/doc/java-devbox-setup.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md

[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-device-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22