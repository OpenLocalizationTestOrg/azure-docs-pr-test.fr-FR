---
title: "aaaBuild votre première fabrique de données (PowerShell) | Documents Microsoft"
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
ms.openlocfilehash: 626260798b56d590577b3c4b24f7cf52873c9f80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-powershell"></a><span data-ttu-id="3af99-103">Didacticiel : Créer votre première fabrique de données Azure à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3af99-103">Tutorial: Build your first Azure data factory using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3af99-104">Vue d’ensemble et étapes préalables requises</span><span class="sxs-lookup"><span data-stu-id="3af99-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="3af99-105">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="3af99-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="3af99-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3af99-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="3af99-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3af99-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="3af99-108">Modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3af99-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="3af99-109">API REST</span><span class="sxs-lookup"><span data-stu-id="3af99-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)
>
>

<span data-ttu-id="3af99-110">Dans cet article, vous utilisez Azure PowerShell toocreate votre première Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="3af99-110">In this article, you use Azure PowerShell toocreate your first Azure data factory.</span></span> <span data-ttu-id="3af99-111">didacticiel de hello toodo à l’aide d’autres outils/kits de développement logiciel, sélectionnez une des options de hello à partir de la liste déroulante de hello.</span><span class="sxs-lookup"><span data-stu-id="3af99-111">toodo hello tutorial using other tools/SDKs, select one of hello options from hello drop-down list.</span></span>

<span data-ttu-id="3af99-112">pipeline Hello dans ce didacticiel a une activité : **activité HDInsight Hive**.</span><span class="sxs-lookup"><span data-stu-id="3af99-112">hello pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="3af99-113">Cette activité s’exécute un script hive sur un cluster Azure HDInsight et les transformations d’entrée de données de sortie tooproduce.</span><span class="sxs-lookup"><span data-stu-id="3af99-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data tooproduce output data.</span></span> <span data-ttu-id="3af99-114">pipeline de Hello est planifiée toorun une fois qu’un mois entre hello spécifié d’heures de début et de fin.</span><span class="sxs-lookup"><span data-stu-id="3af99-114">hello pipeline is scheduled toorun once a month between hello specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="3af99-115">le pipeline de données Hello dans ce didacticiel transforme les données de sortie de données d’entrée tooproduce.</span><span class="sxs-lookup"><span data-stu-id="3af99-115">hello data pipeline in this tutorial transforms input data tooproduce output data.</span></span> <span data-ttu-id="3af99-116">Elle ne copie pas les données à partir d’un magasin de données de destination source données magasin tooa.</span><span class="sxs-lookup"><span data-stu-id="3af99-116">It does not copy data from a source data store tooa destination data store.</span></span> <span data-ttu-id="3af99-117">Pour obtenir un didacticiel sur la façon de toocopy les données à l’aide d’Azure Data Factory, consultez [didacticiel : copier des données à partir du stockage d’objets Blob tooSQL de base de données](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="3af99-117">For a tutorial on how toocopy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="3af99-118">Un pipeline peut contenir plusieurs activités.</span><span class="sxs-lookup"><span data-stu-id="3af99-118">A pipeline can have more than one activity.</span></span> <span data-ttu-id="3af99-119">De plus, vous pouvez concaténer les deux activités (exécutée une activité après l’autre) en définissant le dataset de sortie hello d’une activité hello d’entrée dataset Hello autre activité.</span><span class="sxs-lookup"><span data-stu-id="3af99-119">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="3af99-120">Pour plus d’informations, consultez [Planification et exécution dans Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="3af99-120">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3af99-121">Composants requis</span><span class="sxs-lookup"><span data-stu-id="3af99-121">Prerequisites</span></span>
* <span data-ttu-id="3af99-122">Lisez [vue d’ensemble du didacticiel](data-factory-build-your-first-pipeline.md) article et hello complète **condition préalable** étapes.</span><span class="sxs-lookup"><span data-stu-id="3af99-122">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="3af99-123">Suivez les instructions de [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) article tooinstall version la plus récente d’Azure PowerShell sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="3af99-123">Follow instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article tooinstall latest version of Azure PowerShell on your computer.</span></span>
* <span data-ttu-id="3af99-124">(facultatif) Cet article ne couvre pas toutes les applets de commande hello Data Factory.</span><span class="sxs-lookup"><span data-stu-id="3af99-124">(optional) This article does not cover all hello Data Factory cmdlets.</span></span> <span data-ttu-id="3af99-125">Consultez la [Référence des applets de commande Data Factory](/powershell/module/azurerm.datafactories) pour obtenir une documentation complète sur les applets de commande Data Factory.</span><span class="sxs-lookup"><span data-stu-id="3af99-125">See [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories) for comprehensive documentation on Data Factory cmdlets.</span></span>

## <a name="create-data-factory"></a><span data-ttu-id="3af99-126">Créer une fabrique de données</span><span class="sxs-lookup"><span data-stu-id="3af99-126">Create data factory</span></span>
<span data-ttu-id="3af99-127">Dans cette étape, vous utilisez Azure PowerShell toocreate une fabrique de données Azure nommé **FirstDataFactoryPSH**.</span><span class="sxs-lookup"><span data-stu-id="3af99-127">In this step, you use Azure PowerShell toocreate an Azure Data Factory named **FirstDataFactoryPSH**.</span></span> <span data-ttu-id="3af99-128">Une fabrique de données peut avoir un ou plusieurs pipelines.</span><span class="sxs-lookup"><span data-stu-id="3af99-128">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="3af99-129">Un pipeline peut contenir une ou plusieurs activités.</span><span class="sxs-lookup"><span data-stu-id="3af99-129">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="3af99-130">Par exemple, un activité de copie toocopy des données d’un magasin de données de destination tooa source et un toorun d’activité HDInsight Hive un tootransform de script Hive les données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="3af99-130">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform input data.</span></span> <span data-ttu-id="3af99-131">Commençons par créer la fabrique de données hello dans cette étape.</span><span class="sxs-lookup"><span data-stu-id="3af99-131">Let's start with creating hello data factory in this step.</span></span>

