---
title: "aaaCreate HBase des clusters dans un réseau virtuel - Azure | Documents Microsoft"
description: "Prise en main de HBase dans Azure HDInsight Découvrez comment les clusters toocreate HDInsight HBase sur un réseau virtuel Azure."
keywords: 
services: hdinsight,virtual-network
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 8de8e446-f818-4e61-8fad-e9d38421e80d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/17/2017
ms.author: jgao
ms.openlocfilehash: 097338a5a650bb607a9f6f9ddb59bb88d098b56f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hbase-clusters-on-hdinsight-in-azure-virtual-network"></a><span data-ttu-id="1890d-104">Création de clusters HBase sur HDInsight dans un réseau virtuel Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="1890d-104">Create HBase clusters on HDInsight in Azure Virtual Network</span></span>
<span data-ttu-id="1890d-105">Découvrez comment toocreate HDInsight HBase de Azure de clusters dans un [réseau virtuel Azure][1].</span><span class="sxs-lookup"><span data-stu-id="1890d-105">Learn how toocreate Azure HDInsight HBase clusters in an [Azure Virtual Network][1].</span></span>

<span data-ttu-id="1890d-106">Avec l’intégration de réseau virtuel, clusters HBase peuvent être déployé toohello même virtuel réseau en tant que vos applications, ainsi que les applications peuvent communiquer directement avec HBase.</span><span class="sxs-lookup"><span data-stu-id="1890d-106">With virtual network integration, HBase clusters can be deployed toohello same virtual network as your applications so that applications can communicate with HBase directly.</span></span> <span data-ttu-id="1890d-107">Hello les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="1890d-107">hello benefits include:</span></span>

* <span data-ttu-id="1890d-108">Une connexion directe hello web toohello de nœuds d’application de cluster HBase hello, qui permet la communication via RPC HBase Java appeler les API de (RPC).</span><span class="sxs-lookup"><span data-stu-id="1890d-108">Direct connectivity of hello web application toohello nodes of hello HBase cluster, which enables communication via HBase Java remote procedure call (RPC) APIs.</span></span>
* <span data-ttu-id="1890d-109">Amélioration des performances en évitant à votre trafic de transiter par plusieurs passerelles et équilibrages de charge.</span><span class="sxs-lookup"><span data-stu-id="1890d-109">Improved performance by not having your traffic go over multiple gateways and load-balancers.</span></span>
* <span data-ttu-id="1890d-110">Hello capacité tooprocess des informations sensibles de manière plus sécurisée sans exposer un point de terminaison public.</span><span class="sxs-lookup"><span data-stu-id="1890d-110">hello ability tooprocess sensitive information in a more secure manner without exposing a public endpoint.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="1890d-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1890d-111">Prerequisites</span></span>
<span data-ttu-id="1890d-112">Avant de commencer ce didacticiel, vous devez disposer des éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="1890d-112">Before you begin this tutorial, you must have hello following items:</span></span>

