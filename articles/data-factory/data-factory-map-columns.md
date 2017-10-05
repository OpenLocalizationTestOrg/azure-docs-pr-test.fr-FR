---
title: "Mappage de colonnes de jeux de données dans Azure Data Factory | Microsoft Docs"
description: "Découvrez comment mapper des colonnes source sur des colonnes de destination."
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
ms.openlocfilehash: a50661b377cfbbff3f1f762342cb275d5da82cea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="map-source-dataset-columns-to-destination-dataset-columns"></a><span data-ttu-id="d3c16-103">Mapper des colonnes d’un jeu de données source sur des colonnes d’un jeu de données de destination</span><span class="sxs-lookup"><span data-stu-id="d3c16-103">Map source dataset columns to destination dataset columns</span></span>
<span data-ttu-id="d3c16-104">Le mappage de colonnes peut être utilisé pour spécifier la façon dont les colonnes spécifiées dans la « structure » de la table source sont mappées vers les colonnes spécifiées dans la « structure » de la table du récepteur.</span><span class="sxs-lookup"><span data-stu-id="d3c16-104">Column mapping can be used to specify how columns specified in the “structure” of source table map to columns specified in the “structure” of sink table.</span></span> <span data-ttu-id="d3c16-105">La propriété **columnMapping** est disponible dans la section **typeProperties** de l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="d3c16-105">The **columnMapping** property is available in the **typeProperties** section of the Copy activity.</span></span>

<span data-ttu-id="d3c16-106">Le mappage de colonnes prend en charge les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="d3c16-106">Column mapping supports the following scenarios:</span></span>

* <span data-ttu-id="d3c16-107">Toutes les colonnes de la structure du jeu de données source sont mappées sur toutes les colonnes de la structure du jeu de données récepteur.</span><span class="sxs-lookup"><span data-stu-id="d3c16-107">All columns in the source dataset structure are mapped to all columns in the sink dataset structure.</span></span>
* <span data-ttu-id="d3c16-108">Un sous-ensemble des colonnes de la structure du jeu de données source est mappé sur toutes les colonnes de la structure du jeu de données récepteur.</span><span class="sxs-lookup"><span data-stu-id="d3c16-108">A subset of the columns in the source dataset structure is mapped to all columns in the sink dataset structure.</span></span>

<span data-ttu-id="d3c16-109">Voici une liste de conditions d’erreur qui entraînent la levée d’une exception :</span><span class="sxs-lookup"><span data-stu-id="d3c16-109">The following are error conditions that result in an exception:</span></span>

* <span data-ttu-id="d3c16-110">La « structure » de la table du récepteur contient un nombre de colonnes inférieur ou supérieur à celui spécifié par le mappage de colonnes.</span><span class="sxs-lookup"><span data-stu-id="d3c16-110">Either fewer columns or more columns in the “structure” of sink table than specified in the mapping.</span></span>
* <span data-ttu-id="d3c16-111">Mappage en double.</span><span class="sxs-lookup"><span data-stu-id="d3c16-111">Duplicate mapping.</span></span>
* <span data-ttu-id="d3c16-112">Le résultat de la requête SQL ne comprend pas de nom de colonne qui soit spécifié dans le mappage.</span><span class="sxs-lookup"><span data-stu-id="d3c16-112">SQL query result does not have a column name that is specified in the mapping.</span></span>

> [!NOTE]
> <span data-ttu-id="d3c16-113">Les exemples suivants concernent SQL Azure et les objets blob Azure, mais sont applicables à tout magasin de données prenant en charge les jeux de données rectangulaires.</span><span class="sxs-lookup"><span data-stu-id="d3c16-113">The following samples are for Azure SQL and Azure Blob but are applicable to any data store that supports rectangular datasets.</span></span> <span data-ttu-id="d3c16-114">Ajustez les définitions du jeu de données et du service lié dans les exemples de sorte qu’elles pointent vers les données de la source de données appropriée.</span><span class="sxs-lookup"><span data-stu-id="d3c16-114">Adjust dataset and linked service definitions in examples to point to data in the relevant data source.</span></span>

