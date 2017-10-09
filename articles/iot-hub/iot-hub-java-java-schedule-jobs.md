---
title: travaux aaaSchedule avec Azure IoT Hub (Java) | Documents Microsoft
description: "Comment tooschedule un Azure IoT Hub tooinvoke une méthode directe de la tâche et définir une propriété de votre choix sur plusieurs appareils. Vous utilisez du SDK de périphérique Azure IoT hello pour les applications pour appareil Java tooimplement hello simulée et hello Azure IoT service SDK pour Java tooimplement un travail de service application toorun hello."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/10/2017
ms.author: dobett
ms.openlocfilehash: b1b05fa56c3ce96af0b33d4cca0dd54da0f4e927
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-and-broadcast-jobs-java"></a>Planifier et diffuser des travaux (Java)

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

Utilisez les Azure IoT Hub tooschedule et suivre les travaux qui mettent à jour des millions d’appareils. Utilisez les travaux pour :

* Mettre à jour les propriétés souhaitées
* Mettre à jour les balises
* Appeler des méthodes directes

Une tâche encapsule l’un de ces actions et effectue le suivi hello d’exécution par rapport à un ensemble d’appareils. Une requête de double périphérique définit ensemble hello hello s’exécute sur des appareils. Par exemple, une application back-end peut utiliser un tooinvoke de travail une méthode directe sur 10 000 appareils qui redémarre les appareils hello. Vous spécifiez ensemble hello d’appareils avec une requête de double de périphérique et que vous planifiez hello travail toorun à l’avenir. progression assure le suivi des travaux Hello en tant que chacun des périphériques de hello recevoir et exécuter la méthode directe de redémarrage hello.

toolearn savoir plus sur chacune de ces fonctionnalités, consultez :

* Jumeau d’appareil et propriétés : [Prise en main des représentations d’appareils (Node)](iot-hub-java-java-twin-getstarted.md)
* Méthodes directes : [Guide du développeur IoT Hub - Méthodes directes](iot-hub-devguide-direct-methods.md) et [Didacticiel : utilisation des méthodes directes](iot-hub-java-java-direct-methods.md)

Ce didacticiel vous explique les procédures suivantes :

* Créer une application pour périphérique implémentant une méthode directe nommée **lockDoor**. application d’appareil Hello reçoit également les modifications de propriété de votre choix à partir de l’application back-end de hello.
* Créer une application de serveur principal qui crée un Bonjour toocall de travail **lockDoor** méthode directe sur plusieurs appareils. Une autre tâche envoie la propriété désirée toomultiple périphériques des mises à jour.

À la fin de hello de ce didacticiel, vous avez une application de périphérique de console java et une principal d’application console java :

**APPAREIL simulé** qui se connecte tooyour IoT hub, implémente hello **lockDoor** direct de méthode et les handles de modifications apportées aux propriétés souhaité.

**planifier des travaux** qui utilisent hello toocall de travaux **lockDoor** direct double périphérique hello (méthode) et mise à jour des propriétés de la sur plusieurs appareils souhaitée.

> [!NOTE]
> article de Hello [kits de développement logiciel Azure IoT](iot-hub-devguide-sdks.md) fournit des informations sur hello kits de développement logiciel Azure IoT que vous pouvez utiliser toobuild applications de périphérique et back-end.

## <a name="prerequisites"></a>Composants requis

toocomplete ce didacticiel, vous devez :

