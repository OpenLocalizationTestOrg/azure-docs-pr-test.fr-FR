---
title: "événements d’aaaProcess de concentrateurs d’événements avec Storm - Azure HDInsight | Documents Microsoft"
description: "Découvrez comment tooprocess des données à partir d’Azure Event Hubs avec une topologie Storm c# créés dans Visual Studio, à l’aide de hello outils HDInsight pour Visual Studio."
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
ms.openlocfilehash: 30cd910d80eba066f283197bcbbaf11145bc5524
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-c"></a><span data-ttu-id="44502-103">Traitement des événements Azure Event Hubs avec Storm sur HDInsight (C#)</span><span class="sxs-lookup"><span data-stu-id="44502-103">Process events from Azure Event Hubs with Storm on HDInsight (C#)</span></span>

<span data-ttu-id="44502-104">Découvrez comment toowork avec des concentrateurs d’événements Azure à partir d’Apache Storm sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="44502-104">Learn how toowork with Azure Event Hubs from Apache Storm on HDInsight.</span></span> <span data-ttu-id="44502-105">Ce document utilise une tempête c# topologie tooread et écrire les données de concentrateurs de Evbent</span><span class="sxs-lookup"><span data-stu-id="44502-105">This document uses a C# Storm topology tooread and write data from Evbent Hubs</span></span>

