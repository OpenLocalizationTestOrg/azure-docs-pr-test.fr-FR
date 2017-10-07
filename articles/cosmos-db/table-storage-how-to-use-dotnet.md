---
title: "aaaGet main du stockage de Table Azure à l’aide de .NET | Documents Microsoft"
description: "Stocker des données structurées dans le cloud hello avec le stockage Table Azure, un magasin de données NoSQL."
services: cosmos-db
documentationcenter: .net
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: fe46d883-7bed-49dd-980e-5c71df36adb3
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 04/10/2017
ms.author: mimig
ms.openlocfilehash: a3e9a4c6f6fd5e724535b86a3f99cd4c161de6de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-table-storage-using-net"></a>Prise en main du stockage de tables Azure à l’aide de .NET
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

Stockage de Table Azure est un service qui stocke NoSQL structuré du magasin de données dans le cloud de hello, en fournissant un attribut key/avec une conception schemaless. Stockage de Table schemaless, il est facile tooadapt d’evolve de votre application a besoin de vos données en tant que hello. Accéder aux données de stockage tooTable est rapide et économique pour de nombreux types d’applications et est généralement inférieur coût SQL traditionnel pour les volumes de données similaires.

Vous pouvez utiliser la Table stockage toostore flexible des groupes de données comme les données utilisateur pour les applications web, carnets d’adresses, les informations de périphérique ou autres types de votre service requiert des métadonnées. Vous pouvez stocker n’importe quel nombre d’entités dans une table, et un compte de stockage peut contenir n’importe quel nombre de tables, des limites de capacité toohello hello du compte de stockage.

