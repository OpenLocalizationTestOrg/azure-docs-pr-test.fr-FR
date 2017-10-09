---
title: "données de capteur aaaAnalyze avec Apache Storm et HBase | Documents Microsoft"
description: "Découvrez comment tooconnect tooApache renverser avec un réseau virtuel. Utilisez Storm avec des données de capteur tooprocess HBase à partir d’un concentrateur d’événements et le visualiser avec D3.js."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: a9a1ac8e-5708-4833-b965-e453815e671f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/09/2017
ms.author: larryfr
ms.openlocfilehash: e54fe9ffc720b0089f90e302b24a9438bd43999a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-sensor-data-with-apache-storm-event-hub-and-hbase-in-hdinsight-hadoop"></a><span data-ttu-id="a7711-104">Analyser les données de capteur avec Apache Storm, Event Hub, et HBase dans HDInsight (Hadoop)</span><span class="sxs-lookup"><span data-stu-id="a7711-104">Analyze sensor data with Apache Storm, Event Hub, and HBase in HDInsight (Hadoop)</span></span>

<span data-ttu-id="a7711-105">Découvrez comment toouse Apache renverser sur les données de capteur tooprocess HDInsight à partir du concentrateur d’événements Azure.</span><span class="sxs-lookup"><span data-stu-id="a7711-105">Learn how toouse Apache Storm on HDInsight tooprocess sensor data from Azure Event Hub.</span></span> <span data-ttu-id="a7711-106">les données de salutation sont ensuite stockées dans HBase Apache sur HDInsight et visualisé à l’aide de D3.js.</span><span class="sxs-lookup"><span data-stu-id="a7711-106">hello data is then stored into Apache HBase on HDInsight, and visualized using D3.js.</span></span>

<span data-ttu-id="a7711-107">modèle de gestionnaire de ressources Azure Hello utilisé dans ce document montre comment toocreate plusieurs ressources Azure dans un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="a7711-107">hello Azure Resource Manager template used in this document demonstrates how toocreate multiple Azure resources in a resource group.</span></span> <span data-ttu-id="a7711-108">modèle de Hello crée un réseau virtuel Azure, deux clusters HDInsight (Storm et HBase) et une application Web Azure.</span><span class="sxs-lookup"><span data-stu-id="a7711-108">hello template creates an Azure Virtual Network, two HDInsight clusters (Storm and HBase) and an Azure Web App.</span></span> <span data-ttu-id="a7711-109">Une implémentation de node.js d’un tableau de bord web en temps réel est toohello automatiquement déployé l’application web.</span><span class="sxs-lookup"><span data-stu-id="a7711-109">A node.js implementation of a real-time web dashboard is automatically deployed toohello web app.</span></span>

> [!NOTE]
> <span data-ttu-id="a7711-110">informations Hello dans ce document et l’exemple dans ce document nécessitent HDInsight version 3.6.</span><span class="sxs-lookup"><span data-stu-id="a7711-110">hello information in this document and example in this document require HDInsight version 3.6.</span></span>
>
> <span data-ttu-id="a7711-111">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="a7711-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="a7711-112">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="a7711-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a7711-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a7711-113">Prerequisites</span></span>

