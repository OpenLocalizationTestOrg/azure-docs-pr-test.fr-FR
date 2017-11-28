---
title: "Utilisation du stockage Table à partir de PHP | Microsoft Docs"
description: "Découvrez comment utiliser le service de Table de PHP pour créer, supprimer, insérer et interroger une table."
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
ms.openlocfilehash: 15d3216ef5bb1d7ff312bd886837a3a7b0335afd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-table-storage-from-php"></a><span data-ttu-id="70af1-103">Utilisation du stockage de tables à partir de PHP</span><span class="sxs-lookup"><span data-stu-id="70af1-103">How to use table storage from PHP</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="70af1-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="70af1-104">Overview</span></span>
<span data-ttu-id="70af1-105">Ce guide décrit le déroulement de scénarios courants dans le cadre de l'utilisation du service de tables Azure.</span><span class="sxs-lookup"><span data-stu-id="70af1-105">This guide shows you how to perform common scenarios using the Azure Table service.</span></span> <span data-ttu-id="70af1-106">Les exemples sont écrits en PHP et utilisent le [kit SDK Azure pour PHP][download].</span><span class="sxs-lookup"><span data-stu-id="70af1-106">The samples are written in PHP and use the [Azure SDK for PHP][download].</span></span> <span data-ttu-id="70af1-107">Les scénarios traités incluent la **création et la suppression d'une table, l'insertion, la suppression et l'interrogation d'entités dans une table**.</span><span class="sxs-lookup"><span data-stu-id="70af1-107">The scenarios covered include **creating and deleting a table, and inserting, deleting, and querying entities in a table**.</span></span> <span data-ttu-id="70af1-108">Pour plus d'informations sur le service de Table Azure, consultez la section [Étapes suivantes](#next-steps) .</span><span class="sxs-lookup"><span data-stu-id="70af1-108">For more information on the Azure Table service, see the [Next steps](#next-steps) section.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="70af1-109">Création d'une application PHP</span><span class="sxs-lookup"><span data-stu-id="70af1-109">Create a PHP application</span></span>
<span data-ttu-id="70af1-110">La référence de classes dans le kit SDK Azure pour PHP constitue la seule exigence pour créer une application PHP qui accède au service de Table Azure.</span><span class="sxs-lookup"><span data-stu-id="70af1-110">The only requirement for creating a PHP application that accesses the Azure Table service is the referencing of classes in the Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="70af1-111">Vous pouvez utiliser tous les outils de développement pour créer votre application, y compris Bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="70af1-111">You can use any development tools to create your application, including Notepad.</span></span>

<span data-ttu-id="70af1-112">Dans ce guide, vous utilisez les fonctionnalités du service de Table qui peuvent être appelées dans une application PHP en local, ou dans le code s'exécutant dans un rôle web, un rôle de travail ou un site web Azure.</span><span class="sxs-lookup"><span data-stu-id="70af1-112">In this guide, you use Table service features which can be called from within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-the-azure-client-libraries"></a><span data-ttu-id="70af1-113">Obtention des bibliothèques clientes Azure</span><span class="sxs-lookup"><span data-stu-id="70af1-113">Get the Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-access-the-table-service"></a><span data-ttu-id="70af1-114">Configuration de votre application pour accéder au service de Table</span><span class="sxs-lookup"><span data-stu-id="70af1-114">Configure your application to access the Table service</span></span>
<span data-ttu-id="70af1-115">Pour utiliser les API du service de Table Azure, vous devez procéder comme suit :</span><span class="sxs-lookup"><span data-stu-id="70af1-115">To use the Azure Table service APIs, you need to:</span></span>

1. <span data-ttu-id="70af1-116">référencer le fichier de chargeur automatique à l’aide de l’instruction [require_once][require_once] ; et</span><span class="sxs-lookup"><span data-stu-id="70af1-116">Reference the autoloader file using the [require_once][require_once] statement, and</span></span>
2. <span data-ttu-id="70af1-117">référencer toute classe que vous êtes susceptible d'utiliser.</span><span class="sxs-lookup"><span data-stu-id="70af1-117">Reference any classes you might use.</span></span>

<span data-ttu-id="70af1-118">L'exemple suivant montre comment inclure le fichier du chargeur automatique et référencer la classe **ServicesBuilder** .</span><span class="sxs-lookup"><span data-stu-id="70af1-118">The following example shows how to include the autoloader file and reference the **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="70af1-119">Les exemples de cet article partent du principe que vous avez installé les bibliothèques clientes PHP pour Azure via Composer.</span><span class="sxs-lookup"><span data-stu-id="70af1-119">The examples in this article assume you have installed the PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="70af1-120">Si vous avez installé les bibliothèques manuellement, vous devez référencer le fichier de chargeur automatique <code>WindowsAzure.php</code> .</span><span class="sxs-lookup"><span data-stu-id="70af1-120">If you installed the libraries manually, you need to reference the <code>WindowsAzure.php</code> autoloader file.</span></span>
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="70af1-121">Dans les exemples ci-dessous, l'instruction `require_once` s'affiche toujours, mais seules les classes nécessaires aux besoins de l'exemple à exécuter sont référencées.</span><span class="sxs-lookup"><span data-stu-id="70af1-121">In the examples below, the `require_once` statement is always shown, but only the classes necessary for the example to execute are referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="70af1-122">Configuration d’une connexion de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="70af1-122">Set up an Azure storage connection</span></span>
<span data-ttu-id="70af1-123">Pour instancier un client de service de Table Azure, vous devez disposer au préalable d'une chaîne de connexion valide.</span><span class="sxs-lookup"><span data-stu-id="70af1-123">To instantiate an Azure Table service client, you must first have a valid connection string.</span></span> <span data-ttu-id="70af1-124">Le format de la chaîne de connexion du service de Table est le suivant :</span><span class="sxs-lookup"><span data-stu-id="70af1-124">The format for the Table service connection string is:</span></span>

<span data-ttu-id="70af1-125">Pour accéder à un service en ligne :</span><span class="sxs-lookup"><span data-stu-id="70af1-125">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="70af1-126">Pour accéder au stockage de l’émulateur :</span><span class="sxs-lookup"><span data-stu-id="70af1-126">For accessing the emulator storage:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="70af1-127">Pour créer un client de service Azure, vous devez utiliser la classe **ServicesBuilder** .</span><span class="sxs-lookup"><span data-stu-id="70af1-127">To create any Azure service client, you need to use the **ServicesBuilder** class.</span></span> <span data-ttu-id="70af1-128">Vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="70af1-128">You can:</span></span>

* <span data-ttu-id="70af1-129">lui passer directement la chaîne de connexion ; ou</span><span class="sxs-lookup"><span data-stu-id="70af1-129">pass the connection string directly to it or</span></span>
* <span data-ttu-id="70af1-130">utiliser **CloudConfigurationManager (CCM)** pour vérifier plusieurs sources externes pour la chaîne de connexion :</span><span class="sxs-lookup"><span data-stu-id="70af1-130">use the **CloudConfigurationManager (CCM)** to check multiple external sources for the connection string:</span></span>
  * <span data-ttu-id="70af1-131">Par défaut, il prend en charge une source externe : les variables d’environnement.</span><span class="sxs-lookup"><span data-stu-id="70af1-131">by default, it comes with support for one external source - environmental variables</span></span>
  * <span data-ttu-id="70af1-132">de nouvelles sources peuvent être ajoutées via une extension de la classe **ConnectionStringSource** .</span><span class="sxs-lookup"><span data-stu-id="70af1-132">you can add new sources by extending the **ConnectionStringSource** class</span></span>

<span data-ttu-id="70af1-133">Dans les exemples ci-dessous, la chaîne de connexion est passée directement.</span><span class="sxs-lookup"><span data-stu-id="70af1-133">For the examples outlined here, the connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);
```

## <a name="create-a-table"></a><span data-ttu-id="70af1-134">Création d’une table</span><span class="sxs-lookup"><span data-stu-id="70af1-134">Create a table</span></span>
<span data-ttu-id="70af1-135">Vous pouvez créer une table avec un objet **TableRestProxy** via la méthode **createTable**.</span><span class="sxs-lookup"><span data-stu-id="70af1-135">A **TableRestProxy** object lets you create a table with the **createTable** method.</span></span> <span data-ttu-id="70af1-136">Au moment de créer une table, vous pouvez définir le délai d'expiration du service de Table.</span><span class="sxs-lookup"><span data-stu-id="70af1-136">When creating a table, you can set the Table service timeout.</span></span> <span data-ttu-id="70af1-137">(Pour plus d’informations sur le délai d’expiration du service de Table, consultez [Définition de délais d’expiration pour les opérations du service de Table][table-service-timeouts].)</span><span class="sxs-lookup"><span data-stu-id="70af1-137">(For more information about the Table service timeout, see [Setting Timeouts for Table Service Operations][table-service-timeouts].)</span></span>

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

<span data-ttu-id="70af1-138">Pour plus d’informations sur les restrictions au niveau des noms de table, consultez [Présentation du modèle de données du service de Table][table-data-model].</span><span class="sxs-lookup"><span data-stu-id="70af1-138">For information about restrictions on table names, see [Understanding the Table Service Data Model][table-data-model].</span></span>

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="70af1-139">Ajout d'une entité à une table</span><span class="sxs-lookup"><span data-stu-id="70af1-139">Add an entity to a table</span></span>
<span data-ttu-id="70af1-140">Pour ajouter une entité à une table, créez un objet **Entity** et transmettez-le à **TableRestProxy->insertEntity**.</span><span class="sxs-lookup"><span data-stu-id="70af1-140">To add an entity to a table, create a new **Entity** object and pass it to **TableRestProxy->insertEntity**.</span></span> <span data-ttu-id="70af1-141">Notez que lorsque vous créez une entité, vous devez spécifier une clé `PartitionKey` et `RowKey`.</span><span class="sxs-lookup"><span data-stu-id="70af1-141">Note that when you create an entity, you must specify a `PartitionKey` and `RowKey`.</span></span> <span data-ttu-id="70af1-142">Il s’agit des identificateurs uniques d’une entité, dont les valeurs peuvent être interrogées bien plus rapidement que les autres propriétés d’entité.</span><span class="sxs-lookup"><span data-stu-id="70af1-142">These are the unique identifiers for an entity and are values that can be queried much faster than other entity properties.</span></span> <span data-ttu-id="70af1-143">Le système utilise `PartitionKey` pour distribuer automatiquement les entités de la table sur plusieurs nœuds de stockage.</span><span class="sxs-lookup"><span data-stu-id="70af1-143">The system uses `PartitionKey` to automatically distribute the table's entities over many storage nodes.</span></span> <span data-ttu-id="70af1-144">Les entités partageant la même clé `PartitionKey` sont stockées sur le même nœud.</span><span class="sxs-lookup"><span data-stu-id="70af1-144">Entities with the same `PartitionKey` are stored on the same node.</span></span> <span data-ttu-id="70af1-145">(Les opérations réalisées sur plusieurs entités offrent de meilleures performances lorsque ces entités sont stockées sur un même nœud plutôt que sur différents nœuds.) La clé `RowKey` est l’ID unique d’une entité au sein d’une partition.</span><span class="sxs-lookup"><span data-stu-id="70af1-145">(Operations on multiple entities stored on the same node perform better than on entities stored across different nodes.) The `RowKey` is the unique ID of an entity within a partition.</span></span>

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
$entity->addProperty("Description", null, "Take out the trash.");
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

<span data-ttu-id="70af1-146">Pour plus d’informations sur les propriétés et les types de table, consultez la page [Présentation du modèle de données du service de Table][table-data-model].</span><span class="sxs-lookup"><span data-stu-id="70af1-146">For information about Table properties and types, see [Understanding the Table Service Data Model][table-data-model].</span></span>

<span data-ttu-id="70af1-147">La classe **TableRestProxy** offre deux autres méthodes pour insérer des entités : **insertOrMergeEntity** et **insertOrReplaceEntity**.</span><span class="sxs-lookup"><span data-stu-id="70af1-147">The **TableRestProxy** class offers two alternative methods for inserting entities: **insertOrMergeEntity** and **insertOrReplaceEntity**.</span></span> <span data-ttu-id="70af1-148">Pour utiliser ces méthodes, créez un objet **Entity** et transmettez-le en tant que paramètre à l'une ou l'autre des méthodes.</span><span class="sxs-lookup"><span data-stu-id="70af1-148">To use these methods, create a new **Entity** and pass it as a parameter to either method.</span></span> <span data-ttu-id="70af1-149">Chaque méthode insère l'entité si elle n'existe pas.</span><span class="sxs-lookup"><span data-stu-id="70af1-149">Each method will insert the entity if it does not exist.</span></span> <span data-ttu-id="70af1-150">Si l’entité existe déjà, **insertOrMergeEntity** met à jour la valeur des propriétés si celles-ci existent déjà et en ajoute de nouvelles dans le cas contraire, alors que **insertOrReplaceEntity** remplace entièrement une entité existante.</span><span class="sxs-lookup"><span data-stu-id="70af1-150">If the entity already exists, **insertOrMergeEntity** updates property values if the properties already exist and adds new properties if they do not exist, while **insertOrReplaceEntity** completely replaces an existing entity.</span></span> <span data-ttu-id="70af1-151">L'exemple suivant montre comment utiliser **insertOrMergeEntity**.</span><span class="sxs-lookup"><span data-stu-id="70af1-151">The following example shows how to use **insertOrMergeEntity**.</span></span> <span data-ttu-id="70af1-152">Si l’entité associée à la clé `PartitionKey` « tasksSeattle » et à la clé `RowKey` « 1 » n’existe pas déjà, elle est insérée.</span><span class="sxs-lookup"><span data-stu-id="70af1-152">If the entity with `PartitionKey` "tasksSeattle" and `RowKey` "1" does not already exist, it will be inserted.</span></span> <span data-ttu-id="70af1-153">En revanche, si elle a été ajoutée précédemment (comme indiqué dans l’exemple précédent), la propriété `DueDate` est mise à jour et la propriété `Status` est ajoutée.</span><span class="sxs-lookup"><span data-stu-id="70af1-153">However, if it has previously been inserted (as shown in the example above), the `DueDate` property will be updated, and the `Status` property will be added.</span></span> <span data-ttu-id="70af1-154">Les propriétés `Description` et `Location` sont également mises à jour, mais avec des valeurs qui de fait les laissent inchangées.</span><span class="sxs-lookup"><span data-stu-id="70af1-154">The `Description` and `Location` properties are also updated, but with values that effectively leave them unchanged.</span></span> <span data-ttu-id="70af1-155">Si ces deux dernières propriétés n'ont pas été ajoutées comme indiqué dans l'exemple, mais qu'elles existaient sur l'entité cible, leurs valeurs existantes restent inchangées.</span><span class="sxs-lookup"><span data-stu-id="70af1-155">If these latter two properties were not added as shown in the example, but existed on the target entity, their existing values would remain unchanged.</span></span>

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
$entity->addProperty("Description", null, "Take out the trash.");
$entity->addProperty("DueDate", EdmType::DATETIME, new DateTime()); // Modified the DueDate field.
$entity->addProperty("Location", EdmType::STRING, "Home");
$entity->addProperty("Status", EdmType::STRING, "Complete"); // Added Status field.

try    {
    // Calling insertOrReplaceEntity, instead of insertOrMergeEntity as shown,
    // would simply replace the entity with PartitionKey "tasksSeattle" and RowKey "1".
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

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="70af1-156">Extraction d'une seule entité</span><span class="sxs-lookup"><span data-stu-id="70af1-156">Retrieve a single entity</span></span>
<span data-ttu-id="70af1-157">La méthode **TableRestProxy->getEntity** vous permet de récupérer une seule entité via une requête portant sur ses clés `PartitionKey` et `RowKey`.</span><span class="sxs-lookup"><span data-stu-id="70af1-157">The **TableRestProxy->getEntity** method allows you to retrieve a single entity by querying for its `PartitionKey` and `RowKey`.</span></span> <span data-ttu-id="70af1-158">Dans l’exemple ci-dessous, la clé de partition `tasksSeattle` et la clé de ligne `1` sont transmises à la méthode **getEntity**.</span><span class="sxs-lookup"><span data-stu-id="70af1-158">In the example below, the partition key `tasksSeattle` and row key `1` are passed to the **getEntity** method.</span></span>

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

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="70af1-159">Extraction de toutes les entités d'une partition</span><span class="sxs-lookup"><span data-stu-id="70af1-159">Retrieve all entities in a partition</span></span>
<span data-ttu-id="70af1-160">Les requêtes d’entité sont construites à l’aide de filtres (pour plus d’informations, consultez la page [Interrogation de tables et d’entités][filters]).</span><span class="sxs-lookup"><span data-stu-id="70af1-160">Entity queries are constructed using filters (for more information, see [Querying Tables and Entities][filters]).</span></span> <span data-ttu-id="70af1-161">Pour extraire toutes les entités d’une partition, utilisez le filtre « PartitionKey eq *nom_partition* ».</span><span class="sxs-lookup"><span data-stu-id="70af1-161">To retrieve all entities in partition, use the filter "PartitionKey eq *partition_name*".</span></span> <span data-ttu-id="70af1-162">L’exemple suivant montre comment récupérer toutes les entités de la partition `tasksSeattle` en passant un filtre à la méthode **queryEntities** .</span><span class="sxs-lookup"><span data-stu-id="70af1-162">The following example shows how to retrieve all entities in the `tasksSeattle` partition by passing a filter to the **queryEntities** method.</span></span>

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

## <a name="retrieve-a-subset-of-entities-in-a-partition"></a><span data-ttu-id="70af1-163">Extraction d'un sous-ensemble d'entités dans une partition</span><span class="sxs-lookup"><span data-stu-id="70af1-163">Retrieve a subset of entities in a partition</span></span>
<span data-ttu-id="70af1-164">Pour extraire un sous-ensemble d'entités dans une partition, il est possible d'utiliser le modèle de l'exemple précédent.</span><span class="sxs-lookup"><span data-stu-id="70af1-164">The same pattern used in the previous example can be used to retrieve any subset of entities in a partition.</span></span> <span data-ttu-id="70af1-165">Le sous-ensemble d’entités extrait varie en fonction du filtre utilisé (pour plus d’informations, consultez la page [Interrogation de tables et d’entités][filters]). L’exemple suivant montre comment utiliser un filtre pour extraire toutes les entités avec une valeur `Location` spécifique et une valeur `DueDate` antérieure à une date spécifiée.</span><span class="sxs-lookup"><span data-stu-id="70af1-165">The subset of entities you retrieve are determined by the filter you use (for more information, see [Querying Tables and Entities][filters]).The following example shows how to use a filter to retrieve all entities with a specific `Location` and a `DueDate` less than a specified date.</span></span>

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

## <a name="retrieve-a-subset-of-entity-properties"></a><span data-ttu-id="70af1-166">Extraction d'un sous-ensemble de propriétés d'entité</span><span class="sxs-lookup"><span data-stu-id="70af1-166">Retrieve a subset of entity properties</span></span>
<span data-ttu-id="70af1-167">Une requête peut extraire un sous-ensemble de propriétés d'entité.</span><span class="sxs-lookup"><span data-stu-id="70af1-167">A query can retrieve a subset of entity properties.</span></span> <span data-ttu-id="70af1-168">Cette technique, nommée *projection*, réduit la consommation de bande passante et peut améliorer les performances des requêtes, notamment pour les entités volumineuses.</span><span class="sxs-lookup"><span data-stu-id="70af1-168">This technique, called *projection*, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="70af1-169">Pour spécifier une propriété à extraire, transmettez son nom à la méthode **Query->addSelectField**.</span><span class="sxs-lookup"><span data-stu-id="70af1-169">To specify a property to be retrieved, pass the name of the property to the **Query->addSelectField** method.</span></span> <span data-ttu-id="70af1-170">Vous pouvez appeler cette méthode plusieurs fois pour ajouter des propriétés supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="70af1-170">You can call this method multiple times to add more properties.</span></span> <span data-ttu-id="70af1-171">Après avoir exécuté **TableRestProxy->queryEntities**, les entités renvoyées contiennent uniquement les propriétés sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="70af1-171">After executing **TableRestProxy->queryEntities**, the returned entities will only have the selected properties.</span></span> <span data-ttu-id="70af1-172">(si vous voulez renvoyer un sous-ensemble d'entités de table, utilisez un filtre comme indiqué dans les requêtes précédentes).</span><span class="sxs-lookup"><span data-stu-id="70af1-172">(If you want to return a subset of Table entities, use a filter as shown in the queries above.)</span></span>

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

// All entities in the table are returned, regardless of whether
// they have the Description field.
// To limit the results returned, use a filter.
$entities = $result->getEntities();

foreach($entities as $entity){
    $description = $entity->getProperty("Description")->getValue();
    echo $description."<br />";
}
```

