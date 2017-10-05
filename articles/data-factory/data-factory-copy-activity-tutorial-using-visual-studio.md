---
title: "Didacticiel : Créer un pipeline avec l’activité de copie à l’aide de Visual Studio | Microsoft Docs"
description: "Dans ce didacticiel, vous allez créer un pipeline Azure Data Factory avec une activité de copie à l’aide de Visual Studio."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1751185b-ce0a-4ab2-a9c3-e37b4d149ca3
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: f90b158e45a3679210685765b23c8299eb76ed50
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-visual-studio"></a><span data-ttu-id="3f063-103">Didacticiel : Créer un pipeline avec l'activité de copie à l'aide de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3f063-103">Tutorial: Create a pipeline with Copy Activity using Visual Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3f063-104">Vue d’ensemble et étapes préalables requises</span><span class="sxs-lookup"><span data-stu-id="3f063-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="3f063-105">Assistant de copie</span><span class="sxs-lookup"><span data-stu-id="3f063-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="3f063-106">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="3f063-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="3f063-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3f063-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="3f063-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3f063-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="3f063-109">Modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3f063-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="3f063-110">API REST</span><span class="sxs-lookup"><span data-stu-id="3f063-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="3f063-111">API .NET</span><span class="sxs-lookup"><span data-stu-id="3f063-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="3f063-112">Dans cet article, vous allez apprendre à utiliser Microsoft Visual Studio pour créer une fabrique de données avec un pipeline qui copie les données d’un stockage Blob Azure dans une base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="3f063-112">In this article, you learn how to use the Microsoft Visual Studio to create a data factory with a pipeline that copies data from an Azure blob storage to an Azure SQL database.</span></span> <span data-ttu-id="3f063-113">Si vous débutez avec Azure Data Factory, lisez l’article [Présentation d’Azure Data Factory](data-factory-introduction.md) avant de suivre ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="3f063-113">If you are new to Azure Data Factory, read through the [Introduction to Azure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="3f063-114">Dans ce didacticiel, vous créez un pipeline avec une activité : activité de copie.</span><span class="sxs-lookup"><span data-stu-id="3f063-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="3f063-115">L’activité de copie copie les données d’un magasin de données pris en charge vers un magasin de données de récepteur pris en charge.</span><span class="sxs-lookup"><span data-stu-id="3f063-115">The copy activity copies data from a supported data store to a supported sink data store.</span></span> <span data-ttu-id="3f063-116">Pour obtenir la liste des magasins de données pris en charge en tant que sources et récepteurs, consultez [Magasins de données pris en charge](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="3f063-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="3f063-117">Elle est mise en œuvre par un service disponible dans le monde entier, capable de copier des données entre différents magasins de données de façon sécurisée, fiable et évolutive.</span><span class="sxs-lookup"><span data-stu-id="3f063-117">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="3f063-118">Pour plus d’informations sur l’activité de copie, consultez [Activités de déplacement des données](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="3f063-118">For more information about the Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="3f063-119">Un pipeline peut contenir plusieurs activités.</span><span class="sxs-lookup"><span data-stu-id="3f063-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="3f063-120">En outre, vous pouvez chaîner deux activités (une après l’autre) en configurant le jeu de données de sortie d’une activité en tant que jeu de données d’entrée de l’autre activité.</span><span class="sxs-lookup"><span data-stu-id="3f063-120">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="3f063-121">Pour plus d’informations, consultez [Plusieurs activités dans un pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="3f063-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

> [!NOTE] 
> <span data-ttu-id="3f063-122">Dans ce didacticiel, le pipeline de données copie les données d’un magasin de données source vers un magasin de données de destination.</span><span class="sxs-lookup"><span data-stu-id="3f063-122">The data pipeline in this tutorial copies data from a source data store to a destination data store.</span></span> <span data-ttu-id="3f063-123">Pour un didacticiel sur la transformation des données à l’aide d’Azure Data Factory, consultez [Tutorial: Build your first pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md) (Didacticiel : Créer un pipeline pour transformer des données à l’aide d’un cluster Hadoop).</span><span class="sxs-lookup"><span data-stu-id="3f063-123">For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3f063-124">Composants requis</span><span class="sxs-lookup"><span data-stu-id="3f063-124">Prerequisites</span></span>
1. <span data-ttu-id="3f063-125">Lisez l’article [Vue d’ensemble du didacticiel](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) et effectuez les **étapes préalables requises** .</span><span class="sxs-lookup"><span data-stu-id="3f063-125">Read through [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article and complete the **prerequisite** steps.</span></span>       
2. <span data-ttu-id="3f063-126">Pour créer des instances Data Factory, vous devez avoir un rôle de [collaborateur de fabrique de données](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) au niveau de l’abonnement/du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="3f063-126">To create Data Factory instances, you must be a member of the [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at the subscription/resource group level.</span></span>
3. <span data-ttu-id="3f063-127">Les composants suivants doivent être installés sur votre ordinateur :</span><span class="sxs-lookup"><span data-stu-id="3f063-127">You must have the following installed on your computer:</span></span> 
   * <span data-ttu-id="3f063-128">Visual Studio 2013 ou Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="3f063-128">Visual Studio 2013 or Visual Studio 2015</span></span>
   * <span data-ttu-id="3f063-129">Téléchargez le Kit de développement logiciel (SDK) Azure pour Visual Studio 2013 ou Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="3f063-129">Download Azure SDK for Visual Studio 2013 or Visual Studio 2015.</span></span> <span data-ttu-id="3f063-130">Accédez à la [page de téléchargement d’Azure](https://azure.microsoft.com/downloads/), puis cliquez sur **VS 2013** ou **VS 2015** dans la section **.NET**.</span><span class="sxs-lookup"><span data-stu-id="3f063-130">Navigate to [Azure Download Page](https://azure.microsoft.com/downloads/) and click **VS 2013** or **VS 2015** in the **.NET** section.</span></span>
   * <span data-ttu-id="3f063-131">Téléchargez le dernier plug-in Azure Data Factory pour Visual Studio : [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) ou [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005).</span><span class="sxs-lookup"><span data-stu-id="3f063-131">Download the latest Azure Data Factory plugin for Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) or [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005).</span></span> <span data-ttu-id="3f063-132">Vous pouvez également mettre à jour le plug-in en procédant comme suit : dans le menu, cliquez sur **Outils** -> **Extensions et mises à jour** -> **En ligne** -> **Galerie Visual Studio** -> **Outils Microsoft Azure Data Factory pour Visual Studio** -> **Mettre à jour**.</span><span class="sxs-lookup"><span data-stu-id="3f063-132">You can also update the plugin by doing the following steps: On the menu, click **Tools** -> **Extensions and Updates** -> **Online** -> **Visual Studio Gallery** -> **Microsoft Azure Data Factory Tools for Visual Studio** -> **Update**.</span></span>

## <a name="steps"></a><span data-ttu-id="3f063-133">Étapes</span><span class="sxs-lookup"><span data-stu-id="3f063-133">Steps</span></span>
<span data-ttu-id="3f063-134">Voici les étapes à effectuer dans le cadre de ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="3f063-134">Here are the steps you perform as part of this tutorial:</span></span>

1. <span data-ttu-id="3f063-135">Créez des **services liés** dans la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="3f063-135">Create **linked services** in the data factory.</span></span> <span data-ttu-id="3f063-136">Au cours de cette étape, vous allez créer deux services liés de types : Stockage Azure et base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="3f063-136">In this step, you create two linked services of types: Azure Storage and Azure SQL Database.</span></span> 
    
    <span data-ttu-id="3f063-137">AzureStorageLinkedService relie votre compte de stockage Azure à la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="3f063-137">The AzureStorageLinkedService links your Azure storage account to the data factory.</span></span> <span data-ttu-id="3f063-138">Vous avez créé un conteneur et chargé des données dans ce compte de stockage en remplissant les [conditions préalables](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="3f063-138">You created a container and uploaded data to this storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

    <span data-ttu-id="3f063-139">AzureSqlLinkedService lie votre base de données SQL Azure à la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="3f063-139">AzureSqlLinkedService links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="3f063-140">Les données copiées à partir du stockage Blob sont stockées dans cette base de données.</span><span class="sxs-lookup"><span data-stu-id="3f063-140">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="3f063-141">Vous avez créé une table SQL dans cette base de données en remplissant les [conditions préalables](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="3f063-141">You created a SQL table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>     
2. <span data-ttu-id="3f063-142">Créez des **jeux de données** d’entrée et de sortie dans la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="3f063-142">Create input and output **datasets** in the data factory.</span></span>  
    
    <span data-ttu-id="3f063-143">Le service lié Stockage Azure spécifie la chaîne de connexion que le service Data Factory utilise au moment de l’exécution pour se connecter à votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="3f063-143">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="3f063-144">Le jeu de données blob d’entrée spécifie quant à lui le conteneur et le dossier qui contient les données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="3f063-144">And, the input blob dataset specifies the container and the folder that contains the input data.</span></span>  

    <span data-ttu-id="3f063-145">De même, le service lié Azure SQL Database spécifie la chaîne de connexion que le service Data Factory utilise au moment de l’exécution pour se connecter à votre base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="3f063-145">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="3f063-146">Et le jeu de données de la table SQL de sortie spécifie la table de la base de données dans laquelle les données du stockage Blob sont copiées.</span><span class="sxs-lookup"><span data-stu-id="3f063-146">And, the output SQL table dataset specifies the table in the database to which the data from the blob storage is copied.</span></span>
3. <span data-ttu-id="3f063-147">Créez un **pipeline** dans la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="3f063-147">Create a **pipeline** in the data factory.</span></span> <span data-ttu-id="3f063-148">Dans cette étape, vous allez créer un pipeline avec une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="3f063-148">In this step, you create a pipeline with a copy activity.</span></span>   
    
    <span data-ttu-id="3f063-149">Cette activité copie les données d’un objet blob du stockage Blob Azure dans une table de la base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="3f063-149">The copy activity copies data from a blob in the Azure blob storage to a table in the Azure SQL database.</span></span> <span data-ttu-id="3f063-150">Vous pouvez utiliser une activité de copie dans un pipeline pour copier les données d’une source prise en charge dans une destination prise en charge.</span><span class="sxs-lookup"><span data-stu-id="3f063-150">You can use a copy activity in a pipeline to copy data from any supported source to any supported destination.</span></span> <span data-ttu-id="3f063-151">Pour obtenir la liste des magasins de données pris en charge, consultez [Activités de déplacement des données](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="3f063-151">For a list of supported data stores, see [data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> 
4. <span data-ttu-id="3f063-152">Créez une **fabrique de données** Azure lors du déploiement des entités Data Factory (services liés, jeux de données/tables et pipelines).</span><span class="sxs-lookup"><span data-stu-id="3f063-152">Create an Azure **data factory** when deploying Data Factory entities (linked services, datasets/tables, and pipelines).</span></span> 

## <a name="create-visual-studio-project"></a><span data-ttu-id="3f063-153">Création d’un projet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3f063-153">Create Visual Studio project</span></span>
1. <span data-ttu-id="3f063-154">Lancez **Visual Studio 2015**.</span><span class="sxs-lookup"><span data-stu-id="3f063-154">Launch **Visual Studio 2015**.</span></span> <span data-ttu-id="3f063-155">Cliquez sur **Fichier**, pointez le curseur de la souris sur **Nouveau**, puis cliquez sur **Projet**.</span><span class="sxs-lookup"><span data-stu-id="3f063-155">Click **File**, point to **New**, and click **Project**.</span></span> <span data-ttu-id="3f063-156">La boîte de dialogue **Nouveau projet** doit s’afficher.</span><span class="sxs-lookup"><span data-stu-id="3f063-156">You should see the **New Project** dialog box.</span></span>  
2. <span data-ttu-id="3f063-157">Dans la boîte de dialogue **Nouveau projet**, sélectionnez le modèle **DataFactory**, puis cliquez sur **Projet Data Factory vide**.</span><span class="sxs-lookup"><span data-stu-id="3f063-157">In the **New Project** dialog, select the **DataFactory** template, and click **Empty Data Factory Project**.</span></span>  
   
    ![Boîte de dialogue Nouveau projet](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-project-dialog.png)
3. <span data-ttu-id="3f063-159">Spécifiez le nom du projet, l’emplacement de la solution et le nom de la solution, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="3f063-159">Specify the name of the project, location for the solution, and name of the solution, and then click **OK**.</span></span>
   
    ![Explorateur de solutions](./media/data-factory-copy-activity-tutorial-using-visual-studio/solution-explorer.png)    

## <a name="create-linked-services"></a><span data-ttu-id="3f063-161">Créer des services liés</span><span class="sxs-lookup"><span data-stu-id="3f063-161">Create linked services</span></span>
<span data-ttu-id="3f063-162">Vous allez créer des services liés dans une fabrique de données pour lier vos magasins de données et vos services de calcul à la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="3f063-162">You create linked services in a data factory to link your data stores and compute services to the data factory.</span></span> <span data-ttu-id="3f063-163">Dans ce didacticiel, vous n’allez pas utiliser n’importe quel service de calcul comme Azure HDInsight ou Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="3f063-163">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="3f063-164">Vous allez utiliser deux magasins de données de type Stockage Azure (source) et Base de données SQL Azure (destination).</span><span class="sxs-lookup"><span data-stu-id="3f063-164">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

<span data-ttu-id="3f063-165">Vous allez donc créer deux services liés de types : AzureStorage et AzureSqlDatabase.</span><span class="sxs-lookup"><span data-stu-id="3f063-165">Therefore, you create two linked services of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="3f063-166">Le service lié Stockage Azure relie votre compte de stockage Azure à la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="3f063-166">The Azure Storage linked service links your Azure storage account to the data factory.</span></span> <span data-ttu-id="3f063-167">Ce compte de stockage est celui dans lequel vous avez créé un conteneur et chargé les données en remplissant les [conditions préalables](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="3f063-167">This storage account is the one in which you created a container and uploaded the data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="3f063-168">Le service lié Azure SQL lie votre base de données SQL Azure à la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="3f063-168">Azure SQL linked service links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="3f063-169">Les données copiées à partir du stockage Blob sont stockées dans cette base de données.</span><span class="sxs-lookup"><span data-stu-id="3f063-169">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="3f063-170">Vous avez créé une table emp dans cette base de données en remplissant les [conditions préalables](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="3f063-170">You created the emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

<span data-ttu-id="3f063-171">Les services liés se chargent de lier des magasins de données ou des services de calcul à une fabrique de données Azure.</span><span class="sxs-lookup"><span data-stu-id="3f063-171">Linked services link data stores or compute services to an Azure data factory.</span></span> <span data-ttu-id="3f063-172">Pour connaître l’ensemble des sources et des récepteurs pris en charge par l’activité de copie, consultez [Banques de données et formats pris en charge](data-factory-data-movement-activities.md#supported-data-stores-and-formats) .</span><span class="sxs-lookup"><span data-stu-id="3f063-172">See [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for all the sources and sinks supported by the Copy Activity.</span></span> <span data-ttu-id="3f063-173">Pour obtenir la liste des services de calcul pris en charge par Data Factory, consultez [Services liés de calcul](data-factory-compute-linked-services.md) .</span><span class="sxs-lookup"><span data-stu-id="3f063-173">See [compute linked services](data-factory-compute-linked-services.md) for the list of compute services supported by Data Factory.</span></span> <span data-ttu-id="3f063-174">Dans ce didacticiel, aucun service de calcul n’est utilisé.</span><span class="sxs-lookup"><span data-stu-id="3f063-174">In this tutorial, you do not use any compute service.</span></span> 

### <a name="create-the-azure-storage-linked-service"></a><span data-ttu-id="3f063-175">Créer le service lié Azure Storage</span><span class="sxs-lookup"><span data-stu-id="3f063-175">Create the Azure Storage linked service</span></span>
1. <span data-ttu-id="3f063-176">Dans **l’Explorateur de solutions**, cliquez avec le bouton droit sur **Services liés**, pointez sur **Ajouter** puis cliquez sur **Nouvel élément**.</span><span class="sxs-lookup"><span data-stu-id="3f063-176">In **Solution Explorer**, right-click **Linked Services**, point to **Add**, and click **New Item**.</span></span>      
2. <span data-ttu-id="3f063-177">Dans la boîte de dialogue **Ajouter un nouvel élément**, sélectionnez **Service lié Azure Storage** dans la liste, puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="3f063-177">In the **Add New Item** dialog box, select **Azure Storage Linked Service** from the list, and click **Add**.</span></span> 
   
    ![Nouveau service lié](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-linked-service-dialog.png)
3. <span data-ttu-id="3f063-179">Remplacez `<accountname>` et `<accountkey>` par le nom de votre compte de stockage Azure et par sa clé.</span><span class="sxs-lookup"><span data-stu-id="3f063-179">Replace `<accountname>` and `<accountkey>`* with the name of your Azure storage account and its key.</span></span> 
   
    ![Service lié Azure Storage](./media/data-factory-copy-activity-tutorial-using-visual-studio/azure-storage-linked-service.png)
4. <span data-ttu-id="3f063-181">Enregistrez le fichier **AzureStorageLinkedService1.json** .</span><span class="sxs-lookup"><span data-stu-id="3f063-181">Save the **AzureStorageLinkedService1.json** file.</span></span>

    <span data-ttu-id="3f063-182">Pour plus d’informations sur les propriétés JSON dans la définition de service lié, consultez l’article [Azure Blob Storage connector)](data-factory-azure-blob-connector.md#linked-service-properties) (Connecteur de stockage Blob Azure).</span><span class="sxs-lookup"><span data-stu-id="3f063-182">For more information about JSON properties in the linked service definition, see [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) article.</span></span>

### <a name="create-the-azure-sql-linked-service"></a><span data-ttu-id="3f063-183">Créer le service lié SQL Azure</span><span class="sxs-lookup"><span data-stu-id="3f063-183">Create the Azure SQL linked service</span></span>
1. <span data-ttu-id="3f063-184">Cliquez de nouveau avec le bouton droit sur le nœud **Services liés** dans l’**Explorateur de solutions**, pointez sur **Ajouter**, puis cliquez sur **Nouvel élément**.</span><span class="sxs-lookup"><span data-stu-id="3f063-184">Right-click on **Linked Services** node in the **Solution Explorer** again, point to **Add**, and click **New Item**.</span></span> 
2. <span data-ttu-id="3f063-185">Cette fois, sélectionnez **Service lié SQL Azure**, puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="3f063-185">This time, select **Azure SQL Linked Service**, and click **Add**.</span></span> 
3. <span data-ttu-id="3f063-186">Dans le **fichier AzureSqlLinkedService1.json**, remplacez `<servername>`, `<databasename>`, `<username@servername>` et `<password>` par le nom du compte d’utilisateur, de la base de données et de votre serveur SQL Azure, et par le mot de passe associé.</span><span class="sxs-lookup"><span data-stu-id="3f063-186">In the **AzureSqlLinkedService1.json file**, replace `<servername>`, `<databasename>`, `<username@servername>`, and `<password>` with names of your Azure SQL server, database, user account, and password.</span></span>    
4. <span data-ttu-id="3f063-187">Enregistrez le fichier **AzureSqlLinkedService1.json** .</span><span class="sxs-lookup"><span data-stu-id="3f063-187">Save the **AzureSqlLinkedService1.json** file.</span></span> 
    
    <span data-ttu-id="3f063-188">Pour plus d’informations sur ces propriétés JSON, consultez [Azure SQL Database connector](data-factory-azure-sql-connector.md#linked-service-properties) (Connecteur de base de données SQL Azure).</span><span class="sxs-lookup"><span data-stu-id="3f063-188">For more information about these JSON properties, see [Azure SQL Database connector](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>


## <a name="create-datasets"></a><span data-ttu-id="3f063-189">Créer des jeux de données</span><span class="sxs-lookup"><span data-stu-id="3f063-189">Create datasets</span></span>
<span data-ttu-id="3f063-190">Dans l’étape précédente, vous avez créé des services pour lier votre compte de stockage Azure et une base de données SQL Azure à votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="3f063-190">In the previous step, you created linked services to link your Azure Storage account and Azure SQL database to your data factory.</span></span> <span data-ttu-id="3f063-191">Dans cette étape, vous définissez deux jeux de données nommés InputDataset et OutputDataset, qui représentent les données d’entrée/sortie stockées dans les banques de données référencées par AzureStorageLinkedService1 et AzureSqlLinkedService1, respectivement.</span><span class="sxs-lookup"><span data-stu-id="3f063-191">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in the data stores referred by AzureStorageLinkedService1 and AzureSqlLinkedService1 respectively.</span></span>

<span data-ttu-id="3f063-192">Le service lié Azure Storage spécifie la chaîne de connexion que le service Data Factory utilise au moment de l’exécution pour se connecter à votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="3f063-192">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="3f063-193">Le jeu de données blob d’entrée (InputDataset) spécifie quant à lui le conteneur et le dossier qui contient les données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="3f063-193">And, the input blob dataset (InputDataset) specifies the container and the folder that contains the input data.</span></span>  

<span data-ttu-id="3f063-194">De même, le service lié Azure SQL Database spécifie la chaîne de connexion que le service Data Factory utilise au moment de l’exécution pour se connecter à votre base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="3f063-194">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="3f063-195">Et le jeu de données de la table SQL de sortie (OututDataset) spécifie la table de la base de données dans laquelle les données du stockage Blob sont copiées.</span><span class="sxs-lookup"><span data-stu-id="3f063-195">And, the output SQL table dataset (OututDataset) specifies the table in the database to which the data from the blob storage is copied.</span></span> 

### <a name="create-input-dataset"></a><span data-ttu-id="3f063-196">Créer le jeu de données d’entrée</span><span class="sxs-lookup"><span data-stu-id="3f063-196">Create input dataset</span></span>
<span data-ttu-id="3f063-197">Dans cette étape, vous créez un jeu de données nommé InputDataset qui pointe vers un fichier blob (emp.txt) dans le dossier racine d’un conteneur d’objets blob (adftutorial) du stockage Azure représenté par le service lié AzureStorageLinkedService1.</span><span class="sxs-lookup"><span data-stu-id="3f063-197">In this step, you create a dataset named InputDataset that points to a blob file (emp.txt) in the root folder of a blob container (adftutorial) in the Azure Storage represented by the AzureStorageLinkedService1 linked service.</span></span> <span data-ttu-id="3f063-198">Si vous ne spécifiez de valeur pour fileName (ou si vous ignorez ce paramètre), les données de tous les objets blob du dossier d’entrée sont copiées dans la destination.</span><span class="sxs-lookup"><span data-stu-id="3f063-198">If you don't specify a value for the fileName (or skip it), data from all blobs in the input folder are copied to the destination.</span></span> <span data-ttu-id="3f063-199">Dans ce didacticiel, vous spécifiez une valeur pour fileName.</span><span class="sxs-lookup"><span data-stu-id="3f063-199">In this tutorial, you specify a value for the fileName.</span></span> 

<span data-ttu-id="3f063-200">Ici, vous utilisez le terme « tables » plutôt que « jeux de données ».</span><span class="sxs-lookup"><span data-stu-id="3f063-200">Here, you use the term "tables" rather than "datasets".</span></span> <span data-ttu-id="3f063-201">Une table est un jeu de données rectangulaire. C’est le seul type de jeu de données pris en charge pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="3f063-201">A table is a rectangular dataset and is the only type of dataset supported right now.</span></span> 

1. <span data-ttu-id="3f063-202">Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur **Tables**, pointez sur **Ajouter**, puis cliquez sur **Nouvel élément**.</span><span class="sxs-lookup"><span data-stu-id="3f063-202">Right-click **Tables** in the **Solution Explorer**, point to **Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="3f063-203">Dans la boîte de dialogue **Ajouter un nouvel élément**, sélectionnez **Objet blob Azure**, puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="3f063-203">In the **Add New Item** dialog box, select **Azure Blob**, and click **Add**.</span></span>   
3. <span data-ttu-id="3f063-204">Remplacez le texte JSON par le texte suivant, puis enregistrez le fichier **AzureBlobLocation1.json** .</span><span class="sxs-lookup"><span data-stu-id="3f063-204">Replace the JSON text with the following text and save the **AzureBlobLocation1.json** file.</span></span> 

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
      "linkedServiceName": "AzureStorageLinkedService1",
      "typeProperties": {
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
    <span data-ttu-id="3f063-205">Le tableau suivant décrit les propriétés JSON utilisées dans l'extrait de code :</span><span class="sxs-lookup"><span data-stu-id="3f063-205">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

    | <span data-ttu-id="3f063-206">Propriété</span><span class="sxs-lookup"><span data-stu-id="3f063-206">Property</span></span> | <span data-ttu-id="3f063-207">Description</span><span class="sxs-lookup"><span data-stu-id="3f063-207">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="3f063-208">type</span><span class="sxs-lookup"><span data-stu-id="3f063-208">type</span></span> | <span data-ttu-id="3f063-209">La propriété du type est définie sur **AzureBlob**, car les données se trouvent dans le stockage blob Azure.</span><span class="sxs-lookup"><span data-stu-id="3f063-209">The type property is set to **AzureBlob** because data resides in an Azure blob storage.</span></span> |
    | <span data-ttu-id="3f063-210">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="3f063-210">linkedServiceName</span></span> | <span data-ttu-id="3f063-211">Fait référence au service **AzureStorageLinkedService** que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="3f063-211">Refers to the **AzureStorageLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="3f063-212">folderPath</span><span class="sxs-lookup"><span data-stu-id="3f063-212">folderPath</span></span> | <span data-ttu-id="3f063-213">Spécifie le **conteneur** d’objets blob et le **dossier** qui contient les objets blob d’entrée.</span><span class="sxs-lookup"><span data-stu-id="3f063-213">Specifies the blob **container** and the **folder** that contains input blobs.</span></span> <span data-ttu-id="3f063-214">Dans ce didacticiel, adftutorial est le conteneur d’objets blob et folder est le dossier racine.</span><span class="sxs-lookup"><span data-stu-id="3f063-214">In this tutorial, adftutorial is the blob container and folder is the root folder.</span></span> | 
    | <span data-ttu-id="3f063-215">fileName</span><span class="sxs-lookup"><span data-stu-id="3f063-215">fileName</span></span> | <span data-ttu-id="3f063-216">Cette propriété est facultative.</span><span class="sxs-lookup"><span data-stu-id="3f063-216">This property is optional.</span></span> <span data-ttu-id="3f063-217">Si vous omettez cette propriété, tous les fichiers spécifiés dans le paramètre folderPath sont récupérés.</span><span class="sxs-lookup"><span data-stu-id="3f063-217">If you omit this property, all files from the folderPath are picked.</span></span> <span data-ttu-id="3f063-218">Dans ce didacticiel, **emp.txt** est spécifié pour le paramètre fileName, si bien que seul ce fichier est récupéré pour le traitement.</span><span class="sxs-lookup"><span data-stu-id="3f063-218">In this tutorial, **emp.txt** is specified for the fileName, so only that file is picked up for processing.</span></span> |
    | <span data-ttu-id="3f063-219">format -> type</span><span class="sxs-lookup"><span data-stu-id="3f063-219">format -> type</span></span> |<span data-ttu-id="3f063-220">Le fichier d’entrée étant au format texte, nous utilisons **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="3f063-220">The input file is in the text format, so we use **TextFormat**.</span></span> |
    | <span data-ttu-id="3f063-221">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="3f063-221">columnDelimiter</span></span> | <span data-ttu-id="3f063-222">Les colonnes du fichier d’entrée sont délimitées par une **virgule (`,`)**.</span><span class="sxs-lookup"><span data-stu-id="3f063-222">The columns in the input file are delimited by **comma character (`,`)**.</span></span> |
    | <span data-ttu-id="3f063-223">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="3f063-223">frequency/interval</span></span> | <span data-ttu-id="3f063-224">La fréquence est définie sur **Heure** et l’intervalle est **1**, ce qui signifie que les segments d’entrée sont disponibles **toutes les heures**.</span><span class="sxs-lookup"><span data-stu-id="3f063-224">The frequency is set to **Hour** and interval is  set to **1**, which means that the input slices are available **hourly**.</span></span> <span data-ttu-id="3f063-225">En d’autres termes, le service Data Factory recherche les données d’entrée toutes les heures dans le dossier racine du conteneur d’objets blob (**adftutorial**) que vous avez spécifié.</span><span class="sxs-lookup"><span data-stu-id="3f063-225">In other words, the Data Factory service looks for input data every hour in the root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="3f063-226">Il recherche des données entre les heures de début et de fin du pipeline, pas avant ni après.</span><span class="sxs-lookup"><span data-stu-id="3f063-226">It looks for the data within the pipeline start and end times, not before or after these times.</span></span>  |
    | <span data-ttu-id="3f063-227">external</span><span class="sxs-lookup"><span data-stu-id="3f063-227">external</span></span> | <span data-ttu-id="3f063-228">Cette propriété a la valeur **true** si les données ne sont pas générées par ce pipeline.</span><span class="sxs-lookup"><span data-stu-id="3f063-228">This property is set to **true** if the data is not generated by this pipeline.</span></span> <span data-ttu-id="3f063-229">Dans ce didacticiel, les données d’entrée sont dans le fichier emp.txt, qui n’est pas généré par ce pipeline. Nous définissons donc cette propriété sur true.</span><span class="sxs-lookup"><span data-stu-id="3f063-229">The input data in this tutorial is in the emp.txt file, which is not generated by this pipeline, so we set this property to true.</span></span> |

    <span data-ttu-id="3f063-230">Pour plus d’informations sur ces propriétés JSON, consultez l’article [Azure Blob connector](data-factory-azure-blob-connector.md#dataset-properties) (Connecteur de stockage Blob Azure).</span><span class="sxs-lookup"><span data-stu-id="3f063-230">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>   

### <a name="create-output-dataset"></a><span data-ttu-id="3f063-231">Créer un jeu de données de sortie</span><span class="sxs-lookup"><span data-stu-id="3f063-231">Create output dataset</span></span>
<span data-ttu-id="3f063-232">Dans cette étape, vous créez un jeu de données de sortie nommé **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="3f063-232">In this step, you create an output dataset named **OutputDataset**.</span></span> <span data-ttu-id="3f063-233">Ce jeu de données pointe vers une table SQL de la base de données SQL Azure représentée par **AzureSqlLinkedService1**.</span><span class="sxs-lookup"><span data-stu-id="3f063-233">This dataset points to a SQL table in the Azure SQL database represented by **AzureSqlLinkedService1**.</span></span> 

1. <span data-ttu-id="3f063-234">Dans l’**Explorateur de solutions**, cliquez de nouveau avec le bouton droit sur **Tables**, pointez sur **Ajouter**, puis cliquez sur **Nouvel élément**.</span><span class="sxs-lookup"><span data-stu-id="3f063-234">Right-click **Tables** in the **Solution Explorer** again, point to **Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="3f063-235">Dans la boîte de dialogue **Ajouter un nouvel élément**, sélectionnez **Azure SQL**, puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="3f063-235">In the **Add New Item** dialog box, select **Azure SQL**, and click **Add**.</span></span> 
3. <span data-ttu-id="3f063-236">Remplacez le texte JSON par le texte JSON suivant, puis enregistrez le fichier **AzureSqlTableLocation1.json** .</span><span class="sxs-lookup"><span data-stu-id="3f063-236">Replace the JSON text with the following JSON and save the **AzureSqlTableLocation1.json** file.</span></span>

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
       "linkedServiceName": "AzureSqlLinkedService1",
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
    <span data-ttu-id="3f063-237">Le tableau suivant décrit les propriétés JSON utilisées dans l'extrait de code :</span><span class="sxs-lookup"><span data-stu-id="3f063-237">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

    | <span data-ttu-id="3f063-238">Propriété</span><span class="sxs-lookup"><span data-stu-id="3f063-238">Property</span></span> | <span data-ttu-id="3f063-239">Description</span><span class="sxs-lookup"><span data-stu-id="3f063-239">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="3f063-240">type</span><span class="sxs-lookup"><span data-stu-id="3f063-240">type</span></span> | <span data-ttu-id="3f063-241">La propriété du type est définie sur **AzureSqlTable** car les données sont copiées dans une table de la base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="3f063-241">The type property is set to **AzureSqlTable** because data is copied to a table in an Azure SQL database.</span></span> |
    | <span data-ttu-id="3f063-242">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="3f063-242">linkedServiceName</span></span> | <span data-ttu-id="3f063-243">Fait référence au service **AzureSqlLinkedService** que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="3f063-243">Refers to the **AzureSqlLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="3f063-244">TableName</span><span class="sxs-lookup"><span data-stu-id="3f063-244">tableName</span></span> | <span data-ttu-id="3f063-245">Spécifie la **table** dans laquelle les données sont copiées.</span><span class="sxs-lookup"><span data-stu-id="3f063-245">Specified the **table** to which the data is copied.</span></span> | 
    | <span data-ttu-id="3f063-246">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="3f063-246">frequency/interval</span></span> | <span data-ttu-id="3f063-247">La fréquence est définie sur **Heure** et l’intervalle sur **1**, ce qui signifie que les tranches de sortie sont produites **toutes les heures** entre les heures de début et de fin du pipeline, pas avant ni après.</span><span class="sxs-lookup"><span data-stu-id="3f063-247">The frequency is set to **Hour** and interval is **1**, which means that the output slices are produced **hourly** between the pipeline start and end times, not before or after these times.</span></span>  |

    <span data-ttu-id="3f063-248">La table emp de la base de données contient trois colonnes : **ID**, **FirstName** et **LastName**.</span><span class="sxs-lookup"><span data-stu-id="3f063-248">There are three columns – **ID**, **FirstName**, and **LastName** – in the emp table in the database.</span></span> <span data-ttu-id="3f063-249">ID étant une colonne d’identité, il vous suffit de spécifier **FirstName** et **LastName**.</span><span class="sxs-lookup"><span data-stu-id="3f063-249">ID is an identity column, so you need to specify only **FirstName** and **LastName** here.</span></span>

    <span data-ttu-id="3f063-250">Pour plus d’informations sur ces propriétés JSON, consultez l’article [Azure SQL connector](data-factory-azure-sql-connector.md#dataset-properties) (Connecteur SQL Azure).</span><span class="sxs-lookup"><span data-stu-id="3f063-250">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>

## <a name="create-pipeline"></a><span data-ttu-id="3f063-251">Création d’un pipeline</span><span class="sxs-lookup"><span data-stu-id="3f063-251">Create pipeline</span></span>
<span data-ttu-id="3f063-252">Dans cette étape, vous créez un pipeline avec une **activité de copie** qui utilise **InputDataset** en entrée et **OutputDataset** en sortie.</span><span class="sxs-lookup"><span data-stu-id="3f063-252">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

<span data-ttu-id="3f063-253">Le jeu de données de sortie pilote actuellement la planification.</span><span class="sxs-lookup"><span data-stu-id="3f063-253">Currently, output dataset is what drives the schedule.</span></span> <span data-ttu-id="3f063-254">Dans ce didacticiel, le jeu de données de sortie est configuré pour produire une tranche par heure.</span><span class="sxs-lookup"><span data-stu-id="3f063-254">In this tutorial, output dataset is configured to produce a slice once an hour.</span></span> <span data-ttu-id="3f063-255">Les heures de début et de fin du pipeline sont distantes d’une journée, soit 24 heures.</span><span class="sxs-lookup"><span data-stu-id="3f063-255">The pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="3f063-256">Par conséquent, 24 tranches de jeu de données de sortie sont générées par le pipeline.</span><span class="sxs-lookup"><span data-stu-id="3f063-256">Therefore, 24 slices of output dataset are produced by the pipeline.</span></span> 

1. <span data-ttu-id="3f063-257">Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur **Pipelines**, pointez sur **Ajouter**, puis cliquez sur **Nouvel élément**.</span><span class="sxs-lookup"><span data-stu-id="3f063-257">Right-click **Pipelines** in the **Solution Explorer**, point to **Add**, and click **New Item**.</span></span>  
2. <span data-ttu-id="3f063-258">Sélectionnez **Pipeline de copie de données** dans la boîte de dialogue **Ajouter un nouvel élément**, puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="3f063-258">Select **Copy Data Pipeline** in the **Add New Item** dialog box and click **Add**.</span></span> 
3. <span data-ttu-id="3f063-259">Remplacez le texte JSON par le texte JSON suivant, puis enregistrez le fichier **CopyActivity1.json** .</span><span class="sxs-lookup"><span data-stu-id="3f063-259">Replace the JSON with the following JSON and save the **CopyActivity1.json** file.</span></span>

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
             "style": "StartOfInterval",
             "retry": 0,
             "timeout": "01:00:00"
           }
         }
       ],
       "start": "2017-05-11T00:00:00Z",
       "end": "2017-05-12T00:00:00Z",
       "isPaused": false
     }
    }
    ```   
    - <span data-ttu-id="3f063-260">Dans la section des activités, il existe une seule activité dont le **type** a la valeur **Copy**.</span><span class="sxs-lookup"><span data-stu-id="3f063-260">In the activities section, there is only one activity whose **type** is set to **Copy**.</span></span> <span data-ttu-id="3f063-261">Pour plus d’informations sur l’activité de copie, consultez [Activités de déplacement des données](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="3f063-261">For more information about the copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="3f063-262">Dans les solutions Data Factory, vous pouvez également utiliser [Activités de transformation des données](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="3f063-262">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="3f063-263">L’entrée de l’activité est définie sur **InputDataset** et sa sortie, sur **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="3f063-263">Input for the activity is set to **InputDataset** and output for the activity is set to **OutputDataset**.</span></span> 
    - <span data-ttu-id="3f063-264">Dans la section **typeProperties**, **BlobSource** est spécifié en tant que type de source et **SqlSink**, en tant que type de récepteur.</span><span class="sxs-lookup"><span data-stu-id="3f063-264">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span></span> <span data-ttu-id="3f063-265">Pour obtenir la liste des magasins de données pris en charge en tant que sources et récepteurs pour l’activité de copie, consultez [Magasins de données pris en charge](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="3f063-265">For a complete list of data stores supported by the copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="3f063-266">Pour apprendre à utiliser un magasin de données pris en charge spécifique en tant que source/récepteur, cliquez sur le lien dans le tableau.</span><span class="sxs-lookup"><span data-stu-id="3f063-266">To learn how to use a specific supported data store as a source/sink, click the link in the table.</span></span>  
     
    <span data-ttu-id="3f063-267">Remplacez la valeur de la propriété **start** par le jour actuel et la valeur **end** par le jour suivant.</span><span class="sxs-lookup"><span data-stu-id="3f063-267">Replace the value of the **start** property with the current day and **end** value with the next day.</span></span> <span data-ttu-id="3f063-268">Si vous le souhaitez, spécifiez uniquement la date et ignorez l'heure.</span><span class="sxs-lookup"><span data-stu-id="3f063-268">You can specify only the date part and skip the time part of the date time.</span></span> <span data-ttu-id="3f063-269">Par exemple, « 2016-02-03 », qui équivaut à « 2016-02-03T00:00:00Z ».</span><span class="sxs-lookup"><span data-stu-id="3f063-269">For example, "2016-02-03", which is equivalent to "2016-02-03T00:00:00Z"</span></span>
     
    <span data-ttu-id="3f063-270">Les dates/heures de début et de fin doivent toutes deux être au [format ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="3f063-270">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="3f063-271">Par exemple : 2016-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="3f063-271">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="3f063-272">L’heure de fin ( **end** ) est facultative, mais nous allons l’utiliser dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="3f063-272">The **end** time is optional, but we use it in this tutorial.</span></span> 
     
    <span data-ttu-id="3f063-273">Si vous ne spécifiez aucune valeur pour la propriété **end**, cette dernière est calculée comme suit : « **start + 48 heures** ».</span><span class="sxs-lookup"><span data-stu-id="3f063-273">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="3f063-274">Pour exécuter le pipeline indéfiniment, spécifiez **9999-09-09** comme valeur pour la propriété **end**.</span><span class="sxs-lookup"><span data-stu-id="3f063-274">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span></span>
     
    <span data-ttu-id="3f063-275">Dans l’exemple ci-dessus, il existe 24 tranches de données, car une tranche de données est générée toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="3f063-275">In the preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

    <span data-ttu-id="3f063-276">Pour obtenir une description des propriétés JSON dans une définition de pipeline, consultez l’article [Créer des pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="3f063-276">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="3f063-277">Pour obtenir une description des propriétés JSON dans une définition d’activité de copie, consultez [Activités de déplacement des données](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="3f063-277">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="3f063-278">Pour obtenir une description des propriétés JSON prises en charge par BlobSource, consultez l’article [Connecteur de stockage Blob Azure](data-factory-azure-blob-connector.md).</span><span class="sxs-lookup"><span data-stu-id="3f063-278">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="3f063-279">Pour obtenir une description des propriétés JSON prises en charge par SqlSink, consultez l’article [Azure SQL Database connector](data-factory-azure-sql-connector.md) (Connecteur de base de données SQL Azure).</span><span class="sxs-lookup"><span data-stu-id="3f063-279">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>

## <a name="publishdeploy-data-factory-entities"></a><span data-ttu-id="3f063-280">Publier/déployer des entités Data Factory</span><span class="sxs-lookup"><span data-stu-id="3f063-280">Publish/deploy Data Factory entities</span></span>
<span data-ttu-id="3f063-281">Dans cette étape, vous publiez les entités Data Factory (services liés, jeux de données et pipeline) que vous avez créées précédemment.</span><span class="sxs-lookup"><span data-stu-id="3f063-281">In this step, you publish Data Factory entities (linked services, datasets, and pipeline) you created earlier.</span></span> <span data-ttu-id="3f063-282">Vous spécifiez également le nom de la fabrique de données à créer pour contenir ces entités.</span><span class="sxs-lookup"><span data-stu-id="3f063-282">You also specify the name of the new data factory to be created to hold these entities.</span></span>  

1. <span data-ttu-id="3f063-283">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur le projet, puis cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="3f063-283">Right-click project in the Solution Explorer, and click **Publish**.</span></span> 
2. <span data-ttu-id="3f063-284">Si la boîte de dialogue **Connectez-vous à votre compte Microsoft** s’affiche, saisissez vos informations d’identification pour le compte associé à l’abonnement Azure, puis cliquez sur **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="3f063-284">If you see **Sign in to your Microsoft account** dialog box, enter your credentials for the account that has Azure subscription, and click **sign in**.</span></span>
3. <span data-ttu-id="3f063-285">La boîte de dialogue suivante doit s’afficher :</span><span class="sxs-lookup"><span data-stu-id="3f063-285">You should see the following dialog box:</span></span>
   
   ![Boîte de dialogue Publier](./media/data-factory-copy-activity-tutorial-using-visual-studio/publish.png)
4. <span data-ttu-id="3f063-287">Dans la page Configurer une fabrique de données, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="3f063-287">In the Configure data factory page, do the following steps:</span></span> 
   
   1. <span data-ttu-id="3f063-288">Sélectionnez l'option **Créer une fabrique de données** .</span><span class="sxs-lookup"><span data-stu-id="3f063-288">select **Create New Data Factory** option.</span></span>
   2. <span data-ttu-id="3f063-289">Saisissez **VSTutorialFactory** dans le champ **Nom**.</span><span class="sxs-lookup"><span data-stu-id="3f063-289">Enter **VSTutorialFactory** for **Name**.</span></span>  
      
      > [!IMPORTANT]
      > <span data-ttu-id="3f063-290">Le nom de la fabrique de données Azure doit être un nom global unique.</span><span class="sxs-lookup"><span data-stu-id="3f063-290">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="3f063-291">Si vous obtenez une erreur concernant le nom de la fabrique de données pendant la publication, modifiez ce nom (par exemple, votrenomVSTutorialFactory) et relancez la publication.</span><span class="sxs-lookup"><span data-stu-id="3f063-291">If you receive an error about the name of data factory when publishing, change the name of the data factory (for example, yournameVSTutorialFactory) and try publishing again.</span></span> <span data-ttu-id="3f063-292">Consultez la rubrique [Data Factory - Règles d'affectation des noms](data-factory-naming-rules.md) pour savoir comment nommer les artefacts Data Factory.</span><span class="sxs-lookup"><span data-stu-id="3f063-292">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>        
      > 
      > 
   3. <span data-ttu-id="3f063-293">Sélectionnez votre abonnement Azure pour le champ **Abonnement** .</span><span class="sxs-lookup"><span data-stu-id="3f063-293">Select your Azure subscription for the **Subscription** field.</span></span>
      
      > [!IMPORTANT]
      > <span data-ttu-id="3f063-294">Si vous ne voyez pas les abonnements, vérifiez que vous êtes connecté à l’aide d’un compte administrateur ou coadministrateur de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="3f063-294">If you do not see any subscription, ensure that you logged in using an account that is an admin or co-admin of the subscription.</span></span>  
      > 
      > 
   4. <span data-ttu-id="3f063-295">Sélectionnez le **groupe de ressources** pour la fabrique de données à créer.</span><span class="sxs-lookup"><span data-stu-id="3f063-295">Select the **resource group** for the data factory to be created.</span></span> 
   5. <span data-ttu-id="3f063-296">Sélectionnez la **région** pour la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="3f063-296">Select the **region** for the data factory.</span></span> <span data-ttu-id="3f063-297">Seules les régions prises en charge par le service Data Factory sont affichées dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="3f063-297">Only regions supported by the Data Factory service are shown in the drop-down list.</span></span>
   6. <span data-ttu-id="3f063-298">Cliquez sur **Suivant** pour basculer vers la page **Publier des éléments**.</span><span class="sxs-lookup"><span data-stu-id="3f063-298">Click **Next** to switch to the **Publish Items** page.</span></span>
      
       ![Page Configurer une fabrique de données](media/data-factory-copy-activity-tutorial-using-visual-studio/configure-data-factory-page.png)   
5. <span data-ttu-id="3f063-300">Dans la page **Publier des éléments**, vérifiez que toutes les entités de fabriques de données sont sélectionnées, puis cliquez sur **Suivant** pour basculer vers la page **Résumé**.</span><span class="sxs-lookup"><span data-stu-id="3f063-300">In the **Publish Items** page, ensure that all the Data Factories entities are selected, and click **Next** to switch to the **Summary** page.</span></span>
   
   ![Page Publier des éléments](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-items-page.png)     
6. <span data-ttu-id="3f063-302">Passez en revue le résumé, puis cliquez sur **Suivant** pour démarrer le processus de déploiement et afficher l’**état du déploiement**.</span><span class="sxs-lookup"><span data-stu-id="3f063-302">Review the summary and click **Next** to start the deployment process and view the **Deployment Status**.</span></span>
   
   ![Page Résumé de la publication](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-summary-page.png)
7. <span data-ttu-id="3f063-304">Dans la page **État du déploiement** , vous devez voir l’état du processus de déploiement.</span><span class="sxs-lookup"><span data-stu-id="3f063-304">In the **Deployment Status** page, you should see the status of the deployment process.</span></span> <span data-ttu-id="3f063-305">Une fois le déploiement terminé, cliquez sur Terminer.</span><span class="sxs-lookup"><span data-stu-id="3f063-305">Click Finish after the deployment is done.</span></span>
 
   ![Page État du déploiement](media/data-factory-copy-activity-tutorial-using-visual-studio/deployment-status.png)

<span data-ttu-id="3f063-307">Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="3f063-307">Note the following points:</span></span> 

* <span data-ttu-id="3f063-308">Si vous recevez le message d’erreur : « L’abonnement n’est pas inscrit pour utiliser l’espace de noms Microsoft.DataFactory », effectuez l’une des opérations suivantes et essayez de relancer la publication :</span><span class="sxs-lookup"><span data-stu-id="3f063-308">If you receive the error: "This subscription is not registered to use namespace Microsoft.DataFactory", do one of the following and try publishing again:</span></span> 
  
  * <span data-ttu-id="3f063-309">Dans Azure PowerShell, exécutez la commande suivante pour enregistrer le fournisseur Data Factory.</span><span class="sxs-lookup"><span data-stu-id="3f063-309">In Azure PowerShell, run the following command to register the Data Factory provider.</span></span> 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    <span data-ttu-id="3f063-310">Vous pouvez exécuter la commande suivante pour confirmer que le fournisseur Data Factory est bien enregistré.</span><span class="sxs-lookup"><span data-stu-id="3f063-310">You can run the following command to confirm that the Data Factory provider is registered.</span></span> 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="3f063-311">Connectez-vous au [portail Azure](https://portal.azure.com) à l’aide de l’abonnement Azure et accédez à un panneau Data Factory (ou) créez une fabrique de données dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3f063-311">Login using the Azure subscription into the [Azure portal](https://portal.azure.com) and navigate to a Data Factory blade (or) create a data factory in the Azure portal.</span></span> <span data-ttu-id="3f063-312">Cette action enregistre automatiquement le fournisseur.</span><span class="sxs-lookup"><span data-stu-id="3f063-312">This action automatically registers the provider for you.</span></span>
* <span data-ttu-id="3f063-313">Le nom de la fabrique de données pourra être enregistré en tant que nom DNS et devenir ainsi visible publiquement.</span><span class="sxs-lookup"><span data-stu-id="3f063-313">The name of the data factory may be registered as a DNS name in the future and hence become publically visible.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3f063-314">Pour créer des instances Data Factory, vous devez être administrateur ou co-administrateur de l’abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="3f063-314">To create Data Factory instances, you need to be a admin/co-admin of the Azure subscription</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="3f063-315">Surveillance d’un pipeline</span><span class="sxs-lookup"><span data-stu-id="3f063-315">Monitor pipeline</span></span>
<span data-ttu-id="3f063-316">Accédez à la page d’accueil de votre fabrique de données :</span><span class="sxs-lookup"><span data-stu-id="3f063-316">Navigate to the home page for your data factory:</span></span>

1. <span data-ttu-id="3f063-317">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3f063-317">Log in to [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3f063-318">Cliquez sur **Plus de services** sur le menu de gauche, puis sur **Fabriques de données**.</span><span class="sxs-lookup"><span data-stu-id="3f063-318">Click **More services** on the left menu, and click **Data factories**.</span></span>

    ![Parcourir les fabriques de données](media/data-factory-copy-activity-tutorial-using-visual-studio/browse-data-factories.png)
3. <span data-ttu-id="3f063-320">Commencez à taper le nom de votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="3f063-320">Start typing the name of your data factory.</span></span>

    ![Nom de la fabrique de données](media/data-factory-copy-activity-tutorial-using-visual-studio/enter-data-factory-name.png) 
4. <span data-ttu-id="3f063-322">Cliquez sur votre fabrique de données dans la liste des résultats pour afficher la page d’accueil de votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="3f063-322">Click your data factory in the results list to see the home page for your data factory.</span></span>

    ![Page d'accueil Data Factory](media/data-factory-copy-activity-tutorial-using-visual-studio/data-factory-home-page.png)
5. <span data-ttu-id="3f063-324">Suivez les instructions dans [Surveiller les jeux de données et le pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) pour surveiller le pipeline et les jeux de données que vous avez créés dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="3f063-324">Follow instructions from [Monitor datasets and pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) to monitor the pipeline and datasets you have created in this tutorial.</span></span> <span data-ttu-id="3f063-325">Pour le moment, Visual Studio ne prend pas en charge la surveillance des pipelines Data Factory.</span><span class="sxs-lookup"><span data-stu-id="3f063-325">Currently, Visual Studio does not support monitoring Data Factory pipelines.</span></span> 

## <a name="summary"></a><span data-ttu-id="3f063-326">Résumé</span><span class="sxs-lookup"><span data-stu-id="3f063-326">Summary</span></span>
<span data-ttu-id="3f063-327">Dans ce didacticiel, vous avez créé une fabrique de données Azure pour copier des données d'objet blob Azure dans une base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="3f063-327">In this tutorial, you created an Azure data factory to copy data from an Azure blob to an Azure SQL database.</span></span> <span data-ttu-id="3f063-328">Vous avez utilisé Visual Studio pour créer la fabrique de données, les services liés, les jeux de données et un pipeline.</span><span class="sxs-lookup"><span data-stu-id="3f063-328">You used Visual Studio to create the data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="3f063-329">Voici les opérations globales que vous avez effectuées dans ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="3f063-329">Here are the high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="3f063-330">Création d’une **fabrique de données**Azure.</span><span class="sxs-lookup"><span data-stu-id="3f063-330">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="3f063-331">Création de **services liés**:</span><span class="sxs-lookup"><span data-stu-id="3f063-331">Created **linked services**:</span></span>
   1. <span data-ttu-id="3f063-332">Un service lié **Stockage Azure** pour lier votre compte Stockage Azure contenant des données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="3f063-332">An **Azure Storage** linked service to link your Azure Storage account that holds input data.</span></span>     
   2. <span data-ttu-id="3f063-333">Un service lié **Azure SQL** pour lier votre base de données Azure SQL contenant les données de sortie.</span><span class="sxs-lookup"><span data-stu-id="3f063-333">An **Azure SQL** linked service to link your Azure SQL database that holds the output data.</span></span> 
3. <span data-ttu-id="3f063-334">Création des **jeux de données**qui décrivent les données d’entrée et de sortie des pipelines.</span><span class="sxs-lookup"><span data-stu-id="3f063-334">Created **datasets**, which describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="3f063-335">Création d’un **pipeline** avec une **activité de copie** avec **BlobSource** en tant que source et **SqlSink** en tant que récepteur.</span><span class="sxs-lookup"><span data-stu-id="3f063-335">Created a **pipeline** with a **Copy Activity** with **BlobSource** as source and **SqlSink** as sink.</span></span> 

<span data-ttu-id="3f063-336">Pour savoir comment utiliser une activité Hive HDInsight pour transformer des données à l’aide du cluster Azure HDInsight, consultez [Didacticiel : Générer votre premier pipeline pour traiter les données à l’aide du cluster Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="3f063-336">To see how to use a HDInsight Hive Activity to transform data by using Azure HDInsight cluster, see [ Tutorial: Build your first pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

<span data-ttu-id="3f063-337">Vous pouvez chaîner deux activités (une après l’autre) en configurant le jeu de données de sortie d’une activité en tant que jeu de données d’entrée de l’autre activité.</span><span class="sxs-lookup"><span data-stu-id="3f063-337">You can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="3f063-338">Pour des informations détaillées, consultez [Planification et exécution avec Data Factory](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="3f063-338">See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.</span></span> 

## <a name="view-all-data-factories-in-server-explorer"></a><span data-ttu-id="3f063-339">Afficher toutes les fabriques de données dans l’Explorateur de serveurs</span><span class="sxs-lookup"><span data-stu-id="3f063-339">View all data factories in Server Explorer</span></span>
<span data-ttu-id="3f063-340">Cette section explique comment utiliser l’Explorateur de serveurs dans Visual Studio pour afficher toutes les fabriques de données dans votre abonnement Azure et créer un projet Visual Studio basé sur une fabrique de données existante.</span><span class="sxs-lookup"><span data-stu-id="3f063-340">This section describes how to use the Server Explorer in Visual Studio to view all the data factories in your Azure subscription and create a Visual Studio project based on an existing data factory.</span></span> 

1. <span data-ttu-id="3f063-341">Dans **Visual Studio**, cliquez sur **Affichage** dans le menu, puis sur **Explorateur de serveurs**.</span><span class="sxs-lookup"><span data-stu-id="3f063-341">In **Visual Studio**, click **View** on the menu, and click **Server Explorer**.</span></span>
2. <span data-ttu-id="3f063-342">Dans la fenêtre Explorateur de serveurs, développez **Azure**, puis **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="3f063-342">In the Server Explorer window, expand **Azure** and expand **Data Factory**.</span></span> <span data-ttu-id="3f063-343">Si la boîte de dialogue **Connectez-vous à Visual Studio** s’affiche, saisissez le **compte** associé à votre abonnement Azure, puis cliquez sur **Continuer**.</span><span class="sxs-lookup"><span data-stu-id="3f063-343">If you see **Sign in to Visual Studio**, enter the **account** associated with your Azure subscription and click **Continue**.</span></span> <span data-ttu-id="3f063-344">Saisissez le **mot de passe**, puis cliquez sur **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="3f063-344">Enter **password**, and click **Sign in**.</span></span> <span data-ttu-id="3f063-345">Visual Studio essaie d’obtenir des informations sur toutes les fabriques de données Azure contenues dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="3f063-345">Visual Studio tries to get information about all Azure data factories in your subscription.</span></span> <span data-ttu-id="3f063-346">L’état de cette opération s’affiche dans la fenêtre **Liste des tâches de Data Factory** .</span><span class="sxs-lookup"><span data-stu-id="3f063-346">You see the status of this operation in the **Data Factory Task List** window.</span></span>

    ![Explorateur de serveurs](./media/data-factory-copy-activity-tutorial-using-visual-studio/server-explorer.png)

## <a name="create-a-visual-studio-project-for-an-existing-data-factory"></a><span data-ttu-id="3f063-348">Créer un projet Visual Studio pour une fabrique de données existante</span><span class="sxs-lookup"><span data-stu-id="3f063-348">Create a Visual Studio project for an existing data factory</span></span>

- <span data-ttu-id="3f063-349">Cliquez avec le bouton droit sur une fabrique de données dans l’Explorateur de serveurs, puis sélectionnez **Exporter la fabrique de données vers le nouveau projet** pour créer un projet Visual Studio basé sur une fabrique de données existante.</span><span class="sxs-lookup"><span data-stu-id="3f063-349">Right-click a data factory in Server Explorer, and select **Export Data Factory to New Project** to create a Visual Studio project based on an existing data factory.</span></span>

    ![Exporter la fabrique de données vers un projet Visual Studio](./media/data-factory-copy-activity-tutorial-using-visual-studio/export-data-factory-menu.png)  

## <a name="update-data-factory-tools-for-visual-studio"></a><span data-ttu-id="3f063-351">Mettre à jour des outils Data Factory pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3f063-351">Update Data Factory tools for Visual Studio</span></span>
<span data-ttu-id="3f063-352">Pour mettre à jour des outils Azure Data Factory pour Visual Studio, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="3f063-352">To update Azure Data Factory tools for Visual Studio, do the following steps:</span></span>

1. <span data-ttu-id="3f063-353">Dans le menu, cliquez sur **Outils**, puis sélectionnez **Extensions et mises à jour**.</span><span class="sxs-lookup"><span data-stu-id="3f063-353">Click **Tools** on the menu and select **Extensions and Updates**.</span></span> 
2. <span data-ttu-id="3f063-354">Dans le volet de gauche, sélectionnez **Mises à jour**, puis **Galerie Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="3f063-354">Select **Updates** in the left pane and then select **Visual Studio Gallery**.</span></span>
3. <span data-ttu-id="3f063-355">Sélectionnez **Outils Azure Data Factory pour Visual Studio**, puis cliquez sur **Mettre à jour**.</span><span class="sxs-lookup"><span data-stu-id="3f063-355">Select **Azure Data Factory tools for Visual Studio** and click **Update**.</span></span> <span data-ttu-id="3f063-356">Si cette entrée n’est pas affichée, c’est que vous possédez déjà la dernière version de ces outils.</span><span class="sxs-lookup"><span data-stu-id="3f063-356">If you do not see this entry, you already have the latest version of the tools.</span></span> 

## <a name="use-configuration-files"></a><span data-ttu-id="3f063-357">Utiliser des fichiers de configuration</span><span class="sxs-lookup"><span data-stu-id="3f063-357">Use configuration files</span></span>
<span data-ttu-id="3f063-358">Vous pouvez utiliser des fichiers de configuration dans Visual Studio pour configurer les propriétés des services/tableaux/pipelines liés différemment pour chaque environnement.</span><span class="sxs-lookup"><span data-stu-id="3f063-358">You can use configuration files in Visual Studio to configure properties for linked services/tables/pipelines differently for each environment.</span></span>

<span data-ttu-id="3f063-359">Examinez la définition JSON suivante pour un service lié Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="3f063-359">Consider the following JSON definition for an Azure Storage linked service.</span></span> <span data-ttu-id="3f063-360">Spécifiez **connectionString** avec différentes valeurs pour accountname et accountkey, en fonction de l’environnement (dév./test/production) sur lequel vous déployez des entités Data Factory.</span><span class="sxs-lookup"><span data-stu-id="3f063-360">To specify **connectionString** with different values for accountname and accountkey based on the environment (Dev/Test/Production) to which you are deploying Data Factory entities.</span></span> <span data-ttu-id="3f063-361">Vous pouvez parvenir à ce comportement en utilisant un fichier de configuration distinct pour chaque environnement.</span><span class="sxs-lookup"><span data-stu-id="3f063-361">You can achieve this behavior by using separate configuration file for each environment.</span></span>

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

### <a name="add-a-configuration-file"></a><span data-ttu-id="3f063-362">Ajouter un fichier de configuration</span><span class="sxs-lookup"><span data-stu-id="3f063-362">Add a configuration file</span></span>
<span data-ttu-id="3f063-363">Ajoutez un fichier de configuration pour chaque environnement en effectuant les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="3f063-363">Add a configuration file for each environment by performing the following steps:</span></span>   

1. <span data-ttu-id="3f063-364">Cliquez avec le bouton droit de la souris sur le projet Data Factory dans votre solution Visual Studio, pointez sur **Ajouter**, puis cliquez sur **Nouvel élément**.</span><span class="sxs-lookup"><span data-stu-id="3f063-364">Right-click the Data Factory project in your Visual Studio solution, point to **Add**, and click **New item**.</span></span>
2. <span data-ttu-id="3f063-365">Sélectionnez **Config** dans la liste des modèles installés sur la gauche, choisissez **Fichier de configuration**, entrez un **nom** pour ce fichier, puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="3f063-365">Select **Config** from the list of installed templates on the left, select **Configuration File**, enter a **name** for the configuration file, and click **Add**.</span></span>

    ![Ajouter un fichier de configuration](./media/data-factory-build-your-first-pipeline-using-vs/add-config-file.png)
3. <span data-ttu-id="3f063-367">Ajoutez les paramètres de configuration et leurs valeurs au format suivant :</span><span class="sxs-lookup"><span data-stu-id="3f063-367">Add configuration parameters and their values in the following format:</span></span>

    ```json
    {
        "$schema": "http://datafactories.schema.management.azure.com/vsschemas/V1/Microsoft.DataFactory.Config.json",
        "AzureStorageLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        ],
        "AzureSqlLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value":  "Server=tcp:spsqlserver.database.windows.net,1433;Database=spsqldb;User ID=spelluru;Password=Sowmya123;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        ]
    }
    ```

    <span data-ttu-id="3f063-368">Cet exemple configure la propriété connectionString d’un service lié Azure Storage et d’un service lié SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="3f063-368">This example configures connectionString property of an Azure Storage linked service and an Azure SQL linked service.</span></span> <span data-ttu-id="3f063-369">Notez que la syntaxe de spécification du nom est [JsonPath](http://goessner.net/articles/JsonPath/).</span><span class="sxs-lookup"><span data-stu-id="3f063-369">Notice that the syntax for specifying name is [JsonPath](http://goessner.net/articles/JsonPath/).</span></span>   

    <span data-ttu-id="3f063-370">Si JSON est doté d’une propriété ayant un tableau de valeurs comme indiqué dans le code suivant :</span><span class="sxs-lookup"><span data-stu-id="3f063-370">If JSON has a property that has an array of values as shown in the following code:</span></span>  

    ```json
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
    ```

    <span data-ttu-id="3f063-371">Configurez les propriétés comme indiqué dans le fichier de configuration suivant (utilisez indexation de base zéro) :</span><span class="sxs-lookup"><span data-stu-id="3f063-371">Configure properties as shown in the following configuration file (use zero-based indexing):</span></span>

    ```json
    {
        "name": "$.properties.structure[0].name",
        "value": "FirstName"
    }
    {
        "name": "$.properties.structure[0].type",
        "value": "String"
    }
    {
        "name": "$.properties.structure[1].name",
        "value": "LastName"
    }
    {
        "name": "$.properties.structure[1].type",
        "value": "String"
    }
    ```

### <a name="property-names-with-spaces"></a><span data-ttu-id="3f063-372">Noms de propriétés avec des espaces</span><span class="sxs-lookup"><span data-stu-id="3f063-372">Property names with spaces</span></span>
<span data-ttu-id="3f063-373">Si un nom de propriété comporte des espaces, utilisez des crochets comme indiqué dans l’exemple suivant (nom de serveur de base de données) :</span><span class="sxs-lookup"><span data-stu-id="3f063-373">If a property name has spaces in it, use square brackets as shown in the following example (Database server name):</span></span>

```json
 {
     "name": "$.properties.activities[1].typeProperties.webServiceParameters.['Database server name']",
     "value": "MyAsqlServer.database.windows.net"
 }
```

### <a name="deploy-solution-using-a-configuration"></a><span data-ttu-id="3f063-374">Déployer une solution à l’aide d’une configuration</span><span class="sxs-lookup"><span data-stu-id="3f063-374">Deploy solution using a configuration</span></span>
<span data-ttu-id="3f063-375">Lorsque vous publiez des entités Azure Data Factory dans Visual Studio, vous pouvez spécifier la configuration que vous souhaitez utiliser pour cette opération de publication.</span><span class="sxs-lookup"><span data-stu-id="3f063-375">When you are publishing Azure Data Factory entities in VS, you can specify the configuration that you want to use for that publishing operation.</span></span>

<span data-ttu-id="3f063-376">Pour publier des entités dans un projet Azure Data Factory à l’aide d’un fichier de configuration :</span><span class="sxs-lookup"><span data-stu-id="3f063-376">To publish entities in an Azure Data Factory project using configuration file:</span></span>   

1. <span data-ttu-id="3f063-377">Cliquez avec le bouton droit sur le projet Data Factory, puis cliquez sur **Publier** pour afficher la boîte de dialogue **Publier des éléments**.</span><span class="sxs-lookup"><span data-stu-id="3f063-377">Right-click Data Factory project and click **Publish** to see the **Publish Items** dialog box.</span></span>
2. <span data-ttu-id="3f063-378">Dans la page **Configurer une fabrique de données**, sélectionnez une fabrique de données existante ou spécifiez les valeurs pour en créer une, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="3f063-378">Select an existing data factory or specify values for creating a data factory on the **Configure data factory** page, and click **Next**.</span></span>   
3. <span data-ttu-id="3f063-379">La page **Publier des éléments** contient une liste déroulante avec les configurations disponibles pour le champ **Sélectionner une configuration de déploiement**.</span><span class="sxs-lookup"><span data-stu-id="3f063-379">On the **Publish Items** page: you see a drop-down list with available configurations for the **Select Deployment Config** field.</span></span>

    ![Sélectionner un fichier de config](./media/data-factory-build-your-first-pipeline-using-vs/select-config-file.png)
4. <span data-ttu-id="3f063-381">Sélectionnez le **fichier de configuration** que vous souhaitez utiliser, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="3f063-381">Select the **configuration file** that you would like to use and click **Next**.</span></span>
5. <span data-ttu-id="3f063-382">Vérifiez que vous voyez bien le nom du fichier JSON dans la page **Résumé**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="3f063-382">Confirm that you see the name of JSON file in the **Summary** page and click **Next**.</span></span>
6. <span data-ttu-id="3f063-383">Une fois l’opération de déploiement terminée, cliquez sur **Terminer** .</span><span class="sxs-lookup"><span data-stu-id="3f063-383">Click **Finish** after the deployment operation is finished.</span></span>

<span data-ttu-id="3f063-384">Au cours du déploiement, les valeurs du fichier de configuration sont utilisées pour définir celles des propriétés des fichiers JSON avant que les entités ne soient déployées sur le service Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="3f063-384">When you deploy, the values from the configuration file are used to set values for properties in the JSON files before the entities are deployed to Azure Data Factory service.</span></span>   

## <a name="use-azure-key-vault"></a><span data-ttu-id="3f063-385">Utiliser Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="3f063-385">Use Azure Key Vault</span></span>
<span data-ttu-id="3f063-386">Il n’est pas recommandé et souvent déconseillé vis-à-vis de la stratégie de sécurité pour valider des données sensibles telles que des chaînes de connexion au référentiel de code.</span><span class="sxs-lookup"><span data-stu-id="3f063-386">It is not advisable and often against security policy to commit sensitive data such as connection strings to the code repository.</span></span> <span data-ttu-id="3f063-387">Consultez l’exemple [ADF Secure Publish](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) sur GitHub pour en savoir plus sur le stockage d’informations sensibles dans Azure Key Vault et son utilisation lors de la publication des entités Data Factory.</span><span class="sxs-lookup"><span data-stu-id="3f063-387">See [ADF Secure Publish](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) sample on GitHub to learn about storing sensitive information in Azure Key Vault and using it while publishing Data Factory entities.</span></span> <span data-ttu-id="3f063-388">L’extension Secure Publish pour Visual Studio permet de stocker les secrets dans Key Vault, et seules les références à ceux-ci sont spécifiés dans des services / configurations de déploiement liés.</span><span class="sxs-lookup"><span data-stu-id="3f063-388">The Secure Publish extension for Visual Studio allows the secrets to be stored in Key Vault and only references to them are specified in linked services/ deployment configurations.</span></span> <span data-ttu-id="3f063-389">Ces références sont résolues lorsque vous publiez des entités Data Factory dans Azure.</span><span class="sxs-lookup"><span data-stu-id="3f063-389">These references are resolved when you publish Data Factory entities to Azure.</span></span> <span data-ttu-id="3f063-390">Ces fichiers peuvent ensuite être validés sur le référentiel source sans exposer les secrets.</span><span class="sxs-lookup"><span data-stu-id="3f063-390">These files can then be committed to source repository without exposing any secrets.</span></span>


## <a name="next-steps"></a><span data-ttu-id="3f063-391">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3f063-391">Next steps</span></span>
<span data-ttu-id="3f063-392">Dans ce didacticiel, vous avez utilisé le stockage Blob Azure comme magasin de données source et une base de données SQL Azure comme banque de données de destination dans une opération de copie.</span><span class="sxs-lookup"><span data-stu-id="3f063-392">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="3f063-393">Le tableau ci-dessous contient la liste des magasins de données pris en charge en tant que sources et destinations par l’activité de copie :</span><span class="sxs-lookup"><span data-stu-id="3f063-393">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="3f063-394">Pour découvrir comment copier des données vers/depuis un magasin de données, cliquez sur le lien du magasin de données dans le tableau.</span><span class="sxs-lookup"><span data-stu-id="3f063-394">To learn about how to copy data to/from a data store, click the link for the data store in the table.</span></span>