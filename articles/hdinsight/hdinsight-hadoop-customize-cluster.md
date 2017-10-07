---
title: "à l’aide de Clusters HDInsight aaaCustomize script actions - Azure | Documents Microsoft"
description: "Découvrez comment toocustomize HDInsight clusters à l’aide d’Action de Script."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 3a63e216-4163-40c1-aa04-6b42fd0162ad
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 076fff23e016db47bc7e9963582a545ad638e691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-windows-based-hdinsight-clusters-using-script-action"></a><span data-ttu-id="0f7b6-103">Personnalisation de clusters HDInsight basés sur Windows à l'aide d'une action de script</span><span class="sxs-lookup"><span data-stu-id="0f7b6-103">Customize Windows-based HDInsight clusters using Script Action</span></span>
<span data-ttu-id="0f7b6-104">**Action de script** peut être utilisé tooinvoke [des scripts personnalisés](hdinsight-hadoop-script-actions.md) pendant le processus de création de cluster hello pour l’installation des logiciels supplémentaires sur un cluster.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-104">**Script Action** can be used tooinvoke [custom scripts](hdinsight-hadoop-script-actions.md) during hello cluster creation process for installing additional software on a cluster.</span></span>

<span data-ttu-id="0f7b6-105">informations de Hello dans cet article sont des clusters HDInsight tooWindows spécifiques.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-105">hello information in this article is specific tooWindows-based HDInsight clusters.</span></span> <span data-ttu-id="0f7b6-106">Pour les clusters Linux, consultez la page [Personnaliser des clusters HDInsight Linux à l’aide d’une action de script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="0f7b6-106">For Linux-based clusters, see [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0f7b6-107">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="0f7b6-108">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="0f7b6-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="0f7b6-109">Clusters HDInsight peuvent être personnalisés de plusieurs autres façons, notamment d’autres comptes de stockage Azure, la modification hello Hadoop (core-site.XML, hive-site.XML, etc.) des fichiers de configuration ou ajout de bibliothèques (par exemple, Hive, Oozie) partagées dans emplacements courants dans un cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-109">HDInsight clusters can be customized in a variety of other ways as well, such as including additional Azure Storage accounts, changing hello Hadoop configuration files (core-site.xml, hive-site.xml, etc.), or adding shared libraries (e.g., Hive, Oozie) into common locations in hello cluster.</span></span> <span data-ttu-id="0f7b6-110">Ces personnalisations peuvent être effectuées dans Azure PowerShell, hello Azure HDInsight .NET SDK, ou hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-110">These customizations can be done through Azure PowerShell, hello Azure HDInsight .NET SDK, or hello Azure portal.</span></span> <span data-ttu-id="0f7b6-111">Pour plus d’informations, consultez [Création de clusters Hadoop dans HDInsight][hdinsight-provision-cluster].</span><span class="sxs-lookup"><span data-stu-id="0f7b6-111">For more information, see [Create Hadoop clusters in HDInsight][hdinsight-provision-cluster].</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell-cli-and-dotnet-sdk.md)]

## <a name="script-action-in-hello-cluster-creation-process"></a><span data-ttu-id="0f7b6-112">Action de script dans le processus de création de cluster hello</span><span class="sxs-lookup"><span data-stu-id="0f7b6-112">Script Action in hello cluster creation process</span></span>
<span data-ttu-id="0f7b6-113">Action de script est utilisée uniquement lorsqu’un cluster est en processus hello d’en cours de création.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-113">Script Action is only used while a cluster is in hello process of being created.</span></span> <span data-ttu-id="0f7b6-114">Hello diagramme ci-dessous illustre lors de l’Action de Script est exécutée pendant le processus de création de hello :</span><span class="sxs-lookup"><span data-stu-id="0f7b6-114">hello following diagram illustrates when Script Action is executed during hello creation process:</span></span>

<span data-ttu-id="0f7b6-115">![Personnalisation du cluster HDInsight et procédure de création d’un cluster][img-hdi-cluster-states]</span><span class="sxs-lookup"><span data-stu-id="0f7b6-115">![HDInsight cluster customization and stages during cluster creation][img-hdi-cluster-states]</span></span>

