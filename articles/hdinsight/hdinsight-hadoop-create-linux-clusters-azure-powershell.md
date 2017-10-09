---
title: "aaaCreate Hadoop clusters à l’aide de PowerShell - Azure HDInsight | Documents Microsoft"
description: "Découvrez comment toocreate Hadoop, HBase, tempête ou Spark des clusters à l’aide d’Azure PowerShell sur Linux pour HDInsight."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 4208deca-d64a-45e1-8948-2673d5d7678c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 53afe4702f6b61a0720ceda48a4a34d7fa8797d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-linux-based-clusters-in-hdinsight-using-azure-powershell"></a><span data-ttu-id="72b3e-103">Créer des clusters basés sur Linux dans HDInsight à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="72b3e-103">Create Linux-based clusters in HDInsight using Azure PowerShell</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="72b3e-104">Azure PowerShell est un environnement de script puissant que vous pouvez utiliser toocontrol et automatiser le déploiement de hello et la gestion de vos charges de travail dans Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="72b3e-104">Azure PowerShell is a powerful scripting environment that you can use toocontrol and automate hello deployment and management of your workloads in Microsoft Azure.</span></span> <span data-ttu-id="72b3e-105">Ce document fournit des informations sur comment toocreate un HDInsight basés sur Linux cluster à l’aide de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="72b3e-105">This document provides information about how toocreate a Linux-based HDInsight cluster by using Azure PowerShell.</span></span> <span data-ttu-id="72b3e-106">Il inclut également un exemple de script.</span><span class="sxs-lookup"><span data-stu-id="72b3e-106">It also includes an example script.</span></span>

> [!NOTE]
> <span data-ttu-id="72b3e-107">Azure PowerShell est uniquement disponible sur les clients Windows.</span><span class="sxs-lookup"><span data-stu-id="72b3e-107">Azure PowerShell is only available on Windows clients.</span></span> <span data-ttu-id="72b3e-108">Si vous utilisez un client Mac OS X, Unix ou Linux, consultez [créer un cluster HDInsight de basés sur Linux à l’aide d’Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md) pour plus d’informations sur l’utilisation de hello CLI d’Azure toocreate un cluster.</span><span class="sxs-lookup"><span data-stu-id="72b3e-108">If you are using a Linux, Unix, or Mac OS X client, see [Create a Linux-based HDInsight cluster using Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md) for information about using hello Azure CLI toocreate a cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="72b3e-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="72b3e-109">Prerequisites</span></span>
<span data-ttu-id="72b3e-110">Vous devez disposer de hello avant de commencer cette procédure :</span><span class="sxs-lookup"><span data-stu-id="72b3e-110">You must have hello following before starting this procedure:</span></span>

* <span data-ttu-id="72b3e-111">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="72b3e-111">An Azure subscription.</span></span> <span data-ttu-id="72b3e-112">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="72b3e-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* [<span data-ttu-id="72b3e-113">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="72b3e-113">Azure PowerShell</span></span>](/powershell/azure/install-azurerm-ps)

    > [!IMPORTANT]
    > <span data-ttu-id="72b3e-114">La prise en charge de la gestion des ressources HDInsight par Azure PowerShell à l’aide d’Azure Service Manager est **déconseillée** ; elle a été supprimée le 1er janvier 2017.</span><span class="sxs-lookup"><span data-stu-id="72b3e-114">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="72b3e-115">étapes de Hello dans ce document Utilisez hello nouvelles applets de commande HDInsight qui fonctionnent avec Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="72b3e-115">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="72b3e-116">Suivez les étapes de hello dans [installez Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) tooinstall hello dernière version d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="72b3e-116">Please follow hello steps in [Install Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="72b3e-117">Si vous avez des scripts qui toobe besoin modifié toouse hello nouvelles applets de commande qui fonctionnent avec Azure Resource Manager, consultez [des outils de migration tooAzure développement basé sur le Gestionnaire de ressources pour les clusters HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="72b3e-117">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

## <a name="create-cluster"></a><span data-ttu-id="72b3e-118">Créer un cluster</span><span class="sxs-lookup"><span data-stu-id="72b3e-118">Create cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="72b3e-119">toocreate un cluster HDInsight à l’aide d’Azure PowerShell, vous devez effectuer hello procédures suivantes :</span><span class="sxs-lookup"><span data-stu-id="72b3e-119">toocreate an HDInsight cluster by using Azure PowerShell, you must complete hello following procedures:</span></span>

* <span data-ttu-id="72b3e-120">Création d’un groupe de ressources Azure</span><span class="sxs-lookup"><span data-stu-id="72b3e-120">Create an Azure resource group</span></span>
* <span data-ttu-id="72b3e-121">Création d'un compte Azure Storage</span><span class="sxs-lookup"><span data-stu-id="72b3e-121">Create an Azure Storage account</span></span>
* <span data-ttu-id="72b3e-122">Création d'un conteneur d'objets blob Azure</span><span class="sxs-lookup"><span data-stu-id="72b3e-122">Create an Azure Blob container</span></span>
* <span data-ttu-id="72b3e-123">Création d'un cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="72b3e-123">Create an HDInsight cluster</span></span>

<span data-ttu-id="72b3e-124">Hello de script suivant montre comment toocreate un nouveau cluster :</span><span class="sxs-lookup"><span data-stu-id="72b3e-124">hello following script demonstrates how toocreate a new cluster:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster.ps1?range=5-71)]

