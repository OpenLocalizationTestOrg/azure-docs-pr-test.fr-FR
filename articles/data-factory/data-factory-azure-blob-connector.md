---
title: "données aaaCopy vers/depuis le stockage d’objets Blob Azure | Documents Microsoft"
description: "Découvrez comment toocopy blob des données dans Azure Data Factory. Utilisez notre exemple : comment tooand de données toocopy à partir de la base de données SQL Azure et de stockage d’objets Blob Azure."
keywords: "données d’objets blob, copie d’objet blob azure"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: bec8160f-5e07-47e4-8ee1-ebb14cfb805d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jingwang
ms.openlocfilehash: 8428c64e8e8b1084b3f2f680c4e1819559e4ffa3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooor-from-azure-blob-storage-using-azure-data-factory"></a><span data-ttu-id="d46a7-105">Tooor de données de copie à partir du stockage d’objets Blob Azure à l’aide d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d46a7-105">Copy data tooor from Azure Blob Storage using Azure Data Factory</span></span>
<span data-ttu-id="d46a7-106">Cet article explique comment toouse hello activité de copie dans Azure Data Factory toocopy données tooand à partir du stockage d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="d46a7-106">This article explains how toouse hello Copy Activity in Azure Data Factory toocopy data tooand from Azure Blob Storage.</span></span> <span data-ttu-id="d46a7-107">Il repose sur hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, qui présente une vue d’ensemble du déplacement des données avec l’activité de copie hello.</span><span class="sxs-lookup"><span data-stu-id="d46a7-107">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

## <a name="overview"></a><span data-ttu-id="d46a7-108">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="d46a7-108">Overview</span></span>
<span data-ttu-id="d46a7-109">Vous pouvez copier les données de toute source pris en charge de données tooAzure stockage d’objets Blob de stockage ou à partir des données de récepteur tooany pris en charge de stockage d’objets Blob Azure stockage.</span><span class="sxs-lookup"><span data-stu-id="d46a7-109">You can copy data from any supported source data store tooAzure Blob Storage or from Azure Blob Storage tooany supported sink data store.</span></span> <span data-ttu-id="d46a7-110">Hello tableau suivant fournit une liste des banques de données pris en charge en tant que sources ou récepteurs par l’activité de copie hello.</span><span class="sxs-lookup"><span data-stu-id="d46a7-110">hello following table provides a list of data stores supported as sources or sinks by hello copy activity.</span></span> <span data-ttu-id="d46a7-111">Par exemple, vous pouvez déplacer des données **depuis** une base de données SQL Server ou une base de données Azure SQL Database **vers** un stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="d46a7-111">For example, you can move data **from** a SQL Server database or an Azure SQL database **to** an Azure blob storage.</span></span> <span data-ttu-id="d46a7-112">Et vous pouvez copier des données **depuis** un stockage Blob Azure **vers** un entrepôt Azure SQL Data Warehouse ou une collection Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d46a7-112">And, you can copy data **from** Azure blob storage **to** an Azure SQL Data Warehouse or an Azure Cosmos DB collection.</span></span> 

## <a name="supported-scenarios"></a><span data-ttu-id="d46a7-113">Scénarios pris en charge</span><span class="sxs-lookup"><span data-stu-id="d46a7-113">Supported scenarios</span></span>
<span data-ttu-id="d46a7-114">Vous pouvez copier des données **à partir du stockage d’objets Blob Azure** toohello suivant des magasins de données :</span><span class="sxs-lookup"><span data-stu-id="d46a7-114">You can copy data **from Azure Blob Storage** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="d46a7-115">Vous pouvez copier des données à partir de hello suivant des magasins de données **tooAzure stockage d’objets Blob**:</span><span class="sxs-lookup"><span data-stu-id="d46a7-115">You can copy data from hello following data stores **tooAzure Blob Storage**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]
 
> [!IMPORTANT]
> <span data-ttu-id="d46a7-116">Activité de copie prend en charge la copie de données à partir de / tooboth le stockage Azure à usage général des comptes et à chaud/refroidir stockage d’objets Blob.</span><span class="sxs-lookup"><span data-stu-id="d46a7-116">Copy Activity supports copying data from/tooboth general-purpose Azure Storage accounts and Hot/Cool Blob storage.</span></span> <span data-ttu-id="d46a7-117">prend en charge de l’activité Hello **lors de la lecture à partir de blocs, ajouter ou objets BLOB de pages**, mais prend en charge **l’écriture d’objets BLOB de blocs tooonly**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-117">hello activity supports **reading from block, append, or page blobs**, but supports **writing tooonly block blobs**.</span></span> <span data-ttu-id="d46a7-118">Le stockage Azure Premium n’est pas pris en charge en tant que récepteur, car il repose sur des objets blob de pages.</span><span class="sxs-lookup"><span data-stu-id="d46a7-118">Azure Premium Storage is not supported as a sink because it is backed by page blobs.</span></span>
> 
> <span data-ttu-id="d46a7-119">Activité de copie ne supprime pas les données à partir de la source de hello après que hello données sont correctement copié toohello destination.</span><span class="sxs-lookup"><span data-stu-id="d46a7-119">Copy Activity does not delete data from hello source after hello data is successfully copied toohello destination.</span></span> <span data-ttu-id="d46a7-120">Si vous avez besoin de toodelete source de données après la copie a réussi, créer un [activité personnalisée](data-factory-use-custom-activities.md) toodelete hello des données et utiliser l’activité hello dans le pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="d46a7-120">If you need toodelete source data after a successful copy, create a [custom activity](data-factory-use-custom-activities.md) toodelete hello data and use hello activity in hello pipeline.</span></span> <span data-ttu-id="d46a7-121">Pour obtenir un exemple, consultez hello [exemple d’objet blob ou le dossier Delete sur GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity).</span><span class="sxs-lookup"><span data-stu-id="d46a7-121">For an example, see hello [Delete blob or folder sample on GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity).</span></span> 

## <a name="get-started"></a><span data-ttu-id="d46a7-122">Prise en main</span><span class="sxs-lookup"><span data-stu-id="d46a7-122">Get started</span></span>
<span data-ttu-id="d46a7-123">Vous pouvez créer un pipeline avec une activité de copie qui déplace les données vers/depuis un stockage blob Azure à l’aide de différents outils/API.</span><span class="sxs-lookup"><span data-stu-id="d46a7-123">You can create a pipeline with a copy activity that moves data to/from an Azure Blob Storage by using different tools/APIs.</span></span>