<span data-ttu-id="0f7b6-116">Lors de l’exécution du script hello, cluster de hello passe hello **ClusterCustomization** étape.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-116">When hello script is running, hello cluster enters hello **ClusterCustomization** stage.</span></span> <span data-ttu-id="0f7b6-117">À ce stade, hello script est exécuté sous un compte d’administrateur système hello, en parallèle sur tous les hello spécifié des nœuds de cluster de hello et fournit des privilèges d’administrateur complets sur les nœuds hello.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-117">At this stage, hello script is run under hello system admin account, in parallel on all hello specified nodes in hello cluster, and provides full admin privileges on hello nodes.</span></span>

> [!NOTE]
> <span data-ttu-id="0f7b6-118">Étant donné que vous disposez des privilèges d’administrateur sur les nœuds de cluster hello lors de la **ClusterCustomization** étape, vous pouvez utiliser hello script tooperform des opérations telles que l’arrêt et démarrage des services, y compris les services liés à Hadoop.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-118">Because you have admin privileges on hello cluster nodes during the **ClusterCustomization** stage, you can use hello script tooperform operations like stopping and starting services, including Hadoop-related services.</span></span> <span data-ttu-id="0f7b6-119">Ainsi, dans le cadre du script de hello, vous devez vous assurer que hello Ambari services et autres services Hadoop sont en cours d’exécution avant la fin de script de hello en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-119">So, as part of hello script, you must ensure that hello Ambari services and other Hadoop-related services are up and running before hello script finishes running.</span></span> <span data-ttu-id="0f7b6-120">Ces services sont requis toosuccessfully vérifier l’intégrité de hello et l’état du cluster de hello lors de sa création.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-120">These services are required toosuccessfully ascertain hello health and state of hello cluster while it is being created.</span></span> <span data-ttu-id="0f7b6-121">Si vous changez de configuration sur le cluster qui a une incidence sur ces services, vous devez utiliser les fonctions d’assistance hello fournis.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-121">If you change any configuration on the cluster that affects these services, you must use hello helper functions that are provided.</span></span> <span data-ttu-id="0f7b6-122">Pour plus d’informations sur les fonctions d’assistance, consultez [Développer des scripts d’action de script pour HDInsight][hdinsight-write-script].</span><span class="sxs-lookup"><span data-stu-id="0f7b6-122">For more information about helper functions, see [Develop Script Action scripts for HDInsight][hdinsight-write-script].</span></span>
>
>

<span data-ttu-id="0f7b6-123">sortie de Hello et journaux d’erreurs hello pour le script de hello sont stockés dans le compte de stockage par défaut hello que vous avez spécifié pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-123">hello output and hello error logs for hello script are stored in hello default Storage account you specified for hello cluster.</span></span> <span data-ttu-id="0f7b6-124">Hello journaux sont stockés dans une table avec le nom de hello **u < \cluster-name-fragment >< \time-stamp > setuplog**.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-124">hello logs are stored in a table with hello name **u<\cluster-name-fragment><\time-stamp>setuplog**.</span></span> <span data-ttu-id="0f7b6-125">Il s’agit de journaux d’agrégation à partir du script hello s’exécutent sur tous les nœuds hello (nœud principal et nœuds de travail) dans le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-125">These are aggregate logs from hello script run on all hello nodes (head node and worker nodes) in hello cluster.</span></span>

<span data-ttu-id="0f7b6-126">Chaque cluster peut accepter plusieurs actions de script qui sont appelées dans l’ordre de hello dans lequel elles sont spécifiées.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-126">Each cluster can accept multiple script actions that are invoked in hello order in which they are specified.</span></span> <span data-ttu-id="0f7b6-127">Un script peut être exécuté sur le nœud principal de hello, nœuds de travail hello ou les deux.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-127">A script can be ran on hello head node, hello worker nodes, or both.</span></span>

<span data-ttu-id="0f7b6-128">HDInsight fournit plusieurs hello tooinstall de scripts suivant des composants de clusters HDInsight :</span><span class="sxs-lookup"><span data-stu-id="0f7b6-128">HDInsight provides several scripts tooinstall hello following components on HDInsight clusters:</span></span>

