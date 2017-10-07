---
title: "aaaPolyBase dans le didacticiel sur l’entrepôt de données SQL | Documents Microsoft"
description: "Découvrez les nouveautés de PolyBase et comment toouse pour les scénarios d’entreposage de données."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 0a0103b4-ddd6-4d1e-87be-4965d6e99f3f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 03/01/2017
ms.author: cakarst;barbkess
ms.openlocfilehash: 3e680ec407c1d920dd59ea922b82c9208b5e9a84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-polybase-in-sql-data-warehouse"></a><span data-ttu-id="33ce2-103">Télécharger des données avec PolyBase dans SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="33ce2-103">Load data with PolyBase in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="33ce2-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="33ce2-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)  
> * [<span data-ttu-id="33ce2-105">Data Factory</span><span class="sxs-lookup"><span data-stu-id="33ce2-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [<span data-ttu-id="33ce2-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="33ce2-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [<span data-ttu-id="33ce2-107">BCP</span><span class="sxs-lookup"><span data-stu-id="33ce2-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)
> 
> 

<span data-ttu-id="33ce2-108">Ce didacticiel montre comment les données de tooload dans l’entrepôt de données SQL à l’aide de AzCopy et PolyBase.</span><span class="sxs-lookup"><span data-stu-id="33ce2-108">This tutorial shows how tooload data into SQL Data Warehouse using AzCopy and PolyBase.</span></span> <span data-ttu-id="33ce2-109">À la fin de ce didacticiel, vous saurez comment :</span><span class="sxs-lookup"><span data-stu-id="33ce2-109">When finished, you will know how to:</span></span>

* <span data-ttu-id="33ce2-110">Utiliser le stockage d’objets blob tooAzure AzCopy toocopy données</span><span class="sxs-lookup"><span data-stu-id="33ce2-110">Use AzCopy toocopy data tooAzure blob storage</span></span>
* <span data-ttu-id="33ce2-111">Créer des objets de base de données les données de salutation toodefine</span><span class="sxs-lookup"><span data-stu-id="33ce2-111">Create database objects toodefine hello data</span></span>
* <span data-ttu-id="33ce2-112">Exécuter une requête T-SQL tooload des données hello</span><span class="sxs-lookup"><span data-stu-id="33ce2-112">Run a T-SQL query tooload hello data</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-with-PolyBase-in-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="33ce2-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="33ce2-113">Prerequisites</span></span>
<span data-ttu-id="33ce2-114">toostep dans ce didacticiel, vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="33ce2-114">toostep through this tutorial, you need</span></span>

* <span data-ttu-id="33ce2-115">Une base de données SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="33ce2-115">A SQL Data Warehouse database.</span></span>
* <span data-ttu-id="33ce2-116">Un compte de stockage Azure de type stockage redondant local standard (LRS-Standard), stockage géo-redondant Standard (Standard-GRS) ou stockage géo-redondant avec accès en lecture Standard (Standard-RAGRS)</span><span class="sxs-lookup"><span data-stu-id="33ce2-116">An Azure storage account of type Standard Locally Redundant Storage (Standard-LRS), Standard Geo-Redundant Storage (Standard-GRS), or Standard Read-Access Geo-Redundant Storage (Standard-RAGRS).</span></span>
* <span data-ttu-id="33ce2-117">L’utilitaire de ligne de commande AzCopy</span><span class="sxs-lookup"><span data-stu-id="33ce2-117">AzCopy Command-Line Utility.</span></span> <span data-ttu-id="33ce2-118">Téléchargez et installez hello [version la plus récente de AzCopy] [ latest version of AzCopy] qui est installé avec hello de stockage Microsoft Azure Tools.</span><span class="sxs-lookup"><span data-stu-id="33ce2-118">Download and install hello [latest version of AzCopy][latest version of AzCopy] which is installed with hello Microsoft Azure Storage Tools.</span></span>
  
    ![Outils Azure Storage](./media/sql-data-warehouse-get-started-load-with-polybase/install-azcopy.png)

