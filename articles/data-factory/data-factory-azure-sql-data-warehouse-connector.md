---
title: "les données d’aaaCopy vers/à partir de l’entrepôt de données SQL Azure | Documents Microsoft"
description: "Découvrez comment les données de toocopy vers/à partir de l’entrepôt de données SQL Azure à l’aide d’Azure Data Factory"
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
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 75bfcf3c99844fc1297ca500107da23cf875e41f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-azure-sql-data-warehouse-using-azure-data-factory"></a>Tooand de données de copie à partir de l’entrepôt de données SQL Azure à l’aide d’Azure Data Factory
Cet article explique comment toouse hello activité de copie de données de toomove Azure Data Factory vers/à partir d’Azure SQL Data Warehouse. Il repose sur hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, qui présente une vue d’ensemble du déplacement des données avec l’activité de copie hello.  

> [!TIP]
> tooachieve des meilleures performances, utilisez des données de tooload PolyBase dans Azure SQL Data Warehouse. Hello [PolyBase d’utilisation des données de tooload dans Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) section comporte des détails. Consultez [Charger 1 To dans Azure SQL Data Warehouse en moins de 15 minutes avec Azure Data Factory](data-factory-load-sql-data-warehouse.md) pour obtenir une procédure pas à pas avec un cas d’utilisation.

## <a name="supported-scenarios"></a>Scénarios pris en charge
Vous pouvez copier des données **à partir de l’entrepôt de données SQL Azure** toohello suivant des magasins de données :

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

