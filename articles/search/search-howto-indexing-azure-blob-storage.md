---
title: "aaaIndexing stockage d’objets Blob Azure avec Azure Search"
description: "Découvrez comment tooindex objets Blob Azure Storage et extrait le texte à partir de documents avec Azure Search"
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 2a5968f4-6768-4e16-84d0-8b995592f36a
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/22/2017
ms.author: eugenesh
ms.openlocfilehash: 1bdd34e66a4a9192ed88cacbc7b8456d0dcdfeb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-documents-in-azure-blob-storage-with-azure-search"></a>Indexation de documents dans Azure Blob Storage avec Azure Search
Cet article explique comment les documents tooindex toouse Azure Search (tels que des fichiers PDF, les documents Microsoft Office et plusieurs autres formats courants) stockées dans le stockage Blob Azure. Tout d’abord, il explique principes fondamentaux de hello de paramétrage et configuration d’un indexeur d’objet blob. Ensuite, il propose une exploration plus approfondie de comportements et les scénarios, vous êtes probablement tooencounter.

## <a name="supported-document-formats"></a>Formats de document pris en charge
indexeur d’objet blob Hello peut extraire le hello suivant les formats de documents de texte :

* PDF
* Formats Microsoft Office : DOCX/DOC, XLSX/XLS, PPTX/PPT, MSG (e-mails Outlook)  
* HTML
* XML
* ZIP
* EML
* RTF
* Fichiers de texte brut (voir aussi [l’indexation de texte brut](#IndexingPlainText))
* JSON (consultez [l’indexation d’objets JSON blobs](search-howto-index-json-blobs.md))
* CSV (voir la fonctionnalité de version préliminaire[Indexation d’objets blob CSV](search-howto-index-csv-blobs.md))

> [!IMPORTANT]
> La prise en charge des tableaux CSV et JSON est actuellement en version préliminaire. Ces formats sont disponibles uniquement à l’aide de la version **2016-09-01-Preview** Hello API REST ou la version 2.x-version préliminaire de hello du SDK .NET. N’oubliez pas que les API d’évaluation sont destinées à être utilisées à des fins de test et d’évaluation, et non dans les environnements de production.
>
>

## <a name="setting-up-blob-indexing"></a>Configuration de l’indexation d’objets blob
Vous pouvez configurer un indexeur de Stockage Blob Azure avec les outils suivants :

* [portail Azure](https://ms.portal.azure.com)
* [API REST](https://docs.microsoft.com/rest/api/searchservice/Indexer-operations) de la Recherche Azure
* [Kit de développement logiciel .NET (SDK)](https://aka.ms/search-sdk) de la Recherche Azure

> [!NOTE]
> Certaines fonctionnalités (par exemple, les mappages de champs) ne sont pas encore disponibles dans le portail de hello et ont toobe utilisé par programme.
>
>

Ici, nous allons montrer le flux hello à l’aide des API REST de hello.

### <a name="step-1-create-a-data-source"></a>Étape 1 : Création d’une source de données
Une source de données spécifie les tooindex de données, des informations d’identification nécessaires tooaccess hello données et stratégies tooefficiently identifient les modifications apportées aux données de hello (lignes nouvelles, modifiées ou supprimées). Une source de données peut être utilisée par plusieurs indexeurs Bonjour même service de recherche.

Pour l’indexation des objets blob, source de données hello doit avoir hello propriétés requises suivantes :

* **nom** est le nom unique de hello hello de source de données au sein de votre service de recherche.
* **type** doit être `azureblob`.
* **informations d’identification** fournit la chaîne de connexion de compte de stockage hello en hello `credentials.connectionString` paramètre. Consultez [comment les informations d’identification de toospecify](#Credentials) ci-dessous pour plus d’informations.
* **container** spécifie un conteneur dans votre compte de stockage. Par défaut, tous les objets BLOB dans le conteneur de hello sont récupérables. Si vous souhaitez uniquement des objets BLOB de tooindex dans un répertoire virtuel particulier, vous pouvez spécifier ce répertoire à l’aide de hello facultatif **requête** paramètre.

toocreate une source de données :

    POST https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>;" },
        "container" : { "name" : "my-container", "query" : "<optional-virtual-directory-name>" }
    }   

Pour plus d’informations sur hello créer la source de données API, consultez [créer la source de données](https://docs.microsoft.com/rest/api/searchservice/create-data-source).

<a name="Credentials"></a>
#### <a name="how-toospecify-credentials"></a>Comment les informations d’identification de toospecify ####

Vous pouvez fournir des informations d’identification hello pour le conteneur d’objets blob hello dans une des manières suivantes :

- **Chaîne de connexion au compte de stockage avec accès complet** : `DefaultEndpointsProtocol=https;AccountName=<your storage account>;AccountKey=<your account key>`. Vous pouvez obtenir la chaîne de connexion hello de hello portail Azure en naviguant dans le panneau de compte de stockage toohello > Paramètres > clés (pour les comptes de stockage classique) ou les paramètres > clés (pour les comptes de stockage Azure Resource Manager).
- **Signature d’accès partagé de compte de stockage** chaîne de connexion (SAS) : `BlobEndpoint=https://<your account>.blob.core.windows.net/;SharedAccessSignature=?sv=2016-05-31&sig=<hello signature>&spr=https&se=<hello validity end time>&srt=co&ss=b&sp=rl` hello SAS doit avoir hello liste et autorisations de lecture sur les conteneurs et objets (les objets BLOB dans ce cas).
-  **Signature d’accès partagé de conteneur**: `ContainerSharedAccessUri=https://<your storage account>.blob.core.windows.net/<container name>?sv=2016-05-31&sr=c&sig=<hello signature>&se=<hello validity end time>&sp=rl` hello SAS doit avoir hello liste et autorisations de lecture sur le conteneur de hello.

Pour plus d’informations sur les signatures d’accès partagé au stockage, consultez [Utilisation des signatures d’accès partagé](../storage/common/storage-dotnet-shared-access-signature-part-1.md).

> [!NOTE]
> Si vous utilisez les informations d’identification SAP, vous devez informations d’identification de source de tooupdate hello données régulièrement avec des signatures renouvelé tooprevent leur expiration. Si l’expirent des informations d’identification SAP, indexeur de hello échoue avec un message d’erreur similaire trop`Credentials provided in hello connection string are invalid or have expired.`.  

### <a name="step-2-create-an-index"></a>Étape 2 : Création d’un index
index de Hello spécifie les champs hello dans un document, les attributs, et d’autres constructions cette expérience de recherche de forme hello.

Voici comment toocreate un index avec une recherche `content` champ texte hello de toostore extraite à partir d’objets BLOB :   

    POST https://[service name].search.windows.net/indexes?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
          "name" : "my-target-index",
          "fields": [
            { "name": "id", "type": "Edm.String", "key": true, "searchable": false },
            { "name": "content", "type": "Edm.String", "searchable": true, "filterable": false, "sortable": false, "facetable": false }
          ]
    }

Pour plus d’informations sur la création d’index, consultez [Création d'un index](https://docs.microsoft.com/rest/api/searchservice/create-index)

### <a name="step-3-create-an-indexer"></a>Étape 3 : Création d’un indexeur
Un indexeur connecte une source de données avec un index de recherche cible et fournit une actualisation planifiée des données tooautomate hello.

Une fois que la source de données et d’index hello ont été créées, vous êtes indexeur de hello toocreate prêt :

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "blob-indexer",
      "dataSourceName" : "blob-datasource",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" }
    }

Cet indexeur s’exécute toutes les deux heures (intervalle de planification est défini trop « PT2H »). toorun un indexeur toutes les 30 minutes, définissez intervalle de salutation trop « PT30M ». intervalle de pris en charge le plus court Hello est de 5 minutes. Bonjour planification est facultative : en cas d’omission, un indexeur s’exécute qu’une seule fois lorsqu’il est créé. Toutefois, vous pouvez à tout moment exécuter un indexeur à la demande.   

Pour plus d’informations sur hello créer des API indexeur, l’extraction [créer un indexeur](https://docs.microsoft.com/rest/api/searchservice/create-indexer).

## <a name="how-azure-search-indexes-blobs"></a>Comment Azure Search indexe les objets blob

En fonction de hello [configuration de l’indexeur](#PartsOfBlobToIndex), indexeur d’objet blob hello peut indexer uniquement les métadonnées de stockage (utile quand vous ne tenant compte sur hello des métadonnées et n’avez pas besoin de tooindex hello contenu d’objets BLOB), les métadonnées de stockage et le contenu ou les deux les métadonnées et le contenu textuel. Par défaut, indexeur de hello extrait les métadonnées et le contenu.

> [!NOTE]
> Par défaut, les objets blob avec contenu structuré tels que JSON ou CSV sont indexés en tant que bloc de texte unique. Si vous souhaitez tooindex JSON et les volumes partagés de cluster les objets BLOB de façon structurée, consultez [JSON de l’indexation des objets BLOB](search-howto-index-json-blobs.md) et [CSV de l’indexation des objets BLOB](search-howto-index-csv-blobs.md) fonctionnalités en version préliminaire.
>
> Un document composé ou incorporé (tel qu’une archive ZIP ou un document Word avec e-mail Outlook incorporé intégrant des pièces jointes) est également indexé en tant que document unique.

* du contenu textuel du document de hello Hello est extrait dans un champ de chaîne nommé `content`.

> [!NOTE]
> Azure Search limite la quantité de texte qu’il extrait en fonction du niveau tarifaire de hello : 32 000 caractères pour un niveau, 64 000 Basic et 4 millions de niveaux Standard, Standard S2 et S3 Standard. Un avertissement est inclus dans la réponse d’état indexeur hello pour les documents tronquées.  

* Propriétés de métadonnées de spécifié par l’utilisateur présentes sur l’objet blob de hello, le cas échéant, sont extraits textuellement.
* Propriétés de métadonnées d’objet blob standard sont extraits dans hello suivant de champs :

  * **métadonnées\_stockage\_nom** (Edm.String) - nom du fichier d’objet blob de hello hello. Par exemple, si vous avez un objet blob de /my-container/my-folder/subfolder/resume.pdf, valeur hello de ce champ est `resume.pdf`.
  * **métadonnées\_stockage\_chemin d’accès** (Edm.String) - hello URI complet de l’objet blob de hello, y compris le compte de stockage hello. Par exemple, `https://myaccount.blob.core.windows.net/my-container/my-folder/subfolder/resume.pdf`
  * **métadonnées\_stockage\_contenu\_type** (Edm.String) - type de contenu spécifié par le code de hello vous utilisé des objets blob de tooupload hello. Par exemple, `application/octet-stream`.
  * **métadonnées\_stockage\_dernière\_modifié** (Edm.DateTimeOffset) - dernière modification de l’horodateur pour l’objet blob de hello. Azure Search utilise ce blob tooidentify modifié timestamp, tooavoid tout réindexation après indexation initiale hello.
  * **metadata\_storage\_size** (Edm.Int64) : taille de l’objet blob en octets.
  * **métadonnées\_stockage\_contenu\_md5** (Edm.String) - hachage MD5 du contenu d’objet blob hello, s’il est disponible.
* Format de document de métadonnées propriétés tooeach spécifiques sont extraits dans les champs hello répertoriés [ici](#ContentSpecificMetadata).

Vous n’avez pas besoin toodefine champs pour tous les hello au-dessus des propriétés dans votre index de recherche - capture uniquement les propriétés hello que vous avez besoin pour votre application.

> [!NOTE]
> Souvent, les noms de champs hello dans votre index existant sera différents de noms de champs hello générés pendant l’extraction du document. Vous pouvez utiliser **champ mappages** noms de propriété hello toomap fournis par des noms de champ toohello Azure Search dans votre index de recherche. Découvrez ci-dessous une exemple d’utilisation de mappage de champ.
>
>

<a name="DocumentKeys"></a>
### <a name="defining-document-keys-and-field-mappings"></a>Définition des clés de document et des mappages de champs
Dans Azure Search, clé de document hello identifie de façon unique un document. Chaque index de recherche doit comporter exactement un champ de clé de type Edm.String. champ de clé Hello est requis pour chaque document en cours d’ajout des index toohello (il est réellement hello seul champ obligatoire).  

Vous devez soigneusement quel champ extrait doit mapper le champ de clé de toohello pour votre index. les candidats Hello sont :

* **métadonnées\_stockage\_nom** : cela peut être pratique, mais notez que les noms de hello (1) peuvent ne pas uniques, comme vous pouvez avoir des objets BLOB avec hello même nom dans le même dossier, et (2) hello nom contient des caractères qui ne sont pas valides dans les clés de document, tels que des tirets. Vous pouvez traiter des caractères non valides à l’aide de hello `base64Encode` [fonction de mappage de champ](search-indexer-field-mappings.md#base64EncodeFunction) : Si vous procédez ainsi, n’oubliez pas de clés de document tooencode lorsque les transmettre dans l’API appelle tels que de la recherche. (Par exemple, dans .NET, vous pouvez utiliser hello [UrlTokenEncode méthode](https://msdn.microsoft.com/library/system.web.httpserverutility.urltokenencode.aspx) à cet effet).
* **métadonnées\_stockage\_chemin d’accès** : à l’aide du chemin d’accès complet de hello garantit l’unicité, mais le chemin d’accès hello définitivement contient `/` caractères [non valide dans une clé de document](https://docs.microsoft.com/rest/api/searchservice/naming-rules).  Comme indiqué ci-dessus, vous pouvez hello encodage clés hello à l’aide de hello `base64Encode` [fonction](search-indexer-field-mappings.md#base64EncodeFunction).
* Si aucune des options hello ci-dessus vous convient, vous pouvez ajouter un BLOB toohello de propriété des métadonnées personnalisées. Cette option, toutefois, oblige votre tooadd de processus de téléchargement blob ce blob de tooall de propriété de métadonnées. Étant donné que la clé de hello est une propriété obligatoire, tous les objets BLOB qui n’ont pas cette propriété échoue toobe indexé.

> [!IMPORTANT]
> S’il n’existe aucun mappage explicite pour le champ de clé hello dans les index hello, Azure Search utilise automatiquement `metadata_storage_path` comme hello clé et de base-64 encode les valeurs de clé (hello deuxième option ci-dessus).
>
>

Pour cet exemple, nous allons sélectionner hello `metadata_storage_name` champ en tant que clé de document hello. Supposons également que votre index a un champ de clé nommé `key` et un champ `fileSize` pour le stockage de taille de document hello. toowire les choses comme vous le souhaitez, spécifier hello suivant des mappages de champs lors de la création ou mise à jour de l’indexeur :

    "fieldMappings" : [
      { "sourceFieldName" : "metadata_storage_name", "targetFieldName" : "key", "mappingFunction" : { "name" : "base64Encode" } },
      { "sourceFieldName" : "metadata_storage_size", "targetFieldName" : "fileSize" }
    ]

toobring cet ensemble, voici comment vous pouvez ajouter des mappages de champs et activer codage en base 64 de clés pour un indexeur existant :

    PUT https://[service name].search.windows.net/indexers/blob-indexer?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "dataSourceName" : " blob-datasource ",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" },
      "fieldMappings" : [
        { "sourceFieldName" : "metadata_storage_name", "targetFieldName" : "key", "mappingFunction" : { "name" : "base64Encode" } },
        { "sourceFieldName" : "metadata_storage_size", "targetFieldName" : "fileSize" }
      ]
    }

> [!NOTE]
> toolearn en savoir plus sur les mappages de champs, consultez [cet article](search-indexer-field-mappings.md).
>
>

<a name="WhichBlobsAreIndexed"></a>
## <a name="controlling-which-blobs-are-indexed"></a>Contrôle les objets blob indexés
Vous pouvez contrôler les objets BLOB qui sont indexés et ignorés.

### <a name="index-only-hello-blobs-with-specific-file-extensions"></a>Seuls les objets de BLOB hello avec les extensions de fichier spécifique d’index
Vous pouvez indexer des seuls les objets BLOB hello avec les extensions de nom de fichier hello vous spécifiez à l’aide de hello `indexedFileNameExtensions` paramètre de configuration d’indexeur. valeur de Hello est une chaîne contenant une liste séparée par des virgules des extensions de fichier (avec un point de début). Par exemple, tooindex uniquement hello. PDF et. Objets BLOB DOCX, procédez comme suit :

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "indexedFileNameExtensions" : ".pdf,.docx" } }
    }

### <a name="exclude-blobs-with-specific-file-extensions"></a>Exclusion d’objets blob avec des extensions de fichier spécifiques
Vous pouvez exclure des objets BLOB avec des extensions de nom de fichier spécifique de l’indexation à l’aide de hello `excludedFileNameExtensions` le paramètre de configuration. valeur de Hello est une chaîne contenant une liste séparée par des virgules des extensions de fichier (avec un point de début). Par exemple, tooindex tous les objets BLOB, à l’exception de ceux de hello. PNG et. Extensions JPEG, procédez comme suit :

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "excludedFileNameExtensions" : ".png,.jpeg" } }
    }

Si les paramètres `indexedFileNameExtensions` et `excludedFileNameExtensions` sont tous deux présents, Azure Search regarde d’abord `indexedFileNameExtensions`, puis `excludedFileNameExtensions`. Cela signifie que si hello même extension de fichier est présente dans les deux listes, il sera exclu de l’indexation.

### <a name="dealing-with-unsupported-content-types"></a>Gestion de types de contenu non pris en charge

Par défaut, indexeur d’objet blob hello s’arrête dès qu’il rencontre un objet blob avec un type de contenu non pris en charge (par exemple, une image). Vous pouvez utiliser naturellement hello `excludedFileNameExtensions` paramètre tooskip certains types de contenu. Toutefois, vous devrez peut-être tooindex BLOB sans connaître à l’avance de tous les types de contenu possibles hello. toocontinue indexation lorsqu’un type de contenu non pris en charge est rencontré, définissez hello `failOnUnsupportedContentType` le paramètre de configuration trop`false`:

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "failOnUnsupportedContentType" : false } }
    }

