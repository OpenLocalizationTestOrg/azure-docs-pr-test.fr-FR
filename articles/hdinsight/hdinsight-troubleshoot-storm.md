---
title: "Résolution de problèmes Storm à l’aide d’Azure HDInsight | Microsoft Docs"
description: "Obtenez les réponses aux questions courantes sur l’utilisation d’Apache Storm avec Azure HDInsight."
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
ms.openlocfilehash: 70a3d762431d90acdd6ed2a432a569f34d0ce447
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-storm-by-using-azure-hdinsight"></a><span data-ttu-id="bfa0d-104">Résolution de problèmes Storm à l’aide d’Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="bfa0d-104">Troubleshoot Storm by using Azure HDInsight</span></span>

<span data-ttu-id="bfa0d-105">Découvrez les principaux problèmes rencontrés lors de l’utilisation de charges utiles Apache Storm dans Apache Ambari, et leur résolution.</span><span class="sxs-lookup"><span data-stu-id="bfa0d-105">Learn about the top issues and their resolutions for working with Apache Storm payloads in Apache Ambari.</span></span>

## <a name="how-do-i-access-the-storm-ui-on-a-cluster"></a><span data-ttu-id="bfa0d-106">Comment accéder à l’interface utilisateur Storm sur un cluster ?</span><span class="sxs-lookup"><span data-stu-id="bfa0d-106">How do I access the Storm UI on a cluster</span></span>
<span data-ttu-id="bfa0d-107">Deux options vous permettent d’accéder à l’interface utilisateur Storm à partir d’un navigateur :</span><span class="sxs-lookup"><span data-stu-id="bfa0d-107">You have two options for accessing the Storm UI from a browser:</span></span>

### <a name="ambari-ui"></a><span data-ttu-id="bfa0d-108">Interface utilisateur Ambari</span><span class="sxs-lookup"><span data-stu-id="bfa0d-108">Ambari UI</span></span>
1. <span data-ttu-id="bfa0d-109">Accédez au tableau de bord Ambari.</span><span class="sxs-lookup"><span data-stu-id="bfa0d-109">Go to the Ambari dashboard.</span></span>
2. <span data-ttu-id="bfa0d-110">Dans la liste des services, sélectionnez **Storm**.</span><span class="sxs-lookup"><span data-stu-id="bfa0d-110">In the list of services, select **Storm**.</span></span>
3. <span data-ttu-id="bfa0d-111">Dans le menu **Quick Links** (Liens rapides), sélectionnez **Storm UI**.</span><span class="sxs-lookup"><span data-stu-id="bfa0d-111">In the **Quick Links** menu, select **Storm UI**.</span></span>

### <a name="direct-link"></a><span data-ttu-id="bfa0d-112">Lien direct</span><span class="sxs-lookup"><span data-stu-id="bfa0d-112">Direct link</span></span>
<span data-ttu-id="bfa0d-113">Vous pouvez accéder à l’interface utilisateur de Storm à l’URL suivante :</span><span class="sxs-lookup"><span data-stu-id="bfa0d-113">You can access the Storm UI at the following URL:</span></span>

<span data-ttu-id="bfa0d-114">https://\<nom DNS du cluster\>/stormui</span><span class="sxs-lookup"><span data-stu-id="bfa0d-114">https://\<cluster DNS name\>/stormui</span></span>

<span data-ttu-id="bfa0d-115">Exemple :</span><span class="sxs-lookup"><span data-stu-id="bfa0d-115">Example:</span></span>

 <span data-ttu-id="bfa0d-116">https://stormcluster.azurehdinsight.net/stormui</span><span class="sxs-lookup"><span data-stu-id="bfa0d-116">https://stormcluster.azurehdinsight.net/stormui</span></span>

