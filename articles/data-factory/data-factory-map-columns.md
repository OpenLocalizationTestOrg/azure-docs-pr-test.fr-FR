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
# <a name="map-source-dataset-columns-toodestination-dataset-columns"></a><span data-ttu-id="eb42a-103">Mapper les colonnes de jeu de données source dataset colonnes toodestination</span><span class="sxs-lookup"><span data-stu-id="eb42a-103">Map source dataset columns toodestination dataset columns</span></span>
<span data-ttu-id="eb42a-104">Mappage de colonnes peut être utilisé toospecify comment les colonnes spécifiées dans hello « structure » de toocolumns de mappage de table source spécifiés dans « structure hello » de la table du récepteur.</span><span class="sxs-lookup"><span data-stu-id="eb42a-104">Column mapping can be used toospecify how columns specified in hello “structure” of source table map toocolumns specified in hello “structure” of sink table.</span></span> <span data-ttu-id="eb42a-105">Hello **columnMapping** propriété n’est disponible dans hello **typeProperties** section Hello activité de copie.</span><span class="sxs-lookup"><span data-stu-id="eb42a-105">hello **columnMapping** property is available in hello **typeProperties** section of hello Copy activity.</span></span>

<span data-ttu-id="eb42a-106">Mappage de colonnes prend en charge hello les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="eb42a-106">Column mapping supports hello following scenarios:</span></span>

* <span data-ttu-id="eb42a-107">Toutes les colonnes de structure de jeu de données source hello sont mappés tooall des colonnes dans la structure de jeu de données récepteur hello.</span><span class="sxs-lookup"><span data-stu-id="eb42a-107">All columns in hello source dataset structure are mapped tooall columns in hello sink dataset structure.</span></span>
* <span data-ttu-id="eb42a-108">Un sous-ensemble de colonnes hello dans la structure de jeu de données source hello est tooall mappé pour les colonnes de structure de jeu de données récepteur hello.</span><span class="sxs-lookup"><span data-stu-id="eb42a-108">A subset of hello columns in hello source dataset structure is mapped tooall columns in hello sink dataset structure.</span></span>

<span data-ttu-id="eb42a-109">Hello Voici les conditions d’erreur qui provoque une exception :</span><span class="sxs-lookup"><span data-stu-id="eb42a-109">hello following are error conditions that result in an exception:</span></span>

* <span data-ttu-id="eb42a-110">Moins de colonnes ou plus de colonnes dans hello « structure » de la table du récepteur que spécifié dans le mappage de hello.</span><span class="sxs-lookup"><span data-stu-id="eb42a-110">Either fewer columns or more columns in hello “structure” of sink table than specified in hello mapping.</span></span>
* <span data-ttu-id="eb42a-111">Mappage en double.</span><span class="sxs-lookup"><span data-stu-id="eb42a-111">Duplicate mapping.</span></span>
* <span data-ttu-id="eb42a-112">Résultat de la requête SQL n’a pas un nom de colonne qui est spécifié dans le mappage de hello.</span><span class="sxs-lookup"><span data-stu-id="eb42a-112">SQL query result does not have a column name that is specified in hello mapping.</span></span>

> [!NOTE]
> <span data-ttu-id="eb42a-113">Hello exemples suivants sont pour SQL Azure et les objets Blob Azure, mais banque de données applicable tooany qui prend en charge les jeux de données rectangulaire.</span><span class="sxs-lookup"><span data-stu-id="eb42a-113">hello following samples are for Azure SQL and Azure Blob but are applicable tooany data store that supports rectangular datasets.</span></span> <span data-ttu-id="eb42a-114">Ajustez le jeu de données et les définitions de service lié dans toodata de toopoint d’exemples dans la source de données correspondante hello.</span><span class="sxs-lookup"><span data-stu-id="eb42a-114">Adjust dataset and linked service definitions in examples toopoint toodata in hello relevant data source.</span></span>

## <a name="sample-1--column-mapping-from-azure-sql-tooazure-blob"></a><span data-ttu-id="eb42a-115">Exemple 1 : colonne de mappage à partir de l’objet blob de tooAzure SQL Azure</span><span class="sxs-lookup"><span data-stu-id="eb42a-115">Sample 1 – column mapping from Azure SQL tooAzure blob</span></span>
<span data-ttu-id="eb42a-116">Dans cet exemple, table d’entrée de hello possède une structure et qu’elle pointe tooa SQL table dans une base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="eb42a-116">In this sample, hello input table has a structure and it points tooa SQL table in an Azure SQL database.</span></span>

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

