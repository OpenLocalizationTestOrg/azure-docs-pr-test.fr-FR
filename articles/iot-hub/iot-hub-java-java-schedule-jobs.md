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
# <a name="schedule-and-broadcast-jobs-java"></a><span data-ttu-id="42b68-104">Planifier et diffuser des travaux (Java)</span><span class="sxs-lookup"><span data-stu-id="42b68-104">Schedule and broadcast jobs (Java)</span></span>

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

<span data-ttu-id="42b68-105">Utilisez les Azure IoT Hub tooschedule et suivre les travaux qui mettent à jour des millions d’appareils.</span><span class="sxs-lookup"><span data-stu-id="42b68-105">Use Azure IoT Hub tooschedule and track jobs that update millions of devices.</span></span> <span data-ttu-id="42b68-106">Utilisez les travaux pour :</span><span class="sxs-lookup"><span data-stu-id="42b68-106">Use jobs to:</span></span>

* <span data-ttu-id="42b68-107">Mettre à jour les propriétés souhaitées</span><span class="sxs-lookup"><span data-stu-id="42b68-107">Update desired properties</span></span>
* <span data-ttu-id="42b68-108">Mettre à jour les balises</span><span class="sxs-lookup"><span data-stu-id="42b68-108">Update tags</span></span>
* <span data-ttu-id="42b68-109">Appeler des méthodes directes</span><span class="sxs-lookup"><span data-stu-id="42b68-109">Invoke direct methods</span></span>

<span data-ttu-id="42b68-110">Une tâche encapsule l’un de ces actions et effectue le suivi hello d’exécution par rapport à un ensemble d’appareils.</span><span class="sxs-lookup"><span data-stu-id="42b68-110">A job wraps one of these actions and tracks hello execution against a set of devices.</span></span> <span data-ttu-id="42b68-111">Une requête de double périphérique définit ensemble hello hello s’exécute sur des appareils.</span><span class="sxs-lookup"><span data-stu-id="42b68-111">A device twin query defines hello set of devices hello job executes against.</span></span> <span data-ttu-id="42b68-112">Par exemple, une application back-end peut utiliser un tooinvoke de travail une méthode directe sur 10 000 appareils qui redémarre les appareils hello.</span><span class="sxs-lookup"><span data-stu-id="42b68-112">For example, a back-end app can use a job tooinvoke a direct method on 10,000 devices that reboots hello devices.</span></span> <span data-ttu-id="42b68-113">Vous spécifiez ensemble hello d’appareils avec une requête de double de périphérique et que vous planifiez hello travail toorun à l’avenir.</span><span class="sxs-lookup"><span data-stu-id="42b68-113">You specify hello set of devices with a device twin query and schedule hello job toorun at a future time.</span></span> <span data-ttu-id="42b68-114">progression assure le suivi des travaux Hello en tant que chacun des périphériques de hello recevoir et exécuter la méthode directe de redémarrage hello.</span><span class="sxs-lookup"><span data-stu-id="42b68-114">hello job tracks progress as each of hello devices receive and execute hello reboot direct method.</span></span>

<span data-ttu-id="42b68-115">toolearn savoir plus sur chacune de ces fonctionnalités, consultez :</span><span class="sxs-lookup"><span data-stu-id="42b68-115">toolearn more about each of these capabilities, see:</span></span>

* <span data-ttu-id="42b68-116">Jumeau d’appareil et propriétés : [Prise en main des représentations d’appareils (Node)](iot-hub-java-java-twin-getstarted.md)</span><span class="sxs-lookup"><span data-stu-id="42b68-116">Device twin and properties: [Get started with device twins](iot-hub-java-java-twin-getstarted.md)</span></span>
* <span data-ttu-id="42b68-117">Méthodes directes : [Guide du développeur IoT Hub - Méthodes directes](iot-hub-devguide-direct-methods.md) et [Didacticiel : utilisation des méthodes directes](iot-hub-java-java-direct-methods.md)</span><span class="sxs-lookup"><span data-stu-id="42b68-117">Direct methods: [IoT Hub developer guide - direct methods](iot-hub-devguide-direct-methods.md) and [Tutorial: Use direct methods](iot-hub-java-java-direct-methods.md)</span></span>

