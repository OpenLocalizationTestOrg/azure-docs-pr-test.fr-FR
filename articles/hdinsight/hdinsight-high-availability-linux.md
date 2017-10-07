---
title: "disponibilité aaaHigh de Hadoop - Azure HDInsight | Documents Microsoft"
description: "Découvrez comment les clusters HDInsight améliorent la fiabilité et la disponibilité en utilisant un nœud principal supplémentaire. Apprenez comment cela a un impact sur les services Hadoop tels que Ambari et Hive, ainsi que comment tooindividually connecter tooeach de nœud principal à l’aide de SSH."
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
ms.openlocfilehash: 9ff62afe6b63b241cb984225233157219f8d7411
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-reliability-of-hadoop-clusters-in-hdinsight"></a><span data-ttu-id="22748-105">Disponibilité et fiabilité des clusters Hadoop dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="22748-105">Availability and reliability of Hadoop clusters in HDInsight</span></span>

<span data-ttu-id="22748-106">Clusters HDInsight fournissent deux disponibilité de nœuds principaux tooincrease hello et la fiabilité des services Hadoop et des travaux en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="22748-106">HDInsight clusters provide two head nodes tooincrease hello availability and reliability of Hadoop services and jobs running.</span></span>

<span data-ttu-id="22748-107">Hadoop garantit de hauts niveaux de disponibilité et de fiabilité en répliquant des services et données sur plusieurs nœuds d’un cluster.</span><span class="sxs-lookup"><span data-stu-id="22748-107">Hadoop achieves high availability and reliability by replicating services and data across multiple nodes in a cluster.</span></span> <span data-ttu-id="22748-108">Toutefois, les distributions standard de Hadoop ne comportent généralement qu’un seul nœud principal.</span><span class="sxs-lookup"><span data-stu-id="22748-108">However standard distributions of Hadoop typically have only a single head node.</span></span> <span data-ttu-id="22748-109">Toute coupure de courant de nœud principal de hello unique peut entraîner l’utilisation de toostop hello cluster.</span><span class="sxs-lookup"><span data-stu-id="22748-109">Any outage of hello single head node can cause hello cluster toostop working.</span></span> <span data-ttu-id="22748-110">HDInsight fournit la disponibilité et la fiabilité de Hadoop deux headnodes tooimprove.</span><span class="sxs-lookup"><span data-stu-id="22748-110">HDInsight provides two headnodes tooimprove Hadoop's availability and reliability.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="22748-111">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="22748-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="22748-112">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="22748-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="availability-and-reliability-of-nodes"></a><span data-ttu-id="22748-113">Disponibilité et fiabilité des nœuds</span><span class="sxs-lookup"><span data-stu-id="22748-113">Availability and reliability of nodes</span></span>

<span data-ttu-id="22748-114">Les nœuds d’un cluster HDInsight sont implémentés à l’aide de machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="22748-114">Nodes in an HDInsight cluster are implemented using Azure Virtual Machines.</span></span> <span data-ttu-id="22748-115">Hello sections suivantes abordent les types de nœud individuel hello utilisés avec HDInsight.</span><span class="sxs-lookup"><span data-stu-id="22748-115">hello following sections discuss hello individual node types used with HDInsight.</span></span> 

> [!NOTE]
> <span data-ttu-id="22748-116">Les types de nœuds utilisables varient selon le type de cluster concerné.</span><span class="sxs-lookup"><span data-stu-id="22748-116">Not all node types are used for a cluster type.</span></span> <span data-ttu-id="22748-117">Par exemple, un type de cluster Hadoop ne comporte aucun nœud Nimbus.</span><span class="sxs-lookup"><span data-stu-id="22748-117">For example, a Hadoop cluster type does not have any Nimbus nodes.</span></span> <span data-ttu-id="22748-118">Pour plus d’informations sur les nœuds utilisés par les types de cluster HDInsight, consultez la section de types de Cluster de hello Hello [Hadoop basé sur Linux de créer des clusters dans HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) document.</span><span class="sxs-lookup"><span data-stu-id="22748-118">For more information on nodes used by HDInsight cluster types, see hello Cluster types section of hello [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) document.</span></span>

### <a name="head-nodes"></a><span data-ttu-id="22748-119">Nœuds principaux</span><span class="sxs-lookup"><span data-stu-id="22748-119">Head nodes</span></span>

<span data-ttu-id="22748-120">tooensure haute disponibilité des services Hadoop, HDInsight fournit deux nœuds principaux.</span><span class="sxs-lookup"><span data-stu-id="22748-120">tooensure high availability of Hadoop services, HDInsight provides two head nodes.</span></span> <span data-ttu-id="22748-121">Les deux nœuds principaux sont actifs et en cours d’exécution dans le cluster HDInsight de hello simultanément.</span><span class="sxs-lookup"><span data-stu-id="22748-121">Both head nodes are active and running within hello HDInsight cluster simultaneously.</span></span> <span data-ttu-id="22748-122">Certains services, par exemple HDFS et YARN, ne sont « actifs » que sur un seul nœud principal à un instant t.</span><span class="sxs-lookup"><span data-stu-id="22748-122">Some services, such as HDFS or YARN, are only 'active' on one head node at any given time.</span></span> <span data-ttu-id="22748-123">Autres services tels que HiveServer2 ou le magasin de métadonnées Hive sont actifs sur les deux nœuds principal hello même temps.</span><span class="sxs-lookup"><span data-stu-id="22748-123">Other services such as HiveServer2 or Hive MetaStore are active on both head nodes at hello same time.</span></span>