1. <span data-ttu-id="3af99-132">Démarrez Azure PowerShell et exécutez hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="3af99-132">Start Azure PowerShell and run hello following command.</span></span> <span data-ttu-id="3af99-133">Laissez Azure PowerShell ouverte jusqu'à la fin de hello de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="3af99-133">Keep Azure PowerShell open until hello end of this tutorial.</span></span> <span data-ttu-id="3af99-134">Si vous fermez et rouvrez, vous devez toorun ces commandes à nouveau.</span><span class="sxs-lookup"><span data-stu-id="3af99-134">If you close and reopen, you need toorun these commands again.</span></span>
   * <span data-ttu-id="3af99-135">Exécutez hello suivant de commande et entrez le nom d’utilisateur hello et le mot de passe que vous utilisez toosign dans toohello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3af99-135">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>
    ```PowerShell
    Login-AzureRmAccount
    ```    
   * <span data-ttu-id="3af99-136">Exécutez hello suivant commande tooview tous les abonnements hello pour ce compte.</span><span class="sxs-lookup"><span data-stu-id="3af99-136">Run hello following command tooview all hello subscriptions for this account.</span></span>
    ```PowerShell
    Get-AzureRmSubscription 
    ```
   * <span data-ttu-id="3af99-137">Tooselect hello abonnement toowork avec la commande suivante d’exécution hello.</span><span class="sxs-lookup"><span data-stu-id="3af99-137">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="3af99-138">Cet abonnement doit être hello identique à celui Bonjour portail Azure hello.</span><span class="sxs-lookup"><span data-stu-id="3af99-138">This subscription should be hello same as hello one you used in hello Azure portal.</span></span>
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```     
2. <span data-ttu-id="3af99-139">Créer un groupe de ressources Azure nommé **ADFTutorialResourceGroup** en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="3af99-139">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command:</span></span>
    
    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
    <span data-ttu-id="3af99-140">Certaines des étapes hello dans ce didacticiel supposent que vous utilisez le groupe de ressources hello nommé ADFTutorialResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="3af99-140">Some of hello steps in this tutorial assume that you use hello resource group named ADFTutorialResourceGroup.</span></span> <span data-ttu-id="3af99-141">Si vous utilisez un autre groupe de ressources, vous devez toouse il à la place de ADFTutorialResourceGroup dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="3af99-141">If you use a different resource group, you need toouse it in place of ADFTutorialResourceGroup in this tutorial.</span></span>
3. <span data-ttu-id="3af99-142">Exécutez hello **New-AzureRmDataFactory** applet de commande qui crée une fabrique de données nommée **FirstDataFactoryPSH**.</span><span class="sxs-lookup"><span data-stu-id="3af99-142">Run hello **New-AzureRmDataFactory** cmdlet that creates a data factory named **FirstDataFactoryPSH**.</span></span>

    ```PowerShell
    New-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH –Location "West US"
    ```
<span data-ttu-id="3af99-143">Hello Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="3af99-143">Note hello following points:</span></span>

* <span data-ttu-id="3af99-144">nom de Hello Hello Azure Data Factory doit être globalement unique.</span><span class="sxs-lookup"><span data-stu-id="3af99-144">hello name of hello Azure Data Factory must be globally unique.</span></span> <span data-ttu-id="3af99-145">Si vous recevez une erreur de hello **nom de fabrique de données « FirstDataFactoryPSH » n’est pas disponible**, modifiez le nom hello (par exemple, yournameFirstDataFactoryPSH).</span><span class="sxs-lookup"><span data-stu-id="3af99-145">If you receive hello error **Data factory name “FirstDataFactoryPSH” is not available**, change hello name (for example, yournameFirstDataFactoryPSH).</span></span> <span data-ttu-id="3af99-146">Utilisez ce nom à la place d’ADFTutorialFactoryPSH quand vous effectuez les étapes de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="3af99-146">Use this name in place of ADFTutorialFactoryPSH while performing steps in this tutorial.</span></span> <span data-ttu-id="3af99-147">Consultez la rubrique [Data Factory - Règles d'affectation des noms](data-factory-naming-rules.md) pour savoir comment nommer les artefacts Data Factory.</span><span class="sxs-lookup"><span data-stu-id="3af99-147">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
* <span data-ttu-id="3af99-148">instances de fabrique de données toocreate, vous devez toobe un collaborateur/administrateur Hello abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="3af99-148">toocreate Data Factory instances, you need toobe a contributor/administrator of hello Azure subscription</span></span>
* <span data-ttu-id="3af99-149">nom Hello hello fabrique de données peut être enregistré comme un nom DNS dans hello futures et donc devenir visible publiquement.</span><span class="sxs-lookup"><span data-stu-id="3af99-149">hello name of hello data factory may be registered as a DNS name in hello future and hence become publically visible.</span></span>
* <span data-ttu-id="3af99-150">Si vous recevez une erreur de hello : «**cet abonnement n’est pas un espace de noms inscrit toouse Microsoft.DataFactory**», effectuez l’une des manières suivantes les hello et essayez de publier à nouveau :</span><span class="sxs-lookup"><span data-stu-id="3af99-150">If you receive hello error: "**This subscription is not registered toouse namespace Microsoft.DataFactory**", do one of hello following and try publishing again:</span></span>

  * <span data-ttu-id="3af99-151">Dans Azure PowerShell, exécutez hello suivant le fournisseur de commandes tooregister hello fabrique de données :</span><span class="sxs-lookup"><span data-stu-id="3af99-151">In Azure PowerShell, run hello following command tooregister hello Data Factory provider:</span></span>

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
      <span data-ttu-id="3af99-152">Vous pouvez exécuter hello suivant commande tooconfirm ce fournisseur est inscrit de fabrique de données hello :</span><span class="sxs-lookup"><span data-stu-id="3af99-152">You can run hello following command tooconfirm that hello Data Factory provider is registered:</span></span>

    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="3af99-153">Connexion à l’aide de hello abonnement Azure dans hello [portail Azure](https://portal.azure.com) et accédez Panneau de Data Factory tooa (ou) créer une fabrique de données Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3af99-153">Login using hello Azure subscription into hello [Azure portal](https://portal.azure.com) and navigate tooa Data Factory blade (or) create a data factory in hello Azure portal.</span></span> <span data-ttu-id="3af99-154">Cette action enregistre automatiquement le fournisseur hello pour vous.</span><span class="sxs-lookup"><span data-stu-id="3af99-154">This action automatically registers hello provider for you.</span></span>

<span data-ttu-id="3af99-155">Avant de créer un pipeline, vous devez toocreate quelques entités de fabrique de données tout d’abord.</span><span class="sxs-lookup"><span data-stu-id="3af99-155">Before creating a pipeline, you need toocreate a few Data Factory entities first.</span></span> <span data-ttu-id="3af99-156">Vous créez tout d’abord les services liés toolink données magasins/calcule tooyour données stockent, définissent l’entrée et sortie des données de d’entrée/sortie toorepresent de jeux de données dans des magasins de données liées et ensuite créer un pipeline de hello avec une activité qui utilise ces jeux de données.</span><span class="sxs-lookup"><span data-stu-id="3af99-156">You first create linked services toolink data stores/computes tooyour data store, define input and output datasets toorepresent input/output data in linked data stores, and then create hello pipeline with an activity that uses these datasets.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="3af99-157">Créez des services liés</span><span class="sxs-lookup"><span data-stu-id="3af99-157">Create linked services</span></span>
<span data-ttu-id="3af99-158">Dans cette étape, vous liez votre compte de stockage Azure et une fabrique de données à la demande Azure HDInsight cluster tooyour.</span><span class="sxs-lookup"><span data-stu-id="3af99-158">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="3af99-159">blocages de compte de stockage Azure Hello hello des données d’entrée et de sortie pour le pipeline hello dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="3af99-159">hello Azure Storage account holds hello input and output data for hello pipeline in this sample.</span></span> <span data-ttu-id="3af99-160">Hello service lié HDInsight est toorun utilisé un script Hive spécifié dans l’activité hello du pipeline hello dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="3af99-160">hello HDInsight linked service is used toorun a Hive script specified in hello activity of hello pipeline in this sample.</span></span> <span data-ttu-id="3af99-161">Identifier les données de magasin/calcul services sont utilisés dans votre scénario et lier ces fabrique de données de services toohello en créant des services liés.</span><span class="sxs-lookup"><span data-stu-id="3af99-161">Identify what data store/compute services are used in your scenario and link those services toohello data factory by creating linked services.</span></span>

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="3af99-162">Créer le service lié Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="3af99-162">Create Azure Storage linked service</span></span>
<span data-ttu-id="3af99-163">Dans cette étape, vous liez votre fabrique de données tooyour compte Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="3af99-163">In this step, you link your Azure Storage account tooyour data factory.</span></span> <span data-ttu-id="3af99-164">Vous utilisez hello même compte de stockage Azure hello HQL et les données d’entrée/sortie toostore de fichier de script.</span><span class="sxs-lookup"><span data-stu-id="3af99-164">You use hello same Azure Storage account toostore input/output data and hello HQL script file.</span></span>

1. <span data-ttu-id="3af99-165">Créer un fichier JSON comportant StorageLinkedService.json dans le dossier de C:\ADFGetStarted hello hello suivant contenu.</span><span class="sxs-lookup"><span data-stu-id="3af99-165">Create a JSON file named StorageLinkedService.json in hello C:\ADFGetStarted folder with hello following content.</span></span> <span data-ttu-id="3af99-166">Créez le dossier hello ADFGetStarted si elle n’existe pas déjà.</span><span class="sxs-lookup"><span data-stu-id="3af99-166">Create hello folder ADFGetStarted if it does not already exist.</span></span>

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
    <span data-ttu-id="3af99-167">Remplacez **nom de compte** avec le nom de hello de votre compte de stockage Azure et **clé de compte** avec la clé d’accès hello Hello compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="3af99-167">Replace **account name** with hello name of your Azure storage account and **account key** with hello access key of hello Azure storage account.</span></span> <span data-ttu-id="3af99-168">toolearn comment accéder à votre espace de stockage tooget de clé, consultez hello plus d’informations sur comment tooview, copier et régénérer stockage touches d’accès [gérer votre compte de stockage](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="3af99-168">toolearn how tooget your storage access key, see hello information about how tooview, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
2. <span data-ttu-id="3af99-169">Dans Azure PowerShell, basculez toohello ADFGetStarted dossier.</span><span class="sxs-lookup"><span data-stu-id="3af99-169">In Azure PowerShell, switch toohello ADFGetStarted folder.</span></span>
3. <span data-ttu-id="3af99-170">Vous pouvez utiliser hello **New-AzureRmDataFactoryLinkedService** applet de commande qui crée un service lié.</span><span class="sxs-lookup"><span data-stu-id="3af99-170">You can use hello **New-AzureRmDataFactoryLinkedService** cmdlet that creates a linked service.</span></span> <span data-ttu-id="3af99-171">Cette applet de commande et d’autres applets de commande fabrique de données que vous utilisez dans ce didacticiel requiert vous toopass des valeurs pour hello *ResourceGroupName* et *DataFactoryName* paramètres.</span><span class="sxs-lookup"><span data-stu-id="3af99-171">This cmdlet and other Data Factory cmdlets you use in this tutorial requires you toopass values for hello *ResourceGroupName* and *DataFactoryName* parameters.</span></span> <span data-ttu-id="3af99-172">Vous pouvez également utiliser **Get-AzureRmDataFactory** tooget un **DataFactory** de l’objet et de passer un objet de hello sans avoir à taper *ResourceGroupName* et  *DataFactoryName* chaque fois que vous exécutez une applet de commande.</span><span class="sxs-lookup"><span data-stu-id="3af99-172">Alternatively, you can use **Get-AzureRmDataFactory** tooget a **DataFactory** object and pass hello object without typing *ResourceGroupName* and *DataFactoryName* each time you run a cmdlet.</span></span> <span data-ttu-id="3af99-173">Sortie de hello tooassign Hello de commandes suivante d’exécution hello **Get-AzureRmDataFactory** tooa de l’applet de commande **$df** variable.</span><span class="sxs-lookup"><span data-stu-id="3af99-173">Run hello following command tooassign hello output of hello **Get-AzureRmDataFactory** cmdlet tooa **$df** variable.</span></span>

    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH
    ```
