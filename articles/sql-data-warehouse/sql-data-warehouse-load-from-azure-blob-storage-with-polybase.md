---
title: "Charger à partir d’Azure Blob vers l’entrepôt de données Azure| Microsoft Docs"
description: "Apprenez à utiliser PolyBase pour charger des données de stockage d’objets blob Azure dans SQL Data Warehouse. Chargez quelques tables à partir de données publiques dans le schéma d’entrepôt de données Contoso Retail."
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
ms.openlocfilehash: 2859c1144f72fd685af89f83024df1409902ab0c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-from-azure-blob-storage-into-sql-data-warehouse-polybase"></a><span data-ttu-id="946c0-104">Charger les données de stockage d’objets blob Azure dans SQL Data Warehouse (PolyBase)</span><span class="sxs-lookup"><span data-stu-id="946c0-104">Load data from Azure blob storage into SQL Data Warehouse (PolyBase)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="946c0-105">Data Factory</span><span class="sxs-lookup"><span data-stu-id="946c0-105">Data Factory</span></span>](sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md)
> * [<span data-ttu-id="946c0-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="946c0-106">PolyBase</span></span>](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md)
> 
> 

<span data-ttu-id="946c0-107">Utilisez PolyBase et les commandes T-SQL pour charger les données de stockage d’objets blob Azure dans Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="946c0-107">Use PolyBase and T-SQL commands to load data from Azure blob storage into Azure SQL Data Warehouse.</span></span> 

<span data-ttu-id="946c0-108">En quelques mots, ce didacticiel charge deux tables de stockage d’objets blob Azure public dans le schéma d’entrepôt de données Contoso Retail.</span><span class="sxs-lookup"><span data-stu-id="946c0-108">To keep it simple, this tutorial loads two tables from a public Azure Storage Blob into the Contoso Retail Data Warehouse schema.</span></span> <span data-ttu-id="946c0-109">Pour charger le jeu de données, exécutez l’exemple [Load the full Contoso Retail Data Warehouse][Load the full Contoso Retail Data Warehouse] (Charger l’ensemble de l’entrepôt de données Contoso Retail) à partir du référentiel d’exemples Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="946c0-109">To load the full data set, run the example [Load the full Contoso Retail Data Warehouse][Load the full Contoso Retail Data Warehouse] from the Microsoft SQL Server Samples repository.</span></span>

<span data-ttu-id="946c0-110">Ce didacticiel vous apprendra à effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="946c0-110">In this tutorial you will:</span></span>

1. <span data-ttu-id="946c0-111">Configurer PolyBase pour effectuer un chargement à partir du stockage d’objets blob Azure</span><span class="sxs-lookup"><span data-stu-id="946c0-111">Configure PolyBase to load from Azure blob storage</span></span>
2. <span data-ttu-id="946c0-112">Charger des données publiques dans votre base de données</span><span class="sxs-lookup"><span data-stu-id="946c0-112">Load public data into your database</span></span>
3. <span data-ttu-id="946c0-113">Procéder à des optimisations une fois le chargement terminé</span><span class="sxs-lookup"><span data-stu-id="946c0-113">Perform optimizations after the load is finished.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="946c0-114">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="946c0-114">Before you begin</span></span>
<span data-ttu-id="946c0-115">Pour exécuter ce didacticiel, vous avez besoin d’un compte Azure qui possède déjà une base de données SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="946c0-115">To run this tutorial, you need an Azure account that already has a SQL Data Warehouse database.</span></span> <span data-ttu-id="946c0-116">Si vous n’en disposez pas, consultez la page [Créer un entrepôt de données SQL][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="946c0-116">If you don't already have this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>

## <a name="1-configure-the-data-source"></a><span data-ttu-id="946c0-117">1. Configurer la source de données</span><span class="sxs-lookup"><span data-stu-id="946c0-117">1. Configure the data source</span></span>
<span data-ttu-id="946c0-118">PolyBase utilise des objets externes T-SQL pour définir l’emplacement et les attributs des données externes.</span><span class="sxs-lookup"><span data-stu-id="946c0-118">PolyBase uses T-SQL external objects to define the location and attributes of the external data.</span></span> <span data-ttu-id="946c0-119">Les définitions d’objet externe sont stockées dans SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="946c0-119">The external object definitions are stored in SQL Data Warehouse.</span></span> <span data-ttu-id="946c0-120">Les données elles-mêmes sont stockées en externe.</span><span class="sxs-lookup"><span data-stu-id="946c0-120">The data itself is stored externally.</span></span>

### <a name="11-create-a-credential"></a><span data-ttu-id="946c0-121">1.1.</span><span class="sxs-lookup"><span data-stu-id="946c0-121">1.1.</span></span> <span data-ttu-id="946c0-122">Créer des informations d’identification</span><span class="sxs-lookup"><span data-stu-id="946c0-122">Create a credential</span></span>
<span data-ttu-id="946c0-123">**Ignorez cette étape** si vous chargez les données publiques de Contoso.</span><span class="sxs-lookup"><span data-stu-id="946c0-123">**Skip this step** if you are loading the Contoso public data.</span></span> <span data-ttu-id="946c0-124">Vous n’avez pas besoin d’un accès sécurisé aux données publiques, car ces dernières sont accessibles à tous.</span><span class="sxs-lookup"><span data-stu-id="946c0-124">You don't need secure access to the public data since it is already accessible to anyone.</span></span>

<span data-ttu-id="946c0-125">**N’ignorez pas cette étape** si vous utilisez ce didacticiel comme modèle pour le chargement de vos propres données.</span><span class="sxs-lookup"><span data-stu-id="946c0-125">**Don't skip this step** if you are using this tutorial as a template for loading your own data.</span></span> <span data-ttu-id="946c0-126">Pour accéder aux données par le biais d’informations d’identification, utilisez le script suivant afin de créer des informations d’identification de niveau base de données, puis définissez l’emplacement de la source de données.</span><span class="sxs-lookup"><span data-stu-id="946c0-126">To access data through a credential, use the following script to create a database-scoped credential, and then use it when defining the location of the data source.</span></span>

```sql
-- A: Create a master key.
-- Only necessary if one does not already exist.
-- Required to encrypt the credential secret in the next step.

CREATE MASTER KEY;


-- B: Create a database scoped credential
-- IDENTITY: Provide any string, it is not used for authentication to Azure storage.
-- SECRET: Provide your Azure storage account key.


CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential
WITH
    IDENTITY = 'user',
    SECRET = '<azure_storage_account_key>'
;


-- C: Create an external data source
-- TYPE: HADOOP - PolyBase uses Hadoop APIs to access data in Azure blob storage.
-- LOCATION: Provide Azure storage account name and blob container name.
-- CREDENTIAL: Provide the credential created in the previous step.

CREATE EXTERNAL DATA SOURCE AzureStorage
WITH (
    TYPE = HADOOP,
    LOCATION = 'wasbs://<blob_container_name>@<azure_storage_account_name>.blob.core.windows.net',
    CREDENTIAL = AzureStorageCredential
);
```

<span data-ttu-id="946c0-127">Passez à l’étape 2.</span><span class="sxs-lookup"><span data-stu-id="946c0-127">Skip to step 2.</span></span>

### <a name="12-create-the-external-data-source"></a><span data-ttu-id="946c0-128">1.2.</span><span class="sxs-lookup"><span data-stu-id="946c0-128">1.2.</span></span> <span data-ttu-id="946c0-129">Créer la source de données externe</span><span class="sxs-lookup"><span data-stu-id="946c0-129">Create the external data source</span></span>
<span data-ttu-id="946c0-130">Utilisez la commande [CREATE EXTERNAL DATA SOURCE][CREATE EXTERNAL DATA SOURCE] pour stocker l’emplacement des données et le type de données.</span><span class="sxs-lookup"><span data-stu-id="946c0-130">Use this [CREATE EXTERNAL DATA SOURCE][CREATE EXTERNAL DATA SOURCE] command to store the location of the data, and the type of data.</span></span> 

```sql
CREATE EXTERNAL DATA SOURCE AzureStorage_west_public
WITH 
(  
    TYPE = Hadoop 
,   LOCATION = 'wasbs://contosoretaildw-tables@contosoretaildw.blob.core.windows.net/'
); 
```

> [!IMPORTANT]
> <span data-ttu-id="946c0-131">Si vous choisissez de rendre publics vos conteneurs de stockage d’objets blob Azure, n’oubliez pas qu’en tant que propriétaire des données vous devez vous acquitter des frais d’acheminement lorsque des données quittent le centre de données.</span><span class="sxs-lookup"><span data-stu-id="946c0-131">If you choose to make your azure blob storage containers public, remember that as the data owner you will be charged for data egress charges when data leaves the data center.</span></span> 
> 
> 

## <a name="2-configure-data-format"></a><span data-ttu-id="946c0-132">2. Configurer le format des données</span><span class="sxs-lookup"><span data-stu-id="946c0-132">2. Configure data format</span></span>
<span data-ttu-id="946c0-133">Les données sont stockées dans des fichiers texte dans le stockage d’objets blob Azure, et chaque champ est séparé par un délimiteur.</span><span class="sxs-lookup"><span data-stu-id="946c0-133">The data is stored in text files in Azure blob storage, and each field is separated with a delimiter.</span></span> <span data-ttu-id="946c0-134">Exécutez cette commande [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT] pour spécifier le format des données dans les fichiers texte.</span><span class="sxs-lookup"><span data-stu-id="946c0-134">Run this [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT] command to specify the format of the data in the text files.</span></span> <span data-ttu-id="946c0-135">Les données Contoso ne sont pas compressées et elles sont séparées par des barres verticales.</span><span class="sxs-lookup"><span data-stu-id="946c0-135">The Contoso data is uncompressed and pipe delimited.</span></span>

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

## <a name="3-create-the-external-tables"></a><span data-ttu-id="946c0-136">3. Créer les tables externes</span><span class="sxs-lookup"><span data-stu-id="946c0-136">3. Create the external tables</span></span>
<span data-ttu-id="946c0-137">Maintenant que vous avez spécifié la source des données et le format de fichier, vous êtes prêt à créer les tables externes.</span><span class="sxs-lookup"><span data-stu-id="946c0-137">Now that you have specified the data source and file format, you are ready to create the external tables.</span></span> 

### <a name="31-create-a-schema-for-the-data"></a><span data-ttu-id="946c0-138">3.1.</span><span class="sxs-lookup"><span data-stu-id="946c0-138">3.1.</span></span> <span data-ttu-id="946c0-139">Créez un schéma pour les données.</span><span class="sxs-lookup"><span data-stu-id="946c0-139">Create a schema for the data.</span></span>
<span data-ttu-id="946c0-140">Pour créer un emplacement de stockage des données Contoso dans votre base de données, créez un schéma.</span><span class="sxs-lookup"><span data-stu-id="946c0-140">To create a place to store the Contoso data in your database, create a schema.</span></span>

```sql
CREATE SCHEMA [asb]
GO
```

### <a name="32-create-the-external-tables"></a><span data-ttu-id="946c0-141">3.2.</span><span class="sxs-lookup"><span data-stu-id="946c0-141">3.2.</span></span> <span data-ttu-id="946c0-142">Créez les tables externes.</span><span class="sxs-lookup"><span data-stu-id="946c0-142">Create the external tables.</span></span>
<span data-ttu-id="946c0-143">Exécutez ce script pour créer les tables externes DimProduct et FactOnlineSales.</span><span class="sxs-lookup"><span data-stu-id="946c0-143">Run this script to create the DimProduct and FactOnlineSales external tables.</span></span> <span data-ttu-id="946c0-144">Nous essayons ici de définir les noms de colonnes et les types de données, et de les lier à l’emplacement et au format des fichiers de stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="946c0-144">All we are doing here is defining column names and data types, and binding them to the location and format of the Azure blob storage files.</span></span> <span data-ttu-id="946c0-145">La définition est stockée dans SQL Data Warehouse et les données se trouvent toujours dans le stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="946c0-145">The definition is stored in SQL Data Warehouse and the data is still in the Azure Storage Blob.</span></span>

<span data-ttu-id="946c0-146">Le paramètre **LOCATION** désigne le dossier qui se situe sous le dossier racine du stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="946c0-146">The  **LOCATION** parameter is the folder under the root folder in the Azure Storage Blob.</span></span> <span data-ttu-id="946c0-147">Chaque table se trouve dans un dossier spécifique.</span><span class="sxs-lookup"><span data-stu-id="946c0-147">Each table is in a different folder.</span></span>

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

## <a name="4-load-the-data"></a><span data-ttu-id="946c0-148">4. Chargement des données</span><span class="sxs-lookup"><span data-stu-id="946c0-148">4. Load the data</span></span>
<span data-ttu-id="946c0-149">Il existe plusieurs façons d’accéder aux données externes.</span><span class="sxs-lookup"><span data-stu-id="946c0-149">There's different ways to access external data.</span></span>  <span data-ttu-id="946c0-150">Vous pouvez interroger les données directement à partir de la table externe, charger les données dans de nouvelles tables de base de données, ou ajouter des données externes à des tables de base de données existantes.</span><span class="sxs-lookup"><span data-stu-id="946c0-150">You can query data directly from the external table, load the data into new database tables, or add external data to existing database tables.</span></span>  

### <a name="41-create-a-new-schema"></a><span data-ttu-id="946c0-151">4.1.</span><span class="sxs-lookup"><span data-stu-id="946c0-151">4.1.</span></span> <span data-ttu-id="946c0-152">Créer un schéma</span><span class="sxs-lookup"><span data-stu-id="946c0-152">Create a new schema</span></span>
<span data-ttu-id="946c0-153">CTAS crée une table qui contient des données.</span><span class="sxs-lookup"><span data-stu-id="946c0-153">CTAS creates a new table that contains data.</span></span>  <span data-ttu-id="946c0-154">Commencez par créer un schéma pour les données Contoso.</span><span class="sxs-lookup"><span data-stu-id="946c0-154">First, create a schema for the contoso data.</span></span>

```sql
CREATE SCHEMA [cso]
GO
```

### <a name="42-load-the-data-into-new-tables"></a><span data-ttu-id="946c0-155">4.2.</span><span class="sxs-lookup"><span data-stu-id="946c0-155">4.2.</span></span> <span data-ttu-id="946c0-156">Charger les données dans de nouvelles tables</span><span class="sxs-lookup"><span data-stu-id="946c0-156">Load the data into new tables</span></span>
<span data-ttu-id="946c0-157">Pour charger des données à partir d’Azure Blob Storage et pour les enregistrer dans une table au sein de votre base de données, utilisez l’instruction [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)].</span><span class="sxs-lookup"><span data-stu-id="946c0-157">To load data from Azure blob storage and save it in a table inside of your database, use the [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] statement.</span></span> <span data-ttu-id="946c0-158">Le chargement avec CTAS s’appuie sur les tables externes fortement typées que vous venez de créer. Pour charger les données dans de nouvelles tables, utilisez une instruction [CTAS][CTAS] par table.</span><span class="sxs-lookup"><span data-stu-id="946c0-158">Loading with CTAS leverages the strongly typed external tables you have just created.To load the data into new tables, use one [CTAS][CTAS] statement per table.</span></span> 
 
<span data-ttu-id="946c0-159">CTAS crée une table et la remplit avec les résultats d’une instruction select.</span><span class="sxs-lookup"><span data-stu-id="946c0-159">CTAS creates a new table and populates it with the results of a select statement.</span></span> <span data-ttu-id="946c0-160">CTAS définit la nouvelle table de manière à proposer les mêmes colonnes et les mêmes types de données que les résultats de l’instruction select.</span><span class="sxs-lookup"><span data-stu-id="946c0-160">CTAS defines the new table to have the same columns and data types as the results of the select statement.</span></span> <span data-ttu-id="946c0-161">Si vous sélectionnez toutes les colonnes d’une table externe, la nouvelle table est un réplica des colonnes et des types de données dans la table externe.</span><span class="sxs-lookup"><span data-stu-id="946c0-161">If you select all the columns from an external table, the new table will be a replica of the columns and data types in the external table.</span></span>

<span data-ttu-id="946c0-162">Dans cet exemple, nous créons la table de dimension et la table de faits qui joueront le rôle de tables distribuées par hachage.</span><span class="sxs-lookup"><span data-stu-id="946c0-162">In this example, we create both the dimension and the fact table as hash distributed tables.</span></span> 

```sql
SELECT GETDATE();
GO

CREATE TABLE [cso].[DimProduct]            WITH (DISTRIBUTION = HASH([ProductKey]  ) ) AS SELECT * FROM [asb].[DimProduct]             OPTION (LABEL = 'CTAS : Load [cso].[DimProduct]             ');
CREATE TABLE [cso].[FactOnlineSales]       WITH (DISTRIBUTION = HASH([ProductKey]  ) ) AS SELECT * FROM [asb].[FactOnlineSales]        OPTION (LABEL = 'CTAS : Load [cso].[FactOnlineSales]        ');
```

### <a name="43-track-the-load-progress"></a><span data-ttu-id="946c0-163">4.3 Suivre la progression du chargement</span><span class="sxs-lookup"><span data-stu-id="946c0-163">4.3 Track the load progress</span></span>
<span data-ttu-id="946c0-164">Vous pouvez suivre la progression de votre chargement à l’aide des vues de gestion dynamique (DMV).</span><span class="sxs-lookup"><span data-stu-id="946c0-164">You can track the progress of your load using dynamic management views (DMVs).</span></span> 

```sql
-- To see all requests
SELECT * FROM sys.dm_pdw_exec_requests;

-- To see a particular request identified by its label
SELECT * FROM sys.dm_pdw_exec_requests as r
WHERE r.[label] = 'CTAS : Load [cso].[DimProduct]             '
      OR r.[label] = 'CTAS : Load [cso].[FactOnlineSales]        '
;

-- To track bytes and files
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

## <a name="5-optimize-columnstore-compression"></a><span data-ttu-id="946c0-165">5. Optimiser la compression columnstore</span><span class="sxs-lookup"><span data-stu-id="946c0-165">5. Optimize columnstore compression</span></span>
<span data-ttu-id="946c0-166">Par défaut, SQL Data Warehouse stocke la table comme un index columnstore en cluster.</span><span class="sxs-lookup"><span data-stu-id="946c0-166">By default, SQL Data Warehouse stores the table as a clustered columnstore index.</span></span> <span data-ttu-id="946c0-167">Après un chargement, certaines lignes de données peuvent ne pas être compressées dans le columnstore.</span><span class="sxs-lookup"><span data-stu-id="946c0-167">After a load completes, some of the data rows might not be compressed into the columnstore.</span></span>  <span data-ttu-id="946c0-168">Cela peut être dû à diverses raisons.</span><span class="sxs-lookup"><span data-stu-id="946c0-168">There's a variety of reasons why this can happen.</span></span> <span data-ttu-id="946c0-169">Pour plus d’informations, consultez [Gérer les index Columnstore][manage columnstore indexes].</span><span class="sxs-lookup"><span data-stu-id="946c0-169">To learn more, see [manage columnstore indexes][manage columnstore indexes].</span></span>

<span data-ttu-id="946c0-170">Pour optimiser les performances des requêtes et la compression du columnstore après un chargement, reconstruisez la table afin de forcer l’index columnstore à compresser toutes les lignes.</span><span class="sxs-lookup"><span data-stu-id="946c0-170">To optimize query performance and columnstore compression after a load, rebuild the table to force the columnstore index to compress all the rows.</span></span> 

```sql
SELECT GETDATE();
GO

ALTER INDEX ALL ON [cso].[DimProduct]               REBUILD;
ALTER INDEX ALL ON [cso].[FactOnlineSales]          REBUILD;
```

<span data-ttu-id="946c0-171">Pour plus d’informations sur la maintenance des index Columnstore, consultez l’article [Gérer les index Columnstore][manage columnstore indexes].</span><span class="sxs-lookup"><span data-stu-id="946c0-171">For more information on maintaining columnstore indexes, see the [manage columnstore indexes][manage columnstore indexes] article.</span></span>

## <a name="6-optimize-statistics"></a><span data-ttu-id="946c0-172">6. Optimiser les statistiques</span><span class="sxs-lookup"><span data-stu-id="946c0-172">6. Optimize statistics</span></span>
<span data-ttu-id="946c0-173">Il est préférable de créer des statistiques sur une colonne immédiatement après un chargement.</span><span class="sxs-lookup"><span data-stu-id="946c0-173">It is best to create single-column statistics immediately after a load.</span></span> <span data-ttu-id="946c0-174">Les statistiques offrent plusieurs possibilités.</span><span class="sxs-lookup"><span data-stu-id="946c0-174">There are some choices for statistics.</span></span> <span data-ttu-id="946c0-175">Par exemple, si vous créez des statistiques sur une colonne pour chaque colonne, il faudra peut-être beaucoup de temps pour reconstruire toutes les statistiques.</span><span class="sxs-lookup"><span data-stu-id="946c0-175">For example, if you create single-column statistics on every column it might take a long time to rebuild all the statistics.</span></span> <span data-ttu-id="946c0-176">S’il est certain que des colonnes ne se trouveront pas dans les prédicats de requête, vous pouvez ignorer la création des statistiques sur ces colonnes.</span><span class="sxs-lookup"><span data-stu-id="946c0-176">If you know certain columns are not going to be in query predicates, you can skip creating statistics on those columns.</span></span>

<span data-ttu-id="946c0-177">Si vous décidez de créer des statistiques sur une colonne pour chaque colonne de chaque table, vous pouvez utiliser l’exemple de code de procédure stockée `prc_sqldw_create_stats` dans l’article portant sur les [statistiques][statistics].</span><span class="sxs-lookup"><span data-stu-id="946c0-177">If you decide to create single-column statistics on every column of every table, you can use the stored procedure code sample `prc_sqldw_create_stats` in the [statistics][statistics] article.</span></span>

<span data-ttu-id="946c0-178">L’exemple suivant est un bon point de départ pour la création de statistiques.</span><span class="sxs-lookup"><span data-stu-id="946c0-178">The following example is a good starting point for creating statistics.</span></span> <span data-ttu-id="946c0-179">Il permet de créer des statistiques sur une colonne pour chaque colonne de la table de dimension, et chaque colonne de jointure des tables de faits.</span><span class="sxs-lookup"><span data-stu-id="946c0-179">It creates single-column statistics on each column in the dimension table, and on each joining column in the fact tables.</span></span> <span data-ttu-id="946c0-180">Vous pouvez toujours ajouter ultérieurement des statistiques sur une ou plusieurs colonnes dans d’autres colonnes de table de faits.</span><span class="sxs-lookup"><span data-stu-id="946c0-180">You can always add single or multi-column statistics to other fact table columns later on.</span></span>

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

## <a name="achievement-unlocked"></a><span data-ttu-id="946c0-181">Et voilà !</span><span class="sxs-lookup"><span data-stu-id="946c0-181">Achievement unlocked!</span></span>
<span data-ttu-id="946c0-182">Vous avez correctement chargé les données publiques dans Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="946c0-182">You have successfully loaded public data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="946c0-183">Bon travail !</span><span class="sxs-lookup"><span data-stu-id="946c0-183">Great job!</span></span>

<span data-ttu-id="946c0-184">Vous pouvez maintenant interroger les tables à l’aide de requêtes comme celle-ci :</span><span class="sxs-lookup"><span data-stu-id="946c0-184">You can now start querying the tables using queries like the following:</span></span>

```sql
SELECT  SUM(f.[SalesAmount]) AS [sales_by_brand_amount]
,       p.[BrandName]
FROM    [cso].[FactOnlineSales] AS f
JOIN    [cso].[DimProduct]      AS p ON f.[ProductKey] = p.[ProductKey]
GROUP BY p.[BrandName]
```

## <a name="next-steps"></a><span data-ttu-id="946c0-185">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="946c0-185">Next steps</span></span>
<span data-ttu-id="946c0-186">Pour charger l’ensemble des données de l’entrepôt de données Contoso Retail, utilisez le script. Pour d’autres conseils de développement, consultez [Vue d’ensemble sur le développement SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="946c0-186">To load the full Contoso Retail Data Warehouse data, use the script in For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

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
[Load the full Contoso Retail Data Warehouse]: https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/contoso-data-warehouse/readme.md
