---
title: "aaaTroubleshoot Storm à l’aide d’Azure HDInsight | Documents Microsoft"
description: "Obtenez des réponses toocommon des questions sur l’utilisation d’Apache Storm avec Azure HDInsight."
keywords: "Azure HDInsight, Storm, FAQ, guide de dépannage, problèmes courants"
services: Azure HDInsight
documentationcenter: na
author: raviperi
manager: 
editor: 
ms.assetid: 74E51183-3EF4-4C67-AA60-6E12FAC999B5
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: raviperi
ms.openlocfilehash: 51bcb3dc28eff5ee7bb33252fb2ec71a88ed8e09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-storm-by-using-azure-hdinsight"></a><span data-ttu-id="809ea-104">Résolution de problèmes Storm à l’aide d’Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="809ea-104">Troubleshoot Storm by using Azure HDInsight</span></span>

<span data-ttu-id="809ea-105">En savoir plus sur les principaux problèmes de hello et leurs résolutions pour travailler avec des charges utiles d’Apache Storm dans Apache Ambari.</span><span class="sxs-lookup"><span data-stu-id="809ea-105">Learn about hello top issues and their resolutions for working with Apache Storm payloads in Apache Ambari.</span></span>

## <a name="how-do-i-access-hello-storm-ui-on-a-cluster"></a><span data-ttu-id="809ea-106">Comment accéder à hello Storm UI sur un cluster</span><span class="sxs-lookup"><span data-stu-id="809ea-106">How do I access hello Storm UI on a cluster</span></span>
<span data-ttu-id="809ea-107">Vous avez deux options pour l’accès aux hello Storm UI à partir d’un navigateur :</span><span class="sxs-lookup"><span data-stu-id="809ea-107">You have two options for accessing hello Storm UI from a browser:</span></span>

### <a name="ambari-ui"></a><span data-ttu-id="809ea-108">Interface utilisateur Ambari</span><span class="sxs-lookup"><span data-stu-id="809ea-108">Ambari UI</span></span>
1. <span data-ttu-id="809ea-109">Accédez à tableau de bord toohello Ambari.</span><span class="sxs-lookup"><span data-stu-id="809ea-109">Go toohello Ambari dashboard.</span></span>
2. <span data-ttu-id="809ea-110">Dans la liste de hello des services, sélectionnez **Storm**.</span><span class="sxs-lookup"><span data-stu-id="809ea-110">In hello list of services, select **Storm**.</span></span>
3. <span data-ttu-id="809ea-111">Bonjour **liens rapides** menu, sélectionnez **Storm UI**.</span><span class="sxs-lookup"><span data-stu-id="809ea-111">In hello **Quick Links** menu, select **Storm UI**.</span></span>

### <a name="direct-link"></a><span data-ttu-id="809ea-112">Lien direct</span><span class="sxs-lookup"><span data-stu-id="809ea-112">Direct link</span></span>
<span data-ttu-id="809ea-113">Vous pouvez accéder hello Storm UI à hello suivant l’URL :</span><span class="sxs-lookup"><span data-stu-id="809ea-113">You can access hello Storm UI at hello following URL:</span></span>

<span data-ttu-id="809ea-114">https://\<nom DNS du cluster\>/stormui</span><span class="sxs-lookup"><span data-stu-id="809ea-114">https://\<cluster DNS name\>/stormui</span></span>

<span data-ttu-id="809ea-115">Exemple :</span><span class="sxs-lookup"><span data-stu-id="809ea-115">Example:</span></span>

 <span data-ttu-id="809ea-116">https://stormcluster.azurehdinsight.net/stormui</span><span class="sxs-lookup"><span data-stu-id="809ea-116">https://stormcluster.azurehdinsight.net/stormui</span></span>

## <a name="how-do-i-transfer-storm-event-hub-spout-checkpoint-information-from-one-topology-tooanother"></a><span data-ttu-id="809ea-117">Comment transférer des informations de point de contrôle du concentrateur bec Storm événement à partir d’une topologie tooanother</span><span class="sxs-lookup"><span data-stu-id="809ea-117">How do I transfer Storm event hub spout checkpoint information from one topology tooanother</span></span>

