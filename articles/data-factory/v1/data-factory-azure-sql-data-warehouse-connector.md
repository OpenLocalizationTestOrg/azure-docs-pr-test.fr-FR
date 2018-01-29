---
title: "Copie de données vers/à partir d’Azure SQL Data Warehouse | Microsoft Docs"
description: "Découvrez comment copier des données vers et à partir d’Azure SQL Data Warehouse à l’aide d’Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: d90fa9bd-4b79-458a-8d40-e896835cfd4a
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2018
ms.author: jingwang
robots: noindex
ms.openlocfilehash: 97782d1437f47a5ec403a98464d38961874d7575
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/23/2018
---
# <a name="copy-data-to-and-from-azure-sql-data-warehouse-using-azure-data-factory"></a>Copier des données vers et à partir d’Azure SQL Data Warehouse à l’aide d’Azure Data Factory
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1 - Disponibilité générale](data-factory-azure-sql-data-warehouse-connector.md)
> * [Version 2 - Préversion](../connector-azure-sql-data-warehouse.md)

> [!NOTE]
> Cet article s’applique à la version 1 de Data factory, qui est généralement disponible (GA). Si vous utilisez la version 2 de Data Factory, disponible en préversion, consultez [Connecteur Azure SQL Data Warehouse dans V2](../connector-azure-sql-data-warehouse.md).

Cet article explique comment utiliser l’activité de copie dans Azure Data Factory pour déplacer des données vers ou à partir d’Azure SQL Data Warehouse. Il s’appuie sur l’article [Activités de déplacement des données](data-factory-data-movement-activities.md), qui présente une vue d’ensemble du déplacement de données avec l’activité de copie.  

> [!TIP]
> Pour obtenir les meilleures performances, utilisez PolyBase pour charger des données dans Azure SQL Data Warehouse. Pour plus de détails, consultez [Utiliser PolyBase pour charger des données dans Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) . Consultez [Charger 1 To dans Azure SQL Data Warehouse en moins de 15 minutes avec Azure Data Factory](data-factory-load-sql-data-warehouse.md) pour obtenir une procédure pas à pas avec un cas d’utilisation.

## <a name="supported-scenarios"></a>Scénarios pris en charge
Vous pouvez copier des données depuis **Azure SQL Data Warehouse** vers les magasins de données suivants :

[!INCLUDE [data-factory-supported-sinks](../../../includes/data-factory-supported-sinks.md)]

Vous pouvez copier des données depuis les magasins de données suivants **vers Azure SQL Data Warehouse** :

[!INCLUDE [data-factory-supported-sources](../../../includes/data-factory-supported-sources.md)]

