---
title: "aaaLoad à partir de l’entrepôt de données objet blob Azure tooAzure | Documents Microsoft"
description: "Découvrez comment les données tooload Azure toouse PolyBase stockage d’objets blob dans SQL Data Warehouse. Charger plusieurs tables à partir de données publics dans le schéma d’entrepôt de données Contoso Retail hello."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: faca0fe7-62e7-4e1f-a86f-032b4ffcb06e
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 4b4978ccefa4d55ff5c89fba84c5e705422ddbb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-azure-blob-storage-into-sql-data-warehouse-polybase"></a><span data-ttu-id="8739c-104">Charger les données de stockage d’objets blob Azure dans SQL Data Warehouse (PolyBase)</span><span class="sxs-lookup"><span data-stu-id="8739c-104">Load data from Azure blob storage into SQL Data Warehouse (PolyBase)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8739c-105">Data Factory</span><span class="sxs-lookup"><span data-stu-id="8739c-105">Data Factory</span></span>](sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md)
> * [<span data-ttu-id="8739c-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="8739c-106">PolyBase</span></span>](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md)
> 
> 

<span data-ttu-id="8739c-107">Utilisez PolyBase T-SQL commandes tooload les données et de stockage d’objets blob Azure dans Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="8739c-107">Use PolyBase and T-SQL commands tooload data from Azure blob storage into Azure SQL Data Warehouse.</span></span> 

<span data-ttu-id="8739c-108">tookeep il simple, ce didacticiel charge deux tables à partir d’un objet Blob de stockage Azure publics dans le schéma d’entrepôt de données Contoso Retail hello.</span><span class="sxs-lookup"><span data-stu-id="8739c-108">tookeep it simple, this tutorial loads two tables from a public Azure Storage Blob into hello Contoso Retail Data Warehouse schema.</span></span> <span data-ttu-id="8739c-109">tooload hello jeu complet de données, exécutez l’exemple de hello [charge hello complète l’entrepôt de données Contoso Retail] [ Load hello full Contoso Retail Data Warehouse] à partir du référentiel de Microsoft SQL Server Samples hello.</span><span class="sxs-lookup"><span data-stu-id="8739c-109">tooload hello full data set, run hello example [Load hello full Contoso Retail Data Warehouse][Load hello full Contoso Retail Data Warehouse] from hello Microsoft SQL Server Samples repository.</span></span>

<span data-ttu-id="8739c-110">Ce didacticiel vous apprendra à effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="8739c-110">In this tutorial you will:</span></span>

1. <span data-ttu-id="8739c-111">Configurer tooload PolyBase depuis le stockage blob Azure</span><span class="sxs-lookup"><span data-stu-id="8739c-111">Configure PolyBase tooload from Azure blob storage</span></span>
2. <span data-ttu-id="8739c-112">Charger des données publiques dans votre base de données</span><span class="sxs-lookup"><span data-stu-id="8739c-112">Load public data into your database</span></span>
3. <span data-ttu-id="8739c-113">Effectuer des optimisations issue de la charge de hello.</span><span class="sxs-lookup"><span data-stu-id="8739c-113">Perform optimizations after hello load is finished.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8739c-114">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="8739c-114">Before you begin</span></span>
<span data-ttu-id="8739c-115">toorun ce didacticiel, vous avez besoin d’un compte Azure qui a déjà une base de données SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="8739c-115">toorun this tutorial, you need an Azure account that already has a SQL Data Warehouse database.</span></span> <span data-ttu-id="8739c-116">Si vous n’en disposez pas, consultez la page [Créer un entrepôt de données SQL][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="8739c-116">If you don't already have this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>

## <a name="1-configure-hello-data-source"></a><span data-ttu-id="8739c-117">1. Configurer la source de données hello</span><span class="sxs-lookup"><span data-stu-id="8739c-117">1. Configure hello data source</span></span>
<span data-ttu-id="8739c-118">PolyBase utilise l’emplacement de T-SQL des objets externes toodefine hello et les attributs de données externes de hello.</span><span class="sxs-lookup"><span data-stu-id="8739c-118">PolyBase uses T-SQL external objects toodefine hello location and attributes of hello external data.</span></span> <span data-ttu-id="8739c-119">définitions de l’objet externe Hello sont stockées dans l’entrepôt de données SQL.</span><span class="sxs-lookup"><span data-stu-id="8739c-119">hello external object definitions are stored in SQL Data Warehouse.</span></span> <span data-ttu-id="8739c-120">données Hello proprement dites sont stockées en externe.</span><span class="sxs-lookup"><span data-stu-id="8739c-120">hello data itself is stored externally.</span></span>

### <a name="11-create-a-credential"></a><span data-ttu-id="8739c-121">1.1.</span><span class="sxs-lookup"><span data-stu-id="8739c-121">1.1.</span></span> <span data-ttu-id="8739c-122">Créer des informations d’identification</span><span class="sxs-lookup"><span data-stu-id="8739c-122">Create a credential</span></span>
<span data-ttu-id="8739c-123">**Ignorez cette étape** si vous chargez des données publiques de Contoso hello.</span><span class="sxs-lookup"><span data-stu-id="8739c-123">**Skip this step** if you are loading hello Contoso public data.</span></span> <span data-ttu-id="8739c-124">Vous n’avez pas besoin données publiques de sécuriser l’accès toohello car il est déjà tooanyone accessible.</span><span class="sxs-lookup"><span data-stu-id="8739c-124">You don't need secure access toohello public data since it is already accessible tooanyone.</span></span>

<span data-ttu-id="8739c-125">**N’ignorez pas cette étape** si vous utilisez ce didacticiel comme modèle pour le chargement de vos propres données.</span><span class="sxs-lookup"><span data-stu-id="8739c-125">**Don't skip this step** if you are using this tutorial as a template for loading your own data.</span></span> <span data-ttu-id="8739c-126">tooaccess des données via les informations d’identification, hello utilisation suivant toocreate une étendue de base de données d’informations d’identification de script et ensuite l’utiliser lors de la définition d’emplacement hello hello de source de données.</span><span class="sxs-lookup"><span data-stu-id="8739c-126">tooaccess data through a credential, use hello following script toocreate a database-scoped credential, and then use it when defining hello location of hello data source.</span></span>

```sql
-- A: Create a master key.
-- Only necessary if one does not already exist.
-- Required tooencrypt hello credential secret in hello next step.

CREATE MASTER KEY;


-- B: Create a database scoped credential
-- IDENTITY: Provide any string, it is not used for authentication tooAzure storage.
-- SECRET: Provide your Azure storage account key.


CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential
WITH
    IDENTITY = 'user',
    SECRET = '<azure_storage_account_key>'
;


-- C: Create an external data source
-- TYPE: HADOOP - PolyBase uses Hadoop APIs tooaccess data in Azure blob storage.
-- LOCATION: Provide Azure storage account name and blob container name.
-- CREDENTIAL: Provide hello credential created in hello previous step.

CREATE EXTERNAL DATA SOURCE AzureStorage
WITH (
    TYPE = HADOOP,
    LOCATION = 'wasbs://<blob_container_name>@<azure_storage_account_name>.blob.core.windows.net',
    CREDENTIAL = AzureStorageCredential
);
```

<span data-ttu-id="8739c-127">Ignorer toostep 2.</span><span class="sxs-lookup"><span data-stu-id="8739c-127">Skip toostep 2.</span></span>

### <a name="12-create-hello-external-data-source"></a><span data-ttu-id="8739c-128">1.2.</span><span class="sxs-lookup"><span data-stu-id="8739c-128">1.2.</span></span> <span data-ttu-id="8739c-129">Créer la source de données externe hello</span><span class="sxs-lookup"><span data-stu-id="8739c-129">Create hello external data source</span></span>
<span data-ttu-id="8739c-130">Utilisez cette [CREATE EXTERNAL DATA SOURCE] [ CREATE EXTERNAL DATA SOURCE] emplacement de hello toostore des données de hello et type hello de données de commande.</span><span class="sxs-lookup"><span data-stu-id="8739c-130">Use this [CREATE EXTERNAL DATA SOURCE][CREATE EXTERNAL DATA SOURCE] command toostore hello location of hello data, and hello type of data.</span></span> 

```sql
CREATE EXTERNAL DATA SOURCE AzureStorage_west_public
WITH 
(  
    TYPE = Hadoop 
,   LOCATION = 'wasbs://contosoretaildw-tables@contosoretaildw.blob.core.windows.net/'
); 
```

> [!IMPORTANT]
> <span data-ttu-id="8739c-131">Si vous choisissez toomake votre public de conteneurs de stockage blob azure, souvenez-vous qu’en tant que propriétaire de données hello vous serez facturé pour les données frais de sortie lorsque des données quittent le centre de données hello.</span><span class="sxs-lookup"><span data-stu-id="8739c-131">If you choose toomake your azure blob storage containers public, remember that as hello data owner you will be charged for data egress charges when data leaves hello data center.</span></span> 
> 
> 

## <a name="2-configure-data-format"></a><span data-ttu-id="8739c-132">2. Configurer le format des données</span><span class="sxs-lookup"><span data-stu-id="8739c-132">2. Configure data format</span></span>
<span data-ttu-id="8739c-133">les données de Hello sont stockées dans des fichiers texte dans le stockage blob Azure, et chaque champ est séparé par un délimiteur.</span><span class="sxs-lookup"><span data-stu-id="8739c-133">hello data is stored in text files in Azure blob storage, and each field is separated with a delimiter.</span></span> <span data-ttu-id="8739c-134">Exécutez ce [CREATE EXTERNAL FILE FORMAT] [ CREATE EXTERNAL FILE FORMAT] format de hello toospecify de commande de données hello dans les fichiers de texte hello.</span><span class="sxs-lookup"><span data-stu-id="8739c-134">Run this [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT] command toospecify hello format of hello data in hello text files.</span></span> <span data-ttu-id="8739c-135">Hello Contoso données n’est pas compressé et délimités de canal.</span><span class="sxs-lookup"><span data-stu-id="8739c-135">hello Contoso data is uncompressed and pipe delimited.</span></span>

```sql
CREATE EXTERNAL FILE FORMAT TextFileFormat 
WITH 
(   FORMAT_TYPE = DELIMITEDTEXT
,    FORMAT_OPTIONS    (   FIELD_TERMINATOR = '|'
                    ,    STRING_DELIMITER = ''
                    ,    DATE_FORMAT         = 'yyyy-MM-dd HH:mm:ss.fff'
                    ,    USE_TYPE_DEFAULT = FALSE 
                    )
);
``` 

## <a name="3-create-hello-external-tables"></a><span data-ttu-id="8739c-136">3. Créer des tables externes hello</span><span class="sxs-lookup"><span data-stu-id="8739c-136">3. Create hello external tables</span></span>
<span data-ttu-id="8739c-137">Maintenant que vous avez spécifié hello données source et formats de fichier, vous êtes prêt toocreate des tables externes hello.</span><span class="sxs-lookup"><span data-stu-id="8739c-137">Now that you have specified hello data source and file format, you are ready toocreate hello external tables.</span></span> 

### <a name="31-create-a-schema-for-hello-data"></a><span data-ttu-id="8739c-138">3.1.</span><span class="sxs-lookup"><span data-stu-id="8739c-138">3.1.</span></span> <span data-ttu-id="8739c-139">Créer un schéma pour les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="8739c-139">Create a schema for hello data.</span></span>
<span data-ttu-id="8739c-140">toocreate un Bonjour de toostore place Contoso des données dans votre base de données, créer un schéma.</span><span class="sxs-lookup"><span data-stu-id="8739c-140">toocreate a place toostore hello Contoso data in your database, create a schema.</span></span>

```sql
CREATE SCHEMA [asb]
GO
```

### <a name="32-create-hello-external-tables"></a><span data-ttu-id="8739c-141">3.2.</span><span class="sxs-lookup"><span data-stu-id="8739c-141">3.2.</span></span> <span data-ttu-id="8739c-142">Créer des tables externes hello.</span><span class="sxs-lookup"><span data-stu-id="8739c-142">Create hello external tables.</span></span>
<span data-ttu-id="8739c-143">Exécutez cette hello toocreate de script DimProduct et FactOnlineSales des tables externes.</span><span class="sxs-lookup"><span data-stu-id="8739c-143">Run this script toocreate hello DimProduct and FactOnlineSales external tables.</span></span> <span data-ttu-id="8739c-144">Nous essayons ici est définition des noms de colonnes et les types de données et les lier à l’emplacement de toohello et le format des fichiers de stockage d’objets blob Azure hello.</span><span class="sxs-lookup"><span data-stu-id="8739c-144">All we are doing here is defining column names and data types, and binding them toohello location and format of hello Azure blob storage files.</span></span> <span data-ttu-id="8739c-145">définition de Hello est stockée dans l’entrepôt de données SQL et les données de salutation sont toujours en hello objet Blob de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="8739c-145">hello definition is stored in SQL Data Warehouse and hello data is still in hello Azure Storage Blob.</span></span>

<span data-ttu-id="8739c-146">Hello **emplacement** paramètre est le dossier hello sous le dossier racine de hello Bonjour objet Blob de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="8739c-146">hello  **LOCATION** parameter is hello folder under hello root folder in hello Azure Storage Blob.</span></span> <span data-ttu-id="8739c-147">Chaque table se trouve dans un dossier spécifique.</span><span class="sxs-lookup"><span data-stu-id="8739c-147">Each table is in a different folder.</span></span>

```sql

--DimProduct
CREATE EXTERNAL TABLE [asb].DimProduct (
    [ProductKey] [int] NOT NULL,
    [ProductLabel] [nvarchar](255) NULL,
    [ProductName] [nvarchar](500) NULL,
    [ProductDescription] [nvarchar](400) NULL,
    [ProductSubcategoryKey] [int] NULL,
    [Manufacturer] [nvarchar](50) NULL,
    [BrandName] [nvarchar](50) NULL,
    [ClassID] [nvarchar](10) NULL,
    [ClassName] [nvarchar](20) NULL,
    [StyleID] [nvarchar](10) NULL,
    [StyleName] [nvarchar](20) NULL,
    [ColorID] [nvarchar](10) NULL,
    [ColorName] [nvarchar](20) NOT NULL,
    [Size] [nvarchar](50) NULL,
    [SizeRange] [nvarchar](50) NULL,
    [SizeUnitMeasureID] [nvarchar](20) NULL,
    [Weight] [float] NULL,
    [WeightUnitMeasureID] [nvarchar](20) NULL,
    [UnitOfMeasureID] [nvarchar](10) NULL,
    [UnitOfMeasureName] [nvarchar](40) NULL,
    [StockTypeID] [nvarchar](10) NULL,
    [StockTypeName] [nvarchar](40) NULL,
    [UnitCost] [money] NULL,
    [UnitPrice] [money] NULL,
    [AvailableForSaleDate] [datetime] NULL,
    [StopSaleDate] [datetime] NULL,
    [Status] [nvarchar](7) NULL,
    [ImageURL] [nvarchar](150) NULL,
    [ProductURL] [nvarchar](150) NULL,
    [ETLLoadID] [int] NULL,
    [LoadDate] [datetime] NULL,
    [UpdateDate] [datetime] NULL
)
WITH
(
    LOCATION='/DimProduct/' 
,   DATA_SOURCE = AzureStorage_west_public
,   FILE_FORMAT = TextFileFormat
,   REJECT_TYPE = VALUE
,   REJECT_VALUE = 0
)
;

--FactOnlineSales
CREATE EXTERNAL TABLE [asb].FactOnlineSales 
(
    [OnlineSalesKey] [int]  NOT NULL,
    [DateKey] [datetime] NOT NULL,
    [StoreKey] [int] NOT NULL,
    [ProductKey] [int] NOT NULL,
    [PromotionKey] [int] NOT NULL,
    [CurrencyKey] [int] NOT NULL,
    [CustomerKey] [int] NOT NULL,
    [SalesOrderNumber] [nvarchar](20) NOT NULL,
    [SalesOrderLineNumber] [int] NULL,
    [SalesQuantity] [int] NOT NULL,
    [SalesAmount] [money] NOT NULL,
    [ReturnQuantity] [int] NOT NULL,
    [ReturnAmount] [money] NULL,
    [DiscountQuantity] [int] NULL,
    [DiscountAmount] [money] NULL,
    [TotalCost] [money] NOT NULL,
    [UnitCost] [money] NULL,
    [UnitPrice] [money] NULL,
    [ETLLoadID] [int] NULL,
    [LoadDate] [datetime] NULL,
    [UpdateDate] [datetime] NULL
)
WITH
(
    LOCATION='/FactOnlineSales/' 
,   DATA_SOURCE = AzureStorage_west_public
,   FILE_FORMAT = TextFileFormat
,   REJECT_TYPE = VALUE
,   REJECT_VALUE = 0
)
;
```

## <a name="4-load-hello-data"></a><span data-ttu-id="8739c-148">4. Charger des données hello</span><span class="sxs-lookup"><span data-stu-id="8739c-148">4. Load hello data</span></span>
<span data-ttu-id="8739c-149">Il existe des données externes tooaccess de différentes façons.</span><span class="sxs-lookup"><span data-stu-id="8739c-149">There's different ways tooaccess external data.</span></span>  <span data-ttu-id="8739c-150">Vous pouvez interroger les données directement à partir d’une table externe hello, charger les données de hello dans de nouvelles tables de base de données ou ajouter des tables de base de données tooexisting de données externes.</span><span class="sxs-lookup"><span data-stu-id="8739c-150">You can query data directly from hello external table, load hello data into new database tables, or add external data tooexisting database tables.</span></span>  

### <a name="41-create-a-new-schema"></a><span data-ttu-id="8739c-151">4.1.</span><span class="sxs-lookup"><span data-stu-id="8739c-151">4.1.</span></span> <span data-ttu-id="8739c-152">Créer un schéma</span><span class="sxs-lookup"><span data-stu-id="8739c-152">Create a new schema</span></span>
<span data-ttu-id="8739c-153">CTAS crée une table qui contient des données.</span><span class="sxs-lookup"><span data-stu-id="8739c-153">CTAS creates a new table that contains data.</span></span>  <span data-ttu-id="8739c-154">Commencez par créer un schéma pour les données de contoso hello.</span><span class="sxs-lookup"><span data-stu-id="8739c-154">First, create a schema for hello contoso data.</span></span>

```sql
CREATE SCHEMA [cso]
GO
```

### <a name="42-load-hello-data-into-new-tables"></a><span data-ttu-id="8739c-155">4.2.</span><span class="sxs-lookup"><span data-stu-id="8739c-155">4.2.</span></span> <span data-ttu-id="8739c-156">Charger des données dans de nouvelles tables hello</span><span class="sxs-lookup"><span data-stu-id="8739c-156">Load hello data into new tables</span></span>
<span data-ttu-id="8739c-157">données tooload à partir d’Azure stockage d’objets blob et enregistrez-le dans une table à l’intérieur de votre base de données, utilisez hello [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] instruction.</span><span class="sxs-lookup"><span data-stu-id="8739c-157">tooload data from Azure blob storage and save it in a table inside of your database, use hello [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] statement.</span></span> <span data-ttu-id="8739c-158">Chargement avec SACT tire parti hello fortement typée des tables externes, vous disposez de données de hello created.tooload simplement dans de nouvelles tables, utilisez une [SACT] [ CTAS] instruction par table.</span><span class="sxs-lookup"><span data-stu-id="8739c-158">Loading with CTAS leverages hello strongly typed external tables you have just created.tooload hello data into new tables, use one [CTAS][CTAS] statement per table.</span></span> 
 
<span data-ttu-id="8739c-159">SACT crée une nouvelle table et le remplit avec des résultats d’une instruction select hello.</span><span class="sxs-lookup"><span data-stu-id="8739c-159">CTAS creates a new table and populates it with hello results of a select statement.</span></span> <span data-ttu-id="8739c-160">SACT définit hello nouvelle table toohave hello les mêmes colonnes et types de données comme résultats hello Hello select (instruction).</span><span class="sxs-lookup"><span data-stu-id="8739c-160">CTAS defines hello new table toohave hello same columns and data types as hello results of hello select statement.</span></span> <span data-ttu-id="8739c-161">Si vous sélectionnez toutes les colonnes hello à partir d’une table externe, la nouvelle table de hello sera un réplica de types de données et des colonnes de hello dans une table externe hello.</span><span class="sxs-lookup"><span data-stu-id="8739c-161">If you select all hello columns from an external table, hello new table will be a replica of hello columns and data types in hello external table.</span></span>

<span data-ttu-id="8739c-162">Dans cet exemple, nous créons des dimension de hello et table de faits hello en tant que tables distribuées de hachage.</span><span class="sxs-lookup"><span data-stu-id="8739c-162">In this example, we create both hello dimension and hello fact table as hash distributed tables.</span></span> 

```sql
SELECT GETDATE();
GO

CREATE TABLE [cso].[DimProduct]            WITH (DISTRIBUTION = HASH([ProductKey]  ) ) AS SELECT * FROM [asb].[DimProduct]             OPTION (LABEL = 'CTAS : Load [cso].[DimProduct]             ');
CREATE TABLE [cso].[FactOnlineSales]       WITH (DISTRIBUTION = HASH([ProductKey]  ) ) AS SELECT * FROM [asb].[FactOnlineSales]        OPTION (LABEL = 'CTAS : Load [cso].[FactOnlineSales]        ');
```

### <a name="43-track-hello-load-progress"></a><span data-ttu-id="8739c-163">4.3 suivre la progression du chargement hello</span><span class="sxs-lookup"><span data-stu-id="8739c-163">4.3 Track hello load progress</span></span>
<span data-ttu-id="8739c-164">Vous pouvez suivre la progression de hello de votre charge à l’aide de vues de gestion dynamique (DMV).</span><span class="sxs-lookup"><span data-stu-id="8739c-164">You can track hello progress of your load using dynamic management views (DMVs).</span></span> 

```sql
-- toosee all requests
SELECT * FROM sys.dm_pdw_exec_requests;

-- toosee a particular request identified by its label
SELECT * FROM sys.dm_pdw_exec_requests as r
WHERE r.[label] = 'CTAS : Load [cso].[DimProduct]             '
      OR r.[label] = 'CTAS : Load [cso].[FactOnlineSales]        '
;

-- tootrack bytes and files
SELECT
    r.command,
    s.request_id,
    r.status,
    count(distinct input_name) as nbr_files, 
    sum(s.bytes_processed)/1024/1024/1024 as gb_processed
FROM
    sys.dm_pdw_exec_requests r
    inner join sys.dm_pdw_dms_external_work s
        on r.request_id = s.request_id
WHERE 
    r.[label] = 'CTAS : Load [cso].[DimProduct]             '
    OR r.[label] = 'CTAS : Load [cso].[FactOnlineSales]        '
GROUP BY
    r.command,
    s.request_id,
    r.status
ORDER BY
    nbr_files desc,
    gb_processed desc;
```

## <a name="5-optimize-columnstore-compression"></a><span data-ttu-id="8739c-165">5. Optimiser la compression columnstore</span><span class="sxs-lookup"><span data-stu-id="8739c-165">5. Optimize columnstore compression</span></span>
<span data-ttu-id="8739c-166">Par défaut, SQL Data Warehouse stocke la table de hello en tant qu’un index cluster columnstore.</span><span class="sxs-lookup"><span data-stu-id="8739c-166">By default, SQL Data Warehouse stores hello table as a clustered columnstore index.</span></span> <span data-ttu-id="8739c-167">Après un chargement, certains hello lignes de données ne peuvent pas être compressé au hello columnstore.</span><span class="sxs-lookup"><span data-stu-id="8739c-167">After a load completes, some of hello data rows might not be compressed into hello columnstore.</span></span>  <span data-ttu-id="8739c-168">Cela peut être dû à diverses raisons.</span><span class="sxs-lookup"><span data-stu-id="8739c-168">There's a variety of reasons why this can happen.</span></span> <span data-ttu-id="8739c-169">toolearn, voir [gérer les index columnstore][manage columnstore indexes].</span><span class="sxs-lookup"><span data-stu-id="8739c-169">toolearn more, see [manage columnstore indexes][manage columnstore indexes].</span></span>

<span data-ttu-id="8739c-170">performances des requêtes toooptimize et la compression de columnstore après un chargement, reconstruire hello table tooforce hello columnstore index toocompress toutes les lignes hello.</span><span class="sxs-lookup"><span data-stu-id="8739c-170">toooptimize query performance and columnstore compression after a load, rebuild hello table tooforce hello columnstore index toocompress all hello rows.</span></span> 

```sql
SELECT GETDATE();
GO

ALTER INDEX ALL ON [cso].[DimProduct]               REBUILD;
ALTER INDEX ALL ON [cso].[FactOnlineSales]          REBUILD;
```

<span data-ttu-id="8739c-171">Pour plus d’informations sur la gestion des index columnstore, consultez hello [gérer les index columnstore] [ manage columnstore indexes] l’article.</span><span class="sxs-lookup"><span data-stu-id="8739c-171">For more information on maintaining columnstore indexes, see hello [manage columnstore indexes][manage columnstore indexes] article.</span></span>

## <a name="6-optimize-statistics"></a><span data-ttu-id="8739c-172">6. Optimiser les statistiques</span><span class="sxs-lookup"><span data-stu-id="8739c-172">6. Optimize statistics</span></span>
<span data-ttu-id="8739c-173">Il s’agit des statistiques de colonne unique toocreate meilleures immédiatement après un chargement.</span><span class="sxs-lookup"><span data-stu-id="8739c-173">It is best toocreate single-column statistics immediately after a load.</span></span> <span data-ttu-id="8739c-174">Les statistiques offrent plusieurs possibilités.</span><span class="sxs-lookup"><span data-stu-id="8739c-174">There are some choices for statistics.</span></span> <span data-ttu-id="8739c-175">Par exemple, si vous créez des statistiques de colonnes uniques sur toutes les colonnes qu’il peut prendre un toorebuild beaucoup de temps toutes les statistiques de hello.</span><span class="sxs-lookup"><span data-stu-id="8739c-175">For example, if you create single-column statistics on every column it might take a long time toorebuild all hello statistics.</span></span> <span data-ttu-id="8739c-176">Si vous savez que certaines colonnes ne vont pas toobe dans les prédicats de requête, vous pouvez ignorer la création des statistiques sur les colonnes.</span><span class="sxs-lookup"><span data-stu-id="8739c-176">If you know certain columns are not going toobe in query predicates, you can skip creating statistics on those columns.</span></span>

<span data-ttu-id="8739c-177">Si vous décidez de toocreate les statistiques de colonnes uniques sur chaque colonne de chaque table, vous pouvez utiliser les exemples de code de procédure stockée hello `prc_sqldw_create_stats` Bonjour [statistiques] [ statistics] l’article.</span><span class="sxs-lookup"><span data-stu-id="8739c-177">If you decide toocreate single-column statistics on every column of every table, you can use hello stored procedure code sample `prc_sqldw_create_stats` in hello [statistics][statistics] article.</span></span>

<span data-ttu-id="8739c-178">Bonjour à l’exemple suivant est un bon point de départ pour la création de statistiques.</span><span class="sxs-lookup"><span data-stu-id="8739c-178">hello following example is a good starting point for creating statistics.</span></span> <span data-ttu-id="8739c-179">Il crée des statistiques de colonnes uniques sur chaque colonne de table de dimension hello et sur chaque colonne de jointure dans des tables de faits hello.</span><span class="sxs-lookup"><span data-stu-id="8739c-179">It creates single-column statistics on each column in hello dimension table, and on each joining column in hello fact tables.</span></span> <span data-ttu-id="8739c-180">Vous pouvez toujours ajouter des colonnes de table de faits unique ou plusieurs colonnes de statistiques tooother ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="8739c-180">You can always add single or multi-column statistics tooother fact table columns later on.</span></span>

```sql
CREATE STATISTICS [stat_cso_DimProduct_AvailableForSaleDate] ON [cso].[DimProduct]([AvailableForSaleDate]);
CREATE STATISTICS [stat_cso_DimProduct_BrandName] ON [cso].[DimProduct]([BrandName]);
CREATE STATISTICS [stat_cso_DimProduct_ClassID] ON [cso].[DimProduct]([ClassID]);
CREATE STATISTICS [stat_cso_DimProduct_ClassName] ON [cso].[DimProduct]([ClassName]);
CREATE STATISTICS [stat_cso_DimProduct_ColorID] ON [cso].[DimProduct]([ColorID]);
CREATE STATISTICS [stat_cso_DimProduct_ColorName] ON [cso].[DimProduct]([ColorName]);
CREATE STATISTICS [stat_cso_DimProduct_ETLLoadID] ON [cso].[DimProduct]([ETLLoadID]);
CREATE STATISTICS [stat_cso_DimProduct_ImageURL] ON [cso].[DimProduct]([ImageURL]);
CREATE STATISTICS [stat_cso_DimProduct_LoadDate] ON [cso].[DimProduct]([LoadDate]);
CREATE STATISTICS [stat_cso_DimProduct_Manufacturer] ON [cso].[DimProduct]([Manufacturer]);
CREATE STATISTICS [stat_cso_DimProduct_ProductDescription] ON [cso].[DimProduct]([ProductDescription]);
CREATE STATISTICS [stat_cso_DimProduct_ProductKey] ON [cso].[DimProduct]([ProductKey]);
CREATE STATISTICS [stat_cso_DimProduct_ProductLabel] ON [cso].[DimProduct]([ProductLabel]);
CREATE STATISTICS [stat_cso_DimProduct_ProductName] ON [cso].[DimProduct]([ProductName]);
CREATE STATISTICS [stat_cso_DimProduct_ProductSubcategoryKey] ON [cso].[DimProduct]([ProductSubcategoryKey]);
CREATE STATISTICS [stat_cso_DimProduct_ProductURL] ON [cso].[DimProduct]([ProductURL]);
CREATE STATISTICS [stat_cso_DimProduct_Size] ON [cso].[DimProduct]([Size]);
CREATE STATISTICS [stat_cso_DimProduct_SizeRange] ON [cso].[DimProduct]([SizeRange]);
CREATE STATISTICS [stat_cso_DimProduct_SizeUnitMeasureID] ON [cso].[DimProduct]([SizeUnitMeasureID]);
CREATE STATISTICS [stat_cso_DimProduct_Status] ON [cso].[DimProduct]([Status]);
CREATE STATISTICS [stat_cso_DimProduct_StockTypeID] ON [cso].[DimProduct]([StockTypeID]);
CREATE STATISTICS [stat_cso_DimProduct_StockTypeName] ON [cso].[DimProduct]([StockTypeName]);
CREATE STATISTICS [stat_cso_DimProduct_StopSaleDate] ON [cso].[DimProduct]([StopSaleDate]);
CREATE STATISTICS [stat_cso_DimProduct_StyleID] ON [cso].[DimProduct]([StyleID]);
CREATE STATISTICS [stat_cso_DimProduct_StyleName] ON [cso].[DimProduct]([StyleName]);
CREATE STATISTICS [stat_cso_DimProduct_UnitCost] ON [cso].[DimProduct]([UnitCost]);
CREATE STATISTICS [stat_cso_DimProduct_UnitOfMeasureID] ON [cso].[DimProduct]([UnitOfMeasureID]);
CREATE STATISTICS [stat_cso_DimProduct_UnitOfMeasureName] ON [cso].[DimProduct]([UnitOfMeasureName]);
CREATE STATISTICS [stat_cso_DimProduct_UnitPrice] ON [cso].[DimProduct]([UnitPrice]);
CREATE STATISTICS [stat_cso_DimProduct_UpdateDate] ON [cso].[DimProduct]([UpdateDate]);
CREATE STATISTICS [stat_cso_DimProduct_Weight] ON [cso].[DimProduct]([Weight]);
CREATE STATISTICS [stat_cso_DimProduct_WeightUnitMeasureID] ON [cso].[DimProduct]([WeightUnitMeasureID]);
CREATE STATISTICS [stat_cso_FactOnlineSales_CurrencyKey] ON [cso].[FactOnlineSales]([CurrencyKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_CustomerKey] ON [cso].[FactOnlineSales]([CustomerKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_DateKey] ON [cso].[FactOnlineSales]([DateKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_OnlineSalesKey] ON [cso].[FactOnlineSales]([OnlineSalesKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_ProductKey] ON [cso].[FactOnlineSales]([ProductKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_PromotionKey] ON [cso].[FactOnlineSales]([PromotionKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_StoreKey] ON [cso].[FactOnlineSales]([StoreKey]);
```

## <a name="achievement-unlocked"></a><span data-ttu-id="8739c-181">Et voilà !</span><span class="sxs-lookup"><span data-stu-id="8739c-181">Achievement unlocked!</span></span>
<span data-ttu-id="8739c-182">Vous avez correctement chargé les données publiques dans Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="8739c-182">You have successfully loaded public data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="8739c-183">Bon travail !</span><span class="sxs-lookup"><span data-stu-id="8739c-183">Great job!</span></span>

<span data-ttu-id="8739c-184">Vous pouvez maintenant démarrer l’interrogation de tables hello à l’aide de requêtes hello suivante :</span><span class="sxs-lookup"><span data-stu-id="8739c-184">You can now start querying hello tables using queries like hello following:</span></span>

```sql
SELECT  SUM(f.[SalesAmount]) AS [sales_by_brand_amount]
,       p.[BrandName]
FROM    [cso].[FactOnlineSales] AS f
JOIN    [cso].[DimProduct]      AS p ON f.[ProductKey] = p.[ProductKey]
GROUP BY p.[BrandName]
```

## <a name="next-steps"></a><span data-ttu-id="8739c-185">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8739c-185">Next steps</span></span>
<span data-ttu-id="8739c-186">tooload hello complète Contoso l’entrepôt de données de vente au détail des données, utiliser un script de hello dans pour obtenir des conseils de développement plus, consultez [vue d’ensemble du développement de SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="8739c-186">tooload hello full Contoso Retail Data Warehouse data, use hello script in For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

<!--Article references-->
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Load data into SQL Data Warehouse]: sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: sql-data-warehouse-overview-develop.md
[manage columnstore indexes]: sql-data-warehouse-tables-index.md
[Statistics]: sql-data-warehouse-tables-statistics.md
[CTAS]: sql-data-warehouse-develop-ctas.md
[label]: sql-data-warehouse-develop-label.md

<!--MSDN references-->
[CREATE EXTERNAL DATA SOURCE]: https://msdn.microsoft.com/en-us/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT]: https://msdn.microsoft.com/en-us/library/dn935026.aspx
[CREATE TABLE AS SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/mt204041.aspx
[sys.dm_pdw_exec_requests]: https://msdn.microsoft.com/library/mt203887.aspx
[REBUILD]: https://msdn.microsoft.com/library/ms188388.aspx

<!--Other Web references-->
[Microsoft Download Center]: http://www.microsoft.com/download/details.aspx?id=36433
[Load hello full Contoso Retail Data Warehouse]: https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/contoso-data-warehouse/readme.md
