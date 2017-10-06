---
title: "données aaaMove MongoDB à l’aide de la fabrique de données | Documents Microsoft"
description: "Découvrez comment toomove données MongoDB de base de données à l’aide d’Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 10ca7d9a-7715-4446-bf59-2d2876584550
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: 154e85712f27b978976c7499c43dde9429f124c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-mongodb-using-azure-data-factory"></a>Déplacer des données depuis MongoDB à l’aide d’Azure Data Factory
Cet article explique comment toouse hello activité de copie de données de toomove Azure Data Factory à partir d’une base de données locale MongoDB. Il repose sur hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, qui présente une vue d’ensemble du déplacement des données avec l’activité de copie hello.

Vous pouvez copier les données d’une banque de données locale MongoDB données magasin tooany pris en charge récepteur. Pour une liste de données pris en charge des magasins récepteurs par l’activité de copie hello, consultez hello [prise en charge des magasins de données](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table. Fabrique de données prend en charge uniquement le déplacement tooother les magasins de données du magasin de données à partir de données MongoDB, mais ne pas pour déplacer des données d’une autre banque de données MongoDB des tooan de magasins de données. 

## <a name="prerequisites"></a>Composants requis
Pour hello Azure Data Factory service toobe tooconnect en mesure de tooyour MongoDB base de données locale, vous devez installer hello suivant des composants :

- Versions MongoDB prises en charge : 2.4, 2.6, 3.0 et 3.2.
- Passerelle de gestion des données sur hello même machine cette base de données hôtes hello ou sur un tooavoid machine distincte en concurrence pour les ressources de base de données hello. Passerelle de gestion des données est un logiciel qui se connecte des services de toocloud de sources de données sur site de manière sécurisée et gérée. Consultez l’article [Passerelle de gestion des données](data-factory-data-management-gateway.md) pour obtenir des informations détaillées sur la passerelle de gestion des données. Consultez [déplacer des données locales toocloud](data-factory-move-data-between-onprem-and-cloud.md) article pour obtenir des instructions sur la configuration de passerelle de hello données toomove de pipeline de données.

    Lorsque vous installez la passerelle de hello, il installe automatiquement un tooMongoDB tooconnect du pilote utilisé Microsoft MongoDB ODBC.

    > [!NOTE]
    > Vous devez toouse hello passerelle tooconnect tooMongoDB même s’il est hébergé dans les machines virtuelles Azure IaaS. Si vous essayez d’instance de tooan tooconnect de MongoDB hébergé dans le cloud, vous pouvez également installer une instance de passerelle hello Bonjour IaaS VM.

## <a name="getting-started"></a>Prise en main
Vous pouvez créer un pipeline avec une activité de copie qui déplace les données d’un magasin de données MongoDB local à l’aide de différents outils/API.

toocreate de façon plus simple Hello un pipeline est toouse hello **Assistant copie de**. Consultez [didacticiel : créer un pipeline à l’aide d’Assistant copie de](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapides sur la création d’un pipeline à l’aide d’Assistant de données de copie hello.

Vous pouvez également utiliser hello suivant outils toocreate un pipeline : **portail Azure**, **Visual Studio**, **Azure PowerShell**, **modèle Azure Resource Manager** , **API .NET**, et **API REST**. Consultez [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions toocreate un pipeline avec une activité de copie. 

Si vous utilisez hello ou une API, vous effectuez hello suivant les étapes toocreate un pipeline qui déplace la banque de données récepteur tooa du magasin de données à partir des données d’une source : 

1. Créer **services liés** fabrique de données tooyour toolink les données d’entrée et de sortie magasins.
2. Créer **datasets** toorepresent d’entrée et sortie l’opération de copie des données pour hello. 
3. Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie. 

Lorsque vous utilisez hello Assistant, les définitions de JSON pour ces entités de fabrique de données (services liés, des datasets et pipeline de hello) sont créées automatiquement pour vous. Lorsque vous utilisez/API des outils (à l’exception des API .NET), vous définissez ces entités de fabrique de données à l’aide du format JSON de hello.  Pour voir un exemple avec des définitions de JSON pour les entités de fabrique de données qui sont des données à partir d’une banque de données locale MongoDB toocopy utilisés, [exemple de JSON : copier des données à partir de MongoDB tooAzure Blob](#json-example-copy-data-from-mongodb-to-azure-blob) section de cet article. 

Hello les sections suivantes fournit des détails sur les propriétés JSON qui sont utilisés toodefine Data Factory entités spécifiques tooMongoDB source :

## <a name="linked-service-properties"></a>Propriétés du service lié
Hello tableau suivant fournit la description pour les éléments JSON spécifiques trop**OnPremisesMongoDB** service lié.

| Propriété | Description | Requis |
| --- | --- | --- |
| type |propriété de type Hello doit indiquer : **OnPremisesMongoDb** |Oui |
| server |Nom hôte ou adresse IP du serveur de MongoDB hello. |Oui |
| port |Le port TCP qui hello MongoDB serveur utilise toolisten pour les connexions client. |Facultatif, valeur par défaut : 27017 |
| authenticationType |De base ou anonyme. |Oui |
| username |Tooaccess du compte utilisateur MongoDB. |Oui (si l’authentification de base est utilisée). |
| password |Mot de passe utilisateur de hello. |Oui (si l’authentification de base est utilisée). |
| authSource |Nom de la base de données MongoDB hello que vous souhaitez toouse toocheck vos informations d’identification pour l’authentification. |Facultatif (si l’authentification de base est utilisée). par défaut : utilise le compte d’administrateur hello et de la base de données de hello spécifié à l’aide de la propriété databaseName. |
| databaseName |Nom de la base de données MongoDB hello que vous souhaitez tooaccess. |Oui |
| gatewayName |Nom de la passerelle hello qui accède au magasin de données hello. |Oui |
| Encryptedcredential |Informations d’identification chiffrées par la passerelle. |Facultatif |

## <a name="dataset-properties"></a>Propriétés du jeu de données
Pour obtenir une liste complète des sections et les propriétés disponibles pour définir des jeux de données, consultez hello [création de datasets](data-factory-create-datasets.md) l’article. Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données (SQL Azure, Azure Blob, Azure Table, etc.).

Hello **typeProperties** section est différente pour chaque type de jeu de données et fournit des informations sur l’emplacement de hello de données hello dans le magasin de données hello. jeu de données de type Hello typeProperties section **MongoDbCollection** a hello propriétés suivantes :

| Propriété | Description | Requis |
| --- | --- | --- |
| collectionName |Nom de collection hello dans la base de données MongoDB. |Oui |

## <a name="copy-activity-properties"></a>Propriétés de l’activité de copie
Pour obtenir une liste complète des sections et les propriétés disponibles pour la définition d’activités, consultez hello [création de Pipelines](data-factory-create-pipelines.md) l’article. Les propriétés comme le nom, la description, les tables d’entrée et de sortie et la stratégie sont disponibles pour tous les types d’activités.

Propriétés disponibles dans hello **typeProperties** section de l’activité de hello sur hello autre part varient selon chaque type d’activité. Pour l’activité de copie, ils varient selon les types de sources et récepteurs hello.

Lorsque la source de hello est de type **MongoDbSource** hello propriétés suivantes est disponible dans la section de typeProperties :

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| query |Utiliser des données tooread hello requête personnalisée. |Chaîne de requête SQL-92. Par exemple : select * from MyTable. |Non (si **collectionName** du **jeu de données** est spécifié) |



## <a name="json-example-copy-data-from-mongodb-tooazure-blob"></a>Exemple de JSON : copier des données à partir de MongoDB tooAzure Blob
Cet exemple fournit des exemples de définitions de JSON que vous pouvez utiliser toocreate un pipeline à l’aide de [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Il montre comment toocopy des données à partir d’un tooan de MongoDB local stockage d’objets Blob Azure. Toutefois, les données peuvent être copié tooany de récepteurs hello indiqué [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) à l’aide de hello activité de copie dans Azure Data Factory.

exemple Hello a hello suivant des entités de fabrique de données :

1. Un service lié de type [OnPremisesMongoDb](#linked-service-properties).
2. Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [MongoDbCollection](#dataset-properties).
4. Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [MongoDbSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

exemple Hello copie des données à partir d’un résultat de requête dans l’objet blob tooa de base de données MongoDB toutes les heures. propriétés JSON Hello utilisées dans ces exemples sont décrits dans les sections suivantes des exemples de hello.

Dans un premier temps, le programme d’installation passerelle de gestion des données hello conformément aux instructions hello Bonjour [passerelle de gestion des données](data-factory-data-management-gateway.md) l’article.

**Service lié MongoDB :**

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties":
    {
        "type": "OnPremisesMongoDb",
        "typeProperties":
        {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< hello IP address or host name of hello MongoDB server >",  
            "port": "<hello number of hello TCP port that hello MongoDB server uses toolisten for client connections.>",
            "username": "<username>",
            "password": "<password>",
           "authSource": "< hello database that you want toouse toocheck your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<mygateway>"
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

**Jeu de données d’entrée MongoDB :** définissant « external » : « true » informe service Data Factory de hello cette table hello est la fabrique de données externe toohello et n’est pas générée par une activité dans la fabrique de données hello.

```json
{
     "name":  "MongoDbInputDataset",
    "properties": {
        "type": "MongoDbCollection",
        "linkedServiceName": "OnPremisesMongoDbLinkedService",
        "typeProperties": {
            "collectionName": "<Collection name>"    
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
            "folderPath": "mycontainer/frommongodb/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

**Activité de copie dans un pipeline avec une source MongoDB et un récepteur d’objets blob :**

pipeline de Hello contient une activité de copie qui est hello toouse configuré au-dessus de jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures. Dans la définition JSON du pipeline hello, hello **source** type est défini trop**MongoDbSource** et **récepteur** type est défini trop**BlobSink**. la requête SQL Hello spécifiée pour hello **requête** propriété sélectionne des données de hello Bonjour au-delà de toocopy d’heure.

```json
{
    "name": "CopyMongoDBToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "MongoDbSource",
                        "query": "$$Text.Format('select * from  MyTable where LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "MongoDbInputDataset"
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
                "name": "MongoDBToAzureBlob"
            }
        ],
        "start": "2016-06-01T18:00:00Z",
        "end": "2016-06-01T19:00:00Z"
    }
}
```


## <a name="schema-by-data-factory"></a>Schéma par Data Factory
Service de fabrique de données Azure déduit le schéma à partir d’une collection de MongoDB en utilisant des documents de hello 100 dernières de collection de hello. Si ces 100 documents ne contiennent pas de schéma complet, certaines colonnes peuvent être ignorés pendant l’opération de copie hello.

## <a name="type-mapping-for-mongodb"></a>Mappage de type pour MongoDB
Comme mentionné dans hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, l’activité de copie effectue les conversions de type automatique à partir des types de sources de toosink types avec hello approche de l’étape 2 :

1. Convertir à partir de la source native types too.NET type
2. Conversion de type de récepteur de toonative de type .NET

Lorsque vous déplacez hello tooMongoDB de données suivant les mappages sont utilisés à partir des types de too.NET types MongoDB.

| Type MongoDB | Type de .NET Framework |
| --- | --- |
| Fichier binaire |Byte[] |
| Boolean |Boolean |
| Date |DateTime |
| NumberDouble |Double |
| NumberInt |Int32 |
| NumberLong |Int64 |
| ObjectID |Chaîne |
| Chaîne |Chaîne |
| UUID |Guid |
| Object |Renormalisé dans des colonnes aplaties avec « _ » comme séparateur imbriqué |

> [!NOTE]
> toolearn sur la prise en charge des tableaux à l’aide de tables virtuelles, consultez trop[prend en charge pour les types complexes à l’aide de tables virtuelles](#support-for-complex-types-using-virtual-tables) section ci-dessous.

Actuellement, hello les types de données MongoDB suivants n’est pas prises en charge : DBPointer, JavaScript, Max/Min de clé, une Expression régulière, symbole, Timestamp, non défini

## <a name="support-for-complex-types-using-virtual-tables"></a>Prise en charge des types complexes à l’aide de tables virtuelles
Azure Data Factory utilise une intégrés ODBC driver tooconnect tooand copier les données de votre base de données MongoDB. Pour les types complexes tels que les objets ou les tableaux avec des types différents dans les documents de hello, pilote de hello normalise nouveau des données dans des tables virtuelles correspondants. Plus précisément, si une table contient des colonnes de ce type, les pilotes hello génère hello tables virtuelles suivantes :

* A **table de base**, lequel contient hello les mêmes données que la table réelle de hello sauf pour les colonnes de type complexe hello. table de base Hello utilise hello même nom en tant que table réelle hello qu’elle représente.
* A **table virtuelle** pour chaque colonne de type complexe, qui étend les données de salutation imbriquée. les tables virtuelles Hello sont nommées à l’aide du nom de hello de table réelle de hello, un séparateur « _ » et un nom de hello du tableau de hello ou un objet.

Tables virtuelles font référence à des données de toohello dans la table réelle de hello, l’activation tooaccess de pilote hello hello données dénormalisées. Consultez la section Exemple ci-dessous pour plus d’informations. Vous pouvez accéder à contenu hello des tableaux de MongoDB en interrogeant et en joignant les tables virtuelles hello.

Vous pouvez utiliser hello [Assistant copie de](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) toointuitively vue hello la liste des tables de base de données MongoDB, y compris les tables virtuelles hello et afficher un aperçu des données hello à l’intérieur. Vous pouvez également créer une requête dans l’Assistant copie de hello et toosee hello résultat de la validation.

### <a name="example"></a>Exemple
Par exemple, « ExampleTable » ci-dessous est une table MongoDB qui dispose d’une colonne avec un tableau d’objets dans chaque cellule (Factures) et d’une colonne avec un tableau de types scalaires (Évaluations).

| _id | Nom du client | Factures | Niveau de service | Évaluations |
| --- | --- | --- | --- | --- |
| 1111 |ABC |[{invoice_id:”123”, item:”toaster”, price:”456”, discount:”0.2”}, {invoice_id:”124”, item:”oven”, price: ”1235”, discount: ”0.2”}] |Silver |[5,6] |
| 2222 |XYZ |[{invoice_id:”135”, item:”fridge”, price: ”12543”, discount: ”0.0”}] |Gold |[1,2] |

pilote de Hello génèrent plusieurs tables virtuelles toorepresent ce tableau. Hello première virtuel table est hello base nommé « ExampleTable », illustré ci-dessous. table de base Hello contient toutes les données de hello de table d’origine de hello, mais les données hello depuis des tableaux de hello a été omises sont développées dans les tables virtuelles hello.

| _id | Nom du client | Niveau de service |
| --- | --- | --- |
| 1111 |ABC |Silver |
| 2222 |XYZ |Gold |

Hello tableaux suivants indiquent hello tables virtuelles qui représentent les tableaux d’origine de hello dans l’exemple de hello. Ces tables contiennent les éléments suivants de hello :

* Une référence arrière toohello d’origine une colonne clé primaire toohello ligne correspondante du tableau d’origine de hello (via la colonne de _id hello)
* Une indication de position hello de données hello dans le tableau d’origine de hello
* Hello développé des données pour chaque élément dans le tableau de hello

Table « ExampleTable_Invoices » :

| _id | ExampleTable_Invoices_dim1_idx | invoice_id | item | price | Remise |
| --- | --- | --- | --- | --- | --- |
| 1111 |0 |123 |grille-pain |456 |0.2 |
| 1111 |1 |124 |four |1235 |0.2 |
| 2222 |0 |135 |réfrigérateur |12543 |0.0 |

Table « ExampleTable_Ratings » :

| _id | ExampleTable_Ratings_dim1_idx | ExampleTable_Ratings |
| --- | --- | --- |
| 1111 |0 |5 |
| 1111 |1 |6 |
| 2222 |0 |1 |
| 2222 |1 |2 |

## <a name="map-source-toosink-columns"></a>Mapper les colonnes de source toosink
toolearn sur le mappage des colonnes dans toocolumns du jeu de données source dans le jeu de données récepteur, consultez [mappage des colonnes de jeu de données dans Azure Data Factory](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Lecture renouvelée de sources relationnelles
Lors de la copie des données à partir de banques de données relationnelles, conserver la répétabilité dans l’esprit tooavoid des résultats inattendus. Dans Azure Data Factory, vous pouvez réexécuter une tranche manuellement. Vous pouvez également configurer une stratégie de nouvelles tentatives pour un jeu de données, afin qu’une tranche soit réexécutée en cas de défaillance. Lorsqu’une tranche est exécuté à nouveau dans les deux cas, vous devez toomake vraiment qui hello des mêmes données n’est en lecture aucune question comment plusieurs fois une tranche est exécutée. Voir [Lecture renouvelée de sources relationnelles](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Performances et réglage
Consultez [copie activité optimiser les performances et Guide d’optimisation](data-factory-copy-activity-performance.md) toolearn sur la clé de facteurs d’affecter les performances de transfert de données (activité de copie) dans Azure Data Factory et de différentes façons toooptimize il.

## <a name="next-steps"></a>Étapes suivantes
Consultez [déplacement des données entre locaux et cloud](data-factory-move-data-between-onprem-and-cloud.md) article pour obtenir des instructions pour la création d’un pipeline de données qui déplace la banque de données Azure tooan du magasin de données à partir de des données locales.
