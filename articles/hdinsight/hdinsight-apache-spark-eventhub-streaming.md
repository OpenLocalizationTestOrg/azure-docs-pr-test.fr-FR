---
title: "diffusion en continu d’aaaUse Apache Spark avec des concentrateurs d’événements dans Azure HDInsight | Documents Microsoft"
description: "Générer un exemple de diffusion en continu d’Apache Spark sur toosend données tooAzure concentrateur d’événements de flux et recevoir les événements dans le cluster HDInsight Spark à l’aide d’une application scala."
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
ms.openlocfilehash: 10cc5884047b3b8249fe8a8822a16a19780a4af3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="apache-spark-streaming-process-data-from-azure-event-hubs-with-spark-cluster-on-hdinsight"></a><span data-ttu-id="3bf09-104">Diffusion en continu Apache Spark : traitement de données d’Azure Event Hubs avec un cluster Spark sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="3bf09-104">Apache Spark streaming: Process data from Azure Event Hubs with Spark cluster on HDInsight</span></span>

<span data-ttu-id="3bf09-105">Dans cet article, vous créez un Apache Spark de diffusion en continu d’exemple qui implique hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="3bf09-105">In this article, you create an Apache Spark streaming sample that involves hello following steps:</span></span>

1. <span data-ttu-id="3bf09-106">Vous utilisez un message tooingest d’application autonome dans un concentrateur d’événements Azure.</span><span class="sxs-lookup"><span data-stu-id="3bf09-106">You use a standalone application tooingest messages into an Azure Event Hub.</span></span>

2. <span data-ttu-id="3bf09-107">Avec deux approches différentes, vous extrayez des messages hello de concentrateur d’événements en temps réel à l’aide d’une application en cours d’exécution dans le cluster Spark sur Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3bf09-107">With two different approaches, you retrieve hello messages from Event Hub in real-time using an application running in Spark cluster on Azure HDInsight.</span></span>

3. <span data-ttu-id="3bf09-108">Génération de diffusion en continu des pipelines analytiques toopersist toodifferent systèmes de stockage ou obtenir des informations à partir des données volée hello.</span><span class="sxs-lookup"><span data-stu-id="3bf09-108">You build streaming analytic pipelines toopersist data toodifferent storage systems, or get insights from data on hello fly.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3bf09-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="3bf09-109">Prerequisites</span></span>

* <span data-ttu-id="3bf09-110">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="3bf09-110">An Azure subscription.</span></span> <span data-ttu-id="3bf09-111">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="3bf09-111">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="3bf09-112">Un cluster Apache Spark sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3bf09-112">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="3bf09-113">Pour obtenir des instructions, consultez [Création de clusters Apache Spark dans Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="3bf09-113">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="spark-streaming-concepts"></a><span data-ttu-id="3bf09-114">Concepts de la diffusion en continu de Spark</span><span class="sxs-lookup"><span data-stu-id="3bf09-114">Spark Streaming concepts</span></span>

