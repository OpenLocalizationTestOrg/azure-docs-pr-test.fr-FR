---
title: "Analyse des données sur les retards de vol avec Hadoop dans HDInsight - Azure | Microsoft Docs"
description: "Apprenez à utiliser un script Windows PowerShell pour créer un cluster HDInsight, exécuter une tâche Hive, exécuter une tache Sqoop et supprimer le cluster."
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
ms.openlocfilehash: 77790136c9bd3a4e3f7dcabea2fbe0bcffb6eafe
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="analyze-flight-delay-data-by-using-hive-in-hdinsight"></a><span data-ttu-id="a04a8-103">Analyse des données sur les retards de vol avec Hive dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="a04a8-103">Analyze flight delay data by using Hive in HDInsight</span></span>
<span data-ttu-id="a04a8-104">Hive permet d’exécuter des tâches Hadoop MapReduce via un langage de création de scripts semblable à SQL, nommé *[HiveQL][hadoop-hiveql]*, qui peut être appliqué à la synthèse, à l’envoi de requêtes et à l’analyse d’importants volumes de données.</span><span class="sxs-lookup"><span data-stu-id="a04a8-104">Hive provides a means of running Hadoop MapReduce jobs through an SQL-like scripting language called *[HiveQL][hadoop-hiveql]*, which can be applied towards summarizing, querying, and analyzing large volumes of data.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a04a8-105">Les étapes décrites dans ce document nécessitent un cluster HDInsight Windows.</span><span class="sxs-lookup"><span data-stu-id="a04a8-105">The steps in this document require a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="a04a8-106">Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="a04a8-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="a04a8-107">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="a04a8-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="a04a8-108">Pour les étapes fonctionnant avec un cluster basé sur Linux, consultez la rubrique [Analyse des données sur les retards de vol avec Hive dans HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md).</span><span class="sxs-lookup"><span data-stu-id="a04a8-108">For steps that work with a Linux-based cluster, see [Analyze flight delay data by using Hive in HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md).</span></span>

<span data-ttu-id="a04a8-109">L’un des principaux avantages d’Azure HDInsight est la séparation du calcul et du stockage des données.</span><span class="sxs-lookup"><span data-stu-id="a04a8-109">One of the major benefits of Azure HDInsight is the separation of data storage and compute.</span></span> <span data-ttu-id="a04a8-110">HDInsight utilise le stockage d’objets blob Azure pour stocker les données.</span><span class="sxs-lookup"><span data-stu-id="a04a8-110">HDInsight uses Azure Blob storage for data storage.</span></span> <span data-ttu-id="a04a8-111">Une tâche classique comprend trois parties :</span><span class="sxs-lookup"><span data-stu-id="a04a8-111">A typical job involves three parts:</span></span>

1. <span data-ttu-id="a04a8-112">**Le stockage des données dans un stockage d’objets blob Azure.**</span><span class="sxs-lookup"><span data-stu-id="a04a8-112">**Store data in Azure Blob storage.**</span></span>  <span data-ttu-id="a04a8-113">Par exemple, les données météorologiques, les données de capteur, les journaux web et, en l’occurrence, les données liées aux retards de vol, sont enregistrés dans un stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="a04a8-113">For example, weather data, sensor data, web logs, and in this case, flight delay data are saved into Azure Blob storage.</span></span>
2. <span data-ttu-id="a04a8-114">**L’exécution des tâches.**</span><span class="sxs-lookup"><span data-stu-id="a04a8-114">**Run jobs.**</span></span> <span data-ttu-id="a04a8-115">Au moment de traiter des données, exécutez un script Windows PowerShell (ou une application cliente) pour créer un cluster HDInsight, exécuter des tâches et supprimer le cluster.</span><span class="sxs-lookup"><span data-stu-id="a04a8-115">When it is time to process the data, you run a Windows PowerShell script (or a client application) to create an HDInsight cluster, run jobs, and delete the cluster.</span></span> <span data-ttu-id="a04a8-116">Les tâches enregistrent les données de sortie dans le stockage d'objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="a04a8-116">The jobs save output data to Azure Blob storage.</span></span> <span data-ttu-id="a04a8-117">Les données de sortie sont conservées même après la suppression du cluster.</span><span class="sxs-lookup"><span data-stu-id="a04a8-117">The output data is retained even after the cluster is deleted.</span></span> <span data-ttu-id="a04a8-118">De cette façon, vous ne payez que ce que vous avez consommé.</span><span class="sxs-lookup"><span data-stu-id="a04a8-118">This way, you pay for only what you have consumed.</span></span>
3. <span data-ttu-id="a04a8-119">**La récupération du résultat à partir du stockage d’objets blob Azure**ou, dans le cas présent, l’exportation des données vers une base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="a04a8-119">**Retrieve the output from Azure Blob storage**, or in this tutorial, export the data to an Azure SQL database.</span></span>

<span data-ttu-id="a04a8-120">Le schéma suivant illustre le scénario et la structure de ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="a04a8-120">The following diagram illustrates the scenario and the structure of this tutorial:</span></span>

![HDI.FlightDelays.flow][img-hdi-flightdelays-flow]

<span data-ttu-id="a04a8-122">Notez que les nombres indiqués dans le schéma correspondent aux titres des sections.</span><span class="sxs-lookup"><span data-stu-id="a04a8-122">Note that the numbers in the diagram correspond to the section titles.</span></span> <span data-ttu-id="a04a8-123">**M** représente le processus principal.</span><span class="sxs-lookup"><span data-stu-id="a04a8-123">**M** stands for the main process.</span></span> <span data-ttu-id="a04a8-124">**A** représente le contenu dans l'annexe.</span><span class="sxs-lookup"><span data-stu-id="a04a8-124">**A** stands for the content in the appendix.</span></span>

<span data-ttu-id="a04a8-125">La partie principale de ce didacticiel indique comment utiliser un script Windows PowerShell pour effectuer les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="a04a8-125">The main portion of the tutorial shows you how to use one Windows PowerShell script to perform the following tasks:</span></span>

* <span data-ttu-id="a04a8-126">Créez un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a04a8-126">Create an HDInsight cluster.</span></span>
* <span data-ttu-id="a04a8-127">Exécution d’une tâche Hive sur le cluster pour calculer les retards moyens enregistrés dans les aéroports.</span><span class="sxs-lookup"><span data-stu-id="a04a8-127">Run a Hive job on the cluster to calculate average delays at airports.</span></span> <span data-ttu-id="a04a8-128">Les données sur les retards de vol sont stockées dans un compte de stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="a04a8-128">The flight delay data is stored in an Azure Blob storage account.</span></span>
* <span data-ttu-id="a04a8-129">Exécution d'une tâche Sqoop pour exporter le résultat de la tâche Hive dans une base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="a04a8-129">Run a Sqoop job to export the Hive job output to an Azure SQL database.</span></span>
* <span data-ttu-id="a04a8-130">Suppression du cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a04a8-130">Delete the HDInsight cluster.</span></span>

<span data-ttu-id="a04a8-131">Dans les annexes, vous trouverez les instructions permettant de télécharger les données sur les retards de vol, de créer/télécharger une chaîne de requête Hive et de préparer une base de données SQL Azure pour la tâche Sqoop.</span><span class="sxs-lookup"><span data-stu-id="a04a8-131">In the appendixes, you can find the instructions for uploading flight delay data, creating/uploading a Hive query string, and preparing the Azure SQL database for the Sqoop job.</span></span>

