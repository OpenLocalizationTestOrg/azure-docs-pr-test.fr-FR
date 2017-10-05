---
title: "Prendre en main le Stockage Table et les services connectés de Visual Studio (services cloud) | Microsoft Docs"
description: "Comment prendre en main le stockage de tables Azure dans un projet service cloud dans Visual Studio après s’être connecté à un compte de stockage à l’aide des services connectés de Visual Studio"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: a3a11ed8-ba7f-4193-912b-e555f5b72184
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 51b71d783806d9b0d58d4473b8c07f77441dadd8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="getting-started-with-azure-table-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="936c4-103">Prendre en main le stockage de tables Azure et les services connectés de Visual Studio (projets services cloud)</span><span class="sxs-lookup"><span data-stu-id="936c4-103">Getting started with Azure table storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="936c4-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="936c4-104">Overview</span></span>
<span data-ttu-id="936c4-105">Cet article décrit comment prendre en main Azure Table Storage dans Visual Studio après avoir créé ou référencé un compte de stockage Azure dans un projet de services cloud via la boîte de dialogue **Ajouter des services connectés** de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="936c4-105">This article describes how to get started using Azure table storage in Visual Studio after you have created or referenced an Azure storage account in a cloud services project by using the Visual Studio **Add Connected Services** dialog.</span></span> <span data-ttu-id="936c4-106">L’opération **Ajouter des services connectés** installe les packages NuGet appropriés pour accéder au stockage Azure de votre projet et ajoute la chaîne de connexion pour le compte de stockage aux fichiers de configuration de votre projet.</span><span class="sxs-lookup"><span data-stu-id="936c4-106">The **Add Connected Services** operation installs the appropriate NuGet packages to access Azure storage in your project and adds the connection string for the storage account to your project configuration files.</span></span>

<span data-ttu-id="936c4-107">Le service de stockage de tables Azure vous permet de stocker de grandes quantités de données structurées.</span><span class="sxs-lookup"><span data-stu-id="936c4-107">The Azure Table storage service enables you to store large amounts of structured data.</span></span> <span data-ttu-id="936c4-108">Il s'agit d'une banque de données NoSQL qui accepte les appels authentifiés provenant de l'intérieur et de l'extérieur du cloud Azure.</span><span class="sxs-lookup"><span data-stu-id="936c4-108">The service is a NoSQL datastore that accepts authenticated calls from inside and outside the Azure cloud.</span></span> <span data-ttu-id="936c4-109">Les tables Azure sont idéales pour le stockage des données structurées non relationnelles.</span><span class="sxs-lookup"><span data-stu-id="936c4-109">Azure tables are ideal for storing structured, non-relational data.</span></span>

<span data-ttu-id="936c4-110">Pour commencer, vous devez créer une table dans votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="936c4-110">To get started, you first need to create a table in your storage account.</span></span> <span data-ttu-id="936c4-111">Nous vous montrerons comment créer une table Azure dans le code et effectuer des opérations de base sur les tables et les entités, comme l’ajout, la modification et la lecture d’entités de table.</span><span class="sxs-lookup"><span data-stu-id="936c4-111">We'll show you how to create an Azure table in code, and also how to perform basic table and entity operations, such as adding, modifying, reading and reading table entities.</span></span> <span data-ttu-id="936c4-112">Les exemples sont écrits en code C\# et utilisent la [bibliothèque cliente Stockage Microsoft Azure pour .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="936c4-112">The samples are written in C\# code and use the [Microsoft Azure Storage client library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="936c4-113">**REMARQUE :** parmi les API qui effectuent des appels au stockage Azure, certaines sont asynchrones.</span><span class="sxs-lookup"><span data-stu-id="936c4-113">**NOTE:** Some of the APIs that perform calls out to Azure storage are asynchronous.</span></span> <span data-ttu-id="936c4-114">Pour plus d’informations, consultez l’article [Programmation asynchrone avec Async et Await](http://msdn.microsoft.com/library/hh191443.aspx) .</span><span class="sxs-lookup"><span data-stu-id="936c4-114">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="936c4-115">Le code ci-dessous suppose que les méthodes de programmation asynchrone sont utilisées.</span><span class="sxs-lookup"><span data-stu-id="936c4-115">The code below assumes async programming methods are being used.</span></span>

