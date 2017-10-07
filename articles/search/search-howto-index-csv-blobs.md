---
title: "aaaIndexing CSV des objets BLOB avec un indexeur d’objet blob Azure Search | Documents Microsoft"
description: "Découvrez comment tooindex CSV des objets BLOB Azure Search"
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: ed3c9cff-1946-4af2-a05a-5e0b3d61eb25
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 12/15/2016
ms.author: eugenesh
ms.openlocfilehash: f2b1ce824e62c5b3f6155c6e88887897cf1a8eae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-csv-blobs-with-azure-search-blob-indexer"></a>Indexation d’objets blob CSV avec l’indexeur d’objets blob Azure Search
Par défaut, l’ [indexeur d’objets blob Azure Search](search-howto-indexing-azure-blob-storage.md) analyse les objets blob de texte délimité comme un bloc de texte unique. Toutefois, avec des objets BLOB contenant des données CSV, il est souvent nécessaire tootreat chaque ligne dans l’objet blob de hello comme un document distinct. Par exemple, compte tenu de hello suivant texte séparé par des : 

    id, datePublished, tags
    1, 2016-01-12, "azure-search,azure,cloud" 
    2, 2016-07-07, "cloud,mobile" 

Vous souhaiterez peut-être tooparse il en 2 documents, chacun contenant les champs « balises », « datePublished » et « id ».

Dans cet article, vous allez apprendre comment tooparse CSV des objets BLOB avec un indexeur d’objet blob Azure Search. 

> [!IMPORTANT]
> Pour l’instant, cette fonctionnalité n’existe qu’en version préliminaire. Il est disponible uniquement dans l’API REST de hello à l’aide de la version **2015-02-28-Preview**. N’oubliez pas que les API d’évaluation sont destinées à être utilisées à des fins de test et d’évaluation, et non dans les environnements de production. 
> 
> 

## <a name="setting-up-csv-indexing"></a>Configuration de l’indexation CSV
objets BLOB de volume partagé de cluster tooindex, créer ou mettre à jour une définition d’indexeur hello `delimitedText` mode d’analyse :  

    {
      "name" : "my-csv-indexer",
      ... other indexer properties
      "parameters" : { "configuration" : { "parsingMode" : "delimitedText", "firstLineContainsHeaders" : true } }
    }

Pour plus d’informations sur hello créer des API indexeur, l’extraction [créer un indexeur](search-api-indexers-2015-02-28-preview.md#create-indexer).

`firstLineContainsHeaders`Indique que hello première (non vide) ligne de chaque objet blob contient des en-têtes.
Si les objets BLOB ne contiennent pas une ligne d’en-tête initiale, les en-têtes de hello doivent être spécifiés dans la configuration d’indexeur hello : 

    "parameters" : { "configuration" : { "parsingMode" : "delimitedText", "delimitedTextHeaders" : "id,datePublished,tags" } } 

Actuellement, l’encodage UTF-8 de hello uniquement est pris en charge. En outre, hello uniquement les virgules `','` caractère est pris en charge comme délimiteur de hello. Si vous devez prendre en charge d’autres formats ou délimiteurs, faites-le nous savoir sur [notre site UserVoice](https://feedback.azure.com/forums/263029-azure-search).

> [!IMPORTANT]
> Lorsque vous utilisez Azure Search, le mode d’analyse de texte hello délimité suppose que tous les objets BLOB dans votre source de données sera CSV. Si vous avez besoin de toosupport un mélange de volumes partagés de cluster et non-CSV des objets BLOB Bonjour même source de données, faites-le nous savoir sur [notre site UserVoice](https://feedback.azure.com/forums/263029-azure-search).
> 
> 

## <a name="request-examples"></a>Exemples de requête
Cette mise à tous les ensemble, Voici des exemples de charge utile complète de hello. 

Source de données : 

    POST https://[service name].search.windows.net/datasources?api-version=2015-02-28-Preview
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "my-blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>;" },
        "container" : { "name" : "my-container", "query" : "<optional, my-folder>" }
    }   

Indexeur :

    POST https://[service name].search.windows.net/indexers?api-version=2015-02-28-Preview
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "my-csv-indexer",
      "dataSourceName" : "my-blob-datasource",
      "targetIndexName" : "my-target-index",
      "parameters" : { "configuration" : { "parsingMode" : "delimitedText", "delimitedTextHeaders" : "id,datePublished,tags" } }
    }

## <a name="help-us-make-azure-search-better"></a>Aidez-nous à améliorer Azure Search
Si vous avez des demandes de fonctionnalités ou des idées pour les améliorations, veuillez contacter toous sur notre [site UserVoice](https://feedback.azure.com/forums/263029-azure-search/).

