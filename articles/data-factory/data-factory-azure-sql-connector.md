---
title: "les données d’aaaCopy vers/à partir de la base de données SQL Azure | Documents Microsoft"
description: "Découvrez comment les données de toocopy vers/à partir de la base de données SQL Azure à l’aide d’Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 484f735b-8464-40ba-a9fc-820e6553159e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: d2ff16191afb028da75699c5e4d0bb310538db0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-azure-sql-database-using-azure-data-factory"></a>Tooand de données de copie à partir de la base de données SQL Azure à l’aide d’Azure Data Factory
Cet article explique comment toouse hello activité de copie dans Azure Data Factory toomove données tooand à partir de la base de données SQL Azure. Il repose sur hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, qui présente une vue d’ensemble du déplacement des données avec l’activité de copie hello.  

## <a name="supported-scenarios"></a>Scénarios pris en charge
Vous pouvez copier des données **à partir de la base de données SQL Azure** toohello suivant des magasins de données :

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

Vous pouvez copier des données à partir de hello suivant des magasins de données **tooAzure base de données SQL**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-authentication-type"></a>Type d’authentification pris en charge
Le connecteur Azure SQL Database prend en charge l’authentification de base.

## <a name="getting-started"></a>Prise en main
Vous pouvez créer un pipeline avec une activité de copie qui déplace les données vers/depuis Azure SQL Database à l’aide de différents outils/API.

