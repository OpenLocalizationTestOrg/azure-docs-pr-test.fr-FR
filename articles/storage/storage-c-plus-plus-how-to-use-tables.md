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
# <a name="how-toouse-table-storage-from-c"></a>Comment toouse le stockage de Table à partir de C++
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>Vue d'ensemble
Ce guide explique comment tooperform des scénarios courants à l’aide de hello service de stockage de Table Azure. exemples de Hello sont écrits en C++ et utiliser hello [bibliothèque cliente de stockage Azure pour C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md). Hello scénarios abordés incluent **création et suppression d’une table** et **utilisation des entités de table**.

> [!NOTE]
> Les cibles de ce guide hello bibliothèque cliente Azure Storage pour C++ version 1.0.0 et versions ultérieures. Hello recommandé de version est la bibliothèque cliente de stockage 2.2.0, qui est disponible via [NuGet](http://www.nuget.org/packages/wastorage) ou [GitHub](https://github.com/Azure/azure-storage-cpp/).
> 
> 

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a>Création d’une application C++
Dans ce guide, vous allez utiliser des fonctionnalités de stockage qui peuvent être exécutées dans une application C++. toodo par conséquent, vous devez tooinstall hello bibliothèque cliente Azure Storage pour C++ et créer un compte de stockage Azure dans votre abonnement Azure.  

tooinstall hello bibliothèque cliente Azure Storage pour C++, vous pouvez utiliser hello méthodes suivantes :

* **Linux :** suivez les indications hello hello [bibliothèque cliente de stockage Azure pour C++ Lisez-moi](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.  
* **Windows :** dans Visual Studio, cliquez sur **Outils &gt; Gestionnaire de package NuGet &gt; Console du gestionnaire de package**. Tapez ce qui suit hello commande dans hello [console du Gestionnaire de Package NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) et appuyez sur ENTRÉE.  
  
     Install-Package wastorage

## <a name="configure-your-application-tooaccess-table-storage"></a>Configurer votre application de tooaccess le stockage de Table
Ajouter suivant de hello inclure haut de toohello d’instructions de hello C++ fichier dans lequel les tables tooaccess API toouse hello stockage Azure :  

```cpp
#include <was/storage_account.h>
#include <was/table.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a>Configuration d’une chaîne de connexion au stockage Azure
Un client de stockage Azure utilise une terminaison de stockage connexion chaîne toostore et informations d’identification pour accéder aux services de gestion de données. Lors de l’exécution d’une application cliente, vous devez fournir la chaîne de connexion de stockage hello Bonjour suivant le format. Utiliser le nom de votre compte et hello stockage clé d’accès pour le compte de stockage hello hello répertoriés dans hello [Azure Portal](https://portal.azure.com) pour hello *AccountName* et *AccountKey* valeurs. Pour plus d’informations sur les comptes et les clés d’accès de stockage, consultez [À propos des comptes Azure Storage](storage-create-storage-account.md). Cet exemple montre comment vous pouvez déclarer une chaîne de connexion de champ statique toohold hello :  

```cpp
// Define hello connection string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

tootest votre application sur votre ordinateur local basé sur Windows, vous pouvez utiliser hello Azure [l’émulateur de stockage](storage-use-emulator.md) qui est installé avec hello [Azure SDK](https://azure.microsoft.com/downloads/). l’émulateur de stockage Hello est un utilitaire qui simule hello Azure Blob, file d’attente et Table services disponibles sur votre ordinateur de développement local. Hello suivant montre comment vous pouvez déclarer un champ statique toohold hello connexion chaîne tooyour local l’émulateur de stockage :  

```cpp
// Define hello connection string with Azure storage emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

toostart hello émulateur de stockage Azure, cliquez sur hello **Démarrer** bouton ou appuyez sur clé de Windows hello. Commencez à taper **émulateur de stockage Azure**, puis sélectionnez **émulateur de stockage Microsoft Azure** à partir de la liste des applications hello.  

Hello exemples suivants supposent que vous avez utilisé une de ces chaînes de connexion de stockage de deux méthodes tooget hello.  

## <a name="retrieve-your-connection-string"></a>Récupération de votre chaîne de connexion
Vous pouvez utiliser hello **cloud_storage_account** classe toorepresent vos informations de compte de stockage. tooretrieve plus d’informations à partir de la chaîne de connexion de stockage hello du compte de votre stockage, vous pouvez utiliser la méthode d’analyse hello.

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

Ensuite, obtenez une référence tooa **cloud_table_client** de classe, comme il vous permet d’obtenir des objets de référence pour les tables et entités stockées dans hello service de stockage de Table. Hello de code suivant crée un **cloud_table_client** objet à l’aide d’objet de compte de stockage hello nous récupérées ci-dessus :  

```cpp
// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();
```

## <a name="create-a-table"></a>Création d’une table
Un objet **cloud_table_client** vous permet d’obtenir les objets de référence pour les tables et entités. Hello de code suivant crée un **cloud_table_client** de l’objet et l’utilise toocreate une nouvelle table.

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

## <a name="add-an-entity-tooa-table"></a>Ajouter une table de tooa d’entité
tooadd une table de tooa entité, créez un **table_entity** de l’objet et lui passer trop**table_operation::insert_entity**. Hello de code suivant utilise prénom du client hello en tant que clé de ligne hello et le nom comme clé de partition hello. Ensemble, les partitions d’une entité et la clé de ligne identifient hello entité dans la table de hello. Entités avec hello même clé de partition peut être interrogé plus rapidement que les différents avec des clés de partition, mais à l’aide de clés de partition divers permet une plus grande évolutivité de l’opération parallèle. Pour plus d’informations, consultez [Liste de contrôle des performances et de l’extensibilité de Microsoft Azure Storage](storage-performance-checklist.md).

Hello de code suivant crée une nouvelle instance de **table_entity** avec certaines toobe de données client stockée. Hello de code suivante appelle **table_operation::insert_entity** toocreate un **table_operation** tooinsert une entité de l’objet dans une table, et associe hello nouvelle entité de table avec lui. Enfin, les appels de code hello hello exécuter la méthode sur hello **cloud_table** objet. Et hello nouvelle **table_operation** envoie une demande de toohello Table service tooinsert hello nouvelle entité customer dans la table « people » de hello.  

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

## <a name="insert-a-batch-of-entities"></a>Insertion d’un lot d’entités
Vous pouvez insérer un lot d’entités toohello service de Table dans une opération d’écriture. Hello de code suivant crée un **table_batch_operation** de l’objet, puis ajoute trois insérer tooit d’opérations. Chaque opération d’insertion est ajoutée en créant un nouvel objet d’entité, ses valeurs, et puis en appelant hello insérer la méthode sur hello **table_batch_operation** objet entité de hello tooassociate avec une nouvelle opération d’insertion. Ensuite, **cloud_table.execute** est appelé l’opération de hello tooexecute.  

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

Toonote de certaines opérations sur les opérations de traitement par lots :  

* Vous pouvez effectuer des too100 insert, delete, merge, replace, opérations insert ou merge et insérer ou remplacer dans n’importe quelle combinaison dans un lot unique.  
* Une opération de traitement peut avoir une opération de récupération, s’il est la seule opération de hello dans un lot de hello.  
* Toutes les entités dans une seule opération doivent avoir hello même clé de partition.  
* Une opération de traitement est la charge utile de données de 4 Mo tooa limité.  

## <a name="retrieve-all-entities-in-a-partition"></a>Extraction de toutes les entités d'une partition
tooquery une table pour toutes les entités dans une partition, utilisez un **table_query** objet. Hello exemple de code suivant spécifie un filtre pour les entités où « Smith » est la clé de partition hello. Cet exemple imprime les champs de chaque entité dans la console de toohello de résultats de requête hello hello.  

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

requête Hello dans cet exemple met toutes les entités hello qui correspondent aux critères de filtre hello. Si vous avez des tables volumineuses et que vous devez souvent les entités de table toodownload hello, nous vous recommandons que vous stockez vos données dans des objets BLOB de stockage Azure à la place.

## <a name="retrieve-a-range-of-entities-in-a-partition"></a>Extraction d’un ensemble d’entités dans une partition
Si vous ne souhaitez pas tooquery toutes les entités hello dans une partition, vous pouvez spécifier une plage en combinant le filtre de clé de partition hello avec un filtre de clé de ligne. Hello exemple de code suivant utilise deux filtres tooget toutes les entités dans la partition « Smith », où la clé de ligne hello (prénom) commence par une lettre « E » dans l’alphabet de hello plus tôt et imprime ensuite les résultats de la requête hello.  

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

## <a name="retrieve-a-single-entity"></a>Extraction d'une seule entité
Vous pouvez écrire une requête tooretrieve une entité unique et spécifique. code Hello suivant utilise **table_operation::retrieve_entity** client de hello toospecify « Jeff Smith ». Cette méthode renvoie qu’une seule entité, plutôt qu’une collection et hello valeur retournée dans **table_result**. Spécification des clés de partition et de ligne dans une requête est tooretrieve de manière plus rapide hello une seule entité hello service de Table.  

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

## <a name="replace-an-entity"></a>Remplacement d’une entité
tooreplace une entité, récupérer à partir du service de Table hello, modifier l’objet d’entité hello, puis enregistrez les modifications hello de nouveau service de Table toohello. Hello code suivant modifie l’adresse de messagerie et le numéro du téléphone d’un client existant. Au lieu d’appeler **table_operation::insert_entity**, ce code utilise **table_operation::replace_entity**. Cela provoque une toobe d’entité hello entièrement remplacé sur le serveur de hello, sauf si l’entité hello sur le serveur de hello a changé depuis sa récupération, auquel cas hello échoue. Cet échec est tooprevent votre application à partir de remplacement accidentel d’une modification effectuée entre hello récupération et mettre à jour par un autre composant de votre application. Hello gestion correcte de cet échec est tooretrieve hello entité à nouveau, apportez vos modifications (si elle est toujours valide), puis effectuer une autre **table_operation::replace_entity** opération. Hello prochaine section vous montrera comment toooverride ce comportement.  

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

## <a name="insert-or-replace-an-entity"></a>Insertion ou remplacement d’une entité
**table_operation::replace_entity** opérations échouent si l’entité de hello a été modifiée, car il a été récupéré à partir du serveur de hello. En outre, vous devez récupérer des entités de hello de hello serveur tout d’abord pour **table_operation::replace_entity** toobe réussie. Dans certains cas, toutefois, vous ne connaissez pas si l’entité hello existe sur le serveur de hello et les valeurs actuelles hello stockés qu’il contient sont sans intérêt, votre mise à jour doit remplacer toutes les. tooaccomplish, vous devez utiliser un **table_operation::insert_or_replace_entity** opération. Cette opération insère l’entité de hello si elle n’existe pas ou elle remplace dans ce cas, quelle que soit la lorsque la dernière mise à jour de hello a été effectuée. Dans l’exemple de code suivant de hello, entité customer de hello pour Jeff Smith est toujours récupérée, mais il est ensuite enregistrée serveur toohello arrière via **table_operation::insert_or_replace_entity**. Les mises à jour apportées entité toohello entre une opération de mise à jour et de récupération hello seront remplacées.  

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

## <a name="query-a-subset-of-entity-properties"></a>Interrogation d’un sous-ensemble de propriétés d’entité
Une table de tooa de requête peut récupérer des propriétés peu d’une entité. requête de hello suivant code Hello utilise hello **table_query::set_select_columns** méthode tooreturn uniquement hello adresses de messagerie des entités de table de hello.  

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
> L’interrogation d’un petit nombre de propriétés d’une entité est une opération plus efficace que l’extraction de toutes les propriétés.
> 
> 

## <a name="delete-an-entity"></a>Suppression d’une entité
Il est facile de supprimer une entité après l’avoir récupérée. Une fois que l’entité de hello est récupérée, appelez **table_operation::delete_entity** avec toodelete d’entité hello. Appelez ensuite hello **cloud_table.execute** (méthode). Bonjour de code suivant récupère et supprime une entité avec une clé de partition « Smith » et une clé de ligne de « Jeff ».  

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

## <a name="delete-a-table"></a>Suppression d’une table
Enfin, hello, exemple de code suivant supprime une table à partir d’un compte de stockage. Une table qui a été supprimée sera indisponible toobe recréée pour une période de temps après la suppression de hello.  

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

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez appris les notions de base de hello du stockage table, suivez ces liens de toolearn plus d’informations sur le stockage Azure :  

* [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) est une application autonome gratuit, à partir de Microsoft qui vous permet de toowork visuellement avec des données de stockage Azure sur Windows, Mac OS et Linux.
* [Comment toouse stockage d’objets Blob à partir de C++](storage-c-plus-plus-how-to-use-blobs.md)
* [Comment toouse stockage de file d’attente à partir de C++](storage-c-plus-plus-how-to-use-queues.md)
* [Listage des ressources Azure Storage en C++](storage-c-plus-plus-enumeration.md)
* [Référence de la bibliothèque cliente de stockage pour C++](http://azure.github.io/azure-storage-cpp)
* [Documentation d’Azure Storage](https://azure.microsoft.com/documentation/services/storage/)
