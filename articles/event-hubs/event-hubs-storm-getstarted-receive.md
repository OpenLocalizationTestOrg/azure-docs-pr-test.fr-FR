---
title: "les événements de concentrateurs d’événements Azure à l’aide d’Apache Storm aaaReceive | Documents Microsoft"
description: "Prise en main de la réception d’événements des Event Hubs avec Apache Storm"
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: java
ms.devlang: multiple
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: a0ab860ee8d504a28aac380c504c928f0d6dbc1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="receive-events-from-event-hubs-using-apache-storm"></a><span data-ttu-id="bd9e3-103">Recevoir des événements d’Event Hubs avec Apache Storm</span><span class="sxs-lookup"><span data-stu-id="bd9e3-103">Receive events from Event Hubs using Apache Storm</span></span>

<span data-ttu-id="bd9e3-104">[Apache Storm](https://storm.incubator.apache.org) est un système de calcul distribué en temps réel qui simplifie de façon fiable le traitement de vastes flux de données.</span><span class="sxs-lookup"><span data-stu-id="bd9e3-104">[Apache Storm](https://storm.incubator.apache.org) is a distributed real-time computation system that simplifies reliable processing of unbounded streams of data.</span></span> <span data-ttu-id="bd9e3-105">Cette section montre comment toouse vagues de concentrateurs d’événements Azure bec tooreceive les événements de concentrateurs d’événements.</span><span class="sxs-lookup"><span data-stu-id="bd9e3-105">This section shows how toouse an Azure Event Hubs Storm spout tooreceive events from Event Hubs.</span></span> <span data-ttu-id="bd9e3-106">À l'aide d'Apache Storm, vous pouvez fractionner des événements entre plusieurs processus hébergés dans des nœuds différents.</span><span class="sxs-lookup"><span data-stu-id="bd9e3-106">Using Apache Storm, you can split events across multiple processes hosted in different nodes.</span></span> <span data-ttu-id="bd9e3-107">Hello intégration des concentrateurs d’événements avec Storm simplifie la consommation d’événements par les points de contrôle en toute transparence sa progression de l’installation de soigneur de Storm, la gestion des points de contrôle persistants et parallèle reçoit de concentrateurs d’événements.</span><span class="sxs-lookup"><span data-stu-id="bd9e3-107">hello Event Hubs integration with Storm simplifies event consumption by transparently checkpointing its progress using Storm's Zookeeper installation, managing persistent checkpoints and parallel receives from Event Hubs.</span></span>

<span data-ttu-id="bd9e3-108">Pour plus d’informations sur les concentrateurs d’événements les modèles de réception, consultez hello [vue d’ensemble des concentrateurs d’événements][Event Hubs overview].</span><span class="sxs-lookup"><span data-stu-id="bd9e3-108">For more information about Event Hubs receive patterns, see hello [Event Hubs overview][Event Hubs overview].</span></span>

## <a name="create-project-and-add-code"></a><span data-ttu-id="bd9e3-109">Créer le projet et ajouter du code</span><span class="sxs-lookup"><span data-stu-id="bd9e3-109">Create project and add code</span></span>

<span data-ttu-id="bd9e3-110">Ce didacticiel utilise un [HDInsight Storm] [ HDInsight Storm] installation, qui est livré avec hello concentrateurs d’événements bec déjà disponible.</span><span class="sxs-lookup"><span data-stu-id="bd9e3-110">This tutorial uses an [HDInsight Storm][HDInsight Storm] installation, which comes with hello Event Hubs spout already available.</span></span>

1. <span data-ttu-id="bd9e3-111">Suivez hello [HDInsight Storm - mise en route](../hdinsight/hdinsight-storm-overview.md) procédure toocreate un HDInsight nouveau cluster, puis connecter tooit via le Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="bd9e3-111">Follow hello [HDInsight Storm - Get Started](../hdinsight/hdinsight-storm-overview.md) procedure toocreate a new HDInsight cluster, and connect tooit via Remote Desktop.</span></span>
2. <span data-ttu-id="bd9e3-112">Hello de copie `%STORM_HOME%\examples\eventhubspout\eventhubs-storm-spout-0.9-jar-with-dependencies.jar` environnement de développement local tooyour de fichier.</span><span class="sxs-lookup"><span data-stu-id="bd9e3-112">Copy hello `%STORM_HOME%\examples\eventhubspout\eventhubs-storm-spout-0.9-jar-with-dependencies.jar` file tooyour local development environment.</span></span> <span data-ttu-id="bd9e3-113">Il contient des événements-storm-bec hello.</span><span class="sxs-lookup"><span data-stu-id="bd9e3-113">This contains hello events-storm-spout.</span></span>
3. <span data-ttu-id="bd9e3-114">Utilisez hello suivant du package de commande tooinstall hello dans le magasin de Maven hello local.</span><span class="sxs-lookup"><span data-stu-id="bd9e3-114">Use hello following command tooinstall hello package into hello local Maven store.</span></span> <span data-ttu-id="bd9e3-115">Cela vous permet de tooadd en tant que référence dans hello tempête de projet dans une étape ultérieure.</span><span class="sxs-lookup"><span data-stu-id="bd9e3-115">This enables you tooadd it as a reference in hello Storm project in a later step.</span></span>

    ```shell
    mvn install:install-file -Dfile=target\eventhubs-storm-spout-0.9-jar-with-dependencies.jar -DgroupId=com.microsoft.eventhubs -DartifactId=eventhubs-storm-spout -Dversion=0.9 -Dpackaging=jar
    ```
4. <span data-ttu-id="bd9e3-116">Dans Eclipse, créez un projet Maven (cliquez sur **Fichier**, **Nouveau**, puis **Projet**).</span><span class="sxs-lookup"><span data-stu-id="bd9e3-116">In Eclipse, create a new Maven project (click **File**, then **New**, then **Project**).</span></span>
   
    ![][12]
5. <span data-ttu-id="bd9e3-117">Sélectionnez l’option **Utiliser l’emplacement d’espace de travail par défaut**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="bd9e3-117">Select **Use default Workspace location**, then click **Next**</span></span>
6. <span data-ttu-id="bd9e3-118">Sélectionnez hello **maven-archétype-démarrage rapide** archétype, puis cliquez sur **suivant**</span><span class="sxs-lookup"><span data-stu-id="bd9e3-118">Select hello **maven-archetype-quickstart** archetype, then click **Next**</span></span>
7. <span data-ttu-id="bd9e3-119">Insérez un **GroupId** et un **ArtifactId**, puis cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="bd9e3-119">Insert a **GroupId** and **ArtifactId**, then click **Finish**</span></span>
8. <span data-ttu-id="bd9e3-120">Dans **pom.xml**, ajouter hello suivant dépendances Bonjour `<dependency>` nœud.</span><span class="sxs-lookup"><span data-stu-id="bd9e3-120">In **pom.xml**, add hello following dependencies in hello `<dependency>` node.</span></span>

    ```xml  
    <dependency>
        <groupId>org.apache.storm</groupId>
        <artifactId>storm-core</artifactId>
        <version>0.9.2-incubating</version>
        <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>com.microsoft.eventhubs</groupId>
        <artifactId>eventhubs-storm-spout</artifactId>
        <version>0.9</version>
    </dependency>
    <dependency>
        <groupId>com.netflix.curator</groupId>
        <artifactId>curator-framework</artifactId>
        <version>1.3.3</version>
        <exclusions>
            <exclusion>
                <groupId>log4j</groupId>
                <artifactId>log4j</artifactId>
            </exclusion>
            <exclusion>
                <groupId>org.slf4j</groupId>
                <artifactId>slf4j-log4j12</artifactId>
            </exclusion>
        </exclusions>
        <scope>provided</scope>
    </dependency>
    ```

9. <span data-ttu-id="bd9e3-121">Bonjour **src** dossier, créez un fichier appelé **config.Properties** et hello copie suivant le contenu, en remplaçant hello `receive rule key` et `event hub name` valeurs :</span><span class="sxs-lookup"><span data-stu-id="bd9e3-121">In hello **src** folder, create a file called **Config.properties** and copy hello following content, substituting hello `receive rule key` and `event hub name` values:</span></span>

    ```java
    eventhubspout.username = ReceiveRule
    eventhubspout.password = {receive rule key}
    eventhubspout.namespace = ioteventhub-ns
    eventhubspout.entitypath = {event hub name}
    eventhubspout.partitions.count = 16
       
    # if not provided, will use storm's zookeeper settings
    # zookeeper.connectionstring=localhost:2181
       
    eventhubspout.checkpoint.interval = 10
    eventhub.receiver.credits = 10
    ```
    <span data-ttu-id="bd9e3-122">Hello valeur pour **eventhub.receiver.credits** détermine le nombre d’événements est traités par lot avant de les libérer le pipeline de Storm toohello.</span><span class="sxs-lookup"><span data-stu-id="bd9e3-122">hello value for **eventhub.receiver.credits** determines how many events are batched before releasing them toohello Storm pipeline.</span></span> <span data-ttu-id="bd9e3-123">Pour des raisons de hello de simplicité, cet exemple définit too10 de cette valeur.</span><span class="sxs-lookup"><span data-stu-id="bd9e3-123">For hello sake of simplicity, this example sets this value too10.</span></span> <span data-ttu-id="bd9e3-124">En production, il doit généralement être définie toohigher ; par exemple, 1024.</span><span class="sxs-lookup"><span data-stu-id="bd9e3-124">In production, it should usually be set toohigher values; for example, 1024.</span></span>
10. <span data-ttu-id="bd9e3-125">Créez une classe appelée **LoggerBolt** avec hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="bd9e3-125">Create a new class called **LoggerBolt** with hello following code:</span></span>
    
    ```java
    import java.util.Map;
    import org.slf4j.Logger;
    import org.slf4j.LoggerFactory;
    import backtype.storm.task.OutputCollector;
    import backtype.storm.task.TopologyContext;
    import backtype.storm.topology.OutputFieldsDeclarer;
    import backtype.storm.topology.base.BaseRichBolt;
    import backtype.storm.tuple.Tuple;
    
    public class LoggerBolt extends BaseRichBolt {
        private OutputCollector collector;
        private static final Logger logger = LoggerFactory
                  .getLogger(LoggerBolt.class);
    
        @Override
        public void execute(Tuple tuple) {
            String value = tuple.getString(0);
            logger.info("Tuple value: " + value);
   
            collector.ack(tuple);
        }
   
        @Override
        public void prepare(Map map, TopologyContext context, OutputCollector collector) {
            this.collector = collector;
            this.count = 0;
        }
        
        @Override
        public void declareOutputFields(OutputFieldsDeclarer declarer) {
            // no output fields
        }
    
    }
    ```
    
    <span data-ttu-id="bd9e3-126">Cet éclair Storm enregistre le contenu hello d’événements de salutation reçue.</span><span class="sxs-lookup"><span data-stu-id="bd9e3-126">This Storm bolt logs hello content of hello received events.</span></span> <span data-ttu-id="bd9e3-127">Cela peut facilement être étendu toostore des tuples dans un service de stockage.</span><span class="sxs-lookup"><span data-stu-id="bd9e3-127">This can easily be extended toostore tuples in a storage service.</span></span> <span data-ttu-id="bd9e3-128">Hello [didacticiel d’analysis HDInsight capteur] utilise ces mêmes données de toostore approche dans HBase.</span><span class="sxs-lookup"><span data-stu-id="bd9e3-128">hello [HDInsight sensor analysis tutorial] uses this same approach toostore data into HBase.</span></span>
11. <span data-ttu-id="bd9e3-129">Créez une classe appelée **LogTopology** avec hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="bd9e3-129">Create a class called **LogTopology** with hello following code:</span></span>
    
    ```java
    import java.io.FileReader;
    import java.util.Properties;
    import backtype.storm.Config;
    import backtype.storm.LocalCluster;
    import backtype.storm.StormSubmitter;
    import backtype.storm.generated.StormTopology;
    import backtype.storm.topology.TopologyBuilder;
    import com.microsoft.eventhubs.samples.EventCount;
    import com.microsoft.eventhubs.spout.EventHubSpout;
    import com.microsoft.eventhubs.spout.EventHubSpoutConfig;
        
    public class LogTopology {
        protected EventHubSpoutConfig spoutConfig;
        protected int numWorkers;
        
        protected void readEHConfig(String[] args) throws Exception {
            Properties properties = new Properties();
            if (args.length > 1) {
                properties.load(new FileReader(args[1]));
            } else {
                properties.load(EventCount.class.getClassLoader()
                        .getResourceAsStream("Config.properties"));
            }
        
            String username = properties.getProperty("eventhubspout.username");
            String password = properties.getProperty("eventhubspout.password");
            String namespaceName = properties
                    .getProperty("eventhubspout.namespace");
            String entityPath = properties.getProperty("eventhubspout.entitypath");
            String zkEndpointAddress = properties
                    .getProperty("zookeeper.connectionstring"); // opt
            int partitionCount = Integer.parseInt(properties
                    .getProperty("eventhubspout.partitions.count"));
            int checkpointIntervalInSeconds = Integer.parseInt(properties
                    .getProperty("eventhubspout.checkpoint.interval"));
            int receiverCredits = Integer.parseInt(properties
                    .getProperty("eventhub.receiver.credits")); // prefetch count
                                                                // (opt)
            System.out.println("Eventhub spout config: ");
            System.out.println("  partition count: " + partitionCount);
            System.out.println("  checkpoint interval: "
                    + checkpointIntervalInSeconds);
            System.out.println("  receiver credits: " + receiverCredits);
     
            spoutConfig = new EventHubSpoutConfig(username, password,
                    namespaceName, entityPath, partitionCount, zkEndpointAddress,
                    checkpointIntervalInSeconds, receiverCredits);
        
            // set hello number of workers toobe hello same as partition number.
            // hello idea is toohave a spout and a logger bolt co-exist in one
            // worker tooavoid shuffling messages across workers in storm cluster.
            numWorkers = spoutConfig.getPartitionCount();
        
            if (args.length > 0) {
                // set topology name so that sample Trident topology can use it as
                // stream name.
                spoutConfig.setTopologyName(args[0]);
            }
        }
        
        protected StormTopology buildTopology() {
            TopologyBuilder topologyBuilder = new TopologyBuilder();
       
            EventHubSpout eventHubSpout = new EventHubSpout(spoutConfig);
            topologyBuilder.setSpout("EventHubsSpout", eventHubSpout,
                    spoutConfig.getPartitionCount()).setNumTasks(
                    spoutConfig.getPartitionCount());
            topologyBuilder
                    .setBolt("LoggerBolt", new LoggerBolt(),
                            spoutConfig.getPartitionCount())
                    .localOrShuffleGrouping("EventHubsSpout")
                    .setNumTasks(spoutConfig.getPartitionCount());
            return topologyBuilder.createTopology();
        }
        
        protected void runScenario(String[] args) throws Exception {
            boolean runLocal = true;
            readEHConfig(args);
            StormTopology topology = buildTopology();
            Config config = new Config();
            config.setDebug(false);
        
            if (runLocal) {
                config.setMaxTaskParallelism(2);
                LocalCluster localCluster = new LocalCluster();
                localCluster.submitTopology("test", config, topology);
                Thread.sleep(5000000);
                localCluster.shutdown();
            } else {
                config.setNumWorkers(numWorkers);
                StormSubmitter.submitTopology(args[0], config, topology);
            }
        }
        
        public static void main(String[] args) throws Exception {
            LogTopology topology = new LogTopology();
            topology.runScenario(args);
        }
    }
    ```

    <span data-ttu-id="bd9e3-130">Cette classe crée un nouveau bec de concentrateurs d’événements, à l’aide des propriétés de hello dans tooinstantiate de fichier de configuration hello il.</span><span class="sxs-lookup"><span data-stu-id="bd9e3-130">This class creates a new Event Hubs spout, using hello properties in hello configuration file tooinstantiate it.</span></span> <span data-ttu-id="bd9e3-131">Il est important de toonote cet exemple crée autant becs verseurs amovibles des tâches en tant que nombre de hello de partitions dans le concentrateur d’événements hello, dans le parallélisme maximal ordre toouse hello autorisée par le concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="bd9e3-131">It is important toonote that this example creates as many spouts tasks as hello number of partitions in hello event hub, in order toouse hello maximum parallelism allowed by that event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bd9e3-132">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bd9e3-132">Next steps</span></span>
<span data-ttu-id="bd9e3-133">Vous pouvez plus d’informations sur les concentrateurs d’événements en visitant hello suivant liens :</span><span class="sxs-lookup"><span data-stu-id="bd9e3-133">You can learn more about Event Hubs by visiting hello following links:</span></span>

* <span data-ttu-id="bd9e3-134">[Vue d’ensemble des hubs d’événements][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="bd9e3-134">[Event Hubs overview][Event Hubs overview]</span></span>
* [<span data-ttu-id="bd9e3-135">Créer un concentrateur d’événements</span><span class="sxs-lookup"><span data-stu-id="bd9e3-135">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="bd9e3-136">FAQ sur les hubs d'événements</span><span class="sxs-lookup"><span data-stu-id="bd9e3-136">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[HDInsight Storm]: ../hdinsight/hdinsight-storm-overview.md
[didacticiel d’analysis HDInsight capteur]: ../hdinsight/hdinsight-storm-sensor-data-analysis.md

<!-- Images -->

[12]: ./media/event-hubs-get-started-receive-storm/create-storm1.png
