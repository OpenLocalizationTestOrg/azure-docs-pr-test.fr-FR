---
title: "Didacticiel : Créer un toomove de données de pipeline à l’aide d’Azure PowerShell | Documents Microsoft"
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
ms.openlocfilehash: 21406d7dfaa0c555b2538fbb52839d761c140fc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-data-factory-pipeline-that-moves-data-by-using-azure-powershell"></a><span data-ttu-id="b7f50-103">Didacticiel : Créer un pipeline Data Factory qui déplace les données à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b7f50-103">Tutorial: Create a Data Factory pipeline that moves data by using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b7f50-104">Vue d’ensemble et étapes préalables requises</span><span class="sxs-lookup"><span data-stu-id="b7f50-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="b7f50-105">Assistant de copie</span><span class="sxs-lookup"><span data-stu-id="b7f50-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="b7f50-106">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="b7f50-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="b7f50-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b7f50-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="b7f50-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b7f50-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="b7f50-109">Modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b7f50-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="b7f50-110">API REST</span><span class="sxs-lookup"><span data-stu-id="b7f50-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="b7f50-111">API .NET</span><span class="sxs-lookup"><span data-stu-id="b7f50-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
>
>

<span data-ttu-id="b7f50-112">Dans cet article, vous apprendrez comment toouse PowerShell toocreate une fabrique de données avec un pipeline qui copie les données à partir d’une base de données SQL Azure de tooan stockage blob Azure.</span><span class="sxs-lookup"><span data-stu-id="b7f50-112">In this article, you learn how toouse PowerShell toocreate a data factory with a pipeline that copies data from an Azure blob storage tooan Azure SQL database.</span></span> <span data-ttu-id="b7f50-113">Si vous êtes tooAzure nouvelle fabrique de données, lisez hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article avant d’entamer ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="b7f50-113">If you are new tooAzure Data Factory, read through hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="b7f50-114">Dans ce didacticiel, vous créez un pipeline avec une activité : activité de copie.</span><span class="sxs-lookup"><span data-stu-id="b7f50-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="b7f50-115">activité de copie Hello copie des données à partir d’un magasin de données de données pris en charge magasin tooa récepteur pris en charge.</span><span class="sxs-lookup"><span data-stu-id="b7f50-115">hello copy activity copies data from a supported data store tooa supported sink data store.</span></span> <span data-ttu-id="b7f50-116">Pour obtenir la liste des magasins de données pris en charge en tant que sources et récepteurs, consultez [Magasins de données pris en charge](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="b7f50-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="b7f50-117">activité Hello est rendue possible par un service globalement disponible qui permettre copier des données entre différentes banques de données de manière sécurisée, fiable et évolutive.</span><span class="sxs-lookup"><span data-stu-id="b7f50-117">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="b7f50-118">Pour plus d’informations sur l’activité de copie de hello, consultez [les activités de déplacement des données](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="b7f50-118">For more information about hello Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="b7f50-119">Un pipeline peut contenir plusieurs activités.</span><span class="sxs-lookup"><span data-stu-id="b7f50-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="b7f50-120">De plus, vous pouvez concaténer les deux activités (exécutée une activité après l’autre) en définissant le dataset de sortie hello d’une activité hello d’entrée dataset Hello autre activité.</span><span class="sxs-lookup"><span data-stu-id="b7f50-120">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="b7f50-121">Pour plus d’informations, consultez [Plusieurs activités dans un pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="b7f50-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

> [!NOTE]
> <span data-ttu-id="b7f50-122">Cet article ne couvre pas toutes les applets de commande hello Data Factory.</span><span class="sxs-lookup"><span data-stu-id="b7f50-122">This article does not cover all hello Data Factory cmdlets.</span></span> <span data-ttu-id="b7f50-123">Consultez la [Référence des applets de commande Data Factory](/powershell/module/azurerm.datafactories) pour obtenir une documentation complète sur ces applets de commande.</span><span class="sxs-lookup"><span data-stu-id="b7f50-123">See [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories) for comprehensive documentation on these cmdlets.</span></span>
> 
> <span data-ttu-id="b7f50-124">le pipeline de données Hello dans ce didacticiel copie des données à partir d’un magasin de données de destination source données magasin tooa.</span><span class="sxs-lookup"><span data-stu-id="b7f50-124">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="b7f50-125">Pour obtenir un didacticiel sur la façon de tootransform les données à l’aide d’Azure Data Factory, consultez [didacticiel : créer un pipeline de données tootransform à l’aide de cluster Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="b7f50-125">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b7f50-126">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b7f50-126">Prerequisites</span></span>
- <span data-ttu-id="b7f50-127">Terminer la configuration requise indiquée dans hello [conditions préalables didacticiels](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="b7f50-127">Complete prerequisites listed in hello [tutorial prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article.</span></span>
- <span data-ttu-id="b7f50-128">Installez **Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="b7f50-128">Install **Azure PowerShell**.</span></span> <span data-ttu-id="b7f50-129">Suivez les instructions de hello dans [comment tooinstall et configurer Azure PowerShell](../powershell-install-configure.md).</span><span class="sxs-lookup"><span data-stu-id="b7f50-129">Follow hello instructions in [How tooinstall and configure Azure PowerShell](../powershell-install-configure.md).</span></span>

## <a name="steps"></a><span data-ttu-id="b7f50-130">Étapes</span><span class="sxs-lookup"><span data-stu-id="b7f50-130">Steps</span></span>
<span data-ttu-id="b7f50-131">Voici les étapes hello que vous effectuez dans le cadre de ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="b7f50-131">Here are hello steps you perform as part of this tutorial:</span></span>

1. <span data-ttu-id="b7f50-132">Créez une **fabrique de données** Azure.</span><span class="sxs-lookup"><span data-stu-id="b7f50-132">Create an Azure **data factory**.</span></span> <span data-ttu-id="b7f50-133">Dans cette étape, vous créez une fabrique de données nommée ADFTutorialDataFactoryPSH.</span><span class="sxs-lookup"><span data-stu-id="b7f50-133">In this step, you create a data factory named ADFTutorialDataFactoryPSH.</span></span> 
2. <span data-ttu-id="b7f50-134">Créer **services liés** dans la fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="b7f50-134">Create **linked services** in hello data factory.</span></span> <span data-ttu-id="b7f50-135">Au cours de cette étape, vous allez créer deux services liés de types : Stockage Azure et base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="b7f50-135">In this step, you create two linked services of types: Azure Storage and Azure SQL Database.</span></span> 
    
    <span data-ttu-id="b7f50-136">Hello AzureStorageLinkedService lie votre fabrique de données toohello compte stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="b7f50-136">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="b7f50-137">Création d’un conteneur et de téléchargé de compte de stockage de données toothis dans le cadre de [conditions préalables](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="b7f50-137">You created a container and uploaded data toothis storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

    <span data-ttu-id="b7f50-138">AzureSqlLinkedService lie votre fabrique de données de toohello de base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="b7f50-138">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="b7f50-139">données Hello sont copiées à partir du stockage d’objets blob hello sont stockées dans cette base de données.</span><span class="sxs-lookup"><span data-stu-id="b7f50-139">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="b7f50-140">Vous avez créé une table SQL dans cette base de données en remplissant les [conditions préalables](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="b7f50-140">You created a SQL table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   
3. <span data-ttu-id="b7f50-141">Créer des entrées et sorties **jeux de données** dans la fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="b7f50-141">Create input and output **datasets** in hello data factory.</span></span>  
    
    <span data-ttu-id="b7f50-142">service lié Azure storage de Hello spécifie la chaîne de connexion hello service Data Factory utilise au moment de l’exécution tooconnect tooyour compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="b7f50-142">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="b7f50-143">Et, le jeu de données objet blob d’entrée hello Spécifie le conteneur de hello et dossier hello qui contient les données d’entrée hello.</span><span class="sxs-lookup"><span data-stu-id="b7f50-143">And, hello input blob dataset specifies hello container and hello folder that contains hello input data.</span></span>  

    <span data-ttu-id="b7f50-144">De même, hello service de base de données SQL Azure lié spécifie la chaîne de connexion hello service Data Factory utilise au moment de l’exécution tooconnect tooyour Azure base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="b7f50-144">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="b7f50-145">De plus, hello sortie SQL table dataset spécifie table hello dans les données de hello toowhich hello de base de données à partir du stockage d’objets blob hello est copié.</span><span class="sxs-lookup"><span data-stu-id="b7f50-145">And, hello output SQL table dataset specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span>
4. <span data-ttu-id="b7f50-146">Créer un **pipeline** dans la fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="b7f50-146">Create a **pipeline** in hello data factory.</span></span> <span data-ttu-id="b7f50-147">Dans cette étape, vous allez créer un pipeline avec une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="b7f50-147">In this step, you create a pipeline with a copy activity.</span></span>   
    
    <span data-ttu-id="b7f50-148">activité de copie Hello copie des données à partir d’un objet blob dans la table du tooa du stockage blob Azure hello dans la base de données SQL Azure hello.</span><span class="sxs-lookup"><span data-stu-id="b7f50-148">hello copy activity copies data from a blob in hello Azure blob storage tooa table in hello Azure SQL database.</span></span> <span data-ttu-id="b7f50-149">Vous pouvez utiliser une activité de copie dans un pipeline toocopy des données d’une destination de tooany pris en charge source prise en charge.</span><span class="sxs-lookup"><span data-stu-id="b7f50-149">You can use a copy activity in a pipeline toocopy data from any supported source tooany supported destination.</span></span> <span data-ttu-id="b7f50-150">Pour obtenir la liste des magasins de données pris en charge, consultez [Activités de déplacement des données](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="b7f50-150">For a list of supported data stores, see [data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> 
5. <span data-ttu-id="b7f50-151">Pipeline de hello moniteur.</span><span class="sxs-lookup"><span data-stu-id="b7f50-151">Monitor hello pipeline.</span></span> <span data-ttu-id="b7f50-152">Dans cette étape, vous **moniteur** hello tranches de jeux de données d’entrée et de sortie à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b7f50-152">In this step, you **monitor** hello slices of input and output datasets by using PowerShell.</span></span>

## <a name="create-a-data-factory"></a><span data-ttu-id="b7f50-153">Créer une fabrique de données</span><span class="sxs-lookup"><span data-stu-id="b7f50-153">Create a data factory</span></span>
> [!IMPORTANT]
> <span data-ttu-id="b7f50-154">Complète [conditions préalables requises pour le didacticiel de hello](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) si vous n’avez pas déjà fait.</span><span class="sxs-lookup"><span data-stu-id="b7f50-154">Complete [prerequisites for hello tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) if you haven't already done so.</span></span>   

<span data-ttu-id="b7f50-155">Une fabrique de données peut avoir un ou plusieurs pipelines.</span><span class="sxs-lookup"><span data-stu-id="b7f50-155">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="b7f50-156">Un pipeline peut contenir une ou plusieurs activités.</span><span class="sxs-lookup"><span data-stu-id="b7f50-156">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="b7f50-157">Par exemple, un activité de copie toocopy des données d’un magasin de données de destination tooa source et un toorun d’activité HDInsight Hive un tootransform de script Hive données tooproduct sortie les données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="b7f50-157">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform input data tooproduct output data.</span></span> <span data-ttu-id="b7f50-158">Commençons par créer la fabrique de données hello dans cette étape.</span><span class="sxs-lookup"><span data-stu-id="b7f50-158">Let's start with creating hello data factory in this step.</span></span>

1. <span data-ttu-id="b7f50-159">Lancez **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="b7f50-159">Launch **PowerShell**.</span></span> <span data-ttu-id="b7f50-160">Laissez Azure PowerShell ouverte jusqu'à la fin de hello de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="b7f50-160">Keep Azure PowerShell open until hello end of this tutorial.</span></span> <span data-ttu-id="b7f50-161">Si vous fermez et rouvrez, vous devez à nouveau les commandes de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="b7f50-161">If you close and reopen, you need toorun hello commands again.</span></span>

    <span data-ttu-id="b7f50-162">Exécutez hello commande suivante, puis entrez les nom d’utilisateur hello et le mot de passe que vous utilisez toosign dans toohello portail Azure :</span><span class="sxs-lookup"><span data-stu-id="b7f50-162">Run hello following command, and enter hello user name and password that you use toosign in toohello Azure portal:</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```   
   
    <span data-ttu-id="b7f50-163">Exécutez hello suivant commande tooview tous les abonnements hello pour ce compte :</span><span class="sxs-lookup"><span data-stu-id="b7f50-163">Run hello following command tooview all hello subscriptions for this account:</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```

    <span data-ttu-id="b7f50-164">Tooselect hello abonnement toowork avec la commande suivante d’exécution hello.</span><span class="sxs-lookup"><span data-stu-id="b7f50-164">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="b7f50-165">Remplacez  **&lt;NameOfAzureSubscription** &gt; avec le nom de hello de votre abonnement Azure :</span><span class="sxs-lookup"><span data-stu-id="b7f50-165">Replace **&lt;NameOfAzureSubscription**&gt; with hello name of your Azure subscription:</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
2. <span data-ttu-id="b7f50-166">Créer un groupe de ressources Azure nommé **ADFTutorialResourceGroup** en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b7f50-166">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command:</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
    
    <span data-ttu-id="b7f50-167">Certaines des étapes hello dans ce didacticiel supposent que vous utilisez le groupe de ressources hello nommé **ADFTutorialResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="b7f50-167">Some of hello steps in this tutorial assume that you use hello resource group named **ADFTutorialResourceGroup**.</span></span> <span data-ttu-id="b7f50-168">Si vous utilisez un autre groupe de ressources, vous devez toouse il à la place de ADFTutorialResourceGroup dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="b7f50-168">If you use a different resource group, you need toouse it in place of ADFTutorialResourceGroup in this tutorial.</span></span>
3. <span data-ttu-id="b7f50-169">Exécutez hello **New-AzureRmDataFactory** toocreate de l’applet de commande une fabrique de données nommée **ADFTutorialDataFactoryPSH**:</span><span class="sxs-lookup"><span data-stu-id="b7f50-169">Run hello **New-AzureRmDataFactory** cmdlet toocreate a data factory named **ADFTutorialDataFactoryPSH**:</span></span>  

    ```PowerShell
    $df=New-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH –Location "West US"
    ```
    <span data-ttu-id="b7f50-170">Ce nom peut avoir déjà été utilisé.</span><span class="sxs-lookup"><span data-stu-id="b7f50-170">This name may already have been taken.</span></span> <span data-ttu-id="b7f50-171">Par conséquent, vous nom hello hello fabrique de données unique en ajoutant un préfixe ou un suffixe (par exemple : ADFTutorialDataFactoryPSH05152017) et réexécutez la commande hello.</span><span class="sxs-lookup"><span data-stu-id="b7f50-171">Therefore, make hello name of hello data factory unique by adding a prefix or suffix (for example: ADFTutorialDataFactoryPSH05152017) and run hello command again.</span></span>  

<span data-ttu-id="b7f50-172">Hello Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="b7f50-172">Note hello following points:</span></span>

* <span data-ttu-id="b7f50-173">nom de Hello de fabrique de données Azure hello doit être globalement unique.</span><span class="sxs-lookup"><span data-stu-id="b7f50-173">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="b7f50-174">Si vous recevez hello l’erreur suivante, renommez hello (par exemple, yournameADFTutorialDataFactoryPSH).</span><span class="sxs-lookup"><span data-stu-id="b7f50-174">If you receive hello following error, change hello name (for example, yournameADFTutorialDataFactoryPSH).</span></span> <span data-ttu-id="b7f50-175">Utilisez ce nom à la place d’ADFTutorialFactoryPSH quand vous effectuez les étapes de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="b7f50-175">Use this name in place of ADFTutorialFactoryPSH while performing steps in this tutorial.</span></span> <span data-ttu-id="b7f50-176">Consultez la rubrique [Data Factory – Règles d’affectation des noms](data-factory-naming-rules.md) pour les artefacts Data Factory.</span><span class="sxs-lookup"><span data-stu-id="b7f50-176">See [Data Factory - Naming Rules](data-factory-naming-rules.md) for Data Factory artifacts.</span></span>

    ```
    Data factory name “ADFTutorialDataFactoryPSH” is not available
    ```
* <span data-ttu-id="b7f50-177">instances de fabrique de données toocreate, vous devez être un administrateur de hello abonnement Azure ou un collaborateur.</span><span class="sxs-lookup"><span data-stu-id="b7f50-177">toocreate Data Factory instances, you must be a contributor or administrator of hello Azure subscription.</span></span>
* <span data-ttu-id="b7f50-178">nom Hello hello fabrique de données peut être enregistré comme un nom DNS dans hello futures et donc devenir visible publiquement.</span><span class="sxs-lookup"><span data-stu-id="b7f50-178">hello name of hello data factory may be registered as a DNS name in hello future, and hence become publicly visible.</span></span>
* <span data-ttu-id="b7f50-179">Hello, l’erreur suivante peut s’afficher : «**cet abonnement n’est pas un espace de noms toouse inscrits Microsoft.DataFactory.**»</span><span class="sxs-lookup"><span data-stu-id="b7f50-179">You may receive hello following error: "**This subscription is not registered toouse namespace Microsoft.DataFactory.**"</span></span> <span data-ttu-id="b7f50-180">Effectuez l’une des manières suivantes les hello et essayez de publier à nouveau :</span><span class="sxs-lookup"><span data-stu-id="b7f50-180">Do one of hello following, and try publishing again:</span></span>

  * <span data-ttu-id="b7f50-181">Dans Azure PowerShell, exécutez hello suivant le fournisseur de commandes tooregister hello fabrique de données :</span><span class="sxs-lookup"><span data-stu-id="b7f50-181">In Azure PowerShell, run hello following command tooregister hello Data Factory provider:</span></span>

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

    <span data-ttu-id="b7f50-182">Ce fournisseur est inscrit de fabrique de données hello, exécutez hello suivant tooconfirm de commande :</span><span class="sxs-lookup"><span data-stu-id="b7f50-182">Run hello following command tooconfirm that hello Data Factory provider is registered:</span></span>

    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="b7f50-183">Connectez-vous à l’aide de hello abonnement Azure toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b7f50-183">Sign in by using hello Azure subscription toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="b7f50-184">Atteindre le panneau de fabrique de données tooa ou créez une fabrique de données Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="b7f50-184">Go tooa Data Factory blade, or create a data factory in hello Azure portal.</span></span> <span data-ttu-id="b7f50-185">Cette action enregistre automatiquement le fournisseur hello pour vous.</span><span class="sxs-lookup"><span data-stu-id="b7f50-185">This action automatically registers hello provider for you.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="b7f50-186">Créez des services liés</span><span class="sxs-lookup"><span data-stu-id="b7f50-186">Create linked services</span></span>
<span data-ttu-id="b7f50-187">Vous créez des services liés dans un toolink de fabrique de données stocke de vos données et fabrique de données toohello de services de calcul.</span><span class="sxs-lookup"><span data-stu-id="b7f50-187">You create linked services in a data factory toolink your data stores and compute services toohello data factory.</span></span> <span data-ttu-id="b7f50-188">Dans ce didacticiel, vous n’allez pas utiliser n’importe quel service de calcul comme Azure HDInsight ou Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="b7f50-188">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="b7f50-189">Vous utilisez deux magasins de données de type Stockage Azure (source) et Base de données SQL Azure (destination).</span><span class="sxs-lookup"><span data-stu-id="b7f50-189">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

<span data-ttu-id="b7f50-190">Vous créez ainsi deux services liés nommés AzureStorageLinkedService et AzureSqlLinkedService de types : AzureStorage et AzureSqlDatabase.</span><span class="sxs-lookup"><span data-stu-id="b7f50-190">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="b7f50-191">Hello AzureStorageLinkedService lie votre fabrique de données toohello compte stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="b7f50-191">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="b7f50-192">Ce compte de stockage est hello une dans laquelle vous créé un conteneur et à télécharger des données de hello dans le cadre de [conditions préalables](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="b7f50-192">This storage account is hello one in which you created a container and uploaded hello data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="b7f50-193">AzureSqlLinkedService lie votre fabrique de données de toohello de base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="b7f50-193">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="b7f50-194">données Hello sont copiées à partir du stockage d’objets blob hello sont stockées dans cette base de données.</span><span class="sxs-lookup"><span data-stu-id="b7f50-194">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="b7f50-195">Vous avez créé la table emp de hello dans cette base de données dans le cadre de [conditions préalables](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="b7f50-195">You created hello emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

### <a name="create-a-linked-service-for-an-azure-storage-account"></a><span data-ttu-id="b7f50-196">Créer un service lié pour un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="b7f50-196">Create a linked service for an Azure storage account</span></span>
<span data-ttu-id="b7f50-197">Dans cette étape, vous liez votre fabrique de données tooyour compte stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="b7f50-197">In this step, you link your Azure storage account tooyour data factory.</span></span>

1. <span data-ttu-id="b7f50-198">Créez un fichier JSON nommé **AzureStorageLinkedService.json** dans **C:\ADFGetStartedPSH** dossier avec hello suivant contenu : (dossier hello créer ADFGetStartedPSH si elle n’existe pas déjà).</span><span class="sxs-lookup"><span data-stu-id="b7f50-198">Create a JSON file named **AzureStorageLinkedService.json** in **C:\ADFGetStartedPSH** folder with hello following content: (Create hello folder ADFGetStartedPSH if it does not already exist.)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="b7f50-199">Remplacez &lt;accountname&gt; et &lt;accountkey&gt; avec le nom et la clé de votre compte de stockage Azure avant d’enregistrer le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="b7f50-199">Replace &lt;accountname&gt; and &lt;accountkey&gt; with name and key of your Azure storage account before saving hello file.</span></span> 

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
2. <span data-ttu-id="b7f50-200">Dans **Azure PowerShell**, commutateur toohello **ADFGetStartedPSH** dossier.</span><span class="sxs-lookup"><span data-stu-id="b7f50-200">In **Azure PowerShell**, switch toohello **ADFGetStartedPSH** folder.</span></span>
4. <span data-ttu-id="b7f50-201">Exécutez hello **New-AzureRmDataFactoryLinkedService** hello de toocreate d’applet de commande de service lié : **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="b7f50-201">Run hello **New-AzureRmDataFactoryLinkedService** cmdlet toocreate hello linked service: **AzureStorageLinkedService**.</span></span> <span data-ttu-id="b7f50-202">Cette applet de commande et d’autres applets de commande fabrique de données que vous utilisez dans ce didacticiel requiert vous toopass des valeurs pour hello **ResourceGroupName** et **DataFactoryName** paramètres.</span><span class="sxs-lookup"><span data-stu-id="b7f50-202">This cmdlet, and other Data Factory cmdlets you use in this tutorial requires you toopass values for hello **ResourceGroupName** and **DataFactoryName** parameters.</span></span> <span data-ttu-id="b7f50-203">Vous pouvez également, vous pouvez passer l’objet DataFactory hello retourné par l’applet de commande New-AzureRmDataFactory hello sans avoir à taper ResourceGroupName et DataFactoryName chaque fois que vous exécutez une applet de commande.</span><span class="sxs-lookup"><span data-stu-id="b7f50-203">Alternatively, you can pass hello DataFactory object returned by hello New-AzureRmDataFactory cmdlet without typing ResourceGroupName and DataFactoryName each time you run a cmdlet.</span></span> 

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureStorageLinkedService.json
    ```
    <span data-ttu-id="b7f50-204">Voici le résultat de l’exemple hello :</span><span class="sxs-lookup"><span data-stu-id="b7f50-204">Here is hello sample output:</span></span>

    ```
    LinkedServiceName : AzureStorageLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.LinkedServiceProperties
    ProvisioningState : Succeeded
    ``` 

    <span data-ttu-id="b7f50-205">Autre méthode de création de ce service lié est toospecify nom de groupe de ressources et le nom de fabrique de données au lieu de spécifier l’objet DataFactory hello.</span><span class="sxs-lookup"><span data-stu-id="b7f50-205">Other way of creating this linked service is toospecify resource group name and data factory name instead of specifying hello DataFactory object.</span></span>  

    ```PowerShell
    New-AzureRmDataFactoryLinkedService -ResourceGroupName ADFTutorialResourceGroup -DataFactoryName <Name of your data factory> -File .\AzureStorageLinkedService.json
    ```

### <a name="create-a-linked-service-for-an-azure-sql-database"></a><span data-ttu-id="b7f50-206">Créer un service lié pour une base de données Azure SQL</span><span class="sxs-lookup"><span data-stu-id="b7f50-206">Create a linked service for an Azure SQL database</span></span>
<span data-ttu-id="b7f50-207">Dans cette étape, vous liez votre fabrique de données de tooyour de base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="b7f50-207">In this step, you link your Azure SQL database tooyour data factory.</span></span>

1. <span data-ttu-id="b7f50-208">Créer un fichier JSON comportant AzureSqlLinkedService.json dans le dossier de C:\ADFGetStartedPSH hello suivant contenu :</span><span class="sxs-lookup"><span data-stu-id="b7f50-208">Create a JSON file named AzureSqlLinkedService.json in C:\ADFGetStartedPSH folder with hello following content:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="b7f50-209">Remplacez &lt;servername&gt;, &lt;databasename&gt;, &lt;username@servername&gt;, et &lt;password&gt; par les noms de votre serveur SQL Azure, de la base de données, du compte d’utilisateur et par le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="b7f50-209">Replace &lt;servername&gt;, &lt;databasename&gt;, &lt;username@servername&gt;, and &lt;password&gt; with names of your Azure SQL server, database, user account, and password.</span></span>
    
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
2. <span data-ttu-id="b7f50-210">Exécutez hello suivant commande toocreate un service lié :</span><span class="sxs-lookup"><span data-stu-id="b7f50-210">Run hello following command toocreate a linked service:</span></span>

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureSqlLinkedService.json
    ```
    
    <span data-ttu-id="b7f50-211">Voici le résultat de l’exemple hello :</span><span class="sxs-lookup"><span data-stu-id="b7f50-211">Here is hello sample output:</span></span>

    ```
    LinkedServiceName : AzureSqlLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.LinkedServiceProperties
    ProvisioningState : Succeeded
    ```

   <span data-ttu-id="b7f50-212">Vérifiez que **autoriser l’accès des services de tooAzure** paramètre est activé pour votre serveur de base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="b7f50-212">Confirm that **Allow access tooAzure services** setting is turned on for your SQL database server.</span></span> <span data-ttu-id="b7f50-213">tooverify et mettez-le sous tension, hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="b7f50-213">tooverify and turn it on, do hello following steps:</span></span>

    1. <span data-ttu-id="b7f50-214">Connectez-vous à toohello [portail Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="b7f50-214">Log in toohello [Azure portal](https://portal.azure.com)</span></span>
    2. <span data-ttu-id="b7f50-215">Cliquez sur **davantage de services >** sur hello gauche, puis cliquez sur **serveurs SQL** Bonjour **bases de données** catégorie.</span><span class="sxs-lookup"><span data-stu-id="b7f50-215">Click **More services >** on hello left, and click **SQL servers** in hello **DATABASES** category.</span></span>
    3. <span data-ttu-id="b7f50-216">Sélectionnez votre serveur dans la liste hello de serveurs SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b7f50-216">Select your server in hello list of SQL servers.</span></span>
    4. <span data-ttu-id="b7f50-217">Dans le panneau hello SQL server, cliquez sur **afficher les paramètres de pare-feu** lien.</span><span class="sxs-lookup"><span data-stu-id="b7f50-217">On hello SQL server blade, click **Show firewall settings** link.</span></span>
    5. <span data-ttu-id="b7f50-218">Bonjour **des paramètres de pare-feu** panneau, cliquez sur **ON** pour **autoriser l’accès des services de tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="b7f50-218">In hello **Firewall settings** blade, click **ON** for **Allow access tooAzure services**.</span></span>
    6. <span data-ttu-id="b7f50-219">Cliquez sur **enregistrer** sur la barre d’outils hello.</span><span class="sxs-lookup"><span data-stu-id="b7f50-219">Click **Save** on hello toolbar.</span></span> 

## <a name="create-datasets"></a><span data-ttu-id="b7f50-220">Créez les jeux de données</span><span class="sxs-lookup"><span data-stu-id="b7f50-220">Create datasets</span></span>
<span data-ttu-id="b7f50-221">Dans l’étape précédente de hello, vous avez créé toolink de services liés de votre compte de stockage Azure et de la fabrique de données de tooyour de base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="b7f50-221">In hello previous step, you created linked services toolink your Azure Storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="b7f50-222">Dans cette étape, vous définissez deux jeux de données nommées InputDataset et OutputDataset qui représentent une entrée et les données de sortie qui sont stockées dans des magasins de données hello visés par AzureStorageLinkedService et AzureSqlLinkedService, respectivement.</span><span class="sxs-lookup"><span data-stu-id="b7f50-222">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in hello data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

<span data-ttu-id="b7f50-223">service lié Azure storage de Hello spécifie la chaîne de connexion hello service Data Factory utilise au moment de l’exécution tooconnect tooyour compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="b7f50-223">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="b7f50-224">Et, le jeu de données objet blob d’entrée hello (InputDataset) spécifie le conteneur de hello et dossier hello qui contient les données d’entrée hello.</span><span class="sxs-lookup"><span data-stu-id="b7f50-224">And, hello input blob dataset (InputDataset) specifies hello container and hello folder that contains hello input data.</span></span>  

<span data-ttu-id="b7f50-225">De même, hello service de base de données SQL Azure lié spécifie la chaîne de connexion hello service Data Factory utilise au moment de l’exécution tooconnect tooyour Azure base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="b7f50-225">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="b7f50-226">Et, hello sortie de jeu de données de table SQL (OututDataset) spécifie la table de hello Bonjour de toowhich hello de base de données à partir du stockage d’objets blob hello, les données sont copiées.</span><span class="sxs-lookup"><span data-stu-id="b7f50-226">And, hello output SQL table dataset (OututDataset) specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span> 

### <a name="create-an-input-dataset"></a><span data-ttu-id="b7f50-227">Créer un jeu de données d’entrée</span><span class="sxs-lookup"><span data-stu-id="b7f50-227">Create an input dataset</span></span>
<span data-ttu-id="b7f50-228">Dans cette étape, vous créez un dataset nommé InputDataset qui pointe le fichier d’objet blob tooa (emp.txt) dans le dossier racine de hello d’un conteneur d’objets blob (adftutorial) Bonjour Azure Storage est représenté par hello AzureStorageLinkedService lié service.</span><span class="sxs-lookup"><span data-stu-id="b7f50-228">In this step, you create a dataset named InputDataset that points tooa blob file (emp.txt) in hello root folder of a blob container (adftutorial) in hello Azure Storage represented by hello AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="b7f50-229">Si vous ne spécifiez une valeur pour le nom de fichier hello (ignorer), les données à partir de tous les objets BLOB dans le dossier d’entrée de hello sont copiés toohello destination.</span><span class="sxs-lookup"><span data-stu-id="b7f50-229">If you don't specify a value for hello fileName (or skip it), data from all blobs in hello input folder are copied toohello destination.</span></span> <span data-ttu-id="b7f50-230">Dans ce didacticiel, vous spécifiez une valeur pour le nom de fichier hello.</span><span class="sxs-lookup"><span data-stu-id="b7f50-230">In this tutorial, you specify a value for hello fileName.</span></span>  

1. <span data-ttu-id="b7f50-231">Créez un fichier JSON nommé **InputDataset.json** Bonjour **C:\ADFGetStartedPSH** dossier, avec hello suivant le contenu :</span><span class="sxs-lookup"><span data-stu-id="b7f50-231">Create a JSON file named **InputDataset.json** in hello **C:\ADFGetStartedPSH** folder, with hello following content:</span></span>

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

    <span data-ttu-id="b7f50-232">Hello tableau suivant fournit des descriptions pour les propriétés JSON hello utilisées dans l’extrait de code hello :</span><span class="sxs-lookup"><span data-stu-id="b7f50-232">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    | <span data-ttu-id="b7f50-233">Propriété</span><span class="sxs-lookup"><span data-stu-id="b7f50-233">Property</span></span> | <span data-ttu-id="b7f50-234">Description</span><span class="sxs-lookup"><span data-stu-id="b7f50-234">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="b7f50-235">type</span><span class="sxs-lookup"><span data-stu-id="b7f50-235">type</span></span> | <span data-ttu-id="b7f50-236">propriété de type Hello est définie trop**AzureBlob** , car les données résident dans un stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="b7f50-236">hello type property is set too**AzureBlob** because data resides in an Azure blob storage.</span></span> |
    | <span data-ttu-id="b7f50-237">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="b7f50-237">linkedServiceName</span></span> | <span data-ttu-id="b7f50-238">Fait référence toohello **AzureStorageLinkedService** que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="b7f50-238">Refers toohello **AzureStorageLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="b7f50-239">folderPath</span><span class="sxs-lookup"><span data-stu-id="b7f50-239">folderPath</span></span> | <span data-ttu-id="b7f50-240">Spécifie l’objet blob de hello **conteneur** et hello **dossier** qui contient des objets BLOB d’entrée.</span><span class="sxs-lookup"><span data-stu-id="b7f50-240">Specifies hello blob **container** and hello **folder** that contains input blobs.</span></span> <span data-ttu-id="b7f50-241">Dans ce didacticiel, adftutorial est le conteneur d’objets blob hello et dossier est le dossier racine de hello.</span><span class="sxs-lookup"><span data-stu-id="b7f50-241">In this tutorial, adftutorial is hello blob container and folder is hello root folder.</span></span> | 
    | <span data-ttu-id="b7f50-242">fileName</span><span class="sxs-lookup"><span data-stu-id="b7f50-242">fileName</span></span> | <span data-ttu-id="b7f50-243">Cette propriété est facultative.</span><span class="sxs-lookup"><span data-stu-id="b7f50-243">This property is optional.</span></span> <span data-ttu-id="b7f50-244">Si vous omettez cette propriété, tous les fichiers à partir de hello folderPath sont récupérées.</span><span class="sxs-lookup"><span data-stu-id="b7f50-244">If you omit this property, all files from hello folderPath are picked.</span></span> <span data-ttu-id="b7f50-245">Dans ce didacticiel, **emp.txt** n’est spécifié pour hello nom de fichier, ainsi que pour ce fichier est récupéré pour le traitement.</span><span class="sxs-lookup"><span data-stu-id="b7f50-245">In this tutorial, **emp.txt** is specified for hello fileName, so only that file is picked up for processing.</span></span> |
    | <span data-ttu-id="b7f50-246">format -> type</span><span class="sxs-lookup"><span data-stu-id="b7f50-246">format -> type</span></span> |<span data-ttu-id="b7f50-247">fichier d’entrée de Hello est au format de texte hello, nous utilisons **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="b7f50-247">hello input file is in hello text format, so we use **TextFormat**.</span></span> |
    | <span data-ttu-id="b7f50-248">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="b7f50-248">columnDelimiter</span></span> | <span data-ttu-id="b7f50-249">colonnes Hello dans le fichier d’entrée de hello sont délimitées par **caractère virgule (`,`)**.</span><span class="sxs-lookup"><span data-stu-id="b7f50-249">hello columns in hello input file are delimited by **comma character (`,`)**.</span></span> |
    | <span data-ttu-id="b7f50-250">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="b7f50-250">frequency/interval</span></span> | <span data-ttu-id="b7f50-251">fréquence de Hello est défini trop**heure** et de l’intervalle est défini trop**1**, ce qui signifie que hello entrée tranches sont disponibles **toutes les heures**.</span><span class="sxs-lookup"><span data-stu-id="b7f50-251">hello frequency is set too**Hour** and interval is  set too**1**, which means that hello input slices are available **hourly**.</span></span> <span data-ttu-id="b7f50-252">En d’autres termes, hello service Data Factory recherche les données d’entrée toutes les heures dans le dossier racine de hello du conteneur d’objets blob (**adftutorial**) vous avez spécifié.</span><span class="sxs-lookup"><span data-stu-id="b7f50-252">In other words, hello Data Factory service looks for input data every hour in hello root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="b7f50-253">Il recherche les données de salutation dans hello pipeline début et fin des heures, pas avant ou après ces moments précis.</span><span class="sxs-lookup"><span data-stu-id="b7f50-253">It looks for hello data within hello pipeline start and end times, not before or after these times.</span></span>  |
    | <span data-ttu-id="b7f50-254">external</span><span class="sxs-lookup"><span data-stu-id="b7f50-254">external</span></span> | <span data-ttu-id="b7f50-255">Cette propriété a la valeur trop**true** si les données de salutation ne sont pas générées par ce pipeline.</span><span class="sxs-lookup"><span data-stu-id="b7f50-255">This property is set too**true** if hello data is not generated by this pipeline.</span></span> <span data-ttu-id="b7f50-256">les données d’entrée de salutation dans ce didacticiel sont dans le fichier hello emp.txt, ce qui n’est pas généré par ce pipeline, et nous avons tootrue de cette propriété.</span><span class="sxs-lookup"><span data-stu-id="b7f50-256">hello input data in this tutorial is in hello emp.txt file, which is not generated by this pipeline, so we set this property tootrue.</span></span> |

    <span data-ttu-id="b7f50-257">Pour plus d’informations sur ces propriétés JSON, voir [Connecteur de stockage Blob Azure](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="b7f50-257">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
2. <span data-ttu-id="b7f50-258">Exécutez hello suivant commande toocreate hello Data Factory dataset.</span><span class="sxs-lookup"><span data-stu-id="b7f50-258">Run hello following command toocreate hello Data Factory dataset.</span></span>

    ```PowerShell  
    New-AzureRmDataFactoryDataset $df -File .\InputDataset.json
    ```
    <span data-ttu-id="b7f50-259">Voici le résultat de l’exemple hello :</span><span class="sxs-lookup"><span data-stu-id="b7f50-259">Here is hello sample output:</span></span>

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

### <a name="create-an-output-dataset"></a><span data-ttu-id="b7f50-260">Créer un jeu de données de sortie</span><span class="sxs-lookup"><span data-stu-id="b7f50-260">Create an output dataset</span></span>
<span data-ttu-id="b7f50-261">Dans cette partie de l’étape de hello, vous créez un dataset de sortie nommé **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="b7f50-261">In this part of hello step, you create an output dataset named **OutputDataset**.</span></span> <span data-ttu-id="b7f50-262">Ce jeu de données pointe tooa SQL table dans la base de données SQL Azure hello représenté par **AzureSqlLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="b7f50-262">This dataset points tooa SQL table in hello Azure SQL database represented by **AzureSqlLinkedService**.</span></span> 

1. <span data-ttu-id="b7f50-263">Créez un fichier JSON nommé **OutputDataset.json** Bonjour **C:\ADFGetStartedPSH** dossier avec hello suivant le contenu :</span><span class="sxs-lookup"><span data-stu-id="b7f50-263">Create a JSON file named **OutputDataset.json** in hello **C:\ADFGetStartedPSH** folder with hello following content:</span></span>

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

    <span data-ttu-id="b7f50-264">Hello tableau suivant fournit des descriptions pour les propriétés JSON hello utilisées dans l’extrait de code hello :</span><span class="sxs-lookup"><span data-stu-id="b7f50-264">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    | <span data-ttu-id="b7f50-265">Propriété</span><span class="sxs-lookup"><span data-stu-id="b7f50-265">Property</span></span> | <span data-ttu-id="b7f50-266">Description</span><span class="sxs-lookup"><span data-stu-id="b7f50-266">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="b7f50-267">type</span><span class="sxs-lookup"><span data-stu-id="b7f50-267">type</span></span> | <span data-ttu-id="b7f50-268">propriété de type Hello est définie trop**AzureSqlTable** , car les données sont table tooa copiées dans une base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="b7f50-268">hello type property is set too**AzureSqlTable** because data is copied tooa table in an Azure SQL database.</span></span> |
    | <span data-ttu-id="b7f50-269">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="b7f50-269">linkedServiceName</span></span> | <span data-ttu-id="b7f50-270">Fait référence toohello **AzureSqlLinkedService** que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="b7f50-270">Refers toohello **AzureSqlLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="b7f50-271">TableName</span><span class="sxs-lookup"><span data-stu-id="b7f50-271">tableName</span></span> | <span data-ttu-id="b7f50-272">Hello spécifié **table** toowhich hello données sont copiées.</span><span class="sxs-lookup"><span data-stu-id="b7f50-272">Specified hello **table** toowhich hello data is copied.</span></span> | 
    | <span data-ttu-id="b7f50-273">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="b7f50-273">frequency/interval</span></span> | <span data-ttu-id="b7f50-274">Hello fréquence est définie trop**heure** et l’intervalle est **1**, ce qui signifie que les tranches de sortie hello sont produits **toutes les heures** entre le début du pipeline hello et les heures, pas avant de fin ou après ces moments précis.</span><span class="sxs-lookup"><span data-stu-id="b7f50-274">hello frequency is set too**Hour** and interval is **1**, which means that hello output slices are produced **hourly** between hello pipeline start and end times, not before or after these times.</span></span>  |

    <span data-ttu-id="b7f50-275">Il existe trois colonnes : **ID**, **FirstName**, et **LastName** : dans la table emp de hello dans la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="b7f50-275">There are three columns – **ID**, **FirstName**, and **LastName** – in hello emp table in hello database.</span></span> <span data-ttu-id="b7f50-276">ID est une colonne d’identité, vous devez toospecify uniquement **FirstName** et **LastName** ici.</span><span class="sxs-lookup"><span data-stu-id="b7f50-276">ID is an identity column, so you need toospecify only **FirstName** and **LastName** here.</span></span>

    <span data-ttu-id="b7f50-277">Pour plus d’informations sur ces propriétés JSON, consultez l’article [Connecteur SQL Azure](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="b7f50-277">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
2. <span data-ttu-id="b7f50-278">Exécutez hello suivant le jeu de données de la fabrique de données de commande toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="b7f50-278">Run hello following command toocreate hello data factory dataset.</span></span>

    ```PowerShell   
    New-AzureRmDataFactoryDataset $df -File .\OutputDataset.json
    ```

    <span data-ttu-id="b7f50-279">Voici le résultat de l’exemple hello :</span><span class="sxs-lookup"><span data-stu-id="b7f50-279">Here is hello sample output:</span></span>

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

## <a name="create-a-pipeline"></a><span data-ttu-id="b7f50-280">Créer un pipeline</span><span class="sxs-lookup"><span data-stu-id="b7f50-280">Create a pipeline</span></span>
<span data-ttu-id="b7f50-281">Dans cette étape, vous créez un pipeline avec une **activité de copie** qui utilise **InputDataset** en entrée et **OutputDataset** en sortie.</span><span class="sxs-lookup"><span data-stu-id="b7f50-281">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

<span data-ttu-id="b7f50-282">Actuellement, le dataset de sortie est les lecteurs hello planification.</span><span class="sxs-lookup"><span data-stu-id="b7f50-282">Currently, output dataset is what drives hello schedule.</span></span> <span data-ttu-id="b7f50-283">Dans ce didacticiel, le dataset de sortie est tooproduce configuré une tranche une fois par heure.</span><span class="sxs-lookup"><span data-stu-id="b7f50-283">In this tutorial, output dataset is configured tooproduce a slice once an hour.</span></span> <span data-ttu-id="b7f50-284">pipeline de Hello a une heure de début et l’heure de fin sont un jour séparé, ce qui est de 24 heures.</span><span class="sxs-lookup"><span data-stu-id="b7f50-284">hello pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="b7f50-285">Par conséquent, 24 tranches du jeu de données de sortie produits par le pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="b7f50-285">Therefore, 24 slices of output dataset are produced by hello pipeline.</span></span> 


1. <span data-ttu-id="b7f50-286">Créez un fichier JSON nommé **ADFTutorialPipeline.json** Bonjour **C:\ADFGetStartedPSH** dossier, avec hello suivant le contenu :</span><span class="sxs-lookup"><span data-stu-id="b7f50-286">Create a JSON file named **ADFTutorialPipeline.json** in hello **C:\ADFGetStartedPSH** folder, with hello following content:</span></span>

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
    <span data-ttu-id="b7f50-287">Hello Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="b7f50-287">Note hello following points:</span></span>
   
    - <span data-ttu-id="b7f50-288">Dans la section d’activités hello, il n'existe qu’une seule activité dont **type** est défini trop**copie**.</span><span class="sxs-lookup"><span data-stu-id="b7f50-288">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span> <span data-ttu-id="b7f50-289">Pour plus d’informations sur l’activité de copie hello, consultez [les activités de déplacement des données](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="b7f50-289">For more information about hello copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="b7f50-290">Dans les solutions Data Factory, vous pouvez également utiliser [Activités de transformation des données](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="b7f50-290">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="b7f50-291">Entrée d’activité hello est définie trop**InputDataset** et de sortie d’activité hello est définie trop**OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="b7f50-291">Input for hello activity is set too**InputDataset** and output for hello activity is set too**OutputDataset**.</span></span> 
    - <span data-ttu-id="b7f50-292">Bonjour **typeProperties** section, **BlobSource** est spécifié comme type de source de hello et **SqlSink** est spécifié comme type de récepteur hello.</span><span class="sxs-lookup"><span data-stu-id="b7f50-292">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span> <span data-ttu-id="b7f50-293">Pour obtenir une liste complète des magasins de données pris en charge par l’activité de copie hello en tant que sources et récepteurs, consultez [prise en charge des magasins de données](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="b7f50-293">For a complete list of data stores supported by hello copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="b7f50-294">toolearn comment toouse données pris en charge spécifiques stocker en tant que source/récepteur, cliquez sur lien hello dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="b7f50-294">toolearn how toouse a specific supported data store as a source/sink, click hello link in hello table.</span></span>  
     
    <span data-ttu-id="b7f50-295">Remplacez la valeur hello hello **Démarrer** propriété hello jour actuel et **fin** valeur avec hello jour suivant.</span><span class="sxs-lookup"><span data-stu-id="b7f50-295">Replace hello value of hello **start** property with hello current day and **end** value with hello next day.</span></span> <span data-ttu-id="b7f50-296">Vous pouvez spécifier qu’une partie date hello et ignorer la partie heure hello hello date heure.</span><span class="sxs-lookup"><span data-stu-id="b7f50-296">You can specify only hello date part and skip hello time part of hello date time.</span></span> <span data-ttu-id="b7f50-297">Par exemple, « 2016-02-03 », qui est l’équivalent trop « 2016-02-03T00:00:00Z »</span><span class="sxs-lookup"><span data-stu-id="b7f50-297">For example, "2016-02-03", which is equivalent too"2016-02-03T00:00:00Z"</span></span>
     
    <span data-ttu-id="b7f50-298">Les dates/heures de début et de fin doivent toutes deux être au [format ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="b7f50-298">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="b7f50-299">Par exemple : 2016-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="b7f50-299">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="b7f50-300">Hello **fin** temps est facultatif, mais nous l’utilisons dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="b7f50-300">hello **end** time is optional, but we use it in this tutorial.</span></span> 
     
    <span data-ttu-id="b7f50-301">Si vous ne spécifiez pas de valeur pour hello **fin** propriété, il est calculé en tant que «**start + 48 heures**».</span><span class="sxs-lookup"><span data-stu-id="b7f50-301">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="b7f50-302">pipeline de hello toorun indéfiniment, spécifiez **9999-09-09** en tant que valeur hello pour hello **fin** propriété.</span><span class="sxs-lookup"><span data-stu-id="b7f50-302">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span>
     
    <span data-ttu-id="b7f50-303">Hello précédent exemple, sont des tranches de données 24 comme chaque tranche de données est généré toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="b7f50-303">In hello preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

    <span data-ttu-id="b7f50-304">Pour obtenir une description des propriétés JSON dans une définition de pipeline, consultez l’article [Créer des pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="b7f50-304">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="b7f50-305">Pour obtenir une description des propriétés JSON dans une définition d’activité de copie, consultez [Activités de déplacement des données](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="b7f50-305">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="b7f50-306">Pour obtenir une description des propriétés JSON prises en charge par BlobSource, consultez l’article [Connecteur de stockage Blob Azure](data-factory-azure-blob-connector.md).</span><span class="sxs-lookup"><span data-stu-id="b7f50-306">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="b7f50-307">Pour obtenir une description des propriétés JSON prises en charge par SqlSink, consultez l’article [Connecteur de base de données SQL Azure](data-factory-azure-sql-connector.md).</span><span class="sxs-lookup"><span data-stu-id="b7f50-307">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>
2. <span data-ttu-id="b7f50-308">Exécutez hello commande toocreate hello données fabrique tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="b7f50-308">Run hello following command toocreate hello data factory table.</span></span>

    ```PowerShell   
    New-AzureRmDataFactoryPipeline $df -File .\ADFTutorialPipeline.json
    ```

    <span data-ttu-id="b7f50-309">Voici le résultat de l’exemple hello :</span><span class="sxs-lookup"><span data-stu-id="b7f50-309">Here is hello sample output:</span></span> 

    ```
    PipelineName      : ADFTutorialPipeline
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.PipelinePropertie
    ProvisioningState : Succeeded
    ```

<span data-ttu-id="b7f50-310">**Félicitations !**</span><span class="sxs-lookup"><span data-stu-id="b7f50-310">**Congratulations!**</span></span> <span data-ttu-id="b7f50-311">Vous venez de créer une fabrique de données Azure avec un pipeline toocopy des données d’une base de données SQL Azure de tooan stockage blob Azure.</span><span class="sxs-lookup"><span data-stu-id="b7f50-311">You have successfully created an Azure data factory with a pipeline toocopy data from an Azure blob storage tooan Azure SQL database.</span></span> 

## <a name="monitor-hello-pipeline"></a><span data-ttu-id="b7f50-312">Pipeline d’analyse hello</span><span class="sxs-lookup"><span data-stu-id="b7f50-312">Monitor hello pipeline</span></span>
<span data-ttu-id="b7f50-313">Dans cette étape, vous utilisez Azure PowerShell toomonitor ce qui se passe dans une fabrique de données Azure.</span><span class="sxs-lookup"><span data-stu-id="b7f50-313">In this step, you use Azure PowerShell toomonitor what’s going on in an Azure data factory.</span></span>

1. <span data-ttu-id="b7f50-314">Remplacez &lt;DataFactoryName&gt; avec nom hello de la fabrique de données et votre **Get-AzureRmDataFactory**et assigner hello sortie tooa $df variable.</span><span class="sxs-lookup"><span data-stu-id="b7f50-314">Replace &lt;DataFactoryName&gt; with hello name of your data factory and run **Get-AzureRmDataFactory**, and assign hello output tooa variable $df.</span></span>

    ```PowerShell  
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name <DataFactoryName>
    ```

    <span data-ttu-id="b7f50-315">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="b7f50-315">For example:</span></span>
    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH0516
    ```
    
    <span data-ttu-id="b7f50-316">Ensuite, exécutez le contenu d’impression hello Hello de toosee $df après la sortie :</span><span class="sxs-lookup"><span data-stu-id="b7f50-316">Then, run print hello contents of $df toosee hello following output:</span></span> 
    
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
2. <span data-ttu-id="b7f50-317">Exécutez **Get-AzureRmDataFactorySlice** tooget plus d’informations sur toutes les tranches de hello **OutputDataset**, qui est le jeu de données hello sortie du pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="b7f50-317">Run **Get-AzureRmDataFactorySlice** tooget details about all slices of hello **OutputDataset**, which is hello output dataset of hello pipeline.</span></span>  

    ```PowerShell   
    Get-AzureRmDataFactorySlice $df -DatasetName OutputDataset -StartDateTime 2017-05-11T00:00:00Z
    ```

   <span data-ttu-id="b7f50-318">Ce paramètre doit correspondre à hello **Démarrer** valeur dans le code JSON de pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="b7f50-318">This setting should match hello **Start** value in hello pipeline JSON.</span></span> <span data-ttu-id="b7f50-319">Vous devez voir 24 secteurs, un pour chaque heure de 12 : 00 de hello jour too12 suis Hello jour suivant.</span><span class="sxs-lookup"><span data-stu-id="b7f50-319">You should see 24 slices, one for each hour from 12 AM of hello current day too12 AM of hello next day.</span></span>

   <span data-ttu-id="b7f50-320">Voici trois tranches d’exemple à partir de la sortie de hello :</span><span class="sxs-lookup"><span data-stu-id="b7f50-320">Here are three sample slices from hello output:</span></span> 

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
3. <span data-ttu-id="b7f50-321">Exécutez **Get-AzureRmDataFactoryRun** tooget les détails de hello de l’activité s’exécute pour un **spécifique** tranche.</span><span class="sxs-lookup"><span data-stu-id="b7f50-321">Run **Get-AzureRmDataFactoryRun** tooget hello details of activity runs for a **specific** slice.</span></span> <span data-ttu-id="b7f50-322">Copier la valeur de date-heure hello à partir de la sortie hello de hello commande toospecify hello valeur précédente pour le paramètre de %StartDateTime;) hello.</span><span class="sxs-lookup"><span data-stu-id="b7f50-322">Copy hello date-time value from hello output of hello previous command toospecify hello value for hello StartDateTime parameter.</span></span> 

    ```PowerShell  
    Get-AzureRmDataFactoryRun $df -DatasetName OutputDataset -StartDateTime "5/11/2017 09:00:00 PM"
    ```

   <span data-ttu-id="b7f50-323">Voici le résultat de l’exemple hello :</span><span class="sxs-lookup"><span data-stu-id="b7f50-323">Here is hello sample output:</span></span> 

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

<span data-ttu-id="b7f50-324">Pour obtenir une documentation complète sur les applets de commande Data Factory, consultez la [Référence des applets de commande Data Factory](/powershell/module/azurerm.datafactories).</span><span class="sxs-lookup"><span data-stu-id="b7f50-324">For comprehensive documentation on Data Factory cmdlets, see [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories).</span></span>

## <a name="summary"></a><span data-ttu-id="b7f50-325">Résumé</span><span class="sxs-lookup"><span data-stu-id="b7f50-325">Summary</span></span>
<span data-ttu-id="b7f50-326">Dans ce didacticiel, vous avez créé un Azure data factory toocopy de données à partir d’une base de données SQL Azure de tooan objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="b7f50-326">In this tutorial, you created an Azure data factory toocopy data from an Azure blob tooan Azure SQL database.</span></span> <span data-ttu-id="b7f50-327">Vous avez utilisé la fabrique de données PowerShell toocreate hello, services liés, jeux de données et un pipeline.</span><span class="sxs-lookup"><span data-stu-id="b7f50-327">You used PowerShell toocreate hello data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="b7f50-328">Voici les étapes principales hello que vous avez effectuées dans ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="b7f50-328">Here are hello high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="b7f50-329">Création d’une **fabrique de données**Azure.</span><span class="sxs-lookup"><span data-stu-id="b7f50-329">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="b7f50-330">Création de **services liés**:</span><span class="sxs-lookup"><span data-stu-id="b7f50-330">Created **linked services**:</span></span>

   <span data-ttu-id="b7f50-331">a.</span><span class="sxs-lookup"><span data-stu-id="b7f50-331">a.</span></span> <span data-ttu-id="b7f50-332">Un **Azure Storage** lié service toolink votre compte de stockage Azure qui contient les données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="b7f50-332">An **Azure Storage** linked service toolink your Azure storage account that holds input data.</span></span>     
   <span data-ttu-id="b7f50-333">b.</span><span class="sxs-lookup"><span data-stu-id="b7f50-333">b.</span></span> <span data-ttu-id="b7f50-334">Un **SQL Azure** lié service toolink votre base de données SQL qui contient les données de sortie hello.</span><span class="sxs-lookup"><span data-stu-id="b7f50-334">An **Azure SQL** linked service toolink your SQL database that holds hello output data.</span></span>
3. <span data-ttu-id="b7f50-335">Création de **jeux de données** qui décrivent les données d’entrée et de sortie des pipelines.</span><span class="sxs-lookup"><span data-stu-id="b7f50-335">Created **datasets** that describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="b7f50-336">Créé un **pipeline** avec **l’activité de copie**, avec **BlobSource** en tant que source de hello et **SqlSink** comme récepteur de hello.</span><span class="sxs-lookup"><span data-stu-id="b7f50-336">Created a **pipeline** with **Copy Activity**, with **BlobSource** as hello source and **SqlSink** as hello sink.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b7f50-337">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b7f50-337">Next steps</span></span>
<span data-ttu-id="b7f50-338">Dans ce didacticiel, vous avez utilisé le stockage Blob Azure comme magasin de données source et une base de données SQL Azure comme banque de données de destination dans une opération de copie.</span><span class="sxs-lookup"><span data-stu-id="b7f50-338">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="b7f50-339">Hello tableau suivant fournit une liste de banques de données pris en charge en tant que sources et destinations par l’activité de copie hello :</span><span class="sxs-lookup"><span data-stu-id="b7f50-339">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="b7f50-340">toolearn sur la banque de données de toocopy vers/à partir de données, cliquez sur lien hello hello magasin de données dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="b7f50-340">toolearn about how toocopy data to/from a data store, click hello link for hello data store in hello table.</span></span> 