<span data-ttu-id="22748-124">Les nœuds principaux (et autres nœuds dans HDInsight) ont une valeur numérique en tant que partie du nom d’hôte hello du nœud de hello.</span><span class="sxs-lookup"><span data-stu-id="22748-124">Head nodes (and other nodes in HDInsight) have a numeric value as part of hello hostname of hello node.</span></span> <span data-ttu-id="22748-125">Par exemple, `hn0-CLUSTERNAME` ou `hn4-CLUSTERNAME`.</span><span class="sxs-lookup"><span data-stu-id="22748-125">For example, `hn0-CLUSTERNAME` or `hn4-CLUSTERNAME`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="22748-126">N’associez pas de valeur numérique de hello indique si un nœud est principal ou secondaire.</span><span class="sxs-lookup"><span data-stu-id="22748-126">Do not associate hello numeric value with whether a node is primary or secondary.</span></span> <span data-ttu-id="22748-127">valeur numérique de Hello est uniquement présent tooprovide un nom unique pour chaque nœud.</span><span class="sxs-lookup"><span data-stu-id="22748-127">hello numeric value is only present tooprovide a unique name for each node.</span></span>

### <a name="nimbus-nodes"></a><span data-ttu-id="22748-128">Nœuds Nimbus</span><span class="sxs-lookup"><span data-stu-id="22748-128">Nimbus Nodes</span></span>

<span data-ttu-id="22748-129">Des nœuds Nimbus sont disponibles avec les clusters Storm.</span><span class="sxs-lookup"><span data-stu-id="22748-129">Nimbus nodes are available with Storm clusters.</span></span> <span data-ttu-id="22748-130">nœuds de Nimbus Hello fournissent toohello fonctionnalités similaires Hadoop JobTracker par la distribution et le traitement d’analyse sur les nœuds de travail.</span><span class="sxs-lookup"><span data-stu-id="22748-130">hello Nimbus nodes provide similar functionality toohello Hadoop JobTracker by distributing and monitoring processing across worker nodes.</span></span> <span data-ttu-id="22748-131">HDInsight fournit deux nœuds Nimbus pour les clusters Storm</span><span class="sxs-lookup"><span data-stu-id="22748-131">HDInsight provides two Nimbus nodes for Storm clusters</span></span>

### <a name="zookeeper-nodes"></a><span data-ttu-id="22748-132">Nœuds Zookeeper</span><span class="sxs-lookup"><span data-stu-id="22748-132">Zookeeper nodes</span></span>

