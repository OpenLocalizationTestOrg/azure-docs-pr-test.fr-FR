---
title: "Créer des clusters Hadoop à l’aide de la ligne de commande - Azure HDInsight | Documents Microsoft"
description: "Apprenez à créer des clusters HDInsight à l’aide de l’interface multiplateforme Azure CLI 1.0."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 50b01483-455c-4d87-b754-2229005a8ab9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 8f2fcb46789d000cd66164508f1159338dcae5f9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-hdinsight-clusters-using-the-azure-cli"></a><span data-ttu-id="f0efe-103">Créer des clusters HDInsight à l’aide de l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="f0efe-103">Create HDInsight clusters using the Azure CLI</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="f0efe-104">Les étapes de cette procédure présentent la création d’un cluster HDInsight 3.5 à l’aide d’Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="f0efe-104">The steps in this document walk-through creating a HDInsight 3.5 cluster using the Azure CLI 1.0.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f0efe-105">Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="f0efe-105">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="f0efe-106">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="f0efe-106">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="f0efe-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f0efe-107">Prerequisites</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* <span data-ttu-id="f0efe-108">**Un abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="f0efe-108">**An Azure subscription**.</span></span> <span data-ttu-id="f0efe-109">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="f0efe-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="f0efe-110">**Interface de ligne de commande Azure**.</span><span class="sxs-lookup"><span data-stu-id="f0efe-110">**Azure CLI**.</span></span> <span data-ttu-id="f0efe-111">Les étapes décrites dans ce document ont été testées pour Azure CLI version 0.10.14.</span><span class="sxs-lookup"><span data-stu-id="f0efe-111">The steps in this document were last tested with Azure CLI version 0.10.14.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="f0efe-112">Les étapes décrites dans ce document ne fonctionnent pas avec Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="f0efe-112">The steps in this document do not work with Azure CLI 2.0.</span></span> <span data-ttu-id="f0efe-113">Azure CLI 2.0 ne prend pas en charge la création d’un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f0efe-113">Azure CLI 2.0 does not support creating an HDInsight cluster.</span></span>

## <a name="log-in-to-your-azure-subscription"></a><span data-ttu-id="f0efe-114">Connexion à votre abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="f0efe-114">Log in to your Azure subscription</span></span>

<span data-ttu-id="f0efe-115">Suivez les étapes décrites dans [Se connecter à un abonnement Azure à partir de l’interface de ligne de commande Azure (Azure CLI)](../xplat-cli-connect.md) et connectez-vous à votre abonnement à l’aide de la méthode **login** .</span><span class="sxs-lookup"><span data-stu-id="f0efe-115">Follow the steps documented in [Connect to an Azure subscription from the Azure Command-Line Interface (Azure CLI)](../xplat-cli-connect.md) and connect to your subscription using the **login** method.</span></span>

## <a name="create-a-cluster"></a><span data-ttu-id="f0efe-116">Créer un cluster</span><span class="sxs-lookup"><span data-stu-id="f0efe-116">Create a cluster</span></span>

<span data-ttu-id="f0efe-117">Les étapes suivantes doivent être exécutées à partir d’une ligne de commande, telle que PowerShell ou Bash.</span><span class="sxs-lookup"><span data-stu-id="f0efe-117">The following steps should be performed from a command line, such as PowerShell or Bash.</span></span>

1. <span data-ttu-id="f0efe-118">Utilisez la commande suivante pour vous identifier auprès de votre abonnement Azure :</span><span class="sxs-lookup"><span data-stu-id="f0efe-118">Use the following command to authenticate to your Azure subscription:</span></span>

        azure login

    <span data-ttu-id="f0efe-119">Vous êtes invité à fournir votre nom et mot de passe.</span><span class="sxs-lookup"><span data-stu-id="f0efe-119">You are prompted to provide your name and password.</span></span> <span data-ttu-id="f0efe-120">Si vous possédez plusieurs abonnements Azure, utilisez `azure account set <subscriptionname>` pour définir l’abonnement que les commandes CLI Azure doivent utiliser.</span><span class="sxs-lookup"><span data-stu-id="f0efe-120">If you have multiple Azure subscriptions, use `azure account set <subscriptionname>` to set the subscription that the Azure CLI commands use.</span></span>

2. <span data-ttu-id="f0efe-121">Passez en mode Gestionnaire de ressources Azure en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f0efe-121">Switch to Azure Resource Manager mode using the following command:</span></span>

        azure config mode arm

