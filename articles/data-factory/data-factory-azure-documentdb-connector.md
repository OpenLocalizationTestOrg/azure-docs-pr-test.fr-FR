---
title: "les données d’aaaMove vers/à partir de la base de données Azure Cosmos | Documents Microsoft"
description: "Découvrez comment déplacer des données vers et à partir de la collection Azure Cosmos DB à l’aide d’Azure Data Factory."
services: data-factory, cosmosdb
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: c9297b71-1bb4-4b29-ba3c-4cf1f5575fac
ms.service: multiple
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: bd23ce4e004a972ce6f3e4165cfdea4f0c18fecc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-cosmos-db-using-azure-data-factory"></a>Déplacer les données tooand à partir de la base de données Azure Cosmos à l’aide d’Azure Data Factory
Cet article explique comment toouse hello activité de copie de données de toomove Azure Data Factory à partir de base de données Azure Cosmos (API DocumentDB). Il repose sur hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, qui présente une vue d’ensemble du déplacement des données avec l’activité de copie hello. 

Vous pouvez copier les données de toute source pris en charge de données tooAzure Cosmos de base de données de stockage ou à partir des données de base de données Azure Cosmos tooany pris en charge récepteur stockage. Pour obtenir la liste des magasins de données pris en charge en tant que sources ou récepteurs par l’activité de copie hello, consultez hello [prise en charge des magasins de données](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table. 

> [!IMPORTANT]
> Le connecteur Azure Cosmos DB ne prend en charge que l’API DocumentDB.

données toocopy sous la forme-est vers/à partir de fichiers JSON ou une autre collection Cosmos DB, consultez [documents JSON d’importation/exportation](#importexport-json-documents).

## <a name="getting-started"></a>Prise en main
Vous pouvez créer un pipeline avec une activité de copie qui déplace les données vers ou à partir d’Azure Cosmos DB à l’aide de différents outils et API.

toocreate de façon plus simple Hello un pipeline est toouse hello **Assistant copie de**. Consultez [didacticiel : créer un pipeline à l’aide d’Assistant copie de](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapides sur la création d’un pipeline à l’aide d’Assistant de données de copie hello.

Vous pouvez également utiliser hello suivant outils toocreate un pipeline : **portail Azure**, **Visual Studio**, **Azure PowerShell**, **modèle Azure Resource Manager** , **API .NET**, et **API REST**. Consultez [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions toocreate un pipeline avec une activité de copie. 

Si vous utilisez hello ou une API, vous effectuez hello suivant les étapes toocreate un pipeline qui déplace la banque de données récepteur tooa du magasin de données à partir des données d’une source : 

1. Créer **services liés** fabrique de données tooyour toolink les données d’entrée et de sortie magasins.
2. Créer **datasets** toorepresent d’entrée et sortie l’opération de copie des données pour hello. 
3. Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie. 

Lorsque vous utilisez hello Assistant, les définitions de JSON pour ces entités de fabrique de données (services liés, des datasets et pipeline de hello) sont créées automatiquement pour vous. Lorsque vous utilisez/API des outils (à l’exception des API .NET), vous définissez ces entités de fabrique de données à l’aide du format JSON de hello.  Pour obtenir des exemples avec des définitions pour les entités de fabrique de données qui sont utilisées toocopy des données vers/à partir de la base de données Cosmos JSON, consultez [exemples JSON](#json-examples) section de cet article. 

Hello les sections suivantes fournit des détails sur les propriétés JSON qui sont utilisés toodefine Data Factory entités spécifiques tooCosmos DB : 

## <a name="linked-service-properties"></a>Propriétés du service lié
Hello tableau suivant fournit la description pour JSON éléments tooAzure spécifique service DB Cosmos lié.

| **Propriété** | **Description** | **Obligatoire** |
| --- | --- | --- |
| type |propriété de type Hello doit indiquer : **DocumentDb** |Oui |
| connectionString |Spécifiez les informations nécessaires de base de données de base de données Cosmos tooconnect tooAzure. |Oui |

Exemple :

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```

## <a name="dataset-properties"></a>Propriétés du jeu de données
Pour une liste complète des sections et les propriétés disponibles pour définir des jeux de données, consultez toohello [création de datasets](data-factory-create-datasets.md) l’article. Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données (SQL Azure, Azure Blob, Azure Table, etc.).

section de typeProperties Hello est différente pour chaque type de jeu de données et fournit des informations sur l’emplacement de hello de données hello dans le magasin de données hello. section hello le jeu de données de type Hello typeProperties **DocumentDbCollection** a les propriétés suivantes de hello.

| **Propriété** | **Description** | **Obligatoire** |
| --- | --- | --- |
| collectionName |Nom de collection de documents de base de données Cosmos de hello. |Oui |

Exemple :

```JSON
{
  "name": "PersonCosmosDbTable",
  "properties": {
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
### <a name="schema-by-data-factory"></a>Schéma par Data Factory
Pour les magasins de données sans schéma comme base de données Azure Cosmos, hello service Data Factory déduit le schéma de hello dans un des hello suivant façons :  

1. Si vous spécifiez la structure hello des données à l’aide de hello **structure** propriété dans la définition de dataset hello, hello service Data Factory respecte cette structure en tant que schéma de hello. Dans ce cas, si une ligne ne contient pas de valeur pour une colonne, une valeur null est fournie pour celle-ci.
2. Si vous ne spécifiez pas de structure hello des données à l’aide de hello **structure** propriété dans la définition de dataset hello, hello service Data Factory déduit le schéma de hello à l’aide de la première ligne de hello dans les données de salutation. Dans ce cas, si la première ligne de hello ne contient pas de schéma complet de hello, certaines colonnes sera manquants dans le résultat de hello d’opération de copie.

Par conséquent, pour les sources de données de schéma, il est recommandé de hello est toospecify hello structure de données à l’aide de hello **structure** propriété.

## <a name="copy-activity-properties"></a>Propriétés de l’activité de copie
Pour une liste complète des sections et les propriétés disponibles pour la définition d’activités, consultez toohello [création de Pipelines](data-factory-create-pipelines.md) l’article. Les propriétés comme le nom, la description, les tables d’entrée et de sortie et la stratégie sont disponibles pour tous les types d’activités.

> [!NOTE]
> Hello activité de copie accepte uniquement une entrée et produit qu’une seule sortie.

Propriétés disponibles dans la section de typeProperties hello d’activité hello sur hello autre part varie avec chaque type d’activité et en cas d’activité de copie ils varient selon les types de sources et récepteurs hello.

En cas d’activité de copie lors de la source est de type **DocumentDbCollectionSource** hello propriétés suivantes est disponible dans **typeProperties** section :

| **Propriété** | **Description** | **Valeurs autorisées** | **Obligatoire** |
| --- | --- | --- | --- |
| query |Spécifier les données de tooread requête hello. |Chaîne de requête prise en charge par Azure Cosmos DB. <br/><br/>Exemple : `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"` |Non <br/><br/>Si ce n’est pas spécifié, hello instruction SQL exécutée :`select <columns defined in structure> from mycollection` |
| nestingSeparator |Tooindicate caractère spécial qui hello document est imbriquée. |Tout caractère. <br/><br/>Azure Cosmos DB est une banque NoSQL de documents JSON, où les structures imbriquées sont autorisées. Azure Data Factory permet de hiérarchie de toodenote utilisateur via nestingSeparator, qui est «. » Bonjour exemples ci-dessus. Avec séparateur de hello, activité de copie hello génère un objet de « Name » hello avec des éléments de trois enfants too"Name.First première, intermédiaire et dernière, en fonction », « Name.Middle » et « Name.Last « Bonjour de définition de table. |Non |

**DocumentDbCollectionSink** prend en charge hello propriétés suivantes :

| **Propriété** | **Description** | **Valeurs autorisées** | **Obligatoire** |
| --- | --- | --- | --- |
| nestingSeparator |Un caractère spécial dans tooindicate de nom hello source colonne imbriquées de document est nécessaire. <br/><br/>Par exemple ci-dessus : `Name.First` dans la sortie de hello table génère hello suivant structure JSON dans le document de base de données Cosmos hello :<br/><br/>"Name": {<br/>    "First": "John"<br/>}, |Caractère utilisé tooseparate des niveaux d’imbrication.<br/><br/>La valeur par défaut est `.` (point). |Caractère utilisé tooseparate des niveaux d’imbrication. <br/><br/>La valeur par défaut est `.` (point). |
| writeBatchSize |Nombre de parallèle demandes documents toocreate de service de base de données Cosmos tooAzure.<br/><br/>Vous pouvez affiner les performances des hello lors de la copie des données à partir de Cosmos DB à l’aide de cette propriété. Vous pouvez vous attendre de meilleures performances lorsque vous augmentez la valeur writeBatchSize, car plusieurs demandes parallèles tooCosmos base de données sont envoyés. Toutefois, vous devez tooavoid la limitation peut lever de message d’erreur hello : « Requête taux est grand ».<br/><br/>Une limitation dépend de divers facteurs, dont la taille des documents, le nombre de termes qu’ils contiennent, la stratégie d’indexation de la collection cible, etc. Pour les opérations de copie, vous pouvez utiliser la plupart des débit disponible à une meilleure hello de toohave de collection (par exemple, S3) (2 500 demande unités par seconde). |Entier  |Non (valeur par défaut : 5) |
| writeBatchTimeout |Temps d’attente pour hello opération toocomplete avant d’expirer. |intervalle de temps<br/><br/> Exemple : « 00:30:00 » (30 minutes). |Non |

## <a name="importexport-json-documents"></a>Importation/exportation de documents JSON
À l’aide de ce connecteur Cosmos DB, vous pouvez facilement :

* Importer des documents JSON de différentes sources dans Cosmos DB, notamment le Stockage Blob Azure, Azure Data Lake, un système de fichiers local ou d’autres banques basées sur des fichiers prises en charge par Azure Data Factory.
* Exporter des documents JSON d’une collection Cosmos DB vers différentes banques basées sur des fichiers.
* Migrer des données entre deux collections Cosmos DB en l’état.

tooachieve ce schéma indépendant de la copier, 
* Lorsque vous utilisez l’Assistant copie de, vérifiez hello **« exporter en tant que-est tooJSON fichiers ou une collection de Cosmos DB »** option.
* Lorsque, à l’aide de la modification de JSON, ne spécifiez pas de section « structure » de hello dans les jeux de données de base de données Cosmos ni propriété « nestingSeparator » sur la base de données Cosmos source/récepteur dans l’activité de copie. tooimport à partir de / tooJSON fichiers d’exportation, hello fichier magasin DataSet spécifier le type de format comme « JsonFormat », « filePattern » de configuration et ignorer les paramètres de format hello rest, consultez [format JSON](data-factory-supported-file-and-compression-formats.md#json-format) section de détails.

## <a name="json-examples"></a>Exemples JSON
Hello exemples suivants proposent des exemples de définitions de JSON que vous pouvez utiliser toocreate un pipeline à l’aide de [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Elles montrent comment tooand de données toocopy à partir de la base de données Azure Cosmos et de stockage d’objets Blob Azure. Toutefois, les données peuvent être copiées **directement** de n’importe quelle tooany de sources hello de récepteurs hello indiqué [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) à l’aide de hello activité de copie dans Azure Data Factory.

## <a name="example-copy-data-from-azure-cosmos-db-tooazure-blob"></a>Exemple : Copier des données à partir de la base de données Azure Cosmos tooAzure Blob
exemple Hello ci-dessous montre :

1. Un service lié de type [DocumentDb](#linked-service-properties).
2. Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [DocumentDbCollection](#dataset-properties).
4. Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [DocumentDbCollectionSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

exemple Hello copie des données dans la base de données Azure Cosmos tooAzure Blob. propriétés JSON Hello utilisées dans ces exemples sont décrits dans les sections suivantes des exemples de hello.

**Service lié Azure Cosmos DB :**

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
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
**Jeu de données d'entrée Document DB Azure :**

exemple Hello suppose que vous avez une collection nommée **personne** dans une base de données de la base de données Azure Cosmos.

Paramètre « external » : « true » et spécifiant externalData les informations de stratégie hello Azure Data Factory du service table hello est fabrique de données externe toohello pas produit par une activité dans la fabrique de données hello.

```JSON
{
  "name": "PersonCosmosDbTable",
  "properties": {
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

**Jeu de données de sortie Azure Blob :**

Les données sont copiées tooa nouvel objet blob toutes les heures avec un chemin d’accès hello blob hello reflétant hello la date/heure spécifique avec une granularité de l’heure.

```JSON
{
  "name": "PersonBlobTableOut",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "docdb",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "nullValue": "NULL"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
Exemple de document JSON Bonjour collection personne dans une base de données de la base de données Cosmos :

```JSON
{
  "PersonId": 2,
  "Name": {
    "First": "Jane",
    "Middle": "",
    "Last": "Doe"
  }
}
```
Cosmos DB prend en charge l'interrogation de documents à l'aide d'une syntaxe de type SQL sur des documents JSON hiérarchiques.

Exemple : 

```sql
SELECT Person.PersonId, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person
```

copie des données à partir de hello collection personne Bonjour tooan de base de données de base de données Azure Cosmos blob Azure de pipeline suivants de Hello. Dans le cadre de hello d’activité hello copie les jeux de données d’entrée et de sortie ont été spécifiés.  

```JSON
{
  "name": "DocDbToBlobPipeline",
  "properties": {
    "activities": [
      {
        "type": "Copy",
        "typeProperties": {
          "source": {
            "type": "DocumentDbCollectionSource",
            "query": "SELECT Person.Id, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person",
            "nestingSeparator": "."
          },
          "sink": {
            "type": "BlobSink",
            "blobWriterAddHeader": true,
            "writeBatchSize": 1000,
            "writeBatchTimeout": "00:00:59"
          }
        },
        "inputs": [
          {
            "name": "PersonCosmosDbTable"
          }
        ],
        "outputs": [
          {
            "name": "PersonBlobTableOut"
          }
        ],
        "policy": {
          "concurrency": 1
        },
        "name": "CopyFromDocDbToBlob"
      }
    ],
    "start": "2015-04-01T00:00:00Z",
    "end": "2015-04-02T00:00:00Z"
  }
}
```
## <a name="example-copy-data-from-azure-blob-tooazure-cosmos-db"></a>Exemple : Copier des données d’objets Blob Azure tooAzure Cosmos DB 
exemple Hello ci-dessous montre :

1. Un service lié de type [DocumentDb](#azure-documentdb-linked-service-properties).
2. Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. un [jeu de données](data-factory-create-datasets.md) d'entrée de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. Un [jeu de données](data-factory-create-datasets.md) de sortie de type [DocumentDbCollection](#azure-documentdb-dataset-type-properties).
5. Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) et [DocumentDbCollectionSink](#azure-documentdb-copy-activity-type-properties).

exemple Hello copie les données d’objets blob Azure tooAzure Cosmos DB. propriétés JSON Hello utilisées dans ces exemples sont décrits dans les sections suivantes des exemples de hello.

**Service lié Azure Blob Storage :**

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
**Service lié Azure Cosmos DB :**

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```
**Jeu de données d'entrée d'objet Blob Azure :**

```JSON
{
  "name": "PersonBlobTableIn",
  "properties": {
    "structure": [
      {
        "name": "Id",
        "type": "Int"
      },
      {
        "name": "FirstName",
        "type": "String"
      },
      {
        "name": "MiddleName",
        "type": "String"
      },
      {
        "name": "LastName",
        "type": "String"
      }
    ],
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "fileName": "input.csv",
      "folderPath": "docdb",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "nullValue": "NULL"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
**Jeu de données de sortie Azure Cosmos DB :**

exemple Hello copie la collection de tooa de données nommée « Person ».

```JSON
{
  "name": "PersonCosmosDbTableOut",
  "properties": {
    "structure": [
      {
        "name": "Id",
        "type": "Int"
      },
      {
        "name": "Name.First",
        "type": "String"
      },
      {
        "name": "Name.Middle",
        "type": "String"
      },
      {
        "name": "Name.Last",
        "type": "String"
      }
    ],
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
copie des données d’objets Blob Azure toohello collection personne Bonjour Cosmos DB de pipeline suivants de Hello. Dans le cadre de hello d’activité hello copie les jeux de données d’entrée et de sortie ont été spécifiés.

```JSON
{
  "name": "BlobToDocDbPipeline",
  "properties": {
    "activities": [
      {
        "type": "Copy",
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "DocumentDbCollectionSink",
            "nestingSeparator": ".",
            "writeBatchSize": 2,
            "writeBatchTimeout": "00:00:00"
          }
          "translator": {
              "type": "TabularTranslator",
              "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, title: aaaTitle, Suffix: Suffix, EmailPromotion: EmailPromotion, rowguid: rowguid, ModifiedDate: ModifiedDate"
          }
        },
        "inputs": [
          {
            "name": "PersonBlobTableIn"
          }
        ],
        "outputs": [
          {
            "name": "PersonCosmosDbTableOut"
          }
        ],
        "policy": {
          "concurrency": 1
        },
        "name": "CopyFromBlobToDocDb"
      }
    ],
    "start": "2015-04-14T00:00:00Z",
    "end": "2015-04-15T00:00:00Z"
  }
}
```
Si l’exemple hello d’objets blob entrée est comme

```
1,John,,Doe
```
Puis hello sortie JSON dans la base de données Cosmos sera en tant que :

```JSON
{
  "Id": 1,
  "Name": {
    "First": "John",
    "Middle": null,
    "Last": "Doe"
  },
  "id": "a5e8595c-62ec-4554-a118-3940f4ff70b6"
}
```
Azure Cosmos DB est une banque NoSQL de documents JSON, où les structures imbriquées sont autorisées. Azure Data Factory permet de hiérarchie de toodenote utilisateur via **nestingSeparator**, qui est «. » » dans cet exemple. Avec séparateur de hello, activité de copie hello génère un objet de « Name » hello avec des éléments de trois enfants too"Name.First première, intermédiaire et dernière, en fonction », « Name.Middle » et « Name.Last « Bonjour de définition de table.

## <a name="appendix"></a>Annexe
1. **Question :** hello mise à jour de la prise en charge de l’activité de copie des enregistrements existants ?

    **Réponse :** non.
2. **Question :** comment fait une nouvelle tentative d’un contrat de base de données Cosmos copie tooAzure avec déjà copié les enregistrements ?

    **Réponse :** si les enregistrements ont un champ « ID » et l’opération de copie hello tente tooinsert un enregistrement avec hello même ID, l’opération de copie hello génère une erreur.  
3. **Question :** Data Factory prend-il en charge le [partitionnement de données basé sur un intervalle ou sur le hachage](../documentdb/documentdb-partition-data.md) ?

    **Réponse :** non.
4. **Question :** puis-je indiquer plusieurs collections Azure Cosmos DB pour une table ?

    **Réponse :** non. Il n’est possible d’indiquer qu’une collection pour le moment.

## <a name="performance-and-tuning"></a>Performances et réglage
Consultez [copie activité optimiser les performances et Guide d’optimisation](data-factory-copy-activity-performance.md) toolearn sur la clé de facteurs d’affecter les performances de transfert de données (activité de copie) dans Azure Data Factory et de différentes façons toooptimize il.