### <a name="ignoring-parsing-errors"></a>Erreurs d’analyse ignorées

La logique d’extraction des documents Azure Search n’est pas parfaite et échoue parfois tooparse des documents d’un type de contenu pris en charge, tel que. DOCX ou. FICHIER PDF. Si vous ne souhaitez pas hello toointerrupt l’indexation dans ce cas, la valeur hello `maxFailedItems` et `maxFailedItemsPerBatch` valeurs de configuration paramètres toosome raisonnable. Par exemple :

    {
      ... other parts of indexer definition
      "parameters" : { "maxFailedItems" : 10, "maxFailedItemsPerBatch" : 10 }
    }

<a name="PartsOfBlobToIndex"></a>
## <a name="controlling-which-parts-of-hello-blob-are-indexed"></a>Contrôler les parties de l’objet blob de hello sont indexés.

Vous pouvez contrôler quelles parties d’objets BLOB de hello sont indexées à l’aide de hello `dataToExtract` le paramètre de configuration. Elle peut prendre hello valeurs suivantes :

* `storageMetadata`-Spécifie que seules hello [spécifié par l’utilisateur les métadonnées et propriétés de l’objet blob standard](../storage/blobs/storage-properties-metadata.md) sont indexés.
* `allMetadata`-Spécifie que les métadonnées de stockage et hello [métadonnées spécifiques du type de contenu](#ContentSpecificMetadata) extraites à partir de l’objet blob de hello contenu sont indexés.
* `contentAndMetadata`-Spécifie que toutes les métadonnées et du contenu textuel extraites à partir de l’objet blob de hello sont indexées. Il s’agit de valeur par défaut de hello.

Par exemple, les métadonnées de stockage uniquement hello tooindex, utilisez :

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "dataToExtract" : "storageMetadata" } }
    }