> [!TIP]
> Lors de la copie de données à partir de SQL Server ou d’Azure SQL Data Warehouse dans Azure SQL Data Warehouse, si la table n’existe pas dans le magasin de destination, Data Factory peut automatiquement créer la table dans SQL Data Warehouse en utilisant le schéma de la table dans le magasin de données source. Consultez [Création automatique de la table](#auto-table-creation) pour plus d’informations.

## <a name="supported-authentication-type"></a>Type d’authentification pris en charge
Le connecteur Azure SQL Data Warehouse prend en charge l’authentification de base.

## <a name="getting-started"></a>Prise en main
Vous pouvez créer un pipeline avec une activité de copie qui déplace les données vers/depuis Azure SQL Data Warehouse à l’aide de différents outils/API.

Le moyen le plus simple de créer un pipeline qui copie les données vers/depuis le Azure SQL Data Warehouse consiste à utiliser l’Assistant Copier des données. Consultez la page [Didacticiel : charger des données dans SQL Data Warehouse avec Data Factory](../../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md) pour un bref aperçu sur la création d’un pipeline à l’aide de l’Assistant copie de données.

Vous pouvez également utiliser les outils suivants pour créer un pipeline : le **portail Azure**, **Visual Studio**, **Azure PowerShell**, le **modèle Azure Resource Manager**, l’**API .NET** et l’**API REST**. Pour obtenir des instructions détaillées sur la création d’un pipeline avec une activité de copie, consultez le [didacticiel sur l’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

Que vous utilisiez des outils ou des API, la création d’un pipeline qui déplace les données d’un magasin de données source vers un magasin de données récepteur implique les étapes suivantes :

1. Création d'une **fabrique de données**. Une fabrique de données peut contenir un ou plusieurs pipelines. 
2. Création de **services liés** pour lier les magasins de données d’entrée et de sortie à votre fabrique de données. Par exemple, si vous copiez des données depuis un stockage d’objets blob Azure vers un entrepôt de données SQL Azure, vous créez deux services liés pour lier votre compte de stockage Azure et Azure SQL Data Warehouse à votre fabrique de données. Pour les propriétés du service lié qui sont spécifiques à Azure SQL Data Warehouse, consultez la section [propriétés du service lié](#linked-service-properties). 
3. Création de **jeux de données** pour représenter les données d’entrée et de sortie de l’opération de copie. Dans l’exemple mentionné dans la dernière étape, vous créez un jeu de données pour spécifier le conteneur d’objets blob et le dossier qui contient les données d’entrée. Vous créez aussi un autre jeu de données pour spécifier la table dans l’entrepôt de données SQL Azure qui contient les données copiées depuis le stockage d’objets blob. Pour les propriétés du jeu de données qui sont spécifiques à Azure SQL Data Warehouse, consultez la section [propriétés du jeu de données](#dataset-properties).
4. Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie. Dans l’exemple mentionné plus haut, vous utilisez BlobSource comme source et SqlDWSink comme récepteur pour l’activité de copie. De même, si vous copiez depuis Azure SQL Data Warehouse vers Stockage Blob Azure, vous utilisez SqlDWSource et BlobSink dans l’activité de copie. Pour les propriétés de l’activité de copie qui sont spécifiques à Azure SQL Data Warehouse, consultez la section [propriétés de l’activité de copie](#copy-activity-properties). Pour plus d’informations sur l’utilisation d’un magasin de données comme source ou comme récepteur, cliquez sur le lien de la section précédente de votre magasin de données.

Lorsque vous utilisez l’Assistant, les définitions JSON de ces entités Data Factory (services liés, jeux de données et pipeline) sont automatiquement créées pour vous. Lorsque vous utilisez des outils/API (à l’exception de l’API .NET), vous devez définir ces entités Data Factory au format JSON.  Pour obtenir des exemples comportant des définitions JSON pour les entités Data Factory utilisées pour copier les données vers ou à partir d’Azure SQL Data Warehouse, consultez la section [Exemples JSON](#json-examples-for-copying-data-to-and-from-sql-data-warehouse) de cet article.

Les sections suivantes offrent des informations détaillées sur les propriétés JSON utilisées pour définir les entités Data Factory propres à Azure SQL Data Warehouse :

## <a name="linked-service-properties"></a>Propriétés du service lié
Le tableau suivant fournit la description des éléments JSON spécifiques au service lié Azure SQL Data Warehouse.

| Propriété | DESCRIPTION | Obligatoire |
| --- | --- | --- |
| Type |La propriété de type doit être définie sur **AzureSqlDW** |OUI |
| connectionString |Spécifier les informations requises pour la connexion à l’instance Azure SQL Data Warehouse pour la propriété connectionString. Seule l’authentification de base est prise en charge. |OUI |

> [!IMPORTANT]
> Configurez le [pare-feu Azure SQL Database](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) et le serveur de base de données pour [autoriser les services Azure à accéder au serveur](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure). En outre, si vous copiez des données vers Azure SQL Data Warehouse à partir d’un emplacement situé en dehors d’Azure, y compris à partir de sources de données locales avec la passerelle de la fabrique de données, configurez la plage d’adresses IP appropriée pour l’ordinateur qui envoie des données à Azure SQL Data Warehouse.

## <a name="dataset-properties"></a>Propriétés du jeu de données
Pour obtenir une liste complète des sections et propriétés disponibles pour la définition de jeux de données, consultez l’article [Création de jeux de données](data-factory-create-datasets.md). Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données (SQL Azure, Azure Blob, Azure Table, etc.).

La section typeProperties est différente pour chaque type de jeu de données et fournit des informations sur l'emplacement des données dans le magasin de données. La section **typeProperties** du jeu de données de type **AzureSqlDWTable** a les propriétés suivantes :

| Propriété | DESCRIPTION | Obligatoire |
| --- | --- | --- |
| TableName |Nom de la table ou de la vue dans la base de données Azure SQL Data Warehouse à laquelle le service lié fait référence. |OUI |

## <a name="copy-activity-properties"></a>Propriétés de l’activité de copie
Pour obtenir la liste complète des sections et des propriétés disponibles pour la définition des activités, consultez l’article [Création de pipelines](data-factory-create-pipelines.md). Les propriétés comme le nom, la description, les tables d’entrée et de sortie et la stratégie sont disponibles pour tous les types d’activités.

> [!NOTE]
> L'activité de copie accepte uniquement une entrée et produit une seule sortie.

En revanche, les propriétés disponibles dans la section typeProperties de l’activité varient pour chaque type d'activité. Pour l’activité de copie, elles dépendent des types de sources et récepteurs.

### <a name="sqldwsource"></a>SqlDWSource
Lorsque la source est de type **SqlDWSource**, les propriétés suivantes sont disponibles dans la section **typeProperties** :

| Propriété | DESCRIPTION | Valeurs autorisées | Obligatoire |
| --- | --- | --- | --- |
| SqlReaderQuery |Utilise la requête personnalisée pour lire des données. |Chaîne de requête SQL. Par exemple : select * from MyTable. |Non  |
| sqlReaderStoredProcedureName |Nom de la procédure stockée qui lit les données de la table source. |Nom de la procédure stockée. La dernière instruction SQL doit être une instruction SELECT dans la procédure stockée. |Non  |
| storedProcedureParameters |Paramètres de la procédure stockée. |Paires nom/valeur. Les noms et la casse des paramètres doivent correspondre aux noms et à la casse des paramètres de la procédure stockée. |Non  |

Si **sqlReaderQuery** est spécifié pour SqlDWSource, l'activité de copie exécute cette requête en fonction de la source Azure SQL Data Warehouse pour obtenir les données.

Vous pouvez également spécifier une procédure stockée en indiquant **sqlReaderStoredProcedureName** et **storedProcedureParameters** (si la procédure stockée accepte des paramètres).

Si vous ne spécifiez pas sqlReaderQuery ou sqlReaderStoredProcedureName, les colonnes définies dans la section Structure du jeu de données JSON sont utilisées pour créer une requête à exécuter sur Azure SQL Data Warehouse. Exemple : `select column1, column2 from mytable`. Si la définition du jeu de données ne possède pas de structure, toutes les colonnes de la table sont sélectionnées.

#### <a name="sqldwsource-example"></a>Exemple SqlDWSource

```JSON
"source": {
    "type": "SqlDWSource",
    "sqlReaderStoredProcedureName": "CopyTestSrcStoredProcedureWithParameters",
    "storedProcedureParameters": {
        "stringData": { "value": "str3" },
        "identifier": { "value": "$$Text.Format('{0:yyyy}', SliceStart)", "type": "Int"}
    }
}
```
**Définition de la procédure stockée :**

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

### <a name="sqldwsink"></a>SqlDWSink
**SqlDWSink** prend en charge les propriétés suivantes :

| Propriété | DESCRIPTION | Valeurs autorisées | Obligatoire |
| --- | --- | --- | --- |
| sqlWriterCleanupScript |Spécifiez une requête pour exécuter l’activité de copie afin que les données d’un segment spécifique soient nettoyées. Consultez la [section sur la répétition](#repeatability-during-copy)pour plus de détails. |Une instruction de requête. |Non  |
| allowPolyBase |Indique s’il faut utiliser PolyBase (le cas échéant) au lieu du mécanisme BULKINSERT. <br/><br/> **L’utilisation de PolyBase est la méthode recommandée pour charger des données dans SQL Data Warehouse.** Reportez-vous à la section [Utiliser PolyBase pour charger des données dans Azure SQL Data Warehouse](#use-polybase-to-load-data-into-azure-sql-data-warehouse) pour connaître les contraintes et les détails. |True  <br/>False (valeur par défaut) |Non  |
| polyBaseSettings |Groupe de propriétés pouvant être spécifié lorsque la propriété **allowPolybase** est définie sur **true**. |&nbsp; |Non  |
| rejectValue |Spécifie le nombre ou le pourcentage de lignes pouvant être rejetées avant l’échec de la requête. <br/><br/>Pour en savoir plus sur les options de rejet de PolyBase dans la section **Arguments** de la rubrique [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) (Créer une table externe (Transact-SQL)). |0 (par défaut), 1, 2, … |Non  |
| rejectType |Spécifie si l’option rejectValue est spécifiée comme une valeur littérale ou un pourcentage. |Value (par défaut), Percentage |Non  |
| rejectSampleValue |Détermine le nombre de lignes à extraire avant que PolyBase recalcule le pourcentage de lignes rejetées. |1, 2, … |Oui, si le **rejectType** est **percentage** |
| useTypeDefault |Spécifie comment gérer les valeurs manquantes dans les fichiers texte délimités lorsque PolyBase extrait des données à partir du fichier texte.<br/><br/>Pour plus d’informations sur cette propriété, consultez la section Arguments dans [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx). |True, False (par défaut) |Non  |
| writeBatchSize |Insère des données dans la table SQL lorsque la taille du tampon atteint writeBatchSize |Nombre entier (nombre de lignes) |Non (valeur par défaut : 10000) |
| writeBatchTimeout |Temps d’attente pour que l’opération d’insertion de lot soit terminée avant d’expirer. |intervalle de temps<br/><br/> Exemple : « 00:30:00 » (30 minutes). |Non  |

#### <a name="sqldwsink-example"></a>Exemple SqlDWSink

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true
}
```

## <a name="use-polybase-to-load-data-into-azure-sql-data-warehouse"></a>Utiliser PolyBase pour charger des données dans Azure SQL Data Warehouse
L’utilisation de **[PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)** est un moyen efficace de charger de grandes quantités de données dans Azure SQL Data Warehouse avec un débit élevé. Vous pouvez profiter d’un gain important de débit en utilisant PolyBase au lieu du mécanisme BULKINSERT par défaut. Consultez [copier le numéro de référence des performances](data-factory-copy-activity-performance.md#performance-reference) qui contient une comparaison détaillée. Consultez [Charger 1 To dans Azure SQL Data Warehouse en moins de 15 minutes avec Azure Data Factory](data-factory-load-sql-data-warehouse.md) pour obtenir une procédure pas à pas avec un cas d’utilisation.

* Si votre source de données se trouve dans **Stockage Blob Azure ou Azure Data Lake Store**, et si le format est compatible avec PolyBase, vous pouvez la copier directement vers Azure SQL Data Warehouse à l’aide de PolyBase. Consultez **[Copie directe à l’aide de PolyBase](#direct-copy-using-polybase)**.
* Si votre banque de données sources et son format ne sont pas pris en charge à l’origine par PolyBase, vous pouvez utiliser la fonctionnalité **[Copie intermédiaire avec PolyBase](#staged-copy-using-polybase)** à la place. Elle propose également un meilleur débit en convertissant les données dans un format compatible avec PolyBase et en stockant les données dans le stockage Blob Azure automatiquement. Il charge ensuite les données dans SQL Data Warehouse.

Définissez la propriété `allowPolyBase` sur **true** comme indiqué dans l’exemple suivant pour Azure Data Factory pour utiliser PolyBase afin de copier les données à partir du stockage d’objets Blob Azure vers Azure SQL Data Warehouse. Lorsque vous définissez allowPolyBase sur true, vous pouvez spécifier des propriétés PolyBase spécifiques à l’aide du groupe de propriétés `polyBaseSettings`. Reportez-vous à la section [SqlDWSink](#SqlDWSink) pour plus d’informations sur les propriétés que vous pouvez utiliser avec polyBaseSettings.

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true,
    "polyBaseSettings":
    {
        "rejectType": "percentage",
        "rejectValue": 10.0,
        "rejectSampleValue": 100,
        "useTypeDefault": true
    }
}
```

### <a name="direct-copy-using-polybase"></a>Copie directe à l’aide de PolyBase
SQL Data Warehouse PolyBase prend directement en charge Stockage Blob Azure et Azure Data Lake Store (à l’aide du principal du service) en tant que source et avec des exigences de format de fichier spécifiques. Si vos données source répondent aux critères décrits dans cette section, vous pouvez les copier directement du magasin de données source vers Azure SQL Data Warehouse à l’aide de PolyBase. Sinon, vous pouvez utiliser la méthode [Copie intermédiaire à l’aide de PolyBase](#staged-copy-using-polybase).

> [!TIP]
> Pour copier des données de Data Lake Store vers SQL Data Warehouse efficacement, voir [Azure Data Factory makes it even easier and convenient to uncover insights from data when using Data Lake Store with SQL Data Warehouse](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/) (Azure Data Factory facilite et rend plus pratique la découverte d’informations à partir de données lors de l’utilisation de Data Lake Store avec SQL Data Warehouse).

Si les critères ne sont pas remplis, Azure Data Factory contrôle les paramètres et rétablit automatiquement le mécanisme BULKINSERT pour le déplacement des données.

1. Le **service lié de la source** est de type : **AzureStorage** ou **AzureDataLakeStore avec authentification du principal de service**.  
2. Le **jeu de données d’entrée** est de type **AzureBlob** ou **AzureDataLakeStore**, et le type de format dans les propriétés `type` est **OrcFormat**, **ParquetFormat** ou **TextFormat** avec les configurations suivantes :

   1. `rowDelimiter` doit être **\n**.
   2. `nullValue` est défini sur **chaîne vide** ("") ou `treatEmptyAsNull` est défini sur **true**.
   3. `encodingName` est défini sur **utf-8**, qui est la valeur **par défaut**.
   4. `escapeChar`, `quoteChar`, `firstRowAsHeader` et `skipLineCount` ne sont pas spécifiés.
   5. `compression` peut être **aucune compression**, **GZip** ou **Deflate**.

    ```JSON
    "typeProperties": {
       "folderPath": "<blobpath>",
       "format": {
           "type": "TextFormat",     
           "columnDelimiter": "<any delimiter>",
           "rowDelimiter": "\n",       
           "nullValue": "",           
           "encodingName": "utf-8"    
       },
       "compression": {  
           "type": "GZip",  
           "level": "Optimal"  
       }  
    },
    ```

3. Il n’y a aucun paramètre `skipHeaderLineCount` sous **BlobSource** ou **AzureDataLakeStore** pour l’activité de copie dans le pipeline.
4. Il n’y a aucun paramètre `sliceIdentifierColumnName` sous **SqlDWSink** pour l’activité de copie dans le pipeline. (PolyBase garantit que toutes les données sont mises à jour ou que rien n’est mis à jour en une seule exécution. Pour définir la **répétabilité**, vous pouvez utiliser `sqlWriterCleanupScript`.
5. Il n’y a pas de `columnMapping` utilisé dans l’activité de copie associée.

### <a name="staged-copy-using-polybase"></a>Copie intermédiaire à l’aide de PolyBase
Lorsque vos données source ne répondent pas aux critères présentés dans la section précédente, vous pouvez activer la copie des données par le biais d’un Stockage Blob Azure intermédiaire (il ne peut pas s’agir d’une offre Stockage Premium). Dans ce cas, Azure Data Factory effectue automatiquement des transformations sur les données pour répondre aux exigences de format de données de PolyBase, utilise PolyBase pour charger les données dans SQL Data Warehouse puis supprime les données temporaires du Stockage Blob. Consultez la rubrique [Copie intermédiaire](data-factory-copy-activity-performance.md#staged-copy) pour plus d’informations sur le fonctionnement général de la copie des données par le biais d’un Blob Azure.

> [!NOTE]
> Lors de la copie de données à partir d’un magasin de données local dans Azure SQL Data Warehouse à l’aide de PolyBase et du stockage intermédiaire, si la version de votre passerelle de gestion des données est antérieure à la version 2.4, vous devez installer JRE (Java Runtime Environment) sur votre ordinateur passerelle, qui est utilisé pour convertir vos données source dans le bon format. Nous vous conseillons de mettre à niveau votre passerelle vers la dernière version pour éviter une telle dépendance.
>

Pour utiliser cette fonctionnalité, vous devez créer un [service lié Azure Storage](data-factory-azure-blob-connector.md#azure-storage-linked-service) qui fait référence au compte de stockage Azure qui comprend le stockage d’objets blob intermédiaire, puis spécifier les propriétés `enableStaging` et `stagingSettings` de l’activité de copie, comme indiqué dans le code suivant :

```json
"activities":[  
{
    "name": "Sample copy activity from SQL Server to SQL Data Warehouse via PolyBase",
    "type": "Copy",
    "inputs": [{ "name": "OnpremisesSQLServerInput" }],
    "outputs": [{ "name": "AzureSQLDWOutput" }],
    "typeProperties": {
        "source": {
            "type": "SqlSource",
        },
        "sink": {
            "type": "SqlDwSink",
            "allowPolyBase": true
        },
        "enableStaging": true,
        "stagingSettings": {
            "linkedServiceName": "MyStagingBlob"
        }
    }
}
]
```

## <a name="best-practices-when-using-polybase"></a>Meilleures pratiques lors de l’utilisation de PolyBase
Les sections suivantes contiennent des bonnes pratiques qui s’ajoutent à celles mentionnées dans [Bonnes pratiques pour Azure SQL Data Warehouse](../../sql-data-warehouse/sql-data-warehouse-best-practices.md).

### <a name="required-database-permission"></a>Autorisation de base de données requise
Pour utiliser PolyBase, il est nécessaire que l’utilisateur utilisé pour charger des données dans SQL Data Warehouse ait [l’autorisation « CONTROL »](https://msdn.microsoft.com/library/ms191291.aspx) sur la base de données cible. Vous pouvez, pour cela, ajouter l’utilisateur en tant que membre du rôle « db_owner ». Découvrez comment procéder dans [cette section](../../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization).

### <a name="row-size-and-data-type-limitation"></a>Limitations en matière de taille de ligne et de type de données
Les charges Polybase sont limitées au chargement de lignes de moins de **1 Mo** et ne peuvent pas charger vers VARCHR(MAX), NVARCHAR(MAX) ou VARBINARY(MAX). Consultez cette [section](../../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads).

Si les données source dont vous disposez ont des lignes d’une taille supérieure à 1 Mo, vous pouvez fractionner verticalement les tables source en plusieurs tables plus petites dans lesquelles la taille de ligne maximale ne dépasse pas la limite. Vous pouvez ensuite charger les tables plus petites à l’aide de PolyBase et les fusionner dans Azure SQL Data Warehouse.

### <a name="sql-data-warehouse-resource-class"></a>Classe de ressources SQL Data Warehouse
Pour obtenir le meilleur débit possible, envisagez d’attribuer une classe de ressources plus volumineuse à l’utilisateur utilisé pour charger des données dans SQL Data Warehouse via PolyBase. Découvrez comment procéder en consultant [Exemple de modification d’une classe de ressources utilisateur](../../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md).

### <a name="tablename-in-azure-sql-data-warehouse"></a>tableName dans Azure SQL Data Warehouse
Le tableau suivant fournit des exemples sur la façon de spécifier la propriété **tableName** dans le jeu de données JSON pour différentes combinaisons de schémas et noms de table.

| Schéma BD | Nom de la table | Propriété JSON tableName |
| --- | --- | --- |
| dbo |MyTable |MyTable ou dbo.MyTable ou [dbo].[MyTable] |
| dbo1 |MyTable |dbo1.MyTable ou [dbo1].[MyTable] |
| dbo |My.Table |[My.Table] ou [dbo].[My.Table] |
| dbo1 |My.Table |[dbo1].[My.Table] |

Si vous voyez l’erreur suivante, il peut s’agir d’un problème avec la valeur spécifiée pour la propriété tableName. Consultez le tableau pour savoir comment spécifier des valeurs pour la propriété JSON tableName.  

```
Type=System.Data.SqlClient.SqlException,Message=Invalid object name 'stg.Account_test'.,Source=.Net SqlClient Data Provider
```

### <a name="columns-with-default-values"></a>Colonnes avec des valeurs par défaut
Actuellement, la fonctionnalité PolyBase dans Data Factory accepte seulement le même nombre de colonnes que la table cible. Par exemple, vous avez une table avec quatre colonnes et l’une d’elles est définie avec une valeur par défaut. Les données d’entrée doivent toujours contenir quatre colonnes. La fourniture d’un jeu de données d’entrée de 3 colonnes produirait une erreur semblable au message suivant :

```
All columns of the table must be specified in the INSERT BULK statement.
```
La valeur NULL est une forme spéciale de valeur par défaut. Si la colonne accepte la valeur Null, les données d’entrée (dans l’objet blob) de cette colonne peuvent être vides (ne peuvent pas être absentes du jeu de données d’entrée). PolyBase insère NULL pour ces données dans Azure SQL Data Warehouse.  

## <a name="auto-table-creation"></a>Création automatique de la table
Si vous utilisez l’assistant de copie pour copier des données à partir de SQL Server ou d’Azure SQL Data Warehouse dans Azure SQL Data Warehouse et que la table qui correspond à la table source n’existe pas dans le magasin de destination, Data Factory peut automatiquement créer la table dans SQL Data Warehouse en utilisant le schéma de table source.

Data Factory crée la table dans le magasin de destination portant le même nom de table dans le magasin de données source. Les types de données des colonnes sont choisis en fonction du mappage de type suivant. Si nécessaire, des conversions de type sont effectuées pour corriger les éventuelles incompatibilités entre les magasins source et de destination. Il utilise également la distribution de tables en tourniquet (Round Robin).

| Type de colonne SQL Database source | Type de colonne SQL DW de destination (limite de taille) |
| --- | --- |
| Int | Int |
| BigInt | BigInt |
| SmallInt | SmallInt |
| TinyInt | TinyInt |
| Bit | Bit |
| Décimal | Décimal |
| Chiffre | Décimal |
| Float | Float |
| Money | Money |
| Real | Real |
| SmallMoney | SmallMoney |
| Binary | Binary |
| Varbinary | Varbinary (jusqu’à 8 000) |
| Date | Date |
| Datetime | Datetime |
| DateTime2 | DateTime2 |
| Temps | Temps |
| DatetimeOffset | DatetimeOffset |
| SmallDateTime | SmallDateTime |
| Texte | Varchar (jusqu'à 8 000) |
| NText | NVarChar (jusqu'à 4 000) |
| Image | VarBinary (jusqu'à 8 000) |
| UniqueIdentifier | UniqueIdentifier |
| Char | Char |
| NChar | NChar |
| VarChar | VarChar (jusqu'à 8 000) |
| NVarChar | NVarChar (jusqu'à 4 000) |
| xml | Varchar (jusqu'à 8 000) |

[!INCLUDE [data-factory-type-repeatability-for-sql-sources](../../../includes/data-factory-type-repeatability-for-sql-sources.md)]

## <a name="type-mapping-for-azure-sql-data-warehouse"></a>Mappage de type pour Azure SQL Data Warehouse
Comme mentionné dans l’article consacré aux [activités de déplacement des données](data-factory-data-movement-activities.md) , l’activité de copie convertit automatiquement les types source en types récepteur à l’aide de l’approche en 2 étapes suivante :

1. Conversion de types natifs source en types .NET
2. Conversion à partir du type .NET en type de récepteur natif

Lors du déplacement des données vers et à partir d’Azure SQL Data Warehouse, les mappages suivants sont utilisés à partir du type SQL vers le type .NET et vice-versa.

Le mappage est identique au [mappage du type de données SQL Server pour ADO.NET](https://msdn.microsoft.com/library/cc716729.aspx)(article en anglais).

| Type de moteur de base de données SQL Server | Type de .NET Framework |
| --- | --- |
| bigint |Int64 |
| binaire |Byte[] |
| bit |Booléen |
| char |String, Char[] |
| date |Datetime |
| DateTime |Datetime |
| datetime2 |Datetime |
| Datetimeoffset |DatetimeOffset |
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
| smalldatetime |Datetime |
| smallint |Int16 |
| smallmoney |Décimal |
| sql_variant |Objet * |
| text |String, Char[] |
| time |intervalle de temps |
| timestamp |Byte[] |
| tinyint |Byte |
| uniqueidentifier |Guid |
| varbinary |Byte[] |
| varchar |String, Char[] |
| xml |xml |

Vous pouvez également mapper les colonnes du jeu de données source sur les colonnes du jeu de données récepteur dans la définition de l’activité de copie. Pour plus d’informations, consultez [Mappage de colonnes de jeux de données dans Azure Data Factory](data-factory-map-columns.md).

## <a name="json-examples-for-copying-data-to-and-from-sql-data-warehouse"></a>Exemples JSON pour copier des données vers et depuis SQL Data Warehouse
Les exemples suivants présentent des exemples de définitions de JSON que vous pouvez utiliser pour créer un pipeline à l’aide [du Portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [de Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [d’Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Ils indiquent comment copier des données vers et depuis Azure SQL Data Warehouse et Azure Blob Storage. Toutefois, les données peuvent être copiées **directement** vers l’un des récepteurs indiqués [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) , via l’activité de copie de Microsoft Azure Data Factory.

### <a name="example-copy-data-from-azure-sql-data-warehouse-to-azure-blob"></a>Exemple : copie de données depuis Azure SQL Data Warehouse vers un objet Blob Azure
L’exemple définit les entités Data Factory suivantes :

1. Un service lié de type [AzureSqlDW](#linked-service-properties).
2. Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [AzureSqlDWTable](#dataset-properties).
4. Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [SqlDWSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

L’exemple copie toutes les heures les données temporelles (horaire, journalière, etc.) d’une table de base de données Azure SQL Data Warehouse vers un objet blob. Les propriétés JSON utilisées dans ces exemples sont décrites dans les sections suivant les exemples.

**Service lié Azure SQL Data Warehouse :**

```JSON
{
  "name": "AzureSqlDWLinkedService",
  "properties": {
    "type": "AzureSqlDW",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
**Service lié Azure Blob Storage :**

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
**Jeu de données d'entrée Azure SQL Data Warehouse :**

L'exemple suppose que vous avez créé une table « MyTable » dans Azure SQL Data Warehouse et qu'elle contient une colonne appelée « timestampcolumn » pour les données de série chronologique.

La définition de « external » : « true» informe le service Data Factory qu’il s’agit d’un jeu de données qui est externe à Data Factory et non produit par une activité dans Data Factory.

```JSON
{
  "name": "AzureSqlDWInput",
  "properties": {
    "type": "AzureSqlDWTable",
    "linkedServiceName": "AzureSqlDWLinkedService",
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
**Jeu de données de sortie d'objet Blob Azure :**

Les données sont écrites dans un nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1). Le chemin d’accès du dossier pour l’objet blob est évalué dynamiquement en fonction de l’heure de début du segment en cours de traitement. Le chemin d'accès du dossier utilise l'année, le mois, le jour et l'heure de l'heure de début.

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

**Activité de copie dans un pipeline avec SqlDWSource et BlobSink :**

Le pipeline contient une activité de copie qui est configurée pour utiliser les jeux de données d'entrée et de sortie, et qui est planifiée pour s'exécuter toutes les heures. Dans la définition du pipeline JSON, le type **source** est défini sur **SqlDWSource** et le type **sink** est défini sur **BlobSink**. La requête SQL spécifiée pour la propriété **SqlReaderQuery** sélectionne les données de la dernière heure à copier.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLDWtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSqlDWInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlDWSource",
            "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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
> [!NOTE]
> Dans l’exemple, **sqlReaderQuery** est spécifié pour SqlDWSource. L’activité de copie exécute cette requête sur la source Azure SQL Data Warehouse pour obtenir les données.
>
> Vous pouvez également spécifier une procédure stockée en indiquant **sqlReaderStoredProcedureName** et **storedProcedureParameters** (si la procédure stockée accepte des paramètres).
>
> Si vous ne spécifiez pas sqlReaderQuery ou sqlReaderStoredProcedureName, les colonnes définies dans la section structure du code JSON du jeu de données sont utilisées pour créer une requête (select column1, column2 from mytable) à exécuter sur Azure SQL Data Warehouse. Si la définition du jeu de données ne possède pas de structure, toutes les colonnes de la table sont sélectionnées.
>
>

### <a name="example-copy-data-from-azure-blob-to-azure-sql-data-warehouse"></a>Exemple : copie de données à partir d’un objet Blob Azure vers Azure SQL Data Warehouse
L’exemple définit les entités Data Factory suivantes :

1. Un service lié de type [AzureSqlDW](#linked-service-properties).
2. Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. un [jeu de données](data-factory-create-datasets.md) d'entrée de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureSqlDWTable](#dataset-properties).
5. Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) et [SqlDWSink](#copy-activity-properties).

L’exemple copie toutes les heures les données temporelles (horaire, journalière, etc.) d’un objet blob Azure vers une table de base de données Azure SQL Data Warehouse. Les propriétés JSON utilisées dans ces exemples sont décrites dans les sections suivant les exemples.

**Service lié Azure SQL Data Warehouse :**

```JSON
{
  "name": "AzureSqlDWLinkedService",
  "properties": {
    "type": "AzureSqlDW",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
**Service lié Azure Blob Storage :**

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
**Jeu de données d'entrée d'objet Blob Azure :**

Les données sont récupérées à partir d'un nouvel objet Blob toutes les heures (fréquence : heure, intervalle : 1). Le nom du chemin d'accès et du fichier de dossier pour l'objet blob sont évalués dynamiquement en fonction de l'heure de début du segment en cours de traitement. Le chemin d’accès du dossier utilise l’année, le mois et le jour de début et le nom de fichier utilise l’heure de début. Le paramètre « external » : « true » informe le service Data Factory que cette table est externe à la fabrique de données et n’est pas produite par une activité dans la fabrique de données.

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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
**Jeu de données de sortie Azure SQL Data Warehouse :**

L'exemple copie les données dans une table nommée « MyTable » dans Azure SQL Data Warehouse. Créez la table dans Azure SQL Data Warehouse avec le même nombre de colonnes que le fichier CSV d’objets blob doit en contenir. De nouvelles lignes sont ajoutées à la table toutes les heures.

```JSON
{
  "name": "AzureSqlDWOutput",
  "properties": {
    "type": "AzureSqlDWTable",
    "linkedServiceName": "AzureSqlDWLinkedService",
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
**Activité de copie dans un pipeline avec BlobSource et SqlDWSink :**

Le pipeline contient une activité de copie qui est configurée pour utiliser les jeux de données d'entrée et de sortie, et qui est planifiée pour s'exécuter toutes les heures. Dans la définition JSON du pipeline, le type **source** est défini sur **BlobSource** et le type **sink** est défini sur **SqlDWSink**.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQLDW",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlDWOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource",
            "blobColumnSeparators": ","
          },
          "sink": {
            "type": "SqlDWSink",
            "allowPolyBase": true
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
Pour une procédure pas à pas, voir [Charger 1 To dans Azure SQL Data Warehouse en moins de 15 minutes avec Azure Data Factory](data-factory-load-sql-data-warehouse.md) et l’article [Charger des données avec Azure Data Factory](../../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md) dans la documentation de SQL Data Warehouse.

## <a name="performance-and-tuning"></a>Performances et réglage
Consultez l’article [Guide sur les performances et le réglage de l’activité de copie](data-factory-copy-activity-performance.md) pour en savoir plus sur les facteurs clés affectant les performances de déplacement des données (activité de copie) dans Azure Data Factory et les différentes manières de les optimiser.