4. <span data-ttu-id="3af99-174">Exécutez maintenant hello **New-AzureRmDataFactoryLinkedService** liés de l’applet de commande qui crée hello **StorageLinkedService** service.</span><span class="sxs-lookup"><span data-stu-id="3af99-174">Now, run hello **New-AzureRmDataFactoryLinkedService** cmdlet that creates hello linked **StorageLinkedService** service.</span></span>

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\StorageLinkedService.json
    ```
    <span data-ttu-id="3af99-175">Si vous n’aviez pas exécuter hello **Get-AzureRmDataFactory** applet de commande et attribué hello sortie toohello **$df** variable, vous devez les valeurs toospecify pour hello *ResourceGroupName*et *DataFactoryName* paramètres comme suit.</span><span class="sxs-lookup"><span data-stu-id="3af99-175">If you hadn't run hello **Get-AzureRmDataFactory** cmdlet and assigned hello output toohello **$df** variable, you would have toospecify values for hello *ResourceGroupName* and *DataFactoryName* parameters as follows.</span></span>

    ```PowerShell
    New-AzureRmDataFactoryLinkedService -ResourceGroupName ADFTutorialResourceGroup -DataFactoryName FirstDataFactoryPSH -File .\StorageLinkedService.json
    ```
    <span data-ttu-id="3af99-176">Si vous fermez Azure PowerShell milieu hello du didacticiel de hello, vous avez toorun hello **Get-AzureRmDataFactory** prochain démarrage du didacticiel de hello toocomplete Azure PowerShell de l’applet de commande.</span><span class="sxs-lookup"><span data-stu-id="3af99-176">If you close Azure PowerShell in hello middle of hello tutorial, you have toorun hello **Get-AzureRmDataFactory** cmdlet next time you start Azure PowerShell toocomplete hello tutorial.</span></span>

### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="3af99-177">Créer le service lié Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="3af99-177">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="3af99-178">Dans cette étape, vous liez une fabrique de données à la demande HDInsight cluster tooyour.</span><span class="sxs-lookup"><span data-stu-id="3af99-178">In this step, you link an on-demand HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="3af99-179">Hello cluster HDInsight est automatiquement créé lors de l’exécution et supprimée une fois ceci effectué inactifs et le traitement de la durée spécifiée hello.</span><span class="sxs-lookup"><span data-stu-id="3af99-179">hello HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for hello specified amount of time.</span></span> <span data-ttu-id="3af99-180">Vous pouvez utiliser votre propre cluster HDInsight au lieu d’utiliser un cluster HDInsight à la demande.</span><span class="sxs-lookup"><span data-stu-id="3af99-180">You could use your own HDInsight cluster instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="3af99-181">Pour plus d’informations, consultez [Services de calcul liés](data-factory-compute-linked-services.md) .</span><span class="sxs-lookup"><span data-stu-id="3af99-181">See [Compute Linked Services](data-factory-compute-linked-services.md) for details.</span></span>

1. <span data-ttu-id="3af99-182">Créez un fichier JSON nommé **HDInsightOnDemandLinkedService**.json Bonjour **C:\ADFGetStarted** dossier avec hello suivant le contenu.</span><span class="sxs-lookup"><span data-stu-id="3af99-182">Create a JSON file named **HDInsightOnDemandLinkedService**.json in hello **C:\ADFGetStarted** folder with hello following content.</span></span>

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
    <span data-ttu-id="3af99-183">Hello tableau suivant fournit des descriptions pour les propriétés JSON hello utilisées dans l’extrait de code hello :</span><span class="sxs-lookup"><span data-stu-id="3af99-183">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

   | <span data-ttu-id="3af99-184">Propriété</span><span class="sxs-lookup"><span data-stu-id="3af99-184">Property</span></span> | <span data-ttu-id="3af99-185">Description</span><span class="sxs-lookup"><span data-stu-id="3af99-185">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="3af99-186">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="3af99-186">ClusterSize</span></span> |<span data-ttu-id="3af99-187">Spécifie la taille de hello du cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="3af99-187">Specifies hello size of hello HDInsight cluster.</span></span> |
   | <span data-ttu-id="3af99-188">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="3af99-188">TimeToLive</span></span> |<span data-ttu-id="3af99-189">Spécifie la durée d’inactivité de ce hello pour le cluster HDInsight de hello, avant d’être supprimé.</span><span class="sxs-lookup"><span data-stu-id="3af99-189">Specifies that hello idle time for hello HDInsight cluster, before it is deleted.</span></span> |
   | <span data-ttu-id="3af99-190">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="3af99-190">linkedServiceName</span></span> |<span data-ttu-id="3af99-191">Spécifie le compte de stockage hello toostore utilisé hello journaux générés par HDInsight</span><span class="sxs-lookup"><span data-stu-id="3af99-191">Specifies hello storage account that is used toostore hello logs that are generated by HDInsight</span></span> |

    <span data-ttu-id="3af99-192">Hello Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="3af99-192">Note hello following points:</span></span>

   * <span data-ttu-id="3af99-193">Hello Data Factory crée un **basés sur Linux** cluster HDInsight pour vous par hello JSON.</span><span class="sxs-lookup"><span data-stu-id="3af99-193">hello Data Factory creates a **Linux-based** HDInsight cluster for you with hello JSON.</span></span> <span data-ttu-id="3af99-194">Pour plus d’informations, voir [Service lié à la demande Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="3af99-194">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
   * <span data-ttu-id="3af99-195">Vous pouvez utiliser votre **propre cluster HDInsight** au lieu d’utiliser un cluster HDInsight à la demande.</span><span class="sxs-lookup"><span data-stu-id="3af99-195">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="3af99-196">Pour plus d’informations, voir [Service lié Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="3af99-196">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
   * <span data-ttu-id="3af99-197">Hello HDInsight cluster crée un **conteneur par défaut** dans le stockage blob hello spécifié dans hello JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="3af99-197">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="3af99-198">HDInsight ne supprime pas ce conteneur lorsque le cluster de hello est supprimé.</span><span class="sxs-lookup"><span data-stu-id="3af99-198">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="3af99-199">Ce comportement est normal.</span><span class="sxs-lookup"><span data-stu-id="3af99-199">This behavior is by design.</span></span> <span data-ttu-id="3af99-200">Avec le service lié HDInsight disponible à la demande, un cluster HDInsight est créé dès qu’une tranche est traitée, à moins qu’il n’existe un cluster actif (**timeToLive**).</span><span class="sxs-lookup"><span data-stu-id="3af99-200">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**).</span></span> <span data-ttu-id="3af99-201">Hello cluster est automatiquement supprimé lorsque le traitement de hello est effectué.</span><span class="sxs-lookup"><span data-stu-id="3af99-201">hello cluster is automatically deleted when hello processing is done.</span></span>

       <span data-ttu-id="3af99-202">Comme un nombre croissant de tranches sont traitées, vous voyez un grand nombre de conteneurs dans votre stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="3af99-202">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="3af99-203">Si vous ne devez pas les pour la résolution des problèmes de travaux de hello, vous souhaiterez peut-être toodelete les coûts de stockage tooreduce hello.</span><span class="sxs-lookup"><span data-stu-id="3af99-203">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="3af99-204">les noms de ces conteneurs Hello suivent un modèle : « adf**yourdatafactoryname**-**linkedservicename**- datetimestamp ».</span><span class="sxs-lookup"><span data-stu-id="3af99-204">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="3af99-205">Utiliser des outils tels que [Explorateur de stockage Microsoft](http://storageexplorer.com/) stockage d’objets blob des conteneurs de toodelete dans votre Azure.</span><span class="sxs-lookup"><span data-stu-id="3af99-205">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

     <span data-ttu-id="3af99-206">Pour plus d’informations, voir [Service lié à la demande Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="3af99-206">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
2. <span data-ttu-id="3af99-207">Exécutez hello **New-AzureRmDataFactoryLinkedService** applet de commande qui crée hello lié service appelé HDInsightOnDemandLinkedService.</span><span class="sxs-lookup"><span data-stu-id="3af99-207">Run hello **New-AzureRmDataFactoryLinkedService** cmdlet that creates hello linked service called HDInsightOnDemandLinkedService.</span></span>
    
    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\HDInsightOnDemandLinkedService.json
    ```

