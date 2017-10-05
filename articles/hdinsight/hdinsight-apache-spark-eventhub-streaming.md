---
title: Utiliser une diffusion en continu Apache Spark avec Event Hubs dans Azure HDInsight | Documents Microsoft
description: "Créez un Exemple de diffusion en continu Apache Spark montrant comment envoyer un flux de données à Azure Event Hub, puis recevoir ces événements dans un cluster Spark HDInsight à l’aide d’une application Scala."
keywords: diffusion en continu apache spark,diffusion en continu spark, exemple spark,exemple de diffusion en continu apache spark,exemple azure event hubs
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 68894e75-3ffa-47bd-8982-96cdad38b7d0
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: 175a2ad70b1f554d05846eb62fb685d4f259af7e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="apache-spark-streaming-process-data-from-azure-event-hubs-with-spark-cluster-on-hdinsight"></a><span data-ttu-id="122d8-104">Diffusion en continu Apache Spark : traitement de données d’Azure Event Hubs avec un cluster Spark sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="122d8-104">Apache Spark streaming: Process data from Azure Event Hubs with Spark cluster on HDInsight</span></span>

<span data-ttu-id="122d8-105">Dans le cadre de cet article, vous allez créer un exemple de diffusion en continu Apache Spark qui implique les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="122d8-105">In this article, you create an Apache Spark streaming sample that involves the following steps:</span></span>

1. <span data-ttu-id="122d8-106">Vous utilisez une application autonome pour ingérer les messages dans Azure Event Hub.</span><span class="sxs-lookup"><span data-stu-id="122d8-106">You use a standalone application to ingest messages into an Azure Event Hub.</span></span>

2. <span data-ttu-id="122d8-107">Avec deux approches différentes, vous récupérez les messages d’Event Hub en temps réel à l’aide d’une application s’exécutant dans le cluster Spark sur Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="122d8-107">With two different approaches, you retrieve the messages from Event Hub in real-time using an application running in Spark cluster on Azure HDInsight.</span></span>

3. <span data-ttu-id="122d8-108">Vous générez des pipelines analytiques de diffusion en continu pour conserver les données dans différents systèmes de stockage ou obtenir en un clin d’œil des insights à partir des données.</span><span class="sxs-lookup"><span data-stu-id="122d8-108">You build streaming analytic pipelines to persist data to different storage systems, or get insights from data on the fly.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="122d8-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="122d8-109">Prerequisites</span></span>

