---
title: "les données d’aaaCopy vers/à partir d’Oracle à l’aide de la fabrique de données | Documents Microsoft"
description: "Découvrez comment toocopy des données vers/à partir d’une base de données Oracle qui est local à l’aide d’Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 3c20aa95-a8a1-4aae-9180-a6a16d64a109
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: adb6d5fbe38e18791616ac77e8179970bbea37fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tofrom-on-premises-oracle-using-azure-data-factory"></a>Copier des données vers/à partir d’Oracle en local à l’aide d’Azure Data Factory
Cet article explique comment toouse hello activité de copie de données de toomove Azure Data Factory vers/à partir d’une base de données Oracle locale. Il repose sur hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, qui présente une vue d’ensemble du déplacement des données avec l’activité de copie hello.

## <a name="supported-scenarios"></a>Scénarios pris en charge
Vous pouvez copier des données **à partir d’une base de données Oracle** toohello suivant des magasins de données :

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

Vous pouvez copier des données à partir de hello suivant des magasins de données **base de données Oracle tooan**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="prerequisites"></a>Composants requis
Fabrique de données prend en charge des sources de Oracle tooon local qui se connecte à l’aide de la passerelle de gestion des données de hello. Consultez [passerelle de gestion des données](data-factory-data-management-gateway.md) toolearn l’article sur la passerelle de gestion des données et [déplacer des données locales toocloud](data-factory-move-data-between-onprem-and-cloud.md) article pour obtenir des instructions sur la configuration de passerelle de hello un pipeline de données toomove des données.

Passerelle est requise même si Oracle hello est hébergé dans une machine virtuelle IaaS de Azure. Vous pouvez installer la passerelle de hello sur hello même IaaS VM sous forme de données de hello stocker ou sur un ordinateur différent virtuel tant que passerelle de hello peuvent se connecter toohello de base de données.

> [!NOTE]
> Consultez [Résolution des problèmes de passerelle](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) pour obtenir des conseils sur la résolution des problèmes de connexion/passerelle.

## <a name="supported-versions-and-installation"></a>Versions prises en charge et installation
Ce connecteur Oracle prend en charge deux versions de pilotes :

- **Pilote Microsoft pour Oracle (recommandé)**: à partir de la passerelle de gestion des données de la version 2.7, un pilote Microsoft pour Oracle est installé automatiquement en même temps que la passerelle de hello, par conséquent, vous n’avez pas besoin handle tooadditionally pilote hello tooestablish connectivité tooOracle et vous pouvez également bénéficier de meilleures performances de copie à l’aide de ce pilote. Voici les versions de bases de données Oracle prises en charge :
    - Oracle 12c R1 (12.1)
    - Oracle 11g R1, R2 (11.1, 11.2)
    - Oracle 10g R1, R2 (10.1, 10.2)
    - Oracle 9i R1, R2 (9.0.1, 9.2)
    - Oracle 8i R3 (8.1.7)

> [!IMPORTANT]
> Pilote Microsoft pour Oracle seulement prend en charge copie de données à partir d’Oracle, mais n’écrit ne pas tooOracle. Et la fonctionnalité de connexion de test de hello Remarque dans l’onglet Diagnostics de passerelle de gestion de données ne prend pas en charge ce pilote. Vous pouvez également utiliser connectivité de hello copie Assistant toovalidate hello.
>

