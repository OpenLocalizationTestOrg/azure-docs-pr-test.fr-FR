---
title: "aaaMove des données à partir d’une source HTTP - Azure | Documents Microsoft"
description: "En savoir plus sur la façon dont la source de données toomove à partir d’un site local ou un cloud HTTP à l’aide d’Azure Data Factory."
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
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: e39b9cbff870aef4be91938cacff39a2fd12d64a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-http-source-using-azure-data-factory"></a>Déplacer des données à partir d’une source HTTP à l’aide d’Azure Data Factory
Cet article décrit comment toouse hello activité de copie de données Azure Data Factory toomove un tooa de point de terminaison HTTP sur le site/cloud prises en charge le magasin de données récepteur. Cet article s’appuie sur hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article qui présente une vue d’ensemble du déplacement des données avec la liste des activités et hello copie de banques de données pris en charge en tant que sources/récepteurs.

Fabrique de données actuellement prend en charge uniquement déplacement de données à partir d’un HTTP source tooother des magasins de données, mais ne pas déplacer les données à partir d’autres données stocke tooan HTTP destination.

## <a name="supported-scenarios-and-authentication-types"></a>Scénarios et types d’authentification pris en charge
Vous pouvez utiliser ces données de tooretrieve du connecteur HTTP à partir de **cloud et locales point de terminaison HTTP/s** à l’aide de HTTP **obtenir** ou **POST** (méthode). Hello, les types d’authentification suivants est pris en charge : **anonyme**, **base**, **Digest**, **Windows**, et  **ClientCertificate**. Notez la différence de hello entre ce connecteur et le hello [connecteur de table Web](data-factory-web-table-connector.md) est : hello ce dernier est utilisé tooextract table de contenu à partir de page web HTML.

Lors de la copie des données à partir d’un point de terminaison HTTP local, vous devez installer une passerelle de gestion des données dans hello local environnement/Azure VM. Consultez [déplacement des données entre les emplacements locaux et cloud](data-factory-move-data-between-onprem-and-cloud.md) toolearn l’article sur la passerelle de gestion des données et des instructions détaillées sur la configuration de passerelle de hello.

## <a name="getting-started"></a>Prise en main
Vous pouvez créer un pipeline avec une activité de copie qui déplace les données d’une source HTTP à l’aide de différents outils/API.

- toocreate de façon plus simple Hello un pipeline est toouse hello **Assistant copie de**. Consultez [didacticiel : créer un pipeline à l’aide d’Assistant copie de](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapides sur la création d’un pipeline à l’aide d’Assistant de données de copie hello.

- Vous pouvez également utiliser hello suivant outils toocreate un pipeline : **portail Azure**, **Visual Studio**, **Azure PowerShell**, **modèle Azure Resource Manager** , **API .NET**, et **API REST**. Consultez [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions toocreate un pipeline avec une activité de copie. Pour JSON échantillonne les données de toocopy à partir de la source HTTP tooAzure stockage d’objets Blob, consultez [exemples JSON](#json-examples) section de cet article.

## <a name="linked-service-properties"></a>Propriétés du service lié
Hello tableau suivant fournit la description du service de tooHTTP spécifique lié éléments JSON.

| Propriété | Description | Requis |
| --- | --- | --- |
| type | propriété de type Hello doit indiquer : `Http`. | Oui |
| url | Toohello de l’URL du serveur Web de base | Oui |
| authenticationType | Spécifie le type d’authentification hello. Les valeurs autorisées sont : **Anonymous** (Anonyme), **Basic** (De base), **Digest**, **Windows**, **ClientCertificate** (Certificat client). <br><br> Font respectivement référence toosections sous ce tableau sur plus de propriétés et des exemples JSON pour ces types d’authentification. | Oui |
| enableServerCertificateValidation | Spécifiez si le serveur tooenable SSL la validation des certificats si la source est le serveur de Web HTTPS | Non, la valeur par défaut est True. |
| gatewayName | Nom de tooan de tooconnect hello passerelle de gestion des données sur site source HTTP. | Oui en cas de copie de données à partir d’une source HTTP locale. |
| Encryptedcredential | Les informations d’identification chiffrées tooaccess hello de point de terminaison HTTP. Généré automatiquement lorsque vous configurez des informations d’authentification hello dans copie Assistant ou hello ClickOnce boîte de dialogue contextuelle. | Non. S’applique uniquement pour la copie de données à partir d’un serveur HTTP local. |

Consultez [déplacement des données entre des sources locales et cloud hello avec la passerelle de gestion des données](data-factory-move-data-between-onprem-and-cloud.md) pour plus d’informations sur la définition des informations d’identification pour la source de données du connecteur local HTTP.

### <a name="using-basic-digest-or-windows-authentication"></a>Utilisation de l’authentification Basic (De base), Digest ou Windows

Définissez `authenticationType` en tant que `Basic`, `Digest`, ou `Windows`et spécifiez hello propriétés suivantes en plus de hello du connecteur HTTP générique celles présentées ci-dessus :

| Propriété | Description | Requis |
| --- | --- | --- |
| username | Nom d’utilisateur tooaccess hello de point de terminaison HTTP. | Oui |
| password | Mot de passe pour l’utilisateur hello (nom d’utilisateur). | Oui |

#### <a name="example-using-basic-digest-or-windows-authentication"></a>Exemple : utilisation de l’authentification Basic (De base), Digest ou Windows

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "basic",
            "url" : "https://en.wikipedia.org/wiki/",
            "userName": "user name",
            "password": "password"
        }
    }
}
```

### <a name="using-clientcertificate-authentication"></a>Utilisation de l’authentification ClientCertificate (Certificat client)

l’authentification de base toouse, définissez `authenticationType` comme `ClientCertificate`et spécifiez hello propriétés suivantes en plus de hello du connecteur HTTP générique celles présentées ci-dessus :

| Propriété | Description | Requis |
| --- | --- | --- |
| embeddedCertData | contenu codé en Base64 Hello de données binaires du fichier d’informations Exchange PFX (Personal) hello. | Spécifiez soit hello `embeddedCertData` ou `certThumbprint`. |
| certThumbprint | Bonjour empreinte numérique du certificat hello qui a été installé sur le magasin de certificats de l’ordinateur de votre passerelle. S’applique uniquement pour la copie de données à partir d’une source HTTP locale. | Spécifiez soit hello `embeddedCertData` ou `certThumbprint`. |
| password | Mot de passe associé au certificat de hello. | Non |

Si vous utilisez `certThumbprint` pour l’authentification et hello du certificat est installé dans le magasin personnel de l’ordinateur local de hello de hello, vous devez le service passerelle toohello toogrant hello autorisation de lecture :

1. Lancez Microsoft Management Console (MMC). Ajouter hello **certificats** que hello cibles du composant logiciel enfichable **ordinateur Local**.
2. Développez **Certificats**, **Personnel**, puis cliquez sur **Certificats**.
3. Certificat hello magasin personnel de hello d’avec le bouton droit, puis sélectionnez **toutes les tâches**->**gérer les clés privées...**
3. Sur hello **sécurité** onglet, ajoutez le compte d’utilisateur hello sous lequel le Service hôte de passerelle de gestion des données s’exécute avec le certificat de toohello hello accès en lecture.  

#### <a name="example-using-client-certificate"></a>Exemple : utilisation d’un certificat client
Cela les liaisons de service vos données fabrique tooan local HTTP web serveur lié. Il utilise un certificat de client est installé sur l’ordinateur de hello avec la passerelle de gestion des données installé.

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "certThumbprint": "thumbprint of certificate",
            "gatewayName": "gateway name"

        }
    }
}
```