Vous pouvez copier des données à partir de hello suivant des magasins de données **tooAzure SQL Data Warehouse**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!TIP]
> Lors de la copie des données à partir de SQL Server ou la base de données SQL Azure tooAzure SQL Data Warehouse, si la table de hello n’existe pas dans la banque de destination hello, Data Factory peut automatiquement créer les table hello dans l’entrepôt de données SQL à l’aide du schéma hello de table de hello dans la source de hello magasin de données. Consultez [Création automatique de la table](#auto-table-creation) pour plus d’informations.

## <a name="supported-authentication-type"></a>Type d’authentification pris en charge
Le connecteur Azure SQL Data Warehouse prend en charge l’authentification de base.

## <a name="getting-started"></a>Prise en main
Vous pouvez créer un pipeline avec une activité de copie qui déplace les données vers/depuis Azure SQL Data Warehouse à l’aide de différents outils/API.

toocreate de façon plus simple Hello un pipeline qui copie des données vers/depuis Azure SQL Data Warehouse est un Assistant de données copie toouse hello. Consultez [didacticiel : charger des données dans l’entrepôt de données SQL avec Data Factory](../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md) pour une procédure pas à pas rapides sur la création d’un pipeline à l’aide d’Assistant de données de copie hello.

Vous pouvez également utiliser hello suivant outils toocreate un pipeline : **portail Azure**, **Visual Studio**, **Azure PowerShell**, **modèle Azure Resource Manager** , **API .NET**, et **API REST**. Consultez [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions toocreate un pipeline avec une activité de copie.

Si vous utilisez hello ou une API, vous effectuez hello suivant les étapes toocreate un pipeline qui déplace la banque de données récepteur tooa du magasin de données à partir des données d’une source :

1. Création d'une **fabrique de données**. Une fabrique de données peut contenir un ou plusieurs pipelines. 
2. Créer **services liés** fabrique de données tooyour toolink les données d’entrée et de sortie magasins. Par exemple, si vous copiez des données à partir d’un entrepôt de données objet blob Azure storage tooan SQL Azure, vous créez deux services liés toolink votre compte de stockage Azure et SQL Azure data warehouse tooyour données factory. Pour les propriétés de service lié qui sont spécifique tooAzure SQL Data Warehouse, consultez [lié des propriétés du service](#linked-service-properties) section. 
3. Créer **datasets** toorepresent d’entrée et sortie l’opération de copie des données pour hello. Exemple hello mentionné dans la dernière étape de hello, vous permet de créer un conteneur d’objets blob de jeu de données toospecify hello et un dossier qui contient les données d’entrée hello. De plus, vous créez une autre table de hello toospecify jeu de données dans l’entrepôt de données SQL Azure hello qui contient les données hello copiées à partir du stockage d’objets blob hello. Pour les propriétés du dataset qui sont spécifique tooAzure SQL Data Warehouse, consultez [propriétés du dataset](#dataset-properties) section.
4. Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie. Dans l’exemple hello mentionné précédemment, vous utilisez BlobSource en tant que source et SqlDWSink comme un récepteur pour l’activité de copie hello. De même, si vous copiez à partir de l’entrepôt de données SQL Azure tooAzure stockage d’objets Blob, vous utilisez SqlDWSource et BlobSink dans l’activité de copie hello. Pour les propriétés d’activité de copie sont tooAzure spécifique SQL Data Warehouse, consultez [copier les propriétés de l’activité](#copy-activity-properties) section. Pour plus d’informations sur comment toouse du magasin de données source ou un récepteur, cliquez sur le lien hello dans la section précédente de hello pour votre magasin de données.

Lorsque vous utilisez hello Assistant, les définitions de JSON pour ces entités de fabrique de données (services liés, des datasets et pipeline de hello) sont créées automatiquement pour vous. Lorsque vous utilisez/API des outils (à l’exception des API .NET), vous définissez ces entités de fabrique de données à l’aide du format JSON de hello.  Pour plus d’exemples de définitions de JSON pour les entités de fabrique de données qui sont utilisées toocopy des données vers/à partir d’un entrepôt de données SQL Azure, consultez [exemples JSON](#json-examples-for-copying-data-to-and-from-sql-data-warehouse) section de cet article.

Hello les sections suivantes fournit des détails sur les propriétés JSON qui sont utilisés toodefine Data Factory entités spécifique tooAzure SQL Data Warehouse :

## <a name="linked-service-properties"></a>Propriétés du service lié
Hello tableau suivant fournit la description pour JSON éléments tooAzure spécifique service d’entrepôt de données SQL lié.

| Propriété | Description | Requis |
| --- | --- | --- |
| type |propriété de type Hello doit indiquer : **AzureSqlDW** |Oui |
| connectionString |Spécifiez les informations nécessaires d’instance d’Azure SQL Data Warehouse tooconnect toohello pour la propriété connectionString de hello. Seule l’authentification de base est prise en charge. |Oui |

> [!IMPORTANT]
> Configurer [pare-feu de base de données SQL Azure](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) et hello le serveur de base de données trop[autoriser les Services Azure tooaccess hello serveur](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure). En outre, si vous copiez des données tooAzure SQL Data Warehouse, notamment Azure externe à partir de sources de données locale avec la passerelle de fabrique de données, configurer la plage d’adresses IP approprié pour l’ordinateur hello qui envoie des données tooAzure SQL Data Warehouse.

## <a name="dataset-properties"></a>Propriétés du jeu de données
Pour obtenir une liste complète des sections et les propriétés disponibles pour définir des jeux de données, consultez hello [création de datasets](data-factory-create-datasets.md) l’article. Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données (SQL Azure, Azure Blob, Azure Table, etc.).

section de typeProperties Hello est différente pour chaque type de jeu de données et fournit des informations sur l’emplacement de hello de données hello dans le magasin de données hello. Hello **typeProperties** section hello le jeu de données de type **AzureSqlDWTable** a hello propriétés suivantes :

| Propriété | Description | Requis |
| --- | --- | --- |
| TableName |Nom de la table de hello ou une vue dans la base de données Azure SQL Data Warehouse hello qui hello service lié fait référence à. |Oui |

## <a name="copy-activity-properties"></a>Propriétés de l’activité de copie
Pour obtenir une liste complète des sections et les propriétés disponibles pour la définition d’activités, consultez hello [création de Pipelines](data-factory-create-pipelines.md) l’article. Les propriétés comme le nom, la description, les tables d’entrée et de sortie et la stratégie sont disponibles pour tous les types d’activités.

> [!NOTE]
> Hello activité de copie accepte uniquement une entrée et produit qu’une seule sortie.

Alors que les propriétés disponibles dans la section typeProperties hello activité hello varient selon chaque type d’activité. Pour l’activité de copie, ils varient selon les types de sources et récepteurs hello.

### <a name="sqldwsource"></a>SqlDWSource
Lorsque la source est de type **SqlDWSource**, hello propriétés suivantes est disponible dans **typeProperties** section :

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| SqlReaderQuery |Utiliser des données tooread hello requête personnalisée. |Chaîne de requête SQL. Par exemple : select * from MyTable. |Non |
| sqlReaderStoredProcedureName |Nom de hello procédure stockée qui lit les données à partir de la table de source de hello. |Nom de hello procédure stockée. instruction SQL de la dernière Hello doit être une instruction SELECT dans la procédure stockée hello. |Non |
| storedProcedureParameters |Pourquoi les paramètres de procédure stockée. |Paires nom/valeur. Noms et la casse des paramètres doivent correspondre à des noms de hello et la casse des paramètres de la procédure stockée hello. |Non |

Si hello **sqlReaderQuery** est spécifié pour hello SqlDWSource, hello activité de copie s’exécute cette requête par rapport à hello données de Azure SQL Data Warehouse source tooget hello.

Ou bien, vous pouvez spécifier une procédure stockée en spécifiant hello **sqlReaderStoredProcedureName** et **storedProcedureParameters** (si hello une procédure stockée accepte des paramètres).

Si vous ne spécifiez pas de sqlReaderQuery ou sqlReaderStoredProcedureName, les colonnes de hello définis dans la section de structure hello du jeu de données hello JSON sont utilisé toobuild un toorun de requête par rapport à hello Azure SQL Data Warehouse. Exemple : `select column1, column2 from mytable`. Si la définition de dataset hello n’a pas de structure de hello, toutes les colonnes sont sélectionnées à partir de la table de hello.

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

### <a name="sqldwsink"></a>SqlDWSink
**SqlDWSink** prend en charge hello propriétés suivantes :

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| sqlWriterCleanupScript |Spécifier une requête pour l’activité de copie tooexecute telles que les données d’un secteur spécifique sont nettoyées. Consultez la [section sur la répétition](#repeatability-during-copy)pour plus de détails. |Une instruction de requête. |Non |
| allowPolyBase |Indique si toouse PolyBase (le cas échéant) au lieu de mécanisme BULKINSERT. <br/><br/> **À l’aide de PolyBase est hello recommandé la façon dont les données tooload dans SQL Data Warehouse.** Consultez [PolyBase d’utilisation des données de tooload dans Azure SQL Data Warehouse](#use-polybase-to-load-data-into-azure-sql-data-warehouse) section pour les contraintes et les détails. |true <br/>False (valeur par défaut) |Non |
| polyBaseSettings |Un groupe de propriétés qui peuvent être spécifiés lorsque hello **allowPolybase** propriété a la valeur trop**true**. |&nbsp; |Non |
| rejectValue |Spécifie le nombre de hello ou un pourcentage de lignes peut être rejetée avant l’échec de la requête de hello. <br/><br/>En savoir plus sur de PolyBase hello rejettent options Bonjour **Arguments** section de [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) rubrique. |0 (par défaut), 1, 2, … |Non |
| rejectType |Spécifie si l’option de rejectValue hello est spécifiée comme une valeur littérale ou pourcentage. |Value (par défaut), Percentage |Non |
| rejectSampleValue |Détermine le nombre hello de lignes tooretrieve avant hello PolyBase recalcule le pourcentage de hello de lignes rejetées. |1, 2, … |Oui, si le **rejectType** est **percentage** |
| useTypeDefault |Spécifie comment toohandle manque des valeurs dans le fichiers texte délimités lorsque PolyBase récupère les données à partir du fichier de texte hello.<br/><br/>En savoir plus sur cette propriété à partir de la section Arguments hello [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx). |True, False (par défaut) |Non |
| writeBatchSize |Insère des données dans une table SQL de hello lorsque la taille de mémoire tampon de hello atteint la valeur writeBatchSize |Nombre entier (nombre de lignes) |Non (valeur par défaut : 10000) |
| writeBatchTimeout |Temps d’attente pour hello lot insert opération toocomplete avant d’expirer. |intervalle de temps<br/><br/> Exemple : « 00:30:00 » (30 minutes). |Non |

#### <a name="sqldwsink-example"></a>Exemple SqlDWSink

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true
}
```

## <a name="use-polybase-tooload-data-into-azure-sql-data-warehouse"></a>Utiliser des données de tooload PolyBase dans Azure SQL Data Warehouse
L’utilisation de **[PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)** est un moyen efficace de charger de grandes quantités de données dans Azure SQL Data Warehouse avec un débit élevé. Vous pouvez voir un grand gain un débit hello à l’aide de PolyBase au lieu de mécanisme BULKINSERT hello par défaut. Consultez [copier le numéro de référence des performances](data-factory-copy-activity-performance.md#performance-reference) qui contient une comparaison détaillée. Consultez [Charger 1 To dans Azure SQL Data Warehouse en moins de 15 minutes avec Azure Data Factory](data-factory-load-sql-data-warehouse.md) pour obtenir une procédure pas à pas avec un cas d’utilisation.

* Si votre source de données se trouve dans **objets Blob Azure ou Azure Data Lake Store**et format de hello est compatible avec PolyBase, vous pouvez copier directement tooAzure SQL Data Warehouse à l’aide de PolyBase. Consultez **[Copie directe à l’aide de PolyBase](#direct-copy-using-polybase)**.
* Si votre magasin de données source et le format n'est pas à l’origine PolyBase prend en charge, vous pouvez utiliser hello  **[copie intermédiaire à l’aide de PolyBase](#staged-copy-using-polybase)**  fonctionnalité à la place. Il fournit également un meilleur débit conversion des données de hello en format compatible avec PolyBase et le stockage des données de hello dans le stockage d’objets Blob Azure automatiquement. Il charge ensuite les données dans SQL Data Warehouse.

Ensemble hello `allowPolyBase` propriété trop**true** comme indiqué dans hello suivant l’exemple pour Azure Data Factory toouse PolyBase toocopy données dans Azure SQL Data Warehouse. Lorsque vous définissez allowPolyBase tootrue, vous pouvez spécifier les propriétés spécifiques de PolyBase à l’aide de hello `polyBaseSettings` groupe de propriétés. consultez hello [SqlDWSink](#SqlDWSink) pour plus d’informations sur les propriétés que vous pouvez utiliser avec polyBaseSettings.

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
SQL Data Warehouse PolyBase prend directement en charge Stockage Blob Azure et Azure Data Lake Store (à l’aide du principal du service) en tant que source et avec des exigences de format de fichier spécifiques. Si votre source de données répond aux critères de hello décrits dans cette section, vous pouvez copier directement à partir de tooAzure de magasin de données source que SQL Data Warehouse à l’aide de PolyBase. Sinon, vous pouvez utiliser la méthode [Copie intermédiaire à l’aide de PolyBase](#staged-copy-using-polybase).

> [!TIP]
> données toocopy Data Lake Store tooSQL l’entrepôt de données efficace, pour en savoir plus à partir de [Azure Data Factory permet même de vos données toouncover plus facile et pratique lors de l’utilisation de Data Lake Store avec l’entrepôt de données SQL](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/).

Si les exigences de hello ne sont pas remplies, Azure Data Factory vérifie les paramètres de hello et repasse automatiquement mécanisme BULKINSERT toohello hello déplacement des données.

1. Le **service lié de la source** est de type : **AzureStorage** ou **AzureDataLakeStore avec authentification du principal de service**.  
2. Hello **dataset d’entrée** est de type : **AzureBlob** ou **AzureDataLakeStore**, et hello du type de format sous `type` propriétés est **OrcFormat** , ou **TextFormat** avec hello suivant configurations :

   1. `rowDelimiter` doit être **\n**.
   2. `nullValue`est défini trop**une chaîne vide** (« »), ou `treatEmptyAsNull` est défini trop**true**.
   3. `encodingName`est défini trop**utf-8**, qui est **par défaut** valeur.
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

3. Il est sans `skipHeaderLineCount` sous **BlobSource** ou **AzureDataLakeStore** pourquoi l’activité de copie dans le pipeline de hello.
4. Il est sans `sliceIdentifierColumnName` sous **SqlDWSink** pourquoi l’activité de copie dans le pipeline de hello. (PolyBase garantit que toutes les données sont mises à jour ou que rien n’est mis à jour en une seule exécution. tooachieve **répétabilité**, vous pouvez utiliser `sqlWriterCleanupScript`).
5. Il existe aucune `columnMapping` utilisé Bonjour associé dans l’activité de copie.

### <a name="staged-copy-using-polybase"></a>Copie intermédiaire à l’aide de PolyBase
Lorsque vos données sources ne répond pas aux critères de hello introduites dans la section précédente de hello, vous pouvez activer la copie des données via un stockage d’objets Blob Azure mise en lots intermédiaire (ne peut pas être le stockage Premium). Dans ce cas, Azure Data Factory automatiquement effectue les transformations sur hello données toomeet données exigences relatives au format de PolyBase, puis utilisez PolyBase tooload données dans l’entrepôt de données SQL et enfin nettoyage vos données temporaires de stockage d’objets Blob hello. Consultez la rubrique [Copie intermédiaire](data-factory-copy-activity-performance.md#staged-copy) pour plus d’informations sur le fonctionnement général de la copie des données par le biais d’un Blob Azure.

> [!NOTE]
> Stocke une copie de données à partir d’un local de données dans Azure SQL Data Warehouse à l’aide de PolyBase et de mise en lots, si votre version de la passerelle de gestion des données est inférieur à 2.4, JRE (Java Runtime Environment) est requis sur votre passerelle lors de l’ordinateur qui est utilisé tootransform vos données sources dans le format approprié. Suggérer que vous mettez à niveau votre tooavoid de dernière toohello passerelle telle dépendance.
>

toouse cette fonctionnalité, créez un [service lié Azure Storage](data-factory-azure-blob-connector.md#azure-storage-linked-service) qui fait référence toohello compte de stockage Azure ayant un stockage temporaire blob hello, puis spécifiez hello `enableStaging` et `stagingSettings` propriétés pourquoi l’activité de copie comme indiqué dans hello suivant de code :

```json
"activities":[  
{
    "name": "Sample copy activity from SQL Server tooSQL Data Warehouse via PolyBase",
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
Hello sections suivantes fournissent plus toohello pratiques meilleures ceux qui sont mentionnés dans [meilleures pratiques pour Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md).

### <a name="required-database-permission"></a>Autorisation de base de données requise
toouse PolyBase, il requiert hello utilisateur en cours données tooload utilisés dans SQL Data Warehouse a hello [l’autorisation « Contrôle »](https://msdn.microsoft.com/library/ms191291.aspx) sur la base de données cible hello. Une façon tooachieve qui est tooadd cet utilisateur en tant que membre du rôle « db_owner ». Découvrez comment toodo qui en suivant [cette section](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization).

### <a name="row-size-and-data-type-limitation"></a>Limitations en matière de taille de ligne et de type de données
Polybase charges sont limités tooloading lignes à la fois plus petit que **1 Mo** et ne peut pas charger tooVARCHR(MAX), nvarchar (max) ou varbinary (max). Consultez trop[ici](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads).

Si vous avez des données sources avec des lignes d’une taille supérieure à 1 Mo, vous souhaiterez les tables sources toosplit hello verticalement en plusieurs petits où hello plus grande taille de ligne de chacun d’eux ne dépasse pas la limite de hello. les tables plus petites Hello peuvent ensuite être chargées à l’aide de PolyBase et fusionnées dans l’entrepôt de données SQL Azure.

### <a name="sql-data-warehouse-resource-class"></a>Classe de ressources SQL Data Warehouse
tooachieve meilleurs résultats possibles, envisagez de tooassign plus grande ressource classe toohello utilisateur en cours utilisé les données tooload dans l’entrepôt de données SQL via PolyBase. Découvrez comment toodo qui en suivant [modifier un exemple de classe de ressource utilisateur](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).

### <a name="tablename-in-azure-sql-data-warehouse"></a>tableName dans Azure SQL Data Warehouse
Hello tableau suivant fournit des exemples sur la façon de toospecify hello **tableName** propriété dans le jeu de données JSON pour différentes combinaisons de nom de schéma et une table.

| Schéma BD | Nom de la table | Propriété JSON tableName |
| --- | --- | --- |
| dbo |MyTable |MyTable ou dbo.MyTable ou [dbo].[MyTable] |
| dbo1 |MyTable |dbo1.MyTable ou [dbo1].[MyTable] |
| dbo |My.Table |[My.Table] ou [dbo].[My.Table] |
| dbo1 |My.Table |[dbo1].[My.Table] |

Si vous voyez hello l’erreur suivante, il peut être un problème avec la valeur hello spécifiée pour la propriété tableName de hello. Consultez la table hello pour les valeurs de toospecify hello méthode correcte pour la propriété JSON tableName hello.  

```
Type=System.Data.SqlClient.SqlException,Message=Invalid object name 'stg.Account_test'.,Source=.Net SqlClient Data Provider
```

### <a name="columns-with-default-values"></a>Colonnes avec des valeurs par défaut
Actuellement, PolyBase accepte uniquement les fonctionnalités dans la fabrique de données hello même nombre de colonnes dans la table cible hello. Par exemple, vous avez une table avec quatre colonnes et l’une d’elles est définie avec une valeur par défaut. les données d’entrée Hello doivent toujours contenir des quatre colonnes. En fournissant un jeu de données d’entrée 3-colonne produirait un toohello similaire erreur message suivant :

```
All columns of hello table must be specified in hello INSERT BULK statement.
```
La valeur NULL est une forme spéciale de valeur par défaut. Si la colonne de hello est nullable, données d’entrée hello (dans l’objet blob) pour cette colonne peut être vides (ne peut pas être manquant à partir du jeu de données d’entrée hello). PolyBase insère NULL pour les Bonjour Azure SQL Data Warehouse.  

## <a name="auto-table-creation"></a>Création automatique de la table
Si vous utilisez des données de toocopy Assistant copie de SQL Server ou de base de données SQL Azure tooAzure SQL Data Warehouse et hello la table qui correspond la table de source toohello n’existe pas dans la banque de destination hello, Data Factory peut créer automatiquement la table de hello Bonjour entrepôt de données à l’aide du schéma de la table source hello.

Fabrique de données crée la table de hello dans la banque de destination hello avec hello même nom dans le magasin de données source hello de la table. types de données Hello pour les colonnes sont choisies en fonction hello suivant le mappage de type. Si nécessaire, il effectue toofix des conversions de type les incompatibilités entre les magasins de source et de destination. Il utilise également la distribution de tables en tourniquet (Round Robin).

| Type de colonne SQL Database source | Type de colonne SQL DW de destination (limite de taille) |
| --- | --- |
| int | int |
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
| Fichier binaire | Fichier binaire |
| Varbinary | Varbinary (haut too8000) |
| Date | Date |
| DateTime | DateTime |
| DateTime2 | DateTime2 |
| Time | Time |
| Datetimeoffset | Datetimeoffset |
| SmallDateTime | SmallDateTime |
| Texte | Varchar (haut too8000) |
| NText | NVarChar (haut too4000) |
| Image | VarBinary (haut too8000) |
| UniqueIdentifier | UniqueIdentifier |
| Char | Char |
| NChar | NChar |
| VarChar | VarChar (haut too8000) |
| NVarChar | NVarChar (haut too4000) |
| xml | Varchar (haut too8000) |

[!INCLUDE [data-factory-type-repeatability-for-sql-sources](../../includes/data-factory-type-repeatability-for-sql-sources.md)]

## <a name="type-mapping-for-azure-sql-data-warehouse"></a>Mappage de type pour Azure SQL Data Warehouse
Comme mentionné dans hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, l’activité de copie effectue les conversions de type automatique à partir des types de sources de toosink types avec hello approche de l’étape 2 :

1. Convertir à partir de la source native types too.NET type
2. Conversion de type de récepteur de toonative de type .NET

Lorsque vous déplacez des données trop & à partir de l’entrepôt de données SQL Azure, hello mappages suivants sont utilisés à partir du type too.NET de type SQL et vice versa.

mappage de Hello est identique à celui hello [mappage des types de données SQL Server pour ADO.NET](https://msdn.microsoft.com/library/cc716729.aspx).

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

Vous pouvez également mapper des colonnes à partir de toocolumns du jeu de données source à partir de récepteur de jeu de données dans la définition d’activité de copie de hello. Pour plus d’informations, consultez [Mappage de colonnes de jeux de données dans Azure Data Factory](data-factory-map-columns.md).

## <a name="json-examples-for-copying-data-tooand-from-sql-data-warehouse"></a>Exemples JSON pour la copie des données tooand à partir de l’entrepôt de données SQL
Hello exemples suivants proposent des exemples de définitions de JSON que vous pouvez utiliser toocreate un pipeline à l’aide de [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Elles montrent comment toocopy les tooand de données de l’entrepôt de données SQL Azure et de stockage d’objets Blob Azure. Toutefois, les données peuvent être copiées **directement** de n’importe quelle tooany de sources de récepteurs hello indiqué [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) à l’aide de hello activité de copie dans Azure Data Factory.

### <a name="example-copy-data-from-azure-sql-data-warehouse-tooazure-blob"></a>Exemple : Copier des données à partir de l’entrepôt de données SQL Azure tooAzure Blob
exemple Hello définit hello suivant des entités de fabrique de données :

1. Un service lié de type [AzureSqlDW](#linked-service-properties).
2. Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [AzureSqlDWTable](#dataset-properties).
4. Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [SqlDWSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

exemple Hello copie les données de séries chronologiques (horaires, quotidiennes, etc.) à partir d’une table dans l’objet blob tooa de base de données Azure SQL Data Warehouse toutes les heures. propriétés JSON Hello utilisées dans ces exemples sont décrits dans les sections suivantes des exemples de hello.

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

exemple Hello suppose que vous avez créé une table « MyTable » dans l’entrepôt de données SQL Azure, et il contienne une colonne appelée « timestampcolumn » pour les données de série chronologique.

Paramètre « external » : « true » informe service Data Factory de hello ce jeu de données hello est la fabrique de données externe toohello et n’est pas généré par une activité dans la fabrique de données hello.

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
**Jeu de données de sortie Azure Blob :**

Les données sont écrites tooa nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1). chemin d’accès du dossier Hello pour l’objet blob de hello est évaluée dynamiquement en fonction de l’heure de début hello de tranche hello qui est en cours de traitement. chemin d’accès du dossier Hello utilise l’année, mois, jours et heures des parties de l’heure de début hello.

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

Hello pipeline contient une activité de copie qui est configuré toouse hello des jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures. Dans la définition JSON du pipeline hello, hello **source** type est défini trop**SqlDWSource** et **récepteur** type est défini trop**BlobSink**. la requête SQL Hello spécifiée pour hello **SqlReaderQuery** propriété sélectionne des données de hello Bonjour au-delà de toocopy d’heure.

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
> Dans l’exemple de hello, **sqlReaderQuery** est spécifié pour hello SqlDWSource. Hello activité de copie s’exécute cette requête contre hello données de Azure SQL Data Warehouse source tooget hello.
>
> Ou bien, vous pouvez spécifier une procédure stockée en spécifiant hello **sqlReaderStoredProcedureName** et **storedProcedureParameters** (si hello une procédure stockée accepte des paramètres).
>
> Si vous ne spécifiez pas de sqlReaderQuery ou sqlReaderStoredProcedureName, colonnes hello définis dans la section de structure hello du jeu de données hello JSON sont toobuild utilisé une requête (select column1, column2 dans MaTable) toorun contre hello Azure SQL Data Warehouse. Si la définition de dataset hello n’a pas de structure de hello, toutes les colonnes sont sélectionnées à partir de la table de hello.
>
>

### <a name="example-copy-data-from-azure-blob-tooazure-sql-data-warehouse"></a>Exemple : Copier des données d’objets Blob Azure tooAzure SQL Data Warehouse
exemple Hello définit hello suivant des entités de fabrique de données :

1. Un service lié de type [AzureSqlDW](#linked-service-properties).
2. Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. un [jeu de données](data-factory-create-datasets.md) d'entrée de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureSqlDWTable](#dataset-properties).
5. Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) et [SqlDWSink](#copy-activity-properties).

exemple Hello copie les données de série chronologique (horaire, quotidienne, etc.) à partir de la table de tooa d’objets blob Azure dans la base de données Azure SQL Data Warehouse toutes les heures. propriétés JSON Hello utilisées dans ces exemples sont décrits dans les sections suivantes des exemples de hello.

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

Les données sont récupérées à partir d'un nouvel objet Blob toutes les heures (fréquence : heure, intervalle : 1). nom de chemin d’accès et de dossier pour l’objet blob de hello Hello sont dynamiquement évaluées en fonction de l’heure de début hello de tranche hello qui est en cours de traitement. chemin d’accès du dossier Hello utilise la partie jour de l’heure de début hello, mois et année et nom de fichier partie d’heure hello de l’heure de début hello. « external » : « true » paramètre informe le service Data Factory de hello que cette table est la fabrique de données externe toohello et qu’il n’est pas générée par une activité dans la fabrique de données hello.

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

exemple Hello copie table tooa de données nommé « MyTable » dans l’entrepôt de données SQL Azure. Créer la table de hello dans Azure SQL Data Warehouse avec hello même nombre de colonnes comme vous le souhaitez toocontain de fichier CSV d’objets Blob hello. Nouvelles lignes sont ajoutées à la table de toohello toutes les heures.

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

Hello pipeline contient une activité de copie qui est configuré toouse hello des jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures. Dans la définition JSON du pipeline hello, hello **source** type est défini trop**BlobSource** et **récepteur** type est défini trop**SqlDWSink**.

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
Pour une procédure pas à pas, consultez hello [1 To de charge dans Azure SQL Data Warehouse moins de 15 minutes avec Azure Data Factory](data-factory-load-sql-data-warehouse.md) et [charger les données avec Azure Data Factory](../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md) article Bonjour Azure SQL Data Warehouse documentation.

## <a name="performance-and-tuning"></a>Performances et réglage
Consultez [copie activité optimiser les performances et Guide d’optimisation](data-factory-copy-activity-performance.md) toolearn sur la clé de facteurs d’affecter les performances de transfert de données (activité de copie) dans Azure Data Factory et de différentes façons toooptimize il.