## <a name="update-an-entity"></a><span data-ttu-id="70af1-173">Mise à jour d'une entité</span><span class="sxs-lookup"><span data-stu-id="70af1-173">Update an entity</span></span>
<span data-ttu-id="70af1-174">Une entité existante peut être mise à jour en lui appliquant les méthodes **Entity->setProperty** et **Entity->addProperty**, puis en appelant **TableRestProxy->updateEntity**.</span><span class="sxs-lookup"><span data-stu-id="70af1-174">An existing entity can be updated by using the **Entity->setProperty** and **Entity->addProperty** methods on the entity, and then calling **TableRestProxy->updateEntity**.</span></span> <span data-ttu-id="70af1-175">Dans l'exemple suivant, une entité est extraite, une propriété modifiée, une autre propriété supprimée et une nouvelle propriété ajoutée.</span><span class="sxs-lookup"><span data-stu-id="70af1-175">The following example retrieves an entity, modifies one property, removes another property, and adds a new property.</span></span> <span data-ttu-id="70af1-176">Notez que vous pouvez supprimer une propriété en lui attribuant la valeur **null**.</span><span class="sxs-lookup"><span data-stu-id="70af1-176">Note that you can remove a property by setting its value to **null**.</span></span>

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

## <a name="delete-an-entity"></a><span data-ttu-id="70af1-177">Suppression d'une entité</span><span class="sxs-lookup"><span data-stu-id="70af1-177">Delete an entity</span></span>
<span data-ttu-id="70af1-178">Pour supprimer une entité, passez le nom de la table ainsi que les clés `PartitionKey` et `RowKey` à la méthode **TableRestProxy->deleteEntity**.</span><span class="sxs-lookup"><span data-stu-id="70af1-178">To delete an entity, pass the table name, and the entity's `PartitionKey` and `RowKey` to the **TableRestProxy->deleteEntity** method.</span></span>

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

