---
title: "Configurer la réplication de cluster HBase dans les réseaux virtuels - Azure | Microsoft Docs"
description: "Apprenez à configurer la réplication HBase pour l’équilibrage de charge, la haute disponibilité, la mise à jour/migration sans interruption de service d’une version HDInsight à une autre, ainsi que la récupération d’urgence."
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
ms.openlocfilehash: 895709391486acb4a9d7a54ef046956539913f7b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-hbase-cluster-replication-within-virtual-networks"></a><span data-ttu-id="0165f-103">Configurer la réplication de cluster HBase dans les réseaux virtuels</span><span class="sxs-lookup"><span data-stu-id="0165f-103">Configure HBase cluster replication within virtual networks</span></span>

<span data-ttu-id="0165f-104">Apprenez à configurer la réplication HBase dans un réseau virtuel ou entre deux réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="0165f-104">Learn how to configure HBase replication within one virtual network (VNet) or between two virtual networks.</span></span>

<span data-ttu-id="0165f-105">La réplication en cluster utilise une méthodologie par émission de données source.</span><span class="sxs-lookup"><span data-stu-id="0165f-105">Cluster replication uses a source-push methodology.</span></span> <span data-ttu-id="0165f-106">Un cluster HBase peut être une source, une destination ou jouer les deux rôles à la fois.</span><span class="sxs-lookup"><span data-stu-id="0165f-106">An HBase cluster can be a source or a destination, or it can fulfill both roles at once.</span></span> <span data-ttu-id="0165f-107">La réplication est asynchrone et l'objectif de la réplication est une cohérence éventuelle.</span><span class="sxs-lookup"><span data-stu-id="0165f-107">Replication is asynchronous, and the goal of replication is eventual consistency.</span></span> <span data-ttu-id="0165f-108">Quand la source reçoit une modification apportée à une famille de colonnes dont la réplication est activée, cette modification est propagée à tous les clusters de destination.</span><span class="sxs-lookup"><span data-stu-id="0165f-108">When the source receives an edit to a column family with replication enabled, that edit is propagated to all destination clusters.</span></span> <span data-ttu-id="0165f-109">Quand les données sont répliquées d’un cluster à un autre, le cluster source et tous les clusters qui ont déjà utilisé les données font l’objet d’un suivi afin d’empêcher les boucles de réplication.</span><span class="sxs-lookup"><span data-stu-id="0165f-109">When data is replicated from one cluster to another, the source cluster and all clusters that have already consumed the data are tracked to prevent replication loops.</span></span>