* <span data-ttu-id="a7711-114">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="a7711-114">An Azure subscription.</span></span>
* <span data-ttu-id="a7711-115">[Node.js](http://nodejs.org/): tableau de bord web de hello toopreview utilisés localement sur votre environnement de développement.</span><span class="sxs-lookup"><span data-stu-id="a7711-115">[Node.js](http://nodejs.org/): Used toopreview hello web dashboard locally on your development environment.</span></span>
* <span data-ttu-id="a7711-116">[Java et hello JDK 1.7](http://www.oracle.com/technetwork/java/javase/downloads/index.html): utilisé la topologie de Storm toodevelop hello.</span><span class="sxs-lookup"><span data-stu-id="a7711-116">[Java and hello JDK 1.7](http://www.oracle.com/technetwork/java/javase/downloads/index.html): Used toodevelop hello Storm topology.</span></span>
* <span data-ttu-id="a7711-117">[Maven](http://maven.apache.org/what-is-maven.html): projet de hello toobuild et compilation utilisé.</span><span class="sxs-lookup"><span data-stu-id="a7711-117">[Maven](http://maven.apache.org/what-is-maven.html): Used toobuild and compile hello project.</span></span>
* <span data-ttu-id="a7711-118">[GIT](http://git-scm.com/): projet de hello toodownload utilisé à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="a7711-118">[Git](http://git-scm.com/): Used toodownload hello project from GitHub.</span></span>
* <span data-ttu-id="a7711-119">Un **SSH** client : tooconnect toohello HDInsight de basés sur Linux clusters utilisés.</span><span class="sxs-lookup"><span data-stu-id="a7711-119">An **SSH** client: Used tooconnect toohello Linux-based HDInsight clusters.</span></span> <span data-ttu-id="a7711-120">Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="a7711-120">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>


> [!IMPORTANT]
> <span data-ttu-id="a7711-121">Vous n’avez pas besoin d’un cluster HDInsight existant.</span><span class="sxs-lookup"><span data-stu-id="a7711-121">You do not need an existing HDInsight cluster.</span></span> <span data-ttu-id="a7711-122">Dans ce document, les étapes de Hello créent hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="a7711-122">hello steps in this document create hello following resources:</span></span>
> 
> * <span data-ttu-id="a7711-123">un réseau virtuel Azure ;</span><span class="sxs-lookup"><span data-stu-id="a7711-123">An Azure Virtual Network</span></span>
> * <span data-ttu-id="a7711-124">un cluster Storm sur HDInsight (basé sur Linux, 2 nœuds Worker) ;</span><span class="sxs-lookup"><span data-stu-id="a7711-124">A Storm on HDInsight cluster (Linux-based, two worker nodes)</span></span>
> * <span data-ttu-id="a7711-125">un cluster HBase sur HDInsight (basé sur Linux, 2 nœuds Worker) ;</span><span class="sxs-lookup"><span data-stu-id="a7711-125">An HBase on HDInsight cluster (Linux-based, two worker nodes)</span></span>
> * <span data-ttu-id="a7711-126">Une application Web Azure qui héberge le tableau de bord web hello</span><span class="sxs-lookup"><span data-stu-id="a7711-126">An Azure Web App that hosts hello web dashboard</span></span>

## <a name="architecture"></a><span data-ttu-id="a7711-127">Architecture</span><span class="sxs-lookup"><span data-stu-id="a7711-127">Architecture</span></span>

![Diagramme d'architecture](./media/hdinsight-storm-sensor-data-analysis/devicesarchitecture.png)

<span data-ttu-id="a7711-129">Cet exemple se compose de hello suivant des composants :</span><span class="sxs-lookup"><span data-stu-id="a7711-129">This example consists of hello following components:</span></span>

* <span data-ttu-id="a7711-130">**Azure Event Hubs**: contient les données collectées à partir des capteurs.</span><span class="sxs-lookup"><span data-stu-id="a7711-130">**Azure Event Hubs**: Contains data that is collected from sensors.</span></span>
* <span data-ttu-id="a7711-131">**Storm sur HDInsight**: fournit le traitement en temps réel des données à partir d’Event Hub.</span><span class="sxs-lookup"><span data-stu-id="a7711-131">**Storm on HDInsight**: Provides real-time processing of data from Event Hub.</span></span>
* <span data-ttu-id="a7711-132">**HBase sur HDInsight**: fournit un magasin de données NoSQL persistant pour les données une fois celles-ci traitées par Storm.</span><span class="sxs-lookup"><span data-stu-id="a7711-132">**HBase on HDInsight**: Provides a persistent NoSQL data store for data after it has been processed by Storm.</span></span>
* <span data-ttu-id="a7711-133">**Service de réseau virtuel Azure**: permet de sécuriser les communications entre hello Storm sur HDInsight et HBase sur les clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a7711-133">**Azure Virtual Network service**: Enables secure communications between hello Storm on HDInsight and HBase on HDInsight clusters.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="a7711-134">Un réseau virtuel est requis lors de l’utilisation des API du client Java HBase hello.</span><span class="sxs-lookup"><span data-stu-id="a7711-134">A virtual network is required when using hello Java HBase client API.</span></span> <span data-ttu-id="a7711-135">Il n’est pas exposée via la passerelle de public hello pour les clusters HBase.</span><span class="sxs-lookup"><span data-stu-id="a7711-135">It is not exposed over hello public gateway for HBase clusters.</span></span> <span data-ttu-id="a7711-136">Clusters HBase lors de l’installation et Storm dans le même réseau virtuel permet de hello hello cluster Storm (ou un autre système sur le réseau virtuel de hello) toodirectly HBase à l’aide des API du client d’accès.</span><span class="sxs-lookup"><span data-stu-id="a7711-136">Installing HBase and Storm clusters into hello same virtual network allows hello Storm cluster (or any other system on hello virtual network) toodirectly access HBase using client API.</span></span>

* <span data-ttu-id="a7711-137">**Site web de tableau de bord**: un exemple de tableau de bord qui suit des données en temps réel.</span><span class="sxs-lookup"><span data-stu-id="a7711-137">**Dashboard website**: An example dashboard that charts data in real time.</span></span>
  
  * <span data-ttu-id="a7711-138">site Web de Hello est implémenté dans Node.js.</span><span class="sxs-lookup"><span data-stu-id="a7711-138">hello website is implemented in Node.js.</span></span>
  * <span data-ttu-id="a7711-139">[Socket.IO](http://socket.io/) est utilisé pour la communication en temps réel entre le topologie de Storm hello et hello.</span><span class="sxs-lookup"><span data-stu-id="a7711-139">[Socket.io](http://socket.io/) is used for real-time communication between hello Storm topology and hello website.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="a7711-140">L’utilisation de Socket.io pour la communication est un détail d’implémentation.</span><span class="sxs-lookup"><span data-stu-id="a7711-140">Using Socket.io for communication is an implementation detail.</span></span> <span data-ttu-id="a7711-141">Vous pouvez utiliser toute infrastructure de communications, telles que WebSockets brut ou SignalR.</span><span class="sxs-lookup"><span data-stu-id="a7711-141">You can use any communications framework, such as raw WebSockets or SignalR.</span></span>

  * <span data-ttu-id="a7711-142">[D3.js](http://d3js.org/) toograph utilisé hello donnée qui sont envoyées du site Web toohello.</span><span class="sxs-lookup"><span data-stu-id="a7711-142">[D3.js](http://d3js.org/) is used toograph hello data that is sent toohello website.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a7711-143">Deux clusters sont nécessaires, car il n’existe aucune méthode prise en charge toocreate un HDInsight cluster Storm et HBase.</span><span class="sxs-lookup"><span data-stu-id="a7711-143">Two clusters are required, as there is no supported method toocreate one HDInsight cluster for both Storm and HBase.</span></span>

<span data-ttu-id="a7711-144">Hello topologie lit les données à partir du concentrateur d’événements à l’aide de hello [org.apache.storm.eventhubs.spout.EventHubSpout](http://storm.apache.org/releases/0.10.1/javadocs/org/apache/storm/eventhubs/spout/class-use/EventHubSpout.html) classe et écrit des données dans HBase à l’aide de hello [org.apache.storm.hbase.bolt.HBaseBolt](https://storm.apache.org/releases/1.0.1/javadocs/org/apache/storm/hbase/bolt/HBaseBolt.html) classe.</span><span class="sxs-lookup"><span data-stu-id="a7711-144">hello topology reads data from Event Hub by using hello [org.apache.storm.eventhubs.spout.EventHubSpout](http://storm.apache.org/releases/0.10.1/javadocs/org/apache/storm/eventhubs/spout/class-use/EventHubSpout.html) class, and writes data into HBase using hello [org.apache.storm.hbase.bolt.HBaseBolt](https://storm.apache.org/releases/1.0.1/javadocs/org/apache/storm/hbase/bolt/HBaseBolt.html) class.</span></span> <span data-ttu-id="a7711-145">Communication avec le site Web de hello s’effectue à l’aide de [socket.io-client.java](https://github.com/nkzawa/socket.io-client.java).</span><span class="sxs-lookup"><span data-stu-id="a7711-145">Communication with hello website is accomplished by using [socket.io-client.java](https://github.com/nkzawa/socket.io-client.java).</span></span>

<span data-ttu-id="a7711-146">Hello suivant schéma explique disposition hello de topologie de hello :</span><span class="sxs-lookup"><span data-stu-id="a7711-146">hello following diagram explains hello layout of hello topology:</span></span>

![diagramme de topologie](./media/hdinsight-storm-sensor-data-analysis/sensoranalysis.png)

> [!NOTE]
> <span data-ttu-id="a7711-148">Ce diagramme est une vue simplifiée d’une topologie de hello.</span><span class="sxs-lookup"><span data-stu-id="a7711-148">This diagram is a simplified view of hello topology.</span></span> <span data-ttu-id="a7711-149">Une instance de chaque composant est créée pour chaque partition de votre hub d’événements.</span><span class="sxs-lookup"><span data-stu-id="a7711-149">An instance of each component is created for each partition in your Event Hub.</span></span> <span data-ttu-id="a7711-150">Ces instances sont répartis entre les nœuds de hello dans un cluster de hello et données sont routées entre eux, comme suit :</span><span class="sxs-lookup"><span data-stu-id="a7711-150">These instances are distributed across hello nodes in hello cluster, and data is routed between them as follows:</span></span>
> 
> * <span data-ttu-id="a7711-151">Les données à partir de l’Analyseur de toohello bec hello sont à charge équilibrée.</span><span class="sxs-lookup"><span data-stu-id="a7711-151">Data from hello spout toohello parser is load balanced.</span></span>
> * <span data-ttu-id="a7711-152">Données à partir de hello analyseur toohello du tableau de bord et HBase sont regroupées par ID de périphérique, afin que les messages à partir de hello même appareil toujours flux toohello même composant.</span><span class="sxs-lookup"><span data-stu-id="a7711-152">Data from hello parser toohello Dashboard and HBase is grouped by Device ID, so that messages from hello same device always flow toohello same component.</span></span>

### <a name="topology-components"></a><span data-ttu-id="a7711-153">Composants de la topologie</span><span class="sxs-lookup"><span data-stu-id="a7711-153">Topology components</span></span>

* <span data-ttu-id="a7711-154">**Bec de concentrateur d’événements**: bec de hello est fourni dans le cadre de la version d’Apache Storm 0.10.0 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="a7711-154">**Event Hub Spout**: hello spout is provided as part of Apache Storm version 0.10.0 and higher.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="a7711-155">bec de concentrateur d’événements Hello utilisé dans cet exemple requiert une tempête sur la version 3.5 ou 3.6 du cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a7711-155">hello Event Hub spout used in this example requires a Storm on HDInsight cluster version 3.5 or 3.6.</span></span>

* <span data-ttu-id="a7711-156">**ParserBolt.java**: données hello qui sont émises par bec de hello sont JSON brut, et parfois plus d’un événement est émis à la fois.</span><span class="sxs-lookup"><span data-stu-id="a7711-156">**ParserBolt.java**: hello data that is emitted by hello spout is raw JSON, and occasionally more than one event is emitted at a time.</span></span> <span data-ttu-id="a7711-157">Cet éclair lit données hello émises par hello bec et traite le message de salutation JSON.</span><span class="sxs-lookup"><span data-stu-id="a7711-157">This bolt reads hello data emitted by hello spout and parses hello JSON message.</span></span> <span data-ttu-id="a7711-158">éclair de Hello émet ensuite les données de salutation sous forme de tuple qui contient plusieurs champs.</span><span class="sxs-lookup"><span data-stu-id="a7711-158">hello bolt then emits hello data as a tuple that contains multiple fields.</span></span>
* <span data-ttu-id="a7711-159">**DashboardBolt.java**: ce composant illustre comment toouse hello bibliothèque cliente de Socket.io pour les données de toosend Java dans le tableau de bord en temps réel toohello web.</span><span class="sxs-lookup"><span data-stu-id="a7711-159">**DashboardBolt.java**: This component demonstrates how toouse hello Socket.io client library for Java toosend data in real time toohello web dashboard.</span></span>
* <span data-ttu-id="a7711-160">**non-hbase.yaml**: hello de définition de la topologie utilisée lors de l’exécution en mode local.</span><span class="sxs-lookup"><span data-stu-id="a7711-160">**no-hbase.yaml**: hello topology definition used when running in local mode.</span></span> <span data-ttu-id="a7711-161">Les composants de HBase ne sont pas utilisés.</span><span class="sxs-lookup"><span data-stu-id="a7711-161">It does not use HBase components.</span></span>
* <span data-ttu-id="a7711-162">**avec hbase.yaml**: hello de définition de la topologie utilisée lors de la topologie de hello en cours d’exécution sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="a7711-162">**with-hbase.yaml**: hello topology definition used when running hello topology on hello cluster.</span></span> <span data-ttu-id="a7711-163">Les composants de HBase sont utilisés.</span><span class="sxs-lookup"><span data-stu-id="a7711-163">It does use HBase components.</span></span>
* <span data-ttu-id="a7711-164">**dev.Properties**: hello pour bec de concentrateur d’événements hello HBase éclair et composants de tableau de bord, les informations de configuration.</span><span class="sxs-lookup"><span data-stu-id="a7711-164">**dev.properties**: hello configuration information for hello Event Hub spout, HBase bolt, and dashboard components.</span></span>

## <a name="prepare-your-environment"></a><span data-ttu-id="a7711-165">Préparation de votre environnement</span><span class="sxs-lookup"><span data-stu-id="a7711-165">Prepare your environment</span></span>

<span data-ttu-id="a7711-166">Avant d’utiliser cet exemple, vous devez créer un concentrateur d’événements Azure typologie Storm hello lit.</span><span class="sxs-lookup"><span data-stu-id="a7711-166">Before you use this example, you must create an Azure Event Hub, which hello Storm topology reads from.</span></span>

### <a name="configure-event-hub"></a><span data-ttu-id="a7711-167">Configuration du hub d'événements</span><span class="sxs-lookup"><span data-stu-id="a7711-167">Configure Event Hub</span></span>

<span data-ttu-id="a7711-168">Concentrateur d’événements est la source de données hello pour cet exemple.</span><span class="sxs-lookup"><span data-stu-id="a7711-168">Event Hub is hello data source for this example.</span></span> <span data-ttu-id="a7711-169">Utilisez hello suivant les étapes toocreate un concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="a7711-169">Use hello following steps toocreate an Event Hub.</span></span>

1. <span data-ttu-id="a7711-170">À partir de hello [portail Azure](https://portal.azure.com), sélectionnez **+ nouveau** -> **Internet of Things** -> **concentrateurs d’événements**.</span><span class="sxs-lookup"><span data-stu-id="a7711-170">From hello [Azure portal](https://portal.azure.com), select **+ New** -> **Internet of Things** -> **Event Hubs**.</span></span>
2. <span data-ttu-id="a7711-171">Bonjour **créer de Namespace** section, effectuer hello tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="a7711-171">In hello **Create Namespace** section, perform hello following tasks:</span></span>
   
   1. <span data-ttu-id="a7711-172">Entrez un **nom** pour l’espace de noms hello.</span><span class="sxs-lookup"><span data-stu-id="a7711-172">Enter a **Name** for hello namespace.</span></span>
   2. <span data-ttu-id="a7711-173">Sélectionnez un niveau tarifaire.</span><span class="sxs-lookup"><span data-stu-id="a7711-173">Select a pricing tier.</span></span> <span data-ttu-id="a7711-174">**De base** est suffisant pour cet exemple.</span><span class="sxs-lookup"><span data-stu-id="a7711-174">**Basic** is sufficient for this example.</span></span>
   3. <span data-ttu-id="a7711-175">Sélectionnez hello Azure **abonnement** toouse.</span><span class="sxs-lookup"><span data-stu-id="a7711-175">Select hello Azure **Subscription** toouse.</span></span>
   4. <span data-ttu-id="a7711-176">Sélectionnez un groupe de ressources existant ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="a7711-176">Either select an existing resource group or create a new one.</span></span>
   5. <span data-ttu-id="a7711-177">Sélectionnez hello **emplacement** pour hello concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="a7711-177">Select hello **Location** for hello Event Hub.</span></span>
   6. <span data-ttu-id="a7711-178">Sélectionnez **code confidentiel toodashboard**, puis cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="a7711-178">Select **Pin toodashboard**, and then click **Create**.</span></span>

3. <span data-ttu-id="a7711-179">Lors de la fin du processus de création de hello, hello informations concentrateurs d’événements pour votre espace de noms s’affiche.</span><span class="sxs-lookup"><span data-stu-id="a7711-179">When hello creation process completes, hello Event Hubs information for your namespace is displayed.</span></span> <span data-ttu-id="a7711-180">À partir d’ici, sélectionnez **+ Ajouter un hub d’événements**.</span><span class="sxs-lookup"><span data-stu-id="a7711-180">From here, select **+ Add Event Hub**.</span></span> <span data-ttu-id="a7711-181">Bonjour **concentrateur d’événements créer** section, entrez un nom de **sensordata**, puis sélectionnez **créer**.</span><span class="sxs-lookup"><span data-stu-id="a7711-181">In hello **Create Event Hub** section, enter a name of **sensordata**, and then select **Create**.</span></span> <span data-ttu-id="a7711-182">Laissez hello autres champs à des valeurs par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="a7711-182">Leave hello other fields at hello default values.</span></span>
4. <span data-ttu-id="a7711-183">À partir de concentrateurs d’événements hello consulter pour votre espace de noms, sélectionnez **concentrateurs d’événements**.</span><span class="sxs-lookup"><span data-stu-id="a7711-183">From hello Event Hubs view for your namespace, select **Event Hubs**.</span></span> <span data-ttu-id="a7711-184">Sélectionnez hello **sensordata** entrée.</span><span class="sxs-lookup"><span data-stu-id="a7711-184">Select hello **sensordata** entry.</span></span>
5. <span data-ttu-id="a7711-185">À partir de hello sensordata concentrateur d’événements, sélectionnez **les stratégies d’accès partagé**.</span><span class="sxs-lookup"><span data-stu-id="a7711-185">From hello sensordata Event Hub, select **Shared access policies**.</span></span> <span data-ttu-id="a7711-186">Hello d’utilisation **+ ajouter** hello tooadd de lien suivant des stratégies :</span><span class="sxs-lookup"><span data-stu-id="a7711-186">Use hello **+ Add** link tooadd hello following policies:</span></span>

    | <span data-ttu-id="a7711-187">Nom de la stratégie</span><span class="sxs-lookup"><span data-stu-id="a7711-187">Policy name</span></span> | <span data-ttu-id="a7711-188">Revendications</span><span class="sxs-lookup"><span data-stu-id="a7711-188">Claims</span></span> |
    | ----- | ----- |
    | <span data-ttu-id="a7711-189">périphériques</span><span class="sxs-lookup"><span data-stu-id="a7711-189">devices</span></span> | <span data-ttu-id="a7711-190">Envoyer</span><span class="sxs-lookup"><span data-stu-id="a7711-190">Send</span></span> |
    | <span data-ttu-id="a7711-191">storm</span><span class="sxs-lookup"><span data-stu-id="a7711-191">storm</span></span> | <span data-ttu-id="a7711-192">Écouter</span><span class="sxs-lookup"><span data-stu-id="a7711-192">Listen</span></span> |

1. <span data-ttu-id="a7711-193">Sélectionnez les deux stratégies et prenez note de hello **clé primaire** valeur.</span><span class="sxs-lookup"><span data-stu-id="a7711-193">Select both policies and make a note of hello **PRIMARY KEY** value.</span></span> <span data-ttu-id="a7711-194">Vous avez besoin de valeur de hello pour les deux stratégies dans les étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="a7711-194">You need hello value for both policies in future steps.</span></span>

## <a name="download-and-configure-hello-project"></a><span data-ttu-id="a7711-195">Télécharger et configurer le projet de hello</span><span class="sxs-lookup"><span data-stu-id="a7711-195">Download and configure hello project</span></span>

<span data-ttu-id="a7711-196">Utilisez hello suivant du projet de hello toodownload à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="a7711-196">Use hello following toodownload hello project from GitHub.</span></span>

    git clone https://github.com/Blackmist/hdinsight-eventhub-example

<span data-ttu-id="a7711-197">Après la commande hello, vous avez hello suivant la structure de répertoires :</span><span class="sxs-lookup"><span data-stu-id="a7711-197">After hello command completes, you have hello following directory structure:</span></span>

    hdinsight-eventhub-example/
        TemperatureMonitor/ - this contains hello topology
            resources/
                log4j2.xml - set logging toominimal.
                no-hbase.yaml - topology definition without hbase components.
                with-hbase.yaml - topology definition with hbase components.
            src/main/java/com/microsoft/examples/bolts/
                ParserBolt.java - parses JSON data into tuples
                DashboardBolt.java - sends data over Socket.IO toohello web dashboard.
        dashboard/nodejs/ - this is hello node.js web dashboard.
        SendEvents/ - utilities toosend fake sensor data.

> [!NOTE]
> <span data-ttu-id="a7711-198">Ce document ne passe pas dans les détails de toofull de code hello inclus dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="a7711-198">This document does not go in toofull details of hello code included in this example.</span></span> <span data-ttu-id="a7711-199">Toutefois, hello code entièrement contient des commentaires.</span><span class="sxs-lookup"><span data-stu-id="a7711-199">However, hello code is fully commented.</span></span>

<span data-ttu-id="a7711-200">tooconfigure hello projet tooread à partir du concentrateur d’événements, ouvrez hello `hdinsight-eventhub-example/TemperatureMonitor/dev.properties` et ajoutez votre toohello d’informations de concentrateur d’événements lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="a7711-200">tooconfigure hello project tooread from Event Hub, open hello `hdinsight-eventhub-example/TemperatureMonitor/dev.properties` file and add your Event Hub information toohello following lines:</span></span>

```bash
eventhub.read.policy.name: your_read_policy_name
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: your_event_hub_name
eventhub.partitions: 2
```

## <a name="compile-and-test-locally"></a><span data-ttu-id="a7711-201">Compilation et test local</span><span class="sxs-lookup"><span data-stu-id="a7711-201">Compile and test locally</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a7711-202">À l’aide de la topologie de hello localement nécessite un environnement de développement Storm en cours.</span><span class="sxs-lookup"><span data-stu-id="a7711-202">Using hello topology locally requires a working Storm development environment.</span></span> <span data-ttu-id="a7711-203">Pour plus d’informations, consultez la page [Configurer un environnement de développement Storm](http://storm.apache.org/releases/1.1.0/Setting-up-development-environment.html) à l’adresse Apache.org.</span><span class="sxs-lookup"><span data-stu-id="a7711-203">For more information, see [Setting up a Storm development environment](http://storm.apache.org/releases/1.1.0/Setting-up-development-environment.html) at Apache.org.</span></span>

> [!WARNING]
> <span data-ttu-id="a7711-204">Si vous utilisez un environnement de développement Windows, vous pouvez recevoir un `java.io.IOException` lors de l’exécution topologie de hello localement.</span><span class="sxs-lookup"><span data-stu-id="a7711-204">If you are using a Windows development environment, you may receive a `java.io.IOException` when running hello topology locally.</span></span> <span data-ttu-id="a7711-205">Dans ce cas, déplacez sur la topologie de hello toorunning sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a7711-205">If so, move on toorunning hello topology on HDInsight.</span></span>

<span data-ttu-id="a7711-206">Avant de tester, vous devez démarrer hello du tableau de bord tooview hello sortie de la topologie de hello et générer des données toostore dans le concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="a7711-206">Before testing, you must start hello dashboard tooview hello output of hello topology and generate data toostore in Event Hub.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a7711-207">composant de HBase Hello de cette topologie n’est pas actif lorsque vous testez localement.</span><span class="sxs-lookup"><span data-stu-id="a7711-207">hello HBase component of this topology is not active when testing locally.</span></span> <span data-ttu-id="a7711-208">Hello API Java pour un cluster HBase de hello ne sont pas accessibles à partir de l’extérieur hello réseau virtuel Azure qui contient des clusters de hello.</span><span class="sxs-lookup"><span data-stu-id="a7711-208">hello Java API for hello HBase cluster cannot be accessed from outside hello Azure Virtual Network that contains hello clusters.</span></span>

### <a name="start-hello-web-application"></a><span data-ttu-id="a7711-209">Démarrer l’application web de hello</span><span class="sxs-lookup"><span data-stu-id="a7711-209">Start hello web application</span></span>

1. <span data-ttu-id="a7711-210">Ouvrez une invite de commandes et modifiez les répertoires`hdinsight-eventhub-example/dashboard`.</span><span class="sxs-lookup"><span data-stu-id="a7711-210">Open a command prompt and change directories too`hdinsight-eventhub-example/dashboard`.</span></span> <span data-ttu-id="a7711-211">Utilisez hello suivant des dépendances de hello tooinstall de commande requis par hello web application :</span><span class="sxs-lookup"><span data-stu-id="a7711-211">Use hello following command tooinstall hello dependencies needed by hello web application:</span></span>
   
    ```bash
    npm install
    ```

2. <span data-ttu-id="a7711-212">Utilisez hello suite de l’application web de commande toostart hello :</span><span class="sxs-lookup"><span data-stu-id="a7711-212">Use hello following command toostart hello web application:</span></span>
   
    ```bash
    node server.js
    ```
   
    <span data-ttu-id="a7711-213">Vous voyez un toohello similaire message suit texte :</span><span class="sxs-lookup"><span data-stu-id="a7711-213">You see a message similar toohello following text:</span></span>
   
        Server listening at port 3000

3. <span data-ttu-id="a7711-214">Ouvrez un navigateur web et entrez `http://localhost:3000/` en tant qu’adresse de hello.</span><span class="sxs-lookup"><span data-stu-id="a7711-214">Open a web browser and enter `http://localhost:3000/` as hello address.</span></span> <span data-ttu-id="a7711-215">Un toohello similaire de page suivant l’image s’affiche :</span><span class="sxs-lookup"><span data-stu-id="a7711-215">A page similar toohello following image is displayed:</span></span>
   
    ![tableau de bord web](./media/hdinsight-storm-sensor-data-analysis/emptydashboard.png)
   
    <span data-ttu-id="a7711-217">Laissez l’invite de commandes ouverte.</span><span class="sxs-lookup"><span data-stu-id="a7711-217">Leave this command prompt open.</span></span> <span data-ttu-id="a7711-218">Après le test, utilisez le serveur web de Ctrl-C toostop hello.</span><span class="sxs-lookup"><span data-stu-id="a7711-218">After testing, use Ctrl-C toostop hello web server.</span></span>

### <a name="generate-data"></a><span data-ttu-id="a7711-219">Générer des données</span><span class="sxs-lookup"><span data-stu-id="a7711-219">Generate data</span></span>

> [!NOTE]
> <span data-ttu-id="a7711-220">Hello étapes de cette section utilisent Node.js afin qu’elles peuvent être utilisées sur n’importe quelle plateforme.</span><span class="sxs-lookup"><span data-stu-id="a7711-220">hello steps in this section use Node.js so that they can be used on any platform.</span></span> <span data-ttu-id="a7711-221">Pour obtenir des exemples de langage, consultez hello `SendEvents` active.</span><span class="sxs-lookup"><span data-stu-id="a7711-221">For other language examples, see hello `SendEvents` directory.</span></span>

1. <span data-ttu-id="a7711-222">Ouvrez une nouvelle invite, interpréteur de commandes ou Terminal Server et remplacez les répertoires`hdinsight-eventhub-example/SendEvents/nodejs`.</span><span class="sxs-lookup"><span data-stu-id="a7711-222">Open a new prompt, shell, or terminal, and change directories too`hdinsight-eventhub-example/SendEvents/nodejs`.</span></span> <span data-ttu-id="a7711-223">dépendances de hello tooinstall requis par l’application hello, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="a7711-223">tooinstall hello dependencies needed by hello application, use hello following command:</span></span>

    ```bash
    npm install
    ```

2. <span data-ttu-id="a7711-224">Ouvrez hello `app.js` dans un éditeur de texte et ajoutez hello informations du concentrateur d’événements obtenues précédemment :</span><span class="sxs-lookup"><span data-stu-id="a7711-224">Open hello `app.js` file in a text editor and add hello Event Hub information you obtained earlier:</span></span>
   
    ```javascript
    // ServiceBus Namespace
    var namespace = 'YourNamespace';
    // Event Hub Name
    var hubname ='sensordata';
    // Shared access Policy name and key (from Event Hub configuration)
    var my_key_name = 'devices';
    var my_key = 'YourKey';
    ```
   
   > [!NOTE]
   > <span data-ttu-id="a7711-225">Cet exemple suppose que vous avez utilisé `sensordata` comme nom hello de votre Hub d’événements.</span><span class="sxs-lookup"><span data-stu-id="a7711-225">This example assumes that you have used `sensordata` as hello name of your Event Hub.</span></span> <span data-ttu-id="a7711-226">Et que `devices` en tant que nom hello de stratégie hello qui a un `Send` de revendication.</span><span class="sxs-lookup"><span data-stu-id="a7711-226">And that `devices` as hello name of hello policy that has a `Send` claim.</span></span>

3. <span data-ttu-id="a7711-227">Utilisez hello suivant commande tooinsert nouvelles entrées dans le concentrateur d’événements :</span><span class="sxs-lookup"><span data-stu-id="a7711-227">Use hello following command tooinsert new entries in Event Hub:</span></span>
   
    ```bash
    node app.js
    ```
   
    <span data-ttu-id="a7711-228">Vous voyez plusieurs lignes de sortie qui contiennent des données hello envoyé tooEvent Hub :</span><span class="sxs-lookup"><span data-stu-id="a7711-228">You see several lines of output that contain hello data sent tooEvent Hub:</span></span>
   
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"0","Temperature":7}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"1","Temperature":39}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"2","Temperature":86}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"3","Temperature":29}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"4","Temperature":30}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"5","Temperature":5}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"6","Temperature":24}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"7","Temperature":40}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"8","Temperature":43}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"9","Temperature":84}

