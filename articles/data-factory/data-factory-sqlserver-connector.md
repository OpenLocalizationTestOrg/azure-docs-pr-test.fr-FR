---
title: "tooand de données aaaMove à partir de SQL Server | Documents Microsoft"
description: "Obtenir des informations sur comment les données de toomove vers/à partir de SQL Server de base de données qui est local ou dans une machine virtuelle de Azure à l’aide d’Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 864ece28-93b5-4309-9873-b095bbe6fedd
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jingwang
ms.openlocfilehash: f0cccf56a670e62ec893d75052a81eb26d562050
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-sql-server-on-premises-or-on-iaas-azure-vm-using-azure-data-factory"></a>Déplacer les données tooand à partir de SQL Server sur site ou sur IaaS (machine virtuelle Azure) à l’aide d’Azure Data Factory
Cet article explique comment toouse hello activité de copie de données de toomove Azure Data Factory vers/à partir d’une base de données SQL Server locale. Il repose sur hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, qui présente une vue d’ensemble du déplacement des données avec l’activité de copie hello. 

## <a name="supported-scenarios"></a>Scénarios pris en charge
Vous pouvez copier des données **à partir d’une base de données SQL Server** toohello suivant des magasins de données :

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

Vous pouvez copier des données à partir de hello suivant des magasins de données **base de données SQL Server tooa**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-sql-server-versions"></a>Versions de SQL Server prises en charge
Cette prise en charge du connecteur SQL Server copie des données à partir de / toohello suivant les versions de l’instance hébergée localement ou IaaS Azure à l’aide de l’authentification SQL et l’authentification Windows : SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008, SQL Server 2005

## <a name="enabling-connectivity"></a>Activation de la connectivité
concepts de Hello et les étapes nécessaires pour la connexion avec SQL Server hébergé localement ou dans Azure IaaS (Infrastructure-as-a-Service) VMs sont hello même. Dans les deux cas, vous devez toouse passerelle de gestion des données pour la connectivité.

Consultez [déplacement des données entre les emplacements locaux et cloud](data-factory-move-data-between-onprem-and-cloud.md) toolearn l’article sur la passerelle de gestion des données et des instructions détaillées sur la configuration de passerelle de hello. La configuration d’une instance de passerelle est pré requise pour la connexion avec SQL Server.

Pendant que vous pouvez installer la passerelle sur hello même local instance de machine virtuelle d’ordinateur ou le cloud comme hello SQL Server pour de meilleures performances, nous vous recommandons de les installer sur des ordinateurs distincts. Passerelle de hello et SQL Server sur des ordinateurs distincts réduit la contention des ressources.

## <a name="getting-started"></a>Prise en main
Vous pouvez créer un pipeline avec une activité de copie qui déplace les données vers/depuis une base de données SQL Server à l’aide de différents outils/API.