* Hello dernières [8 de Kit de développement Java SE](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Maven 3](https://maven.apache.org/install.html)
* Un compte Azure actif. (Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit](http://azure.microsoft.com/pricing/free-trial/) en quelques minutes seulement.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

Si vous préférez identité d’appareil toocreate hello par programmation, lire la section correspondante de hello Bonjour [connectez votre concentrateur de IoT tooyour périphérique à l’aide de Java](iot-hub-java-java-getstarted.md#create-a-device-identity) l’article. Vous pouvez également utiliser hello [iothub-explorer](https://github.com/Azure/iothub-explorer) outil tooadd un IoT hub de périphérique tooyour.

## <a name="create-hello-service-app"></a>Créer l’application de service hello

Dans cette section, vous créez une application console Java qui utilise des travaux pour :

* Appelez hello **lockDoor** méthode directe sur plusieurs appareils.
* Envoyer les propriétés souhaitées toomultiple périphériques.

application hello toocreate :

1. Sur votre ordinateur de développement, créez un dossier vide nommé `iot-java-schedule-jobs`.

1. Bonjour `iot-java-schedule-jobs` dossier, créez un projet Maven appelé **planifier des travaux** à l’aide de hello, la commande suivante à l’invite suivante. Il s’agit d’une commande unique et longue :

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=schedule-jobs -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. À l’invite de commandes, accédez à toohello `schedule-jobs` dossier.

1. À l’aide d’un éditeur de texte, ouvrez hello `pom.xml` fichier Bonjour `schedule-jobs` dossier et ajoutez hello suivant dépendance toohello **dépendances** nœud. Cette dépendance vous permet de toouse hello **iot-service-client** package dans toocommunicate de votre application avec votre IoT hub :

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > Vous pouvez vérifier pour la version la plus récente de hello **iot-service-client** à l’aide de [recherche de Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).

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

1. Enregistrez et fermez hello `pom.xml` fichier.

1. À l’aide d’un éditeur de texte, ouvrez hello `schedule-jobs\src\main\java\com\mycompany\app\App.java` fichier.

1. Ajoutez hello suivant **importer** fichier de toohello instructions :

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceTwinDevice;
    import com.microsoft.azure.sdk.iot.service.devicetwin.Pair;
    import com.microsoft.azure.sdk.iot.service.devicetwin.Query;
    import com.microsoft.azure.sdk.iot.service.devicetwin.SqlQuery;
    import com.microsoft.azure.sdk.iot.service.jobs.JobClient;
    import com.microsoft.azure.sdk.iot.service.jobs.JobResult;
    import com.microsoft.azure.sdk.iot.service.jobs.JobStatus;

    import java.util.Date;
    import java.time.Instant;
    import java.util.HashSet;
    import java.util.Set;
    import java.util.UUID;
    ```

1. Ajouter hello suivant des variables de niveau classe toohello **application** classe. Remplacez `{youriothubconnectionstring}` avec votre chaîne de connexion de hub IoT noté dans hello *créez un IoT Hub* section :

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    // How long hello job is permitted toorun without
    // completing its work on hello set of devices
    private static final long maxExecutionTimeInSeconds = 30;
    ```

1. Ajouter hello suivant de méthode toohello **application** classe tooschedule un Bonjour tooupdate de travail **construction** et **Floor** propriétés de deux conteneurs de périphérique hello souhaitée :

    ```java
    private static JobResult scheduleJobSetDesiredProperties(JobClient jobClient, String jobId) {
      DeviceTwinDevice twin = new DeviceTwinDevice(deviceId);
      Set<Pair> desiredProperties = new HashSet<Pair>();
      desiredProperties.add(new Pair("Building", 43));
      desiredProperties.add(new Pair("Floor", 3));
      twin.setDesiredProperties(desiredProperties);
      // Optimistic concurrency control
      twin.setETag("*");

      // Schedule hello update twin job toorun now
      // against a single device
      System.out.println("Schedule job " + jobId + " for device " + deviceId);
      try {
        JobResult jobResult = jobClient.scheduleUpdateTwin(jobId, 
          "deviceId='" + deviceId + "'",
          twin,
          new Date(),
          maxExecutionTimeInSeconds);
        return jobResult;
      } catch (Exception e) {
        System.out.println("Exception scheduling desired properties job: " + jobId);
        System.out.println(e.getMessage());
        return null;
      }
    }
    ```

1. tooschedule un Bonjour toocall de travail **lockDoor** (méthode), ajouter hello suivant de méthode toohello **application** classe :

    ```java
    private static JobResult scheduleJobCallDirectMethod(JobClient jobClient, String jobId) {
      // Schedule a job now toocall hello lockDoor direct method
      // against a single device. Response and connection
      // timeouts are set too5 seconds.
      System.out.println("Schedule job " + jobId + " for device " + deviceId);
      try {
        JobResult jobResult = jobClient.scheduleDeviceMethod(jobId,
          "deviceId='" + deviceId + "'",
          "lockDoor",
          5L, 5L, null,
          new Date(),
          maxExecutionTimeInSeconds);
        return jobResult;
      } catch (Exception e) {
        System.out.println("Exception scheduling direct method job: " + jobId);
        System.out.println(e.getMessage());
        return null;
      }
    };
    ```

1. toomonitor un travail, ajouter hello suivant de méthode toohello **application** classe :

    ```java
    private static void monitorJob(JobClient jobClient, String jobId) {
      try {
        JobResult jobResult = jobClient.getJob(jobId);
        if(jobResult == null)
        {
          System.out.println("No JobResult for: " + jobId);
          return;
        }
        // Check hello job result until it's completed
        while(jobResult.getJobStatus() != JobStatus.completed)
        {
          Thread.sleep(100);
          jobResult = jobClient.getJob(jobId);
          System.out.println("Status " + jobResult.getJobStatus() + " for job " + jobId);
        }
        System.out.println("Final status " + jobResult.getJobStatus() + " for job " + jobId);
      } catch (Exception e) {
        System.out.println("Exception monitoring job: " + jobId);
        System.out.println(e.getMessage());
        return;
      }
    }
    ```

1. tooquery pour plus d’informations hello de travaux hello vous avez exécuté, ajoutez hello suivant de méthode :

    ```java
    private static void queryDeviceJobs(JobClient jobClient, String start) throws Exception {
      System.out.println("\nQuery device jobs since " + start);

      // Create a jobs query using hello time hello jobs started
      Query deviceJobQuery = jobClient
          .queryDeviceJob(SqlQuery.createSqlQuery("*", SqlQuery.FromType.JOBS, "devices.jobs.startTimeUtc > '" + start + "'", null).getQuery());

      // Iterate over hello list of jobs and print hello details
      while (jobClient.hasNextJob(deviceJobQuery)) {
        System.out.println(jobClient.getNextJob(deviceJobQuery));
      }
    }
    ```

1. Hello de mise à jour **principal** suivant de méthode signature tooinclude hello `throws` clause :

    ```java
    public static void main( String[] args ) throws Exception
    ```

1. toorun et le moniteur de deux travaux ajouter de manière séquentielle, hello suivant code toohello **principal** méthode :

    ```java
    // Record hello start time
    String start = Instant.now().toString();

    // Create JobClient
    JobClient jobClient = JobClient.createFromConnectionString(iotHubConnectionString);
    System.out.println("JobClient created with success");

    // Schedule twin job desired properties
    // Maximum concurrent jobs is 1 for Free and S1 tiers
    String desiredPropertiesJobId = "DPCMD" + UUID.randomUUID();
    scheduleJobSetDesiredProperties(jobClient, desiredPropertiesJobId);
    monitorJob(jobClient, desiredPropertiesJobId);

    // Schedule twin job direct method
    String directMethodJobId = "DMCMD" + UUID.randomUUID();
    scheduleJobCallDirectMethod(jobClient, directMethodJobId);
    monitorJob(jobClient, directMethodJobId);

    // Run a query tooshow hello job detail
    queryDeviceJobs(jobClient, start);

    System.out.println("Shutting down schedule-jobs app");
    ```

1. Enregistrez et fermez hello `schedule-jobs\src\main\java\com\mycompany\app\App.java` fichier

1. Build hello **planifier des travaux** application et corrigez les erreurs. À l’invite de commandes, accédez à toohello `schedule-jobs` dossier et exécution hello commande suivante :

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a>Créer une application d’appareil

Dans cette section, vous créer une application de console Java qui gère hello envoyées à partir de l’appel de méthode directe hello IoT Hub et met en œuvre de propriétés souhaitées.

1. Bonjour `iot-java-schedule-jobs` dossier, créez un projet Maven appelé **appareil simulé** à l’aide de hello, la commande suivante à l’invite suivante. Il s’agit d’une commande unique et longue :

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. À l’invite de commandes, accédez à toohello `simulated-device` dossier.

1. À l’aide d’un éditeur de texte, ouvrez hello `pom.xml` fichier Bonjour `simulated-device` dossier et ajoutez hello suivant dépendances toohello **dépendances** nœud. Cette dépendance vous permet de toouse hello **client de périphérique iot** package dans toocommunicate de votre application avec votre IoT hub :

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > Vous pouvez vérifier pour la version la plus récente de hello **client de périphérique iot** à l’aide de [recherche de Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).

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

1. Enregistrez et fermez hello `pom.xml` fichier.

1. À l’aide d’un éditeur de texte, ouvrez hello `simulated-device\src\main\java\com\mycompany\app\App.java` fichier.

1. Ajoutez hello suivant **importer** fichier de toohello instructions :

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. Ajouter hello suivant des variables de niveau classe toohello **application** classe. En remplaçant `{youriothubname}` avec votre nom de hub IoT, et `{yourdevicekey}` avec la valeur de clé de périphérique hello générées dans hello *créer une identité d’appareil* section :

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    Cet exemple d’application utilise hello **protocole** variable lorsqu’il instancie une **DeviceClient** objet. Actuellement, toouse appareil double fonctionnalités vous devez utiliser le protocole MQTT hello.

1. tooprint appareil double notifications toohello de la console, ajoutez hello imbriqués classe toohello **application** classe :

    ```java
    // Handler for device twin operation notifications from IoT Hub
    protected static class DeviceTwinStatusCallBack implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toodevice twin operation with status " + status.name());
      }
    }
    ```

1. tooprint directe toohello des notifications de méthode de la console, ajoutez hello imbriqués classe toohello **application** classe :

    ```java
    // Handler for direct method notifications from IoT Hub
    protected static class DirectMethodStatusCallback implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toodirect method operation with status " + status.name());
      }
    }
    ```

1. toohandle des appels de méthode directe à partir de IoT Hub, ajoutez des éléments suivants de hello imbriqués classe toohello **application** classe :

    ```java
    // Handler for direct method calls from IoT Hub
    protected static class DirectMethodCallback
        implements DeviceMethodCallback {
      @Override
      public DeviceMethodData call(String methodName, Object methodData, Object context) {
        DeviceMethodData deviceMethodData;
        switch (methodName) {
          case "lockDoor": {
            System.out.println("Executing direct method: " + methodName);
            deviceMethodData = new DeviceMethodData(METHOD_SUCCESS, "Executed direct method " + methodName);
            break;
          }
          default: {
            deviceMethodData = new DeviceMethodData(METHOD_NOT_DEFINED, "Not defined direct method " + methodName);
          }
        }
        // Notify IoT Hub of result
        return deviceMethodData;
      }
    }
    ```

1. Hello de mise à jour **principal** suivant de méthode signature tooinclude hello `throws` clause :

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException
    ```

1. Ajouter hello suivant code toohello **principal** méthode :
    * Créer un toocommunicate de client de périphérique avec IoT Hub.
    * Créer un **périphérique** toostore hello appareil deux propriétés de l’objet.

    ```java
    // Create a device client
    DeviceClient client = new DeviceClient(connString, protocol);

    // An object toomanage device twin desired and reported properties
    Device dataCollector = new Device() {
      @Override
      public void PropertyCall(String propertyKey, Object propertyValue, Object context)
      {
        System.out.println("Received desired property change: " + propertyKey + " " + propertyValue);
      }
    };
    ```

1. services de toostart hello appareil client, ajoutez hello suivant code toohello **principal** méthode :

    ```java
    try {
      // Open hello DeviceClient
      // Start hello device twin services
      // Subscribe toodirect method calls
      client.open();
      client.startDeviceTwin(new DeviceTwinStatusCallBack(), null, dataCollector, null);
      client.subscribeToDeviceMethod(new DirectMethodCallback(), null, new DirectMethodStatusCallback(), null);
    } catch (Exception e) {
      System.out.println("Exception, shutting down \n" + " Cause: " + e.getCause() + " \n" + e.getMessage());
      dataCollector.clean();
      client.closeNow();
      System.out.println("Shutting down...");
    }
    ```

1. toowait pour hello de hello utilisateur toopress **entrée** clé avant l’arrêt, ajouter hello suivant fin toohello de code Hello **principal** méthode :

    ```java
    // Close hello app
    System.out.println("Press any key tooexit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    dataCollector.clean();
    client.closeNow();
    scanner.close();
    ```

1. Enregistrez et fermez hello `simulated-device\src\main\java\com\mycompany\app\App.java` fichier.

1. Build hello **appareil simulé** application et corrigez les erreurs. À l’invite de commandes, accédez à toohello `simulated-device` dossier et exécution hello commande suivante :

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a>Exécuter des applications de hello

Vous êtes maintenant prêt toorun les applications de console hello.

1. À l’invite de commande Bonjour `simulated-device` dossier, exécutez hello après application d’appareil commande toostart hello l’écoute des modifications de propriété de votre choix et des appels de méthode directe :

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![client de périphérique Hello démarre](media/iot-hub-java-java-schedule-jobs/device-app-1.png)

1. À l’invite de commande Bonjour `schedule-jobs` dossier, exécutez hello suivant commande toorun hello **planifier des travaux** toorun deux travaux d’application de service. Hello définit tout d’abord les valeurs de propriété hello souhaité, appels de deuxième hello hello méthode directe :

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![L’application de service Java IoT Hub crée deux travaux](media/iot-hub-java-java-schedule-jobs/service-app-1.png)

1. application d’appareil Hello gère la modification de la propriété hello souhaitée et l’appel de méthode directe hello :

    ![client de périphérique Hello répond toohello modifications](media/iot-hub-java-java-schedule-jobs/device-app-2.png)

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous configuré un IoT hub Bonjour portail Azure et ensuite créé une identité d’appareil dans le Registre des identités de hello IoT hub. Vous avez créé une application back-end toorun deux tâches. tâche Hello définie les valeurs de propriété de votre choix et hello deuxième travail appelé une méthode directe.

Hello utilisation suivant comment les ressources toolearn à :

* Envoyer la télémétrie des appareils avec hello [prise en main IoT Hub](iot-hub-java-java-getstarted.md) didacticiel.
* Contrôler les périphériques de manière interactive (telles que l’activation sur un ventilateur à partir d’une application contrôlée par l’utilisateur) avec hello [utiliser les méthodes directes](iot-hub-java-java-direct-methods.md) didacticiel.
