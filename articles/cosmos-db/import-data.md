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
# <a name="how-tooimport-data-into-azure-cosmos-db-for-hello-documentdb-api"></a>Comment tooimport les données dans la base de données Azure Cosmos pour hello API DocumentDB ?

Ce didacticiel fournit des instructions sur l’utilisation de hello de base de données Azure Cosmos : outil de Migration des données API DocumentDB, qui peut importer des données de diverses sources, y compris les fichiers JSON, des fichiers CSV, SQL, MongoDB, le stockage de Table Windows Azure, Amazon DynamoDB et DocumentDB de base de données Azure Cosmos Collections d’API dans des collections pour utilisent avec la base de données Azure Cosmos et hello API DocumentDB. outil de Migration des données Hello peut également servir lors de la migration à partir d’une seule partition tooa plusieurs partitions collecte pour hello API DocumentDB.

outil de Migration des données Hello fonctionne uniquement lors de l’importation de données dans la base de données Azure Cosmos pour utiliser avec hello API DocumentDB. L’importation de données pour une utilisation avec hello API de Table ou de l’API Graph n’est pas prise en charge pour l’instant. 

tooimport de données pour une utilisation avec hello MongoDB API, consultez [base de données Azure Cosmos : comment les données de toomigrate hello MongoDB API ?](mongodb-migrate.md).

Ce didacticiel couvre hello tâches suivantes :

> [!div class="checklist"]
> * Installation de l’outil de Migration des données hello
> * Importation de données à partir de différentes sources de données
> * Exportation à partir de la base de données Azure Cosmos tooJSON

## <a id="Prerequisites"></a>Configuration requise
Avant de suivre les instructions de hello dans cet article, assurez-vous d’avoir installé des éléments suivants hello :

