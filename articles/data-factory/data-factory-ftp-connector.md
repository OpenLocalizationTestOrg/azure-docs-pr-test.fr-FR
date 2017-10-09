---
title: "aaaMove des données à partir d’un serveur FTP à l’aide d’Azure Data Factory | Documents Microsoft"
description: "En savoir plus sur la façon de toomove les données à partir d’un serveur FTP à l’aide d’Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: eea3bab0-a6e4-4045-ad44-9ce06229c718
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: jingwang
ms.openlocfilehash: c707e29532b2a8a870603948cb6150ab857bd6ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-ftp-server-by-using-azure-data-factory"></a>Déplacer des données à partir d’un serveur FTP à l’aide d’Azure Data Factory
Cet article explique comment toouse hello activité de copie de données de toomove Azure Data Factory à partir d’un serveur FTP. Il repose sur hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, qui présente une vue d’ensemble du déplacement des données avec l’activité de copie hello.

Vous pouvez copier des données à partir d’un magasin de données de récepteur FTP server tooany pris en charge. Pour une liste de données pris en charge des magasins récepteurs par l’activité de copie hello, consultez hello [prise en charge des magasins de données](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table. Fabrique de données prend en charge seulement stocke de déplacement des données d’un FTP server tooother de données, mais ne pas déplacer les données à partir d’autres données stocke tooan FTP server. Il prend en charge à la fois les serveurs FTP locaux et cloud.

> [!NOTE]
> activité de copie Hello ne supprime pas le fichier de source de hello lorsqu’elle est correctement copié toohello destination. Si vous avez besoin de fichier de source de hello toodelete après la copie a réussi, créer un fichier de hello toodelete activité personnalisée et utiliser l’activité hello dans le pipeline de hello. 

## <a name="enable-connectivity"></a>Activez la connectivité.
Si vous déplacez des données d’une **local** magasin de données cloud FTP server tooa (par exemple, tooAzure stockage d’objets Blob), installer et utiliser la passerelle de gestion des données. Hello passerelle de gestion des données est un agent de client qui est installé sur votre ordinateur local et il permet de ressources de cloud services tooconnect tooan local. Pour plus de détails, voir [Passerelle de gestion des données](data-factory-data-management-gateway.md). Pour obtenir des instructions sur la configuration de passerelle de hello et l’utiliser, consultez [déplacement des données entre les emplacements locaux et cloud](data-factory-move-data-between-onprem-and-cloud.md). Vous utilisez server de hello passerelle tooconnect tooan FTP, même si le serveur de hello est sur une infrastructure Windows Azure en tant que service (IaaS) virtual machine (VM).

Il s’agit de passerelle de hello tooinstall possibles sur hello même local machine ou IaaS VM comme hello du serveur FTP. Toutefois, nous vous recommandons d’installer hello passerelle sur un ordinateur distinct ou un conflit de ressources IaaS VM tooavoid et pour de meilleures performances. Lorsque vous installez la passerelle de hello sur un ordinateur distinct, machine de hello doit être le serveur FTP de hello tooaccess en mesure de.

## <a name="get-started"></a>Prise en main
Vous pouvez créer un pipeline avec une activité de copie qui déplace les données d’une source FTP à l’aide de différents outils ou API.

toocreate de façon plus simple Hello un pipeline est toouse hello **Assistant copie de fabrique de données**. Pour obtenir une procédure rapide, consultez l’article [Didacticiel : Créer un pipeline avec l’activité de copie à l’aide de l’Assistant Data Factory Copy](data-factory-copy-data-wizard-tutorial.md).

Vous pouvez également utiliser hello suivant outils toocreate un pipeline : **portail Azure**, **Visual Studio**, **PowerShell**, **le modèle Azure Resource Manager**, **API .NET**, et **API REST**. Consultez [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions toocreate un pipeline avec une activité de copie.

Si vous utilisez des API ou des outils de hello, procédez hello suivant les étapes toocreate un pipeline qui déplace la banque de données récepteur tooa du magasin de données à partir des données sources :

1. Créer **services liés** fabrique de données tooyour toolink les données d’entrée et de sortie magasins.
2. Créer **datasets** toorepresent d’entrée et sortie l’opération de copie des données pour hello.
3. Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.

Lorsque vous utilisez hello Assistant, les définitions de JSON pour ces entités de fabrique de données (services liés, des datasets et pipeline de hello) sont créées automatiquement pour vous. Lorsque vous utilisez des outils ou des API (à l’exception des API .NET), vous définissez ces entités de fabrique de données à l’aide du format JSON de hello. Pour voir un exemple avec des définitions de JSON pour les entités de fabrique de données qui sont utilisées toocopy des données à partir d’une banque de données FTP, hello [exemple de JSON : copier des données d’objet blob tooAzure de serveur FTP](#json-example-copy-data-from-ftp-server-to-azure-blob) section de cet article.

> [!NOTE]
> Pour plus d’informations sur la prise en charge toouse de formats de compression des fichiers et, consultez [des formats de fichiers et de compression dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md).

Hello les sections suivantes fournit des détails sur les propriétés JSON qui sont utilisés toodefine Data Factory entités spécifique tooFTP.

## <a name="linked-service-properties"></a>Propriétés du service lié
Hello tableau suivant décrit les service FTP lié de JSON éléments tooan spécifique.

| Propriété | Description | Requis | Default |
| --- | --- | --- | --- |
| type |Définissez cette tooFtpServer. |Oui |&nbsp; |
| host |Spécifiez le nom de hello ou adresse IP du serveur FTP de hello. |Oui |&nbsp; |
| authenticationType |Spécifiez le type d’authentification hello. |Oui |Basic, anonyme |
| username |Spécifier hello utilisateur a accès toohello FTP serveur. |Non |&nbsp; |
| password |Spécifiez le mot de passe hello pour hello (nom d’utilisateur). |Non |&nbsp; |
| Encryptedcredential |Spécifiez hello crypté d’informations d’identification tooaccess hello FTP serveur. |Non |&nbsp; |
| gatewayName |Spécifier le nom hello de passerelle de hello dans le serveur de passerelle de gestion des données tooconnect tooan sur site FTP. |Non |&nbsp; |
| port |Spécifier le port hello sur quel hello FTP serveur écoute. |Non |21 |
| enableSsl |Spécifiez si toouse FTP sur un canal SSL/TLS. |Non |true |
| enableServerCertificateValidation |Spécifiez si le serveur tooenable SSL la validation des certificats lorsque vous utilisez FTP sur un canal SSL/TLS. |Non |true |

### <a name="use-anonymous-authentication"></a>Utiliser une authentification anonyme

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {        
            "authenticationType": "Anonymous",
              "host": "myftpserver.com"
        }
    }
}
```

### <a name="use-username-and-password-in-plain-text-for-basic-authentication"></a>Utiliser un nom d’utilisateur et d’un mot de passe en texte brut pour l’authentification de base

```JSON
{
    "name": "FTPLinkedService",
      "properties": {
    "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "username": "Admin",
            "password": "123456"
        }
      }
}
```

### <a name="use-port-enablessl-enableservercertificatevalidation"></a>Utiliser un port, enableSsl, enableServerCertificateValidation

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",    
            "username": "Admin",
            "password": "123456",
            "port": "21",
            "enableSsl": true,
            "enableServerCertificateValidation": true
        }
    }
}
```

