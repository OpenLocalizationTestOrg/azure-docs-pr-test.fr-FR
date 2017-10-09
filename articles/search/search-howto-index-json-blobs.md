---
title: "aaaIndexing JSON d’objets BLOB avec un indexeur d’objet blob Azure Search"
description: "Indexation d’objets blob JSON avec l’indexeur d’objets blob Azure Search"
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 57e32e51-9286-46da-9d59-31884650ba99
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/10/2017
ms.author: eugenesh
ms.openlocfilehash: 269968714358cd40ea66863b4dbb97766e1d77e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-json-blobs-with-azure-search-blob-indexer"></a>Indexation d’objets blob JSON avec l’indexeur d’objets blob Azure Search
Cet article explique comment tooconfigure Azure Search blob indexeur tooextract structurés contenu à partir d’objets BLOB contenant JSON.

## <a name="scenarios"></a>Scénarios
Par défaut, [l’indexeur d’objets blob Azure Search](search-howto-indexing-azure-blob-storage.md) analyse les objets blob JSON comme un bloc de texte unique. Souvent, vous souhaitez la structure de hello toopreserve de vos documents JSON. Par exemple, prenons le document JSON de hello

    {
        "article" : {
             "text" : "A hopefully useful article explaining how tooparse JSON blobs",
            "datePublished" : "2016-04-13"
            "tags" : [ "search", "storage", "howto" ]    
        }
    }

Vous souhaiterez peut-être tooparse dans une recherche d’Azure avec « texte », « datePublished » et « balises » des champs de document.

Vous pouvez également lorsque vos objets BLOB contiennent un **tableau d’objets JSON**, vous souhaiterez peut-être chaque élément de hello tableau toobecome un document Azure Search distinct. Par exemple, un objet blob avec ce JSON :  

    [
        { "id" : "1", "text" : "example 1" },
        { "id" : "2", "text" : "example 2" },
        { "id" : "3", "text" : "example 3" }
    ]

Vous pouvez remplir l’index Recherche Azure avec trois documents distincts, chacun avec des champs « id » et « text ».

> [!IMPORTANT]
> tableau JSON de Hello fonctionnalité d’analyse est actuellement en version préliminaire. Il est disponible uniquement dans l’API REST de hello à l’aide de la version **2015-02-28-Preview**. N’oubliez pas que les API d’évaluation sont destinées à être utilisées à des fins de test et d’évaluation, et non dans les environnements de production.
>
>

## <a name="setting-up-json-indexing"></a>Configuration de l’indexation JSON
L’indexation des objets BLOB JSON est extraction de document standard toohello similaire. Commencez par créer la source de données hello exactement comme vous le feriez normalement : 

    POST https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "my-blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>;" },
        "container" : { "name" : "my-container", "query" : "optional, my-folder" }
    }   

Puis créer des index de recherche hello cible si vous n’en avez pas encore. 

Pour finir de créer un indexeur et de définir hello `parsingMode` paramètre trop`json` (tooindex chaque objet blob en tant qu’un seul document) ou `jsonArray` (si vos objets BLOB contiennent des tableaux JSON, et vous avez besoin de chaque élément d’un toobe tableau traité comme un document distinct) :

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "my-json-indexer",
      "dataSourceName" : "my-blob-datasource",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" },
      "parameters" : { "configuration" : { "parsingMode" : "json" } }
    }

Si nécessaire, utilisez **champ mappages** toopick hello propriétés de hello source JSON document utilisé toopopulate votre index de recherche cible, comme indiqué dans la section suivante de hello.