## <a name="step-1-add-sample-data-tooazure-blob-storage"></a><span data-ttu-id="33ce2-120">Étape 1 : Ajouter le stockage d’objets blob tooAzure échantillon de données</span><span class="sxs-lookup"><span data-stu-id="33ce2-120">Step 1: Add sample data tooAzure blob storage</span></span>
<span data-ttu-id="33ce2-121">Données de commandes tooload, nous devons tooput quelques exemples de données dans un stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="33ce2-121">In order tooload data, we need tooput some sample data into an Azure blob storage.</span></span> <span data-ttu-id="33ce2-122">Lors de cette étape, nous allons remplir un objet blob Azure Storage avec des exemples de données.</span><span class="sxs-lookup"><span data-stu-id="33ce2-122">In this step we populate an Azure Storage blob with sample data.</span></span> <span data-ttu-id="33ce2-123">Une version ultérieure, nous allons utiliser PolyBase tooload ces exemples de données dans votre base de données SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="33ce2-123">Later, we will use PolyBase tooload this sample data into your SQL Data Warehouse database.</span></span>

### <a name="a-prepare-a-sample-text-file"></a><span data-ttu-id="33ce2-124">R :</span><span class="sxs-lookup"><span data-stu-id="33ce2-124">A.</span></span> <span data-ttu-id="33ce2-125">Préparer un exemple de fichier texte</span><span class="sxs-lookup"><span data-stu-id="33ce2-125">Prepare a sample text file</span></span>
<span data-ttu-id="33ce2-126">tooprepare un exemple de fichier texte :</span><span class="sxs-lookup"><span data-stu-id="33ce2-126">tooprepare a sample text file:</span></span>

1. <span data-ttu-id="33ce2-127">Ouvrez le bloc-notes, puis copiez hello après des lignes de données dans un nouveau fichier.</span><span class="sxs-lookup"><span data-stu-id="33ce2-127">Open Notepad and copy hello following lines of data into a new file.</span></span> <span data-ttu-id="33ce2-128">Enregistrez ce répertoire temporaire local de tooyour sous % temp%\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="33ce2-128">Save this tooyour local temp directory as %temp%\DimDate2.txt.</span></span>

```
20150301,1,3
20150501,2,4
20151001,4,2
20150201,1,3
20151201,4,2
20150801,3,1
20150601,2,4
20151101,4,2
20150401,2,4
20150701,3,1
20150901,3,1
20150101,1,3
```

### <a name="b-find-your-blob-service-endpoint"></a><span data-ttu-id="33ce2-129">B.</span><span class="sxs-lookup"><span data-stu-id="33ce2-129">B.</span></span> <span data-ttu-id="33ce2-130">Recherchez votre point de terminaison de service blob</span><span class="sxs-lookup"><span data-stu-id="33ce2-130">Find your blob service endpoint</span></span>
<span data-ttu-id="33ce2-131">toofind votre point de terminaison de service blob :</span><span class="sxs-lookup"><span data-stu-id="33ce2-131">toofind your blob service endpoint:</span></span>

1. <span data-ttu-id="33ce2-132">Sélectionnez hello Azure Portal **Parcourir** > **comptes de stockage**.</span><span class="sxs-lookup"><span data-stu-id="33ce2-132">From hello Azure Portal select **Browse** > **Storage Accounts**.</span></span>
2. <span data-ttu-id="33ce2-133">Cliquez sur le compte de stockage hello souhaité toouse.</span><span class="sxs-lookup"><span data-stu-id="33ce2-133">Click hello storage account you want toouse.</span></span>
3. <span data-ttu-id="33ce2-134">Dans le panneau de compte de stockage hello, cliquez sur objets BLOB</span><span class="sxs-lookup"><span data-stu-id="33ce2-134">In hello Storage account blade, click Blobs</span></span>
   
    ![Cliquer sur les objets blobs](./media/sql-data-warehouse-get-started-load-with-polybase/click-blobs.png)