* <span data-ttu-id="1890d-113">**Un abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="1890d-113">**An Azure subscription**.</span></span> <span data-ttu-id="1890d-114">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="1890d-114">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="1890d-115">**Un poste de travail sur lequel est installé Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="1890d-115">**A workstation with Azure PowerShell**.</span></span> <span data-ttu-id="1890d-116">Consultez la page [Installation et utilisation d’Azure PowerShell](https://azure.microsoft.com/documentation/videos/install-and-use-azure-powershell/).</span><span class="sxs-lookup"><span data-stu-id="1890d-116">See [Install and use Azure PowerShell](https://azure.microsoft.com/documentation/videos/install-and-use-azure-powershell/).</span></span>

## <a name="create-hbase-cluster-into-virtual-network"></a><span data-ttu-id="1890d-117">Création de clusters HBase sur un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="1890d-117">Create HBase cluster into virtual network</span></span>
<span data-ttu-id="1890d-118">Dans cette section, vous créez un cluster HBase de basés sur Linux avec un compte de stockage Azure dépendant hello dans un réseau virtuel Azure à l’aide un [modèle Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="1890d-118">In this section, you create a Linux-based HBase cluster with hello dependent Azure Storage account in an Azure virtual network using an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="1890d-119">Pour d’autres méthodes de création de cluster et les paramètres de hello, consultez [HDInsight de créer des clusters](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="1890d-119">For other cluster creation methods and understanding hello settings, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="1890d-120">Pour plus d’informations sur l’utilisation d’un modèle de toocreate Hadoop dans HDInsight les clusters, consultez [Hadoop de créer des clusters dans HDInsight à l’aide de modèles Azure Resource Manager](hdinsight-hadoop-create-windows-clusters-arm-templates.md)</span><span class="sxs-lookup"><span data-stu-id="1890d-120">For more information about using a template toocreate Hadoop clusters in HDInsight, see [Create Hadoop clusters in HDInsight using Azure Resource Manager templates](hdinsight-hadoop-create-windows-clusters-arm-templates.md)</span></span>

> [!NOTE]
> <span data-ttu-id="1890d-121">Certaines propriétés sont codés en dur dans le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="1890d-121">Some properties are hard-coded into hello template.</span></span> <span data-ttu-id="1890d-122">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="1890d-122">For example:</span></span>
>
> * <span data-ttu-id="1890d-123">**Emplacement** : Est des États-Unis 2</span><span class="sxs-lookup"><span data-stu-id="1890d-123">**Location**: East US 2</span></span>
> * <span data-ttu-id="1890d-124">**Version de cluster** : 3.5</span><span class="sxs-lookup"><span data-stu-id="1890d-124">**Cluster version**: 3.5</span></span>
> * <span data-ttu-id="1890d-125">**Nombre de nœuds de travail du cluster** : 2</span><span class="sxs-lookup"><span data-stu-id="1890d-125">**Cluster worker node count**: 2</span></span>
> * <span data-ttu-id="1890d-126">**Compte de stockage par défaut** : une chaîne unique</span><span class="sxs-lookup"><span data-stu-id="1890d-126">**Default storage account**: a unique string</span></span>
> * <span data-ttu-id="1890d-127">**Nom du réseau virtuel** : &lt;Nom du cluster&gt;-réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="1890d-127">**Virtual network name**: &lt;Cluster Name>-vnet</span></span>
> * <span data-ttu-id="1890d-128">**Espace d’adressage du réseau virtuel** : 10.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="1890d-128">**Virtual network address space**: 10.0.0.0/16</span></span>
> * <span data-ttu-id="1890d-129">**Nom du sous-réseau** : subnet1</span><span class="sxs-lookup"><span data-stu-id="1890d-129">**Subnet name**: subnet1</span></span>
> * <span data-ttu-id="1890d-130">**Plage d’adresses de sous-réseau** : 10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="1890d-130">**Subnet address range**: 10.0.0.0/24</span></span>
>
> <span data-ttu-id="1890d-131">&lt;Nom du cluster > est remplacé par le nom de cluster de hello que vous fournissez lors de l’utilisation du modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="1890d-131">&lt;Cluster Name> is replaced with hello cluster name you provide when using hello template.</span></span>
>
>

1. <span data-ttu-id="1890d-132">Cliquez sur hello suit image tooopen hello template Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1890d-132">Click hello following image tooopen hello template in hello Azure portal.</span></span> <span data-ttu-id="1890d-133">Hello modèle se trouve dans [modèles de démarrage rapide Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-linux-vnet/).</span><span class="sxs-lookup"><span data-stu-id="1890d-133">hello template is located in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-linux-vnet/).</span></span>

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-provision-vnet/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. <span data-ttu-id="1890d-134">À partir de hello **les déploiement personnalisé** panneau, entrez hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="1890d-134">From hello **Custom deployment** blade, enter hello following properties:</span></span>

   * <span data-ttu-id="1890d-135">**Abonnement**: sélectionnez un cluster HDInsight d’abonnement Azure utilisé toocreate hello, compte de stockage dépendant de hello et hello réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="1890d-135">**Subscription**: Select an Azure subscription used toocreate hello HDInsight cluster, hello dependent Storage account and hello Azure virtual network.</span></span>
   * <span data-ttu-id="1890d-136">**Groupe de ressources** : sélectionnez **Créer** et donnez un nouveau nom au groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="1890d-136">**Resource group**: Select **Create new**, and specify a new resource group name.</span></span>
   * <span data-ttu-id="1890d-137">**Emplacement**: sélectionnez un emplacement pour le groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="1890d-137">**Location**: Select a location for hello resource group.</span></span>
   * <span data-ttu-id="1890d-138">**ClusterName**: entrez un nom pour hello Hadoop cluster toobe est créé.</span><span class="sxs-lookup"><span data-stu-id="1890d-138">**ClusterName**: Enter a name for hello Hadoop cluster toobe created.</span></span>
   * <span data-ttu-id="1890d-139">**Nom de connexion et mot de passe de cluster**: nom de connexion par défaut hello est **admin**.</span><span class="sxs-lookup"><span data-stu-id="1890d-139">**Cluster login name and password**: hello default login name is **admin**.</span></span>
   * <span data-ttu-id="1890d-140">**Mot de passe et le nom d’utilisateur SSH**: nom d’utilisateur par défaut de hello est **sshuser**.</span><span class="sxs-lookup"><span data-stu-id="1890d-140">**SSH username and password**: hello default username is **sshuser**.</span></span>  <span data-ttu-id="1890d-141">Vous pouvez le renommer.</span><span class="sxs-lookup"><span data-stu-id="1890d-141">You can rename it.</span></span>
   * <span data-ttu-id="1890d-142">**J’accepte les conditions hello susmentionnées générales toohello**: (Sélectionner)</span><span class="sxs-lookup"><span data-stu-id="1890d-142">**I agree toohello terms and hello conditions stated above**: (Select)</span></span>
3. <span data-ttu-id="1890d-143">Cliquez sur **Achat**.</span><span class="sxs-lookup"><span data-stu-id="1890d-143">Click **Purchase**.</span></span> <span data-ttu-id="1890d-144">Cela prend environ environ 20 minutes toocreate un cluster.</span><span class="sxs-lookup"><span data-stu-id="1890d-144">It takes about around 20 minutes toocreate a cluster.</span></span> <span data-ttu-id="1890d-145">Une fois que le cluster de hello est créé, vous pouvez cliquer sur Panneau de cluster hello dans tooopen de portail hello il.</span><span class="sxs-lookup"><span data-stu-id="1890d-145">Once hello cluster is created, you can click hello cluster blade in hello portal tooopen it.</span></span>

<span data-ttu-id="1890d-146">Après avoir terminé le didacticiel de hello, vous pourriez cluster hello de toodelete.</span><span class="sxs-lookup"><span data-stu-id="1890d-146">After you complete hello tutorial, you might want toodelete hello cluster.</span></span> <span data-ttu-id="1890d-147">Avec HDInsight, vos données sont stockées Azure Storage, pour que vous puissiez supprimer un cluster en toute sécurité s’il n’est pas en cours d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="1890d-147">With HDInsight, your data is stored in Azure Storage, so you can safely delete a cluster when it is not in use.</span></span> <span data-ttu-id="1890d-148">Vous devez également payer pour un cluster HDInsight, même lorsque vous ne l’utilisez pas.</span><span class="sxs-lookup"><span data-stu-id="1890d-148">You are also charged for an HDInsight cluster, even when it is not in use.</span></span> <span data-ttu-id="1890d-149">Étant donné que les frais de hello pour le cluster de hello sont autant de fois plus de frais hello pour le stockage, il est judicieux économique toodelete clusters lorsqu’ils ne sont pas en cours d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="1890d-149">Since hello charges for hello cluster are many times more than hello charges for storage, it makes economic sense toodelete clusters when they are not in use.</span></span> <span data-ttu-id="1890d-150">Pour obtenir des instructions de hello de la suppression d’un cluster, consultez [Hadoop de gérer les clusters dans HDInsight à l’aide de hello Azure portal](hdinsight-administer-use-management-portal.md#delete-clusters).</span><span class="sxs-lookup"><span data-stu-id="1890d-150">For hello instructions of deleting a cluster, see [Manage Hadoop clusters in HDInsight by using hello Azure portal](hdinsight-administer-use-management-portal.md#delete-clusters).</span></span>

<span data-ttu-id="1890d-151">toobegin fonctionne avec votre nouveau cluster HBase, vous pouvez utiliser les procédures hello trouvés dans [commencer à utiliser HBase avec Hadoop dans HDInsight](hdinsight-hbase-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="1890d-151">toobegin working with your new HBase cluster, you can use hello procedures found in [Get started using HBase with Hadoop in HDInsight](hdinsight-hbase-tutorial-get-started.md).</span></span>

## <a name="connect-toohello-hbase-cluster-using-hbase-java-rpc-apis"></a><span data-ttu-id="1890d-152">Connecter le cluster de HBase toohello à l’aide des API de RPC HBase Java</span><span class="sxs-lookup"><span data-stu-id="1890d-152">Connect toohello HBase cluster using HBase Java RPC APIs</span></span>
1. <span data-ttu-id="1890d-153">Création d’une infrastructure en tant que service (IaaS) virtual machine dans hello même réseau virtuel Azure et hello même sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="1890d-153">Create an infrastructure as a service (IaaS) virtual machine into hello same Azure virtual network and hello same subnet.</span></span> <span data-ttu-id="1890d-154">Pour plus d’informations sur la création d’une machine virtuelle IaaS, consultez [Création d’une machine virtuelle exécutant Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="1890d-154">For instructions on creating a new IaaS virtual machine, see [Create a Virtual Machine Running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md).</span></span> <span data-ttu-id="1890d-155">Lorsque hello comme suit dans ce document, vous devez utiliser hello valeurs pour la configuration de réseau hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="1890d-155">When following hello steps in this document, you must use hello following values for hello Network configuration:</span></span>

   * <span data-ttu-id="1890d-156">**Réseau virtuel** : &lt;Nom du cluster&gt;-réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="1890d-156">**Virtual network**: &lt;Cluster name>-vnet</span></span>
   * <span data-ttu-id="1890d-157">**Sous-réseau** : subnet1</span><span class="sxs-lookup"><span data-stu-id="1890d-157">**Subnet**: subnet1</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="1890d-158">Remplacez &lt;nom de Cluster > avec le nom de hello que vous avez utilisé lors de la création du cluster HDInsight de hello dans les étapes précédentes.</span><span class="sxs-lookup"><span data-stu-id="1890d-158">Replace &lt;Cluster name> with hello name you used when creating hello HDInsight cluster in previous steps.</span></span>
   >
   >

   <span data-ttu-id="1890d-159">À l’aide de ces valeurs, hello ordinateur virtuel est placé dans hello même réseau virtuel et sous-réseau que le cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="1890d-159">Using these values, hello virtual machine is placed in hello same virtual network and subnet as hello HDInsight cluster.</span></span> <span data-ttu-id="1890d-160">Cette configuration autorise les toodirectly communiquent entre eux.</span><span class="sxs-lookup"><span data-stu-id="1890d-160">This configuration allows them toodirectly communicate with each other.</span></span> <span data-ttu-id="1890d-161">Il existe un moyen toocreate un cluster HDInsight avec un nœud vide.</span><span class="sxs-lookup"><span data-stu-id="1890d-161">There is a way toocreate an HDInsight cluster with an empty edge node.</span></span> <span data-ttu-id="1890d-162">nœud de périmètre Hello peut être cluster de hello toomanage utilisé.</span><span class="sxs-lookup"><span data-stu-id="1890d-162">hello edge node can be used toomanage hello cluster.</span></span>  <span data-ttu-id="1890d-163">Pour plus d’informations, consultez [Utiliser des nœuds de périmètre vides dans HDInsight](hdinsight-apps-use-edge-node.md).</span><span class="sxs-lookup"><span data-stu-id="1890d-163">For more information, see [Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md).</span></span>

2. <span data-ttu-id="1890d-164">Lorsque vous utilisez un tooHBase de tooconnect d’application Java à distance, vous devez utiliser le nom de domaine complet de hello (FQDN).</span><span class="sxs-lookup"><span data-stu-id="1890d-164">When using a Java application tooconnect tooHBase remotely, you must use hello fully qualified domain name (FQDN).</span></span> <span data-ttu-id="1890d-165">toodetermine, vous devez obtenir le suffixe DNS spécifique à la connexion hello du cluster de HBase hello.</span><span class="sxs-lookup"><span data-stu-id="1890d-165">toodetermine this, you must get hello connection-specific DNS suffix of hello HBase cluster.</span></span> <span data-ttu-id="1890d-166">toodo, vous pouvez utiliser une des méthodes suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="1890d-166">toodo that, you can use one of hello following methods:</span></span>

   * <span data-ttu-id="1890d-167">Utilisez un toomake de navigateur Web un appel de Ambari :</span><span class="sxs-lookup"><span data-stu-id="1890d-167">Use a Web browser toomake an Ambari call:</span></span>

     <span data-ttu-id="1890d-168">Parcourir toohttps : / /&lt;nom_cluster >.azurehdinsight.net/api/v1/clusters/&lt;nom_cluster > / héberge ? minimal_response = true.</span><span class="sxs-lookup"><span data-stu-id="1890d-168">Browse toohttps://&lt;ClusterName>.azurehdinsight.net/api/v1/clusters/&lt;ClusterName>/hosts?minimal_response=true.</span></span> <span data-ttu-id="1890d-169">Il trouve un fichier JSON avec des suffixes DNS hello.</span><span class="sxs-lookup"><span data-stu-id="1890d-169">It turns a JSON file with hello DNS suffixes.</span></span>
   * <span data-ttu-id="1890d-170">Utilisez le site Web de Ambari hello :</span><span class="sxs-lookup"><span data-stu-id="1890d-170">Use hello Ambari website:</span></span>

     1. <span data-ttu-id="1890d-171">Parcourir trop https://&lt;nomcluster >. azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="1890d-171">Browse too https://&lt;ClusterName>.azurehdinsight.net.</span></span>
     2. <span data-ttu-id="1890d-172">Cliquez sur **hôtes** à partir du menu du haut hello.</span><span class="sxs-lookup"><span data-stu-id="1890d-172">Click **Hosts** from hello top menu.</span></span>
   * <span data-ttu-id="1890d-173">Utilisez les appels REST Curl toomake :</span><span class="sxs-lookup"><span data-stu-id="1890d-173">Use Curl toomake REST calls:</span></span>

    ```bash
        curl -u <username>:<password> -k https://<clustername>.azurehdinsight.net/ambari/api/v1/clusters/<clustername>.azurehdinsight.net/services/hbase/components/hbrest
    ```

     <span data-ttu-id="1890d-174">Bonjour données JavaScript Objet Notation (JSON) est retourné, trouver l’entrée de « host_name » hello.</span><span class="sxs-lookup"><span data-stu-id="1890d-174">In hello JavaScript Object Notation (JSON) data returned, find hello "host_name" entry.</span></span> <span data-ttu-id="1890d-175">Il contient hello nom de domaine complet pour les nœuds dans le cluster de hello hello.</span><span class="sxs-lookup"><span data-stu-id="1890d-175">It contains hello FQDN for hello nodes in hello cluster.</span></span> <span data-ttu-id="1890d-176">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="1890d-176">For example:</span></span>

         ...
         "host_name": "wordkernode0.<clustername>.b1.cloudapp.net
         ...

     <span data-ttu-id="1890d-177">partie Hello de début de nom de domaine hello avec le nom du cluster hello est le suffixe DNS de hello.</span><span class="sxs-lookup"><span data-stu-id="1890d-177">hello portion of hello domain name beginning with hello cluster name is hello DNS suffix.</span></span> <span data-ttu-id="1890d-178">Par exemple, mon_cluster.b1.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="1890d-178">For example, mycluster.b1.cloudapp.net.</span></span>
   * <span data-ttu-id="1890d-179">Utilisation d'Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1890d-179">Use Azure PowerShell</span></span>

     <span data-ttu-id="1890d-180">Hello utilisation suivant hello de Azure PowerShell script tooregister **Get-ClusterDetail** (fonction), qui peut être suffixe DNS de hello tooreturn utilisé :</span><span class="sxs-lookup"><span data-stu-id="1890d-180">Use hello following Azure PowerShell script tooregister hello **Get-ClusterDetail** function, which can be used tooreturn hello DNS suffix:</span></span>

    ```powershell
        function Get-ClusterDetail(
            [String]
            [Parameter( Position=0, Mandatory=$true )]
            $ClusterDnsName,
            [String]
            [Parameter( Position=1, Mandatory=$true )]
            $Username,
            [String]
            [Parameter( Position=2, Mandatory=$true )]
            $Password,
            [String]
            [Parameter( Position=3, Mandatory=$true )]
            $PropertyName
            )
        {
        <#
            .SYNOPSIS
            Displays information toofacilitate an HDInsight cluster-to-cluster scenario within hello same virtual network.
            .Description
            This command shows hello following 4 properties of an HDInsight cluster:
            1. ZookeeperQuorum (supports only HBase type cluster)
                Shows hello value of HBase property "hbase.zookeeper.quorum".
            2. ZookeeperClientPort (supports only HBase type cluster)
                Shows hello value of HBase property "hbase.zookeeper.property.clientPort".
            3. HBaseRestServers (supports only HBase type cluster)
                Shows a list of host FQDNs that run hello HBase REST server.
            4. FQDNSuffix (supports all cluster types)
                Shows hello FQDN suffix of hosts in hello cluster.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperQuorum
            This command shows hello value of HBase property "hbase.zookeeper.quorum".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperClientPort
            This command shows hello value of HBase property "hbase.zookeeper.property.clientPort".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName HBaseRestServers
            This command shows a list of host FQDNs that run hello HBase REST server.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName FQDNSuffix
            This command shows hello FQDN suffix of hosts in hello cluster.
        #>

            $DnsSuffix = ".azurehdinsight.net"

            $ClusterFQDN = $ClusterDnsName + $DnsSuffix
            $webclient = new-object System.Net.WebClient
            $webclient.Credentials = new-object System.Net.NetworkCredential($Username, $Password)

            if($PropertyName -eq "ZookeeperQuorum")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.zookeeper.quorum"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                Write-host $JsonObject.items[0].properties.'hbase.zookeeper.quorum'
            }
            if($PropertyName -eq "ZookeeperClientPort")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.zookeeper.property.clientPort"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                Write-host $JsonObject.items[0].properties.'hbase.zookeeper.property.clientPort'
            }
            if($PropertyName -eq "HBaseRestServers")
            {
                $Url1 = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.rest.port"
                $Response1 = $webclient.DownloadString($Url1)
                $JsonObject1 = $Response1 | ConvertFrom-Json
                $PortNumber = $JsonObject1.items[0].properties.'hbase.rest.port'

                $Url2 = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/services/hbase/components/hbrest"
                $Response2 = $webclient.DownloadString($Url2)
                $JsonObject2 = $Response2 | ConvertFrom-Json
                foreach ($host_component in $JsonObject2.host_components)
                {
                    $ConnectionString = $host_component.HostRoles.host_name + ":" + $PortNumber
                    Write-host $ConnectionString
                }
            }
            if($PropertyName -eq "FQDNSuffix")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/services/YARN/components/RESOURCEMANAGER"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                $FQDN = $JsonObject.host_components[0].HostRoles.host_name
                $pos = $FQDN.IndexOf(".")
                $Suffix = $FQDN.Substring($pos + 1)
                Write-host $Suffix
            }
        }
    ```

     <span data-ttu-id="1890d-181">Après l’exécution du script PowerShell de Azure hello, utilisez hello commande suivante suffixe DNS de hello tooreturn à l’aide de hello **Get-ClusterDetail** (fonction).</span><span class="sxs-lookup"><span data-stu-id="1890d-181">After running hello Azure PowerShell script, use hello following command tooreturn hello DNS suffix by using hello **Get-ClusterDetail** function.</span></span> <span data-ttu-id="1890d-182">Spécifiez votre nom de cluster HDInsight HBase, ainsi que le nom et le mot de passe de l'administrateur lors de l'utilisation de cette commande.</span><span class="sxs-lookup"><span data-stu-id="1890d-182">Specify your HDInsight HBase cluster name, admin name, and admin password when using this command.</span></span>

    ```powershell
        Get-ClusterDetail -ClusterDnsName <yourclustername> -PropertyName FQDNSuffix -Username <clusteradmin> -Password <clusteradminpassword>
    ```

     <span data-ttu-id="1890d-183">Cette commande retourne le suffixe DNS de hello.</span><span class="sxs-lookup"><span data-stu-id="1890d-183">This command returns hello DNS suffix.</span></span> <span data-ttu-id="1890d-184">Par exemple, **votre_nom_cluster.b4.internal.cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="1890d-184">For example, **yourclustername.b4.internal.cloudapp.net**.</span></span>


<!--
3.    Change hello primary DNS suffix configuration of hello virtual machine. This enables hello virtual machine tooautomatically resolve hello host name of hello HBase cluster without explicit specification of hello suffix. For example, hello *workernode0* host name will be correctly resolved tooworkernode0 of hello HBase cluster.

    toomake hello configuration change:

    1. RDP into hello virtual machine.
    2. Open **Local Group Policy Editor**. hello executable is gpedit.msc.
    3. Expand **Computer Configuration**, expand **Administrative Templates**, expand **Network**, and then click **DNS Client**.
    - Set **Primary DNS Suffix** toohello value obtained in step 2:

        ![hdinsight.hbase.primary.dns.suffix][img-primary-dns-suffix]
    4. Click **OK**.
    5. Reboot hello virtual machine.
-->

<span data-ttu-id="1890d-185">tooverify qui hello d’ordinateur virtuel peuvent communiquer avec hello cluster HBase, utilisez la commande de hello `ping headnode0.<dns suffix>` à partir de l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="1890d-185">tooverify that hello virtual machine can communicate with hello HBase cluster, use hello command `ping headnode0.<dns suffix>` from hello virtual machine.</span></span> <span data-ttu-id="1890d-186">Par exemple, ping headnode0.mon_cluster.b1.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="1890d-186">For example, ping headnode0.mycluster.b1.cloudapp.net.</span></span>

<span data-ttu-id="1890d-187">toouse ces informations dans une application Java, vous pouvez suivre les étapes de hello dans [Maven d’utiliser toobuild Java applications qui utilisent HBase hdinsight (Hadoop)](hdinsight-hbase-build-java-maven.md) toocreate une application.</span><span class="sxs-lookup"><span data-stu-id="1890d-187">toouse this information in a Java application, you can follow hello steps in [Use Maven toobuild Java applications that use HBase with HDInsight (Hadoop)](hdinsight-hbase-build-java-maven.md) toocreate an application.</span></span> <span data-ttu-id="1890d-188">application de hello toohave se connecter à distance HBase tooa, modifier hello **hbase-site.XML** fichier cette hello de toouse exemple nom de domaine complet pour soigneur.</span><span class="sxs-lookup"><span data-stu-id="1890d-188">toohave hello application connect tooa remote HBase server, modify hello **hbase-site.xml** file in this example toouse hello FQDN for Zookeeper.</span></span> <span data-ttu-id="1890d-189">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="1890d-189">For example:</span></span>

    <property>
        <name>hbase.zookeeper.quorum</name>
        <value>zookeeper0.<dns suffix>,zookeeper1.<dns suffix>,zookeeper2.<dns suffix></value>
    </property>

> [!NOTE]
> <span data-ttu-id="1890d-190">Pour plus d’informations sur la résolution de noms dans les réseaux virtuels Azure, y compris la manière toouse votre propre serveur DNS, consultez [résolution de noms (DNS)](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="1890d-190">For more information about name resolution in Azure virtual networks, including how toouse your own DNS server, see [Name Resolution (DNS)](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="1890d-191">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1890d-191">Next steps</span></span>
<span data-ttu-id="1890d-192">Dans ce didacticiel, vous avez appris comment toocreate un cluster HBase.</span><span class="sxs-lookup"><span data-stu-id="1890d-192">In this tutorial, you learned how toocreate an HBase cluster.</span></span> <span data-ttu-id="1890d-193">toolearn, voir :</span><span class="sxs-lookup"><span data-stu-id="1890d-193">toolearn more, see:</span></span>

* [<span data-ttu-id="1890d-194">Prise en main de HDInsight</span><span class="sxs-lookup"><span data-stu-id="1890d-194">Get started with HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="1890d-195">Utiliser des nœuds de périphérie vides dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="1890d-195">Use empty edge nodes in HDInsight</span></span>](hdinsight-apps-use-edge-node.md)
* [<span data-ttu-id="1890d-196">Configuration de la géo-réplication HBase dans HDInsigtht</span><span class="sxs-lookup"><span data-stu-id="1890d-196">Configure HBase replication in HDInsight</span></span>](hdinsight-hbase-replication.md)
* [<span data-ttu-id="1890d-197">Créer des clusters Hadoop dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="1890d-197">Create Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="1890d-198">Prise en main de HBase avec Hadoop dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="1890d-198">Get started using HBase with Hadoop in HDInsight</span></span>](hdinsight-hbase-tutorial-get-started.md)
* [<span data-ttu-id="1890d-199">Analyse de sentiments Twitter avec HBase dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="1890d-199">Analyze Twitter sentiment with HBase in HDInsight</span></span>](hdinsight-hbase-analyze-twitter-sentiment.md)
* <span data-ttu-id="1890d-200">[Présentation du réseau virtuel][vnet-overview]</span><span class="sxs-lookup"><span data-stu-id="1890d-200">[Virtual Network Overview][vnet-overview]</span></span>

[1]: http://azure.microsoft.com/services/virtual-network/
[2]: http://technet.microsoft.com/library/ee176961.aspx
[3]: http://technet.microsoft.com/library/hh847889.aspx

[hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[vnet-overview]: ../virtual-network/virtual-networks-overview.md
[vm-create]: ../virtual-machines/virtual-machines-windows-hero-tutorial.md

[azure-portal]: https://portal.azure.com
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp

[hdinsight-powershell-reference]: https://msdn.microsoft.com/library/dn858087.aspx


[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter


[powershell-install]: /powershell/azureps-cmdlets-docs


[hdinsight-customize-cluster]: hdinsight-hadoop-customize-cluster.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage-powershell]: ../hdinsight-hadoop-use-blob-storage.md#powershell
[hdinsight-analyze-flight-delay-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-hive-odbc]: hdinsight-connect-excel-hive-ODBC-driver.md
[hdinsight-hbase-replication-dns]: hdinsight-hbase-geo-replication-configure-DNS.md

[img-dns-surffix]: ./media/hdinsight-hbase-provision-vnet/DNSSuffix.png
[img-primary-dns-suffix]: ./media/hdinsight-hbase-provision-vnet/PrimaryDNSSuffix.png
[img-provision-cluster-page1]: ./media/hdinsight-hbase-provision-vnet/hbasewizard1.png "Détails de configuration pour le nouveau cluster de HBase hello"
[img-provision-cluster-page5]: ./media/hdinsight-hbase-provision-vnet/hbasewizard5.png "Utilisez l’Action de Script toocustomize un cluster HBase"

[azure-preview-portal]: https://portal.azure.com
