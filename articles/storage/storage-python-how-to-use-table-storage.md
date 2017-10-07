---
title: aaaHow toouse stockage de Table Azure avec Python | Documents Microsoft
description: "Stocker des données structurées dans le cloud hello avec le stockage Table Azure, un magasin de données NoSQL."
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
ms.openlocfilehash: fd0e1b05cc12618f348eaf2d85d0dce5ac32702a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-in-python"></a><span data-ttu-id="c7be0-103">Comment toouse le stockage de Table dans Python</span><span class="sxs-lookup"><span data-stu-id="c7be0-103">How toouse Table storage in Python</span></span>

[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

<span data-ttu-id="c7be0-104">Ce guide vous explique comment les scénarios de stockage de Table Azure courants tooperform dans Python à l’aide de hello [le stockage Microsoft Azure SDK pour Python](https://github.com/Azure/azure-storage-python).</span><span class="sxs-lookup"><span data-stu-id="c7be0-104">This guide shows you how tooperform common Azure Table storage scenarios in Python using hello [Microsoft Azure Storage SDK for Python](https://github.com/Azure/azure-storage-python).</span></span> <span data-ttu-id="c7be0-105">les scénarios de Hello couvertes incluent la création et suppression d’une table et insérer et l’interrogation des entités.</span><span class="sxs-lookup"><span data-stu-id="c7be0-105">hello scenarios covered include creating and deleting a table, and inserting and querying entities.</span></span>

<span data-ttu-id="c7be0-106">Lors de l’utilisation des scénarios hello dans ce didacticiel, vous souhaiterez peut-être toorefer toohello [SDK de stockage Azure pour la référence de l’API de Python](https://azure-storage.readthedocs.io/en/latest/index.html).</span><span class="sxs-lookup"><span data-stu-id="c7be0-106">While working through hello scenarios in this tutorial, you may wish toorefer toohello [Azure Storage SDK for Python API reference](https://azure-storage.readthedocs.io/en/latest/index.html).</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="install-hello-azure-storage-sdk-for-python"></a><span data-ttu-id="c7be0-107">Installer hello stockage Azure SDK pour Python</span><span class="sxs-lookup"><span data-stu-id="c7be0-107">Install hello Azure Storage SDK for Python</span></span>

<span data-ttu-id="c7be0-108">Une fois que vous avez créé un compte de stockage, l’étape suivante consiste à tooinstall hello [le stockage Microsoft Azure SDK pour Python](https://github.com/Azure/azure-storage-python).</span><span class="sxs-lookup"><span data-stu-id="c7be0-108">Once you've created a storage account, your next step is tooinstall hello [Microsoft Azure Storage SDK for Python](https://github.com/Azure/azure-storage-python).</span></span> <span data-ttu-id="c7be0-109">Pour plus d’informations sur l’installation de hello SDK, consultez toohello [README.rst](https://github.com/Azure/azure-storage-python/blob/master/README.rst) fichier hello SDK de stockage pour le référentiel de Python sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="c7be0-109">For details on installing hello SDK, refer toohello [README.rst](https://github.com/Azure/azure-storage-python/blob/master/README.rst) file in hello Storage SDK for Python repository on GitHub.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="c7be0-110">Création d’une table</span><span class="sxs-lookup"><span data-stu-id="c7be0-110">Create a table</span></span>

<span data-ttu-id="c7be0-111">toowork avec hello service Table Azure dans Python, vous devez importer hello [TableService] [ py_TableService] module.</span><span class="sxs-lookup"><span data-stu-id="c7be0-111">toowork with hello Azure Table service in Python, you must import hello [TableService][py_TableService] module.</span></span> <span data-ttu-id="c7be0-112">Étant donné que vous allez travailler avec les entités de Table, vous devez également hello [entité] [ py_Entity] classe.</span><span class="sxs-lookup"><span data-stu-id="c7be0-112">Since you'll be working with Table entities, you also need hello [Entity][py_Entity] class.</span></span> <span data-ttu-id="c7be0-113">Ajoutez ce code haut hello votre fichier Python tooimport les deux :</span><span class="sxs-lookup"><span data-stu-id="c7be0-113">Add this code near hello top your Python file tooimport both:</span></span>

```python
from azure.storage.table import TableService, Entity
```

<span data-ttu-id="c7be0-114">Créez un objet [TableService][py_TableService], en passant votre clé de compte et le nom du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="c7be0-114">Create a [TableService][py_TableService] object, passing in your storage account name and account key.</span></span> <span data-ttu-id="c7be0-115">Remplacez `myaccount` et `mykey` avec votre nom de compte et une clé et un appel [create_table] [ py_create_table] table de hello toocreate dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="c7be0-115">Replace `myaccount` and `mykey` with your account name and key, and call [create_table][py_create_table] toocreate hello table in Azure Storage.</span></span>

```python
table_service = TableService(account_name='myaccount', account_key='mykey')

table_service.create_table('tasktable')
```

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="c7be0-116">Ajouter une table de tooa d’entité</span><span class="sxs-lookup"><span data-stu-id="c7be0-116">Add an entity tooa table</span></span>

<span data-ttu-id="c7be0-117">tooadd une entité, vous créez tout d’abord un objet qui représente l’entité, puis les toohello d’objet passe hello [TableService][py_TableService].[ insert_entity] [ py_insert_entity] (méthode).</span><span class="sxs-lookup"><span data-stu-id="c7be0-117">tooadd an entity, you first create an object that represents your entity, then pass hello object toohello [TableService][py_TableService].[insert_entity][py_insert_entity] method.</span></span> <span data-ttu-id="c7be0-118">objet d’entité Hello peut être un dictionnaire ou un objet de type [entité][py_Entity]et définit les noms et les valeurs de votre entité.</span><span class="sxs-lookup"><span data-stu-id="c7be0-118">hello entity object can be a dictionary or an object of type [Entity][py_Entity], and defines your entity's property names and values.</span></span> <span data-ttu-id="c7be0-119">Chaque entité doit inclure hello requis [PartitionKey et RowKey](#partitionkey-and-rowkey) propriétés, dans Ajout tooany autres propriétés que vous définissez pour l’entité de hello.</span><span class="sxs-lookup"><span data-stu-id="c7be0-119">Every entity must include hello required [PartitionKey and RowKey](#partitionkey-and-rowkey) properties, in addition tooany other properties you define for hello entity.</span></span>

<span data-ttu-id="c7be0-120">Cet exemple crée un objet dictionnaire qui représente une entité, puis le transmet toohello [insert_entity] [ py_insert_entity] tooadd de méthode il toohello table :</span><span class="sxs-lookup"><span data-stu-id="c7be0-120">This example creates a dictionary object representing an entity, then passes it toohello [insert_entity][py_insert_entity] method tooadd it toohello table:</span></span>

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello trash', 'priority' : 200}
table_service.insert_entity('tasktable', task)
```

<span data-ttu-id="c7be0-121">Cet exemple crée un [entité] [ py_Entity] de l’objet, puis il passe toohello [insert_entity] [ py_insert_entity] tooadd de méthode il toohello table :</span><span class="sxs-lookup"><span data-stu-id="c7be0-121">This example creates an [Entity][py_Entity] object, then passes it toohello [insert_entity][py_insert_entity] method tooadd it toohello table:</span></span>

```python
task = Entity()
task.PartitionKey = 'tasksSeattle'
task.RowKey = '002'
task.description = 'Wash hello car'
task.priority = 100
table_service.insert_entity('tasktable', task)
```

### <a name="partitionkey-and-rowkey"></a><span data-ttu-id="c7be0-122">PartitionKey et RowKey</span><span class="sxs-lookup"><span data-stu-id="c7be0-122">PartitionKey and RowKey</span></span>

<span data-ttu-id="c7be0-123">Vous devez spécifier les propriétés **PartitionKey** et **RowKey** pour chaque entité.</span><span class="sxs-lookup"><span data-stu-id="c7be0-123">You must specify both a **PartitionKey** and a **RowKey** property for every entity.</span></span> <span data-ttu-id="c7be0-124">Il s’agit comme ensemble des identificateurs uniques hello vos entités, ils forment la clé primaire de hello d’une entité.</span><span class="sxs-lookup"><span data-stu-id="c7be0-124">These are hello unique identifiers of your entities, as together they form hello primary key of an entity.</span></span> <span data-ttu-id="c7be0-125">Vous pouvez interroger à l’aide de ces valeurs beaucoup plus vite que vous pouvez interroger d’autres propriétés d’entité, car seules ces propriétés sont indexées.</span><span class="sxs-lookup"><span data-stu-id="c7be0-125">You can query using these values much faster than you can query any other entity properties because only these properties are indexed.</span></span>

<span data-ttu-id="c7be0-126">Hello service de Table utilise **PartitionKey** toointelligently répartir les entités de table sur les nœuds de stockage.</span><span class="sxs-lookup"><span data-stu-id="c7be0-126">hello Table service uses **PartitionKey** toointelligently distribute table entities across storage nodes.</span></span> <span data-ttu-id="c7be0-127">Entités qui ont hello même **PartitionKey** sont stockés sur hello même nœud.</span><span class="sxs-lookup"><span data-stu-id="c7be0-127">Entities that have hello same  **PartitionKey** are stored on hello same node.</span></span> <span data-ttu-id="c7be0-128">**RowKey** est hello des ID unique de l’entité hello au sein de la partition hello auquel il appartient.</span><span class="sxs-lookup"><span data-stu-id="c7be0-128">**RowKey** is hello unique ID of hello entity within hello partition it belongs to.</span></span>

## <a name="update-an-entity"></a><span data-ttu-id="c7be0-129">Mise à jour d'une entité</span><span class="sxs-lookup"><span data-stu-id="c7be0-129">Update an entity</span></span>

<span data-ttu-id="c7be0-130">tooupdate toutes des valeurs de propriété d’une entité, appelez hello [update_entity] [ py_update_entity] (méthode).</span><span class="sxs-lookup"><span data-stu-id="c7be0-130">tooupdate all of an entity's property values, call hello [update_entity][py_update_entity] method.</span></span> <span data-ttu-id="c7be0-131">Cet exemple montre comment tooreplace une entité existante avec une version mise à jour :</span><span class="sxs-lookup"><span data-stu-id="c7be0-131">This example shows how tooreplace an existing entity with an updated version:</span></span>

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello garbage', 'priority' : 250}
table_service.update_entity('tasktable', task)
```

<span data-ttu-id="c7be0-132">Si l’entité hello est en cours de mise à jour n’existe pas déjà, puis hello mise à jour échoue.</span><span class="sxs-lookup"><span data-stu-id="c7be0-132">If hello entity that is being updated doesn't already exist, then hello update operation will fail.</span></span> <span data-ttu-id="c7be0-133">Si vous souhaitez toostore une entité si elle existe ou non, utilisez [insert_or_replace_entity][py_insert_or_replace_entity].</span><span class="sxs-lookup"><span data-stu-id="c7be0-133">If you want toostore an entity whether it exists or not, use [insert_or_replace_entity][py_insert_or_replace_entity].</span></span> <span data-ttu-id="c7be0-134">Dans l’exemple suivant de hello, premier appel de hello remplace entité existante de hello.</span><span class="sxs-lookup"><span data-stu-id="c7be0-134">In hello following example, hello first call will replace hello existing entity.</span></span> <span data-ttu-id="c7be0-135">deuxième appel de Hello insère une nouvelle entité, car aucune entité avec hello ne spécifié PartitionKey et RowKey existe dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="c7be0-135">hello second call will insert a new entity, since no entity with hello specified PartitionKey and RowKey exists in hello table.</span></span>

```python
# Replace hello entity created earlier
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello garbage again', 'priority' : 250}
table_service.insert_or_replace_entity('tasktable', task)

# Insert a new entity
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '003', 'description' : 'Buy detergent', 'priority' : 300}
table_service.insert_or_replace_entity('tasktable', task)
```

> [!TIP]
> <span data-ttu-id="c7be0-136">Hello [update_entity] [ py_update_entity] méthode remplace toutes les propriétés et les valeurs d’une entité existante, que vous pouvez également utiliser les propriétés de tooremove à partir d’une entité existante.</span><span class="sxs-lookup"><span data-stu-id="c7be0-136">hello [update_entity][py_update_entity] method replaces all properties and values of an existing entity, which you can also use tooremove properties from an existing entity.</span></span> <span data-ttu-id="c7be0-137">Vous pouvez utiliser hello [merge_entity] [ py_merge_entity] méthode tooupdate une entité existante avec des valeurs de propriété nouvelles ou modifiées sans remplacer complètement les entités hello.</span><span class="sxs-lookup"><span data-stu-id="c7be0-137">You can use hello [merge_entity][py_merge_entity] method tooupdate an existing entity with new or modified property values without completely replacing hello entity.</span></span>

## <a name="modify-multiple-entities"></a><span data-ttu-id="c7be0-138">Modifier plusieurs entités</span><span class="sxs-lookup"><span data-stu-id="c7be0-138">Modify multiple entities</span></span>

<span data-ttu-id="c7be0-139">tooensure hello traitement atomique d’une demande par le service de Table hello, vous pouvez envoyer plusieurs opérations dans un lot.</span><span class="sxs-lookup"><span data-stu-id="c7be0-139">tooensure hello atomic processing of a request by hello Table service, you can submit multiple operations together in a batch.</span></span> <span data-ttu-id="c7be0-140">Tout d’abord, utilisez hello [TableBatch] [ py_TableBatch] classe tooadd plusieurs opérations tooa lot.</span><span class="sxs-lookup"><span data-stu-id="c7be0-140">First, use hello [TableBatch][py_TableBatch] class tooadd multiple operations tooa single batch.</span></span> <span data-ttu-id="c7be0-141">Ensuite, appelez [TableService][py_TableService].[ commit_batch] [ py_commit_batch] toosubmit les opérations de hello dans une opération atomique.</span><span class="sxs-lookup"><span data-stu-id="c7be0-141">Next, call [TableService][py_TableService].[commit_batch][py_commit_batch] toosubmit hello operations in an atomic operation.</span></span> <span data-ttu-id="c7be0-142">Toutes les entités toobe modifié dans le lot doit être Bonjour même partition.</span><span class="sxs-lookup"><span data-stu-id="c7be0-142">All entities toobe modified in batch must be in hello same partition.</span></span>

<span data-ttu-id="c7be0-143">Cet exemple permet d'ajouter deux entités dans un lot :</span><span class="sxs-lookup"><span data-stu-id="c7be0-143">This example adds two entities together in a batch:</span></span>

```python
from azure.storage.table import TableBatch
batch = TableBatch()
task004 = {'PartitionKey': 'tasksSeattle', 'RowKey': '004', 'description' : 'Go grocery shopping', 'priority' : 400}
task005 = {'PartitionKey': 'tasksSeattle', 'RowKey': '005', 'description' : 'Clean hello bathroom', 'priority' : 100}
batch.insert_entity(task004)
batch.insert_entity(task005)
table_service.commit_batch('tasktable', batch)
```

<span data-ttu-id="c7be0-144">Lots peuvent également être utilisées avec la syntaxe du Gestionnaire de contexte hello :</span><span class="sxs-lookup"><span data-stu-id="c7be0-144">Batches can also be used with hello context manager syntax:</span></span>

```python
task006 = {'PartitionKey': 'tasksSeattle', 'RowKey': '006', 'description' : 'Go grocery shopping', 'priority' : 400}
task007 = {'PartitionKey': 'tasksSeattle', 'RowKey': '007', 'description' : 'Clean hello bathroom', 'priority' : 100}

with table_service.batch('tasktable') as batch:
    batch.insert_entity(task006)
    batch.insert_entity(task007)
```

## <a name="query-for-an-entity"></a><span data-ttu-id="c7be0-145">Interrogation d’une entité</span><span class="sxs-lookup"><span data-stu-id="c7be0-145">Query for an entity</span></span>

<span data-ttu-id="c7be0-146">tooquery pour une entité dans une table, transmettre ses toohello PartitionKey et RowKey [TableService][py_TableService].[ get_entity] [ py_get_entity] (méthode).</span><span class="sxs-lookup"><span data-stu-id="c7be0-146">tooquery for an entity in a table, pass its PartitionKey and RowKey toohello [TableService][py_TableService].[get_entity][py_get_entity] method.</span></span>

```python
task = table_service.get_entity('tasktable', 'tasksSeattle', '001')
print(task.description)
print(task.priority)
```

## <a name="query-a-set-of-entities"></a><span data-ttu-id="c7be0-147">Interrogation d’un ensemble d’entités</span><span class="sxs-lookup"><span data-stu-id="c7be0-147">Query a set of entities</span></span>

<span data-ttu-id="c7be0-148">Vous pouvez interroger pour un jeu d’entités, vous devez fournir une chaîne de filtrage par hello **filtre** paramètre.</span><span class="sxs-lookup"><span data-stu-id="c7be0-148">You can query for a set of entities by supplying a filter string with hello **filter** parameter.</span></span> <span data-ttu-id="c7be0-149">Cet exemple recherche toutes les tâches dans Seattle pour appliquer un filtre sur PartitionKey :</span><span class="sxs-lookup"><span data-stu-id="c7be0-149">This example finds all tasks in Seattle by applying a filter on PartitionKey:</span></span>

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'")
for task in tasks:
    print(task.description)
    print(task.priority)
```

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="c7be0-150">Interrogation d’un sous-ensemble de propriétés d’entité</span><span class="sxs-lookup"><span data-stu-id="c7be0-150">Query a subset of entity properties</span></span>

<span data-ttu-id="c7be0-151">Vous pouvez également restreindre les propriétés renvoyées pour chaque entité dans une requête.</span><span class="sxs-lookup"><span data-stu-id="c7be0-151">You can also restrict which properties are returned for each entity in a query.</span></span> <span data-ttu-id="c7be0-152">Cette technique, nommée *projection*, réduit la consommation de bande passante et peut améliorer les performances des requêtes, notamment pour les entités volumineuses ou les jeux de résultats.</span><span class="sxs-lookup"><span data-stu-id="c7be0-152">This technique, called *projection*, reduces bandwidth and can improve query performance, especially for large entities or result sets.</span></span> <span data-ttu-id="c7be0-153">Hello d’utilisation **sélectionnez** paramètre et passe hello les noms de propriétés hello retourné toohello client.</span><span class="sxs-lookup"><span data-stu-id="c7be0-153">Use hello **select** parameter and pass hello names of hello properties you want returned toohello client.</span></span>

<span data-ttu-id="c7be0-154">requête Hello hello suivant code retourne uniquement les descriptions de hello des entités dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="c7be0-154">hello query in hello following code returns only hello descriptions of entities in hello table.</span></span>

> [!NOTE]
> <span data-ttu-id="c7be0-155">Hello suivant fonctionne extrait uniquement par rapport à hello le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="c7be0-155">hello following snippet works only against hello Azure Storage.</span></span> <span data-ttu-id="c7be0-156">Il n’est pas pris en charge par l’émulateur de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="c7be0-156">It is not supported by hello storage emulator.</span></span>

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'", select='description')
for task in tasks:
    print(task.description)
```

## <a name="delete-an-entity"></a><span data-ttu-id="c7be0-157">Suppression d’une entité</span><span class="sxs-lookup"><span data-stu-id="c7be0-157">Delete an entity</span></span>

<span data-ttu-id="c7be0-158">Supprimer une entité en passant son toohello PartitionKey et RowKey [delete_entity] [ py_delete_entity] (méthode).</span><span class="sxs-lookup"><span data-stu-id="c7be0-158">Delete an entity by passing its PartitionKey and RowKey toohello [delete_entity][py_delete_entity] method.</span></span>

```python
table_service.delete_entity('tasktable', 'tasksSeattle', '001')
```

## <a name="delete-a-table"></a><span data-ttu-id="c7be0-159">Suppression d’une table</span><span class="sxs-lookup"><span data-stu-id="c7be0-159">Delete a table</span></span>

<span data-ttu-id="c7be0-160">Si vous n’avez plus besoin une table ou une des entités hello qu’il contient, appelez hello [delete_table] [ py_delete_table] méthode toopermanently supprimer la table de hello de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="c7be0-160">If you no longer need a table or any of hello entities within it, call hello [delete_table][py_delete_table] method toopermanently delete hello table from Azure Storage.</span></span>

```python
table_service.delete_table('tasktable')
```

## <a name="next-steps"></a><span data-ttu-id="c7be0-161">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c7be0-161">Next steps</span></span>

* [<span data-ttu-id="c7be0-162">Référence du kit de développement logiciel (SDK) Stockage Azure pour l’API Python</span><span class="sxs-lookup"><span data-stu-id="c7be0-162">Azure Storage SDK for Python API reference</span></span>](https://azure-storage.readthedocs.io/en/latest/index.html)
* [<span data-ttu-id="c7be0-163">Kit de développement logiciel (SDK) Stockage Azure pour Python</span><span class="sxs-lookup"><span data-stu-id="c7be0-163">Azure Storage SDK for Python</span></span>](https://github.com/Azure/azure-storage-python)
* [<span data-ttu-id="c7be0-164">Centre de développement Python</span><span class="sxs-lookup"><span data-stu-id="c7be0-164">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/)
* <span data-ttu-id="c7be0-165">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) : une application gratuite et multiplateforme de Microsoft qui vous permet d’exploiter visuellement les données de stockage Azure sur Windows, macOS et Linux.</span><span class="sxs-lookup"><span data-stu-id="c7be0-165">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md): A free, cross-platform application for working visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

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