<span data-ttu-id="809ea-118">Lorsque vous développez des topologies de lecture à partir de concentrateurs d’événements Azure à l’aide de hello HDInsight Storm événement hub bec .jar fichier, vous devez déployer une topologie disposant hello même nom sur un nouveau cluster.</span><span class="sxs-lookup"><span data-stu-id="809ea-118">When you develop topologies that read from Azure Event Hubs by using hello HDInsight Storm event hub spout .jar file, you must deploy a topology that has hello same name on a new cluster.</span></span> <span data-ttu-id="809ea-119">Toutefois, vous devez conserver les données de point de contrôle hello qui a été validée tooApache soigneur sur l’ancien cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="809ea-119">However, you must retain hello checkpoint data that was committed tooApache ZooKeeper on hello old cluster.</span></span>

### <a name="where-checkpoint-data-is-stored"></a><span data-ttu-id="809ea-120">Où sont stockées les données de point de contrôle ?</span><span class="sxs-lookup"><span data-stu-id="809ea-120">Where checkpoint data is stored</span></span>
<span data-ttu-id="809ea-121">Les données de point de contrôle pour les décalages sont stockées par bec de concentrateur d’événements hello dans soigneur dans deux chemins d’accès racine :</span><span class="sxs-lookup"><span data-stu-id="809ea-121">Checkpoint data for offsets is stored by hello event hub spout in ZooKeeper in two root paths:</span></span>
- <span data-ttu-id="809ea-122">Les points de contrôle de spout non transactionnels sont stockés dans /eventhubspout.</span><span class="sxs-lookup"><span data-stu-id="809ea-122">Nontransactional spout checkpoints are stored in /eventhubspout.</span></span>
- <span data-ttu-id="809ea-123">Les données de point de contrôle de spout transactionnel sont stockées dans /transactional.</span><span class="sxs-lookup"><span data-stu-id="809ea-123">Transactional spout checkpoint data is stored in /transactional.</span></span>

### <a name="how-toorestore"></a><span data-ttu-id="809ea-124">Comment toorestore</span><span class="sxs-lookup"><span data-stu-id="809ea-124">How toorestore</span></span>
<span data-ttu-id="809ea-125">scripts de hello tooget et bibliothèques que vous utilisez données tooexport hors soigneur et l’importer tooZooKeeper de retour de données hello avec un nouveau nom, consultez [exemples de HDInsight Storm](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/tools/zkdatatool-1.0).</span><span class="sxs-lookup"><span data-stu-id="809ea-125">tooget hello scripts and libraries that you use tooexport data out of ZooKeeper and then import hello data back tooZooKeeper with a new name, see [HDInsight Storm examples](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/tools/zkdatatool-1.0).</span></span>

<span data-ttu-id="809ea-126">le dossier lib Hello a fichiers .jar qui contiennent l’implémentation hello pour l’opération d’importation/exportation hello.</span><span class="sxs-lookup"><span data-stu-id="809ea-126">hello lib folder has .jar files that contain hello implementation for hello export/import operation.</span></span> <span data-ttu-id="809ea-127">Hello bash dossier a un exemple de script qui montre comment les données tooexport à partir de hello server soigneur sur l’ancien cluster de hello et importez-le server de soigneur toohello arrière sur le nouveau cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="809ea-127">hello bash folder has an example script that demonstrates how tooexport data from hello ZooKeeper server on hello old cluster, and then import it back toohello ZooKeeper server on hello new cluster.</span></span>

<span data-ttu-id="809ea-128">Exécutez hello [stormmeta.sh](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/tools/zkdatatool-1.0/bash/stormmeta.sh) hello soigneur nœuds tooexport de script et importer des données.</span><span class="sxs-lookup"><span data-stu-id="809ea-128">Run hello [stormmeta.sh](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/tools/zkdatatool-1.0/bash/stormmeta.sh) script from hello ZooKeeper nodes tooexport and then import data.</span></span> <span data-ttu-id="809ea-129">Mise à jour hello script toohello Hortonworks Data Platform (HDP) version correcte.</span><span class="sxs-lookup"><span data-stu-id="809ea-129">Update hello script toohello correct Hortonworks Data Platform (HDP) version.</span></span> <span data-ttu-id="809ea-130">(Nous travaillons sur la création de scripts génériques dans HDInsight.</span><span class="sxs-lookup"><span data-stu-id="809ea-130">(We are working on making these scripts generic in HDInsight.</span></span> <span data-ttu-id="809ea-131">Scripts génériques peuvent s’exécuter n’importe quel nœud à cluster hello sans modification par l’utilisateur de hello.)</span><span class="sxs-lookup"><span data-stu-id="809ea-131">Generic scripts can run from any node on hello cluster without modifications by hello user.)</span></span>

