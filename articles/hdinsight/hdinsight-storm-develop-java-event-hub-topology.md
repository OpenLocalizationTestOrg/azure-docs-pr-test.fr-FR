---
title: "les événements de concentrateurs d’événements avec Storm sur HDInsight à l’aide de Java aaaProcess | Documents Microsoft"
description: "Découvrez comment tooprocess données concentrateurs d’événements avec une topologie Java Storm créé avec Maven."
services: hdinsight,notification hubs
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 453fa7b0-c8a6-413e-8747-3ac3b71bed86
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/13/2017
ms.author: larryfr
ms.openlocfilehash: 6506f5bc8f6ab0e29350c071a3f84433382038e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-java"></a><span data-ttu-id="4981d-103">Traitement des événements Azure Event Hubs avec Storm sur HDInsight (Java)</span><span class="sxs-lookup"><span data-stu-id="4981d-103">Process events from Azure Event Hubs with Storm on HDInsight (Java)</span></span>

<span data-ttu-id="4981d-104">Découvrez comment toouse Azure Event Hubs avec Storm sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4981d-104">Learn how toouse Azure Event Hubs with Storm on HDInsight.</span></span> <span data-ttu-id="4981d-105">Cet exemple utilise des composants basés sur Java tooread et écrire les données dans Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="4981d-105">This example uses Java-based components tooread and write data in Azure Event Hubs.</span></span>

<span data-ttu-id="4981d-106">Les concentrateurs d’événements Azure vous permet de tooprocess de gros volumes de données à partir de sites Web, des applications et des périphériques.</span><span class="sxs-lookup"><span data-stu-id="4981d-106">Azure Event Hubs allows you tooprocess massive amounts of data from websites, apps, and devices.</span></span> <span data-ttu-id="4981d-107">Hello bec de concentrateur d’événements rend facile toouse Apache renverser sur HDInsight tooanalyze ces données en temps réel.</span><span class="sxs-lookup"><span data-stu-id="4981d-107">hello Event Hub spout makes it easy toouse Apache Storm on HDInsight tooanalyze this data in real time.</span></span> <span data-ttu-id="4981d-108">Vous pouvez également écrire des données tooEvent concentrateurs à partir de Storm à l’aide de hello boulon de concentrateurs d’événements.</span><span class="sxs-lookup"><span data-stu-id="4981d-108">You can also write data tooEvent Hubs from Storm by using hello Event Hubs bolt.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4981d-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="4981d-109">Prerequisites</span></span>