### <a name="use-encryptedcredential-for-authentication-and-gateway"></a>Utiliser encryptedCredential pour l’authentification et la passerelle

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "gatewayName": "mygateway"
        }
      }
}
```

## <a name="dataset-properties"></a>Propriétés du jeu de données
Pour obtenir la liste complète des sections et propriétés disponibles pour la définition de jeux de données, voir [Création de jeux de données](data-factory-create-datasets.md). Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données.

Hello **typeProperties** section est différente pour chaque type de jeu de données. Il fournit des informations qui sont le type de jeu de données toohello spécifique. Hello **typeProperties** section pour un jeu de données de type **le partage de fichiers** a hello propriétés suivantes :

| Propriété | Description | Requis |
| --- | --- | --- |
| folderPath |Dossier de toohello sous-chemin. Utilisez le caractère d’échappement ' \ ' pour les caractères spéciaux dans la chaîne de hello. Consultez la section [Exemples de définitions de jeux de données et de service liés](#sample-linked-service-and-dataset-definitions) pour obtenir des exemples.<br/><br/>Vous pouvez combiner cette propriété avec **partitionBy** toohave chemins d’accès basés sur un secteur de démarrage et date-heure de fin. |Oui |
| fileName |Spécifiez le nom hello du fichier de hello Bonjour **folderPath** si vous souhaitez hello table toorefer tooa fichier spécifique dans le dossier de hello. Si vous ne spécifiez pas de valeur pour cette propriété, la table de hello pointe tooall des fichiers dans le dossier de hello.<br/><br/>Lorsque **nom de fichier** n’est pas spécifié pour un dataset de sortie, hello nom hello généré est Bonjour suivant le format : <br/><br/>Data<Guid>.txt (exemple : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt) |Non |
| fileFilter |Spécifiez un tooselect de toobe utilisé filtre un sous-ensemble de fichiers Bonjour **folderPath**, plutôt que tous les fichiers.<br/><br/>Les valeurs autorisées sont : `*` (plusieurs caractères) et `?` (caractère unique).<br/><br/>Exemple 1 : `"fileFilter": "*.log"`<br/>Exemple 2 : `"fileFilter": 2014-1-?.txt"`<br/><br/> **fileFilter** s’applique à un jeu de données FileShare d’entrée. Cette propriété n’est pas pris en charge avec le Système de fichiers DFS Hadoop (HDFS). |Non |
| partitionedBy |Utilisé toospecify dynamiques **folderPath** et **nom de fichier** pour les données de série chronologique. Par exemple, vous pouvez spécifier un **folderPath** paramétré pour chaque heure de données. |Non |
| format | Hello, les types de format suivants est pris en charge : **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Ensemble hello **type** propriété sous tooone de format de ces valeurs. Pour plus d’informations, consultez hello [au Format texte](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [le Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), et [Parquet Format ](data-factory-supported-file-and-compression-formats.md#parquet-format) sections. <br><br> Si vous souhaitez que les fichiers toocopy lorsqu’ils sont entre des magasins basée sur le fichier (copie binaire), ignorer la section de format hello dans les deux définitions de jeu de données d’entrée et de sortie. |Non |
| compression | Spécifiez le type de hello et le niveau de compression pour les données de salutation. Les types pris en charge sont **GZip**, **Deflate**, **BZip2** et **ZipDeflate**. Les niveaux pris en charge sont **Optimal** et **Fastest**. Pour plus d’informations, consultez [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |Non |
| useBinaryTransfer |Spécifiez si le mode de transfert binaire de hello toouse. les valeurs Hello sont remplies pour le mode binaire (il s’agit de valeur par défaut de hello) et false pour ASCII. Cette propriété peut uniquement être utilisée lorsque hello service lié associé est du type : détails. |Non |

> [!NOTE]
> **fileName** et **fileFilter** ne peuvent pas être utilisés simultanément.

### <a name="use-hello-partionedby-property"></a>Utilisez la propriété partionedBy de hello
Comme indiqué dans la section précédente de hello, vous pouvez spécifier un dynamique **folderPath** et **nom de fichier** pour les données de série chronologique par hello **partitionedBy** propriété.

toolearn sur la série de temps des groupes de données, de planification et de secteurs, consultez [création de datasets](data-factory-create-datasets.md), [de planification et de l’exécution](data-factory-scheduling-and-execution.md), et [création de pipelines](data-factory-create-pipelines.md).

#### <a name="sample-1"></a>Exemple 1

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
Dans cet exemple, {Slice} est remplacé par la valeur hello de variable de système de Data Factory SliceStart, Bonjour format (AAAAMMJJHH) spécifié. Hello SliceStart fait référence à des temps de toostart de tranche de hello. chemin d’accès du dossier Hello est différent pour chaque secteur. (par exemple : wikidatagateway/wikisampledataout/2014100103 ou wikidatagateway/wikisampledataout/2014100104).

#### <a name="sample-2"></a>Exemple 2

```json
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```
Dans cet exemple, hello année, mois, jour et l’heure de SliceStart sont extraits dans des variables distinctes qui sont utilisés par hello **folderPath** et **nom de fichier** propriétés.

## <a name="copy-activity-properties"></a>Propriétés de l’activité de copie
Pour obtenir la liste complète des sections et propriétés disponibles pour la définition des activités, voir [Création de pipelines](data-factory-create-pipelines.md). Les propriétés comme le nom, la description, les tables d'entrée et de sortie et les différentes stratégies sont disponibles pour tous les types d'activités.

Propriétés disponibles dans hello **typeProperties** section de hello activité, hello autre part, varie avec chaque type d’activité. Pour l’activité de copie hello, les propriétés de type hello varient selon les types de sources et récepteurs hello.

Dans l’activité de copie, lors de la source de hello est de type **FileSystemSource**, hello suivant la propriété est disponible dans **typeProperties** section :

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| recursive |Indique si les données de salutation sont lu de manière récursive des sous-dossiers de hello ou uniquement dans le dossier spécifié de hello. |True, False (par défaut) |Non |

## <a name="json-example-copy-data-from-ftp-server-tooazure-blob"></a>Exemple de JSON : copier des données à partir de FTP server tooAzure Blob
Cet exemple montre comment toocopy des données à partir d’un tooAzure de serveur FTP stockage d’objets Blob. Toutefois, les données peuvent être copiées directement tooany Hello récepteurs hello est indiqué dans [prise en charge des magasins de données et les formats](data-factory-data-movement-activities.md#supported-data-stores-and-formats), à l’aide de l’activité de copie hello dans la fabrique de données.  

Hello exemples suivants proposent des exemples de définitions de JSON que vous pouvez utiliser toocreate un pipeline à l’aide de [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), ou [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md):

* Un service lié de type [FtpServer](#linked-service-properties).
* Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
* Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [FileShare](#dataset-properties)
* Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)
* Un [pipeline](data-factory-create-pipelines.md) avec activité de copie qui utilise [FileSystemSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)

exemple Hello copie des données à partir d’un tooan de serveur FTP blob Azure toutes les heures. propriétés JSON Hello utilisées dans ces exemples sont décrits dans les sections suivantes des exemples de hello.

### <a name="ftp-linked-service"></a>Service lié FTP

Cet exemple utilise l’authentification de base, hello nom d’utilisateur et mot de passe en texte brut. Vous pouvez également utiliser un des hello suivant façons :

* Authentification anonyme
* Authentification de base avec des informations d’identification chiffrées
* FTP sur SSL/TLS (FTPS)

Consultez hello [service lié de FTP](#linked-service-properties) section pour différents types d’authentification que vous pouvez utiliser.

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
    "type": "FtpServer",
    "typeProperties": {
        "host": "myftpserver.com",           
        "authenticationType": "Basic",
        "username": "Admin",
        "password": "123456"
    }
  }
}
```
### <a name="azure-storage-linked-service"></a>Service lié Azure Storage

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
### <a name="ftp-input-dataset"></a>Jeu de données d’entrée FTP

Ce jeu de données fait référence toohello FTP dossier `mysharedfolder` et le fichier `test.csv`. Hello pipeline copies hello toohello destination du fichier.

Paramètre **externe** trop**true** informe le service de fabrique de données hello ce jeu de données hello est la fabrique de données externe toohello et n’est pas généré par une activité dans la fabrique de données hello.

```JSON
{
  "name": "FTPFileInput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": "FTPLinkedService",
    "typeProperties": {
      "folderPath": "mysharedfolder",
      "fileName": "test.csv",
      "useBinaryTransfer": true
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

### <a name="azure-blob-output-dataset"></a>Jeu de données de sortie d’objet Blob Azure

Les données sont écrites tooa nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1). chemin d’accès du dossier Hello pour l’objet blob de hello est évaluée dynamiquement, en fonction de l’heure de début hello de tranche hello qui est en cours de traitement. chemin d’accès du dossier Hello utilise hello des parties d’année, mois, jours et heures de l’heure de début hello.

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/ftp/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="a-copy-activity-in-a-pipeline-with-file-system-source-and-blob-sink"></a>Activité de copie dans un pipeline avec une source Système de fichiers et un récepteur blob

Hello pipeline contient une activité de copie qui est configuré toouse hello des jeux de données d’entrée et de sortie, et est toorun planifiée toutes les heures. Dans la définition JSON du pipeline hello, hello **source** type est défini trop**FileSystemSource**et hello **récepteur** type est défini trop**BlobSink**.

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "FTPToBlobCopy",
            "inputs": [{
                "name": "FtpFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
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
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-08-24T18:00:00Z",
        "end": "2016-08-24T19:00:00Z"
    }
}
```
> [!NOTE]
> colonnes de toomap de toocolumns du jeu de données source à partir du jeu de données récepteur, consultez [mappage des colonnes de jeu de données dans Azure Data Factory](data-factory-map-columns.md).

## <a name="next-steps"></a>Étapes suivantes
Consultez hello suivant des articles :

* impact sur les performances de déplacement des données (activité de copie) dans la fabrique de données et différentes façons toooptimize des facteurs toolearn sur la clé, consultez hello [copier activité guide des performances et paramétrage](data-factory-copy-activity-performance.md).

* Pour obtenir des instructions pour la création d’un pipeline avec une activité de copie, consultez hello [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
