---
title: "les clusters de Hadoop aaaCreate à l’aide de la ligne de commande - hello Azure HDInsight | Documents Microsoft"
description: "Découvrez comment les clusters HDInsight toocreate à l’aide de hello multiplateforme Azure CLI 1.0."
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
ms.openlocfilehash: 5295b01054b8c23df0e3b75a3e0e8c933ac48b3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hdinsight-clusters-using-hello-azure-cli"></a><span data-ttu-id="a044d-103">Créer des clusters HDInsight à l’aide de hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="a044d-103">Create HDInsight clusters using hello Azure CLI</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="a044d-104">les étapes dans cette procédure pas à pas document Création d’un cluster HDInsight 3.5 à l’aide de hello Azure CLI 1.0 Hello.</span><span class="sxs-lookup"><span data-stu-id="a044d-104">hello steps in this document walk-through creating a HDInsight 3.5 cluster using hello Azure CLI 1.0.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a044d-105">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="a044d-105">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="a044d-106">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="a044d-106">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="a044d-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a044d-107">Prerequisites</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* <span data-ttu-id="a044d-108">**Un abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="a044d-108">**An Azure subscription**.</span></span> <span data-ttu-id="a044d-109">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="a044d-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="a044d-110">**Interface de ligne de commande Azure**.</span><span class="sxs-lookup"><span data-stu-id="a044d-110">**Azure CLI**.</span></span> <span data-ttu-id="a044d-111">étapes Hello dans ce document ont été testés dernière avec version 0.10.14 CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="a044d-111">hello steps in this document were last tested with Azure CLI version 0.10.14.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="a044d-112">étapes de Hello dans ce document ne fonctionnent pas avec Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="a044d-112">hello steps in this document do not work with Azure CLI 2.0.</span></span> <span data-ttu-id="a044d-113">Azure CLI 2.0 ne prend pas en charge la création d’un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a044d-113">Azure CLI 2.0 does not support creating an HDInsight cluster.</span></span>

## <a name="log-in-tooyour-azure-subscription"></a><span data-ttu-id="a044d-114">Ouvrez une session dans tooyour abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="a044d-114">Log in tooyour Azure subscription</span></span>

<span data-ttu-id="a044d-115">Suivez les étapes de hello documentées dans [connecter tooan abonnement Azure à partir de hello Azure Interface de ligne (Azure)](../xplat-cli-connect.md) et connecter abonnement tooyour à l’aide de hello **connexion** (méthode).</span><span class="sxs-lookup"><span data-stu-id="a044d-115">Follow hello steps documented in [Connect tooan Azure subscription from hello Azure Command-Line Interface (Azure CLI)](../xplat-cli-connect.md) and connect tooyour subscription using hello **login** method.</span></span>

## <a name="create-a-cluster"></a><span data-ttu-id="a044d-116">Créer un cluster</span><span class="sxs-lookup"><span data-stu-id="a044d-116">Create a cluster</span></span>

<span data-ttu-id="a044d-117">Hello suit doit être effectuée à partir d’une ligne de commande, tels que PowerShell ou Bash.</span><span class="sxs-lookup"><span data-stu-id="a044d-117">hello following steps should be performed from a command line, such as PowerShell or Bash.</span></span>

1. <span data-ttu-id="a044d-118">Utilisez hello suivant commande tooauthenticate tooyour abonnement Azure :</span><span class="sxs-lookup"><span data-stu-id="a044d-118">Use hello following command tooauthenticate tooyour Azure subscription:</span></span>

        azure login

    <span data-ttu-id="a044d-119">Vous est demandée tooprovide votre nom et le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="a044d-119">You are prompted tooprovide your name and password.</span></span> <span data-ttu-id="a044d-120">Si vous avez plusieurs abonnements Azure, utilisez `azure account set <subscriptionname>` abonnement hello tooset hello CLI d’Azure commandes utilisent.</span><span class="sxs-lookup"><span data-stu-id="a044d-120">If you have multiple Azure subscriptions, use `azure account set <subscriptionname>` tooset hello subscription that hello Azure CLI commands use.</span></span>

2. <span data-ttu-id="a044d-121">Basculez en mode de gestionnaire de ressources tooAzure à l’aide de hello commande suivante :</span><span class="sxs-lookup"><span data-stu-id="a044d-121">Switch tooAzure Resource Manager mode using hello following command:</span></span>

        azure config mode arm