## <a name="create-datasets"></a><span data-ttu-id="3af99-208">Créez les jeux de données</span><span class="sxs-lookup"><span data-stu-id="3af99-208">Create datasets</span></span>
<span data-ttu-id="3af99-209">Dans cette étape, vous créez des groupes de données toorepresent hello d’entrée et sortie des données pour le traitement de la ruche.</span><span class="sxs-lookup"><span data-stu-id="3af99-209">In this step, you create datasets toorepresent hello input and output data for Hive processing.</span></span> <span data-ttu-id="3af99-210">Ces jeux de données font référence toohello **StorageLinkedService** que vous avez créé précédemment dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="3af99-210">These datasets refer toohello **StorageLinkedService** you have created earlier in this tutorial.</span></span> <span data-ttu-id="3af99-211">Hello tooan de points de service lié compte de stockage Azure et de jeux de données spécifiez conteneur, dossier, le nom de fichier dans le stockage hello qui contient l’entrée et les données de sortie.</span><span class="sxs-lookup"><span data-stu-id="3af99-211">hello linked service points tooan Azure Storage account and datasets specify container, folder, file name in hello storage that holds input and output data.</span></span>

### <a name="create-input-dataset"></a><span data-ttu-id="3af99-212">Créer le jeu de données d’entrée</span><span class="sxs-lookup"><span data-stu-id="3af99-212">Create input dataset</span></span>
1. <span data-ttu-id="3af99-213">Créez un fichier JSON nommé **InputTable.json** Bonjour **C:\ADFGetStarted** dossier avec hello suivant le contenu :</span><span class="sxs-lookup"><span data-stu-id="3af99-213">Create a JSON file named **InputTable.json** in hello **C:\ADFGetStarted** folder with hello following content:</span></span>

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
    <span data-ttu-id="3af99-214">Hello JSON définit un dataset nommé **AzureBlobInput**, qui représente les données d’entrée pour une activité dans le pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="3af99-214">hello JSON defines a dataset named **AzureBlobInput**, which represents input data for an activity in hello pipeline.</span></span> <span data-ttu-id="3af99-215">En outre, il spécifie que les données d’entrée hello se trouve dans le conteneur d’objets blob hello appelé **adfgetstarted** et dossier hello appelé **inputdata**.</span><span class="sxs-lookup"><span data-stu-id="3af99-215">In addition, it specifies that hello input data is located in hello blob container called **adfgetstarted** and hello folder called **inputdata**.</span></span>

    <span data-ttu-id="3af99-216">Hello tableau suivant fournit des descriptions pour les propriétés JSON hello utilisées dans l’extrait de code hello :</span><span class="sxs-lookup"><span data-stu-id="3af99-216">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

   | <span data-ttu-id="3af99-217">Propriété</span><span class="sxs-lookup"><span data-stu-id="3af99-217">Property</span></span> | <span data-ttu-id="3af99-218">Description</span><span class="sxs-lookup"><span data-stu-id="3af99-218">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="3af99-219">type</span><span class="sxs-lookup"><span data-stu-id="3af99-219">type</span></span> |<span data-ttu-id="3af99-220">propriété de type Hello a la valeur tooAzureBlob, car les données résident dans le stockage blob Azure.</span><span class="sxs-lookup"><span data-stu-id="3af99-220">hello type property is set tooAzureBlob because data resides in Azure blob storage.</span></span> |
   | <span data-ttu-id="3af99-221">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="3af99-221">linkedServiceName</span></span> |<span data-ttu-id="3af99-222">fait référence toohello StorageLinkedService que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="3af99-222">refers toohello StorageLinkedService you created earlier.</span></span> |
   | <span data-ttu-id="3af99-223">fileName</span><span class="sxs-lookup"><span data-stu-id="3af99-223">fileName</span></span> |<span data-ttu-id="3af99-224">Cette propriété est facultative.</span><span class="sxs-lookup"><span data-stu-id="3af99-224">This property is optional.</span></span> <span data-ttu-id="3af99-225">Si vous omettez cette propriété, tous les fichiers hello hello folderPath sont récupérées.</span><span class="sxs-lookup"><span data-stu-id="3af99-225">If you omit this property, all hello files from hello folderPath are picked.</span></span> <span data-ttu-id="3af99-226">Dans ce cas, uniquement les input.log hello est traitée.</span><span class="sxs-lookup"><span data-stu-id="3af99-226">In this case, only hello input.log is processed.</span></span> |
   | <span data-ttu-id="3af99-227">type</span><span class="sxs-lookup"><span data-stu-id="3af99-227">type</span></span> |<span data-ttu-id="3af99-228">les fichiers journaux Hello étant au format texte, nous utilisons TextFormat.</span><span class="sxs-lookup"><span data-stu-id="3af99-228">hello log files are in text format, so we use TextFormat.</span></span> |
   | <span data-ttu-id="3af99-229">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="3af99-229">columnDelimiter</span></span> |<span data-ttu-id="3af99-230">colonnes dans les fichiers journaux de hello sont délimitées par un caractère de virgule hello (,).</span><span class="sxs-lookup"><span data-stu-id="3af99-230">columns in hello log files are delimited by hello comma character (,).</span></span> |
   | <span data-ttu-id="3af99-231">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="3af99-231">frequency/interval</span></span> |<span data-ttu-id="3af99-232">fréquence égale tooMonth et l’intervalle est 1, ce qui signifie que les tranches d’entrée hello sont disponibles chaque mois.</span><span class="sxs-lookup"><span data-stu-id="3af99-232">frequency set tooMonth and interval is 1, which means that hello input slices are available monthly.</span></span> |
   | <span data-ttu-id="3af99-233">external</span><span class="sxs-lookup"><span data-stu-id="3af99-233">external</span></span> |<span data-ttu-id="3af99-234">Cette propriété a la valeur tootrue si les données d’entrée hello ne sont pas générées par le service de fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="3af99-234">this property is set tootrue if hello input data is not generated by hello Data Factory service.</span></span> |
