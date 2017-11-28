---
title: "les données d’aaaCopy vers/à partir de la base de données SQL Azure | Documents Microsoft"
description: "Découvrez comment les données de toocopy vers/à partir de la base de données SQL Azure à l’aide d’Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 484f735b-8464-40ba-a9fc-820e6553159e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: d2ff16191afb028da75699c5e4d0bb310538db0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-azure-sql-database-using-azure-data-factory"></a><span data-ttu-id="99052-103">Tooand de données de copie à partir de la base de données SQL Azure à l’aide d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="99052-103">Copy data tooand from Azure SQL Database using Azure Data Factory</span></span>
<span data-ttu-id="99052-104">Cet article explique comment toouse hello activité de copie dans Azure Data Factory toomove données tooand à partir de la base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="99052-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data tooand from Azure SQL Database.</span></span> <span data-ttu-id="99052-105">Il repose sur hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, qui présente une vue d’ensemble du déplacement des données avec l’activité de copie hello.</span><span class="sxs-lookup"><span data-stu-id="99052-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>  

## <a name="supported-scenarios"></a><span data-ttu-id="99052-106">Scénarios pris en charge</span><span class="sxs-lookup"><span data-stu-id="99052-106">Supported scenarios</span></span>
<span data-ttu-id="99052-107">Vous pouvez copier des données **à partir de la base de données SQL Azure** toohello suivant des magasins de données :</span><span class="sxs-lookup"><span data-stu-id="99052-107">You can copy data **from Azure SQL Database** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="99052-108">Vous pouvez copier des données à partir de hello suivant des magasins de données **tooAzure base de données SQL**:</span><span class="sxs-lookup"><span data-stu-id="99052-108">You can copy data from hello following data stores **tooAzure SQL Database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-authentication-type"></a><span data-ttu-id="99052-109">Type d’authentification pris en charge</span><span class="sxs-lookup"><span data-stu-id="99052-109">Supported authentication type</span></span>
<span data-ttu-id="99052-110">Le connecteur Azure SQL Database prend en charge l’authentification de base.</span><span class="sxs-lookup"><span data-stu-id="99052-110">Azure SQL Database connector supports basic authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="99052-111">Prise en main</span><span class="sxs-lookup"><span data-stu-id="99052-111">Getting started</span></span>
<span data-ttu-id="99052-112">Vous pouvez créer un pipeline avec une activité de copie qui déplace les données vers/depuis Azure SQL Database à l’aide de différents outils/API.</span><span class="sxs-lookup"><span data-stu-id="99052-112">You can create a pipeline with a copy activity that moves data to/from an Azure SQL Database by using different tools/APIs.</span></span>