### <a name="about-this-tutorial"></a>À propos de ce didacticiel
Ce didacticiel vous montre comment toouse hello [bibliothèque cliente de stockage Azure pour .NET](https://www.nuget.org/packages/WindowsAzure.Storage/) dans certains scénarios de stockage Azure Table. Ces scénarios sont présentés avec des exemples en C# pour la création et la suppression d’une table, et l’insertion, la mise à jour, la suppression et l’interrogation de données de table.

## <a name="prerequisites"></a>Composants requis

Vous devez hello suivant toocomplete ce didacticiel avec succès :

* [Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [Bibliothèque cliente Azure Storage pour .NET](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [Gestionnaire de configuration Azure pour .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* [Compte Stockage Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a>Autres exemples
Pour obtenir des exemples supplémentaires utilisant Table Storage, voir [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/)(Prise en main d’Azure Table Storage dans .NET). Vous pouvez télécharger l’exemple d’application hello et exécutez-le ou parcourir le code hello sur GitHub.

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a>Ajouter des directives d’utilisation
Ajoutez hello suivant **à l’aide de** haut toohello de directives de hello `Program.cs` fichier :

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Table; // Namespace for Table storage types
```

### <a name="parse-hello-connection-string"></a>Analyser la chaîne de connexion hello
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-table-service-client"></a>Créer le client du service de Table hello
Hello [CloudTableClient] [ dotnet_CloudTableClient] classe vous permet de tooretrieve tables et entités stockées dans le stockage Table. Voici une façon toocreate hello Table service client :

```csharp
// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```

Vous êtes maintenant code prêt toowrite qui lit les données à partir d’et écrit le stockage des données tooTable.

## <a name="create-a-table"></a>Création d’une table
Cet exemple montre comment toocreate une table si elle n’existe pas déjà :

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Retrieve a reference toohello table.
CloudTable table = tableClient.GetTableReference("people");

// Create hello table if it doesn't exist.
table.CreateIfNotExists();
```

## <a name="add-an-entity-tooa-table"></a>Ajouter une table de tooa d’entité
Objets tooC # mappent des entités à l’aide d’une classe personnalisée dérivée de [TableEntity][dotnet_TableEntity]. tooadd une table de tooa entité, créez une classe qui définit des propriétés de votre entité hello. Hello de code suivant définit une classe d’entité qui utilise le prénom du client hello en tant que clé de ligne hello et le nom comme clé de partition hello. Ensemble, les partitions d’une entité et la clé de ligne identifient uniquement dans la table de hello. Les entités avec hello même clé de partition peut être interrogé plus rapidement que les entités avec différentes clés de partition, mais à l’aide de clés de partition divers permet une plus grande évolutivité d’opérations parallèles. Toobe d’entités stockée dans des tables doit être d’un type pris en charge, par exemple dérivé hello [TableEntity] [ dotnet_TableEntity] classe. Propriétés de l’entité vous aimeriez toostore dans une table doivent être des propriétés publiques du type de hello et prend en charge l’obtention et définition des valeurs de. De plus, votre type d’entité *doit* exposer un constructeur sans paramètre.

```csharp
public class CustomerEntity : TableEntity
{
    public CustomerEntity(string lastName, string firstName)
    {
        this.PartitionKey = lastName;
        this.RowKey = firstName;
    }

    public CustomerEntity() { }

    public string Email { get; set; }

    public string PhoneNumber { get; set; }
}
```

Opérations de table qui impliquent des entités sont effectuent via hello [CloudTable] [ dotnet_CloudTable] objet que vous avez créé précédemment dans la section « Créer une table » de hello. toobe opération effectuée Hello est représenté par un [TableOperation] [ dotnet_TableOperation] objet. Hello exemple de code suivant illustre la création de hello Hello [CloudTable] [ dotnet_CloudTable] objet, puis un **CustomerEntity** objet. opération de hello tooprepare, un [TableOperation] [ dotnet_TableOperation] objet est créé entité customer de hello tooinsert dans la table de hello. Enfin, l’opération de hello est exécutée en appelant [CloudTable][dotnet_CloudTable].[ Exécutez][dotnet_CloudTable_Execute].

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a new customer entity.
CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
customer1.Email = "Walter@contoso.com";
customer1.PhoneNumber = "425-555-0101";

// Create hello TableOperation object that inserts hello customer entity.
TableOperation insertOperation = TableOperation.Insert(customer1);

// Execute hello insert operation.
table.Execute(insertOperation);
```

## <a name="insert-a-batch-of-entities"></a>Insertion d’un lot d’entités
Vous pouvez insérer un lot d'entités dans une table en une seule opération d'écriture. Autres remarques sur les opérations par lot :

* Vous pouvez effectuer des mises à jour, suppressions et insertions Bonjour même un seul traitement par lots.
* Une opération de lot unique peut inclure des entités de too100.
* Toutes les entités dans une seule opération doivent avoir hello même clé de partition.
* Bien qu’il soit possible de tooperform une requête sous la forme d’un traitement par lots, il doit être seule opération de hello dans un lot de hello.

Hello exemple de code suivant crée deux objets d’entité et l’ajoute chaque trop[TableBatchOperation] [ dotnet_TableBatchOperation] à l’aide de hello [insérer] [ dotnet_TableBatchOperation_Insert] méthode. Ensuite, [CloudTable][dotnet_CloudTable].[ ExecuteBatch] [ dotnet_CloudTable_ExecuteBatch] est appelé l’opération de hello tooexecute.

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create hello batch operation.
TableBatchOperation batchOperation = new TableBatchOperation();

// Create a customer entity and add it toohello table.
CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
customer1.Email = "Jeff@contoso.com";
customer1.PhoneNumber = "425-555-0104";

// Create another customer entity and add it toohello table.
CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
customer2.Email = "Ben@contoso.com";
customer2.PhoneNumber = "425-555-0102";

// Add both customer entities toohello batch insert operation.
batchOperation.Insert(customer1);
batchOperation.Insert(customer2);

// Execute hello batch operation.
table.ExecuteBatch(batchOperation);
```

## <a name="retrieve-all-entities-in-a-partition"></a>Extraction de toutes les entités d'une partition
tooquery une table pour toutes les entités dans une partition, utilisez un [TableQuery] [ dotnet_TableQuery] objet. Hello exemple de code suivant spécifie un filtre pour les entités où « Smith » est la clé de partition hello. Cet exemple imprime les champs de chaque entité dans la console de toohello de résultats de requête hello hello.

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Construct hello query operation for all customer entities where PartitionKey="Smith".
TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>().Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

// Print hello fields for each customer.
foreach (CustomerEntity entity in table.ExecuteQuery(query))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

## <a name="retrieve-a-range-of-entities-in-a-partition"></a>Extraction d’un ensemble d’entités dans une partition
Si vous ne souhaitez pas tooquery toutes les entités dans une partition, vous pouvez spécifier une plage en combinant le filtre de clé de partition hello avec un filtre de clé de ligne. Hello exemple de code suivant utilise deux filtres tooget toutes les entités dans la partition « Smith », où la clé de ligne hello (prénom) commence par une lettre avant « E » dans l’alphabet de hello, puis imprime les résultats de la requête hello.

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create hello table query.
TableQuery<CustomerEntity> rangeQuery = new TableQuery<CustomerEntity>().Where(
    TableQuery.CombineFilters(
        TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"),
        TableOperators.And,
        TableQuery.GenerateFilterCondition("RowKey", QueryComparisons.LessThan, "E")));

// Loop through hello results, displaying information about hello entity.
foreach (CustomerEntity entity in table.ExecuteQuery(rangeQuery))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

## <a name="retrieve-a-single-entity"></a>Extraction d'une seule entité
Vous pouvez écrire une requête tooretrieve une entité unique et spécifique. code Hello suivant utilise [TableOperation] [ dotnet_TableOperation] client de hello toospecify « Ben Smith ». Cette méthode retourne simplement une entité plutôt qu’une collection et hello a retourné la valeur dans [TableResult][dotnet_TableResult].[ Résultat] [ dotnet_TableResult_Result] est un **CustomerEntity** objet. Spécification des clés de partition et de ligne dans une requête est tooretrieve de manière plus rapide hello une seule entité hello service de Table.

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Print hello phone number of hello result.
if (retrievedResult.Result != null)
{
    Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
}
else
{
    Console.WriteLine("hello phone number could not be retrieved.");
}
```

## <a name="replace-an-entity"></a>Remplacement d’une entité
tooupdate une entité, récupérer à partir du service de Table hello, modifier l’objet d’entité hello, puis enregistrez les modifications hello de nouveau service de Table toohello. Hello code suivant modifie un numéro de téléphone existant. Au lieu d’appeler la méthode [Insert][dotnet_TableOperation_Insert], ce code utilise la méthode [Replace][dotnet_TableOperation_Replace]. [Remplacez] [ dotnet_TableOperation_Replace] causes hello toobe entité entièrement remplacé sur le serveur de hello, sauf si l’entité hello sur le serveur de hello a changé depuis sa récupération, auquel cas hello échoue. Cet échec est tooprevent votre application à partir de remplacement accidentel d’une modification effectuée entre hello récupération et mettre à jour par un autre composant de votre application. Hello gestion correcte de cet échec est tooretrieve hello entité à nouveau, apportez vos modifications (si elle est toujours valide), puis effectuer une autre [remplacer] [ dotnet_TableOperation_Replace] opération. Hello prochaine section vous montrera comment toooverride ce comportement.

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Assign hello result tooa CustomerEntity object.
CustomerEntity updateEntity = (CustomerEntity)retrievedResult.Result;

if (updateEntity != null)
{
    // Change hello phone number.
    updateEntity.PhoneNumber = "425-555-0105";

    // Create hello Replace TableOperation.
    TableOperation updateOperation = TableOperation.Replace(updateEntity);

    // Execute hello operation.
    table.Execute(updateOperation);

    Console.WriteLine("Entity updated.");
}
else
{
    Console.WriteLine("Entity could not be retrieved.");
}
```

## <a name="insert-or-replace-an-entity"></a>Insertion ou remplacement d’une entité
[Remplacez] [ dotnet_TableOperation_Replace] opérations échouent si l’entité de hello a été modifiée, car il a été récupéré à partir du serveur de hello. En outre, vous devez extraire votre entité hello du serveur de hello tout d’abord dans l’ordre pour hello [remplacer] [ dotnet_TableOperation_Replace] toobe opération réussie. Dans certains cas, toutefois, vous ne connaissez pas si l’entité hello existe sur le serveur de hello et les valeurs actuelles hello stockés qu’il contient sont sans importance. Votre mise à jour doit donc toutes les remplacer. tooaccomplish, vous devez utiliser un [InsertOrReplace] [ dotnet_TableOperation_InsertOrReplace] opération. Cette opération insère l’entité de hello si elle n’existe pas ou elle remplace dans ce cas, quelle que soit la lorsque la dernière mise à jour de hello a été effectuée.

Bonjour exemple de code suivant, une entité customer pour 'Fred Jones' est créée et insérée dans la table « people » de hello. Ensuite, nous utilisons hello [InsertOrReplace] [ dotnet_TableOperation_InsertOrReplace] opération toosave une entité avec hello même clé de partition (Jones) et une ligne de clé serveur de toohello (Fred), cette fois avec une valeur différente pour hello PhoneNumber propriété. Comme nous utilisons [InsertOrReplace][dotnet_TableOperation_InsertOrReplace], toutes ses valeurs de propriété sont remplacées. Toutefois, si une entité 'Fred Jones' n’était pas existait déjà dans la table de hello, il serait ont été inséré.

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a customer entity.
CustomerEntity customer3 = new CustomerEntity("Jones", "Fred");
customer3.Email = "Fred@contoso.com";
customer3.PhoneNumber = "425-555-0106";

// Create hello TableOperation object that inserts hello customer entity.
TableOperation insertOperation = TableOperation.Insert(customer3);

// Execute hello operation.
table.Execute(insertOperation);

// Create another customer entity with hello same partition key and row key.
// We've already created a 'Fred Jones' entity and saved it toothe
// 'people' table, but here we're specifying a different value for the
// PhoneNumber property.
CustomerEntity customer4 = new CustomerEntity("Jones", "Fred");
customer4.Email = "Fred@contoso.com";
customer4.PhoneNumber = "425-555-0107";

// Create hello InsertOrReplace TableOperation.
TableOperation insertOrReplaceOperation = TableOperation.InsertOrReplace(customer4);

// Execute hello operation. Because a 'Fred Jones' entity already exists in the
// 'people' table, its property values will be overwritten by those in this
// CustomerEntity. If 'Fred Jones' didn't already exist, hello entity would be
// added toohello table.
table.Execute(insertOrReplaceOperation);
```

## <a name="query-a-subset-of-entity-properties"></a>Interrogation d’un sous-ensemble de propriétés d’entité
Une requête de table pouvez récupérer seulement quelques propriétés d’une entité au lieu de toutes les propriétés de l’entité hello. Cette technique, nommée « projection », réduit la consommation de bande passante et peut améliorer les performances des requêtes, notamment pour les entités volumineuses. requête Hello hello suivant code retourne uniquement les adresses de messagerie hello d’entités dans la table de hello. Pour ce faire, nous utilisons une requête [DynamicTableEntity][dotnet_DynamicTableEntity] et [EntityResolver][dotnet_EntityResolver]. Plus d’informations sur la projection Bonjour [Upsert de présentation et de Projection de requête billet de blog][blog_post_upsert]. Projection n’est pas prise en charge par l’émulateur de stockage hello, pour que ce code s’exécute uniquement lorsque vous utilisez un compte de service de Table hello.

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Define hello query, and select only hello Email property.
TableQuery<DynamicTableEntity> projectionQuery = new TableQuery<DynamicTableEntity>().Select(new string[] { "Email" });

// Define an entity resolver toowork with hello entity after retrieval.
EntityResolver<string> resolver = (pk, rk, ts, props, etag) => props.ContainsKey("Email") ? props["Email"].StringValue : null;

foreach (string projectedEmail in table.ExecuteQuery(projectionQuery, resolver, null, null))
{
    Console.WriteLine(projectedEmail);
}
```

## <a name="delete-an-entity"></a>Suppression d’une entité
Vous pouvez facilement supprimer une entité une fois que vous l’avez extrait à l’aide de hello même modèle indiqué pour la mise à jour une entité. Hello suivant code récupère et supprime une entité customer.

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that expects a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Assign hello result tooa CustomerEntity.
CustomerEntity deleteEntity = (CustomerEntity)retrievedResult.Result;

// Create hello Delete TableOperation.
if (deleteEntity != null)
{
    TableOperation deleteOperation = TableOperation.Delete(deleteEntity);

    // Execute hello operation.
    table.Execute(deleteOperation);

    Console.WriteLine("Entity deleted.");
}
else
{
    Console.WriteLine("Could not retrieve hello entity.");
}
```

## <a name="delete-a-table"></a>Suppression d’une table
Enfin, hello, exemple de code suivant supprime une table à partir d’un compte de stockage. Une table qui a été supprimée sera indisponible toobe recréée pour une période de temps après la suppression de hello.

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Delete hello table it if exists.
table.DeleteIfExists();
```

## <a name="retrieve-entities-in-pages-asynchronously"></a>Récupérer des entités dans les pages de manière asynchrone
Si vous lisez un grand nombre d’entités, et que vous souhaitez tooprocess/afficher des entités lorsqu’ils sont récupérés, plutôt que d’attendre toutes les tooreturn, vous pouvez récupérer des entités à l’aide d’une requête segmentée. Cet exemple montre comment tooreturn les résultats dans les pages à l’aide de modèle de hello Async-Await afin que l’exécution n’est pas bloquée pendant que vous vous attendez à un grand ensemble de résultats tooreturn. Pour plus d’informations sur l’utilisation de hello modèle Async-Await dans .NET, consultez [programmation asynchrone avec Async et Await (c# et Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx).

```csharp
// Initialize a default TableQuery tooretrieve all hello entities in hello table.
TableQuery<CustomerEntity> tableQuery = new TableQuery<CustomerEntity>();

// Initialize hello continuation token toonull toostart from hello beginning of hello table.
TableContinuationToken continuationToken = null;

do
{
    // Retrieve a segment (up too1,000 entities).
    TableQuerySegment<CustomerEntity> tableQueryResult =
        await table.ExecuteQuerySegmentedAsync(tableQuery, continuationToken);

    // Assign hello new continuation token tootell hello service where to
    // continue on hello next iteration (or null if it has reached hello end).
    continuationToken = tableQueryResult.ContinuationToken;

    // Print hello number of rows retrieved.
    Console.WriteLine("Rows retrieved {0}", tableQueryResult.Results.Count);

// Loop until a null continuation token is received, indicating hello end of hello table.
} while(continuationToken != null);
```

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez appris les notions de base de hello du stockage Table, suivez ces toolearn des liens sur les tâches de stockage plus complexes :

* [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) est une application autonome gratuit, à partir de Microsoft qui vous permet de toowork visuellement avec des données de stockage Azure sur Windows, Mac OS et Linux.
* Pour obtenir des exemples supplémentaires utilisant Table Storage, voir [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/)
* Afficher la documentation de référence de service de Table hello pour plus d’informations sur les API disponibles :
* [Référence de la bibliothèque cliente de stockage pour .NET](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
* [Référence d’API REST](http://msdn.microsoft.com/library/azure/dd179355)
* En savoir plus toosimplify hello code que vous écrivez est comment toowork avec le stockage Azure à l’aide de hello [Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md)
* Permet d’afficher plusieurs toolearn de repères de fonctionnalité sur les options supplémentaires pour le stockage des données dans Azure.
* [Prise en main le stockage Blob Azure à l’aide de .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) toostore des données non structurées.
* [Se connecter tooSQL de base de données à l’aide de .NET (c#)](../sql-database/sql-database-develop-dotnet-simple.md) toostore des données relationnelles.

[Download and install hello Azure SDK for .NET]: /develop/net/
[Creating an Azure Project in Visual Studio]: http://msdn.microsoft.com/library/azure/ee405487.aspx

[blog_post_upsert]: http://blogs.msdn.com/b/windowsazurestorage/archive/2011/09/15/windows-azure-tables-introducing-upsert-and-query-projection.aspx

[dotnet_api_ref]: https://msdn.microsoft.com/library/azure/mt347887.aspx
[dotnet_CloudTableClient]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.cloudtableclient.aspx
[dotnet_CloudTable]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.cloudtable.aspx
[dotnet_CloudTable_Execute]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.cloudtable.execute.aspx
[dotnet_CloudTable_ExecuteBatch]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.cloudtable.executebatch.aspx
[dotnet_DynamicTableEntity]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.dynamictableentity.aspx
[dotnet_EntityResolver]: https://msdn.microsoft.com/library/jj733144.aspx
[dotnet_TableBatchOperation]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tablebatchoperation.aspx
[dotnet_TableBatchOperation_Insert]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tablebatchoperation.insert.aspx
[dotnet_TableEntity]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableentity.aspx
[dotnet_TableOperation]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableoperation.aspx
[dotnet_TableOperation_Insert]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableoperation.insert.aspx
[dotnet_TableOperation_InsertOrReplace]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableoperation.insertorreplace.aspx
[dotnet_TableOperation_Replace]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableoperation.replace.aspx
[dotnet_TableQuery]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tablequery.aspx
[dotnet_TableResult]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableresult.aspx
[dotnet_TableResult_Result]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableresult.result.aspx