toocreate de façon plus simple Hello un pipeline est toouse hello **Assistant copie de**. Consultez [didacticiel : créer un pipeline à l’aide d’Assistant copie de](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapides sur la création d’un pipeline à l’aide d’Assistant de données de copie hello.

Vous pouvez également utiliser hello suivant outils toocreate un pipeline : **portail Azure**, **Visual Studio**, **Azure PowerShell**, **modèle Azure Resource Manager** , **API .NET**, et **API REST**. Consultez [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions toocreate un pipeline avec une activité de copie. 

Si vous utilisez hello ou une API, vous effectuez hello suivant les étapes toocreate un pipeline qui déplace la banque de données récepteur tooa du magasin de données à partir des données d’une source : 

1. Création d'une **fabrique de données**. Une fabrique de données peut contenir un ou plusieurs pipelines. 
2. Créer **services liés** fabrique de données tooyour toolink les données d’entrée et de sortie magasins. Par exemple, si vous copiez des données à partir d’une base de données SQL Azure de tooan stockage blob Azure, vous créez deux services liés toolink votre compte de stockage et de la fabrique de données de tooyour de base de données SQL Azure. Pour les propriétés de service lié sont tooAzure spécifique de la base de données SQL, consultez [lié des propriétés du service](#linked-service-properties) section. 
3. Créer **datasets** toorepresent d’entrée et sortie l’opération de copie des données pour hello. Exemple hello mentionné dans la dernière étape de hello, vous permet de créer un conteneur d’objets blob de jeu de données toospecify hello et un dossier qui contient les données d’entrée hello. De plus, vous créez une autre table SQL hello toospecify jeu de données dans la base de données SQL Azure hello qui contient les données hello copiées à partir du stockage d’objets blob hello. Pour les propriétés du dataset qui sont spécifique tooAzure Data Lake Store, consultez [propriétés du dataset](#dataset-properties) section.
4. Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie. Dans l’exemple hello mentionné précédemment, vous utilisez BlobSource en tant que source et SqlSink comme un récepteur pour l’activité de copie hello. De même, si vous copiez à partir de la base de données SQL Azure tooAzure stockage d’objets Blob, vous utilisez SqlSource et BlobSink dans l’activité de copie hello. Pour les propriétés d’activité de copie sont tooAzure spécifique de la base de données SQL, consultez [copier les propriétés de l’activité](#copy-activity-properties) section. Pour plus d’informations sur comment toouse du magasin de données source ou un récepteur, cliquez sur le lien hello dans la section précédente de hello pour votre magasin de données.

Lorsque vous utilisez hello Assistant, les définitions de JSON pour ces entités de fabrique de données (services liés, des datasets et pipeline de hello) sont créées automatiquement pour vous. Lorsque vous utilisez/API des outils (à l’exception des API .NET), vous définissez ces entités de fabrique de données à l’aide du format JSON de hello.  Pour plus d’exemples de définitions de JSON pour les entités de fabrique de données qui sont utilisées toocopy des données vers/à partir d’une base de données SQL Azure, consultez [exemples JSON](#json-examples-for-copying-data-to-and-from-sql-database) section de cet article. 

Hello les sections suivantes fournit des détails sur les propriétés JSON qui sont utilisés toodefine Data Factory entités spécifique tooAzure base de données SQL : 

## <a name="linked-service-properties"></a>Propriétés du service lié
SQL Azure lié à des liens de service une fabrique de données de tooyour de base de données SQL Azure. Hello tableau suivant fournit la description pour JSON éléments tooAzure spécifique SQL de service lié.

| Propriété | Description | Requis |
| --- | --- | --- |
| type |propriété de type Hello doit indiquer : **AzureSqlDatabase** |Oui |
| connectionString |Spécifiez les informations nécessaires d’instance de base de données SQL Azure tooconnect toohello pour la propriété connectionString de hello. Seule l’authentification de base est prise en charge. |Oui |

> [!IMPORTANT]
> Configurer [pare-feu de base de données SQL Azure](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) hello le serveur de base de données trop[autoriser les Services Azure tooaccess hello serveur](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure). En outre, si vous copiez des données tooAzure base de données SQL, notamment Azure externe à partir de sources de données locale avec la passerelle de fabrique de données, configurer la plage d’adresses IP approprié pour l’ordinateur hello qui envoie des données tooAzure base de données SQL.

## <a name="dataset-properties"></a>Propriétés du jeu de données
toospecify un toorepresent de jeu de données d’entrée ou de sortie des données dans une base de données SQL Azure, que vous définissez propriété hello du jeu de données hello : **AzureSqlTable**. Ensemble hello **linkedServiceName** service lié de propriété du nom de toohello hello dataset Hello SQL Azure.  

Pour obtenir une liste complète des sections et les propriétés disponibles pour définir des jeux de données, consultez hello [création de datasets](data-factory-create-datasets.md) l’article. Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données (SQL Azure, Azure Blob, Azure Table, etc.).

section de typeProperties Hello est différente pour chaque type de jeu de données et fournit des informations sur l’emplacement de hello de données hello dans le magasin de données hello. Hello **typeProperties** section hello le jeu de données de type **AzureSqlTable** a hello propriétés suivantes :

| Propriété | Description | Requis |
| --- | --- | --- |
| TableName |Nom de la table de hello ou la vue d’instance de base de données SQL Azure hello service lié fait référence à. |Oui |

## <a name="copy-activity-properties"></a>Propriétés de l’activité de copie
Pour obtenir une liste complète des sections et les propriétés disponibles pour la définition d’activités, consultez hello [création de Pipelines](data-factory-create-pipelines.md) l’article. Les propriétés comme le nom, la description, les tables d’entrée et de sortie et la stratégie sont disponibles pour tous les types d’activités.

> [!NOTE]
> Hello activité de copie accepte uniquement une entrée et produit qu’une seule sortie.

Tandis que les propriétés disponibles dans hello **typeProperties** section d’activité hello varient selon chaque type d’activité. Pour l’activité de copie, ils varient selon les types de sources et récepteurs hello.

Si vous déplacez des données à partir d’une base de données SQL Azure, vous définissez type de source de hello dans l’activité de copie hello trop**SqlSource**. De même, si vous déplacez une base de données SQL Azure données tooan, vous définir le type de récepteur hello dans l’activité de copie hello trop**SqlSink**. Cette section fournit une liste de propriétés prises en charge par SqlSource et SqlSink.

### <a name="sqlsource"></a>SqlSource
Dans l’activité de copie, lors de la source de hello est de type **SqlSource**, hello propriétés suivantes est disponible dans **typeProperties** section :

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| SqlReaderQuery |Utiliser des données tooread hello requête personnalisée. |Chaîne de requête SQL. Exemple : `select * from MyTable`. |Non |
| sqlReaderStoredProcedureName |Nom de hello procédure stockée qui lit les données à partir de la table de source de hello. |Nom de hello procédure stockée. instruction SQL de la dernière Hello doit être une instruction SELECT dans la procédure stockée hello. |Non |
| storedProcedureParameters |Pourquoi les paramètres de procédure stockée. |Paires nom/valeur. Noms et la casse des paramètres doivent correspondre à des noms de hello et la casse des paramètres de la procédure stockée hello. |Non |

Si hello **sqlReaderQuery** est spécifié pour hello SqlSource, hello activité de copie s’exécute cette requête sur des données hello tooget hello base de données SQL Azure source. Ou bien, vous pouvez spécifier une procédure stockée en spécifiant hello **sqlReaderStoredProcedureName** et **storedProcedureParameters** (si hello une procédure stockée accepte des paramètres).

Si vous ne spécifiez pas de sqlReaderQuery ou sqlReaderStoredProcedureName, les colonnes hello définies dans la section de structure hello du jeu de données hello JSON sont toobuild utilisé une requête (`select column1, column2 from mytable`) toorun contre hello de base de données SQL Azure. Si la définition de dataset hello n’a pas de structure de hello, toutes les colonnes sont sélectionnées à partir de la table de hello.

> [!NOTE]
> Lorsque vous utilisez **sqlReaderStoredProcedureName**, vous devez toujours toospecify une valeur pour hello **tableName** propriété dans le dataset hello JSON. Cependant, il n’existe aucune validation effectuée pour cette table.
>
>

### <a name="sqlsource-example"></a>Exemple SqlSource

```JSON
"source": {
    "type": "SqlSource",
    "sqlReaderStoredProcedureName": "CopyTestSrcStoredProcedureWithParameters",
    "storedProcedureParameters": {
        "stringData": { "value": "str3" },
        "identifier": { "value": "$$Text.Format('{0:yyyy}', SliceStart)", "type": "Int"}
    }
}
```

**définition de la procédure stockée Hello :**

```SQL
CREATE PROCEDURE CopyTestSrcStoredProcedureWithParameters
(
    @stringData varchar(20),
    @identifier int
)
AS
SET NOCOUNT ON;
BEGIN
     select *
     from dbo.UnitTestSrcTable
     where dbo.UnitTestSrcTable.stringData != stringData
    and dbo.UnitTestSrcTable.identifier != identifier
END
GO
```

### <a name="sqlsink"></a>SqlSink
**SqlSink** prend en charge hello propriétés suivantes :

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| writeBatchTimeout |Temps d’attente pour hello lot insert opération toocomplete avant d’expirer. |intervalle de temps<br/><br/> Exemple : « 00:30:00 » (30 minutes). |Non |
| writeBatchSize |Insère des données dans une table SQL de hello lorsque la taille de mémoire tampon de hello atteint la valeur writeBatchSize. |Nombre entier (nombre de lignes) |Non (valeur par défaut : 10000) |
| sqlWriterCleanupScript |Spécifier une requête pour l’activité de copie tooexecute telles que les données d’un secteur spécifique sont nettoyées. Pour en savoir plus, voir [Copie renouvelée](#repeatable-copy). |Une instruction de requête. |Non |
| sliceIdentifierColumnName |Spécifiez un nom de colonne pour l’activité de copie toofill avec l’identificateur de secteur généré automatiquement, qui est utilisé tooclean des données d’un secteur spécifique quand réexécutée. Pour en savoir plus, voir [Copie renouvelée](#repeatable-copy). |Nom d’une colonne avec le type de données binary(32). |Non |
| sqlWriterStoredProcedureName |Nom de hello procédure stockée que les données upserts (mises à jour/insertion) dans la table cible hello. |Nom de hello procédure stockée. |Non |
| storedProcedureParameters |Pourquoi les paramètres de procédure stockée. |Paires nom/valeur. Noms et la casse des paramètres doivent correspondre à des noms de hello et la casse des paramètres de la procédure stockée hello. |Non |
| sqlWriterTableType |Spécifiez un toobe de nom de type de table utilisée dans la procédure stockée hello. Activité de copie rend les données de hello déplacées disponibles dans une table temporaire avec ce type de table. Code de procédure stockée puis de fusionner des données hello copiées avec les données existantes. |Nom de type de table. |Non |

#### <a name="sqlsink-example"></a>Exemple SqlSink

```JSON
"sink": {
    "type": "SqlSink",
    "writeBatchSize": 1000000,
    "writeBatchTimeout": "00:05:00",
    "sqlWriterStoredProcedureName": "CopyTestStoredProcedureWithParameters",
    "sqlWriterTableType": "CopyTestTableType",
    "storedProcedureParameters": {
        "identifier": { "value": "1", "type": "Int" },
        "stringData": { "value": "str1" },
        "decimalData": { "value": "1", "type": "Decimal" }
    }
}
```

## <a name="json-examples-for-copying-data-tooand-from-sql-database"></a>Exemples JSON pour la copie des données tooand à partir de la base de données SQL
Hello exemples suivants proposent des exemples de définitions de JSON que vous pouvez utiliser toocreate un pipeline à l’aide de [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Elles montrent comment tooand de données toocopy à partir de la base de données SQL Azure et de stockage d’objets Blob Azure. Toutefois, les données peuvent être copiées **directement** de n’importe quelle tooany de sources de récepteurs hello indiqué [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) à l’aide de hello activité de copie dans Azure Data Factory.

### <a name="example-copy-data-from-azure-sql-database-tooazure-blob"></a>Exemple : Copier des données à partir de la base de données SQL Azure tooAzure Blob
Hello même définit hello suivant des entités de fabrique de données :

1. Un service lié de type [AzureSqlDatabase](#linked-service-properties).
2. Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Un [jeu de données](data-factory-create-datasets.md) d'entrée de type [AzureSqlTable](#dataset-properties).
4. Un [jeu de données](data-factory-create-datasets.md) de sortie de type [Azure Blob](data-factory-azure-blob-connector.md#dataset-properties).
5. Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [SqlSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

exemple Hello copie les données de série chronologique (horaire, quotidienne, etc.) à partir d’une table dans l’objet blob tooa de base de données SQL Azure toutes les heures. propriétés JSON Hello utilisées dans ces exemples sont décrits dans les sections suivantes des exemples de hello.  

**Service lié pour Azure SQL Database :**

```JSON
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
Consultez hello [Service lié de SQL Azure](#linked-service) section pour la liste hello des propriétés prises en charge par ce service lié.

**Service lié Azure Blob Storage :**

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
Consultez hello [objets Blob Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) l’article pour la liste hello de propriétés prises en charge par ce service lié.


**Jeu de données d'entrée SQL Azure :**

exemple Hello suppose que vous avez créé une table « MyTable » dans SQL Azure, et il contienne une colonne appelée « timestampcolumn » pour les données de série chronologique.

Paramètre « external » : « true » informe service Azure Data Factory de hello ce jeu de données hello est la fabrique de données externe toohello et n’est pas généré par une activité dans la fabrique de données hello.

```JSON
{
  "name": "AzureSqlInput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
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

Consultez hello [propriétés de type de jeu de données SQL Azure](#dataset) section pour la liste hello de propriétés prises en charge par ce type de jeu de données.  

**Jeu de données de sortie Azure Blob :**

Les données sont écrites tooa nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1). chemin d’accès du dossier Hello pour l’objet blob de hello est évaluée dynamiquement en fonction de l’heure de début hello de tranche hello qui est en cours de traitement. chemin d’accès du dossier Hello utilise l’année, mois, jours et heures des parties de l’heure de début hello.

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}/",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
Consultez hello [propriétés de type de jeu de données objet Blob Azure](data-factory-azure-blob-connector.md#dataset-properties) section pour la liste hello de propriétés prises en charge par ce type de jeu de données.  

**Activité de copie dans un pipeline avec une source SQL et un récepteur blob :**

Hello pipeline contient une activité de copie qui est configuré toouse hello des jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures. Dans la définition JSON du pipeline hello, hello **source** type est défini trop**SqlSource** et **récepteur** type est défini trop**BlobSink**. la requête SQL Hello spécifiée pour hello **SqlReaderQuery** propriété sélectionne des données de hello Bonjour au-delà de toocopy d’heure.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSQLInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "BlobSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
     ]
   }
}
```
Dans l’exemple de hello, **sqlReaderQuery** est spécifié pour hello SqlSource. Hello activité de copie s’exécute cette requête par rapport à hello données de base de données SQL Azure source tooget hello. Ou bien, vous pouvez spécifier une procédure stockée en spécifiant hello **sqlReaderStoredProcedureName** et **storedProcedureParameters** (si hello une procédure stockée accepte des paramètres).

Si vous ne spécifiez pas de sqlReaderQuery ou sqlReaderStoredProcedureName, les colonnes de hello définis dans la section de structure hello du jeu de données hello JSON sont utilisé toobuild un toorun de requête par rapport à hello de base de données SQL Azure. Par exemple : `select column1, column2 from mytable`. Si la définition de dataset hello n’a pas de structure de hello, toutes les colonnes sont sélectionnées à partir de la table de hello.

Consultez hello [Sql Source](#sqlsource) section et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) pour la liste de propriétés prises en charge par SqlSource et BlobSink hello.

### <a name="example-copy-data-from-azure-blob-tooazure-sql-database"></a>Exemple : Copier des données d’objets Blob Azure tooAzure base de données SQL
exemple Hello définit hello suivant des entités de fabrique de données :  

1. Un service lié de type [AzureSqlDatabase](#linked-service-properties).
2. Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Un [jeu de données](data-factory-create-datasets.md) d'entrée de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureSqlTable](#dataset-properties).
5. Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) et [SqlSink](#copy-activity-properties).

exemple Hello copie les données de séries chronologiques (horaire, quotidienne, etc.) à partir de la table de tooa d’objets blob Azure dans la base de données SQL Azure toutes les heures. propriétés JSON Hello utilisées dans ces exemples sont décrits dans les sections suivantes des exemples de hello.

**Service lié SQL Azure :**

```JSON
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
Consultez hello [Service lié de SQL Azure](#linked-service) section pour la liste hello des propriétés prises en charge par ce service lié.

**Service lié Azure Blob Storage :**

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
Consultez hello [objets Blob Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) l’article pour la liste hello de propriétés prises en charge par ce service lié.


**Jeu de données d'entrée d'objet Blob Azure :**

Les données sont récupérées à partir d'un nouvel objet Blob toutes les heures (fréquence : heure, intervalle : 1). nom de chemin d’accès et de dossier pour l’objet blob de hello Hello sont dynamiquement évaluées en fonction de l’heure de début hello de tranche hello qui est en cours de traitement. chemin d’accès du dossier Hello utilise la partie jour de l’heure de début hello, mois et année et nom de fichier partie d’heure hello de l’heure de début hello. « external » : « true » paramètre informe le service Data Factory de hello que cette table est la fabrique de données externe toohello et qu’il n’est pas générée par une activité dans la fabrique de données hello.

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": "\n"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
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
Consultez hello [propriétés de type de jeu de données objet Blob Azure](data-factory-azure-blob-connector.md#dataset-properties) section pour la liste hello de propriétés prises en charge par ce type de jeu de données.

**Jeu de données de sortie Azure SQL Database :**

exemple Hello copie table tooa de données nommé « MyTable » dans SQL Azure. Créer la table de hello dans SQL Azure avec hello même nombre de colonnes comme vous le souhaitez toocontain de fichier CSV d’objets Blob hello. Nouvelles lignes sont ajoutées à la table de toohello toutes les heures.

```JSON
{
  "name": "AzureSqlOutput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
Consultez hello [propriétés de type de jeu de données SQL Azure](#dataset) section pour la liste hello de propriétés prises en charge par ce type de jeu de données.

**Activité de copie dans un pipeline avec une source blob et un récepteur SQL :**

Hello pipeline contient une activité de copie qui est configuré toouse hello des jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures. Dans la définition JSON du pipeline hello, hello **source** type est défini trop**BlobSource** et **récepteur** type est défini trop**SqlSink**.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQL",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource",
            "blobColumnSeparators": ","
          },
          "sink": {
            "type": "SqlSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
      ]
   }
}
```
Consultez hello [Sql récepteur](#sqlsink) section et [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) pour la liste de propriétés prises en charge par SqlSink et BlobSource hello.

## <a name="identity-columns-in-hello-target-database"></a>Colonnes d’identité dans la base de données cible hello
Cette section fournit un exemple de copie de données à partir d’une table source sans une table de destination tooa colonne identité avec une colonne d’identité.

**Table source :**

```SQL
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
**Table de destination :**

```SQL
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```
Notez que la table cible hello possède une colonne d’identité.

**Définition du jeu de données JSON source**

```JSON
{
    "name": "SampleSource",
    "properties": {
        "type": " SqlServerTable",
        "linkedServiceName": "TestIdentitySQL",
        "typeProperties": {
            "tableName": "SourceTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```
**Définition de jeu de données JSON de destination**

```JSON
{
    "name": "SampleTarget",
    "properties": {
        "structure": [
            { "name": "name" },
            { "name": "age" }
        ],
        "type": "AzureSqlTable",
        "linkedServiceName": "TestIdentitySQLSource",
        "typeProperties": {
            "tableName": "TargetTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }    
}
```

Notez que vos tables source et cible ont des schémas différents (la cible possède une colonne supplémentaire avec identité). Dans ce scénario, vous devez toospecify **structure** propriété dans la définition du dataset cible hello, qui n’inclut pas colonne d’identité hello.

## <a name="invoke-stored-procedure-from-sql-sink"></a>Appel d’une procédure stockée pour un récepteur SQL
Pour obtenir un exemple d’appel d’une procédure stockée à partir d’un récepteur SQL dans l’activité de copie d’un pipeline, consultez l’article [Appeler une procédure stockée pour un récepteur SQL dans l’activité de copie](data-factory-invoke-stored-procedure-from-copy-activity.md). 

## <a name="type-mapping-for-azure-sql-database"></a>Mappage de type pour Azure SQL Database
Comme mentionné dans hello [les activités de déplacement des données](data-factory-data-movement-activities.md) activité de copie de l’article effectue des conversions de type automatique à partir de types de sources de toosink types avec hello approche de l’étape 2 :

1. Convertir à partir de la source native types too.NET type
2. Conversion de type de récepteur de toonative de type .NET

Lorsque vous déplacez des données tooand à partir de la base de données SQL Azure, hello mappages suivants sont utilisés à partir du type too.NET de type SQL et vice versa. mappage de Hello est identique à celui hello mappage des types de données SQL Server pour ADO.NET.

| Type de moteur de base de données SQL Server | Type de .NET Framework |
| --- | --- |
| bigint |Int64 |
| binaire |Byte[] |
| bit |Boolean |
| char |String, Char[] |
| date |DateTime |
| DateTime |DateTime |
| datetime2 |DateTime |
| Datetimeoffset |Datetimeoffset |
| Décimal |Décimal |
| Attribut FILESTREAM (varbinary(max)) |Byte[] |
| Float |Double |
| image |Byte[] |
| int |Int32 |
| money |Décimal |
| nchar |String, Char[] |
| ntext |String, Char[] |
| numérique |Décimal |
| nvarchar |String, Char[] |
| real |Single |
| rowversion |Byte[] |
| smalldatetime |DateTime |
| smallint |Int16 |
| smallmoney |Décimal |
| sql_variant |Objet * |
| texte |String, Char[] |
| time |intervalle de temps |
| timestamp |Byte[] |
| tinyint |Byte |
| uniqueidentifier |Guid |
| varbinary |Byte[] |
| varchar |String, Char[] |
| xml |xml |

## <a name="map-source-toosink-columns"></a>Mapper les colonnes de source toosink
toolearn sur le mappage des colonnes dans toocolumns du jeu de données source dans le jeu de données récepteur, consultez [mappage des colonnes de jeu de données dans Azure Data Factory](data-factory-map-columns.md).

## <a name="repeatable-copy"></a>Copie renouvelée
Lors de la copie des données tooSQL serveur de base de données, l’activité de copie hello ajoute la table de données toohello récepteur par défaut. tooperform UPSERT au lieu de cela, consultez [écriture Repeatable tooSqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) l’article. 

Lors de la copie des données à partir de banques de données relationnelles, conserver la répétabilité dans l’esprit tooavoid des résultats inattendus. Dans Azure Data Factory, vous pouvez réexécuter une tranche manuellement. Vous pouvez également configurer une stratégie de nouvelles tentatives pour un jeu de données, afin qu’une tranche soit réexécutée en cas de défaillance. Lorsqu’une tranche est exécuté à nouveau dans les deux cas, vous devez toomake vraiment qui hello des mêmes données n’est en lecture aucune question comment plusieurs fois une tranche est exécutée. Voir [Lecture renouvelée de sources relationnelles](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Performances et réglage
Consultez [copie activité optimiser les performances et Guide d’optimisation](data-factory-copy-activity-performance.md) toolearn sur la clé de facteurs d’affecter les performances de transfert de données (activité de copie) dans Azure Data Factory et de différentes façons toooptimize il.
