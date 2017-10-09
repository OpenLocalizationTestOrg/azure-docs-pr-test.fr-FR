---
title: "réplication de cluster HBase aaaConfigure dans les réseaux virtuels - Azure | Documents Microsoft"
description: "Découvrez comment tooconfigure HBase la réplication pour l’équilibrage de charge, une haute disponibilité, sans interruption de service migration/mise à jour un tooanother de version HDInsight et la récupération d’urgence."
services: hdinsight,virtual-network
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: ba1c44f26b7cbf4a7a88159b12b3e064ea9f9a20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hbase-cluster-replication-within-virtual-networks"></a><span data-ttu-id="ffffc-103">Configurer la réplication de cluster HBase dans les réseaux virtuels</span><span class="sxs-lookup"><span data-stu-id="ffffc-103">Configure HBase cluster replication within virtual networks</span></span>

<span data-ttu-id="ffffc-104">Découvrez comment tooconfigure HBase réplication dans un réseau virtuel (VNet) ou entre deux réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="ffffc-104">Learn how tooconfigure HBase replication within one virtual network (VNet) or between two virtual networks.</span></span>

<span data-ttu-id="ffffc-105">La réplication en cluster utilise une méthodologie par émission de données source.</span><span class="sxs-lookup"><span data-stu-id="ffffc-105">Cluster replication uses a source-push methodology.</span></span> <span data-ttu-id="ffffc-106">Un cluster HBase peut être une source, une destination ou jouer les deux rôles à la fois.</span><span class="sxs-lookup"><span data-stu-id="ffffc-106">An HBase cluster can be a source or a destination, or it can fulfill both roles at once.</span></span> <span data-ttu-id="ffffc-107">La réplication est asynchrone et objectif hello de réplication est cohérence éventuelle.</span><span class="sxs-lookup"><span data-stu-id="ffffc-107">Replication is asynchronous, and hello goal of replication is eventual consistency.</span></span> <span data-ttu-id="ffffc-108">Lors de la source de hello reçoit une famille de colonne tooa Edition avec la réplication est activée, cette modification est propagé tooall les clusters de destination.</span><span class="sxs-lookup"><span data-stu-id="ffffc-108">When hello source receives an edit tooa column family with replication enabled, that edit is propagated tooall destination clusters.</span></span> <span data-ttu-id="ffffc-109">Lorsque les données sont répliquées à partir d’un cluster tooanother, du cluster source hello et tous les clusters qui ont sollicité déjà les données de salutation sont suivies tooprevent les boucles de réplication.</span><span class="sxs-lookup"><span data-stu-id="ffffc-109">When data is replicated from one cluster tooanother, hello source cluster and all clusters that have already consumed hello data are tracked tooprevent replication loops.</span></span>

