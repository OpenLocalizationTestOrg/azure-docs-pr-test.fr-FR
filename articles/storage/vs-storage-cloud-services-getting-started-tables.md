---
title: "aaaGet a démarré avec le stockage de table et de Visual Studio services connectés (services de cloud computing) | Documents Microsoft"
description: "Comment tooget démarrer l’utilisation du stockage de Table Azure dans un projet de service cloud dans Visual Studio une fois la connexion de compte de stockage tooa à l’aide de Visual Studio services connectés"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: a3a11ed8-ba7f-4193-912b-e555f5b72184
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: efb16953e05764cb162cbdae4d0eab57f781682d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-table-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="de02a-103">Prendre en main le stockage de tables Azure et les services connectés de Visual Studio (projets services cloud)</span><span class="sxs-lookup"><span data-stu-id="de02a-103">Getting started with Azure table storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="de02a-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="de02a-104">Overview</span></span>
<span data-ttu-id="de02a-105">Cet article décrit comment tooget démarrer l’utilisation du stockage de table Windows Azure dans Visual Studio après avoir créé ou référencé un compte de stockage Azure dans un projet de services cloud à l’aide de Visual Studio de hello **ajouter des Services connectés** boîte de dialogue .</span><span class="sxs-lookup"><span data-stu-id="de02a-105">This article describes how tooget started using Azure table storage in Visual Studio after you have created or referenced an Azure storage account in a cloud services project by using hello Visual Studio **Add Connected Services** dialog.</span></span> <span data-ttu-id="de02a-106">Hello **ajouter des Services connectés** opération installe hello approprié NuGet packages tooaccess stockage Azure dans votre projet et ajoute la chaîne de connexion hello pour hello du compte de stockage tooyour les fichiers de configuration de projet.</span><span class="sxs-lookup"><span data-stu-id="de02a-106">hello **Add Connected Services** operation installs hello appropriate NuGet packages tooaccess Azure storage in your project and adds hello connection string for hello storage account tooyour project configuration files.</span></span>

<span data-ttu-id="de02a-107">Hello service de stockage de Table Azure vous permet de toostore de grandes quantités de données structurées.</span><span class="sxs-lookup"><span data-stu-id="de02a-107">hello Azure Table storage service enables you toostore large amounts of structured data.</span></span> <span data-ttu-id="de02a-108">service de Hello est une banque de données NoSQL qui accepte des appels authentifiés provenant à l’intérieur et extérieur hello cloud Azure.</span><span class="sxs-lookup"><span data-stu-id="de02a-108">hello service is a NoSQL datastore that accepts authenticated calls from inside and outside hello Azure cloud.</span></span> <span data-ttu-id="de02a-109">Les tables Azure sont idéales pour le stockage des données structurées non relationnelles.</span><span class="sxs-lookup"><span data-stu-id="de02a-109">Azure tables are ideal for storing structured, non-relational data.</span></span>

<span data-ttu-id="de02a-110">tooget démarré, vous devez toocreate une table dans votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="de02a-110">tooget started, you first need toocreate a table in your storage account.</span></span> <span data-ttu-id="de02a-111">Nous allons vous montrer comment toocreate Azure table dans le code, et également comment tooperform table de base et les opérations d’entité, telles que l’ajout, modification, lecture et la lecture de la table entités.</span><span class="sxs-lookup"><span data-stu-id="de02a-111">We'll show you how toocreate an Azure table in code, and also how tooperform basic table and entity operations, such as adding, modifying, reading and reading table entities.</span></span> <span data-ttu-id="de02a-112">exemples de Hello sont écrits en C\# de code et d’utiliser hello [bibliothèque cliente de stockage Microsoft Azure pour .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="de02a-112">hello samples are written in C\# code and use hello [Microsoft Azure Storage client library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="de02a-113">**Remarque :** certaines hello API qui effectuent des appels tooAzure stockage sont asynchrones.</span><span class="sxs-lookup"><span data-stu-id="de02a-113">**NOTE:** Some of hello APIs that perform calls out tooAzure storage are asynchronous.</span></span> <span data-ttu-id="de02a-114">Pour plus d’informations, consultez l’article [Programmation asynchrone avec Async et Await](http://msdn.microsoft.com/library/hh191443.aspx) .</span><span class="sxs-lookup"><span data-stu-id="de02a-114">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="de02a-115">code Hello ci-dessous suppose que les méthodes de programmation asynchrones sont utilisées.</span><span class="sxs-lookup"><span data-stu-id="de02a-115">hello code below assumes async programming methods are being used.</span></span>

