---
title: "Outil de migration de base de données Azure Cosmos DB | Microsoft Docs"
description: "Découvrez comment utiliser l’outil de migration de données open source Azure Cosmos DB pour importer des données depuis différentes sources, y compris des fichiers MongoDB, SQL Server, Stockage Table, Amazon DynamoDB, CSV et JSON. Conversion CSV vers JSON."
keywords: "csv vers json, outils de migration de base de données, conversion csv vers json"
services: cosmos-db
author: andrewhoh
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: d173581d-782a-445c-98d9-5e3c49b00e25
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: anhoh
ms.custom: mvc
ms.openlocfilehash: 23a4a82dbdb611f4da90562af936fca28da9b24d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-import-data-into-azure-cosmos-db-for-the-documentdb-api"></a><span data-ttu-id="efa58-105">Importer des données dans Azure Cosmos DB pour l’API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="efa58-105">How to import data into Azure Cosmos DB for the DocumentDB API?</span></span>

<span data-ttu-id="efa58-106">Ce didacticiel montre comment utiliser l’outil de migration de données de l’API DocumentDB Azure Cosmos DB pour importer des données dans Azure Cosmos DB à partir de différentes sources, y compris des fichiers JSON, des fichiers CSV, SQL, MongoDB, le stockage Table Azure, Amazon DynamoDB et les collections de l’API DocumentDB Azure Cosmos DB, dans des collections en vue de les utiliser avec Azure Cosmos DB et l’API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="efa58-106">This tutorial provides instructions on using the Azure Cosmos DB: DocumentDB API Data Migration tool, which can import data from various sources, including JSON files, CSV files, SQL, MongoDB, Azure Table storage, Amazon DynamoDB and Azure Cosmos DB DocumentDB API collections into collections for use with Azure Cosmos DB and the DocumentDB API.</span></span> <span data-ttu-id="efa58-107">L’outil de migration de données peut également être utilisé pour migrer des données à partir d’une collection à partition unique vers une collection à plusieurs partitions pour l’API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="efa58-107">The Data Migration tool can also be used when migrating from a single partition collection to a multi-partition collection for the DocumentDB API.</span></span>

<span data-ttu-id="efa58-108">L’outil de migration de données fonctionne uniquement lors de l’importation de données dans Azure Cosmos DB pour une utilisation avec l’API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="efa58-108">The Data Migration tool only works when importing data into Azure Cosmos DB for use with the DocumentDB API.</span></span> <span data-ttu-id="efa58-109">L’importation de données pour une utilisation avec l’API Table ou l’API Graph n’est pas prise en charge pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="efa58-109">Importing data for use with the Table API or Graph API is not supported at this time.</span></span> 

<span data-ttu-id="efa58-110">Pour importer des données pour une utilisation avec l’API MongoDB, consultez [Azure Cosmos DB: How to migrate data for the MongoDB API?](mongodb-migrate.md) (Azure Cosmos DB : migrer des données pour l’API MongoDB).</span><span class="sxs-lookup"><span data-stu-id="efa58-110">To import data for use with the MongoDB API, see [Azure Cosmos DB: How to migrate data for the MongoDB API?](mongodb-migrate.md).</span></span>

<span data-ttu-id="efa58-111">Ce didacticiel décrit les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="efa58-111">This tutorial covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="efa58-112">Installation de l’outil de migration de données</span><span class="sxs-lookup"><span data-stu-id="efa58-112">Installing the Data Migration tool</span></span>
> * <span data-ttu-id="efa58-113">Importation de données à partir de différentes sources de données</span><span class="sxs-lookup"><span data-stu-id="efa58-113">Importing data from different data sources</span></span>
> * <span data-ttu-id="efa58-114">Exportation de données à partir d’Azure Cosmos DB vers JSON</span><span class="sxs-lookup"><span data-stu-id="efa58-114">Exporting from Azure Cosmos DB to JSON</span></span>

## <span data-ttu-id="efa58-115"><a id="Prerequisites"></a>Configuration requise</span><span class="sxs-lookup"><span data-stu-id="efa58-115"><a id="Prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="efa58-116">Avant de suivre les instructions de cet article, vérifiez que les éléments suivants sont installés :</span><span class="sxs-lookup"><span data-stu-id="efa58-116">Before following the instructions in this article, ensure that you have the following installed:</span></span>

