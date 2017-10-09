---
title: "aaaBuild votre première fabrique de données (portail Azure) | Documents Microsoft"
description: "Dans ce didacticiel, vous créez un exemple de pipeline Azure Data Factory à l’aide d’éditeur Data Factory Bonjour portail Azure."
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
ms.openlocfilehash: fc80776001b181a59c04d80d2e05c20b107a63f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-portal"></a><span data-ttu-id="4ec4a-103">Didacticiel : Créer votre première fabrique de données Azure à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="4ec4a-103">Tutorial: Build your first Azure data factory using Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4ec4a-104">Vue d’ensemble et étapes préalables requises</span><span class="sxs-lookup"><span data-stu-id="4ec4a-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="4ec4a-105">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="4ec4a-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="4ec4a-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4ec4a-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="4ec4a-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4ec4a-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="4ec4a-108">Modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4ec4a-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="4ec4a-109">API REST</span><span class="sxs-lookup"><span data-stu-id="4ec4a-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)


<span data-ttu-id="4ec4a-110">Dans cet article, vous apprendrez comment toouse [portail Azure](https://portal.azure.com/) toocreate votre première Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-110">In this article, you learn how toouse [Azure portal](https://portal.azure.com/) toocreate your first Azure data factory.</span></span> <span data-ttu-id="4ec4a-111">didacticiel de hello toodo à l’aide d’autres outils/kits de développement logiciel, sélectionnez une des options de hello à partir de la liste déroulante de hello.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-111">toodo hello tutorial using other tools/SDKs, select one of hello options from hello drop-down list.</span></span> 

<span data-ttu-id="4ec4a-112">pipeline Hello dans ce didacticiel a une activité : **activité HDInsight Hive**.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-112">hello pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="4ec4a-113">Cette activité s’exécute un script hive sur un cluster Azure HDInsight et les transformations d’entrée de données de sortie tooproduce.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data tooproduce output data.</span></span> <span data-ttu-id="4ec4a-114">pipeline de Hello est planifiée toorun une fois qu’un mois entre hello spécifié d’heures de début et de fin.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-114">hello pipeline is scheduled toorun once a month between hello specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="4ec4a-115">le pipeline de données Hello dans ce didacticiel transforme les données de sortie de données d’entrée tooproduce.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-115">hello data pipeline in this tutorial transforms input data tooproduce output data.</span></span> <span data-ttu-id="4ec4a-116">Pour obtenir un didacticiel sur la façon de toocopy les données à l’aide d’Azure Data Factory, consultez [didacticiel : copier des données à partir du stockage d’objets Blob tooSQL de base de données](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="4ec4a-116">For a tutorial on how toocopy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="4ec4a-117">Un pipeline peut contenir plusieurs activités.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-117">A pipeline can have more than one activity.</span></span> <span data-ttu-id="4ec4a-118">De plus, vous pouvez concaténer les deux activités (exécutée une activité après l’autre) en définissant le dataset de sortie hello d’une activité hello d’entrée dataset Hello autre activité.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-118">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="4ec4a-119">Pour plus d’informations, consultez [Planification et exécution dans Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="4ec4a-119">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4ec4a-120">Composants requis</span><span class="sxs-lookup"><span data-stu-id="4ec4a-120">Prerequisites</span></span>
1. <span data-ttu-id="4ec4a-121">Lisez [vue d’ensemble du didacticiel](data-factory-build-your-first-pipeline.md) article et hello complète **condition préalable** étapes.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-121">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete hello **prerequisite** steps.</span></span>
2. <span data-ttu-id="4ec4a-122">Cet article ne fournit pas une vue d’ensemble conceptuelle de hello service Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-122">This article does not provide a conceptual overview of hello Azure Data Factory service.</span></span> <span data-ttu-id="4ec4a-123">Nous recommandons que vous parcourez [Introduction tooAzure Data Factory](data-factory-introduction.md) article pour obtenir une présentation détaillée du service de hello.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-123">We recommend that you go through [Introduction tooAzure Data Factory](data-factory-introduction.md) article for a detailed overview of hello service.</span></span>  

## <a name="create-data-factory"></a><span data-ttu-id="4ec4a-124">Créer une fabrique de données</span><span class="sxs-lookup"><span data-stu-id="4ec4a-124">Create data factory</span></span>
<span data-ttu-id="4ec4a-125">Une fabrique de données peut avoir un ou plusieurs pipelines.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-125">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="4ec4a-126">Un pipeline peut contenir une ou plusieurs activités.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-126">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="4ec4a-127">Par exemple, un activité de copie toocopy des données d’un magasin de données de destination tooa source et un toorun d’activité HDInsight Hive un tootransform de script Hive données tooproduct sortie les données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-127">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform input data tooproduct output data.</span></span> <span data-ttu-id="4ec4a-128">Commençons par créer la fabrique de données hello dans cette étape.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-128">Let's start with creating hello data factory in this step.</span></span>

1. <span data-ttu-id="4ec4a-129">Connectez-vous à toohello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4ec4a-129">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="4ec4a-130">Cliquez sur **nouveau** sur menu gauche hello **données + Analytique**, puis cliquez sur **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-130">Click **NEW** on hello left menu, click **Data + Analytics**, and click **Data Factory**.</span></span>

   ![Panneau Créer](./media/data-factory-build-your-first-pipeline-using-editor/create-blade.png)
3. <span data-ttu-id="4ec4a-132">Bonjour **nouvelle fabrique de données** panneau, entrez **GetStartedDF** pour hello nom.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-132">In hello **New data factory** blade, enter **GetStartedDF** for hello Name.</span></span>

   ![Panneau Nouvelle fabrique de données](./media/data-factory-build-your-first-pipeline-using-editor/new-data-factory-blade.png)

   > [!IMPORTANT]
   > <span data-ttu-id="4ec4a-134">nom de Hello de fabrique de données Azure hello doit être **global unique**.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-134">hello name of hello Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="4ec4a-135">Si vous recevez une erreur de hello : **nom de fabrique de données « GetStartedDF » n’est pas disponible**.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-135">If you receive hello error: **Data factory name “GetStartedDF” is not available**.</span></span> <span data-ttu-id="4ec4a-136">Modifier le nom hello hello fabrique de données (par exemple, yournameGetStartedDF) et essayez à nouveau de créer.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-136">Change hello name of hello data factory (for example, yournameGetStartedDF) and try creating again.</span></span> <span data-ttu-id="4ec4a-137">Consultez la rubrique [Data Factory - Règles d'affectation des noms](data-factory-naming-rules.md) pour savoir comment nommer les artefacts Data Factory.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-137">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
   >
   > <span data-ttu-id="4ec4a-138">nom Hello hello fabrique de données peut être enregistré comme un **DNS** nom dans les futures hello et donc devenir visible publiquement.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-138">hello name of hello data factory may be registered as a **DNS** name in hello future and hence become publically visible.</span></span>
   >
   >
4. <span data-ttu-id="4ec4a-139">Sélectionnez hello **abonnement Azure** où vous souhaitez toobe de fabrique de données hello créé.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-139">Select hello **Azure subscription** where you want hello data factory toobe created.</span></span>
5. <span data-ttu-id="4ec4a-140">Sélectionnez un **groupe de ressources** existant ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-140">Select existing **resource group** or create a resource group.</span></span> <span data-ttu-id="4ec4a-141">Didacticiel de hello, créer un groupe de ressources nommé : **ADFGetStartedRG**.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-141">For hello tutorial, create a resource group named: **ADFGetStartedRG**.</span></span>
6. <span data-ttu-id="4ec4a-142">Sélectionnez hello **emplacement** de fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-142">Select hello **location** for hello data factory.</span></span> <span data-ttu-id="4ec4a-143">Seules les régions pris en charge par hello service Data Factory sont affichées dans la liste déroulante de hello.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-143">Only regions supported by hello Data Factory service are shown in hello drop-down list.</span></span>
7. <span data-ttu-id="4ec4a-144">Sélectionnez **toodashboard du code confidentiel**.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-144">Select **Pin toodashboard**.</span></span> 
8. <span data-ttu-id="4ec4a-145">Cliquez sur **créer** sur hello **nouvelle fabrique de données** panneau.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-145">Click **Create** on hello **New data factory** blade.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="4ec4a-146">instances de fabrique de données toocreate, vous devez être membre du hello [collaborateur de fabrique de données](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) rôle au niveau de groupe de ressource d’abonnement hello.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-146">toocreate Data Factory instances, you must be a member of hello [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at hello subscription/resource group level.</span></span>
   >
   >
7. <span data-ttu-id="4ec4a-147">Tableau de bord de hello, vous voyez hello suivant vignette avec l’état : déploiement de fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-147">On hello dashboard, you see hello following tile with status: Deploying data factory.</span></span>    

   ![État de la création de la fabrique de données](./media/data-factory-build-your-first-pipeline-using-editor/creating-data-factory-image.png)
8. <span data-ttu-id="4ec4a-149">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="4ec4a-149">Congratulations!</span></span> <span data-ttu-id="4ec4a-150">Vous avez créé votre première fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-150">You have successfully created your first data factory.</span></span> <span data-ttu-id="4ec4a-151">Une fois que la fabrique de données hello a été créé avec succès, vous voyez page de fabrique de données hello, qui vous indique hello contenu hello fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-151">After hello data factory has been created successfully, you see hello data factory page, which shows you hello contents of hello data factory.</span></span>     

    ![Panneau Data Factory](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-blade.png)

<span data-ttu-id="4ec4a-153">Avant de créer un pipeline dans la fabrique de données hello, vous devez toocreate quelques entités de fabrique de données tout d’abord.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-153">Before creating a pipeline in hello data factory, you need toocreate a few Data Factory entities first.</span></span> <span data-ttu-id="4ec4a-154">Vous créez tout d’abord les services liés toolink données magasins/calcule tooyour données stockent, définissent l’entrée et sortie des données de d’entrée/sortie toorepresent de jeux de données dans des magasins de données liées et ensuite créer un pipeline de hello avec une activité qui utilise ces jeux de données.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-154">You first create linked services toolink data stores/computes tooyour data store, define input and output datasets toorepresent input/output data in linked data stores, and then create hello pipeline with an activity that uses these datasets.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="4ec4a-155">Créez des services liés</span><span class="sxs-lookup"><span data-stu-id="4ec4a-155">Create linked services</span></span>
<span data-ttu-id="4ec4a-156">Dans cette étape, vous liez votre compte de stockage Azure et une fabrique de données à la demande Azure HDInsight cluster tooyour.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-156">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="4ec4a-157">blocages de compte de stockage Azure Hello hello des données d’entrée et de sortie pour le pipeline hello dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-157">hello Azure Storage account holds hello input and output data for hello pipeline in this sample.</span></span> <span data-ttu-id="4ec4a-158">Hello service lié HDInsight est toorun utilisé un script Hive spécifié dans l’activité hello du pipeline hello dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-158">hello HDInsight linked service is used toorun a Hive script specified in hello activity of hello pipeline in this sample.</span></span> <span data-ttu-id="4ec4a-159">Identifier les [magasin de données](data-factory-data-movement-activities.md)/[les services de calcul](data-factory-compute-linked-services.md) sont utilisés dans votre scénario et de lier ces fabrique de données de services toohello en créant des services liés.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-159">Identify what [data store](data-factory-data-movement-activities.md)/[compute services](data-factory-compute-linked-services.md) are used in your scenario and link those services toohello data factory by creating linked services.</span></span>  

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="4ec4a-160">Créer le service lié Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="4ec4a-160">Create Azure Storage linked service</span></span>
<span data-ttu-id="4ec4a-161">Dans cette étape, vous liez votre fabrique de données tooyour compte Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-161">In this step, you link your Azure Storage account tooyour data factory.</span></span> <span data-ttu-id="4ec4a-162">Dans ce didacticiel, vous utilisez hello même compte de stockage Azure hello HQL et les données d’entrée/sortie toostore de fichier de script.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-162">In this tutorial, you use hello same Azure Storage account toostore input/output data and hello HQL script file.</span></span>

1. <span data-ttu-id="4ec4a-163">Cliquez sur **auteur et déployer** sur hello **DATA FACTORY** panneau pour **GetStartedDF**.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-163">Click **Author and deploy** on hello **DATA FACTORY** blade for **GetStartedDF**.</span></span> <span data-ttu-id="4ec4a-164">Vous devez voir hello éditeur Data Factory.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-164">You should see hello Data Factory Editor.</span></span>

   ![Vignette Créer et déployer](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-author-deploy.png)
2. <span data-ttu-id="4ec4a-166">Cliquez sur **Nouveau magasin de données** et choisissez **Stockage Azure**.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-166">Click **New data store** and choose **Azure storage**.</span></span>

   ![Nouveau magasin de données - Stockage Azure - menu](./media/data-factory-build-your-first-pipeline-using-editor/new-data-store-azure-storage-menu.png)
3. <span data-ttu-id="4ec4a-168">Vous devez voir hello script JSON pour la création d’un stockage Azure lié à service dans l’éditeur de hello.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-168">You should see hello JSON script for creating an Azure Storage linked service in hello editor.</span></span>

   ![Service lié Azure Storage](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. <span data-ttu-id="4ec4a-170">Remplacez **nom de compte** avec le nom de hello de votre compte de stockage Azure et **clé de compte** avec la clé d’accès hello Hello compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-170">Replace **account name** with hello name of your Azure storage account and **account key** with hello access key of hello Azure storage account.</span></span> <span data-ttu-id="4ec4a-171">toolearn comment accéder à votre espace de stockage tooget de clé, consultez hello plus d’informations sur comment tooview, copier et régénérer stockage touches d’accès [gérer votre compte de stockage](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="4ec4a-171">toolearn how tooget your storage access key, see hello information about how tooview, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
5. <span data-ttu-id="4ec4a-172">Cliquez sur **déployer** sur toodeploy hello lié service de la barre de commandes hello.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-172">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

    ![Bouton déployer](./media/data-factory-build-your-first-pipeline-using-editor/deploy-button.png)

   <span data-ttu-id="4ec4a-174">Une fois hello service lié est déployé avec succès, hello **Draft-1** fenêtre doit disparaître et vous voyez **AzureStorageLinkedService** dans l’arborescence hello sur hello gauche.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-174">After hello linked service is deployed successfully, hello **Draft-1** window should disappear and you see **AzureStorageLinkedService** in hello tree view on hello left.</span></span>

    ![Service lié au stockage dans le menu](./media/data-factory-build-your-first-pipeline-using-editor/StorageLinkedServiceInTree.png)    

### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="4ec4a-176">Créer le service lié Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="4ec4a-176">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="4ec4a-177">Dans cette étape, vous liez une fabrique de données à la demande HDInsight cluster tooyour.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-177">In this step, you link an on-demand HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="4ec4a-178">Hello cluster HDInsight est automatiquement créé lors de l’exécution et supprimée une fois ceci effectué inactifs et le traitement de la durée spécifiée hello.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-178">hello HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for hello specified amount of time.</span></span>

1. <span data-ttu-id="4ec4a-179">Bonjour **éditeur Data Factory**, cliquez sur **... Plus**, puis sur **Nouveau calcul** et sélectionnez **Cluster à la demande HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-179">In hello **Data Factory Editor**, click **... More**, click **New compute**, and select **On-demand HDInsight cluster**.</span></span>

    ![Nouveau calcul](./media/data-factory-build-your-first-pipeline-using-editor/new-compute-menu.png)
2. <span data-ttu-id="4ec4a-181">Copiez et collez hello suivant extrait toohello **Draft-1** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-181">Copy and paste hello following snippet toohello **Draft-1** window.</span></span> <span data-ttu-id="4ec4a-182">extrait de code Hello JSON décrit les propriétés hello sont utilisées toocreate hello sur demande du cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-182">hello JSON snippet describes hello properties that are used toocreate hello HDInsight cluster on-demand.</span></span>

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

    <span data-ttu-id="4ec4a-183">Hello tableau suivant fournit des descriptions pour les propriétés JSON hello utilisées dans l’extrait de code hello :</span><span class="sxs-lookup"><span data-stu-id="4ec4a-183">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

   | <span data-ttu-id="4ec4a-184">Propriété</span><span class="sxs-lookup"><span data-stu-id="4ec4a-184">Property</span></span> | <span data-ttu-id="4ec4a-185">Description</span><span class="sxs-lookup"><span data-stu-id="4ec4a-185">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="4ec4a-186">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="4ec4a-186">ClusterSize</span></span> |<span data-ttu-id="4ec4a-187">Spécifie la taille de hello du cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-187">Specifies hello size of hello HDInsight cluster.</span></span> |
   | <span data-ttu-id="4ec4a-188">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="4ec4a-188">TimeToLive</span></span> | <span data-ttu-id="4ec4a-189">Spécifie la durée d’inactivité de ce hello pour le cluster HDInsight de hello, avant d’être supprimé.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-189">Specifies that hello idle time for hello HDInsight cluster, before it is deleted.</span></span> |
   | <span data-ttu-id="4ec4a-190">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="4ec4a-190">linkedServiceName</span></span> | <span data-ttu-id="4ec4a-191">Spécifie le compte de stockage hello toostore utilisé hello journaux générés par HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-191">Specifies hello storage account that is used toostore hello logs that are generated by HDInsight.</span></span> |

    <span data-ttu-id="4ec4a-192">Hello Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="4ec4a-192">Note hello following points:</span></span>

   * <span data-ttu-id="4ec4a-193">Hello Data Factory crée un **basés sur Linux** cluster HDInsight pour vous par hello JSON.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-193">hello Data Factory creates a **Linux-based** HDInsight cluster for you with hello JSON.</span></span> <span data-ttu-id="4ec4a-194">Pour plus d’informations, voir [Service lié à la demande Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="4ec4a-194">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
   * <span data-ttu-id="4ec4a-195">Vous pouvez utiliser votre **propre cluster HDInsight** au lieu d’utiliser un cluster HDInsight à la demande.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-195">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="4ec4a-196">Pour plus d’informations, voir [Service lié Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="4ec4a-196">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
   * <span data-ttu-id="4ec4a-197">Hello HDInsight cluster crée un **conteneur par défaut** dans le stockage blob hello spécifié dans hello JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="4ec4a-197">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="4ec4a-198">HDInsight ne supprime pas ce conteneur lorsque le cluster de hello est supprimé.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-198">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="4ec4a-199">Ce comportement est normal.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-199">This behavior is by design.</span></span> <span data-ttu-id="4ec4a-200">Avec le service lié HDInsight disponible à la demande, un cluster HDInsight est créé dès qu’une tranche est traitée, à moins qu’il n’existe un cluster actif (**timeToLive**).</span><span class="sxs-lookup"><span data-stu-id="4ec4a-200">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**).</span></span> <span data-ttu-id="4ec4a-201">Hello cluster est automatiquement supprimé lorsque le traitement de hello est effectué.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-201">hello cluster is automatically deleted when hello processing is done.</span></span>

       <span data-ttu-id="4ec4a-202">Comme un nombre croissant de tranches sont traitées, vous voyez un grand nombre de conteneurs dans votre stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-202">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="4ec4a-203">Si vous ne devez pas les pour la résolution des problèmes de travaux de hello, vous souhaiterez peut-être toodelete les coûts de stockage tooreduce hello.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-203">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="4ec4a-204">les noms de ces conteneurs Hello suivent un modèle : « adf**yourdatafactoryname**-**linkedservicename**- datetimestamp ».</span><span class="sxs-lookup"><span data-stu-id="4ec4a-204">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="4ec4a-205">Utiliser des outils tels que [Explorateur de stockage Microsoft](http://storageexplorer.com/) stockage d’objets blob des conteneurs de toodelete dans votre Azure.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-205">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

     <span data-ttu-id="4ec4a-206">Pour plus d’informations, voir [Service lié à la demande Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="4ec4a-206">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
3. <span data-ttu-id="4ec4a-207">Cliquez sur **déployer** sur toodeploy hello lié service de la barre de commandes hello.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-207">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

    ![Déployer un service lié HDInsight à la demande](./media/data-factory-build-your-first-pipeline-using-editor/ondemand-hdinsight-deploy.png)
4. <span data-ttu-id="4ec4a-209">Vérifiez que vous voyez les deux **AzureStorageLinkedService** et **HDInsightOnDemandLinkedService** dans l’arborescence hello sur hello gauche.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-209">Confirm that you see both **AzureStorageLinkedService** and **HDInsightOnDemandLinkedService** in hello tree view on hello left.</span></span>

    ![Arborescence avec les services liés](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-linked-services.png)

## <a name="create-datasets"></a><span data-ttu-id="4ec4a-211">Créez les jeux de données</span><span class="sxs-lookup"><span data-stu-id="4ec4a-211">Create datasets</span></span>
<span data-ttu-id="4ec4a-212">Dans cette étape, vous créez des groupes de données toorepresent hello d’entrée et sortie des données pour le traitement de la ruche.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-212">In this step, you create datasets toorepresent hello input and output data for Hive processing.</span></span> <span data-ttu-id="4ec4a-213">Ces jeux de données font référence toohello **AzureStorageLinkedService** que vous avez créé précédemment dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-213">These datasets refer toohello **AzureStorageLinkedService** you have created earlier in this tutorial.</span></span> <span data-ttu-id="4ec4a-214">Hello tooan de points de service lié compte de stockage Azure et de jeux de données spécifiez conteneur, dossier, le nom de fichier dans le stockage hello qui contient l’entrée et les données de sortie.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-214">hello linked service points tooan Azure Storage account and datasets specify container, folder, file name in hello storage that holds input and output data.</span></span>   

### <a name="create-input-dataset"></a><span data-ttu-id="4ec4a-215">Créer le jeu de données d’entrée</span><span class="sxs-lookup"><span data-stu-id="4ec4a-215">Create input dataset</span></span>
1. <span data-ttu-id="4ec4a-216">Bonjour **éditeur Data Factory**, cliquez sur **... Plus** dans la barre de commandes hello, cliquez sur **nouveau dataset**, puis sélectionnez **le stockage Blob Azure**.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-216">In hello **Data Factory Editor**, click **... More** on hello command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>

    ![Nouveau jeu de données](./media/data-factory-build-your-first-pipeline-using-editor/new-data-set.png)
2. <span data-ttu-id="4ec4a-218">Copiez et collez hello suivant fenêtre toohello Draft-1.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-218">Copy and paste hello following snippet toohello Draft-1 window.</span></span> <span data-ttu-id="4ec4a-219">Dans l’extrait de code hello JSON, vous créez un dataset nommé **AzureBlobInput** qui représente les données d’entrée pour une activité dans le pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-219">In hello JSON snippet, you are creating a dataset called **AzureBlobInput** that represents input data for an activity in hello pipeline.</span></span> <span data-ttu-id="4ec4a-220">En outre, vous spécifiez que les données d’entrée hello se trouve dans le conteneur d’objets blob hello appelé **adfgetstarted** et dossier hello appelé **inputdata**.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-220">In addition, you specify that hello input data is located in hello blob container called **adfgetstarted** and hello folder called **inputdata**.</span></span>

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
    <span data-ttu-id="4ec4a-221">Hello tableau suivant fournit des descriptions pour les propriétés JSON hello utilisées dans l’extrait de code hello :</span><span class="sxs-lookup"><span data-stu-id="4ec4a-221">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

   | <span data-ttu-id="4ec4a-222">Propriété</span><span class="sxs-lookup"><span data-stu-id="4ec4a-222">Property</span></span> | <span data-ttu-id="4ec4a-223">Description</span><span class="sxs-lookup"><span data-stu-id="4ec4a-223">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="4ec4a-224">type</span><span class="sxs-lookup"><span data-stu-id="4ec4a-224">type</span></span> |<span data-ttu-id="4ec4a-225">propriété de type Hello est définie trop**AzureBlob** , car les données résident dans un stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-225">hello type property is set too**AzureBlob** because data resides in an Azure blob storage.</span></span> |
   | <span data-ttu-id="4ec4a-226">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="4ec4a-226">linkedServiceName</span></span> |<span data-ttu-id="4ec4a-227">Fait référence toohello **AzureStorageLinkedService** vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-227">Refers toohello **AzureStorageLinkedService** you created earlier.</span></span> |
   | <span data-ttu-id="4ec4a-228">folderPath</span><span class="sxs-lookup"><span data-stu-id="4ec4a-228">folderPath</span></span> | <span data-ttu-id="4ec4a-229">Spécifie l’objet blob de hello **conteneur** et hello **dossier** qui contient des objets BLOB d’entrée.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-229">Specifies hello blob **container** and hello **folder** that contains input blobs.</span></span> | 
   | <span data-ttu-id="4ec4a-230">fileName</span><span class="sxs-lookup"><span data-stu-id="4ec4a-230">fileName</span></span> |<span data-ttu-id="4ec4a-231">Cette propriété est facultative.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-231">This property is optional.</span></span> <span data-ttu-id="4ec4a-232">Si vous omettez cette propriété, tous les fichiers hello hello folderPath sont récupérées.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-232">If you omit this property, all hello files from hello folderPath are picked.</span></span> <span data-ttu-id="4ec4a-233">Dans ce didacticiel, uniquement hello **input.log** est traité.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-233">In this tutorial, only hello **input.log** is processed.</span></span> |
   | <span data-ttu-id="4ec4a-234">type</span><span class="sxs-lookup"><span data-stu-id="4ec4a-234">type</span></span> |<span data-ttu-id="4ec4a-235">les fichiers journaux Hello étant au format texte, nous utilisons **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-235">hello log files are in text format, so we use **TextFormat**.</span></span> |
   | <span data-ttu-id="4ec4a-236">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="4ec4a-236">columnDelimiter</span></span> |<span data-ttu-id="4ec4a-237">colonnes dans les fichiers journaux de hello sont délimitées par **caractère virgule (`,`)**</span><span class="sxs-lookup"><span data-stu-id="4ec4a-237">columns in hello log files are delimited by **comma character (`,`)**</span></span> |
   | <span data-ttu-id="4ec4a-238">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="4ec4a-238">frequency/interval</span></span> |<span data-ttu-id="4ec4a-239">fréquence définie trop**mois** et l’intervalle est **1**, ce qui signifie que hello entrée tranches sont disponibles chaque mois.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-239">frequency set too**Month** and interval is **1**, which means that hello input slices are available monthly.</span></span> |
   | <span data-ttu-id="4ec4a-240">external</span><span class="sxs-lookup"><span data-stu-id="4ec4a-240">external</span></span> | <span data-ttu-id="4ec4a-241">Cette propriété a la valeur trop**true** si les données d’entrée hello ne sont pas générées par ce pipeline.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-241">This property is set too**true** if hello input data is not generated by this pipeline.</span></span> <span data-ttu-id="4ec4a-242">Dans ce didacticiel, le fichier de input.log de hello n’est pas généré par ce pipeline, et nous avons hello propriété tootrue.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-242">In this tutorial, hello input.log file is not generated by this pipeline, so we set hello property tootrue.</span></span> |

    <span data-ttu-id="4ec4a-243">Pour plus d’informations sur ces propriétés JSON, voir [Connecteur de stockage Blob Azure](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="4ec4a-243">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
3. <span data-ttu-id="4ec4a-244">Cliquez sur **déployer** sur le jeu de données toodeploy hello nouvellement créée de la barre de commandes hello.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-244">Click **Deploy** on hello command bar toodeploy hello newly created dataset.</span></span> <span data-ttu-id="4ec4a-245">Vous devez voir hello le jeu de données dans l’arborescence hello sur hello gauche.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-245">You should see hello dataset in hello tree view on hello left.</span></span>

### <a name="create-output-dataset"></a><span data-ttu-id="4ec4a-246">Créer un jeu de données de sortie</span><span class="sxs-lookup"><span data-stu-id="4ec4a-246">Create output dataset</span></span>
<span data-ttu-id="4ec4a-247">Maintenant, vous créez hello sortie dataset toorepresent hello sortie les données stockées dans hello le stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-247">Now, you create hello output dataset toorepresent hello output data stored in hello Azure Blob storage.</span></span>

1. <span data-ttu-id="4ec4a-248">Bonjour **éditeur Data Factory**, cliquez sur **... Plus** dans la barre de commandes hello, cliquez sur **nouveau dataset**, puis sélectionnez **le stockage Blob Azure**.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-248">In hello **Data Factory Editor**, click **... More** on hello command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>  
2. <span data-ttu-id="4ec4a-249">Copiez et collez hello suivant fenêtre toohello Draft-1.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-249">Copy and paste hello following snippet toohello Draft-1 window.</span></span> <span data-ttu-id="4ec4a-250">Dans l’extrait de code hello JSON, vous créez un dataset nommé **AzureBlobOutput**et préciser leur structure de données hello qui sont générées par le script Hive de hello hello.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-250">In hello JSON snippet, you are creating a dataset called **AzureBlobOutput**, and specifying hello structure of hello data that is produced by hello Hive script.</span></span> <span data-ttu-id="4ec4a-251">En outre, vous spécifiez que les résultats de hello sont stockés dans le conteneur d’objets blob hello appelé **adfgetstarted** et dossier hello appelé **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-251">In addition, you specify that hello results are stored in hello blob container called **adfgetstarted** and hello folder called **partitioneddata**.</span></span> <span data-ttu-id="4ec4a-252">Hello **disponibilité** section spécifie ce jeu de données de sortie hello est généré sur une base mensuelle.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-252">hello **availability** section specifies that hello output dataset is produced on a monthly basis.</span></span>

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
    <span data-ttu-id="4ec4a-253">Consultez **créer le jeu de données d’entrée hello** section pour obtenir une description de ces propriétés.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-253">See **Create hello input dataset** section for descriptions of these properties.</span></span> <span data-ttu-id="4ec4a-254">Vous ne définissez pas la propriété d’externe de hello sur un jeu de données de sortie comme jeu de données hello est généré par le service de fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-254">You do not set hello external property on an output dataset as hello dataset is produced by hello Data Factory service.</span></span>
3. <span data-ttu-id="4ec4a-255">Cliquez sur **déployer** sur le jeu de données toodeploy hello nouvellement créée de la barre de commandes hello.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-255">Click **Deploy** on hello command bar toodeploy hello newly created dataset.</span></span>
4. <span data-ttu-id="4ec4a-256">Vérifiez que ce jeu de données hello est créé avec succès.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-256">Verify that hello dataset is created successfully.</span></span>

    ![Arborescence avec les services liés](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-data-set.png)

## <a name="create-pipeline"></a><span data-ttu-id="4ec4a-258">Création d’un pipeline</span><span class="sxs-lookup"><span data-stu-id="4ec4a-258">Create pipeline</span></span>
<span data-ttu-id="4ec4a-259">Dans cette étape, vous créez votre premier pipeline avec une activité **HDInsightHive** .</span><span class="sxs-lookup"><span data-stu-id="4ec4a-259">In this step, you create your first pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="4ec4a-260">Secteur d’entrée est disponible mensuellement (fréquence : mois, intervalle : 1), la tranche de sortie est générée chaque mois et hello du planificateur pour l’activité de hello est également définie toomonthly.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-260">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and hello scheduler property for hello activity is also set toomonthly.</span></span> <span data-ttu-id="4ec4a-261">paramètres Hello pour le jeu de données de sortie hello et planificateur d’activité hello doivent correspondre.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-261">hello settings for hello output dataset and hello activity scheduler must match.</span></span> <span data-ttu-id="4ec4a-262">Actuellement, le dataset de sortie est les lecteurs hello planification, vous devez donc créer un dataset de sortie même si l’activité hello ne produit pas de sortie.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-262">Currently, output dataset is what drives hello schedule, so you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="4ec4a-263">Si l’activité hello n’accepte aucune entrée, vous pouvez ignorer le jeu de données d’entrée création hello.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-263">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span> <span data-ttu-id="4ec4a-264">propriétés qui Hello hello suivant JSON sont expliquées à fin hello de cette section.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-264">hello properties used in hello following JSON are explained at hello end of this section.</span></span>

1. <span data-ttu-id="4ec4a-265">Bonjour **éditeur Data Factory**, cliquez sur **points de suspension (...) Plusieurs commandes** puis cliquez sur **nouveau pipeline**.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-265">In hello **Data Factory Editor**, click **Ellipsis (…) More commands** and then click **New pipeline**.</span></span>

    ![bouton Nouveau pipeline](./media/data-factory-build-your-first-pipeline-using-editor/new-pipeline-button.png)
2. <span data-ttu-id="4ec4a-267">Copiez et collez hello suivant fenêtre toohello Draft-1.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-267">Copy and paste hello following snippet toohello Draft-1 window.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="4ec4a-268">Remplacez **storageaccountname** avec nom hello de votre compte de stockage Bonjour JSON.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-268">Replace **storageaccountname** with hello name of your storage account in hello JSON.</span></span>
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

    <span data-ttu-id="4ec4a-269">Dans l’extrait de code hello JSON, vous créez un pipeline qui se compose d’une activité unique qui utilise la ruche tooprocess données sur un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-269">In hello JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive tooprocess Data on an HDInsight cluster.</span></span>

    <span data-ttu-id="4ec4a-270">fichier de script Hive Hello, **partitionweblogs.hql**, est stocké dans hello compte de stockage Azure (spécifié par scriptLinkedService hello, appelé **AzureStorageLinkedService**) et dans  **script** dossier dans le conteneur de hello **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-270">hello Hive script file, **partitionweblogs.hql**, is stored in hello Azure storage account (specified by hello scriptLinkedService, called **AzureStorageLinkedService**), and in **script** folder in hello container **adfgetstarted**.</span></span>

    <span data-ttu-id="4ec4a-271">Hello **définit** section est de paramètres d’exécution utilisés toospecify hello script hive de toohello passés en tant que valeurs de configuration Hive (exemple : ${hiveconf : inputtable}, ${hiveconf:partitionedtable}).</span><span class="sxs-lookup"><span data-stu-id="4ec4a-271">hello **defines** section is used toospecify hello runtime settings that are passed toohello hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span></span>

    <span data-ttu-id="4ec4a-272">Hello **Démarrer** et **fin** propriétés de pipeline de hello spécifie la période active de hello du pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-272">hello **start** and **end** properties of hello pipeline specifies hello active period of hello pipeline.</span></span>

    <span data-ttu-id="4ec4a-273">Dans l’activité hello JSON, vous spécifiez ce script Hive hello s’exécute sur le calcul hello spécifié par hello **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-273">In hello activity JSON, you specify that hello Hive script runs on hello compute specified by hello **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="4ec4a-274">Consultez la section « JSON de Pipeline » dans [Pipelines et les activités dans Azure Data Factory](data-factory-create-pipelines.md) pour plus d’informations sur les propriétés JSON utilisées dans l’exemple de hello.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-274">See "Pipeline JSON" in [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) for details about JSON properties used in hello example.</span></span>
   >
   >
3. <span data-ttu-id="4ec4a-275">Validez les éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="4ec4a-275">Confirm hello following:</span></span>

   1. <span data-ttu-id="4ec4a-276">**Input.log** fichier existe dans hello **inputdata** dossier Hello **adfgetstarted** conteneur Bonjour stockage d’objets blob Azure</span><span class="sxs-lookup"><span data-stu-id="4ec4a-276">**input.log** file exists in hello **inputdata** folder of hello **adfgetstarted** container in hello Azure blob storage</span></span>
   2. <span data-ttu-id="4ec4a-277">**partitionweblogs.hql** fichier existe dans hello **script** dossier Hello **adfgetstarted** conteneur Bonjour stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-277">**partitionweblogs.hql** file exists in hello **script** folder of hello **adfgetstarted** container in hello Azure blob storage.</span></span> <span data-ttu-id="4ec4a-278">Condition préalable de hello terminé les étapes Bonjour [vue d’ensemble du didacticiel](data-factory-build-your-first-pipeline.md) si vous ne voyez pas ces fichiers.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-278">Complete hello prerequisite steps in hello [Tutorial Overview](data-factory-build-your-first-pipeline.md) if you don't see these files.</span></span>
   3. <span data-ttu-id="4ec4a-279">Vérifiez que vous avez remplacé **storageaccountname** avec nom hello de votre compte de stockage Bonjour JSON de pipeline.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-279">Confirm that you replaced **storageaccountname** with hello name of your storage account in hello pipeline JSON.</span></span>
4. <span data-ttu-id="4ec4a-280">Cliquez sur **déployer** sur le pipeline de hello toodeploy de barre de commandes hello.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-280">Click **Deploy** on hello command bar toodeploy hello pipeline.</span></span> <span data-ttu-id="4ec4a-281">Depuis hello **Démarrer** et **fin** heures sont définies dans hello passée et **isPaused** est toofalse ensemble, pipeline de hello (activité dans le pipeline de hello) immédiatement après le déploiement.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-281">Since hello **start** and **end** times are set in hello past and **isPaused** is set toofalse, hello pipeline (activity in hello pipeline) runs immediately after you deploy.</span></span>
5. <span data-ttu-id="4ec4a-282">Vérifiez que vous voyez pipeline hello dans arborescence hello.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-282">Confirm that you see hello pipeline in hello tree view.</span></span>

    ![Arborescence avec pipeline](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-pipeline.png)
6. <span data-ttu-id="4ec4a-284">Félicitations ! Vous avez créé votre premier pipeline !</span><span class="sxs-lookup"><span data-stu-id="4ec4a-284">Congratulations, you have successfully created your first pipeline!</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="4ec4a-285">Surveillance d’un pipeline</span><span class="sxs-lookup"><span data-stu-id="4ec4a-285">Monitor pipeline</span></span>
### <a name="monitor-pipeline-using-diagram-view"></a><span data-ttu-id="4ec4a-286">Surveillance d’un pipeline à l’aide de la Vue de diagramme</span><span class="sxs-lookup"><span data-stu-id="4ec4a-286">Monitor pipeline using Diagram View</span></span>
1. <span data-ttu-id="4ec4a-287">Cliquez sur **X** tooclose éditeur Data Factory panneaux et toonavigate Panneau de fabrique de données toohello de sauvegarde, puis cliquez sur **diagramme**.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-287">Click **X** tooclose Data Factory Editor blades and toonavigate back toohello Data Factory blade, and click **Diagram**.</span></span>

    ![Vignette schématique](./media/data-factory-build-your-first-pipeline-using-editor/diagram-tile.png)
2. <span data-ttu-id="4ec4a-289">Dans la vue de diagramme de hello, vous consultez une vue d’ensemble des pipelines de hello et jeux de données utilisés dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-289">In hello Diagram View, you see an overview of hello pipelines, and datasets used in this tutorial.</span></span>

    ![Vue du diagramme](./media/data-factory-build-your-first-pipeline-using-editor/diagram-view-2.png)
3. <span data-ttu-id="4ec4a-291">tooview diagramme de toutes les activités dans le pipeline de hello, pipeline avec le bouton droit dans hello et cliquez sur Ouvrir Pipeline.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-291">tooview all activities in hello pipeline, right-click pipeline in hello diagram and click Open Pipeline.</span></span>

    ![Menu Ouvrir un pipeline](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-menu.png)
4. <span data-ttu-id="4ec4a-293">Vérifiez que vous voyez hello HDInsightHive activité hello pipeline.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-293">Confirm that you see hello HDInsightHive activity in hello pipeline.</span></span>

    ![Vue Ouvrir un pipeline](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-view.png)

    <span data-ttu-id="4ec4a-295">toonavigate sauvegarder toohello de vue précédente, cliquez sur **Data factory** dans le menu de navigation hello haut hello.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-295">toonavigate back toohello previous view, click **Data factory** in hello breadcrumb menu at hello top.</span></span>
5. <span data-ttu-id="4ec4a-296">Bonjour **vue de diagramme**, double-cliquez sur le jeu de données hello **AzureBlobInput**.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-296">In hello **Diagram View**, double-click hello dataset **AzureBlobInput**.</span></span> <span data-ttu-id="4ec4a-297">Confirmer que la tranche hello est **prêt** état.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-297">Confirm that hello slice is in **Ready** state.</span></span> <span data-ttu-id="4ec4a-298">Il peut prendre quelques minutes pour hello tranche tooshow dans l’état Ready.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-298">It may take a couple of minutes for hello slice tooshow up in Ready state.</span></span> <span data-ttu-id="4ec4a-299">Si elle ne se produit pas une fois que vous patientez un moment, consultez si vous avez des fichiers d’entrée hello (input.log) placé dans le conteneur de droite hello (adfgetstarted) et de dossier (inputdata).</span><span class="sxs-lookup"><span data-stu-id="4ec4a-299">If it does not happen after you wait for sometime, see if you have hello input file (input.log) placed in hello right container (adfgetstarted) and folder (inputdata).</span></span>

   ![Segment d’entrée dans l’état Prêt](./media/data-factory-build-your-first-pipeline-using-editor/input-slice-ready.png)
6. <span data-ttu-id="4ec4a-301">Cliquez sur **X** tooclose **AzureBlobInput** panneau.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-301">Click **X** tooclose **AzureBlobInput** blade.</span></span>
7. <span data-ttu-id="4ec4a-302">Bonjour **vue de diagramme**, double-cliquez sur le jeu de données hello **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-302">In hello **Diagram View**, double-click hello dataset **AzureBlobOutput**.</span></span> <span data-ttu-id="4ec4a-303">Vous voyez ce secteur hello qui est en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-303">You see that hello slice that is currently being processed.</span></span>

   ![Jeu de données](./media/data-factory-build-your-first-pipeline-using-editor/dataset-blade.png)
8. <span data-ttu-id="4ec4a-305">Lorsque le traitement est terminé, vous consultez la section hello dans **prêt** état.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-305">When processing is done, you see hello slice in **Ready** state.</span></span>

   ![Jeu de données](./media/data-factory-build-your-first-pipeline-using-editor/dataset-slice-ready.png)  

   > [!IMPORTANT]
   > <span data-ttu-id="4ec4a-307">La création d’un cluster HDInsight à la demande prend généralement un certain temps (environ 20 minutes).</span><span class="sxs-lookup"><span data-stu-id="4ec4a-307">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="4ec4a-308">Par conséquent, attendez que le pipeline de hello prennent trop **environ 30 minutes** tooprocess hello tranche.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-308">Therefore, expect hello pipeline too      take **approximately 30 minutes** tooprocess hello slice.</span></span>
   >
   >

9. <span data-ttu-id="4ec4a-309">Lorsque la tranche de hello est à **prêt** d’état, vérifiez hello **partitioneddata** dossier Bonjour **adfgetstarted** conteneur dans votre stockage d’objets blob pour hello les données de sortie.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-309">When hello slice is in **Ready** state, check hello **partitioneddata** folder in hello **adfgetstarted** container in your blob storage for hello output data.</span></span>  

   ![données de sortie](./media/data-factory-build-your-first-pipeline-using-editor/three-ouptut-files.png)
10. <span data-ttu-id="4ec4a-311">Cliquez sur Détails de toosee hello tranche sur celui-ci dans un **tranche de données** panneau.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-311">Click hello slice toosee details about it in a **Data slice** blade.</span></span>

   ![Détails de la tranche](./media/data-factory-build-your-first-pipeline-using-editor/data-slice-details.png)  
11. <span data-ttu-id="4ec4a-313">Cliquez sur une activité à exécuter dans hello **liste s’exécute l’activité** toosee des détails sur une activité exécuter (activité Hive dans notre scénario) dans un **détails de la série activité** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-313">Click an activity run in hello **Activity runs list** toosee details about an activity run (Hive activity in our scenario) in an **Activity run details** window.</span></span>   

   ![Détails de l'exécution d'activité](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-blade.png)    

   <span data-ttu-id="4ec4a-315">À partir de fichiers de journal hello, vous pouvez voir la requête Hive hello qui a été exécutée et les informations d’état.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-315">From hello log files, you can see hello Hive query that was executed and status information.</span></span> <span data-ttu-id="4ec4a-316">Ces journaux sont utiles pour résoudre les problèmes.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-316">These logs are useful for troubleshooting any issues.</span></span>
   <span data-ttu-id="4ec4a-317">Consultez l’article [Surveillance et gestion des pipelines d’Azure Data Factory](data-factory-monitor-manage-pipelines.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-317">See [Monitor and manage pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) article for more details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4ec4a-318">fichier d’entrée de Hello est supprimé lors de la tranche de hello est traitée avec succès.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-318">hello input file gets deleted when hello slice is processed successfully.</span></span> <span data-ttu-id="4ec4a-319">Par conséquent, si vous souhaitez tranche de hello toorerun ou que vous hello didacticiel à nouveau, téléchargez hello d’entrée (input.log) toohello inputdata dossier des fichiers du conteneur d’adfgetstarted hello.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-319">Therefore, if you want toorerun hello slice or do hello tutorial again, upload hello input file (input.log) toohello inputdata folder of hello adfgetstarted container.</span></span>
>
>

### <a name="monitor-pipeline-using-monitor--manage-app"></a><span data-ttu-id="4ec4a-320">Surveiller le pipeline à l’aide de l’application de surveillance et de gestion</span><span class="sxs-lookup"><span data-stu-id="4ec4a-320">Monitor pipeline using Monitor & Manage App</span></span>
<span data-ttu-id="4ec4a-321">Vous pouvez également utiliser le moniteur et gérer les applications toomonitor vos pipelines.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-321">You can also use Monitor & Manage application toomonitor your pipelines.</span></span> <span data-ttu-id="4ec4a-322">Pour en savoir plus sur l’utilisation de cette application, consultez l’article [Surveiller et gérer les pipelines Azure Data Factory à l’aide de l’application de surveillance et gestion](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="4ec4a-322">For detailed information about using this application, see [Monitor and manage Azure Data Factory pipelines using Monitoring and Management App](data-factory-monitor-manage-app.md).</span></span>

1. <span data-ttu-id="4ec4a-323">Cliquez sur **moniteur & gérer** vignette sur la page d’accueil hello pour votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-323">Click **Monitor & Manage** tile on hello home page for your data factory.</span></span>

    ![Vignette Surveiller et gérer](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-tile.png)
2. <span data-ttu-id="4ec4a-325">**L’application de surveillance et de gestion** devrait s’afficher.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-325">You should see **Monitor & Manage application**.</span></span> <span data-ttu-id="4ec4a-326">Hello de modification **l’heure de début** et **heure de fin** toomatch début et fin de votre pipeline, puis cliquez sur **appliquer**.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-326">Change hello **Start time** and **End time** toomatch start and end times of your pipeline, and click **Apply**.</span></span>

    ![Application de surveillance et gestion](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-app.png)
3. <span data-ttu-id="4ec4a-328">Sélectionnez une fenêtre d’activité Bonjour **Windows de l’activité** liste toosee des informations à son.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-328">Select an activity window in hello **Activity Windows** list toosee details about it.</span></span>

    ![Détails de la fenêtre d’activité](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-details.png)

## <a name="summary"></a><span data-ttu-id="4ec4a-330">Résumé</span><span class="sxs-lookup"><span data-stu-id="4ec4a-330">Summary</span></span>
<span data-ttu-id="4ec4a-331">Dans ce didacticiel, vous avez créé un Azure data factory tooprocess de données en exécutant le script Hive sur un cluster de hadoop HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-331">In this tutorial, you created an Azure data factory tooprocess data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="4ec4a-332">Vous avez utilisé hello éditeur Data Factory dans Bonjour Azure toodo portail Bonjour comme suit :</span><span class="sxs-lookup"><span data-stu-id="4ec4a-332">You used hello Data Factory Editor in hello Azure portal toodo hello following steps:</span></span>  

1. <span data-ttu-id="4ec4a-333">Création d’une **fabrique de données**Azure.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-333">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="4ec4a-334">Création de deux **services liés**:</span><span class="sxs-lookup"><span data-stu-id="4ec4a-334">Created two **linked services**:</span></span>
   1. <span data-ttu-id="4ec4a-335">**Le stockage Azure** lié service toolink votre stockage d’objets blob Azure qui contient la fabrique de données toohello les fichiers d’entrée/sortie.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-335">**Azure Storage** linked service toolink your Azure blob storage that holds input/output files toohello data factory.</span></span>
   2. <span data-ttu-id="4ec4a-336">**Azure HDInsight** à la demande liée service toolink une fabrique de données à la demande HDInsight Hadoop cluster toohello.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-336">**Azure HDInsight** on-demand linked service toolink an on-demand HDInsight Hadoop cluster toohello data factory.</span></span> <span data-ttu-id="4ec4a-337">Azure Data Factory crée un HDInsight Hadoop données d’entrée de cluster juste-à-temps tooprocess et générer les données de sortie.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-337">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time tooprocess input data and produce output data.</span></span>
3. <span data-ttu-id="4ec4a-338">Créé deux **jeux de données**, qui décrivent les données d’entrée et de sortie pour l’activité HDInsight Hive dans le pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-338">Created two **datasets**, which describe input and output data for HDInsight Hive activity in hello pipeline.</span></span>
4. <span data-ttu-id="4ec4a-339">Création d’un **pipeline** avec une activité **Hive HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-339">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ec4a-340">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4ec4a-340">Next Steps</span></span>
<span data-ttu-id="4ec4a-341">Dans cet article, vous avez créé un pipeline avec une activité de transformation (Activité HDInsight) qui exécute un script Hive sur un cluster HDInsight à la demande.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-341">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand HDInsight cluster.</span></span> <span data-ttu-id="4ec4a-342">toosee toouse un activité de copie toocopy des données d’une tooAzure d’objets Blob Azure SQL, voir [didacticiel : copier des données à partir d’un tooAzure d’objets blob Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="4ec4a-342">toosee how toouse a Copy Activity toocopy data from an Azure Blob tooAzure SQL, see [Tutorial: Copy data from an Azure blob tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="4ec4a-343">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="4ec4a-343">See Also</span></span>
| <span data-ttu-id="4ec4a-344">Rubrique</span><span class="sxs-lookup"><span data-stu-id="4ec4a-344">Topic</span></span> | <span data-ttu-id="4ec4a-345">Description</span><span class="sxs-lookup"><span data-stu-id="4ec4a-345">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="4ec4a-346">Pipelines</span><span class="sxs-lookup"><span data-stu-id="4ec4a-346">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="4ec4a-347">Cet article vous aidera à comprendre les pipelines et les activités dans Azure Data Factory et comment toouse les tooconstruct bout en bout piloté par les données des flux de travail pour votre entreprise ou votre scénario.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-347">This article helps you understand pipelines and activities in Azure Data Factory and how toouse them tooconstruct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="4ec4a-348">Groupes de données</span><span class="sxs-lookup"><span data-stu-id="4ec4a-348">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="4ec4a-349">Cet article vous aide à comprendre les jeux de données dans Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-349">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="4ec4a-350">Planification et exécution</span><span class="sxs-lookup"><span data-stu-id="4ec4a-350">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="4ec4a-351">Cet article explique les aspects de planification et l’exécution de hello du modèle d’application Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-351">This article explains hello scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="4ec4a-352">Surveiller et gérer les pipelines Azure Data Factory à l’aide de la nouvelle application de surveillance et gestion.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-352">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="4ec4a-353">Cet article décrit comment toomonitor, gérer et déboguer des pipelines à l’aide de hello analyse & application de gestion.</span><span class="sxs-lookup"><span data-stu-id="4ec4a-353">This article describes how toomonitor, manage, and debug pipelines using hello Monitoring & Management App.</span></span> |