* <span data-ttu-id="122d8-110">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="122d8-110">An Azure subscription.</span></span> <span data-ttu-id="122d8-111">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="122d8-111">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="122d8-112">Un cluster Apache Spark sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="122d8-112">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="122d8-113">Pour obtenir des instructions, consultez [Création de clusters Apache Spark dans Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="122d8-113">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="spark-streaming-concepts"></a><span data-ttu-id="122d8-114">Concepts de la diffusion en continu de Spark</span><span class="sxs-lookup"><span data-stu-id="122d8-114">Spark Streaming concepts</span></span>

<span data-ttu-id="122d8-115">Pour obtenir une explication détaillée de la diffusion en continu Spark, voir la [présentation de la diffusion en continu Apache Spark](http://spark.apache.org/docs/latest/streaming-programming-guide.html#overview).</span><span class="sxs-lookup"><span data-stu-id="122d8-115">For a detailed explanation of Spark streaming, see [Apache Spark streaming overview](http://spark.apache.org/docs/latest/streaming-programming-guide.html#overview).</span></span> <span data-ttu-id="122d8-116">HDInsight apporte les mêmes fonctionnalités de diffusion en continu à un cluster Spark sur Azure.</span><span class="sxs-lookup"><span data-stu-id="122d8-116">HDInsight brings the same streaming features to a Spark cluster on Azure.</span></span>  

## <a name="what-does-this-solution-do"></a><span data-ttu-id="122d8-117">Que fait cette solution ?</span><span class="sxs-lookup"><span data-stu-id="122d8-117">What does this solution do?</span></span>

<span data-ttu-id="122d8-118">Dans cet article, pour créer un exemple de diffusion en continu Spark, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="122d8-118">In this article, to create a Spark streaming example, perform the following steps:</span></span>

1. <span data-ttu-id="122d8-119">Créez un Event Hub Azure qui doit recevoir un flux d’événements.</span><span class="sxs-lookup"><span data-stu-id="122d8-119">Create an Azure Event Hub that will receive a stream of events.</span></span>

2. <span data-ttu-id="122d8-120">Exécutez une application autonome locale qui génère des événements et les envoie à Azure Event Hub.</span><span class="sxs-lookup"><span data-stu-id="122d8-120">Run a local standalone application that generates events and pushes it to the Azure Event Hub.</span></span> <span data-ttu-id="122d8-121">L’exemple d’application qui effectue cette opération est publié à l’adresse [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span><span class="sxs-lookup"><span data-stu-id="122d8-121">The sample application that does this is published at [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span></span>

3. <span data-ttu-id="122d8-122">Exécutez une application de diffusion en continu à distance sur un cluster Spark qui lit les événements de diffusion en continu à partir d’Azure Event Hub et effectuez diverses tâches de traitement/d’analyse des données.</span><span class="sxs-lookup"><span data-stu-id="122d8-122">Run a streaming application remotely on a Spark cluster that reads streaming events from Azure Event Hub and perform various data processing/analysis.</span></span>

## <a name="create-an-azure-event-hub"></a><span data-ttu-id="122d8-123">Création d'un hub d'événements Azure</span><span class="sxs-lookup"><span data-stu-id="122d8-123">Create an Azure Event Hub</span></span>

1. <span data-ttu-id="122d8-124">Connectez-vous au [portail Azure](https://ms.portal.azure.com), puis cliquez sur **Nouveau** en haut à gauche de l’écran.</span><span class="sxs-lookup"><span data-stu-id="122d8-124">Log on to the [Azure Portal](https://ms.portal.azure.com), and click **New** at the top left of the screen.</span></span>

2. <span data-ttu-id="122d8-125">Cliquez sur **Internet des Objets**, puis sur **Hubs d’événements**.</span><span class="sxs-lookup"><span data-stu-id="122d8-125">Click **Internet of Things**, then click **Event Hubs**.</span></span>

    <span data-ttu-id="122d8-126">![Créer un Event Hub pour un exemple de diffusion en continu Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-create-event-hub-for-spark-streaming.png "Créer un Event Hub pour un exemple de diffusion en continu Spark")</span><span class="sxs-lookup"><span data-stu-id="122d8-126">![Create event hub for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-create-event-hub-for-spark-streaming.png "Create event hub for Spark streaming example")</span></span>

3. <span data-ttu-id="122d8-127">Dans le panneau **Créer un espace de noms** , entrez un nom d’espace de noms.</span><span class="sxs-lookup"><span data-stu-id="122d8-127">In the **Create namespace** blade, enter a namespace name.</span></span> <span data-ttu-id="122d8-128">Choisissez le niveau tarifaire (De base ou Standard).</span><span class="sxs-lookup"><span data-stu-id="122d8-128">choose the pricing tier (Basic or Standard).</span></span> <span data-ttu-id="122d8-129">Choisissez également un abonnement Azure, un groupe de ressources et l’emplacement où créer la ressource.</span><span class="sxs-lookup"><span data-stu-id="122d8-129">Also, choose an Azure subscription, resource group, and location in which to create the resource.</span></span> <span data-ttu-id="122d8-130">Cliquez sur **Créer** pour créer l’espace de noms.</span><span class="sxs-lookup"><span data-stu-id="122d8-130">Click **Create** to create the namespace.</span></span>

      <span data-ttu-id="122d8-131">![Fournir un nom d’Event Hub pour un exemple de diffusion en continu Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-name-for-spark-streaming.png "Fournir un nom d’Event Hub pour un exemple de diffusion en continu Spark")</span><span class="sxs-lookup"><span data-stu-id="122d8-131">![Provide an event hub name for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-name-for-spark-streaming.png "Provide an event hub name for Spark streaming example")</span></span>

    > [!NOTE]
    > <span data-ttu-id="122d8-132">Vous devez sélectionner le même **emplacement** que celui de votre cluster Apache Spark dans HDInsight pour réduire la latence et les coûts.</span><span class="sxs-lookup"><span data-stu-id="122d8-132">You should select the same **Location** as your Apache Spark cluster in HDInsight to reduce latency and costs.</span></span>
    >
    >

4. <span data-ttu-id="122d8-133">Dans la liste d’espaces de noms Event Hubs, cliquez sur l’espace de noms créé.</span><span class="sxs-lookup"><span data-stu-id="122d8-133">In the Event Hubs namespace list, click the newly-created namespace.</span></span>      


5. <span data-ttu-id="122d8-134">Dans le panneau d’espace de noms, cliquez sur **Event Hubs**, puis sur **+ Event Hub** pour créer un concentrateur Event Hub.</span><span class="sxs-lookup"><span data-stu-id="122d8-134">In the namespace blade, click **Event Hubs**, and then click **+ Event Hub** to create a new Event Hub.</span></span>
   
    <span data-ttu-id="122d8-135">![Créer un Event Hub pour un exemple de diffusion en continu Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-open-event-hubs-blade-for-spark-streaming-example.png "Créer un Event Hub pour un exemple de diffusion en continu Spark")</span><span class="sxs-lookup"><span data-stu-id="122d8-135">![Create event hub for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-open-event-hubs-blade-for-spark-streaming-example.png "Create event hub for Spark streaming example")</span></span>

6. <span data-ttu-id="122d8-136">Tapez un nom pour votre concentrateur Event Hub, puis définissez le nombre de partitions sur 10 et la rétention des messages sur 1.</span><span class="sxs-lookup"><span data-stu-id="122d8-136">Type a name for your Event Hub, set the partition count to 10, and message retention to 1.</span></span> <span data-ttu-id="122d8-137">Étant donné que nous n’archivons pas les messages dans cette solution, vous pouvez laisser la suite telle qu’elle est définie par défaut, puis cliquer sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="122d8-137">We are not archiving the messages in this solution so you can leave the rest as default, and then click **Create**.</span></span>
   
    <span data-ttu-id="122d8-138">![Fournir des détails d’Event Hub pour un exemple de diffusion en continu Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-details-for-spark-streaming-example.png "Fournir des détails d’Event Hub pour un exemple de diffusion en continu Spark")</span><span class="sxs-lookup"><span data-stu-id="122d8-138">![Provide event hub details for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-details-for-spark-streaming-example.png "Provide event hub details for Spark streaming example")</span></span>

7. <span data-ttu-id="122d8-139">Le concentrateur Event Hub que vous venez de créer est répertorié dans le panneau Event Hub.</span><span class="sxs-lookup"><span data-stu-id="122d8-139">The newly created Event Hub is listed in the Event Hub blade.</span></span>
    
     <span data-ttu-id="122d8-140">![Afficher un Event Hub pour l’exemple de diffusion en continu Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-for-spark-streaming-example.png "Afficher un Event Hub pour l’exemple de diffusion en continu Spark")</span><span class="sxs-lookup"><span data-stu-id="122d8-140">![View Event Hub for the Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-for-spark-streaming-example.png "View Event Hub for the Spark streaming example")</span></span>

8. <span data-ttu-id="122d8-141">Revenez au panneau de l’espace de noms (pas le panneau de l’Event Hub spécifique), cliquez sur **Stratégies d’accès partagé**, puis sur **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="122d8-141">Back in the namespace blade (not the specific Event Hub blade), click **Shared access policies**, and then click **RootManageSharedAccessKey**.</span></span>
    
     <span data-ttu-id="122d8-142">![Définir des stratégies d’Event Hub pour l’exemple de diffusion en continu Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-set-event-hub-policies-for-spark-streaming-example.png "Définir des stratégies d’Event Hub pour l’exemple de diffusion en continu Spark")</span><span class="sxs-lookup"><span data-stu-id="122d8-142">![Set Event Hub policies for the Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-set-event-hub-policies-for-spark-streaming-example.png "Set Event Hub policies for the Spark streaming example")</span></span>

9. <span data-ttu-id="122d8-143">Cliquez sur le bouton Copier pour copier la chaîne de connexion et la clé primaire **RootManageSharedAccessKey** dans le Presse-papiers.</span><span class="sxs-lookup"><span data-stu-id="122d8-143">Click the copy button to copy the **RootManageSharedAccessKey** primary key and connection string to the clipboard.</span></span> <span data-ttu-id="122d8-144">Enregistrez-les pour les utiliser ultérieurement dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="122d8-144">Save these to use later in the tutorial.</span></span>
    
     <span data-ttu-id="122d8-145">![Afficher des clés de stratégie d’Event Hub pour l’exemple de diffusion en continu Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-policy-keys.png "Afficher des clés de stratégie d’Event Hub pour l’exemple de diffusion en continu Spark")</span><span class="sxs-lookup"><span data-stu-id="122d8-145">![View Event Hub policy keys for the Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-policy-keys.png "View Event Hub policy keys for the Spark streaming example")</span></span>

## <a name="send-messages-to-azure-event-hub-using-a-sample-scala-application"></a><span data-ttu-id="122d8-146">Envoyer des messages à un Azure Event Hub à l’aide d’un exemple d’application Scala</span><span class="sxs-lookup"><span data-stu-id="122d8-146">Send messages to Azure Event Hub using a sample Scala application</span></span>

<span data-ttu-id="122d8-147">Dans cette section, vous allez utiliser une application Scala locale autonome qui génère un flux d’événements et envoie celui-ci à l’Azure Event Hub que vous avez créé à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="122d8-147">In this section you use a standalone local Scala application that generates a stream of events and sends it to Azure Event Hub that you created earlier.</span></span> <span data-ttu-id="122d8-148">Cette application est disponible sur GitHub à l’adresse [https://github.com/hdinsight/eventhubs-sample-event-producer](https://github.com/hdinsight/eventhubs-sample-event-producer).</span><span class="sxs-lookup"><span data-stu-id="122d8-148">This application is available on GitHub at [https://github.com/hdinsight/eventhubs-sample-event-producer](https://github.com/hdinsight/eventhubs-sample-event-producer).</span></span> <span data-ttu-id="122d8-149">Les étapes décrites ici supposent que vous avez déjà dupliqué ce dépôt GitHub.</span><span class="sxs-lookup"><span data-stu-id="122d8-149">The steps here assume that you have already forked this GitHub repository.</span></span>

1. <span data-ttu-id="122d8-150">Veillez à installer les éléments suivants sur l’ordinateur sur lequel vous exécutez cette application.</span><span class="sxs-lookup"><span data-stu-id="122d8-150">Make sure you have the following installed on the computer where you run this application.</span></span>

    * <span data-ttu-id="122d8-151">Kit de développement logiciel (SDK) Oracle Java.</span><span class="sxs-lookup"><span data-stu-id="122d8-151">Oracle Java Development kit.</span></span> <span data-ttu-id="122d8-152">Vous pouvez l’installer à partir d’ [ici](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="122d8-152">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
    * <span data-ttu-id="122d8-153">Apache Maven.</span><span class="sxs-lookup"><span data-stu-id="122d8-153">Apache Maven.</span></span> <span data-ttu-id="122d8-154">Vous pouvez le télécharger [ici](https://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="122d8-154">You can download it from [here](https://maven.apache.org/download.cgi).</span></span> <span data-ttu-id="122d8-155">Les instructions d’installation de Maven sont disponibles [ici](https://maven.apache.org/install.html).</span><span class="sxs-lookup"><span data-stu-id="122d8-155">Instructions to install Maven are available [here](https://maven.apache.org/install.html).</span></span>

2. <span data-ttu-id="122d8-156">Ouvrez une invite de commandes et accédez à l’emplacement où vous avez cloné le référentiel GitHub pour l’exemple d’application Scala et exécutez la commande suivante pour générer l’application.</span><span class="sxs-lookup"><span data-stu-id="122d8-156">Open a command prompt and navigate to the location you cloned the GitHub repo for the sample Scala application and run the following command to build the application.</span></span>

        mvn package

3. <span data-ttu-id="122d8-157">Le fichier jar de sortie de l’application, **com-microsoft-azure-eventhubs-client-example-0.2.0.jar**, est créé dans le répertoire **/target**.</span><span class="sxs-lookup"><span data-stu-id="122d8-157">The output jar for the application, **com-microsoft-azure-eventhubs-client-example-0.2.0.jar**, is created under **/target** directory.</span></span> <span data-ttu-id="122d8-158">Ce fichier JAR sera utilisé plus loin dans cet article pour tester la solution.</span><span class="sxs-lookup"><span data-stu-id="122d8-158">You use this JAR later in this article to test the complete solution.</span></span>

## <a name="create-application-to-receive-messages-from-event-hub-into-a-spark-cluster"></a><span data-ttu-id="122d8-159">Créer une application pour recevoir des messages d’Event Hub dans un cluster Spark</span><span class="sxs-lookup"><span data-stu-id="122d8-159">Create application to receive messages from Event Hub into a Spark cluster</span></span> 

<span data-ttu-id="122d8-160">Nous disposons de deux approches pour connecter Spark Streaming et Azure Event Hubs : la connexion basée sur récepteur et la connexion basée sur Direct-DStream.</span><span class="sxs-lookup"><span data-stu-id="122d8-160">We have two approaches to connect Spark Streaming and Azure Event Hubs, Receiver-based connection and Direct-DStream-based connection.</span></span> <span data-ttu-id="122d8-161">La connexion basée sur Direct-DStream a été introduite dans la version 2.0.3 en janvier 2017.</span><span class="sxs-lookup"><span data-stu-id="122d8-161">Direct-DStream-based is introduced on Jan of 2017, in the 2.0.3 release.</span></span> <span data-ttu-id="122d8-162">Elle est supposée remplacer la connexion d’origine basée sur récepteur, car elle est plus performante et plus efficace en matière de ressources.</span><span class="sxs-lookup"><span data-stu-id="122d8-162">It is supposed to replace the original receiver-based connection as it is more performant and resource-efficient.</span></span> <span data-ttu-id="122d8-163">Vous trouverez plus de détails à l’adresse [https://github.com/hdinsight/spark-eventhubs](https://github.com/hdinsight/spark-eventhubs).</span><span class="sxs-lookup"><span data-stu-id="122d8-163">More details found in [https://github.com/hdinsight/spark-eventhubs](https://github.com/hdinsight/spark-eventhubs).</span></span> <span data-ttu-id="122d8-164">Direct DStream prend uniquement en charge Spark 2.0+.</span><span class="sxs-lookup"><span data-stu-id="122d8-164">Direct DStream only supports Spark 2.0+.</span></span>

### <a name="build-applications-with-the-dependency-to-spark-eventhubs-connector"></a><span data-ttu-id="122d8-165">Générer des applications avec une dépendance au connecteur spark-eventhubs</span><span class="sxs-lookup"><span data-stu-id="122d8-165">Build applications with the dependency to spark-eventhubs connector</span></span>

<span data-ttu-id="122d8-166">Nous publierons également la version intermédiaire de Spark-EventHubs dans GitHub.</span><span class="sxs-lookup"><span data-stu-id="122d8-166">We will also publish the staging version of Spark-EventHubs in GitHub.</span></span> <span data-ttu-id="122d8-167">Pour utiliser la version intermédiaire de Spark-EventHubs, la première étape consiste à indiquer GitHub en tant que référentiel source en ajoutant l’entrée suivante dans le fichier pom.xml :</span><span class="sxs-lookup"><span data-stu-id="122d8-167">To use the staging version of Spark-EventHubs, the first step is to indicate GitHub as the source repo by adding the following entry to pom.xml:</span></span>

```xml
<repository>
      <id>spark-eventhubs</id>
      <url>https://raw.github.com/hdinsight/spark-eventhubs/maven-repo/</url>
      <snapshots>
        <enabled>true</enabled>
        <updatePolicy>always</updatePolicy>
      </snapshots>
</repository>
```

<span data-ttu-id="122d8-168">Vous pouvez ensuite ajouter les dépendances suivantes à votre projet pour prendre la préversion.</span><span class="sxs-lookup"><span data-stu-id="122d8-168">You can then add the following dependency to your project to take the pre-released version.</span></span>

<span data-ttu-id="122d8-169">Dépendance Maven</span><span class="sxs-lookup"><span data-stu-id="122d8-169">Maven Dependency</span></span>

```xml
<!-- https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11 -->
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>spark-streaming-eventhubs_2.11</artifactId>
    <version>2.0.4</version>
</dependency>
```

<span data-ttu-id="122d8-170">Dépendance SBT</span><span class="sxs-lookup"><span data-stu-id="122d8-170">SBT Dependency</span></span>

```
// https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11
libraryDependencies += "com.microsoft.azure" % "spark-streaming-eventhubs_2.11" % "2.0.4"
```

### <a name="direct-dstream-connection"></a><span data-ttu-id="122d8-171">Connexion Direct DStream</span><span class="sxs-lookup"><span data-stu-id="122d8-171">Direct DStream Connection</span></span>

<span data-ttu-id="122d8-172">Un fichier jar prégénéré contenant des exemples utilisant Direct DStream peut être téléchargé dans [http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar](http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar).</span><span class="sxs-lookup"><span data-stu-id="122d8-172">A pre-built jar file containing examples using Direct DStream can be downloaded in [http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar](http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar).</span></span>

<span data-ttu-id="122d8-173">Le fichier jar contient trois exemples dont le code source est disponible à l’adresse [https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream](https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream).</span><span class="sxs-lookup"><span data-stu-id="122d8-173">The jar file contains three examples whose source code are available at [https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream](https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream).</span></span>

<span data-ttu-id="122d8-174">Utilisons [WindowingWordCount](https://github.com/hdinsight/spark-eventhubs/blob/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream/WindowingWordCount.scala) comme exemple :</span><span class="sxs-lookup"><span data-stu-id="122d8-174">Taking [WindowingWordCount](https://github.com/hdinsight/spark-eventhubs/blob/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream/WindowingWordCount.scala) as an example:</span></span>

```scala
private def createStreamingContext(
  sparkCheckpointDir: String,
  batchDuration: Int,
  namespace: String,
  eventHunName: String,
  eventhubParams: Map[String, String],
  progressDir: String) = {
val ssc = new StreamingContext(new SparkContext(), Seconds(batchDuration))
ssc.checkpoint(sparkCheckpointDir)
val inputDirectStream = EventHubsUtils.createDirectStreams(
  ssc,
  namespace,
  progressDir,
  Map(eventHunName -> eventhubParams))

inputDirectStream.map(receivedRecord => (new String(receivedRecord.getBody), 1)).
  reduceByKeyAndWindow((v1, v2) => v1 + v2, (v1, v2) => v1 - v2, Seconds(batchDuration * 3),
    Seconds(batchDuration)).print()

ssc
}

def main(args: Array[String]): Unit = {

if (args.length != 8) {
  println("Usage: program progressDir PolicyName PolicyKey EventHubNamespace EventHubName" +
    " BatchDuration(seconds) Spark_Checkpoint_Directory maxRate")
  sys.exit(1)
}

val progressDir = args(0)
val policyName = args(1)
val policykey = args(2)
val namespace = args(3)
val name = args(4)
val batchDuration = args(5).toInt
val sparkCheckpointDir = args(6)
val maxRate = args(7)

val eventhubParameters = Map[String, String] (
  "eventhubs.policyname" -> policyName,
  "eventhubs.policykey" -> policykey,
  "eventhubs.namespace" -> namespace,
  "eventhubs.name" -> name,
  "eventhubs.partition.count" -> "32",
  "eventhubs.consumergroup" -> "$Default",
  "eventhubs.maxRate" -> s"$maxRate"
)

val ssc = StreamingContext.getOrCreate(sparkCheckpointDir,
  () => createStreamingContext(sparkCheckpointDir, batchDuration, namespace, name,
    eventhubParameters, progressDir))

ssc.start()
ssc.awaitTermination()
}
```

<span data-ttu-id="122d8-175">Dans l’exemple ci-dessus, `eventhubParameters` sont les paramètres spécifiques à une seule instance EventHubs et vous devez les transférer à l’API `createDirectStreams` qui construit un mappage d’objet Direct DStream à un espace de noms Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="122d8-175">In the above example, `eventhubParameters` are the parameters specific to a single EventHubs instance and you have to pass it to the `createDirectStreams` API which constructs a Direct DStream object mapping to a Event Hubs namespace.</span></span> <span data-ttu-id="122d8-176">Sur l’objet Direct DStream, vous pouvez appeler n’importe quelle API DStream fournie par le framework d’API Spark Streaming.</span><span class="sxs-lookup"><span data-stu-id="122d8-176">Over the Direct DStream object, you can call any DStream API provided by Spark Streaming API framework.</span></span> <span data-ttu-id="122d8-177">Dans cet exemple, nous calculons la fréquence de chaque mot dans les 3 micro-intervalles de lot.</span><span class="sxs-lookup"><span data-stu-id="122d8-177">In this example, we calculate the frequency of each word within the last 3 micro batch intervals.</span></span>

### <a name="receiver-based-connection"></a><span data-ttu-id="122d8-178">Connexion basée sur récepteur</span><span class="sxs-lookup"><span data-stu-id="122d8-178">Receiver-based Connection</span></span>

<span data-ttu-id="122d8-179">Un exemple d’application de diffusion en continu Spark écrite en Scala, qui reçoit des événements et les achemine vers différentes destinations est disponible à l’adresse [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span><span class="sxs-lookup"><span data-stu-id="122d8-179">A Spark streaming example application written in Scala, which receives events and route the to different destinations, is available at [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span></span> <span data-ttu-id="122d8-180">Suivez les étapes ci-dessous pour mettre à jour l’application pour la configuration de votre Event Hub et créer le fichier jar de sortie.</span><span class="sxs-lookup"><span data-stu-id="122d8-180">Follow the steps below to update the application for your Event Hub configuration and create the output jar.</span></span>

1. <span data-ttu-id="122d8-181">Lancez IntelliJ IDEA, sélectionnez **Check out from Version Control** (Extraire du contrôle de version) dans l’écran de démarrage, puis cliquez sur **Git**.</span><span class="sxs-lookup"><span data-stu-id="122d8-181">Launch IntelliJ IDEA and from the launch screen select **Check out from Version Control** and then click **Git**.</span></span>
   
    <span data-ttu-id="122d8-182">![Exemple de diffusion en continu Apache Spark - obtenir des sources de Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-get-source-from-git.png "Exemple de diffusion en continu Apache Spark - obtenir des sources de Git")</span><span class="sxs-lookup"><span data-stu-id="122d8-182">![Apache Spark streaming example - get sources from Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-get-source-from-git.png "Apache Spark streaming example - get sources from Git")</span></span>

2. <span data-ttu-id="122d8-183">Dans la boîte de dialogue **Clone Repository** (Cloner le dépôt), entrez l’URL du dépôt Git à partir duquel opérer le clonage, spécifiez le répertoire vers lequel cloner, puis cliquez sur **Clone**. (Cloner).</span><span class="sxs-lookup"><span data-stu-id="122d8-183">In the **Clone Repository** dialog box, provide the URL to the Git repository to clone from, specify the directory to clone to, and then click **Clone**.</span></span>
   
    <span data-ttu-id="122d8-184">![Exemple de diffusion en continu Apache Spark - cloner Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-clone-from-git.png "Exemple de diffusion en continu Apache Spark - cloner Git")</span><span class="sxs-lookup"><span data-stu-id="122d8-184">![Apache Spark streaming example - clone from Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-clone-from-git.png "Apache Spark streaming example - clone from Git")</span></span>
3. <span data-ttu-id="122d8-185">Suivez les invites jusqu’à ce que le projet soit entièrement cloné.</span><span class="sxs-lookup"><span data-stu-id="122d8-185">Follow the prompts till the project is completely cloned.</span></span> <span data-ttu-id="122d8-186">Appuyez sur **Alt + 1** pour ouvrir la **Vue du projet**.</span><span class="sxs-lookup"><span data-stu-id="122d8-186">Press **Alt + 1** to open the **Project View**.</span></span> <span data-ttu-id="122d8-187">Elle doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="122d8-187">It should resemble the following.</span></span>
   
    <span data-ttu-id="122d8-188">![Exemple de diffusion en continu Apache Spark - Affichage de projet](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-project-view.png "Exemple de diffusion en continu Apache Spark - Affichage de projet")</span><span class="sxs-lookup"><span data-stu-id="122d8-188">![Apache Spark streaming example - Project View](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-project-view.png "Apache Spark streaming example - Project View")</span></span>
4. <span data-ttu-id="122d8-189">Assurez-vous que le code d’application est compilé avec Java8.</span><span class="sxs-lookup"><span data-stu-id="122d8-189">Make sure the application code is compiled with Java8.</span></span> <span data-ttu-id="122d8-190">Pour ce faire, cliquez sur **Fichier**, sur **Structure de projet**, puis sur l’onglet **Projet**, assurez-vous que le niveau de langue du projet est défini sur **8 - Lambdas, type annotations, etc.** (8- Expressions lambda, annotations de type, etc).</span><span class="sxs-lookup"><span data-stu-id="122d8-190">To ensure this, click **File**, click **Project Structure**, and on the **Project** tab, make sure Project language level is set to **8 - Lambdas, type annotations, etc.**.</span></span>
   
    <span data-ttu-id="122d8-191">![Exemple de diffusion en continu Apache Spark - Définir un compilateur](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-java-8-compiler.png "Exemple de diffusion en continu Apache Spark - Définir un compilateur")</span><span class="sxs-lookup"><span data-stu-id="122d8-191">![Apache Spark streaming example - Set compiler](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-java-8-compiler.png "Apache Spark streaming example - Set compiler")</span></span>
5. <span data-ttu-id="122d8-192">Ouvrez le fichier **pom.xml** et assurez-vous que la version de Spark est correcte.</span><span class="sxs-lookup"><span data-stu-id="122d8-192">Open the **pom.xml** and make sure the Spark version is correct.</span></span> <span data-ttu-id="122d8-193">Dans le nœud `<properties>`, recherchez l’extrait de code suivant et vérifiez la version de Spark.</span><span class="sxs-lookup"><span data-stu-id="122d8-193">Under `<properties>` node, look for the following snippet and verify the Spark version.</span></span>

        <scala.version>2.11.8</scala.version>
        <scala.compat.version>2.11.8</scala.compat.version>
        <scala.binary.version>2.11</scala.binary.version>
        <spark.version>2.0.0</spark.version>

6. <span data-ttu-id="122d8-194">L’application requiert un fichier jar de dépendance appelé **fichier jar du pilote JDBC**.</span><span class="sxs-lookup"><span data-stu-id="122d8-194">The application requires a dependency jar called **JDBC driver jar**.</span></span> <span data-ttu-id="122d8-195">Ce fichier est nécessaire pour écrire les messages reçus de l’Event Hub dans une base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="122d8-195">This is required to write the messages received from Event Hub into an Azure SQL database.</span></span> <span data-ttu-id="122d8-196">Vous pouvez télécharger ce fichier jar (version 4.1 ou version ultérieure) à partir d’[ici](https://msdn.microsoft.com/sqlserver/aa937724.aspx).</span><span class="sxs-lookup"><span data-stu-id="122d8-196">You can download this jar (v4.1 or later) from [here](https://msdn.microsoft.com/sqlserver/aa937724.aspx).</span></span> <span data-ttu-id="122d8-197">Ajoutez la référence à ce fichier jar dans la bibliothèque de projet.</span><span class="sxs-lookup"><span data-stu-id="122d8-197">Add reference to this jar in the project library.</span></span> <span data-ttu-id="122d8-198">Procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="122d8-198">Perform the following steps:</span></span>
     
     1. <span data-ttu-id="122d8-199">Dans la fenêtre IntelliJ IDEA où l’application est ouverte, cliquez sur **File** (Fichier), sur **Project Structure** (Structure de projet), puis sur **Libraries** (Bibliothèques).</span><span class="sxs-lookup"><span data-stu-id="122d8-199">From IntelliJ IDEA window where you have the application open, click **File**, click **Project Structure**, and then click **Libraries**.</span></span> 
     2. <span data-ttu-id="122d8-200">Cliquez sur l’icône Ajouter (![icône Ajouter](./media/hdinsight-apache-spark-eventhub-streaming/add-icon.png)), sur **Java**, puis accédez à l’emplacement où vous avez téléchargé le fichier jar du pilote JDBC.</span><span class="sxs-lookup"><span data-stu-id="122d8-200">Click the add icon (![add icon](./media/hdinsight-apache-spark-eventhub-streaming/add-icon.png)), click **Java**, and then navigate to the location where you downloaded the JDBC driver jar.</span></span> <span data-ttu-id="122d8-201">Suivez les invites pour ajouter le fichier jar à la bibliothèque de projet.</span><span class="sxs-lookup"><span data-stu-id="122d8-201">Follow the prompts to add the jar file to the project library.</span></span>

         <span data-ttu-id="122d8-202">![ajouter les dépendances manquantes](./media/hdinsight-apache-spark-eventhub-streaming/add-missing-dependency-jars.png "Ajouter les fichiers jars de dépendance manquants")</span><span class="sxs-lookup"><span data-stu-id="122d8-202">![add missing dependencies](./media/hdinsight-apache-spark-eventhub-streaming/add-missing-dependency-jars.png "Add missing dependency jars")</span></span>
     3. <span data-ttu-id="122d8-203">Cliquez sur **Apply**.</span><span class="sxs-lookup"><span data-stu-id="122d8-203">Click **Apply**.</span></span>

7. <span data-ttu-id="122d8-204">Créez le fichier jar de sortie.</span><span class="sxs-lookup"><span data-stu-id="122d8-204">Create the output jar file.</span></span> <span data-ttu-id="122d8-205">Procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="122d8-205">Perform the following steps.</span></span>

   1. <span data-ttu-id="122d8-206">Dans la boîte de dialogue **Project Structure** (Structure de projet) cliquez sur **Artifacts** (Artefacts), puis sur le signe plus.</span><span class="sxs-lookup"><span data-stu-id="122d8-206">In the **Project Structure** dialog box, click **Artifacts** and then click the plus symbol.</span></span> <span data-ttu-id="122d8-207">Dans la boîte de dialogue contextuelle, cliquez sur **JAR**, puis sur **À partir de modules ayant des dépendances**.</span><span class="sxs-lookup"><span data-stu-id="122d8-207">From the pop-up dialog box, click **JAR**, and then click **From modules with dependencies**.</span></span>      
       
       <span data-ttu-id="122d8-208">![Exemple de diffusion en continu Apache Spark - créer un fichier jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar.png "Exemple de diffusion en continu Apache Spark - créer un fichier jar")</span><span class="sxs-lookup"><span data-stu-id="122d8-208">![Apache Spark streaming example - create JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar.png "Apache Spark streaming example - create JAR")</span></span>
   2. <span data-ttu-id="122d8-209">Dans la boîte de dialogue **Créer un fichier JAR à partir de modules**, cliquez sur le bouton de sélection (![ellipse](./media/hdinsight-apache-spark-eventhub-streaming/ellipsis.png)) en regard de **Classe principale**.</span><span class="sxs-lookup"><span data-stu-id="122d8-209">In the **Create JAR from Modules** dialog box, click the ellipsis (![ellipsis](./media/hdinsight-apache-spark-eventhub-streaming/ellipsis.png)) against the **Main Class**.</span></span>
   3. <span data-ttu-id="122d8-210">Dans la boîte de dialogue **Select Main Class** (Sélectionner une classe principale), sélectionnez l’une des classes disponibles, puis cliquez sur **OK** (OK).</span><span class="sxs-lookup"><span data-stu-id="122d8-210">In the **Select Main Class** dialog box, select any of the available classes and then click **OK**.</span></span>
      
       <span data-ttu-id="122d8-211">![Exemple de diffusion en continu Apache Spark - sélectionner une classe pour un fichier jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-select-class-for-jar.png "Exemple de diffusion en continu Apache Spark - sélectionner une classe pour un fichier jar")</span><span class="sxs-lookup"><span data-stu-id="122d8-211">![Apache Spark streaming example - select class for jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-select-class-for-jar.png "Apache Spark streaming example - select class for jar")</span></span>
   4. <span data-ttu-id="122d8-212">Dans la boîte de dialogue **Create JAR from Modules** (Créer un fichier JAR à partir de modules), assurez-vous que l’option **Extract to the target JAR** (Extraire vers le fichier JAR cible) est activée, puis cliquez sur **OK** (OK).</span><span class="sxs-lookup"><span data-stu-id="122d8-212">In the **Create JAR from Modules** dialog box, make sure that the option to **extract to the target JAR** is selected, and then click **OK**.</span></span> <span data-ttu-id="122d8-213">Cela crée un fichier JAR contenant toutes les dépendances.</span><span class="sxs-lookup"><span data-stu-id="122d8-213">This creates a single JAR with all dependencies.</span></span>
      
       <span data-ttu-id="122d8-214">![Exemple de diffusion en continu Apache Spark - créer un fichier jar à partir de modules](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar-from-modules.png "Exemple de diffusion en continu Apache Spark - créer un fichier jar à partir de modules")</span><span class="sxs-lookup"><span data-stu-id="122d8-214">![Apache Spark streaming example - create jar from modules](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar-from-modules.png "Apache Spark streaming example - create jar from modules")</span></span>
   5. <span data-ttu-id="122d8-215">L’onglet **Output Layout** (Disposition de la sortie) répertorie tous les fichiers jar inclus dans le cadre du projet Maven.</span><span class="sxs-lookup"><span data-stu-id="122d8-215">The **Output Layout** tab lists all the jars that are included as part of the Maven project.</span></span> <span data-ttu-id="122d8-216">Vous pouvez sélectionner et supprimer ceux sur lesquels l’application Scala n’a aucune dépendance directe.</span><span class="sxs-lookup"><span data-stu-id="122d8-216">You can select and delete the ones on which the Scala application has no direct dependency.</span></span> <span data-ttu-id="122d8-217">Pour l’application que nous créons ici, vous pouvez les supprimer tous sauf le dernier (**spark-streaming-data-persistence-examples compile output**).</span><span class="sxs-lookup"><span data-stu-id="122d8-217">For the application we are creating here, you can remove all but the last one (**spark-streaming-data-persistence-examples compile output**).</span></span> <span data-ttu-id="122d8-218">Sélectionnez les fichiers JAR à supprimer, puis cliquez sur l’icône **Delete** (Supprimer) (![icône de suppression](./media/hdinsight-apache-spark-eventhub-streaming/delete-icon.png)).</span><span class="sxs-lookup"><span data-stu-id="122d8-218">Select the jars to delete and then click the **Delete** icon (![delete icon](./media/hdinsight-apache-spark-eventhub-streaming/delete-icon.png)).</span></span>
      
       <span data-ttu-id="122d8-219">![Exemple de diffusion en continu Apache Spark - supprimer un fichier jar extrait](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-delete-output-jars.png "Exemple de diffusion en continu Apache Spark - supprimer un fichier jar extrait")</span><span class="sxs-lookup"><span data-stu-id="122d8-219">![Apache Spark streaming example - delete extracted jars](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-delete-output-jars.png "Apache Spark streaming example - delete extracted jars")</span></span>
      
       <span data-ttu-id="122d8-220">Assurez-vous que la case à cocher **Générer à la création** est activée, ce qui garantit la création du fichier JAR à chaque génération ou mise à jour du projet.</span><span class="sxs-lookup"><span data-stu-id="122d8-220">Make sure **Build on make** box is selected, which ensures that the jar is created every time the project is built or updated.</span></span> <span data-ttu-id="122d8-221">Cliquez sur **Apply**.</span><span class="sxs-lookup"><span data-stu-id="122d8-221">Click **Apply**.</span></span>
   6. <span data-ttu-id="122d8-222">Sous l’onglet **Output Layout** (Disposition de la sortie), en bas à droite de la zone **Available Elements (Éléments disponibles)**, vous pouvez voir le fichier jar SQL JDBC jar que vous avez ajouté précédemment à la bibliothèque de projet.</span><span class="sxs-lookup"><span data-stu-id="122d8-222">In the **Output Layout** tab, right at the bottom of the **Available Elements** box, you have the SQL JDBC jar that you added earlier to the project library.</span></span> <span data-ttu-id="122d8-223">Vous devez l’ajouter à l’onglet **Output Layout** (Disposition de la sortie). Cliquez avec le bouton droit sur le fichier jar, puis cliquez sur **Extract Into Output Root**(Extraire dans la racine de sortie).</span><span class="sxs-lookup"><span data-stu-id="122d8-223">You must add this to the **Output Layout** tab. Right-click the jar file, and then click **Extract Into Output Root**.</span></span>
      
       <span data-ttu-id="122d8-224">![Exemple de diffusion en continu Apache Spark - extraire un fichier jar de dépendance](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-extract-dependency-jar.png "Exemple de diffusion en continu Apache Spark - extraire un fichier jar de dépendance")</span><span class="sxs-lookup"><span data-stu-id="122d8-224">![Apache Spark streaming example - extract dependency jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-extract-dependency-jar.png "Apache Spark streaming example - extract dependency jar")</span></span>  
      
       <span data-ttu-id="122d8-225">L’onglet **Output Layout** (Disposition de la sortie) doit maintenant ressembler à ceci.</span><span class="sxs-lookup"><span data-stu-id="122d8-225">The **Output Layout** tab should now look like this.</span></span>
      
       <span data-ttu-id="122d8-226">![Exemple de diffusion en continu Apache Spark - onglet de sortie finale](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-final-output-tab.png "Exemple de diffusion en continu Apache Spark - onglet de sortie finale")</span><span class="sxs-lookup"><span data-stu-id="122d8-226">![Apache Spark streaming example - final output tab](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-final-output-tab.png "Apache Spark streaming example - final output tab")</span></span>        
      
       <span data-ttu-id="122d8-227">Dans la boîte de dialogue **Project Structure** (Structure de projet), cliquez sur **Apply** (Appliquer), puis sur **OK** (OK).</span><span class="sxs-lookup"><span data-stu-id="122d8-227">In the **Project Structure** dialog box, click **Apply** and then click **OK**.</span></span>    
   7. <span data-ttu-id="122d8-228">Dans la barre de menus, cliquez sur **Build** (Générer), puis sur **Make Project** (Créer le projet).</span><span class="sxs-lookup"><span data-stu-id="122d8-228">From the menu bar, click **Build**, and then click **Make Project**.</span></span> <span data-ttu-id="122d8-229">Vous pouvez également cliquer sur **Générer les artefacts** pour créer le fichier JAR.</span><span class="sxs-lookup"><span data-stu-id="122d8-229">You can also click **Build Artifacts** to create the jar.</span></span> <span data-ttu-id="122d8-230">Le fichier jar de sortie est créé sous **\classes\artifacts**.</span><span class="sxs-lookup"><span data-stu-id="122d8-230">The output jar is created under **\classes\artifacts**.</span></span>
      
       <span data-ttu-id="122d8-231">![Exemple de diffusion en continu Apache Spark - fichier jar de sortie](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-output-jar.png "Exemple de diffusion en continu Apache Spark - fichier jar de sortie")</span><span class="sxs-lookup"><span data-stu-id="122d8-231">![Apache Spark streaming example - output JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-output-jar.png "Apache Spark streaming example - output JAR")</span></span>

## <a name="run-the-application-remotely-on-a-spark-cluster-using-livy"></a><span data-ttu-id="122d8-232">Exécuter l’application à distance sur un cluster Spark à l’aide de Livy</span><span class="sxs-lookup"><span data-stu-id="122d8-232">Run the application remotely on a Spark cluster using Livy</span></span>

<span data-ttu-id="122d8-233">Dans le cadre de cet article, vous allez utiliser Livy pour exécuter l’application de diffusion en continu Apache Spark à distance sur un cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="122d8-233">In this article you use Livy to run the Apache Spark streaming application remotely on a Spark cluster.</span></span> <span data-ttu-id="122d8-234">Pour une présentation détaillée de l’utilisation de Livy avec le cluster HDInsight Spark, voir [Soumettre des travaux à distance à un cluster Apache Spark sur Azure HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span><span class="sxs-lookup"><span data-stu-id="122d8-234">For detailed discussion on how to use Livy with HDInsight Spark cluster, see [Submit jobs remotely to an Apache Spark cluster on Azure HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span></span> <span data-ttu-id="122d8-235">Avant de commencer à exécuter l’application de diffusion en continu Spark, vous devez effectuer plusieurs opérations :</span><span class="sxs-lookup"><span data-stu-id="122d8-235">Before you can start running the Spark streaming application, there are a couple of things you should do:</span></span>

1. <span data-ttu-id="122d8-236">Démarrez l’application autonome locale pour générer des événements et les envoyer à l’Event Hub.</span><span class="sxs-lookup"><span data-stu-id="122d8-236">Start the local standalone application to generate events and sent to Event Hub.</span></span> <span data-ttu-id="122d8-237">Pour ce faire, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="122d8-237">Use the following command to do so:</span></span>

        java -cp com-microsoft-azure-eventhubs-client-example-0.2.0.jar com.microsoft.eventhubs.client.example.EventhubsClientDriver --eventhubs-namespace "mysbnamespace" --eventhubs-name "myeventhub" --policy-name "mysendpolicy" --policy-key "<policy key>" --message-length 32 --thread-count 32 --message-count -1

2. <span data-ttu-id="122d8-238">Copiez le fichier jar de diffusion en continu (**spark-streaming-data-persistence-examples.jar**) vers le stockage Blob Azure associé au cluster.</span><span class="sxs-lookup"><span data-stu-id="122d8-238">Copy the streaming jar (**spark-streaming-data-persistence-examples.jar**) to the Azure Blob storage associated with the cluster.</span></span> <span data-ttu-id="122d8-239">Le fichier jar est ainsi accessible à Livy.</span><span class="sxs-lookup"><span data-stu-id="122d8-239">This makes the jar accessible to Livy.</span></span> <span data-ttu-id="122d8-240">Pour ce faire, vous pouvez utiliser l’utilitaire de ligne de commande [**AzCopy**](../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="122d8-240">You can use [**AzCopy**](../storage/common/storage-use-azcopy.md), a command line utility, to do so.</span></span> <span data-ttu-id="122d8-241">De nombreux autres clients permettent également de télécharger des données.</span><span class="sxs-lookup"><span data-stu-id="122d8-241">There are a lot of other clients you can use to upload data.</span></span> <span data-ttu-id="122d8-242">Pour en savoir plus à leur sujet, consultez [Téléchargement de données pour les travaux Hadoop dans HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="122d8-242">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>
3. <span data-ttu-id="122d8-243">Installez CURL sur l’ordinateur à partir duquel vous exécutez ces applications.</span><span class="sxs-lookup"><span data-stu-id="122d8-243">Install CURL on the computer where you are running these applications from.</span></span> <span data-ttu-id="122d8-244">Nous utilisons CURL pour appeler les points de terminaison Livy afin d’exécuter les travaux à distance.</span><span class="sxs-lookup"><span data-stu-id="122d8-244">We use CURL to invoke the Livy endpoints to run the jobs remotely.</span></span>

### <a name="run-the-spark-streaming-application-to-receive-the-events-into-an-azure-storage-blob-as-text"></a><span data-ttu-id="122d8-245">Exécuter l’application de diffusion en continu Spark pour recevoir les événements dans un Azure Storage Blob en tant que texte</span><span class="sxs-lookup"><span data-stu-id="122d8-245">Run the Spark streaming application to receive the events into an Azure Storage Blob as text</span></span>

<span data-ttu-id="122d8-246">Ouvrez une invite de commandes, accédez au répertoire dans lequel vous avez installé CURL, puis exécutez la commande suivante (en remplaçant le nom/mot de passe d’utilisateur et le nom du cluster) :</span><span class="sxs-lookup"><span data-stu-id="122d8-246">Open a command prompt, navigate to the directory where you installed CURL, and run the following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputBlob.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="122d8-247">Les paramètres du fichier **inputBlob.txt** sont définis comme suit :</span><span class="sxs-lookup"><span data-stu-id="122d8-247">The parameters in the file **inputBlob.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsEventCount", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="122d8-248">Nous devons comprendre quels sont les paramètres dans le fichier d’entrée :</span><span class="sxs-lookup"><span data-stu-id="122d8-248">Let us understand what the parameters in the input file are:</span></span>

* <span data-ttu-id="122d8-249">**file** est le chemin d’accès au fichier jar d’application sur le compte Azure Storage associé au cluster.</span><span class="sxs-lookup"><span data-stu-id="122d8-249">**file** is the path to the application jar file on the Azure storage account associated with the cluster.</span></span>
* <span data-ttu-id="122d8-250">**className** est le nom de la classe dans le fichier jar.</span><span class="sxs-lookup"><span data-stu-id="122d8-250">**className** is the name of the class in the jar.</span></span>
* <span data-ttu-id="122d8-251">**args** est la liste des arguments requis par la classe.</span><span class="sxs-lookup"><span data-stu-id="122d8-251">**args** is the list of arguments required by the class</span></span>
* <span data-ttu-id="122d8-252">**numExecutors** est le nombre de cœurs que Spark utilise pour exécuter l’application de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="122d8-252">**numExecutors** is the number of cores used by Spark to run the streaming application.</span></span> <span data-ttu-id="122d8-253">Il doit toujours y avoir au moins deux fois le nombre de partitions de l’Event Hub.</span><span class="sxs-lookup"><span data-stu-id="122d8-253">This should always be at least twice the number of Event Hub partitions.</span></span>
* <span data-ttu-id="122d8-254">**executorMemory**, **executorCores** et **driverMemory** sont des paramètres utilisés pour affecter les ressources nécessaires à l’application de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="122d8-254">**executorMemory**, **executorCores**, **driverMemory** are parameters used to assign required resources to the streaming application.</span></span>

> [!NOTE]
> <span data-ttu-id="122d8-255">Il est inutile de créer les dossiers de sortie (EventCheckpoint, EventCount/EventCount10) utilisés comme paramètres.</span><span class="sxs-lookup"><span data-stu-id="122d8-255">You do not need to create the output folders (EventCheckpoint, EventCount/EventCount10) that are used as parameters.</span></span> <span data-ttu-id="122d8-256">L’application de diffusion en continu les crée pour vous.</span><span class="sxs-lookup"><span data-stu-id="122d8-256">The streaming application creates them for you.</span></span>
>
>

<span data-ttu-id="122d8-257">Lorsque vous exécutez la commande, vous devez voir une sortie similaire à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="122d8-257">When you run the command, you should see an output like the following:</span></span>

    < HTTP/1.1 201 Created
    < Content-Type: application/json; charset=UTF-8
    < Location: /18
    < Server: Microsoft-IIS/8.5
    < X-Powered-By: ARR/2.5
    < X-Powered-By: ASP.NET
    < Date: Tue, 01 Dec 2015 05:39:10 GMT
    < Content-Length: 37
    <
    {"id":1,"state":"starting","log":[]}* Connection #0 to host mysparkcluster.azurehdinsight.net left intact

<span data-ttu-id="122d8-258">Prenez note de l’ID de lot dans la dernière ligne de la sortie (dans cet exemple, « 1 »).</span><span class="sxs-lookup"><span data-stu-id="122d8-258">Make a note of the batch ID in the last line of the output (in this example it is '1').</span></span> <span data-ttu-id="122d8-259">Pour vérifier que l’application s’exécute correctement, vous pouvez consulter votre compte de stockage Azure associé au cluster, et devriez y voir le dossier **/nombre d’événements/EventCount10** créé.</span><span class="sxs-lookup"><span data-stu-id="122d8-259">To verify that the application runs successfully, you can look at your Azure storage account associated with the cluster and you should see the **/EventCount/EventCount10** folder created there.</span></span> <span data-ttu-id="122d8-260">Ce dossier doit contenir les objets blob qui capturent le nombre d’événements traités pendant la période spécifiée pour le paramètre **batch-interval-in-seconds**.</span><span class="sxs-lookup"><span data-stu-id="122d8-260">This folder should contain blobs that captures the number of events processed within the time period specified for the parameter **batch-interval-in-seconds**.</span></span>

<span data-ttu-id="122d8-261">L’application de diffusion en continu Spark continue à s’exécuter jusqu’à ce que vous l’arrêtiez.</span><span class="sxs-lookup"><span data-stu-id="122d8-261">The Spark streaming application will continue to run until you kill it.</span></span> <span data-ttu-id="122d8-262">Pour ce faire, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="122d8-262">To do so, use the following command:</span></span>

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/1"

### <a name="run-the-applications-to-receive-the-events-into-an-azure-storage-blob-as-json"></a><span data-ttu-id="122d8-263">Exécuter les applications pour recevoir les événements dans un objet blob Azure Storage en tant que fichier JSON</span><span class="sxs-lookup"><span data-stu-id="122d8-263">Run the applications to receive the events into an Azure Storage Blob as JSON</span></span>
<span data-ttu-id="122d8-264">Ouvrez une invite de commandes, accédez au répertoire dans lequel vous avez installé CURL, puis exécutez la commande suivante (en remplaçant le nom/mot de passe d’utilisateur et le nom du cluster) :</span><span class="sxs-lookup"><span data-stu-id="122d8-264">Open a command prompt, navigate to the directory where you installed CURL, and run the following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputJSON.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="122d8-265">Les paramètres du fichier **inputJSON.txt** sont définis comme suit :</span><span class="sxs-lookup"><span data-stu-id="122d8-265">The parameters in the file **inputJSON.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureBlobAsJSON", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-store-folder", "/EventStore10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="122d8-266">Les paramètres sont similaires à ce que vous avez spécifié pour la sortie de texte à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="122d8-266">The parameters are similar to what you specified for the text output, in the previous step.</span></span> <span data-ttu-id="122d8-267">Une fois encore, il est inutile de créer les dossiers de sortie (EventCheckpoint, EventCount/EventCount10) utilisés comme paramètres.</span><span class="sxs-lookup"><span data-stu-id="122d8-267">Again, you do not need to create the output folders (EventCheckpoint, EventCount/EventCount10) that are used as parameters.</span></span> <span data-ttu-id="122d8-268">L’application de diffusion en continu les crée pour vous.</span><span class="sxs-lookup"><span data-stu-id="122d8-268">The streaming application creates them for you.</span></span>

 <span data-ttu-id="122d8-269">Après avoir exécuté la commande, vous pouvez consulter votre compte de stockage Azure associé au cluster, et devriez y voir le dossier **/EventStore10** créé.</span><span class="sxs-lookup"><span data-stu-id="122d8-269">After you run the command, you can look at your Azure storage account associated with the cluster and you should see the **/EventStore10** folder created there.</span></span> <span data-ttu-id="122d8-270">Ouvrez n’importe quel fichier ayant le préfixe **part-**. Vous devriez y voir les événements traités au format JSON.</span><span class="sxs-lookup"><span data-stu-id="122d8-270">Open any file prefixed with **part-** and you should see the events processed in a JSON format.</span></span>

### <a name="run-the-applications-to-receive-the-events-into-a-hive-table"></a><span data-ttu-id="122d8-271">Exécuter les applications pour recevoir les événements dans une table Hive</span><span class="sxs-lookup"><span data-stu-id="122d8-271">Run the applications to receive the events into a Hive table</span></span>
<span data-ttu-id="122d8-272">Pour exécuter l’application de diffusion en continu Spark qui diffuse des événements dans une table Hive, vous avez besoin de composants supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="122d8-272">To run the Spark streaming application that streams events into a Hive table you need some additional components.</span></span> <span data-ttu-id="122d8-273">Ces composants sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="122d8-273">These are:</span></span>

* <span data-ttu-id="122d8-274">datanucleus-api-jdo-3.2.6.jar</span><span class="sxs-lookup"><span data-stu-id="122d8-274">datanucleus-api-jdo-3.2.6.jar</span></span>
* <span data-ttu-id="122d8-275">datanucleus-SGBDR-3.2.9.jar</span><span class="sxs-lookup"><span data-stu-id="122d8-275">datanucleus-rdbms-3.2.9.jar</span></span>
* <span data-ttu-id="122d8-276">datanucleus-core-3.2.10.jar</span><span class="sxs-lookup"><span data-stu-id="122d8-276">datanucleus-core-3.2.10.jar</span></span>
* <span data-ttu-id="122d8-277">hive-site.xml</span><span class="sxs-lookup"><span data-stu-id="122d8-277">hive-site.xml</span></span>

<span data-ttu-id="122d8-278">Les fichiers **.jar** sont disponibles sur votre cluster HDInsight Spark à l’adresse `/usr/hdp/current/spark-client/lib`.</span><span class="sxs-lookup"><span data-stu-id="122d8-278">The **.jar** files are available on your HDInsight Spark cluster at `/usr/hdp/current/spark-client/lib`.</span></span> <span data-ttu-id="122d8-279">Le fichier **hive-site.xml** est disponible à l’adresse `/usr/hdp/current/spark-client/conf`.</span><span class="sxs-lookup"><span data-stu-id="122d8-279">The **hive-site.xml** is available at `/usr/hdp/current/spark-client/conf`.</span></span>

<span data-ttu-id="122d8-280">Vous pouvez utiliser [WinScp](http://winscp.net/eng/download.php) pour copier ces fichiers à partir du cluster sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="122d8-280">You can use [WinScp](http://winscp.net/eng/download.php) to copy over these files from the cluster to your local computer.</span></span> <span data-ttu-id="122d8-281">Vous pouvez ensuite vous servir d’outils pour copier ces fichiers sur votre compte de stockage associé au cluster.</span><span class="sxs-lookup"><span data-stu-id="122d8-281">You can then use tools to copy these files over to your storage account associated with the cluster.</span></span> <span data-ttu-id="122d8-282">Pour plus d’informations sur la façon de charger des fichiers sur le compte de stockage, voir [Téléchargement de données pour des tâches Hadoop dans HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="122d8-282">For more information on how to upload files to the storage account, see [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

<span data-ttu-id="122d8-283">Après avoir copié les fichiers sur votre compte de stockage Azure, ouvrez une invite de commandes, accédez au répertoire dans lequel vous avez installé CURL, puis exécutez la commande suivante (en remplaçant le nom/mot de passe d’utilisateur et le nom du cluster) :</span><span class="sxs-lookup"><span data-stu-id="122d8-283">Once you have copied over the files to your Azure storage account, open a command prompt, navigate to the directory where you installed CURL, and run the following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputHive.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="122d8-284">Les paramètres du fichier **inputHive.txt** sont définis comme suit :</span><span class="sxs-lookup"><span data-stu-id="122d8-284">The parameters in the file **inputHive.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToHiveTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-hive-table", "EventHiveTable10" ], "jars":["wasb:///example/jars/datanucleus-api-jdo-3.2.6.jar", "wasb:///example/jars/datanucleus-rdbms-3.2.9.jar", "wasb:///example/jars/datanucleus-core-3.2.10.jar"], "files":["wasb:///example/jars/hive-site.xml"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="122d8-285">Les paramètres sont similaires à ce que vous avez spécifié pour la sortie de texte aux étapes précédentes.</span><span class="sxs-lookup"><span data-stu-id="122d8-285">The parameters are similar to what you specified for the text output, in the previous steps.</span></span> <span data-ttu-id="122d8-286">Une fois encore, il est inutile de créer les dossiers de sortie(EventCheckpoint, EventCount/EventCount10) ou la table Hive de sortie (EventHiveTable10) utilisés comme paramètres.</span><span class="sxs-lookup"><span data-stu-id="122d8-286">Again, you do not need to create the output folders (EventCheckpoint, EventCount/EventCount10) or the output Hive table (EventHiveTable10) that are used as parameters.</span></span> <span data-ttu-id="122d8-287">L’application de diffusion en continu les crée pour vous.</span><span class="sxs-lookup"><span data-stu-id="122d8-287">The streaming application creates them for you.</span></span> <span data-ttu-id="122d8-288">Notez que l’option **jars** et **files** inclut des chemins d’accès aux fichiers .jar et au fichier hive-site.xml que vous avez copiés vers le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="122d8-288">Note that the **jars** and **files** option includes paths to the .jar files and the hive-site.xml that you copied over to the storage account.</span></span>

<span data-ttu-id="122d8-289">Pour vérifier que la table Hive a été correctement créée, vous pouvez exécuter SSH dans le cluster et exécuter des requêtes Hive.</span><span class="sxs-lookup"><span data-stu-id="122d8-289">To verify that the hive table was successfully created, you can SSH into the cluster and run Hive queries.</span></span> <span data-ttu-id="122d8-290">Pour obtenir des instructions, consultez [Utilisation de Hive avec Hadoop dans HDInsight avec SSH](hdinsight-hadoop-use-hive-ssh.md).</span><span class="sxs-lookup"><span data-stu-id="122d8-290">For instructions, see [Use Hive with Hadoop in HDInsight with SSH](hdinsight-hadoop-use-hive-ssh.md).</span></span> <span data-ttu-id="122d8-291">Après vous être connecté à l’aide de SSH, vous pouvez exécuter la commande suivante pour vérifier que la table Hive, **EventHiveTable10**, est créée.</span><span class="sxs-lookup"><span data-stu-id="122d8-291">Once you are connected using SSH, you can run the following command to verify that the Hive table, **EventHiveTable10**, is created.</span></span>

    show tables;

<span data-ttu-id="122d8-292">Le résultat doit ressembler à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="122d8-292">You should see an output similar to the following:</span></span>

    OK
    eventhivetable10
    hivesampletable

<span data-ttu-id="122d8-293">Vous pouvez également exécuter une requête SELECT pour afficher le contenu de la table.</span><span class="sxs-lookup"><span data-stu-id="122d8-293">You can also run a SELECT query to view the contents of the table.</span></span>

    SELECT * FROM eventhivetable10 LIMIT 10;

<span data-ttu-id="122d8-294">Un résultat similaire à ce qui suit s’affiche normalement :</span><span class="sxs-lookup"><span data-stu-id="122d8-294">You should see an output like the following:</span></span>

    ZN90apUSQODDTx7n6Toh6jDbuPngqT4c
    sor2M7xsFwmaRW8W8NDwMneFNMrOVkW1
    o2HcsU735ejSi2bGEcbUSB4btCFmI1lW
    TLuibq4rbj0T9st9eEzIWJwNGtMWYoYS
    HKCpPlWFWAJILwR69MAq863nCWYzDEw6
    Mvx0GQOPYvPR7ezBEpIHYKTKiEhYammQ
    85dRppSBSbZgThLr1s0GMgKqynDUqudr
    5LAWkNqorLj3ZN9a2mfWr9rZqeXKN4pF
    ulf9wSFNjD7BZXCyunozecov9QpEIYmJ
    vWzM3nvOja8DhYcwn0n5eTfOItZ966pa
    Time taken: 4.434 seconds, Fetched: 10 row(s)


### <a name="run-the-applications-to-receive-the-events-into-an-azure-sql-database-table"></a><span data-ttu-id="122d8-295">Exécuter les applications pour recevoir les événements dans une table de Base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="122d8-295">Run the applications to receive the events into an Azure SQL database table</span></span>
<span data-ttu-id="122d8-296">Avant d’exécuter cette étape, assurez-vous que vous disposez d’une base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="122d8-296">Before running this step, make sure you have an Azure SQL database created.</span></span> <span data-ttu-id="122d8-297">Pour obtenir des instructions, consultez [Créer une base de données SQL en quelques minutes](../sql-database/sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="122d8-297">For instructions, see [Create a SQL database in minutes](../sql-database/sql-database-get-started.md).</span></span> <span data-ttu-id="122d8-298">Pour terminer cette section, vous avez besoin des valeurs de nom de base de données, de nom de serveur de base de données, ainsi que des informations d’identification de l’administrateur de base de données en tant que paramètres.</span><span class="sxs-lookup"><span data-stu-id="122d8-298">To complete this section, you need values for database name, database server name, and the database administrator credentials as parameters.</span></span> <span data-ttu-id="122d8-299">Il est cependant inutile de créer la table de base de données.</span><span class="sxs-lookup"><span data-stu-id="122d8-299">You do not need to create the database table though.</span></span> <span data-ttu-id="122d8-300">L’application de diffusion en continu Spark la crée pour vous.</span><span class="sxs-lookup"><span data-stu-id="122d8-300">The Spark streaming application creates that for you.</span></span>

<span data-ttu-id="122d8-301">Ouvrez une invite de commandes, accédez au répertoire dans lequel vous avez installé CURL, puis exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="122d8-301">Open a command prompt, navigate to the directory where you installed CURL, and run the following command:</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputSQL.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="122d8-302">Les paramètres du fichier **inputSQL.txt** sont définis comme suit :</span><span class="sxs-lookup"><span data-stu-id="122d8-302">The parameters in the file **inputSQL.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureSQLTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--sql-server-fqdn", "<database-server-name>.database.windows.net", "--sql-database-name", "mysparkdatabase", "--database-username", "sparkdbadmin", "--database-password", "<put-password-here>", "--event-sql-table", "EventContent" ], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="122d8-303">Pour vérifier que l’application s’exécute correctement, vous pouvez vous connecter à la base de données SQL Azure à l’aide de SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="122d8-303">To verify that the application runs successfully, you can connect to the Azure SQL database using SQL Server Management Studio.</span></span> <span data-ttu-id="122d8-304">Pour obtenir des instructions sur la procédure à suivre, voir [Se connecter à Base de données SQL avec SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="122d8-304">For instructions on how to do that, see [Connect to SQL Database with SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md).</span></span> <span data-ttu-id="122d8-305">Une fois connecté à la base de données, vous pouvez accéder à la table **EventContent** créée par l’application de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="122d8-305">Once you are connected to the database, you can navigate to the **EventContent** table that was created by the streaming application.</span></span> <span data-ttu-id="122d8-306">Vous pouvez exécuter une requête rapide pour obtenir les données de la table.</span><span class="sxs-lookup"><span data-stu-id="122d8-306">You can run a quick query to get the data from the table.</span></span> <span data-ttu-id="122d8-307">Exécutez la requête suivante :</span><span class="sxs-lookup"><span data-stu-id="122d8-307">Run the following query:</span></span>

    SELECT * FROM EventCount

<span data-ttu-id="122d8-308">Le résultat ressemble à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="122d8-308">You should see output similar to the following:</span></span>

    00046b0f-2552-4980-9c3f-8bba5647c8ee
    000b7530-12f9-4081-8e19-90acd26f9c0c
    000bc521-9c1b-4a42-ab08-dc1893b83f3b
    00123a2a-e00d-496a-9104-108920955718
    0017c68f-7a4e-452d-97ad-5cb1fe5ba81b
    001KsmqL2gfu5ZcuQuTqTxQvVyGCqPp9
    001vIZgOStka4DXtud0e3tX7XbfMnZrN
    00220586-3e1a-4d2d-a89b-05c5892e541a
    0029e309-9e54-4e1b-84be-cd04e6fce5ec
    003333cf-874f-4045-9da3-9f98c2b4ea49
    0043c07e-8d73-420a-9af7-1fcb94575356
    004a11a9-0c2c-4bc0-a7d5-2e0ebd947ab9


## <span data-ttu-id="122d8-309"><a name="seealso"></a>Voir aussi</span><span class="sxs-lookup"><span data-stu-id="122d8-309"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="122d8-310">Vue d’ensemble : Apache Spark sur Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="122d8-310">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)
* [<span data-ttu-id="122d8-311">Conception de la connexion basée sur récepteur et Direct DStream</span><span class="sxs-lookup"><span data-stu-id="122d8-311">Design of Receiver-based Connection and Direct DStream</span></span>](https://www.slideshare.net/NanZhu/seattle-sparkmeetup032317)

### <a name="scenarios"></a><span data-ttu-id="122d8-312">Scénarios</span><span class="sxs-lookup"><span data-stu-id="122d8-312">Scenarios</span></span>
* [<span data-ttu-id="122d8-313">Spark avec BI : effectuez une analyse interactive des données à l’aide de Spark dans HDInsight avec des outils BI</span><span class="sxs-lookup"><span data-stu-id="122d8-313">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="122d8-314">Spark avec Machine Learning : Utiliser Spark dans HDInsight pour l’analyse de la température de bâtiments à l’aide de données HVAC</span><span class="sxs-lookup"><span data-stu-id="122d8-314">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="122d8-315">Spark avec Machine Learning : Utiliser Spark dans HDInsight pour prédire les résultats de l’inspection des aliments</span><span class="sxs-lookup"><span data-stu-id="122d8-315">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="122d8-316">Analyse des journaux de site web à l’aide de Spark dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="122d8-316">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="122d8-317">Créer et exécuter des applications</span><span class="sxs-lookup"><span data-stu-id="122d8-317">Create and run applications</span></span>
* [<span data-ttu-id="122d8-318">Créer une application autonome avec Scala</span><span class="sxs-lookup"><span data-stu-id="122d8-318">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="122d8-319">Exécuter des tâches à distance avec Livy sur un cluster Spark</span><span class="sxs-lookup"><span data-stu-id="122d8-319">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="122d8-320">Outils et extensions</span><span class="sxs-lookup"><span data-stu-id="122d8-320">Tools and extensions</span></span>
* [<span data-ttu-id="122d8-321">Utilisez le plugin d’outils HDInsight pour IntelliJ IDEA pour créer et soumettre des applications Spark Scala</span><span class="sxs-lookup"><span data-stu-id="122d8-321">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="122d8-322">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely) (Utiliser le plug-in Outils HDInsight pour IntelliJ IDEA pour déboguer des applications Spark à distance)</span><span class="sxs-lookup"><span data-stu-id="122d8-322">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="122d8-323">Utiliser des bloc-notes Zeppelin avec un cluster Spark sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="122d8-323">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="122d8-324">Noyaux disponibles pour le bloc-notes Jupyter dans un cluster Spark pour HDInsight</span><span class="sxs-lookup"><span data-stu-id="122d8-324">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="122d8-325">Utiliser des packages externes avec les blocs-notes Jupyter</span><span class="sxs-lookup"><span data-stu-id="122d8-325">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="122d8-326">Install Jupyter on your computer and connect to an HDInsight Spark cluster (Installer Jupyter sur un ordinateur et se connecter au cluster Spark sur HDInsight)</span><span class="sxs-lookup"><span data-stu-id="122d8-326">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="122d8-327">Gestion des ressources</span><span class="sxs-lookup"><span data-stu-id="122d8-327">Manage resources</span></span>
* [<span data-ttu-id="122d8-328">Gérer les ressources du cluster Apache Spark dans Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="122d8-328">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="122d8-329">Suivi et débogage des tâches en cours d’exécution sur un cluster Apache Spark dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="122d8-329">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]: ../storage-create-storage-account/
