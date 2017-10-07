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
# <a name="invoke-stored-procedure-from-copy-activity-in-azure-data-factory"></a>Appeler une procédure stockée à partir d’une activité de copie dans Azure Data Factory
Lors de la copie des données dans [SQL Server](data-factory-sqlserver-connector.md) ou [base de données SQL Azure](data-factory-azure-sql-connector.md), vous pouvez configurer hello **SqlSink** dans l’activité de copie tooinvoke une procédure stockée. Vous souhaiterez peut-être tooperform de procédure stockée hello toouse un traitement supplémentaire (fusion de colonnes, la recherche de valeurs, d’insertion dans plusieurs tables, etc.) est requis avant d’insérer des données dans la table de destination toohello. Cette fonction tire parti des [paramètres table](https://msdn.microsoft.com/library/bb675163.aspx). 

Hello suivant l’exemple montre comment tooinvoke une procédure stockée dans SQL Server de base de données à partir d’un pipeline de fabrique de données (activité de copie) :  

## <a name="output-dataset-json"></a>JSON du jeu de données de sortie
Dans le dataset de sortie hello JSON, définissez hello **type** à : **SqlServerTable**. Définissez-le trop**AzureSqlTable** toouse avec une base de données SQL Azure. Hello valeur pour **tableName** propriété doit correspondre au nom de hello du premier paramètre de procédure stockée hello.  

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

## <a name="sqlsink-section-in-copy-activity-json"></a>Section SqlSink dans le JSON de l’activité de copie
Définir hello **SqlSink** section dans l’activité de copie hello JSON comme suit. tooinvoke une procédure stockée lors de l’insertion de données dans la base de données du récepteur et de destination hello, spécifiez des valeurs pour **SqlWriterStoredProcedureName** et **SqlWriterTableType** propriétés. Pour obtenir une description de ces propriétés, consultez [section SqlSink dans l’article de connecteur SQL Server hello](data-factory-sqlserver-connector.md#sqlsink).

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

## <a name="stored-procedure-definition"></a>Définition de la procédure stockée 
Dans votre base de données, définir la procédure stockée hello hello même nom en tant que **SqlWriterStoredProcedureName**. procédure stockée Hello gère les données d’entrée à partir du magasin de données source hello et insère des données dans une table de base de données de destination hello. nom de Hello de hello premier paramètre de procédure stockée doit correspondre tableName hello défini dans le dataset hello JSON (Marketing).

```sql
CREATE PROCEDURE spOverwriteMarketing @Marketing [dbo].[MarketingType] READONLY, @stringData varchar(256)
AS
BEGIN
    DELETE FROM [dbo].[Marketing] where ProfileID = @stringData
    INSERT [dbo].[Marketing](ProfileID, State)
    SELECT * FROM @Marketing
END
```

## <a name="table-type-definition"></a>Définition du type de table
Dans votre base de données, définissez le type de table de hello avec hello même nom en tant que **SqlWriterTableType**. schéma Hello hello du type de table doit correspondre au schéma hello du jeu de données d’entrée hello.

```sql
CREATE TYPE [dbo].[MarketingType] AS TABLE(
    [ProfileID] [varchar](256) NOT NULL,
    [State] [varchar](256) NOT NULL
)
```

## <a name="next-steps"></a>Étapes suivantes
Passez en revue hello suivant connecteur articles pour exécuter les exemples JSON : 

- [Azure SQL Database](data-factory-azure-sql-connector.md)
- [SQL Server](data-factory-sqlserver-connector.md)
