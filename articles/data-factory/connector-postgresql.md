---
title: "Copier des données de PostgreSQL à l’aide d’Azure Data Factory | Microsoft Docs"
description: "Découvrez comment utiliser l’activité de copie dans un pipeline Azure Data Factory pour copier des données de PostgreSQL vers des banques de données réceptrices prises en charge."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: spelluru
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/18/2017
ms.author: jingwang
ms.openlocfilehash: f2670be1af310ecd57952465fdf7ebd21513eb63
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="copy-data-from-postgresql-by-using-azure-data-factory"></a>Copier des données de PostgreSQL à l’aide d’Azure Data Factory
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1 - Disponibilité générale](v1/data-factory-onprem-postgresql-connector.md)
> * [Version 2 - Préversion](connector-postgresql.md)

Cet article décrit comment utiliser l’activité de copie dans Azure Data Factory pour copier des données d’une base de données PostgreSQL. Il s’appuie sur l’article [présentant une vue d’ensemble de l’activité de copie](copy-activity-overview.md).


> [!NOTE]
> Cet article s’applique à la version 2 de Data Factory, actuellement en préversion. Si vous utilisez la version 1 du service Data Factory, qui est en Disponibilité générale, consultez [Connecteur PostgreSQL dans V1](v1/data-factory-onprem-postgresql-connector.md).

## <a name="supported-scenarios"></a>Scénarios pris en charge

