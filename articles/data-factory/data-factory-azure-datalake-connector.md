---
title: "tooand de données aaaCopy à partir d’Azure Data Lake Store | Documents Microsoft"
description: "Découvrez comment toocopy tooand de données à partir de Data Lake Store à l’aide d’Azure Data Factory"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 25b1ff3c-b2fd-48e5-b759-bb2112122e30
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jingwang
ms.openlocfilehash: 2e78f75f3821738332dacf70f6bf2c16f0136408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-data-lake-store-by-using-data-factory"></a><span data-ttu-id="4ab98-103">Copier des données tooand à partir de Data Lake Store à l’aide de Data Factory</span><span class="sxs-lookup"><span data-stu-id="4ab98-103">Copy data tooand from Data Lake Store by using Data Factory</span></span>
<span data-ttu-id="4ab98-104">Cet article explique comment toouse l’activité de copie dans Azure Data Factory toomove données tooand à partir d’Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4ab98-104">This article explains how toouse Copy Activity in Azure Data Factory toomove data tooand from Azure Data Lake Store.</span></span> <span data-ttu-id="4ab98-105">Il repose sur hello [les activités de déplacement des données](data-factory-data-movement-activities.md) de l’article, une vue d’ensemble du mouvement des données avec l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="4ab98-105">It builds on hello [Data movement activities](data-factory-data-movement-activities.md) article, an overview of data movement with Copy Activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="4ab98-106">Scénarios pris en charge</span><span class="sxs-lookup"><span data-stu-id="4ab98-106">Supported scenarios</span></span>
<span data-ttu-id="4ab98-107">Vous pouvez copier des données **à partir d’Azure Data Lake Store** toohello suivant des magasins de données :</span><span class="sxs-lookup"><span data-stu-id="4ab98-107">You can copy data **from Azure Data Lake Store** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="4ab98-108">Vous pouvez copier des données à partir de hello suivant des magasins de données **tooAzure Data Lake Store**:</span><span class="sxs-lookup"><span data-stu-id="4ab98-108">You can copy data from hello following data stores **tooAzure Data Lake Store**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> <span data-ttu-id="4ab98-109">Créez un compte Data Lake Store avant de créer un pipeline avec activité de copie.</span><span class="sxs-lookup"><span data-stu-id="4ab98-109">Create a Data Lake Store account before creating a pipeline with Copy Activity.</span></span> <span data-ttu-id="4ab98-110">Pour plus d’informations, consultez [Prise en main d’Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4ab98-110">For more information, see [Get started with Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

## <a name="supported-authentication-types"></a><span data-ttu-id="4ab98-111">Types d’authentification pris en charge</span><span class="sxs-lookup"><span data-stu-id="4ab98-111">Supported authentication types</span></span>
<span data-ttu-id="4ab98-112">connecteur de Data Lake Store Hello prend en charge ces types d’authentification :</span><span class="sxs-lookup"><span data-stu-id="4ab98-112">hello Data Lake Store connector supports these authentication types:</span></span>
* <span data-ttu-id="4ab98-113">Authentification d’un principal du service</span><span class="sxs-lookup"><span data-stu-id="4ab98-113">Service principal authentication</span></span>
* <span data-ttu-id="4ab98-114">Utilisation de l’authentification des informations d’identification utilisateur (OAuth)</span><span class="sxs-lookup"><span data-stu-id="4ab98-114">User credential (OAuth) authentication</span></span> 

<span data-ttu-id="4ab98-115">Nous vous recommandons d’utiliser l’authentification de principal du service, en particulier pour une copie planifiée des données.</span><span class="sxs-lookup"><span data-stu-id="4ab98-115">We recommend that you use service principal authentication, especially for a scheduled data copy.</span></span> <span data-ttu-id="4ab98-116">Un comportement d’expiration de jeton peut se produire avec l’authentification par informations d’identification utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4ab98-116">Token expiration behavior can occur with user credential authentication.</span></span> <span data-ttu-id="4ab98-117">Pour plus d’informations, consultez hello [lié des propriétés du service](#linked-service-properties) section.</span><span class="sxs-lookup"><span data-stu-id="4ab98-117">For configuration details, see hello [Linked service properties](#linked-service-properties) section.</span></span>

## <a name="get-started"></a><span data-ttu-id="4ab98-118">Prise en main</span><span class="sxs-lookup"><span data-stu-id="4ab98-118">Get started</span></span>
<span data-ttu-id="4ab98-119">Vous pouvez créer un pipeline avec une activité de copie qui déplace les données vers ou à partir d’Azure Data Lake Store à l’aide de différents outils/API.</span><span class="sxs-lookup"><span data-stu-id="4ab98-119">You can create a pipeline with a copy activity that moves data to/from an Azure Data Lake Store by using different tools/APIs.</span></span>

<span data-ttu-id="4ab98-120">toocreate de façon plus simple Hello une données toocopy de pipeline est toouse hello **Assistant copie de**.</span><span class="sxs-lookup"><span data-stu-id="4ab98-120">hello easiest way toocreate a pipeline toocopy data is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="4ab98-121">Pour obtenir un didacticiel sur la création d’un pipeline à l’aide d’Assistant copie de hello, consultez [didacticiel : créer un pipeline à l’aide d’Assistant copie de](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="4ab98-121">For a tutorial on creating a pipeline by using hello Copy Wizard, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="4ab98-122">Vous pouvez également utiliser hello suivant outils toocreate un pipeline : **portail Azure**, **Visual Studio**, **Azure PowerShell**, **modèle Azure Resource Manager** , **API .NET**, et **API REST**.</span><span class="sxs-lookup"><span data-stu-id="4ab98-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="4ab98-123">Consultez [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions toocreate un pipeline avec une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="4ab98-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="4ab98-124">Si vous utilisez hello ou une API, vous effectuez hello suivant les étapes toocreate un pipeline qui déplace la banque de données récepteur tooa du magasin de données à partir des données d’une source :</span><span class="sxs-lookup"><span data-stu-id="4ab98-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="4ab98-125">Création d'une **fabrique de données**.</span><span class="sxs-lookup"><span data-stu-id="4ab98-125">Create a **data factory**.</span></span> <span data-ttu-id="4ab98-126">Une fabrique de données peut contenir un ou plusieurs pipelines.</span><span class="sxs-lookup"><span data-stu-id="4ab98-126">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="4ab98-127">Créer **services liés** fabrique de données tooyour toolink les données d’entrée et de sortie magasins.</span><span class="sxs-lookup"><span data-stu-id="4ab98-127">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="4ab98-128">Par exemple, si vous copiez des données à partir d’un tooan de stockage d’objets blob Azure Azure Data Lake Store, vous créez deux services liés toolink votre compte de stockage et de la fabrique de données Azure Data Lake store tooyour.</span><span class="sxs-lookup"><span data-stu-id="4ab98-128">For example, if you are copying data from an Azure blob storage tooan Azure Data Lake Store, you create two linked services toolink your Azure storage account and Azure Data Lake store tooyour data factory.</span></span> <span data-ttu-id="4ab98-129">Pour les propriétés de service lié qui sont spécifique tooAzure Data Lake Store, consultez [lié des propriétés du service](#linked-service-properties) section.</span><span class="sxs-lookup"><span data-stu-id="4ab98-129">For linked service properties that are specific tooAzure Data Lake Store, see [linked service properties](#linked-service-properties) section.</span></span> 
2. <span data-ttu-id="4ab98-130">Créer **datasets** toorepresent d’entrée et sortie l’opération de copie des données pour hello.</span><span class="sxs-lookup"><span data-stu-id="4ab98-130">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="4ab98-131">Exemple hello mentionné dans la dernière étape de hello, vous permet de créer un conteneur d’objets blob de jeu de données toospecify hello et un dossier qui contient les données d’entrée hello.</span><span class="sxs-lookup"><span data-stu-id="4ab98-131">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="4ab98-132">De plus, vous créez un autre jeu de données toospecify hello dossier et le fichier de chemin d’accès dans le magasin Data Lake hello qui contient les données hello copiées à partir du stockage d’objets blob hello.</span><span class="sxs-lookup"><span data-stu-id="4ab98-132">And, you create another dataset toospecify hello folder and file path in hello Data Lake store that holds hello data copied from hello blob storage.</span></span> <span data-ttu-id="4ab98-133">Pour les propriétés du dataset qui sont spécifique tooAzure Data Lake Store, consultez [propriétés du dataset](#dataset-properties) section.</span><span class="sxs-lookup"><span data-stu-id="4ab98-133">For dataset properties that are specific tooAzure Data Lake Store, see [dataset properties](#dataset-properties) section.</span></span>
3. <span data-ttu-id="4ab98-134">Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="4ab98-134">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="4ab98-135">Dans l’exemple hello mentionné précédemment, vous utilisez BlobSource en tant que source et AzureDataLakeStoreSink comme un récepteur pour l’activité de copie hello.</span><span class="sxs-lookup"><span data-stu-id="4ab98-135">In hello example mentioned earlier, you use BlobSource as a source and AzureDataLakeStoreSink as a sink for hello copy activity.</span></span> <span data-ttu-id="4ab98-136">De même, si vous copiez à partir d’Azure Data Lake Store tooAzure stockage d’objets Blob, vous utilisez AzureDataLakeStoreSource et BlobSink dans l’activité de copie hello.</span><span class="sxs-lookup"><span data-stu-id="4ab98-136">Similarly, if you are copying from Azure Data Lake Store tooAzure Blob Storage, you use AzureDataLakeStoreSource  and BlobSink in hello copy activity.</span></span> <span data-ttu-id="4ab98-137">Pour les propriétés d’activité de copie qui sont spécifique tooAzure Data Lake Store, consultez [copier les propriétés de l’activité](#copy-activity-properties) section.</span><span class="sxs-lookup"><span data-stu-id="4ab98-137">For copy activity properties that are specific tooAzure Data Lake Store, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="4ab98-138">Pour plus d’informations sur comment toouse du magasin de données source ou un récepteur, cliquez sur le lien hello dans la section précédente de hello pour votre magasin de données.</span><span class="sxs-lookup"><span data-stu-id="4ab98-138">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>  

<span data-ttu-id="4ab98-139">Lorsque vous utilisez hello Assistant, les définitions de JSON pour ces entités de fabrique de données (services liés, des datasets et pipeline de hello) sont créées automatiquement pour vous.</span><span class="sxs-lookup"><span data-stu-id="4ab98-139">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="4ab98-140">Lorsque vous utilisez/API des outils (à l’exception des API .NET), vous définissez ces entités de fabrique de données à l’aide du format JSON de hello.</span><span class="sxs-lookup"><span data-stu-id="4ab98-140">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="4ab98-141">Pour plus d’exemples de définitions de JSON pour les entités de fabrique de données qui sont utilisées toocopy des données vers/depuis une Azure Data Lake Store, consultez [exemples JSON](#json-examples-for-copying-data-to-and-from-data-lake-store) section de cet article.</span><span class="sxs-lookup"><span data-stu-id="4ab98-141">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an Azure Data Lake Store, see [JSON examples](#json-examples-for-copying-data-to-and-from-data-lake-store) section of this article.</span></span>

<span data-ttu-id="4ab98-142">Hello les sections suivantes fournit des détails sur les propriétés JSON qui sont utilisé toodefine Data Factory entités spécifiques tooData Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4ab98-142">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooData Lake Store.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="4ab98-143">Propriétés du service lié</span><span class="sxs-lookup"><span data-stu-id="4ab98-143">Linked service properties</span></span>
<span data-ttu-id="4ab98-144">Un service lié lie une fabrique de données de tooa de magasin de données.</span><span class="sxs-lookup"><span data-stu-id="4ab98-144">A linked service links a data store tooa data factory.</span></span> <span data-ttu-id="4ab98-145">Vous créez un service lié de type **AzureDataLakeStore** toolink votre fabrique de données tooyour données Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4ab98-145">You create a linked service of type **AzureDataLakeStore** toolink your Data Lake Store data tooyour data factory.</span></span> <span data-ttu-id="4ab98-146">Hello tableau suivant décrit les services JSON éléments spécifiques tooData Lake Store lié.</span><span class="sxs-lookup"><span data-stu-id="4ab98-146">hello following table describes JSON elements specific tooData Lake Store linked services.</span></span> <span data-ttu-id="4ab98-147">Vous pouvez choisir entre une authentification par principal de service et par informations d’identification utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4ab98-147">You can choose between service principal and user credential authentication.</span></span>

| <span data-ttu-id="4ab98-148">Propriété</span><span class="sxs-lookup"><span data-stu-id="4ab98-148">Property</span></span> | <span data-ttu-id="4ab98-149">Description</span><span class="sxs-lookup"><span data-stu-id="4ab98-149">Description</span></span> | <span data-ttu-id="4ab98-150">Requis</span><span class="sxs-lookup"><span data-stu-id="4ab98-150">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="4ab98-151">**type**</span><span class="sxs-lookup"><span data-stu-id="4ab98-151">**type**</span></span> | <span data-ttu-id="4ab98-152">propriété de type Hello doit être définie trop**AzureDataLakeStore**.</span><span class="sxs-lookup"><span data-stu-id="4ab98-152">hello type property must be set too**AzureDataLakeStore**.</span></span> | <span data-ttu-id="4ab98-153">Oui</span><span class="sxs-lookup"><span data-stu-id="4ab98-153">Yes</span></span> |
| <span data-ttu-id="4ab98-154">**dataLakeStoreUri**</span><span class="sxs-lookup"><span data-stu-id="4ab98-154">**dataLakeStoreUri**</span></span> | <span data-ttu-id="4ab98-155">Informations sur hello compte Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4ab98-155">Information about hello Azure Data Lake Store account.</span></span> <span data-ttu-id="4ab98-156">Ces informations prennent l’une des hello suivant formats : `https://[accountname].azuredatalakestore.net/webhdfs/v1` ou `adl://[accountname].azuredatalakestore.net/`.</span><span class="sxs-lookup"><span data-stu-id="4ab98-156">This information takes one of hello following formats: `https://[accountname].azuredatalakestore.net/webhdfs/v1` or `adl://[accountname].azuredatalakestore.net/`.</span></span> | <span data-ttu-id="4ab98-157">Oui</span><span class="sxs-lookup"><span data-stu-id="4ab98-157">Yes</span></span> |
| <span data-ttu-id="4ab98-158">**subscriptionId**</span><span class="sxs-lookup"><span data-stu-id="4ab98-158">**subscriptionId**</span></span> | <span data-ttu-id="4ab98-159">Hello de toowhich ID abonnement Azure compte Data Lake Store appartient.</span><span class="sxs-lookup"><span data-stu-id="4ab98-159">Azure subscription ID toowhich hello Data Lake Store account belongs.</span></span> | <span data-ttu-id="4ab98-160">Requis pour le récepteur</span><span class="sxs-lookup"><span data-stu-id="4ab98-160">Required for sink</span></span> |
| <span data-ttu-id="4ab98-161">**resourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="4ab98-161">**resourceGroupName**</span></span> | <span data-ttu-id="4ab98-162">Hello de toowhich de nom de groupe ressource Azure compte Data Lake Store appartient.</span><span class="sxs-lookup"><span data-stu-id="4ab98-162">Azure resource group name toowhich hello Data Lake Store account belongs.</span></span> | <span data-ttu-id="4ab98-163">Requis pour le récepteur</span><span class="sxs-lookup"><span data-stu-id="4ab98-163">Required for sink</span></span> |

### <a name="service-principal-authentication-recommended"></a><span data-ttu-id="4ab98-164">Authentification d’un principal du service (recommandée)</span><span class="sxs-lookup"><span data-stu-id="4ab98-164">Service principal authentication (recommended)</span></span>
<span data-ttu-id="4ab98-165">authentification principale du service toouse, inscrire une entité de l’application dans Azure Active Directory (Azure AD) et accordez à elle hello accéder à tooData Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4ab98-165">toouse service principal authentication, register an application entity in Azure Active Directory (Azure AD) and grant it hello access tooData Lake Store.</span></span> <span data-ttu-id="4ab98-166">Consultez la page [Authentification de service à service](../data-lake-store/data-lake-store-authenticate-using-active-directory.md) pour des instructions détaillées.</span><span class="sxs-lookup"><span data-stu-id="4ab98-166">For detailed steps, see [Service-to-service authentication](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span> <span data-ttu-id="4ab98-167">Prenez note de hello après les valeurs que vous pouvez utiliser toodefine hello de service lié :</span><span class="sxs-lookup"><span data-stu-id="4ab98-167">Make note of hello following values, which you use toodefine hello linked service:</span></span>
* <span data-ttu-id="4ab98-168">ID de l'application</span><span class="sxs-lookup"><span data-stu-id="4ab98-168">Application ID</span></span>
* <span data-ttu-id="4ab98-169">Clé de l'application</span><span class="sxs-lookup"><span data-stu-id="4ab98-169">Application key</span></span> 
* <span data-ttu-id="4ab98-170">ID client</span><span class="sxs-lookup"><span data-stu-id="4ab98-170">Tenant ID</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4ab98-171">Si vous utilisez des pipelines de données hello Assistant copie tooauthor, assurez-vous que vous accordez principal du service hello au moins un **lecteur** rôle dans le contrôle d’accès (gestion des identités et des accès) pour le compte de hello Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4ab98-171">If you are using hello Copy Wizard tooauthor data pipelines, make sure that you grant hello service principal at least a **Reader** role in access control (identity and access management) for hello Data Lake Store account.</span></span> <span data-ttu-id="4ab98-172">En outre, au moins accorder principal du service hello **lecture + Execute** racine de Data Lake Store tooyour autorisation (« / ») et ses enfants.</span><span class="sxs-lookup"><span data-stu-id="4ab98-172">Also, grant hello service principal at least **Read + Execute** permission tooyour Data Lake Store root ("/") and its children.</span></span> <span data-ttu-id="4ab98-173">Dans le cas contraire, vous pouvez voir le message de salutation « hello informations d’identification fournies ne sont pas valides. »</span><span class="sxs-lookup"><span data-stu-id="4ab98-173">Otherwise you might see hello message "hello credentials provided are invalid."</span></span><br/><br/>
<span data-ttu-id="4ab98-174">Une fois que vous créez ou mettez à jour un principal de service dans Azure AD, il peut prendre quelques minutes pour effet de tootake modifications hello.</span><span class="sxs-lookup"><span data-stu-id="4ab98-174">After you create or update a service principal in Azure AD, it can take a few minutes for hello changes tootake effect.</span></span> <span data-ttu-id="4ab98-175">Vérifiez le principal du service hello et configurations de liste (ACL) du contrôle de l’accès Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4ab98-175">Check hello service principal and Data Lake Store access control list (ACL) configurations.</span></span> <span data-ttu-id="4ab98-176">Si vous voyez toujours le message « hello informations d’identification fournies ne sont pas valides » de type hello, patientez et réessayez.</span><span class="sxs-lookup"><span data-stu-id="4ab98-176">If you still see hello message "hello credentials provided are invalid," wait a while and try again.</span></span>

<span data-ttu-id="4ab98-177">Utilisez l’authentification principale du service en spécifiant hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="4ab98-177">Use service principal authentication by specifying hello following properties:</span></span>

| <span data-ttu-id="4ab98-178">Propriété</span><span class="sxs-lookup"><span data-stu-id="4ab98-178">Property</span></span> | <span data-ttu-id="4ab98-179">Description</span><span class="sxs-lookup"><span data-stu-id="4ab98-179">Description</span></span> | <span data-ttu-id="4ab98-180">Requis</span><span class="sxs-lookup"><span data-stu-id="4ab98-180">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="4ab98-181">**servicePrincipalId**</span><span class="sxs-lookup"><span data-stu-id="4ab98-181">**servicePrincipalId**</span></span> | <span data-ttu-id="4ab98-182">Spécifiez l’ID client de. l’application hello</span><span class="sxs-lookup"><span data-stu-id="4ab98-182">Specify hello application's client ID.</span></span> | <span data-ttu-id="4ab98-183">Oui</span><span class="sxs-lookup"><span data-stu-id="4ab98-183">Yes</span></span> |
| <span data-ttu-id="4ab98-184">**servicePrincipalKey**</span><span class="sxs-lookup"><span data-stu-id="4ab98-184">**servicePrincipalKey**</span></span> | <span data-ttu-id="4ab98-185">Spécifiez la clé de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="4ab98-185">Specify hello application's key.</span></span> | <span data-ttu-id="4ab98-186">Oui</span><span class="sxs-lookup"><span data-stu-id="4ab98-186">Yes</span></span> |
| <span data-ttu-id="4ab98-187">**client**</span><span class="sxs-lookup"><span data-stu-id="4ab98-187">**tenant**</span></span> | <span data-ttu-id="4ab98-188">Spécifiez les informations de locataire hello (ID client ou le nom de domaine) dans lequel réside votre application.</span><span class="sxs-lookup"><span data-stu-id="4ab98-188">Specify hello tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="4ab98-189">Vous pouvez le récupérer par pointage de souris hello dans le coin supérieur droit de hello Hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="4ab98-189">You can retrieve it by hovering hello mouse in hello upper-right corner of hello Azure portal.</span></span> | <span data-ttu-id="4ab98-190">Oui</span><span class="sxs-lookup"><span data-stu-id="4ab98-190">Yes</span></span> |

<span data-ttu-id="4ab98-191">**Exemple : authentification du principal de service**</span><span class="sxs-lookup"><span data-stu-id="4ab98-191">**Example: Service principal authentication**</span></span>
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

### <a name="user-credential-authentication"></a><span data-ttu-id="4ab98-192">Authentification des informations d’identification utilisateur</span><span class="sxs-lookup"><span data-stu-id="4ab98-192">User credential authentication</span></span>
<span data-ttu-id="4ab98-193">Ou bien, vous pouvez utiliser des toocopy de l’authentification des informations d’identification utilisateur à partir d’ou tooData Lake Store en spécifiant hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="4ab98-193">Alternatively, you can use user credential authentication toocopy from or tooData Lake Store by specifying hello following properties:</span></span>

| <span data-ttu-id="4ab98-194">Propriété</span><span class="sxs-lookup"><span data-stu-id="4ab98-194">Property</span></span> | <span data-ttu-id="4ab98-195">Description</span><span class="sxs-lookup"><span data-stu-id="4ab98-195">Description</span></span> | <span data-ttu-id="4ab98-196">Requis</span><span class="sxs-lookup"><span data-stu-id="4ab98-196">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="4ab98-197">**authorization**</span><span class="sxs-lookup"><span data-stu-id="4ab98-197">**authorization**</span></span> | <span data-ttu-id="4ab98-198">Cliquez sur hello **Authorize** bouton Bonjour éditeur Data Factory et entrez vos informations d’identification qui affecte le propriété toothis URL hello générées automatiquement d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="4ab98-198">Click hello **Authorize** button in hello Data Factory Editor and enter your credential that assigns hello autogenerated authorization URL toothis property.</span></span> | <span data-ttu-id="4ab98-199">Oui</span><span class="sxs-lookup"><span data-stu-id="4ab98-199">Yes</span></span> |
| <span data-ttu-id="4ab98-200">**sessionId**</span><span class="sxs-lookup"><span data-stu-id="4ab98-200">**sessionId**</span></span> | <span data-ttu-id="4ab98-201">ID de session OAuth à partir de la session de d’autorisation OAuth hello.</span><span class="sxs-lookup"><span data-stu-id="4ab98-201">OAuth session ID from hello OAuth authorization session.</span></span> <span data-ttu-id="4ab98-202">Chaque ID de session est unique et ne peut être utilisé qu’une seule fois.</span><span class="sxs-lookup"><span data-stu-id="4ab98-202">Each session ID is unique and can be used only once.</span></span> <span data-ttu-id="4ab98-203">Ce paramètre est automatiquement généré lorsque vous utilisez hello éditeur Data Factory.</span><span class="sxs-lookup"><span data-stu-id="4ab98-203">This setting is automatically generated when you use hello Data Factory Editor.</span></span> | <span data-ttu-id="4ab98-204">Oui</span><span class="sxs-lookup"><span data-stu-id="4ab98-204">Yes</span></span> |

<span data-ttu-id="4ab98-205">**Exemple : authentification des informations d’identification utilisateur**</span><span class="sxs-lookup"><span data-stu-id="4ab98-205">**Example: User credential authentication**</span></span>
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<session ID>",
            "authorization": "<authorization URL>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

#### <a name="token-expiration"></a><span data-ttu-id="4ab98-206">Expiration du jeton</span><span class="sxs-lookup"><span data-stu-id="4ab98-206">Token expiration</span></span>
<span data-ttu-id="4ab98-207">Hello code d’autorisation que vous avez généré à l’aide de hello **Authorize** bouton expire après un certain temps.</span><span class="sxs-lookup"><span data-stu-id="4ab98-207">hello authorization code that you generate by using hello **Authorize** button expires after a certain amount of time.</span></span> <span data-ttu-id="4ab98-208">Hello suivant message signifie que ce jeton d’authentification hello a expiré :</span><span class="sxs-lookup"><span data-stu-id="4ab98-208">hello following message means that hello authentication token has expired:</span></span>

<span data-ttu-id="4ab98-209">Credential operation error: invalid_grant - AADSTS70002: Error validating credentials.</span><span class="sxs-lookup"><span data-stu-id="4ab98-209">Credential operation error: invalid_grant - AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="4ab98-210">AADSTS70008 : hello fourni octroi d’accès est expiré ou révoqué.</span><span class="sxs-lookup"><span data-stu-id="4ab98-210">AADSTS70008: hello provided access grant is expired or revoked.</span></span> <span data-ttu-id="4ab98-211">Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21-09-31Z.</span><span class="sxs-lookup"><span data-stu-id="4ab98-211">Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21-09-31Z.</span></span>

<span data-ttu-id="4ab98-212">Hello tableau suivant montre des délais d’expiration hello de différents types de comptes d’utilisateur :</span><span class="sxs-lookup"><span data-stu-id="4ab98-212">hello following table shows hello expiration times of different types of user accounts:</span></span>


| <span data-ttu-id="4ab98-213">Type d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="4ab98-213">User type</span></span> | <span data-ttu-id="4ab98-214">Expire après</span><span class="sxs-lookup"><span data-stu-id="4ab98-214">Expires after</span></span> |
|:--- |:--- |
| <span data-ttu-id="4ab98-215">Comptes d’utilisateurs *non* gérés par Azure Active Directory (par exemple @hotmail.com ou @live.com)</span><span class="sxs-lookup"><span data-stu-id="4ab98-215">User accounts *not* managed by Azure Active Directory (for example, @hotmail.com or @live.com)</span></span> |<span data-ttu-id="4ab98-216">12 heures</span><span class="sxs-lookup"><span data-stu-id="4ab98-216">12 hours</span></span> |
| <span data-ttu-id="4ab98-217">Comptes d’utilisateurs gérés par Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4ab98-217">Users accounts managed by Azure Active Directory</span></span> |<span data-ttu-id="4ab98-218">exécution de 14 jours après la dernière tranche de hello</span><span class="sxs-lookup"><span data-stu-id="4ab98-218">14 days after hello last slice run</span></span> <br/><br/><span data-ttu-id="4ab98-219">90 jours, si une tranche basée sur un service lié OAuth est exécutée au moins une fois tous les 14 jours</span><span class="sxs-lookup"><span data-stu-id="4ab98-219">90 days, if a slice based on an OAuth-based linked service runs at least once every 14 days</span></span> |

<span data-ttu-id="4ab98-220">Si vous modifiez votre mot de passe avant l’heure d’expiration du jeton de hello, jeton de hello expire immédiatement.</span><span class="sxs-lookup"><span data-stu-id="4ab98-220">If you change your password before hello token expiration time, hello token expires immediately.</span></span> <span data-ttu-id="4ab98-221">Vous verrez un message de type hello mentionné plus haut dans cette section.</span><span class="sxs-lookup"><span data-stu-id="4ab98-221">You will see hello message mentioned earlier in this section.</span></span>

<span data-ttu-id="4ab98-222">Vous pouvez autoriser à nouveau le compte de hello à l’aide de hello **Authorize** bouton lors de l’expiration du jeton d’hello tooredeploy hello de service lié.</span><span class="sxs-lookup"><span data-stu-id="4ab98-222">You can reauthorize hello account by using hello **Authorize** button when hello token expires tooredeploy hello linked service.</span></span> <span data-ttu-id="4ab98-223">Vous pouvez également générer des valeurs pour hello **sessionId** et **autorisation** propriétés par programme à l’aide hello code suivant :</span><span class="sxs-lookup"><span data-stu-id="4ab98-223">You can also generate values for hello **sessionId** and **authorization** properties programmatically by using hello following code:</span></span>


```csharp
if (linkedService.Properties.TypeProperties is AzureDataLakeStoreLinkedService ||
    linkedService.Properties.TypeProperties is AzureDataLakeAnalyticsLinkedService)
{
    AuthorizationSessionGetResponse authorizationSession = this.Client.OAuth.Get(this.ResourceGroupName, this.DataFactoryName, linkedService.Properties.Type);

    WindowsFormsWebAuthenticationDialog authenticationDialog = new WindowsFormsWebAuthenticationDialog(null);
    string authorization = authenticationDialog.AuthenticateAAD(authorizationSession.AuthorizationSession.Endpoint, new Uri("urn:ietf:wg:oauth:2.0:oob"));

    AzureDataLakeStoreLinkedService azureDataLakeStoreProperties = linkedService.Properties.TypeProperties as AzureDataLakeStoreLinkedService;
    if (azureDataLakeStoreProperties != null)
    {
        azureDataLakeStoreProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeStoreProperties.Authorization = authorization;
    }

    AzureDataLakeAnalyticsLinkedService azureDataLakeAnalyticsProperties = linkedService.Properties.TypeProperties as AzureDataLakeAnalyticsLinkedService;
    if (azureDataLakeAnalyticsProperties != null)
    {
        azureDataLakeAnalyticsProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeAnalyticsProperties.Authorization = authorization;
    }
}
```
<span data-ttu-id="4ab98-224">Pour plus d’informations sur les classes de fabrique de données hello utilisées dans le code hello, consultez hello [AzureDataLakeStoreLinkedService classe](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService classe](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), et [ Classe de AuthorizationSessionGetResponse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) rubriques.</span><span class="sxs-lookup"><span data-stu-id="4ab98-224">For details about hello Data Factory classes used in hello code, see hello [AzureDataLakeStoreLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), and [AuthorizationSessionGetResponse Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) topics.</span></span> <span data-ttu-id="4ab98-225">Ajouter une référence tooversion `2.9.10826.1824` de `Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll` pour hello `WindowsFormsWebAuthenticationDialog` classe utilisée dans le code hello.</span><span class="sxs-lookup"><span data-stu-id="4ab98-225">Add a reference tooversion `2.9.10826.1824` of `Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll` for hello `WindowsFormsWebAuthenticationDialog` class used in hello code.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="4ab98-226">Propriétés du jeu de données</span><span class="sxs-lookup"><span data-stu-id="4ab98-226">Dataset properties</span></span>
<span data-ttu-id="4ab98-227">toospecify un toorepresent jeu de données d’entrée de données dans un magasin Data Lake Store, vous définissez hello **type** propriété du jeu de données hello trop**AzureDataLakeStore**.</span><span class="sxs-lookup"><span data-stu-id="4ab98-227">toospecify a dataset toorepresent input data in a Data Lake Store, you set hello **type** property of hello dataset too**AzureDataLakeStore**.</span></span> <span data-ttu-id="4ab98-228">Ensemble hello **linkedServiceName** service lié de propriété du nom de toohello hello dataset Hello Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4ab98-228">Set hello **linkedServiceName** property of hello dataset toohello name of hello Data Lake Store linked service.</span></span> <span data-ttu-id="4ab98-229">Pour obtenir une liste complète des sections JSON et les propriétés disponibles pour la définition de jeux de données, consultez hello [création de datasets](data-factory-create-datasets.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="4ab98-229">For a full list of JSON sections and properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="4ab98-230">Les sections d’un jeu de données en JSON, comme la **structure**, la **disponibilité** et la **stratégie** sont similaires pour tous les types de jeux de données (par exemple, Azure SQL Database, Azure Blob et Azure Table).</span><span class="sxs-lookup"><span data-stu-id="4ab98-230">Sections of a dataset in JSON, such as **structure**, **availability**, and **policy**, are similar for all dataset types (Azure SQL database, Azure blob, and Azure table, for example).</span></span> <span data-ttu-id="4ab98-231">Hello **typeProperties** section est différente pour chaque type de jeu de données et fournit des informations telles que l’emplacement et le format de données hello dans le magasin de données hello.</span><span class="sxs-lookup"><span data-stu-id="4ab98-231">hello **typeProperties** section is different for each type of dataset and provides information such as location and format of hello data in hello data store.</span></span> 

<span data-ttu-id="4ab98-232">Hello **typeProperties** section pour un jeu de données de type **AzureDataLakeStore** contient hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="4ab98-232">hello **typeProperties** section for a dataset of type **AzureDataLakeStore** contains hello following properties:</span></span>

| <span data-ttu-id="4ab98-233">Propriété</span><span class="sxs-lookup"><span data-stu-id="4ab98-233">Property</span></span> | <span data-ttu-id="4ab98-234">Description</span><span class="sxs-lookup"><span data-stu-id="4ab98-234">Description</span></span> | <span data-ttu-id="4ab98-235">Requis</span><span class="sxs-lookup"><span data-stu-id="4ab98-235">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="4ab98-236">**folderPath**</span><span class="sxs-lookup"><span data-stu-id="4ab98-236">**folderPath**</span></span> |<span data-ttu-id="4ab98-237">Conteneur toohello de chemin d’accès et le dossier de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4ab98-237">Path toohello container and folder in Data Lake Store.</span></span> |<span data-ttu-id="4ab98-238">Oui</span><span class="sxs-lookup"><span data-stu-id="4ab98-238">Yes</span></span> |
| <span data-ttu-id="4ab98-239">**fileName**</span><span class="sxs-lookup"><span data-stu-id="4ab98-239">**fileName**</span></span> |<span data-ttu-id="4ab98-240">Nom du fichier hello dans Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4ab98-240">Name of hello file in Azure Data Lake Store.</span></span> <span data-ttu-id="4ab98-241">Hello **nom de fichier** propriété est facultative et respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="4ab98-241">hello **fileName** property is optional and case-sensitive.</span></span> <br/><br/><span data-ttu-id="4ab98-242">Si vous spécifiez **nom de fichier**, activité hello (y compris la copie) fonctionne sur un fichier spécifique hello.</span><span class="sxs-lookup"><span data-stu-id="4ab98-242">If you specify **fileName**, hello activity (including Copy) works on hello specific file.</span></span><br/><br/><span data-ttu-id="4ab98-243">Lorsque **nom de fichier** n’est pas spécifié, copie inclut tous les fichiers dans **folderPath** hello de jeu de données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="4ab98-243">When **fileName** is not specified, Copy includes all files in **folderPath** in hello input dataset.</span></span><br/><br/><span data-ttu-id="4ab98-244">Lorsque **nom de fichier** n’est pas spécifié pour un dataset de sortie et **preserveHierarchy** n’est pas spécifié dans le récepteur d’activité, nom hello du fichier de hello généré est au format de hello données. _GUID_.txt ».</span><span class="sxs-lookup"><span data-stu-id="4ab98-244">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, hello name of hello generated file is in hello format Data._Guid_.txt\`.</span></span> <span data-ttu-id="4ab98-245">Par exemple : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.</span><span class="sxs-lookup"><span data-stu-id="4ab98-245">For example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.</span></span> |<span data-ttu-id="4ab98-246">Non</span><span class="sxs-lookup"><span data-stu-id="4ab98-246">No</span></span> |
| <span data-ttu-id="4ab98-247">**partitionedBy**</span><span class="sxs-lookup"><span data-stu-id="4ab98-247">**partitionedBy**</span></span> |<span data-ttu-id="4ab98-248">Hello **partitionedBy** propriété est facultative.</span><span class="sxs-lookup"><span data-stu-id="4ab98-248">hello **partitionedBy** property is optional.</span></span> <span data-ttu-id="4ab98-249">Vous pouvez l’utiliser toospecify un chemin d’accès dynamique et le nom de fichier de données de série chronologique.</span><span class="sxs-lookup"><span data-stu-id="4ab98-249">You can use it toospecify a dynamic path and file name for time-series data.</span></span> <span data-ttu-id="4ab98-250">Par exemple, **folderPath** peut être paramétré pour toutes les heures de données.</span><span class="sxs-lookup"><span data-stu-id="4ab98-250">For example, **folderPath** can be parameterized for every hour of data.</span></span> <span data-ttu-id="4ab98-251">Pour plus d’informations et d’exemples, consultez [hello partitionedBy propriété](#using-partitionedby-property).</span><span class="sxs-lookup"><span data-stu-id="4ab98-251">For details and examples, see [hello partitionedBy property](#using-partitionedby-property).</span></span> |<span data-ttu-id="4ab98-252">Non</span><span class="sxs-lookup"><span data-stu-id="4ab98-252">No</span></span> |
| <span data-ttu-id="4ab98-253">**format**</span><span class="sxs-lookup"><span data-stu-id="4ab98-253">**format**</span></span> | <span data-ttu-id="4ab98-254">Hello, les types de format suivants est pris en charge : **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, et  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="4ab98-254">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, and **ParquetFormat**.</span></span> <span data-ttu-id="4ab98-255">Ensemble hello **type** propriété sous **format** tooone de ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="4ab98-255">Set hello **type** property under **format** tooone of these values.</span></span> <span data-ttu-id="4ab98-256">Pour plus d’informations, consultez hello [au format texte](data-factory-supported-file-and-compression-formats.md#text-format), [format JSON](data-factory-supported-file-and-compression-formats.md#json-format), [le format Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [format ORC](data-factory-supported-file-and-compression-formats.md#orc-format), et [Parquet Format ](data-factory-supported-file-and-compression-formats.md#parquet-format) sections Bonjour [les formats de fichiers et de compression pris en charge par Azure Data Factory](data-factory-supported-file-and-compression-formats.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="4ab98-256">For more information, see hello [Text format](data-factory-supported-file-and-compression-formats.md#text-format), [JSON format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro format](data-factory-supported-file-and-compression-formats.md#avro-format), [ORC format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections in hello [File and compression formats supported by Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article.</span></span> <br><br> <span data-ttu-id="4ab98-257">Si vous souhaitez que les fichiers toocopy » en tant que-est « entre des magasins basée sur le fichier (copie binaire), ignorer hello `format` section dans les deux définitions de jeu de données d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="4ab98-257">If you want toocopy files "as-is" between file-based stores (binary copy), skip hello `format` section in both input and output dataset definitions.</span></span> |<span data-ttu-id="4ab98-258">Non</span><span class="sxs-lookup"><span data-stu-id="4ab98-258">No</span></span> |
| <span data-ttu-id="4ab98-259">**compression**</span><span class="sxs-lookup"><span data-stu-id="4ab98-259">**compression**</span></span> | <span data-ttu-id="4ab98-260">Spécifiez le type de hello et le niveau de compression pour les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="4ab98-260">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="4ab98-261">Les types pris en charge sont : **GZip**, **Deflate**, **BZip2** et **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="4ab98-261">Supported types are **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="4ab98-262">Les niveaux pris en charge sont **Optimal** et **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="4ab98-262">Supported levels are **Optimal** and **Fastest**.</span></span> <span data-ttu-id="4ab98-263">Pour plus d’informations, consultez [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="4ab98-263">For more information, see [File and compression formats supported by Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="4ab98-264">Non</span><span class="sxs-lookup"><span data-stu-id="4ab98-264">No</span></span> |

### <a name="hello-partitionedby-property"></a><span data-ttu-id="4ab98-265">propriété de partitionedBy Hello</span><span class="sxs-lookup"><span data-stu-id="4ab98-265">hello partitionedBy property</span></span>
<span data-ttu-id="4ab98-266">Vous pouvez spécifier dynamique **folderPath** et **nom de fichier** propriétés pour les données de série chronologique par hello **partitionedBy** propriété, les fonctions de la fabrique de données et système variables.</span><span class="sxs-lookup"><span data-stu-id="4ab98-266">You can specify dynamic **folderPath** and **fileName** properties for time-series data with hello **partitionedBy** property, Data Factory functions, and system variables.</span></span> <span data-ttu-id="4ab98-267">Pour plus d’informations, consultez hello [Azure Data Factory - fonctions et variables système](data-factory-functions-variables.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="4ab98-267">For details, see hello [Azure Data Factory - functions and system variables](data-factory-functions-variables.md) article.</span></span>


<span data-ttu-id="4ab98-268">Bonjour, l’exemple suivant `{Slice}` est remplacée par la valeur hello de variable de système de Data Factory hello `SliceStart` au format hello spécifié (`yyyyMMddHH`).</span><span class="sxs-lookup"><span data-stu-id="4ab98-268">In hello following example, `{Slice}` is replaced with hello value of hello Data Factory system variable `SliceStart` in hello format specified (`yyyyMMddHH`).</span></span> <span data-ttu-id="4ab98-269">nom de Hello `SliceStart` fait référence toohello heure de début de la tranche de hello.</span><span class="sxs-lookup"><span data-stu-id="4ab98-269">hello name `SliceStart` refers toohello start time of hello slice.</span></span> <span data-ttu-id="4ab98-270">Hello `folderPath` propriété est différente pour chaque secteur, comme dans `wikidatagateway/wikisampledataout/2014100103` ou `wikidatagateway/wikisampledataout/2014100104`.</span><span class="sxs-lookup"><span data-stu-id="4ab98-270">hello `folderPath` property is different for each slice, as in `wikidatagateway/wikisampledataout/2014100103` or `wikidatagateway/wikisampledataout/2014100104`.</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="4ab98-271">Bonjour suivant l’exemple, hello année, mois, jour et temps de `SliceStart` sont extraits dans des variables distinctes qui sont utilisés par hello `folderPath` et `fileName` propriétés :</span><span class="sxs-lookup"><span data-stu-id="4ab98-271">In hello following example, hello year, month, day, and time of `SliceStart` are extracted into separate variables that are used by hello `folderPath` and `fileName` properties:</span></span>
```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```
<span data-ttu-id="4ab98-272">Pour plus d’informations sur les jeux de données de série chronologique, en planifiant et en secteurs, consultez hello [jeux de données dans Azure Data Factory](data-factory-create-datasets.md) et [planification de la fabrique de données et l’exécution](data-factory-scheduling-and-execution.md) articles.</span><span class="sxs-lookup"><span data-stu-id="4ab98-272">For more details on time-series datasets, scheduling, and slices, see hello [Datasets in Azure Data Factory](data-factory-create-datasets.md) and [Data Factory scheduling and execution](data-factory-scheduling-and-execution.md) articles.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="4ab98-273">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="4ab98-273">Copy activity properties</span></span>
<span data-ttu-id="4ab98-274">Pour obtenir une liste complète des sections et les propriétés disponibles pour la définition d’activités, consultez hello [création de pipelines](data-factory-create-pipelines.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="4ab98-274">For a full list of sections and properties available for defining activities, see hello [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="4ab98-275">Les propriétés comme le nom, la description, les tables d’entrée et de sortie et la stratégie sont disponibles pour tous les types d’activités.</span><span class="sxs-lookup"><span data-stu-id="4ab98-275">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="4ab98-276">Hello propriétés disponibles dans hello **typeProperties** section d’une activité varient selon chaque type d’activité.</span><span class="sxs-lookup"><span data-stu-id="4ab98-276">hello properties available in hello **typeProperties** section of an activity vary with each activity type.</span></span> <span data-ttu-id="4ab98-277">Pour une activité de copie, ils varient selon les types de sources et récepteurs hello.</span><span class="sxs-lookup"><span data-stu-id="4ab98-277">For a copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="4ab98-278">**AzureDataLakeStoreSource** prend en charge hello suivant propriété Bonjour **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="4ab98-278">**AzureDataLakeStoreSource** supports hello following property in hello **typeProperties** section:</span></span>

| <span data-ttu-id="4ab98-279">Propriété</span><span class="sxs-lookup"><span data-stu-id="4ab98-279">Property</span></span> | <span data-ttu-id="4ab98-280">Description</span><span class="sxs-lookup"><span data-stu-id="4ab98-280">Description</span></span> | <span data-ttu-id="4ab98-281">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="4ab98-281">Allowed values</span></span> | <span data-ttu-id="4ab98-282">Requis</span><span class="sxs-lookup"><span data-stu-id="4ab98-282">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4ab98-283">**recursive**</span><span class="sxs-lookup"><span data-stu-id="4ab98-283">**recursive**</span></span> |<span data-ttu-id="4ab98-284">Indique si les données de salutation sont lu de manière récursive des sous-dossiers de hello ou uniquement à partir de dossier spécifié de hello.</span><span class="sxs-lookup"><span data-stu-id="4ab98-284">Indicates whether hello data is read recursively from hello subfolders or only from hello specified folder.</span></span> |<span data-ttu-id="4ab98-285">True (valeur par défaut), False</span><span class="sxs-lookup"><span data-stu-id="4ab98-285">True (default value), False</span></span> |<span data-ttu-id="4ab98-286">Non</span><span class="sxs-lookup"><span data-stu-id="4ab98-286">No</span></span> |


<span data-ttu-id="4ab98-287">**AzureDataLakeStoreSink** prend en charge hello propriétés Bonjour suivantes **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="4ab98-287">**AzureDataLakeStoreSink** supports hello following properties in hello **typeProperties** section:</span></span>

| <span data-ttu-id="4ab98-288">Propriété</span><span class="sxs-lookup"><span data-stu-id="4ab98-288">Property</span></span> | <span data-ttu-id="4ab98-289">Description</span><span class="sxs-lookup"><span data-stu-id="4ab98-289">Description</span></span> | <span data-ttu-id="4ab98-290">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="4ab98-290">Allowed values</span></span> | <span data-ttu-id="4ab98-291">Requis</span><span class="sxs-lookup"><span data-stu-id="4ab98-291">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4ab98-292">**copyBehavior**</span><span class="sxs-lookup"><span data-stu-id="4ab98-292">**copyBehavior**</span></span> |<span data-ttu-id="4ab98-293">Spécifie le comportement de copie hello.</span><span class="sxs-lookup"><span data-stu-id="4ab98-293">Specifies hello copy behavior.</span></span> |<span data-ttu-id="4ab98-294"><b>PreserveHierarchy</b>: préserve la hiérarchie des fichiers dans le dossier cible de hello hello.</span><span class="sxs-lookup"><span data-stu-id="4ab98-294"><b>PreserveHierarchy</b>: Preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="4ab98-295">chemin d’accès relatif de Hello du dossier source du fichier toosource est identique toohello un chemin d’accès relatif du dossier tootarget de fichier cible.</span><span class="sxs-lookup"><span data-stu-id="4ab98-295">hello relative path of source file toosource folder is identical toohello relative path of target file tootarget folder.</span></span><br/><br/><span data-ttu-id="4ab98-296"><b>FlattenHierarchy</b>: tous les fichiers à partir du dossier source hello sont créés dans hello premier niveau du dossier cible de hello.</span><span class="sxs-lookup"><span data-stu-id="4ab98-296"><b>FlattenHierarchy</b>: All files from hello source folder are created in hello first level of hello target folder.</span></span> <span data-ttu-id="4ab98-297">les fichiers cibles Hello sont créés avec des noms générés automatiquement.</span><span class="sxs-lookup"><span data-stu-id="4ab98-297">hello target files are created with autogenerated names.</span></span><br/><br/><span data-ttu-id="4ab98-298"><b>MergeFiles</b>: fusionne tous les fichiers à partir de fichiers de tooone du dossier source hello.</span><span class="sxs-lookup"><span data-stu-id="4ab98-298"><b>MergeFiles</b>: Merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="4ab98-299">Si hello nom de fichier ou un objet blob est spécifié, nom de fichier fusionné hello désigne hello spécifié.</span><span class="sxs-lookup"><span data-stu-id="4ab98-299">If hello file or blob name is specified, hello merged file name is hello specified name.</span></span> <span data-ttu-id="4ab98-300">Dans le cas contraire, le nom de fichier hello est généré automatiquement.</span><span class="sxs-lookup"><span data-stu-id="4ab98-300">Otherwise, hello file name is autogenerated.</span></span> |<span data-ttu-id="4ab98-301">Non</span><span class="sxs-lookup"><span data-stu-id="4ab98-301">No</span></span> |

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="4ab98-302">exemples de valeurs recursive et copyBehavior</span><span class="sxs-lookup"><span data-stu-id="4ab98-302">recursive and copyBehavior examples</span></span>
<span data-ttu-id="4ab98-303">Cette section décrit le comportement qui en résulte de hello d’opération de copie hello pour différentes combinaisons de valeurs récursive et copyBehavior.</span><span class="sxs-lookup"><span data-stu-id="4ab98-303">This section describes hello resulting behavior of hello Copy operation for different combinations of recursive and copyBehavior values.</span></span>

| <span data-ttu-id="4ab98-304">recursive</span><span class="sxs-lookup"><span data-stu-id="4ab98-304">recursive</span></span> | <span data-ttu-id="4ab98-305">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="4ab98-305">copyBehavior</span></span> | <span data-ttu-id="4ab98-306">Comportement résultant</span><span class="sxs-lookup"><span data-stu-id="4ab98-306">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4ab98-307">true</span><span class="sxs-lookup"><span data-stu-id="4ab98-307">true</span></span> |<span data-ttu-id="4ab98-308">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="4ab98-308">preserveHierarchy</span></span> |<span data-ttu-id="4ab98-309">Pour un dossier source Dossier1 avec hello suivant structure :</span><span class="sxs-lookup"><span data-stu-id="4ab98-309">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="4ab98-310">Dossier1</span><span class="sxs-lookup"><span data-stu-id="4ab98-310">Folder1</span></span><br/><span data-ttu-id="4ab98-311">&nbsp;&nbsp;&nbsp;&nbsp;Fichier1</span><span class="sxs-lookup"><span data-stu-id="4ab98-311">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="4ab98-312">&nbsp;&nbsp;&nbsp;&nbsp;Fichier2</span><span class="sxs-lookup"><span data-stu-id="4ab98-312">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="4ab98-313">&nbsp;&nbsp;&nbsp;&nbsp;Sousdossier1</span><span class="sxs-lookup"><span data-stu-id="4ab98-313">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="4ab98-314">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier3</span><span class="sxs-lookup"><span data-stu-id="4ab98-314">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="4ab98-315">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier4</span><span class="sxs-lookup"><span data-stu-id="4ab98-315">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="4ab98-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier5</span><span class="sxs-lookup"><span data-stu-id="4ab98-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="4ab98-317">dossier cible de Hello Dossier1 est créée avec hello même structure en tant que source de hello</span><span class="sxs-lookup"><span data-stu-id="4ab98-317">hello target folder Folder1 is created with hello same structure as hello source</span></span><br/><br/><span data-ttu-id="4ab98-318">Dossier1</span><span class="sxs-lookup"><span data-stu-id="4ab98-318">Folder1</span></span><br/><span data-ttu-id="4ab98-319">&nbsp;&nbsp;&nbsp;&nbsp;Fichier1</span><span class="sxs-lookup"><span data-stu-id="4ab98-319">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="4ab98-320">&nbsp;&nbsp;&nbsp;&nbsp;Fichier2</span><span class="sxs-lookup"><span data-stu-id="4ab98-320">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="4ab98-321">&nbsp;&nbsp;&nbsp;&nbsp;Sousdossier1</span><span class="sxs-lookup"><span data-stu-id="4ab98-321">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="4ab98-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier3</span><span class="sxs-lookup"><span data-stu-id="4ab98-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="4ab98-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier4</span><span class="sxs-lookup"><span data-stu-id="4ab98-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="4ab98-324">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier5.</span><span class="sxs-lookup"><span data-stu-id="4ab98-324">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span></span> |
| <span data-ttu-id="4ab98-325">true</span><span class="sxs-lookup"><span data-stu-id="4ab98-325">true</span></span> |<span data-ttu-id="4ab98-326">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="4ab98-326">flattenHierarchy</span></span> |<span data-ttu-id="4ab98-327">Pour un dossier source Dossier1 avec hello suivant structure :</span><span class="sxs-lookup"><span data-stu-id="4ab98-327">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="4ab98-328">Dossier1</span><span class="sxs-lookup"><span data-stu-id="4ab98-328">Folder1</span></span><br/><span data-ttu-id="4ab98-329">&nbsp;&nbsp;&nbsp;&nbsp;Fichier1</span><span class="sxs-lookup"><span data-stu-id="4ab98-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="4ab98-330">&nbsp;&nbsp;&nbsp;&nbsp;Fichier2</span><span class="sxs-lookup"><span data-stu-id="4ab98-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="4ab98-331">&nbsp;&nbsp;&nbsp;&nbsp;Sousdossier1</span><span class="sxs-lookup"><span data-stu-id="4ab98-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="4ab98-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier3</span><span class="sxs-lookup"><span data-stu-id="4ab98-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="4ab98-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier4</span><span class="sxs-lookup"><span data-stu-id="4ab98-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="4ab98-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier5</span><span class="sxs-lookup"><span data-stu-id="4ab98-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="4ab98-335">cible de Hello Dossier1 est créée avec hello suivant structure :</span><span class="sxs-lookup"><span data-stu-id="4ab98-335">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="4ab98-336">Dossier1</span><span class="sxs-lookup"><span data-stu-id="4ab98-336">Folder1</span></span><br/><span data-ttu-id="4ab98-337">&nbsp;&nbsp;&nbsp;&nbsp;nom généré automatiquement pour Fichier1</span><span class="sxs-lookup"><span data-stu-id="4ab98-337">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="4ab98-338">&nbsp;&nbsp;&nbsp;&nbsp;nom généré automatiquement pour Fichier2</span><span class="sxs-lookup"><span data-stu-id="4ab98-338">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="4ab98-339">&nbsp;&nbsp;&nbsp;&nbsp;nom généré automatiquement pour Fichier3</span><span class="sxs-lookup"><span data-stu-id="4ab98-339">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="4ab98-340">&nbsp;&nbsp;&nbsp;&nbsp;nom généré automatiquement pour Fichier4</span><span class="sxs-lookup"><span data-stu-id="4ab98-340">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="4ab98-341">&nbsp;&nbsp;&nbsp;&nbsp;nom généré automatiquement pour Fichier5</span><span class="sxs-lookup"><span data-stu-id="4ab98-341">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="4ab98-342">true</span><span class="sxs-lookup"><span data-stu-id="4ab98-342">true</span></span> |<span data-ttu-id="4ab98-343">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="4ab98-343">mergeFiles</span></span> |<span data-ttu-id="4ab98-344">Pour un dossier source Dossier1 avec hello suivant structure :</span><span class="sxs-lookup"><span data-stu-id="4ab98-344">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="4ab98-345">Dossier1</span><span class="sxs-lookup"><span data-stu-id="4ab98-345">Folder1</span></span><br/><span data-ttu-id="4ab98-346">&nbsp;&nbsp;&nbsp;&nbsp;Fichier1</span><span class="sxs-lookup"><span data-stu-id="4ab98-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="4ab98-347">&nbsp;&nbsp;&nbsp;&nbsp;Fichier2</span><span class="sxs-lookup"><span data-stu-id="4ab98-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="4ab98-348">&nbsp;&nbsp;&nbsp;&nbsp;Sousdossier1</span><span class="sxs-lookup"><span data-stu-id="4ab98-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="4ab98-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier3</span><span class="sxs-lookup"><span data-stu-id="4ab98-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="4ab98-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier4</span><span class="sxs-lookup"><span data-stu-id="4ab98-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="4ab98-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier5</span><span class="sxs-lookup"><span data-stu-id="4ab98-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="4ab98-352">cible de Hello Dossier1 est créée avec hello suivant structure :</span><span class="sxs-lookup"><span data-stu-id="4ab98-352">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="4ab98-353">Dossier1</span><span class="sxs-lookup"><span data-stu-id="4ab98-353">Folder1</span></span><br/><span data-ttu-id="4ab98-354">&nbsp;&nbsp;&nbsp;&nbsp;Le contenu de Fichier1 + Fichier2 + Fichier3 + Fichier4 + Fichier5 est fusionné dans un fichier avec le nom de fichier généré automatiquement</span><span class="sxs-lookup"><span data-stu-id="4ab98-354">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with auto-generated file name</span></span> |
| <span data-ttu-id="4ab98-355">false</span><span class="sxs-lookup"><span data-stu-id="4ab98-355">false</span></span> |<span data-ttu-id="4ab98-356">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="4ab98-356">preserveHierarchy</span></span> |<span data-ttu-id="4ab98-357">Pour un dossier source Dossier1 avec hello suivant structure :</span><span class="sxs-lookup"><span data-stu-id="4ab98-357">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="4ab98-358">Dossier1</span><span class="sxs-lookup"><span data-stu-id="4ab98-358">Folder1</span></span><br/><span data-ttu-id="4ab98-359">&nbsp;&nbsp;&nbsp;&nbsp;Fichier1</span><span class="sxs-lookup"><span data-stu-id="4ab98-359">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="4ab98-360">&nbsp;&nbsp;&nbsp;&nbsp;Fichier2</span><span class="sxs-lookup"><span data-stu-id="4ab98-360">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="4ab98-361">&nbsp;&nbsp;&nbsp;&nbsp;Sousdossier1</span><span class="sxs-lookup"><span data-stu-id="4ab98-361">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="4ab98-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier3</span><span class="sxs-lookup"><span data-stu-id="4ab98-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="4ab98-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier4</span><span class="sxs-lookup"><span data-stu-id="4ab98-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="4ab98-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier5</span><span class="sxs-lookup"><span data-stu-id="4ab98-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="4ab98-365">dossier cible de Hello Dossier1 est créée avec hello suivant de structure</span><span class="sxs-lookup"><span data-stu-id="4ab98-365">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="4ab98-366">Dossier1</span><span class="sxs-lookup"><span data-stu-id="4ab98-366">Folder1</span></span><br/><span data-ttu-id="4ab98-367">&nbsp;&nbsp;&nbsp;&nbsp;Fichier1</span><span class="sxs-lookup"><span data-stu-id="4ab98-367">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="4ab98-368">&nbsp;&nbsp;&nbsp;&nbsp;Fichier2</span><span class="sxs-lookup"><span data-stu-id="4ab98-368">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><br/><span data-ttu-id="4ab98-369">Sous-dossier1, où Fichier3, Fichier4 et Fichier5 ne sont pas sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="4ab98-369">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="4ab98-370">false</span><span class="sxs-lookup"><span data-stu-id="4ab98-370">false</span></span> |<span data-ttu-id="4ab98-371">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="4ab98-371">flattenHierarchy</span></span> |<span data-ttu-id="4ab98-372">Pour un dossier source Dossier1 avec hello suivant structure :</span><span class="sxs-lookup"><span data-stu-id="4ab98-372">For a source folder Folder1 with hello following structure:</span></span><br/><br/><span data-ttu-id="4ab98-373">Dossier1</span><span class="sxs-lookup"><span data-stu-id="4ab98-373">Folder1</span></span><br/><span data-ttu-id="4ab98-374">&nbsp;&nbsp;&nbsp;&nbsp;Fichier1</span><span class="sxs-lookup"><span data-stu-id="4ab98-374">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="4ab98-375">&nbsp;&nbsp;&nbsp;&nbsp;Fichier2</span><span class="sxs-lookup"><span data-stu-id="4ab98-375">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="4ab98-376">&nbsp;&nbsp;&nbsp;&nbsp;Sousdossier1</span><span class="sxs-lookup"><span data-stu-id="4ab98-376">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="4ab98-377">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier3</span><span class="sxs-lookup"><span data-stu-id="4ab98-377">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="4ab98-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier4</span><span class="sxs-lookup"><span data-stu-id="4ab98-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="4ab98-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier5</span><span class="sxs-lookup"><span data-stu-id="4ab98-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="4ab98-380">dossier cible de Hello Dossier1 est créée avec hello suivant de structure</span><span class="sxs-lookup"><span data-stu-id="4ab98-380">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="4ab98-381">Dossier1</span><span class="sxs-lookup"><span data-stu-id="4ab98-381">Folder1</span></span><br/><span data-ttu-id="4ab98-382">&nbsp;&nbsp;&nbsp;&nbsp;nom généré automatiquement pour Fichier1</span><span class="sxs-lookup"><span data-stu-id="4ab98-382">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="4ab98-383">&nbsp;&nbsp;&nbsp;&nbsp;nom généré automatiquement pour Fichier2</span><span class="sxs-lookup"><span data-stu-id="4ab98-383">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><br/><span data-ttu-id="4ab98-384">Sous-dossier1, où Fichier3, Fichier4 et Fichier5 ne sont pas sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="4ab98-384">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="4ab98-385">false</span><span class="sxs-lookup"><span data-stu-id="4ab98-385">false</span></span> |<span data-ttu-id="4ab98-386">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="4ab98-386">mergeFiles</span></span> |<span data-ttu-id="4ab98-387">Pour un dossier source Dossier1 avec hello suivant structure :</span><span class="sxs-lookup"><span data-stu-id="4ab98-387">For a source folder Folder1 with hello following structure:</span></span><br/><br/><span data-ttu-id="4ab98-388">Dossier1</span><span class="sxs-lookup"><span data-stu-id="4ab98-388">Folder1</span></span><br/><span data-ttu-id="4ab98-389">&nbsp;&nbsp;&nbsp;&nbsp;Fichier1</span><span class="sxs-lookup"><span data-stu-id="4ab98-389">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="4ab98-390">&nbsp;&nbsp;&nbsp;&nbsp;Fichier2</span><span class="sxs-lookup"><span data-stu-id="4ab98-390">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="4ab98-391">&nbsp;&nbsp;&nbsp;&nbsp;Sousdossier1</span><span class="sxs-lookup"><span data-stu-id="4ab98-391">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="4ab98-392">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier3</span><span class="sxs-lookup"><span data-stu-id="4ab98-392">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="4ab98-393">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier4</span><span class="sxs-lookup"><span data-stu-id="4ab98-393">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="4ab98-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier5</span><span class="sxs-lookup"><span data-stu-id="4ab98-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="4ab98-395">dossier cible de Hello Dossier1 est créée avec hello suivant de structure</span><span class="sxs-lookup"><span data-stu-id="4ab98-395">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="4ab98-396">Dossier1</span><span class="sxs-lookup"><span data-stu-id="4ab98-396">Folder1</span></span><br/><span data-ttu-id="4ab98-397">&nbsp;&nbsp;&nbsp;&nbsp;Le contenu de Fichier1 + Fichier2 est fusionné dans un fichier avec le nom de fichier généré automatiquement.</span><span class="sxs-lookup"><span data-stu-id="4ab98-397">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with auto-generated file name.</span></span> <span data-ttu-id="4ab98-398">nom généré automatiquement pour Fichier1</span><span class="sxs-lookup"><span data-stu-id="4ab98-398">auto-generated name for File1</span></span><br/><br/><span data-ttu-id="4ab98-399">Sous-dossier1, où Fichier3, Fichier4 et Fichier5 ne sont pas sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="4ab98-399">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="4ab98-400">Formats de fichier et de compression pris en charge</span><span class="sxs-lookup"><span data-stu-id="4ab98-400">Supported file and compression formats</span></span>
<span data-ttu-id="4ab98-401">Pour plus d’informations, consultez hello [des formats de fichiers et de compression dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="4ab98-401">For details, see hello [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article.</span></span>

## <a name="json-examples-for-copying-data-tooand-from-data-lake-store"></a><span data-ttu-id="4ab98-402">Exemples JSON pour la copie des données tooand Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4ab98-402">JSON examples for copying data tooand from Data Lake Store</span></span>
<span data-ttu-id="4ab98-403">Hello exemple suivant fournit des exemples de définitions de JSON.</span><span class="sxs-lookup"><span data-stu-id="4ab98-403">hello following examples provide sample JSON definitions.</span></span> <span data-ttu-id="4ab98-404">Vous pouvez utiliser ces toocreate de définitions exemple un pipeline à l’aide de hello [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="4ab98-404">You can use these sample definitions toocreate a pipeline by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="4ab98-405">Hello exemples montrent comment tooand de données toocopy à partir du stockage Data Lake Store et les objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="4ab98-405">hello examples show how toocopy data tooand from Data Lake Store and Azure Blob storage.</span></span> <span data-ttu-id="4ab98-406">Toutefois, les données peuvent être copiées _directement_ de n’importe quelle tooany de sources hello de récepteurs de hello pris en charge.</span><span class="sxs-lookup"><span data-stu-id="4ab98-406">However, data can be copied _directly_ from any of hello sources tooany of hello supported sinks.</span></span> <span data-ttu-id="4ab98-407">Pour plus d’informations, consultez la section hello « magasins de données pris en charge et formats » dans hello [déplacer des données à l’aide de l’activité de copie](data-factory-data-movement-activities.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="4ab98-407">For more information, see hello section "Supported data stores and formats" in hello [Move data by using Copy Activity](data-factory-data-movement-activities.md) article.</span></span>  

### <a name="example-copy-data-from-azure-blob-storage-tooazure-data-lake-store"></a><span data-ttu-id="4ab98-408">Exemple : Copier des données à partir de tooAzure de stockage d’objets Blob Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4ab98-408">Example: Copy data from Azure Blob Storage tooAzure Data Lake Store</span></span>
<span data-ttu-id="4ab98-409">exemple de code Hello dans cette section montre :</span><span class="sxs-lookup"><span data-stu-id="4ab98-409">hello example code in this section shows:</span></span>

* <span data-ttu-id="4ab98-410">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="4ab98-410">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="4ab98-411">Un service lié de type [AzureDataLakeStore](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="4ab98-411">A linked service of type [AzureDataLakeStore](#linked-service-properties).</span></span>
* <span data-ttu-id="4ab98-412">Un [jeu de données](data-factory-create-datasets.md) d'entrée de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="4ab98-412">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="4ab98-413">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureDataLakeStore](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="4ab98-413">An output [dataset](data-factory-create-datasets.md) of type [AzureDataLakeStore](#dataset-properties).</span></span>
* <span data-ttu-id="4ab98-414">Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) et [AzureDataLakeStoreSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="4ab98-414">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [AzureDataLakeStoreSink](#copy-activity-properties).</span></span>

<span data-ttu-id="4ab98-415">Hello exemples montrent comment série chronologique de données à partir du stockage d’objets Blob Azure sont copiés tooData Lake Store toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="4ab98-415">hello examples show how time-series data from Azure Blob Storage is copied tooData Lake Store every hour.</span></span> 

<span data-ttu-id="4ab98-416">**Service lié Azure Storage**</span><span class="sxs-lookup"><span data-stu-id="4ab98-416">**Azure Storage linked service**</span></span>

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

<span data-ttu-id="4ab98-417">**Service lié Azure Data Lake Store**</span><span class="sxs-lookup"><span data-stu-id="4ab98-417">**Azure Data Lake Store linked service**</span></span>

```JSON
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="4ab98-418">Pour plus d’informations, consultez hello [lié des propriétés du service](#linked-service-properties) section.</span><span class="sxs-lookup"><span data-stu-id="4ab98-418">For configuration details, see hello [Linked service properties](#linked-service-properties) section.</span></span>
>

<span data-ttu-id="4ab98-419">**Jeu de données d'entrée d'objet Blob Azure**</span><span class="sxs-lookup"><span data-stu-id="4ab98-419">**Azure blob input dataset**</span></span>

<span data-ttu-id="4ab98-420">Dans l’exemple suivant de hello, données sont récupérées à partir d’un nouvel objet blob toutes les heures (`"frequency": "Hour", "interval": 1`).</span><span class="sxs-lookup"><span data-stu-id="4ab98-420">In hello following example, data is picked up from a new blob every hour (`"frequency": "Hour", "interval": 1`).</span></span> <span data-ttu-id="4ab98-421">nom de chemin d’accès et de dossier pour l’objet blob de hello Hello sont dynamiquement évaluées en fonction de l’heure de début hello de tranche hello qui est en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="4ab98-421">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="4ab98-422">chemin d’accès du dossier Hello utilise hello year, month et composante jour d’heure de début hello.</span><span class="sxs-lookup"><span data-stu-id="4ab98-422">hello folder path uses hello year, month, and day portion of hello start time.</span></span> <span data-ttu-id="4ab98-423">nom de fichier Hello utilise heure hello heure de début de la partie de hello.</span><span class="sxs-lookup"><span data-stu-id="4ab98-423">hello file name uses hello hour portion of hello start time.</span></span> <span data-ttu-id="4ab98-424">Hello `"external": true` paramètre informe le service de fabrique de données hello cette table hello est la fabrique de données externe toohello et n’est pas générée par une activité dans la fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="4ab98-424">hello `"external": true` setting informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ]
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```

<span data-ttu-id="4ab98-425">**Jeu de données de sortie Azure Data Lake Store**</span><span class="sxs-lookup"><span data-stu-id="4ab98-425">**Azure Data Lake Store output dataset**</span></span>

<span data-ttu-id="4ab98-426">Hello suivant exemple copies données tooData Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4ab98-426">hello following example copies data tooData Lake Store.</span></span> <span data-ttu-id="4ab98-427">Les nouvelles données sont copiées tooData Lake Store toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="4ab98-427">New data is copied tooData Lake Store every hour.</span></span>

```JSON
{
    "name": "AzureDataLakeStoreOutput",
      "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/output/"
        },
        "availability": {
              "frequency": "Hour",
              "interval": 1
        }
      }
}
```


<span data-ttu-id="4ab98-428">**Activité de copie dans un pipeline avec une source Blob et un récepteur Data Lake Store**</span><span class="sxs-lookup"><span data-stu-id="4ab98-428">**Copy activity in a pipeline with a blob source and a Data Lake Store sink**</span></span>

<span data-ttu-id="4ab98-429">Dans l’exemple suivant de hello, pipeline de hello contient une activité de copie qui est configurée toouse hello des jeux de données d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="4ab98-429">In hello following example, hello pipeline contains a copy activity that is configured toouse hello input and output datasets.</span></span> <span data-ttu-id="4ab98-430">activité de copie Hello est toorun planifiée toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="4ab98-430">hello copy activity is scheduled toorun every hour.</span></span> <span data-ttu-id="4ab98-431">Dans la définition JSON du pipeline hello, hello `source` type est défini trop`BlobSource`et hello `sink` type est défini trop`AzureDataLakeStoreSink`.</span><span class="sxs-lookup"><span data-stu-id="4ab98-431">In hello pipeline JSON definition, hello `source` type is set too`BlobSource`, and hello `sink` type is set too`AzureDataLakeStoreSink`.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":
    {  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":
        [  
              {
                "name": "AzureBlobtoDataLake",
                "description": "Copy Activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureBlobInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureDataLakeStoreOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                      },
                      "sink": {
                        "type": "AzureDataLakeStoreSink"
                      }
                },
                   "scheduler": {
                      "frequency": "Hour",
                      "interval": 1
                },
                "policy": {
                      "concurrency": 1,
                      "executionPriorityOrder": "OldestFirst",
                      "retry": 0,
                      "timeout": "01:00:00"
                }
              }
        ]
    }
}
```

### <a name="example-copy-data-from-azure-data-lake-store-tooan-azure-blob"></a><span data-ttu-id="4ab98-432">Exemple : Copier des données à partir d’Azure Data Lake Store tooan objets blob Azure</span><span class="sxs-lookup"><span data-stu-id="4ab98-432">Example: Copy data from Azure Data Lake Store tooan Azure blob</span></span>
<span data-ttu-id="4ab98-433">exemple de code Hello dans cette section montre :</span><span class="sxs-lookup"><span data-stu-id="4ab98-433">hello example code in this section shows:</span></span>

* <span data-ttu-id="4ab98-434">Un service lié de type [AzureDataLakeStore](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="4ab98-434">A linked service of type [AzureDataLakeStore](#linked-service-properties).</span></span>
* <span data-ttu-id="4ab98-435">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="4ab98-435">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="4ab98-436">Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [AzureDataLakeStore](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="4ab98-436">An input [dataset](data-factory-create-datasets.md) of type [AzureDataLakeStore](#dataset-properties).</span></span>
* <span data-ttu-id="4ab98-437">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="4ab98-437">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="4ab98-438">Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [AzureDataLakeStoreSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="4ab98-438">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses [AzureDataLakeStoreSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="4ab98-439">code de Hello copie les données de série chronologique Data Lake Store tooan objets blob Azure toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="4ab98-439">hello code copies time-series data from Data Lake Store tooan Azure blob every hour.</span></span> 

<span data-ttu-id="4ab98-440">**Service lié Azure Data Lake Store**</span><span class="sxs-lookup"><span data-stu-id="4ab98-440">**Azure Data Lake Store linked service**</span></span>

```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>"
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="4ab98-441">Pour plus d’informations, consultez hello [lié des propriétés du service](#linked-service-properties) section.</span><span class="sxs-lookup"><span data-stu-id="4ab98-441">For configuration details, see hello [Linked service properties](#linked-service-properties) section.</span></span>
>

<span data-ttu-id="4ab98-442">**Service lié Azure Storage**</span><span class="sxs-lookup"><span data-stu-id="4ab98-442">**Azure Storage linked service**</span></span>

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="4ab98-443">**Jeu de données Azure Data Lake de sortie**</span><span class="sxs-lookup"><span data-stu-id="4ab98-443">**Azure Data Lake input dataset**</span></span>

<span data-ttu-id="4ab98-444">Dans cet exemple, le paramètre `"external"` trop`true` informe le service de fabrique de données hello cette table hello est la fabrique de données externe toohello et n’est pas générée par une activité dans la fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="4ab98-444">In this example, setting `"external"` too`true` informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
    "name": "AzureDataLakeStoreInput",
      "properties":
    {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            }
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
              "interval": 1
        },
        "policy": {
              "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
              }
        }
      }
}
```
<span data-ttu-id="4ab98-445">**Jeu de données de sortie d’objet Blob Azure**</span><span class="sxs-lookup"><span data-stu-id="4ab98-445">**Azure blob output dataset**</span></span>

<span data-ttu-id="4ab98-446">Bonjour l’exemple suivant, les données sont écrites tooa nouvel objet blob toutes les heures (`"frequency": "Hour", "interval": 1`).</span><span class="sxs-lookup"><span data-stu-id="4ab98-446">In hello following example, data is written tooa new blob every hour (`"frequency": "Hour", "interval": 1`).</span></span> <span data-ttu-id="4ab98-447">chemin d’accès du dossier Hello pour l’objet blob de hello est évaluée dynamiquement en fonction de l’heure de début hello de tranche hello qui est en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="4ab98-447">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="4ab98-448">chemin d’accès du dossier Hello utilise hello année, mois, jour et heures d’heure de début hello.</span><span class="sxs-lookup"><span data-stu-id="4ab98-448">hello folder path uses hello year, month, day, and hours portion of hello start time.</span></span>

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="4ab98-449">**Activité de copie dans un pipeline avec une source Azure Data Lake Store et un récepteur Blob**</span><span class="sxs-lookup"><span data-stu-id="4ab98-449">**A copy activity in a pipeline with an Azure Data Lake Store source and a blob sink**</span></span>

<span data-ttu-id="4ab98-450">Dans l’exemple suivant de hello, pipeline de hello contient une activité de copie qui est configurée toouse hello des jeux de données d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="4ab98-450">In hello following example, hello pipeline contains a copy activity that is configured toouse hello input and output datasets.</span></span> <span data-ttu-id="4ab98-451">activité de copie Hello est toorun planifiée toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="4ab98-451">hello copy activity is scheduled toorun every hour.</span></span> <span data-ttu-id="4ab98-452">Dans la définition JSON du pipeline hello, hello `source` type est défini trop`AzureDataLakeStoreSource`et hello `sink` type est défini trop`BlobSink`.</span><span class="sxs-lookup"><span data-stu-id="4ab98-452">In hello pipeline JSON definition, hello `source` type is set too`AzureDataLakeStoreSource`, and hello `sink` type is set too`BlobSink`.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
              {
                "name": "AzureDakeLaketoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureDataLakeStoreInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureBlobOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "AzureDataLakeStoreSource",
                      },
                      "sink": {
                        "type": "BlobSink"
                      }
                },
                   "scheduler": {
                      "frequency": "Hour",
                      "interval": 1
                },
                "policy": {
                      "concurrency": 1,
                      "executionPriorityOrder": "OldestFirst",
                      "retry": 0,
                      "timeout": "01:00:00"
                }
              }
         ]
    }
}
```

<span data-ttu-id="4ab98-453">Dans la définition d’activité hello copie, vous pouvez également mapper des colonnes de hello toocolumns de jeu de données source dans le jeu de données récepteur hello.</span><span class="sxs-lookup"><span data-stu-id="4ab98-453">In hello copy activity definition, you can also map columns from hello source dataset toocolumns in hello sink dataset.</span></span> <span data-ttu-id="4ab98-454">Pour plus d’informations, consultez [Mappage de colonnes de jeux de données dans Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="4ab98-454">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="4ab98-455">Performances et réglage</span><span class="sxs-lookup"><span data-stu-id="4ab98-455">Performance and tuning</span></span>
<span data-ttu-id="4ab98-456">toolearn sur les facteurs hello qui affectent les performances de l’activité de copie et la manière dont toooptimize, consultez hello [l’activité de copie guide des performances et paramétrage](data-factory-copy-activity-performance.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="4ab98-456">toolearn about hello factors that affect Copy Activity performance and how toooptimize it, see hello [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) article.</span></span>