<span data-ttu-id="70af1-179">Notez que pour les contrôles d’accès concurrentiel, vous pouvez définir la suppression de la propriété Etag d’une entité en employant la méthode **DeleteEntityOptions->setEtag** et en transmettant l’objet **DeleteEntityOptions** à **deleteEntity** en tant que quatrième paramètre.</span><span class="sxs-lookup"><span data-stu-id="70af1-179">Note that for concurrency checks, you can set the Etag for an entity to be deleted by using the **DeleteEntityOptions->setEtag** method and passing the **DeleteEntityOptions** object to **deleteEntity** as a fourth parameter.</span></span>

## <a name="batch-table-operations"></a><span data-ttu-id="70af1-180">Traitement par lots d'opérations de table</span><span class="sxs-lookup"><span data-stu-id="70af1-180">Batch table operations</span></span>
<span data-ttu-id="70af1-181">La méthode **TableRestProxy->batch** permet d’exécuter plusieurs opérations dans une même demande.</span><span class="sxs-lookup"><span data-stu-id="70af1-181">The **TableRestProxy->batch** method allows you to execute multiple operations in a single request.</span></span> <span data-ttu-id="70af1-182">Ce modèle implique d’ajouter des opérations à l’objet **BatchRequest** et de transmettre **ce** dernier à la méthode **TableRestProxy->batch**.</span><span class="sxs-lookup"><span data-stu-id="70af1-182">The pattern here involves adding operations to **BatchRequest** object and then passing the **BatchRequest** object to the **TableRestProxy->batch** method.</span></span> <span data-ttu-id="70af1-183">Pour ajouter une opération à un objet **BatchRequest** , vous pouvez appeler l'une des méthodes suivantes à plusieurs reprises :</span><span class="sxs-lookup"><span data-stu-id="70af1-183">To add an operation to a **BatchRequest** object, you can call any of the following methods multiple times:</span></span>

