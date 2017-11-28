---
title: "Créer des clusters Hadoop à l’aide de PowerShell - Azure HDInsight | Microsoft Docs"
description: "Découvrez comment créer des clusters Hadoop, HBase, Storm ou Spark sur Linux pour HDInsight à l’aide d’Azure PowerShell."
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
ms.openlocfilehash: ca75974e6ec4f60739137d4cb5458bbfd735de3e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-linux-based-clusters-in-hdinsight-using-azure-powershell"></a><span data-ttu-id="fe44c-103">Créer des clusters basés sur Linux dans HDInsight à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="fe44c-103">Create Linux-based clusters in HDInsight using Azure PowerShell</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="fe44c-104">Azure PowerShell est un environnement puissant de création de scripts vous permettant de contrôler et d’automatiser le déploiement et la gestion de vos charges de travail dans Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="fe44c-104">Azure PowerShell is a powerful scripting environment that you can use to control and automate the deployment and management of your workloads in Microsoft Azure.</span></span> <span data-ttu-id="fe44c-105">Ce document fournit des informations sur la création d’un cluster HDInsight basé sur Linux à l’aide d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fe44c-105">This document provides information about how to create a Linux-based HDInsight cluster by using Azure PowerShell.</span></span> <span data-ttu-id="fe44c-106">Il inclut également un exemple de script.</span><span class="sxs-lookup"><span data-stu-id="fe44c-106">It also includes an example script.</span></span>

> [!NOTE]
> <span data-ttu-id="fe44c-107">Azure PowerShell est uniquement disponible sur les clients Windows.</span><span class="sxs-lookup"><span data-stu-id="fe44c-107">Azure PowerShell is only available on Windows clients.</span></span> <span data-ttu-id="fe44c-108">Si vous utilisez un client Linux, Unix ou Mac OS X, consultez [Création de clusters basés sur Linux dans HDInsight à l’aide de l’interface CLI Azure](hdinsight-hadoop-create-linux-clusters-azure-cli.md) pour plus d’informations sur l’utilisation de l’interface CLI Azure pour créer un cluster.</span><span class="sxs-lookup"><span data-stu-id="fe44c-108">If you are using a Linux, Unix, or Mac OS X client, see [Create a Linux-based HDInsight cluster using Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md) for information about using the Azure CLI to create a cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fe44c-109">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="fe44c-109">Prerequisites</span></span>
<span data-ttu-id="fe44c-110">Avant de commencer cette procédure, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="fe44c-110">You must have the following before starting this procedure:</span></span>

* <span data-ttu-id="fe44c-111">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="fe44c-111">An Azure subscription.</span></span> <span data-ttu-id="fe44c-112">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="fe44c-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* [<span data-ttu-id="fe44c-113">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="fe44c-113">Azure PowerShell</span></span>](/powershell/azure/install-azurerm-ps)

    > [!IMPORTANT]
    > <span data-ttu-id="fe44c-114">La prise en charge de la gestion des ressources HDInsight par Azure PowerShell à l’aide d’Azure Service Manager est **déconseillée** ; elle a été supprimée le 1er janvier 2017.</span><span class="sxs-lookup"><span data-stu-id="fe44c-114">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="fe44c-115">Dans ce document, la procédure repose sur les nouvelles applets de commande HDInsight qui fonctionnent avec Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fe44c-115">The steps in this document use the new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="fe44c-116">Suivez les étapes indiquées dans [Installer Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) pour installer la dernière version d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fe44c-116">Please follow the steps in [Install Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) to install the latest version of Azure PowerShell.</span></span> <span data-ttu-id="fe44c-117">Si vous devez modifier certains scripts pour utiliser les nouvelles applets de commande fonctionnant avec Azure Resource Manager, consultez [Migration vers les outils de développement Azure Resource Manager pour les clusters HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="fe44c-117">If you have scripts that need to be modified to use the new cmdlets that work with Azure Resource Manager, see [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

## <a name="create-cluster"></a><span data-ttu-id="fe44c-118">Créer un cluster</span><span class="sxs-lookup"><span data-stu-id="fe44c-118">Create cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="fe44c-119">Les procédures suivantes sont nécessaires pour créer un cluster HDInsight en utilisant Azure PowerShell :</span><span class="sxs-lookup"><span data-stu-id="fe44c-119">To create an HDInsight cluster by using Azure PowerShell, you must complete the following procedures:</span></span>

* <span data-ttu-id="fe44c-120">Création d’un groupe de ressources Azure</span><span class="sxs-lookup"><span data-stu-id="fe44c-120">Create an Azure resource group</span></span>
* <span data-ttu-id="fe44c-121">Création d'un compte Azure Storage</span><span class="sxs-lookup"><span data-stu-id="fe44c-121">Create an Azure Storage account</span></span>
* <span data-ttu-id="fe44c-122">Création d'un conteneur d'objets blob Azure</span><span class="sxs-lookup"><span data-stu-id="fe44c-122">Create an Azure Blob container</span></span>
* <span data-ttu-id="fe44c-123">Création d'un cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="fe44c-123">Create an HDInsight cluster</span></span>

<span data-ttu-id="fe44c-124">Le script suivant montre comment créer un nouveau cluster :</span><span class="sxs-lookup"><span data-stu-id="fe44c-124">The following script demonstrates how to create a new cluster:</span></span>

<span data-ttu-id="fe44c-125">[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster.ps1?range=5-71)]</span><span class="sxs-lookup"><span data-stu-id="fe44c-125">[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster.ps1?range=5-71)]</span></span>

