---
title: "Copie de données vers/à partir d’Azure SQL Data Warehouse | Microsoft Docs"
description: "Découvrez comment copier des données vers et à partir d’Azure SQL Data Warehouse à l’aide d’Azure Data Factory."
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
ms.openlocfilehash: 8cba89e0947646b498af07aa484511bf07bf7b0e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="copy-data-to-and-from-azure-sql-data-warehouse-using-azure-data-factory"></a><span data-ttu-id="bb803-103">Copier des données vers et à partir d’Azure SQL Data Warehouse à l’aide d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="bb803-103">Copy data to and from Azure SQL Data Warehouse using Azure Data Factory</span></span>
<span data-ttu-id="bb803-104">Cet article explique comment utiliser l’activité de copie dans Azure Data Factory pour déplacer des données vers ou à partir d’Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="bb803-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from Azure SQL Data Warehouse.</span></span> <span data-ttu-id="bb803-105">Il s’appuie sur l’article [Activités de déplacement des données](data-factory-data-movement-activities.md), qui présente une vue d’ensemble du déplacement de données avec l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="bb803-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>  

> [!TIP]
> <span data-ttu-id="bb803-106">Pour obtenir les meilleures performances, utilisez PolyBase pour charger des données dans Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="bb803-106">To achieve best performance, use PolyBase to load data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="bb803-107">Pour plus de détails, consultez [Utiliser PolyBase pour charger des données dans Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) .</span><span class="sxs-lookup"><span data-stu-id="bb803-107">The [Use PolyBase to load data into Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) section has details.</span></span> <span data-ttu-id="bb803-108">Consultez [Charger 1 To dans Azure SQL Data Warehouse en moins de 15 minutes avec Azure Data Factory](data-factory-load-sql-data-warehouse.md) pour obtenir une procédure pas à pas avec un cas d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="bb803-108">For a walkthrough with a use case, see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md).</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="bb803-109">Scénarios pris en charge</span><span class="sxs-lookup"><span data-stu-id="bb803-109">Supported scenarios</span></span>
<span data-ttu-id="bb803-110">Vous pouvez copier des données depuis **Azure SQL Data Warehouse** vers les magasins de données suivants :</span><span class="sxs-lookup"><span data-stu-id="bb803-110">You can copy data **from Azure SQL Data Warehouse** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="bb803-111">Vous pouvez copier des données depuis les magasins de données suivants **vers Azure SQL Data Warehouse** :</span><span class="sxs-lookup"><span data-stu-id="bb803-111">You can copy data from the following data stores **to Azure SQL Data Warehouse**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!TIP]
> <span data-ttu-id="bb803-112">Lors de la copie de données à partir de SQL Server ou d’Azure SQL Data Warehouse dans Azure SQL Data Warehouse, si la table n’existe pas dans le magasin de destination, Data Factory peut automatiquement créer la table dans SQL Data Warehouse en utilisant le schéma de la table dans le magasin de données source.</span><span class="sxs-lookup"><span data-stu-id="bb803-112">When copying data from SQL Server or Azure SQL Database to Azure SQL Data Warehouse, if the table does not exist in the destination store, Data Factory can automatically create the table in SQL Data Warehouse by using the schema of the table in the source data store.</span></span> <span data-ttu-id="bb803-113">Consultez [Création automatique de la table](#auto-table-creation) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="bb803-113">See [Auto table creation](#auto-table-creation) for details.</span></span>

## <a name="supported-authentication-type"></a><span data-ttu-id="bb803-114">Type d’authentification pris en charge</span><span class="sxs-lookup"><span data-stu-id="bb803-114">Supported authentication type</span></span>
<span data-ttu-id="bb803-115">Le connecteur Azure SQL Data Warehouse prend en charge l’authentification de base.</span><span class="sxs-lookup"><span data-stu-id="bb803-115">Azure SQL Data Warehouse connector support basic authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="bb803-116">Prise en main</span><span class="sxs-lookup"><span data-stu-id="bb803-116">Getting started</span></span>
<span data-ttu-id="bb803-117">Vous pouvez créer un pipeline avec une activité de copie qui déplace les données vers/depuis Azure SQL Data Warehouse à l’aide de différents outils/API.</span><span class="sxs-lookup"><span data-stu-id="bb803-117">You can create a pipeline with a copy activity that moves data to/from an Azure SQL Data Warehouse by using different tools/APIs.</span></span>

<span data-ttu-id="bb803-118">Le moyen le plus simple de créer un pipeline qui copie les données vers/depuis le Azure SQL Data Warehouse consiste à utiliser l’Assistant Copier des données.</span><span class="sxs-lookup"><span data-stu-id="bb803-118">The easiest way to create a pipeline that copies data to/from Azure SQL Data Warehouse is to use the Copy data wizard.</span></span> <span data-ttu-id="bb803-119">Consultez la page [Didacticiel : charger des données dans SQL Data Warehouse avec Data Factory](../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md) pour un bref aperçu sur la création d’un pipeline à l’aide de l’Assistant copie de données.</span><span class="sxs-lookup"><span data-stu-id="bb803-119">See [Tutorial: Load data into SQL Data Warehouse with Data Factory](../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="bb803-120">Vous pouvez également utiliser les outils suivants pour créer un pipeline : le **portail Azure**, **Visual Studio**, **Azure PowerShell**, le **modèle Azure Resource Manager**, l’**API .NET** et l’**API REST**.</span><span class="sxs-lookup"><span data-stu-id="bb803-120">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="bb803-121">Consultez le [Didacticiel de l’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions détaillées sur la création d’un pipeline avec une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="bb803-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="bb803-122">Que vous utilisiez des outils ou des API, la création d’un pipeline qui déplace les données d’un magasin de données source vers un magasin de données récepteur implique les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="bb803-122">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="bb803-123">Création d'une **fabrique de données**.</span><span class="sxs-lookup"><span data-stu-id="bb803-123">Create a **data factory**.</span></span> <span data-ttu-id="bb803-124">Une fabrique de données peut contenir un ou plusieurs pipelines.</span><span class="sxs-lookup"><span data-stu-id="bb803-124">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="bb803-125">Création de **services liés** pour lier les magasins de données d’entrée et de sortie à votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="bb803-125">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="bb803-126">Par exemple, si vous copiez des données depuis un stockage d’objets blob Azure vers un entrepôt de données SQL Azure, vous créez deux services liés pour lier votre compte de stockage Azure et Azure SQL Data Warehouse à votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="bb803-126">For example, if you are copying data from an Azure blob storage to an Azure SQL data warehouse, you create two linked services to link your Azure storage account and Azure SQL data warehouse to your data factory.</span></span> <span data-ttu-id="bb803-127">Pour les propriétés du service lié qui sont spécifiques à Azure SQL Data Warehouse, consultez la section [propriétés du service lié](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="bb803-127">For linked service properties that are specific to Azure SQL Data Warehouse, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="bb803-128">Création de **jeux de données** pour représenter les données d’entrée et de sortie de l’opération de copie.</span><span class="sxs-lookup"><span data-stu-id="bb803-128">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="bb803-129">Dans l’exemple mentionné dans la dernière étape, vous créez un jeu de données pour spécifier le conteneur d’objets blob et le dossier qui contient les données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="bb803-129">In the example mentioned in the last step, you create a dataset to specify the blob container and folder that contains the input data.</span></span> <span data-ttu-id="bb803-130">Vous créez aussi un autre jeu de données pour spécifier la table dans l’entrepôt de données SQL Azure qui contient les données copiées depuis le stockage d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="bb803-130">And, you create another dataset to specify the table in the Azure SQL data warehouse that holds the data copied from the blob storage.</span></span> <span data-ttu-id="bb803-131">Pour les propriétés du jeu de données qui sont spécifiques à Azure SQL Data Warehouse, consultez la section [propriétés du jeu de données](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="bb803-131">For dataset properties that are specific to Azure SQL Data Warehouse, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="bb803-132">Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="bb803-132">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="bb803-133">Dans l’exemple mentionné plus haut, vous utilisez BlobSource comme source et SqlDWSink comme récepteur pour l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="bb803-133">In the example mentioned earlier, you use BlobSource as a source and SqlDWSink as a sink for the copy activity.</span></span> <span data-ttu-id="bb803-134">De même, si vous copiez depuis Azure SQL Data Warehouse vers Stockage Blob Azure, vous utilisez SqlDWSource et BlobSink dans l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="bb803-134">Similarly, if you are copying from Azure SQL Data Warehouse to Azure Blob Storage, you use SqlDWSource and BlobSink in the copy activity.</span></span> <span data-ttu-id="bb803-135">Pour les propriétés de l’activité de copie qui sont spécifiques à Azure SQL Data Warehouse, consultez la section [propriétés de l’activité de copie](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="bb803-135">For copy activity properties that are specific to Azure SQL Data Warehouse, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="bb803-136">Pour plus d’informations sur l’utilisation d’un magasin de données comme source ou comme récepteur, cliquez sur le lien dans la section précédente pour votre magasin de données.</span><span class="sxs-lookup"><span data-stu-id="bb803-136">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span>

<span data-ttu-id="bb803-137">Lorsque vous utilisez l’Assistant, les définitions JSON de ces entités Data Factory (services liés, jeux de données et pipeline) sont automatiquement créées pour vous.</span><span class="sxs-lookup"><span data-stu-id="bb803-137">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="bb803-138">Lorsque vous utilisez des outils/API (à l’exception de l’API .NET), vous devez définir ces entités Data Factory au format JSON.</span><span class="sxs-lookup"><span data-stu-id="bb803-138">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="bb803-139">Pour obtenir des exemples comportant des définitions JSON pour les entités Data Factory utilisées pour copier les données vers ou à partir d’Azure SQL Data Warehouse, consultez la section [Exemples JSON](#json-examples-for-copying-data-to-and-from-sql-data-warehouse) de cet article.</span><span class="sxs-lookup"><span data-stu-id="bb803-139">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure SQL Data Warehouse, see [JSON examples](#json-examples-for-copying-data-to-and-from-sql-data-warehouse) section of this article.</span></span>

<span data-ttu-id="bb803-140">Les sections suivantes offrent des informations détaillées sur les propriétés JSON utilisées pour définir les entités Data Factory propres à Azure SQL Data Warehouse :</span><span class="sxs-lookup"><span data-stu-id="bb803-140">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure SQL Data Warehouse:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="bb803-141">Propriétés du service lié</span><span class="sxs-lookup"><span data-stu-id="bb803-141">Linked service properties</span></span>
<span data-ttu-id="bb803-142">Le tableau suivant fournit la description des éléments JSON spécifiques au service lié Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="bb803-142">The following table provides description for JSON elements specific to Azure SQL Data Warehouse linked service.</span></span>

| <span data-ttu-id="bb803-143">Propriété</span><span class="sxs-lookup"><span data-stu-id="bb803-143">Property</span></span> | <span data-ttu-id="bb803-144">Description</span><span class="sxs-lookup"><span data-stu-id="bb803-144">Description</span></span> | <span data-ttu-id="bb803-145">Requis</span><span class="sxs-lookup"><span data-stu-id="bb803-145">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bb803-146">type</span><span class="sxs-lookup"><span data-stu-id="bb803-146">type</span></span> |<span data-ttu-id="bb803-147">La propriété de type doit être définie sur **AzureSqlDW**</span><span class="sxs-lookup"><span data-stu-id="bb803-147">The type property must be set to: **AzureSqlDW**</span></span> |<span data-ttu-id="bb803-148">Oui</span><span class="sxs-lookup"><span data-stu-id="bb803-148">Yes</span></span> |
| <span data-ttu-id="bb803-149">connectionString</span><span class="sxs-lookup"><span data-stu-id="bb803-149">connectionString</span></span> |<span data-ttu-id="bb803-150">Spécifier les informations requises pour la connexion à l’instance Azure SQL Data Warehouse pour la propriété connectionString.</span><span class="sxs-lookup"><span data-stu-id="bb803-150">Specify information needed to connect to the Azure SQL Data Warehouse instance for the connectionString property.</span></span> <span data-ttu-id="bb803-151">Seule l’authentification de base est prise en charge.</span><span class="sxs-lookup"><span data-stu-id="bb803-151">Only basic authentication is supported.</span></span> |<span data-ttu-id="bb803-152">Oui</span><span class="sxs-lookup"><span data-stu-id="bb803-152">Yes</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="bb803-153">Configurez le [pare-feu Azure SQL Database](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) et le serveur de base de données pour [autoriser les services Azure à accéder au serveur](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span><span class="sxs-lookup"><span data-stu-id="bb803-153">Configure [Azure SQL Database Firewall](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) and the database server to [allow Azure Services to access the server](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span></span> <span data-ttu-id="bb803-154">En outre, si vous copiez des données vers Azure SQL Data Warehouse à partir d’un emplacement situé en dehors d’Azure, y compris à partir de sources de données locales avec la passerelle de la fabrique de données, configurez la plage d’adresses IP appropriée pour l’ordinateur qui envoie des données à Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="bb803-154">Additionally, if you are copying data to Azure SQL Data Warehouse from outside Azure including from on-premises data sources with data factory gateway, configure appropriate IP address range for the machine that is sending data to Azure SQL Data Warehouse.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="bb803-155">Propriétés du jeu de données</span><span class="sxs-lookup"><span data-stu-id="bb803-155">Dataset properties</span></span>
<span data-ttu-id="bb803-156">Pour obtenir une liste complète des sections et propriétés disponibles pour la définition de jeux de données, consultez l’article [Création de jeux de données](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="bb803-156">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="bb803-157">Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données (SQL Azure, Azure Blob, Azure Table, etc.).</span><span class="sxs-lookup"><span data-stu-id="bb803-157">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="bb803-158">La section typeProperties est différente pour chaque type de jeu de données et fournit des informations sur l'emplacement des données dans le magasin de données.</span><span class="sxs-lookup"><span data-stu-id="bb803-158">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="bb803-159">La section **typeProperties** du jeu de données de type **AzureSqlDWTable** a les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="bb803-159">The **typeProperties** section for the dataset of type **AzureSqlDWTable** has the following properties:</span></span>

| <span data-ttu-id="bb803-160">Propriété</span><span class="sxs-lookup"><span data-stu-id="bb803-160">Property</span></span> | <span data-ttu-id="bb803-161">Description</span><span class="sxs-lookup"><span data-stu-id="bb803-161">Description</span></span> | <span data-ttu-id="bb803-162">Requis</span><span class="sxs-lookup"><span data-stu-id="bb803-162">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bb803-163">TableName</span><span class="sxs-lookup"><span data-stu-id="bb803-163">tableName</span></span> |<span data-ttu-id="bb803-164">Nom de la table ou de la vue dans la base de données Azure SQL Data Warehouse à laquelle le service lié fait référence.</span><span class="sxs-lookup"><span data-stu-id="bb803-164">Name of the table or view in the Azure SQL Data Warehouse database that the linked service refers to.</span></span> |<span data-ttu-id="bb803-165">Oui</span><span class="sxs-lookup"><span data-stu-id="bb803-165">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="bb803-166">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="bb803-166">Copy activity properties</span></span>
<span data-ttu-id="bb803-167">Pour obtenir la liste complète des sections et des propriétés disponibles pour la définition des activités, consultez l’article [Création de pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="bb803-167">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="bb803-168">Les propriétés comme le nom, la description, les tables d’entrée et de sortie et la stratégie sont disponibles pour tous les types d’activités.</span><span class="sxs-lookup"><span data-stu-id="bb803-168">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="bb803-169">L'activité de copie accepte uniquement une entrée et produit une seule sortie.</span><span class="sxs-lookup"><span data-stu-id="bb803-169">The Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="bb803-170">En revanche, les propriétés disponibles dans la section typeProperties de l’activité varient pour chaque type d'activité.</span><span class="sxs-lookup"><span data-stu-id="bb803-170">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="bb803-171">Pour l’activité de copie, elles dépendent des types de sources et récepteurs.</span><span class="sxs-lookup"><span data-stu-id="bb803-171">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

### <a name="sqldwsource"></a><span data-ttu-id="bb803-172">SqlDWSource</span><span class="sxs-lookup"><span data-stu-id="bb803-172">SqlDWSource</span></span>
<span data-ttu-id="bb803-173">Lorsque la source est de type **SqlDWSource**, les propriétés suivantes sont disponibles dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="bb803-173">When source is of type **SqlDWSource**, the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="bb803-174">Propriété</span><span class="sxs-lookup"><span data-stu-id="bb803-174">Property</span></span> | <span data-ttu-id="bb803-175">Description</span><span class="sxs-lookup"><span data-stu-id="bb803-175">Description</span></span> | <span data-ttu-id="bb803-176">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="bb803-176">Allowed values</span></span> | <span data-ttu-id="bb803-177">Requis</span><span class="sxs-lookup"><span data-stu-id="bb803-177">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="bb803-178">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="bb803-178">sqlReaderQuery</span></span> |<span data-ttu-id="bb803-179">Utilise la requête personnalisée pour lire des données.</span><span class="sxs-lookup"><span data-stu-id="bb803-179">Use the custom query to read data.</span></span> |<span data-ttu-id="bb803-180">Chaîne de requête SQL.</span><span class="sxs-lookup"><span data-stu-id="bb803-180">SQL query string.</span></span> <span data-ttu-id="bb803-181">Par exemple : select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="bb803-181">For example: select * from MyTable.</span></span> |<span data-ttu-id="bb803-182">Non</span><span class="sxs-lookup"><span data-stu-id="bb803-182">No</span></span> |
| <span data-ttu-id="bb803-183">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="bb803-183">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="bb803-184">Nom de la procédure stockée qui lit les données de la table source.</span><span class="sxs-lookup"><span data-stu-id="bb803-184">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="bb803-185">Nom de la procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="bb803-185">Name of the stored procedure.</span></span> <span data-ttu-id="bb803-186">La dernière instruction SQL doit être une instruction SELECT dans la procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="bb803-186">The last SQL statement must be a SELECT statement in the stored procedure.</span></span> |<span data-ttu-id="bb803-187">Non</span><span class="sxs-lookup"><span data-stu-id="bb803-187">No</span></span> |
| <span data-ttu-id="bb803-188">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="bb803-188">storedProcedureParameters</span></span> |<span data-ttu-id="bb803-189">Paramètres de la procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="bb803-189">Parameters for the stored procedure.</span></span> |<span data-ttu-id="bb803-190">Paires nom/valeur.</span><span class="sxs-lookup"><span data-stu-id="bb803-190">Name/value pairs.</span></span> <span data-ttu-id="bb803-191">Les noms et la casse des paramètres doivent correspondre aux noms et à la casse des paramètres de la procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="bb803-191">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="bb803-192">Non</span><span class="sxs-lookup"><span data-stu-id="bb803-192">No</span></span> |

<span data-ttu-id="bb803-193">Si **sqlReaderQuery** est spécifié pour SqlDWSource, l'activité de copie exécute cette requête en fonction de la source Azure SQL Data Warehouse pour obtenir les données.</span><span class="sxs-lookup"><span data-stu-id="bb803-193">If the **sqlReaderQuery** is specified for the SqlDWSource, the Copy Activity runs this query against the Azure SQL Data Warehouse source to get the data.</span></span>

<span data-ttu-id="bb803-194">Vous pouvez également spécifier une procédure stockée en indiquant **sqlReaderStoredProcedureName** et **storedProcedureParameters** (si la procédure stockée accepte des paramètres).</span><span class="sxs-lookup"><span data-stu-id="bb803-194">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="bb803-195">Si vous ne spécifiez pas sqlReaderQuery ou sqlReaderStoredProcedureName, les colonnes définies dans la section Structure du jeu de données JSON sont utilisées pour créer une requête à exécuter sur Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="bb803-195">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section of the dataset JSON are used to build a query to run against the Azure SQL Data Warehouse.</span></span> <span data-ttu-id="bb803-196">Exemple : `select column1, column2 from mytable`.</span><span class="sxs-lookup"><span data-stu-id="bb803-196">Example: `select column1, column2 from mytable`.</span></span> <span data-ttu-id="bb803-197">Si la définition du jeu de données ne possède pas de structure, toutes les colonnes de la table sont sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="bb803-197">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

#### <a name="sqldwsource-example"></a><span data-ttu-id="bb803-198">Exemple SqlDWSource</span><span class="sxs-lookup"><span data-stu-id="bb803-198">SqlDWSource example</span></span>

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
<span data-ttu-id="bb803-199">**Définition de la procédure stockée :**</span><span class="sxs-lookup"><span data-stu-id="bb803-199">**The stored procedure definition:**</span></span>

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

### <a name="sqldwsink"></a><span data-ttu-id="bb803-200">SqlDWSink</span><span class="sxs-lookup"><span data-stu-id="bb803-200">SqlDWSink</span></span>
<span data-ttu-id="bb803-201">**SqlDWSink** prend en charge les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="bb803-201">**SqlDWSink** supports the following properties:</span></span>

| <span data-ttu-id="bb803-202">Propriété</span><span class="sxs-lookup"><span data-stu-id="bb803-202">Property</span></span> | <span data-ttu-id="bb803-203">Description</span><span class="sxs-lookup"><span data-stu-id="bb803-203">Description</span></span> | <span data-ttu-id="bb803-204">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="bb803-204">Allowed values</span></span> | <span data-ttu-id="bb803-205">Requis</span><span class="sxs-lookup"><span data-stu-id="bb803-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="bb803-206">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="bb803-206">sqlWriterCleanupScript</span></span> |<span data-ttu-id="bb803-207">Spécifiez une requête pour exécuter l’activité de copie afin que les données d’un segment spécifique soient nettoyées.</span><span class="sxs-lookup"><span data-stu-id="bb803-207">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="bb803-208">Consultez la [section sur la répétition](#repeatability-during-copy)pour plus de détails.</span><span class="sxs-lookup"><span data-stu-id="bb803-208">For details, see [repeatability section](#repeatability-during-copy).</span></span> |<span data-ttu-id="bb803-209">Une instruction de requête.</span><span class="sxs-lookup"><span data-stu-id="bb803-209">A query statement.</span></span> |<span data-ttu-id="bb803-210">Non</span><span class="sxs-lookup"><span data-stu-id="bb803-210">No</span></span> |
| <span data-ttu-id="bb803-211">allowPolyBase</span><span class="sxs-lookup"><span data-stu-id="bb803-211">allowPolyBase</span></span> |<span data-ttu-id="bb803-212">Indique s’il faut utiliser PolyBase (le cas échéant) au lieu du mécanisme BULKINSERT.</span><span class="sxs-lookup"><span data-stu-id="bb803-212">Indicates whether to use PolyBase (when applicable) instead of BULKINSERT mechanism.</span></span> <br/><br/> <span data-ttu-id="bb803-213">**L’utilisation de PolyBase est la méthode recommandée pour charger des données dans SQL Data Warehouse.**</span><span class="sxs-lookup"><span data-stu-id="bb803-213">**Using PolyBase is the recommended way to load data into SQL Data Warehouse.**</span></span> <span data-ttu-id="bb803-214">Reportez-vous à la section [Utiliser PolyBase pour charger des données dans Azure SQL Data Warehouse](#use-polybase-to-load-data-into-azure-sql-data-warehouse) pour connaître les contraintes et les détails.</span><span class="sxs-lookup"><span data-stu-id="bb803-214">See [Use PolyBase to load data into Azure SQL Data Warehouse](#use-polybase-to-load-data-into-azure-sql-data-warehouse) section for constraints and details.</span></span> |<span data-ttu-id="bb803-215">True </span><span class="sxs-lookup"><span data-stu-id="bb803-215">True</span></span> <br/><span data-ttu-id="bb803-216">False (valeur par défaut)</span><span class="sxs-lookup"><span data-stu-id="bb803-216">False (default)</span></span> |<span data-ttu-id="bb803-217">Non</span><span class="sxs-lookup"><span data-stu-id="bb803-217">No</span></span> |
| <span data-ttu-id="bb803-218">polyBaseSettings</span><span class="sxs-lookup"><span data-stu-id="bb803-218">polyBaseSettings</span></span> |<span data-ttu-id="bb803-219">Groupe de propriétés pouvant être spécifié lorsque la propriété **allowPolybase** est définie sur **true**.</span><span class="sxs-lookup"><span data-stu-id="bb803-219">A group of properties that can be specified when the **allowPolybase** property is set to **true**.</span></span> |&nbsp; |<span data-ttu-id="bb803-220">Non</span><span class="sxs-lookup"><span data-stu-id="bb803-220">No</span></span> |
| <span data-ttu-id="bb803-221">rejectValue</span><span class="sxs-lookup"><span data-stu-id="bb803-221">rejectValue</span></span> |<span data-ttu-id="bb803-222">Spécifie le nombre ou le pourcentage de lignes pouvant être rejetées avant l’échec de la requête.</span><span class="sxs-lookup"><span data-stu-id="bb803-222">Specifies the number or percentage of rows that can be rejected before the query fails.</span></span> <br/><br/><span data-ttu-id="bb803-223">Pour en savoir plus sur les options de rejet de PolyBase dans la section **Arguments** de la rubrique [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) (Créer une table externe (Transact-SQL)).</span><span class="sxs-lookup"><span data-stu-id="bb803-223">Learn more about the PolyBase’s reject options in the **Arguments** section of [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) topic.</span></span> |<span data-ttu-id="bb803-224">0 (par défaut), 1, 2, …</span><span class="sxs-lookup"><span data-stu-id="bb803-224">0 (default), 1, 2, …</span></span> |<span data-ttu-id="bb803-225">Non</span><span class="sxs-lookup"><span data-stu-id="bb803-225">No</span></span> |
| <span data-ttu-id="bb803-226">rejectType</span><span class="sxs-lookup"><span data-stu-id="bb803-226">rejectType</span></span> |<span data-ttu-id="bb803-227">Spécifie si l’option rejectValue est spécifiée comme une valeur littérale ou un pourcentage.</span><span class="sxs-lookup"><span data-stu-id="bb803-227">Specifies whether the rejectValue option is specified as a literal value or a percentage.</span></span> |<span data-ttu-id="bb803-228">Value (par défaut), Percentage</span><span class="sxs-lookup"><span data-stu-id="bb803-228">Value (default), Percentage</span></span> |<span data-ttu-id="bb803-229">Non</span><span class="sxs-lookup"><span data-stu-id="bb803-229">No</span></span> |
| <span data-ttu-id="bb803-230">rejectSampleValue</span><span class="sxs-lookup"><span data-stu-id="bb803-230">rejectSampleValue</span></span> |<span data-ttu-id="bb803-231">Détermine le nombre de lignes à extraire avant que PolyBase recalcule le pourcentage de lignes rejetées.</span><span class="sxs-lookup"><span data-stu-id="bb803-231">Determines the number of rows to retrieve before the PolyBase recalculates the percentage of rejected rows.</span></span> |<span data-ttu-id="bb803-232">1, 2, …</span><span class="sxs-lookup"><span data-stu-id="bb803-232">1, 2, …</span></span> |<span data-ttu-id="bb803-233">Oui, si le **rejectType** est **percentage**</span><span class="sxs-lookup"><span data-stu-id="bb803-233">Yes, if **rejectType** is **percentage**</span></span> |
| <span data-ttu-id="bb803-234">useTypeDefault</span><span class="sxs-lookup"><span data-stu-id="bb803-234">useTypeDefault</span></span> |<span data-ttu-id="bb803-235">Spécifie comment gérer les valeurs manquantes dans les fichiers texte délimités lorsque PolyBase extrait des données à partir du fichier texte.</span><span class="sxs-lookup"><span data-stu-id="bb803-235">Specifies how to handle missing values in delimited text files when PolyBase retrieves data from the text file.</span></span><br/><br/><span data-ttu-id="bb803-236">Pour plus d’informations sur cette propriété, consultez la section Arguments dans [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span><span class="sxs-lookup"><span data-stu-id="bb803-236">Learn more about this property from the Arguments section in [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span></span> |<span data-ttu-id="bb803-237">True, False (par défaut)</span><span class="sxs-lookup"><span data-stu-id="bb803-237">True, False (default)</span></span> |<span data-ttu-id="bb803-238">Non</span><span class="sxs-lookup"><span data-stu-id="bb803-238">No</span></span> |
| <span data-ttu-id="bb803-239">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="bb803-239">writeBatchSize</span></span> |<span data-ttu-id="bb803-240">Insère des données dans la table SQL lorsque la taille du tampon atteint writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="bb803-240">Inserts data into the SQL table when the buffer size reaches writeBatchSize</span></span> |<span data-ttu-id="bb803-241">Nombre entier (nombre de lignes)</span><span class="sxs-lookup"><span data-stu-id="bb803-241">Integer (number of rows)</span></span> |<span data-ttu-id="bb803-242">Non (valeur par défaut : 10000)</span><span class="sxs-lookup"><span data-stu-id="bb803-242">No (default: 10000)</span></span> |
| <span data-ttu-id="bb803-243">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="bb803-243">writeBatchTimeout</span></span> |<span data-ttu-id="bb803-244">Temps d’attente pour que l’opération d’insertion de lot soit terminée avant d’expirer.</span><span class="sxs-lookup"><span data-stu-id="bb803-244">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="bb803-245">intervalle de temps</span><span class="sxs-lookup"><span data-stu-id="bb803-245">timespan</span></span><br/><br/> <span data-ttu-id="bb803-246">Exemple : « 00:30:00 » (30 minutes).</span><span class="sxs-lookup"><span data-stu-id="bb803-246">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="bb803-247">Non</span><span class="sxs-lookup"><span data-stu-id="bb803-247">No</span></span> |

#### <a name="sqldwsink-example"></a><span data-ttu-id="bb803-248">Exemple SqlDWSink</span><span class="sxs-lookup"><span data-stu-id="bb803-248">SqlDWSink example</span></span>

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true
}
```

## <a name="use-polybase-to-load-data-into-azure-sql-data-warehouse"></a><span data-ttu-id="bb803-249">Utiliser PolyBase pour charger des données dans Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="bb803-249">Use PolyBase to load data into Azure SQL Data Warehouse</span></span>
<span data-ttu-id="bb803-250">L’utilisation de **[PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)** est un moyen efficace de charger de grandes quantités de données dans Azure SQL Data Warehouse avec un débit élevé.</span><span class="sxs-lookup"><span data-stu-id="bb803-250">Using **[PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)** is an efficient way of loading large amount of data into Azure SQL Data Warehouse with high throughput.</span></span> <span data-ttu-id="bb803-251">Vous pouvez profiter d’un gain important de débit en utilisant PolyBase au lieu du mécanisme BULKINSERT par défaut.</span><span class="sxs-lookup"><span data-stu-id="bb803-251">You can see a large gain in the throughput by using PolyBase instead of the default BULKINSERT mechanism.</span></span> <span data-ttu-id="bb803-252">Consultez [copier le numéro de référence des performances](data-factory-copy-activity-performance.md#performance-reference) qui contient une comparaison détaillée.</span><span class="sxs-lookup"><span data-stu-id="bb803-252">See [copy performance reference number](data-factory-copy-activity-performance.md#performance-reference) with detailed comparison.</span></span> <span data-ttu-id="bb803-253">Consultez [Charger 1 To dans Azure SQL Data Warehouse en moins de 15 minutes avec Azure Data Factory](data-factory-load-sql-data-warehouse.md) pour obtenir une procédure pas à pas avec un cas d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="bb803-253">For a walkthrough with a use case, see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md).</span></span>

* <span data-ttu-id="bb803-254">Si votre source de données se trouve dans **Stockage Blob Azure ou Azure Data Lake Store**, et si le format est compatible avec PolyBase, vous pouvez la copier directement vers Azure SQL Data Warehouse à l’aide de PolyBase.</span><span class="sxs-lookup"><span data-stu-id="bb803-254">If your source data is in **Azure Blob or Azure Data Lake Store**, and the format is compatible with PolyBase, you can directly copy to Azure SQL Data Warehouse using PolyBase.</span></span> <span data-ttu-id="bb803-255">Consultez **[Copie directe à l’aide de PolyBase](#direct-copy-using-polybase)**.</span><span class="sxs-lookup"><span data-stu-id="bb803-255">See **[Direct copy using PolyBase](#direct-copy-using-polybase)** with details.</span></span>
* <span data-ttu-id="bb803-256">Si votre banque de données sources et son format ne sont pas pris en charge à l’origine par PolyBase, vous pouvez utiliser la fonctionnalité **[Copie intermédiaire avec PolyBase](#staged-copy-using-polybase)** à la place.</span><span class="sxs-lookup"><span data-stu-id="bb803-256">If your source data store and format is not originally supported by PolyBase, you can use the **[Staged Copy using PolyBase](#staged-copy-using-polybase)** feature instead.</span></span> <span data-ttu-id="bb803-257">Elle propose également un meilleur débit en convertissant les données dans un format compatible avec PolyBase et en stockant les données dans le stockage Blob Azure automatiquement.</span><span class="sxs-lookup"><span data-stu-id="bb803-257">It also provides you better throughput by automatically converting the data into PolyBase-compatible format and storing the data in Azure Blob storage.</span></span> <span data-ttu-id="bb803-258">Il charge ensuite les données dans SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="bb803-258">It then loads data into SQL Data Warehouse.</span></span>

<span data-ttu-id="bb803-259">Définissez la propriété `allowPolyBase` sur **true** comme indiqué dans l’exemple suivant pour Azure Data Factory pour utiliser PolyBase afin de copier les données à partir du stockage d’objets Blob Azure vers Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="bb803-259">Set the `allowPolyBase` property to **true** as shown in the following example for Azure Data Factory to use PolyBase to copy data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="bb803-260">Lorsque vous définissez allowPolyBase sur true, vous pouvez spécifier des propriétés PolyBase spécifiques à l’aide du groupe de propriétés `polyBaseSettings`.</span><span class="sxs-lookup"><span data-stu-id="bb803-260">When you set allowPolyBase to true, you can specify PolyBase specific properties using the `polyBaseSettings` property group.</span></span> <span data-ttu-id="bb803-261">Reportez-vous à la section [SqlDWSink](#SqlDWSink) pour plus d’informations sur les propriétés que vous pouvez utiliser avec polyBaseSettings.</span><span class="sxs-lookup"><span data-stu-id="bb803-261">see the [SqlDWSink](#SqlDWSink) section for details about properties that you can use with polyBaseSettings.</span></span>

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

### <a name="direct-copy-using-polybase"></a><span data-ttu-id="bb803-262">Copie directe à l’aide de PolyBase</span><span class="sxs-lookup"><span data-stu-id="bb803-262">Direct copy using PolyBase</span></span>
<span data-ttu-id="bb803-263">SQL Data Warehouse PolyBase prend directement en charge Stockage Blob Azure et Azure Data Lake Store (à l’aide du principal du service) en tant que source et avec des exigences de format de fichier spécifiques.</span><span class="sxs-lookup"><span data-stu-id="bb803-263">SQL Data Warehouse PolyBase directly support Azure Blob and Azure Data Lake Store (using service principal) as source and with specific file format requirements.</span></span> <span data-ttu-id="bb803-264">Si vos données source répondent aux critères décrits dans cette section, vous pouvez les copier directement du magasin de données source vers Azure SQL Data Warehouse à l’aide de PolyBase.</span><span class="sxs-lookup"><span data-stu-id="bb803-264">If your source data meets the criteria described in this section, you can directly copy from source data store to Azure SQL Data Warehouse using PolyBase.</span></span> <span data-ttu-id="bb803-265">Sinon, vous pouvez utiliser la méthode [Copie intermédiaire à l’aide de PolyBase](#staged-copy-using-polybase).</span><span class="sxs-lookup"><span data-stu-id="bb803-265">Otherwise, you can use [Staged Copy using PolyBase](#staged-copy-using-polybase).</span></span>

> [!TIP]
> <span data-ttu-id="bb803-266">Pour copier des données de Data Lake Store vers SQL Data Warehouse efficacement, voir [Azure Data Factory makes it even easier and convenient to uncover insights from data when using Data Lake Store with SQL Data Warehouse](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/) (Azure Data Factory facilite et rend plus pratique la découverte d’informations à partir de données lors de l’utilisation de Data Lake Store avec SQL Data Warehouse).</span><span class="sxs-lookup"><span data-stu-id="bb803-266">To copy data from Data Lake Store to SQL Data Warehouse efficiently, learn more from [Azure Data Factory makes it even easier and convenient to uncover insights from data when using Data Lake Store with SQL Data Warehouse](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/).</span></span>

<span data-ttu-id="bb803-267">Si les critères ne sont pas remplis, Azure Data Factory contrôle les paramètres et rétablit automatiquement le mécanisme BULKINSERT pour le déplacement des données.</span><span class="sxs-lookup"><span data-stu-id="bb803-267">If the requirements are not met, Azure Data Factory checks the settings and automatically falls back to the BULKINSERT mechanism for the data movement.</span></span>

1. <span data-ttu-id="bb803-268">Le **service lié de la source** est de type : **AzureStorage** ou **AzureDataLakeStore avec authentification du principal de service**.</span><span class="sxs-lookup"><span data-stu-id="bb803-268">**Source linked service** is of type: **AzureStorage** or **AzureDataLakeStore with service principal authentication**.</span></span>  
2. <span data-ttu-id="bb803-269">Le **jeu de données d’entrée** est de type **Azure Blob** ou **AzureDataLakeStore** et le type de format dans les propriétés `type` est **OrcFormat** ou **TextFormat** avec les configurations suivantes :</span><span class="sxs-lookup"><span data-stu-id="bb803-269">The **input dataset** is of type: **AzureBlob** or **AzureDataLakeStore**, and the format type under `type` properties is **OrcFormat**, or **TextFormat** with the following configurations:</span></span>

   1. <span data-ttu-id="bb803-270">`rowDelimiter` doit être **\n**.</span><span class="sxs-lookup"><span data-stu-id="bb803-270">`rowDelimiter` must be **\n**.</span></span>
   2. <span data-ttu-id="bb803-271">`nullValue` est défini sur **chaîne vide** ("") ou `treatEmptyAsNull` est défini sur **true**.</span><span class="sxs-lookup"><span data-stu-id="bb803-271">`nullValue` is set to **empty string** (""), or `treatEmptyAsNull` is set to **true**.</span></span>
   3. <span data-ttu-id="bb803-272">`encodingName` est défini sur **utf-8**, qui est la valeur **par défaut**.</span><span class="sxs-lookup"><span data-stu-id="bb803-272">`encodingName` is set to **utf-8**, which is **default** value.</span></span>
   4. <span data-ttu-id="bb803-273">`escapeChar`, `quoteChar`, `firstRowAsHeader` et `skipLineCount` ne sont pas spécifiés.</span><span class="sxs-lookup"><span data-stu-id="bb803-273">`escapeChar`, `quoteChar`, `firstRowAsHeader`, and `skipLineCount` are not specified.</span></span>
   5. <span data-ttu-id="bb803-274">`compression` peut être **aucune compression**, **GZip** ou **Deflate**.</span><span class="sxs-lookup"><span data-stu-id="bb803-274">`compression` can be **no compression**, **GZip**, or **Deflate**.</span></span>

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

3. <span data-ttu-id="bb803-275">Il n’y a aucun paramètre `skipHeaderLineCount` sous **BlobSource** ou **AzureDataLakeStore** pour l’activité de copie dans le pipeline.</span><span class="sxs-lookup"><span data-stu-id="bb803-275">There is no `skipHeaderLineCount` setting under **BlobSource** or **AzureDataLakeStore** for the Copy activity in the pipeline.</span></span>
4. <span data-ttu-id="bb803-276">Il n’y a aucun paramètre `sliceIdentifierColumnName` sous **SqlDWSink** pour l’activité de copie dans le pipeline.</span><span class="sxs-lookup"><span data-stu-id="bb803-276">There is no `sliceIdentifierColumnName` setting under **SqlDWSink** for the Copy activity in the pipeline.</span></span> <span data-ttu-id="bb803-277">(PolyBase garantit que toutes les données sont mises à jour ou que rien n’est mis à jour en une seule exécution.</span><span class="sxs-lookup"><span data-stu-id="bb803-277">(PolyBase guarantees that all data is updated or nothing is updated in a single run.</span></span> <span data-ttu-id="bb803-278">Pour définir la **répétabilité**, vous pouvez utiliser `sqlWriterCleanupScript`.</span><span class="sxs-lookup"><span data-stu-id="bb803-278">To achieve **repeatability**, you could use `sqlWriterCleanupScript`).</span></span>
5. <span data-ttu-id="bb803-279">Il n’y a pas de `columnMapping` utilisé dans l’activité de copie associée.</span><span class="sxs-lookup"><span data-stu-id="bb803-279">There is no `columnMapping` being used in the associated in Copy activity.</span></span>

### <a name="staged-copy-using-polybase"></a><span data-ttu-id="bb803-280">Copie intermédiaire à l’aide de PolyBase</span><span class="sxs-lookup"><span data-stu-id="bb803-280">Staged Copy using PolyBase</span></span>
<span data-ttu-id="bb803-281">Lorsque vos données source ne répondent pas aux critères présentés dans la section précédente, vous pouvez activer la copie des données par le biais d’un Stockage Blob Azure intermédiaire (il ne peut pas s’agir d’une offre Stockage Premium).</span><span class="sxs-lookup"><span data-stu-id="bb803-281">When your source data doesn’t meet the criteria introduced in the previous section, you can enable copying data via an interim staging Azure Blob Storage (cannot be Premium Storage).</span></span> <span data-ttu-id="bb803-282">Dans ce cas, Azure Data Factory effectue automatiquement des transformations sur les données pour répondre aux exigences de format de données de PolyBase, utilise PolyBase pour charger les données dans SQL Data Warehouse puis supprime les données temporaires du Stockage Blob.</span><span class="sxs-lookup"><span data-stu-id="bb803-282">In this case, Azure Data Factory automatically performs transformations on the data to meet data format requirements of PolyBase, then use PolyBase to load data into SQL Data Warehouse, and at last clean-up your temp data from the Blob storage.</span></span> <span data-ttu-id="bb803-283">Consultez la rubrique [Copie intermédiaire](data-factory-copy-activity-performance.md#staged-copy) pour plus d’informations sur le fonctionnement général de la copie des données par le biais d’un Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="bb803-283">See [Staged Copy](data-factory-copy-activity-performance.md#staged-copy) for details on how copying data via a staging Azure Blob works in general.</span></span>

> [!NOTE]
> <span data-ttu-id="bb803-284">Lors de la copie de données à partir d’un magasin de données local dans Azure SQL Data Warehouse à l’aide de PolyBase et du stockage intermédiaire, si la version de votre passerelle de gestion des données est antérieure à la version 2.4, vous devez installer JRE (Java Runtime Environment) sur votre ordinateur passerelle, qui est utilisé pour convertir vos données source dans le bon format.</span><span class="sxs-lookup"><span data-stu-id="bb803-284">When copying data from an on-prem data store into Azure SQL Data Warehouse using PolyBase and staging, if your Data Management Gateway version is below 2.4, JRE (Java Runtime Environment) is required on your gateway machine that is used to transform your source data into proper format.</span></span> <span data-ttu-id="bb803-285">Nous vous conseillons de mettre à niveau votre passerelle vers la dernière version pour éviter une telle dépendance.</span><span class="sxs-lookup"><span data-stu-id="bb803-285">Suggest you upgrade your gateway to the latest to avoid such dependency.</span></span>
>

<span data-ttu-id="bb803-286">Pour utiliser cette fonctionnalité, vous devez créer un [service lié Azure Storage](data-factory-azure-blob-connector.md#azure-storage-linked-service) qui fait référence au compte de stockage Azure qui comprend le stockage d’objets blob intermédiaire, puis spécifier les propriétés `enableStaging` et `stagingSettings` de l’activité de copie, comme indiqué dans le code suivant :</span><span class="sxs-lookup"><span data-stu-id="bb803-286">To use this feature, create an [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) that refers to the Azure Storage Account that has the interim blob storage, then specify the `enableStaging` and `stagingSettings` properties for the Copy Activity as shown in the following code:</span></span>

```json
"activities":[  
{
    "name": "Sample copy activity from SQL Server to SQL Data Warehouse via PolyBase",
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

## <a name="best-practices-when-using-polybase"></a><span data-ttu-id="bb803-287">Meilleures pratiques lors de l’utilisation de PolyBase</span><span class="sxs-lookup"><span data-stu-id="bb803-287">Best practices when using PolyBase</span></span>
<span data-ttu-id="bb803-288">Les sections suivantes contiennent des bonnes pratiques qui s’ajoutent à celles mentionnées dans [Bonnes pratiques pour Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="bb803-288">The following sections provide additional best practices to the ones that are mentioned in [Best practices for Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md).</span></span>

### <a name="required-database-permission"></a><span data-ttu-id="bb803-289">Autorisation de base de données requise</span><span class="sxs-lookup"><span data-stu-id="bb803-289">Required database permission</span></span>
<span data-ttu-id="bb803-290">Pour utiliser PolyBase, il est nécessaire que l’utilisateur utilisé pour charger des données dans SQL Data Warehouse ait [l’autorisation « CONTROL »](https://msdn.microsoft.com/library/ms191291.aspx) sur la base de données cible.</span><span class="sxs-lookup"><span data-stu-id="bb803-290">To use PolyBase, it requires the user being used to load data into SQL Data Warehouse has the ["CONTROL" permission](https://msdn.microsoft.com/library/ms191291.aspx) on the target database.</span></span> <span data-ttu-id="bb803-291">Vous pouvez, pour cela, ajouter l’utilisateur en tant que membre du rôle « db_owner ».</span><span class="sxs-lookup"><span data-stu-id="bb803-291">One way to achieve that is to add that user as a member of "db_owner" role.</span></span> <span data-ttu-id="bb803-292">Découvrez comment procéder dans [cette section](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization).</span><span class="sxs-lookup"><span data-stu-id="bb803-292">Learn how to do that by following [this section](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization).</span></span>

### <a name="row-size-and-data-type-limitation"></a><span data-ttu-id="bb803-293">Limitations en matière de taille de ligne et de type de données</span><span class="sxs-lookup"><span data-stu-id="bb803-293">Row size and data type limitation</span></span>
<span data-ttu-id="bb803-294">Les charges Polybase sont limitées au chargement de lignes de moins de **1 Mo** et ne peuvent pas charger vers VARCHR(MAX), NVARCHAR(MAX) ou VARBINARY(MAX).</span><span class="sxs-lookup"><span data-stu-id="bb803-294">Polybase loads are limited to loading rows both smaller than **1 MB** and cannot load to VARCHR(MAX), NVARCHAR(MAX) or VARBINARY(MAX).</span></span> <span data-ttu-id="bb803-295">Consultez cette [section](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads).</span><span class="sxs-lookup"><span data-stu-id="bb803-295">Refer to [here](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads).</span></span>

<span data-ttu-id="bb803-296">Si les données source dont vous disposez ont des lignes d’une taille supérieure à 1 Mo, vous pouvez fractionner verticalement les tables source en plusieurs tables plus petites dans lesquelles la taille de ligne maximale ne dépasse pas la limite.</span><span class="sxs-lookup"><span data-stu-id="bb803-296">If you have source data with rows of size greater than 1 MB, you may want to split the source tables vertically into several small ones where the largest row size of each of them does not exceed the limit.</span></span> <span data-ttu-id="bb803-297">Vous pouvez ensuite charger les tables plus petites à l’aide de PolyBase et les fusionner dans Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="bb803-297">The smaller tables can then be loaded using PolyBase and merged together in Azure SQL Data Warehouse.</span></span>

### <a name="sql-data-warehouse-resource-class"></a><span data-ttu-id="bb803-298">Classe de ressources SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="bb803-298">SQL Data Warehouse resource class</span></span>
<span data-ttu-id="bb803-299">Pour obtenir le meilleur débit possible, envisagez d’attribuer une classe de ressources plus volumineuse à l’utilisateur utilisé pour charger des données dans SQL Data Warehouse via PolyBase.</span><span class="sxs-lookup"><span data-stu-id="bb803-299">To achieve best possible throughput, consider to assign larger resource class to the user being used to load data into SQL Data Warehouse via PolyBase.</span></span> <span data-ttu-id="bb803-300">Découvrez comment procéder en consultant [Exemple de modification d’une classe de ressources utilisateur](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="bb803-300">Learn how to do that by following [Change a user resource class example](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>

### <a name="tablename-in-azure-sql-data-warehouse"></a><span data-ttu-id="bb803-301">tableName dans Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="bb803-301">tableName in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="bb803-302">Le tableau suivant fournit des exemples sur la façon de spécifier la propriété **tableName** dans le jeu de données JSON pour différentes combinaisons de schémas et noms de table.</span><span class="sxs-lookup"><span data-stu-id="bb803-302">The following table provides examples on how to specify the **tableName** property in dataset JSON for various combinations of schema and table name.</span></span>

| <span data-ttu-id="bb803-303">Schéma BD</span><span class="sxs-lookup"><span data-stu-id="bb803-303">DB Schema</span></span> | <span data-ttu-id="bb803-304">Nom de la table</span><span class="sxs-lookup"><span data-stu-id="bb803-304">Table name</span></span> | <span data-ttu-id="bb803-305">Propriété JSON tableName</span><span class="sxs-lookup"><span data-stu-id="bb803-305">tableName JSON property</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bb803-306">dbo</span><span class="sxs-lookup"><span data-stu-id="bb803-306">dbo</span></span> |<span data-ttu-id="bb803-307">MyTable</span><span class="sxs-lookup"><span data-stu-id="bb803-307">MyTable</span></span> |<span data-ttu-id="bb803-308">MyTable ou dbo.MyTable ou [dbo].[MyTable]</span><span class="sxs-lookup"><span data-stu-id="bb803-308">MyTable or dbo.MyTable or [dbo].[MyTable]</span></span> |
| <span data-ttu-id="bb803-309">dbo1</span><span class="sxs-lookup"><span data-stu-id="bb803-309">dbo1</span></span> |<span data-ttu-id="bb803-310">MyTable</span><span class="sxs-lookup"><span data-stu-id="bb803-310">MyTable</span></span> |<span data-ttu-id="bb803-311">dbo1.MyTable ou [dbo1].[MyTable]</span><span class="sxs-lookup"><span data-stu-id="bb803-311">dbo1.MyTable or [dbo1].[MyTable]</span></span> |
| <span data-ttu-id="bb803-312">dbo</span><span class="sxs-lookup"><span data-stu-id="bb803-312">dbo</span></span> |<span data-ttu-id="bb803-313">My.Table</span><span class="sxs-lookup"><span data-stu-id="bb803-313">My.Table</span></span> |<span data-ttu-id="bb803-314">[My.Table] ou [dbo].[My.Table]</span><span class="sxs-lookup"><span data-stu-id="bb803-314">[My.Table] or [dbo].[My.Table]</span></span> |
| <span data-ttu-id="bb803-315">dbo1</span><span class="sxs-lookup"><span data-stu-id="bb803-315">dbo1</span></span> |<span data-ttu-id="bb803-316">My.Table</span><span class="sxs-lookup"><span data-stu-id="bb803-316">My.Table</span></span> |<span data-ttu-id="bb803-317">[dbo1].[My.Table]</span><span class="sxs-lookup"><span data-stu-id="bb803-317">[dbo1].[My.Table]</span></span> |

<span data-ttu-id="bb803-318">Si vous voyez l’erreur suivante, il peut s’agir d’un problème avec la valeur spécifiée pour la propriété tableName.</span><span class="sxs-lookup"><span data-stu-id="bb803-318">If you see the following error, it could be an issue with the value you specified for the tableName property.</span></span> <span data-ttu-id="bb803-319">Consultez le tableau pour savoir comment spécifier des valeurs pour la propriété JSON tableName.</span><span class="sxs-lookup"><span data-stu-id="bb803-319">See the table for the correct way to specify values for the tableName JSON property.</span></span>  

```
Type=System.Data.SqlClient.SqlException,Message=Invalid object name 'stg.Account_test'.,Source=.Net SqlClient Data Provider
```

### <a name="columns-with-default-values"></a><span data-ttu-id="bb803-320">Colonnes avec des valeurs par défaut</span><span class="sxs-lookup"><span data-stu-id="bb803-320">Columns with default values</span></span>
<span data-ttu-id="bb803-321">Actuellement, la fonctionnalité PolyBase dans Data Factory accepte seulement le même nombre de colonnes que la table cible.</span><span class="sxs-lookup"><span data-stu-id="bb803-321">Currently, PolyBase feature in Data Factory only accepts the same number of columns as in the target table.</span></span> <span data-ttu-id="bb803-322">Par exemple, vous avez une table avec quatre colonnes et l’une d’elles est définie avec une valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="bb803-322">Say, you have a table with four columns and one of them is defined with a default value.</span></span> <span data-ttu-id="bb803-323">Les données d’entrée doivent toujours contenir quatre colonnes.</span><span class="sxs-lookup"><span data-stu-id="bb803-323">The input data should still contain four columns.</span></span> <span data-ttu-id="bb803-324">La fourniture d’un jeu de données d’entrée de 3 colonnes produirait une erreur semblable au message suivant :</span><span class="sxs-lookup"><span data-stu-id="bb803-324">Providing a 3-column input dataset would yield an error similar to the following message:</span></span>

```
All columns of the table must be specified in the INSERT BULK statement.
```
<span data-ttu-id="bb803-325">La valeur NULL est une forme spéciale de valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="bb803-325">NULL value is a special form of default value.</span></span> <span data-ttu-id="bb803-326">Si la colonne accepte la valeur Null, les données d’entrée (dans l’objet blob) de cette colonne peuvent être vides (ne peuvent pas être absentes du jeu de données d’entrée).</span><span class="sxs-lookup"><span data-stu-id="bb803-326">If the column is nullable, the input data (in blob) for that column could be empty (cannot be missing from the input dataset).</span></span> <span data-ttu-id="bb803-327">PolyBase insère NULL pour ces données dans Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="bb803-327">PolyBase inserts NULL for them in the Azure SQL Data Warehouse.</span></span>  

## <a name="auto-table-creation"></a><span data-ttu-id="bb803-328">Création automatique de la table</span><span class="sxs-lookup"><span data-stu-id="bb803-328">Auto table creation</span></span>
<span data-ttu-id="bb803-329">Si vous utilisez l’assistant de copie pour copier des données à partir de SQL Server ou d’Azure SQL Data Warehouse dans Azure SQL Data Warehouse et que la table qui correspond à la table source n’existe pas dans le magasin de destination, Data Factory peut automatiquement créer la table dans SQL Data Warehouse en utilisant le schéma de table source.</span><span class="sxs-lookup"><span data-stu-id="bb803-329">If you are using Copy Wizard to copy data from SQL Server or Azure SQL Database to Azure SQL Data Warehouse and the table that corresponds to the source table does not exist in the destination store, Data Factory can automatically create the table in the data warehouse by using the source table schema.</span></span>

<span data-ttu-id="bb803-330">Data Factory crée la table dans le magasin de destination portant le même nom de table dans le magasin de données source.</span><span class="sxs-lookup"><span data-stu-id="bb803-330">Data Factory creates the table in the destination store with the same table name in the source data store.</span></span> <span data-ttu-id="bb803-331">Les types de données des colonnes sont choisis en fonction du mappage de type suivant.</span><span class="sxs-lookup"><span data-stu-id="bb803-331">The data types for columns are chosen based on the following type mapping.</span></span> <span data-ttu-id="bb803-332">Si nécessaire, des conversions de type sont effectuées pour corriger les éventuelles incompatibilités entre les magasins source et de destination.</span><span class="sxs-lookup"><span data-stu-id="bb803-332">If needed, it performs type conversions to fix any incompatibilities between source and destination stores.</span></span> <span data-ttu-id="bb803-333">Il utilise également la distribution de tables en tourniquet (Round Robin).</span><span class="sxs-lookup"><span data-stu-id="bb803-333">It also uses Round Robin table distribution.</span></span>

| <span data-ttu-id="bb803-334">Type de colonne SQL Database source</span><span class="sxs-lookup"><span data-stu-id="bb803-334">Source SQL Database column type</span></span> | <span data-ttu-id="bb803-335">Type de colonne SQL DW de destination (limite de taille)</span><span class="sxs-lookup"><span data-stu-id="bb803-335">Destination SQL DW column type (size limitation)</span></span> |
| --- | --- |
| <span data-ttu-id="bb803-336">int</span><span class="sxs-lookup"><span data-stu-id="bb803-336">Int</span></span> | <span data-ttu-id="bb803-337">int</span><span class="sxs-lookup"><span data-stu-id="bb803-337">Int</span></span> |
| <span data-ttu-id="bb803-338">BigInt</span><span class="sxs-lookup"><span data-stu-id="bb803-338">BigInt</span></span> | <span data-ttu-id="bb803-339">BigInt</span><span class="sxs-lookup"><span data-stu-id="bb803-339">BigInt</span></span> |
| <span data-ttu-id="bb803-340">SmallInt</span><span class="sxs-lookup"><span data-stu-id="bb803-340">SmallInt</span></span> | <span data-ttu-id="bb803-341">SmallInt</span><span class="sxs-lookup"><span data-stu-id="bb803-341">SmallInt</span></span> |
| <span data-ttu-id="bb803-342">TinyInt</span><span class="sxs-lookup"><span data-stu-id="bb803-342">TinyInt</span></span> | <span data-ttu-id="bb803-343">TinyInt</span><span class="sxs-lookup"><span data-stu-id="bb803-343">TinyInt</span></span> |
| <span data-ttu-id="bb803-344">Bit</span><span class="sxs-lookup"><span data-stu-id="bb803-344">Bit</span></span> | <span data-ttu-id="bb803-345">Bit</span><span class="sxs-lookup"><span data-stu-id="bb803-345">Bit</span></span> |
| <span data-ttu-id="bb803-346">Décimal</span><span class="sxs-lookup"><span data-stu-id="bb803-346">Decimal</span></span> | <span data-ttu-id="bb803-347">Décimal</span><span class="sxs-lookup"><span data-stu-id="bb803-347">Decimal</span></span> |
| <span data-ttu-id="bb803-348">Chiffre</span><span class="sxs-lookup"><span data-stu-id="bb803-348">Numeric</span></span> | <span data-ttu-id="bb803-349">Décimal</span><span class="sxs-lookup"><span data-stu-id="bb803-349">Decimal</span></span> |
| <span data-ttu-id="bb803-350">Float</span><span class="sxs-lookup"><span data-stu-id="bb803-350">Float</span></span> | <span data-ttu-id="bb803-351">Float</span><span class="sxs-lookup"><span data-stu-id="bb803-351">Float</span></span> |
| <span data-ttu-id="bb803-352">Money</span><span class="sxs-lookup"><span data-stu-id="bb803-352">Money</span></span> | <span data-ttu-id="bb803-353">Money</span><span class="sxs-lookup"><span data-stu-id="bb803-353">Money</span></span> |
| <span data-ttu-id="bb803-354">Real</span><span class="sxs-lookup"><span data-stu-id="bb803-354">Real</span></span> | <span data-ttu-id="bb803-355">Real</span><span class="sxs-lookup"><span data-stu-id="bb803-355">Real</span></span> |
| <span data-ttu-id="bb803-356">SmallMoney</span><span class="sxs-lookup"><span data-stu-id="bb803-356">SmallMoney</span></span> | <span data-ttu-id="bb803-357">SmallMoney</span><span class="sxs-lookup"><span data-stu-id="bb803-357">SmallMoney</span></span> |
| <span data-ttu-id="bb803-358">Fichier binaire</span><span class="sxs-lookup"><span data-stu-id="bb803-358">Binary</span></span> | <span data-ttu-id="bb803-359">Fichier binaire</span><span class="sxs-lookup"><span data-stu-id="bb803-359">Binary</span></span> |
| <span data-ttu-id="bb803-360">Varbinary</span><span class="sxs-lookup"><span data-stu-id="bb803-360">Varbinary</span></span> | <span data-ttu-id="bb803-361">Varbinary (jusqu’à 8 000)</span><span class="sxs-lookup"><span data-stu-id="bb803-361">Varbinary (up to 8000)</span></span> |
| <span data-ttu-id="bb803-362">Date</span><span class="sxs-lookup"><span data-stu-id="bb803-362">Date</span></span> | <span data-ttu-id="bb803-363">Date</span><span class="sxs-lookup"><span data-stu-id="bb803-363">Date</span></span> |
| <span data-ttu-id="bb803-364">DateTime</span><span class="sxs-lookup"><span data-stu-id="bb803-364">DateTime</span></span> | <span data-ttu-id="bb803-365">DateTime</span><span class="sxs-lookup"><span data-stu-id="bb803-365">DateTime</span></span> |
| <span data-ttu-id="bb803-366">DateTime2</span><span class="sxs-lookup"><span data-stu-id="bb803-366">DateTime2</span></span> | <span data-ttu-id="bb803-367">DateTime2</span><span class="sxs-lookup"><span data-stu-id="bb803-367">DateTime2</span></span> |
| <span data-ttu-id="bb803-368">Time</span><span class="sxs-lookup"><span data-stu-id="bb803-368">Time</span></span> | <span data-ttu-id="bb803-369">Time</span><span class="sxs-lookup"><span data-stu-id="bb803-369">Time</span></span> |
| <span data-ttu-id="bb803-370">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="bb803-370">DateTimeOffset</span></span> | <span data-ttu-id="bb803-371">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="bb803-371">DateTimeOffset</span></span> |
| <span data-ttu-id="bb803-372">SmallDateTime</span><span class="sxs-lookup"><span data-stu-id="bb803-372">SmallDateTime</span></span> | <span data-ttu-id="bb803-373">SmallDateTime</span><span class="sxs-lookup"><span data-stu-id="bb803-373">SmallDateTime</span></span> |
| <span data-ttu-id="bb803-374">Texte</span><span class="sxs-lookup"><span data-stu-id="bb803-374">Text</span></span> | <span data-ttu-id="bb803-375">Varchar (jusqu'à 8 000)</span><span class="sxs-lookup"><span data-stu-id="bb803-375">Varchar (up to 8000)</span></span> |
| <span data-ttu-id="bb803-376">NText</span><span class="sxs-lookup"><span data-stu-id="bb803-376">NText</span></span> | <span data-ttu-id="bb803-377">NVarChar (jusqu'à 4 000)</span><span class="sxs-lookup"><span data-stu-id="bb803-377">NVarChar (up to 4000)</span></span> |
| <span data-ttu-id="bb803-378">Image</span><span class="sxs-lookup"><span data-stu-id="bb803-378">Image</span></span> | <span data-ttu-id="bb803-379">VarBinary (jusqu'à 8 000)</span><span class="sxs-lookup"><span data-stu-id="bb803-379">VarBinary (up to 8000)</span></span> |
| <span data-ttu-id="bb803-380">UniqueIdentifier</span><span class="sxs-lookup"><span data-stu-id="bb803-380">UniqueIdentifier</span></span> | <span data-ttu-id="bb803-381">UniqueIdentifier</span><span class="sxs-lookup"><span data-stu-id="bb803-381">UniqueIdentifier</span></span> |
| <span data-ttu-id="bb803-382">Char</span><span class="sxs-lookup"><span data-stu-id="bb803-382">Char</span></span> | <span data-ttu-id="bb803-383">Char</span><span class="sxs-lookup"><span data-stu-id="bb803-383">Char</span></span> |
| <span data-ttu-id="bb803-384">NChar</span><span class="sxs-lookup"><span data-stu-id="bb803-384">NChar</span></span> | <span data-ttu-id="bb803-385">NChar</span><span class="sxs-lookup"><span data-stu-id="bb803-385">NChar</span></span> |
| <span data-ttu-id="bb803-386">VarChar</span><span class="sxs-lookup"><span data-stu-id="bb803-386">VarChar</span></span> | <span data-ttu-id="bb803-387">VarChar (jusqu'à 8 000)</span><span class="sxs-lookup"><span data-stu-id="bb803-387">VarChar (up to 8000)</span></span> |
| <span data-ttu-id="bb803-388">NVarChar</span><span class="sxs-lookup"><span data-stu-id="bb803-388">NVarChar</span></span> | <span data-ttu-id="bb803-389">NVarChar (jusqu'à 4 000)</span><span class="sxs-lookup"><span data-stu-id="bb803-389">NVarChar (up to 4000)</span></span> |
| <span data-ttu-id="bb803-390">xml</span><span class="sxs-lookup"><span data-stu-id="bb803-390">Xml</span></span> | <span data-ttu-id="bb803-391">Varchar (jusqu'à 8 000)</span><span class="sxs-lookup"><span data-stu-id="bb803-391">Varchar (up to 8000)</span></span> |

[!INCLUDE [data-factory-type-repeatability-for-sql-sources](../../includes/data-factory-type-repeatability-for-sql-sources.md)]

## <a name="type-mapping-for-azure-sql-data-warehouse"></a><span data-ttu-id="bb803-392">Mappage de type pour Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="bb803-392">Type mapping for Azure SQL Data Warehouse</span></span>
<span data-ttu-id="bb803-393">Comme mentionné dans l’article consacré aux [activités de déplacement des données](data-factory-data-movement-activities.md) , l’activité de copie convertit automatiquement les types source en types récepteur à l’aide de l’approche en 2 étapes suivante :</span><span class="sxs-lookup"><span data-stu-id="bb803-393">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="bb803-394">Conversion de types natifs source en types .NET</span><span class="sxs-lookup"><span data-stu-id="bb803-394">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="bb803-395">Conversion de types .NET en types récepteur natifs</span><span class="sxs-lookup"><span data-stu-id="bb803-395">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="bb803-396">Lors du déplacement des données vers et à partir d’Azure SQL Data Warehouse, les mappages suivants sont utilisés à partir du type SQL vers le type .NET et vice-versa.</span><span class="sxs-lookup"><span data-stu-id="bb803-396">When moving data to & from Azure SQL Data Warehouse, the following mappings are used from SQL type to .NET type and vice versa.</span></span>

<span data-ttu-id="bb803-397">Le mappage est identique au [mappage du type de données SQL Server pour ADO.NET](https://msdn.microsoft.com/library/cc716729.aspx)(article en anglais).</span><span class="sxs-lookup"><span data-stu-id="bb803-397">The mapping is same as the [SQL Server Data Type Mapping for ADO.NET](https://msdn.microsoft.com/library/cc716729.aspx).</span></span>

| <span data-ttu-id="bb803-398">Type de moteur de base de données SQL Server</span><span class="sxs-lookup"><span data-stu-id="bb803-398">SQL Server Database Engine type</span></span> | <span data-ttu-id="bb803-399">Type de .NET Framework</span><span class="sxs-lookup"><span data-stu-id="bb803-399">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="bb803-400">bigint</span><span class="sxs-lookup"><span data-stu-id="bb803-400">bigint</span></span> |<span data-ttu-id="bb803-401">Int64</span><span class="sxs-lookup"><span data-stu-id="bb803-401">Int64</span></span> |
| <span data-ttu-id="bb803-402">binaire</span><span class="sxs-lookup"><span data-stu-id="bb803-402">binary</span></span> |<span data-ttu-id="bb803-403">Byte[]</span><span class="sxs-lookup"><span data-stu-id="bb803-403">Byte[]</span></span> |
| <span data-ttu-id="bb803-404">bit</span><span class="sxs-lookup"><span data-stu-id="bb803-404">bit</span></span> |<span data-ttu-id="bb803-405">Boolean</span><span class="sxs-lookup"><span data-stu-id="bb803-405">Boolean</span></span> |
| <span data-ttu-id="bb803-406">char</span><span class="sxs-lookup"><span data-stu-id="bb803-406">char</span></span> |<span data-ttu-id="bb803-407">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="bb803-407">String, Char[]</span></span> |
| <span data-ttu-id="bb803-408">date</span><span class="sxs-lookup"><span data-stu-id="bb803-408">date</span></span> |<span data-ttu-id="bb803-409">DateTime</span><span class="sxs-lookup"><span data-stu-id="bb803-409">DateTime</span></span> |
| <span data-ttu-id="bb803-410">DateTime</span><span class="sxs-lookup"><span data-stu-id="bb803-410">Datetime</span></span> |<span data-ttu-id="bb803-411">DateTime</span><span class="sxs-lookup"><span data-stu-id="bb803-411">DateTime</span></span> |
| <span data-ttu-id="bb803-412">datetime2</span><span class="sxs-lookup"><span data-stu-id="bb803-412">datetime2</span></span> |<span data-ttu-id="bb803-413">DateTime</span><span class="sxs-lookup"><span data-stu-id="bb803-413">DateTime</span></span> |
| <span data-ttu-id="bb803-414">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="bb803-414">Datetimeoffset</span></span> |<span data-ttu-id="bb803-415">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="bb803-415">DateTimeOffset</span></span> |
| <span data-ttu-id="bb803-416">Décimal</span><span class="sxs-lookup"><span data-stu-id="bb803-416">Decimal</span></span> |<span data-ttu-id="bb803-417">Décimal</span><span class="sxs-lookup"><span data-stu-id="bb803-417">Decimal</span></span> |
| <span data-ttu-id="bb803-418">Attribut FILESTREAM (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="bb803-418">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="bb803-419">Byte[]</span><span class="sxs-lookup"><span data-stu-id="bb803-419">Byte[]</span></span> |
| <span data-ttu-id="bb803-420">Float</span><span class="sxs-lookup"><span data-stu-id="bb803-420">Float</span></span> |<span data-ttu-id="bb803-421">Double</span><span class="sxs-lookup"><span data-stu-id="bb803-421">Double</span></span> |
| <span data-ttu-id="bb803-422">image</span><span class="sxs-lookup"><span data-stu-id="bb803-422">image</span></span> |<span data-ttu-id="bb803-423">Byte[]</span><span class="sxs-lookup"><span data-stu-id="bb803-423">Byte[]</span></span> |
| <span data-ttu-id="bb803-424">int</span><span class="sxs-lookup"><span data-stu-id="bb803-424">int</span></span> |<span data-ttu-id="bb803-425">Int32</span><span class="sxs-lookup"><span data-stu-id="bb803-425">Int32</span></span> |
| <span data-ttu-id="bb803-426">money</span><span class="sxs-lookup"><span data-stu-id="bb803-426">money</span></span> |<span data-ttu-id="bb803-427">Décimal</span><span class="sxs-lookup"><span data-stu-id="bb803-427">Decimal</span></span> |
| <span data-ttu-id="bb803-428">nchar</span><span class="sxs-lookup"><span data-stu-id="bb803-428">nchar</span></span> |<span data-ttu-id="bb803-429">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="bb803-429">String, Char[]</span></span> |
| <span data-ttu-id="bb803-430">ntext</span><span class="sxs-lookup"><span data-stu-id="bb803-430">ntext</span></span> |<span data-ttu-id="bb803-431">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="bb803-431">String, Char[]</span></span> |
| <span data-ttu-id="bb803-432">numérique</span><span class="sxs-lookup"><span data-stu-id="bb803-432">numeric</span></span> |<span data-ttu-id="bb803-433">Décimal</span><span class="sxs-lookup"><span data-stu-id="bb803-433">Decimal</span></span> |
| <span data-ttu-id="bb803-434">nvarchar</span><span class="sxs-lookup"><span data-stu-id="bb803-434">nvarchar</span></span> |<span data-ttu-id="bb803-435">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="bb803-435">String, Char[]</span></span> |
| <span data-ttu-id="bb803-436">real</span><span class="sxs-lookup"><span data-stu-id="bb803-436">real</span></span> |<span data-ttu-id="bb803-437">Single</span><span class="sxs-lookup"><span data-stu-id="bb803-437">Single</span></span> |
| <span data-ttu-id="bb803-438">rowversion</span><span class="sxs-lookup"><span data-stu-id="bb803-438">rowversion</span></span> |<span data-ttu-id="bb803-439">Byte[]</span><span class="sxs-lookup"><span data-stu-id="bb803-439">Byte[]</span></span> |
| <span data-ttu-id="bb803-440">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="bb803-440">smalldatetime</span></span> |<span data-ttu-id="bb803-441">DateTime</span><span class="sxs-lookup"><span data-stu-id="bb803-441">DateTime</span></span> |
| <span data-ttu-id="bb803-442">smallint</span><span class="sxs-lookup"><span data-stu-id="bb803-442">smallint</span></span> |<span data-ttu-id="bb803-443">Int16</span><span class="sxs-lookup"><span data-stu-id="bb803-443">Int16</span></span> |
| <span data-ttu-id="bb803-444">smallmoney</span><span class="sxs-lookup"><span data-stu-id="bb803-444">smallmoney</span></span> |<span data-ttu-id="bb803-445">Décimal</span><span class="sxs-lookup"><span data-stu-id="bb803-445">Decimal</span></span> |
| <span data-ttu-id="bb803-446">sql_variant</span><span class="sxs-lookup"><span data-stu-id="bb803-446">sql_variant</span></span> |<span data-ttu-id="bb803-447">Objet *</span><span class="sxs-lookup"><span data-stu-id="bb803-447">Object *</span></span> |
| <span data-ttu-id="bb803-448">texte</span><span class="sxs-lookup"><span data-stu-id="bb803-448">text</span></span> |<span data-ttu-id="bb803-449">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="bb803-449">String, Char[]</span></span> |
| <span data-ttu-id="bb803-450">time</span><span class="sxs-lookup"><span data-stu-id="bb803-450">time</span></span> |<span data-ttu-id="bb803-451">intervalle de temps</span><span class="sxs-lookup"><span data-stu-id="bb803-451">TimeSpan</span></span> |
| <span data-ttu-id="bb803-452">timestamp</span><span class="sxs-lookup"><span data-stu-id="bb803-452">timestamp</span></span> |<span data-ttu-id="bb803-453">Byte[]</span><span class="sxs-lookup"><span data-stu-id="bb803-453">Byte[]</span></span> |
| <span data-ttu-id="bb803-454">tinyint</span><span class="sxs-lookup"><span data-stu-id="bb803-454">tinyint</span></span> |<span data-ttu-id="bb803-455">Byte</span><span class="sxs-lookup"><span data-stu-id="bb803-455">Byte</span></span> |
| <span data-ttu-id="bb803-456">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="bb803-456">uniqueidentifier</span></span> |<span data-ttu-id="bb803-457">Guid</span><span class="sxs-lookup"><span data-stu-id="bb803-457">Guid</span></span> |
| <span data-ttu-id="bb803-458">varbinary</span><span class="sxs-lookup"><span data-stu-id="bb803-458">varbinary</span></span> |<span data-ttu-id="bb803-459">Byte[]</span><span class="sxs-lookup"><span data-stu-id="bb803-459">Byte[]</span></span> |
| <span data-ttu-id="bb803-460">varchar</span><span class="sxs-lookup"><span data-stu-id="bb803-460">varchar</span></span> |<span data-ttu-id="bb803-461">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="bb803-461">String, Char[]</span></span> |
| <span data-ttu-id="bb803-462">xml</span><span class="sxs-lookup"><span data-stu-id="bb803-462">xml</span></span> |<span data-ttu-id="bb803-463">xml</span><span class="sxs-lookup"><span data-stu-id="bb803-463">Xml</span></span> |

<span data-ttu-id="bb803-464">Vous pouvez également mapper les colonnes du jeu de données source sur les colonnes du jeu de données récepteur dans la définition de l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="bb803-464">You can also map columns from source dataset to columns from sink dataset in the copy activity definition.</span></span> <span data-ttu-id="bb803-465">Pour plus d’informations, consultez [Mappage de colonnes de jeux de données dans Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="bb803-465">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="json-examples-for-copying-data-to-and-from-sql-data-warehouse"></a><span data-ttu-id="bb803-466">Exemples JSON pour copier des données vers et depuis SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="bb803-466">JSON examples for copying data to and from SQL Data Warehouse</span></span>
<span data-ttu-id="bb803-467">Les exemples suivants présentent des exemples de définitions de JSON que vous pouvez utiliser pour créer un pipeline à l’aide [du Portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [de Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [d’Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="bb803-467">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="bb803-468">Ils indiquent comment copier des données vers et depuis Azure SQL Data Warehouse et Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="bb803-468">They show how to copy data to and from Azure SQL Data Warehouse and Azure Blob Storage.</span></span> <span data-ttu-id="bb803-469">Toutefois, les données peuvent être copiées **directement** vers l’un des récepteurs indiqués [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) , via l’activité de copie de Microsoft Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="bb803-469">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-azure-sql-data-warehouse-to-azure-blob"></a><span data-ttu-id="bb803-470">Exemple : copie de données depuis Azure SQL Data Warehouse vers un objet Blob Azure</span><span class="sxs-lookup"><span data-stu-id="bb803-470">Example: Copy data from Azure SQL Data Warehouse to Azure Blob</span></span>
<span data-ttu-id="bb803-471">L’exemple définit les entités Data Factory suivantes :</span><span class="sxs-lookup"><span data-stu-id="bb803-471">The sample defines the following Data Factory entities:</span></span>

1. <span data-ttu-id="bb803-472">Un service lié de type [AzureSqlDW](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="bb803-472">A linked service of type [AzureSqlDW](#linked-service-properties).</span></span>
2. <span data-ttu-id="bb803-473">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="bb803-473">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="bb803-474">Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [AzureSqlDWTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="bb803-474">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlDWTable](#dataset-properties).</span></span>
4. <span data-ttu-id="bb803-475">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="bb803-475">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="bb803-476">Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [SqlDWSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="bb803-476">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [SqlDWSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="bb803-477">L’exemple copie toutes les heures les données temporelles (horaire, journalière, etc.) d’une table de base de données Azure SQL Data Warehouse vers un objet blob.</span><span class="sxs-lookup"><span data-stu-id="bb803-477">The sample copies time-series (hourly, daily, etc.) data from a table in Azure SQL Data Warehouse database to a blob every hour.</span></span> <span data-ttu-id="bb803-478">Les propriétés JSON utilisées dans ces exemples sont décrites dans les sections suivant les exemples.</span><span class="sxs-lookup"><span data-stu-id="bb803-478">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="bb803-479">**Service lié Azure SQL Data Warehouse :**</span><span class="sxs-lookup"><span data-stu-id="bb803-479">**Azure SQL Data Warehouse linked service:**</span></span>

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
<span data-ttu-id="bb803-480">**Service lié Azure Blob Storage :**</span><span class="sxs-lookup"><span data-stu-id="bb803-480">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="bb803-481">**Jeu de données d'entrée Azure SQL Data Warehouse :**</span><span class="sxs-lookup"><span data-stu-id="bb803-481">**Azure SQL Data Warehouse input dataset:**</span></span>

<span data-ttu-id="bb803-482">L'exemple suppose que vous avez créé une table « MyTable » dans Azure SQL Data Warehouse et qu'elle contient une colonne appelée « timestampcolumn » pour les données de série chronologique.</span><span class="sxs-lookup"><span data-stu-id="bb803-482">The sample assumes you have created a table “MyTable” in Azure SQL Data Warehouse and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="bb803-483">La définition de « external » : « true» informe le service Data Factory qu’il s’agit d’un jeu de données qui est externe à Data Factory et non produit par une activité dans Data Factory.</span><span class="sxs-lookup"><span data-stu-id="bb803-483">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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
<span data-ttu-id="bb803-484">**Jeu de données de sortie Azure Blob :**</span><span class="sxs-lookup"><span data-stu-id="bb803-484">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="bb803-485">Les données sont écrites dans un nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="bb803-485">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="bb803-486">Le chemin d’accès du dossier pour l’objet blob est évalué dynamiquement en fonction de l’heure de début du segment en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="bb803-486">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="bb803-487">Le chemin d’accès du dossier utilise l’année, le mois, le jour et l’heure de l’heure de début.</span><span class="sxs-lookup"><span data-stu-id="bb803-487">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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

<span data-ttu-id="bb803-488">**Activité de copie dans un pipeline avec SqlDWSource et BlobSink :**</span><span class="sxs-lookup"><span data-stu-id="bb803-488">**Copy activity in a pipeline with SqlDWSource and BlobSink:**</span></span>

<span data-ttu-id="bb803-489">Le pipeline contient une activité de copie qui est configurée pour utiliser les jeux de données d'entrée et de sortie, et qui est planifiée pour s'exécuter toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="bb803-489">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="bb803-490">Dans la définition du pipeline JSON, le type **source** est défini sur **SqlDWSource** et le type **sink** est défini sur **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="bb803-490">In the pipeline JSON definition, the **source** type is set to **SqlDWSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="bb803-491">La requête SQL spécifiée pour la propriété **SqlReaderQuery** sélectionne les données de la dernière heure à copier.</span><span class="sxs-lookup"><span data-stu-id="bb803-491">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

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
> <span data-ttu-id="bb803-492">Dans l’exemple, **sqlReaderQuery** est spécifié pour SqlDWSource.</span><span class="sxs-lookup"><span data-stu-id="bb803-492">In the example, **sqlReaderQuery** is specified for the SqlDWSource.</span></span> <span data-ttu-id="bb803-493">L’activité de copie exécute cette requête sur la source Azure SQL Data Warehouse pour obtenir les données.</span><span class="sxs-lookup"><span data-stu-id="bb803-493">The Copy Activity runs this query against the Azure SQL Data Warehouse source to get the data.</span></span>
>
> <span data-ttu-id="bb803-494">Vous pouvez également spécifier une procédure stockée en indiquant **sqlReaderStoredProcedureName** et **storedProcedureParameters** (si la procédure stockée accepte des paramètres).</span><span class="sxs-lookup"><span data-stu-id="bb803-494">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>
>
> <span data-ttu-id="bb803-495">Si vous ne spécifiez pas sqlReaderQuery ou sqlReaderStoredProcedureName, les colonnes définies dans la section structure du code JSON du jeu de données sont utilisées pour créer une requête (select column1, column2 from mytable) à exécuter sur Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="bb803-495">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section of the dataset JSON are used to build a query (select column1, column2 from mytable) to run against the Azure SQL Data Warehouse.</span></span> <span data-ttu-id="bb803-496">Si la définition du jeu de données ne possède pas de structure, toutes les colonnes de la table sont sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="bb803-496">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>
>
>

### <a name="example-copy-data-from-azure-blob-to-azure-sql-data-warehouse"></a><span data-ttu-id="bb803-497">Exemple : copie de données à partir d’un objet Blob Azure vers Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="bb803-497">Example: Copy data from Azure Blob to Azure SQL Data Warehouse</span></span>
<span data-ttu-id="bb803-498">L’exemple définit les entités Data Factory suivantes :</span><span class="sxs-lookup"><span data-stu-id="bb803-498">The sample defines the following Data Factory entities:</span></span>

1. <span data-ttu-id="bb803-499">Un service lié de type [AzureSqlDW](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="bb803-499">A linked service of type [AzureSqlDW](#linked-service-properties).</span></span>
2. <span data-ttu-id="bb803-500">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="bb803-500">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="bb803-501">un [jeu de données](data-factory-create-datasets.md) d'entrée de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="bb803-501">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="bb803-502">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureSqlDWTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="bb803-502">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlDWTable](#dataset-properties).</span></span>
5. <span data-ttu-id="bb803-503">Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) et [SqlDWSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="bb803-503">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlDWSink](#copy-activity-properties).</span></span>

<span data-ttu-id="bb803-504">L’exemple copie toutes les heures les données temporelles (horaire, journalière, etc.) d’un objet blob Azure vers une table de base de données Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="bb803-504">The sample copies time-series data (hourly, daily, etc.) from Azure blob to a table in Azure SQL Data Warehouse database every hour.</span></span> <span data-ttu-id="bb803-505">Les propriétés JSON utilisées dans ces exemples sont décrites dans les sections suivant les exemples.</span><span class="sxs-lookup"><span data-stu-id="bb803-505">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="bb803-506">**Service lié Azure SQL Data Warehouse :**</span><span class="sxs-lookup"><span data-stu-id="bb803-506">**Azure SQL Data Warehouse linked service:**</span></span>

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
<span data-ttu-id="bb803-507">**Service lié Azure Blob Storage :**</span><span class="sxs-lookup"><span data-stu-id="bb803-507">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="bb803-508">**Jeu de données d'entrée d'objet Blob Azure :**</span><span class="sxs-lookup"><span data-stu-id="bb803-508">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="bb803-509">Les données sont récupérées à partir d'un nouvel objet Blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="bb803-509">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="bb803-510">Le nom du chemin d'accès et du fichier de dossier pour l'objet blob sont évalués dynamiquement en fonction de l'heure de début du segment en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="bb803-510">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="bb803-511">Le chemin d’accès du dossier utilise l’année, le mois et le jour de début et le nom de fichier utilise l’heure de début.</span><span class="sxs-lookup"><span data-stu-id="bb803-511">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="bb803-512">Le paramètre « external » : « true » informe le service Data Factory que cette table est externe à la fabrique de données et n’est pas produite par une activité dans la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="bb803-512">“external”: “true” setting informs the Data Factory service that this table is external to the data factory and is not produced by an activity in the data factory.</span></span>

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
<span data-ttu-id="bb803-513">**Jeu de données de sortie Azure SQL Data Warehouse :**</span><span class="sxs-lookup"><span data-stu-id="bb803-513">**Azure SQL Data Warehouse output dataset:**</span></span>

<span data-ttu-id="bb803-514">L'exemple copie les données dans une table nommée « MyTable » dans Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="bb803-514">The sample copies data to a table named “MyTable” in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="bb803-515">Créez la table dans Azure SQL Data Warehouse avec le même nombre de colonnes que le fichier CSV d’objets blob doit en contenir.</span><span class="sxs-lookup"><span data-stu-id="bb803-515">Create the table in Azure SQL Data Warehouse with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="bb803-516">De nouvelles lignes sont ajoutées à la table toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="bb803-516">New rows are added to the table every hour.</span></span>

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
<span data-ttu-id="bb803-517">**Activité de copie dans un pipeline avec BlobSource et SqlDWSink :**</span><span class="sxs-lookup"><span data-stu-id="bb803-517">**Copy activity in a pipeline with BlobSource and SqlDWSink:**</span></span>

<span data-ttu-id="bb803-518">Le pipeline contient une activité de copie qui est configurée pour utiliser les jeux de données d'entrée et de sortie, et qui est planifiée pour s'exécuter toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="bb803-518">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="bb803-519">Dans la définition JSON du pipeline, le type **source** est défini sur **BlobSource** et le type **sink** est défini sur **SqlDWSink**.</span><span class="sxs-lookup"><span data-stu-id="bb803-519">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlDWSink**.</span></span>

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
<span data-ttu-id="bb803-520">Pour une procédure pas à pas, voir [Charger 1 To dans Azure SQL Data Warehouse en moins de 15 minutes avec Azure Data Factory](data-factory-load-sql-data-warehouse.md) et l’article [Charger des données avec Azure Data Factory](../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md) dans la documentation de SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="bb803-520">For a walkthrough, see the see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md) and [Load data with Azure Data Factory](../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md) article in the Azure SQL Data Warehouse documentation.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="bb803-521">Performances et réglage</span><span class="sxs-lookup"><span data-stu-id="bb803-521">Performance and Tuning</span></span>
<span data-ttu-id="bb803-522">Consultez l’article [Guide sur les performances et le réglage de l’activité de copie](data-factory-copy-activity-performance.md) pour en savoir plus sur les facteurs clés affectant les performances de déplacement des données (activité de copie) dans Azure Data Factory et les différentes manières de les optimiser.</span><span class="sxs-lookup"><span data-stu-id="bb803-522">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
