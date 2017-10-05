---
title: "Appeler une procédure stockée à partir d’une activité de copie Azure Data Factory | Microsoft Docs"
description: "Découvrez comment appeler une procédure stockée dans Azure SQL Database ou SQL Server à partir d’une activité de copie Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: af6e4a57e726598c266ee766656aa2cc22e374e3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="invoke-stored-procedure-from-copy-activity-in-azure-data-factory"></a><span data-ttu-id="9b84c-103">Appeler une procédure stockée à partir d’une activité de copie dans Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="9b84c-103">Invoke stored procedure from copy activity in Azure Data Factory</span></span>
<span data-ttu-id="9b84c-104">Lorsque vous copiez des données dans [SQL Server](data-factory-sqlserver-connector.md) ou [Azure SQL Database](data-factory-azure-sql-connector.md), vous pouvez configurer l’élément **SqlSink** dans l’activité de copie pour appeler une procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="9b84c-104">When copying data into [SQL Server](data-factory-sqlserver-connector.md) or [Azure SQL Database](data-factory-azure-sql-connector.md), you can configure the **SqlSink** in copy activity to invoke a stored procedure.</span></span> <span data-ttu-id="9b84c-105">Vous pourriez vouloir utiliser la procédure stockée pour effectuer les traitements supplémentaires (fusion de colonnes, recherche de valeurs, insertion dans plusieurs tables, etc.) requis avant d’insérer les données dans la table de destination.</span><span class="sxs-lookup"><span data-stu-id="9b84c-105">You may want to use the stored procedure to perform any additional processing (merging columns, looking up values, insertion into multiple tables, etc.) is required before inserting data in to the destination table.</span></span> <span data-ttu-id="9b84c-106">Cette fonction tire parti des [paramètres table](https://msdn.microsoft.com/library/bb675163.aspx).</span><span class="sxs-lookup"><span data-stu-id="9b84c-106">This feature takes advantage of [Table-Valued Parameters](https://msdn.microsoft.com/library/bb675163.aspx).</span></span> 

<span data-ttu-id="9b84c-107">L’exemple suivant montre comment invoquer une procédure stockée dans une base de données SQL Server à partir d’un pipeline Data Factory (activité de copie) :</span><span class="sxs-lookup"><span data-stu-id="9b84c-107">The following sample shows how to invoke a stored procedure in a SQL Server database from a Data Factory pipeline (copy activity):</span></span>  

## <a name="output-dataset-json"></a><span data-ttu-id="9b84c-108">JSON du jeu de données de sortie</span><span class="sxs-lookup"><span data-stu-id="9b84c-108">Output dataset JSON</span></span>
<span data-ttu-id="9b84c-109">Dans le JSON du jeu de données de sortie, définissez le **type** sur : **SqlServerTable**.</span><span class="sxs-lookup"><span data-stu-id="9b84c-109">In the output dataset JSON, set the **type** to: **SqlServerTable**.</span></span> <span data-ttu-id="9b84c-110">Affectez-lui la valeur **AzureSqlTable** pour l’utiliser avec une base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="9b84c-110">Set it to **AzureSqlTable** to use with an Azure SQL database.</span></span> <span data-ttu-id="9b84c-111">La valeur de la propriété **tableName** doit correspondre au nom du premier paramètre de la procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="9b84c-111">The value for **tableName** property must match the name of first parameter of the stored procedure.</span></span>  

```json
{
  "name": "SqlOutput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlLinkedService",
    "typeProperties": {
      "tableName": "Marketing"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

## <a name="sqlsink-section-in-copy-activity-json"></a><span data-ttu-id="9b84c-112">Section SqlSink dans le JSON de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="9b84c-112">SqlSink section in copy activity JSON</span></span>
<span data-ttu-id="9b84c-113">Définissez la section **SqlSink** dans le JSON de l’activité de copie comme suit.</span><span class="sxs-lookup"><span data-stu-id="9b84c-113">Define the **SqlSink** section in the copy activity JSON as follows.</span></span> <span data-ttu-id="9b84c-114">Pour appeler une procédure stockée lors de l’insertion de données dans la base de données réceptrice ou de destination, spécifiez des valeurs pour les propriétés **SqlWriterStoredProcedureName** et **SqlWriterTableType**.</span><span class="sxs-lookup"><span data-stu-id="9b84c-114">To invoke a stored procedure while inserting data into the sink/destination database, specify values for both **SqlWriterStoredProcedureName** and **SqlWriterTableType** properties.</span></span> <span data-ttu-id="9b84c-115">Pour obtenir une description de ces propriétés, consultez la [section SqlSink de l’article sur le connecteur SQL Server](data-factory-sqlserver-connector.md#sqlsink).</span><span class="sxs-lookup"><span data-stu-id="9b84c-115">For descriptions of these properties, see [SqlSink section in the SQL Server connector article](data-factory-sqlserver-connector.md#sqlsink).</span></span>

```json
"sink":
{
    "type": "SqlSink",
    "SqlWriterTableType": "MarketingType",
    "SqlWriterStoredProcedureName": "spOverwriteMarketing", 
    "storedProcedureParameters":
            {
                "stringData": 
                {
                    "value": "str1"     
                }
            }
}
```

## <a name="stored-procedure-definition"></a><span data-ttu-id="9b84c-116">Définition de la procédure stockée</span><span class="sxs-lookup"><span data-stu-id="9b84c-116">Stored procedure definition</span></span> 
<span data-ttu-id="9b84c-117">Dans votre base de données, définissez la procédure stockée avec le même nom que **SqlWriterStoredProcedureName**.</span><span class="sxs-lookup"><span data-stu-id="9b84c-117">In your database, define the stored procedure with the same name as **SqlWriterStoredProcedureName**.</span></span> <span data-ttu-id="9b84c-118">La procédure stockée gère les données d’entrée provenant du magasin de données source et insère les données dans une table dans la base de données de destination.</span><span class="sxs-lookup"><span data-stu-id="9b84c-118">The stored procedure handles input data from the source data store, and inserts data into a table in the destination database.</span></span> <span data-ttu-id="9b84c-119">Le nom du premier paramètre de la procédure stockée doit correspondre au nom de table défini dans le JSON du jeu de données (Marketing).</span><span class="sxs-lookup"><span data-stu-id="9b84c-119">The name of the first parameter of stored procedure must match the tableName defined in the dataset JSON (Marketing).</span></span>

```sql
CREATE PROCEDURE spOverwriteMarketing @Marketing [dbo].[MarketingType] READONLY, @stringData varchar(256)
AS
BEGIN
    DELETE FROM [dbo].[Marketing] where ProfileID = @stringData
    INSERT [dbo].[Marketing](ProfileID, State)
    SELECT * FROM @Marketing
END
```

## <a name="table-type-definition"></a><span data-ttu-id="9b84c-120">Définition du type de table</span><span class="sxs-lookup"><span data-stu-id="9b84c-120">Table type definition</span></span>
<span data-ttu-id="9b84c-121">Dans votre base de données, définissez le type de table avec le même nom que **SqlWriterTableType**.</span><span class="sxs-lookup"><span data-stu-id="9b84c-121">In your database, define the table type with the same name as **SqlWriterTableType**.</span></span> <span data-ttu-id="9b84c-122">Le schéma du type de table doit correspondre au schéma du jeu de données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="9b84c-122">The schema of the table type must match the schema of the input dataset.</span></span>

```sql
CREATE TYPE [dbo].[MarketingType] AS TABLE(
    [ProfileID] [varchar](256) NOT NULL,
    [State] [varchar](256) NOT NULL
)
```

## <a name="next-steps"></a><span data-ttu-id="9b84c-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9b84c-123">Next steps</span></span>
<span data-ttu-id="9b84c-124">Pour accéder à des exemples JSON complets, consultez les articles suivants sur les connecteurs :</span><span class="sxs-lookup"><span data-stu-id="9b84c-124">Review the following connector articles that for complete JSON examples:</span></span> 

- [<span data-ttu-id="9b84c-125">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="9b84c-125">Azure SQL Database</span></span>](data-factory-azure-sql-connector.md)
- [<span data-ttu-id="9b84c-126">SQL Server</span><span class="sxs-lookup"><span data-stu-id="9b84c-126">SQL Server</span></span>](data-factory-sqlserver-connector.md)
