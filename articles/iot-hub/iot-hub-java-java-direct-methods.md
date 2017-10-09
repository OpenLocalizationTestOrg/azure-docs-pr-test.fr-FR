---
title: "aaaUse Azure IoT Hub direct de méthodes (Java) | Documents Microsoft"
description: "Comment toouse Azure IoT Hub direct de méthodes. Vous utilisez du SDK de périphérique Azure IoT hello pour Java tooimplement une application d’appareil simulé qui inclut une méthode directe et la hello Azure IoT service SDK pour Java tooimplement une application de service qui appelle la méthode directe hello."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: ab035b8e-bff8-4e12-9536-f31d6b6fe425
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: b6f2f4a64535ab649a3965cd9c5a19bebaf88eef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-java"></a>Utilisation des méthodes directes (Java)

[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

Dans ce tutoriel, vous allez créer deux applications de console Java :

* **méthode directe Invoke**, une principal d’application Java qui appelle une méthode dans l’application d’appareil simulé hello et affiche la réponse de hello.
* **APPAREIL simulé**, une application Java qui simule un appareil de connexion tooyour IoT hub avec l’identité d’appareil hello vous créez. Cette application répond toohello directement appelée à partir de back-end hello.

> [!NOTE]
> Pour plus d’informations sur les kits de développement logiciel de hello que vous pouvez utiliser toobuild applications toorun sur les périphériques et votre principal de la solution, consultez [kits de développement logiciel Azure IoT][lnk-hub-sdks].

toocomplete ce didacticiel, vous devez :

* Java SE 8. <br/> [Préparer votre environnement de développement] [ lnk-dev-setup] décrit comment tooinstall Java pour ce didacticiel sur Windows ou Linux.
* Maven 3.  <br/> [Préparer votre environnement de développement] [ lnk-dev-setup] décrit comment tooinstall [Maven] [ lnk-maven] pour ce didacticiel sur Windows ou Linux.
* [Node.js version 0.10.0 ou supérieure](http://nodejs.org).

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a>Création d’une application de périphérique simulé

Dans cette section, vous créez une application de console Java qui répond méthode tooa appelée par solution hello retour de fin.

1. Créez un dossier vide appelé iot-java-direct-method.

1. Dans le dossier de méthode iot-java-direct hello, créez un projet de Maven appelé **appareil simulé** à l’aide de hello, la commande suivante à l’invite suivante. Hello commande suivante est une commande unique longue :

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. Votre invite de commandes, accédez à dossier d’appareil simulé toohello.

1. À l’aide d’un éditeur de texte, ouvrir le fichier de pom.xml hello dans le dossier d’appareil simulé hello et ajouter hello suivant dépendances toohello **dépendances** nœud. Cette dépendance permet à vous toouse hello client de périphérique iot package dans toocommunicate de votre application avec votre IoT hub :

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

1. À l’aide d’un éditeur de texte, d’ouvrir le fichier de simulated-device\src\main\java\com\mycompany\app\App.java hello.

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
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    Cet exemple d’application utilise hello **protocole** variable lorsqu’il instancie une **DeviceClient** objet. Actuellement, toouse directe des méthodes que vous devez utiliser le protocole MQTT hello.

1. tooreturn un IoT hub état code tooyour, ajoutez des éléments suivants de hello imbriqués classe toohello **application** classe :

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded toodevice method operation with status " + status.name());
      }
    }
    ```

1. appels de méthode directe d’hello toohandle de hello solution serveur principal, ajoutez des éléments suivants de hello imbriqués classe toohello **application** classe :

    ```java
    protected static class DirectMethodCallback implements com.microsoft.azure.sdk.iot.device.DeviceTwin.DeviceMethodCallback
    {
      @Override
      public DeviceMethodData call(String methodName, Object methodData, Object context)
      {
        DeviceMethodData deviceMethodData;
        switch (methodName)
        {
          case "writeLine" :
          {
            int status = METHOD_SUCCESS;
            System.out.println(new String((byte[])methodData));
            deviceMethodData = new DeviceMethodData(status, "Executed direct method " + methodName);
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

1. toocreate un **DeviceClient** et écouter les appels de méthode directe, ajoutez un **principal** méthode toohello **application** classe :

    ```java
    public static void main(String[] args)
      throws IOException, URISyntaxException
    {
      System.out.println("Starting device sample...");

      DeviceClient client = new DeviceClient(connString, protocol);

      try
      {
        client.open();
        client.subscribeToDeviceMethod(new DirectMethodCallback(), null, new DirectMethodStatusCallback(), null);
        System.out.println("Subscribed toodirect methods. Waiting...");
      }
      catch (Exception e)
      {
        System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" +  e.getMessage());
        client.close();
        System.out.println("Shutting down...");
      }

      System.out.println("Press any key tooexit...");
      Scanner scanner = new Scanner(System.in);
      scanner.nextLine();
      scanner.close();
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. Enregistrez et fermez le fichier de simulated-device\src\main\java\com\mycompany\app\App.java hello

1. Build hello **appareil simulé** application et corrigez les erreurs. Votre invite de commandes, accédez à dossier d’appareil simulé toohello et exécution hello commande suivante :

    `mvn clean package -DskipTests`

## <a name="call-a-direct-method-on-a-device"></a>Appeler une méthode directe sur un appareil

Dans cette section, vous créez une application de console Java qui appelle une méthode directe, puis affiche les réponse hello. Cette application console connecte tooyour méthode directe de IoT Hub tooinvoke hello.

1. Dans le dossier de méthode iot-java-direct hello, créez un projet de Maven appelé **méthode direct invoke** à l’aide de hello, la commande suivante à l’invite suivante. Hello commande suivante est une commande unique longue :

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=invoke-direct-method -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. Votre invite de commandes, accédez à toohello invoke-direct-méthode dossier.

1. À l’aide d’un éditeur de texte, ouvrez le fichier de pom.xml de hello dans le dossier d’appel de méthode de direct hello et ajouter hello suivant dépendance toohello **dépendances** nœud. Cette dépendance permet de vous toouse hello iot-service-package client dans votre toocommunicate d’application avec votre IoT hub :

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

1. À l’aide d’un éditeur de texte, d’ouvrir le fichier de invoke-direct-method\src\main\java\com\mycompany\app\App.java hello.

1. Ajoutez hello suivant **importer** fichier de toohello instructions :

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceMethod;
    import com.microsoft.azure.sdk.iot.service.devicetwin.MethodResult;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.concurrent.TimeUnit;
    ```

1. Ajouter hello suivant des variables de niveau classe toohello **application** classe. Remplacez `{youriothubconnectionstring}` avec votre chaîne de connexion de hub IoT noté dans hello *créez un IoT Hub* section :

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String methodName = "writeLine";
    public static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    public static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    public static final String payload = "a line toobe written";
    ```

1. méthode hello tooinvoke appareil simulé de hello, ajouter hello suivant code toohello **principal** méthode :

    ```java
    System.out.println("Starting sample...");
    DeviceMethod methodClient = DeviceMethod.createFromConnectionString(iotHubConnectionString);

    try
    {
        System.out.println("Invoke direct method");
        MethodResult result = methodClient.invoke(deviceId, methodName, responseTimeout, connectTimeout, payload);

        if(result == null)
        {
            throw new IOException("Direct method invoke returns null");
        }
        System.out.println("Status=" + result.getStatus());
        System.out.println("Payload=" + result.getPayload());
    }
    catch (IotHubException e)
    {
        System.out.println(e.getMessage());
    }

    System.out.println("Shutting down sample...");
    ```

1. Enregistrez et fermez le fichier de invoke-direct-method\src\main\java\com\mycompany\app\App.java hello

1. Build hello **méthode direct invoke** application et corrigez les erreurs. Votre invite de commandes, accédez à dossier d’appel de méthode de direct toohello et exécution hello commande suivante :

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a>Exécuter des applications de hello

Vous êtes maintenant prêt toorun les applications de console hello.

1. À une invite de commandes dans le dossier d’appareil simulé hello, exécutez hello suivant toobegin commande écoute les appels de méthode à partir de votre hub IoT :

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IoT Hub simulée toolisten d’application de périphérique pour les appels de méthode directe][8]

1. À une invite de commandes dans le dossier d’appel de méthode de direct hello, exécutez hello suivant de commande toocall une méthode sur votre appareil simulé à partir de votre hub IoT :

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IoT Hub service application toocall une méthode directe][7]

1. APPAREIL simulé de Hello répond l’appel de méthode directe toohello :

    ![Application d’appareil simulé Java IoT Hub répond l’appel de méthode directe toohello][9]

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous configuré un IoT hub Bonjour portail Azure et ensuite créé une identité d’appareil dans le Registre des identités de hello IoT hub. Vous avez utilisé ce périphérique identité tooenable hello simulée appareil application tooreact toomethods appelée par le cloud de hello. Vous avez créé également une application qui appelle des méthodes sur l’appareil de hello et affiche la réponse hello périphérique de hello.

tooexplore autres scénarios IoT, consultez [planifier des travaux sur plusieurs appareils][lnk-devguide-jobs].

toolearn tooextend votre méthode de planification et de solution IoT des appels sur plusieurs appareils, consultez hello [planification et les tâches de diffusion] [ lnk-tutorial-jobs] didacticiel.

<!-- Images. -->
[7]: ./media/iot-hub-java-java-direct-methods/invoke-method.png
[8]: ./media/iot-hub-java-java-direct-methods/device-listen.png
[9]: ./media/iot-hub-java-java-direct-methods/device-respond.png

<!-- Links -->
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-java/blob/master/doc/java-devbox-setup.md
[lnk-maven]: https://maven.apache.org/what-is-maven.html
[lnk-hub-sdks]: iot-hub-devguide-sdks.md

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-device-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
