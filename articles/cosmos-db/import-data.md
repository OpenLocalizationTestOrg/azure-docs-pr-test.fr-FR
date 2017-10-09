---
title: "outil de migration d’aaaDatabase pour la base de données Azure Cosmos | Documents Microsoft"
description: "Découvrez comment toouse hello Ouvrir source Azure Cosmos DB données migration tools tooimport données tooAzure Cosmos DB à partir de diverses sources, y compris les fichiers MongoDB, SQL Server, Table stockage, Amazon DynamoDB, CSV et JSON. Conversion de tooJSON de volume partagé de cluster."
keywords: "CSV toojson, outils de migration de base de données, convertir des csv toojson"
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
ms.openlocfilehash: 997648a31602d854db75bb6ce4e2ecff36fc1069
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimport-data-into-azure-cosmos-db-for-hello-documentdb-api"></a><span data-ttu-id="6bce2-105">Comment tooimport les données dans la base de données Azure Cosmos pour hello API DocumentDB ?</span><span class="sxs-lookup"><span data-stu-id="6bce2-105">How tooimport data into Azure Cosmos DB for hello DocumentDB API?</span></span>

<span data-ttu-id="6bce2-106">Ce didacticiel fournit des instructions sur l’utilisation de hello de base de données Azure Cosmos : outil de Migration des données API DocumentDB, qui peut importer des données de diverses sources, y compris les fichiers JSON, des fichiers CSV, SQL, MongoDB, le stockage de Table Windows Azure, Amazon DynamoDB et DocumentDB de base de données Azure Cosmos Collections d’API dans des collections pour utilisent avec la base de données Azure Cosmos et hello API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="6bce2-106">This tutorial provides instructions on using hello Azure Cosmos DB: DocumentDB API Data Migration tool, which can import data from various sources, including JSON files, CSV files, SQL, MongoDB, Azure Table storage, Amazon DynamoDB and Azure Cosmos DB DocumentDB API collections into collections for use with Azure Cosmos DB and hello DocumentDB API.</span></span> <span data-ttu-id="6bce2-107">outil de Migration des données Hello peut également servir lors de la migration à partir d’une seule partition tooa plusieurs partitions collecte pour hello API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="6bce2-107">hello Data Migration tool can also be used when migrating from a single partition collection tooa multi-partition collection for hello DocumentDB API.</span></span>

<span data-ttu-id="6bce2-108">outil de Migration des données Hello fonctionne uniquement lors de l’importation de données dans la base de données Azure Cosmos pour utiliser avec hello API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="6bce2-108">hello Data Migration tool only works when importing data into Azure Cosmos DB for use with hello DocumentDB API.</span></span> <span data-ttu-id="6bce2-109">L’importation de données pour une utilisation avec hello API de Table ou de l’API Graph n’est pas prise en charge pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="6bce2-109">Importing data for use with hello Table API or Graph API is not supported at this time.</span></span> 

