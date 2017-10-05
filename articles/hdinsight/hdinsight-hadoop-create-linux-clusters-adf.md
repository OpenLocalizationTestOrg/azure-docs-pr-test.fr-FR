---
title: "Créer des clusters Hadoop à la demande à l’aide de Data Factory - Azure HDInsight | Microsoft Docs"
description: "Découvrez comment créer des clusters Hadoop à la demande dans HDInsight avec Azure Data Factory."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: spelluru
manager: jhubbard
editor: cgronlun
ms.assetid: 1f3b3a78-4d16-4d99-ba6e-06f7bb185d6a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/20/2017
ms.author: spelluru
ms.openlocfilehash: e68f1d72965d9516e0552c84d03d234c21739390
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="create-on-demand-hadoop-clusters-in-hdinsight-using-azure-data-factory"></a><span data-ttu-id="7500e-103">Créer des clusters Hadoop à la demande dans HDInsight avec Azure Data Factor</span><span class="sxs-lookup"><span data-stu-id="7500e-103">Create on-demand Hadoop clusters in HDInsight using Azure Data Factory</span></span>
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="7500e-104">[Azure Data Factory](../data-factory/data-factory-introduction.md) est un service d’intégration de données cloud qui gère et automatise le déplacement et la transformation des données.</span><span class="sxs-lookup"><span data-stu-id="7500e-104">[Azure Data Factory](../data-factory/data-factory-introduction.md) is a cloud-based data integration service that orchestrates and automates the movement and transformation of data.</span></span> <span data-ttu-id="7500e-105">Il peut créer un cluster Hadoop HDInsight juste-à-temps pour traiter une tranche de données d’entrée et supprimer le cluster à l’issue du traitement.</span><span class="sxs-lookup"><span data-stu-id="7500e-105">It can create a HDInsight Hadoop cluster just-in-time to process an input data slice and delete the cluster when the processing is complete.</span></span> <span data-ttu-id="7500e-106">Voici quelques-uns des avantages liés à l’utilisation d’un cluster Hadoop HDInsight à la demande :</span><span class="sxs-lookup"><span data-stu-id="7500e-106">Some of the benefits of using an on-demand HDInsight Hadoop cluster are:</span></span>

- <span data-ttu-id="7500e-107">Vous payez uniquement pour le temps d’exécution du travail sur le cluster Hadoop HDInsight (ainsi que pour une brève durée d’inactivité configurable).</span><span class="sxs-lookup"><span data-stu-id="7500e-107">You only pay for the time job is running on the HDInsight Hadoop cluster (plus a brief configurable idle time).</span></span> <span data-ttu-id="7500e-108">La facturation des clusters HDInsight est calculée au prorata des minutes écoulées, que vous les utilisiez ou non.</span><span class="sxs-lookup"><span data-stu-id="7500e-108">The billing for HDInsight clusters is pro-rated per minute, whether you are using them or not.</span></span> <span data-ttu-id="7500e-109">Lorsque vous utilisez un service lié HDInsight à la demande dans Data Factory, les clusters sont créés à la demande.</span><span class="sxs-lookup"><span data-stu-id="7500e-109">When you use an on-demand HDInsight linked service in Data Factory, the clusters are created on-demand.</span></span> <span data-ttu-id="7500e-110">Et les clusters sont automatiquement supprimés lorsque les tâches sont terminées.</span><span class="sxs-lookup"><span data-stu-id="7500e-110">And the clusters are deleted automatically when the jobs are completed.</span></span> <span data-ttu-id="7500e-111">Par conséquent, vous ne payez que pour le temps d’exécution du travail et pour la courte durée d’inactivité (paramètre de durée de vie [TTL, Time to Live]).</span><span class="sxs-lookup"><span data-stu-id="7500e-111">Therefore, you only pay for the job running time and the brief idle time (time-to-live setting).</span></span>
- <span data-ttu-id="7500e-112">Vous pouvez créer un workflow à l’aide d’un pipeline Data Factory.</span><span class="sxs-lookup"><span data-stu-id="7500e-112">You can create a workflow using a Data Factory pipeline.</span></span> <span data-ttu-id="7500e-113">Par exemple, vous pouvez faire en sorte que le pipeline copie des données d’un serveur SQL Server local vers un stockage Blob Azure, puis qu’il traite ces données en exécutant un script Hive et un script Pig sur un cluster Hadoop HDInsight à la demande.</span><span class="sxs-lookup"><span data-stu-id="7500e-113">For example, you can have the pipeline to copy data from an on-premises SQL Server to an Azure blob storage, process the data by running a Hive script and a Pig script on an on-demand HDInsight Hadoop cluster.</span></span> <span data-ttu-id="7500e-114">Ensuite, copiez les données résultantes dans un entrepôt de données Azure SQL Data Warehouse pour que les applications décisionnelles puissent les consommer.</span><span class="sxs-lookup"><span data-stu-id="7500e-114">Then, copy the result data to an Azure SQL Data Warehouse for BI applications to consume.</span></span>
- <span data-ttu-id="7500e-115">Vous pouvez planifier une exécution périodique du workflow (horaire, quotidienne, hebdomadaire, mensuelle, etc.).</span><span class="sxs-lookup"><span data-stu-id="7500e-115">You can schedule the workflow to run periodically (hourly, daily, weekly, monthly, etc.).</span></span>