> [!IMPORTANT]
> Lorsque vous utilisez le mode d’analyse `json` ou `jsonArray`, Recherche Azure suppose que tous les objets blob dans votre source de données contiennent JSON. Si vous avez besoin de toosupport un mélange de JSON et non-JSON des objets BLOB Bonjour même source de données, nous dire sur [notre site UserVoice](https://feedback.azure.com/forums/263029-azure-search).
>
>

## <a name="using-field-mappings-toobuild-search-documents"></a>À l’aide du champ mappages toobuild recherche de documents
Actuellement, Azure Search ne peut pas indexer des documents JSON arbitraires directement, car il ne prend en charge que les types de données primitifs, les tableaux de chaînes et les points GeoJSON. Toutefois, vous pouvez utiliser **champ mappages** toopick des parties de votre JSON de document et « finesse » dans les champs de niveau supérieur du document de recherche hello. toolearn relatives aux principes élémentaires de mappages de champ, consultez [pont les mappages de champs d’indexeur Azure Search différences hello entre les sources de données et les index de recherche](search-indexer-field-mappings.md).

Fidéliser tooour exemple de document JSON :

    {
        "article" : {
             "text" : "A hopefully useful article explaining how tooparse JSON blobs",
            "datePublished" : "2016-04-13"
            "tags" : [ "search", "storage", "howto" ]    
        }
    }

Supposons que vous avez un index de recherche avec hello suivant champs : `text` de type `Edm.String`, `date` de type `Edm.DateTimeOffset`, et `tags` de type `Collection(Edm.String)`. toomap votre JSON dans hello souhaité forme, utilisez hello suivant des mappages de champs :

    "fieldMappings" : [
        { "sourceFieldName" : "/article/text", "targetFieldName" : "text" },
        { "sourceFieldName" : "/article/datePublished", "targetFieldName" : "date" },
        { "sourceFieldName" : "/article/tags", "targetFieldName" : "tags" }
      ]

Hello des noms de champ source dans les mappages de hello sont spécifiés à l’aide de hello [JSON pointeur](http://tools.ietf.org/html/rfc6901) notation. Vous démarrez avec une racine de toohello toorefer barre oblique de votre document JSON, puis choisissez la propriété hello souhaitée (au niveau arbitraire d’imbrication) à l’aide du chemin d’accès séparés par des barres obliques vers l’avant.

Vous pouvez également faire référence à des éléments de tableau tooindividual à l’aide d’un index de base zéro. Par exemple, toopick hello premier élément de matrice « tags » hello hello au-dessus de l’exemple, utilisez un mappage de champs comme suit :

    { "sourceFieldName" : "/article/tags/0", "targetFieldName" : "firstTag" }

> [!NOTE]
> Si un nom de champ source dans un chemin d’accès du mappage de champ fait référence de propriété tooa qui n’existe pas dans JSON, ce mappage est ignoré sans erreur. Cela nous permet de prendre en charge les documents avec un schéma différent (cas fréquent). Étant donné qu’aucune validation, vous devez tooavoid fautes de frappe soins tootake dans la spécification de mappage de champ.
>
>

Si vos documents JSON ne contiennent que des propriétés de niveau supérieur, il se peut que vous n’ayez pas besoin d’aucun mappage de champ. Par exemple, si votre JSON ressemble à ce, propriétés de niveau supérieur hello « texte », « datePublished » et « balises » mappe directement toohello les champs correspondants dans l’index de recherche hello :

    {
       "text" : "A hopefully useful article explaining how tooparse JSON blobs",
       "datePublished" : "2016-04-13"
       "tags" : [ "search", "storage", "howto" ]    
     }

Voici une charge utile d’indexeur complète avec les mappages de champs :

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "my-json-indexer",
      "dataSourceName" : "my-blob-datasource",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" },
      "parameters" : { "configuration" : { "parsingMode" : "json" } },
      "fieldMappings" : [
        { "sourceFieldName" : "/article/text", "targetFieldName" : "text" },
        { "sourceFieldName" : "/article/datePublished", "targetFieldName" : "date" },
        { "sourceFieldName" : "/article/tags", "targetFieldName" : "tags" }
        ]
    }

## <a name="indexing-nested-json-arrays"></a>Indexation de tableaux JSON imbriqués
Que se passe-t-il si vous souhaitez tooindex un tableau d’objets JSON, mais ce tableau est imbriqué quelque part dans le document de hello ? Vous pouvez choisir de dont la propriété contient le tableau de hello à l’aide de hello `documentRoot` propriété de configuration. Par exemple, si vos objets blob ressemblent à ceci :

    {
        "level1" : {
            "level2" : [
                { "id" : "1", "text" : "Use hello documentRoot property" },
                { "id" : "2", "text" : "toopluck hello array you want tooindex" },
                { "id" : "3", "text" : "even if it's nested inside hello document" }  
            ]
        }
    }

utiliser ce tableau de hello tooindex configuration contenu dans hello `level2` propriété :

    {
        "name" : "my-json-array-indexer",
        ... other indexer properties
        "parameters" : { "configuration" : { "parsingMode" : "jsonArray", "documentRoot" : "/level1/level2" } }
    }

## <a name="help-us-make-azure-search-better"></a>Aidez-nous à améliorer Azure Search
Si vous avez des demandes de fonctionnalités ou des idées pour les améliorations, atteindre toous sur notre [site UserVoice](https://feedback.azure.com/forums/263029-azure-search/).