<span data-ttu-id="d46a7-124">toocreate de façon plus simple Hello un pipeline est toouse hello **Assistant copie de**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-124">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="d46a7-125">Cet article a une [procédure pas à pas](#walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage) pour la création d’un toocopy de données de pipeline à partir d’un tooanother d’emplacement de stockage d’objets Blob Azure emplacement de stockage d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="d46a7-125">This article has a [walkthrough](#walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage) for creating a pipeline toocopy data from an Azure Blob Storage location  tooanother Azure Blob Storage location.</span></span> <span data-ttu-id="d46a7-126">Pour obtenir un didacticiel sur la création d’un toocopy de données de pipeline à partir d’une base de données SQL de tooAzure stockage d’objets Blob Azure, consultez [didacticiel : créer un pipeline à l’aide d’Assistant copie de](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="d46a7-126">For a tutorial on creating a pipeline toocopy data from an Azure Blob Storage tooAzure SQL Database, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="d46a7-127">Vous pouvez également utiliser hello suivant outils toocreate un pipeline : **portail Azure**, **Visual Studio**, **Azure PowerShell**, **modèle Azure Resource Manager** , **API .NET**, et **API REST**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-127">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="d46a7-128">Consultez [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions toocreate un pipeline avec une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="d46a7-128">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="d46a7-129">Si vous utilisez hello ou une API, vous effectuez hello suivant les étapes toocreate un pipeline qui déplace la banque de données récepteur tooa du magasin de données à partir des données d’une source :</span><span class="sxs-lookup"><span data-stu-id="d46a7-129">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="d46a7-130">Création d'une **fabrique de données**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-130">Create a **data factory**.</span></span> <span data-ttu-id="d46a7-131">Une fabrique de données peut contenir un ou plusieurs pipelines.</span><span class="sxs-lookup"><span data-stu-id="d46a7-131">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="d46a7-132">Créer **services liés** fabrique de données tooyour toolink les données d’entrée et de sortie magasins.</span><span class="sxs-lookup"><span data-stu-id="d46a7-132">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="d46a7-133">Par exemple, si vous copiez des données à partir d’une base de données SQL Azure de tooan stockage blob Azure, vous créez deux services liés toolink votre compte de stockage et de la fabrique de données de tooyour de base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="d46a7-133">For example, if you are copying data from an Azure blob storage tooan Azure SQL database, you create two linked services toolink your Azure storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="d46a7-134">Pour les propriétés de service lié qui sont spécifique tooAzure stockage d’objets Blob, consultez [lié des propriétés du service](#linked-service-properties) section.</span><span class="sxs-lookup"><span data-stu-id="d46a7-134">For linked service properties that are specific tooAzure Blob Storage, see [linked service properties](#linked-service-properties) section.</span></span> 
2. <span data-ttu-id="d46a7-135">Créer **datasets** toorepresent d’entrée et sortie l’opération de copie des données pour hello.</span><span class="sxs-lookup"><span data-stu-id="d46a7-135">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="d46a7-136">Exemple hello mentionné dans la dernière étape de hello, vous permet de créer un conteneur d’objets blob de jeu de données toospecify hello et un dossier qui contient les données d’entrée hello.</span><span class="sxs-lookup"><span data-stu-id="d46a7-136">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="d46a7-137">De plus, vous créez une autre table SQL hello toospecify jeu de données dans la base de données SQL Azure hello qui contient les données hello copiées à partir du stockage d’objets blob hello.</span><span class="sxs-lookup"><span data-stu-id="d46a7-137">And, you create another dataset toospecify hello SQL table in hello Azure SQL database that holds hello data copied from hello blob storage.</span></span> <span data-ttu-id="d46a7-138">Pour les propriétés du dataset qui sont spécifique tooAzure stockage d’objets Blob, consultez [propriétés du dataset](#dataset-properties) section.</span><span class="sxs-lookup"><span data-stu-id="d46a7-138">For dataset properties that are specific tooAzure Blob Storage, see [dataset properties](#dataset-properties) section.</span></span>
3. <span data-ttu-id="d46a7-139">Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="d46a7-139">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="d46a7-140">Dans l’exemple hello mentionné précédemment, vous utilisez BlobSource en tant que source et SqlSink comme un récepteur pour l’activité de copie hello.</span><span class="sxs-lookup"><span data-stu-id="d46a7-140">In hello example mentioned earlier, you use BlobSource as a source and SqlSink as a sink for hello copy activity.</span></span> <span data-ttu-id="d46a7-141">De même, si vous copiez à partir de la base de données SQL Azure tooAzure stockage d’objets Blob, vous utilisez SqlSource et BlobSink dans l’activité de copie hello.</span><span class="sxs-lookup"><span data-stu-id="d46a7-141">Similarly, if you are copying from Azure SQL Database tooAzure Blob Storage, you use SqlSource and BlobSink in hello copy activity.</span></span> <span data-ttu-id="d46a7-142">Pour les propriétés d’activité de copie sont spécifique tooAzure stockage d’objets Blob, consultez [copier les propriétés de l’activité](#copy-activity-properties) section.</span><span class="sxs-lookup"><span data-stu-id="d46a7-142">For copy activity properties that are specific tooAzure Blob Storage, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="d46a7-143">Pour plus d’informations sur comment toouse du magasin de données source ou un récepteur, cliquez sur le lien hello dans la section précédente de hello pour votre magasin de données.</span><span class="sxs-lookup"><span data-stu-id="d46a7-143">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>  

<span data-ttu-id="d46a7-144">Lorsque vous utilisez hello Assistant, les définitions de JSON pour ces entités de fabrique de données (services liés, des datasets et pipeline de hello) sont créées automatiquement pour vous.</span><span class="sxs-lookup"><span data-stu-id="d46a7-144">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="d46a7-145">Lorsque vous utilisez/API des outils (à l’exception des API .NET), vous définissez ces entités de fabrique de données à l’aide du format JSON de hello.</span><span class="sxs-lookup"><span data-stu-id="d46a7-145">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="d46a7-146">Pour plus d’exemples de définitions de JSON pour les entités de fabrique de données qui sont utilisées toocopy des données vers/depuis un stockage d’objets Blob Azure, consultez [exemples JSON](#json-examples-for-copying-data-to-and-from-blob-storage  ) section de cet article.</span><span class="sxs-lookup"><span data-stu-id="d46a7-146">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an Azure Blob Storage, see [JSON examples](#json-examples-for-copying-data-to-and-from-blob-storage  ) section of this article.</span></span>

<span data-ttu-id="d46a7-147">Hello les sections suivantes fournit des détails sur les propriétés JSON qui sont utilisés toodefine Data Factory entités spécifique tooAzure stockage d’objets Blob.</span><span class="sxs-lookup"><span data-stu-id="d46a7-147">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAzure Blob Storage.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="d46a7-148">Propriétés du service lié</span><span class="sxs-lookup"><span data-stu-id="d46a7-148">Linked service properties</span></span>
<span data-ttu-id="d46a7-149">Il existe deux types de services liés, vous pouvez utiliser toolink une fabrique de données Azure tooan le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="d46a7-149">There are two types of linked services you can use toolink an Azure Storage tooan Azure data factory.</span></span> <span data-ttu-id="d46a7-150">Il s’agit des services liés **AzureStorage** et **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-150">They are: **AzureStorage** linked service and **AzureStorageSas** linked service.</span></span> <span data-ttu-id="d46a7-151">Hello service lié Azure Storage fournit la fabrique de données hello avec accès global toohello le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="d46a7-151">hello Azure Storage linked service provides hello data factory with global access toohello Azure Storage.</span></span> <span data-ttu-id="d46a7-152">Alors que hello Azure stockage SAS (Shared Access Signature) lié service fournit fabrique de données hello avec l’accès restreint/temps toohello le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="d46a7-152">Whereas, hello Azure Storage SAS (Shared Access Signature) linked service provides hello data factory with restricted/time-bound access toohello Azure Storage.</span></span> <span data-ttu-id="d46a7-153">Il n'existe aucune différence entre ces deux services liés.</span><span class="sxs-lookup"><span data-stu-id="d46a7-153">There are no other differences between these two linked services.</span></span> <span data-ttu-id="d46a7-154">Sélectionnez service hello lié qui correspond le mieux à vos besoins.</span><span class="sxs-lookup"><span data-stu-id="d46a7-154">Choose hello linked service that suits your needs.</span></span> <span data-ttu-id="d46a7-155">Hello sections suivantes fournissent plus d’informations sur ces deux services liés.</span><span class="sxs-lookup"><span data-stu-id="d46a7-155">hello following sections provide more details on these two linked services.</span></span>

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a><span data-ttu-id="d46a7-156">Propriétés du jeu de données</span><span class="sxs-lookup"><span data-stu-id="d46a7-156">Dataset properties</span></span>
<span data-ttu-id="d46a7-157">toospecify un toorepresent de jeu de données d’entrée ou de sortie des données dans un stockage d’objets Blob Azure, que vous définissez propriété hello du jeu de données hello : **AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-157">toospecify a dataset toorepresent input or output data in an Azure Blob Storage, you set hello type property of hello dataset to: **AzureBlob**.</span></span> <span data-ttu-id="d46a7-158">Ensemble hello **linkedServiceName** service lié de propriété du nom de toohello hello dataset Hello le stockage Azure ou SAS de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="d46a7-158">Set hello **linkedServiceName** property of hello dataset toohello name of hello Azure Storage or Azure Storage SAS linked service.</span></span>  <span data-ttu-id="d46a7-159">propriétés de type Hello du jeu de données hello spécifient hello **conteneur d’objets blob** et hello **dossier** dans le stockage blob hello.</span><span class="sxs-lookup"><span data-stu-id="d46a7-159">hello type properties of hello dataset specify hello **blob container** and hello **folder** in hello blob storage.</span></span>

<span data-ttu-id="d46a7-160">Pour obtenir une liste complète des sections JSON et les propriétés disponibles pour définir des jeux de données, consultez hello [création de datasets](data-factory-create-datasets.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="d46a7-160">For a full list of JSON sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="d46a7-161">Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données (SQL Azure, Azure Blob, Azure Table, etc.).</span><span class="sxs-lookup"><span data-stu-id="d46a7-161">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="d46a7-162">Fabrique de données prend en charge hello conforme CLS .NET en fonction des valeurs de type qui fournit des informations de type dans « structure » pour les sources de données de schéma-sur-lecture comme objets blob Azure suivantes : Int16, Int32, Int64, Single, Double, Decimal, Byte [], Bool, String, Guid, Datetime, DateTimeOffset, Timespan.</span><span class="sxs-lookup"><span data-stu-id="d46a7-162">Data factory supports hello following CLS-compliant .NET based type values for providing type information in “structure” for schema-on-read data sources like Azure blob: Int16, Int32, Int64, Single, Double, Decimal, Byte[], Bool, String, Guid, Datetime, Datetimeoffset, Timespan.</span></span> <span data-ttu-id="d46a7-163">Fabrique de données effectue automatiquement les conversions de type lors du déplacement du magasin de données récepteur tooa du magasin de données à partir des données sources.</span><span class="sxs-lookup"><span data-stu-id="d46a7-163">Data Factory automatically performs type conversions when moving data from a source data store tooa sink data store.</span></span>

<span data-ttu-id="d46a7-164">Hello **typeProperties** section est différente pour chaque type de jeu de données et fournit des informations à propos de l’emplacement de hello, format, etc., de données hello dans le magasin de données hello.</span><span class="sxs-lookup"><span data-stu-id="d46a7-164">hello **typeProperties** section is different for each type of dataset and provides information about hello location, format etc., of hello data in hello data store.</span></span> <span data-ttu-id="d46a7-165">jeu de données de type Hello typeProperties section **AzureBlob** dataset a hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="d46a7-165">hello typeProperties section for dataset of type **AzureBlob** dataset has hello following properties:</span></span>

| <span data-ttu-id="d46a7-166">Propriété</span><span class="sxs-lookup"><span data-stu-id="d46a7-166">Property</span></span> | <span data-ttu-id="d46a7-167">Description</span><span class="sxs-lookup"><span data-stu-id="d46a7-167">Description</span></span> | <span data-ttu-id="d46a7-168">Requis</span><span class="sxs-lookup"><span data-stu-id="d46a7-168">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d46a7-169">folderPath</span><span class="sxs-lookup"><span data-stu-id="d46a7-169">folderPath</span></span> |<span data-ttu-id="d46a7-170">Conteneur toohello de chemin d’accès et le dossier de stockage d’objets blob hello.</span><span class="sxs-lookup"><span data-stu-id="d46a7-170">Path toohello container and folder in hello blob storage.</span></span> <span data-ttu-id="d46a7-171">Exemple : monconteneurblob\mondossierblob\\</span><span class="sxs-lookup"><span data-stu-id="d46a7-171">Example: myblobcontainer\myblobfolder\\</span></span> |<span data-ttu-id="d46a7-172">Oui</span><span class="sxs-lookup"><span data-stu-id="d46a7-172">Yes</span></span> |
| <span data-ttu-id="d46a7-173">fileName</span><span class="sxs-lookup"><span data-stu-id="d46a7-173">fileName</span></span> |<span data-ttu-id="d46a7-174">Nom de l’objet blob de hello.</span><span class="sxs-lookup"><span data-stu-id="d46a7-174">Name of hello blob.</span></span> <span data-ttu-id="d46a7-175">fileName est facultatif et sensible à la casse.</span><span class="sxs-lookup"><span data-stu-id="d46a7-175">fileName is optional and case-sensitive.</span></span><br/><br/><span data-ttu-id="d46a7-176">Si vous spécifiez un nom de fichier, le hello activité (y compris la copie) fonctionne sur hello Blob spécifique.</span><span class="sxs-lookup"><span data-stu-id="d46a7-176">If you specify a filename, hello activity (including Copy) works on hello specific Blob.</span></span><br/><br/><span data-ttu-id="d46a7-177">Lorsque le nom de fichier n’est pas spécifié, copie inclut tous les objets BLOB dans folderPath hello pour le jeu de données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="d46a7-177">When fileName is not specified, Copy includes all Blobs in hello folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="d46a7-178">Lorsque **nom de fichier** n’est pas spécifié pour un dataset de sortie et **preserveHierarchy** n’est pas spécifié dans le récepteur d’activité, nom hello du fichier de hello généré serait Bonjour sous ce format : données.<Guid>. txt (par exemple : : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="d46a7-178">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, hello name of hello generated file would be in hello following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="d46a7-179">Non</span><span class="sxs-lookup"><span data-stu-id="d46a7-179">No</span></span> |
| <span data-ttu-id="d46a7-180">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="d46a7-180">partitionedBy</span></span> |<span data-ttu-id="d46a7-181">partitionedBy est une propriété facultative.</span><span class="sxs-lookup"><span data-stu-id="d46a7-181">partitionedBy is an optional property.</span></span> <span data-ttu-id="d46a7-182">Vous pouvez utiliser il toospecify un folderPath dynamique et le nom de fichier de données de série chronologique.</span><span class="sxs-lookup"><span data-stu-id="d46a7-182">You can use it toospecify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="d46a7-183">Par exemple, folderPath peut être paramétré pour toutes les heures de données.</span><span class="sxs-lookup"><span data-stu-id="d46a7-183">For example, folderPath can be parameterized for every hour of data.</span></span> <span data-ttu-id="d46a7-184">Consultez hello [à l’aide de la section de propriété partitionedBy](#using-partitionedBy-property) pour plus d’informations et des exemples.</span><span class="sxs-lookup"><span data-stu-id="d46a7-184">See hello [Using partitionedBy property section](#using-partitionedBy-property) for details and examples.</span></span> |<span data-ttu-id="d46a7-185">Non</span><span class="sxs-lookup"><span data-stu-id="d46a7-185">No</span></span> |
| <span data-ttu-id="d46a7-186">format</span><span class="sxs-lookup"><span data-stu-id="d46a7-186">format</span></span> | <span data-ttu-id="d46a7-187">Hello, les types de format suivants est pris en charge : **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-187">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="d46a7-188">Ensemble hello **type** propriété sous tooone de format de ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="d46a7-188">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="d46a7-189">Pour en savoir plus, consultez les sections relatives à [format Text](data-factory-supported-file-and-compression-formats.md#text-format), [format Json](data-factory-supported-file-and-compression-formats.md#json-format), [format Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [format Orc](data-factory-supported-file-and-compression-formats.md#orc-format) et [format Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="d46a7-189">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="d46a7-190">Si vous souhaitez trop**copier les fichiers en tant que-est** entre des magasins basée sur le fichier (copie binaire), ignorer la section de format hello dans les deux définitions de jeu de données d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="d46a7-190">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="d46a7-191">Non</span><span class="sxs-lookup"><span data-stu-id="d46a7-191">No</span></span> |
| <span data-ttu-id="d46a7-192">compression</span><span class="sxs-lookup"><span data-stu-id="d46a7-192">compression</span></span> | <span data-ttu-id="d46a7-193">Spécifiez le type de hello et le niveau de compression pour les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="d46a7-193">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="d46a7-194">Les types pris en charge sont : **GZip**, **Deflate**, **BZip2** et **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-194">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="d46a7-195">Les niveaux pris en charge sont **Optimal** et **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-195">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="d46a7-196">Pour plus d’informations, consultez [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="d46a7-196">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="d46a7-197">Non</span><span class="sxs-lookup"><span data-stu-id="d46a7-197">No</span></span> |

### <a name="using-partitionedby-property"></a><span data-ttu-id="d46a7-198">Utilisation de la propriété partitionedBy</span><span class="sxs-lookup"><span data-stu-id="d46a7-198">Using partitionedBy property</span></span>
<span data-ttu-id="d46a7-199">Comme indiqué dans la section précédente de hello, vous pouvez spécifier un folderPath dynamique et le nom de fichier de données de série chronologique par hello **partitionedBy** propriété, [fonctions de la fabrique de données et les variables système hello](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="d46a7-199">As mentioned in hello previous section, you can specify a dynamic folderPath and filename for time series data with hello **partitionedBy** property, [Data Factory functions, and hello system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="d46a7-200">Pour obtenir plus d’informations sur les jeux de données de série chronologique, la planification et les segments, consultez les articles [Création de jeux de données](data-factory-create-datasets.md) et [Planification et exécution](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="d46a7-200">For more information on time series datasets, scheduling, and slices, see [Creating Datasets](data-factory-create-datasets.md) and [Scheduling & Execution](data-factory-scheduling-and-execution.md) articles.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="d46a7-201">Exemple 1</span><span class="sxs-lookup"><span data-stu-id="d46a7-201">Sample 1</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="d46a7-202">Dans cet exemple, {Slice} est remplacé par la valeur hello de fabrique de données variable système SliceStart au format (AAAAMMJJHH) de la hello spécifiée.</span><span class="sxs-lookup"><span data-stu-id="d46a7-202">In this example, {Slice} is replaced with hello value of Data Factory system variable SliceStart in hello format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="d46a7-203">Hello SliceStart fait référence à des temps de toostart de tranche de hello.</span><span class="sxs-lookup"><span data-stu-id="d46a7-203">hello SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="d46a7-204">Hello folderPath est différent pour chaque secteur.</span><span class="sxs-lookup"><span data-stu-id="d46a7-204">hello folderPath is different for each slice.</span></span> <span data-ttu-id="d46a7-205">Par exemple : wikidatagateway/wikisampledataout/2014100103 ou wikidatagateway/wikisampledataout/2014100104.</span><span class="sxs-lookup"><span data-stu-id="d46a7-205">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104</span></span>

#### <a name="sample-2"></a><span data-ttu-id="d46a7-206">Exemple 2</span><span class="sxs-lookup"><span data-stu-id="d46a7-206">Sample 2</span></span>

```json
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

<span data-ttu-id="d46a7-207">Dans cet exemple, l'année, le mois, le jour et l'heure de SliceStart sont extraits dans des variables distinctes qui sont utilisées par les propriétés folderPath et fileName.</span><span class="sxs-lookup"><span data-stu-id="d46a7-207">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="d46a7-208">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="d46a7-208">Copy activity properties</span></span>
<span data-ttu-id="d46a7-209">Pour obtenir une liste complète des sections et les propriétés disponibles pour la définition d’activités, consultez hello [création de Pipelines](data-factory-create-pipelines.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="d46a7-209">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="d46a7-210">Les propriétés comme le nom, la description, les jeux de données d’entrée et de sortie et les stratégies sont disponibles pour tous les types d’activités.</span><span class="sxs-lookup"><span data-stu-id="d46a7-210">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span> <span data-ttu-id="d46a7-211">Tandis que les propriétés disponibles dans hello **typeProperties** section d’activité hello varient selon chaque type d’activité.</span><span class="sxs-lookup"><span data-stu-id="d46a7-211">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="d46a7-212">Pour l’activité de copie, ils varient selon les types de sources et récepteurs hello.</span><span class="sxs-lookup"><span data-stu-id="d46a7-212">For Copy activity, they vary depending on hello types of sources and sinks.</span></span> <span data-ttu-id="d46a7-213">Si vous déplacez des données à partir d’un stockage d’objets Blob Azure, vous définissez type de source de hello dans l’activité de copie hello trop**BlobSource**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-213">If you are moving data from an Azure Blob Storage, you set hello source type in hello copy activity too**BlobSource**.</span></span> <span data-ttu-id="d46a7-214">De même, si vous déplacez des données tooan stockage d’objets Blob Azure, vous définir le type de récepteur hello dans l’activité de copie hello trop**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-214">Similarly, if you are moving data tooan Azure Blob Storage, you set hello sink type in hello copy activity too**BlobSink**.</span></span> <span data-ttu-id="d46a7-215">Cette section fournit une liste de propriétés prises en charge par BlobSource et BlobSink.</span><span class="sxs-lookup"><span data-stu-id="d46a7-215">This section provides a list of properties supported by BlobSource and BlobSink.</span></span>

<span data-ttu-id="d46a7-216">**BlobSource** prend en charge hello propriétés Bonjour suivantes **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="d46a7-216">**BlobSource** supports hello following properties in hello **typeProperties** section:</span></span>

| <span data-ttu-id="d46a7-217">Propriété</span><span class="sxs-lookup"><span data-stu-id="d46a7-217">Property</span></span> | <span data-ttu-id="d46a7-218">Description</span><span class="sxs-lookup"><span data-stu-id="d46a7-218">Description</span></span> | <span data-ttu-id="d46a7-219">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="d46a7-219">Allowed values</span></span> | <span data-ttu-id="d46a7-220">Requis</span><span class="sxs-lookup"><span data-stu-id="d46a7-220">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d46a7-221">recursive</span><span class="sxs-lookup"><span data-stu-id="d46a7-221">recursive</span></span> |<span data-ttu-id="d46a7-222">Indique si les données de salutation sont lu de manière récursive à partir de dossiers de sub hello ou uniquement à partir de dossier spécifié de hello.</span><span class="sxs-lookup"><span data-stu-id="d46a7-222">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="d46a7-223">True (valeur par défaut), False</span><span class="sxs-lookup"><span data-stu-id="d46a7-223">True (default value), False</span></span> |<span data-ttu-id="d46a7-224">Non</span><span class="sxs-lookup"><span data-stu-id="d46a7-224">No</span></span> |

<span data-ttu-id="d46a7-225">**BlobSink** prend en charge les propriétés suivantes de hello **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="d46a7-225">**BlobSink** supports hello following properties **typeProperties** section:</span></span>

| <span data-ttu-id="d46a7-226">Propriété</span><span class="sxs-lookup"><span data-stu-id="d46a7-226">Property</span></span> | <span data-ttu-id="d46a7-227">Description</span><span class="sxs-lookup"><span data-stu-id="d46a7-227">Description</span></span> | <span data-ttu-id="d46a7-228">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="d46a7-228">Allowed values</span></span> | <span data-ttu-id="d46a7-229">Requis</span><span class="sxs-lookup"><span data-stu-id="d46a7-229">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d46a7-230">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="d46a7-230">copyBehavior</span></span> |<span data-ttu-id="d46a7-231">Définit le comportement de copie de hello lors de la source de hello est BlobSource ou système de fichiers.</span><span class="sxs-lookup"><span data-stu-id="d46a7-231">Defines hello copy behavior when hello source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="d46a7-232"><b>PreserveHierarchy</b>: préserve hello hiérarchie de fichiers dans le dossier cible de hello.</span><span class="sxs-lookup"><span data-stu-id="d46a7-232"><b>PreserveHierarchy</b>: preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="d46a7-233">chemin d’accès relatif de Hello du dossier source du fichier toosource est identique toohello un chemin d’accès relatif du dossier tootarget de fichier cible.</span><span class="sxs-lookup"><span data-stu-id="d46a7-233">hello relative path of source file toosource folder is identical toohello relative path of target file tootarget folder.</span></span><br/><br/><span data-ttu-id="d46a7-234"><b>FlattenHierarchy</b>: tous les fichiers à partir du dossier source hello sont Bonjour tout d’abord au niveau du dossier cible.</span><span class="sxs-lookup"><span data-stu-id="d46a7-234"><b>FlattenHierarchy</b>: all files from hello source folder are in hello first level of target folder.</span></span> <span data-ttu-id="d46a7-235">les fichiers cibles Hello ont un nom généré automatiquement.</span><span class="sxs-lookup"><span data-stu-id="d46a7-235">hello target files have auto generated name.</span></span> <br/><br/><span data-ttu-id="d46a7-236"><b>MergeFiles</b>: fusionne tous les fichiers à partir de fichiers de tooone du dossier source hello.</span><span class="sxs-lookup"><span data-stu-id="d46a7-236"><b>MergeFiles</b>: merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="d46a7-237">Si hello nom de fichier/objet Blob est spécifié, le nom de fichier fusionné hello serait nom spécifié de hello ; dans le cas contraire, serait de nom de fichier généré automatiquement.</span><span class="sxs-lookup"><span data-stu-id="d46a7-237">If hello File/Blob Name is specified, hello merged file name would be hello specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="d46a7-238">Non</span><span class="sxs-lookup"><span data-stu-id="d46a7-238">No</span></span> |

<span data-ttu-id="d46a7-239">**BlobSource** prend également en charge ces deux propriétés pour la compatibilité descendante.</span><span class="sxs-lookup"><span data-stu-id="d46a7-239">**BlobSource** also supports these two properties for backward compatibility.</span></span>

* <span data-ttu-id="d46a7-240">**treatEmptyAsNull**: Spécifie si tootreat null ou une chaîne vide en tant que valeur null.</span><span class="sxs-lookup"><span data-stu-id="d46a7-240">**treatEmptyAsNull**: Specifies whether tootreat null or empty string as null value.</span></span>
* <span data-ttu-id="d46a7-241">**skipHeaderLineCount** : spécifie le nombre de lignes à ignorer.</span><span class="sxs-lookup"><span data-stu-id="d46a7-241">**skipHeaderLineCount** - Specifies how many lines need be skipped.</span></span> <span data-ttu-id="d46a7-242">Applicable uniquement quand le jeu de données d’entrée utilise TextFormat.</span><span class="sxs-lookup"><span data-stu-id="d46a7-242">It is applicable only when input dataset is using TextFormat.</span></span>

<span data-ttu-id="d46a7-243">De même, **BlobSink** prend en charge hello suivant de propriété pour la compatibilité descendante.</span><span class="sxs-lookup"><span data-stu-id="d46a7-243">Similarly, **BlobSink** supports hello following property for backward compatibility.</span></span>

* <span data-ttu-id="d46a7-244">**blobWriterAddHeader**: Spécifie si le jeu de données de sortie tooadd un en-tête de définitions de colonne lors de l’écriture de tooan.</span><span class="sxs-lookup"><span data-stu-id="d46a7-244">**blobWriterAddHeader**: Specifies whether tooadd a header of column definitions while writing tooan output dataset.</span></span>

<span data-ttu-id="d46a7-245">Hello de prise en charge de jeux de données maintenant les propriétés qui implémentent suivantes hello même fonctionnalité : **treatEmptyAsNull**, **skipLineCount**, **firstRowAsHeader**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-245">Datasets now support hello following properties that implement hello same functionality: **treatEmptyAsNull**, **skipLineCount**, **firstRowAsHeader**.</span></span>

<span data-ttu-id="d46a7-246">Hello tableau suivant fournit des conseils sur l’utilisation des propriétés du nouveau dataset hello à la place de ces propriétés de source/récepteur blob.</span><span class="sxs-lookup"><span data-stu-id="d46a7-246">hello following table provides guidance on using hello new dataset properties in place of these blob source/sink properties.</span></span>

| <span data-ttu-id="d46a7-247">Propriété de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="d46a7-247">Copy Activity property</span></span> | <span data-ttu-id="d46a7-248">Propriété du jeu de données</span><span class="sxs-lookup"><span data-stu-id="d46a7-248">Dataset property</span></span> |
|:--- |:--- |
| <span data-ttu-id="d46a7-249">skipHeaderLineCount sur BlobSource</span><span class="sxs-lookup"><span data-stu-id="d46a7-249">skipHeaderLineCount on BlobSource</span></span> |<span data-ttu-id="d46a7-250">skipLineCount et firstRowAsHeader.</span><span class="sxs-lookup"><span data-stu-id="d46a7-250">skipLineCount and firstRowAsHeader.</span></span> <span data-ttu-id="d46a7-251">Les lignes sont ignorées tout d’abord, et puis première ligne de hello est lu comme un en-tête.</span><span class="sxs-lookup"><span data-stu-id="d46a7-251">Lines are skipped first and then hello first row is read as a header.</span></span> |
| <span data-ttu-id="d46a7-252">treatEmptyAsNull sur BlobSource</span><span class="sxs-lookup"><span data-stu-id="d46a7-252">treatEmptyAsNull on BlobSource</span></span> |<span data-ttu-id="d46a7-253">treatEmptyAsNull sur le jeu de données d’entrée</span><span class="sxs-lookup"><span data-stu-id="d46a7-253">treatEmptyAsNull on input dataset</span></span> |
| <span data-ttu-id="d46a7-254">blobWriterAddHeader sur BlobSink</span><span class="sxs-lookup"><span data-stu-id="d46a7-254">blobWriterAddHeader on BlobSink</span></span> |<span data-ttu-id="d46a7-255">firstRowAsHeader sur le jeu de données de sortie</span><span class="sxs-lookup"><span data-stu-id="d46a7-255">firstRowAsHeader on output dataset</span></span> |

<span data-ttu-id="d46a7-256">Consultez la section [Définition de TextFormat](data-factory-supported-file-and-compression-formats.md#text-format) pour plus d’informations sur ces propriétés.</span><span class="sxs-lookup"><span data-stu-id="d46a7-256">See [Specifying TextFormat](data-factory-supported-file-and-compression-formats.md#text-format) section for detailed information on these properties.</span></span>    

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="d46a7-257">exemples de valeurs recursive et copyBehavior</span><span class="sxs-lookup"><span data-stu-id="d46a7-257">recursive and copyBehavior examples</span></span>
<span data-ttu-id="d46a7-258">Cette section décrit le comportement qui en résulte de hello d’opération de copie hello pour différentes combinaisons de valeurs récursive et copyBehavior.</span><span class="sxs-lookup"><span data-stu-id="d46a7-258">This section describes hello resulting behavior of hello Copy operation for different combinations of recursive and copyBehavior values.</span></span>

| <span data-ttu-id="d46a7-259">recursive</span><span class="sxs-lookup"><span data-stu-id="d46a7-259">recursive</span></span> | <span data-ttu-id="d46a7-260">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="d46a7-260">copyBehavior</span></span> | <span data-ttu-id="d46a7-261">Comportement résultant</span><span class="sxs-lookup"><span data-stu-id="d46a7-261">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d46a7-262">true</span><span class="sxs-lookup"><span data-stu-id="d46a7-262">true</span></span> |<span data-ttu-id="d46a7-263">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="d46a7-263">preserveHierarchy</span></span> |<span data-ttu-id="d46a7-264">Pour un dossier source Dossier1 avec hello suivant structure :</span><span class="sxs-lookup"><span data-stu-id="d46a7-264">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="d46a7-265">Dossier1</span><span class="sxs-lookup"><span data-stu-id="d46a7-265">Folder1</span></span><br/><span data-ttu-id="d46a7-266">&nbsp;&nbsp;&nbsp;&nbsp;Fichier1</span><span class="sxs-lookup"><span data-stu-id="d46a7-266">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="d46a7-267">&nbsp;&nbsp;&nbsp;&nbsp;Fichier2</span><span class="sxs-lookup"><span data-stu-id="d46a7-267">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="d46a7-268">&nbsp;&nbsp;&nbsp;&nbsp;Sousdossier1</span><span class="sxs-lookup"><span data-stu-id="d46a7-268">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="d46a7-269">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier3</span><span class="sxs-lookup"><span data-stu-id="d46a7-269">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="d46a7-270">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier4</span><span class="sxs-lookup"><span data-stu-id="d46a7-270">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="d46a7-271">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier5</span><span class="sxs-lookup"><span data-stu-id="d46a7-271">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="d46a7-272">dossier cible de Hello Dossier1 est créée avec hello même structure en tant que source de hello</span><span class="sxs-lookup"><span data-stu-id="d46a7-272">hello target folder Folder1 is created with hello same structure as hello source</span></span><br/><br/><span data-ttu-id="d46a7-273">Dossier1</span><span class="sxs-lookup"><span data-stu-id="d46a7-273">Folder1</span></span><br/><span data-ttu-id="d46a7-274">&nbsp;&nbsp;&nbsp;&nbsp;Fichier1</span><span class="sxs-lookup"><span data-stu-id="d46a7-274">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="d46a7-275">&nbsp;&nbsp;&nbsp;&nbsp;Fichier2</span><span class="sxs-lookup"><span data-stu-id="d46a7-275">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="d46a7-276">&nbsp;&nbsp;&nbsp;&nbsp;Sousdossier1</span><span class="sxs-lookup"><span data-stu-id="d46a7-276">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="d46a7-277">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier3</span><span class="sxs-lookup"><span data-stu-id="d46a7-277">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="d46a7-278">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier4</span><span class="sxs-lookup"><span data-stu-id="d46a7-278">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="d46a7-279">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier5.</span><span class="sxs-lookup"><span data-stu-id="d46a7-279">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span></span> |
| <span data-ttu-id="d46a7-280">true</span><span class="sxs-lookup"><span data-stu-id="d46a7-280">true</span></span> |<span data-ttu-id="d46a7-281">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="d46a7-281">flattenHierarchy</span></span> |<span data-ttu-id="d46a7-282">Pour un dossier source Dossier1 avec hello suivant structure :</span><span class="sxs-lookup"><span data-stu-id="d46a7-282">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="d46a7-283">Dossier1</span><span class="sxs-lookup"><span data-stu-id="d46a7-283">Folder1</span></span><br/><span data-ttu-id="d46a7-284">&nbsp;&nbsp;&nbsp;&nbsp;Fichier1</span><span class="sxs-lookup"><span data-stu-id="d46a7-284">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="d46a7-285">&nbsp;&nbsp;&nbsp;&nbsp;Fichier2</span><span class="sxs-lookup"><span data-stu-id="d46a7-285">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="d46a7-286">&nbsp;&nbsp;&nbsp;&nbsp;Sousdossier1</span><span class="sxs-lookup"><span data-stu-id="d46a7-286">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="d46a7-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier3</span><span class="sxs-lookup"><span data-stu-id="d46a7-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="d46a7-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier4</span><span class="sxs-lookup"><span data-stu-id="d46a7-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="d46a7-289">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier5</span><span class="sxs-lookup"><span data-stu-id="d46a7-289">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="d46a7-290">cible de Hello Dossier1 est créée avec hello suivant structure :</span><span class="sxs-lookup"><span data-stu-id="d46a7-290">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="d46a7-291">Dossier1</span><span class="sxs-lookup"><span data-stu-id="d46a7-291">Folder1</span></span><br/><span data-ttu-id="d46a7-292">&nbsp;&nbsp;&nbsp;&nbsp;nom généré automatiquement pour Fichier1</span><span class="sxs-lookup"><span data-stu-id="d46a7-292">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="d46a7-293">&nbsp;&nbsp;&nbsp;&nbsp;nom généré automatiquement pour Fichier2</span><span class="sxs-lookup"><span data-stu-id="d46a7-293">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="d46a7-294">&nbsp;&nbsp;&nbsp;&nbsp;nom généré automatiquement pour Fichier3</span><span class="sxs-lookup"><span data-stu-id="d46a7-294">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="d46a7-295">&nbsp;&nbsp;&nbsp;&nbsp;nom généré automatiquement pour Fichier4</span><span class="sxs-lookup"><span data-stu-id="d46a7-295">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="d46a7-296">&nbsp;&nbsp;&nbsp;&nbsp;nom généré automatiquement pour Fichier5</span><span class="sxs-lookup"><span data-stu-id="d46a7-296">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="d46a7-297">true</span><span class="sxs-lookup"><span data-stu-id="d46a7-297">true</span></span> |<span data-ttu-id="d46a7-298">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="d46a7-298">mergeFiles</span></span> |<span data-ttu-id="d46a7-299">Pour un dossier source Dossier1 avec hello suivant structure :</span><span class="sxs-lookup"><span data-stu-id="d46a7-299">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="d46a7-300">Dossier1</span><span class="sxs-lookup"><span data-stu-id="d46a7-300">Folder1</span></span><br/><span data-ttu-id="d46a7-301">&nbsp;&nbsp;&nbsp;&nbsp;Fichier1</span><span class="sxs-lookup"><span data-stu-id="d46a7-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="d46a7-302">&nbsp;&nbsp;&nbsp;&nbsp;Fichier2</span><span class="sxs-lookup"><span data-stu-id="d46a7-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="d46a7-303">&nbsp;&nbsp;&nbsp;&nbsp;Sousdossier1</span><span class="sxs-lookup"><span data-stu-id="d46a7-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="d46a7-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier3</span><span class="sxs-lookup"><span data-stu-id="d46a7-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="d46a7-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier4</span><span class="sxs-lookup"><span data-stu-id="d46a7-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="d46a7-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier5</span><span class="sxs-lookup"><span data-stu-id="d46a7-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="d46a7-307">cible de Hello Dossier1 est créée avec hello suivant structure :</span><span class="sxs-lookup"><span data-stu-id="d46a7-307">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="d46a7-308">Dossier1</span><span class="sxs-lookup"><span data-stu-id="d46a7-308">Folder1</span></span><br/><span data-ttu-id="d46a7-309">&nbsp;&nbsp;&nbsp;&nbsp;Le contenu de Fichier1 + Fichier2 + Fichier3 + Fichier4 + Fichier5 est fusionné dans un fichier avec le nom de fichier généré automatiquement</span><span class="sxs-lookup"><span data-stu-id="d46a7-309">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with auto-generated file name</span></span> |
| <span data-ttu-id="d46a7-310">false</span><span class="sxs-lookup"><span data-stu-id="d46a7-310">false</span></span> |<span data-ttu-id="d46a7-311">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="d46a7-311">preserveHierarchy</span></span> |<span data-ttu-id="d46a7-312">Pour un dossier source Dossier1 avec hello suivant structure :</span><span class="sxs-lookup"><span data-stu-id="d46a7-312">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="d46a7-313">Dossier1</span><span class="sxs-lookup"><span data-stu-id="d46a7-313">Folder1</span></span><br/><span data-ttu-id="d46a7-314">&nbsp;&nbsp;&nbsp;&nbsp;Fichier1</span><span class="sxs-lookup"><span data-stu-id="d46a7-314">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="d46a7-315">&nbsp;&nbsp;&nbsp;&nbsp;Fichier2</span><span class="sxs-lookup"><span data-stu-id="d46a7-315">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="d46a7-316">&nbsp;&nbsp;&nbsp;&nbsp;Sousdossier1</span><span class="sxs-lookup"><span data-stu-id="d46a7-316">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="d46a7-317">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier3</span><span class="sxs-lookup"><span data-stu-id="d46a7-317">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="d46a7-318">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier4</span><span class="sxs-lookup"><span data-stu-id="d46a7-318">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="d46a7-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier5</span><span class="sxs-lookup"><span data-stu-id="d46a7-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="d46a7-320">dossier cible de Hello Dossier1 est créée avec hello suivant de structure</span><span class="sxs-lookup"><span data-stu-id="d46a7-320">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="d46a7-321">Dossier1</span><span class="sxs-lookup"><span data-stu-id="d46a7-321">Folder1</span></span><br/><span data-ttu-id="d46a7-322">&nbsp;&nbsp;&nbsp;&nbsp;Fichier1</span><span class="sxs-lookup"><span data-stu-id="d46a7-322">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="d46a7-323">&nbsp;&nbsp;&nbsp;&nbsp;Fichier2</span><span class="sxs-lookup"><span data-stu-id="d46a7-323">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><br/><span data-ttu-id="d46a7-324">Sous-dossier1, où Fichier3, Fichier4 et Fichier5 ne sont pas sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="d46a7-324">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="d46a7-325">false</span><span class="sxs-lookup"><span data-stu-id="d46a7-325">false</span></span> |<span data-ttu-id="d46a7-326">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="d46a7-326">flattenHierarchy</span></span> |<span data-ttu-id="d46a7-327">Pour un dossier source Dossier1 avec hello suivant structure :</span><span class="sxs-lookup"><span data-stu-id="d46a7-327">For a source folder Folder1 with hello following structure:</span></span><br/><br/><span data-ttu-id="d46a7-328">Dossier1</span><span class="sxs-lookup"><span data-stu-id="d46a7-328">Folder1</span></span><br/><span data-ttu-id="d46a7-329">&nbsp;&nbsp;&nbsp;&nbsp;Fichier1</span><span class="sxs-lookup"><span data-stu-id="d46a7-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="d46a7-330">&nbsp;&nbsp;&nbsp;&nbsp;Fichier2</span><span class="sxs-lookup"><span data-stu-id="d46a7-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="d46a7-331">&nbsp;&nbsp;&nbsp;&nbsp;Sousdossier1</span><span class="sxs-lookup"><span data-stu-id="d46a7-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="d46a7-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier3</span><span class="sxs-lookup"><span data-stu-id="d46a7-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="d46a7-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier4</span><span class="sxs-lookup"><span data-stu-id="d46a7-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="d46a7-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier5</span><span class="sxs-lookup"><span data-stu-id="d46a7-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="d46a7-335">dossier cible de Hello Dossier1 est créée avec hello suivant de structure</span><span class="sxs-lookup"><span data-stu-id="d46a7-335">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="d46a7-336">Dossier1</span><span class="sxs-lookup"><span data-stu-id="d46a7-336">Folder1</span></span><br/><span data-ttu-id="d46a7-337">&nbsp;&nbsp;&nbsp;&nbsp;nom généré automatiquement pour Fichier1</span><span class="sxs-lookup"><span data-stu-id="d46a7-337">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="d46a7-338">&nbsp;&nbsp;&nbsp;&nbsp;nom généré automatiquement pour Fichier2</span><span class="sxs-lookup"><span data-stu-id="d46a7-338">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><br/><span data-ttu-id="d46a7-339">Sous-dossier1, où Fichier3, Fichier4 et Fichier5 ne sont pas sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="d46a7-339">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="d46a7-340">false</span><span class="sxs-lookup"><span data-stu-id="d46a7-340">false</span></span> |<span data-ttu-id="d46a7-341">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="d46a7-341">mergeFiles</span></span> |<span data-ttu-id="d46a7-342">Pour un dossier source Dossier1 avec hello suivant structure :</span><span class="sxs-lookup"><span data-stu-id="d46a7-342">For a source folder Folder1 with hello following structure:</span></span><br/><br/><span data-ttu-id="d46a7-343">Dossier1</span><span class="sxs-lookup"><span data-stu-id="d46a7-343">Folder1</span></span><br/><span data-ttu-id="d46a7-344">&nbsp;&nbsp;&nbsp;&nbsp;Fichier1</span><span class="sxs-lookup"><span data-stu-id="d46a7-344">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="d46a7-345">&nbsp;&nbsp;&nbsp;&nbsp;Fichier2</span><span class="sxs-lookup"><span data-stu-id="d46a7-345">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="d46a7-346">&nbsp;&nbsp;&nbsp;&nbsp;Sousdossier1</span><span class="sxs-lookup"><span data-stu-id="d46a7-346">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="d46a7-347">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier3</span><span class="sxs-lookup"><span data-stu-id="d46a7-347">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="d46a7-348">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier4</span><span class="sxs-lookup"><span data-stu-id="d46a7-348">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="d46a7-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier5</span><span class="sxs-lookup"><span data-stu-id="d46a7-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="d46a7-350">dossier cible de Hello Dossier1 est créée avec hello suivant de structure</span><span class="sxs-lookup"><span data-stu-id="d46a7-350">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="d46a7-351">Dossier1</span><span class="sxs-lookup"><span data-stu-id="d46a7-351">Folder1</span></span><br/><span data-ttu-id="d46a7-352">&nbsp;&nbsp;&nbsp;&nbsp;Le contenu de Fichier1 + Fichier2 est fusionné dans un fichier avec le nom de fichier généré automatiquement.</span><span class="sxs-lookup"><span data-stu-id="d46a7-352">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with auto-generated file name.</span></span> <span data-ttu-id="d46a7-353">nom généré automatiquement pour Fichier1</span><span class="sxs-lookup"><span data-stu-id="d46a7-353">auto-generated name for File1</span></span><br/><br/><span data-ttu-id="d46a7-354">Sous-dossier1, où Fichier3, Fichier4 et Fichier5 ne sont pas sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="d46a7-354">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |

## <a name="walkthrough-use-copy-wizard-toocopy-data-tofrom-blob-storage"></a><span data-ttu-id="d46a7-355">Procédure pas à pas : Des données de toocopy d’utiliser l’Assistant copie vers/depuis le stockage d’objets Blob</span><span class="sxs-lookup"><span data-stu-id="d46a7-355">Walkthrough: Use Copy Wizard toocopy data to/from Blob Storage</span></span>
<span data-ttu-id="d46a7-356">Examinons à présent comment tooquickly copier des données à partir de Azure stockage d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="d46a7-356">Let's look at how tooquickly copy data to/from an Azure blob storage.</span></span> <span data-ttu-id="d46a7-357">Dans cette procédure pas à pas, les banques de données source et de destination sont du type stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="d46a7-357">In this walkthrough, both source and destination data stores of type: Azure Blob Storage.</span></span> <span data-ttu-id="d46a7-358">Hello pipeline dans cette procédure copie les données à partir d’un dossier de tooanother Bonjour même conteneur d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="d46a7-358">hello pipeline in this walkthrough copies data from a folder tooanother folder in hello same blob container.</span></span> <span data-ttu-id="d46a7-359">Cette procédure pas à pas est volontairement simple tooshow paramètres ou des propriétés lors de l’utilisation du stockage d’objets Blob comme source ou récepteur.</span><span class="sxs-lookup"><span data-stu-id="d46a7-359">This walkthrough is intentionally simple tooshow you settings or properties when using Blob Storage as a source or sink.</span></span> 

### <a name="prerequisites"></a><span data-ttu-id="d46a7-360">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d46a7-360">Prerequisites</span></span>
1. <span data-ttu-id="d46a7-361">Créez un **compte de stockage Azure** à usage général si vous n’en avez pas encore un.</span><span class="sxs-lookup"><span data-stu-id="d46a7-361">Create a general-purpose **Azure Storage Account** if you don't have one already.</span></span> <span data-ttu-id="d46a7-362">Vous utilisez le stockage d’objets blob hello à la fois comme **source** et **destination** stocker des données dans cette procédure pas à pas.</span><span class="sxs-lookup"><span data-stu-id="d46a7-362">You use hello blob storage as both **source** and **destination** data store in this walkthrough.</span></span> <span data-ttu-id="d46a7-363">Si vous n’avez pas un compte de stockage Azure, consultez hello [créer un compte de stockage](../storage/common/storage-create-storage-account.md#create-a-storage-account) toocreate suit un article.</span><span class="sxs-lookup"><span data-stu-id="d46a7-363">if you don't have an Azure storage account, see hello [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps toocreate one.</span></span>
2. <span data-ttu-id="d46a7-364">Créer un conteneur d’objets blob nommé **adfblobconnector** hello compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="d46a7-364">Create a blob container named **adfblobconnector** in hello storage account.</span></span> 
4. <span data-ttu-id="d46a7-365">Créez un dossier nommé **d’entrée** Bonjour **adfblobconnector** conteneur.</span><span class="sxs-lookup"><span data-stu-id="d46a7-365">Create a folder named **input** in hello **adfblobconnector** container.</span></span>
5. <span data-ttu-id="d46a7-366">Créez un fichier nommé **emp.txt** avec hello suivant de contenu et le télécharger toohello **d’entrée** dossier à l’aide des outils tels que [Explorateur de stockage Azure](https://azurestorageexplorer.codeplex.com/)</span><span class="sxs-lookup"><span data-stu-id="d46a7-366">Create a file named **emp.txt** with hello following content and upload it toohello **input** folder by using tools such as [Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/)</span></span>
    ```json
    John, Doe
    Jane, Doe
    ```
### <a name="create-hello-data-factory"></a><span data-ttu-id="d46a7-367">Créer la fabrique de données hello</span><span class="sxs-lookup"><span data-stu-id="d46a7-367">Create hello data factory</span></span>
1. <span data-ttu-id="d46a7-368">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d46a7-368">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d46a7-369">Cliquez sur **+ nouveau** à partir de l’angle supérieur gauche de hello, cliquez sur **Intelligence + analytique**, puis cliquez sur **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-369">Click **+ NEW** from hello top-left corner, click **Intelligence + analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="d46a7-370">Bonjour **nouvelle fabrique de données** panneau :</span><span class="sxs-lookup"><span data-stu-id="d46a7-370">In hello **New data factory** blade:</span></span>   
    1. <span data-ttu-id="d46a7-371">Entrez **ADFBlobConnectorDF** pour hello **nom**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-371">Enter **ADFBlobConnectorDF** for hello **name**.</span></span> <span data-ttu-id="d46a7-372">nom de Hello de fabrique de données Azure hello doit être globalement unique.</span><span class="sxs-lookup"><span data-stu-id="d46a7-372">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="d46a7-373">Si vous recevez une erreur de hello : `*Data factory name “ADFBlobConnectorDF” is not available`, de modifier le nom hello hello fabrique de données (par exemple, yournameADFBlobConnectorDF) et essayez à nouveau de créer.</span><span class="sxs-lookup"><span data-stu-id="d46a7-373">If you receive hello error: `*Data factory name “ADFBlobConnectorDF” is not available`, change hello name of hello data factory (for example, yournameADFBlobConnectorDF) and try creating again.</span></span> <span data-ttu-id="d46a7-374">Consultez la rubrique [Data Factory - Règles d'affectation des noms](data-factory-naming-rules.md) pour savoir comment nommer les artefacts Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d46a7-374">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
    2. <span data-ttu-id="d46a7-375">Sélectionnez votre **abonnement**Azure.</span><span class="sxs-lookup"><span data-stu-id="d46a7-375">Select your Azure **subscription**.</span></span>
    3. <span data-ttu-id="d46a7-376">Pour le groupe de ressources, sélectionnez **utiliser l’existant** tooselect un ressource groupe (ou) sélectionnez **nouvel** tooenter un nom pour un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="d46a7-376">For Resource Group, select **Use existing** tooselect an existing resource group (or) select **Create new** tooenter a name for a resource group.</span></span>
    4. <span data-ttu-id="d46a7-377">Sélectionnez un **emplacement** de fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="d46a7-377">Select a **location** for hello data factory.</span></span>
    5. <span data-ttu-id="d46a7-378">Sélectionnez **toodashboard du code confidentiel** bas hello du Panneau de hello de case à cocher.</span><span class="sxs-lookup"><span data-stu-id="d46a7-378">Select **Pin toodashboard** check box at hello bottom of hello blade.</span></span>
    6. <span data-ttu-id="d46a7-379">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-379">Click **Create**.</span></span>
3. <span data-ttu-id="d46a7-380">Après la création de hello est terminée, vous voyez hello **Data Factory** panneau comme indiqué dans hello suivant image : ![page d’accueil de fabrique de données](./media/data-factory-azure-blob-connector/data-factory-home-page.png)</span><span class="sxs-lookup"><span data-stu-id="d46a7-380">After hello creation is complete, you see hello **Data Factory** blade as shown in hello following image: ![Data factory home page](./media/data-factory-azure-blob-connector/data-factory-home-page.png)</span></span>

### <a name="copy-wizard"></a><span data-ttu-id="d46a7-381">Assistant de copie</span><span class="sxs-lookup"><span data-stu-id="d46a7-381">Copy Wizard</span></span>
1. <span data-ttu-id="d46a7-382">Sur la page d’accueil de Data Factory hello, cliquez sur hello **copier des données [Aperçu]** vignette toolaunch **Assistant copie de données** dans un onglet séparé.</span><span class="sxs-lookup"><span data-stu-id="d46a7-382">On hello Data Factory home page, click hello **Copy data [PREVIEW]** tile toolaunch **Copy Data Wizard** in a separate tab.</span></span>    
    
    > [!NOTE]
    >    <span data-ttu-id="d46a7-383">Si vous voyez ce navigateur hello est bloqué au niveau de « Autorisation... », désactiver/Décochez **bloquer les cookies tiers et les données de site** définition (ou) qu’il soit activé et créer une exception pour **login.microsoftonline.com**, puis essayez de lancer les Assistant hello à nouveau.</span><span class="sxs-lookup"><span data-stu-id="d46a7-383">If you see that hello web browser is stuck at "Authorizing...", disable/uncheck **Block third-party cookies and site data** setting (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching hello wizard again.</span></span>
2. <span data-ttu-id="d46a7-384">Bonjour **propriétés** page :</span><span class="sxs-lookup"><span data-stu-id="d46a7-384">In hello **Properties** page:</span></span>
    1. <span data-ttu-id="d46a7-385">Entrez **CopyPipeline** comme **Nom de la tâche**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-385">Enter **CopyPipeline** for **Task name**.</span></span> <span data-ttu-id="d46a7-386">nom de tâche Hello est hello du pipeline hello dans votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="d46a7-386">hello task name is hello name of hello pipeline in your data factory.</span></span>
    2. <span data-ttu-id="d46a7-387">Entrez un **description** pour la tâche hello (facultatif).</span><span class="sxs-lookup"><span data-stu-id="d46a7-387">Enter a **description** for hello task (optional).</span></span>
    3. <span data-ttu-id="d46a7-388">Pour **cadence de tâche ou de la planification de la tâche**, conserver hello **exécuter régulièrement selon la planification** option.</span><span class="sxs-lookup"><span data-stu-id="d46a7-388">For **Task cadence or Task schedule**, keep hello **Run regularly on schedule** option.</span></span> <span data-ttu-id="d46a7-389">Si vous souhaitez toorun cette tâche qu’une seule fois au lieu de s’exécuter à plusieurs reprises selon une planification, sélectionnez **exécuter qu’une seule fois maintenant**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-389">If you want toorun this task only once instead of run repeatedly on a schedule, select **Run once now**.</span></span> <span data-ttu-id="d46a7-390">Si vous sélectionnez l’option **Run once now (Exécuter une seule fois maintenant)**, un [pipeline à usage unique](data-factory-create-pipelines.md#onetime-pipeline) est créé.</span><span class="sxs-lookup"><span data-stu-id="d46a7-390">If you select, **Run once now** option, a [one-time pipeline](data-factory-create-pipelines.md#onetime-pipeline) is created.</span></span> 
    4. <span data-ttu-id="d46a7-391">Conservez les paramètres hello pour **périodique modèle**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-391">Keep hello settings for **Recurring pattern**.</span></span> <span data-ttu-id="d46a7-392">Cette tâche s’exécute tous les jours entre hello début et de fin que vous spécifiez dans l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="d46a7-392">This task runs daily between hello start and end times you specify in hello next step.</span></span>
    5. <span data-ttu-id="d46a7-393">Hello de modification **date heure de début** trop**21/04/2017**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-393">Change hello **Start date time** too**04/21/2017**.</span></span> 
    6. <span data-ttu-id="d46a7-394">Hello de modification **date heure de fin** trop**25/04/2017**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-394">Change hello **End date time** too**04/25/2017**.</span></span> <span data-ttu-id="d46a7-395">Vous souhaiterez peut-être date de hello tootype au lieu de parcourir le calendrier de hello.</span><span class="sxs-lookup"><span data-stu-id="d46a7-395">You may want tootype hello date instead of browsing through hello calendar.</span></span>     
    8. <span data-ttu-id="d46a7-396">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-396">Click **Next**.</span></span>
      <span data-ttu-id="d46a7-397">![Outil de copie - Page Propriétés](./media/data-factory-azure-blob-connector/copy-tool-properties-page.png)</span><span class="sxs-lookup"><span data-stu-id="d46a7-397">![Copy Tool - Properties page](./media/data-factory-azure-blob-connector/copy-tool-properties-page.png)</span></span> 
3. <span data-ttu-id="d46a7-398">Sur hello **magasin de données Source** , cliquez sur **stockage d’objets Blob Azure** vignette.</span><span class="sxs-lookup"><span data-stu-id="d46a7-398">On hello **Source data store** page, click **Azure Blob Storage** tile.</span></span> <span data-ttu-id="d46a7-399">Vous utilisez cette banque de données de page toospecify hello source pour la tâche de copie hello.</span><span class="sxs-lookup"><span data-stu-id="d46a7-399">You use this page toospecify hello source data store for hello copy task.</span></span> <span data-ttu-id="d46a7-400">Vous pouvez utiliser un service lié de magasin de données existant (ou) spécifier un nouveau magasin de données.</span><span class="sxs-lookup"><span data-stu-id="d46a7-400">You can use an existing data store linked service (or) specify a new data store.</span></span> <span data-ttu-id="d46a7-401">service lié de toouse existant, vous devez sélectionner **de lié SERVICES existants** et sélectionnez hello service lié à droite.</span><span class="sxs-lookup"><span data-stu-id="d46a7-401">toouse an existing linked service, you would select **FROM EXISTING LINKED SERVICES** and select hello right linked service.</span></span> 
    <span data-ttu-id="d46a7-402">![Outil de copie - Page Banque de données sources](./media/data-factory-azure-blob-connector/copy-tool-source-data-store-page.png)</span><span class="sxs-lookup"><span data-stu-id="d46a7-402">![Copy Tool - Source data store page](./media/data-factory-azure-blob-connector/copy-tool-source-data-store-page.png)</span></span>
4. <span data-ttu-id="d46a7-403">Sur hello **spécifier le compte de stockage d’objets Blob Azure hello** page :</span><span class="sxs-lookup"><span data-stu-id="d46a7-403">On hello **Specify hello Azure Blob storage account** page:</span></span>
   1. <span data-ttu-id="d46a7-404">Conserver le nom généré automatiquement de hello pour **nom de la connexion**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-404">Keep hello auto-generated name for **Connection name**.</span></span> <span data-ttu-id="d46a7-405">nom de la connexion Hello est nom hello du service hello lié de type : le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="d46a7-405">hello connection name is hello name of hello linked service of type: Azure Storage.</span></span> 
   2. <span data-ttu-id="d46a7-406">Vérifiez que l’option **À partir des abonnements** est sélectionnée pour **Account selection method** (Méthode de sélection du compte).</span><span class="sxs-lookup"><span data-stu-id="d46a7-406">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="d46a7-407">Sélectionnez votre abonnement Azure ou conservez **Sélectionner tout** pour l’option **Abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-407">Select your Azure subscription or keep **Select all** for **Azure subscription**.</span></span>   
   4. <span data-ttu-id="d46a7-408">Sélectionnez un **compte de stockage Azure** hello à partir de la liste de stockage Azure comptes disponible dans l’abonnement de hello sélectionné.</span><span class="sxs-lookup"><span data-stu-id="d46a7-408">Select an **Azure storage account** from hello list of Azure storage accounts available in hello selected subscription.</span></span> <span data-ttu-id="d46a7-409">Vous pouvez également choisir tooenter les paramètres de compte de stockage manuellement en sélectionnant **entrer manuellement** option hello **méthode de sélection du compte**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-409">You can also choose tooenter storage account settings manually by selecting **Enter manually** option for hello **Account selection method**.</span></span>
   5. <span data-ttu-id="d46a7-410">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-410">Click **Next**.</span></span> 
      <span data-ttu-id="d46a7-411">![Outil Copier - spécifiez le compte de stockage d’objets Blob Azure hello](./media/data-factory-azure-blob-connector/copy-tool-specify-azure-blob-storage-account.png)</span><span class="sxs-lookup"><span data-stu-id="d46a7-411">![Copy Tool - Specify hello Azure Blob storage account](./media/data-factory-azure-blob-connector/copy-tool-specify-azure-blob-storage-account.png)</span></span>
5. <span data-ttu-id="d46a7-412">Sur **choisir un fichier d’entrée hello ou un dossier** page :</span><span class="sxs-lookup"><span data-stu-id="d46a7-412">On **Choose hello input file or folder** page:</span></span>
   1. <span data-ttu-id="d46a7-413">Double-cliquez sur **adfblobcontainer**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-413">Double-click **adfblobcontainer**.</span></span>
   2. <span data-ttu-id="d46a7-414">Sélectionnez **input**, puis cliquez sur **Choisir**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-414">Select **input**, and click **Choose**.</span></span> <span data-ttu-id="d46a7-415">Dans cette procédure pas à pas, vous sélectionnez les dossiers d’entrée hello.</span><span class="sxs-lookup"><span data-stu-id="d46a7-415">In this walkthrough, you select hello input folder.</span></span> <span data-ttu-id="d46a7-416">Vous pouvez également sélectionner à la place le fichier de emp.txt hello dans le dossier de hello.</span><span class="sxs-lookup"><span data-stu-id="d46a7-416">You could also select hello emp.txt file in hello folder instead.</span></span> 
      <span data-ttu-id="d46a7-417">![Outil Copier - choisir un fichier d’entrée de hello ou un dossier](./media/data-factory-azure-blob-connector/copy-tool-choose-input-file-or-folder.png)</span><span class="sxs-lookup"><span data-stu-id="d46a7-417">![Copy Tool - Choose hello input file or folder](./media/data-factory-azure-blob-connector/copy-tool-choose-input-file-or-folder.png)</span></span>
6. <span data-ttu-id="d46a7-418">Sur hello **choisir un fichier d’entrée hello ou un dossier** page :</span><span class="sxs-lookup"><span data-stu-id="d46a7-418">On hello **Choose hello input file or folder** page:</span></span>
    1. <span data-ttu-id="d46a7-419">Vérifiez que hello **fichier ou dossier** est défini trop**adfblobconnector/entrée**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-419">Confirm that hello **file or folder** is set too**adfblobconnector/input**.</span></span> <span data-ttu-id="d46a7-420">Si les fichiers de hello sont des sous-dossiers, par exemple, 04/01/2017 2017/04/02 et ainsi de suite, entrez adfblobconnector/entrée / {year} / {month} / {day} pour le fichier ou dossier.</span><span class="sxs-lookup"><span data-stu-id="d46a7-420">If hello files are in sub folders, for example, 2017/04/01, 2017/04/02, and so on, enter adfblobconnector/input/{year}/{month}/{day} for file or folder.</span></span> <span data-ttu-id="d46a7-421">Lorsque vous appuyez sur TAB en dehors de la zone de texte hello, vous voyez trois formats tooselect de listes déroulantes pour l’année (aaaa), month (MM) et le jour (jj).</span><span class="sxs-lookup"><span data-stu-id="d46a7-421">When you press TAB out of hello text box, you see three drop-down lists tooselect formats for year (yyyy), month (MM), and day (dd).</span></span> 
    2. <span data-ttu-id="d46a7-422">Ne définissez pas **Copy file recursively (Copier le fichier de façon récursive)**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-422">Do not set **Copy file recursively**.</span></span> <span data-ttu-id="d46a7-423">Sélectionnez cette toorecursively option Parcourir de dossiers pour les fichiers toobe copiés toohello destination.</span><span class="sxs-lookup"><span data-stu-id="d46a7-423">Select this option toorecursively traverse through folders for files toobe copied toohello destination.</span></span> 
    3. <span data-ttu-id="d46a7-424">Ne pas hello **copie binaire** option.</span><span class="sxs-lookup"><span data-stu-id="d46a7-424">Do not hello **binary copy** option.</span></span> <span data-ttu-id="d46a7-425">Sélectionnez cette option de tooperform une copie binaire de destination toohello du fichier source.</span><span class="sxs-lookup"><span data-stu-id="d46a7-425">Select this option tooperform a binary copy of source file toohello destination.</span></span> <span data-ttu-id="d46a7-426">Ne sélectionnez pas cette procédure pas à pas afin que vous puissiez voir davantage d’options dans les pages suivantes de hello.</span><span class="sxs-lookup"><span data-stu-id="d46a7-426">Do not select for this walkthrough so that you can see more options in hello next pages.</span></span> 
    4. <span data-ttu-id="d46a7-427">Vérifiez que hello **le type de Compression** est défini trop**aucun**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-427">Confirm that hello **Compression type** is set too**None**.</span></span> <span data-ttu-id="d46a7-428">Sélectionnez une valeur pour cette option si vos fichiers source sont compressés dans un des formats de hello pris en charge.</span><span class="sxs-lookup"><span data-stu-id="d46a7-428">Select a value for this option if your source files are compressed in one of hello supported formats.</span></span> 
    5. <span data-ttu-id="d46a7-429">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-429">Click **Next**.</span></span>
    <span data-ttu-id="d46a7-430">![Outil Copier - choisir un fichier d’entrée de hello ou un dossier](./media/data-factory-azure-blob-connector/chose-input-file-folder.png)</span><span class="sxs-lookup"><span data-stu-id="d46a7-430">![Copy Tool - Choose hello input file or folder](./media/data-factory-azure-blob-connector/chose-input-file-folder.png)</span></span> 
7. <span data-ttu-id="d46a7-431">Sur hello **les paramètres de format de fichier** page, vous voyez les délimiteurs hello et schéma de hello est détecté automatiquement par l’Assistant de hello par l’analyse du fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="d46a7-431">On hello **File format settings** page, you see hello delimiters and hello schema that is auto-detected by hello wizard by parsing hello file.</span></span> 
    1. <span data-ttu-id="d46a7-432">Confirmer les options suivantes de hello : un.</span><span class="sxs-lookup"><span data-stu-id="d46a7-432">Confirm hello following options: a.</span></span> <span data-ttu-id="d46a7-433">Hello **format de fichier** est défini trop**au format texte**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-433">hello **file format** is set too**Text format**.</span></span> <span data-ttu-id="d46a7-434">Vous pouvez voir tous les formats de hello pris en charge dans la liste déroulante de hello.</span><span class="sxs-lookup"><span data-stu-id="d46a7-434">You can see all hello supported formats in hello drop-down list.</span></span> <span data-ttu-id="d46a7-435">Exemple : JSON, Avro, ORC, Parquet.</span><span class="sxs-lookup"><span data-stu-id="d46a7-435">For example: JSON, Avro, ORC, Parquet.</span></span>
        <span data-ttu-id="d46a7-436">b.</span><span class="sxs-lookup"><span data-stu-id="d46a7-436">b.</span></span> <span data-ttu-id="d46a7-437">Hello **délimiteur de colonne** est défini trop`Comma (,)`.</span><span class="sxs-lookup"><span data-stu-id="d46a7-437">hello **column delimiter** is set too`Comma (,)`.</span></span> <span data-ttu-id="d46a7-438">Vous pouvez voir hello autres séparateurs de colonnes pris en charge par la fabrique de données dans la liste déroulante de hello.</span><span class="sxs-lookup"><span data-stu-id="d46a7-438">You can see hello other column delimiters supported by Data Factory in hello drop-down list.</span></span> <span data-ttu-id="d46a7-439">Vous pouvez également spécifier un séparateur personnalisé.</span><span class="sxs-lookup"><span data-stu-id="d46a7-439">You can also specify a custom delimiter.</span></span>
        <span data-ttu-id="d46a7-440">c.</span><span class="sxs-lookup"><span data-stu-id="d46a7-440">c.</span></span> <span data-ttu-id="d46a7-441">Hello **séparateur de lignes** est défini trop`Carriage Return + Line feed (\r\n)`.</span><span class="sxs-lookup"><span data-stu-id="d46a7-441">hello **row delimiter** is set too`Carriage Return + Line feed (\r\n)`.</span></span> <span data-ttu-id="d46a7-442">Vous pouvez voir hello autres séparateurs de lignes pris en charge par la fabrique de données dans la liste déroulante de hello.</span><span class="sxs-lookup"><span data-stu-id="d46a7-442">You can see hello other row delimiters supported by Data Factory in hello drop-down list.</span></span> <span data-ttu-id="d46a7-443">Vous pouvez également spécifier un séparateur personnalisé.</span><span class="sxs-lookup"><span data-stu-id="d46a7-443">You can also specify a custom delimiter.</span></span>
        <span data-ttu-id="d46a7-444">d.</span><span class="sxs-lookup"><span data-stu-id="d46a7-444">d.</span></span> <span data-ttu-id="d46a7-445">Hello **ignorer le nombre de lignes** est défini trop**0**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-445">hello **skip line count** is set too**0**.</span></span> <span data-ttu-id="d46a7-446">Si vous souhaitez que quelques lignes toobe ignorée haut hello du fichier de hello, entrez le numéro de hello ici.</span><span class="sxs-lookup"><span data-stu-id="d46a7-446">If you want a few lines toobe skipped at hello top of hello file, enter hello number here.</span></span>
        <span data-ttu-id="d46a7-447">e.</span><span class="sxs-lookup"><span data-stu-id="d46a7-447">e.</span></span>  <span data-ttu-id="d46a7-448">Hello **première ligne de données contient des noms de colonne** n’est pas définie.</span><span class="sxs-lookup"><span data-stu-id="d46a7-448">hello **first data row contains column names** is not set.</span></span> <span data-ttu-id="d46a7-449">Si les fichiers de sources de hello contiennent des noms de colonnes dans la première ligne de hello, sélectionnez cette option.</span><span class="sxs-lookup"><span data-stu-id="d46a7-449">If hello source files contain column names in hello first row, select this option.</span></span>
        <span data-ttu-id="d46a7-450">f.</span><span class="sxs-lookup"><span data-stu-id="d46a7-450">f.</span></span> <span data-ttu-id="d46a7-451">Hello **traiter la valeur de la colonne vide comme null** option est définie.</span><span class="sxs-lookup"><span data-stu-id="d46a7-451">hello **treat empty column value as null** option is set.</span></span>
    2. <span data-ttu-id="d46a7-452">Développez **paramètres avancés** toosee advanced option disponible.</span><span class="sxs-lookup"><span data-stu-id="d46a7-452">Expand **Advanced settings** toosee advanced option available.</span></span>
    3. <span data-ttu-id="d46a7-453">Au bas de hello de page de hello, consultez hello **aperçu** de données à partir du fichier de emp.txt hello.</span><span class="sxs-lookup"><span data-stu-id="d46a7-453">At hello bottom of hello page, see hello **preview** of data from hello emp.txt file.</span></span>
    4. <span data-ttu-id="d46a7-454">Cliquez sur **schéma** onglet au schéma de hello hello bas toosee cet Assistant copie de hello déduit en examinant les données de salutation dans le fichier de source de hello.</span><span class="sxs-lookup"><span data-stu-id="d46a7-454">Click **SCHEMA** tab at hello bottom toosee hello schema that hello copy wizard inferred by looking at hello data in hello source file.</span></span>
    5. <span data-ttu-id="d46a7-455">Cliquez sur **suivant** une fois que vous passez en revue les délimiteurs hello et afficher un aperçu des données.</span><span class="sxs-lookup"><span data-stu-id="d46a7-455">Click **Next** after you review hello delimiters and preview data.</span></span>
    <span data-ttu-id="d46a7-456">![Outil de copie - Paramètres de format de fichier](./media/data-factory-azure-blob-connector/copy-tool-file-format-settings.png)</span><span class="sxs-lookup"><span data-stu-id="d46a7-456">![Copy Tool - File format settings](./media/data-factory-azure-blob-connector/copy-tool-file-format-settings.png)</span></span>  
8. <span data-ttu-id="d46a7-457">Sur hello **page de magasin de données de Destination**, sélectionnez **stockage d’objets Blob Azure**, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-457">On hello **Destination data store page**, select **Azure Blob Storage**, and click **Next**.</span></span> <span data-ttu-id="d46a7-458">Vous utilisez hello stockage d’objets Blob Azure en tant que les deux magasins hello les données source et de destination dans cette procédure pas à pas.</span><span class="sxs-lookup"><span data-stu-id="d46a7-458">You are using hello Azure Blob Storage as both hello source and destination data stores in this walkthrough.</span></span>    
    <span data-ttu-id="d46a7-459">![Outil de copie - Sélectionner la banque de données de destination](media/data-factory-azure-blob-connector/select-destination-data-store.png)</span><span class="sxs-lookup"><span data-stu-id="d46a7-459">![Copy Tool - select destination data store](media/data-factory-azure-blob-connector/select-destination-data-store.png)</span></span>
9. <span data-ttu-id="d46a7-460">Sur **spécifier le compte de stockage d’objets Blob Azure hello** page :</span><span class="sxs-lookup"><span data-stu-id="d46a7-460">On **Specify hello Azure Blob storage account** page:</span></span>
   1. <span data-ttu-id="d46a7-461">Entrez **AzureStorageLinkedService** pour hello **nom de la connexion** champ.</span><span class="sxs-lookup"><span data-stu-id="d46a7-461">Enter **AzureStorageLinkedService** for hello **Connection name** field.</span></span>
   2. <span data-ttu-id="d46a7-462">Vérifiez que l’option **À partir des abonnements** est sélectionnée pour **Account selection method** (Méthode de sélection du compte).</span><span class="sxs-lookup"><span data-stu-id="d46a7-462">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="d46a7-463">Sélectionnez votre **abonnement**Azure.</span><span class="sxs-lookup"><span data-stu-id="d46a7-463">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="d46a7-464">Sélectionnez votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="d46a7-464">Select your Azure storage account.</span></span> 
   5. <span data-ttu-id="d46a7-465">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-465">Click **Next**.</span></span>     
10. <span data-ttu-id="d46a7-466">Sur hello **fichier ou le dossier de sortie choisir hello** page :</span><span class="sxs-lookup"><span data-stu-id="d46a7-466">On hello **Choose hello output file or folder** page:</span></span> 
    6. <span data-ttu-id="d46a7-467">spécifiez le **chemin d’accès du dossier** **adfblobconnector/output/{année}/{mois}/{jour}**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-467">specify **Folder path** as **adfblobconnector/output/{year}/{month}/{day}**.</span></span> <span data-ttu-id="d46a7-468">Entrez **TAB**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-468">Enter **TAB**.</span></span>
    7. <span data-ttu-id="d46a7-469">Pourquoi **année**, sélectionnez **aaaa**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-469">For hello **year**, select **yyyy**.</span></span>
    8. <span data-ttu-id="d46a7-470">Pourquoi **mois**, vérifiez qu’il est défini trop**MM**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-470">For hello **month**, confirm that it is set too**MM**.</span></span>
    9. <span data-ttu-id="d46a7-471">Pourquoi **jour**, vérifiez qu’il est défini trop**jj**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-471">For hello **day**, confirm that it is set too**dd**.</span></span>
    10. <span data-ttu-id="d46a7-472">Vérifiez que hello **le type de compression** est défini trop**aucun**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-472">Confirm that hello **compression type** is set too**None**.</span></span>
    11. <span data-ttu-id="d46a7-473">Vérifiez que hello **copier comportement** est défini trop**fusionner les fichiers**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-473">Confirm that hello **copy behavior** is set too**Merge files**.</span></span> <span data-ttu-id="d46a7-474">Si la sortie hello fichier avec le même nom existe déjà de hello, hello nouveau contenu est ajouté toohello même fichier à la fin de hello.</span><span class="sxs-lookup"><span data-stu-id="d46a7-474">If hello output file with hello same name already exists, hello new content is added toohello same file at hello end.</span></span>
    12. <span data-ttu-id="d46a7-475">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-475">Click **Next**.</span></span>
    <span data-ttu-id="d46a7-476">![Outil de copie - Choisir le fichier ou le dossier de sortie](media/data-factory-azure-blob-connector/choose-the-output-file-or-folder.png)</span><span class="sxs-lookup"><span data-stu-id="d46a7-476">![Copy Tool - Choose output file or folder](media/data-factory-azure-blob-connector/choose-the-output-file-or-folder.png)</span></span>
11. <span data-ttu-id="d46a7-477">Sur hello **les paramètres de format de fichier** page, passez en revue les paramètres de hello, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-477">On hello **File format settings** page, review hello settings, and click **Next**.</span></span> <span data-ttu-id="d46a7-478">Une des options supplémentaires de hello ici est tooadd un fichier de sortie d’en-tête toohello.</span><span class="sxs-lookup"><span data-stu-id="d46a7-478">One of hello additional options here is tooadd a header toohello output file.</span></span> <span data-ttu-id="d46a7-479">Si vous sélectionnez cette option, une ligne d’en-tête est ajoutée avec des noms de colonnes de hello schéma hello de source de hello.</span><span class="sxs-lookup"><span data-stu-id="d46a7-479">If you select that option, a header row is added with names of hello columns from hello schema of hello source.</span></span> <span data-ttu-id="d46a7-480">Vous pouvez renommer les noms de colonne par défaut hello lors de l’affichage de schéma hello pour la source de hello.</span><span class="sxs-lookup"><span data-stu-id="d46a7-480">You can rename hello default column names when viewing hello schema for hello source.</span></span> <span data-ttu-id="d46a7-481">Par exemple, vous pouvez modifier hello première colonne tooFirst nom et la deuxième colonne tooLast nom.</span><span class="sxs-lookup"><span data-stu-id="d46a7-481">For example, you could change hello first column tooFirst Name and second column tooLast Name.</span></span> <span data-ttu-id="d46a7-482">Puis, le fichier de sortie hello est généré avec un en-tête avec ces noms comme noms de colonne.</span><span class="sxs-lookup"><span data-stu-id="d46a7-482">Then, hello output file is generated with a header with these names as column names.</span></span> 
    <span data-ttu-id="d46a7-483">![Outil de copie - Paramètres de format de fichier pour la destination](media/data-factory-azure-blob-connector/file-format-destination.png)</span><span class="sxs-lookup"><span data-stu-id="d46a7-483">![Copy Tool - File format settings for destination](media/data-factory-azure-blob-connector/file-format-destination.png)</span></span>
12. <span data-ttu-id="d46a7-484">Sur hello **les paramètres de performances** page, vérifiez que **cloud unités** et **parallèles copies** sont définies trop**automatique**et cliquez sur Suivant.</span><span class="sxs-lookup"><span data-stu-id="d46a7-484">On hello **Performance settings** page, confirm that **cloud units** and **parallel copies** are set too**Auto**, and click Next.</span></span> <span data-ttu-id="d46a7-485">Pour plus d’informations sur ces paramètres, consultez le [Guide sur les performances et le réglage de l’activité de copie](data-factory-copy-activity-performance.md#parallel-copy).</span><span class="sxs-lookup"><span data-stu-id="d46a7-485">For details about these settings, see [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md#parallel-copy).</span></span>
    <span data-ttu-id="d46a7-486">![Outil de copie - Paramètres de performances](media/data-factory-azure-blob-connector/copy-performance-settings.png)</span><span class="sxs-lookup"><span data-stu-id="d46a7-486">![Copy Tool - Performance settings](media/data-factory-azure-blob-connector/copy-performance-settings.png)</span></span> 
14. <span data-ttu-id="d46a7-487">Sur hello **Résumé** page, passez en revue tous les paramètres (propriétés de la tâche, les paramètres pour la source et de destination et copier les paramètres), puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-487">On hello **Summary** page, review all settings (task properties, settings for source and destination, and copy settings), and click **Next**.</span></span>
    <span data-ttu-id="d46a7-488">![Outil de copie - Page Résumé](media/data-factory-azure-blob-connector/copy-tool-summary-page.png)</span><span class="sxs-lookup"><span data-stu-id="d46a7-488">![Copy Tool - Summary page](media/data-factory-azure-blob-connector/copy-tool-summary-page.png)</span></span>
15. <span data-ttu-id="d46a7-489">Passez en revue les informations contenues dans hello **Résumé** page, puis cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-489">Review information in hello **Summary** page, and click **Finish**.</span></span> <span data-ttu-id="d46a7-490">Assistant de Hello crée deux services liés, les deux jeux de données (entrées et sorties) et un seul pipeline dans la fabrique de données hello (à partir de lancement de hello Assistant copie de).</span><span class="sxs-lookup"><span data-stu-id="d46a7-490">hello wizard creates two linked services, two datasets (input and output), and one pipeline in hello data factory (from where you launched hello Copy Wizard).</span></span>
    <span data-ttu-id="d46a7-491">![Outil de copie - Page Déploiement](media/data-factory-azure-blob-connector/copy-tool-deployment-page.png)</span><span class="sxs-lookup"><span data-stu-id="d46a7-491">![Copy Tool - Deployment page](media/data-factory-azure-blob-connector/copy-tool-deployment-page.png)</span></span>

### <a name="monitor-hello-pipeline-copy-task"></a><span data-ttu-id="d46a7-492">Surveiller le pipeline hello (tâche de copie)</span><span class="sxs-lookup"><span data-stu-id="d46a7-492">Monitor hello pipeline (copy task)</span></span>

1. <span data-ttu-id="d46a7-493">Cliquez sur le lien de hello `Click here toomonitor copy pipeline` sur hello **déploiement** page.</span><span class="sxs-lookup"><span data-stu-id="d46a7-493">Click hello link `Click here toomonitor copy pipeline` on hello **Deployment** page.</span></span> 
2. <span data-ttu-id="d46a7-494">Vous devez voir hello **surveiller et gérer des applications** dans un onglet séparé.  ![Application Surveiller et gérer](media/data-factory-azure-blob-connector/monitor-manage-app.png)</span><span class="sxs-lookup"><span data-stu-id="d46a7-494">You should see hello **Monitor and Manage application** in a separate tab.  ![Monitor and Manage App](media/data-factory-azure-blob-connector/monitor-manage-app.png)</span></span>
3. <span data-ttu-id="d46a7-495">Hello de modification **Démarrer** trop de temps en haut de hello`04/19/2017` et **fin** trop de temps`04/27/2017`, puis cliquez sur **appliquer**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-495">Change hello **start** time at hello top too`04/19/2017` and **end** time too`04/27/2017`, and then click **Apply**.</span></span> 
4. <span data-ttu-id="d46a7-496">Vous devez voir cinq windows activité Bonjour **WINDOWS de l’activité** liste.</span><span class="sxs-lookup"><span data-stu-id="d46a7-496">You should see five activity windows in hello **ACTIVITY WINDOWS** list.</span></span> <span data-ttu-id="d46a7-497">Hello **WindowStart** fois doivent couvrir tous les jours à partir de l’heure de fin de pipeline début toopipeline.</span><span class="sxs-lookup"><span data-stu-id="d46a7-497">hello **WindowStart** times should cover all days from pipeline start toopipeline end times.</span></span> 
5. <span data-ttu-id="d46a7-498">Cliquez sur **Actualiser** bouton pour hello **WINDOWS de l’activité** liste plusieurs fois jusqu'à ce que vous voyiez état hello de toutes les fenêtres d’activité hello a la valeur tooReady.</span><span class="sxs-lookup"><span data-stu-id="d46a7-498">Click **Refresh** button for hello **ACTIVITY WINDOWS** list a few times until you see hello status of all hello activity windows is set tooReady.</span></span> 
6. <span data-ttu-id="d46a7-499">À présent, vérifiez que les fichiers de sortie hello sont générées dans le dossier de sortie hello du conteneur d’adfblobconnector.</span><span class="sxs-lookup"><span data-stu-id="d46a7-499">Now, verify that hello output files are generated in hello output folder of adfblobconnector container.</span></span> <span data-ttu-id="d46a7-500">Vous devez voir hello suivant la structure de dossiers dans le dossier de sortie hello :</span><span class="sxs-lookup"><span data-stu-id="d46a7-500">You should see hello following folder structure in hello output folder:</span></span> 
    ```
    2017/04/21
    2017/04/22
    2017/04/23
    2017/04/24
    2017/04/25    
    ```
<span data-ttu-id="d46a7-501">Pour plus d’informations sur la surveillance et la gestion des fabriques de données, consultez l’article [Monitor and manage Data Factory pipeline (Surveiller et gérer le pipeline Data Factory)](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="d46a7-501">For detailed information about monitoring and managing data factories, see [Monitor and manage Data Factory pipeline](data-factory-monitor-manage-app.md) article.</span></span> 
 
### <a name="data-factory-entities"></a><span data-ttu-id="d46a7-502">Entités Data Factory</span><span class="sxs-lookup"><span data-stu-id="d46a7-502">Data Factory entities</span></span>
<span data-ttu-id="d46a7-503">Passez maintenant, onglet toohello retour avec la page d’accueil de Data Factory hello.</span><span class="sxs-lookup"><span data-stu-id="d46a7-503">Now, switch back toohello tab with hello Data Factory home page.</span></span> <span data-ttu-id="d46a7-504">Notez qu’il existe désormais deux services liés, deux jeux de données et un pipeline dans votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="d46a7-504">Notice that there are two linked services, two datasets, and one pipeline in your data factory now.</span></span> 

![Page d’accueil Data Factory comportant des entités](media/data-factory-azure-blob-connector/data-factory-home-page-with-numbers.png)

<span data-ttu-id="d46a7-506">Cliquez sur **auteur et déployer** toolaunch éditeur Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d46a7-506">Click **Author and deploy** toolaunch Data Factory Editor.</span></span> 

![Data Factory Editor](media/data-factory-azure-blob-connector/data-factory-editor.png)

<span data-ttu-id="d46a7-508">Vous devez voir hello suivant des entités de fabrique de données dans votre fabrique de données :</span><span class="sxs-lookup"><span data-stu-id="d46a7-508">You should see hello following Data Factory entities in your data factory:</span></span> 

 - <span data-ttu-id="d46a7-509">Deux services liés,</span><span class="sxs-lookup"><span data-stu-id="d46a7-509">Two linked services.</span></span> <span data-ttu-id="d46a7-510">Un pour la source de hello et hello autre destination de hello.</span><span class="sxs-lookup"><span data-stu-id="d46a7-510">One for hello source and hello other one for hello destination.</span></span> <span data-ttu-id="d46a7-511">Les deux services hello lié font référence toohello même compte de stockage Azure dans cette procédure pas à pas.</span><span class="sxs-lookup"><span data-stu-id="d46a7-511">Both hello linked services refer toohello same Azure Storage account in this walkthrough.</span></span> 
 - <span data-ttu-id="d46a7-512">Deux jeux de données,</span><span class="sxs-lookup"><span data-stu-id="d46a7-512">Two datasets.</span></span> <span data-ttu-id="d46a7-513">un jeu de données d’entrée et un jeu de données de sortie.</span><span class="sxs-lookup"><span data-stu-id="d46a7-513">An input dataset and an output dataset.</span></span> <span data-ttu-id="d46a7-514">Dans cette procédure pas à pas, les deux utilisent hello même conteneur d’objets blob, mais reportez-vous dossiers toodifferent (entrées et sorties).</span><span class="sxs-lookup"><span data-stu-id="d46a7-514">In this walkthrough, both use hello same blob container but refer toodifferent folders (input and output).</span></span>
 - <span data-ttu-id="d46a7-515">Un pipeline.</span><span class="sxs-lookup"><span data-stu-id="d46a7-515">A pipeline.</span></span> <span data-ttu-id="d46a7-516">pipeline de Hello contient une activité de copie qui utilise une source d’objets blob et un objet blob récepteur toocopy des données d’une tooanother d’emplacement d’objets blob Azure emplacement d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="d46a7-516">hello pipeline contains a copy activity that uses a blob source and a blob sink toocopy data from an Azure blob location tooanother Azure blob location.</span></span> 

<span data-ttu-id="d46a7-517">Hello sections suivantes fournissent plus d’informations sur ces entités.</span><span class="sxs-lookup"><span data-stu-id="d46a7-517">hello following sections provide more information about these entities.</span></span> 

#### <a name="linked-services"></a><span data-ttu-id="d46a7-518">Services liés</span><span class="sxs-lookup"><span data-stu-id="d46a7-518">Linked services</span></span>
<span data-ttu-id="d46a7-519">Vous devez voir deux services liés,</span><span class="sxs-lookup"><span data-stu-id="d46a7-519">You should see two linked services.</span></span> <span data-ttu-id="d46a7-520">Un pour la source de hello et hello autre destination de hello.</span><span class="sxs-lookup"><span data-stu-id="d46a7-520">One for hello source and hello other one for hello destination.</span></span> <span data-ttu-id="d46a7-521">Dans cette procédure pas à pas, les deux définitions de regarder hello identiques à l’exception des noms de hello.</span><span class="sxs-lookup"><span data-stu-id="d46a7-521">In this walkthrough, both definitions look hello same except for hello names.</span></span> <span data-ttu-id="d46a7-522">Hello **type** Hello service lié est défini trop**AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-522">hello **type** of hello linked service is set too**AzureStorage**.</span></span> <span data-ttu-id="d46a7-523">Propriété la plus importante de définition du service lié de hello est hello **connectionString**, qui est utilisé par la fabrique de données tooconnect tooyour compte de stockage Azure lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="d46a7-523">Most important property of hello linked service definition is hello **connectionString**, which is used by Data Factory tooconnect tooyour Azure Storage account at runtime.</span></span> <span data-ttu-id="d46a7-524">Ignorer la propriété hubName de hello dans la définition de hello.</span><span class="sxs-lookup"><span data-stu-id="d46a7-524">Ignore hello hubName property in hello definition.</span></span> 

##### <a name="source-blob-storage-linked-service"></a><span data-ttu-id="d46a7-525">Service lié du stockage d’objets blob source</span><span class="sxs-lookup"><span data-stu-id="d46a7-525">Source blob storage linked service</span></span>
```json
{
    "name": "Source-BlobStorage-z4y",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=mystorageaccount;AccountKey=**********"
        }
    }
}
```

##### <a name="destination-blob-storage-linked-service"></a><span data-ttu-id="d46a7-526">Service lié du stockage d’objets blob de destination</span><span class="sxs-lookup"><span data-stu-id="d46a7-526">Destination blob storage linked service</span></span>

```json
{
    "name": "Destination-BlobStorage-z4y",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=mystorageaccount;AccountKey=**********"
        }
    }
}
```

<span data-ttu-id="d46a7-527">Pour plus d’informations sur le service lié Stockage Azure, consultez la section [Propriétés du service lié](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d46a7-527">For more information about Azure Storage linked service, see [Linked service properties](#linked-service-properties) section.</span></span> 

#### <a name="datasets"></a><span data-ttu-id="d46a7-528">Groupes de données</span><span class="sxs-lookup"><span data-stu-id="d46a7-528">Datasets</span></span>
<span data-ttu-id="d46a7-529">Il existe deux jeux de données : un jeu de données d’entrée et un jeu de données de sortie.</span><span class="sxs-lookup"><span data-stu-id="d46a7-529">There are two datasets: an input dataset and an output dataset.</span></span> <span data-ttu-id="d46a7-530">type Hello du jeu de données hello est défini trop**AzureBlob** pour les deux.</span><span class="sxs-lookup"><span data-stu-id="d46a7-530">hello type of hello dataset is set too**AzureBlob** for both.</span></span> 

<span data-ttu-id="d46a7-531">jeu de données d’entrée Hello pointe toohello **d’entrée** dossier Hello **adfblobconnector** conteneur d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="d46a7-531">hello input dataset points toohello **input** folder of hello **adfblobconnector** blob container.</span></span> <span data-ttu-id="d46a7-532">Hello **externe** propriété a la valeur trop**true** pour ce jeu de données en tant que hello données ne sont pas produites par le pipeline de hello avec l’activité de copie hello acceptant ce jeu de données en tant qu’entrée.</span><span class="sxs-lookup"><span data-stu-id="d46a7-532">hello **external** property is set too**true** for this dataset as hello data is not produced by hello pipeline with hello copy activity that takes this dataset as an input.</span></span> 

<span data-ttu-id="d46a7-533">Hello sortie dataset points toohello **sortie** dossier Hello même conteneur d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="d46a7-533">hello output dataset points toohello **output** folder of hello same blob container.</span></span> <span data-ttu-id="d46a7-534">Hello dataset de sortie utilise également hello year, month et le jour de hello **SliceStart** toodynamically de variables système évaluer le chemin d’accès de hello pour le fichier de sortie hello.</span><span class="sxs-lookup"><span data-stu-id="d46a7-534">hello output dataset also uses hello year, month, and day of hello **SliceStart** system variable toodynamically evaluate hello path for hello output file.</span></span> <span data-ttu-id="d46a7-535">Pour obtenir la liste des fonctions et variables système prises en charge par Data Factory, consultez [Variables système et fonctions Data Factory](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="d46a7-535">For a list of functions and system variables supported by Data Factory, see [Data Factory functions and system variables](data-factory-functions-variables.md).</span></span> <span data-ttu-id="d46a7-536">Hello **externe** propriété a la valeur trop**false** (valeur par défaut), car ce jeu de données est généré par le pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="d46a7-536">hello **external** property is set too**false** (default value) because this dataset is produced by hello pipeline.</span></span> 

<span data-ttu-id="d46a7-537">Pour plus d’informations sur les propriétés prises en charge par le jeu de données d’objets blob Azure, consultez la section [Propriétés du jeu de données](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d46a7-537">For more information about properties supported by Azure Blob dataset, see [Dataset properties](#dataset-properties) section.</span></span>

##### <a name="input-dataset"></a><span data-ttu-id="d46a7-538">Jeu de données d'entrée</span><span class="sxs-lookup"><span data-stu-id="d46a7-538">Input dataset</span></span>

```json
{
    "name": "InputDataset-z4y",
    "properties": {
        "structure": [
            { "name": "Prop_0", "type": "String" },
            { "name": "Prop_1", "type": "String" }
        ],
        "type": "AzureBlob",
        "linkedServiceName": "Source-BlobStorage-z4y",
        "typeProperties": {
            "folderPath": "adfblobconnector/input/",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```

##### <a name="output-dataset"></a><span data-ttu-id="d46a7-539">Jeu de données de sortie</span><span class="sxs-lookup"><span data-stu-id="d46a7-539">Output dataset</span></span>

```json
{
    "name": "OutputDataset-z4y",
    "properties": {
        "structure": [
            { "name": "Prop_0", "type": "String" },
            { "name": "Prop_1", "type": "String" }
        ],
        "type": "AzureBlob",
        "linkedServiceName": "Destination-BlobStorage-z4y",
        "typeProperties": {
            "folderPath": "adfblobconnector/output/{year}/{month}/{day}",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            },
            "partitionedBy": [
                { "name": "year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
                { "name": "month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
                { "name": "day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } }
            ]
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }
}
```

#### <a name="pipeline"></a><span data-ttu-id="d46a7-540">Pipeline</span><span class="sxs-lookup"><span data-stu-id="d46a7-540">Pipeline</span></span>
<span data-ttu-id="d46a7-541">pipeline de Hello a qu’une seule activité.</span><span class="sxs-lookup"><span data-stu-id="d46a7-541">hello pipeline has just one activity.</span></span> <span data-ttu-id="d46a7-542">Hello **type** Hello activité est définie trop**copie**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-542">hello **type** of hello activity is set too**Copy**.</span></span>  <span data-ttu-id="d46a7-543">Dans les propriétés de type hello pour l’activité de hello, il existe deux sections, une pour la source et hello autre pour le récepteur.</span><span class="sxs-lookup"><span data-stu-id="d46a7-543">In hello type properties for hello activity, there are two sections, one for source and hello other one for sink.</span></span> <span data-ttu-id="d46a7-544">type de source de Hello est défini trop**BlobSource** comme activité hello copie des données à partir d’un stockage d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="d46a7-544">hello source type is set too**BlobSource** as hello activity is copying data from a blob storage.</span></span> <span data-ttu-id="d46a7-545">Hello le type de récepteur est défini trop**BlobSink** en tant qu’activité hello copie le stockage d’objets blob de données tooa.</span><span class="sxs-lookup"><span data-stu-id="d46a7-545">hello sink type is set too**BlobSink** as hello activity copying data tooa blob storage.</span></span> <span data-ttu-id="d46a7-546">activité de copie Hello prend InputDataset-z4y en tant qu’entrée de hello et OutputDataset-z4y en tant que sortie de hello.</span><span class="sxs-lookup"><span data-stu-id="d46a7-546">hello copy activity takes InputDataset-z4y as hello input and OutputDataset-z4y as hello output.</span></span> 

<span data-ttu-id="d46a7-547">Pour plus d’informations sur les propriétés prises en charge par BlobSource et BlobSink, consultez la section [Propriétés de l’activité de copie](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="d46a7-547">For more information about properties supported by BlobSource and BlobSink, see [Copy activity properties](#copy-activity-properties) section.</span></span> 

```json
{
    "name": "CopyPipeline",
    "properties": {
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource",
                        "recursive": false
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "MergeFiles",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataset-z4y"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset-z4y"
                    }
                ],
                "policy": {
                    "timeout": "1.00:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "style": "StartOfInterval",
                    "retry": 3,
                    "longRetry": 0,
                    "longRetryInterval": "00:00:00"
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "Activity-0-Blob path_ adfblobconnector_input_->OutputDataset-z4y"
            }
        ],
        "start": "2017-04-21T22:34:00Z",
        "end": "2017-04-25T05:00:00Z",
        "isPaused": false,
        "pipelineMode": "Scheduled"
    }
}
```

## <a name="json-examples-for-copying-data-tooand-from-blob-storage"></a><span data-ttu-id="d46a7-548">Exemples JSON pour la copie des données tooand depuis le stockage Blob</span><span class="sxs-lookup"><span data-stu-id="d46a7-548">JSON examples for copying data tooand from Blob Storage</span></span>  
<span data-ttu-id="d46a7-549">Hello exemples suivants proposent des exemples de définitions de JSON que vous pouvez utiliser toocreate un pipeline à l’aide de [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="d46a7-549">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="d46a7-550">Elles montrent comment tooand de données toocopy à partir de la base de données SQL Azure et de stockage d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="d46a7-550">They show how toocopy data tooand from Azure Blob Storage and Azure SQL Database.</span></span> <span data-ttu-id="d46a7-551">Toutefois, les données peuvent être copiées **directement** de n’importe quelle tooany de sources de récepteurs hello indiqué [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) à l’aide de hello activité de copie dans Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d46a7-551">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

### <a name="json-example-copy-data-from-blob-storage-toosql-database"></a><span data-ttu-id="d46a7-552">Exemple de JSON : Copier les données de stockage d’objets Blob tooSQL de base de données</span><span class="sxs-lookup"><span data-stu-id="d46a7-552">JSON Example: Copy data from Blob Storage tooSQL Database</span></span>
<span data-ttu-id="d46a7-553">Hello ci-dessous illustre d’exemple :</span><span class="sxs-lookup"><span data-stu-id="d46a7-553">hello following sample shows:</span></span>

1. <span data-ttu-id="d46a7-554">Un service lié de type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d46a7-554">A linked service of type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="d46a7-555">Un service lié de type [AzureStorage](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d46a7-555">A linked service of type [AzureStorage](#linked-service-properties).</span></span>
3. <span data-ttu-id="d46a7-556">Un [jeu de données](data-factory-create-datasets.md) d'entrée de type [AzureBlob](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d46a7-556">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](#dataset-properties).</span></span>
4. <span data-ttu-id="d46a7-557">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d46a7-557">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="d46a7-558">Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [BlobSource](#copy-activity-properties) et [SqlSink](data-factory-azure-sql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="d46a7-558">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [BlobSource](#copy-activity-properties) and [SqlSink](data-factory-azure-sql-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="d46a7-559">exemple Hello copie les données de série chronologique dans une table de SQL Azure blob Azure tooan toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="d46a7-559">hello sample copies time-series data from an Azure blob tooan Azure SQL table hourly.</span></span> <span data-ttu-id="d46a7-560">propriétés JSON Hello utilisées dans ces exemples sont décrits dans les sections suivantes des exemples de hello.</span><span class="sxs-lookup"><span data-stu-id="d46a7-560">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="d46a7-561">**Service lié SQL Azure :**</span><span class="sxs-lookup"><span data-stu-id="d46a7-561">**Azure SQL linked service:**</span></span>

```json
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
<span data-ttu-id="d46a7-562">**Service lié Azure Storage :**</span><span class="sxs-lookup"><span data-stu-id="d46a7-562">**Azure Storage linked service:**</span></span>

```json
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
<span data-ttu-id="d46a7-563">Azure Data Factory prend en charge deux types de service lié Azure Storage : **AzureStorage** et **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-563">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="d46a7-564">Pour hello premier, vous spécifiez la chaîne de connexion hello qui inclut la clé de compte hello et pourquoi une version ultérieure, vous spécifiez hello Uri de Signature d’accès partagé (SAS).</span><span class="sxs-lookup"><span data-stu-id="d46a7-564">For hello first one, you specify hello connection string that includes hello account key and for hello later one, you specify hello Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="d46a7-565">Pour plus d’informations, consultez la section [Services liés](#linked-service-properties) .</span><span class="sxs-lookup"><span data-stu-id="d46a7-565">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="d46a7-566">**Jeu de données d'entrée d'objet Blob Azure :**</span><span class="sxs-lookup"><span data-stu-id="d46a7-566">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="d46a7-567">Les données sont récupérées à partir d'un nouvel objet Blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="d46a7-567">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="d46a7-568">nom de chemin d’accès et de dossier pour l’objet blob de hello Hello sont dynamiquement évaluées en fonction de l’heure de début hello de tranche hello qui est en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="d46a7-568">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="d46a7-569">chemin d’accès du dossier Hello utilise la partie jour de l’heure de début hello, mois et année et nom de fichier partie d’heure hello de l’heure de début hello.</span><span class="sxs-lookup"><span data-stu-id="d46a7-569">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="d46a7-570">« external » : « true » paramètre informe Data Factory cette table hello est la fabrique de données externe toohello et n’est pas générée par une activité dans la fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="d46a7-570">“external”: “true” setting informs Data Factory that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" } }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": "\n"
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
<span data-ttu-id="d46a7-571">**Jeu de données de sortie SQL Azure :**</span><span class="sxs-lookup"><span data-stu-id="d46a7-571">**Azure SQL output dataset:**</span></span>

<span data-ttu-id="d46a7-572">exemple Hello copie table tooa de données nommé « MyTable » dans une base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="d46a7-572">hello sample copies data tooa table named “MyTable” in an Azure SQL database.</span></span> <span data-ttu-id="d46a7-573">Créer la table de hello dans votre base de données SQL Azure hello même nombre de colonnes comme vous le souhaitez toocontain de fichier CSV d’objets Blob hello.</span><span class="sxs-lookup"><span data-stu-id="d46a7-573">Create hello table in your Azure SQL database with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="d46a7-574">Nouvelles lignes sont ajoutées à la table de toohello toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="d46a7-574">New rows are added toohello table every hour.</span></span>

```json
{
  "name": "AzureSqlOutput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="d46a7-575">**Activité de copie dans un pipeline avec une source blob et un récepteur SQL :**</span><span class="sxs-lookup"><span data-stu-id="d46a7-575">**A copy activity in a pipeline with Blob source and SQL sink:**</span></span>

<span data-ttu-id="d46a7-576">Hello pipeline contient une activité de copie qui est configuré toouse hello des jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="d46a7-576">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="d46a7-577">Dans la définition JSON du pipeline hello, hello **source** type est défini trop**BlobSource** et **récepteur** type est défini trop**SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-577">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**SqlSink**.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQL",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink"
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
### <a name="json-example-copy-data-from-azure-sql-tooazure-blob"></a><span data-ttu-id="d46a7-578">Exemple de JSON : Copier des données à partir de SQL Azure tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="d46a7-578">JSON Example: Copy data from Azure SQL tooAzure Blob</span></span>
<span data-ttu-id="d46a7-579">Hello ci-dessous illustre d’exemple :</span><span class="sxs-lookup"><span data-stu-id="d46a7-579">hello following sample shows:</span></span>

1. <span data-ttu-id="d46a7-580">Un service lié de type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d46a7-580">A linked service of type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="d46a7-581">Un service lié de type [AzureStorage](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d46a7-581">A linked service of type [AzureStorage](#linked-service-properties).</span></span>
3. <span data-ttu-id="d46a7-582">Un [jeu de données](data-factory-create-datasets.md) d'entrée de type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d46a7-582">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="d46a7-583">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d46a7-583">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](#dataset-properties).</span></span>
5. <span data-ttu-id="d46a7-584">Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [SqlSource](data-factory-azure-sql-connector.md#copy-activity-properties) et [BlobSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="d46a7-584">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [SqlSource](data-factory-azure-sql-connector.md#copy-activity-properties) and [BlobSink](#copy-activity-properties).</span></span>

<span data-ttu-id="d46a7-585">exemple Hello copie toutes les heures des données de séries chronologiques à partir d’un tooan de table SQL Azure blob Azure.</span><span class="sxs-lookup"><span data-stu-id="d46a7-585">hello sample copies time-series data from an Azure SQL table tooan Azure blob hourly.</span></span> <span data-ttu-id="d46a7-586">propriétés JSON Hello utilisées dans ces exemples sont décrits dans les sections suivantes des exemples de hello.</span><span class="sxs-lookup"><span data-stu-id="d46a7-586">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="d46a7-587">**Service lié SQL Azure :**</span><span class="sxs-lookup"><span data-stu-id="d46a7-587">**Azure SQL linked service:**</span></span>

```json
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
<span data-ttu-id="d46a7-588">**Service lié Azure Storage :**</span><span class="sxs-lookup"><span data-stu-id="d46a7-588">**Azure Storage linked service:**</span></span>

```json
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
<span data-ttu-id="d46a7-589">Azure Data Factory prend en charge deux types de service lié Azure Storage : **AzureStorage** et **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-589">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="d46a7-590">Pour hello premier, vous spécifiez la chaîne de connexion hello qui inclut la clé de compte hello et pourquoi une version ultérieure, vous spécifiez hello Uri de Signature d’accès partagé (SAS).</span><span class="sxs-lookup"><span data-stu-id="d46a7-590">For hello first one, you specify hello connection string that includes hello account key and for hello later one, you specify hello Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="d46a7-591">Pour plus d’informations, consultez la section [Services liés](#linked-service-properties) .</span><span class="sxs-lookup"><span data-stu-id="d46a7-591">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="d46a7-592">**Jeu de données d'entrée SQL Azure :**</span><span class="sxs-lookup"><span data-stu-id="d46a7-592">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="d46a7-593">exemple Hello suppose que vous avez créé une table « MyTable » dans SQL Azure, et il contienne une colonne appelée « timestampcolumn » pour les données de série chronologique.</span><span class="sxs-lookup"><span data-stu-id="d46a7-593">hello sample assumes you have created a table “MyTable” in Azure SQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="d46a7-594">Paramètre « external » : « true » informe service Data Factory cette table hello est la fabrique de données externe toohello et n’est pas générée par une activité dans la fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="d46a7-594">Setting “external”: ”true” informs Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
  "name": "AzureSqlInput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
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

<span data-ttu-id="d46a7-595">**Jeu de données de sortie Azure Blob :**</span><span class="sxs-lookup"><span data-stu-id="d46a7-595">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="d46a7-596">Les données sont écrites tooa nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="d46a7-596">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="d46a7-597">chemin d’accès du dossier Hello pour l’objet blob de hello est évaluée dynamiquement en fonction de l’heure de début hello de tranche hello qui est en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="d46a7-597">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="d46a7-598">chemin d’accès du dossier Hello utilise l’année, mois, jours et heures des parties de l’heure de début hello.</span><span class="sxs-lookup"><span data-stu-id="d46a7-598">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}/",
      "partitionedBy": [
        {
          "name": "Year",
          "value": { "type": "DateTime",  "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" } }
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

<span data-ttu-id="d46a7-599">**Activité de copie dans un pipeline avec une source SQL et un récepteur blob :**</span><span class="sxs-lookup"><span data-stu-id="d46a7-599">**A copy activity in a pipeline with SQL source and Blob sink:**</span></span>

<span data-ttu-id="d46a7-600">Hello pipeline contient une activité de copie qui est configuré toouse hello des jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="d46a7-600">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="d46a7-601">Dans la définition JSON du pipeline hello, hello **source** type est défini trop**SqlSource** et **récepteur** type est défini trop**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="d46a7-601">In hello pipeline JSON definition, hello **source** type is set too**SqlSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="d46a7-602">la requête SQL Hello spécifiée pour hello **SqlReaderQuery** propriété sélectionne des données de hello Bonjour au-delà de toocopy d’heure.</span><span class="sxs-lookup"><span data-stu-id="d46a7-602">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
              {
                "name": "AzureSQLtoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureSQLInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureBlobOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "SqlSource",
                        "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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

> [!NOTE]
> <span data-ttu-id="d46a7-603">colonnes de toomap de toocolumns du jeu de données source à partir du jeu de données récepteur, consultez [mappage des colonnes de jeu de données dans Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="d46a7-603">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="d46a7-604">Performances et réglage</span><span class="sxs-lookup"><span data-stu-id="d46a7-604">Performance and Tuning</span></span>
<span data-ttu-id="d46a7-605">Consultez [copie activité optimiser les performances et Guide d’optimisation](data-factory-copy-activity-performance.md) toolearn sur la clé de facteurs d’affecter les performances de transfert de données (activité de copie) dans Azure Data Factory et de différentes façons toooptimize il.</span><span class="sxs-lookup"><span data-stu-id="d46a7-605">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
