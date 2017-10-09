---
title: "aaaHow toouse le stockage de table à partir de PHP | Documents Microsoft"
description: "Découvrez comment toouse hello service de Table à partir de PHP toocreate et supprimer une table et insert, delete et table de requête hello."
services: storage
documentationcenter: php
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 1e57f371-6208-4753-b2a0-05db4aede8e3
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: php
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 1e1036118e208280b4c205da7d7eea61e79359c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-from-php"></a>Comment toouse table stockage à partir de PHP
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>Vue d'ensemble
Ce guide vous explique comment tooperform des scénarios courants utilisant hello service Table Azure. exemples de Hello sont écrits en PHP et utiliser hello [Azure SDK pour PHP][download]. Hello scénarios abordés incluent **création et la suppression d’une table et insertion, suppression et interrogation des entités dans une table**. Pour plus d’informations sur hello service Table Azure, consultez hello [étapes](#next-steps) section.

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a>Création d'une application PHP
Hello uniquement requis pour la création d’une application PHP qui accède au service de Table Azure hello est hello faisant référence à des classes Bonjour Azure SDK pour PHP à partir de votre code. Vous pouvez utiliser n’importe quel toocreate d’outils de développement de votre application, notamment le bloc-notes.

Dans ce guide, vous utilisez les fonctionnalités du service de Table qui peuvent être appelées dans une application PHP en local, ou dans le code s'exécutant dans un rôle web, un rôle de travail ou un site web Azure.

## <a name="get-hello-azure-client-libraries"></a>Obtenir les bibliothèques clientes Azure hello
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-hello-table-service"></a>Configurer votre service de Table application tooaccess hello
service de Table Azure hello toouse API, vous devez :

1. Fichier de chargeur automatique de hello référence à l’aide de hello [require_once] [ require_once] instruction, et
2. référencer toute classe que vous êtes susceptible d'utiliser.

Hello suivant montre comment tooinclude hello hello de référence et le fichier de chargeur automatique **ServicesBuilder** classe.

> [!NOTE]
> exemples Hello dans cet article supposent que vous avez installé hello PHP les bibliothèques clientes pour Azure via l’éditeur. Si vous avez installé les bibliothèques hello manuellement, vous devez tooreference hello <code>WindowsAzure.php</code> fichier de chargeur automatique.
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

Dans les exemples de hello ci-dessous, hello `require_once` instruction est toujours affichée, mais uniquement les classes de hello nécessaires pour hello exemple tooexecute sont référencés.

## <a name="set-up-an-azure-storage-connection"></a>Configuration d’une connexion de stockage Azure
tooinstantiate un client du service Table Azure, vous devez avoir une chaîne de connexion valide. format Hello pour hello chaîne de connexion de service de Table est la suivante :

Pour accéder à un service en ligne :

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

Pour accéder au stockage d’émulateur hello :

```php
UseDevelopmentStorage=true
```

toocreate n’importe quel client de service Azure, vous devez toouse hello **ServicesBuilder** classe. Vous pouvez :

* passer hello connexion chaîne directement tooit ou
* Utilisez hello **CloudConfigurationManager (CCM)** toocheck externe de plusieurs sources pour la chaîne de connexion hello :
  * Par défaut, il prend en charge une source externe : les variables d’environnement.
  * Vous pouvez ajouter de nouvelles sources en étendant hello **ConnectionStringSource** classe

Pour obtenir des exemples hello décrites ici, la chaîne de connexion hello sera passé directement.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);
```

## <a name="create-a-table"></a>Création d’une table
A **TableRestProxy** objet vous permet de créer une table avec hello **createTable** (méthode). Lorsque vous créez une table, vous pouvez définir le délai d’attente de service de Table hello. (Pour plus d’informations sur le délai d’attente de service de Table hello, consultez [définition de délais pour les opérations de Service de Table][table-service-timeouts].)

```php
require_once 'vendor\autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

