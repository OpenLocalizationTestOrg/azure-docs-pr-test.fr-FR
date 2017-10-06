---
title: "aaaMove des données de MySQL à l’aide d’Azure Data Factory | Documents Microsoft"
description: "Découvrez comment toomove les données de MySQL de base de données à l’aide d’Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 452f4fce-9eb5-40a0-92f8-1e98691bea4c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: jingwang
ms.openlocfilehash: 3ffe969e42ce1a54b265c4739df43fdc594ea891
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-mysql-using-azure-data-factory"></a>Déplacer des données depuis MySQL à l’aide d’Azure Data Factory
Cet article explique comment toouse hello activité de copie de données de toomove Azure Data Factory à partir d’une base de données MySQL locale. Il repose sur hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, qui présente une vue d’ensemble du déplacement des données avec l’activité de copie hello.

Vous pouvez copier les données d’une banque de données locale MySQL tooany pris en charge données magasin récepteur. Pour une liste de données pris en charge des magasins récepteurs par l’activité de copie hello, consultez hello [prise en charge des magasins de données](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table. Fabrique de données prend en charge uniquement le déplacement tooother les magasins de données du magasin de données à partir de données MySQL, mais ne pas pour déplacer des données d’une autre banque de données MySQL tooan données magasins. 

## <a name="prerequisites"></a>Composants requis
Service de fabrique de données prend en charge des sources de MySQL tooon local qui se connecte à l’aide de la passerelle de gestion des données de hello. Consultez [déplacement des données entre les emplacements locaux et cloud](data-factory-move-data-between-onprem-and-cloud.md) toolearn l’article sur la passerelle de gestion des données et des instructions détaillées sur la configuration de passerelle de hello.

Passerelle est requise même si la base de données MySQL hello est hébergé dans une machine virtuelle de Azure IaaS (VM). Vous pouvez installer la passerelle de hello sur hello même machine virtuelle en tant que données de hello stocker ou sur un ordinateur différent virtuel tant que passerelle de hello peuvent se connecter toohello de base de données.

> [!NOTE]
> Consultez [Résolution des problèmes de passerelle](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) pour obtenir des conseils sur la résolution des problèmes de connexion/passerelle.

## <a name="supported-versions-and-installation"></a>Versions prises en charge et installation
Pour toohello tooconnect de passerelle de gestion des données de la base de données MySQL, vous devez tooinstall hello [Connector/Net MySQL pour Microsoft Windows](https://dev.mysql.com/downloads/connector/net/) (version 6.6.5 ou version ultérieure) sur hello même système que hello passerelle de gestion des données. MySQL version 5.1 et ultérieures est pris en charge.

> [!TIP]
> Si vous rencontrez l’erreur « Échec de l’authentification, car la partie distante de hello a fermé hello flux de transport. », envisagez de tooupgrade hello version toohigher de Connector/Net MySQL.

## <a name="getting-started"></a>Prise en main
Vous pouvez créer un pipeline avec une activité de copie qui déplace les données d’un magasin de données Cassandra local à l’aide de différents outils/API. 

- toocreate de façon plus simple Hello un pipeline est toouse hello **Assistant copie de**. Consultez [didacticiel : créer un pipeline à l’aide d’Assistant copie de](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapides sur la création d’un pipeline à l’aide d’Assistant de données de copie hello. 
- Vous pouvez également utiliser hello suivant outils toocreate un pipeline : **portail Azure**, **Visual Studio**, **Azure PowerShell**, **modèle Azure Resource Manager** , **API .NET**, et **API REST**. Consultez [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions toocreate un pipeline avec une activité de copie. 

Si vous utilisez hello ou une API, vous effectuez hello suivant les étapes toocreate un pipeline qui déplace la banque de données récepteur tooa du magasin de données à partir des données d’une source :

1. Créer **services liés** fabrique de données tooyour toolink les données d’entrée et de sortie magasins.
2. Créer **datasets** toorepresent d’entrée et sortie l’opération de copie des données pour hello. 
3. Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie. 

Lorsque vous utilisez hello Assistant, les définitions de JSON pour ces entités de fabrique de données (services liés, des datasets et pipeline de hello) sont créées automatiquement pour vous. Lorsque vous utilisez/API des outils (à l’exception des API .NET), vous définissez ces entités de fabrique de données à l’aide du format JSON de hello.  Pour voir un exemple avec des définitions de JSON pour les entités de fabrique de données qui sont utilisés toocopy des données à partir d’une banque de données MySQL locale, [exemple de JSON : copier des données de MySQL tooAzure Blob](#json-example-copy-data-from-mysql-to-azure-blob) section de cet article. 

Hello les sections suivantes fournit des détails sur les propriétés JSON qui sont le magasin de données MySQL utilisés toodefine Data Factory entités tooa spécifique :

## <a name="linked-service-properties"></a>Propriétés du service lié
Hello tableau suivant fournit la description du service de tooMySQL spécifique lié éléments JSON.

| Propriété | Description | Requis |
| --- | --- | --- |
| type |propriété de type Hello doit indiquer : **OnPremisesMySql** |Oui |
| server |Nom du serveur de MySQL hello. |Oui |
| database |Nom de la base de données MySQL hello. |Oui |
| schema |Nom de schéma hello hello de base de données. |Non |
| authenticationType |Type d’authentification utilisé tooconnect toohello base de données MySQL. Les valeurs possibles sont les suivantes : `Basic`. |Oui |
| username |Spécifiez la base de données utilisateur nom tooconnect toohello MySQL. |Oui |
| password |Spécifiez le mot de passe de compte d’utilisateur hello spécifié. |Oui |
| gatewayName |Nom de passerelle hello hello service Data Factory doit utiliser la base de données MySQL tooconnect toohello local. |Oui |

## <a name="dataset-properties"></a>Propriétés du jeu de données
Pour obtenir une liste complète des sections et les propriétés disponibles pour définir des jeux de données, consultez hello [création de datasets](data-factory-create-datasets.md) l’article. Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données (SQL Azure, Azure Blob, Azure Table, etc.).

Hello **typeProperties** section est différente pour chaque type de jeu de données et fournit des informations sur l’emplacement de hello de données hello dans le magasin de données hello. jeu de données de type Hello typeProperties section **RelationalTable** (qui comprend de jeu de données MySQL) a hello propriétés suivantes

| Propriété | Description | Requis |
| --- | --- | --- |
| TableName |Nom de table hello Bonjour instance de base de données MySQL service lié fait référence à. |Non (si la **requête** de **RelationalSource** est spécifiée) |

## <a name="copy-activity-properties"></a>Propriétés de l’activité de copie
Pour obtenir une liste complète des sections et les propriétés disponibles pour la définition d’activités, consultez hello [création de Pipelines](data-factory-create-pipelines.md) l’article. Les propriétés comme le nom, la description, les tables d'entrée et de sortie et les différentes stratégies sont disponibles pour tous les types d’activités.

Tandis que les propriétés disponibles dans hello **typeProperties** section d’activité hello varient selon chaque type d’activité. Pour l’activité de copie, ils varient selon les types de sources et récepteurs hello.

Lorsque la source de l’activité de copie est de type **RelationalSource** (qui inclut MySQL), hello propriétés suivantes est disponible dans la section de typeProperties :

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| query |Utiliser des données tooread hello requête personnalisée. |Chaîne de requête SQL. Par exemple : select * from MyTable. |Non (si **tableName** de **dataset** est spécifiée) |


## <a name="json-example-copy-data-from-mysql-tooazure-blob"></a>Exemple de JSON : copier des données de MySQL tooAzure Blob
Cet exemple fournit des exemples de définitions de JSON que vous pouvez utiliser toocreate un pipeline à l’aide de [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Elle indique la base de données toocopy à partir d’un MySQL locale tooan stockage d’objets Blob Azure. Toutefois, les données peuvent être copié tooany de récepteurs hello indiqué [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) à l’aide de hello activité de copie dans Azure Data Factory.

> [!IMPORTANT]
> Cet exemple fournit des extraits de code JSON. Il n’inclut pas d’instructions détaillées pour créer la fabrique de données hello. Les instructions se trouvent dans l’article [Déplacement de données entre des emplacements locaux et le cloud](data-factory-move-data-between-onprem-and-cloud.md) .

exemple Hello a hello suivant des entités de fabrique de données :

1. Un service lié de type [OnPremisesMySql](data-factory-onprem-mysql-connector.md#linked-service-properties).
2. Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [RelationalTable](data-factory-onprem-mysql-connector.md#dataset-properties).
4. Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [RelationalSource](data-factory-onprem-mysql-connector.md#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

exemple Hello copie toutes les heures des données à partir d’un résultat de requête dans l’objet blob tooa de base de données MySQL. propriétés JSON Hello utilisées dans ces exemples sont décrits dans les sections suivantes des exemples de hello.

Dans un premier temps, le programme d’installation passerelle de gestion des données hello. instructions de Hello sont Bonjour [déplacement des données entre les emplacements locaux et cloud](data-factory-move-data-between-onprem-and-cloud.md) l’article.

**Service lié MySQL :**

```JSON
    {
      "name": "OnPremMySqlLinkedService",
      "properties": {
        "type": "OnPremisesMySql",
        "typeProperties": {
          "server": "<server name>",
          "database": "<database name>",
          "schema": "<schema name>",
          "authenticationType": "<authentication type>",
          "userName": "<user name>",
          "password": "<password>",
          "gatewayName": "<gateway>"
        }
      }
    }
```

**Service lié Azure Storage :**

```JSON
    {
      "name": "AzureStorageLinkedService",
      "properties": {
        "type": "AzureStorage",
        "typeProperties": {
          "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
      }
    }
```

**Jeu de données d’entrée MySQL :**

exemple Hello suppose que vous avez créé une table « MyTable » dans MySQL et il contienne une colonne appelée « timestampcolumn » pour les données de série chronologique.

Paramètre « external » : « true » informe service Data Factory de hello cette table hello est la fabrique de données externe toohello et n’est pas générée par une activité dans la fabrique de données hello.

```JSON
    {
        "name": "MySqlDataSet",
        "properties": {
            "published": false,
            "type": "RelationalTable",
            "linkedServiceName": "OnPremMySqlLinkedService",
            "typeProperties": {},
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

**Jeu de données de sortie Azure Blob :**

Les données sont écrites tooa nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1). chemin d’accès du dossier Hello pour l’objet blob de hello est évaluée dynamiquement en fonction de l’heure de début hello de tranche hello qui est en cours de traitement. chemin d’accès du dossier Hello utilise l’année, mois, jours et heures des parties de l’heure de début hello.

```JSON
    {
        "name": "AzureBlobMySqlDataSet",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "folderPath": "mycontainer/mysql/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
                "format": {
                    "type": "TextFormat",
                    "rowDelimiter": "\n",
                    "columnDelimiter": "\t"
                },
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
                ]
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
```

**Pipeline avec activité de copie :**

Hello pipeline contient une activité de copie qui est configuré toouse hello des jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures. Dans la définition JSON du pipeline hello, hello **source** type est défini trop**RelationalSource** et **récepteur** type est défini trop**BlobSink**. la requête SQL Hello spécifiée pour hello **requête** propriété sélectionne des données de hello Bonjour au-delà de toocopy d’heure.

```JSON
    {
        "name": "CopyMySqlToBlob",
        "properties": {
            "description": "pipeline for copy activity",
            "activities": [
                {
                    "type": "Copy",
                    "typeProperties": {
                        "source": {
                            "type": "RelationalSource",
                            "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                        },
                        "sink": {
                            "type": "BlobSink",
                            "writeBatchSize": 0,
                            "writeBatchTimeout": "00:00:00"
                        }
                    },
                    "inputs": [
                        {
                            "name": "MySqlDataSet"
                        }
                    ],
                    "outputs": [
                        {
                            "name": "AzureBlobMySqlDataSet"
                        }
                    ],
                    "policy": {
                        "timeout": "01:00:00",
                        "concurrency": 1
                    },
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                    },
                    "name": "MySqlToBlob"
                }
            ],
            "start": "2014-06-01T18:00:00Z",
            "end": "2014-06-01T19:00:00Z"
        }
    }
```


### <a name="type-mapping-for-mysql"></a>Mappage de type pour MySQL
Comme mentionné dans hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, l’activité de copie effectue les conversions de type automatique à partir de types de sources de toosink types avec hello suivant l’approche en deux étapes :

1. Convertir à partir de la source native types too.NET type
2. Conversion de type de récepteur de toonative de type .NET

Lorsque vous déplacez des données tooMySQL, hello mappages suivants sont utilisés à partir des types de too.NET de types de MySQL.

| Type de base de données MySQL | Type de .NET Framework |
| --- | --- |
| bigint non signé |Décimal |
| bigint |Int64 |
| bit |Décimal |
| objet blob |Byte[] |
| valeur booléenne |Boolean |
| char |String |
| date |Datetime |
| Datetime |Datetime |
| Décimal |Décimal |
| double précision |Double |
| Double |Double |
| enum |String |
| float |Single |
| int non signé |Int64 |
| int |Int32 |
| entier non signé |Int64 |
| integer |Int32 |
| long varbinary |Byte[] |
| long varchar |String |
| longblob |Byte[] |
| longtext |String |
| mediumblob |Byte[] |
| mediumint non signé |Int64 |
| mediumint |Int32 |
| mediumtext |String |
| numérique |Décimal |
| real |Double |
| set |String |
| smallint non signé |Int32 |
| smallint |Int16 |
| texte |String |
| time |intervalle de temps |
| timestamp |Datetime |
| tinyblob |Byte[] |
| tinyint non signé |Int16 |
| tinyint |Int16 |
| tinytext |String |
| varchar |String |
| year |Int |

## <a name="map-source-toosink-columns"></a>Mapper les colonnes de source toosink
toolearn sur le mappage des colonnes dans toocolumns du jeu de données source dans le jeu de données récepteur, consultez [mappage des colonnes de jeu de données dans Azure Data Factory](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Lecture renouvelée de sources relationnelles
Lors de la copie des données à partir de banques de données relationnelles, conserver la répétabilité dans l’esprit tooavoid des résultats inattendus. Dans Azure Data Factory, vous pouvez réexécuter une tranche manuellement. Vous pouvez également configurer une stratégie de nouvelles tentatives pour un jeu de données, afin qu’une tranche soit réexécutée en cas de défaillance. Lorsqu’une tranche est exécuté à nouveau dans les deux cas, vous devez toomake vraiment qui hello des mêmes données n’est en lecture aucune question comment plusieurs fois une tranche est exécutée. Voir [Lecture renouvelée de sources relationnelles](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Performances et réglage
Consultez [copie activité optimiser les performances et Guide d’optimisation](data-factory-copy-activity-performance.md) toolearn sur la clé de facteurs d’affecter les performances de transfert de données (activité de copie) dans Azure Data Factory et de différentes façons toooptimize il.