<span data-ttu-id="99052-113">toocreate de façon plus simple Hello un pipeline est toouse hello **Assistant copie de**.</span><span class="sxs-lookup"><span data-stu-id="99052-113">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="99052-114">Consultez [didacticiel : créer un pipeline à l’aide d’Assistant copie de](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapides sur la création d’un pipeline à l’aide d’Assistant de données de copie hello.</span><span class="sxs-lookup"><span data-stu-id="99052-114">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="99052-115">Vous pouvez également utiliser hello suivant outils toocreate un pipeline : **portail Azure**, **Visual Studio**, **Azure PowerShell**, **modèle Azure Resource Manager** , **API .NET**, et **API REST**.</span><span class="sxs-lookup"><span data-stu-id="99052-115">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="99052-116">Consultez [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions toocreate un pipeline avec une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="99052-116">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="99052-117">Si vous utilisez hello ou une API, vous effectuez hello suivant les étapes toocreate un pipeline qui déplace la banque de données récepteur tooa du magasin de données à partir des données d’une source :</span><span class="sxs-lookup"><span data-stu-id="99052-117">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="99052-118">Création d'une **fabrique de données**.</span><span class="sxs-lookup"><span data-stu-id="99052-118">Create a **data factory**.</span></span> <span data-ttu-id="99052-119">Une fabrique de données peut contenir un ou plusieurs pipelines.</span><span class="sxs-lookup"><span data-stu-id="99052-119">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="99052-120">Créer **services liés** fabrique de données tooyour toolink les données d’entrée et de sortie magasins.</span><span class="sxs-lookup"><span data-stu-id="99052-120">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="99052-121">Par exemple, si vous copiez des données à partir d’une base de données SQL Azure de tooan stockage blob Azure, vous créez deux services liés toolink votre compte de stockage et de la fabrique de données de tooyour de base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="99052-121">For example, if you are copying data from an Azure blob storage tooan Azure SQL database, you create two linked services toolink your Azure storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="99052-122">Pour les propriétés de service lié sont tooAzure spécifique de la base de données SQL, consultez [lié des propriétés du service](#linked-service-properties) section.</span><span class="sxs-lookup"><span data-stu-id="99052-122">For linked service properties that are specific tooAzure SQL Database, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="99052-123">Créer **datasets** toorepresent d’entrée et sortie l’opération de copie des données pour hello.</span><span class="sxs-lookup"><span data-stu-id="99052-123">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="99052-124">Exemple hello mentionné dans la dernière étape de hello, vous permet de créer un conteneur d’objets blob de jeu de données toospecify hello et un dossier qui contient les données d’entrée hello.</span><span class="sxs-lookup"><span data-stu-id="99052-124">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="99052-125">De plus, vous créez une autre table SQL hello toospecify jeu de données dans la base de données SQL Azure hello qui contient les données hello copiées à partir du stockage d’objets blob hello.</span><span class="sxs-lookup"><span data-stu-id="99052-125">And, you create another dataset toospecify hello SQL table in hello Azure SQL database  that holds hello data copied from hello blob storage.</span></span> <span data-ttu-id="99052-126">Pour les propriétés du dataset qui sont spécifique tooAzure Data Lake Store, consultez [propriétés du dataset](#dataset-properties) section.</span><span class="sxs-lookup"><span data-stu-id="99052-126">For dataset properties that are specific tooAzure Data Lake Store, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="99052-127">Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="99052-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="99052-128">Dans l’exemple hello mentionné précédemment, vous utilisez BlobSource en tant que source et SqlSink comme un récepteur pour l’activité de copie hello.</span><span class="sxs-lookup"><span data-stu-id="99052-128">In hello example mentioned earlier, you use BlobSource as a source and SqlSink as a sink for hello copy activity.</span></span> <span data-ttu-id="99052-129">De même, si vous copiez à partir de la base de données SQL Azure tooAzure stockage d’objets Blob, vous utilisez SqlSource et BlobSink dans l’activité de copie hello.</span><span class="sxs-lookup"><span data-stu-id="99052-129">Similarly, if you are copying from Azure SQL Database tooAzure Blob Storage, you use SqlSource and BlobSink in hello copy activity.</span></span> <span data-ttu-id="99052-130">Pour les propriétés d’activité de copie sont tooAzure spécifique de la base de données SQL, consultez [copier les propriétés de l’activité](#copy-activity-properties) section.</span><span class="sxs-lookup"><span data-stu-id="99052-130">For copy activity properties that are specific tooAzure SQL Database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="99052-131">Pour plus d’informations sur comment toouse du magasin de données source ou un récepteur, cliquez sur le lien hello dans la section précédente de hello pour votre magasin de données.</span><span class="sxs-lookup"><span data-stu-id="99052-131">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>

<span data-ttu-id="99052-132">Lorsque vous utilisez hello Assistant, les définitions de JSON pour ces entités de fabrique de données (services liés, des datasets et pipeline de hello) sont créées automatiquement pour vous.</span><span class="sxs-lookup"><span data-stu-id="99052-132">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="99052-133">Lorsque vous utilisez/API des outils (à l’exception des API .NET), vous définissez ces entités de fabrique de données à l’aide du format JSON de hello.</span><span class="sxs-lookup"><span data-stu-id="99052-133">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="99052-134">Pour plus d’exemples de définitions de JSON pour les entités de fabrique de données qui sont utilisées toocopy des données vers/à partir d’une base de données SQL Azure, consultez [exemples JSON](#json-examples-for-copying-data-to-and-from-sql-database) section de cet article.</span><span class="sxs-lookup"><span data-stu-id="99052-134">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an Azure SQL Database, see [JSON examples](#json-examples-for-copying-data-to-and-from-sql-database) section of this article.</span></span> 

<span data-ttu-id="99052-135">Hello les sections suivantes fournit des détails sur les propriétés JSON qui sont utilisés toodefine Data Factory entités spécifique tooAzure base de données SQL :</span><span class="sxs-lookup"><span data-stu-id="99052-135">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAzure SQL Database:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="99052-136">Propriétés du service lié</span><span class="sxs-lookup"><span data-stu-id="99052-136">Linked service properties</span></span>
<span data-ttu-id="99052-137">SQL Azure lié à des liens de service une fabrique de données de tooyour de base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="99052-137">An Azure SQL linked service links an Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="99052-138">Hello tableau suivant fournit la description pour JSON éléments tooAzure spécifique SQL de service lié.</span><span class="sxs-lookup"><span data-stu-id="99052-138">hello following table provides description for JSON elements specific tooAzure SQL linked service.</span></span>

| <span data-ttu-id="99052-139">Propriété</span><span class="sxs-lookup"><span data-stu-id="99052-139">Property</span></span> | <span data-ttu-id="99052-140">Description</span><span class="sxs-lookup"><span data-stu-id="99052-140">Description</span></span> | <span data-ttu-id="99052-141">Requis</span><span class="sxs-lookup"><span data-stu-id="99052-141">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="99052-142">type</span><span class="sxs-lookup"><span data-stu-id="99052-142">type</span></span> |<span data-ttu-id="99052-143">propriété de type Hello doit indiquer : **AzureSqlDatabase**</span><span class="sxs-lookup"><span data-stu-id="99052-143">hello type property must be set to: **AzureSqlDatabase**</span></span> |<span data-ttu-id="99052-144">Oui</span><span class="sxs-lookup"><span data-stu-id="99052-144">Yes</span></span> |
| <span data-ttu-id="99052-145">connectionString</span><span class="sxs-lookup"><span data-stu-id="99052-145">connectionString</span></span> |<span data-ttu-id="99052-146">Spécifiez les informations nécessaires d’instance de base de données SQL Azure tooconnect toohello pour la propriété connectionString de hello.</span><span class="sxs-lookup"><span data-stu-id="99052-146">Specify information needed tooconnect toohello Azure SQL Database instance for hello connectionString property.</span></span> <span data-ttu-id="99052-147">Seule l’authentification de base est prise en charge.</span><span class="sxs-lookup"><span data-stu-id="99052-147">Only basic authentication is supported.</span></span> |<span data-ttu-id="99052-148">Oui</span><span class="sxs-lookup"><span data-stu-id="99052-148">Yes</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="99052-149">Configurer [pare-feu de base de données SQL Azure](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) hello le serveur de base de données trop[autoriser les Services Azure tooaccess hello serveur](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span><span class="sxs-lookup"><span data-stu-id="99052-149">Configure [Azure SQL Database Firewall](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) hello database server too[allow Azure Services tooaccess hello server](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span></span> <span data-ttu-id="99052-150">En outre, si vous copiez des données tooAzure base de données SQL, notamment Azure externe à partir de sources de données locale avec la passerelle de fabrique de données, configurer la plage d’adresses IP approprié pour l’ordinateur hello qui envoie des données tooAzure base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="99052-150">Additionally, if you are copying data tooAzure SQL Database from outside Azure including from on-premises data sources with data factory gateway, configure appropriate IP address range for hello machine that is sending data tooAzure SQL Database.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="99052-151">Propriétés du jeu de données</span><span class="sxs-lookup"><span data-stu-id="99052-151">Dataset properties</span></span>
<span data-ttu-id="99052-152">toospecify un toorepresent de jeu de données d’entrée ou de sortie des données dans une base de données SQL Azure, que vous définissez propriété hello du jeu de données hello : **AzureSqlTable**.</span><span class="sxs-lookup"><span data-stu-id="99052-152">toospecify a dataset toorepresent input or output data in an Azure SQL database, you set hello type property of hello dataset to: **AzureSqlTable**.</span></span> <span data-ttu-id="99052-153">Ensemble hello **linkedServiceName** service lié de propriété du nom de toohello hello dataset Hello SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="99052-153">Set hello **linkedServiceName** property of hello dataset toohello name of hello Azure SQL linked service.</span></span>  

<span data-ttu-id="99052-154">Pour obtenir une liste complète des sections et les propriétés disponibles pour définir des jeux de données, consultez hello [création de datasets](data-factory-create-datasets.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="99052-154">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="99052-155">Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données (SQL Azure, Azure Blob, Azure Table, etc.).</span><span class="sxs-lookup"><span data-stu-id="99052-155">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="99052-156">section de typeProperties Hello est différente pour chaque type de jeu de données et fournit des informations sur l’emplacement de hello de données hello dans le magasin de données hello.</span><span class="sxs-lookup"><span data-stu-id="99052-156">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="99052-157">Hello **typeProperties** section hello le jeu de données de type **AzureSqlTable** a hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="99052-157">hello **typeProperties** section for hello dataset of type **AzureSqlTable** has hello following properties:</span></span>

| <span data-ttu-id="99052-158">Propriété</span><span class="sxs-lookup"><span data-stu-id="99052-158">Property</span></span> | <span data-ttu-id="99052-159">Description</span><span class="sxs-lookup"><span data-stu-id="99052-159">Description</span></span> | <span data-ttu-id="99052-160">Requis</span><span class="sxs-lookup"><span data-stu-id="99052-160">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="99052-161">TableName</span><span class="sxs-lookup"><span data-stu-id="99052-161">tableName</span></span> |<span data-ttu-id="99052-162">Nom de la table de hello ou la vue d’instance de base de données SQL Azure hello service lié fait référence à.</span><span class="sxs-lookup"><span data-stu-id="99052-162">Name of hello table or view in hello Azure SQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="99052-163">Oui</span><span class="sxs-lookup"><span data-stu-id="99052-163">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="99052-164">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="99052-164">Copy activity properties</span></span>
<span data-ttu-id="99052-165">Pour obtenir une liste complète des sections et les propriétés disponibles pour la définition d’activités, consultez hello [création de Pipelines](data-factory-create-pipelines.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="99052-165">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="99052-166">Les propriétés comme le nom, la description, les tables d’entrée et de sortie et la stratégie sont disponibles pour tous les types d’activités.</span><span class="sxs-lookup"><span data-stu-id="99052-166">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="99052-167">Hello activité de copie accepte uniquement une entrée et produit qu’une seule sortie.</span><span class="sxs-lookup"><span data-stu-id="99052-167">hello Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="99052-168">Tandis que les propriétés disponibles dans hello **typeProperties** section d’activité hello varient selon chaque type d’activité.</span><span class="sxs-lookup"><span data-stu-id="99052-168">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="99052-169">Pour l’activité de copie, ils varient selon les types de sources et récepteurs hello.</span><span class="sxs-lookup"><span data-stu-id="99052-169">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="99052-170">Si vous déplacez des données à partir d’une base de données SQL Azure, vous définissez type de source de hello dans l’activité de copie hello trop**SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="99052-170">If you are moving data from an Azure SQL database, you set hello source type in hello copy activity too**SqlSource**.</span></span> <span data-ttu-id="99052-171">De même, si vous déplacez une base de données SQL Azure données tooan, vous définir le type de récepteur hello dans l’activité de copie hello trop**SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="99052-171">Similarly, if you are moving data tooan Azure SQL database, you set hello sink type in hello copy activity too**SqlSink**.</span></span> <span data-ttu-id="99052-172">Cette section fournit une liste de propriétés prises en charge par SqlSource et SqlSink.</span><span class="sxs-lookup"><span data-stu-id="99052-172">This section provides a list of properties supported by SqlSource and SqlSink.</span></span>

### <a name="sqlsource"></a><span data-ttu-id="99052-173">SqlSource</span><span class="sxs-lookup"><span data-stu-id="99052-173">SqlSource</span></span>
<span data-ttu-id="99052-174">Dans l’activité de copie, lors de la source de hello est de type **SqlSource**, hello propriétés suivantes est disponible dans **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="99052-174">In copy activity, when hello source is of type **SqlSource**, hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="99052-175">Propriété</span><span class="sxs-lookup"><span data-stu-id="99052-175">Property</span></span> | <span data-ttu-id="99052-176">Description</span><span class="sxs-lookup"><span data-stu-id="99052-176">Description</span></span> | <span data-ttu-id="99052-177">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="99052-177">Allowed values</span></span> | <span data-ttu-id="99052-178">Requis</span><span class="sxs-lookup"><span data-stu-id="99052-178">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="99052-179">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="99052-179">sqlReaderQuery</span></span> |<span data-ttu-id="99052-180">Utiliser des données tooread hello requête personnalisée.</span><span class="sxs-lookup"><span data-stu-id="99052-180">Use hello custom query tooread data.</span></span> |<span data-ttu-id="99052-181">Chaîne de requête SQL.</span><span class="sxs-lookup"><span data-stu-id="99052-181">SQL query string.</span></span> <span data-ttu-id="99052-182">Exemple : `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="99052-182">Example: `select * from MyTable`.</span></span> |<span data-ttu-id="99052-183">Non</span><span class="sxs-lookup"><span data-stu-id="99052-183">No</span></span> |
| <span data-ttu-id="99052-184">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="99052-184">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="99052-185">Nom de hello procédure stockée qui lit les données à partir de la table de source de hello.</span><span class="sxs-lookup"><span data-stu-id="99052-185">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="99052-186">Nom de hello procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="99052-186">Name of hello stored procedure.</span></span> <span data-ttu-id="99052-187">instruction SQL de la dernière Hello doit être une instruction SELECT dans la procédure stockée hello.</span><span class="sxs-lookup"><span data-stu-id="99052-187">hello last SQL statement must be a SELECT statement in hello stored procedure.</span></span> |<span data-ttu-id="99052-188">Non</span><span class="sxs-lookup"><span data-stu-id="99052-188">No</span></span> |
| <span data-ttu-id="99052-189">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="99052-189">storedProcedureParameters</span></span> |<span data-ttu-id="99052-190">Pourquoi les paramètres de procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="99052-190">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="99052-191">Paires nom/valeur.</span><span class="sxs-lookup"><span data-stu-id="99052-191">Name/value pairs.</span></span> <span data-ttu-id="99052-192">Noms et la casse des paramètres doivent correspondre à des noms de hello et la casse des paramètres de la procédure stockée hello.</span><span class="sxs-lookup"><span data-stu-id="99052-192">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="99052-193">Non</span><span class="sxs-lookup"><span data-stu-id="99052-193">No</span></span> |

<span data-ttu-id="99052-194">Si hello **sqlReaderQuery** est spécifié pour hello SqlSource, hello activité de copie s’exécute cette requête sur des données hello tooget hello base de données SQL Azure source.</span><span class="sxs-lookup"><span data-stu-id="99052-194">If hello **sqlReaderQuery** is specified for hello SqlSource, hello Copy Activity runs this query against hello Azure SQL Database source tooget hello data.</span></span> <span data-ttu-id="99052-195">Ou bien, vous pouvez spécifier une procédure stockée en spécifiant hello **sqlReaderStoredProcedureName** et **storedProcedureParameters** (si hello une procédure stockée accepte des paramètres).</span><span class="sxs-lookup"><span data-stu-id="99052-195">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>

<span data-ttu-id="99052-196">Si vous ne spécifiez pas de sqlReaderQuery ou sqlReaderStoredProcedureName, les colonnes hello définies dans la section de structure hello du jeu de données hello JSON sont toobuild utilisé une requête (`select column1, column2 from mytable`) toorun contre hello de base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="99052-196">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section of hello dataset JSON are used toobuild a query (`select column1, column2 from mytable`) toorun against hello Azure SQL Database.</span></span> <span data-ttu-id="99052-197">Si la définition de dataset hello n’a pas de structure de hello, toutes les colonnes sont sélectionnées à partir de la table de hello.</span><span class="sxs-lookup"><span data-stu-id="99052-197">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

> [!NOTE]
> <span data-ttu-id="99052-198">Lorsque vous utilisez **sqlReaderStoredProcedureName**, vous devez toujours toospecify une valeur pour hello **tableName** propriété dans le dataset hello JSON.</span><span class="sxs-lookup"><span data-stu-id="99052-198">When you use **sqlReaderStoredProcedureName**, you still need toospecify a value for hello **tableName** property in hello dataset JSON.</span></span> <span data-ttu-id="99052-199">Cependant, il n’existe aucune validation effectuée pour cette table.</span><span class="sxs-lookup"><span data-stu-id="99052-199">There are no validations performed against this table though.</span></span>
>
>

### <a name="sqlsource-example"></a><span data-ttu-id="99052-200">Exemple SqlSource</span><span class="sxs-lookup"><span data-stu-id="99052-200">SqlSource example</span></span>

```JSON
"source": {
    "type": "SqlSource",
    "sqlReaderStoredProcedureName": "CopyTestSrcStoredProcedureWithParameters",
    "storedProcedureParameters": {
        "stringData": { "value": "str3" },
        "identifier": { "value": "$$Text.Format('{0:yyyy}', SliceStart)", "type": "Int"}
    }
}
```

<span data-ttu-id="99052-201">**définition de la procédure stockée Hello :**</span><span class="sxs-lookup"><span data-stu-id="99052-201">**hello stored procedure definition:**</span></span>

```SQL
CREATE PROCEDURE CopyTestSrcStoredProcedureWithParameters
(
    @stringData varchar(20),
    @identifier int
)
AS
SET NOCOUNT ON;
BEGIN
     select *
     from dbo.UnitTestSrcTable
     where dbo.UnitTestSrcTable.stringData != stringData
    and dbo.UnitTestSrcTable.identifier != identifier
END
GO
```

### <a name="sqlsink"></a><span data-ttu-id="99052-202">SqlSink</span><span class="sxs-lookup"><span data-stu-id="99052-202">SqlSink</span></span>
<span data-ttu-id="99052-203">**SqlSink** prend en charge hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="99052-203">**SqlSink** supports hello following properties:</span></span>

| <span data-ttu-id="99052-204">Propriété</span><span class="sxs-lookup"><span data-stu-id="99052-204">Property</span></span> | <span data-ttu-id="99052-205">Description</span><span class="sxs-lookup"><span data-stu-id="99052-205">Description</span></span> | <span data-ttu-id="99052-206">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="99052-206">Allowed values</span></span> | <span data-ttu-id="99052-207">Requis</span><span class="sxs-lookup"><span data-stu-id="99052-207">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="99052-208">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="99052-208">writeBatchTimeout</span></span> |<span data-ttu-id="99052-209">Temps d’attente pour hello lot insert opération toocomplete avant d’expirer.</span><span class="sxs-lookup"><span data-stu-id="99052-209">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="99052-210">intervalle de temps</span><span class="sxs-lookup"><span data-stu-id="99052-210">timespan</span></span><br/><br/> <span data-ttu-id="99052-211">Exemple : « 00:30:00 » (30 minutes).</span><span class="sxs-lookup"><span data-stu-id="99052-211">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="99052-212">Non</span><span class="sxs-lookup"><span data-stu-id="99052-212">No</span></span> |
| <span data-ttu-id="99052-213">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="99052-213">writeBatchSize</span></span> |<span data-ttu-id="99052-214">Insère des données dans une table SQL de hello lorsque la taille de mémoire tampon de hello atteint la valeur writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="99052-214">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="99052-215">Nombre entier (nombre de lignes)</span><span class="sxs-lookup"><span data-stu-id="99052-215">Integer (number of rows)</span></span> |<span data-ttu-id="99052-216">Non (valeur par défaut : 10000)</span><span class="sxs-lookup"><span data-stu-id="99052-216">No (default: 10000)</span></span> |
| <span data-ttu-id="99052-217">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="99052-217">sqlWriterCleanupScript</span></span> |<span data-ttu-id="99052-218">Spécifier une requête pour l’activité de copie tooexecute telles que les données d’un secteur spécifique sont nettoyées.</span><span class="sxs-lookup"><span data-stu-id="99052-218">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="99052-219">Pour en savoir plus, voir [Copie renouvelée](#repeatable-copy).</span><span class="sxs-lookup"><span data-stu-id="99052-219">For more information, see [repeatable copy](#repeatable-copy).</span></span> |<span data-ttu-id="99052-220">Une instruction de requête.</span><span class="sxs-lookup"><span data-stu-id="99052-220">A query statement.</span></span> |<span data-ttu-id="99052-221">Non</span><span class="sxs-lookup"><span data-stu-id="99052-221">No</span></span> |
| <span data-ttu-id="99052-222">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="99052-222">sliceIdentifierColumnName</span></span> |<span data-ttu-id="99052-223">Spécifiez un nom de colonne pour l’activité de copie toofill avec l’identificateur de secteur généré automatiquement, qui est utilisé tooclean des données d’un secteur spécifique quand réexécutée.</span><span class="sxs-lookup"><span data-stu-id="99052-223">Specify a column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> <span data-ttu-id="99052-224">Pour en savoir plus, voir [Copie renouvelée](#repeatable-copy).</span><span class="sxs-lookup"><span data-stu-id="99052-224">For more information, see [repeatable copy](#repeatable-copy).</span></span> |<span data-ttu-id="99052-225">Nom d’une colonne avec le type de données binary(32).</span><span class="sxs-lookup"><span data-stu-id="99052-225">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="99052-226">Non</span><span class="sxs-lookup"><span data-stu-id="99052-226">No</span></span> |
| <span data-ttu-id="99052-227">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="99052-227">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="99052-228">Nom de hello procédure stockée que les données upserts (mises à jour/insertion) dans la table cible hello.</span><span class="sxs-lookup"><span data-stu-id="99052-228">Name of hello stored procedure that upserts (updates/inserts) data into hello target table.</span></span> |<span data-ttu-id="99052-229">Nom de hello procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="99052-229">Name of hello stored procedure.</span></span> |<span data-ttu-id="99052-230">Non</span><span class="sxs-lookup"><span data-stu-id="99052-230">No</span></span> |
| <span data-ttu-id="99052-231">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="99052-231">storedProcedureParameters</span></span> |<span data-ttu-id="99052-232">Pourquoi les paramètres de procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="99052-232">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="99052-233">Paires nom/valeur.</span><span class="sxs-lookup"><span data-stu-id="99052-233">Name/value pairs.</span></span> <span data-ttu-id="99052-234">Noms et la casse des paramètres doivent correspondre à des noms de hello et la casse des paramètres de la procédure stockée hello.</span><span class="sxs-lookup"><span data-stu-id="99052-234">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="99052-235">Non</span><span class="sxs-lookup"><span data-stu-id="99052-235">No</span></span> |
| <span data-ttu-id="99052-236">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="99052-236">sqlWriterTableType</span></span> |<span data-ttu-id="99052-237">Spécifiez un toobe de nom de type de table utilisée dans la procédure stockée hello.</span><span class="sxs-lookup"><span data-stu-id="99052-237">Specify a table type name toobe used in hello stored procedure.</span></span> <span data-ttu-id="99052-238">Activité de copie rend les données de hello déplacées disponibles dans une table temporaire avec ce type de table.</span><span class="sxs-lookup"><span data-stu-id="99052-238">Copy activity makes hello data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="99052-239">Code de procédure stockée puis de fusionner des données hello copiées avec les données existantes.</span><span class="sxs-lookup"><span data-stu-id="99052-239">Stored procedure code can then merge hello data being copied with existing data.</span></span> |<span data-ttu-id="99052-240">Nom de type de table.</span><span class="sxs-lookup"><span data-stu-id="99052-240">A table type name.</span></span> |<span data-ttu-id="99052-241">Non</span><span class="sxs-lookup"><span data-stu-id="99052-241">No</span></span> |

#### <a name="sqlsink-example"></a><span data-ttu-id="99052-242">Exemple SqlSink</span><span class="sxs-lookup"><span data-stu-id="99052-242">SqlSink example</span></span>

```JSON
"sink": {
    "type": "SqlSink",
    "writeBatchSize": 1000000,
    "writeBatchTimeout": "00:05:00",
    "sqlWriterStoredProcedureName": "CopyTestStoredProcedureWithParameters",
    "sqlWriterTableType": "CopyTestTableType",
    "storedProcedureParameters": {
        "identifier": { "value": "1", "type": "Int" },
        "stringData": { "value": "str1" },
        "decimalData": { "value": "1", "type": "Decimal" }
    }
}
```

## <a name="json-examples-for-copying-data-tooand-from-sql-database"></a><span data-ttu-id="99052-243">Exemples JSON pour la copie des données tooand à partir de la base de données SQL</span><span class="sxs-lookup"><span data-stu-id="99052-243">JSON examples for copying data tooand from SQL Database</span></span>
<span data-ttu-id="99052-244">Hello exemples suivants proposent des exemples de définitions de JSON que vous pouvez utiliser toocreate un pipeline à l’aide de [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="99052-244">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="99052-245">Elles montrent comment tooand de données toocopy à partir de la base de données SQL Azure et de stockage d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="99052-245">They show how toocopy data tooand from Azure SQL Database and Azure Blob Storage.</span></span> <span data-ttu-id="99052-246">Toutefois, les données peuvent être copiées **directement** de n’importe quelle tooany de sources de récepteurs hello indiqué [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) à l’aide de hello activité de copie dans Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="99052-246">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-azure-sql-database-tooazure-blob"></a><span data-ttu-id="99052-247">Exemple : Copier des données à partir de la base de données SQL Azure tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="99052-247">Example: Copy data from Azure SQL Database tooAzure Blob</span></span>
<span data-ttu-id="99052-248">Hello même définit hello suivant des entités de fabrique de données :</span><span class="sxs-lookup"><span data-stu-id="99052-248">hello same defines hello following Data Factory entities:</span></span>

1. <span data-ttu-id="99052-249">Un service lié de type [AzureSqlDatabase](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="99052-249">A linked service of type [AzureSqlDatabase](#linked-service-properties).</span></span>
2. <span data-ttu-id="99052-250">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="99052-250">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="99052-251">Un [jeu de données](data-factory-create-datasets.md) d'entrée de type [AzureSqlTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="99052-251">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](#dataset-properties).</span></span>
4. <span data-ttu-id="99052-252">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [Azure Blob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="99052-252">An output [dataset](data-factory-create-datasets.md) of type [Azure Blob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="99052-253">Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [SqlSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="99052-253">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [SqlSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="99052-254">exemple Hello copie les données de série chronologique (horaire, quotidienne, etc.) à partir d’une table dans l’objet blob tooa de base de données SQL Azure toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="99052-254">hello sample copies time-series data (hourly, daily, etc.) from a table in Azure SQL database tooa blob every hour.</span></span> <span data-ttu-id="99052-255">propriétés JSON Hello utilisées dans ces exemples sont décrits dans les sections suivantes des exemples de hello.</span><span class="sxs-lookup"><span data-stu-id="99052-255">hello JSON properties used in these samples are described in sections following hello samples.</span></span>  

<span data-ttu-id="99052-256">**Service lié pour Azure SQL Database :**</span><span class="sxs-lookup"><span data-stu-id="99052-256">**Azure SQL Database linked service:**</span></span>

```JSON
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
<span data-ttu-id="99052-257">Consultez hello [Service lié de SQL Azure](#linked-service) section pour la liste hello des propriétés prises en charge par ce service lié.</span><span class="sxs-lookup"><span data-stu-id="99052-257">See hello [Azure SQL Linked Service](#linked-service) section for hello list of properties supported by this linked service.</span></span>

<span data-ttu-id="99052-258">**Service lié Azure Blob Storage :**</span><span class="sxs-lookup"><span data-stu-id="99052-258">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="99052-259">Consultez hello [objets Blob Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) l’article pour la liste hello de propriétés prises en charge par ce service lié.</span><span class="sxs-lookup"><span data-stu-id="99052-259">See hello [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) article for hello list of properties supported by this linked service.</span></span>


<span data-ttu-id="99052-260">**Jeu de données d'entrée SQL Azure :**</span><span class="sxs-lookup"><span data-stu-id="99052-260">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="99052-261">exemple Hello suppose que vous avez créé une table « MyTable » dans SQL Azure, et il contienne une colonne appelée « timestampcolumn » pour les données de série chronologique.</span><span class="sxs-lookup"><span data-stu-id="99052-261">hello sample assumes you have created a table “MyTable” in Azure SQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="99052-262">Paramètre « external » : « true » informe service Azure Data Factory de hello ce jeu de données hello est la fabrique de données externe toohello et n’est pas généré par une activité dans la fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="99052-262">Setting “external”: ”true” informs hello Azure Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
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

<span data-ttu-id="99052-263">Consultez hello [propriétés de type de jeu de données SQL Azure](#dataset) section pour la liste hello de propriétés prises en charge par ce type de jeu de données.</span><span class="sxs-lookup"><span data-stu-id="99052-263">See hello [Azure SQL dataset type properties](#dataset) section for hello list of properties supported by this dataset type.</span></span>  

<span data-ttu-id="99052-264">**Jeu de données de sortie Azure Blob :**</span><span class="sxs-lookup"><span data-stu-id="99052-264">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="99052-265">Les données sont écrites tooa nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="99052-265">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="99052-266">chemin d’accès du dossier Hello pour l’objet blob de hello est évaluée dynamiquement en fonction de l’heure de début hello de tranche hello qui est en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="99052-266">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="99052-267">chemin d’accès du dossier Hello utilise l’année, mois, jours et heures des parties de l’heure de début hello.</span><span class="sxs-lookup"><span data-stu-id="99052-267">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```JSON
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
<span data-ttu-id="99052-268">Consultez hello [propriétés de type de jeu de données objet Blob Azure](data-factory-azure-blob-connector.md#dataset-properties) section pour la liste hello de propriétés prises en charge par ce type de jeu de données.</span><span class="sxs-lookup"><span data-stu-id="99052-268">See hello [Azure Blob dataset type properties](data-factory-azure-blob-connector.md#dataset-properties) section for hello list of properties supported by this dataset type.</span></span>  

<span data-ttu-id="99052-269">**Activité de copie dans un pipeline avec une source SQL et un récepteur blob :**</span><span class="sxs-lookup"><span data-stu-id="99052-269">**A copy activity in a pipeline with SQL source and Blob sink:**</span></span>

<span data-ttu-id="99052-270">Hello pipeline contient une activité de copie qui est configuré toouse hello des jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="99052-270">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="99052-271">Dans la définition JSON du pipeline hello, hello **source** type est défini trop**SqlSource** et **récepteur** type est défini trop**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="99052-271">In hello pipeline JSON definition, hello **source** type is set too**SqlSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="99052-272">la requête SQL Hello spécifiée pour hello **SqlReaderQuery** propriété sélectionne des données de hello Bonjour au-delà de toocopy d’heure.</span><span class="sxs-lookup"><span data-stu-id="99052-272">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

```JSON
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
<span data-ttu-id="99052-273">Dans l’exemple de hello, **sqlReaderQuery** est spécifié pour hello SqlSource.</span><span class="sxs-lookup"><span data-stu-id="99052-273">In hello example, **sqlReaderQuery** is specified for hello SqlSource.</span></span> <span data-ttu-id="99052-274">Hello activité de copie s’exécute cette requête par rapport à hello données de base de données SQL Azure source tooget hello.</span><span class="sxs-lookup"><span data-stu-id="99052-274">hello Copy Activity runs this query against hello Azure SQL Database source tooget hello data.</span></span> <span data-ttu-id="99052-275">Ou bien, vous pouvez spécifier une procédure stockée en spécifiant hello **sqlReaderStoredProcedureName** et **storedProcedureParameters** (si hello une procédure stockée accepte des paramètres).</span><span class="sxs-lookup"><span data-stu-id="99052-275">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>

<span data-ttu-id="99052-276">Si vous ne spécifiez pas de sqlReaderQuery ou sqlReaderStoredProcedureName, les colonnes de hello définis dans la section de structure hello du jeu de données hello JSON sont utilisé toobuild un toorun de requête par rapport à hello de base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="99052-276">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section of hello dataset JSON are used toobuild a query toorun against hello Azure SQL Database.</span></span> <span data-ttu-id="99052-277">Par exemple : `select column1, column2 from mytable`.</span><span class="sxs-lookup"><span data-stu-id="99052-277">For example: `select column1, column2 from mytable`.</span></span> <span data-ttu-id="99052-278">Si la définition de dataset hello n’a pas de structure de hello, toutes les colonnes sont sélectionnées à partir de la table de hello.</span><span class="sxs-lookup"><span data-stu-id="99052-278">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

<span data-ttu-id="99052-279">Consultez hello [Sql Source](#sqlsource) section et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) pour la liste de propriétés prises en charge par SqlSource et BlobSink hello.</span><span class="sxs-lookup"><span data-stu-id="99052-279">See hello [Sql Source](#sqlsource) section and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) for hello list of properties supported by SqlSource and BlobSink.</span></span>

### <a name="example-copy-data-from-azure-blob-tooazure-sql-database"></a><span data-ttu-id="99052-280">Exemple : Copier des données d’objets Blob Azure tooAzure base de données SQL</span><span class="sxs-lookup"><span data-stu-id="99052-280">Example: Copy data from Azure Blob tooAzure SQL Database</span></span>
<span data-ttu-id="99052-281">exemple Hello définit hello suivant des entités de fabrique de données :</span><span class="sxs-lookup"><span data-stu-id="99052-281">hello sample defines hello following Data Factory entities:</span></span>  

1. <span data-ttu-id="99052-282">Un service lié de type [AzureSqlDatabase](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="99052-282">A linked service of type [AzureSqlDatabase](#linked-service-properties).</span></span>
2. <span data-ttu-id="99052-283">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="99052-283">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="99052-284">Un [jeu de données](data-factory-create-datasets.md) d'entrée de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="99052-284">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="99052-285">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureSqlTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="99052-285">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](#dataset-properties).</span></span>
5. <span data-ttu-id="99052-286">Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) et [SqlSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="99052-286">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlSink](#copy-activity-properties).</span></span>

<span data-ttu-id="99052-287">exemple Hello copie les données de séries chronologiques (horaire, quotidienne, etc.) à partir de la table de tooa d’objets blob Azure dans la base de données SQL Azure toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="99052-287">hello sample copies time-series data (hourly, daily, etc.) from Azure blob tooa table in Azure SQL database every hour.</span></span> <span data-ttu-id="99052-288">propriétés JSON Hello utilisées dans ces exemples sont décrits dans les sections suivantes des exemples de hello.</span><span class="sxs-lookup"><span data-stu-id="99052-288">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="99052-289">**Service lié SQL Azure :**</span><span class="sxs-lookup"><span data-stu-id="99052-289">**Azure SQL linked service:**</span></span>

```JSON
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
<span data-ttu-id="99052-290">Consultez hello [Service lié de SQL Azure](#linked-service) section pour la liste hello des propriétés prises en charge par ce service lié.</span><span class="sxs-lookup"><span data-stu-id="99052-290">See hello [Azure SQL Linked Service](#linked-service) section for hello list of properties supported by this linked service.</span></span>

<span data-ttu-id="99052-291">**Service lié Azure Blob Storage :**</span><span class="sxs-lookup"><span data-stu-id="99052-291">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="99052-292">Consultez hello [objets Blob Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) l’article pour la liste hello de propriétés prises en charge par ce service lié.</span><span class="sxs-lookup"><span data-stu-id="99052-292">See hello [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) article for hello list of properties supported by this linked service.</span></span>


<span data-ttu-id="99052-293">**Jeu de données d'entrée d'objet Blob Azure :**</span><span class="sxs-lookup"><span data-stu-id="99052-293">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="99052-294">Les données sont récupérées à partir d'un nouvel objet Blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="99052-294">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="99052-295">nom de chemin d’accès et de dossier pour l’objet blob de hello Hello sont dynamiquement évaluées en fonction de l’heure de début hello de tranche hello qui est en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="99052-295">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="99052-296">chemin d’accès du dossier Hello utilise la partie jour de l’heure de début hello, mois et année et nom de fichier partie d’heure hello de l’heure de début hello.</span><span class="sxs-lookup"><span data-stu-id="99052-296">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="99052-297">« external » : « true » paramètre informe le service Data Factory de hello que cette table est la fabrique de données externe toohello et qu’il n’est pas générée par une activité dans la fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="99052-297">“external”: “true” setting informs hello Data Factory service that this table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/",
      "fileName": "{Hour}.csv",
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
<span data-ttu-id="99052-298">Consultez hello [propriétés de type de jeu de données objet Blob Azure](data-factory-azure-blob-connector.md#dataset-properties) section pour la liste hello de propriétés prises en charge par ce type de jeu de données.</span><span class="sxs-lookup"><span data-stu-id="99052-298">See hello [Azure Blob dataset type properties](data-factory-azure-blob-connector.md#dataset-properties) section for hello list of properties supported by this dataset type.</span></span>

<span data-ttu-id="99052-299">**Jeu de données de sortie Azure SQL Database :**</span><span class="sxs-lookup"><span data-stu-id="99052-299">**Azure SQL Database output dataset:**</span></span>

<span data-ttu-id="99052-300">exemple Hello copie table tooa de données nommé « MyTable » dans SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="99052-300">hello sample copies data tooa table named “MyTable” in Azure SQL.</span></span> <span data-ttu-id="99052-301">Créer la table de hello dans SQL Azure avec hello même nombre de colonnes comme vous le souhaitez toocontain de fichier CSV d’objets Blob hello.</span><span class="sxs-lookup"><span data-stu-id="99052-301">Create hello table in Azure SQL with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="99052-302">Nouvelles lignes sont ajoutées à la table de toohello toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="99052-302">New rows are added toohello table every hour.</span></span>

```JSON
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
<span data-ttu-id="99052-303">Consultez hello [propriétés de type de jeu de données SQL Azure](#dataset) section pour la liste hello de propriétés prises en charge par ce type de jeu de données.</span><span class="sxs-lookup"><span data-stu-id="99052-303">See hello [Azure SQL dataset type properties](#dataset) section for hello list of properties supported by this dataset type.</span></span>

<span data-ttu-id="99052-304">**Activité de copie dans un pipeline avec une source blob et un récepteur SQL :**</span><span class="sxs-lookup"><span data-stu-id="99052-304">**A copy activity in a pipeline with Blob source and SQL sink:**</span></span>

<span data-ttu-id="99052-305">Hello pipeline contient une activité de copie qui est configuré toouse hello des jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="99052-305">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="99052-306">Dans la définition JSON du pipeline hello, hello **source** type est défini trop**BlobSource** et **récepteur** type est défini trop**SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="99052-306">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**SqlSink**.</span></span>

```JSON
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
            "type": "BlobSource",
            "blobColumnSeparators": ","
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
<span data-ttu-id="99052-307">Consultez hello [Sql récepteur](#sqlsink) section et [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) pour la liste de propriétés prises en charge par SqlSink et BlobSource hello.</span><span class="sxs-lookup"><span data-stu-id="99052-307">See hello [Sql Sink](#sqlsink) section and [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) for hello list of properties supported by SqlSink and BlobSource.</span></span>

## <a name="identity-columns-in-hello-target-database"></a><span data-ttu-id="99052-308">Colonnes d’identité dans la base de données cible hello</span><span class="sxs-lookup"><span data-stu-id="99052-308">Identity columns in hello target database</span></span>
<span data-ttu-id="99052-309">Cette section fournit un exemple de copie de données à partir d’une table source sans une table de destination tooa colonne identité avec une colonne d’identité.</span><span class="sxs-lookup"><span data-stu-id="99052-309">This section provides an example for copying data from a source table without an identity column tooa destination table with an identity column.</span></span>

<span data-ttu-id="99052-310">**Table source :**</span><span class="sxs-lookup"><span data-stu-id="99052-310">**Source table:**</span></span>

```SQL
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
<span data-ttu-id="99052-311">**Table de destination :**</span><span class="sxs-lookup"><span data-stu-id="99052-311">**Destination table:**</span></span>

```SQL
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```
<span data-ttu-id="99052-312">Notez que la table cible hello possède une colonne d’identité.</span><span class="sxs-lookup"><span data-stu-id="99052-312">Notice that hello target table has an identity column.</span></span>

<span data-ttu-id="99052-313">**Définition du jeu de données JSON source**</span><span class="sxs-lookup"><span data-stu-id="99052-313">**Source dataset JSON definition**</span></span>

```JSON
{
    "name": "SampleSource",
    "properties": {
        "type": " SqlServerTable",
        "linkedServiceName": "TestIdentitySQL",
        "typeProperties": {
            "tableName": "SourceTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```
<span data-ttu-id="99052-314">**Définition de jeu de données JSON de destination**</span><span class="sxs-lookup"><span data-stu-id="99052-314">**Destination dataset JSON definition**</span></span>

```JSON
{
    "name": "SampleTarget",
    "properties": {
        "structure": [
            { "name": "name" },
            { "name": "age" }
        ],
        "type": "AzureSqlTable",
        "linkedServiceName": "TestIdentitySQLSource",
        "typeProperties": {
            "tableName": "TargetTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }    
}
```

<span data-ttu-id="99052-315">Notez que vos tables source et cible ont des schémas différents (la cible possède une colonne supplémentaire avec identité).</span><span class="sxs-lookup"><span data-stu-id="99052-315">Notice that as your source and target table have different schema (target has an additional column with identity).</span></span> <span data-ttu-id="99052-316">Dans ce scénario, vous devez toospecify **structure** propriété dans la définition du dataset cible hello, qui n’inclut pas colonne d’identité hello.</span><span class="sxs-lookup"><span data-stu-id="99052-316">In this scenario, you need toospecify **structure** property in hello target dataset definition, which doesn’t include hello identity column.</span></span>

## <a name="invoke-stored-procedure-from-sql-sink"></a><span data-ttu-id="99052-317">Appel d’une procédure stockée pour un récepteur SQL</span><span class="sxs-lookup"><span data-stu-id="99052-317">Invoke stored procedure from SQL sink</span></span>
<span data-ttu-id="99052-318">Pour obtenir un exemple d’appel d’une procédure stockée à partir d’un récepteur SQL dans l’activité de copie d’un pipeline, consultez l’article [Appeler une procédure stockée pour un récepteur SQL dans l’activité de copie](data-factory-invoke-stored-procedure-from-copy-activity.md).</span><span class="sxs-lookup"><span data-stu-id="99052-318">For an example of invoking a stored procedure from SQL sink in a copy activity of a pipeline, see [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) article.</span></span> 

## <a name="type-mapping-for-azure-sql-database"></a><span data-ttu-id="99052-319">Mappage de type pour Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="99052-319">Type mapping for Azure SQL Database</span></span>
<span data-ttu-id="99052-320">Comme mentionné dans hello [les activités de déplacement des données](data-factory-data-movement-activities.md) activité de copie de l’article effectue des conversions de type automatique à partir de types de sources de toosink types avec hello approche de l’étape 2 :</span><span class="sxs-lookup"><span data-stu-id="99052-320">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="99052-321">Convertir à partir de la source native types too.NET type</span><span class="sxs-lookup"><span data-stu-id="99052-321">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="99052-322">Conversion de type de récepteur de toonative de type .NET</span><span class="sxs-lookup"><span data-stu-id="99052-322">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="99052-323">Lorsque vous déplacez des données tooand à partir de la base de données SQL Azure, hello mappages suivants sont utilisés à partir du type too.NET de type SQL et vice versa.</span><span class="sxs-lookup"><span data-stu-id="99052-323">When moving data tooand from Azure SQL Database, hello following mappings are used from SQL type too.NET type and vice versa.</span></span> <span data-ttu-id="99052-324">mappage de Hello est identique à celui hello mappage des types de données SQL Server pour ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="99052-324">hello mapping is same as hello SQL Server Data Type Mapping for ADO.NET.</span></span>

| <span data-ttu-id="99052-325">Type de moteur de base de données SQL Server</span><span class="sxs-lookup"><span data-stu-id="99052-325">SQL Server Database Engine type</span></span> | <span data-ttu-id="99052-326">Type de .NET Framework</span><span class="sxs-lookup"><span data-stu-id="99052-326">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="99052-327">bigint</span><span class="sxs-lookup"><span data-stu-id="99052-327">bigint</span></span> |<span data-ttu-id="99052-328">Int64</span><span class="sxs-lookup"><span data-stu-id="99052-328">Int64</span></span> |
| <span data-ttu-id="99052-329">binaire</span><span class="sxs-lookup"><span data-stu-id="99052-329">binary</span></span> |<span data-ttu-id="99052-330">Byte[]</span><span class="sxs-lookup"><span data-stu-id="99052-330">Byte[]</span></span> |
| <span data-ttu-id="99052-331">bit</span><span class="sxs-lookup"><span data-stu-id="99052-331">bit</span></span> |<span data-ttu-id="99052-332">Boolean</span><span class="sxs-lookup"><span data-stu-id="99052-332">Boolean</span></span> |
| <span data-ttu-id="99052-333">char</span><span class="sxs-lookup"><span data-stu-id="99052-333">char</span></span> |<span data-ttu-id="99052-334">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="99052-334">String, Char[]</span></span> |
| <span data-ttu-id="99052-335">date</span><span class="sxs-lookup"><span data-stu-id="99052-335">date</span></span> |<span data-ttu-id="99052-336">DateTime</span><span class="sxs-lookup"><span data-stu-id="99052-336">DateTime</span></span> |
| <span data-ttu-id="99052-337">DateTime</span><span class="sxs-lookup"><span data-stu-id="99052-337">Datetime</span></span> |<span data-ttu-id="99052-338">DateTime</span><span class="sxs-lookup"><span data-stu-id="99052-338">DateTime</span></span> |
| <span data-ttu-id="99052-339">datetime2</span><span class="sxs-lookup"><span data-stu-id="99052-339">datetime2</span></span> |<span data-ttu-id="99052-340">DateTime</span><span class="sxs-lookup"><span data-stu-id="99052-340">DateTime</span></span> |
| <span data-ttu-id="99052-341">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="99052-341">Datetimeoffset</span></span> |<span data-ttu-id="99052-342">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="99052-342">DateTimeOffset</span></span> |
| <span data-ttu-id="99052-343">Décimal</span><span class="sxs-lookup"><span data-stu-id="99052-343">Decimal</span></span> |<span data-ttu-id="99052-344">Décimal</span><span class="sxs-lookup"><span data-stu-id="99052-344">Decimal</span></span> |
| <span data-ttu-id="99052-345">Attribut FILESTREAM (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="99052-345">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="99052-346">Byte[]</span><span class="sxs-lookup"><span data-stu-id="99052-346">Byte[]</span></span> |
| <span data-ttu-id="99052-347">Float</span><span class="sxs-lookup"><span data-stu-id="99052-347">Float</span></span> |<span data-ttu-id="99052-348">Double</span><span class="sxs-lookup"><span data-stu-id="99052-348">Double</span></span> |
| <span data-ttu-id="99052-349">image</span><span class="sxs-lookup"><span data-stu-id="99052-349">image</span></span> |<span data-ttu-id="99052-350">Byte[]</span><span class="sxs-lookup"><span data-stu-id="99052-350">Byte[]</span></span> |
| <span data-ttu-id="99052-351">int</span><span class="sxs-lookup"><span data-stu-id="99052-351">int</span></span> |<span data-ttu-id="99052-352">Int32</span><span class="sxs-lookup"><span data-stu-id="99052-352">Int32</span></span> |
| <span data-ttu-id="99052-353">money</span><span class="sxs-lookup"><span data-stu-id="99052-353">money</span></span> |<span data-ttu-id="99052-354">Décimal</span><span class="sxs-lookup"><span data-stu-id="99052-354">Decimal</span></span> |
| <span data-ttu-id="99052-355">nchar</span><span class="sxs-lookup"><span data-stu-id="99052-355">nchar</span></span> |<span data-ttu-id="99052-356">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="99052-356">String, Char[]</span></span> |
| <span data-ttu-id="99052-357">ntext</span><span class="sxs-lookup"><span data-stu-id="99052-357">ntext</span></span> |<span data-ttu-id="99052-358">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="99052-358">String, Char[]</span></span> |
| <span data-ttu-id="99052-359">numérique</span><span class="sxs-lookup"><span data-stu-id="99052-359">numeric</span></span> |<span data-ttu-id="99052-360">Décimal</span><span class="sxs-lookup"><span data-stu-id="99052-360">Decimal</span></span> |
| <span data-ttu-id="99052-361">nvarchar</span><span class="sxs-lookup"><span data-stu-id="99052-361">nvarchar</span></span> |<span data-ttu-id="99052-362">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="99052-362">String, Char[]</span></span> |
| <span data-ttu-id="99052-363">real</span><span class="sxs-lookup"><span data-stu-id="99052-363">real</span></span> |<span data-ttu-id="99052-364">Single</span><span class="sxs-lookup"><span data-stu-id="99052-364">Single</span></span> |
| <span data-ttu-id="99052-365">rowversion</span><span class="sxs-lookup"><span data-stu-id="99052-365">rowversion</span></span> |<span data-ttu-id="99052-366">Byte[]</span><span class="sxs-lookup"><span data-stu-id="99052-366">Byte[]</span></span> |
| <span data-ttu-id="99052-367">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="99052-367">smalldatetime</span></span> |<span data-ttu-id="99052-368">DateTime</span><span class="sxs-lookup"><span data-stu-id="99052-368">DateTime</span></span> |
| <span data-ttu-id="99052-369">smallint</span><span class="sxs-lookup"><span data-stu-id="99052-369">smallint</span></span> |<span data-ttu-id="99052-370">Int16</span><span class="sxs-lookup"><span data-stu-id="99052-370">Int16</span></span> |
| <span data-ttu-id="99052-371">smallmoney</span><span class="sxs-lookup"><span data-stu-id="99052-371">smallmoney</span></span> |<span data-ttu-id="99052-372">Décimal</span><span class="sxs-lookup"><span data-stu-id="99052-372">Decimal</span></span> |
| <span data-ttu-id="99052-373">sql_variant</span><span class="sxs-lookup"><span data-stu-id="99052-373">sql_variant</span></span> |<span data-ttu-id="99052-374">Objet *</span><span class="sxs-lookup"><span data-stu-id="99052-374">Object *</span></span> |
| <span data-ttu-id="99052-375">texte</span><span class="sxs-lookup"><span data-stu-id="99052-375">text</span></span> |<span data-ttu-id="99052-376">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="99052-376">String, Char[]</span></span> |
| <span data-ttu-id="99052-377">time</span><span class="sxs-lookup"><span data-stu-id="99052-377">time</span></span> |<span data-ttu-id="99052-378">intervalle de temps</span><span class="sxs-lookup"><span data-stu-id="99052-378">TimeSpan</span></span> |
| <span data-ttu-id="99052-379">timestamp</span><span class="sxs-lookup"><span data-stu-id="99052-379">timestamp</span></span> |<span data-ttu-id="99052-380">Byte[]</span><span class="sxs-lookup"><span data-stu-id="99052-380">Byte[]</span></span> |
| <span data-ttu-id="99052-381">tinyint</span><span class="sxs-lookup"><span data-stu-id="99052-381">tinyint</span></span> |<span data-ttu-id="99052-382">Byte</span><span class="sxs-lookup"><span data-stu-id="99052-382">Byte</span></span> |
| <span data-ttu-id="99052-383">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="99052-383">uniqueidentifier</span></span> |<span data-ttu-id="99052-384">Guid</span><span class="sxs-lookup"><span data-stu-id="99052-384">Guid</span></span> |
| <span data-ttu-id="99052-385">varbinary</span><span class="sxs-lookup"><span data-stu-id="99052-385">varbinary</span></span> |<span data-ttu-id="99052-386">Byte[]</span><span class="sxs-lookup"><span data-stu-id="99052-386">Byte[]</span></span> |
| <span data-ttu-id="99052-387">varchar</span><span class="sxs-lookup"><span data-stu-id="99052-387">varchar</span></span> |<span data-ttu-id="99052-388">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="99052-388">String, Char[]</span></span> |
| <span data-ttu-id="99052-389">xml</span><span class="sxs-lookup"><span data-stu-id="99052-389">xml</span></span> |<span data-ttu-id="99052-390">xml</span><span class="sxs-lookup"><span data-stu-id="99052-390">Xml</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="99052-391">Mapper les colonnes de source toosink</span><span class="sxs-lookup"><span data-stu-id="99052-391">Map source toosink columns</span></span>
<span data-ttu-id="99052-392">toolearn sur le mappage des colonnes dans toocolumns du jeu de données source dans le jeu de données récepteur, consultez [mappage des colonnes de jeu de données dans Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="99052-392">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-copy"></a><span data-ttu-id="99052-393">Copie renouvelée</span><span class="sxs-lookup"><span data-stu-id="99052-393">Repeatable copy</span></span>
<span data-ttu-id="99052-394">Lors de la copie des données tooSQL serveur de base de données, l’activité de copie hello ajoute la table de données toohello récepteur par défaut.</span><span class="sxs-lookup"><span data-stu-id="99052-394">When copying data tooSQL Server Database, hello copy activity appends data toohello sink table by default.</span></span> <span data-ttu-id="99052-395">tooperform UPSERT au lieu de cela, consultez [écriture Repeatable tooSqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) l’article.</span><span class="sxs-lookup"><span data-stu-id="99052-395">tooperform an UPSERT instead,  See [Repeatable write tooSqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) article.</span></span> 

<span data-ttu-id="99052-396">Lors de la copie des données à partir de banques de données relationnelles, conserver la répétabilité dans l’esprit tooavoid des résultats inattendus.</span><span class="sxs-lookup"><span data-stu-id="99052-396">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="99052-397">Dans Azure Data Factory, vous pouvez réexécuter une tranche manuellement.</span><span class="sxs-lookup"><span data-stu-id="99052-397">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="99052-398">Vous pouvez également configurer une stratégie de nouvelles tentatives pour un jeu de données, afin qu’une tranche soit réexécutée en cas de défaillance.</span><span class="sxs-lookup"><span data-stu-id="99052-398">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="99052-399">Lorsqu’une tranche est exécuté à nouveau dans les deux cas, vous devez toomake vraiment qui hello des mêmes données n’est en lecture aucune question comment plusieurs fois une tranche est exécutée.</span><span class="sxs-lookup"><span data-stu-id="99052-399">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="99052-400">Voir [Lecture renouvelée de sources relationnelles](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="99052-400">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="99052-401">Performances et réglage</span><span class="sxs-lookup"><span data-stu-id="99052-401">Performance and Tuning</span></span>
<span data-ttu-id="99052-402">Consultez [copie activité optimiser les performances et Guide d’optimisation](data-factory-copy-activity-performance.md) toolearn sur la clé de facteurs d’affecter les performances de transfert de données (activité de copie) dans Azure Data Factory et de différentes façons toooptimize il.</span><span class="sxs-lookup"><span data-stu-id="99052-402">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