<span data-ttu-id="72b3e-125">valeurs Hello que vous spécifiez pour la connexion de cluster hello sont utilisées toocreate hello Hadoop compte d’utilisateur pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="72b3e-125">hello values you specify for hello cluster login are used toocreate hello Hadoop user account for hello cluster.</span></span> <span data-ttu-id="72b3e-126">Utilisez cette tooservices tooconnect de compte hébergé sur le cluster de hello, comme des interfaces utilisateur ou des API REST de web.</span><span class="sxs-lookup"><span data-stu-id="72b3e-126">Use this account tooconnect tooservices hosted on hello cluster such as web UIs or REST APIs.</span></span>

<span data-ttu-id="72b3e-127">valeurs Hello que vous spécifiez pour l’utilisateur SSH hello sont utilisateur SSH hello toocreate utilisé pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="72b3e-127">hello values you specify for hello SSH user are used toocreate hello SSH user for hello cluster.</span></span> <span data-ttu-id="72b3e-128">Utilisez ce compte toostart une session SSH à distance sur le cluster de hello et exécuter des tâches.</span><span class="sxs-lookup"><span data-stu-id="72b3e-128">Use this account toostart a remote SSH session on hello cluster and run jobs.</span></span> <span data-ttu-id="72b3e-129">Pour plus d’informations, consultez hello [utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span><span class="sxs-lookup"><span data-stu-id="72b3e-129">For more information, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="72b3e-130">Si vous envisagez de toouse plus de 32 nœuds de travail (lors de la création du cluster ou en hello mise à l’échelle du cluster après la création), vous devez également spécifier une taille de nœud principal avec au moins 8 cœurs et 14 Go de RAM.</span><span class="sxs-lookup"><span data-stu-id="72b3e-130">If you plan toouse more than 32 worker nodes (either at cluster creation or by scaling hello cluster after creation), you must also specify a head node size with at least 8 cores and 14 GB of RAM.</span></span>
>
> <span data-ttu-id="72b3e-131">Pour plus d’informations sur les tailles de nœud et les coûts associés, consultez [Tarification HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="72b3e-131">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

<span data-ttu-id="72b3e-132">Peut prendre jusqu'à too20 minutes toocreate un cluster.</span><span class="sxs-lookup"><span data-stu-id="72b3e-132">It can take up too20 minutes toocreate a cluster.</span></span>

## <a name="create-cluster-configuration-object"></a><span data-ttu-id="72b3e-133">Création de cluster : objet de configuration</span><span class="sxs-lookup"><span data-stu-id="72b3e-133">Create cluster: Configuration object</span></span>

<span data-ttu-id="72b3e-134">Vous pouvez également créer un objet de configuration HDInsight à l’aide de l’applet de commande `New-AzureRmHDInsightClusterConfig`.</span><span class="sxs-lookup"><span data-stu-id="72b3e-134">You can also create an HDInsight configuration object using `New-AzureRmHDInsightClusterConfig` cmdlet.</span></span> <span data-ttu-id="72b3e-135">Vous pouvez ensuite modifier cette configuration objet tooenable autres options de configuration de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="72b3e-135">You can then modify this configuration object tooenable additional configuration options for your cluster.</span></span> <span data-ttu-id="72b3e-136">Enfin, utilisez hello `-Config` paramètre Hello `New-AzureRmHDInsightCluster` configuration de hello toouse applet de commande.</span><span class="sxs-lookup"><span data-stu-id="72b3e-136">Finally, use hello `-Config` parameter of hello `New-AzureRmHDInsightCluster` cmdlet toouse hello configuration.</span></span>

<span data-ttu-id="72b3e-137">Hello script suivant crée un tooconfigure d’objet de configuration serveur R sur le type de cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="72b3e-137">hello following script creates a configuration object tooconfigure an R Server on HDInsight cluster type.</span></span> <span data-ttu-id="72b3e-138">Hello configuration permet un nœud, RStudio et un compte de stockage supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="72b3e-138">hello configuration enables an edge node, RStudio, and an additional storage account.</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster-with-config.ps1?range=59-98)]