2. <span data-ttu-id="3af99-235">Exécutez hello commande Azure PowerShell toocreate hello Data Factory DataSet suivante :</span><span class="sxs-lookup"><span data-stu-id="3af99-235">Run hello following command in Azure PowerShell toocreate hello Data Factory dataset:</span></span>

    ```PowerShell
    New-AzureRmDataFactoryDataset $df -File .\InputTable.json
    ```

### <a name="create-output-dataset"></a><span data-ttu-id="3af99-236">Créer un jeu de données de sortie</span><span class="sxs-lookup"><span data-stu-id="3af99-236">Create output dataset</span></span>
<span data-ttu-id="3af99-237">Maintenant, vous créez hello sortie dataset toorepresent hello sortie les données stockées dans hello le stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="3af99-237">Now, you create hello output dataset toorepresent hello output data stored in hello Azure Blob storage.</span></span>

1. <span data-ttu-id="3af99-238">Créez un fichier JSON nommé **OutputTable.json** Bonjour **C:\ADFGetStarted** dossier avec hello suivant le contenu :</span><span class="sxs-lookup"><span data-stu-id="3af99-238">Create a JSON file named **OutputTable.json** in hello **C:\ADFGetStarted** folder with hello following content:</span></span>

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
    <span data-ttu-id="3af99-239">Hello JSON définit un dataset nommé **AzureBlobOutput**, qui représente les données de sortie d’une activité dans le pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="3af99-239">hello JSON defines a dataset named **AzureBlobOutput**, which represents output data for an activity in hello pipeline.</span></span> <span data-ttu-id="3af99-240">En outre, il spécifie que les résultats de hello sont stockés dans le conteneur d’objets blob hello appelé **adfgetstarted** et dossier hello appelé **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="3af99-240">In addition, it specifies that hello results are stored in hello blob container called **adfgetstarted** and hello folder called **partitioneddata**.</span></span> <span data-ttu-id="3af99-241">Hello **disponibilité** section spécifie ce jeu de données de sortie hello est généré sur une base mensuelle.</span><span class="sxs-lookup"><span data-stu-id="3af99-241">hello **availability** section specifies that hello output dataset is produced on a monthly basis.</span></span>