Vous pouvez copier des données d’une base de données PostgreSQL vers toute banque de données réceptrice prise en charge. Pour obtenir la liste des banques de données prises en charge en tant que sources ou récepteurs par l’activité de copie, consultez le tableau [Banques de données prises en charge](copy-activity-overview.md#supported-data-stores-and-formats).

Plus précisément, ce connecteur PostgreSQL prend en charge PostgreSQL **version 7.4 et versions ultérieures**.

## <a name="prerequisites"></a>Composants requis

Pour utiliser ce connecteur PostgreSQL, vous devez :

- Configurer un runtime d’intégration auto-hébergé. Pour plus d’informations, voir l’article [Runtime d’intégration auto-hébergé](create-self-hosted-integration-runtime.md).
- Installer le [fournisseur de données Ngpsql pour PostgreSQL](http://go.microsoft.com/fwlink/?linkid=282716) 2.0.12 ou version ultérieure sur l’ordinateur exécutant le runtime d’intégration.

## <a name="getting-started"></a>Prise en main
Vous pouvez créer un pipeline avec l’activité de copie à l’aide du SDK .NET, du SDK Python, d’Azure PowerShell, de l’API REST ou du modèle Azure Resource Manager. Consultez le [Didacticiel de l’activité de copie](quickstart-create-data-factory-dot-net.md) pour obtenir des instructions détaillées sur la création d’un pipeline avec une activité de copie.

Les sections suivantes fournissent des informations sur les propriétés utilisées pour définir les entités Data Factory spécifiques du connecteur PostgreSQL.

## <a name="linked-service-properties"></a>Propriétés du service lié

Les propriétés prises en charge pour le service lié PostgreSQL sont les suivantes :

| Propriété | Description | Requis |
|:--- |:--- |:--- |
| type | La propriété type doit être définie sur **PostgreSql** | Oui |
| server | Nom du serveur PostgreSQL. |Oui |
| database | Nom de la base de données PostgreSQL. |Oui |
| schema | Nom du schéma dans la base de données. Le nom du schéma respecte la casse. |Non |
| username | Spécifiez le nom d’utilisateur à utiliser pour la connexion à la base de données PostgreSQL. |Oui |
| password | Spécifiez le mot de passe du compte d’utilisateur que vous avez spécifié pour le nom d’utilisateur. Marquez ce champ comme SecureString. |Oui |
| connectVia | [Runtime d’intégration](concepts-integration-runtime.md) à utiliser pour la connexion à la banque de données. Un Runtime d’intégration autohébergé est nécessaire comme indiqué dans [Prérequis](#prerequisites). |Oui |

**Exemple :**

```json
{
    "name": "PostgreSqlLinkedService",
    "properties": {
        "type": "PostgreSql",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "username": "<username>",
            "password": {
                "type": "SecureString",
                "value": "<password>"
            }
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

## <a name="dataset-properties"></a>Propriétés du jeu de données

Pour obtenir la liste complète des sections et propriétés disponibles pour la définition de jeux de données, consultez l’article sur les jeux de données. Cette section fournit la liste des propriétés prises en charge par le jeu de données PostgreSQL.

Pour copier des données de PostgreSQL, affectez la valeur **RelationalTable** à la propriété type du jeu de données. Les propriétés prises en charge sont les suivantes :

| Propriété | Description | Requis |
|:--- |:--- |:--- |
| type | La propriété type du jeu de données doit être définie sur **RelationalTable** | Oui |
| TableName | Nom de la table dans la base de données PostgreSQL. | Non (si « query » dans la source de l’activité est spécifié) |

**Exemple**

```json
{
    "name": "PostgreSQLDataset",
    "properties":
    {
        "type": "RelationalTable",
        "linkedServiceName": {
            "referenceName": "<PostgreSQL linked service name>",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {}
    }
}
```

## <a name="copy-activity-properties"></a>Propriétés de l’activité de copie

Pour obtenir la liste complète des sections et des propriétés disponibles pour la définition des activités, consultez l’article [Pipelines](concepts-pipelines-activities.md). Cette section fournit la liste des propriétés prises en charge par la source PostgreSQL.

### <a name="postgresql-as-source"></a>PostgreSQL en tant que source

Pour copier des données de PostgreSQL, définissez **RelationalSource** comme type de source dans l’activité de copie. Les propriétés prises en charge dans la section **source** de l’activité de copie sont les suivantes :

| Propriété | Description | Requis |
|:--- |:--- |:--- |
| type | La propriété type de la source d’activité de copie doit être définie sur **RelationalSource** | Oui |
| query | Utiliser la requête SQL personnalisée pour lire les données. Par exemple : `"query": "SELECT * FROM \"MySchema\".\"MyTable\""`. | Non (si « tableName » est spécifié dans dataset) |

> [!NOTE]
> Les noms de schéma et de table respectent la casse. Encadrez-les avec des guillemets doubles (`""`) dans la requête.

**Exemple :**

```json
"activities":[
    {
        "name": "CopyFromPostgreSQL",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<PostgreSQL input dataset name>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<output dataset name>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "RelationalSource",
                "query": "SELECT * FROM \"MySchema\".\"MyTable\""
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

## <a name="data-type-mapping-for-postgresql"></a>Mappage de type de données pour PostgreSQL

Lors de la copie de données de PostgreSQL, les mappages suivants sont utilisés entre les types de données PostgreSQL et les types de données intermédiaires d’Azure Data Factory. Pour découvrir comment l’activité de copie mappe le schéma et le type de données la source au récepteur, voir [Mappages de schémas et de types de données](copy-activity-schema-and-type-mapping.md).

| Type de données PostgreSQL | Alias PostgresSQL | Type de données intermédiaires de Data Factory |
|:--- |:--- |:--- |
| `abstime` | |`Datetime` | &nbsp;
| `bigint` | `int8` | `Int64` |
| `bigserial` | `serial8` | `Int64` |
| `bit [ (n) ]` | | `Byte[], String` | &nbsp;
| `bit varying [ (n) ]` | `varbit |Byte[], String` |
| `boolean` | `bool` | `Boolean` |
| `box` | | `Byte[], String` | &nbsp;
| `bytea` | | `Byte[], String` |&nbsp;
| `character [ (n) ]` | `char [ (n) ]` | `String` |
| `character varying [ (n) ]` | `varchar [ (n) ]` | `String` |
| `cid` | | `String` |&nbsp;
| `cidr` | | `String` |&nbsp;
| `circle` | |`Byte[], String` |&nbsp;
| `date` | |`Datetime` |&nbsp;
| `daterange` | |`String` |&nbsp;
| `double precision` |`float8` |`Double` |
| `inet` | |`Byte[], String` |&nbsp;
| `intarry` | |`String` |&nbsp;
| `int4range` | |`String` |&nbsp;
| `int8range` | |`String` |&nbsp;
| `integer` | `int, int4 |Int32` |
| `interval [ fields ] [ (p) ]` | | `Timespan` |&nbsp;
| `json` | | `String` |&nbsp;
| `jsonb` | | `Byte[]` |&nbsp;
| `line` | | `Byte[], String` |&nbsp;
| `lseg` | | `Byte[], String` |&nbsp;
| `macaddr` | | `Byte[], String` |&nbsp;
| `money` | | `Decimal` |&nbsp;
| `numeric [ (p, s) ]`|`decimal [ (p, s) ]` |`Decimal` |
| `numrange` | |`String` |&nbsp;
| `oid` | |`Int32` |&nbsp;
| `path` | |`Byte[], String` |&nbsp;
| `pg_lsn` | |`Int64` |&nbsp;
| `point` | |`Byte[], String` |&nbsp;
| `polygon` | |`Byte[], String` |&nbsp;
| `real` |`float4` |`Single` |
| `smallint` |`int2` |`Int16` |
| `smallserial` |`serial2` |`Int16` |
| `serial` |`serial4` |`Int32` |
| `text` | |`String` |&nbsp;


## <a name="next-steps"></a>Étapes suivantes
Pour obtenir la liste des banques de données prises en charge en tant que sources et récepteurs par l’activité de copie dans Azure Data Factory, consultez le tableau [banques de données prises en charge](copy-activity-overview.md##supported-data-stores-and-formats).