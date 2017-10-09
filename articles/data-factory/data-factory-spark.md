---
title: "les programmes à partir d’Azure Data Factory aaaInvoke Spark | Documents Microsoft"
description: "Découvrez comment les programmes de Spark tooinvoke à partir d’un à l’aide de la fabrique de données Azure hello activité MapReduce."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: fd98931c-cab5-4d66-97cb-4c947861255c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: f88943ece7ee3d21dedbd857609f1b2713b62741
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="invoke-spark-programs-from-azure-data-factory-pipelines"></a><span data-ttu-id="76d5d-103">Appeler des programmes Spark à partir des pipelines Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="76d5d-103">Invoke Spark programs from Azure Data Factory pipelines</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="76d5d-104">Activité Hive</span><span class="sxs-lookup"><span data-stu-id="76d5d-104">Hive Activity</span></span>](data-factory-hive-activity.md)
> * [<span data-ttu-id="76d5d-105">Activité pig</span><span class="sxs-lookup"><span data-stu-id="76d5d-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="76d5d-106">Activité MapReduce</span><span class="sxs-lookup"><span data-stu-id="76d5d-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="76d5d-107">Activité de diffusion en continu Hadoop</span><span class="sxs-lookup"><span data-stu-id="76d5d-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="76d5d-108">Activité Spark</span><span class="sxs-lookup"><span data-stu-id="76d5d-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="76d5d-109">Activité d’exécution par lot Machine Learning</span><span class="sxs-lookup"><span data-stu-id="76d5d-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="76d5d-110">Activité des ressources de mise à jour de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="76d5d-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="76d5d-111">Activité de procédure stockée</span><span class="sxs-lookup"><span data-stu-id="76d5d-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="76d5d-112">Activité U-SQL Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="76d5d-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="76d5d-113">Activité personnalisée .NET</span><span class="sxs-lookup"><span data-stu-id="76d5d-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="introduction"></a><span data-ttu-id="76d5d-114">Introduction</span><span class="sxs-lookup"><span data-stu-id="76d5d-114">Introduction</span></span>
<span data-ttu-id="76d5d-115">Activité de Spark est un des hello [activités de transformation des données](data-factory-data-transformation-activities.md) pris en charge par Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="76d5d-115">Spark Activity is one of hello [data transformation activities](data-factory-data-transformation-activities.md) supported by Azure Data Factory.</span></span> <span data-ttu-id="76d5d-116">Cette activité s’exécute hello spécifiée programme Spark sur votre cluster Apache Spark dans Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="76d5d-116">This activity runs hello specified Spark program on your Apache Spark cluster in Azure HDInsight.</span></span>    

> [!IMPORTANT]
> - <span data-ttu-id="76d5d-117">L’activité Spark ne prend pas en charge les clusters Spark HDInsight qui utilisent Azure Data Lake Store en tant que stockage principal.</span><span class="sxs-lookup"><span data-stu-id="76d5d-117">Spark Activity does not support HDInsight Spark clusters that use an Azure Data Lake Store as primary storage.</span></span>
> - <span data-ttu-id="76d5d-118">L’activité Spark prend en charge uniquement les clusters Spark HDInsight existants (c’est-à-dire vos propres clusters).</span><span class="sxs-lookup"><span data-stu-id="76d5d-118">Spark Activity supports only existing (your own) HDInsight Spark clusters.</span></span> <span data-ttu-id="76d5d-119">Elle ne prend pas en charge les services liés HDInsight à la demande.</span><span class="sxs-lookup"><span data-stu-id="76d5d-119">It does not support an on-demand HDInsight linked service.</span></span>

## <a name="walkthrough-create-a-pipeline-with-spark-activity"></a><span data-ttu-id="76d5d-120">Procédure pas à pas : création d’un pipeline avec l’activité Spark</span><span class="sxs-lookup"><span data-stu-id="76d5d-120">Walkthrough: create a pipeline with Spark activity</span></span>
<span data-ttu-id="76d5d-121">Ici, les étapes classiques de hello toocreate un pipeline de fabrique de données avec une activité Spark.</span><span class="sxs-lookup"><span data-stu-id="76d5d-121">Here are hello typical steps toocreate a Data Factory pipeline with a Spark activity.</span></span>  

1. <span data-ttu-id="76d5d-122">Créer une fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="76d5d-122">Create a data factory.</span></span>
2. <span data-ttu-id="76d5d-123">Créer un toolink de service lié Azure Storage de votre stockage Azure qui est associé à votre fabrique de données toohello cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="76d5d-123">Create an Azure Storage linked service toolink your Azure storage that is associated with your HDInsight Spark cluster toohello data factory.</span></span>     
2. <span data-ttu-id="76d5d-124">Créer un toolink de service lié HDInsight Azure de votre cluster Apache Spark dans Azure HDInsight toohello data factory.</span><span class="sxs-lookup"><span data-stu-id="76d5d-124">Create an Azure HDInsight linked service toolink your Apache Spark cluster in Azure HDInsight toohello data factory.</span></span>
3. <span data-ttu-id="76d5d-125">Créer un jeu de données qui fait référence toohello lié Azure Storage service.</span><span class="sxs-lookup"><span data-stu-id="76d5d-125">Create a dataset that refers toohello Azure Storage linked service.</span></span> <span data-ttu-id="76d5d-126">Actuellement, vous devez spécifier un jeu de données de sortie d’une activité même si aucune sortie n’est produite.</span><span class="sxs-lookup"><span data-stu-id="76d5d-126">Currently, you must specify an output dataset for an activity even if there is no output being produced.</span></span>  
4. <span data-ttu-id="76d5d-127">Créer un pipeline avec activités Spark qui fait référence de service lié HDInsight de toohello créé dans #2.</span><span class="sxs-lookup"><span data-stu-id="76d5d-127">Create a pipeline with Spark activity that refers toohello HDInsight linked service created in #2.</span></span> <span data-ttu-id="76d5d-128">activité Hello est configurée avec hello le jeu de données créé à l’étape précédente de hello comme un jeu de données de sortie.</span><span class="sxs-lookup"><span data-stu-id="76d5d-128">hello activity is configured with hello dataset you created in hello previous step as an output dataset.</span></span> <span data-ttu-id="76d5d-129">jeu de données de sortie Hello est les lecteurs hello planification (horaire, quotidienne, etc.).</span><span class="sxs-lookup"><span data-stu-id="76d5d-129">hello output dataset is what drives hello schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="76d5d-130">Par conséquent, vous devez spécifier le jeu de données de sortie hello même si l’activité hello ne produit pas vraiment une sortie.</span><span class="sxs-lookup"><span data-stu-id="76d5d-130">Therefore, you must specify hello output dataset even though hello activity does not really produce an output.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="76d5d-131">Composants requis</span><span class="sxs-lookup"><span data-stu-id="76d5d-131">Prerequisites</span></span>
1. <span data-ttu-id="76d5d-132">Créer un **compte de stockage Azure à usage général** en suivant les instructions de procédure pas à pas hello : [créer un compte de stockage](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="76d5d-132">Create a **general-purpose Azure Storage Account** by following instructions in hello walkthrough: [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>  
2. <span data-ttu-id="76d5d-133">Créer un **cluster Apache Spark dans Azure HDInsight** en suivant les instructions dans le didacticiel de hello : [cluster créer Apache Spark dans Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="76d5d-133">Create an **Apache Spark cluster in Azure HDInsight** by following instructions in hello tutorial: [Create Apache Spark cluster in Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> <span data-ttu-id="76d5d-134">Associer un compte de stockage Azure hello que vous avez créé à l’étape 1 de # avec ce cluster.</span><span class="sxs-lookup"><span data-stu-id="76d5d-134">Associate hello Azure storage account you created in step #1 with this cluster.</span></span>  
3. <span data-ttu-id="76d5d-135">Téléchargez et lisez le fichier de script python hello **test.py** situé à : [https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py](https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py).</span><span class="sxs-lookup"><span data-stu-id="76d5d-135">Download and review hello python script file **test.py** located at: [https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py](https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py).</span></span>  
3.  <span data-ttu-id="76d5d-136">Télécharger **test.py** toohello **pyFiles** dossier Bonjour **adfspark** conteneur dans votre stockage d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="76d5d-136">Upload **test.py** toohello **pyFiles** folder in hello **adfspark** container in your Azure Blob storage.</span></span> <span data-ttu-id="76d5d-137">Créer le conteneur de hello et le dossier de hello s’ils n’existent pas.</span><span class="sxs-lookup"><span data-stu-id="76d5d-137">Create hello container and hello folder if they do not exist.</span></span>

### <a name="create-data-factory"></a><span data-ttu-id="76d5d-138">Créer une fabrique de données</span><span class="sxs-lookup"><span data-stu-id="76d5d-138">Create data factory</span></span>
<span data-ttu-id="76d5d-139">Commençons par créer la fabrique de données hello dans cette étape.</span><span class="sxs-lookup"><span data-stu-id="76d5d-139">Let's start with creating hello data factory in this step.</span></span>

1. <span data-ttu-id="76d5d-140">Connectez-vous à toohello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="76d5d-140">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="76d5d-141">Cliquez sur **nouveau** sur menu gauche hello **données + Analytique**, puis cliquez sur **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="76d5d-141">Click **NEW** on hello left menu, click **Data + Analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="76d5d-142">Bonjour **nouvelle fabrique de données** panneau, entrez **SparkDF** pour hello nom.</span><span class="sxs-lookup"><span data-stu-id="76d5d-142">In hello **New data factory** blade, enter **SparkDF** for hello Name.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="76d5d-143">nom de Hello de fabrique de données Azure hello doit être **global unique**.</span><span class="sxs-lookup"><span data-stu-id="76d5d-143">hello name of hello Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="76d5d-144">Si vous voyez l’erreur de hello : **nom de fabrique de données « SparkDF » n’est pas disponible**.</span><span class="sxs-lookup"><span data-stu-id="76d5d-144">If you see hello error: **Data factory name “SparkDF” is not available**.</span></span> <span data-ttu-id="76d5d-145">Modifier le nom hello hello fabrique de données (par exemple, yournameSparkDFdate et essayez à nouveau de créer.</span><span class="sxs-lookup"><span data-stu-id="76d5d-145">Change hello name of hello data factory (for example, yournameSparkDFdate, and try creating again.</span></span> <span data-ttu-id="76d5d-146">Consultez la rubrique [Data Factory - Règles d'affectation des noms](data-factory-naming-rules.md) pour savoir comment nommer les artefacts Data Factory.</span><span class="sxs-lookup"><span data-stu-id="76d5d-146">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>   
4. <span data-ttu-id="76d5d-147">Sélectionnez hello **abonnement Azure** où vous souhaitez toobe de fabrique de données hello créé.</span><span class="sxs-lookup"><span data-stu-id="76d5d-147">Select hello **Azure subscription** where you want hello data factory toobe created.</span></span>
5. <span data-ttu-id="76d5d-148">Sélectionnez un **groupe de ressources** Azure existant ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="76d5d-148">Select an existing **resource group** or create an Azure resource group.</span></span>
6. <span data-ttu-id="76d5d-149">Sélectionnez **toodashboard du code confidentiel** option.</span><span class="sxs-lookup"><span data-stu-id="76d5d-149">Select **Pin toodashboard** option.</span></span>  
6. <span data-ttu-id="76d5d-150">Cliquez sur **créer** sur hello **nouvelle fabrique de données** panneau.</span><span class="sxs-lookup"><span data-stu-id="76d5d-150">Click **Create** on hello **New data factory** blade.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="76d5d-151">instances de fabrique de données toocreate, vous devez être membre du hello [collaborateur de fabrique de données](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) rôle au niveau de groupe de ressource d’abonnement hello.</span><span class="sxs-lookup"><span data-stu-id="76d5d-151">toocreate Data Factory instances, you must be a member of hello [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at hello subscription/resource group level.</span></span>
7. <span data-ttu-id="76d5d-152">Vous voyez la fabrique de données hello en cours de création dans hello **tableau de bord** de hello portail Azure comme suit :</span><span class="sxs-lookup"><span data-stu-id="76d5d-152">You see hello data factory being created in hello **dashboard** of hello Azure portal as follows:</span></span>   
8. <span data-ttu-id="76d5d-153">Une fois que la fabrique de données hello a été créé avec succès, vous voyez page de fabrique de données hello, qui vous indique hello contenu hello fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="76d5d-153">After hello data factory has been created successfully, you see hello data factory page, which shows you hello contents of hello data factory.</span></span> <span data-ttu-id="76d5d-154">Si vous ne voyez pas la page de fabrique de données hello, cliquez sur mosaïque hello pour votre fabrique de données sur le tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="76d5d-154">If you do not see hello data factory page, click hello tile for your data factory on hello dashboard.</span></span>

    ![Panneau Data Factory](./media/data-factory-spark/data-factory-blade.png)

### <a name="create-linked-services"></a><span data-ttu-id="76d5d-156">Créez des services liés</span><span class="sxs-lookup"><span data-stu-id="76d5d-156">Create linked services</span></span>
<span data-ttu-id="76d5d-157">Dans cette étape, vous créez deux services liés, un toolink votre fabrique de données tooyour cluster Spark et hello autres toolink votre fabrique de données de stockage Azure tooyour.</span><span class="sxs-lookup"><span data-stu-id="76d5d-157">In this step, you create two linked services, one toolink your Spark cluster tooyour data factory, and hello other toolink your Azure storage tooyour data factory.</span></span>  

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="76d5d-158">Créer le service lié Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="76d5d-158">Create Azure Storage linked service</span></span>
<span data-ttu-id="76d5d-159">Dans cette étape, vous liez votre fabrique de données tooyour compte Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="76d5d-159">In this step, you link your Azure Storage account tooyour data factory.</span></span> <span data-ttu-id="76d5d-160">Un jeu de données que vous créez dans une étape ultérieure de cette procédure fait référence toothis lié service.</span><span class="sxs-lookup"><span data-stu-id="76d5d-160">A dataset you create in a step later in this walkthrough refers toothis linked service.</span></span> <span data-ttu-id="76d5d-161">Hello service lié HDInsight que vous définissez dans l’étape suivante de hello fait référence toothis lié service.</span><span class="sxs-lookup"><span data-stu-id="76d5d-161">hello HDInsight linked service that you define in hello next step refers toothis linked service too.</span></span>  

1. <span data-ttu-id="76d5d-162">Cliquez sur **auteur et déployer** sur hello **Data Factory** Panneau de votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="76d5d-162">Click **Author and deploy** on hello **Data Factory** blade for your data factory.</span></span> <span data-ttu-id="76d5d-163">Vous devez voir hello éditeur Data Factory.</span><span class="sxs-lookup"><span data-stu-id="76d5d-163">You should see hello Data Factory Editor.</span></span>
2. <span data-ttu-id="76d5d-164">Cliquez sur **Nouveau magasin de données** et choisissez **Stockage Azure**.</span><span class="sxs-lookup"><span data-stu-id="76d5d-164">Click **New data store** and choose **Azure storage**.</span></span>

   ![Nouveau magasin de données - Stockage Azure - menu](./media/data-factory-spark/new-data-store-azure-storage-menu.png)
3. <span data-ttu-id="76d5d-166">Vous devez voir hello **script JSON** pour la création d’un stockage Azure des service dans l’éditeur de hello lié.</span><span class="sxs-lookup"><span data-stu-id="76d5d-166">You should see hello **JSON script** for creating an Azure Storage linked service in hello editor.</span></span>

   ![Service lié Azure Storage](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. <span data-ttu-id="76d5d-168">Remplacez **nom de compte** et **clé de compte** avec la clé de hello accès et le nom de votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="76d5d-168">Replace **account name** and **account key** with hello name and access key of your Azure storage account.</span></span> <span data-ttu-id="76d5d-169">toolearn comment accéder à votre espace de stockage tooget de clé, consultez hello plus d’informations sur comment tooview, copier et régénérer stockage touches d’accès [gérer votre compte de stockage](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="76d5d-169">toolearn how tooget your storage access key, see hello information about how tooview, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
5. <span data-ttu-id="76d5d-170">toodeploy hello service lié, cliquez sur **déployer** sur la barre de commandes hello.</span><span class="sxs-lookup"><span data-stu-id="76d5d-170">toodeploy hello linked service, click **Deploy** on hello command bar.</span></span> <span data-ttu-id="76d5d-171">Une fois hello service lié est déployé avec succès, hello **Draft-1** fenêtre doit disparaître et vous voyez **AzureStorageLinkedService** dans l’arborescence hello sur hello gauche.</span><span class="sxs-lookup"><span data-stu-id="76d5d-171">After hello linked service is deployed successfully, hello **Draft-1** window should disappear and you see **AzureStorageLinkedService** in hello tree view on hello left.</span></span>

#### <a name="create-hdinsight-linked-service"></a><span data-ttu-id="76d5d-172">Créer un service lié Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="76d5d-172">Create HDInsight linked service</span></span>
<span data-ttu-id="76d5d-173">Dans cette étape, vous créez toolink du service lié HDInsight Azure votre fabrique de données toohello cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="76d5d-173">In this step, you create Azure HDInsight linked service toolink your HDInsight Spark cluster toohello data factory.</span></span> <span data-ttu-id="76d5d-174">cluster HDInsight de Hello est programme de Spark hello utilisé toorun spécifié dans l’activité de Spark hello du pipeline hello dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="76d5d-174">hello HDInsight cluster is used toorun hello Spark program specified in hello Spark activity of hello pipeline in this sample.</span></span>  

1. <span data-ttu-id="76d5d-175">Si ce bouton n'est pas affiché dans la barre d'outils, cliquez sur **... Plus** dans la barre d’outils de hello, cliquez sur **nouveau calcul**, puis cliquez sur **cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="76d5d-175">Click **... More** on hello toolbar, click **New compute**, and then click **HDInsight cluster**.</span></span>

    ![Créer un service lié Azure HDInsight](media/data-factory-spark/new-hdinsight-linked-service.png)
2. <span data-ttu-id="76d5d-177">Copiez et collez hello suivant extrait toohello **Draft-1** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="76d5d-177">Copy and paste hello following snippet toohello **Draft-1** window.</span></span> <span data-ttu-id="76d5d-178">Dans l’éditeur JSON hello, procédez comme hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="76d5d-178">In hello JSON editor, do hello following steps:</span></span>
    1. <span data-ttu-id="76d5d-179">Spécifiez hello **URI** pour hello HDInsight Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="76d5d-179">Specify hello **URI** for hello HDInsight Spark cluster.</span></span> <span data-ttu-id="76d5d-180">Par exemple : `https://<sparkclustername>.azurehdinsight.net/`.</span><span class="sxs-lookup"><span data-stu-id="76d5d-180">For example: `https://<sparkclustername>.azurehdinsight.net/`.</span></span>
    2. <span data-ttu-id="76d5d-181">Spécifiez le nom hello Hello **utilisateur** qui a cluster Spark de toohello accès.</span><span class="sxs-lookup"><span data-stu-id="76d5d-181">Specify hello name of hello **user** who has access toohello Spark cluster.</span></span>
    3. <span data-ttu-id="76d5d-182">Spécifiez hello **mot de passe** pour l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="76d5d-182">Specify hello **password** for user.</span></span>
    4. <span data-ttu-id="76d5d-183">Spécifiez hello **service lié Azure Storage** associé hello cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="76d5d-183">Specify hello **Azure Storage linked service** that is associated with hello HDInsight Spark cluster.</span></span> <span data-ttu-id="76d5d-184">Dans cet exemple, il s’agit de **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="76d5d-184">In this example, it is: **AzureStorageLinkedService**.</span></span>

    ```json
    {
        "name": "HDInsightLinkedService",
        "properties": {
            "type": "HDInsight",
            "typeProperties": {
                "clusterUri": "https://<sparkclustername>.azurehdinsight.net/",
                "userName": "admin",
                "password": "**********",
                "linkedServiceName": "AzureStorageLinkedService"
            }
        }
    }
    ```

    > [!IMPORTANT]
    > - <span data-ttu-id="76d5d-185">L’activité Spark ne prend pas en charge les clusters Spark HDInsight qui utilisent Azure Data Lake Store en tant que stockage principal.</span><span class="sxs-lookup"><span data-stu-id="76d5d-185">Spark Activity does not support HDInsight Spark clusters that use an Azure Data Lake Store as primary storage.</span></span>
    > - <span data-ttu-id="76d5d-186">L’activité Spark prend en charge uniquement le cluster Spark HDInsight existant (c’est-à-dire votre propre cluster).</span><span class="sxs-lookup"><span data-stu-id="76d5d-186">Spark Activity supports only existing (your own) HDInsight Spark cluster.</span></span> <span data-ttu-id="76d5d-187">Elle ne prend pas en charge les services liés HDInsight à la demande.</span><span class="sxs-lookup"><span data-stu-id="76d5d-187">It does not support an on-demand HDInsight linked service.</span></span>

    <span data-ttu-id="76d5d-188">Consultez [Service lié HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) pour plus d’informations sur hello HDInsight le service lié.</span><span class="sxs-lookup"><span data-stu-id="76d5d-188">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details about hello HDInsight linked service.</span></span>
3.  <span data-ttu-id="76d5d-189">toodeploy hello service lié, cliquez sur **déployer** sur la barre de commandes hello.</span><span class="sxs-lookup"><span data-stu-id="76d5d-189">toodeploy hello linked service, click **Deploy** on hello command bar.</span></span>  

### <a name="create-output-dataset"></a><span data-ttu-id="76d5d-190">Créer un jeu de données de sortie</span><span class="sxs-lookup"><span data-stu-id="76d5d-190">Create output dataset</span></span>
<span data-ttu-id="76d5d-191">jeu de données de sortie Hello est les lecteurs hello planification (horaire, quotidienne, etc.).</span><span class="sxs-lookup"><span data-stu-id="76d5d-191">hello output dataset is what drives hello schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="76d5d-192">Par conséquent, vous devez spécifier un jeu de données de sortie pour l’activité de spark hello dans le pipeline de hello même si l’activité hello ne produit pas vraiment de sortie.</span><span class="sxs-lookup"><span data-stu-id="76d5d-192">Therefore, you must specify an output dataset for hello spark activity in hello pipeline even though hello activity does not really produce any output.</span></span> <span data-ttu-id="76d5d-193">Spécification d’un jeu de données d’entrée pour l’activité de hello est facultative.</span><span class="sxs-lookup"><span data-stu-id="76d5d-193">Specifying an input dataset for hello activity is optional.</span></span>

1. <span data-ttu-id="76d5d-194">Bonjour **éditeur Data Factory**, cliquez sur **... Plus** dans la barre de commandes hello, cliquez sur **nouveau dataset**, puis sélectionnez **le stockage Blob Azure**.</span><span class="sxs-lookup"><span data-stu-id="76d5d-194">In hello **Data Factory Editor**, click **... More** on hello command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>  
2. <span data-ttu-id="76d5d-195">Copiez et collez hello suivant fenêtre toohello Draft-1.</span><span class="sxs-lookup"><span data-stu-id="76d5d-195">Copy and paste hello following snippet toohello Draft-1 window.</span></span> <span data-ttu-id="76d5d-196">extrait de code Hello JSON définit un jeu de données appelée **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="76d5d-196">hello JSON snippet defines a dataset called **OutputDataset**.</span></span> <span data-ttu-id="76d5d-197">En outre, vous spécifiez que les résultats de hello sont stockés dans le conteneur d’objets blob hello appelé **adfspark** et dossier hello appelé **pyFiles/sortie**.</span><span class="sxs-lookup"><span data-stu-id="76d5d-197">In addition, you specify that hello results are stored in hello blob container called **adfspark** and hello folder called **pyFiles/output**.</span></span> <span data-ttu-id="76d5d-198">Comme mentionné précédemment, ce jeu de données est un jeu de données factice.</span><span class="sxs-lookup"><span data-stu-id="76d5d-198">As mentioned earlier, this dataset is a dummy dataset.</span></span> <span data-ttu-id="76d5d-199">programme de Spark Hello dans cet exemple ne produit pas de sortie.</span><span class="sxs-lookup"><span data-stu-id="76d5d-199">hello Spark program in this example does not produce any output.</span></span> <span data-ttu-id="76d5d-200">Hello **disponibilité** section spécifie ce jeu de données de sortie hello est produite quotidiennement.</span><span class="sxs-lookup"><span data-stu-id="76d5d-200">hello **availability** section specifies that hello output dataset is produced daily.</span></span>  

    ```json
    {
        "name": "OutputDataset",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "sparkoutput.txt",
                "folderPath": "adfspark/pyFiles/output",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": "\t"
                }
            },
            "availability": {
                "frequency": "Day",
                "interval": 1
            }
        }
    }
    ```
3. <span data-ttu-id="76d5d-201">toodeploy hello du jeu de données, cliquez sur **déployer** sur la barre de commandes hello.</span><span class="sxs-lookup"><span data-stu-id="76d5d-201">toodeploy hello dataset, click **Deploy** on hello command bar.</span></span>


### <a name="create-pipeline"></a><span data-ttu-id="76d5d-202">Création d’un pipeline</span><span class="sxs-lookup"><span data-stu-id="76d5d-202">Create pipeline</span></span>
<span data-ttu-id="76d5d-203">Dans cette étape, vous allez créer un pipeline avec une activité **HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="76d5d-203">In this step, you create a pipeline with a **HDInsightSpark** activity.</span></span> <span data-ttu-id="76d5d-204">Actuellement, le dataset de sortie est les lecteurs hello planification, vous devez donc créer un dataset de sortie même si l’activité hello ne produit pas de sortie.</span><span class="sxs-lookup"><span data-stu-id="76d5d-204">Currently, output dataset is what drives hello schedule, so you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="76d5d-205">Si l’activité hello n’accepte aucune entrée, vous pouvez ignorer le jeu de données d’entrée création hello.</span><span class="sxs-lookup"><span data-stu-id="76d5d-205">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span> <span data-ttu-id="76d5d-206">Par conséquent, aucun jeu de données d’entrée n’est spécifié dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="76d5d-206">Therefore, no input dataset is specified in this example.</span></span>

1. <span data-ttu-id="76d5d-207">Bonjour **éditeur Data Factory**, cliquez sur **... Plus** sur hello de barre de commandes, puis cliquez sur **nouveau pipeline**.</span><span class="sxs-lookup"><span data-stu-id="76d5d-207">In hello **Data Factory Editor**, click **… More** on hello command bar, and then click **New pipeline**.</span></span>
2. <span data-ttu-id="76d5d-208">Remplacez le script hello dans la fenêtre hello Draft-1 avec hello script suivant :</span><span class="sxs-lookup"><span data-stu-id="76d5d-208">Replace hello script in hello Draft-1 window with hello following script:</span></span>

    ```json
    {
        "name": "SparkPipeline",
        "properties": {
            "activities": [
                {
                    "type": "HDInsightSpark",
                    "typeProperties": {
                        "rootPath": "adfspark\\pyFiles",
                        "entryFilePath": "test.py",
                        "getDebugInfo": "Always"
                    },
                    "outputs": [
                        {
                            "name": "OutputDataset"
                        }
                    ],
                    "name": "MySparkActivity",
                    "linkedServiceName": "HDInsightLinkedService"
                }
            ],
            "start": "2017-02-05T00:00:00Z",
            "end": "2017-02-06T00:00:00Z"
        }
    }
    ```
    <span data-ttu-id="76d5d-209">Hello Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="76d5d-209">Note hello following points:</span></span>
    - <span data-ttu-id="76d5d-210">Hello **type** propriété a la valeur trop**HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="76d5d-210">hello **type** property is set too**HDInsightSpark**.</span></span>
    - <span data-ttu-id="76d5d-211">Hello **rootPath** est défini trop**adfspark\\pyFiles** où adfspark est le conteneur d’objets Blob Azure hello et pyFiles est un dossier précis dans le conteneur.</span><span class="sxs-lookup"><span data-stu-id="76d5d-211">hello **rootPath** is set too**adfspark\\pyFiles** where adfspark is hello Azure Blob container and pyFiles is fine folder in that container.</span></span> <span data-ttu-id="76d5d-212">Dans cet exemple, hello stockage d’objets Blob Azure est hello qui est associé au cluster de Spark hello.</span><span class="sxs-lookup"><span data-stu-id="76d5d-212">In this example, hello Azure Blob Storage is hello one that is associated with hello Spark cluster.</span></span> <span data-ttu-id="76d5d-213">Vous pouvez télécharger hello fichier tooa stockage Azure différent.</span><span class="sxs-lookup"><span data-stu-id="76d5d-213">You can upload hello file tooa different Azure Storage.</span></span> <span data-ttu-id="76d5d-214">Si vous procédez ainsi, vous pouvez créer un toolink de service lié Azure Storage cette fabrique de données de stockage compte toohello.</span><span class="sxs-lookup"><span data-stu-id="76d5d-214">If you do so, create an Azure Storage linked service toolink that storage account toohello data factory.</span></span> <span data-ttu-id="76d5d-215">Ensuite, spécifiez le nom hello du service de hello lié en tant que valeur pour hello **sparkJobLinkedService** propriété.</span><span class="sxs-lookup"><span data-stu-id="76d5d-215">Then, specify hello name of hello linked service as a value for hello **sparkJobLinkedService** property.</span></span> <span data-ttu-id="76d5d-216">Consultez [propriétés de l’activité de Spark](#spark-activity-properties) pour plus d’informations sur cette propriété et d’autres propriétés prises en charge par hello Spark activité.</span><span class="sxs-lookup"><span data-stu-id="76d5d-216">See [Spark Activity properties](#spark-activity-properties) for details about this property and other properties supported by hello Spark Activity.</span></span>  
    - <span data-ttu-id="76d5d-217">Hello **entryFilePath** a la valeur toohello **test.py**, qui est le fichier de python hello.</span><span class="sxs-lookup"><span data-stu-id="76d5d-217">hello **entryFilePath** is set toohello **test.py**, which is hello python file.</span></span>
    - <span data-ttu-id="76d5d-218">Hello **getDebugInfo** propriété a la valeur trop**toujours**, ce qui signifie que les fichiers journaux de hello est toujours généré (succès ou échec).</span><span class="sxs-lookup"><span data-stu-id="76d5d-218">hello **getDebugInfo** property is set too**Always**, which means hello log files are always generated (success or failure).</span></span>

        > [!IMPORTANT]
        > <span data-ttu-id="76d5d-219">Nous recommandons que vous ne définissez pas cette propriété trop`Always` dans un environnement de production, sauf si vous dépannez un problème.</span><span class="sxs-lookup"><span data-stu-id="76d5d-219">We recommend that you do not set this property too`Always` in a production environment unless you are troubleshooting an issue.</span></span>
    - <span data-ttu-id="76d5d-220">Hello **génère** section a un jeu de données de sortie.</span><span class="sxs-lookup"><span data-stu-id="76d5d-220">hello **outputs** section has one output dataset.</span></span> <span data-ttu-id="76d5d-221">Vous devez spécifier un jeu de données de sortie même si le programme de spark hello ne produit pas de sortie.</span><span class="sxs-lookup"><span data-stu-id="76d5d-221">You must specify an output dataset even if hello spark program does not produce any output.</span></span> <span data-ttu-id="76d5d-222">planification de hello lecteurs Hello sortie dataset pour le pipeline de hello (horaire, quotidienne, etc.).</span><span class="sxs-lookup"><span data-stu-id="76d5d-222">hello output dataset drives hello schedule for hello pipeline (hourly, daily, etc.).</span></span>  

        <span data-ttu-id="76d5d-223">Pour plus d’informations sur les propriétés hello pris en charge par l’activité de Spark, consultez [nouvelles propriétés de l’activité](#spark-activity-properties) section.</span><span class="sxs-lookup"><span data-stu-id="76d5d-223">For details about hello properties supported by Spark activity, see [Spark activity properties](#spark-activity-properties) section.</span></span>
3. <span data-ttu-id="76d5d-224">pipeline de hello toodeploy, cliquez sur **déployer** sur la barre de commandes hello.</span><span class="sxs-lookup"><span data-stu-id="76d5d-224">toodeploy hello pipeline, click **Deploy** on hello command bar.</span></span>

### <a name="monitor-pipeline"></a><span data-ttu-id="76d5d-225">Surveillance d’un pipeline</span><span class="sxs-lookup"><span data-stu-id="76d5d-225">Monitor pipeline</span></span>
1. <span data-ttu-id="76d5d-226">Cliquez sur **X** tooclose éditeur Data Factory panneaux et toonavigate sauvegarder toohello page d’accueil de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="76d5d-226">Click **X** tooclose Data Factory Editor blades and toonavigate back toohello Data Factory home page.</span></span> <span data-ttu-id="76d5d-227">Cliquez sur **analyse et gestion** hello toolaunch analyse de l’application dans un autre onglet.</span><span class="sxs-lookup"><span data-stu-id="76d5d-227">Click **Monitor and Manage** toolaunch hello monitoring application in another tab.</span></span>

    ![Mosaïque Surveiller et gérer](media/data-factory-spark/monitor-and-manage-tile.png)
2. <span data-ttu-id="76d5d-229">Hello de modification **l’heure de début** trop de filtre en haut de hello**2/1/2017**, puis cliquez sur **appliquer**.</span><span class="sxs-lookup"><span data-stu-id="76d5d-229">Change hello **Start time** filter at hello top too**2/1/2017**, and click **Apply**.</span></span>
3. <span data-ttu-id="76d5d-230">Vous devez voir qu’une seule fenêtre d’activité qu’il existe un seul jour entre hello début (2017-02-01) et de fin des heures (2017-02-02) du pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="76d5d-230">You should see only one activity window as there is only one day between hello start (2017-02-01) and end times (2017-02-02) of hello pipeline.</span></span> <span data-ttu-id="76d5d-231">Confirmer cette tranche de données hello est **prêt** état.</span><span class="sxs-lookup"><span data-stu-id="76d5d-231">Confirm that hello data slice is in **ready** state.</span></span>

    ![Pipeline d’analyse hello](media/data-factory-spark/monitor-and-manage-app.png)    
4. <span data-ttu-id="76d5d-233">Sélectionnez hello **fenêtre d’activité** toosee plus d’informations sur l’exécution de l’activité hello.</span><span class="sxs-lookup"><span data-stu-id="76d5d-233">Select hello **activity window** toosee details about hello activity run.</span></span> <span data-ttu-id="76d5d-234">S’il existe une erreur, vous consultez les détails à ce sujet dans le volet de droite hello.</span><span class="sxs-lookup"><span data-stu-id="76d5d-234">If there is an error, you see details about it in hello right pane.</span></span>

### <a name="verify-hello-results"></a><span data-ttu-id="76d5d-235">Vérifier les résultats de hello</span><span class="sxs-lookup"><span data-stu-id="76d5d-235">Verify hello results</span></span>

1. <span data-ttu-id="76d5d-236">Lancez le **bloc-notes Jupyter** pour votre cluster Spark HDInsight via l’URL suivante : https://NOMDUCLUSTER.azurehdinsight.net/jupyter.</span><span class="sxs-lookup"><span data-stu-id="76d5d-236">Launch **Jupyter notebook** for your HDInsight Spark cluster by navigating to: https://CLUSTERNAME.azurehdinsight.net/jupyter.</span></span> <span data-ttu-id="76d5d-237">Vous pouvez également lancer le tableau de bord de votre cluster Spark HDInsight, puis ouvrir le **bloc-notes Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="76d5d-237">You can also launch cluster dashboard for your HDInsight Spark cluster, and then launch **Jupyter Notebook**.</span></span>
2. <span data-ttu-id="76d5d-238">Cliquez sur **nouveau** -> **PySpark** toostart un nouvel ordinateur portable.</span><span class="sxs-lookup"><span data-stu-id="76d5d-238">Click **New** -> **PySpark** toostart a new notebook.</span></span>

    ![Nouveau bloc-notes Jupyter](media/data-factory-spark/jupyter-new-book.png)
3. <span data-ttu-id="76d5d-240">Exécution hello commande suivante copie/collage de texte hello et appuyez sur **MAJ + ENTRÉE** à fin hello d’instruction de deuxième hello.</span><span class="sxs-lookup"><span data-stu-id="76d5d-240">Run hello following command by copy/pasting hello text and pressing **SHIFT + ENTER** at hello end of hello second statement.</span></span>  

    ```sql
    %%sql

    SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"
    ```
4. <span data-ttu-id="76d5d-241">Vérifiez que les données de salutation à partir de la table de hvac hello :</span><span class="sxs-lookup"><span data-stu-id="76d5d-241">Confirm that you see hello data from hello hvac table:</span></span>  

    ![Résultats de la requête Jupyter](media/data-factory-spark/jupyter-notebook-results.png)

<span data-ttu-id="76d5d-243">Consultez la section relative à [l’exécution d’une requête SQL Spark](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md#run-a-hive-query-using-spark-sql) pour obtenir des instructions détaillées.</span><span class="sxs-lookup"><span data-stu-id="76d5d-243">See [Run a Spark SQL query](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md#run-a-hive-query-using-spark-sql) section for detailed instructions.</span></span> 

### <a name="troubleshooting"></a><span data-ttu-id="76d5d-244">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="76d5d-244">Troubleshooting</span></span>
<span data-ttu-id="76d5d-245">Étant donné que vous définissez **getDebugInfo** trop**toujours**, vous voyez un **journal** sous-dossier Bonjour **pyFiles** dossier dans votre conteneur d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="76d5d-245">Since you set **getDebugInfo** too**Always**, you see a **log** subfolder in hello **pyFiles** folder in your Azure Blob container.</span></span> <span data-ttu-id="76d5d-246">fichier de journal Hello dans le dossier du journal hello fournit des détails supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="76d5d-246">hello log file in hello log folder provides additional details.</span></span> <span data-ttu-id="76d5d-247">Ce fichier journal est particulièrement utile en cas d’erreur.</span><span class="sxs-lookup"><span data-stu-id="76d5d-247">This log file is especially useful when there is an error.</span></span> <span data-ttu-id="76d5d-248">Dans un environnement de production, vous souhaiterez peut-être tooset il trop**échec**.</span><span class="sxs-lookup"><span data-stu-id="76d5d-248">In a production environment, you may want tooset it too**Failure**.</span></span>

<span data-ttu-id="76d5d-249">Pour résoudre le problème, procédez comme hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="76d5d-249">For further troubleshooting, do hello following steps:</span></span>


1. <span data-ttu-id="76d5d-250">Accédez trop`https://<CLUSTERNAME>.azurehdinsight.net/yarnui/hn/cluster`.</span><span class="sxs-lookup"><span data-stu-id="76d5d-250">Navigate too`https://<CLUSTERNAME>.azurehdinsight.net/yarnui/hn/cluster`.</span></span>

    ![Application d’interface utilisateur YARN](media/data-factory-spark/yarnui-application.png)  
2. <span data-ttu-id="76d5d-252">Cliquez sur **journaux** pour l’une des hello exécuter tentatives.</span><span class="sxs-lookup"><span data-stu-id="76d5d-252">Click **Logs** for one of hello run attempts.</span></span>

    ![Page d’application](media/data-factory-spark/yarn-applications.png)
3. <span data-ttu-id="76d5d-254">Vous devez voir les informations d’erreur supplémentaires dans la page du journal hello.</span><span class="sxs-lookup"><span data-stu-id="76d5d-254">You should see additional error information in hello log page.</span></span>

    ![Erreur du journal](media/data-factory-spark/yarnui-application-error.png)

<span data-ttu-id="76d5d-256">Hello les sections suivantes fournit des informations sur le cluster d’Apache Spark Data Factory entités toouse et l’activité de Spark dans votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="76d5d-256">hello following sections provide information about Data Factory entities toouse Apache Spark cluster and Spark Activity in your data factory.</span></span>

## <a name="spark-activity-properties"></a><span data-ttu-id="76d5d-257">Propriétés de l'activité Spark</span><span class="sxs-lookup"><span data-stu-id="76d5d-257">Spark activity properties</span></span>
<span data-ttu-id="76d5d-258">Voici hello exemple JSON de définition d’un pipeline avec Spark activité :</span><span class="sxs-lookup"><span data-stu-id="76d5d-258">Here is hello sample JSON definition of a pipeline with Spark Activity:</span></span>    

```json
{
    "name": "SparkPipeline",
    "properties": {
        "activities": [
            {
                "type": "HDInsightSpark",
                "typeProperties": {
                    "rootPath": "adfspark\\pyFiles",
                    "entryFilePath": "test.py",
                    "arguments": [ "arg1", "arg2" ],
                    "sparkConfig": {
                        "spark.python.worker.memory": "512m"
                    }
                    "getDebugInfo": "Always"
                },
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ],
                "name": "MySparkActivity",
                "description": "This activity invokes hello Spark program",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-02-01T00:00:00Z",
        "end": "2017-02-02T00:00:00Z"
    }
}
```

<span data-ttu-id="76d5d-259">Hello tableau suivant décrit les propriétés JSON hello utilisées Bonjour définition JSON :</span><span class="sxs-lookup"><span data-stu-id="76d5d-259">hello following table describes hello JSON properties used in hello JSON definition:</span></span>

| <span data-ttu-id="76d5d-260">Propriété</span><span class="sxs-lookup"><span data-stu-id="76d5d-260">Property</span></span> | <span data-ttu-id="76d5d-261">Description</span><span class="sxs-lookup"><span data-stu-id="76d5d-261">Description</span></span> | <span data-ttu-id="76d5d-262">Requis</span><span class="sxs-lookup"><span data-stu-id="76d5d-262">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="76d5d-263">name</span><span class="sxs-lookup"><span data-stu-id="76d5d-263">name</span></span> | <span data-ttu-id="76d5d-264">Nom de l’activité hello dans le pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="76d5d-264">Name of hello activity in hello pipeline.</span></span> | <span data-ttu-id="76d5d-265">Oui</span><span class="sxs-lookup"><span data-stu-id="76d5d-265">Yes</span></span> |
| <span data-ttu-id="76d5d-266">description</span><span class="sxs-lookup"><span data-stu-id="76d5d-266">description</span></span> | <span data-ttu-id="76d5d-267">Texte décrivant de quelle activité hello effectue.</span><span class="sxs-lookup"><span data-stu-id="76d5d-267">Text describing what hello activity does.</span></span> | <span data-ttu-id="76d5d-268">Non</span><span class="sxs-lookup"><span data-stu-id="76d5d-268">No</span></span> |
| <span data-ttu-id="76d5d-269">type</span><span class="sxs-lookup"><span data-stu-id="76d5d-269">type</span></span> | <span data-ttu-id="76d5d-270">Cette propriété doit être définie tooHDInsightSpark.</span><span class="sxs-lookup"><span data-stu-id="76d5d-270">This property must be set tooHDInsightSpark.</span></span> | <span data-ttu-id="76d5d-271">Oui</span><span class="sxs-lookup"><span data-stu-id="76d5d-271">Yes</span></span> |
| <span data-ttu-id="76d5d-272">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="76d5d-272">linkedServiceName</span></span> | <span data-ttu-id="76d5d-273">Nom de hello HDInsight lié service sur le hello Spark programme s’exécute.</span><span class="sxs-lookup"><span data-stu-id="76d5d-273">Name of hello HDInsight linked service on which hello Spark program runs.</span></span> | <span data-ttu-id="76d5d-274">Oui</span><span class="sxs-lookup"><span data-stu-id="76d5d-274">Yes</span></span> |
| <span data-ttu-id="76d5d-275">rootPath</span><span class="sxs-lookup"><span data-stu-id="76d5d-275">rootPath</span></span> | <span data-ttu-id="76d5d-276">conteneur d’objets Blob Azure Hello et le dossier qui contient le fichier de Spark hello.</span><span class="sxs-lookup"><span data-stu-id="76d5d-276">hello Azure Blob container and folder that contains hello Spark file.</span></span> <span data-ttu-id="76d5d-277">nom de fichier Hello respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="76d5d-277">hello file name is case-sensitive.</span></span> | <span data-ttu-id="76d5d-278">Oui</span><span class="sxs-lookup"><span data-stu-id="76d5d-278">Yes</span></span> |
| <span data-ttu-id="76d5d-279">entryFilePath</span><span class="sxs-lookup"><span data-stu-id="76d5d-279">entryFilePath</span></span> | <span data-ttu-id="76d5d-280">Dossier racine du toohello chemin d’accès relatif de hello Spark/package de code.</span><span class="sxs-lookup"><span data-stu-id="76d5d-280">Relative path toohello root folder of hello Spark code/package.</span></span> | <span data-ttu-id="76d5d-281">Oui</span><span class="sxs-lookup"><span data-stu-id="76d5d-281">Yes</span></span> |
| <span data-ttu-id="76d5d-282">className</span><span class="sxs-lookup"><span data-stu-id="76d5d-282">className</span></span> | <span data-ttu-id="76d5d-283">Classe principale Java/Spark de l’application.</span><span class="sxs-lookup"><span data-stu-id="76d5d-283">Application's Java/Spark main class</span></span> | <span data-ttu-id="76d5d-284">Non</span><span class="sxs-lookup"><span data-stu-id="76d5d-284">No</span></span> |
| <span data-ttu-id="76d5d-285">arguments</span><span class="sxs-lookup"><span data-stu-id="76d5d-285">arguments</span></span> | <span data-ttu-id="76d5d-286">Une liste de programme de Spark toohello des arguments de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="76d5d-286">A list of command-line arguments toohello Spark program.</span></span> | <span data-ttu-id="76d5d-287">Non</span><span class="sxs-lookup"><span data-stu-id="76d5d-287">No</span></span> |
| <span data-ttu-id="76d5d-288">proxyUser</span><span class="sxs-lookup"><span data-stu-id="76d5d-288">proxyUser</span></span> | <span data-ttu-id="76d5d-289">programme Spark de Hello utilisateur compte tooimpersonate tooexecute hello</span><span class="sxs-lookup"><span data-stu-id="76d5d-289">hello user account tooimpersonate tooexecute hello Spark program</span></span> | <span data-ttu-id="76d5d-290">Non</span><span class="sxs-lookup"><span data-stu-id="76d5d-290">No</span></span> |
| <span data-ttu-id="76d5d-291">sparkConfig</span><span class="sxs-lookup"><span data-stu-id="76d5d-291">sparkConfig</span></span> | <span data-ttu-id="76d5d-292">Spécifier les valeurs des propriétés de configuration Spark répertoriées dans la rubrique de hello : [Configuration Spark - propriétés de l’Application](https://spark.apache.org/docs/latest/configuration.html#available-properties).</span><span class="sxs-lookup"><span data-stu-id="76d5d-292">Specify values for Spark configuration properties listed in hello topic: [Spark Configuration - Application properties](https://spark.apache.org/docs/latest/configuration.html#available-properties).</span></span> | <span data-ttu-id="76d5d-293">Non</span><span class="sxs-lookup"><span data-stu-id="76d5d-293">No</span></span> |
| <span data-ttu-id="76d5d-294">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="76d5d-294">getDebugInfo</span></span> | <span data-ttu-id="76d5d-295">Spécifie les fichiers journaux hello Spark toohello copié le stockage Azure utilisé par le cluster HDInsight (ou) spécifié par sparkJobLinkedService.</span><span class="sxs-lookup"><span data-stu-id="76d5d-295">Specifies when hello Spark log files are copied toohello Azure storage used by HDInsight cluster (or) specified by sparkJobLinkedService.</span></span> <span data-ttu-id="76d5d-296">Valeurs autorisées : Aucun, Toujours ou Échec.</span><span class="sxs-lookup"><span data-stu-id="76d5d-296">Allowed values: None, Always, or Failure.</span></span> <span data-ttu-id="76d5d-297">Valeur par défaut : Aucun.</span><span class="sxs-lookup"><span data-stu-id="76d5d-297">Default value: None.</span></span> | <span data-ttu-id="76d5d-298">Non</span><span class="sxs-lookup"><span data-stu-id="76d5d-298">No</span></span> |
| <span data-ttu-id="76d5d-299">sparkJobLinkedService</span><span class="sxs-lookup"><span data-stu-id="76d5d-299">sparkJobLinkedService</span></span> | <span data-ttu-id="76d5d-300">Hello service lié Azure Storage qui contient les journaux, les dépendances et les fichiers de travail hello Spark.</span><span class="sxs-lookup"><span data-stu-id="76d5d-300">hello Azure Storage linked service that holds hello Spark job file, dependencies, and logs.</span></span>  <span data-ttu-id="76d5d-301">Si vous ne spécifiez pas une valeur pour cette propriété, le stockage de hello associé au cluster HDInsight est utilisé.</span><span class="sxs-lookup"><span data-stu-id="76d5d-301">If you do not specify a value for this property, hello storage associated with HDInsight cluster is used.</span></span> | <span data-ttu-id="76d5d-302">Non</span><span class="sxs-lookup"><span data-stu-id="76d5d-302">No</span></span> |

## <a name="folder-structure"></a><span data-ttu-id="76d5d-303">Structure de dossiers</span><span class="sxs-lookup"><span data-stu-id="76d5d-303">Folder structure</span></span>
<span data-ttu-id="76d5d-304">Hello activité de Spark ne prend pas en charge un script en ligne en tant que Pig et effectuer des activités de la ruche.</span><span class="sxs-lookup"><span data-stu-id="76d5d-304">hello Spark activity does not support an in-line script as Pig and Hive activities do.</span></span> <span data-ttu-id="76d5d-305">Les travaux Spark sont également plus extensibles que les travaux Pig/Hive.</span><span class="sxs-lookup"><span data-stu-id="76d5d-305">Spark jobs are also more extensible than Pig/Hive jobs.</span></span> <span data-ttu-id="76d5d-306">Pour les travaux de Spark, vous pouvez fournir plusieurs dépendances, telles que les packages (placés dans java de hello CLASSPATH), python fichiers jar (placés sur hello PYTHONPATH) et tous les autres fichiers.</span><span class="sxs-lookup"><span data-stu-id="76d5d-306">For Spark jobs, you can provide multiple dependencies such as jar packages (placed in hello java CLASSPATH), python files (placed on hello PYTHONPATH), and any other files.</span></span>

<span data-ttu-id="76d5d-307">Créer hello suivant la structure de dossiers Bonjour référencé par hello service lié HDInsight le stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="76d5d-307">Create hello following folder structure in hello Azure Blob storage referenced by hello HDInsight linked service.</span></span> <span data-ttu-id="76d5d-308">Ensuite, téléchargez les fichiers dépendants toohello approprié sous-dossiers dans le dossier racine de hello représenté par **entryFilePath**.</span><span class="sxs-lookup"><span data-stu-id="76d5d-308">Then, upload dependent files toohello appropriate sub folders in hello root folder represented by **entryFilePath**.</span></span> <span data-ttu-id="76d5d-309">Par exemple, téléchargez le sous-dossier de python fichiers toohello pyFiles et jar fichiers toohello fichiers JAR sous-dossier du dossier racine de hello.</span><span class="sxs-lookup"><span data-stu-id="76d5d-309">For example, upload python files toohello pyFiles subfolder and jar files toohello jars subfolder of hello root folder.</span></span> <span data-ttu-id="76d5d-310">Lors de l’exécution, service Data Factory attend hello suivant la structure de dossiers Bonjour le stockage Blob Azure :</span><span class="sxs-lookup"><span data-stu-id="76d5d-310">At runtime, Data Factory service expects hello following folder structure in hello Azure Blob storage:</span></span>     

| <span data-ttu-id="76d5d-311">Chemin</span><span class="sxs-lookup"><span data-stu-id="76d5d-311">Path</span></span> | <span data-ttu-id="76d5d-312">Description</span><span class="sxs-lookup"><span data-stu-id="76d5d-312">Description</span></span> | <span data-ttu-id="76d5d-313">Requis</span><span class="sxs-lookup"><span data-stu-id="76d5d-313">Required</span></span> | <span data-ttu-id="76d5d-314">Type</span><span class="sxs-lookup"><span data-stu-id="76d5d-314">Type</span></span> |
| ---- | ----------- | -------- | ---- |
| <span data-ttu-id="76d5d-315">.</span><span class="sxs-lookup"><span data-stu-id="76d5d-315">.</span></span> | <span data-ttu-id="76d5d-316">chemin d’accès racine de Hello du travail de Spark hello dans le service de stockage lié hello</span><span class="sxs-lookup"><span data-stu-id="76d5d-316">hello root path of hello Spark job in hello storage linked service</span></span>    | <span data-ttu-id="76d5d-317">Oui</span><span class="sxs-lookup"><span data-stu-id="76d5d-317">Yes</span></span> | <span data-ttu-id="76d5d-318">Dossier</span><span class="sxs-lookup"><span data-stu-id="76d5d-318">Folder</span></span> |
| <span data-ttu-id="76d5d-319">&lt;défini par l’utilisateur &gt;</span><span class="sxs-lookup"><span data-stu-id="76d5d-319">&lt;user defined &gt;</span></span> | <span data-ttu-id="76d5d-320">chemin d’accès Hello pointant vers le fichier d’entrée toohello du travail de Spark hello</span><span class="sxs-lookup"><span data-stu-id="76d5d-320">hello path pointing toohello entry file of hello Spark job</span></span> | <span data-ttu-id="76d5d-321">Oui</span><span class="sxs-lookup"><span data-stu-id="76d5d-321">Yes</span></span> | <span data-ttu-id="76d5d-322">Fichier</span><span class="sxs-lookup"><span data-stu-id="76d5d-322">File</span></span> |
| <span data-ttu-id="76d5d-323">./jars</span><span class="sxs-lookup"><span data-stu-id="76d5d-323">./jars</span></span> | <span data-ttu-id="76d5d-324">Tous les fichiers sous ce dossier sont téléchargés et placés sur le chemin de classe java hello du cluster de hello</span><span class="sxs-lookup"><span data-stu-id="76d5d-324">All files under this folder are uploaded and placed on hello java classpath of hello cluster</span></span> | <span data-ttu-id="76d5d-325">Non</span><span class="sxs-lookup"><span data-stu-id="76d5d-325">No</span></span> | <span data-ttu-id="76d5d-326">Dossier</span><span class="sxs-lookup"><span data-stu-id="76d5d-326">Folder</span></span> |
| <span data-ttu-id="76d5d-327">./pyFiles</span><span class="sxs-lookup"><span data-stu-id="76d5d-327">./pyFiles</span></span> | <span data-ttu-id="76d5d-328">Tous les fichiers sous ce dossier sont téléchargés et placés sur hello PYTHONPATH du cluster de hello</span><span class="sxs-lookup"><span data-stu-id="76d5d-328">All files under this folder are uploaded and placed on hello PYTHONPATH of hello cluster</span></span> | <span data-ttu-id="76d5d-329">Non</span><span class="sxs-lookup"><span data-stu-id="76d5d-329">No</span></span> | <span data-ttu-id="76d5d-330">Dossier</span><span class="sxs-lookup"><span data-stu-id="76d5d-330">Folder</span></span> |
| <span data-ttu-id="76d5d-331">./files</span><span class="sxs-lookup"><span data-stu-id="76d5d-331">./files</span></span> | <span data-ttu-id="76d5d-332">Tous les fichiers dans ce dossier sont téléchargés et placés dans le répertoire de travail de l’exécuteur</span><span class="sxs-lookup"><span data-stu-id="76d5d-332">All files under this folder are uploaded and placed on executor working directory</span></span> | <span data-ttu-id="76d5d-333">Non</span><span class="sxs-lookup"><span data-stu-id="76d5d-333">No</span></span> | <span data-ttu-id="76d5d-334">Dossier</span><span class="sxs-lookup"><span data-stu-id="76d5d-334">Folder</span></span> |
| <span data-ttu-id="76d5d-335">./archives</span><span class="sxs-lookup"><span data-stu-id="76d5d-335">./archives</span></span> | <span data-ttu-id="76d5d-336">Tous les fichiers dans ce dossier ne sont pas compressés</span><span class="sxs-lookup"><span data-stu-id="76d5d-336">All files under this folder are uncompressed</span></span> | <span data-ttu-id="76d5d-337">Non</span><span class="sxs-lookup"><span data-stu-id="76d5d-337">No</span></span> | <span data-ttu-id="76d5d-338">Dossier</span><span class="sxs-lookup"><span data-stu-id="76d5d-338">Folder</span></span> |
| <span data-ttu-id="76d5d-339">./logs</span><span class="sxs-lookup"><span data-stu-id="76d5d-339">./logs</span></span> | <span data-ttu-id="76d5d-340">dossier Hello sur lequel sont enregistrés les journaux de cluster de Spark hello.</span><span class="sxs-lookup"><span data-stu-id="76d5d-340">hello folder where logs from hello Spark cluster are stored.</span></span>| <span data-ttu-id="76d5d-341">Non</span><span class="sxs-lookup"><span data-stu-id="76d5d-341">No</span></span> | <span data-ttu-id="76d5d-342">Dossier</span><span class="sxs-lookup"><span data-stu-id="76d5d-342">Folder</span></span> |

<span data-ttu-id="76d5d-343">Voici un exemple pour un stockage qui contient deux fichiers de travail Spark Bonjour Azure Blob Storage référencé par hello service lié HDInsight.</span><span class="sxs-lookup"><span data-stu-id="76d5d-343">Here is an example for a storage containing two Spark job files in hello Azure Blob Storage referenced by hello HDInsight linked service.</span></span>

```
SparkJob1
    main.jar
    files
        input1.txt
        input2.txt
    jars
        package1.jar
        package2.jar
    logs

SparkJob2
    main.py
    pyFiles
        scrip1.py
        script2.py
    logs
```