### <a name="using-blob-metadata-toocontrol-how-blobs-are-indexed"></a>À l’aide de toocontrol de métadonnées blob comment les objets BLOB est indexés

paramètres de configuration Hello décrites ci-dessus s’appliquent tooall BLOB. Vous pouvez être amené toocontrol comment *les objets BLOB individuels* sont indexés. Ce faire, vous pouvez ajoutant hello suit les propriétés de métadonnées et les valeurs d’objets blob :

| Nom de la propriété | Valeur de la propriété | Explication |
| --- | --- | --- |
| AzureSearch_Skip |"true" |Fait en sorte que les objets blob hello blob indexeur toocompletely skip hello. Ni l’extraction des métadonnées, ni l’extraction de contenu n’est tentée. Cela est utile lorsqu’un objet blob particulier de façon répétée et interrompt le processus d’indexation hello. |
| AzureSearch_SkipContent |"true" |Cela équivaut à `"dataToExtract" : "allMetadata"` définition décrit [ci-dessus](#PartsOfBlobToIndex) tooa étendue des blob particulier. |

## <a name="incremental-indexing-and-deletion-detection"></a>Indexation incrémentielle et détection des suppressions
Lorsque vous configurez un toorun d’indexeur blob selon une planification, il réindexe uniquement hello modifié des objets BLOB, comme déterminé par l’objet blob de hello `LastModified` timestamp.

> [!NOTE]
> Vous n’avez pas une stratégie de détection de modification toospecify : indexation incrémentielle est automatiquement activée.

documents de suppression toosupport, utilisez une approche de « suppression réversible ». Si vous supprimez des objets BLOB de hello ferme, documents correspondants ne seront pas supprimés à partir de l’index de recherche hello. Au lieu de cela, utilisez hello comme suit :  

1. Ajouter un tooAzure tooindicate d’objets blob de métadonnées personnalisées propriété toohello recherche qu’il est logiquement supprimé
2. Configurer une stratégie de détection de suppression réversible sur la source de données hello
3. Une fois que l’indexeur de hello a traité les blob hello (comme indiqué par l’état de l’indexeur hello API), vous pouvez supprimer physiquement les blob hello

Par exemple, hello suivant stratégie considère un toobe blob supprimé s’il a une propriété de métadonnées `IsDeleted` avec la valeur de hello `true`:

    PUT https://[service name].search.windows.net/datasources/blob-datasource?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "<your storage connection string>" },
        "container" : { "name" : "my-container", "query" : "my-folder" },
        "dataDeletionDetectionPolicy" : {
            "@odata.type" :"#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",     
            "softDeleteColumnName" : "IsDeleted",
            "softDeleteMarkerValue" : "true"
        }
    }   