### <a name="build-and-start-hello-topology"></a><span data-ttu-id="a7711-229">Créez et démarrez la topologie de hello</span><span class="sxs-lookup"><span data-stu-id="a7711-229">Build and start hello topology</span></span>

1. <span data-ttu-id="a7711-230">Ouvrez une nouvelle invite de commandes et modifiez les répertoires`hdinsight-eventhub-example/TemperatureMonitor`.</span><span class="sxs-lookup"><span data-stu-id="a7711-230">Open a new command prompt and change directories too`hdinsight-eventhub-example/TemperatureMonitor`.</span></span> <span data-ttu-id="a7711-231">toobuild et package hello topologie, utiliser hello commande suivante :</span><span class="sxs-lookup"><span data-stu-id="a7711-231">toobuild and package hello topology, use hello following command:</span></span> 

    ```bash
    mvn clean package
    ```

2. <span data-ttu-id="a7711-232">toostart hello topologie en mode local, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="a7711-232">toostart hello topology in local mode, use hello following command:</span></span>

    ```bash
    storm jar target/TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local --filter dev.properties resources/no-hbase.yaml
    ```

    * <span data-ttu-id="a7711-233">`--local`topologie de hello démarre en mode local.</span><span class="sxs-lookup"><span data-stu-id="a7711-233">`--local` starts hello topology in local mode.</span></span>
    * <span data-ttu-id="a7711-234">`--filter`utilise hello `dev.properties` toopopulate paramètres du fichier de définition de la topologie hello.</span><span class="sxs-lookup"><span data-stu-id="a7711-234">`--filter` uses hello `dev.properties` file toopopulate parameters in hello topology definition.</span></span>
    * <span data-ttu-id="a7711-235">`resources/no-hbase.yaml`utilise hello `no-hbase.yaml` définition de la topologie.</span><span class="sxs-lookup"><span data-stu-id="a7711-235">`resources/no-hbase.yaml` uses hello `no-hbase.yaml` topology definition.</span></span>
 
   <span data-ttu-id="a7711-236">Une fois démarré, la topologie de hello lit les entrées à partir du concentrateur d’événements et les envoie toohello le tableau de bord en cours d’exécution sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="a7711-236">Once started, hello topology reads entries from Event Hub, and sends them toohello dashboard running on your local machine.</span></span> <span data-ttu-id="a7711-237">Vous devriez voir lignes dans hello web du tableau de bord, toohello similaire suivant l’image :</span><span class="sxs-lookup"><span data-stu-id="a7711-237">You should see lines appear in hello web dashboard, similar toohello following image:</span></span>
   
    ![tableau de bord avec données](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

2. <span data-ttu-id="a7711-239">Alors que le tableau de bord hello est en cours d’exécution, utilisez hello `node app.js` commande hello précédente étapes toosend nouvelles données tooEvent concentrateurs.</span><span class="sxs-lookup"><span data-stu-id="a7711-239">While hello dashboard is running, use hello `node app.js` command from hello previous steps toosend new data tooEvent Hubs.</span></span> <span data-ttu-id="a7711-240">Étant donné que les valeurs de température hello sont générés de façon aléatoire, graphique de hello doit mettre à jour des modifications importantes des tooshow de température.</span><span class="sxs-lookup"><span data-stu-id="a7711-240">Because hello temperature values are randomly generated, hello graph should update tooshow large changes in temperature.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a7711-241">Vous devez être en hello **hdinsight-eventhub-exemple/SendEvents/Nodejs** lorsque vous utilisez hello `node app.js` commande.</span><span class="sxs-lookup"><span data-stu-id="a7711-241">You must be in hello **hdinsight-eventhub-example/SendEvents/Nodejs** directory when using hello `node app.js` command.</span></span>

3. <span data-ttu-id="a7711-242">Après la vérification des mises à jour de ce tableau de bord hello, topologie de hello d’arrêt à l’aide de Ctrl + C.</span><span class="sxs-lookup"><span data-stu-id="a7711-242">After verifying that hello dashboard updates, stop hello topology using Ctrl+C.</span></span> <span data-ttu-id="a7711-243">Vous pouvez également utiliser le serveur web local de Ctrl + C toostop hello.</span><span class="sxs-lookup"><span data-stu-id="a7711-243">You can use Ctrl+C toostop hello local web server also.</span></span>

## <a name="create-a-storm-and-hbase-cluster"></a><span data-ttu-id="a7711-244">Créer un cluster Storm et HBase</span><span class="sxs-lookup"><span data-stu-id="a7711-244">Create a Storm and HBase cluster</span></span>

<span data-ttu-id="a7711-245">Hello les étapes de cette section utilisent un [modèle Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md) toocreate un cluster de réseau virtuel Azure et Storm et HBase sur le réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="a7711-245">hello steps in this section use an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md) toocreate an Azure Virtual Network and a Storm and HBase cluster on hello virtual network.</span></span> <span data-ttu-id="a7711-246">modèle de Hello crée une application Web Azure et déploie une copie du tableau de bord hello dans celui-ci.</span><span class="sxs-lookup"><span data-stu-id="a7711-246">hello template also creates an Azure Web App and deploys a copy of hello dashboard into it.</span></span>