<span data-ttu-id="809ea-132">commande d’exportation Hello écrit hello métadonnées tooan système de fichiers distribués d’Apache Hadoop (HDFS) chemin (dans un magasin de stockage d’objets Blob Azure ou Azure Data Lake Store) à un emplacement que vous définissez.</span><span class="sxs-lookup"><span data-stu-id="809ea-132">hello export command writes hello metadata tooan Apache Hadoop Distributed File System (HDFS) path (in an Azure Blob Storage or Azure Data Lake Store store) at a location that you set.</span></span>

### <a name="examples"></a><span data-ttu-id="809ea-133">Exemples</span><span class="sxs-lookup"><span data-stu-id="809ea-133">Examples</span></span>

#### <a name="export-offset-metadata"></a><span data-ttu-id="809ea-134">Exporter les métadonnées de décalage</span><span class="sxs-lookup"><span data-stu-id="809ea-134">Export offset metadata</span></span>
1. <span data-ttu-id="809ea-135">Utilisez cluster soigneur SSH toogo toohello sur cluster hello quel point de contrôle hello offset doit toobe exporté.</span><span class="sxs-lookup"><span data-stu-id="809ea-135">Use SSH toogo toohello ZooKeeper cluster on hello cluster from which hello checkpoint offset needs toobe exported.</span></span>
2. <span data-ttu-id="809ea-136">Exécution hello commande suivante (une fois que vous mettez à jour hello chaîne de version HDP) tooexport soigneur décalage des données toohello /stormmetadta/zkdata HDFS chemin d’accès :</span><span class="sxs-lookup"><span data-stu-id="809ea-136">Run hello following command (after you update hello HDP version string) tooexport ZooKeeper offset data toohello /stormmetadta/zkdata HDFS path:</span></span>

    ```apache   
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter export /eventhubspout /stormmetadata/zkdata
    ```

#### <a name="import-offset-metadata"></a><span data-ttu-id="809ea-137">Importer les métadonnées de décalage</span><span class="sxs-lookup"><span data-stu-id="809ea-137">Import offset metadata</span></span>
1. <span data-ttu-id="809ea-138">Utilisez cluster soigneur SSH toogo toohello sur cluster hello quel point de contrôle hello offset doit toobe exporté.</span><span class="sxs-lookup"><span data-stu-id="809ea-138">Use SSH toogo toohello ZooKeeper cluster on hello cluster from which hello checkpoint offset needs toobe exported.</span></span>
2. <span data-ttu-id="809ea-139">Exécution hello après une commande (une fois que vous mettez à jour de chaîne de version HDP hello) tooimport soigneur décalage des données hello HDFS chemin d’accès/stormmetadata/zkdata toohello soigneur serveur sur un cluster de hello cible :</span><span class="sxs-lookup"><span data-stu-id="809ea-139">Run hello following command (after you update hello HDP version string) tooimport ZooKeeper offset data from hello HDFS path /stormmetadata/zkdata toohello ZooKeeper server on hello target cluster:</span></span>

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter import /eventhubspout /home/sshadmin/zkdata
    ```
   
#### <a name="delete-offset-metadata-so-that-topologies-can-start-processing-data-from-hello-beginning-or-from-a-timestamp-that-hello-user-chooses"></a><span data-ttu-id="809ea-140">Supprimer les métadonnées de décalage topologies peuvent démarrer le traitement des données à partir du début de hello, ou d’un horodateur choisit cet utilisateur hello</span><span class="sxs-lookup"><span data-stu-id="809ea-140">Delete offset metadata so that topologies can start processing data from hello beginning, or from a timestamp that hello user chooses</span></span>
1. <span data-ttu-id="809ea-141">Utilisez cluster soigneur SSH toogo toohello sur cluster hello quel point de contrôle hello offset doit toobe exporté.</span><span class="sxs-lookup"><span data-stu-id="809ea-141">Use SSH toogo toohello ZooKeeper cluster on hello cluster from which hello checkpoint offset needs toobe exported.</span></span>
2. <span data-ttu-id="809ea-142">Exécution hello après une commande (une fois que vous mettez à jour de chaîne de version HDP hello) toodelete tous les soigneur décalage des données dans le cluster actuel hello :</span><span class="sxs-lookup"><span data-stu-id="809ea-142">Run hello following command (after you update hello HDP version string) toodelete all ZooKeeper offset data in hello current cluster:</span></span>

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter delete /eventhubspout
    ```

