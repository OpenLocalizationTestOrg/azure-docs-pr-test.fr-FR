---
title: Utilisation du stockage Table Azure avec Python | Microsoft Docs
description: "Stockez des données structurées dans le cloud à l’aide du stockage de tables Azure, un magasin de données NoSQL."
services: storage
documentationcenter: python
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 7ddb9f3e-4e6d-4103-96e6-f0351d69a17b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/16/2017
ms.author: marsma
ms.openlocfilehash: c310a52182bbc3cf44ed4dc6a04e97aa59200a64
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-table-storage-in-python"></a><span data-ttu-id="09b04-103">Utilisation du stockage de tables dans Python</span><span class="sxs-lookup"><span data-stu-id="09b04-103">How to use Table storage in Python</span></span>

[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

<span data-ttu-id="09b04-104">Ce guide vous montre comment traiter des scénarios courants de stockage de table Azure en Python à l’aide du [Kit de développement logiciel (SDK) Microsoft Azure Storage pour Python](https://github.com/Azure/azure-storage-python).</span><span class="sxs-lookup"><span data-stu-id="09b04-104">This guide shows you how to perform common Azure Table storage scenarios in Python using the [Microsoft Azure Storage SDK for Python](https://github.com/Azure/azure-storage-python).</span></span> <span data-ttu-id="09b04-105">Les scénarios traités incluent la création et la suppression d'une table, l'insertion et l'interrogation d'entités.</span><span class="sxs-lookup"><span data-stu-id="09b04-105">The scenarios covered include creating and deleting a table, and inserting and querying entities.</span></span>

<span data-ttu-id="09b04-106">Pendant que vous étudiez les scénarios de ce didacticiel, vous pouvez vous référer à la [Référence du kit de développement logiciel (SDK) Stockage Azure pour l’API Python](https://azure-storage.readthedocs.io/en/latest/index.html).</span><span class="sxs-lookup"><span data-stu-id="09b04-106">While working through the scenarios in this tutorial, you may wish to refer to the [Azure Storage SDK for Python API reference](https://azure-storage.readthedocs.io/en/latest/index.html).</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="install-the-azure-storage-sdk-for-python"></a><span data-ttu-id="09b04-107">Installation du kit de développement logiciel (SDK) Microsoft Azure Storage pour Python</span><span class="sxs-lookup"><span data-stu-id="09b04-107">Install the Azure Storage SDK for Python</span></span>

<span data-ttu-id="09b04-108">Une fois que vous avez créé un compte de stockage, l’étape suivante consiste à installer le [Kit de développement logiciel (SDK) Microsoft Azure Storage pour Python](https://github.com/Azure/azure-storage-python).</span><span class="sxs-lookup"><span data-stu-id="09b04-108">Once you've created a storage account, your next step is to install the [Microsoft Azure Storage SDK for Python](https://github.com/Azure/azure-storage-python).</span></span> <span data-ttu-id="09b04-109">Pour plus de détails sur l’installation du kit de développement logiciel, reportez-vous au fichier [README.rst](https://github.com/Azure/azure-storage-python/blob/master/README.rst) dans le kit de développement de stockage pour le référentiel de Python sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="09b04-109">For details on installing the SDK, refer to the [README.rst](https://github.com/Azure/azure-storage-python/blob/master/README.rst) file in the Storage SDK for Python repository on GitHub.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="09b04-110">Création d’une table</span><span class="sxs-lookup"><span data-stu-id="09b04-110">Create a table</span></span>

<span data-ttu-id="09b04-111">Pour travailler avec le service de table Azure dans Python, vous devez importer le module [TableService][py_TableService].</span><span class="sxs-lookup"><span data-stu-id="09b04-111">To work with the Azure Table service in Python, you must import the [TableService][py_TableService] module.</span></span> <span data-ttu-id="09b04-112">Comme vous allez travailler avec les entités de table, vous avez également besoin de la classe [entité][py_Entity].</span><span class="sxs-lookup"><span data-stu-id="09b04-112">Since you'll be working with Table entities, you also need the [Entity][py_Entity] class.</span></span> <span data-ttu-id="09b04-113">Ajoutez ce code vers le haut de votre fichier Python pour importer les deux :</span><span class="sxs-lookup"><span data-stu-id="09b04-113">Add this code near the top your Python file to import both:</span></span>

```python
from azure.storage.table import TableService, Entity
```

<span data-ttu-id="09b04-114">Créez un objet [TableService][py_TableService], en passant votre clé de compte et le nom du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="09b04-114">Create a [TableService][py_TableService] object, passing in your storage account name and account key.</span></span> <span data-ttu-id="09b04-115">Remplacez `myaccount` et `mykey` par votre nom de compte et votre clé, et appelez [create_table][py_create_table] pour créer la table dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="09b04-115">Replace `myaccount` and `mykey` with your account name and key, and call [create_table][py_create_table] to create the table in Azure Storage.</span></span>

```python
table_service = TableService(account_name='myaccount', account_key='mykey')

table_service.create_table('tasktable')
```

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="09b04-116">Ajout d'une entité à une table</span><span class="sxs-lookup"><span data-stu-id="09b04-116">Add an entity to a table</span></span>

<span data-ttu-id="09b04-117">Pour ajouter une entité, vous créez d’abord un objet qui représente votre entité, puis passez l’objet à la méthode [TableService][py_TableService].[insert_entity][py_insert_entity].</span><span class="sxs-lookup"><span data-stu-id="09b04-117">To add an entity, you first create an object that represents your entity, then pass the object to the [TableService][py_TableService].[insert_entity][py_insert_entity] method.</span></span> <span data-ttu-id="09b04-118">L’objet d’entité peut être un dictionnaire ou un objet de type [Entité][py_Entity], et définit les noms et valeurs de votre entité.</span><span class="sxs-lookup"><span data-stu-id="09b04-118">The entity object can be a dictionary or an object of type [Entity][py_Entity], and defines your entity's property names and values.</span></span> <span data-ttu-id="09b04-119">Chaque entité doit inclure les propriétés [PartitionKey et RowKey](#partitionkey-and-rowkey), en plus de toutes les autres propriétés que vous définissez pour l’entité.</span><span class="sxs-lookup"><span data-stu-id="09b04-119">Every entity must include the required [PartitionKey and RowKey](#partitionkey-and-rowkey) properties, in addition to any other properties you define for the entity.</span></span>

<span data-ttu-id="09b04-120">Cet exemple crée un objet dictionnaire représentant une entité, puis le passe à la méthode [insert_entity][py_insert_entity] pour l’ajouter à la table :</span><span class="sxs-lookup"><span data-stu-id="09b04-120">This example creates a dictionary object representing an entity, then passes it to the [insert_entity][py_insert_entity] method to add it to the table:</span></span>

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out the trash', 'priority' : 200}
table_service.insert_entity('tasktable', task)
```

<span data-ttu-id="09b04-121">Cet exemple crée un objet [Entité][py_Entity], puis le passe à la méthode [insert_entity][py_insert_entity] pour l’ajouter à la table :</span><span class="sxs-lookup"><span data-stu-id="09b04-121">This example creates an [Entity][py_Entity] object, then passes it to the [insert_entity][py_insert_entity] method to add it to the table:</span></span>

```python
task = Entity()
task.PartitionKey = 'tasksSeattle'
task.RowKey = '002'
task.description = 'Wash the car'
task.priority = 100
table_service.insert_entity('tasktable', task)
```

### <a name="partitionkey-and-rowkey"></a><span data-ttu-id="09b04-122">PartitionKey et RowKey</span><span class="sxs-lookup"><span data-stu-id="09b04-122">PartitionKey and RowKey</span></span>

<span data-ttu-id="09b04-123">Vous devez spécifier les propriétés **PartitionKey** et **RowKey** pour chaque entité.</span><span class="sxs-lookup"><span data-stu-id="09b04-123">You must specify both a **PartitionKey** and a **RowKey** property for every entity.</span></span> <span data-ttu-id="09b04-124">Il s’agit des identificateurs uniques de vos entités, car ils forment ensemble la clé primaire d’une entité.</span><span class="sxs-lookup"><span data-stu-id="09b04-124">These are the unique identifiers of your entities, as together they form the primary key of an entity.</span></span> <span data-ttu-id="09b04-125">Vous pouvez interroger à l’aide de ces valeurs beaucoup plus vite que vous pouvez interroger d’autres propriétés d’entité, car seules ces propriétés sont indexées.</span><span class="sxs-lookup"><span data-stu-id="09b04-125">You can query using these values much faster than you can query any other entity properties because only these properties are indexed.</span></span>

<span data-ttu-id="09b04-126">Le service de table utilise **PartitionKey** pour répartir intelligemment les entités de table entre nœuds de stockage.</span><span class="sxs-lookup"><span data-stu-id="09b04-126">The Table service uses **PartitionKey** to intelligently distribute table entities across storage nodes.</span></span> <span data-ttu-id="09b04-127">Les entités partageant la même clé **PartitionKey** sont stockées sur le même nœud.</span><span class="sxs-lookup"><span data-stu-id="09b04-127">Entities that have the same  **PartitionKey** are stored on the same node.</span></span> <span data-ttu-id="09b04-128">**RowKey** est l'identifiant unique de l'entité dans sa partition.</span><span class="sxs-lookup"><span data-stu-id="09b04-128">**RowKey** is the unique ID of the entity within the partition it belongs to.</span></span>

## <a name="update-an-entity"></a><span data-ttu-id="09b04-129">Mise à jour d'une entité</span><span class="sxs-lookup"><span data-stu-id="09b04-129">Update an entity</span></span>

<span data-ttu-id="09b04-130">Pour mettre à jour toutes les valeurs de propriété d’une entité, appelez la méthode [update_entity][py_update_entity].</span><span class="sxs-lookup"><span data-stu-id="09b04-130">To update all of an entity's property values, call the [update_entity][py_update_entity] method.</span></span> <span data-ttu-id="09b04-131">Cet exemple montre comment remplacer d'une entité existante par une version mise à jour :</span><span class="sxs-lookup"><span data-stu-id="09b04-131">This example shows how to replace an existing entity with an updated version:</span></span>

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out the garbage', 'priority' : 250}
table_service.update_entity('tasktable', task)
```

<span data-ttu-id="09b04-132">Si l'entité à remplacer n'existe pas encore, l'opération de mise à jour échoue.</span><span class="sxs-lookup"><span data-stu-id="09b04-132">If the entity that is being updated doesn't already exist, then the update operation will fail.</span></span> <span data-ttu-id="09b04-133">Si vous voulez stocker une entité, qu’elle existe déjà ou non, utilisez [insert_or_replace_entity][py_insert_or_replace_entity].</span><span class="sxs-lookup"><span data-stu-id="09b04-133">If you want to store an entity whether it exists or not, use [insert_or_replace_entity][py_insert_or_replace_entity].</span></span> <span data-ttu-id="09b04-134">Dans l'exemple suivant, le premier appel remplace l'entité existante.</span><span class="sxs-lookup"><span data-stu-id="09b04-134">In the following example, the first call will replace the existing entity.</span></span> <span data-ttu-id="09b04-135">Le deuxième appel insère une nouvelle entité, car il n’existe aucune entité ayant les clés PartitionKey et RowKey spécifiées.</span><span class="sxs-lookup"><span data-stu-id="09b04-135">The second call will insert a new entity, since no entity with the specified PartitionKey and RowKey exists in the table.</span></span>

```python
# Replace the entity created earlier
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out the garbage again', 'priority' : 250}
table_service.insert_or_replace_entity('tasktable', task)

# Insert a new entity
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '003', 'description' : 'Buy detergent', 'priority' : 300}
table_service.insert_or_replace_entity('tasktable', task)
```

> [!TIP]
> <span data-ttu-id="09b04-136">La méthode [update_entity][py_update_entity] remplace toutes les propriétés et valeurs d’une entité existante, ce qui vous permet également de supprimer les propriétés d’une entité existante.</span><span class="sxs-lookup"><span data-stu-id="09b04-136">The [update_entity][py_update_entity] method replaces all properties and values of an existing entity, which you can also use to remove properties from an existing entity.</span></span> <span data-ttu-id="09b04-137">Vous pouvez utiliser la méthode [merge_entity][py_merge_entity] pour mettre à jour une entité existante avec des valeurs de propriétés nouvelles ou modifiées sans remplacement complet de l’entité.</span><span class="sxs-lookup"><span data-stu-id="09b04-137">You can use the [merge_entity][py_merge_entity] method to update an existing entity with new or modified property values without completely replacing the entity.</span></span>

## <a name="modify-multiple-entities"></a><span data-ttu-id="09b04-138">Modifier plusieurs entités</span><span class="sxs-lookup"><span data-stu-id="09b04-138">Modify multiple entities</span></span>

<span data-ttu-id="09b04-139">Pour garantir le traitement atomique d’une demande par le service de table, vous pouvez envoyer plusieurs opérations dans un lot.</span><span class="sxs-lookup"><span data-stu-id="09b04-139">To ensure the atomic processing of a request by the Table service, you can submit multiple operations together in a batch.</span></span> <span data-ttu-id="09b04-140">Tout d’abord, utilisez la classe [TableBatch][py_TableBatch] pour ajouter plusieurs opérations à un seul lot.</span><span class="sxs-lookup"><span data-stu-id="09b04-140">First, use the [TableBatch][py_TableBatch] class to add multiple operations to a single batch.</span></span> <span data-ttu-id="09b04-141">Ensuite, appelez [TableService][py_TableService].[ commit_batch][py_commit_batch] pour envoyer les opérations dans une opération atomique.</span><span class="sxs-lookup"><span data-stu-id="09b04-141">Next, call [TableService][py_TableService].[commit_batch][py_commit_batch] to submit the operations in an atomic operation.</span></span> <span data-ttu-id="09b04-142">Toutes les entités à modifier dans le lot doivent être dans la même partition.</span><span class="sxs-lookup"><span data-stu-id="09b04-142">All entities to be modified in batch must be in the same partition.</span></span>

<span data-ttu-id="09b04-143">Cet exemple permet d'ajouter deux entités dans un lot :</span><span class="sxs-lookup"><span data-stu-id="09b04-143">This example adds two entities together in a batch:</span></span>

```python
from azure.storage.table import TableBatch
batch = TableBatch()
task004 = {'PartitionKey': 'tasksSeattle', 'RowKey': '004', 'description' : 'Go grocery shopping', 'priority' : 400}
task005 = {'PartitionKey': 'tasksSeattle', 'RowKey': '005', 'description' : 'Clean the bathroom', 'priority' : 100}
batch.insert_entity(task004)
batch.insert_entity(task005)
table_service.commit_batch('tasktable', batch)
```

<span data-ttu-id="09b04-144">Les lots peuvent également être utilisés avec la syntaxe du gestionnaire de contexte :</span><span class="sxs-lookup"><span data-stu-id="09b04-144">Batches can also be used with the context manager syntax:</span></span>

```python
task006 = {'PartitionKey': 'tasksSeattle', 'RowKey': '006', 'description' : 'Go grocery shopping', 'priority' : 400}
task007 = {'PartitionKey': 'tasksSeattle', 'RowKey': '007', 'description' : 'Clean the bathroom', 'priority' : 100}

with table_service.batch('tasktable') as batch:
    batch.insert_entity(task006)
    batch.insert_entity(task007)
```

## <a name="query-for-an-entity"></a><span data-ttu-id="09b04-145">Interrogation d’une entité</span><span class="sxs-lookup"><span data-stu-id="09b04-145">Query for an entity</span></span>

<span data-ttu-id="09b04-146">Pour rechercher une entité dans une table, passez ses paramètres PartitionKey et RowKey à la méthode [TableService][py_TableService].[ get_entity][py_get_entity].</span><span class="sxs-lookup"><span data-stu-id="09b04-146">To query for an entity in a table, pass its PartitionKey and RowKey to the [TableService][py_TableService].[get_entity][py_get_entity] method.</span></span>

```python
task = table_service.get_entity('tasktable', 'tasksSeattle', '001')
print(task.description)
print(task.priority)
```

## <a name="query-a-set-of-entities"></a><span data-ttu-id="09b04-147">Interrogation d’un ensemble d’entités</span><span class="sxs-lookup"><span data-stu-id="09b04-147">Query a set of entities</span></span>

<span data-ttu-id="09b04-148">Vous pouvez interroger un jeu d’entités en fournissant une chaîne de filtre avec le paramètre **filter**.</span><span class="sxs-lookup"><span data-stu-id="09b04-148">You can query for a set of entities by supplying a filter string with the **filter** parameter.</span></span> <span data-ttu-id="09b04-149">Cet exemple recherche toutes les tâches dans Seattle pour appliquer un filtre sur PartitionKey :</span><span class="sxs-lookup"><span data-stu-id="09b04-149">This example finds all tasks in Seattle by applying a filter on PartitionKey:</span></span>

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'")
for task in tasks:
    print(task.description)
    print(task.priority)
```

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="09b04-150">Interrogation d’un sous-ensemble de propriétés d’entité</span><span class="sxs-lookup"><span data-stu-id="09b04-150">Query a subset of entity properties</span></span>

<span data-ttu-id="09b04-151">Vous pouvez également restreindre les propriétés renvoyées pour chaque entité dans une requête.</span><span class="sxs-lookup"><span data-stu-id="09b04-151">You can also restrict which properties are returned for each entity in a query.</span></span> <span data-ttu-id="09b04-152">Cette technique, nommée *projection*, réduit la consommation de bande passante et peut améliorer les performances des requêtes, notamment pour les entités volumineuses ou les jeux de résultats.</span><span class="sxs-lookup"><span data-stu-id="09b04-152">This technique, called *projection*, reduces bandwidth and can improve query performance, especially for large entities or result sets.</span></span> <span data-ttu-id="09b04-153">Utilisez le paramètre **select** et transmettez le nom des propriétés à renvoyer au client.</span><span class="sxs-lookup"><span data-stu-id="09b04-153">Use the **select** parameter and pass the names of the properties you want returned to the client.</span></span>

<span data-ttu-id="09b04-154">La requête contenue dans le code suivant ne renvoie que la description des entités de la table.</span><span class="sxs-lookup"><span data-stu-id="09b04-154">The query in the following code returns only the descriptions of entities in the table.</span></span>

> [!NOTE]
> <span data-ttu-id="09b04-155">L’extrait suivant ne fonctionne qu’avec Stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="09b04-155">The following snippet works only against the Azure Storage.</span></span> <span data-ttu-id="09b04-156">L’émulateur de stockage ne le prend pas en charge.</span><span class="sxs-lookup"><span data-stu-id="09b04-156">It is not supported by the storage emulator.</span></span>

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'", select='description')
for task in tasks:
    print(task.description)
```

## <a name="delete-an-entity"></a><span data-ttu-id="09b04-157">Suppression d'une entité</span><span class="sxs-lookup"><span data-stu-id="09b04-157">Delete an entity</span></span>

<span data-ttu-id="09b04-158">Supprimez une entité en passant des propriétés PartitionKey et RowKey à la méthode [delete_entity][py_delete_entity].</span><span class="sxs-lookup"><span data-stu-id="09b04-158">Delete an entity by passing its PartitionKey and RowKey to the [delete_entity][py_delete_entity] method.</span></span>

```python
table_service.delete_entity('tasktable', 'tasksSeattle', '001')
```

## <a name="delete-a-table"></a><span data-ttu-id="09b04-159">Suppression d’une table</span><span class="sxs-lookup"><span data-stu-id="09b04-159">Delete a table</span></span>

<span data-ttu-id="09b04-160">Si vous n’avez plus besoin une table ou une des entités qui s’y trouvent, appelez la méthode [delete_table][py_delete_table] pour supprimer définitivement la table du stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="09b04-160">If you no longer need a table or any of the entities within it, call the [delete_table][py_delete_table] method to permanently delete the table from Azure Storage.</span></span>

```python
table_service.delete_table('tasktable')
```

## <a name="next-steps"></a><span data-ttu-id="09b04-161">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="09b04-161">Next steps</span></span>

* [<span data-ttu-id="09b04-162">Référence du kit de développement logiciel (SDK) Stockage Azure pour l’API Python</span><span class="sxs-lookup"><span data-stu-id="09b04-162">Azure Storage SDK for Python API reference</span></span>](https://azure-storage.readthedocs.io/en/latest/index.html)
* [<span data-ttu-id="09b04-163">Kit de développement logiciel (SDK) Stockage Azure pour Python</span><span class="sxs-lookup"><span data-stu-id="09b04-163">Azure Storage SDK for Python</span></span>](https://github.com/Azure/azure-storage-python)
* [<span data-ttu-id="09b04-164">Centre de développement Python</span><span class="sxs-lookup"><span data-stu-id="09b04-164">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/)
* <span data-ttu-id="09b04-165">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) : une application gratuite et multiplateforme de Microsoft qui vous permet d’exploiter visuellement les données de stockage Azure sur Windows, macOS et Linux.</span><span class="sxs-lookup"><span data-stu-id="09b04-165">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md): A free, cross-platform application for working visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

[py_commit_batch]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.commit_batch
[py_create_table]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.create_table
[py_delete_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.delete_entity
[py_delete_table]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.delete_table
[py_Entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.models.html#azure.storage.table.models.Entity
[py_get_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.get_entity
[py_insert_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.insert_entity
[py_insert_or_replace_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.insert_or_replace_entity
[py_merge_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.merge_entity
[py_update_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.update_entity
[py_TableService]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html
[py_TableBatch]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tablebatch.html#azure.storage.table.tablebatch.TableBatch
