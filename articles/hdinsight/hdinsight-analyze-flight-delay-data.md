---
title: "données de retard de vol aaaAnalyze avec Hadoop dans HDInsight - Azure | Documents Microsoft"
description: "Découvrez comment toouse un Windows PowerShell script toocreate un cluster HDInsight, exécuter un travail Hive, exécuter un travail Sqoop et supprimer hello cluster."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00e26aa9-82fb-4dbe-b87d-ffe8e39a5412
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 6ebaee65d9b270e5dc2141dd1265011d372f497d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-flight-delay-data-by-using-hive-in-hdinsight"></a><span data-ttu-id="817b6-103">Analyse des données sur les retards de vol avec Hive dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="817b6-103">Analyze flight delay data by using Hive in HDInsight</span></span>
<span data-ttu-id="817b6-104">Hive permet d’exécuter des tâches Hadoop MapReduce via un langage de création de scripts semblable à SQL, nommé *[HiveQL][hadoop-hiveql]*, qui peut être appliqué à la synthèse, à l’envoi de requêtes et à l’analyse d’importants volumes de données.</span><span class="sxs-lookup"><span data-stu-id="817b6-104">Hive provides a means of running Hadoop MapReduce jobs through an SQL-like scripting language called *[HiveQL][hadoop-hiveql]*, which can be applied towards summarizing, querying, and analyzing large volumes of data.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="817b6-105">Hello étapes décrites dans ce document nécessitent un cluster HDInsight de basés sur Windows.</span><span class="sxs-lookup"><span data-stu-id="817b6-105">hello steps in this document require a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="817b6-106">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="817b6-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="817b6-107">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="817b6-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="817b6-108">Pour les étapes fonctionnant avec un cluster basé sur Linux, consultez la rubrique [Analyse des données sur les retards de vol avec Hive dans HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md).</span><span class="sxs-lookup"><span data-stu-id="817b6-108">For steps that work with a Linux-based cluster, see [Analyze flight delay data by using Hive in HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md).</span></span>

<span data-ttu-id="817b6-109">Un des principaux avantages de hello d’Azure HDInsight est séparation hello de calcul et de stockage de données.</span><span class="sxs-lookup"><span data-stu-id="817b6-109">One of hello major benefits of Azure HDInsight is hello separation of data storage and compute.</span></span> <span data-ttu-id="817b6-110">HDInsight utilise le stockage d’objets blob Azure pour stocker les données.</span><span class="sxs-lookup"><span data-stu-id="817b6-110">HDInsight uses Azure Blob storage for data storage.</span></span> <span data-ttu-id="817b6-111">Une tâche classique comprend trois parties :</span><span class="sxs-lookup"><span data-stu-id="817b6-111">A typical job involves three parts:</span></span>

1. <span data-ttu-id="817b6-112">**Le stockage des données dans un stockage d’objets blob Azure.**</span><span class="sxs-lookup"><span data-stu-id="817b6-112">**Store data in Azure Blob storage.**</span></span>  <span data-ttu-id="817b6-113">Par exemple, les données météorologiques, les données de capteur, les journaux web et, en l’occurrence, les données liées aux retards de vol, sont enregistrés dans un stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="817b6-113">For example, weather data, sensor data, web logs, and in this case, flight delay data are saved into Azure Blob storage.</span></span>
2. <span data-ttu-id="817b6-114">**L’exécution des tâches.**</span><span class="sxs-lookup"><span data-stu-id="817b6-114">**Run jobs.**</span></span> <span data-ttu-id="817b6-115">Lorsqu’il est données hello tooprocess du temps, vous exécutez un script Windows PowerShell (ou une application cliente) toocreate un cluster HDInsight, exécuter des travaux et supprimer le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="817b6-115">When it is time tooprocess hello data, you run a Windows PowerShell script (or a client application) toocreate an HDInsight cluster, run jobs, and delete hello cluster.</span></span> <span data-ttu-id="817b6-116">travaux Hello enregistrer les données de sortie tooAzure stockage d’objets Blob.</span><span class="sxs-lookup"><span data-stu-id="817b6-116">hello jobs save output data tooAzure Blob storage.</span></span> <span data-ttu-id="817b6-117">les données de sortie Hello sont conservées même après la suppression de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="817b6-117">hello output data is retained even after hello cluster is deleted.</span></span> <span data-ttu-id="817b6-118">De cette façon, vous ne payez que ce que vous avez consommé.</span><span class="sxs-lookup"><span data-stu-id="817b6-118">This way, you pay for only what you have consumed.</span></span>
3. <span data-ttu-id="817b6-119">**Récupérer la sortie de hello du stockage d’objets Blob Azure**, ou dans ce didacticiel, exporter la base de données SQL Azure hello données tooan.</span><span class="sxs-lookup"><span data-stu-id="817b6-119">**Retrieve hello output from Azure Blob storage**, or in this tutorial, export hello data tooan Azure SQL database.</span></span>

<span data-ttu-id="817b6-120">Hello diagramme suivant illustre le scénario de hello et structure hello de ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="817b6-120">hello following diagram illustrates hello scenario and hello structure of this tutorial:</span></span>

![HDI.FlightDelays.flow][img-hdi-flightdelays-flow]

<span data-ttu-id="817b6-122">Notez que les nombres hello dans le diagramme de hello correspondent toohello les titres de section.</span><span class="sxs-lookup"><span data-stu-id="817b6-122">Note that hello numbers in hello diagram correspond toohello section titles.</span></span> <span data-ttu-id="817b6-123">**M** représente le processus principal hello.</span><span class="sxs-lookup"><span data-stu-id="817b6-123">**M** stands for hello main process.</span></span> <span data-ttu-id="817b6-124">**A** représente le contenu dans l’annexe de hello hello.</span><span class="sxs-lookup"><span data-stu-id="817b6-124">**A** stands for hello content in hello appendix.</span></span>

<span data-ttu-id="817b6-125">partie principale de Hello du didacticiel de hello vous montre des tâches de toouse un Windows PowerShell script tooperform hello suivant :</span><span class="sxs-lookup"><span data-stu-id="817b6-125">hello main portion of hello tutorial shows you how toouse one Windows PowerShell script tooperform hello following tasks:</span></span>

* <span data-ttu-id="817b6-126">Créez un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="817b6-126">Create an HDInsight cluster.</span></span>
* <span data-ttu-id="817b6-127">Exécuter un travail Hive sur des retards de hello cluster toocalculate moyenne dans les aéroports.</span><span class="sxs-lookup"><span data-stu-id="817b6-127">Run a Hive job on hello cluster toocalculate average delays at airports.</span></span> <span data-ttu-id="817b6-128">données de retard de vol Hello sont stockées dans un compte de stockage d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="817b6-128">hello flight delay data is stored in an Azure Blob storage account.</span></span>
* <span data-ttu-id="817b6-129">Exécuter un Sqoop travail tooexport hello ruche travail sortie tooan SQL Azure de base de données.</span><span class="sxs-lookup"><span data-stu-id="817b6-129">Run a Sqoop job tooexport hello Hive job output tooan Azure SQL database.</span></span>
* <span data-ttu-id="817b6-130">Supprimer le cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="817b6-130">Delete hello HDInsight cluster.</span></span>

<span data-ttu-id="817b6-131">Dans les annexes hello, vous trouverez des instructions de hello pour télécharger des données de retard de vol, création/chargement d’une chaîne de requête Hive et préparation de la base de données SQL Azure hello pour le travail de Sqoop hello.</span><span class="sxs-lookup"><span data-stu-id="817b6-131">In hello appendixes, you can find hello instructions for uploading flight delay data, creating/uploading a Hive query string, and preparing hello Azure SQL database for hello Sqoop job.</span></span>

> [!NOTE]
> <span data-ttu-id="817b6-132">étapes de Hello dans ce document sont des clusters HDInsight tooWindows spécifiques.</span><span class="sxs-lookup"><span data-stu-id="817b6-132">hello steps in this document are specific tooWindows-based HDInsight clusters.</span></span> <span data-ttu-id="817b6-133">Pour les étapes fonctionnant avec un cluster basé sur Linux, consultez la rubrique [Analyse des données sur les retards de vol avec Hive dans HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md).</span><span class="sxs-lookup"><span data-stu-id="817b6-133">For steps that work with a Linux-based cluster, see [Analyze flight delay data using Hive in HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md)</span></span>

### <a name="prerequisites"></a><span data-ttu-id="817b6-134">Composants requis</span><span class="sxs-lookup"><span data-stu-id="817b6-134">Prerequisites</span></span>
<span data-ttu-id="817b6-135">Avant de commencer ce didacticiel, vous devez disposer des éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="817b6-135">Before you begin this tutorial, you must have hello following items:</span></span>