## <a name="how-do-i-locate-storm-binaries-on-a-cluster"></a><span data-ttu-id="809ea-143">Comment localiser les fichiers binaires de Storm sur un cluster ?</span><span class="sxs-lookup"><span data-stu-id="809ea-143">How do I locate Storm binaries on a cluster</span></span>
<span data-ttu-id="809ea-144">Fichiers binaires de Storm pour la pile HDP hello en cours sont dans /usr/hdp/current/storm-client.</span><span class="sxs-lookup"><span data-stu-id="809ea-144">Storm binaries for hello current HDP stack are in /usr/hdp/current/storm-client.</span></span> <span data-ttu-id="809ea-145">emplacement de Hello est hello même pour les nœuds principaux et les nœuds de travail.</span><span class="sxs-lookup"><span data-stu-id="809ea-145">hello location is hello same both for head nodes and for worker nodes.</span></span>
 
<span data-ttu-id="809ea-146">Il peut y avoir plusieurs fichiers binaires pour des versions spécifiques de HDP à l’emplacement /usr/hdp (par exemple, /usr/hdp/2.5.0.1233/storm).</span><span class="sxs-lookup"><span data-stu-id="809ea-146">There might be multiple binaries for specific HDP versions in /usr/hdp (for example, /usr/hdp/2.5.0.1233/storm).</span></span> <span data-ttu-id="809ea-147">dossier de /usr/hdp/current/storm-client Hello est symlinked toohello version la plus récente est en cours d’exécution sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="809ea-147">hello /usr/hdp/current/storm-client folder is symlinked toohello latest version that is running on hello cluster.</span></span>