> [!NOTE]
> <span data-ttu-id="a7711-247">Un réseau virtuel est utilisé afin que la topologie hello en cours d’exécution sur le cluster de Storm hello peut communiquer directement avec cluster de HBase hello à l’aide de hello HBase Java API.</span><span class="sxs-lookup"><span data-stu-id="a7711-247">A virtual network is used so that hello topology running on hello Storm cluster can directly communicate with hello HBase cluster using hello HBase Java API.</span></span>

<span data-ttu-id="a7711-248">modèle de gestionnaire de ressources Hello utilisé dans ce document se trouve dans un conteneur d’objets blob publics à **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-hbase-storm-cluster-in-vnet-3.6.json**.</span><span class="sxs-lookup"><span data-stu-id="a7711-248">hello Resource Manager template used in this document is located in a public blob container at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-hbase-storm-cluster-in-vnet-3.6.json**.</span></span>

1. <span data-ttu-id="a7711-249">Cliquez sur hello suivant toosign bouton dans tooAzure et modèle du Gestionnaire de ressources ouvrir hello Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a7711-249">Click hello following button toosign in tooAzure and open hello Resource Manager template in hello Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-hbase-storm-cluster-in-vnet-3.6.json" target="_blank"><img src="./media/hdinsight-storm-sensor-data-analysis/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. <span data-ttu-id="a7711-250">À partir de hello **les déploiement personnalisé** section, entrez hello valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="a7711-250">From hello **Custom deployment** section, enter hello following values:</span></span>
   
    ![Paramètres HDInsight](./media/hdinsight-storm-sensor-data-analysis/parameters.png)
   
   * <span data-ttu-id="a7711-252">**Nom du Cluster de base**: cette valeur est utilisée comme nom de base hello pour les clusters de Storm et HBase hello.</span><span class="sxs-lookup"><span data-stu-id="a7711-252">**Base Cluster Name**: This value is used as hello base name for hello Storm and HBase clusters.</span></span> <span data-ttu-id="a7711-253">Par exemple, si vous entrez **abc**, cela crée un cluster Storm nommé **storm-abc** et un cluster HBase nommé **hbase-abc**.</span><span class="sxs-lookup"><span data-stu-id="a7711-253">For example, entering **abc** creates a Storm cluster named **storm-abc** and an HBase cluster named **hbase-abc**.</span></span>
   * <span data-ttu-id="a7711-254">**Nom d’utilisateur de cluster**: nom d’utilisateur admin hello pour les clusters de Storm et HBase hello.</span><span class="sxs-lookup"><span data-stu-id="a7711-254">**Cluster Login User Name**: hello admin user name for hello Storm and HBase clusters.</span></span>
   * <span data-ttu-id="a7711-255">**Mot de passe de connexion cluster**: hello mot de passe administrateur pour les clusters de Storm et HBase hello.</span><span class="sxs-lookup"><span data-stu-id="a7711-255">**Cluster Login Password**: hello admin user password for hello Storm and HBase clusters.</span></span>
   * <span data-ttu-id="a7711-256">**Nom d’utilisateur SSH**: hello toocreate d’utilisateur SSH pour les clusters de Storm et HBase hello.</span><span class="sxs-lookup"><span data-stu-id="a7711-256">**SSH User Name**: hello SSH user toocreate for hello Storm and HBase clusters.</span></span>
   * <span data-ttu-id="a7711-257">**Mot de passe SSH**: mot de passe de hello pour hello SSH pour les clusters de Storm et HBase hello.</span><span class="sxs-lookup"><span data-stu-id="a7711-257">**SSH Password**: hello password for hello SSH user for hello Storm and HBase clusters.</span></span>
   * <span data-ttu-id="a7711-258">**Emplacement**: région hello créés dans les clusters hello.</span><span class="sxs-lookup"><span data-stu-id="a7711-258">**Location**: hello region that hello clusters are created in.</span></span>
     
     <span data-ttu-id="a7711-259">Cliquez sur **OK** toosave les paramètres hello.</span><span class="sxs-lookup"><span data-stu-id="a7711-259">Click **OK** toosave hello parameters.</span></span>