3. <span data-ttu-id="f0efe-122">Créez un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="f0efe-122">Create a resource group.</span></span> <span data-ttu-id="f0efe-123">Ce groupe de ressources contient le cluster HDInsight et le compte de stockage associé.</span><span class="sxs-lookup"><span data-stu-id="f0efe-123">This resource group contains the HDInsight cluster and associated storage account.</span></span>

        azure group create groupname location

    * <span data-ttu-id="f0efe-124">Remplacez `groupname` par un nom unique pour le groupe.</span><span class="sxs-lookup"><span data-stu-id="f0efe-124">Replace `groupname` with a unique name for the group.</span></span>

    * <span data-ttu-id="f0efe-125">Remplacez `location` par la région géographique dans laquelle vous souhaitez créer le groupe.</span><span class="sxs-lookup"><span data-stu-id="f0efe-125">Replace `location` with the geographic region that you want to create the group in.</span></span>

       <span data-ttu-id="f0efe-126">Pour obtenir la liste des emplacements valides, utilisez la commande `azure location list` , puis un des emplacements de la colonne `Name`.</span><span class="sxs-lookup"><span data-stu-id="f0efe-126">For a list of valid locations, use the `azure location list` command, and then use one of the locations from the `Name` column.</span></span>

4. <span data-ttu-id="f0efe-127">Créez un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="f0efe-127">Create a storage account.</span></span> <span data-ttu-id="f0efe-128">Ce compte de stockage est utilisé comme espace de stockage par défaut pour le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f0efe-128">This storage account is used as the default storage for the HDInsight cluster.</span></span>

        azure storage account create -g groupname --sku-name RAGRS -l location --kind Storage storagename

    * <span data-ttu-id="f0efe-129">Remplacez `groupname` par le nom du groupe créé à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="f0efe-129">Replace `groupname` with the name of the group created in the previous step.</span></span>

    * <span data-ttu-id="f0efe-130">Remplacez `location` par le même emplacement que celui utilisé à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="f0efe-130">Replace `location` with the same location used in the previous step.</span></span>

    * <span data-ttu-id="f0efe-131">Remplacez `storagename` par un nom de compte de stockage unique.</span><span class="sxs-lookup"><span data-stu-id="f0efe-131">Replace `storagename` with a unique name for the storage account.</span></span>

        > [!NOTE]
        > <span data-ttu-id="f0efe-132">Pour plus d’informations sur les paramètres utilisés dans cette commande, utilisez `azure storage account create -h` pour afficher l’aide relative à cette commande.</span><span class="sxs-lookup"><span data-stu-id="f0efe-132">For more information on the parameters used in this command, use `azure storage account create -h` to view help for this command.</span></span>

5. <span data-ttu-id="f0efe-133">Récupérez la clé utilisée pour accéder au compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="f0efe-133">Retrieve the key used to access the storage account.</span></span>

        azure storage account keys list -g groupname storagename

    * <span data-ttu-id="f0efe-134">Remplacez `groupname` par le nom du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="f0efe-134">Replace `groupname` with the resource group name.</span></span>
    * <span data-ttu-id="f0efe-135">Remplacez `storagename` par le nom du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="f0efe-135">Replace `storagename` with the name of the storage account.</span></span>

     <span data-ttu-id="f0efe-136">Dans les données renvoyées, enregistrez la valeur `key` par `key1`.</span><span class="sxs-lookup"><span data-stu-id="f0efe-136">In the data that is returned, save the `key` value for `key1`.</span></span>

