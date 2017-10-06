---
title: "les données d’aaaMove vers/à partir de la Table Azure | Documents Microsoft"
description: "Découvrez comment les données de toomove vers/depuis le stockage de Table Azure à l’aide d’Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 07b046b1-7884-4e57-a613-337292416319
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jingwang
ms.openlocfilehash: 3dc3da6d88854674a9108b600534bc5d07575f15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-table-using-azure-data-factory"></a>Déplacer les données tooand à partir de la Table Azure à l’aide d’Azure Data Factory
Cet article explique comment toouse hello activité de copie de données de toomove Azure Data Factory vers ou depuis le stockage de Table Azure. Il repose sur hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, qui présente une vue d’ensemble du déplacement des données avec l’activité de copie hello. 

Vous pouvez copier les données de toute source pris en charge stocker tooAzure le stockage de Table de données ou à partir de données de récepteur tooany pris en charge le stockage Table store. Pour obtenir la liste des magasins de données pris en charge en tant que sources ou récepteurs par l’activité de copie hello, consultez hello [prise en charge des magasins de données](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table. 

## <a name="getting-started"></a>Prise en main
Vous pouvez créer un pipeline avec une activité de copie qui déplace les données vers/depuis un Stockage Table Azure à l’aide de différents outils/API.

toocreate de façon plus simple Hello un pipeline est toouse hello **Assistant copie de**. Consultez [didacticiel : créer un pipeline à l’aide d’Assistant copie de](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapides sur la création d’un pipeline à l’aide d’Assistant de données de copie hello.

Vous pouvez également utiliser hello suivant outils toocreate un pipeline : **portail Azure**, **Visual Studio**, **Azure PowerShell**, **modèle Azure Resource Manager** , **API .NET**, et **API REST**. Consultez [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions toocreate un pipeline avec une activité de copie. 

Si vous utilisez hello ou une API, vous effectuez hello suivant les étapes toocreate un pipeline qui déplace la banque de données récepteur tooa du magasin de données à partir des données d’une source : 

1. Créer **services liés** fabrique de données tooyour toolink les données d’entrée et de sortie magasins.
2. Créer **datasets** toorepresent d’entrée et sortie l’opération de copie des données pour hello. 
3. Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie. 

Lorsque vous utilisez hello Assistant, les définitions de JSON pour ces entités de fabrique de données (services liés, des datasets et pipeline de hello) sont créées automatiquement pour vous. Lorsque vous utilisez/API des outils (à l’exception des API .NET), vous définissez ces entités de fabrique de données à l’aide du format JSON de hello.  Pour plus d’exemples de définitions de JSON pour les entités de fabrique de données qui sont utilisés toocopy des données vers/depuis un stockage de tables Azure, consultez [exemples JSON](#json-examples) section de cet article. 

Hello les sections suivantes fournit des détails sur les propriétés JSON qui sont utilisés toodefine Data Factory entités spécifique tooAzure le stockage de Table : 

## <a name="linked-service-properties"></a>Propriétés du service lié
Il existe deux types de services liés, vous pouvez utiliser toolink une fabrique de données Azure tooan stockage blob Azure. Il s’agit des services liés **AzureStorage** et **AzureStorageSas**. Hello service lié Azure Storage fournit la fabrique de données hello avec accès global toohello le stockage Azure. Alors que hello Azure stockage SAS (Shared Access Signature) lié service fournit fabrique de données hello avec l’accès restreint/temps toohello le stockage Azure. Il n'existe aucune différence entre ces deux services liés. Sélectionnez service hello lié qui correspond le mieux à vos besoins. Hello sections suivantes fournissent plus d’informations sur ces deux services liés.

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a>Propriétés du jeu de données
Pour obtenir une liste complète des sections et les propriétés disponibles pour définir des jeux de données, consultez hello [création de datasets](data-factory-create-datasets.md) l’article. Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données (SQL Azure, Azure Blob, Azure Table, etc.).

section de typeProperties Hello est différente pour chaque type de jeu de données et fournit des informations sur l’emplacement de hello de données hello dans le magasin de données hello. Hello **typeProperties** section hello le jeu de données de type **AzureTable** a les propriétés suivantes de hello.

| Propriété | Description | Requis |
| --- | --- | --- |
| TableName |Nom de table hello dans l’instance de base de données de Table Azure hello ce service lié fait référence à. |Oui. Lorsqu’un nom de table est spécifié sans un azureTableSourceQuery, tous les enregistrements à partir de la table de hello sont copiés toohello destination. Si un azureTableSourceQuery est également spécifiée, les enregistrements de la table hello qui répond aux requêtes de hello sont copiés toohello destination. |

### <a name="schema-by-data-factory"></a>Schéma par Data Factory
Pour les magasins de données sans schéma comme Table de Azure, hello service Data Factory déduit le schéma de hello dans un des hello suivant façons :

1. Si vous spécifiez la structure hello des données à l’aide de hello **structure** propriété dans la définition de dataset hello, hello service Data Factory respecte cette structure en tant que schéma de hello. Dans ce cas, si une ligne ne contient pas de valeur pour une colonne, une valeur null est fournie pour celle-ci.
2. Si vous ne spécifiez pas structure hello des données à l’aide de hello **structure** propriété dans la définition de dataset hello, Data Factory déduit le schéma de hello à l’aide de la première ligne de hello dans les données de salutation. Dans ce cas, si la première ligne de hello ne contient pas de schéma complet de hello, certaines colonnes sont ignorés dans le résultat de hello d’opération de copie.

Par conséquent, pour les sources de données de schéma, il est recommandé de hello est toospecify hello structure de données à l’aide de hello **structure** propriété.

## <a name="copy-activity-properties"></a>Propriétés de l’activité de copie
Pour obtenir une liste complète des sections et les propriétés disponibles pour la définition d’activités, consultez hello [création de Pipelines](data-factory-create-pipelines.md) l’article. Les propriétés comme le nom, la description, les jeux de données d’entrée et de sortie et les stratégies sont disponibles pour tous les types d’activités.

Propriétés disponibles dans la section de typeProperties hello d’activité hello sur hello autre part varient selon chaque type d’activité. Pour l’activité de copie, ils varient selon les types de sources et récepteurs hello.

**AzureTableSource** prend en charge hello propriétés dans la section de typeProperties suivantes :

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| AzureTableSourceQuery |Utiliser des données tooread hello requête personnalisée. |Chaîne de requête de table Azure. Consultez les exemples dans la section suivante de hello. |Non. Lorsqu’un nom de table est spécifié sans un azureTableSourceQuery, tous les enregistrements à partir de la table de hello sont copiés toohello destination. Si un azureTableSourceQuery est également spécifiée, les enregistrements de la table hello qui répond aux requêtes de hello sont copiés toohello destination. |
| azureTableSourceIgnoreTableNotFound |Indiquer si exception de hello avale de table n’existe pas. |TRUE<br/>FALSE |Non |

### <a name="azuretablesourcequery-examples"></a>Exemples azureTableSourceQuery
Si la colonne de table Azure est de type chaîne :

```JSON
azureTableSourceQuery": "$$Text.Format('PartitionKey ge \\'{0:yyyyMMddHH00_0000}\\' and PartitionKey le \\'{0:yyyyMMddHH00_9999}\\'', SliceStart)"
```

Si la colonne de table Azure est de type datetime:

```JSON
"azureTableSourceQuery": "$$Text.Format('DeploymentEndTime gt datetime\\'{0:yyyy-MM-ddTHH:mm:ssZ}\\' and DeploymentEndTime le datetime\\'{1:yyyy-MM-ddTHH:mm:ssZ}\\'', SliceStart, SliceEnd)"
```

**AzureTableSink** prend en charge hello propriétés dans la section de typeProperties suivantes :

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| azureTableDefaultPartitionKeyValue |Valeur par défaut partition clé qui peut être utilisé par le récepteur de hello. |Valeur de chaîne. |Non |
| azureTablePartitionKeyName |Spécifiez le nom de colonne hello dont les valeurs sont utilisées comme clés de partition. Si non spécifié, AzureTableDefaultPartitionKeyValue est utilisé comme clé de partition hello. |Nom de colonne. |Non |
| azureTableRowKeyName |Spécifiez le nom de colonne hello dont les valeurs de colonne sont utilisées comme clé de ligne. Si aucune valeur n'est spécifiée, un GUID est utilisé pour chaque ligne. |Nom de colonne. |Non |
| azureTableInsertType |Hello mode tooinsert les données dans Azure table.<br/><br/>Cette propriété contrôle si les lignes existantes dans la table de sortie hello avec les clés de partition et de ligne correspondantes ont leurs valeurs remplacé ou fusionnées. <br/><br/>toolearn sur le fonctionnement de ces paramètres (fusion et remplacement), consultez [insertion ou l’entité de fusion](https://msdn.microsoft.com/library/azure/hh452241.aspx) et [insérer ou remplacer une entité](https://msdn.microsoft.com/library/azure/hh452242.aspx) rubriques. <br/><br> Ce paramètre s’applique au niveau de ligne hello, pas de niveau de table d’hello, et aucune de ces options supprime des lignes dans la table de sortie hello qui n’existent pas dans l’entrée de hello. |fusionner (par défaut)<br/>remplacer |Non |
| writeBatchSize |Insère des données dans hello table Azure quand la valeur de hello writeBatchSize ou writeBatchTimeout est atteinte. |Nombre entier (nombre de lignes) |Non (valeur par défaut : 10000) |
| writeBatchTimeout |Insère des données dans hello table Azure quand la valeur de hello writeBatchSize ou writeBatchTimeout est atteinte |intervalle de temps<br/><br/>Exemple : « 00: 20:00 » (20 minutes) |Non (le délai d’expiration de valeur par défaut toostorage client par défaut la valeur 90 s) |

### <a name="azuretablepartitionkeyname"></a>azureTablePartitionKeyName
Mapper une colonne de destination de tooa de colonne source à l’aide de la propriété JSON de traduction hello avant que vous pouvez utiliser la colonne de destination hello comme hello azureTablePartitionKeyName.

Bonjour l’exemple suivant, la colonne de source DivisionID est colonne de destination mappé toohello : DivisionID.  

```JSON
"translator": {
    "type": "TabularTranslator",
    "columnMappings": "DivisionID: DivisionID, FirstName: FirstName, LastName: LastName"
}
```
Hello DivisionID est spécifié en tant que clé de partition hello.

```JSON
"sink": {
    "type": "AzureTableSink",
    "azureTablePartitionKeyName": "DivisionID",
    "writeBatchSize": 100,
    "writeBatchTimeout": "01:00:00"
}
```
## <a name="json-examples"></a>Exemples JSON
Hello exemples suivants proposent des exemples de définitions de JSON que vous pouvez utiliser toocreate un pipeline à l’aide de [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Elles montrent comment tooand de données toocopy de stockage de Table Azure et base de données des objets Blob Azure. Toutefois, les données peuvent être copiées **directement** de n’importe quelle tooany de sources hello de récepteurs de hello pris en charge. Pour plus d’informations, consultez la section hello « magasins de données pris en charge et formats » dans [déplacer des données à l’aide de l’activité de copie](data-factory-data-movement-activities.md).

## <a name="example-copy-data-from-azure-table-tooazure-blob"></a>Exemple : Copier des données à partir de la Table Azure tooAzure Blob
Hello ci-dessous illustre d’exemple :

1. Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (utilisé pour la table et l’objet blob).
2. Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [AzureTable](#dataset-properties).
3. Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. Hello [pipeline](data-factory-create-pipelines.md) avec l’activité de copie qui utilise [AzureTableSource](#activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

exemple Hello copie les données appartenant à partition par défaut de toohello dans un objet blob tooa de Table Azure toutes les heures. propriétés JSON Hello utilisées dans ces exemples sont décrits dans les sections suivantes des exemples de hello.

**Service lié Azure Storage :**

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
Azure Data Factory prend en charge deux types de service lié Azure Storage : **AzureStorage** et **AzureStorageSas**. Pour hello premier, vous spécifiez la chaîne de connexion hello qui inclut la clé de compte hello et pourquoi une version ultérieure, vous spécifiez hello Uri de Signature d’accès partagé (SAS). Pour plus d’informations, consultez la section [Services liés](#linked-service-properties) .  

**Jeu de données d'entrée Table Azure :**

exemple Hello suppose que vous avez créé une table « MaTable » dans la Table Azure.

Paramètre « external » : « true » informe service Data Factory de hello ce jeu de données hello est la fabrique de données externe toohello et n’est pas généré par une activité dans la fabrique de données hello.

```JSON
{
  "name": "AzureTableInput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
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

**Activité de copie dans un pipeline avec AzureTableSource et BlobSink :**

Hello pipeline contient une activité de copie qui est configuré toouse hello des jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures. Dans la définition JSON du pipeline hello, hello **source** type est défini trop**AzureTableSource** et **récepteur** type est défini trop**BlobSink**. spécifié avec la requête SQL Hello **AzureTableSourceQuery** propriété sélectionne des données de hello de partition par défaut de hello toocopy de chaque heure.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
            {
                "name": "AzureTabletoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                      {
                        "name": "AzureTableInput"
                    }
                ],
                "outputs": [
                      {
                            "name": "AzureBlobOutput"
                      }
                ],
                "typeProperties": {
                      "source": {
                        "type": "AzureTableSource",
                        "AzureTableSourceQuery": "PartitionKey eq 'DefaultPartitionKey'"
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

## <a name="example-copy-data-from-azure-blob-tooazure-table"></a>Exemple : Copier des données d’objets Blob Azure tooAzure Table
Hello ci-dessous illustre d’exemple :

1. Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (utilisé pour la table et l’objet blob)
2. un [jeu de données](data-factory-create-datasets.md) d'entrée de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
3. Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureTable](#dataset-properties).
4. Hello [pipeline](data-factory-create-pipelines.md) avec l’activité de copie qui utilise [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) et [AzureTableSink](#copy-activity-properties).

exemple Hello copie les données de séries chronologiques à partir d’un tooan d’objets blob Azure table Azure toutes les heures. propriétés JSON Hello utilisées dans ces exemples sont décrits dans les sections suivantes des exemples de hello.

**Service lié Azure Storage (pour Table Azure et objet Blob Azure) :**

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

Azure Data Factory prend en charge deux types de service lié Azure Storage : **AzureStorage** et **AzureStorageSas**. Pour hello premier, vous spécifiez la chaîne de connexion hello qui inclut la clé de compte hello et pourquoi une version ultérieure, vous spécifiez hello Uri de Signature d’accès partagé (SAS). Pour plus d’informations, consultez la section [Services liés](#linked-service-properties) .

**Jeu de données d'entrée d'objet Blob Azure :**

Les données sont récupérées à partir d'un nouvel objet Blob toutes les heures (fréquence : heure, intervalle : 1). nom de chemin d’accès et de dossier pour l’objet blob de hello Hello sont dynamiquement évaluées en fonction de l’heure de début hello de tranche hello qui est en cours de traitement. chemin d’accès du dossier Hello utilise la partie jour de l’heure de début hello, mois et année et nom de fichier partie d’heure hello de l’heure de début hello. « external » : « true » paramètre informe le service de fabrique de données de hello ce jeu de données hello est la fabrique de données externe toohello et n’est pas généré par une activité dans la fabrique de données hello.

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

**Jeu de données de sortie Table Azure :**

exemple Hello copie table tooa de données nommé « MyTable » dans la Table Azure. Créer une table Azure avec hello même nombre de colonnes comme vous le souhaitez toocontain de fichier CSV d’objets Blob hello. Nouvelles lignes sont ajoutées à la table de toohello toutes les heures.

```JSON
{
  "name": "AzureTableOutput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
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

**Activité de copie dans un pipeline avec BlobSource et AzureTableSink :**

Hello pipeline contient une activité de copie qui est configuré toouse hello des jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures. Dans la définition JSON du pipeline hello, hello **source** type est défini trop**BlobSource** et **récepteur** type est défini trop**AzureTableSink**.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoTable",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureTableOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "AzureTableSink",
            "writeBatchSize": 100,
            "writeBatchTimeout": "01:00:00"
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
## <a name="type-mapping-for-azure-table"></a>Mappage de type de Table Azure
Comme mentionné dans hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, l’activité de copie effectue les conversions de type automatique à partir de types de sources de toosink types avec hello suivant l’approche en deux étapes.

1. Convertir à partir de la source native types too.NET type
2. Conversion de type de récepteur de toonative de type .NET

Lorsque vous déplacez des données trop & à partir de la Table Azure, hello suivant [des mappages définis par le service de Table Azure](https://msdn.microsoft.com/library/azure/dd179338.aspx) servent de type de too.NET types OData de Table Azure et vice versa.

| Type de données OData | Type .NET | Détails |
| --- | --- | --- |
| Edm.Binary |byte[] |Un tableau d’octets des too64 Ko. |
| Edm.Boolean |valeur booléenne |Valeur booléenne. |
| Edm.DateTime |DateTime |Valeur de 64 bits exprimée en temps universel coordonné (UTC). prise en charge de Hello DateTime commence à partir de 12:00 minuit, le 1er janvier 1601. (NOTRE ÈRE), UTC. Hello se termine le 31 décembre 9999. |
| Edm.Double |double |Valeur à virgule flottante de 64 bits. |
| Edm.Guid |Guid |Identificateur global unique de 128 bits. |
| Edm.Int32 |Int32 |Nombre entier 32 bits. |
| Edm.Int64 |Int64 |Nombre entier 64 bits. |
| Edm.String |String |Valeur encodée en UTF-16. Les valeurs de chaîne peuvent être des too64 Ko. |

### <a name="type-conversion-sample"></a>Exemple de conversion de type
Hello suivant l’exemple est pour copier des données à partir d’une Table de tooAzure objets Blob Azure avec des conversions de type.

Supposons que jeu de données Blob hello est au format CSV et comporte trois colonnes. Un d’eux est une colonne datetime avec un format datetime personnalisées à l’aide d’un nom abrégé Français pour le jour de la semaine de hello.

Définir le dataset de Source de l’objet Blob de hello comme suit, ainsi que des définitions de type pour les colonnes hello.

```JSON
{
    "name": " AzureBlobInput",
    "properties":
    {
         "structure":
          [
                { "name": "userid", "type": "Int64"},
                { "name": "name", "type": "String"},
                { "name": "lastlogindate", "type": "Datetime", "culture": "fr-fr", "format": "ddd-MM-YYYY"}
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
        "external": true,
        "availability":
        {
            "frequency": "Hour",
            "interval": 1,
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
Compte tenu de mappage de type hello du type de too.NET type OData de Table Azure, vous devrez définir table de hello dans la Table Azure avec hello suivant le schéma.

**Schéma de Table Azure :**

| Nom de la colonne | Type |
| --- | --- |
| userid |Edm.Int64 |
| name |Edm.String |
| lastlogindate |Edm.DateTime |

Ensuite, définissez le jeu de données de Table Azure hello comme suit. Vous n’avez pas besoin de section « structure » de toospecify avec les informations de type hello, car les informations de type hello sont déjà spécifiées dans hello sous-jacent du magasin de données.

```JSON
{
  "name": "AzureTableOutput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
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

Dans ce cas, la fabrique de données automatiquement conversions de type, y compris le champ de date/heure hello avec le format de date/heure personnalisé hello à l’aide de la culture de hello « fr-fr » lors du déplacement des données à partir de l’objet Blob tooAzure Table.

> [!NOTE]
> colonnes de toomap de toocolumns du jeu de données source à partir du jeu de données récepteur, consultez [mappage des colonnes de jeu de données dans Azure Data Factory](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Performances et réglage
impact sur les performances de transfert de données (activité de copie) dans Azure Data Factory et de différentes façons toooptimize des facteurs toolearn sur la clé, consultez [copie activité optimiser les performances et Guide d’optimisation](data-factory-copy-activity-performance.md).