try    {
    // Create table.
    $tableRestProxy->createTable("mytable");
}
catch(ServiceException $e){
    $code = $e->getCode();
    $error_message = $e->getMessage();
    // Handle exception based on error codes and messages.
    // Error codes and messages can be found here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
}
```

Pour plus d’informations sur les restrictions sur les noms de table, consultez [hello de présentation des modèle de données de Service de Table][table-data-model].

## <a name="add-an-entity-tooa-table"></a>Ajouter une table de tooa d’entité
tooadd une table de tooa entité, créez un **entité** de l’objet et lui passer trop**TableRestProxy -> insertEntity**. Notez que lorsque vous créez une entité, vous devez spécifier une clé `PartitionKey` et `RowKey`. Ceux-ci sont des identificateurs uniques pour une entité hello et sont des valeurs qui peuvent être interrogées beaucoup plus rapidement que les autres propriétés de l’entité. Hello système utilise `PartitionKey` tooautomatically distribuer les entités de la table hello sur plusieurs nœuds de stockage. Les entités avec hello même `PartitionKey` sont stockés sur hello même nœud. (Les opérations sur plusieurs entités stockées sur hello même nœud effectuer supérieure aux entités stockées sur différents nœuds.) Hello `RowKey` est hello des ID unique d’une entité dans une partition.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\Entity;
use MicrosoftAzure\Storage\Table\Models\EdmType;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$entity = new Entity();
$entity->setPartitionKey("tasksSeattle");
$entity->setRowKey("1");
$entity->addProperty("Description", null, "Take out hello trash.");
$entity->addProperty("DueDate",
                        EdmType::DATETIME,
                        new DateTime("2012-11-05T08:15:00-08:00"));
$entity->addProperty("Location", EdmType::STRING, "Home");

try{
    $tableRestProxy->insertEntity("mytable", $entity);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
}
```

Pour plus d’informations sur les propriétés de la Table et de types, consultez [hello de présentation des modèle de données de Service de Table][table-data-model].

Hello **TableRestProxy** classe offre deux méthodes alternatives pour l’insertion d’entités : **insertOrMergeEntity** et **insertOrReplaceEntity**. toouse ces méthodes, créez un **entité** et passez-le en tant que paramètre tooeither méthode. Chaque méthode insère l’entité de hello s’il n’existe pas. Si l’entité de hello existe déjà, **insertOrMergeEntity** met à jour les valeurs de propriété si les propriétés hello existent déjà et ajoute les nouvelles propriétés s’ils n’existent pas, alors que **insertOrReplaceEntity** complètement remplace une entité existante. Hello suivant montre l’exemple de comment toouse **insertOrMergeEntity**. Si hello entité avec `PartitionKey` « tasksSeattle » et `RowKey` « 1 » n’existe pas déjà, il sera inséré. Toutefois, s’il a été inséré précédemment (comme indiqué dans l’exemple hello ci-dessus), hello `DueDate` propriété sera mise à jour et hello `Status` propriété sera ajoutée. Hello `Description` et `Location` sont également mises à jour, mais avec des valeurs qui efficacement les laisser inchangés. Si ces deux dernières propriétés ont été pas ajoutées comme indiqué dans l’exemple de hello, mais se trouvait sur l’entité cible hello, leurs valeurs existantes reste inchangées.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\Entity;
use MicrosoftAzure\Storage\Table\Models\EdmType;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

//Create new entity.
$entity = new Entity();

// PartitionKey and RowKey are required.
$entity->setPartitionKey("tasksSeattle");
$entity->setRowKey("1");

// If entity exists, existing properties are updated with new values and
// new properties are added. Missing properties are unchanged.
$entity->addProperty("Description", null, "Take out hello trash.");
$entity->addProperty("DueDate", EdmType::DATETIME, new DateTime()); // Modified hello DueDate field.
$entity->addProperty("Location", EdmType::STRING, "Home");
$entity->addProperty("Status", EdmType::STRING, "Complete"); // Added Status field.