* [Microsoft .NET Framework 4.51](https://www.microsoft.com/download/developer-tools.aspx) ou une version ultérieure.

## <a id="Overviewl"></a>Vue d’ensemble de l’outil de Migration des données hello
outil de Migration des données Hello est une solution open source qui importe des données tooAzure Cosmos DB à partir de diverses sources, notamment :

* Fichiers JSON
* MongoDB
* SQL Server
* Fichiers CSV
* Stockage de tables Azure
* Amazon DynamoDB
* HBase
* Collections Azure Cosmos DB

Pendant que l’outil d’importation hello inclut une interface utilisateur graphique (dtui.exe), il peut également être pilotée à partir de la ligne de commande hello (dt.exe). En fait, il est une option de commande de hello associé toooutput après avoir configuré une importation via l’interface utilisateur de hello. Des données sources tabulaires (par exemple, des fichiers SQL Server ou CSV) peuvent être transformées de manière à ce que des relations hiérarchiques (sous-documents) puissent être créées pendant l'importation. Conserver la lecture toolearn plus d’informations sur les options de source, tooimport de lignes de commande d’exemple à partir de chaque source, importer options cibles et l’affichage des résultats.

## <a id="Install"></a>Installer l’outil de Migration des données hello
code de source d’outil de migration Hello est disponible sur GitHub dans [ce référentiel](https://github.com/azure/azure-documentdb-datamigrationtool) et une version compilée est disponible à partir de [Microsoft Download Center](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d). Vous pouvez compiler hello solution ou simplement télécharger et extraire le répertoire de tooa hello version compilée de votre choix. Exécutez ensuite l’un des fichiers suivants :

* **Dtui.exe**: version de l’interface graphique de l’outil de hello
* **DT.exe**: version de ligne de commande de l’outil de hello

## <a name="import-data"></a>Importer des données

Une fois que vous avez installé l’outil de hello, il est temps tooimport vos données. Le type de données voulez-vous tooimport ?

* [Fichiers JSON](#JSON)
* [MongoDB](#MongoDB)
* [Fichiers d’exportation MongoDB](#MongoDBExport)
* [SQL Server](#SQL)
* [Fichiers CSV](#CSV)
* [Stockage Table Azure](#AzureTableSource)
* [Amazon DynamoDB](#DynamoDBSource)
* [Objet blob](#BlobImport)
* [Collections Azure Cosmos DB](#DocumentDBSource)
* [HBase](#HBaseSource)
* [Importation en bloc Azure Cosmos DB](#DocumentDBBulkImport)
* [Importation d’enregistrement séquentiel Azure Cosmos DB](#DocumentDSeqTarget)


## <a id="JSON"></a>fichiers au format JSON tooimport
Hello option importateur JSON fichier source vous permet de tooimport un ou plusieurs de documents JSON fichiers ou JSON qui contiennent chacun un tableau des documents JSON. Lorsque vous ajoutez des dossiers qui contiennent des tooimport de fichiers JSON, vous pouvez hello de rechercher des fichiers dans les sous-dossiers de manière récursive.

![Capture d’écran des options sources du fichier JSON - Outils de migration de base de données](./media/import-data/jsonsource.png)

Voici quelques exemples de ligne de commande fichiers JSON tooimport :

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

## <a id="MongoDB"></a>tooimport de MongoDB

> [!IMPORTANT]
> Si vous importez un compte de base de données Azure Cosmos tooan avec prise en charge pour MongoDB, suivez ces [instructions](mongodb-migrate.md).
> 
> 

Hello option d’importateur MongoDB source vous permet de tooimport à partir d’une collection de MongoDB individuels et en option, filtrez les documents à l’aide d’une requête et/ou modifier la structure du document hello à l’aide d’une projection.  

![Capture d’écran des options sources MongoDB](./media/import-data/mongodbsource.png)

chaîne de connexion Hello est au format de MongoDB hello standard :

    mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database>

> [!NOTE]
> Utilisez hello Vérifiez commande tooensure qui hello instance MongoDB spécifiée dans le champ de chaîne de connexion hello est accessible.
> 
> 

Entrez le nom hello de collection hello à partir de laquelle les données seront importées. Vous pouvez éventuellement spécifier ou fournir un fichier pour une requête (par exemple, {pop : {$gt : 5000}}) et/ou la projection (par exemple, {loc:0}) tooboth filtre et forme hello données toobe importé.

Voici certains tooimport d’exemples de ligne de commande à partir de MongoDB :

    #Import all documents from a MongoDB collection
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZips /t.IdField:_id /t.CollectionThroughput:2500

    #Import documents from a MongoDB collection which match hello query and exclude hello loc field
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /s.Query:{pop:{$gt:50000}} /s.Projection:{loc:0} /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZipsTransform /t.IdField:_id/t.CollectionThroughput:2500

## <a id="MongoDBExport"></a>fichiers d’exportation tooimport MongoDB

> [!IMPORTANT]
> Si vous importez un compte de base de données Azure Cosmos tooan avec prise en charge pour MongoDB, suivez ces [instructions](mongodb-migrate.md).
> 
> 

Hello, option du fichier source importateur pour MongoDB exportation JSON vous permet de tooimport un ou plusieurs fichiers JSON généré par l’utilitaire mongoexport hello.  

![Capture d’écran des options sources d’exportation MongoDB](./media/import-data/mongodbexportsource.png)

Lorsque vous ajoutez des dossiers qui contiennent les fichiers JSON d’exportation MongoDB pour l’importation, vous pouvez hello de rechercher des fichiers dans les sous-dossiers de manière récursive.

Voici une tooimport d’exemple de ligne de commande à partir de l’exportation de MongoDB fichiers JSON :

    dt.exe /s:MongoDBExport /s.Files:D:\mongoemployees.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:employees /t.IdField:_id /t.Dates:Epoch /t.CollectionThroughput:2500

## <a id="SQL"></a>tooimport à partir de SQL Server
Hello option importateur de la source SQL vous permet de tooimport à partir d’une base de données SQL Server et en option, filtrez toobe d’enregistrements hello importé à l’aide d’une requête. En outre, vous pouvez modifier la structure du document hello en spécifiant un séparateur d’imbrication (plus tard).  

![Capture d’écran des options sources SQL - Outils de migration de base de données](./media/import-data/sqlexportsource.png)

Hello de chaîne de connexion hello est format de chaîne de connexion hello standard SQL.

> [!NOTE]
> Utilisez hello Vérifiez commande tooensure qui hello instance SQL Server spécifiée dans le champ de chaîne de connexion hello est accessible.
> 
> 

Hello imbrication propriété separator est (sous-documents) des relations hiérarchiques toocreate utilisé pendant l’importation. Tenez compte des hello suivant la requête SQL :

*select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'*

Qui renvoie hello suivant des résultats (partielles) :

![Capture d’écran des résultats de requête SQL](./media/import-data/sqlqueryresults.png)

Notez les alias hello telles que Address.AddressType et Address.Location.StateProvinceName. En spécifiant un séparateur d’imbrication de '.', outil d’importation hello crée l’adresse et d’importer des sous-documents Address.Location pendant hello. Voici un exemple de document qui en résulte dans Azure Cosmos DB :

*{« ID » : « 956 », « Nom » : « Service et vente au détail », « Adresse »: {« AddressType »: « Siège », « AddressLine1 »: « #500-75 o ’ Connor Street », « Lieu »: {« Ville »: « Ottawa », « StateProvinceName »: « Ontario »}, « Code postal »: « K4B 1S2 », « CountryRegionName »: « Canada »}}*

Voici certains tooimport d’exemples de ligne de commande à partir de SQL Server :

    #Import records from SQL which match a query
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, * from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Stores /t.IdField:Id /t.CollectionThroughput:2500

    #Import records from sql which match a query and create hierarchical relationships
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /s.NestingSeparator:. /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:StoresSub /t.IdField:Id /t.CollectionThroughput:2500

## <a id="CSV"></a>les fichiers CSV tooimport et convert CSV tooJSON
Hello, option d’importateur CSV fichier source permet de vous tooimport un ou plusieurs fichiers CSV. Lorsque vous ajoutez des dossiers qui contiennent les fichiers des volumes partagés de cluster pour l’importation, vous pouvez hello de rechercher des fichiers dans les sous-dossiers de manière récursive.

![Options de source de capture d’écran de volume partagé de cluster - CSV tooJSON](media/import-data/csvsource.png)

Source SQL toohello similaire, hello imbrication separator, propriété peut être utilisé toocreate des relations hiérarchiques (sous-chemin de documents) lors de l’importation. Tenez compte des hello suivant la ligne d’en-tête de volume partagé de cluster et les lignes de données :

![Exemples d’enregistrements d’écran de volume partagé de cluster - CSV tooJSON](./media/import-data/csvsample.png)

Notez les alias hello telles que DomainInfo.Domain_Name et RedirectInfo.Redirecting. En spécifiant un séparateur d’imbrication de '.', outil d’importation hello créera DomainInfo et importer des sous-documents RedirectInfo pendant hello. Voici un exemple de document qui en résulte dans Azure Cosmos DB :

*{« DomainInfo » : {« Nom_domaine » : « ACUS.GOV », « Domain_Name_Address » : « http://www. ACUS.GOV »}, « Agence fédérale » : « Conférence Administrative de hello United States », « RedirectInfo » : {« Redirection » : « 0 », « Redirect_Destination » : « »}, « id » : « 9cc565c5-ebcd-1c03-ebd3-cc3e2ecd814d »}*

outil d’importation Hello va tenter de tooinfer informations de type pour les valeurs sans guillemets dans les fichiers CSV (valeurs entre guillemets sont toujours traités en tant que chaînes).  Les types sont identifiées dans hello suivant l’ordre : nombre, date/heure, valeur booléenne.  

Il existe deux autres toonote de choses sur l’importation d’un volume partagé de cluster :

1. Par défaut, les valeurs sans guillemets sont toujours privées de leurs tabulations et espaces, tandis que les valeurs entre guillemets sont conservées telles quelles. Ce comportement peut être substitué par hello que Trim entre guillemets l’option de ligne de commande /s.TrimQuoted case à cocher ou hello des valeurs.
2. Par défaut, une valeur null sans guillemets est considérée comme une valeur null. Ce comportement peut être substitué (autrement dit, de traiter une valeur null sans guillemets sous forme de chaîne « null ») avec hello Treat NULL en tant qu’option de ligne de commande /s.NoUnquotedNulls case à cocher ou hello des chaîne de guillemets.

Voici un exemple de ligne de commande pour une importation CSV :

    dt.exe /s:CsvFile /s.Files:.\Employees.csv /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Employees /t.IdField:EntityID /t.CollectionThroughput:2500

## <a id="AzureTableSource"></a>tooimport à partir du stockage de Table Azure
Hello option d’importateur de source de stockage Azure Table vous permet de tooimport à partir d’une table de stockage Azure Table individuelle et en option, filtrez toobe d’entités de table hello importé. Notez que vous ne peut pas utiliser des données de stockage Azure Table hello Migration des données outil tooimport dans la base de données Azure Cosmos pour une utilisation avec hello API de Table. Uniquement l’importation tooAzure Cosmos DB pour une utilisation avec hello API DocumentDB est pris en charge pour l’instant.

![Capture d’écran des options sources de stockage de tables Azure](./media/import-data/azuretablesource.png)

format Hello Hello chaîne de connexion de stockage de Table Azure est la suivante :

    DefaultEndpointsProtocol=<protocol>;AccountName=<Account Name>;AccountKey=<Account Key>;

> [!NOTE]
> Utilisez hello Vérifiez commande tooensure qui hello instance de stockage Azure Table spécifiée dans le champ de chaîne de connexion hello est accessible.
> 
> 

Entrez le nom hello Hello Azure table à partir de laquelle les données seront importées. Vous pouvez éventuellement spécifier un [filtre](https://msdn.microsoft.com/library/azure/ff683669.aspx).

Hello, option de Table Azure storage source importateur a hello options supplémentaires suivantes :

1. Inclusion des champs internes
   1. Tous : inclure tous les champs internes (PartitionKey, RowKey et Timestamp)
   2. Aucun : exclure tous les champs internes
   3. RowKey - inclure uniquement les champs de RowKey hello
2. Sélection des colonnes
   1. Les filtres de stockage de tables Azure ne prennent pas en charge les projections. Si vous souhaitez que les propriétés d’entité tooonly importation spécifiques Table Azure, ajoutez-les comme liste de sélection des colonnes toohello. Toutes les autres propriétés d'entité seront ignorées.

Voici une tooimport d’exemple de ligne de commande à partir du stockage de Table Azure :

    dt.exe /s:AzureTable /s.ConnectionString:"DefaultEndpointsProtocol=https;AccountName=<Account Name>;AccountKey=<Account Key>" /s.Table:metrics /s.InternalFields:All /s.Filter:"PartitionKey eq 'Partition1' and RowKey gt '00001'" /s.Projection:ObjectCount;ObjectSize  /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:metrics /t.CollectionThroughput:2500

## <a id="DynamoDBSource"></a>tooimport d’Amazon DynamoDB
Hello, option d’importateur Amazon DynamoDB source vous permet de tooimport à partir d’une table Amazon DynamoDB et en option, filtrez toobe d’entités hello importé. Plusieurs modèles sont fournis pour faciliter au maximum la configuration d'une importation.

![Capture d’écran des options sources Amazon DynamoDB - Outils de migration de base de données](./media/import-data/dynamodbsource1.png)

![Capture d’écran des options sources Amazon DynamoDB - Outils de migration de base de données](./media/import-data/dynamodbsource2.png)

format Hello Hello chaîne de connexion Amazon DynamoDB est :

    ServiceURL=<Service Address>;AccessKey=<Access Key>;SecretKey=<Secret Key>;

> [!NOTE]
> Utilisez hello Vérifiez commande tooensure qui hello instance Amazon DynamoDB spécifiée dans le champ de chaîne de connexion hello est accessible.
> 
> 

Voici une tooimport d’exemple de ligne de commande à partir d’Amazon DynamoDB :

    dt.exe /s:DynamoDB /s.ConnectionString:ServiceURL=https://dynamodb.us-east-1.amazonaws.com;AccessKey=<accessKey>;SecretKey=<secretKey> /s.Request:"{   """TableName""": """ProductCatalog""" }" /t:DocumentDBBulk /t.ConnectionString:"AccountEndpoint=<Azure Cosmos DB Endpoint>;AccountKey=<Azure Cosmos DB Key>;Database=<Azure Cosmos DB Database>;" /t.Collection:catalogCollection /t.CollectionThroughput:2500

## <a id="BlobImport"></a>fichiers tooimport à partir du stockage d’objets Blob Azure
Hello fichier JSON, fichier d’exportation MongoDB et options importateur de source de fichier CSV permettent de tooimport un ou plusieurs fichiers à partir du stockage d’objets Blob Azure. Après avoir spécifié une URL de conteneur d’objets Blob et de la clé de compte, il suffit de fournir un tooimport de fichier (s) de hello tooselect expression régulière.

![Capture d’écran des options sources du fichier blob](./media/import-data/blobsource.png)

Voici les fichiers de ligne de commande exemple tooimport JSON à partir du stockage d’objets Blob Azure :

    dt.exe /s:JsonFile /s.Files:"blobs://<account key>@account.blob.core.windows.net:443/importcontainer/.*" /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:doctest

## <a id="DocumentDBSource"></a>tooimport à partir d’une collection de l’API de DocumentDB de base de données Azure Cosmos
Hello, option de base de données Azure Cosmos source importateur vous permet de tooimport des données à partir d’une ou plusieurs collections de base de données Azure Cosmos et en option, filtrez les documents à l’aide d’une requête.  

![Capture d’écran des options sources d’Azure Cosmos DB](./media/import-data/documentdbsource.png)

format Hello Hello chaîne de connexion de base de données Azure Cosmos est :

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

Hello chaîne de connexion de compte de base de données Azure Cosmos peut être récupéré à partir du Panneau de clés hello Hello portail Azure, comme décrit dans [comment toomanage un compte de base de données Azure Cosmos](manage-account.md)toutefois hello le nom de base de données hello doit toobe ajouté toohello chaîne de connexion dans hello suivant le format :

    Database=<CosmosDB Database>;

> [!NOTE]
> Utilisez hello Vérifiez commande tooensure qui hello l’instance de base de données Azure Cosmos spécifiée dans le champ de chaîne de connexion hello est accessible.
> 
> 

tooimport à partir d’une collection de base de données Azure Cosmos unique, entrez le nom hello de collection hello à partir de laquelle les données seront importées. tooimport provenant de plusieurs collections de base de données Azure Cosmos, fournir une expression régulière de toomatch un ou plusieurs noms de collection (par exemple, collection01 | collection02 | collection03). Vous pouvez éventuellement spécifier, ou fournir un fichier pour un filtre de requête de tooboth et forme hello toobe de données importée.

> [!NOTE]
> Étant donné que le champ de regroupement hello accepte des expressions régulières, si vous importez à partir d’une collection unique dont le nom contient des caractères de l’expression régulière, ces caractères doivent être échappés en conséquence.
> 
> 

Hello, option de base de données Azure Cosmos source importateur a des options avancées suivantes de hello :

1. Inclure les champs internes : Spécifie ou non les propriétés de système de document de base de données Azure Cosmos tooinclude Bonjour exporter (par exemple, _rid, _ts).
2. Nombre de tentatives en cas d’échec : Spécifie le nombre de hello de tooretry hello connexion tooAzure Cosmos DB en cas de défaillances temporaires (par exemple, une interruption de connexion de réseau).
3. Intervalle avant nouvelle tentative : Spécifie la durée pendant laquelle toowait nouvelles tentatives hello connexion tooAzure Cosmos DB en cas de défaillances temporaires (par exemple, une interruption de connexion de réseau).
4. Mode de connexion : Spécifie toouse de mode de connexion hello avec la base de données Azure Cosmos. les choix disponibles Hello sont DirectTcp, DirectHttps et la passerelle. modes de connexion directe Hello sont plus rapides, lorsque le mode de passerelle hello est pare-feu plus convivial car elle utilise uniquement le port 443.

![Capture d’écran des options sources avancées d’Azure Cosmos DB](./media/import-data/documentdbsourceoptions.png)

> [!TIP]
> Hello importation outil par défaut tooconnection DirectTcp. Si vous rencontrez des problèmes liés au pare-feu, changez de mode de tooconnection passerelle, car il ne nécessite que le port 443.
> 
> 

Voici certains tooimport d’exemples de ligne de commande à partir de la base de données Azure Cosmos :

    #Migrate data from one Azure Cosmos DB collection tooanother Azure Cosmos DB collections
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:TEColl /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:TESessions /t.CollectionThroughput:2500

    #Migrate data from multiple Azure Cosmos DB collections tooa single Azure Cosmos DB collection
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:comp1|comp2|comp3|comp4 /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:singleCollection /t.CollectionThroughput:2500

    #Export an Azure Cosmos DB collection tooa JSON file
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:StoresSub /t:JsonFile /t.File:StoresExport.json /t.Overwrite /t.CollectionThroughput:2500

> [!TIP]
> Hello, outil d’importation Azure Cosmos DB données prend également en charge l’importation des données de hello [Azure Cosmos DB émulateur](local-emulator.md). Lorsque vous importez des données à partir d’un émulateur local, définir de point de terminaison hello trop`https://localhost:<port>`. 
> 
> 

## <a id="HBaseSource"></a>tooimport dans HBase
Hello, option d’importateur HBase source vous permet de tooimport des données à partir d’une table HBase et en option, filtrez les données de salutation. Plusieurs modèles sont fournis pour faciliter au maximum la configuration d'une importation.

![Capture d’écran des options sources HBase](./media/import-data/hbasesource1.png)

![Capture d’écran des options sources HBase](./media/import-data/hbasesource2.png)

format Hello Hello chaîne de connexion HBase Stargate est :

    ServiceURL=<server-address>;Username=<username>;Password=<password>

> [!NOTE]
> Utilisez hello Vérifiez commande tooensure qui hello instance HBase spécifiée dans le champ de chaîne de connexion hello est accessible.
> 
> 

Voici une tooimport d’exemple de ligne de commande à partir de HBase :

    dt.exe /s:HBase /s.ConnectionString:ServiceURL=<server-address>;Username=<username>;Password=<password> /s.Table:Contacts /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:hbaseimport

## <a id="DocumentDBBulkTarget"></a>tooimport toohello DocumentDB API (d’importation en bloc)
importateur de base de données en bloc Cosmos de Azure Hello vous permet de tooimport à partir d’une des options de source disponible hello, à l’aide d’une procédure de base de données Cosmos Azure stockée par souci d’efficacité. outil de Hello prend en charge la collection de base de données Azure Cosmos partitionnée unique d’importation tooone, ainsi que d’importation partitionnée par laquelle les données sont partitionnées sur plusieurs collections de base de données Azure Cosmos partitionnée unique. Pour plus d’informations sur le partitionnement de données, consultez [Partitionnement et mise à l’échelle dans Azure Cosmos DB](partition-data.md). outil de Hello créer, exécuter et supprimer puis procédure stockée hello hello cible regroupements.  

![Capture d’écran des options de bloc d’Azure Cosmos DB](./media/import-data/documentdbbulk.png)

format Hello Hello chaîne de connexion de base de données Azure Cosmos est :

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

Hello chaîne de connexion de compte de base de données Azure Cosmos peut être récupéré à partir du Panneau de clés hello Hello portail Azure, comme décrit dans [comment toomanage un compte de base de données Azure Cosmos](manage-account.md)toutefois hello le nom de base de données hello doit toobe ajouté toohello chaîne de connexion dans hello suivant le format :

    Database=<CosmosDB Database>;

> [!NOTE]
> Utilisez hello Vérifiez commande tooensure qui hello l’instance de base de données Azure Cosmos spécifiée dans le champ de chaîne de connexion hello est accessible.
> 
> 

tooimport tooa collection en une seule, entrez le nom hello de hello collection toowhich données seront importées et cliquez sur le bouton Ajouter de hello. tooimport toomultiple collections, spécifiez le nom de chaque collection individuellement ou hello suivant de syntaxe toospecify plusieurs collections : *collection_prefix*[index - index de fin de début]. Lorsque vous spécifiez plusieurs collections via la syntaxe de susmentionnés hello, gardez les points suivants hello à l’esprit :

1. Seuls les modèles de nom de plage de nombres entiers sont pris en charge. Par exemple, la spécification de regroupement [0-3] produira hello suivant des collections : collection0 collection1, collection2, collection3.
2. Vous pouvez utiliser une syntaxe abrégée : collection[3], qui émet le même jeu de collections que celui mentionné à l'étape 1.
3. Plusieurs substitutions peuvent être fournies. Par exemple, collection[0-1] [0-9] génère 20 noms de collection avec des zéros non significatifs (collection01, ..02, ..03).

Une fois hello ou les noms de collection ont été spécifiées, choisissez le débit souhaité de hello de collections de hello (400 RUs too10, 000 RUs). Pour de meilleures performances d’importation, choisissez un débit plus élevé. Pour plus d’informations sur les niveaux de performances, consultez les [niveaux de performances d’Azure Cosmos DB](performance-levels.md).

> [!NOTE]
> paramètre de débit de performance Hello s’applique uniquement à la création de toocollection. Si hello spécifié de la collection existe déjà, son débit n’est pas modifiée.
> 
> 

Lorsque vous importez des collections de toomultiple, outil d’importation hello prend en charge le partitionnement par hachage en fonction. Dans ce scénario, spécifiez la propriété de document hello vous souhaitez toouse comme clé de Partition de hello (si la clé de Partition est vide, documents seront partitionnées au hasard entre les collections de cible hello).

Vous pouvez éventuellement spécifier quel champ de la source d’importation hello doit être utilisé en tant que propriété d’id de document de base de données Azure Cosmos de hello pendant l’importation hello (Notez que si les documents ne contiennent pas cette propriété, puis outil d’importation hello génère un GUID en tant que valeur de la propriété id hello).

De nombreuses options avancées sont disponibles lors de l'importation. Tout d’abord, tandis que l’outil de hello inclut un bloc par défaut importer une procédure stockée (BulkInsert.js), vous pouvez toospecify votre propre procédure d’importation stockée :

 ![Capture d’écran de l’option sproc d’insertion de bloc Azure Cosmos DB](./media/import-data/bulkinsertsp.png)

De plus, lorsque vous importez des types de date (par exemple, depuis SQL Server ou MongoDB), vous pouvez choisir entre trois options d'importation :

 ![Capture d’écran des options d’importation de date et d’heure Azure Cosmos DB](./media/import-data/datetimeoptions.png)

* Chaîne : conserver en tant que valeur de chaîne
* Epoch : conserver en tant que valeur numérique Epoch
* Les deux : conserver la chaîne et les valeurs numériques Epoch Cette option crée un sous-document, par exemple : « date_joined » : {« Valeur »: « 2013-10-21T21:17:25.2410000Z », « Epoch » : 1382390245}

importateur de base de données en bloc Cosmos de Azure Hello a hello autres options avancées suivantes :

1. Taille du lot : hello outil par défaut tooa taille de lot de 50.  Si toobe de documents hello importé est volumineux, envisagez de réduire la taille de lot hello. À l’inverse, si toobe de documents hello importé est petit, envisagez d’augmenter la taille de lot hello.
2. Taille de Script maximale (octets) : outil de hello par défaut est la taille de script max tooa de 512 Ko
3. Désactiver la génération automatique de code : Si chaque toobe document importée contient un champ d’id, puis en sélectionnant cette option peut augmenter les performances. Les documents avec un champ d’ID unique manquant ne seront pas importés.
4. Mise à jour des Documents existants : hello outil toonot de valeurs par défaut en remplaçant les documents existants avec l’id est en conflit. Cette option permettra de remplacer les documents existants par les ID correspondants. Cette fonctionnalité est utile pour les migrations de données planifiées qui mettent à jour des documents existants.
5. Nombre de tentatives en cas d’échec : Spécifie le nombre de hello de tooretry hello connexion tooAzure Cosmos DB en cas de défaillances temporaires (par exemple, une interruption de connexion de réseau).
6. Intervalle avant nouvelle tentative : Spécifie la durée pendant laquelle toowait nouvelles tentatives hello connexion tooAzure Cosmos DB en cas de défaillances temporaires (par exemple, une interruption de connexion de réseau).
7. Mode de connexion : Spécifie toouse de mode de connexion hello avec la base de données Azure Cosmos. les choix disponibles Hello sont DirectTcp, DirectHttps et la passerelle. modes de connexion directe Hello sont plus rapides, lorsque le mode de passerelle hello est pare-feu plus convivial car elle utilise uniquement le port 443.

![Capture d’écran des options d’importation en bloc avancées d’Azure Cosmos DB](./media/import-data/docdbbulkoptions.png)

> [!TIP]
> Hello importation outil par défaut tooconnection DirectTcp. Si vous rencontrez des problèmes liés au pare-feu, changez de mode de tooconnection passerelle, car il ne nécessite que le port 443.
> 
> 

## <a id="DocumentDBSeqTarget"></a>tooimport toohello DocumentDB API (importation d’enregistrements séquentiel)
importateur de séquentiel d’enregistrement de base de données Azure Cosmos Hello vous permet de tooimport à partir d’une des options de source disponible hello chaque enregistrement par enregistrement. Vous pouvez choisir cette option si vous importez un regroupement existant tooan qui a atteint son quota de procédures stockées. tooa d’importation Hello outil prend en charge une seule collection de base de données Azure Cosmos (partition unique et plusieurs partition), ainsi que d’importation partitionnée par laquelle les données sont partitionnées sur plusieurs collections de base de données Azure Cosmos à partition unique ou plusieurs partitions. Pour plus d’informations sur le partitionnement de données, consultez [Partitionnement et mise à l’échelle dans Azure Cosmos DB](partition-data.md).

![Capture d’écran des options d’importation d’enregistrement séquentiel d’Azure Cosmos DB](./media/import-data/documentdbsequential.png)

format Hello Hello chaîne de connexion de base de données Azure Cosmos est :

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

Hello chaîne de connexion de compte de base de données Azure Cosmos peut être récupéré à partir du Panneau de clés hello Hello portail Azure, comme décrit dans [comment toomanage un compte de base de données Azure Cosmos](manage-account.md)toutefois hello le nom de base de données hello doit toobe ajouté toohello chaîne de connexion dans hello suivant le format :

    Database=<Azure Cosmos DB Database>;

> [!NOTE]
> Utilisez hello Vérifiez commande tooensure qui hello l’instance de base de données Azure Cosmos spécifiée dans le champ de chaîne de connexion hello est accessible.
> 
> 

tooimport tooa collection en une seule, entrez le nom hello de hello collection toowhich données seront importées et cliquez sur le bouton Ajouter de hello. tooimport toomultiple collections, spécifiez le nom de chaque collection individuellement ou hello suivant de syntaxe toospecify plusieurs collections : *collection_prefix*[index - index de fin de début]. Lorsque vous spécifiez plusieurs collections via la syntaxe de susmentionnés hello, gardez les points suivants hello à l’esprit :

1. Seuls les modèles de nom de plage de nombres entiers sont pris en charge. Par exemple, la spécification de regroupement [0-3] produira hello suivant des collections : collection0 collection1, collection2, collection3.
2. Vous pouvez utiliser une syntaxe abrégée : collection[3], qui émet le même jeu de collections que celui mentionné à l'étape 1.
3. Plusieurs substitutions peuvent être fournies. Par exemple, collection[0-1] [0-9] génère 20 noms de collection avec des zéros non significatifs (collection01, ..02, ..03).

Une fois hello ou les noms de collection ont été spécifiées, choisissez le débit souhaité de hello de collections de hello (400 RUs too250, 000 RUs). Pour de meilleures performances d’importation, choisissez un débit plus élevé. Pour plus d’informations sur les niveaux de performances, consultez les [niveaux de performances d’Azure Cosmos DB](performance-levels.md). Toute importation toocollections avec un débit > 10 000 RUs nécessite une clé de partition. Si vous choisissez toohave RUs plus de 250 000, vous devez toofile une demande dans toohave de portail hello augmentée de votre compte.

> [!NOTE]
> paramètre de débit Hello s’applique uniquement à la création de toocollection. Si hello spécifié de la collection existe déjà, son débit n’est pas modifiée.
> 
> 

Lorsque vous importez des collections de toomultiple, outil d’importation hello prend en charge le partitionnement par hachage en fonction. Dans ce scénario, spécifiez la propriété de document hello vous souhaitez toouse comme clé de Partition de hello (si la clé de Partition est vide, documents seront partitionnées au hasard entre les collections de cible hello).

Vous pouvez éventuellement spécifier quel champ de la source d’importation hello doit être utilisé en tant que propriété d’id de document de base de données Azure Cosmos de hello pendant l’importation hello (Notez que si les documents ne contiennent pas cette propriété, puis outil d’importation hello génère un GUID en tant que valeur de la propriété id hello).

De nombreuses options avancées sont disponibles lors de l'importation. Tout d’abord, lorsque vous importez des types de date (par exemple, depuis SQL Server ou MongoDB), vous pouvez choisir entre trois options d'importation :

 ![Capture d’écran des options d’importation de date et d’heure Azure Cosmos DB](./media/import-data/datetimeoptions.png)

* Chaîne : conserver en tant que valeur de chaîne
* Epoch : conserver en tant que valeur numérique Epoch
* Les deux : conserver la chaîne et les valeurs numériques Epoch Cette option crée un sous-document, par exemple : « date_joined » : {« Valeur »: « 2013-10-21T21:17:25.2410000Z », « Epoch » : 1382390245}

Bonjour Azure Cosmos DB - importateur d’enregistrement séquentiel a hello autres options avancées suivantes :

1. Nombre de requêtes parallèles : outil de hello par défaut too2 les demandes parallèles. Si toobe de documents hello importé est petit, envisagez d’augmenter le nombre de hello de demandes parallèles. Notez que si ce nombre est élevé en trop, hello importation peut rencontrer la limitation.
2. Désactiver la génération automatique de code : Si chaque toobe document importée contient un champ d’id, puis en sélectionnant cette option peut augmenter les performances. Les documents avec un champ d’ID unique manquant ne seront pas importés.
3. Mise à jour des Documents existants : hello outil toonot de valeurs par défaut en remplaçant les documents existants avec l’id est en conflit. Cette option permettra de remplacer les documents existants par les ID correspondants. Cette fonctionnalité est utile pour les migrations de données planifiées qui mettent à jour des documents existants.
4. Nombre de tentatives en cas d’échec : Spécifie le nombre de hello de tooretry hello connexion tooAzure Cosmos DB en cas de défaillances temporaires (par exemple, une interruption de connexion de réseau).
5. Intervalle avant nouvelle tentative : Spécifie la durée pendant laquelle toowait nouvelles tentatives hello connexion tooAzure Cosmos DB en cas de défaillances temporaires (par exemple, une interruption de connexion de réseau).
6. Mode de connexion : Spécifie toouse de mode de connexion hello avec la base de données Azure Cosmos. les choix disponibles Hello sont DirectTcp, DirectHttps et la passerelle. modes de connexion directe Hello sont plus rapides, lorsque le mode de passerelle hello est pare-feu plus convivial car elle utilise uniquement le port 443.

![Capture d’écran des options d’importation d’enregistrement séquentiel avancées d’Azure Cosmos DB](./media/import-data/documentdbsequentialoptions.png)

> [!TIP]
> Hello importation outil par défaut tooconnection DirectTcp. Si vous rencontrez des problèmes liés au pare-feu, changez de mode de tooconnection passerelle, car il ne nécessite que le port 443.
> 
> 

## <a id="IndexingPolicy"></a>Spécification d’une stratégie d’indexation lors de la création de collections Azure Cosmos DB
Lorsque vous autorisez des collections de toocreate outil migration de hello lors de l’importation, vous pouvez spécifier la stratégie d’indexation hello des collections de hello. Bonjour avancé section options de hello Azure Cosmos DB et d’importation Azure Cosmos DB séquentiel options d’enregistrement, accédez à section de la stratégie d’indexation toohello.

![Capture d’écran des options de stratégie d’indexation avancées d’Azure Cosmos DB](./media/import-data/indexingpolicy1.png)

À l’aide de hello option de stratégie d’indexation avancées, vous pouvez sélectionner un fichier de stratégie d’indexation, manuellement entrer une stratégie d’indexation ou sélectionner un jeu de modèles par défaut (en cliquant avec le bouton droit dans hello l’indexation de stratégie de zone de texte).

les modèles de stratégie Hello hello outil fournit sont :

* Par défaut. Cette stratégie est préférable si vous exécutez des requêtes d’efficacité sur des chaînes et des requêtes ORDER BY, de plage et d’efficacité sur des nombres. Cette stratégie dispose d’une surcharge de stockage d'index inférieure à Plage.
* Plage. Cette stratégie est préférable si vous exécutez des requêtes ORDER BY, de plage et d'efficacité sur des nombres et des chaînes. Cette stratégie dispose d’une surcharge de stockage d'index supérieure à Par défaut ou Hachage.

![Capture d’écran des options de stratégie d’indexation avancées d’Azure Cosmos DB](./media/import-data/indexingpolicy2.png)

> [!NOTE]
> Si vous ne spécifiez pas une stratégie d’indexation, puis stratégie par défaut de hello sera appliquée. Pour plus d’informations sur les stratégies d’indexation, consultez [Stratégies d’indexation d’Azure Cosmos DB](indexing-policies.md).
> 
> 

## <a name="export-toojson-file"></a>Fichier d’exportation tooJSON
exportateur de JSON de base de données Azure Cosmos Hello vous permet de tooexport des hello source disponible options tooa fichier JSON qui contient un tableau des documents JSON. outil de Hello gère l’exportation hello pour vous, ou vous pouvez choisir la commande de migration qui en résulte tooview hello et exécuter des commandes de hello vous-même. fichier JSON résultante de Hello peut-être être stockée localement ou dans le stockage Blob Azure.

![Capture d’écran des options d’exportation de fichier local JSON Azure Cosmos DB](./media/import-data/jsontarget.png)

![Capture d’écran des options d’exportation du stockage blob Azure JSON Azure Cosmos DB](./media/import-data/jsontarget2.png)

Vous pouvez éventuellement choisir hello tooprettify résultant JSON, ce qui augmente la taille hello de document résultant de hello lors de la fabrication hello contenu plus lisibles par l’utilisateur.

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

## <a name="advanced-configuration"></a>Configuration avancée
Dans l’écran de configuration avancée hello, spécifiez emplacement hello de hello journal fichier toowhich vous souhaitez que les erreurs écrites. Hello, suivant les règles s’appliquent toothis page :

1. Si un nom de fichier n’est pas fourni, puis toutes les erreurs seront affichera sur la page de résultats hello.
2. Si un nom de fichier est fourni sans un répertoire, puis les fichiers hello seront créée (ou remplacée) dans l’annuaire d’environnement actuelle hello.
3. Si vous sélectionnez un existant seront remplacé le fichier, puis les fichiers hello, il n’existe aucune option d’ajout.

Ensuite, choisissez si toolog toutes les critiques, ou aucun message d’erreur. Enfin, déterminer la fréquence à laquelle hello sur le message de transfert écran sera mise à jour avec sa progression.

    ![Screenshot of Advanced configuration screen](./media/import-data/AdvancedConfiguration.png)

## <a name="confirm-import-settings-and-view-command-line"></a>Confirmation des paramètres d'importation et affichage de la ligne de commande
1. Après avoir spécifié les informations de la source, les informations de la cible et configuration avancée, passez en revue le résumé de la migration hello et, le cas échéant, afficher ou copier hello résultant migration commande (copie hello est utile tooautomate des opérations d’importation) :
   
    ![Capture d'écran de l'écran de résumé](./media/import-data/summary.png)
   
    ![Capture d'écran de l'écran de résumé](./media/import-data/summarycommand.png)
2. Une fois que vous êtes satisfait de vos options sources et cibles, cliquez sur **Importer**. Hello écoulé, le nombre transférée et informations d’échec (si vous n’avez pas fourni un nom de fichier de configuration avancée de hello) met à jour que l’importation de hello est en cours. Une fois terminé, vous pouvez exporter les résultats de hello (par exemple, toodeal d’erreurs d’importation).
   
    ![Capture d’écran des options d’exportation JSON Azure Cosmos DB](./media/import-data/viewresults.png)
3. Vous pouvez également démarrer une nouvelle importation, soit conserver les paramètres existants de hello (par exemple, les choix de plus d’informations, source et cible de chaîne de connexion, etc.) ou à la redéfinition de toutes les valeurs.
   
    ![Capture d’écran des options d’exportation JSON Azure Cosmos DB](./media/import-data/newimport.png)

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous avez effectué les éléments suivants de hello :

> [!div class="checklist"]
> * Installé l’outil de Migration des données hello
> * Importation de données à partir de différentes sources de données
> * Exporté à partir de la base de données Azure Cosmos tooJSON

Vous pouvez maintenant continuer le didacticiel suivant de toohello et savoir comment les données de tooquery à l’aide de la base de données Azure Cosmos. 

> [!div class="nextstepaction"]
>[Comment les données tooquery ?](../cosmos-db/tutorial-query-documentdb.md)
