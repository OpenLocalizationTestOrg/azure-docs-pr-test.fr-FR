---
title: "Didacticiel : Créer un pipeline pour déplacer les données à l’aide d’Azure PowerShell | Microsoft Docs"
description: "Dans ce didacticiel, vous créez un pipeline Azure Data Factory avec une activité de copie à l’aide d’Azure PowerShell."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 71087349-9365-4e95-9847-170658216ed8
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 81efe7c6af29af778686e1f6bcf62fedc9711052
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-create-a-data-factory-pipeline-that-moves-data-by-using-azure-powershell"></a><span data-ttu-id="df5ab-103">Didacticiel : Créer un pipeline Data Factory qui déplace les données à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="df5ab-103">Tutorial: Create a Data Factory pipeline that moves data by using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="df5ab-104">Vue d’ensemble et étapes préalables requises</span><span class="sxs-lookup"><span data-stu-id="df5ab-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="df5ab-105">Assistant de copie</span><span class="sxs-lookup"><span data-stu-id="df5ab-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="df5ab-106">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="df5ab-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="df5ab-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="df5ab-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="df5ab-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="df5ab-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="df5ab-109">Modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="df5ab-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="df5ab-110">API REST</span><span class="sxs-lookup"><span data-stu-id="df5ab-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="df5ab-111">API .NET</span><span class="sxs-lookup"><span data-stu-id="df5ab-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
>
>

