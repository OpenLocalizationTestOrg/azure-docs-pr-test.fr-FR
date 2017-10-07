---
title: les clusters aaaManage Hadoop dans HDInsight avec PowerShell - Azure | Documents Microsoft
description: "Découvrez comment tooperform administration tâches pour hello clusters Hadoop dans HDInsight à l’aide d’Azure PowerShell."
services: hdinsight
editor: cgronlun
manager: jhubbard
tags: azure-portal
author: mumian
documentationcenter: 
ms.assetid: bfdfa754-18e5-4ef9-b0d6-2dbdcebc0283
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 3df082d752fa8c703db82a54b82b740290af6729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-azure-powershell"></a><span data-ttu-id="fa127-103">Gestion des clusters Hadoop dans HDInsight au moyen d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="fa127-103">Manage Hadoop clusters in HDInsight by using Azure PowerShell</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="fa127-104">Azure PowerShell est un environnement de script puissant que vous pouvez utiliser toocontrol et automatiser le déploiement de hello et la gestion de vos charges de travail dans Azure.</span><span class="sxs-lookup"><span data-stu-id="fa127-104">Azure PowerShell is a powerful scripting environment that you can use toocontrol and automate hello deployment and management of your workloads in Azure.</span></span> <span data-ttu-id="fa127-105">Dans cet article, vous allez apprendre comment utilisent des clusters Hadoop de toomanage dans Azure HDInsight à l’aide d’une console Azure PowerShell locale via hello de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fa127-105">In this article, you will learn how toomanage Hadoop clusters in Azure HDInsight by using a local Azure PowerShell console through hello use of Windows PowerShell.</span></span> <span data-ttu-id="fa127-106">Pour la liste hello Hello applets de commande HDInsight PowerShell, consultez [référence d’applet de commande HDInsight][hdinsight-powershell-reference].</span><span class="sxs-lookup"><span data-stu-id="fa127-106">For hello list of hello HDInsight PowerShell cmdlets, see [HDInsight cmdlet reference][hdinsight-powershell-reference].</span></span>

<span data-ttu-id="fa127-107">**Configuration requise**</span><span class="sxs-lookup"><span data-stu-id="fa127-107">**Prerequisites**</span></span>

