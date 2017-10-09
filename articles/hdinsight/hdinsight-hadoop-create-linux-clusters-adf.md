---
title: "aaaCreate des clusters Hadoop de la demande à l’aide de Data Factory - Azure HDInsight | Documents Microsoft"
description: "Découvrez comment toocreate à la demande Hadoop clusters dans HDInsight à l’aide d’Azure Data Factory."
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
ms.openlocfilehash: c869776ac270e37dec710b5fc8d2a792d9263129
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-on-demand-hadoop-clusters-in-hdinsight-using-azure-data-factory"></a><span data-ttu-id="44eef-103">Créer des clusters Hadoop à la demande dans HDInsight avec Azure Data Factor</span><span class="sxs-lookup"><span data-stu-id="44eef-103">Create on-demand Hadoop clusters in HDInsight using Azure Data Factory</span></span>
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="44eef-104">[Azure Data Factory](../data-factory/data-factory-introduction.md) est un service d’intégration de données basées sur le cloud qui orchestre et automatise le déplacement de hello et la transformation de données.</span><span class="sxs-lookup"><span data-stu-id="44eef-104">[Azure Data Factory](../data-factory/data-factory-introduction.md) is a cloud-based data integration service that orchestrates and automates hello movement and transformation of data.</span></span> <span data-ttu-id="44eef-105">Il permet de créer un tooprocess juste-à-temps du cluster HDInsight Hadoop une tranche de données d’entrée et de supprimer le cluster de hello au terme du traitement de hello.</span><span class="sxs-lookup"><span data-stu-id="44eef-105">It can create a HDInsight Hadoop cluster just-in-time tooprocess an input data slice and delete hello cluster when hello processing is complete.</span></span> <span data-ttu-id="44eef-106">Hello les avantages de l’utilisation d’un cluster de HDInsight Hadoop à la demande sont :</span><span class="sxs-lookup"><span data-stu-id="44eef-106">Some of hello benefits of using an on-demand HDInsight Hadoop cluster are:</span></span>

- <span data-ttu-id="44eef-107">Un paiement uniquement pour la tâche de temps hello s’exécute sur hello du cluster HDInsight Hadoop (plus un bref temps d’inactivité configurable).</span><span class="sxs-lookup"><span data-stu-id="44eef-107">You only pay for hello time job is running on hello HDInsight Hadoop cluster (plus a brief configurable idle time).</span></span> <span data-ttu-id="44eef-108">facturation Hello pour les clusters HDInsight est proportionnel par minute, que vous les utilisiez ou non.</span><span class="sxs-lookup"><span data-stu-id="44eef-108">hello billing for HDInsight clusters is pro-rated per minute, whether you are using them or not.</span></span> <span data-ttu-id="44eef-109">Lorsque vous utilisez un service lié HDInsight de la demande dans la fabrique de données, les clusters hello sont créés à la demande.</span><span class="sxs-lookup"><span data-stu-id="44eef-109">When you use an on-demand HDInsight linked service in Data Factory, hello clusters are created on-demand.</span></span> <span data-ttu-id="44eef-110">Et les clusters hello sont supprimées automatiquement lorsque les tâches de hello sont terminées.</span><span class="sxs-lookup"><span data-stu-id="44eef-110">And hello clusters are deleted automatically when hello jobs are completed.</span></span> <span data-ttu-id="44eef-111">Par conséquent, vous ne payez que pour la tâche hello heure et la durée d’inactivité brève hello (paramètre de durée de vie) en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="44eef-111">Therefore, you only pay for hello job running time and hello brief idle time (time-to-live setting).</span></span>
- <span data-ttu-id="44eef-112">Vous pouvez créer un workflow à l’aide d’un pipeline Data Factory.</span><span class="sxs-lookup"><span data-stu-id="44eef-112">You can create a workflow using a Data Factory pipeline.</span></span> <span data-ttu-id="44eef-113">Par exemple, vous pouvez avoir des données de toocopy hello pipeline à partir d’un tooan de SQL Server locale stockage d’objets blob Azure, traiter les données hello en exécutant un script Hive et un script Pig sur un cluster HDInsight Hadoop de la demande.</span><span class="sxs-lookup"><span data-stu-id="44eef-113">For example, you can have hello pipeline toocopy data from an on-premises SQL Server tooan Azure blob storage, process hello data by running a Hive script and a Pig script on an on-demand HDInsight Hadoop cluster.</span></span> <span data-ttu-id="44eef-114">Ensuite, copiez hello résultat données tooan Azure SQL Data Warehouse pour tooconsume d’applications BI.</span><span class="sxs-lookup"><span data-stu-id="44eef-114">Then, copy hello result data tooan Azure SQL Data Warehouse for BI applications tooconsume.</span></span>
- <span data-ttu-id="44eef-115">Vous pouvez planifier hello workflow toorun régulièrement (horaire, quotidienne, hebdomadaire, mensuelle, etc.).</span><span class="sxs-lookup"><span data-stu-id="44eef-115">You can schedule hello workflow toorun periodically (hourly, daily, weekly, monthly, etc.).</span></span>