> [!NOTE]
> <span data-ttu-id="44502-106">Pour obtenir une version Java de ce projet, consultez [Traitement des événements Azure Event Hubs avec Storm sur HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="44502-106">For a Java version of this project, see [Process events from Azure Event Hubs with Storm on HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span></span>

## <a name="scpnet"></a><span data-ttu-id="44502-107">SCP.NET</span><span class="sxs-lookup"><span data-stu-id="44502-107">SCP.NET</span></span>

<span data-ttu-id="44502-108">étapes Hello dans ce document utilisent SCP.NET, un package NuGet qui la rend facile toocreate c# topologies et les composants pour une utilisation avec Storm sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="44502-108">hello steps in this document use SCP.NET, a NuGet package that makes it easy toocreate C# topologies and components for use with Storm on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="44502-109">Alors que les étapes hello dans ce document reposent sur un environnement de développement Windows avec Visual Studio, projet compilé de hello peut être soumis tooa Storm sur le cluster HDInsight qui utilise Linux.</span><span class="sxs-lookup"><span data-stu-id="44502-109">While hello steps in this document rely on a Windows development environment with Visual Studio, hello compiled project can be submitted tooa Storm on HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="44502-110">Seuls les clusters basés sur Linux créés après le 28 octobre 2016 prennent en charge les topologies SCP.NET.</span><span class="sxs-lookup"><span data-stu-id="44502-110">Only Linux-based clusters created after October 28, 2016, support SCP.NET topologies.</span></span>

<span data-ttu-id="44502-111">HDInsight 3.4 et topologies de toorun Mono c# utilisation supérieure.</span><span class="sxs-lookup"><span data-stu-id="44502-111">HDInsight 3.4 and greater use Mono toorun C# topologies.</span></span> <span data-ttu-id="44502-112">exemple Hello utilisé dans ce document fonctionne avec HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="44502-112">hello example used in this document works with HDInsight 3.6.</span></span> <span data-ttu-id="44502-113">Si vous prévoyez de créer vos propres solutions .NET pour HDInsight, vérifiez hello [compatibilité Mono](http://www.mono-project.com/docs/about-mono/compatibility/) document pour identifier les éventuelles incompatibilités.</span><span class="sxs-lookup"><span data-stu-id="44502-113">If you plan on creating your own .NET solutions for HDInsight, check hello [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document for potential incompatibilities.</span></span>

### <a name="cluster-versioning"></a><span data-ttu-id="44502-114">Contrôle de version de cluster</span><span class="sxs-lookup"><span data-stu-id="44502-114">Cluster versioning</span></span>

<span data-ttu-id="44502-115">Hello package NuGet de Microsoft.SCP.Net.SDK vous utilisez pour votre projet doit correspondre au version majeure de hello de Storm installé sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="44502-115">hello Microsoft.SCP.Net.SDK NuGet package you use for your project must match hello major version of Storm installed on HDInsight.</span></span> <span data-ttu-id="44502-116">Les versions 3.5 et 3.6 de HDInsight utilisent Storm 1.x. Vous devez donc utiliser la version 1.0.x.x de SCP.NET avec ces clusters.</span><span class="sxs-lookup"><span data-stu-id="44502-116">HDInsight versions 3.5 and 3.6 use Storm 1.x, so you must use SCP.NET version 1.0.x.x with these clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="44502-117">exemple Hello dans ce document attend un 3.5 HDInsight ou cluster 3.6.</span><span class="sxs-lookup"><span data-stu-id="44502-117">hello example in this document expects an HDInsight 3.5 or 3.6 cluster.</span></span>
>
> <span data-ttu-id="44502-118">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="44502-118">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="44502-119">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="44502-119">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="44502-120">Les topologies C# doivent également cibler la version 4.5 de .NET.</span><span class="sxs-lookup"><span data-stu-id="44502-120">C# topologies must also target .NET 4.5.</span></span>

## <a name="how-toowork-with-event-hubs"></a><span data-ttu-id="44502-121">Comment toowork avec des concentrateurs d’événements</span><span class="sxs-lookup"><span data-stu-id="44502-121">How toowork with Event Hubs</span></span>

<span data-ttu-id="44502-122">Microsoft fournit un ensemble de composants Java qui peuvent être toocommunicate utilisé avec les concentrateurs d’événements à partir d’une topologie Storm.</span><span class="sxs-lookup"><span data-stu-id="44502-122">Microsoft provides a set of Java components that can be used toocommunicate with Event Hubs from a Storm topology.</span></span> <span data-ttu-id="44502-123">Vous pouvez trouver hello Java archives (JAR) fichier qui contient une version compatible de HDInsight 3.6 de ces composants à [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span><span class="sxs-lookup"><span data-stu-id="44502-123">You can find hello Java archive (JAR) file that contains an HDInsight 3.6 compatible version of these components at [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="44502-124">Alors que les composants de hello sont écrits en Java, vous pouvez les utiliser facilement à partir d’une topologie c#.</span><span class="sxs-lookup"><span data-stu-id="44502-124">While hello components are written in Java, you can easily use them from a C# topology.</span></span>

<span data-ttu-id="44502-125">Hello, suivant les composants est utilisé dans cet exemple :</span><span class="sxs-lookup"><span data-stu-id="44502-125">hello following components are used in this example:</span></span>

* <span data-ttu-id="44502-126">__EventHubSpout__ : lit les données à partir d’Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="44502-126">__EventHubSpout__: Reads data from Event Hubs.</span></span>
* <span data-ttu-id="44502-127">__EventHubBolt__: écrit les données tooEvent concentrateurs.</span><span class="sxs-lookup"><span data-stu-id="44502-127">__EventHubBolt__: Writes data tooEvent Hubs.</span></span>
* <span data-ttu-id="44502-128">__EventHubSpoutConfig__: utilisé tooconfigure EventHubSpout.</span><span class="sxs-lookup"><span data-stu-id="44502-128">__EventHubSpoutConfig__: Used tooconfigure EventHubSpout.</span></span>
* <span data-ttu-id="44502-129">__EventHubBoltConfig__: utilisé tooconfigure EventHubBolt.</span><span class="sxs-lookup"><span data-stu-id="44502-129">__EventHubBoltConfig__: Used tooconfigure EventHubBolt.</span></span>

### <a name="example-spout-usage"></a><span data-ttu-id="44502-130">Exemple d’utilisation du spout</span><span class="sxs-lookup"><span data-stu-id="44502-130">Example spout usage</span></span>

<span data-ttu-id="44502-131">SCP.NET fournit des méthodes pour l’ajout d’une topologie de tooyour EventHubSpout.</span><span class="sxs-lookup"><span data-stu-id="44502-131">SCP.NET provides methods for adding an EventHubSpout tooyour topology.</span></span> <span data-ttu-id="44502-132">Ces méthodes rendent plus facile tooadd un bec que l’utilisation des méthodes génériques de hello pour ajouter un composant Java.</span><span class="sxs-lookup"><span data-stu-id="44502-132">These methods make it easier tooadd a spout than using hello generic methods for adding a Java component.</span></span> <span data-ttu-id="44502-133">Hello exemple suivant montre comment un bec à l’aide de toocreate hello __SetEventHubSpout__ et **EventHubSpoutConfig** méthodes fournies par SCP.NET :</span><span class="sxs-lookup"><span data-stu-id="44502-133">hello following example demonstrates how toocreate a spout by using hello __SetEventHubSpout__ and **EventHubSpoutConfig** methods provided by SCP.NET:</span></span>

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

<span data-ttu-id="44502-134">Hello précédent exemple crée un nouveau composant bec nommé __EventHubSpout__et il configure toocommunicate avec un concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="44502-134">hello previous example creates a new spout component named __EventHubSpout__, and configures it toocommunicate with an event hub.</span></span> <span data-ttu-id="44502-135">indicateur de parallélisme Hello pour le composant de hello a la valeur nombre toohello de partitions dans le concentrateur d’événements hello.</span><span class="sxs-lookup"><span data-stu-id="44502-135">hello parallelism hint for hello component is set toohello number of partitions in hello event hub.</span></span> <span data-ttu-id="44502-136">Ce paramètre permet de Storm toocreate une instance du composant hello pour chaque partition.</span><span class="sxs-lookup"><span data-stu-id="44502-136">This setting allows Storm toocreate an instance of hello component for each partition.</span></span>

### <a name="example-bolt-usage"></a><span data-ttu-id="44502-137">Exemple d’utilisation du bolt</span><span class="sxs-lookup"><span data-stu-id="44502-137">Example bolt usage</span></span>

<span data-ttu-id="44502-138">Hello d’utilisation **JavaComponmentConstructor** méthode toocreate une instance d’éclair de hello.</span><span class="sxs-lookup"><span data-stu-id="44502-138">Use hello **JavaComponmentConstructor** method toocreate an instance of hello bolt.</span></span> <span data-ttu-id="44502-139">Hello exemple suivant montre comment toocreate et configurer une nouvelle instance de hello **EventHubBolt**:</span><span class="sxs-lookup"><span data-stu-id="44502-139">hello following example demonstrates how toocreate and configure a new instance of hello **EventHubBolt**:</span></span>

```csharp
// Java construcvtor for hello Event Hub Bolt
JavaComponentConstructor constructor = JavaComponentConstructor.CreateFromClojureExpr(
    String.Format(@"(org.apache.storm.eventhubs.bolt.EventHubBolt. (org.apache.storm.eventhubs.bolt.EventHubBoltConfig. " +
        @"""{0}"" ""{1}"" ""{2}"" ""{3}"" ""{4}"" {5}))",
        ConfigurationManager.AppSettings["EventHubPolicyName"],
        ConfigurationManager.AppSettings["EventHubPolicyKey"],
        ConfigurationManager.AppSettings["EventHubNamespace"],
        "servicebus.windows.net",
        ConfigurationManager.AppSettings["EventHubName"],
        "true"));

// Set hello bolt toosubscribe toodata from hello spout
topologyBuilder.SetJavaBolt(
    "eventhubbolt",
    constructor,
    partitionCount)
        .shuffleGrouping("Spout");
```

> [!NOTE]
> <span data-ttu-id="44502-140">Cet exemple utilise une expression Clojure transmise sous forme de chaîne au lieu d’utiliser **JavaComponentConstructor** toocreate un **EventHubBoltConfig**, comme l’exemple de bec hello a fait.</span><span class="sxs-lookup"><span data-stu-id="44502-140">This example uses a Clojure expression passed as a string, instead of using **JavaComponentConstructor** toocreate an **EventHubBoltConfig**, as hello spout example did.</span></span> <span data-ttu-id="44502-141">Les deux méthodes fonctionnent.</span><span class="sxs-lookup"><span data-stu-id="44502-141">Either method works.</span></span> <span data-ttu-id="44502-142">Utiliser la méthode hello qui vous semble la meilleure tooyou.</span><span class="sxs-lookup"><span data-stu-id="44502-142">Use hello method that feels best tooyou.</span></span>

## <a name="download-hello-completed-project"></a><span data-ttu-id="44502-143">Télécharger le projet de hello terminée</span><span class="sxs-lookup"><span data-stu-id="44502-143">Download hello completed project</span></span>

<span data-ttu-id="44502-144">Vous pouvez télécharger une version complète du projet hello créée dans ce didacticiel à partir de [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="44502-144">You can download a complete version of hello project created in this tutorial from [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span> <span data-ttu-id="44502-145">Toutefois, vous devez toujours les paramètres de configuration tooprovide en suivant les étapes de hello dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="44502-145">However, you still need tooprovide configuration settings by following hello steps in this tutorial.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="44502-146">Composants requis</span><span class="sxs-lookup"><span data-stu-id="44502-146">Prerequisites</span></span>

* <span data-ttu-id="44502-147">Un cluster [Apache Storm sur HDInsight version 3.5 ou 3.6](hdinsight-apache-storm-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="44502-147">An [Apache Storm on HDInsight cluster version 3.5 or 3.6](hdinsight-apache-storm-tutorial-get-started.md).</span></span>

    > [!WARNING]
    > <span data-ttu-id="44502-148">exemple Hello utilisé dans ce document requiert Storm sur HDInsight version 3.5 ou 3.6.</span><span class="sxs-lookup"><span data-stu-id="44502-148">hello example used in this document requires Storm on HDInsight version 3.5 or 3.6.</span></span> <span data-ttu-id="44502-149">Cela ne fonctionne pas avec les versions antérieures de HDInsight, en raison de changements de nom de classe toobreaking.</span><span class="sxs-lookup"><span data-stu-id="44502-149">This does not work with older versions of HDInsight, due toobreaking class name changes.</span></span> <span data-ttu-id="44502-150">Pour une version de cet exemple fonctionnant avec les anciens clusters, consultez [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub/releases).</span><span class="sxs-lookup"><span data-stu-id="44502-150">For a version of this example that works with older clusters, see [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub/releases).</span></span>

* <span data-ttu-id="44502-151">Un [concentrateur d’événements Azure](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="44502-151">An [Azure event hub](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

* <span data-ttu-id="44502-152">Hello [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="44502-152">hello [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span></span>

* <span data-ttu-id="44502-153">Hello [outils HDInsight pour Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="44502-153">hello [HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

* <span data-ttu-id="44502-154">Java JDK 1.8 ou version ultérieure sur votre environnement de développement.</span><span class="sxs-lookup"><span data-stu-id="44502-154">Java JDK 1.8 or later on your development environment.</span></span> <span data-ttu-id="44502-155">Les téléchargements JDK sont disponibles dans [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="44502-155">JDK downloads are available from [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>

  * <span data-ttu-id="44502-156">Hello **JAVA_HOME** environnement variable doit toohello de point de répertoire qui contient Java.</span><span class="sxs-lookup"><span data-stu-id="44502-156">hello **JAVA_HOME** environment variable must point toohello directory that contains Java.</span></span>
  * <span data-ttu-id="44502-157">Hello **%JAVA_HOME%/bin** répertoire doit être dans le chemin d’accès hello.</span><span class="sxs-lookup"><span data-stu-id="44502-157">hello **%JAVA_HOME%/bin** directory must be in hello path.</span></span>

## <a name="download-hello-event-hubs-components"></a><span data-ttu-id="44502-158">Télécharger les composants de concentrateurs d’événements hello</span><span class="sxs-lookup"><span data-stu-id="44502-158">Download hello Event Hubs components</span></span>

<span data-ttu-id="44502-159">Téléchargement hello concentrateurs d’événements bec et composant à partir de boulon [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span><span class="sxs-lookup"><span data-stu-id="44502-159">Download hello Event Hubs spout and bolt component from [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span></span>

<span data-ttu-id="44502-160">Créez un répertoire nommé `eventhubspout`et enregistrez le fichier de hello dans l’annuaire de hello.</span><span class="sxs-lookup"><span data-stu-id="44502-160">Create a directory named `eventhubspout`, and save hello file into hello directory.</span></span>

## <a name="configure-event-hubs"></a><span data-ttu-id="44502-161">Configurer les hubs d’événement</span><span class="sxs-lookup"><span data-stu-id="44502-161">Configure Event Hubs</span></span>

<span data-ttu-id="44502-162">Concentrateurs d’événements est la source de données de hello pour cet exemple.</span><span class="sxs-lookup"><span data-stu-id="44502-162">Event Hubs is hello data source for this example.</span></span> <span data-ttu-id="44502-163">Utilisez les informations de hello de section de « Créer un concentrateur d’événements » hello de [prise en main les concentrateurs d’événements](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="44502-163">Use hello information in hello "Create an event hub" section of [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

1. <span data-ttu-id="44502-164">Après avoir créé un concentrateur d’événements hello, afficher hello **EventHub** panneau Bonjour Azure portail, puis sélectionnez **les stratégies d’accès partagé**.</span><span class="sxs-lookup"><span data-stu-id="44502-164">After hello event hub has been created, view hello **EventHub** blade in hello Azure portal, and select **Shared access policies**.</span></span> <span data-ttu-id="44502-165">Sélectionnez **+ ajouter** hello tooadd suivant des stratégies :</span><span class="sxs-lookup"><span data-stu-id="44502-165">Select **+ Add** tooadd hello following policies:</span></span>

   | <span data-ttu-id="44502-166">Nom</span><span class="sxs-lookup"><span data-stu-id="44502-166">Name</span></span> | <span data-ttu-id="44502-167">Autorisations</span><span class="sxs-lookup"><span data-stu-id="44502-167">Permissions</span></span> |
   | --- | --- |
   | <span data-ttu-id="44502-168">writer</span><span class="sxs-lookup"><span data-stu-id="44502-168">writer</span></span> |<span data-ttu-id="44502-169">Envoyer</span><span class="sxs-lookup"><span data-stu-id="44502-169">Send</span></span> |
   | <span data-ttu-id="44502-170">reader</span><span class="sxs-lookup"><span data-stu-id="44502-170">reader</span></span> |<span data-ttu-id="44502-171">Écouter</span><span class="sxs-lookup"><span data-stu-id="44502-171">Listen</span></span> |

    ![Capture d’écran de la fenêtre de stratégies d’accès partagé](./media/hdinsight-storm-develop-csharp-event-hub-topology/sas.png)

2. <span data-ttu-id="44502-173">Sélectionnez hello **lecteur** et **writer** stratégies.</span><span class="sxs-lookup"><span data-stu-id="44502-173">Select hello **reader** and **writer** policies.</span></span> <span data-ttu-id="44502-174">Copiez et enregistrez la valeur de clé primaire hello pour les deux stratégies, car ces valeurs sont utilisées ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="44502-174">Copy and save hello primary key value for both policies, as these values are used later.</span></span>

## <a name="configure-hello-eventhubwriter"></a><span data-ttu-id="44502-175">Configurer hello EventHubWriter</span><span class="sxs-lookup"><span data-stu-id="44502-175">Configure hello EventHubWriter</span></span>

1. <span data-ttu-id="44502-176">Si vous n’avez pas déjà installé version la plus récente des outils de HDInsight hello hello pour Visual Studio, consultez [prise en main à l’aide des outils HDInsight pour Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="44502-176">If you have not already installed hello latest version of hello HDInsight tools for Visual Studio, see [Get started using HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

2. <span data-ttu-id="44502-177">Télécharger à partir de solution hello [eventhub-storm-hybride](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="44502-177">Download hello solution from [eventhub-storm-hybrid](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span>

3. <span data-ttu-id="44502-178">Bonjour **EventHubWriter** projet, ouvrez hello **App.config** fichier.</span><span class="sxs-lookup"><span data-stu-id="44502-178">In hello **EventHubWriter** project, open hello **App.config** file.</span></span> <span data-ttu-id="44502-179">Utilisez hello des informations à partir du concentrateur d’événements hello que vous avez configuré toofill antérieure dans la valeur hello pour hello suivant clés :</span><span class="sxs-lookup"><span data-stu-id="44502-179">Use hello information from hello event hub that you configured earlier toofill in hello value for hello following keys:</span></span>

   | <span data-ttu-id="44502-180">Clé</span><span class="sxs-lookup"><span data-stu-id="44502-180">Key</span></span> | <span data-ttu-id="44502-181">Valeur</span><span class="sxs-lookup"><span data-stu-id="44502-181">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="44502-182">EventHubPolicyName</span><span class="sxs-lookup"><span data-stu-id="44502-182">EventHubPolicyName</span></span> |<span data-ttu-id="44502-183">enregistreur (si vous avez utilisé un autre nom pour la stratégie hello avec *envoyer* autorisation, utilisez-le à la place.)</span><span class="sxs-lookup"><span data-stu-id="44502-183">writer (If you used a different name for hello policy with *Send* permission, use it instead.)</span></span> |
   | <span data-ttu-id="44502-184">EventHubPolicyKey</span><span class="sxs-lookup"><span data-stu-id="44502-184">EventHubPolicyKey</span></span> |<span data-ttu-id="44502-185">clé Hello pour la stratégie de writer hello.</span><span class="sxs-lookup"><span data-stu-id="44502-185">hello key for hello writer policy.</span></span> |
   | <span data-ttu-id="44502-186">eventHubNamespace</span><span class="sxs-lookup"><span data-stu-id="44502-186">EventHubNamespace</span></span> |<span data-ttu-id="44502-187">espace de noms Hello qui contient votre concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="44502-187">hello namespace that contains your event hub.</span></span> |
   | <span data-ttu-id="44502-188">eventHubName</span><span class="sxs-lookup"><span data-stu-id="44502-188">EventHubName</span></span> |<span data-ttu-id="44502-189">Le nom de votre concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="44502-189">Your event hub name.</span></span> |
   | <span data-ttu-id="44502-190">EventHubPartitionCount</span><span class="sxs-lookup"><span data-stu-id="44502-190">EventHubPartitionCount</span></span> |<span data-ttu-id="44502-191">nombre de Hello de partitions dans votre concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="44502-191">hello number of partitions in your event hub.</span></span> |

4. <span data-ttu-id="44502-192">Enregistrez et fermez hello **App.config** fichier.</span><span class="sxs-lookup"><span data-stu-id="44502-192">Save and close hello **App.config** file.</span></span>

## <a name="configure-hello-eventhubreader"></a><span data-ttu-id="44502-193">Configurer hello EventHubReader</span><span class="sxs-lookup"><span data-stu-id="44502-193">Configure hello EventHubReader</span></span>

1. <span data-ttu-id="44502-194">Ouvrez hello **EventHubReader** projet.</span><span class="sxs-lookup"><span data-stu-id="44502-194">Open hello **EventHubReader** project.</span></span>

2. <span data-ttu-id="44502-195">Ouvrez hello **App.config** fichier hello **EventHubReader**.</span><span class="sxs-lookup"><span data-stu-id="44502-195">Open hello **App.config** file for hello **EventHubReader**.</span></span> <span data-ttu-id="44502-196">Utilisez hello des informations à partir du concentrateur d’événements hello que vous avez configuré toofill antérieure dans la valeur hello pour hello suivant clés :</span><span class="sxs-lookup"><span data-stu-id="44502-196">Use hello information from hello event hub that you configured earlier toofill in hello value for hello following keys:</span></span>

   | <span data-ttu-id="44502-197">Clé</span><span class="sxs-lookup"><span data-stu-id="44502-197">Key</span></span> | <span data-ttu-id="44502-198">Valeur</span><span class="sxs-lookup"><span data-stu-id="44502-198">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="44502-199">EventHubPolicyName</span><span class="sxs-lookup"><span data-stu-id="44502-199">EventHubPolicyName</span></span> |<span data-ttu-id="44502-200">lecteur (si vous avez utilisé un autre nom pour la stratégie hello avec *écouter* autorisation, utilisez-le à la place.)</span><span class="sxs-lookup"><span data-stu-id="44502-200">reader (If you used a different name for hello policy with *listen* permission, use it instead.)</span></span> |
   | <span data-ttu-id="44502-201">EventHubPolicyKey</span><span class="sxs-lookup"><span data-stu-id="44502-201">EventHubPolicyKey</span></span> |<span data-ttu-id="44502-202">clé Hello pour la stratégie de lecteur hello.</span><span class="sxs-lookup"><span data-stu-id="44502-202">hello key for hello reader policy.</span></span> |
   | <span data-ttu-id="44502-203">eventHubNamespace</span><span class="sxs-lookup"><span data-stu-id="44502-203">EventHubNamespace</span></span> |<span data-ttu-id="44502-204">espace de noms Hello qui contient votre concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="44502-204">hello namespace that contains your event hub.</span></span> |
   | <span data-ttu-id="44502-205">eventHubName</span><span class="sxs-lookup"><span data-stu-id="44502-205">EventHubName</span></span> |<span data-ttu-id="44502-206">Le nom de votre concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="44502-206">Your event hub name.</span></span> |
   | <span data-ttu-id="44502-207">EventHubPartitionCount</span><span class="sxs-lookup"><span data-stu-id="44502-207">EventHubPartitionCount</span></span> |<span data-ttu-id="44502-208">nombre de Hello de partitions dans votre concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="44502-208">hello number of partitions in your event hub.</span></span> |

3. <span data-ttu-id="44502-209">Enregistrez et fermez hello **App.config** fichier.</span><span class="sxs-lookup"><span data-stu-id="44502-209">Save and close hello **App.config** file.</span></span>

## <a name="deploy-hello-topologies"></a><span data-ttu-id="44502-210">Déployer des topologies de hello</span><span class="sxs-lookup"><span data-stu-id="44502-210">Deploy hello topologies</span></span>

1. <span data-ttu-id="44502-211">À partir de **l’Explorateur de solutions**, avec le bouton hello **EventHubReader** le projet, puis sélectionnez **envoyer tooStorm sur HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="44502-211">From **Solution Explorer**, right-click hello **EventHubReader** project, and select **Submit tooStorm on HDInsight**.</span></span>

    ![Capture d’écran d’Explorateur de solutions, avec tooStorm envoyer sur HDInsight mis en surbrillance](./media/hdinsight-storm-develop-csharp-event-hub-topology/submittostorm.png)

2. <span data-ttu-id="44502-213">Sur hello **soumettre une topologie** boîte de dialogue, sélectionnez votre **Cluster Storm**.</span><span class="sxs-lookup"><span data-stu-id="44502-213">On hello **Submit Topology** dialog box, select your **Storm Cluster**.</span></span> <span data-ttu-id="44502-214">Développez **des Configurations supplémentaires**, sélectionnez **chemins d’accès de Java**, sélectionnez **...** et sélectionnez hello répertoire qui contient le fichier JAR hello que vous avez téléchargé précédemment.</span><span class="sxs-lookup"><span data-stu-id="44502-214">Expand **Additional Configurations**, select **Java File Paths**, select **...**, and select hello directory that contains hello JAR file that you downloaded earlier.</span></span> <span data-ttu-id="44502-215">Pour finir, cliquez sur **Envoyer**.</span><span class="sxs-lookup"><span data-stu-id="44502-215">Finally, click **Submit**.</span></span>

    ![Capture d’écran de la boîte de dialogue Envoyer la topologie](./media/hdinsight-storm-develop-csharp-event-hub-topology/submit.png)

3. <span data-ttu-id="44502-217">Lors de la topologie de hello a été envoyée, hello **Storm Topologies visionneuse** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="44502-217">When hello topology has been submitted, hello **Storm Topologies Viewer** appears.</span></span> <span data-ttu-id="44502-218">tooview plus d’informations sur la topologie de hello, sélectionnez hello **EventHubReader** topologie dans le volet gauche de hello.</span><span class="sxs-lookup"><span data-stu-id="44502-218">tooview information about hello topology, select hello **EventHubReader** topology in hello left pane.</span></span>

    ![Capture d’écran de la visionneuse de topologies Storm](./media/hdinsight-storm-develop-csharp-event-hub-topology/topologyviewer.png)

4. <span data-ttu-id="44502-220">À partir de **l’Explorateur de solutions**, avec le bouton hello **EventHubWriter** le projet, puis sélectionnez **envoyer tooStorm sur HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="44502-220">From **Solution Explorer**, right-click hello **EventHubWriter** project, and select **Submit tooStorm on HDInsight**.</span></span>

5. <span data-ttu-id="44502-221">Sur hello **soumettre une topologie** boîte de dialogue, sélectionnez votre **Cluster Storm**.</span><span class="sxs-lookup"><span data-stu-id="44502-221">On hello **Submit Topology** dialog box, select your **Storm Cluster**.</span></span> <span data-ttu-id="44502-222">Développez **des Configurations supplémentaires**, sélectionnez **chemins d’accès de Java**, sélectionnez **...** , et le répertoire hello select qui contient le fichier JAR hello que vous avez téléchargé précédemment.</span><span class="sxs-lookup"><span data-stu-id="44502-222">Expand **Additional Configurations**, select **Java File Paths**, select **...**, and select hello directory that contains hello JAR file you downloaded earlier.</span></span> <span data-ttu-id="44502-223">Pour finir, cliquez sur **Envoyer**.</span><span class="sxs-lookup"><span data-stu-id="44502-223">Finally, click **Submit**.</span></span>

6. <span data-ttu-id="44502-224">Lors de la topologie de hello a été envoyée, actualisez la liste de topologie de hello Bonjour **Storm Topologies visionneuse** tooverify les deux topologies sont en cours d’exécution sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="44502-224">When hello topology has been submitted, refresh hello topology list in hello **Storm Topologies Viewer** tooverify that both topologies are running on hello cluster.</span></span>

7. <span data-ttu-id="44502-225">Dans **Storm Topologies visionneuse**, sélectionnez hello **EventHubReader** topologie.</span><span class="sxs-lookup"><span data-stu-id="44502-225">In **Storm Topologies Viewer**, select hello **EventHubReader** topology.</span></span>

8. <span data-ttu-id="44502-226">composant de hello tooopen résumé d’éclair de hello, double-cliquez sur hello **LogBolt** composant dans le diagramme de hello.</span><span class="sxs-lookup"><span data-stu-id="44502-226">tooopen hello component summary for hello bolt, double-click hello **LogBolt** component in hello diagram.</span></span>

9. <span data-ttu-id="44502-227">Bonjour **exécuteurs** , sélectionnez un des liens de hello Bonjour **Port** colonne.</span><span class="sxs-lookup"><span data-stu-id="44502-227">In hello **Executors** section, select one of hello links in hello **Port** column.</span></span> <span data-ttu-id="44502-228">Affiche les informations enregistrées par le composant hello.</span><span class="sxs-lookup"><span data-stu-id="44502-228">This displays information logged by hello component.</span></span> <span data-ttu-id="44502-229">les informations de Hello connecté sont similaires toohello suivant du texte :</span><span class="sxs-lookup"><span data-stu-id="44502-229">hello logged information is similar toohello following text:</span></span>

        2017-03-02 14:51:29.255 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,255 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1830978598,"deviceId":"8566ccbc-034d-45db-883d-d8a31f34068e"}
        2017-03-02 14:51:29.283 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,283 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1756413275,"deviceId":"647a5eff-823d-482f-a8b4-b95b35ae570b"}
        2017-03-02 14:51:29.313 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,312 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1108478910,"deviceId":"206a68fa-8264-4d61-9100-bfdb68ee8f0a"}

## <a name="stop-hello-topologies"></a><span data-ttu-id="44502-230">Arrêter les topologies hello</span><span class="sxs-lookup"><span data-stu-id="44502-230">Stop hello topologies</span></span>

<span data-ttu-id="44502-231">topologies de hello toostop, sélectionnez chaque topologie Bonjour **visionneuse de topologie Storm**, puis cliquez sur **Kill**.</span><span class="sxs-lookup"><span data-stu-id="44502-231">toostop hello topologies, select each topology in hello **Storm Topology Viewer**, then click **Kill**.</span></span>

![Capture d’écran de la visionneuse de topologies Storm avec le bouton Supprimer mis en surbrillance](./media/hdinsight-storm-develop-csharp-event-hub-topology/killtopology.png)

## <a name="delete-your-cluster"></a><span data-ttu-id="44502-233">Supprimer votre cluster</span><span class="sxs-lookup"><span data-stu-id="44502-233">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="44502-234">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="44502-234">Next steps</span></span>

<span data-ttu-id="44502-235">Dans ce document, vous avez appris comment toouse de concentrateurs d’événements Java hello bec et boulon à partir d’un toowork topologie c# avec des données dans Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="44502-235">In this document, you have learned how toouse hello Java Event Hubs spout and bolt from a C# topology toowork with data in Azure Event Hubs.</span></span> <span data-ttu-id="44502-236">toolearn plus sur la création de topologies de c#, voir hello :</span><span class="sxs-lookup"><span data-stu-id="44502-236">toolearn more about creating C# topologies, see hello following:</span></span>

* [<span data-ttu-id="44502-237">Développement de topologies C# pour Apache Storm dans HDInsight à l'aide de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="44502-237">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="44502-238">Guide de programmation SCP</span><span class="sxs-lookup"><span data-stu-id="44502-238">SCP programming guide</span></span>](hdinsight-storm-scp-programming-guide.md)
* [<span data-ttu-id="44502-239">Exemples de topologies pour Storm dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="44502-239">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