<span data-ttu-id="42b68-118">Ce didacticiel vous explique les procédures suivantes :</span><span class="sxs-lookup"><span data-stu-id="42b68-118">This tutorial shows you how to:</span></span>

* <span data-ttu-id="42b68-119">Créer une application pour périphérique implémentant une méthode directe nommée **lockDoor**.</span><span class="sxs-lookup"><span data-stu-id="42b68-119">Create a device app that implements a direct method called **lockDoor**.</span></span> <span data-ttu-id="42b68-120">application d’appareil Hello reçoit également les modifications de propriété de votre choix à partir de l’application back-end de hello.</span><span class="sxs-lookup"><span data-stu-id="42b68-120">hello device app also receives desired property changes from hello back-end app.</span></span>
* <span data-ttu-id="42b68-121">Créer une application de serveur principal qui crée un Bonjour toocall de travail **lockDoor** méthode directe sur plusieurs appareils.</span><span class="sxs-lookup"><span data-stu-id="42b68-121">Create a back-end app that creates a job toocall hello **lockDoor** direct method on multiple devices.</span></span> <span data-ttu-id="42b68-122">Une autre tâche envoie la propriété désirée toomultiple périphériques des mises à jour.</span><span class="sxs-lookup"><span data-stu-id="42b68-122">Another job sends desired property updates toomultiple devices.</span></span>

<span data-ttu-id="42b68-123">À la fin de hello de ce didacticiel, vous avez une application de périphérique de console java et une principal d’application console java :</span><span class="sxs-lookup"><span data-stu-id="42b68-123">At hello end of this tutorial, you have a java console device app and a java console back-end app:</span></span>

<span data-ttu-id="42b68-124">**APPAREIL simulé** qui se connecte tooyour IoT hub, implémente hello **lockDoor** direct de méthode et les handles de modifications apportées aux propriétés souhaité.</span><span class="sxs-lookup"><span data-stu-id="42b68-124">**simulated-device** that connects tooyour IoT hub, implements hello **lockDoor** direct method, and handles desired property changes.</span></span>

<span data-ttu-id="42b68-125">**planifier des travaux** qui utilisent hello toocall de travaux **lockDoor** direct double périphérique hello (méthode) et mise à jour des propriétés de la sur plusieurs appareils souhaitée.</span><span class="sxs-lookup"><span data-stu-id="42b68-125">**schedule-jobs** that use jobs toocall hello **lockDoor** direct method and update hello device twin desired properties on multiple devices.</span></span>

> [!NOTE]
> <span data-ttu-id="42b68-126">article de Hello [kits de développement logiciel Azure IoT](iot-hub-devguide-sdks.md) fournit des informations sur hello kits de développement logiciel Azure IoT que vous pouvez utiliser toobuild applications de périphérique et back-end.</span><span class="sxs-lookup"><span data-stu-id="42b68-126">hello article [Azure IoT SDKs](iot-hub-devguide-sdks.md) provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="42b68-127">Composants requis</span><span class="sxs-lookup"><span data-stu-id="42b68-127">Prerequisites</span></span>