4. <span data-ttu-id="33ce2-136">Enregistrez votre URL de point de terminaison du service blob pour l’utiliser à une date ultérieure.</span><span class="sxs-lookup"><span data-stu-id="33ce2-136">Save your blob service endpoint URL for later.</span></span>
   
    ![Point de terminaison de service blob](./media/sql-data-warehouse-get-started-load-with-polybase/blob-service.png)

### <a name="c-find-your-azure-storage-key"></a><span data-ttu-id="33ce2-138">C.</span><span class="sxs-lookup"><span data-stu-id="33ce2-138">C.</span></span> <span data-ttu-id="33ce2-139">Rechercher votre clé de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="33ce2-139">Find your Azure storage key</span></span>
<span data-ttu-id="33ce2-140">toofind votre clé de stockage Azure :</span><span class="sxs-lookup"><span data-stu-id="33ce2-140">toofind your Azure storage key:</span></span>

1. <span data-ttu-id="33ce2-141">À partir de hello portail Azure, sélectionnez **Parcourir** > **comptes de stockage**.</span><span class="sxs-lookup"><span data-stu-id="33ce2-141">From hello Azure Portal, select **Browse** > **Storage Accounts**.</span></span>
2. <span data-ttu-id="33ce2-142">Cliquez sur le compte de stockage hello souhaité toouse.</span><span class="sxs-lookup"><span data-stu-id="33ce2-142">Click on hello storage account you want toouse.</span></span>
3. <span data-ttu-id="33ce2-143">Sélectionnez **Tous les paramètres** > **Clés d’accès**.</span><span class="sxs-lookup"><span data-stu-id="33ce2-143">Select **All settings** > **Access keys**.</span></span>
4. <span data-ttu-id="33ce2-144">Cliquez sur hello copie boîte toocopy une du Presse-papiers toohello accès aux clés.</span><span class="sxs-lookup"><span data-stu-id="33ce2-144">Click hello copy box toocopy one of your access keys toohello clipboard.</span></span>
   
    ![Copier la clé de stockage Azure](./media/sql-data-warehouse-get-started-load-with-polybase/access-key.png)

### <a name="d-copy-hello-sample-file-tooazure-blob-storage"></a><span data-ttu-id="33ce2-146">D.</span><span class="sxs-lookup"><span data-stu-id="33ce2-146">D.</span></span> <span data-ttu-id="33ce2-147">Copiez le stockage d’objets blob hello exemple fichier tooAzure</span><span class="sxs-lookup"><span data-stu-id="33ce2-147">Copy hello sample file tooAzure blob storage</span></span>
<span data-ttu-id="33ce2-148">toocopy votre stockage d’objets blob de données tooAzure :</span><span class="sxs-lookup"><span data-stu-id="33ce2-148">toocopy your data tooAzure blob storage:</span></span>

1. <span data-ttu-id="33ce2-149">Ouvrez une invite de commandes et modifiez le répertoire d’installation des répertoires toohello AzCopy.</span><span class="sxs-lookup"><span data-stu-id="33ce2-149">Open a command prompt, and change directories toohello AzCopy installation directory.</span></span> <span data-ttu-id="33ce2-150">Cette commande modifie le répertoire d’installation par défaut toohello sur un client de Windows 64 bits.</span><span class="sxs-lookup"><span data-stu-id="33ce2-150">This command changes toohello default installation directory on a 64-bit Windows client.</span></span>
   
    ```
    cd /d "%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy"
    ```
