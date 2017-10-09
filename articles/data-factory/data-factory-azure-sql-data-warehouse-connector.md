---
title: "les données d’aaaCopy vers/à partir de l’entrepôt de données SQL Azure | Documents Microsoft"
description: "Découvrez comment les données de toocopy vers/à partir de l’entrepôt de données SQL Azure à l’aide d’Azure Data Factory"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: d90fa9bd-4b79-458a-8d40-e896835cfd4a
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 75bfcf3c99844fc1297ca500107da23cf875e41f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-azure-sql-data-warehouse-using-azure-data-factory"></a><span data-ttu-id="da6d7-103">Tooand de données de copie à partir de l’entrepôt de données SQL Azure à l’aide d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="da6d7-103">Copy data tooand from Azure SQL Data Warehouse using Azure Data Factory</span></span>
<span data-ttu-id="da6d7-104">Cet article explique comment toouse hello activité de copie de données de toomove Azure Data Factory vers/à partir d’Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="da6d7-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data to/from Azure SQL Data Warehouse.</span></span> <span data-ttu-id="da6d7-105">Il repose sur hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, qui présente une vue d’ensemble du déplacement des données avec l’activité de copie hello.</span><span class="sxs-lookup"><span data-stu-id="da6d7-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>  

> [!TIP]
> <span data-ttu-id="da6d7-106">tooachieve des meilleures performances, utilisez des données de tooload PolyBase dans Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="da6d7-106">tooachieve best performance, use PolyBase tooload data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="da6d7-107">Hello [PolyBase d’utilisation des données de tooload dans Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) section comporte des détails.</span><span class="sxs-lookup"><span data-stu-id="da6d7-107">hello [Use PolyBase tooload data into Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) section has details.</span></span> <span data-ttu-id="da6d7-108">Consultez [Charger 1 To dans Azure SQL Data Warehouse en moins de 15 minutes avec Azure Data Factory](data-factory-load-sql-data-warehouse.md) pour obtenir une procédure pas à pas avec un cas d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="da6d7-108">For a walkthrough with a use case, see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md).</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="da6d7-109">Scénarios pris en charge</span><span class="sxs-lookup"><span data-stu-id="da6d7-109">Supported scenarios</span></span>
<span data-ttu-id="da6d7-110">Vous pouvez copier des données **à partir de l’entrepôt de données SQL Azure** toohello suivant des magasins de données :</span><span class="sxs-lookup"><span data-stu-id="da6d7-110">You can copy data **from Azure SQL Data Warehouse** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="da6d7-111">Vous pouvez copier des données à partir de hello suivant des magasins de données **tooAzure SQL Data Warehouse**:</span><span class="sxs-lookup"><span data-stu-id="da6d7-111">You can copy data from hello following data stores **tooAzure SQL Data Warehouse**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!TIP]
> <span data-ttu-id="da6d7-112">Lors de la copie des données à partir de SQL Server ou la base de données SQL Azure tooAzure SQL Data Warehouse, si la table de hello n’existe pas dans la banque de destination hello, Data Factory peut automatiquement créer les table hello dans l’entrepôt de données SQL à l’aide du schéma hello de table de hello dans la source de hello magasin de données.</span><span class="sxs-lookup"><span data-stu-id="da6d7-112">When copying data from SQL Server or Azure SQL Database tooAzure SQL Data Warehouse, if hello table does not exist in hello destination store, Data Factory can automatically create hello table in SQL Data Warehouse by using hello schema of hello table in hello source data store.</span></span> <span data-ttu-id="da6d7-113">Consultez [Création automatique de la table](#auto-table-creation) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="da6d7-113">See [Auto table creation](#auto-table-creation) for details.</span></span>

## <a name="supported-authentication-type"></a><span data-ttu-id="da6d7-114">Type d’authentification pris en charge</span><span class="sxs-lookup"><span data-stu-id="da6d7-114">Supported authentication type</span></span>
<span data-ttu-id="da6d7-115">Le connecteur Azure SQL Data Warehouse prend en charge l’authentification de base.</span><span class="sxs-lookup"><span data-stu-id="da6d7-115">Azure SQL Data Warehouse connector support basic authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="da6d7-116">Prise en main</span><span class="sxs-lookup"><span data-stu-id="da6d7-116">Getting started</span></span>
<span data-ttu-id="da6d7-117">Vous pouvez créer un pipeline avec une activité de copie qui déplace les données vers/depuis Azure SQL Data Warehouse à l’aide de différents outils/API.</span><span class="sxs-lookup"><span data-stu-id="da6d7-117">You can create a pipeline with a copy activity that moves data to/from an Azure SQL Data Warehouse by using different tools/APIs.</span></span>

<span data-ttu-id="da6d7-118">toocreate de façon plus simple Hello un pipeline qui copie des données vers/depuis Azure SQL Data Warehouse est un Assistant de données copie toouse hello.</span><span class="sxs-lookup"><span data-stu-id="da6d7-118">hello easiest way toocreate a pipeline that copies data to/from Azure SQL Data Warehouse is toouse hello Copy data wizard.</span></span> <span data-ttu-id="da6d7-119">Consultez [didacticiel : charger des données dans l’entrepôt de données SQL avec Data Factory](../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md) pour une procédure pas à pas rapides sur la création d’un pipeline à l’aide d’Assistant de données de copie hello.</span><span class="sxs-lookup"><span data-stu-id="da6d7-119">See [Tutorial: Load data into SQL Data Warehouse with Data Factory](../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="da6d7-120">Vous pouvez également utiliser hello suivant outils toocreate un pipeline : **portail Azure**, **Visual Studio**, **Azure PowerShell**, **modèle Azure Resource Manager** , **API .NET**, et **API REST**.</span><span class="sxs-lookup"><span data-stu-id="da6d7-120">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="da6d7-121">Consultez [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions toocreate un pipeline avec une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="da6d7-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="da6d7-122">Si vous utilisez hello ou une API, vous effectuez hello suivant les étapes toocreate un pipeline qui déplace la banque de données récepteur tooa du magasin de données à partir des données d’une source :</span><span class="sxs-lookup"><span data-stu-id="da6d7-122">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="da6d7-123">Création d'une **fabrique de données**.</span><span class="sxs-lookup"><span data-stu-id="da6d7-123">Create a **data factory**.</span></span> <span data-ttu-id="da6d7-124">Une fabrique de données peut contenir un ou plusieurs pipelines.</span><span class="sxs-lookup"><span data-stu-id="da6d7-124">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="da6d7-125">Créer **services liés** fabrique de données tooyour toolink les données d’entrée et de sortie magasins.</span><span class="sxs-lookup"><span data-stu-id="da6d7-125">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="da6d7-126">Par exemple, si vous copiez des données à partir d’un entrepôt de données objet blob Azure storage tooan SQL Azure, vous créez deux services liés toolink votre compte de stockage Azure et SQL Azure data warehouse tooyour données factory.</span><span class="sxs-lookup"><span data-stu-id="da6d7-126">For example, if you are copying data from an Azure blob storage tooan Azure SQL data warehouse, you create two linked services toolink your Azure storage account and Azure SQL data warehouse tooyour data factory.</span></span> <span data-ttu-id="da6d7-127">Pour les propriétés de service lié qui sont spécifique tooAzure SQL Data Warehouse, consultez [lié des propriétés du service](#linked-service-properties) section.</span><span class="sxs-lookup"><span data-stu-id="da6d7-127">For linked service properties that are specific tooAzure SQL Data Warehouse, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="da6d7-128">Créer **datasets** toorepresent d’entrée et sortie l’opération de copie des données pour hello.</span><span class="sxs-lookup"><span data-stu-id="da6d7-128">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="da6d7-129">Exemple hello mentionné dans la dernière étape de hello, vous permet de créer un conteneur d’objets blob de jeu de données toospecify hello et un dossier qui contient les données d’entrée hello.</span><span class="sxs-lookup"><span data-stu-id="da6d7-129">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="da6d7-130">De plus, vous créez une autre table de hello toospecify jeu de données dans l’entrepôt de données SQL Azure hello qui contient les données hello copiées à partir du stockage d’objets blob hello.</span><span class="sxs-lookup"><span data-stu-id="da6d7-130">And, you create another dataset toospecify hello table in hello Azure SQL data warehouse that holds hello data copied from hello blob storage.</span></span> <span data-ttu-id="da6d7-131">Pour les propriétés du dataset qui sont spécifique tooAzure SQL Data Warehouse, consultez [propriétés du dataset](#dataset-properties) section.</span><span class="sxs-lookup"><span data-stu-id="da6d7-131">For dataset properties that are specific tooAzure SQL Data Warehouse, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="da6d7-132">Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="da6d7-132">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="da6d7-133">Dans l’exemple hello mentionné précédemment, vous utilisez BlobSource en tant que source et SqlDWSink comme un récepteur pour l’activité de copie hello.</span><span class="sxs-lookup"><span data-stu-id="da6d7-133">In hello example mentioned earlier, you use BlobSource as a source and SqlDWSink as a sink for hello copy activity.</span></span> <span data-ttu-id="da6d7-134">De même, si vous copiez à partir de l’entrepôt de données SQL Azure tooAzure stockage d’objets Blob, vous utilisez SqlDWSource et BlobSink dans l’activité de copie hello.</span><span class="sxs-lookup"><span data-stu-id="da6d7-134">Similarly, if you are copying from Azure SQL Data Warehouse tooAzure Blob Storage, you use SqlDWSource and BlobSink in hello copy activity.</span></span> <span data-ttu-id="da6d7-135">Pour les propriétés d’activité de copie sont tooAzure spécifique SQL Data Warehouse, consultez [copier les propriétés de l’activité](#copy-activity-properties) section.</span><span class="sxs-lookup"><span data-stu-id="da6d7-135">For copy activity properties that are specific tooAzure SQL Data Warehouse, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="da6d7-136">Pour plus d’informations sur comment toouse du magasin de données source ou un récepteur, cliquez sur le lien hello dans la section précédente de hello pour votre magasin de données.</span><span class="sxs-lookup"><span data-stu-id="da6d7-136">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>

<span data-ttu-id="da6d7-137">Lorsque vous utilisez hello Assistant, les définitions de JSON pour ces entités de fabrique de données (services liés, des datasets et pipeline de hello) sont créées automatiquement pour vous.</span><span class="sxs-lookup"><span data-stu-id="da6d7-137">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="da6d7-138">Lorsque vous utilisez/API des outils (à l’exception des API .NET), vous définissez ces entités de fabrique de données à l’aide du format JSON de hello.</span><span class="sxs-lookup"><span data-stu-id="da6d7-138">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="da6d7-139">Pour plus d’exemples de définitions de JSON pour les entités de fabrique de données qui sont utilisées toocopy des données vers/à partir d’un entrepôt de données SQL Azure, consultez [exemples JSON](#json-examples-for-copying-data-to-and-from-sql-data-warehouse) section de cet article.</span><span class="sxs-lookup"><span data-stu-id="da6d7-139">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an Azure SQL Data Warehouse, see [JSON examples](#json-examples-for-copying-data-to-and-from-sql-data-warehouse) section of this article.</span></span>

<span data-ttu-id="da6d7-140">Hello les sections suivantes fournit des détails sur les propriétés JSON qui sont utilisés toodefine Data Factory entités spécifique tooAzure SQL Data Warehouse :</span><span class="sxs-lookup"><span data-stu-id="da6d7-140">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAzure SQL Data Warehouse:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="da6d7-141">Propriétés du service lié</span><span class="sxs-lookup"><span data-stu-id="da6d7-141">Linked service properties</span></span>
<span data-ttu-id="da6d7-142">Hello tableau suivant fournit la description pour JSON éléments tooAzure spécifique service d’entrepôt de données SQL lié.</span><span class="sxs-lookup"><span data-stu-id="da6d7-142">hello following table provides description for JSON elements specific tooAzure SQL Data Warehouse linked service.</span></span>

| <span data-ttu-id="da6d7-143">Propriété</span><span class="sxs-lookup"><span data-stu-id="da6d7-143">Property</span></span> | <span data-ttu-id="da6d7-144">Description</span><span class="sxs-lookup"><span data-stu-id="da6d7-144">Description</span></span> | <span data-ttu-id="da6d7-145">Requis</span><span class="sxs-lookup"><span data-stu-id="da6d7-145">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="da6d7-146">type</span><span class="sxs-lookup"><span data-stu-id="da6d7-146">type</span></span> |<span data-ttu-id="da6d7-147">propriété de type Hello doit indiquer : **AzureSqlDW**</span><span class="sxs-lookup"><span data-stu-id="da6d7-147">hello type property must be set to: **AzureSqlDW**</span></span> |<span data-ttu-id="da6d7-148">Oui</span><span class="sxs-lookup"><span data-stu-id="da6d7-148">Yes</span></span> |
| <span data-ttu-id="da6d7-149">connectionString</span><span class="sxs-lookup"><span data-stu-id="da6d7-149">connectionString</span></span> |<span data-ttu-id="da6d7-150">Spécifiez les informations nécessaires d’instance d’Azure SQL Data Warehouse tooconnect toohello pour la propriété connectionString de hello.</span><span class="sxs-lookup"><span data-stu-id="da6d7-150">Specify information needed tooconnect toohello Azure SQL Data Warehouse instance for hello connectionString property.</span></span> <span data-ttu-id="da6d7-151">Seule l’authentification de base est prise en charge.</span><span class="sxs-lookup"><span data-stu-id="da6d7-151">Only basic authentication is supported.</span></span> |<span data-ttu-id="da6d7-152">Oui</span><span class="sxs-lookup"><span data-stu-id="da6d7-152">Yes</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="da6d7-153">Configurer [pare-feu de base de données SQL Azure](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) et hello le serveur de base de données trop[autoriser les Services Azure tooaccess hello serveur](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span><span class="sxs-lookup"><span data-stu-id="da6d7-153">Configure [Azure SQL Database Firewall](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) and hello database server too[allow Azure Services tooaccess hello server](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span></span> <span data-ttu-id="da6d7-154">En outre, si vous copiez des données tooAzure SQL Data Warehouse, notamment Azure externe à partir de sources de données locale avec la passerelle de fabrique de données, configurer la plage d’adresses IP approprié pour l’ordinateur hello qui envoie des données tooAzure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="da6d7-154">Additionally, if you are copying data tooAzure SQL Data Warehouse from outside Azure including from on-premises data sources with data factory gateway, configure appropriate IP address range for hello machine that is sending data tooAzure SQL Data Warehouse.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="da6d7-155">Propriétés du jeu de données</span><span class="sxs-lookup"><span data-stu-id="da6d7-155">Dataset properties</span></span>
<span data-ttu-id="da6d7-156">Pour obtenir une liste complète des sections et les propriétés disponibles pour définir des jeux de données, consultez hello [création de datasets](data-factory-create-datasets.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="da6d7-156">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="da6d7-157">Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données (SQL Azure, Azure Blob, Azure Table, etc.).</span><span class="sxs-lookup"><span data-stu-id="da6d7-157">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="da6d7-158">section de typeProperties Hello est différente pour chaque type de jeu de données et fournit des informations sur l’emplacement de hello de données hello dans le magasin de données hello.</span><span class="sxs-lookup"><span data-stu-id="da6d7-158">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="da6d7-159">Hello **typeProperties** section hello le jeu de données de type **AzureSqlDWTable** a hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="da6d7-159">hello **typeProperties** section for hello dataset of type **AzureSqlDWTable** has hello following properties:</span></span>

| <span data-ttu-id="da6d7-160">Propriété</span><span class="sxs-lookup"><span data-stu-id="da6d7-160">Property</span></span> | <span data-ttu-id="da6d7-161">Description</span><span class="sxs-lookup"><span data-stu-id="da6d7-161">Description</span></span> | <span data-ttu-id="da6d7-162">Requis</span><span class="sxs-lookup"><span data-stu-id="da6d7-162">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="da6d7-163">TableName</span><span class="sxs-lookup"><span data-stu-id="da6d7-163">tableName</span></span> |<span data-ttu-id="da6d7-164">Nom de la table de hello ou une vue dans la base de données Azure SQL Data Warehouse hello qui hello service lié fait référence à.</span><span class="sxs-lookup"><span data-stu-id="da6d7-164">Name of hello table or view in hello Azure SQL Data Warehouse database that hello linked service refers to.</span></span> |<span data-ttu-id="da6d7-165">Oui</span><span class="sxs-lookup"><span data-stu-id="da6d7-165">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="da6d7-166">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="da6d7-166">Copy activity properties</span></span>
<span data-ttu-id="da6d7-167">Pour obtenir une liste complète des sections et les propriétés disponibles pour la définition d’activités, consultez hello [création de Pipelines](data-factory-create-pipelines.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="da6d7-167">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="da6d7-168">Les propriétés comme le nom, la description, les tables d’entrée et de sortie et la stratégie sont disponibles pour tous les types d’activités.</span><span class="sxs-lookup"><span data-stu-id="da6d7-168">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="da6d7-169">Hello activité de copie accepte uniquement une entrée et produit qu’une seule sortie.</span><span class="sxs-lookup"><span data-stu-id="da6d7-169">hello Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="da6d7-170">Alors que les propriétés disponibles dans la section typeProperties hello activité hello varient selon chaque type d’activité.</span><span class="sxs-lookup"><span data-stu-id="da6d7-170">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="da6d7-171">Pour l’activité de copie, ils varient selon les types de sources et récepteurs hello.</span><span class="sxs-lookup"><span data-stu-id="da6d7-171">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

### <a name="sqldwsource"></a><span data-ttu-id="da6d7-172">SqlDWSource</span><span class="sxs-lookup"><span data-stu-id="da6d7-172">SqlDWSource</span></span>
<span data-ttu-id="da6d7-173">Lorsque la source est de type **SqlDWSource**, hello propriétés suivantes est disponible dans **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="da6d7-173">When source is of type **SqlDWSource**, hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="da6d7-174">Propriété</span><span class="sxs-lookup"><span data-stu-id="da6d7-174">Property</span></span> | <span data-ttu-id="da6d7-175">Description</span><span class="sxs-lookup"><span data-stu-id="da6d7-175">Description</span></span> | <span data-ttu-id="da6d7-176">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="da6d7-176">Allowed values</span></span> | <span data-ttu-id="da6d7-177">Requis</span><span class="sxs-lookup"><span data-stu-id="da6d7-177">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="da6d7-178">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="da6d7-178">sqlReaderQuery</span></span> |<span data-ttu-id="da6d7-179">Utiliser des données tooread hello requête personnalisée.</span><span class="sxs-lookup"><span data-stu-id="da6d7-179">Use hello custom query tooread data.</span></span> |<span data-ttu-id="da6d7-180">Chaîne de requête SQL.</span><span class="sxs-lookup"><span data-stu-id="da6d7-180">SQL query string.</span></span> <span data-ttu-id="da6d7-181">Par exemple : select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="da6d7-181">For example: select * from MyTable.</span></span> |<span data-ttu-id="da6d7-182">Non</span><span class="sxs-lookup"><span data-stu-id="da6d7-182">No</span></span> |
| <span data-ttu-id="da6d7-183">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="da6d7-183">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="da6d7-184">Nom de hello procédure stockée qui lit les données à partir de la table de source de hello.</span><span class="sxs-lookup"><span data-stu-id="da6d7-184">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="da6d7-185">Nom de hello procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="da6d7-185">Name of hello stored procedure.</span></span> <span data-ttu-id="da6d7-186">instruction SQL de la dernière Hello doit être une instruction SELECT dans la procédure stockée hello.</span><span class="sxs-lookup"><span data-stu-id="da6d7-186">hello last SQL statement must be a SELECT statement in hello stored procedure.</span></span> |<span data-ttu-id="da6d7-187">Non</span><span class="sxs-lookup"><span data-stu-id="da6d7-187">No</span></span> |
| <span data-ttu-id="da6d7-188">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="da6d7-188">storedProcedureParameters</span></span> |<span data-ttu-id="da6d7-189">Pourquoi les paramètres de procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="da6d7-189">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="da6d7-190">Paires nom/valeur.</span><span class="sxs-lookup"><span data-stu-id="da6d7-190">Name/value pairs.</span></span> <span data-ttu-id="da6d7-191">Noms et la casse des paramètres doivent correspondre à des noms de hello et la casse des paramètres de la procédure stockée hello.</span><span class="sxs-lookup"><span data-stu-id="da6d7-191">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="da6d7-192">Non</span><span class="sxs-lookup"><span data-stu-id="da6d7-192">No</span></span> |

<span data-ttu-id="da6d7-193">Si hello **sqlReaderQuery** est spécifié pour hello SqlDWSource, hello activité de copie s’exécute cette requête par rapport à hello données de Azure SQL Data Warehouse source tooget hello.</span><span class="sxs-lookup"><span data-stu-id="da6d7-193">If hello **sqlReaderQuery** is specified for hello SqlDWSource, hello Copy Activity runs this query against hello Azure SQL Data Warehouse source tooget hello data.</span></span>

<span data-ttu-id="da6d7-194">Ou bien, vous pouvez spécifier une procédure stockée en spécifiant hello **sqlReaderStoredProcedureName** et **storedProcedureParameters** (si hello une procédure stockée accepte des paramètres).</span><span class="sxs-lookup"><span data-stu-id="da6d7-194">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>

<span data-ttu-id="da6d7-195">Si vous ne spécifiez pas de sqlReaderQuery ou sqlReaderStoredProcedureName, les colonnes de hello définis dans la section de structure hello du jeu de données hello JSON sont utilisé toobuild un toorun de requête par rapport à hello Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="da6d7-195">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section of hello dataset JSON are used toobuild a query toorun against hello Azure SQL Data Warehouse.</span></span> <span data-ttu-id="da6d7-196">Exemple : `select column1, column2 from mytable`.</span><span class="sxs-lookup"><span data-stu-id="da6d7-196">Example: `select column1, column2 from mytable`.</span></span> <span data-ttu-id="da6d7-197">Si la définition de dataset hello n’a pas de structure de hello, toutes les colonnes sont sélectionnées à partir de la table de hello.</span><span class="sxs-lookup"><span data-stu-id="da6d7-197">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

#### <a name="sqldwsource-example"></a><span data-ttu-id="da6d7-198">Exemple SqlDWSource</span><span class="sxs-lookup"><span data-stu-id="da6d7-198">SqlDWSource example</span></span>

```JSON
"source": {
    "type": "SqlDWSource",
    "sqlReaderStoredProcedureName": "CopyTestSrcStoredProcedureWithParameters",
    "storedProcedureParameters": {
        "stringData": { "value": "str3" },
        "identifier": { "value": "$$Text.Format('{0:yyyy}', SliceStart)", "type": "Int"}
    }
}
```
<span data-ttu-id="da6d7-199">**définition de la procédure stockée Hello :**</span><span class="sxs-lookup"><span data-stu-id="da6d7-199">**hello stored procedure definition:**</span></span>

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

### <a name="sqldwsink"></a><span data-ttu-id="da6d7-200">SqlDWSink</span><span class="sxs-lookup"><span data-stu-id="da6d7-200">SqlDWSink</span></span>
<span data-ttu-id="da6d7-201">**SqlDWSink** prend en charge hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="da6d7-201">**SqlDWSink** supports hello following properties:</span></span>

| <span data-ttu-id="da6d7-202">Propriété</span><span class="sxs-lookup"><span data-stu-id="da6d7-202">Property</span></span> | <span data-ttu-id="da6d7-203">Description</span><span class="sxs-lookup"><span data-stu-id="da6d7-203">Description</span></span> | <span data-ttu-id="da6d7-204">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="da6d7-204">Allowed values</span></span> | <span data-ttu-id="da6d7-205">Requis</span><span class="sxs-lookup"><span data-stu-id="da6d7-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="da6d7-206">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="da6d7-206">sqlWriterCleanupScript</span></span> |<span data-ttu-id="da6d7-207">Spécifier une requête pour l’activité de copie tooexecute telles que les données d’un secteur spécifique sont nettoyées.</span><span class="sxs-lookup"><span data-stu-id="da6d7-207">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="da6d7-208">Consultez la [section sur la répétition](#repeatability-during-copy)pour plus de détails.</span><span class="sxs-lookup"><span data-stu-id="da6d7-208">For details, see [repeatability section](#repeatability-during-copy).</span></span> |<span data-ttu-id="da6d7-209">Une instruction de requête.</span><span class="sxs-lookup"><span data-stu-id="da6d7-209">A query statement.</span></span> |<span data-ttu-id="da6d7-210">Non</span><span class="sxs-lookup"><span data-stu-id="da6d7-210">No</span></span> |
| <span data-ttu-id="da6d7-211">allowPolyBase</span><span class="sxs-lookup"><span data-stu-id="da6d7-211">allowPolyBase</span></span> |<span data-ttu-id="da6d7-212">Indique si toouse PolyBase (le cas échéant) au lieu de mécanisme BULKINSERT.</span><span class="sxs-lookup"><span data-stu-id="da6d7-212">Indicates whether toouse PolyBase (when applicable) instead of BULKINSERT mechanism.</span></span> <br/><br/> <span data-ttu-id="da6d7-213">**À l’aide de PolyBase est hello recommandé la façon dont les données tooload dans SQL Data Warehouse.**</span><span class="sxs-lookup"><span data-stu-id="da6d7-213">**Using PolyBase is hello recommended way tooload data into SQL Data Warehouse.**</span></span> <span data-ttu-id="da6d7-214">Consultez [PolyBase d’utilisation des données de tooload dans Azure SQL Data Warehouse](#use-polybase-to-load-data-into-azure-sql-data-warehouse) section pour les contraintes et les détails.</span><span class="sxs-lookup"><span data-stu-id="da6d7-214">See [Use PolyBase tooload data into Azure SQL Data Warehouse](#use-polybase-to-load-data-into-azure-sql-data-warehouse) section for constraints and details.</span></span> |<span data-ttu-id="da6d7-215">true</span><span class="sxs-lookup"><span data-stu-id="da6d7-215">True</span></span> <br/><span data-ttu-id="da6d7-216">False (valeur par défaut)</span><span class="sxs-lookup"><span data-stu-id="da6d7-216">False (default)</span></span> |<span data-ttu-id="da6d7-217">Non</span><span class="sxs-lookup"><span data-stu-id="da6d7-217">No</span></span> |
| <span data-ttu-id="da6d7-218">polyBaseSettings</span><span class="sxs-lookup"><span data-stu-id="da6d7-218">polyBaseSettings</span></span> |<span data-ttu-id="da6d7-219">Un groupe de propriétés qui peuvent être spécifiés lorsque hello **allowPolybase** propriété a la valeur trop**true**.</span><span class="sxs-lookup"><span data-stu-id="da6d7-219">A group of properties that can be specified when hello **allowPolybase** property is set too**true**.</span></span> |&nbsp; |<span data-ttu-id="da6d7-220">Non</span><span class="sxs-lookup"><span data-stu-id="da6d7-220">No</span></span> |
| <span data-ttu-id="da6d7-221">rejectValue</span><span class="sxs-lookup"><span data-stu-id="da6d7-221">rejectValue</span></span> |<span data-ttu-id="da6d7-222">Spécifie le nombre de hello ou un pourcentage de lignes peut être rejetée avant l’échec de la requête de hello.</span><span class="sxs-lookup"><span data-stu-id="da6d7-222">Specifies hello number or percentage of rows that can be rejected before hello query fails.</span></span> <br/><br/><span data-ttu-id="da6d7-223">En savoir plus sur de PolyBase hello rejettent options Bonjour **Arguments** section de [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) rubrique.</span><span class="sxs-lookup"><span data-stu-id="da6d7-223">Learn more about hello PolyBase’s reject options in hello **Arguments** section of [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) topic.</span></span> |<span data-ttu-id="da6d7-224">0 (par défaut), 1, 2, …</span><span class="sxs-lookup"><span data-stu-id="da6d7-224">0 (default), 1, 2, …</span></span> |<span data-ttu-id="da6d7-225">Non</span><span class="sxs-lookup"><span data-stu-id="da6d7-225">No</span></span> |
| <span data-ttu-id="da6d7-226">rejectType</span><span class="sxs-lookup"><span data-stu-id="da6d7-226">rejectType</span></span> |<span data-ttu-id="da6d7-227">Spécifie si l’option de rejectValue hello est spécifiée comme une valeur littérale ou pourcentage.</span><span class="sxs-lookup"><span data-stu-id="da6d7-227">Specifies whether hello rejectValue option is specified as a literal value or a percentage.</span></span> |<span data-ttu-id="da6d7-228">Value (par défaut), Percentage</span><span class="sxs-lookup"><span data-stu-id="da6d7-228">Value (default), Percentage</span></span> |<span data-ttu-id="da6d7-229">Non</span><span class="sxs-lookup"><span data-stu-id="da6d7-229">No</span></span> |
| <span data-ttu-id="da6d7-230">rejectSampleValue</span><span class="sxs-lookup"><span data-stu-id="da6d7-230">rejectSampleValue</span></span> |<span data-ttu-id="da6d7-231">Détermine le nombre hello de lignes tooretrieve avant hello PolyBase recalcule le pourcentage de hello de lignes rejetées.</span><span class="sxs-lookup"><span data-stu-id="da6d7-231">Determines hello number of rows tooretrieve before hello PolyBase recalculates hello percentage of rejected rows.</span></span> |<span data-ttu-id="da6d7-232">1, 2, …</span><span class="sxs-lookup"><span data-stu-id="da6d7-232">1, 2, …</span></span> |<span data-ttu-id="da6d7-233">Oui, si le **rejectType** est **percentage**</span><span class="sxs-lookup"><span data-stu-id="da6d7-233">Yes, if **rejectType** is **percentage**</span></span> |
| <span data-ttu-id="da6d7-234">useTypeDefault</span><span class="sxs-lookup"><span data-stu-id="da6d7-234">useTypeDefault</span></span> |<span data-ttu-id="da6d7-235">Spécifie comment toohandle manque des valeurs dans le fichiers texte délimités lorsque PolyBase récupère les données à partir du fichier de texte hello.</span><span class="sxs-lookup"><span data-stu-id="da6d7-235">Specifies how toohandle missing values in delimited text files when PolyBase retrieves data from hello text file.</span></span><br/><br/><span data-ttu-id="da6d7-236">En savoir plus sur cette propriété à partir de la section Arguments hello [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span><span class="sxs-lookup"><span data-stu-id="da6d7-236">Learn more about this property from hello Arguments section in [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span></span> |<span data-ttu-id="da6d7-237">True, False (par défaut)</span><span class="sxs-lookup"><span data-stu-id="da6d7-237">True, False (default)</span></span> |<span data-ttu-id="da6d7-238">Non</span><span class="sxs-lookup"><span data-stu-id="da6d7-238">No</span></span> |
| <span data-ttu-id="da6d7-239">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="da6d7-239">writeBatchSize</span></span> |<span data-ttu-id="da6d7-240">Insère des données dans une table SQL de hello lorsque la taille de mémoire tampon de hello atteint la valeur writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="da6d7-240">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize</span></span> |<span data-ttu-id="da6d7-241">Nombre entier (nombre de lignes)</span><span class="sxs-lookup"><span data-stu-id="da6d7-241">Integer (number of rows)</span></span> |<span data-ttu-id="da6d7-242">Non (valeur par défaut : 10000)</span><span class="sxs-lookup"><span data-stu-id="da6d7-242">No (default: 10000)</span></span> |
| <span data-ttu-id="da6d7-243">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="da6d7-243">writeBatchTimeout</span></span> |<span data-ttu-id="da6d7-244">Temps d’attente pour hello lot insert opération toocomplete avant d’expirer.</span><span class="sxs-lookup"><span data-stu-id="da6d7-244">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="da6d7-245">intervalle de temps</span><span class="sxs-lookup"><span data-stu-id="da6d7-245">timespan</span></span><br/><br/> <span data-ttu-id="da6d7-246">Exemple : « 00:30:00 » (30 minutes).</span><span class="sxs-lookup"><span data-stu-id="da6d7-246">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="da6d7-247">Non</span><span class="sxs-lookup"><span data-stu-id="da6d7-247">No</span></span> |

#### <a name="sqldwsink-example"></a><span data-ttu-id="da6d7-248">Exemple SqlDWSink</span><span class="sxs-lookup"><span data-stu-id="da6d7-248">SqlDWSink example</span></span>

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true
}
```

## <a name="use-polybase-tooload-data-into-azure-sql-data-warehouse"></a><span data-ttu-id="da6d7-249">Utiliser des données de tooload PolyBase dans Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="da6d7-249">Use PolyBase tooload data into Azure SQL Data Warehouse</span></span>
<span data-ttu-id="da6d7-250">L’utilisation de **[PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)** est un moyen efficace de charger de grandes quantités de données dans Azure SQL Data Warehouse avec un débit élevé.</span><span class="sxs-lookup"><span data-stu-id="da6d7-250">Using **[PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)** is an efficient way of loading large amount of data into Azure SQL Data Warehouse with high throughput.</span></span> <span data-ttu-id="da6d7-251">Vous pouvez voir un grand gain un débit hello à l’aide de PolyBase au lieu de mécanisme BULKINSERT hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="da6d7-251">You can see a large gain in hello throughput by using PolyBase instead of hello default BULKINSERT mechanism.</span></span> <span data-ttu-id="da6d7-252">Consultez [copier le numéro de référence des performances](data-factory-copy-activity-performance.md#performance-reference) qui contient une comparaison détaillée.</span><span class="sxs-lookup"><span data-stu-id="da6d7-252">See [copy performance reference number](data-factory-copy-activity-performance.md#performance-reference) with detailed comparison.</span></span> <span data-ttu-id="da6d7-253">Consultez [Charger 1 To dans Azure SQL Data Warehouse en moins de 15 minutes avec Azure Data Factory](data-factory-load-sql-data-warehouse.md) pour obtenir une procédure pas à pas avec un cas d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="da6d7-253">For a walkthrough with a use case, see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md).</span></span>

* <span data-ttu-id="da6d7-254">Si votre source de données se trouve dans **objets Blob Azure ou Azure Data Lake Store**et format de hello est compatible avec PolyBase, vous pouvez copier directement tooAzure SQL Data Warehouse à l’aide de PolyBase.</span><span class="sxs-lookup"><span data-stu-id="da6d7-254">If your source data is in **Azure Blob or Azure Data Lake Store**, and hello format is compatible with PolyBase, you can directly copy tooAzure SQL Data Warehouse using PolyBase.</span></span> <span data-ttu-id="da6d7-255">Consultez **[Copie directe à l’aide de PolyBase](#direct-copy-using-polybase)**.</span><span class="sxs-lookup"><span data-stu-id="da6d7-255">See **[Direct copy using PolyBase](#direct-copy-using-polybase)** with details.</span></span>
* <span data-ttu-id="da6d7-256">Si votre magasin de données source et le format n'est pas à l’origine PolyBase prend en charge, vous pouvez utiliser hello  **[copie intermédiaire à l’aide de PolyBase](#staged-copy-using-polybase)**  fonctionnalité à la place.</span><span class="sxs-lookup"><span data-stu-id="da6d7-256">If your source data store and format is not originally supported by PolyBase, you can use hello **[Staged Copy using PolyBase](#staged-copy-using-polybase)** feature instead.</span></span> <span data-ttu-id="da6d7-257">Il fournit également un meilleur débit conversion des données de hello en format compatible avec PolyBase et le stockage des données de hello dans le stockage d’objets Blob Azure automatiquement.</span><span class="sxs-lookup"><span data-stu-id="da6d7-257">It also provides you better throughput by automatically converting hello data into PolyBase-compatible format and storing hello data in Azure Blob storage.</span></span> <span data-ttu-id="da6d7-258">Il charge ensuite les données dans SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="da6d7-258">It then loads data into SQL Data Warehouse.</span></span>

<span data-ttu-id="da6d7-259">Ensemble hello `allowPolyBase` propriété trop**true** comme indiqué dans hello suivant l’exemple pour Azure Data Factory toouse PolyBase toocopy données dans Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="da6d7-259">Set hello `allowPolyBase` property too**true** as shown in hello following example for Azure Data Factory toouse PolyBase toocopy data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="da6d7-260">Lorsque vous définissez allowPolyBase tootrue, vous pouvez spécifier les propriétés spécifiques de PolyBase à l’aide de hello `polyBaseSettings` groupe de propriétés.</span><span class="sxs-lookup"><span data-stu-id="da6d7-260">When you set allowPolyBase tootrue, you can specify PolyBase specific properties using hello `polyBaseSettings` property group.</span></span> <span data-ttu-id="da6d7-261">consultez hello [SqlDWSink](#SqlDWSink) pour plus d’informations sur les propriétés que vous pouvez utiliser avec polyBaseSettings.</span><span class="sxs-lookup"><span data-stu-id="da6d7-261">see hello [SqlDWSink](#SqlDWSink) section for details about properties that you can use with polyBaseSettings.</span></span>

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true,
    "polyBaseSettings":
    {
        "rejectType": "percentage",
        "rejectValue": 10.0,
        "rejectSampleValue": 100,
        "useTypeDefault": true
    }
}
```

### <a name="direct-copy-using-polybase"></a><span data-ttu-id="da6d7-262">Copie directe à l’aide de PolyBase</span><span class="sxs-lookup"><span data-stu-id="da6d7-262">Direct copy using PolyBase</span></span>
<span data-ttu-id="da6d7-263">SQL Data Warehouse PolyBase prend directement en charge Stockage Blob Azure et Azure Data Lake Store (à l’aide du principal du service) en tant que source et avec des exigences de format de fichier spécifiques.</span><span class="sxs-lookup"><span data-stu-id="da6d7-263">SQL Data Warehouse PolyBase directly support Azure Blob and Azure Data Lake Store (using service principal) as source and with specific file format requirements.</span></span> <span data-ttu-id="da6d7-264">Si votre source de données répond aux critères de hello décrits dans cette section, vous pouvez copier directement à partir de tooAzure de magasin de données source que SQL Data Warehouse à l’aide de PolyBase.</span><span class="sxs-lookup"><span data-stu-id="da6d7-264">If your source data meets hello criteria described in this section, you can directly copy from source data store tooAzure SQL Data Warehouse using PolyBase.</span></span> <span data-ttu-id="da6d7-265">Sinon, vous pouvez utiliser la méthode [Copie intermédiaire à l’aide de PolyBase](#staged-copy-using-polybase).</span><span class="sxs-lookup"><span data-stu-id="da6d7-265">Otherwise, you can use [Staged Copy using PolyBase](#staged-copy-using-polybase).</span></span>

> [!TIP]
> <span data-ttu-id="da6d7-266">données toocopy Data Lake Store tooSQL l’entrepôt de données efficace, pour en savoir plus à partir de [Azure Data Factory permet même de vos données toouncover plus facile et pratique lors de l’utilisation de Data Lake Store avec l’entrepôt de données SQL](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/).</span><span class="sxs-lookup"><span data-stu-id="da6d7-266">toocopy data from Data Lake Store tooSQL Data Warehouse efficiently, learn more from [Azure Data Factory makes it even easier and convenient toouncover insights from data when using Data Lake Store with SQL Data Warehouse](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/).</span></span>

<span data-ttu-id="da6d7-267">Si les exigences de hello ne sont pas remplies, Azure Data Factory vérifie les paramètres de hello et repasse automatiquement mécanisme BULKINSERT toohello hello déplacement des données.</span><span class="sxs-lookup"><span data-stu-id="da6d7-267">If hello requirements are not met, Azure Data Factory checks hello settings and automatically falls back toohello BULKINSERT mechanism for hello data movement.</span></span>

1. <span data-ttu-id="da6d7-268">Le **service lié de la source** est de type : **AzureStorage** ou **AzureDataLakeStore avec authentification du principal de service**.</span><span class="sxs-lookup"><span data-stu-id="da6d7-268">**Source linked service** is of type: **AzureStorage** or **AzureDataLakeStore with service principal authentication**.</span></span>  
2. <span data-ttu-id="da6d7-269">Hello **dataset d’entrée** est de type : **AzureBlob** ou **AzureDataLakeStore**, et hello du type de format sous `type` propriétés est **OrcFormat** , ou **TextFormat** avec hello suivant configurations :</span><span class="sxs-lookup"><span data-stu-id="da6d7-269">hello **input dataset** is of type: **AzureBlob** or **AzureDataLakeStore**, and hello format type under `type` properties is **OrcFormat**, or **TextFormat** with hello following configurations:</span></span>

   1. <span data-ttu-id="da6d7-270">`rowDelimiter` doit être **\n**.</span><span class="sxs-lookup"><span data-stu-id="da6d7-270">`rowDelimiter` must be **\n**.</span></span>
   2. <span data-ttu-id="da6d7-271">`nullValue`est défini trop**une chaîne vide** (« »), ou `treatEmptyAsNull` est défini trop**true**.</span><span class="sxs-lookup"><span data-stu-id="da6d7-271">`nullValue` is set too**empty string** (""), or `treatEmptyAsNull` is set too**true**.</span></span>
   3. <span data-ttu-id="da6d7-272">`encodingName`est défini trop**utf-8**, qui est **par défaut** valeur.</span><span class="sxs-lookup"><span data-stu-id="da6d7-272">`encodingName` is set too**utf-8**, which is **default** value.</span></span>
   4. <span data-ttu-id="da6d7-273">`escapeChar`, `quoteChar`, `firstRowAsHeader` et `skipLineCount` ne sont pas spécifiés.</span><span class="sxs-lookup"><span data-stu-id="da6d7-273">`escapeChar`, `quoteChar`, `firstRowAsHeader`, and `skipLineCount` are not specified.</span></span>
   5. <span data-ttu-id="da6d7-274">`compression` peut être **aucune compression**, **GZip** ou **Deflate**.</span><span class="sxs-lookup"><span data-stu-id="da6d7-274">`compression` can be **no compression**, **GZip**, or **Deflate**.</span></span>

    ```JSON
    "typeProperties": {
       "folderPath": "<blobpath>",
       "format": {
           "type": "TextFormat",     
           "columnDelimiter": "<any delimiter>",
           "rowDelimiter": "\n",       
           "nullValue": "",           
           "encodingName": "utf-8"    
       },
       "compression": {  
           "type": "GZip",  
           "level": "Optimal"  
       }  
    },
    ```

3. <span data-ttu-id="da6d7-275">Il est sans `skipHeaderLineCount` sous **BlobSource** ou **AzureDataLakeStore** pourquoi l’activité de copie dans le pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="da6d7-275">There is no `skipHeaderLineCount` setting under **BlobSource** or **AzureDataLakeStore** for hello Copy activity in hello pipeline.</span></span>
4. <span data-ttu-id="da6d7-276">Il est sans `sliceIdentifierColumnName` sous **SqlDWSink** pourquoi l’activité de copie dans le pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="da6d7-276">There is no `sliceIdentifierColumnName` setting under **SqlDWSink** for hello Copy activity in hello pipeline.</span></span> <span data-ttu-id="da6d7-277">(PolyBase garantit que toutes les données sont mises à jour ou que rien n’est mis à jour en une seule exécution.</span><span class="sxs-lookup"><span data-stu-id="da6d7-277">(PolyBase guarantees that all data is updated or nothing is updated in a single run.</span></span> <span data-ttu-id="da6d7-278">tooachieve **répétabilité**, vous pouvez utiliser `sqlWriterCleanupScript`).</span><span class="sxs-lookup"><span data-stu-id="da6d7-278">tooachieve **repeatability**, you could use `sqlWriterCleanupScript`).</span></span>
5. <span data-ttu-id="da6d7-279">Il existe aucune `columnMapping` utilisé Bonjour associé dans l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="da6d7-279">There is no `columnMapping` being used in hello associated in Copy activity.</span></span>

### <a name="staged-copy-using-polybase"></a><span data-ttu-id="da6d7-280">Copie intermédiaire à l’aide de PolyBase</span><span class="sxs-lookup"><span data-stu-id="da6d7-280">Staged Copy using PolyBase</span></span>
<span data-ttu-id="da6d7-281">Lorsque vos données sources ne répond pas aux critères de hello introduites dans la section précédente de hello, vous pouvez activer la copie des données via un stockage d’objets Blob Azure mise en lots intermédiaire (ne peut pas être le stockage Premium).</span><span class="sxs-lookup"><span data-stu-id="da6d7-281">When your source data doesn’t meet hello criteria introduced in hello previous section, you can enable copying data via an interim staging Azure Blob Storage (cannot be Premium Storage).</span></span> <span data-ttu-id="da6d7-282">Dans ce cas, Azure Data Factory automatiquement effectue les transformations sur hello données toomeet données exigences relatives au format de PolyBase, puis utilisez PolyBase tooload données dans l’entrepôt de données SQL et enfin nettoyage vos données temporaires de stockage d’objets Blob hello.</span><span class="sxs-lookup"><span data-stu-id="da6d7-282">In this case, Azure Data Factory automatically performs transformations on hello data toomeet data format requirements of PolyBase, then use PolyBase tooload data into SQL Data Warehouse, and at last clean-up your temp data from hello Blob storage.</span></span> <span data-ttu-id="da6d7-283">Consultez la rubrique [Copie intermédiaire](data-factory-copy-activity-performance.md#staged-copy) pour plus d’informations sur le fonctionnement général de la copie des données par le biais d’un Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="da6d7-283">See [Staged Copy](data-factory-copy-activity-performance.md#staged-copy) for details on how copying data via a staging Azure Blob works in general.</span></span>

> [!NOTE]
> <span data-ttu-id="da6d7-284">Stocke une copie de données à partir d’un local de données dans Azure SQL Data Warehouse à l’aide de PolyBase et de mise en lots, si votre version de la passerelle de gestion des données est inférieur à 2.4, JRE (Java Runtime Environment) est requis sur votre passerelle lors de l’ordinateur qui est utilisé tootransform vos données sources dans le format approprié.</span><span class="sxs-lookup"><span data-stu-id="da6d7-284">When copying data from an on-prem data store into Azure SQL Data Warehouse using PolyBase and staging, if your Data Management Gateway version is below 2.4, JRE (Java Runtime Environment) is required on your gateway machine that is used tootransform your source data into proper format.</span></span> <span data-ttu-id="da6d7-285">Suggérer que vous mettez à niveau votre tooavoid de dernière toohello passerelle telle dépendance.</span><span class="sxs-lookup"><span data-stu-id="da6d7-285">Suggest you upgrade your gateway toohello latest tooavoid such dependency.</span></span>
>

<span data-ttu-id="da6d7-286">toouse cette fonctionnalité, créez un [service lié Azure Storage](data-factory-azure-blob-connector.md#azure-storage-linked-service) qui fait référence toohello compte de stockage Azure ayant un stockage temporaire blob hello, puis spécifiez hello `enableStaging` et `stagingSettings` propriétés pourquoi l’activité de copie comme indiqué dans hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="da6d7-286">toouse this feature, create an [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) that refers toohello Azure Storage Account that has hello interim blob storage, then specify hello `enableStaging` and `stagingSettings` properties for hello Copy Activity as shown in hello following code:</span></span>

```json
"activities":[  
{
    "name": "Sample copy activity from SQL Server tooSQL Data Warehouse via PolyBase",
    "type": "Copy",
    "inputs": [{ "name": "OnpremisesSQLServerInput" }],
    "outputs": [{ "name": "AzureSQLDWOutput" }],
    "typeProperties": {
        "source": {
            "type": "SqlSource",
        },
        "sink": {
            "type": "SqlDwSink",
            "allowPolyBase": true
        },
        "enableStaging": true,
        "stagingSettings": {
            "linkedServiceName": "MyStagingBlob"
        }
    }
}
]
```

## <a name="best-practices-when-using-polybase"></a><span data-ttu-id="da6d7-287">Meilleures pratiques lors de l’utilisation de PolyBase</span><span class="sxs-lookup"><span data-stu-id="da6d7-287">Best practices when using PolyBase</span></span>
<span data-ttu-id="da6d7-288">Hello sections suivantes fournissent plus toohello pratiques meilleures ceux qui sont mentionnés dans [meilleures pratiques pour Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="da6d7-288">hello following sections provide additional best practices toohello ones that are mentioned in [Best practices for Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md).</span></span>

### <a name="required-database-permission"></a><span data-ttu-id="da6d7-289">Autorisation de base de données requise</span><span class="sxs-lookup"><span data-stu-id="da6d7-289">Required database permission</span></span>
<span data-ttu-id="da6d7-290">toouse PolyBase, il requiert hello utilisateur en cours données tooload utilisés dans SQL Data Warehouse a hello [l’autorisation « Contrôle »](https://msdn.microsoft.com/library/ms191291.aspx) sur la base de données cible hello.</span><span class="sxs-lookup"><span data-stu-id="da6d7-290">toouse PolyBase, it requires hello user being used tooload data into SQL Data Warehouse has hello ["CONTROL" permission](https://msdn.microsoft.com/library/ms191291.aspx) on hello target database.</span></span> <span data-ttu-id="da6d7-291">Une façon tooachieve qui est tooadd cet utilisateur en tant que membre du rôle « db_owner ».</span><span class="sxs-lookup"><span data-stu-id="da6d7-291">One way tooachieve that is tooadd that user as a member of "db_owner" role.</span></span> <span data-ttu-id="da6d7-292">Découvrez comment toodo qui en suivant [cette section](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization).</span><span class="sxs-lookup"><span data-stu-id="da6d7-292">Learn how toodo that by following [this section](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization).</span></span>

### <a name="row-size-and-data-type-limitation"></a><span data-ttu-id="da6d7-293">Limitations en matière de taille de ligne et de type de données</span><span class="sxs-lookup"><span data-stu-id="da6d7-293">Row size and data type limitation</span></span>
<span data-ttu-id="da6d7-294">Polybase charges sont limités tooloading lignes à la fois plus petit que **1 Mo** et ne peut pas charger tooVARCHR(MAX), nvarchar (max) ou varbinary (max).</span><span class="sxs-lookup"><span data-stu-id="da6d7-294">Polybase loads are limited tooloading rows both smaller than **1 MB** and cannot load tooVARCHR(MAX), NVARCHAR(MAX) or VARBINARY(MAX).</span></span> <span data-ttu-id="da6d7-295">Consultez trop[ici](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads).</span><span class="sxs-lookup"><span data-stu-id="da6d7-295">Refer too[here](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads).</span></span>

<span data-ttu-id="da6d7-296">Si vous avez des données sources avec des lignes d’une taille supérieure à 1 Mo, vous souhaiterez les tables sources toosplit hello verticalement en plusieurs petits où hello plus grande taille de ligne de chacun d’eux ne dépasse pas la limite de hello.</span><span class="sxs-lookup"><span data-stu-id="da6d7-296">If you have source data with rows of size greater than 1 MB, you may want toosplit hello source tables vertically into several small ones where hello largest row size of each of them does not exceed hello limit.</span></span> <span data-ttu-id="da6d7-297">les tables plus petites Hello peuvent ensuite être chargées à l’aide de PolyBase et fusionnées dans l’entrepôt de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="da6d7-297">hello smaller tables can then be loaded using PolyBase and merged together in Azure SQL Data Warehouse.</span></span>

### <a name="sql-data-warehouse-resource-class"></a><span data-ttu-id="da6d7-298">Classe de ressources SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="da6d7-298">SQL Data Warehouse resource class</span></span>
<span data-ttu-id="da6d7-299">tooachieve meilleurs résultats possibles, envisagez de tooassign plus grande ressource classe toohello utilisateur en cours utilisé les données tooload dans l’entrepôt de données SQL via PolyBase.</span><span class="sxs-lookup"><span data-stu-id="da6d7-299">tooachieve best possible throughput, consider tooassign larger resource class toohello user being used tooload data into SQL Data Warehouse via PolyBase.</span></span> <span data-ttu-id="da6d7-300">Découvrez comment toodo qui en suivant [modifier un exemple de classe de ressource utilisateur](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="da6d7-300">Learn how toodo that by following [Change a user resource class example](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>

### <a name="tablename-in-azure-sql-data-warehouse"></a><span data-ttu-id="da6d7-301">tableName dans Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="da6d7-301">tableName in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="da6d7-302">Hello tableau suivant fournit des exemples sur la façon de toospecify hello **tableName** propriété dans le jeu de données JSON pour différentes combinaisons de nom de schéma et une table.</span><span class="sxs-lookup"><span data-stu-id="da6d7-302">hello following table provides examples on how toospecify hello **tableName** property in dataset JSON for various combinations of schema and table name.</span></span>

| <span data-ttu-id="da6d7-303">Schéma BD</span><span class="sxs-lookup"><span data-stu-id="da6d7-303">DB Schema</span></span> | <span data-ttu-id="da6d7-304">Nom de la table</span><span class="sxs-lookup"><span data-stu-id="da6d7-304">Table name</span></span> | <span data-ttu-id="da6d7-305">Propriété JSON tableName</span><span class="sxs-lookup"><span data-stu-id="da6d7-305">tableName JSON property</span></span> |
| --- | --- | --- |
| <span data-ttu-id="da6d7-306">dbo</span><span class="sxs-lookup"><span data-stu-id="da6d7-306">dbo</span></span> |<span data-ttu-id="da6d7-307">MyTable</span><span class="sxs-lookup"><span data-stu-id="da6d7-307">MyTable</span></span> |<span data-ttu-id="da6d7-308">MyTable ou dbo.MyTable ou [dbo].[MyTable]</span><span class="sxs-lookup"><span data-stu-id="da6d7-308">MyTable or dbo.MyTable or [dbo].[MyTable]</span></span> |
| <span data-ttu-id="da6d7-309">dbo1</span><span class="sxs-lookup"><span data-stu-id="da6d7-309">dbo1</span></span> |<span data-ttu-id="da6d7-310">MyTable</span><span class="sxs-lookup"><span data-stu-id="da6d7-310">MyTable</span></span> |<span data-ttu-id="da6d7-311">dbo1.MyTable ou [dbo1].[MyTable]</span><span class="sxs-lookup"><span data-stu-id="da6d7-311">dbo1.MyTable or [dbo1].[MyTable]</span></span> |
| <span data-ttu-id="da6d7-312">dbo</span><span class="sxs-lookup"><span data-stu-id="da6d7-312">dbo</span></span> |<span data-ttu-id="da6d7-313">My.Table</span><span class="sxs-lookup"><span data-stu-id="da6d7-313">My.Table</span></span> |<span data-ttu-id="da6d7-314">[My.Table] ou [dbo].[My.Table]</span><span class="sxs-lookup"><span data-stu-id="da6d7-314">[My.Table] or [dbo].[My.Table]</span></span> |
| <span data-ttu-id="da6d7-315">dbo1</span><span class="sxs-lookup"><span data-stu-id="da6d7-315">dbo1</span></span> |<span data-ttu-id="da6d7-316">My.Table</span><span class="sxs-lookup"><span data-stu-id="da6d7-316">My.Table</span></span> |<span data-ttu-id="da6d7-317">[dbo1].[My.Table]</span><span class="sxs-lookup"><span data-stu-id="da6d7-317">[dbo1].[My.Table]</span></span> |

<span data-ttu-id="da6d7-318">Si vous voyez hello l’erreur suivante, il peut être un problème avec la valeur hello spécifiée pour la propriété tableName de hello.</span><span class="sxs-lookup"><span data-stu-id="da6d7-318">If you see hello following error, it could be an issue with hello value you specified for hello tableName property.</span></span> <span data-ttu-id="da6d7-319">Consultez la table hello pour les valeurs de toospecify hello méthode correcte pour la propriété JSON tableName hello.</span><span class="sxs-lookup"><span data-stu-id="da6d7-319">See hello table for hello correct way toospecify values for hello tableName JSON property.</span></span>  

```
Type=System.Data.SqlClient.SqlException,Message=Invalid object name 'stg.Account_test'.,Source=.Net SqlClient Data Provider
```

### <a name="columns-with-default-values"></a><span data-ttu-id="da6d7-320">Colonnes avec des valeurs par défaut</span><span class="sxs-lookup"><span data-stu-id="da6d7-320">Columns with default values</span></span>
<span data-ttu-id="da6d7-321">Actuellement, PolyBase accepte uniquement les fonctionnalités dans la fabrique de données hello même nombre de colonnes dans la table cible hello.</span><span class="sxs-lookup"><span data-stu-id="da6d7-321">Currently, PolyBase feature in Data Factory only accepts hello same number of columns as in hello target table.</span></span> <span data-ttu-id="da6d7-322">Par exemple, vous avez une table avec quatre colonnes et l’une d’elles est définie avec une valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="da6d7-322">Say, you have a table with four columns and one of them is defined with a default value.</span></span> <span data-ttu-id="da6d7-323">les données d’entrée Hello doivent toujours contenir des quatre colonnes.</span><span class="sxs-lookup"><span data-stu-id="da6d7-323">hello input data should still contain four columns.</span></span> <span data-ttu-id="da6d7-324">En fournissant un jeu de données d’entrée 3-colonne produirait un toohello similaire erreur message suivant :</span><span class="sxs-lookup"><span data-stu-id="da6d7-324">Providing a 3-column input dataset would yield an error similar toohello following message:</span></span>

```
All columns of hello table must be specified in hello INSERT BULK statement.
```
<span data-ttu-id="da6d7-325">La valeur NULL est une forme spéciale de valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="da6d7-325">NULL value is a special form of default value.</span></span> <span data-ttu-id="da6d7-326">Si la colonne de hello est nullable, données d’entrée hello (dans l’objet blob) pour cette colonne peut être vides (ne peut pas être manquant à partir du jeu de données d’entrée hello).</span><span class="sxs-lookup"><span data-stu-id="da6d7-326">If hello column is nullable, hello input data (in blob) for that column could be empty (cannot be missing from hello input dataset).</span></span> <span data-ttu-id="da6d7-327">PolyBase insère NULL pour les Bonjour Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="da6d7-327">PolyBase inserts NULL for them in hello Azure SQL Data Warehouse.</span></span>  

## <a name="auto-table-creation"></a><span data-ttu-id="da6d7-328">Création automatique de la table</span><span class="sxs-lookup"><span data-stu-id="da6d7-328">Auto table creation</span></span>
<span data-ttu-id="da6d7-329">Si vous utilisez des données de toocopy Assistant copie de SQL Server ou de base de données SQL Azure tooAzure SQL Data Warehouse et hello la table qui correspond la table de source toohello n’existe pas dans la banque de destination hello, Data Factory peut créer automatiquement la table de hello Bonjour entrepôt de données à l’aide du schéma de la table source hello.</span><span class="sxs-lookup"><span data-stu-id="da6d7-329">If you are using Copy Wizard toocopy data from SQL Server or Azure SQL Database tooAzure SQL Data Warehouse and hello table that corresponds toohello source table does not exist in hello destination store, Data Factory can automatically create hello table in hello data warehouse by using hello source table schema.</span></span>

<span data-ttu-id="da6d7-330">Fabrique de données crée la table de hello dans la banque de destination hello avec hello même nom dans le magasin de données source hello de la table.</span><span class="sxs-lookup"><span data-stu-id="da6d7-330">Data Factory creates hello table in hello destination store with hello same table name in hello source data store.</span></span> <span data-ttu-id="da6d7-331">types de données Hello pour les colonnes sont choisies en fonction hello suivant le mappage de type.</span><span class="sxs-lookup"><span data-stu-id="da6d7-331">hello data types for columns are chosen based on hello following type mapping.</span></span> <span data-ttu-id="da6d7-332">Si nécessaire, il effectue toofix des conversions de type les incompatibilités entre les magasins de source et de destination.</span><span class="sxs-lookup"><span data-stu-id="da6d7-332">If needed, it performs type conversions toofix any incompatibilities between source and destination stores.</span></span> <span data-ttu-id="da6d7-333">Il utilise également la distribution de tables en tourniquet (Round Robin).</span><span class="sxs-lookup"><span data-stu-id="da6d7-333">It also uses Round Robin table distribution.</span></span>

| <span data-ttu-id="da6d7-334">Type de colonne SQL Database source</span><span class="sxs-lookup"><span data-stu-id="da6d7-334">Source SQL Database column type</span></span> | <span data-ttu-id="da6d7-335">Type de colonne SQL DW de destination (limite de taille)</span><span class="sxs-lookup"><span data-stu-id="da6d7-335">Destination SQL DW column type (size limitation)</span></span> |
| --- | --- |
| <span data-ttu-id="da6d7-336">int</span><span class="sxs-lookup"><span data-stu-id="da6d7-336">Int</span></span> | <span data-ttu-id="da6d7-337">int</span><span class="sxs-lookup"><span data-stu-id="da6d7-337">Int</span></span> |
| <span data-ttu-id="da6d7-338">BigInt</span><span class="sxs-lookup"><span data-stu-id="da6d7-338">BigInt</span></span> | <span data-ttu-id="da6d7-339">BigInt</span><span class="sxs-lookup"><span data-stu-id="da6d7-339">BigInt</span></span> |
| <span data-ttu-id="da6d7-340">SmallInt</span><span class="sxs-lookup"><span data-stu-id="da6d7-340">SmallInt</span></span> | <span data-ttu-id="da6d7-341">SmallInt</span><span class="sxs-lookup"><span data-stu-id="da6d7-341">SmallInt</span></span> |
| <span data-ttu-id="da6d7-342">TinyInt</span><span class="sxs-lookup"><span data-stu-id="da6d7-342">TinyInt</span></span> | <span data-ttu-id="da6d7-343">TinyInt</span><span class="sxs-lookup"><span data-stu-id="da6d7-343">TinyInt</span></span> |
| <span data-ttu-id="da6d7-344">Bit</span><span class="sxs-lookup"><span data-stu-id="da6d7-344">Bit</span></span> | <span data-ttu-id="da6d7-345">Bit</span><span class="sxs-lookup"><span data-stu-id="da6d7-345">Bit</span></span> |
| <span data-ttu-id="da6d7-346">Décimal</span><span class="sxs-lookup"><span data-stu-id="da6d7-346">Decimal</span></span> | <span data-ttu-id="da6d7-347">Décimal</span><span class="sxs-lookup"><span data-stu-id="da6d7-347">Decimal</span></span> |
| <span data-ttu-id="da6d7-348">Chiffre</span><span class="sxs-lookup"><span data-stu-id="da6d7-348">Numeric</span></span> | <span data-ttu-id="da6d7-349">Décimal</span><span class="sxs-lookup"><span data-stu-id="da6d7-349">Decimal</span></span> |
| <span data-ttu-id="da6d7-350">Float</span><span class="sxs-lookup"><span data-stu-id="da6d7-350">Float</span></span> | <span data-ttu-id="da6d7-351">Float</span><span class="sxs-lookup"><span data-stu-id="da6d7-351">Float</span></span> |
| <span data-ttu-id="da6d7-352">Money</span><span class="sxs-lookup"><span data-stu-id="da6d7-352">Money</span></span> | <span data-ttu-id="da6d7-353">Money</span><span class="sxs-lookup"><span data-stu-id="da6d7-353">Money</span></span> |
| <span data-ttu-id="da6d7-354">Real</span><span class="sxs-lookup"><span data-stu-id="da6d7-354">Real</span></span> | <span data-ttu-id="da6d7-355">Real</span><span class="sxs-lookup"><span data-stu-id="da6d7-355">Real</span></span> |
| <span data-ttu-id="da6d7-356">SmallMoney</span><span class="sxs-lookup"><span data-stu-id="da6d7-356">SmallMoney</span></span> | <span data-ttu-id="da6d7-357">SmallMoney</span><span class="sxs-lookup"><span data-stu-id="da6d7-357">SmallMoney</span></span> |
| <span data-ttu-id="da6d7-358">Fichier binaire</span><span class="sxs-lookup"><span data-stu-id="da6d7-358">Binary</span></span> | <span data-ttu-id="da6d7-359">Fichier binaire</span><span class="sxs-lookup"><span data-stu-id="da6d7-359">Binary</span></span> |
| <span data-ttu-id="da6d7-360">Varbinary</span><span class="sxs-lookup"><span data-stu-id="da6d7-360">Varbinary</span></span> | <span data-ttu-id="da6d7-361">Varbinary (haut too8000)</span><span class="sxs-lookup"><span data-stu-id="da6d7-361">Varbinary (up too8000)</span></span> |
| <span data-ttu-id="da6d7-362">Date</span><span class="sxs-lookup"><span data-stu-id="da6d7-362">Date</span></span> | <span data-ttu-id="da6d7-363">Date</span><span class="sxs-lookup"><span data-stu-id="da6d7-363">Date</span></span> |
| <span data-ttu-id="da6d7-364">DateTime</span><span class="sxs-lookup"><span data-stu-id="da6d7-364">DateTime</span></span> | <span data-ttu-id="da6d7-365">DateTime</span><span class="sxs-lookup"><span data-stu-id="da6d7-365">DateTime</span></span> |
| <span data-ttu-id="da6d7-366">DateTime2</span><span class="sxs-lookup"><span data-stu-id="da6d7-366">DateTime2</span></span> | <span data-ttu-id="da6d7-367">DateTime2</span><span class="sxs-lookup"><span data-stu-id="da6d7-367">DateTime2</span></span> |
| <span data-ttu-id="da6d7-368">Time</span><span class="sxs-lookup"><span data-stu-id="da6d7-368">Time</span></span> | <span data-ttu-id="da6d7-369">Time</span><span class="sxs-lookup"><span data-stu-id="da6d7-369">Time</span></span> |
| <span data-ttu-id="da6d7-370">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="da6d7-370">DateTimeOffset</span></span> | <span data-ttu-id="da6d7-371">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="da6d7-371">DateTimeOffset</span></span> |
| <span data-ttu-id="da6d7-372">SmallDateTime</span><span class="sxs-lookup"><span data-stu-id="da6d7-372">SmallDateTime</span></span> | <span data-ttu-id="da6d7-373">SmallDateTime</span><span class="sxs-lookup"><span data-stu-id="da6d7-373">SmallDateTime</span></span> |
| <span data-ttu-id="da6d7-374">Texte</span><span class="sxs-lookup"><span data-stu-id="da6d7-374">Text</span></span> | <span data-ttu-id="da6d7-375">Varchar (haut too8000)</span><span class="sxs-lookup"><span data-stu-id="da6d7-375">Varchar (up too8000)</span></span> |
| <span data-ttu-id="da6d7-376">NText</span><span class="sxs-lookup"><span data-stu-id="da6d7-376">NText</span></span> | <span data-ttu-id="da6d7-377">NVarChar (haut too4000)</span><span class="sxs-lookup"><span data-stu-id="da6d7-377">NVarChar (up too4000)</span></span> |
| <span data-ttu-id="da6d7-378">Image</span><span class="sxs-lookup"><span data-stu-id="da6d7-378">Image</span></span> | <span data-ttu-id="da6d7-379">VarBinary (haut too8000)</span><span class="sxs-lookup"><span data-stu-id="da6d7-379">VarBinary (up too8000)</span></span> |
| <span data-ttu-id="da6d7-380">UniqueIdentifier</span><span class="sxs-lookup"><span data-stu-id="da6d7-380">UniqueIdentifier</span></span> | <span data-ttu-id="da6d7-381">UniqueIdentifier</span><span class="sxs-lookup"><span data-stu-id="da6d7-381">UniqueIdentifier</span></span> |
| <span data-ttu-id="da6d7-382">Char</span><span class="sxs-lookup"><span data-stu-id="da6d7-382">Char</span></span> | <span data-ttu-id="da6d7-383">Char</span><span class="sxs-lookup"><span data-stu-id="da6d7-383">Char</span></span> |
| <span data-ttu-id="da6d7-384">NChar</span><span class="sxs-lookup"><span data-stu-id="da6d7-384">NChar</span></span> | <span data-ttu-id="da6d7-385">NChar</span><span class="sxs-lookup"><span data-stu-id="da6d7-385">NChar</span></span> |
| <span data-ttu-id="da6d7-386">VarChar</span><span class="sxs-lookup"><span data-stu-id="da6d7-386">VarChar</span></span> | <span data-ttu-id="da6d7-387">VarChar (haut too8000)</span><span class="sxs-lookup"><span data-stu-id="da6d7-387">VarChar (up too8000)</span></span> |
| <span data-ttu-id="da6d7-388">NVarChar</span><span class="sxs-lookup"><span data-stu-id="da6d7-388">NVarChar</span></span> | <span data-ttu-id="da6d7-389">NVarChar (haut too4000)</span><span class="sxs-lookup"><span data-stu-id="da6d7-389">NVarChar (up too4000)</span></span> |
| <span data-ttu-id="da6d7-390">xml</span><span class="sxs-lookup"><span data-stu-id="da6d7-390">Xml</span></span> | <span data-ttu-id="da6d7-391">Varchar (haut too8000)</span><span class="sxs-lookup"><span data-stu-id="da6d7-391">Varchar (up too8000)</span></span> |

[!INCLUDE [data-factory-type-repeatability-for-sql-sources](../../includes/data-factory-type-repeatability-for-sql-sources.md)]

## <a name="type-mapping-for-azure-sql-data-warehouse"></a><span data-ttu-id="da6d7-392">Mappage de type pour Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="da6d7-392">Type mapping for Azure SQL Data Warehouse</span></span>
<span data-ttu-id="da6d7-393">Comme mentionné dans hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, l’activité de copie effectue les conversions de type automatique à partir des types de sources de toosink types avec hello approche de l’étape 2 :</span><span class="sxs-lookup"><span data-stu-id="da6d7-393">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="da6d7-394">Convertir à partir de la source native types too.NET type</span><span class="sxs-lookup"><span data-stu-id="da6d7-394">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="da6d7-395">Conversion de type de récepteur de toonative de type .NET</span><span class="sxs-lookup"><span data-stu-id="da6d7-395">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="da6d7-396">Lorsque vous déplacez des données trop & à partir de l’entrepôt de données SQL Azure, hello mappages suivants sont utilisés à partir du type too.NET de type SQL et vice versa.</span><span class="sxs-lookup"><span data-stu-id="da6d7-396">When moving data too& from Azure SQL Data Warehouse, hello following mappings are used from SQL type too.NET type and vice versa.</span></span>

<span data-ttu-id="da6d7-397">mappage de Hello est identique à celui hello [mappage des types de données SQL Server pour ADO.NET](https://msdn.microsoft.com/library/cc716729.aspx).</span><span class="sxs-lookup"><span data-stu-id="da6d7-397">hello mapping is same as hello [SQL Server Data Type Mapping for ADO.NET](https://msdn.microsoft.com/library/cc716729.aspx).</span></span>

| <span data-ttu-id="da6d7-398">Type de moteur de base de données SQL Server</span><span class="sxs-lookup"><span data-stu-id="da6d7-398">SQL Server Database Engine type</span></span> | <span data-ttu-id="da6d7-399">Type de .NET Framework</span><span class="sxs-lookup"><span data-stu-id="da6d7-399">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="da6d7-400">bigint</span><span class="sxs-lookup"><span data-stu-id="da6d7-400">bigint</span></span> |<span data-ttu-id="da6d7-401">Int64</span><span class="sxs-lookup"><span data-stu-id="da6d7-401">Int64</span></span> |
| <span data-ttu-id="da6d7-402">binaire</span><span class="sxs-lookup"><span data-stu-id="da6d7-402">binary</span></span> |<span data-ttu-id="da6d7-403">Byte[]</span><span class="sxs-lookup"><span data-stu-id="da6d7-403">Byte[]</span></span> |
| <span data-ttu-id="da6d7-404">bit</span><span class="sxs-lookup"><span data-stu-id="da6d7-404">bit</span></span> |<span data-ttu-id="da6d7-405">Boolean</span><span class="sxs-lookup"><span data-stu-id="da6d7-405">Boolean</span></span> |
| <span data-ttu-id="da6d7-406">char</span><span class="sxs-lookup"><span data-stu-id="da6d7-406">char</span></span> |<span data-ttu-id="da6d7-407">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="da6d7-407">String, Char[]</span></span> |
| <span data-ttu-id="da6d7-408">date</span><span class="sxs-lookup"><span data-stu-id="da6d7-408">date</span></span> |<span data-ttu-id="da6d7-409">DateTime</span><span class="sxs-lookup"><span data-stu-id="da6d7-409">DateTime</span></span> |
| <span data-ttu-id="da6d7-410">DateTime</span><span class="sxs-lookup"><span data-stu-id="da6d7-410">Datetime</span></span> |<span data-ttu-id="da6d7-411">DateTime</span><span class="sxs-lookup"><span data-stu-id="da6d7-411">DateTime</span></span> |
| <span data-ttu-id="da6d7-412">datetime2</span><span class="sxs-lookup"><span data-stu-id="da6d7-412">datetime2</span></span> |<span data-ttu-id="da6d7-413">DateTime</span><span class="sxs-lookup"><span data-stu-id="da6d7-413">DateTime</span></span> |
| <span data-ttu-id="da6d7-414">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="da6d7-414">Datetimeoffset</span></span> |<span data-ttu-id="da6d7-415">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="da6d7-415">DateTimeOffset</span></span> |
| <span data-ttu-id="da6d7-416">Décimal</span><span class="sxs-lookup"><span data-stu-id="da6d7-416">Decimal</span></span> |<span data-ttu-id="da6d7-417">Décimal</span><span class="sxs-lookup"><span data-stu-id="da6d7-417">Decimal</span></span> |
| <span data-ttu-id="da6d7-418">Attribut FILESTREAM (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="da6d7-418">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="da6d7-419">Byte[]</span><span class="sxs-lookup"><span data-stu-id="da6d7-419">Byte[]</span></span> |
| <span data-ttu-id="da6d7-420">Float</span><span class="sxs-lookup"><span data-stu-id="da6d7-420">Float</span></span> |<span data-ttu-id="da6d7-421">Double</span><span class="sxs-lookup"><span data-stu-id="da6d7-421">Double</span></span> |
| <span data-ttu-id="da6d7-422">image</span><span class="sxs-lookup"><span data-stu-id="da6d7-422">image</span></span> |<span data-ttu-id="da6d7-423">Byte[]</span><span class="sxs-lookup"><span data-stu-id="da6d7-423">Byte[]</span></span> |
| <span data-ttu-id="da6d7-424">int</span><span class="sxs-lookup"><span data-stu-id="da6d7-424">int</span></span> |<span data-ttu-id="da6d7-425">Int32</span><span class="sxs-lookup"><span data-stu-id="da6d7-425">Int32</span></span> |
| <span data-ttu-id="da6d7-426">money</span><span class="sxs-lookup"><span data-stu-id="da6d7-426">money</span></span> |<span data-ttu-id="da6d7-427">Décimal</span><span class="sxs-lookup"><span data-stu-id="da6d7-427">Decimal</span></span> |
| <span data-ttu-id="da6d7-428">nchar</span><span class="sxs-lookup"><span data-stu-id="da6d7-428">nchar</span></span> |<span data-ttu-id="da6d7-429">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="da6d7-429">String, Char[]</span></span> |
| <span data-ttu-id="da6d7-430">ntext</span><span class="sxs-lookup"><span data-stu-id="da6d7-430">ntext</span></span> |<span data-ttu-id="da6d7-431">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="da6d7-431">String, Char[]</span></span> |
| <span data-ttu-id="da6d7-432">numérique</span><span class="sxs-lookup"><span data-stu-id="da6d7-432">numeric</span></span> |<span data-ttu-id="da6d7-433">Décimal</span><span class="sxs-lookup"><span data-stu-id="da6d7-433">Decimal</span></span> |
| <span data-ttu-id="da6d7-434">nvarchar</span><span class="sxs-lookup"><span data-stu-id="da6d7-434">nvarchar</span></span> |<span data-ttu-id="da6d7-435">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="da6d7-435">String, Char[]</span></span> |
| <span data-ttu-id="da6d7-436">real</span><span class="sxs-lookup"><span data-stu-id="da6d7-436">real</span></span> |<span data-ttu-id="da6d7-437">Single</span><span class="sxs-lookup"><span data-stu-id="da6d7-437">Single</span></span> |
| <span data-ttu-id="da6d7-438">rowversion</span><span class="sxs-lookup"><span data-stu-id="da6d7-438">rowversion</span></span> |<span data-ttu-id="da6d7-439">Byte[]</span><span class="sxs-lookup"><span data-stu-id="da6d7-439">Byte[]</span></span> |
| <span data-ttu-id="da6d7-440">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="da6d7-440">smalldatetime</span></span> |<span data-ttu-id="da6d7-441">DateTime</span><span class="sxs-lookup"><span data-stu-id="da6d7-441">DateTime</span></span> |
| <span data-ttu-id="da6d7-442">smallint</span><span class="sxs-lookup"><span data-stu-id="da6d7-442">smallint</span></span> |<span data-ttu-id="da6d7-443">Int16</span><span class="sxs-lookup"><span data-stu-id="da6d7-443">Int16</span></span> |
| <span data-ttu-id="da6d7-444">smallmoney</span><span class="sxs-lookup"><span data-stu-id="da6d7-444">smallmoney</span></span> |<span data-ttu-id="da6d7-445">Décimal</span><span class="sxs-lookup"><span data-stu-id="da6d7-445">Decimal</span></span> |
| <span data-ttu-id="da6d7-446">sql_variant</span><span class="sxs-lookup"><span data-stu-id="da6d7-446">sql_variant</span></span> |<span data-ttu-id="da6d7-447">Objet *</span><span class="sxs-lookup"><span data-stu-id="da6d7-447">Object *</span></span> |
| <span data-ttu-id="da6d7-448">texte</span><span class="sxs-lookup"><span data-stu-id="da6d7-448">text</span></span> |<span data-ttu-id="da6d7-449">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="da6d7-449">String, Char[]</span></span> |
| <span data-ttu-id="da6d7-450">time</span><span class="sxs-lookup"><span data-stu-id="da6d7-450">time</span></span> |<span data-ttu-id="da6d7-451">intervalle de temps</span><span class="sxs-lookup"><span data-stu-id="da6d7-451">TimeSpan</span></span> |
| <span data-ttu-id="da6d7-452">timestamp</span><span class="sxs-lookup"><span data-stu-id="da6d7-452">timestamp</span></span> |<span data-ttu-id="da6d7-453">Byte[]</span><span class="sxs-lookup"><span data-stu-id="da6d7-453">Byte[]</span></span> |
| <span data-ttu-id="da6d7-454">tinyint</span><span class="sxs-lookup"><span data-stu-id="da6d7-454">tinyint</span></span> |<span data-ttu-id="da6d7-455">Byte</span><span class="sxs-lookup"><span data-stu-id="da6d7-455">Byte</span></span> |
| <span data-ttu-id="da6d7-456">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="da6d7-456">uniqueidentifier</span></span> |<span data-ttu-id="da6d7-457">Guid</span><span class="sxs-lookup"><span data-stu-id="da6d7-457">Guid</span></span> |
| <span data-ttu-id="da6d7-458">varbinary</span><span class="sxs-lookup"><span data-stu-id="da6d7-458">varbinary</span></span> |<span data-ttu-id="da6d7-459">Byte[]</span><span class="sxs-lookup"><span data-stu-id="da6d7-459">Byte[]</span></span> |
| <span data-ttu-id="da6d7-460">varchar</span><span class="sxs-lookup"><span data-stu-id="da6d7-460">varchar</span></span> |<span data-ttu-id="da6d7-461">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="da6d7-461">String, Char[]</span></span> |
| <span data-ttu-id="da6d7-462">xml</span><span class="sxs-lookup"><span data-stu-id="da6d7-462">xml</span></span> |<span data-ttu-id="da6d7-463">xml</span><span class="sxs-lookup"><span data-stu-id="da6d7-463">Xml</span></span> |

<span data-ttu-id="da6d7-464">Vous pouvez également mapper des colonnes à partir de toocolumns du jeu de données source à partir de récepteur de jeu de données dans la définition d’activité de copie de hello.</span><span class="sxs-lookup"><span data-stu-id="da6d7-464">You can also map columns from source dataset toocolumns from sink dataset in hello copy activity definition.</span></span> <span data-ttu-id="da6d7-465">Pour plus d’informations, consultez [Mappage de colonnes de jeux de données dans Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="da6d7-465">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="json-examples-for-copying-data-tooand-from-sql-data-warehouse"></a><span data-ttu-id="da6d7-466">Exemples JSON pour la copie des données tooand à partir de l’entrepôt de données SQL</span><span class="sxs-lookup"><span data-stu-id="da6d7-466">JSON examples for copying data tooand from SQL Data Warehouse</span></span>
<span data-ttu-id="da6d7-467">Hello exemples suivants proposent des exemples de définitions de JSON que vous pouvez utiliser toocreate un pipeline à l’aide de [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="da6d7-467">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="da6d7-468">Elles montrent comment toocopy les tooand de données de l’entrepôt de données SQL Azure et de stockage d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="da6d7-468">They show how toocopy data tooand from Azure SQL Data Warehouse and Azure Blob Storage.</span></span> <span data-ttu-id="da6d7-469">Toutefois, les données peuvent être copiées **directement** de n’importe quelle tooany de sources de récepteurs hello indiqué [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) à l’aide de hello activité de copie dans Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="da6d7-469">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-azure-sql-data-warehouse-tooazure-blob"></a><span data-ttu-id="da6d7-470">Exemple : Copier des données à partir de l’entrepôt de données SQL Azure tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="da6d7-470">Example: Copy data from Azure SQL Data Warehouse tooAzure Blob</span></span>
<span data-ttu-id="da6d7-471">exemple Hello définit hello suivant des entités de fabrique de données :</span><span class="sxs-lookup"><span data-stu-id="da6d7-471">hello sample defines hello following Data Factory entities:</span></span>

1. <span data-ttu-id="da6d7-472">Un service lié de type [AzureSqlDW](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="da6d7-472">A linked service of type [AzureSqlDW](#linked-service-properties).</span></span>
2. <span data-ttu-id="da6d7-473">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="da6d7-473">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="da6d7-474">Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [AzureSqlDWTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="da6d7-474">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlDWTable](#dataset-properties).</span></span>
4. <span data-ttu-id="da6d7-475">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="da6d7-475">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="da6d7-476">Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [SqlDWSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="da6d7-476">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [SqlDWSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="da6d7-477">exemple Hello copie les données de séries chronologiques (horaires, quotidiennes, etc.) à partir d’une table dans l’objet blob tooa de base de données Azure SQL Data Warehouse toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="da6d7-477">hello sample copies time-series (hourly, daily, etc.) data from a table in Azure SQL Data Warehouse database tooa blob every hour.</span></span> <span data-ttu-id="da6d7-478">propriétés JSON Hello utilisées dans ces exemples sont décrits dans les sections suivantes des exemples de hello.</span><span class="sxs-lookup"><span data-stu-id="da6d7-478">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="da6d7-479">**Service lié Azure SQL Data Warehouse :**</span><span class="sxs-lookup"><span data-stu-id="da6d7-479">**Azure SQL Data Warehouse linked service:**</span></span>

```JSON
{
  "name": "AzureSqlDWLinkedService",
  "properties": {
    "type": "AzureSqlDW",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
<span data-ttu-id="da6d7-480">**Service lié Azure Blob Storage :**</span><span class="sxs-lookup"><span data-stu-id="da6d7-480">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="da6d7-481">**Jeu de données d'entrée Azure SQL Data Warehouse :**</span><span class="sxs-lookup"><span data-stu-id="da6d7-481">**Azure SQL Data Warehouse input dataset:**</span></span>

<span data-ttu-id="da6d7-482">exemple Hello suppose que vous avez créé une table « MyTable » dans l’entrepôt de données SQL Azure, et il contienne une colonne appelée « timestampcolumn » pour les données de série chronologique.</span><span class="sxs-lookup"><span data-stu-id="da6d7-482">hello sample assumes you have created a table “MyTable” in Azure SQL Data Warehouse and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="da6d7-483">Paramètre « external » : « true » informe service Data Factory de hello ce jeu de données hello est la fabrique de données externe toohello et n’est pas généré par une activité dans la fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="da6d7-483">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "AzureSqlDWInput",
  "properties": {
    "type": "AzureSqlDWTable",
    "linkedServiceName": "AzureSqlDWLinkedService",
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
<span data-ttu-id="da6d7-484">**Jeu de données de sortie Azure Blob :**</span><span class="sxs-lookup"><span data-stu-id="da6d7-484">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="da6d7-485">Les données sont écrites tooa nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="da6d7-485">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="da6d7-486">chemin d’accès du dossier Hello pour l’objet blob de hello est évaluée dynamiquement en fonction de l’heure de début hello de tranche hello qui est en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="da6d7-486">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="da6d7-487">chemin d’accès du dossier Hello utilise l’année, mois, jours et heures des parties de l’heure de début hello.</span><span class="sxs-lookup"><span data-stu-id="da6d7-487">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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

<span data-ttu-id="da6d7-488">**Activité de copie dans un pipeline avec SqlDWSource et BlobSink :**</span><span class="sxs-lookup"><span data-stu-id="da6d7-488">**Copy activity in a pipeline with SqlDWSource and BlobSink:**</span></span>

<span data-ttu-id="da6d7-489">Hello pipeline contient une activité de copie qui est configuré toouse hello des jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="da6d7-489">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="da6d7-490">Dans la définition JSON du pipeline hello, hello **source** type est défini trop**SqlDWSource** et **récepteur** type est défini trop**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="da6d7-490">In hello pipeline JSON definition, hello **source** type is set too**SqlDWSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="da6d7-491">la requête SQL Hello spécifiée pour hello **SqlReaderQuery** propriété sélectionne des données de hello Bonjour au-delà de toocopy d’heure.</span><span class="sxs-lookup"><span data-stu-id="da6d7-491">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLDWtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSqlDWInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlDWSource",
            "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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
> <span data-ttu-id="da6d7-492">Dans l’exemple de hello, **sqlReaderQuery** est spécifié pour hello SqlDWSource.</span><span class="sxs-lookup"><span data-stu-id="da6d7-492">In hello example, **sqlReaderQuery** is specified for hello SqlDWSource.</span></span> <span data-ttu-id="da6d7-493">Hello activité de copie s’exécute cette requête contre hello données de Azure SQL Data Warehouse source tooget hello.</span><span class="sxs-lookup"><span data-stu-id="da6d7-493">hello Copy Activity runs this query against hello Azure SQL Data Warehouse source tooget hello data.</span></span>
>
> <span data-ttu-id="da6d7-494">Ou bien, vous pouvez spécifier une procédure stockée en spécifiant hello **sqlReaderStoredProcedureName** et **storedProcedureParameters** (si hello une procédure stockée accepte des paramètres).</span><span class="sxs-lookup"><span data-stu-id="da6d7-494">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>
>
> <span data-ttu-id="da6d7-495">Si vous ne spécifiez pas de sqlReaderQuery ou sqlReaderStoredProcedureName, colonnes hello définis dans la section de structure hello du jeu de données hello JSON sont toobuild utilisé une requête (select column1, column2 dans MaTable) toorun contre hello Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="da6d7-495">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section of hello dataset JSON are used toobuild a query (select column1, column2 from mytable) toorun against hello Azure SQL Data Warehouse.</span></span> <span data-ttu-id="da6d7-496">Si la définition de dataset hello n’a pas de structure de hello, toutes les colonnes sont sélectionnées à partir de la table de hello.</span><span class="sxs-lookup"><span data-stu-id="da6d7-496">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>
>
>

### <a name="example-copy-data-from-azure-blob-tooazure-sql-data-warehouse"></a><span data-ttu-id="da6d7-497">Exemple : Copier des données d’objets Blob Azure tooAzure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="da6d7-497">Example: Copy data from Azure Blob tooAzure SQL Data Warehouse</span></span>
<span data-ttu-id="da6d7-498">exemple Hello définit hello suivant des entités de fabrique de données :</span><span class="sxs-lookup"><span data-stu-id="da6d7-498">hello sample defines hello following Data Factory entities:</span></span>

1. <span data-ttu-id="da6d7-499">Un service lié de type [AzureSqlDW](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="da6d7-499">A linked service of type [AzureSqlDW](#linked-service-properties).</span></span>
2. <span data-ttu-id="da6d7-500">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="da6d7-500">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="da6d7-501">un [jeu de données](data-factory-create-datasets.md) d'entrée de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="da6d7-501">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="da6d7-502">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureSqlDWTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="da6d7-502">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlDWTable](#dataset-properties).</span></span>
5. <span data-ttu-id="da6d7-503">Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) et [SqlDWSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="da6d7-503">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlDWSink](#copy-activity-properties).</span></span>

<span data-ttu-id="da6d7-504">exemple Hello copie les données de série chronologique (horaire, quotidienne, etc.) à partir de la table de tooa d’objets blob Azure dans la base de données Azure SQL Data Warehouse toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="da6d7-504">hello sample copies time-series data (hourly, daily, etc.) from Azure blob tooa table in Azure SQL Data Warehouse database every hour.</span></span> <span data-ttu-id="da6d7-505">propriétés JSON Hello utilisées dans ces exemples sont décrits dans les sections suivantes des exemples de hello.</span><span class="sxs-lookup"><span data-stu-id="da6d7-505">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="da6d7-506">**Service lié Azure SQL Data Warehouse :**</span><span class="sxs-lookup"><span data-stu-id="da6d7-506">**Azure SQL Data Warehouse linked service:**</span></span>

```JSON
{
  "name": "AzureSqlDWLinkedService",
  "properties": {
    "type": "AzureSqlDW",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
<span data-ttu-id="da6d7-507">**Service lié Azure Blob Storage :**</span><span class="sxs-lookup"><span data-stu-id="da6d7-507">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="da6d7-508">**Jeu de données d'entrée d'objet Blob Azure :**</span><span class="sxs-lookup"><span data-stu-id="da6d7-508">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="da6d7-509">Les données sont récupérées à partir d'un nouvel objet Blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="da6d7-509">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="da6d7-510">nom de chemin d’accès et de dossier pour l’objet blob de hello Hello sont dynamiquement évaluées en fonction de l’heure de début hello de tranche hello qui est en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="da6d7-510">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="da6d7-511">chemin d’accès du dossier Hello utilise la partie jour de l’heure de début hello, mois et année et nom de fichier partie d’heure hello de l’heure de début hello.</span><span class="sxs-lookup"><span data-stu-id="da6d7-511">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="da6d7-512">« external » : « true » paramètre informe le service Data Factory de hello que cette table est la fabrique de données externe toohello et qu’il n’est pas générée par une activité dans la fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="da6d7-512">“external”: “true” setting informs hello Data Factory service that this table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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
<span data-ttu-id="da6d7-513">**Jeu de données de sortie Azure SQL Data Warehouse :**</span><span class="sxs-lookup"><span data-stu-id="da6d7-513">**Azure SQL Data Warehouse output dataset:**</span></span>

<span data-ttu-id="da6d7-514">exemple Hello copie table tooa de données nommé « MyTable » dans l’entrepôt de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="da6d7-514">hello sample copies data tooa table named “MyTable” in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="da6d7-515">Créer la table de hello dans Azure SQL Data Warehouse avec hello même nombre de colonnes comme vous le souhaitez toocontain de fichier CSV d’objets Blob hello.</span><span class="sxs-lookup"><span data-stu-id="da6d7-515">Create hello table in Azure SQL Data Warehouse with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="da6d7-516">Nouvelles lignes sont ajoutées à la table de toohello toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="da6d7-516">New rows are added toohello table every hour.</span></span>

```JSON
{
  "name": "AzureSqlDWOutput",
  "properties": {
    "type": "AzureSqlDWTable",
    "linkedServiceName": "AzureSqlDWLinkedService",
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
<span data-ttu-id="da6d7-517">**Activité de copie dans un pipeline avec BlobSource et SqlDWSink :**</span><span class="sxs-lookup"><span data-stu-id="da6d7-517">**Copy activity in a pipeline with BlobSource and SqlDWSink:**</span></span>

<span data-ttu-id="da6d7-518">Hello pipeline contient une activité de copie qui est configuré toouse hello des jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="da6d7-518">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="da6d7-519">Dans la définition JSON du pipeline hello, hello **source** type est défini trop**BlobSource** et **récepteur** type est défini trop**SqlDWSink**.</span><span class="sxs-lookup"><span data-stu-id="da6d7-519">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**SqlDWSink**.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQLDW",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlDWOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource",
            "blobColumnSeparators": ","
          },
          "sink": {
            "type": "SqlDWSink",
            "allowPolyBase": true
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
<span data-ttu-id="da6d7-520">Pour une procédure pas à pas, consultez hello [1 To de charge dans Azure SQL Data Warehouse moins de 15 minutes avec Azure Data Factory](data-factory-load-sql-data-warehouse.md) et [charger les données avec Azure Data Factory](../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md) article Bonjour Azure SQL Data Warehouse documentation.</span><span class="sxs-lookup"><span data-stu-id="da6d7-520">For a walkthrough, see hello see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md) and [Load data with Azure Data Factory](../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md) article in hello Azure SQL Data Warehouse documentation.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="da6d7-521">Performances et réglage</span><span class="sxs-lookup"><span data-stu-id="da6d7-521">Performance and Tuning</span></span>
<span data-ttu-id="da6d7-522">Consultez [copie activité optimiser les performances et Guide d’optimisation](data-factory-copy-activity-performance.md) toolearn sur la clé de facteurs d’affecter les performances de transfert de données (activité de copie) dans Azure Data Factory et de différentes façons toooptimize il.</span><span class="sxs-lookup"><span data-stu-id="da6d7-522">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