## <a name="how-do-i-transfer-storm-event-hub-spout-checkpoint-information-from-one-topology-to-another"></a><span data-ttu-id="bfa0d-117">Comment transférer les informations de point de contrôle du spout Storm Eventhub d’une topologie à une autre ?</span><span class="sxs-lookup"><span data-stu-id="bfa0d-117">How do I transfer Storm event hub spout checkpoint information from one topology to another</span></span>

<span data-ttu-id="bfa0d-118">Lorsque vous développez des topologies qui lisent à partir des hubs d’événements Azure en utilisant le fichier .jar du spout Storm Eventhub, vous devez déployer une topologie portant le même nom sur un nouveau cluster.</span><span class="sxs-lookup"><span data-stu-id="bfa0d-118">When you develop topologies that read from Azure Event Hubs by using the HDInsight Storm event hub spout .jar file, you must deploy a topology that has the same name on a new cluster.</span></span> <span data-ttu-id="bfa0d-119">Toutefois, vous devez conserver les données de point de contrôle validées dans Apache ZooKeeper sur l’ancien cluster.</span><span class="sxs-lookup"><span data-stu-id="bfa0d-119">However, you must retain the checkpoint data that was committed to Apache ZooKeeper on the old cluster.</span></span>

### <a name="where-checkpoint-data-is-stored"></a><span data-ttu-id="bfa0d-120">Où sont stockées les données de point de contrôle ?</span><span class="sxs-lookup"><span data-stu-id="bfa0d-120">Where checkpoint data is stored</span></span>
<span data-ttu-id="bfa0d-121">Les données de point de contrôle des décalages sont enregistrées par le spout EventHub dans Zookeeper sous deux chemins d’accès racine :</span><span class="sxs-lookup"><span data-stu-id="bfa0d-121">Checkpoint data for offsets is stored by the event hub spout in ZooKeeper in two root paths:</span></span>
- <span data-ttu-id="bfa0d-122">Les points de contrôle de spout non transactionnels sont stockés dans /eventhubspout.</span><span class="sxs-lookup"><span data-stu-id="bfa0d-122">Nontransactional spout checkpoints are stored in /eventhubspout.</span></span>
- <span data-ttu-id="bfa0d-123">Les données de point de contrôle de spout transactionnel sont stockées dans /transactional.</span><span class="sxs-lookup"><span data-stu-id="bfa0d-123">Transactional spout checkpoint data is stored in /transactional.</span></span>

### <a name="how-to-restore"></a><span data-ttu-id="bfa0d-124">Comment effectuer une restauration ?</span><span class="sxs-lookup"><span data-stu-id="bfa0d-124">How to restore</span></span>
<span data-ttu-id="bfa0d-125">Pour obtenir les scripts et les bibliothèques utilisés pour exporter des données depuis ZooKeeper et les réimporter sous un nom différent, consultez les [exemples HDInsight Storm](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/tools/zkdatatool-1.0).</span><span class="sxs-lookup"><span data-stu-id="bfa0d-125">To get the scripts and libraries that you use to export data out of ZooKeeper and then import the data back to ZooKeeper with a new name, see [HDInsight Storm examples](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/tools/zkdatatool-1.0).</span></span>

<span data-ttu-id="bfa0d-126">Le dossier lib renferme des fichiers .jar contenant les instructions d’implémentation de l’opération d’exportation/importation.</span><span class="sxs-lookup"><span data-stu-id="bfa0d-126">The lib folder has .jar files that contain the implementation for the export/import operation.</span></span> <span data-ttu-id="bfa0d-127">Le dossier bash comporte un exemple de script montrant comment exporter des données depuis le serveur ZooKeeper de l’ancien cluster et les réimporter dans le serveur ZooKeeper du nouveau cluster.</span><span class="sxs-lookup"><span data-stu-id="bfa0d-127">The bash folder has an example script that demonstrates how to export data from the ZooKeeper server on the old cluster, and then import it back to the ZooKeeper server on the new cluster.</span></span>