## <a name="indexing-large-datasets"></a>Indexation de jeux de données volumineux

L’indexation d’objets blob peut être un processus long. Dans les cas où vous avez des millions d’objets BLOB tooindex, vous pouvez accélérer l’indexation par le partitionnement des données et à l’aide de plusieurs indexeurs tooprocess hello de données en parallèle. Par exemple, vous pouvez effectuer la configuration suivante :

- Partitionnez les données dans plusieurs conteneurs d’objets blob ou des dossiers virtuels.
- Configurez plusieurs sources de données Recherche Azure, une par conteneur ou dossier. dossier d’objets blob toopoint tooa, utilisez hello `query` paramètre :

    ```
    {
        "name" : "blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "<your storage connection string>" },
        "container" : { "name" : "my-container", "query" : "my-folder" }
    }
    ```

- Créez un indexeur correspondant pour chaque source de données. Tous les hello indexeurs peuvent point toohello même index de recherche cible.  

- Une unité de recherche dans votre service peut exécuter un indexeur à tout moment donné. La création de plusieurs indexeurs comme décrit ci-dessus est utile uniquement s’ils s’exécutent en parallèle. toorun plusieurs indexeurs en parallèle, faire évoluer votre service de recherche en créant un nombre approprié de partitions et réplicas. Par exemple, si votre service de recherche a 6 unités de recherche (par exemple, les réplicas de 2 partitions x 3), puis 6 indexeurs peuvent exécuter simultanément, ce qui entraîne une augmentation avec une débit d’indexation hello. toolearn en savoir plus sur la mise à l’échelle et la planification de la capacité, consultez [mettre à l’échelle des niveaux de ressources pour les requêtes et indexation des charges de travail dans Azure Search](search-capacity-planning.md).

