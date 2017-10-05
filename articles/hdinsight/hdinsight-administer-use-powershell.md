---
title: Gestion des clusters Hadoop dans HDInsight avec PowerShell - Azure | Microsoft Docs
description: "Découvrez comment effectuer des tâches d'administration pour les clusters Hadoop dans HDInsight au moyen d'Azure PowerShell."
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
ms.openlocfilehash: c47dabd7c4aa4ba0be08c419989e536711f03677
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-azure-powershell"></a><span data-ttu-id="72dc4-103">Gestion des clusters Hadoop dans HDInsight au moyen d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="72dc4-103">Manage Hadoop clusters in HDInsight by using Azure PowerShell</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="72dc4-104">Azure PowerShell est un environnement de création de scripts vous permettant de contrôler et d'automatiser le déploiement et la gestion de vos charges de travail dans Azure.</span><span class="sxs-lookup"><span data-stu-id="72dc4-104">Azure PowerShell is a powerful scripting environment that you can use to control and automate the deployment and management of your workloads in Azure.</span></span> <span data-ttu-id="72dc4-105">Cet article vous explique comment gérer les clusters Hadoop dans Azure HDInsight en utilisant la console locale Azure PowerShell par le biais de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="72dc4-105">In this article, you will learn how to manage Hadoop clusters in Azure HDInsight by using a local Azure PowerShell console through the use of Windows PowerShell.</span></span> <span data-ttu-id="72dc4-106">Pour la liste des applets de commande PowerShell pour HDInsight, consultez la rubrique [Référence des applets de commande HDInsight][hdinsight-powershell-reference].</span><span class="sxs-lookup"><span data-stu-id="72dc4-106">For the list of the HDInsight PowerShell cmdlets, see [HDInsight cmdlet reference][hdinsight-powershell-reference].</span></span>

<span data-ttu-id="72dc4-107">**Configuration requise**</span><span class="sxs-lookup"><span data-stu-id="72dc4-107">**Prerequisites**</span></span>