<span data-ttu-id="7500e-116">Dans Azure Data Factory, une fabrique de données peut comporter un ou plusieurs pipelines de données.</span><span class="sxs-lookup"><span data-stu-id="7500e-116">In Azure Data Factory, a data factory can have one or more data pipelines.</span></span> <span data-ttu-id="7500e-117">Un pipeline de données comprend une ou plusieurs activités.</span><span class="sxs-lookup"><span data-stu-id="7500e-117">A data pipeline has one or more activities.</span></span> <span data-ttu-id="7500e-118">Il existe deux types d’activités : les [activités de déplacement des données](../data-factory/data-factory-data-movement-activities.md) et les [activités de transformation des données](../data-factory/data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="7500e-118">There are two types of activities: [Data Movement Activities](../data-factory/data-factory-data-movement-activities.md) and [Data Transformation Activities](../data-factory/data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="7500e-119">Vous utilisez les activités de déplacement des données (pour l’instant, uniquement l’activité de copie) pour déplacer des données d’une banque de données source vers une banque de données de destination.</span><span class="sxs-lookup"><span data-stu-id="7500e-119">You use data movement activities (currently, only Copy Activity) to move data from a source data store to a destination data store.</span></span> <span data-ttu-id="7500e-120">Vous utilisez les activités de transformation des données pour transformer/traiter les données.</span><span class="sxs-lookup"><span data-stu-id="7500e-120">You use data transformation activities to transform/process data.</span></span> <span data-ttu-id="7500e-121">L’activité Hive HDInsight est l’une des activités de transformation prises en charge par Data Factory.</span><span class="sxs-lookup"><span data-stu-id="7500e-121">HDInsight Hive Activity is one of the transformation activities supported by Data Factory.</span></span> <span data-ttu-id="7500e-122">Dans ce didacticiel, vous utilisez l’activité de transformation Hive.</span><span class="sxs-lookup"><span data-stu-id="7500e-122">You use the Hive transformation activity in this tutorial.</span></span>

<span data-ttu-id="7500e-123">Vous pouvez configurer une activité Hive pour qu’elle utilise votre propre cluster Hadoop HDInsight ou un cluster Hadoop HDInsight à la demande.</span><span class="sxs-lookup"><span data-stu-id="7500e-123">You can configure a hive activity to use your own HDInsight Hadoop cluster or an on-demand HDInsight Hadoop cluster.</span></span> <span data-ttu-id="7500e-124">Dans ce didacticiel, l’activité Hive figurant dans le pipeline de fabrique de données est configurée pour utiliser un cluster HDInsight à la demande.</span><span class="sxs-lookup"><span data-stu-id="7500e-124">In this tutorial, the Hive activity in the data factory pipeline is configured to use an on-demand HDInsight cluster.</span></span> <span data-ttu-id="7500e-125">Par conséquent, lorsque l’activité s’exécute pour traiter une tranche de données, le déroulement des opérations est le suivant :</span><span class="sxs-lookup"><span data-stu-id="7500e-125">Therefore, when the activity runs to process a data slice, here is what happens:</span></span>

1. <span data-ttu-id="7500e-126">Un cluster Hadoop HDInsight est automatiquement créé juste-à-temps à votre intention pour traiter la tranche.</span><span class="sxs-lookup"><span data-stu-id="7500e-126">A HDInsight Hadoop cluster is automatically created for you just-in-time to process the slice.</span></span>  
2. <span data-ttu-id="7500e-127">Les données d’entrée sont traitées par l’exécution d’un script HiveQL sur le cluster.</span><span class="sxs-lookup"><span data-stu-id="7500e-127">The input data is processed by running a HiveQL script on the cluster.</span></span>
3. <span data-ttu-id="7500e-128">Le cluster Hadoop HDInsight est supprimé à l’issue du traitement et reste inactif pendant l’intervalle de temps configuré (paramètre timeToLive).</span><span class="sxs-lookup"><span data-stu-id="7500e-128">The HDInsight Hadoop cluster is deleted after the processing is complete and the cluster is idle for the configured amount of time (timeToLive setting).</span></span> <span data-ttu-id="7500e-129">Si la tranche de données suivante peut être traitée au cours de cette durée d’inactivité timeToLive, elle est traitée à l’aide du même cluster.</span><span class="sxs-lookup"><span data-stu-id="7500e-129">If the next data slice is available for processing with in this timeToLive idle time, the same cluster is used to process the slice.</span></span>  

<span data-ttu-id="7500e-130">Dans ce didacticiel, le script HiveQL associé à l’activité Hive effectue les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="7500e-130">In this tutorial, the HiveQL script associated with the hive activity performs the following actions:</span></span>

1. <span data-ttu-id="7500e-131">Il crée une table externe qui référence les données brutes de journal Web stockées dans un stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="7500e-131">Creates an external table that references the raw web log data stored in an Azure Blob storage.</span></span>
2. <span data-ttu-id="7500e-132">Il partitionne les données brutes par année et par mois.</span><span class="sxs-lookup"><span data-stu-id="7500e-132">Partitions the raw data by year and month.</span></span>
3. <span data-ttu-id="7500e-133">Il stocke les données partitionnées dans le stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="7500e-133">Stores the partitioned data in the Azure blob storage.</span></span>

<span data-ttu-id="7500e-134">Dans ce didacticiel, le script HiveQL associé à l’activité Hive crée une table externe qui référence les données brutes de journal Web stockées dans le stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="7500e-134">In this tutorial, the HiveQL script associated with the hive activity creates an external table that references the raw web log data stored in the Azure Blob Storage.</span></span> <span data-ttu-id="7500e-135">Voici les échantillons de lignes pour chaque mois du fichier d’entrée.</span><span class="sxs-lookup"><span data-stu-id="7500e-135">Here are the sample rows for each month in the input file.</span></span>

```
2014-01-01,02:01:09,SAMPLEWEBSITE,GET,/blogposts/mvc4/step2.png,X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,53175,871
2014-02-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
2014-03-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
```

<span data-ttu-id="7500e-136">Le script HiveQL partitionne les données brutes par année et par mois.</span><span class="sxs-lookup"><span data-stu-id="7500e-136">The HiveQL script partitions the raw data by year and month.</span></span> <span data-ttu-id="7500e-137">Il crée trois dossiers de sortie en fonction de l’entrée précédente.</span><span class="sxs-lookup"><span data-stu-id="7500e-137">It creates three output folders based on the previous input.</span></span> <span data-ttu-id="7500e-138">Chaque dossier contient un fichier avec les entrées correspondant à chaque mois.</span><span class="sxs-lookup"><span data-stu-id="7500e-138">Each folder contains a file with entries from each month.</span></span>

```
adfgetstarted/partitioneddata/year=2014/month=1/000000_0
adfgetstarted/partitioneddata/year=2014/month=2/000000_0
adfgetstarted/partitioneddata/year=2014/month=3/000000_0
```

<span data-ttu-id="7500e-139">Pour obtenir la liste des activités de transformation de données de Data Factory en plus de l’activité Hive, consultez [Transformation et analyse en utilisant Azure Data Factory](../data-factory/data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="7500e-139">For a list of Data Factory data transformation activities in addition to Hive activity, see [Transform and analyze using Azure Data Factory](../data-factory/data-factory-data-transformation-activities.md).</span></span>

> [!NOTE]
> <span data-ttu-id="7500e-140">Actuellement, vous ne pouvez créer qu’un cluster HDInsight version 3.2 à partir d’Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="7500e-140">Currently, you can only create HDInsight cluster version 3.2 from Azure Data Factory.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7500e-141">Composants requis</span><span class="sxs-lookup"><span data-stu-id="7500e-141">Prerequisites</span></span>
<span data-ttu-id="7500e-142">Avant de commencer à suivre les instructions de cet article, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="7500e-142">Before you begin the instructions in this article, you must have the following items:</span></span>

* <span data-ttu-id="7500e-143">[Abonnement Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="7500e-143">[Azure subscription](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="7500e-144">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7500e-144">Azure PowerShell.</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

### <a name="prepare-storage-account"></a><span data-ttu-id="7500e-145">Préparer le compte de stockage</span><span class="sxs-lookup"><span data-stu-id="7500e-145">Prepare storage account</span></span>
<span data-ttu-id="7500e-146">Vous pouvez utiliser jusqu’à trois comptes de stockage dans ce scénario :</span><span class="sxs-lookup"><span data-stu-id="7500e-146">You can use up to three storage accounts in this scenario:</span></span>

- <span data-ttu-id="7500e-147">le compte de stockage par défaut du cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="7500e-147">default storage account for the HDInsight cluster</span></span>
- <span data-ttu-id="7500e-148">le compte de stockage des données d’entrée</span><span class="sxs-lookup"><span data-stu-id="7500e-148">storage account for the input data</span></span>
- <span data-ttu-id="7500e-149">le compte de stockage des données de sortie</span><span class="sxs-lookup"><span data-stu-id="7500e-149">storage account for the output data</span></span>

<span data-ttu-id="7500e-150">Pour simplifier ce didacticiel, vous utilisez un seul compte de stockage pour ces trois fonctions.</span><span class="sxs-lookup"><span data-stu-id="7500e-150">To simplify the tutorial, you use one storage account to serve the three purposes.</span></span> <span data-ttu-id="7500e-151">L’exemple de script Azure PowerShell de cette section exécute les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="7500e-151">The Azure PowerShell sample script found in this section performs the following tasks:</span></span>

1. <span data-ttu-id="7500e-152">Connectez-vous à Azure.</span><span class="sxs-lookup"><span data-stu-id="7500e-152">Log in to Azure.</span></span>
2. <span data-ttu-id="7500e-153">Création d’un groupe de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="7500e-153">Create an Azure resource group.</span></span>
3. <span data-ttu-id="7500e-154">Création d’un compte Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="7500e-154">Create an Azure Storage account.</span></span>
4. <span data-ttu-id="7500e-155">Création d’un conteneur d’objets blob dans le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="7500e-155">Create a Blob container in the storage account</span></span>
5. <span data-ttu-id="7500e-156">Copie des deux fichiers suivants dans le conteneur d’objets blob :</span><span class="sxs-lookup"><span data-stu-id="7500e-156">Copy the following two files to the Blob container:</span></span>

   * <span data-ttu-id="7500e-157">Fichier d’entrée : [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log)</span><span class="sxs-lookup"><span data-stu-id="7500e-157">Input data file: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log)</span></span>
   * <span data-ttu-id="7500e-158">Script HiveQL : [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql)</span><span class="sxs-lookup"><span data-stu-id="7500e-158">HiveQL script: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql)</span></span>

     <span data-ttu-id="7500e-159">Les deux fichiers sont stockés dans un conteneur d’objets blob public.</span><span class="sxs-lookup"><span data-stu-id="7500e-159">Both files are stored in a public Blob container.</span></span>


<span data-ttu-id="7500e-160">**Pour préparer le stockage et copier les fichiers à l’aide d’Azure PowerShell :**</span><span class="sxs-lookup"><span data-stu-id="7500e-160">**To prepare the storage and copy the files using Azure PowerShell:**</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7500e-161">Spécifiez des noms pour le groupe de ressources Azure et le compte de stockage Azure qui seront créés par le script.</span><span class="sxs-lookup"><span data-stu-id="7500e-161">Specify names for the Azure resource group and the Azure storage account that will be created by the script.</span></span>
> <span data-ttu-id="7500e-162">Notez le **nom du groupe de ressources**, le **nom du compte de stockage** et la **clé du compte de stockage** générés en sortie par le script.</span><span class="sxs-lookup"><span data-stu-id="7500e-162">Write down **resource group name**, **storage account name**, and **storage account key** outputted by the script.</span></span> <span data-ttu-id="7500e-163">Vous aurez besoin de ces informations dans la section suivante.</span><span class="sxs-lookup"><span data-stu-id="7500e-163">You need them in the next section.</span></span>

```powershell
$resourceGroupName = "<Azure Resource Group Name>"
$storageAccountName = "<Azure Storage Account Name>"
$location = "East US 2"

$sourceStorageAccountName = "hditutorialdata"  
$sourceContainerName = "adfhiveactivity"

$destStorageAccountName = $storageAccountName
$destContainerName = "adfgetstarted" # don't change this value.

####################################
# Connect to Azure
####################################
#region - Connect to Azure subscription
Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
try{Get-AzureRmContext}
catch{Login-AzureRmAccount}
#endregion

####################################
# Create a resource group, storage, and container
####################################

#region - create Azure resources
Write-Host "`nCreating resource group, storage account and blob container ..." -ForegroundColor Green

New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
New-AzureRmStorageAccount `
    -ResourceGroupName $resourceGroupName `
    -Name $destStorageAccountName `
    -type Standard_LRS `
    -Location $location

$destStorageAccountKey = (Get-AzureRmStorageAccountKey `
    -ResourceGroupName $resourceGroupName `
    -Name $destStorageAccountName)[0].Value

$sourceContext = New-AzureStorageContext `
    -StorageAccountName $sourceStorageAccountName `
    -Anonymous
$destContext = New-AzureStorageContext `
    -StorageAccountName $destStorageAccountName `
    -StorageAccountKey $destStorageAccountKey

New-AzureStorageContainer -Name $destContainerName -Context $destContext
#endregion

####################################
# Copy files
####################################
#region - copy files
Write-Host "`nCopying files ..." -ForegroundColor Green

$blobs = Get-AzureStorageBlob `
    -Context $sourceContext `
    -Container $sourceContainerName

$blobs|Start-AzureStorageBlobCopy `
    -DestContext $destContext `
    -DestContainer $destContainerName

Write-Host "`nCopied files ..." -ForegroundColor Green
Get-AzureStorageBlob -Context $destContext -Container $destContainerName
#endregion

Write-host "`nYou will use the following values:" -ForegroundColor Green
write-host "`nResource group name: $resourceGroupName"
Write-host "Storage Account Name: $destStorageAccountName"
write-host "Storage Account Key: $destStorageAccountKey"

Write-host "`nScript completed" -ForegroundColor Green
```

<span data-ttu-id="7500e-164">Si vous avez besoin d’aide avec le script PowerShell, consultez l’article [Utilisation d’Azure PowerShell avec le service Stockage Azure](../storage/common/storage-powershell-guide-full.md).</span><span class="sxs-lookup"><span data-stu-id="7500e-164">If you need help with the PowerShell script, see [Using the Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md).</span></span> <span data-ttu-id="7500e-165">Si vous préférez utiliser l’interface de ligne de commande Azure, consultez la section [Annexe](#appendix) relative au script d’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="7500e-165">If you like to use Azure CLI instead, see the [Appendix](#appendix) section for the Azure CLI script.</span></span>

<span data-ttu-id="7500e-166">**Pour examiner le compte de stockage et son contenu**</span><span class="sxs-lookup"><span data-stu-id="7500e-166">**To examine the storage account and the contents**</span></span>

1. <span data-ttu-id="7500e-167">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7500e-167">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="7500e-168">Cliquez sur **Groupes de ressources** dans le volet de gauche.</span><span class="sxs-lookup"><span data-stu-id="7500e-168">Click **Resource groups** on the left pane.</span></span>
3. <span data-ttu-id="7500e-169">Double-cliquez sur le nom du groupe de ressources que vous avez créé dans votre script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7500e-169">Double-click the resource group name you created in your PowerShell script.</span></span> <span data-ttu-id="7500e-170">Utilisez le filtre si la liste des groupes de ressources est trop longue.</span><span class="sxs-lookup"><span data-stu-id="7500e-170">Use the filter if you have too many resource groups listed.</span></span>
4. <span data-ttu-id="7500e-171">Dans la mosaïque **Ressources** , vous devez voir une ressource, sauf si vous partagez le groupe de ressources avec d’autres projets.</span><span class="sxs-lookup"><span data-stu-id="7500e-171">On the **Resources** tile, you shall have one resource listed unless you share the resource group with other projects.</span></span> <span data-ttu-id="7500e-172">Cette ressource correspond au compte de stockage avec le nom que vous avez spécifié précédemment.</span><span class="sxs-lookup"><span data-stu-id="7500e-172">That resource is the storage account with the name you specified earlier.</span></span> <span data-ttu-id="7500e-173">Cliquez sur le nom du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="7500e-173">Click the storage account name.</span></span>
5. <span data-ttu-id="7500e-174">Cliquez sur la mosaïque **Objets Blob** .</span><span class="sxs-lookup"><span data-stu-id="7500e-174">Click the **Blobs** tiles.</span></span>
6. <span data-ttu-id="7500e-175">Cliquez sur le conteneur **adfgetstarted** .</span><span class="sxs-lookup"><span data-stu-id="7500e-175">Click the **adfgetstarted** container.</span></span> <span data-ttu-id="7500e-176">Vous voyez deux dossiers : **inputdata** et **script**.</span><span class="sxs-lookup"><span data-stu-id="7500e-176">You see two folders: **inputdata** and **script**.</span></span>
7. <span data-ttu-id="7500e-177">Ouvrez le dossier et vérifiez les fichiers des deux dossiers.</span><span class="sxs-lookup"><span data-stu-id="7500e-177">Open the folder and check the files in the folders.</span></span> <span data-ttu-id="7500e-178">Le dossier inputdata contient le fichier input.log avec les données d’entrée, tandis que le dossier script contient le fichier de script HiveQL.</span><span class="sxs-lookup"><span data-stu-id="7500e-178">The inputdata contains the input.log file with input data and the script folder contains the HiveQL script file.</span></span>

## <a name="create-a-data-factory-using-resource-manager-template"></a><span data-ttu-id="7500e-179">Créer une fabrique de données à l’aide du modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7500e-179">Create a data factory using Resource Manager template</span></span>
<span data-ttu-id="7500e-180">Avec le compte de stockage, les données d’entrée et le script HiveQL préparé, vous êtes prêt à créer une fabrique de données Azure.</span><span class="sxs-lookup"><span data-stu-id="7500e-180">With the storage account, the input data, and the HiveQL script prepared, you are ready to create an Azure data factory.</span></span> <span data-ttu-id="7500e-181">Il existe plusieurs méthodes pour créer la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="7500e-181">There are several methods for creating data factory.</span></span> <span data-ttu-id="7500e-182">Dans ce didacticiel, vous créez une fabrique de données en déployant un modèle Azure Resource Manager à l’aide du Portail Azure.</span><span class="sxs-lookup"><span data-stu-id="7500e-182">In this tutorial, you create a data factory by deploying an Azure Resource Manager template using the Azure portal.</span></span> <span data-ttu-id="7500e-183">Vous pouvez également déployer un modèle Resource Manager en utilisant [l’interface de ligne de commande Azure](../azure-resource-manager/resource-group-template-deploy-cli.md) et [Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span><span class="sxs-lookup"><span data-stu-id="7500e-183">You can also deploy a Resource Manager template by using [Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md) and [Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span></span> <span data-ttu-id="7500e-184">Pour les autres méthodes de création de fabriques de données, consultez la page [Didacticiel : créer votre première fabrique de données](../data-factory/data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="7500e-184">For other data factory creation methods, see [Tutorial: Build your first data factory](../data-factory/data-factory-build-your-first-pipeline.md).</span></span>

1. <span data-ttu-id="7500e-185">Cliquez sur l’image suivante pour vous connecter à Azure et ouvrir le modèle Resource Manager dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="7500e-185">Click the following image to sign in to Azure and open the Resource Manager template in the Azure portal.</span></span> <span data-ttu-id="7500e-186">Le modèle se trouve dans https://hditutorialdata.blob.core.windows.net/adfhiveactivity/data-factory-hdinsight-on-demand.json.</span><span class="sxs-lookup"><span data-stu-id="7500e-186">The template is located at https://hditutorialdata.blob.core.windows.net/adfhiveactivity/data-factory-hdinsight-on-demand.json.</span></span> <span data-ttu-id="7500e-187">Pour obtenir des informations détaillées sur les entités définies dans le modèle, consultez la section [Entités Data Factory dans le modèle](#data-factory-entities-in-the-template).</span><span class="sxs-lookup"><span data-stu-id="7500e-187">See the [Data Factory entities in the template](#data-factory-entities-in-the-template) section for detailed information about entities defined in the template.</span></span> 

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fadfhiveactivity%2Fdata-factory-hdinsight-on-demand.json" target="_blank"><img src="./media/hdinsight-hadoop-create-linux-clusters-adf/deploy-to-azure.png" alt="Deploy to Azure"></a>
2. <span data-ttu-id="7500e-188">Sélectionnez l’option **Utiliser existant** pour le paramètre **Groupe de ressources**, puis sélectionnez le nom du groupe de ressources que vous avez créé à l’étape précédente (à l’aide du script PowerShell).</span><span class="sxs-lookup"><span data-stu-id="7500e-188">Select **Use existing** option for the **Resource group** setting, and select the name of the resource group you created in the previous step (using PowerShell script).</span></span>
3. <span data-ttu-id="7500e-189">Entrez un nom pour la fabrique de données (**Nom de la fabrique de données**).</span><span class="sxs-lookup"><span data-stu-id="7500e-189">Enter a name for the data factory (**Data Factory Name**).</span></span> <span data-ttu-id="7500e-190">Ce nom doit être globalement unique.</span><span class="sxs-lookup"><span data-stu-id="7500e-190">This name must be globally unique.</span></span>
4. <span data-ttu-id="7500e-191">Entrez le **nom du compte de stockage** et la **clé du compte de stockage** que vous avez notés à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="7500e-191">Enter the **storage account name** and **storage account key** you wrote down in the previous step.</span></span>
5. <span data-ttu-id="7500e-192">Après avoir lu les **termes et conditions**, cochez la case **J’accepte les termes et conditions mentionnés ci-dessus**.</span><span class="sxs-lookup"><span data-stu-id="7500e-192">Select **I agree to the terms and conditions** stated above after reading through **terms and conditions**.</span></span>
6. <span data-ttu-id="7500e-193">Sélectionnez l’option **Épingler au tableau de bord**.</span><span class="sxs-lookup"><span data-stu-id="7500e-193">Select **Pin to dashboard** option.</span></span>
6. <span data-ttu-id="7500e-194">Cliquez sur **Acheter/Créer**.</span><span class="sxs-lookup"><span data-stu-id="7500e-194">Click **Purchase/Create**.</span></span> <span data-ttu-id="7500e-195">La vignette **Déploiement du modèle de déploiement** apparaît sur le tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="7500e-195">You see a tile on the Dashboard called **Deploying Template deployment**.</span></span> <span data-ttu-id="7500e-196">Attendez que le panneau **Groupe de ressources** de votre groupe de ressources s’affiche.</span><span class="sxs-lookup"><span data-stu-id="7500e-196">Wait until the **Resource group** blade for your resource group opens.</span></span> <span data-ttu-id="7500e-197">Pour ouvrir le volet du groupe de ressources, vous pouvez également cliquer sur la vignette libellée avec le nom de votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="7500e-197">You can also click the tile titled as your resource group name to open the resource group blade.</span></span>
6. <span data-ttu-id="7500e-198">Si le panneau du groupe de ressources n’est pas encore ouvert, cliquez sur la vignette pour ouvrir le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="7500e-198">Click the tile to open the resource group if the resource group blade is not already open.</span></span> <span data-ttu-id="7500e-199">Vous devez maintenant voir une autre ressource de fabrique de données en plus de la ressource du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="7500e-199">Now you shall see one more data factory resource listed in addition to the storage account resource.</span></span>
7. <span data-ttu-id="7500e-200">Cliquez sur le nom de votre fabrique de données (valeur que vous avez spécifiée pour le paramètre **Nom de la fabrique de données**).</span><span class="sxs-lookup"><span data-stu-id="7500e-200">Click the name of your data factory (value you specified for the **Data Factory Name** parameter).</span></span>
8. <span data-ttu-id="7500e-201">Dans le panneau Data Factory, cliquez sur la vignette **Diagramme**.</span><span class="sxs-lookup"><span data-stu-id="7500e-201">In the Data Factory blade, click the **Diagram** tile.</span></span> <span data-ttu-id="7500e-202">Le diagramme montre une activité avec un jeu de données d’entrée et un jeu de données de sortie :</span><span class="sxs-lookup"><span data-stu-id="7500e-202">The diagram shows one activity with an input dataset, and an output dataset:</span></span>

    ![Diagramme du pipeline d’activité Hive à la demande HDInsight avec Azure Data Factory](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-pipeline-diagram.png)

    <span data-ttu-id="7500e-204">Les noms sont définis dans le modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7500e-204">The names are defined in the Resource Manager template.</span></span>
9. <span data-ttu-id="7500e-205">Double-cliquez sur **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="7500e-205">Double-click **AzureBlobOutput**.</span></span>
10. <span data-ttu-id="7500e-206">Dans **Tranches récemment mises à jour**, une tranche doit s’afficher.</span><span class="sxs-lookup"><span data-stu-id="7500e-206">On the **Recent updated slices**, you shall see one slice.</span></span> <span data-ttu-id="7500e-207">Si l’état est **En cours**, attendez jusqu’à ce qu’il passe à **Prêt**.</span><span class="sxs-lookup"><span data-stu-id="7500e-207">If the status is **In progress**, wait until it is changed to **Ready**.</span></span> <span data-ttu-id="7500e-208">La création d’un cluster HDInsight nécessite environ **20 minutes**.</span><span class="sxs-lookup"><span data-stu-id="7500e-208">It usually takes about **20 minutes** to create an HDInsight cluster.</span></span>

### <a name="check-the-data-factory-output"></a><span data-ttu-id="7500e-209">Vérifier la sortie de la fabrique de données</span><span class="sxs-lookup"><span data-stu-id="7500e-209">Check the data factory output</span></span>

1. <span data-ttu-id="7500e-210">Utilisez la même procédure dans la dernière session pour vérifier les conteneurs du conteneur adfgetstarted.</span><span class="sxs-lookup"><span data-stu-id="7500e-210">Use the same procedure in the last session to check the containers of the adfgetstarted container.</span></span> <span data-ttu-id="7500e-211">Il existe deux nouveaux conteneurs en plus de **adfgetsarted**:</span><span class="sxs-lookup"><span data-stu-id="7500e-211">There are two new containers in addition to **adfgetsarted**:</span></span>

   * <span data-ttu-id="7500e-212">Un conteneur dont le nom est conforme au modèle suivant : `adf<yourdatafactoryname>-linkedservicename-datetimestamp`.</span><span class="sxs-lookup"><span data-stu-id="7500e-212">A container with name that follows the pattern: `adf<yourdatafactoryname>-linkedservicename-datetimestamp`.</span></span> <span data-ttu-id="7500e-213">Il s’agit du conteneur par défaut pour le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7500e-213">This container is the default container for the HDInsight cluster.</span></span>
   * <span data-ttu-id="7500e-214">adfjobs : ce conteneur est le conteneur des journaux de travaux Azure Data Factory (ADF).</span><span class="sxs-lookup"><span data-stu-id="7500e-214">adfjobs: This container is the container for the ADF job logs.</span></span>

     <span data-ttu-id="7500e-215">La sortie de la fabrique de données est stockée dans le conteneur **adfgetstarted**, comme vous l’avez configuré dans le modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7500e-215">The data factory output is stored in **afgetstarted** as you configured in the Resource Manager template.</span></span>
2. <span data-ttu-id="7500e-216">Cliquez sur **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="7500e-216">Click **adfgetstarted**.</span></span>
3. <span data-ttu-id="7500e-217">Double-cliquez sur **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="7500e-217">Double-click **partitioneddata**.</span></span> <span data-ttu-id="7500e-218">Un dossier **year=2014** s’affiche, car tous les journaux Web datent de l’année 2014.</span><span class="sxs-lookup"><span data-stu-id="7500e-218">You see a **year=2014** folder because all the web logs are dated in year 2014.</span></span>

    ![Sortie du pipeline d’activité Hive à la demande HDInsight avec Azure Data Factory](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-year.png)

    <span data-ttu-id="7500e-220">Si vous ouvrez la liste, vous devez voir trois dossiers pour janvier, février et mars.</span><span class="sxs-lookup"><span data-stu-id="7500e-220">If you drill down the list, you shall see three folders for January, February, and March.</span></span> <span data-ttu-id="7500e-221">Il y a un journal pour chaque mois.</span><span class="sxs-lookup"><span data-stu-id="7500e-221">And there is a log for each month.</span></span>

    ![Sortie du pipeline d’activité Hive à la demande HDInsight avec Azure Data Factory](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-month.png)

## <a name="data-factory-entities-in-the-template"></a><span data-ttu-id="7500e-223">Entités Data Factory dans le modèle</span><span class="sxs-lookup"><span data-stu-id="7500e-223">Data Factory entities in the template</span></span>
<span data-ttu-id="7500e-224">Le modèle Resource Manager de niveau supérieur d’une fabrique de données ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="7500e-224">Here is how the top-level Resource Manager template for a data factory looks like:</span></span>

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": { ...
    },
    "variables": { ...
    },
    "resources": [
        {
            "name": "[parameters('dataFactoryName')]",
            "apiVersion": "[variables('apiVersion')]",
            "type": "Microsoft.DataFactory/datafactories",
            "location": "westus",
            "resources": [
                { ... },
                { ... },
                { ... },
                { ... }
            ]
        }
    ]
}
```

### <a name="define-data-factory"></a><span data-ttu-id="7500e-225">Définir une fabrique de données</span><span class="sxs-lookup"><span data-stu-id="7500e-225">Define data factory</span></span>
<span data-ttu-id="7500e-226">Vous définissez une fabrique de données dans le modèle Resource Manager, comme indiqué dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="7500e-226">You define a data factory in the Resource Manager template as shown in the following sample:</span></span>  

```json
"resources": [
{
    "name": "[parameters('dataFactoryName')]",
    "apiVersion": "[variables('apiVersion')]",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "westus",
}
```
<span data-ttu-id="7500e-227">L’élément dataFactoryName est le nom de la fabrique de données que vous spécifiez lorsque vous déployez le modèle.</span><span class="sxs-lookup"><span data-stu-id="7500e-227">The dataFactoryName is the name of the data factory you specify when you deploy the template.</span></span> <span data-ttu-id="7500e-228">Pour l’instant, Data Factory est uniquement pris en charge dans les régions États-Unis de l’Est, États-Unis de l’Ouest et Europe du Nord.</span><span class="sxs-lookup"><span data-stu-id="7500e-228">Data factory is currently only supported in the East US, West US, and North Europe regions.</span></span>

### <a name="defining-entities-within-the-data-factory"></a><span data-ttu-id="7500e-229">Définition d’entités dans la fabrique de données</span><span class="sxs-lookup"><span data-stu-id="7500e-229">Defining entities within the data factory</span></span>
<span data-ttu-id="7500e-230">Les entités Data Factory suivantes sont définies dans le modèle JSON :</span><span class="sxs-lookup"><span data-stu-id="7500e-230">The following Data Factory entities are defined in the JSON template:</span></span>

* [<span data-ttu-id="7500e-231">Service lié Azure Storage</span><span class="sxs-lookup"><span data-stu-id="7500e-231">Azure Storage linked service</span></span>](#azure-storage-linked-service)
* [<span data-ttu-id="7500e-232">Service lié à la demande HDInsight</span><span class="sxs-lookup"><span data-stu-id="7500e-232">HDInsight on-demand linked service</span></span>](#hdinsight-on-demand-linked-service)
* [<span data-ttu-id="7500e-233">Jeu de données d'entrée d'objet Blob Azure</span><span class="sxs-lookup"><span data-stu-id="7500e-233">Azure blob input dataset</span></span>](#azure-blob-input-dataset)
* [<span data-ttu-id="7500e-234">Jeu de données de sortie d’objet Blob Azure</span><span class="sxs-lookup"><span data-stu-id="7500e-234">Azure blob output dataset</span></span>](#azure-blob-output-dataset)
* [<span data-ttu-id="7500e-235">Pipeline de données avec une activité de copie</span><span class="sxs-lookup"><span data-stu-id="7500e-235">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="7500e-236">Service lié Azure Storage</span><span class="sxs-lookup"><span data-stu-id="7500e-236">Azure Storage linked service</span></span>
<span data-ttu-id="7500e-237">Le service lié Stockage Azure relie votre compte de stockage Azure à la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="7500e-237">The Azure Storage linked service links your Azure storage account to the data factory.</span></span> <span data-ttu-id="7500e-238">Dans ce didacticiel, le même compte de stockage est utilisé comme compte de stockage HDInsight par défaut, comme stockage des données d’entrée et comme stockage des données de sortie.</span><span class="sxs-lookup"><span data-stu-id="7500e-238">In this tutorial, the same storage account is used as the default HDInsight storage account, input data storage, and output data storage.</span></span> <span data-ttu-id="7500e-239">Par conséquent, vous ne définissez qu’un seul service lié Stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="7500e-239">Therefore, you define only one Azure Storage linked service.</span></span> <span data-ttu-id="7500e-240">Dans la définition du service lié, vous spécifiez le nom et la clé de votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="7500e-240">In the linked service definition, you specify the name and key of your Azure storage account.</span></span> <span data-ttu-id="7500e-241">Consultez [Service lié Stockage Azure](../data-factory/data-factory-azure-blob-connector.md#azure-storage-linked-service) pour en savoir plus sur les propriétés JSON utilisées pour définir un service lié Stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="7500e-241">See [Azure Storage linked service](../data-factory/data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used to define an Azure Storage linked service.</span></span>

```json
{
    "name": "[variables('storageLinkedServiceName')]",
    "type": "linkedservices",
    "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]" ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]"
        }
    }
}
```
<span data-ttu-id="7500e-242">La propriété **connectionString** utilise les paramètres storageAccountName et storageAccountKey.</span><span class="sxs-lookup"><span data-stu-id="7500e-242">The **connectionString** uses the storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="7500e-243">Vous renseignez ces paramètres lors du déploiement du modèle.</span><span class="sxs-lookup"><span data-stu-id="7500e-243">You specify values for these parameters while deploying the template.</span></span>  

#### <a name="hdinsight-on-demand-linked-service"></a><span data-ttu-id="7500e-244">Service lié à la demande HDInsight</span><span class="sxs-lookup"><span data-stu-id="7500e-244">HDInsight on-demand linked service</span></span>
<span data-ttu-id="7500e-245">Dans la définition du service lié HDInsight à la demande, vous spécifiez les valeurs des paramètres de configuration que le service Data Factory utilise pour créer un cluster Hadoop HDInsight au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="7500e-245">In the on-demand HDInsight linked service definition, you specify values for configuration parameters that are used by the Data Factory service to create a HDInsight Hadoop cluster at runtime.</span></span> <span data-ttu-id="7500e-246">Consultez l’article [Services liés de calcul](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) pour en savoir plus sur les propriétés JSON utilisées pour définir un service lié à la demande HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7500e-246">See [Compute linked services](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article for details about JSON properties used to define an HDInsight on-demand linked service.</span></span>  

```json

{
    "type": "linkedservices",
    "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "sshUserName": "myuser",                            
            "sshPassword": "MyPassword!",
            "linkedServiceName": "[variables('storageLinkedServiceName')]"
        }
    }
}
```
<span data-ttu-id="7500e-247">Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="7500e-247">Note the following points:</span></span>

* <span data-ttu-id="7500e-248">Data Factory crée un cluster HDInsight **Linux** à votre intention.</span><span class="sxs-lookup"><span data-stu-id="7500e-248">The Data Factory creates a **Linux-based** HDInsight cluster for you.</span></span>
* <span data-ttu-id="7500e-249">Le cluster Hadoop HDInsight est créé dans la même région que le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="7500e-249">The HDInsight Hadoop cluster is created in the same region as the storage account.</span></span>
* <span data-ttu-id="7500e-250">Notez le paramètre *timeToLive* .</span><span class="sxs-lookup"><span data-stu-id="7500e-250">Notice the *timeToLive* setting.</span></span> <span data-ttu-id="7500e-251">La fabrique de données supprime automatiquement le cluster quand celui-ci est inactif pendant 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="7500e-251">The data factory deletes the cluster automatically after the cluster is being idle for 30 minutes.</span></span>
* <span data-ttu-id="7500e-252">Le cluster HDInsight crée un **conteneur par défaut** dans le stockage d’objets blob que vous avez spécifié dans le JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="7500e-252">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (**linkedServiceName**).</span></span> <span data-ttu-id="7500e-253">HDInsight ne supprime pas ce conteneur lorsque le cluster est supprimé.</span><span class="sxs-lookup"><span data-stu-id="7500e-253">HDInsight does not delete this container when the cluster is deleted.</span></span> <span data-ttu-id="7500e-254">Ce comportement est normal.</span><span class="sxs-lookup"><span data-stu-id="7500e-254">This behavior is by design.</span></span> <span data-ttu-id="7500e-255">Avec le service lié HDInsight à la demande, un cluster HDInsight est créé à chaque fois qu’une tranche doit être traitée, à moins qu’il n’existe un cluster activé (**timeToLive**), et est supprimé une fois le traitement activé.</span><span class="sxs-lookup"><span data-stu-id="7500e-255">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice needs to be processed unless there is an existing live cluster (**timeToLive**) and is deleted when the processing is done.</span></span>

<span data-ttu-id="7500e-256">Pour plus d’informations, voir [Service lié à la demande Azure HDInsight](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="7500e-256">See [On-demand HDInsight Linked Service](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7500e-257">Comme un nombre croissant de tranches sont traitées, vous voyez un grand nombre de conteneurs dans votre stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="7500e-257">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="7500e-258">Si vous n’en avez pas besoin pour dépanner les travaux, il se peut que vous deviez les supprimer pour réduire les frais de stockage.</span><span class="sxs-lookup"><span data-stu-id="7500e-258">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="7500e-259">Le nom de ces conteneurs suit un modèle : « **nomdevotrefabriquededonnéesadf**-**nomduservicelié**-horodatage ».</span><span class="sxs-lookup"><span data-stu-id="7500e-259">The names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="7500e-260">Utilisez des outils tels que [Microsoft Storage Explorer](http://storageexplorer.com/) pour supprimer des conteneurs dans votre stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="7500e-260">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span></span>

#### <a name="azure-blob-input-dataset"></a><span data-ttu-id="7500e-261">Jeu de données d'entrée d'objet Blob Azure</span><span class="sxs-lookup"><span data-stu-id="7500e-261">Azure blob input dataset</span></span>
<span data-ttu-id="7500e-262">Dans la définition du jeu de données d’entrée, vous spécifiez les noms du conteneur d’objets blob, du dossier et du fichier contenant les données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="7500e-262">In the input dataset definition, you specify the names of blob container, folder, and file that contains the input data.</span></span> <span data-ttu-id="7500e-263">Consultez [Propriétés du jeu de données d’objet blob Azure](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) pour en savoir plus sur les propriétés JSON permettant de définir un jeu de données d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="7500e-263">See [Azure Blob dataset properties](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span></span>

```json

{
    "type": "datasets",
    "name": "[variables('blobInputDatasetName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('storageLinkedServiceName')]",
        "typeProperties": {
            "fileName": "input.log",
            "folderPath": "adfgetstarted/inputdata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}

```

<span data-ttu-id="7500e-264">Notez les paramètres spécifiques ci-après dans la définition JSON :</span><span class="sxs-lookup"><span data-stu-id="7500e-264">Notice the following specific settings in the JSON definition:</span></span>

```json
"fileName": "input.log",
"folderPath": "adfgetstarted/inputdata",
```

#### <a name="azure-blob-output-dataset"></a><span data-ttu-id="7500e-265">Jeu de données de sortie d’objet Blob Azure</span><span class="sxs-lookup"><span data-stu-id="7500e-265">Azure Blob output dataset</span></span>
<span data-ttu-id="7500e-266">Dans la définition du jeu de données de sortie, vous spécifiez les noms du conteneur d’objets blob et du dossier contenant les données de sortie.</span><span class="sxs-lookup"><span data-stu-id="7500e-266">In the output dataset definition, you specify the names of blob container and folder that holds the output data.</span></span> <span data-ttu-id="7500e-267">Consultez [Propriétés du jeu de données d’objet blob Azure](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) pour en savoir plus sur les propriétés JSON permettant de définir un jeu de données d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="7500e-267">See [Azure Blob dataset properties](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span></span>  

```json

{
    "type": "datasets",
    "name": "[variables('blobOutputDatasetName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('storageLinkedServiceName')]",
        "typeProperties": {
            "folderPath": "adfgetstarted/partitioneddata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1,
            "style": "EndOfInterval"
        }
    }
}
```

<span data-ttu-id="7500e-268">L’élément folderPath spécifie le chemin du dossier qui contient les données de sortie :</span><span class="sxs-lookup"><span data-stu-id="7500e-268">The folderPath specifies the path to the folder that holds the output data:</span></span>

```json
"folderPath": "adfgetstarted/partitioneddata",
```

<span data-ttu-id="7500e-269">Le paramètre [dataset availability](../data-factory/data-factory-create-datasets.md#dataset-availability) se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="7500e-269">The [dataset availability](../data-factory/data-factory-create-datasets.md#dataset-availability) setting is as follows:</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "style": "EndOfInterval"
},
```

<span data-ttu-id="7500e-270">Dans Azure Data Factory, la disponibilité du jeu de données de résultats conditionne le pipeline.</span><span class="sxs-lookup"><span data-stu-id="7500e-270">In Azure Data Factory, output dataset availability drives the pipeline.</span></span> <span data-ttu-id="7500e-271">Dans cet exemple, la tranche est produite le dernier jour de chaque mois (EndOfInterval).</span><span class="sxs-lookup"><span data-stu-id="7500e-271">In this example, the slice is produced monthly on the last day of month (EndOfInterval).</span></span> <span data-ttu-id="7500e-272">Pour plus d’informations, consultez [Planification et exécution avec Data Factory](../data-factory/data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="7500e-272">For more information, see [Data Factory Scheduling and Execution](../data-factory/data-factory-scheduling-and-execution.md).</span></span>

#### <a name="data-pipeline"></a><span data-ttu-id="7500e-273">Pipeline de données</span><span class="sxs-lookup"><span data-stu-id="7500e-273">Data pipeline</span></span>
<span data-ttu-id="7500e-274">Vous définissez un pipeline qui transforme les données en exécutant le script Hive sur un cluster Azure HDInsight à la demande.</span><span class="sxs-lookup"><span data-stu-id="7500e-274">You define a pipeline that transforms data by running Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="7500e-275">Consultez [Pipeline JSON](../data-factory/data-factory-create-pipelines.md#pipeline-json) pour obtenir des descriptions des éléments JSON permettant de définir un pipeline dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="7500e-275">See [Pipeline JSON](../data-factory/data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used to define a pipeline in this example.</span></span>

```json
{
    "type": "datapipelines",
    "name": "[parameters('dataFactoryName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('hdInsightOnDemandLinkedServiceName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/datasets/', variables('blobInputDatasetName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/datasets/', variables('blobOutputDatasetName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "description": "Azure Data Factory pipeline with an Hadoop Hive activity",
        "activities": [
            {
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                    "scriptLinkedService": "[variables('storageLinkedServiceName')]",
                    "defines": {
                        "inputtable": "[concat('wasb://adfgetstarted@', parameters('storageAccountName'), '.blob.core.windows.net/inputdata')]",
                        "partitionedtable": "[concat('wasb://adfgetstarted@', parameters('storageAccountName'), '.blob.core.windows.net/partitioneddata')]"
                    }
                },
                "inputs": [
                    {
                        "name": "AzureBlobInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "policy": {
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "RunSampleHiveActivity",
                "linkedServiceName": "HDInsightOnDemandLinkedService"
            }
        ],
        "start": "2016-01-01T00:00:00Z",
        "end": "2016-01-31T00:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="7500e-276">Le pipeline ne contient qu’une seule activité, l’activité HDInsightHive.</span><span class="sxs-lookup"><span data-stu-id="7500e-276">The pipeline contains one activity, HDInsightHive activity.</span></span> <span data-ttu-id="7500e-277">Étant donné que les dates de début et de fin appartiennent toutes deux au mois de janvier 2016, le traitement ne porte que sur les données d’un seul mois (une tranche).</span><span class="sxs-lookup"><span data-stu-id="7500e-277">As both start and end dates are in January 2016, data for only one month (a slice) is processed.</span></span> <span data-ttu-id="7500e-278">Puisque les deux éléments *start* et *end* de l’activité correspondent à une date située dans le passé, Data Factory traite immédiatement les données du mois.</span><span class="sxs-lookup"><span data-stu-id="7500e-278">Both *start* and *end* of the activity have a past date, so the Data Factory processes data for the month immediately.</span></span> <span data-ttu-id="7500e-279">Si la fin est une date à venir, la fabrique de données crée une autre tranche en temps voulu.</span><span class="sxs-lookup"><span data-stu-id="7500e-279">If the end is a future date, the data factory creates another slice when the time comes.</span></span> <span data-ttu-id="7500e-280">Pour plus d’informations, consultez [Planification et exécution avec Data Factory](../data-factory/data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="7500e-280">For more information, see [Data Factory Scheduling and Execution](../data-factory/data-factory-scheduling-and-execution.md).</span></span>

## <a name="clean-up-the-tutorial"></a><span data-ttu-id="7500e-281">Nettoyage du didacticiel</span><span class="sxs-lookup"><span data-stu-id="7500e-281">Clean up the tutorial</span></span>

### <a name="delete-the-blob-containers-created-by-on-demand-hdinsight-cluster"></a><span data-ttu-id="7500e-282">Supprimer les conteneurs d’objets blob créés par le cluster HDInsight à la demande</span><span class="sxs-lookup"><span data-stu-id="7500e-282">Delete the blob containers created by on-demand HDInsight cluster</span></span>
<span data-ttu-id="7500e-283">Avec le service lié HDInsight à la demande, un cluster HDInsight est créé à chaque fois qu’une tranche doit être traitée, à moins qu’il existe un cluster activé (timeToLive). Le cluster est supprimé une fois le traitement terminé.</span><span class="sxs-lookup"><span data-stu-id="7500e-283">With on-demand HDInsight linked service, an HDInsight cluster is created every time a slice needs to be processed unless there is an existing live cluster (timeToLive); and the cluster is deleted when the processing is done.</span></span> <span data-ttu-id="7500e-284">Pour chaque cluster, Azure Data Factory crée un conteneur d’objets blob dans le stockage Blob Azure utilisé comme compte de stockage par défaut pour le cluster.</span><span class="sxs-lookup"><span data-stu-id="7500e-284">For each cluster, Azure Data Factory creates a blob container in the Azure blob storage used as the default stroage account for the cluster.</span></span> <span data-ttu-id="7500e-285">Bien que le cluster HDInsight soit supprimé, le conteneur de stockage d’objets blob par défaut et le compte de stockage associé ne sont pas supprimés.</span><span class="sxs-lookup"><span data-stu-id="7500e-285">Even though HDInsight cluster is deleted, the default blob storage container and the associated storage account are not deleted.</span></span> <span data-ttu-id="7500e-286">Ce comportement est normal.</span><span class="sxs-lookup"><span data-stu-id="7500e-286">This behavior is by design.</span></span> <span data-ttu-id="7500e-287">Comme un nombre croissant de tranches sont traitées, vous voyez un grand nombre de conteneurs dans votre stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="7500e-287">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="7500e-288">Si vous n’en avez pas besoin pour dépanner les travaux, il se peut que vous deviez les supprimer pour réduire les frais de stockage.</span><span class="sxs-lookup"><span data-stu-id="7500e-288">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="7500e-289">Les noms de ces conteneurs sont conformes au modèle suivant : `adfyourdatafactoryname-linkedservicename-datetimestamp`.</span><span class="sxs-lookup"><span data-stu-id="7500e-289">The names of these containers follow a pattern: `adfyourdatafactoryname-linkedservicename-datetimestamp`.</span></span>

<span data-ttu-id="7500e-290">Supprimez les dossiers **adfjobs** et **adfyourdatafactoryname-linkedservicename-datetimestamp**.</span><span class="sxs-lookup"><span data-stu-id="7500e-290">Delete the **adfjobs** and **adfyourdatafactoryname-linkedservicename-datetimestamp** folders.</span></span> <span data-ttu-id="7500e-291">Le conteneur adfjobs contient les journaux de travaux d’Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="7500e-291">The adfjobs container contains job logs from Azure Data Factory.</span></span>

### <a name="delete-the-resource-group"></a><span data-ttu-id="7500e-292">Supprimer le groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="7500e-292">Delete the resource group</span></span>
<span data-ttu-id="7500e-293">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) est utilisé pour déployer, gérer et surveiller votre solution en tant que groupe.</span><span class="sxs-lookup"><span data-stu-id="7500e-293">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) is used to deploy, manage, and monitor your solution as a group.</span></span>  <span data-ttu-id="7500e-294">La suppression d’un groupe de ressources supprime tous les composants qu’il contient.</span><span class="sxs-lookup"><span data-stu-id="7500e-294">Deleting a resource group deletes all the components inside the group.</span></span>  

1. <span data-ttu-id="7500e-295">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7500e-295">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="7500e-296">Cliquez sur **Groupes de ressources** dans le volet de gauche.</span><span class="sxs-lookup"><span data-stu-id="7500e-296">Click **Resource groups** on the left pane.</span></span>
3. <span data-ttu-id="7500e-297">Cliquez sur le nom du groupe de ressources que vous avez créé dans votre script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7500e-297">Click the resource group name you created in your PowerShell script.</span></span> <span data-ttu-id="7500e-298">Utilisez le filtre si la liste des groupes de ressources est trop longue.</span><span class="sxs-lookup"><span data-stu-id="7500e-298">Use the filter if you have too many resource groups listed.</span></span> <span data-ttu-id="7500e-299">Il ouvre le groupe de ressources dans un nouveau panneau.</span><span class="sxs-lookup"><span data-stu-id="7500e-299">It opens the resource group in a new blade.</span></span>
4. <span data-ttu-id="7500e-300">Dans la mosaïque **Ressources**, vous devez voir le compte de stockage par défaut et la fabrique de données, sauf si vous partagez le groupe de ressources avec d’autres projets.</span><span class="sxs-lookup"><span data-stu-id="7500e-300">On the **Resources** tile, you shall have the default storage account and the data factory listed unless you share the resource group with other projects.</span></span>
5. <span data-ttu-id="7500e-301">Cliquez sur **Supprimer** dans la partie supérieure du panneau.</span><span class="sxs-lookup"><span data-stu-id="7500e-301">Click **Delete** on the top of the blade.</span></span> <span data-ttu-id="7500e-302">Ce faisant, vous supprimez le compte de stockage et les données stockées dans ce dernier.</span><span class="sxs-lookup"><span data-stu-id="7500e-302">Doing so deletes the storage account and the data stored in the storage account.</span></span>
6. <span data-ttu-id="7500e-303">Entrez le nom du groupe de ressources pour confirmer la suppression, puis cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="7500e-303">Enter the resource group name to confirm deletion, and then click **Delete**.</span></span>

<span data-ttu-id="7500e-304">Si vous ne souhaitez pas supprimer le compte de stockage en même temps que le groupe de ressources, envisagez l’architecture suivante en séparant les données métiers du compte de stockage par défaut.</span><span class="sxs-lookup"><span data-stu-id="7500e-304">In case you don't want to delete the storage account when you delete the resource group, consider the following architecture by separating the business data from the default storage account.</span></span> <span data-ttu-id="7500e-305">Dans ce cas, vous disposez d’un groupe de ressources pour le compte de stockage avec les données métiers, et d’un autre groupe de ressources pour le compte de stockage par défaut pour le service lié HDInsight et la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="7500e-305">In this case, you have one resource group for the storage account with the business data, and the other resource group for the default storage account for HDInsight linked service and the data factory.</span></span> <span data-ttu-id="7500e-306">La suppression du second groupe de ressources n’a aucune incidence sur le compte de stockage des données métiers.</span><span class="sxs-lookup"><span data-stu-id="7500e-306">When you delete the second resource group, it does not impact the business data storage account.</span></span> <span data-ttu-id="7500e-307">Pour ce faire :</span><span class="sxs-lookup"><span data-stu-id="7500e-307">To do so:</span></span>

* <span data-ttu-id="7500e-308">Ajoutez le code suivant au groupe de ressources de niveau supérieur avec la ressource Microsoft.DataFactory/datafactories dans votre modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7500e-308">Add the following to the top-level resource group along with the Microsoft.DataFactory/datafactories resource in your Resource Manager template.</span></span> <span data-ttu-id="7500e-309">Ce code crée un compte de stockage :</span><span class="sxs-lookup"><span data-stu-id="7500e-309">It creates a storage account:</span></span>

    ```json
    {
        "name": "[parameters('defaultStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": {

        },
        "properties": {
            "accountType": "Standard_LRS"
        }
    },
    ```
* <span data-ttu-id="7500e-310">Ajoutez un nouveau point de service lié au nouveau compte de stockage :</span><span class="sxs-lookup"><span data-stu-id="7500e-310">Add a new linked service point to the new storage account:</span></span>

    ```json
    {
        "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]" ],
        "type": "linkedservices",
        "name": "[variables('defaultStorageLinkedServiceName')]",
        "apiVersion": "[variables('apiVersion')]",
        "properties": {
            "type": "AzureStorage",
            "typeProperties": {
                "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('defaultStorageAccountName'),';AccountKey=',listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('defaultStorageAccountName')), variables('defaultApiVersion')).key1)]"
            }
        }
    },
    ```
* <span data-ttu-id="7500e-311">Configurez le LinkedService HDInsight à la demande avec un dependsOn supplémentaire et un additionalLinkedServiceNames :</span><span class="sxs-lookup"><span data-stu-id="7500e-311">Configure the HDInsight ondemand linked service with an additional dependsOn and an additionalLinkedServiceNames:</span></span>

    ```json
    {
        "dependsOn": [
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('defaultStorageLinkedServiceName'))]",
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('storageLinkedServiceName'))]"

        ],
        "type": "linkedservices",
        "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
        "apiVersion": "[variables('apiVersion')]",
        "properties": {
            "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "sshUserName": "myuser",                            
                "sshPassword": "MyPassword!",
                "linkedServiceName": "[variables('storageLinkedServiceName')]",
                "additionalLinkedServiceNames": "[variables('defaultStorageLinkedServiceName')]"
            }
        }
    },            
    ```
## <a name="next-steps"></a><span data-ttu-id="7500e-312">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7500e-312">Next steps</span></span>
<span data-ttu-id="7500e-313">Dans cet article, vous avez appris comment utiliser Azure Data Factory pour créer un cluster HDInsight à la demande pour traiter des tâches Hive.</span><span class="sxs-lookup"><span data-stu-id="7500e-313">In this article, you have learned how to use Azure Data Factory to create on-demand HDInsight cluster to process Hive jobs.</span></span> <span data-ttu-id="7500e-314">En savoir plus :</span><span class="sxs-lookup"><span data-stu-id="7500e-314">To read more:</span></span>

* [<span data-ttu-id="7500e-315">Didacticiel Hadoop : prise en main de Hadoop sous Linux dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="7500e-315">Hadoop tutorial: Get started using Linux-based Hadoop in HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="7500e-316">Création de clusters Hadoop basés sur Linux dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="7500e-316">Create Linux-based Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="7500e-317">Documentation HDInsight</span><span class="sxs-lookup"><span data-stu-id="7500e-317">HDInsight documentation</span></span>](https://azure.microsoft.com/documentation/services/hdinsight/)
* [<span data-ttu-id="7500e-318">Documentation Data Factory</span><span class="sxs-lookup"><span data-stu-id="7500e-318">Data factory documentation</span></span>](https://azure.microsoft.com/documentation/services/data-factory/)

## <a name="appendix"></a><span data-ttu-id="7500e-319">Annexe</span><span class="sxs-lookup"><span data-stu-id="7500e-319">Appendix</span></span>

### <a name="azure-cli-script"></a><span data-ttu-id="7500e-320">Script d’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="7500e-320">Azure CLI script</span></span>
<span data-ttu-id="7500e-321">Pour suivre ce didacticiel, vous pouvez utiliser l’interface de ligne de commande Azure plutôt qu’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7500e-321">You can use Azure CLI instead of using Azure PowerShell to do the tutorial.</span></span> <span data-ttu-id="7500e-322">Pour utiliser l’interface de ligne de commande Azure, commencez par installer cette interface en suivant les instructions suivantes :</span><span class="sxs-lookup"><span data-stu-id="7500e-322">To use Azure CLI, first install Azure CLI as per the following instructions:</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

#### <a name="use-azure-cli-to-prepare-the-storage-and-copy-the-files"></a><span data-ttu-id="7500e-323">Utiliser l’interface de ligne de commande Azure pour préparer le stockage et copier les fichiers</span><span class="sxs-lookup"><span data-stu-id="7500e-323">Use Azure CLI to prepare the storage and copy the files</span></span>

```
azure login

azure config mode arm

azure group create --name "<Azure Resource Group Name>" --location "East US 2"

azure storage account create --resource-group "<Azure Resource Group Name>" --location "East US 2" --type "LRS" <Azure Storage Account Name>

azure storage account keys list --resource-group "<Azure Resource Group Name>" "<Azure Storage Account Name>"
azure storage container create "adfgetstarted" --account-name "<Azure Storage AccountName>" --account-key "<Azure Storage Account Key>"

azure storage blob copy start "https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log" --dest-account-name "<Azure Storage Account Name>" --dest-account-key "<Azure Storage Account Key>" --dest-container "adfgetstarted"
azure storage blob copy start "https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql" --dest-account-name "<Azure Storage Account Name>" --dest-account-key "<Azure Storage Account Key>" --dest-container "adfgetstarted"
```

<span data-ttu-id="7500e-324">Le nom du conteneur est *adfgetstarted*.</span><span class="sxs-lookup"><span data-stu-id="7500e-324">The container name is *adfgetstarted*.</span></span> <span data-ttu-id="7500e-325">Gardez-le tel quel.</span><span class="sxs-lookup"><span data-stu-id="7500e-325">Keep it as it is.</span></span> <span data-ttu-id="7500e-326">Dans le cas contraire, vous devez mettre à jour le modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7500e-326">Otherwise you need to update the Resource Manager template.</span></span> <span data-ttu-id="7500e-327">Si vous avez besoin d’aide avec ce script d’interface de ligne de commande, consultez [Utilisation de la CLI Microsoft Azure avec Microsoft Azure Storage](../storage/common/storage-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="7500e-327">If you need help with this CLI script, see [Using the Azure CLI with Azure Storage](../storage/common/storage-azure-cli.md).</span></span>