- **Le fournisseur de données Oracle pour .NET :** vous pouvez également choisir les données de toocopy toouse fournisseur de données Oracle à partir de / tooOracle. Ce composant est inclus dans [Oracle Data Access Components for Windows](http://www.oracle.com/technetwork/topics/dotnet/downloads/). Installer la version appropriée de hello (32/64 bits) sur l’ordinateur hello où hello gateway est installé. [Fournisseur de données Oracle .NET 12.1](http://docs.oracle.com/database/121/ODPNT/InstallSystemRequirements.htm#ODPNT149) accessible tooOracle 10 g version 2 ou version ultérieure de la base de données.

    Si vous choisissez « Installation XCopy », suivez les étapes de hello readme.htm. Nous vous recommandons de que choisir de programme d’installation de hello avec une interface utilisateur (non-XCopy une).

    Après avoir installé le fournisseur de hello, **redémarrer** hello service hôte de passerelle de gestion des données sur votre ordinateur à l’aide des Services applet (ou) Gestionnaire de Configuration de passerelle de gestion de données.  

Si vous utilisez le pipeline de copie copie Assistant tooauthor hello, hello pilote sera déterminé automatiquement. Le pilote Microsoft est utilisé par défaut, sauf la version de votre passerelle est antérieure à 2.7 ou si vous choisissez Oracle comme récepteur.

## <a name="getting-started"></a>Prise en main
Vous pouvez créer un pipeline avec une activité de copie qui déplace les données vers/depuis une base de données Oracle locale à l’aide de différents outils/API.

toocreate de façon plus simple Hello un pipeline est toouse hello **Assistant copie de**. Consultez [didacticiel : créer un pipeline à l’aide d’Assistant copie de](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapides sur la création d’un pipeline à l’aide d’Assistant de données de copie hello.

Vous pouvez également utiliser hello suivant outils toocreate un pipeline : **portail Azure**, **Visual Studio**, **Azure PowerShell**, **modèle Azure Resource Manager** , **API .NET**, et **API REST**. Consultez [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions toocreate un pipeline avec une activité de copie.

Si vous utilisez hello ou une API, vous effectuez hello suivant les étapes toocreate un pipeline qui déplace la banque de données récepteur tooa du magasin de données à partir des données d’une source :

1. Création d'une **fabrique de données**. Une fabrique de données peut contenir un ou plusieurs pipelines. 
2. Créer **services liés** fabrique de données tooyour toolink les données d’entrée et de sortie magasins. Par exemple, si vous copiez des données à partir d’un tooan de base de données Oralce stockage d’objets blob Azure, vous créez deux services liés toolink votre base de données Oracle et de la fabrique de données de stockage Azure compte tooyour. Pour les propriétés de service lié sont tooOracle spécifique, consultez [lié des propriétés du service](#linked-service-properties) section.
3. Créer **datasets** toorepresent d’entrée et sortie l’opération de copie des données pour hello. Dans l’exemple hello mentionné dans la dernière étape de hello, vous créer une table de hello toospecify jeu de données dans votre base de données Oracle qui contient les données d’entrée hello. Vous créez un autre conteneur d’objets blob dataset toospecify hello et dossier hello qui contient les données de salutation provenant de base de données Oracle hello. Pour les propriétés du dataset qui sont tooOracle spécifique, consultez [propriétés du dataset](#dataset-properties) section.
4. Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie. Dans l’exemple hello mentionné précédemment, vous utilisez OracleSource en tant que source et BlobSink comme un récepteur pour l’activité de copie hello. De même, si vous copiez à partir du stockage d’objets Blob Azure tooOracle de base de données, vous utilisez BlobSource et OracleSink dans l’activité de copie hello. Pour les propriétés d’activité de copie sont tooOracle spécifique de base de données, consultez [copier les propriétés de l’activité](#copy-activity-properties) section. Pour plus d’informations sur comment toouse du magasin de données source ou un récepteur, cliquez sur le lien hello dans la section précédente de hello pour votre magasin de données. 

Lorsque vous utilisez hello Assistant, les définitions de JSON pour ces entités de fabrique de données (services liés, des datasets et pipeline de hello) sont créées automatiquement pour vous. Lorsque vous utilisez/API des outils (à l’exception des API .NET), vous définissez ces entités de fabrique de données à l’aide du format JSON de hello.  Pour plus d’exemples de définitions de JSON pour les entités de fabrique de données qui sont utilisées toocopy des données vers/à partir d’une base de données Oracle locale, consultez [exemples JSON](#json-examples-for-copying-data-to-and-from-oracle-database) section de cet article.

Hello les sections suivantes fournit des détails sur les propriétés JSON qui sont des entités de fabrique de données toodefine utilisé :

## <a name="linked-service-properties"></a>Propriétés du service lié
Hello tableau suivant fournit la description du service de tooOracle spécifique lié éléments JSON.

| Propriété | Description | Requis |
| --- | --- | --- |
| type |propriété de type Hello doit indiquer : **OnPremisesOracle** |Oui |
| driverType | Spécifier les données de toocopy toouse pilote à partir de / tooOracle de base de données. Valeurs autorisées : **Microsoft** ou **ODP** (par défaut). Consultez la section [Version prise en charge et installation](#supported-versions-and-installation) sur les détails du pilote. | Non |
| connectionString | Spécifiez les informations nécessaires d’instance de base de données Oracle tooconnect toohello pour la propriété connectionString de hello. | Oui |
| gatewayName | Nom de la passerelle hello qui est utilisé tooconnect toohello serveur Oracle locale |Oui |

**Exemple : avec le pilote Microsoft**
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString":"Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

**Exemple : avec le pilote ODP**

Consultez trop[ce site](https://www.connectionstrings.com/oracle-data-provider-for-net-odp-net/) pour hello formats autorisé.

```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "connectionString": "Data Source=(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=<hostname>)(PORT=<port number>))(CONNECT_DATA=(SERVICE_NAME=<SID>)));
User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

## <a name="dataset-properties"></a>Propriétés du jeu de données
Pour obtenir une liste complète des sections et les propriétés disponibles pour définir des jeux de données, consultez hello [création de datasets](data-factory-create-datasets.md) l’article. Les sections telles que la structure, la disponibilité et la stratégie d’un jeu de données JSON sont similaires pour tous les types de jeux de données (Oracle, objet blob Azure, table Azure, etc.).

section de typeProperties Hello est différente pour chaque type de jeu de données et fournit des informations sur l’emplacement de hello de données hello dans le magasin de données hello. section de typeProperties Hello pour hello le jeu de données de type OracleTable a hello propriétés suivantes :

| Propriété | Description | Requis |
| --- | --- | --- |
| TableName |Nom de table hello Bonjour base de données Oracle hello service lié fait référence à. |Non (si **oracleReaderQuery** de **OracleSource** est spécifié) |

## <a name="copy-activity-properties"></a>Propriétés de l’activité de copie
Pour obtenir une liste complète des sections et les propriétés disponibles pour la définition d’activités, consultez hello [création de Pipelines](data-factory-create-pipelines.md) l’article. Les propriétés comme le nom, la description, les tables d’entrée et de sortie et la stratégie sont disponibles pour tous les types d’activités.

> [!NOTE]
> Hello activité de copie accepte uniquement une entrée et produit qu’une seule sortie.

Alors que les propriétés disponibles dans la section typeProperties hello activité hello varient selon chaque type d’activité. Pour l’activité de copie, ils varient selon les types de sources et récepteurs hello.

### <a name="oraclesource"></a>OracleSource
Dans l’activité de copie, lors de la source de hello est de type **OracleSource** hello propriétés suivantes est disponible dans **typeProperties** section :

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| oracleReaderQuery |Utiliser des données tooread hello requête personnalisée. |Chaîne de requête SQL. Par exemple : select * from MyTable <br/><br/>Si non spécifié, hello instruction SQL exécutée : sélectionnez * dans MaTable |Non (si **tableName** de **dataset** est spécifiée) |

### <a name="oraclesink"></a>OracleSink
**OracleSink** prend en charge hello propriétés suivantes :

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| writeBatchTimeout |Temps d’attente pour hello lot insert opération toocomplete avant d’expirer. |intervalle de temps<br/><br/> Exemple : « 00:30:00 » (30 minutes). |Non |
| writeBatchSize |Insère des données dans une table SQL de hello lorsque la taille de mémoire tampon de hello atteint la valeur writeBatchSize. |Nombre entier (nombre de lignes) |Non (valeur par défaut : 100) |
| sqlWriterCleanupScript |Spécifier une requête pour l’activité de copie tooexecute telles que les données d’un secteur spécifique sont nettoyées. |Une instruction de requête. |Non |
| sliceIdentifierColumnName |Spécifiez nom de colonne pour l’activité de copie toofill avec l’identificateur de secteur généré automatiquement, qui est utilisé tooclean des données d’un secteur spécifique quand réexécutée. |Nom d’une colonne avec le type de données binary(32). |Non |

## <a name="json-examples-for-copying-data-tooand-from-oracle-database"></a>Exemples JSON pour la copie des données tooand à partir de la base de données Oracle
Hello exemple suivant fournit des exemples de définitions de JSON que vous pouvez utiliser toocreate un pipeline à l’aide de [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Elles montrent comment toocopy des données à partir de / tooan Oracle database vers/depuis le stockage d’objets Blob Azure. Toutefois, les données peuvent être copié tooany de récepteurs hello indiqué [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) à l’aide de hello activité de copie dans Azure Data Factory.   

## <a name="example-copy-data-from-oracle-tooazure-blob"></a>Exemple : Copier des données à partir d’Oracle tooAzure Blob

exemple Hello a hello suivant des entités de fabrique de données :

1. Un service lié de type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).
2. Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).
4. Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [OracleSource](data-factory-onprem-oracle-connector.md#copy-activity-properties) comme source et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) comme récepteur.

exemple Hello copie toutes les heures des données à partir d’une table dans un blob de tooa de base de données Oracle locale. Pour plus d’informations sur les diverses propriétés utilisées dans l’exemple hello, consultez la documentation dans les sections suivantes des exemples de hello.

**Service lié Oracle :**

```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString":"Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

**Service lié Azure Blob Storage :**

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<Account key>"
        }
    }
}
```

**Jeu de données d’entrée Oracle :**

exemple Hello suppose que vous avez créé une table « MyTable » dans Oracle, et il contienne une colonne appelée « timestampcolumn » pour les données de série chronologique.

Paramètre « external » : « true » informe service Data Factory de hello ce jeu de données hello est la fabrique de données externe toohello et n’est pas généré par une activité dans la fabrique de données hello.

```json
{
    "name": "OracleInput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "offset": "01:00:00",
            "interval": "1",
            "anchorDateTime": "2014-02-27T12:00:00",
            "frequency": "Hour"
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

Les données sont écrites tooa nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1). nom de chemin d’accès et de dossier pour l’objet blob de hello Hello sont dynamiquement évaluées en fonction de l’heure de début hello de tranche hello qui est en cours de traitement. chemin d’accès du dossier Hello utilise l’année, mois, jours et heures des parties de l’heure de début hello.

```json
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

**Pipeline avec activité de copie :**

Hello pipeline contient une activité de copie qui est configuré toouse hello des jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures. Dans la définition JSON du pipeline hello, hello **source** type est défini trop**OracleSource** et **récepteur** type est défini trop**BlobSink**.  spécifié avec la requête SQL Hello **oracleReaderQuery** propriété sélectionne des données de hello Bonjour au-delà de toocopy d’heure.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
            {
                "name": "OracletoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                    {
                        "name": " OracleInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "typeProperties": {
                    "source": {
                        "type": "OracleSource",
                        "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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

## <a name="example-copy-data-from-azure-blob-toooracle"></a>Exemple : Copier des données d’objets Blob Azure tooOracle
Cet exemple montre comment toocopy les données à partir d’un tooan de stockage d’objets Blob Azure en local de la base de données Oracle. Toutefois, les données peuvent être copiées **directement** à partir des sources de hello indiqués [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) à l’aide de hello activité de copie dans Azure Data Factory.  

exemple Hello a hello suivant des entités de fabrique de données :

1. Un service lié de type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).
2. Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. un [jeu de données](data-factory-create-datasets.md) d'entrée de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).
5. Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) comme source et [OracleSink](data-factory-onprem-oracle-connector.md#copy-activity-properties) comme récepteur.

exemple Hello copie des données à partir d’une table de tooa d’objets blob dans une base de données Oracle locale toutes les heures. Pour plus d’informations sur les diverses propriétés utilisées dans l’exemple hello, consultez la documentation dans les sections suivantes des exemples de hello.

**Service lié Oracle :**
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "connectionString": "Data Source=(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=<hostname>)(PORT=<port number>))(CONNECT_DATA=(SERVICE_NAME=<SID>)));
            User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

**Service lié Azure Blob Storage :**
```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<Account key>"
        }
    }
}
```

**Jeu de données d'entrée d'objet Blob Azure**

Les données sont récupérées à partir d'un nouvel objet Blob toutes les heures (fréquence : heure, intervalle : 1). nom de chemin d’accès et de dossier pour l’objet blob de hello Hello sont dynamiquement évaluées en fonction de l’heure de début hello de tranche hello qui est en cours de traitement. chemin d’accès du dossier Hello utilise la partie jour de l’heure de début hello, mois et année et nom de fichier partie d’heure hello de l’heure de début hello. « external » : « true » paramètre informe le service Data Factory de hello que cette table est la fabrique de données externe toohello et qu’il n’est pas générée par une activité dans la fabrique de données hello.

```json
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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
            "frequency": "Day",
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

**Jeu de données de sortie Oracle :**

exemple Hello suppose que vous avez créé une table « MaTable » dans Oracle. Créer la table de hello dans Oracle avec hello même nombre de colonnes comme vous le souhaitez toocontain de fichier CSV d’objets Blob hello. Nouvelles lignes sont ajoutées à la table de toohello toutes les heures.

```json
{
    "name": "OracleOutput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Day",
            "interval": "1"
        }
    }
}
```

**Pipeline avec activité de copie :**

Hello pipeline contient une activité de copie qui est configuré toouse hello des jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures. Dans la définition JSON du pipeline hello, hello **source** type est défini trop**BlobSource** et hello **récepteur** type est défini trop**OracleSink**.  

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-05T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
            {
                "name": "AzureBlobtoOracle",
                "description": "Copy Activity",
                "type": "Copy",
                "inputs": [
                    {
                        "name": "AzureBlobInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "OracleOutput"
                    }
                ],
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "OracleSink"
                    }
                },
                "scheduler": {
                    "frequency": "Day",
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


## <a name="troubleshooting-tips"></a>Conseils de dépannage
### <a name="problem-1-net-framework-data-provider"></a>Problème 1 : Fournisseur de données .NET Framework

Hello suivante **message d’erreur**:

    Copy activity met invalid parameters: 'UnknownParameterName', Detailed message: Unable toofind hello requested .Net Framework Data Provider. It may not be installed”.  

**Causes possibles :**

1. Hello, fournisseur de données .NET Framework pour Oracle n’a pas été installé.
2. Hello, fournisseur de données .NET Framework pour Oracle a été installé too.NET Framework 2.0 et est introuvable dans les dossiers hello .NET Framework 4.0.

**Résolution/solution de contournement :**

1. Si vous n’avez pas installé hello fournisseur .NET pour Oracle, [installer](http://www.oracle.com/technetwork/topics/dotnet/downloads/) et recommencez le scénario de hello.
2. Si vous obtenez un message d’erreur hello même après l’installation du fournisseur de hello, procédez comme hello comme suit :
   1. Ouvrir la configuration de la machine de .NET 2.0 à partir du dossier hello : <system disk>: \Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG\machine.config.
   2. Recherchez **le fournisseur de données Oracle pour .NET**, et vous devez être en mesure de toofind une entrée comme indiqué dans hello suivant l’exemple sous **system.data** -> **DbProviderFactories**: «<add name="Oracle Data Provider for .NET" invariant="Oracle.DataAccess.Client" description="Du fournisseur de données oracle pour .NET" type="Oracle.DataAccess.Client.OracleClientFactory, Oracle.DataAccess, Version=2.112.3.0, Culture=neutral, PublicKeyToken=89b483f429c47342" />.
3. Copiez ce fichier machine.config de toohello entrée Bonjour suivant v4.0 dossier : <system disk>: \Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config et modification hello version too4.xxx.x.x.
4. Installez « < chemin d’accès ODP.NET installé > \11.2.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll » dans hello global assembly cache (GAC) en exécutant `gacutil /i [provider path]`. ## des conseils de dépannage

### <a name="problem-2-datetime-formatting"></a>Problème 2 : Mise en forme de la date et de l’heure

Hello suivante **message d’erreur**:

    Message=Operation failed in Oracle Database with hello following error: 'ORA-01861: literal does not match format string'.,Source=,''Type=Oracle.DataAccess.Client.OracleException,Message=ORA-01861: literal does not match format string,Source=Oracle Data Provider for .NET,'.

**Résolution/solution de contournement :**

Vous devrez peut-être la chaîne de requête tooadjust hello dans votre activité de copie basée sur la façon dont les dates sont configurés dans votre base de données Oracle, comme indiqué dans les éléments suivants de hello exemple (à l’aide de la fonction to_date hello) :

    "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= to_date(\\'{0:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\')  AND timestampcolumn < to_date(\\'{1:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\') ', WindowStart, WindowEnd)"


## <a name="type-mapping-for-oracle"></a>Mappage de type pour Oracle
Comme mentionné dans hello [les activités de déplacement des données](data-factory-data-movement-activities.md) activité de copie de l’article effectue des conversions de type automatique à partir de types de sources de toosink types avec hello approche de l’étape 2 :

1. Convertir à partir de la source native types too.NET type
2. Conversion de type de récepteur de toonative de type .NET

Lors du déplacement des données à partir d’Oracle, hello suivant les mappages est utilisé à partir du type too.NET de type de données Oracle et vice versa.

| Type de données Oracle | Type de données .NET Framework. |
| --- | --- |
| BFILE |Byte[] |
| BLOB |Byte[] |
| CHAR |String |
| CLOB |String |
| DATE |DateTime |
| FLOAT |Décimale, chaîne (si précision > 28) |
| INTEGER |Décimale, chaîne (si précision > 28) |
| INTERVALLE année tooMONTH |Int32 |
| INTERVALLE jour tooSECOND |TimeSpan |
| LONG |String |
| LONG RAW |Byte[] |
| NCHAR |String |
| NCLOB |String |
| NUMBER |Décimale, chaîne (si précision > 28) |
| NVARCHAR2 |String |
| RAW |Byte[] |
| ROWID |String |
| TIMESTAMP |DateTime |
| TIMESTAMP WITH LOCAL TIME ZONE |DateTime |
| TIMESTAMP WITH TIME ZONE |DateTime |
| UNSIGNED INTEGER |NUMBER |
| VARCHAR2 |String |
| XML |String |

> [!NOTE]
> Type de données **intervalle année tooMONTH** et **INTERVAL DAY tooSECOND** ne sont pas pris en charge lors de l’utilisation du pilote Microsoft.

## <a name="map-source-toosink-columns"></a>Mapper les colonnes de source toosink
toolearn sur le mappage des colonnes dans toocolumns du jeu de données source dans le jeu de données récepteur, consultez [mappage des colonnes de jeu de données dans Azure Data Factory](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Lecture renouvelée de sources relationnelles
Lors de la copie des données à partir de banques de données relationnelles, conserver la répétabilité dans l’esprit tooavoid des résultats inattendus. Dans Azure Data Factory, vous pouvez réexécuter une tranche manuellement. Vous pouvez également configurer une stratégie de nouvelles tentatives pour un jeu de données, afin qu’une tranche soit réexécutée en cas de défaillance. Lorsqu’une tranche est exécuté à nouveau dans les deux cas, vous devez toomake vraiment qui hello des mêmes données n’est en lecture aucune question comment plusieurs fois une tranche est exécutée. Voir [Lecture renouvelée de sources relationnelles](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Performances et réglage
Consultez [copie activité optimiser les performances et Guide d’optimisation](data-factory-copy-activity-performance.md) toolearn sur la clé de facteurs d’affecter les performances de transfert de données (activité de copie) dans Azure Data Factory et de différentes façons toooptimize il.