<span data-ttu-id="22748-133">Des nœuds [ZooKeeper](http://zookeeper.apache.org/) sont utilisés pour l’élection de leader des services maîtres sur nœuds principaux.</span><span class="sxs-lookup"><span data-stu-id="22748-133">[ZooKeeper](http://zookeeper.apache.org/) nodes are used for leader election of master services on head nodes.</span></span> <span data-ttu-id="22748-134">Ils sont également utilisé tooinsure que les services, les nœuds de données (traitement) et les passerelles connaissent le nœud principal, un service principal est actif sur.</span><span class="sxs-lookup"><span data-stu-id="22748-134">They are also used tooinsure that services, data (worker) nodes, and gateways know which head node a master service is active on.</span></span> <span data-ttu-id="22748-135">Par défaut, HDInsight fournit trois nœuds ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="22748-135">By default, HDInsight provides three ZooKeeper nodes.</span></span>

### <a name="worker-nodes"></a><span data-ttu-id="22748-136">Nœuds de travail</span><span class="sxs-lookup"><span data-stu-id="22748-136">Worker nodes</span></span>

<span data-ttu-id="22748-137">Nœuds de travail effectuent une analyse de données réelles hello lorsqu’une tâche est soumis toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="22748-137">Worker nodes perform hello actual data analysis when a job is submitted toohello cluster.</span></span> <span data-ttu-id="22748-138">Si un nœud de travail échoue, la tâche hello elle effectuait est nœud de travail tooanother soumis.</span><span class="sxs-lookup"><span data-stu-id="22748-138">If a worker node fails, hello task that it was performing is submitted tooanother worker node.</span></span> <span data-ttu-id="22748-139">Par défaut, HDInsight crée quatre nœuds de travail.</span><span class="sxs-lookup"><span data-stu-id="22748-139">By default, HDInsight creates four worker nodes.</span></span> <span data-ttu-id="22748-140">Vous pouvez modifier ce nombre toosuit à vos besoins pendant et après la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="22748-140">You can change this number toosuit your needs both during and after cluster creation.</span></span>

### <a name="edge-node"></a><span data-ttu-id="22748-141">Nœud de périmètre</span><span class="sxs-lookup"><span data-stu-id="22748-141">Edge node</span></span>

<span data-ttu-id="22748-142">Un nœud ne participe pas activement à dans l’analyse des données au sein du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="22748-142">An edge node does not actively participate in data analysis within hello cluster.</span></span> <span data-ttu-id="22748-143">Il est utilisé par les développeurs ou chercheurs de données qui travaillent avec Hadoop.</span><span class="sxs-lookup"><span data-stu-id="22748-143">It is used by developers or data scientists when working with Hadoop.</span></span> <span data-ttu-id="22748-144">qualité de vie du nœud Hello edge dans hello même réseau virtuel Azure comme hello autres nœuds de cluster de hello et peut accéder directement à tous les autres nœuds.</span><span class="sxs-lookup"><span data-stu-id="22748-144">hello edge node lives in hello same Azure Virtual Network as hello other nodes in hello cluster, and can directly access all other nodes.</span></span> <span data-ttu-id="22748-145">nœud de bord de Hello peut être utilisé sans mettre les ressources en s’éloignant de services Hadoop critiques ou des tâches d’analyse.</span><span class="sxs-lookup"><span data-stu-id="22748-145">hello edge node can be used without taking resources away from critical Hadoop services or analysis jobs.</span></span>

<span data-ttu-id="22748-146">Actuellement, le serveur R HDInsight est hello seul cluster type qui fournit un nœud par défaut.</span><span class="sxs-lookup"><span data-stu-id="22748-146">Currently, R Server on HDInsight is hello only cluster type that provides an edge node by default.</span></span> <span data-ttu-id="22748-147">Pour R Server sur HDInsight, nœud de périmètre hello est utilisé code de test R localement sur le nœud hello avant de le soumettre cluster toohello pour le traitement distribué.</span><span class="sxs-lookup"><span data-stu-id="22748-147">For R Server on HDInsight, hello edge node is used test R code locally on hello node before submitting it toohello cluster for distributed processing.</span></span>

<span data-ttu-id="22748-148">Pour plus d’informations sur l’utilisation d’un nœud avec les types de clusters autre que R Server, consultez hello [utiliser noeuds dans HDInsight](hdinsight-apps-use-edge-node.md) document.</span><span class="sxs-lookup"><span data-stu-id="22748-148">For information on using an edge node with cluster types other than R Server, see hello [Use edge nodes in HDInsight](hdinsight-apps-use-edge-node.md) document.</span></span>

## <a name="accessing-hello-nodes"></a><span data-ttu-id="22748-149">L’accès aux nœuds de hello</span><span class="sxs-lookup"><span data-stu-id="22748-149">Accessing hello nodes</span></span>

<span data-ttu-id="22748-150">Cluster d’accès toohello sur hello internet est fournie via une passerelle publique.</span><span class="sxs-lookup"><span data-stu-id="22748-150">Access toohello cluster over hello internet is provided through a public gateway.</span></span> <span data-ttu-id="22748-151">L’accès est limité tooconnecting nœuds principaux de toohello et (si elle existe) hello nœud de périmètre.</span><span class="sxs-lookup"><span data-stu-id="22748-151">Access is limited tooconnecting toohello head nodes and (if one exists) hello edge node.</span></span> <span data-ttu-id="22748-152">Tooservices d’accès en cours d’exécution sur les nœuds principal hello n’est pas concerné en demandant à plusieurs nœuds principal.</span><span class="sxs-lookup"><span data-stu-id="22748-152">Access tooservices running on hello head nodes is not effected by having multiple head nodes.</span></span> <span data-ttu-id="22748-153">Hello passerelle publique itinéraires demandes toohello nœud principal qui héberge hello le service demandé.</span><span class="sxs-lookup"><span data-stu-id="22748-153">hello public gateway routes requests toohello head node that hosts hello requested service.</span></span> <span data-ttu-id="22748-154">Par exemple, si Ambari est actuellement hébergé sur le nœud principal de hello secondaire, la passerelle de hello route les demandes entrantes pour le nœud de toothat Ambari.</span><span class="sxs-lookup"><span data-stu-id="22748-154">For example, if Ambari is currently hosted on hello secondary head node, hello gateway routes incoming requests for Ambari toothat node.</span></span>

<span data-ttu-id="22748-155">L’accès via la passerelle de public hello est limitée tooport 443 (HTTPS), 22 et 23.</span><span class="sxs-lookup"><span data-stu-id="22748-155">Access over hello public gateway is limited tooport 443 (HTTPS), 22, and 23.</span></span>

* <span data-ttu-id="22748-156">Port __443__ est utilisé tooaccess Ambari et autres web l’interface utilisateur ou des API REST hébergée sur les nœuds principaux hello.</span><span class="sxs-lookup"><span data-stu-id="22748-156">Port __443__ is used tooaccess Ambari and other web UI or REST APIs hosted on hello head nodes.</span></span>

* <span data-ttu-id="22748-157">Port __22__ est le nœud principal de tooaccess utilisé hello principal ou un nœud de bord avec SSH.</span><span class="sxs-lookup"><span data-stu-id="22748-157">Port __22__ is used tooaccess hello primary head node or edge node with SSH.</span></span>

* <span data-ttu-id="22748-158">Port __23__ est utilisé tooaccess hello secondaire nœud principal avec SSH.</span><span class="sxs-lookup"><span data-stu-id="22748-158">Port __23__ is used tooaccess hello secondary head node with SSH.</span></span> <span data-ttu-id="22748-159">Par exemple, `ssh username@mycluster-ssh.azurehdinsight.net` se connecte toohello principal nœud de tête hello cluster nommé **mycluster**.</span><span class="sxs-lookup"><span data-stu-id="22748-159">For example, `ssh username@mycluster-ssh.azurehdinsight.net` connects toohello primary head node of hello cluster named **mycluster**.</span></span>

<span data-ttu-id="22748-160">Pour plus d’informations sur l’utilisation de SSH, consultez hello [utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span><span class="sxs-lookup"><span data-stu-id="22748-160">For more information on using SSH, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

### <a name="internal-fully-qualified-domain-names-fqdn"></a><span data-ttu-id="22748-161">Noms de domaine pleinement qualifiés internes (FQDN)</span><span class="sxs-lookup"><span data-stu-id="22748-161">Internal fully qualified domain names (FQDN)</span></span>

<span data-ttu-id="22748-162">Nœuds dans un cluster HDInsight ont une adresse IP et le nom de domaine complet qui est accessible à partir du cluster de hello interne.</span><span class="sxs-lookup"><span data-stu-id="22748-162">Nodes in an HDInsight cluster have an internal IP address and FQDN that can only be accessed from hello cluster.</span></span> <span data-ttu-id="22748-163">Lors de l’accès aux services sur le cluster hello à l’aide de hello interne nom de domaine complet ou l’adresse IP, vous devez utiliser Ambari tooverify hello IP ou nom de domaine complet toouse lorsque vous accédez hello service.</span><span class="sxs-lookup"><span data-stu-id="22748-163">When accessing services on hello cluster using hello internal FQDN or IP address, you should use Ambari tooverify hello IP or FQDN toouse when accessing hello service.</span></span>

<span data-ttu-id="22748-164">Par exemple, hello Oozie service peut s’exécuter uniquement sur un seul nœud principal et à l’aide de hello `oozie` commande à partir d’une session SSH requiert le service de toohello URL hello.</span><span class="sxs-lookup"><span data-stu-id="22748-164">For example, hello Oozie service can only run on one head node, and using hello `oozie` command from an SSH session requires hello URL toohello service.</span></span> <span data-ttu-id="22748-165">Cette URL peut être récupérée à partir de Ambari à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="22748-165">This URL can be retrieved from Ambari by using hello following command:</span></span>

    curl -u admin:PASSWORD "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations?type=oozie-site&tag=TOPOLOGY_RESOLVED" | grep oozie.base.url

<span data-ttu-id="22748-166">Cette commande retourne un toohello similaire valeur suivant la commande, qui contient les toouse URL interne hello avec hello `oozie` commande :</span><span class="sxs-lookup"><span data-stu-id="22748-166">This command returns a value similar toohello following command, which contains hello internal URL toouse with hello `oozie` command:</span></span>

    "oozie.base.url": "http://hn0-CLUSTERNAME-randomcharacters.cx.internal.cloudapp.net:11000/oozie"

<span data-ttu-id="22748-167">Pour plus d’informations sur l’utilisation des API REST de Ambari de hello, consultez [surveiller et gérer HDInsight, à l’aide de hello API REST de Ambari](hdinsight-hadoop-manage-ambari-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="22748-167">For more information on working with hello Ambari REST API, see [Monitor and Manage HDInsight using hello Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md).</span></span>

### <a name="accessing-other-node-types"></a><span data-ttu-id="22748-168">Accès à d’autres types de nœuds</span><span class="sxs-lookup"><span data-stu-id="22748-168">Accessing other node types</span></span>

<span data-ttu-id="22748-169">Vous pouvez vous connecter toonodes pas directement accessibles sur hello internet à l’aide des méthodes suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="22748-169">You can connect toonodes that are not directly accessible over hello internet by using hello following methods:</span></span>

* <span data-ttu-id="22748-170">**SSH**: une fois connecté tooa du nœud principal à l’aide de SSH, vous pouvez ensuite utiliser SSH à partir des nœuds de tooother tooconnect hello du nœud principal dans le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="22748-170">**SSH**: Once connected tooa head node using SSH, you can then use SSH from hello head node tooconnect tooother nodes in hello cluster.</span></span> <span data-ttu-id="22748-171">Pour plus d’informations, consultez hello [utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span><span class="sxs-lookup"><span data-stu-id="22748-171">For more information, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

* <span data-ttu-id="22748-172">**Tunnel SSH**: Si vous avez besoin de tooaccess un service web hébergé sur un des nœuds hello qui n’est pas exposée toohello internet, vous devez utiliser un tunnel SSH.</span><span class="sxs-lookup"><span data-stu-id="22748-172">**SSH Tunnel**: If you need tooaccess a web service hosted on one of hello nodes that is not exposed toohello internet, you must use an SSH tunnel.</span></span> <span data-ttu-id="22748-173">Pour plus d’informations, consultez hello [utiliser un tunnel SSH avec HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span><span class="sxs-lookup"><span data-stu-id="22748-173">For more information, see hello [Use an SSH tunnel with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

* <span data-ttu-id="22748-174">**Réseau virtuel Azure**: Si votre HDInsight cluster fait partie d’un réseau virtuel Azure, n’importe quelle ressource sur hello même réseau virtuel peut accéder directement à tous les nœuds de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="22748-174">**Azure Virtual Network**: If your HDInsight cluster is part of an Azure Virtual Network, any resource on hello same Virtual Network can directly access all nodes in hello cluster.</span></span> <span data-ttu-id="22748-175">Pour plus d’informations, consultez hello [HDInsight étendre à l’aide du réseau virtuel Azure](hdinsight-extend-hadoop-virtual-network.md) document.</span><span class="sxs-lookup"><span data-stu-id="22748-175">For more information, see hello [Extend HDInsight using Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span>

## <a name="how-toocheck-on-a-service-status"></a><span data-ttu-id="22748-176">Comment toocheck sur un état de service</span><span class="sxs-lookup"><span data-stu-id="22748-176">How toocheck on a service status</span></span>

<span data-ttu-id="22748-177">état de hello toocheck des services qui s’exécutent sur les nœuds principaux hello, utilisez hello Ambari Web UI ou hello Ambari REST API.</span><span class="sxs-lookup"><span data-stu-id="22748-177">toocheck hello status of services that run on hello head nodes, use hello Ambari Web UI or hello Ambari REST API.</span></span>

### <a name="ambari-web-ui"></a><span data-ttu-id="22748-178">Interface utilisateur web d'Ambari</span><span class="sxs-lookup"><span data-stu-id="22748-178">Ambari Web UI</span></span>

<span data-ttu-id="22748-179">Hello l’interface utilisateur de Ambari Web est visible à https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="22748-179">hello Ambari Web UI is viewable at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="22748-180">Remplacez **CLUSTERNAME** avec nom hello de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="22748-180">Replace **CLUSTERNAME** with hello name of your cluster.</span></span> <span data-ttu-id="22748-181">Si vous y êtes invité, entrez les informations d’identification des utilisateurs HTTP hello pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="22748-181">If prompted, enter hello HTTP user credentials for your cluster.</span></span> <span data-ttu-id="22748-182">nom d’utilisateur HTTP Hello par défaut est **admin** et hello est hello de mot de passe saisis lors de la création du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="22748-182">hello default HTTP user name is **admin** and hello password is hello password you entered when creating hello cluster.</span></span>

<span data-ttu-id="22748-183">Lorsque vous arrivez sur la page de confirmation d’Ambari hello, services de hello installé sont répertoriés sur la gauche hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="22748-183">When you arrive on hello Ambari page, hello installed services are listed on hello left of hello page.</span></span>

![Services installés](./media/hdinsight-high-availability-linux/services.png)

<span data-ttu-id="22748-185">Il existe une série d’icônes qui peuvent s’afficher l’état tooindicate de service suivante tooa.</span><span class="sxs-lookup"><span data-stu-id="22748-185">There are a series of icons that may appear next tooa service tooindicate status.</span></span> <span data-ttu-id="22748-186">Toutes les alertes liées tooa peut être affiché à l’aide hello **alertes** lien en hello haut hello.</span><span class="sxs-lookup"><span data-stu-id="22748-186">Any alerts related tooa service can be viewed using hello **Alerts** link at hello top of hello page.</span></span> <span data-ttu-id="22748-187">Vous pouvez sélectionner chaque tooview service plus d’informations sur ce dernier.</span><span class="sxs-lookup"><span data-stu-id="22748-187">You can select each service tooview more information on it.</span></span>

<span data-ttu-id="22748-188">Lors de la page du service hello fournit des informations sur l’état de hello et la configuration de chaque service, il ne fournit pas les informations sur lequel service hello de nœud principal est en cours d’exécution sur.</span><span class="sxs-lookup"><span data-stu-id="22748-188">While hello service page provides information on hello status and configuration of each service, it does not provide information on which head node hello service is running on.</span></span> <span data-ttu-id="22748-189">tooview cette plus d’informations, l’utilisation hello **hôtes** lien en hello haut hello.</span><span class="sxs-lookup"><span data-stu-id="22748-189">tooview this information, use hello **Hosts** link at hello top of hello page.</span></span> <span data-ttu-id="22748-190">Cette page affiche les ordinateurs hôtes au sein du cluster hello, y compris les nœuds principal hello.</span><span class="sxs-lookup"><span data-stu-id="22748-190">This page displays hosts within hello cluster, including hello head nodes.</span></span>

![liste des hôtes](./media/hdinsight-high-availability-linux/hosts.png)

<span data-ttu-id="22748-192">En sélectionnant hello lien de l’un des nœuds de tête hello affiche hello composants services et en cours d’exécution sur ce nœud.</span><span class="sxs-lookup"><span data-stu-id="22748-192">Selecting hello link for one of hello head nodes displays hello services and components running on that node.</span></span>

![État du composant](./media/hdinsight-high-availability-linux/nodeservices.png)

<span data-ttu-id="22748-194">Pour plus d’informations sur l’utilisation de Ambari, consultez [analyse et de gérer HDInsight à l’aide de hello l’interface utilisateur de Ambari Web](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="22748-194">For more information on using Ambari, see [Monitor and manage HDInsight using hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

### <a name="ambari-rest-api"></a><span data-ttu-id="22748-195">API Ambari REST</span><span class="sxs-lookup"><span data-stu-id="22748-195">Ambari REST API</span></span>

<span data-ttu-id="22748-196">Hello Ambari REST API est disponible via hello internet.</span><span class="sxs-lookup"><span data-stu-id="22748-196">hello Ambari REST API is available over hello internet.</span></span> <span data-ttu-id="22748-197">passerelle de Hello HDInsight publique gère routage demandes toohello nœud principal qui héberge actuellement hello API REST.</span><span class="sxs-lookup"><span data-stu-id="22748-197">hello HDInsight public gateway handles routing requests toohello head node that is currently hosting hello REST API.</span></span>

<span data-ttu-id="22748-198">Vous pouvez utiliser hello suivant l’état d’un service via l’API REST de Ambari de hello hello de toocheck la commande :</span><span class="sxs-lookup"><span data-stu-id="22748-198">You can use hello following command toocheck hello state of a service through hello Ambari REST API:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICENAME?fields=ServiceInfo/state

* <span data-ttu-id="22748-199">Remplacez **mot de passe** avec le mot de passe utilisateur (admin) hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="22748-199">Replace **PASSWORD** with hello HTTP user (admin) account password.</span></span>
* <span data-ttu-id="22748-200">Remplacez **CLUSTERNAME** avec nom hello du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="22748-200">Replace **CLUSTERNAME** with hello name of hello cluster.</span></span>
* <span data-ttu-id="22748-201">Remplacez **SERVICENAME** avec nom hello du service de hello vous souhaitez que l’état de hello de toocheck de.</span><span class="sxs-lookup"><span data-stu-id="22748-201">Replace **SERVICENAME** with hello name of hello service you want toocheck hello status of.</span></span>

<span data-ttu-id="22748-202">Par exemple, les état hello toocheck Hello **HDFS** service sur un cluster nommé **mycluster**, avec un mot de passe **mot de passe**, vous utiliseriez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="22748-202">For example, toocheck hello status of hello **HDFS** service on a cluster named **mycluster**, with a password of **password**, you would use hello following command:</span></span>

    curl -u admin:password https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state

<span data-ttu-id="22748-203">réponse de Hello est similaire toohello suivant JSON :</span><span class="sxs-lookup"><span data-stu-id="22748-203">hello response is similar toohello following JSON:</span></span>

    {
      "href" : "http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8080/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state",
      "ServiceInfo" : {
        "cluster_name" : "mycluster",
        "service_name" : "HDFS",
        "state" : "STARTED"
      }
    }

<span data-ttu-id="22748-204">Hello URL indique que le service de hello est en cours d’exécution sur un nœud principal nommé **hn0-CLUSTERNAME**.</span><span class="sxs-lookup"><span data-stu-id="22748-204">hello URL tells us that hello service is currently running on a head node named **hn0-CLUSTERNAME**.</span></span>

<span data-ttu-id="22748-205">Hello état indique que le service de hello est en cours d’exécution, ou **démarré**.</span><span class="sxs-lookup"><span data-stu-id="22748-205">hello state tells us that hello service is currently running, or **STARTED**.</span></span>

<span data-ttu-id="22748-206">Si vous ne connaissez pas les services sont installés sur le cluster de hello, vous pouvez utiliser hello suivant commande tooretrieve une liste :</span><span class="sxs-lookup"><span data-stu-id="22748-206">If you do not know what services are installed on hello cluster, you can use hello following command tooretrieve a list:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services

<span data-ttu-id="22748-207">Pour plus d’informations sur l’utilisation des API REST de Ambari de hello, consultez [surveiller et gérer HDInsight, à l’aide de hello API REST de Ambari](hdinsight-hadoop-manage-ambari-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="22748-207">For more information on working with hello Ambari REST API, see [Monitor and Manage HDInsight using hello Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md).</span></span>

#### <a name="service-components"></a><span data-ttu-id="22748-208">Composants du service</span><span class="sxs-lookup"><span data-stu-id="22748-208">Service components</span></span>

<span data-ttu-id="22748-209">Services peuvent contenir des composants que vous souhaitez état hello toocheck individuellement.</span><span class="sxs-lookup"><span data-stu-id="22748-209">Services may contain components that you wish toocheck hello status of individually.</span></span> <span data-ttu-id="22748-210">Par exemple, HDFS contient hello NameNode.</span><span class="sxs-lookup"><span data-stu-id="22748-210">For example, HDFS contains hello NameNode component.</span></span> <span data-ttu-id="22748-211">tooview plus d’informations sur un composant, commande hello serait :</span><span class="sxs-lookup"><span data-stu-id="22748-211">tooview information on a component, hello command would be:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

<span data-ttu-id="22748-212">Si vous ne connaissez pas les composants sont fournis par un service, vous pouvez utiliser hello suivant commande tooretrieve une liste :</span><span class="sxs-lookup"><span data-stu-id="22748-212">If you do not know what components are provided by a service, you can use hello following command tooretrieve a list:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

## <a name="how-tooaccess-log-files-on-hello-head-nodes"></a><span data-ttu-id="22748-213">Comment tooaccess fichiers journaux sur les nœuds principaux hello</span><span class="sxs-lookup"><span data-stu-id="22748-213">How tooaccess log files on hello head nodes</span></span>

### <a name="ssh"></a><span data-ttu-id="22748-214">SSH</span><span class="sxs-lookup"><span data-stu-id="22748-214">SSH</span></span>

<span data-ttu-id="22748-215">Lors de nœud principal de tooa connecté via SSH, les fichiers journaux se trouve dans **/var/log**.</span><span class="sxs-lookup"><span data-stu-id="22748-215">While connected tooa head node through SSH, log files can be found under **/var/log**.</span></span> <span data-ttu-id="22748-216">Par exemple, **/var/log/hadoop-yarn/yarn** contiennent les journaux correspondant à YARN.</span><span class="sxs-lookup"><span data-stu-id="22748-216">For example, **/var/log/hadoop-yarn/yarn** contain logs for YARN.</span></span>

<span data-ttu-id="22748-217">Chaque nœud principal peut avoir des entrées de journal unique, vérifiez donc hello se connecte à la fois.</span><span class="sxs-lookup"><span data-stu-id="22748-217">Each head node can have unique log entries, so you should check hello logs on both.</span></span>

### <a name="sftp"></a><span data-ttu-id="22748-218">SFTP</span><span class="sxs-lookup"><span data-stu-id="22748-218">SFTP</span></span>

<span data-ttu-id="22748-219">Vous pouvez également connecter toohello de nœud principal à l’aide de hello SSH File Transfer Protocol ou sécuriser fichier SFTP (Transfer Protocol) et le télécharger directement les fichiers journaux de hello.</span><span class="sxs-lookup"><span data-stu-id="22748-219">You can also connect toohello head node using hello SSH File Transfer Protocol or Secure File Transfer Protocol (SFTP), and download hello log files directly.</span></span>

<span data-ttu-id="22748-220">Toousing similaire lors de la connexion de cluster toohello vous devez fournir un client SSH hello SSH utilisateur compte nom et hello SSH l’adresse du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="22748-220">Similar toousing an SSH client, when connecting toohello cluster you must provide hello SSH user account name and hello SSH address of hello cluster.</span></span> <span data-ttu-id="22748-221">Par exemple, `sftp username@mycluster-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="22748-221">For example, `sftp username@mycluster-ssh.azurehdinsight.net`.</span></span> <span data-ttu-id="22748-222">Fournir le mot de passe de hello compte hello lorsque vous y êtes invité, ou fournissez une clé publique à l’aide de hello `-i` paramètre.</span><span class="sxs-lookup"><span data-stu-id="22748-222">Provide hello password for hello account when prompted, or provide a public key using hello `-i` parameter.</span></span>

<span data-ttu-id="22748-223">Une fois connecté, vous voyez apparaître une invite `sftp>` .</span><span class="sxs-lookup"><span data-stu-id="22748-223">Once connected, you are presented with a `sftp>` prompt.</span></span> <span data-ttu-id="22748-224">À partir de cette invite, vous pouvez changer de répertoire, ainsi que charger et télécharger des fichiers.</span><span class="sxs-lookup"><span data-stu-id="22748-224">From this prompt, you can change directories, upload, and download files.</span></span> <span data-ttu-id="22748-225">Par exemple, hello suivant les commandes modifier les répertoires toohello **/var/log/hadoop/hdfs** active, puis téléchargez de tous les fichiers dans le répertoire de hello.</span><span class="sxs-lookup"><span data-stu-id="22748-225">For example, hello following commands change directories toohello **/var/log/hadoop/hdfs** directory and then download all files in hello directory.</span></span>

    cd /var/log/hadoop/hdfs
    get *

<span data-ttu-id="22748-226">Pour obtenir la liste des commandes disponibles, entrez `help` à hello `sftp>` invite.</span><span class="sxs-lookup"><span data-stu-id="22748-226">For a list of available commands, enter `help` at hello `sftp>` prompt.</span></span>

> [!NOTE]
> <span data-ttu-id="22748-227">Il existe également des interfaces graphiques qui vous permettent de système de fichiers toovisualize hello lorsqu’il est connecté à l’aide de SFTP.</span><span class="sxs-lookup"><span data-stu-id="22748-227">There are also graphical interfaces that allow you toovisualize hello file system when connected using SFTP.</span></span> <span data-ttu-id="22748-228">Par exemple, [MobaXTerm](http://mobaxterm.mobatek.net/) vous permet de système de fichiers toobrowse hello à l’aide d’un Explorateur de tooWindows similaire interface.</span><span class="sxs-lookup"><span data-stu-id="22748-228">For example, [MobaXTerm](http://mobaxterm.mobatek.net/) allows you toobrowse hello file system using an interface similar tooWindows Explorer.</span></span>

### <a name="ambari"></a><span data-ttu-id="22748-229">Ambari</span><span class="sxs-lookup"><span data-stu-id="22748-229">Ambari</span></span>

> [!NOTE]
> <span data-ttu-id="22748-230">tooaccess journaux à l’aide de Ambari, vous devez utiliser un tunnel SSH.</span><span class="sxs-lookup"><span data-stu-id="22748-230">tooaccess log files using Ambari, you must use an SSH tunnel.</span></span> <span data-ttu-id="22748-231">des interfaces web Hello pour les services individuels hello ne sont pas exposées publiquement sur Internet de hello.</span><span class="sxs-lookup"><span data-stu-id="22748-231">hello web interfaces for hello individual services are not exposed publicly on hello Internet.</span></span> <span data-ttu-id="22748-232">Pour plus d’informations sur l’utilisation d’un tunnel SSH, consultez hello [utiliser SSH Tunneling](hdinsight-linux-ambari-ssh-tunnel.md) document.</span><span class="sxs-lookup"><span data-stu-id="22748-232">For information on using an SSH tunnel, see hello [Use SSH Tunneling](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

<span data-ttu-id="22748-233">À partir de l’interface utilisateur de Ambari Web de hello, sélectionnez service hello vous souhaitez tooview journaux (par exemple, des fils).</span><span class="sxs-lookup"><span data-stu-id="22748-233">From hello Ambari Web UI, select hello service you wish tooview logs for (for example, YARN).</span></span> <span data-ttu-id="22748-234">Utilisez ensuite **liens rapides** tooselect les journaux pour le hello tooview de nœud principal.</span><span class="sxs-lookup"><span data-stu-id="22748-234">Then use **Quick Links** tooselect which head node tooview hello logs for.</span></span>

![À l’aide rapide lie tooview journaux](./media/hdinsight-high-availability-linux/viewlogs.png)

## <a name="how-tooconfigure-hello-node-size"></a><span data-ttu-id="22748-236">Comment tooconfigure hello taille du nœud</span><span class="sxs-lookup"><span data-stu-id="22748-236">How tooconfigure hello node size</span></span>

<span data-ttu-id="22748-237">taille de Hello d’un nœud peut être sélectionné uniquement lors de la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="22748-237">hello size of a node can only be selected during cluster creation.</span></span> <span data-ttu-id="22748-238">Vous trouverez une liste de hello différentes tailles de machine virtuelle disponibles pour HDInsight sur hello [HDInsight page de tarification](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="22748-238">You can find a list of hello different VM sizes available for HDInsight on hello [HDInsight pricing page](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

<span data-ttu-id="22748-239">Lorsque vous créez un cluster, vous pouvez spécifier la taille hello de nœuds de hello.</span><span class="sxs-lookup"><span data-stu-id="22748-239">When creating a cluster, you can specify hello size of hello nodes.</span></span> <span data-ttu-id="22748-240">Hello ci-après fournit des conseils sur la façon dont la taille de hello toospecify à l’aide hello [portail Azure][preview-portal], [Azure PowerShell][azure-powershell], et hello [CLI d’Azure][azure-cli]:</span><span class="sxs-lookup"><span data-stu-id="22748-240">hello following information provides guidance on how toospecify hello size using hello [Azure portal][preview-portal], [Azure PowerShell][azure-powershell], and hello [Azure CLI][azure-cli]:</span></span>

* <span data-ttu-id="22748-241">**Portail Azure**: lorsque vous créez un cluster, vous pouvez définir la taille hello de nœuds hello utilisé par hello cluster :</span><span class="sxs-lookup"><span data-stu-id="22748-241">**Azure portal**: When creating a cluster, you can set hello size of hello nodes used by hello cluster:</span></span>

    ![Image de l'Assistant de création de cluster avec sélection de taille de nœud](./media/hdinsight-high-availability-linux/headnodesize.png)

* <span data-ttu-id="22748-243">**CLI Azure**: lors de l’utilisation de hello `azure hdinsight cluster create` de commande, vous pouvez définir la taille de hello de tête de hello, de traitement et les nœuds soigneur à l’aide de hello `--headNodeSize`, `--workerNodeSize`, et `--zookeeperNodeSize` paramètres.</span><span class="sxs-lookup"><span data-stu-id="22748-243">**Azure CLI**: When using hello `azure hdinsight cluster create` command, you can set hello size of hello head, worker, and ZooKeeper nodes by using hello `--headNodeSize`, `--workerNodeSize`, and `--zookeeperNodeSize` parameters.</span></span>

* <span data-ttu-id="22748-244">**Azure PowerShell**: lors de l’utilisation de hello `New-AzureRmHDInsightCluster` applet de commande, vous pouvez définir taille hello de tête de hello, de traitement et les nœuds soigneur à l’aide de hello `-HeadNodeVMSize`, `-WorkerNodeSize`, et `-ZookeeperNodeSize` paramètres.</span><span class="sxs-lookup"><span data-stu-id="22748-244">**Azure PowerShell**: When using hello `New-AzureRmHDInsightCluster` cmdlet, you can set hello size of hello head, worker, and ZooKeeper nodes by using hello `-HeadNodeVMSize`, `-WorkerNodeSize`, and `-ZookeeperNodeSize` parameters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="22748-245">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="22748-245">Next steps</span></span>

<span data-ttu-id="22748-246">Utilisez hello suivant toolearn des liens plus sur les éléments mentionnés dans ce document.</span><span class="sxs-lookup"><span data-stu-id="22748-246">Use hello following links toolearn more about things mentioned in this document.</span></span>

* [<span data-ttu-id="22748-247">Référence REST Ambari</span><span class="sxs-lookup"><span data-stu-id="22748-247">Ambari REST Reference</span></span>](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)
* [<span data-ttu-id="22748-248">Installer et configurer hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="22748-248">Install and configure hello Azure CLI</span></span>](../cli-install-nodejs.md)
* [<span data-ttu-id="22748-249">Installation et configuration d'Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="22748-249">Install and configure Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="22748-250">Gestion de HDInsight à l'aide d'Ambari</span><span class="sxs-lookup"><span data-stu-id="22748-250">Manage HDInsight using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)
* [<span data-ttu-id="22748-251">Approvisionnement de clusters HDInsight sous Linux</span><span class="sxs-lookup"><span data-stu-id="22748-251">Provision Linux-based HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)

[preview-portal]: https://portal.azure.com/
[azure-powershell]: /powershell/azureps-cmdlets-docs
[azure-cli]: ../cli-install-nodejs.md
