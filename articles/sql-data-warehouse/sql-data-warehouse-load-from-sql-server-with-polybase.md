---
title: "Charger des données à partir de SQL Server dans Azure SQL Data Warehouse (PolyBase) | Microsoft Docs"
description: "Utilise BCP pour exporter des données à partir de SQL Server vers des fichiers plats, AZCopy pour importer des données dans le stockage d’objets blob Azure et PolyBase pour recevoir les données dans Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 860c86e0-90f7-492c-9a84-1bdd3d1735cd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 966100094f98bae41bf90df500d005fa78b31ec3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="load-data-with-polybase-in-sql-data-warehouse"></a><span data-ttu-id="d44f1-103">Télécharger des données avec PolyBase dans SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="d44f1-103">Load data with PolyBase in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d44f1-104">SSIS</span><span class="sxs-lookup"><span data-stu-id="d44f1-104">SSIS</span></span>](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [<span data-ttu-id="d44f1-105">PolyBase</span><span class="sxs-lookup"><span data-stu-id="d44f1-105">PolyBase</span></span>](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [<span data-ttu-id="d44f1-106">bcp</span><span class="sxs-lookup"><span data-stu-id="d44f1-106">bcp</span></span>](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

<span data-ttu-id="d44f1-107">Ce didacticiel explique comment charger des données dans SQL Data Warehouse avec AzCopy et PolyBase.</span><span class="sxs-lookup"><span data-stu-id="d44f1-107">This tutorial shows how to load data into SQL Data Warehouse by using AzCopy and PolyBase.</span></span> <span data-ttu-id="d44f1-108">À la fin de ce didacticiel, vous saurez comment :</span><span class="sxs-lookup"><span data-stu-id="d44f1-108">When finished, you will know how to:</span></span>

* <span data-ttu-id="d44f1-109">Utilisez AzCopy pour copier des données vers le stockage d’objets blobs Azure</span><span class="sxs-lookup"><span data-stu-id="d44f1-109">Use AzCopy to copy data to Azure blob storage</span></span>
* <span data-ttu-id="d44f1-110">Créer des objets de base de données pour définir les données</span><span class="sxs-lookup"><span data-stu-id="d44f1-110">Create database objects to define the data</span></span>
* <span data-ttu-id="d44f1-111">Exécuter une requête T-SQL pour charger les données</span><span class="sxs-lookup"><span data-stu-id="d44f1-111">Run a T-SQL query to load the data</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-with-PolyBase-in-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="d44f1-112">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d44f1-112">Prerequisites</span></span>
<span data-ttu-id="d44f1-113">Pour parcourir ce didacticiel, vous avez besoin des éléments suivants</span><span class="sxs-lookup"><span data-stu-id="d44f1-113">To step through this tutorial, you need</span></span>

* <span data-ttu-id="d44f1-114">Une base de données SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="d44f1-114">A SQL Data Warehouse database.</span></span>
* <span data-ttu-id="d44f1-115">Un compte de stockage Azure de type stockage redondant local standard (LRS-Standard), stockage géo-redondant Standard (Standard-GRS) ou stockage géo-redondant avec accès en lecture Standard (Standard-RAGRS)</span><span class="sxs-lookup"><span data-stu-id="d44f1-115">An Azure storage account of type Standard Locally Redundant Storage (Standard-LRS), Standard Geo-Redundant Storage (Standard-GRS), or Standard Read-Access Geo-Redundant Storage (Standard-RAGRS).</span></span>
* <span data-ttu-id="d44f1-116">L’utilitaire de ligne de commande AzCopy</span><span class="sxs-lookup"><span data-stu-id="d44f1-116">AzCopy Command-Line Utility.</span></span> <span data-ttu-id="d44f1-117">Téléchargez et installez la [version la plus récente d’AzCopy][latest version of AzCopy] qui est installée avec les outils Stockage Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d44f1-117">Download and install the [latest version of AzCopy][latest version of AzCopy] which is installed with the Microsoft Azure Storage Tools.</span></span>
  
    ![Outils Azure Storage](./media/sql-data-warehouse-get-started-load-with-polybase/install-azcopy.png)

## <a name="step-1-add-sample-data-to-azure-blob-storage"></a><span data-ttu-id="d44f1-119">Étape 1 : ajouter les données exemple au stockage d’objets blobs Azure</span><span class="sxs-lookup"><span data-stu-id="d44f1-119">Step 1: Add sample data to Azure blob storage</span></span>
<span data-ttu-id="d44f1-120">Pour charger des données, nous devons placer des exemples de données dans un stockage d’objets blobs Azure.</span><span class="sxs-lookup"><span data-stu-id="d44f1-120">In order to load data, we need to put some sample data into an Azure blob storage.</span></span> <span data-ttu-id="d44f1-121">Lors de cette étape, nous allons remplir un objet blob Azure Storage avec des exemples de données.</span><span class="sxs-lookup"><span data-stu-id="d44f1-121">In this step we populate an Azure Storage blob with sample data.</span></span> <span data-ttu-id="d44f1-122">Plus tard, nous allons utiliser PolyBase pour charger ces exemples de données dans votre base de données SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d44f1-122">Later, we will use PolyBase to load this sample data into your SQL Data Warehouse database.</span></span>

### <a name="a-prepare-a-sample-text-file"></a><span data-ttu-id="d44f1-123">A.</span><span class="sxs-lookup"><span data-stu-id="d44f1-123">A.</span></span> <span data-ttu-id="d44f1-124">Préparer un exemple de fichier texte</span><span class="sxs-lookup"><span data-stu-id="d44f1-124">Prepare a sample text file</span></span>
<span data-ttu-id="d44f1-125">Pour préparer un exemple de fichier texte :</span><span class="sxs-lookup"><span data-stu-id="d44f1-125">To prepare a sample text file:</span></span>

1. <span data-ttu-id="d44f1-126">Ouvrez le Bloc-notes et copiez les lignes de données suivantes dans un nouveau fichier.</span><span class="sxs-lookup"><span data-stu-id="d44f1-126">Open Notepad and copy the following lines of data into a new file.</span></span> <span data-ttu-id="d44f1-127">Enregistrez-les dans votre répertoire temporaire local %temp%\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="d44f1-127">Save this to your local temp directory as %temp%\DimDate2.txt.</span></span>

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

### <a name="b-find-your-blob-service-endpoint"></a><span data-ttu-id="d44f1-128">B.</span><span class="sxs-lookup"><span data-stu-id="d44f1-128">B.</span></span> <span data-ttu-id="d44f1-129">Recherchez votre point de terminaison de service blob</span><span class="sxs-lookup"><span data-stu-id="d44f1-129">Find your blob service endpoint</span></span>
<span data-ttu-id="d44f1-130">Pour trouver votre point de terminaison de service blob :</span><span class="sxs-lookup"><span data-stu-id="d44f1-130">To find your blob service endpoint:</span></span>

1. <span data-ttu-id="d44f1-131">Dans le portail Azure, sélectionnez **Parcourir** > **Comptes de stockage**.</span><span class="sxs-lookup"><span data-stu-id="d44f1-131">From the Azure Portal select **Browse** > **Storage Accounts**.</span></span>
2. <span data-ttu-id="d44f1-132">Cliquez sur le compte de stockage que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="d44f1-132">Click the storage account you want to use.</span></span>
3. <span data-ttu-id="d44f1-133">Dans le panneau du compte de stockage, cliquez sur Objets blobs.</span><span class="sxs-lookup"><span data-stu-id="d44f1-133">In the Storage account blade, click Blobs</span></span>
   
    ![Cliquer sur les objets blobs](./media/sql-data-warehouse-get-started-load-with-polybase/click-blobs.png)
4. <span data-ttu-id="d44f1-135">Enregistrez votre URL de point de terminaison du service blob pour l’utiliser à une date ultérieure.</span><span class="sxs-lookup"><span data-stu-id="d44f1-135">Save your blob service endpoint URL for later.</span></span>
   
    ![Point de terminaison de service blob](./media/sql-data-warehouse-get-started-load-with-polybase/blob-service.png)

### <a name="c-find-your-azure-storage-key"></a><span data-ttu-id="d44f1-137">C.</span><span class="sxs-lookup"><span data-stu-id="d44f1-137">C.</span></span> <span data-ttu-id="d44f1-138">Rechercher votre clé de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="d44f1-138">Find your Azure storage key</span></span>
<span data-ttu-id="d44f1-139">Pour trouver votre clé de stockage Azure :</span><span class="sxs-lookup"><span data-stu-id="d44f1-139">To find your Azure storage key:</span></span>

1. <span data-ttu-id="d44f1-140">Dans le portail Azure, sélectionnez **Parcourir** > **Comptes de stockage**.</span><span class="sxs-lookup"><span data-stu-id="d44f1-140">From the Azure Portal, select **Browse** > **Storage Accounts**.</span></span>
2. <span data-ttu-id="d44f1-141">Cliquez sur le compte de stockage que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="d44f1-141">Click on the storage account you want to use.</span></span>
3. <span data-ttu-id="d44f1-142">Sélectionnez **Tous les paramètres** > **Clés d’accès**.</span><span class="sxs-lookup"><span data-stu-id="d44f1-142">Select **All settings** > **Access keys**.</span></span>
4. <span data-ttu-id="d44f1-143">Cliquez sur la zone de copie pour copier l’une de vos clés d’accès dans le presse-papiers.</span><span class="sxs-lookup"><span data-stu-id="d44f1-143">Click the copy box to copy one of your access keys to the clipboard.</span></span>
   
    ![Copier la clé de stockage Azure](./media/sql-data-warehouse-get-started-load-with-polybase/access-key.png)

### <a name="d-copy-the-sample-file-to-azure-blob-storage"></a><span data-ttu-id="d44f1-145">D.</span><span class="sxs-lookup"><span data-stu-id="d44f1-145">D.</span></span> <span data-ttu-id="d44f1-146">Copiez l’exemple de fichier de données dans le stockage d’objets blobs Azure.</span><span class="sxs-lookup"><span data-stu-id="d44f1-146">Copy the sample file to Azure blob storage</span></span>
<span data-ttu-id="d44f1-147">Pour copier vos données dans le stockage d’objets blob Azure :</span><span class="sxs-lookup"><span data-stu-id="d44f1-147">To copy your data to Azure blob storage:</span></span>

1. <span data-ttu-id="d44f1-148">Ouvrez une invite de commandes, puis changez de répertoire pour le répertoire d’installation AzCopy.</span><span class="sxs-lookup"><span data-stu-id="d44f1-148">Open a command prompt, and change directories to the AzCopy installation directory.</span></span> <span data-ttu-id="d44f1-149">Cette commande passe au répertoire d’installation par défaut sur un client Windows 64 bits.</span><span class="sxs-lookup"><span data-stu-id="d44f1-149">This command changes to the default installation directory on a 64-bit Windows client.</span></span>
   
    ```
    cd /d "%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy"
    ```
2. <span data-ttu-id="d44f1-150">Exécutez la commande suivante pour télécharger le fichier.</span><span class="sxs-lookup"><span data-stu-id="d44f1-150">Run the following command to upload the file.</span></span> <span data-ttu-id="d44f1-151">Spécifiez l’URL du point de terminaison de votre service d’objets blobs pour <blob service endpoint URL> et votre clé de compte de stockage Azure pour <azure_storage_account_key>.</span><span class="sxs-lookup"><span data-stu-id="d44f1-151">Specify your blob service endpoint URL for <blob service endpoint URL> and your Azure storage account key for <azure_storage_account_key>.</span></span>
   
    ```
    .\AzCopy.exe /Source:C:\Temp\ /Dest:<blob service endpoint URL> /datacontainer/datedimension/ /DestKey:<azure_storage_account_key> /Pattern:DimDate2.txt
    ```

<span data-ttu-id="d44f1-152">Consultez également [Prise en main de l’utilitaire de ligne de commande AzCopy][latest version of AzCopy].</span><span class="sxs-lookup"><span data-stu-id="d44f1-152">See also [Getting Started with the AzCopy Command-Line Utility][latest version of AzCopy].</span></span>

### <a name="e-explore-your-blob-storage-container"></a><span data-ttu-id="d44f1-153">E.</span><span class="sxs-lookup"><span data-stu-id="d44f1-153">E.</span></span> <span data-ttu-id="d44f1-154">Explorer votre conteneur de stockage d’objets blobs</span><span class="sxs-lookup"><span data-stu-id="d44f1-154">Explore your blob storage container</span></span>
<span data-ttu-id="d44f1-155">Pour voir le fichier que vous avez téléchargé vers le stockage d’objets blobs :</span><span class="sxs-lookup"><span data-stu-id="d44f1-155">To see the file you uploaded to blob storage:</span></span>

1. <span data-ttu-id="d44f1-156">Revenez au panneau de votre service d’objets blobs.</span><span class="sxs-lookup"><span data-stu-id="d44f1-156">Go back to your Blob service blade.</span></span>
2. <span data-ttu-id="d44f1-157">Sous Conteneurs, double-cliquez sur **datacontainer**.</span><span class="sxs-lookup"><span data-stu-id="d44f1-157">Under Containers, double-click **datacontainer**.</span></span>
3. <span data-ttu-id="d44f1-158">Pour explorer le chemin d’accès à vos données, cliquez sur le dossier **datedimension** et vous verrez votre fichier **DimDate2.txt** chargé.</span><span class="sxs-lookup"><span data-stu-id="d44f1-158">To explore the path to your data, click the folder **datedimension** and you will see your uploaded file **DimDate2.txt**.</span></span>
4. <span data-ttu-id="d44f1-159">Pour afficher les propriétés, cliquez sur **DimDate2.txt**.</span><span class="sxs-lookup"><span data-stu-id="d44f1-159">To view properties, click **DimDate2.txt**.</span></span>
5. <span data-ttu-id="d44f1-160">Le panneau de propriétés d’objets blobs vous permet de télécharger ou de supprimer le fichier.</span><span class="sxs-lookup"><span data-stu-id="d44f1-160">Note that in the Blob properties blade, you can download or delete the file.</span></span>
   
    ![Afficher le stockage blob Azure](./media/sql-data-warehouse-get-started-load-with-polybase/view-blob.png)

## <a name="step-2-create-an-external-table-for-the-sample-data"></a><span data-ttu-id="d44f1-162">Étape 2 : Créer une table externe pour les exemples de données</span><span class="sxs-lookup"><span data-stu-id="d44f1-162">Step 2: Create an external table for the sample data</span></span>
<span data-ttu-id="d44f1-163">Dans cette section, nous allons créer une table externe qui définit les exemples de données.</span><span class="sxs-lookup"><span data-stu-id="d44f1-163">In this section we create an external table that defines the sample data.</span></span>

<span data-ttu-id="d44f1-164">PolyBase utilise les tables externes pour accéder des données dans le stockage d’objets blobs Azure.</span><span class="sxs-lookup"><span data-stu-id="d44f1-164">PolyBase uses external tables to access data in Azure blob storage.</span></span> <span data-ttu-id="d44f1-165">Étant donné que les données ne sont pas stockées dans SQL Data Warehouse, PolyBase gère l’authentification pour les données externes à l’aide des informations d’identification de niveau base de données.</span><span class="sxs-lookup"><span data-stu-id="d44f1-165">Since the data is not stored within SQL Data Warehouse, PolyBase handles authentication to the external data by using a database-scoped credential.</span></span>

<span data-ttu-id="d44f1-166">Dans cette étape, l’exemple utilise les instructions Transact-SQL pour créer une table externe.</span><span class="sxs-lookup"><span data-stu-id="d44f1-166">The example in this step uses these Transact-SQL statements to create an external table.</span></span>

* <span data-ttu-id="d44f1-167">[Créer une clé principale (Transact-SQL)][Create Master Key (Transact-SQL)] pour chiffrer le secret de vos informations d’identification de niveau base de données.</span><span class="sxs-lookup"><span data-stu-id="d44f1-167">[Create Master Key (Transact-SQL)][Create Master Key (Transact-SQL)] to encrypt the secret of your database scoped credential.</span></span>
* <span data-ttu-id="d44f1-168">[Créer des informations d’identification de niveau base de données (Transact-SQL)][Create Database Scoped Credential (Transact-SQL)] pour spécifier les informations d’authentification de votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="d44f1-168">[Create Database Scoped Credential (Transact-SQL)][Create Database Scoped Credential (Transact-SQL)] to specify authentication information for your Azure storage account.</span></span>
* <span data-ttu-id="d44f1-169">[Créer une source de données externe (Transact-SQL)][Create External Data Source (Transact-SQL)] pour spécifier l’emplacement de votre stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="d44f1-169">[Create External Data Source (Transact-SQL)][Create External Data Source (Transact-SQL)] to specify the location of your Azure blob storage.</span></span>
* <span data-ttu-id="d44f1-170">[Créer un format de fichier externe (Transact-SQL)][Create External File Format (Transact-SQL)] pour spécifier le format de vos données.</span><span class="sxs-lookup"><span data-stu-id="d44f1-170">[Create External File Format (Transact-SQL)][Create External File Format (Transact-SQL)] to specify the format of your data.</span></span>
* <span data-ttu-id="d44f1-171">[Créer une table externe (Transact-SQL)][Create External Table (Transact-SQL)] pour spécifier la définition de la table et l’emplacement des données.</span><span class="sxs-lookup"><span data-stu-id="d44f1-171">[Create External Table (Transact-SQL)][Create External Table (Transact-SQL)] to specify the table definition and location of the data.</span></span>

<span data-ttu-id="d44f1-172">Exécutez cette requête sur votre base de données SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d44f1-172">Run this query against your SQL Data Warehouse database.</span></span> <span data-ttu-id="d44f1-173">Il crée une table externe nommée DimDate2External dans le schéma dbo qui pointe vers les données d’exemple DimDate2.txt dans le stockage d’objets blobs Azure.</span><span class="sxs-lookup"><span data-stu-id="d44f1-173">It will create an external table named DimDate2External in the dbo schema that points to the DimDate2.txt sample data in the Azure blob storage.</span></span>

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


-- D: Create an external file format
-- FORMAT_TYPE: Type of file format in Azure storage (supported: DELIMITEDTEXT, RCFILE, ORC, PARQUET).
-- FORMAT_OPTIONS: Specify field terminator, string delimiter, date format etc. for delimited text files.
-- Specify DATA_COMPRESSION method if data is compressed.

CREATE EXTERNAL FILE FORMAT TextFile
WITH (
    FORMAT_TYPE = DelimitedText,
    FORMAT_OPTIONS (FIELD_TERMINATOR = ',')
);


-- E: Create the external table
-- Specify column names and data types. This needs to match the data in the sample file.
-- LOCATION: Specify path to file or directory that contains the data (relative to the blob container).
-- To point to all files under the blob container, use LOCATION='.'

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


-- Run a query on the external table

SELECT count(*) FROM dbo.DimDate2External;

```


<span data-ttu-id="d44f1-174">Dans l’Explorateur d’objets SQL Server dans Visual Studio, vous pouvez voir le format de fichier externe, la source de données externe et la table DimDate2External.</span><span class="sxs-lookup"><span data-stu-id="d44f1-174">In SQL Server Object Explorer in Visual Studio, you can see the external file format, external data source, and the DimDate2External table.</span></span>

![Afficher les tables externes](./media/sql-data-warehouse-get-started-load-with-polybase/external-table.png)

## <a name="step-3-load-data-into-sql-data-warehouse"></a><span data-ttu-id="d44f1-176">Étape 3 : Charger des données dans SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="d44f1-176">Step 3: Load data into SQL Data Warehouse</span></span>
<span data-ttu-id="d44f1-177">Une fois la table externe créée, vous pouvez charger les données dans une nouvelle table ou les insérer dans une table existante.</span><span class="sxs-lookup"><span data-stu-id="d44f1-177">Once the external table is created, you can either load the data into a new table or insert it into an existing table.</span></span>

* <span data-ttu-id="d44f1-178">Pour charger les données dans une nouvelle table, exécutez l’instruction [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)].</span><span class="sxs-lookup"><span data-stu-id="d44f1-178">To load the data into a new table, run the [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] statement.</span></span> <span data-ttu-id="d44f1-179">La nouvelle table contient des colonnes nommées dans la requête.</span><span class="sxs-lookup"><span data-stu-id="d44f1-179">The new table will have the columns named in the query.</span></span> <span data-ttu-id="d44f1-180">Les types de données présentes dans les colonnes correspondent à des types de données dans la définition de la table externe.</span><span class="sxs-lookup"><span data-stu-id="d44f1-180">The data types of the columns will match the data types in the external table definition.</span></span>
* <span data-ttu-id="d44f1-181">Pour charger les données dans une table existante, utilisez l’instruction [INSERT...SELECT (Transact-SQL)][INSERT...SELECT (Transact-SQL)].</span><span class="sxs-lookup"><span data-stu-id="d44f1-181">To load the data into an existing table, use the [INSERT...SELECT (Transact-SQL)][INSERT...SELECT (Transact-SQL)] statement.</span></span>

```sql
-- Load the data from Azure blob storage to SQL Data Warehouse

CREATE TABLE dbo.DimDate2
WITH
(   
    CLUSTERED COLUMNSTORE INDEX,
    DISTRIBUTION = ROUND_ROBIN
)
AS
SELECT * FROM [dbo].[DimDate2External];
```

## <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="d44f1-182">Étape 4 : Créer des statistiques sur vos données nouvellement chargées</span><span class="sxs-lookup"><span data-stu-id="d44f1-182">Step 4: Create statistics on your newly loaded data</span></span>
<span data-ttu-id="d44f1-183">SQL Data Warehouse ne prend pas en charge les statistiques de création ou de mise à jour automatiques.</span><span class="sxs-lookup"><span data-stu-id="d44f1-183">SQL Data Warehouse does not auto-create or auto-update statistics.</span></span> <span data-ttu-id="d44f1-184">Par conséquent, pour obtenir des performances élevées pour les requêtes, il est important de créer des statistiques pour chaque colonne de chaque table après le premier chargement.</span><span class="sxs-lookup"><span data-stu-id="d44f1-184">Therefore, to achieve high query performance, it's important to create statistics on each column of each table after the first load.</span></span> <span data-ttu-id="d44f1-185">Il est également important de mettre à jour les statistiques après des modifications importantes des données.</span><span class="sxs-lookup"><span data-stu-id="d44f1-185">It's also important to update statistics after substantial changes in the data.</span></span>

<span data-ttu-id="d44f1-186">Cet exemple crée des statistiques de colonne unique sur la nouvelle table DimDate2.</span><span class="sxs-lookup"><span data-stu-id="d44f1-186">This example creates single-column statistics on the new DimDate2 table.</span></span>

```sql
CREATE STATISTICS [DateId] on [DimDate2] ([DateId]);
CREATE STATISTICS [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
CREATE STATISTICS [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
```

<span data-ttu-id="d44f1-187">Pour en savoir plus, consultez la section [Statistiques][Statistics].</span><span class="sxs-lookup"><span data-stu-id="d44f1-187">To learn more, see [Statistics][Statistics].</span></span>  

## <a name="next-steps"></a><span data-ttu-id="d44f1-188">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d44f1-188">Next steps</span></span>
<span data-ttu-id="d44f1-189">Consultez le [guide PolyBase][PolyBase guide] pour obtenir d’autres informations sur le développement d’une solution utilisant PolyBase.</span><span class="sxs-lookup"><span data-stu-id="d44f1-189">See the [PolyBase guide][PolyBase guide] for further information you should know as you develop a solution that uses PolyBase.</span></span>

<!--Image references-->


<!--Article references-->
[PolyBase in SQL Data Warehouse Tutorial]: ./sql-data-warehouse-get-started-load-with-polybase.md
[Load data with bcp]: ./sql-data-warehouse-load-with-bcp.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[PolyBase guide]: ./sql-data-warehouse-load-polybase-guide.md
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