> [!NOTE]
> <span data-ttu-id="a04a8-132">Les étapes de cette procédure sont spécifiques aux clusters HDInsight basés sur Windows.</span><span class="sxs-lookup"><span data-stu-id="a04a8-132">The steps in this document are specific to Windows-based HDInsight clusters.</span></span> <span data-ttu-id="a04a8-133">Pour les étapes fonctionnant avec un cluster basé sur Linux, consultez la rubrique [Analyse des données sur les retards de vol avec Hive dans HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md).</span><span class="sxs-lookup"><span data-stu-id="a04a8-133">For steps that work with a Linux-based cluster, see [Analyze flight delay data using Hive in HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md)</span></span>

### <a name="prerequisites"></a><span data-ttu-id="a04a8-134">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a04a8-134">Prerequisites</span></span>
<span data-ttu-id="a04a8-135">Avant de commencer ce didacticiel, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="a04a8-135">Before you begin this tutorial, you must have the following items:</span></span>

* <span data-ttu-id="a04a8-136">**Un abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="a04a8-136">**An Azure subscription**.</span></span> <span data-ttu-id="a04a8-137">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="a04a8-137">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="a04a8-138">**Un poste de travail sur lequel est installé Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="a04a8-138">**A workstation with Azure PowerShell**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="a04a8-139">La prise en charge de la gestion des ressources HDInsight par Azure PowerShell à l’aide d’Azure Service Manager est **déconseillée** ; elle a été supprimée le 1er janvier 2017.</span><span class="sxs-lookup"><span data-stu-id="a04a8-139">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="a04a8-140">Dans ce document, la procédure repose sur les nouvelles applets de commande HDInsight qui fonctionnent avec Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a04a8-140">The steps in this document use the new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="a04a8-141">Suivez les étapes indiquées dans [Installation et de configuration d’Azure PowerShell](/powershell/azureps-cmdlets-docs) pour installer la dernière version d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a04a8-141">Please follow the steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) to install the latest version of Azure PowerShell.</span></span> <span data-ttu-id="a04a8-142">Si vous devez modifier certains scripts pour utiliser les nouvelles applets de commande fonctionnant avec Azure Resource Manager, consultez [Migration vers les outils de développement Azure Resource Manager pour les clusters HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="a04a8-142">If you have scripts that need to be modified to use the new cmdlets that work with Azure Resource Manager, see [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

<span data-ttu-id="a04a8-143">**Fichiers utilisés dans ce didacticiel**</span><span class="sxs-lookup"><span data-stu-id="a04a8-143">**Files used in this tutorial**</span></span>

<span data-ttu-id="a04a8-144">Ce didacticiel utilise les données de ponctualité des vols des compagnies aériennes de la [Research and Innovative Technology Administration, Bureau of Transportation Statistics (RITA)][rita-website].</span><span class="sxs-lookup"><span data-stu-id="a04a8-144">This tutorial uses the on-time performance of airline flight data from [Research and Innovative Technology Administration, Bureau of Transportation Statistics or RITA][rita-website].</span></span>
<span data-ttu-id="a04a8-145">Une copie des données a été téléchargée dans un conteneur de stockage d’objets blob Azure avec l’autorisation d’accès aux objets blob publics.</span><span class="sxs-lookup"><span data-stu-id="a04a8-145">A copy of the data has been uploaded to an Azure Blob storage container with the Public Blob access permission.</span></span>
<span data-ttu-id="a04a8-146">Une partie de votre script PowerShell copie les données à partir du conteneur d'objets blob public dans le conteneur d'objets blob par défaut de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="a04a8-146">A part of your PowerShell script copies the data from the public blob container to the default blob container of your cluster.</span></span> <span data-ttu-id="a04a8-147">Le script HiveQL est également copié dans le même conteneur d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="a04a8-147">The HiveQL script is also copied to the same Blob container.</span></span>
<span data-ttu-id="a04a8-148">Pour savoir comment obtenir/télécharger les données sur votre propre compte de stockage et comment créer/télécharger le fichier de script HiveQL, consultez l’[annexe A](#appendix-a) et l’[annexe B](#appendix-b).</span><span class="sxs-lookup"><span data-stu-id="a04a8-148">If you want to learn how to get/upload the data to your own Storage account, and how to create/upload the HiveQL script file, see [Appendix A](#appendix-a) and [Appendix B](#appendix-b).</span></span>

<span data-ttu-id="a04a8-149">Le tableau suivant répertorie les fichiers utilisés dans ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="a04a8-149">The following table lists the files used in this tutorial:</span></span>

<table border="1">
<tr><th><span data-ttu-id="a04a8-150">Fichiers</span><span class="sxs-lookup"><span data-stu-id="a04a8-150">Files</span></span></th><th><span data-ttu-id="a04a8-151">Description</span><span class="sxs-lookup"><span data-stu-id="a04a8-151">Description</span></span></th></tr>
<tr><td>wasb://flightdelay@hditutorialdata.blob.core.windows.net/flightdelays.hql</td><td><span data-ttu-id="a04a8-152">Fichier script HiveQL utilisé par la tâche Hive.</span><span class="sxs-lookup"><span data-stu-id="a04a8-152">The HiveQL script file used by the Hive job.</span></span> <span data-ttu-id="a04a8-153">Ce script a été téléchargé dans un conteneur de stockage d'objets blob Azure avec l'autorisation d'accès publique.</span><span class="sxs-lookup"><span data-stu-id="a04a8-153">This script has been uploaded to an Azure Blob storage account with the public access.</span></span> <span data-ttu-id="a04a8-154">L’<a href="#appendix-b">annexe B</a> présente des instructions sur la préparation et le téléchargement de ce fichier sur votre propre compte de stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="a04a8-154"><a href="#appendix-b">Appendix B</a> has instructions on preparing and uploading this file to your own Azure Blob storage account.</span></span></td></tr>
<tr><td>wasb://flightdelay@hditutorialdata.blob.core.windows.net/2013Data</td><td><span data-ttu-id="a04a8-155">Données d’entrée pour la tâche Hive.</span><span class="sxs-lookup"><span data-stu-id="a04a8-155">Input data for the Hive job.</span></span> <span data-ttu-id="a04a8-156">Les données ont été téléchargées dans un compte de stockage d’objets blob Azure avec une autorisation d’accès public.</span><span class="sxs-lookup"><span data-stu-id="a04a8-156">The data has been uploaded to an Azure Blob storage account with the public access.</span></span> <span data-ttu-id="a04a8-157">L’<a href="#appendix-a">annexe A</a> présente des instructions sur l’obtention des données et leur téléchargement sur votre propre compte de stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="a04a8-157"><a href="#appendix-a">Appendix A</a> has instructions on getting the data and uploading the data to your own Azure Blob storage account.</span></span></td></tr>
<tr><td><span data-ttu-id="a04a8-158">\tutorials\flightdelays\output</span><span class="sxs-lookup"><span data-stu-id="a04a8-158">\tutorials\flightdelays\output</span></span></td><td><span data-ttu-id="a04a8-159">Chemin de sortie pour la tâche Hive.</span><span class="sxs-lookup"><span data-stu-id="a04a8-159">The output path for the Hive job.</span></span> <span data-ttu-id="a04a8-160">Le conteneur par défaut est utilisé pour le stockage des données de sortie.</span><span class="sxs-lookup"><span data-stu-id="a04a8-160">The default container is used for storing the output data.</span></span></td></tr>
<tr><td><span data-ttu-id="a04a8-161">\tutorials\flightdelays\jobstatus</span><span class="sxs-lookup"><span data-stu-id="a04a8-161">\tutorials\flightdelays\jobstatus</span></span></td><td><span data-ttu-id="a04a8-162">Le dossier de statut Hive sur le conteneur par défaut.</span><span class="sxs-lookup"><span data-stu-id="a04a8-162">The Hive job status folder on the default container.</span></span></td></tr>
</table>

## <a name="create-cluster-and-run-hivesqoop-jobs"></a><span data-ttu-id="a04a8-163">Création d’un cluster et exécution de tâches Hive/Sqoop</span><span class="sxs-lookup"><span data-stu-id="a04a8-163">Create cluster and run Hive/Sqoop jobs</span></span>
<span data-ttu-id="a04a8-164">Hadoop MapReduce correspond au traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="a04a8-164">Hadoop MapReduce is batch processing.</span></span> <span data-ttu-id="a04a8-165">La manière la plus économique d’exécuter une tâche Hive consiste à créer un cluster pour la tâche et à supprimer cette dernière une fois qu’elle est terminée.</span><span class="sxs-lookup"><span data-stu-id="a04a8-165">The most cost-effective way to run a Hive job is to create a cluster for the job, and delete the job after the job is completed.</span></span> <span data-ttu-id="a04a8-166">Le script suivant couvre le processus dans son intégralité.</span><span class="sxs-lookup"><span data-stu-id="a04a8-166">The following script covers the whole process.</span></span>
<span data-ttu-id="a04a8-167">Pour plus d’informations sur la création d’un cluster HDInsight et l’exécution de tâches Hive, consultez les rubriques [Création de clusters Hadoop dans HDInsight][hdinsight-provision] et [Utilisation de Hive avec HDInsight][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="a04a8-167">For more information on creating an HDInsight cluster and running Hive jobs, see [Create Hadoop clusters in HDInsight][hdinsight-provision] and [Use Hive with HDInsight][hdinsight-use-hive].</span></span>

<span data-ttu-id="a04a8-168">**Pour exécuter des requêtes Hive à l’aide d’Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="a04a8-168">**To run the Hive queries by Azure PowerShell**</span></span>

1. <span data-ttu-id="a04a8-169">Créez une base de données SQL Azure et la table pour le résultat de tâche Sqoop au moyen des instructions figurant dans l’ [annexe C](#appendix-c).</span><span class="sxs-lookup"><span data-stu-id="a04a8-169">Create an Azure SQL database and the table for the Sqoop job output by using the instructions in [Appendix C](#appendix-c).</span></span>
2. <span data-ttu-id="a04a8-170">Ouvrez Windows PowerShell ISE et exécutez le script suivant :</span><span class="sxs-lookup"><span data-stu-id="a04a8-170">Open Windows PowerShell ISE, and run the following script:</span></span>

    ```powershell
    $subscriptionID = "<Azure Subscription ID>"
    $nameToken = "<Enter an Alias>"

    ###########################################
    # You must configure the follwing variables
    # for an existing Azure SQL Database
    ###########################################
    $existingSqlDatabaseServerName = "<Azure SQL Database Server>"
    $existingSqlDatabaseLogin = "<Azure SQL Database Server Login>"
    $existingSqlDatabasePassword = "<Azure SQL Database Server login password>"
    $existingSqlDatabaseName = "<Azure SQL Database name>"

    $localFolder = "E:\Tutorials\Downloads\" # A temp location for copying files.
    $azcopyPath = "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy" # depends on the version, the folder can be different

    ###########################################
    # (Optional) configure the following variables
    ###########################################

    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $location = "EAST US 2"

    $HDInsightClusterName = $namePrefix + "hdi"
    $httpUserName = "admin"
    $httpPassword = "<Enter the Password>"

    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $HDInsightClusterName # use the cluster name

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

    # Create the default storage account
    New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName -Location $location -Type Standard_LRS

    # Create the default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey
    New-AzureStorageContainer -Name $defaultBlobContainerName -Context $defaultStorageAccountContext

    # Create the HDInsight cluster
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
    # Prepare the HiveQL script and source data
    ###########################################

    # Create the temp location
    New-Item -Path $localFolder -ItemType Directory -Force

    # Download the sample file from Azure Blob storage
    $context = New-AzureStorageContext -StorageAccountName "hditutorialdata" -Anonymous
    $blobs = Get-AzureStorageBlob -Container "flightdelay" -Context $context
    #$blobs | Get-AzureStorageBlobContent -Context $context -Destination $localFolder

    # Upload data to default container

    $azcopycmd = "cmd.exe /C '$azcopyPath\azcopy.exe' /S /Source:'$localFolder' /Dest:'https://$defaultStorageAccountName.blob.core.windows.net/$defaultBlobContainerName/tutorials/flightdelays' /DestKey:$defaultStorageAccountKey"

    Invoke-Expression -Command:$azcopycmd

    ###########################################
    # Submit the Hive job
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
    # Submit the Sqoop job
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
    # Delete the cluster
    ###########################################
    Remove-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName
    ```
3. <span data-ttu-id="a04a8-171">Connectez-vous à votre base de données SQL et consultez les retards de vol moyens par ville dans la table AvgDelays :</span><span class="sxs-lookup"><span data-stu-id="a04a8-171">Connect to your SQL database and see average flight delays by city in the AvgDelays table:</span></span>

    ![HDI.FlightDelays.AvgDelays.Dataset][image-hdi-flightdelays-avgdelays-dataset]

- - -

## <span data-ttu-id="a04a8-173"><a id="appendix-a"></a>Annexe A - Téléchargement de données de retard de vol vers le stockage d’objets blob Azure</span><span class="sxs-lookup"><span data-stu-id="a04a8-173"><a id="appendix-a"></a>Appendix A - Upload flight delay data to Azure Blob storage</span></span>
<span data-ttu-id="a04a8-174">Le téléchargement du fichier de données et des fichiers de script HiveQL (voir l’ [annexe B](#appendix-b)) nécessite un minimum de planification.</span><span class="sxs-lookup"><span data-stu-id="a04a8-174">Uploading the data file and the HiveQL script files (see [Appendix B](#appendix-b)) requires some planning.</span></span> <span data-ttu-id="a04a8-175">Il s’agit de stocker les fichiers de données et le fichier HiveQL avant de créer un cluster HDInsight et d’exécuter la tâche Hive.</span><span class="sxs-lookup"><span data-stu-id="a04a8-175">The idea is to store the data files and the HiveQL file before creating an HDInsight cluster and running the Hive job.</span></span> <span data-ttu-id="a04a8-176">Deux options s'offrent à vous :</span><span class="sxs-lookup"><span data-stu-id="a04a8-176">You have two options:</span></span>

* <span data-ttu-id="a04a8-177">**Utiliser le même compte Azure Storage qui sera utilisé par le cluster HDInsight en tant que système de fichier par défaut.**</span><span class="sxs-lookup"><span data-stu-id="a04a8-177">**Use the same Azure Storage account that will be used by the HDInsight cluster as the default file system.**</span></span> <span data-ttu-id="a04a8-178">Étant donné que le cluster HDInsight disposera de la clé d’accès au compte de stockage, vous n’avez pas besoin d’effectuer des modifications supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="a04a8-178">Because the HDInsight cluster will have the Storage account access key, you don't need to make any additional changes.</span></span>
* <span data-ttu-id="a04a8-179">**Utiliser un compte Azure Storage différent du système de fichier par défaut du cluster HDInsight.**</span><span class="sxs-lookup"><span data-stu-id="a04a8-179">**Use a different Azure Storage account from the HDInsight cluster default file system.**</span></span> <span data-ttu-id="a04a8-180">Le cas échéant, vous devez modifier la partie de création du script Windows PowerShell figurant dans [Création d’un cluster HDInsight et exécution de tâches Hive/Sqoop](#runjob) de manière à lier le compte de stockage comme compte supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="a04a8-180">If this is the case, you must modify the creation part of the Windows PowerShell script found in [Create HDInsight cluster and run Hive/Sqoop jobs](#runjob) to link the Storage account as an additional Storage account.</span></span> <span data-ttu-id="a04a8-181">Pour plus d’informations, consultez la rubrique [Création de clusters Hadoop dans HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="a04a8-181">For instructions, see [Create Hadoop clusters in HDInsight][hdinsight-provision].</span></span> <span data-ttu-id="a04a8-182">Le cluster HDInsight connaît ainsi la clé d’accès du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="a04a8-182">The HDInsight cluster then knows the access key for the Storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="a04a8-183">Le chemin d’accès au stockage d’objets blob pour le fichier de données est codé en dur dans le fichier de script HiveQL.</span><span class="sxs-lookup"><span data-stu-id="a04a8-183">The Blob storage path for the data file is hard coded in the HiveQL script file.</span></span> <span data-ttu-id="a04a8-184">Vous devez le mettre à jour en conséquence.</span><span class="sxs-lookup"><span data-stu-id="a04a8-184">You must update it accordingly.</span></span>

<span data-ttu-id="a04a8-185">**Pour télécharger les données de vol**</span><span class="sxs-lookup"><span data-stu-id="a04a8-185">**To download the flight data**</span></span>

1. <span data-ttu-id="a04a8-186">Accédez à [Research and Innovative Technology Administration, Bureau of Transportation Statistics][rita-website].</span><span class="sxs-lookup"><span data-stu-id="a04a8-186">Browse to [Research and Innovative Technology Administration, Bureau of Transportation Statistics][rita-website].</span></span>
2. <span data-ttu-id="a04a8-187">Sur la page, sélectionnez les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="a04a8-187">On the page, select the following values:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="a04a8-188">Nom</span><span class="sxs-lookup"><span data-stu-id="a04a8-188">Name</span></span></th><th><span data-ttu-id="a04a8-189">Valeur</span><span class="sxs-lookup"><span data-stu-id="a04a8-189">Value</span></span></th></tr>
    <tr><td><span data-ttu-id="a04a8-190">Filtre année</span><span class="sxs-lookup"><span data-stu-id="a04a8-190">Filter Year</span></span></td><td><span data-ttu-id="a04a8-191">2013</span><span class="sxs-lookup"><span data-stu-id="a04a8-191">2013</span></span> </td></tr>
    <tr><td><span data-ttu-id="a04a8-192">Filtre période</span><span class="sxs-lookup"><span data-stu-id="a04a8-192">Filter Period</span></span></td><td><span data-ttu-id="a04a8-193">Janvier</span><span class="sxs-lookup"><span data-stu-id="a04a8-193">January</span></span></td></tr>
    <tr><td><span data-ttu-id="a04a8-194">Champs</span><span class="sxs-lookup"><span data-stu-id="a04a8-194">Fields</span></span></td><td><span data-ttu-id="a04a8-195">*Year*, *FlightDate*, *UniqueCarrier*, *Carrier*, *FlightNum*, *OriginAirportID*, *Origin*, *OriginCityName*, *OriginState*, *DestAirportID*, *Dest*, *DestCityName*, *DestState*, *DepDelayMinutes*, *ArrDelay*, *ArrDelayMinutes*, *CarrierDelay*, *WeatherDelay*, *NASDelay*, *SecurityDelay*, *LateAircraftDelay* (effacez tous les autres champs)</span><span class="sxs-lookup"><span data-stu-id="a04a8-195">*Year*, *FlightDate*, *UniqueCarrier*, *Carrier*, *FlightNum*, *OriginAirportID*, *Origin*, *OriginCityName*, *OriginState*, *DestAirportID*, *Dest*, *DestCityName*, *DestState*, *DepDelayMinutes*, *ArrDelay*, *ArrDelayMinutes*, *CarrierDelay*, *WeatherDelay*, *NASDelay*, *SecurityDelay*, *LateAircraftDelay* (clear all other fields)</span></span></td></tr>
    </table><span data-ttu-id="a04a8-196">
3. Cliquez sur **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="a04a8-196">
3. Click **Download**.</span></span>
<span data-ttu-id="a04a8-197">4.</span><span class="sxs-lookup"><span data-stu-id="a04a8-197">4.</span></span> <span data-ttu-id="a04a8-198">Décompressez le fichier dans le dossier **C:\Tutorials\FlightDelay\2013Data**.</span><span class="sxs-lookup"><span data-stu-id="a04a8-198">Unzip the file to the **C:\Tutorials\FlightDelay\2013Data** folder.</span></span> <span data-ttu-id="a04a8-199">Chaque fichier correspond à un fichier CSV d’environ 60 Go.</span><span class="sxs-lookup"><span data-stu-id="a04a8-199">Each file is a CSV file and is approximately 60GB in size.</span></span>
<span data-ttu-id="a04a8-200">5.</span><span class="sxs-lookup"><span data-stu-id="a04a8-200">5.</span></span> <span data-ttu-id="a04a8-201">Donnez au fichier le nom du mois dont il contient les données.</span><span class="sxs-lookup"><span data-stu-id="a04a8-201">Rename the file to the name of the month that it contains data for.</span></span> <span data-ttu-id="a04a8-202">Par exemple, renommez le fichier contenant les données du mois de janvier *Janvier.csv*.</span><span class="sxs-lookup"><span data-stu-id="a04a8-202">For example, the file containing the January data would be named *January.csv*.</span></span>
<span data-ttu-id="a04a8-203">6.</span><span class="sxs-lookup"><span data-stu-id="a04a8-203">6.</span></span> <span data-ttu-id="a04a8-204">Répétez les étapes 2 et 5 pour télécharger chaque fichier correspondant aux 12 mois de l’année 2013.</span><span class="sxs-lookup"><span data-stu-id="a04a8-204">Repeat steps 2 and 5 to download a file for each of the 12 months in 2013.</span></span> <span data-ttu-id="a04a8-205">Vous devez disposer d’au moins un fichier pour exécuter le didacticiel.</span><span class="sxs-lookup"><span data-stu-id="a04a8-205">You will need a minimum of one file to run the tutorial.</span></span>

<span data-ttu-id="a04a8-206">**Pour télécharger les données de retard de vol vers le stockage d’objets blob Azure**</span><span class="sxs-lookup"><span data-stu-id="a04a8-206">**To upload the flight delay data to Azure Blob storage**</span></span>

1. <span data-ttu-id="a04a8-207">Préparez les paramètres :</span><span class="sxs-lookup"><span data-stu-id="a04a8-207">Prepare the parameters:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="a04a8-208">Nom de la variable</span><span class="sxs-lookup"><span data-stu-id="a04a8-208">Variable Name</span></span></th><th><span data-ttu-id="a04a8-209">Remarques</span><span class="sxs-lookup"><span data-stu-id="a04a8-209">Notes</span></span></th></tr>
    <tr><td><span data-ttu-id="a04a8-210">$storageAccountName</span><span class="sxs-lookup"><span data-stu-id="a04a8-210">$storageAccountName</span></span></td><td><span data-ttu-id="a04a8-211">Compte Azure Storage sur lequel vous voulez télécharger les données.</span><span class="sxs-lookup"><span data-stu-id="a04a8-211">The Azure Storage account where you want to upload the data to.</span></span></td></tr>
    <tr><td><span data-ttu-id="a04a8-212">$blobContainerName</span><span class="sxs-lookup"><span data-stu-id="a04a8-212">$blobContainerName</span></span></td><td><span data-ttu-id="a04a8-213">Conteneur d'objets blob dans lequel vous voulez télécharger les données.</span><span class="sxs-lookup"><span data-stu-id="a04a8-213">The Blob container where you want to upload the data to.</span></span></td></tr>
    </table>
2. <span data-ttu-id="a04a8-214">Ouvrez Azure PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="a04a8-214">Open Azure PowerShell ISE.</span></span>
<span data-ttu-id="a04a8-215">3.</span><span class="sxs-lookup"><span data-stu-id="a04a8-215">3.</span></span> <span data-ttu-id="a04a8-216">Collez le script suivant dans le volet du script :</span><span class="sxs-lookup"><span data-stu-id="a04a8-216">Paste the following script into the script pane:</span></span>

    ```powershell
    [CmdletBinding()]
    Param(

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter the Azure storage account name for creating a new HDInsight cluster. If the account doesn't exist, the script will create one.")]
        [String]$storageAccountName,

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter the Azure blob container name for creating a new HDInsight cluster. If not specified, the HDInsight cluster name will be used.")]
        [String]$blobContainerName
    )

    #Region - Variables
    $localFolder = "C:\Tutorials\FlightDelay\2013Data"  # The source folder
    $destFolder = "tutorials/flightdelay/2013data"     #The blob name prefix for the files to be uploaded
    #EndRegion

    #Region - Connect to Azure subscription
    Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #Region - Validate user input
    Write-Host "`nValidating the Azure Storage account and the Blob container..." -ForegroundColor Green
    # Validate the Storage account
    if (-not (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}))
    {
        Write-Host "The storage account, $storageAccountName, doesn't exist." -ForegroundColor Red
        exit
    }
    else{
        $resourceGroupName = (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}).ResourceGroupName
    }

    # Validate the container
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    if (-not (Get-AzureStorageContainer -Context $storageContext |Where-Object{$_.Name -eq $blobContainerName}))
    {
        Write-Host "The Blob container, $blobContainerName, doesn't exist" -ForegroundColor Red
        Exit
    }
    #EngRegion

    #Region - Copy the file from local workstation to Azure Blob storage
    if (test-path -Path $localFolder)
    {
        foreach ($item in Get-ChildItem -Path $localFolder){
            $fileName = "$localFolder\$item"
            $blobName = "$destFolder/$item"

            Write-Host "Copying $fileName to $blobName" -ForegroundColor Green

            Set-AzureStorageBlobContent -File $fileName -Container $blobContainerName -Blob $blobName -Context $storageContext
        }
    }
    else
    {
        Write-Host "The source folder on the workstation doesn't exist" -ForegroundColor Red
    }

    # List the uploaded files on HDInsight
    Get-AzureStorageBlob -Container $blobContainerName  -Context $storageContext -Prefix $destFolder
    #EndRegion
    ```
4. <span data-ttu-id="a04a8-217">Appuyez sur **F5** pour exécuter le script.</span><span class="sxs-lookup"><span data-stu-id="a04a8-217">Press **F5** to run the script.</span></span>

<span data-ttu-id="a04a8-218">Si vous décidez d’utiliser une autre méthode pour télécharger les fichiers, vérifiez que le chemin d’accès au fichier est tutorials/flightdelay/data.</span><span class="sxs-lookup"><span data-stu-id="a04a8-218">If you choose to use a different method for uploading the files, please make sure the file path is tutorials/flightdelay/data.</span></span> <span data-ttu-id="a04a8-219">La syntaxe permettant d'accéder aux fichiers est la suivante :</span><span class="sxs-lookup"><span data-stu-id="a04a8-219">The syntax for accessing the files is:</span></span>

    wasb://<ContainerName>@<StorageAccountName>.blob.core.windows.net/tutorials/flightdelay/data

<span data-ttu-id="a04a8-220">Le chemin d’accès tutorials/flightdelay/data correspond au dossier virtuel que vous avez créé lors du chargement des fichiers.</span><span class="sxs-lookup"><span data-stu-id="a04a8-220">The path tutorials/flightdelay/data is the virtual folder you created when you uploaded the files.</span></span> <span data-ttu-id="a04a8-221">Assurez-vous qu'il existe 12 fichiers, un par mois.</span><span class="sxs-lookup"><span data-stu-id="a04a8-221">Verify that there are 12 files, one for each month.</span></span>

> [!NOTE]
> <span data-ttu-id="a04a8-222">Vous devez mettre à jour la requête Hive pour lire à partir du nouvel emplacement.</span><span class="sxs-lookup"><span data-stu-id="a04a8-222">You must update the Hive query to read from the new location.</span></span>
>
> <span data-ttu-id="a04a8-223">Vous devez configurer l’autorisation d’accès au conteneur pour qu’il soit public ou lier le compte de stockage au cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a04a8-223">You must either configure the container access permission to be public or bind the Storage account to the HDInsight cluster.</span></span> <span data-ttu-id="a04a8-224">Dans le cas contraire, la chaîne de requête Hive ne pourra pas accéder aux fichiers de données.</span><span class="sxs-lookup"><span data-stu-id="a04a8-224">Otherwise, the Hive query string will not be able to access the data files.</span></span>

- - -

## <span data-ttu-id="a04a8-225"><a id="appendix-b"></a>Annexe B - Création et téléchargement d’un script HiveQL</span><span class="sxs-lookup"><span data-stu-id="a04a8-225"><a id="appendix-b"></a>Appendix B - Create and upload a HiveQL script</span></span>
<span data-ttu-id="a04a8-226">À l'aide d'Azure PowerShell, vous pouvez exécuter plusieurs instructions HiveQL, une par une, ou empaqueter l'instruction HiveQL dans un fichier de script.</span><span class="sxs-lookup"><span data-stu-id="a04a8-226">Using Azure PowerShell, you can run multiple HiveQL statements one at a time, or package the HiveQL statement into a script file.</span></span> <span data-ttu-id="a04a8-227">Cette section explique comment créer un script HiveQL et télécharger celui-ci vers le stockage d’objets blob Azure en utilisant Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a04a8-227">This section shows you how to create a HiveQL script and upload the script to Azure Blob storage by using Azure PowerShell.</span></span> <span data-ttu-id="a04a8-228">Hive requiert le stockage de scripts HiveQL dans le stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="a04a8-228">Hive requires the HiveQL scripts to be stored in Azure Blob storage.</span></span>

<span data-ttu-id="a04a8-229">Le script HiveQL exécutera les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="a04a8-229">The HiveQL script will perform the following:</span></span>

1. <span data-ttu-id="a04a8-230">**Il supprime la table delays_raw**, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="a04a8-230">**Drop the delays_raw table**, in case the table already exists.</span></span>
2. <span data-ttu-id="a04a8-231">**Il crée la table externe Hive delays_raw** pointant vers l’emplacement du stockage d’objets blob où se trouvent les fichiers de retard de vol.</span><span class="sxs-lookup"><span data-stu-id="a04a8-231">**Create the delays_raw external Hive table** pointing to the Blob storage location with the flight delay files.</span></span> <span data-ttu-id="a04a8-232">Cette requête spécifie les champs délimités par « , » et les lignes se terminant par « \n ».</span><span class="sxs-lookup"><span data-stu-id="a04a8-232">This query specifies that fields are delimited by "," and that lines are terminated by "\n".</span></span> <span data-ttu-id="a04a8-233">Cela pose un problème lorsque les valeurs des champs contiennent des virgules, car Hive n'est pas en mesure de différencier une virgule utilisée en tant que délimiteur de champ d'une virgule faisant partie d'une valeur de champ (ce qui est le cas pour les valeurs des champs ORIGIN\_CITY\_NAME and DEST\_CITY\_NAME).</span><span class="sxs-lookup"><span data-stu-id="a04a8-233">This poses a problem when field values contain commas because Hive cannot differentiate between a comma that is a field delimiter and a one that is part of a field value (which is the case in field values for ORIGIN\_CITY\_NAME and DEST\_CITY\_NAME).</span></span> <span data-ttu-id="a04a8-234">Pour y remédier, la requête crée des colonnes TEMP afin de contenir les données incorrectement réparties dans les colonnes.</span><span class="sxs-lookup"><span data-stu-id="a04a8-234">To address this, the query creates TEMP columns to hold data that is incorrectly split into columns.</span></span>
3. <span data-ttu-id="a04a8-235">**Il supprime la table des retards**, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="a04a8-235">**Drop the delays table**, in case the table already exists.</span></span>
4. <span data-ttu-id="a04a8-236">**Il crée la table des retards**.</span><span class="sxs-lookup"><span data-stu-id="a04a8-236">**Create the delays table**.</span></span> <span data-ttu-id="a04a8-237">Il est conseillé de nettoyer les données avant tout traitement plus approfondi.</span><span class="sxs-lookup"><span data-stu-id="a04a8-237">It is helpful to clean up the data before further processing.</span></span> <span data-ttu-id="a04a8-238">Cette requête crée une nouvelle table, *delays*, à partir de la table delays_raw.</span><span class="sxs-lookup"><span data-stu-id="a04a8-238">This query creates a new table, *delays*, from the delays_raw table.</span></span> <span data-ttu-id="a04a8-239">Notez que les colonnes TEMP (comme indiqué précédemment) ne sont pas copiées et que la fonction **substring** est utilisée pour supprimer les guillemets présents dans les données.</span><span class="sxs-lookup"><span data-stu-id="a04a8-239">Note that the TEMP columns (as mentioned previously) are not copied, and that the **substring** function is used to remove quotation marks from the data.</span></span>
5. <span data-ttu-id="a04a8-240">**Il calcule les retards moyens liés aux conditions météo et regroupe les résultats par nom de ville.**</span><span class="sxs-lookup"><span data-stu-id="a04a8-240">**Compute the average weather delay and groups the results by city name.**</span></span> <span data-ttu-id="a04a8-241">Il transmet également les résultats au stockage d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="a04a8-241">It will also output the results to Blob storage.</span></span> <span data-ttu-id="a04a8-242">Notez que la requête supprime les apostrophes des données et exclut les lignes dans lesquelles la valeur de **weather_delay** est de type null.</span><span class="sxs-lookup"><span data-stu-id="a04a8-242">Note that the query will remove apostrophes from the data and will exclude rows where the value for **weather_delay** is null.</span></span> <span data-ttu-id="a04a8-243">Ces mesures sont nécessaires, car Sqoop, qui est utilisé ultérieurement dans ce didacticiel, ne gère pas correctement ces valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="a04a8-243">This is necessary because Sqoop, used later in this tutorial, doesn't handle those values gracefully by default.</span></span>

<span data-ttu-id="a04a8-244">Pour obtenir la liste complète des commandes HiveQL, consultez la rubrique [Langage de définition des données Hive][hadoop-hiveql].</span><span class="sxs-lookup"><span data-stu-id="a04a8-244">For a full list of the HiveQL commands, see [Hive Data Definition Language][hadoop-hiveql].</span></span> <span data-ttu-id="a04a8-245">Chaque commande HiveQL doit se terminer par un point virgule.</span><span class="sxs-lookup"><span data-stu-id="a04a8-245">Each HiveQL command must terminate with a semicolon.</span></span>

<span data-ttu-id="a04a8-246">**Pour créer un fichier de script HiveQL**</span><span class="sxs-lookup"><span data-stu-id="a04a8-246">**To create a HiveQL script file**</span></span>

1. <span data-ttu-id="a04a8-247">Préparez les paramètres :</span><span class="sxs-lookup"><span data-stu-id="a04a8-247">Prepare the parameters:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="a04a8-248">Nom de la variable</span><span class="sxs-lookup"><span data-stu-id="a04a8-248">Variable Name</span></span></th><th><span data-ttu-id="a04a8-249">Remarques</span><span class="sxs-lookup"><span data-stu-id="a04a8-249">Notes</span></span></th></tr>
    <tr><td><span data-ttu-id="a04a8-250">$storageAccountName</span><span class="sxs-lookup"><span data-stu-id="a04a8-250">$storageAccountName</span></span></td><td><span data-ttu-id="a04a8-251">Compte Azure Storage sur lequel vous voulez télécharger le script HiveQL.</span><span class="sxs-lookup"><span data-stu-id="a04a8-251">The Azure Storage account where you want to upload the HiveQL script to.</span></span></td></tr>
    <tr><td><span data-ttu-id="a04a8-252">$blobContainerName</span><span class="sxs-lookup"><span data-stu-id="a04a8-252">$blobContainerName</span></span></td><td><span data-ttu-id="a04a8-253">Conteneur d'objets blob dans lequel vous voulez télécharger le script HiveQL.</span><span class="sxs-lookup"><span data-stu-id="a04a8-253">The Blob container where you want to upload the HiveQL script to.</span></span></td></tr>
    </table>
2. <span data-ttu-id="a04a8-254">Ouvrez Azure PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="a04a8-254">Open Azure PowerShell ISE.</span></span>
<span data-ttu-id="a04a8-255">3.</span><span class="sxs-lookup"><span data-stu-id="a04a8-255">3.</span></span> <span data-ttu-id="a04a8-256">Copiez-collez le script suivant dans le volet du script :</span><span class="sxs-lookup"><span data-stu-id="a04a8-256">Copy and paste the following script into the script pane:</span></span>

    ```powershell
    [CmdletBinding()]
    Param(

        # Azure Blob storage variables
        [Parameter(Mandatory=$True,
                    HelpMessage="Enter the Azure storage account name for creating a new HDInsight cluster. If the account doesn't exist, the script will create one.")]
        [String]$storageAccountName,

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter the Azure blob container name for creating a new HDInsight cluster. If not specified, the HDInsight cluster name will be used.")]
        [String]$blobContainerName
    )

    #region - Define variables
    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    # The HiveQL script file is exported as this file before it's uploaded to Blob storage
    $hqlLocalFileName = "e:\tutorials\flightdelay\flightdelays.hql"

    # The HiveQL script file will be uploaded to Blob storage as this blob name
    $hqlBlobName = "tutorials/flightdelay/flightdelays.hql"

    # These two constants are used by the HiveQL script file
    #$srcDataFolder = "tutorials/flightdelay/data"
    $dstDataFolder = "/tutorials/flightdelay/output"
    #endregion

    #Region - Connect to Azure subscription
    Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #Region - Validate user input
    Write-Host "`nValidating the Azure Storage account and the Blob container..." -ForegroundColor Green
    # Validate the Storage account
    if (-not (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}))
    {
        Write-Host "The storage account, $storageAccountName, doesn't exist." -ForegroundColor Red
        exit
    }
    else{
        $resourceGroupName = (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}).ResourceGroupName
    }

    # Validate the container
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    if (-not (Get-AzureStorageContainer -Context $storageContext |Where-Object{$_.Name -eq $blobContainerName}))
    {
        Write-Host "The Blob container, $blobContainerName, doesn't exist" -ForegroundColor Red
        Exit
    }
    #EngRegion

    #region - Validate the file and file path

    # Check if a file with the same file name already exists on the workstation
    Write-Host "`nvalidating the folder structure on the workstation for saving the HQL script file ..."  -ForegroundColor Green
    if (test-path $hqlLocalFileName){

        $isDelete = Read-Host 'The file, ' $hqlLocalFileName ', exists.  Do you want to overwirte it? (Y/N)'

        if ($isDelete.ToLower() -ne "y")
        {
            Exit
        }
    }

    # Create the folder if it doesn't exist
    $folder = split-path $hqlLocalFileName
    if (-not (test-path $folder))
    {
        Write-Host "`nCreating folder, $folder ..." -ForegroundColor Green

        new-item $folder -ItemType directory
    }
    #end region

    #region - Write the Hive script into a local file
    Write-Host "`nWriting the Hive script into a file on your workstation ..." `
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

    #region - Upload the Hive script to the default Blob container
    Write-Host "`nUploading the Hive script to the default Blob container ..." -ForegroundColor Green

    # Create a storage context object
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Upload the file from local workstation to Blob storage
    Set-AzureStorageBlobContent -File $hqlLocalFileName -Container $blobContainerName -Blob $hqlBlobName -Context $destContext
    #endregion

    Write-host "`nEnd of the PowerShell script" -ForegroundColor Green
    ```

    <span data-ttu-id="a04a8-257">Voici les variables utilisées dans le script :</span><span class="sxs-lookup"><span data-stu-id="a04a8-257">Here are the variables used in the script:</span></span>

   * <span data-ttu-id="a04a8-258">**$hqlLocalFileName** - Le script enregistre le fichier script HiveQL en local avant de le télécharger dans le stockage d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="a04a8-258">**$hqlLocalFileName** - The script saves the HiveQL script file locally before uploading it to Blob storage.</span></span> <span data-ttu-id="a04a8-259">Il s'agit du nom de fichier.</span><span class="sxs-lookup"><span data-stu-id="a04a8-259">This is the file name.</span></span> <span data-ttu-id="a04a8-260">La valeur par défaut est <u>C:\tutorials\flightdelay\flightdelays.hql</u>.</span><span class="sxs-lookup"><span data-stu-id="a04a8-260">The default value is <u>C:\tutorials\flightdelay\flightdelays.hql</u>.</span></span>
   * <span data-ttu-id="a04a8-261">**$hqlBlobName** - Il s’agit du nom d’objet blob du fichier de script HiveQL utilisé dans le stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="a04a8-261">**$hqlBlobName** - This is the HiveQL script file blob name used in the Azure Blob storage.</span></span> <span data-ttu-id="a04a8-262">La valeur par défaut est tutorials/flightdelay/flightdelays.hql.</span><span class="sxs-lookup"><span data-stu-id="a04a8-262">The default value is tutorials/flightdelay/flightdelays.hql.</span></span> <span data-ttu-id="a04a8-263">Étant donné que le fichier sera écrit directement dans le stockage d'objets blob Azure, il n'y a PAS de « / » au début du nom d'objet blob.</span><span class="sxs-lookup"><span data-stu-id="a04a8-263">Because the file will be written directly to Azure Blob storage, there is NOT a "/" at the beginning of the blob name.</span></span> <span data-ttu-id="a04a8-264">Si vous voulez accéder au fichier à partir du stockage d’objets blob, il vous faudra ajouter « / » au début du nom de fichier.</span><span class="sxs-lookup"><span data-stu-id="a04a8-264">If you want to access the file from Blob storage, you will need to add a "/" at the beginning of the file name.</span></span>
   * <span data-ttu-id="a04a8-265">**$srcDataFolder** et **$dstDataFolder** - = "tutorials/flightdelay/data" = "tutorials/flightdelay/output"</span><span class="sxs-lookup"><span data-stu-id="a04a8-265">**$srcDataFolder** and **$dstDataFolder** - = "tutorials/flightdelay/data" = "tutorials/flightdelay/output"</span></span>

- - -
## <span data-ttu-id="a04a8-266"><a id="appendix-c"></a>Annexe C - Préparation d’une base de données SQL Azure pour le résultat de tâche Sqoop</span><span class="sxs-lookup"><span data-stu-id="a04a8-266"><a id="appendix-c"></a>Appendix C - Prepare an Azure SQL database for the Sqoop job output</span></span>
<span data-ttu-id="a04a8-267">**Pour préparer la base de données SQL (fusionnez celle-ci avec le script Sqoop)**</span><span class="sxs-lookup"><span data-stu-id="a04a8-267">**To prepare the SQL database (merge this with the Sqoop script)**</span></span>

1. <span data-ttu-id="a04a8-268">Préparez les paramètres :</span><span class="sxs-lookup"><span data-stu-id="a04a8-268">Prepare the parameters:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="a04a8-269">Nom de la variable</span><span class="sxs-lookup"><span data-stu-id="a04a8-269">Variable Name</span></span></th><th><span data-ttu-id="a04a8-270">Remarques</span><span class="sxs-lookup"><span data-stu-id="a04a8-270">Notes</span></span></th></tr>
    <tr><td><span data-ttu-id="a04a8-271">$sqlDatabaseServerName</span><span class="sxs-lookup"><span data-stu-id="a04a8-271">$sqlDatabaseServerName</span></span></td><td><span data-ttu-id="a04a8-272">Nom du serveur de la base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="a04a8-272">The name of the Azure SQL database server.</span></span> <span data-ttu-id="a04a8-273">N'entrez rien pour créer un nouveau serveur.</span><span class="sxs-lookup"><span data-stu-id="a04a8-273">Enter nothing to create a new server.</span></span></td></tr>
    <tr><td><span data-ttu-id="a04a8-274">$sqlDatabaseUsername</span><span class="sxs-lookup"><span data-stu-id="a04a8-274">$sqlDatabaseUsername</span></span></td><td><span data-ttu-id="a04a8-275">Nom de connexion pour le serveur de la base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="a04a8-275">The login name for the Azure SQL database server.</span></span> <span data-ttu-id="a04a8-276">Si $sqlDatabaseServerName est un serveur existant, la connexion et le mot de passe de connexion permettent de s'authentifier auprès du serveur.</span><span class="sxs-lookup"><span data-stu-id="a04a8-276">If $sqlDatabaseServerName is an existing server, the login and login password are used to authenticate with the server.</span></span> <span data-ttu-id="a04a8-277">Sinon, ils permettent de créer un nouveau serveur.</span><span class="sxs-lookup"><span data-stu-id="a04a8-277">Otherwise they are used to create a new server.</span></span></td></tr>
    <tr><td><span data-ttu-id="a04a8-278">$sqlDatabasePassword</span><span class="sxs-lookup"><span data-stu-id="a04a8-278">$sqlDatabasePassword</span></span></td><td><span data-ttu-id="a04a8-279">Mot de passe pour se connecter au serveur de la base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="a04a8-279">The login password for the Azure SQL database server.</span></span></td></tr>
    <tr><td><span data-ttu-id="a04a8-280">$sqlDatabaseLocation</span><span class="sxs-lookup"><span data-stu-id="a04a8-280">$sqlDatabaseLocation</span></span></td><td><span data-ttu-id="a04a8-281">Cette valeur est uniquement utilisée lors de la création d’un nouveau serveur de base de données Azure.</span><span class="sxs-lookup"><span data-stu-id="a04a8-281">This value is used only when you're creating a new Azure database server.</span></span></td></tr>
    <tr><td><span data-ttu-id="a04a8-282">$sqlDatabaseName</span><span class="sxs-lookup"><span data-stu-id="a04a8-282">$sqlDatabaseName</span></span></td><td><span data-ttu-id="a04a8-283">Base de données SQL utilisée pour créer la table AvgDelays pour la tâche Sqoop.</span><span class="sxs-lookup"><span data-stu-id="a04a8-283">The SQL database used to create the AvgDelays table for the Sqoop job.</span></span> <span data-ttu-id="a04a8-284">Si vous laissez cette valeur vide, une base de données intitulée HDISqoop est créée.</span><span class="sxs-lookup"><span data-stu-id="a04a8-284">Leaving it blank will create a database called HDISqoop.</span></span> <span data-ttu-id="a04a8-285">La table créée pour le résultat de la tâche Sqoop s’appelle AvgDelays.</span><span class="sxs-lookup"><span data-stu-id="a04a8-285">The table name for the Sqoop job output is AvgDelays.</span></span> </td></tr>
    </table>
2. <span data-ttu-id="a04a8-286">Ouvrez Azure PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="a04a8-286">Open Azure PowerShell ISE.</span></span>
<span data-ttu-id="a04a8-287">3.</span><span class="sxs-lookup"><span data-stu-id="a04a8-287">3.</span></span> <span data-ttu-id="a04a8-288">Copiez-collez le script suivant dans le volet du script :</span><span class="sxs-lookup"><span data-stu-id="a04a8-288">Copy and paste the following script into the script pane:</span></span>

    ```powershell
    [CmdletBinding()]
    Param(

        # Azure Resource group variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter the Azure resource group name. It will be created if it doesn't exist.")]
        [String]$resourceGroupName,

        # SQL database server variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter the Azure SQL Database Server Name. It will be created if it doesn't exist.")]
        [String]$sqlDatabaseServer,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter the Azure SQL Database admin user.")]
        [String]$sqlDatabaseLogin,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter the Azure SQL Database admin user password.")]
        [String]$sqlDatabasePassword,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter the region to create the Database in.")]
        [String]$sqlDatabaseLocation,   #For example, West US.

        # SQL database variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter the database name. It will be created if it doesn't exist.")]
        [String]$sqlDatabaseName # specify the database name if you have one created. Otherwise use "" to have the script create one for you.
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

    #Region - Connect to Azure subscription
    Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
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

        #To allow other Azure services to access the server add a firewall rule and set both the StartIpAddress and EndIpAddress to 0.0.0.0. Note that this allows Azure traffic from any Azure subscription to access the server.
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

    #region -  Execute an SQL command to create the AvgDelays table

    Write-Host "`nCreating SQL Database table ..."  -ForegroundColor Green
    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $conn.open()
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.connection = $conn
    $cmd.commandtext = $sqlCreateAvgDelaysTable
    $cmd.executenonquery()

    $conn.close()

    Write-host "`nEnd of the PowerShell script" -ForegroundColor Green
    ```

   > [!NOTE]
   > <span data-ttu-id="a04a8-289">Le script utilise un service REST (representational state transfer), http://bot.whatismyipaddress.com, pour extraire votre adresse IP externe.</span><span class="sxs-lookup"><span data-stu-id="a04a8-289">The script uses a representational state transfer (REST) service, http://bot.whatismyipaddress.com, to retrieve your external IP address.</span></span> <span data-ttu-id="a04a8-290">L’adresse IP permet de créer une règle de pare-feu pour votre serveur de base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="a04a8-290">The IP address is used for creating a firewall rule for your SQL database server.</span></span>

    <span data-ttu-id="a04a8-291">Voici quelques variables utilisées dans le script :</span><span class="sxs-lookup"><span data-stu-id="a04a8-291">Here are some variables used in the script:</span></span>

   * <span data-ttu-id="a04a8-292">**$ipAddressRestService** : la valeur par défaut est http://bot.whatismyipaddress.com.</span><span class="sxs-lookup"><span data-stu-id="a04a8-292">**$ipAddressRestService** - The default value is http://bot.whatismyipaddress.com.</span></span> <span data-ttu-id="a04a8-293">Il s’agit d’un service REST d’adresse IP publique permettant d’obtenir votre adresse IP externe.</span><span class="sxs-lookup"><span data-stu-id="a04a8-293">It is a public IP address REST service for getting your external IP address.</span></span> <span data-ttu-id="a04a8-294">Vous pouvez utiliser d'autres services si vous voulez.</span><span class="sxs-lookup"><span data-stu-id="a04a8-294">You can use other services if you want.</span></span> <span data-ttu-id="a04a8-295">L’adresse IP externe extraite au moyen du service servira à créer une règle de pare-feu pour votre serveur de base de données SQL Azure, ce qui vous permet d’accéder à la base de données à partir de votre poste de travail (au moyen d’un script Windows PowerShell).</span><span class="sxs-lookup"><span data-stu-id="a04a8-295">The external IP address retrieved through the service will be used to create a firewall rule for your Azure SQL database server, so that you can access the database from your workstation (by using a Windows PowerShell script).</span></span>
   * <span data-ttu-id="a04a8-296">**$fireWallRuleName** - Il s’agit du nom de la règle de pare-feu pour le serveur de la base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="a04a8-296">**$fireWallRuleName** - This is the name of the firewall rule for the Azure SQL database server.</span></span> <span data-ttu-id="a04a8-297">Le nom par défaut est <u>FlightDelay</u>.</span><span class="sxs-lookup"><span data-stu-id="a04a8-297">The default name is <u>FlightDelay</u>.</span></span> <span data-ttu-id="a04a8-298">Vous pouvez le renommer si vous voulez.</span><span class="sxs-lookup"><span data-stu-id="a04a8-298">You can rename it if you want.</span></span>
   * <span data-ttu-id="a04a8-299">**$sqlDatabaseMaxSizeGB** - Cette valeur est uniquement utilisée lors de la création d’un nouveau serveur de base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="a04a8-299">**$sqlDatabaseMaxSizeGB** - This value is used only when you're creating a new Azure SQL database server.</span></span> <span data-ttu-id="a04a8-300">La valeur par défaut est 10 Go.</span><span class="sxs-lookup"><span data-stu-id="a04a8-300">The default value is 10GB.</span></span> <span data-ttu-id="a04a8-301">Une capacité de 10 Go est suffisante pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="a04a8-301">10GB is sufficient for this tutorial.</span></span>
   * <span data-ttu-id="a04a8-302">**$sqlDatabaseName** - Cette valeur est uniquement utilisée lors de la création d’une nouvelle base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="a04a8-302">**$sqlDatabaseName** - This value is used only when you're creating a new Azure SQL database.</span></span> <span data-ttu-id="a04a8-303">La valeur par défaut est HDISqoop.</span><span class="sxs-lookup"><span data-stu-id="a04a8-303">The default value is HDISqoop.</span></span> <span data-ttu-id="a04a8-304">Si vous la renommez, vous devez mettre à jour le script Sqoop Windows PowerShell en conséquence.</span><span class="sxs-lookup"><span data-stu-id="a04a8-304">If you rename it, you must update the Sqoop Windows PowerShell script accordingly.</span></span>
4. <span data-ttu-id="a04a8-305">Appuyez sur **F5** pour exécuter le script.</span><span class="sxs-lookup"><span data-stu-id="a04a8-305">Press **F5** to run the script.</span></span>
5. <span data-ttu-id="a04a8-306">Validez la sortie du script.</span><span class="sxs-lookup"><span data-stu-id="a04a8-306">Validate the script output.</span></span> <span data-ttu-id="a04a8-307">Vérifiez que le script s'est correctement exécuté.</span><span class="sxs-lookup"><span data-stu-id="a04a8-307">Make sure the script ran successfully.</span></span>

## <span data-ttu-id="a04a8-308"><a id="nextsteps"></a> Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a04a8-308"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="a04a8-309">Vous savez à présent télécharger un fichier vers le stockage d’objets blob Azure, renseigner une table Hive à l’aide des données du stockage d’objets blob Azure, exécuter des requêtes Hive et utiliser Sqoop pour exporter des données entre HDFS et une base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="a04a8-309">Now you understand how to upload a file to Azure Blob storage, how to populate a Hive table by using the data from Azure Blob storage, how to run Hive queries, and how to use Sqoop to export data from HDFS to an Azure SQL database.</span></span> <span data-ttu-id="a04a8-310">Pour en savoir plus, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="a04a8-310">To learn more, see the following articles:</span></span>

* <span data-ttu-id="a04a8-311">[Prise en main de HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="a04a8-311">[Get started with HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="a04a8-312">[Utilisation de Hive avec HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="a04a8-312">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="a04a8-313">[Utilisation d’Oozie avec HDInsight][hdinsight-use-oozie]</span><span class="sxs-lookup"><span data-stu-id="a04a8-313">[Use Oozie with HDInsight][hdinsight-use-oozie]</span></span>
* <span data-ttu-id="a04a8-314">[Utilisation de Sqoop avec HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="a04a8-314">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="a04a8-315">[Utilisation de Pig avec HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="a04a8-315">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="a04a8-316">[Développement de programmes MapReduce en Java pour HDInsight][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="a04a8-316">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>

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
