---
title: "aaaMove des données à partir de SAP HANA à l’aide d’Azure Data Factory | Documents Microsoft"
description: "En savoir plus sur la façon de toomove les données à partir de SAP HANA à l’aide d’Azure Data Factory."
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
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 5cefe4c8ed01ea4e86e02496b2f8a9083d0b949c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-sap-hana-using-azure-data-factory"></a>Déplacer des données depuis SAP HANA à l’aide d’Azure Data Factory
Cet article explique comment toouse hello activité de copie de données de toomove Azure Data Factory à partir d’un ordinateur local SAP HANA. Il repose sur hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, qui présente une vue d’ensemble du déplacement des données avec l’activité de copie hello.

Vous pouvez copier les données d’une banque de données locale SAP HANA données magasin tooany pris en charge récepteur. Pour une liste de données pris en charge des magasins récepteurs par l’activité de copie hello, consultez hello [prise en charge des magasins de données](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table. Fabrique de données prend actuellement en charge uniquement le déplacement de banques de données à partir d’un tooother de données SAP HANA, mais pas pour déplacer des données d’autres données de magasins tooan SAP HANA.

## <a name="supported-versions-and-installation"></a>Versions prises en charge et installation
Ce connecteur prend en charge n’importe quelle version de base de données SAP HANA. Il prend en charge la copie de données à partir de modèles d’informations HANA (comme les vues Analyse et Calcul) et les tables Ligne/Colonne à l’aide de requêtes SQL.

tooenable hello connectivité toohello instance de SAP HANA, installez hello suivant des composants :
- **Passerelle de gestion des données**: service Data Factory prend en charge la connexion de données locales tooon magasins (y compris SAP HANA) à l’aide d’un composant appelé passerelle de gestion des données. toolearn sur la passerelle de gestion des données et des instructions détaillées pour configurer la passerelle de hello, consultez [magasin de données toocloud du magasin de données de déplacement entre des données locales](data-factory-move-data-between-onprem-and-cloud.md) l’article. Passerelle est requise même si hello SAP HANA est hébergé dans une machine virtuelle de Azure IaaS (VM). Vous pouvez installer la passerelle de hello sur hello même machine virtuelle en tant que données de hello stocker ou sur un ordinateur différent virtuel tant que passerelle de hello peuvent se connecter toohello de base de données.
- **Pilote ODBC de HANA SAP** sur l’ordinateur de passerelle hello. Vous pouvez télécharger le pilote ODBC de HANA SAP de hello de hello [centre de téléchargement de logiciel SAP](https://support.sap.com/swdc). Recherche par mot clé de hello **SAP HANA CLIENT pour Windows**. 

## <a name="getting-started"></a>Prise en main
Vous pouvez créer un pipeline avec une activité de copie qui déplace les données d’un magasin de données Cassandra local à l’aide de différents outils/API. 

- toocreate de façon plus simple Hello un pipeline est toouse hello **Assistant copie de**. Consultez [didacticiel : créer un pipeline à l’aide d’Assistant copie de](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapides sur la création d’un pipeline à l’aide d’Assistant de données de copie hello. 
- Vous pouvez également utiliser hello suivant outils toocreate un pipeline : **portail Azure**, **Visual Studio**, **Azure PowerShell**, **modèle Azure Resource Manager** , **API .NET**, et **API REST**. Consultez [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions toocreate un pipeline avec une activité de copie. 

Si vous utilisez hello ou une API, vous effectuez hello suivant les étapes toocreate un pipeline qui déplace la banque de données récepteur tooa du magasin de données à partir des données d’une source :

1. Créer **services liés** fabrique de données tooyour toolink les données d’entrée et de sortie magasins.
2. Créer **datasets** toorepresent d’entrée et sortie l’opération de copie des données pour hello. 
3. Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie. 

Lorsque vous utilisez hello Assistant, les définitions de JSON pour ces entités de fabrique de données (services liés, des datasets et pipeline de hello) sont créées automatiquement pour vous. Lorsque vous utilisez/API des outils (à l’exception des API .NET), vous définissez ces entités de fabrique de données à l’aide du format JSON de hello.  Pour voir un exemple avec des définitions de JSON pour les entités de fabrique de données qui sont utilisées toocopy des données à partir d’un ordinateur local SAP HANA, [exemple de JSON : copier des données à partir de SAP HANA tooAzure Blob](#json-example-copy-data-from-sap-hana-to-azure-blob) section de cet article. 

Hello les sections suivantes fournit des détails sur les propriétés JSON qui sont le magasin de données SAP HANA utilisé toodefine Data Factory entités tooan spécifique :

## <a name="linked-service-properties"></a>Propriétés du service lié
Hello tableau suivant fournit la description pour JSON éléments tooSAP spécifique HANA de service lié.

Propriété | Description | Valeurs autorisées | Requis
-------- | ----------- | -------------- | --------
server | Nom du serveur hello sur quel hello SAP HANA instance réside. Si votre serveur utilise un port personnalisé, spécifiez `server:port`. | string | Oui
authenticationType | Type d'authentification. | chaîne. « Basic » ou « Windows » | Oui 
username | Nom d’utilisateur de hello qui a le serveur d’accès toohello SAP | string | Oui
password | Mot de passe utilisateur de hello. | string | Oui
gatewayName | Nom de passerelle hello hello service Data Factory doit utiliser l’instance de SAP HANA tooconnect toohello sur site. | string | Oui
Encryptedcredential | chaîne d’identification de Hello chiffré. | string | Non

## <a name="dataset-properties"></a>Propriétés du jeu de données
Pour obtenir une liste complète des sections et les propriétés disponibles pour définir des jeux de données, consultez hello [création de datasets](data-factory-create-datasets.md) l’article. Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données (SQL Azure, Azure Blob, Azure Table, etc.).

Hello **typeProperties** section est différente pour chaque type de jeu de données et fournit des informations sur l’emplacement de hello de données hello dans le magasin de données hello. Aucune propriété spécifique au type pris en charge pour le dataset de SAP HANA hello de type **RelationalTable**. 


## <a name="copy-activity-properties"></a>Propriétés de l’activité de copie
Pour obtenir une liste complète des sections et les propriétés disponibles pour la définition d’activités, consultez hello [création de Pipelines](data-factory-create-pipelines.md) l’article. Les propriétés comme le nom, la description, les tables d'entrée et de sortie et les différentes stratégies sont disponibles pour tous les types d’activités.

Tandis que les propriétés disponibles dans hello **typeProperties** section d’activité hello varient selon chaque type d’activité. Pour l’activité de copie, ils varient selon les types de sources et récepteurs hello.

Lorsque la source de l’activité de copie est de type **RelationalSource** (qui inclut SAP HANA), hello propriétés suivantes est disponible dans la section de typeProperties :

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| query | Spécifie les hello requête tooread de données SQL à partir de l’instance de SAP HANA hello. | Requête SQL. | Oui |

## <a name="json-example-copy-data-from-sap-hana-tooazure-blob"></a>Exemple de JSON : copier des données à partir de SAP HANA tooAzure Blob
Hello exemple suivant fournit des exemples de définitions de JSON que vous pouvez utiliser toocreate un pipeline à l’aide de [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Cet exemple montre comment toocopy des données à partir d’un tooan de SAP HANA local stockage d’objets Blob Azure. Toutefois, les données peuvent être copiées **directement** tooany de récepteurs hello répertoriés [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) à l’aide de hello activité de copie dans Azure Data Factory.  

> [!IMPORTANT]
> Cet exemple fournit des extraits de code JSON. Il n’inclut pas d’instructions détaillées pour créer la fabrique de données hello. Les instructions se trouvent dans l’article [Déplacement de données entre des emplacements locaux et le cloud](data-factory-move-data-between-onprem-and-cloud.md) .

exemple Hello a hello suivant des entités de fabrique de données :

1. Un service lié de type [SapHana](#linked-service-properties).
2. Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [RelationalTable](#dataset-properties).
4. Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [RelationalSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

exemple Hello copie toutes les heures des données à partir d’un tooan d’instance SAP HANA blob Azure. propriétés JSON Hello utilisées dans ces exemples sont décrits dans les sections suivantes des exemples de hello.

Dans un premier temps, le programme d’installation passerelle de gestion des données hello. instructions de Hello sont Bonjour [déplacement des données entre les emplacements locaux et cloud](data-factory-move-data-between-onprem-and-cloud.md) l’article.

### <a name="sap-hana-linked-service"></a>Service lié SAP HANA
Cela liées à des liens de service votre fabrique de données SAP HANA instance toohello. propriété de type Hello est définie trop**SapHana**. section de typeProperties Hello fournit des informations de connexion pour l’instance de SAP HANA hello.

```json
{
    "name": "SapHanaLinkedService",
    "properties":
    {
        "type": "SapHana",
        "typeProperties":
        {
            "server": "<server name>",
            "authenticationType": "<Basic, or Windows>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}

```

### <a name="azure-storage-linked-service"></a>Service lié Azure Storage
Cela lié à des liens de service votre fabrique de données toohello compte Azure Storage. propriété de type Hello est définie trop**AzureStorage**. section de typeProperties Hello fournit des informations de connexion pour hello compte de stockage Azure.

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

### <a name="sap-hana-input-dataset"></a>Jeu de données d’entrée SAP HANA

Ce jeu de données définit un jeu de données SAP HANA hello. Vous définissez type hello du jeu de données de Data Factory hello trop**RelationalTable**. Actuellement, vous ne spécifiez pas de propriétés propres à un type pour un jeu de données SAP HANA. requête Hello dans la définition de l’activité de copie de hello spécifie quel tooread de données à partir de l’instance de SAP HANA hello. 

Définition de propriété externe tootrue informe service Data Factory de hello cette table hello est la fabrique de données externe toohello n’est pas générée par une activité dans la fabrique de données hello.

Propriétés de la fréquence et l’intervalle définit la planification de hello. Dans ce cas, les données de salutation sont en lecture à partir de l’instance de SAP HANA hello toutes les heures. 

```json
{
    "name": "SapHanaDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapHanaLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

### <a name="azure-blob-output-dataset"></a>Jeu de données de sortie d’objet Blob Azure
Ce jeu de données définit un jeu de données objet Blob Azure hello sortie. propriété de type Hello est définie à tooAzureBlob. section de typeProperties Hello fournit où sont stockées les données hello copiées à partir de l’instance de SAP HANA hello. les données de salutation sont écrit tooa nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1). chemin d’accès du dossier Hello pour l’objet blob de hello est évaluée dynamiquement en fonction de l’heure de début hello de tranche hello qui est en cours de traitement. chemin d’accès du dossier Hello utilise l’année, mois, jours et heures des parties de l’heure de début hello.

```json
{
    "name": "AzureBlobDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/saphana/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="pipeline-with-copy-activity"></a>Pipeline avec activité de copie

Hello pipeline contient une activité de copie qui est configuré toouse hello des jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures. Dans la définition JSON du pipeline hello, hello **source** type est défini trop**RelationalSource** (pour une source de SAP HANA) et **récepteur** type est défini trop**BlobSink**. la requête SQL Hello spécifiée pour hello **requête** propriété sélectionne des données de hello Bonjour au-delà de toocopy d’heure.

```json
{
    "name": "CopySapHanaToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "<SQL Query for HANA>"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "SapHanaDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobDataSet"
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
                "name": "SapHanaToBlob"
            }
        ],
        "start": "2017-03-01T18:00:00Z",
        "end": "2017-03-01T19:00:00Z"
    }
}
```


### <a name="type-mapping-for-sap-hana"></a>Mappage de type pour SAP HANA
Comme mentionné dans hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, l’activité de copie effectue les conversions de type automatique à partir de types de sources de toosink types avec hello suivant l’approche en deux étapes :

1. Convertir à partir de la source native types too.NET type
2. Conversion de type de récepteur de toonative de type .NET

Lors du déplacement des données à partir de SAP HANA, hello suivant les mappages est utilisé à partir de types de too.NET de types de SAP HANA.

Type SAP HANA | Type basé sur .NET
------------- | ---------------
TINYINT | Byte
SMALLINT | Int16
INT | Int32
BIGINT | Int64
REAL | Single
DOUBLE | Single
DÉCIMAL | Décimal
BOOLEAN | Byte
VARCHAR | String
NVARCHAR | String
CLOB | Byte[]
ALPHANUM | String
BLOB | Byte[]
DATE | DateTime
TEMPS | intervalle de temps
TIMESTAMP | DateTime
SECONDDATE | DateTime

## <a name="known-limitations"></a>Limites connues
Il existe quelques limitations connues lors de la copie des données à partir de SAP HANA :

- Les chaînes NVARCHAR sont tronquées toomaximum la longueur de 4 000 caractères Unicode
- SMALLDECIMAL n’est pas pris en charge
- VARBINARY n’est pas pris en charge
- Les dates valides sont celles comprises entre 1899/12/30 et 9999/12/31

## <a name="map-source-toosink-columns"></a>Mapper les colonnes de source toosink
toolearn sur le mappage des colonnes dans toocolumns du jeu de données source dans le jeu de données récepteur, consultez [mappage des colonnes de jeu de données dans Azure Data Factory](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Lecture renouvelée de sources relationnelles
Lors de la copie des données à partir de banques de données relationnelles, conserver la répétabilité dans l’esprit tooavoid des résultats inattendus. Dans Azure Data Factory, vous pouvez réexécuter une tranche manuellement. Vous pouvez également configurer une stratégie de nouvelles tentatives pour un jeu de données, afin qu’une tranche soit réexécutée en cas de défaillance. Lorsqu’une tranche est exécuté à nouveau dans les deux cas, vous devez toomake vraiment qui hello des mêmes données n’est en lecture aucune question comment plusieurs fois une tranche est exécutée. Voir [Lecture renouvelée de sources relationnelles](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)

## <a name="performance-and-tuning"></a>Performances et réglage
Consultez [copie activité optimiser les performances et Guide d’optimisation](data-factory-copy-activity-performance.md) toolearn sur la clé de facteurs d’affecter les performances de transfert de données (activité de copie) dans Azure Data Factory et de différentes façons toooptimize il.