<span data-ttu-id="eb42a-117">Dans cet exemple, table de sortie hello possède une structure et qu’elle pointe tooa blob dans un stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="eb42a-117">In this sample, hello output table has a structure and it points tooa blob in an Azure blob storage.</span></span>

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

<span data-ttu-id="eb42a-118">Hello suivant JSON définit une activité de copie dans un pipeline.</span><span class="sxs-lookup"><span data-stu-id="eb42a-118">hello following JSON defines a copy activity in a pipeline.</span></span> <span data-ttu-id="eb42a-119">colonnes de Hello à partir de la source mappées toocolumns dans le récepteur (**columnMappings**) à l’aide de hello **traducteur** propriété.</span><span class="sxs-lookup"><span data-stu-id="eb42a-119">hello columns from source mapped toocolumns in sink (**columnMappings**) by using hello **Translator** property.</span></span>

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
<span data-ttu-id="eb42a-120">**Flux du mappage de colonnes :**</span><span class="sxs-lookup"><span data-stu-id="eb42a-120">**Column mapping flow:**</span></span>

![Flux du mappage de colonnes](./media/data-factory-map-columns/column-mapping-flow.png)

## <a name="sample-2--column-mapping-with-sql-query-from-azure-sql-tooazure-blob"></a><span data-ttu-id="eb42a-122">Exemple 2 : requête SQL à partir de l’objet blob de Azure SQL tooAzure de mappage de colonne</span><span class="sxs-lookup"><span data-stu-id="eb42a-122">Sample 2 – column mapping with SQL query from Azure SQL tooAzure blob</span></span>
<span data-ttu-id="eb42a-123">Dans cet exemple, une requête SQL est utilisé tooextract des données à partir de SQL Azure au lieu de simplement spécifier nom de la table hello et noms de colonne hello dans la section « structure ».</span><span class="sxs-lookup"><span data-stu-id="eb42a-123">In this sample, a SQL query is used tooextract data from Azure SQL instead of simply specifying hello table name and hello column names in “structure” section.</span></span> 

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
<span data-ttu-id="eb42a-124">Dans ce cas, les résultats de requête hello sont premier toocolumns mappé spécifié dans « structure » de la source.</span><span class="sxs-lookup"><span data-stu-id="eb42a-124">In this case, hello query results are first mapped toocolumns specified in “structure” of source.</span></span> <span data-ttu-id="eb42a-125">Ensuite, les colonnes de hello à partir de la source « structure » sont mappés toocolumns de récepteur « structure » avec les règles spécifiées dans columnMappings.</span><span class="sxs-lookup"><span data-stu-id="eb42a-125">Next, hello columns from source “structure” are mapped toocolumns in sink “structure” with rules specified in columnMappings.</span></span>  <span data-ttu-id="eb42a-126">Supposons que la requête de hello retourne 5 colonnes, les deux plus de colonnes que celles spécifiées dans hello « structure » de la source.</span><span class="sxs-lookup"><span data-stu-id="eb42a-126">Suppose hello query returns 5 columns, two more columns than those specified in hello “structure” of source.</span></span>

<span data-ttu-id="eb42a-127">**Flux du mappage de colonnes**</span><span class="sxs-lookup"><span data-stu-id="eb42a-127">**Column mapping flow**</span></span>

![Flux du mappage de colonnes 2](./media/data-factory-map-columns/column-mapping-flow-2.png)

## <a name="next-steps"></a><span data-ttu-id="eb42a-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="eb42a-129">Next steps</span></span>
<span data-ttu-id="eb42a-130">Consultez l’article de hello pour obtenir un didacticiel sur l’utilisation de l’activité de copie :</span><span class="sxs-lookup"><span data-stu-id="eb42a-130">See hello article for a tutorial on using Copy Activity:</span></span> 

- [<span data-ttu-id="eb42a-131">Copier les données de stockage d’objets Blob tooSQL de base de données</span><span class="sxs-lookup"><span data-stu-id="eb42a-131">Copy data from Blob Storage tooSQL Database</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
