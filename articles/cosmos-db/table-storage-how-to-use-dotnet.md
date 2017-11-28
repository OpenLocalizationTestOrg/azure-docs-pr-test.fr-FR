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
# <a name="get-started-with-azure-table-storage-using-net"></a><span data-ttu-id="090cc-103">Prise en main du stockage de tables Azure à l’aide de .NET</span><span class="sxs-lookup"><span data-stu-id="090cc-103">Get started with Azure Table storage using .NET</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

<span data-ttu-id="090cc-104">Stockage de Table Azure est un service qui stocke NoSQL structuré du magasin de données dans le cloud de hello, en fournissant un attribut key/avec une conception schemaless.</span><span class="sxs-lookup"><span data-stu-id="090cc-104">Azure Table storage is a service that stores structured NoSQL data in hello cloud, providing a key/attribute store with a schemaless design.</span></span> <span data-ttu-id="090cc-105">Stockage de Table schemaless, il est facile tooadapt d’evolve de votre application a besoin de vos données en tant que hello.</span><span class="sxs-lookup"><span data-stu-id="090cc-105">Because Table storage is schemaless, it's easy tooadapt your data as hello needs of your application evolve.</span></span> <span data-ttu-id="090cc-106">Accéder aux données de stockage tooTable est rapide et économique pour de nombreux types d’applications et est généralement inférieur coût SQL traditionnel pour les volumes de données similaires.</span><span class="sxs-lookup"><span data-stu-id="090cc-106">Access tooTable storage data is fast and cost-effective for many types of applications, and is typically lower in cost than traditional SQL for similar volumes of data.</span></span>

