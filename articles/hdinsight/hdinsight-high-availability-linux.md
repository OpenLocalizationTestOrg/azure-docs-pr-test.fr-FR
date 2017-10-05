---
title: "Haute disponibilité pour Hadoop - Azure HDInsight | Documents Microsoft"
description: "Découvrez comment les clusters HDInsight améliorent la fiabilité et la disponibilité en utilisant un nœud principal supplémentaire. Découvrez dans quelle mesure les services Hadoop tels qu’Ambari et Hive sont concernés, et comment se connecter à chaque nœud principal via SSH."
services: hdinsight
editor: cgronlun
manager: jhubbard
author: Blackmist
documentationcenter: 
tags: azure-portal
keywords: "haute disponibilité hadoop"
ms.assetid: 99c9f59c-cf6b-4529-99d1-bf060435e8d4
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 07/28/2017
ms.author: larryfr
ms.openlocfilehash: e66ba67a36fc48d1762ba302d708e060489fdc71
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="availability-and-reliability-of-hadoop-clusters-in-hdinsight"></a><span data-ttu-id="9af08-105">Disponibilité et fiabilité des clusters Hadoop dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="9af08-105">Availability and reliability of Hadoop clusters in HDInsight</span></span>

<span data-ttu-id="9af08-106">Les clusters HDInsight fournissent deux nœuds principaux afin d’augmenter la disponibilité et la fiabilité des services et travaux Hadoop en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="9af08-106">HDInsight clusters provide two head nodes to increase the availability and reliability of Hadoop services and jobs running.</span></span>

<span data-ttu-id="9af08-107">Hadoop garantit de hauts niveaux de disponibilité et de fiabilité en répliquant des services et données sur plusieurs nœuds d’un cluster.</span><span class="sxs-lookup"><span data-stu-id="9af08-107">Hadoop achieves high availability and reliability by replicating services and data across multiple nodes in a cluster.</span></span> <span data-ttu-id="9af08-108">Toutefois, les distributions standard de Hadoop ne comportent généralement qu’un seul nœud principal.</span><span class="sxs-lookup"><span data-stu-id="9af08-108">However standard distributions of Hadoop typically have only a single head node.</span></span> <span data-ttu-id="9af08-109">Toute défaillance du nœud principal unique peut entraîner un arrêt de fonctionnement du cluster.</span><span class="sxs-lookup"><span data-stu-id="9af08-109">Any outage of the single head node can cause the cluster to stop working.</span></span> <span data-ttu-id="9af08-110">HDInsight fournit deux nœuds principaux pour améliorer la disponibilité et la fiabilité de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="9af08-110">HDInsight provides two headnodes to improve Hadoop's availability and reliability.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9af08-111">Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="9af08-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="9af08-112">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="9af08-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="availability-and-reliability-of-nodes"></a><span data-ttu-id="9af08-113">Disponibilité et fiabilité des nœuds</span><span class="sxs-lookup"><span data-stu-id="9af08-113">Availability and reliability of nodes</span></span>

<span data-ttu-id="9af08-114">Les nœuds d’un cluster HDInsight sont implémentés à l’aide de machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="9af08-114">Nodes in an HDInsight cluster are implemented using Azure Virtual Machines.</span></span> <span data-ttu-id="9af08-115">Les sections ci-après décrivent les différents types de nœuds utilisés avec HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9af08-115">The following sections discuss the individual node types used with HDInsight.</span></span> 

