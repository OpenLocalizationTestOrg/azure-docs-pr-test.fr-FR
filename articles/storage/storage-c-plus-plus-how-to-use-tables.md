---
title: aaaHow toouse le stockage de Table (C++) | Documents Microsoft
description: "Stocker des données structurées dans le cloud hello avec le stockage Table Azure, un magasin de données NoSQL."
services: storage
documentationcenter: .net
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: f191f308-e4b2-4de9-85cb-551b82b1ea7c
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: seguler
ms.openlocfilehash: 8eee0031350ab6ff3f76fb288b2f896687aa17a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-from-c"></a><span data-ttu-id="381db-103">Comment toouse le stockage de Table à partir de C++</span><span class="sxs-lookup"><span data-stu-id="381db-103">How toouse Table storage from C++</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="381db-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="381db-104">Overview</span></span>
<span data-ttu-id="381db-105">Ce guide explique comment tooperform des scénarios courants à l’aide de hello service de stockage de Table Azure.</span><span class="sxs-lookup"><span data-stu-id="381db-105">This guide will show you how tooperform common scenarios by using hello Azure Table storage service.</span></span> <span data-ttu-id="381db-106">exemples de Hello sont écrits en C++ et utiliser hello [bibliothèque cliente de stockage Azure pour C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="381db-106">hello samples are written in C++ and use hello [Azure Storage Client Library for C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="381db-107">Hello scénarios abordés incluent **création et suppression d’une table** et **utilisation des entités de table**.</span><span class="sxs-lookup"><span data-stu-id="381db-107">hello scenarios covered include **creating and deleting a table** and **working with table entities**.</span></span>

> [!NOTE]
> <span data-ttu-id="381db-108">Les cibles de ce guide hello bibliothèque cliente Azure Storage pour C++ version 1.0.0 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="381db-108">This guide targets hello Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="381db-109">Hello recommandé de version est la bibliothèque cliente de stockage 2.2.0, qui est disponible via [NuGet](http://www.nuget.org/packages/wastorage) ou [GitHub](https://github.com/Azure/azure-storage-cpp/).</span><span class="sxs-lookup"><span data-stu-id="381db-109">hello recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp/).</span></span>
> 
> 

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="381db-110">Création d’une application C++</span><span class="sxs-lookup"><span data-stu-id="381db-110">Create a C++ application</span></span>
<span data-ttu-id="381db-111">Dans ce guide, vous allez utiliser des fonctionnalités de stockage qui peuvent être exécutées dans une application C++.</span><span class="sxs-lookup"><span data-stu-id="381db-111">In this guide, you will use storage features that can be run within a C++ application.</span></span> <span data-ttu-id="381db-112">toodo par conséquent, vous devez tooinstall hello bibliothèque cliente Azure Storage pour C++ et créer un compte de stockage Azure dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="381db-112">toodo so, you will need tooinstall hello Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>  

<span data-ttu-id="381db-113">tooinstall hello bibliothèque cliente Azure Storage pour C++, vous pouvez utiliser hello méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="381db-113">tooinstall hello Azure Storage Client Library for C++, you can use hello following methods:</span></span>

* <span data-ttu-id="381db-114">**Linux :** suivez les indications hello hello [bibliothèque cliente de stockage Azure pour C++ Lisez-moi](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span><span class="sxs-lookup"><span data-stu-id="381db-114">**Linux:** Follow hello instructions given on hello [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>  
* <span data-ttu-id="381db-115">**Windows :** dans Visual Studio, cliquez sur **Outils &gt; Gestionnaire de package NuGet &gt; Console du gestionnaire de package**.</span><span class="sxs-lookup"><span data-stu-id="381db-115">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="381db-116">Tapez ce qui suit hello commande dans hello [console du Gestionnaire de Package NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) et appuyez sur ENTRÉE.</span><span class="sxs-lookup"><span data-stu-id="381db-116">Type hello following command into hello [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press Enter.</span></span>  
  
     <span data-ttu-id="381db-117">Install-Package wastorage</span><span class="sxs-lookup"><span data-stu-id="381db-117">Install-Package wastorage</span></span>

## <a name="configure-your-application-tooaccess-table-storage"></a><span data-ttu-id="381db-118">Configurer votre application de tooaccess le stockage de Table</span><span class="sxs-lookup"><span data-stu-id="381db-118">Configure your application tooaccess Table storage</span></span>
<span data-ttu-id="381db-119">Ajouter suivant de hello inclure haut de toohello d’instructions de hello C++ fichier dans lequel les tables tooaccess API toouse hello stockage Azure :</span><span class="sxs-lookup"><span data-stu-id="381db-119">Add hello following include statements toohello top of hello C++ file where you want toouse hello Azure storage APIs tooaccess tables:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/table.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="381db-120">Configuration d’une chaîne de connexion au stockage Azure</span><span class="sxs-lookup"><span data-stu-id="381db-120">Set up an Azure storage connection string</span></span>
<span data-ttu-id="381db-121">Un client de stockage Azure utilise une terminaison de stockage connexion chaîne toostore et informations d’identification pour accéder aux services de gestion de données.</span><span class="sxs-lookup"><span data-stu-id="381db-121">An Azure storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="381db-122">Lors de l’exécution d’une application cliente, vous devez fournir la chaîne de connexion de stockage hello Bonjour suivant le format.</span><span class="sxs-lookup"><span data-stu-id="381db-122">When running a client application, you must provide hello storage connection string in hello following format.</span></span> <span data-ttu-id="381db-123">Utiliser le nom de votre compte et hello stockage clé d’accès pour le compte de stockage hello hello répertoriés dans hello [Azure Portal](https://portal.azure.com) pour hello *AccountName* et *AccountKey* valeurs.</span><span class="sxs-lookup"><span data-stu-id="381db-123">Use hello name of your storage account and hello storage access key for hello storage account listed in hello [Azure Portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="381db-124">Pour plus d’informations sur les comptes et les clés d’accès de stockage, consultez [À propos des comptes Azure Storage](storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="381db-124">For information on storage accounts and access keys, see [About Azure storage accounts](storage-create-storage-account.md).</span></span> <span data-ttu-id="381db-125">Cet exemple montre comment vous pouvez déclarer une chaîne de connexion de champ statique toohold hello :</span><span class="sxs-lookup"><span data-stu-id="381db-125">This example shows how you can declare a static field toohold hello connection string:</span></span>  

```cpp
// Define hello connection string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="381db-126">tootest votre application sur votre ordinateur local basé sur Windows, vous pouvez utiliser hello Azure [l’émulateur de stockage](storage-use-emulator.md) qui est installé avec hello [Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="381db-126">tootest your application in your local Windows-based computer, you can use hello Azure [storage emulator](storage-use-emulator.md) that is installed with hello [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="381db-127">l’émulateur de stockage Hello est un utilitaire qui simule hello Azure Blob, file d’attente et Table services disponibles sur votre ordinateur de développement local.</span><span class="sxs-lookup"><span data-stu-id="381db-127">hello storage emulator is a utility that simulates hello Azure Blob, Queue, and Table services available on your local development machine.</span></span> <span data-ttu-id="381db-128">Hello suivant montre comment vous pouvez déclarer un champ statique toohold hello connexion chaîne tooyour local l’émulateur de stockage :</span><span class="sxs-lookup"><span data-stu-id="381db-128">hello following example shows how you can declare a static field toohold hello connection string tooyour local storage emulator:</span></span>  

```cpp
// Define hello connection string with Azure storage emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="381db-129">toostart hello émulateur de stockage Azure, cliquez sur hello **Démarrer** bouton ou appuyez sur clé de Windows hello.</span><span class="sxs-lookup"><span data-stu-id="381db-129">toostart hello Azure storage emulator, click hello **Start** button or press hello Windows key.</span></span> <span data-ttu-id="381db-130">Commencez à taper **émulateur de stockage Azure**, puis sélectionnez **émulateur de stockage Microsoft Azure** à partir de la liste des applications hello.</span><span class="sxs-lookup"><span data-stu-id="381db-130">Begin typing **Azure Storage Emulator**, and then select **Microsoft Azure Storage Emulator** from hello list of applications.</span></span>  

<span data-ttu-id="381db-131">Hello exemples suivants supposent que vous avez utilisé une de ces chaînes de connexion de stockage de deux méthodes tooget hello.</span><span class="sxs-lookup"><span data-stu-id="381db-131">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>  

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="381db-132">Récupération de votre chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="381db-132">Retrieve your connection string</span></span>
<span data-ttu-id="381db-133">Vous pouvez utiliser hello **cloud_storage_account** classe toorepresent vos informations de compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="381db-133">You can use hello **cloud_storage_account** class toorepresent your storage account information.</span></span> <span data-ttu-id="381db-134">tooretrieve plus d’informations à partir de la chaîne de connexion de stockage hello du compte de votre stockage, vous pouvez utiliser la méthode d’analyse hello.</span><span class="sxs-lookup"><span data-stu-id="381db-134">tooretrieve your storage account information from hello storage connection string, you can use hello parse method.</span></span>

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

<span data-ttu-id="381db-135">Ensuite, obtenez une référence tooa **cloud_table_client** de classe, comme il vous permet d’obtenir des objets de référence pour les tables et entités stockées dans hello service de stockage de Table.</span><span class="sxs-lookup"><span data-stu-id="381db-135">Next, get a reference tooa **cloud_table_client** class, as it lets you get reference objects for tables and entities stored within hello Table storage service.</span></span> <span data-ttu-id="381db-136">Hello de code suivant crée un **cloud_table_client** objet à l’aide d’objet de compte de stockage hello nous récupérées ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="381db-136">hello following code creates a **cloud_table_client** object by using hello storage account object we retrieved above:</span></span>  

```cpp
// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();
```

## <a name="create-a-table"></a><span data-ttu-id="381db-137">Création d’une table</span><span class="sxs-lookup"><span data-stu-id="381db-137">Create a table</span></span>
<span data-ttu-id="381db-138">Un objet **cloud_table_client** vous permet d’obtenir les objets de référence pour les tables et entités.</span><span class="sxs-lookup"><span data-stu-id="381db-138">A **cloud_table_client** object lets you get reference objects for tables and entities.</span></span> <span data-ttu-id="381db-139">Hello de code suivant crée un **cloud_table_client** de l’objet et l’utilise toocreate une nouvelle table.</span><span class="sxs-lookup"><span data-stu-id="381db-139">hello following code creates a **cloud_table_client** object and uses it toocreate a new table.</span></span>

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);  

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Retrieve a reference tooa table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create hello table if it doesn't exist.
table.create_if_not_exists();  
```

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="381db-140">Ajouter une table de tooa d’entité</span><span class="sxs-lookup"><span data-stu-id="381db-140">Add an entity tooa table</span></span>
<span data-ttu-id="381db-141">tooadd une table de tooa entité, créez un **table_entity** de l’objet et lui passer trop**table_operation::insert_entity**.</span><span class="sxs-lookup"><span data-stu-id="381db-141">tooadd an entity tooa table, create a new **table_entity** object and pass it too**table_operation::insert_entity**.</span></span> <span data-ttu-id="381db-142">Hello de code suivant utilise prénom du client hello en tant que clé de ligne hello et le nom comme clé de partition hello.</span><span class="sxs-lookup"><span data-stu-id="381db-142">hello following code uses hello customer's first name as hello row key and last name as hello partition key.</span></span> <span data-ttu-id="381db-143">Ensemble, les partitions d’une entité et la clé de ligne identifient hello entité dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="381db-143">Together, an entity's partition and row key uniquely identify hello entity in hello table.</span></span> <span data-ttu-id="381db-144">Entités avec hello même clé de partition peut être interrogé plus rapidement que les différents avec des clés de partition, mais à l’aide de clés de partition divers permet une plus grande évolutivité de l’opération parallèle.</span><span class="sxs-lookup"><span data-stu-id="381db-144">Entities with hello same partition key can be queried faster than those with different partition keys, but using diverse partition keys allows for greater parallel operation scalability.</span></span> <span data-ttu-id="381db-145">Pour plus d’informations, consultez [Liste de contrôle des performances et de l’extensibilité de Microsoft Azure Storage](storage-performance-checklist.md).</span><span class="sxs-lookup"><span data-stu-id="381db-145">For more information, see [Microsoft Azure storage performance and scalability checklist](storage-performance-checklist.md).</span></span>

<span data-ttu-id="381db-146">Hello de code suivant crée une nouvelle instance de **table_entity** avec certaines toobe de données client stockée.</span><span class="sxs-lookup"><span data-stu-id="381db-146">hello following code creates a new instance of **table_entity** with some customer data toobe stored.</span></span> <span data-ttu-id="381db-147">Hello de code suivante appelle **table_operation::insert_entity** toocreate un **table_operation** tooinsert une entité de l’objet dans une table, et associe hello nouvelle entité de table avec lui.</span><span class="sxs-lookup"><span data-stu-id="381db-147">hello code next calls **table_operation::insert_entity** toocreate a **table_operation** object tooinsert an entity into a table, and associates hello new table entity with it.</span></span> <span data-ttu-id="381db-148">Enfin, les appels de code hello hello exécuter la méthode sur hello **cloud_table** objet.</span><span class="sxs-lookup"><span data-stu-id="381db-148">Finally, hello code calls hello execute method on hello **cloud_table** object.</span></span> <span data-ttu-id="381db-149">Et hello nouvelle **table_operation** envoie une demande de toohello Table service tooinsert hello nouvelle entité customer dans la table « people » de hello.</span><span class="sxs-lookup"><span data-stu-id="381db-149">And hello new **table_operation** sends a request toohello Table service tooinsert hello new customer entity into hello "people" table.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Retrieve a reference tooa table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create hello table if it doesn't exist.
table.create_if_not_exists();

// Create a new customer entity.
azure::storage::table_entity customer1(U("Harp"), U("Walter"));

azure::storage::table_entity::properties_type& properties = customer1.properties();
properties.reserve(2);
properties[U("Email")] = azure::storage::entity_property(U("Walter@contoso.com"));

properties[U("Phone")] = azure::storage::entity_property(U("425-555-0101"));

// Create hello table operation that inserts hello customer entity.
azure::storage::table_operation insert_operation = azure::storage::table_operation::insert_entity(customer1);

// Execute hello insert operation.
azure::storage::table_result insert_result = table.execute(insert_operation);
```

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="381db-150">Insertion d’un lot d’entités</span><span class="sxs-lookup"><span data-stu-id="381db-150">Insert a batch of entities</span></span>
<span data-ttu-id="381db-151">Vous pouvez insérer un lot d’entités toohello service de Table dans une opération d’écriture.</span><span class="sxs-lookup"><span data-stu-id="381db-151">You can insert a batch of entities toohello Table service in one write operation.</span></span> <span data-ttu-id="381db-152">Hello de code suivant crée un **table_batch_operation** de l’objet, puis ajoute trois insérer tooit d’opérations.</span><span class="sxs-lookup"><span data-stu-id="381db-152">hello following code creates a **table_batch_operation** object, and then adds three insert operations tooit.</span></span> <span data-ttu-id="381db-153">Chaque opération d’insertion est ajoutée en créant un nouvel objet d’entité, ses valeurs, et puis en appelant hello insérer la méthode sur hello **table_batch_operation** objet entité de hello tooassociate avec une nouvelle opération d’insertion.</span><span class="sxs-lookup"><span data-stu-id="381db-153">Each insert operation is added by creating a new entity object, setting its values, and then calling hello insert method on hello **table_batch_operation** object tooassociate hello entity with a new insert operation.</span></span> <span data-ttu-id="381db-154">Ensuite, **cloud_table.execute** est appelé l’opération de hello tooexecute.</span><span class="sxs-lookup"><span data-stu-id="381db-154">Then, **cloud_table.execute** is called tooexecute hello operation.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Define a batch operation.
azure::storage::table_batch_operation batch_operation;

// Create a customer entity and add it toohello table.
azure::storage::table_entity customer1(U("Smith"), U("Jeff"));

azure::storage::table_entity::properties_type& properties1 = customer1.properties();
properties1.reserve(2);
properties1[U("Email")] = azure::storage::entity_property(U("Jeff@contoso.com"));
properties1[U("Phone")] = azure::storage::entity_property(U("425-555-0104"));

// Create another customer entity and add it toohello table.
azure::storage::table_entity customer2(U("Smith"), U("Ben"));

azure::storage::table_entity::properties_type& properties2 = customer2.properties();
properties2.reserve(2);
properties2[U("Email")] = azure::storage::entity_property(U("Ben@contoso.com"));
properties2[U("Phone")] = azure::storage::entity_property(U("425-555-0102"));

// Create a third customer entity tooadd toohello table.
azure::storage::table_entity customer3(U("Smith"), U("Denise"));

azure::storage::table_entity::properties_type& properties3 = customer3.properties();
properties3.reserve(2);
properties3[U("Email")] = azure::storage::entity_property(U("Denise@contoso.com"));
properties3[U("Phone")] = azure::storage::entity_property(U("425-555-0103"));

// Add customer entities toohello batch insert operation.
batch_operation.insert_or_replace_entity(customer1);
batch_operation.insert_or_replace_entity(customer2);
batch_operation.insert_or_replace_entity(customer3);

// Execute hello batch operation.
std::vector<azure::storage::table_result> results = table.execute_batch(batch_operation);
```

<span data-ttu-id="381db-155">Toonote de certaines opérations sur les opérations de traitement par lots :</span><span class="sxs-lookup"><span data-stu-id="381db-155">Some things toonote on batch operations:</span></span>  

* <span data-ttu-id="381db-156">Vous pouvez effectuer des too100 insert, delete, merge, replace, opérations insert ou merge et insérer ou remplacer dans n’importe quelle combinaison dans un lot unique.</span><span class="sxs-lookup"><span data-stu-id="381db-156">You can perform up too100 insert, delete, merge, replace, insert-or-merge, and insert-or-replace operations in any combination in a single batch.</span></span>  
* <span data-ttu-id="381db-157">Une opération de traitement peut avoir une opération de récupération, s’il est la seule opération de hello dans un lot de hello.</span><span class="sxs-lookup"><span data-stu-id="381db-157">A batch operation can have a retrieve operation, if it is hello only operation in hello batch.</span></span>  
* <span data-ttu-id="381db-158">Toutes les entités dans une seule opération doivent avoir hello même clé de partition.</span><span class="sxs-lookup"><span data-stu-id="381db-158">All entities in a single batch operation must have hello same partition key.</span></span>  
* <span data-ttu-id="381db-159">Une opération de traitement est la charge utile de données de 4 Mo tooa limité.</span><span class="sxs-lookup"><span data-stu-id="381db-159">A batch operation is limited tooa 4-MB data payload.</span></span>  

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="381db-160">Extraction de toutes les entités d'une partition</span><span class="sxs-lookup"><span data-stu-id="381db-160">Retrieve all entities in a partition</span></span>
<span data-ttu-id="381db-161">tooquery une table pour toutes les entités dans une partition, utilisez un **table_query** objet.</span><span class="sxs-lookup"><span data-stu-id="381db-161">tooquery a table for all entities in a partition, use a **table_query** object.</span></span> <span data-ttu-id="381db-162">Hello exemple de code suivant spécifie un filtre pour les entités où « Smith » est la clé de partition hello.</span><span class="sxs-lookup"><span data-stu-id="381db-162">hello following code example specifies a filter for entities where 'Smith' is hello partition key.</span></span> <span data-ttu-id="381db-163">Cet exemple imprime les champs de chaque entité dans la console de toohello de résultats de requête hello hello.</span><span class="sxs-lookup"><span data-stu-id="381db-163">This example prints hello fields of each entity in hello query results toohello console.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Construct hello query operation for all customer entities where PartitionKey="Smith".
azure::storage::table_query query;

query.set_filter_string(azure::storage::table_query::generate_filter_condition(U("PartitionKey"), azure::storage::query_comparison_operator::equal, U("Smith")));

// Execute hello query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Print hello fields for each customer.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    const azure::storage::table_entity::properties_type& properties = it->properties();

    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key()
        << U(", Property1: ") << properties.at(U("Email")).string_value()
        << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
}  
```

<span data-ttu-id="381db-164">requête Hello dans cet exemple met toutes les entités hello qui correspondent aux critères de filtre hello.</span><span class="sxs-lookup"><span data-stu-id="381db-164">hello query in this example brings all hello entities that match hello filter criteria.</span></span> <span data-ttu-id="381db-165">Si vous avez des tables volumineuses et que vous devez souvent les entités de table toodownload hello, nous vous recommandons que vous stockez vos données dans des objets BLOB de stockage Azure à la place.</span><span class="sxs-lookup"><span data-stu-id="381db-165">If you have large tables and need toodownload hello table entities often, we recommend that you store your data in Azure storage blobs instead.</span></span>

## <a name="retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="381db-166">Extraction d’un ensemble d’entités dans une partition</span><span class="sxs-lookup"><span data-stu-id="381db-166">Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="381db-167">Si vous ne souhaitez pas tooquery toutes les entités hello dans une partition, vous pouvez spécifier une plage en combinant le filtre de clé de partition hello avec un filtre de clé de ligne.</span><span class="sxs-lookup"><span data-stu-id="381db-167">If you don't want tooquery all hello entities in a partition, you can specify a range by combining hello partition key filter with a row key filter.</span></span> <span data-ttu-id="381db-168">Hello exemple de code suivant utilise deux filtres tooget toutes les entités dans la partition « Smith », où la clé de ligne hello (prénom) commence par une lettre « E » dans l’alphabet de hello plus tôt et imprime ensuite les résultats de la requête hello.</span><span class="sxs-lookup"><span data-stu-id="381db-168">hello following code example uses two filters tooget all entities in partition 'Smith' where hello row key (first name) starts with a letter earlier than 'E' in hello alphabet and then prints hello query results.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create hello table query.
azure::storage::table_query query;

query.set_filter_string(azure::storage::table_query::combine_filter_conditions(
    azure::storage::table_query::generate_filter_condition(U("PartitionKey"),
    azure::storage::query_comparison_operator::equal, U("Smith")),
    azure::storage::query_logical_operator::op_and,
    azure::storage::table_query::generate_filter_condition(U("RowKey"), azure::storage::query_comparison_operator::less_than, U("E"))));

// Execute hello query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Loop through hello results, displaying information about hello entity.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    const azure::storage::table_entity::properties_type& properties = it->properties();

    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key()
        << U(", Property1: ") << properties.at(U("Email")).string_value()
        << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
}  
```

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="381db-169">Extraction d'une seule entité</span><span class="sxs-lookup"><span data-stu-id="381db-169">Retrieve a single entity</span></span>
<span data-ttu-id="381db-170">Vous pouvez écrire une requête tooretrieve une entité unique et spécifique.</span><span class="sxs-lookup"><span data-stu-id="381db-170">You can write a query tooretrieve a single, specific entity.</span></span> <span data-ttu-id="381db-171">code Hello suivant utilise **table_operation::retrieve_entity** client de hello toospecify « Jeff Smith ».</span><span class="sxs-lookup"><span data-stu-id="381db-171">hello following code uses **table_operation::retrieve_entity** toospecify hello customer 'Jeff Smith'.</span></span> <span data-ttu-id="381db-172">Cette méthode renvoie qu’une seule entité, plutôt qu’une collection et hello valeur retournée dans **table_result**.</span><span class="sxs-lookup"><span data-stu-id="381db-172">This method returns just one entity, rather than a collection, and hello returned value is in **table_result**.</span></span> <span data-ttu-id="381db-173">Spécification des clés de partition et de ligne dans une requête est tooretrieve de manière plus rapide hello une seule entité hello service de Table.</span><span class="sxs-lookup"><span data-stu-id="381db-173">Specifying both partition and row keys in a query is hello fastest way tooretrieve a single entity from hello Table service.</span></span>  

```cpp
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Retrieve hello entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Output hello entity.
azure::storage::table_entity entity = retrieve_result.entity();
const azure::storage::table_entity::properties_type& properties = entity.properties();

std::wcout << U("PartitionKey: ") << entity.partition_key() << U(", RowKey: ") << entity.row_key()
    << U(", Property1: ") << properties.at(U("Email")).string_value()
    << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
```

## <a name="replace-an-entity"></a><span data-ttu-id="381db-174">Remplacement d’une entité</span><span class="sxs-lookup"><span data-stu-id="381db-174">Replace an entity</span></span>
<span data-ttu-id="381db-175">tooreplace une entité, récupérer à partir du service de Table hello, modifier l’objet d’entité hello, puis enregistrez les modifications hello de nouveau service de Table toohello.</span><span class="sxs-lookup"><span data-stu-id="381db-175">tooreplace an entity, retrieve it from hello Table service, modify hello entity object, and then save hello changes back toohello Table service.</span></span> <span data-ttu-id="381db-176">Hello code suivant modifie l’adresse de messagerie et le numéro du téléphone d’un client existant.</span><span class="sxs-lookup"><span data-stu-id="381db-176">hello following code changes an existing customer's phone number and email address.</span></span> <span data-ttu-id="381db-177">Au lieu d’appeler **table_operation::insert_entity**, ce code utilise **table_operation::replace_entity**.</span><span class="sxs-lookup"><span data-stu-id="381db-177">Instead of calling **table_operation::insert_entity**, this code uses **table_operation::replace_entity**.</span></span> <span data-ttu-id="381db-178">Cela provoque une toobe d’entité hello entièrement remplacé sur le serveur de hello, sauf si l’entité hello sur le serveur de hello a changé depuis sa récupération, auquel cas hello échoue.</span><span class="sxs-lookup"><span data-stu-id="381db-178">This causes hello entity toobe fully replaced on hello server, unless hello entity on hello server has changed since it was retrieved, in which case hello operation will fail.</span></span> <span data-ttu-id="381db-179">Cet échec est tooprevent votre application à partir de remplacement accidentel d’une modification effectuée entre hello récupération et mettre à jour par un autre composant de votre application.</span><span class="sxs-lookup"><span data-stu-id="381db-179">This failure is tooprevent your application from inadvertently overwriting a change made between hello retrieval and update by another component of your application.</span></span> <span data-ttu-id="381db-180">Hello gestion correcte de cet échec est tooretrieve hello entité à nouveau, apportez vos modifications (si elle est toujours valide), puis effectuer une autre **table_operation::replace_entity** opération.</span><span class="sxs-lookup"><span data-stu-id="381db-180">hello proper handling of this failure is tooretrieve hello entity again, make your changes (if still valid), and then perform another **table_operation::replace_entity** operation.</span></span> <span data-ttu-id="381db-181">Hello prochaine section vous montrera comment toooverride ce comportement.</span><span class="sxs-lookup"><span data-stu-id="381db-181">hello next section will show you how toooverride this behavior.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Replace an entity.
azure::storage::table_entity entity_to_replace(U("Smith"), U("Jeff"));
azure::storage::table_entity::properties_type& properties_to_replace = entity_to_replace.properties();
properties_to_replace.reserve(2);

// Specify a new phone number.
properties_to_replace[U("Phone")] = azure::storage::entity_property(U("425-555-0106"));

// Specify a new email address.
properties_to_replace[U("Email")] = azure::storage::entity_property(U("JeffS@contoso.com"));

// Create an operation tooreplace hello entity.
azure::storage::table_operation replace_operation = azure::storage::table_operation::replace_entity(entity_to_replace);

// Submit hello operation toohello Table service.
azure::storage::table_result replace_result = table.execute(replace_operation);
```

## <a name="insert-or-replace-an-entity"></a><span data-ttu-id="381db-182">Insertion ou remplacement d’une entité</span><span class="sxs-lookup"><span data-stu-id="381db-182">Insert-or-replace an entity</span></span>
<span data-ttu-id="381db-183">**table_operation::replace_entity** opérations échouent si l’entité de hello a été modifiée, car il a été récupéré à partir du serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="381db-183">**table_operation::replace_entity** operations will fail if hello entity has been changed since it was retrieved from hello server.</span></span> <span data-ttu-id="381db-184">En outre, vous devez récupérer des entités de hello de hello serveur tout d’abord pour **table_operation::replace_entity** toobe réussie.</span><span class="sxs-lookup"><span data-stu-id="381db-184">Furthermore, you must retrieve hello entity from hello server first in order for **table_operation::replace_entity** toobe successful.</span></span> <span data-ttu-id="381db-185">Dans certains cas, toutefois, vous ne connaissez pas si l’entité hello existe sur le serveur de hello et les valeurs actuelles hello stockés qu’il contient sont sans intérêt, votre mise à jour doit remplacer toutes les.</span><span class="sxs-lookup"><span data-stu-id="381db-185">Sometimes, however, you don't know if hello entity exists on hello server and hello current values stored in it are irrelevant—your update should overwrite them all.</span></span> <span data-ttu-id="381db-186">tooaccomplish, vous devez utiliser un **table_operation::insert_or_replace_entity** opération.</span><span class="sxs-lookup"><span data-stu-id="381db-186">tooaccomplish this, you would use a **table_operation::insert_or_replace_entity** operation.</span></span> <span data-ttu-id="381db-187">Cette opération insère l’entité de hello si elle n’existe pas ou elle remplace dans ce cas, quelle que soit la lorsque la dernière mise à jour de hello a été effectuée.</span><span class="sxs-lookup"><span data-stu-id="381db-187">This operation inserts hello entity if it doesn't exist, or replaces it if it does, regardless of when hello last update was made.</span></span> <span data-ttu-id="381db-188">Dans l’exemple de code suivant de hello, entité customer de hello pour Jeff Smith est toujours récupérée, mais il est ensuite enregistrée serveur toohello arrière via **table_operation::insert_or_replace_entity**.</span><span class="sxs-lookup"><span data-stu-id="381db-188">In hello following code example, hello customer entity for Jeff Smith is still retrieved, but it is then saved back toohello server via **table_operation::insert_or_replace_entity**.</span></span> <span data-ttu-id="381db-189">Les mises à jour apportées entité toohello entre une opération de mise à jour et de récupération hello seront remplacées.</span><span class="sxs-lookup"><span data-stu-id="381db-189">Any updates made toohello entity between hello retrieval and update operation will be overwritten.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Insert-or-replace an entity.
azure::storage::table_entity entity_to_insert_or_replace(U("Smith"), U("Jeff"));
azure::storage::table_entity::properties_type& properties_to_insert_or_replace = entity_to_insert_or_replace.properties();

properties_to_insert_or_replace.reserve(2);

// Specify a phone number.
properties_to_insert_or_replace[U("Phone")] = azure::storage::entity_property(U("425-555-0107"));

// Specify an email address.
properties_to_insert_or_replace[U("Email")] = azure::storage::entity_property(U("Jeffsm@contoso.com"));

// Create an operation tooinsert-or-replace hello entity.
azure::storage::table_operation insert_or_replace_operation = azure::storage::table_operation::insert_or_replace_entity(entity_to_insert_or_replace);

// Submit hello operation toohello Table service.
azure::storage::table_result insert_or_replace_result = table.execute(insert_or_replace_operation);
```

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="381db-190">Interrogation d’un sous-ensemble de propriétés d’entité</span><span class="sxs-lookup"><span data-stu-id="381db-190">Query a subset of entity properties</span></span>
<span data-ttu-id="381db-191">Une table de tooa de requête peut récupérer des propriétés peu d’une entité.</span><span class="sxs-lookup"><span data-stu-id="381db-191">A query tooa table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="381db-192">requête de hello suivant code Hello utilise hello **table_query::set_select_columns** méthode tooreturn uniquement hello adresses de messagerie des entités de table de hello.</span><span class="sxs-lookup"><span data-stu-id="381db-192">hello query in hello following code uses hello **table_query::set_select_columns** method tooreturn only hello email addresses of entities in hello table.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Define hello query, and select only hello Email property.
azure::storage::table_query query;
std::vector<utility::string_t> columns;

columns.push_back(U("Email"));
query.set_select_columns(columns);

// Execute hello query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Display hello results.
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
> <span data-ttu-id="381db-193">L’interrogation d’un petit nombre de propriétés d’une entité est une opération plus efficace que l’extraction de toutes les propriétés.</span><span class="sxs-lookup"><span data-stu-id="381db-193">Querying a few properties from an entity is a more efficient operation than retrieving all properties.</span></span>
> 
> 

## <a name="delete-an-entity"></a><span data-ttu-id="381db-194">Suppression d’une entité</span><span class="sxs-lookup"><span data-stu-id="381db-194">Delete an entity</span></span>
<span data-ttu-id="381db-195">Il est facile de supprimer une entité après l’avoir récupérée.</span><span class="sxs-lookup"><span data-stu-id="381db-195">You can easily delete an entity after you have retrieved it.</span></span> <span data-ttu-id="381db-196">Une fois que l’entité de hello est récupérée, appelez **table_operation::delete_entity** avec toodelete d’entité hello.</span><span class="sxs-lookup"><span data-stu-id="381db-196">Once hello entity is retrieved, call **table_operation::delete_entity** with hello entity toodelete.</span></span> <span data-ttu-id="381db-197">Appelez ensuite hello **cloud_table.execute** (méthode).</span><span class="sxs-lookup"><span data-stu-id="381db-197">Then call hello **cloud_table.execute** method.</span></span> <span data-ttu-id="381db-198">Bonjour de code suivant récupère et supprime une entité avec une clé de partition « Smith » et une clé de ligne de « Jeff ».</span><span class="sxs-lookup"><span data-stu-id="381db-198">hello following code retrieves and deletes an entity with a partition key of "Smith" and a row key of "Jeff".</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create an operation tooretrieve hello entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Create an operation toodelete hello entity.
azure::storage::table_operation delete_operation = azure::storage::table_operation::delete_entity(retrieve_result.entity());

// Submit hello delete operation toohello Table service.
azure::storage::table_result delete_result = table.execute(delete_operation);  
```

## <a name="delete-a-table"></a><span data-ttu-id="381db-199">Suppression d’une table</span><span class="sxs-lookup"><span data-stu-id="381db-199">Delete a table</span></span>
<span data-ttu-id="381db-200">Enfin, hello, exemple de code suivant supprime une table à partir d’un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="381db-200">Finally, hello following code example deletes a table from a storage account.</span></span> <span data-ttu-id="381db-201">Une table qui a été supprimée sera indisponible toobe recréée pour une période de temps après la suppression de hello.</span><span class="sxs-lookup"><span data-stu-id="381db-201">A table that has been deleted will be unavailable toobe re-created for a period of time following hello deletion.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create an operation tooretrieve hello entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Create an operation toodelete hello entity.
azure::storage::table_operation delete_operation = azure::storage::table_operation::delete_entity(retrieve_result.entity());

// Submit hello delete operation toohello Table service.
azure::storage::table_result delete_result = table.execute(delete_operation);
```

## <a name="next-steps"></a><span data-ttu-id="381db-202">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="381db-202">Next steps</span></span>
<span data-ttu-id="381db-203">Maintenant que vous avez appris les notions de base de hello du stockage table, suivez ces liens de toolearn plus d’informations sur le stockage Azure :</span><span class="sxs-lookup"><span data-stu-id="381db-203">Now that you've learned hello basics of table storage, follow these links toolearn more about Azure Storage:</span></span>  

* <span data-ttu-id="381db-204">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) est une application autonome gratuit, à partir de Microsoft qui vous permet de toowork visuellement avec des données de stockage Azure sur Windows, Mac OS et Linux.</span><span class="sxs-lookup"><span data-stu-id="381db-204">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* [<span data-ttu-id="381db-205">Comment toouse stockage d’objets Blob à partir de C++</span><span class="sxs-lookup"><span data-stu-id="381db-205">How toouse Blob storage from C++</span></span>](storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="381db-206">Comment toouse stockage de file d’attente à partir de C++</span><span class="sxs-lookup"><span data-stu-id="381db-206">How toouse Queue storage from C++</span></span>](storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="381db-207">Listage des ressources Azure Storage en C++</span><span class="sxs-lookup"><span data-stu-id="381db-207">List Azure Storage resources in C++</span></span>](storage-c-plus-plus-enumeration.md)
* [<span data-ttu-id="381db-208">Référence de la bibliothèque cliente de stockage pour C++</span><span class="sxs-lookup"><span data-stu-id="381db-208">Storage Client Library for C++ reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="381db-209">Documentation d’Azure Storage</span><span class="sxs-lookup"><span data-stu-id="381db-209">Azure Storage documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