2. <span data-ttu-id="3af99-242">Exécutez hello commande Azure PowerShell toocreate hello Data Factory DataSet suivante :</span><span class="sxs-lookup"><span data-stu-id="3af99-242">Run hello following command in Azure PowerShell toocreate hello Data Factory dataset:</span></span>

    ```PowerShell
    New-AzureRmDataFactoryDataset $df -File .\OutputTable.json
    ```

## <a name="create-pipeline"></a><span data-ttu-id="3af99-243">Création d’un pipeline</span><span class="sxs-lookup"><span data-stu-id="3af99-243">Create pipeline</span></span>
<span data-ttu-id="3af99-244">Dans cette étape, vous créez votre premier pipeline avec une activité **HDInsightHive** .</span><span class="sxs-lookup"><span data-stu-id="3af99-244">In this step, you create your first pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="3af99-245">Secteur d’entrée est disponible mensuellement (fréquence : mois, intervalle : 1), la tranche de sortie est générée chaque mois et hello du planificateur pour l’activité de hello est également définie toomonthly.</span><span class="sxs-lookup"><span data-stu-id="3af99-245">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and hello scheduler property for hello activity is also set toomonthly.</span></span> <span data-ttu-id="3af99-246">paramètres Hello pour le jeu de données de sortie hello et planificateur d’activité hello doivent correspondre.</span><span class="sxs-lookup"><span data-stu-id="3af99-246">hello settings for hello output dataset and hello activity scheduler must match.</span></span> <span data-ttu-id="3af99-247">Actuellement, le dataset de sortie est les lecteurs hello planification, vous devez donc créer un dataset de sortie même si l’activité hello ne produit pas de sortie.</span><span class="sxs-lookup"><span data-stu-id="3af99-247">Currently, output dataset is what drives hello schedule, so you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="3af99-248">Si l’activité hello n’accepte aucune entrée, vous pouvez ignorer le jeu de données d’entrée création hello.</span><span class="sxs-lookup"><span data-stu-id="3af99-248">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span> <span data-ttu-id="3af99-249">propriétés qui Hello hello suivant JSON sont expliquées à fin hello de cette section.</span><span class="sxs-lookup"><span data-stu-id="3af99-249">hello properties used in hello following JSON are explained at hello end of this section.</span></span>

1. <span data-ttu-id="3af99-250">Créer un fichier JSON comportant MyFirstPipelinePSH.json dans le dossier de C:\ADFGetStarted hello hello suivant contenu :</span><span class="sxs-lookup"><span data-stu-id="3af99-250">Create a JSON file named MyFirstPipelinePSH.json in hello C:\ADFGetStarted folder with hello following content:</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="3af99-251">Remplacez **storageaccountname** avec nom hello de votre compte de stockage Bonjour JSON.</span><span class="sxs-lookup"><span data-stu-id="3af99-251">Replace **storageaccountname** with hello name of your storage account in hello JSON.</span></span>
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
    <span data-ttu-id="3af99-252">Dans l’extrait de code hello JSON, vous créez un pipeline qui se compose d’une activité unique qui utilise la ruche tooprocess données sur un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3af99-252">In hello JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive tooprocess Data on an HDInsight cluster.</span></span>

    <span data-ttu-id="3af99-253">fichier de script Hive Hello, **partitionweblogs.hql**, est stocké dans hello compte de stockage Azure (spécifié par scriptLinkedService hello, appelé **StorageLinkedService**) et dans **script**  dossier dans le conteneur de hello **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="3af99-253">hello Hive script file, **partitionweblogs.hql**, is stored in hello Azure storage account (specified by hello scriptLinkedService, called **StorageLinkedService**), and in **script** folder in hello container **adfgetstarted**.</span></span>

    <span data-ttu-id="3af99-254">Hello **définit** section est de paramètres d’exécution utilisés toospecify hello être passé le script hive de toohello en tant que valeurs de configuration Hive (exemple : ${hiveconf : inputtable}, ${hiveconf:partitionedtable}).</span><span class="sxs-lookup"><span data-stu-id="3af99-254">hello **defines** section is used toospecify hello runtime settings that be passed toohello hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span></span>

    <span data-ttu-id="3af99-255">Hello **Démarrer** et **fin** propriétés de pipeline de hello spécifie la période active de hello du pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="3af99-255">hello **start** and **end** properties of hello pipeline specifies hello active period of hello pipeline.</span></span>

    <span data-ttu-id="3af99-256">Dans l’activité hello JSON, vous spécifiez ce script Hive hello s’exécute sur le calcul hello spécifié par hello **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="3af99-256">In hello activity JSON, you specify that hello Hive script runs on hello compute specified by hello **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3af99-257">Consultez la section « JSON de Pipeline » dans [Pipelines et les activités dans Azure Data Factory](data-factory-create-pipelines.md) pour plus d’informations sur les propriétés JSON qui sont utilisées dans l’exemple de hello.</span><span class="sxs-lookup"><span data-stu-id="3af99-257">See "Pipeline JSON" in [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) for details about JSON properties that are used in hello example.</span></span>

