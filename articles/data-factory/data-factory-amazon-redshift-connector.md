---
title: "données Amazon Redshift à l’aide de la fabrique de données aaaMove | Documents Microsoft"
description: "En savoir plus sur la façon de toomove données Amazon Redshift à l’aide d’Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 01d15078-58dc-455c-9d9d-98fbdf4ea51e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: 2a097320734ebdd57282d250f7fdba35741777f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-amazon-redshift-using-azure-data-factory"></a>Déplacer des données depuis Amazon Redshift à l’aide d’Azure Data Factory
Cet article explique comment toouse hello activité de copie de données Azure Data Factory toomove Amazon Redshift. article de Hello s’appuie sur hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, qui présente une vue d’ensemble du déplacement des données avec l’activité de copie hello. 

Vous pouvez copier des données à partir du magasin de données récepteur Amazon Redshift tooany pris en charge. Pour obtenir la liste des magasins de données pris en charge en tant que les récepteurs par l’activité de copie hello, consultez [prise en charge des magasins de données](data-factory-data-movement-activities.md#supported-data-stores-and-formats). Fabrique de données prend actuellement en charge le déplacement des données à partir des magasins de données Amazon Redshift tooother, mais ne pas pour le déplacement des données à partir d’autres tooAmazon de magasins de données Redshift.

## <a name="prerequisites"></a>Composants requis
* Si vous déplacez une banque de données locale données tooan, installez [passerelle de gestion des données](data-factory-data-management-gateway.md) sur un ordinateur local. Ensuite, accordez passerelle de gestion des données (utiliser une adresse IP de l’ordinateur de hello) hello tooAmazon Redshift cluster d’accès. Consultez [cluster de toohello accès autoriser](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html) pour obtenir des instructions.
* Si vous déplacez le magasin de données tooan données Azure, consultez [plages IP de centre de données Azure](https://www.microsoft.com/download/details.aspx?id=41653) pour l’adresse IP de calcul de hello et les plages SQL utilisées par les centres de données Azure hello.

## <a name="getting-started"></a>Prise en main
Vous pouvez créer un pipeline avec une activité de copie qui déplace les données d’une source Amazon Redshift à l’aide de différents outils/API.

toocreate de façon plus simple Hello un pipeline est toouse hello **Assistant copie de**. Consultez [didacticiel : créer un pipeline à l’aide d’Assistant copie de](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapides sur la création d’un pipeline à l’aide d’Assistant de données de copie hello.

Vous pouvez également utiliser hello suivant outils toocreate un pipeline : **portail Azure**, **Visual Studio**, **Azure PowerShell**, **modèle Azure Resource Manager** , **API .NET**, et **API REST**. Consultez [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions toocreate un pipeline avec une activité de copie. 

Si vous utilisez hello ou une API, vous effectuez hello suivant les étapes toocreate un pipeline qui déplace la banque de données récepteur tooa du magasin de données à partir des données d’une source : 

1. Créer **services liés** fabrique de données tooyour toolink les données d’entrée et de sortie magasins.
2. Créer **datasets** toorepresent d’entrée et sortie l’opération de copie des données pour hello. 
3. Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie. 

Lorsque vous utilisez hello Assistant, les définitions de JSON pour ces entités de fabrique de données (services liés, des datasets et pipeline de hello) sont créées automatiquement pour vous. Lorsque vous utilisez/API des outils (à l’exception des API .NET), vous définissez ces entités de fabrique de données à l’aide du format JSON de hello.  Pour voir un exemple avec des définitions de JSON pour les entités de fabrique de données qui sont utilisées toocopy des données à partir d’une banque de données Amazon Redshift, [exemple de JSON : copier des données d’Amazon Redshift tooAzure Blob](#json-example-copy-data-from-amazon-redshift-to-azure-blob) section de cet article. 

Hello les sections suivantes fournit des détails sur les propriétés JSON qui sont utilisés toodefine Data Factory entités spécifique tooAmazon Redshift : 

## <a name="linked-service-properties"></a>Propriétés du service lié
Hello tableau suivant fournit la description pour JSON éléments tooAmazon spécifique Redshift lié service.

| Propriété | Description | Requis |
| --- | --- | --- |
| type |propriété de type Hello doit indiquer : **AmazonRedshift**. |Oui |
| server |Nom hôte ou adresse IP du serveur d’Amazon Redshift hello. |Oui |
| port |nombre de Hello de port TCP hello hello Amazon Redshift serveur utilise toolisten pour les connexions client. |Non, valeur par défaut : 5439 |
| database |Nom de la base de données Amazon Redshift hello. |Oui |
| username |Nom d’utilisateur qui a la base de données access toohello. |Oui |
| password |Mot de passe pour le compte d’utilisateur hello. |Oui |

## <a name="dataset-properties"></a>Propriétés du jeu de données
Pour obtenir une liste complète des sections et les propriétés disponibles pour définir des jeux de données, consultez hello [création de datasets](data-factory-create-datasets.md) l’article. Les sections comme la structure, la disponibilité et la stratégie sont similaires pour tous les types de jeux de données (SQL Azure, Azure Blob, Azure Table, etc.).

Hello **typeProperties** section est différente pour chaque type de jeu de données. Il fournit des informations sur l’emplacement de hello de données hello dans le magasin de données hello. jeu de données de type Hello typeProperties section **RelationalTable** (qui comprend de jeu de données Amazon Redshift) a hello propriétés suivantes

| Propriété | Description | Requis |
| --- | --- | --- |
| TableName |Nom de table hello dans la base de données Amazon Redshift hello ce service lié fait référence à. |Non (si la **requête** de **RelationalSource** est spécifiée) |

## <a name="copy-activity-properties"></a>Propriétés de l’activité de copie
Pour obtenir une liste complète des sections et les propriétés disponibles pour la définition d’activités, consultez hello [création de Pipelines](data-factory-create-pipelines.md) l’article. Les propriétés comme le nom, la description, les tables d'entrée et de sortie et les différentes stratégies sont disponibles pour tous les types d'activités.

Tandis que les propriétés disponibles dans hello **typeProperties** section d’activité hello varient selon chaque type d’activité. Pour l’activité de copie, ils varient selon les types de sources et récepteurs hello.

Lorsque la source de l’activité de copie est de type **RelationalSource** (qui inclut Amazon Redshift), hello propriétés suivantes est disponible dans la section de typeProperties :

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| query |Utiliser des données tooread hello requête personnalisée. |Chaîne de requête SQL. Par exemple : select * from MyTable. |Non (si **tableName** de **dataset** est spécifiée) |

## <a name="json-example-copy-data-from-amazon-redshift-tooazure-blob"></a>Exemple de JSON : copier des données d’Amazon Redshift tooAzure Blob
Cet exemple montre la base de données toocopy à partir d’un Amazon Redshift tooan stockage d’objets Blob Azure. Toutefois, les données peuvent être copiées **directement** tooany de récepteurs hello indiqué [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) à l’aide de hello activité de copie dans Azure Data Factory.  

exemple Hello a hello suivant des entités de fabrique de données :

* Un service lié de type [AmazonRedshift](#linked-service-properties).
* Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
* Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [RelationalTable](#dataset-properties).
* Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [RelationalSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md##copy-activity-properties).

exemple Hello copie des données à partir d’un résultat de requête dans l’objet blob de Amazon Redshift tooa toutes les heures. propriétés JSON Hello utilisées dans ces exemples sont décrits dans les sections suivantes des exemples de hello.

**Service lié Amazon Redshift :**

```json
{
    "name": "AmazonRedshiftLinkedService",
    "properties":
    {
        "type": "AmazonRedshift",
        "typeProperties":
        {
            "server": "< hello IP address or host name of hello Amazon Redshift server >",
            "port": <hello number of hello TCP port that hello Amazon Redshift server uses toolisten for client connections.>,
            "database": "<hello database name of hello Amazon Redshift database>",
            "username": "<username>",
            "password": "<password>"
        }
    }
}
```

**Service lié Azure Storage :**

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
**Jeu de données d’entrée Amazon Redshift :**

Paramètre `"external": true` informe le service de fabrique de données hello ce jeu de données hello est la fabrique de données externe toohello et n’est pas généré par une activité dans la fabrique de données hello. Définir tootrue de cette propriété sur un jeu de données d’entrée qui n’est pas généré par une activité dans le pipeline de hello.

```json
{
    "name": "AmazonRedshiftInputDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "AmazonRedshiftLinkedService",
        "typeProperties": {
            "tableName": "<Table name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

**Jeu de données de sortie Azure Blob :**

Les données sont écrites tooa nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1). chemin d’accès du dossier Hello pour l’objet blob de hello est évaluée dynamiquement en fonction de l’heure de début hello de tranche hello qui est en cours de traitement. chemin d’accès du dossier Hello utilise l’année, mois, jours et heures des parties de l’heure de début hello.

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/fromamazonredshift/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

**Activité de copie dans un pipeline, avec une source Azure Redshift (RelationalSource) et un récepteur blob :**

Hello pipeline contient une activité de copie qui est configuré toouse hello des jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures. Dans la définition JSON du pipeline hello, hello **source** type est défini trop**RelationalSource** et **récepteur** type est défini trop**BlobSink**. la requête SQL Hello spécifiée pour hello **requête** propriété sélectionne des données de hello Bonjour au-delà de toocopy d’heure.

```json
{
    "name": "CopyAmazonRedshiftToBlob",
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
                        "name": "AmazonRedshiftInputDataset"
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
                "name": "AmazonRedshiftToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```
### <a name="type-mapping-for-amazon-redshift"></a>Mappage de type pour Amazon Redshift
Comme mentionné dans hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, l’activité de copie effectue les conversions de type automatique à partir de types de sources de toosink types avec hello suivant l’approche en deux étapes :

1. Convertir à partir de la source native types too.NET type
2. Conversion de type de récepteur de toonative de type .NET

Lors du déplacement des données tooAmazon Redshift, hello suivant les mappages est utilisé à partir des types de too.NET Amazon Redshift types.

| Type Amazon Redshift | Type basé sur .NET |
| --- | --- |
| SMALLINT |Int16 |
| INTEGER |Int32 |
| BIGINT |Int64 |
| DÉCIMAL |DÉCIMAL |
| REAL |Single |
| DOUBLE PRECISION |Double |
| BOOLEAN |String |
| CHAR |String |
| VARCHAR |String |
| DATE |DateTime |
| TIMESTAMP |DateTime |
| TEXTE |String |

## <a name="map-source-toosink-columns"></a>Mapper les colonnes de source toosink
toolearn sur le mappage des colonnes dans toocolumns du jeu de données source dans le jeu de données récepteur, consultez [mappage des colonnes de jeu de données dans Azure Data Factory](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Lecture renouvelée de sources relationnelles
Lors de la copie des données à partir de banques de données relationnelles, conserver la répétabilité dans l’esprit tooavoid des résultats inattendus. Dans Azure Data Factory, vous pouvez réexécuter une tranche manuellement. Vous pouvez également configurer une stratégie de nouvelles tentatives pour un jeu de données, afin qu’une tranche soit réexécutée en cas de défaillance. Lorsqu’une tranche est exécuté à nouveau dans les deux cas, vous devez toomake vraiment qui hello des mêmes données n’est en lecture aucune question comment plusieurs fois une tranche est exécutée. Voir [Lecture renouvelée de sources relationnelles](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)

## <a name="performance-and-tuning"></a>Performances et réglage
Consultez [copie activité optimiser les performances et Guide d’optimisation](data-factory-copy-activity-performance.md) toolearn sur la clé de facteurs d’affecter les performances de transfert de données (activité de copie) dans Azure Data Factory et de différentes façons toooptimize il.

## <a name="next-steps"></a>Étapes suivantes
Consultez hello suivant des articles :

* [Didacticiel de l’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions détaillées sur la création d’un pipeline avec Activité de copie.
