---
title: "aaaHow toouse le stockage de Table à partir de Java | Documents Microsoft"
description: "Stocker des données structurées dans le cloud hello avec le stockage Table Azure, un magasin de données NoSQL."
services: cosmos-db
documentationcenter: java
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: 45145189-e67f-4ca6-b15d-43af7bfd3f97
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: 20d03e867219cc254da8dad37cf3cf61bca65671
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-from-java"></a>Comment toouse le stockage de Table à partir de Java
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>Vue d'ensemble
Ce guide vous explique comment tooperform des scénarios courants utilisant hello service de stockage de Table Azure. exemples de Hello sont écrits en Java et utiliser hello [SDK de stockage Azure pour Java][Azure Storage SDK for Java]. Hello scénarios abordés incluent **création**, **liste**, et **suppression** tables, ainsi que **insertion**,  **interrogation**, **modification**, et **suppression** entités dans une table. Pour plus d’informations sur les tables, consultez hello [étapes](#Next-Steps) section.

Remarque : un Kit de développement logiciel (SDK) est disponible pour les développeurs qui utilisent Azure Storage sur des appareils Android. Pour plus d’informations, consultez hello [stockage de Azure SDK pour Android][Azure Storage SDK for Android].

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a>Création d’une application Java
Dans ce guide, vous allez utiliser des fonctionnalités de stockage qui peuvent être exécutées dans une application Java en local, ou dans le code s'exécutant dans un rôle Web ou un rôle de travail dans Azure.

toodo par conséquent, vous devez tooinstall hello du Kit de développement Java (JDK) et créer un compte de stockage Azure dans votre abonnement Azure. Une fois que vous l’avez fait, vous devez tooverify votre système de développement répond aux exigences minimales de hello et les dépendances qui sont répertoriées dans hello [SDK de stockage Azure pour Java] [ Azure Storage SDK for Java] référentiel sur GitHub. Si votre système répond à ces exigences, vous pouvez suivre les instructions de hello pour télécharger et installer les bibliothèques de stockage Azure hello pour Java sur votre système à partir de ce référentiel. Une fois ces tâches terminées, vous serez en mesure de toocreate une application Java qui utilise des exemples de hello dans cet article.

## <a name="configure-your-application-tooaccess-table-storage"></a>Configurer le stockage de table tooaccess application
Ajoutez hello après importation instructions toohello en haut de hello Java fichier dans lequel les tables tooaccess API toouse Microsoft Azure storage :

```java
// Include hello following imports toouse table APIs
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.table.*;
import com.microsoft.azure.storage.table.TableQuery.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a>Configuration d’une chaîne de connexion au stockage Azure
Un client de stockage Azure utilise une terminaison de stockage connexion chaîne toostore et informations d’identification pour accéder aux services de gestion de données. Lors de l’exécution dans une application cliente, vous devez fournir la chaîne de connexion de stockage hello Bonjour suivant le format, à l’aide du nom de hello de votre compte de stockage et clé d’accès primaire pour le compte de stockage hello dans hello de hello [portail Azure](https://portal.azure.com)pour hello *AccountName* et *AccountKey* valeurs. Cet exemple montre comment vous pouvez déclarer une chaîne de connexion de champ statique toohold hello :

```java
// Define hello connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

Dans une application en cours d’exécution au sein d’un rôle dans Microsoft Azure, cette chaîne peut être stockée dans le fichier de configuration de service hello, *ServiceConfiguration.cscfg*et sont accessibles avec un appel toohello  **RoleEnvironment.getConfigurationSettings** (méthode). Voici un exemple de mise en route de la chaîne de connexion hello un **paramètre** élément nommé *StorageConnectionString* dans le fichier de configuration de service hello :

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

Hello exemples suivants supposent que vous avez utilisé une de ces chaînes de connexion de stockage de deux méthodes tooget hello.

## <a name="how-to-create-a-table"></a>Création d'une table
Un objet **CloudTableClient** vous permet d'obtenir les objets de référence pour les tables et entités. Hello de code suivant crée un **CloudTableClient** de l’objet et l’utilise toocreate un nouveau **CloudTable** objet qui représente une table nommée « utilisateurs ». (Remarque : il existe des méthodes supplémentaires toocreate **CloudStorageAccount** objets ; pour plus d’informations, consultez **CloudStorageAccount** Bonjour [référence SDK cliente de stockage Azure].)

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

## <a name="how-to-list-hello-tables"></a>Comment : répertorier les tables hello
tooget une liste de tables, appel hello **CloudTableClient.listTables()** méthode tooretrieve une liste pouvant être itérable des noms de table.

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

## <a name="how-to-add-an-entity-tooa-table"></a>Comment : ajouter une table de tooa d’entité
Mappent des entités tooJava les objets à l’aide d’une classe personnalisée qui implémente **TableEntity**. Pour plus de commodité, hello **TableServiceEntity** la classe implémente **TableEntity** et utilise les méthodes toogetter et l’accesseur Set est nommés pour les propriétés toomap réflexion hello propriétés. tooadd une table de tooa entité, créez tout d’abord une classe qui définit les propriétés hello de votre entité. Hello de code suivant définit une classe d’entité qui utilise le prénom du client hello en tant que clé de ligne hello et nom de famille en tant que clé de partition hello. Ensemble, les partitions d’une entité et la clé de ligne identifient hello entité dans la table de hello. Entités avec la même clé de partition peut être interrogé plus rapidement que ceux avec différentes clés de partition de hello.

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

Les opérations de table impliquant des entités ont besoin d'un objet **TableOperation** . Cet objet définit hello opération toobe est effectuée sur une entité, qui peut être exécutée avec un **CloudTable** objet. Hello de code suivant crée une nouvelle instance de hello **CustomerEntity** classe avec certains toobe de données client stockée. Hello de code suivante appelle **TableOperation.insertOrReplace** toocreate un **TableOperation** tooinsert une entité de l’objet dans une table, et associe hello new **CustomerEntity**avec lui. Enfin, le code de hello appelle hello **exécuter** méthode sur hello **CloudTable** objet, en spécifiant la table « people » de hello et hello nouvelle **TableOperation**, qui envoie ensuite un toohello stockage service tooinsert hello nouveau client entité de la requête dans la table « people » de hello ou remplacez l’entité de hello s’il existe déjà.

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

## <a name="how-to-insert-a-batch-of-entities"></a>Insertion d’un lot d’entités
Vous pouvez insérer un lot de service de table toohello entités dans une opération d’écriture. Hello de code suivant crée un **TableBatchOperation** de l’objet, puis ajoute trois insérer tooit d’opérations. Chaque opération d’insertion est ajoutée en créant un nouvel objet d’entité, la définition de ses valeurs et puis appelant hello **insérer** méthode sur hello **TableBatchOperation** de l’objet entité de hello tooassociate avec un nouveau opération d’insertion. Puis hello code appelle **exécuter** sur hello **CloudTable** objet, en spécifiant la table « people » de hello et hello **TableBatchOperation** objet, qui envoie le lot hello de table service de stockage Operations toohello dans une demande unique.

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

Toonote de certaines opérations sur les opérations de traitement par lots :

* Vous pouvez effectuer des too100 insert, delete, merge, replace, insert ou merge et insérer ou remplacer des opérations dans n’importe quelle combinaison dans un lot unique.
* Une opération de traitement peut avoir une opération de récupération, s’il est la seule opération de hello dans un lot de hello.
* Toutes les entités dans une seule opération doivent avoir hello même clé de partition.
* Une opération de traitement est la charge utile de données limité tooa 4 Mo.

## <a name="how-to-retrieve-all-entities-in-a-partition"></a>Extraction de toutes les entités dans une partition
tooquery une table pour les entités dans une partition, vous pouvez utiliser un **TableQuery**. Appelez **TableQuery.from** toocreate une requête sur une table particulière qui retourne un type de résultat spécifié. Hello de code suivant spécifie un filtre pour les entités où « Smith » est la clé de partition hello. **TableQuery.generateFilterCondition** est une méthode d’assistance toocreate des filtres pour les requêtes. Appelez **où** sur référence hello retourné par hello **TableQuery.from** toohello requête de méthode tooapply hello filtre. Lorsque les requêtes hello sont exécutée par un appel trop**exécuter** sur hello **CloudTable** de l’objet, il retourne un **itérateur** avec hello **CustomerEntity**résultat de type spécifié. Vous pouvez ensuite utiliser hello **itérateur** retournées dans un pour chaque boucle tooconsume hello obtenir les résultats. Ce code imprime les champs de chaque entité dans la console de toohello de résultats de requête hello hello.

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

## <a name="how-to-retrieve-a-range-of-entities-in-a-partition"></a>Récupération d’un ensemble d’entités dans une partition
Si vous ne souhaitez pas tooquery toutes les entités hello dans une partition, vous pouvez spécifier une plage à l’aide des opérateurs de comparaison dans un filtre. Hello suivant combine deux filtres tooget toutes les entités dans la partition « Smith » où clé de ligne hello (prénom) commence par une lettre de too'E un code » dans l’alphabet de hello. Il imprime ensuite les résultats de la requête hello. Si vous utilisez la table de toohello ajouté hello entités dans le traitement par lots hello insérer la section de ce guide, seulement deux entités sont retournées à ce stade (Ben et Denise Smith) ; Jeff Smith n’est pas inclus.

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

## <a name="how-to-retrieve-a-single-entity"></a>Extraction d'une seule entité
Vous pouvez écrire une requête tooretrieve une entité unique et spécifique. code Hello suivant appelle **TableOperation.retrieve** avec partition clé et la ligne de paramètres de clé toospecify hello client « Jeff Smith », au lieu de créer un **TableQuery** et à l’aide de hello toodo de filtres même chose. Lors de l’exécution, hello récupérer opération retourne seule entité, plutôt qu’une collection. Hello **getResultAsType** effectue un cast de la méthode hello résultat toohello de type de cible d’affectation hello, un **CustomerEntity** objet. Si ce type n’est pas compatible avec le type hello spécifié pour la requête de hello, une exception est levée. La valeur null est renvoyée si aucune entité n'a de correspondance exacte avec la clé de partition et de ligne. Spécification des clés de partition et de ligne dans une requête est tooretrieve de manière plus rapide hello une seule entité hello service de Table.

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

## <a name="how-to-modify-an-entity"></a>Procédure : Modification d’une entité
toomodify une entité, récupérer à partir du service de table hello, vérifiez l’objet d’entité toohello modifications et enregistrer hello service de table de retour toohello avec une opération de remplacement ou de fusion. Hello code suivant modifie un numéro de téléphone existant. Au lieu d’appeler **TableOperation.insert** comme nous l’avons fait tooinsert, ce code appelle **TableOperation.replace**. Hello **CloudTable.execute** méthode appelle le service de table hello et l’entité de hello est remplacée, sauf si une autre application le modifié dans le temps de hello étant donné que cette application extrait. Lorsque cela se produit, une exception est levée, et les entités hello doivent être récupérées, modifiée et enregistrée une nouvelle fois. Ce modèle de nouvelle tentative d'accès concurrentiel optimiste est courant dans un système de stockage distribué.

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

## <a name="how-to-query-a-subset-of-entity-properties"></a>Envoi d’une requête de sous-ensemble de propriétés d’entité
Une table de tooa de requête peut récupérer des propriétés peu d’une entité. Cette technique, nommée « projection », réduit la consommation de bande passante et peut améliorer les performances des requêtes, notamment pour les entités volumineuses. requête de hello suivant code Hello utilise hello **sélectionnez** méthode tooreturn uniquement hello adresses de messagerie des entités de table de hello. Hello résultats sont projetés dans une collection de **chaîne** à l’aide de hello d’un **EntityResolver**, qui hello de conversion de type sur les entités hello retourné à partir du serveur de hello. Pour plus d’informations sur la projection, consultez la rubrique [Tables Azure : présentation d’Upsert et Query Projection][Azure Tables: Introducing Upsert and Query Projection]. Notez que la projection n’est pas pris en charge sur l’émulateur de stockage local hello, pour que ce code s’exécute uniquement lorsque vous utilisez un compte de service de table hello.

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

## <a name="how-to-insert-or-replace-an-entity"></a>Procédure : Insertion ou remplacement d’une entité
Vous souhaitez souvent tooadd une table d’entités tooa sans savoir s’il existe déjà dans la table de hello. Une opération d’insertion ou remplacement vous permet de toomake une demande unique qui insère les entités hello si il ou n’existe pas remplacer hello un existant dans ce cas. S’appuyant sur des exemples préalables, hello de code suivant insère ou remplace l’entité de hello pour « Walter harpe ». Après avoir créé une nouvelle entité, ce code appelle hello **TableOperation.insertOrReplace** (méthode). Ce code appelle ensuite **exécuter** sur hello **CloudTable** de l’objet avec insert de table et hello hello ou opération de table en tant que paramètres de hello de remplacement. tooupdate uniquement dans le cadre d’une entité, hello **TableOperation.insertOrMerge** méthode peut être utilisée à la place. Notez qu’insert-ou-le remplacement n’est pas pris en charge sur l’émulateur de stockage local hello, pour que ce code s’exécute uniquement lorsque vous utilisez un compte de service de table hello. Pour plus d’informations sur l’opération d’insertion ou de remplacement et d’insertion ou de fusion, consultez la rubrique [Tables Azure : présentation d’Upsert et Query Projection][Azure Tables: Introducing Upsert and Query Projection].

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

## <a name="how-to-delete-an-entity"></a>Suppression d'une entité
Il est facile de supprimer une entité après l’avoir récupérée. Une fois que l’entité de hello est récupérée, appelez **TableOperation.delete** avec toodelete d’entité hello. Appelez ensuite **exécuter** sur hello **CloudTable** objet. Hello suivant code récupère et supprime une entité customer.

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

## <a name="how-to-delete-a-table"></a>Suppression d'une table
Enfin, hello de code suivant supprime une table à partir d’un compte de stockage. Une table qui a été supprimée sera indisponible toobe recréé pour une période de temps suivant suppression hello, généralement inférieur à 40 secondes.

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

## <a name="next-steps"></a>Étapes suivantes

* [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) est une application autonome gratuit, à partir de Microsoft qui vous permet de toowork visuellement avec des données de stockage Azure sur Windows, Mac OS et Linux.
* [Kit de développement logiciel (SDK) Azure Storage pour Java][Azure Storage SDK for Java]
* [référence SDK cliente de stockage Azure][référence SDK cliente de stockage Azure]
* [API REST Stockage Azure][Azure Storage REST API]
* [Blog de l’équipe Stockage Azure][Azure Storage Team Blog]

Pour plus d’informations, consultez [Azure pour les développeurs Java](/java/azure).

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[référence SDK cliente de stockage Azure]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[Azure Tables: Introducing Upsert and Query Projection]: http://blogs.msdn.com/b/windowsazurestorage/archive/2011/09/15/windows-azure-tables-introducing-upsert-and-query-projection.aspx