<span data-ttu-id="090cc-107">Vous pouvez utiliser la Table stockage toostore flexible des groupes de données comme les données utilisateur pour les applications web, carnets d’adresses, les informations de périphérique ou autres types de votre service requiert des métadonnées.</span><span class="sxs-lookup"><span data-stu-id="090cc-107">You can use Table storage toostore flexible datasets like user data for web applications, address books, device information, or other types of metadata your service requires.</span></span> <span data-ttu-id="090cc-108">Vous pouvez stocker n’importe quel nombre d’entités dans une table, et un compte de stockage peut contenir n’importe quel nombre de tables, des limites de capacité toohello hello du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="090cc-108">You can store any number of entities in a table, and a storage account may contain any number of tables, up toohello capacity limit of hello storage account.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="090cc-109">À propos de ce didacticiel</span><span class="sxs-lookup"><span data-stu-id="090cc-109">About this tutorial</span></span>
<span data-ttu-id="090cc-110">Ce didacticiel vous montre comment toouse hello [bibliothèque cliente de stockage Azure pour .NET](https://www.nuget.org/packages/WindowsAzure.Storage/) dans certains scénarios de stockage Azure Table.</span><span class="sxs-lookup"><span data-stu-id="090cc-110">This tutorial shows you how toouse hello [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/) in some common Azure Table storage scenarios.</span></span> <span data-ttu-id="090cc-111">Ces scénarios sont présentés avec des exemples en C# pour la création et la suppression d’une table, et l’insertion, la mise à jour, la suppression et l’interrogation de données de table.</span><span class="sxs-lookup"><span data-stu-id="090cc-111">These scenarios are presented using C# examples for creating and deleting a table, and inserting, updating, deleting, and querying table data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="090cc-112">Composants requis</span><span class="sxs-lookup"><span data-stu-id="090cc-112">Prerequisites</span></span>

<span data-ttu-id="090cc-113">Vous devez hello suivant toocomplete ce didacticiel avec succès :</span><span class="sxs-lookup"><span data-stu-id="090cc-113">You need hello following toocomplete this tutorial successfully:</span></span>

* [<span data-ttu-id="090cc-114">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="090cc-114">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="090cc-115">Bibliothèque cliente Azure Storage pour .NET</span><span class="sxs-lookup"><span data-stu-id="090cc-115">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="090cc-116">Gestionnaire de configuration Azure pour .NET</span><span class="sxs-lookup"><span data-stu-id="090cc-116">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* [<span data-ttu-id="090cc-117">Compte Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="090cc-117">Azure storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a><span data-ttu-id="090cc-118">Autres exemples</span><span class="sxs-lookup"><span data-stu-id="090cc-118">More samples</span></span>
<span data-ttu-id="090cc-119">Pour obtenir des exemples supplémentaires utilisant Table Storage, voir [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/)(Prise en main d’Azure Table Storage dans .NET).</span><span class="sxs-lookup"><span data-stu-id="090cc-119">For additional examples using Table storage, see [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/).</span></span> <span data-ttu-id="090cc-120">Vous pouvez télécharger l’exemple d’application hello et exécutez-le ou parcourir le code hello sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="090cc-120">You can download hello sample application and run it, or browse hello code on GitHub.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="090cc-121">Ajouter des directives d’utilisation</span><span class="sxs-lookup"><span data-stu-id="090cc-121">Add using directives</span></span>
<span data-ttu-id="090cc-122">Ajoutez hello suivant **à l’aide de** haut toohello de directives de hello `Program.cs` fichier :</span><span class="sxs-lookup"><span data-stu-id="090cc-122">Add hello following **using** directives toohello top of hello `Program.cs` file:</span></span>

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Table; // Namespace for Table storage types
```

### <a name="parse-hello-connection-string"></a><span data-ttu-id="090cc-123">Analyser la chaîne de connexion hello</span><span class="sxs-lookup"><span data-stu-id="090cc-123">Parse hello connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-table-service-client"></a><span data-ttu-id="090cc-124">Créer le client du service de Table hello</span><span class="sxs-lookup"><span data-stu-id="090cc-124">Create hello Table service client</span></span>
<span data-ttu-id="090cc-125">Hello [CloudTableClient] [ dotnet_CloudTableClient] classe vous permet de tooretrieve tables et entités stockées dans le stockage Table.</span><span class="sxs-lookup"><span data-stu-id="090cc-125">hello [CloudTableClient][dotnet_CloudTableClient] class enables you tooretrieve tables and entities stored in Table storage.</span></span> <span data-ttu-id="090cc-126">Voici une façon toocreate hello Table service client :</span><span class="sxs-lookup"><span data-stu-id="090cc-126">Here's one way toocreate hello Table service client:</span></span>

```csharp
// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```

<span data-ttu-id="090cc-127">Vous êtes maintenant code prêt toowrite qui lit les données à partir d’et écrit le stockage des données tooTable.</span><span class="sxs-lookup"><span data-stu-id="090cc-127">Now you are ready toowrite code that reads data from and writes data tooTable storage.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="090cc-128">Création d’une table</span><span class="sxs-lookup"><span data-stu-id="090cc-128">Create a table</span></span>
<span data-ttu-id="090cc-129">Cet exemple montre comment toocreate une table si elle n’existe pas déjà :</span><span class="sxs-lookup"><span data-stu-id="090cc-129">This example shows how toocreate a table if it does not already exist:</span></span>

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

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="090cc-130">Ajouter une table de tooa d’entité</span><span class="sxs-lookup"><span data-stu-id="090cc-130">Add an entity tooa table</span></span>
<span data-ttu-id="090cc-131">Objets tooC # mappent des entités à l’aide d’une classe personnalisée dérivée de [TableEntity][dotnet_TableEntity].</span><span class="sxs-lookup"><span data-stu-id="090cc-131">Entities map tooC# objects by using a custom class derived from [TableEntity][dotnet_TableEntity].</span></span> <span data-ttu-id="090cc-132">tooadd une table de tooa entité, créez une classe qui définit des propriétés de votre entité hello.</span><span class="sxs-lookup"><span data-stu-id="090cc-132">tooadd an entity tooa table, create a class that defines hello properties of your entity.</span></span> <span data-ttu-id="090cc-133">Hello de code suivant définit une classe d’entité qui utilise le prénom du client hello en tant que clé de ligne hello et le nom comme clé de partition hello.</span><span class="sxs-lookup"><span data-stu-id="090cc-133">hello following code defines an entity class that uses hello customer's first name as hello row key and last name as hello partition key.</span></span> <span data-ttu-id="090cc-134">Ensemble, les partitions d’une entité et la clé de ligne identifient uniquement dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="090cc-134">Together, an entity's partition and row key uniquely identify it in hello table.</span></span> <span data-ttu-id="090cc-135">Les entités avec hello même clé de partition peut être interrogé plus rapidement que les entités avec différentes clés de partition, mais à l’aide de clés de partition divers permet une plus grande évolutivité d’opérations parallèles.</span><span class="sxs-lookup"><span data-stu-id="090cc-135">Entities with hello same partition key can be queried faster than entities with different partition keys, but using diverse partition keys allows for greater scalability of parallel operations.</span></span> <span data-ttu-id="090cc-136">Toobe d’entités stockée dans des tables doit être d’un type pris en charge, par exemple dérivé hello [TableEntity] [ dotnet_TableEntity] classe.</span><span class="sxs-lookup"><span data-stu-id="090cc-136">Entities toobe stored in tables must be of a supported type, for example derived from hello [TableEntity][dotnet_TableEntity] class.</span></span> <span data-ttu-id="090cc-137">Propriétés de l’entité vous aimeriez toostore dans une table doivent être des propriétés publiques du type de hello et prend en charge l’obtention et définition des valeurs de.</span><span class="sxs-lookup"><span data-stu-id="090cc-137">Entity properties you'd like toostore in a table must be public properties of hello type, and support both getting and setting of values.</span></span> <span data-ttu-id="090cc-138">De plus, votre type d’entité *doit* exposer un constructeur sans paramètre.</span><span class="sxs-lookup"><span data-stu-id="090cc-138">Also, your entity type *must* expose a parameter-less constructor.</span></span>

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

<span data-ttu-id="090cc-139">Opérations de table qui impliquent des entités sont effectuent via hello [CloudTable] [ dotnet_CloudTable] objet que vous avez créé précédemment dans la section « Créer une table » de hello.</span><span class="sxs-lookup"><span data-stu-id="090cc-139">Table operations that involve entities are performed via hello [CloudTable][dotnet_CloudTable] object that you created earlier in hello "Create a table" section.</span></span> <span data-ttu-id="090cc-140">toobe opération effectuée Hello est représenté par un [TableOperation] [ dotnet_TableOperation] objet.</span><span class="sxs-lookup"><span data-stu-id="090cc-140">hello operation toobe performed is represented by a [TableOperation][dotnet_TableOperation] object.</span></span> <span data-ttu-id="090cc-141">Hello exemple de code suivant illustre la création de hello Hello [CloudTable] [ dotnet_CloudTable] objet, puis un **CustomerEntity** objet.</span><span class="sxs-lookup"><span data-stu-id="090cc-141">hello following code example shows hello creation of hello [CloudTable][dotnet_CloudTable] object and then a **CustomerEntity** object.</span></span> <span data-ttu-id="090cc-142">opération de hello tooprepare, un [TableOperation] [ dotnet_TableOperation] objet est créé entité customer de hello tooinsert dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="090cc-142">tooprepare hello operation, a [TableOperation][dotnet_TableOperation] object is created tooinsert hello customer entity into hello table.</span></span> <span data-ttu-id="090cc-143">Enfin, l’opération de hello est exécutée en appelant [CloudTable][dotnet_CloudTable].[ Exécutez][dotnet_CloudTable_Execute].</span><span class="sxs-lookup"><span data-stu-id="090cc-143">Finally, hello operation is executed by calling [CloudTable][dotnet_CloudTable].[Execute][dotnet_CloudTable_Execute].</span></span>

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

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="090cc-144">Insertion d’un lot d’entités</span><span class="sxs-lookup"><span data-stu-id="090cc-144">Insert a batch of entities</span></span>
<span data-ttu-id="090cc-145">Vous pouvez insérer un lot d'entités dans une table en une seule opération d'écriture.</span><span class="sxs-lookup"><span data-stu-id="090cc-145">You can insert a batch of entities into a table in one write operation.</span></span> <span data-ttu-id="090cc-146">Autres remarques sur les opérations par lot :</span><span class="sxs-lookup"><span data-stu-id="090cc-146">Some other notes on batch operations:</span></span>

* <span data-ttu-id="090cc-147">Vous pouvez effectuer des mises à jour, suppressions et insertions Bonjour même un seul traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="090cc-147">You can perform updates, deletes, and inserts in hello same single batch operation.</span></span>
* <span data-ttu-id="090cc-148">Une opération de lot unique peut inclure des entités de too100.</span><span class="sxs-lookup"><span data-stu-id="090cc-148">A single batch operation can include up too100 entities.</span></span>
* <span data-ttu-id="090cc-149">Toutes les entités dans une seule opération doivent avoir hello même clé de partition.</span><span class="sxs-lookup"><span data-stu-id="090cc-149">All entities in a single batch operation must have hello same partition key.</span></span>
* <span data-ttu-id="090cc-150">Bien qu’il soit possible de tooperform une requête sous la forme d’un traitement par lots, il doit être seule opération de hello dans un lot de hello.</span><span class="sxs-lookup"><span data-stu-id="090cc-150">While it is possible tooperform a query as a batch operation, it must be hello only operation in hello batch.</span></span>

<span data-ttu-id="090cc-151">Hello exemple de code suivant crée deux objets d’entité et l’ajoute chaque trop[TableBatchOperation] [ dotnet_TableBatchOperation] à l’aide de hello [insérer] [ dotnet_TableBatchOperation_Insert] méthode.</span><span class="sxs-lookup"><span data-stu-id="090cc-151">hello following code example creates two entity objects and adds each too[TableBatchOperation][dotnet_TableBatchOperation] by using hello [Insert][dotnet_TableBatchOperation_Insert] method.</span></span> <span data-ttu-id="090cc-152">Ensuite, [CloudTable][dotnet_CloudTable].[ ExecuteBatch] [ dotnet_CloudTable_ExecuteBatch] est appelé l’opération de hello tooexecute.</span><span class="sxs-lookup"><span data-stu-id="090cc-152">Then, [CloudTable][dotnet_CloudTable].[ExecuteBatch][dotnet_CloudTable_ExecuteBatch] is called tooexecute hello operation.</span></span>

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

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="090cc-153">Extraction de toutes les entités d'une partition</span><span class="sxs-lookup"><span data-stu-id="090cc-153">Retrieve all entities in a partition</span></span>
<span data-ttu-id="090cc-154">tooquery une table pour toutes les entités dans une partition, utilisez un [TableQuery] [ dotnet_TableQuery] objet.</span><span class="sxs-lookup"><span data-stu-id="090cc-154">tooquery a table for all entities in a partition, use a [TableQuery][dotnet_TableQuery] object.</span></span> <span data-ttu-id="090cc-155">Hello exemple de code suivant spécifie un filtre pour les entités où « Smith » est la clé de partition hello.</span><span class="sxs-lookup"><span data-stu-id="090cc-155">hello following code example specifies a filter for entities where 'Smith' is hello partition key.</span></span> <span data-ttu-id="090cc-156">Cet exemple imprime les champs de chaque entité dans la console de toohello de résultats de requête hello hello.</span><span class="sxs-lookup"><span data-stu-id="090cc-156">This example prints hello fields of each entity in hello query results toohello console.</span></span>

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

## <a name="retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="090cc-157">Extraction d’un ensemble d’entités dans une partition</span><span class="sxs-lookup"><span data-stu-id="090cc-157">Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="090cc-158">Si vous ne souhaitez pas tooquery toutes les entités dans une partition, vous pouvez spécifier une plage en combinant le filtre de clé de partition hello avec un filtre de clé de ligne.</span><span class="sxs-lookup"><span data-stu-id="090cc-158">If you don't want tooquery all entities in a partition, you can specify a range by combining hello partition key filter with a row key filter.</span></span> <span data-ttu-id="090cc-159">Hello exemple de code suivant utilise deux filtres tooget toutes les entités dans la partition « Smith », où la clé de ligne hello (prénom) commence par une lettre avant « E » dans l’alphabet de hello, puis imprime les résultats de la requête hello.</span><span class="sxs-lookup"><span data-stu-id="090cc-159">hello following code example uses two filters tooget all entities in partition 'Smith' where hello row key (first name) starts with a letter before 'E' in hello alphabet, then prints hello query results.</span></span>

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

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="090cc-160">Extraction d'une seule entité</span><span class="sxs-lookup"><span data-stu-id="090cc-160">Retrieve a single entity</span></span>
<span data-ttu-id="090cc-161">Vous pouvez écrire une requête tooretrieve une entité unique et spécifique.</span><span class="sxs-lookup"><span data-stu-id="090cc-161">You can write a query tooretrieve a single, specific entity.</span></span> <span data-ttu-id="090cc-162">code Hello suivant utilise [TableOperation] [ dotnet_TableOperation] client de hello toospecify « Ben Smith ».</span><span class="sxs-lookup"><span data-stu-id="090cc-162">hello following code uses [TableOperation][dotnet_TableOperation] toospecify hello customer 'Ben Smith'.</span></span> <span data-ttu-id="090cc-163">Cette méthode retourne simplement une entité plutôt qu’une collection et hello a retourné la valeur dans [TableResult][dotnet_TableResult].[ Résultat] [ dotnet_TableResult_Result] est un **CustomerEntity** objet.</span><span class="sxs-lookup"><span data-stu-id="090cc-163">This method returns just one entity rather than a collection, and hello returned value in [TableResult][dotnet_TableResult].[Result][dotnet_TableResult_Result] is a **CustomerEntity** object.</span></span> <span data-ttu-id="090cc-164">Spécification des clés de partition et de ligne dans une requête est tooretrieve de manière plus rapide hello une seule entité hello service de Table.</span><span class="sxs-lookup"><span data-stu-id="090cc-164">Specifying both partition and row keys in a query is hello fastest way tooretrieve a single entity from hello Table service.</span></span>

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

## <a name="replace-an-entity"></a><span data-ttu-id="090cc-165">Remplacement d’une entité</span><span class="sxs-lookup"><span data-stu-id="090cc-165">Replace an entity</span></span>
<span data-ttu-id="090cc-166">tooupdate une entité, récupérer à partir du service de Table hello, modifier l’objet d’entité hello, puis enregistrez les modifications hello de nouveau service de Table toohello.</span><span class="sxs-lookup"><span data-stu-id="090cc-166">tooupdate an entity, retrieve it from hello Table service, modify hello entity object, and then save hello changes back toohello Table service.</span></span> <span data-ttu-id="090cc-167">Hello code suivant modifie un numéro de téléphone existant.</span><span class="sxs-lookup"><span data-stu-id="090cc-167">hello following code changes an existing customer's phone number.</span></span> <span data-ttu-id="090cc-168">Au lieu d’appeler la méthode [Insert][dotnet_TableOperation_Insert], ce code utilise la méthode [Replace][dotnet_TableOperation_Replace].</span><span class="sxs-lookup"><span data-stu-id="090cc-168">Instead of calling [Insert][dotnet_TableOperation_Insert], this code uses [Replace][dotnet_TableOperation_Replace].</span></span> <span data-ttu-id="090cc-169">[Remplacez] [ dotnet_TableOperation_Replace] causes hello toobe entité entièrement remplacé sur le serveur de hello, sauf si l’entité hello sur le serveur de hello a changé depuis sa récupération, auquel cas hello échoue.</span><span class="sxs-lookup"><span data-stu-id="090cc-169">[Replace][dotnet_TableOperation_Replace] causes hello entity toobe fully replaced on hello server, unless hello entity on hello server has changed since it was retrieved, in which case hello operation will fail.</span></span> <span data-ttu-id="090cc-170">Cet échec est tooprevent votre application à partir de remplacement accidentel d’une modification effectuée entre hello récupération et mettre à jour par un autre composant de votre application.</span><span class="sxs-lookup"><span data-stu-id="090cc-170">This failure is tooprevent your application from inadvertently overwriting a change made between hello retrieval and update by another component of your application.</span></span> <span data-ttu-id="090cc-171">Hello gestion correcte de cet échec est tooretrieve hello entité à nouveau, apportez vos modifications (si elle est toujours valide), puis effectuer une autre [remplacer] [ dotnet_TableOperation_Replace] opération.</span><span class="sxs-lookup"><span data-stu-id="090cc-171">hello proper handling of this failure is tooretrieve hello entity again, make your changes (if still valid), and then perform another [Replace][dotnet_TableOperation_Replace] operation.</span></span> <span data-ttu-id="090cc-172">Hello prochaine section vous montrera comment toooverride ce comportement.</span><span class="sxs-lookup"><span data-stu-id="090cc-172">hello next section will show you how toooverride this behavior.</span></span>

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

## <a name="insert-or-replace-an-entity"></a><span data-ttu-id="090cc-173">Insertion ou remplacement d’une entité</span><span class="sxs-lookup"><span data-stu-id="090cc-173">Insert-or-replace an entity</span></span>
<span data-ttu-id="090cc-174">[Remplacez] [ dotnet_TableOperation_Replace] opérations échouent si l’entité de hello a été modifiée, car il a été récupéré à partir du serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="090cc-174">[Replace][dotnet_TableOperation_Replace] operations will fail if hello entity has been changed since it was retrieved from hello server.</span></span> <span data-ttu-id="090cc-175">En outre, vous devez extraire votre entité hello du serveur de hello tout d’abord dans l’ordre pour hello [remplacer] [ dotnet_TableOperation_Replace] toobe opération réussie.</span><span class="sxs-lookup"><span data-stu-id="090cc-175">Furthermore, you must retrieve hello entity from hello server first in order for hello [Replace][dotnet_TableOperation_Replace] operation toobe successful.</span></span> <span data-ttu-id="090cc-176">Dans certains cas, toutefois, vous ne connaissez pas si l’entité hello existe sur le serveur de hello et les valeurs actuelles hello stockés qu’il contient sont sans importance.</span><span class="sxs-lookup"><span data-stu-id="090cc-176">Sometimes, however, you don't know if hello entity exists on hello server and hello current values stored in it are irrelevant.</span></span> <span data-ttu-id="090cc-177">Votre mise à jour doit donc toutes les remplacer.</span><span class="sxs-lookup"><span data-stu-id="090cc-177">Your update should overwrite them all.</span></span> <span data-ttu-id="090cc-178">tooaccomplish, vous devez utiliser un [InsertOrReplace] [ dotnet_TableOperation_InsertOrReplace] opération.</span><span class="sxs-lookup"><span data-stu-id="090cc-178">tooaccomplish this, you would use an [InsertOrReplace][dotnet_TableOperation_InsertOrReplace] operation.</span></span> <span data-ttu-id="090cc-179">Cette opération insère l’entité de hello si elle n’existe pas ou elle remplace dans ce cas, quelle que soit la lorsque la dernière mise à jour de hello a été effectuée.</span><span class="sxs-lookup"><span data-stu-id="090cc-179">This operation inserts hello entity if it doesn't exist, or replaces it if it does, regardless of when hello last update was made.</span></span>

<span data-ttu-id="090cc-180">Bonjour exemple de code suivant, une entité customer pour 'Fred Jones' est créée et insérée dans la table « people » de hello.</span><span class="sxs-lookup"><span data-stu-id="090cc-180">In hello following code example, a customer entity for 'Fred Jones' is created and inserted into hello 'people' table.</span></span> <span data-ttu-id="090cc-181">Ensuite, nous utilisons hello [InsertOrReplace] [ dotnet_TableOperation_InsertOrReplace] opération toosave une entité avec hello même clé de partition (Jones) et une ligne de clé serveur de toohello (Fred), cette fois avec une valeur différente pour hello PhoneNumber propriété.</span><span class="sxs-lookup"><span data-stu-id="090cc-181">Next, we use hello [InsertOrReplace][dotnet_TableOperation_InsertOrReplace] operation toosave an entity with hello same partition key (Jones) and row key (Fred) toohello server, this time with a different value for hello PhoneNumber property.</span></span> <span data-ttu-id="090cc-182">Comme nous utilisons [InsertOrReplace][dotnet_TableOperation_InsertOrReplace], toutes ses valeurs de propriété sont remplacées.</span><span class="sxs-lookup"><span data-stu-id="090cc-182">Because we use [InsertOrReplace][dotnet_TableOperation_InsertOrReplace], all of its property values are replaced.</span></span> <span data-ttu-id="090cc-183">Toutefois, si une entité 'Fred Jones' n’était pas existait déjà dans la table de hello, il serait ont été inséré.</span><span class="sxs-lookup"><span data-stu-id="090cc-183">However, if a 'Fred Jones' entity hadn't already existed in hello table, it would have been inserted.</span></span>

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

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="090cc-184">Interrogation d’un sous-ensemble de propriétés d’entité</span><span class="sxs-lookup"><span data-stu-id="090cc-184">Query a subset of entity properties</span></span>
<span data-ttu-id="090cc-185">Une requête de table pouvez récupérer seulement quelques propriétés d’une entité au lieu de toutes les propriétés de l’entité hello.</span><span class="sxs-lookup"><span data-stu-id="090cc-185">A table query can retrieve just a few properties from an entity instead of all hello entity properties.</span></span> <span data-ttu-id="090cc-186">Cette technique, nommée « projection », réduit la consommation de bande passante et peut améliorer les performances des requêtes, notamment pour les entités volumineuses.</span><span class="sxs-lookup"><span data-stu-id="090cc-186">This technique, called projection, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="090cc-187">requête Hello hello suivant code retourne uniquement les adresses de messagerie hello d’entités dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="090cc-187">hello query in hello following code returns only hello email addresses of entities in hello table.</span></span> <span data-ttu-id="090cc-188">Pour ce faire, nous utilisons une requête [DynamicTableEntity][dotnet_DynamicTableEntity] et [EntityResolver][dotnet_EntityResolver].</span><span class="sxs-lookup"><span data-stu-id="090cc-188">This is done by using a query of [DynamicTableEntity][dotnet_DynamicTableEntity] and also [EntityResolver][dotnet_EntityResolver].</span></span> <span data-ttu-id="090cc-189">Plus d’informations sur la projection Bonjour [Upsert de présentation et de Projection de requête billet de blog][blog_post_upsert].</span><span class="sxs-lookup"><span data-stu-id="090cc-189">You can learn more about projection in hello [Introducing Upsert and Query Projection blog post][blog_post_upsert].</span></span> <span data-ttu-id="090cc-190">Projection n’est pas prise en charge par l’émulateur de stockage hello, pour que ce code s’exécute uniquement lorsque vous utilisez un compte de service de Table hello.</span><span class="sxs-lookup"><span data-stu-id="090cc-190">Projection is not supported by hello storage emulator, so this code runs only when you're using an account in hello Table service.</span></span>

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

## <a name="delete-an-entity"></a><span data-ttu-id="090cc-191">Suppression d’une entité</span><span class="sxs-lookup"><span data-stu-id="090cc-191">Delete an entity</span></span>
<span data-ttu-id="090cc-192">Vous pouvez facilement supprimer une entité une fois que vous l’avez extrait à l’aide de hello même modèle indiqué pour la mise à jour une entité.</span><span class="sxs-lookup"><span data-stu-id="090cc-192">You can easily delete an entity after you have retrieved it by using hello same pattern shown for updating an entity.</span></span> <span data-ttu-id="090cc-193">Hello suivant code récupère et supprime une entité customer.</span><span class="sxs-lookup"><span data-stu-id="090cc-193">hello following code retrieves and deletes a customer entity.</span></span>

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

## <a name="delete-a-table"></a><span data-ttu-id="090cc-194">Suppression d’une table</span><span class="sxs-lookup"><span data-stu-id="090cc-194">Delete a table</span></span>
<span data-ttu-id="090cc-195">Enfin, hello, exemple de code suivant supprime une table à partir d’un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="090cc-195">Finally, hello following code example deletes a table from a storage account.</span></span> <span data-ttu-id="090cc-196">Une table qui a été supprimée sera indisponible toobe recréée pour une période de temps après la suppression de hello.</span><span class="sxs-lookup"><span data-stu-id="090cc-196">A table that has been deleted will be unavailable toobe re-created for a period of time following hello deletion.</span></span>

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

## <a name="retrieve-entities-in-pages-asynchronously"></a><span data-ttu-id="090cc-197">Récupérer des entités dans les pages de manière asynchrone</span><span class="sxs-lookup"><span data-stu-id="090cc-197">Retrieve entities in pages asynchronously</span></span>
<span data-ttu-id="090cc-198">Si vous lisez un grand nombre d’entités, et que vous souhaitez tooprocess/afficher des entités lorsqu’ils sont récupérés, plutôt que d’attendre toutes les tooreturn, vous pouvez récupérer des entités à l’aide d’une requête segmentée.</span><span class="sxs-lookup"><span data-stu-id="090cc-198">If you are reading a large number of entities, and you want tooprocess/display entities as they are retrieved rather than waiting for them all tooreturn, you can retrieve entities by using a segmented query.</span></span> <span data-ttu-id="090cc-199">Cet exemple montre comment tooreturn les résultats dans les pages à l’aide de modèle de hello Async-Await afin que l’exécution n’est pas bloquée pendant que vous vous attendez à un grand ensemble de résultats tooreturn.</span><span class="sxs-lookup"><span data-stu-id="090cc-199">This example shows how tooreturn results in pages by using hello Async-Await pattern so that execution is not blocked while you're waiting for a large set of results tooreturn.</span></span> <span data-ttu-id="090cc-200">Pour plus d’informations sur l’utilisation de hello modèle Async-Await dans .NET, consultez [programmation asynchrone avec Async et Await (c# et Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx).</span><span class="sxs-lookup"><span data-stu-id="090cc-200">For more details on using hello Async-Await pattern in .NET, see [Asynchronous programming with Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx).</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="090cc-201">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="090cc-201">Next steps</span></span>
<span data-ttu-id="090cc-202">Maintenant que vous avez appris les notions de base de hello du stockage Table, suivez ces toolearn des liens sur les tâches de stockage plus complexes :</span><span class="sxs-lookup"><span data-stu-id="090cc-202">Now that you've learned hello basics of Table storage, follow these links toolearn about more complex storage tasks:</span></span>

* <span data-ttu-id="090cc-203">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) est une application autonome gratuit, à partir de Microsoft qui vous permet de toowork visuellement avec des données de stockage Azure sur Windows, Mac OS et Linux.</span><span class="sxs-lookup"><span data-stu-id="090cc-203">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="090cc-204">Pour obtenir des exemples supplémentaires utilisant Table Storage, voir [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/)</span><span class="sxs-lookup"><span data-stu-id="090cc-204">See more Table storage samples in [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/)</span></span>
* <span data-ttu-id="090cc-205">Afficher la documentation de référence de service de Table hello pour plus d’informations sur les API disponibles :</span><span class="sxs-lookup"><span data-stu-id="090cc-205">View hello Table service reference documentation for complete details about available APIs:</span></span>
* [<span data-ttu-id="090cc-206">Référence de la bibliothèque cliente de stockage pour .NET</span><span class="sxs-lookup"><span data-stu-id="090cc-206">Storage Client Library for .NET reference</span></span>](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
* [<span data-ttu-id="090cc-207">Référence d’API REST</span><span class="sxs-lookup"><span data-stu-id="090cc-207">REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="090cc-208">En savoir plus toosimplify hello code que vous écrivez est comment toowork avec le stockage Azure à l’aide de hello [Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="090cc-208">Learn how toosimplify hello code you write toowork with Azure Storage by using hello [Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md)</span></span>
* <span data-ttu-id="090cc-209">Permet d’afficher plusieurs toolearn de repères de fonctionnalité sur les options supplémentaires pour le stockage des données dans Azure.</span><span class="sxs-lookup"><span data-stu-id="090cc-209">View more feature guides toolearn about additional options for storing data in Azure.</span></span>
* <span data-ttu-id="090cc-210">[Prise en main le stockage Blob Azure à l’aide de .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) toostore des données non structurées.</span><span class="sxs-lookup"><span data-stu-id="090cc-210">[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) toostore unstructured data.</span></span>
* <span data-ttu-id="090cc-211">[Se connecter tooSQL de base de données à l’aide de .NET (c#)](../sql-database/sql-database-develop-dotnet-simple.md) toostore des données relationnelles.</span><span class="sxs-lookup"><span data-stu-id="090cc-211">[Connect tooSQL Database by using .NET (C#)](../sql-database/sql-database-develop-dotnet-simple.md) toostore relational data.</span></span>

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