try    {
    // Calling insertOrReplaceEntity, instead of insertOrMergeEntity as shown,
    // would simply replace hello entity with PartitionKey "tasksSeattle" and RowKey "1".
    $tableRestProxy->insertOrMergeEntity("mytable", $entity);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="retrieve-a-single-entity"></a>Extraction d'une seule entité
Hello **TableRestProxy -> getEntity** méthode vous permet de tooretrieve une seule entité en recherchant son `PartitionKey` et `RowKey`. Dans l’exemple hello ci-dessous, hello clé de partition `tasksSeattle` et clé de ligne `1` sont passés toohello **getEntity** (méthode).

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

try    {
    $result = $tableRestProxy->getEntity("mytable", "tasksSeattle", 1);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

$entity = $result->getEntity();

echo $entity->getPartitionKey().":".$entity->getRowKey();
```

## <a name="retrieve-all-entities-in-a-partition"></a>Extraction de toutes les entités d'une partition
Les requêtes d’entité sont construites à l’aide de filtres (pour plus d’informations, consultez la page [Interrogation de tables et d’entités][filters]). tooretrieve toutes les entités dans la partition, utilisez les filtre hello » PartitionKey eq *nom_partition*». Hello suivant montre l’exemple de comment tooretrieve toutes les entités de hello `tasksSeattle` partition en passant un filtre toohello **queryEntities** (méthode).

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$filter = "PartitionKey eq 'tasksSeattle'";

try    {
    $result = $tableRestProxy->queryEntities("mytable", $filter);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

$entities = $result->getEntities();

foreach($entities as $entity){
    echo $entity->getPartitionKey().":".$entity->getRowKey()."<br />";
}
```

## <a name="retrieve-a-subset-of-entities-in-a-partition"></a>Extraction d'un sous-ensemble d'entités dans une partition
Hello même modèle utilisé dans l’exemple précédent de hello peut être utilisé tooretrieve n’importe quel sous-ensemble d’entités dans une partition. sous-ensemble Hello d’entités que vous récupérez sont déterminées par le filtre hello (pour plus d’informations, consultez [interrogeant les Tables et les entités][filters]) .hello suivant montre l’exemple de comment toouse un tooretrieve de filtre toutes les entités avec un spécifique `Location` et un `DueDate` inférieur à une date spécifiée.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$filter = "Location eq 'Office' and DueDate lt '2012-11-5'";

try    {
    $result = $tableRestProxy->queryEntities("mytable", $filter);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

$entities = $result->getEntities();

foreach($entities as $entity){
    echo $entity->getPartitionKey().":".$entity->getRowKey()."<br />";
}
```

## <a name="retrieve-a-subset-of-entity-properties"></a>Extraction d'un sous-ensemble de propriétés d'entité
Une requête peut extraire un sous-ensemble de propriétés d'entité. Cette technique, nommée *projection*, réduit la consommation de bande passante et peut améliorer les performances des requêtes, notamment pour les entités volumineuses. de récupérer une propriété toobe toospecify, passez nom hello de hello propriété toohello **requête -> addSelectField** (méthode). Vous pouvez appeler cette méthode plusieurs fois tooadd plus de propriétés. Après l’exécution de **TableRestProxy -> queryEntities**, hello retourné entités ont uniquement des propriétés de hello sélectionné. (Si vous voulez tooreturn un sous-ensemble d’entités de Table, utilisez un filtre comme indiqué dans les requêtes hello ci-dessus.)

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\QueryEntitiesOptions;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$options = new QueryEntitiesOptions();
$options->addSelectField("Description");

try    {
    $result = $tableRestProxy->queryEntities("mytable", $options);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

// All entities in hello table are returned, regardless of whether
// they have hello Description field.
// toolimit hello results returned, use a filter.
$entities = $result->getEntities();

foreach($entities as $entity){
    $description = $entity->getProperty("Description")->getValue();
    echo $description."<br />";
}
```

## <a name="update-an-entity"></a>Mise à jour d'une entité
Une entité existante peut être mis à jour à l’aide de hello **entité -> setProperty** et **entité -> addProperty** méthodes sur l’entité de hello et en appelant **TableRestProxy -> updateEntity** . Hello exemple suivant récupère une entité, modifie une propriété, supprime une autre propriété et ajoute une nouvelle propriété. Notez que vous pouvez supprimer une propriété en définissant sa valeur trop**null**.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\Entity;
use MicrosoftAzure\Storage\Table\Models\EdmType;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$result = $tableRestProxy->getEntity("mytable", "tasksSeattle", 1);

$entity = $result->getEntity();

$entity->setPropertyValue("DueDate", new DateTime()); //Modified DueDate.

$entity->setPropertyValue("Location", null); //Removed Location.

$entity->addProperty("Status", EdmType::STRING, "In progress"); //Added Status.

try    {
    $tableRestProxy->updateEntity("mytable", $entity);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="delete-an-entity"></a>Suppression d’une entité
toodelete une entité, passez le nom de la table hello et l’entité hello `PartitionKey` et `RowKey` toohello **TableRestProxy -> deleteEntity** (méthode).

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

try    {
    // Delete entity.
    $tableRestProxy->deleteEntity("mytable", "tasksSeattle", "2");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

Notez que pour les contrôles d’accès concurrentiel, vous pouvez définir hello Etag pour une toobe entité supprimée à l’aide de hello **DeleteEntityOptions -> setEtag** méthode et en passant hello **DeleteEntityOptions** trop de l’objet**deleteEntity** en tant que quatrième paramètre.

## <a name="batch-table-operations"></a>Traitement par lots d'opérations de table
Hello **TableRestProxy -> traitement par lots** méthode vous permet de tooexecute plusieurs opérations dans une demande unique. Hello modèle implique l’ajout des opérations trop**BatchRequest** objet et à passer hello **BatchRequest** objet toohello **TableRestProxy -> traitement par lots** (méthode). tooadd une opération de tooa **BatchRequest** de l’objet, vous pouvez appeler les hello plusieurs fois de méthodes suivantes :

* **addInsertEntity** (permet d'ajouter une opération insertEntity)
* **addUpdateEntity** (permet d'ajouter une opération updateEntity)
* **addMergeEntity** (permet d'ajouter une opération mergeEntity)
* **addInsertOrReplaceEntity** (permet d'ajouter une opération insertOrReplaceEntity)
* **addInsertOrMergeEntity** (permet d'ajouter une opération insertOrMergeEntity)
* **addDeleteEntity** (permet d'ajouter une opération deleteEntity)

Hello suivant montre l’exemple de comment tooexecute **insertEntity** et **deleteEntity** opérations dans une demande unique :

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\Entity;
use MicrosoftAzure\Storage\Table\Models\EdmType;
use MicrosoftAzure\Storage\Table\Models\BatchOperations;

    // Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

// Create list of batch operation.
$operations = new BatchOperations();

$entity1 = new Entity();
$entity1->setPartitionKey("tasksSeattle");
$entity1->setRowKey("2");
$entity1->addProperty("Description", null, "Clean roof gutters.");
$entity1->addProperty("DueDate",
                        EdmType::DATETIME,
                        new DateTime("2012-11-05T08:15:00-08:00"));
$entity1->addProperty("Location", EdmType::STRING, "Home");

// Add operation toolist of batch operations.
$operations->addInsertEntity("mytable", $entity1);

// Add operation toolist of batch operations.
$operations->addDeleteEntity("mytable", "tasksSeattle", "1");

try    {
    $tableRestProxy->batch($operations);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

Pour plus d’informations sur le traitement par lots d’opérations de table, consultez la page [Exécution de transactions de groupe d’entités][entity-group-transactions].

## <a name="delete-a-table"></a>Suppression d’une table
Enfin, toodelete une table, passer toohello de nom de table hello **TableRestProxy -> deleteTable** (méthode).

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

try    {
    // Delete table.
    $tableRestProxy->deleteTable("mytable");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez appris les notions de base de hello Hello service Table Azure, suivez ces toolearn des liens sur les tâches de stockage plus complexes.

* [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) est une application autonome gratuit, à partir de Microsoft qui vous permet de toowork visuellement avec des données de stockage Azure sur Windows, Mac OS et Linux.

* [Centre de développement PHP](/develop/php/).

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://php.net/require_once
[table-service-timeouts]: http://msdn.microsoft.com/library/azure/dd894042.aspx

[table-data-model]: http://msdn.microsoft.com/library/azure/dd179338.aspx
[filters]: http://msdn.microsoft.com/library/azure/dd894031.aspx
[entity-group-transactions]: http://msdn.microsoft.com/library/azure/dd894038.aspx