<span data-ttu-id="809ea-148">Pour plus d’informations, consultez [cluster de HDInsight tooan de se connecter à l’aide de SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) et [Storm](http://storm.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="809ea-148">For more information, see [Connect tooan HDInsight cluster by using SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) and [Storm](http://storm.apache.org/).</span></span>
 
## <a name="how-do-i-determine-hello-deployment-topology-of-a-storm-cluster"></a><span data-ttu-id="809ea-149">Comment déterminer la topologie de déploiement hello d’un cluster Storm</span><span class="sxs-lookup"><span data-stu-id="809ea-149">How do I determine hello deployment topology of a Storm cluster</span></span>
<span data-ttu-id="809ea-150">Commencez par identifier tous les composants installés avec HDInsight Storm.</span><span class="sxs-lookup"><span data-stu-id="809ea-150">First, identify all components that are installed with HDInsight Storm.</span></span> <span data-ttu-id="809ea-151">Un cluster Storm se compose de quatre catégories de nœuds :</span><span class="sxs-lookup"><span data-stu-id="809ea-151">A Storm cluster consists of four node categories:</span></span>

* <span data-ttu-id="809ea-152">Nœuds de passerelle</span><span class="sxs-lookup"><span data-stu-id="809ea-152">Gateway nodes</span></span>
* <span data-ttu-id="809ea-153">Nœuds principaux</span><span class="sxs-lookup"><span data-stu-id="809ea-153">Head nodes</span></span>
* <span data-ttu-id="809ea-154">Nœuds ZooKeeper</span><span class="sxs-lookup"><span data-stu-id="809ea-154">ZooKeeper nodes</span></span>
* <span data-ttu-id="809ea-155">Nœuds de travail</span><span class="sxs-lookup"><span data-stu-id="809ea-155">Worker nodes</span></span>
 
### <a name="gateway-nodes"></a><span data-ttu-id="809ea-156">Nœuds de passerelle</span><span class="sxs-lookup"><span data-stu-id="809ea-156">Gateway nodes</span></span>
<span data-ttu-id="809ea-157">Un nœud de passerelle est une passerelle et le service de proxy inverse qui permet un accès public tooan active Ambari management service.</span><span class="sxs-lookup"><span data-stu-id="809ea-157">A gateway node is a gateway and reverse proxy service that enables public access tooan active Ambari management service.</span></span> <span data-ttu-id="809ea-158">Il gère également le choix du leader Ambari.</span><span class="sxs-lookup"><span data-stu-id="809ea-158">It also handles Ambari leader election.</span></span>
 
### <a name="head-nodes"></a><span data-ttu-id="809ea-159">Nœuds principaux</span><span class="sxs-lookup"><span data-stu-id="809ea-159">Head nodes</span></span>
<span data-ttu-id="809ea-160">Les nœuds principaux Storm exécutent hello suivant services :</span><span class="sxs-lookup"><span data-stu-id="809ea-160">Storm head nodes run hello following services:</span></span>
* <span data-ttu-id="809ea-161">Nimbus</span><span class="sxs-lookup"><span data-stu-id="809ea-161">Nimbus</span></span>
* <span data-ttu-id="809ea-162">Ambari Server</span><span class="sxs-lookup"><span data-stu-id="809ea-162">Ambari server</span></span>
* <span data-ttu-id="809ea-163">Ambari Metrics Server</span><span class="sxs-lookup"><span data-stu-id="809ea-163">Ambari Metrics server</span></span>
* <span data-ttu-id="809ea-164">Ambari Metrics Collector</span><span class="sxs-lookup"><span data-stu-id="809ea-164">Ambari Metrics Collector</span></span>
 
### <a name="zookeeper-nodes"></a><span data-ttu-id="809ea-165">Nœuds ZooKeeper</span><span class="sxs-lookup"><span data-stu-id="809ea-165">ZooKeeper nodes</span></span>
<span data-ttu-id="809ea-166">HDInsight est fourni avec un quorum de trois nœuds ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="809ea-166">HDInsight comes with a three-node ZooKeeper quorum.</span></span> <span data-ttu-id="809ea-167">taille du quorum Hello est fixe et ne peuvent pas être reconfiguré.</span><span class="sxs-lookup"><span data-stu-id="809ea-167">hello quorum size is fixed, and cannot be reconfigured.</span></span>
 
<span data-ttu-id="809ea-168">Services Storm dans un cluster de hello sont quorum de soigneur tooautomatically configuré utilisez hello.</span><span class="sxs-lookup"><span data-stu-id="809ea-168">Storm services in hello cluster are configured tooautomatically use hello ZooKeeper quorum.</span></span>
 
### <a name="worker-nodes"></a><span data-ttu-id="809ea-169">Nœuds de travail</span><span class="sxs-lookup"><span data-stu-id="809ea-169">Worker nodes</span></span>
<span data-ttu-id="809ea-170">Nœuds de travail Storm exécutent hello suivant services :</span><span class="sxs-lookup"><span data-stu-id="809ea-170">Storm worker nodes run hello following services:</span></span>
* <span data-ttu-id="809ea-171">Supervisor</span><span class="sxs-lookup"><span data-stu-id="809ea-171">Supervisor</span></span>
* <span data-ttu-id="809ea-172">Machines virtuelles Java (JVM) de travail, pour l’exécution des topologies</span><span class="sxs-lookup"><span data-stu-id="809ea-172">Worker Java virtual machines (JVMs), for running topologies</span></span>
* <span data-ttu-id="809ea-173">Ambari Agent</span><span class="sxs-lookup"><span data-stu-id="809ea-173">Ambari agent</span></span>
 
## <a name="how-do-i-locate-storm-event-hub-spout-binaries-for-development"></a><span data-ttu-id="809ea-174">Comment localiser les fichiers binaires de spout EventHub Storm pour le développement ?</span><span class="sxs-lookup"><span data-stu-id="809ea-174">How do I locate Storm event hub spout binaries for development</span></span>
 
<span data-ttu-id="809ea-175">Pour plus d’informations sur l’utilisation de fichiers .jar de Storm événement hub bec avec votre topologie, consultez hello suivant des ressources.</span><span class="sxs-lookup"><span data-stu-id="809ea-175">For more information about using Storm event hub spout .jar files with your topology, see hello following resources.</span></span>
 
### <a name="java-based-topology"></a><span data-ttu-id="809ea-176">Topologie basée sur Java</span><span class="sxs-lookup"><span data-stu-id="809ea-176">Java-based topology</span></span>
[<span data-ttu-id="809ea-177">Traitement des événements Azure Event Hubs avec Storm sur HDInsight (Java)</span><span class="sxs-lookup"><span data-stu-id="809ea-177">Process events from Azure Event Hubs with Storm on HDInsight (Java)</span></span>](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-java-event-hub-topology)
 
### <a name="c-based-topology-mono-on-hdinsight-34-linux-storm-clusters"></a><span data-ttu-id="809ea-178">Topologie basée sur C# (Mono sur les clusters Storm HDInsight 3.4+ Linux)</span><span class="sxs-lookup"><span data-stu-id="809ea-178">C#-based topology (Mono on HDInsight 3.4+ Linux Storm clusters)</span></span>
[<span data-ttu-id="809ea-179">Traiter des événements issus d’Azure Event Hubs avec Storm sur HDInsight (C#)</span><span class="sxs-lookup"><span data-stu-id="809ea-179">Process events from Azure Event Hubs with Storm on HDInsight (C#)</span></span>](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-csharp-event-hub-topology)
 
### <a name="latest-storm-event-hub-spout-binaries-for-hdinsight-35-linux-storm-clusters"></a><span data-ttu-id="809ea-180">Fichiers binaires de spout EventHub Storm les plus récents pour les clusters Storm HDInsight 3.5+ Linux</span><span class="sxs-lookup"><span data-stu-id="809ea-180">Latest Storm event hub spout binaries for HDInsight 3.5+ Linux Storm clusters</span></span>
<span data-ttu-id="809ea-181">toolearn toouse hello dernière Storm événement hub bec qui fonctionne avec HDInsight 3.5 + Linux Storm clusters, voir hello mvn-repo [fichier Lisez-moi](https://github.com/hdinsight/mvn-repo/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="809ea-181">toolearn how toouse hello latest Storm event hub spout that works with HDInsight 3.5+ Linux Storm clusters, see hello mvn-repo [readme file](https://github.com/hdinsight/mvn-repo/blob/master/README.md).</span></span>
 
### <a name="source-code-examples"></a><span data-ttu-id="809ea-182">Exemples de code source</span><span class="sxs-lookup"><span data-stu-id="809ea-182">Source code examples</span></span>
<span data-ttu-id="809ea-183">Consultez [exemples](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) de façon tooread et écrire à partir du concentrateur d’événements Azure à l’aide d’une topologie d’Apache Storm (écrite en Java) sur un cluster Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="809ea-183">See [examples](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) of how tooread and write from Azure Event Hub using an Apache Storm topology (written in Java) on an Azure HDInsight cluster.</span></span>
 
## <a name="how-do-i-locate-storm-log4j-configuration-files-on-clusters"></a><span data-ttu-id="809ea-184">Comment localiser les fichiers de configuration Storm Log4J sur les clusters ?</span><span class="sxs-lookup"><span data-stu-id="809ea-184">How do I locate Storm Log4J configuration files on clusters</span></span>
 
<span data-ttu-id="809ea-185">tooidentify Apache Log4J les fichiers de configuration pour les services de Storm.</span><span class="sxs-lookup"><span data-stu-id="809ea-185">tooidentify Apache Log4J configuration files for Storm services.</span></span>
 
### <a name="on-head-nodes"></a><span data-ttu-id="809ea-186">Sur les nœuds principaux</span><span class="sxs-lookup"><span data-stu-id="809ea-186">On head nodes</span></span>
<span data-ttu-id="809ea-187">configuration de Hello Nimbus Log4J est lu à partir / usr/hdp/\<version HDP\>/storm/log4j2/cluster.xml.</span><span class="sxs-lookup"><span data-stu-id="809ea-187">hello Nimbus Log4J configuration is read from /usr/hdp/\<HDP version\>/storm/log4j2/cluster.xml.</span></span>
 
### <a name="on-worker-nodes"></a><span data-ttu-id="809ea-188">Sur les nœuds de travail</span><span class="sxs-lookup"><span data-stu-id="809ea-188">On worker nodes</span></span>
<span data-ttu-id="809ea-189">configuration de superviseur Log4J Hello est lu à partir / usr/hdp/\<version HDP\>/storm/log4j2/cluster.xml.</span><span class="sxs-lookup"><span data-stu-id="809ea-189">hello supervisor Log4J configuration is read from /usr/hdp/\<HDP version\>/storm/log4j2/cluster.xml.</span></span>
 
<span data-ttu-id="809ea-190">fichier de configuration du travail Log4J Hello est lu à partir / usr/hdp/\<version HDP\>/storm/log4j2/worker.xml.</span><span class="sxs-lookup"><span data-stu-id="809ea-190">hello worker Log4J configuration file is read from /usr/hdp/\<HDP version\>/storm/log4j2/worker.xml.</span></span>
 
<span data-ttu-id="809ea-191">Par exemple : /usr/hdp/2.6.0.2-76/storm/log4j2/cluster.xml /usr/hdp/2.6.0.2-76/storm/log4j2/worker.xml</span><span class="sxs-lookup"><span data-stu-id="809ea-191">Examples: /usr/hdp/2.6.0.2-76/storm/log4j2/cluster.xml /usr/hdp/2.6.0.2-76/storm/log4j2/worker.xml</span></span>