* <span data-ttu-id="efa58-117">[Microsoft .NET Framework 4.51](https://www.microsoft.com/download/developer-tools.aspx) ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="efa58-117">[Microsoft .NET Framework 4.51](https://www.microsoft.com/download/developer-tools.aspx) or higher.</span></span>

## <span data-ttu-id="efa58-118"><a id="Overviewl"></a>Présentation de l’outil de migration de données</span><span class="sxs-lookup"><span data-stu-id="efa58-118"><a id="Overviewl"></a>Overview of the Data Migration tool</span></span>
<span data-ttu-id="efa58-119">L’outil de migration de données est une solution open source permettant d’importer des données dans Azure Cosmos DB à partir de différentes sources, notamment :</span><span class="sxs-lookup"><span data-stu-id="efa58-119">The Data Migration tool is an open source solution that imports data to Azure Cosmos DB from a variety of sources, including:</span></span>

* <span data-ttu-id="efa58-120">Fichiers JSON</span><span class="sxs-lookup"><span data-stu-id="efa58-120">JSON files</span></span>
* <span data-ttu-id="efa58-121">MongoDB</span><span class="sxs-lookup"><span data-stu-id="efa58-121">MongoDB</span></span>
* <span data-ttu-id="efa58-122">SQL Server</span><span class="sxs-lookup"><span data-stu-id="efa58-122">SQL Server</span></span>
* <span data-ttu-id="efa58-123">Fichiers CSV</span><span class="sxs-lookup"><span data-stu-id="efa58-123">CSV files</span></span>
* <span data-ttu-id="efa58-124">Stockage de tables Azure</span><span class="sxs-lookup"><span data-stu-id="efa58-124">Azure Table storage</span></span>
* <span data-ttu-id="efa58-125">Amazon DynamoDB</span><span class="sxs-lookup"><span data-stu-id="efa58-125">Amazon DynamoDB</span></span>
* <span data-ttu-id="efa58-126">HBase</span><span class="sxs-lookup"><span data-stu-id="efa58-126">HBase</span></span>
* <span data-ttu-id="efa58-127">Collections Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="efa58-127">Azure Cosmos DB collections</span></span>

<span data-ttu-id="efa58-128">L'outil d'importation inclut une interface utilisateur graphique (dtui.exe) et peut aussi être piloté à partir de la ligne de commande (dt.exe).</span><span class="sxs-lookup"><span data-stu-id="efa58-128">While the import tool includes a graphical user interface (dtui.exe), it can also be driven from the command line (dt.exe).</span></span> <span data-ttu-id="efa58-129">En fait, il existe une option pour générer la commande associée après avoir configuré une importation via l'interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="efa58-129">In fact, there is an option to output the associated command after setting up an import through the UI.</span></span> <span data-ttu-id="efa58-130">Des données sources tabulaires (par exemple, des fichiers SQL Server ou CSV) peuvent être transformées de manière à ce que des relations hiérarchiques (sous-documents) puissent être créées pendant l'importation.</span><span class="sxs-lookup"><span data-stu-id="efa58-130">Tabular source data (e.g. SQL Server or CSV files) can be transformed such that hierarchical relationships (subdocuments) can be created during import.</span></span> <span data-ttu-id="efa58-131">Poursuivez votre lecture pour en savoir plus sur les options sources, les exemples de lignes de commande pour l’importation depuis chaque source, les options cibles et l'affichage des résultats d’importation.</span><span class="sxs-lookup"><span data-stu-id="efa58-131">Keep reading to learn more about source options, sample command lines to import from each source, target options, and viewing import results.</span></span>

## <span data-ttu-id="efa58-132"><a id="Install"></a>Installer l’outil de migration de données</span><span class="sxs-lookup"><span data-stu-id="efa58-132"><a id="Install"></a>Install the Data Migration tool</span></span>
<span data-ttu-id="efa58-133">Le code source de l’outil de migration est disponible sur GitHub dans [ce dépôt](https://github.com/azure/azure-documentdb-datamigrationtool) et une version compilée est disponible dans le [Centre de téléchargement Microsoft](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d).</span><span class="sxs-lookup"><span data-stu-id="efa58-133">The migration tool source code is available on GitHub in [this repository](https://github.com/azure/azure-documentdb-datamigrationtool) and a compiled version is available from [Microsoft Download Center](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d).</span></span> <span data-ttu-id="efa58-134">Vous pouvez compiler la solution ou simplement télécharger et extraire la version compilée dans un répertoire de votre choix.</span><span class="sxs-lookup"><span data-stu-id="efa58-134">You may either compile the solution or simply download and extract the compiled version to a directory of your choice.</span></span> <span data-ttu-id="efa58-135">Exécutez ensuite l’un des fichiers suivants :</span><span class="sxs-lookup"><span data-stu-id="efa58-135">Then run either:</span></span>

* <span data-ttu-id="efa58-136">**Dtui.exe**: version de l’interface graphique de l’outil</span><span class="sxs-lookup"><span data-stu-id="efa58-136">**Dtui.exe**: Graphical interface version of the tool</span></span>
* <span data-ttu-id="efa58-137">**Dt.exe**: version en ligne de commande de l’outil</span><span class="sxs-lookup"><span data-stu-id="efa58-137">**Dt.exe**: Command-line version of the tool</span></span>

## <a name="import-data"></a><span data-ttu-id="efa58-138">Importer des données</span><span class="sxs-lookup"><span data-stu-id="efa58-138">Import data</span></span>

<span data-ttu-id="efa58-139">Une fois que vous avez installé l’outil, il est temps d’importer vos données.</span><span class="sxs-lookup"><span data-stu-id="efa58-139">Once you've installed the tool, it's time to import your data.</span></span> <span data-ttu-id="efa58-140">Quel type de données voulez-vous importer ?</span><span class="sxs-lookup"><span data-stu-id="efa58-140">What kind of data do you want to import?</span></span>

* [<span data-ttu-id="efa58-141">Fichiers JSON</span><span class="sxs-lookup"><span data-stu-id="efa58-141">JSON files</span></span>](#JSON)
* [<span data-ttu-id="efa58-142">MongoDB</span><span class="sxs-lookup"><span data-stu-id="efa58-142">MongoDB</span></span>](#MongoDB)
* [<span data-ttu-id="efa58-143">Fichiers d’exportation MongoDB</span><span class="sxs-lookup"><span data-stu-id="efa58-143">MongoDB Export files</span></span>](#MongoDBExport)
* [<span data-ttu-id="efa58-144">SQL Server</span><span class="sxs-lookup"><span data-stu-id="efa58-144">SQL Server</span></span>](#SQL)
* [<span data-ttu-id="efa58-145">Fichiers CSV</span><span class="sxs-lookup"><span data-stu-id="efa58-145">CSV files</span></span>](#CSV)
* [<span data-ttu-id="efa58-146">Stockage Table Azure</span><span class="sxs-lookup"><span data-stu-id="efa58-146">Azure Table storage</span></span>](#AzureTableSource)
* [<span data-ttu-id="efa58-147">Amazon DynamoDB</span><span class="sxs-lookup"><span data-stu-id="efa58-147">Amazon DynamoDB</span></span>](#DynamoDBSource)
* [<span data-ttu-id="efa58-148">Objet blob</span><span class="sxs-lookup"><span data-stu-id="efa58-148">Blob</span></span>](#BlobImport)
* [<span data-ttu-id="efa58-149">Collections Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="efa58-149">Azure Cosmos DB collections</span></span>](#DocumentDBSource)
* [<span data-ttu-id="efa58-150">HBase</span><span class="sxs-lookup"><span data-stu-id="efa58-150">HBase</span></span>](#HBaseSource)
* [<span data-ttu-id="efa58-151">Importation en bloc Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="efa58-151">Azure Cosmos DB bulk import</span></span>](#DocumentDBBulkImport)
* [<span data-ttu-id="efa58-152">Importation d’enregistrement séquentiel Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="efa58-152">Azure Cosmos DB sequential record import</span></span>](#DocumentDSeqTarget)


## <span data-ttu-id="efa58-153"><a id="JSON"></a>Importation de fichiers JSON</span><span class="sxs-lookup"><span data-stu-id="efa58-153"><a id="JSON"></a>To import JSON files</span></span>
<span data-ttu-id="efa58-154">L'option d'importateur source du fichier JSON vous permet d'importer un ou plusieurs fichiers JSON ou des fichiers JSON qui contiennent chacun un tableau de documents JSON.</span><span class="sxs-lookup"><span data-stu-id="efa58-154">The JSON file source importer option allows you to import one or more single document JSON files or JSON files that each contain an array of JSON documents.</span></span> <span data-ttu-id="efa58-155">Quand vous ajoutez des dossiers qui contiennent des fichiers JSON à importer, vous avez la possibilité de rechercher des fichiers de manière récursive dans les sous-dossiers.</span><span class="sxs-lookup"><span data-stu-id="efa58-155">When adding folders that contain JSON files to import, you have the option of recursively searching for files in subfolders.</span></span>

![Capture d’écran des options sources du fichier JSON - Outils de migration de base de données](./media/import-data/jsonsource.png)

<span data-ttu-id="efa58-157">Voici quelques exemples de lignes de commande pour importer des fichiers JSON :</span><span class="sxs-lookup"><span data-stu-id="efa58-157">Here are some command line samples to import JSON files:</span></span>

    #Import a single JSON file
    dt.exe /s:JsonFile /s.Files:.\Sessions.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Sessions /t.CollectionThroughput:2500

    #Import a directory of JSON files
    dt.exe /s:JsonFile /s.Files:C:\TESessions\*.json /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Sessions /t.CollectionThroughput:2500

    #Import a directory (including sub-directories) of JSON files
    dt.exe /s:JsonFile /s.Files:C:\LastFMMusic\**\*.json /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Music /t.CollectionThroughput:2500

    #Import a directory (single), directory (recursive), and individual JSON files
    dt.exe /s:JsonFile /s.Files:C:\Tweets\*.*;C:\LargeDocs\**\*.*;C:\TESessions\Session48172.json;C:\TESessions\Session48173.json;C:\TESessions\Session48174.json;C:\TESessions\Session48175.json;C:\TESessions\Session48177.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:subs /t.CollectionThroughput:2500

    #Import a single JSON file and partition the data across 4 collections
    dt.exe /s:JsonFile /s.Files:D:\\CompanyData\\Companies.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:comp[1-4] /t.PartitionKey:name /t.CollectionThroughput:2500

## <span data-ttu-id="efa58-158"><a id="MongoDB"></a>Importation à partir de MongoDB</span><span class="sxs-lookup"><span data-stu-id="efa58-158"><a id="MongoDB"></a>To import from MongoDB</span></span>

> [!IMPORTANT]
> <span data-ttu-id="efa58-159">Si vous importez des données vers un compte Azure Cosmos DB avec la prise en charge de MongoDB, suivez ces [instructions](mongodb-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="efa58-159">If you are importing to an Azure Cosmos DB account with Support for MongoDB, follow these [instructions](mongodb-migrate.md).</span></span>
> 
> 

<span data-ttu-id="efa58-160">L'option d'importateur source MongoDB vous permet d’importer à partir d'une collection MongoDB individuelle et de filtrer éventuellement les documents à l'aide d'une requête et/ou de modifier la structure du document à l'aide d'une projection.</span><span class="sxs-lookup"><span data-stu-id="efa58-160">The MongoDB source importer option allows you to import from an individual MongoDB collection and optionally filter documents using a query and/or modify the document structure by using a projection.</span></span>  

![Capture d’écran des options sources MongoDB](./media/import-data/mongodbsource.png)

<span data-ttu-id="efa58-162">La chaîne de connexion est au format MongoDB standard :</span><span class="sxs-lookup"><span data-stu-id="efa58-162">The connection string is in the standard MongoDB format:</span></span>

    mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database>

> [!NOTE]
> <span data-ttu-id="efa58-163">Utilisez la commande Verify pour vous assurer que l'instance MongoDB spécifiée dans le champ de la chaîne de connexion est accessible.</span><span class="sxs-lookup"><span data-stu-id="efa58-163">Use the Verify command to ensure that the MongoDB instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="efa58-164">Saisissez le nom de la collection depuis laquelle les données seront importées.</span><span class="sxs-lookup"><span data-stu-id="efa58-164">Enter the name of the collection from which data will be imported.</span></span> <span data-ttu-id="efa58-165">Vous pouvez éventuellement spécifier ou fournir un fichier pour une requête (par exemple, {pop: {$gt: 5000}} ) et/ou une projection (par exemple, {loc:0} ) pour filtrer et mettre en forme les données à importer.</span><span class="sxs-lookup"><span data-stu-id="efa58-165">You may optionally specify or provide a file for a query (e.g. {pop: {$gt:5000}} ) and/or projection (e.g. {loc:0} ) to both filter and shape the data to be imported.</span></span>

<span data-ttu-id="efa58-166">Voici quelques exemples de ligne de commande pour l’importation depuis MongoDB :</span><span class="sxs-lookup"><span data-stu-id="efa58-166">Here are some command line samples to import from MongoDB:</span></span>

    #Import all documents from a MongoDB collection
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZips /t.IdField:_id /t.CollectionThroughput:2500

    #Import documents from a MongoDB collection which match the query and exclude the loc field
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /s.Query:{pop:{$gt:50000}} /s.Projection:{loc:0} /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZipsTransform /t.IdField:_id/t.CollectionThroughput:2500

## <span data-ttu-id="efa58-167"><a id="MongoDBExport"></a>Importation de fichiers d’exportation MongoDB</span><span class="sxs-lookup"><span data-stu-id="efa58-167"><a id="MongoDBExport"></a>To import MongoDB export files</span></span>

> [!IMPORTANT]
> <span data-ttu-id="efa58-168">Si vous importez des données vers un compte Azure Cosmos DB prenant en charge MongoDB, suivez ces [instructions](mongodb-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="efa58-168">If you are importing to an Azure Cosmos DB account with support for MongoDB, follow these [instructions](mongodb-migrate.md).</span></span>
> 
> 

<span data-ttu-id="efa58-169">L’option d’importateur source du fichier JSON d’exportation MongoDB vous permet d’importer un ou plusieurs fichiers JSON générés depuis l’utilitaire mongoexport.</span><span class="sxs-lookup"><span data-stu-id="efa58-169">The MongoDB export JSON file source importer option allows you to import one or more JSON files produced from the mongoexport utility.</span></span>  

![Capture d’écran des options sources d’exportation MongoDB](./media/import-data/mongodbexportsource.png)

<span data-ttu-id="efa58-171">Lorsque vous ajoutez des dossiers qui contiennent des fichiers JSON d’exportation à importer, vous avez la possibilité de rechercher des fichiers de manière récursive dans les sous-dossiers.</span><span class="sxs-lookup"><span data-stu-id="efa58-171">When adding folders that contain MongoDB export JSON files for import, you have the option of recursively searching for files in subfolders.</span></span>

<span data-ttu-id="efa58-172">Voici un exemple de ligne de commande pour importer à partir de fichiers JSON d'exportation MongoDB :</span><span class="sxs-lookup"><span data-stu-id="efa58-172">Here is a command line sample to import from MongoDB export JSON files:</span></span>

    dt.exe /s:MongoDBExport /s.Files:D:\mongoemployees.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:employees /t.IdField:_id /t.Dates:Epoch /t.CollectionThroughput:2500

## <span data-ttu-id="efa58-173"><a id="SQL"></a>Importation depuis SQL Server</span><span class="sxs-lookup"><span data-stu-id="efa58-173"><a id="SQL"></a>To import from SQL Server</span></span>
<span data-ttu-id="efa58-174">L’option d’importateur source SQL vous permet d'importer à partir d'une base de données SQL Server individuelle et de filtrer éventuellement les enregistrements à importer à l'aide d'une requête.</span><span class="sxs-lookup"><span data-stu-id="efa58-174">The SQL source importer option allows you to import from an individual SQL Server database and optionally filter the records to be imported using a query.</span></span> <span data-ttu-id="efa58-175">De plus, vous pouvez modifier la structure du document en spécifiant un séparateur d'imbrication (plus d’informations dans un instant).</span><span class="sxs-lookup"><span data-stu-id="efa58-175">In addition, you can modify the document structure by specifying a nesting separator (more on that in a moment).</span></span>  

![Capture d’écran des options sources SQL - Outils de migration de base de données](./media/import-data/sqlexportsource.png)

<span data-ttu-id="efa58-177">Le format de la chaîne de connexion est le format de chaîne de connexion SQL standard.</span><span class="sxs-lookup"><span data-stu-id="efa58-177">The format of the connection string is the standard SQL connection string format.</span></span>

> [!NOTE]
> <span data-ttu-id="efa58-178">Utilisez la commande Verify pour vous assurer que l'instance SQL Server spécifiée dans le champ de la chaîne de connexion est accessible.</span><span class="sxs-lookup"><span data-stu-id="efa58-178">Use the Verify command to ensure that the SQL Server instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="efa58-179">La propriété du séparateur d'imbrication est utilisée pour créer des relations hiérarchiques (sous-documents) lors de l'importation.</span><span class="sxs-lookup"><span data-stu-id="efa58-179">The nesting separator property is used to create hierarchical relationships (sub-documents) during import.</span></span> <span data-ttu-id="efa58-180">Examinez la requête SQL suivante :</span><span class="sxs-lookup"><span data-stu-id="efa58-180">Consider the following SQL query:</span></span>

<span data-ttu-id="efa58-181">*select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'*</span><span class="sxs-lookup"><span data-stu-id="efa58-181">*select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'*</span></span>

<span data-ttu-id="efa58-182">Cette requête retourne les résultats (partiels) suivants :</span><span class="sxs-lookup"><span data-stu-id="efa58-182">Which returns the following (partial) results:</span></span>

![Capture d’écran des résultats de requête SQL](./media/import-data/sqlqueryresults.png)

<span data-ttu-id="efa58-184">Notez les alias tels que Address.AddressType et Address.Location.StateProvinceName.</span><span class="sxs-lookup"><span data-stu-id="efa58-184">Note the aliases such as Address.AddressType and Address.Location.StateProvinceName.</span></span> <span data-ttu-id="efa58-185">En spécifiant un séparateur d'imbrication de « . », l'outil d'importation crée les sous-documents Address et Address.Location lors de l'importation.</span><span class="sxs-lookup"><span data-stu-id="efa58-185">By specifying a nesting separator of ‘.’, the import tool creates Address and Address.Location subdocuments during the import.</span></span> <span data-ttu-id="efa58-186">Voici un exemple de document qui en résulte dans Azure Cosmos DB :</span><span class="sxs-lookup"><span data-stu-id="efa58-186">Here is an example of a resulting document in Azure Cosmos DB:</span></span>

<span data-ttu-id="efa58-187">*{« ID » : « 956 », « Nom » : « Service et vente au détail », « Adresse »: {« AddressType »: « Siège », « AddressLine1 »: « #500-75 o ’ Connor Street », « Lieu »: {« Ville »: « Ottawa », « StateProvinceName »: « Ontario »}, « Code postal »: « K4B 1S2 », « CountryRegionName »: « Canada »}}*</span><span class="sxs-lookup"><span data-stu-id="efa58-187">*{ "id": "956", "Name": "Finer Sales and Service", "Address": { "AddressType": "Main Office", "AddressLine1": "#500-75 O'Connor Street", "Location": { "City": "Ottawa", "StateProvinceName": "Ontario" }, "PostalCode": "K4B 1S2", "CountryRegionName": "Canada" } }*</span></span>

<span data-ttu-id="efa58-188">Voici quelques exemples de lignes de commande pour l’importation depuis SQL Server :</span><span class="sxs-lookup"><span data-stu-id="efa58-188">Here are some command line samples to import from SQL Server:</span></span>

    #Import records from SQL which match a query
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, * from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Stores /t.IdField:Id /t.CollectionThroughput:2500

    #Import records from sql which match a query and create hierarchical relationships
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /s.NestingSeparator:. /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:StoresSub /t.IdField:Id /t.CollectionThroughput:2500

## <span data-ttu-id="efa58-189"><a id="CSV"></a>Importation de fichiers CSV et conversion de fichiers CSV au format JSON</span><span class="sxs-lookup"><span data-stu-id="efa58-189"><a id="CSV"></a>To import CSV files and convert CSV to JSON</span></span>
<span data-ttu-id="efa58-190">L'option d'importateur source du fichier CSV vous permet d'importer un ou plusieurs fichiers CSV.</span><span class="sxs-lookup"><span data-stu-id="efa58-190">The CSV file source importer option enables you to import one or more CSV files.</span></span> <span data-ttu-id="efa58-191">Quand vous ajoutez des dossiers qui contiennent des fichiers CSV à importer, vous avez la possibilité de rechercher des fichiers de manière récursive dans les sous-dossiers.</span><span class="sxs-lookup"><span data-stu-id="efa58-191">When adding folders that contain CSV files for import, you have the option of recursively searching for files in subfolders.</span></span>

![Capture d’écran des options sources CSV - CSV vers JSON](media/import-data/csvsource.png)

<span data-ttu-id="efa58-193">De même que pour la source SQL, la propriété du séparateur d'imbrication peut être utilisée pour créer des relations hiérarchiques (sous-documents) lors de l'importation.</span><span class="sxs-lookup"><span data-stu-id="efa58-193">Similar to the SQL source, the nesting separator property may be used to create hierarchical relationships (sub-documents) during import.</span></span> <span data-ttu-id="efa58-194">Prenez en compte la ligne d'en-tête et les lignes de données du CSV suivant :</span><span class="sxs-lookup"><span data-stu-id="efa58-194">Consider the following CSV header row and data rows:</span></span>

![Capture d’écran des exemples d’enregistrement CSV - CSV vers JSON](./media/import-data/csvsample.png)

<span data-ttu-id="efa58-196">Notez les alias tels que DomainInfo.Domain_Name et RedirectInfo.Redirecting.</span><span class="sxs-lookup"><span data-stu-id="efa58-196">Note the aliases such as DomainInfo.Domain_Name and RedirectInfo.Redirecting.</span></span> <span data-ttu-id="efa58-197">En spécifiant un séparateur d'imbrication de « . », l'outil d'importation crée les sous-documents DomainInfo et RedirectInfo lors de l'importation.</span><span class="sxs-lookup"><span data-stu-id="efa58-197">By specifying a nesting separator of ‘.’, the import tool will create DomainInfo and RedirectInfo subdocuments during the import.</span></span> <span data-ttu-id="efa58-198">Voici un exemple de document qui en résulte dans Azure Cosmos DB :</span><span class="sxs-lookup"><span data-stu-id="efa58-198">Here is an example of a resulting document in Azure Cosmos DB:</span></span>

<span data-ttu-id="efa58-199">*{« DomainInfo » : {« Domain_name » : « ACUS.GOV », « Domain_Name_Address » : « http://www.ACUS.GOV »}, « Agence fédérale » : « Conférence administrative des États-Unis », « RedirectInfo » : {« Redirection » : « 0 », « Redirect_Destination » : « »}, « ID » : « 9cc565c5-ebcd-1c03-ebd3-cc3e2ecd814d »}*</span><span class="sxs-lookup"><span data-stu-id="efa58-199">*{ "DomainInfo": { "Domain_Name": "ACUS.GOV", "Domain_Name_Address": "http://www.ACUS.GOV" }, "Federal Agency": "Administrative Conference of the United States", "RedirectInfo": { "Redirecting": "0", "Redirect_Destination": "" }, "id": "9cc565c5-ebcd-1c03-ebd3-cc3e2ecd814d" }*</span></span>

<span data-ttu-id="efa58-200">L'outil d'importation va tenter de déduire les informations de type pour les valeurs sans guillemets dans les fichiers CSV (les valeurs entre guillemets sont toujours traitées comme des chaînes).</span><span class="sxs-lookup"><span data-stu-id="efa58-200">The import tool will attempt to infer type information for unquoted values in CSV files (quoted values are always treated as strings).</span></span>  <span data-ttu-id="efa58-201">Les types sont identifiés dans l'ordre suivant : nombre, date et heure, valeur booléenne.</span><span class="sxs-lookup"><span data-stu-id="efa58-201">Types are identified in the following order: number, datetime, boolean.</span></span>  

<span data-ttu-id="efa58-202">Deux autres points sont à prendre en considération concernant l'importation CSV :</span><span class="sxs-lookup"><span data-stu-id="efa58-202">There are two other things to note about CSV import:</span></span>

1. <span data-ttu-id="efa58-203">Par défaut, les valeurs sans guillemets sont toujours privées de leurs tabulations et espaces, tandis que les valeurs entre guillemets sont conservées telles quelles.</span><span class="sxs-lookup"><span data-stu-id="efa58-203">By default, unquoted values are always trimmed for tabs and spaces, while quoted values are preserved as-is.</span></span> <span data-ttu-id="efa58-204">Ce comportement peut être remplacé en cochant la case Trim quoted values (Rogner les valeurs entre guillemets) ou à l'aide de l'option de ligne de commande /s.TrimQuoted.</span><span class="sxs-lookup"><span data-stu-id="efa58-204">This behavior can be overridden with the Trim quoted values checkbox or the /s.TrimQuoted command line option.</span></span>
2. <span data-ttu-id="efa58-205">Par défaut, une valeur null sans guillemets est considérée comme une valeur null.</span><span class="sxs-lookup"><span data-stu-id="efa58-205">By default, an unquoted null is treated as a null value.</span></span> <span data-ttu-id="efa58-206">Ce comportement peut être remplacé (c'est-à-dire, traiter une valeur null sans guillemets comme une chaîne « null ») en cochant la case Treat unquoted NULL as string (Traiter les valeurs null sans guillemets comme des chaînes) ou à l'aide de l'option de ligne de commande /s.NoUnquotedNulls.</span><span class="sxs-lookup"><span data-stu-id="efa58-206">This behavior can be overridden (i.e. treat an unquoted null as a “null” string) with the Treat unquoted NULL as string checkbox or the /s.NoUnquotedNulls command line option.</span></span>

<span data-ttu-id="efa58-207">Voici un exemple de ligne de commande pour une importation CSV :</span><span class="sxs-lookup"><span data-stu-id="efa58-207">Here is a command line sample for CSV import:</span></span>

    dt.exe /s:CsvFile /s.Files:.\Employees.csv /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Employees /t.IdField:EntityID /t.CollectionThroughput:2500

## <span data-ttu-id="efa58-208"><a id="AzureTableSource"></a>Importation depuis le stockage de tables Azure</span><span class="sxs-lookup"><span data-stu-id="efa58-208"><a id="AzureTableSource"></a>To import from Azure Table storage</span></span>
<span data-ttu-id="efa58-209">L'option d’importateur source de stockage de tables Azure vous permet d'importer à partir d'une table de stockage de tables Azure individuelle et de filtrer éventuellement les entités de table à importer.</span><span class="sxs-lookup"><span data-stu-id="efa58-209">The Azure Table storage source importer option allows you to import from an individual Azure Table storage table and optionally filter the table entities to be imported.</span></span> <span data-ttu-id="efa58-210">Notez que vous ne pouvez pas utiliser l’outil de migration de données pour importer des données de stockage de tables Azure dans Azure Cosmos DB pour une utilisation avec l’API Table.</span><span class="sxs-lookup"><span data-stu-id="efa58-210">Note that you cannot use the Data Migration tool to import Azure Table storage data into Azure Cosmos DB for use with the Table API.</span></span> <span data-ttu-id="efa58-211">Seule l’importation vers Azure Cosmos DB pour une utilisation avec l’API DocumentDB est prise en charge pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="efa58-211">Only importing to Azure Cosmos DB for use with the DocumentDB API is supported at this time.</span></span>

![Capture d’écran des options sources de stockage de tables Azure](./media/import-data/azuretablesource.png)

<span data-ttu-id="efa58-213">Le format de la chaîne de connexion de stockage de tables Azure est :</span><span class="sxs-lookup"><span data-stu-id="efa58-213">The format of the Azure Table storage connection string is:</span></span>

    DefaultEndpointsProtocol=<protocol>;AccountName=<Account Name>;AccountKey=<Account Key>;

> [!NOTE]
> <span data-ttu-id="efa58-214">Utilisez la commande Verify pour vous assurer que l'instance de stockage de tables Azure spécifiée dans le champ de la chaîne de connexion est accessible.</span><span class="sxs-lookup"><span data-stu-id="efa58-214">Use the Verify command to ensure that the Azure Table storage instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="efa58-215">Saisissez le nom de la table Azure depuis laquelle les données seront importées.</span><span class="sxs-lookup"><span data-stu-id="efa58-215">Enter the name of the Azure table from which data will be imported.</span></span> <span data-ttu-id="efa58-216">Vous pouvez éventuellement spécifier un [filtre](https://msdn.microsoft.com/library/azure/ff683669.aspx).</span><span class="sxs-lookup"><span data-stu-id="efa58-216">You may optionally specify a [filter](https://msdn.microsoft.com/library/azure/ff683669.aspx).</span></span>

<span data-ttu-id="efa58-217">L'option d’importateur source de stockage de tables Azure dispose des options supplémentaires suivantes :</span><span class="sxs-lookup"><span data-stu-id="efa58-217">The Azure Table storage source importer option has the following additional options:</span></span>

1. <span data-ttu-id="efa58-218">Inclusion des champs internes</span><span class="sxs-lookup"><span data-stu-id="efa58-218">Include Internal Fields</span></span>
   1. <span data-ttu-id="efa58-219">Tous : inclure tous les champs internes (PartitionKey, RowKey et Timestamp)</span><span class="sxs-lookup"><span data-stu-id="efa58-219">All - Include all internal fields (PartitionKey, RowKey, and Timestamp)</span></span>
   2. <span data-ttu-id="efa58-220">Aucun : exclure tous les champs internes</span><span class="sxs-lookup"><span data-stu-id="efa58-220">None - Exclude all internal fields</span></span>
   3. <span data-ttu-id="efa58-221">RowKey : inclure uniquement le champ RowKey</span><span class="sxs-lookup"><span data-stu-id="efa58-221">RowKey - Only include the RowKey field</span></span>
2. <span data-ttu-id="efa58-222">Sélection des colonnes</span><span class="sxs-lookup"><span data-stu-id="efa58-222">Select Columns</span></span>
   1. <span data-ttu-id="efa58-223">Les filtres de stockage de tables Azure ne prennent pas en charge les projections.</span><span class="sxs-lookup"><span data-stu-id="efa58-223">Azure Table storage filters do not support projections.</span></span> <span data-ttu-id="efa58-224">Si vous souhaitez importer uniquement des propriétés d'entité de table Azure spécifiques, ajoutez-les à la liste Sélection des colonnes.</span><span class="sxs-lookup"><span data-stu-id="efa58-224">If you want to only import specific Azure Table entity properties, add them to the Select Columns list.</span></span> <span data-ttu-id="efa58-225">Toutes les autres propriétés d'entité seront ignorées.</span><span class="sxs-lookup"><span data-stu-id="efa58-225">All other entity properties will be ignored.</span></span>

<span data-ttu-id="efa58-226">Voici un exemple de ligne de commande pour importer depuis le stockage de tables Azure :</span><span class="sxs-lookup"><span data-stu-id="efa58-226">Here is a command line sample to import from Azure Table storage:</span></span>

    dt.exe /s:AzureTable /s.ConnectionString:"DefaultEndpointsProtocol=https;AccountName=<Account Name>;AccountKey=<Account Key>" /s.Table:metrics /s.InternalFields:All /s.Filter:"PartitionKey eq 'Partition1' and RowKey gt '00001'" /s.Projection:ObjectCount;ObjectSize  /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:metrics /t.CollectionThroughput:2500

## <span data-ttu-id="efa58-227"><a id="DynamoDBSource"></a>Importation à partir d’Amazon DynamoDB</span><span class="sxs-lookup"><span data-stu-id="efa58-227"><a id="DynamoDBSource"></a>To import from Amazon DynamoDB</span></span>
<span data-ttu-id="efa58-228">L’option d’importateur source d’Amazon DynamoDB vous permet d'importer à partir d'une table d’Amazon DynamoDB et de filtrer éventuellement les entités à importer.</span><span class="sxs-lookup"><span data-stu-id="efa58-228">The Amazon DynamoDB source importer option allows you to import from an individual Amazon DynamoDB table and optionally filter the entities to be imported.</span></span> <span data-ttu-id="efa58-229">Plusieurs modèles sont fournis pour faciliter au maximum la configuration d'une importation.</span><span class="sxs-lookup"><span data-stu-id="efa58-229">Several templates are provided so that setting up an import is as easy as possible.</span></span>

![Capture d’écran des options sources Amazon DynamoDB - Outils de migration de base de données](./media/import-data/dynamodbsource1.png)

![Capture d’écran des options sources Amazon DynamoDB - Outils de migration de base de données](./media/import-data/dynamodbsource2.png)

<span data-ttu-id="efa58-232">Le format de la chaîne de connexion Amazon DynamoDB est :</span><span class="sxs-lookup"><span data-stu-id="efa58-232">The format of the Amazon DynamoDB connection string is:</span></span>

    ServiceURL=<Service Address>;AccessKey=<Access Key>;SecretKey=<Secret Key>;

> [!NOTE]
> <span data-ttu-id="efa58-233">Utilisez la commande Verify pour vous assurer que l'instance Amazon DynamoBD spécifiée dans le champ de la chaîne de connexion est accessible.</span><span class="sxs-lookup"><span data-stu-id="efa58-233">Use the Verify command to ensure that the Amazon DynamoDB instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="efa58-234">Voici un exemple de ligne de commande pour importer à partir d'Amazon DynamoDB :</span><span class="sxs-lookup"><span data-stu-id="efa58-234">Here is a command line sample to import from Amazon DynamoDB:</span></span>

    dt.exe /s:DynamoDB /s.ConnectionString:ServiceURL=https://dynamodb.us-east-1.amazonaws.com;AccessKey=<accessKey>;SecretKey=<secretKey> /s.Request:"{   """TableName""": """ProductCatalog""" }" /t:DocumentDBBulk /t.ConnectionString:"AccountEndpoint=<Azure Cosmos DB Endpoint>;AccountKey=<Azure Cosmos DB Key>;Database=<Azure Cosmos DB Database>;" /t.Collection:catalogCollection /t.CollectionThroughput:2500

## <span data-ttu-id="efa58-235"><a id="BlobImport"></a>Importation de fichiers à partir du stockage blob Azure</span><span class="sxs-lookup"><span data-stu-id="efa58-235"><a id="BlobImport"></a>To import files from Azure Blob storage</span></span>
<span data-ttu-id="efa58-236">Les options d’importateur source du fichier JSON, du fichier d'exportation MongoDB et du fichier CSV vous permettent d'importer un ou plusieurs fichiers à partir du stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="efa58-236">The JSON file, MongoDB export file, and CSV file source importer options allow you to import one or more files from Azure Blob storage.</span></span> <span data-ttu-id="efa58-237">Après avoir spécifié l’URL d’un conteneur d'objets blob et une clé de compte, fournissez simplement une expression régulière pour sélectionner le(s) fichier(s) à importer.</span><span class="sxs-lookup"><span data-stu-id="efa58-237">After specifying a Blob container URL and Account Key, simply provide a regular expression to select the file(s) to import.</span></span>

![Capture d’écran des options sources du fichier blob](./media/import-data/blobsource.png)

<span data-ttu-id="efa58-239">Voici un exemple de ligne de commande pour importer des fichiers JSON à partir du stockage d’objets blob Azure :</span><span class="sxs-lookup"><span data-stu-id="efa58-239">Here is command line sample to import JSON files from Azure Blob storage:</span></span>

    dt.exe /s:JsonFile /s.Files:"blobs://<account key>@account.blob.core.windows.net:443/importcontainer/.*" /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:doctest

## <span data-ttu-id="efa58-240"><a id="DocumentDBSource"></a>Pour importer des données à partir d’une collection de l’API DocumentDB Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="efa58-240"><a id="DocumentDBSource"></a>To import from an Azure Cosmos DB DocumentDB API collection</span></span>
<span data-ttu-id="efa58-241">L’option de l’importateur source Azure Cosmos DB vous permet d’importer des données à partir d’une ou de plusieurs collections Azure Cosmos DB et de filtrer éventuellement des documents à l’aide d’une requête.</span><span class="sxs-lookup"><span data-stu-id="efa58-241">The Azure Cosmos DB source importer option allows you to import data from one or more Azure Cosmos DB collections and optionally filter documents using a query.</span></span>  

![Capture d’écran des options sources d’Azure Cosmos DB](./media/import-data/documentdbsource.png)

<span data-ttu-id="efa58-243">Le format de la chaîne de connexion Azure Cosmos DB est :</span><span class="sxs-lookup"><span data-stu-id="efa58-243">The format of the Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="efa58-244">La chaîne de connexion d’un compte Azure Cosmos DB peut être récupérée à partir du panneau Clés du portail Azure, comme décrit dans [How to manage an Azure Cosmos DB account](manage-account.md) (Gestion d’un compte Azure Cosmos DB), mais le nom de la base de données doit être ajouté à la chaîne de connexion au format suivant :</span><span class="sxs-lookup"><span data-stu-id="efa58-244">The Azure Cosmos DB account connection string can be retrieved from the Keys blade of the Azure portal, as described in [How to manage an Azure Cosmos DB account](manage-account.md), however the name of the database needs to be appended to the connection string in the following format:</span></span>

    Database=<CosmosDB Database>;

> [!NOTE]
> <span data-ttu-id="efa58-245">Utilisez la commande Verify pour vous assurer que l’instance Azure Cosmos DB spécifiée dans le champ de la chaîne de connexion est accessible.</span><span class="sxs-lookup"><span data-stu-id="efa58-245">Use the Verify command to ensure that the Azure Cosmos DB instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="efa58-246">Pour importer à partir d’une seule collection Azure Cosmos DB, entrez le nom de la collection à partir de laquelle les données seront importées.</span><span class="sxs-lookup"><span data-stu-id="efa58-246">To import from a single Azure Cosmos DB collection, enter the name of the collection from which data will be imported.</span></span> <span data-ttu-id="efa58-247">Pour importer à partir de plusieurs collections Azure Cosmos DB, fournissez une expression régulière correspondant à un ou plusieurs noms de collection (par exemple, collection01 | collection02 | collection03).</span><span class="sxs-lookup"><span data-stu-id="efa58-247">To import from multiple Azure Cosmos DB collections, provide a regular expression to match one or more collection names (e.g. collection01 | collection02 | collection03).</span></span> <span data-ttu-id="efa58-248">Vous pouvez éventuellement spécifier ou fournir un fichier pour une requête pour filtrer et mettre en forme les données à importer.</span><span class="sxs-lookup"><span data-stu-id="efa58-248">You may optionally specify, or provide a file for, a query to both filter and shape the data to be imported.</span></span>

> [!NOTE]
> <span data-ttu-id="efa58-249">Étant donné que le champ de collection accepte les expressions régulières, si vous importez à partir d'une collection unique dont le nom contient des caractères d'expression régulière, ces caractères doivent être placés en conséquence dans une séquence d'échappement.</span><span class="sxs-lookup"><span data-stu-id="efa58-249">Since the collection field accepts regular expressions, if you are importing from a single collection whose name contains regular expression characters, then those characters must be escaped accordingly.</span></span>
> 
> 

<span data-ttu-id="efa58-250">L’option d’importateur source Azure Cosmos DB dispose des options avancées suivantes :</span><span class="sxs-lookup"><span data-stu-id="efa58-250">The Azure Cosmos DB source importer option has the following advanced options:</span></span>

1. <span data-ttu-id="efa58-251">Inclusion des champs internes : cette option précise les propriétés système du document Azure Cosmos DB à inclure ou non dans l’exportation (par exemple, _rid, _ts).</span><span class="sxs-lookup"><span data-stu-id="efa58-251">Include Internal Fields: Specifies whether or not to include Azure Cosmos DB document system properties in the export (e.g. _rid, _ts).</span></span>
2. <span data-ttu-id="efa58-252">Nombre de nouvelles tentatives en cas de défaillance : cette option précise le nombre de nouvelles tentatives de connexion à Azure Cosmos DB en cas de défaillances temporaires (par exemple, une interruption de connectivité du réseau).</span><span class="sxs-lookup"><span data-stu-id="efa58-252">Number of Retries on Failure: Specifies the number of times to retry the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
3. <span data-ttu-id="efa58-253">Intervalle avant nouvelle tentative : cette option indique le temps à attendre entre les nouvelles tentatives de connexion à Azure Cosmos DB en cas de défaillances temporaires (par exemple, une interruption de la connectivité du réseau).</span><span class="sxs-lookup"><span data-stu-id="efa58-253">Retry Interval: Specifies how long to wait between retrying the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
4. <span data-ttu-id="efa58-254">Mode de connexion : cette option indique le mode de connexion à utiliser avec Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="efa58-254">Connection Mode: Specifies the connection mode to use with Azure Cosmos DB.</span></span> <span data-ttu-id="efa58-255">Les choix disponibles sont DirectTcp, DirectHttps et la passerelle.</span><span class="sxs-lookup"><span data-stu-id="efa58-255">The available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="efa58-256">Les modes de connexion directs sont plus rapides, tandis que le mode passerelle est mieux adapté au pare-feu car il utilise uniquement le port 443.</span><span class="sxs-lookup"><span data-stu-id="efa58-256">The direct connection modes are faster, while the gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Capture d’écran des options sources avancées d’Azure Cosmos DB](./media/import-data/documentdbsourceoptions.png)

> [!TIP]
> <span data-ttu-id="efa58-258">L’outil d’importation utilise le mode de connexion DirectTcp par défaut.</span><span class="sxs-lookup"><span data-stu-id="efa58-258">The import tool defaults to connection mode DirectTcp.</span></span> <span data-ttu-id="efa58-259">Si vous rencontrez des problèmes liés au pare-feu, passer au mode de connexion passerelle qui ne nécessite que le port 443.</span><span class="sxs-lookup"><span data-stu-id="efa58-259">If you experience firewall issues, switch to connection mode Gateway, as it only requires port 443.</span></span>
> 
> 

<span data-ttu-id="efa58-260">Voici quelques exemples de lignes de commande pour l’importation depuis Azure Cosmos DB :</span><span class="sxs-lookup"><span data-stu-id="efa58-260">Here are some command line samples to import from Azure Cosmos DB:</span></span>

    #Migrate data from one Azure Cosmos DB collection to another Azure Cosmos DB collections
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:TEColl /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:TESessions /t.CollectionThroughput:2500

    #Migrate data from multiple Azure Cosmos DB collections to a single Azure Cosmos DB collection
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:comp1|comp2|comp3|comp4 /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:singleCollection /t.CollectionThroughput:2500

    #Export an Azure Cosmos DB collection to a JSON file
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:StoresSub /t:JsonFile /t.File:StoresExport.json /t.Overwrite /t.CollectionThroughput:2500

> [!TIP]
> <span data-ttu-id="efa58-261">L’outil d’importation de données Azure Cosmos DB prend également en charge l’importation de données à partir de [l’émulateur Azure Cosmos DB](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="efa58-261">The Azure Cosmos DB Data Import Tool also supports import of data from the [Azure Cosmos DB Emulator](local-emulator.md).</span></span> <span data-ttu-id="efa58-262">Quand vous importez des données à partir d’un émulateur local, affectez `https://localhost:<port>` comme point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="efa58-262">When importing data from a local emulator, set the endpoint to `https://localhost:<port>`.</span></span> 
> 
> 

## <span data-ttu-id="efa58-263"><a id="HBaseSource"></a>Importation à partir de HBase</span><span class="sxs-lookup"><span data-stu-id="efa58-263"><a id="HBaseSource"></a>To import from HBase</span></span>
<span data-ttu-id="efa58-264">L’option d’importateur source HBase vous permet d’importer des données à partir d'une table HBase et de filtrer éventuellement les données.</span><span class="sxs-lookup"><span data-stu-id="efa58-264">The HBase source importer option allows you to import data from an HBase table and optionally filter the data.</span></span> <span data-ttu-id="efa58-265">Plusieurs modèles sont fournis pour faciliter au maximum la configuration d'une importation.</span><span class="sxs-lookup"><span data-stu-id="efa58-265">Several templates are provided so that setting up an import is as easy as possible.</span></span>

![Capture d’écran des options sources HBase](./media/import-data/hbasesource1.png)

![Capture d’écran des options sources HBase](./media/import-data/hbasesource2.png)

<span data-ttu-id="efa58-268">Le format de la chaîne de connexion HBase Stargate est :</span><span class="sxs-lookup"><span data-stu-id="efa58-268">The format of the HBase Stargate connection string is:</span></span>

    ServiceURL=<server-address>;Username=<username>;Password=<password>

> [!NOTE]
> <span data-ttu-id="efa58-269">Utilisez la commande Verify pour vous assurer que l'instance HBase spécifiée dans le champ de la chaîne de connexion est accessible.</span><span class="sxs-lookup"><span data-stu-id="efa58-269">Use the Verify command to ensure that the HBase instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="efa58-270">Voici un exemple de ligne de commande pour importer à partir de HBase :</span><span class="sxs-lookup"><span data-stu-id="efa58-270">Here is a command line sample to import from HBase:</span></span>

    dt.exe /s:HBase /s.ConnectionString:ServiceURL=<server-address>;Username=<username>;Password=<password> /s.Table:Contacts /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:hbaseimport

## <span data-ttu-id="efa58-271"><a id="DocumentDBBulkTarget"></a>Importation vers l’API DocumentDB (importation en bloc)</span><span class="sxs-lookup"><span data-stu-id="efa58-271"><a id="DocumentDBBulkTarget"></a>To import to the DocumentDB API (Bulk Import)</span></span>
<span data-ttu-id="efa58-272">L’importateur en bloc Azure Cosmos DB vous permet d’importer à partir des options sources disponibles, à l’aide d’une procédure Azure Cosmos DB stockée pour plus d’efficacité.</span><span class="sxs-lookup"><span data-stu-id="efa58-272">The Azure Cosmos DB Bulk importer allows you to import from any of the available source options, using an Azure Cosmos DB stored procedure for efficiency.</span></span> <span data-ttu-id="efa58-273">L’outil prend en charge l’importation dans une seule collection Azure Cosmos DB à partition unique, ainsi que l’importation partitionnée pour laquelle les données sont partitionnées sur plusieurs collections Azure Cosmos DB à partition unique.</span><span class="sxs-lookup"><span data-stu-id="efa58-273">The tool supports import to one single-partitioned Azure Cosmos DB collection, as well as sharded import whereby data is partitioned across multiple single-partitioned Azure Cosmos DB collections.</span></span> <span data-ttu-id="efa58-274">Pour plus d’informations sur le partitionnement de données, consultez [Partitionnement et mise à l’échelle dans Azure Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="efa58-274">For more information about partitioning data, see [Partitioning and scaling in Azure Cosmos DB](partition-data.md).</span></span> <span data-ttu-id="efa58-275">L'outil va créer, exécuter, puis supprimer la procédure stockée de la ou les collections cibles.</span><span class="sxs-lookup"><span data-stu-id="efa58-275">The tool will create, execute, and then delete the stored procedure from the target collection(s).</span></span>  

![Capture d’écran des options de bloc d’Azure Cosmos DB](./media/import-data/documentdbbulk.png)

<span data-ttu-id="efa58-277">Le format de la chaîne de connexion Azure Cosmos DB est :</span><span class="sxs-lookup"><span data-stu-id="efa58-277">The format of the Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="efa58-278">La chaîne de connexion d’un compte Azure Cosmos DB peut être récupérée à partir du panneau Clés du portail Azure, comme décrit dans [How to manage an Azure Cosmos DB account](manage-account.md) (Gestion d’un compte Azure Cosmos DB), mais le nom de la base de données doit être ajouté à la chaîne de connexion au format suivant :</span><span class="sxs-lookup"><span data-stu-id="efa58-278">The Azure Cosmos DB account connection string can be retrieved from the Keys blade of the Azure portal, as described in [How to manage an Azure Cosmos DB account](manage-account.md), however the name of the database needs to be appended to the connection string in the following format:</span></span>

    Database=<CosmosDB Database>;

> [!NOTE]
> <span data-ttu-id="efa58-279">Utilisez la commande Verify pour vous assurer que l’instance Azure Cosmos DB spécifiée dans le champ de la chaîne de connexion est accessible.</span><span class="sxs-lookup"><span data-stu-id="efa58-279">Use the Verify command to ensure that the Azure Cosmos DB instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="efa58-280">Pour importer dans seule collection, entrez le nom de la collection dans laquelle les données seront importées et cliquez sur le bouton Ajouter.</span><span class="sxs-lookup"><span data-stu-id="efa58-280">To import to a single collection, enter the name of the collection to which data will be imported and click the Add button.</span></span> <span data-ttu-id="efa58-281">Pour importer dans plusieurs collections, entrez le nom de chaque collection individuellement ou utilisez la syntaxe suivante pour spécifier plusieurs collections : *préfixe_collection*[index de début - index de fin].</span><span class="sxs-lookup"><span data-stu-id="efa58-281">To import to multiple collections, either enter each collection name individually or use the following syntax to specify multiple collections: *collection_prefix*[start index - end index].</span></span> <span data-ttu-id="efa58-282">Quand vous spécifiez plusieurs collections via la syntaxe ci-dessus, n'oubliez pas les points suivants :</span><span class="sxs-lookup"><span data-stu-id="efa58-282">When specifying multiple collections via the aforementioned syntax, keep the following in mind:</span></span>

1. <span data-ttu-id="efa58-283">Seuls les modèles de nom de plage de nombres entiers sont pris en charge.</span><span class="sxs-lookup"><span data-stu-id="efa58-283">Only integer range name patterns are supported.</span></span> <span data-ttu-id="efa58-284">Par exemple, la spécification de collection[0-3] produit les collections suivantes : collection0, collection1, collection2, collection3.</span><span class="sxs-lookup"><span data-stu-id="efa58-284">For example, specifying collection[0-3] will produce the following collections: collection0, collection1, collection2, collection3.</span></span>
2. <span data-ttu-id="efa58-285">Vous pouvez utiliser une syntaxe abrégée : collection[3], qui émet le même jeu de collections que celui mentionné à l'étape 1.</span><span class="sxs-lookup"><span data-stu-id="efa58-285">You can use an abbreviated syntax: collection[3] will emit same set of collections mentioned in step 1.</span></span>
3. <span data-ttu-id="efa58-286">Plusieurs substitutions peuvent être fournies.</span><span class="sxs-lookup"><span data-stu-id="efa58-286">More than one substitution can be provided.</span></span> <span data-ttu-id="efa58-287">Par exemple, collection[0-1] [0-9] génère 20 noms de collection avec des zéros non significatifs (collection01, ..02, ..03).</span><span class="sxs-lookup"><span data-stu-id="efa58-287">For example, collection[0-1] [0-9] will generate 20 collection names with leading zeros (collection01, ..02, ..03).</span></span>

<span data-ttu-id="efa58-288">Une fois que les noms de la collection ont été spécifiés, choisissez le débit souhaité des collections (entre 400 RU et 10 000 RU).</span><span class="sxs-lookup"><span data-stu-id="efa58-288">Once the collection name(s) have been specified, choose the desired throughput of the collection(s) (400 RUs to 10,000 RUs).</span></span> <span data-ttu-id="efa58-289">Pour de meilleures performances d’importation, choisissez un débit plus élevé.</span><span class="sxs-lookup"><span data-stu-id="efa58-289">For best import performance, choose a higher throughput.</span></span> <span data-ttu-id="efa58-290">Pour plus d’informations sur les niveaux de performances, consultez les [niveaux de performances d’Azure Cosmos DB](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="efa58-290">For more information about performance levels, see [Performance levels in Azure Cosmos DB](performance-levels.md).</span></span>

> [!NOTE]
> <span data-ttu-id="efa58-291">Le paramètre de débit de performance s’applique uniquement à la création de collections.</span><span class="sxs-lookup"><span data-stu-id="efa58-291">The performance throughput setting only applies to collection creation.</span></span> <span data-ttu-id="efa58-292">Si la collection spécifiée existe déjà, son débit ne sera pas modifié.</span><span class="sxs-lookup"><span data-stu-id="efa58-292">If the specified collection already exists, its throughput will not be modified.</span></span>
> 
> 

<span data-ttu-id="efa58-293">Pendant l'importation de plusieurs collections, l'outil d'importation prend en charge le partitionnement basé sur le hachage.</span><span class="sxs-lookup"><span data-stu-id="efa58-293">When importing to multiple collections, the import tool supports hash based sharding.</span></span> <span data-ttu-id="efa58-294">Dans ce scénario, spécifiez la propriété de document que vous voulez utiliser comme clé de partition (si la clé de partition est vide, les documents seront partitionnés de manière aléatoire entre les collections cibles).</span><span class="sxs-lookup"><span data-stu-id="efa58-294">In this scenario, specify the document property you wish to use as the Partition Key (if Partition Key is left blank, documents will be sharded randomly across the target collections).</span></span>

<span data-ttu-id="efa58-295">Vous pouvez éventuellement spécifier quel champ de la source d’importation doit être utilisé en tant que propriété d’ID du document Azure Cosmos DB lors de l’importation (Notez que si les documents ne contiennent pas cette propriété, l’outil d’importation génère alors un GUID comme valeur de propriété de l’ID).</span><span class="sxs-lookup"><span data-stu-id="efa58-295">You may optionally specify which field in the import source should be used as the Azure Cosmos DB document id property during the import (note that if documents do not contain this property, then the import tool will generate a GUID as the id property value).</span></span>

<span data-ttu-id="efa58-296">De nombreuses options avancées sont disponibles lors de l'importation.</span><span class="sxs-lookup"><span data-stu-id="efa58-296">There are a number of advanced options available during import.</span></span> <span data-ttu-id="efa58-297">Tout d'abord, tandis que l'outil inclut une procédure stockée d’importation en bloc par défaut (BulkInsert.js), vous pouvez choisir d’indiquer votre propre procédure stockée d'importation :</span><span class="sxs-lookup"><span data-stu-id="efa58-297">First, while the tool includes a default bulk import stored procedure (BulkInsert.js), you may choose to specify your own import stored procedure:</span></span>

 ![Capture d’écran de l’option sproc d’insertion de bloc Azure Cosmos DB](./media/import-data/bulkinsertsp.png)

<span data-ttu-id="efa58-299">De plus, lorsque vous importez des types de date (par exemple, depuis SQL Server ou MongoDB), vous pouvez choisir entre trois options d'importation :</span><span class="sxs-lookup"><span data-stu-id="efa58-299">Additionally, when importing date types (e.g. from SQL Server or MongoDB), you can choose between three import options:</span></span>

 ![Capture d’écran des options d’importation de date et d’heure Azure Cosmos DB](./media/import-data/datetimeoptions.png)

* <span data-ttu-id="efa58-301">Chaîne : conserver en tant que valeur de chaîne</span><span class="sxs-lookup"><span data-stu-id="efa58-301">String: Persist as a string value</span></span>
* <span data-ttu-id="efa58-302">Epoch : conserver en tant que valeur numérique Epoch</span><span class="sxs-lookup"><span data-stu-id="efa58-302">Epoch: Persist as an Epoch number value</span></span>
* <span data-ttu-id="efa58-303">Les deux : conserver la chaîne et les valeurs numériques Epoch</span><span class="sxs-lookup"><span data-stu-id="efa58-303">Both: Persist both string and Epoch number values.</span></span> <span data-ttu-id="efa58-304">Cette option crée un sous-document, par exemple : « date_joined » : {« Valeur »: « 2013-10-21T21:17:25.2410000Z », « Epoch » : 1382390245}</span><span class="sxs-lookup"><span data-stu-id="efa58-304">This option will create a subdocument, for example: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span></span>

<span data-ttu-id="efa58-305">L’importateur en bloc Azure Cosmos DB dispose des options avancées supplémentaires suivantes :</span><span class="sxs-lookup"><span data-stu-id="efa58-305">The Azure Cosmos DB Bulk importer has the following additional advanced options:</span></span>

1. <span data-ttu-id="efa58-306">Taille du lot : l'outil par défaut avec une taille de lot de 50.</span><span class="sxs-lookup"><span data-stu-id="efa58-306">Batch Size: The tool defaults to a batch size of 50.</span></span>  <span data-ttu-id="efa58-307">Si les documents qui doivent être importés sont volumineux, pensez à réduire la taille du lot.</span><span class="sxs-lookup"><span data-stu-id="efa58-307">If the documents to be imported are large, consider lowering the batch size.</span></span> <span data-ttu-id="efa58-308">À l’inverse, si les documents qui doivent être importés sont peu volumineux, pensez à augmenter la taille du lot.</span><span class="sxs-lookup"><span data-stu-id="efa58-308">Conversely, if the documents to be imported are small, consider raising the batch size.</span></span>
2. <span data-ttu-id="efa58-309">Taille de script maximale (octets) : l'outil par défaut avec une taille de script maximale de 512 ko</span><span class="sxs-lookup"><span data-stu-id="efa58-309">Max Script Size (bytes): The tool defaults to a max script size of 512KB</span></span>
3. <span data-ttu-id="efa58-310">Désactivation de la génération automatique d’ID : si tous les documents à importer contiennent un champ d'ID, la sélection de cette option permettra d’en augmenter les performances.</span><span class="sxs-lookup"><span data-stu-id="efa58-310">Disable Automatic Id Generation: If every document to be imported contains an id field, then selecting this option can increase performance.</span></span> <span data-ttu-id="efa58-311">Les documents avec un champ d’ID unique manquant ne seront pas importés.</span><span class="sxs-lookup"><span data-stu-id="efa58-311">Documents missing a unique id field will not be imported.</span></span>
4. <span data-ttu-id="efa58-312">Mise à jour des documents existants : par défaut, l’outil ne replace pas les documents existants présentant des conflits d'ID.</span><span class="sxs-lookup"><span data-stu-id="efa58-312">Update Existing Documents: The tool defaults to not replacing existing documents with id conflicts.</span></span> <span data-ttu-id="efa58-313">Cette option permettra de remplacer les documents existants par les ID correspondants.</span><span class="sxs-lookup"><span data-stu-id="efa58-313">Selecting this option will allow overwriting existing documents with matching ids.</span></span> <span data-ttu-id="efa58-314">Cette fonctionnalité est utile pour les migrations de données planifiées qui mettent à jour des documents existants.</span><span class="sxs-lookup"><span data-stu-id="efa58-314">This feature is useful for scheduled data migrations that update existing documents.</span></span>
5. <span data-ttu-id="efa58-315">Nombre de nouvelles tentatives en cas de défaillance : cette option précise le nombre de nouvelles tentatives de connexion à Azure Cosmos DB en cas de défaillances temporaires (par exemple, une interruption de connectivité du réseau).</span><span class="sxs-lookup"><span data-stu-id="efa58-315">Number of Retries on Failure: Specifies the number of times to retry the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
6. <span data-ttu-id="efa58-316">Intervalle avant nouvelle tentative : cette option indique le temps à attendre entre les nouvelles tentatives de connexion à Azure Cosmos DB en cas de défaillances temporaires (par exemple, une interruption de la connectivité du réseau).</span><span class="sxs-lookup"><span data-stu-id="efa58-316">Retry Interval: Specifies how long to wait between retrying the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
7. <span data-ttu-id="efa58-317">Mode de connexion : cette option indique le mode de connexion à utiliser avec Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="efa58-317">Connection Mode: Specifies the connection mode to use with Azure Cosmos DB.</span></span> <span data-ttu-id="efa58-318">Les choix disponibles sont DirectTcp, DirectHttps et la passerelle.</span><span class="sxs-lookup"><span data-stu-id="efa58-318">The available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="efa58-319">Les modes de connexion directs sont plus rapides, tandis que le mode passerelle est mieux adapté au pare-feu car il utilise uniquement le port 443.</span><span class="sxs-lookup"><span data-stu-id="efa58-319">The direct connection modes are faster, while the gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Capture d’écran des options d’importation en bloc avancées d’Azure Cosmos DB](./media/import-data/docdbbulkoptions.png)

> [!TIP]
> <span data-ttu-id="efa58-321">L’outil d’importation utilise le mode de connexion DirectTcp par défaut.</span><span class="sxs-lookup"><span data-stu-id="efa58-321">The import tool defaults to connection mode DirectTcp.</span></span> <span data-ttu-id="efa58-322">Si vous rencontrez des problèmes liés au pare-feu, passer au mode de connexion passerelle qui ne nécessite que le port 443.</span><span class="sxs-lookup"><span data-stu-id="efa58-322">If you experience firewall issues, switch to connection mode Gateway, as it only requires port 443.</span></span>
> 
> 

## <span data-ttu-id="efa58-323"><a id="DocumentDBSeqTarget"></a>Importation vers l’API DocumentDB (importation d’enregistrement séquentiel)</span><span class="sxs-lookup"><span data-stu-id="efa58-323"><a id="DocumentDBSeqTarget"></a>To import to the DocumentDB API (Sequential Record Import)</span></span>
<span data-ttu-id="efa58-324">L’importateur d’enregistrement séquentiel Azure Cosmos DB vous permet d’importer à partir de n’importe quelle option source disponible sur un enregistrement en fonction des enregistrements.</span><span class="sxs-lookup"><span data-stu-id="efa58-324">The Azure Cosmos DB sequential record importer allows you to import from any of the available source options on a record by record basis.</span></span> <span data-ttu-id="efa58-325">Vous pouvez choisir cette option si vous importez vers une collection existante ayant atteint son quota de procédures stockées.</span><span class="sxs-lookup"><span data-stu-id="efa58-325">You might choose this option if you’re importing to an existing collection that has reached its quota of stored procedures.</span></span> <span data-ttu-id="efa58-326">L’outil prend en charge l’importation dans une seule collection Azure Cosmos DB (à partition unique et à plusieurs partitions), ainsi que l’importation partitionnée pour laquelle les données sont partitionnées sur plusieurs collections Azure Cosmos DB à partition unique et/ou à plusieurs partitions.</span><span class="sxs-lookup"><span data-stu-id="efa58-326">The tool supports import to a single (both single-partition and multi-partition) Azure Cosmos DB collection, as well as sharded import whereby data is partitioned across multiple single-partition and/or multi-partition Azure Cosmos DB collections.</span></span> <span data-ttu-id="efa58-327">Pour plus d’informations sur le partitionnement de données, consultez [Partitionnement et mise à l’échelle dans Azure Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="efa58-327">For more information about partitioning data, see [Partitioning and scaling in Azure Cosmos DB](partition-data.md).</span></span>

![Capture d’écran des options d’importation d’enregistrement séquentiel d’Azure Cosmos DB](./media/import-data/documentdbsequential.png)

<span data-ttu-id="efa58-329">Le format de la chaîne de connexion Azure Cosmos DB est :</span><span class="sxs-lookup"><span data-stu-id="efa58-329">The format of the Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="efa58-330">La chaîne de connexion d’un compte Azure Cosmos DB peut être récupérée à partir du panneau Clés du portail Azure, comme décrit dans [How to manage an Azure Cosmos DB account](manage-account.md) (Gestion d’un compte Azure Cosmos DB), mais le nom de la base de données doit être ajouté à la chaîne de connexion au format suivant :</span><span class="sxs-lookup"><span data-stu-id="efa58-330">The Azure Cosmos DB account connection string can be retrieved from the Keys blade of the Azure portal, as described in [How to manage an Azure Cosmos DB account](manage-account.md), however the name of the database needs to be appended to the connection string in the following format:</span></span>

    Database=<Azure Cosmos DB Database>;

> [!NOTE]
> <span data-ttu-id="efa58-331">Utilisez la commande Verify pour vous assurer que l’instance Azure Cosmos DB spécifiée dans le champ de la chaîne de connexion est accessible.</span><span class="sxs-lookup"><span data-stu-id="efa58-331">Use the Verify command to ensure that the Azure Cosmos DB instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="efa58-332">Pour importer dans seule collection, entrez le nom de la collection dans laquelle les données seront importées et cliquez sur le bouton Ajouter.</span><span class="sxs-lookup"><span data-stu-id="efa58-332">To import to a single collection, enter the name of the collection to which data will be imported and click the Add button.</span></span> <span data-ttu-id="efa58-333">Pour importer dans plusieurs collections, entrez le nom de chaque collection individuellement ou utilisez la syntaxe suivante pour spécifier plusieurs collections : *préfixe_collection*[index de début - index de fin].</span><span class="sxs-lookup"><span data-stu-id="efa58-333">To import to multiple collections, either enter each collection name individually or use the following syntax to specify multiple collections: *collection_prefix*[start index - end index].</span></span> <span data-ttu-id="efa58-334">Quand vous spécifiez plusieurs collections via la syntaxe ci-dessus, n'oubliez pas les points suivants :</span><span class="sxs-lookup"><span data-stu-id="efa58-334">When specifying multiple collections via the aforementioned syntax, keep the following in mind:</span></span>

1. <span data-ttu-id="efa58-335">Seuls les modèles de nom de plage de nombres entiers sont pris en charge.</span><span class="sxs-lookup"><span data-stu-id="efa58-335">Only integer range name patterns are supported.</span></span> <span data-ttu-id="efa58-336">Par exemple, la spécification de collection[0-3] produit les collections suivantes : collection0, collection1, collection2, collection3.</span><span class="sxs-lookup"><span data-stu-id="efa58-336">For example, specifying collection[0-3] will produce the following collections: collection0, collection1, collection2, collection3.</span></span>
2. <span data-ttu-id="efa58-337">Vous pouvez utiliser une syntaxe abrégée : collection[3], qui émet le même jeu de collections que celui mentionné à l'étape 1.</span><span class="sxs-lookup"><span data-stu-id="efa58-337">You can use an abbreviated syntax: collection[3] will emit same set of collections mentioned in step 1.</span></span>
3. <span data-ttu-id="efa58-338">Plusieurs substitutions peuvent être fournies.</span><span class="sxs-lookup"><span data-stu-id="efa58-338">More than one substitution can be provided.</span></span> <span data-ttu-id="efa58-339">Par exemple, collection[0-1] [0-9] génère 20 noms de collection avec des zéros non significatifs (collection01, ..02, ..03).</span><span class="sxs-lookup"><span data-stu-id="efa58-339">For example, collection[0-1] [0-9] will generate 20 collection names with leading zeros (collection01, ..02, ..03).</span></span>

<span data-ttu-id="efa58-340">Une fois que les noms de la collection ont été spécifiés, choisissez le débit souhaité des collections (entre 400 RU et 250 000 RU).</span><span class="sxs-lookup"><span data-stu-id="efa58-340">Once the collection name(s) have been specified, choose the desired throughput of the collection(s) (400 RUs to 250,000 RUs).</span></span> <span data-ttu-id="efa58-341">Pour de meilleures performances d’importation, choisissez un débit plus élevé.</span><span class="sxs-lookup"><span data-stu-id="efa58-341">For best import performance, choose a higher throughput.</span></span> <span data-ttu-id="efa58-342">Pour plus d’informations sur les niveaux de performances, consultez les [niveaux de performances d’Azure Cosmos DB](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="efa58-342">For more information about performance levels, see [Performance levels in Azure Cosmos DB](performance-levels.md).</span></span> <span data-ttu-id="efa58-343">Les importations dans des collections avec un débit > 10 000 RU nécessitent une clé de partition.</span><span class="sxs-lookup"><span data-stu-id="efa58-343">Any import to collections with throughput >10,000 RUs will require a partition key.</span></span> <span data-ttu-id="efa58-344">Si vous choisissez d’avoir plus de 250 000 RU, vous devrez envoyer une demande d’augmentation de votre compte dans le portail.</span><span class="sxs-lookup"><span data-stu-id="efa58-344">If you choose to have more than 250,000 RUs, you will need to file a request in the portal to have your account increased.</span></span>

> [!NOTE]
> <span data-ttu-id="efa58-345">Le paramètre de débit s’applique uniquement à la création de collections.</span><span class="sxs-lookup"><span data-stu-id="efa58-345">The throughput setting only applies to collection creation.</span></span> <span data-ttu-id="efa58-346">Si la collection spécifiée existe déjà, son débit ne sera pas modifié.</span><span class="sxs-lookup"><span data-stu-id="efa58-346">If the specified collection already exists, its throughput will not be modified.</span></span>
> 
> 

<span data-ttu-id="efa58-347">Pendant l'importation de plusieurs collections, l'outil d'importation prend en charge le partitionnement basé sur le hachage.</span><span class="sxs-lookup"><span data-stu-id="efa58-347">When importing to multiple collections, the import tool supports hash based sharding.</span></span> <span data-ttu-id="efa58-348">Dans ce scénario, spécifiez la propriété de document que vous voulez utiliser comme clé de partition (si la clé de partition est vide, les documents seront partitionnés de manière aléatoire entre les collections cibles).</span><span class="sxs-lookup"><span data-stu-id="efa58-348">In this scenario, specify the document property you wish to use as the Partition Key (if Partition Key is left blank, documents will be sharded randomly across the target collections).</span></span>

<span data-ttu-id="efa58-349">Vous pouvez éventuellement spécifier quel champ de la source d’importation doit être utilisé en tant que propriété d’ID du document Azure Cosmos DB lors de l’importation (Notez que si les documents ne contiennent pas cette propriété, l’outil d’importation génère alors un GUID comme valeur de propriété de l’ID).</span><span class="sxs-lookup"><span data-stu-id="efa58-349">You may optionally specify which field in the import source should be used as the Azure Cosmos DB document id property during the import (note that if documents do not contain this property, then the import tool will generate a GUID as the id property value).</span></span>

<span data-ttu-id="efa58-350">De nombreuses options avancées sont disponibles lors de l'importation.</span><span class="sxs-lookup"><span data-stu-id="efa58-350">There are a number of advanced options available during import.</span></span> <span data-ttu-id="efa58-351">Tout d’abord, lorsque vous importez des types de date (par exemple, depuis SQL Server ou MongoDB), vous pouvez choisir entre trois options d'importation :</span><span class="sxs-lookup"><span data-stu-id="efa58-351">First, when importing date types (e.g. from SQL Server or MongoDB), you can choose between three import options:</span></span>

 ![Capture d’écran des options d’importation de date et d’heure Azure Cosmos DB](./media/import-data/datetimeoptions.png)

* <span data-ttu-id="efa58-353">Chaîne : conserver en tant que valeur de chaîne</span><span class="sxs-lookup"><span data-stu-id="efa58-353">String: Persist as a string value</span></span>
* <span data-ttu-id="efa58-354">Epoch : conserver en tant que valeur numérique Epoch</span><span class="sxs-lookup"><span data-stu-id="efa58-354">Epoch: Persist as an Epoch number value</span></span>
* <span data-ttu-id="efa58-355">Les deux : conserver la chaîne et les valeurs numériques Epoch</span><span class="sxs-lookup"><span data-stu-id="efa58-355">Both: Persist both string and Epoch number values.</span></span> <span data-ttu-id="efa58-356">Cette option crée un sous-document, par exemple : « date_joined » : {« Valeur »: « 2013-10-21T21:17:25.2410000Z », « Epoch » : 1382390245}</span><span class="sxs-lookup"><span data-stu-id="efa58-356">This option will create a subdocument, for example: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span></span>

<span data-ttu-id="efa58-357">L’importateur d’enregistrement séquentiel Azure Cosmos DB dispose des options avancées supplémentaires suivantes :</span><span class="sxs-lookup"><span data-stu-id="efa58-357">The Azure Cosmos DB - Sequential record importer has the following additional advanced options:</span></span>

1. <span data-ttu-id="efa58-358">Nombre de demandes parallèles : l'outil par défaut avec 2 demandes parallèles.</span><span class="sxs-lookup"><span data-stu-id="efa58-358">Number of Parallel Requests: The tool defaults to 2 parallel requests.</span></span> <span data-ttu-id="efa58-359">Si les documents qui doivent être importés sont peu volumineux, pensez à augmenter le nombre de demandes parallèles.</span><span class="sxs-lookup"><span data-stu-id="efa58-359">If the documents to be imported are small, consider raising the number of parallel requests.</span></span> <span data-ttu-id="efa58-360">Notez que si ce nombre est trop élevé, l'importation peut rencontrer une limitation.</span><span class="sxs-lookup"><span data-stu-id="efa58-360">Note that if this number is raised too much, the import may experience throttling.</span></span>
2. <span data-ttu-id="efa58-361">Désactivation de la génération automatique d’ID : si tous les documents à importer contiennent un champ d'ID, la sélection de cette option permettra d’en augmenter les performances.</span><span class="sxs-lookup"><span data-stu-id="efa58-361">Disable Automatic Id Generation: If every document to be imported contains an id field, then selecting this option can increase performance.</span></span> <span data-ttu-id="efa58-362">Les documents avec un champ d’ID unique manquant ne seront pas importés.</span><span class="sxs-lookup"><span data-stu-id="efa58-362">Documents missing a unique id field will not be imported.</span></span>
3. <span data-ttu-id="efa58-363">Mise à jour des documents existants : par défaut, l’outil ne replace pas les documents existants présentant des conflits d'ID.</span><span class="sxs-lookup"><span data-stu-id="efa58-363">Update Existing Documents: The tool defaults to not replacing existing documents with id conflicts.</span></span> <span data-ttu-id="efa58-364">Cette option permettra de remplacer les documents existants par les ID correspondants.</span><span class="sxs-lookup"><span data-stu-id="efa58-364">Selecting this option will allow overwriting existing documents with matching ids.</span></span> <span data-ttu-id="efa58-365">Cette fonctionnalité est utile pour les migrations de données planifiées qui mettent à jour des documents existants.</span><span class="sxs-lookup"><span data-stu-id="efa58-365">This feature is useful for scheduled data migrations that update existing documents.</span></span>
4. <span data-ttu-id="efa58-366">Nombre de nouvelles tentatives en cas de défaillance : cette option précise le nombre de nouvelles tentatives de connexion à Azure Cosmos DB en cas de défaillances temporaires (par exemple, une interruption de connectivité du réseau).</span><span class="sxs-lookup"><span data-stu-id="efa58-366">Number of Retries on Failure: Specifies the number of times to retry the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
5. <span data-ttu-id="efa58-367">Intervalle avant nouvelle tentative : cette option indique le temps à attendre entre les nouvelles tentatives de connexion à Azure Cosmos DB en cas de défaillances temporaires (par exemple, une interruption de la connectivité du réseau).</span><span class="sxs-lookup"><span data-stu-id="efa58-367">Retry Interval: Specifies how long to wait between retrying the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
6. <span data-ttu-id="efa58-368">Mode de connexion : cette option indique le mode de connexion à utiliser avec Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="efa58-368">Connection Mode: Specifies the connection mode to use with Azure Cosmos DB.</span></span> <span data-ttu-id="efa58-369">Les choix disponibles sont DirectTcp, DirectHttps et la passerelle.</span><span class="sxs-lookup"><span data-stu-id="efa58-369">The available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="efa58-370">Les modes de connexion directs sont plus rapides, tandis que le mode passerelle est mieux adapté au pare-feu car il utilise uniquement le port 443.</span><span class="sxs-lookup"><span data-stu-id="efa58-370">The direct connection modes are faster, while the gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Capture d’écran des options d’importation d’enregistrement séquentiel avancées d’Azure Cosmos DB](./media/import-data/documentdbsequentialoptions.png)

> [!TIP]
> <span data-ttu-id="efa58-372">L’outil d’importation utilise le mode de connexion DirectTcp par défaut.</span><span class="sxs-lookup"><span data-stu-id="efa58-372">The import tool defaults to connection mode DirectTcp.</span></span> <span data-ttu-id="efa58-373">Si vous rencontrez des problèmes liés au pare-feu, passer au mode de connexion passerelle qui ne nécessite que le port 443.</span><span class="sxs-lookup"><span data-stu-id="efa58-373">If you experience firewall issues, switch to connection mode Gateway, as it only requires port 443.</span></span>
> 
> 

## <span data-ttu-id="efa58-374"><a id="IndexingPolicy"></a>Spécification d’une stratégie d’indexation lors de la création de collections Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="efa58-374"><a id="IndexingPolicy"></a>Specify an indexing policy when creating Azure Cosmos DB collections</span></span>
<span data-ttu-id="efa58-375">Lorsque vous autorisez l'outil de migration à créer des collections pendant l'importation, vous pouvez spécifier la stratégie d'indexation des collections.</span><span class="sxs-lookup"><span data-stu-id="efa58-375">When you allow the migration tool to create collections during import, you can specify the indexing policy of the collections.</span></span> <span data-ttu-id="efa58-376">Dans la section des options d’importation en bloc avancées Azure Cosmos DB et des options d’enregistrement séquentiel Azure Cosmos DB, accédez à la section de la stratégie de l’indexation.</span><span class="sxs-lookup"><span data-stu-id="efa58-376">In the advanced options section of the Azure Cosmos DB Bulk import and Azure Cosmos DB Sequential record options, navigate to the Indexing Policy section.</span></span>

![Capture d’écran des options de stratégie d’indexation avancées d’Azure Cosmos DB](./media/import-data/indexingpolicy1.png)

<span data-ttu-id="efa58-378">À l'aide de l’option de stratégie d'indexation avancée, vous pouvez sélectionner un fichier de stratégie d'indexation, saisir manuellement une stratégie d'indexation ou en sélectionner une parmi les différents modèles proposés par défaut (en cliquant avec le bouton droit dans la zone de texte de stratégie d'indexation).</span><span class="sxs-lookup"><span data-stu-id="efa58-378">Using the Indexing Policy advanced option, you can select an indexing policy file, manually enter an indexing policy, or select from a set of default templates (by right clicking in the indexing policy textbox).</span></span>

<span data-ttu-id="efa58-379">L'outil fournit les modèles de stratégie suivants :</span><span class="sxs-lookup"><span data-stu-id="efa58-379">The policy templates the tool provides are:</span></span>

* <span data-ttu-id="efa58-380">Par défaut.</span><span class="sxs-lookup"><span data-stu-id="efa58-380">Default.</span></span> <span data-ttu-id="efa58-381">Cette stratégie est préférable si vous exécutez des requêtes d’efficacité sur des chaînes et des requêtes ORDER BY, de plage et d’efficacité sur des nombres.</span><span class="sxs-lookup"><span data-stu-id="efa58-381">This policy is best when you’re performing equality queries against strings and using ORDER BY, range, and equality queries for numbers.</span></span> <span data-ttu-id="efa58-382">Cette stratégie dispose d’une surcharge de stockage d'index inférieure à Plage.</span><span class="sxs-lookup"><span data-stu-id="efa58-382">This policy has a lower index storage overhead than Range.</span></span>
* <span data-ttu-id="efa58-383">Plage.</span><span class="sxs-lookup"><span data-stu-id="efa58-383">Range.</span></span> <span data-ttu-id="efa58-384">Cette stratégie est préférable si vous exécutez des requêtes ORDER BY, de plage et d'efficacité sur des nombres et des chaînes.</span><span class="sxs-lookup"><span data-stu-id="efa58-384">This policy is best you’re using ORDER BY, range and equality queries on both numbers and strings.</span></span> <span data-ttu-id="efa58-385">Cette stratégie dispose d’une surcharge de stockage d'index supérieure à Par défaut ou Hachage.</span><span class="sxs-lookup"><span data-stu-id="efa58-385">This policy has a higher index storage overhead than Default or Hash.</span></span>

![Capture d’écran des options de stratégie d’indexation avancées d’Azure Cosmos DB](./media/import-data/indexingpolicy2.png)

> [!NOTE]
> <span data-ttu-id="efa58-387">Si vous ne spécifiez pas de stratégie d'indexation, la stratégie par défaut sera appliquée.</span><span class="sxs-lookup"><span data-stu-id="efa58-387">If you do not specify an indexing policy, then the default policy will be applied.</span></span> <span data-ttu-id="efa58-388">Pour plus d’informations sur les stratégies d’indexation, consultez [Stratégies d’indexation d’Azure Cosmos DB](indexing-policies.md).</span><span class="sxs-lookup"><span data-stu-id="efa58-388">For more information about indexing policies, see [Azure Cosmos DB indexing policies](indexing-policies.md).</span></span>
> 
> 

## <a name="export-to-json-file"></a><span data-ttu-id="efa58-389">Exportation vers un fichier JSON</span><span class="sxs-lookup"><span data-stu-id="efa58-389">Export to JSON file</span></span>
<span data-ttu-id="efa58-390">L’exportateur JSON Azure Cosmos DB vous permet d’exporter des options sources disponibles vers un fichier JSON qui contient un tableau des documents JSON.</span><span class="sxs-lookup"><span data-stu-id="efa58-390">The Azure Cosmos DB JSON exporter allows you to export any of the available source options to a JSON file that contains an array of JSON documents.</span></span> <span data-ttu-id="efa58-391">L'outil gère l'exportation pour vous. Vous pouvez également choisir d'afficher la commande de migration qui en résulte et d’exécuter la commande vous-même.</span><span class="sxs-lookup"><span data-stu-id="efa58-391">The tool will handle the export for you, or you can choose to view the resulting migration command and run the command yourself.</span></span> <span data-ttu-id="efa58-392">Le fichier JSON résultant peut être stocké localement ou dans le stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="efa58-392">The resulting JSON file may be stored locally or in Azure Blob storage.</span></span>

![Capture d’écran des options d’exportation de fichier local JSON Azure Cosmos DB](./media/import-data/jsontarget.png)

![Capture d’écran des options d’exportation du stockage blob Azure JSON Azure Cosmos DB](./media/import-data/jsontarget2.png)

<span data-ttu-id="efa58-395">Vous pouvez éventuellement choisir d’agrémenter le JSON qui en résulte, ce qui augmente la taille du document obtenu tout en rendant le contenu plus lisible.</span><span class="sxs-lookup"><span data-stu-id="efa58-395">You may optionally choose to prettify the resulting JSON, which will increase the size of the resulting document while making the contents more human readable.</span></span>

    Standard JSON export
    [{"id":"Sample","Title":"About Paris","Language":{"Name":"English"},"Author":{"Name":"Don","Location":{"City":"Paris","Country":"France"}},"Content":"Don's document in Azure Cosmos DB is a valid JSON document as defined by the JSON spec.","PageViews":10000,"Topics":[{"Title":"History of Paris"},{"Title":"Places to see in Paris"}]}]

    Prettified JSON export
    [
     {
    "id": "Sample",
    "Title": "About Paris",
    "Language": {
      "Name": "English"
    },
    "Author": {
      "Name": "Don",
      "Location": {
        "City": "Paris",
        "Country": "France"
      }
    },
    "Content": "Don's document in Azure Cosmos DB is a valid JSON document as defined by the JSON spec.",
    "PageViews": 10000,
    "Topics": [
      {
        "Title": "History of Paris"
      },
      {
        "Title": "Places to see in Paris"
      }
    ]
    }]

## <a name="advanced-configuration"></a><span data-ttu-id="efa58-396">Configuration avancée</span><span class="sxs-lookup"><span data-stu-id="efa58-396">Advanced configuration</span></span>
<span data-ttu-id="efa58-397">Dans l'écran Configuration avancée, spécifiez l'emplacement du fichier journal dans lequel écrire toutes les erreurs.</span><span class="sxs-lookup"><span data-stu-id="efa58-397">In the Advanced configuration screen, specify the location of the log file to which you would like any errors written.</span></span> <span data-ttu-id="efa58-398">Les règles suivantes s'appliquent à cette page :</span><span class="sxs-lookup"><span data-stu-id="efa58-398">The following rules apply to this page:</span></span>

1. <span data-ttu-id="efa58-399">Si un nom de fichier n'est pas fourni, toutes les erreurs sont retournées dans la page de résultats.</span><span class="sxs-lookup"><span data-stu-id="efa58-399">If a file name is not provided, then all errors will be returned on the Results page.</span></span>
2. <span data-ttu-id="efa58-400">Si un nom de fichier est fourni sans répertoire, le fichier est créé (ou remplacé) dans le répertoire de l'environnement actuel.</span><span class="sxs-lookup"><span data-stu-id="efa58-400">If a file name is provided without a directory, then the file will be created (or overwritten) in the current environment directory.</span></span>
3. <span data-ttu-id="efa58-401">Si vous sélectionnez un fichier existant, le fichier est remplacé, il n'existe aucune option d'ajout.</span><span class="sxs-lookup"><span data-stu-id="efa58-401">If you select an existing file, then the file will be overwritten, there is no append option.</span></span>

<span data-ttu-id="efa58-402">Choisissez ensuite si vous souhaitez consigner tous les messages d’erreur, uniquement les messages critiques, ou aucun message d'erreur.</span><span class="sxs-lookup"><span data-stu-id="efa58-402">Then, choose whether to log all, critical, or no error messages.</span></span> <span data-ttu-id="efa58-403">Enfin, indiquez la fréquence à laquelle le message de transfert à l’écran sera mis à jour à mesure de sa progression.</span><span class="sxs-lookup"><span data-stu-id="efa58-403">Finally, decide how frequently the on screen transfer message will be updated with its progress.</span></span>

    ![Screenshot of Advanced configuration screen](./media/import-data/AdvancedConfiguration.png)

## <a name="confirm-import-settings-and-view-command-line"></a><span data-ttu-id="efa58-404">Confirmation des paramètres d'importation et affichage de la ligne de commande</span><span class="sxs-lookup"><span data-stu-id="efa58-404">Confirm import settings and view command line</span></span>
1. <span data-ttu-id="efa58-405">Après avoir spécifié les informations sources et cibles ainsi que la configuration avancée, vérifiez le résumé de la migration et affichez ou copiez éventuellement la commande de migration qui en résulte (la copie de la commande est utile pour automatiser les opérations d'importation) :</span><span class="sxs-lookup"><span data-stu-id="efa58-405">After specifying source information, target information, and advanced configuration, review the migration summary and, optionally, view/copy the resulting migration command (copying the command is useful to automate import operations):</span></span>
   
    ![Capture d'écran de l'écran de résumé](./media/import-data/summary.png)
   
    ![Capture d'écran de l'écran de résumé](./media/import-data/summarycommand.png)
2. <span data-ttu-id="efa58-408">Une fois que vous êtes satisfait de vos options sources et cibles, cliquez sur **Importer**.</span><span class="sxs-lookup"><span data-stu-id="efa58-408">Once you’re satisfied with your source and target options, click **Import**.</span></span> <span data-ttu-id="efa58-409">Le temps écoulé, le nombre transféré et les informations relatives aux échecs (si vous n'avez pas fourni de nom de fichier dans la Configuration avancée) sont mis à jour pendant le processus d'importation.</span><span class="sxs-lookup"><span data-stu-id="efa58-409">The elapsed time, transferred count, and failure information (if you didn't provide a file name in the Advanced configuration) will update as the import is in process.</span></span> <span data-ttu-id="efa58-410">Une fois cela terminé, vous pouvez exporter les résultats (par exemple, pour gérer les défaillances d’importation).</span><span class="sxs-lookup"><span data-stu-id="efa58-410">Once complete, you can export the results (e.g. to deal with any import failures).</span></span>
   
    ![Capture d’écran des options d’exportation JSON Azure Cosmos DB](./media/import-data/viewresults.png)
3. <span data-ttu-id="efa58-412">Vous pouvez également démarrer une nouvelle importation en conservant les paramètres existants (par exemple, les informations de la chaîne de connexion, le choix source et cible, etc.) ou en réinitialisant toutes les valeurs.</span><span class="sxs-lookup"><span data-stu-id="efa58-412">You may also start a new import, either keeping the existing settings (e.g. connection string information, source and target choice, etc.) or resetting all values.</span></span>
   
    ![Capture d’écran des options d’exportation JSON Azure Cosmos DB](./media/import-data/newimport.png)

## <a name="next-steps"></a><span data-ttu-id="efa58-414">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="efa58-414">Next steps</span></span>

<span data-ttu-id="efa58-415">Dans ce didacticiel, vous avez effectué les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="efa58-415">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="efa58-416">Installation de l’outil de migration de données</span><span class="sxs-lookup"><span data-stu-id="efa58-416">Installed the Data Migration tool</span></span>
> * <span data-ttu-id="efa58-417">Importation de données à partir de différentes sources de données</span><span class="sxs-lookup"><span data-stu-id="efa58-417">Imported data from different data sources</span></span>
> * <span data-ttu-id="efa58-418">Exportation de données à partir d’Azure Cosmos DB vers JSON</span><span class="sxs-lookup"><span data-stu-id="efa58-418">Exported from Azure Cosmos DB to JSON</span></span>

<span data-ttu-id="efa58-419">Vous pouvez maintenant passer à l’étape suivante du didacticiel et découvrir comment interroger les données à l’aide d’Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="efa58-419">You can now proceed to the next tutorial and learn how to query data using Azure Cosmos DB.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="efa58-420">Comment interroger les données ?</span><span class="sxs-lookup"><span data-stu-id="efa58-420">How to query data?</span></span>](../cosmos-db/tutorial-query-documentdb.md)