* <span data-ttu-id="817b6-136">**Un abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="817b6-136">**An Azure subscription**.</span></span> <span data-ttu-id="817b6-137">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="817b6-137">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="817b6-138">**Un poste de travail sur lequel est installé Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="817b6-138">**A workstation with Azure PowerShell**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="817b6-139">La prise en charge de la gestion des ressources HDInsight par Azure PowerShell à l’aide d’Azure Service Manager est **déconseillée** ; elle a été supprimée le 1er janvier 2017.</span><span class="sxs-lookup"><span data-stu-id="817b6-139">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="817b6-140">étapes de Hello dans ce document Utilisez hello nouvelles applets de commande HDInsight qui fonctionnent avec Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="817b6-140">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="817b6-141">Suivez les étapes de hello dans [installer et configurer Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello dernière version d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="817b6-141">Please follow hello steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="817b6-142">Si vous avez des scripts qui toobe besoin modifié toouse hello nouvelles applets de commande qui fonctionnent avec Azure Resource Manager, consultez [des outils de migration tooAzure développement basé sur le Gestionnaire de ressources pour les clusters HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="817b6-142">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

<span data-ttu-id="817b6-143">**Fichiers utilisés dans ce didacticiel**</span><span class="sxs-lookup"><span data-stu-id="817b6-143">**Files used in this tutorial**</span></span>

<span data-ttu-id="817b6-144">Ce didacticiel utilise hello sur performances compagnie aérienne de données de vol de [recherche et Administration de la technologie novatrice, Bureau de statistiques de transport ou RITA][rita-website].</span><span class="sxs-lookup"><span data-stu-id="817b6-144">This tutorial uses hello on-time performance of airline flight data from [Research and Innovative Technology Administration, Bureau of Transportation Statistics or RITA][rita-website].</span></span>
<span data-ttu-id="817b6-145">Une copie de hello données a été téléchargé tooan conteneur de stockage d’objets Blob Azure avec l’autorisation d’accès Public Blob hello.</span><span class="sxs-lookup"><span data-stu-id="817b6-145">A copy of hello data has been uploaded tooan Azure Blob storage container with hello Public Blob access permission.</span></span>
<span data-ttu-id="817b6-146">Une partie de votre script PowerShell copie des données de hello de hello blob publics conteneur toohello par défaut conteneur d’objets blob de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="817b6-146">A part of your PowerShell script copies hello data from hello public blob container toohello default blob container of your cluster.</span></span> <span data-ttu-id="817b6-147">Hello HiveQL script est également copié toohello même conteneur d’objets Blob.</span><span class="sxs-lookup"><span data-stu-id="817b6-147">hello HiveQL script is also copied toohello same Blob container.</span></span>
<span data-ttu-id="817b6-148">Si vous souhaitez toolearn comment tooget/téléchargement hello données tooyour propriétaire de compte de stockage, et comment toocreate/téléchargement hello HiveQL script de fichier, consultez [annexe A](#appendix-a) et [annexe B](#appendix-b).</span><span class="sxs-lookup"><span data-stu-id="817b6-148">If you want toolearn how tooget/upload hello data tooyour own Storage account, and how toocreate/upload hello HiveQL script file, see [Appendix A](#appendix-a) and [Appendix B](#appendix-b).</span></span>

<span data-ttu-id="817b6-149">Hello tableau suivant répertorie les fichiers hello utilisés dans ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="817b6-149">hello following table lists hello files used in this tutorial:</span></span>

<table border="1">
<tr><th><span data-ttu-id="817b6-150">Fichiers</span><span class="sxs-lookup"><span data-stu-id="817b6-150">Files</span></span></th><th><span data-ttu-id="817b6-151">Description</span><span class="sxs-lookup"><span data-stu-id="817b6-151">Description</span></span></th></tr>
<tr><td>wasb://flightdelay@hditutorialdata.blob.core.windows.net/flightdelays.hql</td><td><span data-ttu-id="817b6-152">fichier de script HiveQL Hello utilisé par hello tâche Hive.</span><span class="sxs-lookup"><span data-stu-id="817b6-152">hello HiveQL script file used by hello Hive job.</span></span> <span data-ttu-id="817b6-153">Ce script a été téléchargé tooan compte de stockage d’objets Blob Azure avec un accès public hello.</span><span class="sxs-lookup"><span data-stu-id="817b6-153">This script has been uploaded tooan Azure Blob storage account with hello public access.</span></span> <span data-ttu-id="817b6-154"><a href="#appendix-b">Annexe B</a> contient des instructions sur la préparation et le téléchargement de ce compte de stockage de fichier tooyour propre objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="817b6-154"><a href="#appendix-b">Appendix B</a> has instructions on preparing and uploading this file tooyour own Azure Blob storage account.</span></span></td></tr>
<tr><td>wasb://flightdelay@hditutorialdata.blob.core.windows.net/2013Data</td><td><span data-ttu-id="817b6-155">Données d’entrée pour le travail de ruche hello.</span><span class="sxs-lookup"><span data-stu-id="817b6-155">Input data for hello Hive job.</span></span> <span data-ttu-id="817b6-156">les données de salutation a été téléchargé tooan compte de stockage d’objets Blob Azure avec un accès public hello.</span><span class="sxs-lookup"><span data-stu-id="817b6-156">hello data has been uploaded tooan Azure Blob storage account with hello public access.</span></span> <span data-ttu-id="817b6-157"><a href="#appendix-a">Annexe A</a> contient des instructions sur l’obtention de données de hello et le téléchargement de compte de stockage Azure Blob propre hello données tooyour.</span><span class="sxs-lookup"><span data-stu-id="817b6-157"><a href="#appendix-a">Appendix A</a> has instructions on getting hello data and uploading hello data tooyour own Azure Blob storage account.</span></span></td></tr>
<tr><td><span data-ttu-id="817b6-158">\tutorials\flightdelays\output</span><span class="sxs-lookup"><span data-stu-id="817b6-158">\tutorials\flightdelays\output</span></span></td><td><span data-ttu-id="817b6-159">chemin de sortie Hello pour le travail de ruche hello.</span><span class="sxs-lookup"><span data-stu-id="817b6-159">hello output path for hello Hive job.</span></span> <span data-ttu-id="817b6-160">conteneur par défaut de Hello est utilisé pour stocker les données de sortie hello.</span><span class="sxs-lookup"><span data-stu-id="817b6-160">hello default container is used for storing hello output data.</span></span></td></tr>
<tr><td><span data-ttu-id="817b6-161">\tutorials\flightdelays\jobstatus</span><span class="sxs-lookup"><span data-stu-id="817b6-161">\tutorials\flightdelays\jobstatus</span></span></td><td><span data-ttu-id="817b6-162">Hello ruche travail état dossier conteneur par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="817b6-162">hello Hive job status folder on hello default container.</span></span></td></tr>
</table>

## <a name="create-cluster-and-run-hivesqoop-jobs"></a><span data-ttu-id="817b6-163">Création d’un cluster et exécution de tâches Hive/Sqoop</span><span class="sxs-lookup"><span data-stu-id="817b6-163">Create cluster and run Hive/Sqoop jobs</span></span>
<span data-ttu-id="817b6-164">Hadoop MapReduce correspond au traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="817b6-164">Hadoop MapReduce is batch processing.</span></span> <span data-ttu-id="817b6-165">Hello plus rentable toorun un travail Hive est toocreate un cluster pour la tâche de hello et supprimer le travail de hello après la tâche de hello.</span><span class="sxs-lookup"><span data-stu-id="817b6-165">hello most cost-effective way toorun a Hive job is toocreate a cluster for hello job, and delete hello job after hello job is completed.</span></span> <span data-ttu-id="817b6-166">Hello script suivant couvre les processus hello.</span><span class="sxs-lookup"><span data-stu-id="817b6-166">hello following script covers hello whole process.</span></span>
<span data-ttu-id="817b6-167">Pour plus d’informations sur la création d’un cluster HDInsight et l’exécution de tâches Hive, consultez les rubriques [Création de clusters Hadoop dans HDInsight][hdinsight-provision] et [Utilisation de Hive avec HDInsight][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="817b6-167">For more information on creating an HDInsight cluster and running Hive jobs, see [Create Hadoop clusters in HDInsight][hdinsight-provision] and [Use Hive with HDInsight][hdinsight-use-hive].</span></span>

<span data-ttu-id="817b6-168">**requêtes Hive toorun hello par Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="817b6-168">**toorun hello Hive queries by Azure PowerShell**</span></span>

1. <span data-ttu-id="817b6-169">Créer une table de base de données et hello SQL Azure pour la sortie de tâche hello Sqoop à l’aide d’instructions hello dans [annexe C](#appendix-c).</span><span class="sxs-lookup"><span data-stu-id="817b6-169">Create an Azure SQL database and hello table for hello Sqoop job output by using hello instructions in [Appendix C](#appendix-c).</span></span>
2. <span data-ttu-id="817b6-170">Ouvrez Windows PowerShell ISE et exécutez hello script suivant :</span><span class="sxs-lookup"><span data-stu-id="817b6-170">Open Windows PowerShell ISE, and run hello following script:</span></span>

    ```powershell
    $subscriptionID = "<Azure Subscription ID>"
    $nameToken = "<Enter an Alias>"

    ###########################################
    # You must configure hello follwing variables
    # for an existing Azure SQL Database
    ###########################################
    $existingSqlDatabaseServerName = "<Azure SQL Database Server>"
    $existingSqlDatabaseLogin = "<Azure SQL Database Server Login>"
    $existingSqlDatabasePassword = "<Azure SQL Database Server login password>"
    $existingSqlDatabaseName = "<Azure SQL Database name>"

    $localFolder = "E:\Tutorials\Downloads\" # A temp location for copying files.
    $azcopyPath = "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy" # depends on hello version, hello folder can be different

    ###########################################
    # (Optional) configure hello following variables
    ###########################################

    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $location = "EAST US 2"

    $HDInsightClusterName = $namePrefix + "hdi"
    $httpUserName = "admin"
    $httpPassword = "<Enter hello Password>"

    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $HDInsightClusterName # use hello cluster name

    $existingSqlDatabaseTableName = "AvgDelays"
    $sqlDatabaseConnectionString = "jdbc:sqlserver://$existingSqlDatabaseServerName.database.windows.net;user=$existingSqlDatabaseLogin@$existingSqlDatabaseServerName;password=$existingSqlDatabaseLogin;database=$existingSqlDatabaseName"

    $hqlScriptFile = "/tutorials/flightdelays/flightdelays.hql"

    $jobStatusFolder = "/tutorials/flightdelays/jobstatus"

    ###########################################
    # Login
    ###########################################
    try{
        $acct = Get-AzureRmSubscription
    }
    catch{
        Login-AzureRmAccount
    }
    Select-AzureRmSubscription -SubscriptionID $subscriptionID

    ###########################################
    # Create a new HDInsight cluster
    ###########################################

    # Create ARM group
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create hello default storage account
    New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName -Location $location -Type Standard_LRS

    # Create hello default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey
    New-AzureStorageContainer -Name $defaultBlobContainerName -Context $defaultStorageAccountContext

    # Create hello HDInsight cluster
    $pw = ConvertTo-SecureString -String $httpPassword -AsPlainText -Force
    $httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -Location $location `
        -ClusterType Hadoop `
        -OSType Windows `
        -ClusterSizeInNodes 2 `
        -HttpCredential $httpCredential `
        -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultStorageContainer $existingDefaultBlobContainerName

    ###########################################
    # Prepare hello HiveQL script and source data
    ###########################################

    # Create hello temp location
    New-Item -Path $localFolder -ItemType Directory -Force

    # Download hello sample file from Azure Blob storage
    $context = New-AzureStorageContext -StorageAccountName "hditutorialdata" -Anonymous
    $blobs = Get-AzureStorageBlob -Container "flightdelay" -Context $context
    #$blobs | Get-AzureStorageBlobContent -Context $context -Destination $localFolder

    # Upload data toodefault container

    $azcopycmd = "cmd.exe /C '$azcopyPath\azcopy.exe' /S /Source:'$localFolder' /Dest:'https://$defaultStorageAccountName.blob.core.windows.net/$defaultBlobContainerName/tutorials/flightdelays' /DestKey:$defaultStorageAccountKey"

    Invoke-Expression -Command:$azcopycmd

    ###########################################
    # Submit hello Hive job
    ###########################################
    Use-AzureRmHDInsightCluster -ClusterName $HDInsightClusterName -HttpCredential $httpCredential
    $response = Invoke-AzureRmHDInsightHiveJob `
                    -Files $hqlScriptFile `
                    -DefaultContainer $defaultBlobContainerName `
                    -DefaultStorageAccountName $defaultStorageAccountName `
                    -DefaultStorageAccountKey $defaultStorageAccountKey `
                    -StatusFolder $jobStatusFolder

    write-Host $response

    ###########################################
    # Submit hello Sqoop job
    ###########################################
    $exportDir = "wasb://$defaultBlobContainerName@$defaultStorageAccountName.blob.core.windows.net/tutorials/flightdelays/output"

    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
                    -Command "export --connect $sqlDatabaseConnectionString --table $sqlDatabaseTableName --export-dir $exportDir --fields-terminated-by \001 "
    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ResourceGroupName $resourceGroupName `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -HttpCredential $httpCredential `
        -WaitTimeoutInSeconds 3600 `
        -Job $sqoopJob.JobId

    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -DefaultContainer $existingDefaultBlobContainerName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardError

    ###########################################
    # Delete hello cluster
    ###########################################
    Remove-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName
    ```
3. <span data-ttu-id="817b6-171">Connexion de base de données SQL tooyour et consultez les retards de vol moyenne par ville dans la table de AvgDelays hello :</span><span class="sxs-lookup"><span data-stu-id="817b6-171">Connect tooyour SQL database and see average flight delays by city in hello AvgDelays table:</span></span>

    ![HDI.FlightDelays.AvgDelays.Dataset][image-hdi-flightdelays-avgdelays-dataset]

- - -

## <span data-ttu-id="817b6-173"><a id="appendix-a"></a>Annexe A - téléchargement flight delay données tooAzure stockage d’objets Blob</span><span class="sxs-lookup"><span data-stu-id="817b6-173"><a id="appendix-a"></a>Appendix A - Upload flight delay data tooAzure Blob storage</span></span>
<span data-ttu-id="817b6-174">Téléchargement du fichier de données hello et les fichiers de script de HiveQL hello (consultez [annexe B](#appendix-b)) requiert une planification.</span><span class="sxs-lookup"><span data-stu-id="817b6-174">Uploading hello data file and hello HiveQL script files (see [Appendix B](#appendix-b)) requires some planning.</span></span> <span data-ttu-id="817b6-175">Hello est toostore des fichiers de données hello et fichier de HiveQL hello avant de créer un cluster HDInsight et de travail de ruche hello en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="817b6-175">hello idea is toostore hello data files and hello HiveQL file before creating an HDInsight cluster and running hello Hive job.</span></span> <span data-ttu-id="817b6-176">Deux options s'offrent à vous :</span><span class="sxs-lookup"><span data-stu-id="817b6-176">You have two options:</span></span>

* <span data-ttu-id="817b6-177">**Utilisez hello même compte de stockage Azure qui servira par cluster HDInsight de hello en tant que système de fichiers par défaut hello.**</span><span class="sxs-lookup"><span data-stu-id="817b6-177">**Use hello same Azure Storage account that will be used by hello HDInsight cluster as hello default file system.**</span></span> <span data-ttu-id="817b6-178">Étant donné que le cluster HDInsight de hello aura hello compte clé d’accès, vous n’avez pas besoin toomake des modifications supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="817b6-178">Because hello HDInsight cluster will have hello Storage account access key, you don't need toomake any additional changes.</span></span>
* <span data-ttu-id="817b6-179">**Utilisez un compte de stockage Azure différent de hello système de fichiers HDInsight cluster par défaut.**</span><span class="sxs-lookup"><span data-stu-id="817b6-179">**Use a different Azure Storage account from hello HDInsight cluster default file system.**</span></span> <span data-ttu-id="817b6-180">Si c’est le cas de hello, vous devez modifier la partie de la création de hello Hello Windows PowerShell script trouvé dans [cluster HDInsight de créer et tâches d’exécution Hive/Sqoop](#runjob) toolink hello compte de stockage comme un compte de stockage supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="817b6-180">If this is hello case, you must modify hello creation part of hello Windows PowerShell script found in [Create HDInsight cluster and run Hive/Sqoop jobs](#runjob) toolink hello Storage account as an additional Storage account.</span></span> <span data-ttu-id="817b6-181">Pour plus d’informations, consultez la rubrique [Création de clusters Hadoop dans HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="817b6-181">For instructions, see [Create Hadoop clusters in HDInsight][hdinsight-provision].</span></span> <span data-ttu-id="817b6-182">cluster HDInsight de Hello sait ensuite la clé d’accès hello hello compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="817b6-182">hello HDInsight cluster then knows hello access key for hello Storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="817b6-183">Bonjour le chemin d’accès de stockage Blob pour hello fichier de données est codé en dur dans le fichier de script HiveQL hello.</span><span class="sxs-lookup"><span data-stu-id="817b6-183">hello Blob storage path for hello data file is hard coded in hello HiveQL script file.</span></span> <span data-ttu-id="817b6-184">Vous devez le mettre à jour en conséquence.</span><span class="sxs-lookup"><span data-stu-id="817b6-184">You must update it accordingly.</span></span>

<span data-ttu-id="817b6-185">**données de vol hello toodownload**</span><span class="sxs-lookup"><span data-stu-id="817b6-185">**toodownload hello flight data**</span></span>

1. <span data-ttu-id="817b6-186">Parcourir trop[recherche et l’Administration de technologie novatrice, Bureau de statistiques de transport][rita-website].</span><span class="sxs-lookup"><span data-stu-id="817b6-186">Browse too[Research and Innovative Technology Administration, Bureau of Transportation Statistics][rita-website].</span></span>
2. <span data-ttu-id="817b6-187">Sur la page de hello, sélectionnez hello valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="817b6-187">On hello page, select hello following values:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="817b6-188">Nom</span><span class="sxs-lookup"><span data-stu-id="817b6-188">Name</span></span></th><th><span data-ttu-id="817b6-189">Valeur</span><span class="sxs-lookup"><span data-stu-id="817b6-189">Value</span></span></th></tr>
    <tr><td><span data-ttu-id="817b6-190">Filtre année</span><span class="sxs-lookup"><span data-stu-id="817b6-190">Filter Year</span></span></td><td><span data-ttu-id="817b6-191">2013</span><span class="sxs-lookup"><span data-stu-id="817b6-191">2013</span></span> </td></tr>
    <tr><td><span data-ttu-id="817b6-192">Filtre période</span><span class="sxs-lookup"><span data-stu-id="817b6-192">Filter Period</span></span></td><td><span data-ttu-id="817b6-193">Janvier</span><span class="sxs-lookup"><span data-stu-id="817b6-193">January</span></span></td></tr>
    <tr><td><span data-ttu-id="817b6-194">Champs</span><span class="sxs-lookup"><span data-stu-id="817b6-194">Fields</span></span></td><td><span data-ttu-id="817b6-195">*Year*, *FlightDate*, *UniqueCarrier*, *Carrier*, *FlightNum*, *OriginAirportID*, *Origin*, *OriginCityName*, *OriginState*, *DestAirportID*, *Dest*, *DestCityName*, *DestState*, *DepDelayMinutes*, *ArrDelay*, *ArrDelayMinutes*, *CarrierDelay*, *WeatherDelay*, *NASDelay*, *SecurityDelay*, *LateAircraftDelay* (effacez tous les autres champs)</span><span class="sxs-lookup"><span data-stu-id="817b6-195">*Year*, *FlightDate*, *UniqueCarrier*, *Carrier*, *FlightNum*, *OriginAirportID*, *Origin*, *OriginCityName*, *OriginState*, *DestAirportID*, *Dest*, *DestCityName*, *DestState*, *DepDelayMinutes*, *ArrDelay*, *ArrDelayMinutes*, *CarrierDelay*, *WeatherDelay*, *NASDelay*, *SecurityDelay*, *LateAircraftDelay* (clear all other fields)</span></span></td></tr>
    </table><span data-ttu-id="817b6-196">
3. Cliquez sur **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="817b6-196">
3. Click **Download**.</span></span>
<span data-ttu-id="817b6-197">4.</span><span class="sxs-lookup"><span data-stu-id="817b6-197">4.</span></span> <span data-ttu-id="817b6-198">Décompressez hello fichier toohello **C:\Tutorials\FlightDelay\2013Data** dossier.</span><span class="sxs-lookup"><span data-stu-id="817b6-198">Unzip hello file toohello **C:\Tutorials\FlightDelay\2013Data** folder.</span></span> <span data-ttu-id="817b6-199">Chaque fichier correspond à un fichier CSV d’environ 60 Go.</span><span class="sxs-lookup"><span data-stu-id="817b6-199">Each file is a CSV file and is approximately 60GB in size.</span></span>
<span data-ttu-id="817b6-200">5.</span><span class="sxs-lookup"><span data-stu-id="817b6-200">5.</span></span> <span data-ttu-id="817b6-201">Renommer hello fichier toohello du mois hello qu’il contient des données.</span><span class="sxs-lookup"><span data-stu-id="817b6-201">Rename hello file toohello name of hello month that it contains data for.</span></span> <span data-ttu-id="817b6-202">Par exemple, fichier hello contenant hello janvier données serait nommé *January.csv*.</span><span class="sxs-lookup"><span data-stu-id="817b6-202">For example, hello file containing hello January data would be named *January.csv*.</span></span>
<span data-ttu-id="817b6-203">6.</span><span class="sxs-lookup"><span data-stu-id="817b6-203">6.</span></span> <span data-ttu-id="817b6-204">Répétez le toodownload les étapes 2 et 5 un fichier pour chaque hello 12 mois dans 2013.</span><span class="sxs-lookup"><span data-stu-id="817b6-204">Repeat steps 2 and 5 toodownload a file for each of hello 12 months in 2013.</span></span> <span data-ttu-id="817b6-205">Vous devez au minimum un didacticiel de hello toorun fichier.</span><span class="sxs-lookup"><span data-stu-id="817b6-205">You will need a minimum of one file toorun hello tutorial.</span></span>

<span data-ttu-id="817b6-206">**tooupload hello flight delay données tooAzure stockage d’objets Blob**</span><span class="sxs-lookup"><span data-stu-id="817b6-206">**tooupload hello flight delay data tooAzure Blob storage**</span></span>

1. <span data-ttu-id="817b6-207">Préparer les paramètres hello :</span><span class="sxs-lookup"><span data-stu-id="817b6-207">Prepare hello parameters:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="817b6-208">Nom de la variable</span><span class="sxs-lookup"><span data-stu-id="817b6-208">Variable Name</span></span></th><th><span data-ttu-id="817b6-209">Remarques</span><span class="sxs-lookup"><span data-stu-id="817b6-209">Notes</span></span></th></tr>
    <tr><td><span data-ttu-id="817b6-210">$storageAccountName</span><span class="sxs-lookup"><span data-stu-id="817b6-210">$storageAccountName</span></span></td><td><span data-ttu-id="817b6-211">compte de stockage Azure où vous souhaitez que les données hello tooupload de Hello.</span><span class="sxs-lookup"><span data-stu-id="817b6-211">hello Azure Storage account where you want tooupload hello data to.</span></span></td></tr>
    <tr><td><span data-ttu-id="817b6-212">$blobContainerName</span><span class="sxs-lookup"><span data-stu-id="817b6-212">$blobContainerName</span></span></td><td><span data-ttu-id="817b6-213">conteneur d’objets Blob Hello où vous souhaitez que les données hello tooupload.</span><span class="sxs-lookup"><span data-stu-id="817b6-213">hello Blob container where you want tooupload hello data to.</span></span></td></tr>
    </table>
2. <span data-ttu-id="817b6-214">Ouvrez Azure PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="817b6-214">Open Azure PowerShell ISE.</span></span>
<span data-ttu-id="817b6-215">3.</span><span class="sxs-lookup"><span data-stu-id="817b6-215">3.</span></span> <span data-ttu-id="817b6-216">Collez hello script suivant dans le volet de script hello :</span><span class="sxs-lookup"><span data-stu-id="817b6-216">Paste hello following script into hello script pane:</span></span>

    ```powershell
    [CmdletBinding()]
    Param(

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure storage account name for creating a new HDInsight cluster. If hello account doesn't exist, hello script will create one.")]
        [String]$storageAccountName,

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure blob container name for creating a new HDInsight cluster. If not specified, hello HDInsight cluster name will be used.")]
        [String]$blobContainerName
    )

    #Region - Variables
    $localFolder = "C:\Tutorials\FlightDelay\2013Data"  # hello source folder
    $destFolder = "tutorials/flightdelay/2013data"     #hello blob name prefix for hello files toobe uploaded
    #EndRegion

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #Region - Validate user input
    Write-Host "`nValidating hello Azure Storage account and hello Blob container..." -ForegroundColor Green
    # Validate hello Storage account
    if (-not (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}))
    {
        Write-Host "hello storage account, $storageAccountName, doesn't exist." -ForegroundColor Red
        exit
    }
    else{
        $resourceGroupName = (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}).ResourceGroupName
    }

    # Validate hello container
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    if (-not (Get-AzureStorageContainer -Context $storageContext |Where-Object{$_.Name -eq $blobContainerName}))
    {
        Write-Host "hello Blob container, $blobContainerName, doesn't exist" -ForegroundColor Red
        Exit
    }
    #EngRegion

    #Region - Copy hello file from local workstation tooAzure Blob storage
    if (test-path -Path $localFolder)
    {
        foreach ($item in Get-ChildItem -Path $localFolder){
            $fileName = "$localFolder\$item"
            $blobName = "$destFolder/$item"

            Write-Host "Copying $fileName too$blobName" -ForegroundColor Green

            Set-AzureStorageBlobContent -File $fileName -Container $blobContainerName -Blob $blobName -Context $storageContext
        }
    }
    else
    {
        Write-Host "hello source folder on hello workstation doesn't exist" -ForegroundColor Red
    }

    # List hello uploaded files on HDInsight
    Get-AzureStorageBlob -Container $blobContainerName  -Context $storageContext -Prefix $destFolder
    #EndRegion
    ```
4. <span data-ttu-id="817b6-217">Appuyez sur **F5** script de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="817b6-217">Press **F5** toorun hello script.</span></span>

<span data-ttu-id="817b6-218">Si vous choisissez toouse une autre méthode de téléchargement des fichiers de hello, assurez-vous que le chemin d’accès du fichier hello est didacticiels/flightdelay/données.</span><span class="sxs-lookup"><span data-stu-id="817b6-218">If you choose toouse a different method for uploading hello files, please make sure hello file path is tutorials/flightdelay/data.</span></span> <span data-ttu-id="817b6-219">syntaxe Hello pour accéder aux fichiers de hello est :</span><span class="sxs-lookup"><span data-stu-id="817b6-219">hello syntax for accessing hello files is:</span></span>

    wasb://<ContainerName>@<StorageAccountName>.blob.core.windows.net/tutorials/flightdelay/data

<span data-ttu-id="817b6-220">Hello chemin didacticiels/flightdelay/données est un dossier virtuel de hello que vous avez créé lorsque vous avez téléchargé les fichiers hello.</span><span class="sxs-lookup"><span data-stu-id="817b6-220">hello path tutorials/flightdelay/data is hello virtual folder you created when you uploaded hello files.</span></span> <span data-ttu-id="817b6-221">Assurez-vous qu'il existe 12 fichiers, un par mois.</span><span class="sxs-lookup"><span data-stu-id="817b6-221">Verify that there are 12 files, one for each month.</span></span>

> [!NOTE]
> <span data-ttu-id="817b6-222">Vous devez mettre à jour hello ruche requête tooread à partir de l’emplacement du nouveau hello.</span><span class="sxs-lookup"><span data-stu-id="817b6-222">You must update hello Hive query tooread from hello new location.</span></span>
>
> <span data-ttu-id="817b6-223">Vous devez configurer hello conteneur accès autorisation toobe public ou lier toohello de compte de stockage hello cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="817b6-223">You must either configure hello container access permission toobe public or bind hello Storage account toohello HDInsight cluster.</span></span> <span data-ttu-id="817b6-224">Sinon, chaîne de requête Hive hello ne sera pas en mesure de tooaccess des fichiers de données hello.</span><span class="sxs-lookup"><span data-stu-id="817b6-224">Otherwise, hello Hive query string will not be able tooaccess hello data files.</span></span>

- - -

## <span data-ttu-id="817b6-225"><a id="appendix-b"></a>Annexe B - Création et téléchargement d’un script HiveQL</span><span class="sxs-lookup"><span data-stu-id="817b6-225"><a id="appendix-b"></a>Appendix B - Create and upload a HiveQL script</span></span>
<span data-ttu-id="817b6-226">À l’aide d’Azure PowerShell, vous pouvez exécuter plusieurs instructions HiveQL une à une heure ou package hello HiveQL instruction dans un fichier de script.</span><span class="sxs-lookup"><span data-stu-id="817b6-226">Using Azure PowerShell, you can run multiple HiveQL statements one at a time, or package hello HiveQL statement into a script file.</span></span> <span data-ttu-id="817b6-227">Cette section vous montre comment toocreate un script HiveQL hello de chargement de script et tooAzure stockage d’objets Blob à l’aide d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="817b6-227">This section shows you how toocreate a HiveQL script and upload hello script tooAzure Blob storage by using Azure PowerShell.</span></span> <span data-ttu-id="817b6-228">Ruche requiert hello HiveQL scripts toobe stockée dans le stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="817b6-228">Hive requires hello HiveQL scripts toobe stored in Azure Blob storage.</span></span>

<span data-ttu-id="817b6-229">Hello script HiveQL effectuera suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="817b6-229">hello HiveQL script will perform hello following:</span></span>

1. <span data-ttu-id="817b6-230">**Supprimer la table de delays_raw hello**, au cas où la table hello existe déjà.</span><span class="sxs-lookup"><span data-stu-id="817b6-230">**Drop hello delays_raw table**, in case hello table already exists.</span></span>
2. <span data-ttu-id="817b6-231">**Créer une table Hive externe hello delays_raw** pointant d’emplacement de stockage d’objets Blob toohello avec les fichiers de retard de vol hello.</span><span class="sxs-lookup"><span data-stu-id="817b6-231">**Create hello delays_raw external Hive table** pointing toohello Blob storage location with hello flight delay files.</span></span> <span data-ttu-id="817b6-232">Cette requête spécifie les champs délimités par « , » et les lignes se terminant par « \n ».</span><span class="sxs-lookup"><span data-stu-id="817b6-232">This query specifies that fields are delimited by "," and that lines are terminated by "\n".</span></span> <span data-ttu-id="817b6-233">Cela pose un problème lorsque les valeurs de champ contiennent des virgules, car la ruche ne peut pas différencier une virgule est un délimiteur de champ et un qui fait partie d’une valeur de champ (qui est le cas de hello dans les valeurs de champ pour l’origine\_Ville\_nom et DEST\_ Ville\_nom).</span><span class="sxs-lookup"><span data-stu-id="817b6-233">This poses a problem when field values contain commas because Hive cannot differentiate between a comma that is a field delimiter and a one that is part of a field value (which is hello case in field values for ORIGIN\_CITY\_NAME and DEST\_CITY\_NAME).</span></span> <span data-ttu-id="817b6-234">tooaddress, hello requête crée les colonnes TEMP données toohold sont incorrectement divisées en colonnes.</span><span class="sxs-lookup"><span data-stu-id="817b6-234">tooaddress this, hello query creates TEMP columns toohold data that is incorrectly split into columns.</span></span>
3. <span data-ttu-id="817b6-235">**Supprimer la table de retards hello**, au cas où la table hello existe déjà.</span><span class="sxs-lookup"><span data-stu-id="817b6-235">**Drop hello delays table**, in case hello table already exists.</span></span>
4. <span data-ttu-id="817b6-236">**Créer la table de retards hello**.</span><span class="sxs-lookup"><span data-stu-id="817b6-236">**Create hello delays table**.</span></span> <span data-ttu-id="817b6-237">Il est utile tooclean les données de hello avant tout traitement supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="817b6-237">It is helpful tooclean up hello data before further processing.</span></span> <span data-ttu-id="817b6-238">Cette requête crée une nouvelle table, *retards*, à partir de la table de delays_raw hello.</span><span class="sxs-lookup"><span data-stu-id="817b6-238">This query creates a new table, *delays*, from hello delays_raw table.</span></span> <span data-ttu-id="817b6-239">Notez que les colonnes TEMP hello (comme indiqué précédemment) ne sont pas copiés et ce hello **sous-chaîne** fonction est guillemets tooremove utilisés à partir des données de hello.</span><span class="sxs-lookup"><span data-stu-id="817b6-239">Note that hello TEMP columns (as mentioned previously) are not copied, and that hello **substring** function is used tooremove quotation marks from hello data.</span></span>
5. <span data-ttu-id="817b6-240">**Calcul résultats hello hello météo moyenne délai et les groupes par nom de ville.**</span><span class="sxs-lookup"><span data-stu-id="817b6-240">**Compute hello average weather delay and groups hello results by city name.**</span></span> <span data-ttu-id="817b6-241">Il produira également de stockage de tooBlob résultats hello.</span><span class="sxs-lookup"><span data-stu-id="817b6-241">It will also output hello results tooBlob storage.</span></span> <span data-ttu-id="817b6-242">Notez cette requête hello supprimera les apostrophes à partir des données de hello et exclut les lignes où la valeur hello pour **weather_delay** a la valeur null.</span><span class="sxs-lookup"><span data-stu-id="817b6-242">Note that hello query will remove apostrophes from hello data and will exclude rows where hello value for **weather_delay** is null.</span></span> <span data-ttu-id="817b6-243">Ces mesures sont nécessaires, car Sqoop, qui est utilisé ultérieurement dans ce didacticiel, ne gère pas correctement ces valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="817b6-243">This is necessary because Sqoop, used later in this tutorial, doesn't handle those values gracefully by default.</span></span>

<span data-ttu-id="817b6-244">Pour obtenir une liste complète des commandes de HiveQL hello, consultez [Hive Data Definition Language][hadoop-hiveql].</span><span class="sxs-lookup"><span data-stu-id="817b6-244">For a full list of hello HiveQL commands, see [Hive Data Definition Language][hadoop-hiveql].</span></span> <span data-ttu-id="817b6-245">Chaque commande HiveQL doit se terminer par un point virgule.</span><span class="sxs-lookup"><span data-stu-id="817b6-245">Each HiveQL command must terminate with a semicolon.</span></span>

<span data-ttu-id="817b6-246">**toocreate un fichier de script HiveQL**</span><span class="sxs-lookup"><span data-stu-id="817b6-246">**toocreate a HiveQL script file**</span></span>

1. <span data-ttu-id="817b6-247">Préparer les paramètres hello :</span><span class="sxs-lookup"><span data-stu-id="817b6-247">Prepare hello parameters:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="817b6-248">Nom de la variable</span><span class="sxs-lookup"><span data-stu-id="817b6-248">Variable Name</span></span></th><th><span data-ttu-id="817b6-249">Remarques</span><span class="sxs-lookup"><span data-stu-id="817b6-249">Notes</span></span></th></tr>
    <tr><td><span data-ttu-id="817b6-250">$storageAccountName</span><span class="sxs-lookup"><span data-stu-id="817b6-250">$storageAccountName</span></span></td><td><span data-ttu-id="817b6-251">Hello compte de stockage Azure où vous souhaitez que tooupload hello script HiveQL.</span><span class="sxs-lookup"><span data-stu-id="817b6-251">hello Azure Storage account where you want tooupload hello HiveQL script to.</span></span></td></tr>
    <tr><td><span data-ttu-id="817b6-252">$blobContainerName</span><span class="sxs-lookup"><span data-stu-id="817b6-252">$blobContainerName</span></span></td><td><span data-ttu-id="817b6-253">conteneur d’objets Blob Hello où vous souhaitez que tooupload hello script HiveQL.</span><span class="sxs-lookup"><span data-stu-id="817b6-253">hello Blob container where you want tooupload hello HiveQL script to.</span></span></td></tr>
    </table>
2. <span data-ttu-id="817b6-254">Ouvrez Azure PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="817b6-254">Open Azure PowerShell ISE.</span></span>
<span data-ttu-id="817b6-255">3.</span><span class="sxs-lookup"><span data-stu-id="817b6-255">3.</span></span> <span data-ttu-id="817b6-256">Copiez et collez le script suivant dans le volet de script hello de hello :</span><span class="sxs-lookup"><span data-stu-id="817b6-256">Copy and paste hello following script into hello script pane:</span></span>

    ```powershell
    [CmdletBinding()]
    Param(

        # Azure Blob storage variables
        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure storage account name for creating a new HDInsight cluster. If hello account doesn't exist, hello script will create one.")]
        [String]$storageAccountName,

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure blob container name for creating a new HDInsight cluster. If not specified, hello HDInsight cluster name will be used.")]
        [String]$blobContainerName
    )

    #region - Define variables
    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    # hello HiveQL script file is exported as this file before it's uploaded tooBlob storage
    $hqlLocalFileName = "e:\tutorials\flightdelay\flightdelays.hql"

    # hello HiveQL script file will be uploaded tooBlob storage as this blob name
    $hqlBlobName = "tutorials/flightdelay/flightdelays.hql"

    # These two constants are used by hello HiveQL script file
    #$srcDataFolder = "tutorials/flightdelay/data"
    $dstDataFolder = "/tutorials/flightdelay/output"
    #endregion

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #Region - Validate user input
    Write-Host "`nValidating hello Azure Storage account and hello Blob container..." -ForegroundColor Green
    # Validate hello Storage account
    if (-not (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}))
    {
        Write-Host "hello storage account, $storageAccountName, doesn't exist." -ForegroundColor Red
        exit
    }
    else{
        $resourceGroupName = (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}).ResourceGroupName
    }

    # Validate hello container
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    if (-not (Get-AzureStorageContainer -Context $storageContext |Where-Object{$_.Name -eq $blobContainerName}))
    {
        Write-Host "hello Blob container, $blobContainerName, doesn't exist" -ForegroundColor Red
        Exit
    }
    #EngRegion

    #region - Validate hello file and file path

    # Check if a file with hello same file name already exists on hello workstation
    Write-Host "`nvalidating hello folder structure on hello workstation for saving hello HQL script file ..."  -ForegroundColor Green
    if (test-path $hqlLocalFileName){

        $isDelete = Read-Host 'hello file, ' $hqlLocalFileName ', exists.  Do you want toooverwirte it? (Y/N)'

        if ($isDelete.ToLower() -ne "y")
        {
            Exit
        }
    }

    # Create hello folder if it doesn't exist
    $folder = split-path $hqlLocalFileName
    if (-not (test-path $folder))
    {
        Write-Host "`nCreating folder, $folder ..." -ForegroundColor Green

        new-item $folder -ItemType directory
    }
    #end region

    #region - Write hello Hive script into a local file
    Write-Host "`nWriting hello Hive script into a file on your workstation ..." `
                -ForegroundColor Green

    $hqlDropDelaysRaw = "DROP TABLE delays_raw;"

    $hqlCreateDelaysRaw = "CREATE EXTERNAL TABLE delays_raw (" +
            "YEAR string, " +
            "FL_DATE string, " +
            "UNIQUE_CARRIER string, " +
            "CARRIER string, " +
            "FL_NUM string, " +
            "ORIGIN_AIRPORT_ID string, " +
            "ORIGIN string, " +
            "ORIGIN_CITY_NAME string, " +
            "ORIGIN_CITY_NAME_TEMP string, " +
            "ORIGIN_STATE_ABR string, " +
            "DEST_AIRPORT_ID string, " +
            "DEST string, " +
            "DEST_CITY_NAME string, " +
            "DEST_CITY_NAME_TEMP string, " +
            "DEST_STATE_ABR string, " +
            "DEP_DELAY_NEW float, " +
            "ARR_DELAY_NEW float, " +
            "CARRIER_DELAY float, " +
            "WEATHER_DELAY float, " +
            "NAS_DELAY float, " +
            "SECURITY_DELAY float, " +
            "LATE_AIRCRAFT_DELAY float) " +
        "ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' " +
        "LINES TERMINATED BY '\n' " +
        "STORED AS TEXTFILE " +
        "LOCATION 'wasb://flightdelay@hditutorialdata.blob.core.windows.net/2013Data';"

    $hqlDropDelays = "DROP TABLE delays;"

    $hqlCreateDelays = "CREATE TABLE delays AS " +
        "SELECT YEAR AS year, " +
            "FL_DATE AS flight_date, " +
            "substring(UNIQUE_CARRIER, 2, length(UNIQUE_CARRIER) -1) AS unique_carrier, " +
            "substring(CARRIER, 2, length(CARRIER) -1) AS carrier, " +
            "substring(FL_NUM, 2, length(FL_NUM) -1) AS flight_num, " +
            "ORIGIN_AIRPORT_ID AS origin_airport_id, " +
            "substring(ORIGIN, 2, length(ORIGIN) -1) AS origin_airport_code, " +
            "substring(ORIGIN_CITY_NAME, 2) AS origin_city_name, " +
            "substring(ORIGIN_STATE_ABR, 2, length(ORIGIN_STATE_ABR) -1)  AS origin_state_abr, " +
            "DEST_AIRPORT_ID AS dest_airport_id, " +
            "substring(DEST, 2, length(DEST) -1) AS dest_airport_code, " +
            "substring(DEST_CITY_NAME,2) AS dest_city_name, " +
            "substring(DEST_STATE_ABR, 2, length(DEST_STATE_ABR) -1) AS dest_state_abr, " +
            "DEP_DELAY_NEW AS dep_delay_new, " +
            "ARR_DELAY_NEW AS arr_delay_new, " +
            "CARRIER_DELAY AS carrier_delay, " +
            "WEATHER_DELAY AS weather_delay, " +
            "NAS_DELAY AS nas_delay, " +
            "SECURITY_DELAY AS security_delay, " +
            "LATE_AIRCRAFT_DELAY AS late_aircraft_delay " +
        "FROM delays_raw;"

    $hqlInsertLocal = "INSERT OVERWRITE DIRECTORY '$dstDataFolder' " +
        "SELECT regexp_replace(origin_city_name, '''', ''), " +
            "avg(weather_delay) " +
        "FROM delays " +
        "WHERE weather_delay IS NOT NULL " +
        "GROUP BY origin_city_name;"

    $hqlScript = $hqlDropDelaysRaw + $hqlCreateDelaysRaw + $hqlDropDelays + $hqlCreateDelays + $hqlInsertLocal

    $hqlScript | Out-File $hqlLocalFileName -Encoding ascii -Force
    #endregion

    #region - Upload hello Hive script toohello default Blob container
    Write-Host "`nUploading hello Hive script toohello default Blob container ..." -ForegroundColor Green

    # Create a storage context object
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Upload hello file from local workstation tooBlob storage
    Set-AzureStorageBlobContent -File $hqlLocalFileName -Container $blobContainerName -Blob $hqlBlobName -Context $destContext
    #endregion

    Write-host "`nEnd of hello PowerShell script" -ForegroundColor Green
    ```

    <span data-ttu-id="817b6-257">Voici les variables hello utilisées dans le script de hello :</span><span class="sxs-lookup"><span data-stu-id="817b6-257">Here are hello variables used in hello script:</span></span>

   * <span data-ttu-id="817b6-258">**$hqlLocalFileName** -hello script enregistre fichier de script HiveQL hello localement avant de le télécharger tooBlob stockage.</span><span class="sxs-lookup"><span data-stu-id="817b6-258">**$hqlLocalFileName** - hello script saves hello HiveQL script file locally before uploading it tooBlob storage.</span></span> <span data-ttu-id="817b6-259">Il s’agit de nom de fichier hello.</span><span class="sxs-lookup"><span data-stu-id="817b6-259">This is hello file name.</span></span> <span data-ttu-id="817b6-260">la valeur par défaut Hello est <u>C:\tutorials\flightdelay\flightdelays.hql</u>.</span><span class="sxs-lookup"><span data-stu-id="817b6-260">hello default value is <u>C:\tutorials\flightdelay\flightdelays.hql</u>.</span></span>
   * <span data-ttu-id="817b6-261">**$hqlBlobName** -hello HiveQL script blob nom du fichier utilisé dans hello le stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="817b6-261">**$hqlBlobName** - This is hello HiveQL script file blob name used in hello Azure Blob storage.</span></span> <span data-ttu-id="817b6-262">valeur par défaut de Hello est tutorials/flightdelay/flightdelays.hql.</span><span class="sxs-lookup"><span data-stu-id="817b6-262">hello default value is tutorials/flightdelay/flightdelays.hql.</span></span> <span data-ttu-id="817b6-263">Étant donné que hello fichier sera écrit directement tooAzure stockage d’objets Blob, il n’est pas un « / » au début de hello du nom d’objet blob hello.</span><span class="sxs-lookup"><span data-stu-id="817b6-263">Because hello file will be written directly tooAzure Blob storage, there is NOT a "/" at hello beginning of hello blob name.</span></span> <span data-ttu-id="817b6-264">Si vous voulez tooaccess hello depuis le stockage Blob, vous devez tooadd « / » au début de hello hello du nom de fichier.</span><span class="sxs-lookup"><span data-stu-id="817b6-264">If you want tooaccess hello file from Blob storage, you will need tooadd a "/" at hello beginning of hello file name.</span></span>
   * <span data-ttu-id="817b6-265">**$srcDataFolder** et **$dstDataFolder** - = "tutorials/flightdelay/data" = "tutorials/flightdelay/output"</span><span class="sxs-lookup"><span data-stu-id="817b6-265">**$srcDataFolder** and **$dstDataFolder** - = "tutorials/flightdelay/data" = "tutorials/flightdelay/output"</span></span>

- - -
## <span data-ttu-id="817b6-266"><a id="appendix-c"></a>Annexe C - préparer une base de données SQL Azure hello sortie de travail Sqoop</span><span class="sxs-lookup"><span data-stu-id="817b6-266"><a id="appendix-c"></a>Appendix C - Prepare an Azure SQL database for hello Sqoop job output</span></span>
<span data-ttu-id="817b6-267">**base de données SQL tooprepare hello (fusionne avec hello Sqoop script)**</span><span class="sxs-lookup"><span data-stu-id="817b6-267">**tooprepare hello SQL database (merge this with hello Sqoop script)**</span></span>

1. <span data-ttu-id="817b6-268">Préparer les paramètres hello :</span><span class="sxs-lookup"><span data-stu-id="817b6-268">Prepare hello parameters:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="817b6-269">Nom de la variable</span><span class="sxs-lookup"><span data-stu-id="817b6-269">Variable Name</span></span></th><th><span data-ttu-id="817b6-270">Remarques</span><span class="sxs-lookup"><span data-stu-id="817b6-270">Notes</span></span></th></tr>
    <tr><td><span data-ttu-id="817b6-271">$sqlDatabaseServerName</span><span class="sxs-lookup"><span data-stu-id="817b6-271">$sqlDatabaseServerName</span></span></td><td><span data-ttu-id="817b6-272">nom de Hello du serveur de base de données SQL Azure hello.</span><span class="sxs-lookup"><span data-stu-id="817b6-272">hello name of hello Azure SQL database server.</span></span> <span data-ttu-id="817b6-273">Entrez rien toocreate un nouveau serveur.</span><span class="sxs-lookup"><span data-stu-id="817b6-273">Enter nothing toocreate a new server.</span></span></td></tr>
    <tr><td><span data-ttu-id="817b6-274">$sqlDatabaseUsername</span><span class="sxs-lookup"><span data-stu-id="817b6-274">$sqlDatabaseUsername</span></span></td><td><span data-ttu-id="817b6-275">nom de connexion Hello pour le serveur de base de données SQL Azure hello.</span><span class="sxs-lookup"><span data-stu-id="817b6-275">hello login name for hello Azure SQL database server.</span></span> <span data-ttu-id="817b6-276">Si $sqlDatabaseServerName est un serveur existant, connexion de hello et le mot de passe sont tooauthenticate utilisé avec le serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="817b6-276">If $sqlDatabaseServerName is an existing server, hello login and login password are used tooauthenticate with hello server.</span></span> <span data-ttu-id="817b6-277">Sinon, elles sont utilisée toocreate un nouveau serveur.</span><span class="sxs-lookup"><span data-stu-id="817b6-277">Otherwise they are used toocreate a new server.</span></span></td></tr>
    <tr><td><span data-ttu-id="817b6-278">$sqlDatabasePassword</span><span class="sxs-lookup"><span data-stu-id="817b6-278">$sqlDatabasePassword</span></span></td><td><span data-ttu-id="817b6-279">Hello mot de passe pour le serveur de base de données SQL Azure hello.</span><span class="sxs-lookup"><span data-stu-id="817b6-279">hello login password for hello Azure SQL database server.</span></span></td></tr>
    <tr><td><span data-ttu-id="817b6-280">$sqlDatabaseLocation</span><span class="sxs-lookup"><span data-stu-id="817b6-280">$sqlDatabaseLocation</span></span></td><td><span data-ttu-id="817b6-281">Cette valeur est uniquement utilisée lors de la création d’un nouveau serveur de base de données Azure.</span><span class="sxs-lookup"><span data-stu-id="817b6-281">This value is used only when you're creating a new Azure database server.</span></span></td></tr>
    <tr><td><span data-ttu-id="817b6-282">$sqlDatabaseName</span><span class="sxs-lookup"><span data-stu-id="817b6-282">$sqlDatabaseName</span></span></td><td><span data-ttu-id="817b6-283">base de données SQL Hello utilisé table de AvgDelays toocreate hello pour le travail de Sqoop hello.</span><span class="sxs-lookup"><span data-stu-id="817b6-283">hello SQL database used toocreate hello AvgDelays table for hello Sqoop job.</span></span> <span data-ttu-id="817b6-284">Si vous laissez cette valeur vide, une base de données intitulée HDISqoop est créée.</span><span class="sxs-lookup"><span data-stu-id="817b6-284">Leaving it blank will create a database called HDISqoop.</span></span> <span data-ttu-id="817b6-285">nom de la table Hello pour hello sortie de travail Sqoop est AvgDelays.</span><span class="sxs-lookup"><span data-stu-id="817b6-285">hello table name for hello Sqoop job output is AvgDelays.</span></span> </td></tr>
    </table>
2. <span data-ttu-id="817b6-286">Ouvrez Azure PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="817b6-286">Open Azure PowerShell ISE.</span></span>
<span data-ttu-id="817b6-287">3.</span><span class="sxs-lookup"><span data-stu-id="817b6-287">3.</span></span> <span data-ttu-id="817b6-288">Copiez et collez le script suivant dans le volet de script hello de hello :</span><span class="sxs-lookup"><span data-stu-id="817b6-288">Copy and paste hello following script into hello script pane:</span></span>

    ```powershell
    [CmdletBinding()]
    Param(

        # Azure Resource group variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure resource group name. It will be created if it doesn't exist.")]
        [String]$resourceGroupName,

        # SQL database server variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database Server Name. It will be created if it doesn't exist.")]
        [String]$sqlDatabaseServer,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database admin user.")]
        [String]$sqlDatabaseLogin,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database admin user password.")]
        [String]$sqlDatabasePassword,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello region toocreate hello Database in.")]
        [String]$sqlDatabaseLocation,   #For example, West US.

        # SQL database variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello database name. It will be created if it doesn't exist.")]
        [String]$sqlDatabaseName # specify hello database name if you have one created. Otherwise use "" toohave hello script create one for you.
    )

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    #region - Constants and variables

    # IP address REST service used for retrieving external IP address and creating firewall rules
    [String]$ipAddressRestService = "http://bot.whatismyipaddress.com"
    [String]$fireWallRuleName = "FlightDelay"

    # SQL database variables
    [String]$sqlDatabaseMaxSizeGB = 10

    #SQL query string for creating AvgDelays table
    [String]$sqlDatabaseTableName = "AvgDelays"
    [String]$sqlCreateAvgDelaysTable = " CREATE TABLE [dbo].[$sqlDatabaseTableName](
                [origin_city_name] [nvarchar](50) NOT NULL,
                [weather_delay] float,
            CONSTRAINT [PK_$sqlDatabaseTableName] PRIMARY KEY CLUSTERED
            (
                [origin_city_name] ASC
            )
            )"
    #endregion

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #region - Create and validate Azure resouce group
    try{
        Get-AzureRmResourceGroup -Name $resourceGroupName
    }
    catch{
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $sqlDatabaseLocation
    }

    #EndRegion

    #region - Create and validate Azure SQL database server
    try{
        Get-AzureRmSqlServer -ServerName $sqlDatabaseServer -ResourceGroupName $resourceGroupName}
    catch{
        Write-Host "`nCreating SQL Database server ..."  -ForegroundColor Green

        $sqlDatabasePW = ConvertTo-SecureString -String $sqlDatabasePassword -AsPlainText -Force
        $credential = New-Object System.Management.Automation.PSCredential($sqlDatabaseLogin,$sqlDatabasePW)

        $sqlDatabaseServer = (New-AzureRmSqlServer -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -SqlAdministratorCredentials $credential -Location $sqlDatabaseLocation).ServerName
        Write-Host "`tThe new SQL database server name is $sqlDatabaseServer." -ForegroundColor Cyan

        Write-Host "`nCreating firewall rule, $fireWallRuleName ..." -ForegroundColor Green
        $workstationIPAddress = Invoke-RestMethod $ipAddressRestService
        New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -FirewallRuleName "$fireWallRuleName-workstation" -StartIpAddress $workstationIPAddress -EndIpAddress $workstationIPAddress

        #tooallow other Azure services tooaccess hello server add a firewall rule and set both hello StartIpAddress and EndIpAddress too0.0.0.0. Note that this allows Azure traffic from any Azure subscription tooaccess hello server.
        New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -FirewallRuleName "$fireWallRuleName-Azureservices" -StartIpAddress "0.0.0.0" -EndIpAddress "0.0.0.0"
    }

    #endregion

    #region - Create and validate Azure SQL database

    try {
        Get-AzureRmSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -DatabaseName $sqlDatabaseName
    }
    catch {
        Write-Host "`nCreating SQL Database, $sqlDatabaseName ..."  -ForegroundColor Green
        New-AzureRMSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -DatabaseName $sqlDatabaseName -Edition "Standard" -RequestedServiceObjectiveName "S1"
    }

    #endregion

    #region -  Execute an SQL command toocreate hello AvgDelays table

    Write-Host "`nCreating SQL Database table ..."  -ForegroundColor Green
    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $conn.open()
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.connection = $conn
    $cmd.commandtext = $sqlCreateAvgDelaysTable
    $cmd.executenonquery()

    $conn.close()

    Write-host "`nEnd of hello PowerShell script" -ForegroundColor Green
    ```

   > [!NOTE]
   > <span data-ttu-id="817b6-289">Hello script utilise un service de transfert (REST) état representational, http://bot.whatismyipaddress.com, tooretrieve votre adresse IP externe.</span><span class="sxs-lookup"><span data-stu-id="817b6-289">hello script uses a representational state transfer (REST) service, http://bot.whatismyipaddress.com, tooretrieve your external IP address.</span></span> <span data-ttu-id="817b6-290">adresse IP de Hello est utilisé pour la création d’une règle de pare-feu pour votre serveur de base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="817b6-290">hello IP address is used for creating a firewall rule for your SQL database server.</span></span>

    <span data-ttu-id="817b6-291">Voici quelques-unes des variables utilisées dans le script de hello :</span><span class="sxs-lookup"><span data-stu-id="817b6-291">Here are some variables used in hello script:</span></span>

   * <span data-ttu-id="817b6-292">**$ipAddressRestService** -valeur par défaut de hello est http://bot.whatismyipaddress.com. Il s’agit d’un service REST d’adresse IP publique permettant d’obtenir votre adresse IP externe.</span><span class="sxs-lookup"><span data-stu-id="817b6-292">**$ipAddressRestService** - hello default value is http://bot.whatismyipaddress.com. It is a public IP address REST service for getting your external IP address.</span></span> <span data-ttu-id="817b6-293">Vous pouvez utiliser d'autres services si vous voulez.</span><span class="sxs-lookup"><span data-stu-id="817b6-293">You can use other services if you want.</span></span> <span data-ttu-id="817b6-294">adresse IP externe Hello récupérée via le service de hello sera utilisé toocreate une règle de pare-feu pour votre serveur de base de données SQL Azure, afin que vous pouvez accéder de la base de données hello à partir de votre station de travail (en utilisant un script Windows PowerShell).</span><span class="sxs-lookup"><span data-stu-id="817b6-294">hello external IP address retrieved through hello service will be used toocreate a firewall rule for your Azure SQL database server, so that you can access hello database from your workstation (by using a Windows PowerShell script).</span></span>
   * <span data-ttu-id="817b6-295">**$fireWallRuleName** -il s’agit d’un nom de hello hello de règle de pare-feu pour le serveur de base de données SQL Azure hello.</span><span class="sxs-lookup"><span data-stu-id="817b6-295">**$fireWallRuleName** - This is hello name of hello firewall rule for hello Azure SQL database server.</span></span> <span data-ttu-id="817b6-296">le nom par défaut Hello est <u>FlightDelay</u>.</span><span class="sxs-lookup"><span data-stu-id="817b6-296">hello default name is <u>FlightDelay</u>.</span></span> <span data-ttu-id="817b6-297">Vous pouvez le renommer si vous voulez.</span><span class="sxs-lookup"><span data-stu-id="817b6-297">You can rename it if you want.</span></span>
   * <span data-ttu-id="817b6-298">**$sqlDatabaseMaxSizeGB** - Cette valeur est uniquement utilisée lors de la création d’un nouveau serveur de base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="817b6-298">**$sqlDatabaseMaxSizeGB** - This value is used only when you're creating a new Azure SQL database server.</span></span> <span data-ttu-id="817b6-299">valeur par défaut de Hello est de 10 Go.</span><span class="sxs-lookup"><span data-stu-id="817b6-299">hello default value is 10GB.</span></span> <span data-ttu-id="817b6-300">Une capacité de 10 Go est suffisante pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="817b6-300">10GB is sufficient for this tutorial.</span></span>
   * <span data-ttu-id="817b6-301">**$sqlDatabaseName** - Cette valeur est uniquement utilisée lors de la création d’une nouvelle base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="817b6-301">**$sqlDatabaseName** - This value is used only when you're creating a new Azure SQL database.</span></span> <span data-ttu-id="817b6-302">valeur par défaut de Hello est HDISqoop.</span><span class="sxs-lookup"><span data-stu-id="817b6-302">hello default value is HDISqoop.</span></span> <span data-ttu-id="817b6-303">Si vous renommez, vous devez mettre à jour en conséquence hello Sqoop de script Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="817b6-303">If you rename it, you must update hello Sqoop Windows PowerShell script accordingly.</span></span>
4. <span data-ttu-id="817b6-304">Appuyez sur **F5** script de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="817b6-304">Press **F5** toorun hello script.</span></span>
5. <span data-ttu-id="817b6-305">Valider la sortie du script hello.</span><span class="sxs-lookup"><span data-stu-id="817b6-305">Validate hello script output.</span></span> <span data-ttu-id="817b6-306">Assurez-vous que le script de hello s’est correctement exécutée.</span><span class="sxs-lookup"><span data-stu-id="817b6-306">Make sure hello script ran successfully.</span></span>

## <span data-ttu-id="817b6-307"><a id="nextsteps"></a> Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="817b6-307"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="817b6-308">Présent que vous savez comment tooupload un tooAzure fichier stockage d’objets Blob, comment toopopulate une ruche de table à l’aide de données hello du stockage d’objets Blob Azure, comment toorun Hive requêtes et comment toouse données tooexport de Sqoop à partir de la base de données SQL Azure de tooan HDFS.</span><span class="sxs-lookup"><span data-stu-id="817b6-308">Now you understand how tooupload a file tooAzure Blob storage, how toopopulate a Hive table by using hello data from Azure Blob storage, how toorun Hive queries, and how toouse Sqoop tooexport data from HDFS tooan Azure SQL database.</span></span> <span data-ttu-id="817b6-309">toolearn, voir hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="817b6-309">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="817b6-310">[Prise en main de HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="817b6-310">[Get started with HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="817b6-311">[Utilisation de Hive avec HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="817b6-311">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="817b6-312">[Utilisation d’Oozie avec HDInsight][hdinsight-use-oozie]</span><span class="sxs-lookup"><span data-stu-id="817b6-312">[Use Oozie with HDInsight][hdinsight-use-oozie]</span></span>
* <span data-ttu-id="817b6-313">[Utilisation de Sqoop avec HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="817b6-313">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="817b6-314">[Utilisation de Pig avec HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="817b6-314">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="817b6-315">[Développement de programmes MapReduce en Java pour HDInsight][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="817b6-315">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[rita-website]: http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time
[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[hadoop-hiveql]: https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL
[hadoop-shell-commands]: http://hadoop.apache.org/docs/r0.18.3/hdfs_shell.html

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx

[image-hdi-flightdelays-avgdelays-dataset]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.AvgDelays.DataSet.png
[img-hdi-flightdelays-run-hive-job-output]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.RunHiveJob.Output.png
[img-hdi-flightdelays-flow]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.Flow.png