toocreate de façon plus simple Hello un pipeline est toouse hello **Assistant copie de**. Consultez [didacticiel : créer un pipeline à l’aide d’Assistant copie de](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapides sur la création d’un pipeline à l’aide d’Assistant de données de copie hello.

Vous pouvez également utiliser hello suivant outils toocreate un pipeline : **portail Azure**, **Visual Studio**, **Azure PowerShell**, **modèle Azure Resource Manager** , **API .NET**, et **API REST**. Consultez [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions toocreate un pipeline avec une activité de copie. 

Si vous utilisez hello ou une API, vous effectuez hello suivant les étapes toocreate un pipeline qui déplace la banque de données récepteur tooa du magasin de données à partir des données d’une source : 

1. Création d'une **fabrique de données**. Une fabrique de données peut contenir un ou plusieurs pipelines. 
2. Créer **services liés** fabrique de données tooyour toolink les données d’entrée et de sortie magasins. Par exemple, si vous copiez des données à partir d’un tooan de base de données SQL Server stockage d’objets blob Azure, vous créez deux services liés toolink votre base de données SQL Server et de la fabrique de données de stockage Azure compte tooyour. Pour les propriétés de service lié qui sont la base de données du serveur tooSQL spécifiques, consultez [lié des propriétés du service](#linked-service-properties) section. 
3. Créer **datasets** toorepresent d’entrée et sortie l’opération de copie des données pour hello. Dans l’exemple hello mentionné dans la dernière étape de hello, vous créez une table de dataset toospecify hello SQL dans votre base de données SQL Server qui contient les données d’entrée hello. Vous créez un autre conteneur d’objets blob dataset toospecify hello et dossier hello qui contient les données de salutation provenant de hello de base de données SQL Server. Pour les propriétés du dataset qui sont la base de données du serveur tooSQL spécifiques, consultez [propriétés du dataset](#dataset-properties) section.
4. Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie. Dans l’exemple hello mentionné précédemment, vous utilisez SqlSource en tant que source et BlobSink comme un récepteur pour l’activité de copie hello. De même, si vous copiez à partir du stockage d’objets Blob Azure tooSQL serveur de base de données, vous utilisez BlobSource et SqlSink dans l’activité de copie hello. Pour les propriétés d’activité de copie sont tooSQL spécifique de base de données de serveur, consultez [copier les propriétés de l’activité](#copy-activity-properties) section. Pour plus d’informations sur comment toouse du magasin de données source ou un récepteur, cliquez sur le lien hello dans la section précédente de hello pour votre magasin de données. 

Lorsque vous utilisez hello Assistant, les définitions de JSON pour ces entités de fabrique de données (services liés, des datasets et pipeline de hello) sont créées automatiquement pour vous. Lorsque vous utilisez/API des outils (à l’exception des API .NET), vous définissez ces entités de fabrique de données à l’aide du format JSON de hello.  Pour obtenir des exemples avec des définitions de JSON pour les entités de fabrique de données qui sont utilisés toocopy des données vers/à partir d’une base de données locale SQL Server, consultez [exemples JSON](#json-examples-for-copying-data-from-and-to-sql-server) section de cet article. 

Hello les sections suivantes fournit des détails sur les propriétés JSON qui sont utilisés toodefine Data Factory entités spécifique tooSQL Server : 

## <a name="linked-service-properties"></a>Propriétés du service lié
Vous créez un service lié de type **OnPremisesSqlServer** toolink une fabrique de données de tooa de base de données locale SQL Server. Hello tableau suivant fournit la description du service de SQL Server lié JSON éléments tooon local spécifique.

Hello tableau suivant fournit la description pour JSON éléments tooSQL spécifique service du serveur lié.

| Propriété | Description | Requis |
| --- | --- | --- |
| type |propriété de type Hello doit indiquer : **OnPremisesSqlServer**. |Oui |
| connectionString |Spécifiez les informations connectionString nécessaires de base de données SQL Server tooconnect toohello local à l’aide de l’authentification Windows ou authentification SQL. |Oui |
| gatewayName |Nom de passerelle hello hello service Data Factory doit utiliser la base de données SQL Server tooconnect toohello local. |Oui |
| username |Spécifiez le nom d’utilisateur si vous utilisez l’authentification Windows. Exemple : **domainname\\username**. |Non |
| password |Spécifiez le mot de passe de compte d’utilisateur hello que vous avez spécifié pour le nom d’utilisateur hello. |Non |

Vous pouvez chiffrer les informations d’identification à l’aide de hello **New-AzureRmDataFactoryEncryptValue** applet de commande et les utiliser dans la chaîne de connexion hello comme indiqué dans hello exemple suivant (**EncryptedCredential** propriété) :  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

### <a name="samples"></a>Exemples
**JSON pour utilisation de l’authentification SQL**

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties":
    {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
**JSON pour utilisation de l’authentification Windows**

Passerelle de gestion des données emprunte l’identité hello spécifié compte tooconnect toohello local SQL Server base de données utilisateur. 

```json
{
     "Name": " MyOnPremisesSQLDB",
     "Properties":
     {
         "type": "OnPremisesSqlServer",
         "typeProperties": {
             "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
             "username": "<domain\\username>",
             "password": "<password>",
             "gatewayName": "<gateway name>"
        }
     }
}
```

## <a name="dataset-properties"></a>Propriétés du jeu de données
Dans les exemples de hello, vous avez utilisé un jeu de données de type **SqlServerTable** toorepresent une table dans une base de données SQL Server.  

Pour obtenir une liste complète des sections et les propriétés disponibles pour définir des jeux de données, consultez hello [création de datasets](data-factory-create-datasets.md) l’article. Les sections comme la structure, la disponibilité et la stratégie d’un jeu de données JSON sont similaires pour tous les types de jeux de données (SQL Server, objet Blob Azure, table Azure, etc.).

section de typeProperties Hello est différente pour chaque type de jeu de données et fournit des informations sur l’emplacement de hello de données hello dans le magasin de données hello. Hello **typeProperties** section hello le jeu de données de type **SqlServerTable** a hello propriétés suivantes :

| Propriété | Description | Requis |
| --- | --- | --- |
| TableName |Nom de la table de hello ou la vue d’instance de base de données SQL Server hello service lié fait référence à. |Oui |

## <a name="copy-activity-properties"></a>Propriétés de l’activité de copie
Si vous déplacez des données à partir d’une base de données SQL Server, vous définissez type de source de hello dans l’activité de copie hello trop**SqlSource**. De même, si vous déplacez une base de données tooa SQL Server, vous définir le type de récepteur hello dans l’activité de copie hello trop**SqlSink**. Cette section fournit une liste de propriétés prises en charge par SqlSource et SqlSink.

Pour obtenir une liste complète des sections et les propriétés disponibles pour la définition d’activités, consultez hello [création de Pipelines](data-factory-create-pipelines.md) l’article. Les propriétés comme le nom, la description, les tables d'entrée et de sortie et les différentes stratégies sont disponibles pour tous les types d'activités.

> [!NOTE]
> Hello activité de copie accepte uniquement une entrée et produit qu’une seule sortie.

Alors que les propriétés disponibles dans la section typeProperties hello activité hello varient selon chaque type d’activité. Pour l’activité de copie, ils varient selon les types de sources et récepteurs hello.

### <a name="sqlsource"></a>SqlSource
Lorsque la source dans une activité de copie est de type **SqlSource**, hello propriétés suivantes est disponible dans **typeProperties** section :

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| SqlReaderQuery |Utiliser des données tooread hello requête personnalisée. |Chaîne de requête SQL. Par exemple : select * from MyTable. Peut faire référence à plusieurs tables de base de données hello référencé par le jeu de données d’entrée hello. Si non spécifié, hello instruction SQL exécutée : select from MyTable. |Non |
| sqlReaderStoredProcedureName |Nom de hello procédure stockée qui lit les données à partir de la table de source de hello. |Nom de hello procédure stockée. instruction SQL de la dernière Hello doit être une instruction SELECT dans la procédure stockée hello. |Non |
| storedProcedureParameters |Pourquoi les paramètres de procédure stockée. |Paires nom/valeur. Noms et la casse des paramètres doivent correspondre à des noms de hello et la casse des paramètres de la procédure stockée hello. |Non |

Si hello **sqlReaderQuery** est spécifié pour hello SqlSource, hello activité de copie s’exécute cette requête sur des données hello tooget hello base de données SQL Server source.

Ou bien, vous pouvez spécifier une procédure stockée en spécifiant hello **sqlReaderStoredProcedureName** et **storedProcedureParameters** (si hello une procédure stockée accepte des paramètres).

Si vous ne spécifiez pas de sqlReaderQuery ou sqlReaderStoredProcedureName, les colonnes de hello définis dans la section de structure hello sont utilisée toobuild un toorun requête select sur hello de base de données SQL Server. Si la définition de dataset hello n’a pas de structure de hello, toutes les colonnes sont sélectionnées à partir de la table de hello.

> [!NOTE]
> Lorsque vous utilisez **sqlReaderStoredProcedureName**, vous devez toujours toospecify une valeur pour hello **tableName** propriété dans le dataset hello JSON. Cependant, il n’existe aucune validation effectuée pour cette table.

### <a name="sqlsink"></a>SqlSink
**SqlSink** prend en charge hello propriétés suivantes :

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| writeBatchTimeout |Temps d’attente pour hello lot insert opération toocomplete avant d’expirer. |intervalle de temps<br/><br/> Exemple : « 00:30:00 » (30 minutes). |Non |
| writeBatchSize |Insère des données dans une table SQL de hello lorsque la taille de mémoire tampon de hello atteint la valeur writeBatchSize. |Nombre entier (nombre de lignes) |Non (valeur par défaut : 10000) |
| sqlWriterCleanupScript |Spécifier la requête pour l’activité de copie tooexecute telles que les données d’un secteur spécifique sont nettoyées. Pour en savoir plus, voir la section [Copie renouvelée](#repeatable-copy). |Une instruction de requête. |Non |
| sliceIdentifierColumnName |Spécifiez nom de colonne pour l’activité de copie toofill avec l’identificateur de secteur généré automatiquement, qui est utilisé tooclean des données d’un secteur spécifique quand réexécutée. Pour en savoir plus, voir la section [Copie renouvelée](#repeatable-copy). |Nom d’une colonne avec le type de données binary(32). |Non |
| sqlWriterStoredProcedureName |Nom de hello procédure stockée que les données upserts (mises à jour/insertion) dans la table cible hello. |Nom de hello procédure stockée. |Non |
| storedProcedureParameters |Pourquoi les paramètres de procédure stockée. |Paires nom/valeur. Noms et la casse des paramètres doivent correspondre à des noms de hello et la casse des paramètres de la procédure stockée hello. |Non |
| sqlWriterTableType |Spécifiez toobe de nom de type de table utilisée dans la procédure stockée hello. Activité de copie rend les données de hello déplacées disponibles dans une table temporaire avec ce type de table. Code de procédure stockée puis de fusionner des données hello copiées avec les données existantes. |Nom de type de table. |Non |


## <a name="json-examples-for-copying-data-from-and-toosql-server"></a>Exemples JSON pour copier des données à partir d’et tooSQL Server
Hello exemples suivants proposent des exemples de définitions de JSON que vous pouvez utiliser toocreate un pipeline à l’aide de [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Hello suivant exemples indiquent comment tooand de données toocopy à partir de SQL Server et le stockage d’objets Blob Azure. Toutefois, les données peuvent être copiées **directement** de n’importe quelle tooany de sources de récepteurs hello indiqué [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) à l’aide de hello activité de copie dans Azure Data Factory.     

## <a name="example-copy-data-from-sql-server-tooazure-blob"></a>Exemple : Copier des données à partir de SQL Server tooAzure Blob
Hello ci-dessous illustre d’exemple :

1. Service lié de type [OnPremisesSqlServer](#linked-service-properties).
2. Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [SqlServerTable](#dataset-properties).
4. Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Hello [pipeline](data-factory-create-pipelines.md) avec l’activité de copie qui utilise [SqlSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

exemple Hello copie des données de série chronologique à partir d’un tooan de table SQL Server Azure blob toutes les heures. propriétés JSON Hello utilisées dans ces exemples sont décrits dans les sections suivantes des exemples de hello.

Dans un premier temps, le programme d’installation passerelle de gestion des données hello. instructions de Hello sont Bonjour [déplacement des données entre les emplacements locaux et cloud](data-factory-move-data-between-onprem-and-cloud.md) l’article.

**Service SQL Server lié**
```json
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
**Service lié Azure Blob Storage**

```json
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
**Jeu de données d’entrée de SQL Server**

exemple Hello suppose que vous avez créé une table « MyTable » dans SQL Server et il contienne une colonne appelée « timestampcolumn » pour les données de série chronologique. Vous pouvez interroger sur plusieurs tables en hello même à l’aide d’un dataset unique, mais une seule table de base de données doit être utilisé pour typeProperty de tableName hello du groupe de données.

Paramètre « external » : « true » informe service Data Factory ce jeu de données hello est la fabrique de données externe toohello et n’est pas généré par une activité dans la fabrique de données hello.

```json
{
  "name": "SqlServerInput",
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
**Jeu de données de sortie d’objet Blob Azure**

Les données sont écrites tooa nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1). chemin d’accès du dossier Hello pour l’objet blob de hello est évaluée dynamiquement en fonction de l’heure de début hello de tranche hello qui est en cours de traitement. chemin d’accès du dossier Hello utilise l’année, mois, jours et heures des parties de l’heure de début hello.

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
**Pipeline avec activité de copie**

pipeline de Hello contient une activité de copie qui est configuré toouse ces jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures. Dans la définition JSON du pipeline hello, hello **source** type est défini trop**SqlSource** et **récepteur** type est défini trop**BlobSink**. la requête SQL Hello spécifiée pour hello **SqlReaderQuery** propriété sélectionne des données de hello Bonjour au-delà de toocopy d’heure.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2016-06-01T18:00:00",
    "end":"2016-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "SqlServertoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": " SqlServerInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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
Dans cet exemple, **sqlReaderQuery** est spécifié pour hello SqlSource. Hello activité de copie s’exécute cette requête par rapport aux données de base de données SQL Server source tooget hello de hello. Ou bien, vous pouvez spécifier une procédure stockée en spécifiant hello **sqlReaderStoredProcedureName** et **storedProcedureParameters** (si hello une procédure stockée accepte des paramètres). Hello sqlReaderQuery permettre faire référence à plusieurs tables de base de données hello référencé par le jeu de données d’entrée hello. Il n’est pas limité tooonly hello tableau comme hello typeProperty de tableName du jeu de données.

Si vous ne spécifiez pas sqlReaderQuery ou sqlReaderStoredProcedureName, les colonnes de hello définis dans la section de structure hello sont utilisée toobuild un toorun requête select sur hello de base de données SQL Server. Si la définition de dataset hello n’a pas de structure de hello, toutes les colonnes sont sélectionnées à partir de la table de hello.

Consultez hello [Sql Source](#sqlsource) section et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) pour la liste de propriétés prises en charge par SqlSource et BlobSink hello.

## <a name="example-copy-data-from-azure-blob-toosql-server"></a>Exemple : Copier des données d’objets Blob Azure tooSQL Server
Hello ci-dessous illustre d’exemple :

1. Hello liés de service de type [OnPremisesSqlServer](#linked-service-properties).
2. Hello liés de service de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Un [jeu de données](data-factory-create-datasets.md) d'entrée de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. un [jeu de données](data-factory-create-datasets.md) de sortie de type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties) ;
5. Hello [pipeline](data-factory-create-pipelines.md) avec l’activité de copie qui utilise [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) et [SqlSink](#sql-server-copy-activity-type-properties).

exemple Hello copie les données de séries chronologiques à partir d’une table de SQL Server tooa objets blob Azure toutes les heures. propriétés JSON Hello utilisées dans ces exemples sont décrits dans les sections suivantes des exemples de hello.

**Service SQL Server lié**

```json
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
**Service lié Azure Blob Storage**

```json
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
**Jeu de données d'entrée d'objet Blob Azure**

Les données sont récupérées à partir d'un nouvel objet Blob toutes les heures (fréquence : heure, intervalle : 1). nom de chemin d’accès et de dossier pour l’objet blob de hello Hello sont dynamiquement évaluées en fonction de l’heure de début hello de tranche hello qui est en cours de traitement. chemin d’accès du dossier Hello utilise la partie jour de l’heure de début hello, mois et année et nom de fichier partie d’heure hello de l’heure de début hello. « external » : « true » paramètre informe le service de fabrique de données de hello ce jeu de données hello est la fabrique de données externe toohello et n’est pas généré par une activité dans la fabrique de données hello.

```json
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
**Jeu de données de sortie de SQL Server**

exemple Hello copie table tooa de données nommé « MyTable » dans SQL Server. Créer la table de hello dans SQL Server avec hello même nombre de colonnes comme vous le souhaitez toocontain de fichier CSV d’objets Blob hello. Nouvelles lignes sont ajoutées à la table de toohello toutes les heures.

```json
{
  "name": "SqlServerOutput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
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
**Pipeline avec activité de copie**

pipeline de Hello contient une activité de copie qui est configuré toouse ces jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures. Dans la définition JSON du pipeline hello, hello **source** type est défini trop**BlobSource** et **récepteur** type est défini trop**SqlSink**.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQL",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": " SqlServerOutput "
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource",
            "blobColumnSeparators": ","
          },
          "sink": {
            "type": "SqlSink"
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

## <a name="troubleshooting-connection-issues"></a>Résolution des problèmes de connexion
1. Configurez vos connexions à distance de SQL Server tooaccept. Démarrez **SQL Server Management Studio**, cliquez avec le bouton droit de la souris sur **Serveur**, puis cliquez sur **Propriétés**. Sélectionnez **connexions** à partir de la liste de hello et vérification **server de toohello autoriser les connexions à distance**.

    ![Activation des connexions à distance](./media/data-factory-sqlserver-connector/AllowRemoteConnections.png)

    Consultez [configurer hello remote access Server Configuration Option](https://msdn.microsoft.com/library/ms191464.aspx) pour obtenir des instructions détaillées.
2. Lancez le **Gestionnaire de configuration SQL Server**. Développez **Configuration du réseau SQL Server** pour hello instance vous souhaitez, puis sélectionnez **protocoles pour MSSQLSERVER**. Vous devez voir des protocoles dans le volet droit hello. Activez TCP/IP en cliquant avec le bouton droit sur **TCP/IP** et en cliquant sur **Activer**.

    ![Activation de TCP/IP](./media/data-factory-sqlserver-connector/EnableTCPProptocol.png)

    Consultez la page [Activer ou désactiver un protocole réseau de serveur](https://msdn.microsoft.com/library/ms191294.aspx) pour obtenir des détails et découvrir d’autres façons d’activer le protocole TCP/IP.
3. Dans la même fenêtre de hello, double-cliquez sur **TCP/IP** toolaunch **propriétés TCP/IP** fenêtre.
4. Commutateur toohello **des adresses IP** onglet. Faites défiler vers le bas toosee **IPAll** section. Notez les hello ** le Port TCP ** (valeur par défaut est **1433**).
5. Créer un **règle pour le pare-feu Windows de hello** hello machine tooallow du trafic entrant via ce port.  
6. **Vérifiez la connexion**: tooconnect toohello SQL Server à l’aide du nom qualifié complet, utilisez SQL Server Management Studio à partir d’un autre ordinateur. Par exemple : « <machine><domain>.corp<company>.com, 1433 ».

   > [!IMPORTANT]

   > Consultez [déplacement des données entre des sources locales et cloud hello avec la passerelle de gestion des données](data-factory-move-data-between-onprem-and-cloud.md) pour plus d’informations.
   >
   > Consultez [Résolution des problèmes de passerelle](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) pour obtenir des conseils sur la résolution des problèmes de connexion/passerelle.
   >
   >


## <a name="identity-columns-in-hello-target-database"></a>Colonnes d’identité dans la base de données cible hello
Cette section fournit un exemple qui copie les données d’une table source avec aucune table de destination tooa colonne identité avec une colonne d’identité.

**Table source :**

```sql
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
**Table de destination :**

```sql
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```

Notez que la table cible hello possède une colonne d’identité.

**Définition du jeu de données JSON source**

```json
{
    "name": "SampleSource",
    "properties": {
        "published": false,
        "type": " SqlServerTable",
        "linkedServiceName": "TestIdentitySQL",
        "typeProperties": {
            "tableName": "SourceTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```
**Définition de jeu de données JSON de destination**

```json
{
    "name": "SampleTarget",
    "properties": {
        "structure": [
            { "name": "name" },
            { "name": "age" }
        ],
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "TestIdentitySQLSource",
        "typeProperties": {
            "tableName": "TargetTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }
}
```

Notez que vos tables source et cible ont des schémas différents (la cible possède une colonne supplémentaire avec identité). Dans ce scénario, vous devez toospecify **structure** propriété dans la définition du dataset cible hello, qui n’inclut pas colonne d’identité hello.

## <a name="invoke-stored-procedure-from-sql-sink"></a>Appel d’une procédure stockée pour un récepteur SQL
L’article [Appeler une procédure stockée pour un récepteur SQL dans l’activité de copie](data-factory-invoke-stored-procedure-from-copy-activity.md) illustre l’appel d’une procédure stockée à partir d’un récepteur SQL dans l’activité de copie d’un pipeline.

## <a name="type-mapping-for-sql-server"></a>Mappage de type pour SQL Server
Comme mentionné dans hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, hello activité de copie effectue les conversions de type automatique à partir de types de sources de toosink types avec hello approche de l’étape 2 :

1. Convertir à partir de la source native types too.NET type
2. Conversion de type de récepteur de toonative de type .NET

Lorsque le déplacement des données trop & à partir de SQL server, hello mappages suivants sont utilisés à partir du type too.NET de type SQL et vice versa.

mappage de Hello est identique à celui hello mappage des types de données SQL Server pour ADO.NET.

| Type de moteur de base de données SQL Server | Type de .NET Framework |
| --- | --- |
| bigint |Int64 |
| binaire |Byte[] |
| bit |Boolean |
| char |String, Char[] |
| date |DateTime |
| DateTime |DateTime |
| datetime2 |DateTime |
| Datetimeoffset |Datetimeoffset |
| Décimal |Décimal |
| Attribut FILESTREAM (varbinary(max)) |Byte[] |
| Float |Double |
| image |Byte[] |
| int |Int32 |
| money |Décimal |
| nchar |String, Char[] |
| ntext |String, Char[] |
| numérique |Décimal |
| nvarchar |String, Char[] |
| real |Single |
| rowversion |Byte[] |
| smalldatetime |DateTime |
| smallint |Int16 |
| smallmoney |Décimal |
| sql_variant |Objet * |
| texte |String, Char[] |
| time |intervalle de temps |
| timestamp |Byte[] |
| tinyint |Byte |
| uniqueidentifier |Guid |
| varbinary |Byte[] |
| varchar |String, Char[] |
| xml |xml |

## <a name="mapping-source-toosink-columns"></a>Mappage des colonnes toosink source
colonnes de toomap de toocolumns du jeu de données source à partir du jeu de données récepteur, consultez [mappage des colonnes de jeu de données dans Azure Data Factory](data-factory-map-columns.md).

## <a name="repeatable-copy"></a>Copie renouvelée
Lors de la copie des données tooSQL serveur de base de données, l’activité de copie hello ajoute la table de données toohello récepteur par défaut. tooperform UPSERT au lieu de cela, consultez [écriture Repeatable tooSqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) l’article. 

Lors de la copie des données à partir de banques de données relationnelles, conserver la répétabilité dans l’esprit tooavoid des résultats inattendus. Dans Azure Data Factory, vous pouvez réexécuter une tranche manuellement. Vous pouvez également configurer une stratégie de nouvelles tentatives pour un jeu de données, afin qu’une tranche soit réexécutée en cas de défaillance. Lorsqu’une tranche est exécuté à nouveau dans les deux cas, vous devez toomake vraiment qui hello des mêmes données n’est en lecture aucune question comment plusieurs fois une tranche est exécutée. Voir [Lecture renouvelée de sources relationnelles](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Performances et réglage
Consultez [copie activité optimiser les performances et Guide d’optimisation](data-factory-copy-activity-performance.md) toolearn sur la clé de facteurs d’affecter les performances de transfert de données (activité de copie) dans Azure Data Factory et de différentes façons toooptimize il.