3. <span data-ttu-id="a044d-122">Créez un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="a044d-122">Create a resource group.</span></span> <span data-ttu-id="a044d-123">Ce groupe de ressources contient le cluster HDInsight de hello et compte de stockage associé.</span><span class="sxs-lookup"><span data-stu-id="a044d-123">This resource group contains hello HDInsight cluster and associated storage account.</span></span>

        azure group create groupname location

    * <span data-ttu-id="a044d-124">Remplacez `groupname` avec un nom unique pour le groupe de hello.</span><span class="sxs-lookup"><span data-stu-id="a044d-124">Replace `groupname` with a unique name for hello group.</span></span>

    * <span data-ttu-id="a044d-125">Remplacez `location` par région géographique hello que toocreate hello groupe dans.</span><span class="sxs-lookup"><span data-stu-id="a044d-125">Replace `location` with hello geographic region that you want toocreate hello group in.</span></span>

       <span data-ttu-id="a044d-126">Pour obtenir la liste des emplacements valides, utilisez hello `azure location list` de commandes et utilisez un des emplacements hello de hello `Name` colonne.</span><span class="sxs-lookup"><span data-stu-id="a044d-126">For a list of valid locations, use hello `azure location list` command, and then use one of hello locations from hello `Name` column.</span></span>

4. <span data-ttu-id="a044d-127">Créez un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="a044d-127">Create a storage account.</span></span> <span data-ttu-id="a044d-128">Ce compte de stockage est utilisé comme espace de stockage par défaut hello pour le cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="a044d-128">This storage account is used as hello default storage for hello HDInsight cluster.</span></span>

        azure storage account create -g groupname --sku-name RAGRS -l location --kind Storage storagename

    * <span data-ttu-id="a044d-129">Remplacez `groupname` par nom de hello du groupe de hello créé à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="a044d-129">Replace `groupname` with hello name of hello group created in hello previous step.</span></span>

    * <span data-ttu-id="a044d-130">Remplacez `location` par hello même emplacement utilisé à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="a044d-130">Replace `location` with hello same location used in hello previous step.</span></span>

    * <span data-ttu-id="a044d-131">Remplacez `storagename` avec un nom unique pour le compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="a044d-131">Replace `storagename` with a unique name for hello storage account.</span></span>

        > [!NOTE]
        > <span data-ttu-id="a044d-132">Pour plus d’informations sur les paramètres de hello utilisé dans cette commande, utilisez `azure storage account create -h` aide tooview pour cette commande.</span><span class="sxs-lookup"><span data-stu-id="a044d-132">For more information on hello parameters used in this command, use `azure storage account create -h` tooview help for this command.</span></span>

5. <span data-ttu-id="a044d-133">Récupérer le compte de stockage hello hello clé tooaccess utilisé.</span><span class="sxs-lookup"><span data-stu-id="a044d-133">Retrieve hello key used tooaccess hello storage account.</span></span>

        azure storage account keys list -g groupname storagename

    * <span data-ttu-id="a044d-134">Remplacez `groupname` avec le nom de groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="a044d-134">Replace `groupname` with hello resource group name.</span></span>
    * <span data-ttu-id="a044d-135">Remplacez `storagename` par nom hello hello du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="a044d-135">Replace `storagename` with hello name of hello storage account.</span></span>

     <span data-ttu-id="a044d-136">Dans les données hello qui sont retournées, enregistrer hello `key` valeur `key1`.</span><span class="sxs-lookup"><span data-stu-id="a044d-136">In hello data that is returned, save hello `key` value for `key1`.</span></span>

