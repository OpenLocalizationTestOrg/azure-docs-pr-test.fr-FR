---
title: "aaaMove des données à partir du serveur SFTP à l’aide d’Azure Data Factory | Documents Microsoft"
description: "En savoir plus sur la façon de toomove les données à partir d’un site local ou un serveur SFTP en nuage à l’aide d’Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: jingwang
ms.openlocfilehash: b976289e2c1b1899634bb5565b375499077fa554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-sftp-server-using-azure-data-factory"></a>Déplacer des données depuis un serveur SFTP à l’aide d’Azure Data Factory
Cet article décrit comment toouse hello activité de copie de données Azure Data Factory toomove un tooa de serveur SFTP sur le site/cloud prises en charge le magasin de données récepteur. Cet article s’appuie sur hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article qui présente une vue d’ensemble du déplacement des données avec la liste des activités et hello copie de banques de données pris en charge en tant que sources/récepteurs.

Fabrique de données prend actuellement en charge uniquement le déplacement de banques de données à partir d’une données tooother du serveur SFTP, mais pas pour déplacer des données d’autres données de magasins serveur SFTP de tooan. Il prend en charge à la fois les serveurs SFTP locaux et cloud.

> [!NOTE]
> Activité de copie ne supprime pas le fichier de source de hello lorsqu’elle est correctement copié toohello destination. Si vous avez besoin de fichier de source de hello toodelete après la copie a réussi, créer un fichier de hello toodelete activité personnalisée et utiliser l’activité hello dans le pipeline de hello. 

## <a name="supported-scenarios-and-authentication-types"></a>Scénarios et types d’authentification pris en charge
Vous pouvez utiliser ce SFTP connecteur toocopy les données de **à la fois de cloud computing serveurs SFTP et les serveurs SFTP local**. **Base** et **paramètres SshPublicKey** types d’authentification sont pris en charge lors de la connexion du serveur SFTP de toohello.

Lors de la copie des données à partir d’un serveur SFTP de local, vous devez installer une passerelle de gestion des données dans hello local environnement/Azure VM. Consultez [passerelle de gestion des données](data-factory-data-management-gateway.md) pour plus d’informations sur la passerelle hello. Consultez [déplacement des données entre les emplacements locaux et cloud](data-factory-move-data-between-onprem-and-cloud.md) article pour obtenir des instructions sur la configuration de passerelle de hello et l’utiliser.

## <a name="getting-started"></a>Prise en main
Vous pouvez créer un pipeline avec une activité de copie qui déplace les données d’une source SFTP à l’aide de différents outils/API.