<span data-ttu-id="fe44c-126">Les valeurs que vous spécifiez pour la connexion du cluster sont utilisées pour créer le compte d’utilisateur Hadoop pour le cluster.</span><span class="sxs-lookup"><span data-stu-id="fe44c-126">The values you specify for the cluster login are used to create the Hadoop user account for the cluster.</span></span> <span data-ttu-id="fe44c-127">Utilisez ce compte pour la connexion aux services hébergés sur le cluster, tels que des interfaces utilisateur ou des API REST.</span><span class="sxs-lookup"><span data-stu-id="fe44c-127">Use this account to connect to services hosted on the cluster such as web UIs or REST APIs.</span></span>

<span data-ttu-id="fe44c-128">Les valeurs que vous spécifiez pour l’utilisateur SSH sont utilisées pour créer l’utilisateur SSH pour le cluster.</span><span class="sxs-lookup"><span data-stu-id="fe44c-128">The values you specify for the SSH user are used to create the SSH user for the cluster.</span></span> <span data-ttu-id="fe44c-129">Utilisez ce compte pour démarrer une session SSH à distance sur le cluster et pour exécuter des tâches.</span><span class="sxs-lookup"><span data-stu-id="fe44c-129">Use this account to start a remote SSH session on the cluster and run jobs.</span></span> <span data-ttu-id="fe44c-130">Pour plus d’informations, consultez le document [Utiliser SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="fe44c-130">For more information, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fe44c-131">Si vous envisagez d’utiliser plus de 32 nœuds de travail lors de la création du cluster ou en faisant évoluer le cluster après sa création, vous devez également spécifier une taille de nœud principal avec au moins 8 cœurs et 14 Go de RAM.</span><span class="sxs-lookup"><span data-stu-id="fe44c-131">If you plan to use more than 32 worker nodes (either at cluster creation or by scaling the cluster after creation), you must also specify a head node size with at least 8 cores and 14 GB of RAM.</span></span>
>
> <span data-ttu-id="fe44c-132">Pour plus d’informations sur les tailles de nœud et les coûts associés, consultez [Tarification HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="fe44c-132">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

<span data-ttu-id="fe44c-133">La création d’un cluster peut prendre jusqu’à 20 minutes.</span><span class="sxs-lookup"><span data-stu-id="fe44c-133">It can take up to 20 minutes to create a cluster.</span></span>

## <a name="create-cluster-configuration-object"></a><span data-ttu-id="fe44c-134">Création de cluster : objet de configuration</span><span class="sxs-lookup"><span data-stu-id="fe44c-134">Create cluster: Configuration object</span></span>

<span data-ttu-id="fe44c-135">Vous pouvez également créer un objet de configuration HDInsight à l’aide de l’applet de commande `New-AzureRmHDInsightClusterConfig`.</span><span class="sxs-lookup"><span data-stu-id="fe44c-135">You can also create an HDInsight configuration object using `New-AzureRmHDInsightClusterConfig` cmdlet.</span></span> <span data-ttu-id="fe44c-136">Il est ensuite possible de modifier cet objet de configuration pour activer des options de configuration supplémentaires pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="fe44c-136">You can then modify this configuration object to enable additional configuration options for your cluster.</span></span> <span data-ttu-id="fe44c-137">Enfin, utilisez le paramètre `-Config` de l’applet de commande `New-AzureRmHDInsightCluster` pour utiliser la configuration.</span><span class="sxs-lookup"><span data-stu-id="fe44c-137">Finally, use the `-Config` parameter of the `New-AzureRmHDInsightCluster` cmdlet to use the configuration.</span></span>

<span data-ttu-id="fe44c-138">Le script suivant crée un objet de configuration pour configurer un R Server sur le type de cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fe44c-138">The following script creates a configuration object to configure an R Server on HDInsight cluster type.</span></span> <span data-ttu-id="fe44c-139">La configuration active un nœud de périmètre, RStudio et un compte de stockage supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="fe44c-139">The configuration enables an edge node, RStudio, and an additional storage account.</span></span>

<span data-ttu-id="fe44c-140">[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster-with-config.ps1?range=59-98)]</span><span class="sxs-lookup"><span data-stu-id="fe44c-140">[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster-with-config.ps1?range=59-98)]</span></span>