#### <a name="example-using-client-certificate-in-a-file"></a>Exemple : utilisation d’un certificat client dans un fichier
Cela les liaisons de service vos données fabrique tooan local HTTP web serveur lié. Elle utilise un fichier de certificat client sur l’ordinateur de hello avec la passerelle de gestion des données installé.

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "embeddedCertData": "base64 encoded cert data",
            "password": "password of cert"
        }
    }
}
```

## <a name="dataset-properties"></a>Propriétés du jeu de données
Pour obtenir une liste complète des sections et les propriétés disponibles pour définir des jeux de données, consultez hello [création de datasets](data-factory-create-datasets.md) l’article. Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données (SQL Azure, Azure Blob, Azure Table, etc.).

Hello **typeProperties** section est différente pour chaque type de jeu de données et fournit des informations sur l’emplacement de hello de données hello dans le magasin de données hello. jeu de données de type Hello typeProperties section **Http** a les propriétés suivantes de hello

| Propriété | Description | Requis |
|:--- |:--- |:--- |
| type | Type hello du jeu de données hello spécifié. doit être défini trop`Http`. | Oui |
| relativeUrl | Une ressource URL toohello relative qui contient les données de salutation. Lorsque le chemin d’accès n’est pas spécifié, seul hello URL spécifiée dans la définition de service hello lié est utilisé. <br><br> tooconstruct des URL dynamique, vous pouvez utiliser [les variables système et les fonctions de la fabrique de données](data-factory-functions-variables.md), par exemple, « relativeUrl » : « $$Text.Format ('/ my/rapport ? mois = {0}-{0:MM} & fmt = csv », SliceStart) ». | Non |
| requestMethod | Méthode HTTP. Les valeurs autorisées sont **GET** ou **POST**. | Non. La valeur par défaut est `GET`. |
| additionalHeaders | En-têtes de requête HTTP supplémentaires. | Non |
| RequestBody | Corps de la requête HTTP. | Non |
| format | Si vous souhaitez toosimply **hello de données à partir du point de terminaison HTTP en tant que-est** sans qu’il analyse, ignorer les paramètres de ce format. <br><br> Si vous souhaitez la réponse de hello HTTP tooparse contenu pendant la copie, hello les types de format suivants est pris en charge : **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**. Pour en savoir plus, consultez les sections relatives à [format Text](data-factory-supported-file-and-compression-formats.md#text-format), [format Json](data-factory-supported-file-and-compression-formats.md#json-format), [format Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [format Orc](data-factory-supported-file-and-compression-formats.md#orc-format) et [format Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format). |Non |
| compression | Spécifiez le type de hello et le niveau de compression pour les données de salutation. Les types pris en charge sont : **GZip**, **Deflate**, **BZip2** et **ZipDeflate**. Les niveaux pris en charge sont **Optimal** et **Fastest**. Pour plus d’informations, consultez [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |Non |

### <a name="example-using-hello-get-default-method"></a>Exemple : utilisation de méthode GET (par défaut) de hello

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "XXX/test.xml",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

### <a name="example-using-hello-post-method"></a>Exemple : utilisation de méthode POST hello

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "/XXX/test.xml",
           "requestMethod": "Post",
            "requestBody": "body for POST HTTP request"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

## <a name="copy-activity-properties"></a>Propriétés de l’activité de copie
Pour obtenir une liste complète des sections et les propriétés disponibles pour la définition d’activités, consultez hello [création de Pipelines](data-factory-create-pipelines.md) l’article. Les propriétés comme le nom, la description, les tables d’entrée et de sortie et la stratégie sont disponibles pour tous les types d’activités.

Propriétés disponibles dans hello **typeProperties** section de l’activité de hello sur hello autre part varient selon chaque type d’activité. Pour l’activité de copie, ils varient selon les types de sources et récepteurs hello.

Actuellement, lorsque source hello dans l’activité de copie est de type **HttpSource**, hello propriétés suivantes est prises en charge.

| Propriété | Description | Requis |
| -------- | ----------- | -------- |
| httpRequestTimeout | Bonjour le délai d’attente (TimeSpan) pour tooget de demande HTTP hello une réponse. Il est tooget hello du délai d’attente de réponse, pas les données de réponse du tooread hello du délai d’attente. | Non. Valeur par défaut : 00:01:40 |

## <a name="supported-file-and-compression-formats"></a>Formats de fichier et de compression pris en charge
Pour plus d’informations, voir [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md).

## <a name="json-examples"></a>Exemples JSON
Hello exemple ci-dessous fournit des exemples de définitions de JSON que vous pouvez utiliser toocreate un pipeline à l’aide de [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Elles montrent comment la source de données de toocopy HTTP tooAzure stockage d’objets Blob. Toutefois, les données peuvent être copiées **directement** de n’importe quelle tooany de sources de récepteurs hello indiqué [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) à l’aide de hello activité de copie dans Azure Data Factory.

### <a name="example-copy-data-from-http-source-tooazure-blob-storage"></a>Exemple : Copier des données à partir de la source HTTP tooAzure stockage d’objets Blob
Hello solution Data Factory pour cet exemple contient hello suivant des entités de fabrique de données :

1. Un service lié de type [HTTP](#linked-service-properties).
2. Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [Http](#dataset-properties).
4. Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [ttpSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

exemple Hello copie des données à partir d’un tooan de source HTTP blob Azure toutes les heures. propriétés JSON Hello utilisées dans ces exemples sont décrits dans les sections suivantes des exemples de hello.

### <a name="http-linked-service"></a>Service lié HTTP
Cet exemple utilise hello HTTP lié à service avec l’authentification anonyme. Pour connaître les différents types d’authentification que vous pouvez utiliser, consultez la section [Service lié HTTP](#linked-service-properties).

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
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

### <a name="http-input-dataset"></a>Jeu de données d’entrée HTTP
Paramètre **externe** trop**true** informe le service de fabrique de données hello ce jeu de données hello est la fabrique de données externe toohello et n’est pas généré par une activité dans la fabrique de données hello.

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}

```