- toocreate de façon plus simple Hello un pipeline est toouse hello **Assistant copie de**. Consultez [didacticiel : créer un pipeline à l’aide d’Assistant copie de](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapides sur la création d’un pipeline à l’aide d’Assistant de données de copie hello.

- Vous pouvez également utiliser hello suivant outils toocreate un pipeline : **portail Azure**, **Visual Studio**, **Azure PowerShell**, **modèle Azure Resource Manager** , **API .NET**, et **API REST**. Consultez [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions toocreate un pipeline avec une activité de copie. Pour JSON échantillonne les données de toocopy de tooAzure du serveur SFTP stockage d’objets Blob, consultez [exemple de JSON : copier des données d’objet blob tooAzure de serveur SFTP](#json-example-copy-data-from-sftp-server-to-azure-blob) section de cet article.

## <a name="linked-service-properties"></a>Propriétés du service lié
Hello tableau suivant fournit la description du service de tooFTP spécifique lié éléments JSON.

| Propriété | Description | Requis |
| --- | --- | --- | --- |
| type | propriété de type Hello doit être définie trop`Sftp`. |Oui |
| host | Nom ou adresse IP du serveur SFTP de hello. |Oui |
| port |Port d’écoute sur le hello SFTP serveur. la valeur par défaut Hello est : 21 |Non |
| authenticationType |Spécification du type d’authentification. Valeurs autorisées : **De base** et **SshPublicKey**. <br><br> Consultez trop[l’authentification de base à l’aide](#using-basic-authentication) et [à l’aide de SSH authentification par clé publique](#using-ssh-public-key-authentication) sections respectivement sur plus de propriétés et des exemples JSON. |Oui |
| skipHostKeyValidation | Spécifiez si tooskip validation de clé de l’hôte. | Non. Hello la valeur par défaut : false |
| hostKeyFingerprint | Spécifier les empreintes hello de clé d’hôte hello. | Oui si hello `skipHostKeyValidation` a la valeur toofalse.  |
| gatewayName |Nom de hello passerelle de gestion des données tooconnect tooan local serveur SFTP. | Oui en cas de copie de données à partir d’un serveur SFTP local. |
| Encryptedcredential | Les informations d’identification chiffrées tooaccess hello SFTP le serveur. Généré automatiquement lorsque vous spécifiez l’authentification de base (nom d’utilisateur + mot de passe) ou paramètres SshPublicKey (nom d’utilisateur + chemin d’accès de la clé privée ou contenu) dans la copie Assistant ou hello ClickOnce boîte de dialogue contextuelle. | Non. S’applique uniquement pour la copie de données à partir d’un serveur SFTP local. |

### <a name="using-basic-authentication"></a>Utilisation de l’authentification de base

l’authentification de base toouse, définissez `authenticationType` comme `Basic`et spécifiez les propriétés suivantes en plus de hello connecteur SFTP génériques introduits dans la dernière section de hello de hello :

| Propriété | Description | Requis |
| --- | --- | --- | --- |
| username | Utilisateur a accès toohello SFTP serveur. |Oui |
| password | Mot de passe pour l’utilisateur hello (nom d’utilisateur). | Oui |

#### <a name="example-basic-authentication"></a>Exemple : authentification de base
```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "password": "xxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
    }
}
```

#### <a name="example-basic-authentication-with-encrypted-credential"></a>Exemple : authentification de base avec des informations d’identification chiffrées

```JSON
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
      }
}
```

### <a name="using-ssh-public-key-authentication"></a>Utilisation de l’authentification par clé publique SSH

toouse SSH authentification par clé publique, définissez `authenticationType` comme `SshPublicKey`et spécifiez les propriétés suivantes en plus de hello connecteur SFTP génériques introduits dans la dernière section de hello de hello :

| Propriété | Description | Requis |
| --- | --- | --- | --- |
| username |Utilisateur qui a accès toohello SFTP serveur |Oui |
| privateKeyPath | Spécifiez le chemin d’accès absolu toohello cette passerelle peut accéder à fichier de clé privée. | Spécifiez soit hello `privateKeyPath` ou `privateKeyContent`. <br><br> S’applique uniquement pour la copie de données à partir d’un serveur SFTP local. |
| privateKeyContent | Une chaîne sérialisée de contenu de clé privée hello. Hello Assistant copie peut lire le fichier de clé privée hello et extraire le contenu de clé privée hello automatiquement. Si vous utilisez n’importe quel autre outil/Kit de développement logiciel, utilisez à la place des propriétés de privateKeyPath hello. | Spécifiez soit hello `privateKeyPath` ou `privateKeyContent`. |
| passPhrase | Spécifiez hello expression/mot de passe toodecrypt hello privée clé si le fichier de clé hello est protégé par un mot de passe. | Oui si le fichier de clé privée hello est protégé par un mot de passe. |

> [!NOTE]
> Le connecteur SFTP prend uniquement en charge la clé OpenSSH. Assurez-vous que votre fichier de clé hello format est correct. Vous pouvez utiliser tooconvert outil Putty depuis le format de tooOpenSSH .ppk.

#### <a name="example-sshpublickey-authentication-using-private-key-filepath"></a>Exemple : authentification SshPublicKey à l’aide du chemin du fichier de clé privée

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyPath",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyPath": "D:\\privatekey_openssh",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true,
            "gatewayName": "mygateway"
        }
    }
}
```

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a>Exemple : authentification SshPublicKey à l’aide du contenu de clé privée

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyContent",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver.westus.cloudapp.azure.com",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyContent": "<base64 string of hello private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

## <a name="dataset-properties"></a>Propriétés du jeu de données
Pour obtenir une liste complète des sections et les propriétés disponibles pour définir des jeux de données, consultez hello [création de datasets](data-factory-create-datasets.md) l’article. Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données.

Hello **typeProperties** section est différente pour chaque type de jeu de données. Il fournit des informations qui sont le type de jeu de données toohello spécifique. un jeu de données de type Hello typeProperties section **le partage de fichiers** dataset a hello propriétés suivantes :

| Propriété | Description | Requis |
| --- | --- | --- |
| folderPath |Sous-dossier des toohello chemin d’accès. Utilisez le caractère d’échappement ' \ ' pour les caractères spéciaux dans la chaîne de hello. Consultez la section [Exemples de définitions de jeux de données et de service liés](#sample-linked-service-and-dataset-definitions) pour obtenir des exemples.<br/><br/>Vous pouvez combiner cette propriété avec **partitionBy** toohave chemins d’accès basés sur un secteur de début et date et l’heure de fin. |Oui |
| fileName |Spécifiez le nom hello du fichier de hello Bonjour **folderPath** si vous souhaitez hello table toorefer tooa fichier spécifique dans le dossier de hello. Si vous ne spécifiez pas de valeur pour cette propriété, la table de hello pointe tooall des fichiers dans le dossier de hello.<br/><br/>Lorsque le nom de fichier n’est pas spécifié pour un dataset de sortie, nom hello du fichier de hello généré serait Bonjour sous ce format : <br/><br/>Data.<Guid>.txt (par exemple : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt) |Non |
| fileFilter |Spécifier qu'un filtre toobe utilisé tooselect un sous-ensemble de fichiers dans hello folderPath plutôt que tous les fichiers.<br/><br/>Les valeurs autorisées sont : `*` (plusieurs caractères) et `?` (caractère unique).<br/><br/>Exemple 1 : `"fileFilter": "*.log"`<br/>Exemple 2 : `"fileFilter": 2014-1-?.txt"`<br/><br/> fileFilter s’applique à un jeu de données FileShare d’entrée. Cette propriété n’est pas prise en charge avec HDFS. |Non |
| partitionedBy |partitionedBy peut être utilisé toospecify un folderPath dynamique, le nom de fichier de données de série chronologique. Par exemple, folderPath peut être paramétré pour toutes les heures de données. |Non |
| format | Hello, les types de format suivants est pris en charge : **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Ensemble hello **type** propriété sous tooone de format de ces valeurs. Pour en savoir plus, consultez les sections relatives à [format Text](data-factory-supported-file-and-compression-formats.md#text-format), [format Json](data-factory-supported-file-and-compression-formats.md#json-format), [format Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [format Orc](data-factory-supported-file-and-compression-formats.md#orc-format) et [format Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Si vous souhaitez trop**copier les fichiers en tant que-est** entre des magasins basée sur le fichier (copie binaire), ignorer la section de format hello dans les deux définitions de jeu de données d’entrée et de sortie. |Non |
| compression | Spécifiez le type de hello et le niveau de compression pour les données de salutation. Les types pris en charge sont : **GZip**, **Deflate**, **BZip2** et **ZipDeflate**. Les niveaux pris en charge sont **Optimal** et **Fastest**. Pour plus d’informations, consultez [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |Non |
| useBinaryTransfer |Spécifiez si vous voulez utiliser le mode de transfert binaire. True pour le mode binaire et false pour ASCII. Valeur par défaut : true. Cette propriété peut uniquement être utilisée lorsque le type de service lié associé est : FtpServer. |Non |

> [!NOTE]
> fileName et fileFilter ne peuvent pas être utilisés simultanément.

### <a name="using-partionedby-property"></a>Utilisation de la propriété partitionedBy
Comme indiqué dans la section précédente de hello, vous pouvez spécifier un folderPath dynamique, le nom de fichier de données de série chronologique avec partitionedBy. Vous pouvez le faire avec les macros Data Factory hello et variable hello système SliceStart, SliceEnd indiquant hello période logique pour une tranche de données spécifiée.

toolearn sur la série de temps des groupes de données, de planification et de secteurs, consultez [création de Datasets](data-factory-create-datasets.md), [de planification et l’exécution de](data-factory-scheduling-and-execution.md), et [création de Pipelines](data-factory-create-pipelines.md) articles.

#### <a name="sample-1"></a>Exemple 1 :

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
Dans cet exemple {Slice} est remplacé par la valeur hello de fabrique de données variable système SliceStart au format (AAAAMMJJHH) de la hello spécifiée. Hello SliceStart fait référence à des temps de toostart de tranche de hello. Hello folderPath est différent pour chaque secteur. Par exemple : wikidatagateway/wikisampledataout/2014100103 ou wikidatagateway/wikisampledataout/2014100104.

#### <a name="sample-2"></a>Exemple 2 :

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
Dans cet exemple, l'année, le mois, le jour et l'heure de SliceStart sont extraits dans des variables distinctes qui sont utilisées par les propriétés folderPath et fileName.

## <a name="copy-activity-properties"></a>Propriétés de l’activité de copie
Pour obtenir une liste complète des sections et les propriétés disponibles pour la définition d’activités, consultez hello [création de Pipelines](data-factory-create-pipelines.md) l’article. Les propriétés comme le nom, la description, les tables d'entrée et de sortie et les différentes stratégies sont disponibles pour tous les types d'activités.

Alors que les propriétés de hello disponibles dans la section typeProperties hello activité hello varient selon chaque type d’activité. Pour l’activité de copie, les propriétés de type hello varient selon les types de sources et récepteurs hello.

[!INCLUDE [data-factory-file-system-source](../../includes/data-factory-file-system-source.md)]

## <a name="supported-file-and-compression-formats"></a>Formats de fichier et de compression pris en charge
Pour plus d’informations, voir [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md).

## <a name="json-example-copy-data-from-sftp-server-tooazure-blob"></a>Exemple de JSON : Copier des données d’objet blob tooAzure de serveur SFTP
Hello exemple suivant fournit des exemples de définitions de JSON que vous pouvez utiliser toocreate un pipeline à l’aide de [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Elles montrent comment la source de données de toocopy de SFTP tooAzure stockage d’objets Blob. Toutefois, les données peuvent être copiées **directement** de n’importe quelle tooany de sources de récepteurs hello indiqué [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) à l’aide de hello activité de copie dans Azure Data Factory.

> [!IMPORTANT]
> Cet exemple fournit des extraits de code JSON. Il n’inclut pas d’instructions détaillées pour créer la fabrique de données hello. Les instructions se trouvent dans l’article [Déplacement de données entre des emplacements locaux et le cloud](data-factory-move-data-between-onprem-and-cloud.md) .

exemple Hello a hello suivant des entités de fabrique de données :

* Un service lié de type [sftp](#linked-service-properties).
* Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
* Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [FileShare](#dataset-properties).
* Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* Un [pipeline](data-factory-create-pipelines.md) avec activité de copie qui utilise [FileSystemSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

exemple Hello copie des données à partir d’un tooan du serveur SFTP blob Azure toutes les heures. propriétés JSON Hello utilisées dans ces exemples sont décrits dans les sections suivantes des exemples de hello.

**Service lié SFTP**

Cet exemple utilise l’authentification de base hello avec le nom d’utilisateur et mot de passe en texte brut. Vous pouvez également utiliser un des hello suivant façons :

* Authentification de base avec des informations d’identification chiffrées
* Authentification par clé publique SSH

Consultez la section [Service lié FTP](#linked-service-properties) pour connaître les différents types d’authentification que vous pouvez utiliser.

```JSON

{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "myuser",
            "password": "mypassword",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
    }
}
```
**Service lié Azure Storage**

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
**Jeu de données d’entrée SFTP**

Ce jeu de données fait référence le dossier SFTP toohello `mysharedfolder` et le fichier `test.csv`. Hello pipeline copies hello toohello destination du fichier.

Paramètre « external » : « true » informe service Data Factory de hello ce jeu de données hello est la fabrique de données externe toohello et n’est pas généré par une activité dans la fabrique de données hello.

```JSON
{
  "name": "SFTPFileInput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": "SftpLinkedService",
    "typeProperties": {
      "folderPath": "mysharedfolder",
      "fileName": "test.csv"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

**Jeu de données de sortie d’objet Blob Azure**

Les données sont écrites tooa nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1). chemin d’accès du dossier Hello pour l’objet blob de hello est évaluée dynamiquement en fonction de l’heure de début hello de tranche hello qui est en cours de traitement. chemin d’accès du dossier Hello utilise l’année, mois, jours et heures des parties de l’heure de début hello.

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sftp/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

**Pipeline avec activité de copie**

Hello pipeline contient une activité de copie qui est configuré toouse hello des jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures. Dans la définition JSON du pipeline hello, hello **source** type est défini trop**FileSystemSource** et **récepteur** type est défini trop**BlobSink**.

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "SFTPToBlobCopy",
            "inputs": [{
                "name": "SFTPFileInput"
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
        "start": "2017-02-20T18:00:00Z",
        "end": "2017-02-20T19:00:00Z"
    }
}
```

## <a name="performance-and-tuning"></a>Performances et réglage
Consultez [copie activité optimiser les performances et Guide d’optimisation](data-factory-copy-activity-performance.md) toolearn sur la clé de facteurs d’affecter les performances de transfert de données (activité de copie) dans Azure Data Factory et de différentes façons toooptimize il.

## <a name="next-steps"></a>Étapes suivantes
Consultez hello suivant des articles :

* [Didacticiel de l’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions détaillées sur la création d’un pipeline avec Activité de copie.
