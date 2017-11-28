---
title: "aaaHow toouse le stockage de Table à partir de Java | Documents Microsoft"
description: "Stocker des données structurées dans le cloud hello avec le stockage Table Azure, un magasin de données NoSQL."
services: storage
documentationcenter: java
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 45145189-e67f-4ca6-b15d-43af7bfd3f97
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: f72cac3fc10cf0aef74780b84c515d93d715d787
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-from-java"></a><span data-ttu-id="3811d-103">Comment toouse le stockage de Table à partir de Java</span><span class="sxs-lookup"><span data-stu-id="3811d-103">How toouse Table storage from Java</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="3811d-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="3811d-104">Overview</span></span>
<span data-ttu-id="3811d-105">Ce guide vous explique comment tooperform des scénarios courants utilisant hello service de stockage de Table Azure.</span><span class="sxs-lookup"><span data-stu-id="3811d-105">This guide will show you how tooperform common scenarios using hello Azure Table storage service.</span></span> <span data-ttu-id="3811d-106">exemples de Hello sont écrits en Java et utiliser hello [SDK de stockage Azure pour Java][Azure Storage SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="3811d-106">hello samples are written in Java and use hello [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="3811d-107">Hello scénarios abordés incluent **création**, **liste**, et **suppression** tables, ainsi que **insertion**,  **interrogation**, **modification**, et **suppression** entités dans une table.</span><span class="sxs-lookup"><span data-stu-id="3811d-107">hello scenarios covered include **creating**, **listing**, and **deleting** tables, as well as **inserting**, **querying**, **modifying**, and **deleting** entities in a table.</span></span> <span data-ttu-id="3811d-108">Pour plus d’informations sur les tables, consultez hello [étapes](#Next-Steps) section.</span><span class="sxs-lookup"><span data-stu-id="3811d-108">For more information on tables, see hello [Next steps](#Next-Steps) section.</span></span>

<span data-ttu-id="3811d-109">Remarque : un Kit de développement logiciel (SDK) est disponible pour les développeurs qui utilisent Azure Storage sur des appareils Android.</span><span class="sxs-lookup"><span data-stu-id="3811d-109">Note: An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="3811d-110">Pour plus d’informations, consultez hello [stockage de Azure SDK pour Android][Azure Storage SDK for Android].</span><span class="sxs-lookup"><span data-stu-id="3811d-110">For more information, see hello [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="3811d-111">Création d’une application Java</span><span class="sxs-lookup"><span data-stu-id="3811d-111">Create a Java application</span></span>
<span data-ttu-id="3811d-112">Dans ce guide, vous allez utiliser des fonctionnalités de stockage qui peuvent être exécutées dans une application Java en local, ou dans le code s'exécutant dans un rôle Web ou un rôle de travail dans Azure.</span><span class="sxs-lookup"><span data-stu-id="3811d-112">In this guide, you will use storage features which can be run within a Java application locally, or in code running within a web role or worker role in Azure.</span></span>

<span data-ttu-id="3811d-113">toodo par conséquent, vous devez tooinstall hello du Kit de développement Java (JDK) et créer un compte de stockage Azure dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="3811d-113">toodo so, you will need tooinstall hello Java Development Kit (JDK) and create an Azure storage account in your Azure subscription.</span></span> <span data-ttu-id="3811d-114">Une fois que vous l’avez fait, vous devez tooverify votre système de développement répond aux exigences minimales de hello et les dépendances qui sont répertoriées dans hello [SDK de stockage Azure pour Java] [ Azure Storage SDK for Java] référentiel sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="3811d-114">Once you have done so, you will need tooverify that your development system meets hello minimum requirements and dependencies which are listed in hello [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="3811d-115">Si votre système répond à ces exigences, vous pouvez suivre les instructions de hello pour télécharger et installer les bibliothèques de stockage Azure hello pour Java sur votre système à partir de ce référentiel.</span><span class="sxs-lookup"><span data-stu-id="3811d-115">If your system meets those requirements, you can follow hello instructions for downloading and installing hello Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="3811d-116">Une fois ces tâches terminées, vous serez en mesure de toocreate une application Java qui utilise des exemples de hello dans cet article.</span><span class="sxs-lookup"><span data-stu-id="3811d-116">Once you have completed those tasks, you will be able toocreate a Java application which uses hello examples in this article.</span></span>

## <a name="configure-your-application-tooaccess-table-storage"></a><span data-ttu-id="3811d-117">Configurer le stockage de table tooaccess application</span><span class="sxs-lookup"><span data-stu-id="3811d-117">Configure your application tooaccess table storage</span></span>
<span data-ttu-id="3811d-118">Ajoutez hello après importation instructions toohello en haut de hello Java fichier dans lequel les tables tooaccess API toouse Microsoft Azure storage :</span><span class="sxs-lookup"><span data-stu-id="3811d-118">Add hello following import statements toohello top of hello Java file where you want toouse Microsoft Azure storage APIs tooaccess tables:</span></span>

```java
// Include hello following imports toouse table APIs
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.table.*;
import com.microsoft.azure.storage.table.TableQuery.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="3811d-119">Configuration d’une chaîne de connexion au stockage Azure</span><span class="sxs-lookup"><span data-stu-id="3811d-119">Set up an Azure storage connection string</span></span>
<span data-ttu-id="3811d-120">Un client de stockage Azure utilise une terminaison de stockage connexion chaîne toostore et informations d’identification pour accéder aux services de gestion de données.</span><span class="sxs-lookup"><span data-stu-id="3811d-120">An Azure storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="3811d-121">Lors de l’exécution dans une application cliente, vous devez fournir la chaîne de connexion de stockage hello Bonjour suivant le format, à l’aide du nom de hello de votre compte de stockage et clé d’accès primaire pour le compte de stockage hello dans hello de hello [portail Azure](https://portal.azure.com)pour hello *AccountName* et *AccountKey* valeurs.</span><span class="sxs-lookup"><span data-stu-id="3811d-121">When running in a client application, you must provide hello storage connection string in hello following format, using hello name of your storage account and hello Primary access key for hello storage account listed in hello [Azure portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="3811d-122">Cet exemple montre comment vous pouvez déclarer une chaîne de connexion de champ statique toohold hello :</span><span class="sxs-lookup"><span data-stu-id="3811d-122">This example shows how you can declare a static field toohold hello connection string:</span></span>

```java
// Define hello connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

<span data-ttu-id="3811d-123">Dans une application en cours d’exécution au sein d’un rôle dans Microsoft Azure, cette chaîne peut être stockée dans le fichier de configuration de service hello, *ServiceConfiguration.cscfg*et sont accessibles avec un appel toohello  **RoleEnvironment.getConfigurationSettings** (méthode).</span><span class="sxs-lookup"><span data-stu-id="3811d-123">In an application running within a role in Microsoft Azure, this string can be stored in hello service configuration file, *ServiceConfiguration.cscfg*, and can be accessed with a call toohello **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="3811d-124">Voici un exemple de mise en route de la chaîne de connexion hello un **paramètre** élément nommé *StorageConnectionString* dans le fichier de configuration de service hello :</span><span class="sxs-lookup"><span data-stu-id="3811d-124">Here's an example of getting hello connection string from a **Setting** element named *StorageConnectionString* in hello service configuration file:</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="3811d-125">Hello exemples suivants supposent que vous avez utilisé une de ces chaînes de connexion de stockage de deux méthodes tooget hello.</span><span class="sxs-lookup"><span data-stu-id="3811d-125">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>

## <a name="how-to-create-a-table"></a><span data-ttu-id="3811d-126">Création d'une table</span><span class="sxs-lookup"><span data-stu-id="3811d-126">How to: Create a table</span></span>
<span data-ttu-id="3811d-127">Un objet **CloudTableClient** vous permet d'obtenir les objets de référence pour les tables et entités.</span><span class="sxs-lookup"><span data-stu-id="3811d-127">A **CloudTableClient** object lets you get reference objects for tables and entities.</span></span> <span data-ttu-id="3811d-128">Hello de code suivant crée un **CloudTableClient** de l’objet et l’utilise toocreate un nouveau **CloudTable** objet qui représente une table nommée « utilisateurs ».</span><span class="sxs-lookup"><span data-stu-id="3811d-128">hello following code creates a **CloudTableClient** object and uses it toocreate a new **CloudTable** object which represents a table named "people".</span></span> <span data-ttu-id="3811d-129">(Remarque : il existe des méthodes supplémentaires toocreate **CloudStorageAccount** objets ; pour plus d’informations, consultez **CloudStorageAccount** Bonjour [référence SDK cliente de stockage Azure].)</span><span class="sxs-lookup"><span data-stu-id="3811d-129">(Note: There are additional ways toocreate **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in hello [Azure Storage Client SDK Reference].)</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create hello table if it doesn't exist.
    String tableName = "people";
    CloudTable cloudTable = tableClient.getTableReference(tableName);
    cloudTable.createIfNotExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-list-hello-tables"></a><span data-ttu-id="3811d-130">Comment : répertorier les tables hello</span><span class="sxs-lookup"><span data-stu-id="3811d-130">How to: List hello tables</span></span>
<span data-ttu-id="3811d-131">tooget une liste de tables, appel hello **CloudTableClient.listTables()** méthode tooretrieve une liste pouvant être itérable des noms de table.</span><span class="sxs-lookup"><span data-stu-id="3811d-131">tooget a list of tables, call hello **CloudTableClient.listTables()** method tooretrieve an iterable list of table names.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Loop through hello collection of table names.
    for (String table : tableClient.listTables())
    {
        // Output each table name.
        System.out.println(table);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-add-an-entity-tooa-table"></a><span data-ttu-id="3811d-132">Comment : ajouter une table de tooa d’entité</span><span class="sxs-lookup"><span data-stu-id="3811d-132">How to: Add an entity tooa table</span></span>
<span data-ttu-id="3811d-133">Mappent des entités tooJava les objets à l’aide d’une classe personnalisée qui implémente **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="3811d-133">Entities map tooJava objects using a custom class implementing **TableEntity**.</span></span> <span data-ttu-id="3811d-134">Pour plus de commodité, hello **TableServiceEntity** la classe implémente **TableEntity** et utilise les méthodes toogetter et l’accesseur Set est nommés pour les propriétés toomap réflexion hello propriétés.</span><span class="sxs-lookup"><span data-stu-id="3811d-134">For convenience, hello **TableServiceEntity** class implements **TableEntity** and uses reflection toomap properties toogetter and setter methods named for hello properties.</span></span> <span data-ttu-id="3811d-135">tooadd une table de tooa entité, créez tout d’abord une classe qui définit les propriétés hello de votre entité.</span><span class="sxs-lookup"><span data-stu-id="3811d-135">tooadd an entity tooa table, first create a class that defines hello properties of your entity.</span></span> <span data-ttu-id="3811d-136">Hello de code suivant définit une classe d’entité qui utilise le prénom du client hello en tant que clé de ligne hello et nom de famille en tant que clé de partition hello.</span><span class="sxs-lookup"><span data-stu-id="3811d-136">hello following code defines an entity class which uses hello customer's first name as hello row key, and last name as hello partition key.</span></span> <span data-ttu-id="3811d-137">Ensemble, les partitions d’une entité et la clé de ligne identifient hello entité dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="3811d-137">Together, an entity's partition and row key uniquely identify hello entity in hello table.</span></span> <span data-ttu-id="3811d-138">Entités avec la même clé de partition peut être interrogé plus rapidement que ceux avec différentes clés de partition de hello.</span><span class="sxs-lookup"><span data-stu-id="3811d-138">Entities with hello same partition key can be queried faster than those with different partition keys.</span></span>

```java
public class CustomerEntity extends TableServiceEntity {
    public CustomerEntity(String lastName, String firstName) {
        this.partitionKey = lastName;
        this.rowKey = firstName;
    }

    public CustomerEntity() { }

    String email;
    String phoneNumber;

    public String getEmail() {
        return this.email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public String getPhoneNumber() {
        return this.phoneNumber;
    }

    public void setPhoneNumber(String phoneNumber) {
        this.phoneNumber = phoneNumber;
    }
}
```

<span data-ttu-id="3811d-139">Les opérations de table impliquant des entités ont besoin d'un objet **TableOperation** .</span><span class="sxs-lookup"><span data-stu-id="3811d-139">Table operations involving entities require a **TableOperation** object.</span></span> <span data-ttu-id="3811d-140">Cet objet définit hello opération toobe est effectuée sur une entité, qui peut être exécutée avec un **CloudTable** objet.</span><span class="sxs-lookup"><span data-stu-id="3811d-140">This object defines hello operation toobe performed on an entity, which can be executed with a **CloudTable** object.</span></span> <span data-ttu-id="3811d-141">Hello de code suivant crée une nouvelle instance de hello **CustomerEntity** classe avec certains toobe de données client stockée.</span><span class="sxs-lookup"><span data-stu-id="3811d-141">hello following code creates a new instance of hello **CustomerEntity** class with some customer data toobe stored.</span></span> <span data-ttu-id="3811d-142">Hello de code suivante appelle **TableOperation.insertOrReplace** toocreate un **TableOperation** tooinsert une entité de l’objet dans une table, et associe hello new **CustomerEntity**avec lui.</span><span class="sxs-lookup"><span data-stu-id="3811d-142">hello code next calls **TableOperation.insertOrReplace** toocreate a **TableOperation** object tooinsert an entity into a table, and associates hello new **CustomerEntity** with it.</span></span> <span data-ttu-id="3811d-143">Enfin, le code de hello appelle hello **exécuter** méthode sur hello **CloudTable** objet, en spécifiant la table « people » de hello et hello nouvelle **TableOperation**, qui envoie ensuite un toohello stockage service tooinsert hello nouveau client entité de la requête dans la table « people » de hello ou remplacez l’entité de hello s’il existe déjà.</span><span class="sxs-lookup"><span data-stu-id="3811d-143">Finally, hello code calls hello **execute** method on hello **CloudTable** object, specifying hello "people" table and hello new **TableOperation**, which then sends a request toohello storage service tooinsert hello new customer entity into hello "people" table, or replace hello entity if it already exists.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.setEmail("Walter@contoso.com");
    customer1.setPhoneNumber("425-555-0101");

    // Create an operation tooadd hello new customer toohello people table.
    TableOperation insertCustomer1 = TableOperation.insertOrReplace(customer1);

    // Submit hello operation toohello table service.
    cloudTable.execute(insertCustomer1);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-insert-a-batch-of-entities"></a><span data-ttu-id="3811d-144">Insertion d’un lot d’entités</span><span class="sxs-lookup"><span data-stu-id="3811d-144">How to: Insert a batch of entities</span></span>
<span data-ttu-id="3811d-145">Vous pouvez insérer un lot de service de table toohello entités dans une opération d’écriture.</span><span class="sxs-lookup"><span data-stu-id="3811d-145">You can insert a batch of entities toohello table service in one write operation.</span></span> <span data-ttu-id="3811d-146">Hello de code suivant crée un **TableBatchOperation** de l’objet, puis ajoute trois insérer tooit d’opérations.</span><span class="sxs-lookup"><span data-stu-id="3811d-146">hello following code creates a **TableBatchOperation** object, then adds three insert operations tooit.</span></span> <span data-ttu-id="3811d-147">Chaque opération d’insertion est ajoutée en créant un nouvel objet d’entité, la définition de ses valeurs et puis appelant hello **insérer** méthode sur hello **TableBatchOperation** de l’objet entité de hello tooassociate avec un nouveau opération d’insertion.</span><span class="sxs-lookup"><span data-stu-id="3811d-147">Each insert operation is added by creating a new entity object, setting its values, and then calling hello **insert** method on hello **TableBatchOperation** object tooassociate hello entity with a new insert operation.</span></span> <span data-ttu-id="3811d-148">Puis hello code appelle **exécuter** sur hello **CloudTable** objet, en spécifiant la table « people » de hello et hello **TableBatchOperation** objet, qui envoie le lot hello de table service de stockage Operations toohello dans une demande unique.</span><span class="sxs-lookup"><span data-stu-id="3811d-148">Then hello code calls **execute** on hello **CloudTable** object, specifying hello "people" table and hello **TableBatchOperation** object, which sends hello batch of table operations toohello storage service in a single request.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Define a batch operation.
    TableBatchOperation batchOperation = new TableBatchOperation();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a customer entity tooadd toohello table.
    CustomerEntity customer = new CustomerEntity("Smith", "Jeff");
    customer.setEmail("Jeff@contoso.com");
    customer.setPhoneNumber("425-555-0104");
    batchOperation.insertOrReplace(customer);

    // Create another customer entity tooadd toohello table.
    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.setEmail("Ben@contoso.com");
    customer2.setPhoneNumber("425-555-0102");
    batchOperation.insertOrReplace(customer2);

    // Create a third customer entity tooadd toohello table.
    CustomerEntity customer3 = new CustomerEntity("Smith", "Denise");
    customer3.setEmail("Denise@contoso.com");
    customer3.setPhoneNumber("425-555-0103");
    batchOperation.insertOrReplace(customer3);

    // Execute hello batch of operations on hello "people" table.
    cloudTable.execute(batchOperation);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

<span data-ttu-id="3811d-149">Toonote de certaines opérations sur les opérations de traitement par lots :</span><span class="sxs-lookup"><span data-stu-id="3811d-149">Some things toonote on batch operations:</span></span>

* <span data-ttu-id="3811d-150">Vous pouvez effectuer des too100 insert, delete, merge, replace, insert ou merge et insérer ou remplacer des opérations dans n’importe quelle combinaison dans un lot unique.</span><span class="sxs-lookup"><span data-stu-id="3811d-150">You can perform up too100 insert, delete, merge, replace, insert or merge, and insert or replace operations in any combination in a single batch.</span></span>
* <span data-ttu-id="3811d-151">Une opération de traitement peut avoir une opération de récupération, s’il est la seule opération de hello dans un lot de hello.</span><span class="sxs-lookup"><span data-stu-id="3811d-151">A batch operation can have a retrieve operation, if it is hello only operation in hello batch.</span></span>
* <span data-ttu-id="3811d-152">Toutes les entités dans une seule opération doivent avoir hello même clé de partition.</span><span class="sxs-lookup"><span data-stu-id="3811d-152">All entities in a single batch operation must have hello same partition key.</span></span>
* <span data-ttu-id="3811d-153">Une opération de traitement est la charge utile de données limité tooa 4 Mo.</span><span class="sxs-lookup"><span data-stu-id="3811d-153">A batch operation is limited tooa 4MB data payload.</span></span>

## <a name="how-to-retrieve-all-entities-in-a-partition"></a><span data-ttu-id="3811d-154">Extraction de toutes les entités dans une partition</span><span class="sxs-lookup"><span data-stu-id="3811d-154">How to: Retrieve all entities in a partition</span></span>
<span data-ttu-id="3811d-155">tooquery une table pour les entités dans une partition, vous pouvez utiliser un **TableQuery**.</span><span class="sxs-lookup"><span data-stu-id="3811d-155">tooquery a table for entities in a partition, you can use a **TableQuery**.</span></span> <span data-ttu-id="3811d-156">Appelez **TableQuery.from** toocreate une requête sur une table particulière qui retourne un type de résultat spécifié.</span><span class="sxs-lookup"><span data-stu-id="3811d-156">Call **TableQuery.from** toocreate a query on a particular table that returns a specified result type.</span></span> <span data-ttu-id="3811d-157">Hello de code suivant spécifie un filtre pour les entités où « Smith » est la clé de partition hello.</span><span class="sxs-lookup"><span data-stu-id="3811d-157">hello following code specifies a filter for entities where 'Smith' is hello partition key.</span></span> <span data-ttu-id="3811d-158">**TableQuery.generateFilterCondition** est une méthode d’assistance toocreate des filtres pour les requêtes.</span><span class="sxs-lookup"><span data-stu-id="3811d-158">**TableQuery.generateFilterCondition** is a helper method toocreate filters for queries.</span></span> <span data-ttu-id="3811d-159">Appelez **où** sur référence hello retourné par hello **TableQuery.from** toohello requête de méthode tooapply hello filtre.</span><span class="sxs-lookup"><span data-stu-id="3811d-159">Call **where** on hello reference returned by hello **TableQuery.from** method tooapply hello filter toohello query.</span></span> <span data-ttu-id="3811d-160">Lorsque les requêtes hello sont exécutée par un appel trop**exécuter** sur hello **CloudTable** de l’objet, il retourne un **itérateur** avec hello **CustomerEntity**résultat de type spécifié.</span><span class="sxs-lookup"><span data-stu-id="3811d-160">When hello query is executed with a call too**execute** on hello **CloudTable** object, it returns an **Iterator** with hello **CustomerEntity** result type specified.</span></span> <span data-ttu-id="3811d-161">Vous pouvez ensuite utiliser hello **itérateur** retournées dans un pour chaque boucle tooconsume hello obtenir les résultats.</span><span class="sxs-lookup"><span data-stu-id="3811d-161">You can then use hello **Iterator** returned in a for each loop tooconsume hello results.</span></span> <span data-ttu-id="3811d-162">Ce code imprime les champs de chaque entité dans la console de toohello de résultats de requête hello hello.</span><span class="sxs-lookup"><span data-stu-id="3811d-162">This code prints hello fields of each entity in hello query results toohello console.</span></span>

```java
try
{
    // Define constants for filters.
    final String PARTITION_KEY = "PartitionKey";
    final String ROW_KEY = "RowKey";
    final String TIMESTAMP = "Timestamp";

    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a filter condition where hello partition key is "Smith".
    String partitionFilter = TableQuery.generateFilterCondition(
        PARTITION_KEY,
        QueryComparisons.EQUAL,
        "Smith");

    // Specify a partition query, using "Smith" as hello partition key filter.
    TableQuery<CustomerEntity> partitionQuery =
        TableQuery.from(CustomerEntity.class)
        .where(partitionFilter);

    // Loop through hello results, displaying information about hello entity.
    for (CustomerEntity entity : cloudTable.execute(partitionQuery)) {
        System.out.println(entity.getPartitionKey() +
            " " + entity.getRowKey() +
            "\t" + entity.getEmail() +
            "\t" + entity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="3811d-163">Récupération d’un ensemble d’entités dans une partition</span><span class="sxs-lookup"><span data-stu-id="3811d-163">How to: Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="3811d-164">Si vous ne souhaitez pas tooquery toutes les entités hello dans une partition, vous pouvez spécifier une plage à l’aide des opérateurs de comparaison dans un filtre.</span><span class="sxs-lookup"><span data-stu-id="3811d-164">If you don't want tooquery all hello entities in a partition, you can specify a range by using comparison operators in a filter.</span></span> <span data-ttu-id="3811d-165">Hello suivant combine deux filtres tooget toutes les entités dans la partition « Smith » où clé de ligne hello (prénom) commence par une lettre de too'E un code » dans l’alphabet de hello.</span><span class="sxs-lookup"><span data-stu-id="3811d-165">hello following code combines two filters tooget all entities in partition "Smith" where hello row key (first name) starts with a letter up too'E' in hello alphabet.</span></span> <span data-ttu-id="3811d-166">Il imprime ensuite les résultats de la requête hello.</span><span class="sxs-lookup"><span data-stu-id="3811d-166">Then it prints hello query results.</span></span> <span data-ttu-id="3811d-167">Si vous utilisez la table de toohello ajouté hello entités dans le traitement par lots hello insérer la section de ce guide, seulement deux entités sont retournées à ce stade (Ben et Denise Smith) ; Jeff Smith n’est pas inclus.</span><span class="sxs-lookup"><span data-stu-id="3811d-167">If you use hello entities added toohello table in hello batch insert section of this guide, only two entities are returned this time (Ben and Denise Smith); Jeff Smith is not included.</span></span>

```java
try
{
    // Define constants for filters.
    final String PARTITION_KEY = "PartitionKey";
    final String ROW_KEY = "RowKey";
    final String TIMESTAMP = "Timestamp";

    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a filter condition where hello partition key is "Smith".
    String partitionFilter = TableQuery.generateFilterCondition(
        PARTITION_KEY,
        QueryComparisons.EQUAL,
        "Smith");

    // Create a filter condition where hello row key is less than hello letter "E".
    String rowFilter = TableQuery.generateFilterCondition(
        ROW_KEY,
        QueryComparisons.LESS_THAN,
        "E");

    // Combine hello two conditions into a filter expression.
    String combinedFilter = TableQuery.combineFilters(partitionFilter,
        Operators.AND, rowFilter);

    // Specify a range query, using "Smith" as hello partition key,
    // with hello row key being up toohello letter "E".
    TableQuery<CustomerEntity> rangeQuery =
        TableQuery.from(CustomerEntity.class)
        .where(combinedFilter);

    // Loop through hello results, displaying information about hello entity
    for (CustomerEntity entity : cloudTable.execute(rangeQuery)) {
        System.out.println(entity.getPartitionKey() +
            " " + entity.getRowKey() +
            "\t" + entity.getEmail() +
            "\t" + entity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-retrieve-a-single-entity"></a><span data-ttu-id="3811d-168">Extraction d'une seule entité</span><span class="sxs-lookup"><span data-stu-id="3811d-168">How to: Retrieve a single entity</span></span>
<span data-ttu-id="3811d-169">Vous pouvez écrire une requête tooretrieve une entité unique et spécifique.</span><span class="sxs-lookup"><span data-stu-id="3811d-169">You can write a query tooretrieve a single, specific entity.</span></span> <span data-ttu-id="3811d-170">code Hello suivant appelle **TableOperation.retrieve** avec partition clé et la ligne de paramètres de clé toospecify hello client « Jeff Smith », au lieu de créer un **TableQuery** et à l’aide de hello toodo de filtres même chose.</span><span class="sxs-lookup"><span data-stu-id="3811d-170">hello following code calls **TableOperation.retrieve** with partition key and row key parameters toospecify hello customer "Jeff Smith", instead of creating a **TableQuery** and using filters toodo hello same thing.</span></span> <span data-ttu-id="3811d-171">Lors de l’exécution, hello récupérer opération retourne seule entité, plutôt qu’une collection.</span><span class="sxs-lookup"><span data-stu-id="3811d-171">When executed, hello retrieve operation returns just one entity, rather than a collection.</span></span> <span data-ttu-id="3811d-172">Hello **getResultAsType** effectue un cast de la méthode hello résultat toohello de type de cible d’affectation hello, un **CustomerEntity** objet.</span><span class="sxs-lookup"><span data-stu-id="3811d-172">hello **getResultAsType** method casts hello result toohello type of hello assignment target, a **CustomerEntity** object.</span></span> <span data-ttu-id="3811d-173">Si ce type n’est pas compatible avec le type hello spécifié pour la requête de hello, une exception est levée.</span><span class="sxs-lookup"><span data-stu-id="3811d-173">If this type is not compatible with hello type specified for hello query, an exception will be thrown.</span></span> <span data-ttu-id="3811d-174">La valeur null est renvoyée si aucune entité n'a de correspondance exacte avec la clé de partition et de ligne.</span><span class="sxs-lookup"><span data-stu-id="3811d-174">A null value is returned if no entity has an exact partition and row key match.</span></span> <span data-ttu-id="3811d-175">Spécification des clés de partition et de ligne dans une requête est tooretrieve de manière plus rapide hello une seule entité hello service de Table.</span><span class="sxs-lookup"><span data-stu-id="3811d-175">Specifying both partition and row keys in a query is hello fastest way tooretrieve a single entity from hello Table service.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Retrieve hello entity with partition key of "Smith" and row key of "Jeff"
    TableOperation retrieveSmithJeff =
        TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Submit hello operation toohello table service and get hello specific entity.
    CustomerEntity specificEntity =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Output hello entity.
    if (specificEntity != null)
    {
        System.out.println(specificEntity.getPartitionKey() +
            " " + specificEntity.getRowKey() +
            "\t" + specificEntity.getEmail() +
            "\t" + specificEntity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-modify-an-entity"></a><span data-ttu-id="3811d-176">Procédure : Modification d’une entité</span><span class="sxs-lookup"><span data-stu-id="3811d-176">How to: Modify an entity</span></span>
<span data-ttu-id="3811d-177">toomodify une entité, récupérer à partir du service de table hello, vérifiez l’objet d’entité toohello modifications et enregistrer hello service de table de retour toohello avec une opération de remplacement ou de fusion.</span><span class="sxs-lookup"><span data-stu-id="3811d-177">toomodify an entity, retrieve it from hello table service, make changes toohello entity object, and save hello changes back toohello table service with a replace or merge operation.</span></span> <span data-ttu-id="3811d-178">Hello code suivant modifie un numéro de téléphone existant.</span><span class="sxs-lookup"><span data-stu-id="3811d-178">hello following code changes an existing customer's phone number.</span></span> <span data-ttu-id="3811d-179">Au lieu d’appeler **TableOperation.insert** comme nous l’avons fait tooinsert, ce code appelle **TableOperation.replace**.</span><span class="sxs-lookup"><span data-stu-id="3811d-179">Instead of calling **TableOperation.insert** like we did tooinsert, this code calls **TableOperation.replace**.</span></span> <span data-ttu-id="3811d-180">Hello **CloudTable.execute** méthode appelle le service de table hello et l’entité de hello est remplacée, sauf si une autre application le modifié dans le temps de hello étant donné que cette application extrait.</span><span class="sxs-lookup"><span data-stu-id="3811d-180">hello **CloudTable.execute** method calls hello table service, and hello entity is replaced, unless another application changed it in hello time since this application retrieved it.</span></span> <span data-ttu-id="3811d-181">Lorsque cela se produit, une exception est levée, et les entités hello doivent être récupérées, modifiée et enregistrée une nouvelle fois.</span><span class="sxs-lookup"><span data-stu-id="3811d-181">When that happens, an exception is thrown, and hello entity must be retrieved, modified, and saved again.</span></span> <span data-ttu-id="3811d-182">Ce modèle de nouvelle tentative d'accès concurrentiel optimiste est courant dans un système de stockage distribué.</span><span class="sxs-lookup"><span data-stu-id="3811d-182">This optimistic concurrency retry pattern is common in a distributed storage system.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Retrieve hello entity with partition key of "Smith" and row key of "Jeff".
    TableOperation retrieveSmithJeff =
        TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Submit hello operation toohello table service and get hello specific entity.
    CustomerEntity specificEntity =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Specify a new phone number.
    specificEntity.setPhoneNumber("425-555-0105");

    // Create an operation tooreplace hello entity.
    TableOperation replaceEntity = TableOperation.replace(specificEntity);

    // Submit hello operation toohello table service.
    cloudTable.execute(replaceEntity);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-query-a-subset-of-entity-properties"></a><span data-ttu-id="3811d-183">Envoi d’une requête de sous-ensemble de propriétés d’entité</span><span class="sxs-lookup"><span data-stu-id="3811d-183">How to: Query a subset of entity properties</span></span>
<span data-ttu-id="3811d-184">Une table de tooa de requête peut récupérer des propriétés peu d’une entité.</span><span class="sxs-lookup"><span data-stu-id="3811d-184">A query tooa table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="3811d-185">Cette technique, nommée « projection », réduit la consommation de bande passante et peut améliorer les performances des requêtes, notamment pour les entités volumineuses.</span><span class="sxs-lookup"><span data-stu-id="3811d-185">This technique, called projection, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="3811d-186">requête de hello suivant code Hello utilise hello **sélectionnez** méthode tooreturn uniquement hello adresses de messagerie des entités de table de hello.</span><span class="sxs-lookup"><span data-stu-id="3811d-186">hello query in hello following code uses hello **select** method tooreturn only hello email addresses of entities in hello table.</span></span> <span data-ttu-id="3811d-187">Hello résultats sont projetés dans une collection de **chaîne** à l’aide de hello d’un **EntityResolver**, qui hello de conversion de type sur les entités hello retourné à partir du serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="3811d-187">hello results are projected into a collection of **String** with hello help of an **EntityResolver**, which does hello type conversion on hello entities returned from hello server.</span></span> <span data-ttu-id="3811d-188">Pour plus d’informations sur la projection, consultez la rubrique [Tables Azure : présentation d’Upsert et Query Projection][Azure Tables: Introducing Upsert and Query Projection].</span><span class="sxs-lookup"><span data-stu-id="3811d-188">You can learn more about projection in [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection].</span></span> <span data-ttu-id="3811d-189">Notez que la projection n’est pas pris en charge sur l’émulateur de stockage local hello, pour que ce code s’exécute uniquement lorsque vous utilisez un compte de service de table hello.</span><span class="sxs-lookup"><span data-stu-id="3811d-189">Note that projection is not supported on hello local storage emulator, so this code runs only when using an account on hello table service.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Define a projection query that retrieves only hello Email property
    TableQuery<CustomerEntity> projectionQuery =
        TableQuery.from(CustomerEntity.class)
        .select(new String[] {"Email"});

    // Define a Entity resolver tooproject hello entity toohello Email value.
    EntityResolver<String> emailResolver = new EntityResolver<String>() {
        @Override
        public String resolve(String PartitionKey, String RowKey, Date timeStamp, HashMap<String, EntityProperty> properties, String etag) {
            return properties.get("Email").getValueAsString();
        }
    };

    // Loop through hello results, displaying hello Email values.
    for (String projectedString :
        cloudTable.execute(projectionQuery, emailResolver)) {
            System.out.println(projectedString);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-insert-or-replace-an-entity"></a><span data-ttu-id="3811d-190">Procédure : Insertion ou remplacement d’une entité</span><span class="sxs-lookup"><span data-stu-id="3811d-190">How to: Insert or Replace an entity</span></span>
<span data-ttu-id="3811d-191">Vous souhaitez souvent tooadd une table d’entités tooa sans savoir s’il existe déjà dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="3811d-191">Often you want tooadd an entity tooa table without knowing if it already exists in hello table.</span></span> <span data-ttu-id="3811d-192">Une opération d’insertion ou remplacement vous permet de toomake une demande unique qui insère les entités hello si il ou n’existe pas remplacer hello un existant dans ce cas.</span><span class="sxs-lookup"><span data-stu-id="3811d-192">An insert-or-replace operation allows you toomake a single request which will insert hello entity if it does not exist or replace hello existing one if it does.</span></span> <span data-ttu-id="3811d-193">S’appuyant sur des exemples préalables, hello de code suivant insère ou remplace l’entité de hello pour « Walter harpe ».</span><span class="sxs-lookup"><span data-stu-id="3811d-193">Building on prior examples, hello following code inserts or replaces hello entity for "Walter Harp".</span></span> <span data-ttu-id="3811d-194">Après avoir créé une nouvelle entité, ce code appelle hello **TableOperation.insertOrReplace** (méthode).</span><span class="sxs-lookup"><span data-stu-id="3811d-194">After creating a new entity, this code calls hello **TableOperation.insertOrReplace** method.</span></span> <span data-ttu-id="3811d-195">Ce code appelle ensuite **exécuter** sur hello **CloudTable** de l’objet avec insert de table et hello hello ou opération de table en tant que paramètres de hello de remplacement.</span><span class="sxs-lookup"><span data-stu-id="3811d-195">This code then calls **execute** on hello **CloudTable** object with hello table and hello insert or replace table operation as hello parameters.</span></span> <span data-ttu-id="3811d-196">tooupdate uniquement dans le cadre d’une entité, hello **TableOperation.insertOrMerge** méthode peut être utilisée à la place.</span><span class="sxs-lookup"><span data-stu-id="3811d-196">tooupdate only part of an entity, hello **TableOperation.insertOrMerge** method can be used instead.</span></span> <span data-ttu-id="3811d-197">Notez qu’insert-ou-le remplacement n’est pas pris en charge sur l’émulateur de stockage local hello, pour que ce code s’exécute uniquement lorsque vous utilisez un compte de service de table hello.</span><span class="sxs-lookup"><span data-stu-id="3811d-197">Note that insert-or-replace is not supported on hello local storage emulator, so this code runs only when using an account on hello table service.</span></span> <span data-ttu-id="3811d-198">Pour plus d’informations sur l’opération d’insertion ou de remplacement et d’insertion ou de fusion, consultez la rubrique [Tables Azure : présentation d’Upsert et Query Projection][Azure Tables: Introducing Upsert and Query Projection].</span><span class="sxs-lookup"><span data-stu-id="3811d-198">You can learn more about insert-or-replace and insert-or-merge in this [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection].</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a new customer entity.
    CustomerEntity customer5 = new CustomerEntity("Harp", "Walter");
    customer5.setEmail("Walter@contoso.com");
    customer5.setPhoneNumber("425-555-0106");

    // Create an operation tooadd hello new customer toohello people table.
    TableOperation insertCustomer5 = TableOperation.insertOrReplace(customer5);

    // Submit hello operation toohello table service.
    cloudTable.execute(insertCustomer5);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-an-entity"></a><span data-ttu-id="3811d-199">Suppression d'une entité</span><span class="sxs-lookup"><span data-stu-id="3811d-199">How to: Delete an entity</span></span>
<span data-ttu-id="3811d-200">Il est facile de supprimer une entité après l’avoir récupérée.</span><span class="sxs-lookup"><span data-stu-id="3811d-200">You can easily delete an entity after you have retrieved it.</span></span> <span data-ttu-id="3811d-201">Une fois que l’entité de hello est récupérée, appelez **TableOperation.delete** avec toodelete d’entité hello.</span><span class="sxs-lookup"><span data-stu-id="3811d-201">Once hello entity is retrieved, call **TableOperation.delete** with hello entity toodelete.</span></span> <span data-ttu-id="3811d-202">Appelez ensuite **exécuter** sur hello **CloudTable** objet.</span><span class="sxs-lookup"><span data-stu-id="3811d-202">Then call **execute** on hello **CloudTable** object.</span></span> <span data-ttu-id="3811d-203">Hello suivant code récupère et supprime une entité customer.</span><span class="sxs-lookup"><span data-stu-id="3811d-203">hello following code retrieves and deletes a customer entity.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create an operation tooretrieve hello entity with partition key of "Smith" and row key of "Jeff".
    TableOperation retrieveSmithJeff = TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Retrieve hello entity with partition key of "Smith" and row key of "Jeff".
    CustomerEntity entitySmithJeff =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Create an operation toodelete hello entity.
    TableOperation deleteSmithJeff = TableOperation.delete(entitySmithJeff);

    // Submit hello delete operation toohello table service.
    cloudTable.execute(deleteSmithJeff);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-a-table"></a><span data-ttu-id="3811d-204">Suppression d'une table</span><span class="sxs-lookup"><span data-stu-id="3811d-204">How to: Delete a table</span></span>
<span data-ttu-id="3811d-205">Enfin, hello de code suivant supprime une table à partir d’un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="3811d-205">Finally, hello following code deletes a table from a storage account.</span></span> <span data-ttu-id="3811d-206">Une table qui a été supprimée sera indisponible toobe recréé pour une période de temps suivant suppression hello, généralement inférieur à 40 secondes.</span><span class="sxs-lookup"><span data-stu-id="3811d-206">A table which has been deleted will be unavailable toobe recreated for a period of time following hello deletion, usually less than forty seconds.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Delete hello table and all its data if it exists.
    CloudTable cloudTable = tableClient.getTableReference("people");
    cloudTable.deleteIfExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```
[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="next-steps"></a><span data-ttu-id="3811d-207">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3811d-207">Next steps</span></span>

* <span data-ttu-id="3811d-208">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) est une application autonome gratuit, à partir de Microsoft qui vous permet de toowork visuellement avec des données de stockage Azure sur Windows, Mac OS et Linux.</span><span class="sxs-lookup"><span data-stu-id="3811d-208">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="3811d-209">[Kit de développement logiciel (SDK) Azure Storage pour Java][Azure Storage SDK for Java]</span><span class="sxs-lookup"><span data-stu-id="3811d-209">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="3811d-210">[référence SDK cliente de stockage Azure][référence SDK cliente de stockage Azure]</span><span class="sxs-lookup"><span data-stu-id="3811d-210">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="3811d-211">[API REST Stockage Azure][Azure Storage REST API]</span><span class="sxs-lookup"><span data-stu-id="3811d-211">[Azure Storage REST API][Azure Storage REST API]</span></span>
* <span data-ttu-id="3811d-212">[Blog de l’équipe Stockage Azure][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="3811d-212">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

<span data-ttu-id="3811d-213">Pour plus d’informations, consultez également hello [centre de développement Java](/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="3811d-213">For more information, see also hello [Java Developer Center](/develop/java/).</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[référence SDK cliente de stockage Azure]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[Azure Tables: Introducing Upsert and Query Projection]: http://blogs.msdn.com/b/windowsazurestorage/archive/2011/09/15/windows-azure-tables-introducing-upsert-and-query-projection.aspx