<span data-ttu-id="df5ab-112">Dans cet article, vous allez apprendre à utiliser PowerShell pour créer une fabrique de données avec un pipeline qui copie les données d’un stockage Blob Azure dans une base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="df5ab-112">In this article, you learn how to use PowerShell to create a data factory with a pipeline that copies data from an Azure blob storage to an Azure SQL database.</span></span> <span data-ttu-id="df5ab-113">Si vous débutez avec Azure Data Factory, lisez l’article [Présentation d’Azure Data Factory](data-factory-introduction.md) avant de suivre ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="df5ab-113">If you are new to Azure Data Factory, read through the [Introduction to Azure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="df5ab-114">Dans ce didacticiel, vous créez un pipeline avec une activité : activité de copie.</span><span class="sxs-lookup"><span data-stu-id="df5ab-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="df5ab-115">L’activité de copie copie les données d’un magasin de données pris en charge vers un magasin de données de récepteur pris en charge.</span><span class="sxs-lookup"><span data-stu-id="df5ab-115">The copy activity copies data from a supported data store to a supported sink data store.</span></span> <span data-ttu-id="df5ab-116">Pour obtenir la liste des magasins de données pris en charge en tant que sources et récepteurs, consultez [Magasins de données pris en charge](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="df5ab-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="df5ab-117">Elle est mise en œuvre par un service disponible dans le monde entier, capable de copier des données entre différents magasins de données de façon sécurisée, fiable et évolutive.</span><span class="sxs-lookup"><span data-stu-id="df5ab-117">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="df5ab-118">Pour plus d’informations sur l’activité de copie, consultez [Activités de déplacement des données](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="df5ab-118">For more information about the Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="df5ab-119">Un pipeline peut contenir plusieurs activités.</span><span class="sxs-lookup"><span data-stu-id="df5ab-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="df5ab-120">En outre, vous pouvez chaîner deux activités (une après l’autre) en configurant le jeu de données de sortie d’une activité en tant que jeu de données d’entrée de l’autre activité.</span><span class="sxs-lookup"><span data-stu-id="df5ab-120">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="df5ab-121">Pour plus d’informations, consultez [Plusieurs activités dans un pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="df5ab-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

> [!NOTE]
> <span data-ttu-id="df5ab-122">cet article ne couvre pas toutes les applets de commande Data Factory.</span><span class="sxs-lookup"><span data-stu-id="df5ab-122">This article does not cover all the Data Factory cmdlets.</span></span> <span data-ttu-id="df5ab-123">Consultez la [Référence des applets de commande Data Factory](/powershell/module/azurerm.datafactories) pour obtenir une documentation complète sur ces applets de commande.</span><span class="sxs-lookup"><span data-stu-id="df5ab-123">See [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories) for comprehensive documentation on these cmdlets.</span></span>
> 
> <span data-ttu-id="df5ab-124">Dans ce didacticiel, le pipeline de données copie les données d’un magasin de données source vers un magasin de données de destination.</span><span class="sxs-lookup"><span data-stu-id="df5ab-124">The data pipeline in this tutorial copies data from a source data store to a destination data store.</span></span> <span data-ttu-id="df5ab-125">Pour un didacticiel sur la transformation des données à l’aide d’Azure Data Factory, consultez [Tutorial: Build your first pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md) (Didacticiel : Créer un pipeline pour transformer des données à l’aide d’un cluster Hadoop).</span><span class="sxs-lookup"><span data-stu-id="df5ab-125">For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="df5ab-126">Composants requis</span><span class="sxs-lookup"><span data-stu-id="df5ab-126">Prerequisites</span></span>
- <span data-ttu-id="df5ab-127">Assurez-vous que vous respectez la configuration requise décrite dans l’article [Configuration requise pour le didacticiel](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="df5ab-127">Complete prerequisites listed in the [tutorial prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article.</span></span>
- <span data-ttu-id="df5ab-128">Installez **Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="df5ab-128">Install **Azure PowerShell**.</span></span> <span data-ttu-id="df5ab-129">Suivez les instructions de la page [Installation et configuration d’Azure PowerShell](../powershell-install-configure.md).</span><span class="sxs-lookup"><span data-stu-id="df5ab-129">Follow the instructions in [How to install and configure Azure PowerShell](../powershell-install-configure.md).</span></span>

## <a name="steps"></a><span data-ttu-id="df5ab-130">Étapes</span><span class="sxs-lookup"><span data-stu-id="df5ab-130">Steps</span></span>
<span data-ttu-id="df5ab-131">Voici les étapes à effectuer dans le cadre de ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="df5ab-131">Here are the steps you perform as part of this tutorial:</span></span>

1. <span data-ttu-id="df5ab-132">Créer une **fabrique de données** Azure.</span><span class="sxs-lookup"><span data-stu-id="df5ab-132">Create an Azure **data factory**.</span></span> <span data-ttu-id="df5ab-133">Dans cette étape, vous créez une fabrique de données nommée ADFTutorialDataFactoryPSH.</span><span class="sxs-lookup"><span data-stu-id="df5ab-133">In this step, you create a data factory named ADFTutorialDataFactoryPSH.</span></span> 
2. <span data-ttu-id="df5ab-134">Créez des **services liés** dans la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="df5ab-134">Create **linked services** in the data factory.</span></span> <span data-ttu-id="df5ab-135">Au cours de cette étape, vous allez créer deux services liés de types : Stockage Azure et base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="df5ab-135">In this step, you create two linked services of types: Azure Storage and Azure SQL Database.</span></span> 
    
    <span data-ttu-id="df5ab-136">AzureStorageLinkedService relie votre compte de stockage Azure à la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="df5ab-136">The AzureStorageLinkedService links your Azure storage account to the data factory.</span></span> <span data-ttu-id="df5ab-137">Vous avez créé un conteneur et chargé des données dans ce compte de stockage en remplissant les [conditions préalables](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="df5ab-137">You created a container and uploaded data to this storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

    <span data-ttu-id="df5ab-138">AzureSqlLinkedService lie votre base de données SQL Azure à la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="df5ab-138">AzureSqlLinkedService links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="df5ab-139">Les données copiées à partir du stockage Blob sont stockées dans cette base de données.</span><span class="sxs-lookup"><span data-stu-id="df5ab-139">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="df5ab-140">Vous avez créé une table SQL dans cette base de données en remplissant les [conditions préalables](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="df5ab-140">You created a SQL table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   
3. <span data-ttu-id="df5ab-141">Créez des **jeux de données** d’entrée et de sortie dans la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="df5ab-141">Create input and output **datasets** in the data factory.</span></span>  
    
    <span data-ttu-id="df5ab-142">Le service lié Stockage Azure spécifie la chaîne de connexion que le service Data Factory utilise au moment de l’exécution pour se connecter à votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="df5ab-142">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="df5ab-143">Le jeu de données blob d’entrée spécifie quant à lui le conteneur et le dossier qui contient les données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="df5ab-143">And, the input blob dataset specifies the container and the folder that contains the input data.</span></span>  

    <span data-ttu-id="df5ab-144">De même, le service lié Azure SQL Database spécifie la chaîne de connexion que le service Data Factory utilise au moment de l’exécution pour se connecter à votre base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="df5ab-144">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="df5ab-145">Et le jeu de données de la table SQL de sortie spécifie la table de la base de données dans laquelle les données du stockage Blob sont copiées.</span><span class="sxs-lookup"><span data-stu-id="df5ab-145">And, the output SQL table dataset specifies the table in the database to which the data from the blob storage is copied.</span></span>
4. <span data-ttu-id="df5ab-146">Créez un **pipeline** dans la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="df5ab-146">Create a **pipeline** in the data factory.</span></span> <span data-ttu-id="df5ab-147">Dans cette étape, vous allez créer un pipeline avec une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="df5ab-147">In this step, you create a pipeline with a copy activity.</span></span>   
    
    <span data-ttu-id="df5ab-148">Cette activité copie les données d’un objet blob du stockage Blob Azure dans une table de la base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="df5ab-148">The copy activity copies data from a blob in the Azure blob storage to a table in the Azure SQL database.</span></span> <span data-ttu-id="df5ab-149">Vous pouvez utiliser une activité de copie dans un pipeline pour copier les données d’une source prise en charge dans une destination prise en charge.</span><span class="sxs-lookup"><span data-stu-id="df5ab-149">You can use a copy activity in a pipeline to copy data from any supported source to any supported destination.</span></span> <span data-ttu-id="df5ab-150">Pour obtenir la liste des magasins de données pris en charge, consultez [Activités de déplacement des données](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="df5ab-150">For a list of supported data stores, see [data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> 
5. <span data-ttu-id="df5ab-151">Surveiller le pipeline.</span><span class="sxs-lookup"><span data-stu-id="df5ab-151">Monitor the pipeline.</span></span> <span data-ttu-id="df5ab-152">Dans cette étape, vous allez **surveiller** les tranches de jeux de données d’entrée et de sortie à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="df5ab-152">In this step, you **monitor** the slices of input and output datasets by using PowerShell.</span></span>

## <a name="create-a-data-factory"></a><span data-ttu-id="df5ab-153">Créer une fabrique de données</span><span class="sxs-lookup"><span data-stu-id="df5ab-153">Create a data factory</span></span>
> [!IMPORTANT]
> <span data-ttu-id="df5ab-154">Assurez-vous de remplir les [conditions préalables à l’exécution du didacticiel](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) si ce n’est déjà fait.</span><span class="sxs-lookup"><span data-stu-id="df5ab-154">Complete [prerequisites for the tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) if you haven't already done so.</span></span>   

<span data-ttu-id="df5ab-155">Une fabrique de données peut avoir un ou plusieurs pipelines.</span><span class="sxs-lookup"><span data-stu-id="df5ab-155">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="df5ab-156">Un pipeline peut contenir une ou plusieurs activités.</span><span class="sxs-lookup"><span data-stu-id="df5ab-156">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="df5ab-157">Par exemple, une activité de copie pour copier des données d’une source vers un magasin de données de destination, et une activité Hive HDInsight pour exécuter un script Hive pour transformer des données d’entrée et produire des données de sortie.</span><span class="sxs-lookup"><span data-stu-id="df5ab-157">For example, a Copy Activity to copy data from a source to a destination data store and a HDInsight Hive activity to run a Hive script to transform input data to product output data.</span></span> <span data-ttu-id="df5ab-158">Commençons par la création de la fabrique de données dans cette étape.</span><span class="sxs-lookup"><span data-stu-id="df5ab-158">Let's start with creating the data factory in this step.</span></span>

1. <span data-ttu-id="df5ab-159">Lancez **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="df5ab-159">Launch **PowerShell**.</span></span> <span data-ttu-id="df5ab-160">Conservez Azure PowerShell ouvert jusqu’à la fin de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="df5ab-160">Keep Azure PowerShell open until the end of this tutorial.</span></span> <span data-ttu-id="df5ab-161">Si vous fermez puis rouvrez Azure PowerShell, vous devez réexécuter ces commandes.</span><span class="sxs-lookup"><span data-stu-id="df5ab-161">If you close and reopen, you need to run the commands again.</span></span>

    <span data-ttu-id="df5ab-162">Exécutez la commande suivante, puis saisissez le nom d’utilisateur et le mot de passe que vous avez utilisés pour la connexion au portail Azure :</span><span class="sxs-lookup"><span data-stu-id="df5ab-162">Run the following command, and enter the user name and password that you use to sign in to the Azure portal:</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```   
   
    <span data-ttu-id="df5ab-163">Exécutez la commande suivante pour afficher tous les abonnements de ce compte :</span><span class="sxs-lookup"><span data-stu-id="df5ab-163">Run the following command to view all the subscriptions for this account:</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```

    <span data-ttu-id="df5ab-164">Exécutez la commande suivante pour sélectionner l’abonnement que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="df5ab-164">Run the following command to select the subscription that you want to work with.</span></span> <span data-ttu-id="df5ab-165">Remplacez **&lt;NameOfAzureSubscription**&gt; par le nom de votre abonnement Azure :</span><span class="sxs-lookup"><span data-stu-id="df5ab-165">Replace **&lt;NameOfAzureSubscription**&gt; with the name of your Azure subscription:</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
2. <span data-ttu-id="df5ab-166">Créez un groupe de ressources Azure nommé **ADFTutorialResourceGroup** en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="df5ab-166">Create an Azure resource group named **ADFTutorialResourceGroup** by running the following command:</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
    
    <span data-ttu-id="df5ab-167">Certaines étapes de ce didacticiel supposent que vous utilisez le groupe de ressources nommé **ADFTutorialResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="df5ab-167">Some of the steps in this tutorial assume that you use the resource group named **ADFTutorialResourceGroup**.</span></span> <span data-ttu-id="df5ab-168">Si vous utilisez un autre groupe de ressources, vous devrez l’utiliser à la place d’ADFTutorialResourceGroup dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="df5ab-168">If you use a different resource group, you need to use it in place of ADFTutorialResourceGroup in this tutorial.</span></span>
3. <span data-ttu-id="df5ab-169">Exécutez l’applet de commande **New-AzureRmDataFactory** pour créer une fabrique de données nommée **ADFTutorialDataFactoryPSH** :</span><span class="sxs-lookup"><span data-stu-id="df5ab-169">Run the **New-AzureRmDataFactory** cmdlet to create a data factory named **ADFTutorialDataFactoryPSH**:</span></span>  

    ```PowerShell
    $df=New-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH –Location "West US"
    ```
    <span data-ttu-id="df5ab-170">Ce nom peut avoir déjà été utilisé.</span><span class="sxs-lookup"><span data-stu-id="df5ab-170">This name may already have been taken.</span></span> <span data-ttu-id="df5ab-171">Par conséquent, rendez le nom de la fabrique de données unique en ajoutant un préfixe ou un suffixe (par exemple : ADFTutorialDataFactoryPSH05152017) et réexécutez la commande.</span><span class="sxs-lookup"><span data-stu-id="df5ab-171">Therefore, make the name of the data factory unique by adding a prefix or suffix (for example: ADFTutorialDataFactoryPSH05152017) and run the command again.</span></span>  

<span data-ttu-id="df5ab-172">Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="df5ab-172">Note the following points:</span></span>

* <span data-ttu-id="df5ab-173">Le nom de la fabrique de données Azure doit être un nom global unique.</span><span class="sxs-lookup"><span data-stu-id="df5ab-173">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="df5ab-174">Si l’erreur suivante s’affiche, changez le nom (par exemple, votrenomADFTutorialDataFactoryPSH).</span><span class="sxs-lookup"><span data-stu-id="df5ab-174">If you receive the following error, change the name (for example, yournameADFTutorialDataFactoryPSH).</span></span> <span data-ttu-id="df5ab-175">Utilisez ce nom à la place d’ADFTutorialFactoryPSH quand vous effectuez les étapes de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="df5ab-175">Use this name in place of ADFTutorialFactoryPSH while performing steps in this tutorial.</span></span> <span data-ttu-id="df5ab-176">Consultez la rubrique [Data Factory – Règles d’affectation des noms](data-factory-naming-rules.md) pour les artefacts Data Factory.</span><span class="sxs-lookup"><span data-stu-id="df5ab-176">See [Data Factory - Naming Rules](data-factory-naming-rules.md) for Data Factory artifacts.</span></span>

    ```
    Data factory name “ADFTutorialDataFactoryPSH” is not available
    ```
* <span data-ttu-id="df5ab-177">Pour créer des instances de fabrique de données, vous devez avoir le statut d’administrateur/collaborateur de l’abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="df5ab-177">To create Data Factory instances, you must be a contributor or administrator of the Azure subscription.</span></span>
* <span data-ttu-id="df5ab-178">Le nom de la fabrique de données pourra être enregistré en tant que nom DNS et devenir ainsi visible publiquement.</span><span class="sxs-lookup"><span data-stu-id="df5ab-178">The name of the data factory may be registered as a DNS name in the future, and hence become publicly visible.</span></span>
* <span data-ttu-id="df5ab-179">Vous recevrez peut-être l’erreur suivante : « **This subscription is not registered to use namespace Microsoft.DataFactory** » (Cet abonnement n’est pas enregistré pour utiliser l’espace de noms Microsoft.DataFactory).</span><span class="sxs-lookup"><span data-stu-id="df5ab-179">You may receive the following error: "**This subscription is not registered to use namespace Microsoft.DataFactory.**"</span></span> <span data-ttu-id="df5ab-180">Effectuez l’une des opérations suivantes, puis essayez de publier à nouveau :</span><span class="sxs-lookup"><span data-stu-id="df5ab-180">Do one of the following, and try publishing again:</span></span>

  * <span data-ttu-id="df5ab-181">Dans Azure PowerShell, exécutez la commande suivante pour enregistrer le fournisseur Data Factory :</span><span class="sxs-lookup"><span data-stu-id="df5ab-181">In Azure PowerShell, run the following command to register the Data Factory provider:</span></span>

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

    <span data-ttu-id="df5ab-182">Exécutez la commande suivante pour confirmer l’enregistrement du fournisseur Data Factory :</span><span class="sxs-lookup"><span data-stu-id="df5ab-182">Run the following command to confirm that the Data Factory provider is registered:</span></span>

    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="df5ab-183">Connectez-vous au [portail Azure](https://portal.azure.com) à l’aide de votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="df5ab-183">Sign in by using the Azure subscription to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="df5ab-184">Accédez à un panneau Data Factory, ou créez une fabrique de données dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="df5ab-184">Go to a Data Factory blade, or create a data factory in the Azure portal.</span></span> <span data-ttu-id="df5ab-185">Cette action enregistre automatiquement le fournisseur.</span><span class="sxs-lookup"><span data-stu-id="df5ab-185">This action automatically registers the provider for you.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="df5ab-186">Créer des services liés</span><span class="sxs-lookup"><span data-stu-id="df5ab-186">Create linked services</span></span>
<span data-ttu-id="df5ab-187">Vous allez créer des services liés dans une fabrique de données pour lier vos magasins de données et vos services de calcul à la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="df5ab-187">You create linked services in a data factory to link your data stores and compute services to the data factory.</span></span> <span data-ttu-id="df5ab-188">Dans ce didacticiel, vous n’allez pas utiliser n’importe quel service de calcul comme Azure HDInsight ou Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="df5ab-188">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="df5ab-189">Vous utilisez deux magasins de données de type Stockage Azure (source) et Base de données SQL Azure (destination).</span><span class="sxs-lookup"><span data-stu-id="df5ab-189">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

<span data-ttu-id="df5ab-190">Vous créez ainsi deux services liés nommés AzureStorageLinkedService et AzureSqlLinkedService de types : AzureStorage et AzureSqlDatabase.</span><span class="sxs-lookup"><span data-stu-id="df5ab-190">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="df5ab-191">AzureStorageLinkedService relie votre compte de stockage Azure à la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="df5ab-191">The AzureStorageLinkedService links your Azure storage account to the data factory.</span></span> <span data-ttu-id="df5ab-192">Ce compte de stockage est celui dans lequel vous avez créé un conteneur et chargé les données en remplissant les [conditions préalables](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="df5ab-192">This storage account is the one in which you created a container and uploaded the data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="df5ab-193">AzureSqlLinkedService lie votre base de données SQL Azure à la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="df5ab-193">AzureSqlLinkedService links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="df5ab-194">Les données copiées à partir du stockage Blob sont stockées dans cette base de données.</span><span class="sxs-lookup"><span data-stu-id="df5ab-194">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="df5ab-195">Vous avez créé une table emp dans cette base de données en remplissant les [conditions préalables](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="df5ab-195">You created the emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

### <a name="create-a-linked-service-for-an-azure-storage-account"></a><span data-ttu-id="df5ab-196">Créer un service lié pour un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="df5ab-196">Create a linked service for an Azure storage account</span></span>
<span data-ttu-id="df5ab-197">Dans cette étape, vous allez lier votre compte Stockage Azure à votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="df5ab-197">In this step, you link your Azure storage account to your data factory.</span></span>

1. <span data-ttu-id="df5ab-198">Créez un fichier JSON nommé **AzureStorageLinkedService.json** dans le dossier **C:\ADFGetStartedPSH** avec le contenu suivant : (créez le dossier ADFGetStartedPSH s’il n’existe pas déjà).</span><span class="sxs-lookup"><span data-stu-id="df5ab-198">Create a JSON file named **AzureStorageLinkedService.json** in **C:\ADFGetStartedPSH** folder with the following content: (Create the folder ADFGetStartedPSH if it does not already exist.)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="df5ab-199">Remplacez &lt;accountname&gt; et &lt;accountkey&gt; par le nom et la clé de votre compte de stockage Azure avant d’enregistrer le fichier.</span><span class="sxs-lookup"><span data-stu-id="df5ab-199">Replace &lt;accountname&gt; and &lt;accountkey&gt; with name and key of your Azure storage account before saving the file.</span></span> 

    ```json
    {
        "name": "AzureStorageLinkedService",
        "properties": {
            "type": "AzureStorage",
            "typeProperties": {
                "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        }
     }
    ``` 
2. <span data-ttu-id="df5ab-200">Dans **Azure PowerShell**, basculez vers le dossier **ADFGetStartedPSH**.</span><span class="sxs-lookup"><span data-stu-id="df5ab-200">In **Azure PowerShell**, switch to the **ADFGetStartedPSH** folder.</span></span>
4. <span data-ttu-id="df5ab-201">Exécutez l’applet de commande **New-AzureRmDataFactoryLinkedService** pour créer le service lié : : **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="df5ab-201">Run the **New-AzureRmDataFactoryLinkedService** cmdlet to create the linked service: **AzureStorageLinkedService**.</span></span> <span data-ttu-id="df5ab-202">Cette applet de commande et d’autres applets de commande Data Factory que vous utilisez dans ce didacticiel vous obligent à transmettre des valeurs aux paramètres **ResourceGroupName** et **DataFactoryName**.</span><span class="sxs-lookup"><span data-stu-id="df5ab-202">This cmdlet, and other Data Factory cmdlets you use in this tutorial requires you to pass values for the **ResourceGroupName** and **DataFactoryName** parameters.</span></span> <span data-ttu-id="df5ab-203">Vous pouvez également transmettre l’objet DataFactory renvoyé par l’applet de commande AzureRmDataFactory sans avoir à saisir ResourceGroupName et DataFactoryName chaque fois que vous exécutez une applet de commande.</span><span class="sxs-lookup"><span data-stu-id="df5ab-203">Alternatively, you can pass the DataFactory object returned by the New-AzureRmDataFactory cmdlet without typing ResourceGroupName and DataFactoryName each time you run a cmdlet.</span></span> 

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureStorageLinkedService.json
    ```
    <span data-ttu-id="df5ab-204">Voici l'exemple de sortie :</span><span class="sxs-lookup"><span data-stu-id="df5ab-204">Here is the sample output:</span></span>

    ```
    LinkedServiceName : AzureStorageLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.LinkedServiceProperties
    ProvisioningState : Succeeded
    ``` 

    <span data-ttu-id="df5ab-205">Vous pouvez aussi créer ce service lié en spécifiant le nom du groupe de ressources et le nom de la fabrique de données au lieu de l’objet DataFactory.</span><span class="sxs-lookup"><span data-stu-id="df5ab-205">Other way of creating this linked service is to specify resource group name and data factory name instead of specifying the DataFactory object.</span></span>  

    ```PowerShell
    New-AzureRmDataFactoryLinkedService -ResourceGroupName ADFTutorialResourceGroup -DataFactoryName <Name of your data factory> -File .\AzureStorageLinkedService.json
    ```

### <a name="create-a-linked-service-for-an-azure-sql-database"></a><span data-ttu-id="df5ab-206">Créer un service lié pour une base de données Azure SQL</span><span class="sxs-lookup"><span data-stu-id="df5ab-206">Create a linked service for an Azure SQL database</span></span>
<span data-ttu-id="df5ab-207">Dans cette étape, vous liez votre base de données SQL Azure à votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="df5ab-207">In this step, you link your Azure SQL database to your data factory.</span></span>

1. <span data-ttu-id="df5ab-208">Créez un fichier JSON nommé AzureSqlLinkedService.json dans C:\ADFGetStartedPSH avec le contenu suivant :</span><span class="sxs-lookup"><span data-stu-id="df5ab-208">Create a JSON file named AzureSqlLinkedService.json in C:\ADFGetStartedPSH folder with the following content:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="df5ab-209">Remplacez &lt;servername&gt;, &lt;databasename&gt;, &lt;username@servername&gt;, et &lt;password&gt; par les noms de votre serveur SQL Azure, de la base de données, du compte d’utilisateur et par le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="df5ab-209">Replace &lt;servername&gt;, &lt;databasename&gt;, &lt;username@servername&gt;, and &lt;password&gt; with names of your Azure SQL server, database, user account, and password.</span></span>
    
    ```json
    {
        "name": "AzureSqlLinkedService",
        "properties": {
            "type": "AzureSqlDatabase",
            "typeProperties": {
                "connectionString": "Server=tcp:<server>.database.windows.net,1433;Database=<databasename>;User ID=<user>@<server>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        }
     }
    ```
2. <span data-ttu-id="df5ab-210">Exécutez la commande suivante pour créer un service lié :</span><span class="sxs-lookup"><span data-stu-id="df5ab-210">Run the following command to create a linked service:</span></span>

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureSqlLinkedService.json
    ```
    
    <span data-ttu-id="df5ab-211">Voici l'exemple de sortie :</span><span class="sxs-lookup"><span data-stu-id="df5ab-211">Here is the sample output:</span></span>

    ```
    LinkedServiceName : AzureSqlLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.LinkedServiceProperties
    ProvisioningState : Succeeded
    ```

   <span data-ttu-id="df5ab-212">Vérifiez que le paramètre **Autoriser l’accès aux services Azure** est activé pour votre serveur de base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="df5ab-212">Confirm that **Allow access to Azure services** setting is turned on for your SQL database server.</span></span> <span data-ttu-id="df5ab-213">Pour vérifier et l’activer, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="df5ab-213">To verify and turn it on, do the following steps:</span></span>

    1. <span data-ttu-id="df5ab-214">Connectez-vous au [portail Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="df5ab-214">Log in to the [Azure portal](https://portal.azure.com)</span></span>
    2. <span data-ttu-id="df5ab-215">Cliquez **Plus de services** à gauche, puis sur **Serveurs SQL** dans la catégorie **BASES DE DONNÉES**.</span><span class="sxs-lookup"><span data-stu-id="df5ab-215">Click **More services >** on the left, and click **SQL servers** in the **DATABASES** category.</span></span>
    3. <span data-ttu-id="df5ab-216">Sélectionnez votre serveur dans la liste des serveurs SQL.</span><span class="sxs-lookup"><span data-stu-id="df5ab-216">Select your server in the list of SQL servers.</span></span>
    4. <span data-ttu-id="df5ab-217">Dans le panneau du serveur SQL, cliquez sur le lien **Afficher les paramètres de pare-feu**.</span><span class="sxs-lookup"><span data-stu-id="df5ab-217">On the SQL server blade, click **Show firewall settings** link.</span></span>
    5. <span data-ttu-id="df5ab-218">Dans le panneau **Paramètres de pare-feu**, cliquez sur **ACTIVER** pour **Autoriser l’accès aux services Azure**.</span><span class="sxs-lookup"><span data-stu-id="df5ab-218">In the **Firewall settings** blade, click **ON** for **Allow access to Azure services**.</span></span>
    6. <span data-ttu-id="df5ab-219">Cliquez sur **Save** dans la barre d'outils.</span><span class="sxs-lookup"><span data-stu-id="df5ab-219">Click **Save** on the toolbar.</span></span> 

## <a name="create-datasets"></a><span data-ttu-id="df5ab-220">Créer des jeux de données</span><span class="sxs-lookup"><span data-stu-id="df5ab-220">Create datasets</span></span>
<span data-ttu-id="df5ab-221">Dans l’étape précédente, vous avez créé des services liés pour lier votre compte de stockage Azure et une base de données SQL Azure à votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="df5ab-221">In the previous step, you created linked services to link your Azure Storage account and Azure SQL database to your data factory.</span></span> <span data-ttu-id="df5ab-222">Dans cette étape, vous définissez deux jeux de données nommés InputDataset et OutputDataset, qui représentent les données d’entrée/sortie stockées dans les banques de données référencées par AzureStorageLinkedService et AzureSqlLinkedService, respectivement.</span><span class="sxs-lookup"><span data-stu-id="df5ab-222">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in the data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

<span data-ttu-id="df5ab-223">Le service lié Stockage Azure spécifie la chaîne de connexion que le service Data Factory utilise au moment de l’exécution pour se connecter à votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="df5ab-223">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="df5ab-224">Le jeu de données blob d’entrée (InputDataset) spécifie quant à lui le conteneur et le dossier qui contient les données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="df5ab-224">And, the input blob dataset (InputDataset) specifies the container and the folder that contains the input data.</span></span>  

<span data-ttu-id="df5ab-225">De même, le service lié Azure SQL Database spécifie la chaîne de connexion que le service Data Factory utilise au moment de l’exécution pour se connecter à votre base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="df5ab-225">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="df5ab-226">Et le jeu de données de la table SQL de sortie (OututDataset) spécifie la table de la base de données dans laquelle les données du stockage Blob sont copiées.</span><span class="sxs-lookup"><span data-stu-id="df5ab-226">And, the output SQL table dataset (OututDataset) specifies the table in the database to which the data from the blob storage is copied.</span></span> 

### <a name="create-an-input-dataset"></a><span data-ttu-id="df5ab-227">Créer un jeu de données d’entrée</span><span class="sxs-lookup"><span data-stu-id="df5ab-227">Create an input dataset</span></span>
<span data-ttu-id="df5ab-228">Dans cette étape, vous créez un jeu de données nommé InputDataset qui pointe vers un fichier blob (emp.txt) dans le dossier racine d’un conteneur d’objets blob (adftutorial) du stockage Azure représenté par le service lié AzureStorageLinkedService.</span><span class="sxs-lookup"><span data-stu-id="df5ab-228">In this step, you create a dataset named InputDataset that points to a blob file (emp.txt) in the root folder of a blob container (adftutorial) in the Azure Storage represented by the AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="df5ab-229">Si vous ne spécifiez pas de valeur pour fileName (ou si vous ignorez ce paramètre), les données de tous les objets blob du dossier d’entrée sont copiées dans la destination.</span><span class="sxs-lookup"><span data-stu-id="df5ab-229">If you don't specify a value for the fileName (or skip it), data from all blobs in the input folder are copied to the destination.</span></span> <span data-ttu-id="df5ab-230">Dans ce didacticiel, vous spécifiez une valeur pour fileName.</span><span class="sxs-lookup"><span data-stu-id="df5ab-230">In this tutorial, you specify a value for the fileName.</span></span>  

1. <span data-ttu-id="df5ab-231">Créez un fichier JSON nommé **InputDataset.json** dans le dossier **C:\ADFGetStartedPSH** avec le contenu suivant :</span><span class="sxs-lookup"><span data-stu-id="df5ab-231">Create a JSON file named **InputDataset.json** in the **C:\ADFGetStartedPSH** folder, with the following content:</span></span>

    ```json
    {
        "name": "InputDataset",
        "properties": {
            "structure": [
                {
                    "name": "FirstName",
                    "type": "String"
                },
                {
                    "name": "LastName",
                    "type": "String"
                }
            ],
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "emp.txt",
                "folderPath": "adftutorial/",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "external": true,
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
     }
    ```

    <span data-ttu-id="df5ab-232">Le tableau suivant décrit les propriétés JSON utilisées dans l'extrait de code :</span><span class="sxs-lookup"><span data-stu-id="df5ab-232">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

    | <span data-ttu-id="df5ab-233">Propriété</span><span class="sxs-lookup"><span data-stu-id="df5ab-233">Property</span></span> | <span data-ttu-id="df5ab-234">Description</span><span class="sxs-lookup"><span data-stu-id="df5ab-234">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="df5ab-235">type</span><span class="sxs-lookup"><span data-stu-id="df5ab-235">type</span></span> | <span data-ttu-id="df5ab-236">La propriété du type est définie sur **AzureBlob**, car les données se trouvent dans le stockage blob Azure.</span><span class="sxs-lookup"><span data-stu-id="df5ab-236">The type property is set to **AzureBlob** because data resides in an Azure blob storage.</span></span> |
    | <span data-ttu-id="df5ab-237">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="df5ab-237">linkedServiceName</span></span> | <span data-ttu-id="df5ab-238">Fait référence au service **AzureStorageLinkedService** que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="df5ab-238">Refers to the **AzureStorageLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="df5ab-239">folderPath</span><span class="sxs-lookup"><span data-stu-id="df5ab-239">folderPath</span></span> | <span data-ttu-id="df5ab-240">Spécifie le **conteneur** d’objets blob et le **dossier** qui contient les objets blob d’entrée.</span><span class="sxs-lookup"><span data-stu-id="df5ab-240">Specifies the blob **container** and the **folder** that contains input blobs.</span></span> <span data-ttu-id="df5ab-241">Dans ce didacticiel, adftutorial est le conteneur d’objets blob et folder est le dossier racine.</span><span class="sxs-lookup"><span data-stu-id="df5ab-241">In this tutorial, adftutorial is the blob container and folder is the root folder.</span></span> | 
    | <span data-ttu-id="df5ab-242">fileName</span><span class="sxs-lookup"><span data-stu-id="df5ab-242">fileName</span></span> | <span data-ttu-id="df5ab-243">Cette propriété est facultative.</span><span class="sxs-lookup"><span data-stu-id="df5ab-243">This property is optional.</span></span> <span data-ttu-id="df5ab-244">Si vous omettez cette propriété, tous les fichiers spécifiés dans le paramètre folderPath sont récupérés.</span><span class="sxs-lookup"><span data-stu-id="df5ab-244">If you omit this property, all files from the folderPath are picked.</span></span> <span data-ttu-id="df5ab-245">Dans ce didacticiel, **emp.txt** est spécifié pour le paramètre fileName, si bien que seul ce fichier est récupéré pour le traitement.</span><span class="sxs-lookup"><span data-stu-id="df5ab-245">In this tutorial, **emp.txt** is specified for the fileName, so only that file is picked up for processing.</span></span> |
    | <span data-ttu-id="df5ab-246">format -> type</span><span class="sxs-lookup"><span data-stu-id="df5ab-246">format -> type</span></span> |<span data-ttu-id="df5ab-247">Le fichier d’entrée étant au format texte, nous utilisons **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="df5ab-247">The input file is in the text format, so we use **TextFormat**.</span></span> |
    | <span data-ttu-id="df5ab-248">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="df5ab-248">columnDelimiter</span></span> | <span data-ttu-id="df5ab-249">Les colonnes du fichier d’entrée sont délimitées par une **virgule (`,`)**.</span><span class="sxs-lookup"><span data-stu-id="df5ab-249">The columns in the input file are delimited by **comma character (`,`)**.</span></span> |
    | <span data-ttu-id="df5ab-250">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="df5ab-250">frequency/interval</span></span> | <span data-ttu-id="df5ab-251">La fréquence est définie sur **Heure** et l’intervalle est **1**, ce qui signifie que les segments d’entrée sont disponibles **toutes les heures**.</span><span class="sxs-lookup"><span data-stu-id="df5ab-251">The frequency is set to **Hour** and interval is  set to **1**, which means that the input slices are available **hourly**.</span></span> <span data-ttu-id="df5ab-252">En d’autres termes, le service Data Factory recherche les données d’entrée toutes les heures dans le dossier racine du conteneur d’objets blob (**adftutorial**) que vous avez spécifié.</span><span class="sxs-lookup"><span data-stu-id="df5ab-252">In other words, the Data Factory service looks for input data every hour in the root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="df5ab-253">Il recherche des données entre les heures de début et de fin du pipeline, pas avant ni après.</span><span class="sxs-lookup"><span data-stu-id="df5ab-253">It looks for the data within the pipeline start and end times, not before or after these times.</span></span>  |
    | <span data-ttu-id="df5ab-254">external</span><span class="sxs-lookup"><span data-stu-id="df5ab-254">external</span></span> | <span data-ttu-id="df5ab-255">Cette propriété a la valeur **true** si les données ne sont pas générées par ce pipeline.</span><span class="sxs-lookup"><span data-stu-id="df5ab-255">This property is set to **true** if the data is not generated by this pipeline.</span></span> <span data-ttu-id="df5ab-256">Dans ce didacticiel, les données d’entrée sont dans le fichier emp.txt, qui n’est pas généré par ce pipeline. Nous définissons donc cette propriété sur true.</span><span class="sxs-lookup"><span data-stu-id="df5ab-256">The input data in this tutorial is in the emp.txt file, which is not generated by this pipeline, so we set this property to true.</span></span> |

    <span data-ttu-id="df5ab-257">Pour plus d’informations sur ces propriétés JSON, consultez l’article [Connecteur de stockage Blob Azure](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="df5ab-257">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
2. <span data-ttu-id="df5ab-258">Exécutez la commande suivante pour créer le jeu de données Data Factory :</span><span class="sxs-lookup"><span data-stu-id="df5ab-258">Run the following command to create the Data Factory dataset.</span></span>

    ```PowerShell  
    New-AzureRmDataFactoryDataset $df -File .\InputDataset.json
    ```
    <span data-ttu-id="df5ab-259">Voici l'exemple de sortie :</span><span class="sxs-lookup"><span data-stu-id="df5ab-259">Here is the sample output:</span></span>

    ```
    DatasetName       : InputDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Availability      : Microsoft.Azure.Management.DataFactories.Common.Models.Availability
    Location          : Microsoft.Azure.Management.DataFactories.Models.AzureBlobDataset
    Policy            : Microsoft.Azure.Management.DataFactories.Common.Models.Policy
    Structure         : {FirstName, LastName}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DatasetProperties
    ProvisioningState : Succeeded
    ```

### <a name="create-an-output-dataset"></a><span data-ttu-id="df5ab-260">Créer un jeu de données de sortie</span><span class="sxs-lookup"><span data-stu-id="df5ab-260">Create an output dataset</span></span>
<span data-ttu-id="df5ab-261">Dans cette partie de l’étape, vous créez un jeu de données de sortie nommé **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="df5ab-261">In this part of the step, you create an output dataset named **OutputDataset**.</span></span> <span data-ttu-id="df5ab-262">Ce jeu de données pointe vers une table SQL de la base de données SQL Azure représentée par **AzureSqlLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="df5ab-262">This dataset points to a SQL table in the Azure SQL database represented by **AzureSqlLinkedService**.</span></span> 

1. <span data-ttu-id="df5ab-263">Créez un fichier JSON nommé **OutputDataset.json** dans le dossier **C:\ADFGetStartedPSH** avec le contenu suivant :</span><span class="sxs-lookup"><span data-stu-id="df5ab-263">Create a JSON file named **OutputDataset.json** in the **C:\ADFGetStartedPSH** folder with the following content:</span></span>

    ```json
    {
        "name": "OutputDataset",
        "properties": {
            "structure": [
                {
                    "name": "FirstName",
                    "type": "String"
                },
                {
                    "name": "LastName",
                    "type": "String"
                }
            ],
            "type": "AzureSqlTable",
            "linkedServiceName": "AzureSqlLinkedService",
            "typeProperties": {
                "tableName": "emp"
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
    ```

    <span data-ttu-id="df5ab-264">Le tableau suivant décrit les propriétés JSON utilisées dans l'extrait de code :</span><span class="sxs-lookup"><span data-stu-id="df5ab-264">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

    | <span data-ttu-id="df5ab-265">Propriété</span><span class="sxs-lookup"><span data-stu-id="df5ab-265">Property</span></span> | <span data-ttu-id="df5ab-266">Description</span><span class="sxs-lookup"><span data-stu-id="df5ab-266">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="df5ab-267">type</span><span class="sxs-lookup"><span data-stu-id="df5ab-267">type</span></span> | <span data-ttu-id="df5ab-268">La propriété du type est définie sur **AzureSqlTable** car les données sont copiées dans une table de la base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="df5ab-268">The type property is set to **AzureSqlTable** because data is copied to a table in an Azure SQL database.</span></span> |
    | <span data-ttu-id="df5ab-269">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="df5ab-269">linkedServiceName</span></span> | <span data-ttu-id="df5ab-270">Fait référence au service **AzureSqlLinkedService** que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="df5ab-270">Refers to the **AzureSqlLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="df5ab-271">TableName</span><span class="sxs-lookup"><span data-stu-id="df5ab-271">tableName</span></span> | <span data-ttu-id="df5ab-272">Spécifie la **table** dans laquelle les données sont copiées.</span><span class="sxs-lookup"><span data-stu-id="df5ab-272">Specified the **table** to which the data is copied.</span></span> | 
    | <span data-ttu-id="df5ab-273">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="df5ab-273">frequency/interval</span></span> | <span data-ttu-id="df5ab-274">La fréquence est définie sur **Heure** et l’intervalle sur **1**, ce qui signifie que les tranches de sortie sont produites **toutes les heures** entre les heures de début et de fin du pipeline, pas avant ni après.</span><span class="sxs-lookup"><span data-stu-id="df5ab-274">The frequency is set to **Hour** and interval is **1**, which means that the output slices are produced **hourly** between the pipeline start and end times, not before or after these times.</span></span>  |

    <span data-ttu-id="df5ab-275">La table emp de la base de données contient trois colonnes : **ID**, **FirstName** et **LastName**.</span><span class="sxs-lookup"><span data-stu-id="df5ab-275">There are three columns – **ID**, **FirstName**, and **LastName** – in the emp table in the database.</span></span> <span data-ttu-id="df5ab-276">ID étant une colonne d’identité, il vous suffit de spécifier **FirstName** et **LastName**.</span><span class="sxs-lookup"><span data-stu-id="df5ab-276">ID is an identity column, so you need to specify only **FirstName** and **LastName** here.</span></span>

    <span data-ttu-id="df5ab-277">Pour plus d’informations sur ces propriétés JSON, consultez l’article [Connecteur SQL Azure](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="df5ab-277">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
2. <span data-ttu-id="df5ab-278">Exécutez la commande suivante pour créer le jeu de données de fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="df5ab-278">Run the following command to create the data factory dataset.</span></span>

    ```PowerShell   
    New-AzureRmDataFactoryDataset $df -File .\OutputDataset.json
    ```

    <span data-ttu-id="df5ab-279">Voici l'exemple de sortie :</span><span class="sxs-lookup"><span data-stu-id="df5ab-279">Here is the sample output:</span></span>

    ```
    DatasetName       : OutputDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Availability      : Microsoft.Azure.Management.DataFactories.Common.Models.Availability
    Location          : Microsoft.Azure.Management.DataFactories.Models.AzureSqlTableDataset
    Policy            :
    Structure         : {FirstName, LastName}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DatasetProperties
    ProvisioningState : Succeeded
    ```

## <a name="create-a-pipeline"></a><span data-ttu-id="df5ab-280">Créer un pipeline</span><span class="sxs-lookup"><span data-stu-id="df5ab-280">Create a pipeline</span></span>
<span data-ttu-id="df5ab-281">Dans cette étape, vous créez un pipeline avec une **activité de copie** qui utilise **InputDataset** en entrée et **OutputDataset** en sortie.</span><span class="sxs-lookup"><span data-stu-id="df5ab-281">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

<span data-ttu-id="df5ab-282">Le jeu de données de sortie pilote actuellement la planification.</span><span class="sxs-lookup"><span data-stu-id="df5ab-282">Currently, output dataset is what drives the schedule.</span></span> <span data-ttu-id="df5ab-283">Dans ce didacticiel, le jeu de données de sortie est configuré pour produire une tranche par heure.</span><span class="sxs-lookup"><span data-stu-id="df5ab-283">In this tutorial, output dataset is configured to produce a slice once an hour.</span></span> <span data-ttu-id="df5ab-284">Les heures de début et de fin du pipeline sont distantes d’une journée, soit 24 heures.</span><span class="sxs-lookup"><span data-stu-id="df5ab-284">The pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="df5ab-285">Par conséquent, 24 tranches de jeu de données de sortie sont générées par le pipeline.</span><span class="sxs-lookup"><span data-stu-id="df5ab-285">Therefore, 24 slices of output dataset are produced by the pipeline.</span></span> 


1. <span data-ttu-id="df5ab-286">Créez un fichier JSON nommé **ADFTutorialPipeline.json** dans le dossier **C:\ADFGetStartedPSH** avec le contenu suivant :</span><span class="sxs-lookup"><span data-stu-id="df5ab-286">Create a JSON file named **ADFTutorialPipeline.json** in the **C:\ADFGetStartedPSH** folder, with the following content:</span></span>

    ```json   
    {
      "name": "ADFTutorialPipeline",
      "properties": {
        "description": "Copy data from a blob to Azure SQL table",
        "activities": [
          {
            "name": "CopyFromBlobToSQL",
            "type": "Copy",
            "inputs": [
              {
                "name": "InputDataset"
              }
            ],
            "outputs": [
              {
                "name": "OutputDataset"
              }
            ],
            "typeProperties": {
              "source": {
                "type": "BlobSource"
              },
              "sink": {
                "type": "SqlSink",
                "writeBatchSize": 10000,
                "writeBatchTimeout": "60:00:00"
              }
            },
            "Policy": {
              "concurrency": 1,
              "executionPriorityOrder": "NewestFirst",
              "retry": 0,
              "timeout": "01:00:00"
            }
          }
        ],
        "start": "2017-05-11T00:00:00Z",
        "end": "2017-05-12T00:00:00Z"
      }
    } 
    ```
    <span data-ttu-id="df5ab-287">Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="df5ab-287">Note the following points:</span></span>
   
    - <span data-ttu-id="df5ab-288">Dans la section des activités, il existe une seule activité dont le **type** a la valeur **Copy**.</span><span class="sxs-lookup"><span data-stu-id="df5ab-288">In the activities section, there is only one activity whose **type** is set to **Copy**.</span></span> <span data-ttu-id="df5ab-289">Pour plus d’informations sur l’activité de copie, consultez [Activités de déplacement des données](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="df5ab-289">For more information about the copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="df5ab-290">Dans les solutions Data Factory, vous pouvez également utiliser [Activités de transformation des données](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="df5ab-290">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="df5ab-291">L’entrée de l’activité est définie sur **InputDataset** et sa sortie, sur **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="df5ab-291">Input for the activity is set to **InputDataset** and output for the activity is set to **OutputDataset**.</span></span> 
    - <span data-ttu-id="df5ab-292">Dans la section **typeProperties**, **BlobSource** est spécifié en tant que type de source et **SqlSink**, en tant que type de récepteur.</span><span class="sxs-lookup"><span data-stu-id="df5ab-292">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span></span> <span data-ttu-id="df5ab-293">Pour obtenir la liste des magasins de données pris en charge en tant que sources et récepteurs pour l’activité de copie, consultez [Magasins de données pris en charge](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="df5ab-293">For a complete list of data stores supported by the copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="df5ab-294">Pour apprendre à utiliser un magasin de données pris en charge spécifique en tant que source/récepteur, cliquez sur le lien dans le tableau.</span><span class="sxs-lookup"><span data-stu-id="df5ab-294">To learn how to use a specific supported data store as a source/sink, click the link in the table.</span></span>  
     
    <span data-ttu-id="df5ab-295">Remplacez la valeur de la propriété **start** par le jour actuel et la valeur **end** par le jour suivant.</span><span class="sxs-lookup"><span data-stu-id="df5ab-295">Replace the value of the **start** property with the current day and **end** value with the next day.</span></span> <span data-ttu-id="df5ab-296">Si vous le souhaitez, spécifiez uniquement la date et ignorez l'heure.</span><span class="sxs-lookup"><span data-stu-id="df5ab-296">You can specify only the date part and skip the time part of the date time.</span></span> <span data-ttu-id="df5ab-297">Par exemple, « 2016-02-03 », qui équivaut à « 2016-02-03T00:00:00Z ».</span><span class="sxs-lookup"><span data-stu-id="df5ab-297">For example, "2016-02-03", which is equivalent to "2016-02-03T00:00:00Z"</span></span>
     
    <span data-ttu-id="df5ab-298">Les dates/heures de début et de fin doivent toutes deux être au [format ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="df5ab-298">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="df5ab-299">Par exemple : 2016-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="df5ab-299">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="df5ab-300">L’heure de fin ( **end** ) est facultative, mais nous allons l’utiliser dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="df5ab-300">The **end** time is optional, but we use it in this tutorial.</span></span> 
     
    <span data-ttu-id="df5ab-301">Si vous ne spécifiez aucune valeur pour la propriété **end**, cette dernière est calculée comme suit : « **start + 48 heures** ».</span><span class="sxs-lookup"><span data-stu-id="df5ab-301">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="df5ab-302">Pour exécuter le pipeline indéfiniment, spécifiez **9999-09-09** comme valeur pour la propriété **end**.</span><span class="sxs-lookup"><span data-stu-id="df5ab-302">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span></span>
     
    <span data-ttu-id="df5ab-303">Dans l’exemple ci-dessus, il existe 24 tranches de données, car une tranche de données est générée toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="df5ab-303">In the preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

    <span data-ttu-id="df5ab-304">Pour obtenir une description des propriétés JSON dans une définition de pipeline, consultez l’article [Créer des pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="df5ab-304">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="df5ab-305">Pour obtenir une description des propriétés JSON dans une définition d’activité de copie, consultez [Activités de déplacement des données](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="df5ab-305">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="df5ab-306">Pour obtenir une description des propriétés JSON prises en charge par BlobSource, consultez l’article [Connecteur de stockage Blob Azure](data-factory-azure-blob-connector.md).</span><span class="sxs-lookup"><span data-stu-id="df5ab-306">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="df5ab-307">Pour obtenir une description des propriétés JSON prises en charge par SqlSink, consultez l’article [Azure SQL Database connector](data-factory-azure-sql-connector.md) (Connecteur de base de données SQL Azure).</span><span class="sxs-lookup"><span data-stu-id="df5ab-307">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>
2. <span data-ttu-id="df5ab-308">Exécutez la commande suivante pour créer la table de fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="df5ab-308">Run the following command to create the data factory table.</span></span>

    ```PowerShell   
    New-AzureRmDataFactoryPipeline $df -File .\ADFTutorialPipeline.json
    ```

    <span data-ttu-id="df5ab-309">Voici l'exemple de sortie :</span><span class="sxs-lookup"><span data-stu-id="df5ab-309">Here is the sample output:</span></span> 

    ```
    PipelineName      : ADFTutorialPipeline
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.PipelinePropertie
    ProvisioningState : Succeeded
    ```

<span data-ttu-id="df5ab-310">**Félicitations !**</span><span class="sxs-lookup"><span data-stu-id="df5ab-310">**Congratulations!**</span></span> <span data-ttu-id="df5ab-311">Vous avez créé une fabrique de données Azure, avec un pipeline permettant de copier les données d’un stockage Blob Azure vers une base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="df5ab-311">You have successfully created an Azure data factory with a pipeline to copy data from an Azure blob storage to an Azure SQL database.</span></span> 

## <a name="monitor-the-pipeline"></a><span data-ttu-id="df5ab-312">Surveiller le pipeline</span><span class="sxs-lookup"><span data-stu-id="df5ab-312">Monitor the pipeline</span></span>
<span data-ttu-id="df5ab-313">Au cours de cette étape, vous utilisez Azure PowerShell pour surveiller ce qui se passe dans une fabrique de données Azure.</span><span class="sxs-lookup"><span data-stu-id="df5ab-313">In this step, you use Azure PowerShell to monitor what’s going on in an Azure data factory.</span></span>

1. <span data-ttu-id="df5ab-314">Remplacez &lt;DataFactoryName&gt; par le nom de votre fabrique de données, exécutez **Get-AzureRmDataFactory** et affectez la sortie à une variable $df.</span><span class="sxs-lookup"><span data-stu-id="df5ab-314">Replace &lt;DataFactoryName&gt; with the name of your data factory and run **Get-AzureRmDataFactory**, and assign the output to a variable $df.</span></span>

    ```PowerShell  
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name <DataFactoryName>
    ```

    <span data-ttu-id="df5ab-315">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="df5ab-315">For example:</span></span>
    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH0516
    ```
    
    <span data-ttu-id="df5ab-316">Ensuite, exécutez le contenu de $df pour afficher la sortie suivante :</span><span class="sxs-lookup"><span data-stu-id="df5ab-316">Then, run print the contents of $df to see the following output:</span></span> 
    
    ```
    PS C:\ADFGetStartedPSH> $df
    
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DataFactoryId     : 6f194b34-03b3-49ab-8f03-9f8a7b9d3e30
    ResourceGroupName : ADFTutorialResourceGroup
    Location          : West US
    Tags              : {}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DataFactoryProperties
    ProvisioningState : Succeeded
    ```
2. <span data-ttu-id="df5ab-317">Exécutez **Get-AzureRmDataFactorySlice** pour obtenir des détails sur toutes les tranches de **OutputDatabase**, qui correspond au jeu de données de sortie du pipeline.</span><span class="sxs-lookup"><span data-stu-id="df5ab-317">Run **Get-AzureRmDataFactorySlice** to get details about all slices of the **OutputDataset**, which is the output dataset of the pipeline.</span></span>  

    ```PowerShell   
    Get-AzureRmDataFactorySlice $df -DatasetName OutputDataset -StartDateTime 2017-05-11T00:00:00Z
    ```

   <span data-ttu-id="df5ab-318">Ce paramètre doit correspondre à la valeur **Start** dans le pipeline JSON.</span><span class="sxs-lookup"><span data-stu-id="df5ab-318">This setting should match the **Start** value in the pipeline JSON.</span></span> <span data-ttu-id="df5ab-319">Vous devez voir 24 tranches, une pour chaque heure entre 12: 00 du jour actuel et 12: 00 le lendemain.</span><span class="sxs-lookup"><span data-stu-id="df5ab-319">You should see 24 slices, one for each hour from 12 AM of the current day to 12 AM of the next day.</span></span>

   <span data-ttu-id="df5ab-320">Voici trois exemples de tranches de la sortie :</span><span class="sxs-lookup"><span data-stu-id="df5ab-320">Here are three sample slices from the output:</span></span> 

    ``` 
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 11:00:00 PM
    End               : 5/12/2017 12:00:00 AM
    RetryCount        : 0
    State             : Ready
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0

    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 9:00:00 PM
    End               : 5/11/2017 10:00:00 PM
    RetryCount        : 0
    State             : InProgress
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0   

    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 8:00:00 PM
    End               : 5/11/2017 9:00:00 PM
    RetryCount        : 0
    State             : Waiting
    SubState          : ConcurrencyLimit
    LatencyStatus     :
    LongRetryCount    : 0
    ```
3. <span data-ttu-id="df5ab-321">Exécutez **Get-AzureRmDataFactoryRun** pour obtenir les détails d’exécution d’activité pour une tranche **spécifique**.</span><span class="sxs-lookup"><span data-stu-id="df5ab-321">Run **Get-AzureRmDataFactoryRun** to get the details of activity runs for a **specific** slice.</span></span> <span data-ttu-id="df5ab-322">Copiez la valeur date-heure à partir de la sortie de la commande précédente pour spécifier la valeur du paramètre StartDateTime.</span><span class="sxs-lookup"><span data-stu-id="df5ab-322">Copy the date-time value from the output of the previous command to specify the value for the StartDateTime parameter.</span></span> 

    ```PowerShell  
    Get-AzureRmDataFactoryRun $df -DatasetName OutputDataset -StartDateTime "5/11/2017 09:00:00 PM"
    ```

   <span data-ttu-id="df5ab-323">Voici l'exemple de sortie :</span><span class="sxs-lookup"><span data-stu-id="df5ab-323">Here is the sample output:</span></span> 

    ```
    Id                  : c0ddbd75-d0c7-4816-a775-704bbd7c7eab_636301332000000000_636301368000000000_OutputDataset
    ResourceGroupName   : ADFTutorialResourceGroup
    DataFactoryName     : ADFTutorialDataFactoryPSH0516
    DatasetName         : OutputDataset
    ProcessingStartTime : 5/16/2017 8:00:33 PM
    ProcessingEndTime   : 5/16/2017 8:01:36 PM
    PercentComplete     : 100
    DataSliceStart      : 5/11/2017 9:00:00 PM
    DataSliceEnd        : 5/11/2017 10:00:00 PM
    Status              : Succeeded
    Timestamp           : 5/16/2017 8:00:33 PM
    RetryAttempt        : 0
    Properties          : {}
    ErrorMessage        :
    ActivityName        : CopyFromBlobToSQL
    PipelineName        : ADFTutorialPipeline
    Type                : Copy  
    ```

<span data-ttu-id="df5ab-324">Pour obtenir une documentation complète sur les applets de commande Data Factory, consultez la [Référence des applets de commande Data Factory](/powershell/module/azurerm.datafactories).</span><span class="sxs-lookup"><span data-stu-id="df5ab-324">For comprehensive documentation on Data Factory cmdlets, see [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories).</span></span>

## <a name="summary"></a><span data-ttu-id="df5ab-325">Résumé</span><span class="sxs-lookup"><span data-stu-id="df5ab-325">Summary</span></span>
<span data-ttu-id="df5ab-326">Dans ce didacticiel, vous avez créé une fabrique de données Azure pour copier des données d’objet blob Azure dans une base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="df5ab-326">In this tutorial, you created an Azure data factory to copy data from an Azure blob to an Azure SQL database.</span></span> <span data-ttu-id="df5ab-327">Vous avez utilisé PowerShell pour créer la fabrique de données, les services liés, les jeux de données et un pipeline.</span><span class="sxs-lookup"><span data-stu-id="df5ab-327">You used PowerShell to create the data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="df5ab-328">Voici les étapes de premier niveau que vous avez effectuées dans ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="df5ab-328">Here are the high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="df5ab-329">Création d’une **fabrique de données**Azure.</span><span class="sxs-lookup"><span data-stu-id="df5ab-329">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="df5ab-330">Création de **services liés**:</span><span class="sxs-lookup"><span data-stu-id="df5ab-330">Created **linked services**:</span></span>

   <span data-ttu-id="df5ab-331">a.</span><span class="sxs-lookup"><span data-stu-id="df5ab-331">a.</span></span> <span data-ttu-id="df5ab-332">Un service lié **Stockage Azure** pour lier votre compte Stockage Azure contenant des données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="df5ab-332">An **Azure Storage** linked service to link your Azure storage account that holds input data.</span></span>     
   <span data-ttu-id="df5ab-333">b.</span><span class="sxs-lookup"><span data-stu-id="df5ab-333">b.</span></span> <span data-ttu-id="df5ab-334">Un service lié **Azure SQL** pour lier votre base de données SQL contenant les données de sortie.</span><span class="sxs-lookup"><span data-stu-id="df5ab-334">An **Azure SQL** linked service to link your SQL database that holds the output data.</span></span>
3. <span data-ttu-id="df5ab-335">Création de **jeux de données** qui décrivent les données d’entrée et de sortie des pipelines.</span><span class="sxs-lookup"><span data-stu-id="df5ab-335">Created **datasets** that describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="df5ab-336">Création d’un **pipeline** avec une **activité de copie** avec **BlobSource** en tant que source et **SqlSink** en tant que récepteur.</span><span class="sxs-lookup"><span data-stu-id="df5ab-336">Created a **pipeline** with **Copy Activity**, with **BlobSource** as the source and **SqlSink** as the sink.</span></span>

## <a name="next-steps"></a><span data-ttu-id="df5ab-337">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="df5ab-337">Next steps</span></span>
<span data-ttu-id="df5ab-338">Dans ce didacticiel, vous avez utilisé le stockage Blob Azure comme magasin de données source et une base de données SQL Azure comme banque de données de destination dans une opération de copie.</span><span class="sxs-lookup"><span data-stu-id="df5ab-338">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="df5ab-339">Le tableau ci-dessous contient la liste des magasins de données pris en charge en tant que sources et destinations par l’activité de copie :</span><span class="sxs-lookup"><span data-stu-id="df5ab-339">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="df5ab-340">Pour découvrir comment copier des données vers/depuis un magasin de données, cliquez sur le lien du magasin de données dans le tableau.</span><span class="sxs-lookup"><span data-stu-id="df5ab-340">To learn about how to copy data to/from a data store, click the link for the data store in the table.</span></span> 

