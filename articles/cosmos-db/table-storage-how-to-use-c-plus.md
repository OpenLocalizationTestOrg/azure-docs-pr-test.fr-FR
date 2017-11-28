---
title: Utilisation du stockage Table (C++) | Microsoft Docs
description: "Stockez des données structurées dans le cloud à l’aide du stockage de tables Azure, un magasin de données NoSQL."
services: cosmos-db
documentationcenter: .net
author: mimig1
manager: jahogg
editor: tysonn
ms.assetid: f191f308-e4b2-4de9-85cb-551b82b1ea7c
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: mimig
ms.openlocfilehash: 8314292cdb9b7a3f464c60119ed10f6b06ed4d10
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-table-storage-from-c"></a><span data-ttu-id="20927-103">Utilisation du stockage de table à partir de C++</span><span class="sxs-lookup"><span data-stu-id="20927-103">How to use Table storage from C++</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="20927-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="20927-104">Overview</span></span>
<span data-ttu-id="20927-105">Ce guide décrit le déroulement de scénarios courants dans le cadre de l’utilisation du service de stockage de table Azure.</span><span class="sxs-lookup"><span data-stu-id="20927-105">This guide will show you how to perform common scenarios by using the Azure Table storage service.</span></span> <span data-ttu-id="20927-106">Les exemples ont été écrits en C++ et utilisent la [bibliothèque cliente Azure Storage pour C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="20927-106">The samples are written in C++ and use the [Azure Storage Client Library for C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="20927-107">Les scénarios traités incluent la **création et la suppression d’une table**, ainsi que **l’utilisation d’entités de table**.</span><span class="sxs-lookup"><span data-stu-id="20927-107">The scenarios covered include **creating and deleting a table** and **working with table entities**.</span></span>

> [!NOTE]
> <span data-ttu-id="20927-108">Ce guide cible la bibliothèque cliente Azure Storage pour C++ version 1.0.0 et les versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="20927-108">This guide targets the Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="20927-109">La version recommandée est la bibliothèque cliente de stockage version 2.2.0, disponible par le biais de [NuGet](http://www.nuget.org/packages/wastorage) ou [GitHub](https://github.com/Azure/azure-storage-cpp/).</span><span class="sxs-lookup"><span data-stu-id="20927-109">The recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp/).</span></span>
> 
> 

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="20927-110">Création d’une application C++</span><span class="sxs-lookup"><span data-stu-id="20927-110">Create a C++ application</span></span>
<span data-ttu-id="20927-111">Dans ce guide, vous allez utiliser des fonctionnalités de stockage qui peuvent être exécutées dans une application C++.</span><span class="sxs-lookup"><span data-stu-id="20927-111">In this guide, you will use storage features that can be run within a C++ application.</span></span> <span data-ttu-id="20927-112">Pour ce faire, vous devez installer la bibliothèque cliente Azure Storage pour C++ et créer un compte Azure Storage dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="20927-112">To do so, you will need to install the Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>  

<span data-ttu-id="20927-113">Pour installer la bibliothèque cliente Azure Storage pour C++, vous pouvez procéder comme suit :</span><span class="sxs-lookup"><span data-stu-id="20927-113">To install the Azure Storage Client Library for C++, you can use the following methods:</span></span>

* <span data-ttu-id="20927-114">**Linux :** suivez les instructions disponibles dans la page [Bibliothèque cliente Azure Storage pour C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) .</span><span class="sxs-lookup"><span data-stu-id="20927-114">**Linux:** Follow the instructions given on the [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>  
* <span data-ttu-id="20927-115">**Windows :** dans Visual Studio, cliquez sur **Outils > Gestionnaire de package NuGet > Console du gestionnaire de package**.</span><span class="sxs-lookup"><span data-stu-id="20927-115">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="20927-116">Entrez la commande suivante dans la [console du gestionnaire du package NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) et appuyez sur Entrée.</span><span class="sxs-lookup"><span data-stu-id="20927-116">Type the following command into the [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press Enter.</span></span>  
  
     <span data-ttu-id="20927-117">Install-Package wastorage</span><span class="sxs-lookup"><span data-stu-id="20927-117">Install-Package wastorage</span></span>

## <a name="configure-your-application-to-access-table-storage"></a><span data-ttu-id="20927-118">Configuration de votre application pour accéder au stockage de table</span><span class="sxs-lookup"><span data-stu-id="20927-118">Configure your application to access Table storage</span></span>
<span data-ttu-id="20927-119">Ajoutez l’instruction import suivante au début du fichier C++ dans lequel vous voulez utiliser des API de stockage Azure pour accéder aux tables :</span><span class="sxs-lookup"><span data-stu-id="20927-119">Add the following include statements to the top of the C++ file where you want to use the Azure storage APIs to access tables:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/table.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="20927-120">Configuration d’une chaîne de connexion au stockage Azure</span><span class="sxs-lookup"><span data-stu-id="20927-120">Set up an Azure storage connection string</span></span>
<span data-ttu-id="20927-121">Un client de stockage Azure utilise une chaîne de connexion de stockage pour stocker des points de terminaison et des informations d’identification permettant d’accéder aux services de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="20927-121">An Azure storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="20927-122">Quand vous exécutez une application cliente, vous devez fournir la chaîne de connexion de stockage dans le format suivant.</span><span class="sxs-lookup"><span data-stu-id="20927-122">When running a client application, you must provide the storage connection string in the following format.</span></span> <span data-ttu-id="20927-123">Utilisez le nom de votre compte de stockage et la clé d’accès de stockage pour le compte de stockage répertorié sur le [portail Azure](https://portal.azure.com) pour les valeurs *AccountName* et *AccountKey*.</span><span class="sxs-lookup"><span data-stu-id="20927-123">Use the name of your storage account and the storage access key for the storage account listed in the [Azure Portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="20927-124">Pour plus d’informations sur les comptes et les clés d’accès de stockage, consultez [À propos des comptes Azure Storage](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="20927-124">For information on storage accounts and access keys, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="20927-125">Cet exemple vous montre comment déclarer un champ statique pour qu’il contienne une chaîne de connexion :</span><span class="sxs-lookup"><span data-stu-id="20927-125">This example shows how you can declare a static field to hold the connection string:</span></span>  

```cpp
// Define the connection string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="20927-126">Pour tester votre application sur votre ordinateur Windows local, vous pouvez utiliser [l’émulateur de stockage](../storage/common/storage-use-emulator.md) Azure installé avec le [Kit de développement logiciel (SDK) Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="20927-126">To test your application in your local Windows-based computer, you can use the Azure [storage emulator](../storage/common/storage-use-emulator.md) that is installed with the [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="20927-127">L’émulateur de stockage est un utilitaire qui simule les services Azure d’objet blob, de file d’attente et de table disponibles sur votre ordinateur de développement local.</span><span class="sxs-lookup"><span data-stu-id="20927-127">The storage emulator is a utility that simulates the Azure Blob, Queue, and Table services available on your local development machine.</span></span> <span data-ttu-id="20927-128">L’exemple suivant vous montre comment déclarer un champ statique pour qu’il contienne une chaîne de connexion vers votre émulateur de stockage local :</span><span class="sxs-lookup"><span data-stu-id="20927-128">The following example shows how you can declare a static field to hold the connection string to your local storage emulator:</span></span>  

```cpp
// Define the connection string with Azure storage emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="20927-129">Pour démarrer l’émulateur de stockage Azure, cliquez sur le bouton **Démarrer** ou appuyez sur la touche Windows.</span><span class="sxs-lookup"><span data-stu-id="20927-129">To start the Azure storage emulator, click the **Start** button or press the Windows key.</span></span> <span data-ttu-id="20927-130">Commencez à taper **Émulateur de stockage Azure**, puis sélectionnez **Émulateur de stockage Microsoft Azure** dans la liste des applications.</span><span class="sxs-lookup"><span data-stu-id="20927-130">Begin typing **Azure Storage Emulator**, and then select **Microsoft Azure Storage Emulator** from the list of applications.</span></span>  

<span data-ttu-id="20927-131">Les exemples ci-dessous partent du principe que vous avez utilisé l’une de ces deux méthodes pour obtenir la chaîne de connexion de stockage.</span><span class="sxs-lookup"><span data-stu-id="20927-131">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>  

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="20927-132">Récupération de votre chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="20927-132">Retrieve your connection string</span></span>
<span data-ttu-id="20927-133">Vous pouvez utiliser la classe **cloud_storage_account** pour représenter les informations de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="20927-133">You can use the **cloud_storage_account** class to represent your storage account information.</span></span> <span data-ttu-id="20927-134">Pour extraire les informations de votre compte de stockage de la chaîne de connexion de stockage, vous pouvez utiliser la méthode parse.</span><span class="sxs-lookup"><span data-stu-id="20927-134">To retrieve your storage account information from the storage connection string, you can use the parse method.</span></span>

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

<span data-ttu-id="20927-135">Ensuite, récupérez une référence à une classe **cloud_table_client**, car elle vous permet d’obtenir des objets de référence pour les tables et entités stockées dans le service de stockage de Table.</span><span class="sxs-lookup"><span data-stu-id="20927-135">Next, get a reference to a **cloud_table_client** class, as it lets you get reference objects for tables and entities stored within the Table storage service.</span></span> <span data-ttu-id="20927-136">Le code suivant crée un objet **cloud_table_client** en utilisant l’objet de compte de stockage récupéré ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="20927-136">The following code creates a **cloud_table_client** object by using the storage account object we retrieved above:</span></span>  

```cpp
// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();
```

## <a name="create-a-table"></a><span data-ttu-id="20927-137">Création d’une table</span><span class="sxs-lookup"><span data-stu-id="20927-137">Create a table</span></span>
<span data-ttu-id="20927-138">Un objet **cloud_table_client** vous permet d’obtenir les objets de référence pour les tables et entités.</span><span class="sxs-lookup"><span data-stu-id="20927-138">A **cloud_table_client** object lets you get reference objects for tables and entities.</span></span> <span data-ttu-id="20927-139">Le code suivant crée un objet **cloud_table_client** et l’utilise pour créer une table.</span><span class="sxs-lookup"><span data-stu-id="20927-139">The following code creates a **cloud_table_client** object and uses it to create a new table.</span></span>

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);  

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Retrieve a reference to a table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create the table if it doesn't exist.
table.create_if_not_exists();  
```

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="20927-140">Ajout d'une entité à une table</span><span class="sxs-lookup"><span data-stu-id="20927-140">Add an entity to a table</span></span>
<span data-ttu-id="20927-141">Pour ajouter une entité à une table, créez un objet **table_entity** et transmettez-le à **table_operation::insert_entity**.</span><span class="sxs-lookup"><span data-stu-id="20927-141">To add an entity to a table, create a new **table_entity** object and pass it to **table_operation::insert_entity**.</span></span> <span data-ttu-id="20927-142">Le code suivant utilise le prénom du client en tant que clé de ligne et son nom de famille en tant que clé de partition.</span><span class="sxs-lookup"><span data-stu-id="20927-142">The following code uses the customer's first name as the row key and last name as the partition key.</span></span> <span data-ttu-id="20927-143">Ensemble, les clés de partition et de ligne d’une entité identifient l’entité de façon unique dans la table.</span><span class="sxs-lookup"><span data-stu-id="20927-143">Together, an entity's partition and row key uniquely identify the entity in the table.</span></span> <span data-ttu-id="20927-144">Les requêtes d’entités dont les clés de partition sont identiques sont plus rapides que celles d’entités dont les clés de partition sont différentes, mais le fait d’utiliser différentes clés de partition améliore l’extensibilité des opérations parallèles.</span><span class="sxs-lookup"><span data-stu-id="20927-144">Entities with the same partition key can be queried faster than those with different partition keys, but using diverse partition keys allows for greater parallel operation scalability.</span></span> <span data-ttu-id="20927-145">Pour plus d’informations, consultez [Liste de contrôle des performances et de l’extensibilité de Microsoft Azure Storage](../storage/common/storage-performance-checklist.md).</span><span class="sxs-lookup"><span data-stu-id="20927-145">For more information, see [Microsoft Azure storage performance and scalability checklist](../storage/common/storage-performance-checklist.md).</span></span>

<span data-ttu-id="20927-146">Le code suivant crée une instance de la classe **table_entity** avec des données client à stocker.</span><span class="sxs-lookup"><span data-stu-id="20927-146">The following code creates a new instance of **table_entity** with some customer data to be stored.</span></span> <span data-ttu-id="20927-147">Le code appelle ensuite **table_operation::insert_entity** pour créer un objet **table_operation** pour insérer une entité dans une table et y associer la nouvelle entité de table.</span><span class="sxs-lookup"><span data-stu-id="20927-147">The code next calls **table_operation::insert_entity** to create a **table_operation** object to insert an entity into a table, and associates the new table entity with it.</span></span> <span data-ttu-id="20927-148">Enfin, le code appelle la méthode execute sur l’objet **cloud_table**.</span><span class="sxs-lookup"><span data-stu-id="20927-148">Finally, the code calls the execute method on the **cloud_table** object.</span></span> <span data-ttu-id="20927-149">Puis le nouvel objet **table_operation** envoie une demande au service de Table pour insérer la nouvelle entité de client dans la table « people ».</span><span class="sxs-lookup"><span data-stu-id="20927-149">And the new **table_operation** sends a request to the Table service to insert the new customer entity into the "people" table.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Retrieve a reference to a table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create the table if it doesn't exist.
table.create_if_not_exists();

// Create a new customer entity.
azure::storage::table_entity customer1(U("Harp"), U("Walter"));

azure::storage::table_entity::properties_type& properties = customer1.properties();
properties.reserve(2);
properties[U("Email")] = azure::storage::entity_property(U("Walter@contoso.com"));

properties[U("Phone")] = azure::storage::entity_property(U("425-555-0101"));

// Create the table operation that inserts the customer entity.
azure::storage::table_operation insert_operation = azure::storage::table_operation::insert_entity(customer1);

// Execute the insert operation.
azure::storage::table_result insert_result = table.execute(insert_operation);
```

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="20927-150">Insertion d'un lot d'entités</span><span class="sxs-lookup"><span data-stu-id="20927-150">Insert a batch of entities</span></span>
<span data-ttu-id="20927-151">Vous pouvez insérer un lot d’entités dans le service de Table en une seule opération d’écriture.</span><span class="sxs-lookup"><span data-stu-id="20927-151">You can insert a batch of entities to the Table service in one write operation.</span></span> <span data-ttu-id="20927-152">Le code suivant crée un objet **table_batch_operation**, puis y ajoute trois opérations d’insertion.</span><span class="sxs-lookup"><span data-stu-id="20927-152">The following code creates a **table_batch_operation** object, and then adds three insert operations to it.</span></span> <span data-ttu-id="20927-153">Chaque opération d’insertion est ajoutée en créant un objet d’entité, en définissant ses valeurs, puis en appelant la méthode insert sur l’objet **table_batch_operation** pour associer l’entité avec une nouvelle opération d’insertion.</span><span class="sxs-lookup"><span data-stu-id="20927-153">Each insert operation is added by creating a new entity object, setting its values, and then calling the insert method on the **table_batch_operation** object to associate the entity with a new insert operation.</span></span> <span data-ttu-id="20927-154">La méthode **cloud_table.execute** est ensuite appelée pour exécuter l’opération.</span><span class="sxs-lookup"><span data-stu-id="20927-154">Then, **cloud_table.execute** is called to execute the operation.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Define a batch operation.
azure::storage::table_batch_operation batch_operation;

// Create a customer entity and add it to the table.
azure::storage::table_entity customer1(U("Smith"), U("Jeff"));

azure::storage::table_entity::properties_type& properties1 = customer1.properties();
properties1.reserve(2);
properties1[U("Email")] = azure::storage::entity_property(U("Jeff@contoso.com"));
properties1[U("Phone")] = azure::storage::entity_property(U("425-555-0104"));

// Create another customer entity and add it to the table.
azure::storage::table_entity customer2(U("Smith"), U("Ben"));

azure::storage::table_entity::properties_type& properties2 = customer2.properties();
properties2.reserve(2);
properties2[U("Email")] = azure::storage::entity_property(U("Ben@contoso.com"));
properties2[U("Phone")] = azure::storage::entity_property(U("425-555-0102"));

// Create a third customer entity to add to the table.
azure::storage::table_entity customer3(U("Smith"), U("Denise"));

azure::storage::table_entity::properties_type& properties3 = customer3.properties();
properties3.reserve(2);
properties3[U("Email")] = azure::storage::entity_property(U("Denise@contoso.com"));
properties3[U("Phone")] = azure::storage::entity_property(U("425-555-0103"));

// Add customer entities to the batch insert operation.
batch_operation.insert_or_replace_entity(customer1);
batch_operation.insert_or_replace_entity(customer2);
batch_operation.insert_or_replace_entity(customer3);

// Execute the batch operation.
std::vector<azure::storage::table_result> results = table.execute_batch(batch_operation);
```

<span data-ttu-id="20927-155">Quelques remarques sur les opérations par lots :</span><span class="sxs-lookup"><span data-stu-id="20927-155">Some things to note on batch operations:</span></span>  

* <span data-ttu-id="20927-156">Vous pouvez effectuer jusqu’à 100 opérations d’insertion, de suppression, de fusion, de remplacement, d’insertion ou fusion et d’insertion ou de remplacement dans n’importe quelle combinaison en un seul lot.</span><span class="sxs-lookup"><span data-stu-id="20927-156">You can perform up to 100 insert, delete, merge, replace, insert-or-merge, and insert-or-replace operations in any combination in a single batch.</span></span>  
* <span data-ttu-id="20927-157">Une opération par lot peut comporter une opération d’extraction, s’il s’agit de la seule opération du lot.</span><span class="sxs-lookup"><span data-stu-id="20927-157">A batch operation can have a retrieve operation, if it is the only operation in the batch.</span></span>  
* <span data-ttu-id="20927-158">Toutes les entités d’une opération par lot doivent avoir la même clé de partition.</span><span class="sxs-lookup"><span data-stu-id="20927-158">All entities in a single batch operation must have the same partition key.</span></span>  
* <span data-ttu-id="20927-159">Une opération par lot est limitée à une charge utile de données de 4 Mo.</span><span class="sxs-lookup"><span data-stu-id="20927-159">A batch operation is limited to a 4-MB data payload.</span></span>  

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="20927-160">Extraction de toutes les entités d'une partition</span><span class="sxs-lookup"><span data-stu-id="20927-160">Retrieve all entities in a partition</span></span>
<span data-ttu-id="20927-161">Pour exécuter une requête de table pour toutes les entités d’une partition, utilisez un objet **table_query**.</span><span class="sxs-lookup"><span data-stu-id="20927-161">To query a table for all entities in a partition, use a **table_query** object.</span></span> <span data-ttu-id="20927-162">L’exemple de code suivant indique un filtre pour les entités où ’Smith’ est la clé de partition.</span><span class="sxs-lookup"><span data-stu-id="20927-162">The following code example specifies a filter for entities where 'Smith' is the partition key.</span></span> <span data-ttu-id="20927-163">Il imprime les champs de chaque entité dans les résultats de requête vers la console.</span><span class="sxs-lookup"><span data-stu-id="20927-163">This example prints the fields of each entity in the query results to the console.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Construct the query operation for all customer entities where PartitionKey="Smith".
azure::storage::table_query query;

query.set_filter_string(azure::storage::table_query::generate_filter_condition(U("PartitionKey"), azure::storage::query_comparison_operator::equal, U("Smith")));

// Execute the query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Print the fields for each customer.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    const azure::storage::table_entity::properties_type& properties = it->properties();

    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key()
        << U(", Property1: ") << properties.at(U("Email")).string_value()
        << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
}  
```

<span data-ttu-id="20927-164">La requête de cet exemple affiche toutes les entités qui correspondent aux critères de filtre.</span><span class="sxs-lookup"><span data-stu-id="20927-164">The query in this example brings all the entities that match the filter criteria.</span></span> <span data-ttu-id="20927-165">Si vous avez des tables volumineuses et que vous devez télécharger les entités de table souvent, nous vous recommandons de plutôt stocker vos données dans des objets blob de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="20927-165">If you have large tables and need to download the table entities often, we recommend that you store your data in Azure storage blobs instead.</span></span>

## <a name="retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="20927-166">Extraction d’un ensemble d’entités dans une partition</span><span class="sxs-lookup"><span data-stu-id="20927-166">Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="20927-167">Si vous ne voulez pas exécuter une requête pour toutes les entités d'une partition, vous pouvez spécifier un ensemble en combinant le filtre de clé de partition avec un filtre de clé de ligne.</span><span class="sxs-lookup"><span data-stu-id="20927-167">If you don't want to query all the entities in a partition, you can specify a range by combining the partition key filter with a row key filter.</span></span> <span data-ttu-id="20927-168">L’exemple de code suivant utilise deux filtres pour obtenir toutes les entités dans la partition « Smith » où la clé de ligne (prénom) commence par une lettre située avant la lettre « E » dans l’ordre alphabétique, puis imprime les résultats de la requête.</span><span class="sxs-lookup"><span data-stu-id="20927-168">The following code example uses two filters to get all entities in partition 'Smith' where the row key (first name) starts with a letter earlier than 'E' in the alphabet and then prints the query results.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create the table query.
azure::storage::table_query query;

query.set_filter_string(azure::storage::table_query::combine_filter_conditions(
    azure::storage::table_query::generate_filter_condition(U("PartitionKey"),
    azure::storage::query_comparison_operator::equal, U("Smith")),
    azure::storage::query_logical_operator::op_and,
    azure::storage::table_query::generate_filter_condition(U("RowKey"), azure::storage::query_comparison_operator::less_than, U("E"))));

// Execute the query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Loop through the results, displaying information about the entity.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    const azure::storage::table_entity::properties_type& properties = it->properties();

    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key()
        << U(", Property1: ") << properties.at(U("Email")).string_value()
        << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
}  
```

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="20927-169">Extraction d'une seule entité</span><span class="sxs-lookup"><span data-stu-id="20927-169">Retrieve a single entity</span></span>
<span data-ttu-id="20927-170">Vous pouvez écrire une requête pour extraire une seule entité.</span><span class="sxs-lookup"><span data-stu-id="20927-170">You can write a query to retrieve a single, specific entity.</span></span> <span data-ttu-id="20927-171">Le code suivant utilise **table_operation::retrieve_entity** pour spécifier le client « Jeff Smith ».</span><span class="sxs-lookup"><span data-stu-id="20927-171">The following code uses **table_operation::retrieve_entity** to specify the customer 'Jeff Smith'.</span></span> <span data-ttu-id="20927-172">Cette méthode renvoie une seule entité, au lieu d’une collection. De plus, la valeur renvoyée est dans **table_result**.</span><span class="sxs-lookup"><span data-stu-id="20927-172">This method returns just one entity, rather than a collection, and the returned value is in **table_result**.</span></span> <span data-ttu-id="20927-173">La méthode la plus rapide pour extraire une seule entité dans le service de Table consiste à spécifier une clé de partition et une clé de ligne.</span><span class="sxs-lookup"><span data-stu-id="20927-173">Specifying both partition and row keys in a query is the fastest way to retrieve a single entity from the Table service.</span></span>  

```cpp
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Retrieve the entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Output the entity.
azure::storage::table_entity entity = retrieve_result.entity();
const azure::storage::table_entity::properties_type& properties = entity.properties();

std::wcout << U("PartitionKey: ") << entity.partition_key() << U(", RowKey: ") << entity.row_key()
    << U(", Property1: ") << properties.at(U("Email")).string_value()
    << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
```

## <a name="replace-an-entity"></a><span data-ttu-id="20927-174">Remplacement d’une entité</span><span class="sxs-lookup"><span data-stu-id="20927-174">Replace an entity</span></span>
<span data-ttu-id="20927-175">Pour remplacer une entité, récupérez-la dans le service de Table, modifiez l’objet d’entité, puis enregistrez les modifications dans le service de Table.</span><span class="sxs-lookup"><span data-stu-id="20927-175">To replace an entity, retrieve it from the Table service, modify the entity object, and then save the changes back to the Table service.</span></span> <span data-ttu-id="20927-176">Le code suivant modifie le numéro de téléphone et l’adresse de messagerie électronique d’un client existant.</span><span class="sxs-lookup"><span data-stu-id="20927-176">The following code changes an existing customer's phone number and email address.</span></span> <span data-ttu-id="20927-177">Au lieu d’appeler **table_operation::insert_entity**, ce code utilise **table_operation::replace_entity**.</span><span class="sxs-lookup"><span data-stu-id="20927-177">Instead of calling **table_operation::insert_entity**, this code uses **table_operation::replace_entity**.</span></span> <span data-ttu-id="20927-178">Ceci entraîne le remplacement complet de l’entité sur le serveur, sauf si cette dernière a été modifiée depuis sa récupération, auquel cas l’opération échoue.</span><span class="sxs-lookup"><span data-stu-id="20927-178">This causes the entity to be fully replaced on the server, unless the entity on the server has changed since it was retrieved, in which case the operation will fail.</span></span> <span data-ttu-id="20927-179">Cet échec survient pour empêcher votre application de remplacer par erreur une modification apportée entre la récupération et la mise à jour par un autre composant de votre application.</span><span class="sxs-lookup"><span data-stu-id="20927-179">This failure is to prevent your application from inadvertently overwriting a change made between the retrieval and update by another component of your application.</span></span> <span data-ttu-id="20927-180">Pour gérer correctement cet échec, vous devez récupérer de nouveau l’entité, apporter vos modifications (si elles sont toujours valides), puis effectuer une autre opération **table_operation::replace_entity**.</span><span class="sxs-lookup"><span data-stu-id="20927-180">The proper handling of this failure is to retrieve the entity again, make your changes (if still valid), and then perform another **table_operation::replace_entity** operation.</span></span> <span data-ttu-id="20927-181">La prochaine section vous apprendra à remplacer ce comportement.</span><span class="sxs-lookup"><span data-stu-id="20927-181">The next section will show you how to override this behavior.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Replace an entity.
azure::storage::table_entity entity_to_replace(U("Smith"), U("Jeff"));
azure::storage::table_entity::properties_type& properties_to_replace = entity_to_replace.properties();
properties_to_replace.reserve(2);

// Specify a new phone number.
properties_to_replace[U("Phone")] = azure::storage::entity_property(U("425-555-0106"));

// Specify a new email address.
properties_to_replace[U("Email")] = azure::storage::entity_property(U("JeffS@contoso.com"));

// Create an operation to replace the entity.
azure::storage::table_operation replace_operation = azure::storage::table_operation::replace_entity(entity_to_replace);

// Submit the operation to the Table service.
azure::storage::table_result replace_result = table.execute(replace_operation);
```

## <a name="insert-or-replace-an-entity"></a><span data-ttu-id="20927-182">Insertion ou remplacement d’une entité</span><span class="sxs-lookup"><span data-stu-id="20927-182">Insert-or-replace an entity</span></span>
<span data-ttu-id="20927-183">Les opérations **table_operation::replace_entity** échouent si l’entité est modifiée depuis sa récupération à partir du serveur.</span><span class="sxs-lookup"><span data-stu-id="20927-183">**table_operation::replace_entity** operations will fail if the entity has been changed since it was retrieved from the server.</span></span> <span data-ttu-id="20927-184">De plus, pour que l’opération **table_operation::replace_entity** réussisse, vous devez d’abord récupérer l’entité à partir du serveur.</span><span class="sxs-lookup"><span data-stu-id="20927-184">Furthermore, you must retrieve the entity from the server first in order for **table_operation::replace_entity** to be successful.</span></span> <span data-ttu-id="20927-185">Cependant, il se peut parfois que vous ne sachiez pas si l’entité existe sur le serveur et si les valeurs stockées sont inadaptées. Votre mise à jour doit donc toutes les remplacer.</span><span class="sxs-lookup"><span data-stu-id="20927-185">Sometimes, however, you don't know if the entity exists on the server and the current values stored in it are irrelevant—your update should overwrite them all.</span></span> <span data-ttu-id="20927-186">Pour ce faire, utilisez une opération **table_operation::insert_or_replace_entity**.</span><span class="sxs-lookup"><span data-stu-id="20927-186">To accomplish this, you would use a **table_operation::insert_or_replace_entity** operation.</span></span> <span data-ttu-id="20927-187">Cette opération insère l’entité (s’il n’y en a pas déjà une) ou la remplace (s’il y en a une), indépendamment du moment de la dernière mise à jour.</span><span class="sxs-lookup"><span data-stu-id="20927-187">This operation inserts the entity if it doesn't exist, or replaces it if it does, regardless of when the last update was made.</span></span> <span data-ttu-id="20927-188">Dans l’exemple de code suivant, l’entité de client pour Jeff Smith est toujours récupérée, mais elle est ensuite enregistrée sur le serveur via **table_operation::insert_or_replace_entity**.</span><span class="sxs-lookup"><span data-stu-id="20927-188">In the following code example, the customer entity for Jeff Smith is still retrieved, but it is then saved back to the server via **table_operation::insert_or_replace_entity**.</span></span> <span data-ttu-id="20927-189">Les mises à jour apportées à l’entité entre les opérations de récupération et de mise à jour sont remplacées.</span><span class="sxs-lookup"><span data-stu-id="20927-189">Any updates made to the entity between the retrieval and update operation will be overwritten.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Insert-or-replace an entity.
azure::storage::table_entity entity_to_insert_or_replace(U("Smith"), U("Jeff"));
azure::storage::table_entity::properties_type& properties_to_insert_or_replace = entity_to_insert_or_replace.properties();

properties_to_insert_or_replace.reserve(2);

// Specify a phone number.
properties_to_insert_or_replace[U("Phone")] = azure::storage::entity_property(U("425-555-0107"));

// Specify an email address.
properties_to_insert_or_replace[U("Email")] = azure::storage::entity_property(U("Jeffsm@contoso.com"));

// Create an operation to insert-or-replace the entity.
azure::storage::table_operation insert_or_replace_operation = azure::storage::table_operation::insert_or_replace_entity(entity_to_insert_or_replace);

// Submit the operation to the Table service.
azure::storage::table_result insert_or_replace_result = table.execute(insert_or_replace_operation);
```

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="20927-190">Interrogation d’un sous-ensemble de propriétés d’entité</span><span class="sxs-lookup"><span data-stu-id="20927-190">Query a subset of entity properties</span></span>
<span data-ttu-id="20927-191">Vous pouvez utiliser une requête de table pour extraire uniquement quelques propriétés d’une entité.</span><span class="sxs-lookup"><span data-stu-id="20927-191">A query to a table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="20927-192">La requête contenue dans le code suivant utilise la méthode **table_query::set_select_columns** pour renvoyer uniquement les adresses de messagerie des entités dans la table.</span><span class="sxs-lookup"><span data-stu-id="20927-192">The query in the following code uses the **table_query::set_select_columns** method to return only the email addresses of entities in the table.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Define the query, and select only the Email property.
azure::storage::table_query query;
std::vector<utility::string_t> columns;

columns.push_back(U("Email"));
query.set_select_columns(columns);

// Execute the query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Display the results.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key();

    const azure::storage::table_entity::properties_type& properties = it->properties();
    for (auto prop_it = properties.begin(); prop_it != properties.end(); ++prop_it)
    {
        std::wcout << ", " << prop_it->first << ": " << prop_it->second.str();
    }

    std::wcout << std::endl;
}
```

> [!NOTE]
> <span data-ttu-id="20927-193">L’interrogation d’un petit nombre de propriétés d’une entité est une opération plus efficace que l’extraction de toutes les propriétés.</span><span class="sxs-lookup"><span data-stu-id="20927-193">Querying a few properties from an entity is a more efficient operation than retrieving all properties.</span></span>
> 
> 

## <a name="delete-an-entity"></a><span data-ttu-id="20927-194">Suppression d’une entité</span><span class="sxs-lookup"><span data-stu-id="20927-194">Delete an entity</span></span>
<span data-ttu-id="20927-195">Il est facile de supprimer une entité après l’avoir récupérée.</span><span class="sxs-lookup"><span data-stu-id="20927-195">You can easily delete an entity after you have retrieved it.</span></span> <span data-ttu-id="20927-196">Une fois que l’entité est extraite, appelez **table_operation::delete_entity** avec l’entité à supprimer.</span><span class="sxs-lookup"><span data-stu-id="20927-196">Once the entity is retrieved, call **table_operation::delete_entity** with the entity to delete.</span></span> <span data-ttu-id="20927-197">Appelez ensuite la méthode **cloud_table.execute**.</span><span class="sxs-lookup"><span data-stu-id="20927-197">Then call the **cloud_table.execute** method.</span></span> <span data-ttu-id="20927-198">Le code suivant récupère et supprime une entité dont la clé de partition est « Smith » et la clé de ligne « Jeff ».</span><span class="sxs-lookup"><span data-stu-id="20927-198">The following code retrieves and deletes an entity with a partition key of "Smith" and a row key of "Jeff".</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create an operation to retrieve the entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Create an operation to delete the entity.
azure::storage::table_operation delete_operation = azure::storage::table_operation::delete_entity(retrieve_result.entity());

// Submit the delete operation to the Table service.
azure::storage::table_result delete_result = table.execute(delete_operation);  
```

## <a name="delete-a-table"></a><span data-ttu-id="20927-199">Suppression d’une table</span><span class="sxs-lookup"><span data-stu-id="20927-199">Delete a table</span></span>
<span data-ttu-id="20927-200">Pour finir, l’exemple de code suivant supprime une table d’un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="20927-200">Finally, the following code example deletes a table from a storage account.</span></span> <span data-ttu-id="20927-201">Une table supprimée ne peut plus être recréée pendant un certain temps.</span><span class="sxs-lookup"><span data-stu-id="20927-201">A table that has been deleted will be unavailable to be re-created for a period of time following the deletion.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create an operation to retrieve the entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Create an operation to delete the entity.
azure::storage::table_operation delete_operation = azure::storage::table_operation::delete_entity(retrieve_result.entity());

// Submit the delete operation to the Table service.
azure::storage::table_result delete_result = table.execute(delete_operation);
```

## <a name="next-steps"></a><span data-ttu-id="20927-202">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="20927-202">Next steps</span></span>
<span data-ttu-id="20927-203">Les bases du stockage des tables étant assimilées, voir les liens suivants pour en savoir plus sur Azure Storage :</span><span class="sxs-lookup"><span data-stu-id="20927-203">Now that you've learned the basics of table storage, follow these links to learn more about Azure Storage:</span></span>  

* <span data-ttu-id="20927-204">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) est une application autonome et gratuite de Microsoft qui vous permet d’exploiter visuellement les données de Stockage Azure sur Windows, macOS et Linux.</span><span class="sxs-lookup"><span data-stu-id="20927-204">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* [<span data-ttu-id="20927-205">Utilisation du stockage d’objets blob à partir de C++</span><span class="sxs-lookup"><span data-stu-id="20927-205">How to use Blob storage from C++</span></span>](../storage/blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="20927-206">Utilisation du service de stockage de files d’attente à partir de C++</span><span class="sxs-lookup"><span data-stu-id="20927-206">How to use Queue storage from C++</span></span>](../storage/queues/storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="20927-207">Listage des ressources Azure Storage en C++</span><span class="sxs-lookup"><span data-stu-id="20927-207">List Azure Storage resources in C++</span></span>](../storage/common/storage-c-plus-plus-enumeration.md)
* [<span data-ttu-id="20927-208">Référence de la bibliothèque cliente de stockage pour C++</span><span class="sxs-lookup"><span data-stu-id="20927-208">Storage Client Library for C++ reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="20927-209">Documentation d’Azure Storage</span><span class="sxs-lookup"><span data-stu-id="20927-209">Azure Storage documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
