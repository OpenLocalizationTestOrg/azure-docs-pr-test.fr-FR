---
title: "données aaaMove Amazon Simple Service de stockage à l’aide de Data Factory | Documents Microsoft"
description: "En savoir plus sur la façon de toomove les données à partir du Service de stockage Simple Amazon (S3) à l’aide d’Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 636d3179-eba8-4841-bcb4-3563f6822a26
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 8a8cd2845fd1de74413bd0372f3aabfb4817549b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-amazon-simple-storage-service-by-using-azure-data-factory"></a>Déplacement de données à partir d’Amazon Simple Storage Service à l’aide d’Azure Data Factory
Cet article explique comment toouse hello activité de copie de données de toomove Azure Data Factory à partir du Service de stockage Simple Amazon (S3). Il repose sur hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, qui présente une vue d’ensemble du déplacement des données avec l’activité de copie hello.

Vous pouvez copier des données à partir de la banque de données récepteur Amazon S3 tooany pris en charge. Pour une liste de données pris en charge des magasins récepteurs par l’activité de copie hello, consultez hello [prise en charge des magasins de données](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table. Fabrique de données prend actuellement en charge le déplacement des données uniquement à partir des magasins de données Amazon S3 tooother, mais ne pas déplacer les données à partir d’autres données stocke tooAmazon S3.

## <a name="required-permissions"></a>Autorisations requises
données toocopy de Amazon S3, assurez-vous que vous avez été accordées hello les autorisations suivantes :

* `s3:GetObject` et `s3:GetObjectVersion` pour les opérations d’objet Amazon S3 ;
* `s3:ListBucket` pour les opérations de compartiment Amazon S3. Si vous utilisez hello Assistant Copier les données de fabrique, `s3:ListAllMyBuckets` est également requis.

Pour plus d’informations sur la liste complète des autorisations d’Amazon S3 hello, consultez [spécifier les autorisations dans une stratégie](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html).

## <a name="getting-started"></a>Prise en main
Vous pouvez créer un pipeline avec une activité de copie qui déplace les données d’une source Amazon S3 à l’aide de différents outils ou API.

toocreate de façon plus simple Hello un pipeline est toouse hello **Assistant copie de**. Pour obtenir une description rapide, consultez [Didacticiel : créer un pipeline à l’aide de l’Assistant Copie](data-factory-copy-data-wizard-tutorial.md).

Vous pouvez également utiliser hello suivant outils toocreate un pipeline : **portail Azure**, **Visual Studio**, **Azure PowerShell**, **modèle Azure Resource Manager** , **API .NET**, et **API REST**. Pour obtenir des instructions toocreate un pipeline avec une activité de copie, consultez hello [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

Si vous utilisez des outils ou des API, vous allez exécuter hello suivant les étapes toocreate un pipeline qui déplace la banque de données récepteur tooa du magasin de données à partir des données sources :

1. Créer **services liés** fabrique de données tooyour toolink les données d’entrée et de sortie magasins.
2. Créer **datasets** toorepresent d’entrée et sortie l’opération de copie des données pour hello.
3. Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.

Lorsque vous utilisez hello Assistant, les définitions de JSON pour ces entités de fabrique de données (services liés, des datasets et pipeline de hello) sont créées automatiquement pour vous. Lorsque vous utilisez des outils ou des API (à l’exception des API .NET), vous définissez ces entités de fabrique de données à l’aide du format JSON de hello. Pour voir un exemple avec des définitions de JSON pour les entités de fabrique de données qui sont utilisées toocopy des données à partir d’une banque de données Amazon S3, hello [exemple de JSON : copier des données d’Amazon S3 tooAzure Blob](#json-example-copy-data-from-amazon-s3-to-azure-blob) section de cet article.

> [!NOTE]
> Pour plus d’informations sur les formats de fichier et de compression pris en charge pour une activité de copie, consultez [Formats de fichier et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md).

Hello les sections suivantes fournit des détails sur les propriétés JSON qui sont utilisés toodefine Data Factory entités spécifique tooAmazon S3.

## <a name="linked-service-properties"></a>Propriétés du service lié
Un service lié lie une fabrique de données de tooa de magasin de données. Vous créez un service lié de type **AwsAccessKey** toolink vos données Amazon S3 stocker la fabrique de données tooyour. Hello tableau suivant fournit un service de description pour JSON éléments tooAmazon spécifique S3 (AwsAccessKey) liée.

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| accessKeyID |ID de clé d’accès de clé secrète hello. |string |Oui |
| secretAccessKey |clé d’accès de clé secrète Hello elle-même. |Chaîne secrète chiffrée |Oui |

Voici un exemple :

```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

## <a name="dataset-properties"></a>Propriétés du jeu de données
toospecify un toorepresent de jeu de données d’entrée les données dans le stockage d’objets Blob Azure, propriété de type hello ensemble du jeu de données hello**AmazonS3**. Ensemble hello **linkedServiceName** service lié de propriété du nom de toohello hello dataset Hello Amazon S3. Pour obtenir la liste complète des sections et propriétés disponibles pour la définition de jeux de données, voir [Création de jeux de données](data-factory-create-datasets.md). 

Les sections comme la structure, la disponibilité et la stratégie sont similaires pour tous les types de jeux de données (par exemple, SQL Database, Azure Blob et Azure Table). Hello **typeProperties** section est différente pour chaque type de jeu de données et fournit des informations sur l’emplacement de hello de données hello dans le magasin de données hello. Hello **typeProperties** section pour un jeu de données de type **AmazonS3** (qui inclut les dataset hello Amazon S3) a hello propriétés suivantes :

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| bucketName |nom du compartiment Hello S3. |String |Oui |
| key |clé d’objet Hello S3. |String |Non |
| prefix |Préfixe de la clé d’objet hello S3. Les objets dont les clés commencent par ce préfixe sont sélectionnés. S’applique uniquement lorsque la clé est vide. |string |Non |
| version |version Hello d’objet hello S3, si le contrôle de version S3 est activé. |String |Non |
| format | Hello, les types de format suivants est pris en charge : **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Ensemble hello **type** propriété sous tooone de format de ces valeurs. Pour plus d’informations, consultez hello [au format texte](data-factory-supported-file-and-compression-formats.md#text-format), [format JSON](data-factory-supported-file-and-compression-formats.md#json-format), [le format Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc format](data-factory-supported-file-and-compression-formats.md#orc-format), et [format de Parquet ](data-factory-supported-file-and-compression-formats.md#parquet-format) sections. <br><br> Si vous souhaitez que les fichiers toocopy en tant que-entre le fichier magasins (copie binaire), ignorer hello format section dans les deux définitions de jeu de données d’entrée et de sortie. |Non | |
| compression | Spécifiez le type de hello et le niveau de compression pour les données de salutation. les types Hello pris en charge sont : **GZip**, **Deflate**, **BZip2**, et **ZipDeflate**. les niveaux de Hello pris en charge sont : **Optimal** et **plus rapide**. Pour plus d’informations, consultez [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |Non | |


> [!NOTE]
> **bucketName + touche** Spécifie l’emplacement de hello d’objet hello S3, où compartiment est le conteneur racine hello S3 objets et la clé est hello chemin d’accès complet toohello S3 objet.

### <a name="sample-dataset-with-prefix"></a>Exemple de jeu de données avec le préfixe

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "prefix": "testFolder/test",
            "bucketName": "testbucket",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
### <a name="sample-dataset-with-version"></a>Exemple de jeu de données (avec la version)

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "key": "testFolder/test.orc",
            "bucketName": "testbucket",
            "version": "XXXXXXXXXczm0CJajYkHf0_k6LhBmkcL",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

### <a name="dynamic-paths-for-s3"></a>Chemins d’accès dynamiques pour S3
Hello précédent exemple utilise des valeurs fixes pour hello **clé** et **bucketName** propriétés dans le jeu de données hello Amazon S3.

```json
"key": "testFolder/test.orc",
"bucketName": "testbucket",
```

Vous pouvez demander à Data Factory de calculer ces propriétés dynamiquement au moment de l’exécution à l’aide de variables système telles que SliceStart.

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

Vous pouvez effectuer même hello pour hello **préfixe** propriété d’un jeu de données Amazon S3. Pour obtenir la liste des fonctions et variables prises en charge, consultez [Variables système et fonctions Data Factory](data-factory-functions-variables.md).

## <a name="copy-activity-properties"></a>Propriétés de l’activité de copie
Pour obtenir la liste complète des sections et propriétés disponibles pour la définition des activités, voir [Création de pipelines](data-factory-create-pipelines.md). Les propriétés comme le nom, la description, les tables d'entrée et de sortie et les différentes stratégies sont disponibles pour tous les types d'activités. Propriétés disponibles dans hello **typeProperties** section d’activité hello varient selon chaque type d’activité. Pour l’activité de copie hello, les propriétés varient selon les types de sources et récepteurs hello. Lorsqu’une source de l’activité de copie hello est de type **FileSystemSource** (qui inclut Amazon S3), hello suivant la propriété est disponible dans **typeProperties** section :

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| recursive |Spécifie si la liste de toorecursively S3 objets sous le répertoire de hello. |true/false |Non |

## <a name="json-example-copy-data-from-amazon-s3-tooazure-blob-storage"></a>Exemple de JSON : copier des données d’Amazon S3 tooAzure stockage d’objets Blob
Cet exemple montre comment toocopy des données à partir d’Amazon S3 tooan stockage d’objets Blob Azure. Toutefois, les données peuvent être copiées directement trop[des récepteurs hello qui sont pris en charge](data-factory-data-movement-activities.md#supported-data-stores-and-formats) à l’aide de l’activité de copie hello dans la fabrique de données.

exemple Hello fournit les définitions de JSON pour hello suivant des entités de fabrique de données. Vous pouvez utiliser ces définitions de toocreate un pipeline toocopy des données d’Amazon S3 tooBlob stockage, à l’aide de hello [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), ou [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).   

* Un service lié de type [AwsAccessKey](#linked-service-properties).
* Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
* Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [AmazonS3](#dataset-properties).
* Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* Un [pipeline](data-factory-create-pipelines.md) avec activité de copie qui utilise [FileSystemSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

exemple Hello copie des données d’Amazon S3 tooan objets blob Azure toutes les heures. propriétés JSON Hello utilisées dans ces exemples sont décrits dans les sections suivantes des exemples de hello.

### <a name="amazon-s3-linked-service"></a>Service lié Amazon S3

```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a>Service lié Azure Storage

```json
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

### <a name="amazon-s3-input-dataset"></a>Jeu de données d’entrée Amazon S3

Paramètre **« external » : true** informe service Data Factory de hello ce jeu de données hello est la fabrique de données externe toohello. Définir tootrue de cette propriété sur un jeu de données d’entrée qui n’est pas généré par une activité dans le pipeline de hello.

```json
    {
        "name": "AmazonS3InputDataset",
        "properties": {
            "type": "AmazonS3",
            "linkedServiceName": "AmazonS3LinkedService",
            "typeProperties": {
                "key": "testFolder/test.orc",
                "bucketName": "testbucket",
                "format": {
                    "type": "OrcFormat"
                }
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "external": true
        }
    }
```


### <a name="azure-blob-output-dataset"></a>Jeu de données de sortie d’objet Blob Azure

Les données sont écrites tooa nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1). chemin d’accès du dossier Hello pour l’objet blob de hello est évaluée dynamiquement en fonction de l’heure de début hello de tranche hello qui est en cours de traitement. chemin d’accès du dossier Hello utilise hello des parties d’année, mois, jours et heures de l’heure de début hello.

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/fromamazons3/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="copy-activity-in-a-pipeline-with-an-amazon-s3-source-and-a-blob-sink"></a>Activité de copie dans un pipeline avec une source Amazon S3 et un récepteur blob

Hello pipeline contient une activité de copie qui est configuré toouse hello des jeux de données d’entrée et de sortie, et est toorun planifiée toutes les heures. Dans la définition JSON du pipeline hello, hello **source** type est défini trop**FileSystemSource**, et **récepteur** type est défini trop**BlobSink**.

```json
{
    "name": "CopyAmazonS3ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "FileSystemSource",
                        "recursive": true
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AmazonS3InputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutputDataSet"
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
                "name": "AmazonS3ToBlob"
            }
        ],
        "start": "2014-08-08T18:00:00Z",
        "end": "2014-08-08T19:00:00Z"
    }
}
```
> [!NOTE]
> toomap des colonnes à partir d’un toocolumns de jeu de données source à partir d’un jeu de données récepteur, consultez [mappage des colonnes de jeu de données dans Azure Data Factory](data-factory-map-columns.md).


## <a name="next-steps"></a>Étapes suivantes
Consultez hello suivant des articles :

* impact sur les performances de déplacement des données (activité de copie) dans la fabrique de données et différentes façons toooptimize des facteurs toolearn sur la clé, consultez hello [copier activité guide des performances et paramétrage](data-factory-copy-activity-performance.md).

* Pour obtenir des instructions pour la création d’un pipeline avec une activité de copie, consultez hello [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