<span data-ttu-id="0165f-110">Dans ce didacticiel, vous allez configurer une réplication source-destination.</span><span class="sxs-lookup"><span data-stu-id="0165f-110">In this tutorial, you will configure a source-destination replication.</span></span> <span data-ttu-id="0165f-111">Pour d'autres topologies de cluster, consultez le [Guide de référence d'Apache HBase](http://hbase.apache.org/book.html#_cluster_replication).</span><span class="sxs-lookup"><span data-stu-id="0165f-111">For other cluster topologies, see [Apache HBase Reference Guide](http://hbase.apache.org/book.html#_cluster_replication).</span></span>

<span data-ttu-id="0165f-112">Cas d’utilisation de la réplication HBase pour un seul réseau virtuel :</span><span class="sxs-lookup"><span data-stu-id="0165f-112">HBase replication usage cases for a single virtual network:</span></span>

* <span data-ttu-id="0165f-113">Équilibrage de charge, par exemple, l’exécution d’analyses ou de travaux MapReduce sur le cluster de destination et l’ingestion de données sur le cluster source</span><span class="sxs-lookup"><span data-stu-id="0165f-113">Load balancing--for example, running scans or MapReduce jobs on the destination cluster and ingesting data on the source cluster</span></span>
* <span data-ttu-id="0165f-114">Haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="0165f-114">High availability</span></span>
* <span data-ttu-id="0165f-115">Migration des données à partir d’un cluster HBase vers un autre</span><span class="sxs-lookup"><span data-stu-id="0165f-115">Migrating data from one HBase cluster to another</span></span>
* <span data-ttu-id="0165f-116">Mise à niveau d’un cluster Azure HDInsight à partir d’une version vers une autre</span><span class="sxs-lookup"><span data-stu-id="0165f-116">Upgrading an Azure HDInsight cluster from one version to another</span></span>

<span data-ttu-id="0165f-117">Cas d’utilisation de la réplication HBase pour deux réseaux virtuels :</span><span class="sxs-lookup"><span data-stu-id="0165f-117">HBase replication usage cases for two virtual networks:</span></span>

* <span data-ttu-id="0165f-118">Récupération d'urgence</span><span class="sxs-lookup"><span data-stu-id="0165f-118">Disaster recovery</span></span>
* <span data-ttu-id="0165f-119">Équilibrage de charge et partitionnement de l’application</span><span class="sxs-lookup"><span data-stu-id="0165f-119">Load balancing and partitioning the application</span></span>
* <span data-ttu-id="0165f-120">Haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="0165f-120">High availability</span></span>

<span data-ttu-id="0165f-121">Vous répliquez des clusters à l’aide de scripts [d’action de script](hdinsight-hadoop-customize-cluster-linux.md) disponibles dans [GitHub](https://github.com/Azure/hbase-utils/tree/master/replication).</span><span class="sxs-lookup"><span data-stu-id="0165f-121">You replicate clusters by using [script action](hdinsight-hadoop-customize-cluster-linux.md) scripts located at [GitHub](https://github.com/Azure/hbase-utils/tree/master/replication).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0165f-122">Composants requis</span><span class="sxs-lookup"><span data-stu-id="0165f-122">Prerequisites</span></span>
<span data-ttu-id="0165f-123">Avant de commencer ce didacticiel, vous devez disposer d’un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="0165f-123">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="0165f-124">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="0165f-124">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="configure-the-environments"></a><span data-ttu-id="0165f-125">Configurer les environnements</span><span class="sxs-lookup"><span data-stu-id="0165f-125">Configure the environments</span></span>

<span data-ttu-id="0165f-126">Il existe trois options de configuration :</span><span class="sxs-lookup"><span data-stu-id="0165f-126">There are three possible configurations:</span></span>

- <span data-ttu-id="0165f-127">Deux clusters HBase dans un réseau virtuel Azure</span><span class="sxs-lookup"><span data-stu-id="0165f-127">Two HBase clusters in one Azure virtual network</span></span>
- <span data-ttu-id="0165f-128">Deux clusters HBase dans deux réseaux virtuels différents dans la même région</span><span class="sxs-lookup"><span data-stu-id="0165f-128">Two HBase clusters in two different virtual networks in the same region</span></span>
- <span data-ttu-id="0165f-129">Deux clusters HBase dans deux réseaux virtuels différents dans deux régions distinctes (géoréplication)</span><span class="sxs-lookup"><span data-stu-id="0165f-129">Two HBase clusters in two different virtual networks in two different regions (geo-replication)</span></span>

<span data-ttu-id="0165f-130">Pour simplifier la configuration des environnements, nous avons créé quelques [modèles Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0165f-130">To make it easier to configure the environments, we have created some [Azure Resource Manager templates](../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="0165f-131">Si vous préférez configurer les environnements en utilisant d’autres méthodes, consultez :</span><span class="sxs-lookup"><span data-stu-id="0165f-131">If you prefer to configure the environments by using other methods, see:</span></span>

- [<span data-ttu-id="0165f-132">Création de clusters Hadoop basés sur Linux dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="0165f-132">Create Linux-based Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
- [<span data-ttu-id="0165f-133">Création de clusters HBase dans un réseau virtuel Azure</span><span class="sxs-lookup"><span data-stu-id="0165f-133">Create HBase clusters in Azure Virtual Network</span></span>](hdinsight-hbase-provision-vnet.md)

### <a name="configure-one-virtual-network"></a><span data-ttu-id="0165f-134">Configurer un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="0165f-134">Configure one virtual network</span></span>

<span data-ttu-id="0165f-135">Cliquez sur l’image suivante pour créer deux clusters HBase dans le même réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="0165f-135">Click the following image to create two HBase clusters in the same virtual network.</span></span> <span data-ttu-id="0165f-136">Ce modèle est stocké dans les [modèles de démarrage rapide Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-one-vnet/).</span><span class="sxs-lookup"><span data-stu-id="0165f-136">The template is stored in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-one-vnet/).</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-one-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy to Azure"></a>

### <a name="configure-two-virtual-networks-in-the-same-region"></a><span data-ttu-id="0165f-137">Configurer deux réseaux virtuels dans la même région</span><span class="sxs-lookup"><span data-stu-id="0165f-137">Configure two virtual networks in the same region</span></span>

<span data-ttu-id="0165f-138">Cliquez sur l’image suivante pour créer deux réseaux virtuels avec homologation de réseaux virtuels et deux clusters HBase dans la même région.</span><span class="sxs-lookup"><span data-stu-id="0165f-138">Click the following image to create two virtual networks with VNet peering and two HBase clusters in the same region.</span></span> <span data-ttu-id="0165f-139">Ce modèle est stocké dans les [modèles de démarrage rapide Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-two-vnets-same-region/).</span><span class="sxs-lookup"><span data-stu-id="0165f-139">The template is stored in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-two-vnets-same-region/).</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-two-vnets-same-region%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy to Azure"></a>



<span data-ttu-id="0165f-140">Ce scénario nécessite [l’homologation de réseaux virtuels](../virtual-network/virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0165f-140">This scenario requires [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span> <span data-ttu-id="0165f-141">Le modèle permet l’homologation de réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="0165f-141">The template enables VNet peering.</span></span>   

<span data-ttu-id="0165f-142">La réplication HBase utilise des adresses IP des machines virtuelles ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="0165f-142">HBase replication uses IP addresses of the ZooKeeper VMs.</span></span> <span data-ttu-id="0165f-143">Vous devez configurer des adresses IP statiques pour les nœuds ZooKeeper HBase de destination.</span><span class="sxs-lookup"><span data-stu-id="0165f-143">You must configure static IP addresses for the destination HBase ZooKeeper nodes.</span></span>

<span data-ttu-id="0165f-144">**Pour configurer des adresses IP statiques**</span><span class="sxs-lookup"><span data-stu-id="0165f-144">**To configure static IP addresses**</span></span>

1. <span data-ttu-id="0165f-145">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0165f-145">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0165f-146">Dans le menu de gauche, cliquez sur **Groupes de ressources**.</span><span class="sxs-lookup"><span data-stu-id="0165f-146">From the left menu, click **Resource Groups**.</span></span>
3. <span data-ttu-id="0165f-147">Cliquez sur votre groupe de ressources qui contient le cluster HBase de destination.</span><span class="sxs-lookup"><span data-stu-id="0165f-147">Click your resource group that contains the destination HBase cluster.</span></span> <span data-ttu-id="0165f-148">Il s’agit du groupe de ressources que vous avez spécifié lorsque vous avez utilisé le modèle Resource Manager pour créer l’environnement.</span><span class="sxs-lookup"><span data-stu-id="0165f-148">This is the resource group that you specified when you used the Resource Manager template to create the environment.</span></span> <span data-ttu-id="0165f-149">Vous pouvez utiliser le filtre pour restreindre la liste.</span><span class="sxs-lookup"><span data-stu-id="0165f-149">You can use the filter to narrow down the list.</span></span> <span data-ttu-id="0165f-150">Vous pouvez voir une liste de ressources qui contient les deux réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="0165f-150">You can see a list of resources that contains the two virtual networks.</span></span>
4. <span data-ttu-id="0165f-151">Cliquez sur le réseau virtuel qui contient le cluster HBase de destination.</span><span class="sxs-lookup"><span data-stu-id="0165f-151">Click the virtual network that contains the destination HBase cluster.</span></span> <span data-ttu-id="0165f-152">Par exemple, cliquez sur **xxxx-vnet2**.</span><span class="sxs-lookup"><span data-stu-id="0165f-152">For example, click **xxxx-vnet2**.</span></span> <span data-ttu-id="0165f-153">Vous pouvez voir trois appareils avec des noms qui commencent par **nic-zookeepermode-**.</span><span class="sxs-lookup"><span data-stu-id="0165f-153">You can see three devices with names that start with **nic-zookeepermode-**.</span></span> <span data-ttu-id="0165f-154">Ces appareils sont les trois machines virtuelles ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="0165f-154">Those devices are the three ZooKeeper VMs.</span></span>
5. <span data-ttu-id="0165f-155">Cliquez sur l’une des machines virtuelles ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="0165f-155">Click one of the ZooKeeper VMs.</span></span>
6. <span data-ttu-id="0165f-156">Cliquez sur **Configurations IP**.</span><span class="sxs-lookup"><span data-stu-id="0165f-156">Click **IP configurations**.</span></span>
7. <span data-ttu-id="0165f-157">Dans la liste, cliquez sur **ipConfig1**.</span><span class="sxs-lookup"><span data-stu-id="0165f-157">Click **ipConfig1** from the list.</span></span>
8. <span data-ttu-id="0165f-158">Cliquez sur **Statique**et notez l’adresse IP réelle.</span><span class="sxs-lookup"><span data-stu-id="0165f-158">Click **Static**, and write down the actual IP address.</span></span> <span data-ttu-id="0165f-159">Lorsque vous exécutez l’action de script pour activer la réplication, vous avez besoin de l’adresse IP.</span><span class="sxs-lookup"><span data-stu-id="0165f-159">You will need the IP address when you run the script action to enable replication.</span></span>

  ![Adresse IP statique ZooKeeper de réplication HDInsight HBase](./media/hdinsight-hbase-replication/hdinsight-hbase-replication-zookeeper-static-ip.png)

9. <span data-ttu-id="0165f-161">Répétez l’étape 6 pour définir l’adresse IP statique des deux autres nœuds ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="0165f-161">Repeat step 6 to set the static IP address for the other two ZooKeeper nodes.</span></span>

<span data-ttu-id="0165f-162">Pour le scénario de réseaux virtuels croisés (cross-VNet), vous devez utiliser le commutateur **-ip** lors de l’appel de l’action de script **hdi_enable_replication.sh**.</span><span class="sxs-lookup"><span data-stu-id="0165f-162">For the cross-VNet scenario, you must use the **-ip** switch when calling the **hdi_enable_replication.sh** script action.</span></span>

### <a name="configure-two-virtual-networks-in-two-different-regions"></a><span data-ttu-id="0165f-163">Configurer deux réseaux virtuels dans deux régions différentes</span><span class="sxs-lookup"><span data-stu-id="0165f-163">Configure two virtual networks in two different regions</span></span>

<span data-ttu-id="0165f-164">Cliquez sur l’image suivante pour créer deux réseaux virtuels dans deux régions différentes.</span><span class="sxs-lookup"><span data-stu-id="0165f-164">Click the following image to create two virtual networks in two different regions.</span></span> <span data-ttu-id="0165f-165">Le modèle est stocké dans un conteneur de blobs Azure public.</span><span class="sxs-lookup"><span data-stu-id="0165f-165">The template is stored in a public Azure Blob container.</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fhbaseha%2Fdeploy-hbase-geo-replication.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy to Azure"></a>

<span data-ttu-id="0165f-166">Créez une passerelle VPN entre les deux réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="0165f-166">Create a VPN gateway between the two virtual networks.</span></span> <span data-ttu-id="0165f-167">Pour savoir comment faire, consultez [Création d’un réseau virtuel avec une connexion de site à site à l’aide du portail Azure](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0165f-167">For instructions, see [Create a VNet with a site-to-site connection](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).</span></span>

<span data-ttu-id="0165f-168">La réplication HBase utilise des adresses IP des machines virtuelles ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="0165f-168">HBase replication uses IP addresses of the ZooKeeper VMs.</span></span> <span data-ttu-id="0165f-169">Vous devez configurer des adresses IP statiques pour les nœuds ZooKeeper HBase de destination.</span><span class="sxs-lookup"><span data-stu-id="0165f-169">You must configure static IP addresses for the destination HBase ZooKeeper nodes.</span></span> <span data-ttu-id="0165f-170">Pour configurer une adresse IP statique, consultez la section « Configurer deux réseaux virtuels dans la même région » de cet article.</span><span class="sxs-lookup"><span data-stu-id="0165f-170">To configure static IP, see the "Configure two virtual networks in the same region" section in this article.</span></span>

<span data-ttu-id="0165f-171">Pour le scénario de réseaux virtuels croisés (cross-VNet), vous devez utiliser le commutateur **-ip** lors de l’appel de l’action de script **hdi_enable_replication.sh**.</span><span class="sxs-lookup"><span data-stu-id="0165f-171">For the cross-VNet scenario, you must use the **-ip** switch when calling the **hdi_enable_replication.sh** script action.</span></span>

## <a name="load-test-data"></a><span data-ttu-id="0165f-172">Charger les données de test</span><span class="sxs-lookup"><span data-stu-id="0165f-172">Load test data</span></span>

<span data-ttu-id="0165f-173">Lorsque vous répliquez un cluster, vous devez spécifier les tables à répliquer.</span><span class="sxs-lookup"><span data-stu-id="0165f-173">When you replicate a cluster, you must specify the tables to replicate.</span></span> <span data-ttu-id="0165f-174">Dans cette section, vous allez charger des données dans le cluster source.</span><span class="sxs-lookup"><span data-stu-id="0165f-174">In this section, you will load some data into the source cluster.</span></span> <span data-ttu-id="0165f-175">Dans la section suivante, vous allez activer la réplication entre les deux clusters.</span><span class="sxs-lookup"><span data-stu-id="0165f-175">In the next section, you will enable replication between the two clusters.</span></span>

<span data-ttu-id="0165f-176">Suivez les instructions de [Didacticiel HBase : prise en main de HBase avec Hadoop dans HDInsight Linux](hdinsight-hbase-tutorial-get-started-linux.md) pour créer une table **Contacts** et insérer des données dans la table.</span><span class="sxs-lookup"><span data-stu-id="0165f-176">Follow the instructions in [HBase tutorial: Get started using Apache HBase with Linux-based Hadoop in HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) to create a **Contacts** table and insert some data into the table.</span></span>

## <a name="enable-replication"></a><span data-ttu-id="0165f-177">Activer la réplication</span><span class="sxs-lookup"><span data-stu-id="0165f-177">Enable replication</span></span>

<span data-ttu-id="0165f-178">Les étapes suivantes montrent comment appeler le script d’action de script à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0165f-178">The following steps show how to call the script action script from the Azure portal.</span></span> <span data-ttu-id="0165f-179">Pour exécuter une action de script à l’aide d’Azure PowerShell et de l’interface de ligne de commande Azure, consultez [Personnalisation de clusters HDInsight basés sur Linux à l’aide d’une action de script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="0165f-179">For running a script action by using Azure PowerShell and the Azure command-line interface (CLI), see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="0165f-180">**Pour activer la réplication HBase à partir du portail Azure**</span><span class="sxs-lookup"><span data-stu-id="0165f-180">**To enable HBase replication from the Azure portal**</span></span>

1. <span data-ttu-id="0165f-181">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0165f-181">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0165f-182">Ouvrez le cluster HBase source.</span><span class="sxs-lookup"><span data-stu-id="0165f-182">Open the source HBase cluster.</span></span>
3. <span data-ttu-id="0165f-183">Dans le menu de cluster, cliquez sur **Actions de script**.</span><span class="sxs-lookup"><span data-stu-id="0165f-183">From the cluster menu, click **Script Actions**.</span></span>
4. <span data-ttu-id="0165f-184">En haut du panneau, cliquez sur **Envoyer**.</span><span class="sxs-lookup"><span data-stu-id="0165f-184">Click **Submit New** from the top of the blade.</span></span>
5. <span data-ttu-id="0165f-185">Sélectionnez ou saisissez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="0165f-185">Select or enter the following information:</span></span>

  - <span data-ttu-id="0165f-186">**Nom** : saisissez **Activer la réplication**.</span><span class="sxs-lookup"><span data-stu-id="0165f-186">**Name**: Enter **Enable replication**.</span></span>
  - <span data-ttu-id="0165f-187">**Bash Script URL (URL de script bash)** : saisissez **https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_enable_replication.sh**.</span><span class="sxs-lookup"><span data-stu-id="0165f-187">**Bash Script URL**: Enter **https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_enable_replication.sh**.</span></span>
  - <span data-ttu-id="0165f-188">**Principal** : Sélectionné.</span><span class="sxs-lookup"><span data-stu-id="0165f-188">**Head**: Selected.</span></span> <span data-ttu-id="0165f-189">Supprimez les autres types de nœuds.</span><span class="sxs-lookup"><span data-stu-id="0165f-189">Clear the other node types.</span></span>
  - <span data-ttu-id="0165f-190">**Paramètres** : les paramètres d’exemple suivants activent la réplication pour toutes les tables existantes et copient toutes les données du cluster source vers le cluster de destination :</span><span class="sxs-lookup"><span data-stu-id="0165f-190">**Parameters**: The following sample parameters enable replication for all the existing tables and copy all the data from the source cluster to the destination cluster:</span></span>

            -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -copydata

6. <span data-ttu-id="0165f-191">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="0165f-191">Click **Create**.</span></span> <span data-ttu-id="0165f-192">L’exécution du script peut prendre un certain temps, en particulier lorsque l’argument -copydata est utilisé.</span><span class="sxs-lookup"><span data-stu-id="0165f-192">The script can take some time, especially when the -copydata argument is used.</span></span>

<span data-ttu-id="0165f-193">Arguments requis :</span><span class="sxs-lookup"><span data-stu-id="0165f-193">Required arguments:</span></span>

|<span data-ttu-id="0165f-194">Nom</span><span class="sxs-lookup"><span data-stu-id="0165f-194">Name</span></span>|<span data-ttu-id="0165f-195">Description</span><span class="sxs-lookup"><span data-stu-id="0165f-195">Description</span></span>|
|----|-----------|
|<span data-ttu-id="0165f-196">-s, --src-cluster</span><span class="sxs-lookup"><span data-stu-id="0165f-196">-s, --src-cluster</span></span> | <span data-ttu-id="0165f-197">Spécifiez le nom DNS du cluster HBase source.</span><span class="sxs-lookup"><span data-stu-id="0165f-197">Specify the DNS name of the source HBase cluster.</span></span> <span data-ttu-id="0165f-198">Par exemple : -s hbsrccluster, --src-cluster=hbsrccluster</span><span class="sxs-lookup"><span data-stu-id="0165f-198">For example: -s hbsrccluster, --src-cluster=hbsrccluster</span></span> |
|<span data-ttu-id="0165f-199">-d, --dst-cluster</span><span class="sxs-lookup"><span data-stu-id="0165f-199">-d, --dst-cluster</span></span> | <span data-ttu-id="0165f-200">Spécifiez le nom DNS du cluster HBase de destination (réplica).</span><span class="sxs-lookup"><span data-stu-id="0165f-200">Specify the DNS name of the destination (replica) HBase cluster.</span></span> <span data-ttu-id="0165f-201">Par exemple : -s dsthbcluster, --src-cluster=dsthbcluster</span><span class="sxs-lookup"><span data-stu-id="0165f-201">For example: -s dsthbcluster, --src-cluster=dsthbcluster</span></span> |
|<span data-ttu-id="0165f-202">-sp, --src-ambari-password</span><span class="sxs-lookup"><span data-stu-id="0165f-202">-sp, --src-ambari-password</span></span> | <span data-ttu-id="0165f-203">Spécifiez le mot de passe d’administrateur pour Ambari sur le cluster HBase source.</span><span class="sxs-lookup"><span data-stu-id="0165f-203">Specify the admin password for Ambari on the source HBase cluster.</span></span> |
|<span data-ttu-id="0165f-204">-dp, --dst-ambari-password</span><span class="sxs-lookup"><span data-stu-id="0165f-204">-dp, --dst-ambari-password</span></span> | <span data-ttu-id="0165f-205">Spécifiez le mot de passe d’administrateur pour Ambari sur le cluster HBase de destination.</span><span class="sxs-lookup"><span data-stu-id="0165f-205">Specify the admin password for Ambari on the destination HBase cluster.</span></span>|

<span data-ttu-id="0165f-206">Arguments facultatifs :</span><span class="sxs-lookup"><span data-stu-id="0165f-206">Optional arguments:</span></span>

|<span data-ttu-id="0165f-207">Nom</span><span class="sxs-lookup"><span data-stu-id="0165f-207">Name</span></span>|<span data-ttu-id="0165f-208">Description</span><span class="sxs-lookup"><span data-stu-id="0165f-208">Description</span></span>|
|----|-----------|
|<span data-ttu-id="0165f-209">-su, --src-ambari-user</span><span class="sxs-lookup"><span data-stu-id="0165f-209">-su, --src-ambari-user</span></span> | <span data-ttu-id="0165f-210">Spécifiez le nom d’utilisateur administrateur pour Ambari sur le cluster HBase source.</span><span class="sxs-lookup"><span data-stu-id="0165f-210">Specify the admin username for Ambari on the source HBase cluster.</span></span> <span data-ttu-id="0165f-211">La valeur par défaut est **admin**.</span><span class="sxs-lookup"><span data-stu-id="0165f-211">The default value is **admin**.</span></span> |
|<span data-ttu-id="0165f-212">-du, --dst-ambari-user</span><span class="sxs-lookup"><span data-stu-id="0165f-212">-du, --dst-ambari-user</span></span> | <span data-ttu-id="0165f-213">Spécifiez le nom d’utilisateur administrateur pour Ambari sur le cluster HBase de destination.</span><span class="sxs-lookup"><span data-stu-id="0165f-213">Specify the admin username for Ambari on the destination HBase cluster.</span></span> <span data-ttu-id="0165f-214">La valeur par défaut est **admin**.</span><span class="sxs-lookup"><span data-stu-id="0165f-214">The default value is **admin**.</span></span> |
|<span data-ttu-id="0165f-215">-t, --table-list</span><span class="sxs-lookup"><span data-stu-id="0165f-215">-t, --table-list</span></span> | <span data-ttu-id="0165f-216">Spécifiez les tables à répliquer.</span><span class="sxs-lookup"><span data-stu-id="0165f-216">Specify the tables to be replicated.</span></span> <span data-ttu-id="0165f-217">Par exemple : --table-list="table1;table2;table3".</span><span class="sxs-lookup"><span data-stu-id="0165f-217">For example: --table-list="table1;table2;table3".</span></span> <span data-ttu-id="0165f-218">Si vous ne spécifiez pas de tables, toutes les tables HBase existantes sont répliquées.</span><span class="sxs-lookup"><span data-stu-id="0165f-218">If you don't specify tables, all existing HBase tables are replicated.</span></span>|
|<span data-ttu-id="0165f-219">-m, --machine</span><span class="sxs-lookup"><span data-stu-id="0165f-219">-m, --machine</span></span> | <span data-ttu-id="0165f-220">Spécifiez le nœud principal sur lequel l’action de script s’exécute.</span><span class="sxs-lookup"><span data-stu-id="0165f-220">Specify the head node where the script action will run.</span></span> <span data-ttu-id="0165f-221">La valeur peut être hn1 ou hn0.</span><span class="sxs-lookup"><span data-stu-id="0165f-221">The value is either hn1 or hn0.</span></span> <span data-ttu-id="0165f-222">La valeur hn0 étant généralement plus utilisée, nous vous recommandons de choisir hn1.</span><span class="sxs-lookup"><span data-stu-id="0165f-222">Because hn0 is usually busier, we recommend using hn1.</span></span> <span data-ttu-id="0165f-223">Vous utilisez cette option lorsque vous exécutez le script $0 comme une action de script à partir du portail HDInsight ou d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0165f-223">You use this option when you're running the $0 script as a script action from the HDInsight portal or Azure PowerShell.</span></span>|
|<span data-ttu-id="0165f-224">-ip</span><span class="sxs-lookup"><span data-stu-id="0165f-224">-ip</span></span> | <span data-ttu-id="0165f-225">Cet argument est obligatoire lorsque vous activez la réplication entre deux réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="0165f-225">This argument is required when you're enabling replication between two virtual networks.</span></span> <span data-ttu-id="0165f-226">Cet argument agit comme un commutateur pour utiliser les adresses IP statiques des nœuds ZooKeeper à partir de clusters de réplica au lieu des noms de domaine complets.</span><span class="sxs-lookup"><span data-stu-id="0165f-226">This argument acts as a switch to use the static IPs of ZooKeeper nodes from replica clusters instead of FQDN names.</span></span> <span data-ttu-id="0165f-227">Les adresses IP statiques doivent être préconfigurées avant d’activer la réplication.</span><span class="sxs-lookup"><span data-stu-id="0165f-227">The static IPs need to be preconfigured before you enable replication.</span></span> |
|<span data-ttu-id="0165f-228">-cp, -copydata</span><span class="sxs-lookup"><span data-stu-id="0165f-228">-cp, -copydata</span></span> | <span data-ttu-id="0165f-229">Activez la migration des données existantes sur les tables pour lesquelles la réplication est activée.</span><span class="sxs-lookup"><span data-stu-id="0165f-229">Enable the migration of existing data on the tables where replication is enabled.</span></span> |
|<span data-ttu-id="0165f-230">-rpm, -replicate-phoenix-meta</span><span class="sxs-lookup"><span data-stu-id="0165f-230">-rpm, -replicate-phoenix-meta</span></span> | <span data-ttu-id="0165f-231">Activez la réplication sur les tables système Phoenix.</span><span class="sxs-lookup"><span data-stu-id="0165f-231">Enable replication on Phoenix system tables.</span></span> <br><br><span data-ttu-id="0165f-232">*Utilisez cette option avec précaution.*</span><span class="sxs-lookup"><span data-stu-id="0165f-232">*Use this option with caution.*</span></span> <span data-ttu-id="0165f-233">Nous vous recommandons de recréer des tables Phoenix sur les clusters de réplica avant d’utiliser ce script.</span><span class="sxs-lookup"><span data-stu-id="0165f-233">We recommend that you re-create Phoenix tables on replica clusters before you use this script.</span></span> |
|<span data-ttu-id="0165f-234">-h, --help</span><span class="sxs-lookup"><span data-stu-id="0165f-234">-h, --help</span></span> | <span data-ttu-id="0165f-235">Affichez des informations sur l’utilisation.</span><span class="sxs-lookup"><span data-stu-id="0165f-235">Display usage information.</span></span> |

<span data-ttu-id="0165f-236">La section print_usage() du [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_enable_replication.sh) fournit une explication détaillée des paramètres.</span><span class="sxs-lookup"><span data-stu-id="0165f-236">The print_usage() section of the [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_enable_replication.sh) provides a detailed explanation of parameters.</span></span>

<span data-ttu-id="0165f-237">Une fois le déploiement de l’action de script terminé, vous pouvez utiliser SSH pour vous connecter au cluster HBase de destination et vérifier que les données ont été répliquées.</span><span class="sxs-lookup"><span data-stu-id="0165f-237">After the script action is successfully deployed, you can use SSH to connect to the destination HBase cluster, and verify the data has been replicated.</span></span>

### <a name="replication-scenarios"></a><span data-ttu-id="0165f-238">Scénarios de réplication</span><span class="sxs-lookup"><span data-stu-id="0165f-238">Replication scenarios</span></span>

<span data-ttu-id="0165f-239">La liste suivante présente certains cas d’utilisation générale et la définition de leurs paramètres :</span><span class="sxs-lookup"><span data-stu-id="0165f-239">The following list shows you some general usage cases and their parameter settings:</span></span>

- <span data-ttu-id="0165f-240">**Activer la réplication sur toutes les tables entre les deux clusters**.</span><span class="sxs-lookup"><span data-stu-id="0165f-240">**Enable replication on all tables between the two clusters**.</span></span> <span data-ttu-id="0165f-241">Ce scénario ne nécessite pas la copie/migration des données existantes sur les tables, et n’utilise pas de tables Phoenix.</span><span class="sxs-lookup"><span data-stu-id="0165f-241">This scenario does not require the copy/migration of existing data on the tables, and it does not use Phoenix tables.</span></span> <span data-ttu-id="0165f-242">Utilisez les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="0165f-242">Use the following parameters:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password>  

- <span data-ttu-id="0165f-243">**Activer la réplication sur des tables spécifiques**.</span><span class="sxs-lookup"><span data-stu-id="0165f-243">**Enable replication on specific tables**.</span></span> <span data-ttu-id="0165f-244">Pour activer la réplication sur table1, table2 et table3, utilisez les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="0165f-244">Use the following parameters to enable replication on table1, table2, and table3:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3"

- <span data-ttu-id="0165f-245">**Activer la réplication sur des tables spécifiques et copier les données existantes**.</span><span class="sxs-lookup"><span data-stu-id="0165f-245">**Enable replication on specific tables and copy the existing data**.</span></span> <span data-ttu-id="0165f-246">Pour activer la réplication sur table1, table2 et table3, utilisez les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="0165f-246">Use the following parameters to enable replication on table1, table2, and table3:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -copydata

- <span data-ttu-id="0165f-247">**Activer la réplication sur toutes les tables avec la réplication des métadonnées Phoenix à partir de la source vers la destination**.</span><span class="sxs-lookup"><span data-stu-id="0165f-247">**Enable replication on all tables with replicating phoenix metadata from source to destination**.</span></span> <span data-ttu-id="0165f-248">La réplication des métadonnées Phoenix n’est pas parfaite et doit être utilisée avec précaution.</span><span class="sxs-lookup"><span data-stu-id="0165f-248">Phoenix metadata replication is not perfect and should be enabled with caution.</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -replicate-phoenix-meta

## <a name="copy-and-migrate-data"></a><span data-ttu-id="0165f-249">Copier et migrer des données</span><span class="sxs-lookup"><span data-stu-id="0165f-249">Copy and migrate data</span></span>

<span data-ttu-id="0165f-250">Il existe deux scripts d’action de script distincts pour copier/migrer des données une fois la réplication activée :</span><span class="sxs-lookup"><span data-stu-id="0165f-250">There are two separate script action scripts for copying/migrating data after replication is enabled:</span></span>

- <span data-ttu-id="0165f-251">[Script pour les petites tables](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_copy_table.sh) (taille de quelques gigaoctest et copie globale censée se terminer en moins d’une heure)</span><span class="sxs-lookup"><span data-stu-id="0165f-251">[Script for small tables](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_copy_table.sh) (a few gigabytes in size, and overall copy is expected to finish in less than one hour)</span></span>

- <span data-ttu-id="0165f-252">[Script pour les tables volumineuses](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/nohup_hdi_copy_table.sh) (copie censée prendre plus d’une heure)</span><span class="sxs-lookup"><span data-stu-id="0165f-252">[Script for large tables](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/nohup_hdi_copy_table.sh) (expected to take longer than one hour to copy)</span></span>

<span data-ttu-id="0165f-253">Vous pouvez suivre la même procédure que celle utilisée dans la section [Activer la réplication](#enable-replication) pour appeler l’action de script avec les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="0165f-253">You can follow the same procedure in [Enable replication](#enable-replication) to call the script action with the following parameters:</span></span>

    -m hn1 -t <table1:start_timestamp:end_timestamp;table2:start_timestamp:end_timestamp;...> -p <replication_peer> [-everythingTillNow]

<span data-ttu-id="0165f-254">La section print_usage() du [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_copy_table.sh) fournit une description détaillée des paramètres.</span><span class="sxs-lookup"><span data-stu-id="0165f-254">The print_usage() section of the [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_copy_table.sh) provides a detailed description of parameters.</span></span>

### <a name="scenarios"></a><span data-ttu-id="0165f-255">Scénarios</span><span class="sxs-lookup"><span data-stu-id="0165f-255">Scenarios</span></span>

- <span data-ttu-id="0165f-256">**Copier des tables spécifiques (test1, test2 et test3) pour toutes les lignes modifiées jusqu’à présent (horodatage actuel)** :</span><span class="sxs-lookup"><span data-stu-id="0165f-256">**Copy specific tables (test1, test2, and test3) for all rows edited till now (current time stamp)**:</span></span>

        -m hn1 -t "test1::;test2::;test3::" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow
  <span data-ttu-id="0165f-257">ou</span><span class="sxs-lookup"><span data-stu-id="0165f-257">or</span></span>

        -m hn1 -t "test1::;test2::;test3::" --replication-peer="zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow


- <span data-ttu-id="0165f-258">**Copier des tables spécifiques avec une plage horaire spécifiée** :</span><span class="sxs-lookup"><span data-stu-id="0165f-258">**Copy specific tables with specified time range**:</span></span>

        -m hn1 -t "table1:0:452256397;table2:14141444:452256397" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure"


## <a name="disable-replication"></a><span data-ttu-id="0165f-259">Désactiver la réplication</span><span class="sxs-lookup"><span data-stu-id="0165f-259">Disable replication</span></span>

<span data-ttu-id="0165f-260">Pour désactiver la réplication, vous utilisez un autre script d’action de script disponible dans [GitHub](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh).</span><span class="sxs-lookup"><span data-stu-id="0165f-260">To disable replication, you use another script action script located at [GitHub](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh).</span></span> <span data-ttu-id="0165f-261">Vous pouvez suivre la même procédure que celle utilisée dans la section [Activer la réplication](#enable-replication) pour appeler l’action de script avec les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="0165f-261">You can follow the same procedure in [Enable replication](#enable-replication) to call the script action with the following parameters:</span></span>

    -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari Password> <-all|-t "table1;table2;...">  

<span data-ttu-id="0165f-262">La section print_usage() du [script](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh) fournit une explication détaillée des paramètres.</span><span class="sxs-lookup"><span data-stu-id="0165f-262">The print_usage() section of the [script](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh) provides a detailed explanation of parameters.</span></span>

### <a name="scenarios"></a><span data-ttu-id="0165f-263">Scénarios</span><span class="sxs-lookup"><span data-stu-id="0165f-263">Scenarios</span></span>

- <span data-ttu-id="0165f-264">**Désactiver la réplication sur toutes les tables** :</span><span class="sxs-lookup"><span data-stu-id="0165f-264">**Disable replication on all tables**:</span></span>

        -m hn1 -s <source cluster DNS name> -sp Mypassword\!789 -all
  <span data-ttu-id="0165f-265">ou</span><span class="sxs-lookup"><span data-stu-id="0165f-265">or</span></span>

        --src-cluster=<source cluster DNS name> --dst-cluster=<destination cluster DNS name> --src-ambari-user=<source cluster Ambari username> --src-ambari-password=<source cluster Ambari password>

- <span data-ttu-id="0165f-266">**Désactiver la réplication sur les tables spécifiées (table1, table2 et table3)** :</span><span class="sxs-lookup"><span data-stu-id="0165f-266">**Disable replication on specified tables (table1, table2, and table3)**:</span></span>

        -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari password> -t "table1;table2;table3"

## <a name="next-steps"></a><span data-ttu-id="0165f-267">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0165f-267">Next steps</span></span>

<span data-ttu-id="0165f-268">Dans ce didacticiel, vous avez appris à configurer la réplication de HBase entre deux centres de données.</span><span class="sxs-lookup"><span data-stu-id="0165f-268">In this tutorial, you learned how to configure HBase replication across two datacenters.</span></span> <span data-ttu-id="0165f-269">Pour en savoir plus sur HDInsight et HBase, voir :</span><span class="sxs-lookup"><span data-stu-id="0165f-269">To learn more about HDInsight and HBase, see:</span></span>

* <span data-ttu-id="0165f-270">[Didacticiel HBase : prise en main de HBase avec Hadoop dans HDInsight Linux][hdinsight-hbase-get-started]</span><span class="sxs-lookup"><span data-stu-id="0165f-270">[Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started]</span></span>
* <span data-ttu-id="0165f-271">[Présentation de HBase dans HDInsight : une base de données NoSQL fournissant des fonctionnalités similaires à BigTable pour Hadoop][hdinsight-hbase-overview]</span><span class="sxs-lookup"><span data-stu-id="0165f-271">[HDInsight HBase overview][hdinsight-hbase-overview]</span></span>
* <span data-ttu-id="0165f-272">[Création de clusters HBase dans un réseau virtuel Azure][hdinsight-hbase-provision-vnet]</span><span class="sxs-lookup"><span data-stu-id="0165f-272">[Create HBase clusters in Azure Virtual Network][hdinsight-hbase-provision-vnet]</span></span>
* <span data-ttu-id="0165f-273">[Analyse de sentiments Twitter en temps réel avec HBase dans HDInsight][hdinsight-hbase-twitter-sentiment]</span><span class="sxs-lookup"><span data-stu-id="0165f-273">[Analyze real-time Twitter sentiment with HBase][hdinsight-hbase-twitter-sentiment]</span></span>
* <span data-ttu-id="0165f-274">[Analyse des données de capteur avec Storm et HBase dans HDInsight (Hadoop)][hdinsight-sensor-data]</span><span class="sxs-lookup"><span data-stu-id="0165f-274">[Analyzing sensor data with Storm and HBase in HDInsight (Hadoop)][hdinsight-sensor-data]</span></span>

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