* <span data-ttu-id="936c4-116">Pour plus d’informations sur la manipulation des tables par programme, consultez la page [Prise en main du stockage de tables Azure à l’aide de .NET](../storage/storage-dotnet-how-to-use-tables.md) .</span><span class="sxs-lookup"><span data-stu-id="936c4-116">See [Get started with Azure Table storage using .NET](../storage/storage-dotnet-how-to-use-tables.md) for more information on programmatically manipulating tables.</span></span>
* <span data-ttu-id="936c4-117">Pour des informations générales sur Azure Storage, consultez la [documentation relative au stockage](https://azure.microsoft.com/documentation/services/storage/) .</span><span class="sxs-lookup"><span data-stu-id="936c4-117">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span></span>
* <span data-ttu-id="936c4-118">Pour des informations générales sur les services cloud Azure, consultez la [documentation des services cloud](https://azure.microsoft.com/documentation/services/cloud-services/) .</span><span class="sxs-lookup"><span data-stu-id="936c4-118">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span></span>
* <span data-ttu-id="936c4-119">Pour plus d’informations sur la programmation d’applications ASP.NET, consultez la page [ASP.NET](http://www.asp.net) .</span><span class="sxs-lookup"><span data-stu-id="936c4-119">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span></span>

## <a name="access-tables-in-code"></a><span data-ttu-id="936c4-120">Accès aux tables dans le code</span><span class="sxs-lookup"><span data-stu-id="936c4-120">Access tables in code</span></span>
<span data-ttu-id="936c4-121">Pour accéder aux tables dans les projets de service cloud, vous devez inclure les éléments suivants dans les fichiers sources C# qui accèdent au stockage de tables Azure.</span><span class="sxs-lookup"><span data-stu-id="936c4-121">To access tables in cloud service projects, you need to include the following items to any C# source files that access Azure table storage.</span></span>

1. <span data-ttu-id="936c4-122">Vérifiez que les déclarations d’espace de noms figurant au début du fichier C# incluent ces instructions **using** .</span><span class="sxs-lookup"><span data-stu-id="936c4-122">Make sure the namespace declarations at the top of the C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Table;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="936c4-123">Obtenez un objet **CloudStorageAccount** qui représente les informations de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="936c4-123">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="936c4-124">Le code suivant permet d'obtenir la chaîne de connexion de stockage et les informations de compte de stockage à partir de la configuration du service Azure.</span><span class="sxs-lookup"><span data-stu-id="936c4-124">Use the following code to get the storage connection string and storage account information from the Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage account name>
         _AzureStorageConnectionString"));
   > [!NOTE]
   > <span data-ttu-id="936c4-125">Placez tout le code ci-dessus avant celui des exemples suivants.</span><span class="sxs-lookup"><span data-stu-id="936c4-125">Use all of the above code in front of the code in the following samples.</span></span>
   > 
   > 
3. <span data-ttu-id="936c4-126">Obtenez un objet **CloudTableClient** pour référencer les objets de table de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="936c4-126">Get a **CloudTableClient** object to reference the table objects in your storage account.</span></span>
   
         // Create the table client.
         CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
4. <span data-ttu-id="936c4-127">Obtenez un objet de référence **CloudTable** pour référencer une table et des entités spécifiques.</span><span class="sxs-lookup"><span data-stu-id="936c4-127">Get a **CloudTable** reference object to reference a specific table and entities.</span></span>
   
        // Get a reference to a table named "peopleTable".
        CloudTable peopleTable = tableClient.GetTableReference("peopleTable");

## <a name="create-a-table-in-code"></a><span data-ttu-id="936c4-128">Création d'une table dans le code</span><span class="sxs-lookup"><span data-stu-id="936c4-128">Create a table in code</span></span>
<span data-ttu-id="936c4-129">Pour créer la table Azure, ajoutez simplement un appel à **CreateIfNotExistsAsync** après avoir obtenu un objet **CloudTable** comme indiqué dans la section « Accès aux tables dans le code ».</span><span class="sxs-lookup"><span data-stu-id="936c4-129">To create the Azure table, just add a call to **CreateIfNotExistsAsync** to the after you get a **CloudTable** object as described in the "Access tables in code" section.</span></span>

    // Create the CloudTable if it does not exist.
    await peopleTable.CreateIfNotExistsAsync();

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="936c4-130">Ajout d'une entité à une table</span><span class="sxs-lookup"><span data-stu-id="936c4-130">Add an entity to a table</span></span>
<span data-ttu-id="936c4-131">Pour ajouter une entité à une table, créez une classe définissant les propriétés de votre entité.</span><span class="sxs-lookup"><span data-stu-id="936c4-131">To add an entity to a table, create a class that defines the properties of your entity.</span></span> <span data-ttu-id="936c4-132">Le code suivant définit une classe d’entité nommée **CustomerEntity** , utilisant le prénom du client en tant que clé de ligne et son nom de famille en tant que clé de partition.</span><span class="sxs-lookup"><span data-stu-id="936c4-132">The following code defines an entity class called **CustomerEntity** that uses the customer's first name as the row key and the last name as the partition key.</span></span>

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

<span data-ttu-id="936c4-133">Les opérations de table impliquant des entités sont effectuées en utilisant l’objet **CloudTable** créé précédemment dans la section « Accéder aux tables dans le code ».</span><span class="sxs-lookup"><span data-stu-id="936c4-133">Table operations involving entities are done using the **CloudTable** object that you created earlier in "Access tables in code."</span></span> <span data-ttu-id="936c4-134">L'objet **TableOperation** représente l'opération à effectuer.</span><span class="sxs-lookup"><span data-stu-id="936c4-134">The **TableOperation** object represents the operation to be done.</span></span> <span data-ttu-id="936c4-135">L’exemple de code suivant montre comment créer des objets **CloudTable** et **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="936c4-135">The following code example shows how to create a **CloudTable** object and a **CustomerEntity** object.</span></span> <span data-ttu-id="936c4-136">Pour préparer l’opération, un objet **TableOperation** est créé pour insérer l’entité du client dans la table.</span><span class="sxs-lookup"><span data-stu-id="936c4-136">To prepare the operation, a **TableOperation** is created to insert the customer entity into the table.</span></span> <span data-ttu-id="936c4-137">Enfin, l’opération est exécutée en appelant **CloudTable.ExecuteAsync**.</span><span class="sxs-lookup"><span data-stu-id="936c4-137">Finally, the operation is executed by calling **CloudTable.ExecuteAsync**.</span></span>

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    customer1.PhoneNumber = "425-555-0101";

    // Create the TableOperation that inserts the customer entity.
    TableOperation insertOperation = TableOperation.Insert(customer1);

    // Execute the insert operation.
    await peopleTable.ExecuteAsync(insertOperation);


## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="936c4-138">Insertion d'un lot d'entités</span><span class="sxs-lookup"><span data-stu-id="936c4-138">Insert a batch of entities</span></span>
<span data-ttu-id="936c4-139">Vous pouvez insérer plusieurs entités dans une table en une seule opération d'écriture.</span><span class="sxs-lookup"><span data-stu-id="936c4-139">You can insert multiple entities into a table in a single write operation.</span></span> <span data-ttu-id="936c4-140">L’exemple de code suivant crée deux objets d’entité (« Jeff Smith » et « Ben Smith »), les ajoute à un objet **TableBatchOperation** en utilisant la méthode Insert, puis démarre l’opération en appelant **CloudTable.ExecuteBatchAsync**.</span><span class="sxs-lookup"><span data-stu-id="936c4-140">The following code example creates two entity objects ("Jeff Smith" and "Ben Smith"), adds them to a **TableBatchOperation** object using the Insert method, and then starts the operation by calling **CloudTable.ExecuteBatchAsync**.</span></span>

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
    await peopleTable.ExecuteBatchAsync(batchOperation);

## <a name="get-all-of-the-entities-in-a-partition"></a><span data-ttu-id="936c4-141">Recherche de toutes les entités d'une partition</span><span class="sxs-lookup"><span data-stu-id="936c4-141">Get all of the entities in a partition</span></span>
<span data-ttu-id="936c4-142">Pour exécuter une requête de table portant sur toutes les entités d'une partition, utilisez un objet **TableQuery** .</span><span class="sxs-lookup"><span data-stu-id="936c4-142">To query a table for all of the entities in a partition, use a **TableQuery** object.</span></span> <span data-ttu-id="936c4-143">L’exemple de code suivant indique un filtre pour les entités où ’Smith’ est la clé de partition.</span><span class="sxs-lookup"><span data-stu-id="936c4-143">The following code example specifies a filter for entities where 'Smith' is the partition key.</span></span> <span data-ttu-id="936c4-144">Il imprime les champs de chaque entité dans les résultats de requête vers la console.</span><span class="sxs-lookup"><span data-stu-id="936c4-144">This example prints the fields of each entity in the query results to the console.</span></span>

    // Construct the query operation for all customer entities where PartitionKey="Smith".
    TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>()
        .Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

    // Print the fields for each customer.
    TableContinuationToken token = null;
    do
    {
        TableQuerySegment<CustomerEntity> resultSegment = await peopleTable.ExecuteQuerySegmentedAsync(query, token);
        token = resultSegment.ContinuationToken;

        foreach (CustomerEntity entity in resultSegment.Results)
        {
            Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
            entity.Email, entity.PhoneNumber);
        }
    } while (token != null);

    return View();


## <a name="get-a-single-entity"></a><span data-ttu-id="936c4-145">Obtention d'une seule entité</span><span class="sxs-lookup"><span data-stu-id="936c4-145">Get a single entity</span></span>
<span data-ttu-id="936c4-146">Vous pouvez écrire une requête pour obtenir une seule entité.</span><span class="sxs-lookup"><span data-stu-id="936c4-146">You can write a query to get a single, specific entity.</span></span> <span data-ttu-id="936c4-147">Le code suivant utilise un objet **TableOperation** pour spécifier le client « Ben Smith ».</span><span class="sxs-lookup"><span data-stu-id="936c4-147">The following code uses a **TableOperation** object to specify a customer named 'Ben Smith'.</span></span> <span data-ttu-id="936c4-148">Cette méthode renvoie une seule entité (et non une collection). De plus, la valeur renvoyée dans **TableResult.Result** est un objet **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="936c4-148">This method returns just one entity, rather than a collection, and the returned value in **TableResult.Result** is a **CustomerEntity** object.</span></span> <span data-ttu-id="936c4-149">La méthode la plus rapide pour extraire une seule entité dans le service de **Table** consiste à spécifier une clé de partition et une clé de ligne.</span><span class="sxs-lookup"><span data-stu-id="936c4-149">Specifying both partition and row keys in a query is the fastest way to retrieve a single entity from the **Table** service.</span></span>

    // Create a retrieve operation that takes a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute the retrieve operation.
    TableResult retrievedResult = await peopleTable.ExecuteAsync(retrieveOperation);

    // Print the phone number of the result.
    if (retrievedResult.Result != null)
       Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
    else
       Console.WriteLine("The phone number could not be retrieved.");

## <a name="delete-an-entity"></a><span data-ttu-id="936c4-150">Suppression d’une entité</span><span class="sxs-lookup"><span data-stu-id="936c4-150">Delete an entity</span></span>
<span data-ttu-id="936c4-151">Une fois l'entité trouvée, vous pouvez la supprimer.</span><span class="sxs-lookup"><span data-stu-id="936c4-151">You can delete an entity after you find it.</span></span> <span data-ttu-id="936c4-152">Le code suivant recherche l'entité de client « Ben Smith », puis la supprime.</span><span class="sxs-lookup"><span data-stu-id="936c4-152">The following code looks for a customer entity named "Ben Smith", and if it finds it, it deletes it.</span></span>

    // Create a retrieve operation that expects a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute the operation.
    TableResult retrievedResult = peopleTable.Execute(retrieveOperation);

    // Assign the result to a CustomerEntity object.
    CustomerEntity deleteEntity = (CustomerEntity)retrievedResult.Result;

    // Create the Delete TableOperation and then execute it.
    if (deleteEntity != null)
    {
       TableOperation deleteOperation = TableOperation.Delete(deleteEntity);

       // Execute the operation.
       await peopleTable.ExecuteAsync(deleteOperation);

       Console.WriteLine("Entity deleted.");
    }

    else
       Console.WriteLine("Couldn't delete the entity.");

## <a name="next-steps"></a><span data-ttu-id="936c4-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="936c4-153">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-tables-next-steps](../../includes/vs-storage-dotnet-tables-next-steps.md)]