<span data-ttu-id="44eef-116">Dans Azure Data Factory, une fabrique de données peut comporter un ou plusieurs pipelines de données.</span><span class="sxs-lookup"><span data-stu-id="44eef-116">In Azure Data Factory, a data factory can have one or more data pipelines.</span></span> <span data-ttu-id="44eef-117">Un pipeline de données comprend une ou plusieurs activités.</span><span class="sxs-lookup"><span data-stu-id="44eef-117">A data pipeline has one or more activities.</span></span> <span data-ttu-id="44eef-118">Il existe deux types d’activités : les [activités de déplacement des données](../data-factory/data-factory-data-movement-activities.md) et les [activités de transformation des données](../data-factory/data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="44eef-118">There are two types of activities: [Data Movement Activities](../data-factory/data-factory-data-movement-activities.md) and [Data Transformation Activities](../data-factory/data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="44eef-119">Vous utilisez le déplacement des activités (actuellement, seule l’activité copie) toomove de données à partir d’un magasin de données de destination source données magasin tooa.</span><span class="sxs-lookup"><span data-stu-id="44eef-119">You use data movement activities (currently, only Copy Activity) toomove data from a source data store tooa destination data store.</span></span> <span data-ttu-id="44eef-120">Vous utilisez la transformation activités tootransform/processus de données.</span><span class="sxs-lookup"><span data-stu-id="44eef-120">You use data transformation activities tootransform/process data.</span></span> <span data-ttu-id="44eef-121">Activité de la ruche de HDInsight est une des activités de transformation hello pris en charge par la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="44eef-121">HDInsight Hive Activity is one of hello transformation activities supported by Data Factory.</span></span> <span data-ttu-id="44eef-122">Vous utilisez l’activité de transformation Hive hello dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="44eef-122">You use hello Hive transformation activity in this tutorial.</span></span>

<span data-ttu-id="44eef-123">Vous pouvez configurer un toouse d’activité hive votre propre cluster HDInsight Hadoop ou un cluster de HDInsight Hadoop à la demande.</span><span class="sxs-lookup"><span data-stu-id="44eef-123">You can configure a hive activity toouse your own HDInsight Hadoop cluster or an on-demand HDInsight Hadoop cluster.</span></span> <span data-ttu-id="44eef-124">Dans ce didacticiel, hello activité Hive dans le pipeline de fabrique de données hello est toouse configuré un cluster de HDInsight à la demande.</span><span class="sxs-lookup"><span data-stu-id="44eef-124">In this tutorial, hello Hive activity in hello data factory pipeline is configured toouse an on-demand HDInsight cluster.</span></span> <span data-ttu-id="44eef-125">Par conséquent, lorsque l’activité hello exécute tooprocess une tranche de données, voici ce qui se passe :</span><span class="sxs-lookup"><span data-stu-id="44eef-125">Therefore, when hello activity runs tooprocess a data slice, here is what happens:</span></span>

1. <span data-ttu-id="44eef-126">Un cluster HDInsight Hadoop est automatiquement créé pour la tranche hello juste-à-temps tooprocess.</span><span class="sxs-lookup"><span data-stu-id="44eef-126">A HDInsight Hadoop cluster is automatically created for you just-in-time tooprocess hello slice.</span></span>  
2. <span data-ttu-id="44eef-127">les données d’entrée Hello sont traitées en exécutant un script HiveQL sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="44eef-127">hello input data is processed by running a HiveQL script on hello cluster.</span></span>
3. <span data-ttu-id="44eef-128">Hello cluster HDInsight Hadoop est supprimé après le traitement de hello est terminé et cluster de hello est inactive pour durée hello configuré (paramètre de la propriété timeToLive).</span><span class="sxs-lookup"><span data-stu-id="44eef-128">hello HDInsight Hadoop cluster is deleted after hello processing is complete and hello cluster is idle for hello configured amount of time (timeToLive setting).</span></span> <span data-ttu-id="44eef-129">Si la tranche de données suivante hello est disponible pour le traitement avec dans ce délai d’inactivité de la propriété timeToLive, hello même cluster est utilisé tooprocess hello tranche.</span><span class="sxs-lookup"><span data-stu-id="44eef-129">If hello next data slice is available for processing with in this timeToLive idle time, hello same cluster is used tooprocess hello slice.</span></span>  

<span data-ttu-id="44eef-130">Dans ce didacticiel, hello script HiveQL associé hello ruche activité exécute hello suivant des actions :</span><span class="sxs-lookup"><span data-stu-id="44eef-130">In this tutorial, hello HiveQL script associated with hello hive activity performs hello following actions:</span></span>

1. <span data-ttu-id="44eef-131">Crée une table externe références hello des données de journal web brut stockées dans un stockage d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="44eef-131">Creates an external table that references hello raw web log data stored in an Azure Blob storage.</span></span>
2. <span data-ttu-id="44eef-132">Données brutes du hello partitions par année et mois.</span><span class="sxs-lookup"><span data-stu-id="44eef-132">Partitions hello raw data by year and month.</span></span>
3. <span data-ttu-id="44eef-133">Magasins hello les données partitionnées dans hello stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="44eef-133">Stores hello partitioned data in hello Azure blob storage.</span></span>

<span data-ttu-id="44eef-134">Dans ce didacticiel, hello script HiveQL associé hello ruche activité crée une table externe références hello les données de journal web brutes stockées Bonjour stockage d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="44eef-134">In this tutorial, hello HiveQL script associated with hello hive activity creates an external table that references hello raw web log data stored in hello Azure Blob Storage.</span></span> <span data-ttu-id="44eef-135">Voici les lignes d’exemple hello pour chaque mois dans le fichier d’entrée de hello.</span><span class="sxs-lookup"><span data-stu-id="44eef-135">Here are hello sample rows for each month in hello input file.</span></span>

```
2014-01-01,02:01:09,SAMPLEWEBSITE,GET,/blogposts/mvc4/step2.png,X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,53175,871
2014-02-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
2014-03-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
```

<span data-ttu-id="44eef-136">partitions de script HiveQL Hello hello données brutes par année et mois.</span><span class="sxs-lookup"><span data-stu-id="44eef-136">hello HiveQL script partitions hello raw data by year and month.</span></span> <span data-ttu-id="44eef-137">Il crée trois dossiers de sortie en fonction de la saisie de hello.</span><span class="sxs-lookup"><span data-stu-id="44eef-137">It creates three output folders based on hello previous input.</span></span> <span data-ttu-id="44eef-138">Chaque dossier contient un fichier avec les entrées correspondant à chaque mois.</span><span class="sxs-lookup"><span data-stu-id="44eef-138">Each folder contains a file with entries from each month.</span></span>

```
adfgetstarted/partitioneddata/year=2014/month=1/000000_0
adfgetstarted/partitioneddata/year=2014/month=2/000000_0
adfgetstarted/partitioneddata/year=2014/month=3/000000_0
```

<span data-ttu-id="44eef-139">Pour obtenir la liste des activités de transformation de données de fabrique de données dans l’activité de tooHive addition, consultez [transformer et analyser à l’aide d’Azure Data Factory](../data-factory/data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="44eef-139">For a list of Data Factory data transformation activities in addition tooHive activity, see [Transform and analyze using Azure Data Factory](../data-factory/data-factory-data-transformation-activities.md).</span></span>

> [!NOTE]
> <span data-ttu-id="44eef-140">Actuellement, vous ne pouvez créer qu’un cluster HDInsight version 3.2 à partir d’Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="44eef-140">Currently, you can only create HDInsight cluster version 3.2 from Azure Data Factory.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44eef-141">Composants requis</span><span class="sxs-lookup"><span data-stu-id="44eef-141">Prerequisites</span></span>
<span data-ttu-id="44eef-142">Avant de suivre les instructions hello dans cet article, vous devez disposer de hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="44eef-142">Before you begin hello instructions in this article, you must have hello following items:</span></span>

* <span data-ttu-id="44eef-143">[Abonnement Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="44eef-143">[Azure subscription](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="44eef-144">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="44eef-144">Azure PowerShell.</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

### <a name="prepare-storage-account"></a><span data-ttu-id="44eef-145">Préparer le compte de stockage</span><span class="sxs-lookup"><span data-stu-id="44eef-145">Prepare storage account</span></span>
<span data-ttu-id="44eef-146">Vous pouvez utiliser des comptes de stockage toothree dans ce scénario :</span><span class="sxs-lookup"><span data-stu-id="44eef-146">You can use up toothree storage accounts in this scenario:</span></span>

- <span data-ttu-id="44eef-147">compte de stockage par défaut pour le cluster HDInsight de hello</span><span class="sxs-lookup"><span data-stu-id="44eef-147">default storage account for hello HDInsight cluster</span></span>
- <span data-ttu-id="44eef-148">compte de stockage pour les données d’entrée hello</span><span class="sxs-lookup"><span data-stu-id="44eef-148">storage account for hello input data</span></span>
- <span data-ttu-id="44eef-149">compte de stockage pour les données de sortie hello</span><span class="sxs-lookup"><span data-stu-id="44eef-149">storage account for hello output data</span></span>

<span data-ttu-id="44eef-150">didacticiel de hello toosimplify, vous utilisez un compte tooserve hello trois des fins de stockage.</span><span class="sxs-lookup"><span data-stu-id="44eef-150">toosimplify hello tutorial, you use one storage account tooserve hello three purposes.</span></span> <span data-ttu-id="44eef-151">Bonjour Azure PowerShell exemple de script dans cette section effectue hello tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="44eef-151">hello Azure PowerShell sample script found in this section performs hello following tasks:</span></span>

1. <span data-ttu-id="44eef-152">Ouvrez une session dans tooAzure.</span><span class="sxs-lookup"><span data-stu-id="44eef-152">Log in tooAzure.</span></span>
2. <span data-ttu-id="44eef-153">Création d’un groupe de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="44eef-153">Create an Azure resource group.</span></span>
3. <span data-ttu-id="44eef-154">Création d’un compte Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="44eef-154">Create an Azure Storage account.</span></span>
4. <span data-ttu-id="44eef-155">Créer un conteneur d’objets Blob dans le compte de stockage hello</span><span class="sxs-lookup"><span data-stu-id="44eef-155">Create a Blob container in hello storage account</span></span>
5. <span data-ttu-id="44eef-156">Copiez hello suivant le conteneur d’objets Blob toohello deux fichiers :</span><span class="sxs-lookup"><span data-stu-id="44eef-156">Copy hello following two files toohello Blob container:</span></span>

   * <span data-ttu-id="44eef-157">Fichier d’entrée : [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log)</span><span class="sxs-lookup"><span data-stu-id="44eef-157">Input data file: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log)</span></span>
   * <span data-ttu-id="44eef-158">Script HiveQL : [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql)</span><span class="sxs-lookup"><span data-stu-id="44eef-158">HiveQL script: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql)</span></span>

     <span data-ttu-id="44eef-159">Les deux fichiers sont stockés dans un conteneur d’objets blob public.</span><span class="sxs-lookup"><span data-stu-id="44eef-159">Both files are stored in a public Blob container.</span></span>


<span data-ttu-id="44eef-160">**tooprepare hello stockage et copier hello des fichiers à l’aide d’Azure PowerShell :**</span><span class="sxs-lookup"><span data-stu-id="44eef-160">**tooprepare hello storage and copy hello files using Azure PowerShell:**</span></span>
> [!IMPORTANT]
> <span data-ttu-id="44eef-161">Spécifiez les noms de groupe de ressources Azure hello et de compte de stockage Azure hello qui sera créé par le script de hello.</span><span class="sxs-lookup"><span data-stu-id="44eef-161">Specify names for hello Azure resource group and hello Azure storage account that will be created by hello script.</span></span>
> <span data-ttu-id="44eef-162">Notez **nom de groupe de ressources**, **nom de compte de stockage**, et **clé de compte de stockage** générées par le script de hello.</span><span class="sxs-lookup"><span data-stu-id="44eef-162">Write down **resource group name**, **storage account name**, and **storage account key** outputted by hello script.</span></span> <span data-ttu-id="44eef-163">Vous avez besoin dans la section suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="44eef-163">You need them in hello next section.</span></span>

```powershell
$resourceGroupName = "<Azure Resource Group Name>"
$storageAccountName = "<Azure Storage Account Name>"
$location = "East US 2"

$sourceStorageAccountName = "hditutorialdata"  
$sourceContainerName = "adfhiveactivity"

$destStorageAccountName = $storageAccountName
$destContainerName = "adfgetstarted" # don't change this value.

####################################
# Connect tooAzure
####################################
#region - Connect tooAzure subscription
Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
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

Write-host "`nYou will use hello following values:" -ForegroundColor Green
write-host "`nResource group name: $resourceGroupName"
Write-host "Storage Account Name: $destStorageAccountName"
write-host "Storage Account Key: $destStorageAccountKey"

Write-host "`nScript completed" -ForegroundColor Green
```

<span data-ttu-id="44eef-164">Si vous avez besoin d’aide avec le script PowerShell de hello, consultez [Using hello Azure PowerShell avec le stockage Azure](../storage/common/storage-powershell-guide-full.md).</span><span class="sxs-lookup"><span data-stu-id="44eef-164">If you need help with hello PowerShell script, see [Using hello Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md).</span></span> <span data-ttu-id="44eef-165">Si vous le souhaitez toouse CLI d’Azure, consultez hello [annexe](#appendix) section pourquoi les script CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="44eef-165">If you like toouse Azure CLI instead, see hello [Appendix](#appendix) section for hello Azure CLI script.</span></span>

<span data-ttu-id="44eef-166">**tooexamine hello stockage compte et hello le contenu**</span><span class="sxs-lookup"><span data-stu-id="44eef-166">**tooexamine hello storage account and hello contents**</span></span>

1. <span data-ttu-id="44eef-167">Ouverture de session toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="44eef-167">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="44eef-168">Cliquez sur **groupes de ressources** sur le volet gauche de hello.</span><span class="sxs-lookup"><span data-stu-id="44eef-168">Click **Resource groups** on hello left pane.</span></span>
3. <span data-ttu-id="44eef-169">Double-cliquez sur le nom de groupe de ressources hello que vous avez créé dans votre script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="44eef-169">Double-click hello resource group name you created in your PowerShell script.</span></span> <span data-ttu-id="44eef-170">Utilisez le filtre de hello si vous avez trop de groupes de ressources répertoriées.</span><span class="sxs-lookup"><span data-stu-id="44eef-170">Use hello filter if you have too many resource groups listed.</span></span>
4. <span data-ttu-id="44eef-171">Sur hello **ressources** vignette, doit avoir une seule ressource répertoriée, sauf si vous partagez un groupe de ressources hello avec d’autres projets.</span><span class="sxs-lookup"><span data-stu-id="44eef-171">On hello **Resources** tile, you shall have one resource listed unless you share hello resource group with other projects.</span></span> <span data-ttu-id="44eef-172">Cette ressource est un compte de stockage hello portant hello, que vous avez spécifié précédemment.</span><span class="sxs-lookup"><span data-stu-id="44eef-172">That resource is hello storage account with hello name you specified earlier.</span></span> <span data-ttu-id="44eef-173">Cliquez sur le nom de compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="44eef-173">Click hello storage account name.</span></span>
5. <span data-ttu-id="44eef-174">Cliquez sur hello **BLOB** vignettes.</span><span class="sxs-lookup"><span data-stu-id="44eef-174">Click hello **Blobs** tiles.</span></span>
6. <span data-ttu-id="44eef-175">Cliquez sur hello **adfgetstarted** conteneur.</span><span class="sxs-lookup"><span data-stu-id="44eef-175">Click hello **adfgetstarted** container.</span></span> <span data-ttu-id="44eef-176">Vous voyez deux dossiers : **inputdata** et **script**.</span><span class="sxs-lookup"><span data-stu-id="44eef-176">You see two folders: **inputdata** and **script**.</span></span>
7. <span data-ttu-id="44eef-177">Ouvrez le dossier de hello et vérifiez si hello dans les dossiers hello.</span><span class="sxs-lookup"><span data-stu-id="44eef-177">Open hello folder and check hello files in hello folders.</span></span> <span data-ttu-id="44eef-178">Hello inputdata contient le fichier input.log de hello avec les données d’entrée et le dossier de scripts hello contient le fichier de script HiveQL hello.</span><span class="sxs-lookup"><span data-stu-id="44eef-178">hello inputdata contains hello input.log file with input data and hello script folder contains hello HiveQL script file.</span></span>

## <a name="create-a-data-factory-using-resource-manager-template"></a><span data-ttu-id="44eef-179">Créer une fabrique de données à l’aide du modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="44eef-179">Create a data factory using Resource Manager template</span></span>
<span data-ttu-id="44eef-180">Compte de stockage hello, les données d’entrée hello et hello script HiveQL préparé, vous êtes prêt toocreate une fabrique de données Azure.</span><span class="sxs-lookup"><span data-stu-id="44eef-180">With hello storage account, hello input data, and hello HiveQL script prepared, you are ready toocreate an Azure data factory.</span></span> <span data-ttu-id="44eef-181">Il existe plusieurs méthodes pour créer la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="44eef-181">There are several methods for creating data factory.</span></span> <span data-ttu-id="44eef-182">Dans ce didacticiel, vous créez une fabrique de données en déployant un modèle Azure Resource Manager à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="44eef-182">In this tutorial, you create a data factory by deploying an Azure Resource Manager template using hello Azure portal.</span></span> <span data-ttu-id="44eef-183">Vous pouvez également déployer un modèle Resource Manager en utilisant [l’interface de ligne de commande Azure](../azure-resource-manager/resource-group-template-deploy-cli.md) et [Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span><span class="sxs-lookup"><span data-stu-id="44eef-183">You can also deploy a Resource Manager template by using [Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md) and [Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span></span> <span data-ttu-id="44eef-184">Pour les autres méthodes de création de fabriques de données, consultez la page [Didacticiel : créer votre première fabrique de données](../data-factory/data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="44eef-184">For other data factory creation methods, see [Tutorial: Build your first data factory](../data-factory/data-factory-build-your-first-pipeline.md).</span></span>

1. <span data-ttu-id="44eef-185">Cliquez sur hello suivant toosign image dans tooAzure et modèle du Gestionnaire de ressources ouvrir hello Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="44eef-185">Click hello following image toosign in tooAzure and open hello Resource Manager template in hello Azure portal.</span></span> <span data-ttu-id="44eef-186">modèle de Hello se trouve dans https://hditutorialdata.blob.core.windows.net/adfhiveactivity/data-factory-hdinsight-on-demand.json.</span><span class="sxs-lookup"><span data-stu-id="44eef-186">hello template is located at https://hditutorialdata.blob.core.windows.net/adfhiveactivity/data-factory-hdinsight-on-demand.json.</span></span> <span data-ttu-id="44eef-187">Consultez hello [des entités de fabrique de données dans le modèle de hello](#data-factory-entities-in-the-template) section pour plus d’informations sur les entités définies dans le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="44eef-187">See hello [Data Factory entities in hello template](#data-factory-entities-in-the-template) section for detailed information about entities defined in hello template.</span></span> 

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fadfhiveactivity%2Fdata-factory-hdinsight-on-demand.json" target="_blank"><img src="./media/hdinsight-hadoop-create-linux-clusters-adf/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. <span data-ttu-id="44eef-188">Sélectionnez **utiliser l’existant** option hello **groupe de ressources** paramètre et le nom hello sélectionnez hello du groupe de ressources créé à l’étape précédente de hello (à l’aide du script PowerShell).</span><span class="sxs-lookup"><span data-stu-id="44eef-188">Select **Use existing** option for hello **Resource group** setting, and select hello name of hello resource group you created in hello previous step (using PowerShell script).</span></span>
3. <span data-ttu-id="44eef-189">Entrez un nom pour la fabrique de données hello (**nom de la fabrique de données**).</span><span class="sxs-lookup"><span data-stu-id="44eef-189">Enter a name for hello data factory (**Data Factory Name**).</span></span> <span data-ttu-id="44eef-190">Ce nom doit être globalement unique.</span><span class="sxs-lookup"><span data-stu-id="44eef-190">This name must be globally unique.</span></span>
4. <span data-ttu-id="44eef-191">Entrez hello **nom de compte de stockage** et **clé de compte de stockage** notés à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="44eef-191">Enter hello **storage account name** and **storage account key** you wrote down in hello previous step.</span></span>
5. <span data-ttu-id="44eef-192">Sélectionnez **J’accepte les conditions générales toohello** mentionnées ci-dessus après avoir parcouru **termes et conditions**.</span><span class="sxs-lookup"><span data-stu-id="44eef-192">Select **I agree toohello terms and conditions** stated above after reading through **terms and conditions**.</span></span>
6. <span data-ttu-id="44eef-193">Sélectionnez **toodashboard du code confidentiel** option.</span><span class="sxs-lookup"><span data-stu-id="44eef-193">Select **Pin toodashboard** option.</span></span>
6. <span data-ttu-id="44eef-194">Cliquez sur **Acheter/Créer**.</span><span class="sxs-lookup"><span data-stu-id="44eef-194">Click **Purchase/Create**.</span></span> <span data-ttu-id="44eef-195">Vous voyez une vignette sur hello tableau de bord appelé **déploiement d’un modèle de déploiement**.</span><span class="sxs-lookup"><span data-stu-id="44eef-195">You see a tile on hello Dashboard called **Deploying Template deployment**.</span></span> <span data-ttu-id="44eef-196">Attendez que hello **groupe de ressources** panneau pour votre groupe de ressources s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="44eef-196">Wait until hello **Resource group** blade for your resource group opens.</span></span> <span data-ttu-id="44eef-197">Vous pouvez également cliquer sur la vignette hello intitulée comme panneau de votre groupe de ressources groupe nom tooopen hello ressource.</span><span class="sxs-lookup"><span data-stu-id="44eef-197">You can also click hello tile titled as your resource group name tooopen hello resource group blade.</span></span>
6. <span data-ttu-id="44eef-198">Si le panneau des ressources de groupe hello n’est pas déjà ouvert, cliquez sur groupe de ressources hello vignette tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="44eef-198">Click hello tile tooopen hello resource group if hello resource group blade is not already open.</span></span> <span data-ttu-id="44eef-199">Maintenant que vous allez voir une ressource de fabrique de données plus répertoriés en outre toohello des ressources de compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="44eef-199">Now you shall see one more data factory resource listed in addition toohello storage account resource.</span></span>
7. <span data-ttu-id="44eef-200">Cliquez sur nom hello votre fabrique de données (valeur que vous avez spécifié pour hello **nom de la fabrique de données** paramètre).</span><span class="sxs-lookup"><span data-stu-id="44eef-200">Click hello name of your data factory (value you specified for hello **Data Factory Name** parameter).</span></span>
8. <span data-ttu-id="44eef-201">Dans le panneau de la fabrique de données hello, cliquez sur hello **diagramme** vignette.</span><span class="sxs-lookup"><span data-stu-id="44eef-201">In hello Data Factory blade, click hello **Diagram** tile.</span></span> <span data-ttu-id="44eef-202">diagramme de Hello montre une activité avec un jeu de données d’entrée et un jeu de données de sortie :</span><span class="sxs-lookup"><span data-stu-id="44eef-202">hello diagram shows one activity with an input dataset, and an output dataset:</span></span>

    ![Diagramme du pipeline d’activité Hive à la demande HDInsight avec Azure Data Factory](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-pipeline-diagram.png)

    <span data-ttu-id="44eef-204">les noms de Hello sont définis dans le modèle de gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="44eef-204">hello names are defined in hello Resource Manager template.</span></span>
9. <span data-ttu-id="44eef-205">Double-cliquez sur **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="44eef-205">Double-click **AzureBlobOutput**.</span></span>
10. <span data-ttu-id="44eef-206">Sur hello **récents mis à jour les tranches**, vous devez voir un secteur.</span><span class="sxs-lookup"><span data-stu-id="44eef-206">On hello **Recent updated slices**, you shall see one slice.</span></span> <span data-ttu-id="44eef-207">Si l’état de hello est **en cours d’exécution**, patientez jusqu'à ce qu’il a été modifié trop**prêt**.</span><span class="sxs-lookup"><span data-stu-id="44eef-207">If hello status is **In progress**, wait until it is changed too**Ready**.</span></span> <span data-ttu-id="44eef-208">Cela prend généralement environ **20 minutes** toocreate un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="44eef-208">It usually takes about **20 minutes** toocreate an HDInsight cluster.</span></span>

### <a name="check-hello-data-factory-output"></a><span data-ttu-id="44eef-209">Vérifier la sortie de fabrique de données hello</span><span class="sxs-lookup"><span data-stu-id="44eef-209">Check hello data factory output</span></span>

1. <span data-ttu-id="44eef-210">Utilisez hello même procédure dans hello dernière session toocheck hello conteneurs du conteneur d’adfgetstarted hello.</span><span class="sxs-lookup"><span data-stu-id="44eef-210">Use hello same procedure in hello last session toocheck hello containers of hello adfgetstarted container.</span></span> <span data-ttu-id="44eef-211">Il existe deux nouveaux conteneurs en outre trop**adfgetsarted**:</span><span class="sxs-lookup"><span data-stu-id="44eef-211">There are two new containers in addition too**adfgetsarted**:</span></span>

   * <span data-ttu-id="44eef-212">Un conteneur portant le nom qui suit le modèle de hello : `adf<yourdatafactoryname>-linkedservicename-datetimestamp`.</span><span class="sxs-lookup"><span data-stu-id="44eef-212">A container with name that follows hello pattern: `adf<yourdatafactoryname>-linkedservicename-datetimestamp`.</span></span> <span data-ttu-id="44eef-213">Ce conteneur est un conteneur par défaut de hello pour le cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="44eef-213">This container is hello default container for hello HDInsight cluster.</span></span>
   * <span data-ttu-id="44eef-214">adfjobs : ce conteneur est le conteneur hello pour les journaux de travaux hello ADF.</span><span class="sxs-lookup"><span data-stu-id="44eef-214">adfjobs: This container is hello container for hello ADF job logs.</span></span>

     <span data-ttu-id="44eef-215">sortie de fabrique de données Hello est stockée dans **afgetstarted** que vous avez configurés dans le modèle de gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="44eef-215">hello data factory output is stored in **afgetstarted** as you configured in hello Resource Manager template.</span></span>
2. <span data-ttu-id="44eef-216">Cliquez sur **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="44eef-216">Click **adfgetstarted**.</span></span>
3. <span data-ttu-id="44eef-217">Double-cliquez sur **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="44eef-217">Double-click **partitioneddata**.</span></span> <span data-ttu-id="44eef-218">Vous voyez un **année = 2014** dossier, car tous les journaux de web hello date année 2014.</span><span class="sxs-lookup"><span data-stu-id="44eef-218">You see a **year=2014** folder because all hello web logs are dated in year 2014.</span></span>

    ![Sortie du pipeline d’activité Hive à la demande HDInsight avec Azure Data Factory](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-year.png)

    <span data-ttu-id="44eef-220">Si vous affichez la liste de hello, vous devez voir trois dossiers pour janvier, février et mars.</span><span class="sxs-lookup"><span data-stu-id="44eef-220">If you drill down hello list, you shall see three folders for January, February, and March.</span></span> <span data-ttu-id="44eef-221">Il y a un journal pour chaque mois.</span><span class="sxs-lookup"><span data-stu-id="44eef-221">And there is a log for each month.</span></span>

    ![Sortie du pipeline d’activité Hive à la demande HDInsight avec Azure Data Factory](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-month.png)

## <a name="data-factory-entities-in-hello-template"></a><span data-ttu-id="44eef-223">Entités de fabrique de données dans le modèle de hello</span><span class="sxs-lookup"><span data-stu-id="44eef-223">Data Factory entities in hello template</span></span>
<span data-ttu-id="44eef-224">Voici comment le modèle de gestionnaire de ressources du niveau supérieur hello pour une fabrique de données ressemble à :</span><span class="sxs-lookup"><span data-stu-id="44eef-224">Here is how hello top-level Resource Manager template for a data factory looks like:</span></span>

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

### <a name="define-data-factory"></a><span data-ttu-id="44eef-225">Définir une fabrique de données</span><span class="sxs-lookup"><span data-stu-id="44eef-225">Define data factory</span></span>
<span data-ttu-id="44eef-226">Vous définissez une fabrique de données dans le modèle de gestionnaire de ressources hello comme indiqué dans hello suivant l’exemple :</span><span class="sxs-lookup"><span data-stu-id="44eef-226">You define a data factory in hello Resource Manager template as shown in hello following sample:</span></span>  

```json
"resources": [
{
    "name": "[parameters('dataFactoryName')]",
    "apiVersion": "[variables('apiVersion')]",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "westus",
}
```
<span data-ttu-id="44eef-227">Hello dataFactoryName est le nom hello hello fabrique de données que vous spécifiez lorsque vous déployez le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="44eef-227">hello dataFactoryName is hello name of hello data factory you specify when you deploy hello template.</span></span> <span data-ttu-id="44eef-228">Fabrique de données est uniquement pris en charge dans les régions est des États-Unis, ouest des États-Unis et Europe du Nord hello.</span><span class="sxs-lookup"><span data-stu-id="44eef-228">Data factory is currently only supported in hello East US, West US, and North Europe regions.</span></span>

### <a name="defining-entities-within-hello-data-factory"></a><span data-ttu-id="44eef-229">Définition des entités au sein de la fabrique de données hello</span><span class="sxs-lookup"><span data-stu-id="44eef-229">Defining entities within hello data factory</span></span>
<span data-ttu-id="44eef-230">Hello des entités de fabrique de données suivantes sont définies dans le modèle JSON hello :</span><span class="sxs-lookup"><span data-stu-id="44eef-230">hello following Data Factory entities are defined in hello JSON template:</span></span>

* [<span data-ttu-id="44eef-231">Service lié Azure Storage</span><span class="sxs-lookup"><span data-stu-id="44eef-231">Azure Storage linked service</span></span>](#azure-storage-linked-service)
* [<span data-ttu-id="44eef-232">Service lié à la demande HDInsight</span><span class="sxs-lookup"><span data-stu-id="44eef-232">HDInsight on-demand linked service</span></span>](#hdinsight-on-demand-linked-service)
* [<span data-ttu-id="44eef-233">Jeu de données d'entrée d'objet Blob Azure</span><span class="sxs-lookup"><span data-stu-id="44eef-233">Azure blob input dataset</span></span>](#azure-blob-input-dataset)
* [<span data-ttu-id="44eef-234">Jeu de données de sortie d’objet Blob Azure</span><span class="sxs-lookup"><span data-stu-id="44eef-234">Azure blob output dataset</span></span>](#azure-blob-output-dataset)
* [<span data-ttu-id="44eef-235">Pipeline de données avec une activité de copie</span><span class="sxs-lookup"><span data-stu-id="44eef-235">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="44eef-236">Service lié Azure Storage</span><span class="sxs-lookup"><span data-stu-id="44eef-236">Azure Storage linked service</span></span>
<span data-ttu-id="44eef-237">Hello le stockage Azure lié à des liens de service votre fabrique de données toohello compte stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="44eef-237">hello Azure Storage linked service links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="44eef-238">Dans ce didacticiel, hello même compte de stockage est utilisé en tant que compte de stockage HDInsight hello par défaut, le stockage de données d’entrée et stockage des données de sortie.</span><span class="sxs-lookup"><span data-stu-id="44eef-238">In this tutorial, hello same storage account is used as hello default HDInsight storage account, input data storage, and output data storage.</span></span> <span data-ttu-id="44eef-239">Par conséquent, vous ne définissez qu’un seul service lié Stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="44eef-239">Therefore, you define only one Azure Storage linked service.</span></span> <span data-ttu-id="44eef-240">Dans la définition de service lié de hello, vous spécifiez le nom de hello et la clé de votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="44eef-240">In hello linked service definition, you specify hello name and key of your Azure storage account.</span></span> <span data-ttu-id="44eef-241">Consultez [service lié Azure Storage](../data-factory/data-factory-azure-blob-connector.md#azure-storage-linked-service) pour plus d’informations sur JSON propriétés utilisées toodefine un stockage Azure le service lié.</span><span class="sxs-lookup"><span data-stu-id="44eef-241">See [Azure Storage linked service](../data-factory/data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used toodefine an Azure Storage linked service.</span></span>

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
<span data-ttu-id="44eef-242">Hello **connectionString** utilise hello paramètres storageAccountName et storageAccountKey.</span><span class="sxs-lookup"><span data-stu-id="44eef-242">hello **connectionString** uses hello storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="44eef-243">Vous spécifiez des valeurs pour ces paramètres lors du déploiement de modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="44eef-243">You specify values for these parameters while deploying hello template.</span></span>  

#### <a name="hdinsight-on-demand-linked-service"></a><span data-ttu-id="44eef-244">Service lié à la demande HDInsight</span><span class="sxs-lookup"><span data-stu-id="44eef-244">HDInsight on-demand linked service</span></span>
<span data-ttu-id="44eef-245">Bonjour à la demande HDInsight lié définition de service, vous spécifiez les valeurs des paramètres de configuration qui sont utilisés par hello Data Factory service toocreate un HDInsight Hadoop de cluster lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="44eef-245">In hello on-demand HDInsight linked service definition, you specify values for configuration parameters that are used by hello Data Factory service toocreate a HDInsight Hadoop cluster at runtime.</span></span> <span data-ttu-id="44eef-246">Consultez [services liés de calcul](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article pour plus d’informations sur JSON propriétés utilisées toodefine un service lié à la demande de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="44eef-246">See [Compute linked services](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article for details about JSON properties used toodefine an HDInsight on-demand linked service.</span></span>  

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
<span data-ttu-id="44eef-247">Hello Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="44eef-247">Note hello following points:</span></span>

* <span data-ttu-id="44eef-248">Hello Data Factory crée un **basés sur Linux** cluster HDInsight pour vous.</span><span class="sxs-lookup"><span data-stu-id="44eef-248">hello Data Factory creates a **Linux-based** HDInsight cluster for you.</span></span>
* <span data-ttu-id="44eef-249">Hello cluster HDInsight Hadoop est créé dans hello même région que le compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="44eef-249">hello HDInsight Hadoop cluster is created in hello same region as hello storage account.</span></span>
* <span data-ttu-id="44eef-250">Hello d’avis *timeToLive* paramètre.</span><span class="sxs-lookup"><span data-stu-id="44eef-250">Notice hello *timeToLive* setting.</span></span> <span data-ttu-id="44eef-251">fabrique de données Hello supprime le cluster de hello automatiquement une fois le cluster de hello est inactif pendant 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="44eef-251">hello data factory deletes hello cluster automatically after hello cluster is being idle for 30 minutes.</span></span>
* <span data-ttu-id="44eef-252">Hello HDInsight cluster crée un **conteneur par défaut** dans le stockage blob hello spécifié dans hello JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="44eef-252">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="44eef-253">HDInsight ne supprime pas ce conteneur lorsque le cluster de hello est supprimé.</span><span class="sxs-lookup"><span data-stu-id="44eef-253">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="44eef-254">Ce comportement est normal.</span><span class="sxs-lookup"><span data-stu-id="44eef-254">This behavior is by design.</span></span> <span data-ttu-id="44eef-255">Service lié HDInsight à la demande un cluster HDInsight est créé chaque fois qu’une tranche doit toobe traité sauf s’il existe un cluster dynamique existant (**timeToLive**) et est supprimé quand le traitement de hello est effectué.</span><span class="sxs-lookup"><span data-stu-id="44eef-255">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice needs toobe processed unless there is an existing live cluster (**timeToLive**) and is deleted when hello processing is done.</span></span>

<span data-ttu-id="44eef-256">Pour plus d’informations, voir [Service lié à la demande Azure HDInsight](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="44eef-256">See [On-demand HDInsight Linked Service](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="44eef-257">Comme un nombre croissant de tranches sont traitées, vous voyez un grand nombre de conteneurs dans votre stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="44eef-257">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="44eef-258">Si vous ne devez pas les pour la résolution des problèmes de travaux de hello, vous souhaiterez peut-être toodelete les coûts de stockage tooreduce hello.</span><span class="sxs-lookup"><span data-stu-id="44eef-258">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="44eef-259">les noms de ces conteneurs Hello suivent un modèle : « adf**yourdatafactoryname**-**linkedservicename**- datetimestamp ».</span><span class="sxs-lookup"><span data-stu-id="44eef-259">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="44eef-260">Utiliser des outils tels que [Explorateur de stockage Microsoft](http://storageexplorer.com/) stockage d’objets blob des conteneurs de toodelete dans votre Azure.</span><span class="sxs-lookup"><span data-stu-id="44eef-260">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

#### <a name="azure-blob-input-dataset"></a><span data-ttu-id="44eef-261">Jeu de données d'entrée d'objet Blob Azure</span><span class="sxs-lookup"><span data-stu-id="44eef-261">Azure blob input dataset</span></span>
<span data-ttu-id="44eef-262">Dans la définition du jeu de données d’entrée hello, vous spécifiez les noms de conteneur d’objets blob, de dossier et de fichier qui contient les données d’entrée hello hello.</span><span class="sxs-lookup"><span data-stu-id="44eef-262">In hello input dataset definition, you specify hello names of blob container, folder, and file that contains hello input data.</span></span> <span data-ttu-id="44eef-263">Consultez [propriétés de jeu de données d’objets Blob Azure](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) pour plus d’informations sur les propriétés utilisées de JSON toodefine un jeu de données d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="44eef-263">See [Azure Blob dataset properties](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure Blob dataset.</span></span>

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

<span data-ttu-id="44eef-264">Notez hello suivant des paramètres spécifiques dans la définition de JSON hello :</span><span class="sxs-lookup"><span data-stu-id="44eef-264">Notice hello following specific settings in hello JSON definition:</span></span>

```json
"fileName": "input.log",
"folderPath": "adfgetstarted/inputdata",
```

#### <a name="azure-blob-output-dataset"></a><span data-ttu-id="44eef-265">Jeu de données de sortie d’objet Blob Azure</span><span class="sxs-lookup"><span data-stu-id="44eef-265">Azure Blob output dataset</span></span>
<span data-ttu-id="44eef-266">Dans la définition de dataset de sortie hello, vous spécifiez les noms de conteneur d’objets blob et le dossier qui contient les données de sortie hello hello.</span><span class="sxs-lookup"><span data-stu-id="44eef-266">In hello output dataset definition, you specify hello names of blob container and folder that holds hello output data.</span></span> <span data-ttu-id="44eef-267">Consultez [propriétés de jeu de données d’objets Blob Azure](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) pour plus d’informations sur les propriétés utilisées de JSON toodefine un jeu de données d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="44eef-267">See [Azure Blob dataset properties](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure Blob dataset.</span></span>  

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

<span data-ttu-id="44eef-268">Hello folderPath spécifie hello chemin d’accès toohello dossier qui contient les données de sortie hello :</span><span class="sxs-lookup"><span data-stu-id="44eef-268">hello folderPath specifies hello path toohello folder that holds hello output data:</span></span>

```json
"folderPath": "adfgetstarted/partitioneddata",
```

<span data-ttu-id="44eef-269">Hello [dataset disponibilité](../data-factory/data-factory-create-datasets.md#dataset-availability) paramètre est le suivant :</span><span class="sxs-lookup"><span data-stu-id="44eef-269">hello [dataset availability](../data-factory/data-factory-create-datasets.md#dataset-availability) setting is as follows:</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "style": "EndOfInterval"
},
```

<span data-ttu-id="44eef-270">Dans Azure Data Factory, pipeline de sortie dataset disponibilité lecteurs hello.</span><span class="sxs-lookup"><span data-stu-id="44eef-270">In Azure Data Factory, output dataset availability drives hello pipeline.</span></span> <span data-ttu-id="44eef-271">Dans cet exemple, hello tranche est produite mensuelle hello dernier jour du mois (EndOfInterval).</span><span class="sxs-lookup"><span data-stu-id="44eef-271">In this example, hello slice is produced monthly on hello last day of month (EndOfInterval).</span></span> <span data-ttu-id="44eef-272">Pour plus d’informations, consultez [Planification et exécution avec Data Factory](../data-factory/data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="44eef-272">For more information, see [Data Factory Scheduling and Execution](../data-factory/data-factory-scheduling-and-execution.md).</span></span>

#### <a name="data-pipeline"></a><span data-ttu-id="44eef-273">Pipeline de données</span><span class="sxs-lookup"><span data-stu-id="44eef-273">Data pipeline</span></span>
<span data-ttu-id="44eef-274">Vous définissez un pipeline qui transforme les données en exécutant le script Hive sur un cluster Azure HDInsight à la demande.</span><span class="sxs-lookup"><span data-stu-id="44eef-274">You define a pipeline that transforms data by running Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="44eef-275">Consultez [JSON de Pipeline](../data-factory/data-factory-create-pipelines.md#pipeline-json) pour les descriptions des éléments utilisés de JSON toodefine un pipeline dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="44eef-275">See [Pipeline JSON](../data-factory/data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used toodefine a pipeline in this example.</span></span>

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

<span data-ttu-id="44eef-276">pipeline de Hello contient une activité, HDInsightHive activité.</span><span class="sxs-lookup"><span data-stu-id="44eef-276">hello pipeline contains one activity, HDInsightHive activity.</span></span> <span data-ttu-id="44eef-277">Étant donné que les dates de début et de fin appartiennent toutes deux au mois de janvier 2016, le traitement ne porte que sur les données d’un seul mois (une tranche).</span><span class="sxs-lookup"><span data-stu-id="44eef-277">As both start and end dates are in January 2016, data for only one month (a slice) is processed.</span></span> <span data-ttu-id="44eef-278">Les deux *Démarrer* et *fin* d’activité hello ont une date passée, donc hello fabrique de données traite les données pour le mois de hello immédiatement.</span><span class="sxs-lookup"><span data-stu-id="44eef-278">Both *start* and *end* of hello activity have a past date, so hello Data Factory processes data for hello month immediately.</span></span> <span data-ttu-id="44eef-279">Si la fin de hello est une date ultérieure, fabrique de données hello crée une autre tranche hello moment venu.</span><span class="sxs-lookup"><span data-stu-id="44eef-279">If hello end is a future date, hello data factory creates another slice when hello time comes.</span></span> <span data-ttu-id="44eef-280">Pour plus d’informations, consultez [Planification et exécution avec Data Factory](../data-factory/data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="44eef-280">For more information, see [Data Factory Scheduling and Execution](../data-factory/data-factory-scheduling-and-execution.md).</span></span>

## <a name="clean-up-hello-tutorial"></a><span data-ttu-id="44eef-281">Nettoyer le didacticiel de hello</span><span class="sxs-lookup"><span data-stu-id="44eef-281">Clean up hello tutorial</span></span>

### <a name="delete-hello-blob-containers-created-by-on-demand-hdinsight-cluster"></a><span data-ttu-id="44eef-282">Supprimer des conteneurs d’objets blob hello créés par cluster de HDInsight à la demande</span><span class="sxs-lookup"><span data-stu-id="44eef-282">Delete hello blob containers created by on-demand HDInsight cluster</span></span>
<span data-ttu-id="44eef-283">Service lié HDInsight à la demande un cluster HDInsight est créé chaque fois qu’une tranche doit toobe traité sauf s’il existe un cluster dynamique existant (timeToLive) ; et cluster de hello est supprimé lorsque le traitement de hello est effectué.</span><span class="sxs-lookup"><span data-stu-id="44eef-283">With on-demand HDInsight linked service, an HDInsight cluster is created every time a slice needs toobe processed unless there is an existing live cluster (timeToLive); and hello cluster is deleted when hello processing is done.</span></span> <span data-ttu-id="44eef-284">Pour chaque cluster, Azure Data Factory crée un conteneur d’objets blob dans hello stockage d’objets blob Azure utilisé comme compte de stockage par défaut hello pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="44eef-284">For each cluster, Azure Data Factory creates a blob container in hello Azure blob storage used as hello default stroage account for hello cluster.</span></span> <span data-ttu-id="44eef-285">Bien que le cluster HDInsight est supprimé, conteneur de stockage d’objets blob hello par défaut et le compte de stockage hello associée ne sont pas supprimés.</span><span class="sxs-lookup"><span data-stu-id="44eef-285">Even though HDInsight cluster is deleted, hello default blob storage container and hello associated storage account are not deleted.</span></span> <span data-ttu-id="44eef-286">Ce comportement est normal.</span><span class="sxs-lookup"><span data-stu-id="44eef-286">This behavior is by design.</span></span> <span data-ttu-id="44eef-287">Comme un nombre croissant de tranches sont traitées, vous voyez un grand nombre de conteneurs dans votre stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="44eef-287">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="44eef-288">Si vous ne devez pas les pour la résolution des problèmes de travaux de hello, vous souhaiterez peut-être toodelete les coûts de stockage tooreduce hello.</span><span class="sxs-lookup"><span data-stu-id="44eef-288">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="44eef-289">les noms de ces conteneurs Hello suivent un modèle : `adfyourdatafactoryname-linkedservicename-datetimestamp`.</span><span class="sxs-lookup"><span data-stu-id="44eef-289">hello names of these containers follow a pattern: `adfyourdatafactoryname-linkedservicename-datetimestamp`.</span></span>

<span data-ttu-id="44eef-290">Supprimer hello **adfjobs** et **adfyourdatafactoryname-linkedservicename-datetimestamp** dossiers.</span><span class="sxs-lookup"><span data-stu-id="44eef-290">Delete hello **adfjobs** and **adfyourdatafactoryname-linkedservicename-datetimestamp** folders.</span></span> <span data-ttu-id="44eef-291">conteneur d’adfjobs Hello contient des journaux de travail à partir d’Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="44eef-291">hello adfjobs container contains job logs from Azure Data Factory.</span></span>

### <a name="delete-hello-resource-group"></a><span data-ttu-id="44eef-292">Supprimer le groupe de ressources hello</span><span class="sxs-lookup"><span data-stu-id="44eef-292">Delete hello resource group</span></span>
<span data-ttu-id="44eef-293">[Le Gestionnaire de ressources Azure](../azure-resource-manager/resource-group-overview.md) est toodeploy utilisé, gérer et surveiller votre solution en tant que groupe.</span><span class="sxs-lookup"><span data-stu-id="44eef-293">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) is used toodeploy, manage, and monitor your solution as a group.</span></span>  <span data-ttu-id="44eef-294">La suppression d’un groupe de ressources supprime tous les composants hello à l’intérieur du groupe de hello.</span><span class="sxs-lookup"><span data-stu-id="44eef-294">Deleting a resource group deletes all hello components inside hello group.</span></span>  

1. <span data-ttu-id="44eef-295">Ouverture de session toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="44eef-295">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="44eef-296">Cliquez sur **groupes de ressources** sur le volet gauche de hello.</span><span class="sxs-lookup"><span data-stu-id="44eef-296">Click **Resource groups** on hello left pane.</span></span>
3. <span data-ttu-id="44eef-297">Cliquez sur le nom de groupe de ressources hello que vous avez créé dans votre script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="44eef-297">Click hello resource group name you created in your PowerShell script.</span></span> <span data-ttu-id="44eef-298">Utilisez le filtre de hello si vous avez trop de groupes de ressources répertoriées.</span><span class="sxs-lookup"><span data-stu-id="44eef-298">Use hello filter if you have too many resource groups listed.</span></span> <span data-ttu-id="44eef-299">Il ouvre le groupe de ressources hello dans un nouveau panneau.</span><span class="sxs-lookup"><span data-stu-id="44eef-299">It opens hello resource group in a new blade.</span></span>
4. <span data-ttu-id="44eef-300">Sur hello **ressources** vignette, doit avoir compte de stockage par défaut hello et la fabrique de données hello répertoriés, sauf si vous partagez un groupe de ressources hello avec d’autres projets.</span><span class="sxs-lookup"><span data-stu-id="44eef-300">On hello **Resources** tile, you shall have hello default storage account and hello data factory listed unless you share hello resource group with other projects.</span></span>
5. <span data-ttu-id="44eef-301">Cliquez sur **supprimer** haut hello du Panneau de hello.</span><span class="sxs-lookup"><span data-stu-id="44eef-301">Click **Delete** on hello top of hello blade.</span></span> <span data-ttu-id="44eef-302">Cela supprime le compte de stockage hello et données hello stockées dans le compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="44eef-302">Doing so deletes hello storage account and hello data stored in hello storage account.</span></span>
6. <span data-ttu-id="44eef-303">Entrez la suppression tooconfirm nom du groupe de ressources hello, puis cliquez sur **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="44eef-303">Enter hello resource group name tooconfirm deletion, and then click **Delete**.</span></span>

<span data-ttu-id="44eef-304">Au cas où vous ne souhaitez pas compte de stockage toodelete hello lorsque vous supprimez le groupe de ressources hello, envisagez de hello suivant architecture en séparant les données d’entreprise hello de compte de stockage par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="44eef-304">In case you don't want toodelete hello storage account when you delete hello resource group, consider hello following architecture by separating hello business data from hello default storage account.</span></span> <span data-ttu-id="44eef-305">Dans ce cas, vous disposez d’un groupe de ressources pour le compte de stockage hello avec les données métier hello et hello autre groupe de ressources pour le compte de stockage par défaut hello pour HDInsight lié hello et service de fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="44eef-305">In this case, you have one resource group for hello storage account with hello business data, and hello other resource group for hello default storage account for HDInsight linked service and hello data factory.</span></span> <span data-ttu-id="44eef-306">Lorsque vous supprimez le deuxième groupe de ressources hello, il n’affecte pas de compte de stockage de données hello entreprise.</span><span class="sxs-lookup"><span data-stu-id="44eef-306">When you delete hello second resource group, it does not impact hello business data storage account.</span></span> <span data-ttu-id="44eef-307">toodo pour :</span><span class="sxs-lookup"><span data-stu-id="44eef-307">toodo so:</span></span>

* <span data-ttu-id="44eef-308">Ajoutez hello suivant du groupe de ressources de niveau supérieur de toohello, ainsi que de hello Microsoft.DataFactory/datafactories des ressources dans votre modèle de gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="44eef-308">Add hello following toohello top-level resource group along with hello Microsoft.DataFactory/datafactories resource in your Resource Manager template.</span></span> <span data-ttu-id="44eef-309">Ce code crée un compte de stockage :</span><span class="sxs-lookup"><span data-stu-id="44eef-309">It creates a storage account:</span></span>

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
* <span data-ttu-id="44eef-310">Ajouter un nouveau service lié point toohello compte de stockage :</span><span class="sxs-lookup"><span data-stu-id="44eef-310">Add a new linked service point toohello new storage account:</span></span>

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
* <span data-ttu-id="44eef-311">Configurer hello HDInsight liée à la demande service avec un dependsOn supplémentaire et une additionalLinkedServiceNames :</span><span class="sxs-lookup"><span data-stu-id="44eef-311">Configure hello HDInsight ondemand linked service with an additional dependsOn and an additionalLinkedServiceNames:</span></span>

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
## <a name="next-steps"></a><span data-ttu-id="44eef-312">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="44eef-312">Next steps</span></span>
<span data-ttu-id="44eef-313">Dans cet article, vous avez appris comment toouse Azure Data Factory toocreate à la demande HDInsight cluster tooprocess ruche de travaux.</span><span class="sxs-lookup"><span data-stu-id="44eef-313">In this article, you have learned how toouse Azure Data Factory toocreate on-demand HDInsight cluster tooprocess Hive jobs.</span></span> <span data-ttu-id="44eef-314">tooread plus :</span><span class="sxs-lookup"><span data-stu-id="44eef-314">tooread more:</span></span>

* [<span data-ttu-id="44eef-315">Didacticiel Hadoop : prise en main de Hadoop sous Linux dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="44eef-315">Hadoop tutorial: Get started using Linux-based Hadoop in HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="44eef-316">Création de clusters Hadoop basés sur Linux dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="44eef-316">Create Linux-based Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="44eef-317">Documentation HDInsight</span><span class="sxs-lookup"><span data-stu-id="44eef-317">HDInsight documentation</span></span>](https://azure.microsoft.com/documentation/services/hdinsight/)
* [<span data-ttu-id="44eef-318">Documentation Data Factory</span><span class="sxs-lookup"><span data-stu-id="44eef-318">Data factory documentation</span></span>](https://azure.microsoft.com/documentation/services/data-factory/)

## <a name="appendix"></a><span data-ttu-id="44eef-319">Annexe</span><span class="sxs-lookup"><span data-stu-id="44eef-319">Appendix</span></span>

### <a name="azure-cli-script"></a><span data-ttu-id="44eef-320">Script d’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="44eef-320">Azure CLI script</span></span>
<span data-ttu-id="44eef-321">Vous pouvez utiliser CLI d’Azure au lieu d’utiliser le didacticiel de hello toodo Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="44eef-321">You can use Azure CLI instead of using Azure PowerShell toodo hello tutorial.</span></span> <span data-ttu-id="44eef-322">toouse CLI d’Azure, installez tout d’abord CLI d’Azure conformément à hello suivant les instructions :</span><span class="sxs-lookup"><span data-stu-id="44eef-322">toouse Azure CLI, first install Azure CLI as per hello following instructions:</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

#### <a name="use-azure-cli-tooprepare-hello-storage-and-copy-hello-files"></a><span data-ttu-id="44eef-323">Utiliser le stockage Azure CLI tooprepare hello et copiez les fichiers hello</span><span class="sxs-lookup"><span data-stu-id="44eef-323">Use Azure CLI tooprepare hello storage and copy hello files</span></span>

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

<span data-ttu-id="44eef-324">nom du conteneur Hello est *adfgetstarted*.</span><span class="sxs-lookup"><span data-stu-id="44eef-324">hello container name is *adfgetstarted*.</span></span> <span data-ttu-id="44eef-325">Gardez-le tel quel.</span><span class="sxs-lookup"><span data-stu-id="44eef-325">Keep it as it is.</span></span> <span data-ttu-id="44eef-326">Sinon, vous devez modèle de gestionnaire de ressources tooupdate hello.</span><span class="sxs-lookup"><span data-stu-id="44eef-326">Otherwise you need tooupdate hello Resource Manager template.</span></span> <span data-ttu-id="44eef-327">Si vous avez besoin d’aide avec ce script CLI, consultez [Using hello CLI d’Azure avec le stockage Azure](../storage/common/storage-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="44eef-327">If you need help with this CLI script, see [Using hello Azure CLI with Azure Storage](../storage/common/storage-azure-cli.md).</span></span>