<span data-ttu-id="bfa0d-128">Exécutez le script [stormmeta.sh](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/tools/zkdatatool-1.0/bash/stormmeta.sh) à partir des nœuds ZooKeeper pour exporter et réimporter des données.</span><span class="sxs-lookup"><span data-stu-id="bfa0d-128">Run the [stormmeta.sh](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/tools/zkdatatool-1.0/bash/stormmeta.sh) script from the ZooKeeper nodes to export and then import data.</span></span> <span data-ttu-id="bfa0d-129">Indiquez la version appropriée de Hortonworks Data Platform (HDP) dans le script.</span><span class="sxs-lookup"><span data-stu-id="bfa0d-129">Update the script to the correct Hortonworks Data Platform (HDP) version.</span></span> <span data-ttu-id="bfa0d-130">(Nous travaillons sur la création de scripts génériques dans HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bfa0d-130">(We are working on making these scripts generic in HDInsight.</span></span> <span data-ttu-id="bfa0d-131">Les scripts génériques peuvent s’exécuter à partir de n’importe quel nœud du cluster sans modifications de l’utilisateur.)</span><span class="sxs-lookup"><span data-stu-id="bfa0d-131">Generic scripts can run from any node on the cluster without modifications by the user.)</span></span>

<span data-ttu-id="bfa0d-132">La commande d’exportation écrit les métadonnées sur un chemin d’accès Apache Hadoop Distributed File System (HDFS), dans un magasin de stockage Blob Azure ou Azure Data Lake Store) à un emplacement que vous définissez.</span><span class="sxs-lookup"><span data-stu-id="bfa0d-132">The export command writes the metadata to an Apache Hadoop Distributed File System (HDFS) path (in an Azure Blob Storage or Azure Data Lake Store store) at a location that you set.</span></span>

### <a name="examples"></a><span data-ttu-id="bfa0d-133">Exemples</span><span class="sxs-lookup"><span data-stu-id="bfa0d-133">Examples</span></span>

#### <a name="export-offset-metadata"></a><span data-ttu-id="bfa0d-134">Exporter les métadonnées de décalage</span><span class="sxs-lookup"><span data-stu-id="bfa0d-134">Export offset metadata</span></span>
1. <span data-ttu-id="bfa0d-135">À l’aide de SSH, accédez à l’ancien cluster ZooKeeper à partir duquel les données de décalage de point de contrôle doivent être exportées.</span><span class="sxs-lookup"><span data-stu-id="bfa0d-135">Use SSH to go to the ZooKeeper cluster on the cluster from which the checkpoint offset needs to be exported.</span></span>
2. <span data-ttu-id="bfa0d-136">Exécutez la commande suivante (après avoir mis à jour la chaîne de la version HDP) pour exporter les données de décalage ZooKeeper vers le chemin de stockage HDFS /stormmetadta/zkdata :</span><span class="sxs-lookup"><span data-stu-id="bfa0d-136">Run the following command (after you update the HDP version string) to export ZooKeeper offset data to the /stormmetadta/zkdata HDFS path:</span></span>

    ```apache   
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter export /eventhubspout /stormmetadata/zkdata
    ```

