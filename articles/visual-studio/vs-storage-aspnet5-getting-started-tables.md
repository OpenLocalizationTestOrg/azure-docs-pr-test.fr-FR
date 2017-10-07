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
# <a name="how-tooget-started-with-azure-table-storage-and-visual-studio-connected-services"></a>Comment tooget démarrer avec stockage de Table Azure et Visual Studio services connectés
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a>Vue d'ensemble
Cet article décrit comment obtenir démarré à l’aide de la Table Azure storage dans Visual Studio après avoir créé ou référencé d’un compte de stockage Azure dans un projet ASP.NET Core à l’aide de hello Visual Studio **ajouter des Services connectés** boîte de dialogue.

Hello service de stockage de Table Azure vous permet de toostore de grandes quantités de données structurées. service de Hello est un magasin de données NoSQL qui accepte des appels authentifiés provenant à l’intérieur et extérieur hello cloud Azure. Les tables Azure sont idéales pour le stockage des données structurées non relationnelles.

Hello **ajouter des Services connectés** opération installe hello approprié NuGet packages tooaccess stockage Azure dans votre projet et ajoute la chaîne de connexion hello pour hello du compte de stockage tooyour les fichiers de configuration de projet.

Pour obtenir des informations plus générales sur l’utilisation d’Azure Table Storage, consultez la page [Prise en main du stockage de tables Azure à l’aide de .NET](../storage/storage-dotnet-how-to-use-tables.md).

tooget démarré, vous devez toocreate une table dans votre compte de stockage. Nous allons vous montrer comment toocreate Azure table dans le code. Nous allons également vous montrer comment tooperform table de base et les opérations d’entité, telles que l’ajout, modification, lecture et la lecture de la table entités. exemples de Hello sont écrits en C\# de code et d’utiliser hello bibliothèque cliente de stockage Azure pour .NET.

**Remarque** -certaines hello API qui effectuent des appels de stockage de tooAzure dans ASP.NET Core sont asynchrones. Pour plus d’informations, voir l’article [Programmation asynchrone avec Async et Await](http://msdn.microsoft.com/library/hh191443.aspx) . code Hello ci-dessous suppose que les méthodes de programmation asynchrones sont utilisées.

## <a name="access-tables-in-code"></a>Accès aux tables dans le code
tooaccess des tables dans les projets ASP.NET Core, vous devez hello tooinclude les fichiers source des éléments tooany C# qui a accès au stockage de table Azure suivants.

1. Assurez-vous que les déclarations d’espace de noms hello haut hello du fichier de hello c# incluent ces **à l’aide de** instructions.
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Table;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. Obtenez un objet **CloudStorageAccount** qui représente les informations de votre compte de stockage. Hello utilisation suivant tooget de code hello votre chaîne de connexion de stockage et les informations de compte de stockage à partir de la configuration du service Azure hello.
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
            CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
   
    **Remarque** -utilisent les hello ci-dessus code devant les code hello dans hello suivant des exemples.
3. Obtenir un **CloudTableClient** tooreference les objets de table hello dans votre compte de stockage de l’objet.  
   
        // Create hello table client.
        CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
4. Obtenir un **CloudTable** référence d’objet tooreference une table spécifique et des entités.
   
        // Get a reference tooa table named "peopleTable"
        CloudTable table = tableClient.GetTableReference("peopleTable");

## <a name="create-a-table-in-code"></a>Création d'une table dans le code
toocreate hello table Azure, ajoutez simplement un appel trop**CreateIfNotExistsAsync()**.

    // Create hello CloudTable if it does not exist
    await table.CreateIfNotExistsAsync();

## <a name="add-an-entity-tooa-table"></a>Ajouter une table de tooa d’entité
tooadd une table de tooa entité que vous créez une classe qui définit les propriétés de hello de votre entité. Hello de code suivant définit une classe d’entité appelée **CustomerEntity** qu’utilise hello prénom du client en tant que clé de ligne hello et le nom comme clé de partition hello.

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

Opérations de table impliquant des entités sont effectuées à l’aide de hello **CloudTable** de l’objet créé dans « Accéder aux tables dans le code ». Hello **TableOperation** objet représente hello opération toobe est terminé. Hello suivant exemple de code montre comment toocreate un **CloudTable** objet et un **CustomerEntity** objet. opération de hello tooprepare, un **TableOperation** est créé entité customer de hello tooinsert dans la table de hello. Enfin, l’opération de hello est exécutée en appelant CloudTable.ExecuteAsync.

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    customer1.PhoneNumber = "425-555-0101";

    // Create hello TableOperation that inserts hello customer entity.
    TableOperation insertOperation = TableOperation.Insert(customer1);

    // Execute hello insert operation.
    await peopleTable.ExecuteAsync(insertOperation);

## <a name="insert-a-batch-of-entities"></a>Insertion d’un lot d’entités
Vous pouvez insérer plusieurs entités dans une table en une seule opération d'écriture. Hello exemple de code suivant crée deux objets d’entité (« Jeff Smith » et « Ben Smith »), les ajoute tooa **TableBatchOperation** objet à l’aide de hello **insérer** méthode, puis l’opération de hello commence par appel de CloudTable.ExecuteBatchAsync.

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

## <a name="get-all-of-hello-entities-in-a-partition"></a>Obtenir toutes les entités de hello dans une partition
tooquery une table pour toutes les entités hello dans une partition, utilisez un **TableQuery** objet. Hello exemple de code suivant spécifie un filtre pour les entités où « Smith » est la clé de partition hello. Cet exemple imprime les champs de chaque entité dans la console de toohello de résultats de requête hello hello.

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

## <a name="get-a-single-entity"></a>Obtention d'une seule entité
Vous pouvez écrire une requête tooget une entité unique et spécifique. code Hello suivant utilise un **TableOperation** toospecify un client nommé « Ben Smith » de l’objet. Cette méthode retourne simplement une entité, plutôt qu’une collection et hello a retourné la valeur dans **TableResult.Result** est un **CustomerEntity** objet. Spécification des clés de partition et de ligne dans une requête est tooretrieve de manière plus rapide hello une seule entité hello **Table** service.

    // Create a retrieve operation that takes a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute hello retrieve operation.
    TableResult retrievedResult = await peopleTable.ExecuteAsync(retrieveOperation);

    // Print hello phone number of hello result.
    if (retrievedResult.Result != null)
       Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
    else
       Console.WriteLine("hello phone number could not be retrieved.");

## <a name="delete-an-entity"></a>Suppression d’une entité
Une fois l'entité trouvée, vous pouvez la supprimer. Hello de code suivant recherche une entité client nommée « Ben Smith » et si elle le trouve, il le supprime.

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

## <a name="next-steps"></a>Étapes suivantes
[!INCLUDE [vs-storage-dotnet-tables-next-steps](../../includes/vs-storage-dotnet-tables-next-steps.md)]