> [!WARNING]
> <span data-ttu-id="fe44c-141">L’utilisation d’un compte de stockage dans un autre emplacement que le cluster HDInsight n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="fe44c-141">Using a storage account in a different location than the HDInsight cluster is not supported.</span></span> <span data-ttu-id="fe44c-142">Pour cet exemple, créez le compte de stockage supplémentaire dans le même emplacement que le serveur.</span><span class="sxs-lookup"><span data-stu-id="fe44c-142">When using this example, create the additional storage account in the same location as the server.</span></span>

## <a name="customize-clusters"></a><span data-ttu-id="fe44c-143">Personnalisation des clusters</span><span class="sxs-lookup"><span data-stu-id="fe44c-143">Customize clusters</span></span>

* <span data-ttu-id="fe44c-144">Consultez [Personnalisation de clusters HDInsight à l’aide de Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="fe44c-144">See [Customize HDInsight clusters using Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell).</span></span>
* <span data-ttu-id="fe44c-145">Consultez [Personnalisation de clusters HDInsight à l’aide d’une action de script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="fe44c-145">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="fe44c-146">Suppression du cluster</span><span class="sxs-lookup"><span data-stu-id="fe44c-146">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="fe44c-147">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="fe44c-147">Troubleshoot</span></span>

<span data-ttu-id="fe44c-148">Si vous rencontrez des problèmes lors de la création de clusters HDInsight, reportez-vous aux [exigences de contrôle d’accès](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="fe44c-148">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe44c-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fe44c-149">Next steps</span></span>

<span data-ttu-id="fe44c-150">Maintenant que vous avez créé un cluster HDInsight, parcourez les ressources ci-dessous pour apprendre à l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="fe44c-150">Now that you have successfully created an HDInsight cluster, use the following resources to learn how to work with your cluster.</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="fe44c-151">Clusters Hadoop</span><span class="sxs-lookup"><span data-stu-id="fe44c-151">Hadoop clusters</span></span>

* [<span data-ttu-id="fe44c-152">Utilisation de Hive avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="fe44c-152">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="fe44c-153">Utilisation de Pig avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="fe44c-153">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="fe44c-154">Utilisation de MapReduce avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="fe44c-154">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="fe44c-155">Clusters HBase</span><span class="sxs-lookup"><span data-stu-id="fe44c-155">HBase clusters</span></span>

* [<span data-ttu-id="fe44c-156">Prise en main de HBase sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="fe44c-156">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="fe44c-157">Développement d’applications Java pour HBase sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="fe44c-157">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="fe44c-158">Clusters Storm</span><span class="sxs-lookup"><span data-stu-id="fe44c-158">Storm clusters</span></span>

* [<span data-ttu-id="fe44c-159">Développement de topologies Java pour Storm sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="fe44c-159">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="fe44c-160">Utilisation de composants Python dans Storm sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="fe44c-160">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="fe44c-161">Déploiement et analyse des topologies avec Storm sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="fe44c-161">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)

### <a name="spark-clusters"></a><span data-ttu-id="fe44c-162">Clusters Spark</span><span class="sxs-lookup"><span data-stu-id="fe44c-162">Spark clusters</span></span>

* [<span data-ttu-id="fe44c-163">Créer une application autonome avec Scala</span><span class="sxs-lookup"><span data-stu-id="fe44c-163">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="fe44c-164">Exécution de travaux à distance avec Livy sur un cluster Spark</span><span class="sxs-lookup"><span data-stu-id="fe44c-164">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)
* [<span data-ttu-id="fe44c-165">Spark avec BI : effectuez une analyse interactive des données à l’aide de Spark dans HDInsight avec des outils BI</span><span class="sxs-lookup"><span data-stu-id="fe44c-165">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="fe44c-166">Spark avec Machine Learning : utilisez Spark dans HDInsight pour prédire les résultats de l’inspection des aliments</span><span class="sxs-lookup"><span data-stu-id="fe44c-166">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="fe44c-167">Streaming Spark : utilisez Spark dans HDInsight pour créer des applications de streaming en continu en temps réel</span><span class="sxs-lookup"><span data-stu-id="fe44c-167">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)