#### <a name="import-offset-metadata"></a><span data-ttu-id="bfa0d-137">Importer les métadonnées de décalage</span><span class="sxs-lookup"><span data-stu-id="bfa0d-137">Import offset metadata</span></span>
1. <span data-ttu-id="bfa0d-138">À l’aide de SSH, accédez à l’ancien cluster ZooKeeper à partir duquel les données de décalage de point de contrôle doivent être exportées.</span><span class="sxs-lookup"><span data-stu-id="bfa0d-138">Use SSH to go to the ZooKeeper cluster on the cluster from which the checkpoint offset needs to be exported.</span></span>
2. <span data-ttu-id="bfa0d-139">Exécutez la commande suivante (après avoir mis à jour la chaîne de la version HDP) pour importer les données de décalage ZooKeeper à partir du chemin de stockage HDFS /stormmetadata/zkdata vers le serveur ZooKeeper dans le cluster cible :</span><span class="sxs-lookup"><span data-stu-id="bfa0d-139">Run the following command (after you update the HDP version string) to import ZooKeeper offset data from the HDFS path /stormmetadata/zkdata to the ZooKeeper server on the target cluster:</span></span>

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter import /eventhubspout /home/sshadmin/zkdata
    ```
   
#### <a name="delete-offset-metadata-so-that-topologies-can-start-processing-data-from-the-beginning-or-from-a-timestamp-that-the-user-chooses"></a><span data-ttu-id="bfa0d-140">Supprimer les métadonnées de décalage afin que les topologies puissent commencer à traiter les données à partir du début ou d’un horodatage défini par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="bfa0d-140">Delete offset metadata so that topologies can start processing data from the beginning, or from a timestamp that the user chooses</span></span>
1. <span data-ttu-id="bfa0d-141">À l’aide de SSH, accédez à l’ancien cluster ZooKeeper à partir duquel les données de décalage de point de contrôle doivent être exportées.</span><span class="sxs-lookup"><span data-stu-id="bfa0d-141">Use SSH to go to the ZooKeeper cluster on the cluster from which the checkpoint offset needs to be exported.</span></span>
2. <span data-ttu-id="bfa0d-142">Exécutez la commande suivante (après avoir mis à jour la chaîne de la version HDP) pour supprimer les données de décalage ZooKeeper du cluster actuel :</span><span class="sxs-lookup"><span data-stu-id="bfa0d-142">Run the following command (after you update the HDP version string) to delete all ZooKeeper offset data in the current cluster:</span></span>

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter delete /eventhubspout
    ```

## <a name="how-do-i-locate-storm-binaries-on-a-cluster"></a><span data-ttu-id="bfa0d-143">Comment localiser les fichiers binaires de Storm sur un cluster ?</span><span class="sxs-lookup"><span data-stu-id="bfa0d-143">How do I locate Storm binaries on a cluster</span></span>
<span data-ttu-id="bfa0d-144">Les fichiers binaires Storm de la pile HDP actuelle se trouvent à l’emplacement /usr/hdp/current/storm-client.</span><span class="sxs-lookup"><span data-stu-id="bfa0d-144">Storm binaries for the current HDP stack are in /usr/hdp/current/storm-client.</span></span> <span data-ttu-id="bfa0d-145">L’emplacement est le même pour les nœuds principaux et les nœuds de travail.</span><span class="sxs-lookup"><span data-stu-id="bfa0d-145">The location is the same both for head nodes and for worker nodes.</span></span>
 
<span data-ttu-id="bfa0d-146">Il peut y avoir plusieurs fichiers binaires pour des versions spécifiques de HDP à l’emplacement /usr/hdp (par exemple, /usr/hdp/2.5.0.1233/storm).</span><span class="sxs-lookup"><span data-stu-id="bfa0d-146">There might be multiple binaries for specific HDP versions in /usr/hdp (for example, /usr/hdp/2.5.0.1233/storm).</span></span> <span data-ttu-id="bfa0d-147">Un lien symbolique avec le dossier /usr/hdp/current/storm-client est créé vers la version la plus récente exécutée sur le cluster.</span><span class="sxs-lookup"><span data-stu-id="bfa0d-147">The /usr/hdp/current/storm-client folder is symlinked to the latest version that is running on the cluster.</span></span>