2. <span data-ttu-id="3af99-258">Vérifiez que vous voyez hello **input.log** fichier Bonjour **adfgetstarted/inputdata** dossier hello stockage d’objets blob Azure et exécution hello suivant de pipeline de commande toodeploy hello.</span><span class="sxs-lookup"><span data-stu-id="3af99-258">Confirm that you see hello **input.log** file in hello **adfgetstarted/inputdata** folder in hello Azure blob storage, and run hello following command toodeploy hello pipeline.</span></span> <span data-ttu-id="3af99-259">Depuis hello **Démarrer** et **fin** heures sont définies dans hello passée et **isPaused** est toofalse ensemble, pipeline de hello (activité dans le pipeline de hello) immédiatement après le déploiement.</span><span class="sxs-lookup"><span data-stu-id="3af99-259">Since hello **start** and **end** times are set in hello past and **isPaused** is set toofalse, hello pipeline (activity in hello pipeline) runs immediately after you deploy.</span></span>

    ```PowerShell
    New-AzureRmDataFactoryPipeline $df -File .\MyFirstPipelinePSH.json
    ```
3. <span data-ttu-id="3af99-260">Félicitations, vous avez réussi à créer votre premier pipeline avec Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3af99-260">Congratulations, you have successfully created your first pipeline using Azure PowerShell!</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="3af99-261">Surveillance d’un pipeline</span><span class="sxs-lookup"><span data-stu-id="3af99-261">Monitor pipeline</span></span>
<span data-ttu-id="3af99-262">Dans cette étape, vous utilisez Azure PowerShell toomonitor ce qui se passe dans une fabrique de données Azure.</span><span class="sxs-lookup"><span data-stu-id="3af99-262">In this step, you use Azure PowerShell toomonitor what’s going on in an Azure data factory.</span></span>

