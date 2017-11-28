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
ms.openlocfilehash: d99d8875807bab41f5122ab95a09f83f82923529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-visual-studio"></a><span data-ttu-id="bde22-103">Didacticiel : Créer un pipeline avec l'activité de copie à l'aide de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bde22-103">Tutorial: Create a pipeline with Copy Activity using Visual Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bde22-104">Vue d’ensemble et étapes préalables requises</span><span class="sxs-lookup"><span data-stu-id="bde22-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="bde22-105">Assistant de copie</span><span class="sxs-lookup"><span data-stu-id="bde22-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="bde22-106">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="bde22-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="bde22-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bde22-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="bde22-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bde22-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="bde22-109">Modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bde22-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="bde22-110">API REST</span><span class="sxs-lookup"><span data-stu-id="bde22-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="bde22-111">API .NET</span><span class="sxs-lookup"><span data-stu-id="bde22-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="bde22-112">Dans cet article, vous découvrez comment toouse hello toocreate de Microsoft Visual Studio, une fabrique de données avec un pipeline qui copie les données à partir d’une base de données SQL Azure de tooan stockage blob Azure.</span><span class="sxs-lookup"><span data-stu-id="bde22-112">In this article, you learn how toouse hello Microsoft Visual Studio toocreate a data factory with a pipeline that copies data from an Azure blob storage tooan Azure SQL database.</span></span> <span data-ttu-id="bde22-113">Si vous êtes tooAzure nouvelle fabrique de données, lisez hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article avant d’entamer ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="bde22-113">If you are new tooAzure Data Factory, read through hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="bde22-114">Dans ce didacticiel, vous créez un pipeline avec une activité : activité de copie.</span><span class="sxs-lookup"><span data-stu-id="bde22-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="bde22-115">activité de copie Hello copie des données à partir d’un magasin de données de données pris en charge magasin tooa récepteur pris en charge.</span><span class="sxs-lookup"><span data-stu-id="bde22-115">hello copy activity copies data from a supported data store tooa supported sink data store.</span></span> <span data-ttu-id="bde22-116">Pour obtenir la liste des magasins de données pris en charge en tant que sources et récepteurs, consultez [Magasins de données pris en charge](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="bde22-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="bde22-117">activité Hello est rendue possible par un service globalement disponible qui permettre copier des données entre différentes banques de données de manière sécurisée, fiable et évolutive.</span><span class="sxs-lookup"><span data-stu-id="bde22-117">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="bde22-118">Pour plus d’informations sur l’activité de copie de hello, consultez [les activités de déplacement des données](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="bde22-118">For more information about hello Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="bde22-119">Un pipeline peut contenir plusieurs activités.</span><span class="sxs-lookup"><span data-stu-id="bde22-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="bde22-120">De plus, vous pouvez concaténer les deux activités (exécutée une activité après l’autre) en définissant le dataset de sortie hello d’une activité hello d’entrée dataset Hello autre activité.</span><span class="sxs-lookup"><span data-stu-id="bde22-120">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="bde22-121">Pour plus d’informations, consultez [Plusieurs activités dans un pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="bde22-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

> [!NOTE] 
> <span data-ttu-id="bde22-122">le pipeline de données Hello dans ce didacticiel copie des données à partir d’un magasin de données de destination source données magasin tooa.</span><span class="sxs-lookup"><span data-stu-id="bde22-122">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="bde22-123">Pour obtenir un didacticiel sur la façon de tootransform les données à l’aide d’Azure Data Factory, consultez [didacticiel : créer un pipeline de données tootransform à l’aide de cluster Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="bde22-123">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bde22-124">Composants requis</span><span class="sxs-lookup"><span data-stu-id="bde22-124">Prerequisites</span></span>
1. <span data-ttu-id="bde22-125">Lisez [vue d’ensemble du didacticiel](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article et hello complète **condition préalable** étapes.</span><span class="sxs-lookup"><span data-stu-id="bde22-125">Read through [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article and complete hello **prerequisite** steps.</span></span>       
2. <span data-ttu-id="bde22-126">instances de fabrique de données toocreate, vous devez être membre du hello [collaborateur de fabrique de données](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) rôle au niveau de groupe de ressource d’abonnement hello.</span><span class="sxs-lookup"><span data-stu-id="bde22-126">toocreate Data Factory instances, you must be a member of hello [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at hello subscription/resource group level.</span></span>
3. <span data-ttu-id="bde22-127">Vous devez disposer de hello installé sur votre ordinateur :</span><span class="sxs-lookup"><span data-stu-id="bde22-127">You must have hello following installed on your computer:</span></span> 
   * <span data-ttu-id="bde22-128">Visual Studio 2013 ou Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="bde22-128">Visual Studio 2013 or Visual Studio 2015</span></span>
   * <span data-ttu-id="bde22-129">Téléchargez le Kit de développement logiciel (SDK) Azure pour Visual Studio 2013 ou Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="bde22-129">Download Azure SDK for Visual Studio 2013 or Visual Studio 2015.</span></span> <span data-ttu-id="bde22-130">Accédez trop[Page de téléchargement Azure](https://azure.microsoft.com/downloads/) et cliquez sur **VS 2013** ou **VS 2015** Bonjour **.NET** section.</span><span class="sxs-lookup"><span data-stu-id="bde22-130">Navigate too[Azure Download Page](https://azure.microsoft.com/downloads/) and click **VS 2013** or **VS 2015** in hello **.NET** section.</span></span>
   * <span data-ttu-id="bde22-131">Téléchargement du plug-in Azure Data Factory dernière hello pour Visual Studio : [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) ou [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005).</span><span class="sxs-lookup"><span data-stu-id="bde22-131">Download hello latest Azure Data Factory plugin for Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) or [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005).</span></span> <span data-ttu-id="bde22-132">Vous pouvez également actualiser les plug-in hello en procédant comme hello comme suit : cliquez sur hello, **outils** -> **Extensions et mises à jour** -> **Online**  ->  **Galerie visual Studio** -> **Microsoft Azure Data Factory Tools pour Visual Studio** -> **mise à jour**.</span><span class="sxs-lookup"><span data-stu-id="bde22-132">You can also update hello plugin by doing hello following steps: On hello menu, click **Tools** -> **Extensions and Updates** -> **Online** -> **Visual Studio Gallery** -> **Microsoft Azure Data Factory Tools for Visual Studio** -> **Update**.</span></span>

## <a name="steps"></a><span data-ttu-id="bde22-133">Étapes</span><span class="sxs-lookup"><span data-stu-id="bde22-133">Steps</span></span>
<span data-ttu-id="bde22-134">Voici les étapes hello que vous effectuez dans le cadre de ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="bde22-134">Here are hello steps you perform as part of this tutorial:</span></span>

1. <span data-ttu-id="bde22-135">Créer **services liés** dans la fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="bde22-135">Create **linked services** in hello data factory.</span></span> <span data-ttu-id="bde22-136">Au cours de cette étape, vous allez créer deux services liés de types : Stockage Azure et base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="bde22-136">In this step, you create two linked services of types: Azure Storage and Azure SQL Database.</span></span> 
    
    <span data-ttu-id="bde22-137">Hello AzureStorageLinkedService lie votre fabrique de données toohello compte stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="bde22-137">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="bde22-138">Création d’un conteneur et de téléchargé de compte de stockage de données toothis dans le cadre de [conditions préalables](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="bde22-138">You created a container and uploaded data toothis storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

    <span data-ttu-id="bde22-139">AzureSqlLinkedService lie votre fabrique de données de toohello de base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="bde22-139">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="bde22-140">données Hello sont copiées à partir du stockage d’objets blob hello sont stockées dans cette base de données.</span><span class="sxs-lookup"><span data-stu-id="bde22-140">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="bde22-141">Vous avez créé une table SQL dans cette base de données en remplissant les [conditions préalables](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="bde22-141">You created a SQL table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>     
2. <span data-ttu-id="bde22-142">Créer des entrées et sorties **jeux de données** dans la fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="bde22-142">Create input and output **datasets** in hello data factory.</span></span>  
    
    <span data-ttu-id="bde22-143">service lié Azure storage de Hello spécifie la chaîne de connexion hello service Data Factory utilise au moment de l’exécution tooconnect tooyour compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="bde22-143">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="bde22-144">Et, le jeu de données objet blob d’entrée hello Spécifie le conteneur de hello et dossier hello qui contient les données d’entrée hello.</span><span class="sxs-lookup"><span data-stu-id="bde22-144">And, hello input blob dataset specifies hello container and hello folder that contains hello input data.</span></span>  

    <span data-ttu-id="bde22-145">De même, hello service de base de données SQL Azure lié spécifie la chaîne de connexion hello service Data Factory utilise au moment de l’exécution tooconnect tooyour Azure base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="bde22-145">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="bde22-146">De plus, hello sortie SQL table dataset spécifie table hello dans les données de hello toowhich hello de base de données à partir du stockage d’objets blob hello est copié.</span><span class="sxs-lookup"><span data-stu-id="bde22-146">And, hello output SQL table dataset specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span>
3. <span data-ttu-id="bde22-147">Créer un **pipeline** dans la fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="bde22-147">Create a **pipeline** in hello data factory.</span></span> <span data-ttu-id="bde22-148">Dans cette étape, vous allez créer un pipeline avec une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="bde22-148">In this step, you create a pipeline with a copy activity.</span></span>   
    
    <span data-ttu-id="bde22-149">activité de copie Hello copie des données à partir d’un objet blob dans la table du tooa du stockage blob Azure hello dans la base de données SQL Azure hello.</span><span class="sxs-lookup"><span data-stu-id="bde22-149">hello copy activity copies data from a blob in hello Azure blob storage tooa table in hello Azure SQL database.</span></span> <span data-ttu-id="bde22-150">Vous pouvez utiliser une activité de copie dans un pipeline toocopy des données d’une destination de tooany pris en charge source prise en charge.</span><span class="sxs-lookup"><span data-stu-id="bde22-150">You can use a copy activity in a pipeline toocopy data from any supported source tooany supported destination.</span></span> <span data-ttu-id="bde22-151">Pour obtenir la liste des magasins de données pris en charge, consultez [Activités de déplacement des données](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="bde22-151">For a list of supported data stores, see [data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> 
4. <span data-ttu-id="bde22-152">Créez une **fabrique de données** Azure lors du déploiement des entités Data Factory (services liés, jeux de données/tables et pipelines).</span><span class="sxs-lookup"><span data-stu-id="bde22-152">Create an Azure **data factory** when deploying Data Factory entities (linked services, datasets/tables, and pipelines).</span></span> 

## <a name="create-visual-studio-project"></a><span data-ttu-id="bde22-153">Création d’un projet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bde22-153">Create Visual Studio project</span></span>
1. <span data-ttu-id="bde22-154">Lancez **Visual Studio 2015**.</span><span class="sxs-lookup"><span data-stu-id="bde22-154">Launch **Visual Studio 2015**.</span></span> <span data-ttu-id="bde22-155">Cliquez sur **fichier**, pointez trop**nouveau**, puis cliquez sur **projet**.</span><span class="sxs-lookup"><span data-stu-id="bde22-155">Click **File**, point too**New**, and click **Project**.</span></span> <span data-ttu-id="bde22-156">Vous devez voir hello **nouveau projet** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="bde22-156">You should see hello **New Project** dialog box.</span></span>  
2. <span data-ttu-id="bde22-157">Bonjour **nouveau projet** boîte de dialogue, sélectionnez hello **DataFactory** modèle, puis cliquez sur **projet de la fabrique de données vide**.</span><span class="sxs-lookup"><span data-stu-id="bde22-157">In hello **New Project** dialog, select hello **DataFactory** template, and click **Empty Data Factory Project**.</span></span>  
   
    ![Boîte de dialogue Nouveau projet](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-project-dialog.png)
3. <span data-ttu-id="bde22-159">Spécifiez le nom hello de projet de hello, l’emplacement de la solution de hello et le nom de la solution de hello, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="bde22-159">Specify hello name of hello project, location for hello solution, and name of hello solution, and then click **OK**.</span></span>
   
    ![Explorateur de solutions](./media/data-factory-copy-activity-tutorial-using-visual-studio/solution-explorer.png)    

## <a name="create-linked-services"></a><span data-ttu-id="bde22-161">Créez des services liés</span><span class="sxs-lookup"><span data-stu-id="bde22-161">Create linked services</span></span>
<span data-ttu-id="bde22-162">Vous créez des services liés dans un toolink de fabrique de données stocke de vos données et fabrique de données toohello de services de calcul.</span><span class="sxs-lookup"><span data-stu-id="bde22-162">You create linked services in a data factory toolink your data stores and compute services toohello data factory.</span></span> <span data-ttu-id="bde22-163">Dans ce didacticiel, vous n’allez pas utiliser n’importe quel service de calcul comme Azure HDInsight ou Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="bde22-163">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="bde22-164">Vous allez utiliser deux magasins de données de type Stockage Azure (source) et Base de données SQL Azure (destination).</span><span class="sxs-lookup"><span data-stu-id="bde22-164">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

<span data-ttu-id="bde22-165">Vous allez donc créer deux services liés de types : AzureStorage et AzureSqlDatabase.</span><span class="sxs-lookup"><span data-stu-id="bde22-165">Therefore, you create two linked services of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="bde22-166">Hello le stockage Azure lié à des liens de service votre fabrique de données toohello compte stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="bde22-166">hello Azure Storage linked service links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="bde22-167">Ce compte de stockage est hello une dans laquelle vous créé un conteneur et à télécharger des données de hello dans le cadre de [conditions préalables](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="bde22-167">This storage account is hello one in which you created a container and uploaded hello data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="bde22-168">Liaisons de service de lié SQL Azure votre fabrique de données de toohello de base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="bde22-168">Azure SQL linked service links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="bde22-169">données Hello sont copiées à partir du stockage d’objets blob hello sont stockées dans cette base de données.</span><span class="sxs-lookup"><span data-stu-id="bde22-169">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="bde22-170">Vous avez créé la table emp de hello dans cette base de données dans le cadre de [conditions préalables](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="bde22-170">You created hello emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

<span data-ttu-id="bde22-171">Services liés lier des magasins de données ou la fabrique de données Azure tooan de services de calcul.</span><span class="sxs-lookup"><span data-stu-id="bde22-171">Linked services link data stores or compute services tooan Azure data factory.</span></span> <span data-ttu-id="bde22-172">Consultez [prise en charge des magasins de données](data-factory-data-movement-activities.md#supported-data-stores-and-formats) pour tous les hello sources et récepteurs pris en charge par l’activité de copie de hello.</span><span class="sxs-lookup"><span data-stu-id="bde22-172">See [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for all hello sources and sinks supported by hello Copy Activity.</span></span> <span data-ttu-id="bde22-173">Consultez [services liés de calcul](data-factory-compute-linked-services.md) pour la liste des services de calcul pris en charge par la fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="bde22-173">See [compute linked services](data-factory-compute-linked-services.md) for hello list of compute services supported by Data Factory.</span></span> <span data-ttu-id="bde22-174">Dans ce didacticiel, aucun service de calcul n’est utilisé.</span><span class="sxs-lookup"><span data-stu-id="bde22-174">In this tutorial, you do not use any compute service.</span></span> 

### <a name="create-hello-azure-storage-linked-service"></a><span data-ttu-id="bde22-175">Créer le service lié Azure Storage de hello</span><span class="sxs-lookup"><span data-stu-id="bde22-175">Create hello Azure Storage linked service</span></span>
1. <span data-ttu-id="bde22-176">Dans **l’Explorateur de solutions**, avec le bouton droit **Services liés**, pointez trop**ajouter**, puis cliquez sur **un nouvel élément**.</span><span class="sxs-lookup"><span data-stu-id="bde22-176">In **Solution Explorer**, right-click **Linked Services**, point too**Add**, and click **New Item**.</span></span>      
2. <span data-ttu-id="bde22-177">Bonjour **ajouter un nouvel élément** boîte de dialogue, sélectionnez **Service lié Azure Storage** à partir de la liste de hello, puis cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="bde22-177">In hello **Add New Item** dialog box, select **Azure Storage Linked Service** from hello list, and click **Add**.</span></span> 
   
    ![Nouveau service lié](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-linked-service-dialog.png)
3. <span data-ttu-id="bde22-179">Remplacez `<accountname>` et `<accountkey>`* nom hello de votre compte de stockage Azure et sa clé.</span><span class="sxs-lookup"><span data-stu-id="bde22-179">Replace `<accountname>` and `<accountkey>`* with hello name of your Azure storage account and its key.</span></span> 
   
    ![Service lié Stockage Azure](./media/data-factory-copy-activity-tutorial-using-visual-studio/azure-storage-linked-service.png)
4. <span data-ttu-id="bde22-181">Enregistrer hello **AzureStorageLinkedService1.json** fichier.</span><span class="sxs-lookup"><span data-stu-id="bde22-181">Save hello **AzureStorageLinkedService1.json** file.</span></span>

    <span data-ttu-id="bde22-182">Pour plus d’informations sur les propriétés JSON dans la définition de service hello lié, consultez [connecteur de stockage d’objets Blob Azure](data-factory-azure-blob-connector.md#linked-service-properties) l’article.</span><span class="sxs-lookup"><span data-stu-id="bde22-182">For more information about JSON properties in hello linked service definition, see [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) article.</span></span>

### <a name="create-hello-azure-sql-linked-service"></a><span data-ttu-id="bde22-183">Créer le service lié SQL Azure de hello</span><span class="sxs-lookup"><span data-stu-id="bde22-183">Create hello Azure SQL linked service</span></span>
1. <span data-ttu-id="bde22-184">Avec le bouton droit sur **Services liés** nœud Bonjour **l’Explorateur de solutions** à nouveau, pointez trop**ajouter**, puis cliquez sur **un nouvel élément**.</span><span class="sxs-lookup"><span data-stu-id="bde22-184">Right-click on **Linked Services** node in hello **Solution Explorer** again, point too**Add**, and click **New Item**.</span></span> 
2. <span data-ttu-id="bde22-185">Cette fois, sélectionnez **Service lié SQL Azure**, puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="bde22-185">This time, select **Azure SQL Linked Service**, and click **Add**.</span></span> 
3. <span data-ttu-id="bde22-186">Bonjour **AzureSqlLinkedService1.json fichier**, remplacez `<servername>`, `<databasename>`, `<username@servername>`, et `<password>` avec des noms de votre serveur SQL Azure, base de données, compte d’utilisateur et mot de passe.</span><span class="sxs-lookup"><span data-stu-id="bde22-186">In hello **AzureSqlLinkedService1.json file**, replace `<servername>`, `<databasename>`, `<username@servername>`, and `<password>` with names of your Azure SQL server, database, user account, and password.</span></span>    
4. <span data-ttu-id="bde22-187">Enregistrer hello **AzureSqlLinkedService1.json** fichier.</span><span class="sxs-lookup"><span data-stu-id="bde22-187">Save hello **AzureSqlLinkedService1.json** file.</span></span> 
    
    <span data-ttu-id="bde22-188">Pour plus d’informations sur ces propriétés JSON, consultez [Connecteur de base de données SQL Azure](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="bde22-188">For more information about these JSON properties, see [Azure SQL Database connector](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>


## <a name="create-datasets"></a><span data-ttu-id="bde22-189">Créez les jeux de données</span><span class="sxs-lookup"><span data-stu-id="bde22-189">Create datasets</span></span>
<span data-ttu-id="bde22-190">Dans l’étape précédente de hello, vous avez créé toolink de services liés de votre compte de stockage Azure et de la fabrique de données de tooyour de base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="bde22-190">In hello previous step, you created linked services toolink your Azure Storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="bde22-191">Dans cette étape, vous définissez deux jeux de données nommées InputDataset et OutputDataset qui représentent une entrée et les données de sortie qui sont stockées dans des magasins de données hello visés par AzureStorageLinkedService1 et AzureSqlLinkedService1, respectivement.</span><span class="sxs-lookup"><span data-stu-id="bde22-191">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in hello data stores referred by AzureStorageLinkedService1 and AzureSqlLinkedService1 respectively.</span></span>

<span data-ttu-id="bde22-192">service lié Azure storage de Hello spécifie la chaîne de connexion hello service Data Factory utilise au moment de l’exécution tooconnect tooyour compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="bde22-192">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="bde22-193">Et, le jeu de données objet blob d’entrée hello (InputDataset) spécifie le conteneur de hello et dossier hello qui contient les données d’entrée hello.</span><span class="sxs-lookup"><span data-stu-id="bde22-193">And, hello input blob dataset (InputDataset) specifies hello container and hello folder that contains hello input data.</span></span>  

<span data-ttu-id="bde22-194">De même, hello service de base de données SQL Azure lié spécifie la chaîne de connexion hello service Data Factory utilise au moment de l’exécution tooconnect tooyour Azure base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="bde22-194">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="bde22-195">Et, hello sortie de jeu de données de table SQL (OututDataset) spécifie la table de hello Bonjour de toowhich hello de base de données à partir du stockage d’objets blob hello, les données sont copiées.</span><span class="sxs-lookup"><span data-stu-id="bde22-195">And, hello output SQL table dataset (OututDataset) specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span> 

### <a name="create-input-dataset"></a><span data-ttu-id="bde22-196">Créer le jeu de données d’entrée</span><span class="sxs-lookup"><span data-stu-id="bde22-196">Create input dataset</span></span>
<span data-ttu-id="bde22-197">Dans cette étape, vous créez un dataset nommé InputDataset qui pointe le fichier d’objet blob tooa (emp.txt) dans le dossier racine de hello d’un conteneur d’objets blob (adftutorial) Bonjour Azure Storage est représenté par hello AzureStorageLinkedService1 lié service.</span><span class="sxs-lookup"><span data-stu-id="bde22-197">In this step, you create a dataset named InputDataset that points tooa blob file (emp.txt) in hello root folder of a blob container (adftutorial) in hello Azure Storage represented by hello AzureStorageLinkedService1 linked service.</span></span> <span data-ttu-id="bde22-198">Si vous ne spécifiez une valeur pour le nom de fichier hello (ignorer), les données à partir de tous les objets BLOB dans le dossier d’entrée de hello sont copiés toohello destination.</span><span class="sxs-lookup"><span data-stu-id="bde22-198">If you don't specify a value for hello fileName (or skip it), data from all blobs in hello input folder are copied toohello destination.</span></span> <span data-ttu-id="bde22-199">Dans ce didacticiel, vous spécifiez une valeur pour le nom de fichier hello.</span><span class="sxs-lookup"><span data-stu-id="bde22-199">In this tutorial, you specify a value for hello fileName.</span></span> 

<span data-ttu-id="bde22-200">Ici, vous utilisez le terme hello « tables » plutôt que « jeux de données ».</span><span class="sxs-lookup"><span data-stu-id="bde22-200">Here, you use hello term "tables" rather than "datasets".</span></span> <span data-ttu-id="bde22-201">Une table est un jeu de données rectangulaire et hello seul type de jeu de données pris en charge actuellement.</span><span class="sxs-lookup"><span data-stu-id="bde22-201">A table is a rectangular dataset and is hello only type of dataset supported right now.</span></span> 

1. <span data-ttu-id="bde22-202">Avec le bouton droit **Tables** Bonjour **l’Explorateur de solutions**, pointez trop**ajouter**, puis cliquez sur **un nouvel élément**.</span><span class="sxs-lookup"><span data-stu-id="bde22-202">Right-click **Tables** in hello **Solution Explorer**, point too**Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="bde22-203">Bonjour **ajouter un nouvel élément** boîte de dialogue, sélectionnez **objets Blob Azure**, puis cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="bde22-203">In hello **Add New Item** dialog box, select **Azure Blob**, and click **Add**.</span></span>   
3. <span data-ttu-id="bde22-204">Remplacer un texte JSON hello hello suivant du texte et enregistrer hello **AzureBlobLocation1.json** fichier.</span><span class="sxs-lookup"><span data-stu-id="bde22-204">Replace hello JSON text with hello following text and save hello **AzureBlobLocation1.json** file.</span></span> 

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
    <span data-ttu-id="bde22-205">Hello tableau suivant fournit des descriptions pour les propriétés JSON hello utilisées dans l’extrait de code hello :</span><span class="sxs-lookup"><span data-stu-id="bde22-205">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    | <span data-ttu-id="bde22-206">Propriété</span><span class="sxs-lookup"><span data-stu-id="bde22-206">Property</span></span> | <span data-ttu-id="bde22-207">Description</span><span class="sxs-lookup"><span data-stu-id="bde22-207">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="bde22-208">type</span><span class="sxs-lookup"><span data-stu-id="bde22-208">type</span></span> | <span data-ttu-id="bde22-209">propriété de type Hello est définie trop**AzureBlob** , car les données résident dans un stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="bde22-209">hello type property is set too**AzureBlob** because data resides in an Azure blob storage.</span></span> |
    | <span data-ttu-id="bde22-210">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="bde22-210">linkedServiceName</span></span> | <span data-ttu-id="bde22-211">Fait référence toohello **AzureStorageLinkedService** que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="bde22-211">Refers toohello **AzureStorageLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="bde22-212">folderPath</span><span class="sxs-lookup"><span data-stu-id="bde22-212">folderPath</span></span> | <span data-ttu-id="bde22-213">Spécifie l’objet blob de hello **conteneur** et hello **dossier** qui contient des objets BLOB d’entrée.</span><span class="sxs-lookup"><span data-stu-id="bde22-213">Specifies hello blob **container** and hello **folder** that contains input blobs.</span></span> <span data-ttu-id="bde22-214">Dans ce didacticiel, adftutorial est le conteneur d’objets blob hello et dossier est le dossier racine de hello.</span><span class="sxs-lookup"><span data-stu-id="bde22-214">In this tutorial, adftutorial is hello blob container and folder is hello root folder.</span></span> | 
    | <span data-ttu-id="bde22-215">fileName</span><span class="sxs-lookup"><span data-stu-id="bde22-215">fileName</span></span> | <span data-ttu-id="bde22-216">Cette propriété est facultative.</span><span class="sxs-lookup"><span data-stu-id="bde22-216">This property is optional.</span></span> <span data-ttu-id="bde22-217">Si vous omettez cette propriété, tous les fichiers à partir de hello folderPath sont récupérées.</span><span class="sxs-lookup"><span data-stu-id="bde22-217">If you omit this property, all files from hello folderPath are picked.</span></span> <span data-ttu-id="bde22-218">Dans ce didacticiel, **emp.txt** n’est spécifié pour hello nom de fichier, ainsi que pour ce fichier est récupéré pour le traitement.</span><span class="sxs-lookup"><span data-stu-id="bde22-218">In this tutorial, **emp.txt** is specified for hello fileName, so only that file is picked up for processing.</span></span> |
    | <span data-ttu-id="bde22-219">format -> type</span><span class="sxs-lookup"><span data-stu-id="bde22-219">format -> type</span></span> |<span data-ttu-id="bde22-220">fichier d’entrée de Hello est au format de texte hello, nous utilisons **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="bde22-220">hello input file is in hello text format, so we use **TextFormat**.</span></span> |
    | <span data-ttu-id="bde22-221">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="bde22-221">columnDelimiter</span></span> | <span data-ttu-id="bde22-222">colonnes Hello dans le fichier d’entrée de hello sont délimitées par **caractère virgule (`,`)**.</span><span class="sxs-lookup"><span data-stu-id="bde22-222">hello columns in hello input file are delimited by **comma character (`,`)**.</span></span> |
    | <span data-ttu-id="bde22-223">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="bde22-223">frequency/interval</span></span> | <span data-ttu-id="bde22-224">fréquence de Hello est défini trop**heure** et de l’intervalle est défini trop**1**, ce qui signifie que hello entrée tranches sont disponibles **toutes les heures**.</span><span class="sxs-lookup"><span data-stu-id="bde22-224">hello frequency is set too**Hour** and interval is  set too**1**, which means that hello input slices are available **hourly**.</span></span> <span data-ttu-id="bde22-225">En d’autres termes, hello service Data Factory recherche les données d’entrée toutes les heures dans le dossier racine de hello du conteneur d’objets blob (**adftutorial**) vous avez spécifié.</span><span class="sxs-lookup"><span data-stu-id="bde22-225">In other words, hello Data Factory service looks for input data every hour in hello root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="bde22-226">Il recherche les données de salutation dans hello pipeline début et fin des heures, pas avant ou après ces moments précis.</span><span class="sxs-lookup"><span data-stu-id="bde22-226">It looks for hello data within hello pipeline start and end times, not before or after these times.</span></span>  |
    | <span data-ttu-id="bde22-227">external</span><span class="sxs-lookup"><span data-stu-id="bde22-227">external</span></span> | <span data-ttu-id="bde22-228">Cette propriété a la valeur trop**true** si les données de salutation ne sont pas générées par ce pipeline.</span><span class="sxs-lookup"><span data-stu-id="bde22-228">This property is set too**true** if hello data is not generated by this pipeline.</span></span> <span data-ttu-id="bde22-229">les données d’entrée de salutation dans ce didacticiel sont dans le fichier hello emp.txt, ce qui n’est pas généré par ce pipeline, et nous avons tootrue de cette propriété.</span><span class="sxs-lookup"><span data-stu-id="bde22-229">hello input data in this tutorial is in hello emp.txt file, which is not generated by this pipeline, so we set this property tootrue.</span></span> |

    <span data-ttu-id="bde22-230">Pour plus d’informations sur ces propriétés JSON, voir [Connecteur de stockage Blob Azure](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="bde22-230">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>   

### <a name="create-output-dataset"></a><span data-ttu-id="bde22-231">Créer un jeu de données de sortie</span><span class="sxs-lookup"><span data-stu-id="bde22-231">Create output dataset</span></span>
<span data-ttu-id="bde22-232">Dans cette étape, vous créez un jeu de données de sortie nommé **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="bde22-232">In this step, you create an output dataset named **OutputDataset**.</span></span> <span data-ttu-id="bde22-233">Ce jeu de données pointe tooa SQL table dans la base de données SQL Azure hello représenté par **AzureSqlLinkedService1**.</span><span class="sxs-lookup"><span data-stu-id="bde22-233">This dataset points tooa SQL table in hello Azure SQL database represented by **AzureSqlLinkedService1**.</span></span> 

1. <span data-ttu-id="bde22-234">Avec le bouton droit **Tables** Bonjour **l’Explorateur de solutions** à nouveau, pointez trop**ajouter**, puis cliquez sur **un nouvel élément**.</span><span class="sxs-lookup"><span data-stu-id="bde22-234">Right-click **Tables** in hello **Solution Explorer** again, point too**Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="bde22-235">Bonjour **ajouter un nouvel élément** boîte de dialogue, sélectionnez **SQL Azure**, puis cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="bde22-235">In hello **Add New Item** dialog box, select **Azure SQL**, and click **Add**.</span></span> 
3. <span data-ttu-id="bde22-236">Remplacer un texte JSON hello hello suivant JSON et enregistrer hello **AzureSqlTableLocation1.json** fichier.</span><span class="sxs-lookup"><span data-stu-id="bde22-236">Replace hello JSON text with hello following JSON and save hello **AzureSqlTableLocation1.json** file.</span></span>

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
    <span data-ttu-id="bde22-237">Hello tableau suivant fournit des descriptions pour les propriétés JSON hello utilisées dans l’extrait de code hello :</span><span class="sxs-lookup"><span data-stu-id="bde22-237">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    | <span data-ttu-id="bde22-238">Propriété</span><span class="sxs-lookup"><span data-stu-id="bde22-238">Property</span></span> | <span data-ttu-id="bde22-239">Description</span><span class="sxs-lookup"><span data-stu-id="bde22-239">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="bde22-240">type</span><span class="sxs-lookup"><span data-stu-id="bde22-240">type</span></span> | <span data-ttu-id="bde22-241">propriété de type Hello est définie trop**AzureSqlTable** , car les données sont table tooa copiées dans une base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="bde22-241">hello type property is set too**AzureSqlTable** because data is copied tooa table in an Azure SQL database.</span></span> |
    | <span data-ttu-id="bde22-242">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="bde22-242">linkedServiceName</span></span> | <span data-ttu-id="bde22-243">Fait référence toohello **AzureSqlLinkedService** que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="bde22-243">Refers toohello **AzureSqlLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="bde22-244">TableName</span><span class="sxs-lookup"><span data-stu-id="bde22-244">tableName</span></span> | <span data-ttu-id="bde22-245">Hello spécifié **table** toowhich hello données sont copiées.</span><span class="sxs-lookup"><span data-stu-id="bde22-245">Specified hello **table** toowhich hello data is copied.</span></span> | 
    | <span data-ttu-id="bde22-246">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="bde22-246">frequency/interval</span></span> | <span data-ttu-id="bde22-247">Hello fréquence est définie trop**heure** et l’intervalle est **1**, ce qui signifie que les tranches de sortie hello sont produits **toutes les heures** entre le début du pipeline hello et les heures, pas avant de fin ou après ces moments précis.</span><span class="sxs-lookup"><span data-stu-id="bde22-247">hello frequency is set too**Hour** and interval is **1**, which means that hello output slices are produced **hourly** between hello pipeline start and end times, not before or after these times.</span></span>  |

    <span data-ttu-id="bde22-248">Il existe trois colonnes : **ID**, **FirstName**, et **LastName** : dans la table emp de hello dans la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="bde22-248">There are three columns – **ID**, **FirstName**, and **LastName** – in hello emp table in hello database.</span></span> <span data-ttu-id="bde22-249">ID est une colonne d’identité, vous devez toospecify uniquement **FirstName** et **LastName** ici.</span><span class="sxs-lookup"><span data-stu-id="bde22-249">ID is an identity column, so you need toospecify only **FirstName** and **LastName** here.</span></span>

    <span data-ttu-id="bde22-250">Pour plus d’informations sur ces propriétés JSON, consultez l’article [Connecteur SQL Azure](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="bde22-250">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>

## <a name="create-pipeline"></a><span data-ttu-id="bde22-251">Création d’un pipeline</span><span class="sxs-lookup"><span data-stu-id="bde22-251">Create pipeline</span></span>
<span data-ttu-id="bde22-252">Dans cette étape, vous créez un pipeline avec une **activité de copie** qui utilise **InputDataset** en entrée et **OutputDataset** en sortie.</span><span class="sxs-lookup"><span data-stu-id="bde22-252">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

<span data-ttu-id="bde22-253">Actuellement, le dataset de sortie est les lecteurs hello planification.</span><span class="sxs-lookup"><span data-stu-id="bde22-253">Currently, output dataset is what drives hello schedule.</span></span> <span data-ttu-id="bde22-254">Dans ce didacticiel, le dataset de sortie est tooproduce configuré une tranche une fois par heure.</span><span class="sxs-lookup"><span data-stu-id="bde22-254">In this tutorial, output dataset is configured tooproduce a slice once an hour.</span></span> <span data-ttu-id="bde22-255">pipeline de Hello a une heure de début et l’heure de fin sont un jour séparé, ce qui est de 24 heures.</span><span class="sxs-lookup"><span data-stu-id="bde22-255">hello pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="bde22-256">Par conséquent, 24 tranches du jeu de données de sortie produits par le pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="bde22-256">Therefore, 24 slices of output dataset are produced by hello pipeline.</span></span> 

1. <span data-ttu-id="bde22-257">Avec le bouton droit **Pipelines** Bonjour **l’Explorateur de solutions**, pointez trop**ajouter**, puis cliquez sur **un nouvel élément**.</span><span class="sxs-lookup"><span data-stu-id="bde22-257">Right-click **Pipelines** in hello **Solution Explorer**, point too**Add**, and click **New Item**.</span></span>  
2. <span data-ttu-id="bde22-258">Sélectionnez **Pipeline de données de copie** Bonjour **ajouter un nouvel élément** boîte de dialogue et cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="bde22-258">Select **Copy Data Pipeline** in hello **Add New Item** dialog box and click **Add**.</span></span> 
3. <span data-ttu-id="bde22-259">Remplacez hello JSON hello suivant JSON et enregistrer hello **CopyActivity1.json** fichier.</span><span class="sxs-lookup"><span data-stu-id="bde22-259">Replace hello JSON with hello following JSON and save hello **CopyActivity1.json** file.</span></span>

  ```json   
    {
     "name": "ADFTutorialPipeline",
     "properties": {
       "description": "Copy data from a blob tooAzure SQL table",
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
    - <span data-ttu-id="bde22-260">Dans la section d’activités hello, il n'existe qu’une seule activité dont **type** est défini trop**copie**.</span><span class="sxs-lookup"><span data-stu-id="bde22-260">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span> <span data-ttu-id="bde22-261">Pour plus d’informations sur l’activité de copie hello, consultez [les activités de déplacement des données](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="bde22-261">For more information about hello copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="bde22-262">Dans les solutions Data Factory, vous pouvez également utiliser [Activités de transformation des données](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="bde22-262">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="bde22-263">Entrée d’activité hello est définie trop**InputDataset** et de sortie d’activité hello est définie trop**OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="bde22-263">Input for hello activity is set too**InputDataset** and output for hello activity is set too**OutputDataset**.</span></span> 
    - <span data-ttu-id="bde22-264">Bonjour **typeProperties** section, **BlobSource** est spécifié comme type de source de hello et **SqlSink** est spécifié comme type de récepteur hello.</span><span class="sxs-lookup"><span data-stu-id="bde22-264">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span> <span data-ttu-id="bde22-265">Pour obtenir une liste complète des magasins de données pris en charge par l’activité de copie hello en tant que sources et récepteurs, consultez [prise en charge des magasins de données](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="bde22-265">For a complete list of data stores supported by hello copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="bde22-266">toolearn comment toouse données pris en charge spécifiques stocker en tant que source/récepteur, cliquez sur lien hello dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="bde22-266">toolearn how toouse a specific supported data store as a source/sink, click hello link in hello table.</span></span>  
     
    <span data-ttu-id="bde22-267">Remplacez la valeur hello hello **Démarrer** propriété hello jour actuel et **fin** valeur avec hello jour suivant.</span><span class="sxs-lookup"><span data-stu-id="bde22-267">Replace hello value of hello **start** property with hello current day and **end** value with hello next day.</span></span> <span data-ttu-id="bde22-268">Vous pouvez spécifier qu’une partie date hello et ignorer la partie heure hello hello date heure.</span><span class="sxs-lookup"><span data-stu-id="bde22-268">You can specify only hello date part and skip hello time part of hello date time.</span></span> <span data-ttu-id="bde22-269">Par exemple, « 2016-02-03 », qui est l’équivalent trop « 2016-02-03T00:00:00Z »</span><span class="sxs-lookup"><span data-stu-id="bde22-269">For example, "2016-02-03", which is equivalent too"2016-02-03T00:00:00Z"</span></span>
     
    <span data-ttu-id="bde22-270">Les dates/heures de début et de fin doivent toutes deux être au [format ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="bde22-270">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="bde22-271">Par exemple : 2016-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="bde22-271">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="bde22-272">Hello **fin** temps est facultatif, mais nous l’utilisons dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="bde22-272">hello **end** time is optional, but we use it in this tutorial.</span></span> 
     
    <span data-ttu-id="bde22-273">Si vous ne spécifiez pas de valeur pour hello **fin** propriété, il est calculé en tant que «**start + 48 heures**».</span><span class="sxs-lookup"><span data-stu-id="bde22-273">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="bde22-274">pipeline de hello toorun indéfiniment, spécifiez **9999-09-09** en tant que valeur hello pour hello **fin** propriété.</span><span class="sxs-lookup"><span data-stu-id="bde22-274">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span>
     
    <span data-ttu-id="bde22-275">Hello précédent exemple, sont des tranches de données 24 comme chaque tranche de données est généré toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="bde22-275">In hello preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

    <span data-ttu-id="bde22-276">Pour obtenir une description des propriétés JSON dans une définition de pipeline, consultez l’article [Créer des pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="bde22-276">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="bde22-277">Pour obtenir une description des propriétés JSON dans une définition d’activité de copie, consultez [Activités de déplacement des données](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="bde22-277">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="bde22-278">Pour obtenir une description des propriétés JSON prises en charge par BlobSource, consultez l’article [Connecteur de stockage Blob Azure](data-factory-azure-blob-connector.md).</span><span class="sxs-lookup"><span data-stu-id="bde22-278">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="bde22-279">Pour obtenir une description des propriétés JSON prises en charge par SqlSink, consultez l’article [Azure SQL Database connector](data-factory-azure-sql-connector.md) (Connecteur de base de données SQL Azure).</span><span class="sxs-lookup"><span data-stu-id="bde22-279">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>

## <a name="publishdeploy-data-factory-entities"></a><span data-ttu-id="bde22-280">Publier/déployer des entités Data Factory</span><span class="sxs-lookup"><span data-stu-id="bde22-280">Publish/deploy Data Factory entities</span></span>
<span data-ttu-id="bde22-281">Dans cette étape, vous publiez les entités Data Factory (services liés, jeux de données et pipeline) que vous avez créées précédemment.</span><span class="sxs-lookup"><span data-stu-id="bde22-281">In this step, you publish Data Factory entities (linked services, datasets, and pipeline) you created earlier.</span></span> <span data-ttu-id="bde22-282">Vous spécifiez également le nom hello de hello nouvelles données fabrique toobe créé toohold ces entités.</span><span class="sxs-lookup"><span data-stu-id="bde22-282">You also specify hello name of hello new data factory toobe created toohold these entities.</span></span>  

1. <span data-ttu-id="bde22-283">Cliquez sur le projet dans l’Explorateur de solutions de hello, puis cliquez sur **publier**.</span><span class="sxs-lookup"><span data-stu-id="bde22-283">Right-click project in hello Solution Explorer, and click **Publish**.</span></span> 
2. <span data-ttu-id="bde22-284">Si vous voyez **connecter tooyour compte Microsoft** boîte de dialogue, entrez vos informations d’identification de compte hello qui dispose d’abonnement Azure, puis cliquez sur **connectez-vous**.</span><span class="sxs-lookup"><span data-stu-id="bde22-284">If you see **Sign in tooyour Microsoft account** dialog box, enter your credentials for hello account that has Azure subscription, and click **sign in**.</span></span>
3. <span data-ttu-id="bde22-285">Vous devez voir hello suivant la boîte de dialogue :</span><span class="sxs-lookup"><span data-stu-id="bde22-285">You should see hello following dialog box:</span></span>
   
   ![Boîte de dialogue Publier](./media/data-factory-copy-activity-tutorial-using-visual-studio/publish.png)
4. <span data-ttu-id="bde22-287">Dans la page de fabrique configurer données hello, procédez comme hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="bde22-287">In hello Configure data factory page, do hello following steps:</span></span> 
   
   1. <span data-ttu-id="bde22-288">Sélectionnez l’option **Créer une fabrique de données** .</span><span class="sxs-lookup"><span data-stu-id="bde22-288">select **Create New Data Factory** option.</span></span>
   2. <span data-ttu-id="bde22-289">Saisissez **VSTutorialFactory** dans le champ **Nom**.</span><span class="sxs-lookup"><span data-stu-id="bde22-289">Enter **VSTutorialFactory** for **Name**.</span></span>  
      
      > [!IMPORTANT]
      > <span data-ttu-id="bde22-290">nom de Hello de fabrique de données Azure hello doit être globalement unique.</span><span class="sxs-lookup"><span data-stu-id="bde22-290">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="bde22-291">Si vous recevez une erreur sur le nom hello de fabrique de données lors de la publication, modifiez le nom hello de fabrique de données hello (par exemple, yournameVSTutorialFactory) et essayez de publier à nouveau.</span><span class="sxs-lookup"><span data-stu-id="bde22-291">If you receive an error about hello name of data factory when publishing, change hello name of hello data factory (for example, yournameVSTutorialFactory) and try publishing again.</span></span> <span data-ttu-id="bde22-292">Consultez la rubrique [Data Factory - Règles d'affectation des noms](data-factory-naming-rules.md) pour savoir comment nommer les artefacts Data Factory.</span><span class="sxs-lookup"><span data-stu-id="bde22-292">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>        
      > 
      > 
   3. <span data-ttu-id="bde22-293">Sélectionnez votre abonnement Azure pour hello **abonnement** champ.</span><span class="sxs-lookup"><span data-stu-id="bde22-293">Select your Azure subscription for hello **Subscription** field.</span></span>
      
      > [!IMPORTANT]
      > <span data-ttu-id="bde22-294">Si vous ne voyez pas d’un abonnement, assurez-vous que vous connecté en utilisant un compte qui est administrateur ou coadministrateur de l’abonnement de hello.</span><span class="sxs-lookup"><span data-stu-id="bde22-294">If you do not see any subscription, ensure that you logged in using an account that is an admin or co-admin of hello subscription.</span></span>  
      > 
      > 
   4. <span data-ttu-id="bde22-295">Sélectionnez hello **groupe de ressources** pour toobe de fabrique de données hello créé.</span><span class="sxs-lookup"><span data-stu-id="bde22-295">Select hello **resource group** for hello data factory toobe created.</span></span> 
   5. <span data-ttu-id="bde22-296">Sélectionnez hello **région** de fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="bde22-296">Select hello **region** for hello data factory.</span></span> <span data-ttu-id="bde22-297">Seules les régions pris en charge par hello service Data Factory sont affichées dans la liste déroulante de hello.</span><span class="sxs-lookup"><span data-stu-id="bde22-297">Only regions supported by hello Data Factory service are shown in hello drop-down list.</span></span>
   6. <span data-ttu-id="bde22-298">Cliquez sur **suivant** tooswitch toohello **publier des éléments** page.</span><span class="sxs-lookup"><span data-stu-id="bde22-298">Click **Next** tooswitch toohello **Publish Items** page.</span></span>
      
       ![Page Configurer une fabrique de données](media/data-factory-copy-activity-tutorial-using-visual-studio/configure-data-factory-page.png)   
5. <span data-ttu-id="bde22-300">Bonjour **publier des éléments** , vérifiez que tous les hello fabriques de données entités sont sélectionnées, puis cliquez sur **suivant** tooswitch toohello **Résumé** page.</span><span class="sxs-lookup"><span data-stu-id="bde22-300">In hello **Publish Items** page, ensure that all hello Data Factories entities are selected, and click **Next** tooswitch toohello **Summary** page.</span></span>
   
   ![Page Publier des éléments](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-items-page.png)     
6. <span data-ttu-id="bde22-302">Passez en revue la synthèse de hello et cliquez sur **suivant** toostart Bonjour déploiement processus et vue Bonjour **état du déploiement**.</span><span class="sxs-lookup"><span data-stu-id="bde22-302">Review hello summary and click **Next** toostart hello deployment process and view hello **Deployment Status**.</span></span>
   
   ![Page Résumé de la publication](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-summary-page.png)
7. <span data-ttu-id="bde22-304">Bonjour **état du déploiement** page, vous devez voir État hello hello du processus de déploiement.</span><span class="sxs-lookup"><span data-stu-id="bde22-304">In hello **Deployment Status** page, you should see hello status of hello deployment process.</span></span> <span data-ttu-id="bde22-305">Après le déploiement de hello, cliquez sur Terminer.</span><span class="sxs-lookup"><span data-stu-id="bde22-305">Click Finish after hello deployment is done.</span></span>
 
   ![Page État du déploiement](media/data-factory-copy-activity-tutorial-using-visual-studio/deployment-status.png)

<span data-ttu-id="bde22-307">Hello Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="bde22-307">Note hello following points:</span></span> 

* <span data-ttu-id="bde22-308">Si vous recevez une erreur de hello : « cet abonnement n’est pas inscrit toouse, espace de noms Microsoft.DataFactory », effectuez l’une des manières suivantes les hello et essayez de publier à nouveau :</span><span class="sxs-lookup"><span data-stu-id="bde22-308">If you receive hello error: "This subscription is not registered toouse namespace Microsoft.DataFactory", do one of hello following and try publishing again:</span></span> 
  
  * <span data-ttu-id="bde22-309">Dans Azure PowerShell, exécutez hello suivant le fournisseur de commandes tooregister hello Data Factory.</span><span class="sxs-lookup"><span data-stu-id="bde22-309">In Azure PowerShell, run hello following command tooregister hello Data Factory provider.</span></span> 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    <span data-ttu-id="bde22-310">Vous pouvez exécuter hello suivant commande tooconfirm ce fournisseur est inscrit de fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="bde22-310">You can run hello following command tooconfirm that hello Data Factory provider is registered.</span></span> 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="bde22-311">Connexion à l’aide de hello abonnement Azure dans hello [portail Azure](https://portal.azure.com) et accédez Panneau de Data Factory tooa (ou) créer une fabrique de données Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="bde22-311">Login using hello Azure subscription into hello [Azure portal](https://portal.azure.com) and navigate tooa Data Factory blade (or) create a data factory in hello Azure portal.</span></span> <span data-ttu-id="bde22-312">Cette action enregistre automatiquement le fournisseur hello pour vous.</span><span class="sxs-lookup"><span data-stu-id="bde22-312">This action automatically registers hello provider for you.</span></span>
* <span data-ttu-id="bde22-313">nom Hello hello fabrique de données peut être enregistré comme un nom DNS dans hello futures et donc devenir visible publiquement.</span><span class="sxs-lookup"><span data-stu-id="bde22-313">hello name of hello data factory may be registered as a DNS name in hello future and hence become publically visible.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bde22-314">instances de fabrique de données toocreate, vous devez toobe une administration/co-admin Hello abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="bde22-314">toocreate Data Factory instances, you need toobe a admin/co-admin of hello Azure subscription</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="bde22-315">Surveillance d’un pipeline</span><span class="sxs-lookup"><span data-stu-id="bde22-315">Monitor pipeline</span></span>
<span data-ttu-id="bde22-316">Accédez toohello page d’accueil de votre fabrique de données :</span><span class="sxs-lookup"><span data-stu-id="bde22-316">Navigate toohello home page for your data factory:</span></span>

1. <span data-ttu-id="bde22-317">Connectez-vous trop[portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bde22-317">Log in too[Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="bde22-318">Cliquez sur **davantage de services** sur hello du menu de gauche, puis cliquez sur **fabriques de données**.</span><span class="sxs-lookup"><span data-stu-id="bde22-318">Click **More services** on hello left menu, and click **Data factories**.</span></span>

    ![Parcourir les fabriques de données](media/data-factory-copy-activity-tutorial-using-visual-studio/browse-data-factories.png)
3. <span data-ttu-id="bde22-320">Commencez à taper le nom hello votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="bde22-320">Start typing hello name of your data factory.</span></span>

    ![Nom de la fabrique de données](media/data-factory-copy-activity-tutorial-using-visual-studio/enter-data-factory-name.png) 
4. <span data-ttu-id="bde22-322">Cliquez sur votre data factory dans hello résultats liste toosee hello page d’accueil de votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="bde22-322">Click your data factory in hello results list toosee hello home page for your data factory.</span></span>

    ![Page d'accueil Data Factory](media/data-factory-copy-activity-tutorial-using-visual-studio/data-factory-home-page.png)
5. <span data-ttu-id="bde22-324">Suivez les instructions à partir de [analyser des jeux de données et le pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) pipeline de hello toomonitor et jeux de données que vous avez créé dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="bde22-324">Follow instructions from [Monitor datasets and pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) toomonitor hello pipeline and datasets you have created in this tutorial.</span></span> <span data-ttu-id="bde22-325">Pour le moment, Visual Studio ne prend pas en charge la surveillance des pipelines Data Factory.</span><span class="sxs-lookup"><span data-stu-id="bde22-325">Currently, Visual Studio does not support monitoring Data Factory pipelines.</span></span> 

## <a name="summary"></a><span data-ttu-id="bde22-326">Résumé</span><span class="sxs-lookup"><span data-stu-id="bde22-326">Summary</span></span>
<span data-ttu-id="bde22-327">Dans ce didacticiel, vous avez créé un Azure data factory toocopy de données à partir d’une base de données SQL Azure de tooan objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="bde22-327">In this tutorial, you created an Azure data factory toocopy data from an Azure blob tooan Azure SQL database.</span></span> <span data-ttu-id="bde22-328">Vous avez utilisé Visual Studio toocreate hello fabrique de données, les services liés, des groupes de données et un pipeline.</span><span class="sxs-lookup"><span data-stu-id="bde22-328">You used Visual Studio toocreate hello data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="bde22-329">Voici les étapes principales hello que vous avez effectuées dans ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="bde22-329">Here are hello high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="bde22-330">Création d’une **fabrique de données**Azure.</span><span class="sxs-lookup"><span data-stu-id="bde22-330">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="bde22-331">Création de **services liés**:</span><span class="sxs-lookup"><span data-stu-id="bde22-331">Created **linked services**:</span></span>
   1. <span data-ttu-id="bde22-332">Un **Azure Storage** lié service toolink votre compte de stockage Azure qui contient les données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="bde22-332">An **Azure Storage** linked service toolink your Azure Storage account that holds input data.</span></span>     
   2. <span data-ttu-id="bde22-333">Un **SQL Azure** lié service toolink votre base de données SQL Azure qui contient les données de sortie hello.</span><span class="sxs-lookup"><span data-stu-id="bde22-333">An **Azure SQL** linked service toolink your Azure SQL database that holds hello output data.</span></span> 
3. <span data-ttu-id="bde22-334">Création des **jeux de données**qui décrivent les données d’entrée et de sortie des pipelines.</span><span class="sxs-lookup"><span data-stu-id="bde22-334">Created **datasets**, which describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="bde22-335">Création d’un **pipeline** avec une **activité de copie** avec **BlobSource** en tant que source et **SqlSink** en tant que récepteur.</span><span class="sxs-lookup"><span data-stu-id="bde22-335">Created a **pipeline** with a **Copy Activity** with **BlobSource** as source and **SqlSink** as sink.</span></span> 

<span data-ttu-id="bde22-336">toosee toouse une activité de la ruche HDInsight tootransform des données avec cluster Azure HDInsight, voir [ didacticiel : créer vos premières données tootransform de pipeline à l’aide de cluster Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="bde22-336">toosee how toouse a HDInsight Hive Activity tootransform data by using Azure HDInsight cluster, see [ Tutorial: Build your first pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

<span data-ttu-id="bde22-337">Vous pouvez chaîner les deux activités (exécutée une activité après l’autre) en définissant le dataset de sortie hello d’une activité hello d’entrée dataset Hello autre activité.</span><span class="sxs-lookup"><span data-stu-id="bde22-337">You can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="bde22-338">Pour plus d’informations, voir [Planification et exécution dans Data Factory](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="bde22-338">See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.</span></span> 

## <a name="view-all-data-factories-in-server-explorer"></a><span data-ttu-id="bde22-339">Afficher toutes les fabriques de données dans l’Explorateur de serveurs</span><span class="sxs-lookup"><span data-stu-id="bde22-339">View all data factories in Server Explorer</span></span>
<span data-ttu-id="bde22-340">Cette section décrit comment toouse hello de l’Explorateur de serveurs dans Visual Studio tooview toutes les fabriques de données hello dans votre abonnement Azure et comment créer un projet Visual Studio basé sur une fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="bde22-340">This section describes how toouse hello Server Explorer in Visual Studio tooview all hello data factories in your Azure subscription and create a Visual Studio project based on an existing data factory.</span></span> 

1. <span data-ttu-id="bde22-341">Dans **Visual Studio**, cliquez sur **vue** hello menu et cliquez sur **l’Explorateur de serveurs**.</span><span class="sxs-lookup"><span data-stu-id="bde22-341">In **Visual Studio**, click **View** on hello menu, and click **Server Explorer**.</span></span>
2. <span data-ttu-id="bde22-342">Dans la fenêtre de l’Explorateur de serveurs hello, développez **Azure** et développez **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="bde22-342">In hello Server Explorer window, expand **Azure** and expand **Data Factory**.</span></span> <span data-ttu-id="bde22-343">Si vous voyez **connecter tooVisual Studio**, entrez hello **compte** associé à votre abonnement Azure et d’un clic **continuer**.</span><span class="sxs-lookup"><span data-stu-id="bde22-343">If you see **Sign in tooVisual Studio**, enter hello **account** associated with your Azure subscription and click **Continue**.</span></span> <span data-ttu-id="bde22-344">Saisissez le **mot de passe**, puis cliquez sur **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="bde22-344">Enter **password**, and click **Sign in**.</span></span> <span data-ttu-id="bde22-345">Visual Studio essaie de tooget d’informations sur toutes les fabriques de données Azure dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="bde22-345">Visual Studio tries tooget information about all Azure data factories in your subscription.</span></span> <span data-ttu-id="bde22-346">Vous voyez l’état hello de cette opération Bonjour **liste des tâches données fabrique** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="bde22-346">You see hello status of this operation in hello **Data Factory Task List** window.</span></span>

    ![Explorateur de serveurs](./media/data-factory-copy-activity-tutorial-using-visual-studio/server-explorer.png)

## <a name="create-a-visual-studio-project-for-an-existing-data-factory"></a><span data-ttu-id="bde22-348">Créer un projet Visual Studio pour une fabrique de données existante</span><span class="sxs-lookup"><span data-stu-id="bde22-348">Create a Visual Studio project for an existing data factory</span></span>

- <span data-ttu-id="bde22-349">Avec le bouton droit une fabrique de données dans l’Explorateur de serveurs, puis sélectionnez **tooNew d’exporter la fabrique de données projet** toocreate un projet Visual Studio basé sur une fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="bde22-349">Right-click a data factory in Server Explorer, and select **Export Data Factory tooNew Project** toocreate a Visual Studio project based on an existing data factory.</span></span>

    ![Projet VS tooa exportation data factory](./media/data-factory-copy-activity-tutorial-using-visual-studio/export-data-factory-menu.png)  

## <a name="update-data-factory-tools-for-visual-studio"></a><span data-ttu-id="bde22-351">Mettre à jour des outils Data Factory pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bde22-351">Update Data Factory tools for Visual Studio</span></span>
<span data-ttu-id="bde22-352">outils d’Azure Data Factory tooupdate pour Visual Studio, procédez comme hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="bde22-352">tooupdate Azure Data Factory tools for Visual Studio, do hello following steps:</span></span>

1. <span data-ttu-id="bde22-353">Cliquez sur **outils** sur hello menu et sélectionnez **Extensions et mises à jour**.</span><span class="sxs-lookup"><span data-stu-id="bde22-353">Click **Tools** on hello menu and select **Extensions and Updates**.</span></span> 
2. <span data-ttu-id="bde22-354">Sélectionnez **mises à jour** dans hello du volet gauche, puis sélectionnez **galerie Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="bde22-354">Select **Updates** in hello left pane and then select **Visual Studio Gallery**.</span></span>
3. <span data-ttu-id="bde22-355">Sélectionnez **Outils Azure Data Factory pour Visual Studio**, puis cliquez sur **Mettre à jour**.</span><span class="sxs-lookup"><span data-stu-id="bde22-355">Select **Azure Data Factory tools for Visual Studio** and click **Update**.</span></span> <span data-ttu-id="bde22-356">Si vous ne voyez pas cette entrée, vous avez déjà la version la plus récente des outils de hello hello.</span><span class="sxs-lookup"><span data-stu-id="bde22-356">If you do not see this entry, you already have hello latest version of hello tools.</span></span> 

## <a name="use-configuration-files"></a><span data-ttu-id="bde22-357">Utiliser des fichiers de configuration</span><span class="sxs-lookup"><span data-stu-id="bde22-357">Use configuration files</span></span>
<span data-ttu-id="bde22-358">Vous pouvez utiliser des fichiers de configuration dans les propriétés de tooconfigure Visual Studio pour les services/tables/pipelines liés différemment pour chaque environnement.</span><span class="sxs-lookup"><span data-stu-id="bde22-358">You can use configuration files in Visual Studio tooconfigure properties for linked services/tables/pipelines differently for each environment.</span></span>

<span data-ttu-id="bde22-359">Envisagez de hello définition JSON pour un service lié Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="bde22-359">Consider hello following JSON definition for an Azure Storage linked service.</span></span> <span data-ttu-id="bde22-360">toospecify **connectionString** avec des valeurs différentes pour accountname et accountkey selon hello environnement (développement/Test/Production) toowhich vous déployez des entités de fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="bde22-360">toospecify **connectionString** with different values for accountname and accountkey based on hello environment (Dev/Test/Production) toowhich you are deploying Data Factory entities.</span></span> <span data-ttu-id="bde22-361">Vous pouvez parvenir à ce comportement en utilisant un fichier de configuration distinct pour chaque environnement.</span><span class="sxs-lookup"><span data-stu-id="bde22-361">You can achieve this behavior by using separate configuration file for each environment.</span></span>

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

### <a name="add-a-configuration-file"></a><span data-ttu-id="bde22-362">Ajouter un fichier de configuration</span><span class="sxs-lookup"><span data-stu-id="bde22-362">Add a configuration file</span></span>
<span data-ttu-id="bde22-363">Ajoutez un fichier de configuration pour chaque environnement en effectuant hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="bde22-363">Add a configuration file for each environment by performing hello following steps:</span></span>   

1. <span data-ttu-id="bde22-364">Cliquez sur le projet de Data Factory hello dans votre solution Visual Studio, pointez trop**ajouter**, puis cliquez sur **un nouvel élément**.</span><span class="sxs-lookup"><span data-stu-id="bde22-364">Right-click hello Data Factory project in your Visual Studio solution, point too**Add**, and click **New item**.</span></span>
2. <span data-ttu-id="bde22-365">Sélectionnez **Config** à partir de la liste hello de modèles installés sur hello gauche, sélectionnez **fichier de Configuration**, entrez un **nom** pour la configuration de hello fichier, puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="bde22-365">Select **Config** from hello list of installed templates on hello left, select **Configuration File**, enter a **name** for hello configuration file, and click **Add**.</span></span>

    ![Ajouter un fichier de configuration](./media/data-factory-build-your-first-pipeline-using-vs/add-config-file.png)
3. <span data-ttu-id="bde22-367">Ajouter des paramètres de configuration et leurs valeurs Bonjour suivant le format :</span><span class="sxs-lookup"><span data-stu-id="bde22-367">Add configuration parameters and their values in hello following format:</span></span>

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

    <span data-ttu-id="bde22-368">Cet exemple configure la propriété connectionString d’un service lié Azure Storage et d’un service lié SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="bde22-368">This example configures connectionString property of an Azure Storage linked service and an Azure SQL linked service.</span></span> <span data-ttu-id="bde22-369">Notez que la syntaxe de hello pour spécifier un nom est [JsonPath](http://goessner.net/articles/JsonPath/).</span><span class="sxs-lookup"><span data-stu-id="bde22-369">Notice that hello syntax for specifying name is [JsonPath](http://goessner.net/articles/JsonPath/).</span></span>   

    <span data-ttu-id="bde22-370">Si JSON possède une propriété qui a un tableau de valeurs comme indiqué dans hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="bde22-370">If JSON has a property that has an array of values as shown in hello following code:</span></span>  

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

    <span data-ttu-id="bde22-371">Configurez les propriétés comme indiqué dans hello suivant du fichier de configuration (Utilisez zéro) :</span><span class="sxs-lookup"><span data-stu-id="bde22-371">Configure properties as shown in hello following configuration file (use zero-based indexing):</span></span>

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

### <a name="property-names-with-spaces"></a><span data-ttu-id="bde22-372">Noms de propriétés avec des espaces</span><span class="sxs-lookup"><span data-stu-id="bde22-372">Property names with spaces</span></span>
<span data-ttu-id="bde22-373">Si un nom de propriété comporte des espaces, utilisez des crochets comme indiqué dans hello (nom du serveur de base de données) de l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="bde22-373">If a property name has spaces in it, use square brackets as shown in hello following example (Database server name):</span></span>

```json
 {
     "name": "$.properties.activities[1].typeProperties.webServiceParameters.['Database server name']",
     "value": "MyAsqlServer.database.windows.net"
 }
```

### <a name="deploy-solution-using-a-configuration"></a><span data-ttu-id="bde22-374">Déployer une solution à l’aide d’une configuration</span><span class="sxs-lookup"><span data-stu-id="bde22-374">Deploy solution using a configuration</span></span>
<span data-ttu-id="bde22-375">Lorsque vous publiez des entités d’Azure Data Factory dans Visual Studio, vous pouvez spécifier la configuration hello que vous souhaitez toouse pour cette opération de publication.</span><span class="sxs-lookup"><span data-stu-id="bde22-375">When you are publishing Azure Data Factory entities in VS, you can specify hello configuration that you want toouse for that publishing operation.</span></span>

<span data-ttu-id="bde22-376">entités toopublish dans un projet Azure Data Factory à l’aide du fichier de configuration :</span><span class="sxs-lookup"><span data-stu-id="bde22-376">toopublish entities in an Azure Data Factory project using configuration file:</span></span>   

1. <span data-ttu-id="bde22-377">Cliquez sur le projet de la fabrique de données, sur **publier** toosee hello **publier des éléments** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="bde22-377">Right-click Data Factory project and click **Publish** toosee hello **Publish Items** dialog box.</span></span>
2. <span data-ttu-id="bde22-378">Sélectionnez une fabrique de données existante ou de spécifier des valeurs pour la création d’une fabrique de données sur hello **fabrique de données de configuration** page, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="bde22-378">Select an existing data factory or specify values for creating a data factory on hello **Configure data factory** page, and click **Next**.</span></span>   
3. <span data-ttu-id="bde22-379">Sur hello **publier des éléments** page : une liste déroulante avec les configurations disponibles pour hello **sélectionner une configuration de déploiement** champ.</span><span class="sxs-lookup"><span data-stu-id="bde22-379">On hello **Publish Items** page: you see a drop-down list with available configurations for hello **Select Deployment Config** field.</span></span>

    ![Sélectionner un fichier de config](./media/data-factory-build-your-first-pipeline-using-vs/select-config-file.png)
4. <span data-ttu-id="bde22-381">Sélectionnez hello **fichier de configuration** que vous souhaitez toouse et cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="bde22-381">Select hello **configuration file** that you would like toouse and click **Next**.</span></span>
5. <span data-ttu-id="bde22-382">Vérifiez que vous voyez le nom hello du fichier JSON Bonjour **Résumé** page, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="bde22-382">Confirm that you see hello name of JSON file in hello **Summary** page and click **Next**.</span></span>
6. <span data-ttu-id="bde22-383">Cliquez sur **Terminer** une fois l’opération de déploiement hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="bde22-383">Click **Finish** after hello deployment operation is finished.</span></span>

<span data-ttu-id="bde22-384">Lorsque vous déployez, hello valeurs hello fichier de configuration sont tooset utilisé les valeurs des propriétés dans les fichiers au format JSON hello avant que les entités hello soient déployé tooAzure service Data Factory.</span><span class="sxs-lookup"><span data-stu-id="bde22-384">When you deploy, hello values from hello configuration file are used tooset values for properties in hello JSON files before hello entities are deployed tooAzure Data Factory service.</span></span>   

## <a name="use-azure-key-vault"></a><span data-ttu-id="bde22-385">Utiliser Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="bde22-385">Use Azure Key Vault</span></span>
<span data-ttu-id="bde22-386">Il n’est pas recommandé et souvent sur des données sensibles de sécurité stratégie toocommit comme référentiel de code de connexion chaînes toohello.</span><span class="sxs-lookup"><span data-stu-id="bde22-386">It is not advisable and often against security policy toocommit sensitive data such as connection strings toohello code repository.</span></span> <span data-ttu-id="bde22-387">Consultez [ADF Secure publier](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) sample sur toolearn GitHub sur le stockage des informations sensibles dans Azure Key Vault et son utilisation lors de la publication des entités de fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="bde22-387">See [ADF Secure Publish](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) sample on GitHub toolearn about storing sensitive information in Azure Key Vault and using it while publishing Data Factory entities.</span></span> <span data-ttu-id="bde22-388">Hello Secure publier l’extension pour Visual Studio permet hello toobe de clés secrètes stockée dans le coffre de clés et uniquement les références toothem sont spécifiés dans les services liés / configurations de déploiement.</span><span class="sxs-lookup"><span data-stu-id="bde22-388">hello Secure Publish extension for Visual Studio allows hello secrets toobe stored in Key Vault and only references toothem are specified in linked services/ deployment configurations.</span></span> <span data-ttu-id="bde22-389">Ces références sont résolues lors de la publication tooAzure des entités de fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="bde22-389">These references are resolved when you publish Data Factory entities tooAzure.</span></span> <span data-ttu-id="bde22-390">Ces fichiers peuvent ensuite être référentiel toosource validée sans exposer les clés secrètes.</span><span class="sxs-lookup"><span data-stu-id="bde22-390">These files can then be committed toosource repository without exposing any secrets.</span></span>


## <a name="next-steps"></a><span data-ttu-id="bde22-391">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bde22-391">Next steps</span></span>
<span data-ttu-id="bde22-392">Dans ce didacticiel, vous avez utilisé le stockage Blob Azure comme magasin de données source et une base de données SQL Azure comme banque de données de destination dans une opération de copie.</span><span class="sxs-lookup"><span data-stu-id="bde22-392">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="bde22-393">Hello tableau suivant fournit une liste de banques de données pris en charge en tant que sources et destinations par l’activité de copie hello :</span><span class="sxs-lookup"><span data-stu-id="bde22-393">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="bde22-394">toolearn sur la banque de données de toocopy vers/à partir de données, cliquez sur lien hello hello magasin de données dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="bde22-394">toolearn about how toocopy data to/from a data store, click hello link for hello data store in hello table.</span></span>