## <a name="indexing-documents-along-with-related-data"></a>Indexation de documents et des données associées

Vous souhaiterez peut-être trop « assembler « documents provenant de plusieurs sources dans votre index. Par exemple, vous voudrez texte toomerge à partir d’objets BLOB avec d’autres métadonnées stockées dans la base de données Cosmos. Vous pouvez même utiliser hello API d’indexation par émission de données avec plusieurs indexeurs accumuler trop de recherche de documents à partir de plusieurs parties. 

Pour cette toowork, tous les indexeurs et autres composants doivent tooagree sur la clé de document hello. Pour obtenir une procédure détaillée, consultez l’article externe : [Associer des documents à d’autres données dans Recherche Azure](http://blog.lytzen.name/2017/01/combine-documents-with-other-data-in.html)

<a name="IndexingPlainText"></a>
## <a name="indexing-plain-text"></a>Indexation en texte brut 

Si tous vos objets BLOB contiennent le texte brut dans hello même encodage, vous pouvez améliorer considérablement les performances d’indexation à l’aide de **mode d’analyse de texte**. texte toouse hello du jeu, le mode d’analyse `parsingMode` propriété de configuration trop`text`:

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "parsingMode" : "text" } }
    }

Par défaut, hello `UTF-8` encodage est utilisé par défaut. toospecify un encodage différent, utilisez hello `encoding` propriété de configuration : 

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "parsingMode" : "text", "encoding" : "windows-1252" } }
    }


