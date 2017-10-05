---
title: "Créer votre première fabrique de données Azure (portail Azure) | Microsoft Docs"
description: "Dans ce didacticiel, vous créez un exemple de pipeline Azure Data Factory à l’aide de Data Factory Editor dans le portail Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: d5b14e9e-e358-45be-943c-5297435d402d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 9c958aecb841fa02349c6b9e5e1984f6ba4fb611
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-portal"></a><span data-ttu-id="dc7c7-103">Didacticiel : Créer votre première fabrique de données Azure à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="dc7c7-103">Tutorial: Build your first Azure data factory using Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="dc7c7-104">Vue d’ensemble et étapes préalables requises</span><span class="sxs-lookup"><span data-stu-id="dc7c7-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="dc7c7-105">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="dc7c7-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="dc7c7-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="dc7c7-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="dc7c7-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dc7c7-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="dc7c7-108">Modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="dc7c7-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="dc7c7-109">API REST</span><span class="sxs-lookup"><span data-stu-id="dc7c7-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)


<span data-ttu-id="dc7c7-110">Dans cet article, vous allez utiliser le [portail Azure](https://portal.azure.com/) pour créer votre première fabrique de données Azure.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-110">In this article, you learn how to use [Azure portal](https://portal.azure.com/) to create your first Azure data factory.</span></span> <span data-ttu-id="dc7c7-111">Pour suivre le didacticiel avec d’autres outils/Kits de développement logiciel (SDK), sélectionnez une des options dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-111">To do the tutorial using other tools/SDKs, select one of the options from the drop-down list.</span></span> 

<span data-ttu-id="dc7c7-112">Le pipeline dans ce didacticiel a une activité : **Activité HDInsight Hive**.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-112">The pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="dc7c7-113">Cette activité exécute un script Hive sur un cluster HDInsight qui transforme des données d’entrée pour produire des données de sortie.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data to produce output data.</span></span> <span data-ttu-id="dc7c7-114">Le pipeline est programmé pour s’exécuter une fois par mois entre les heures de début et de fin spécifiées.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-114">The pipeline is scheduled to run once a month between the specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="dc7c7-115">Dans ce didacticiel, le pipeline de données transforme les données d’entrée pour produire des données de sortie.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-115">The data pipeline in this tutorial transforms input data to produce output data.</span></span> <span data-ttu-id="dc7c7-116">Pour un didacticiel sur la copie de données à l’aide d’Azure Data Factory, consultez [Copie de données Blob Storage vers une base de données SQL à l’aide de Data Factory](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="dc7c7-116">For a tutorial on how to copy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="dc7c7-117">Un pipeline peut contenir plusieurs activités.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-117">A pipeline can have more than one activity.</span></span> <span data-ttu-id="dc7c7-118">En outre, vous pouvez chaîner deux activités (une après l’autre) en configurant le jeu de données de sortie d’une activité en tant que jeu de données d’entrée de l’autre activité.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-118">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="dc7c7-119">Pour plus d’informations, consultez [Planification et exécution dans Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="dc7c7-119">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dc7c7-120">Composants requis</span><span class="sxs-lookup"><span data-stu-id="dc7c7-120">Prerequisites</span></span>
1. <span data-ttu-id="dc7c7-121">Lisez l’article [Vue d’ensemble du didacticiel](data-factory-build-your-first-pipeline.md) et effectuez les **étapes préalables requises** .</span><span class="sxs-lookup"><span data-stu-id="dc7c7-121">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete the **prerequisite** steps.</span></span>
2. <span data-ttu-id="dc7c7-122">Cet article ne fournit pas de vue d’ensemble conceptuelle du service Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-122">This article does not provide a conceptual overview of the Azure Data Factory service.</span></span> <span data-ttu-id="dc7c7-123">Nous vous recommandons de lire l’article [Introduction à Azure Data Factory](data-factory-introduction.md) pour une présentation détaillée du service.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-123">We recommend that you go through [Introduction to Azure Data Factory](data-factory-introduction.md) article for a detailed overview of the service.</span></span>  

## <a name="create-data-factory"></a><span data-ttu-id="dc7c7-124">Créer une fabrique de données</span><span class="sxs-lookup"><span data-stu-id="dc7c7-124">Create data factory</span></span>
<span data-ttu-id="dc7c7-125">Une fabrique de données peut avoir un ou plusieurs pipelines.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-125">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="dc7c7-126">Un pipeline peut contenir une ou plusieurs activités.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-126">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="dc7c7-127">Par exemple, une activité de copie pour copier des données d’une source vers un magasin de données de destination, et une activité Hive HDInsight pour exécuter un script Hive pour transformer des données d’entrée et produire des données de sortie.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-127">For example, a Copy Activity to copy data from a source to a destination data store and a HDInsight Hive activity to run a Hive script to transform input data to product output data.</span></span> <span data-ttu-id="dc7c7-128">Commençons par la création de la fabrique de données dans cette étape.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-128">Let's start with creating the data factory in this step.</span></span>

1. <span data-ttu-id="dc7c7-129">Connectez-vous au [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="dc7c7-129">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="dc7c7-130">Cliquez sur **NOUVEAU** dans le menu de gauche, puis sur **Données et analyse** et sur **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-130">Click **NEW** on the left menu, click **Data + Analytics**, and click **Data Factory**.</span></span>

   ![Panneau Créer](./media/data-factory-build-your-first-pipeline-using-editor/create-blade.png)
3. <span data-ttu-id="dc7c7-132">Dans le panneau **Nouvelle fabrique de données**, entrez **GetStartedDF** dans le champ Nom.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-132">In the **New data factory** blade, enter **GetStartedDF** for the Name.</span></span>

   ![Panneau Nouvelle fabrique de données](./media/data-factory-build-your-first-pipeline-using-editor/new-data-factory-blade.png)

   > [!IMPORTANT]
   > <span data-ttu-id="dc7c7-134">Le nom de la fabrique de données Azure doit être un nom **global unique**.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-134">The name of the Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="dc7c7-135">Si vous recevez l’erreur : **Le nom de fabrique de données « GetStartedDF » n’est pas disponible**.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-135">If you receive the error: **Data factory name “GetStartedDF” is not available**.</span></span> <span data-ttu-id="dc7c7-136">Modifiez le nom de la fabrique de données (par exemple, votrenomGetStartedDF) et réessayez.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-136">Change the name of the data factory (for example, yournameGetStartedDF) and try creating again.</span></span> <span data-ttu-id="dc7c7-137">Consultez la rubrique [Data Factory - Règles d'affectation des noms](data-factory-naming-rules.md) pour savoir comment nommer les artefacts Data Factory.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-137">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
   >
   > <span data-ttu-id="dc7c7-138">Le nom de la fabrique de données pourra être enregistré en tant que nom **DNS** et devenir ainsi visible publiquement.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-138">The name of the data factory may be registered as a **DNS** name in the future and hence become publically visible.</span></span>
   >
   >
4. <span data-ttu-id="dc7c7-139">Sélectionnez l’ **abonnement Azure** où vous voulez que la fabrique de données soit créée.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-139">Select the **Azure subscription** where you want the data factory to be created.</span></span>
5. <span data-ttu-id="dc7c7-140">Sélectionnez un **groupe de ressources** existant ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-140">Select existing **resource group** or create a resource group.</span></span> <span data-ttu-id="dc7c7-141">Pour les besoins de ce didacticiel, créez un groupe de ressources nommé : **ADFGetStartedRG**.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-141">For the tutorial, create a resource group named: **ADFGetStartedRG**.</span></span>
6. <span data-ttu-id="dc7c7-142">Sélectionnez **l’emplacement** de la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-142">Select the **location** for the data factory.</span></span> <span data-ttu-id="dc7c7-143">Seules les régions prises en charge par le service Data Factory sont affichées dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-143">Only regions supported by the Data Factory service are shown in the drop-down list.</span></span>
7. <span data-ttu-id="dc7c7-144">Sélectionnez **Épingler au tableau de bord**.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-144">Select **Pin to dashboard**.</span></span> 
8. <span data-ttu-id="dc7c7-145">Cliquez sur **Créer** dans le panneau **Nouvelle fabrique de données**.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-145">Click **Create** on the **New data factory** blade.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="dc7c7-146">Pour créer des instances Data Factory, vous devez avoir un rôle de [collaborateur de fabrique de données](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) au niveau de l’abonnement/du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-146">To create Data Factory instances, you must be a member of the [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at the subscription/resource group level.</span></span>
   >
   >
7. <span data-ttu-id="dc7c7-147">Sur le tableau de bord, vous voyez la vignette suivante avec l’état : Déploiement de fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-147">On the dashboard, you see the following tile with status: Deploying data factory.</span></span>    

   ![État de la création de la fabrique de données](./media/data-factory-build-your-first-pipeline-using-editor/creating-data-factory-image.png)
8. <span data-ttu-id="dc7c7-149">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="dc7c7-149">Congratulations!</span></span> <span data-ttu-id="dc7c7-150">Vous avez créé votre première fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-150">You have successfully created your first data factory.</span></span> <span data-ttu-id="dc7c7-151">Une fois la fabrique de données créée, la page correspondante s’affiche et indique son contenu.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-151">After the data factory has been created successfully, you see the data factory page, which shows you the contents of the data factory.</span></span>     

    ![Panneau Data Factory](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-blade.png)

<span data-ttu-id="dc7c7-153">Avant de créer un pipeline dans la fabrique de données, vous devez créer quelques entités Data Factory.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-153">Before creating a pipeline in the data factory, you need to create a few Data Factory entities first.</span></span> <span data-ttu-id="dc7c7-154">Créez d’abord des services liés pour lier des magasins de données/calculs à votre magasin de données, définissez des jeux de données d’entrée et de sortie pour représenter les données d’entrée/sortie dans les magasins de données liés, puis créez le pipeline avec une activité qui utilise ces jeux de données.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-154">You first create linked services to link data stores/computes to your data store, define input and output datasets to represent input/output data in linked data stores, and then create the pipeline with an activity that uses these datasets.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="dc7c7-155">Créer des services liés</span><span class="sxs-lookup"><span data-stu-id="dc7c7-155">Create linked services</span></span>
<span data-ttu-id="dc7c7-156">Dans cette étape, vous liez votre compte Stockage Azure et un cluster Azure HDInsight à la demande à votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-156">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster to your data factory.</span></span> <span data-ttu-id="dc7c7-157">Le compte Stockage Azure contient les données d’entrée et de sortie pour le pipeline de cet exemple.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-157">The Azure Storage account holds the input and output data for the pipeline in this sample.</span></span> <span data-ttu-id="dc7c7-158">Le service lié HDInsight est utilisé pour exécuter le script Hive spécifié dans l’activité du pipeline de cet exemple.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-158">The HDInsight linked service is used to run a Hive script specified in the activity of the pipeline in this sample.</span></span> <span data-ttu-id="dc7c7-159">Identifiez les services de [magasin de données](data-factory-data-movement-activities.md)/[de calcul](data-factory-compute-linked-services.md) qui sont utilisés dans votre scénario et les lier à la fabrique de données en créant des services liés.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-159">Identify what [data store](data-factory-data-movement-activities.md)/[compute services](data-factory-compute-linked-services.md) are used in your scenario and link those services to the data factory by creating linked services.</span></span>  

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="dc7c7-160">Créer le service lié Azure Storage</span><span class="sxs-lookup"><span data-stu-id="dc7c7-160">Create Azure Storage linked service</span></span>
<span data-ttu-id="dc7c7-161">Dans cette étape, vous liez votre compte Stockage Azure à votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-161">In this step, you link your Azure Storage account to your data factory.</span></span> <span data-ttu-id="dc7c7-162">Dans de ce didacticiel, vous utilisez le même compte Stockage Azure pour stocker les données d’entrée/sortie et le fichier de script HQL.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-162">In this tutorial, you use the same Azure Storage account to store input/output data and the HQL script file.</span></span>

1. <span data-ttu-id="dc7c7-163">Cliquez sur **Créer et déployer** dans le panneau **FABRIQUE DE DONNÉES** pour **GetStartedDF**.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-163">Click **Author and deploy** on the **DATA FACTORY** blade for **GetStartedDF**.</span></span> <span data-ttu-id="dc7c7-164">Vous devriez voir l’éditeur Data Factory Editor.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-164">You should see the Data Factory Editor.</span></span>

   ![Vignette Créer et déployer](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-author-deploy.png)
2. <span data-ttu-id="dc7c7-166">Cliquez sur **Nouveau magasin de données** et choisissez **Stockage Azure**.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-166">Click **New data store** and choose **Azure storage**.</span></span>

   ![Nouveau magasin de données - Stockage Azure - menu](./media/data-factory-build-your-first-pipeline-using-editor/new-data-store-azure-storage-menu.png)
3. <span data-ttu-id="dc7c7-168">Le script JSON de création d’un service lié Microsoft Azure Storage doit apparaître dans l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-168">You should see the JSON script for creating an Azure Storage linked service in the editor.</span></span>

   ![Service lié Azure Storage](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. <span data-ttu-id="dc7c7-170">Remplacez **account name** par le nom de votre compte de stockage Azure et **account key** par sa clé d’accès.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-170">Replace **account name** with the name of your Azure storage account and **account key** with the access key of the Azure storage account.</span></span> <span data-ttu-id="dc7c7-171">Pour savoir comment obtenir votre clé d’accès de stockage, reportez-vous aux informations sur l’affichage, la copie et la régénération de clés d’accès de stockage dans [Gérer votre compte de stockage](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="dc7c7-171">To learn how to get your storage access key, see the information about how to view, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
5. <span data-ttu-id="dc7c7-172">Cliquez sur l’option **Déployer** de la barre de commandes pour déployer le service lié.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-172">Click **Deploy** on the command bar to deploy the linked service.</span></span>

    ![Bouton déployer](./media/data-factory-build-your-first-pipeline-using-editor/deploy-button.png)

   <span data-ttu-id="dc7c7-174">Une fois que le service lié est déployé, la fenêtre**Draft-1** doit disparaître tandis que **AzureStorageLinkedService** s’affiche dans l’arborescence sur la gauche.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-174">After the linked service is deployed successfully, the **Draft-1** window should disappear and you see **AzureStorageLinkedService** in the tree view on the left.</span></span>

    ![Service lié au stockage dans le menu](./media/data-factory-build-your-first-pipeline-using-editor/StorageLinkedServiceInTree.png)    

### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="dc7c7-176">Créer le service lié Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="dc7c7-176">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="dc7c7-177">Dans cette étape, vous liez un cluster HDInsight à la demande à votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-177">In this step, you link an on-demand HDInsight cluster to your data factory.</span></span> <span data-ttu-id="dc7c7-178">Le cluster HDInsight est automatiquement créé lors de l’exécution, puis supprimé une fois le traitement effectué et au terme du délai d’inactivité spécifié.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-178">The HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for the specified amount of time.</span></span>

1. <span data-ttu-id="dc7c7-179">Dans **Data Factory Editor**, cliquez sur **... Plus**, puis sur **Nouveau calcul** et sélectionnez **Cluster à la demande HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-179">In the **Data Factory Editor**, click **... More**, click **New compute**, and select **On-demand HDInsight cluster**.</span></span>

    ![Nouveau calcul](./media/data-factory-build-your-first-pipeline-using-editor/new-compute-menu.png)
2. <span data-ttu-id="dc7c7-181">Copiez et collez l’extrait ci-dessous dans la fenêtre **Draft-1** .</span><span class="sxs-lookup"><span data-stu-id="dc7c7-181">Copy and paste the following snippet to the **Draft-1** window.</span></span> <span data-ttu-id="dc7c7-182">L’extrait de code JSON décrit les propriétés permettant de créer le cluster HDInsight à la demande.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-182">The JSON snippet describes the properties that are used to create the HDInsight cluster on-demand.</span></span>

    ```JSON
    {
        "name": "HDInsightOnDemandLinkedService",
        "properties": {
            "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "linkedServiceName": "AzureStorageLinkedService"
            }
        }
    }
    ```

    <span data-ttu-id="dc7c7-183">Le tableau suivant décrit les propriétés JSON utilisées dans l'extrait de code :</span><span class="sxs-lookup"><span data-stu-id="dc7c7-183">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

   | <span data-ttu-id="dc7c7-184">Propriété</span><span class="sxs-lookup"><span data-stu-id="dc7c7-184">Property</span></span> | <span data-ttu-id="dc7c7-185">Description</span><span class="sxs-lookup"><span data-stu-id="dc7c7-185">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="dc7c7-186">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="dc7c7-186">ClusterSize</span></span> |<span data-ttu-id="dc7c7-187">Spécifie la taille du cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-187">Specifies the size of the HDInsight cluster.</span></span> |
   | <span data-ttu-id="dc7c7-188">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="dc7c7-188">TimeToLive</span></span> | <span data-ttu-id="dc7c7-189">Spécifie la durée d’inactivité du cluster HDInsight avant sa suppression.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-189">Specifies that the idle time for the HDInsight cluster, before it is deleted.</span></span> |
   | <span data-ttu-id="dc7c7-190">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="dc7c7-190">linkedServiceName</span></span> | <span data-ttu-id="dc7c7-191">Spécifie le compte de stockage utilisé pour stocker les journaux générés par HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-191">Specifies the storage account that is used to store the logs that are generated by HDInsight.</span></span> |

    <span data-ttu-id="dc7c7-192">Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="dc7c7-192">Note the following points:</span></span>

   * <span data-ttu-id="dc7c7-193">La fabrique de données crée pour vous un cluster HDInsight **Linux** avec le code JSON.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-193">The Data Factory creates a **Linux-based** HDInsight cluster for you with the JSON.</span></span> <span data-ttu-id="dc7c7-194">Pour plus d’informations, voir [Service lié à la demande Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="dc7c7-194">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
   * <span data-ttu-id="dc7c7-195">Vous pouvez utiliser votre **propre cluster HDInsight** au lieu d’utiliser un cluster HDInsight à la demande.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-195">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="dc7c7-196">Pour plus d’informations, voir [Service lié Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="dc7c7-196">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
   * <span data-ttu-id="dc7c7-197">Le cluster HDInsight crée un **conteneur par défaut** dans le stockage d’objets blob que vous avez spécifié dans le JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="dc7c7-197">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (**linkedServiceName**).</span></span> <span data-ttu-id="dc7c7-198">HDInsight ne supprime pas ce conteneur lorsque le cluster est supprimé.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-198">HDInsight does not delete this container when the cluster is deleted.</span></span> <span data-ttu-id="dc7c7-199">Ce comportement est normal.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-199">This behavior is by design.</span></span> <span data-ttu-id="dc7c7-200">Avec le service lié HDInsight disponible à la demande, un cluster HDInsight est créé dès qu’une tranche est traitée, à moins qu’il n’existe un cluster actif (**timeToLive**).</span><span class="sxs-lookup"><span data-stu-id="dc7c7-200">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**).</span></span> <span data-ttu-id="dc7c7-201">Ce cluster est supprimé, une fois le traitement terminé.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-201">The cluster is automatically deleted when the processing is done.</span></span>

       <span data-ttu-id="dc7c7-202">Comme un nombre croissant de tranches sont traitées, vous voyez un grand nombre de conteneurs dans votre stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-202">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="dc7c7-203">Si vous n’en avez pas besoin pour dépanner les travaux, il se peut que vous deviez les supprimer pour réduire les frais de stockage.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-203">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="dc7c7-204">Le nom de ces conteneurs suit un modèle : « **nomdevotrefabriquededonnéesadf**-**nomduservicelié**-horodatage ».</span><span class="sxs-lookup"><span data-stu-id="dc7c7-204">The names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="dc7c7-205">Utilisez des outils tels que [Microsoft Storage Explorer](http://storageexplorer.com/) pour supprimer des conteneurs dans votre stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-205">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span></span>

     <span data-ttu-id="dc7c7-206">Pour plus d’informations, voir [Service lié à la demande Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="dc7c7-206">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
3. <span data-ttu-id="dc7c7-207">Cliquez sur l’option **Déployer** de la barre de commandes pour déployer le service lié.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-207">Click **Deploy** on the command bar to deploy the linked service.</span></span>

    ![Déployer un service lié HDInsight à la demande](./media/data-factory-build-your-first-pipeline-using-editor/ondemand-hdinsight-deploy.png)
4. <span data-ttu-id="dc7c7-209">Confirmez que vous voyez s’afficher à la fois **AzureStorageLinkedService** et **HDInsightOnDemandLinkedService** dans l’arborescence à gauche de l’écran.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-209">Confirm that you see both **AzureStorageLinkedService** and **HDInsightOnDemandLinkedService** in the tree view on the left.</span></span>

    ![Arborescence avec les services liés](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-linked-services.png)

## <a name="create-datasets"></a><span data-ttu-id="dc7c7-211">Créer des jeux de données</span><span class="sxs-lookup"><span data-stu-id="dc7c7-211">Create datasets</span></span>
<span data-ttu-id="dc7c7-212">Dans cette étape, vous créez des jeux de données afin de représenter les données d’entrée et de sortie pour le traitement Hive.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-212">In this step, you create datasets to represent the input and output data for Hive processing.</span></span> <span data-ttu-id="dc7c7-213">Ces jeux de données font référence au service **AzureStorageLinkedService** que vous avez créé précédemment dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-213">These datasets refer to the **AzureStorageLinkedService** you have created earlier in this tutorial.</span></span> <span data-ttu-id="dc7c7-214">Le service lié pointe vers un compte de stockage Azure, et les jeux de données spécifient le conteneur, le dossier et le nom de fichier dans le stockage qui contient les données d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-214">The linked service points to an Azure Storage account and datasets specify container, folder, file name in the storage that holds input and output data.</span></span>   

### <a name="create-input-dataset"></a><span data-ttu-id="dc7c7-215">Créer le jeu de données d’entrée</span><span class="sxs-lookup"><span data-stu-id="dc7c7-215">Create input dataset</span></span>
1. <span data-ttu-id="dc7c7-216">Dans **Data Factory Editor**, cliquez sur **... Plus** dans la barre de commandes, cliquez sur **Nouveau jeu de données** et sélectionnez **Stockage d’objets Blob Azure**.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-216">In the **Data Factory Editor**, click **... More** on the command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>

    ![Nouveau jeu de données](./media/data-factory-build-your-first-pipeline-using-editor/new-data-set.png)
2. <span data-ttu-id="dc7c7-218">Copiez et collez l’extrait ci-dessous dans la fenêtre Draft-1.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-218">Copy and paste the following snippet to the Draft-1 window.</span></span> <span data-ttu-id="dc7c7-219">Dans l’extrait de code JSON, vous créez un jeu de données appelé **AzureBlobInput** , qui représente les données d’entrée pour une activité dans le pipeline.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-219">In the JSON snippet, you are creating a dataset called **AzureBlobInput** that represents input data for an activity in the pipeline.</span></span> <span data-ttu-id="dc7c7-220">En outre, vous spécifiez que les données d’entrée se trouvent dans le conteneur d’objets blob nommé **adfgetstarted** et dans le dossier nommé **inputdata**.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-220">In addition, you specify that the input data is located in the blob container called **adfgetstarted** and the folder called **inputdata**.</span></span>

    ```JSON
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
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
    <span data-ttu-id="dc7c7-221">Le tableau suivant décrit les propriétés JSON utilisées dans l'extrait de code :</span><span class="sxs-lookup"><span data-stu-id="dc7c7-221">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

   | <span data-ttu-id="dc7c7-222">Propriété</span><span class="sxs-lookup"><span data-stu-id="dc7c7-222">Property</span></span> | <span data-ttu-id="dc7c7-223">Description</span><span class="sxs-lookup"><span data-stu-id="dc7c7-223">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="dc7c7-224">type</span><span class="sxs-lookup"><span data-stu-id="dc7c7-224">type</span></span> |<span data-ttu-id="dc7c7-225">La propriété du type est définie sur **AzureBlob**, car les données se trouvent dans le stockage blob Azure.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-225">The type property is set to **AzureBlob** because data resides in an Azure blob storage.</span></span> |
   | <span data-ttu-id="dc7c7-226">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="dc7c7-226">linkedServiceName</span></span> |<span data-ttu-id="dc7c7-227">Fait référence au service **AzureStorageLinkedService** que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-227">Refers to the **AzureStorageLinkedService** you created earlier.</span></span> |
   | <span data-ttu-id="dc7c7-228">folderPath</span><span class="sxs-lookup"><span data-stu-id="dc7c7-228">folderPath</span></span> | <span data-ttu-id="dc7c7-229">Spécifie le **conteneur** d’objets blob et le **dossier** contenant les objets blob d’entrée.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-229">Specifies the blob **container** and the **folder** that contains input blobs.</span></span> | 
   | <span data-ttu-id="dc7c7-230">fileName</span><span class="sxs-lookup"><span data-stu-id="dc7c7-230">fileName</span></span> |<span data-ttu-id="dc7c7-231">Cette propriété est facultative.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-231">This property is optional.</span></span> <span data-ttu-id="dc7c7-232">Si vous omettez cette propriété, tous les fichiers spécifiés dans le paramètre folderPath sont récupérés.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-232">If you omit this property, all the files from the folderPath are picked.</span></span> <span data-ttu-id="dc7c7-233">Dans ce didacticiel, seul le fichier **input.log** est traité.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-233">In this tutorial, only the **input.log** is processed.</span></span> |
   | <span data-ttu-id="dc7c7-234">type</span><span class="sxs-lookup"><span data-stu-id="dc7c7-234">type</span></span> |<span data-ttu-id="dc7c7-235">Les fichiers journaux étant au format texte, nous utilisons **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-235">The log files are in text format, so we use **TextFormat**.</span></span> |
   | <span data-ttu-id="dc7c7-236">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="dc7c7-236">columnDelimiter</span></span> |<span data-ttu-id="dc7c7-237">Les colonnes des fichiers journaux sont délimitées par une **virgule (`,`)**.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-237">columns in the log files are delimited by **comma character (`,`)**</span></span> |
   | <span data-ttu-id="dc7c7-238">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="dc7c7-238">frequency/interval</span></span> |<span data-ttu-id="dc7c7-239">La fréquence est définie sur **Mois** et l’intervalle est **1**, ce qui signifie que les segments d’entrée sont disponibles mensuellement.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-239">frequency set to **Month** and interval is **1**, which means that the input slices are available monthly.</span></span> |
   | <span data-ttu-id="dc7c7-240">external</span><span class="sxs-lookup"><span data-stu-id="dc7c7-240">external</span></span> | <span data-ttu-id="dc7c7-241">Cette propriété a la valeur **true** si les données d’entrée ne sont pas générées par ce pipeline.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-241">This property is set to **true** if the input data is not generated by this pipeline.</span></span> <span data-ttu-id="dc7c7-242">Dans ce didacticiel, le fichier input.log n’étant pas généré par ce pipeline, nous définissons la propriété sur true.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-242">In this tutorial, the input.log file is not generated by this pipeline, so we set the property to true.</span></span> |

    <span data-ttu-id="dc7c7-243">Pour plus d’informations sur ces propriétés JSON, voir [Connecteur de stockage Blob Azure](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="dc7c7-243">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
3. <span data-ttu-id="dc7c7-244">Cliquez sur **Déployer** dans la barre de commandes pour déployer le jeu de données que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-244">Click **Deploy** on the command bar to deploy the newly created dataset.</span></span> <span data-ttu-id="dc7c7-245">Vous devez voir le jeu de données dans l’arborescence sur la gauche.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-245">You should see the dataset in the tree view on the left.</span></span>

### <a name="create-output-dataset"></a><span data-ttu-id="dc7c7-246">Créer un jeu de données de sortie</span><span class="sxs-lookup"><span data-stu-id="dc7c7-246">Create output dataset</span></span>
<span data-ttu-id="dc7c7-247">Vous allez maintenant créer le jeu de données de sortie pour représenter les données de sortie stockées dans le stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-247">Now, you create the output dataset to represent the output data stored in the Azure Blob storage.</span></span>

1. <span data-ttu-id="dc7c7-248">Dans **Data Factory Editor**, cliquez sur **... Plus** dans la barre de commandes, cliquez sur **Nouveau jeu de données** et sélectionnez **Stockage d’objets Blob Azure**.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-248">In the **Data Factory Editor**, click **... More** on the command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>  
2. <span data-ttu-id="dc7c7-249">Copiez et collez l’extrait ci-dessous dans la fenêtre Draft-1.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-249">Copy and paste the following snippet to the Draft-1 window.</span></span> <span data-ttu-id="dc7c7-250">Dans l’extrait de code JSON, vous créez un jeu de données appelé **AzureBlobOutput**et spécifiez la structure des données produites par le script Hive.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-250">In the JSON snippet, you are creating a dataset called **AzureBlobOutput**, and specifying the structure of the data that is produced by the Hive script.</span></span> <span data-ttu-id="dc7c7-251">Indiquez aussi que les résultats sont stockés dans le conteneur d’objets blob appelé **adfgetstarted** et dans le dossier appelé **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-251">In addition, you specify that the results are stored in the blob container called **adfgetstarted** and the folder called **partitioneddata**.</span></span> <span data-ttu-id="dc7c7-252">La section **availability** spécifie que le jeu de données de sortie est produit tous les mois.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-252">The **availability** section specifies that the output dataset is produced on a monthly basis.</span></span>

    ```JSON
    {
      "name": "AzureBlobOutput",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
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
    <span data-ttu-id="dc7c7-253">Consultez la section **Créer le jeu de données d’entrée** pour obtenir une description de ces propriétés.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-253">See **Create the input dataset** section for descriptions of these properties.</span></span> <span data-ttu-id="dc7c7-254">Vous ne définissez pas la propriété externe sur un jeu de données de sortie, car le jeu de données est produit par le service Data Factory.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-254">You do not set the external property on an output dataset as the dataset is produced by the Data Factory service.</span></span>
3. <span data-ttu-id="dc7c7-255">Cliquez sur **Déployer** dans la barre de commandes pour déployer le jeu de données que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-255">Click **Deploy** on the command bar to deploy the newly created dataset.</span></span>
4. <span data-ttu-id="dc7c7-256">Vérifiez que le jeu de données a été correctement créé.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-256">Verify that the dataset is created successfully.</span></span>

    ![Arborescence avec les services liés](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-data-set.png)

## <a name="create-pipeline"></a><span data-ttu-id="dc7c7-258">Création d’un pipeline</span><span class="sxs-lookup"><span data-stu-id="dc7c7-258">Create pipeline</span></span>
<span data-ttu-id="dc7c7-259">Dans cette étape, vous créez votre premier pipeline avec une activité **HDInsightHive** .</span><span class="sxs-lookup"><span data-stu-id="dc7c7-259">In this step, you create your first pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="dc7c7-260">La tranche d’entrée est disponible mensuellement (fréquence : Mois, intervalle : 1), la tranche de sortie est produite mensuellement et la propriété du planificateur pour l’activité est également définie sur Mensuellement.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-260">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and the scheduler property for the activity is also set to monthly.</span></span> <span data-ttu-id="dc7c7-261">Les paramètres pour le jeu de données de sortie et le planificateur d’activité doivent correspondre.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-261">The settings for the output dataset and the activity scheduler must match.</span></span> <span data-ttu-id="dc7c7-262">À ce stade, c'est le jeu de données de sortie qui pilote la planification : vous devez donc créer un jeu de données de sortie même si l’activité ne génère aucune sortie.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-262">Currently, output dataset is what drives the schedule, so you must create an output dataset even if the activity does not produce any output.</span></span> <span data-ttu-id="dc7c7-263">Si l’activité ne prend aucune entrée, vous pouvez ignorer la création du jeu de données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-263">If the activity doesn't take any input, you can skip creating the input dataset.</span></span> <span data-ttu-id="dc7c7-264">Les propriétés utilisées dans le code JSON suivant sont expliquées à la fin de cette section.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-264">The properties used in the following JSON are explained at the end of this section.</span></span>

1. <span data-ttu-id="dc7c7-265">Dans **Data Factory Editor**, cliquez sur **Points de suspension (…) Autres commandes**, puis sur **Nouveau pipeline**.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-265">In the **Data Factory Editor**, click **Ellipsis (…) More commands** and then click **New pipeline**.</span></span>

    ![bouton Nouveau pipeline](./media/data-factory-build-your-first-pipeline-using-editor/new-pipeline-button.png)
2. <span data-ttu-id="dc7c7-267">Copiez et collez l’extrait ci-dessous dans la fenêtre Draft-1.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-267">Copy and paste the following snippet to the Draft-1 window.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="dc7c7-268">Dans le code JSON, remplacez **storageaccountname** par le nom de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-268">Replace **storageaccountname** with the name of your storage account in the JSON.</span></span>
   >
   >

    ```JSON
    {
        "name": "MyFirstPipeline",
        "properties": {
            "description": "My first Azure Data Factory pipeline",
            "activities": [
                {
                    "type": "HDInsightHive",
                    "typeProperties": {
                        "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                        "scriptLinkedService": "AzureStorageLinkedService",
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

    <span data-ttu-id="dc7c7-269">Dans l’extrait de code JSON, vous créez un pipeline qui se compose d’une seule activité utilisant Hive pour traiter des données sur un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-269">In the JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive to process Data on an HDInsight cluster.</span></span>

    <span data-ttu-id="dc7c7-270">Le fichier de script Hive, **partitionweblogs.hql**, est stocké dans le compte de stockage Azure (spécifié par le service scriptLinkedService, appelé **AzureStorageLinkedService**) et dans le dossier **script** du conteneur **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-270">The Hive script file, **partitionweblogs.hql**, is stored in the Azure storage account (specified by the scriptLinkedService, called **AzureStorageLinkedService**), and in **script** folder in the container **adfgetstarted**.</span></span>

    <span data-ttu-id="dc7c7-271">La section **defines** est utilisée pour spécifier les paramètres d’exécution passés au script Hive comme valeurs de configuration Hive (par exemple ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span><span class="sxs-lookup"><span data-stu-id="dc7c7-271">The **defines** section is used to specify the runtime settings that are passed to the hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span></span>

    <span data-ttu-id="dc7c7-272">Les propriétés **start** et **end** du pipeline spécifient la période active du pipeline.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-272">The **start** and **end** properties of the pipeline specifies the active period of the pipeline.</span></span>

    <span data-ttu-id="dc7c7-273">Dans l’activité JSON, vous spécifiez que le script Hive s’exécute sur le calcul spécifié par le service **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-273">In the activity JSON, you specify that the Hive script runs on the compute specified by the **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="dc7c7-274">Consultez « Pipeline JSON » dans [Pipelines et activités dans Azure Data Factory](data-factory-create-pipelines.md) pour plus d’informations sur les propriétés JSON utilisées dans l’exemple.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-274">See "Pipeline JSON" in [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) for details about JSON properties used in the example.</span></span>
   >
   >
3. <span data-ttu-id="dc7c7-275">Vérifiez les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="dc7c7-275">Confirm the following:</span></span>

   1. <span data-ttu-id="dc7c7-276">Le fichier **input.log** existe dans le dossier **inputdata** du conteneur **adfgetstarted** dans le stockage d’objets blob Azure</span><span class="sxs-lookup"><span data-stu-id="dc7c7-276">**input.log** file exists in the **inputdata** folder of the **adfgetstarted** container in the Azure blob storage</span></span>
   2. <span data-ttu-id="dc7c7-277">Le fichier **partitionweblogs.hql** existe dans le dossier **script** du conteneur **adfgetstarted** dans le stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-277">**partitionweblogs.hql** file exists in the **script** folder of the **adfgetstarted** container in the Azure blob storage.</span></span> <span data-ttu-id="dc7c7-278">Suivez les étapes de vérification de la [Vue d’ensemble du didacticiel](data-factory-build-your-first-pipeline.md) si vous ne voyez pas ces fichiers.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-278">Complete the prerequisite steps in the [Tutorial Overview](data-factory-build-your-first-pipeline.md) if you don't see these files.</span></span>
   3. <span data-ttu-id="dc7c7-279">Dans le pipeline JSON, vérifiez que vous avez bien remplacé **storageaccountname** par le nom de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-279">Confirm that you replaced **storageaccountname** with the name of your storage account in the pipeline JSON.</span></span>
4. <span data-ttu-id="dc7c7-280">Cliquez sur **Déployer** dans la barre de commandes pour déployer le pipeline.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-280">Click **Deploy** on the command bar to deploy the pipeline.</span></span> <span data-ttu-id="dc7c7-281">Étant donné que les valeurs pour **start** et **end** sont définies sur des valeurs antérieures au moment actuel, et que **isPaused** est défini sur false, le pipeline (activité dans le pipeline) s’exécute immédiatement après le déploiement.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-281">Since the **start** and **end** times are set in the past and **isPaused** is set to false, the pipeline (activity in the pipeline) runs immediately after you deploy.</span></span>
5. <span data-ttu-id="dc7c7-282">Vérifiez que le pipeline apparaît dans l’arborescence.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-282">Confirm that you see the pipeline in the tree view.</span></span>

    ![Arborescence avec pipeline](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-pipeline.png)
6. <span data-ttu-id="dc7c7-284">Félicitations ! Vous avez créé votre premier pipeline !</span><span class="sxs-lookup"><span data-stu-id="dc7c7-284">Congratulations, you have successfully created your first pipeline!</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="dc7c7-285">Surveillance d’un pipeline</span><span class="sxs-lookup"><span data-stu-id="dc7c7-285">Monitor pipeline</span></span>
### <a name="monitor-pipeline-using-diagram-view"></a><span data-ttu-id="dc7c7-286">Surveillance d’un pipeline à l’aide de la Vue de diagramme</span><span class="sxs-lookup"><span data-stu-id="dc7c7-286">Monitor pipeline using Diagram View</span></span>
1. <span data-ttu-id="dc7c7-287">Cliquez sur **X** pour fermer les panneaux de Data Factory Editor et revenir au panneau Data Factory, puis cliquez sur **Diagramme**.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-287">Click **X** to close Data Factory Editor blades and to navigate back to the Data Factory blade, and click **Diagram**.</span></span>

    ![Vignette schématique](./media/data-factory-build-your-first-pipeline-using-editor/diagram-tile.png)
2. <span data-ttu-id="dc7c7-289">Dans la Vue de diagramme, une vue d’ensemble des pipelines et des jeux de données utilisés dans ce didacticiel s’affiche.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-289">In the Diagram View, you see an overview of the pipelines, and datasets used in this tutorial.</span></span>

    ![Vue du diagramme](./media/data-factory-build-your-first-pipeline-using-editor/diagram-view-2.png)
3. <span data-ttu-id="dc7c7-291">Pour afficher toutes les activités du pipeline, cliquez avec le bouton droit sur le pipeline dans le diagramme, puis cliquez sur Ouvrir un pipeline.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-291">To view all activities in the pipeline, right-click pipeline in the diagram and click Open Pipeline.</span></span>

    ![Menu Ouvrir un pipeline](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-menu.png)
4. <span data-ttu-id="dc7c7-293">Vérifiez que l’activité HDInsightHive est bien dans le pipeline.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-293">Confirm that you see the HDInsightHive activity in the pipeline.</span></span>

    ![Vue Ouvrir un pipeline](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-view.png)

    <span data-ttu-id="dc7c7-295">Pour revenir à la vue précédente, cliquez sur **Fabrique de données** dans le menu de navigation du haut.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-295">To navigate back to the previous view, click **Data factory** in the breadcrumb menu at the top.</span></span>
5. <span data-ttu-id="dc7c7-296">Dans la **Vue de diagramme**, double-cliquez sur le jeu de données **AzureBlobInput**.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-296">In the **Diagram View**, double-click the dataset **AzureBlobInput**.</span></span> <span data-ttu-id="dc7c7-297">Vérifiez que l’état du segment est **Prêt** .</span><span class="sxs-lookup"><span data-stu-id="dc7c7-297">Confirm that the slice is in **Ready** state.</span></span> <span data-ttu-id="dc7c7-298">Plusieurs minutes peuvent être nécessaires avant que le segment n’apparaisse avec l’état Prêt.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-298">It may take a couple of minutes for the slice to show up in Ready state.</span></span> <span data-ttu-id="dc7c7-299">Si rien ne se produit au bout d’un moment, vérifiez que le fichier d’entrée (input.log) est placé dans le conteneur (adfgetstarted) et le dossier (inputdata) appropriés.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-299">If it does not happen after you wait for sometime, see if you have the input file (input.log) placed in the right container (adfgetstarted) and folder (inputdata).</span></span>

   ![Segment d’entrée dans l’état Prêt](./media/data-factory-build-your-first-pipeline-using-editor/input-slice-ready.png)
6. <span data-ttu-id="dc7c7-301">Cliquez sur **X** pour fermer le panneau **AzureBlobInput**.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-301">Click **X** to close **AzureBlobInput** blade.</span></span>
7. <span data-ttu-id="dc7c7-302">Dans la **Vue de diagramme**, double-cliquez sur le jeu de données **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-302">In the **Diagram View**, double-click the dataset **AzureBlobOutput**.</span></span> <span data-ttu-id="dc7c7-303">La tranche est en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-303">You see that the slice that is currently being processed.</span></span>

   ![Jeu de données](./media/data-factory-build-your-first-pipeline-using-editor/dataset-blade.png)
8. <span data-ttu-id="dc7c7-305">Quand le traitement est terminé, l’état de la tranche est **Prêt** .</span><span class="sxs-lookup"><span data-stu-id="dc7c7-305">When processing is done, you see the slice in **Ready** state.</span></span>

   ![Jeu de données](./media/data-factory-build-your-first-pipeline-using-editor/dataset-slice-ready.png)  

   > [!IMPORTANT]
   > <span data-ttu-id="dc7c7-307">La création d’un cluster HDInsight à la demande prend généralement un certain temps (environ 20 minutes).</span><span class="sxs-lookup"><span data-stu-id="dc7c7-307">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="dc7c7-308">Le pipeline devrait donc traiter la tranche en **30 minutes environ** .</span><span class="sxs-lookup"><span data-stu-id="dc7c7-308">Therefore, expect the pipeline to       take **approximately 30 minutes** to process the slice.</span></span>
   >
   >

9. <span data-ttu-id="dc7c7-309">Quand l’état du segment est **Prêt**, vérifiez la présence des données de sortie dans le dossier **partitioneddata** du conteneur **adfgetstarted** de votre stockage d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-309">When the slice is in **Ready** state, check the **partitioneddata** folder in the **adfgetstarted** container in your blob storage for the output data.</span></span>  

   ![données de sortie](./media/data-factory-build-your-first-pipeline-using-editor/three-ouptut-files.png)
10. <span data-ttu-id="dc7c7-311">Cliquez sur la tranche pour en afficher les détails dans le panneau **Tranche de données** .</span><span class="sxs-lookup"><span data-stu-id="dc7c7-311">Click the slice to see details about it in a **Data slice** blade.</span></span>

   ![Détails de la tranche](./media/data-factory-build-your-first-pipeline-using-editor/data-slice-details.png)  
11. <span data-ttu-id="dc7c7-313">Cliquez sur une exécution d’activité (activité Hive dans notre scénario) dans la **liste Exécutions d’activité** pour en afficher les détails dans la fenêtre **Détails de l’exécution d’activité**.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-313">Click an activity run in the **Activity runs list** to see details about an activity run (Hive activity in our scenario) in an **Activity run details** window.</span></span>   

   ![Détails de l'exécution d'activité](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-blade.png)    

   <span data-ttu-id="dc7c7-315">Dans les fichiers journaux, vous pouvez voir la requête Hive qui a été exécutée et son état.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-315">From the log files, you can see the Hive query that was executed and status information.</span></span> <span data-ttu-id="dc7c7-316">Ces journaux sont utiles pour résoudre les problèmes.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-316">These logs are useful for troubleshooting any issues.</span></span>
   <span data-ttu-id="dc7c7-317">Consultez l’article [Surveillance et gestion des pipelines d’Azure Data Factory](data-factory-monitor-manage-pipelines.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-317">See [Monitor and manage pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) article for more details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dc7c7-318">Le fichier d’entrée sera supprimé lorsque la tranche est traitée avec succès.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-318">The input file gets deleted when the slice is processed successfully.</span></span> <span data-ttu-id="dc7c7-319">Par conséquent, si vous souhaitez réexécuter la tranche ou refaire le didacticiel, chargez le fichier d’entrée (input.log) dans le dossier inputdata du conteneur adfgetstarted.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-319">Therefore, if you want to rerun the slice or do the tutorial again, upload the input file (input.log) to the inputdata folder of the adfgetstarted container.</span></span>
>
>

### <a name="monitor-pipeline-using-monitor--manage-app"></a><span data-ttu-id="dc7c7-320">Surveiller le pipeline à l’aide de l’application de surveillance et de gestion</span><span class="sxs-lookup"><span data-stu-id="dc7c7-320">Monitor pipeline using Monitor & Manage App</span></span>
<span data-ttu-id="dc7c7-321">Vous pouvez également utiliser l’application de surveillance et de gestion pour surveiller vos pipelines.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-321">You can also use Monitor & Manage application to monitor your pipelines.</span></span> <span data-ttu-id="dc7c7-322">Pour en savoir plus sur l’utilisation de cette application, consultez l’article [Surveiller et gérer les pipelines Azure Data Factory à l’aide de l’application de surveillance et de gestion](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="dc7c7-322">For detailed information about using this application, see [Monitor and manage Azure Data Factory pipelines using Monitoring and Management App](data-factory-monitor-manage-app.md).</span></span>

1. <span data-ttu-id="dc7c7-323">Cliquez sur la mosaïque **Surveiller et gérer** sur la page d’accueil de votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-323">Click **Monitor & Manage** tile on the home page for your data factory.</span></span>

    ![Vignette Surveiller et gérer](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-tile.png)
2. <span data-ttu-id="dc7c7-325">**L’application de surveillance et de gestion** devrait s’afficher.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-325">You should see **Monitor & Manage application**.</span></span> <span data-ttu-id="dc7c7-326">Modifiez l’**heure de début** et l’**heure de fin** pour qu’elles correspondent aux heures de début et de fin de votre pipeline, puis cliquez sur **Appliquer**.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-326">Change the **Start time** and **End time** to match start and end times of your pipeline, and click **Apply**.</span></span>

    ![Application de surveillance et gestion](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-app.png)
3. <span data-ttu-id="dc7c7-328">Sélectionnez une fenêtre d’activité dans la liste des **fenêtres d’activité** pour en afficher les détails.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-328">Select an activity window in the **Activity Windows** list to see details about it.</span></span>

    ![Détails de la fenêtre d’activité](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-details.png)

## <a name="summary"></a><span data-ttu-id="dc7c7-330">Résumé</span><span class="sxs-lookup"><span data-stu-id="dc7c7-330">Summary</span></span>
<span data-ttu-id="dc7c7-331">Dans ce didacticiel, vous avez créé une fabrique de données Azure pour traiter des données en exécutant le script Hive sur un cluster Hadoop HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-331">In this tutorial, you created an Azure data factory to process data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="dc7c7-332">Vous avez effectué les étapes suivantes dans le portail Azure à l’aide de Data Factory Editor :</span><span class="sxs-lookup"><span data-stu-id="dc7c7-332">You used the Data Factory Editor in the Azure portal to do the following steps:</span></span>  

1. <span data-ttu-id="dc7c7-333">Création d’une **fabrique de données**Azure.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-333">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="dc7c7-334">Création de deux **services liés**:</span><span class="sxs-lookup"><span data-stu-id="dc7c7-334">Created two **linked services**:</span></span>
   1. <span data-ttu-id="dc7c7-335">**Azure Storage** pour lier à la fabrique de données votre stockage d’objets blob Azure contenant les fichiers d’entrée/sortie.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-335">**Azure Storage** linked service to link your Azure blob storage that holds input/output files to the data factory.</span></span>
   2. <span data-ttu-id="dc7c7-336">**Azure HDInsight** à la demande pour lier à la fabrique de données un cluster Hadoop HDInsight à la demande.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-336">**Azure HDInsight** on-demand linked service to link an on-demand HDInsight Hadoop cluster to the data factory.</span></span> <span data-ttu-id="dc7c7-337">Azure Data Factory crée un cluster Hadoop HDInsight juste-à-temps pour traiter les données d’entrée et produire des données de sortie.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-337">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time to process input data and produce output data.</span></span>
3. <span data-ttu-id="dc7c7-338">Création de deux **jeux de données**qui décrivent les données d’entrée et de sortie pour l’activité HDInsight Hive dans le pipeline.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-338">Created two **datasets**, which describe input and output data for HDInsight Hive activity in the pipeline.</span></span>
4. <span data-ttu-id="dc7c7-339">Création d’un **pipeline** avec une activité **Hive HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-339">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dc7c7-340">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="dc7c7-340">Next Steps</span></span>
<span data-ttu-id="dc7c7-341">Dans cet article, vous avez créé un pipeline avec une activité de transformation (Activité HDInsight) qui exécute un script Hive sur un cluster HDInsight à la demande.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-341">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand HDInsight cluster.</span></span> <span data-ttu-id="dc7c7-342">Pour voir comment utiliser une activité de copie pour copier des données depuis un objet blob Azure vers Azure SQL, consultez le [Didacticiel : copie de données depuis un objet blob Azure vers Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="dc7c7-342">To see how to use a Copy Activity to copy data from an Azure Blob to Azure SQL, see [Tutorial: Copy data from an Azure blob to Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="dc7c7-343">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="dc7c7-343">See Also</span></span>
| <span data-ttu-id="dc7c7-344">Rubrique</span><span class="sxs-lookup"><span data-stu-id="dc7c7-344">Topic</span></span> | <span data-ttu-id="dc7c7-345">Description</span><span class="sxs-lookup"><span data-stu-id="dc7c7-345">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="dc7c7-346">Pipelines</span><span class="sxs-lookup"><span data-stu-id="dc7c7-346">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="dc7c7-347">Cet article vous aide à comprendre les pipelines et les activités dans Azure Data Factory, et à les utiliser dans l’optique de créer des workflows pilotés par les données de bout en bout pour votre scénario ou votre entreprise.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-347">This article helps you understand pipelines and activities in Azure Data Factory and how to use them to construct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="dc7c7-348">Groupes de données</span><span class="sxs-lookup"><span data-stu-id="dc7c7-348">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="dc7c7-349">Cet article vous aide à comprendre les jeux de données dans Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-349">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="dc7c7-350">Planification et exécution</span><span class="sxs-lookup"><span data-stu-id="dc7c7-350">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="dc7c7-351">Cet article explique les aspects de la planification et de l’exécution du modèle d’application Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-351">This article explains the scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="dc7c7-352">Surveiller et gérer les pipelines Azure Data Factory à l’aide de la nouvelle application de surveillance et gestion.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-352">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="dc7c7-353">Cet article décrit comment surveiller, gérer et déboguer les pipelines à l’aide de l’application de surveillance et gestion.</span><span class="sxs-lookup"><span data-stu-id="dc7c7-353">This article describes how to monitor, manage, and debug pipelines using the Monitoring & Management App.</span></span> |
