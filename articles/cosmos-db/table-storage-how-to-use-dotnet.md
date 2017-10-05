---
title: "Prise en main du stockage de tables Azure à l’aide de .NET | Microsoft Docs"
description: "Stockez des données structurées dans le cloud à l’aide du stockage de tables Azure, un magasin de données NoSQL."
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
ms.openlocfilehash: ab77fe512d275a92da19bb5dc03da347922238a5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-table-storage-using-net"></a><span data-ttu-id="12f28-103">Prise en main du stockage de tables Azure à l’aide de .NET</span><span class="sxs-lookup"><span data-stu-id="12f28-103">Get started with Azure Table storage using .NET</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

<span data-ttu-id="12f28-104">Le Stockage Table Azure est un service qui stocke des données NoSQL structurées dans le cloud, en fournissant une conception sans schéma à un magasin de clés/attributs.</span><span class="sxs-lookup"><span data-stu-id="12f28-104">Azure Table storage is a service that stores structured NoSQL data in the cloud, providing a key/attribute store with a schemaless design.</span></span> <span data-ttu-id="12f28-105">Comme le stockage de tables est sans schéma, il est aisé d’adapter vos données en fonction des besoins de votre application.</span><span class="sxs-lookup"><span data-stu-id="12f28-105">Because Table storage is schemaless, it's easy to adapt your data as the needs of your application evolve.</span></span> <span data-ttu-id="12f28-106">L’accès aux données du Stockage Table est rapide et économique pour de nombreux types d’applications, et généralement moins coûteux que le SQL traditionnel pour des volumes de données similaires.</span><span class="sxs-lookup"><span data-stu-id="12f28-106">Access to Table storage data is fast and cost-effective for many types of applications, and is typically lower in cost than traditional SQL for similar volumes of data.</span></span>