2. <span data-ttu-id="33ce2-151">Exécutez hello suivant du fichier de commandes tooupload hello.</span><span class="sxs-lookup"><span data-stu-id="33ce2-151">Run hello following command tooupload hello file.</span></span> <span data-ttu-id="33ce2-152">Spécifiez l’URL du point de terminaison de votre service d’objets blobs pour <blob service endpoint URL> et votre clé de compte de stockage Azure pour <azure_storage_account_key>.</span><span class="sxs-lookup"><span data-stu-id="33ce2-152">Specify your blob service endpoint URL for <blob service endpoint URL> and your Azure storage account key for <azure_storage_account_key>.</span></span>
   
    ```
    .\AzCopy.exe /Source:C:\Temp\ /Dest:<blob service endpoint URL> /datacontainer/datedimension/ /DestKey:<azure_storage_account_key> /Pattern:DimDate2.txt
    ```

<span data-ttu-id="33ce2-153">Voir aussi [prise en main de l’utilitaire de ligne de commande AzCopy de hello][Getting Started with hello AzCopy Command-Line Utility].</span><span class="sxs-lookup"><span data-stu-id="33ce2-153">See also [Getting Started with hello AzCopy Command-Line Utility][Getting Started with hello AzCopy Command-Line Utility].</span></span>

### <a name="e-explore-your-blob-storage-container"></a><span data-ttu-id="33ce2-154">E.</span><span class="sxs-lookup"><span data-stu-id="33ce2-154">E.</span></span> <span data-ttu-id="33ce2-155">Explorer votre conteneur de stockage d’objets blobs</span><span class="sxs-lookup"><span data-stu-id="33ce2-155">Explore your blob storage container</span></span>
<span data-ttu-id="33ce2-156">fichier de hello toosee vous avez téléchargé tooblob stockage :</span><span class="sxs-lookup"><span data-stu-id="33ce2-156">toosee hello file you uploaded tooblob storage:</span></span>

1. <span data-ttu-id="33ce2-157">Retournez dans le panneau de service Blob tooyour.</span><span class="sxs-lookup"><span data-stu-id="33ce2-157">Go back tooyour Blob service blade.</span></span>
2. <span data-ttu-id="33ce2-158">Sous Conteneurs, double-cliquez sur **datacontainer**.</span><span class="sxs-lookup"><span data-stu-id="33ce2-158">Under Containers, double-click **datacontainer**.</span></span>
3. <span data-ttu-id="33ce2-159">tooexplore hello chemin d’accès tooyour données, cliquez sur le dossier de hello **datedimension** et vous verrez votre fichier téléchargé **DimDate2.txt**.</span><span class="sxs-lookup"><span data-stu-id="33ce2-159">tooexplore hello path tooyour data, click hello folder **datedimension** and you will see your uploaded file **DimDate2.txt**.</span></span>
4. <span data-ttu-id="33ce2-160">tooview propriétés, cliquez sur **DimDate2.txt**.</span><span class="sxs-lookup"><span data-stu-id="33ce2-160">tooview properties, click **DimDate2.txt**.</span></span>
5. <span data-ttu-id="33ce2-161">Notez que dans le panneau des propriétés hello Blob, vous pouvez télécharger ou supprimer le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="33ce2-161">Note that in hello Blob properties blade, you can download or delete hello file.</span></span>
   
    ![Afficher le stockage blob Azure](./media/sql-data-warehouse-get-started-load-with-polybase/view-blob.png)

## <a name="step-2-create-an-external-table-for-hello-sample-data"></a><span data-ttu-id="33ce2-163">Étape 2 : Créer une table externe de données d’exemple hello</span><span class="sxs-lookup"><span data-stu-id="33ce2-163">Step 2: Create an external table for hello sample data</span></span>
<span data-ttu-id="33ce2-164">Dans cette section, nous créons une table externe qui définit les données d’exemple hello.</span><span class="sxs-lookup"><span data-stu-id="33ce2-164">In this section we create an external table that defines hello sample data.</span></span>