<span data-ttu-id="6bce2-110">tooimport de données pour une utilisation avec hello MongoDB API, consultez [base de données Azure Cosmos : comment les données de toomigrate hello MongoDB API ?](mongodb-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="6bce2-110">tooimport data for use with hello MongoDB API, see [Azure Cosmos DB: How toomigrate data for hello MongoDB API?](mongodb-migrate.md).</span></span>

<span data-ttu-id="6bce2-111">Ce didacticiel couvre hello tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="6bce2-111">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6bce2-112">Installation de l’outil de Migration des données hello</span><span class="sxs-lookup"><span data-stu-id="6bce2-112">Installing hello Data Migration tool</span></span>
> * <span data-ttu-id="6bce2-113">Importation de données à partir de différentes sources de données</span><span class="sxs-lookup"><span data-stu-id="6bce2-113">Importing data from different data sources</span></span>
> * <span data-ttu-id="6bce2-114">Exportation à partir de la base de données Azure Cosmos tooJSON</span><span class="sxs-lookup"><span data-stu-id="6bce2-114">Exporting from Azure Cosmos DB tooJSON</span></span>

## <span data-ttu-id="6bce2-115"><a id="Prerequisites"></a>Configuration requise</span><span class="sxs-lookup"><span data-stu-id="6bce2-115"><a id="Prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="6bce2-116">Avant de suivre les instructions de hello dans cet article, assurez-vous d’avoir installé des éléments suivants hello :</span><span class="sxs-lookup"><span data-stu-id="6bce2-116">Before following hello instructions in this article, ensure that you have hello following installed:</span></span>

* <span data-ttu-id="6bce2-117">[Microsoft .NET Framework 4.51](https://www.microsoft.com/download/developer-tools.aspx) ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="6bce2-117">[Microsoft .NET Framework 4.51](https://www.microsoft.com/download/developer-tools.aspx) or higher.</span></span>

## <span data-ttu-id="6bce2-118"><a id="Overviewl"></a>Vue d’ensemble de l’outil de Migration des données hello</span><span class="sxs-lookup"><span data-stu-id="6bce2-118"><a id="Overviewl"></a>Overview of hello Data Migration tool</span></span>
<span data-ttu-id="6bce2-119">outil de Migration des données Hello est une solution open source qui importe des données tooAzure Cosmos DB à partir de diverses sources, notamment :</span><span class="sxs-lookup"><span data-stu-id="6bce2-119">hello Data Migration tool is an open source solution that imports data tooAzure Cosmos DB from a variety of sources, including:</span></span>

* <span data-ttu-id="6bce2-120">Fichiers JSON</span><span class="sxs-lookup"><span data-stu-id="6bce2-120">JSON files</span></span>
* <span data-ttu-id="6bce2-121">MongoDB</span><span class="sxs-lookup"><span data-stu-id="6bce2-121">MongoDB</span></span>
* <span data-ttu-id="6bce2-122">SQL Server</span><span class="sxs-lookup"><span data-stu-id="6bce2-122">SQL Server</span></span>
* <span data-ttu-id="6bce2-123">Fichiers CSV</span><span class="sxs-lookup"><span data-stu-id="6bce2-123">CSV files</span></span>
* <span data-ttu-id="6bce2-124">Stockage de tables Azure</span><span class="sxs-lookup"><span data-stu-id="6bce2-124">Azure Table storage</span></span>
* <span data-ttu-id="6bce2-125">Amazon DynamoDB</span><span class="sxs-lookup"><span data-stu-id="6bce2-125">Amazon DynamoDB</span></span>
* <span data-ttu-id="6bce2-126">HBase</span><span class="sxs-lookup"><span data-stu-id="6bce2-126">HBase</span></span>
* <span data-ttu-id="6bce2-127">Collections Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="6bce2-127">Azure Cosmos DB collections</span></span>

<span data-ttu-id="6bce2-128">Pendant que l’outil d’importation hello inclut une interface utilisateur graphique (dtui.exe), il peut également être pilotée à partir de la ligne de commande hello (dt.exe).</span><span class="sxs-lookup"><span data-stu-id="6bce2-128">While hello import tool includes a graphical user interface (dtui.exe), it can also be driven from hello command line (dt.exe).</span></span> <span data-ttu-id="6bce2-129">En fait, il est une option de commande de hello associé toooutput après avoir configuré une importation via l’interface utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="6bce2-129">In fact, there is an option toooutput hello associated command after setting up an import through hello UI.</span></span> <span data-ttu-id="6bce2-130">Des données sources tabulaires (par exemple, des fichiers SQL Server ou CSV) peuvent être transformées de manière à ce que des relations hiérarchiques (sous-documents) puissent être créées pendant l'importation.</span><span class="sxs-lookup"><span data-stu-id="6bce2-130">Tabular source data (e.g. SQL Server or CSV files) can be transformed such that hierarchical relationships (subdocuments) can be created during import.</span></span> <span data-ttu-id="6bce2-131">Conserver la lecture toolearn plus d’informations sur les options de source, tooimport de lignes de commande d’exemple à partir de chaque source, importer options cibles et l’affichage des résultats.</span><span class="sxs-lookup"><span data-stu-id="6bce2-131">Keep reading toolearn more about source options, sample command lines tooimport from each source, target options, and viewing import results.</span></span>

## <span data-ttu-id="6bce2-132"><a id="Install"></a>Installer l’outil de Migration des données hello</span><span class="sxs-lookup"><span data-stu-id="6bce2-132"><a id="Install"></a>Install hello Data Migration tool</span></span>
<span data-ttu-id="6bce2-133">code de source d’outil de migration Hello est disponible sur GitHub dans [ce référentiel](https://github.com/azure/azure-documentdb-datamigrationtool) et une version compilée est disponible à partir de [Microsoft Download Center](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d).</span><span class="sxs-lookup"><span data-stu-id="6bce2-133">hello migration tool source code is available on GitHub in [this repository](https://github.com/azure/azure-documentdb-datamigrationtool) and a compiled version is available from [Microsoft Download Center](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d).</span></span> <span data-ttu-id="6bce2-134">Vous pouvez compiler hello solution ou simplement télécharger et extraire le répertoire de tooa hello version compilée de votre choix.</span><span class="sxs-lookup"><span data-stu-id="6bce2-134">You may either compile hello solution or simply download and extract hello compiled version tooa directory of your choice.</span></span> <span data-ttu-id="6bce2-135">Exécutez ensuite l’un des fichiers suivants :</span><span class="sxs-lookup"><span data-stu-id="6bce2-135">Then run either:</span></span>

* <span data-ttu-id="6bce2-136">**Dtui.exe**: version de l’interface graphique de l’outil de hello</span><span class="sxs-lookup"><span data-stu-id="6bce2-136">**Dtui.exe**: Graphical interface version of hello tool</span></span>
* <span data-ttu-id="6bce2-137">**DT.exe**: version de ligne de commande de l’outil de hello</span><span class="sxs-lookup"><span data-stu-id="6bce2-137">**Dt.exe**: Command-line version of hello tool</span></span>

## <a name="import-data"></a><span data-ttu-id="6bce2-138">Importer des données</span><span class="sxs-lookup"><span data-stu-id="6bce2-138">Import data</span></span>

<span data-ttu-id="6bce2-139">Une fois que vous avez installé l’outil de hello, il est temps tooimport vos données.</span><span class="sxs-lookup"><span data-stu-id="6bce2-139">Once you've installed hello tool, it's time tooimport your data.</span></span> <span data-ttu-id="6bce2-140">Le type de données voulez-vous tooimport ?</span><span class="sxs-lookup"><span data-stu-id="6bce2-140">What kind of data do you want tooimport?</span></span>

* [<span data-ttu-id="6bce2-141">Fichiers JSON</span><span class="sxs-lookup"><span data-stu-id="6bce2-141">JSON files</span></span>](#JSON)
* [<span data-ttu-id="6bce2-142">MongoDB</span><span class="sxs-lookup"><span data-stu-id="6bce2-142">MongoDB</span></span>](#MongoDB)
* [<span data-ttu-id="6bce2-143">Fichiers d’exportation MongoDB</span><span class="sxs-lookup"><span data-stu-id="6bce2-143">MongoDB Export files</span></span>](#MongoDBExport)
* [<span data-ttu-id="6bce2-144">SQL Server</span><span class="sxs-lookup"><span data-stu-id="6bce2-144">SQL Server</span></span>](#SQL)
* [<span data-ttu-id="6bce2-145">Fichiers CSV</span><span class="sxs-lookup"><span data-stu-id="6bce2-145">CSV files</span></span>](#CSV)
* [<span data-ttu-id="6bce2-146">Stockage Table Azure</span><span class="sxs-lookup"><span data-stu-id="6bce2-146">Azure Table storage</span></span>](#AzureTableSource)
* [<span data-ttu-id="6bce2-147">Amazon DynamoDB</span><span class="sxs-lookup"><span data-stu-id="6bce2-147">Amazon DynamoDB</span></span>](#DynamoDBSource)
* [<span data-ttu-id="6bce2-148">Objet blob</span><span class="sxs-lookup"><span data-stu-id="6bce2-148">Blob</span></span>](#BlobImport)
* [<span data-ttu-id="6bce2-149">Collections Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="6bce2-149">Azure Cosmos DB collections</span></span>](#DocumentDBSource)
* [<span data-ttu-id="6bce2-150">HBase</span><span class="sxs-lookup"><span data-stu-id="6bce2-150">HBase</span></span>](#HBaseSource)
* [<span data-ttu-id="6bce2-151">Importation en bloc Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="6bce2-151">Azure Cosmos DB bulk import</span></span>](#DocumentDBBulkImport)
* [<span data-ttu-id="6bce2-152">Importation d’enregistrement séquentiel Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="6bce2-152">Azure Cosmos DB sequential record import</span></span>](#DocumentDSeqTarget)


## <span data-ttu-id="6bce2-153"><a id="JSON"></a>fichiers au format JSON tooimport</span><span class="sxs-lookup"><span data-stu-id="6bce2-153"><a id="JSON"></a>tooimport JSON files</span></span>
<span data-ttu-id="6bce2-154">Hello option importateur JSON fichier source vous permet de tooimport un ou plusieurs de documents JSON fichiers ou JSON qui contiennent chacun un tableau des documents JSON.</span><span class="sxs-lookup"><span data-stu-id="6bce2-154">hello JSON file source importer option allows you tooimport one or more single document JSON files or JSON files that each contain an array of JSON documents.</span></span> <span data-ttu-id="6bce2-155">Lorsque vous ajoutez des dossiers qui contiennent des tooimport de fichiers JSON, vous pouvez hello de rechercher des fichiers dans les sous-dossiers de manière récursive.</span><span class="sxs-lookup"><span data-stu-id="6bce2-155">When adding folders that contain JSON files tooimport, you have hello option of recursively searching for files in subfolders.</span></span>

![Capture d’écran des options sources du fichier JSON - Outils de migration de base de données](./media/import-data/jsonsource.png)

<span data-ttu-id="6bce2-157">Voici quelques exemples de ligne de commande fichiers JSON tooimport :</span><span class="sxs-lookup"><span data-stu-id="6bce2-157">Here are some command line samples tooimport JSON files:</span></span>

    #Import a single JSON file
    dt.exe /s:JsonFile /s.Files:.\Sessions.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Sessions /t.CollectionThroughput:2500

    #Import a directory of JSON files
    dt.exe /s:JsonFile /s.Files:C:\TESessions\*.json /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Sessions /t.CollectionThroughput:2500

    #Import a directory (including sub-directories) of JSON files
    dt.exe /s:JsonFile /s.Files:C:\LastFMMusic\**\*.json /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Music /t.CollectionThroughput:2500

    #Import a directory (single), directory (recursive), and individual JSON files
    dt.exe /s:JsonFile /s.Files:C:\Tweets\*.*;C:\LargeDocs\**\*.*;C:\TESessions\Session48172.json;C:\TESessions\Session48173.json;C:\TESessions\Session48174.json;C:\TESessions\Session48175.json;C:\TESessions\Session48177.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:subs /t.CollectionThroughput:2500

    #Import a single JSON file and partition hello data across 4 collections
    dt.exe /s:JsonFile /s.Files:D:\\CompanyData\\Companies.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:comp[1-4] /t.PartitionKey:name /t.CollectionThroughput:2500

## <span data-ttu-id="6bce2-158"><a id="MongoDB"></a>tooimport de MongoDB</span><span class="sxs-lookup"><span data-stu-id="6bce2-158"><a id="MongoDB"></a>tooimport from MongoDB</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6bce2-159">Si vous importez un compte de base de données Azure Cosmos tooan avec prise en charge pour MongoDB, suivez ces [instructions](mongodb-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="6bce2-159">If you are importing tooan Azure Cosmos DB account with Support for MongoDB, follow these [instructions](mongodb-migrate.md).</span></span>
> 
> 

<span data-ttu-id="6bce2-160">Hello option d’importateur MongoDB source vous permet de tooimport à partir d’une collection de MongoDB individuels et en option, filtrez les documents à l’aide d’une requête et/ou modifier la structure du document hello à l’aide d’une projection.</span><span class="sxs-lookup"><span data-stu-id="6bce2-160">hello MongoDB source importer option allows you tooimport from an individual MongoDB collection and optionally filter documents using a query and/or modify hello document structure by using a projection.</span></span>  

![Capture d’écran des options sources MongoDB](./media/import-data/mongodbsource.png)

<span data-ttu-id="6bce2-162">chaîne de connexion Hello est au format de MongoDB hello standard :</span><span class="sxs-lookup"><span data-stu-id="6bce2-162">hello connection string is in hello standard MongoDB format:</span></span>

    mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database>

> [!NOTE]
> <span data-ttu-id="6bce2-163">Utilisez hello Vérifiez commande tooensure qui hello instance MongoDB spécifiée dans le champ de chaîne de connexion hello est accessible.</span><span class="sxs-lookup"><span data-stu-id="6bce2-163">Use hello Verify command tooensure that hello MongoDB instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="6bce2-164">Entrez le nom hello de collection hello à partir de laquelle les données seront importées.</span><span class="sxs-lookup"><span data-stu-id="6bce2-164">Enter hello name of hello collection from which data will be imported.</span></span> <span data-ttu-id="6bce2-165">Vous pouvez éventuellement spécifier ou fournir un fichier pour une requête (par exemple, {pop : {$gt : 5000}}) et/ou la projection (par exemple, {loc:0}) tooboth filtre et forme hello données toobe importé.</span><span class="sxs-lookup"><span data-stu-id="6bce2-165">You may optionally specify or provide a file for a query (e.g. {pop: {$gt:5000}} ) and/or projection (e.g. {loc:0} ) tooboth filter and shape hello data toobe imported.</span></span>

<span data-ttu-id="6bce2-166">Voici certains tooimport d’exemples de ligne de commande à partir de MongoDB :</span><span class="sxs-lookup"><span data-stu-id="6bce2-166">Here are some command line samples tooimport from MongoDB:</span></span>

    #Import all documents from a MongoDB collection
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZips /t.IdField:_id /t.CollectionThroughput:2500

    #Import documents from a MongoDB collection which match hello query and exclude hello loc field
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /s.Query:{pop:{$gt:50000}} /s.Projection:{loc:0} /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZipsTransform /t.IdField:_id/t.CollectionThroughput:2500

## <span data-ttu-id="6bce2-167"><a id="MongoDBExport"></a>fichiers d’exportation tooimport MongoDB</span><span class="sxs-lookup"><span data-stu-id="6bce2-167"><a id="MongoDBExport"></a>tooimport MongoDB export files</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6bce2-168">Si vous importez un compte de base de données Azure Cosmos tooan avec prise en charge pour MongoDB, suivez ces [instructions](mongodb-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="6bce2-168">If you are importing tooan Azure Cosmos DB account with support for MongoDB, follow these [instructions](mongodb-migrate.md).</span></span>
> 
> 

<span data-ttu-id="6bce2-169">Hello, option du fichier source importateur pour MongoDB exportation JSON vous permet de tooimport un ou plusieurs fichiers JSON généré par l’utilitaire mongoexport hello.</span><span class="sxs-lookup"><span data-stu-id="6bce2-169">hello MongoDB export JSON file source importer option allows you tooimport one or more JSON files produced from hello mongoexport utility.</span></span>  

![Capture d’écran des options sources d’exportation MongoDB](./media/import-data/mongodbexportsource.png)

<span data-ttu-id="6bce2-171">Lorsque vous ajoutez des dossiers qui contiennent les fichiers JSON d’exportation MongoDB pour l’importation, vous pouvez hello de rechercher des fichiers dans les sous-dossiers de manière récursive.</span><span class="sxs-lookup"><span data-stu-id="6bce2-171">When adding folders that contain MongoDB export JSON files for import, you have hello option of recursively searching for files in subfolders.</span></span>

<span data-ttu-id="6bce2-172">Voici une tooimport d’exemple de ligne de commande à partir de l’exportation de MongoDB fichiers JSON :</span><span class="sxs-lookup"><span data-stu-id="6bce2-172">Here is a command line sample tooimport from MongoDB export JSON files:</span></span>

    dt.exe /s:MongoDBExport /s.Files:D:\mongoemployees.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:employees /t.IdField:_id /t.Dates:Epoch /t.CollectionThroughput:2500

## <span data-ttu-id="6bce2-173"><a id="SQL"></a>tooimport à partir de SQL Server</span><span class="sxs-lookup"><span data-stu-id="6bce2-173"><a id="SQL"></a>tooimport from SQL Server</span></span>
<span data-ttu-id="6bce2-174">Hello option importateur de la source SQL vous permet de tooimport à partir d’une base de données SQL Server et en option, filtrez toobe d’enregistrements hello importé à l’aide d’une requête.</span><span class="sxs-lookup"><span data-stu-id="6bce2-174">hello SQL source importer option allows you tooimport from an individual SQL Server database and optionally filter hello records toobe imported using a query.</span></span> <span data-ttu-id="6bce2-175">En outre, vous pouvez modifier la structure du document hello en spécifiant un séparateur d’imbrication (plus tard).</span><span class="sxs-lookup"><span data-stu-id="6bce2-175">In addition, you can modify hello document structure by specifying a nesting separator (more on that in a moment).</span></span>  

![Capture d’écran des options sources SQL - Outils de migration de base de données](./media/import-data/sqlexportsource.png)

<span data-ttu-id="6bce2-177">Hello de chaîne de connexion hello est format de chaîne de connexion hello standard SQL.</span><span class="sxs-lookup"><span data-stu-id="6bce2-177">hello format of hello connection string is hello standard SQL connection string format.</span></span>

> [!NOTE]
> <span data-ttu-id="6bce2-178">Utilisez hello Vérifiez commande tooensure qui hello instance SQL Server spécifiée dans le champ de chaîne de connexion hello est accessible.</span><span class="sxs-lookup"><span data-stu-id="6bce2-178">Use hello Verify command tooensure that hello SQL Server instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="6bce2-179">Hello imbrication propriété separator est (sous-documents) des relations hiérarchiques toocreate utilisé pendant l’importation.</span><span class="sxs-lookup"><span data-stu-id="6bce2-179">hello nesting separator property is used toocreate hierarchical relationships (sub-documents) during import.</span></span> <span data-ttu-id="6bce2-180">Tenez compte des hello suivant la requête SQL :</span><span class="sxs-lookup"><span data-stu-id="6bce2-180">Consider hello following SQL query:</span></span>

<span data-ttu-id="6bce2-181">*select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'*</span><span class="sxs-lookup"><span data-stu-id="6bce2-181">*select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'*</span></span>

<span data-ttu-id="6bce2-182">Qui renvoie hello suivant des résultats (partielles) :</span><span class="sxs-lookup"><span data-stu-id="6bce2-182">Which returns hello following (partial) results:</span></span>

![Capture d’écran des résultats de requête SQL](./media/import-data/sqlqueryresults.png)

<span data-ttu-id="6bce2-184">Notez les alias hello telles que Address.AddressType et Address.Location.StateProvinceName.</span><span class="sxs-lookup"><span data-stu-id="6bce2-184">Note hello aliases such as Address.AddressType and Address.Location.StateProvinceName.</span></span> <span data-ttu-id="6bce2-185">En spécifiant un séparateur d’imbrication de '.', outil d’importation hello crée l’adresse et d’importer des sous-documents Address.Location pendant hello.</span><span class="sxs-lookup"><span data-stu-id="6bce2-185">By specifying a nesting separator of ‘.’, hello import tool creates Address and Address.Location subdocuments during hello import.</span></span> <span data-ttu-id="6bce2-186">Voici un exemple de document qui en résulte dans Azure Cosmos DB :</span><span class="sxs-lookup"><span data-stu-id="6bce2-186">Here is an example of a resulting document in Azure Cosmos DB:</span></span>

<span data-ttu-id="6bce2-187">*{« ID » : « 956 », « Nom » : « Service et vente au détail », « Adresse »: {« AddressType »: « Siège », « AddressLine1 »: « #500-75 o ’ Connor Street », « Lieu »: {« Ville »: « Ottawa », « StateProvinceName »: « Ontario »}, « Code postal »: « K4B 1S2 », « CountryRegionName »: « Canada »}}*</span><span class="sxs-lookup"><span data-stu-id="6bce2-187">*{ "id": "956", "Name": "Finer Sales and Service", "Address": { "AddressType": "Main Office", "AddressLine1": "#500-75 O'Connor Street", "Location": { "City": "Ottawa", "StateProvinceName": "Ontario" }, "PostalCode": "K4B 1S2", "CountryRegionName": "Canada" } }*</span></span>

<span data-ttu-id="6bce2-188">Voici certains tooimport d’exemples de ligne de commande à partir de SQL Server :</span><span class="sxs-lookup"><span data-stu-id="6bce2-188">Here are some command line samples tooimport from SQL Server:</span></span>

    #Import records from SQL which match a query
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, * from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Stores /t.IdField:Id /t.CollectionThroughput:2500

    #Import records from sql which match a query and create hierarchical relationships
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /s.NestingSeparator:. /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:StoresSub /t.IdField:Id /t.CollectionThroughput:2500

## <span data-ttu-id="6bce2-189"><a id="CSV"></a>les fichiers CSV tooimport et convert CSV tooJSON</span><span class="sxs-lookup"><span data-stu-id="6bce2-189"><a id="CSV"></a>tooimport CSV files and convert CSV tooJSON</span></span>
<span data-ttu-id="6bce2-190">Hello, option d’importateur CSV fichier source permet de vous tooimport un ou plusieurs fichiers CSV.</span><span class="sxs-lookup"><span data-stu-id="6bce2-190">hello CSV file source importer option enables you tooimport one or more CSV files.</span></span> <span data-ttu-id="6bce2-191">Lorsque vous ajoutez des dossiers qui contiennent les fichiers des volumes partagés de cluster pour l’importation, vous pouvez hello de rechercher des fichiers dans les sous-dossiers de manière récursive.</span><span class="sxs-lookup"><span data-stu-id="6bce2-191">When adding folders that contain CSV files for import, you have hello option of recursively searching for files in subfolders.</span></span>

![Options de source de capture d’écran de volume partagé de cluster - CSV tooJSON](media/import-data/csvsource.png)

<span data-ttu-id="6bce2-193">Source SQL toohello similaire, hello imbrication separator, propriété peut être utilisé toocreate des relations hiérarchiques (sous-chemin de documents) lors de l’importation.</span><span class="sxs-lookup"><span data-stu-id="6bce2-193">Similar toohello SQL source, hello nesting separator property may be used toocreate hierarchical relationships (sub-documents) during import.</span></span> <span data-ttu-id="6bce2-194">Tenez compte des hello suivant la ligne d’en-tête de volume partagé de cluster et les lignes de données :</span><span class="sxs-lookup"><span data-stu-id="6bce2-194">Consider hello following CSV header row and data rows:</span></span>

![Exemples d’enregistrements d’écran de volume partagé de cluster - CSV tooJSON](./media/import-data/csvsample.png)

<span data-ttu-id="6bce2-196">Notez les alias hello telles que DomainInfo.Domain_Name et RedirectInfo.Redirecting.</span><span class="sxs-lookup"><span data-stu-id="6bce2-196">Note hello aliases such as DomainInfo.Domain_Name and RedirectInfo.Redirecting.</span></span> <span data-ttu-id="6bce2-197">En spécifiant un séparateur d’imbrication de '.', outil d’importation hello créera DomainInfo et importer des sous-documents RedirectInfo pendant hello.</span><span class="sxs-lookup"><span data-stu-id="6bce2-197">By specifying a nesting separator of ‘.’, hello import tool will create DomainInfo and RedirectInfo subdocuments during hello import.</span></span> <span data-ttu-id="6bce2-198">Voici un exemple de document qui en résulte dans Azure Cosmos DB :</span><span class="sxs-lookup"><span data-stu-id="6bce2-198">Here is an example of a resulting document in Azure Cosmos DB:</span></span>

<span data-ttu-id="6bce2-199">*{« DomainInfo » : {« Nom_domaine » : « ACUS.GOV », « Domain_Name_Address » : « http://www. ACUS.GOV »}, « Agence fédérale » : « Conférence Administrative de hello United States », « RedirectInfo » : {« Redirection » : « 0 », « Redirect_Destination » : « »}, « id » : « 9cc565c5-ebcd-1c03-ebd3-cc3e2ecd814d »}*</span><span class="sxs-lookup"><span data-stu-id="6bce2-199">*{ "DomainInfo": { "Domain_Name": "ACUS.GOV", "Domain_Name_Address": "http://www.ACUS.GOV" }, "Federal Agency": "Administrative Conference of hello United States", "RedirectInfo": { "Redirecting": "0", "Redirect_Destination": "" }, "id": "9cc565c5-ebcd-1c03-ebd3-cc3e2ecd814d" }*</span></span>

<span data-ttu-id="6bce2-200">outil d’importation Hello va tenter de tooinfer informations de type pour les valeurs sans guillemets dans les fichiers CSV (valeurs entre guillemets sont toujours traités en tant que chaînes).</span><span class="sxs-lookup"><span data-stu-id="6bce2-200">hello import tool will attempt tooinfer type information for unquoted values in CSV files (quoted values are always treated as strings).</span></span>  <span data-ttu-id="6bce2-201">Les types sont identifiées dans hello suivant l’ordre : nombre, date/heure, valeur booléenne.</span><span class="sxs-lookup"><span data-stu-id="6bce2-201">Types are identified in hello following order: number, datetime, boolean.</span></span>  

<span data-ttu-id="6bce2-202">Il existe deux autres toonote de choses sur l’importation d’un volume partagé de cluster :</span><span class="sxs-lookup"><span data-stu-id="6bce2-202">There are two other things toonote about CSV import:</span></span>

1. <span data-ttu-id="6bce2-203">Par défaut, les valeurs sans guillemets sont toujours privées de leurs tabulations et espaces, tandis que les valeurs entre guillemets sont conservées telles quelles.</span><span class="sxs-lookup"><span data-stu-id="6bce2-203">By default, unquoted values are always trimmed for tabs and spaces, while quoted values are preserved as-is.</span></span> <span data-ttu-id="6bce2-204">Ce comportement peut être substitué par hello que Trim entre guillemets l’option de ligne de commande /s.TrimQuoted case à cocher ou hello des valeurs.</span><span class="sxs-lookup"><span data-stu-id="6bce2-204">This behavior can be overridden with hello Trim quoted values checkbox or hello /s.TrimQuoted command line option.</span></span>
2. <span data-ttu-id="6bce2-205">Par défaut, une valeur null sans guillemets est considérée comme une valeur null.</span><span class="sxs-lookup"><span data-stu-id="6bce2-205">By default, an unquoted null is treated as a null value.</span></span> <span data-ttu-id="6bce2-206">Ce comportement peut être substitué (autrement dit, de traiter une valeur null sans guillemets sous forme de chaîne « null ») avec hello Treat NULL en tant qu’option de ligne de commande /s.NoUnquotedNulls case à cocher ou hello des chaîne de guillemets.</span><span class="sxs-lookup"><span data-stu-id="6bce2-206">This behavior can be overridden (i.e. treat an unquoted null as a “null” string) with hello Treat unquoted NULL as string checkbox or hello /s.NoUnquotedNulls command line option.</span></span>

<span data-ttu-id="6bce2-207">Voici un exemple de ligne de commande pour une importation CSV :</span><span class="sxs-lookup"><span data-stu-id="6bce2-207">Here is a command line sample for CSV import:</span></span>

    dt.exe /s:CsvFile /s.Files:.\Employees.csv /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Employees /t.IdField:EntityID /t.CollectionThroughput:2500

## <span data-ttu-id="6bce2-208"><a id="AzureTableSource"></a>tooimport à partir du stockage de Table Azure</span><span class="sxs-lookup"><span data-stu-id="6bce2-208"><a id="AzureTableSource"></a>tooimport from Azure Table storage</span></span>
<span data-ttu-id="6bce2-209">Hello option d’importateur de source de stockage Azure Table vous permet de tooimport à partir d’une table de stockage Azure Table individuelle et en option, filtrez toobe d’entités de table hello importé.</span><span class="sxs-lookup"><span data-stu-id="6bce2-209">hello Azure Table storage source importer option allows you tooimport from an individual Azure Table storage table and optionally filter hello table entities toobe imported.</span></span> <span data-ttu-id="6bce2-210">Notez que vous ne peut pas utiliser des données de stockage Azure Table hello Migration des données outil tooimport dans la base de données Azure Cosmos pour une utilisation avec hello API de Table.</span><span class="sxs-lookup"><span data-stu-id="6bce2-210">Note that you cannot use hello Data Migration tool tooimport Azure Table storage data into Azure Cosmos DB for use with hello Table API.</span></span> <span data-ttu-id="6bce2-211">Uniquement l’importation tooAzure Cosmos DB pour une utilisation avec hello API DocumentDB est pris en charge pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="6bce2-211">Only importing tooAzure Cosmos DB for use with hello DocumentDB API is supported at this time.</span></span>

![Capture d’écran des options sources de stockage de tables Azure](./media/import-data/azuretablesource.png)

<span data-ttu-id="6bce2-213">format Hello Hello chaîne de connexion de stockage de Table Azure est la suivante :</span><span class="sxs-lookup"><span data-stu-id="6bce2-213">hello format of hello Azure Table storage connection string is:</span></span>

    DefaultEndpointsProtocol=<protocol>;AccountName=<Account Name>;AccountKey=<Account Key>;

> [!NOTE]
> <span data-ttu-id="6bce2-214">Utilisez hello Vérifiez commande tooensure qui hello instance de stockage Azure Table spécifiée dans le champ de chaîne de connexion hello est accessible.</span><span class="sxs-lookup"><span data-stu-id="6bce2-214">Use hello Verify command tooensure that hello Azure Table storage instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="6bce2-215">Entrez le nom hello Hello Azure table à partir de laquelle les données seront importées.</span><span class="sxs-lookup"><span data-stu-id="6bce2-215">Enter hello name of hello Azure table from which data will be imported.</span></span> <span data-ttu-id="6bce2-216">Vous pouvez éventuellement spécifier un [filtre](https://msdn.microsoft.com/library/azure/ff683669.aspx).</span><span class="sxs-lookup"><span data-stu-id="6bce2-216">You may optionally specify a [filter](https://msdn.microsoft.com/library/azure/ff683669.aspx).</span></span>

<span data-ttu-id="6bce2-217">Hello, option de Table Azure storage source importateur a hello options supplémentaires suivantes :</span><span class="sxs-lookup"><span data-stu-id="6bce2-217">hello Azure Table storage source importer option has hello following additional options:</span></span>

1. <span data-ttu-id="6bce2-218">Inclusion des champs internes</span><span class="sxs-lookup"><span data-stu-id="6bce2-218">Include Internal Fields</span></span>
   1. <span data-ttu-id="6bce2-219">Tous : inclure tous les champs internes (PartitionKey, RowKey et Timestamp)</span><span class="sxs-lookup"><span data-stu-id="6bce2-219">All - Include all internal fields (PartitionKey, RowKey, and Timestamp)</span></span>
   2. <span data-ttu-id="6bce2-220">Aucun : exclure tous les champs internes</span><span class="sxs-lookup"><span data-stu-id="6bce2-220">None - Exclude all internal fields</span></span>
   3. <span data-ttu-id="6bce2-221">RowKey - inclure uniquement les champs de RowKey hello</span><span class="sxs-lookup"><span data-stu-id="6bce2-221">RowKey - Only include hello RowKey field</span></span>
2. <span data-ttu-id="6bce2-222">Sélection des colonnes</span><span class="sxs-lookup"><span data-stu-id="6bce2-222">Select Columns</span></span>
   1. <span data-ttu-id="6bce2-223">Les filtres de stockage de tables Azure ne prennent pas en charge les projections.</span><span class="sxs-lookup"><span data-stu-id="6bce2-223">Azure Table storage filters do not support projections.</span></span> <span data-ttu-id="6bce2-224">Si vous souhaitez que les propriétés d’entité tooonly importation spécifiques Table Azure, ajoutez-les comme liste de sélection des colonnes toohello.</span><span class="sxs-lookup"><span data-stu-id="6bce2-224">If you want tooonly import specific Azure Table entity properties, add them toohello Select Columns list.</span></span> <span data-ttu-id="6bce2-225">Toutes les autres propriétés d'entité seront ignorées.</span><span class="sxs-lookup"><span data-stu-id="6bce2-225">All other entity properties will be ignored.</span></span>

<span data-ttu-id="6bce2-226">Voici une tooimport d’exemple de ligne de commande à partir du stockage de Table Azure :</span><span class="sxs-lookup"><span data-stu-id="6bce2-226">Here is a command line sample tooimport from Azure Table storage:</span></span>

    dt.exe /s:AzureTable /s.ConnectionString:"DefaultEndpointsProtocol=https;AccountName=<Account Name>;AccountKey=<Account Key>" /s.Table:metrics /s.InternalFields:All /s.Filter:"PartitionKey eq 'Partition1' and RowKey gt '00001'" /s.Projection:ObjectCount;ObjectSize  /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:metrics /t.CollectionThroughput:2500

## <span data-ttu-id="6bce2-227"><a id="DynamoDBSource"></a>tooimport d’Amazon DynamoDB</span><span class="sxs-lookup"><span data-stu-id="6bce2-227"><a id="DynamoDBSource"></a>tooimport from Amazon DynamoDB</span></span>
<span data-ttu-id="6bce2-228">Hello, option d’importateur Amazon DynamoDB source vous permet de tooimport à partir d’une table Amazon DynamoDB et en option, filtrez toobe d’entités hello importé.</span><span class="sxs-lookup"><span data-stu-id="6bce2-228">hello Amazon DynamoDB source importer option allows you tooimport from an individual Amazon DynamoDB table and optionally filter hello entities toobe imported.</span></span> <span data-ttu-id="6bce2-229">Plusieurs modèles sont fournis pour faciliter au maximum la configuration d'une importation.</span><span class="sxs-lookup"><span data-stu-id="6bce2-229">Several templates are provided so that setting up an import is as easy as possible.</span></span>

![Capture d’écran des options sources Amazon DynamoDB - Outils de migration de base de données](./media/import-data/dynamodbsource1.png)

![Capture d’écran des options sources Amazon DynamoDB - Outils de migration de base de données](./media/import-data/dynamodbsource2.png)

<span data-ttu-id="6bce2-232">format Hello Hello chaîne de connexion Amazon DynamoDB est :</span><span class="sxs-lookup"><span data-stu-id="6bce2-232">hello format of hello Amazon DynamoDB connection string is:</span></span>

    ServiceURL=<Service Address>;AccessKey=<Access Key>;SecretKey=<Secret Key>;

> [!NOTE]
> <span data-ttu-id="6bce2-233">Utilisez hello Vérifiez commande tooensure qui hello instance Amazon DynamoDB spécifiée dans le champ de chaîne de connexion hello est accessible.</span><span class="sxs-lookup"><span data-stu-id="6bce2-233">Use hello Verify command tooensure that hello Amazon DynamoDB instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="6bce2-234">Voici une tooimport d’exemple de ligne de commande à partir d’Amazon DynamoDB :</span><span class="sxs-lookup"><span data-stu-id="6bce2-234">Here is a command line sample tooimport from Amazon DynamoDB:</span></span>

    dt.exe /s:DynamoDB /s.ConnectionString:ServiceURL=https://dynamodb.us-east-1.amazonaws.com;AccessKey=<accessKey>;SecretKey=<secretKey> /s.Request:"{   """TableName""": """ProductCatalog""" }" /t:DocumentDBBulk /t.ConnectionString:"AccountEndpoint=<Azure Cosmos DB Endpoint>;AccountKey=<Azure Cosmos DB Key>;Database=<Azure Cosmos DB Database>;" /t.Collection:catalogCollection /t.CollectionThroughput:2500

## <span data-ttu-id="6bce2-235"><a id="BlobImport"></a>fichiers tooimport à partir du stockage d’objets Blob Azure</span><span class="sxs-lookup"><span data-stu-id="6bce2-235"><a id="BlobImport"></a>tooimport files from Azure Blob storage</span></span>
<span data-ttu-id="6bce2-236">Hello fichier JSON, fichier d’exportation MongoDB et options importateur de source de fichier CSV permettent de tooimport un ou plusieurs fichiers à partir du stockage d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="6bce2-236">hello JSON file, MongoDB export file, and CSV file source importer options allow you tooimport one or more files from Azure Blob storage.</span></span> <span data-ttu-id="6bce2-237">Après avoir spécifié une URL de conteneur d’objets Blob et de la clé de compte, il suffit de fournir un tooimport de fichier (s) de hello tooselect expression régulière.</span><span class="sxs-lookup"><span data-stu-id="6bce2-237">After specifying a Blob container URL and Account Key, simply provide a regular expression tooselect hello file(s) tooimport.</span></span>

![Capture d’écran des options sources du fichier blob](./media/import-data/blobsource.png)

<span data-ttu-id="6bce2-239">Voici les fichiers de ligne de commande exemple tooimport JSON à partir du stockage d’objets Blob Azure :</span><span class="sxs-lookup"><span data-stu-id="6bce2-239">Here is command line sample tooimport JSON files from Azure Blob storage:</span></span>

    dt.exe /s:JsonFile /s.Files:"blobs://<account key>@account.blob.core.windows.net:443/importcontainer/.*" /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:doctest

## <span data-ttu-id="6bce2-240"><a id="DocumentDBSource"></a>tooimport à partir d’une collection de l’API de DocumentDB de base de données Azure Cosmos</span><span class="sxs-lookup"><span data-stu-id="6bce2-240"><a id="DocumentDBSource"></a>tooimport from an Azure Cosmos DB DocumentDB API collection</span></span>
<span data-ttu-id="6bce2-241">Hello, option de base de données Azure Cosmos source importateur vous permet de tooimport des données à partir d’une ou plusieurs collections de base de données Azure Cosmos et en option, filtrez les documents à l’aide d’une requête.</span><span class="sxs-lookup"><span data-stu-id="6bce2-241">hello Azure Cosmos DB source importer option allows you tooimport data from one or more Azure Cosmos DB collections and optionally filter documents using a query.</span></span>  

![Capture d’écran des options sources d’Azure Cosmos DB](./media/import-data/documentdbsource.png)

<span data-ttu-id="6bce2-243">format Hello Hello chaîne de connexion de base de données Azure Cosmos est :</span><span class="sxs-lookup"><span data-stu-id="6bce2-243">hello format of hello Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="6bce2-244">Hello chaîne de connexion de compte de base de données Azure Cosmos peut être récupéré à partir du Panneau de clés hello Hello portail Azure, comme décrit dans [comment toomanage un compte de base de données Azure Cosmos](manage-account.md)toutefois hello le nom de base de données hello doit toobe ajouté toohello chaîne de connexion dans hello suivant le format :</span><span class="sxs-lookup"><span data-stu-id="6bce2-244">hello Azure Cosmos DB account connection string can be retrieved from hello Keys blade of hello Azure portal, as described in [How toomanage an Azure Cosmos DB account](manage-account.md), however hello name of hello database needs toobe appended toohello connection string in hello following format:</span></span>

    Database=<CosmosDB Database>;

> [!NOTE]
> <span data-ttu-id="6bce2-245">Utilisez hello Vérifiez commande tooensure qui hello l’instance de base de données Azure Cosmos spécifiée dans le champ de chaîne de connexion hello est accessible.</span><span class="sxs-lookup"><span data-stu-id="6bce2-245">Use hello Verify command tooensure that hello Azure Cosmos DB instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="6bce2-246">tooimport à partir d’une collection de base de données Azure Cosmos unique, entrez le nom hello de collection hello à partir de laquelle les données seront importées.</span><span class="sxs-lookup"><span data-stu-id="6bce2-246">tooimport from a single Azure Cosmos DB collection, enter hello name of hello collection from which data will be imported.</span></span> <span data-ttu-id="6bce2-247">tooimport provenant de plusieurs collections de base de données Azure Cosmos, fournir une expression régulière de toomatch un ou plusieurs noms de collection (par exemple, collection01 | collection02 | collection03).</span><span class="sxs-lookup"><span data-stu-id="6bce2-247">tooimport from multiple Azure Cosmos DB collections, provide a regular expression toomatch one or more collection names (e.g. collection01 | collection02 | collection03).</span></span> <span data-ttu-id="6bce2-248">Vous pouvez éventuellement spécifier, ou fournir un fichier pour un filtre de requête de tooboth et forme hello toobe de données importée.</span><span class="sxs-lookup"><span data-stu-id="6bce2-248">You may optionally specify, or provide a file for, a query tooboth filter and shape hello data toobe imported.</span></span>

> [!NOTE]
> <span data-ttu-id="6bce2-249">Étant donné que le champ de regroupement hello accepte des expressions régulières, si vous importez à partir d’une collection unique dont le nom contient des caractères de l’expression régulière, ces caractères doivent être échappés en conséquence.</span><span class="sxs-lookup"><span data-stu-id="6bce2-249">Since hello collection field accepts regular expressions, if you are importing from a single collection whose name contains regular expression characters, then those characters must be escaped accordingly.</span></span>
> 
> 

<span data-ttu-id="6bce2-250">Hello, option de base de données Azure Cosmos source importateur a des options avancées suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="6bce2-250">hello Azure Cosmos DB source importer option has hello following advanced options:</span></span>

1. <span data-ttu-id="6bce2-251">Inclure les champs internes : Spécifie ou non les propriétés de système de document de base de données Azure Cosmos tooinclude Bonjour exporter (par exemple, _rid, _ts).</span><span class="sxs-lookup"><span data-stu-id="6bce2-251">Include Internal Fields: Specifies whether or not tooinclude Azure Cosmos DB document system properties in hello export (e.g. _rid, _ts).</span></span>
2. <span data-ttu-id="6bce2-252">Nombre de tentatives en cas d’échec : Spécifie le nombre de hello de tooretry hello connexion tooAzure Cosmos DB en cas de défaillances temporaires (par exemple, une interruption de connexion de réseau).</span><span class="sxs-lookup"><span data-stu-id="6bce2-252">Number of Retries on Failure: Specifies hello number of times tooretry hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
3. <span data-ttu-id="6bce2-253">Intervalle avant nouvelle tentative : Spécifie la durée pendant laquelle toowait nouvelles tentatives hello connexion tooAzure Cosmos DB en cas de défaillances temporaires (par exemple, une interruption de connexion de réseau).</span><span class="sxs-lookup"><span data-stu-id="6bce2-253">Retry Interval: Specifies how long toowait between retrying hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
4. <span data-ttu-id="6bce2-254">Mode de connexion : Spécifie toouse de mode de connexion hello avec la base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="6bce2-254">Connection Mode: Specifies hello connection mode toouse with Azure Cosmos DB.</span></span> <span data-ttu-id="6bce2-255">les choix disponibles Hello sont DirectTcp, DirectHttps et la passerelle.</span><span class="sxs-lookup"><span data-stu-id="6bce2-255">hello available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="6bce2-256">modes de connexion directe Hello sont plus rapides, lorsque le mode de passerelle hello est pare-feu plus convivial car elle utilise uniquement le port 443.</span><span class="sxs-lookup"><span data-stu-id="6bce2-256">hello direct connection modes are faster, while hello gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Capture d’écran des options sources avancées d’Azure Cosmos DB](./media/import-data/documentdbsourceoptions.png)

> [!TIP]
> <span data-ttu-id="6bce2-258">Hello importation outil par défaut tooconnection DirectTcp.</span><span class="sxs-lookup"><span data-stu-id="6bce2-258">hello import tool defaults tooconnection mode DirectTcp.</span></span> <span data-ttu-id="6bce2-259">Si vous rencontrez des problèmes liés au pare-feu, changez de mode de tooconnection passerelle, car il ne nécessite que le port 443.</span><span class="sxs-lookup"><span data-stu-id="6bce2-259">If you experience firewall issues, switch tooconnection mode Gateway, as it only requires port 443.</span></span>
> 
> 

<span data-ttu-id="6bce2-260">Voici certains tooimport d’exemples de ligne de commande à partir de la base de données Azure Cosmos :</span><span class="sxs-lookup"><span data-stu-id="6bce2-260">Here are some command line samples tooimport from Azure Cosmos DB:</span></span>

    #Migrate data from one Azure Cosmos DB collection tooanother Azure Cosmos DB collections
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:TEColl /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:TESessions /t.CollectionThroughput:2500

    #Migrate data from multiple Azure Cosmos DB collections tooa single Azure Cosmos DB collection
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:comp1|comp2|comp3|comp4 /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:singleCollection /t.CollectionThroughput:2500

    #Export an Azure Cosmos DB collection tooa JSON file
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:StoresSub /t:JsonFile /t.File:StoresExport.json /t.Overwrite /t.CollectionThroughput:2500

> [!TIP]
> <span data-ttu-id="6bce2-261">Hello, outil d’importation Azure Cosmos DB données prend également en charge l’importation des données de hello [Azure Cosmos DB émulateur](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="6bce2-261">hello Azure Cosmos DB Data Import Tool also supports import of data from hello [Azure Cosmos DB Emulator](local-emulator.md).</span></span> <span data-ttu-id="6bce2-262">Lorsque vous importez des données à partir d’un émulateur local, définir de point de terminaison hello trop`https://localhost:<port>`.</span><span class="sxs-lookup"><span data-stu-id="6bce2-262">When importing data from a local emulator, set hello endpoint too`https://localhost:<port>`.</span></span> 
> 
> 

## <span data-ttu-id="6bce2-263"><a id="HBaseSource"></a>tooimport dans HBase</span><span class="sxs-lookup"><span data-stu-id="6bce2-263"><a id="HBaseSource"></a>tooimport from HBase</span></span>
<span data-ttu-id="6bce2-264">Hello, option d’importateur HBase source vous permet de tooimport des données à partir d’une table HBase et en option, filtrez les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="6bce2-264">hello HBase source importer option allows you tooimport data from an HBase table and optionally filter hello data.</span></span> <span data-ttu-id="6bce2-265">Plusieurs modèles sont fournis pour faciliter au maximum la configuration d'une importation.</span><span class="sxs-lookup"><span data-stu-id="6bce2-265">Several templates are provided so that setting up an import is as easy as possible.</span></span>

![Capture d’écran des options sources HBase](./media/import-data/hbasesource1.png)

![Capture d’écran des options sources HBase](./media/import-data/hbasesource2.png)

<span data-ttu-id="6bce2-268">format Hello Hello chaîne de connexion HBase Stargate est :</span><span class="sxs-lookup"><span data-stu-id="6bce2-268">hello format of hello HBase Stargate connection string is:</span></span>

    ServiceURL=<server-address>;Username=<username>;Password=<password>

> [!NOTE]
> <span data-ttu-id="6bce2-269">Utilisez hello Vérifiez commande tooensure qui hello instance HBase spécifiée dans le champ de chaîne de connexion hello est accessible.</span><span class="sxs-lookup"><span data-stu-id="6bce2-269">Use hello Verify command tooensure that hello HBase instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="6bce2-270">Voici une tooimport d’exemple de ligne de commande à partir de HBase :</span><span class="sxs-lookup"><span data-stu-id="6bce2-270">Here is a command line sample tooimport from HBase:</span></span>

    dt.exe /s:HBase /s.ConnectionString:ServiceURL=<server-address>;Username=<username>;Password=<password> /s.Table:Contacts /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:hbaseimport

## <span data-ttu-id="6bce2-271"><a id="DocumentDBBulkTarget"></a>tooimport toohello DocumentDB API (d’importation en bloc)</span><span class="sxs-lookup"><span data-stu-id="6bce2-271"><a id="DocumentDBBulkTarget"></a>tooimport toohello DocumentDB API (Bulk Import)</span></span>
<span data-ttu-id="6bce2-272">importateur de base de données en bloc Cosmos de Azure Hello vous permet de tooimport à partir d’une des options de source disponible hello, à l’aide d’une procédure de base de données Cosmos Azure stockée par souci d’efficacité.</span><span class="sxs-lookup"><span data-stu-id="6bce2-272">hello Azure Cosmos DB Bulk importer allows you tooimport from any of hello available source options, using an Azure Cosmos DB stored procedure for efficiency.</span></span> <span data-ttu-id="6bce2-273">outil de Hello prend en charge la collection de base de données Azure Cosmos partitionnée unique d’importation tooone, ainsi que d’importation partitionnée par laquelle les données sont partitionnées sur plusieurs collections de base de données Azure Cosmos partitionnée unique.</span><span class="sxs-lookup"><span data-stu-id="6bce2-273">hello tool supports import tooone single-partitioned Azure Cosmos DB collection, as well as sharded import whereby data is partitioned across multiple single-partitioned Azure Cosmos DB collections.</span></span> <span data-ttu-id="6bce2-274">Pour plus d’informations sur le partitionnement de données, consultez [Partitionnement et mise à l’échelle dans Azure Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="6bce2-274">For more information about partitioning data, see [Partitioning and scaling in Azure Cosmos DB](partition-data.md).</span></span> <span data-ttu-id="6bce2-275">outil de Hello créer, exécuter et supprimer puis procédure stockée hello hello cible regroupements.</span><span class="sxs-lookup"><span data-stu-id="6bce2-275">hello tool will create, execute, and then delete hello stored procedure from hello target collection(s).</span></span>  

![Capture d’écran des options de bloc d’Azure Cosmos DB](./media/import-data/documentdbbulk.png)

<span data-ttu-id="6bce2-277">format Hello Hello chaîne de connexion de base de données Azure Cosmos est :</span><span class="sxs-lookup"><span data-stu-id="6bce2-277">hello format of hello Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="6bce2-278">Hello chaîne de connexion de compte de base de données Azure Cosmos peut être récupéré à partir du Panneau de clés hello Hello portail Azure, comme décrit dans [comment toomanage un compte de base de données Azure Cosmos](manage-account.md)toutefois hello le nom de base de données hello doit toobe ajouté toohello chaîne de connexion dans hello suivant le format :</span><span class="sxs-lookup"><span data-stu-id="6bce2-278">hello Azure Cosmos DB account connection string can be retrieved from hello Keys blade of hello Azure portal, as described in [How toomanage an Azure Cosmos DB account](manage-account.md), however hello name of hello database needs toobe appended toohello connection string in hello following format:</span></span>

    Database=<CosmosDB Database>;

> [!NOTE]
> <span data-ttu-id="6bce2-279">Utilisez hello Vérifiez commande tooensure qui hello l’instance de base de données Azure Cosmos spécifiée dans le champ de chaîne de connexion hello est accessible.</span><span class="sxs-lookup"><span data-stu-id="6bce2-279">Use hello Verify command tooensure that hello Azure Cosmos DB instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="6bce2-280">tooimport tooa collection en une seule, entrez le nom hello de hello collection toowhich données seront importées et cliquez sur le bouton Ajouter de hello.</span><span class="sxs-lookup"><span data-stu-id="6bce2-280">tooimport tooa single collection, enter hello name of hello collection toowhich data will be imported and click hello Add button.</span></span> <span data-ttu-id="6bce2-281">tooimport toomultiple collections, spécifiez le nom de chaque collection individuellement ou hello suivant de syntaxe toospecify plusieurs collections : *collection_prefix*[index - index de fin de début].</span><span class="sxs-lookup"><span data-stu-id="6bce2-281">tooimport toomultiple collections, either enter each collection name individually or use hello following syntax toospecify multiple collections: *collection_prefix*[start index - end index].</span></span> <span data-ttu-id="6bce2-282">Lorsque vous spécifiez plusieurs collections via la syntaxe de susmentionnés hello, gardez les points suivants hello à l’esprit :</span><span class="sxs-lookup"><span data-stu-id="6bce2-282">When specifying multiple collections via hello aforementioned syntax, keep hello following in mind:</span></span>

1. <span data-ttu-id="6bce2-283">Seuls les modèles de nom de plage de nombres entiers sont pris en charge.</span><span class="sxs-lookup"><span data-stu-id="6bce2-283">Only integer range name patterns are supported.</span></span> <span data-ttu-id="6bce2-284">Par exemple, la spécification de regroupement [0-3] produira hello suivant des collections : collection0 collection1, collection2, collection3.</span><span class="sxs-lookup"><span data-stu-id="6bce2-284">For example, specifying collection[0-3] will produce hello following collections: collection0, collection1, collection2, collection3.</span></span>
2. <span data-ttu-id="6bce2-285">Vous pouvez utiliser une syntaxe abrégée : collection[3], qui émet le même jeu de collections que celui mentionné à l'étape 1.</span><span class="sxs-lookup"><span data-stu-id="6bce2-285">You can use an abbreviated syntax: collection[3] will emit same set of collections mentioned in step 1.</span></span>
3. <span data-ttu-id="6bce2-286">Plusieurs substitutions peuvent être fournies.</span><span class="sxs-lookup"><span data-stu-id="6bce2-286">More than one substitution can be provided.</span></span> <span data-ttu-id="6bce2-287">Par exemple, collection[0-1] [0-9] génère 20 noms de collection avec des zéros non significatifs (collection01, ..02, ..03).</span><span class="sxs-lookup"><span data-stu-id="6bce2-287">For example, collection[0-1] [0-9] will generate 20 collection names with leading zeros (collection01, ..02, ..03).</span></span>

<span data-ttu-id="6bce2-288">Une fois hello ou les noms de collection ont été spécifiées, choisissez le débit souhaité de hello de collections de hello (400 RUs too10, 000 RUs).</span><span class="sxs-lookup"><span data-stu-id="6bce2-288">Once hello collection name(s) have been specified, choose hello desired throughput of hello collection(s) (400 RUs too10,000 RUs).</span></span> <span data-ttu-id="6bce2-289">Pour de meilleures performances d’importation, choisissez un débit plus élevé.</span><span class="sxs-lookup"><span data-stu-id="6bce2-289">For best import performance, choose a higher throughput.</span></span> <span data-ttu-id="6bce2-290">Pour plus d’informations sur les niveaux de performances, consultez les [niveaux de performances d’Azure Cosmos DB](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="6bce2-290">For more information about performance levels, see [Performance levels in Azure Cosmos DB](performance-levels.md).</span></span>

> [!NOTE]
> <span data-ttu-id="6bce2-291">paramètre de débit de performance Hello s’applique uniquement à la création de toocollection.</span><span class="sxs-lookup"><span data-stu-id="6bce2-291">hello performance throughput setting only applies toocollection creation.</span></span> <span data-ttu-id="6bce2-292">Si hello spécifié de la collection existe déjà, son débit n’est pas modifiée.</span><span class="sxs-lookup"><span data-stu-id="6bce2-292">If hello specified collection already exists, its throughput will not be modified.</span></span>
> 
> 

<span data-ttu-id="6bce2-293">Lorsque vous importez des collections de toomultiple, outil d’importation hello prend en charge le partitionnement par hachage en fonction.</span><span class="sxs-lookup"><span data-stu-id="6bce2-293">When importing toomultiple collections, hello import tool supports hash based sharding.</span></span> <span data-ttu-id="6bce2-294">Dans ce scénario, spécifiez la propriété de document hello vous souhaitez toouse comme clé de Partition de hello (si la clé de Partition est vide, documents seront partitionnées au hasard entre les collections de cible hello).</span><span class="sxs-lookup"><span data-stu-id="6bce2-294">In this scenario, specify hello document property you wish toouse as hello Partition Key (if Partition Key is left blank, documents will be sharded randomly across hello target collections).</span></span>

<span data-ttu-id="6bce2-295">Vous pouvez éventuellement spécifier quel champ de la source d’importation hello doit être utilisé en tant que propriété d’id de document de base de données Azure Cosmos de hello pendant l’importation hello (Notez que si les documents ne contiennent pas cette propriété, puis outil d’importation hello génère un GUID en tant que valeur de la propriété id hello).</span><span class="sxs-lookup"><span data-stu-id="6bce2-295">You may optionally specify which field in hello import source should be used as hello Azure Cosmos DB document id property during hello import (note that if documents do not contain this property, then hello import tool will generate a GUID as hello id property value).</span></span>

<span data-ttu-id="6bce2-296">De nombreuses options avancées sont disponibles lors de l'importation.</span><span class="sxs-lookup"><span data-stu-id="6bce2-296">There are a number of advanced options available during import.</span></span> <span data-ttu-id="6bce2-297">Tout d’abord, tandis que l’outil de hello inclut un bloc par défaut importer une procédure stockée (BulkInsert.js), vous pouvez toospecify votre propre procédure d’importation stockée :</span><span class="sxs-lookup"><span data-stu-id="6bce2-297">First, while hello tool includes a default bulk import stored procedure (BulkInsert.js), you may choose toospecify your own import stored procedure:</span></span>

 ![Capture d’écran de l’option sproc d’insertion de bloc Azure Cosmos DB](./media/import-data/bulkinsertsp.png)

<span data-ttu-id="6bce2-299">De plus, lorsque vous importez des types de date (par exemple, depuis SQL Server ou MongoDB), vous pouvez choisir entre trois options d'importation :</span><span class="sxs-lookup"><span data-stu-id="6bce2-299">Additionally, when importing date types (e.g. from SQL Server or MongoDB), you can choose between three import options:</span></span>

 ![Capture d’écran des options d’importation de date et d’heure Azure Cosmos DB](./media/import-data/datetimeoptions.png)

* <span data-ttu-id="6bce2-301">Chaîne : conserver en tant que valeur de chaîne</span><span class="sxs-lookup"><span data-stu-id="6bce2-301">String: Persist as a string value</span></span>
* <span data-ttu-id="6bce2-302">Epoch : conserver en tant que valeur numérique Epoch</span><span class="sxs-lookup"><span data-stu-id="6bce2-302">Epoch: Persist as an Epoch number value</span></span>
* <span data-ttu-id="6bce2-303">Les deux : conserver la chaîne et les valeurs numériques Epoch</span><span class="sxs-lookup"><span data-stu-id="6bce2-303">Both: Persist both string and Epoch number values.</span></span> <span data-ttu-id="6bce2-304">Cette option crée un sous-document, par exemple : « date_joined » : {« Valeur »: « 2013-10-21T21:17:25.2410000Z », « Epoch » : 1382390245}</span><span class="sxs-lookup"><span data-stu-id="6bce2-304">This option will create a subdocument, for example: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span></span>

<span data-ttu-id="6bce2-305">importateur de base de données en bloc Cosmos de Azure Hello a hello autres options avancées suivantes :</span><span class="sxs-lookup"><span data-stu-id="6bce2-305">hello Azure Cosmos DB Bulk importer has hello following additional advanced options:</span></span>

1. <span data-ttu-id="6bce2-306">Taille du lot : hello outil par défaut tooa taille de lot de 50.</span><span class="sxs-lookup"><span data-stu-id="6bce2-306">Batch Size: hello tool defaults tooa batch size of 50.</span></span>  <span data-ttu-id="6bce2-307">Si toobe de documents hello importé est volumineux, envisagez de réduire la taille de lot hello.</span><span class="sxs-lookup"><span data-stu-id="6bce2-307">If hello documents toobe imported are large, consider lowering hello batch size.</span></span> <span data-ttu-id="6bce2-308">À l’inverse, si toobe de documents hello importé est petit, envisagez d’augmenter la taille de lot hello.</span><span class="sxs-lookup"><span data-stu-id="6bce2-308">Conversely, if hello documents toobe imported are small, consider raising hello batch size.</span></span>
2. <span data-ttu-id="6bce2-309">Taille de Script maximale (octets) : outil de hello par défaut est la taille de script max tooa de 512 Ko</span><span class="sxs-lookup"><span data-stu-id="6bce2-309">Max Script Size (bytes): hello tool defaults tooa max script size of 512KB</span></span>
3. <span data-ttu-id="6bce2-310">Désactiver la génération automatique de code : Si chaque toobe document importée contient un champ d’id, puis en sélectionnant cette option peut augmenter les performances.</span><span class="sxs-lookup"><span data-stu-id="6bce2-310">Disable Automatic Id Generation: If every document toobe imported contains an id field, then selecting this option can increase performance.</span></span> <span data-ttu-id="6bce2-311">Les documents avec un champ d’ID unique manquant ne seront pas importés.</span><span class="sxs-lookup"><span data-stu-id="6bce2-311">Documents missing a unique id field will not be imported.</span></span>
4. <span data-ttu-id="6bce2-312">Mise à jour des Documents existants : hello outil toonot de valeurs par défaut en remplaçant les documents existants avec l’id est en conflit.</span><span class="sxs-lookup"><span data-stu-id="6bce2-312">Update Existing Documents: hello tool defaults toonot replacing existing documents with id conflicts.</span></span> <span data-ttu-id="6bce2-313">Cette option permettra de remplacer les documents existants par les ID correspondants.</span><span class="sxs-lookup"><span data-stu-id="6bce2-313">Selecting this option will allow overwriting existing documents with matching ids.</span></span> <span data-ttu-id="6bce2-314">Cette fonctionnalité est utile pour les migrations de données planifiées qui mettent à jour des documents existants.</span><span class="sxs-lookup"><span data-stu-id="6bce2-314">This feature is useful for scheduled data migrations that update existing documents.</span></span>
5. <span data-ttu-id="6bce2-315">Nombre de tentatives en cas d’échec : Spécifie le nombre de hello de tooretry hello connexion tooAzure Cosmos DB en cas de défaillances temporaires (par exemple, une interruption de connexion de réseau).</span><span class="sxs-lookup"><span data-stu-id="6bce2-315">Number of Retries on Failure: Specifies hello number of times tooretry hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
6. <span data-ttu-id="6bce2-316">Intervalle avant nouvelle tentative : Spécifie la durée pendant laquelle toowait nouvelles tentatives hello connexion tooAzure Cosmos DB en cas de défaillances temporaires (par exemple, une interruption de connexion de réseau).</span><span class="sxs-lookup"><span data-stu-id="6bce2-316">Retry Interval: Specifies how long toowait between retrying hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
7. <span data-ttu-id="6bce2-317">Mode de connexion : Spécifie toouse de mode de connexion hello avec la base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="6bce2-317">Connection Mode: Specifies hello connection mode toouse with Azure Cosmos DB.</span></span> <span data-ttu-id="6bce2-318">les choix disponibles Hello sont DirectTcp, DirectHttps et la passerelle.</span><span class="sxs-lookup"><span data-stu-id="6bce2-318">hello available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="6bce2-319">modes de connexion directe Hello sont plus rapides, lorsque le mode de passerelle hello est pare-feu plus convivial car elle utilise uniquement le port 443.</span><span class="sxs-lookup"><span data-stu-id="6bce2-319">hello direct connection modes are faster, while hello gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Capture d’écran des options d’importation en bloc avancées d’Azure Cosmos DB](./media/import-data/docdbbulkoptions.png)

> [!TIP]
> <span data-ttu-id="6bce2-321">Hello importation outil par défaut tooconnection DirectTcp.</span><span class="sxs-lookup"><span data-stu-id="6bce2-321">hello import tool defaults tooconnection mode DirectTcp.</span></span> <span data-ttu-id="6bce2-322">Si vous rencontrez des problèmes liés au pare-feu, changez de mode de tooconnection passerelle, car il ne nécessite que le port 443.</span><span class="sxs-lookup"><span data-stu-id="6bce2-322">If you experience firewall issues, switch tooconnection mode Gateway, as it only requires port 443.</span></span>
> 
> 

## <span data-ttu-id="6bce2-323"><a id="DocumentDBSeqTarget"></a>tooimport toohello DocumentDB API (importation d’enregistrements séquentiel)</span><span class="sxs-lookup"><span data-stu-id="6bce2-323"><a id="DocumentDBSeqTarget"></a>tooimport toohello DocumentDB API (Sequential Record Import)</span></span>
<span data-ttu-id="6bce2-324">importateur de séquentiel d’enregistrement de base de données Azure Cosmos Hello vous permet de tooimport à partir d’une des options de source disponible hello chaque enregistrement par enregistrement.</span><span class="sxs-lookup"><span data-stu-id="6bce2-324">hello Azure Cosmos DB sequential record importer allows you tooimport from any of hello available source options on a record by record basis.</span></span> <span data-ttu-id="6bce2-325">Vous pouvez choisir cette option si vous importez un regroupement existant tooan qui a atteint son quota de procédures stockées.</span><span class="sxs-lookup"><span data-stu-id="6bce2-325">You might choose this option if you’re importing tooan existing collection that has reached its quota of stored procedures.</span></span> <span data-ttu-id="6bce2-326">tooa d’importation Hello outil prend en charge une seule collection de base de données Azure Cosmos (partition unique et plusieurs partition), ainsi que d’importation partitionnée par laquelle les données sont partitionnées sur plusieurs collections de base de données Azure Cosmos à partition unique ou plusieurs partitions.</span><span class="sxs-lookup"><span data-stu-id="6bce2-326">hello tool supports import tooa single (both single-partition and multi-partition) Azure Cosmos DB collection, as well as sharded import whereby data is partitioned across multiple single-partition and/or multi-partition Azure Cosmos DB collections.</span></span> <span data-ttu-id="6bce2-327">Pour plus d’informations sur le partitionnement de données, consultez [Partitionnement et mise à l’échelle dans Azure Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="6bce2-327">For more information about partitioning data, see [Partitioning and scaling in Azure Cosmos DB](partition-data.md).</span></span>

![Capture d’écran des options d’importation d’enregistrement séquentiel d’Azure Cosmos DB](./media/import-data/documentdbsequential.png)

<span data-ttu-id="6bce2-329">format Hello Hello chaîne de connexion de base de données Azure Cosmos est :</span><span class="sxs-lookup"><span data-stu-id="6bce2-329">hello format of hello Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="6bce2-330">Hello chaîne de connexion de compte de base de données Azure Cosmos peut être récupéré à partir du Panneau de clés hello Hello portail Azure, comme décrit dans [comment toomanage un compte de base de données Azure Cosmos](manage-account.md)toutefois hello le nom de base de données hello doit toobe ajouté toohello chaîne de connexion dans hello suivant le format :</span><span class="sxs-lookup"><span data-stu-id="6bce2-330">hello Azure Cosmos DB account connection string can be retrieved from hello Keys blade of hello Azure portal, as described in [How toomanage an Azure Cosmos DB account](manage-account.md), however hello name of hello database needs toobe appended toohello connection string in hello following format:</span></span>

    Database=<Azure Cosmos DB Database>;

> [!NOTE]
> <span data-ttu-id="6bce2-331">Utilisez hello Vérifiez commande tooensure qui hello l’instance de base de données Azure Cosmos spécifiée dans le champ de chaîne de connexion hello est accessible.</span><span class="sxs-lookup"><span data-stu-id="6bce2-331">Use hello Verify command tooensure that hello Azure Cosmos DB instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="6bce2-332">tooimport tooa collection en une seule, entrez le nom hello de hello collection toowhich données seront importées et cliquez sur le bouton Ajouter de hello.</span><span class="sxs-lookup"><span data-stu-id="6bce2-332">tooimport tooa single collection, enter hello name of hello collection toowhich data will be imported and click hello Add button.</span></span> <span data-ttu-id="6bce2-333">tooimport toomultiple collections, spécifiez le nom de chaque collection individuellement ou hello suivant de syntaxe toospecify plusieurs collections : *collection_prefix*[index - index de fin de début].</span><span class="sxs-lookup"><span data-stu-id="6bce2-333">tooimport toomultiple collections, either enter each collection name individually or use hello following syntax toospecify multiple collections: *collection_prefix*[start index - end index].</span></span> <span data-ttu-id="6bce2-334">Lorsque vous spécifiez plusieurs collections via la syntaxe de susmentionnés hello, gardez les points suivants hello à l’esprit :</span><span class="sxs-lookup"><span data-stu-id="6bce2-334">When specifying multiple collections via hello aforementioned syntax, keep hello following in mind:</span></span>

1. <span data-ttu-id="6bce2-335">Seuls les modèles de nom de plage de nombres entiers sont pris en charge.</span><span class="sxs-lookup"><span data-stu-id="6bce2-335">Only integer range name patterns are supported.</span></span> <span data-ttu-id="6bce2-336">Par exemple, la spécification de regroupement [0-3] produira hello suivant des collections : collection0 collection1, collection2, collection3.</span><span class="sxs-lookup"><span data-stu-id="6bce2-336">For example, specifying collection[0-3] will produce hello following collections: collection0, collection1, collection2, collection3.</span></span>
2. <span data-ttu-id="6bce2-337">Vous pouvez utiliser une syntaxe abrégée : collection[3], qui émet le même jeu de collections que celui mentionné à l'étape 1.</span><span class="sxs-lookup"><span data-stu-id="6bce2-337">You can use an abbreviated syntax: collection[3] will emit same set of collections mentioned in step 1.</span></span>
3. <span data-ttu-id="6bce2-338">Plusieurs substitutions peuvent être fournies.</span><span class="sxs-lookup"><span data-stu-id="6bce2-338">More than one substitution can be provided.</span></span> <span data-ttu-id="6bce2-339">Par exemple, collection[0-1] [0-9] génère 20 noms de collection avec des zéros non significatifs (collection01, ..02, ..03).</span><span class="sxs-lookup"><span data-stu-id="6bce2-339">For example, collection[0-1] [0-9] will generate 20 collection names with leading zeros (collection01, ..02, ..03).</span></span>

<span data-ttu-id="6bce2-340">Une fois hello ou les noms de collection ont été spécifiées, choisissez le débit souhaité de hello de collections de hello (400 RUs too250, 000 RUs).</span><span class="sxs-lookup"><span data-stu-id="6bce2-340">Once hello collection name(s) have been specified, choose hello desired throughput of hello collection(s) (400 RUs too250,000 RUs).</span></span> <span data-ttu-id="6bce2-341">Pour de meilleures performances d’importation, choisissez un débit plus élevé.</span><span class="sxs-lookup"><span data-stu-id="6bce2-341">For best import performance, choose a higher throughput.</span></span> <span data-ttu-id="6bce2-342">Pour plus d’informations sur les niveaux de performances, consultez les [niveaux de performances d’Azure Cosmos DB](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="6bce2-342">For more information about performance levels, see [Performance levels in Azure Cosmos DB](performance-levels.md).</span></span> <span data-ttu-id="6bce2-343">Toute importation toocollections avec un débit > 10 000 RUs nécessite une clé de partition.</span><span class="sxs-lookup"><span data-stu-id="6bce2-343">Any import toocollections with throughput >10,000 RUs will require a partition key.</span></span> <span data-ttu-id="6bce2-344">Si vous choisissez toohave RUs plus de 250 000, vous devez toofile une demande dans toohave de portail hello augmentée de votre compte.</span><span class="sxs-lookup"><span data-stu-id="6bce2-344">If you choose toohave more than 250,000 RUs, you will need toofile a request in hello portal toohave your account increased.</span></span>

> [!NOTE]
> <span data-ttu-id="6bce2-345">paramètre de débit Hello s’applique uniquement à la création de toocollection.</span><span class="sxs-lookup"><span data-stu-id="6bce2-345">hello throughput setting only applies toocollection creation.</span></span> <span data-ttu-id="6bce2-346">Si hello spécifié de la collection existe déjà, son débit n’est pas modifiée.</span><span class="sxs-lookup"><span data-stu-id="6bce2-346">If hello specified collection already exists, its throughput will not be modified.</span></span>
> 
> 

<span data-ttu-id="6bce2-347">Lorsque vous importez des collections de toomultiple, outil d’importation hello prend en charge le partitionnement par hachage en fonction.</span><span class="sxs-lookup"><span data-stu-id="6bce2-347">When importing toomultiple collections, hello import tool supports hash based sharding.</span></span> <span data-ttu-id="6bce2-348">Dans ce scénario, spécifiez la propriété de document hello vous souhaitez toouse comme clé de Partition de hello (si la clé de Partition est vide, documents seront partitionnées au hasard entre les collections de cible hello).</span><span class="sxs-lookup"><span data-stu-id="6bce2-348">In this scenario, specify hello document property you wish toouse as hello Partition Key (if Partition Key is left blank, documents will be sharded randomly across hello target collections).</span></span>

<span data-ttu-id="6bce2-349">Vous pouvez éventuellement spécifier quel champ de la source d’importation hello doit être utilisé en tant que propriété d’id de document de base de données Azure Cosmos de hello pendant l’importation hello (Notez que si les documents ne contiennent pas cette propriété, puis outil d’importation hello génère un GUID en tant que valeur de la propriété id hello).</span><span class="sxs-lookup"><span data-stu-id="6bce2-349">You may optionally specify which field in hello import source should be used as hello Azure Cosmos DB document id property during hello import (note that if documents do not contain this property, then hello import tool will generate a GUID as hello id property value).</span></span>

<span data-ttu-id="6bce2-350">De nombreuses options avancées sont disponibles lors de l'importation.</span><span class="sxs-lookup"><span data-stu-id="6bce2-350">There are a number of advanced options available during import.</span></span> <span data-ttu-id="6bce2-351">Tout d’abord, lorsque vous importez des types de date (par exemple, depuis SQL Server ou MongoDB), vous pouvez choisir entre trois options d'importation :</span><span class="sxs-lookup"><span data-stu-id="6bce2-351">First, when importing date types (e.g. from SQL Server or MongoDB), you can choose between three import options:</span></span>

 ![Capture d’écran des options d’importation de date et d’heure Azure Cosmos DB](./media/import-data/datetimeoptions.png)

* <span data-ttu-id="6bce2-353">Chaîne : conserver en tant que valeur de chaîne</span><span class="sxs-lookup"><span data-stu-id="6bce2-353">String: Persist as a string value</span></span>
* <span data-ttu-id="6bce2-354">Epoch : conserver en tant que valeur numérique Epoch</span><span class="sxs-lookup"><span data-stu-id="6bce2-354">Epoch: Persist as an Epoch number value</span></span>
* <span data-ttu-id="6bce2-355">Les deux : conserver la chaîne et les valeurs numériques Epoch</span><span class="sxs-lookup"><span data-stu-id="6bce2-355">Both: Persist both string and Epoch number values.</span></span> <span data-ttu-id="6bce2-356">Cette option crée un sous-document, par exemple : « date_joined » : {« Valeur »: « 2013-10-21T21:17:25.2410000Z », « Epoch » : 1382390245}</span><span class="sxs-lookup"><span data-stu-id="6bce2-356">This option will create a subdocument, for example: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span></span>

<span data-ttu-id="6bce2-357">Bonjour Azure Cosmos DB - importateur d’enregistrement séquentiel a hello autres options avancées suivantes :</span><span class="sxs-lookup"><span data-stu-id="6bce2-357">hello Azure Cosmos DB - Sequential record importer has hello following additional advanced options:</span></span>

1. <span data-ttu-id="6bce2-358">Nombre de requêtes parallèles : outil de hello par défaut too2 les demandes parallèles.</span><span class="sxs-lookup"><span data-stu-id="6bce2-358">Number of Parallel Requests: hello tool defaults too2 parallel requests.</span></span> <span data-ttu-id="6bce2-359">Si toobe de documents hello importé est petit, envisagez d’augmenter le nombre de hello de demandes parallèles.</span><span class="sxs-lookup"><span data-stu-id="6bce2-359">If hello documents toobe imported are small, consider raising hello number of parallel requests.</span></span> <span data-ttu-id="6bce2-360">Notez que si ce nombre est élevé en trop, hello importation peut rencontrer la limitation.</span><span class="sxs-lookup"><span data-stu-id="6bce2-360">Note that if this number is raised too much, hello import may experience throttling.</span></span>
2. <span data-ttu-id="6bce2-361">Désactiver la génération automatique de code : Si chaque toobe document importée contient un champ d’id, puis en sélectionnant cette option peut augmenter les performances.</span><span class="sxs-lookup"><span data-stu-id="6bce2-361">Disable Automatic Id Generation: If every document toobe imported contains an id field, then selecting this option can increase performance.</span></span> <span data-ttu-id="6bce2-362">Les documents avec un champ d’ID unique manquant ne seront pas importés.</span><span class="sxs-lookup"><span data-stu-id="6bce2-362">Documents missing a unique id field will not be imported.</span></span>
3. <span data-ttu-id="6bce2-363">Mise à jour des Documents existants : hello outil toonot de valeurs par défaut en remplaçant les documents existants avec l’id est en conflit.</span><span class="sxs-lookup"><span data-stu-id="6bce2-363">Update Existing Documents: hello tool defaults toonot replacing existing documents with id conflicts.</span></span> <span data-ttu-id="6bce2-364">Cette option permettra de remplacer les documents existants par les ID correspondants.</span><span class="sxs-lookup"><span data-stu-id="6bce2-364">Selecting this option will allow overwriting existing documents with matching ids.</span></span> <span data-ttu-id="6bce2-365">Cette fonctionnalité est utile pour les migrations de données planifiées qui mettent à jour des documents existants.</span><span class="sxs-lookup"><span data-stu-id="6bce2-365">This feature is useful for scheduled data migrations that update existing documents.</span></span>
4. <span data-ttu-id="6bce2-366">Nombre de tentatives en cas d’échec : Spécifie le nombre de hello de tooretry hello connexion tooAzure Cosmos DB en cas de défaillances temporaires (par exemple, une interruption de connexion de réseau).</span><span class="sxs-lookup"><span data-stu-id="6bce2-366">Number of Retries on Failure: Specifies hello number of times tooretry hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
5. <span data-ttu-id="6bce2-367">Intervalle avant nouvelle tentative : Spécifie la durée pendant laquelle toowait nouvelles tentatives hello connexion tooAzure Cosmos DB en cas de défaillances temporaires (par exemple, une interruption de connexion de réseau).</span><span class="sxs-lookup"><span data-stu-id="6bce2-367">Retry Interval: Specifies how long toowait between retrying hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
6. <span data-ttu-id="6bce2-368">Mode de connexion : Spécifie toouse de mode de connexion hello avec la base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="6bce2-368">Connection Mode: Specifies hello connection mode toouse with Azure Cosmos DB.</span></span> <span data-ttu-id="6bce2-369">les choix disponibles Hello sont DirectTcp, DirectHttps et la passerelle.</span><span class="sxs-lookup"><span data-stu-id="6bce2-369">hello available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="6bce2-370">modes de connexion directe Hello sont plus rapides, lorsque le mode de passerelle hello est pare-feu plus convivial car elle utilise uniquement le port 443.</span><span class="sxs-lookup"><span data-stu-id="6bce2-370">hello direct connection modes are faster, while hello gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Capture d’écran des options d’importation d’enregistrement séquentiel avancées d’Azure Cosmos DB](./media/import-data/documentdbsequentialoptions.png)

> [!TIP]
> <span data-ttu-id="6bce2-372">Hello importation outil par défaut tooconnection DirectTcp.</span><span class="sxs-lookup"><span data-stu-id="6bce2-372">hello import tool defaults tooconnection mode DirectTcp.</span></span> <span data-ttu-id="6bce2-373">Si vous rencontrez des problèmes liés au pare-feu, changez de mode de tooconnection passerelle, car il ne nécessite que le port 443.</span><span class="sxs-lookup"><span data-stu-id="6bce2-373">If you experience firewall issues, switch tooconnection mode Gateway, as it only requires port 443.</span></span>
> 
> 

## <span data-ttu-id="6bce2-374"><a id="IndexingPolicy"></a>Spécification d’une stratégie d’indexation lors de la création de collections Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="6bce2-374"><a id="IndexingPolicy"></a>Specify an indexing policy when creating Azure Cosmos DB collections</span></span>
<span data-ttu-id="6bce2-375">Lorsque vous autorisez des collections de toocreate outil migration de hello lors de l’importation, vous pouvez spécifier la stratégie d’indexation hello des collections de hello.</span><span class="sxs-lookup"><span data-stu-id="6bce2-375">When you allow hello migration tool toocreate collections during import, you can specify hello indexing policy of hello collections.</span></span> <span data-ttu-id="6bce2-376">Bonjour avancé section options de hello Azure Cosmos DB et d’importation Azure Cosmos DB séquentiel options d’enregistrement, accédez à section de la stratégie d’indexation toohello.</span><span class="sxs-lookup"><span data-stu-id="6bce2-376">In hello advanced options section of hello Azure Cosmos DB Bulk import and Azure Cosmos DB Sequential record options, navigate toohello Indexing Policy section.</span></span>

![Capture d’écran des options de stratégie d’indexation avancées d’Azure Cosmos DB](./media/import-data/indexingpolicy1.png)

<span data-ttu-id="6bce2-378">À l’aide de hello option de stratégie d’indexation avancées, vous pouvez sélectionner un fichier de stratégie d’indexation, manuellement entrer une stratégie d’indexation ou sélectionner un jeu de modèles par défaut (en cliquant avec le bouton droit dans hello l’indexation de stratégie de zone de texte).</span><span class="sxs-lookup"><span data-stu-id="6bce2-378">Using hello Indexing Policy advanced option, you can select an indexing policy file, manually enter an indexing policy, or select from a set of default templates (by right clicking in hello indexing policy textbox).</span></span>

<span data-ttu-id="6bce2-379">les modèles de stratégie Hello hello outil fournit sont :</span><span class="sxs-lookup"><span data-stu-id="6bce2-379">hello policy templates hello tool provides are:</span></span>

* <span data-ttu-id="6bce2-380">Par défaut.</span><span class="sxs-lookup"><span data-stu-id="6bce2-380">Default.</span></span> <span data-ttu-id="6bce2-381">Cette stratégie est préférable si vous exécutez des requêtes d’efficacité sur des chaînes et des requêtes ORDER BY, de plage et d’efficacité sur des nombres.</span><span class="sxs-lookup"><span data-stu-id="6bce2-381">This policy is best when you’re performing equality queries against strings and using ORDER BY, range, and equality queries for numbers.</span></span> <span data-ttu-id="6bce2-382">Cette stratégie dispose d’une surcharge de stockage d'index inférieure à Plage.</span><span class="sxs-lookup"><span data-stu-id="6bce2-382">This policy has a lower index storage overhead than Range.</span></span>
* <span data-ttu-id="6bce2-383">Plage.</span><span class="sxs-lookup"><span data-stu-id="6bce2-383">Range.</span></span> <span data-ttu-id="6bce2-384">Cette stratégie est préférable si vous exécutez des requêtes ORDER BY, de plage et d'efficacité sur des nombres et des chaînes.</span><span class="sxs-lookup"><span data-stu-id="6bce2-384">This policy is best you’re using ORDER BY, range and equality queries on both numbers and strings.</span></span> <span data-ttu-id="6bce2-385">Cette stratégie dispose d’une surcharge de stockage d'index supérieure à Par défaut ou Hachage.</span><span class="sxs-lookup"><span data-stu-id="6bce2-385">This policy has a higher index storage overhead than Default or Hash.</span></span>

![Capture d’écran des options de stratégie d’indexation avancées d’Azure Cosmos DB](./media/import-data/indexingpolicy2.png)

> [!NOTE]
> <span data-ttu-id="6bce2-387">Si vous ne spécifiez pas une stratégie d’indexation, puis stratégie par défaut de hello sera appliquée.</span><span class="sxs-lookup"><span data-stu-id="6bce2-387">If you do not specify an indexing policy, then hello default policy will be applied.</span></span> <span data-ttu-id="6bce2-388">Pour plus d’informations sur les stratégies d’indexation, consultez [Stratégies d’indexation d’Azure Cosmos DB](indexing-policies.md).</span><span class="sxs-lookup"><span data-stu-id="6bce2-388">For more information about indexing policies, see [Azure Cosmos DB indexing policies](indexing-policies.md).</span></span>
> 
> 

## <a name="export-toojson-file"></a><span data-ttu-id="6bce2-389">Fichier d’exportation tooJSON</span><span class="sxs-lookup"><span data-stu-id="6bce2-389">Export tooJSON file</span></span>
<span data-ttu-id="6bce2-390">exportateur de JSON de base de données Azure Cosmos Hello vous permet de tooexport des hello source disponible options tooa fichier JSON qui contient un tableau des documents JSON.</span><span class="sxs-lookup"><span data-stu-id="6bce2-390">hello Azure Cosmos DB JSON exporter allows you tooexport any of hello available source options tooa JSON file that contains an array of JSON documents.</span></span> <span data-ttu-id="6bce2-391">outil de Hello gère l’exportation hello pour vous, ou vous pouvez choisir la commande de migration qui en résulte tooview hello et exécuter des commandes de hello vous-même.</span><span class="sxs-lookup"><span data-stu-id="6bce2-391">hello tool will handle hello export for you, or you can choose tooview hello resulting migration command and run hello command yourself.</span></span> <span data-ttu-id="6bce2-392">fichier JSON résultante de Hello peut-être être stockée localement ou dans le stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="6bce2-392">hello resulting JSON file may be stored locally or in Azure Blob storage.</span></span>

![Capture d’écran des options d’exportation de fichier local JSON Azure Cosmos DB](./media/import-data/jsontarget.png)

![Capture d’écran des options d’exportation du stockage blob Azure JSON Azure Cosmos DB](./media/import-data/jsontarget2.png)

<span data-ttu-id="6bce2-395">Vous pouvez éventuellement choisir hello tooprettify résultant JSON, ce qui augmente la taille hello de document résultant de hello lors de la fabrication hello contenu plus lisibles par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6bce2-395">You may optionally choose tooprettify hello resulting JSON, which will increase hello size of hello resulting document while making hello contents more human readable.</span></span>

    Standard JSON export
    [{"id":"Sample","Title":"About Paris","Language":{"Name":"English"},"Author":{"Name":"Don","Location":{"City":"Paris","Country":"France"}},"Content":"Don's document in Azure Cosmos DB is a valid JSON document as defined by hello JSON spec.","PageViews":10000,"Topics":[{"Title":"History of Paris"},{"Title":"Places toosee in Paris"}]}]

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
    "Content": "Don's document in Azure Cosmos DB is a valid JSON document as defined by hello JSON spec.",
    "PageViews": 10000,
    "Topics": [
      {
        "Title": "History of Paris"
      },
      {
        "Title": "Places toosee in Paris"
      }
    ]
    }]

## <a name="advanced-configuration"></a><span data-ttu-id="6bce2-396">Configuration avancée</span><span class="sxs-lookup"><span data-stu-id="6bce2-396">Advanced configuration</span></span>
<span data-ttu-id="6bce2-397">Dans l’écran de configuration avancée hello, spécifiez emplacement hello de hello journal fichier toowhich vous souhaitez que les erreurs écrites.</span><span class="sxs-lookup"><span data-stu-id="6bce2-397">In hello Advanced configuration screen, specify hello location of hello log file toowhich you would like any errors written.</span></span> <span data-ttu-id="6bce2-398">Hello, suivant les règles s’appliquent toothis page :</span><span class="sxs-lookup"><span data-stu-id="6bce2-398">hello following rules apply toothis page:</span></span>

1. <span data-ttu-id="6bce2-399">Si un nom de fichier n’est pas fourni, puis toutes les erreurs seront affichera sur la page de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="6bce2-399">If a file name is not provided, then all errors will be returned on hello Results page.</span></span>
2. <span data-ttu-id="6bce2-400">Si un nom de fichier est fourni sans un répertoire, puis les fichiers hello seront créée (ou remplacée) dans l’annuaire d’environnement actuelle hello.</span><span class="sxs-lookup"><span data-stu-id="6bce2-400">If a file name is provided without a directory, then hello file will be created (or overwritten) in hello current environment directory.</span></span>
3. <span data-ttu-id="6bce2-401">Si vous sélectionnez un existant seront remplacé le fichier, puis les fichiers hello, il n’existe aucune option d’ajout.</span><span class="sxs-lookup"><span data-stu-id="6bce2-401">If you select an existing file, then hello file will be overwritten, there is no append option.</span></span>

<span data-ttu-id="6bce2-402">Ensuite, choisissez si toolog toutes les critiques, ou aucun message d’erreur.</span><span class="sxs-lookup"><span data-stu-id="6bce2-402">Then, choose whether toolog all, critical, or no error messages.</span></span> <span data-ttu-id="6bce2-403">Enfin, déterminer la fréquence à laquelle hello sur le message de transfert écran sera mise à jour avec sa progression.</span><span class="sxs-lookup"><span data-stu-id="6bce2-403">Finally, decide how frequently hello on screen transfer message will be updated with its progress.</span></span>

    ![Screenshot of Advanced configuration screen](./media/import-data/AdvancedConfiguration.png)

## <a name="confirm-import-settings-and-view-command-line"></a><span data-ttu-id="6bce2-404">Confirmation des paramètres d'importation et affichage de la ligne de commande</span><span class="sxs-lookup"><span data-stu-id="6bce2-404">Confirm import settings and view command line</span></span>
1. <span data-ttu-id="6bce2-405">Après avoir spécifié les informations de la source, les informations de la cible et configuration avancée, passez en revue le résumé de la migration hello et, le cas échéant, afficher ou copier hello résultant migration commande (copie hello est utile tooautomate des opérations d’importation) :</span><span class="sxs-lookup"><span data-stu-id="6bce2-405">After specifying source information, target information, and advanced configuration, review hello migration summary and, optionally, view/copy hello resulting migration command (copying hello command is useful tooautomate import operations):</span></span>
   
    ![Capture d'écran de l'écran de résumé](./media/import-data/summary.png)
   
    ![Capture d'écran de l'écran de résumé](./media/import-data/summarycommand.png)
2. <span data-ttu-id="6bce2-408">Une fois que vous êtes satisfait de vos options sources et cibles, cliquez sur **Importer**.</span><span class="sxs-lookup"><span data-stu-id="6bce2-408">Once you’re satisfied with your source and target options, click **Import**.</span></span> <span data-ttu-id="6bce2-409">Hello écoulé, le nombre transférée et informations d’échec (si vous n’avez pas fourni un nom de fichier de configuration avancée de hello) met à jour que l’importation de hello est en cours.</span><span class="sxs-lookup"><span data-stu-id="6bce2-409">hello elapsed time, transferred count, and failure information (if you didn't provide a file name in hello Advanced configuration) will update as hello import is in process.</span></span> <span data-ttu-id="6bce2-410">Une fois terminé, vous pouvez exporter les résultats de hello (par exemple, toodeal d’erreurs d’importation).</span><span class="sxs-lookup"><span data-stu-id="6bce2-410">Once complete, you can export hello results (e.g. toodeal with any import failures).</span></span>
   
    ![Capture d’écran des options d’exportation JSON Azure Cosmos DB](./media/import-data/viewresults.png)
3. <span data-ttu-id="6bce2-412">Vous pouvez également démarrer une nouvelle importation, soit conserver les paramètres existants de hello (par exemple, les choix de plus d’informations, source et cible de chaîne de connexion, etc.) ou à la redéfinition de toutes les valeurs.</span><span class="sxs-lookup"><span data-stu-id="6bce2-412">You may also start a new import, either keeping hello existing settings (e.g. connection string information, source and target choice, etc.) or resetting all values.</span></span>
   
    ![Capture d’écran des options d’exportation JSON Azure Cosmos DB](./media/import-data/newimport.png)

## <a name="next-steps"></a><span data-ttu-id="6bce2-414">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6bce2-414">Next steps</span></span>

<span data-ttu-id="6bce2-415">Dans ce didacticiel, vous avez effectué les éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="6bce2-415">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6bce2-416">Installé l’outil de Migration des données hello</span><span class="sxs-lookup"><span data-stu-id="6bce2-416">Installed hello Data Migration tool</span></span>
> * <span data-ttu-id="6bce2-417">Importation de données à partir de différentes sources de données</span><span class="sxs-lookup"><span data-stu-id="6bce2-417">Imported data from different data sources</span></span>
> * <span data-ttu-id="6bce2-418">Exporté à partir de la base de données Azure Cosmos tooJSON</span><span class="sxs-lookup"><span data-stu-id="6bce2-418">Exported from Azure Cosmos DB tooJSON</span></span>

<span data-ttu-id="6bce2-419">Vous pouvez maintenant continuer le didacticiel suivant de toohello et savoir comment les données de tooquery à l’aide de la base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="6bce2-419">You can now proceed toohello next tutorial and learn how tooquery data using Azure Cosmos DB.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="6bce2-420">Comment les données tooquery ?</span><span class="sxs-lookup"><span data-stu-id="6bce2-420">How tooquery data?</span></span>](../cosmos-db/tutorial-query-documentdb.md)