<span data-ttu-id="fa127-108">Avant de commencer cet article, vous devez disposer de hello :</span><span class="sxs-lookup"><span data-stu-id="fa127-108">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="fa127-109">**Un abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="fa127-109">**An Azure subscription**.</span></span> <span data-ttu-id="fa127-110">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="fa127-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="install-azure-powershell"></a><span data-ttu-id="fa127-111">Installation d'Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="fa127-111">Install Azure PowerShell</span></span>
[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

<span data-ttu-id="fa127-112">Si vous avez installé Azure PowerShell version 0.9x, vous devez le désinstaller avant d’installer une version plus récente.</span><span class="sxs-lookup"><span data-stu-id="fa127-112">If you have installed Azure PowerShell version 0.9x, you must uninstall it before installing a newer version.</span></span>

<span data-ttu-id="fa127-113">version de hello toocheck de hello installé PowerShell :</span><span class="sxs-lookup"><span data-stu-id="fa127-113">toocheck hello version of hello installed PowerShell:</span></span>

    Get-Module *azure*

<span data-ttu-id="fa127-114">toouninstall hello ancienne version, exécuter des programmes et fonctionnalités dans le panneau de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="fa127-114">toouninstall hello older version, run Programs and Features in hello control panel.</span></span>

## <a name="create-clusters"></a><span data-ttu-id="fa127-115">Créer des clusters</span><span class="sxs-lookup"><span data-stu-id="fa127-115">Create clusters</span></span>
<span data-ttu-id="fa127-116">Consultez la page [Créer des clusters basés sur Linux dans HDInsight à l’aide d’Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="fa127-116">See [Create Linux-based clusters in HDInsight using Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)</span></span>

## <a name="list-clusters"></a><span data-ttu-id="fa127-117">Énumérer les clusters</span><span class="sxs-lookup"><span data-stu-id="fa127-117">List clusters</span></span>
<span data-ttu-id="fa127-118">Utilisez hello suivant toolist de commande tous les clusters dans l’abonnement actif de hello :</span><span class="sxs-lookup"><span data-stu-id="fa127-118">Use hello following command toolist all clusters in hello current subscription:</span></span>

    Get-AzureRmHDInsightCluster

## <a name="show-cluster"></a><span data-ttu-id="fa127-119">Afficher le cluster</span><span class="sxs-lookup"><span data-stu-id="fa127-119">Show cluster</span></span>
<span data-ttu-id="fa127-120">Utilisez hello les détails de tooshow de commande d’un cluster spécifique dans l’abonnement actif de hello suivants :</span><span class="sxs-lookup"><span data-stu-id="fa127-120">Use hello following command tooshow details of a specific cluster in hello current subscription:</span></span>

    Get-AzureRmHDInsightCluster -ClusterName <Cluster Name>

## <a name="delete-clusters"></a><span data-ttu-id="fa127-121">Suppression des clusters</span><span class="sxs-lookup"><span data-stu-id="fa127-121">Delete clusters</span></span>
<span data-ttu-id="fa127-122">Utilisez hello suivant commande toodelete un cluster :</span><span class="sxs-lookup"><span data-stu-id="fa127-122">Use hello following command toodelete a cluster:</span></span>

    Remove-AzureRmHDInsightCluster -ClusterName <Cluster Name>

<span data-ttu-id="fa127-123">Vous pouvez également supprimer un cluster en supprimant le groupe de ressources hello contient hello cluster.</span><span class="sxs-lookup"><span data-stu-id="fa127-123">You can also delete a cluster by removing hello resource group that contains hello cluster.</span></span> <span data-ttu-id="fa127-124">Notez cette opération supprimera toutes les ressources hello groupe hello, y compris le compte de stockage par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="fa127-124">Please note, this will delete all hello resources in hello group including hello default storage account.</span></span>

    Remove-AzureRmResourceGroup -Name <Resource Group Name>

## <a name="scale-clusters"></a><span data-ttu-id="fa127-125">Mise à l’échelle des clusters</span><span class="sxs-lookup"><span data-stu-id="fa127-125">Scale clusters</span></span>
<span data-ttu-id="fa127-126">cluster Hello fonctionnalité de mise à l’échelle permet un nombre de hello toochange de nœuds de travail utilisé par un cluster qui s’exécute dans Azure HDInsight sans avoir toore-créer le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="fa127-126">hello cluster scaling feature allows you toochange hello number of worker nodes used by a cluster that is running in Azure HDInsight without having toore-create hello cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="fa127-127">Seuls les clusters ayant la version 3.1.3 de HDInsight ou une version ultérieure sont pris en charge.</span><span class="sxs-lookup"><span data-stu-id="fa127-127">Only clusters with HDInsight version 3.1.3 or higher are supported.</span></span> <span data-ttu-id="fa127-128">Si vous ne savez pas de version hello de votre cluster, vous pouvez vérifier la page de propriétés hello.</span><span class="sxs-lookup"><span data-stu-id="fa127-128">If you are unsure of hello version of your cluster, you can check hello Properties page.</span></span>  <span data-ttu-id="fa127-129">Voir [Énumération et affichage des clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="fa127-129">See [List and show clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span></span>
>
>

<span data-ttu-id="fa127-130">impact Hello modifiant nombre hello de nœuds de données pour chaque type de cluster pris en charge par HDInsight :</span><span class="sxs-lookup"><span data-stu-id="fa127-130">hello impact of changing hello number of data nodes for each type of cluster supported by HDInsight:</span></span>

* <span data-ttu-id="fa127-131">Hadoop</span><span class="sxs-lookup"><span data-stu-id="fa127-131">Hadoop</span></span>

    <span data-ttu-id="fa127-132">Vous pouvez augmenter de façon transparente nombre hello de nœuds de travail dans un cluster Hadoop qui est en cours d’exécution sans impact sur toutes les tâches en attente ou en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="fa127-132">You can seamlessly increase hello number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span></span> <span data-ttu-id="fa127-133">Nouvelles tâches peuvent également être soumises pendant que l’opération de hello est en cours.</span><span class="sxs-lookup"><span data-stu-id="fa127-133">New jobs can also be submitted while hello operation is in progress.</span></span> <span data-ttu-id="fa127-134">Échecs dans une opération de mise à l’échelle sont correctement gérés afin que hello cluster est toujours conservé dans un état fonctionnel.</span><span class="sxs-lookup"><span data-stu-id="fa127-134">Failures in a scaling operation are gracefully handled so that hello cluster is always left in a functional state.</span></span>

    <span data-ttu-id="fa127-135">Lorsqu’un cluster Hadoop est réduite en réduisant le nombre de hello de nœuds de données, certains services hello dans un cluster de hello sont redémarrés.</span><span class="sxs-lookup"><span data-stu-id="fa127-135">When a Hadoop cluster is scaled down by reducing hello number of data nodes, some of hello services in hello cluster are restarted.</span></span> <span data-ttu-id="fa127-136">Ainsi, en cours d’exécution et en attente de toofail de travaux à l’achèvement de hello Hello opération de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="fa127-136">This causes all running and pending jobs toofail at hello completion of hello scaling operation.</span></span> <span data-ttu-id="fa127-137">Vous pouvez, toutefois, renvoyer des tâches de hello une fois l’opération hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="fa127-137">You can, however, resubmit hello jobs once hello operation is complete.</span></span>
* <span data-ttu-id="fa127-138">HBase</span><span class="sxs-lookup"><span data-stu-id="fa127-138">HBase</span></span>

    <span data-ttu-id="fa127-139">Vous pouvez accéder en toute transparence ajouter ou supprimer le cluster de nœuds tooyour HBase pendant son exécution.</span><span class="sxs-lookup"><span data-stu-id="fa127-139">You can seamlessly add or remove nodes tooyour HBase cluster while it is running.</span></span> <span data-ttu-id="fa127-140">Serveurs régionaux sont équilibrés automatiquement après quelques minutes d’achèvement hello opération de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="fa127-140">Regional Servers are automatically balanced within a few minutes of completing hello scaling operation.</span></span> <span data-ttu-id="fa127-141">Toutefois, vous pouvez équilibrer manuellement les serveurs régionaux hello en vous connectant à un nœud principal de toohello du cluster et hello en cours d’exécution suivant des commandes dans une fenêtre d’invite de commandes :</span><span class="sxs-lookup"><span data-stu-id="fa127-141">However, you can also manually balance hello regional servers by logging in toohello headnode of cluster and running hello following commands from a command prompt window:</span></span>

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* <span data-ttu-id="fa127-142">Storm</span><span class="sxs-lookup"><span data-stu-id="fa127-142">Storm</span></span>

    <span data-ttu-id="fa127-143">Vous pouvez accéder en toute transparence ajouter ou supprimer le cluster de données nœuds tooyour Storm pendant son exécution.</span><span class="sxs-lookup"><span data-stu-id="fa127-143">You can seamlessly add or remove data nodes tooyour Storm cluster while it is running.</span></span> <span data-ttu-id="fa127-144">Mais après la réussite de l’opération de mise à l’échelle de hello, vous devrez topologie de hello toorebalance.</span><span class="sxs-lookup"><span data-stu-id="fa127-144">But after a successful completion of hello scaling operation, you will need toorebalance hello topology.</span></span>

    <span data-ttu-id="fa127-145">Cela peut se faire de deux façons à l’aide de :</span><span class="sxs-lookup"><span data-stu-id="fa127-145">Rebalancing can be accomplished in two ways:</span></span>

  * <span data-ttu-id="fa127-146">l'interface utilisateur Web de Storm</span><span class="sxs-lookup"><span data-stu-id="fa127-146">Storm web UI</span></span>
  * <span data-ttu-id="fa127-147">l’outil d’interface de ligne de commande (CLI)</span><span class="sxs-lookup"><span data-stu-id="fa127-147">Command-line interface (CLI) tool</span></span>

    <span data-ttu-id="fa127-148">Reportez-vous toohello [documentation d’Apache Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="fa127-148">Please refer toohello [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span></span>

    <span data-ttu-id="fa127-149">interface utilisateur web de Storm Hello est disponible sur le cluster HDInsight de hello :</span><span class="sxs-lookup"><span data-stu-id="fa127-149">hello Storm web UI is available on hello HDInsight cluster:</span></span>

    ![HDInsight storm mise à l’échelle rééquilibrage](./media/hdinsight-administer-use-management-portal/hdinsight.portal.scale.cluster.png)

    <span data-ttu-id="fa127-151">Voici un exemple comment toouse hello CLI commande topologie de Storm toorebalance hello :</span><span class="sxs-lookup"><span data-stu-id="fa127-151">Here is an example how toouse hello CLI command toorebalance hello Storm topology:</span></span>

        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

<span data-ttu-id="fa127-152">hello toochange taille du cluster Hadoop en utilisant Azure PowerShell, exécutez hello de commande suivante à partir d’un ordinateur client :</span><span class="sxs-lookup"><span data-stu-id="fa127-152">toochange hello Hadoop cluster size by using Azure PowerShell, run hello following command from a client machine:</span></span>

    Set-AzureRmHDInsightClusterSize -ClusterName <Cluster Name> -TargetInstanceCount <NewSize>


## <a name="grantrevoke-access"></a><span data-ttu-id="fa127-153">Octroyer/Révoquer l’accès</span><span class="sxs-lookup"><span data-stu-id="fa127-153">Grant/revoke access</span></span>
<span data-ttu-id="fa127-154">Clusters HDInsight ont hello suivant (tous ces services ont des points de terminaison RESTful) des services web HTTP :</span><span class="sxs-lookup"><span data-stu-id="fa127-154">HDInsight clusters have hello following HTTP web services (all of these services have RESTful endpoints):</span></span>

* <span data-ttu-id="fa127-155">ODBC</span><span class="sxs-lookup"><span data-stu-id="fa127-155">ODBC</span></span>
* <span data-ttu-id="fa127-156">JDBC</span><span class="sxs-lookup"><span data-stu-id="fa127-156">JDBC</span></span>
* <span data-ttu-id="fa127-157">Ambari</span><span class="sxs-lookup"><span data-stu-id="fa127-157">Ambari</span></span>
* <span data-ttu-id="fa127-158">Oozie</span><span class="sxs-lookup"><span data-stu-id="fa127-158">Oozie</span></span>
* <span data-ttu-id="fa127-159">Templeton</span><span class="sxs-lookup"><span data-stu-id="fa127-159">Templeton</span></span>

<span data-ttu-id="fa127-160">Par défaut, l'accès à ces services est octroyé.</span><span class="sxs-lookup"><span data-stu-id="fa127-160">By default, these services are granted for access.</span></span> <span data-ttu-id="fa127-161">Vous pouvez révoquer ou octroyer l’accès de hello.</span><span class="sxs-lookup"><span data-stu-id="fa127-161">You can revoke/grant hello access.</span></span> <span data-ttu-id="fa127-162">toorevoke :</span><span class="sxs-lookup"><span data-stu-id="fa127-162">toorevoke:</span></span>

    Revoke-AzureRmHDInsightHttpServicesAccess -ClusterName <Cluster Name>

<span data-ttu-id="fa127-163">toogrant :</span><span class="sxs-lookup"><span data-stu-id="fa127-163">toogrant:</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    # Credential option 1
    $hadoopUserName = "admin"
    $hadoopUserPassword = "<Enter hello Password>"
    $hadoopUserPW = ConvertTo-SecureString -String $hadoopUserPassword -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential($hadoopUserName,$hadoopUserPW)

    # Credential option 2
    #$credential = Get-Credential -Message "Enter hello HTTP username and password:" -UserName "admin"

    Grant-AzureRmHDInsightHttpServicesAccess -ClusterName $clusterName -HttpCredential $credential

> [!NOTE]
> <span data-ttu-id="fa127-164">Par attribution/révocation de l’accès hello, vous allez réinitialiser le mot de passe et le nom d’utilisateur de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="fa127-164">By granting/revoking hello access, you will reset hello cluster user name and password.</span></span>
>
>

<span data-ttu-id="fa127-165">Peut également être cela via le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="fa127-165">This can also be done via hello Portal.</span></span> <span data-ttu-id="fa127-166">Consultez [HDInsight de gérer à l’aide de hello portail Azure][hdinsight-admin-portal].</span><span class="sxs-lookup"><span data-stu-id="fa127-166">See [Administer HDInsight by using hello Azure portal][hdinsight-admin-portal].</span></span>

## <a name="update-http-user-credentials"></a><span data-ttu-id="fa127-167">Mettre à jour les informations d’identification de l’utilisateur HTTP</span><span class="sxs-lookup"><span data-stu-id="fa127-167">Update HTTP user credentials</span></span>
<span data-ttu-id="fa127-168">Il est même hello procédure en tant que [Grant/revoke HTTP accès](#grant/revoke-access). Si le cluster de hello a été accordée hello accès HTTP, vous devez d’abord la révoquer.</span><span class="sxs-lookup"><span data-stu-id="fa127-168">It is hello same procedure as [Grant/revoke HTTP access](#grant/revoke-access).If hello cluster has been granted hello HTTP access, you must first revoke it.</span></span>  <span data-ttu-id="fa127-169">Et accorder l’accès hello avec nouvelles informations d’identification utilisateur HTTP.</span><span class="sxs-lookup"><span data-stu-id="fa127-169">And then grant hello access with new HTTP user credentials.</span></span>

## <a name="find-hello-default-storage-account"></a><span data-ttu-id="fa127-170">Recherchez le compte de stockage par défaut hello</span><span class="sxs-lookup"><span data-stu-id="fa127-170">Find hello default storage account</span></span>
<span data-ttu-id="fa127-171">Hello Powershell script suivant montre comment les tooget hello nom de compte de stockage par défaut et hello clé de compte de stockage par défaut pour un cluster.</span><span class="sxs-lookup"><span data-stu-id="fa127-171">hello following Powershell script demonstrates how tooget hello default storage account name and hello default storage account key for a cluster.</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup
    $defaultStorageAccountName = ($cluster.DefaultStorageAccount).Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $cluster.DefaultStorageContainer
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey

## <a name="find-hello-resource-group"></a><span data-ttu-id="fa127-172">Recherchez le groupe de ressources hello</span><span class="sxs-lookup"><span data-stu-id="fa127-172">Find hello resource group</span></span>
<span data-ttu-id="fa127-173">En mode de gestionnaire de ressources hello, chaque cluster HDInsight appartient le groupe de ressources Azure tooan.</span><span class="sxs-lookup"><span data-stu-id="fa127-173">In hello Resource Manager mode, each HDInsight cluster belongs tooan Azure resource group.</span></span>  <span data-ttu-id="fa127-174">groupe de ressources toofind hello :</span><span class="sxs-lookup"><span data-stu-id="fa127-174">toofind hello resource group:</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup


## <a name="submit-jobs"></a><span data-ttu-id="fa127-175">Soumettre les travaux</span><span class="sxs-lookup"><span data-stu-id="fa127-175">Submit jobs</span></span>
<span data-ttu-id="fa127-176">**tâches MapReduce toosubmit**</span><span class="sxs-lookup"><span data-stu-id="fa127-176">**toosubmit MapReduce jobs**</span></span>

<span data-ttu-id="fa127-177">Consultez [Exécution des exemples Hadoop MapReduce dans HDInsight basé sur Windows](hdinsight-run-samples.md)</span><span class="sxs-lookup"><span data-stu-id="fa127-177">See [Run Hadoop MapReduce samples in Windows-based HDInsight](hdinsight-run-samples.md).</span></span>

<span data-ttu-id="fa127-178">**travaux de ruche toosubmit**</span><span class="sxs-lookup"><span data-stu-id="fa127-178">**toosubmit Hive jobs**</span></span>

<span data-ttu-id="fa127-179">Consultez [Exécution de requêtes Hive avec PowerShell](hdinsight-hadoop-use-hive-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="fa127-179">See [Run Hive queries using PowerShell](hdinsight-hadoop-use-hive-powershell.md).</span></span>

<span data-ttu-id="fa127-180">**travaux de Pig toosubmit**</span><span class="sxs-lookup"><span data-stu-id="fa127-180">**toosubmit Pig jobs**</span></span>

<span data-ttu-id="fa127-181">Consultez [Exécution de tâches Pig avec PowerShell](hdinsight-hadoop-use-pig-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="fa127-181">See [Run Pig jobs using PowerShell](hdinsight-hadoop-use-pig-powershell.md).</span></span>

<span data-ttu-id="fa127-182">**travaux de Sqoop toosubmit**</span><span class="sxs-lookup"><span data-stu-id="fa127-182">**toosubmit Sqoop jobs**</span></span>

<span data-ttu-id="fa127-183">Consultez l'article [Utilisation de Sqoop avec HDInsight](hdinsight-use-sqoop.md).</span><span class="sxs-lookup"><span data-stu-id="fa127-183">See [Use Sqoop with HDInsight](hdinsight-use-sqoop.md).</span></span>

<span data-ttu-id="fa127-184">**travaux de Oozie toosubmit**</span><span class="sxs-lookup"><span data-stu-id="fa127-184">**toosubmit Oozie jobs**</span></span>

<span data-ttu-id="fa127-185">Consultez [Oozie utilisation avec Hadoop toodefine et exécuter un flux de travail dans HDInsight](hdinsight-use-oozie.md).</span><span class="sxs-lookup"><span data-stu-id="fa127-185">See [Use Oozie with Hadoop toodefine and run a workflow in HDInsight](hdinsight-use-oozie.md).</span></span>

## <a name="upload-data-tooazure-blob-storage"></a><span data-ttu-id="fa127-186">Télécharger le stockage d’objets Blob de données tooAzure</span><span class="sxs-lookup"><span data-stu-id="fa127-186">Upload data tooAzure Blob storage</span></span>
<span data-ttu-id="fa127-187">Consultez [télécharger des données tooHDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="fa127-187">See [Upload data tooHDInsight][hdinsight-upload-data].</span></span>

## <a name="see-also"></a><span data-ttu-id="fa127-188">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="fa127-188">See Also</span></span>
* <span data-ttu-id="fa127-189">[Documentation de référence des applets de commande HDInsight][hdinsight-powershell-reference]</span><span class="sxs-lookup"><span data-stu-id="fa127-189">[HDInsight cmdlet reference documentation][hdinsight-powershell-reference]</span></span>
* <span data-ttu-id="fa127-190">[Administrer HDInsight à l’aide de hello portail Azure][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="fa127-190">[Administer HDInsight by using hello Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="fa127-191">[Administration de HDInsight à l’aide de l’interface de ligne de commande][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="fa127-191">[Administer HDInsight using a command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="fa127-192">[Création de clusters HDInsight][hdinsight-provision]</span><span class="sxs-lookup"><span data-stu-id="fa127-192">[Create HDInsight clusters][hdinsight-provision]</span></span>
* <span data-ttu-id="fa127-193">[Télécharger des données tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="fa127-193">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="fa127-194">[Envoi de tâches Hadoop par programme][hdinsight-submit-jobs]</span><span class="sxs-lookup"><span data-stu-id="fa127-194">[Submit Hadoop jobs programmatically][hdinsight-submit-jobs]</span></span>
* <span data-ttu-id="fa127-195">[Prise en main d’Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="fa127-195">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-provision-custom-options]: hdinsight-hadoop-provision-linux-clusters.md#configuration
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[hdinsight-admin-cli]: hdinsight-administer-use-command-line.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-flight]: hdinsight-analyze-flight-delay-data.md

[hdinsight-powershell-reference]: https://msdn.microsoft.com/library/dn858087.aspx

[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[image-hdi-ps-provision]: ./media/hdinsight-administer-use-powershell/HDI.PS.Provision.png