<span data-ttu-id="33ce2-165">PolyBase utilise les données tooaccess de tables externes dans le stockage blob Azure.</span><span class="sxs-lookup"><span data-stu-id="33ce2-165">PolyBase uses external tables tooaccess data in Azure blob storage.</span></span> <span data-ttu-id="33ce2-166">Car les données de salutation ne sont pas stockées dans l’entrepôt de données SQL, PolyBase gère les données externes de l’authentification toohello à l’aide d’une information d’identification de l’étendue de base de données.</span><span class="sxs-lookup"><span data-stu-id="33ce2-166">Since hello data is not stored within SQL Data Warehouse, PolyBase handles authentication toohello external data by using a database-scoped credential.</span></span>

<span data-ttu-id="33ce2-167">exemple Hello dans cette étape utilise ces toocreate d’instructions Transact-SQL une table externe.</span><span class="sxs-lookup"><span data-stu-id="33ce2-167">hello example in this step uses these Transact-SQL statements toocreate an external table.</span></span>

* <span data-ttu-id="33ce2-168">[Create Master Key (Transact-SQL)] [ Create Master Key (Transact-SQL)] secret de hello tooencrypt de votre base de données d’une étendue d’informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="33ce2-168">[Create Master Key (Transact-SQL)][Create Master Key (Transact-SQL)] tooencrypt hello secret of your database scoped credential.</span></span>
* <span data-ttu-id="33ce2-169">[Création d’informations d’identification d’une étendue de base de données (Transact-SQL)] [ Create Database Scoped Credential (Transact-SQL)] toospecify les informations d’authentification pour votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="33ce2-169">[Create Database Scoped Credential (Transact-SQL)][Create Database Scoped Credential (Transact-SQL)] toospecify authentication information for your Azure storage account.</span></span>
* <span data-ttu-id="33ce2-170">[Créer la Source de données externe (Transact-SQL)] [ Create External Data Source (Transact-SQL)] emplacement de hello toospecify de votre stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="33ce2-170">[Create External Data Source (Transact-SQL)][Create External Data Source (Transact-SQL)] toospecify hello location of your Azure blob storage.</span></span>
* <span data-ttu-id="33ce2-171">[Créer un Format de fichier externe (Transact-SQL)] [ Create External File Format (Transact-SQL)] format de hello toospecify de vos données.</span><span class="sxs-lookup"><span data-stu-id="33ce2-171">[Create External File Format (Transact-SQL)][Create External File Format (Transact-SQL)] toospecify hello format of your data.</span></span>
* <span data-ttu-id="33ce2-172">[Créer une Table externe (Transact-SQL)] [ Create External Table (Transact-SQL)] toospecify la définition de table hello et l’emplacement de hello des données.</span><span class="sxs-lookup"><span data-stu-id="33ce2-172">[Create External Table (Transact-SQL)][Create External Table (Transact-SQL)] toospecify hello table definition and location of hello data.</span></span>

<span data-ttu-id="33ce2-173">Exécutez cette requête sur votre base de données SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="33ce2-173">Run this query against your SQL Data Warehouse database.</span></span> <span data-ttu-id="33ce2-174">Il crée une table externe nommée DimDate2External dans le schéma dbo hello qui pointe toohello DimDate2.txt exemples de données dans le stockage d’objets blob Azure hello.</span><span class="sxs-lookup"><span data-stu-id="33ce2-174">It will create an external table named DimDate2External in hello dbo schema that points toohello DimDate2.txt sample data in hello Azure blob storage.</span></span>

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


-- D: Create an external file format
-- FORMAT_TYPE: Type of file format in Azure storage (supported: DELIMITEDTEXT, RCFILE, ORC, PARQUET).
-- FORMAT_OPTIONS: Specify field terminator, string delimiter, date format etc. for delimited text files.
-- Specify DATA_COMPRESSION method if data is compressed.

CREATE EXTERNAL FILE FORMAT TextFile
WITH (
    FORMAT_TYPE = DelimitedText,
    FORMAT_OPTIONS (FIELD_TERMINATOR = ',')
);