<span data-ttu-id="bfa0d-148">Pour plus d’informations, consultez les pages [Se connecter à HDInsight (Hadoop) à l’aide de SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) et [Storm](http://storm.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="bfa0d-148">For more information, see [Connect to an HDInsight cluster by using SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) and [Storm](http://storm.apache.org/).</span></span>
 
## <a name="how-do-i-determine-the-deployment-topology-of-a-storm-cluster"></a><span data-ttu-id="bfa0d-149">Comment déterminer la topologie de déploiement d’un cluster Storm ?</span><span class="sxs-lookup"><span data-stu-id="bfa0d-149">How do I determine the deployment topology of a Storm cluster</span></span>
<span data-ttu-id="bfa0d-150">Commencez par identifier tous les composants installés avec HDInsight Storm.</span><span class="sxs-lookup"><span data-stu-id="bfa0d-150">First, identify all components that are installed with HDInsight Storm.</span></span> <span data-ttu-id="bfa0d-151">Un cluster Storm se compose de quatre catégories de nœuds :</span><span class="sxs-lookup"><span data-stu-id="bfa0d-151">A Storm cluster consists of four node categories:</span></span>

* <span data-ttu-id="bfa0d-152">Nœuds de passerelle</span><span class="sxs-lookup"><span data-stu-id="bfa0d-152">Gateway nodes</span></span>
* <span data-ttu-id="bfa0d-153">Nœuds principaux</span><span class="sxs-lookup"><span data-stu-id="bfa0d-153">Head nodes</span></span>
* <span data-ttu-id="bfa0d-154">Nœuds ZooKeeper</span><span class="sxs-lookup"><span data-stu-id="bfa0d-154">ZooKeeper nodes</span></span>
* <span data-ttu-id="bfa0d-155">Nœuds de travail</span><span class="sxs-lookup"><span data-stu-id="bfa0d-155">Worker nodes</span></span>
 
### <a name="gateway-nodes"></a><span data-ttu-id="bfa0d-156">Nœuds de passerelle</span><span class="sxs-lookup"><span data-stu-id="bfa0d-156">Gateway nodes</span></span>
<span data-ttu-id="bfa0d-157">Un nœud de passerelle est un service de passerelle et de proxy inverse qui permet un accès public à un service de gestion Ambari actif.</span><span class="sxs-lookup"><span data-stu-id="bfa0d-157">A gateway node is a gateway and reverse proxy service that enables public access to an active Ambari management service.</span></span> <span data-ttu-id="bfa0d-158">Il gère également le choix du leader Ambari.</span><span class="sxs-lookup"><span data-stu-id="bfa0d-158">It also handles Ambari leader election.</span></span>
 
### <a name="head-nodes"></a><span data-ttu-id="bfa0d-159">Nœuds principaux</span><span class="sxs-lookup"><span data-stu-id="bfa0d-159">Head nodes</span></span>
<span data-ttu-id="bfa0d-160">Les nœuds principaux Storm exécutent les services suivants :</span><span class="sxs-lookup"><span data-stu-id="bfa0d-160">Storm head nodes run the following services:</span></span>
* <span data-ttu-id="bfa0d-161">Nimbus</span><span class="sxs-lookup"><span data-stu-id="bfa0d-161">Nimbus</span></span>
* <span data-ttu-id="bfa0d-162">Ambari Server</span><span class="sxs-lookup"><span data-stu-id="bfa0d-162">Ambari server</span></span>
* <span data-ttu-id="bfa0d-163">Ambari Metrics Server</span><span class="sxs-lookup"><span data-stu-id="bfa0d-163">Ambari Metrics server</span></span>
* <span data-ttu-id="bfa0d-164">Ambari Metrics Collector</span><span class="sxs-lookup"><span data-stu-id="bfa0d-164">Ambari Metrics Collector</span></span>
 
### <a name="zookeeper-nodes"></a><span data-ttu-id="bfa0d-165">Nœuds ZooKeeper</span><span class="sxs-lookup"><span data-stu-id="bfa0d-165">ZooKeeper nodes</span></span>
<span data-ttu-id="bfa0d-166">HDInsight est fourni avec un quorum de trois nœuds ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="bfa0d-166">HDInsight comes with a three-node ZooKeeper quorum.</span></span> <span data-ttu-id="bfa0d-167">Sa taille est fixe et n’est pas reconfigurable.</span><span class="sxs-lookup"><span data-stu-id="bfa0d-167">The quorum size is fixed, and cannot be reconfigured.</span></span>
 
<span data-ttu-id="bfa0d-168">Les services Storm du cluster sont configurés pour utiliser le quorum ZooKeeper automatiquement.</span><span class="sxs-lookup"><span data-stu-id="bfa0d-168">Storm services in the cluster are configured to automatically use the ZooKeeper quorum.</span></span>
 
### <a name="worker-nodes"></a><span data-ttu-id="bfa0d-169">Nœuds de travail</span><span class="sxs-lookup"><span data-stu-id="bfa0d-169">Worker nodes</span></span>
<span data-ttu-id="bfa0d-170">Les nœuds de travail Storm exécutent les services suivants :</span><span class="sxs-lookup"><span data-stu-id="bfa0d-170">Storm worker nodes run the following services:</span></span>
* <span data-ttu-id="bfa0d-171">Supervisor</span><span class="sxs-lookup"><span data-stu-id="bfa0d-171">Supervisor</span></span>
* <span data-ttu-id="bfa0d-172">Machines virtuelles Java (JVM) de travail, pour l’exécution des topologies</span><span class="sxs-lookup"><span data-stu-id="bfa0d-172">Worker Java virtual machines (JVMs), for running topologies</span></span>
* <span data-ttu-id="bfa0d-173">Ambari Agent</span><span class="sxs-lookup"><span data-stu-id="bfa0d-173">Ambari agent</span></span>
 
## <a name="how-do-i-locate-storm-event-hub-spout-binaries-for-development"></a><span data-ttu-id="bfa0d-174">Comment localiser les fichiers binaires de spout EventHub Storm pour le développement ?</span><span class="sxs-lookup"><span data-stu-id="bfa0d-174">How do I locate Storm event hub spout binaries for development</span></span>
 
<span data-ttu-id="bfa0d-175">Pour plus d’informations sur l’utilisation de fichiers .jar de spout EventHub Storm avec votre topologie, consultez les ressources suivantes.</span><span class="sxs-lookup"><span data-stu-id="bfa0d-175">For more information about using Storm event hub spout .jar files with your topology, see the following resources.</span></span>
 
### <a name="java-based-topology"></a><span data-ttu-id="bfa0d-176">Topologie basée sur Java</span><span class="sxs-lookup"><span data-stu-id="bfa0d-176">Java-based topology</span></span>
[<span data-ttu-id="bfa0d-177">Traitement des événements Azure Event Hubs avec Storm sur HDInsight (Java)</span><span class="sxs-lookup"><span data-stu-id="bfa0d-177">Process events from Azure Event Hubs with Storm on HDInsight (Java)</span></span>](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-java-event-hub-topology)
 
### <a name="c-based-topology-mono-on-hdinsight-34-linux-storm-clusters"></a><span data-ttu-id="bfa0d-178">Topologie basée sur C# (Mono sur les clusters Storm HDInsight 3.4+ Linux)</span><span class="sxs-lookup"><span data-stu-id="bfa0d-178">C#-based topology (Mono on HDInsight 3.4+ Linux Storm clusters)</span></span>
[<span data-ttu-id="bfa0d-179">Traiter des événements issus d’Azure Event Hubs avec Storm sur HDInsight (C#)</span><span class="sxs-lookup"><span data-stu-id="bfa0d-179">Process events from Azure Event Hubs with Storm on HDInsight (C#)</span></span>](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-csharp-event-hub-topology)
 
### <a name="latest-storm-event-hub-spout-binaries-for-hdinsight-35-linux-storm-clusters"></a><span data-ttu-id="bfa0d-180">Fichiers binaires de spout EventHub Storm les plus récents pour les clusters Storm HDInsight 3.5+ Linux</span><span class="sxs-lookup"><span data-stu-id="bfa0d-180">Latest Storm event hub spout binaries for HDInsight 3.5+ Linux Storm clusters</span></span>
<span data-ttu-id="bfa0d-181">Pour savoir comment utiliser le spout EventHub Storm le plus récent compatible avec les clusters Storm HDInsight 3.5+ Linux, consultez le [fichier readme](https://github.com/hdinsight/mvn-repo/blob/master/README.md) du référentiel mvn-repo.</span><span class="sxs-lookup"><span data-stu-id="bfa0d-181">To learn how to use the latest Storm event hub spout that works with HDInsight 3.5+ Linux Storm clusters, see the mvn-repo [readme file](https://github.com/hdinsight/mvn-repo/blob/master/README.md).</span></span>
 
### <a name="source-code-examples"></a><span data-ttu-id="bfa0d-182">Exemples de code source</span><span class="sxs-lookup"><span data-stu-id="bfa0d-182">Source code examples</span></span>
<span data-ttu-id="bfa0d-183">Consultez ces [exemples](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) pour savoir comment lire et écrire à partir d’Azure EventHub à l’aide d’une topologie Apache Storm (écrite en Java) sur un cluster Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bfa0d-183">See [examples](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) of how to read and write from Azure Event Hub using an Apache Storm topology (written in Java) on an Azure HDInsight cluster.</span></span>
 
## <a name="how-do-i-locate-storm-log4j-configuration-files-on-clusters"></a><span data-ttu-id="bfa0d-184">Comment localiser les fichiers de configuration Storm Log4J sur les clusters ?</span><span class="sxs-lookup"><span data-stu-id="bfa0d-184">How do I locate Storm Log4J configuration files on clusters</span></span>
 
<span data-ttu-id="bfa0d-185">Pour identifier les fichiers de configuration Apache Log4J des services Storm.</span><span class="sxs-lookup"><span data-stu-id="bfa0d-185">To identify Apache Log4J configuration files for Storm services.</span></span>
 
### <a name="on-head-nodes"></a><span data-ttu-id="bfa0d-186">Sur les nœuds principaux</span><span class="sxs-lookup"><span data-stu-id="bfa0d-186">On head nodes</span></span>
<span data-ttu-id="bfa0d-187">Le fichier de configuration Log4J du service Nimbus est lu à partir du chemin /usr/hdp/\<version HDP\>/storm/log4j2/cluster.xml.</span><span class="sxs-lookup"><span data-stu-id="bfa0d-187">The Nimbus Log4J configuration is read from /usr/hdp/\<HDP version\>/storm/log4j2/cluster.xml.</span></span>
 
### <a name="on-worker-nodes"></a><span data-ttu-id="bfa0d-188">Sur les nœuds de travail</span><span class="sxs-lookup"><span data-stu-id="bfa0d-188">On worker nodes</span></span>
<span data-ttu-id="bfa0d-189">Le fichier de configuration Log4J du service Supervisor est lu à partir du chemin /usr/hdp/\<version HDP\>/storm/log4j2/cluster.xml.</span><span class="sxs-lookup"><span data-stu-id="bfa0d-189">The supervisor Log4J configuration is read from /usr/hdp/\<HDP version\>/storm/log4j2/cluster.xml.</span></span>
 
<span data-ttu-id="bfa0d-190">Le fichier de configuration Log4J du Worker est lu à partir du chemin /usr/hdp/\<version HDP\>/storm/log4j2/cluster.xml.</span><span class="sxs-lookup"><span data-stu-id="bfa0d-190">The worker Log4J configuration file is read from /usr/hdp/\<HDP version\>/storm/log4j2/worker.xml.</span></span>
 
<span data-ttu-id="bfa0d-191">Par exemple : /usr/hdp/2.6.0.2-76/storm/log4j2/cluster.xml /usr/hdp/2.6.0.2-76/storm/log4j2/worker.xml</span><span class="sxs-lookup"><span data-stu-id="bfa0d-191">Examples: /usr/hdp/2.6.0.2-76/storm/log4j2/cluster.xml /usr/hdp/2.6.0.2-76/storm/log4j2/worker.xml</span></span>