| <span data-ttu-id="0f7b6-129">Nom</span><span class="sxs-lookup"><span data-stu-id="0f7b6-129">Name</span></span> | <span data-ttu-id="0f7b6-130">Script</span><span class="sxs-lookup"><span data-stu-id="0f7b6-130">Script</span></span> |
| --- | --- |
| <span data-ttu-id="0f7b6-131">**Installation de Spark**</span><span class="sxs-lookup"><span data-stu-id="0f7b6-131">**Install Spark**</span></span> |<span data-ttu-id="0f7b6-132">https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-132">https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1.</span></span> <span data-ttu-id="0f7b6-133">Consultez [Installer et utiliser Spark sur les clusters HDInsight][hdinsight-install-spark].</span><span class="sxs-lookup"><span data-stu-id="0f7b6-133">See [Install and use Spark on HDInsight clusters][hdinsight-install-spark].</span></span> |
| <span data-ttu-id="0f7b6-134">**Installation de R**</span><span class="sxs-lookup"><span data-stu-id="0f7b6-134">**Install R**</span></span> |<span data-ttu-id="0f7b6-135">https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-135">https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1.</span></span> <span data-ttu-id="0f7b6-136">Consultez [Installer et utiliser R sur les clusters HDInsight][hdinsight-install-r].</span><span class="sxs-lookup"><span data-stu-id="0f7b6-136">See [Install and use R on HDInsight clusters][hdinsight-install-r].</span></span> |
| <span data-ttu-id="0f7b6-137">**Installation de Solr**</span><span class="sxs-lookup"><span data-stu-id="0f7b6-137">**Install Solr**</span></span> |<span data-ttu-id="0f7b6-138">https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-138">https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1.</span></span> <span data-ttu-id="0f7b6-139">Consultez [Installer et utiliser Solr sur les clusters HDInsight](hdinsight-hadoop-solr-install.md).</span><span class="sxs-lookup"><span data-stu-id="0f7b6-139">See [Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span> |
| <span data-ttu-id="0f7b6-140">- **Installation de Giraph**</span><span class="sxs-lookup"><span data-stu-id="0f7b6-140">- **Install Giraph**</span></span> |<span data-ttu-id="0f7b6-141">https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-141">https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1.</span></span> <span data-ttu-id="0f7b6-142">Consultez [Installer et utiliser Giraph sur les clusters HDInsight](hdinsight-hadoop-giraph-install.md).</span><span class="sxs-lookup"><span data-stu-id="0f7b6-142">See [Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span> |
| <span data-ttu-id="0f7b6-143">**Précharger les bibliothèques Hive**</span><span class="sxs-lookup"><span data-stu-id="0f7b6-143">**Pre-load Hive libraries**</span></span> |<span data-ttu-id="0f7b6-144">https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-144">https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1.</span></span> <span data-ttu-id="0f7b6-145">Consultez [Ajouter des bibliothèques Hive sur des clusters HDInsight](hdinsight-hadoop-add-hive-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="0f7b6-145">See [Add Hive libraries on HDInsight clusters](hdinsight-hadoop-add-hive-libraries.md)</span></span> |

## <a name="call-scripts-using-hello-azure-portal"></a><span data-ttu-id="0f7b6-146">Appeler des scripts à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="0f7b6-146">Call scripts using hello Azure portal</span></span>
<span data-ttu-id="0f7b6-147">**À partir de hello portail Azure**</span><span class="sxs-lookup"><span data-stu-id="0f7b6-147">**From hello Azure portal**</span></span>

