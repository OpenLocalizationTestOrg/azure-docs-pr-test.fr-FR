---
title: "aaaHow tooget a démarré avec le stockage de table et de Visual Studio services connectés (ASP.NET Core) | Documents Microsoft"
description: "Comment tooget démarrer avec un stockage de Table Azure dans un projet ASP.NET Core dans Visual Studio une fois la connexion de compte de stockage tooa à l’aide de Visual Studio services connectés"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: c3c451d1-71ff-4222-a348-c41c98a02b85
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: e3eb3f3e65456108dd3cde7e3e470f98ba456e35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-started-with-azure-table-storage-and-visual-studio-connected-services"></a><span data-ttu-id="8f052-103">Comment tooget démarrer avec stockage de Table Azure et Visual Studio services connectés</span><span class="sxs-lookup"><span data-stu-id="8f052-103">How tooget started with Azure Table storage and Visual Studio connected services</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="8f052-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="8f052-104">Overview</span></span>
<span data-ttu-id="8f052-105">Cet article décrit comment obtenir démarré à l’aide de la Table Azure storage dans Visual Studio après avoir créé ou référencé d’un compte de stockage Azure dans un projet ASP.NET Core à l’aide de hello Visual Studio **ajouter des Services connectés** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="8f052-105">This article describes how get started using Azure Table storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using hello Visual Studio **Add Connected Services** dialog.</span></span>

<span data-ttu-id="8f052-106">Hello service de stockage de Table Azure vous permet de toostore de grandes quantités de données structurées.</span><span class="sxs-lookup"><span data-stu-id="8f052-106">hello Azure Table storage service enables you toostore large amounts of structured data.</span></span> <span data-ttu-id="8f052-107">service de Hello est un magasin de données NoSQL qui accepte des appels authentifiés provenant à l’intérieur et extérieur hello cloud Azure.</span><span class="sxs-lookup"><span data-stu-id="8f052-107">hello service is a NoSQL data store that accepts authenticated calls from inside and outside hello Azure cloud.</span></span> <span data-ttu-id="8f052-108">Les tables Azure sont idéales pour le stockage des données structurées non relationnelles.</span><span class="sxs-lookup"><span data-stu-id="8f052-108">Azure tables are ideal for storing structured, non-relational data.</span></span>

<span data-ttu-id="8f052-109">Hello **ajouter des Services connectés** opération installe hello approprié NuGet packages tooaccess stockage Azure dans votre projet et ajoute la chaîne de connexion hello pour hello du compte de stockage tooyour les fichiers de configuration de projet.</span><span class="sxs-lookup"><span data-stu-id="8f052-109">hello **Add Connected Services** operation installs hello appropriate NuGet packages tooaccess Azure storage in your project and adds hello connection string for hello storage account tooyour project configuration files.</span></span>

<span data-ttu-id="8f052-110">Pour obtenir des informations plus générales sur l’utilisation d’Azure Table Storage, consultez la page [Prise en main du stockage de tables Azure à l’aide de .NET](../storage/storage-dotnet-how-to-use-tables.md).</span><span class="sxs-lookup"><span data-stu-id="8f052-110">For more general information about using Azure Table storage, see [Get started with Azure Table storage using .NET](../storage/storage-dotnet-how-to-use-tables.md).</span></span>

<span data-ttu-id="8f052-111">tooget démarré, vous devez toocreate une table dans votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="8f052-111">tooget started, you first need toocreate a table in your storage account.</span></span> <span data-ttu-id="8f052-112">Nous allons vous montrer comment toocreate Azure table dans le code.</span><span class="sxs-lookup"><span data-stu-id="8f052-112">We'll show you how toocreate an Azure table in code.</span></span> <span data-ttu-id="8f052-113">Nous allons également vous montrer comment tooperform table de base et les opérations d’entité, telles que l’ajout, modification, lecture et la lecture de la table entités.</span><span class="sxs-lookup"><span data-stu-id="8f052-113">We'll also show you how tooperform basic table and entity operations, such as adding, modifying, reading and reading table entities.</span></span> <span data-ttu-id="8f052-114">exemples de Hello sont écrits en C\# de code et d’utiliser hello bibliothèque cliente de stockage Azure pour .NET.</span><span class="sxs-lookup"><span data-stu-id="8f052-114">hello samples are written in C\# code and use hello Azure Storage Client Library for .NET.</span></span>