* <span data-ttu-id="70af1-184">**addInsertEntity** (permet d'ajouter une opération insertEntity)</span><span class="sxs-lookup"><span data-stu-id="70af1-184">**addInsertEntity** (adds an insertEntity operation)</span></span>
* <span data-ttu-id="70af1-185">**addUpdateEntity** (permet d'ajouter une opération updateEntity)</span><span class="sxs-lookup"><span data-stu-id="70af1-185">**addUpdateEntity** (adds an updateEntity operation)</span></span>
* <span data-ttu-id="70af1-186">**addMergeEntity** (permet d'ajouter une opération mergeEntity)</span><span class="sxs-lookup"><span data-stu-id="70af1-186">**addMergeEntity** (adds a mergeEntity operation)</span></span>
* <span data-ttu-id="70af1-187">**addInsertOrReplaceEntity** (permet d'ajouter une opération insertOrReplaceEntity)</span><span class="sxs-lookup"><span data-stu-id="70af1-187">**addInsertOrReplaceEntity** (adds an insertOrReplaceEntity operation)</span></span>
* <span data-ttu-id="70af1-188">**addInsertOrMergeEntity** (permet d'ajouter une opération insertOrMergeEntity)</span><span class="sxs-lookup"><span data-stu-id="70af1-188">**addInsertOrMergeEntity** (adds an insertOrMergeEntity operation)</span></span>
* <span data-ttu-id="70af1-189">**addDeleteEntity** (permet d'ajouter une opération deleteEntity)</span><span class="sxs-lookup"><span data-stu-id="70af1-189">**addDeleteEntity** (adds a deleteEntity operation)</span></span>

<span data-ttu-id="70af1-190">L’exemple suivant montre comment exécuter des opérations **insertEntity** et **deleteEntity** dans une même demande :</span><span class="sxs-lookup"><span data-stu-id="70af1-190">The following example shows how to execute **insertEntity** and **deleteEntity** operations in a single request:</span></span>

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

// Add operation to list of batch operations.
$operations->addInsertEntity("mytable", $entity1);

// Add operation to list of batch operations.
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

<span data-ttu-id="70af1-191">Pour plus d’informations sur le traitement par lots d’opérations de table, consultez la page [Exécution de transactions de groupe d’entités][entity-group-transactions].</span><span class="sxs-lookup"><span data-stu-id="70af1-191">For more information about batching Table operations, see [Performing Entity Group Transactions][entity-group-transactions].</span></span>

## <a name="delete-a-table"></a><span data-ttu-id="70af1-192">Suppression d’une table</span><span class="sxs-lookup"><span data-stu-id="70af1-192">Delete a table</span></span>
<span data-ttu-id="70af1-193">Enfin, pour supprimer une table, transmettez son nom à la méthode **TableRestProxy->deleteTable**.</span><span class="sxs-lookup"><span data-stu-id="70af1-193">Finally, to delete a table, pass the table name to the **TableRestProxy->deleteTable** method.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="70af1-194">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="70af1-194">Next steps</span></span>
<span data-ttu-id="70af1-195">Maintenant que vous avez appris les principes de base du service Table Azure, consultez les liens suivants pour découvrir des tâches de stockage plus complexes.</span><span class="sxs-lookup"><span data-stu-id="70af1-195">Now that you've learned the basics of the Azure Table service, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="70af1-196">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) est une application autonome et gratuite de Microsoft qui vous permet d’exploiter visuellement les données de Stockage Azure sur Windows, macOS et Linux.</span><span class="sxs-lookup"><span data-stu-id="70af1-196">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

* <span data-ttu-id="70af1-197">[Centre de développement PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="70af1-197">[PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://php.net/require_once
[table-service-timeouts]: http://msdn.microsoft.com/library/azure/dd894042.aspx

[table-data-model]: http://msdn.microsoft.com/library/azure/dd179338.aspx
[filters]: http://msdn.microsoft.com/library/azure/dd894031.aspx
[entity-group-transactions]: http://msdn.microsoft.com/library/azure/dd894038.aspx