1. <span data-ttu-id="0f7b6-148">Démarrez la création d'un cluster comme décrit dans [Création de clusters Hadoop dans HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="0f7b6-148">Start creating a cluster as described at [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
2. <span data-ttu-id="0f7b6-149">Sous Configuration facultative, pourquoi **Actions de Script** panneau, cliquez sur **ajouter une action de script** tooprovide des détails sur l’action de script hello, comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="0f7b6-149">Under Optional Configuration, for hello **Script Actions** blade, click **add script action** tooprovide details about hello script action, as shown below:</span></span>

    <span data-ttu-id="0f7b6-150">![Utilisez l’Action de Script toocustomize un cluster](./media/hdinsight-hadoop-customize-cluster/HDI.CreateCluster.8.png "toocustomize d’Action de Script d’utiliser un cluster")</span><span class="sxs-lookup"><span data-stu-id="0f7b6-150">![Use Script Action toocustomize a cluster](./media/hdinsight-hadoop-customize-cluster/HDI.CreateCluster.8.png "Use Script Action toocustomize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="0f7b6-151">Propriété</span><span class="sxs-lookup"><span data-stu-id="0f7b6-151">Property</span></span></th><th><span data-ttu-id="0f7b6-152">Valeur</span><span class="sxs-lookup"><span data-stu-id="0f7b6-152">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="0f7b6-153">Nom</span><span class="sxs-lookup"><span data-stu-id="0f7b6-153">Name</span></span></td>
            <td><span data-ttu-id="0f7b6-154">Spécifiez un nom pour l’action de script hello.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-154">Specify a name for hello script action.</span></span></td></tr>
        <tr><td><span data-ttu-id="0f7b6-155">URI du script</span><span class="sxs-lookup"><span data-stu-id="0f7b6-155">Script URI</span></span></td>
            <td><span data-ttu-id="0f7b6-156">Spécifiez hello URI toohello script qui est appelée toocustomize hello cluster.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-156">Specify hello URI toohello script that is invoked toocustomize hello cluster.</span></span> <span data-ttu-id="0f7b6-157">s</span><span class="sxs-lookup"><span data-stu-id="0f7b6-157">s</span></span></td></tr>
        <tr><td><span data-ttu-id="0f7b6-158">Head/Worker</span><span class="sxs-lookup"><span data-stu-id="0f7b6-158">Head/Worker</span></span></td>
            <td><span data-ttu-id="0f7b6-159">Spécifier les nœuds hello (**Head** ou **travail**) sur la personnalisation hello script est exécuté.</b>.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-159">Specify hello nodes (**Head** or **Worker**) on which hello customization script is run.</b>.</span></span>
        <tr><td><span data-ttu-id="0f7b6-160">Paramètres</span><span class="sxs-lookup"><span data-stu-id="0f7b6-160">Parameters</span></span></td>
            <td><span data-ttu-id="0f7b6-161">Spécifiez des paramètres de hello, si requis par le script de hello.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-161">Specify hello parameters, if required by hello script.</span></span></td></tr>
    </table>

    <span data-ttu-id="0f7b6-162">Appuyez sur entrée tooadd plus de script action tooinstall plusieurs composants de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-162">Press ENTER tooadd more than one script action tooinstall multiple components on hello cluster.</span></span>
3. <span data-ttu-id="0f7b6-163">Cliquez sur **sélectionnez** toosave hello configuration des actions de script et poursuivre la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-163">Click **Select** toosave hello script action configuration and continue with cluster creation.</span></span>

## <a name="call-scripts-using-azure-powershell"></a><span data-ttu-id="0f7b6-164">Appel de scripts à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0f7b6-164">Call scripts using Azure PowerShell</span></span>
<span data-ttu-id="0f7b6-165">Ce script PowerShell suivant montre comment tooinstall Spark sur Windows en fonction de cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-165">This following PowerShell script demonstrates how tooinstall Spark on Windows based HDInsight cluster.</span></span>  

    # Provide values for these variables
    $subscriptionID = "<Azure Suscription ID>" # After "Login-AzureRmAccount", use "Get-AzureRmSubscription" toolist IDs.

    $nameToken = "<Enter A Name Token>"  # hello token is use toocreate Azure service names.
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $location = "EAST US 2" # used for creating resource group, storage account, and HDInsight cluster.

    $hdinsightClusterName = $namePrefix + "spark"
    $httpUserName = "admin"
    $httpPassword = "<Enter a Password>"

    $defaultStorageAccountName = "$namePrefix" + "store"
    $defaultBlobContainerName = $hdinsightClusterName

    #############################################################
    # Connect tooAzure
    #############################################################

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }
    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #############################################################
    # Prepare hello dependent components
    #############################################################

    # Create resource group
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_GRS
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                    -StorageAccountName $defaultStorageAccountName `
                                    -StorageAccountKey $storageAccountKey  
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext

    #############################################################
    # Create cluster with ApacheSpark
    #############################################################

    # Specify hello configuration options
    $config = New-AzureRmHDInsightClusterConfig `
                -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
                -DefaultStorageAccountKey $defaultStorageAccountKey


    # Add a script action toohello cluster configuration
    $config = Add-AzureRmHDInsightScriptAction `
                -Config $config `
                -Name "Install Spark" `
                -NodeType HeadNode `
                -Uri https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1 `

    # Start creating a cluster with Spark installed
    New-AzureRmHDInsightCluster `
            -ResourceGroupName $resourceGroupName `
            -ClusterName $hdinsightClusterName `
            -Location $location `
            -ClusterSizeInNodes 2 `
            -ClusterType Hadoop `
            -OSType Windows `
            -DefaultStorageContainer $defaultBlobContainerName `
            -Config $config


<span data-ttu-id="0f7b6-166">tooinstall autres logiciels, vous devez tooreplace fichier de script hello dans le script de hello :</span><span class="sxs-lookup"><span data-stu-id="0f7b6-166">tooinstall other software, you will need tooreplace hello script file in hello script:</span></span>

<span data-ttu-id="0f7b6-167">Lorsque vous y êtes invité, entrez les informations d’identification de l’hello pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-167">When prompted, enter hello credentials for hello cluster.</span></span> <span data-ttu-id="0f7b6-168">Il peut prendre plusieurs minutes avant que le cluster de hello est créé.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-168">It can take several minutes before hello cluster is created.</span></span>

## <a name="call-scripts-using-net-sdk"></a><span data-ttu-id="0f7b6-169">Appel de scripts à l'aide du Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="0f7b6-169">Call scripts using .NET SDK</span></span>
<span data-ttu-id="0f7b6-170">Hello exemple suivant montre comment tooinstall Spark sur Windows en fonction de cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-170">hello following sample demonstrates how tooinstall Spark on Windows based HDInsight cluster.</span></span> <span data-ttu-id="0f7b6-171">tooinstall autres logiciels, vous devez tooreplace fichier de script hello dans le code hello.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-171">tooinstall other software, you will need tooreplace hello script file in hello code.</span></span>

<span data-ttu-id="0f7b6-172">**toocreate un cluster HDInsight avec Spark**</span><span class="sxs-lookup"><span data-stu-id="0f7b6-172">**toocreate an HDInsight cluster with Spark**</span></span>

1. <span data-ttu-id="0f7b6-173">Créez une application console C# dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-173">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="0f7b6-174">À partir de la Console du Gestionnaire de Package Nuget de hello, exécutez hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-174">From hello Nuget Package Manager Console, run hello following command.</span></span>

        Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
        Install-Package Microsoft.Azure.Management.ResourceManager -Pre
        Install-Package Microsoft.Azure.Management.HDInsight
3. <span data-ttu-id="0f7b6-175">Hello utilisation suivant à l’aide des instructions dans le fichier Program.cs de hello :</span><span class="sxs-lookup"><span data-stu-id="0f7b6-175">Use hello following using statements in hello Program.cs file:</span></span>

        using System;
        using System.Security;
        using Microsoft.Azure;
        using Microsoft.Azure.Management.HDInsight;
        using Microsoft.Azure.Management.HDInsight.Models;
        using Microsoft.Azure.Management.ResourceManager;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest;
        using Microsoft.Rest.Azure.Authentication;
4. <span data-ttu-id="0f7b6-176">Placez le code de hello dans la classe hello avec les éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="0f7b6-176">Place hello code in hello class with hello following:</span></span>

        private static HDInsightManagementClient _hdiManagementClient;

        // Replace with your AAD tenant ID if necessary
        private const string TenantId = UserTokenProvider.CommonTenantId;
        private const string SubscriptionId = "<Your Azure Subscription ID>";
        // This is hello GUID for hello PowerShell client. Used for interactive logins in this example.
        private const string ClientId = "1950a258-227b-4e31-a9cf-717495945fc2";
        private const string ResourceGroupName = "<ExistingAzureResourceGroupName>";
        private const string NewClusterName = "<NewAzureHDInsightClusterName>";
        private const int NewClusterNumWorkerNodes = 2;
        private const string NewClusterLocation = "East US";
        private const string NewClusterVersion = "3.2";
        private const string ExistingStorageName = "<ExistingAzureStorageAccountName>";
        private const string ExistingStorageKey = "<ExistingAzureStorageAccountKey>";
        private const string ExistingContainer = "<ExistingAzureBlobStorageContainer>";
        private const string NewClusterType = "Hadoop";
        private const OSType NewClusterOSType = OSType.Windows;
        private const string NewClusterUsername = "<HttpUserName>";
        private const string NewClusterPassword = "<HttpUserPassword>";

        static void Main(string[] args)
        {
            System.Console.WriteLine("Running");

            // Authenticate and get a token
            var authToken = Authenticate(TenantId, ClientId, SubscriptionId);
            // Flag subscription for HDInsight, if it isn't already.
            EnableHDInsight(authToken);
            // Get an HDInsight management client
            _hdiManagementClient = new HDInsightManagementClient(authToken);

            CreateCluster();
        }

        private static void CreateCluster()
        {
            var parameters = new ClusterCreateParameters
            {
                ClusterSizeInNodes = NewClusterNumWorkerNodes,
                Location = NewClusterLocation,
                ClusterType = NewClusterType,
                OSType = NewClusterOSType,
                Version = NewClusterVersion,
                DefaultStorageInfo = new AzureStorageInfo(ExistingStorageName, ExistingStorageKey, ExistingContainer),
                UserName = NewClusterUsername,
                Password = NewClusterPassword,
            };

            ScriptAction sparkScriptAction = new ScriptAction("Install Spark",
                new Uri("https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1"), "");

            parameters.ScriptActions.Add(ClusterNodeType.HeadNode, new System.Collections.Generic.List<ScriptAction> { sparkScriptAction });
            parameters.ScriptActions.Add(ClusterNodeType.WorkerNode, new System.Collections.Generic.List<ScriptAction> { sparkScriptAction });

            _hdiManagementClient.Clusters.Create(ResourceGroupName, NewClusterName, parameters);
        }

        /// <summary>
        /// Authenticate tooan Azure subscription and retrieve an authentication token
        /// </summary>
        /// <param name="TenantId">hello AAD tenant ID</param>
        /// <param name="ClientId">hello AAD client ID</param>
        /// <param name="SubscriptionId">hello Azure subscription ID</param>
        /// <returns></returns>
        static TokenCloudCredentials Authenticate(string TenantId, string ClientId, string SubscriptionId)
        {
            var authContext = new AuthenticationContext("https://login.microsoftonline.com/" + TenantId);
            var tokenAuthResult = authContext.AcquireToken("https://management.core.windows.net/",
                ClientId,
                new Uri("urn:ietf:wg:oauth:2.0:oob"),
                PromptBehavior.Always,
                UserIdentifier.AnyUser);
            return new TokenCloudCredentials(SubscriptionId, tokenAuthResult.AccessToken);
        }
        /// <summary>
        /// Marks your subscription as one that can use HDInsight, if it has not already been marked as such.
        /// </summary>
        /// <remarks>This is essentially a one-time action; if you have already done something with HDInsight
        /// on your subscription, then this isn't needed at all and will do nothing.</remarks>
        /// <param name="authToken">An authentication token for your Azure subscription</param>
        static void EnableHDInsight(TokenCloudCredentials authToken)
        {
            // Create a client for hello Resource manager and set hello subscription ID
            var resourceManagementClient = new ResourceManagementClient(new TokenCredentials(authToken.Token));
            resourceManagementClient.SubscriptionId = SubscriptionId;
            // Register hello HDInsight provider
            var rpResult = resourceManagementClient.Providers.Register("Microsoft.HDInsight");
        }
5. <span data-ttu-id="0f7b6-177">Appuyez sur **F5** application hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-177">Press **F5** toorun hello application.</span></span>

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a><span data-ttu-id="0f7b6-178">Prise en charge des logiciels open source utilisés sur les clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="0f7b6-178">Support for open-source software used on HDInsight clusters</span></span>
<span data-ttu-id="0f7b6-179">Hello service Microsoft Azure HDInsight est une plate-forme flexible qui vous permet de toobuild des applications de données volumineuses dans le cloud de hello à l’aide d’un écosystème de technologies open source sur Hadoop.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-179">hello Microsoft Azure HDInsight service is a flexible platform that enables you toobuild big-data applications in hello cloud by using an ecosystem of open-source technologies formed around Hadoop.</span></span> <span data-ttu-id="0f7b6-180">Microsoft Azure offre un niveau général de la prise en charge pour les technologies open source, comme indiqué dans hello **prennent en charge l’étendue** section Hello <a href="http://azure.microsoft.com/support/faq/" target="_blank">site Web du Forum aux questions sur Azure prend en charge</a>.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-180">Microsoft Azure provides a general level of support for open-source technologies, as discussed in hello **Support Scope** section of hello <a href="http://azure.microsoft.com/support/faq/" target="_blank">Azure Support FAQ website</a>.</span></span> <span data-ttu-id="0f7b6-181">Hello service HDInsight fournit un niveau supplémentaire de prise en charge de certains composants de hello, comme décrit ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-181">hello HDInsight service provides an additional level of support for some of hello components, as described below.</span></span>

<span data-ttu-id="0f7b6-182">Il existe deux types de composants open source qui sont disponibles dans hello service HDInsight :</span><span class="sxs-lookup"><span data-stu-id="0f7b6-182">There are two types of open-source components that are available in hello HDInsight service:</span></span>

* <span data-ttu-id="0f7b6-183">**Les composants intégrés** -ces composants sont déjà installés sur les clusters HDInsight et fournir des fonctionnalités principales du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-183">**Built-in components** - These components are pre-installed on HDInsight clusters and provide core functionality of hello cluster.</span></span> <span data-ttu-id="0f7b6-184">Par exemple, fils ResourceManager, langage de requête Hive hello (HiveQL) et la bibliothèque de Mahout hello appartiennent toothis catégorie.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-184">For example, YARN ResourceManager, hello Hive query language (HiveQL), and hello Mahout library belong toothis category.</span></span> <span data-ttu-id="0f7b6-185">Une liste complète des composants de cluster est disponible dans [quelles sont les nouveautés dans les versions de cluster Hadoop hello fournies par HDInsight ?](hdinsight-component-versioning.md) </a>.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-185">A full list of cluster components is available in [What's new in hello Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md)</a>.</span></span>
* <span data-ttu-id="0f7b6-186">**Les composants personnalisés** -vous, en tant qu’utilisateur de cluster de hello, pourrez installer ou utiliser dans votre charge de travail n’importe quel composant disponible dans la Communauté de hello ou créée par vous.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-186">**Custom components** - You, as a user of hello cluster, can install or use in your workload any component available in hello community or created by you.</span></span>

<span data-ttu-id="0f7b6-187">Charge entièrement les composants intégrés, et permet de tooisolate et résoudre les problèmes connexes toothese composants de Support technique de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-187">Built-in components are fully supported, and Microsoft Support will help tooisolate and resolve issues related toothese components.</span></span>

> [!WARNING]
> <span data-ttu-id="0f7b6-188">Les composants fournis avec le cluster HDInsight de hello sont entièrement gérés et permet de tooisolate et résoudre les problèmes connexes toothese composants de Support technique de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-188">Components provided with hello HDInsight cluster are fully supported and Microsoft Support will help tooisolate and resolve issues related toothese components.</span></span>
>
> <span data-ttu-id="0f7b6-189">Les composants personnalisés de réception efforcera toohelp vous toofurther hello de dépannage.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-189">Custom components receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="0f7b6-190">Cela peut entraîner hello de résoudre ou demandant que vous tooengage les canaux disponibles pour hello ouvrir technologies source où se trouve une grande expérience pour cette technologie.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-190">This might result in resolving hello issue OR asking you tooengage available channels for hello open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="0f7b6-191">Vous pouvez, par exemple, utiliser de nombreux sites de communauté, comme le [forum MSDN sur HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). En outre, les projets Apache ont des sites de projet sur [http://apache.org](http://apache.org) ; par exemple, [Hadoop](http://hadoop.apache.org/) ou [Spark](http://spark.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="0f7b6-191">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/), [Spark](http://spark.apache.org/).</span></span>
>
>

<span data-ttu-id="0f7b6-192">Hello service HDInsight propose plusieurs manières toouse des composants personnalisés.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-192">hello HDInsight service provides several ways toouse custom components.</span></span> <span data-ttu-id="0f7b6-193">Quelle que soit la comment un composant est utilisé ou installé sur le cluster de hello, hello même niveau de prise en charge s’applique.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-193">Regardless of how a component is used or installed on hello cluster, hello same level of support applies.</span></span> <span data-ttu-id="0f7b6-194">Voici une liste des méthodes les plus courantes de hello que les composants personnalisés peuvent être utilisés sur les clusters HDInsight :</span><span class="sxs-lookup"><span data-stu-id="0f7b6-194">Below is a list of hello most common ways that custom components can be used on HDInsight clusters:</span></span>

1. <span data-ttu-id="0f7b6-195">Envoi de travaux - Hadoop ou autres types de tâches qui s’exécutent, ou utilisent des composants personnalisés peut être soumis toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-195">Job submission - Hadoop or other types of jobs that execute or use custom components can be submitted toohello cluster.</span></span>
2. <span data-ttu-id="0f7b6-196">Personnalisation de cluster - lors de la création du cluster, vous pouvez spécifier des paramètres supplémentaires et des composants personnalisés qui seront installés sur les nœuds de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-196">Cluster customization - During cluster creation, you can specify additional settings and custom components that will be installed on hello cluster nodes.</span></span>
3. <span data-ttu-id="0f7b6-197">Exemples - pour les composants personnalisés populaires, Microsoft et d’autres peuvent fournir des exemples de la façon dont ces composants peuvent être utilisés sur des clusters HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-197">Samples - For popular custom components, Microsoft and others may provide samples of how these components can be used on hello HDInsight clusters.</span></span> <span data-ttu-id="0f7b6-198">Ces exemples sont fournis sans support.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-198">These samples are provided without support.</span></span>

## <a name="develop-script-action-scripts"></a><span data-ttu-id="0f7b6-199">Développer des scripts d’action de script</span><span class="sxs-lookup"><span data-stu-id="0f7b6-199">Develop Script Action scripts</span></span>
<span data-ttu-id="0f7b6-200">Consultez [Développer des scripts d’action de script pour HDInsight][hdinsight-write-script].</span><span class="sxs-lookup"><span data-stu-id="0f7b6-200">See [Develop Script Action scripts for HDInsight][hdinsight-write-script].</span></span>

## <a name="see-also"></a><span data-ttu-id="0f7b6-201">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="0f7b6-201">See also</span></span>
* <span data-ttu-id="0f7b6-202">[Créer des clusters Hadoop dans HDInsight] [ hdinsight-provision-cluster] fournit des instructions sur la façon dont toocreate un HDInsight de cluster à l’aide d’autres options personnalisées.</span><span class="sxs-lookup"><span data-stu-id="0f7b6-202">[Create Hadoop clusters in HDInsight][hdinsight-provision-cluster] provides instructions on how toocreate an HDInsight cluster by using other custom options.</span></span>
* <span data-ttu-id="0f7b6-203">[Développer des scripts d’action de script pour HDInsight][hdinsight-write-script]</span><span class="sxs-lookup"><span data-stu-id="0f7b6-203">[Develop Script Action scripts for HDInsight][hdinsight-write-script]</span></span>
* <span data-ttu-id="0f7b6-204">[Installer et utiliser Spark sur les clusters HDInsight][hdinsight-install-spark]</span><span class="sxs-lookup"><span data-stu-id="0f7b6-204">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]</span></span>
* <span data-ttu-id="0f7b6-205">[Installer et utiliser R sur les clusters HDInsight][hdinsight-install-r]</span><span class="sxs-lookup"><span data-stu-id="0f7b6-205">[Install and use R on HDInsight clusters][hdinsight-install-r]</span></span>
* <span data-ttu-id="0f7b6-206">[Installer et utiliser Solr sur les clusters HDInsight](hdinsight-hadoop-solr-install.md)</span><span class="sxs-lookup"><span data-stu-id="0f7b6-206">[Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span>
* <span data-ttu-id="0f7b6-207">[Installez et utilisez Giraph sur les clusters HDInsight](hdinsight-hadoop-giraph-install.md).</span><span class="sxs-lookup"><span data-stu-id="0f7b6-207">[Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span>

[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-write-script]: hdinsight-hadoop-script-actions.md
[hdinsight-provision-cluster]: hdinsight-hadoop-provision-linux-clusters.md
[powershell-install-configure]: /powershell/azureps-cmdlets-docs


[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "Procédure de création d’un cluster"
