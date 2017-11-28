---
title: "Traitement des événements de concentrateurs d’événements avec Storm - Azure HDInsight | Microsoft Docs"
description: "Découvrez comment traiter les données de concentrateurs d’événements Azure avec une topologie Storm C# créée dans Visual Studio à l’aide des outils HDInsight pour Visual Studio."
services: hdinsight,notification hubs
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 67f9d08c-eea0-401b-952b-db765655dad0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.openlocfilehash: 4b6fd87b057d93175d3ef284238d77be3bdde61d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-c"></a><span data-ttu-id="fa379-103">Traitement des événements Azure Event Hubs avec Storm sur HDInsight (C#)</span><span class="sxs-lookup"><span data-stu-id="fa379-103">Process events from Azure Event Hubs with Storm on HDInsight (C#)</span></span>

<span data-ttu-id="fa379-104">Découvrez comment utiliser des événements Azure Event Hubs d’Apache Storm sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fa379-104">Learn how to work with Azure Event Hubs from Apache Storm on HDInsight.</span></span> <span data-ttu-id="fa379-105">Ce document utilise une topologie C# Storm pour lire et écrire des données à partir d’événements Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="fa379-105">This document uses a C# Storm topology to read and write data from Evbent Hubs</span></span>

> [!NOTE]
> <span data-ttu-id="fa379-106">Pour obtenir une version Java de ce projet, consultez [Traitement des événements Azure Event Hubs avec Storm sur HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="fa379-106">For a Java version of this project, see [Process events from Azure Event Hubs with Storm on HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span></span>

## <a name="scpnet"></a><span data-ttu-id="fa379-107">SCP.NET</span><span class="sxs-lookup"><span data-stu-id="fa379-107">SCP.NET</span></span>

<span data-ttu-id="fa379-108">Les étapes indiquées dans ce document utilisent SCP.NET, un package NuGet qui vous permet de créer des topologies et des composants C# pour les utiliser avec Storm sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fa379-108">The steps in this document use SCP.NET, a NuGet package that makes it easy to create C# topologies and components for use with Storm on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fa379-109">Bien que les étapes décrites dans ce document reposent sur un environnement de développement Windows avec Visual Studio, le projet compilé peut être soumis à un cluster Storm sur HDInsight utilisant Linux.</span><span class="sxs-lookup"><span data-stu-id="fa379-109">While the steps in this document rely on a Windows development environment with Visual Studio, the compiled project can be submitted to a Storm on HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="fa379-110">Seuls les clusters basés sur Linux créés après le 28 octobre 2016 prennent en charge les topologies SCP.NET.</span><span class="sxs-lookup"><span data-stu-id="fa379-110">Only Linux-based clusters created after October 28, 2016, support SCP.NET topologies.</span></span>

<span data-ttu-id="fa379-111">La version 3.4 de HDInsight (et les versions suivantes) utilisent Mono pour exécuter des topologies C#.</span><span class="sxs-lookup"><span data-stu-id="fa379-111">HDInsight 3.4 and greater use Mono to run C# topologies.</span></span> <span data-ttu-id="fa379-112">L’exemple utilisé dans ce document fonctionne avec HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="fa379-112">The example used in this document works with HDInsight 3.6.</span></span> <span data-ttu-id="fa379-113">Si vous prévoyez de créer vos propres solutions .NET pour HDInsight, consultez le document sur la [mono-compatibilité](http://www.mono-project.com/docs/about-mono/compatibility/) pour identifier les éventuelles incompatibilités.</span><span class="sxs-lookup"><span data-stu-id="fa379-113">If you plan on creating your own .NET solutions for HDInsight, check the [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document for potential incompatibilities.</span></span>

### <a name="cluster-versioning"></a><span data-ttu-id="fa379-114">Contrôle de version de cluster</span><span class="sxs-lookup"><span data-stu-id="fa379-114">Cluster versioning</span></span>

<span data-ttu-id="fa379-115">Le package NuGet Microsoft.SCP.Net.SDK que vous utilisez pour votre projet doit correspondre à la version principale de Storm installée sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fa379-115">The Microsoft.SCP.Net.SDK NuGet package you use for your project must match the major version of Storm installed on HDInsight.</span></span> <span data-ttu-id="fa379-116">Les versions 3.5 et 3.6 de HDInsight utilisent Storm 1.x. Vous devez donc utiliser la version 1.0.x.x de SCP.NET avec ces clusters.</span><span class="sxs-lookup"><span data-stu-id="fa379-116">HDInsight versions 3.5 and 3.6 use Storm 1.x, so you must use SCP.NET version 1.0.x.x with these clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fa379-117">L’exemple inclus dans ce document attend un cluster HDInsight 3.5 ou 3.6.</span><span class="sxs-lookup"><span data-stu-id="fa379-117">The example in this document expects an HDInsight 3.5 or 3.6 cluster.</span></span>
>
> <span data-ttu-id="fa379-118">Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="fa379-118">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="fa379-119">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="fa379-119">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="fa379-120">Les topologies C# doivent également cibler la version 4.5 de .NET.</span><span class="sxs-lookup"><span data-stu-id="fa379-120">C# topologies must also target .NET 4.5.</span></span>

## <a name="how-to-work-with-event-hubs"></a><span data-ttu-id="fa379-121">Utilisation d’Event Hubs</span><span class="sxs-lookup"><span data-stu-id="fa379-121">How to work with Event Hubs</span></span>

<span data-ttu-id="fa379-122">Microsoft fournit un ensemble de composants Java qui peut être utilisé pour communiquer avec les concentrateurs d’événements à partir d’une topologie Storm.</span><span class="sxs-lookup"><span data-stu-id="fa379-122">Microsoft provides a set of Java components that can be used to communicate with Event Hubs from a Storm topology.</span></span> <span data-ttu-id="fa379-123">Vous trouverez le fichier d’archive Java (JAR) qui contient une version compatible HDInsight 3.6 de ces composants à l’adresse [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span><span class="sxs-lookup"><span data-stu-id="fa379-123">You can find the Java archive (JAR) file that contains an HDInsight 3.6 compatible version of these components at [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fa379-124">Même si les composants sont écrits en Java, vous pouvez les utiliser facilement à partir d’une topologie C#.</span><span class="sxs-lookup"><span data-stu-id="fa379-124">While the components are written in Java, you can easily use them from a C# topology.</span></span>

<span data-ttu-id="fa379-125">Les composants suivants sont utilisés dans cet exemple :</span><span class="sxs-lookup"><span data-stu-id="fa379-125">The following components are used in this example:</span></span>

* <span data-ttu-id="fa379-126">__EventHubSpout__ : lit les données à partir d’Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="fa379-126">__EventHubSpout__: Reads data from Event Hubs.</span></span>
* <span data-ttu-id="fa379-127">__EventHubBolt__ : écrit des données dans Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="fa379-127">__EventHubBolt__: Writes data to Event Hubs.</span></span>
* <span data-ttu-id="fa379-128">__EventHubSpoutConfig__ : permet de configurer EventHubSpout.</span><span class="sxs-lookup"><span data-stu-id="fa379-128">__EventHubSpoutConfig__: Used to configure EventHubSpout.</span></span>
* <span data-ttu-id="fa379-129">__EventHubBoltConfig__ : permet de configurer EventHubBolt.</span><span class="sxs-lookup"><span data-stu-id="fa379-129">__EventHubBoltConfig__: Used to configure EventHubBolt.</span></span>

### <a name="example-spout-usage"></a><span data-ttu-id="fa379-130">Exemple d’utilisation du spout</span><span class="sxs-lookup"><span data-stu-id="fa379-130">Example spout usage</span></span>

<span data-ttu-id="fa379-131">SCP.NET fournit des méthodes pour l’ajout d’un EventHubSpout à votre topologie.</span><span class="sxs-lookup"><span data-stu-id="fa379-131">SCP.NET provides methods for adding an EventHubSpout to your topology.</span></span> <span data-ttu-id="fa379-132">Il est plus facile d’utiliser ces méthodes pour ajouter un Spout que d’utiliser les méthodes génériques pour ajouter un composant Java.</span><span class="sxs-lookup"><span data-stu-id="fa379-132">These methods make it easier to add a spout than using the generic methods for adding a Java component.</span></span> <span data-ttu-id="fa379-133">L’exemple suivant illustre la création d’un spout en utilisant les méthodes __SetEventHubSpout__ et **EventHubSpoutConfig** de SCP.NET :</span><span class="sxs-lookup"><span data-stu-id="fa379-133">The following example demonstrates how to create a spout by using the __SetEventHubSpout__ and **EventHubSpoutConfig** methods provided by SCP.NET:</span></span>

```csharp
 topologyBuilder.SetEventHubSpout(
    "EventHubSpout",
    new EventHubSpoutConfig(
        ConfigurationManager.AppSettings["EventHubSharedAccessKeyName"],
        ConfigurationManager.AppSettings["EventHubSharedAccessKey"],
        ConfigurationManager.AppSettings["EventHubNamespace"],
        ConfigurationManager.AppSettings["EventHubEntityPath"],
        eventHubPartitions),
    eventHubPartitions);
```

<span data-ttu-id="fa379-134">L’exemple précédent crée un composant spout nommé __EventHubSpout__ et le configure pour communiquer avec un concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="fa379-134">The previous example creates a new spout component named __EventHubSpout__, and configures it to communicate with an event hub.</span></span> <span data-ttu-id="fa379-135">L’indicateur de parallélisme du composant est défini sur le nombre de partitions dans le concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="fa379-135">The parallelism hint for the component is set to the number of partitions in the event hub.</span></span> <span data-ttu-id="fa379-136">Ce paramètre permet à Storm de créer une instance du composant pour chaque partition.</span><span class="sxs-lookup"><span data-stu-id="fa379-136">This setting allows Storm to create an instance of the component for each partition.</span></span>

### <a name="example-bolt-usage"></a><span data-ttu-id="fa379-137">Exemple d’utilisation du bolt</span><span class="sxs-lookup"><span data-stu-id="fa379-137">Example bolt usage</span></span>

<span data-ttu-id="fa379-138">Utilisez la méthode **JavaComponentConstructor** pour créer une instance du bolt.</span><span class="sxs-lookup"><span data-stu-id="fa379-138">Use the **JavaComponmentConstructor** method to create an instance of the bolt.</span></span> <span data-ttu-id="fa379-139">L’exemple suivant illustre la création et la configuration d’une instance de **l’EventHubBolt** :</span><span class="sxs-lookup"><span data-stu-id="fa379-139">The following example demonstrates how to create and configure a new instance of the **EventHubBolt**:</span></span>

```csharp
// Java construcvtor for the Event Hub Bolt
JavaComponentConstructor constructor = JavaComponentConstructor.CreateFromClojureExpr(
    String.Format(@"(org.apache.storm.eventhubs.bolt.EventHubBolt. (org.apache.storm.eventhubs.bolt.EventHubBoltConfig. " +
        @"""{0}"" ""{1}"" ""{2}"" ""{3}"" ""{4}"" {5}))",
        ConfigurationManager.AppSettings["EventHubPolicyName"],
        ConfigurationManager.AppSettings["EventHubPolicyKey"],
        ConfigurationManager.AppSettings["EventHubNamespace"],
        "servicebus.windows.net",
        ConfigurationManager.AppSettings["EventHubName"],
        "true"));

// Set the bolt to subscribe to data from the spout
topologyBuilder.SetJavaBolt(
    "eventhubbolt",
    constructor,
    partitionCount)
        .shuffleGrouping("Spout");
```

> [!NOTE]
> <span data-ttu-id="fa379-140">Cet exemple utilise une expression Clojure transmise sous forme de chaîne au lieu d’utiliser **JavaComponentConstructor** pour créer un **EventHubBoltConfig**, comme dans l’exemple de spout.</span><span class="sxs-lookup"><span data-stu-id="fa379-140">This example uses a Clojure expression passed as a string, instead of using **JavaComponentConstructor** to create an **EventHubBoltConfig**, as the spout example did.</span></span> <span data-ttu-id="fa379-141">Les deux méthodes fonctionnent.</span><span class="sxs-lookup"><span data-stu-id="fa379-141">Either method works.</span></span> <span data-ttu-id="fa379-142">Utilisez celle qui vous convient.</span><span class="sxs-lookup"><span data-stu-id="fa379-142">Use the method that feels best to you.</span></span>

## <a name="download-the-completed-project"></a><span data-ttu-id="fa379-143">Télécharger le projet complet</span><span class="sxs-lookup"><span data-stu-id="fa379-143">Download the completed project</span></span>

<span data-ttu-id="fa379-144">Vous pouvez télécharger une version complète du projet créé dans ce didacticiel à partir de [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="fa379-144">You can download a complete version of the project created in this tutorial from [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span> <span data-ttu-id="fa379-145">Toutefois, vous devrez tout de même fournir des paramètres de configuration en suivant les étapes de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="fa379-145">However, you still need to provide configuration settings by following the steps in this tutorial.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="fa379-146">Composants requis</span><span class="sxs-lookup"><span data-stu-id="fa379-146">Prerequisites</span></span>

* <span data-ttu-id="fa379-147">Un cluster [Apache Storm sur HDInsight version 3.5 ou 3.6](hdinsight-apache-storm-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="fa379-147">An [Apache Storm on HDInsight cluster version 3.5 or 3.6](hdinsight-apache-storm-tutorial-get-started.md).</span></span>

    > [!WARNING]
    > <span data-ttu-id="fa379-148">L’exemple utilisé dans ce document requiert Storm sur HDInsight version 3.5 ou 3.6.</span><span class="sxs-lookup"><span data-stu-id="fa379-148">The example used in this document requires Storm on HDInsight version 3.5 or 3.6.</span></span> <span data-ttu-id="fa379-149">Cela ne fonctionne pas avec les versions antérieures de HDInsight en raison des modifications apportées aux noms de classes.</span><span class="sxs-lookup"><span data-stu-id="fa379-149">This does not work with older versions of HDInsight, due to breaking class name changes.</span></span> <span data-ttu-id="fa379-150">Pour une version de cet exemple fonctionnant avec les anciens clusters, consultez [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub/releases).</span><span class="sxs-lookup"><span data-stu-id="fa379-150">For a version of this example that works with older clusters, see [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub/releases).</span></span>

* <span data-ttu-id="fa379-151">Un [concentrateur d’événements Azure](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="fa379-151">An [Azure event hub](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

* <span data-ttu-id="fa379-152">Le [kit de développement logiciel (SDK) Azure .NET](http://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="fa379-152">The [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span></span>

* <span data-ttu-id="fa379-153">Les [outils HDInsight pour Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="fa379-153">The [HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

* <span data-ttu-id="fa379-154">Java JDK 1.8 ou version ultérieure sur votre environnement de développement.</span><span class="sxs-lookup"><span data-stu-id="fa379-154">Java JDK 1.8 or later on your development environment.</span></span> <span data-ttu-id="fa379-155">Les téléchargements JDK sont disponibles dans [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="fa379-155">JDK downloads are available from [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>

  * <span data-ttu-id="fa379-156">La variable d’environnement **JAVA_HOME** doit pointer vers le répertoire qui contient Java.</span><span class="sxs-lookup"><span data-stu-id="fa379-156">The **JAVA_HOME** environment variable must point to the directory that contains Java.</span></span>
  * <span data-ttu-id="fa379-157">Le répertoire **%JAVA_HOME%/bin** doit se trouver dans le chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="fa379-157">The **%JAVA_HOME%/bin** directory must be in the path.</span></span>

## <a name="download-the-event-hubs-components"></a><span data-ttu-id="fa379-158">Télécharger les composants des concentrateurs d’événements</span><span class="sxs-lookup"><span data-stu-id="fa379-158">Download the Event Hubs components</span></span>

<span data-ttu-id="fa379-159">Téléchargez les composants Spout et Bolt des événements Event Hubs à l’adresse [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span><span class="sxs-lookup"><span data-stu-id="fa379-159">Download the Event Hubs spout and bolt component from [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span></span>

<span data-ttu-id="fa379-160">Créez un répertoire nommé `eventhubspout` et enregistrez le fichier dans le répertoire.</span><span class="sxs-lookup"><span data-stu-id="fa379-160">Create a directory named `eventhubspout`, and save the file into the directory.</span></span>

## <a name="configure-event-hubs"></a><span data-ttu-id="fa379-161">Configurer les hubs d’événement</span><span class="sxs-lookup"><span data-stu-id="fa379-161">Configure Event Hubs</span></span>

<span data-ttu-id="fa379-162">Event Hubs est la source de données pour cet exemple.</span><span class="sxs-lookup"><span data-stu-id="fa379-162">Event Hubs is the data source for this example.</span></span> <span data-ttu-id="fa379-163">Utilisez les informations contenues dans la section « Création d’un espace de noms de concentrateurs d’événements et d’un concentrateur d’événements » du document [Bien démarrer avec l’envoi de messages vers des concentrateurs d’événements Azure dans .NET Standard](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="fa379-163">Use the information in the "Create an event hub" section of [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

1. <span data-ttu-id="fa379-164">Après avoir créé le concentrateur d’événements, affichez le panneau **EventHub** dans le portail Azure et sélectionnez **Stratégies d’accès partagé**.</span><span class="sxs-lookup"><span data-stu-id="fa379-164">After the event hub has been created, view the **EventHub** blade in the Azure portal, and select **Shared access policies**.</span></span> <span data-ttu-id="fa379-165">Sélectionnez **+ Ajouter** pour ajouter les stratégies suivantes :</span><span class="sxs-lookup"><span data-stu-id="fa379-165">Select **+ Add** to add the following policies:</span></span>

   | <span data-ttu-id="fa379-166">Nom</span><span class="sxs-lookup"><span data-stu-id="fa379-166">Name</span></span> | <span data-ttu-id="fa379-167">Autorisations</span><span class="sxs-lookup"><span data-stu-id="fa379-167">Permissions</span></span> |
   | --- | --- |
   | <span data-ttu-id="fa379-168">writer</span><span class="sxs-lookup"><span data-stu-id="fa379-168">writer</span></span> |<span data-ttu-id="fa379-169">Envoyer</span><span class="sxs-lookup"><span data-stu-id="fa379-169">Send</span></span> |
   | <span data-ttu-id="fa379-170">reader</span><span class="sxs-lookup"><span data-stu-id="fa379-170">reader</span></span> |<span data-ttu-id="fa379-171">Écouter</span><span class="sxs-lookup"><span data-stu-id="fa379-171">Listen</span></span> |

    ![Capture d’écran de la fenêtre de stratégies d’accès partagé](./media/hdinsight-storm-develop-csharp-event-hub-topology/sas.png)

2. <span data-ttu-id="fa379-173">Sélectionnez les stratégies **reader** et **writer**.</span><span class="sxs-lookup"><span data-stu-id="fa379-173">Select the **reader** and **writer** policies.</span></span> <span data-ttu-id="fa379-174">Copiez et enregistrez la valeur de clé primaire des deux stratégies, car elles sont utilisées ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="fa379-174">Copy and save the primary key value for both policies, as these values are used later.</span></span>

## <a name="configure-the-eventhubwriter"></a><span data-ttu-id="fa379-175">Configuration de l’EventHubWriter</span><span class="sxs-lookup"><span data-stu-id="fa379-175">Configure the EventHubWriter</span></span>

1. <span data-ttu-id="fa379-176">Si vous n’avez pas encore installé la dernière version des outils HDInsight pour Visual Studio, consultez [Se connecter à Azure HDInsight et exécuter des requêtes Hive avec Data Lake Tools pour Visual Studio | Microsoft Docs](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="fa379-176">If you have not already installed the latest version of the HDInsight tools for Visual Studio, see [Get started using HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

2. <span data-ttu-id="fa379-177">Téléchargez la solution depuis [eventhub-storm-hybrid](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="fa379-177">Download the solution from [eventhub-storm-hybrid](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span>

3. <span data-ttu-id="fa379-178">Dans le projet **EventHubWriter**, ouvrez le fichier **App.config**.</span><span class="sxs-lookup"><span data-stu-id="fa379-178">In the **EventHubWriter** project, open the **App.config** file.</span></span> <span data-ttu-id="fa379-179">Utilisez les informations à partir du concentrateur d’événements que vous avez configuré précédemment pour renseigner la valeur des clés suivantes :</span><span class="sxs-lookup"><span data-stu-id="fa379-179">Use the information from the event hub that you configured earlier to fill in the value for the following keys:</span></span>

   | <span data-ttu-id="fa379-180">Clé</span><span class="sxs-lookup"><span data-stu-id="fa379-180">Key</span></span> | <span data-ttu-id="fa379-181">Valeur</span><span class="sxs-lookup"><span data-stu-id="fa379-181">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="fa379-182">EventHubPolicyName</span><span class="sxs-lookup"><span data-stu-id="fa379-182">EventHubPolicyName</span></span> |<span data-ttu-id="fa379-183">writer (si vous avez utilisé un nom différent pour la stratégie avec l’autorisation *Send*, utilisez-le à la place.)</span><span class="sxs-lookup"><span data-stu-id="fa379-183">writer (If you used a different name for the policy with *Send* permission, use it instead.)</span></span> |
   | <span data-ttu-id="fa379-184">EventHubPolicyKey</span><span class="sxs-lookup"><span data-stu-id="fa379-184">EventHubPolicyKey</span></span> |<span data-ttu-id="fa379-185">La clé de la stratégie writer.</span><span class="sxs-lookup"><span data-stu-id="fa379-185">The key for the writer policy.</span></span> |
   | <span data-ttu-id="fa379-186">eventHubNamespace</span><span class="sxs-lookup"><span data-stu-id="fa379-186">EventHubNamespace</span></span> |<span data-ttu-id="fa379-187">L’espace de noms qui contient votre concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="fa379-187">The namespace that contains your event hub.</span></span> |
   | <span data-ttu-id="fa379-188">eventHubName</span><span class="sxs-lookup"><span data-stu-id="fa379-188">EventHubName</span></span> |<span data-ttu-id="fa379-189">Le nom de votre concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="fa379-189">Your event hub name.</span></span> |
   | <span data-ttu-id="fa379-190">EventHubPartitionCount</span><span class="sxs-lookup"><span data-stu-id="fa379-190">EventHubPartitionCount</span></span> |<span data-ttu-id="fa379-191">Le nombre de partitions dans votre concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="fa379-191">The number of partitions in your event hub.</span></span> |

4. <span data-ttu-id="fa379-192">Enregistrez et fermez le fichier **App.config**.</span><span class="sxs-lookup"><span data-stu-id="fa379-192">Save and close the **App.config** file.</span></span>

## <a name="configure-the-eventhubreader"></a><span data-ttu-id="fa379-193">Configuration de l’EventHubReader</span><span class="sxs-lookup"><span data-stu-id="fa379-193">Configure the EventHubReader</span></span>

1. <span data-ttu-id="fa379-194">Ouvrez le projet **EventHubReader**.</span><span class="sxs-lookup"><span data-stu-id="fa379-194">Open the **EventHubReader** project.</span></span>

2. <span data-ttu-id="fa379-195">Ouvrez le fichier **App.config** pour **EventHubReader**.</span><span class="sxs-lookup"><span data-stu-id="fa379-195">Open the **App.config** file for the **EventHubReader**.</span></span> <span data-ttu-id="fa379-196">Utilisez les informations à partir du concentrateur d’événements que vous avez configuré précédemment pour renseigner la valeur des clés suivantes :</span><span class="sxs-lookup"><span data-stu-id="fa379-196">Use the information from the event hub that you configured earlier to fill in the value for the following keys:</span></span>

   | <span data-ttu-id="fa379-197">Clé</span><span class="sxs-lookup"><span data-stu-id="fa379-197">Key</span></span> | <span data-ttu-id="fa379-198">Valeur</span><span class="sxs-lookup"><span data-stu-id="fa379-198">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="fa379-199">EventHubPolicyName</span><span class="sxs-lookup"><span data-stu-id="fa379-199">EventHubPolicyName</span></span> |<span data-ttu-id="fa379-200">reader (si vous avez utilisé un nom différent pour la stratégie avec l’autorisation *listen*, utilisez-le à la place.)</span><span class="sxs-lookup"><span data-stu-id="fa379-200">reader (If you used a different name for the policy with *listen* permission, use it instead.)</span></span> |
   | <span data-ttu-id="fa379-201">EventHubPolicyKey</span><span class="sxs-lookup"><span data-stu-id="fa379-201">EventHubPolicyKey</span></span> |<span data-ttu-id="fa379-202">La clé de la stratégie reader.</span><span class="sxs-lookup"><span data-stu-id="fa379-202">The key for the reader policy.</span></span> |
   | <span data-ttu-id="fa379-203">eventHubNamespace</span><span class="sxs-lookup"><span data-stu-id="fa379-203">EventHubNamespace</span></span> |<span data-ttu-id="fa379-204">L’espace de noms qui contient votre concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="fa379-204">The namespace that contains your event hub.</span></span> |
   | <span data-ttu-id="fa379-205">eventHubName</span><span class="sxs-lookup"><span data-stu-id="fa379-205">EventHubName</span></span> |<span data-ttu-id="fa379-206">Le nom de votre concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="fa379-206">Your event hub name.</span></span> |
   | <span data-ttu-id="fa379-207">EventHubPartitionCount</span><span class="sxs-lookup"><span data-stu-id="fa379-207">EventHubPartitionCount</span></span> |<span data-ttu-id="fa379-208">Le nombre de partitions dans votre concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="fa379-208">The number of partitions in your event hub.</span></span> |

3. <span data-ttu-id="fa379-209">Enregistrez et fermez le fichier **App.config**.</span><span class="sxs-lookup"><span data-stu-id="fa379-209">Save and close the **App.config** file.</span></span>

## <a name="deploy-the-topologies"></a><span data-ttu-id="fa379-210">Déploiement des topologies</span><span class="sxs-lookup"><span data-stu-id="fa379-210">Deploy the topologies</span></span>

1. <span data-ttu-id="fa379-211">Dans **l’Explorateur de solutions**, cliquez avec le bouton droit de la souris sur le projet **EventHubReader** et sélectionnez **Envoyer à Storm sur HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="fa379-211">From **Solution Explorer**, right-click the **EventHubReader** project, and select **Submit to Storm on HDInsight**.</span></span>

    ![Capture d’écran de l’Explorateur de solutions, avec l’option Envoyer à Storm sur HDInsight mise en surbrillance](./media/hdinsight-storm-develop-csharp-event-hub-topology/submittostorm.png)

2. <span data-ttu-id="fa379-213">Dans la boîte de dialogue **Envoyer la topologie**, sélectionnez votre **cluster Storm**.</span><span class="sxs-lookup"><span data-stu-id="fa379-213">On the **Submit Topology** dialog box, select your **Storm Cluster**.</span></span> <span data-ttu-id="fa379-214">Développez **Configurations supplémentaires**, sélectionnez **Chemins d’accès aux fichiers Java**, sélectionnez **...**, puis choisissez le répertoire qui contient le fichier JAR que vous avez téléchargé précédemment.</span><span class="sxs-lookup"><span data-stu-id="fa379-214">Expand **Additional Configurations**, select **Java File Paths**, select **...**, and select the directory that contains the JAR file that you downloaded earlier.</span></span> <span data-ttu-id="fa379-215">Pour finir, cliquez sur **Envoyer**.</span><span class="sxs-lookup"><span data-stu-id="fa379-215">Finally, click **Submit**.</span></span>

    ![Capture d’écran de la boîte de dialogue Envoyer la topologie](./media/hdinsight-storm-develop-csharp-event-hub-topology/submit.png)

3. <span data-ttu-id="fa379-217">Une fois la topologie envoyée, la **Visionneuse de topologies Storm** apparaît.</span><span class="sxs-lookup"><span data-stu-id="fa379-217">When the topology has been submitted, the **Storm Topologies Viewer** appears.</span></span> <span data-ttu-id="fa379-218">Sélectionnez la topologie **EventHubReader** dans le volet gauche pour afficher des informations sur la topologie.</span><span class="sxs-lookup"><span data-stu-id="fa379-218">To view information about the topology, select the **EventHubReader** topology in the left pane.</span></span>

    ![Capture d’écran de la visionneuse de topologies Storm](./media/hdinsight-storm-develop-csharp-event-hub-topology/topologyviewer.png)

4. <span data-ttu-id="fa379-220">Dans **l’Explorateur de solutions**, cliquez avec le bouton droit de la souris sur le projet **EventHubWriter** et sélectionnez **Envoyer à Storm sur HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="fa379-220">From **Solution Explorer**, right-click the **EventHubWriter** project, and select **Submit to Storm on HDInsight**.</span></span>

5. <span data-ttu-id="fa379-221">Dans la boîte de dialogue **Envoyer la topologie**, sélectionnez votre **cluster Storm**.</span><span class="sxs-lookup"><span data-stu-id="fa379-221">On the **Submit Topology** dialog box, select your **Storm Cluster**.</span></span> <span data-ttu-id="fa379-222">Développez **Configurations supplémentaires**, sélectionnez **Chemins d’accès aux fichiers Java**, sélectionnez **...**, puis choisissez le répertoire qui contient le fichier JAR que vous avez téléchargé précédemment.</span><span class="sxs-lookup"><span data-stu-id="fa379-222">Expand **Additional Configurations**, select **Java File Paths**, select **...**, and select the directory that contains the JAR file you downloaded earlier.</span></span> <span data-ttu-id="fa379-223">Pour finir, cliquez sur **Envoyer**.</span><span class="sxs-lookup"><span data-stu-id="fa379-223">Finally, click **Submit**.</span></span>

6. <span data-ttu-id="fa379-224">Une fois la topologie envoyée, actualisez la liste des topologies dans la **Visionneuse de topologies Storm** pour vérifier que les deux topologies sont en cours d’exécution sur le cluster.</span><span class="sxs-lookup"><span data-stu-id="fa379-224">When the topology has been submitted, refresh the topology list in the **Storm Topologies Viewer** to verify that both topologies are running on the cluster.</span></span>

7. <span data-ttu-id="fa379-225">Dans la **Visionneuse de topologies Storm**, sélectionnez la topologie **EventHubReader**.</span><span class="sxs-lookup"><span data-stu-id="fa379-225">In **Storm Topologies Viewer**, select the **EventHubReader** topology.</span></span>

8. <span data-ttu-id="fa379-226">Pour ouvrir le résumé du composant associé au bolt, double-cliquez sur le composant **LogBolt** dans le diagramme.</span><span class="sxs-lookup"><span data-stu-id="fa379-226">To open the component summary for the bolt, double-click the **LogBolt** component in the diagram.</span></span>

9. <span data-ttu-id="fa379-227">Dans la section **Exécuteurs**, sélectionnez un des liens dans la colonne **Port**.</span><span class="sxs-lookup"><span data-stu-id="fa379-227">In the **Executors** section, select one of the links in the **Port** column.</span></span> <span data-ttu-id="fa379-228">Cela affiche les informations enregistrées par le composant.</span><span class="sxs-lookup"><span data-stu-id="fa379-228">This displays information logged by the component.</span></span> <span data-ttu-id="fa379-229">Les informations enregistrées sont similaires au texte suivant :</span><span class="sxs-lookup"><span data-stu-id="fa379-229">The logged information is similar to the following text:</span></span>

        2017-03-02 14:51:29.255 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,255 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1830978598,"deviceId":"8566ccbc-034d-45db-883d-d8a31f34068e"}
        2017-03-02 14:51:29.283 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,283 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1756413275,"deviceId":"647a5eff-823d-482f-a8b4-b95b35ae570b"}
        2017-03-02 14:51:29.313 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,312 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1108478910,"deviceId":"206a68fa-8264-4d61-9100-bfdb68ee8f0a"}

## <a name="stop-the-topologies"></a><span data-ttu-id="fa379-230">Arrêt des topologies</span><span class="sxs-lookup"><span data-stu-id="fa379-230">Stop the topologies</span></span>

<span data-ttu-id="fa379-231">Pour arrêter les topologies, sélectionnez chaque topologie dans la **Visionneuse de topologies Storm**, puis cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="fa379-231">To stop the topologies, select each topology in the **Storm Topology Viewer**, then click **Kill**.</span></span>

![Capture d’écran de la visionneuse de topologies Storm avec le bouton Supprimer mis en surbrillance](./media/hdinsight-storm-develop-csharp-event-hub-topology/killtopology.png)

## <a name="delete-your-cluster"></a><span data-ttu-id="fa379-233">Supprimer votre cluster</span><span class="sxs-lookup"><span data-stu-id="fa379-233">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="fa379-234">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fa379-234">Next steps</span></span>

<span data-ttu-id="fa379-235">Dans ce document, vous avez découvert comment utiliser le spout et le bolt du concentrateur d’événements Java à partir d’une topologie C# pour utiliser des données dans le concentrateur d’événements Azure.</span><span class="sxs-lookup"><span data-stu-id="fa379-235">In this document, you have learned how to use the Java Event Hubs spout and bolt from a C# topology to work with data in Azure Event Hubs.</span></span> <span data-ttu-id="fa379-236">Pour en savoir plus sur la création de topologies C#, consultez les documents suivants :</span><span class="sxs-lookup"><span data-stu-id="fa379-236">To learn more about creating C# topologies, see the following:</span></span>

* [<span data-ttu-id="fa379-237">Développement de topologies C# pour Apache Storm dans HDInsight à l'aide de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fa379-237">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="fa379-238">Guide de programmation SCP</span><span class="sxs-lookup"><span data-stu-id="fa379-238">SCP programming guide</span></span>](hdinsight-storm-scp-programming-guide.md)
* [<span data-ttu-id="fa379-239">Exemples de topologies pour Storm dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="fa379-239">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
