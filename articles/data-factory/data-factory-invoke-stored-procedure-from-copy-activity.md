---
title: "procédure d’aaaInvoke à partir de l’activité de copie de fabrique de données Azure | Documents Microsoft"
description: "Découvrez comment tooinvoke une procédure stockée dans la base de données SQL Azure ou SQL Server à partir d’une fabrique de données Azure activité de copie."
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
ms.openlocfilehash: 986377118afb8c08607c2325fcc3ab00b3de9268
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="invoke-stored-procedure-from-copy-activity-in-azure-data-factory"></a><span data-ttu-id="4d778-103">Appeler une procédure stockée à partir d’une activité de copie dans Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="4d778-103">Invoke stored procedure from copy activity in Azure Data Factory</span></span>
<span data-ttu-id="4d778-104">Lors de la copie des données dans [SQL Server](data-factory-sqlserver-connector.md) ou [base de données SQL Azure](data-factory-azure-sql-connector.md), vous pouvez configurer hello **SqlSink** dans l’activité de copie tooinvoke une procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="4d778-104">When copying data into [SQL Server](data-factory-sqlserver-connector.md) or [Azure SQL Database](data-factory-azure-sql-connector.md), you can configure hello **SqlSink** in copy activity tooinvoke a stored procedure.</span></span> <span data-ttu-id="4d778-105">Vous souhaiterez peut-être tooperform de procédure stockée hello toouse un traitement supplémentaire (fusion de colonnes, la recherche de valeurs, d’insertion dans plusieurs tables, etc.) est requis avant d’insérer des données dans la table de destination toohello.</span><span class="sxs-lookup"><span data-stu-id="4d778-105">You may want toouse hello stored procedure tooperform any additional processing (merging columns, looking up values, insertion into multiple tables, etc.) is required before inserting data in toohello destination table.</span></span> <span data-ttu-id="4d778-106">Cette fonction tire parti des [paramètres table](https://msdn.microsoft.com/library/bb675163.aspx).</span><span class="sxs-lookup"><span data-stu-id="4d778-106">This feature takes advantage of [Table-Valued Parameters](https://msdn.microsoft.com/library/bb675163.aspx).</span></span> 

<span data-ttu-id="4d778-107">Hello suivant l’exemple montre comment tooinvoke une procédure stockée dans SQL Server de base de données à partir d’un pipeline de fabrique de données (activité de copie) :</span><span class="sxs-lookup"><span data-stu-id="4d778-107">hello following sample shows how tooinvoke a stored procedure in a SQL Server database from a Data Factory pipeline (copy activity):</span></span>  

## <a name="output-dataset-json"></a><span data-ttu-id="4d778-108">JSON du jeu de données de sortie</span><span class="sxs-lookup"><span data-stu-id="4d778-108">Output dataset JSON</span></span>
<span data-ttu-id="4d778-109">Dans le dataset de sortie hello JSON, définissez hello **type** à : **SqlServerTable**.</span><span class="sxs-lookup"><span data-stu-id="4d778-109">In hello output dataset JSON, set hello **type** to: **SqlServerTable**.</span></span> <span data-ttu-id="4d778-110">Définissez-le trop**AzureSqlTable** toouse avec une base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="4d778-110">Set it too**AzureSqlTable** toouse with an Azure SQL database.</span></span> <span data-ttu-id="4d778-111">Hello valeur pour **tableName** propriété doit correspondre au nom de hello du premier paramètre de procédure stockée hello.</span><span class="sxs-lookup"><span data-stu-id="4d778-111">hello value for **tableName** property must match hello name of first parameter of hello stored procedure.</span></span>  

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

## <a name="sqlsink-section-in-copy-activity-json"></a><span data-ttu-id="4d778-112">Section SqlSink dans le JSON de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="4d778-112">SqlSink section in copy activity JSON</span></span>
<span data-ttu-id="4d778-113">Définir hello **SqlSink** section dans l’activité de copie hello JSON comme suit.</span><span class="sxs-lookup"><span data-stu-id="4d778-113">Define hello **SqlSink** section in hello copy activity JSON as follows.</span></span> <span data-ttu-id="4d778-114">tooinvoke une procédure stockée lors de l’insertion de données dans la base de données du récepteur et de destination hello, spécifiez des valeurs pour **SqlWriterStoredProcedureName** et **SqlWriterTableType** propriétés.</span><span class="sxs-lookup"><span data-stu-id="4d778-114">tooinvoke a stored procedure while inserting data into hello sink/destination database, specify values for both **SqlWriterStoredProcedureName** and **SqlWriterTableType** properties.</span></span> <span data-ttu-id="4d778-115">Pour obtenir une description de ces propriétés, consultez [section SqlSink dans l’article de connecteur SQL Server hello](data-factory-sqlserver-connector.md#sqlsink).</span><span class="sxs-lookup"><span data-stu-id="4d778-115">For descriptions of these properties, see [SqlSink section in hello SQL Server connector article](data-factory-sqlserver-connector.md#sqlsink).</span></span>

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

## <a name="stored-procedure-definition"></a><span data-ttu-id="4d778-116">Définition de la procédure stockée</span><span class="sxs-lookup"><span data-stu-id="4d778-116">Stored procedure definition</span></span> 
<span data-ttu-id="4d778-117">Dans votre base de données, définir la procédure stockée hello hello même nom en tant que **SqlWriterStoredProcedureName**.</span><span class="sxs-lookup"><span data-stu-id="4d778-117">In your database, define hello stored procedure with hello same name as **SqlWriterStoredProcedureName**.</span></span> <span data-ttu-id="4d778-118">procédure stockée Hello gère les données d’entrée à partir du magasin de données source hello et insère des données dans une table de base de données de destination hello.</span><span class="sxs-lookup"><span data-stu-id="4d778-118">hello stored procedure handles input data from hello source data store, and inserts data into a table in hello destination database.</span></span> <span data-ttu-id="4d778-119">nom de Hello de hello premier paramètre de procédure stockée doit correspondre tableName hello défini dans le dataset hello JSON (Marketing).</span><span class="sxs-lookup"><span data-stu-id="4d778-119">hello name of hello first parameter of stored procedure must match hello tableName defined in hello dataset JSON (Marketing).</span></span>

```sql
CREATE PROCEDURE spOverwriteMarketing @Marketing [dbo].[MarketingType] READONLY, @stringData varchar(256)
AS
BEGIN
    DELETE FROM [dbo].[Marketing] where ProfileID = @stringData
    INSERT [dbo].[Marketing](ProfileID, State)
    SELECT * FROM @Marketing
END
```

## <a name="table-type-definition"></a><span data-ttu-id="4d778-120">Définition du type de table</span><span class="sxs-lookup"><span data-stu-id="4d778-120">Table type definition</span></span>
<span data-ttu-id="4d778-121">Dans votre base de données, définissez le type de table de hello avec hello même nom en tant que **SqlWriterTableType**.</span><span class="sxs-lookup"><span data-stu-id="4d778-121">In your database, define hello table type with hello same name as **SqlWriterTableType**.</span></span> <span data-ttu-id="4d778-122">schéma Hello hello du type de table doit correspondre au schéma hello du jeu de données d’entrée hello.</span><span class="sxs-lookup"><span data-stu-id="4d778-122">hello schema of hello table type must match hello schema of hello input dataset.</span></span>

```sql
CREATE TYPE [dbo].[MarketingType] AS TABLE(
    [ProfileID] [varchar](256) NOT NULL,
    [State] [varchar](256) NOT NULL
)
```

## <a name="next-steps"></a><span data-ttu-id="4d778-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4d778-123">Next steps</span></span>
<span data-ttu-id="4d778-124">Passez en revue hello suivant connecteur articles pour exécuter les exemples JSON :</span><span class="sxs-lookup"><span data-stu-id="4d778-124">Review hello following connector articles that for complete JSON examples:</span></span> 

- [<span data-ttu-id="4d778-125">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="4d778-125">Azure SQL Database</span></span>](data-factory-azure-sql-connector.md)
- [<span data-ttu-id="4d778-126">SQL Server</span><span class="sxs-lookup"><span data-stu-id="4d778-126">SQL Server</span></span>](data-factory-sqlserver-connector.md)