3. <span data-ttu-id="a7711-260">Hello d’utilisation **notions de base** section toocreate un groupe de ressources ou sélectionnez-en un existant.</span><span class="sxs-lookup"><span data-stu-id="a7711-260">Use hello **Basics** section toocreate a resource group or select an existing one.</span></span>
4. <span data-ttu-id="a7711-261">Bonjour **emplacement du groupe de ressources** menu déroulant, sélectionnez hello même emplacement que vous avez sélectionné pour hello **emplacement** paramètre Bonjour **paramètres** section.</span><span class="sxs-lookup"><span data-stu-id="a7711-261">In hello **Resource group location** dropdown menu, select hello same location as you selected for hello **Location** parameter in hello **Settings** section.</span></span>
5. <span data-ttu-id="a7711-262">Lire les conditions générales hello et sélectionnez **J’accepte les termes du contrat de toohello et conditions susmentionnées**.</span><span class="sxs-lookup"><span data-stu-id="a7711-262">Read hello terms and conditions, and then select **I agree toohello terms and conditions stated above**.</span></span>
6. <span data-ttu-id="a7711-263">Enfin, recherchez **code confidentiel toodashboard** , puis sélectionnez **bon**.</span><span class="sxs-lookup"><span data-stu-id="a7711-263">Finally, check **Pin toodashboard** and then select **Purchase**.</span></span> <span data-ttu-id="a7711-264">Il prend environ 20 minutes toocreate les clusters hello.</span><span class="sxs-lookup"><span data-stu-id="a7711-264">It takes about 20 minutes toocreate hello clusters.</span></span>