<span data-ttu-id="12f28-107">Vous pouvez utiliser le Stockage Table pour stocker des jeux de données flexibles, comme des données utilisateur pour des applications Web, des carnets d’adresses, des informations sur les périphériques ou d’autres types de métadonnées requis par votre service.</span><span class="sxs-lookup"><span data-stu-id="12f28-107">You can use Table storage to store flexible datasets like user data for web applications, address books, device information, or other types of metadata your service requires.</span></span> <span data-ttu-id="12f28-108">Vous pouvez stocker un nombre quelconque d'entités dans une table, et un compte de stockage peut contenir un nombre quelconque de tables, jusqu'à la limite de capacité du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="12f28-108">You can store any number of entities in a table, and a storage account may contain any number of tables, up to the capacity limit of the storage account.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="12f28-109">À propos de ce didacticiel</span><span class="sxs-lookup"><span data-stu-id="12f28-109">About this tutorial</span></span>
<span data-ttu-id="12f28-110">Ce didacticiel montre comment utiliser la [bibliothèque cliente de Stockage Azure pour .NET](https://www.nuget.org/packages/WindowsAzure.Storage/) dans certains des scénarios courants du Stockage Table Azure.</span><span class="sxs-lookup"><span data-stu-id="12f28-110">This tutorial shows you how to use the [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/) in some common Azure Table storage scenarios.</span></span> <span data-ttu-id="12f28-111">Ces scénarios sont présentés avec des exemples en C# pour la création et la suppression d’une table, et l’insertion, la mise à jour, la suppression et l’interrogation de données de table.</span><span class="sxs-lookup"><span data-stu-id="12f28-111">These scenarios are presented using C# examples for creating and deleting a table, and inserting, updating, deleting, and querying table data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="12f28-112">Composants requis</span><span class="sxs-lookup"><span data-stu-id="12f28-112">Prerequisites</span></span>

<span data-ttu-id="12f28-113">Vous aurez besoin des éléments suivants pour suivre ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="12f28-113">You need the following to complete this tutorial successfully:</span></span>

* [<span data-ttu-id="12f28-114">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="12f28-114">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="12f28-115">Bibliothèque cliente Azure Storage pour .NET</span><span class="sxs-lookup"><span data-stu-id="12f28-115">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="12f28-116">Gestionnaire de configuration Azure pour .NET</span><span class="sxs-lookup"><span data-stu-id="12f28-116">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* [<span data-ttu-id="12f28-117">Compte Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="12f28-117">Azure storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a><span data-ttu-id="12f28-118">Autres exemples</span><span class="sxs-lookup"><span data-stu-id="12f28-118">More samples</span></span>
<span data-ttu-id="12f28-119">Pour obtenir des exemples supplémentaires utilisant Table Storage, voir [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/)(Prise en main d’Azure Table Storage dans .NET).</span><span class="sxs-lookup"><span data-stu-id="12f28-119">For additional examples using Table storage, see [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/).</span></span> <span data-ttu-id="12f28-120">Vous pouvez télécharger l’exemple d’application et l’exécuter ou parcourir le code sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="12f28-120">You can download the sample application and run it, or browse the code on GitHub.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="12f28-121">Ajouter des directives d’utilisation</span><span class="sxs-lookup"><span data-stu-id="12f28-121">Add using directives</span></span>
<span data-ttu-id="12f28-122">Ajoutez les directives **d’utilisation** suivantes au fichier `Program.cs` :</span><span class="sxs-lookup"><span data-stu-id="12f28-122">Add the following **using** directives to the top of the `Program.cs` file:</span></span>

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Table; // Namespace for Table storage types
```

### <a name="parse-the-connection-string"></a><span data-ttu-id="12f28-123">Analyse de la chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="12f28-123">Parse the connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-the-table-service-client"></a><span data-ttu-id="12f28-124">Création du client du service de Table</span><span class="sxs-lookup"><span data-stu-id="12f28-124">Create the Table service client</span></span>
<span data-ttu-id="12f28-125">La classe [CloudTableClient][dotnet_CloudTableClient] vous permet de récupérer des tables et entités stockées dans le Stockage Table.</span><span class="sxs-lookup"><span data-stu-id="12f28-125">The [CloudTableClient][dotnet_CloudTableClient] class enables you to retrieve tables and entities stored in Table storage.</span></span> <span data-ttu-id="12f28-126">Voici un moyen de créer le client du service de Table :</span><span class="sxs-lookup"><span data-stu-id="12f28-126">Here's one way to create the Table service client:</span></span>

```csharp
// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```

<span data-ttu-id="12f28-127">Vous êtes maintenant prêt à écrire du code qui lit et écrit des données dans Table Storage.</span><span class="sxs-lookup"><span data-stu-id="12f28-127">Now you are ready to write code that reads data from and writes data to Table storage.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="12f28-128">Création d’une table</span><span class="sxs-lookup"><span data-stu-id="12f28-128">Create a table</span></span>
<span data-ttu-id="12f28-129">Cet exemple montre comment créer une table, si elle n’existe pas encore :</span><span class="sxs-lookup"><span data-stu-id="12f28-129">This example shows how to create a table if it does not already exist:</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Retrieve a reference to the table.
CloudTable table = tableClient.GetTableReference("people");

// Create the table if it doesn't exist.
table.CreateIfNotExists();
```

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="12f28-130">Ajout d'une entité à une table</span><span class="sxs-lookup"><span data-stu-id="12f28-130">Add an entity to a table</span></span>
<span data-ttu-id="12f28-131">Les entités mappent vers les objets C# en utilisant une classe personnalisée dérivée d’une [TableEntity][dotnet_TableEntity].</span><span class="sxs-lookup"><span data-stu-id="12f28-131">Entities map to C# objects by using a custom class derived from [TableEntity][dotnet_TableEntity].</span></span> <span data-ttu-id="12f28-132">Pour ajouter une entité à une table, créez une classe définissant les propriétés de votre entité.</span><span class="sxs-lookup"><span data-stu-id="12f28-132">To add an entity to a table, create a class that defines the properties of your entity.</span></span> <span data-ttu-id="12f28-133">Le code suivant définit une classe d’entité utilisant le prénom du client en tant que clé de ligne et son nom de famille en tant que clé de partition.</span><span class="sxs-lookup"><span data-stu-id="12f28-133">The following code defines an entity class that uses the customer's first name as the row key and last name as the partition key.</span></span> <span data-ttu-id="12f28-134">Ensemble, les clés de partition et de ligne d’une entité l’identifient de façon unique dans la table.</span><span class="sxs-lookup"><span data-stu-id="12f28-134">Together, an entity's partition and row key uniquely identify it in the table.</span></span> <span data-ttu-id="12f28-135">Les requêtes d’entités dont les clés de partition sont identiques sont plus rapides que les entités dont les clés de partition sont différentes, mais le fait d’utiliser différentes clés de partition améliore l’extensibilité des opérations parallèles.</span><span class="sxs-lookup"><span data-stu-id="12f28-135">Entities with the same partition key can be queried faster than entities with different partition keys, but using diverse partition keys allows for greater scalability of parallel operations.</span></span> <span data-ttu-id="12f28-136">Les entités à stocker dans des tables doivent être d’un type pris en charge, par exemple dérivées de la classe [TableEntity][dotnet_TableEntity].</span><span class="sxs-lookup"><span data-stu-id="12f28-136">Entities to be stored in tables must be of a supported type, for example derived from the [TableEntity][dotnet_TableEntity] class.</span></span> <span data-ttu-id="12f28-137">Les propriétés de l’entité à stocker dans une table doivent être des propriétés publiques du type et prendre en charge la récupération et la définition de valeurs.</span><span class="sxs-lookup"><span data-stu-id="12f28-137">Entity properties you'd like to store in a table must be public properties of the type, and support both getting and setting of values.</span></span> <span data-ttu-id="12f28-138">De plus, votre type d’entité *doit* exposer un constructeur sans paramètre.</span><span class="sxs-lookup"><span data-stu-id="12f28-138">Also, your entity type *must* expose a parameter-less constructor.</span></span>

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

<span data-ttu-id="12f28-139">Les opérations de table qui impliquent des entités sont effectuées par le biais de l’objet [CloudTable][dotnet_CloudTable] que vous avez créé précédemment dans la section « Création d’une table ».</span><span class="sxs-lookup"><span data-stu-id="12f28-139">Table operations that involve entities are performed via the [CloudTable][dotnet_CloudTable] object that you created earlier in the "Create a table" section.</span></span> <span data-ttu-id="12f28-140">L’opération à effectuer est représentée par un objet [TableOperation][dotnet_TableOperation].</span><span class="sxs-lookup"><span data-stu-id="12f28-140">The operation to be performed is represented by a [TableOperation][dotnet_TableOperation] object.</span></span> <span data-ttu-id="12f28-141">L’exemple de code suivant illustre la création des objets [CloudTable][dotnet_CloudTable] et **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="12f28-141">The following code example shows the creation of the [CloudTable][dotnet_CloudTable] object and then a **CustomerEntity** object.</span></span> <span data-ttu-id="12f28-142">Pour préparer l’opération, un objet [TableOperation][dotnet_TableOperation] est créé afin d’insérer l’entité du client dans la table.</span><span class="sxs-lookup"><span data-stu-id="12f28-142">To prepare the operation, a [TableOperation][dotnet_TableOperation] object is created to insert the customer entity into the table.</span></span> <span data-ttu-id="12f28-143">Finalement, l’opération est exécutée en appelant [CloudTable][dotnet_CloudTable].[Execute][dotnet_CloudTable_Execute].</span><span class="sxs-lookup"><span data-stu-id="12f28-143">Finally, the operation is executed by calling [CloudTable][dotnet_CloudTable].[Execute][dotnet_CloudTable_Execute].</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a new customer entity.
CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
customer1.Email = "Walter@contoso.com";
customer1.PhoneNumber = "425-555-0101";

// Create the TableOperation object that inserts the customer entity.
TableOperation insertOperation = TableOperation.Insert(customer1);

// Execute the insert operation.
table.Execute(insertOperation);
```

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="12f28-144">Insertion d’un lot d’entités</span><span class="sxs-lookup"><span data-stu-id="12f28-144">Insert a batch of entities</span></span>
<span data-ttu-id="12f28-145">Vous pouvez insérer un lot d'entités dans une table en une seule opération d'écriture.</span><span class="sxs-lookup"><span data-stu-id="12f28-145">You can insert a batch of entities into a table in one write operation.</span></span> <span data-ttu-id="12f28-146">Autres remarques sur les opérations par lot :</span><span class="sxs-lookup"><span data-stu-id="12f28-146">Some other notes on batch operations:</span></span>

* <span data-ttu-id="12f28-147">Vous pouvez effectuer des mises à jour, des suppressions et des insertions dans la même opération par lot.</span><span class="sxs-lookup"><span data-stu-id="12f28-147">You can perform updates, deletes, and inserts in the same single batch operation.</span></span>
* <span data-ttu-id="12f28-148">Une seule opération par lot peut inclure jusqu’à 100 entités.</span><span class="sxs-lookup"><span data-stu-id="12f28-148">A single batch operation can include up to 100 entities.</span></span>
* <span data-ttu-id="12f28-149">Toutes les entités d'une opération par lot doivent avoir la même clé de partition.</span><span class="sxs-lookup"><span data-stu-id="12f28-149">All entities in a single batch operation must have the same partition key.</span></span>
* <span data-ttu-id="12f28-150">Même s'il est possible d'exécuter une requête en tant qu'opération par lot, il doit s'agir de la seule opération du lot.</span><span class="sxs-lookup"><span data-stu-id="12f28-150">While it is possible to perform a query as a batch operation, it must be the only operation in the batch.</span></span>

<span data-ttu-id="12f28-151">L’exemple de code suivant crée deux objets d’entité et ajoute chacun d’eux à [TableBatchOperation][dotnet_TableBatchOperation] en utilisant la méthode [Insert][dotnet_TableBatchOperation_Insert].</span><span class="sxs-lookup"><span data-stu-id="12f28-151">The following code example creates two entity objects and adds each to [TableBatchOperation][dotnet_TableBatchOperation] by using the [Insert][dotnet_TableBatchOperation_Insert] method.</span></span> <span data-ttu-id="12f28-152">La méthode [CloudTable][dotnet_CloudTable].[ExecuteBatch][dotnet_CloudTable_ExecuteBatch] est ensuite appelée pour exécuter l’opération.</span><span class="sxs-lookup"><span data-stu-id="12f28-152">Then, [CloudTable][dotnet_CloudTable].[ExecuteBatch][dotnet_CloudTable_ExecuteBatch] is called to execute the operation.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create the batch operation.
TableBatchOperation batchOperation = new TableBatchOperation();

// Create a customer entity and add it to the table.
CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
customer1.Email = "Jeff@contoso.com";
customer1.PhoneNumber = "425-555-0104";

// Create another customer entity and add it to the table.
CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
customer2.Email = "Ben@contoso.com";
customer2.PhoneNumber = "425-555-0102";

// Add both customer entities to the batch insert operation.
batchOperation.Insert(customer1);
batchOperation.Insert(customer2);

// Execute the batch operation.
table.ExecuteBatch(batchOperation);
```

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="12f28-153">Extraction de toutes les entités d'une partition</span><span class="sxs-lookup"><span data-stu-id="12f28-153">Retrieve all entities in a partition</span></span>
<span data-ttu-id="12f28-154">Pour exécuter une requête de table pour toutes les entités d’une partition, utilisez un objet [TableQuery][dotnet_TableQuery].</span><span class="sxs-lookup"><span data-stu-id="12f28-154">To query a table for all entities in a partition, use a [TableQuery][dotnet_TableQuery] object.</span></span> <span data-ttu-id="12f28-155">L’exemple de code suivant indique un filtre pour les entités où ’Smith’ est la clé de partition.</span><span class="sxs-lookup"><span data-stu-id="12f28-155">The following code example specifies a filter for entities where 'Smith' is the partition key.</span></span> <span data-ttu-id="12f28-156">Il imprime les champs de chaque entité dans les résultats de requête vers la console.</span><span class="sxs-lookup"><span data-stu-id="12f28-156">This example prints the fields of each entity in the query results to the console.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Construct the query operation for all customer entities where PartitionKey="Smith".
TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>().Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

// Print the fields for each customer.
foreach (CustomerEntity entity in table.ExecuteQuery(query))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

## <a name="retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="12f28-157">Extraction d’un ensemble d’entités dans une partition</span><span class="sxs-lookup"><span data-stu-id="12f28-157">Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="12f28-158">Si vous ne voulez pas exécuter une requête pour toutes les entités d’une partition, vous pouvez spécifier un ensemble en combinant le filtre de clé de partition avec un filtre de clé de ligne.</span><span class="sxs-lookup"><span data-stu-id="12f28-158">If you don't want to query all entities in a partition, you can specify a range by combining the partition key filter with a row key filter.</span></span> <span data-ttu-id="12f28-159">L’exemple de code suivant utilise deux filtres pour obtenir toutes les entités dans la partition « Smith » où la clé de ligne (prénom) commence par une lettre située avant la lettre « E » dans l’ordre alphabétique, puis imprime les résultats de la requête.</span><span class="sxs-lookup"><span data-stu-id="12f28-159">The following code example uses two filters to get all entities in partition 'Smith' where the row key (first name) starts with a letter before 'E' in the alphabet, then prints the query results.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create the table query.
TableQuery<CustomerEntity> rangeQuery = new TableQuery<CustomerEntity>().Where(
    TableQuery.CombineFilters(
        TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"),
        TableOperators.And,
        TableQuery.GenerateFilterCondition("RowKey", QueryComparisons.LessThan, "E")));

// Loop through the results, displaying information about the entity.
foreach (CustomerEntity entity in table.ExecuteQuery(rangeQuery))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="12f28-160">Extraction d'une seule entité</span><span class="sxs-lookup"><span data-stu-id="12f28-160">Retrieve a single entity</span></span>
<span data-ttu-id="12f28-161">Vous pouvez écrire une requête pour extraire une seule entité.</span><span class="sxs-lookup"><span data-stu-id="12f28-161">You can write a query to retrieve a single, specific entity.</span></span> <span data-ttu-id="12f28-162">Le code suivant utilise [TableOperation][dotnet_TableOperation] pour spécifier le client « Ben Smith ».</span><span class="sxs-lookup"><span data-stu-id="12f28-162">The following code uses [TableOperation][dotnet_TableOperation] to specify the customer 'Ben Smith'.</span></span> <span data-ttu-id="12f28-163">Cette méthode renvoie une seule entité (et non une collection). De plus, la valeur renvoyée dans [TableResult][dotnet_TableResult].[Result][dotnet_TableResult_Result] est un objet **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="12f28-163">This method returns just one entity rather than a collection, and the returned value in [TableResult][dotnet_TableResult].[Result][dotnet_TableResult_Result] is a **CustomerEntity** object.</span></span> <span data-ttu-id="12f28-164">La méthode la plus rapide pour extraire une seule entité dans le service de Table consiste à spécifier une clé de partition et une clé de ligne.</span><span class="sxs-lookup"><span data-stu-id="12f28-164">Specifying both partition and row keys in a query is the fastest way to retrieve a single entity from the Table service.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute the retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Print the phone number of the result.
if (retrievedResult.Result != null)
{
    Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
}
else
{
    Console.WriteLine("The phone number could not be retrieved.");
}
```

## <a name="replace-an-entity"></a><span data-ttu-id="12f28-165">Remplacement d’une entité</span><span class="sxs-lookup"><span data-stu-id="12f28-165">Replace an entity</span></span>
<span data-ttu-id="12f28-166">Pour mettre à jour une entité, récupérez-la du service de Table, modifiez l’objet d’entité, puis enregistrez les modifications dans le service de Table.</span><span class="sxs-lookup"><span data-stu-id="12f28-166">To update an entity, retrieve it from the Table service, modify the entity object, and then save the changes back to the Table service.</span></span> <span data-ttu-id="12f28-167">Le code suivant modifie le numéro de téléphone d'un client existant.</span><span class="sxs-lookup"><span data-stu-id="12f28-167">The following code changes an existing customer's phone number.</span></span> <span data-ttu-id="12f28-168">Au lieu d’appeler la méthode [Insert][dotnet_TableOperation_Insert], ce code utilise la méthode [Replace][dotnet_TableOperation_Replace].</span><span class="sxs-lookup"><span data-stu-id="12f28-168">Instead of calling [Insert][dotnet_TableOperation_Insert], this code uses [Replace][dotnet_TableOperation_Replace].</span></span> <span data-ttu-id="12f28-169">[Replace][dotnet_TableOperation_Replace] entraîne le remplacement complet de l’entité sur le serveur, sauf si cette dernière a été modifiée depuis sa récupération, auquel cas l’opération échoue.</span><span class="sxs-lookup"><span data-stu-id="12f28-169">[Replace][dotnet_TableOperation_Replace] causes the entity to be fully replaced on the server, unless the entity on the server has changed since it was retrieved, in which case the operation will fail.</span></span> <span data-ttu-id="12f28-170">Cet échec survient pour empêcher votre application de remplacer par erreur une modification apportée entre la récupération et la mise à jour par un autre composant de votre application.</span><span class="sxs-lookup"><span data-stu-id="12f28-170">This failure is to prevent your application from inadvertently overwriting a change made between the retrieval and update by another component of your application.</span></span> <span data-ttu-id="12f28-171">Pour gérer correctement cet échec, vous devez récupérer de nouveau l’entité, apporter vos modifications (si elles sont toujours valides), puis effectuer une autre opération [Replace][dotnet_TableOperation_Replace].</span><span class="sxs-lookup"><span data-stu-id="12f28-171">The proper handling of this failure is to retrieve the entity again, make your changes (if still valid), and then perform another [Replace][dotnet_TableOperation_Replace] operation.</span></span> <span data-ttu-id="12f28-172">La prochaine section vous apprendra à remplacer ce comportement.</span><span class="sxs-lookup"><span data-stu-id="12f28-172">The next section will show you how to override this behavior.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute the operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Assign the result to a CustomerEntity object.
CustomerEntity updateEntity = (CustomerEntity)retrievedResult.Result;

if (updateEntity != null)
{
    // Change the phone number.
    updateEntity.PhoneNumber = "425-555-0105";

    // Create the Replace TableOperation.
    TableOperation updateOperation = TableOperation.Replace(updateEntity);

    // Execute the operation.
    table.Execute(updateOperation);

    Console.WriteLine("Entity updated.");
}
else
{
    Console.WriteLine("Entity could not be retrieved.");
}
```

## <a name="insert-or-replace-an-entity"></a><span data-ttu-id="12f28-173">Insertion ou remplacement d’une entité</span><span class="sxs-lookup"><span data-stu-id="12f28-173">Insert-or-replace an entity</span></span>
<span data-ttu-id="12f28-174">Les opérations [Replace][dotnet_TableOperation_Replace] échouent si l’entité a été modifiée depuis sa récupération à partir du serveur.</span><span class="sxs-lookup"><span data-stu-id="12f28-174">[Replace][dotnet_TableOperation_Replace] operations will fail if the entity has been changed since it was retrieved from the server.</span></span> <span data-ttu-id="12f28-175">De plus, vous devez d’abord récupérer l’entité du serveur pour que l’opération [Replace][dotnet_TableOperation_Replace] réussisse.</span><span class="sxs-lookup"><span data-stu-id="12f28-175">Furthermore, you must retrieve the entity from the server first in order for the [Replace][dotnet_TableOperation_Replace] operation to be successful.</span></span> <span data-ttu-id="12f28-176">Cependant, il se peut parfois que vous ne sachiez pas si l’entité existe sur le serveur et si les valeurs stockées sont inadaptées.</span><span class="sxs-lookup"><span data-stu-id="12f28-176">Sometimes, however, you don't know if the entity exists on the server and the current values stored in it are irrelevant.</span></span> <span data-ttu-id="12f28-177">Votre mise à jour doit donc toutes les remplacer.</span><span class="sxs-lookup"><span data-stu-id="12f28-177">Your update should overwrite them all.</span></span> <span data-ttu-id="12f28-178">Pour cela, il vous faut utiliser une opération [InsertOrReplace][dotnet_TableOperation_InsertOrReplace].</span><span class="sxs-lookup"><span data-stu-id="12f28-178">To accomplish this, you would use an [InsertOrReplace][dotnet_TableOperation_InsertOrReplace] operation.</span></span> <span data-ttu-id="12f28-179">Cette opération insère l’entité (s’il n’y en a pas déjà une) ou la remplace (s’il y en a une), indépendamment du moment de la dernière mise à jour.</span><span class="sxs-lookup"><span data-stu-id="12f28-179">This operation inserts the entity if it doesn't exist, or replaces it if it does, regardless of when the last update was made.</span></span>

<span data-ttu-id="12f28-180">Dans l’exemple de code suivant, une entité client de « Fred Jones » est créée et insérée dans la table « people ».</span><span class="sxs-lookup"><span data-stu-id="12f28-180">In the following code example, a customer entity for 'Fred Jones' is created and inserted into the 'people' table.</span></span> <span data-ttu-id="12f28-181">Ensuite, nous utilisons l’opération [InsertOrReplace][dotnet_TableOperation_InsertOrReplace] pour enregistrer une entité avec la même clé de partition (Jones) et la même clé de ligne (Fred) sur le serveur, cette fois avec une valeur différente pour la propriété PhoneNumber.</span><span class="sxs-lookup"><span data-stu-id="12f28-181">Next, we use the [InsertOrReplace][dotnet_TableOperation_InsertOrReplace] operation to save an entity with the same partition key (Jones) and row key (Fred) to the server, this time with a different value for the PhoneNumber property.</span></span> <span data-ttu-id="12f28-182">Comme nous utilisons [InsertOrReplace][dotnet_TableOperation_InsertOrReplace], toutes ses valeurs de propriété sont remplacées.</span><span class="sxs-lookup"><span data-stu-id="12f28-182">Because we use [InsertOrReplace][dotnet_TableOperation_InsertOrReplace], all of its property values are replaced.</span></span> <span data-ttu-id="12f28-183">Toutefois, s’il n’existait pas d’entité « Fred Jones » dans la table, elle aurait été insérée.</span><span class="sxs-lookup"><span data-stu-id="12f28-183">However, if a 'Fred Jones' entity hadn't already existed in the table, it would have been inserted.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a customer entity.
CustomerEntity customer3 = new CustomerEntity("Jones", "Fred");
customer3.Email = "Fred@contoso.com";
customer3.PhoneNumber = "425-555-0106";

// Create the TableOperation object that inserts the customer entity.
TableOperation insertOperation = TableOperation.Insert(customer3);

// Execute the operation.
table.Execute(insertOperation);

// Create another customer entity with the same partition key and row key.
// We've already created a 'Fred Jones' entity and saved it to the
// 'people' table, but here we're specifying a different value for the
// PhoneNumber property.
CustomerEntity customer4 = new CustomerEntity("Jones", "Fred");
customer4.Email = "Fred@contoso.com";
customer4.PhoneNumber = "425-555-0107";

// Create the InsertOrReplace TableOperation.
TableOperation insertOrReplaceOperation = TableOperation.InsertOrReplace(customer4);

// Execute the operation. Because a 'Fred Jones' entity already exists in the
// 'people' table, its property values will be overwritten by those in this
// CustomerEntity. If 'Fred Jones' didn't already exist, the entity would be
// added to the table.
table.Execute(insertOrReplaceOperation);
```

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="12f28-184">Interrogation d’un sous-ensemble de propriétés d’entité</span><span class="sxs-lookup"><span data-stu-id="12f28-184">Query a subset of entity properties</span></span>
<span data-ttu-id="12f28-185">Vous pouvez utiliser une requête de table pour récupérer uniquement quelques propriétés au lieu de l’intégralité des propriétés de l’entité.</span><span class="sxs-lookup"><span data-stu-id="12f28-185">A table query can retrieve just a few properties from an entity instead of all the entity properties.</span></span> <span data-ttu-id="12f28-186">Cette technique, nommée « projection », réduit la consommation de bande passante et peut améliorer les performances des requêtes, notamment pour les entités volumineuses.</span><span class="sxs-lookup"><span data-stu-id="12f28-186">This technique, called projection, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="12f28-187">La requête contenue dans le code suivant renvoie uniquement les adresses de messagerie électronique des entités dans la table.</span><span class="sxs-lookup"><span data-stu-id="12f28-187">The query in the following code returns only the email addresses of entities in the table.</span></span> <span data-ttu-id="12f28-188">Pour ce faire, nous utilisons une requête [DynamicTableEntity][dotnet_DynamicTableEntity] et [EntityResolver][dotnet_EntityResolver].</span><span class="sxs-lookup"><span data-stu-id="12f28-188">This is done by using a query of [DynamicTableEntity][dotnet_DynamicTableEntity] and also [EntityResolver][dotnet_EntityResolver].</span></span> <span data-ttu-id="12f28-189">Pour plus d’informations sur la projection, consultez le billet de blog [Présentation d’Upsert et de la projection de requête][blog_post_upsert].</span><span class="sxs-lookup"><span data-stu-id="12f28-189">You can learn more about projection in the [Introducing Upsert and Query Projection blog post][blog_post_upsert].</span></span> <span data-ttu-id="12f28-190">La projection n’est pas prise en charge par l’émulateur de stockage : ce code ne s’exécute donc que si vous utilisez un compte dans le service de Table.</span><span class="sxs-lookup"><span data-stu-id="12f28-190">Projection is not supported by the storage emulator, so this code runs only when you're using an account in the Table service.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Define the query, and select only the Email property.
TableQuery<DynamicTableEntity> projectionQuery = new TableQuery<DynamicTableEntity>().Select(new string[] { "Email" });

// Define an entity resolver to work with the entity after retrieval.
EntityResolver<string> resolver = (pk, rk, ts, props, etag) => props.ContainsKey("Email") ? props["Email"].StringValue : null;

foreach (string projectedEmail in table.ExecuteQuery(projectionQuery, resolver, null, null))
{
    Console.WriteLine(projectedEmail);
}
```

## <a name="delete-an-entity"></a><span data-ttu-id="12f28-191">Suppression d’une entité</span><span class="sxs-lookup"><span data-stu-id="12f28-191">Delete an entity</span></span>
<span data-ttu-id="12f28-192">Il est facile de supprimer une entité après l’avoir récupérée. Il suffit pour cela d’utiliser la procédure suivie pour la mise à jour d’une entité.</span><span class="sxs-lookup"><span data-stu-id="12f28-192">You can easily delete an entity after you have retrieved it by using the same pattern shown for updating an entity.</span></span> <span data-ttu-id="12f28-193">Le code suivant extrait et supprime une entité de client.</span><span class="sxs-lookup"><span data-stu-id="12f28-193">The following code retrieves and deletes a customer entity.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that expects a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute the operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Assign the result to a CustomerEntity.
CustomerEntity deleteEntity = (CustomerEntity)retrievedResult.Result;

// Create the Delete TableOperation.
if (deleteEntity != null)
{
    TableOperation deleteOperation = TableOperation.Delete(deleteEntity);

    // Execute the operation.
    table.Execute(deleteOperation);

    Console.WriteLine("Entity deleted.");
}
else
{
    Console.WriteLine("Could not retrieve the entity.");
}
```

## <a name="delete-a-table"></a><span data-ttu-id="12f28-194">Suppression d’une table</span><span class="sxs-lookup"><span data-stu-id="12f28-194">Delete a table</span></span>
<span data-ttu-id="12f28-195">Pour finir, l’exemple de code suivant supprime une table d’un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="12f28-195">Finally, the following code example deletes a table from a storage account.</span></span> <span data-ttu-id="12f28-196">Une table supprimée ne peut plus être recréée pendant un certain temps.</span><span class="sxs-lookup"><span data-stu-id="12f28-196">A table that has been deleted will be unavailable to be re-created for a period of time following the deletion.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Delete the table it if exists.
table.DeleteIfExists();
```

## <a name="retrieve-entities-in-pages-asynchronously"></a><span data-ttu-id="12f28-197">Récupérer des entités dans les pages de manière asynchrone</span><span class="sxs-lookup"><span data-stu-id="12f28-197">Retrieve entities in pages asynchronously</span></span>
<span data-ttu-id="12f28-198">Si vous lisez un grand nombre d’entités et souhaitez traiter ou afficher les entités dès qu’elles sont récupérées au lieu d’attendre qu’elles aient toutes été renvoyées, vous pouvez les récupérer à l’aide d’une requête segmentée.</span><span class="sxs-lookup"><span data-stu-id="12f28-198">If you are reading a large number of entities, and you want to process/display entities as they are retrieved rather than waiting for them all to return, you can retrieve entities by using a segmented query.</span></span> <span data-ttu-id="12f28-199">Cet exemple illustre comment renvoyer les résultats dans des pages au moyen du modèle Async-Await afin que l’exécution ne soit pas bloquée pendant que vous attendez le renvoi d’un ensemble de résultats volumineux.</span><span class="sxs-lookup"><span data-stu-id="12f28-199">This example shows how to return results in pages by using the Async-Await pattern so that execution is not blocked while you're waiting for a large set of results to return.</span></span> <span data-ttu-id="12f28-200">Pour plus d’informations sur l’utilisation du modèle Async-Await dans .NET, consultez l’article [Programmation asynchrone avec Async et Await (C# et Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx).</span><span class="sxs-lookup"><span data-stu-id="12f28-200">For more details on using the Async-Await pattern in .NET, see [Asynchronous programming with Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx).</span></span>

```csharp
// Initialize a default TableQuery to retrieve all the entities in the table.
TableQuery<CustomerEntity> tableQuery = new TableQuery<CustomerEntity>();

// Initialize the continuation token to null to start from the beginning of the table.
TableContinuationToken continuationToken = null;

do
{
    // Retrieve a segment (up to 1,000 entities).
    TableQuerySegment<CustomerEntity> tableQueryResult =
        await table.ExecuteQuerySegmentedAsync(tableQuery, continuationToken);

    // Assign the new continuation token to tell the service where to
    // continue on the next iteration (or null if it has reached the end).
    continuationToken = tableQueryResult.ContinuationToken;

    // Print the number of rows retrieved.
    Console.WriteLine("Rows retrieved {0}", tableQueryResult.Results.Count);

// Loop until a null continuation token is received, indicating the end of the table.
} while(continuationToken != null);
```

## <a name="next-steps"></a><span data-ttu-id="12f28-201">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="12f28-201">Next steps</span></span>
<span data-ttu-id="12f28-202">Comme vous connaissez maintenant les bases du stockage des tables, vous pouvez consulter les liens suivants pour apprendre à exécuter les tâches de stockage plus complexes.</span><span class="sxs-lookup"><span data-stu-id="12f28-202">Now that you've learned the basics of Table storage, follow these links to learn about more complex storage tasks:</span></span>

* <span data-ttu-id="12f28-203">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) est une application autonome et gratuite de Microsoft qui vous permet d’exploiter visuellement les données de Stockage Azure sur Windows, macOS et Linux.</span><span class="sxs-lookup"><span data-stu-id="12f28-203">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="12f28-204">Pour obtenir des exemples supplémentaires utilisant Table Storage, voir [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/)</span><span class="sxs-lookup"><span data-stu-id="12f28-204">See more Table storage samples in [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/)</span></span>
* <span data-ttu-id="12f28-205">Pour plus d'informations sur les API disponibles, consultez la documentation de référence du service de Table :</span><span class="sxs-lookup"><span data-stu-id="12f28-205">View the Table service reference documentation for complete details about available APIs:</span></span>
* [<span data-ttu-id="12f28-206">Référence de la bibliothèque cliente de stockage pour .NET</span><span class="sxs-lookup"><span data-stu-id="12f28-206">Storage Client Library for .NET reference</span></span>](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
* [<span data-ttu-id="12f28-207">Référence d’API REST</span><span class="sxs-lookup"><span data-stu-id="12f28-207">REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="12f28-208">Découvrez comment simplifier le code que vous écrivez avec Azure Storage, à l’aide du [Kit de développement logiciel (SDK) Azure WebJobs](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="12f28-208">Learn how to simplify the code you write to work with Azure Storage by using the [Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md)</span></span>
* <span data-ttu-id="12f28-209">Pour plus d’informations sur les autres options de stockage de données dans Azure, consultez d’autres guides de fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="12f28-209">View more feature guides to learn about additional options for storing data in Azure.</span></span>
* <span data-ttu-id="12f28-210">[Prise en main d’Azure Blob Storage à l’aide de .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) pour le stockage de données non structurées.</span><span class="sxs-lookup"><span data-stu-id="12f28-210">[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) to store unstructured data.</span></span>
* <span data-ttu-id="12f28-211">[Connexion à SQL Database à l’aide de .NET (C#)](../sql-database/sql-database-develop-dotnet-simple.md) pour stocker des données relationnelles.</span><span class="sxs-lookup"><span data-stu-id="12f28-211">[Connect to SQL Database by using .NET (C#)](../sql-database/sql-database-develop-dotnet-simple.md) to store relational data.</span></span>

[Download and install the Azure SDK for .NET]: /develop/net/
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
