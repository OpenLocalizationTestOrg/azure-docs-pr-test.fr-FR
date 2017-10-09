---
title: "index de tooSearch aaaPush données à l’aide de Data Factory | Documents Microsoft"
description: "En savoir plus sur la façon de toopush données tooAzure Index de recherche à l’aide d’Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: f8d46e1e-5c37-4408-80fb-c54be532a4ab
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: f2d973d0a2c24d6448e2d59e37e24503aa433018
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="push-data-tooan-azure-search-index-by-using-azure-data-factory"></a>Push index Azure Search de tooan données à l’aide d’Azure Data Factory
Cet article décrit comment les données de toopush toouse hello activité de copie à partir des données sources pris en charge stocker les index de recherche tooAzure. Magasins de données source pris en charge sont répertoriés dans la colonne de Source de hello Hello [prise en charge des sources et récepteurs](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table. Cet article s’appuie sur hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, qui présente une vue d’ensemble du déplacement des données avec l’activité de copie et de combinaisons de magasin de données pris en charge.

## <a name="enabling-connectivity"></a>Activation de la connectivité
banque de données locale tooan de connexion de tooallow service Data Factory, vous installez la passerelle de gestion des données dans votre environnement local. Vous pouvez installer la passerelle sur hello même ordinateur qui héberge la source de données hello stocker ou sur un tooavoid machine distincte qui entrent en concurrence pour les ressources avec des données hello magasin.

Passerelle de gestion des données se connecte à des services de toocloud de sources de données sur site de manière sécurisée et gérée. Pour plus d’informations sur la passerelle de gestion de données, consultez l’article [Déplacement de données entre des sources locales et le cloud à l’aide de la passerelle de gestion des données](data-factory-move-data-between-onprem-and-cloud.md) .

## <a name="getting-started"></a>Prise en main
Vous pouvez créer un pipeline avec une activité de copie qui envoie des données à partir d’un index de recherche source données magasin tooAzure à l’aide de différents outils/API.

toocreate de façon plus simple Hello un pipeline est toouse hello **Assistant copie de**. Consultez [didacticiel : créer un pipeline à l’aide d’Assistant copie de](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapides sur la création d’un pipeline à l’aide d’Assistant de données de copie hello.

Vous pouvez également utiliser hello suivant outils toocreate un pipeline : **portail Azure**, **Visual Studio**, **Azure PowerShell**, **modèle Azure Resource Manager** , **API .NET**, et **API REST**. Consultez [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions toocreate un pipeline avec une activité de copie. 

Si vous utilisez hello ou une API, vous effectuez hello suivant les étapes toocreate un pipeline qui déplace la banque de données récepteur tooa du magasin de données à partir des données d’une source : 

1. Créer **services liés** fabrique de données tooyour toolink les données d’entrée et de sortie magasins.
2. Créer **datasets** toorepresent d’entrée et sortie l’opération de copie des données pour hello. 
3. Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie. 

Lorsque vous utilisez hello Assistant, les définitions de JSON pour ces entités de fabrique de données (services liés, des datasets et pipeline de hello) sont créées automatiquement pour vous. Lorsque vous utilisez/API des outils (à l’exception des API .NET), vous définissez ces entités de fabrique de données à l’aide du format JSON de hello.  Pour voir un exemple avec des définitions pour les entités de fabrique de données qui sont des index de recherche tooAzure toocopy utilisé données JSON, [exemple de JSON : copier des données à partir de l’index de recherche local SQL Server tooAzure](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index) section de cet article. 

Hello les sections suivantes fournit des détails sur les propriétés JSON qui sont utilisés toodefine Data Factory entités spécifique tooAzure Index de recherche :

## <a name="linked-service-properties"></a>Propriétés du service lié

Hello tableau suivant fournit des descriptions pour les éléments JSON toohello spécifique au service Azure Search est lié.

| Propriété | Description | Requis |
| -------- | ----------- | -------- |
| type | propriété de type Hello doit indiquer : **AzureSearch**. | Oui |
| url | URL de hello service Azure Search. | Oui |
| key | Clé d’administration pour hello service Azure Search. | Oui |

## <a name="dataset-properties"></a>Propriétés du jeu de données

Pour obtenir une liste complète des sections et les propriétés qui sont disponibles pour définir des jeux de données, consultez hello [création de datasets](data-factory-create-datasets.md) l’article. Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données. Hello **typeProperties** section est différente pour chaque type de jeu de données. Hello typeProperties section pour un jeu de données de type de hello **AzureSearchIndex** a hello propriétés suivantes :

| Propriété | Description | Requis |
| -------- | ----------- | -------- |
| type | propriété de type Hello doit être définie trop**AzureSearchIndex**.| Oui |
| indexName | Nom de l’index de recherche de Azure hello. Fabrique de données ne crée pas d’index de hello. index de Hello doit exister dans Azure Search. | Oui |


## <a name="copy-activity-properties"></a>Propriétés de l’activité de copie
Pour obtenir une liste complète des sections et des propriétés qui sont disponibles pour la définition d’activités, consultez hello [création de pipelines](data-factory-create-pipelines.md) l’article. Les propriétés comme le nom, la description, les tables d’entrée et de sortie et les différentes stratégies sont disponibles pour tous les types d’activité. Alors que les propriétés disponibles dans la section de typeProperties hello varient selon chaque type d’activité. Pour l’activité de copie, ils varient selon les types de sources et récepteurs hello.

Pour l’activité de copie, lorsque le récepteur de hello est de type de hello **AzureSearchIndexSink**, hello propriétés suivantes est disponible dans la section de typeProperties :

| Propriété | Description | Valeurs autorisées | Requis |
| -------- | ----------- | -------------- | -------- |
| WriteBehavior | Spécifie si toomerge ou remplacer un document existe déjà dans l’index de hello. Consultez hello [WriteBehavior propriété](#writebehavior-property).| Merge (par défaut)<br/>Télécharger| Non |
| writeBatchSize | Télécharge des données dans l’index de recherche de Azure hello lorsque la taille de mémoire tampon de hello atteint la valeur writeBatchSize. Consultez hello [valeur WriteBatchSize propriété](#writebatchsize-property) pour plus d’informations. | 1 too1, 000. Valeur par défaut : 1 000. | Non |

### <a name="writebehavior-property"></a>Propriété WriteBehavior
AzureSearchSink effectue une opération d’upsert lors de l’écriture des données. En d’autres termes, lorsque vous écrivez un document, si la clé de document hello existe déjà dans l’index de recherche de Azure hello, Azure Search met à jour les documents existants hello plutôt que de lever une exception de conflit.

Hello AzureSearchSink fournit hello suivant deux comportements upsert (en utilisant AzureSearch SDK) :

- **Fusion**: associent toutes les colonnes hello dans le nouveau document de hello hello une existante. Pour les colonnes avec la valeur null dans le nouveau document de hello, la valeur de hello Bonjour une existante est conservée.
- **Télécharger**: remplace de document nouveau hello hello existant. Pour les colonnes non spécifiées dans le nouveau document de hello, hello valeur toonull s’il existe une valeur non null dans un document existant de hello ou non.

comportement par défaut de Hello est **fusion**.

### <a name="writebatchsize-property"></a>Propriété WriteBatchSize
Le service Recherche Azure prend en charge l’écriture de documents sous forme d’un lot. Un lot peut contenir 1 too1, 000 Actions. Une action gère une opération de téléchargement et de fusion hello tooperform document.

### <a name="data-type-support"></a>Prise en charge des types de données
Hello tableau suivant indique si un type de données Azure Search est pris en charge ou non.

| Type de données Recherche Azure | Pris en charge dans le récepteur de l’index Recherche Azure |
| ---------------------- | ------------------------------ |
| String | O |
| Int32 | O |
| Int64 | O |
| Double | O |
| Booléen | O |
| DataTimeOffset | O |
| Tableau de chaînes | N |
| GeographyPoint | N |

## <a name="json-example-copy-data-from-on-premises-sql-server-tooazure-search-index"></a>Exemple de JSON : copier des données à partir de l’index de recherche tooAzure local SQL Server

Hello ci-dessous illustre d’exemple :

1.  Un service lié de type [AzureSearch](#linked-service-properties).
2.  Service lié de type [OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties).
3.  Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).
4.  Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureSearchIndex](#dataset-properties).
4.  Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) et [AzureSearchIndexSink](#copy-activity-properties).

exemple Hello copie toutes les heures des données de séries chronologiques à partir d’un index Azure Search tooan de base de données de SQL Server locale. les propriétés JSON Hello utilisées dans cet exemple sont décrites dans les sections suivantes des exemples de hello.

Dans un premier temps, le programme d’installation passerelle de gestion des données hello sur votre ordinateur local. instructions de Hello sont Bonjour [déplacement des données entre les emplacements locaux et cloud](data-factory-move-data-between-onprem-and-cloud.md) l’article.

**Service lié Recherche Azure :**

```JSON
{
    "name": "AzureSearchLinkedService",
    "properties": {
        "type": "AzureSearch",
        "typeProperties": {
            "url": "https://<service>.search.windows.net",
            "key": "<AdminKey>"
        }
    }
}
```

**Service SQL Server lié**

```JSON
{
  "Name": "SqlServerLinkedService",
  "properties": {
    "type": "OnPremisesSqlServer",
    "typeProperties": {
      "connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;",
      "gatewayName": "<gatewayname>"
    }
  }
}
```

**Jeu de données d’entrée de SQL Server**

exemple Hello suppose que vous avez créé une table « MyTable » dans SQL Server et il contienne une colonne appelée « timestampcolumn » pour les données de série chronologique. Vous pouvez interroger sur plusieurs tables en hello même à l’aide d’un dataset unique, mais une seule table de base de données doit être utilisé pour typeProperty de tableName hello du groupe de données.

Paramètre « external » : « true » informe service Data Factory ce jeu de données hello est la fabrique de données externe toohello et n’est pas généré par une activité dans la fabrique de données hello.

```JSON
{
  "name": "SqlServerDataset",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
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

**Jeu de données de sortie Recherche Azure :**

Hello exemple copies données tooan Azure Search index nommé **produits**. Fabrique de données ne crée pas d’index de hello. tootest hello exemple, créer un index portant ce nom. Créez l’index de recherche de Azure hello hello même nombre de colonnes dans le jeu de données d’entrée hello. Nouvelles entrées sont ajoutées à index Azure Search de toohello toutes les heures.

```JSON
{
    "name": "AzureSearchIndexDataset",
    "properties": {
        "type": "AzureSearchIndex",
        "linkedServiceName": "AzureSearchLinkedService",
        "typeProperties" : {
            "indexName": "products",
        },
        "availability": {
            "frequency": "Minute",
            "interval": 15
        }
   }
}
```

**Activité de copie dans un pipeline avec une source SQL et un récepteur de l’index Recherche Azure :**

Hello pipeline contient une activité de copie qui est configuré toouse hello des jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures. Dans la définition JSON du pipeline hello, hello **source** type est défini trop**SqlSource** et **récepteur** type est défini trop**AzureSearchIndexSink**. la requête SQL Hello spécifiée pour hello **SqlReaderQuery** propriété sélectionne des données de hello Bonjour au-delà de toocopy d’heure.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "SqlServertoAzureSearchIndex",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": " SqlServerInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSearchIndexDataset"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "AzureSearchIndexSink"
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

Si vous copiez des données d’un magasin de données cloud vers Recherche Azure, la propriété `executionLocation` est requise. Hello extrait de code JSON suivant montre les changements de hello requis dans l’activité de copie `typeProperties` comme exemple. Consultez la section [Copier des données entre des banques de données cloud](data-factory-data-movement-activities.md#global) pour plus d’informations et les valeurs prises en charge.

```JSON
"typeProperties": {
  "source": {
    "type": "BlobSource"
  },
  "sink": {
    "type": "AzureSearchIndexSink"
  },
  "executionLocation": "West US"
}
```


## <a name="copy-from-a-cloud-source"></a>Copier à partir d’une source cloud
Si vous copiez des données d’un magasin de données cloud vers Recherche Azure, la propriété `executionLocation` est requise. Hello extrait de code JSON suivant montre les changements de hello requis dans l’activité de copie `typeProperties` comme exemple. Consultez la section [Copier des données entre des banques de données cloud](data-factory-data-movement-activities.md#global) pour plus d’informations et les valeurs prises en charge.

```JSON
"typeProperties": {
  "source": {
    "type": "BlobSource"
  },
  "sink": {
    "type": "AzureSearchIndexSink"
  },
  "executionLocation": "West US"
}
```

Vous pouvez également mapper des colonnes à partir de toocolumns du jeu de données source à partir de récepteur de jeu de données dans la définition d’activité de copie de hello. Pour plus d’informations, consultez [Mappage de colonnes de jeux de données dans Azure Data Factory](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Performances et réglage  
Consultez hello [l’activité de copie guide des performances et paramétrage](data-factory-copy-activity-performance.md) toolearn sur la clé de facteurs impact sur les performances de transfert de données (activité de copie) et de différentes façons toooptimize il.

## <a name="next-steps"></a>Étapes suivantes
Consultez hello suivant des articles :

* [Didacticiel de l’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions détaillées sur la création d’un pipeline avec Activité de copie.