> [!NOTE]
> <span data-ttu-id="9af08-116">Les types de nœuds utilisables varient selon le type de cluster concerné.</span><span class="sxs-lookup"><span data-stu-id="9af08-116">Not all node types are used for a cluster type.</span></span> <span data-ttu-id="9af08-117">Par exemple, un type de cluster Hadoop ne comporte aucun nœud Nimbus.</span><span class="sxs-lookup"><span data-stu-id="9af08-117">For example, a Hadoop cluster type does not have any Nimbus nodes.</span></span> <span data-ttu-id="9af08-118">Pour plus d’informations sur les nœuds utilisés par les types de clusters HDInsight, consultez la section Types de cluster du document [Création de clusters Hadoop basés sur Linux dans HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span><span class="sxs-lookup"><span data-stu-id="9af08-118">For more information on nodes used by HDInsight cluster types, see the Cluster types section of the [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) document.</span></span>

### <a name="head-nodes"></a><span data-ttu-id="9af08-119">Nœuds principaux</span><span class="sxs-lookup"><span data-stu-id="9af08-119">Head nodes</span></span>

<span data-ttu-id="9af08-120">Pour garantir une haute disponibilité des services Hadoop, HDInsight fournit deux nœuds principaux.</span><span class="sxs-lookup"><span data-stu-id="9af08-120">To ensure high availability of Hadoop services, HDInsight provides two head nodes.</span></span> <span data-ttu-id="9af08-121">Les deux nœuds principaux sont actifs et s’exécutent simultanément sur le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9af08-121">Both head nodes are active and running within the HDInsight cluster simultaneously.</span></span> <span data-ttu-id="9af08-122">Certains services, par exemple HDFS et YARN, ne sont « actifs » que sur un seul nœud principal à un instant t.</span><span class="sxs-lookup"><span data-stu-id="9af08-122">Some services, such as HDFS or YARN, are only 'active' on one head node at any given time.</span></span> <span data-ttu-id="9af08-123">D'autres services tels que HiveServer2 ou Hive MetaStore sont actifs sur les deux nœuds principaux simultanément.</span><span class="sxs-lookup"><span data-stu-id="9af08-123">Other services such as HiveServer2 or Hive MetaStore are active on both head nodes at the same time.</span></span>

<span data-ttu-id="9af08-124">Les nœuds principaux (et les autres nœuds dans HDInsight) possèdent une valeur numérique comme partie du nom d’hôte du nœud.</span><span class="sxs-lookup"><span data-stu-id="9af08-124">Head nodes (and other nodes in HDInsight) have a numeric value as part of the hostname of the node.</span></span> <span data-ttu-id="9af08-125">Par exemple, `hn0-CLUSTERNAME` ou `hn4-CLUSTERNAME`.</span><span class="sxs-lookup"><span data-stu-id="9af08-125">For example, `hn0-CLUSTERNAME` or `hn4-CLUSTERNAME`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9af08-126">N’associez pas la valeur numérique avec l’information selon laquelle un nœud est principal ou secondaire.</span><span class="sxs-lookup"><span data-stu-id="9af08-126">Do not associate the numeric value with whether a node is primary or secondary.</span></span> <span data-ttu-id="9af08-127">La valeur numérique est uniquement présente afin de fournir un nom unique à chaque nœud.</span><span class="sxs-lookup"><span data-stu-id="9af08-127">The numeric value is only present to provide a unique name for each node.</span></span>

### <a name="nimbus-nodes"></a><span data-ttu-id="9af08-128">Nœuds Nimbus</span><span class="sxs-lookup"><span data-stu-id="9af08-128">Nimbus Nodes</span></span>

<span data-ttu-id="9af08-129">Des nœuds Nimbus sont disponibles avec les clusters Storm.</span><span class="sxs-lookup"><span data-stu-id="9af08-129">Nimbus nodes are available with Storm clusters.</span></span> <span data-ttu-id="9af08-130">Les nœuds Nimbus offrent des fonctionnalités comparables au service Hadoop JobTracker en distribuant et en surveillant le traitement sur l’ensemble des nœuds de travail.</span><span class="sxs-lookup"><span data-stu-id="9af08-130">The Nimbus nodes provide similar functionality to the Hadoop JobTracker by distributing and monitoring processing across worker nodes.</span></span> <span data-ttu-id="9af08-131">HDInsight fournit deux nœuds Nimbus pour les clusters Storm</span><span class="sxs-lookup"><span data-stu-id="9af08-131">HDInsight provides two Nimbus nodes for Storm clusters</span></span>

### <a name="zookeeper-nodes"></a><span data-ttu-id="9af08-132">Nœuds Zookeeper</span><span class="sxs-lookup"><span data-stu-id="9af08-132">Zookeeper nodes</span></span>

<span data-ttu-id="9af08-133">Des nœuds [ZooKeeper](http://zookeeper.apache.org/) sont utilisés pour l’élection de leader des services maîtres sur nœuds principaux.</span><span class="sxs-lookup"><span data-stu-id="9af08-133">[ZooKeeper](http://zookeeper.apache.org/) nodes are used for leader election of master services on head nodes.</span></span> <span data-ttu-id="9af08-134">Ils sont également utilisés pour s’assurer que les services, les nœuds de données (worker) et les passerelles sachent sur quel nœud principal un service maître est actif.</span><span class="sxs-lookup"><span data-stu-id="9af08-134">They are also used to insure that services, data (worker) nodes, and gateways know which head node a master service is active on.</span></span> <span data-ttu-id="9af08-135">Par défaut, HDInsight fournit trois nœuds ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="9af08-135">By default, HDInsight provides three ZooKeeper nodes.</span></span>

### <a name="worker-nodes"></a><span data-ttu-id="9af08-136">Nœuds de travail</span><span class="sxs-lookup"><span data-stu-id="9af08-136">Worker nodes</span></span>

<span data-ttu-id="9af08-137">Les nœuds de travail effectuent l’analyse de données proprement dite lorsqu’un travail est soumis au cluster.</span><span class="sxs-lookup"><span data-stu-id="9af08-137">Worker nodes perform the actual data analysis when a job is submitted to the cluster.</span></span> <span data-ttu-id="9af08-138">En cas de défaillance d’un nœud de travail, la tâche en cours d’exécution sur ce dernier est soumise à un autre nœud de travail.</span><span class="sxs-lookup"><span data-stu-id="9af08-138">If a worker node fails, the task that it was performing is submitted to another worker node.</span></span> <span data-ttu-id="9af08-139">Par défaut, HDInsight crée quatre nœuds de travail.</span><span class="sxs-lookup"><span data-stu-id="9af08-139">By default, HDInsight creates four worker nodes.</span></span> <span data-ttu-id="9af08-140">Vous pouvez modifier ce chiffre en fonction vos besoins, pendant et après la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="9af08-140">You can change this number to suit your needs both during and after cluster creation.</span></span>

### <a name="edge-node"></a><span data-ttu-id="9af08-141">Nœud de périmètre</span><span class="sxs-lookup"><span data-stu-id="9af08-141">Edge node</span></span>

<span data-ttu-id="9af08-142">Un nœud ne participe pas activement à l’analyse de données au sein du cluster.</span><span class="sxs-lookup"><span data-stu-id="9af08-142">An edge node does not actively participate in data analysis within the cluster.</span></span> <span data-ttu-id="9af08-143">Il est utilisé par les développeurs ou chercheurs de données qui travaillent avec Hadoop.</span><span class="sxs-lookup"><span data-stu-id="9af08-143">It is used by developers or data scientists when working with Hadoop.</span></span> <span data-ttu-id="9af08-144">Le nœud de périmètre se trouve dans le même réseau virtuel Azure que les autres nœuds du cluster et peut accéder directement à tous les autres nœuds.</span><span class="sxs-lookup"><span data-stu-id="9af08-144">The edge node lives in the same Azure Virtual Network as the other nodes in the cluster, and can directly access all other nodes.</span></span> <span data-ttu-id="9af08-145">Le nœud Edge peut être utilisé sans qu’il faille recourir à des ressources de services Hadoop ou de tâches d’analyse critiques.</span><span class="sxs-lookup"><span data-stu-id="9af08-145">The edge node can be used without taking resources away from critical Hadoop services or analysis jobs.</span></span>

<span data-ttu-id="9af08-146">Pour l’instant, R Server sur HDInsight est le seul type de cluster à fournir un nœud de périmètre par défaut.</span><span class="sxs-lookup"><span data-stu-id="9af08-146">Currently, R Server on HDInsight is the only cluster type that provides an edge node by default.</span></span> <span data-ttu-id="9af08-147">Dans le cas de R Server sur HDInsight, le nœud de périmètre est utilisé pour tester le code R localement sur le nœud avant de le soumettre au cluster à des fins de traitement distribué.</span><span class="sxs-lookup"><span data-stu-id="9af08-147">For R Server on HDInsight, the edge node is used test R code locally on the node before submitting it to the cluster for distributed processing.</span></span>

<span data-ttu-id="9af08-148">Pour plus d’informations sur l’utilisation d’un nœud de périmètre avec des types de clusters autres que R Server, consultez le document [Utiliser des nœuds de périmètre dans HDInsight](hdinsight-apps-use-edge-node.md).</span><span class="sxs-lookup"><span data-stu-id="9af08-148">For information on using an edge node with cluster types other than R Server, see the [Use edge nodes in HDInsight](hdinsight-apps-use-edge-node.md) document.</span></span>

## <a name="accessing-the-nodes"></a><span data-ttu-id="9af08-149">Accès aux nœuds</span><span class="sxs-lookup"><span data-stu-id="9af08-149">Accessing the nodes</span></span>

<span data-ttu-id="9af08-150">L’accès au cluster par Internet est fourni par le biais d’une passerelle publique.</span><span class="sxs-lookup"><span data-stu-id="9af08-150">Access to the cluster over the internet is provided through a public gateway.</span></span> <span data-ttu-id="9af08-151">L’accès est limité à la connexion aux nœuds principaux et (s’il en existe un) au nœud de périmètre.</span><span class="sxs-lookup"><span data-stu-id="9af08-151">Access is limited to connecting to the head nodes and (if one exists) the edge node.</span></span> <span data-ttu-id="9af08-152">L’accès aux services qui s’exécutent sur les nœuds principaux n’est pas affecté par la présence de plusieurs nœuds principaux.</span><span class="sxs-lookup"><span data-stu-id="9af08-152">Access to services running on the head nodes is not effected by having multiple head nodes.</span></span> <span data-ttu-id="9af08-153">La passerelle publique achemine les demandes vers le nœud principal qui héberge le service demandé.</span><span class="sxs-lookup"><span data-stu-id="9af08-153">The public gateway routes requests to the head node that hosts the requested service.</span></span> <span data-ttu-id="9af08-154">Par exemple, si Ambari est actuellement hébergé sur le nœud principal secondaire, la passerelle achemine les demandes entrantes pour Ambari vers ce nœud.</span><span class="sxs-lookup"><span data-stu-id="9af08-154">For example, if Ambari is currently hosted on the secondary head node, the gateway routes incoming requests for Ambari to that node.</span></span>

<span data-ttu-id="9af08-155">L’accès via la passerelle publique est limité aux ports 443 (HTTPS), 22 et 23.</span><span class="sxs-lookup"><span data-stu-id="9af08-155">Access over the public gateway is limited to port 443 (HTTPS), 22, and 23.</span></span>

* <span data-ttu-id="9af08-156">Le port __443__ permet d’accéder à Ambari et à d’autres interfaces utilisateur web ou API REST hébergées sur les nœuds principaux.</span><span class="sxs-lookup"><span data-stu-id="9af08-156">Port __443__ is used to access Ambari and other web UI or REST APIs hosted on the head nodes.</span></span>

* <span data-ttu-id="9af08-157">Le port __22__ est utilisé pour accéder au nœud principal primaire ou au nœud de périmètre via SSH.</span><span class="sxs-lookup"><span data-stu-id="9af08-157">Port __22__ is used to access the primary head node or edge node with SSH.</span></span>

* <span data-ttu-id="9af08-158">Le port __23__ est utilisé pour accéder au nœud principal secondaire via SSH.</span><span class="sxs-lookup"><span data-stu-id="9af08-158">Port __23__ is used to access the secondary head node with SSH.</span></span> <span data-ttu-id="9af08-159">Par exemple, `ssh username@mycluster-ssh.azurehdinsight.net` établit une connexion au nœud principal primaire du cluster nommé **mycluster**.</span><span class="sxs-lookup"><span data-stu-id="9af08-159">For example, `ssh username@mycluster-ssh.azurehdinsight.net` connects to the primary head node of the cluster named **mycluster**.</span></span>

<span data-ttu-id="9af08-160">Pour plus d’informations sur l’utilisation de SSH, consultez le document [Utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="9af08-160">For more information on using SSH, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

### <a name="internal-fully-qualified-domain-names-fqdn"></a><span data-ttu-id="9af08-161">Noms de domaine pleinement qualifiés internes (FQDN)</span><span class="sxs-lookup"><span data-stu-id="9af08-161">Internal fully qualified domain names (FQDN)</span></span>

<span data-ttu-id="9af08-162">Les nœuds présents dans un cluster HDInsight sont dotés d’une adresse IP interne et d’un nom de domaine complet uniquement accessibles à partir du cluster.</span><span class="sxs-lookup"><span data-stu-id="9af08-162">Nodes in an HDInsight cluster have an internal IP address and FQDN that can only be accessed from the cluster.</span></span> <span data-ttu-id="9af08-163">Lorsque vous accédez à des services sur le cluster à l'aide de l'adresse IP ou du nom de domaine complet interne, vous devez utiliser Ambari pour vérifier l'adresse IP ou le nom de domaine complet à utiliser.</span><span class="sxs-lookup"><span data-stu-id="9af08-163">When accessing services on the cluster using the internal FQDN or IP address, you should use Ambari to verify the IP or FQDN to use when accessing the service.</span></span>

<span data-ttu-id="9af08-164">Par exemple, le service Oozie peut s'exécuter uniquement sur un nœud principal et l'utilisation de la commande `oozie` à partir d'une session SSH requiert l'URL du service.</span><span class="sxs-lookup"><span data-stu-id="9af08-164">For example, the Oozie service can only run on one head node, and using the `oozie` command from an SSH session requires the URL to the service.</span></span> <span data-ttu-id="9af08-165">Cette URL peut être extraite d’Ambari avec la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9af08-165">This URL can be retrieved from Ambari by using the following command:</span></span>

    curl -u admin:PASSWORD "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations?type=oozie-site&tag=TOPOLOGY_RESOLVED" | grep oozie.base.url

<span data-ttu-id="9af08-166">Cette commande renvoie une valeur qui se présente comme la commande suivante, qui contient l’URL interne à utiliser avec la commande `oozie` :</span><span class="sxs-lookup"><span data-stu-id="9af08-166">This command returns a value similar to the following command, which contains the internal URL to use with the `oozie` command:</span></span>

    "oozie.base.url": "http://hn0-CLUSTERNAME-randomcharacters.cx.internal.cloudapp.net:11000/oozie"

<span data-ttu-id="9af08-167">Pour plus d’informations sur l’API REST Ambari, consultez la page [Surveiller et gérer HDInsight avec l’API REST Ambari](hdinsight-hadoop-manage-ambari-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="9af08-167">For more information on working with the Ambari REST API, see [Monitor and Manage HDInsight using the Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md).</span></span>

### <a name="accessing-other-node-types"></a><span data-ttu-id="9af08-168">Accès à d’autres types de nœuds</span><span class="sxs-lookup"><span data-stu-id="9af08-168">Accessing other node types</span></span>

<span data-ttu-id="9af08-169">Vous pouvez vous connecter aux nœuds qui ne sont pas directement accessibles sur Internet en utilisant les méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="9af08-169">You can connect to nodes that are not directly accessible over the internet by using the following methods:</span></span>

* <span data-ttu-id="9af08-170">**SSH** : une fois connecté à un nœud principal au moyen de SSH, vous pouvez utiliser SSH à partir de ce nœud principal pour vous connecter à d’autres nœuds du cluster.</span><span class="sxs-lookup"><span data-stu-id="9af08-170">**SSH**: Once connected to a head node using SSH, you can then use SSH from the head node to connect to other nodes in the cluster.</span></span> <span data-ttu-id="9af08-171">Pour plus d’informations, consultez le document [Utiliser SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="9af08-171">For more information, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

* <span data-ttu-id="9af08-172">**Tunnel SSH** : si vous avez besoin d’accéder à un service web hébergé sur l’un des nœuds qui ne sont pas exposés à Internet, vous devez utiliser un tunnel SSH.</span><span class="sxs-lookup"><span data-stu-id="9af08-172">**SSH Tunnel**: If you need to access a web service hosted on one of the nodes that is not exposed to the internet, you must use an SSH tunnel.</span></span> <span data-ttu-id="9af08-173">Pour plus d’informations, consultez le document [Utiliser un tunnel SSH avec HDInsight](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="9af08-173">For more information, see the [Use an SSH tunnel with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

* <span data-ttu-id="9af08-174">**Réseau virtuel Azure** : si votre cluster HDInsight fait partie intégrante d’un réseau virtuel Azure, toutes les ressources du même réseau virtuel peuvent accéder directement à tous les nœuds du cluster.</span><span class="sxs-lookup"><span data-stu-id="9af08-174">**Azure Virtual Network**: If your HDInsight cluster is part of an Azure Virtual Network, any resource on the same Virtual Network can directly access all nodes in the cluster.</span></span> <span data-ttu-id="9af08-175">Pour plus d’informations, consultez le document [Étendre HDInsight en utilisant un réseau virtuel Azure](hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="9af08-175">For more information, see the [Extend HDInsight using Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span>

## <a name="how-to-check-on-a-service-status"></a><span data-ttu-id="9af08-176">Comment contrôler  l'état d'un service</span><span class="sxs-lookup"><span data-stu-id="9af08-176">How to check on a service status</span></span>

<span data-ttu-id="9af08-177">Pour vérifier l’état des services qui s’exécutent sur les nœuds principaux, utilisez l’interface utilisateur web d’Ambari ou l’API REST Ambari.</span><span class="sxs-lookup"><span data-stu-id="9af08-177">To check the status of services that run on the head nodes, use the Ambari Web UI or the Ambari REST API.</span></span>

### <a name="ambari-web-ui"></a><span data-ttu-id="9af08-178">Interface utilisateur web d'Ambari</span><span class="sxs-lookup"><span data-stu-id="9af08-178">Ambari Web UI</span></span>

<span data-ttu-id="9af08-179">Ouvrez l’interface utilisateur web d’Ambari à l’adresse https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="9af08-179">The Ambari Web UI is viewable at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="9af08-180">Remplacez **CLUSTERNAME** par le nom de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="9af08-180">Replace **CLUSTERNAME** with the name of your cluster.</span></span> <span data-ttu-id="9af08-181">Si vous y êtes invité, saisissez les informations d'identification utilisateur de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="9af08-181">If prompted, enter the HTTP user credentials for your cluster.</span></span> <span data-ttu-id="9af08-182">Le nom d'utilisateur HTTP par défaut est **admin** et le mot de passe est le mot de passe que vous avez saisi lors de la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="9af08-182">The default HTTP user name is **admin** and the password is the password you entered when creating the cluster.</span></span>

<span data-ttu-id="9af08-183">Lorsque vous arrivez sur la page Ambari, les services installés apparaissent à gauche de la page.</span><span class="sxs-lookup"><span data-stu-id="9af08-183">When you arrive on the Ambari page, the installed services are listed on the left of the page.</span></span>

![Services installés](./media/hdinsight-high-availability-linux/services.png)

<span data-ttu-id="9af08-185">Une série d'icônes s'affichent en regard d'un service pour indiquer son état.</span><span class="sxs-lookup"><span data-stu-id="9af08-185">There are a series of icons that may appear next to a service to indicate status.</span></span> <span data-ttu-id="9af08-186">Des alertes liées à un service peuvent être affichées à l'aide du lien **Alertes** situé en haut de la page.</span><span class="sxs-lookup"><span data-stu-id="9af08-186">Any alerts related to a service can be viewed using the **Alerts** link at the top of the page.</span></span> <span data-ttu-id="9af08-187">Vous pouvez sélectionner chaque service pour afficher plus d'informations sur ce dernier.</span><span class="sxs-lookup"><span data-stu-id="9af08-187">You can select each service to view more information on it.</span></span>

<span data-ttu-id="9af08-188">La page de service fournit des informations sur l'état et la configuration de chaque service. Il ne fournit pas d'informations sur le nœud principal sur lequel le service s'exécute.</span><span class="sxs-lookup"><span data-stu-id="9af08-188">While the service page provides information on the status and configuration of each service, it does not provide information on which head node the service is running on.</span></span> <span data-ttu-id="9af08-189">Pour afficher ces informations, utilisez le lien **Hôtes** en haut de la page.</span><span class="sxs-lookup"><span data-stu-id="9af08-189">To view this information, use the **Hosts** link at the top of the page.</span></span> <span data-ttu-id="9af08-190">Cette page affiche les hôtes au sein du cluster, notamment les nœuds principaux.</span><span class="sxs-lookup"><span data-stu-id="9af08-190">This page displays hosts within the cluster, including the head nodes.</span></span>

![liste des hôtes](./media/hdinsight-high-availability-linux/hosts.png)

<span data-ttu-id="9af08-192">Sélectionner le lien de l’un des nœuds principaux permet d’afficher les services et les composants qui s’exécutent sur ce nœud.</span><span class="sxs-lookup"><span data-stu-id="9af08-192">Selecting the link for one of the head nodes displays the services and components running on that node.</span></span>

![État du composant](./media/hdinsight-high-availability-linux/nodeservices.png)

<span data-ttu-id="9af08-194">Pour plus d’informations sur Ambari, consultez la page [Surveiller et gérer HDInsight avec l’interface utilisateur web d’Ambari](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="9af08-194">For more information on using Ambari, see [Monitor and manage HDInsight using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

### <a name="ambari-rest-api"></a><span data-ttu-id="9af08-195">API Ambari REST</span><span class="sxs-lookup"><span data-stu-id="9af08-195">Ambari REST API</span></span>

<span data-ttu-id="9af08-196">L’API REST Ambari est disponible sur internet.</span><span class="sxs-lookup"><span data-stu-id="9af08-196">The Ambari REST API is available over the internet.</span></span> <span data-ttu-id="9af08-197">La passerelle publique HDInsight gère l’acheminement des demandes vers le nœud principal hébergeant l’API REST.</span><span class="sxs-lookup"><span data-stu-id="9af08-197">The HDInsight public gateway handles routing requests to the head node that is currently hosting the REST API.</span></span>

<span data-ttu-id="9af08-198">Vous pouvez utiliser la commande suivante pour vérifier l'état d'un service via l'API REST Ambari :</span><span class="sxs-lookup"><span data-stu-id="9af08-198">You can use the following command to check the state of a service through the Ambari REST API:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICENAME?fields=ServiceInfo/state

* <span data-ttu-id="9af08-199">Remplacez **PASSWORD** par le mot de passe du compte d’utilisateur HTTP (admin).</span><span class="sxs-lookup"><span data-stu-id="9af08-199">Replace **PASSWORD** with the HTTP user (admin) account password.</span></span>
* <span data-ttu-id="9af08-200">Remplacez **CLUSTERNAME** par le nom de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="9af08-200">Replace **CLUSTERNAME** with the name of the cluster.</span></span>
* <span data-ttu-id="9af08-201">Remplacez **SERVICENAME** par le nom du service dont vous voulez contrôler l’état.</span><span class="sxs-lookup"><span data-stu-id="9af08-201">Replace **SERVICENAME** with the name of the service you want to check the status of.</span></span>

<span data-ttu-id="9af08-202">Par exemple, pour vérifier l’état du service **HDFS** dans un cluster nommé **mycluster**, avec un mot de passe **password**, vous devez utiliser la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9af08-202">For example, to check the status of the **HDFS** service on a cluster named **mycluster**, with a password of **password**, you would use the following command:</span></span>

    curl -u admin:password https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state

<span data-ttu-id="9af08-203">La réponse se présente comme le JSON suivant :</span><span class="sxs-lookup"><span data-stu-id="9af08-203">The response is similar to the following JSON:</span></span>

    {
      "href" : "http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8080/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state",
      "ServiceInfo" : {
        "cluster_name" : "mycluster",
        "service_name" : "HDFS",
        "state" : "STARTED"
      }
    }

<span data-ttu-id="9af08-204">L’URL indique que le service est en cours d’exécution sur un nœud principal nommé **hn0-CLUSTERNAME**.</span><span class="sxs-lookup"><span data-stu-id="9af08-204">The URL tells us that the service is currently running on a head node named **hn0-CLUSTERNAME**.</span></span>

<span data-ttu-id="9af08-205">L'URL indique que le service est en cours d'exécution ou **démarré**.</span><span class="sxs-lookup"><span data-stu-id="9af08-205">The state tells us that the service is currently running, or **STARTED**.</span></span>

<span data-ttu-id="9af08-206">Si vous ne connaissez pas les services installés sur le cluster, vous pouvez utiliser la commande suivante pour en récupérer la liste :</span><span class="sxs-lookup"><span data-stu-id="9af08-206">If you do not know what services are installed on the cluster, you can use the following command to retrieve a list:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services

<span data-ttu-id="9af08-207">Pour plus d’informations sur l’API REST Ambari, consultez la page [Surveiller et gérer HDInsight avec l’API REST Ambari](hdinsight-hadoop-manage-ambari-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="9af08-207">For more information on working with the Ambari REST API, see [Monitor and Manage HDInsight using the Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md).</span></span>

#### <a name="service-components"></a><span data-ttu-id="9af08-208">Composants du service</span><span class="sxs-lookup"><span data-stu-id="9af08-208">Service components</span></span>

<span data-ttu-id="9af08-209">Les services peuvent contenir des composants dont vous souhaitez vérifier l'état individuellement.</span><span class="sxs-lookup"><span data-stu-id="9af08-209">Services may contain components that you wish to check the status of individually.</span></span> <span data-ttu-id="9af08-210">Par exemple, HDFS contient le composant NameNode.</span><span class="sxs-lookup"><span data-stu-id="9af08-210">For example, HDFS contains the NameNode component.</span></span> <span data-ttu-id="9af08-211">Pour afficher des informations relatives à un composant, la commande serait :</span><span class="sxs-lookup"><span data-stu-id="9af08-211">To view information on a component, the command would be:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

<span data-ttu-id="9af08-212">Si vous ne connaissez pas les composants fournis par un service, vous pouvez utiliser la commande suivante pour en récupérer la liste :</span><span class="sxs-lookup"><span data-stu-id="9af08-212">If you do not know what components are provided by a service, you can use the following command to retrieve a list:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

## <a name="how-to-access-log-files-on-the-head-nodes"></a><span data-ttu-id="9af08-213">Accès aux fichiers journaux sur les nœuds principaux</span><span class="sxs-lookup"><span data-stu-id="9af08-213">How to access log files on the head nodes</span></span>

### <a name="ssh"></a><span data-ttu-id="9af08-214">SSH</span><span class="sxs-lookup"><span data-stu-id="9af08-214">SSH</span></span>

<span data-ttu-id="9af08-215">Lorsque vous êtes connecté à un nœud principal via SSH, les fichiers journaux se trouvent sous **/var/log**.</span><span class="sxs-lookup"><span data-stu-id="9af08-215">While connected to a head node through SSH, log files can be found under **/var/log**.</span></span> <span data-ttu-id="9af08-216">Par exemple, **/var/log/hadoop-yarn/yarn** contiennent les journaux correspondant à YARN.</span><span class="sxs-lookup"><span data-stu-id="9af08-216">For example, **/var/log/hadoop-yarn/yarn** contain logs for YARN.</span></span>

<span data-ttu-id="9af08-217">Chaque nœud principal peut contenir des entrées de journal uniques. Vous devez donc vérifier les journaux correspondant aux deux.</span><span class="sxs-lookup"><span data-stu-id="9af08-217">Each head node can have unique log entries, so you should check the logs on both.</span></span>

### <a name="sftp"></a><span data-ttu-id="9af08-218">SFTP</span><span class="sxs-lookup"><span data-stu-id="9af08-218">SFTP</span></span>

<span data-ttu-id="9af08-219">Vous pouvez également vous connecter au nœud principal à l’aide du protocole FTP SSH, ou protocole FTP sécurisé (SFTP), et télécharger directement les fichiers journaux.</span><span class="sxs-lookup"><span data-stu-id="9af08-219">You can also connect to the head node using the SSH File Transfer Protocol or Secure File Transfer Protocol (SFTP), and download the log files directly.</span></span>

<span data-ttu-id="9af08-220">Comme lors de l’utilisation d’un client SSH, lorsque vous vous connectez au cluster, vous devez fournir le nom du compte d’utilisateur SSH et l’adresse SSH du cluster.</span><span class="sxs-lookup"><span data-stu-id="9af08-220">Similar to using an SSH client, when connecting to the cluster you must provide the SSH user account name and the SSH address of the cluster.</span></span> <span data-ttu-id="9af08-221">Par exemple, `sftp username@mycluster-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="9af08-221">For example, `sftp username@mycluster-ssh.azurehdinsight.net`.</span></span> <span data-ttu-id="9af08-222">Lorsque vous y êtes invité, fournissez le mot de passe du compte ou une clé publique à l’aide du paramètre `-i`.</span><span class="sxs-lookup"><span data-stu-id="9af08-222">Provide the password for the account when prompted, or provide a public key using the `-i` parameter.</span></span>

<span data-ttu-id="9af08-223">Une fois connecté, vous voyez apparaître une invite `sftp>` .</span><span class="sxs-lookup"><span data-stu-id="9af08-223">Once connected, you are presented with a `sftp>` prompt.</span></span> <span data-ttu-id="9af08-224">À partir de cette invite, vous pouvez changer de répertoire, ainsi que charger et télécharger des fichiers.</span><span class="sxs-lookup"><span data-stu-id="9af08-224">From this prompt, you can change directories, upload, and download files.</span></span> <span data-ttu-id="9af08-225">Par exemple, les commandes ci-après activent le répertoire **/var/log/hadoop/hdfs** , puis téléchargent tous les fichiers dans ce répertoire.</span><span class="sxs-lookup"><span data-stu-id="9af08-225">For example, the following commands change directories to the **/var/log/hadoop/hdfs** directory and then download all files in the directory.</span></span>

    cd /var/log/hadoop/hdfs
    get *

<span data-ttu-id="9af08-226">Pour obtenir la liste des commandes disponibles, entrez `help` au niveau de l’invite `sftp>`.</span><span class="sxs-lookup"><span data-stu-id="9af08-226">For a list of available commands, enter `help` at the `sftp>` prompt.</span></span>

> [!NOTE]
> <span data-ttu-id="9af08-227">Il existe également des interfaces graphiques qui vous permettent de visualiser le système de fichiers lorsque vous êtes connecté à l’aide du protocole SFTP.</span><span class="sxs-lookup"><span data-stu-id="9af08-227">There are also graphical interfaces that allow you to visualize the file system when connected using SFTP.</span></span> <span data-ttu-id="9af08-228">Par exemple, [MobaXTerm](http://mobaxterm.mobatek.net/) vous offre la possibilité de parcourir le système de fichiers au moyen d’une interface semblable à l’Explorateur Windows.</span><span class="sxs-lookup"><span data-stu-id="9af08-228">For example, [MobaXTerm](http://mobaxterm.mobatek.net/) allows you to browse the file system using an interface similar to Windows Explorer.</span></span>

### <a name="ambari"></a><span data-ttu-id="9af08-229">Ambari</span><span class="sxs-lookup"><span data-stu-id="9af08-229">Ambari</span></span>

> [!NOTE]
> <span data-ttu-id="9af08-230">Pour accéder aux fichiers journaux avec Ambari, vous devez utiliser un tunnel SSH.</span><span class="sxs-lookup"><span data-stu-id="9af08-230">To access log files using Ambari, you must use an SSH tunnel.</span></span> <span data-ttu-id="9af08-231">Les interfaces web des différents services ne sont pas exposée publiquement sur Internet.</span><span class="sxs-lookup"><span data-stu-id="9af08-231">The web interfaces for the individual services are not exposed publicly on the Internet.</span></span> <span data-ttu-id="9af08-232">Pour plus d’informations sur l’utilisation du tunnel SSH, voir le document [Utilisation d’un Tunneling SSH](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="9af08-232">For information on using an SSH tunnel, see the [Use SSH Tunneling](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

<span data-ttu-id="9af08-233">Dans l’interface utilisateur web d’Ambari, sélectionnez le service dont vous souhaitez afficher les journaux (par exemple, YARN).</span><span class="sxs-lookup"><span data-stu-id="9af08-233">From the Ambari Web UI, select the service you wish to view logs for (for example, YARN).</span></span> <span data-ttu-id="9af08-234">Utilisez ensuite les **liens rapides** pour sélectionner le nœud principal pour lequel vous souhaitez afficher les journaux.</span><span class="sxs-lookup"><span data-stu-id="9af08-234">Then use **Quick Links** to select which head node to view the logs for.</span></span>

![Utilisation des liens rapides pour afficher les journaux](./media/hdinsight-high-availability-linux/viewlogs.png)

## <a name="how-to-configure-the-node-size"></a><span data-ttu-id="9af08-236">Configuration de la taille des nœuds</span><span class="sxs-lookup"><span data-stu-id="9af08-236">How to configure the node size</span></span>

<span data-ttu-id="9af08-237">La taille d’un nœud n’est sélectionnable que lors de la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="9af08-237">The size of a node can only be selected during cluster creation.</span></span> <span data-ttu-id="9af08-238">Pour obtenir la liste des différentes tailles de machine virtuelle disponibles pour HDInsight, voir la page [Tarification de HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="9af08-238">You can find a list of the different VM sizes available for HDInsight on the [HDInsight pricing page](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

<span data-ttu-id="9af08-239">Lorsque vous créez un cluster, vous pouvez spécifier la taille des nœuds.</span><span class="sxs-lookup"><span data-stu-id="9af08-239">When creating a cluster, you can specify the size of the nodes.</span></span> <span data-ttu-id="9af08-240">Les informations suivantes aident à spécifier la taille avec le [Portail Azure][preview-portal], [Azure PowerShell][azure-powershell] et [l’interface de ligne de commande Azure][azure-cli] :</span><span class="sxs-lookup"><span data-stu-id="9af08-240">The following information provides guidance on how to specify the size using the [Azure portal][preview-portal], [Azure PowerShell][azure-powershell], and the [Azure CLI][azure-cli]:</span></span>

* <span data-ttu-id="9af08-241">**Portail Azure** : à la création d’un cluster, vous pouvez définir la taille des nœuds utilisés par le cluster :</span><span class="sxs-lookup"><span data-stu-id="9af08-241">**Azure portal**: When creating a cluster, you can set the size of the nodes used by the cluster:</span></span>

    ![Image de l'Assistant de création de cluster avec sélection de taille de nœud](./media/hdinsight-high-availability-linux/headnodesize.png)

* <span data-ttu-id="9af08-243">**Interface de ligne de commande Azure** : lorsque vous utilisez la commande `azure hdinsight cluster create`, vous pouvez définir la taille des nœuds principaux, de travail et ZooKeeper en utilisant les paramètres `--headNodeSize`, `--workerNodeSize` et `--zookeeperNodeSize`.</span><span class="sxs-lookup"><span data-stu-id="9af08-243">**Azure CLI**: When using the `azure hdinsight cluster create` command, you can set the size of the head, worker, and ZooKeeper nodes by using the `--headNodeSize`, `--workerNodeSize`, and `--zookeeperNodeSize` parameters.</span></span>

* <span data-ttu-id="9af08-244">**Azure PowerShell** : lorsque vous utilisez l’applet de commande `New-AzureRmHDInsightCluster`, vous pouvez définir la taille des nœuds principaux, de travail et ZooKeeper en utilisant les paramètres `-HeadNodeVMSize`, `-WorkerNodeSize` et `-ZookeeperNodeSize`.</span><span class="sxs-lookup"><span data-stu-id="9af08-244">**Azure PowerShell**: When using the `New-AzureRmHDInsightCluster` cmdlet, you can set the size of the head, worker, and ZooKeeper nodes by using the `-HeadNodeVMSize`, `-WorkerNodeSize`, and `-ZookeeperNodeSize` parameters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9af08-245">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9af08-245">Next steps</span></span>

<span data-ttu-id="9af08-246">Utilisez les liens suivants pour en savoir plus sur les éléments mentionnés dans ce document.</span><span class="sxs-lookup"><span data-stu-id="9af08-246">Use the following links to learn more about things mentioned in this document.</span></span>

* [<span data-ttu-id="9af08-247">Référence REST Ambari</span><span class="sxs-lookup"><span data-stu-id="9af08-247">Ambari REST Reference</span></span>](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)
* [<span data-ttu-id="9af08-248">Installation et configuration Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9af08-248">Install and configure the Azure CLI</span></span>](../cli-install-nodejs.md)
* [<span data-ttu-id="9af08-249">Installation et configuration d'Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9af08-249">Install and configure Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="9af08-250">Gestion de HDInsight à l'aide d'Ambari</span><span class="sxs-lookup"><span data-stu-id="9af08-250">Manage HDInsight using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)
* [<span data-ttu-id="9af08-251">Approvisionnement de clusters HDInsight sous Linux</span><span class="sxs-lookup"><span data-stu-id="9af08-251">Provision Linux-based HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)

[preview-portal]: https://portal.azure.com/
[azure-powershell]: /powershell/azureps-cmdlets-docs
[azure-cli]: ../cli-install-nodejs.md