<span data-ttu-id="8f052-115">**Remarque** -certaines hello API qui effectuent des appels de stockage de tooAzure dans ASP.NET Core sont asynchrones.</span><span class="sxs-lookup"><span data-stu-id="8f052-115">**NOTE** - Some of hello APIs that perform calls out tooAzure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="8f052-116">Pour plus d’informations, voir l’article [Programmation asynchrone avec Async et Await](http://msdn.microsoft.com/library/hh191443.aspx) .</span><span class="sxs-lookup"><span data-stu-id="8f052-116">See [Asynchronous Programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="8f052-117">code Hello ci-dessous suppose que les méthodes de programmation asynchrones sont utilisées.</span><span class="sxs-lookup"><span data-stu-id="8f052-117">hello code below assumes Async programming methods are being used.</span></span>

## <a name="access-tables-in-code"></a><span data-ttu-id="8f052-118">Accès aux tables dans le code</span><span class="sxs-lookup"><span data-stu-id="8f052-118">Access tables in code</span></span>
<span data-ttu-id="8f052-119">tooaccess des tables dans les projets ASP.NET Core, vous devez hello tooinclude les fichiers source des éléments tooany C# qui a accès au stockage de table Azure suivants.</span><span class="sxs-lookup"><span data-stu-id="8f052-119">tooaccess tables in ASP.NET Core projects, you need tooinclude hello following items tooany C# source files that access Azure table storage.</span></span>

1. <span data-ttu-id="8f052-120">Assurez-vous que les déclarations d’espace de noms hello haut hello du fichier de hello c# incluent ces **à l’aide de** instructions.</span><span class="sxs-lookup"><span data-stu-id="8f052-120">Make sure hello namespace declarations at hello top of hello C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Table;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="8f052-121">Obtenez un objet **CloudStorageAccount** qui représente les informations de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="8f052-121">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="8f052-122">Hello utilisation suivant tooget de code hello votre chaîne de connexion de stockage et les informations de compte de stockage à partir de la configuration du service Azure hello.</span><span class="sxs-lookup"><span data-stu-id="8f052-122">Use hello following code tooget hello your storage connection string and storage account information from hello Azure service configuration.</span></span>
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
            CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
   
    <span data-ttu-id="8f052-123">**Remarque** -utilisent les hello ci-dessus code devant les code hello dans hello suivant des exemples.</span><span class="sxs-lookup"><span data-stu-id="8f052-123">**NOTE** - Use all of hello above code in front of hello code in hello following samples.</span></span>
3. <span data-ttu-id="8f052-124">Obtenir un **CloudTableClient** tooreference les objets de table hello dans votre compte de stockage de l’objet.</span><span class="sxs-lookup"><span data-stu-id="8f052-124">Get a **CloudTableClient** object tooreference hello table objects in your storage account.</span></span>  
   
        // Create hello table client.
        CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
4. <span data-ttu-id="8f052-125">Obtenir un **CloudTable** référence d’objet tooreference une table spécifique et des entités.</span><span class="sxs-lookup"><span data-stu-id="8f052-125">Get a **CloudTable** reference object tooreference a specific table and entities.</span></span>
   
        // Get a reference tooa table named "peopleTable"
        CloudTable table = tableClient.GetTableReference("peopleTable");

## <a name="create-a-table-in-code"></a><span data-ttu-id="8f052-126">Création d'une table dans le code</span><span class="sxs-lookup"><span data-stu-id="8f052-126">Create a table in code</span></span>
<span data-ttu-id="8f052-127">toocreate hello table Azure, ajoutez simplement un appel trop**CreateIfNotExistsAsync()**.</span><span class="sxs-lookup"><span data-stu-id="8f052-127">toocreate hello Azure table, just add a call too**CreateIfNotExistsAsync()**.</span></span>

    // Create hello CloudTable if it does not exist
    await table.CreateIfNotExistsAsync();

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="8f052-128">Ajouter une table de tooa d’entité</span><span class="sxs-lookup"><span data-stu-id="8f052-128">Add an entity tooa table</span></span>
<span data-ttu-id="8f052-129">tooadd une table de tooa entité que vous créez une classe qui définit les propriétés de hello de votre entité.</span><span class="sxs-lookup"><span data-stu-id="8f052-129">tooadd an entity tooa table you create a class that defines hello properties of your entity.</span></span> <span data-ttu-id="8f052-130">Hello de code suivant définit une classe d’entité appelée **CustomerEntity** qu’utilise hello prénom du client en tant que clé de ligne hello et le nom comme clé de partition hello.</span><span class="sxs-lookup"><span data-stu-id="8f052-130">hello following code defines an entity class called **CustomerEntity** that uses hello customer's first name as hello row key and last name as hello partition key.</span></span>

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

<span data-ttu-id="8f052-131">Opérations de table impliquant des entités sont effectuées à l’aide de hello **CloudTable** de l’objet créé dans « Accéder aux tables dans le code ».</span><span class="sxs-lookup"><span data-stu-id="8f052-131">Table operations involving entities are done using hello **CloudTable** object you created earlier in "Access tables in code."</span></span> <span data-ttu-id="8f052-132">Hello **TableOperation** objet représente hello opération toobe est terminé.</span><span class="sxs-lookup"><span data-stu-id="8f052-132">hello **TableOperation** object represents hello operation toobe done.</span></span> <span data-ttu-id="8f052-133">Hello suivant exemple de code montre comment toocreate un **CloudTable** objet et un **CustomerEntity** objet.</span><span class="sxs-lookup"><span data-stu-id="8f052-133">hello following code example shows how toocreate a **CloudTable** object and a **CustomerEntity** object.</span></span> <span data-ttu-id="8f052-134">opération de hello tooprepare, un **TableOperation** est créé entité customer de hello tooinsert dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="8f052-134">tooprepare hello operation, a **TableOperation** is created tooinsert hello customer entity into hello table.</span></span> <span data-ttu-id="8f052-135">Enfin, l’opération de hello est exécutée en appelant CloudTable.ExecuteAsync.</span><span class="sxs-lookup"><span data-stu-id="8f052-135">Finally, hello operation is executed by calling CloudTable.ExecuteAsync.</span></span>

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    customer1.PhoneNumber = "425-555-0101";

    // Create hello TableOperation that inserts hello customer entity.
    TableOperation insertOperation = TableOperation.Insert(customer1);

    // Execute hello insert operation.
    await peopleTable.ExecuteAsync(insertOperation);

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="8f052-136">Insertion d’un lot d’entités</span><span class="sxs-lookup"><span data-stu-id="8f052-136">Insert a batch of entities</span></span>
<span data-ttu-id="8f052-137">Vous pouvez insérer plusieurs entités dans une table en une seule opération d'écriture.</span><span class="sxs-lookup"><span data-stu-id="8f052-137">You can insert multiple entities into a table in a single write operation.</span></span> <span data-ttu-id="8f052-138">Hello exemple de code suivant crée deux objets d’entité (« Jeff Smith » et « Ben Smith »), les ajoute tooa **TableBatchOperation** objet à l’aide de hello **insérer** méthode, puis l’opération de hello commence par appel de CloudTable.ExecuteBatchAsync.</span><span class="sxs-lookup"><span data-stu-id="8f052-138">hello following code example creates two entity objects ("Jeff Smith" and "Ben Smith"), adds them tooa **TableBatchOperation** object using hello **Insert** method, and then starts hello operation by calling CloudTable.ExecuteBatchAsync.</span></span>

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
    await peopleTable.ExecuteBatchAsync(batchOperation);

## <a name="get-all-of-hello-entities-in-a-partition"></a><span data-ttu-id="8f052-139">Obtenir toutes les entités de hello dans une partition</span><span class="sxs-lookup"><span data-stu-id="8f052-139">Get all of hello entities in a partition</span></span>
<span data-ttu-id="8f052-140">tooquery une table pour toutes les entités hello dans une partition, utilisez un **TableQuery** objet.</span><span class="sxs-lookup"><span data-stu-id="8f052-140">tooquery a table for all of hello entities in a partition, use a **TableQuery** object.</span></span> <span data-ttu-id="8f052-141">Hello exemple de code suivant spécifie un filtre pour les entités où « Smith » est la clé de partition hello.</span><span class="sxs-lookup"><span data-stu-id="8f052-141">hello following code example specifies a filter for entities where 'Smith' is hello partition key.</span></span> <span data-ttu-id="8f052-142">Cet exemple imprime les champs de chaque entité dans la console de toohello de résultats de requête hello hello.</span><span class="sxs-lookup"><span data-stu-id="8f052-142">This example prints hello fields of each entity in hello query results toohello console.</span></span>

    // Construct hello query operation for all customer entities where PartitionKey="Smith".
    TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>().Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

    // Print hello fields for each customer.
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

## <a name="get-a-single-entity"></a><span data-ttu-id="8f052-143">Obtention d'une seule entité</span><span class="sxs-lookup"><span data-stu-id="8f052-143">Get a single entity</span></span>
<span data-ttu-id="8f052-144">Vous pouvez écrire une requête tooget une entité unique et spécifique.</span><span class="sxs-lookup"><span data-stu-id="8f052-144">You can write a query tooget a single, specific entity.</span></span> <span data-ttu-id="8f052-145">code Hello suivant utilise un **TableOperation** toospecify un client nommé « Ben Smith » de l’objet.</span><span class="sxs-lookup"><span data-stu-id="8f052-145">hello following code uses a **TableOperation** object toospecify a customer named 'Ben Smith'.</span></span> <span data-ttu-id="8f052-146">Cette méthode retourne simplement une entité, plutôt qu’une collection et hello a retourné la valeur dans **TableResult.Result** est un **CustomerEntity** objet.</span><span class="sxs-lookup"><span data-stu-id="8f052-146">This method returns just one entity, rather than a collection, and hello returned value in **TableResult.Result** is a **CustomerEntity** object.</span></span> <span data-ttu-id="8f052-147">Spécification des clés de partition et de ligne dans une requête est tooretrieve de manière plus rapide hello une seule entité hello **Table** service.</span><span class="sxs-lookup"><span data-stu-id="8f052-147">Specifying both partition and row keys in a query is hello fastest way tooretrieve a single entity from hello **Table** service.</span></span>

    // Create a retrieve operation that takes a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute hello retrieve operation.
    TableResult retrievedResult = await peopleTable.ExecuteAsync(retrieveOperation);

    // Print hello phone number of hello result.
    if (retrievedResult.Result != null)
       Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
    else
       Console.WriteLine("hello phone number could not be retrieved.");

## <a name="delete-an-entity"></a><span data-ttu-id="8f052-148">Suppression d’une entité</span><span class="sxs-lookup"><span data-stu-id="8f052-148">Delete an entity</span></span>
<span data-ttu-id="8f052-149">Une fois l'entité trouvée, vous pouvez la supprimer.</span><span class="sxs-lookup"><span data-stu-id="8f052-149">You can delete an entity after you find it.</span></span> <span data-ttu-id="8f052-150">Hello de code suivant recherche une entité client nommée « Ben Smith » et si elle le trouve, il le supprime.</span><span class="sxs-lookup"><span data-stu-id="8f052-150">hello following code looks for a customer entity named "Ben Smith" and if it finds it, it deletes it.</span></span>

    // Create a retrieve operation that expects a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute hello operation.
    TableResult retrievedResult = peopleTable.Execute(retrieveOperation);

    // Assign hello result tooa CustomerEntity object.
    CustomerEntity deleteEntity = (CustomerEntity)retrievedResult.Result;

    // Create hello Delete TableOperation and then execute it.
    if (deleteEntity != null)
    {
       TableOperation deleteOperation = TableOperation.Delete(deleteEntity);

       // Execute hello operation.
       await peopleTable.ExecuteAsync(deleteOperation);

       Console.WriteLine("Entity deleted.");
    }

    else
       Console.WriteLine("Couldn't delete hello entity.");

## <a name="next-steps"></a><span data-ttu-id="8f052-151">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8f052-151">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-tables-next-steps](../../includes/vs-storage-dotnet-tables-next-steps.md)]

