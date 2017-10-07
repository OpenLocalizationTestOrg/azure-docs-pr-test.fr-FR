---
title: Index de recherche Azure aaaQuery | Documents Microsoft
description: "Générer une requête de recherche dans Azure search et utilisez les paramètres toofilter et tri recherche résultats de la recherche."
services: search
manager: jhubbard
documentationcenter: 
author: ashmaka
ms.assetid: 69205d7a-363f-4b92-a53f-6ca818a3d2c7
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 04/26/2017
ms.author: ashmaka
ms.openlocfilehash: 4a5ffffe179695fc09446760e21a738dd36c29b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="query-your-azure-search-index"></a>Interroger votre index Azure Search
> [!div class="op_single_selector"]
> * [Vue d'ensemble](search-query-overview.md)
> * [Portail](search-explorer.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
> 
> 

Lors de l’envoi de demandes de recherche tooAzure recherche, il existe un nombre de paramètres qui peuvent être spécifiées en même temps que les mots hello réel qui sont tapées dans la zone de recherche hello de votre application. Ces paramètres de requête vous permettent de tooachieve un contrôle plus approfondie de hello [expérience de recherche en texte intégral](search-lucene-query-architecture.md).

Voici une liste qui contient des explications des utilisations courantes des paramètres de requête hello dans Azure Search. Pour la prise en charge complète des paramètres de requête et leur comportement, consultez hello détaillées des pages pour hello [API REST](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) et [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters#microsoft_azure_search_models_searchparameters#properties_summary).

## <a name="types-of-queries"></a>Types de requête
Azure Search offre de nombreuses options toocreate extrêmement puissante requêtes. Hello deux principaux types de requête que vous allez utiliser sont `search` et `filter`. A `search` requête recherche pour un ou plusieurs termes dans tous les *recherche* champs dans votre index et fonctionne de manière hello un moteur de recherche comme Google ou Bing toowork souhaitées. Une requête `filter` permet d’évaluer une expression booléenne dans tous les champs *filtrables* d’un index. Contrairement aux `search` requêtes, `filter` contenu exact de hello d’un champ, ce qui signifie qu’ils respectent la casse pour les champs string correspondre aux requêtes.

Vous pouvez utiliser des recherches et des filtres conjointement ou séparément. Si vous les utilisez ensemble, hello est appliqué le premier index entier toohello, puis recherche de hello est effectuée sur les résultats du filtre de hello hello. Filtres peuvent être par conséquent, les performances des requêtes tooimprove une technique utile, car elles réduisent ensemble hello des documents hello tooprocess de besoins de requête de recherche.

syntaxe Hello pour les expressions de filtre est un sous-ensemble de hello [langue de filtre OData](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search). Pour les requêtes de recherche, vous pouvez utiliser soit hello [une syntaxe simplifiée](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search) ou hello [syntaxe de requête Lucene](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search) qui sont décrites ci-dessous.

### <a name="simple-query-syntax"></a>Syntaxe de requête simple
Hello [syntaxe de requête simple](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search) est hello langage de requête par défaut utilisé dans Azure Search. syntaxe de requête simple Hello prend en charge un nombre d’opérateurs de recherche courants notamment hello AND, OR, pas une expression, suffixe et les opérateurs de priorité.

### <a name="lucene-query-syntax"></a>syntaxe de requête Lucene
Hello [syntaxe de requête Lucene](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search) vous permet de hello toouse largement adopté et langage de requête expressif développée dans le cadre de [Apache Lucene](https://lucene.apache.org/core/4_10_2/queryparser/org/apache/lucene/queryparser/classic/package-summary.html).

À l’aide de cette syntaxe de requête vous permet de tooeasily atteindre hello suivant des fonctionnalités : [les requêtes de portée d’un champ](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_fields), [recherche floue](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_fuzzy), [recherche de proximité](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_proximity), [ renforcement de terme](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_termboost), [recherche d’expression régulière](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_regex), [recherche par caractères génériques](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_wildcard), [notions de base de syntaxe](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_syntax), et [à l’aide des requêtes opérateurs booléens](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_boolean).

## <a name="ordering-results"></a>Classement des résultats
Lors de la réception des résultats d’une requête de recherche, vous pouvez demander qu’Azure Search fait Office de résultats hello classés par valeur dans un champ spécifique. Par défaut, Azure Search trie les résultats de la recherche hello classement hello du score de recherche de chaque document, qui est dérivé de [TF-IDF](https://en.wikipedia.org/wiki/Tf%E2%80%93idf).

Si vous souhaitez tooreturn Azure Search vos résultats classés par une valeur différente de score de recherche hello, vous pouvez utiliser hello `orderby` paramètre de recherche. Vous pouvez spécifier la valeur hello hello `orderby` tooinclude le champ de paramètre des noms et appelle toohello [ `geo.distance()` fonction](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search) pour les valeurs géospatiales. Chaque expression peut être suivie `asc` tooindicate que les résultats sont demandés dans l’ordre croissant, et `desc` tooindicate que les résultats sont demandés dans l’ordre décroissant. classement par défaut du Hello par ordre croissant.

## <a name="paging"></a>Pagination
Azure Search rend facile tooimplement la pagination des résultats de recherche. À l’aide de hello `top` et `skip` paramètres, vous pouvez facilement émettre des requêtes de recherche qui vous tooreceive hello ensemble des résultats de la recherche en sous-ensembles gérables et ordonnés, qui permettent de facilement pratiques de l’interface utilisateur de recherche pertinents. Lors de la réception de ces sous-ensembles plus petits de résultats, vous pouvez également recevoir compte hello de documents dans l’ensemble total de hello des résultats de recherche.

Plus d’informations sur la pagination des résultats de recherche dans l’article de hello [affichage des résultats de recherche de toopage dans Azure Search](search-pagination-page-layout.md).

## <a name="hit-highlighting"></a>Mise en surbrillance des correspondances
Dans Azure Search, mettant en évidence la partie exacte de hello des résultats de recherche qui correspondent à la requête de recherche hello est facilitée par l’utilisation hello `highlight`, `highlightPreTag`, et `highlightPostTag` paramètres. Vous pouvez spécifier quels *recherche* champs doivent avoir leur mise en correspondance texte souligné, ainsi que la spécification hello exacte chaîne balises tooappend toohello début et fin de hello correspondance du texte qu’Azure Search retourne.

## <a name="try-out-query-syntax"></a>Essais de syntaxe de requête

différences de syntaxe Hello meilleure manière toounderstand est en soumettant des requêtes et examinez les résultats.

+ Utilisez [rechercher dans l’Explorateur](search-explorer.md) Bonjour portail Azure. En déployant [index d’exemple hello](search-get-started-portal.md), vous pouvez interroger l’index de hello en quelques minutes à l’aide des outils dans le portail de hello.

+ Utilisez [Fiddler](search-fiddler.md) ou Chrome Postman toosubmit requêtes tooan index que vous avez téléchargé le service de recherche tooyour. Les deux outils prennent en charge le point de terminaison HTTP REST appelle tooan. 
