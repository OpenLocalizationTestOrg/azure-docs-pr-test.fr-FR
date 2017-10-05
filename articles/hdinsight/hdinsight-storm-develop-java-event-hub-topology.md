---
title: "Traitement des événements d’Event Hubs avec Storm sur HDInsight avec Java | Microsoft Docs"
description: "Découvrez comment traiter les données Event Hubs avec une topologie Storm basée sur Java créée avec Maven."
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
ms.openlocfilehash: 2e8ebbdab2be7bed224a67facec798820615bb22
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-java"></a><span data-ttu-id="525e6-103">Traitement des événements Azure Event Hubs avec Storm sur HDInsight (Java)</span><span class="sxs-lookup"><span data-stu-id="525e6-103">Process events from Azure Event Hubs with Storm on HDInsight (Java)</span></span>

<span data-ttu-id="525e6-104">Découvrez comment utiliser Azure Event Hubs avec Storm sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="525e6-104">Learn how to use Azure Event Hubs with Storm on HDInsight.</span></span> <span data-ttu-id="525e6-105">Cet exemple utilise des composants basés sur Java pour lire et écrire des données dans Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="525e6-105">This example uses Java-based components to read and write data in Azure Event Hubs.</span></span>

<span data-ttu-id="525e6-106">Azure Event Hubs permet de traiter d’énormes quantités de données provenant de sites web, d’applications et d’appareils.</span><span class="sxs-lookup"><span data-stu-id="525e6-106">Azure Event Hubs allows you to process massive amounts of data from websites, apps, and devices.</span></span> <span data-ttu-id="525e6-107">Le spout Event Hub simplifie l’utilisation d’Apache Storm sur HDInsight pour analyser ces données en temps réel.</span><span class="sxs-lookup"><span data-stu-id="525e6-107">The Event Hub spout makes it easy to use Apache Storm on HDInsight to analyze this data in real time.</span></span> <span data-ttu-id="525e6-108">Vous pouvez également écrire des données dans les hubs d’événements à partir de Storm à l’aide du bolt des hubs d’événements.</span><span class="sxs-lookup"><span data-stu-id="525e6-108">You can also write data to Event Hubs from Storm by using the Event Hubs bolt.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="525e6-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="525e6-109">Prerequisites</span></span>