<span data-ttu-id="3bf09-115">Pour obtenir une explication détaillée de la diffusion en continu Spark, voir la [présentation de la diffusion en continu Apache Spark](http://spark.apache.org/docs/latest/streaming-programming-guide.html#overview).</span><span class="sxs-lookup"><span data-stu-id="3bf09-115">For a detailed explanation of Spark streaming, see [Apache Spark streaming overview](http://spark.apache.org/docs/latest/streaming-programming-guide.html#overview).</span></span> <span data-ttu-id="3bf09-116">HDInsight met hello de cluster même tooa fonctionnalités diffusion en continu Spark sur Azure.</span><span class="sxs-lookup"><span data-stu-id="3bf09-116">HDInsight brings hello same streaming features tooa Spark cluster on Azure.</span></span>  

## <a name="what-does-this-solution-do"></a><span data-ttu-id="3bf09-117">Que fait cette solution ?</span><span class="sxs-lookup"><span data-stu-id="3bf09-117">What does this solution do?</span></span>

<span data-ttu-id="3bf09-118">Dans cet article, toocreate un exemple de diffusion en continu Spark, effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="3bf09-118">In this article, toocreate a Spark streaming example, perform hello following steps:</span></span>

1. <span data-ttu-id="3bf09-119">Créez un Event Hub Azure qui doit recevoir un flux d’événements.</span><span class="sxs-lookup"><span data-stu-id="3bf09-119">Create an Azure Event Hub that will receive a stream of events.</span></span>

2. <span data-ttu-id="3bf09-120">Exécuter une application autonome local qui génère des événements et le place toohello concentrateur d’événements Azure.</span><span class="sxs-lookup"><span data-stu-id="3bf09-120">Run a local standalone application that generates events and pushes it toohello Azure Event Hub.</span></span> <span data-ttu-id="3bf09-121">exemple d’application Hello qui effectue l’opération est publiée à [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span><span class="sxs-lookup"><span data-stu-id="3bf09-121">hello sample application that does this is published at [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span></span>

3. <span data-ttu-id="3bf09-122">Exécutez une application de diffusion en continu à distance sur un cluster Spark qui lit les événements de diffusion en continu à partir d’Azure Event Hub et effectuez diverses tâches de traitement/d’analyse des données.</span><span class="sxs-lookup"><span data-stu-id="3bf09-122">Run a streaming application remotely on a Spark cluster that reads streaming events from Azure Event Hub and perform various data processing/analysis.</span></span>

## <a name="create-an-azure-event-hub"></a><span data-ttu-id="3bf09-123">Création d'un hub d'événements Azure</span><span class="sxs-lookup"><span data-stu-id="3bf09-123">Create an Azure Event Hub</span></span>

1. <span data-ttu-id="3bf09-124">Session toohello [Azure Portal](https://ms.portal.azure.com), puis cliquez sur **nouveau** à hello haut à gauche de l’écran hello.</span><span class="sxs-lookup"><span data-stu-id="3bf09-124">Log on toohello [Azure Portal](https://ms.portal.azure.com), and click **New** at hello top left of hello screen.</span></span>

2. <span data-ttu-id="3bf09-125">Cliquez sur **Internet des Objets**, puis sur **Hubs d’événements**.</span><span class="sxs-lookup"><span data-stu-id="3bf09-125">Click **Internet of Things**, then click **Event Hubs**.</span></span>

    <span data-ttu-id="3bf09-126">![Créer un Event Hub pour un exemple de diffusion en continu Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-create-event-hub-for-spark-streaming.png "Créer un Event Hub pour un exemple de diffusion en continu Spark")</span><span class="sxs-lookup"><span data-stu-id="3bf09-126">![Create event hub for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-create-event-hub-for-spark-streaming.png "Create event hub for Spark streaming example")</span></span>

3. <span data-ttu-id="3bf09-127">Bonjour **créer l’espace de noms** panneau, entrez un nom d’espace de noms.</span><span class="sxs-lookup"><span data-stu-id="3bf09-127">In hello **Create namespace** blade, enter a namespace name.</span></span> <span data-ttu-id="3bf09-128">Choisissez hello tarification (base ou Standard).</span><span class="sxs-lookup"><span data-stu-id="3bf09-128">choose hello pricing tier (Basic or Standard).</span></span> <span data-ttu-id="3bf09-129">En outre, choisissez un abonnement Azure, le groupe de ressources et l’emplacement de ressources toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="3bf09-129">Also, choose an Azure subscription, resource group, and location in which toocreate hello resource.</span></span> <span data-ttu-id="3bf09-130">Cliquez sur **créer** toocreate hello espace de noms.</span><span class="sxs-lookup"><span data-stu-id="3bf09-130">Click **Create** toocreate hello namespace.</span></span>

      <span data-ttu-id="3bf09-131">![Fournir un nom d’Event Hub pour un exemple de diffusion en continu Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-name-for-spark-streaming.png "Fournir un nom d’Event Hub pour un exemple de diffusion en continu Spark")</span><span class="sxs-lookup"><span data-stu-id="3bf09-131">![Provide an event hub name for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-name-for-spark-streaming.png "Provide an event hub name for Spark streaming example")</span></span>

    > [!NOTE]
    > <span data-ttu-id="3bf09-132">Vous devez sélectionnez hello même **emplacement** que votre cluster Apache Spark dans HDInsight tooreduce latence et les coûts.</span><span class="sxs-lookup"><span data-stu-id="3bf09-132">You should select hello same **Location** as your Apache Spark cluster in HDInsight tooreduce latency and costs.</span></span>
    >
    >

4. <span data-ttu-id="3bf09-133">Dans hello concentrateurs d’événements espace de noms, cliquez sur espace de noms nouvellement créé hello.</span><span class="sxs-lookup"><span data-stu-id="3bf09-133">In hello Event Hubs namespace list, click hello newly-created namespace.</span></span>      


5. <span data-ttu-id="3bf09-134">Dans le panneau espace de noms de hello, cliquez sur **concentrateurs d’événements**, puis cliquez sur **+ concentrateur d’événements** toocreate un concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="3bf09-134">In hello namespace blade, click **Event Hubs**, and then click **+ Event Hub** toocreate a new Event Hub.</span></span>
   
    <span data-ttu-id="3bf09-135">![Créer un Event Hub pour un exemple de diffusion en continu Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-open-event-hubs-blade-for-spark-streaming-example.png "Créer un Event Hub pour un exemple de diffusion en continu Spark")</span><span class="sxs-lookup"><span data-stu-id="3bf09-135">![Create event hub for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-open-event-hubs-blade-for-spark-streaming-example.png "Create event hub for Spark streaming example")</span></span>

6. <span data-ttu-id="3bf09-136">Tapez un nom pour votre concentrateur d’événements, jeu hello partition count too10 et too1 de rétention de message.</span><span class="sxs-lookup"><span data-stu-id="3bf09-136">Type a name for your Event Hub, set hello partition count too10, and message retention too1.</span></span> <span data-ttu-id="3bf09-137">Nous ne sommes pas archivage des messages hello dans cette solution afin de vous pouvez laisser le reste hello comme valeur par défaut, puis cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="3bf09-137">We are not archiving hello messages in this solution so you can leave hello rest as default, and then click **Create**.</span></span>
   
    <span data-ttu-id="3bf09-138">![Fournir des détails d’Event Hub pour un exemple de diffusion en continu Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-details-for-spark-streaming-example.png "Fournir des détails d’Event Hub pour un exemple de diffusion en continu Spark")</span><span class="sxs-lookup"><span data-stu-id="3bf09-138">![Provide event hub details for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-details-for-spark-streaming-example.png "Provide event hub details for Spark streaming example")</span></span>

7. <span data-ttu-id="3bf09-139">Hello nouvellement créé Hub d’événements est répertorié dans le panneau de concentrateur d’événements hello.</span><span class="sxs-lookup"><span data-stu-id="3bf09-139">hello newly created Event Hub is listed in hello Event Hub blade.</span></span>
    
     <span data-ttu-id="3bf09-140">![Afficher le concentrateur d’événements pour l’exemple de diffusion en continu de Spark hello](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-for-spark-streaming-example.png "mode concentrateur d’événements pour hello au service de diffusion en continu d’exemple")</span><span class="sxs-lookup"><span data-stu-id="3bf09-140">![View Event Hub for hello Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-for-spark-streaming-example.png "View Event Hub for hello Spark streaming example")</span></span>

8. <span data-ttu-id="3bf09-141">Dans le panneau d’espace de noms hello (pas hello spécifique concentrateur d’événements blade), cliquez sur **les stratégies d’accès partagé**, puis cliquez sur **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="3bf09-141">Back in hello namespace blade (not hello specific Event Hub blade), click **Shared access policies**, and then click **RootManageSharedAccessKey**.</span></span>
    
     <span data-ttu-id="3bf09-142">![Définir des stratégies de concentrateur d’événements pour l’exemple de diffusion en continu de Spark hello](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-set-event-hub-policies-for-spark-streaming-example.png "des stratégies de concentrateur d’événements défini pour hello au service de diffusion en continu d’exemple")</span><span class="sxs-lookup"><span data-stu-id="3bf09-142">![Set Event Hub policies for hello Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-set-event-hub-policies-for-spark-streaming-example.png "Set Event Hub policies for hello Spark streaming example")</span></span>

9. <span data-ttu-id="3bf09-143">Cliquez sur Bonjour copie bouton toocopy Bonjour **RootManageSharedAccessKey** principal Presse-papiers toohello chaîne clé et de la connexion.</span><span class="sxs-lookup"><span data-stu-id="3bf09-143">Click hello copy button toocopy hello **RootManageSharedAccessKey** primary key and connection string toohello clipboard.</span></span> <span data-ttu-id="3bf09-144">Enregistrez ces toouse plus loin dans le didacticiel de hello.</span><span class="sxs-lookup"><span data-stu-id="3bf09-144">Save these toouse later in hello tutorial.</span></span>
    
     <span data-ttu-id="3bf09-145">![Afficher les clés de stratégie de concentrateur d’événements pour l’exemple de diffusion en continu de Spark hello](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-policy-keys.png "clés de stratégie de mode concentrateur d’événements pour hello au service de diffusion en continu d’exemple")</span><span class="sxs-lookup"><span data-stu-id="3bf09-145">![View Event Hub policy keys for hello Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-policy-keys.png "View Event Hub policy keys for hello Spark streaming example")</span></span>

## <a name="send-messages-tooazure-event-hub-using-a-sample-scala-application"></a><span data-ttu-id="3bf09-146">Envoyer des messages tooAzure concentrateur d’événements à l’aide d’un exemple d’application Scala</span><span class="sxs-lookup"><span data-stu-id="3bf09-146">Send messages tooAzure Event Hub using a sample Scala application</span></span>

<span data-ttu-id="3bf09-147">Dans cette section vous utilisez une application Scala autonome locale qui génère un flux d’événements et l’envoie tooAzure concentrateur d’événements que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="3bf09-147">In this section you use a standalone local Scala application that generates a stream of events and sends it tooAzure Event Hub that you created earlier.</span></span> <span data-ttu-id="3bf09-148">Cette application est disponible sur GitHub à l’adresse [https://github.com/hdinsight/eventhubs-sample-event-producer](https://github.com/hdinsight/eventhubs-sample-event-producer).</span><span class="sxs-lookup"><span data-stu-id="3bf09-148">This application is available on GitHub at [https://github.com/hdinsight/eventhubs-sample-event-producer](https://github.com/hdinsight/eventhubs-sample-event-producer).</span></span> <span data-ttu-id="3bf09-149">Hello étapes supposent que vous avez déjà dupliquée ce référentiel GitHub.</span><span class="sxs-lookup"><span data-stu-id="3bf09-149">hello steps here assume that you have already forked this GitHub repository.</span></span>

1. <span data-ttu-id="3bf09-150">Assurez-vous que vous avez suivant hello installé sur l’ordinateur hello sur lequel vous exécutez cette application.</span><span class="sxs-lookup"><span data-stu-id="3bf09-150">Make sure you have hello following installed on hello computer where you run this application.</span></span>

    * <span data-ttu-id="3bf09-151">Kit de développement logiciel (SDK) Oracle Java.</span><span class="sxs-lookup"><span data-stu-id="3bf09-151">Oracle Java Development kit.</span></span> <span data-ttu-id="3bf09-152">Vous pouvez l’installer à partir d’ [ici](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="3bf09-152">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
    * <span data-ttu-id="3bf09-153">Apache Maven.</span><span class="sxs-lookup"><span data-stu-id="3bf09-153">Apache Maven.</span></span> <span data-ttu-id="3bf09-154">Vous pouvez le télécharger [ici](https://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="3bf09-154">You can download it from [here](https://maven.apache.org/download.cgi).</span></span> <span data-ttu-id="3bf09-155">Instructions tooinstall Maven sont disponibles [ici](https://maven.apache.org/install.html).</span><span class="sxs-lookup"><span data-stu-id="3bf09-155">Instructions tooinstall Maven are available [here](https://maven.apache.org/install.html).</span></span>

2. <span data-ttu-id="3bf09-156">Ouvrez une invite de commandes et accédez emplacement toohello vous avez cloné du référentiel GitHub hello pour exemple d’application de Scala hello et exécutez hello après application de commande toobuild hello.</span><span class="sxs-lookup"><span data-stu-id="3bf09-156">Open a command prompt and navigate toohello location you cloned hello GitHub repo for hello sample Scala application and run hello following command toobuild hello application.</span></span>

        mvn package

3. <span data-ttu-id="3bf09-157">jar de sortie Hello pour l’application hello, **com-microsoft-azure-eventhubs-client-example-0.2.0.jar**, est créé sous **/target** active.</span><span class="sxs-lookup"><span data-stu-id="3bf09-157">hello output jar for hello application, **com-microsoft-azure-eventhubs-client-example-0.2.0.jar**, is created under **/target** directory.</span></span> <span data-ttu-id="3bf09-158">Vous utilisez ce fichier JAR plus loin dans cette solution complète de l’article tootest hello.</span><span class="sxs-lookup"><span data-stu-id="3bf09-158">You use this JAR later in this article tootest hello complete solution.</span></span>

## <a name="create-application-tooreceive-messages-from-event-hub-into-a-spark-cluster"></a><span data-ttu-id="3bf09-159">Créer des messages tooreceive d’application à partir du concentrateur d’événements dans un cluster Spark</span><span class="sxs-lookup"><span data-stu-id="3bf09-159">Create application tooreceive messages from Event Hub into a Spark cluster</span></span> 

<span data-ttu-id="3bf09-160">Nous avons deux approches tooconnect Spark de diffusion en continu Azure Event Hubs, connexion basée sur le récepteur et Direct DStream pas en charge les connexions.</span><span class="sxs-lookup"><span data-stu-id="3bf09-160">We have two approaches tooconnect Spark Streaming and Azure Event Hubs, Receiver-based connection and Direct-DStream-based connection.</span></span> <span data-ttu-id="3bf09-161">En fonction des DStream direct est introduit sur janvier 2017, dans la version de hello 2.0.3.</span><span class="sxs-lookup"><span data-stu-id="3bf09-161">Direct-DStream-based is introduced on Jan of 2017, in hello 2.0.3 release.</span></span> <span data-ttu-id="3bf09-162">Il est supposé tooreplace hello d’origine récepteur connexion car il n’est plus performante et efficace de ressources.</span><span class="sxs-lookup"><span data-stu-id="3bf09-162">It is supposed tooreplace hello original receiver-based connection as it is more performant and resource-efficient.</span></span> <span data-ttu-id="3bf09-163">Vous trouverez plus de détails à l’adresse [https://github.com/hdinsight/spark-eventhubs](https://github.com/hdinsight/spark-eventhubs).</span><span class="sxs-lookup"><span data-stu-id="3bf09-163">More details found in [https://github.com/hdinsight/spark-eventhubs](https://github.com/hdinsight/spark-eventhubs).</span></span> <span data-ttu-id="3bf09-164">Direct DStream prend uniquement en charge Spark 2.0+.</span><span class="sxs-lookup"><span data-stu-id="3bf09-164">Direct DStream only supports Spark 2.0+.</span></span>

### <a name="build-applications-with-hello-dependency-toospark-eventhubs-connector"></a><span data-ttu-id="3bf09-165">Créer des applications avec le connecteur de hello dépendance toospark-eventhubs</span><span class="sxs-lookup"><span data-stu-id="3bf09-165">Build applications with hello dependency toospark-eventhubs connector</span></span>

<span data-ttu-id="3bf09-166">Nous publierons également hello mise en lots de la version de Spark-EventHubs dans GitHub.</span><span class="sxs-lookup"><span data-stu-id="3bf09-166">We will also publish hello staging version of Spark-EventHubs in GitHub.</span></span> <span data-ttu-id="3bf09-167">version de mise en lots hello toouse de Spark-EventHubs, hello première étape consiste tooindicate GitHub comme hello référentiel de code source en ajoutant hello suivant toopom.xml d’entrée :</span><span class="sxs-lookup"><span data-stu-id="3bf09-167">toouse hello staging version of Spark-EventHubs, hello first step is tooindicate GitHub as hello source repo by adding hello following entry toopom.xml:</span></span>

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

<span data-ttu-id="3bf09-168">Vous pouvez ensuite ajouter hello suivant dépendance tooyour projet tootake hello version précédente.</span><span class="sxs-lookup"><span data-stu-id="3bf09-168">You can then add hello following dependency tooyour project tootake hello pre-released version.</span></span>

<span data-ttu-id="3bf09-169">Dépendance Maven</span><span class="sxs-lookup"><span data-stu-id="3bf09-169">Maven Dependency</span></span>

```xml
<!-- https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11 -->
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>spark-streaming-eventhubs_2.11</artifactId>
    <version>2.0.4</version>
</dependency>
```

<span data-ttu-id="3bf09-170">Dépendance SBT</span><span class="sxs-lookup"><span data-stu-id="3bf09-170">SBT Dependency</span></span>

```
// https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11
libraryDependencies += "com.microsoft.azure" % "spark-streaming-eventhubs_2.11" % "2.0.4"
```

### <a name="direct-dstream-connection"></a><span data-ttu-id="3bf09-171">Connexion Direct DStream</span><span class="sxs-lookup"><span data-stu-id="3bf09-171">Direct DStream Connection</span></span>

<span data-ttu-id="3bf09-172">Un fichier jar prégénéré contenant des exemples utilisant Direct DStream peut être téléchargé dans [http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar](http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar).</span><span class="sxs-lookup"><span data-stu-id="3bf09-172">A pre-built jar file containing examples using Direct DStream can be downloaded in [http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar](http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar).</span></span>

<span data-ttu-id="3bf09-173">le fichier jar Hello contient trois exemples dont le code source sont disponibles au [https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream](https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream).</span><span class="sxs-lookup"><span data-stu-id="3bf09-173">hello jar file contains three examples whose source code are available at [https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream](https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream).</span></span>

<span data-ttu-id="3bf09-174">Utilisons [WindowingWordCount](https://github.com/hdinsight/spark-eventhubs/blob/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream/WindowingWordCount.scala) comme exemple :</span><span class="sxs-lookup"><span data-stu-id="3bf09-174">Taking [WindowingWordCount](https://github.com/hdinsight/spark-eventhubs/blob/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream/WindowingWordCount.scala) as an example:</span></span>

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

<span data-ttu-id="3bf09-175">Bonjour au-dessus de l’exemple, `eventhubParameters` sont hello paramètres spécifiques tooa EventHubs uniques et que vous avez toopass il toohello `createDirectStreams` API qui crée un espace de concentrateurs d’événements tooa DStream Direct objet mappage noms.</span><span class="sxs-lookup"><span data-stu-id="3bf09-175">In hello above example, `eventhubParameters` are hello parameters specific tooa single EventHubs instance and you have toopass it toohello `createDirectStreams` API which constructs a Direct DStream object mapping tooa Event Hubs namespace.</span></span> <span data-ttu-id="3bf09-176">Sur l’objet DStream directe de hello, vous pouvez appeler toute API DStream fournie par l’infrastructure de l’API de diffusion en continu de Spark.</span><span class="sxs-lookup"><span data-stu-id="3bf09-176">Over hello Direct DStream object, you can call any DStream API provided by Spark Streaming API framework.</span></span> <span data-ttu-id="3bf09-177">Dans cet exemple, nous calculons fréquence hello de chaque mot dans des intervalles de lot micro 3 dernière hello.</span><span class="sxs-lookup"><span data-stu-id="3bf09-177">In this example, we calculate hello frequency of each word within hello last 3 micro batch intervals.</span></span>

### <a name="receiver-based-connection"></a><span data-ttu-id="3bf09-178">Connexion basée sur récepteur</span><span class="sxs-lookup"><span data-stu-id="3bf09-178">Receiver-based Connection</span></span>

<span data-ttu-id="3bf09-179">Un Spark écrite dans Scala, qui reçoit les événements et les destinations de routage hello toodifferent, exemple d’application de diffusion en continu est disponible à l’adresse [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span><span class="sxs-lookup"><span data-stu-id="3bf09-179">A Spark streaming example application written in Scala, which receives events and route hello toodifferent destinations, is available at [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span></span> <span data-ttu-id="3bf09-180">Suivez les étapes de hello sous l’application de hello tooupdate pour votre configuration de concentrateur d’événements et créez des hello sortie jar.</span><span class="sxs-lookup"><span data-stu-id="3bf09-180">Follow hello steps below tooupdate hello application for your Event Hub configuration and create hello output jar.</span></span>

1. <span data-ttu-id="3bf09-181">Lancez l’idée de IntelliJ et de hello lancer l’écran, sélectionnez **extraire du contrôle de Version** puis cliquez sur **Git**.</span><span class="sxs-lookup"><span data-stu-id="3bf09-181">Launch IntelliJ IDEA and from hello launch screen select **Check out from Version Control** and then click **Git**.</span></span>
   
    <span data-ttu-id="3bf09-182">![Exemple de diffusion en continu Apache Spark - obtenir des sources de Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-get-source-from-git.png "Exemple de diffusion en continu Apache Spark - obtenir des sources de Git")</span><span class="sxs-lookup"><span data-stu-id="3bf09-182">![Apache Spark streaming example - get sources from Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-get-source-from-git.png "Apache Spark streaming example - get sources from Git")</span></span>

2. <span data-ttu-id="3bf09-183">Bonjour **Clone référentiel** boîte de dialogue, fournissez hello URL toohello Git référentiel tooclone à partir de, spécifiez tooclone de répertoire hello pour, puis cliquez sur **Clone**.</span><span class="sxs-lookup"><span data-stu-id="3bf09-183">In hello **Clone Repository** dialog box, provide hello URL toohello Git repository tooclone from, specify hello directory tooclone to, and then click **Clone**.</span></span>
   
    <span data-ttu-id="3bf09-184">![Exemple de diffusion en continu Apache Spark - cloner Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-clone-from-git.png "Exemple de diffusion en continu Apache Spark - cloner Git")</span><span class="sxs-lookup"><span data-stu-id="3bf09-184">![Apache Spark streaming example - clone from Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-clone-from-git.png "Apache Spark streaming example - clone from Git")</span></span>
3. <span data-ttu-id="3bf09-185">Suivez les invites de hello jusqu'à ce que le projet de hello est entièrement cloné.</span><span class="sxs-lookup"><span data-stu-id="3bf09-185">Follow hello prompts till hello project is completely cloned.</span></span> <span data-ttu-id="3bf09-186">Appuyez sur **Alt + 1** tooopen hello **vue projet**.</span><span class="sxs-lookup"><span data-stu-id="3bf09-186">Press **Alt + 1** tooopen hello **Project View**.</span></span> <span data-ttu-id="3bf09-187">Il doit ressembler à suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="3bf09-187">It should resemble hello following.</span></span>
   
    <span data-ttu-id="3bf09-188">![Exemple de diffusion en continu Apache Spark - Affichage de projet](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-project-view.png "Exemple de diffusion en continu Apache Spark - Affichage de projet")</span><span class="sxs-lookup"><span data-stu-id="3bf09-188">![Apache Spark streaming example - Project View](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-project-view.png "Apache Spark streaming example - Project View")</span></span>
4. <span data-ttu-id="3bf09-189">Assurez-vous que le code de l’application hello est compilé avec Java8.</span><span class="sxs-lookup"><span data-stu-id="3bf09-189">Make sure hello application code is compiled with Java8.</span></span> <span data-ttu-id="3bf09-190">tooensure, cliquez sur **fichier**, cliquez sur **Structure de projet**et sur hello **projet** onglet, vérifiez qu’au niveau du projet language est défini trop**8 - les expressions lambda, type annotations, etc.**.</span><span class="sxs-lookup"><span data-stu-id="3bf09-190">tooensure this, click **File**, click **Project Structure**, and on hello **Project** tab, make sure Project language level is set too**8 - Lambdas, type annotations, etc.**.</span></span>
   
    <span data-ttu-id="3bf09-191">![Exemple de diffusion en continu Apache Spark - Définir un compilateur](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-java-8-compiler.png "Exemple de diffusion en continu Apache Spark - Définir un compilateur")</span><span class="sxs-lookup"><span data-stu-id="3bf09-191">![Apache Spark streaming example - Set compiler](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-java-8-compiler.png "Apache Spark streaming example - Set compiler")</span></span>
5. <span data-ttu-id="3bf09-192">Ouvrez hello **pom.xml** et assurez-vous que la version de Spark hello est correcte.</span><span class="sxs-lookup"><span data-stu-id="3bf09-192">Open hello **pom.xml** and make sure hello Spark version is correct.</span></span> <span data-ttu-id="3bf09-193">Sous `<properties>` nœud, recherchez hello suivant extrait et vérifier la version de Spark hello.</span><span class="sxs-lookup"><span data-stu-id="3bf09-193">Under `<properties>` node, look for hello following snippet and verify hello Spark version.</span></span>

        <scala.version>2.11.8</scala.version>
        <scala.compat.version>2.11.8</scala.compat.version>
        <scala.binary.version>2.11</scala.binary.version>
        <spark.version>2.0.0</spark.version>

6. <span data-ttu-id="3bf09-194">application Hello nécessite un fichier jar de dépendance appelé **jar du pilote JDBC**.</span><span class="sxs-lookup"><span data-stu-id="3bf09-194">hello application requires a dependency jar called **JDBC driver jar**.</span></span> <span data-ttu-id="3bf09-195">Il s’agit de messages de type hello toowrite requis provenant du concentrateur d’événements dans une base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="3bf09-195">This is required toowrite hello messages received from Event Hub into an Azure SQL database.</span></span> <span data-ttu-id="3bf09-196">Vous pouvez télécharger ce fichier jar (version 4.1 ou version ultérieure) à partir d’[ici](https://msdn.microsoft.com/sqlserver/aa937724.aspx).</span><span class="sxs-lookup"><span data-stu-id="3bf09-196">You can download this jar (v4.1 or later) from [here](https://msdn.microsoft.com/sqlserver/aa937724.aspx).</span></span> <span data-ttu-id="3bf09-197">Ajoutez la référence toothis jar dans la bibliothèque de projet hello.</span><span class="sxs-lookup"><span data-stu-id="3bf09-197">Add reference toothis jar in hello project library.</span></span> <span data-ttu-id="3bf09-198">Effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="3bf09-198">Perform hello following steps:</span></span>
     
     1. <span data-ttu-id="3bf09-199">Dans la fenêtre IntelliJ idée où vous avez application hello ouvert, cliquez sur **fichier**, cliquez sur **Structure de projet**, puis cliquez sur **bibliothèques**.</span><span class="sxs-lookup"><span data-stu-id="3bf09-199">From IntelliJ IDEA window where you have hello application open, click **File**, click **Project Structure**, and then click **Libraries**.</span></span> 
     2. <span data-ttu-id="3bf09-200">Cliquez sur hello icône d’ajout (![icône d’ajout de](./media/hdinsight-apache-spark-eventhub-streaming/add-icon.png)), cliquez sur **Java**, puis accédez emplacement toohello où vous avez téléchargé le jar de pilote JDBC hello.</span><span class="sxs-lookup"><span data-stu-id="3bf09-200">Click hello add icon (![add icon](./media/hdinsight-apache-spark-eventhub-streaming/add-icon.png)), click **Java**, and then navigate toohello location where you downloaded hello JDBC driver jar.</span></span> <span data-ttu-id="3bf09-201">Suivez les bibliothèque de projet toohello hello jar fichier hello invites tooadd.</span><span class="sxs-lookup"><span data-stu-id="3bf09-201">Follow hello prompts tooadd hello jar file toohello project library.</span></span>

         <span data-ttu-id="3bf09-202">![ajouter les dépendances manquantes](./media/hdinsight-apache-spark-eventhub-streaming/add-missing-dependency-jars.png "Ajouter les fichiers jars de dépendance manquants")</span><span class="sxs-lookup"><span data-stu-id="3bf09-202">![add missing dependencies](./media/hdinsight-apache-spark-eventhub-streaming/add-missing-dependency-jars.png "Add missing dependency jars")</span></span>
     3. <span data-ttu-id="3bf09-203">Cliquez sur **Apply**.</span><span class="sxs-lookup"><span data-stu-id="3bf09-203">Click **Apply**.</span></span>

7. <span data-ttu-id="3bf09-204">Créer le fichier jar de sortie hello.</span><span class="sxs-lookup"><span data-stu-id="3bf09-204">Create hello output jar file.</span></span> <span data-ttu-id="3bf09-205">Effectuer hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="3bf09-205">Perform hello following steps.</span></span>

   1. <span data-ttu-id="3bf09-206">Bonjour **Structure de projet** boîte de dialogue, cliquez sur **artefacts** puis hello plus de symbole.</span><span class="sxs-lookup"><span data-stu-id="3bf09-206">In hello **Project Structure** dialog box, click **Artifacts** and then click hello plus symbol.</span></span> <span data-ttu-id="3bf09-207">Dans la boîte de dialogue contextuelle hello, cliquez sur **JAR**, puis cliquez sur **à partir de modules avec des dépendances**.</span><span class="sxs-lookup"><span data-stu-id="3bf09-207">From hello pop-up dialog box, click **JAR**, and then click **From modules with dependencies**.</span></span>      
       
       <span data-ttu-id="3bf09-208">![Exemple de diffusion en continu Apache Spark - créer un fichier jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar.png "Exemple de diffusion en continu Apache Spark - créer un fichier jar")</span><span class="sxs-lookup"><span data-stu-id="3bf09-208">![Apache Spark streaming example - create JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar.png "Apache Spark streaming example - create JAR")</span></span>
   2. <span data-ttu-id="3bf09-209">Bonjour **créer JAR à partir de Modules** boîte de dialogue, cliquez sur les points de suspension hello (![points de suspension](./media/hdinsight-apache-spark-eventhub-streaming/ellipsis.png)) par rapport à hello **principale classe**.</span><span class="sxs-lookup"><span data-stu-id="3bf09-209">In hello **Create JAR from Modules** dialog box, click hello ellipsis (![ellipsis](./media/hdinsight-apache-spark-eventhub-streaming/ellipsis.png)) against hello **Main Class**.</span></span>
   3. <span data-ttu-id="3bf09-210">Bonjour **sélection de la classe principale** boîte de dialogue zone, sélectionnez une des classes disponibles de hello, puis sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="3bf09-210">In hello **Select Main Class** dialog box, select any of hello available classes and then click **OK**.</span></span>
      
       <span data-ttu-id="3bf09-211">![Exemple de diffusion en continu Apache Spark - sélectionner une classe pour un fichier jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-select-class-for-jar.png "Exemple de diffusion en continu Apache Spark - sélectionner une classe pour un fichier jar")</span><span class="sxs-lookup"><span data-stu-id="3bf09-211">![Apache Spark streaming example - select class for jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-select-class-for-jar.png "Apache Spark streaming example - select class for jar")</span></span>
   4. <span data-ttu-id="3bf09-212">Bonjour **créer JAR à partir de Modules** boîte de dialogue zone, assurez-vous que cette option hello trop**extraire toohello cible JAR** est sélectionné, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="3bf09-212">In hello **Create JAR from Modules** dialog box, make sure that hello option too**extract toohello target JAR** is selected, and then click **OK**.</span></span> <span data-ttu-id="3bf09-213">Cela crée un fichier JAR contenant toutes les dépendances.</span><span class="sxs-lookup"><span data-stu-id="3bf09-213">This creates a single JAR with all dependencies.</span></span>
      
       <span data-ttu-id="3bf09-214">![Exemple de diffusion en continu Apache Spark - créer un fichier jar à partir de modules](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar-from-modules.png "Exemple de diffusion en continu Apache Spark - créer un fichier jar à partir de modules")</span><span class="sxs-lookup"><span data-stu-id="3bf09-214">![Apache Spark streaming example - create jar from modules](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar-from-modules.png "Apache Spark streaming example - create jar from modules")</span></span>
   5. <span data-ttu-id="3bf09-215">Hello **mise en page de sortie** onglet répertorie tous les fichiers JAR hello qui sont inclus dans le cadre du projet de Maven hello.</span><span class="sxs-lookup"><span data-stu-id="3bf09-215">hello **Output Layout** tab lists all hello jars that are included as part of hello Maven project.</span></span> <span data-ttu-id="3bf09-216">Vous pouvez sélectionner et hello supprimer ceux sur lesquels hello Scala application ne possède pas de dépendance directe.</span><span class="sxs-lookup"><span data-stu-id="3bf09-216">You can select and delete hello ones on which hello Scala application has no direct dependency.</span></span> <span data-ttu-id="3bf09-217">Pour l’application hello, nous allons créer ici, vous pouvez supprimer tout sauf hello dernière (**spark-diffusion en continu--persistance-exemples de données de compilation sortie**).</span><span class="sxs-lookup"><span data-stu-id="3bf09-217">For hello application we are creating here, you can remove all but hello last one (**spark-streaming-data-persistence-examples compile output**).</span></span> <span data-ttu-id="3bf09-218">Sélectionnez hello JAR toodelete, puis cliquez sur hello **supprimer** icône (![icône Supprimer](./media/hdinsight-apache-spark-eventhub-streaming/delete-icon.png)).</span><span class="sxs-lookup"><span data-stu-id="3bf09-218">Select hello jars toodelete and then click hello **Delete** icon (![delete icon](./media/hdinsight-apache-spark-eventhub-streaming/delete-icon.png)).</span></span>
      
       <span data-ttu-id="3bf09-219">![Exemple de diffusion en continu Apache Spark - supprimer un fichier jar extrait](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-delete-output-jars.png "Exemple de diffusion en continu Apache Spark - supprimer un fichier jar extrait")</span><span class="sxs-lookup"><span data-stu-id="3bf09-219">![Apache Spark streaming example - delete extracted jars](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-delete-output-jars.png "Apache Spark streaming example - delete extracted jars")</span></span>
      
       <span data-ttu-id="3bf09-220">Assurez-vous que **Build sur Vérifiez** à cocher est activée, ce qui garantit que ce fichier jar hello est créé chaque fois que projet de hello est généré ou mis à jour.</span><span class="sxs-lookup"><span data-stu-id="3bf09-220">Make sure **Build on make** box is selected, which ensures that hello jar is created every time hello project is built or updated.</span></span> <span data-ttu-id="3bf09-221">Cliquez sur **Apply**.</span><span class="sxs-lookup"><span data-stu-id="3bf09-221">Click **Apply**.</span></span>
   6. <span data-ttu-id="3bf09-222">Bonjour **mise en page de sortie** onglet, à droite en bas de hello de hello **éléments disponibles** zone, que vous avez jar SQL JDBC hello que vous avez ajouté de bibliothèque de projet toohello antérieur.</span><span class="sxs-lookup"><span data-stu-id="3bf09-222">In hello **Output Layout** tab, right at hello bottom of hello **Available Elements** box, you have hello SQL JDBC jar that you added earlier toohello project library.</span></span> <span data-ttu-id="3bf09-223">Vous devez ajouter cette toohello **mise en page de sortie** onglet. Cliquez sur le fichier jar hello, puis cliquez sur **extraire dans la racine de sortie**.</span><span class="sxs-lookup"><span data-stu-id="3bf09-223">You must add this toohello **Output Layout** tab. Right-click hello jar file, and then click **Extract Into Output Root**.</span></span>
      
       <span data-ttu-id="3bf09-224">![Exemple de diffusion en continu Apache Spark - extraire un fichier jar de dépendance](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-extract-dependency-jar.png "Exemple de diffusion en continu Apache Spark - extraire un fichier jar de dépendance")</span><span class="sxs-lookup"><span data-stu-id="3bf09-224">![Apache Spark streaming example - extract dependency jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-extract-dependency-jar.png "Apache Spark streaming example - extract dependency jar")</span></span>  
      
       <span data-ttu-id="3bf09-225">Hello **mise en page de sortie** onglet doit maintenant ressembler à ceci.</span><span class="sxs-lookup"><span data-stu-id="3bf09-225">hello **Output Layout** tab should now look like this.</span></span>
      
       <span data-ttu-id="3bf09-226">![Exemple de diffusion en continu Apache Spark - onglet de sortie finale](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-final-output-tab.png "Exemple de diffusion en continu Apache Spark - onglet de sortie finale")</span><span class="sxs-lookup"><span data-stu-id="3bf09-226">![Apache Spark streaming example - final output tab](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-final-output-tab.png "Apache Spark streaming example - final output tab")</span></span>        
      
       <span data-ttu-id="3bf09-227">Bonjour **Structure de projet** boîte de dialogue, cliquez sur **appliquer** puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="3bf09-227">In hello **Project Structure** dialog box, click **Apply** and then click **OK**.</span></span>    
   7. <span data-ttu-id="3bf09-228">Dans la barre de menus de hello, cliquez sur **générer**, puis cliquez sur **créer le projet**.</span><span class="sxs-lookup"><span data-stu-id="3bf09-228">From hello menu bar, click **Build**, and then click **Make Project**.</span></span> <span data-ttu-id="3bf09-229">Vous pouvez également cliquer sur **des artefacts de Build** jar de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="3bf09-229">You can also click **Build Artifacts** toocreate hello jar.</span></span> <span data-ttu-id="3bf09-230">Hello jar de sortie est créé sous **\classes\artifacts**.</span><span class="sxs-lookup"><span data-stu-id="3bf09-230">hello output jar is created under **\classes\artifacts**.</span></span>
      
       <span data-ttu-id="3bf09-231">![Exemple de diffusion en continu Apache Spark - fichier jar de sortie](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-output-jar.png "Exemple de diffusion en continu Apache Spark - fichier jar de sortie")</span><span class="sxs-lookup"><span data-stu-id="3bf09-231">![Apache Spark streaming example - output JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-output-jar.png "Apache Spark streaming example - output JAR")</span></span>

## <a name="run-hello-application-remotely-on-a-spark-cluster-using-livy"></a><span data-ttu-id="3bf09-232">Exécuter des application hello à distance sur un cluster Spark à l’aide de Livy</span><span class="sxs-lookup"><span data-stu-id="3bf09-232">Run hello application remotely on a Spark cluster using Livy</span></span>

<span data-ttu-id="3bf09-233">Dans cet article vous utilisez Livy toorun hello Apache Spark diffusion en continu application à distance sur un cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="3bf09-233">In this article you use Livy toorun hello Apache Spark streaming application remotely on a Spark cluster.</span></span> <span data-ttu-id="3bf09-234">Pour obtenir une présentation détaillée sur comment toouse Livy avec HDInsight Spark de cluster, consultez [travaux d’envoi à distance tooan Apache Spark cluster sur Azure HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span><span class="sxs-lookup"><span data-stu-id="3bf09-234">For detailed discussion on how toouse Livy with HDInsight Spark cluster, see [Submit jobs remotely tooan Apache Spark cluster on Azure HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span></span> <span data-ttu-id="3bf09-235">Avant de démarrer l’application de diffusion en continu de Spark hello en cours d’exécution, il existe deux choses à faire :</span><span class="sxs-lookup"><span data-stu-id="3bf09-235">Before you can start running hello Spark streaming application, there are a couple of things you should do:</span></span>

1. <span data-ttu-id="3bf09-236">Début hello toogenerate les événements d’application local autonome et envoyé tooEvent Hub.</span><span class="sxs-lookup"><span data-stu-id="3bf09-236">Start hello local standalone application toogenerate events and sent tooEvent Hub.</span></span> <span data-ttu-id="3bf09-237">Utilisez hello suivant commande toodo ainsi :</span><span class="sxs-lookup"><span data-stu-id="3bf09-237">Use hello following command toodo so:</span></span>

        java -cp com-microsoft-azure-eventhubs-client-example-0.2.0.jar com.microsoft.eventhubs.client.example.EventhubsClientDriver --eventhubs-namespace "mysbnamespace" --eventhubs-name "myeventhub" --policy-name "mysendpolicy" --policy-key "<policy key>" --message-length 32 --thread-count 32 --message-count -1

2. <span data-ttu-id="3bf09-238">Hello copie jar de diffusion en continu (**spark-diffusion en continu-données-persistance-Examples.jar**) toohello stockage d’objets Blob Azure associé hello cluster.</span><span class="sxs-lookup"><span data-stu-id="3bf09-238">Copy hello streaming jar (**spark-streaming-data-persistence-examples.jar**) toohello Azure Blob storage associated with hello cluster.</span></span> <span data-ttu-id="3bf09-239">Cela rend tooLivy accessible de hello jar.</span><span class="sxs-lookup"><span data-stu-id="3bf09-239">This makes hello jar accessible tooLivy.</span></span> <span data-ttu-id="3bf09-240">Vous pouvez utiliser [ **AzCopy**](../storage/common/storage-use-azcopy.md), par conséquent, utilitaire, toodo une commande de ligne.</span><span class="sxs-lookup"><span data-stu-id="3bf09-240">You can use [**AzCopy**](../storage/common/storage-use-azcopy.md), a command line utility, toodo so.</span></span> <span data-ttu-id="3bf09-241">Il existe beaucoup d’autres clients, vous pouvez utiliser les données tooupload.</span><span class="sxs-lookup"><span data-stu-id="3bf09-241">There are a lot of other clients you can use tooupload data.</span></span> <span data-ttu-id="3bf09-242">Pour en savoir plus à leur sujet, consultez [Téléchargement de données pour les travaux Hadoop dans HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="3bf09-242">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>
3. <span data-ttu-id="3bf09-243">Installez CURL sur hello ordinateur sur lequel vous exécutez ces applications à partir de.</span><span class="sxs-lookup"><span data-stu-id="3bf09-243">Install CURL on hello computer where you are running these applications from.</span></span> <span data-ttu-id="3bf09-244">Nous utilisons hello de tooinvoke CURL hello de toorun de points de terminaison Livy des travaux à distance.</span><span class="sxs-lookup"><span data-stu-id="3bf09-244">We use CURL tooinvoke hello Livy endpoints toorun hello jobs remotely.</span></span>

### <a name="run-hello-spark-streaming-application-tooreceive-hello-events-into-an-azure-storage-blob-as-text"></a><span data-ttu-id="3bf09-245">Exécutez hello Spark diffusion en continu tooreceive hello événements de l’application dans un objet Blob de stockage Azure sous forme de texte</span><span class="sxs-lookup"><span data-stu-id="3bf09-245">Run hello Spark streaming application tooreceive hello events into an Azure Storage Blob as text</span></span>

<span data-ttu-id="3bf09-246">Ouvrez une invite de commandes, accédez répertoire toohello où vous avez installé CURL et exécutez hello (remplacer le nom d’utilisateur/mot de passe et du cluster) de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="3bf09-246">Open a command prompt, navigate toohello directory where you installed CURL, and run hello following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputBlob.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="3bf09-247">Hello paramètres hello fichier **inputBlob.txt** sont définies comme suit :</span><span class="sxs-lookup"><span data-stu-id="3bf09-247">hello parameters in hello file **inputBlob.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsEventCount", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="3bf09-248">Découvrons que sont les paramètres hello hello fichier d’entrée :</span><span class="sxs-lookup"><span data-stu-id="3bf09-248">Let us understand what hello parameters in hello input file are:</span></span>

* <span data-ttu-id="3bf09-249">**fichier** est fichier hello chemin d’accès toohello application jar sur le compte de stockage Azure hello associé hello cluster.</span><span class="sxs-lookup"><span data-stu-id="3bf09-249">**file** is hello path toohello application jar file on hello Azure storage account associated with hello cluster.</span></span>
* <span data-ttu-id="3bf09-250">**className** est le nom hello de classe hello dans jar de hello.</span><span class="sxs-lookup"><span data-stu-id="3bf09-250">**className** is hello name of hello class in hello jar.</span></span>
* <span data-ttu-id="3bf09-251">**args** liste hello d’arguments requis par la classe hello</span><span class="sxs-lookup"><span data-stu-id="3bf09-251">**args** is hello list of arguments required by hello class</span></span>
* <span data-ttu-id="3bf09-252">**numExecutors** est nombre hello de noyaux utilisés par hello de toorun Spark application de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="3bf09-252">**numExecutors** is hello number of cores used by Spark toorun hello streaming application.</span></span> <span data-ttu-id="3bf09-253">Il doit toujours être au moins deux fois hello différentes partitions du Hub d’événements.</span><span class="sxs-lookup"><span data-stu-id="3bf09-253">This should always be at least twice hello number of Event Hub partitions.</span></span>
* <span data-ttu-id="3bf09-254">**executorMemory**, **executorCores**, **driverMemory** sont des applications de diffusion en continu toohello ressources tooassign requis de paramètres utilisés.</span><span class="sxs-lookup"><span data-stu-id="3bf09-254">**executorMemory**, **executorCores**, **driverMemory** are parameters used tooassign required resources toohello streaming application.</span></span>

> [!NOTE]
> <span data-ttu-id="3bf09-255">Vous n’avez pas besoin de toocreate hello dossiers de sortie (EventCheckpoint, nombre d’événements/EventCount10) qui sont utilisées comme paramètres.</span><span class="sxs-lookup"><span data-stu-id="3bf09-255">You do not need toocreate hello output folders (EventCheckpoint, EventCount/EventCount10) that are used as parameters.</span></span> <span data-ttu-id="3bf09-256">application de diffusion en continu de Hello crée pour vous.</span><span class="sxs-lookup"><span data-stu-id="3bf09-256">hello streaming application creates them for you.</span></span>
>
>

<span data-ttu-id="3bf09-257">Lorsque vous exécutez la commande hello, vous devez voir une sortie semblable à hello suivante :</span><span class="sxs-lookup"><span data-stu-id="3bf09-257">When you run hello command, you should see an output like hello following:</span></span>

    < HTTP/1.1 201 Created
    < Content-Type: application/json; charset=UTF-8
    < Location: /18
    < Server: Microsoft-IIS/8.5
    < X-Powered-By: ARR/2.5
    < X-Powered-By: ASP.NET
    < Date: Tue, 01 Dec 2015 05:39:10 GMT
    < Content-Length: 37
    <
    {"id":1,"state":"starting","log":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact

<span data-ttu-id="3bf09-258">Prenez note de l’ID de lot hello dans hello dernière ligne de sortie hello (dans cet exemple, il est « 1 »).</span><span class="sxs-lookup"><span data-stu-id="3bf09-258">Make a note of hello batch ID in hello last line of hello output (in this example it is '1').</span></span> <span data-ttu-id="3bf09-259">tooverify qui hello application s’exécute correctement, vous pouvez consulter votre compte de stockage Azure associé hello cluster et vous devez voir hello **/nombre d’événements/EventCount10** dossier créé.</span><span class="sxs-lookup"><span data-stu-id="3bf09-259">tooverify that hello application runs successfully, you can look at your Azure storage account associated with hello cluster and you should see hello **/EventCount/EventCount10** folder created there.</span></span> <span data-ttu-id="3bf09-260">Ce dossier doit contenir les objets BLOB qui capture le nombre de hello d’événements traités au sein de hello période de temps spécifiée pour le paramètre hello **lot intervalle en secondes**.</span><span class="sxs-lookup"><span data-stu-id="3bf09-260">This folder should contain blobs that captures hello number of events processed within hello time period specified for hello parameter **batch-interval-in-seconds**.</span></span>

<span data-ttu-id="3bf09-261">application de diffusion en continu de Spark Hello continuera toorun jusqu'à ce que vous l’arrêter.</span><span class="sxs-lookup"><span data-stu-id="3bf09-261">hello Spark streaming application will continue toorun until you kill it.</span></span> <span data-ttu-id="3bf09-262">toodo utilisez donc hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="3bf09-262">toodo so, use hello following command:</span></span>

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/1"

### <a name="run-hello-applications-tooreceive-hello-events-into-an-azure-storage-blob-as-json"></a><span data-ttu-id="3bf09-263">Exécuter des applications de hello les événements hello tooreceive dans un objet Blob de stockage Azure en tant que JSON</span><span class="sxs-lookup"><span data-stu-id="3bf09-263">Run hello applications tooreceive hello events into an Azure Storage Blob as JSON</span></span>
<span data-ttu-id="3bf09-264">Ouvrez une invite de commandes, accédez répertoire toohello où vous avez installé CURL et exécutez hello (remplacer le nom d’utilisateur/mot de passe et du cluster) de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="3bf09-264">Open a command prompt, navigate toohello directory where you installed CURL, and run hello following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputJSON.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="3bf09-265">Hello paramètres hello fichier **inputJSON.txt** sont définies comme suit :</span><span class="sxs-lookup"><span data-stu-id="3bf09-265">hello parameters in hello file **inputJSON.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureBlobAsJSON", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-store-folder", "/EventStore10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="3bf09-266">les paramètres de Hello sont similaires toowhat que vous avez spécifié pour la sortie de texte hello, dans l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="3bf09-266">hello parameters are similar toowhat you specified for hello text output, in hello previous step.</span></span> <span data-ttu-id="3bf09-267">Là encore, il est inutile toocreate hello dossiers de sortie (EventCheckpoint, nombre d’événements/EventCount10) qui sont utilisées comme paramètres.</span><span class="sxs-lookup"><span data-stu-id="3bf09-267">Again, you do not need toocreate hello output folders (EventCheckpoint, EventCount/EventCount10) that are used as parameters.</span></span> <span data-ttu-id="3bf09-268">application de diffusion en continu de Hello crée pour vous.</span><span class="sxs-lookup"><span data-stu-id="3bf09-268">hello streaming application creates them for you.</span></span>

 <span data-ttu-id="3bf09-269">Une fois que vous exécutez la commande hello, vous pouvez consulter votre compte de stockage Azure associé hello cluster et vous devez voir hello **/EventStore10** dossier créé.</span><span class="sxs-lookup"><span data-stu-id="3bf09-269">After you run hello command, you can look at your Azure storage account associated with hello cluster and you should see hello **/EventStore10** folder created there.</span></span> <span data-ttu-id="3bf09-270">Ouvrez n’importe quel fichier préfixe **partie -** et vous devez voir les événements de hello traités dans un format JSON.</span><span class="sxs-lookup"><span data-stu-id="3bf09-270">Open any file prefixed with **part-** and you should see hello events processed in a JSON format.</span></span>

### <a name="run-hello-applications-tooreceive-hello-events-into-a-hive-table"></a><span data-ttu-id="3bf09-271">Exécuter des applications de hello les événements hello tooreceive dans une table Hive</span><span class="sxs-lookup"><span data-stu-id="3bf09-271">Run hello applications tooreceive hello events into a Hive table</span></span>
<span data-ttu-id="3bf09-272">toorun hello application de diffusion en continu de Spark que les événements de flux de données dans une ruche tables que vous avez besoin des composants supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="3bf09-272">toorun hello Spark streaming application that streams events into a Hive table you need some additional components.</span></span> <span data-ttu-id="3bf09-273">Ces composants sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="3bf09-273">These are:</span></span>

* <span data-ttu-id="3bf09-274">datanucleus-api-jdo-3.2.6.jar</span><span class="sxs-lookup"><span data-stu-id="3bf09-274">datanucleus-api-jdo-3.2.6.jar</span></span>
* <span data-ttu-id="3bf09-275">datanucleus-SGBDR-3.2.9.jar</span><span class="sxs-lookup"><span data-stu-id="3bf09-275">datanucleus-rdbms-3.2.9.jar</span></span>
* <span data-ttu-id="3bf09-276">datanucleus-core-3.2.10.jar</span><span class="sxs-lookup"><span data-stu-id="3bf09-276">datanucleus-core-3.2.10.jar</span></span>
* <span data-ttu-id="3bf09-277">hive-site.xml</span><span class="sxs-lookup"><span data-stu-id="3bf09-277">hive-site.xml</span></span>

<span data-ttu-id="3bf09-278">Hello **.jar** fichiers sont disponibles sur votre cluster HDInsight Spark à `/usr/hdp/current/spark-client/lib`.</span><span class="sxs-lookup"><span data-stu-id="3bf09-278">hello **.jar** files are available on your HDInsight Spark cluster at `/usr/hdp/current/spark-client/lib`.</span></span> <span data-ttu-id="3bf09-279">Hello **hive-site.XML** est disponible à l’adresse `/usr/hdp/current/spark-client/conf`.</span><span class="sxs-lookup"><span data-stu-id="3bf09-279">hello **hive-site.xml** is available at `/usr/hdp/current/spark-client/conf`.</span></span>

<span data-ttu-id="3bf09-280">Vous pouvez utiliser [WinScp](http://winscp.net/eng/download.php) toocopy ces fichiers à partir de l’ordinateur local de hello cluster tooyour.</span><span class="sxs-lookup"><span data-stu-id="3bf09-280">You can use [WinScp](http://winscp.net/eng/download.php) toocopy over these files from hello cluster tooyour local computer.</span></span> <span data-ttu-id="3bf09-281">Vous pouvez ensuite utiliser toocopy outils ces fichiers sur le compte de stockage tooyour associées au cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="3bf09-281">You can then use tools toocopy these files over tooyour storage account associated with hello cluster.</span></span> <span data-ttu-id="3bf09-282">Pour plus d’informations sur l’utilisation des fichiers de compte de stockage toohello tooupload, consultez [télécharger des données pour les travaux Hadoop dans HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="3bf09-282">For more information on how tooupload files toohello storage account, see [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

<span data-ttu-id="3bf09-283">Une fois que vous avez copié les fichiers de hello tooyour compte de stockage Azure, ouvrez une invite de commandes, accédez répertoire toohello où vous avez installé CURL et exécutez hello (remplacer le nom d’utilisateur/mot de passe et du cluster) de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="3bf09-283">Once you have copied over hello files tooyour Azure storage account, open a command prompt, navigate toohello directory where you installed CURL, and run hello following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputHive.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="3bf09-284">Hello paramètres hello fichier **inputHive.txt** sont définies comme suit :</span><span class="sxs-lookup"><span data-stu-id="3bf09-284">hello parameters in hello file **inputHive.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToHiveTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-hive-table", "EventHiveTable10" ], "jars":["wasb:///example/jars/datanucleus-api-jdo-3.2.6.jar", "wasb:///example/jars/datanucleus-rdbms-3.2.9.jar", "wasb:///example/jars/datanucleus-core-3.2.10.jar"], "files":["wasb:///example/jars/hive-site.xml"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="3bf09-285">les paramètres de Hello sont similaires toowhat que vous avez spécifié pour la sortie de texte hello, dans les étapes précédentes hello.</span><span class="sxs-lookup"><span data-stu-id="3bf09-285">hello parameters are similar toowhat you specified for hello text output, in hello previous steps.</span></span> <span data-ttu-id="3bf09-286">Là encore, vous ne devez pas de sortie de hello toocreate table Hive (EventHiveTable10) qui sont utilisées comme paramètres de sortie de dossiers (EventCheckpoint, nombre d’événements/EventCount10) ou hello.</span><span class="sxs-lookup"><span data-stu-id="3bf09-286">Again, you do not need toocreate hello output folders (EventCheckpoint, EventCount/EventCount10) or hello output Hive table (EventHiveTable10) that are used as parameters.</span></span> <span data-ttu-id="3bf09-287">application de diffusion en continu de Hello crée pour vous.</span><span class="sxs-lookup"><span data-stu-id="3bf09-287">hello streaming application creates them for you.</span></span> <span data-ttu-id="3bf09-288">Notez que hello **JAR** et **fichiers** option inclut les fichiers de chemins d’accès toohello .jar et hello hive-site.XML que vous avez copié sur le compte de stockage toohello.</span><span class="sxs-lookup"><span data-stu-id="3bf09-288">Note that hello **jars** and **files** option includes paths toohello .jar files and hello hive-site.xml that you copied over toohello storage account.</span></span>

<span data-ttu-id="3bf09-289">tooverify qui hello table hive a été créé avec succès, vous pouvez SSH en cluster de hello et exécution des requêtes Hive.</span><span class="sxs-lookup"><span data-stu-id="3bf09-289">tooverify that hello hive table was successfully created, you can SSH into hello cluster and run Hive queries.</span></span> <span data-ttu-id="3bf09-290">Pour obtenir des instructions, consultez [Utilisation de Hive avec Hadoop dans HDInsight avec SSH](hdinsight-hadoop-use-hive-ssh.md).</span><span class="sxs-lookup"><span data-stu-id="3bf09-290">For instructions, see [Use Hive with Hadoop in HDInsight with SSH](hdinsight-hadoop-use-hive-ssh.md).</span></span> <span data-ttu-id="3bf09-291">Une fois que vous êtes connecté à l’aide de SSH, vous pouvez exécuter hello suivant commande tooverify cette table Hive hello, **EventHiveTable10**, est créé.</span><span class="sxs-lookup"><span data-stu-id="3bf09-291">Once you are connected using SSH, you can run hello following command tooverify that hello Hive table, **EventHiveTable10**, is created.</span></span>

    show tables;

<span data-ttu-id="3bf09-292">Vous devez voir s’afficher une sortie similaire toohello :</span><span class="sxs-lookup"><span data-stu-id="3bf09-292">You should see an output similar toohello following:</span></span>

    OK
    eventhivetable10
    hivesampletable

<span data-ttu-id="3bf09-293">Vous pouvez également exécuter une requête SELECT contenu de hello tooview de la table de hello.</span><span class="sxs-lookup"><span data-stu-id="3bf09-293">You can also run a SELECT query tooview hello contents of hello table.</span></span>

    SELECT * FROM eventhivetable10 LIMIT 10;

<span data-ttu-id="3bf09-294">Vous devez voir une sortie semblable à hello suivante :</span><span class="sxs-lookup"><span data-stu-id="3bf09-294">You should see an output like hello following:</span></span>

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


### <a name="run-hello-applications-tooreceive-hello-events-into-an-azure-sql-database-table"></a><span data-ttu-id="3bf09-295">Exécuter des applications de hello les événements hello tooreceive dans une table de base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="3bf09-295">Run hello applications tooreceive hello events into an Azure SQL database table</span></span>
<span data-ttu-id="3bf09-296">Avant d’exécuter cette étape, assurez-vous que vous disposez d’une base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="3bf09-296">Before running this step, make sure you have an Azure SQL database created.</span></span> <span data-ttu-id="3bf09-297">Pour obtenir des instructions, consultez [Créer une base de données SQL en quelques minutes](../sql-database/sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3bf09-297">For instructions, see [Create a SQL database in minutes](../sql-database/sql-database-get-started.md).</span></span> <span data-ttu-id="3bf09-298">toocomplete cette section, vous avez besoin de valeurs pour le nom de la base de données, nom du serveur de base de données et administrateur de base de données hello en tant que paramètres.</span><span class="sxs-lookup"><span data-stu-id="3bf09-298">toocomplete this section, you need values for database name, database server name, and hello database administrator credentials as parameters.</span></span> <span data-ttu-id="3bf09-299">Il est inutile table de base de données toocreate hello cependant.</span><span class="sxs-lookup"><span data-stu-id="3bf09-299">You do not need toocreate hello database table though.</span></span> <span data-ttu-id="3bf09-300">Hello application de diffusion en continu de Spark qui crée pour vous.</span><span class="sxs-lookup"><span data-stu-id="3bf09-300">hello Spark streaming application creates that for you.</span></span>

<span data-ttu-id="3bf09-301">Ouvrez une invite de commandes, accédez répertoire toohello où vous avez installé CURL et exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="3bf09-301">Open a command prompt, navigate toohello directory where you installed CURL, and run hello following command:</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputSQL.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="3bf09-302">Hello paramètres hello fichier **inputSQL.txt** sont définies comme suit :</span><span class="sxs-lookup"><span data-stu-id="3bf09-302">hello parameters in hello file **inputSQL.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureSQLTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--sql-server-fqdn", "<database-server-name>.database.windows.net", "--sql-database-name", "mysparkdatabase", "--database-username", "sparkdbadmin", "--database-password", "<put-password-here>", "--event-sql-table", "EventContent" ], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="3bf09-303">tooverify qui hello application s’exécute correctement, vous pouvez vous connecter à base de données SQL Azure toohello à l’aide de SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="3bf09-303">tooverify that hello application runs successfully, you can connect toohello Azure SQL database using SQL Server Management Studio.</span></span> <span data-ttu-id="3bf09-304">Pour obtenir des instructions sur la façon de toodo qui, consultez [connecter tooSQL de base de données avec SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="3bf09-304">For instructions on how toodo that, see [Connect tooSQL Database with SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md).</span></span> <span data-ttu-id="3bf09-305">Une fois que vous êtes connecté toohello de base de données, vous pouvez naviguer toohello **EventContent** table qui a été créé par l’application de diffusion en continu de hello.</span><span class="sxs-lookup"><span data-stu-id="3bf09-305">Once you are connected toohello database, you can navigate toohello **EventContent** table that was created by hello streaming application.</span></span> <span data-ttu-id="3bf09-306">Vous pouvez exécuter un requête rapide tooget hello de données à partir de la table de hello.</span><span class="sxs-lookup"><span data-stu-id="3bf09-306">You can run a quick query tooget hello data from hello table.</span></span> <span data-ttu-id="3bf09-307">Exécutez hello suivant la requête :</span><span class="sxs-lookup"><span data-stu-id="3bf09-307">Run hello following query:</span></span>

    SELECT * FROM EventCount

<span data-ttu-id="3bf09-308">Vous devez voir s’afficher sortie similaire toohello :</span><span class="sxs-lookup"><span data-stu-id="3bf09-308">You should see output similar toohello following:</span></span>

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


## <span data-ttu-id="3bf09-309"><a name="seealso"></a>Voir aussi</span><span class="sxs-lookup"><span data-stu-id="3bf09-309"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="3bf09-310">Vue d’ensemble : Apache Spark sur Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="3bf09-310">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)
* [<span data-ttu-id="3bf09-311">Conception de la connexion basée sur récepteur et Direct DStream</span><span class="sxs-lookup"><span data-stu-id="3bf09-311">Design of Receiver-based Connection and Direct DStream</span></span>](https://www.slideshare.net/NanZhu/seattle-sparkmeetup032317)

### <a name="scenarios"></a><span data-ttu-id="3bf09-312">Scénarios</span><span class="sxs-lookup"><span data-stu-id="3bf09-312">Scenarios</span></span>
* [<span data-ttu-id="3bf09-313">Spark avec BI : effectuez une analyse interactive des données à l’aide de Spark dans HDInsight avec des outils BI</span><span class="sxs-lookup"><span data-stu-id="3bf09-313">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="3bf09-314">Spark avec Machine Learning : utilisez Spark dans HDInsight pour l’analyse de la température des bâtiments à l’aide des données des systèmes HVAC</span><span class="sxs-lookup"><span data-stu-id="3bf09-314">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="3bf09-315">Spark avec Machine Learning : Spark utilisation dans résultats de l’inspection alimentaires toopredict HDInsight</span><span class="sxs-lookup"><span data-stu-id="3bf09-315">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="3bf09-316">Analyse des journaux de site web à l’aide de Spark dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="3bf09-316">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="3bf09-317">Créer et exécuter des applications</span><span class="sxs-lookup"><span data-stu-id="3bf09-317">Create and run applications</span></span>
* [<span data-ttu-id="3bf09-318">Créer une application autonome avec Scala</span><span class="sxs-lookup"><span data-stu-id="3bf09-318">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="3bf09-319">Exécuter des tâches à distance avec Livy sur un cluster Spark</span><span class="sxs-lookup"><span data-stu-id="3bf09-319">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="3bf09-320">Outils et extensions</span><span class="sxs-lookup"><span data-stu-id="3bf09-320">Tools and extensions</span></span>
* [<span data-ttu-id="3bf09-321">Utiliser le plug-in des outils HDInsight pour IntelliJ idée toocreate et soumettre des applications les plus importantes Spark Scala</span><span class="sxs-lookup"><span data-stu-id="3bf09-321">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="3bf09-322">Utiliser des plug-in des outils HDInsight pour les applications de Spark toodebug IntelliJ idée à distance</span><span class="sxs-lookup"><span data-stu-id="3bf09-322">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="3bf09-323">Utiliser des bloc-notes Zeppelin avec un cluster Spark sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="3bf09-323">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="3bf09-324">Noyaux disponibles pour le bloc-notes Jupyter dans un cluster Spark pour HDInsight</span><span class="sxs-lookup"><span data-stu-id="3bf09-324">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="3bf09-325">Utiliser des packages externes avec les blocs-notes Jupyter</span><span class="sxs-lookup"><span data-stu-id="3bf09-325">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="3bf09-326">Installer Notebook sur votre ordinateur et vous connecter tooan cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="3bf09-326">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="3bf09-327">Gestion des ressources</span><span class="sxs-lookup"><span data-stu-id="3bf09-327">Manage resources</span></span>
* [<span data-ttu-id="3bf09-328">Gérer les ressources de cluster d’Apache Spark hello dans Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="3bf09-328">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="3bf09-329">Track and debug jobs running on an Apache Spark cluster in HDInsight (Suivi et débogage des tâches en cours d’exécution sur un cluster Apache Spark dans HDInsight)</span><span class="sxs-lookup"><span data-stu-id="3bf09-329">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]: ../storage-create-storage-account/
