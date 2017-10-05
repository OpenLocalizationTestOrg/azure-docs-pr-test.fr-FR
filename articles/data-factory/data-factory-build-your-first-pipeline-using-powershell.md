---
title: "Créer votre première fabrique de données Azure (PowerShell) | Microsoft Docs"
description: "Dans ce didacticiel, vous allez créer un exemple de pipeline Azure Data Factory à l’aide d’Azure PowerShell."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 22ec1236-ea86-4eb7-b903-0e79a58b90c7
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 40a63339be90d0c5d972605c7f6fa029ca1e2ba4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-powershell"></a><span data-ttu-id="d9749-103">Didacticiel : Créer votre première fabrique de données Azure à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d9749-103">Tutorial: Build your first Azure data factory using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d9749-104">Vue d’ensemble et étapes préalables requises</span><span class="sxs-lookup"><span data-stu-id="d9749-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="d9749-105">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="d9749-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="d9749-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d9749-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="d9749-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d9749-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="d9749-108">Modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d9749-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="d9749-109">API REST</span><span class="sxs-lookup"><span data-stu-id="d9749-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)
>
>

<span data-ttu-id="d9749-110">Dans cet article, vous utilisez Azure PowerShell pour créer votre première fabrique de données Azure.</span><span class="sxs-lookup"><span data-stu-id="d9749-110">In this article, you use Azure PowerShell to create your first Azure data factory.</span></span> <span data-ttu-id="d9749-111">Pour suivre le didacticiel avec d’autres outils/Kits de développement logiciel (SDK), sélectionnez une des options dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="d9749-111">To do the tutorial using other tools/SDKs, select one of the options from the drop-down list.</span></span>

<span data-ttu-id="d9749-112">Le pipeline dans ce didacticiel a une activité : **Activité HDInsight Hive**.</span><span class="sxs-lookup"><span data-stu-id="d9749-112">The pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="d9749-113">Cette activité exécute un script Hive sur un cluster HDInsight qui transforme des données d’entrée pour produire des données de sortie.</span><span class="sxs-lookup"><span data-stu-id="d9749-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data to produce output data.</span></span> <span data-ttu-id="d9749-114">Le pipeline est programmé pour s’exécuter une fois par mois entre les heures de début et de fin spécifiées.</span><span class="sxs-lookup"><span data-stu-id="d9749-114">The pipeline is scheduled to run once a month between the specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="d9749-115">Dans ce didacticiel, le pipeline de données transforme les données d’entrée pour produire des données de sortie.</span><span class="sxs-lookup"><span data-stu-id="d9749-115">The data pipeline in this tutorial transforms input data to produce output data.</span></span> <span data-ttu-id="d9749-116">Il ne copie pas les données d’un magasin de données source vers un magasin de données de destination.</span><span class="sxs-lookup"><span data-stu-id="d9749-116">It does not copy data from a source data store to a destination data store.</span></span> <span data-ttu-id="d9749-117">Pour un didacticiel sur la copie de données à l’aide d’Azure Data Factory, consultez [Copie de données Blob Storage vers une base de données SQL à l’aide de Data Factory](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="d9749-117">For a tutorial on how to copy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="d9749-118">Un pipeline peut contenir plusieurs activités.</span><span class="sxs-lookup"><span data-stu-id="d9749-118">A pipeline can have more than one activity.</span></span> <span data-ttu-id="d9749-119">En outre, vous pouvez chaîner deux activités (une après l’autre) en configurant le jeu de données de sortie d’une activité en tant que jeu de données d’entrée de l’autre activité.</span><span class="sxs-lookup"><span data-stu-id="d9749-119">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="d9749-120">Pour plus d’informations, consultez [Planification et exécution dans Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="d9749-120">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9749-121">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d9749-121">Prerequisites</span></span>
* <span data-ttu-id="d9749-122">Lisez l’article [Vue d’ensemble du didacticiel](data-factory-build-your-first-pipeline.md) et effectuez les **étapes préalables requises** .</span><span class="sxs-lookup"><span data-stu-id="d9749-122">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete the **prerequisite** steps.</span></span>
* <span data-ttu-id="d9749-123">Suivez les instructions de l’article [Installation et configuration d’Azure PowerShell](/powershell/azure/overview) pour installer la dernière version d’Azure PowerShell sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="d9749-123">Follow instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) article to install latest version of Azure PowerShell on your computer.</span></span>
* <span data-ttu-id="d9749-124">(facultatif) Cet article ne couvre pas toutes les applets de commande de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d9749-124">(optional) This article does not cover all the Data Factory cmdlets.</span></span> <span data-ttu-id="d9749-125">Consultez la [Référence des applets de commande Data Factory](/powershell/module/azurerm.datafactories) pour obtenir une documentation complète sur les applets de commande Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d9749-125">See [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories) for comprehensive documentation on Data Factory cmdlets.</span></span>

## <a name="create-data-factory"></a><span data-ttu-id="d9749-126">Créer une fabrique de données</span><span class="sxs-lookup"><span data-stu-id="d9749-126">Create data factory</span></span>
<span data-ttu-id="d9749-127">Dans cette étape, vous utilisez Azure PowerShell pour créer une fabrique de données Azure nommée **FirstDataFactoryPSH**.</span><span class="sxs-lookup"><span data-stu-id="d9749-127">In this step, you use Azure PowerShell to create an Azure Data Factory named **FirstDataFactoryPSH**.</span></span> <span data-ttu-id="d9749-128">Une fabrique de données peut avoir un ou plusieurs pipelines.</span><span class="sxs-lookup"><span data-stu-id="d9749-128">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="d9749-129">Un pipeline peut contenir une ou plusieurs activités.</span><span class="sxs-lookup"><span data-stu-id="d9749-129">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="d9749-130">Par exemple, une activité de copie censée copier des données d’un magasin de données source vers un magasin de données de destination, et une activité Hive HDInsight pour exécuter un script Hive pour transformer des données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="d9749-130">For example, a Copy Activity to copy data from a source to a destination data store and a HDInsight Hive activity to run a Hive script to transform input data.</span></span> <span data-ttu-id="d9749-131">Commençons par la création de la fabrique de données dans cette étape.</span><span class="sxs-lookup"><span data-stu-id="d9749-131">Let's start with creating the data factory in this step.</span></span>