* <span data-ttu-id="525e6-110">Un cluster Apache Storm sur HDInsight version 3.6.</span><span class="sxs-lookup"><span data-stu-id="525e6-110">An Apache Storm on HDInsight cluster version 3.6.</span></span> <span data-ttu-id="525e6-111">Pour plus d’informations, voir [Prise en main de Storm sur HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="525e6-111">For more information, see [Get started with Storm on HDInsight cluster](hdinsight-apache-storm-tutorial-get-started-linux.md).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="525e6-112">Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="525e6-112">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="525e6-113">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="525e6-113">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="525e6-114">Un [hub d’événements Azure](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="525e6-114">An [Azure Event Hub](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

* <span data-ttu-id="525e6-115">[Kit de développeur Java (JDK) Oracle version 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) ou un équivalent, par exemple, [OpenJDK](http://openjdk.java.net/).</span><span class="sxs-lookup"><span data-stu-id="525e6-115">[Oracle Java Developer Kit (JDK) version 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) or equivalent, such as [OpenJDK](http://openjdk.java.net/).</span></span>

* <span data-ttu-id="525e6-116">[Maven](https://maven.apache.org/download.cgi) : Maven est un système de génération de projet pour les projets Java.</span><span class="sxs-lookup"><span data-stu-id="525e6-116">[Maven](https://maven.apache.org/download.cgi): Maven is a project build system for Java projects.</span></span>

* <span data-ttu-id="525e6-117">Un éditeur de texte ou un environnement de développement intégré (IDE).</span><span class="sxs-lookup"><span data-stu-id="525e6-117">A text editor or integrated development environment (IDE).</span></span>

    > [!NOTE]
    > <span data-ttu-id="525e6-118">Votre éditeur ou IDE peut avoir des fonctionnalités spécifiques pour l’utilisation avec Maven, qui ne sont pas traitées dans ce document.</span><span class="sxs-lookup"><span data-stu-id="525e6-118">Your editor or IDE may have specific functionality for working with Maven that is not addressed in this document.</span></span> <span data-ttu-id="525e6-119">Pour plus d’informations sur les capacités de votre environnement d’édition, consultez la documentation du produit que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="525e6-119">For information about the capabilities of your editing environment, see the documentation for the product you are using.</span></span>

    * <span data-ttu-id="525e6-120">Un client SSH.</span><span class="sxs-lookup"><span data-stu-id="525e6-120">An SSH client.</span></span> <span data-ttu-id="525e6-121">Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="525e6-121">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="525e6-122">Les commandes `ssh` et `scp`.</span><span class="sxs-lookup"><span data-stu-id="525e6-122">The `ssh` and `scp` commands.</span></span> <span data-ttu-id="525e6-123">Elles servent à copier des fichiers vers le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="525e6-123">These are used to copy files to the HDInsight cluster.</span></span> <span data-ttu-id="525e6-124">Sous Windows, vous pouvez les obtenir via Bash dans Windows 10.</span><span class="sxs-lookup"><span data-stu-id="525e6-124">On Windows, you can get these through Bash on Windows 10.</span></span>

## <a name="understanding-the-example"></a><span data-ttu-id="525e6-125">Vue d’ensemble de l’exemple</span><span class="sxs-lookup"><span data-stu-id="525e6-125">Understanding the example</span></span>

<span data-ttu-id="525e6-126">L’exemple [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) contient deux topologies :</span><span class="sxs-lookup"><span data-stu-id="525e6-126">The [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) example contains two topologies:</span></span>

<span data-ttu-id="525e6-127">La topologie `resources/writer.yaml` écrit des données aléatoires dans Azure Event Hub.</span><span class="sxs-lookup"><span data-stu-id="525e6-127">The `resources/writer.yaml` topology writes random data to an Azure Event Hub.</span></span> <span data-ttu-id="525e6-128">Les données sont générées par le composant `DeviceSpout` et comprennent un ID d’appareil aléatoire et une valeur d’appareil.</span><span class="sxs-lookup"><span data-stu-id="525e6-128">The data is generated by the `DeviceSpout` component, and is a random device ID and device value.</span></span> <span data-ttu-id="525e6-129">Ainsi, elles simulent certains matériels qui émettent un ID de chaîne et une valeur numérique.</span><span class="sxs-lookup"><span data-stu-id="525e6-129">So it's simulating some hardware that emits a string ID and a numeric value.</span></span>

<span data-ttu-id="525e6-130">La topologie `resources/reader.yaml` lit les données Event Hub (les données écrites par EventHubWriter), analyse les données JSON, puis enregistre les données `deviceId` et `deviceValue`.</span><span class="sxs-lookup"><span data-stu-id="525e6-130">Thee `resources/reader.yaml` topology reads data from Event Hub (the data written by EventHubWriter,) parses the JSON data, and then logs the `deviceId` and `deviceValue` data.</span></span>

<span data-ttu-id="525e6-131">Les données sont formatées sous forme de document JSON avant d’être écrites dans l’Event Hub ; lors de la lecture par le lecteur, elles sont analysées depuis JSON vers des tuples.</span><span class="sxs-lookup"><span data-stu-id="525e6-131">The data is formatted as a JSON document before it is written to Event Hub, and when read by the reader it is parsed out of JSON and into tuples.</span></span> <span data-ttu-id="525e6-132">Le format JSON est le suivant :</span><span class="sxs-lookup"><span data-stu-id="525e6-132">The JSON format is as follows:</span></span>

    { "deviceId": "unique identifier", "deviceValue": some value }

### <a name="project-configuration"></a><span data-ttu-id="525e6-133">Configuration du projet</span><span class="sxs-lookup"><span data-stu-id="525e6-133">Project configuration</span></span>

<span data-ttu-id="525e6-134">Le fichier `POM.xml` contient des informations de configuration pour ce projet Maven.</span><span class="sxs-lookup"><span data-stu-id="525e6-134">The `POM.xml` file contains configuration information for this Maven project.</span></span> <span data-ttu-id="525e6-135">Éléments intéressants :</span><span class="sxs-lookup"><span data-stu-id="525e6-135">The interesting pieces are:</span></span>

#### <a name="event-hub-components"></a><span data-ttu-id="525e6-136">Composants Event Hub</span><span class="sxs-lookup"><span data-stu-id="525e6-136">Event Hub components</span></span>

<span data-ttu-id="525e6-137">Le composant qui lit et écrit dans Azure Event Hubs se trouve dans le [référentiel HDInsight](https://github.com/hdinsight/mvn-rep).</span><span class="sxs-lookup"><span data-stu-id="525e6-137">The component that reads and writes to Azure Event Hubs is located in the [HDInsight repository](https://github.com/hdinsight/mvn-rep).</span></span> <span data-ttu-id="525e6-138">Les sections suivantes du fichier `POM.xml` chargent les composants à partir de ce référentiel.</span><span class="sxs-lookup"><span data-stu-id="525e6-138">The following sections in the `POM.xml` file load the components from this repository</span></span>

```xml
<repositories>
    <repository>
        <id>hdinsight-examples</id>
        <url>http://raw.github.com/hdinsight/mvn-repo/master</url>
    </repository>
</repositories>
```

#### <a name="the-eventhubs-storm-spout-dependency"></a><span data-ttu-id="525e6-139">Dépendance du spout Storm EventHubs</span><span class="sxs-lookup"><span data-stu-id="525e6-139">The EventHubs Storm Spout dependency</span></span>

```xml
<dependency>
    <groupId>com.microsoft</groupId>
    <artifactId>eventhubs</artifactId>
    <version>${storm.eventhub.version}</version>
</dependency>
```

<span data-ttu-id="525e6-140">Ce fichier XML définit une dépendance pour le package eventhubs. Il contient à la fois un spout pour la lecture à partir d’Event Hubs et un bolt pour l’écriture dans Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="525e6-140">This xml defines a dependency for the eventhubs package, which contains both a spout for reading from Event Hubs, and a bolt for writing to it.</span></span>

```xml
</source>
    <target>1.8</target>
    </configuration>
</plugin>
```

<span data-ttu-id="525e6-141">Ce fichier XML configure le projet de sorte à générer un résultat pour Java 8, résultat qui est ensuite utilisé par HDInsight 3.5 ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="525e6-141">This xml configures the project to generate output for Java 8, which is used by HDInsight 3.5 or higher.</span></span>

#### <a name="the-maven-shade-plugin"></a><span data-ttu-id="525e6-142">maven-shade-plugin</span><span class="sxs-lookup"><span data-stu-id="525e6-142">The maven-shade-plugin</span></span>

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

<span data-ttu-id="525e6-143">Ce fichier XML configure la solution pour empaqueter la sortie dans une sorte de super fichier jar.</span><span class="sxs-lookup"><span data-stu-id="525e6-143">This xml configures the solution to package the output into an uber jar.</span></span> <span data-ttu-id="525e6-144">Ce fichier jar contient le code de projet et les dépendances requises.</span><span class="sxs-lookup"><span data-stu-id="525e6-144">The jar contains both the project code and required dependencies.</span></span> <span data-ttu-id="525e6-145">Il est également utilisé pour :</span><span class="sxs-lookup"><span data-stu-id="525e6-145">It is also used to:</span></span>

* <span data-ttu-id="525e6-146">Renommer les fichiers de licence pour les dépendances.</span><span class="sxs-lookup"><span data-stu-id="525e6-146">Rename license files for the dependencies.</span></span>
* <span data-ttu-id="525e6-147">Exclure les sécurités/signatures.</span><span class="sxs-lookup"><span data-stu-id="525e6-147">Exclude security/signatures.</span></span>
* <span data-ttu-id="525e6-148">Assurez-vous que plusieurs implémentations de la même interface soient fusionnées dans une entrée.</span><span class="sxs-lookup"><span data-stu-id="525e6-148">Ensure that multiple implementations of the same interface are merged into one entry.</span></span>

<span data-ttu-id="525e6-149">Ces paramètres de configuration évitent les erreurs au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="525e6-149">These configuration settings prevent errors at runtime.</span></span>

#### <a name="topology-definitions"></a><span data-ttu-id="525e6-150">Définitions de topologie</span><span class="sxs-lookup"><span data-stu-id="525e6-150">Topology definitions</span></span>

<span data-ttu-id="525e6-151">Cet exemple utilise le framework [Flux](https://storm.apache.org/releases/1.1.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="525e6-151">This example uses the [Flux](https://storm.apache.org/releases/1.1.0/flux.html) framework.</span></span> <span data-ttu-id="525e6-152">Ce framework utilise le langage YAML pour définir les topologies.</span><span class="sxs-lookup"><span data-stu-id="525e6-152">This framework uses YAML to define the topologies.</span></span> <span data-ttu-id="525e6-153">Le principal avantage, c’est que vous ne codez pas la topologie en dur dans le code Java.</span><span class="sxs-lookup"><span data-stu-id="525e6-153">The primary benefit is that you aren't hard coding the topology in Java code.</span></span> <span data-ttu-id="525e6-154">Étant donné que la définition est rédigée en YAML, vous pouvez la modifier avant de soumettre la topologie, sans devoir tout recompiler.</span><span class="sxs-lookup"><span data-stu-id="525e6-154">Since the definition is YAML, you can change it before submitting the topology, without having to recompile everything.</span></span>

<span data-ttu-id="525e6-155">__writer.yaml__ :</span><span class="sxs-lookup"><span data-stu-id="525e6-155">__writer.yaml__:</span></span>

```yaml
---
# Topology that reads from Event Hubs
name: "eventhubwriter"

components:
  # Configure the Event Hub spout
  - id: "eventhubbolt-config"
    className: "org.apache.storm.eventhubs.bolt.EventHubBoltConfig"
    constructorArgs:
      # These are populated from the .properties file when the topology is started
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
    # parallelism hint. This should be the same as the number of partitions for your Event Hub, so we read it from the dev.properties file passed at run time.
    parallelism: ${eventhub.partitions}

  # Log information
  - id: "log-bolt"
    className: "org.apache.storm.flux.wrappers.bolts.LogInfoBolt"
    parallelism: 1

# How data flows through the components
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

<span data-ttu-id="525e6-156">__reader.yaml__ :</span><span class="sxs-lookup"><span data-stu-id="525e6-156">__reader.yaml__:</span></span>

```yaml
---
# Topology that reads from Event Hubs
name: "eventhubreader"

components:
  # Configure the Event Hub spout
  - id: "eventhubspout-config"
    className: "org.apache.storm.eventhubs.spout.EventHubSpoutConfig"
    constructorArgs:
      # These are populated from the .properties file when the topology is started
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
    # parallelism hint. This should be the same as the number of partitions for your Event Hub, so we read it from the dev.properties file passed at run time.
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

# How data flows through the components
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

#### <a name="tell-the-topology-about-event-hub"></a><span data-ttu-id="525e6-157">Transmettre les informations Event Hub à la topologie</span><span class="sxs-lookup"><span data-stu-id="525e6-157">Tell the topology about Event Hub</span></span>

<span data-ttu-id="525e6-158">Au moment de l’exécution, le fichier `dev.properties` est utilisé pour transmettre la configuration Event Hub à la topologie.</span><span class="sxs-lookup"><span data-stu-id="525e6-158">At run time, the `dev.properties` file is used to pass the Event Hub configuration to the topology.</span></span> <span data-ttu-id="525e6-159">L’exemple suivant montre le contenu par défaut du fichier :</span><span class="sxs-lookup"><span data-stu-id="525e6-159">The following example is the default contents of the file:</span></span>

```yaml
eventhub.write.policy.name: writer
eventhub.write.policy.key: your_key_here
eventhub.read.policy.name: reader
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: storm
eventhub.partitions: 2
```

## <a name="configure-environment-variables"></a><span data-ttu-id="525e6-160">Configuration des variables d’environnement</span><span class="sxs-lookup"><span data-stu-id="525e6-160">Configure environment variables</span></span>

<span data-ttu-id="525e6-161">Les variables d’environnement suivantes peuvent être définies lors de l’installation de Java et du Kit de développeur Java (JDK) sur votre station de travail de développement.</span><span class="sxs-lookup"><span data-stu-id="525e6-161">The following environment variables may be set when you install Java and the JDK on your development workstation.</span></span> <span data-ttu-id="525e6-162">Toutefois, vous devez vérifier qu’elles existent et qu’elles contiennent les valeurs correctes pour votre système.</span><span class="sxs-lookup"><span data-stu-id="525e6-162">However, you should check that they exist and that they contain the correct values for your system.</span></span>

* <span data-ttu-id="525e6-163">**JAVA_HOME** : doit pointer vers le répertoire d’installation de l’environnement d’exécution Java (JRE).</span><span class="sxs-lookup"><span data-stu-id="525e6-163">**JAVA_HOME** - should point to the directory where the Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="525e6-164">Par exemple, sur une distribution Unix ou Linux, il doit avoir une valeur semblable à `/usr/lib/jvm/java-7-oracle`.</span><span class="sxs-lookup"><span data-stu-id="525e6-164">For example, in a Unix or Linux distribution, it should have a value similar to `/usr/lib/jvm/java-7-oracle`.</span></span> <span data-ttu-id="525e6-165">Sous Windows, il a une valeur semblable à `c:\Program Files (x86)\Java\jre1.7`</span><span class="sxs-lookup"><span data-stu-id="525e6-165">In Windows, it would have a value similar to `c:\Program Files (x86)\Java\jre1.7`</span></span>
* <span data-ttu-id="525e6-166">**PATH** :doit contenir les chemins d’accès suivants :</span><span class="sxs-lookup"><span data-stu-id="525e6-166">**PATH** - should contain the following paths:</span></span>

  * <span data-ttu-id="525e6-167">**JAVA_HOME** (ou le chemin d’accès équivalent)</span><span class="sxs-lookup"><span data-stu-id="525e6-167">**JAVA_HOME** (or the equivalent path)</span></span>
  * <span data-ttu-id="525e6-168">**JAVA_HOME\bin** (ou le chemin d’accès équivalent)</span><span class="sxs-lookup"><span data-stu-id="525e6-168">**JAVA_HOME\bin** (or the equivalent path)</span></span>
  * <span data-ttu-id="525e6-169">Le répertoire d’installation de Maven</span><span class="sxs-lookup"><span data-stu-id="525e6-169">The directory where Maven is installed</span></span>

## <a name="configure-event-hub"></a><span data-ttu-id="525e6-170">Configuration du hub d'événements</span><span class="sxs-lookup"><span data-stu-id="525e6-170">Configure Event Hub</span></span>

<span data-ttu-id="525e6-171">Event Hubs est la source de données pour cet exemple.</span><span class="sxs-lookup"><span data-stu-id="525e6-171">Event Hubs is the data source for this example.</span></span> <span data-ttu-id="525e6-172">Procédez comme suit pour créer un Event Hub.</span><span class="sxs-lookup"><span data-stu-id="525e6-172">Use the following steps to create a Event Hub.</span></span>

1. <span data-ttu-id="525e6-173">Dans le [portail Azure Classic](https://manage.windowsazure.com), sélectionnez **NEW** > **Service Bus** > **Event Hub** > **Création personnalisée**.</span><span class="sxs-lookup"><span data-stu-id="525e6-173">From the [Azure Classic Portal](https://manage.windowsazure.com), select **NEW** > **Service Bus** > **Event Hub** > **Custom Create**.</span></span>

2. <span data-ttu-id="525e6-174">Dans l’écran **Ajouter un nouvel hub d’événements**, entrez le **Nom du hub d’événements**.</span><span class="sxs-lookup"><span data-stu-id="525e6-174">On the **Add a new Event Hub** screen, enter an **Event Hub Name**.</span></span> <span data-ttu-id="525e6-175">Sélectionnez la **région** pour créer le hub, puis créez un espace de noms ou sélectionnez-en un existant.</span><span class="sxs-lookup"><span data-stu-id="525e6-175">Select the **Region** to create the hub in, and then create a namespace or select an existing one.</span></span> <span data-ttu-id="525e6-176">Enfin, cliquez sur la **flèche** pour continuer.</span><span class="sxs-lookup"><span data-stu-id="525e6-176">Finally, click the **Arrow** to continue.</span></span>

    ![page 1 de l’assistant](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz1.png)

   > [!NOTE]
   > <span data-ttu-id="525e6-178">Vous devez sélectionner le même **emplacement** que celui de votre serveur Storm sur HDInsight pour réduire la latence et les coûts.</span><span class="sxs-lookup"><span data-stu-id="525e6-178">Select the same **Location** as your Storm on HDInsight server to reduce latency and costs.</span></span>

3. <span data-ttu-id="525e6-179">Dans l’écran **Configurer un hub d’événements**, entrez les valeurs pour **Nombre de partitions** et **Rétention des messages**.</span><span class="sxs-lookup"><span data-stu-id="525e6-179">On the **Configure Event Hub** screen, enter the **Partition count** and **Message Retention** values.</span></span> <span data-ttu-id="525e6-180">Pour cet exemple, entrez 10 pour le nombre de partitions et 1 pour la conservation des messages.</span><span class="sxs-lookup"><span data-stu-id="525e6-180">For this example, use a partition count of 10 and a message retention of 1.</span></span> <span data-ttu-id="525e6-181">Notez le nombre de partitions, car vous en aurez besoin ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="525e6-181">Note the partition count because you need this value later.</span></span>

    ![page 2 de l’assistant](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz2.png)

4. <span data-ttu-id="525e6-183">Une fois le hub d’événements créé, sélectionnez l’espace de noms, **Event Hubs**, puis le hub d’événements créé auparavant.</span><span class="sxs-lookup"><span data-stu-id="525e6-183">After the event hub has been created, select the namespace, select **Event Hubs**, and then select the event hub that you created earlier.</span></span>
5. <span data-ttu-id="525e6-184">Sélectionnez **Configurer**, puis créez deux nouvelles stratégies d’accès en utilisant les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="525e6-184">Select **Configure**, then create two new access policies by using the following information:</span></span>

    <table>
    <tr><th><span data-ttu-id="525e6-185">Nom</span><span class="sxs-lookup"><span data-stu-id="525e6-185">Name</span></span></th><th><span data-ttu-id="525e6-186">Autorisations</span><span class="sxs-lookup"><span data-stu-id="525e6-186">Permissions</span></span></th></tr>
    <tr><td><span data-ttu-id="525e6-187">Writer</span><span class="sxs-lookup"><span data-stu-id="525e6-187">Writer</span></span></td><td><span data-ttu-id="525e6-188">Envoyer</span><span class="sxs-lookup"><span data-stu-id="525e6-188">Send</span></span></td></tr>
    <tr><td><span data-ttu-id="525e6-189">Lecteur</span><span class="sxs-lookup"><span data-stu-id="525e6-189">Reader</span></span></td><td><span data-ttu-id="525e6-190">Écouter</span><span class="sxs-lookup"><span data-stu-id="525e6-190">Listen</span></span></td></tr>
    </table>

    <span data-ttu-id="525e6-191">Après avoir créé les autorisations, sélectionnez l’icône **Enregistrer** située en bas de page.</span><span class="sxs-lookup"><span data-stu-id="525e6-191">After You create the permissions, select the **Save** icon at the bottom of the page.</span></span> <span data-ttu-id="525e6-192">Ces stratégies d’accès partagé sont utilisées pour lire et écrire dans Event Hub.</span><span class="sxs-lookup"><span data-stu-id="525e6-192">These shared access policies are used to read and write to Event Hub.</span></span>

    ![stratégies](./media/hdinsight-storm-develop-csharp-event-hub-topology/policy.png)

6. <span data-ttu-id="525e6-194">Après avoir enregistré vos stratégies, utilisez le **Générateur de clés d’accès partagé** situé en bas de page pour récupérer les clés des stratégies **writer** et **reader**.</span><span class="sxs-lookup"><span data-stu-id="525e6-194">After you save the policies, use the **Shared access key generator** at the bottom of the page to retrieve the key for the **writer** and **reader** policies.</span></span> <span data-ttu-id="525e6-195">Enregistrez ces clés.</span><span class="sxs-lookup"><span data-stu-id="525e6-195">Save these keys.</span></span>

## <a name="download-and-build-the-project"></a><span data-ttu-id="525e6-196">Télécharger et générer le projet</span><span class="sxs-lookup"><span data-stu-id="525e6-196">Download and build the project</span></span>

1. <span data-ttu-id="525e6-197">Téléchargez le projet à partir de GitHub : [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="525e6-197">Download the project from GitHub: [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub).</span></span> <span data-ttu-id="525e6-198">Vous pouvez télécharger le package dans une archive .zip ou utiliser [git](https://git-scm.com/) pour cloner le projet localement.</span><span class="sxs-lookup"><span data-stu-id="525e6-198">You can either download the package as a zip archive, or use [git](https://git-scm.com/) to clone the project locally.</span></span>

2. <span data-ttu-id="525e6-199">Modifiez le fichier `dev.properties` et intégrez-y la configuration de votre Event Hub.</span><span class="sxs-lookup"><span data-stu-id="525e6-199">Modify the `dev.properties` file with the configuration for your Event Hub.</span></span>

3. <span data-ttu-id="525e6-200">Pour générer le projet et créer un package, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="525e6-200">Use the following to build and package the project:</span></span>

        mvn package

    <span data-ttu-id="525e6-201">Cette commande télécharge les dépendances requises, génère le projet, puis crée le package.</span><span class="sxs-lookup"><span data-stu-id="525e6-201">This command downloads required dependencies, builds, and then packages the project.</span></span> <span data-ttu-id="525e6-202">Le résultat est stocké dans le répertoire **/target** dans un fichier **EventHubExample-1.0-SNAPSHOT.jar**.</span><span class="sxs-lookup"><span data-stu-id="525e6-202">The output is stored in the **/target** directory as **EventHubExample-1.0-SNAPSHOT.jar**.</span></span>

## <a name="test-locally"></a><span data-ttu-id="525e6-203">Tester les topologies localement</span><span class="sxs-lookup"><span data-stu-id="525e6-203">Test locally</span></span>

<span data-ttu-id="525e6-204">Ces topologies lisent et écrivent uniquement dans Event Hubs, vous pouvez les tester localement si vous utilisez un [environnement de développement Storm](http://storm.apache.org/releases/current/Setting-up-development-environment.html).</span><span class="sxs-lookup"><span data-stu-id="525e6-204">Since these topologies just read and write to Event Hubs, you can test them locally if you have a [Storm development environment](http://storm.apache.org/releases/current/Setting-up-development-environment.html).</span></span> <span data-ttu-id="525e6-205">Effectuez les étapes suivantes pour exécuter les topologies localement dans l’environnement de développement :</span><span class="sxs-lookup"><span data-stu-id="525e6-205">Use the following steps to run locally in the dev environment:</span></span>

1. <span data-ttu-id="525e6-206">Exécutez le writer :</span><span class="sxs-lookup"><span data-stu-id="525e6-206">Run the writer:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /writer.yaml --filter dev.properties

2. <span data-ttu-id="525e6-207">Exécutez le reader :</span><span class="sxs-lookup"><span data-stu-id="525e6-207">Run the reader:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /reader.yaml --filter dev.properties

> [!TIP]
> * <span data-ttu-id="525e6-208">`--local` : exécuter la topologie en mode local (non distribué).</span><span class="sxs-lookup"><span data-stu-id="525e6-208">`--local`: Run the topology in local mode (non-distributed).</span></span>
> * <span data-ttu-id="525e6-209">`-R /writer.yaml` : charger la définition de la topologie à partir de l’élément `resources` empaqueté dans le fichier jar.</span><span class="sxs-lookup"><span data-stu-id="525e6-209">`-R /writer.yaml`: Load the topology definition from the `resources` packaged in the jar.</span></span> <span data-ttu-id="525e6-210">Si la topologie est un fichier sur le système de fichiers local, spécifiez-en alors le chemin d’accès (dernier paramètre).</span><span class="sxs-lookup"><span data-stu-id="525e6-210">If the topology is a file on the local file system, specify the path to it as the last parameter instead.</span></span>
> * <span data-ttu-id="525e6-211">`--filter dev.properties` : utiliser le contenu de `dev.properties` pour renseigner les valeurs dans les définitions de topologie.</span><span class="sxs-lookup"><span data-stu-id="525e6-211">`--filter dev.properties`: Use the contents of `dev.properties` to fill in the values in the topology definitions.</span></span> <span data-ttu-id="525e6-212">Par exemple, `${eventhub.read.policy.name}`.</span><span class="sxs-lookup"><span data-stu-id="525e6-212">For example, `${eventhub.read.policy.name}`.</span></span>

<span data-ttu-id="525e6-213">La sortie est enregistrée dans la console en cas d’exécution locale.</span><span class="sxs-lookup"><span data-stu-id="525e6-213">Output is logged to the console when running locally.</span></span> <span data-ttu-id="525e6-214">Utilisez la combinaison de touches __Ctrl+C__ pour arrêter la topologie.</span><span class="sxs-lookup"><span data-stu-id="525e6-214">Use __Ctrl+C__ to stop the topology.</span></span>

## <a name="deploy-the-topologies"></a><span data-ttu-id="525e6-215">Déploiement des topologies</span><span class="sxs-lookup"><span data-stu-id="525e6-215">Deploy the topologies</span></span>

1. <span data-ttu-id="525e6-216">Utilisez SCP pour copier le package jar dans votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="525e6-216">Use SCP to copy the jar package to your HDInsight cluster.</span></span> <span data-ttu-id="525e6-217">Remplacez USERNAME par l’utilisateur SSH de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="525e6-217">Replace USERNAME with the SSH user for your cluster.</span></span> <span data-ttu-id="525e6-218">Remplacez CLUSTERNAME par le nom de votre cluster HDInsight :</span><span class="sxs-lookup"><span data-stu-id="525e6-218">Replace CLUSTERNAME with the name of your HDInsight cluster:</span></span>

        scp ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.

    <span data-ttu-id="525e6-219">Si vous avez utilisé un mot de passe pour votre compte SSH, vous êtes invité à le saisir.</span><span class="sxs-lookup"><span data-stu-id="525e6-219">If you used a password for your SSH account, you are prompted to enter the password.</span></span> <span data-ttu-id="525e6-220">Si vous avez utilisé une clé SSH avec le compte, vous devrez peut-être utiliser le paramètre `-i` pour spécifier le chemin d’accès au fichier de clé.</span><span class="sxs-lookup"><span data-stu-id="525e6-220">If you used an SSH key with the account, you may need to use the `-i` parameter to specify the path to the key file.</span></span> <span data-ttu-id="525e6-221">Par exemple, `scp -i ~/.ssh/id_rsa ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.`</span><span class="sxs-lookup"><span data-stu-id="525e6-221">For example, `scp -i ~/.ssh/id_rsa ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.`</span></span>

    <span data-ttu-id="525e6-222">Cette commande copie le fichier sur le répertoire de base de votre utilisateur SSH sur le cluster.</span><span class="sxs-lookup"><span data-stu-id="525e6-222">This command copies the file to the home directory of your SSH user on the cluster.</span></span>

2. <span data-ttu-id="525e6-223">Une fois le téléchargement du fichier terminé, utilisez SSH pour vous connecter au cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="525e6-223">Once the file has finished uploading, use SSH to connect to the HDInsight cluster.</span></span> <span data-ttu-id="525e6-224">Remplacez **USERNAME** par le nom de votre connexion SSH.</span><span class="sxs-lookup"><span data-stu-id="525e6-224">Replace **USERNAME** the name of your SSH login.</span></span> <span data-ttu-id="525e6-225">Remplacez **CLUSTERNAME** par le nom de votre cluster HDInsight :</span><span class="sxs-lookup"><span data-stu-id="525e6-225">Replace **CLUSTERNAME** with your HDInsight cluster name:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    > [!NOTE]
    > <span data-ttu-id="525e6-226">Si vous avez utilisé un mot de passe pour votre compte SSH, vous êtes invité à le saisir.</span><span class="sxs-lookup"><span data-stu-id="525e6-226">If you used a password for your SSH account, you are prompted to enter the password.</span></span> <span data-ttu-id="525e6-227">Si vous avez utilisé une clé SSH avec le compte, vous devrez peut-être utiliser le paramètre `-i` pour spécifier le chemin d’accès au fichier de clé.</span><span class="sxs-lookup"><span data-stu-id="525e6-227">If you used an SSH key with the account, you may need to use the `-i` parameter to specify the path to the key file.</span></span> <span data-ttu-id="525e6-228">L’exemple suivant charge la clé privée à partir de `~/.ssh/id_rsa` :</span><span class="sxs-lookup"><span data-stu-id="525e6-228">The following example loads the private key from `~/.ssh/id_rsa`:</span></span>
    >
    > `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`

3. <span data-ttu-id="525e6-229">Utilisez la commande suivante pour démarrer les topologies :</span><span class="sxs-lookup"><span data-stu-id="525e6-229">Use the following command to start the topologies:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties

    > [!TIP]
    > * <span data-ttu-id="525e6-230">`--remote` : envoie la topologie au service Nimbus, qui la démarre sur les nœuds de travail du cluster.</span><span class="sxs-lookup"><span data-stu-id="525e6-230">`--remote`: Submits the topology to the Nimbus service, which starts it on the worker nodes in the cluster.</span></span>

4. <span data-ttu-id="525e6-231">Pour afficher les données enregistrées, accédez à l’adresse https://CLUSTERNAME.azurehdinsight.net/stormui, où __CLUSTERNAME__ est le nom de votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="525e6-231">To view the logged data, go to https://CLUSTERNAME.azurehdinsight.net/stormui, where __CLUSTERNAME__ is the name of your HDInsight cluster.</span></span> <span data-ttu-id="525e6-232">Sélectionnez les topologies et explorez-en les composants.</span><span class="sxs-lookup"><span data-stu-id="525e6-232">Select the topologies and drill down to the components.</span></span> <span data-ttu-id="525e6-233">Sélectionnez l’entrée de __port__ d’une instance de composant pour afficher les informations enregistrées.</span><span class="sxs-lookup"><span data-stu-id="525e6-233">Select the __port__ entry for an instance of a component to view logged information.</span></span>

5. <span data-ttu-id="525e6-234">Utilisez les commandes suivantes pour arrêter les topologies :</span><span class="sxs-lookup"><span data-stu-id="525e6-234">Use the following commands to stop the topologies:</span></span>

        storm kill reader
        storm kill writer

## <a name="delete-your-cluster"></a><span data-ttu-id="525e6-235">Supprimer votre cluster</span><span class="sxs-lookup"><span data-stu-id="525e6-235">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="525e6-236">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="525e6-236">Next steps</span></span>

* [<span data-ttu-id="525e6-237">Exemples de topologies pour Storm dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="525e6-237">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