<span data-ttu-id="72dc4-108">Avant de commencer cet article, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="72dc4-108">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="72dc4-109">**Un abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="72dc4-109">**An Azure subscription**.</span></span> <span data-ttu-id="72dc4-110">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="72dc4-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="install-azure-powershell"></a><span data-ttu-id="72dc4-111">Installation d'Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="72dc4-111">Install Azure PowerShell</span></span>
[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

<span data-ttu-id="72dc4-112">Si vous avez installé Azure PowerShell version 0.9x, vous devez le désinstaller avant d’installer une version plus récente.</span><span class="sxs-lookup"><span data-stu-id="72dc4-112">If you have installed Azure PowerShell version 0.9x, you must uninstall it before installing a newer version.</span></span>

<span data-ttu-id="72dc4-113">Pour connaître la version de PowerShell installée :</span><span class="sxs-lookup"><span data-stu-id="72dc4-113">To check the version of the installed PowerShell:</span></span>

    Get-Module *azure*

<span data-ttu-id="72dc4-114">Pour désinstaller l’ancienne version, exécutez Programmes et fonctionnalités dans le Panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="72dc4-114">To uninstall the older version, run Programs and Features in the control panel.</span></span>

## <a name="create-clusters"></a><span data-ttu-id="72dc4-115">Créer des clusters</span><span class="sxs-lookup"><span data-stu-id="72dc4-115">Create clusters</span></span>
<span data-ttu-id="72dc4-116">Consultez la page [Créer des clusters basés sur Linux dans HDInsight à l’aide d’Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="72dc4-116">See [Create Linux-based clusters in HDInsight using Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)</span></span>

## <a name="list-clusters"></a><span data-ttu-id="72dc4-117">Énumérer les clusters</span><span class="sxs-lookup"><span data-stu-id="72dc4-117">List clusters</span></span>
<span data-ttu-id="72dc4-118">Utilisez la commande suivante pour afficher la liste de tous les clusters de l’abonnement actif :</span><span class="sxs-lookup"><span data-stu-id="72dc4-118">Use the following command to list all clusters in the current subscription:</span></span>

    Get-AzureRmHDInsightCluster

## <a name="show-cluster"></a><span data-ttu-id="72dc4-119">Afficher le cluster</span><span class="sxs-lookup"><span data-stu-id="72dc4-119">Show cluster</span></span>
<span data-ttu-id="72dc4-120">Utilisez la commande suivante pour afficher les détails d’un cluster spécifique dans l’abonnement actif :</span><span class="sxs-lookup"><span data-stu-id="72dc4-120">Use the following command to show details of a specific cluster in the current subscription:</span></span>

    Get-AzureRmHDInsightCluster -ClusterName <Cluster Name>

## <a name="delete-clusters"></a><span data-ttu-id="72dc4-121">Suppression des clusters</span><span class="sxs-lookup"><span data-stu-id="72dc4-121">Delete clusters</span></span>
<span data-ttu-id="72dc4-122">Utilisez la commande suivante pour supprimer un cluster :</span><span class="sxs-lookup"><span data-stu-id="72dc4-122">Use the following command to delete a cluster:</span></span>

    Remove-AzureRmHDInsightCluster -ClusterName <Cluster Name>

<span data-ttu-id="72dc4-123">Vous pouvez également supprimer un cluster en supprimant le groupe de ressources qui le contient.</span><span class="sxs-lookup"><span data-stu-id="72dc4-123">You can also delete a cluster by removing the resource group that contains the cluster.</span></span> <span data-ttu-id="72dc4-124">Notez que cette opération supprime toutes les ressources dans le groupe, notamment le compte de stockage par défaut.</span><span class="sxs-lookup"><span data-stu-id="72dc4-124">Please note, this will delete all the resources in the group including the default storage account.</span></span>

    Remove-AzureRmResourceGroup -Name <Resource Group Name>

## <a name="scale-clusters"></a><span data-ttu-id="72dc4-125">Mise à l’échelle des clusters</span><span class="sxs-lookup"><span data-stu-id="72dc4-125">Scale clusters</span></span>
<span data-ttu-id="72dc4-126">La fonctionnalité de mise à l’échelle d’un cluster vous permet de modifier le nombre de nœuds de travail utilisés par un cluster exécuté dans Azure HDInsight sans avoir à recréer ce cluster.</span><span class="sxs-lookup"><span data-stu-id="72dc4-126">The cluster scaling feature allows you to change the number of worker nodes used by a cluster that is running in Azure HDInsight without having to re-create the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="72dc4-127">Seuls les clusters ayant la version 3.1.3 de HDInsight ou une version ultérieure sont pris en charge.</span><span class="sxs-lookup"><span data-stu-id="72dc4-127">Only clusters with HDInsight version 3.1.3 or higher are supported.</span></span> <span data-ttu-id="72dc4-128">Si vous n’êtes pas sûr de la version de votre cluster, vous pouvez consulter la page Propriétés.</span><span class="sxs-lookup"><span data-stu-id="72dc4-128">If you are unsure of the version of your cluster, you can check the Properties page.</span></span>  <span data-ttu-id="72dc4-129">Voir [Énumération et affichage des clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="72dc4-129">See [List and show clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span></span>
>
>

<span data-ttu-id="72dc4-130">Impact de la modification du nombre de nœuds de données pour chaque type de cluster pris en charge par HDInsight :</span><span class="sxs-lookup"><span data-stu-id="72dc4-130">The impact of changing the number of data nodes for each type of cluster supported by HDInsight:</span></span>

* <span data-ttu-id="72dc4-131">Hadoop</span><span class="sxs-lookup"><span data-stu-id="72dc4-131">Hadoop</span></span>

    <span data-ttu-id="72dc4-132">Vous pouvez augmenter de façon continue le nombre de nœuds de travail dans un cluster Hadoop exécuté sans affecter aucune tâche en attente ou en cours.</span><span class="sxs-lookup"><span data-stu-id="72dc4-132">You can seamlessly increase the number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span></span> <span data-ttu-id="72dc4-133">De nouvelles tâches peuvent également être soumises lorsque l'opération est en cours.</span><span class="sxs-lookup"><span data-stu-id="72dc4-133">New jobs can also be submitted while the operation is in progress.</span></span> <span data-ttu-id="72dc4-134">Les défaillances dans l'opération de mise à l'échelle sont correctement gérées de sorte que le cluster reste toujours fonctionnel.</span><span class="sxs-lookup"><span data-stu-id="72dc4-134">Failures in a scaling operation are gracefully handled so that the cluster is always left in a functional state.</span></span>

    <span data-ttu-id="72dc4-135">Lorsqu’un cluster Hadoop est diminué par la réduction du nombre de nœuds de données, certains services du cluster sont redémarrés.</span><span class="sxs-lookup"><span data-stu-id="72dc4-135">When a Hadoop cluster is scaled down by reducing the number of data nodes, some of the services in the cluster are restarted.</span></span> <span data-ttu-id="72dc4-136">Pour cette raison, toutes les tâches en cours ou en attente échouent lors de la réalisation de l'opération de mise à l'échelle.</span><span class="sxs-lookup"><span data-stu-id="72dc4-136">This causes all running and pending jobs to fail at the completion of the scaling operation.</span></span> <span data-ttu-id="72dc4-137">Toutefois, vous pouvez soumettre à nouveau les tâches une fois l'opération terminée.</span><span class="sxs-lookup"><span data-stu-id="72dc4-137">You can, however, resubmit the jobs once the operation is complete.</span></span>
* <span data-ttu-id="72dc4-138">HBase</span><span class="sxs-lookup"><span data-stu-id="72dc4-138">HBase</span></span>

    <span data-ttu-id="72dc4-139">Vous pouvez ajouter ou supprimer des nœuds en continu dans votre cluster HBase lorsque celui-ci s’exécute.</span><span class="sxs-lookup"><span data-stu-id="72dc4-139">You can seamlessly add or remove nodes to your HBase cluster while it is running.</span></span> <span data-ttu-id="72dc4-140">Les serveurs régionaux sont équilibrés automatiquement quelques minutes après la fin de l’opération de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="72dc4-140">Regional Servers are automatically balanced within a few minutes of completing the scaling operation.</span></span> <span data-ttu-id="72dc4-141">Cependant, vous pouvez équilibrer manuellement des serveurs régionaux en vous connectant au nœud principal du cluster et en exécutant les commandes suivantes à partir d’une fenêtre d’invite de commandes :</span><span class="sxs-lookup"><span data-stu-id="72dc4-141">However, you can also manually balance the regional servers by logging in to the headnode of cluster and running the following commands from a command prompt window:</span></span>

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* <span data-ttu-id="72dc4-142">Storm</span><span class="sxs-lookup"><span data-stu-id="72dc4-142">Storm</span></span>

    <span data-ttu-id="72dc4-143">Vous pouvez ajouter ou supprimer des nœuds de données en continu dans votre cluster Storm lorsque celui-ci s'exécute.</span><span class="sxs-lookup"><span data-stu-id="72dc4-143">You can seamlessly add or remove data nodes to your Storm cluster while it is running.</span></span> <span data-ttu-id="72dc4-144">Mais une fois l’opération de mise à l’échelle terminée avec succès, vous devrez rééquilibrer la topologie.</span><span class="sxs-lookup"><span data-stu-id="72dc4-144">But after a successful completion of the scaling operation, you will need to rebalance the topology.</span></span>

    <span data-ttu-id="72dc4-145">Cela peut se faire de deux façons à l’aide de :</span><span class="sxs-lookup"><span data-stu-id="72dc4-145">Rebalancing can be accomplished in two ways:</span></span>

  * <span data-ttu-id="72dc4-146">l'interface utilisateur Web de Storm</span><span class="sxs-lookup"><span data-stu-id="72dc4-146">Storm web UI</span></span>
  * <span data-ttu-id="72dc4-147">l’outil d’interface de ligne de commande (CLI)</span><span class="sxs-lookup"><span data-stu-id="72dc4-147">Command-line interface (CLI) tool</span></span>

    <span data-ttu-id="72dc4-148">Pour plus d’informations, consultez la documentation [Apache Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) .</span><span class="sxs-lookup"><span data-stu-id="72dc4-148">Please refer to the [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span></span>

    <span data-ttu-id="72dc4-149">L’interface utilisateur web de Storm est disponible dans le cluster HDInsight :</span><span class="sxs-lookup"><span data-stu-id="72dc4-149">The Storm web UI is available on the HDInsight cluster:</span></span>

    ![HDInsight storm mise à l’échelle rééquilibrage](./media/hdinsight-administer-use-management-portal/hdinsight.portal.scale.cluster.png)

    <span data-ttu-id="72dc4-151">Voici un exemple relatif à l'utilisation de la commande de l'interface en ligne de commande pour rééquilibrer la topologie Storm :</span><span class="sxs-lookup"><span data-stu-id="72dc4-151">Here is an example how to use the CLI command to rebalance the Storm topology:</span></span>

        ## Reconfigure the topology "mytopology" to use 5 worker processes,
        ## the spout "blue-spout" to use 3 executors, and
        ## the bolt "yellow-bolt" to use 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

<span data-ttu-id="72dc4-152">Pour modifier la taille du cluster Hadoop à l’aide d’Azure PowerShell, exécutez la commande suivante depuis un ordinateur client :</span><span class="sxs-lookup"><span data-stu-id="72dc4-152">To change the Hadoop cluster size by using Azure PowerShell, run the following command from a client machine:</span></span>

    Set-AzureRmHDInsightClusterSize -ClusterName <Cluster Name> -TargetInstanceCount <NewSize>


## <a name="grantrevoke-access"></a><span data-ttu-id="72dc4-153">Octroyer/Révoquer l’accès</span><span class="sxs-lookup"><span data-stu-id="72dc4-153">Grant/revoke access</span></span>
<span data-ttu-id="72dc4-154">Les clusters HDInsight disposent des services web HTTP suivants (tous ces services ont des points de terminaison RESTful) :</span><span class="sxs-lookup"><span data-stu-id="72dc4-154">HDInsight clusters have the following HTTP web services (all of these services have RESTful endpoints):</span></span>

* <span data-ttu-id="72dc4-155">ODBC</span><span class="sxs-lookup"><span data-stu-id="72dc4-155">ODBC</span></span>
* <span data-ttu-id="72dc4-156">JDBC</span><span class="sxs-lookup"><span data-stu-id="72dc4-156">JDBC</span></span>
* <span data-ttu-id="72dc4-157">Ambari</span><span class="sxs-lookup"><span data-stu-id="72dc4-157">Ambari</span></span>
* <span data-ttu-id="72dc4-158">Oozie</span><span class="sxs-lookup"><span data-stu-id="72dc4-158">Oozie</span></span>
* <span data-ttu-id="72dc4-159">Templeton</span><span class="sxs-lookup"><span data-stu-id="72dc4-159">Templeton</span></span>

<span data-ttu-id="72dc4-160">Par défaut, l'accès à ces services est octroyé.</span><span class="sxs-lookup"><span data-stu-id="72dc4-160">By default, these services are granted for access.</span></span> <span data-ttu-id="72dc4-161">Vous avez la possibilité de supprimer/octroyer l'accès.</span><span class="sxs-lookup"><span data-stu-id="72dc4-161">You can revoke/grant the access.</span></span> <span data-ttu-id="72dc4-162">Pour révoquer :</span><span class="sxs-lookup"><span data-stu-id="72dc4-162">To revoke:</span></span>

    Revoke-AzureRmHDInsightHttpServicesAccess -ClusterName <Cluster Name>

<span data-ttu-id="72dc4-163">Pour octroyer :</span><span class="sxs-lookup"><span data-stu-id="72dc4-163">To grant:</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    # Credential option 1
    $hadoopUserName = "admin"
    $hadoopUserPassword = "<Enter the Password>"
    $hadoopUserPW = ConvertTo-SecureString -String $hadoopUserPassword -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential($hadoopUserName,$hadoopUserPW)

    # Credential option 2
    #$credential = Get-Credential -Message "Enter the HTTP username and password:" -UserName "admin"

    Grant-AzureRmHDInsightHttpServicesAccess -ClusterName $clusterName -HttpCredential $credential

> [!NOTE]
> <span data-ttu-id="72dc4-164">En octroyant/révoquant l’accès, vous réinitialisez le nom d’utilisateur et le mot de passe du cluster.</span><span class="sxs-lookup"><span data-stu-id="72dc4-164">By granting/revoking the access, you will reset the cluster user name and password.</span></span>
>
>

<span data-ttu-id="72dc4-165">Vous pouvez également le faire via le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="72dc4-165">This can also be done via the Portal.</span></span> <span data-ttu-id="72dc4-166">Consultez [Administration de HDInsight à l’aide du portail Azure][hdinsight-admin-portal].</span><span class="sxs-lookup"><span data-stu-id="72dc4-166">See [Administer HDInsight by using the Azure portal][hdinsight-admin-portal].</span></span>

## <a name="update-http-user-credentials"></a><span data-ttu-id="72dc4-167">Mettre à jour les informations d’identification de l’utilisateur HTTP</span><span class="sxs-lookup"><span data-stu-id="72dc4-167">Update HTTP user credentials</span></span>
<span data-ttu-id="72dc4-168">Il s’agit de la même procédure que [l’octroi et la révocation de l’accès HTTP](#grant/revoke-access). Si l’accès HTTP a été octroyé au cluster, vous devez tout d’abord le révoquer.</span><span class="sxs-lookup"><span data-stu-id="72dc4-168">It is the same procedure as [Grant/revoke HTTP access](#grant/revoke-access).If the cluster has been granted the HTTP access, you must first revoke it.</span></span>  <span data-ttu-id="72dc4-169">Octroyez ensuite l’accès avec les informations d’identification de l’utilisateur HTTP.</span><span class="sxs-lookup"><span data-stu-id="72dc4-169">And then grant the access with new HTTP user credentials.</span></span>

## <a name="find-the-default-storage-account"></a><span data-ttu-id="72dc4-170">Trouvez le compte de stockage par défaut</span><span class="sxs-lookup"><span data-stu-id="72dc4-170">Find the default storage account</span></span>
<span data-ttu-id="72dc4-171">Le script Powershell suivant montre comment obtenir le nom de compte de stockage par défaut et la clé de compte de stockage par défaut pour un cluster.</span><span class="sxs-lookup"><span data-stu-id="72dc4-171">The following Powershell script demonstrates how to get the default storage account name and the default storage account key for a cluster.</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup
    $defaultStorageAccountName = ($cluster.DefaultStorageAccount).Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $cluster.DefaultStorageContainer
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey

## <a name="find-the-resource-group"></a><span data-ttu-id="72dc4-172">Trouvez le groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="72dc4-172">Find the resource group</span></span>
<span data-ttu-id="72dc4-173">En mode Resource Manager, chaque cluster HDInsight appartient à un groupe de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="72dc4-173">In the Resource Manager mode, each HDInsight cluster belongs to an Azure resource group.</span></span>  <span data-ttu-id="72dc4-174">Pour rechercher le groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="72dc4-174">To find the resource group:</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup


## <a name="submit-jobs"></a><span data-ttu-id="72dc4-175">Soumettre les travaux</span><span class="sxs-lookup"><span data-stu-id="72dc4-175">Submit jobs</span></span>
<span data-ttu-id="72dc4-176">**Pour envoyer des tâches MapReduce**</span><span class="sxs-lookup"><span data-stu-id="72dc4-176">**To submit MapReduce jobs**</span></span>

<span data-ttu-id="72dc4-177">Consultez [Exécution des exemples Hadoop MapReduce dans HDInsight basé sur Windows](hdinsight-run-samples.md)</span><span class="sxs-lookup"><span data-stu-id="72dc4-177">See [Run Hadoop MapReduce samples in Windows-based HDInsight](hdinsight-run-samples.md).</span></span>

<span data-ttu-id="72dc4-178">**Pour envoyer des tâches Hive**</span><span class="sxs-lookup"><span data-stu-id="72dc4-178">**To submit Hive jobs**</span></span>

<span data-ttu-id="72dc4-179">Consultez [Exécution de requêtes Hive avec PowerShell](hdinsight-hadoop-use-hive-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="72dc4-179">See [Run Hive queries using PowerShell](hdinsight-hadoop-use-hive-powershell.md).</span></span>

<span data-ttu-id="72dc4-180">**Pour envoyer des tâches Pig**</span><span class="sxs-lookup"><span data-stu-id="72dc4-180">**To submit Pig jobs**</span></span>

<span data-ttu-id="72dc4-181">Consultez [Exécution de tâches Pig avec PowerShell](hdinsight-hadoop-use-pig-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="72dc4-181">See [Run Pig jobs using PowerShell](hdinsight-hadoop-use-pig-powershell.md).</span></span>

<span data-ttu-id="72dc4-182">**Pour envoyer des tâches Sqoop**</span><span class="sxs-lookup"><span data-stu-id="72dc4-182">**To submit Sqoop jobs**</span></span>

<span data-ttu-id="72dc4-183">Consultez l'article [Utilisation de Sqoop avec HDInsight](hdinsight-use-sqoop.md).</span><span class="sxs-lookup"><span data-stu-id="72dc4-183">See [Use Sqoop with HDInsight](hdinsight-use-sqoop.md).</span></span>

<span data-ttu-id="72dc4-184">**Pour envoyer des tâches Oozie**</span><span class="sxs-lookup"><span data-stu-id="72dc4-184">**To submit Oozie jobs**</span></span>

<span data-ttu-id="72dc4-185">Consultez [Utilisation d’Oozie avec Hadoop pour définir et exécuter un workflow dans HDInsight](hdinsight-use-oozie.md).</span><span class="sxs-lookup"><span data-stu-id="72dc4-185">See [Use Oozie with Hadoop to define and run a workflow in HDInsight](hdinsight-use-oozie.md).</span></span>

## <a name="upload-data-to-azure-blob-storage"></a><span data-ttu-id="72dc4-186">Téléchargement de données vers le stockage d'objets blob Azure</span><span class="sxs-lookup"><span data-stu-id="72dc4-186">Upload data to Azure Blob storage</span></span>
<span data-ttu-id="72dc4-187">Consultez la rubrique [Téléchargement de données vers HDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="72dc4-187">See [Upload data to HDInsight][hdinsight-upload-data].</span></span>

## <a name="see-also"></a><span data-ttu-id="72dc4-188">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="72dc4-188">See Also</span></span>
* <span data-ttu-id="72dc4-189">[Documentation de référence des applets de commande HDInsight][hdinsight-powershell-reference]</span><span class="sxs-lookup"><span data-stu-id="72dc4-189">[HDInsight cmdlet reference documentation][hdinsight-powershell-reference]</span></span>
* <span data-ttu-id="72dc4-190">[Administration de HDInsight à l’aide du portail Azure][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="72dc4-190">[Administer HDInsight by using the Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="72dc4-191">[Administration de HDInsight à l’aide de l’interface de ligne de commande][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="72dc4-191">[Administer HDInsight using a command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="72dc4-192">[Création de clusters HDInsight][hdinsight-provision]</span><span class="sxs-lookup"><span data-stu-id="72dc4-192">[Create HDInsight clusters][hdinsight-provision]</span></span>
* <span data-ttu-id="72dc4-193">[Téléchargement de données vers HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="72dc4-193">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="72dc4-194">[Envoi de tâches Hadoop par programme][hdinsight-submit-jobs]</span><span class="sxs-lookup"><span data-stu-id="72dc4-194">[Submit Hadoop jobs programmatically][hdinsight-submit-jobs]</span></span>
* <span data-ttu-id="72dc4-195">[Prise en main d’Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="72dc4-195">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>

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