6. <span data-ttu-id="f0efe-137">Créez un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f0efe-137">Create an HDInsight cluster.</span></span>

        azure hdinsight cluster create -g groupname -l location -y Linux --clusterType Hadoop --defaultStorageAccountName storagename.blob.core.windows.net --defaultStorageAccountKey storagekey --defaultStorageContainer clustername --workerNodeCount 3 --userName admin --password httppassword --sshUserName sshuser --sshPassword sshuserpassword clustername

    * <span data-ttu-id="f0efe-138">Remplacez `groupname` par le nom du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="f0efe-138">Replace `groupname` with the resource group name.</span></span>

    * <span data-ttu-id="f0efe-139">Remplacez `Hadoop` par le type de cluster que vous souhaitez créer.</span><span class="sxs-lookup"><span data-stu-id="f0efe-139">Replace `Hadoop` with the cluster type that you wish to create.</span></span> <span data-ttu-id="f0efe-140">Par exemple, `Hadoop`, `HBase`, `Kafka`, `Spark` ou `Storm`.</span><span class="sxs-lookup"><span data-stu-id="f0efe-140">For example, `Hadoop`, `HBase`, `Kafka`, `Spark`, or `Storm`.</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="f0efe-141">Il existe différents types de clusters HDInsight correspondant à la charge de travail ou à la technologie pour laquelle ils sont utilisés.</span><span class="sxs-lookup"><span data-stu-id="f0efe-141">HDInsight clusters come in various types, which correspond to the workload or technology that the cluster is tuned for.</span></span> <span data-ttu-id="f0efe-142">Il n’existe aucune méthode prise en charge pour créer un cluster combinant plusieurs types, tels que Storm et HBase sur un seul cluster.</span><span class="sxs-lookup"><span data-stu-id="f0efe-142">There is no supported method to create a cluster that combines multiple types, such as Storm and HBase on one cluster.</span></span>

    * <span data-ttu-id="f0efe-143">Remplacez `location` par le même emplacement que celui utilisé aux étapes précédentes.</span><span class="sxs-lookup"><span data-stu-id="f0efe-143">Replace `location` with the same location used in previous steps.</span></span>

    * <span data-ttu-id="f0efe-144">Remplacez `storagename` par le nom du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="f0efe-144">Replace `storagename` with the storage account name.</span></span>

    * <span data-ttu-id="f0efe-145">Remplacez `storagekey` par la clé obtenue à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="f0efe-145">Replace `storagekey` with the key obtained in the previous step.</span></span>

    * <span data-ttu-id="f0efe-146">Pour le paramètre `--defaultStorageContainer` , utilisez le même nom que celui utilisé pour le cluster.</span><span class="sxs-lookup"><span data-stu-id="f0efe-146">For the `--defaultStorageContainer` parameter, use the same name as you are using for the cluster.</span></span>

    * <span data-ttu-id="f0efe-147">Remplacez `admin` et `httppassword` par le nom et le mot de passe à utiliser lors de l’accès au cluster via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="f0efe-147">Replace `admin` and `httppassword` with the name and password you wish to use when accessing the cluster through HTTPS.</span></span>

    * <span data-ttu-id="f0efe-148">Remplacez `sshuser` et `sshuserpassword` par le nom et le mot de passe à utiliser lors de l’accès au cluster via SSH</span><span class="sxs-lookup"><span data-stu-id="f0efe-148">Replace `sshuser` and `sshuserpassword` with the username and password you wish to use when accessing the cluster using SSH</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="f0efe-149">Cet exemple crée un cluster avec deux nœuds de travail.</span><span class="sxs-lookup"><span data-stu-id="f0efe-149">This example creates a cluster with two worker notes.</span></span> <span data-ttu-id="f0efe-150">Vous pouvez également modifier le nombre de nœuds worker après la création du cluster en effectuant des opérations de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="f0efe-150">You can also change the number of worker nodes after cluster creation by performing scaling operations.</span></span> <span data-ttu-id="f0efe-151">Si vous envisagez d’utiliser plus de 32 nœuds worker, vous devez sélectionner une taille de nœud principal avec au moins 8 cœurs et 14 Go de RAM.</span><span class="sxs-lookup"><span data-stu-id="f0efe-151">If you plan on using more than 32 worker nodes, then you must select a head node size with at least 8 cores and 14-GB RAM.</span></span> <span data-ttu-id="f0efe-152">Vous pouvez définir la taille du nœud principal à l’aide du paramètre `--headNodeSize` pendant la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="f0efe-152">You can set the head node size by using the `--headNodeSize` parameter during cluster creation.</span></span>
    >
    > <span data-ttu-id="f0efe-153">Pour plus d’informations sur les tailles de nœud et les coûts associés, consultez [Tarification HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="f0efe-153">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

    <span data-ttu-id="f0efe-154">Le processus de création de cluster peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="f0efe-154">It may take several minutes for the cluster creation process to finish.</span></span> <span data-ttu-id="f0efe-155">En règle générale, il dure environ 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="f0efe-155">Usually around 15.</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="f0efe-156">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="f0efe-156">Troubleshoot</span></span>

<span data-ttu-id="f0efe-157">Si vous rencontrez des problèmes lors de la création de clusters HDInsight, reportez-vous aux [exigences de contrôle d’accès](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="f0efe-157">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0efe-158">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f0efe-158">Next steps</span></span>

<span data-ttu-id="f0efe-159">Vous avez créé un cluster HDInsight à l’aide de l’interface de ligne de commande Azure. Pour apprendre à l’utiliser, consultez les rubriques ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="f0efe-159">Now that you have successfully created an HDInsight cluster using the Azure CLI, use the following to learn how to work with your cluster:</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="f0efe-160">Clusters Hadoop</span><span class="sxs-lookup"><span data-stu-id="f0efe-160">Hadoop clusters</span></span>

* [<span data-ttu-id="f0efe-161">Utilisation de Hive avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="f0efe-161">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="f0efe-162">Utilisation de Pig avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="f0efe-162">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="f0efe-163">Utilisation de MapReduce avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="f0efe-163">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="f0efe-164">Clusters HBase</span><span class="sxs-lookup"><span data-stu-id="f0efe-164">HBase clusters</span></span>

* [<span data-ttu-id="f0efe-165">Prise en main de HBase sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="f0efe-165">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="f0efe-166">Développement d’applications Java pour HBase sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="f0efe-166">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="f0efe-167">Clusters Storm</span><span class="sxs-lookup"><span data-stu-id="f0efe-167">Storm clusters</span></span>

* [<span data-ttu-id="f0efe-168">Développement de topologies Java pour Storm sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="f0efe-168">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="f0efe-169">Utilisation de composants Python dans Storm sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="f0efe-169">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="f0efe-170">Déploiement et analyse des topologies avec Storm sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="f0efe-170">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)