* <span data-ttu-id="4981d-110">Un cluster Apache Storm sur HDInsight version 3.6.</span><span class="sxs-lookup"><span data-stu-id="4981d-110">An Apache Storm on HDInsight cluster version 3.6.</span></span> <span data-ttu-id="4981d-111">Pour plus d’informations, voir [Prise en main de Storm sur HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="4981d-111">For more information, see [Get started with Storm on HDInsight cluster](hdinsight-apache-storm-tutorial-get-started-linux.md).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="4981d-112">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="4981d-112">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="4981d-113">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="4981d-113">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="4981d-114">Un [hub d’événements Azure](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="4981d-114">An [Azure Event Hub](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

* <span data-ttu-id="4981d-115">[Kit de développeur Java (JDK) Oracle version 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) ou un équivalent, par exemple, [OpenJDK](http://openjdk.java.net/).</span><span class="sxs-lookup"><span data-stu-id="4981d-115">[Oracle Java Developer Kit (JDK) version 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) or equivalent, such as [OpenJDK](http://openjdk.java.net/).</span></span>

* <span data-ttu-id="4981d-116">[Maven](https://maven.apache.org/download.cgi) : Maven est un système de génération de projet pour les projets Java.</span><span class="sxs-lookup"><span data-stu-id="4981d-116">[Maven](https://maven.apache.org/download.cgi): Maven is a project build system for Java projects.</span></span>

* <span data-ttu-id="4981d-117">Un éditeur de texte ou un environnement de développement intégré (IDE).</span><span class="sxs-lookup"><span data-stu-id="4981d-117">A text editor or integrated development environment (IDE).</span></span>

    > [!NOTE]
    > <span data-ttu-id="4981d-118">Votre éditeur ou IDE peut avoir des fonctionnalités spécifiques pour l’utilisation avec Maven, qui ne sont pas traitées dans ce document.</span><span class="sxs-lookup"><span data-stu-id="4981d-118">Your editor or IDE may have specific functionality for working with Maven that is not addressed in this document.</span></span> <span data-ttu-id="4981d-119">Pour plus d’informations sur les fonctionnalités de hello de votre environnement d’édition, consultez la documentation hello pour produit hello que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="4981d-119">For information about hello capabilities of your editing environment, see hello documentation for hello product you are using.</span></span>

    * <span data-ttu-id="4981d-120">Un client SSH.</span><span class="sxs-lookup"><span data-stu-id="4981d-120">An SSH client.</span></span> <span data-ttu-id="4981d-121">Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="4981d-121">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="4981d-122">Hello `ssh` et `scp` commandes.</span><span class="sxs-lookup"><span data-stu-id="4981d-122">hello `ssh` and `scp` commands.</span></span> <span data-ttu-id="4981d-123">Il s’agit de cluster de HDInsight utilisé toocopy fichiers toohello.</span><span class="sxs-lookup"><span data-stu-id="4981d-123">These are used toocopy files toohello HDInsight cluster.</span></span> <span data-ttu-id="4981d-124">Sous Windows, vous pouvez les obtenir via Bash dans Windows 10.</span><span class="sxs-lookup"><span data-stu-id="4981d-124">On Windows, you can get these through Bash on Windows 10.</span></span>

## <a name="understanding-hello-example"></a><span data-ttu-id="4981d-125">Exemple hello de présentation</span><span class="sxs-lookup"><span data-stu-id="4981d-125">Understanding hello example</span></span>

<span data-ttu-id="4981d-126">Hello [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) exemple contient deux topologies :</span><span class="sxs-lookup"><span data-stu-id="4981d-126">hello [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) example contains two topologies:</span></span>

<span data-ttu-id="4981d-127">Hello `resources/writer.yaml` topologie écrit des données aléatoires tooan concentrateur d’événements Azure.</span><span class="sxs-lookup"><span data-stu-id="4981d-127">hello `resources/writer.yaml` topology writes random data tooan Azure Event Hub.</span></span> <span data-ttu-id="4981d-128">les données de salutation sont générées par hello `DeviceSpout` composant, et est une valeur de l’appareil et un ID de périphérique aléatoire.</span><span class="sxs-lookup"><span data-stu-id="4981d-128">hello data is generated by hello `DeviceSpout` component, and is a random device ID and device value.</span></span> <span data-ttu-id="4981d-129">Ainsi, elles simulent certains matériels qui émettent un ID de chaîne et une valeur numérique.</span><span class="sxs-lookup"><span data-stu-id="4981d-129">So it's simulating some hardware that emits a string ID and a numeric value.</span></span>

<span data-ttu-id="4981d-130">Les trois `resources/reader.yaml` topologie lit des données à partir du concentrateur d’événements (écrites par EventHubWriter, les données hello) analyse les données JSON de hello et ouvre une session hello `deviceId` et `deviceValue` données.</span><span class="sxs-lookup"><span data-stu-id="4981d-130">Thee `resources/reader.yaml` topology reads data from Event Hub (hello data written by EventHubWriter,) parses hello JSON data, and then logs hello `deviceId` and `deviceValue` data.</span></span>

<span data-ttu-id="4981d-131">les données de salutation sont mise en forme comme un document JSON avant d’être écrite tooEvent Hub et lors de la lecture par le lecteur de hello il est analysé en dehors de JSON et dans des tuples.</span><span class="sxs-lookup"><span data-stu-id="4981d-131">hello data is formatted as a JSON document before it is written tooEvent Hub, and when read by hello reader it is parsed out of JSON and into tuples.</span></span> <span data-ttu-id="4981d-132">format JSON Hello est comme suit :</span><span class="sxs-lookup"><span data-stu-id="4981d-132">hello JSON format is as follows:</span></span>

    { "deviceId": "unique identifier", "deviceValue": some value }

### <a name="project-configuration"></a><span data-ttu-id="4981d-133">Configuration du projet</span><span class="sxs-lookup"><span data-stu-id="4981d-133">Project configuration</span></span>

<span data-ttu-id="4981d-134">Hello `POM.xml` fichier contient des informations de configuration pour ce projet Maven.</span><span class="sxs-lookup"><span data-stu-id="4981d-134">hello `POM.xml` file contains configuration information for this Maven project.</span></span> <span data-ttu-id="4981d-135">intéressantes Hello sont :</span><span class="sxs-lookup"><span data-stu-id="4981d-135">hello interesting pieces are:</span></span>

#### <a name="event-hub-components"></a><span data-ttu-id="4981d-136">Composants Event Hub</span><span class="sxs-lookup"><span data-stu-id="4981d-136">Event Hub components</span></span>

<span data-ttu-id="4981d-137">composant de Hello qui lit et écrit les concentrateurs d’événements tooAzure se trouve dans hello [HDInsight référentiel](https://github.com/hdinsight/mvn-rep).</span><span class="sxs-lookup"><span data-stu-id="4981d-137">hello component that reads and writes tooAzure Event Hubs is located in hello [HDInsight repository](https://github.com/hdinsight/mvn-rep).</span></span> <span data-ttu-id="4981d-138">Hello suivants sections Bonjour `POM.xml` composants hello du chargement de fichiers à partir de ce référentiel</span><span class="sxs-lookup"><span data-stu-id="4981d-138">hello following sections in hello `POM.xml` file load hello components from this repository</span></span>

```xml
<repositories>
    <repository>
        <id>hdinsight-examples</id>
        <url>http://raw.github.com/hdinsight/mvn-repo/master</url>
    </repository>
</repositories>
```

#### <a name="hello-eventhubs-storm-spout-dependency"></a><span data-ttu-id="4981d-139">Hello bec de Storm EventHubs de dépendance</span><span class="sxs-lookup"><span data-stu-id="4981d-139">hello EventHubs Storm Spout dependency</span></span>

```xml
<dependency>
    <groupId>com.microsoft</groupId>
    <artifactId>eventhubs</artifactId>
    <version>${storm.eventhub.version}</version>
</dependency>
```

<span data-ttu-id="4981d-140">Ce code xml définit une dépendance pour le package hello eventhubs, qui contient à la fois un bec pour lire à partir de concentrateurs d’événements et un éclair pour l’écriture de tooit.</span><span class="sxs-lookup"><span data-stu-id="4981d-140">This xml defines a dependency for hello eventhubs package, which contains both a spout for reading from Event Hubs, and a bolt for writing tooit.</span></span>

```xml
</source>
    <target>1.8</target>
    </configuration>
</plugin>
```

<span data-ttu-id="4981d-141">Ce code xml configure la sortie du toogenerate hello projet Java 8, qui est utilisé par HDInsight 3.5 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="4981d-141">This xml configures hello project toogenerate output for Java 8, which is used by HDInsight 3.5 or higher.</span></span>

#### <a name="hello-maven-shade-plugin"></a><span data-ttu-id="4981d-142">Hello maven-ton plug-in</span><span class="sxs-lookup"><span data-stu-id="4981d-142">hello maven-shade-plugin</span></span>

```xml
<!-- build an uber jar -->
<plugin>
<groupId>org.apache.maven.plugins</groupId>
<artifactId>maven-shade-plugin</artifactId>
<version>2.3</version>
<configuration>
    <transformers>
    <!-- Keep us from getting a can't overwrite file error -->
    <transformer implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer"/>
    <transformer implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer"/>
    </transformers>
    <!-- Keep us from getting a bad signature error -->
    <filters>
    <filter>
        <artifact>*:*</artifact>
        <excludes>
            <exclude>META-INF/*.SF</exclude>
            <exclude>META-INF/*.DSA</exclude>
            <exclude>META-INF/*.RSA</exclude>
        </excludes>
    </filter>
    </filters>
</configuration>
<executions>
    <execution>
    <phase>package</phase>
    <goals>
        <goal>shade</goal>
    </goals>
    </execution>
</executions>
</plugin>
```

<span data-ttu-id="4981d-143">Ce code xml configure la sortie de hello hello solution toopackage dans un fichier jar générale.</span><span class="sxs-lookup"><span data-stu-id="4981d-143">This xml configures hello solution toopackage hello output into an uber jar.</span></span> <span data-ttu-id="4981d-144">jar de Hello contient le code de projet hello et les dépendances requises.</span><span class="sxs-lookup"><span data-stu-id="4981d-144">hello jar contains both hello project code and required dependencies.</span></span> <span data-ttu-id="4981d-145">Il est également utilisé pour :</span><span class="sxs-lookup"><span data-stu-id="4981d-145">It is also used to:</span></span>

* <span data-ttu-id="4981d-146">Renommez les fichiers de licence pour les dépendances de hello.</span><span class="sxs-lookup"><span data-stu-id="4981d-146">Rename license files for hello dependencies.</span></span>
* <span data-ttu-id="4981d-147">Exclure les sécurités/signatures.</span><span class="sxs-lookup"><span data-stu-id="4981d-147">Exclude security/signatures.</span></span>
* <span data-ttu-id="4981d-148">Vérifiez que plusieurs implémentations de hello même interface sont fusionnées en une seule entrée.</span><span class="sxs-lookup"><span data-stu-id="4981d-148">Ensure that multiple implementations of hello same interface are merged into one entry.</span></span>

<span data-ttu-id="4981d-149">Ces paramètres de configuration évitent les erreurs au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="4981d-149">These configuration settings prevent errors at runtime.</span></span>

#### <a name="topology-definitions"></a><span data-ttu-id="4981d-150">Définitions de topologie</span><span class="sxs-lookup"><span data-stu-id="4981d-150">Topology definitions</span></span>

<span data-ttu-id="4981d-151">Cet exemple utilise hello [Flux](https://storm.apache.org/releases/1.1.0/flux.html) framework.</span><span class="sxs-lookup"><span data-stu-id="4981d-151">This example uses hello [Flux](https://storm.apache.org/releases/1.1.0/flux.html) framework.</span></span> <span data-ttu-id="4981d-152">Cette infrastructure utilise les topologies hello YAML toodefine.</span><span class="sxs-lookup"><span data-stu-id="4981d-152">This framework uses YAML toodefine hello topologies.</span></span> <span data-ttu-id="4981d-153">Hello le principal avantage est que vous n’êtes pas dur codage topologie hello dans le code Java.</span><span class="sxs-lookup"><span data-stu-id="4981d-153">hello primary benefit is that you aren't hard coding hello topology in Java code.</span></span> <span data-ttu-id="4981d-154">Définition de hello étant YAML, vous pouvez le modifier avant de soumettre la topologie de hello, sans avoir à toorecompile tous les éléments.</span><span class="sxs-lookup"><span data-stu-id="4981d-154">Since hello definition is YAML, you can change it before submitting hello topology, without having toorecompile everything.</span></span>

<span data-ttu-id="4981d-155">__writer.yaml__ :</span><span class="sxs-lookup"><span data-stu-id="4981d-155">__writer.yaml__:</span></span>

```yaml
---
# Topology that reads from Event Hubs
name: "eventhubwriter"

components:
  # Configure hello Event Hub spout
  - id: "eventhubbolt-config"
    className: "org.apache.storm.eventhubs.bolt.EventHubBoltConfig"
    constructorArgs:
      # These are populated from hello .properties file when hello topology is started
      - "${eventhub.write.policy.name}"
      - "${eventhub.write.policy.key}"
      - "${eventhub.namespace}"
      - "servicebus.windows.net"
      - "${eventhub.name}"

spouts:
  - id: "device-emulator-spout"
    className: "com.microsoft.example.DeviceSpout"
    parallelism: ${eventhub.partitions}

bolts:
  - id: "eventhub-bolt"
    className: "org.apache.storm.eventhubs.bolt.EventHubBolt"
    constructorArgs:
      - ref: "eventhubbolt-config" # config declared in components section
    # parallelism hint. This should be hello same as hello number of partitions for your Event Hub, so we read it from hello dev.properties file passed at run time.
    parallelism: ${eventhub.partitions}

  # Log information
  - id: "log-bolt"
    className: "org.apache.storm.flux.wrappers.bolts.LogInfoBolt"
    parallelism: 1

# How data flows through hello components
streams:
  - name: "spout -> eventhub" # just a string used for logging
    from: "device-emulator-spout"
    to: "eventhub-bolt"
    grouping:
        type: SHUFFLE

  - name: "spout -> logger"
    from: "device-emulator-spout"
    to: "log-bolt"
    grouping:
        type: SHUFFLE
```

<span data-ttu-id="4981d-156">__reader.yaml__ :</span><span class="sxs-lookup"><span data-stu-id="4981d-156">__reader.yaml__:</span></span>

```yaml
---
# Topology that reads from Event Hubs
name: "eventhubreader"

components:
  # Configure hello Event Hub spout
  - id: "eventhubspout-config"
    className: "org.apache.storm.eventhubs.spout.EventHubSpoutConfig"
    constructorArgs:
      # These are populated from hello .properties file when hello topology is started
      - "${eventhub.read.policy.name}"
      - "${eventhub.read.policy.key}"
      - "${eventhub.namespace}"
      - "${eventhub.name}"
      - ${eventhub.partitions}

spouts:
  - id: "eventhub-spout"
    className: "org.apache.storm.eventhubs.spout.EventHubSpout"
    constructorArgs:
      - ref: "eventhubspout-config" # config declared in components section
    # parallelism hint. This should be hello same as hello number of partitions for your Event Hub, so we read it from hello dev.properties file passed at run time.
    parallelism: ${eventhub.partitions}

bolts:
  # Log information
  - id: "log-bolt"
    className: "org.apache.storm.flux.wrappers.bolts.LogInfoBolt"
    parallelism: 1

  # Parses from JSON into tuples
  - id: "parser-bolt"
    className: "com.microsoft.example.ParserBolt"
    parallelism: ${eventhub.partitions}

# How data flows through hello components
streams:
  - name: "spout -> parser" # just a string used for logging
    from: "eventhub-spout"
    to: "parser-bolt"
    grouping:
        type: SHUFFLE

  - name: "parser -> log-bolt"
    from: "parser-bolt"
    to: "log-bolt"
    grouping:
        type: SHUFFLE
```

#### <a name="tell-hello-topology-about-event-hub"></a><span data-ttu-id="4981d-157">Topologie de hello dire de concentrateur d’événements</span><span class="sxs-lookup"><span data-stu-id="4981d-157">Tell hello topology about Event Hub</span></span>

<span data-ttu-id="4981d-158">Au moment de l’exécution, hello `dev.properties` fichier est utilisé toopass hello concentrateur d’événements configuration toohello topologie.</span><span class="sxs-lookup"><span data-stu-id="4981d-158">At run time, hello `dev.properties` file is used toopass hello Event Hub configuration toohello topology.</span></span> <span data-ttu-id="4981d-159">Hello exemple suivant est contenu par défaut de hello du fichier de hello :</span><span class="sxs-lookup"><span data-stu-id="4981d-159">hello following example is hello default contents of hello file:</span></span>

```yaml
eventhub.write.policy.name: writer
eventhub.write.policy.key: your_key_here
eventhub.read.policy.name: reader
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: storm
eventhub.partitions: 2
```

## <a name="configure-environment-variables"></a><span data-ttu-id="4981d-160">Configuration des variables d’environnement</span><span class="sxs-lookup"><span data-stu-id="4981d-160">Configure environment variables</span></span>

<span data-ttu-id="4981d-161">Hello variables d’environnement suivantes peuvent être définis lors de l’installation de Java et hello JDK sur votre station de travail de développement.</span><span class="sxs-lookup"><span data-stu-id="4981d-161">hello following environment variables may be set when you install Java and hello JDK on your development workstation.</span></span> <span data-ttu-id="4981d-162">Toutefois, vous devez vérifier qu’ils existent et qu’ils contiennent des valeurs correctes de hello pour votre système.</span><span class="sxs-lookup"><span data-stu-id="4981d-162">However, you should check that they exist and that they contain hello correct values for your system.</span></span>

* <span data-ttu-id="4981d-163">**JAVA_HOME** -doit pointer Active toohello où hello Java runtime environment (JRE) est installé.</span><span class="sxs-lookup"><span data-stu-id="4981d-163">**JAVA_HOME** - should point toohello directory where hello Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="4981d-164">Par exemple, dans une distribution Unix ou Linux, il doit avoir une valeur similaire trop`/usr/lib/jvm/java-7-oracle`.</span><span class="sxs-lookup"><span data-stu-id="4981d-164">For example, in a Unix or Linux distribution, it should have a value similar too`/usr/lib/jvm/java-7-oracle`.</span></span> <span data-ttu-id="4981d-165">Dans Windows, il aurait une valeur similaire trop`c:\Program Files (x86)\Java\jre1.7`</span><span class="sxs-lookup"><span data-stu-id="4981d-165">In Windows, it would have a value similar too`c:\Program Files (x86)\Java\jre1.7`</span></span>
* <span data-ttu-id="4981d-166">**Chemin d’accès** -doit contenir hello suivant des chemins d’accès :</span><span class="sxs-lookup"><span data-stu-id="4981d-166">**PATH** - should contain hello following paths:</span></span>

  * <span data-ttu-id="4981d-167">**JAVA_HOME** (ou les chemins d’accès équivalents hello)</span><span class="sxs-lookup"><span data-stu-id="4981d-167">**JAVA_HOME** (or hello equivalent path)</span></span>
  * <span data-ttu-id="4981d-168">**JAVA_HOME\bin** (ou les chemins d’accès équivalents hello)</span><span class="sxs-lookup"><span data-stu-id="4981d-168">**JAVA_HOME\bin** (or hello equivalent path)</span></span>
  * <span data-ttu-id="4981d-169">répertoire d’Hello installation Maven</span><span class="sxs-lookup"><span data-stu-id="4981d-169">hello directory where Maven is installed</span></span>

## <a name="configure-event-hub"></a><span data-ttu-id="4981d-170">Configuration du hub d'événements</span><span class="sxs-lookup"><span data-stu-id="4981d-170">Configure Event Hub</span></span>

<span data-ttu-id="4981d-171">Concentrateurs d’événements est la source de données de hello pour cet exemple.</span><span class="sxs-lookup"><span data-stu-id="4981d-171">Event Hubs is hello data source for this example.</span></span> <span data-ttu-id="4981d-172">Utilisez hello suivant les étapes toocreate un concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="4981d-172">Use hello following steps toocreate a Event Hub.</span></span>

1. <span data-ttu-id="4981d-173">À partir de hello [portail classique Azure](https://manage.windowsazure.com), sélectionnez **nouveau** > **Service Bus** > **concentrateur d’événements**  >  **Création personnalisée**.</span><span class="sxs-lookup"><span data-stu-id="4981d-173">From hello [Azure Classic Portal](https://manage.windowsazure.com), select **NEW** > **Service Bus** > **Event Hub** > **Custom Create**.</span></span>

2. <span data-ttu-id="4981d-174">Sur hello **ajouter un concentrateur d’événements** écran, entrez un **nom de Hub d’événements**.</span><span class="sxs-lookup"><span data-stu-id="4981d-174">On hello **Add a new Event Hub** screen, enter an **Event Hub Name**.</span></span> <span data-ttu-id="4981d-175">Sélectionnez hello **région** toocreate hello concentrateur, puis créer un espace de noms ou sélectionnez-en un existant.</span><span class="sxs-lookup"><span data-stu-id="4981d-175">Select hello **Region** toocreate hello hub in, and then create a namespace or select an existing one.</span></span> <span data-ttu-id="4981d-176">Enfin, cliquez sur hello **flèche** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="4981d-176">Finally, click hello **Arrow** toocontinue.</span></span>

    ![page 1 de l’assistant](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz1.png)

   > [!NOTE]
   > <span data-ttu-id="4981d-178">Sélectionnez hello même **emplacement** comme votre Storm sur HDInsight serveur tooreduce latence et les coûts.</span><span class="sxs-lookup"><span data-stu-id="4981d-178">Select hello same **Location** as your Storm on HDInsight server tooreduce latency and costs.</span></span>

3. <span data-ttu-id="4981d-179">Sur hello **concentrateur d’événements configurer** écran, entrez hello **nombre de Partition** et **rétention des messages** valeurs.</span><span class="sxs-lookup"><span data-stu-id="4981d-179">On hello **Configure Event Hub** screen, enter hello **Partition count** and **Message Retention** values.</span></span> <span data-ttu-id="4981d-180">Pour cet exemple, entrez 10 pour le nombre de partitions et 1 pour la conservation des messages.</span><span class="sxs-lookup"><span data-stu-id="4981d-180">For this example, use a partition count of 10 and a message retention of 1.</span></span> <span data-ttu-id="4981d-181">Notez le nombre de partitions hello, car vous avez besoin de cette valeur ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="4981d-181">Note hello partition count because you need this value later.</span></span>

    ![page 2 de l’assistant](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz2.png)

4. <span data-ttu-id="4981d-183">Une fois le concentrateur d’événements hello a été créé, sélectionnez hello espace de noms, sélectionnez **concentrateurs d’événements**, puis sélectionnez le concentrateur d’événements hello que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="4981d-183">After hello event hub has been created, select hello namespace, select **Event Hubs**, and then select hello event hub that you created earlier.</span></span>
5. <span data-ttu-id="4981d-184">Sélectionnez **configurer**, puis créez deux nouvelles stratégies d’accès à l’aide de hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="4981d-184">Select **Configure**, then create two new access policies by using hello following information:</span></span>

    <table>
    <tr><th><span data-ttu-id="4981d-185">Nom</span><span class="sxs-lookup"><span data-stu-id="4981d-185">Name</span></span></th><th><span data-ttu-id="4981d-186">Autorisations</span><span class="sxs-lookup"><span data-stu-id="4981d-186">Permissions</span></span></th></tr>
    <tr><td><span data-ttu-id="4981d-187">Writer</span><span class="sxs-lookup"><span data-stu-id="4981d-187">Writer</span></span></td><td><span data-ttu-id="4981d-188">Envoyer</span><span class="sxs-lookup"><span data-stu-id="4981d-188">Send</span></span></td></tr>
    <tr><td><span data-ttu-id="4981d-189">Lecteur</span><span class="sxs-lookup"><span data-stu-id="4981d-189">Reader</span></span></td><td><span data-ttu-id="4981d-190">Écouter</span><span class="sxs-lookup"><span data-stu-id="4981d-190">Listen</span></span></td></tr>
    </table>

    <span data-ttu-id="4981d-191">Après avoir créé des autorisations de hello, sélectionnez hello **enregistrer** icône bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="4981d-191">After You create hello permissions, select hello **Save** icon at hello bottom of hello page.</span></span> <span data-ttu-id="4981d-192">Ces stratégies d’accès partagé sont utilisé tooread et écrire tooEvent Hub.</span><span class="sxs-lookup"><span data-stu-id="4981d-192">These shared access policies are used tooread and write tooEvent Hub.</span></span>

    ![stratégies](./media/hdinsight-storm-develop-csharp-event-hub-topology/policy.png)

6. <span data-ttu-id="4981d-194">Après avoir enregistré les stratégies hello, utilisez hello **Générateur de clés d’accès partagé** bas hello de clé hello page tooretrieve hello hello **writer** et **lecteur** stratégies.</span><span class="sxs-lookup"><span data-stu-id="4981d-194">After you save hello policies, use hello **Shared access key generator** at hello bottom of hello page tooretrieve hello key for hello **writer** and **reader** policies.</span></span> <span data-ttu-id="4981d-195">Enregistrez ces clés.</span><span class="sxs-lookup"><span data-stu-id="4981d-195">Save these keys.</span></span>

## <a name="download-and-build-hello-project"></a><span data-ttu-id="4981d-196">Télécharger et générer le projet de hello</span><span class="sxs-lookup"><span data-stu-id="4981d-196">Download and build hello project</span></span>

1. <span data-ttu-id="4981d-197">Télécharger le projet de hello à partir de GitHub : [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="4981d-197">Download hello project from GitHub: [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub).</span></span> <span data-ttu-id="4981d-198">Vous pouvez télécharger le package hello sous la forme d’une archive zip, ou utilisez [git](https://git-scm.com/) tooclone le projet hello local.</span><span class="sxs-lookup"><span data-stu-id="4981d-198">You can either download hello package as a zip archive, or use [git](https://git-scm.com/) tooclone hello project locally.</span></span>

2. <span data-ttu-id="4981d-199">Modifier hello `dev.properties` fichier de configuration hello pour votre concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="4981d-199">Modify hello `dev.properties` file with hello configuration for your Event Hub.</span></span>

3. <span data-ttu-id="4981d-200">Utilisez hello suivant du projet de hello toobuild et le package :</span><span class="sxs-lookup"><span data-stu-id="4981d-200">Use hello following toobuild and package hello project:</span></span>

        mvn package

    <span data-ttu-id="4981d-201">Cette commande télécharge les dépendances nécessaires, builds, et puis packages hello projet.</span><span class="sxs-lookup"><span data-stu-id="4981d-201">This command downloads required dependencies, builds, and then packages hello project.</span></span> <span data-ttu-id="4981d-202">sortie de Hello est stockée dans hello **/target** répertoire comme **EventHubExample-1.0-SNAPSHOT.jar**.</span><span class="sxs-lookup"><span data-stu-id="4981d-202">hello output is stored in hello **/target** directory as **EventHubExample-1.0-SNAPSHOT.jar**.</span></span>

## <a name="test-locally"></a><span data-ttu-id="4981d-203">Tester les topologies localement</span><span class="sxs-lookup"><span data-stu-id="4981d-203">Test locally</span></span>

<span data-ttu-id="4981d-204">Étant donné que ces topologies uniquement lire et écrire tooEvent Hubs, vous pouvez les tester localement si vous avez un [environnement de développement Storm](http://storm.apache.org/releases/current/Setting-up-development-environment.html).</span><span class="sxs-lookup"><span data-stu-id="4981d-204">Since these topologies just read and write tooEvent Hubs, you can test them locally if you have a [Storm development environment](http://storm.apache.org/releases/current/Setting-up-development-environment.html).</span></span> <span data-ttu-id="4981d-205">Utilisez hello suivant toorun étapes localement dans l’environnement de développement hello :</span><span class="sxs-lookup"><span data-stu-id="4981d-205">Use hello following steps toorun locally in hello dev environment:</span></span>

1. <span data-ttu-id="4981d-206">Enregistreur de hello, exécutez :</span><span class="sxs-lookup"><span data-stu-id="4981d-206">Run hello writer:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /writer.yaml --filter dev.properties

2. <span data-ttu-id="4981d-207">Lecteur de hello, exécutez :</span><span class="sxs-lookup"><span data-stu-id="4981d-207">Run hello reader:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /reader.yaml --filter dev.properties

> [!TIP]
> * <span data-ttu-id="4981d-208">`--local`: Topologie hello exécution en mode local (non distribuées).</span><span class="sxs-lookup"><span data-stu-id="4981d-208">`--local`: Run hello topology in local mode (non-distributed).</span></span>
> * <span data-ttu-id="4981d-209">`-R /writer.yaml`: Charger la définition de la topologie hello de hello `resources` empaquetées dans le fichier jar de hello.</span><span class="sxs-lookup"><span data-stu-id="4981d-209">`-R /writer.yaml`: Load hello topology definition from hello `resources` packaged in hello jar.</span></span> <span data-ttu-id="4981d-210">Si la topologie de hello est un fichier sur le système de fichiers local hello, spécifiez tooit de chemin d’accès hello comme dernier paramètre de hello.</span><span class="sxs-lookup"><span data-stu-id="4981d-210">If hello topology is a file on hello local file system, specify hello path tooit as hello last parameter instead.</span></span>
> * <span data-ttu-id="4981d-211">`--filter dev.properties`: Utilisez contenu hello de `dev.properties` toofill dans les valeurs hello dans les définitions de topologie hello.</span><span class="sxs-lookup"><span data-stu-id="4981d-211">`--filter dev.properties`: Use hello contents of `dev.properties` toofill in hello values in hello topology definitions.</span></span> <span data-ttu-id="4981d-212">Par exemple, `${eventhub.read.policy.name}`.</span><span class="sxs-lookup"><span data-stu-id="4981d-212">For example, `${eventhub.read.policy.name}`.</span></span>

<span data-ttu-id="4981d-213">Sortie est journalisée toohello console s’exécute en local.</span><span class="sxs-lookup"><span data-stu-id="4981d-213">Output is logged toohello console when running locally.</span></span> <span data-ttu-id="4981d-214">Utilisez __Ctrl + C__ topologie de hello toostop.</span><span class="sxs-lookup"><span data-stu-id="4981d-214">Use __Ctrl+C__ toostop hello topology.</span></span>

## <a name="deploy-hello-topologies"></a><span data-ttu-id="4981d-215">Déployer des topologies de hello</span><span class="sxs-lookup"><span data-stu-id="4981d-215">Deploy hello topologies</span></span>

1. <span data-ttu-id="4981d-216">Utilisez SCP toocopy hello jar package tooyour cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4981d-216">Use SCP toocopy hello jar package tooyour HDInsight cluster.</span></span> <span data-ttu-id="4981d-217">Remplacez le nom d’utilisateur à utilisateur SSH hello pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="4981d-217">Replace USERNAME with hello SSH user for your cluster.</span></span> <span data-ttu-id="4981d-218">Remplacez CLUSTERNAME nom hello de votre cluster HDInsight :</span><span class="sxs-lookup"><span data-stu-id="4981d-218">Replace CLUSTERNAME with hello name of your HDInsight cluster:</span></span>

        scp ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.

    <span data-ttu-id="4981d-219">Si vous avez utilisé un mot de passe pour votre compte SSH, vous êtes un mot de passe hello tooenter demandées.</span><span class="sxs-lookup"><span data-stu-id="4981d-219">If you used a password for your SSH account, you are prompted tooenter hello password.</span></span> <span data-ttu-id="4981d-220">Si vous avez utilisé une clé SSH avec compte de hello, vous devrez peut-être toouse hello `-i` paramètre toospecify hello chemin d’accès toohello fichier de clé.</span><span class="sxs-lookup"><span data-stu-id="4981d-220">If you used an SSH key with hello account, you may need toouse hello `-i` parameter toospecify hello path toohello key file.</span></span> <span data-ttu-id="4981d-221">Par exemple, `scp -i ~/.ssh/id_rsa ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.`</span><span class="sxs-lookup"><span data-stu-id="4981d-221">For example, `scp -i ~/.ssh/id_rsa ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.`</span></span>

    <span data-ttu-id="4981d-222">Cette commande copie hello fichier toohello répertoire de base de votre utilisateur SSH sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="4981d-222">This command copies hello file toohello home directory of your SSH user on hello cluster.</span></span>

2. <span data-ttu-id="4981d-223">Une fois le téléchargement du fichier hello a terminé, utilisez le cluster HDInsight SSH tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="4981d-223">Once hello file has finished uploading, use SSH tooconnect toohello HDInsight cluster.</span></span> <span data-ttu-id="4981d-224">Remplacez **nom d’utilisateur** nom hello de votre connexion SSH.</span><span class="sxs-lookup"><span data-stu-id="4981d-224">Replace **USERNAME** hello name of your SSH login.</span></span> <span data-ttu-id="4981d-225">Remplacez **CLUSTERNAME** par le nom de votre cluster HDInsight :</span><span class="sxs-lookup"><span data-stu-id="4981d-225">Replace **CLUSTERNAME** with your HDInsight cluster name:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    > [!NOTE]
    > <span data-ttu-id="4981d-226">Si vous avez utilisé un mot de passe pour votre compte SSH, vous êtes un mot de passe hello tooenter demandées.</span><span class="sxs-lookup"><span data-stu-id="4981d-226">If you used a password for your SSH account, you are prompted tooenter hello password.</span></span> <span data-ttu-id="4981d-227">Si vous avez utilisé une clé SSH avec compte de hello, vous devrez peut-être toouse hello `-i` paramètre toospecify hello chemin d’accès toohello fichier de clé.</span><span class="sxs-lookup"><span data-stu-id="4981d-227">If you used an SSH key with hello account, you may need toouse hello `-i` parameter toospecify hello path toohello key file.</span></span> <span data-ttu-id="4981d-228">Hello exemple suivant charge hello la clé privée `~/.ssh/id_rsa`:</span><span class="sxs-lookup"><span data-stu-id="4981d-228">hello following example loads hello private key from `~/.ssh/id_rsa`:</span></span>
    >
    > `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`

3. <span data-ttu-id="4981d-229">Utilisez hello suivant des topologies de commande toostart hello :</span><span class="sxs-lookup"><span data-stu-id="4981d-229">Use hello following command toostart hello topologies:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties

    > [!TIP]
    > * <span data-ttu-id="4981d-230">`--remote`: Soumet hello topologie toohello service Nimbus, ce qui démarre sur les nœuds de cluster de hello travail de hello.</span><span class="sxs-lookup"><span data-stu-id="4981d-230">`--remote`: Submits hello topology toohello Nimbus service, which starts it on hello worker nodes in hello cluster.</span></span>

4. <span data-ttu-id="4981d-231">les données tooview hello connecté, accédez à toohttps://CLUSTERNAME.azurehdinsight.net/stormui, où __CLUSTERNAME__ hello désigne votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4981d-231">tooview hello logged data, go toohttps://CLUSTERNAME.azurehdinsight.net/stormui, where __CLUSTERNAME__ is hello name of your HDInsight cluster.</span></span> <span data-ttu-id="4981d-232">Sélectionnez les topologies hello et Descendre toohello composants.</span><span class="sxs-lookup"><span data-stu-id="4981d-232">Select hello topologies and drill down toohello components.</span></span> <span data-ttu-id="4981d-233">Sélectionnez hello __port__ entrée pour une instance d’un composant de tooview a enregistré des informations.</span><span class="sxs-lookup"><span data-stu-id="4981d-233">Select hello __port__ entry for an instance of a component tooview logged information.</span></span>

5. <span data-ttu-id="4981d-234">Utilisez hello suivant des topologies de hello toostop de commandes :</span><span class="sxs-lookup"><span data-stu-id="4981d-234">Use hello following commands toostop hello topologies:</span></span>

        storm kill reader
        storm kill writer

## <a name="delete-your-cluster"></a><span data-ttu-id="4981d-235">Supprimer votre cluster</span><span class="sxs-lookup"><span data-stu-id="4981d-235">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="4981d-236">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4981d-236">Next steps</span></span>

* [<span data-ttu-id="4981d-237">Exemples de topologies pour Storm dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="4981d-237">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
