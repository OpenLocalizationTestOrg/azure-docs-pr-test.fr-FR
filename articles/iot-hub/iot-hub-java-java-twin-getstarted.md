---
title: "aaaGet main jumeaux d’appareil Azure IoT Hub (Java) | Documents Microsoft"
description: "Comment toouse Azure IoT Hub appareil jumeaux tooadd balises, puis utilisez une requête IoT Hub. Vous utilisez du SDK de périphérique Azure IoT hello pour périphériques d’application Java tooimplement hello et hello Azure IoT service SDK pour Java tooimplement une application de service qui ajoute des balises de hello et s’exécute hello requête de IoT Hub."
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
ms.date: 07/04/2017
ms.author: dobett
ms.openlocfilehash: 25f6fc81471d59c62bcdc3766bb5c33f5733c930
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-java"></a>Bien démarrer avec les jumeaux d’appareils (Java)

[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

Dans ce tutoriel, vous allez créer deux applications de console Java :

* **add-tags-query**, application principale Java qui ajoute des balises et interroge les jumeaux d’appareils.
* **APPAREIL simulé**, une périphérique d’application Java que qui connecte tooyour IoT hub et les rapports de son état de connectivité à l’aide d’une propriété signalée.

> [!NOTE]
> article de Hello [kits de développement logiciel Azure IoT](iot-hub-devguide-sdks.md) fournit des informations sur hello kits de développement logiciel Azure IoT que vous pouvez utiliser toobuild applications de périphérique et back-end.

toocomplete ce didacticiel, vous devez :

* Hello dernières [8 de Kit de développement Java SE](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Maven 3](https://maven.apache.org/install.html)
* Un compte Azure actif. (Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit](http://azure.microsoft.com/pricing/free-trial/) en quelques minutes seulement.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

Si vous préférez identité d’appareil toocreate hello par programmation, lire la section correspondante de hello Bonjour [connectez votre concentrateur de IoT tooyour périphérique à l’aide de Java](iot-hub-java-java-getstarted.md#create-a-device-identity) l’article.

## <a name="create-hello-service-app"></a>Créer l’application de service hello

Dans cette section, vous créez une application Java qui ajoute des métadonnées de l’emplacement associé à un double d’appareil toohello balise dans IoT Hub **myDeviceId**. application Hello interroge d’abord IoT hub pour les périphériques situés dans hello des États-Unis, puis pour les appareils qui indiquent une connexion réseau cellulaire.

1. Sur votre ordinateur de développement, créez un dossier vide nommé `iot-java-twin-getstarted`.

1. Bonjour `iot-java-twin-getstarted` dossier, créez un projet Maven appelé **ajouter de requête de balises** à l’aide de hello, la commande suivante à l’invite suivante. Il s’agit d’une commande unique et longue :

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=add-tags-query -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. À l’invite de commandes, accédez à toohello `add-tags-query` dossier.

1. À l’aide d’un éditeur de texte, ouvrez hello `pom.xml` fichier Bonjour `add-tags-query` dossier et ajoutez hello suivant dépendance toohello **dépendances** nœud. Cette dépendance vous permet de toouse hello **iot-service-client** package dans toocommunicate de votre application avec votre IoT hub :

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

1. À l’aide d’un éditeur de texte, ouvrez hello `add-tags-query\src\main\java\com\mycompany\app\App.java` fichier.

1. Ajoutez hello suivant **importer** fichier de toohello instructions :

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.*;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.HashSet;
    import java.util.Set;
    ```

1. Ajouter hello suivant des variables de niveau classe toohello **application** classe. Remplacez `{youriothubconnectionstring}` avec votre chaîne de connexion de hub IoT noté dans hello *créez un IoT Hub* section :

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String region = "US";
    public static final String plant = "Redmond43";
    ```

1. Hello de mise à jour **principal** suivant de méthode signature tooinclude hello `throws` clause :

    ```java
    public static void main( String[] args ) throws IOException
    ```

1. Ajouter hello suivant code toohello **principal** hello toocreate de méthode **DeviceTwin** et **DeviceTwinDevice** objets. Hello **DeviceTwin** objet gère la communication de hello avec votre IoT hub. Hello **DeviceTwinDevice** objet représente le double de périphérique hello avec ses propriétés et les balises :

    ```java
    // Get hello DeviceTwin and DeviceTwinDevice objects
    DeviceTwin twinClient = DeviceTwin.createFromConnectionString(iotHubConnectionString);
    DeviceTwinDevice device = new DeviceTwinDevice(deviceId);
    ```

1. Ajoutez hello suivant `try/catch` bloquer toohello **principal** méthode :

    ```java
    try {
      // Code goes here
    } catch (IotHubException e) {
      System.out.println(e.getMessage());
    } catch (IOException e) {
      System.out.println(e.getMessage());
    }
    ```

1. tooupdate hello **région** et **plant** balises double de périphérique en double de votre appareil, ajouter hello suivant code Bonjour `try` bloc :

    ```java
    // Get hello device twin from IoT Hub
    System.out.println("Device twin before update:");
    twinClient.getTwin(device);
    System.out.println(device);

    // Update device twin tags if they are different
    // from hello existing values
    String currentTags = device.tagsToString();
    if ((!currentTags.contains("region=" + region) && !currentTags.contains("plant=" + plant))) {
      // Create hello tags and attach them toohello DeviceTwinDevice object
      Set<Pair> tags = new HashSet<Pair>();
      tags.add(new Pair("region", region));
      tags.add(new Pair("plant", plant));
      device.setTags(tags);

      // Update hello device twin in IoT Hub
      System.out.println("Updating device twin");
      twinClient.updateTwin(device);
    }

    // Retrieve hello device twin with hello tag values from IoT Hub
    System.out.println("Device twin after update:");
    twinClient.getTwin(device);
    System.out.println(device);
    ```

1. jumeaux de périphérique tooquery hello dans IoT hub, ajouter hello suivant code toohello `try` bloc après le code hello ajoutée à l’étape précédente de hello. code de Hello exécute deux requêtes. Chaque requête retourne un maximum de 100 appareils :

    ```java
    // Query hello device twins in IoT Hub
    System.out.println("Devices in Redmond:");

    // Construct hello query
    SqlQuery sqlQuery = SqlQuery.createSqlQuery("*", SqlQuery.FromType.DEVICES, "tags.plant='Redmond43'", null);

    // Run hello query, returning a maximum of 100 devices
    Query twinQuery = twinClient.queryTwin(sqlQuery.getQuery(), 100);
    while (twinClient.hasNextDeviceTwin(twinQuery)) {
      DeviceTwinDevice d = twinClient.getNextDeviceTwin(twinQuery);
      System.out.println(d.getDeviceId());
    }

    System.out.println("Devices in Redmond using a cellular network:");

    // Construct hello query
    sqlQuery = SqlQuery.createSqlQuery("*", SqlQuery.FromType.DEVICES, "tags.plant='Redmond43' AND properties.reported.connectivityType = 'cellular'", null);

    // Run hello query, returning a maximum of 100 devices
    twinQuery = twinClient.queryTwin(sqlQuery.getQuery(), 3);
    while (twinClient.hasNextDeviceTwin(twinQuery)) {
      DeviceTwinDevice d = twinClient.getNextDeviceTwin(twinQuery);
      System.out.println(d.getDeviceId());
    }
    ```

1. Enregistrez et fermez hello `add-tags-query\src\main\java\com\mycompany\app\App.java` fichier

1. Build hello **ajouter de requête de balises** application et corrigez les erreurs. À l’invite de commandes, accédez à toohello `add-tags-query` dossier et exécution hello commande suivante :

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a>Créer une application d’appareil

Dans cette section, vous créer une application de console Java qui définit une valeur de propriété signalé est envoyée tooIoT Hub.

1. Bonjour `iot-java-twin-getstarted` dossier, créez un projet Maven appelé **appareil simulé** à l’aide de hello, la commande suivante à l’invite suivante. Il s’agit d’une commande unique et longue :

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
    private static String deviceId = "myDeviceId";
    ```

    Cet exemple d’application utilise hello **protocole** variable lorsqu’il instancie une **DeviceClient** objet. Actuellement, toouse appareil double fonctionnalités vous devez utiliser le protocole MQTT hello.

1. Ajouter hello suivant code toohello **principal** méthode :
    * Créer un toocommunicate de client de périphérique avec IoT Hub.
    * Créer un **périphérique** toostore hello appareil deux propriétés de l’objet.

    ```java
    DeviceClient client = new DeviceClient(connString, protocol);

    // Create a Device object toostore hello device twin properties
    Device dataCollector = new Device() {
      // Print details when a property value changes
      @Override
      public void PropertyCall(String propertyKey, Object propertyValue, Object context) {
        System.out.println(propertyKey + " changed too" + propertyValue);
      }
    };
    ```

1. Ajouter hello suivant code toohello **principal** méthode toocreate un **connectivityType** a signalé de propriété et l’envoyer tooIoT Hub :

    ```java
    try {
      // Open hello DeviceClient and start hello device twin services.
      client.open();
      client.startDeviceTwin(new DeviceTwinStatusCallBack(), null, dataCollector, null);

      // Create a reported property and send it tooyour IoT hub.
      dataCollector.setReportedProp(new Property("connectivityType", "cellular"));
      client.sendReportedProperties(dataCollector.getReportedProp());
    }
    catch (Exception e) {
      System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" + e.getMessage());
      dataCollector.clean();
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. Ajouter hello suivant fin toohello de code Hello **principal** (méthode). En attente de hello **entrée** clé permet au statut de hello IoT Hub tooreport d’opérations de double hello appareil :

    ```java
    System.out.println("Press any key tooexit...");

    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();

    dataCollector.clean();
    client.close();
    ```

1. Enregistrez et fermez hello `simulated-device\src\main\java\com\mycompany\app\App.java` fichier.

1. Build hello **appareil simulé** application et corrigez les erreurs. À l’invite de commandes, accédez à toohello `simulated-device` dossier et exécution hello commande suivante :

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a>Exécuter des applications de hello

Vous êtes maintenant prêt toorun les applications de console hello.

1. À l’invite de commande Bonjour `add-tags-query` dossier, exécutez hello suivant commande toorun hello **ajouter de requête de balises** application de service :

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IoT Hub service application tooupdate baliser les valeurs et exécuter des requêtes de l’appareil](media/iot-hub-java-java-twin-getstarted/service-app-1.png)

    Vous pouvez voir hello **plant** et **région** balises ajoutées double de périphérique toohello. Hello première requête retourne votre appareil, mais hello deuxième pas.

1. À l’invite de commande Bonjour `simulated-device` dossier, exécutez hello suivant commande tooadd hello **connectivityType** signalés double de propriété toohello appareil :

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![client de périphérique Hello ajoute hello ** connectivityType ** signalé de propriété](media/iot-hub-java-java-twin-getstarted/device-app-1.png)

1. À l’invite de commande Bonjour `add-tags-query` dossier, exécutez hello suivant commande toorun hello **ajouter de requête de balises** service application une deuxième fois :

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IoT Hub service application tooupdate baliser les valeurs et exécuter des requêtes de l’appareil](media/iot-hub-java-java-twin-getstarted/service-app-2.png)

    Maintenant que votre appareil a envoyé hello **connectivityType** propriété tooIoT concentrateur, seconde hello retourne votre appareil.

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous configuré un IoT hub Bonjour portail Azure et ensuite créé une identité d’appareil dans le Registre des identités de hello IoT hub. Vous ajouté des métadonnées de l’appareil sous forme de balises à partir d’une application back-end et a écrit un appareil application tooreport appareil connectivité des informations en double du périphérique hello. Vous avez également appris comment tooquery hello informations double de l’appareil à l’aide du langage de requête de type SQL IoT Hub hello.

Hello utilisation suivant comment les ressources toolearn à :

* Envoyer la télémétrie des appareils avec hello [prise en main IoT Hub](iot-hub-java-java-getstarted.md) didacticiel.
* Contrôler les périphériques de manière interactive (telles que l’activation sur un ventilateur à partir d’une application contrôlée par l’utilisateur) avec hello [utiliser les méthodes directes](iot-hub-java-java-direct-methods.md) didacticiel.

<!-- Images. -->
[7]: ./media/iot-hub-java-java-twin-getstarted/invoke-method.png
[8]: ./media/iot-hub-java-java-twin-getstarted/device-listen.png
[9]: ./media/iot-hub-java-java-twin-getstarted/device-respond.png

<!-- Links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