## <a name="sample-1--column-mapping-from-azure-sql-to-azure-blob"></a><span data-ttu-id="d3c16-115">Exemple 1 : mappage de colonnes depuis SQL Azure vers un objet blob Azure</span><span class="sxs-lookup"><span data-stu-id="d3c16-115">Sample 1 – column mapping from Azure SQL to Azure blob</span></span>
<span data-ttu-id="d3c16-116">Dans cet exemple, la table d’entrée possède une structure et pointe vers une table SQL comprise dans une base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="d3c16-116">In this sample, the input table has a structure and it points to a SQL table in an Azure SQL database.</span></span>

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

<span data-ttu-id="d3c16-117">Dans cet exemple, la table de sortie possède une structure et pointe vers un objet blob compris dans un stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="d3c16-117">In this sample, the output table has a structure and it points to a blob in an Azure blob storage.</span></span>

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

<span data-ttu-id="d3c16-118">Le JSON suivant définit une activité de copie dans un pipeline.</span><span class="sxs-lookup"><span data-stu-id="d3c16-118">The following JSON defines a copy activity in a pipeline.</span></span> <span data-ttu-id="d3c16-119">Les colonnes de la source sont mappées sur les colonnes du récepteur (**columnMappings**) à l’aide de la propriété **Translator**.</span><span class="sxs-lookup"><span data-stu-id="d3c16-119">The columns from source mapped to columns in sink (**columnMappings**) by using the **Translator** property.</span></span>

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
<span data-ttu-id="d3c16-120">**Flux du mappage de colonnes :**</span><span class="sxs-lookup"><span data-stu-id="d3c16-120">**Column mapping flow:**</span></span>

![Flux du mappage de colonnes](./media/data-factory-map-columns/column-mapping-flow.png)

## <a name="sample-2--column-mapping-with-sql-query-from-azure-sql-to-azure-blob"></a><span data-ttu-id="d3c16-122">Exemple 2 : mappage de colonnes à l’aide d’une requête SQL depuis SQL Azure vers un objet blob Azure</span><span class="sxs-lookup"><span data-stu-id="d3c16-122">Sample 2 – column mapping with SQL query from Azure SQL to Azure blob</span></span>
<span data-ttu-id="d3c16-123">Dans cet exemple, une requête SQL est utilisée pour extraire des données de SQL Azure au lieu de simplement spécifier le nom de la table et le nom des colonnes dans la section « structure ».</span><span class="sxs-lookup"><span data-stu-id="d3c16-123">In this sample, a SQL query is used to extract data from Azure SQL instead of simply specifying the table name and the column names in “structure” section.</span></span> 

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
<span data-ttu-id="d3c16-124">Dans ce cas, les résultats de la requête sont d’abord mappés vers les colonnes spécifiées dans la « structure » de la source.</span><span class="sxs-lookup"><span data-stu-id="d3c16-124">In this case, the query results are first mapped to columns specified in “structure” of source.</span></span> <span data-ttu-id="d3c16-125">Ensuite, les colonnes de la « structure » de la source sont mappées vers les colonnes de la « structure » du récepteur avec les règles spécifiées dans columnMappings.</span><span class="sxs-lookup"><span data-stu-id="d3c16-125">Next, the columns from source “structure” are mapped to columns in sink “structure” with rules specified in columnMappings.</span></span>  <span data-ttu-id="d3c16-126">Supposons que la requête retourne cinq colonnes, c’est-à-dire deux colonnes de plus que celles spécifiées dans la « structure » de la source.</span><span class="sxs-lookup"><span data-stu-id="d3c16-126">Suppose the query returns 5 columns, two more columns than those specified in the “structure” of source.</span></span>

<span data-ttu-id="d3c16-127">**Flux du mappage de colonnes**</span><span class="sxs-lookup"><span data-stu-id="d3c16-127">**Column mapping flow**</span></span>

![Flux du mappage de colonnes 2](./media/data-factory-map-columns/column-mapping-flow-2.png)

## <a name="next-steps"></a><span data-ttu-id="d3c16-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d3c16-129">Next steps</span></span>
<span data-ttu-id="d3c16-130">Suivez le didacticiel sur l’activité de copie dans l’article suivant :</span><span class="sxs-lookup"><span data-stu-id="d3c16-130">See the article for a tutorial on using Copy Activity:</span></span> 

- [<span data-ttu-id="d3c16-131">Copie de données à partir du Stockage Blob vers une base de données SQL</span><span class="sxs-lookup"><span data-stu-id="d3c16-131">Copy data from Blob Storage to SQL Database</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