<span data-ttu-id="42b68-128">toocomplete ce didacticiel, vous devez :</span><span class="sxs-lookup"><span data-stu-id="42b68-128">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="42b68-129">Hello dernières [8 de Kit de développement Java SE](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="42b68-129">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="42b68-130">Maven 3</span><span class="sxs-lookup"><span data-stu-id="42b68-130">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="42b68-131">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="42b68-131">An active Azure account.</span></span> <span data-ttu-id="42b68-132">(Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit](http://azure.microsoft.com/pricing/free-trial/) en quelques minutes seulement.)</span><span class="sxs-lookup"><span data-stu-id="42b68-132">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="42b68-133">Si vous préférez identité d’appareil toocreate hello par programmation, lire la section correspondante de hello Bonjour [connectez votre concentrateur de IoT tooyour périphérique à l’aide de Java](iot-hub-java-java-getstarted.md#create-a-device-identity) l’article.</span><span class="sxs-lookup"><span data-stu-id="42b68-133">If you prefer toocreate hello device identity programmatically, read hello corresponding section in hello [Connect your device tooyour IoT hub using Java](iot-hub-java-java-getstarted.md#create-a-device-identity) article.</span></span> <span data-ttu-id="42b68-134">Vous pouvez également utiliser hello [iothub-explorer](https://github.com/Azure/iothub-explorer) outil tooadd un IoT hub de périphérique tooyour.</span><span class="sxs-lookup"><span data-stu-id="42b68-134">You can also use hello [iothub-explorer](https://github.com/Azure/iothub-explorer) tool tooadd a device tooyour IoT hub.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="42b68-135">Créer l’application de service hello</span><span class="sxs-lookup"><span data-stu-id="42b68-135">Create hello service app</span></span>

<span data-ttu-id="42b68-136">Dans cette section, vous créez une application console Java qui utilise des travaux pour :</span><span class="sxs-lookup"><span data-stu-id="42b68-136">In this section, you create a Java console app that uses jobs to:</span></span>

* <span data-ttu-id="42b68-137">Appelez hello **lockDoor** méthode directe sur plusieurs appareils.</span><span class="sxs-lookup"><span data-stu-id="42b68-137">Call hello **lockDoor** direct method on multiple devices.</span></span>
* <span data-ttu-id="42b68-138">Envoyer les propriétés souhaitées toomultiple périphériques.</span><span class="sxs-lookup"><span data-stu-id="42b68-138">Send desired properties toomultiple devices.</span></span>

<span data-ttu-id="42b68-139">application hello toocreate :</span><span class="sxs-lookup"><span data-stu-id="42b68-139">toocreate hello app:</span></span>

1. <span data-ttu-id="42b68-140">Sur votre ordinateur de développement, créez un dossier vide nommé `iot-java-schedule-jobs`.</span><span class="sxs-lookup"><span data-stu-id="42b68-140">On your development machine, create an empty folder called `iot-java-schedule-jobs`.</span></span>

1. <span data-ttu-id="42b68-141">Bonjour `iot-java-schedule-jobs` dossier, créez un projet Maven appelé **planifier des travaux** à l’aide de hello, la commande suivante à l’invite suivante.</span><span class="sxs-lookup"><span data-stu-id="42b68-141">In hello `iot-java-schedule-jobs` folder, create a Maven project called **schedule-jobs** using hello following command at your command prompt.</span></span> <span data-ttu-id="42b68-142">Il s’agit d’une commande unique et longue :</span><span class="sxs-lookup"><span data-stu-id="42b68-142">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=schedule-jobs -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="42b68-143">À l’invite de commandes, accédez à toohello `schedule-jobs` dossier.</span><span class="sxs-lookup"><span data-stu-id="42b68-143">At your command prompt, navigate toohello `schedule-jobs` folder.</span></span>

1. <span data-ttu-id="42b68-144">À l’aide d’un éditeur de texte, ouvrez hello `pom.xml` fichier Bonjour `schedule-jobs` dossier et ajoutez hello suivant dépendance toohello **dépendances** nœud.</span><span class="sxs-lookup"><span data-stu-id="42b68-144">Using a text editor, open hello `pom.xml` file in hello `schedule-jobs` folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="42b68-145">Cette dépendance vous permet de toouse hello **iot-service-client** package dans toocommunicate de votre application avec votre IoT hub :</span><span class="sxs-lookup"><span data-stu-id="42b68-145">This dependency enables you toouse hello **iot-service-client** package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="42b68-146">Vous pouvez vérifier pour la version la plus récente de hello **iot-service-client** à l’aide de [recherche de Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="42b68-146">You can check for hello latest version of **iot-service-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="42b68-147">Ajoutez hello suivant **générer** nœud après hello **dépendances** nœud.</span><span class="sxs-lookup"><span data-stu-id="42b68-147">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="42b68-148">Cette configuration indique d’application hello toobuild 1,8 Maven toouse Java :</span><span class="sxs-lookup"><span data-stu-id="42b68-148">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="42b68-149">Enregistrez et fermez hello `pom.xml` fichier.</span><span class="sxs-lookup"><span data-stu-id="42b68-149">Save and close hello `pom.xml` file.</span></span>

1. <span data-ttu-id="42b68-150">À l’aide d’un éditeur de texte, ouvrez hello `schedule-jobs\src\main\java\com\mycompany\app\App.java` fichier.</span><span class="sxs-lookup"><span data-stu-id="42b68-150">Using a text editor, open hello `schedule-jobs\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="42b68-151">Ajoutez hello suivant **importer** fichier de toohello instructions :</span><span class="sxs-lookup"><span data-stu-id="42b68-151">Add hello following **import** statements toohello file:</span></span>

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

1. <span data-ttu-id="42b68-152">Ajouter hello suivant des variables de niveau classe toohello **application** classe.</span><span class="sxs-lookup"><span data-stu-id="42b68-152">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="42b68-153">Remplacez `{youriothubconnectionstring}` avec votre chaîne de connexion de hub IoT noté dans hello *créez un IoT Hub* section :</span><span class="sxs-lookup"><span data-stu-id="42b68-153">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in hello *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    // How long hello job is permitted toorun without
    // completing its work on hello set of devices
    private static final long maxExecutionTimeInSeconds = 30;
    ```

1. <span data-ttu-id="42b68-154">Ajouter hello suivant de méthode toohello **application** classe tooschedule un Bonjour tooupdate de travail **construction** et **Floor** propriétés de deux conteneurs de périphérique hello souhaitée :</span><span class="sxs-lookup"><span data-stu-id="42b68-154">Add hello following method toohello **App** class tooschedule a job tooupdate hello **Building** and **Floor** desired properties in hello device twin:</span></span>

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

1. <span data-ttu-id="42b68-155">tooschedule un Bonjour toocall de travail **lockDoor** (méthode), ajouter hello suivant de méthode toohello **application** classe :</span><span class="sxs-lookup"><span data-stu-id="42b68-155">tooschedule a job toocall hello **lockDoor** method, add hello following method toohello **App** class:</span></span>

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

1. <span data-ttu-id="42b68-156">toomonitor un travail, ajouter hello suivant de méthode toohello **application** classe :</span><span class="sxs-lookup"><span data-stu-id="42b68-156">toomonitor a job, add hello following method toohello **App** class:</span></span>

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

1. <span data-ttu-id="42b68-157">tooquery pour plus d’informations hello de travaux hello vous avez exécuté, ajoutez hello suivant de méthode :</span><span class="sxs-lookup"><span data-stu-id="42b68-157">tooquery for hello details of hello jobs you ran, add hello following method:</span></span>

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

1. <span data-ttu-id="42b68-158">Hello de mise à jour **principal** suivant de méthode signature tooinclude hello `throws` clause :</span><span class="sxs-lookup"><span data-stu-id="42b68-158">Update hello **main** method signature tooinclude hello following `throws` clause:</span></span>

    ```java
    public static void main( String[] args ) throws Exception
    ```

1. <span data-ttu-id="42b68-159">toorun et le moniteur de deux travaux ajouter de manière séquentielle, hello suivant code toohello **principal** méthode :</span><span class="sxs-lookup"><span data-stu-id="42b68-159">toorun and monitor two jobs sequentially, add hello following code toohello **main** method:</span></span>

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

1. <span data-ttu-id="42b68-160">Enregistrez et fermez hello `schedule-jobs\src\main\java\com\mycompany\app\App.java` fichier</span><span class="sxs-lookup"><span data-stu-id="42b68-160">Save and close hello `schedule-jobs\src\main\java\com\mycompany\app\App.java` file</span></span>

1. <span data-ttu-id="42b68-161">Build hello **planifier des travaux** application et corrigez les erreurs.</span><span class="sxs-lookup"><span data-stu-id="42b68-161">Build hello **schedule-jobs** app and correct any errors.</span></span> <span data-ttu-id="42b68-162">À l’invite de commandes, accédez à toohello `schedule-jobs` dossier et exécution hello commande suivante :</span><span class="sxs-lookup"><span data-stu-id="42b68-162">At your command prompt, navigate toohello `schedule-jobs` folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a><span data-ttu-id="42b68-163">Créer une application d’appareil</span><span class="sxs-lookup"><span data-stu-id="42b68-163">Create a device app</span></span>

<span data-ttu-id="42b68-164">Dans cette section, vous créer une application de console Java qui gère hello envoyées à partir de l’appel de méthode directe hello IoT Hub et met en œuvre de propriétés souhaitées.</span><span class="sxs-lookup"><span data-stu-id="42b68-164">In this section, you create a Java console app that handles hello desired properties sent from IoT Hub and implements hello direct method call.</span></span>

1. <span data-ttu-id="42b68-165">Bonjour `iot-java-schedule-jobs` dossier, créez un projet Maven appelé **appareil simulé** à l’aide de hello, la commande suivante à l’invite suivante.</span><span class="sxs-lookup"><span data-stu-id="42b68-165">In hello `iot-java-schedule-jobs` folder, create a Maven project called **simulated-device** using hello following command at your command prompt.</span></span> <span data-ttu-id="42b68-166">Il s’agit d’une commande unique et longue :</span><span class="sxs-lookup"><span data-stu-id="42b68-166">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="42b68-167">À l’invite de commandes, accédez à toohello `simulated-device` dossier.</span><span class="sxs-lookup"><span data-stu-id="42b68-167">At your command prompt, navigate toohello `simulated-device` folder.</span></span>

1. <span data-ttu-id="42b68-168">À l’aide d’un éditeur de texte, ouvrez hello `pom.xml` fichier Bonjour `simulated-device` dossier et ajoutez hello suivant dépendances toohello **dépendances** nœud.</span><span class="sxs-lookup"><span data-stu-id="42b68-168">Using a text editor, open hello `pom.xml` file in hello `simulated-device` folder and add hello following dependencies toohello **dependencies** node.</span></span> <span data-ttu-id="42b68-169">Cette dépendance vous permet de toouse hello **client de périphérique iot** package dans toocommunicate de votre application avec votre IoT hub :</span><span class="sxs-lookup"><span data-stu-id="42b68-169">This dependency enables you toouse hello **iot-device-client** package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="42b68-170">Vous pouvez vérifier pour la version la plus récente de hello **client de périphérique iot** à l’aide de [recherche de Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="42b68-170">You can check for hello latest version of **iot-device-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="42b68-171">Ajoutez hello suivant **générer** nœud après hello **dépendances** nœud.</span><span class="sxs-lookup"><span data-stu-id="42b68-171">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="42b68-172">Cette configuration indique d’application hello toobuild 1,8 Maven toouse Java :</span><span class="sxs-lookup"><span data-stu-id="42b68-172">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="42b68-173">Enregistrez et fermez hello `pom.xml` fichier.</span><span class="sxs-lookup"><span data-stu-id="42b68-173">Save and close hello `pom.xml` file.</span></span>

1. <span data-ttu-id="42b68-174">À l’aide d’un éditeur de texte, ouvrez hello `simulated-device\src\main\java\com\mycompany\app\App.java` fichier.</span><span class="sxs-lookup"><span data-stu-id="42b68-174">Using a text editor, open hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="42b68-175">Ajoutez hello suivant **importer** fichier de toohello instructions :</span><span class="sxs-lookup"><span data-stu-id="42b68-175">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. <span data-ttu-id="42b68-176">Ajouter hello suivant des variables de niveau classe toohello **application** classe.</span><span class="sxs-lookup"><span data-stu-id="42b68-176">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="42b68-177">En remplaçant `{youriothubname}` avec votre nom de hub IoT, et `{yourdevicekey}` avec la valeur de clé de périphérique hello générées dans hello *créer une identité d’appareil* section :</span><span class="sxs-lookup"><span data-stu-id="42b68-177">Replacing `{youriothubname}` with your IoT hub name, and `{yourdevicekey}` with hello device key value you generated in hello *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    <span data-ttu-id="42b68-178">Cet exemple d’application utilise hello **protocole** variable lorsqu’il instancie une **DeviceClient** objet.</span><span class="sxs-lookup"><span data-stu-id="42b68-178">This sample app uses hello **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="42b68-179">Actuellement, toouse appareil double fonctionnalités vous devez utiliser le protocole MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="42b68-179">Currently, toouse device twin features you must use hello MQTT protocol.</span></span>

1. <span data-ttu-id="42b68-180">tooprint appareil double notifications toohello de la console, ajoutez hello imbriqués classe toohello **application** classe :</span><span class="sxs-lookup"><span data-stu-id="42b68-180">tooprint device twin notifications toohello console, add hello following nested class toohello **App** class:</span></span>

    ```java
    // Handler for device twin operation notifications from IoT Hub
    protected static class DeviceTwinStatusCallBack implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toodevice twin operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="42b68-181">tooprint directe toohello des notifications de méthode de la console, ajoutez hello imbriqués classe toohello **application** classe :</span><span class="sxs-lookup"><span data-stu-id="42b68-181">tooprint direct method notifications toohello console, add hello following nested class toohello **App** class:</span></span>

    ```java
    // Handler for direct method notifications from IoT Hub
    protected static class DirectMethodStatusCallback implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toodirect method operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="42b68-182">toohandle des appels de méthode directe à partir de IoT Hub, ajoutez des éléments suivants de hello imbriqués classe toohello **application** classe :</span><span class="sxs-lookup"><span data-stu-id="42b68-182">toohandle direct method calls from IoT Hub, add hello following nested class toohello **App** class:</span></span>

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

1. <span data-ttu-id="42b68-183">Hello de mise à jour **principal** suivant de méthode signature tooinclude hello `throws` clause :</span><span class="sxs-lookup"><span data-stu-id="42b68-183">Update hello **main** method signature tooinclude hello following `throws` clause:</span></span>

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException
    ```

1. <span data-ttu-id="42b68-184">Ajouter hello suivant code toohello **principal** méthode :</span><span class="sxs-lookup"><span data-stu-id="42b68-184">Add hello following code toohello **main** method to:</span></span>
    * <span data-ttu-id="42b68-185">Créer un toocommunicate de client de périphérique avec IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="42b68-185">Create a device client toocommunicate with IoT Hub.</span></span>
    * <span data-ttu-id="42b68-186">Créer un **périphérique** toostore hello appareil deux propriétés de l’objet.</span><span class="sxs-lookup"><span data-stu-id="42b68-186">Create a **Device** object toostore hello device twin properties.</span></span>

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

1. <span data-ttu-id="42b68-187">services de toostart hello appareil client, ajoutez hello suivant code toohello **principal** méthode :</span><span class="sxs-lookup"><span data-stu-id="42b68-187">toostart hello device client services, add hello following code toohello **main** method:</span></span>

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

1. <span data-ttu-id="42b68-188">toowait pour hello de hello utilisateur toopress **entrée** clé avant l’arrêt, ajouter hello suivant fin toohello de code Hello **principal** méthode :</span><span class="sxs-lookup"><span data-stu-id="42b68-188">toowait for hello user toopress hello **Enter** key before shutting down, add hello following code toohello end of hello **main** method:</span></span>

    ```java
    // Close hello app
    System.out.println("Press any key tooexit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    dataCollector.clean();
    client.closeNow();
    scanner.close();
    ```

1. <span data-ttu-id="42b68-189">Enregistrez et fermez hello `simulated-device\src\main\java\com\mycompany\app\App.java` fichier.</span><span class="sxs-lookup"><span data-stu-id="42b68-189">Save and close hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="42b68-190">Build hello **appareil simulé** application et corrigez les erreurs.</span><span class="sxs-lookup"><span data-stu-id="42b68-190">Build hello **simulated-device** app and correct any errors.</span></span> <span data-ttu-id="42b68-191">À l’invite de commandes, accédez à toohello `simulated-device` dossier et exécution hello commande suivante :</span><span class="sxs-lookup"><span data-stu-id="42b68-191">At your command prompt, navigate toohello `simulated-device` folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a><span data-ttu-id="42b68-192">Exécuter des applications de hello</span><span class="sxs-lookup"><span data-stu-id="42b68-192">Run hello apps</span></span>

<span data-ttu-id="42b68-193">Vous êtes maintenant prêt toorun les applications de console hello.</span><span class="sxs-lookup"><span data-stu-id="42b68-193">You are now ready toorun hello console apps.</span></span>

1. <span data-ttu-id="42b68-194">À l’invite de commande Bonjour `simulated-device` dossier, exécutez hello après application d’appareil commande toostart hello l’écoute des modifications de propriété de votre choix et des appels de méthode directe :</span><span class="sxs-lookup"><span data-stu-id="42b68-194">At a command prompt in hello `simulated-device` folder, run hello following command toostart hello device app listening for desired property changes and direct method calls:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![client de périphérique Hello démarre](media/iot-hub-java-java-schedule-jobs/device-app-1.png)

1. <span data-ttu-id="42b68-196">À l’invite de commande Bonjour `schedule-jobs` dossier, exécutez hello suivant commande toorun hello **planifier des travaux** toorun deux travaux d’application de service.</span><span class="sxs-lookup"><span data-stu-id="42b68-196">At a command prompt in hello `schedule-jobs` folder, run hello following command toorun hello **schedule-jobs** service app toorun two jobs.</span></span> <span data-ttu-id="42b68-197">Hello définit tout d’abord les valeurs de propriété hello souhaité, appels de deuxième hello hello méthode directe :</span><span class="sxs-lookup"><span data-stu-id="42b68-197">hello first sets hello desired property values, hello second calls hello direct method:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![L’application de service Java IoT Hub crée deux travaux](media/iot-hub-java-java-schedule-jobs/service-app-1.png)

1. <span data-ttu-id="42b68-199">application d’appareil Hello gère la modification de la propriété hello souhaitée et l’appel de méthode directe hello :</span><span class="sxs-lookup"><span data-stu-id="42b68-199">hello device app handles hello desired property change and hello direct method call:</span></span>

    ![client de périphérique Hello répond toohello modifications](media/iot-hub-java-java-schedule-jobs/device-app-2.png)

## <a name="next-steps"></a><span data-ttu-id="42b68-201">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="42b68-201">Next steps</span></span>

<span data-ttu-id="42b68-202">Dans ce didacticiel, vous configuré un IoT hub Bonjour portail Azure et ensuite créé une identité d’appareil dans le Registre des identités de hello IoT hub.</span><span class="sxs-lookup"><span data-stu-id="42b68-202">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="42b68-203">Vous avez créé une application back-end toorun deux tâches.</span><span class="sxs-lookup"><span data-stu-id="42b68-203">You created a back-end app toorun two jobs.</span></span> <span data-ttu-id="42b68-204">tâche Hello définie les valeurs de propriété de votre choix et hello deuxième travail appelé une méthode directe.</span><span class="sxs-lookup"><span data-stu-id="42b68-204">hello first job set desired property values, and hello second job called a direct method.</span></span>

<span data-ttu-id="42b68-205">Hello utilisation suivant comment les ressources toolearn à :</span><span class="sxs-lookup"><span data-stu-id="42b68-205">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="42b68-206">Envoyer la télémétrie des appareils avec hello [prise en main IoT Hub](iot-hub-java-java-getstarted.md) didacticiel.</span><span class="sxs-lookup"><span data-stu-id="42b68-206">Send telemetry from devices with hello [Get started with IoT Hub](iot-hub-java-java-getstarted.md) tutorial.</span></span>
* <span data-ttu-id="42b68-207">Contrôler les périphériques de manière interactive (telles que l’activation sur un ventilateur à partir d’une application contrôlée par l’utilisateur) avec hello [utiliser les méthodes directes](iot-hub-java-java-direct-methods.md) didacticiel.</span><span class="sxs-lookup"><span data-stu-id="42b68-207">Control devices interactively (such as turning on a fan from a user-controlled app) with hello [Use direct methods](iot-hub-java-java-direct-methods.md) tutorial.</span></span>