1. <span data-ttu-id="d9749-132">Démarrez Azure PowerShell et exécutez la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="d9749-132">Start Azure PowerShell and run the following command.</span></span> <span data-ttu-id="d9749-133">Conservez Azure PowerShell ouvert jusqu’à la fin de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="d9749-133">Keep Azure PowerShell open until the end of this tutorial.</span></span> <span data-ttu-id="d9749-134">Si vous la fermez, puis la rouvrez, vous devez réexécuter ces commandes.</span><span class="sxs-lookup"><span data-stu-id="d9749-134">If you close and reopen, you need to run these commands again.</span></span>
   * <span data-ttu-id="d9749-135">Exécutez la commande suivante, puis saisissez le nom d’utilisateur et le mot de passe que vous avez utilisés pour la connexion au portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d9749-135">Run the following command and enter the user name and password that you use to sign in to the Azure portal.</span></span>
    ```PowerShell
    Login-AzureRmAccount
    ```    
   * <span data-ttu-id="d9749-136">Exécutez la commande suivante pour afficher tous les abonnements de ce compte.</span><span class="sxs-lookup"><span data-stu-id="d9749-136">Run the following command to view all the subscriptions for this account.</span></span>
    ```PowerShell
    Get-AzureRmSubscription 
    ```
   * <span data-ttu-id="d9749-137">Exécutez la commande suivante pour sélectionner l’abonnement que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="d9749-137">Run the following command to select the subscription that you want to work with.</span></span> <span data-ttu-id="d9749-138">Cet abonnement doit être identique à celui utilisé dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d9749-138">This subscription should be the same as the one you used in the Azure portal.</span></span>
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```     
2. <span data-ttu-id="d9749-139">Créez un groupe de ressources Azure nommé **ADFTutorialResourceGroup** en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d9749-139">Create an Azure resource group named **ADFTutorialResourceGroup** by running the following command:</span></span>
    
    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
    <span data-ttu-id="d9749-140">Certaines étapes de ce didacticiel supposent que vous utilisez le groupe de ressources nommé ADFTutorialResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="d9749-140">Some of the steps in this tutorial assume that you use the resource group named ADFTutorialResourceGroup.</span></span> <span data-ttu-id="d9749-141">Si vous utilisez un autre groupe de ressources, vous devrez l’utiliser à la place d’ADFTutorialResourceGroup dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="d9749-141">If you use a different resource group, you need to use it in place of ADFTutorialResourceGroup in this tutorial.</span></span>
3. <span data-ttu-id="d9749-142">Exécutez l’applet de commande **New-AzureRmDataFactory** qui crée une fabrique de données nommée **FirstDataFactoryPSH**.</span><span class="sxs-lookup"><span data-stu-id="d9749-142">Run the **New-AzureRmDataFactory** cmdlet that creates a data factory named **FirstDataFactoryPSH**.</span></span>

    ```PowerShell
    New-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH –Location "West US"
    ```
<span data-ttu-id="d9749-143">Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="d9749-143">Note the following points:</span></span>

* <span data-ttu-id="d9749-144">Le nom de la fabrique de données Azure doit être un nom global unique.</span><span class="sxs-lookup"><span data-stu-id="d9749-144">The name of the Azure Data Factory must be globally unique.</span></span> <span data-ttu-id="d9749-145">Si l’erreur suivante s’affiche : **Le nom de la fabrique de données « FirstDataFactoryPSH » n’est pas disponible**, changez le nom (par exemple en votrenomFirstDataFactoryPSH).</span><span class="sxs-lookup"><span data-stu-id="d9749-145">If you receive the error **Data factory name “FirstDataFactoryPSH” is not available**, change the name (for example, yournameFirstDataFactoryPSH).</span></span> <span data-ttu-id="d9749-146">Utilisez ce nom à la place d’ADFTutorialFactoryPSH quand vous effectuez les étapes de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="d9749-146">Use this name in place of ADFTutorialFactoryPSH while performing steps in this tutorial.</span></span> <span data-ttu-id="d9749-147">Consultez la rubrique [Data Factory - Règles d’affectation des noms](data-factory-naming-rules.md) pour savoir comment nommer les artefacts Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d9749-147">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
* <span data-ttu-id="d9749-148">Pour créer des instances de fabrique de données, vous devez avoir le statut d’administrateur/collaborateur de l’abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="d9749-148">To create Data Factory instances, you need to be a contributor/administrator of the Azure subscription</span></span>
* <span data-ttu-id="d9749-149">Le nom de la fabrique de données pourra être enregistré en tant que nom DNS et devenir ainsi visible publiquement.</span><span class="sxs-lookup"><span data-stu-id="d9749-149">The name of the data factory may be registered as a DNS name in the future and hence become publically visible.</span></span>
* <span data-ttu-id="d9749-150">Si vous recevez le message d’erreur : «**L’abonnement n’est pas inscrit pour utiliser l’espace de noms Microsoft.DataFactory**», effectuez l’une des opérations suivantes et essayez de relancer la publication :</span><span class="sxs-lookup"><span data-stu-id="d9749-150">If you receive the error: "**This subscription is not registered to use namespace Microsoft.DataFactory**", do one of the following and try publishing again:</span></span>

  * <span data-ttu-id="d9749-151">Dans Azure PowerShell, exécutez la commande suivante pour enregistrer le fournisseur Data Factory :</span><span class="sxs-lookup"><span data-stu-id="d9749-151">In Azure PowerShell, run the following command to register the Data Factory provider:</span></span>

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
      <span data-ttu-id="d9749-152">Vous pouvez exécuter la commande suivante pour confirmer l’enregistrement du fournisseur Data Factory :</span><span class="sxs-lookup"><span data-stu-id="d9749-152">You can run the following command to confirm that the Data Factory provider is registered:</span></span>

    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="d9749-153">Connectez-vous au [portail Azure](https://portal.azure.com) à l’aide de l’abonnement Azure et accédez à un panneau Data Factory (ou) créez une fabrique de données dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d9749-153">Login using the Azure subscription into the [Azure portal](https://portal.azure.com) and navigate to a Data Factory blade (or) create a data factory in the Azure portal.</span></span> <span data-ttu-id="d9749-154">Cette action enregistre automatiquement le fournisseur.</span><span class="sxs-lookup"><span data-stu-id="d9749-154">This action automatically registers the provider for you.</span></span>

<span data-ttu-id="d9749-155">Avant de créer un pipeline, vous devez d’abord créer quelques entités de la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="d9749-155">Before creating a pipeline, you need to create a few Data Factory entities first.</span></span> <span data-ttu-id="d9749-156">Créez d’abord des services liés pour lier des magasins de données/calculs à votre magasin de données, définissez des jeux de données d’entrée et de sortie pour représenter les données d’entrée/sortie dans les magasins de données liés, puis créez le pipeline avec une activité qui utilise ces jeux de données.</span><span class="sxs-lookup"><span data-stu-id="d9749-156">You first create linked services to link data stores/computes to your data store, define input and output datasets to represent input/output data in linked data stores, and then create the pipeline with an activity that uses these datasets.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="d9749-157">Créer des services liés</span><span class="sxs-lookup"><span data-stu-id="d9749-157">Create linked services</span></span>
<span data-ttu-id="d9749-158">Dans cette étape, vous liez votre compte Stockage Azure et un cluster Azure HDInsight à la demande à votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="d9749-158">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster to your data factory.</span></span> <span data-ttu-id="d9749-159">Le compte Stockage Azure contient les données d’entrée et de sortie pour le pipeline de cet exemple.</span><span class="sxs-lookup"><span data-stu-id="d9749-159">The Azure Storage account holds the input and output data for the pipeline in this sample.</span></span> <span data-ttu-id="d9749-160">Le service lié HDInsight est utilisé pour exécuter le script Hive spécifié dans l’activité du pipeline de cet exemple.</span><span class="sxs-lookup"><span data-stu-id="d9749-160">The HDInsight linked service is used to run a Hive script specified in the activity of the pipeline in this sample.</span></span> <span data-ttu-id="d9749-161">Identifiez les services de magasin de données/de calcul qui sont utilisés dans votre scénario et les lier à la fabrique de données en créant des services liés.</span><span class="sxs-lookup"><span data-stu-id="d9749-161">Identify what data store/compute services are used in your scenario and link those services to the data factory by creating linked services.</span></span>

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="d9749-162">Créer le service lié Azure Storage</span><span class="sxs-lookup"><span data-stu-id="d9749-162">Create Azure Storage linked service</span></span>
<span data-ttu-id="d9749-163">Dans cette étape, vous liez votre compte Stockage Azure à votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="d9749-163">In this step, you link your Azure Storage account to your data factory.</span></span> <span data-ttu-id="d9749-164">Vous utilisez le même compte Stockage Azure pour stocker les données d’entrée/sortie et le fichier de script HQL.</span><span class="sxs-lookup"><span data-stu-id="d9749-164">You use the same Azure Storage account to store input/output data and the HQL script file.</span></span>

1. <span data-ttu-id="d9749-165">Créez un fichier JSON nommé StorageLinkedService.json dans le dossier C:\ADFGetStarted, avec le contenu suivant.</span><span class="sxs-lookup"><span data-stu-id="d9749-165">Create a JSON file named StorageLinkedService.json in the C:\ADFGetStarted folder with the following content.</span></span> <span data-ttu-id="d9749-166">Créez le dossier ADFGetStarted s’il n’existe pas encore.</span><span class="sxs-lookup"><span data-stu-id="d9749-166">Create the folder ADFGetStarted if it does not already exist.</span></span>

    ```json
    {
        "name": "StorageLinkedService",
        "properties": {
            "type": "AzureStorage",
            "description": "",
            "typeProperties": {
                "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        }
    }
    ```
    <span data-ttu-id="d9749-167">Remplacez **account name** par le nom de votre compte de stockage Azure et **account key** par sa clé d’accès.</span><span class="sxs-lookup"><span data-stu-id="d9749-167">Replace **account name** with the name of your Azure storage account and **account key** with the access key of the Azure storage account.</span></span> <span data-ttu-id="d9749-168">Pour savoir comment obtenir votre clé d’accès de stockage, reportez-vous aux informations sur l’affichage, la copie et la régénération de clés d’accès de stockage dans [Gérer votre compte de stockage](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="d9749-168">To learn how to get your storage access key, see the information about how to view, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
2. <span data-ttu-id="d9749-169">Dans Azure PowerShell, accédez au dossier ADFGetStarted.</span><span class="sxs-lookup"><span data-stu-id="d9749-169">In Azure PowerShell, switch to the ADFGetStarted folder.</span></span>
3. <span data-ttu-id="d9749-170">Vous pouvez utiliser l’applet de commande **New-AzureRmDataFactoryLinkedService** qui crée un service lié.</span><span class="sxs-lookup"><span data-stu-id="d9749-170">You can use the **New-AzureRmDataFactoryLinkedService** cmdlet that creates a linked service.</span></span> <span data-ttu-id="d9749-171">Cette applet de commande et d’autres applets de commande Data Factory que vous utilisez dans ce didacticiel vous obligent à transmettre des valeurs aux paramètres *ResourceGroupName* et *DataFactoryName*.</span><span class="sxs-lookup"><span data-stu-id="d9749-171">This cmdlet and other Data Factory cmdlets you use in this tutorial requires you to pass values for the *ResourceGroupName* and *DataFactoryName* parameters.</span></span> <span data-ttu-id="d9749-172">Vous pouvez également utiliser **Get-AzureRmDataFactory** pour obtenir un objet **DataFactory** et transmettre l’objet sans avoir à saisir *ResourceGroupName* et *DataFactoryName* chaque fois que vous exécutez une applet de commande.</span><span class="sxs-lookup"><span data-stu-id="d9749-172">Alternatively, you can use **Get-AzureRmDataFactory** to get a **DataFactory** object and pass the object without typing *ResourceGroupName* and *DataFactoryName* each time you run a cmdlet.</span></span> <span data-ttu-id="d9749-173">Exécutez la commande suivante pour affecter le résultat de l’applet de commande **Get-AzureRmDataFactory** à une variable **$df**.</span><span class="sxs-lookup"><span data-stu-id="d9749-173">Run the following command to assign the output of the **Get-AzureRmDataFactory** cmdlet to a **$df** variable.</span></span>

    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH
    ```
4. <span data-ttu-id="d9749-174">Exécutez maintenant l’applet de commande **New-AzureRmDataFactoryLinkedService** qui crée le service **StorageLinkedService** lié.</span><span class="sxs-lookup"><span data-stu-id="d9749-174">Now, run the **New-AzureRmDataFactoryLinkedService** cmdlet that creates the linked **StorageLinkedService** service.</span></span>

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\StorageLinkedService.json
    ```
    <span data-ttu-id="d9749-175">Si vous n’avez pas exécuté l’applet de commande **Get-AzureRmDataFactory** et affecté la sortie à la variable **$df**, vous devez spécifier des valeurs pour les paramètres *ResourceGroupName* et *DataFactoryName* comme suit.</span><span class="sxs-lookup"><span data-stu-id="d9749-175">If you hadn't run the **Get-AzureRmDataFactory** cmdlet and assigned the output to the **$df** variable, you would have to specify values for the *ResourceGroupName* and *DataFactoryName* parameters as follows.</span></span>

    ```PowerShell
    New-AzureRmDataFactoryLinkedService -ResourceGroupName ADFTutorialResourceGroup -DataFactoryName FirstDataFactoryPSH -File .\StorageLinkedService.json
    ```
    <span data-ttu-id="d9749-176">Si vous fermez Azure PowerShell au milieu du didacticiel, vous devez exécuter l’applet de commande **Get-AzureRmDataFactory** au prochain démarrage d’Azure PowerShell pour terminer le didacticiel.</span><span class="sxs-lookup"><span data-stu-id="d9749-176">If you close Azure PowerShell in the middle of the tutorial, you have to run the **Get-AzureRmDataFactory** cmdlet next time you start Azure PowerShell to complete the tutorial.</span></span>

### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="d9749-177">Créer le service lié Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="d9749-177">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="d9749-178">Dans cette étape, vous liez un cluster HDInsight à la demande à votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="d9749-178">In this step, you link an on-demand HDInsight cluster to your data factory.</span></span> <span data-ttu-id="d9749-179">Le cluster HDInsight est automatiquement créé lors de l’exécution, puis supprimé une fois le traitement effectué et au terme du délai d’inactivité spécifié.</span><span class="sxs-lookup"><span data-stu-id="d9749-179">The HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for the specified amount of time.</span></span> <span data-ttu-id="d9749-180">Vous pouvez utiliser votre propre cluster HDInsight au lieu d’utiliser un cluster HDInsight à la demande.</span><span class="sxs-lookup"><span data-stu-id="d9749-180">You could use your own HDInsight cluster instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="d9749-181">Pour plus d’informations, consultez [Services de calcul liés](data-factory-compute-linked-services.md) .</span><span class="sxs-lookup"><span data-stu-id="d9749-181">See [Compute Linked Services](data-factory-compute-linked-services.md) for details.</span></span>

1. <span data-ttu-id="d9749-182">Créez un fichier JSON nommé **HDInsightOnDemandLinkedService**.json dans le dossier **C:\ADFGetStarted** avec le contenu suivant.</span><span class="sxs-lookup"><span data-stu-id="d9749-182">Create a JSON file named **HDInsightOnDemandLinkedService**.json in the **C:\ADFGetStarted** folder with the following content.</span></span>

    ```json
    {
        "name": "HDInsightOnDemandLinkedService",
        "properties": {
            "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "linkedServiceName": "StorageLinkedService"
            }
        }
    }
    ```
    <span data-ttu-id="d9749-183">Le tableau suivant décrit les propriétés JSON utilisées dans l'extrait de code :</span><span class="sxs-lookup"><span data-stu-id="d9749-183">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

   | <span data-ttu-id="d9749-184">Propriété</span><span class="sxs-lookup"><span data-stu-id="d9749-184">Property</span></span> | <span data-ttu-id="d9749-185">Description</span><span class="sxs-lookup"><span data-stu-id="d9749-185">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="d9749-186">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="d9749-186">ClusterSize</span></span> |<span data-ttu-id="d9749-187">Spécifie la taille du cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d9749-187">Specifies the size of the HDInsight cluster.</span></span> |
   | <span data-ttu-id="d9749-188">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="d9749-188">TimeToLive</span></span> |<span data-ttu-id="d9749-189">Spécifie la durée d’inactivité du cluster HDInsight avant sa suppression.</span><span class="sxs-lookup"><span data-stu-id="d9749-189">Specifies that the idle time for the HDInsight cluster, before it is deleted.</span></span> |
   | <span data-ttu-id="d9749-190">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="d9749-190">linkedServiceName</span></span> |<span data-ttu-id="d9749-191">Spécifie le compte de stockage utilisé pour stocker les journaux générés par HDInsight</span><span class="sxs-lookup"><span data-stu-id="d9749-191">Specifies the storage account that is used to store the logs that are generated by HDInsight</span></span> |

    <span data-ttu-id="d9749-192">Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="d9749-192">Note the following points:</span></span>

   * <span data-ttu-id="d9749-193">La fabrique de données crée pour vous un cluster HDInsight **Linux** avec le code JSON.</span><span class="sxs-lookup"><span data-stu-id="d9749-193">The Data Factory creates a **Linux-based** HDInsight cluster for you with the JSON.</span></span> <span data-ttu-id="d9749-194">Pour plus d’informations, voir [Service lié à la demande Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="d9749-194">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
   * <span data-ttu-id="d9749-195">Vous pouvez utiliser votre **propre cluster HDInsight** au lieu d’utiliser un cluster HDInsight à la demande.</span><span class="sxs-lookup"><span data-stu-id="d9749-195">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="d9749-196">Pour plus d’informations, voir [Service lié Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="d9749-196">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
   * <span data-ttu-id="d9749-197">Le cluster HDInsight crée un **conteneur par défaut** dans le stockage d’objets blob que vous avez spécifié dans le JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="d9749-197">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (**linkedServiceName**).</span></span> <span data-ttu-id="d9749-198">HDInsight ne supprime pas ce conteneur lorsque le cluster est supprimé.</span><span class="sxs-lookup"><span data-stu-id="d9749-198">HDInsight does not delete this container when the cluster is deleted.</span></span> <span data-ttu-id="d9749-199">Ce comportement est normal.</span><span class="sxs-lookup"><span data-stu-id="d9749-199">This behavior is by design.</span></span> <span data-ttu-id="d9749-200">Avec le service lié HDInsight disponible à la demande, un cluster HDInsight est créé dès qu’une tranche est traitée, à moins qu’il n’existe un cluster actif (**timeToLive**).</span><span class="sxs-lookup"><span data-stu-id="d9749-200">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**).</span></span> <span data-ttu-id="d9749-201">Ce cluster est supprimé, une fois le traitement terminé.</span><span class="sxs-lookup"><span data-stu-id="d9749-201">The cluster is automatically deleted when the processing is done.</span></span>

       <span data-ttu-id="d9749-202">Comme un nombre croissant de tranches sont traitées, vous voyez un grand nombre de conteneurs dans votre stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="d9749-202">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="d9749-203">Si vous n’en avez pas besoin pour dépanner les travaux, il se peut que vous deviez les supprimer pour réduire les frais de stockage.</span><span class="sxs-lookup"><span data-stu-id="d9749-203">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="d9749-204">Le nom de ces conteneurs suit un modèle : « **nomdevotrefabriquededonnéesadf**-**nomduservicelié**-horodatage ».</span><span class="sxs-lookup"><span data-stu-id="d9749-204">The names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="d9749-205">Utilisez des outils tels que [Microsoft Storage Explorer](http://storageexplorer.com/) pour supprimer des conteneurs dans votre stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="d9749-205">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span></span>

     <span data-ttu-id="d9749-206">Pour plus d’informations, voir [Service lié à la demande Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="d9749-206">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
2. <span data-ttu-id="d9749-207">Exécutez l’applet de commande **New-AzureRmDataFactoryLinkedService** qui crée le service lié nommé HDInsightOnDemandLinkedService.</span><span class="sxs-lookup"><span data-stu-id="d9749-207">Run the **New-AzureRmDataFactoryLinkedService** cmdlet that creates the linked service called HDInsightOnDemandLinkedService.</span></span>
    
    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\HDInsightOnDemandLinkedService.json
    ```

## <a name="create-datasets"></a><span data-ttu-id="d9749-208">Créer des jeux de données</span><span class="sxs-lookup"><span data-stu-id="d9749-208">Create datasets</span></span>
<span data-ttu-id="d9749-209">Dans cette étape, vous créez des jeux de données afin de représenter les données d’entrée et de sortie pour le traitement Hive.</span><span class="sxs-lookup"><span data-stu-id="d9749-209">In this step, you create datasets to represent the input and output data for Hive processing.</span></span> <span data-ttu-id="d9749-210">Ces jeux de données font référence au service **StorageLinkedService** que vous avez créé précédemment dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="d9749-210">These datasets refer to the **StorageLinkedService** you have created earlier in this tutorial.</span></span> <span data-ttu-id="d9749-211">Le service lié pointe vers un compte de stockage Azure, et les jeux de données spécifient le conteneur, le dossier et le nom de fichier dans le stockage qui contient les données d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="d9749-211">The linked service points to an Azure Storage account and datasets specify container, folder, file name in the storage that holds input and output data.</span></span>

### <a name="create-input-dataset"></a><span data-ttu-id="d9749-212">Créer le jeu de données d’entrée</span><span class="sxs-lookup"><span data-stu-id="d9749-212">Create input dataset</span></span>
1. <span data-ttu-id="d9749-213">Créez un fichier JSON nommé **InputTable.json** dans le dossier **C:\ADFGetStarted** avec le contenu suivant :</span><span class="sxs-lookup"><span data-stu-id="d9749-213">Create a JSON file named **InputTable.json** in the **C:\ADFGetStarted** folder with the following content:</span></span>

    ```json
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "StorageLinkedService",
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
    <span data-ttu-id="d9749-214">Le code JSON définit un jeu de données nommé **AzureBlobInput**, qui représente les données d’entrée correspondant à une activité du pipeline.</span><span class="sxs-lookup"><span data-stu-id="d9749-214">The JSON defines a dataset named **AzureBlobInput**, which represents input data for an activity in the pipeline.</span></span> <span data-ttu-id="d9749-215">En outre, ce code spécifie que les données d’entrée figurent dans le conteneur d’objets blob **adfgetstarted** et dans le dossier **inputdata**.</span><span class="sxs-lookup"><span data-stu-id="d9749-215">In addition, it specifies that the input data is located in the blob container called **adfgetstarted** and the folder called **inputdata**.</span></span>

    <span data-ttu-id="d9749-216">Le tableau suivant décrit les propriétés JSON utilisées dans l'extrait de code :</span><span class="sxs-lookup"><span data-stu-id="d9749-216">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

   | <span data-ttu-id="d9749-217">Propriété</span><span class="sxs-lookup"><span data-stu-id="d9749-217">Property</span></span> | <span data-ttu-id="d9749-218">Description</span><span class="sxs-lookup"><span data-stu-id="d9749-218">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="d9749-219">type</span><span class="sxs-lookup"><span data-stu-id="d9749-219">type</span></span> |<span data-ttu-id="d9749-220">La propriété type est définie sur AzureBlob, car les données se trouvent dans le stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="d9749-220">The type property is set to AzureBlob because data resides in Azure blob storage.</span></span> |
   | <span data-ttu-id="d9749-221">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="d9749-221">linkedServiceName</span></span> |<span data-ttu-id="d9749-222">fait référence au service StorageLinkedService que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="d9749-222">refers to the StorageLinkedService you created earlier.</span></span> |
   | <span data-ttu-id="d9749-223">fileName</span><span class="sxs-lookup"><span data-stu-id="d9749-223">fileName</span></span> |<span data-ttu-id="d9749-224">Cette propriété est facultative.</span><span class="sxs-lookup"><span data-stu-id="d9749-224">This property is optional.</span></span> <span data-ttu-id="d9749-225">Si vous omettez cette propriété, tous les fichiers spécifiés dans le paramètre folderPath sont récupérés.</span><span class="sxs-lookup"><span data-stu-id="d9749-225">If you omit this property, all the files from the folderPath are picked.</span></span> <span data-ttu-id="d9749-226">Dans le cas présent, seul le fichier input.log est traité.</span><span class="sxs-lookup"><span data-stu-id="d9749-226">In this case, only the input.log is processed.</span></span> |
   | <span data-ttu-id="d9749-227">type</span><span class="sxs-lookup"><span data-stu-id="d9749-227">type</span></span> |<span data-ttu-id="d9749-228">Les fichiers journaux sont au format texte : nous utilisons donc TextFormat.</span><span class="sxs-lookup"><span data-stu-id="d9749-228">The log files are in text format, so we use TextFormat.</span></span> |
   | <span data-ttu-id="d9749-229">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="d9749-229">columnDelimiter</span></span> |<span data-ttu-id="d9749-230">Les colonnes des fichiers journaux sont délimitées par une virgule (,).</span><span class="sxs-lookup"><span data-stu-id="d9749-230">columns in the log files are delimited by the comma character (,).</span></span> |
   | <span data-ttu-id="d9749-231">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="d9749-231">frequency/interval</span></span> |<span data-ttu-id="d9749-232">La fréquence est définie sur Mois et l’intervalle est 1, ce qui signifie que les segments d’entrée sont disponibles mensuellement.</span><span class="sxs-lookup"><span data-stu-id="d9749-232">frequency set to Month and interval is 1, which means that the input slices are available monthly.</span></span> |
   | <span data-ttu-id="d9749-233">external</span><span class="sxs-lookup"><span data-stu-id="d9749-233">external</span></span> |<span data-ttu-id="d9749-234">Cette propriété a la valeur true si les données d’entrée ne sont pas générées par le service Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d9749-234">this property is set to true if the input data is not generated by the Data Factory service.</span></span> |
2. <span data-ttu-id="d9749-235">Exécutez la commande suivante dans Azure PowerShell pour créer le jeu de données Data Factory :</span><span class="sxs-lookup"><span data-stu-id="d9749-235">Run the following command in Azure PowerShell to create the Data Factory dataset:</span></span>

    ```PowerShell
    New-AzureRmDataFactoryDataset $df -File .\InputTable.json
    ```

### <a name="create-output-dataset"></a><span data-ttu-id="d9749-236">Créer un jeu de données de sortie</span><span class="sxs-lookup"><span data-stu-id="d9749-236">Create output dataset</span></span>
<span data-ttu-id="d9749-237">Vous allez maintenant créer le jeu de données de sortie pour représenter les données de sortie stockées dans le stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="d9749-237">Now, you create the output dataset to represent the output data stored in the Azure Blob storage.</span></span>

1. <span data-ttu-id="d9749-238">Créez un fichier JSON nommé **OutputTable.json** dans le dossier **C:\ADFGetStarted** avec le contenu suivant :</span><span class="sxs-lookup"><span data-stu-id="d9749-238">Create a JSON file named **OutputTable.json** in the **C:\ADFGetStarted** folder with the following content:</span></span>

    ```json
    {
      "name": "AzureBlobOutput",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
          "folderPath": "adfgetstarted/partitioneddata",
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "availability": {
          "frequency": "Month",
          "interval": 1
        }
      }
    }
    ```
    <span data-ttu-id="d9749-239">Le code JSON définit un jeu de données nommé **AzureBlobOutput**, qui représente les données de sortie correspondant à une activité du pipeline.</span><span class="sxs-lookup"><span data-stu-id="d9749-239">The JSON defines a dataset named **AzureBlobOutput**, which represents output data for an activity in the pipeline.</span></span> <span data-ttu-id="d9749-240">En outre, ce code spécifie que les résultats sont stockés dans le conteneur d’objets blob **adfgetstarted** et dans le dossier **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="d9749-240">In addition, it specifies that the results are stored in the blob container called **adfgetstarted** and the folder called **partitioneddata**.</span></span> <span data-ttu-id="d9749-241">La section **availability** spécifie que le jeu de données de sortie est produit tous les mois.</span><span class="sxs-lookup"><span data-stu-id="d9749-241">The **availability** section specifies that the output dataset is produced on a monthly basis.</span></span>
2. <span data-ttu-id="d9749-242">Exécutez la commande suivante dans Azure PowerShell pour créer le jeu de données Data Factory :</span><span class="sxs-lookup"><span data-stu-id="d9749-242">Run the following command in Azure PowerShell to create the Data Factory dataset:</span></span>

    ```PowerShell
    New-AzureRmDataFactoryDataset $df -File .\OutputTable.json
    ```

## <a name="create-pipeline"></a><span data-ttu-id="d9749-243">Création d’un pipeline</span><span class="sxs-lookup"><span data-stu-id="d9749-243">Create pipeline</span></span>
<span data-ttu-id="d9749-244">Dans cette étape, vous créez votre premier pipeline avec une activité **HDInsightHive** .</span><span class="sxs-lookup"><span data-stu-id="d9749-244">In this step, you create your first pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="d9749-245">La tranche d’entrée est disponible mensuellement (fréquence : Mois, intervalle : 1), la tranche de sortie est produite mensuellement et la propriété du planificateur pour l’activité est également définie sur Mensuellement.</span><span class="sxs-lookup"><span data-stu-id="d9749-245">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and the scheduler property for the activity is also set to monthly.</span></span> <span data-ttu-id="d9749-246">Les paramètres pour le jeu de données de sortie et le planificateur d’activité doivent correspondre.</span><span class="sxs-lookup"><span data-stu-id="d9749-246">The settings for the output dataset and the activity scheduler must match.</span></span> <span data-ttu-id="d9749-247">À ce stade, c'est le jeu de données de sortie qui pilote la planification : vous devez donc créer un jeu de données de sortie même si l’activité ne génère aucune sortie.</span><span class="sxs-lookup"><span data-stu-id="d9749-247">Currently, output dataset is what drives the schedule, so you must create an output dataset even if the activity does not produce any output.</span></span> <span data-ttu-id="d9749-248">Si l’activité ne prend aucune entrée, vous pouvez ignorer la création du jeu de données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="d9749-248">If the activity doesn't take any input, you can skip creating the input dataset.</span></span> <span data-ttu-id="d9749-249">Les propriétés utilisées dans le code JSON suivant sont expliquées à la fin de cette section.</span><span class="sxs-lookup"><span data-stu-id="d9749-249">The properties used in the following JSON are explained at the end of this section.</span></span>

1. <span data-ttu-id="d9749-250">Créez un fichier JSON nommé MyFirstPipelinePSH.json dans le dossier C:\ADFGetStarted avec le contenu suivant :</span><span class="sxs-lookup"><span data-stu-id="d9749-250">Create a JSON file named MyFirstPipelinePSH.json in the C:\ADFGetStarted folder with the following content:</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="d9749-251">Dans le code JSON, remplacez **storageaccountname** par le nom de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="d9749-251">Replace **storageaccountname** with the name of your storage account in the JSON.</span></span>
   >
   >

    ```json
    {
        "name": "MyFirstPipeline",
        "properties": {
            "description": "My first Azure Data Factory pipeline",
            "activities": [
                {
                    "type": "HDInsightHive",
                    "typeProperties": {
                        "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                        "scriptLinkedService": "StorageLinkedService",
                        "defines": {
                            "inputtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/inputdata",
                            "partitionedtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/partitioneddata"
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
                    "scheduler": {
                        "frequency": "Month",
                        "interval": 1
                    },
                    "name": "RunSampleHiveActivity",
                    "linkedServiceName": "HDInsightOnDemandLinkedService"
                }
            ],
            "start": "2017-07-01T00:00:00Z",
            "end": "2017-07-02T00:00:00Z",
            "isPaused": false
        }
    }
    ```
    <span data-ttu-id="d9749-252">Dans l’extrait de code JSON, vous créez un pipeline qui se compose d’une seule activité utilisant Hive pour traiter des données sur un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d9749-252">In the JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive to process Data on an HDInsight cluster.</span></span>

    <span data-ttu-id="d9749-253">Le fichier de script Hive, **partitionweblogs.hql**, est stocké dans le compte de stockage Azure (spécifié par le service scriptLinkedService, appelé **StorageLinkedService**) et dans un dossier **script** du conteneur **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="d9749-253">The Hive script file, **partitionweblogs.hql**, is stored in the Azure storage account (specified by the scriptLinkedService, called **StorageLinkedService**), and in **script** folder in the container **adfgetstarted**.</span></span>

    <span data-ttu-id="d9749-254">La section **defines** est utilisée pour spécifier les paramètres d’exécution passés au script Hive comme valeurs de configuration Hive (par exemple ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span><span class="sxs-lookup"><span data-stu-id="d9749-254">The **defines** section is used to specify the runtime settings that be passed to the hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span></span>

    <span data-ttu-id="d9749-255">Les propriétés **start** et **end** du pipeline spécifient la période active du pipeline.</span><span class="sxs-lookup"><span data-stu-id="d9749-255">The **start** and **end** properties of the pipeline specifies the active period of the pipeline.</span></span>

    <span data-ttu-id="d9749-256">Dans l’activité JSON, vous spécifiez que le script Hive s’exécute sur le calcul spécifié par le service **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="d9749-256">In the activity JSON, you specify that the Hive script runs on the compute specified by the **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d9749-257">Consultez « Pipeline JSON » dans [Pipelines et activités dans Azure Data Factory](data-factory-create-pipelines.md) pour plus d’informations sur les propriétés JSON utilisées dans l’exemple.</span><span class="sxs-lookup"><span data-stu-id="d9749-257">See "Pipeline JSON" in [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) for details about JSON properties that are used in the example.</span></span>

2. <span data-ttu-id="d9749-258">Vérifiez que le fichier **input.log** apparaît dans le dossier **adfgetstarted/inputdata** du Stockage Blob Azure, puis exécutez la commande suivante pour déployer le pipeline.</span><span class="sxs-lookup"><span data-stu-id="d9749-258">Confirm that you see the **input.log** file in the **adfgetstarted/inputdata** folder in the Azure blob storage, and run the following command to deploy the pipeline.</span></span> <span data-ttu-id="d9749-259">Étant donné que les valeurs pour **start** et **end** sont définies sur des valeurs antérieures au moment actuel, et que **isPaused** est défini sur false, le pipeline (activité dans le pipeline) s’exécute immédiatement après le déploiement.</span><span class="sxs-lookup"><span data-stu-id="d9749-259">Since the **start** and **end** times are set in the past and **isPaused** is set to false, the pipeline (activity in the pipeline) runs immediately after you deploy.</span></span>

    ```PowerShell
    New-AzureRmDataFactoryPipeline $df -File .\MyFirstPipelinePSH.json
    ```
3. <span data-ttu-id="d9749-260">Félicitations, vous avez réussi à créer votre premier pipeline avec Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d9749-260">Congratulations, you have successfully created your first pipeline using Azure PowerShell!</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="d9749-261">Surveillance d’un pipeline</span><span class="sxs-lookup"><span data-stu-id="d9749-261">Monitor pipeline</span></span>
<span data-ttu-id="d9749-262">Au cours de cette étape, vous utilisez Azure PowerShell pour surveiller ce qui se passe dans une fabrique de données Azure.</span><span class="sxs-lookup"><span data-stu-id="d9749-262">In this step, you use Azure PowerShell to monitor what’s going on in an Azure data factory.</span></span>

1. <span data-ttu-id="d9749-263">Exécutez **Get-AzureRmDataFactory** et affectez le résultat à une variable **$df**.</span><span class="sxs-lookup"><span data-stu-id="d9749-263">Run **Get-AzureRmDataFactory** and assign the output to a **$df** variable.</span></span>

    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH
    ```
2. <span data-ttu-id="d9749-264">Exécutez **Get-AzureRmDataFactorySlice** pour obtenir des détails sur toutes les tranches de **EmpSQLTable**, qui correspond à la table de sortie du pipeline.</span><span class="sxs-lookup"><span data-stu-id="d9749-264">Run **Get-AzureRmDataFactorySlice** to get details about all slices of the **EmpSQLTable**, which is the output table of the pipeline.</span></span>

    ```PowerShell
    Get-AzureRmDataFactorySlice $df -DatasetName AzureBlobOutput -StartDateTime 2017-07-01
    ```
    <span data-ttu-id="d9749-265">Notez que la valeur StartDateTime que vous spécifiez ici est identique à l’heure de début que vous avez spécifiée dans le pipeline de JSON.</span><span class="sxs-lookup"><span data-stu-id="d9749-265">Notice that the StartDateTime you specify here is the same start time specified in the pipeline JSON.</span></span> <span data-ttu-id="d9749-266">Voici l'exemple de sortie :</span><span class="sxs-lookup"><span data-stu-id="d9749-266">Here is the sample output:</span></span>

    ```PowerShell
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : FirstDataFactoryPSH
    DatasetName       : AzureBlobOutput
    Start             : 7/1/2017 12:00:00 AM
    End               : 7/2/2017 12:00:00 AM
    RetryCount        : 0
    State             : InProgress
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0
    ```
3. <span data-ttu-id="d9749-267">Exécutez **Get-AzureRmDataFactoryRun** pour obtenir les détails des exécutions d’activité pour un segment spécifique.</span><span class="sxs-lookup"><span data-stu-id="d9749-267">Run **Get-AzureRmDataFactoryRun** to get the details of activity runs for a specific slice.</span></span>

    ```PowerShell
    Get-AzureRmDataFactoryRun $df -DatasetName AzureBlobOutput -StartDateTime 2017-07-01
    ```

    <span data-ttu-id="d9749-268">Voici l'exemple de sortie :</span><span class="sxs-lookup"><span data-stu-id="d9749-268">Here is the sample output:</span></span> 

    ```PowerShell
    Id                  : 0f6334f2-d56c-4d48-b427-d4f0fb4ef883_635268096000000000_635292288000000000_AzureBlobOutput
    ResourceGroupName   : ADFTutorialResourceGroup
    DataFactoryName     : FirstDataFactoryPSH
    DatasetName         : AzureBlobOutput
    ProcessingStartTime : 12/18/2015 4:50:33 AM
    ProcessingEndTime   : 12/31/9999 11:59:59 PM
    PercentComplete     : 0
    DataSliceStart      : 7/1/2017 12:00:00 AM
    DataSliceEnd        : 7/2/2017 12:00:00 AM
    Status              : AllocatingResources
    Timestamp           : 12/18/2015 4:50:33 AM
    RetryAttempt        : 0
    Properties          : {}
    ErrorMessage        :
    ActivityName        : RunSampleHiveActivity
    PipelineName        : MyFirstPipeline
    Type                : Script
    ```
    <span data-ttu-id="d9749-269">Vous pouvez continuer d’exécuter cette applet de commande jusqu’à ce que le segment apparaisse dans l’état **Prêt** ou **En échec**.</span><span class="sxs-lookup"><span data-stu-id="d9749-269">You can keep running this cmdlet until you see the slice in **Ready** state or **Failed** state.</span></span> <span data-ttu-id="d9749-270">Quand l’état du segment est Prêt, vérifiez la présence des données de sortie dans le dossier **partitioneddata** du conteneur **adfgetstarted** de votre stockage d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="d9749-270">When the slice is in Ready state, check the **partitioneddata** folder in the **adfgetstarted** container in your blob storage for the output data.</span></span>  <span data-ttu-id="d9749-271">La création d’un cluster HDInsight à la demande prend généralement un certain temps.</span><span class="sxs-lookup"><span data-stu-id="d9749-271">Creation of an on-demand HDInsight cluster usually takes some time.</span></span>

    ![données de sortie](./media/data-factory-build-your-first-pipeline-using-powershell/three-ouptut-files.png)

> [!IMPORTANT]
> <span data-ttu-id="d9749-273">La création d’un cluster HDInsight à la demande prend généralement un certain temps (environ 20 minutes).</span><span class="sxs-lookup"><span data-stu-id="d9749-273">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="d9749-274">Le pipeline devrait donc traiter la tranche en **30 minutes environ** .</span><span class="sxs-lookup"><span data-stu-id="d9749-274">Therefore, expect the pipeline to take **approximately 30 minutes** to process the slice.</span></span>
>
> <span data-ttu-id="d9749-275">Le fichier d’entrée sera supprimé lorsque la tranche est traitée avec succès.</span><span class="sxs-lookup"><span data-stu-id="d9749-275">The input file gets deleted when the slice is processed successfully.</span></span> <span data-ttu-id="d9749-276">Par conséquent, si vous souhaitez réexécuter la tranche ou refaire le didacticiel, chargez le fichier d’entrée (input.log) dans le dossier inputdata du conteneur adfgetstarted.</span><span class="sxs-lookup"><span data-stu-id="d9749-276">Therefore, if you want to rerun the slice or do the tutorial again, upload the input file (input.log) to the inputdata folder of the adfgetstarted container.</span></span>
>
>

## <a name="summary"></a><span data-ttu-id="d9749-277">Résumé</span><span class="sxs-lookup"><span data-stu-id="d9749-277">Summary</span></span>
<span data-ttu-id="d9749-278">Dans ce didacticiel, vous avez créé une fabrique de données Azure pour traiter des données en exécutant le script Hive sur un cluster Hadoop HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d9749-278">In this tutorial, you created an Azure data factory to process data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="d9749-279">Vous avez effectué les étapes suivantes dans le portail Azure à l’aide de Data Factory Editor :</span><span class="sxs-lookup"><span data-stu-id="d9749-279">You used the Data Factory Editor in the Azure portal to do the following steps:</span></span>

1. <span data-ttu-id="d9749-280">Création d’une **fabrique de données**Azure.</span><span class="sxs-lookup"><span data-stu-id="d9749-280">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="d9749-281">Création de deux **services liés**:</span><span class="sxs-lookup"><span data-stu-id="d9749-281">Created two **linked services**:</span></span>
   1. <span data-ttu-id="d9749-282">**Azure Storage** pour lier à la fabrique de données votre stockage d’objets blob Azure contenant les fichiers d’entrée/sortie.</span><span class="sxs-lookup"><span data-stu-id="d9749-282">**Azure Storage** linked service to link your Azure blob storage that holds input/output files to the data factory.</span></span>
   2. <span data-ttu-id="d9749-283">**Azure HDInsight** à la demande pour lier à la fabrique de données un cluster Hadoop HDInsight à la demande.</span><span class="sxs-lookup"><span data-stu-id="d9749-283">**Azure HDInsight** on-demand linked service to link an on-demand HDInsight Hadoop cluster to the data factory.</span></span> <span data-ttu-id="d9749-284">Azure Data Factory crée un cluster Hadoop HDInsight juste-à-temps pour traiter les données d’entrée et produire des données de sortie.</span><span class="sxs-lookup"><span data-stu-id="d9749-284">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time to process input data and produce output data.</span></span>
3. <span data-ttu-id="d9749-285">Création de deux **jeux de données**qui décrivent les données d’entrée et de sortie pour l’activité HDInsight Hive dans le pipeline.</span><span class="sxs-lookup"><span data-stu-id="d9749-285">Created two **datasets**, which describe input and output data for HDInsight Hive activity in the pipeline.</span></span>
4. <span data-ttu-id="d9749-286">Création d’un **pipeline** avec une activité **Hive HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="d9749-286">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9749-287">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d9749-287">Next steps</span></span>
<span data-ttu-id="d9749-288">Dans cet article, vous avez créé un pipeline avec une activité de transformation (Activité HDInsight) qui exécute un script Hive sur un cluster Azure HDInsight à la demande.</span><span class="sxs-lookup"><span data-stu-id="d9749-288">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="d9749-289">Pour voir comment utiliser une activité de copie pour copier des données depuis un objet blob Azure vers Azure SQL, consultez le [Didacticiel : copie de données depuis un objet blob Azure vers Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="d9749-289">To see how to use a Copy Activity to copy data from an Azure Blob to Azure SQL, see [Tutorial: Copy data from an Azure Blob to Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="d9749-290">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="d9749-290">See Also</span></span>
| <span data-ttu-id="d9749-291">Rubrique</span><span class="sxs-lookup"><span data-stu-id="d9749-291">Topic</span></span> | <span data-ttu-id="d9749-292">Description</span><span class="sxs-lookup"><span data-stu-id="d9749-292">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="d9749-293">Informations de référence sur les applets de commande de Data Factory</span><span class="sxs-lookup"><span data-stu-id="d9749-293">Data Factory Cmdlet Reference</span></span>](/powershell/module/azurerm.datafactories) |<span data-ttu-id="d9749-294">Consultez la documentation complète sur les applets de commande de Data Factory</span><span class="sxs-lookup"><span data-stu-id="d9749-294">See comprehensive documentation on Data Factory cmdlets</span></span> |
| [<span data-ttu-id="d9749-295">Pipelines</span><span class="sxs-lookup"><span data-stu-id="d9749-295">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="d9749-296">Cet article vous aide à comprendre les pipelines et les activités dans Azure Data Factory, et à les utiliser dans l’optique de créer des workflows pilotés par les données de bout en bout pour votre scénario ou votre entreprise.</span><span class="sxs-lookup"><span data-stu-id="d9749-296">This article helps you understand pipelines and activities in Azure Data Factory and how to use them to construct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="d9749-297">Groupes de données</span><span class="sxs-lookup"><span data-stu-id="d9749-297">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="d9749-298">Cet article vous aide à comprendre les jeux de données dans Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d9749-298">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="d9749-299">Planification et exécution</span><span class="sxs-lookup"><span data-stu-id="d9749-299">Scheduling and Execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="d9749-300">Cet article explique les aspects de la planification et de l’exécution du modèle d’application Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d9749-300">This article explains the scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="d9749-301">Surveiller et gérer les pipelines Azure Data Factory à l’aide de la nouvelle application de surveillance et gestion.</span><span class="sxs-lookup"><span data-stu-id="d9749-301">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="d9749-302">Cet article décrit comment surveiller, gérer et déboguer les pipelines à l’aide de l’application de surveillance et gestion.</span><span class="sxs-lookup"><span data-stu-id="d9749-302">This article describes how to monitor, manage, and debug pipelines using the Monitoring & Management App.</span></span> |
