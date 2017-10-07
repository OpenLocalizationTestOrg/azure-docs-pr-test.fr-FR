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
# <a name="how-toouse-table-storage-in-python"></a>Comment toouse le stockage de Table dans Python

[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

Ce guide vous explique comment les scénarios de stockage de Table Azure courants tooperform dans Python à l’aide de hello [le stockage Microsoft Azure SDK pour Python](https://github.com/Azure/azure-storage-python). les scénarios de Hello couvertes incluent la création et suppression d’une table et insérer et l’interrogation des entités.

Lors de l’utilisation des scénarios hello dans ce didacticiel, vous souhaiterez peut-être toorefer toohello [SDK de stockage Azure pour la référence de l’API de Python](https://azure-storage.readthedocs.io/en/latest/index.html).

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="install-hello-azure-storage-sdk-for-python"></a>Installer hello stockage Azure SDK pour Python

Une fois que vous avez créé un compte de stockage, l’étape suivante consiste à tooinstall hello [le stockage Microsoft Azure SDK pour Python](https://github.com/Azure/azure-storage-python). Pour plus d’informations sur l’installation de hello SDK, consultez toohello [README.rst](https://github.com/Azure/azure-storage-python/blob/master/README.rst) fichier hello SDK de stockage pour le référentiel de Python sur GitHub.

## <a name="create-a-table"></a>Création d’une table

toowork avec hello service Table Azure dans Python, vous devez importer hello [TableService] [ py_TableService] module. Étant donné que vous allez travailler avec les entités de Table, vous devez également hello [entité] [ py_Entity] classe. Ajoutez ce code haut hello votre fichier Python tooimport les deux :

```python
from azure.storage.table import TableService, Entity
```

Créez un objet [TableService][py_TableService], en passant votre clé de compte et le nom du compte de stockage. Remplacez `myaccount` et `mykey` avec votre nom de compte et une clé et un appel [create_table] [ py_create_table] table de hello toocreate dans le stockage Azure.

```python
table_service = TableService(account_name='myaccount', account_key='mykey')

table_service.create_table('tasktable')
```

## <a name="add-an-entity-tooa-table"></a>Ajouter une table de tooa d’entité

tooadd une entité, vous créez tout d’abord un objet qui représente l’entité, puis les toohello d’objet passe hello [TableService][py_TableService].[ insert_entity] [ py_insert_entity] (méthode). objet d’entité Hello peut être un dictionnaire ou un objet de type [entité][py_Entity]et définit les noms et les valeurs de votre entité. Chaque entité doit inclure hello requis [PartitionKey et RowKey](#partitionkey-and-rowkey) propriétés, dans Ajout tooany autres propriétés que vous définissez pour l’entité de hello.

Cet exemple crée un objet dictionnaire qui représente une entité, puis le transmet toohello [insert_entity] [ py_insert_entity] tooadd de méthode il toohello table :

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello trash', 'priority' : 200}
table_service.insert_entity('tasktable', task)
```

Cet exemple crée un [entité] [ py_Entity] de l’objet, puis il passe toohello [insert_entity] [ py_insert_entity] tooadd de méthode il toohello table :

```python
task = Entity()
task.PartitionKey = 'tasksSeattle'
task.RowKey = '002'
task.description = 'Wash hello car'
task.priority = 100
table_service.insert_entity('tasktable', task)
```

### <a name="partitionkey-and-rowkey"></a>PartitionKey et RowKey

Vous devez spécifier les propriétés **PartitionKey** et **RowKey** pour chaque entité. Il s’agit comme ensemble des identificateurs uniques hello vos entités, ils forment la clé primaire de hello d’une entité. Vous pouvez interroger à l’aide de ces valeurs beaucoup plus vite que vous pouvez interroger d’autres propriétés d’entité, car seules ces propriétés sont indexées.

Hello service de Table utilise **PartitionKey** toointelligently répartir les entités de table sur les nœuds de stockage. Entités qui ont hello même **PartitionKey** sont stockés sur hello même nœud. **RowKey** est hello des ID unique de l’entité hello au sein de la partition hello auquel il appartient.

## <a name="update-an-entity"></a>Mise à jour d'une entité

tooupdate toutes des valeurs de propriété d’une entité, appelez hello [update_entity] [ py_update_entity] (méthode). Cet exemple montre comment tooreplace une entité existante avec une version mise à jour :

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello garbage', 'priority' : 250}
table_service.update_entity('tasktable', task)
```

Si l’entité hello est en cours de mise à jour n’existe pas déjà, puis hello mise à jour échoue. Si vous souhaitez toostore une entité si elle existe ou non, utilisez [insert_or_replace_entity][py_insert_or_replace_entity]. Dans l’exemple suivant de hello, premier appel de hello remplace entité existante de hello. deuxième appel de Hello insère une nouvelle entité, car aucune entité avec hello ne spécifié PartitionKey et RowKey existe dans la table de hello.

```python
# Replace hello entity created earlier
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello garbage again', 'priority' : 250}
table_service.insert_or_replace_entity('tasktable', task)

# Insert a new entity
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '003', 'description' : 'Buy detergent', 'priority' : 300}
table_service.insert_or_replace_entity('tasktable', task)
```

> [!TIP]
> Hello [update_entity] [ py_update_entity] méthode remplace toutes les propriétés et les valeurs d’une entité existante, que vous pouvez également utiliser les propriétés de tooremove à partir d’une entité existante. Vous pouvez utiliser hello [merge_entity] [ py_merge_entity] méthode tooupdate une entité existante avec des valeurs de propriété nouvelles ou modifiées sans remplacer complètement les entités hello.

## <a name="modify-multiple-entities"></a>Modifier plusieurs entités

tooensure hello traitement atomique d’une demande par le service de Table hello, vous pouvez envoyer plusieurs opérations dans un lot. Tout d’abord, utilisez hello [TableBatch] [ py_TableBatch] classe tooadd plusieurs opérations tooa lot. Ensuite, appelez [TableService][py_TableService].[ commit_batch] [ py_commit_batch] toosubmit les opérations de hello dans une opération atomique. Toutes les entités toobe modifié dans le lot doit être Bonjour même partition.

Cet exemple permet d'ajouter deux entités dans un lot :

```python
from azure.storage.table import TableBatch
batch = TableBatch()
task004 = {'PartitionKey': 'tasksSeattle', 'RowKey': '004', 'description' : 'Go grocery shopping', 'priority' : 400}
task005 = {'PartitionKey': 'tasksSeattle', 'RowKey': '005', 'description' : 'Clean hello bathroom', 'priority' : 100}
batch.insert_entity(task004)
batch.insert_entity(task005)
table_service.commit_batch('tasktable', batch)
```

Lots peuvent également être utilisées avec la syntaxe du Gestionnaire de contexte hello :

```python
task006 = {'PartitionKey': 'tasksSeattle', 'RowKey': '006', 'description' : 'Go grocery shopping', 'priority' : 400}
task007 = {'PartitionKey': 'tasksSeattle', 'RowKey': '007', 'description' : 'Clean hello bathroom', 'priority' : 100}

with table_service.batch('tasktable') as batch:
    batch.insert_entity(task006)
    batch.insert_entity(task007)
```

## <a name="query-for-an-entity"></a>Interrogation d’une entité

tooquery pour une entité dans une table, transmettre ses toohello PartitionKey et RowKey [TableService][py_TableService].[ get_entity] [ py_get_entity] (méthode).

```python
task = table_service.get_entity('tasktable', 'tasksSeattle', '001')
print(task.description)
print(task.priority)
```

## <a name="query-a-set-of-entities"></a>Interrogation d’un ensemble d’entités

Vous pouvez interroger pour un jeu d’entités, vous devez fournir une chaîne de filtrage par hello **filtre** paramètre. Cet exemple recherche toutes les tâches dans Seattle pour appliquer un filtre sur PartitionKey :

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'")
for task in tasks:
    print(task.description)
    print(task.priority)
```

## <a name="query-a-subset-of-entity-properties"></a>Interrogation d’un sous-ensemble de propriétés d’entité

Vous pouvez également restreindre les propriétés renvoyées pour chaque entité dans une requête. Cette technique, nommée *projection*, réduit la consommation de bande passante et peut améliorer les performances des requêtes, notamment pour les entités volumineuses ou les jeux de résultats. Hello d’utilisation **sélectionnez** paramètre et passe hello les noms de propriétés hello retourné toohello client.

requête Hello hello suivant code retourne uniquement les descriptions de hello des entités dans la table de hello.

> [!NOTE]
> Hello suivant fonctionne extrait uniquement par rapport à hello le stockage Azure. Il n’est pas pris en charge par l’émulateur de stockage hello.

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'", select='description')
for task in tasks:
    print(task.description)
```

## <a name="delete-an-entity"></a>Suppression d’une entité

Supprimer une entité en passant son toohello PartitionKey et RowKey [delete_entity] [ py_delete_entity] (méthode).

```python
table_service.delete_entity('tasktable', 'tasksSeattle', '001')
```

## <a name="delete-a-table"></a>Suppression d’une table

Si vous n’avez plus besoin une table ou une des entités hello qu’il contient, appelez hello [delete_table] [ py_delete_table] méthode toopermanently supprimer la table de hello de stockage Azure.

```python
table_service.delete_table('tasktable')
```

## <a name="next-steps"></a>Étapes suivantes

* [Référence du kit de développement logiciel (SDK) Stockage Azure pour l’API Python](https://azure-storage.readthedocs.io/en/latest/index.html)
* [Kit de développement logiciel (SDK) Stockage Azure pour Python](https://github.com/Azure/azure-storage-python)
* [Centre de développement Python](https://azure.microsoft.com/develop/python/)
* [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) : une application gratuite et multiplateforme de Microsoft qui vous permet d’exploiter visuellement les données de stockage Azure sur Windows, macOS et Linux.

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