<span data-ttu-id="ffffc-110">Dans ce didacticiel, vous allez configurer une réplication source-destination.</span><span class="sxs-lookup"><span data-stu-id="ffffc-110">In this tutorial, you will configure a source-destination replication.</span></span> <span data-ttu-id="ffffc-111">Pour d'autres topologies de cluster, consultez le [Guide de référence d'Apache HBase](http://hbase.apache.org/book.html#_cluster_replication).</span><span class="sxs-lookup"><span data-stu-id="ffffc-111">For other cluster topologies, see [Apache HBase Reference Guide](http://hbase.apache.org/book.html#_cluster_replication).</span></span>

<span data-ttu-id="ffffc-112">Cas d’utilisation de la réplication HBase pour un seul réseau virtuel :</span><span class="sxs-lookup"><span data-stu-id="ffffc-112">HBase replication usage cases for a single virtual network:</span></span>

* <span data-ttu-id="ffffc-113">L’équilibrage de charge--par exemple, en cours d’exécution des analyses ou des tâches MapReduce sur le cluster de destination hello et la réception de données sur le cluster source de hello</span><span class="sxs-lookup"><span data-stu-id="ffffc-113">Load balancing--for example, running scans or MapReduce jobs on hello destination cluster and ingesting data on hello source cluster</span></span>
* <span data-ttu-id="ffffc-114">Haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="ffffc-114">High availability</span></span>
* <span data-ttu-id="ffffc-115">Migration des données à partir d’un tooanother de cluster HBase</span><span class="sxs-lookup"><span data-stu-id="ffffc-115">Migrating data from one HBase cluster tooanother</span></span>
* <span data-ttu-id="ffffc-116">La mise à niveau d’un cluster Azure HDInsight à partir d’une version tooanother</span><span class="sxs-lookup"><span data-stu-id="ffffc-116">Upgrading an Azure HDInsight cluster from one version tooanother</span></span>

<span data-ttu-id="ffffc-117">Cas d’utilisation de la réplication HBase pour deux réseaux virtuels :</span><span class="sxs-lookup"><span data-stu-id="ffffc-117">HBase replication usage cases for two virtual networks:</span></span>

* <span data-ttu-id="ffffc-118">Récupération d'urgence</span><span class="sxs-lookup"><span data-stu-id="ffffc-118">Disaster recovery</span></span>
* <span data-ttu-id="ffffc-119">L’équilibrage de charge et de partitionnement application hello</span><span class="sxs-lookup"><span data-stu-id="ffffc-119">Load balancing and partitioning hello application</span></span>
* <span data-ttu-id="ffffc-120">Haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="ffffc-120">High availability</span></span>

<span data-ttu-id="ffffc-121">Vous répliquez des clusters à l’aide de scripts [d’action de script](hdinsight-hadoop-customize-cluster-linux.md) disponibles dans [GitHub](https://github.com/Azure/hbase-utils/tree/master/replication).</span><span class="sxs-lookup"><span data-stu-id="ffffc-121">You replicate clusters by using [script action](hdinsight-hadoop-customize-cluster-linux.md) scripts located at [GitHub](https://github.com/Azure/hbase-utils/tree/master/replication).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ffffc-122">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ffffc-122">Prerequisites</span></span>
<span data-ttu-id="ffffc-123">Avant de commencer ce didacticiel, vous devez disposer d’un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="ffffc-123">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="ffffc-124">Consultez la rubrique [Obtenir une version d'évaluation gratuite d'Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="ffffc-124">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="configure-hello-environments"></a><span data-ttu-id="ffffc-125">Configurez des environnements de hello</span><span class="sxs-lookup"><span data-stu-id="ffffc-125">Configure hello environments</span></span>

<span data-ttu-id="ffffc-126">Il existe trois options de configuration :</span><span class="sxs-lookup"><span data-stu-id="ffffc-126">There are three possible configurations:</span></span>

- <span data-ttu-id="ffffc-127">Deux clusters HBase dans un réseau virtuel Azure</span><span class="sxs-lookup"><span data-stu-id="ffffc-127">Two HBase clusters in one Azure virtual network</span></span>
- <span data-ttu-id="ffffc-128">Deux clusters HBase dans deux réseaux virtuels différents dans hello même région</span><span class="sxs-lookup"><span data-stu-id="ffffc-128">Two HBase clusters in two different virtual networks in hello same region</span></span>
- <span data-ttu-id="ffffc-129">Deux clusters HBase dans deux réseaux virtuels différents dans deux régions distinctes (géoréplication)</span><span class="sxs-lookup"><span data-stu-id="ffffc-129">Two HBase clusters in two different virtual networks in two different regions (geo-replication)</span></span>

<span data-ttu-id="ffffc-130">toomake il les environnements hello tooconfigure plus faciles, nous avons créé certains [modèles Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ffffc-130">toomake it easier tooconfigure hello environments, we have created some [Azure Resource Manager templates](../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="ffffc-131">Si vous préférez les environnements hello tooconfigure par d’autres méthodes, consultez :</span><span class="sxs-lookup"><span data-stu-id="ffffc-131">If you prefer tooconfigure hello environments by using other methods, see:</span></span>

- [<span data-ttu-id="ffffc-132">Création de clusters Hadoop basés sur Linux dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="ffffc-132">Create Linux-based Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
- [<span data-ttu-id="ffffc-133">Création de clusters HBase dans un réseau virtuel Azure</span><span class="sxs-lookup"><span data-stu-id="ffffc-133">Create HBase clusters in Azure Virtual Network</span></span>](hdinsight-hbase-provision-vnet.md)

### <a name="configure-one-virtual-network"></a><span data-ttu-id="ffffc-134">Configurer un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="ffffc-134">Configure one virtual network</span></span>

<span data-ttu-id="ffffc-135">Cliquez sur hello suivant image toocreate deux HBase clusters Bonjour même réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="ffffc-135">Click hello following image toocreate two HBase clusters in hello same virtual network.</span></span> <span data-ttu-id="ffffc-136">modèle de Hello est stocké dans [modèles de démarrage rapide Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-one-vnet/).</span><span class="sxs-lookup"><span data-stu-id="ffffc-136">hello template is stored in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-one-vnet/).</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-one-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>

### <a name="configure-two-virtual-networks-in-hello-same-region"></a><span data-ttu-id="ffffc-137">Configurer deux réseaux virtuels Bonjour même région</span><span class="sxs-lookup"><span data-stu-id="ffffc-137">Configure two virtual networks in hello same region</span></span>

<span data-ttu-id="ffffc-138">Cliquez sur Suivant image toocreate deux réseaux virtuels avec deux clusters HBase Bonjour et de réseau virtuel d’homologation de hello même région.</span><span class="sxs-lookup"><span data-stu-id="ffffc-138">Click hello following image toocreate two virtual networks with VNet peering and two HBase clusters in hello same region.</span></span> <span data-ttu-id="ffffc-139">modèle de Hello est stocké dans [modèles de démarrage rapide Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-two-vnets-same-region/).</span><span class="sxs-lookup"><span data-stu-id="ffffc-139">hello template is stored in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-two-vnets-same-region/).</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-two-vnets-same-region%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>



<span data-ttu-id="ffffc-140">Ce scénario nécessite [l’homologation de réseaux virtuels](../virtual-network/virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ffffc-140">This scenario requires [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span> <span data-ttu-id="ffffc-141">modèle de Hello permet d’homologation de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="ffffc-141">hello template enables VNet peering.</span></span>   

<span data-ttu-id="ffffc-142">HBase la réplication utilise des adresses IP de hello soigneur VMs.</span><span class="sxs-lookup"><span data-stu-id="ffffc-142">HBase replication uses IP addresses of hello ZooKeeper VMs.</span></span> <span data-ttu-id="ffffc-143">Vous devez configurer des adresses IP statiques pour les nœuds de HBase soigneur destination hello.</span><span class="sxs-lookup"><span data-stu-id="ffffc-143">You must configure static IP addresses for hello destination HBase ZooKeeper nodes.</span></span>

<span data-ttu-id="ffffc-144">**tooconfigure des adresses IP statiques**</span><span class="sxs-lookup"><span data-stu-id="ffffc-144">**tooconfigure static IP addresses**</span></span>

1. <span data-ttu-id="ffffc-145">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ffffc-145">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ffffc-146">Dans le menu de gauche hello, cliquez sur **groupes de ressources**.</span><span class="sxs-lookup"><span data-stu-id="ffffc-146">From hello left menu, click **Resource Groups**.</span></span>
3. <span data-ttu-id="ffffc-147">Cliquez sur votre groupe de ressources qui contient le cluster HBase de destination hello.</span><span class="sxs-lookup"><span data-stu-id="ffffc-147">Click your resource group that contains hello destination HBase cluster.</span></span> <span data-ttu-id="ffffc-148">Il s’agit de groupe de ressources hello que vous avez spécifié lorsque vous avez utilisé l’environnement de hello toocreate hello Gestionnaire de ressources du modèle.</span><span class="sxs-lookup"><span data-stu-id="ffffc-148">This is hello resource group that you specified when you used hello Resource Manager template toocreate hello environment.</span></span> <span data-ttu-id="ffffc-149">Vous pouvez utiliser toonarrow de filtre hello déroulant hello.</span><span class="sxs-lookup"><span data-stu-id="ffffc-149">You can use hello filter toonarrow down hello list.</span></span> <span data-ttu-id="ffffc-150">Vous pouvez voir une liste de ressources qui contient les réseaux virtuels deux hello.</span><span class="sxs-lookup"><span data-stu-id="ffffc-150">You can see a list of resources that contains hello two virtual networks.</span></span>
4. <span data-ttu-id="ffffc-151">Cliquez sur le réseau virtuel hello qui contient le cluster HBase de destination hello.</span><span class="sxs-lookup"><span data-stu-id="ffffc-151">Click hello virtual network that contains hello destination HBase cluster.</span></span> <span data-ttu-id="ffffc-152">Par exemple, cliquez sur **xxxx-vnet2**.</span><span class="sxs-lookup"><span data-stu-id="ffffc-152">For example, click **xxxx-vnet2**.</span></span> <span data-ttu-id="ffffc-153">Vous pouvez voir trois appareils avec des noms qui commencent par **nic-zookeepermode-**.</span><span class="sxs-lookup"><span data-stu-id="ffffc-153">You can see three devices with names that start with **nic-zookeepermode-**.</span></span> <span data-ttu-id="ffffc-154">Ces appareils sont des machines virtuelles de hello trois soigneur.</span><span class="sxs-lookup"><span data-stu-id="ffffc-154">Those devices are hello three ZooKeeper VMs.</span></span>
5. <span data-ttu-id="ffffc-155">Cliquez sur une de hello soigneur VMs.</span><span class="sxs-lookup"><span data-stu-id="ffffc-155">Click one of hello ZooKeeper VMs.</span></span>
6. <span data-ttu-id="ffffc-156">Cliquez sur **Configurations IP**.</span><span class="sxs-lookup"><span data-stu-id="ffffc-156">Click **IP configurations**.</span></span>
7. <span data-ttu-id="ffffc-157">Cliquez sur **ipConfig1** à partir de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="ffffc-157">Click **ipConfig1** from hello list.</span></span>
8. <span data-ttu-id="ffffc-158">Cliquez sur **statique**et notez les adresses IP réelles hello.</span><span class="sxs-lookup"><span data-stu-id="ffffc-158">Click **Static**, and write down hello actual IP address.</span></span> <span data-ttu-id="ffffc-159">Vous devez adresse hello lors de l’exécution de la réplication de tooenable hello script action.</span><span class="sxs-lookup"><span data-stu-id="ffffc-159">You will need hello IP address when you run hello script action tooenable replication.</span></span>

  ![Adresse IP statique ZooKeeper de réplication HDInsight HBase](./media/hdinsight-hbase-replication/hdinsight-hbase-replication-zookeeper-static-ip.png)

9. <span data-ttu-id="ffffc-161">Répétez l’étape 6 tooset hello adresse IP pour hello deux autres nœuds soigneur.</span><span class="sxs-lookup"><span data-stu-id="ffffc-161">Repeat step 6 tooset hello static IP address for hello other two ZooKeeper nodes.</span></span>

<span data-ttu-id="ffffc-162">Pour le scénario de réseau virtuel entre hello, vous devez utiliser hello **- ip** commutateur lors de l’appel hello **hdi_enable_replication.sh** action de script.</span><span class="sxs-lookup"><span data-stu-id="ffffc-162">For hello cross-VNet scenario, you must use hello **-ip** switch when calling hello **hdi_enable_replication.sh** script action.</span></span>

### <a name="configure-two-virtual-networks-in-two-different-regions"></a><span data-ttu-id="ffffc-163">Configurer deux réseaux virtuels dans deux régions différentes</span><span class="sxs-lookup"><span data-stu-id="ffffc-163">Configure two virtual networks in two different regions</span></span>

<span data-ttu-id="ffffc-164">Cliquez sur hello suivant image toocreate deux réseaux virtuels dans les deux régions différentes.</span><span class="sxs-lookup"><span data-stu-id="ffffc-164">Click hello following image toocreate two virtual networks in two different regions.</span></span> <span data-ttu-id="ffffc-165">modèle de Hello est stocké dans un conteneur d’objets Blob Azure publique.</span><span class="sxs-lookup"><span data-stu-id="ffffc-165">hello template is stored in a public Azure Blob container.</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fhbaseha%2Fdeploy-hbase-geo-replication.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>

<span data-ttu-id="ffffc-166">Créer une passerelle VPN entre les réseaux virtuels deux hello.</span><span class="sxs-lookup"><span data-stu-id="ffffc-166">Create a VPN gateway between hello two virtual networks.</span></span> <span data-ttu-id="ffffc-167">Pour savoir comment faire, consultez [Création d’un réseau virtuel avec une connexion de site à site à l’aide du portail Azure](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ffffc-167">For instructions, see [Create a VNet with a site-to-site connection](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).</span></span>

<span data-ttu-id="ffffc-168">HBase la réplication utilise des adresses IP de hello soigneur VMs.</span><span class="sxs-lookup"><span data-stu-id="ffffc-168">HBase replication uses IP addresses of hello ZooKeeper VMs.</span></span> <span data-ttu-id="ffffc-169">Vous devez configurer des adresses IP statiques pour les nœuds de HBase soigneur destination hello.</span><span class="sxs-lookup"><span data-stu-id="ffffc-169">You must configure static IP addresses for hello destination HBase ZooKeeper nodes.</span></span> <span data-ttu-id="ffffc-170">tooconfigure l’adresse IP statique, consultez hello « configurer deux des réseaux virtuels dans hello même région » section dans cet article.</span><span class="sxs-lookup"><span data-stu-id="ffffc-170">tooconfigure static IP, see hello "Configure two virtual networks in hello same region" section in this article.</span></span>

<span data-ttu-id="ffffc-171">Pour le scénario de réseau virtuel entre hello, vous devez utiliser hello **- ip** commutateur lors de l’appel hello **hdi_enable_replication.sh** action de script.</span><span class="sxs-lookup"><span data-stu-id="ffffc-171">For hello cross-VNet scenario, you must use hello **-ip** switch when calling hello **hdi_enable_replication.sh** script action.</span></span>

## <a name="load-test-data"></a><span data-ttu-id="ffffc-172">Charger les données de test</span><span class="sxs-lookup"><span data-stu-id="ffffc-172">Load test data</span></span>

<span data-ttu-id="ffffc-173">Lorsque vous répliquez un cluster, vous devez spécifier hello tables tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="ffffc-173">When you replicate a cluster, you must specify hello tables tooreplicate.</span></span> <span data-ttu-id="ffffc-174">Dans cette section, vous allez charger des données dans un cluster de source de hello.</span><span class="sxs-lookup"><span data-stu-id="ffffc-174">In this section, you will load some data into hello source cluster.</span></span> <span data-ttu-id="ffffc-175">Dans la section suivante de hello, vous devez activer la réplication entre deux clusters de hello.</span><span class="sxs-lookup"><span data-stu-id="ffffc-175">In hello next section, you will enable replication between hello two clusters.</span></span>

<span data-ttu-id="ffffc-176">Suivez les instructions de hello dans [HBase didacticiel : prise en main Apache HBase avec basés sur Linux de Hadoop dans HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) toocreate un **Contacts** de table et d’insérer des données dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="ffffc-176">Follow hello instructions in [HBase tutorial: Get started using Apache HBase with Linux-based Hadoop in HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) toocreate a **Contacts** table and insert some data into hello table.</span></span>

## <a name="enable-replication"></a><span data-ttu-id="ffffc-177">Activer la réplication</span><span class="sxs-lookup"><span data-stu-id="ffffc-177">Enable replication</span></span>

<span data-ttu-id="ffffc-178">Hello suit montrent comment toocall hello script d’action de script à partir de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ffffc-178">hello following steps show how toocall hello script action script from hello Azure portal.</span></span> <span data-ttu-id="ffffc-179">Pour exécuter une action de script à l’aide d’Azure PowerShell et hello Azure interface de ligne de commande (CLI), consultez [HDInsight de basés sur Linux de personnaliser des clusters à l’aide d’action de script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="ffffc-179">For running a script action by using Azure PowerShell and hello Azure command-line interface (CLI), see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="ffffc-180">**réplication HBase tooenable hello portail Azure**</span><span class="sxs-lookup"><span data-stu-id="ffffc-180">**tooenable HBase replication from hello Azure portal**</span></span>

1. <span data-ttu-id="ffffc-181">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ffffc-181">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ffffc-182">Cluster de HBase hello Open source.</span><span class="sxs-lookup"><span data-stu-id="ffffc-182">Open hello source HBase cluster.</span></span>
3. <span data-ttu-id="ffffc-183">Dans le menu de cluster hello, cliquez sur **Actions de Script**.</span><span class="sxs-lookup"><span data-stu-id="ffffc-183">From hello cluster menu, click **Script Actions**.</span></span>
4. <span data-ttu-id="ffffc-184">Cliquez sur **soumettre de nouvelles** de haut hello du Panneau de hello.</span><span class="sxs-lookup"><span data-stu-id="ffffc-184">Click **Submit New** from hello top of hello blade.</span></span>
5. <span data-ttu-id="ffffc-185">Sélectionnez ou entrez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="ffffc-185">Select or enter hello following information:</span></span>

  - <span data-ttu-id="ffffc-186">**Nom** : saisissez **Activer la réplication**.</span><span class="sxs-lookup"><span data-stu-id="ffffc-186">**Name**: Enter **Enable replication**.</span></span>
  - <span data-ttu-id="ffffc-187">**Bash Script URL (URL de script bash)** : saisissez **https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_enable_replication.sh**.</span><span class="sxs-lookup"><span data-stu-id="ffffc-187">**Bash Script URL**: Enter **https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_enable_replication.sh**.</span></span>
  - <span data-ttu-id="ffffc-188">**Principal** : Sélectionné.</span><span class="sxs-lookup"><span data-stu-id="ffffc-188">**Head**: Selected.</span></span> <span data-ttu-id="ffffc-189">Bonjour clairement des autres types de nœuds.</span><span class="sxs-lookup"><span data-stu-id="ffffc-189">Clear hello other node types.</span></span>
  - <span data-ttu-id="ffffc-190">**Paramètres**: suivante de hello exemples de paramètres activer la réplication pour toutes les tables existantes hello et copier toutes les données hello du cluster de destination toohello hello source cluster :</span><span class="sxs-lookup"><span data-stu-id="ffffc-190">**Parameters**: hello following sample parameters enable replication for all hello existing tables and copy all hello data from hello source cluster toohello destination cluster:</span></span>

            -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -copydata

6. <span data-ttu-id="ffffc-191">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="ffffc-191">Click **Create**.</span></span> <span data-ttu-id="ffffc-192">script de Hello peut prendre un certain temps, en particulier lorsque l’argument de - copydata hello est utilisé.</span><span class="sxs-lookup"><span data-stu-id="ffffc-192">hello script can take some time, especially when hello -copydata argument is used.</span></span>

<span data-ttu-id="ffffc-193">Arguments requis :</span><span class="sxs-lookup"><span data-stu-id="ffffc-193">Required arguments:</span></span>

|<span data-ttu-id="ffffc-194">Nom</span><span class="sxs-lookup"><span data-stu-id="ffffc-194">Name</span></span>|<span data-ttu-id="ffffc-195">Description</span><span class="sxs-lookup"><span data-stu-id="ffffc-195">Description</span></span>|
|----|-----------|
|<span data-ttu-id="ffffc-196">-s, --src-cluster</span><span class="sxs-lookup"><span data-stu-id="ffffc-196">-s, --src-cluster</span></span> | <span data-ttu-id="ffffc-197">Spécifiez le nom DNS de hello du cluster de HBase hello source.</span><span class="sxs-lookup"><span data-stu-id="ffffc-197">Specify hello DNS name of hello source HBase cluster.</span></span> <span data-ttu-id="ffffc-198">Par exemple : -s hbsrccluster, --src-cluster=hbsrccluster</span><span class="sxs-lookup"><span data-stu-id="ffffc-198">For example: -s hbsrccluster, --src-cluster=hbsrccluster</span></span> |
|<span data-ttu-id="ffffc-199">-d, --dst-cluster</span><span class="sxs-lookup"><span data-stu-id="ffffc-199">-d, --dst-cluster</span></span> | <span data-ttu-id="ffffc-200">Spécifiez le nom DNS de hello de destination de hello (réplica) cluster HBase.</span><span class="sxs-lookup"><span data-stu-id="ffffc-200">Specify hello DNS name of hello destination (replica) HBase cluster.</span></span> <span data-ttu-id="ffffc-201">Par exemple : -s dsthbcluster, --src-cluster=dsthbcluster</span><span class="sxs-lookup"><span data-stu-id="ffffc-201">For example: -s dsthbcluster, --src-cluster=dsthbcluster</span></span> |
|<span data-ttu-id="ffffc-202">-sp, --src-ambari-password</span><span class="sxs-lookup"><span data-stu-id="ffffc-202">-sp, --src-ambari-password</span></span> | <span data-ttu-id="ffffc-203">Spécifiez un mot de passe administrateur hello pour Ambari sur un cluster HBase de source hello.</span><span class="sxs-lookup"><span data-stu-id="ffffc-203">Specify hello admin password for Ambari on hello source HBase cluster.</span></span> |
|<span data-ttu-id="ffffc-204">-dp, --dst-ambari-password</span><span class="sxs-lookup"><span data-stu-id="ffffc-204">-dp, --dst-ambari-password</span></span> | <span data-ttu-id="ffffc-205">Spécifiez un mot de passe administrateur hello pour Ambari sur un cluster HBase de destination hello.</span><span class="sxs-lookup"><span data-stu-id="ffffc-205">Specify hello admin password for Ambari on hello destination HBase cluster.</span></span>|

<span data-ttu-id="ffffc-206">Arguments facultatifs :</span><span class="sxs-lookup"><span data-stu-id="ffffc-206">Optional arguments:</span></span>

|<span data-ttu-id="ffffc-207">Nom</span><span class="sxs-lookup"><span data-stu-id="ffffc-207">Name</span></span>|<span data-ttu-id="ffffc-208">Description</span><span class="sxs-lookup"><span data-stu-id="ffffc-208">Description</span></span>|
|----|-----------|
|<span data-ttu-id="ffffc-209">-su, --src-ambari-user</span><span class="sxs-lookup"><span data-stu-id="ffffc-209">-su, --src-ambari-user</span></span> | <span data-ttu-id="ffffc-210">Spécifiez le nom d’utilisateur de hello admin pour Ambari sur un cluster HBase de source hello.</span><span class="sxs-lookup"><span data-stu-id="ffffc-210">Specify hello admin username for Ambari on hello source HBase cluster.</span></span> <span data-ttu-id="ffffc-211">la valeur par défaut Hello est **admin**.</span><span class="sxs-lookup"><span data-stu-id="ffffc-211">hello default value is **admin**.</span></span> |
|<span data-ttu-id="ffffc-212">-du, --dst-ambari-user</span><span class="sxs-lookup"><span data-stu-id="ffffc-212">-du, --dst-ambari-user</span></span> | <span data-ttu-id="ffffc-213">Spécifiez le nom d’utilisateur de hello admin pour Ambari sur un cluster HBase de destination hello.</span><span class="sxs-lookup"><span data-stu-id="ffffc-213">Specify hello admin username for Ambari on hello destination HBase cluster.</span></span> <span data-ttu-id="ffffc-214">la valeur par défaut Hello est **admin**.</span><span class="sxs-lookup"><span data-stu-id="ffffc-214">hello default value is **admin**.</span></span> |
|<span data-ttu-id="ffffc-215">-t, --table-list</span><span class="sxs-lookup"><span data-stu-id="ffffc-215">-t, --table-list</span></span> | <span data-ttu-id="ffffc-216">Spécifiez hello toobe de tables répliquée.</span><span class="sxs-lookup"><span data-stu-id="ffffc-216">Specify hello tables toobe replicated.</span></span> <span data-ttu-id="ffffc-217">Par exemple : --table-list="table1;table2;table3".</span><span class="sxs-lookup"><span data-stu-id="ffffc-217">For example: --table-list="table1;table2;table3".</span></span> <span data-ttu-id="ffffc-218">Si vous ne spécifiez pas de tables, toutes les tables HBase existantes sont répliquées.</span><span class="sxs-lookup"><span data-stu-id="ffffc-218">If you don't specify tables, all existing HBase tables are replicated.</span></span>|
|<span data-ttu-id="ffffc-219">-m, --machine</span><span class="sxs-lookup"><span data-stu-id="ffffc-219">-m, --machine</span></span> | <span data-ttu-id="ffffc-220">Spécifiez le nœud principal de hello où l’action de script hello s’exécutera.</span><span class="sxs-lookup"><span data-stu-id="ffffc-220">Specify hello head node where hello script action will run.</span></span> <span data-ttu-id="ffffc-221">valeur de Hello est hn1 ou hn0.</span><span class="sxs-lookup"><span data-stu-id="ffffc-221">hello value is either hn1 or hn0.</span></span> <span data-ttu-id="ffffc-222">La valeur hn0 étant généralement plus utilisée, nous vous recommandons de choisir hn1.</span><span class="sxs-lookup"><span data-stu-id="ffffc-222">Because hn0 is usually busier, we recommend using hn1.</span></span> <span data-ttu-id="ffffc-223">Vous utilisez cette option lorsque vous exécutez le script de hello $0 comme une action de script à partir de portail de HDInsight hello ou Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ffffc-223">You use this option when you're running hello $0 script as a script action from hello HDInsight portal or Azure PowerShell.</span></span>|
|<span data-ttu-id="ffffc-224">-ip</span><span class="sxs-lookup"><span data-stu-id="ffffc-224">-ip</span></span> | <span data-ttu-id="ffffc-225">Cet argument est obligatoire lorsque vous activez la réplication entre deux réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="ffffc-225">This argument is required when you're enabling replication between two virtual networks.</span></span> <span data-ttu-id="ffffc-226">Cet argument agit comme un commutateur toouse hello IPs de soigneur des nœuds statiques à partir de clusters de réplica au lieu des noms de domaine complets.</span><span class="sxs-lookup"><span data-stu-id="ffffc-226">This argument acts as a switch toouse hello static IPs of ZooKeeper nodes from replica clusters instead of FQDN names.</span></span> <span data-ttu-id="ffffc-227">Hello statique des adresses IP doivent toobe préconfiguré avant d’activer la réplication.</span><span class="sxs-lookup"><span data-stu-id="ffffc-227">hello static IPs need toobe preconfigured before you enable replication.</span></span> |
|<span data-ttu-id="ffffc-228">-cp, -copydata</span><span class="sxs-lookup"><span data-stu-id="ffffc-228">-cp, -copydata</span></span> | <span data-ttu-id="ffffc-229">Activez hello la migration des données existantes sur les tables hello où la réplication est activée.</span><span class="sxs-lookup"><span data-stu-id="ffffc-229">Enable hello migration of existing data on hello tables where replication is enabled.</span></span> |
|<span data-ttu-id="ffffc-230">-rpm, -replicate-phoenix-meta</span><span class="sxs-lookup"><span data-stu-id="ffffc-230">-rpm, -replicate-phoenix-meta</span></span> | <span data-ttu-id="ffffc-231">Activez la réplication sur les tables système Phoenix.</span><span class="sxs-lookup"><span data-stu-id="ffffc-231">Enable replication on Phoenix system tables.</span></span> <br><br><span data-ttu-id="ffffc-232">*Utilisez cette option avec précaution.*</span><span class="sxs-lookup"><span data-stu-id="ffffc-232">*Use this option with caution.*</span></span> <span data-ttu-id="ffffc-233">Nous vous recommandons de recréer des tables Phoenix sur les clusters de réplica avant d’utiliser ce script.</span><span class="sxs-lookup"><span data-stu-id="ffffc-233">We recommend that you re-create Phoenix tables on replica clusters before you use this script.</span></span> |
|<span data-ttu-id="ffffc-234">-h, --help</span><span class="sxs-lookup"><span data-stu-id="ffffc-234">-h, --help</span></span> | <span data-ttu-id="ffffc-235">Affichez des informations sur l’utilisation.</span><span class="sxs-lookup"><span data-stu-id="ffffc-235">Display usage information.</span></span> |

<span data-ttu-id="ffffc-236">Hello section print_usage() Hello [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_enable_replication.sh) fournit une explication détaillée des paramètres.</span><span class="sxs-lookup"><span data-stu-id="ffffc-236">hello print_usage() section of hello [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_enable_replication.sh) provides a detailed explanation of parameters.</span></span>

<span data-ttu-id="ffffc-237">Une fois l’action de script hello correctement déployé, vous pouvez utiliser SSH tooconnect toohello destination HBase cluster et vérifiez que les données de salutation ont été répliquées.</span><span class="sxs-lookup"><span data-stu-id="ffffc-237">After hello script action is successfully deployed, you can use SSH tooconnect toohello destination HBase cluster, and verify hello data has been replicated.</span></span>

### <a name="replication-scenarios"></a><span data-ttu-id="ffffc-238">Scénarios de réplication</span><span class="sxs-lookup"><span data-stu-id="ffffc-238">Replication scenarios</span></span>

<span data-ttu-id="ffffc-239">Hello liste suivante montre certains cas d’utilisation générales et leurs paramètres :</span><span class="sxs-lookup"><span data-stu-id="ffffc-239">hello following list shows you some general usage cases and their parameter settings:</span></span>

- <span data-ttu-id="ffffc-240">**Activer la réplication sur toutes les tables entre les clusters hello deux**.</span><span class="sxs-lookup"><span data-stu-id="ffffc-240">**Enable replication on all tables between hello two clusters**.</span></span> <span data-ttu-id="ffffc-241">Ce scénario ne nécessite pas de copie de hello/migration de données sur les tables de hello, et il n’utilise pas de tables de Phoenix.</span><span class="sxs-lookup"><span data-stu-id="ffffc-241">This scenario does not require hello copy/migration of existing data on hello tables, and it does not use Phoenix tables.</span></span> <span data-ttu-id="ffffc-242">Utilisez hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="ffffc-242">Use hello following parameters:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password>  

- <span data-ttu-id="ffffc-243">**Activer la réplication sur des tables spécifiques**.</span><span class="sxs-lookup"><span data-stu-id="ffffc-243">**Enable replication on specific tables**.</span></span> <span data-ttu-id="ffffc-244">Utilisez hello suivant la réplication tooenable paramètres table1, table2 et table3 :</span><span class="sxs-lookup"><span data-stu-id="ffffc-244">Use hello following parameters tooenable replication on table1, table2, and table3:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3"

- <span data-ttu-id="ffffc-245">**Activer la réplication sur des tables spécifiques et copier les données existantes hello**.</span><span class="sxs-lookup"><span data-stu-id="ffffc-245">**Enable replication on specific tables and copy hello existing data**.</span></span> <span data-ttu-id="ffffc-246">Utilisez hello suivant la réplication tooenable paramètres table1, table2 et table3 :</span><span class="sxs-lookup"><span data-stu-id="ffffc-246">Use hello following parameters tooenable replication on table1, table2, and table3:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -copydata

- <span data-ttu-id="ffffc-247">**Activer la réplication sur toutes les tables avec la réplication phoenix métadonnées à partir de la source toodestination**.</span><span class="sxs-lookup"><span data-stu-id="ffffc-247">**Enable replication on all tables with replicating phoenix metadata from source toodestination**.</span></span> <span data-ttu-id="ffffc-248">La réplication des métadonnées Phoenix n’est pas parfaite et doit être utilisée avec précaution.</span><span class="sxs-lookup"><span data-stu-id="ffffc-248">Phoenix metadata replication is not perfect and should be enabled with caution.</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -replicate-phoenix-meta

## <a name="copy-and-migrate-data"></a><span data-ttu-id="ffffc-249">Copier et migrer des données</span><span class="sxs-lookup"><span data-stu-id="ffffc-249">Copy and migrate data</span></span>

<span data-ttu-id="ffffc-250">Il existe deux scripts d’action de script distincts pour copier/migrer des données une fois la réplication activée :</span><span class="sxs-lookup"><span data-stu-id="ffffc-250">There are two separate script action scripts for copying/migrating data after replication is enabled:</span></span>

- <span data-ttu-id="ffffc-251">[Script pour les petites tables](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_copy_table.sh) (copie globale et taille de quelques gigaoctets est toofinish attendu dans moins d’une heure)</span><span class="sxs-lookup"><span data-stu-id="ffffc-251">[Script for small tables](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_copy_table.sh) (a few gigabytes in size, and overall copy is expected toofinish in less than one hour)</span></span>

- <span data-ttu-id="ffffc-252">[Script pour les tables volumineuses](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/nohup_hdi_copy_table.sh) (attendu tootake supérieure à une heure toocopy)</span><span class="sxs-lookup"><span data-stu-id="ffffc-252">[Script for large tables](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/nohup_hdi_copy_table.sh) (expected tootake longer than one hour toocopy)</span></span>

<span data-ttu-id="ffffc-253">Vous pouvez suivre hello même procédure dans [activer la réplication](#enable-replication) action de script toocall hello avec hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="ffffc-253">You can follow hello same procedure in [Enable replication](#enable-replication) toocall hello script action with hello following parameters:</span></span>

    -m hn1 -t <table1:start_timestamp:end_timestamp;table2:start_timestamp:end_timestamp;...> -p <replication_peer> [-everythingTillNow]

<span data-ttu-id="ffffc-254">Hello section print_usage() Hello [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_copy_table.sh) fournit une description détaillée des paramètres.</span><span class="sxs-lookup"><span data-stu-id="ffffc-254">hello print_usage() section of hello [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_copy_table.sh) provides a detailed description of parameters.</span></span>

### <a name="scenarios"></a><span data-ttu-id="ffffc-255">Scénarios</span><span class="sxs-lookup"><span data-stu-id="ffffc-255">Scenarios</span></span>

- <span data-ttu-id="ffffc-256">**Copier des tables spécifiques (test1, test2 et test3) pour toutes les lignes modifiées jusqu’à présent (horodatage actuel)** :</span><span class="sxs-lookup"><span data-stu-id="ffffc-256">**Copy specific tables (test1, test2, and test3) for all rows edited till now (current time stamp)**:</span></span>

        -m hn1 -t "test1::;test2::;test3::" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow
  <span data-ttu-id="ffffc-257">ou</span><span class="sxs-lookup"><span data-stu-id="ffffc-257">or</span></span>

        -m hn1 -t "test1::;test2::;test3::" --replication-peer="zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow


- <span data-ttu-id="ffffc-258">**Copier des tables spécifiques avec une plage horaire spécifiée** :</span><span class="sxs-lookup"><span data-stu-id="ffffc-258">**Copy specific tables with specified time range**:</span></span>

        -m hn1 -t "table1:0:452256397;table2:14141444:452256397" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure"


## <a name="disable-replication"></a><span data-ttu-id="ffffc-259">Désactiver la réplication</span><span class="sxs-lookup"><span data-stu-id="ffffc-259">Disable replication</span></span>

<span data-ttu-id="ffffc-260">toodisable la réplication, vous utilisez un autre script d’action de script situé [GitHub](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh).</span><span class="sxs-lookup"><span data-stu-id="ffffc-260">toodisable replication, you use another script action script located at [GitHub](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh).</span></span> <span data-ttu-id="ffffc-261">Vous pouvez suivre hello même procédure dans [activer la réplication](#enable-replication) action de script toocall hello avec hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="ffffc-261">You can follow hello same procedure in [Enable replication](#enable-replication) toocall hello script action with hello following parameters:</span></span>

    -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari Password> <-all|-t "table1;table2;...">  

<span data-ttu-id="ffffc-262">Hello section print_usage() Hello [script](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh) fournit une explication détaillée des paramètres.</span><span class="sxs-lookup"><span data-stu-id="ffffc-262">hello print_usage() section of hello [script](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh) provides a detailed explanation of parameters.</span></span>

### <a name="scenarios"></a><span data-ttu-id="ffffc-263">Scénarios</span><span class="sxs-lookup"><span data-stu-id="ffffc-263">Scenarios</span></span>

- <span data-ttu-id="ffffc-264">**Désactiver la réplication sur toutes les tables** :</span><span class="sxs-lookup"><span data-stu-id="ffffc-264">**Disable replication on all tables**:</span></span>

        -m hn1 -s <source cluster DNS name> -sp Mypassword\!789 -all
  <span data-ttu-id="ffffc-265">ou</span><span class="sxs-lookup"><span data-stu-id="ffffc-265">or</span></span>

        --src-cluster=<source cluster DNS name> --dst-cluster=<destination cluster DNS name> --src-ambari-user=<source cluster Ambari username> --src-ambari-password=<source cluster Ambari password>

- <span data-ttu-id="ffffc-266">**Désactiver la réplication sur les tables spécifiées (table1, table2 et table3)** :</span><span class="sxs-lookup"><span data-stu-id="ffffc-266">**Disable replication on specified tables (table1, table2, and table3)**:</span></span>

        -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari password> -t "table1;table2;table3"

## <a name="next-steps"></a><span data-ttu-id="ffffc-267">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ffffc-267">Next steps</span></span>

<span data-ttu-id="ffffc-268">Dans ce didacticiel, vous avez appris comment tooconfigure HBase la réplication entre deux centres de données.</span><span class="sxs-lookup"><span data-stu-id="ffffc-268">In this tutorial, you learned how tooconfigure HBase replication across two datacenters.</span></span> <span data-ttu-id="ffffc-269">toolearn en savoir plus sur HDInsight et HBase, consultez :</span><span class="sxs-lookup"><span data-stu-id="ffffc-269">toolearn more about HDInsight and HBase, see:</span></span>

* <span data-ttu-id="ffffc-270">[Didacticiel HBase : prise en main de HBase avec Hadoop dans HDInsight Linux][hdinsight-hbase-get-started]</span><span class="sxs-lookup"><span data-stu-id="ffffc-270">[Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started]</span></span>
* <span data-ttu-id="ffffc-271">[Présentation de HBase dans HDInsight : une base de données NoSQL fournissant des fonctionnalités similaires à BigTable pour Hadoop][hdinsight-hbase-overview]</span><span class="sxs-lookup"><span data-stu-id="ffffc-271">[HDInsight HBase overview][hdinsight-hbase-overview]</span></span>
* <span data-ttu-id="ffffc-272">[Création de clusters HBase dans un réseau virtuel Azure][hdinsight-hbase-provision-vnet]</span><span class="sxs-lookup"><span data-stu-id="ffffc-272">[Create HBase clusters in Azure Virtual Network][hdinsight-hbase-provision-vnet]</span></span>
* <span data-ttu-id="ffffc-273">[Analyse de sentiments Twitter en temps réel avec HBase dans HDInsight][hdinsight-hbase-twitter-sentiment]</span><span class="sxs-lookup"><span data-stu-id="ffffc-273">[Analyze real-time Twitter sentiment with HBase][hdinsight-hbase-twitter-sentiment]</span></span>
* <span data-ttu-id="ffffc-274">[Analyse des données de capteur avec Storm et HBase dans HDInsight (Hadoop)][hdinsight-sensor-data]</span><span class="sxs-lookup"><span data-stu-id="ffffc-274">[Analyzing sensor data with Storm and HBase in HDInsight (Hadoop)][hdinsight-sensor-data]</span></span>

[hdinsight-hbase-geo-replication-vnet]: hdinsight-hbase-geo-replication-configure-vnets.md
[hdinsight-hbase-geo-replication-dns]: ../hdinsight-hbase-geo-replication-configure-VNet.md


[img-vnet-diagram]: ./media/hdinsight-hbase-geo-replication/HDInsight.HBase.Replication.Network.diagram.png

[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started-linux.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[hdinsight-sensor-data]: hdinsight-storm-sensor-data-analysis.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