6. <span data-ttu-id="a044d-137">Créez un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a044d-137">Create an HDInsight cluster.</span></span>

        azure hdinsight cluster create -g groupname -l location -y Linux --clusterType Hadoop --defaultStorageAccountName storagename.blob.core.windows.net --defaultStorageAccountKey storagekey --defaultStorageContainer clustername --workerNodeCount 3 --userName admin --password httppassword --sshUserName sshuser --sshPassword sshuserpassword clustername

    * <span data-ttu-id="a044d-138">Remplacez `groupname` avec le nom de groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="a044d-138">Replace `groupname` with hello resource group name.</span></span>

    * <span data-ttu-id="a044d-139">Remplacez `Hadoop` avec le type de cluster hello que vous souhaitez toocreate.</span><span class="sxs-lookup"><span data-stu-id="a044d-139">Replace `Hadoop` with hello cluster type that you wish toocreate.</span></span> <span data-ttu-id="a044d-140">Par exemple, `Hadoop`, `HBase`, `Kafka`, `Spark` ou `Storm`.</span><span class="sxs-lookup"><span data-stu-id="a044d-140">For example, `Hadoop`, `HBase`, `Kafka`, `Spark`, or `Storm`.</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="a044d-141">HDInsight clusters sont disponibles dans différents types, qui correspondent toohello la charge de travail ou la technologie qui hello cluster est réglée pour.</span><span class="sxs-lookup"><span data-stu-id="a044d-141">HDInsight clusters come in various types, which correspond toohello workload or technology that hello cluster is tuned for.</span></span> <span data-ttu-id="a044d-142">Il n’a aucun toocreate méthode prise en charge un cluster qui combine plusieurs types, tels que Storm et HBase sur un seul cluster.</span><span class="sxs-lookup"><span data-stu-id="a044d-142">There is no supported method toocreate a cluster that combines multiple types, such as Storm and HBase on one cluster.</span></span>

    * <span data-ttu-id="a044d-143">Remplacez `location` par hello même emplacement utilisé dans les étapes précédentes.</span><span class="sxs-lookup"><span data-stu-id="a044d-143">Replace `location` with hello same location used in previous steps.</span></span>

    * <span data-ttu-id="a044d-144">Remplacez `storagename` par le nom de compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="a044d-144">Replace `storagename` with hello storage account name.</span></span>

    * <span data-ttu-id="a044d-145">Remplacez `storagekey` avec clé hello obtenu à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="a044d-145">Replace `storagekey` with hello key obtained in hello previous step.</span></span>

    * <span data-ttu-id="a044d-146">Pourquoi `--defaultStorageContainer` paramètre, hello utilisez même nom que celui que vous utilisez pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="a044d-146">For hello `--defaultStorageContainer` parameter, use hello same name as you are using for hello cluster.</span></span>

    * <span data-ttu-id="a044d-147">Remplacez `admin` et `httppassword` avec le nom de hello et le mot de passe vous souhaitez toouse lors de l’accès de cluster de hello via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a044d-147">Replace `admin` and `httppassword` with hello name and password you wish toouse when accessing hello cluster through HTTPS.</span></span>

    * <span data-ttu-id="a044d-148">Remplacez `sshuser` et `sshuserpassword` avec le nom d’utilisateur hello et le mot de passe vous souhaitez toouse lors de l’accès cluster hello à l’aide de SSH</span><span class="sxs-lookup"><span data-stu-id="a044d-148">Replace `sshuser` and `sshuserpassword` with hello username and password you wish toouse when accessing hello cluster using SSH</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="a044d-149">Cet exemple crée un cluster avec deux nœuds de travail.</span><span class="sxs-lookup"><span data-stu-id="a044d-149">This example creates a cluster with two worker notes.</span></span> <span data-ttu-id="a044d-150">Vous pouvez également modifier le nombre de hello de nœuds worker après la création du cluster en effectuant des opérations de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="a044d-150">You can also change hello number of worker nodes after cluster creation by performing scaling operations.</span></span> <span data-ttu-id="a044d-151">Si vous envisagez d’utiliser plus de 32 nœuds worker, vous devez sélectionner une taille de nœud principal avec au moins 8 cœurs et 14 Go de RAM.</span><span class="sxs-lookup"><span data-stu-id="a044d-151">If you plan on using more than 32 worker nodes, then you must select a head node size with at least 8 cores and 14-GB RAM.</span></span> <span data-ttu-id="a044d-152">Vous pouvez définir la taille du nœud principal hello à l’aide de hello `--headNodeSize` paramètre lors de la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="a044d-152">You can set hello head node size by using hello `--headNodeSize` parameter during cluster creation.</span></span>
    >
    > <span data-ttu-id="a044d-153">Pour plus d’informations sur les tailles de nœud et les coûts associés, consultez [Tarification HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="a044d-153">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

    <span data-ttu-id="a044d-154">Il peut prendre plusieurs minutes pour toofinish de processus de création de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="a044d-154">It may take several minutes for hello cluster creation process toofinish.</span></span> <span data-ttu-id="a044d-155">En règle générale, il dure environ 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="a044d-155">Usually around 15.</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="a044d-156">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="a044d-156">Troubleshoot</span></span>

<span data-ttu-id="a044d-157">Si vous rencontrez des problèmes lors de la création de clusters HDInsight, reportez-vous aux [exigences de contrôle d’accès](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="a044d-157">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a044d-158">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a044d-158">Next steps</span></span>

<span data-ttu-id="a044d-159">Maintenant que vous avez créé un cluster HDInsight à l’aide de hello CLI d’Azure, utilisez hello suivant toolearn comment toowork avec votre cluster :</span><span class="sxs-lookup"><span data-stu-id="a044d-159">Now that you have successfully created an HDInsight cluster using hello Azure CLI, use hello following toolearn how toowork with your cluster:</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="a044d-160">Clusters Hadoop</span><span class="sxs-lookup"><span data-stu-id="a044d-160">Hadoop clusters</span></span>

* [<span data-ttu-id="a044d-161">Utilisation de Hive avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="a044d-161">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="a044d-162">Utilisation de Pig avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="a044d-162">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="a044d-163">Utilisation de MapReduce avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="a044d-163">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="a044d-164">Clusters HBase</span><span class="sxs-lookup"><span data-stu-id="a044d-164">HBase clusters</span></span>

* [<span data-ttu-id="a044d-165">Prise en main de HBase sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="a044d-165">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="a044d-166">Développement d’applications Java pour HBase sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="a044d-166">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="a044d-167">Clusters Storm</span><span class="sxs-lookup"><span data-stu-id="a044d-167">Storm clusters</span></span>

* [<span data-ttu-id="a044d-168">Développement de topologies Java pour Storm sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="a044d-168">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="a044d-169">Utilisation de composants Python dans Storm sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="a044d-169">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="a044d-170">Déploiement et analyse des topologies avec Storm sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="a044d-170">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)