### <a name="azure-blob-output-dataset"></a>Jeu de données de sortie d’objet Blob Azure

Les données sont écrites tooa nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1).

```JSON
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/Movies"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

### <a name="pipeline-with-copy-activity"></a>Pipeline avec activité de copie

Hello pipeline contient une activité de copie qui est configuré toouse hello des jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures. Dans la définition JSON du pipeline hello, hello **source** type est défini trop**HttpSource** et **récepteur** type est défini trop**BlobSink**.

Consultez [HttpSource](#copy-activity-properties) pour la liste des propriétés prises en charge par hello HttpSource hello.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "HttpSourceToAzureBlob",
        "description": "Copy from an HTTP source tooan Azure blob",
        "type": "Copy",
        "inputs": [
          {
            "name": "HttpSourceDataInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "HttpSource"
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

> [!NOTE]
> colonnes de toomap de toocolumns du jeu de données source à partir du jeu de données récepteur, consultez [mappage des colonnes de jeu de données dans Azure Data Factory](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Performances et réglage
Consultez [copie activité optimiser les performances et Guide d’optimisation](data-factory-copy-activity-performance.md) toolearn sur la clé de facteurs d’affecter les performances de transfert de données (activité de copie) dans Azure Data Factory et de différentes façons toooptimize il.