1. <span data-ttu-id="3af99-263">Exécutez **Get-AzureRmDataFactory** et affecter hello sortie tooa **$df** variable.</span><span class="sxs-lookup"><span data-stu-id="3af99-263">Run **Get-AzureRmDataFactory** and assign hello output tooa **$df** variable.</span></span>

    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH
    ```
2. <span data-ttu-id="3af99-264">Exécutez **Get-AzureRmDataFactorySlice** tooget plus d’informations sur toutes les tranches de hello **EmpSQLTable**, qui est la table de sortie hello du pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="3af99-264">Run **Get-AzureRmDataFactorySlice** tooget details about all slices of hello **EmpSQLTable**, which is hello output table of hello pipeline.</span></span>

    ```PowerShell
    Get-AzureRmDataFactorySlice $df -DatasetName AzureBlobOutput -StartDateTime 2017-07-01
    ```
    <span data-ttu-id="3af99-265">Notez que hello %StartDateTime;) que vous spécifiez ici est hello que même heure de début spécifiée dans le code JSON de pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="3af99-265">Notice that hello StartDateTime you specify here is hello same start time specified in hello pipeline JSON.</span></span> <span data-ttu-id="3af99-266">Voici le résultat de l’exemple hello :</span><span class="sxs-lookup"><span data-stu-id="3af99-266">Here is hello sample output:</span></span>

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
3. <span data-ttu-id="3af99-267">Exécutez **Get-AzureRmDataFactoryRun** tooget les détails de hello de l’activité s’exécute pour une tranche spécifique.</span><span class="sxs-lookup"><span data-stu-id="3af99-267">Run **Get-AzureRmDataFactoryRun** tooget hello details of activity runs for a specific slice.</span></span>

    ```PowerShell
    Get-AzureRmDataFactoryRun $df -DatasetName AzureBlobOutput -StartDateTime 2017-07-01
    ```

    <span data-ttu-id="3af99-268">Voici le résultat de l’exemple hello :</span><span class="sxs-lookup"><span data-stu-id="3af99-268">Here is hello sample output:</span></span> 

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
    <span data-ttu-id="3af99-269">Vous pouvez conserver en cours d’exécution cette applet de commande jusqu'à ce que vous voyiez secteur hello dans **prêt** état ou **n’a pas pu** état.</span><span class="sxs-lookup"><span data-stu-id="3af99-269">You can keep running this cmdlet until you see hello slice in **Ready** state or **Failed** state.</span></span> <span data-ttu-id="3af99-270">Lors de la tranche de hello est prêt, vérifiez hello **partitioneddata** dossier Bonjour **adfgetstarted** conteneur dans votre stockage d’objets blob pour hello les données de sortie.</span><span class="sxs-lookup"><span data-stu-id="3af99-270">When hello slice is in Ready state, check hello **partitioneddata** folder in hello **adfgetstarted** container in your blob storage for hello output data.</span></span>  <span data-ttu-id="3af99-271">La création d’un cluster HDInsight à la demande prend généralement un certain temps.</span><span class="sxs-lookup"><span data-stu-id="3af99-271">Creation of an on-demand HDInsight cluster usually takes some time.</span></span>

    ![données de sortie](./media/data-factory-build-your-first-pipeline-using-powershell/three-ouptut-files.png)

> [!IMPORTANT]
> <span data-ttu-id="3af99-273">La création d’un cluster HDInsight à la demande prend généralement un certain temps (environ 20 minutes).</span><span class="sxs-lookup"><span data-stu-id="3af99-273">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="3af99-274">Par conséquent, s’attendent hello pipeline tootake **environ 30 minutes** tooprocess hello tranche.</span><span class="sxs-lookup"><span data-stu-id="3af99-274">Therefore, expect hello pipeline tootake **approximately 30 minutes** tooprocess hello slice.</span></span>
>
> <span data-ttu-id="3af99-275">fichier d’entrée de Hello est supprimé lors de la tranche de hello est traitée avec succès.</span><span class="sxs-lookup"><span data-stu-id="3af99-275">hello input file gets deleted when hello slice is processed successfully.</span></span> <span data-ttu-id="3af99-276">Par conséquent, si vous souhaitez tranche de hello toorerun ou que vous hello didacticiel à nouveau, téléchargez hello d’entrée (input.log) toohello inputdata dossier des fichiers du conteneur d’adfgetstarted hello.</span><span class="sxs-lookup"><span data-stu-id="3af99-276">Therefore, if you want toorerun hello slice or do hello tutorial again, upload hello input file (input.log) toohello inputdata folder of hello adfgetstarted container.</span></span>
>
>

## <a name="summary"></a><span data-ttu-id="3af99-277">Résumé</span><span class="sxs-lookup"><span data-stu-id="3af99-277">Summary</span></span>
<span data-ttu-id="3af99-278">Dans ce didacticiel, vous avez créé un Azure data factory tooprocess de données en exécutant le script Hive sur un cluster de hadoop HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3af99-278">In this tutorial, you created an Azure data factory tooprocess data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="3af99-279">Vous avez utilisé hello éditeur Data Factory dans Bonjour Azure toodo portail Bonjour comme suit :</span><span class="sxs-lookup"><span data-stu-id="3af99-279">You used hello Data Factory Editor in hello Azure portal toodo hello following steps:</span></span>

1. <span data-ttu-id="3af99-280">Création d’une **fabrique de données**Azure.</span><span class="sxs-lookup"><span data-stu-id="3af99-280">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="3af99-281">Création de deux **services liés**:</span><span class="sxs-lookup"><span data-stu-id="3af99-281">Created two **linked services**:</span></span>
   1. <span data-ttu-id="3af99-282">**Le stockage Azure** lié service toolink votre stockage d’objets blob Azure qui contient la fabrique de données toohello les fichiers d’entrée/sortie.</span><span class="sxs-lookup"><span data-stu-id="3af99-282">**Azure Storage** linked service toolink your Azure blob storage that holds input/output files toohello data factory.</span></span>
   2. <span data-ttu-id="3af99-283">**Azure HDInsight** à la demande liée service toolink une fabrique de données à la demande HDInsight Hadoop cluster toohello.</span><span class="sxs-lookup"><span data-stu-id="3af99-283">**Azure HDInsight** on-demand linked service toolink an on-demand HDInsight Hadoop cluster toohello data factory.</span></span> <span data-ttu-id="3af99-284">Azure Data Factory crée un HDInsight Hadoop données d’entrée de cluster juste-à-temps tooprocess et générer les données de sortie.</span><span class="sxs-lookup"><span data-stu-id="3af99-284">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time tooprocess input data and produce output data.</span></span>
3. <span data-ttu-id="3af99-285">Créé deux **jeux de données**, qui décrivent les données d’entrée et de sortie pour l’activité HDInsight Hive dans le pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="3af99-285">Created two **datasets**, which describe input and output data for HDInsight Hive activity in hello pipeline.</span></span>
4. <span data-ttu-id="3af99-286">Création d’un **pipeline** avec une activité **Hive HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="3af99-286">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3af99-287">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3af99-287">Next steps</span></span>
<span data-ttu-id="3af99-288">Dans cet article, vous avez créé un pipeline avec une activité de transformation (Activité HDInsight) qui exécute un script Hive sur un cluster Azure HDInsight à la demande.</span><span class="sxs-lookup"><span data-stu-id="3af99-288">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="3af99-289">toosee toouse un activité de copie toocopy des données d’une tooAzure d’objets Blob Azure SQL, voir [didacticiel : copier des données à partir d’un tooAzure d’objets Blob Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="3af99-289">toosee how toouse a Copy Activity toocopy data from an Azure Blob tooAzure SQL, see [Tutorial: Copy data from an Azure Blob tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="3af99-290">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="3af99-290">See Also</span></span>
| <span data-ttu-id="3af99-291">Rubrique</span><span class="sxs-lookup"><span data-stu-id="3af99-291">Topic</span></span> | <span data-ttu-id="3af99-292">Description</span><span class="sxs-lookup"><span data-stu-id="3af99-292">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="3af99-293">Informations de référence sur les applets de commande de Data Factory</span><span class="sxs-lookup"><span data-stu-id="3af99-293">Data Factory Cmdlet Reference</span></span>](/powershell/module/azurerm.datafactories) |<span data-ttu-id="3af99-294">Consultez la documentation complète sur les applets de commande de Data Factory</span><span class="sxs-lookup"><span data-stu-id="3af99-294">See comprehensive documentation on Data Factory cmdlets</span></span> |
| [<span data-ttu-id="3af99-295">Pipelines</span><span class="sxs-lookup"><span data-stu-id="3af99-295">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="3af99-296">Cet article vous aidera à comprendre les pipelines et les activités dans Azure Data Factory et comment toouse les tooconstruct bout en bout piloté par les données des flux de travail pour votre entreprise ou votre scénario.</span><span class="sxs-lookup"><span data-stu-id="3af99-296">This article helps you understand pipelines and activities in Azure Data Factory and how toouse them tooconstruct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="3af99-297">Groupes de données</span><span class="sxs-lookup"><span data-stu-id="3af99-297">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="3af99-298">Cet article vous aide à comprendre les jeux de données dans Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="3af99-298">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="3af99-299">Planification et exécution</span><span class="sxs-lookup"><span data-stu-id="3af99-299">Scheduling and Execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="3af99-300">Cet article explique les aspects de planification et l’exécution de hello du modèle d’application Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="3af99-300">This article explains hello scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="3af99-301">Surveiller et gérer les pipelines Azure Data Factory à l’aide de la nouvelle application de surveillance et gestion.</span><span class="sxs-lookup"><span data-stu-id="3af99-301">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="3af99-302">Cet article décrit comment toomonitor, gérer et déboguer des pipelines à l’aide de hello analyse & application de gestion.</span><span class="sxs-lookup"><span data-stu-id="3af99-302">This article describes how toomonitor, manage, and debug pipelines using hello Monitoring & Management App.</span></span> |