> [!WARNING]
> <span data-ttu-id="72b3e-139">À l’aide d’un compte de stockage dans un emplacement autre que le cluster HDInsight de hello n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="72b3e-139">Using a storage account in a different location than hello HDInsight cluster is not supported.</span></span> <span data-ttu-id="72b3e-140">Lorsque vous utilisez cet exemple, créer un compte de stockage supplémentaire hello Bonjour même emplacement que le serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="72b3e-140">When using this example, create hello additional storage account in hello same location as hello server.</span></span>

## <a name="customize-clusters"></a><span data-ttu-id="72b3e-141">Personnalisation des clusters</span><span class="sxs-lookup"><span data-stu-id="72b3e-141">Customize clusters</span></span>

* <span data-ttu-id="72b3e-142">Consultez [Personnalisation de clusters HDInsight à l’aide de Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="72b3e-142">See [Customize HDInsight clusters using Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell).</span></span>
* <span data-ttu-id="72b3e-143">Consultez [Personnalisation de clusters HDInsight à l’aide d’une action de script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="72b3e-143">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="72b3e-144">Supprimer le cluster de hello</span><span class="sxs-lookup"><span data-stu-id="72b3e-144">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="72b3e-145">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="72b3e-145">Troubleshoot</span></span>

<span data-ttu-id="72b3e-146">Si vous rencontrez des problèmes lors de la création de clusters HDInsight, reportez-vous aux [exigences de contrôle d’accès](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="72b3e-146">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="72b3e-147">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="72b3e-147">Next steps</span></span>

<span data-ttu-id="72b3e-148">Maintenant que vous avez créé un cluster HDInsight, utilisez hello suivant comment les ressources toolearn toowork avec votre cluster.</span><span class="sxs-lookup"><span data-stu-id="72b3e-148">Now that you have successfully created an HDInsight cluster, use hello following resources toolearn how toowork with your cluster.</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="72b3e-149">Clusters Hadoop</span><span class="sxs-lookup"><span data-stu-id="72b3e-149">Hadoop clusters</span></span>

* [<span data-ttu-id="72b3e-150">Utilisation de Hive avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="72b3e-150">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="72b3e-151">Utilisation de Pig avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="72b3e-151">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="72b3e-152">Utilisation de MapReduce avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="72b3e-152">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="72b3e-153">Clusters HBase</span><span class="sxs-lookup"><span data-stu-id="72b3e-153">HBase clusters</span></span>

* [<span data-ttu-id="72b3e-154">Prise en main de HBase sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="72b3e-154">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="72b3e-155">Développement d’applications Java pour HBase sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="72b3e-155">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="72b3e-156">Clusters Storm</span><span class="sxs-lookup"><span data-stu-id="72b3e-156">Storm clusters</span></span>

* [<span data-ttu-id="72b3e-157">Développement de topologies Java pour Storm sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="72b3e-157">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="72b3e-158">Utilisation de composants Python dans Storm sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="72b3e-158">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="72b3e-159">Déploiement et analyse des topologies avec Storm sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="72b3e-159">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)

### <a name="spark-clusters"></a><span data-ttu-id="72b3e-160">Clusters Spark</span><span class="sxs-lookup"><span data-stu-id="72b3e-160">Spark clusters</span></span>

* [<span data-ttu-id="72b3e-161">Créer une application autonome avec Scala</span><span class="sxs-lookup"><span data-stu-id="72b3e-161">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="72b3e-162">Exécution de travaux à distance avec Livy sur un cluster Spark</span><span class="sxs-lookup"><span data-stu-id="72b3e-162">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)
* [<span data-ttu-id="72b3e-163">Spark avec BI : effectuez une analyse interactive des données à l’aide de Spark dans HDInsight avec des outils BI</span><span class="sxs-lookup"><span data-stu-id="72b3e-163">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="72b3e-164">Spark avec Machine Learning : Spark utilisation dans résultats de l’inspection alimentaires toopredict HDInsight</span><span class="sxs-lookup"><span data-stu-id="72b3e-164">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="72b3e-165">Streaming Spark : Utiliser Spark dans HDInsight pour créer des applications de diffusion en continu en temps réel</span><span class="sxs-lookup"><span data-stu-id="72b3e-165">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)

