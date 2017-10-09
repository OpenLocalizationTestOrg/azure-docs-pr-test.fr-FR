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
# <a name="how-toouse-table-storage-from-php"></a><span data-ttu-id="46f34-103">Comment toouse table stockage à partir de PHP</span><span class="sxs-lookup"><span data-stu-id="46f34-103">How toouse table storage from PHP</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="46f34-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="46f34-104">Overview</span></span>
<span data-ttu-id="46f34-105">Ce guide vous explique comment tooperform des scénarios courants utilisant hello service Table Azure.</span><span class="sxs-lookup"><span data-stu-id="46f34-105">This guide shows you how tooperform common scenarios using hello Azure Table service.</span></span> <span data-ttu-id="46f34-106">exemples de Hello sont écrits en PHP et utiliser hello [Azure SDK pour PHP][download].</span><span class="sxs-lookup"><span data-stu-id="46f34-106">hello samples are written in PHP and use hello [Azure SDK for PHP][download].</span></span> <span data-ttu-id="46f34-107">Hello scénarios abordés incluent **création et la suppression d’une table et insertion, suppression et interrogation des entités dans une table**.</span><span class="sxs-lookup"><span data-stu-id="46f34-107">hello scenarios covered include **creating and deleting a table, and inserting, deleting, and querying entities in a table**.</span></span> <span data-ttu-id="46f34-108">Pour plus d’informations sur hello service Table Azure, consultez hello [étapes](#next-steps) section.</span><span class="sxs-lookup"><span data-stu-id="46f34-108">For more information on hello Azure Table service, see hello [Next steps](#next-steps) section.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="46f34-109">Création d'une application PHP</span><span class="sxs-lookup"><span data-stu-id="46f34-109">Create a PHP application</span></span>
<span data-ttu-id="46f34-110">Hello uniquement requis pour la création d’une application PHP qui accède au service de Table Azure hello est hello faisant référence à des classes Bonjour Azure SDK pour PHP à partir de votre code.</span><span class="sxs-lookup"><span data-stu-id="46f34-110">hello only requirement for creating a PHP application that accesses hello Azure Table service is hello referencing of classes in hello Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="46f34-111">Vous pouvez utiliser n’importe quel toocreate d’outils de développement de votre application, notamment le bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="46f34-111">You can use any development tools toocreate your application, including Notepad.</span></span>

<span data-ttu-id="46f34-112">Dans ce guide, vous utilisez les fonctionnalités du service de Table qui peuvent être appelées dans une application PHP en local, ou dans le code s'exécutant dans un rôle web, un rôle de travail ou un site web Azure.</span><span class="sxs-lookup"><span data-stu-id="46f34-112">In this guide, you use Table service features which can be called from within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-hello-azure-client-libraries"></a><span data-ttu-id="46f34-113">Obtenir les bibliothèques clientes Azure hello</span><span class="sxs-lookup"><span data-stu-id="46f34-113">Get hello Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-hello-table-service"></a><span data-ttu-id="46f34-114">Configurer votre service de Table application tooaccess hello</span><span class="sxs-lookup"><span data-stu-id="46f34-114">Configure your application tooaccess hello Table service</span></span>
<span data-ttu-id="46f34-115">service de Table Azure hello toouse API, vous devez :</span><span class="sxs-lookup"><span data-stu-id="46f34-115">toouse hello Azure Table service APIs, you need to:</span></span>

1. <span data-ttu-id="46f34-116">Fichier de chargeur automatique de hello référence à l’aide de hello [require_once] [ require_once] instruction, et</span><span class="sxs-lookup"><span data-stu-id="46f34-116">Reference hello autoloader file using hello [require_once][require_once] statement, and</span></span>
2. <span data-ttu-id="46f34-117">référencer toute classe que vous êtes susceptible d'utiliser.</span><span class="sxs-lookup"><span data-stu-id="46f34-117">Reference any classes you might use.</span></span>

<span data-ttu-id="46f34-118">Hello suivant montre comment tooinclude hello hello de référence et le fichier de chargeur automatique **ServicesBuilder** classe.</span><span class="sxs-lookup"><span data-stu-id="46f34-118">hello following example shows how tooinclude hello autoloader file and reference hello **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="46f34-119">exemples Hello dans cet article supposent que vous avez installé hello PHP les bibliothèques clientes pour Azure via l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="46f34-119">hello examples in this article assume you have installed hello PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="46f34-120">Si vous avez installé les bibliothèques hello manuellement, vous devez tooreference hello <code>WindowsAzure.php</code> fichier de chargeur automatique.</span><span class="sxs-lookup"><span data-stu-id="46f34-120">If you installed hello libraries manually, you need tooreference hello <code>WindowsAzure.php</code> autoloader file.</span></span>
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="46f34-121">Dans les exemples de hello ci-dessous, hello `require_once` instruction est toujours affichée, mais uniquement les classes de hello nécessaires pour hello exemple tooexecute sont référencés.</span><span class="sxs-lookup"><span data-stu-id="46f34-121">In hello examples below, hello `require_once` statement is always shown, but only hello classes necessary for hello example tooexecute are referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="46f34-122">Configuration d’une connexion de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="46f34-122">Set up an Azure storage connection</span></span>
<span data-ttu-id="46f34-123">tooinstantiate un client du service Table Azure, vous devez avoir une chaîne de connexion valide.</span><span class="sxs-lookup"><span data-stu-id="46f34-123">tooinstantiate an Azure Table service client, you must first have a valid connection string.</span></span> <span data-ttu-id="46f34-124">format Hello pour hello chaîne de connexion de service de Table est la suivante :</span><span class="sxs-lookup"><span data-stu-id="46f34-124">hello format for hello Table service connection string is:</span></span>

<span data-ttu-id="46f34-125">Pour accéder à un service en ligne :</span><span class="sxs-lookup"><span data-stu-id="46f34-125">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="46f34-126">Pour accéder au stockage d’émulateur hello :</span><span class="sxs-lookup"><span data-stu-id="46f34-126">For accessing hello emulator storage:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="46f34-127">toocreate n’importe quel client de service Azure, vous devez toouse hello **ServicesBuilder** classe.</span><span class="sxs-lookup"><span data-stu-id="46f34-127">toocreate any Azure service client, you need toouse hello **ServicesBuilder** class.</span></span> <span data-ttu-id="46f34-128">Vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="46f34-128">You can:</span></span>

* <span data-ttu-id="46f34-129">passer hello connexion chaîne directement tooit ou</span><span class="sxs-lookup"><span data-stu-id="46f34-129">pass hello connection string directly tooit or</span></span>
* <span data-ttu-id="46f34-130">Utilisez hello **CloudConfigurationManager (CCM)** toocheck externe de plusieurs sources pour la chaîne de connexion hello :</span><span class="sxs-lookup"><span data-stu-id="46f34-130">use hello **CloudConfigurationManager (CCM)** toocheck multiple external sources for hello connection string:</span></span>
  * <span data-ttu-id="46f34-131">Par défaut, il prend en charge une source externe : les variables d’environnement.</span><span class="sxs-lookup"><span data-stu-id="46f34-131">by default, it comes with support for one external source - environmental variables</span></span>
  * <span data-ttu-id="46f34-132">Vous pouvez ajouter de nouvelles sources en étendant hello **ConnectionStringSource** classe</span><span class="sxs-lookup"><span data-stu-id="46f34-132">you can add new sources by extending hello **ConnectionStringSource** class</span></span>

<span data-ttu-id="46f34-133">Pour obtenir des exemples hello décrites ici, la chaîne de connexion hello sera passé directement.</span><span class="sxs-lookup"><span data-stu-id="46f34-133">For hello examples outlined here, hello connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);
```

## <a name="create-a-table"></a><span data-ttu-id="46f34-134">Création d’une table</span><span class="sxs-lookup"><span data-stu-id="46f34-134">Create a table</span></span>
<span data-ttu-id="46f34-135">A **TableRestProxy** objet vous permet de créer une table avec hello **createTable** (méthode).</span><span class="sxs-lookup"><span data-stu-id="46f34-135">A **TableRestProxy** object lets you create a table with hello **createTable** method.</span></span> <span data-ttu-id="46f34-136">Lorsque vous créez une table, vous pouvez définir le délai d’attente de service de Table hello.</span><span class="sxs-lookup"><span data-stu-id="46f34-136">When creating a table, you can set hello Table service timeout.</span></span> <span data-ttu-id="46f34-137">(Pour plus d’informations sur le délai d’attente de service de Table hello, consultez [définition de délais pour les opérations de Service de Table][table-service-timeouts].)</span><span class="sxs-lookup"><span data-stu-id="46f34-137">(For more information about hello Table service timeout, see [Setting Timeouts for Table Service Operations][table-service-timeouts].)</span></span>

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

<span data-ttu-id="46f34-138">Pour plus d’informations sur les restrictions sur les noms de table, consultez [hello de présentation des modèle de données de Service de Table][table-data-model].</span><span class="sxs-lookup"><span data-stu-id="46f34-138">For information about restrictions on table names, see [Understanding hello Table Service Data Model][table-data-model].</span></span>

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="46f34-139">Ajouter une table de tooa d’entité</span><span class="sxs-lookup"><span data-stu-id="46f34-139">Add an entity tooa table</span></span>
<span data-ttu-id="46f34-140">tooadd une table de tooa entité, créez un **entité** de l’objet et lui passer trop**TableRestProxy -> insertEntity**.</span><span class="sxs-lookup"><span data-stu-id="46f34-140">tooadd an entity tooa table, create a new **Entity** object and pass it too**TableRestProxy->insertEntity**.</span></span> <span data-ttu-id="46f34-141">Notez que lorsque vous créez une entité, vous devez spécifier une clé `PartitionKey` et `RowKey`.</span><span class="sxs-lookup"><span data-stu-id="46f34-141">Note that when you create an entity, you must specify a `PartitionKey` and `RowKey`.</span></span> <span data-ttu-id="46f34-142">Ceux-ci sont des identificateurs uniques pour une entité hello et sont des valeurs qui peuvent être interrogées beaucoup plus rapidement que les autres propriétés de l’entité.</span><span class="sxs-lookup"><span data-stu-id="46f34-142">These are hello unique identifiers for an entity and are values that can be queried much faster than other entity properties.</span></span> <span data-ttu-id="46f34-143">Hello système utilise `PartitionKey` tooautomatically distribuer les entités de la table hello sur plusieurs nœuds de stockage.</span><span class="sxs-lookup"><span data-stu-id="46f34-143">hello system uses `PartitionKey` tooautomatically distribute hello table's entities over many storage nodes.</span></span> <span data-ttu-id="46f34-144">Les entités avec hello même `PartitionKey` sont stockés sur hello même nœud.</span><span class="sxs-lookup"><span data-stu-id="46f34-144">Entities with hello same `PartitionKey` are stored on hello same node.</span></span> <span data-ttu-id="46f34-145">(Les opérations sur plusieurs entités stockées sur hello même nœud effectuer supérieure aux entités stockées sur différents nœuds.) Hello `RowKey` est hello des ID unique d’une entité dans une partition.</span><span class="sxs-lookup"><span data-stu-id="46f34-145">(Operations on multiple entities stored on hello same node perform better than on entities stored across different nodes.) hello `RowKey` is hello unique ID of an entity within a partition.</span></span>

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

<span data-ttu-id="46f34-146">Pour plus d’informations sur les propriétés de la Table et de types, consultez [hello de présentation des modèle de données de Service de Table][table-data-model].</span><span class="sxs-lookup"><span data-stu-id="46f34-146">For information about Table properties and types, see [Understanding hello Table Service Data Model][table-data-model].</span></span>

<span data-ttu-id="46f34-147">Hello **TableRestProxy** classe offre deux méthodes alternatives pour l’insertion d’entités : **insertOrMergeEntity** et **insertOrReplaceEntity**.</span><span class="sxs-lookup"><span data-stu-id="46f34-147">hello **TableRestProxy** class offers two alternative methods for inserting entities: **insertOrMergeEntity** and **insertOrReplaceEntity**.</span></span> <span data-ttu-id="46f34-148">toouse ces méthodes, créez un **entité** et passez-le en tant que paramètre tooeither méthode.</span><span class="sxs-lookup"><span data-stu-id="46f34-148">toouse these methods, create a new **Entity** and pass it as a parameter tooeither method.</span></span> <span data-ttu-id="46f34-149">Chaque méthode insère l’entité de hello s’il n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="46f34-149">Each method will insert hello entity if it does not exist.</span></span> <span data-ttu-id="46f34-150">Si l’entité de hello existe déjà, **insertOrMergeEntity** met à jour les valeurs de propriété si les propriétés hello existent déjà et ajoute les nouvelles propriétés s’ils n’existent pas, alors que **insertOrReplaceEntity** complètement remplace une entité existante.</span><span class="sxs-lookup"><span data-stu-id="46f34-150">If hello entity already exists, **insertOrMergeEntity** updates property values if hello properties already exist and adds new properties if they do not exist, while **insertOrReplaceEntity** completely replaces an existing entity.</span></span> <span data-ttu-id="46f34-151">Hello suivant montre l’exemple de comment toouse **insertOrMergeEntity**.</span><span class="sxs-lookup"><span data-stu-id="46f34-151">hello following example shows how toouse **insertOrMergeEntity**.</span></span> <span data-ttu-id="46f34-152">Si hello entité avec `PartitionKey` « tasksSeattle » et `RowKey` « 1 » n’existe pas déjà, il sera inséré.</span><span class="sxs-lookup"><span data-stu-id="46f34-152">If hello entity with `PartitionKey` "tasksSeattle" and `RowKey` "1" does not already exist, it will be inserted.</span></span> <span data-ttu-id="46f34-153">Toutefois, s’il a été inséré précédemment (comme indiqué dans l’exemple hello ci-dessus), hello `DueDate` propriété sera mise à jour et hello `Status` propriété sera ajoutée.</span><span class="sxs-lookup"><span data-stu-id="46f34-153">However, if it has previously been inserted (as shown in hello example above), hello `DueDate` property will be updated, and hello `Status` property will be added.</span></span> <span data-ttu-id="46f34-154">Hello `Description` et `Location` sont également mises à jour, mais avec des valeurs qui efficacement les laisser inchangés.</span><span class="sxs-lookup"><span data-stu-id="46f34-154">hello `Description` and `Location` properties are also updated, but with values that effectively leave them unchanged.</span></span> <span data-ttu-id="46f34-155">Si ces deux dernières propriétés ont été pas ajoutées comme indiqué dans l’exemple de hello, mais se trouvait sur l’entité cible hello, leurs valeurs existantes reste inchangées.</span><span class="sxs-lookup"><span data-stu-id="46f34-155">If these latter two properties were not added as shown in hello example, but existed on hello target entity, their existing values would remain unchanged.</span></span>

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

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="46f34-156">Extraction d'une seule entité</span><span class="sxs-lookup"><span data-stu-id="46f34-156">Retrieve a single entity</span></span>
<span data-ttu-id="46f34-157">Hello **TableRestProxy -> getEntity** méthode vous permet de tooretrieve une seule entité en recherchant son `PartitionKey` et `RowKey`.</span><span class="sxs-lookup"><span data-stu-id="46f34-157">hello **TableRestProxy->getEntity** method allows you tooretrieve a single entity by querying for its `PartitionKey` and `RowKey`.</span></span> <span data-ttu-id="46f34-158">Dans l’exemple hello ci-dessous, hello clé de partition `tasksSeattle` et clé de ligne `1` sont passés toohello **getEntity** (méthode).</span><span class="sxs-lookup"><span data-stu-id="46f34-158">In hello example below, hello partition key `tasksSeattle` and row key `1` are passed toohello **getEntity** method.</span></span>

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

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="46f34-159">Extraction de toutes les entités d'une partition</span><span class="sxs-lookup"><span data-stu-id="46f34-159">Retrieve all entities in a partition</span></span>
<span data-ttu-id="46f34-160">Les requêtes d’entité sont construites à l’aide de filtres (pour plus d’informations, consultez la page [Interrogation de tables et d’entités][filters]).</span><span class="sxs-lookup"><span data-stu-id="46f34-160">Entity queries are constructed using filters (for more information, see [Querying Tables and Entities][filters]).</span></span> <span data-ttu-id="46f34-161">tooretrieve toutes les entités dans la partition, utilisez les filtre hello » PartitionKey eq *nom_partition*».</span><span class="sxs-lookup"><span data-stu-id="46f34-161">tooretrieve all entities in partition, use hello filter "PartitionKey eq *partition_name*".</span></span> <span data-ttu-id="46f34-162">Hello suivant montre l’exemple de comment tooretrieve toutes les entités de hello `tasksSeattle` partition en passant un filtre toohello **queryEntities** (méthode).</span><span class="sxs-lookup"><span data-stu-id="46f34-162">hello following example shows how tooretrieve all entities in hello `tasksSeattle` partition by passing a filter toohello **queryEntities** method.</span></span>

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

## <a name="retrieve-a-subset-of-entities-in-a-partition"></a><span data-ttu-id="46f34-163">Extraction d'un sous-ensemble d'entités dans une partition</span><span class="sxs-lookup"><span data-stu-id="46f34-163">Retrieve a subset of entities in a partition</span></span>
<span data-ttu-id="46f34-164">Hello même modèle utilisé dans l’exemple précédent de hello peut être utilisé tooretrieve n’importe quel sous-ensemble d’entités dans une partition.</span><span class="sxs-lookup"><span data-stu-id="46f34-164">hello same pattern used in hello previous example can be used tooretrieve any subset of entities in a partition.</span></span> <span data-ttu-id="46f34-165">sous-ensemble Hello d’entités que vous récupérez sont déterminées par le filtre hello (pour plus d’informations, consultez [interrogeant les Tables et les entités][filters]) .hello suivant montre l’exemple de comment toouse un tooretrieve de filtre toutes les entités avec un spécifique `Location` et un `DueDate` inférieur à une date spécifiée.</span><span class="sxs-lookup"><span data-stu-id="46f34-165">hello subset of entities you retrieve are determined by hello filter you use (for more information, see [Querying Tables and Entities][filters]).hello following example shows how toouse a filter tooretrieve all entities with a specific `Location` and a `DueDate` less than a specified date.</span></span>

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

## <a name="retrieve-a-subset-of-entity-properties"></a><span data-ttu-id="46f34-166">Extraction d'un sous-ensemble de propriétés d'entité</span><span class="sxs-lookup"><span data-stu-id="46f34-166">Retrieve a subset of entity properties</span></span>
<span data-ttu-id="46f34-167">Une requête peut extraire un sous-ensemble de propriétés d'entité.</span><span class="sxs-lookup"><span data-stu-id="46f34-167">A query can retrieve a subset of entity properties.</span></span> <span data-ttu-id="46f34-168">Cette technique, nommée *projection*, réduit la consommation de bande passante et peut améliorer les performances des requêtes, notamment pour les entités volumineuses.</span><span class="sxs-lookup"><span data-stu-id="46f34-168">This technique, called *projection*, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="46f34-169">de récupérer une propriété toobe toospecify, passez nom hello de hello propriété toohello **requête -> addSelectField** (méthode).</span><span class="sxs-lookup"><span data-stu-id="46f34-169">toospecify a property toobe retrieved, pass hello name of hello property toohello **Query->addSelectField** method.</span></span> <span data-ttu-id="46f34-170">Vous pouvez appeler cette méthode plusieurs fois tooadd plus de propriétés.</span><span class="sxs-lookup"><span data-stu-id="46f34-170">You can call this method multiple times tooadd more properties.</span></span> <span data-ttu-id="46f34-171">Après l’exécution de **TableRestProxy -> queryEntities**, hello retourné entités ont uniquement des propriétés de hello sélectionné.</span><span class="sxs-lookup"><span data-stu-id="46f34-171">After executing **TableRestProxy->queryEntities**, hello returned entities will only have hello selected properties.</span></span> <span data-ttu-id="46f34-172">(Si vous voulez tooreturn un sous-ensemble d’entités de Table, utilisez un filtre comme indiqué dans les requêtes hello ci-dessus.)</span><span class="sxs-lookup"><span data-stu-id="46f34-172">(If you want tooreturn a subset of Table entities, use a filter as shown in hello queries above.)</span></span>

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

## <a name="update-an-entity"></a><span data-ttu-id="46f34-173">Mise à jour d'une entité</span><span class="sxs-lookup"><span data-stu-id="46f34-173">Update an entity</span></span>
<span data-ttu-id="46f34-174">Une entité existante peut être mis à jour à l’aide de hello **entité -> setProperty** et **entité -> addProperty** méthodes sur l’entité de hello et en appelant **TableRestProxy -> updateEntity** .</span><span class="sxs-lookup"><span data-stu-id="46f34-174">An existing entity can be updated by using hello **Entity->setProperty** and **Entity->addProperty** methods on hello entity, and then calling **TableRestProxy->updateEntity**.</span></span> <span data-ttu-id="46f34-175">Hello exemple suivant récupère une entité, modifie une propriété, supprime une autre propriété et ajoute une nouvelle propriété.</span><span class="sxs-lookup"><span data-stu-id="46f34-175">hello following example retrieves an entity, modifies one property, removes another property, and adds a new property.</span></span> <span data-ttu-id="46f34-176">Notez que vous pouvez supprimer une propriété en définissant sa valeur trop**null**.</span><span class="sxs-lookup"><span data-stu-id="46f34-176">Note that you can remove a property by setting its value too**null**.</span></span>

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

## <a name="delete-an-entity"></a><span data-ttu-id="46f34-177">Suppression d’une entité</span><span class="sxs-lookup"><span data-stu-id="46f34-177">Delete an entity</span></span>
<span data-ttu-id="46f34-178">toodelete une entité, passez le nom de la table hello et l’entité hello `PartitionKey` et `RowKey` toohello **TableRestProxy -> deleteEntity** (méthode).</span><span class="sxs-lookup"><span data-stu-id="46f34-178">toodelete an entity, pass hello table name, and hello entity's `PartitionKey` and `RowKey` toohello **TableRestProxy->deleteEntity** method.</span></span>

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

<span data-ttu-id="46f34-179">Notez que pour les contrôles d’accès concurrentiel, vous pouvez définir hello Etag pour une toobe entité supprimée à l’aide de hello **DeleteEntityOptions -> setEtag** méthode et en passant hello **DeleteEntityOptions** trop de l’objet**deleteEntity** en tant que quatrième paramètre.</span><span class="sxs-lookup"><span data-stu-id="46f34-179">Note that for concurrency checks, you can set hello Etag for an entity toobe deleted by using hello **DeleteEntityOptions->setEtag** method and passing hello **DeleteEntityOptions** object too**deleteEntity** as a fourth parameter.</span></span>

## <a name="batch-table-operations"></a><span data-ttu-id="46f34-180">Traitement par lots d'opérations de table</span><span class="sxs-lookup"><span data-stu-id="46f34-180">Batch table operations</span></span>
<span data-ttu-id="46f34-181">Hello **TableRestProxy -> traitement par lots** méthode vous permet de tooexecute plusieurs opérations dans une demande unique.</span><span class="sxs-lookup"><span data-stu-id="46f34-181">hello **TableRestProxy->batch** method allows you tooexecute multiple operations in a single request.</span></span> <span data-ttu-id="46f34-182">Hello modèle implique l’ajout des opérations trop**BatchRequest** objet et à passer hello **BatchRequest** objet toohello **TableRestProxy -> traitement par lots** (méthode).</span><span class="sxs-lookup"><span data-stu-id="46f34-182">hello pattern here involves adding operations too**BatchRequest** object and then passing hello **BatchRequest** object toohello **TableRestProxy->batch** method.</span></span> <span data-ttu-id="46f34-183">tooadd une opération de tooa **BatchRequest** de l’objet, vous pouvez appeler les hello plusieurs fois de méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="46f34-183">tooadd an operation tooa **BatchRequest** object, you can call any of hello following methods multiple times:</span></span>

* <span data-ttu-id="46f34-184">**addInsertEntity** (permet d'ajouter une opération insertEntity)</span><span class="sxs-lookup"><span data-stu-id="46f34-184">**addInsertEntity** (adds an insertEntity operation)</span></span>
* <span data-ttu-id="46f34-185">**addUpdateEntity** (permet d'ajouter une opération updateEntity)</span><span class="sxs-lookup"><span data-stu-id="46f34-185">**addUpdateEntity** (adds an updateEntity operation)</span></span>
* <span data-ttu-id="46f34-186">**addMergeEntity** (permet d'ajouter une opération mergeEntity)</span><span class="sxs-lookup"><span data-stu-id="46f34-186">**addMergeEntity** (adds a mergeEntity operation)</span></span>
* <span data-ttu-id="46f34-187">**addInsertOrReplaceEntity** (permet d'ajouter une opération insertOrReplaceEntity)</span><span class="sxs-lookup"><span data-stu-id="46f34-187">**addInsertOrReplaceEntity** (adds an insertOrReplaceEntity operation)</span></span>
* <span data-ttu-id="46f34-188">**addInsertOrMergeEntity** (permet d'ajouter une opération insertOrMergeEntity)</span><span class="sxs-lookup"><span data-stu-id="46f34-188">**addInsertOrMergeEntity** (adds an insertOrMergeEntity operation)</span></span>
* <span data-ttu-id="46f34-189">**addDeleteEntity** (permet d'ajouter une opération deleteEntity)</span><span class="sxs-lookup"><span data-stu-id="46f34-189">**addDeleteEntity** (adds a deleteEntity operation)</span></span>

<span data-ttu-id="46f34-190">Hello suivant montre l’exemple de comment tooexecute **insertEntity** et **deleteEntity** opérations dans une demande unique :</span><span class="sxs-lookup"><span data-stu-id="46f34-190">hello following example shows how tooexecute **insertEntity** and **deleteEntity** operations in a single request:</span></span>

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

<span data-ttu-id="46f34-191">Pour plus d’informations sur le traitement par lots d’opérations de table, consultez la page [Exécution de transactions de groupe d’entités][entity-group-transactions].</span><span class="sxs-lookup"><span data-stu-id="46f34-191">For more information about batching Table operations, see [Performing Entity Group Transactions][entity-group-transactions].</span></span>

## <a name="delete-a-table"></a><span data-ttu-id="46f34-192">Suppression d’une table</span><span class="sxs-lookup"><span data-stu-id="46f34-192">Delete a table</span></span>
<span data-ttu-id="46f34-193">Enfin, toodelete une table, passer toohello de nom de table hello **TableRestProxy -> deleteTable** (méthode).</span><span class="sxs-lookup"><span data-stu-id="46f34-193">Finally, toodelete a table, pass hello table name toohello **TableRestProxy->deleteTable** method.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="46f34-194">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="46f34-194">Next steps</span></span>
<span data-ttu-id="46f34-195">Maintenant que vous avez appris les notions de base de hello Hello service Table Azure, suivez ces toolearn des liens sur les tâches de stockage plus complexes.</span><span class="sxs-lookup"><span data-stu-id="46f34-195">Now that you've learned hello basics of hello Azure Table service, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="46f34-196">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) est une application autonome gratuit, à partir de Microsoft qui vous permet de toowork visuellement avec des données de stockage Azure sur Windows, Mac OS et Linux.</span><span class="sxs-lookup"><span data-stu-id="46f34-196">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

* <span data-ttu-id="46f34-197">[Centre de développement PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="46f34-197">[PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://php.net/require_once
[table-service-timeouts]: http://msdn.microsoft.com/library/azure/dd894042.aspx

[table-data-model]: http://msdn.microsoft.com/library/azure/dd179338.aspx
[filters]: http://msdn.microsoft.com/library/azure/dd894031.aspx
[entity-group-transactions]: http://msdn.microsoft.com/library/azure/dd894038.aspx