-- E: Create hello external table
-- Specify column names and data types. This needs toomatch hello data in hello sample file.
-- LOCATION: Specify path toofile or directory that contains hello data (relative toohello blob container).
-- toopoint tooall files under hello blob container, use LOCATION='.'

CREATE EXTERNAL TABLE dbo.DimDate2External (
    DateId INT NOT NULL,
    CalendarQuarter TINYINT NOT NULL,
    FiscalQuarter TINYINT NOT NULL
)
WITH (
    LOCATION='/datedimension/',
    DATA_SOURCE=AzureStorage,
    FILE_FORMAT=TextFile
);


-- Run a query on hello external table

SELECT count(*) FROM dbo.DimDate2External;

```


<span data-ttu-id="33ce2-175">Dans l’Explorateur d’objets SQL Server dans Visual Studio, vous pouvez voir le format de fichier externe hello, source de données externe et hello DimDate2External table.</span><span class="sxs-lookup"><span data-stu-id="33ce2-175">In SQL Server Object Explorer in Visual Studio, you can see hello external file format, external data source, and hello DimDate2External table.</span></span>

![Afficher les tables externes](./media/sql-data-warehouse-get-started-load-with-polybase/external-table.png)

## <a name="step-3-load-data-into-sql-data-warehouse"></a><span data-ttu-id="33ce2-177">Étape 3 : Charger des données dans SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="33ce2-177">Step 3: Load data into SQL Data Warehouse</span></span>
<span data-ttu-id="33ce2-178">Une fois qu’une table externe hello est créée, vous pouvez charger des données de hello dans une nouvelle table ou insérer dans une table existante.</span><span class="sxs-lookup"><span data-stu-id="33ce2-178">Once hello external table is created, you can either load hello data into a new table or insert it into an existing table.</span></span>

* <span data-ttu-id="33ce2-179">les données de salutation tooload dans une nouvelle table, exécutez hello [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] instruction.</span><span class="sxs-lookup"><span data-stu-id="33ce2-179">tooload hello data into a new table, run hello [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] statement.</span></span> <span data-ttu-id="33ce2-180">nouvelle table de Hello aura colonnes hello nommées dans la requête de hello.</span><span class="sxs-lookup"><span data-stu-id="33ce2-180">hello new table will have hello columns named in hello query.</span></span> <span data-ttu-id="33ce2-181">types de données Hello de colonnes de hello correspondra à des types de données hello dans la définition de la table externe hello.</span><span class="sxs-lookup"><span data-stu-id="33ce2-181">hello data types of hello columns will match hello data types in hello external table definition.</span></span>
* <span data-ttu-id="33ce2-182">les données de salutation tooload dans une table existante, utilisez hello [INSERT... SELECT (Transact-SQL)] [ INSERT...SELECT (Transact-SQL)] instruction.</span><span class="sxs-lookup"><span data-stu-id="33ce2-182">tooload hello data into an existing table, use hello [INSERT...SELECT (Transact-SQL)][INSERT...SELECT (Transact-SQL)] statement.</span></span>

```sql
-- Load hello data from Azure blob storage tooSQL Data Warehouse