* <span data-ttu-id="de02a-116">Pour plus d’informations sur la manipulation des tables par programme, consultez la page [Prise en main du stockage de tables Azure à l’aide de .NET](storage-dotnet-how-to-use-tables.md) .</span><span class="sxs-lookup"><span data-stu-id="de02a-116">See [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md) for more information on programmatically manipulating tables.</span></span>
* <span data-ttu-id="de02a-117">Pour des informations générales sur Azure Storage, consultez la [documentation relative au stockage](https://azure.microsoft.com/documentation/services/storage/) .</span><span class="sxs-lookup"><span data-stu-id="de02a-117">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span></span>
* <span data-ttu-id="de02a-118">Pour des informations générales sur les services cloud Azure, consultez la [documentation des services cloud](https://azure.microsoft.com/documentation/services/cloud-services/) .</span><span class="sxs-lookup"><span data-stu-id="de02a-118">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span></span>
* <span data-ttu-id="de02a-119">Pour plus d’informations sur la programmation d’applications ASP.NET, consultez la page [ASP.NET](http://www.asp.net) .</span><span class="sxs-lookup"><span data-stu-id="de02a-119">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span></span>

## <a name="access-tables-in-code"></a><span data-ttu-id="de02a-120">Accès aux tables dans le code</span><span class="sxs-lookup"><span data-stu-id="de02a-120">Access tables in code</span></span>
<span data-ttu-id="de02a-121">tooaccess des tables dans les projets de service cloud, vous devez hello tooinclude les fichiers source des éléments tooany C# qui a accès au stockage de table Azure suivants.</span><span class="sxs-lookup"><span data-stu-id="de02a-121">tooaccess tables in cloud service projects, you need tooinclude hello following items tooany C# source files that access Azure table storage.</span></span>

1. <span data-ttu-id="de02a-122">Assurez-vous que les déclarations d’espace de noms hello haut hello du fichier de hello c# incluent ces **à l’aide de** instructions.</span><span class="sxs-lookup"><span data-stu-id="de02a-122">Make sure hello namespace declarations at hello top of hello C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Table;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="de02a-123">Obtenez un objet **CloudStorageAccount** qui représente les informations de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="de02a-123">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="de02a-124">Utilisez hello suivant code tooget hello connexion chaîne et le stockage informations compte de stockage à partir de la configuration du service Azure hello.</span><span class="sxs-lookup"><span data-stu-id="de02a-124">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage account name>
         _AzureStorageConnectionString"));
   > [!NOTE]
   > <span data-ttu-id="de02a-125">Utiliser tout hello ci-dessus code devant les code hello Bonjour suivant des exemples.</span><span class="sxs-lookup"><span data-stu-id="de02a-125">Use all of hello above code in front of hello code in hello following samples.</span></span>
   > 
   > 
3. <span data-ttu-id="de02a-126">Obtenir un **CloudTableClient** tooreference les objets de table hello dans votre compte de stockage de l’objet.</span><span class="sxs-lookup"><span data-stu-id="de02a-126">Get a **CloudTableClient** object tooreference hello table objects in your storage account.</span></span>
   
         // Create hello table client.
         CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
4. <span data-ttu-id="de02a-127">Obtenir un **CloudTable** référence d’objet tooreference une table spécifique et des entités.</span><span class="sxs-lookup"><span data-stu-id="de02a-127">Get a **CloudTable** reference object tooreference a specific table and entities.</span></span>
   
        // Get a reference tooa table named "peopleTable".
        CloudTable peopleTable = tableClient.GetTableReference("peopleTable");

## <a name="create-a-table-in-code"></a><span data-ttu-id="de02a-128">Création d'une table dans le code</span><span class="sxs-lookup"><span data-stu-id="de02a-128">Create a table in code</span></span>
<span data-ttu-id="de02a-129">toocreate hello table Azure, ajoutez simplement un appel trop**CreateIfNotExistsAsync** toohello après avoir obtenu un **CloudTable** de l’objet comme décrit dans la section « Accéder aux tables dans le code » de hello.</span><span class="sxs-lookup"><span data-stu-id="de02a-129">toocreate hello Azure table, just add a call too**CreateIfNotExistsAsync** toohello after you get a **CloudTable** object as described in hello "Access tables in code" section.</span></span>

    // Create hello CloudTable if it does not exist.
    await peopleTable.CreateIfNotExistsAsync();

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="de02a-130">Ajouter une table de tooa d’entité</span><span class="sxs-lookup"><span data-stu-id="de02a-130">Add an entity tooa table</span></span>
<span data-ttu-id="de02a-131">tooadd une table de tooa entité, créez une classe qui définit des propriétés de votre entité hello.</span><span class="sxs-lookup"><span data-stu-id="de02a-131">tooadd an entity tooa table, create a class that defines hello properties of your entity.</span></span> <span data-ttu-id="de02a-132">Hello de code suivant définit une classe d’entité appelée **CustomerEntity** qu’utilise hello prénom du client en tant que clé de ligne hello et le nom comme clé de partition hello hello.</span><span class="sxs-lookup"><span data-stu-id="de02a-132">hello following code defines an entity class called **CustomerEntity** that uses hello customer's first name as hello row key and hello last name as hello partition key.</span></span>

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

<span data-ttu-id="de02a-133">Opérations de table impliquant des entités sont effectuées à l’aide de hello **CloudTable** objet que vous avez créé plus haut dans « Accéder aux tables dans le code ».</span><span class="sxs-lookup"><span data-stu-id="de02a-133">Table operations involving entities are done using hello **CloudTable** object that you created earlier in "Access tables in code."</span></span> <span data-ttu-id="de02a-134">Hello **TableOperation** objet représente hello opération toobe est terminé.</span><span class="sxs-lookup"><span data-stu-id="de02a-134">hello **TableOperation** object represents hello operation toobe done.</span></span> <span data-ttu-id="de02a-135">Hello suivant exemple de code montre comment toocreate un **CloudTable** objet et un **CustomerEntity** objet.</span><span class="sxs-lookup"><span data-stu-id="de02a-135">hello following code example shows how toocreate a **CloudTable** object and a **CustomerEntity** object.</span></span> <span data-ttu-id="de02a-136">opération de hello tooprepare, un **TableOperation** est créé entité customer de hello tooinsert dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="de02a-136">tooprepare hello operation, a **TableOperation** is created tooinsert hello customer entity into hello table.</span></span> <span data-ttu-id="de02a-137">Enfin, l’opération de hello est exécutée en appelant **CloudTable.ExecuteAsync**.</span><span class="sxs-lookup"><span data-stu-id="de02a-137">Finally, hello operation is executed by calling **CloudTable.ExecuteAsync**.</span></span>

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    customer1.PhoneNumber = "425-555-0101";

    // Create hello TableOperation that inserts hello customer entity.
    TableOperation insertOperation = TableOperation.Insert(customer1);

    // Execute hello insert operation.
    await peopleTable.ExecuteAsync(insertOperation);


## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="de02a-138">Insertion d’un lot d’entités</span><span class="sxs-lookup"><span data-stu-id="de02a-138">Insert a batch of entities</span></span>
<span data-ttu-id="de02a-139">Vous pouvez insérer plusieurs entités dans une table en une seule opération d'écriture.</span><span class="sxs-lookup"><span data-stu-id="de02a-139">You can insert multiple entities into a table in a single write operation.</span></span> <span data-ttu-id="de02a-140">Hello exemple de code suivant crée deux objets d’entité (« Jeff Smith » et « Ben Smith »), les ajoute tooa **TableBatchOperation** de l’objet à l’aide de hello la méthode d’insertion, puis démarre hello opération en appelant  **CloudTable.ExecuteBatchAsync**.</span><span class="sxs-lookup"><span data-stu-id="de02a-140">hello following code example creates two entity objects ("Jeff Smith" and "Ben Smith"), adds them tooa **TableBatchOperation** object using hello Insert method, and then starts hello operation by calling **CloudTable.ExecuteBatchAsync**.</span></span>

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

## <a name="get-all-of-hello-entities-in-a-partition"></a><span data-ttu-id="de02a-141">Obtenir toutes les entités de hello dans une partition</span><span class="sxs-lookup"><span data-stu-id="de02a-141">Get all of hello entities in a partition</span></span>
<span data-ttu-id="de02a-142">tooquery une table pour toutes les entités hello dans une partition, utilisez un **TableQuery** objet.</span><span class="sxs-lookup"><span data-stu-id="de02a-142">tooquery a table for all of hello entities in a partition, use a **TableQuery** object.</span></span> <span data-ttu-id="de02a-143">Hello exemple de code suivant spécifie un filtre pour les entités où « Smith » est la clé de partition hello.</span><span class="sxs-lookup"><span data-stu-id="de02a-143">hello following code example specifies a filter for entities where 'Smith' is hello partition key.</span></span> <span data-ttu-id="de02a-144">Cet exemple imprime les champs de chaque entité dans la console de toohello de résultats de requête hello hello.</span><span class="sxs-lookup"><span data-stu-id="de02a-144">This example prints hello fields of each entity in hello query results toohello console.</span></span>

    // Construct hello query operation for all customer entities where PartitionKey="Smith".
    TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>()
        .Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

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

    return View();


## <a name="get-a-single-entity"></a><span data-ttu-id="de02a-145">Obtention d'une seule entité</span><span class="sxs-lookup"><span data-stu-id="de02a-145">Get a single entity</span></span>
<span data-ttu-id="de02a-146">Vous pouvez écrire une requête tooget une entité unique et spécifique.</span><span class="sxs-lookup"><span data-stu-id="de02a-146">You can write a query tooget a single, specific entity.</span></span> <span data-ttu-id="de02a-147">code Hello suivant utilise un **TableOperation** toospecify un client nommé « Ben Smith » de l’objet.</span><span class="sxs-lookup"><span data-stu-id="de02a-147">hello following code uses a **TableOperation** object toospecify a customer named 'Ben Smith'.</span></span> <span data-ttu-id="de02a-148">Cette méthode retourne simplement une entité, plutôt qu’une collection et hello a retourné la valeur dans **TableResult.Result** est un **CustomerEntity** objet.</span><span class="sxs-lookup"><span data-stu-id="de02a-148">This method returns just one entity, rather than a collection, and hello returned value in **TableResult.Result** is a **CustomerEntity** object.</span></span> <span data-ttu-id="de02a-149">Spécification des clés de partition et de ligne dans une requête est tooretrieve de manière plus rapide hello une seule entité hello **Table** service.</span><span class="sxs-lookup"><span data-stu-id="de02a-149">Specifying both partition and row keys in a query is hello fastest way tooretrieve a single entity from hello **Table** service.</span></span>

    // Create a retrieve operation that takes a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute hello retrieve operation.
    TableResult retrievedResult = await peopleTable.ExecuteAsync(retrieveOperation);

    // Print hello phone number of hello result.
    if (retrievedResult.Result != null)
       Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
    else
       Console.WriteLine("hello phone number could not be retrieved.");

## <a name="delete-an-entity"></a><span data-ttu-id="de02a-150">Suppression d’une entité</span><span class="sxs-lookup"><span data-stu-id="de02a-150">Delete an entity</span></span>
<span data-ttu-id="de02a-151">Une fois l'entité trouvée, vous pouvez la supprimer.</span><span class="sxs-lookup"><span data-stu-id="de02a-151">You can delete an entity after you find it.</span></span> <span data-ttu-id="de02a-152">Hello de code suivant recherche une entité client nommée « Ben Smith », et si elle le trouve, il le supprime.</span><span class="sxs-lookup"><span data-stu-id="de02a-152">hello following code looks for a customer entity named "Ben Smith", and if it finds it, it deletes it.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="de02a-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="de02a-153">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-tables-next-steps](../../includes/vs-storage-dotnet-tables-next-steps.md)]