<a name="ContentSpecificMetadata"></a>
## <a name="content-type-specific-metadata-properties"></a>Propriétés de métadonnées propres au type de contenu
Bonjour tableau suivant résume le traitement effectué pour chaque format de document et décrit les propriétés de métadonnées hello extraites par Azure Search.

| Format de document/type de contenu | Propriétés de métadonnées propres au type de contenu | Détails du traitement |
| --- | --- | --- |
| HTML (`text/html`) |`metadata_content_encoding`<br/>`metadata_content_type`<br/>`metadata_language`<br/>`metadata_description`<br/>`metadata_keywords`<br/>`metadata_title` |Suppression du balisage HTML et extraction du texte |
| PDF (`application/pdf`) |`metadata_content_type`<br/>`metadata_language`<br/>`metadata_author`<br/>`metadata_title` |Extraction du texte, y compris les documents incorporés (à l’exclusion des images) |
| DOCX (application/vnd.openxmlformats-officedocument.wordprocessingml.document) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_character_count`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_page_count`<br/>`metadata_word_count` |Extraction du texte, y compris les documents incorporés |
| DOC (application/msword) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_character_count`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_page_count`<br/>`metadata_word_count` |Extraction du texte, y compris les documents incorporés |
| XLSX (application/vnd.openxmlformats-officedocument.spreadsheetml.sheet) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_creation_date`<br/>`metadata_last_modified` |Extraction du texte, y compris les documents incorporés |
| XLS (application/vnd.ms-excel) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_creation_date`<br/>`metadata_last_modified` |Extraction du texte, y compris les documents incorporés |
| PPTX (application/vnd.openxmlformats-officedocument.presentationml.presentation) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_slide_count`<br/>`metadata_title` |Extraction du texte, y compris les documents incorporés |
| PPT (application/vnd.ms-powerpoint) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_slide_count`<br/>`metadata_title` |Extraction du texte, y compris les documents incorporés |
| MSG (application/vnd.ms-outlook) |`metadata_content_type`<br/>`metadata_message_from`<br/>`metadata_message_to`<br/>`metadata_message_cc`<br/>`metadata_message_bcc`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_subject` |Extraction du texte, y compris les pièces jointes |
| ZIP (application/zip) |`metadata_content_type` |Extrayez le texte de tous les documents d’archive de hello |
| XML (application/xml) |`metadata_content_type`</br>`metadata_content_encoding`</br> |Suppression du balisage XML et extraction du texte |
| JSON (application/json) |`metadata_content_type`</br>`metadata_content_encoding` |Extraction du texte<br/>Remarque : Si vous avez besoin de tooextract document comportant plusieurs champs à partir d’un objet blob de JSON, consultez [JSON de l’indexation des objets BLOB](search-howto-index-json-blobs.md) pour plus d’informations |
| EML (message/rfc822) |`metadata_content_type`<br/>`metadata_message_from`<br/>`metadata_message_to`<br/>`metadata_message_cc`<br/>`metadata_creation_date`<br/>`metadata_subject` |Extraction du texte, y compris les pièces jointes |
| RTF (application/rtf) |`metadata_content_type`</br>`metadata_author`</br>`metadata_character_count`</br>`metadata_creation_date`</br>`metadata_page_count`</br>`metadata_word_count`</br> | Extraction du texte|
| Texte brut (text/plain) |`metadata_content_type`</br>`metadata_content_encoding`</br> | Extraction du texte|


## <a name="help-us-make-azure-search-better"></a>Aidez-nous à améliorer Azure Search
Si vous souhaitez nous soumettre des demandes d’ajout de fonctionnalités ou des idées d’amélioration, contactez-nous sur notre [site UserVoice](https://feedback.azure.com/forums/263029-azure-search/).