CREATE TABLE dbo.DimDate2
WITH
(   
    CLUSTERED COLUMNSTORE INDEX,
    DISTRIBUTION = ROUND_ROBIN
)
AS
SELECT * FROM [dbo].[DimDate2External];
```

## <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="33ce2-183">Étape 4 : Créer des statistiques sur vos données nouvellement chargées</span><span class="sxs-lookup"><span data-stu-id="33ce2-183">Step 4: Create statistics on your newly loaded data</span></span>
<span data-ttu-id="33ce2-184">SQL Data Warehouse ne prend pas en charge les statistiques de création ou de mise à jour automatiques.</span><span class="sxs-lookup"><span data-stu-id="33ce2-184">SQL Data Warehouse does not auto-create or auto-update statistics.</span></span> <span data-ttu-id="33ce2-185">Par conséquent, les performances de requête tooachieve, il est important de statistiques toocreate sur chaque colonne de chaque table après hello d’abord chargement.</span><span class="sxs-lookup"><span data-stu-id="33ce2-185">Therefore, tooachieve high query performance, it's important toocreate statistics on each column of each table after hello first load.</span></span> <span data-ttu-id="33ce2-186">Il est également important tooupdate statistiques après des modifications importantes dans les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="33ce2-186">It's also important tooupdate statistics after substantial changes in hello data.</span></span>

<span data-ttu-id="33ce2-187">Cet exemple crée des statistiques de colonne unique sur la nouvelle table de DimDate2 hello.</span><span class="sxs-lookup"><span data-stu-id="33ce2-187">This example creates single-column statistics on hello new DimDate2 table.</span></span>

```sql
CREATE STATISTICS [DateId] on [DimDate2] ([DateId]);
CREATE STATISTICS [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
CREATE STATISTICS [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
```

<span data-ttu-id="33ce2-188">toolearn, voir [statistiques][Statistics].</span><span class="sxs-lookup"><span data-stu-id="33ce2-188">toolearn more, see [Statistics][Statistics].</span></span>  

## <a name="next-steps"></a><span data-ttu-id="33ce2-189">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="33ce2-189">Next steps</span></span>
<span data-ttu-id="33ce2-190">Consultez hello [guide de PolyBase] [ PolyBase guide] pour plus d’informations à connaître lorsque vous développez une solution qui utilise PolyBase.</span><span class="sxs-lookup"><span data-stu-id="33ce2-190">See hello [PolyBase guide][PolyBase guide] for further information you should know as you develop a solution that uses PolyBase.</span></span>

<!--Image references-->


<!--Article references-->
[PolyBase in SQL Data Warehouse Tutorial]: ./sql-data-warehouse-get-started-load-with-polybase.md
[Load data with bcp]: ./sql-data-warehouse-load-with-bcp.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[PolyBase guide]: ./sql-data-warehouse-load-polybase-guide.md
[Getting Started with hello AzCopy Command-Line Utility]:../storage/common/storage-use-azcopy.md
[latest version of AzCopy]:../storage/common/storage-use-azcopy.md

<!--External references-->
[supported source/sink]: https://msdn.microsoft.com/library/dn894007.aspx
[copy activity]: https://msdn.microsoft.com/library/dn835035.aspx
[SQL Server destination adapter]: https://msdn.microsoft.com/library/ms141095.aspx
[SSIS]: https://msdn.microsoft.com/library/ms141026.aspx


[CREATE EXTERNAL DATA SOURCE (Transact-SQL)]:https://msdn.microsoft.com/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT (Transact-SQL)]:https://msdn.microsoft.com/library/dn935026.aspx
[CREATE EXTERNAL TABLE (Transact-SQL)]:https://msdn.microsoft.com/library/dn935021.aspx

[DROP EXTERNAL DATA SOURCE (Transact-SQL)]:https://msdn.microsoft.com/library/mt146367.aspx
[DROP EXTERNAL FILE FORMAT (Transact-SQL)]:https://msdn.microsoft.com/library/mt146379.aspx
[DROP EXTERNAL TABLE (Transact-SQL)]:https://msdn.microsoft.com/library/mt130698.aspx

[CREATE TABLE AS SELECT (Transact-SQL)]:https://msdn.microsoft.com/library/mt204041.aspx
[INSERT...SELECT (Transact-SQL)]:https://msdn.microsoft.com/library/ms174335.aspx
[CREATE MASTER KEY (Transact-SQL)]:https://msdn.microsoft.com/library/ms174382.aspx
[CREATE CREDENTIAL (Transact-SQL)]:https://msdn.microsoft.com/library/ms189522.aspx
[CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)]:https://msdn.microsoft.com/library/mt270260.aspx
[DROP CREDENTIAL (Transact-SQL)]:https://msdn.microsoft.com/library/ms189450.aspx