<span data-ttu-id="a7711-265">Une fois que les ressources hello ont été créées, plus d’informations sur le groupe de ressources hello s’affiche.</span><span class="sxs-lookup"><span data-stu-id="a7711-265">Once hello resources have been created, information about hello resource group is displayed.</span></span>

![Groupe de ressources de réseau virtuel de hello et des clusters](./media/hdinsight-storm-sensor-data-analysis/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="a7711-267">Notez que les noms de hello des clusters HDInsight de hello sont **storm-BASENAME** et **hbase-BASENAME**, où BASENAME est nom hello toohello modèle fourni.</span><span class="sxs-lookup"><span data-stu-id="a7711-267">Notice that hello names of hello HDInsight clusters are **storm-BASENAME** and **hbase-BASENAME**, where BASENAME is hello name you provided toohello template.</span></span> <span data-ttu-id="a7711-268">Vous utilisez ces noms dans une étape ultérieure lors de la connexion toohello clusters.</span><span class="sxs-lookup"><span data-stu-id="a7711-268">You use these names in a later step when connecting toohello clusters.</span></span> <span data-ttu-id="a7711-269">Également, notez que hello nom du site de tableau de bord hello est **basename-tableau de bord**.</span><span class="sxs-lookup"><span data-stu-id="a7711-269">Also note that hello name of hello dashboard site is **basename-dashboard**.</span></span> <span data-ttu-id="a7711-270">Cette valeur sera utilisée ultérieurement dans ce document.</span><span class="sxs-lookup"><span data-stu-id="a7711-270">This value is used later in this document.</span></span>

## <a name="configure-hello-dashboard-bolt"></a><span data-ttu-id="a7711-271">Configurer éclair du tableau de bord hello</span><span class="sxs-lookup"><span data-stu-id="a7711-271">Configure hello Dashboard bolt</span></span>

<span data-ttu-id="a7711-272">toosend données toohello tableau de bord déployé comme une application web, vous devez modifier hello ligne Bonjour `dev.properties`fichier :</span><span class="sxs-lookup"><span data-stu-id="a7711-272">toosend data toohello dashboard deployed as a web app, you must modify hello following line in hello `dev.properties`file:</span></span>

```yaml
dashboard.uri: http://localhost:3000
```

<span data-ttu-id="a7711-273">Modification `http://localhost:3000` trop`http://BASENAME-dashboard.azurewebsites.net` et enregistrez le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="a7711-273">Change `http://localhost:3000` too`http://BASENAME-dashboard.azurewebsites.net` and save hello file.</span></span> <span data-ttu-id="a7711-274">Remplacez **BASENAME** par nom de base hello entré à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="a7711-274">Replace **BASENAME** with hello base name you provided in hello previous step.</span></span> <span data-ttu-id="a7711-275">Vous pouvez également utiliser le groupe de ressources hello créé précédemment URL hello tooselect hello du tableau de bord et de la vue.</span><span class="sxs-lookup"><span data-stu-id="a7711-275">You can also use hello resource group created previously tooselect hello dashboard and view hello URL.</span></span>

## <a name="create-hello-hbase-table"></a><span data-ttu-id="a7711-276">Créer la table HBase à hello</span><span class="sxs-lookup"><span data-stu-id="a7711-276">Create hello HBase table</span></span>

<span data-ttu-id="a7711-277">toostore des données dans HBase, nous devons d’abord créer une table.</span><span class="sxs-lookup"><span data-stu-id="a7711-277">toostore data in HBase, we must first create a table.</span></span> <span data-ttu-id="a7711-278">Ressources nécessitant une tempête toowrite à créer au préalable, car des ressources toocreate lors de la tentative d’à l’intérieur d’une topologie Storm peuvent entraîner plusieurs instances de la tentative de toocreate hello même ressource.</span><span class="sxs-lookup"><span data-stu-id="a7711-278">Pre-create resources that Storm needs toowrite to, as trying toocreate resources from inside a Storm topology can result in multiple instances trying toocreate hello same resource.</span></span> <span data-ttu-id="a7711-279">Créer des ressources de hello en dehors de la topologie de hello et utiliser Storm pour lecture/écriture et analytique.</span><span class="sxs-lookup"><span data-stu-id="a7711-279">Create hello resources outside hello topology and use Storm for reading/writing and analytics.</span></span>

1. <span data-ttu-id="a7711-280">Utiliser SSH tooconnect toohello HBase cluster à l’aide de SSH hello et mot de passe fourni toohello modèle lors de la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="a7711-280">Use SSH tooconnect toohello HBase cluster using hello SSH user and password you supplied toohello template during cluster creation.</span></span> <span data-ttu-id="a7711-281">Par exemple, si la connexion à l’aide de hello `ssh` vous utiliseriez hello selon la syntaxe de la commande :</span><span class="sxs-lookup"><span data-stu-id="a7711-281">For example, if connecting using hello `ssh` command, you would use hello following syntax:</span></span>
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```
   
    <span data-ttu-id="a7711-282">Remplacez `sshuser` avec le nom d’utilisateur SSH hello que vous avez fourni lors de la création du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="a7711-282">Replace `sshuser` with hello SSH user name you provided when creating hello cluster.</span></span> <span data-ttu-id="a7711-283">Remplacez `clustername` avec le nom du cluster HBase hello.</span><span class="sxs-lookup"><span data-stu-id="a7711-283">Replace `clustername` with hello HBase cluster name.</span></span>

2. <span data-ttu-id="a7711-284">À partir de la session SSH de hello, démarrez le shell HBase de hello.</span><span class="sxs-lookup"><span data-stu-id="a7711-284">From hello SSH session, start hello HBase shell.</span></span>
   
    ```bash
    hbase shell
    ```
   
    <span data-ttu-id="a7711-285">Une fois que l’interpréteur de commandes hello a chargé, vous voyez un `hbase(main):001:0>` invite.</span><span class="sxs-lookup"><span data-stu-id="a7711-285">Once hello shell has loaded, you see an `hbase(main):001:0>` prompt.</span></span>

3. <span data-ttu-id="a7711-286">À partir de hello shell HBase, entrez hello suivant commande toocreate données capteur table toostore hello :</span><span class="sxs-lookup"><span data-stu-id="a7711-286">From hello HBase shell, enter hello following command toocreate a table toostore hello sensor data:</span></span>
   
    ```hbase
    create 'SensorData', 'cf'
    ```

4. <span data-ttu-id="a7711-287">Vérifiez que la table hello a été créée à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="a7711-287">Verify that hello table has been created by using hello following command:</span></span>
   
    ```hbase
    scan 'SensorData'
    ```
   
    <span data-ttu-id="a7711-288">Cela retourne les informations toohello semblable l’exemple suivant, qui indique qu’il n’y a 0 ligne dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="a7711-288">This returns information similar toohello following example, indicating that there are 0 rows in hello table.</span></span>
   
        ROW                   COLUMN+CELL                                       0 row(s) in 0.1900 seconds

5. <span data-ttu-id="a7711-289">Entrez `exit` tooexit hello shell HBase :</span><span class="sxs-lookup"><span data-stu-id="a7711-289">Enter `exit` tooexit hello HBase shell:</span></span>

## <a name="configure-hello-hbase-bolt"></a><span data-ttu-id="a7711-290">Configurer éclair de HBase hello</span><span class="sxs-lookup"><span data-stu-id="a7711-290">Configure hello HBase bolt</span></span>

<span data-ttu-id="a7711-291">tooHBase toowrite à partir du cluster de Storm hello, vous devez fournir éclair de HBase hello avec les détails de la configuration de votre cluster HBase hello.</span><span class="sxs-lookup"><span data-stu-id="a7711-291">toowrite tooHBase from hello Storm cluster, you must provide hello HBase bolt with hello configuration details of your HBase cluster.</span></span>

1. <span data-ttu-id="a7711-292">Utilisez une des hello suivant le quorum de soigneur exemples tooretrieve hello pour votre cluster HBase :</span><span class="sxs-lookup"><span data-stu-id="a7711-292">Use one of hello following examples tooretrieve hello Zookeeper quorum for your HBase cluster:</span></span>

    ```bash
    CLUSTERNAME='your_HDInsight_cluster_name'
    curl -u admin -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/HBASE/components/HBASE_MASTER" | jq '.metrics.hbase.master.ZookeeperQuorum'
    ```

    > [!NOTE]
    > <span data-ttu-id="a7711-293">Remplacez `your_HDInsight_cluster_name` par nom de hello de votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a7711-293">Replace `your_HDInsight_cluster_name` with hello name of your HDInsight cluster.</span></span> <span data-ttu-id="a7711-294">Pour plus d’informations sur l’installation de hello `jq` utilitaire, consultez [https://stedolan.github.io/jq/](https://stedolan.github.io/jq/).</span><span class="sxs-lookup"><span data-stu-id="a7711-294">For more information on installing hello `jq` utility, see [https://stedolan.github.io/jq/](https://stedolan.github.io/jq/).</span></span>
    >
    > <span data-ttu-id="a7711-295">Lorsque vous y êtes invité, entrez le mot de passe de hello pour la connexion d’administration hello HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a7711-295">When prompted, enter hello password for hello HDInsight admin login.</span></span>

    ```powershell
    $clusterName = 'your_HDInsight_cluster_name`
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HBASE/components/HBASE_MASTER" -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.metrics.hbase.master.ZookeeperQuorum
    ```

    > [!NOTE]
    > <span data-ttu-id="a7711-296">Remplacez ' your_HDInsight_cluster_name avec nom hello de votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a7711-296">Replace \`your_HDInsight_cluster_name with hello name of your HDInsight cluster.</span></span> <span data-ttu-id="a7711-297">Lorsque vous y êtes invité, entrez le mot de passe de hello pour la connexion d’administration hello HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a7711-297">When prompted, enter hello password for hello HDInsight admin login.</span></span>
    >
    > <span data-ttu-id="a7711-298">Cet exemple nécessite Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a7711-298">This example requires Azure PowerShell.</span></span> <span data-ttu-id="a7711-299">Pour plus d’informations sur l’utilisation d’Azure PowerShell, voir [Prise en main d’Azure PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/Getting-Started-with-Windows-PowerShell?view=powershell-6)</span><span class="sxs-lookup"><span data-stu-id="a7711-299">For more information on using Azure PowerShell, see [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/Getting-Started-with-Windows-PowerShell?view=powershell-6)</span></span>

    <span data-ttu-id="a7711-300">les informations de Hello retournées par ces exemples sont similaires toohello suivant du texte :</span><span class="sxs-lookup"><span data-stu-id="a7711-300">hello information returned by these examples is similar toohello following text:</span></span>

    `zk2-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk0-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk3-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181`

    <span data-ttu-id="a7711-301">Ces informations sont utilisées par toocommunicate Storm avec un cluster HBase de hello.</span><span class="sxs-lookup"><span data-stu-id="a7711-301">This information is used by Storm toocommunicate with hello HBase cluster.</span></span>

2. <span data-ttu-id="a7711-302">Modifier hello `dev.properties` et ajoutez hello soigneur quorum informations toohello ligne suivante :</span><span class="sxs-lookup"><span data-stu-id="a7711-302">Modify hello `dev.properties` file and add hello Zookeeper quorum information toohello following line:</span></span>

    ```yaml
    hbase.zookeeper.quorum: your_hbase_quorum
    ```

## <a name="build-package-and-deploy-hello-solution-toohdinsight"></a><span data-ttu-id="a7711-303">Générez, empaquetez et déployez hello solution tooHDInsight</span><span class="sxs-lookup"><span data-stu-id="a7711-303">Build, package, and deploy hello solution tooHDInsight</span></span>

<span data-ttu-id="a7711-304">Dans votre environnement de développement, utilisez hello suivant cluster storm toohello de la topologie étapes toodeploy hello Storm.</span><span class="sxs-lookup"><span data-stu-id="a7711-304">In your development environment, use hello following steps toodeploy hello Storm topology toohello storm cluster.</span></span>

1. <span data-ttu-id="a7711-305">À partir de hello `TemperatureMonitor` répertoire, suivante de hello utilisez commande tooperform une nouvelle build et créer un package du fichier JAR à partir de votre projet :</span><span class="sxs-lookup"><span data-stu-id="a7711-305">From hello `TemperatureMonitor` directory, use hello following command tooperform a new build and create a JAR package from your project:</span></span>
   
        mvn clean package
   
    <span data-ttu-id="a7711-306">Cette commande crée un fichier nommé `TemperatureMonitor-1.0-SNAPSHOT.jar in hello `répertoire cible de votre projet.</span><span class="sxs-lookup"><span data-stu-id="a7711-306">This command creates a file named `TemperatureMonitor-1.0-SNAPSHOT.jar in hello `target\` directory of your project.</span></span>

2. <span data-ttu-id="a7711-307">Hello d’utilisation scp tooupload `TemperatureMonitor-1.0-SNAPSHOT.jar` et `dev.properties` cluster de fichiers tooyour Storm.</span><span class="sxs-lookup"><span data-stu-id="a7711-307">Use scp tooupload hello `TemperatureMonitor-1.0-SNAPSHOT.jar` and `dev.properties` files tooyour Storm cluster.</span></span> <span data-ttu-id="a7711-308">Bonjour à l’exemple, remplacez `sshuser` avec vous fournies lors de la création du cluster de hello, par l’utilisateur SSH hello et `clustername` avec nom hello de votre cluster Storm.</span><span class="sxs-lookup"><span data-stu-id="a7711-308">In hello following example, replace `sshuser` with hello SSH user you provided when creating hello cluster, and `clustername` with hello name of your Storm cluster.</span></span> <span data-ttu-id="a7711-309">Lorsque vous y êtes invité, entrez le mot de passe de hello pour l’utilisateur SSH hello.</span><span class="sxs-lookup"><span data-stu-id="a7711-309">When prompted, enter hello password for hello SSH user.</span></span>
   
    ```bash
    scp target/TemperatureMonitor-1.0-SNAPSHOT.jar dev.properties sshuser@clustername-ssh.azurehdinsight.net:
    ```

   > [!NOTE]
   > <span data-ttu-id="a7711-310">Il peut prendre plusieurs minutes les fichiers tooupload hello.</span><span class="sxs-lookup"><span data-stu-id="a7711-310">It may take several minutes tooupload hello files.</span></span>

    <span data-ttu-id="a7711-311">Pour plus d’informations sur l’utilisation de hello `scp` et `ssh` commandes hdinsight, consultez [utilisation de SSH avec HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="a7711-311">For more information on using hello `scp` and `ssh` commands with HDInsight, see [Use SSH with HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

3. <span data-ttu-id="a7711-312">Une fois que le fichier de hello a été téléchargé, connectez le cluster de tempête de toohello à l’aide de SSH.</span><span class="sxs-lookup"><span data-stu-id="a7711-312">Once hello file has been uploaded, connect toohello Storm cluster using SSH.</span></span>
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="a7711-313">Remplacez `sshuser` avec le nom d’utilisateur SSH hello.</span><span class="sxs-lookup"><span data-stu-id="a7711-313">Replace `sshuser` with hello SSH user name.</span></span> <span data-ttu-id="a7711-314">Remplacez `clustername` avec le nom du cluster Storm hello.</span><span class="sxs-lookup"><span data-stu-id="a7711-314">Replace `clustername` with hello Storm cluster name.</span></span>

4. <span data-ttu-id="a7711-315">toostart hello topologie, utiliser hello commande à partir de la session SSH hello suivante :</span><span class="sxs-lookup"><span data-stu-id="a7711-315">toostart hello topology, use hello following command from hello SSH session:</span></span>
   
    ```bash
    storm jar TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote --filter dev.properties -R /with-hbase.yaml
    ```

    * <span data-ttu-id="a7711-316">`--remote`soumet hello topologie toohello service Nimbus, qui distribue les nœuds de superviseur toohello dans un cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="a7711-316">`--remote` submits hello topology toohello Nimbus service, which distributes it toohello supervisor nodes in hello cluster.</span></span>
    * <span data-ttu-id="a7711-317">`--filter`utilise hello `dev.properties` toopopulate paramètres du fichier de définition de la topologie hello.</span><span class="sxs-lookup"><span data-stu-id="a7711-317">`--filter` uses hello `dev.properties` file toopopulate parameters in hello topology definition.</span></span>
    * <span data-ttu-id="a7711-318">`-R /with-hbase.yaml`utilise hello `with-hbase.yaml` topologie inclus dans le package de hello.</span><span class="sxs-lookup"><span data-stu-id="a7711-318">`-R /with-hbase.yaml` uses hello `with-hbase.yaml` topology included in hello package.</span></span>

5. <span data-ttu-id="a7711-319">Une fois que la topologie de hello a démarré, ouvrez un site Web toohello de navigateur vous avez publié sur Azure, puis utilisez hello `node app.js` commande toosend tooEvent de données concentrateur.</span><span class="sxs-lookup"><span data-stu-id="a7711-319">After hello topology has started, open a browser toohello website you published on Azure, then use hello `node app.js` command toosend data tooEvent Hub.</span></span> <span data-ttu-id="a7711-320">Vous devez voir les informations de hello du tableau de bord mise à jour toodisplay hello web.</span><span class="sxs-lookup"><span data-stu-id="a7711-320">You should see hello web dashboard update toodisplay hello information.</span></span>
   
    ![dashboard](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

## <a name="view-hbase-data"></a><span data-ttu-id="a7711-322">Afficher les données HBase</span><span class="sxs-lookup"><span data-stu-id="a7711-322">View HBase data</span></span>

<span data-ttu-id="a7711-323">Utilisez hello suivant les étapes tooconnect tooHBase et vérifiez que les données de hello ont été écrites toohello table :</span><span class="sxs-lookup"><span data-stu-id="a7711-323">Use hello following steps tooconnect tooHBase and verify that hello data has been written toohello table:</span></span>

1. <span data-ttu-id="a7711-324">Utiliser SSH tooconnect toohello HBase cluster.</span><span class="sxs-lookup"><span data-stu-id="a7711-324">Use SSH tooconnect toohello HBase cluster.</span></span>
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="a7711-325">Remplacez `sshuser` avec le nom d’utilisateur SSH hello.</span><span class="sxs-lookup"><span data-stu-id="a7711-325">Replace `sshuser` with hello SSH user name.</span></span> <span data-ttu-id="a7711-326">Remplacez `clustername` avec le nom du cluster HBase hello.</span><span class="sxs-lookup"><span data-stu-id="a7711-326">Replace `clustername` with hello HBase cluster name.</span></span>

2. <span data-ttu-id="a7711-327">À partir de la session SSH de hello, démarrez le shell HBase de hello.</span><span class="sxs-lookup"><span data-stu-id="a7711-327">From hello SSH session, start hello HBase shell.</span></span>
   
    ```bash
    hbase shell
    ```
   
    <span data-ttu-id="a7711-328">Une fois que l’interpréteur de commandes hello a chargé, vous voyez un `hbase(main):001:0>` invite.</span><span class="sxs-lookup"><span data-stu-id="a7711-328">Once hello shell has loaded, you see an `hbase(main):001:0>` prompt.</span></span>

3. <span data-ttu-id="a7711-329">Afficher les lignes de table de hello :</span><span class="sxs-lookup"><span data-stu-id="a7711-329">View rows from hello table:</span></span>
   
    ```hbase
    scan 'SensorData'
    ```
   
    <span data-ttu-id="a7711-330">Cette commande retourne toohello similaires en informations suivant le texte, indiquant qu’il existe des données dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="a7711-330">This command returns information similar toohello following text, indicating that there is data in hello table.</span></span>
   
        hbase(main):002:0> scan 'SensorData'
        ROW                             COLUMN+CELL
        \x00\x00\x00\x00               column=cf:temperature, timestamp=1467290788277, value=\x00\x00\x00\x04
        \x00\x00\x00\x00               column=cf:timestamp, timestamp=1467290788277, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x01               column=cf:temperature, timestamp=1467290788348, value=\x00\x00\x00M
        \x00\x00\x00\x01               column=cf:timestamp, timestamp=1467290788348, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x02               column=cf:temperature, timestamp=1467290788268, value=\x00\x00\x00R
        \x00\x00\x00\x02               column=cf:timestamp, timestamp=1467290788268, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x03               column=cf:temperature, timestamp=1467290788269, value=\x00\x00\x00#
        \x00\x00\x00\x03               column=cf:timestamp, timestamp=1467290788269, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x04               column=cf:temperature, timestamp=1467290788356, value=\x00\x00\x00>
        \x00\x00\x00\x04               column=cf:timestamp, timestamp=1467290788356, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x05               column=cf:temperature, timestamp=1467290788326, value=\x00\x00\x00\x0D
        \x00\x00\x00\x05               column=cf:timestamp, timestamp=1467290788326, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x06               column=cf:temperature, timestamp=1467290788253, value=\x00\x00\x009
        \x00\x00\x00\x06               column=cf:timestamp, timestamp=1467290788253, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x07               column=cf:temperature, timestamp=1467290788229, value=\x00\x00\x00\x12
        \x00\x00\x00\x07               column=cf:timestamp, timestamp=1467290788229, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x08               column=cf:temperature, timestamp=1467290788336, value=\x00\x00\x00\x16
        \x00\x00\x00\x08               column=cf:timestamp, timestamp=1467290788336, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x09               column=cf:temperature, timestamp=1467290788246, value=\x00\x00\x001
        \x00\x00\x00\x09               column=cf:timestamp, timestamp=1467290788246, value=2015-02-10T14:43.05.00320Z
        10 row(s) in 0.1800 seconds
   
   > [!NOTE]
   > <span data-ttu-id="a7711-331">Cette opération retourne un maximum de 10 lignes à partir de la table de hello.</span><span class="sxs-lookup"><span data-stu-id="a7711-331">This scan operation returns a maximum of 10 rows from hello table.</span></span>

## <a name="delete-your-clusters"></a><span data-ttu-id="a7711-332">Supprimer vos clusters</span><span class="sxs-lookup"><span data-stu-id="a7711-332">Delete your clusters</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="a7711-333">clusters de hello toodelete, de stockage et de l’application web à la fois, supprimer groupe de ressources hello qui les contient.</span><span class="sxs-lookup"><span data-stu-id="a7711-333">toodelete hello clusters, storage, and web app at one time, delete hello resource group that contains them.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a7711-334">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a7711-334">Next steps</span></span>

<span data-ttu-id="a7711-335">Pour plus d’exemples de topologies Storm avec HDInsight, consultez les [exemples de topologies pour Storm sur HDInsight](hdinsight-storm-example-topology.md)</span><span class="sxs-lookup"><span data-stu-id="a7711-335">For more examples of Storm topologies with HDInsight, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md)</span></span>

<span data-ttu-id="a7711-336">Pour plus d’informations sur Apache Storm, consultez hello [Apache Storm](https://storm.incubator.apache.org/) site.</span><span class="sxs-lookup"><span data-stu-id="a7711-336">For more information about Apache Storm, see hello [Apache Storm](https://storm.incubator.apache.org/) site.</span></span>

<span data-ttu-id="a7711-337">Pour plus d’informations sur HBase sur HDInsight, consultez hello [HBase HDInsight aperçu](hdinsight-hbase-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a7711-337">For more information about HBase on HDInsight, see hello [HBase with HDInsight Overview](hdinsight-hbase-overview.md).</span></span>

<span data-ttu-id="a7711-338">Pour plus d’informations sur Socket.io, consultez hello [socket.io](http://socket.io/) site.</span><span class="sxs-lookup"><span data-stu-id="a7711-338">For more information about Socket.io, see hello [socket.io](http://socket.io/) site.</span></span>

<span data-ttu-id="a7711-339">Pour plus d'informations sur D3.js, consultez la page [D3.js : documents pilotés par les données](http://d3js.org/).</span><span class="sxs-lookup"><span data-stu-id="a7711-339">For more information about D3.js, see [D3.js - Data Driven Documents](http://d3js.org/).</span></span>

<span data-ttu-id="a7711-340">Pour plus d'informations sur la création de topologies en Java, consultez [Développement de topologies Java pour Apache Storm sur HDInsight](hdinsight-storm-develop-java-topology.md).</span><span class="sxs-lookup"><span data-stu-id="a7711-340">For information about creating topologies in Java, see [Develop Java topologies for Apache Storm on HDInsight](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="a7711-341">Pour plus d'informations sur la création de topologies en .NET, consultez [Développement de topologies C# pour Apache Storm sur HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="a7711-341">For information about creating topologies in .NET, see [Develop C# topologies for Apache Storm on HDInsight using Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

[azure-portal]: https://portal.azure.com
