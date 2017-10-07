---
title: "colonnes de jeu de données aaaMapping dans Azure Data Factory | Documents Microsoft"
description: "Découvrez comment toomap source colonnes toodestination colonnes."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 8f78d4af675bec0a70e5f6e83ec1ffb511408b5a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="map-source-dataset-columns-toodestination-dataset-columns"></a>Mapper les colonnes de jeu de données source dataset colonnes toodestination
Mappage de colonnes peut être utilisé toospecify comment les colonnes spécifiées dans hello « structure » de toocolumns de mappage de table source spécifiés dans « structure hello » de la table du récepteur. Hello **columnMapping** propriété n’est disponible dans hello **typeProperties** section Hello activité de copie.

Mappage de colonnes prend en charge hello les scénarios suivants :

* Toutes les colonnes de structure de jeu de données source hello sont mappés tooall des colonnes dans la structure de jeu de données récepteur hello.
* Un sous-ensemble de colonnes hello dans la structure de jeu de données source hello est tooall mappé pour les colonnes de structure de jeu de données récepteur hello.

Hello Voici les conditions d’erreur qui provoque une exception :

* Moins de colonnes ou plus de colonnes dans hello « structure » de la table du récepteur que spécifié dans le mappage de hello.
* Mappage en double.
* Résultat de la requête SQL n’a pas un nom de colonne qui est spécifié dans le mappage de hello.

> [!NOTE]
> Hello exemples suivants sont pour SQL Azure et les objets Blob Azure, mais banque de données applicable tooany qui prend en charge les jeux de données rectangulaire. Ajustez le jeu de données et les définitions de service lié dans toodata de toopoint d’exemples dans la source de données correspondante hello.

## <a name="sample-1--column-mapping-from-azure-sql-tooazure-blob"></a>Exemple 1 : colonne de mappage à partir de l’objet blob de tooAzure SQL Azure
Dans cet exemple, table d’entrée de hello possède une structure et qu’elle pointe tooa SQL table dans une base de données SQL Azure.

```json
{
    "name": "AzureSQLInput",
    "properties": {
        "structure": 
         [
           { "name": "userid"},
           { "name": "name"},
           { "name": "group"}
         ],
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

Dans cet exemple, table de sortie hello possède une structure et qu’elle pointe tooa blob dans un stockage d’objets blob Azure.

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
         "structure": 
          [
                { "name": "myuserid"},
                { "name": "myname" },
                { "name": "mygroup"}
          ],
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder",
            "fileName":"myfile.csv",
            "format":
            {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

Hello suivant JSON définit une activité de copie dans un pipeline. colonnes de Hello à partir de la source mappées toocolumns dans le récepteur (**columnMappings**) à l’aide de hello **traducteur** propriété.

```json
{
    "name": "CopyActivity",
    "description": "description", 
    "type": "Copy",
    "inputs":  [ { "name": "AzureSQLInput"  } ],
    "outputs":  [ { "name": "AzureBlobOutput" } ],
    "typeProperties":    {
        "source":
        {
            "type": "SqlSource"
        },
        "sink":
        {
            "type": "BlobSink"
        },
        "translator": 
        {
            "type": "TabularTranslator",
            "ColumnMappings": "UserId: MyUserId, Group: MyGroup, Name: MyName"
        }
    },
   "scheduler": {
          "frequency": "Hour",
          "interval": 1
        }
}
```
**Flux du mappage de colonnes :**

![Flux du mappage de colonnes](./media/data-factory-map-columns/column-mapping-flow.png)

## <a name="sample-2--column-mapping-with-sql-query-from-azure-sql-tooazure-blob"></a>Exemple 2 : requête SQL à partir de l’objet blob de Azure SQL tooAzure de mappage de colonne
Dans cet exemple, une requête SQL est utilisé tooextract des données à partir de SQL Azure au lieu de simplement spécifier nom de la table hello et noms de colonne hello dans la section « structure ». 

```json
{
    "name": "CopyActivity",
    "description": "description", 
    "type": "CopyActivity",
    "inputs":  [ { "name": " AzureSQLInput"  } ],
    "outputs":  [ { "name": " AzureBlobOutput" } ],
    "typeProperties":
    {
        "source":
        {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('SELECT * FROM MyTable WHERE StartDateTime = \\'{0:yyyyMMdd-HH}\\'', WindowStart)"
        },
        "sink":
        {
            "type": "BlobSink"
        },
        "Translator": 
        {
            "type": "TabularTranslator",
            "ColumnMappings": "UserId: MyUserId, Group: MyGroup,Name: MyName"
        }
    },
    "scheduler": {
          "frequency": "Hour",
          "interval": 1
        }
}
```
Dans ce cas, les résultats de requête hello sont premier toocolumns mappé spécifié dans « structure » de la source. Ensuite, les colonnes de hello à partir de la source « structure » sont mappés toocolumns de récepteur « structure » avec les règles spécifiées dans columnMappings.  Supposons que la requête de hello retourne 5 colonnes, les deux plus de colonnes que celles spécifiées dans hello « structure » de la source.

**Flux du mappage de colonnes**

![Flux du mappage de colonnes 2](./media/data-factory-map-columns/column-mapping-flow-2.png)

## <a name="next-steps"></a>Étapes suivantes
Consultez l’article de hello pour obtenir un didacticiel sur l’utilisation de l’activité de copie : 

- [Copier les données de stockage d’objets Blob tooSQL de base de données](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
