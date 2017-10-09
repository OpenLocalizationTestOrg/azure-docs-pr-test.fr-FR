---
title: "les exemples de requête aaaLucene pour Azure Search | Documents Microsoft"
description: "Syntaxe de requête Lucene pour la recherche partielle, la recherche de proximité, l’amélioration de termes, la recherche d’expressions régulières et la recherche par caractères génériques."
services: search
documentationcenter: 
author: LiamCa
manager: pablocas
editor: 
tags: Lucene query analyzer syntax
ms.assetid: 147f360d-a5ce-4d7b-a909-c8b65bfb748c
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/21/2017
ms.author: liamca
ms.openlocfilehash: d859cf697ef9485a49e9e0591b68e812ffa55f1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="lucene-query-syntax-examples-for-building-queries-in-azure-search"></a>Exemples de syntaxe de requête Lucene pour créer des requêtes dans Azure Search
Lors de la construction des requêtes pour Azure Search, vous pouvez utiliser par défaut hello [syntaxe de requête simple](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) ou hello [Lucene Analyseur de requêtes dans Azure Search](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search). Hello Analyseur de requêtes Lucene prend en charge les constructions de requête plus complexes, telles que les requêtes de portée d’un champ de recherche floue, recherche de proximité, terme boosting et recherche d’expression régulière.

Dans cet article, vous pouvez parcourir des exemples décrivant les opérations de requête disponibles lorsque vous utilisez la syntaxe complète de hello.

## <a name="viewing-hello-examples-in-jsfiddle"></a>Affichage des exemples de hello dans JSFiddle

Tous les exemples hello dans cet article sont des requêtes exécutables qui s’exécutent sur un index de recherche préchargé dans [JSFiddle](https://jsfiddle.net), un éditeur de code en ligne pour le test de script et HTML. 

toorun, avec le bouton droit sur hello requête exemple URL tooopen JSFiddle dans une fenêtre de navigateur distincte.

> [!NOTE]
> les exemples suivants Hello exploitent un index de recherche composé des tâches disponibles sur un jeu de données fournie par hello [ville de New York OpenData](https://nycopendata.socrata.com/) initiative. Ces données ne doivent pas être considérées comme étant à jour ou complètes. index de Hello est sur un service de bac à sable fourni par Microsoft. Il est inutile un abonnement Azure ou l’Azure Search tootry ces requêtes.
>


## <a name="how-tooinvoke-full-lucene-parsing"></a>Comment tooinvoke complète Lucene l’analyse.

Tous les exemples hello dans cet article spécifient hello **queryType = complet** paramètre, en indiquant cette syntaxe complète de hello, gérée par hello Analyseur de requêtes Lucene de recherche. 

**Exemple 1** : hello avec le bouton suivant tooopen d’extrait de code de requête dans une nouvelle fenêtre de navigateur page qui charge JSFiddle et s’exécute hello requête :

* [&amp;queryType=full&amp;search=*](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26searchFields=business_title%26$select=business_title%26queryType=full%26search=*)

Dans la nouvelle fenêtre de navigateur hello source JavaScript de hello et de sortie HTML sont présentées côte à côte. script de Hello fait référence à une requête complète (pas seulement hello extrait de code, comme indiqué dans le lien de hello). requête complète et Hello est indiqué dans les URL pour chaque exemple hello. 

Cette requête retourne des documents à partir de notre index New York City Jobs (nycjobs, chargé sur un service de bac à sable (sandbox)). Par souci de concision, les requêtes hello spécifie uniquement les titres d’entreprise sont retournées. requête sous-jacente de Hello complète est la suivante :

    http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26searchFields=business_title%26$select=business_title%26queryType=full%26search=*

Hello **searchFields** paramètre restreint le champ titre de hello recherche toojust hello entreprise. Hello **queryType** est défini trop**complète**, qui indique le hello Azure Search toouse Analyseur de requêtes Lucene pour cette requête.

> [!NOTE]
> Pour des informations sur le traitement des requêtes, consultez [Fonctionnement de la recherche en texte intégral dans Recherche Azure](search-lucene-query-architecture.md). Pour plus d’informations sur les paramètres de recherche, consultez [Rechercher des documents (API REST du service Recherche Azure)](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).
>

### <a name="fielded-query-operation"></a>Opération de requête portant sur un champ
Vous pouvez modifier les exemples hello dans cet article en spécifiant un **fieldname:searchterm** construction toodefine une opération de requête saisies, où champ de hello est un mot unique, et terme de recherche hello est également un mot ou une expression, Si vous le souhaitez, avec des opérateurs booléens. Certains exemples hello suivants :

* business_title:(senior NOT junior)
* state:("New York" AND "New Jersey")

Si vous souhaitez que les deux toobe chaînes évaluée comme une entité unique, comme dans ce cas, recherchez les deux villes distinctes dans le champ d’emplacement hello, être tooput que plusieurs chaînes entre guillemets. En outre, assurez-vous d’opérateur de hello en majuscules comme NOT et and.

champ Hello dans **fieldname:searchterm** doit être un champ de recherche. Pour plus d’informations sur l’utilisation des attributs d’index dans les définitions de champs, consultez [Créer un index (API REST du service Azure Search)](https://docs.microsoft.com/rest/api/searchservice/create-index) .

**Exemple 2** --extrait de code de cette requête recherche les livres par hello terme senior dans celles-ci, mais pas junior requête suivante de hello avec le bouton :

* [&amp;queryType=full&amp;search= business_title:senior NOT junior](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:senior+NOT+junior)

## <a name="fuzzy-search-example"></a>Exemple de recherche partielle
Une recherche partielle recherche des correspondances dans les termes qui ont une construction similaire. D’après la [documentation Lucene](https://lucene.apache.org/core/4_10_2/queryparser/org/apache/lucene/queryparser/classic/package-summary.html), les recherches partielles sont basées sur la [Distance Levenshtein-Damerau](https://en.wikipedia.org/wiki/Damerau%e2%80%93Levenshtein_distance).

toodo une recherche floue, ajouter un tilde de hello « ~ » symbole à fin hello d’un mot unique avec un paramètre optionnel, une valeur comprise entre 0 et 2, qui spécifie la distance de modification hello. Par exemple, "blue~" ou "blue~1" retournent blue, blues et glue.

**Exemple 3** --suivant de hello avec le bouton requête extrait de code. Cette requête recherche des tâches avec l’association du terme hello (où il est mal orthographié) :

* [&amp;queryType=full&amp;search= business_title:asosiate~](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:asosiate~)

> [!Note]
> Les requêtes partielles ne sont pas [analysées](https://docs.microsoft.com/azure/search/search-lucene-query-architecture#stage-2-lexical-analysis), ce qui peut être surprenant si vous vous attendez à une racinisation ou lemmatisation. L’analyse lexicale est effectuée uniquement sur des termes complets (requête sur un terme ou une expression). Termes incomplet (requête de préfixe, les requêtes génériques, requête d’expression régulière, requête floue), les types de requêtes sont ajoutées directement toohello arbre de requêtes, en ignorant la phase d’analyse hello. Hello que transformation effectuée sur les termes de requête incomplète est minuscules.
>

## <a name="proximity-search-example"></a>Exemple Recherche de proximité
Recherches de proximité sont des termes utilisés toofind qui sont proches dans un document. Insérer un tilde « ~ » symbole au hello phrase de fin d’une suivi par numéro de hello de mots qui créent des limites de proximité hello. Par exemple, « aéroport hôtel » ~ 5 constaterez hôtel de termes hello et aéroport dans 5 mots dans un document.

**Exemple 4** --requête hello de clic droit. Rechercher des tâches avec le terme hello « analyste » où il est séparé par non plus d’un mot :

* [&amp;queryType=full&amp;search=business_title:"senior analyst"~1](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:%22senior%20analyst%22~1)

**Exemple 5** --essayez à nouveau en supprimant les mots hello entre le terme hello « analyste ».

* [&amp;queryType=full&amp;search=business_title:"senior analyst"~0](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:%22senior%20analyst%22~0)

## <a name="term-boosting-examples"></a>Exemple Promotion de termes
Renforcement de terme fait référence à tooranking un document plus élevé si elle contient hello augmentés terme, toodocuments relatif qui ne contiennent pas le terme de hello. À ne pas confondre avec les profils de score qui promeuvent certains champs, plutôt que des termes spécifiques. Hello exemple suivant permet d’illustrer les différences de hello.

Envisagez correspond à un profil de score qui augmente dans un champ particulier, tel que **genre** dans l’exemple de musicstoreindex hello. Renforcement de terme peut être utilisé toofurther renforcement certains termes de recherche plus élevée. Par exemple, « rock ^ 2 électronique » augmentera les documents qui contiennent des termes de recherche hello Bonjour **genre** champ supérieur aux autres champs de recherche dans les index hello. En outre, les documents qui contiennent le terme de recherche hello « rock » seront classées supérieure hello recherche le terme « electronic » en raison de la valeur de renforcement de terme hello (2).

tooboost une condition, utilisez hello du point d’insertion, « ^ », symbole avec un facteur (nombre) à fin hello du terme hello vous recherchez. Hello hello facteur hello plus élevée, plus pertinente par rapport à terme de hello sera relatif tooother les termes de recherche. Par défaut, le facteur de valorisation hello est 1. Bien que le facteur hello doit être positive, il peut être inférieur à 1 (par exemple, 0,2).

**Exemple 6** --requête hello de clic droit. Rechercher des tâches avec le terme hello « analyste ordinateur » où nous voyons aucun résultat avec l’ordinateur de mots et d’analyse, mais les travaux de l’analyste sont haut hello des résultats de hello.

* [&amp;queryType=full&amp;search=business_title:computer analyst](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:computer%5e2%20analyst)

**Exemple 7** --essayez de nouveau, cette fois boosting résultats avec l’ordinateur du terme hello sur analyste de terme hello si les deux mots n’existent pas.

* [&amp;queryType=full&amp;search=business_title:computer^2 analyst](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:computer%5e2%20analyst)

## <a name="regular-expression-example"></a>Exemple Expression régulière
Une recherche d’expression régulière trouve une correspondance basée sur le contenu hello entre les barres obliques « / », comme documenté dans hello [classe RegExp](http://lucene.apache.org/core/4_10_2/core/org/apache/lucene/util/automaton/RegExp.html).

**Exemple 8** --requête hello de clic droit. Rechercher des tâches par le terme hello Senior ou Junior.

* `&queryType=full&$select=business_title&search=business_title:/(Sen|Jun)ior/`

URL de Hello pour cet exemple n’est pas rendus correctement dans la page de hello. Pour résoudre ce problème, copier l’URL de hello ci-dessous et collez-le dans l’adresse URL du navigateur hello :`http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26queryType=full%26$select=business_title%26search=business_title:/(Sen|Jun)ior/)`

## <a name="wildcard-search-example"></a>Exemple Recherche par caractères génériques
Vous pouvez utiliser la syntaxe généralement reconnue pour effectuer des recherches avec plusieurs caractères génériques (\*) ou un caractère générique unique (?). Notez la requête de Lucene hello analyseur prend en charge hello de ces symboles avec un terme unique et pas une expression.

**Exemple 9** --requête hello de clic droit. Rechercher des tâches qui contiennent des hello préfixe « prog », qui comprend les titres d’entreprise avec les termes du contrat de hello de programmation et programmeur qu’il contient.

* [&amp;queryType=full&amp;$select=business_title&amp;search=business_title:prog*](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26queryType=full%26$select=business_title%26search=business_title:prog*)

Vous ne pouvez pas utiliser un signe * ou ? symbole hello premier caractère d’une recherche.

## <a name="next-steps"></a>Étapes suivantes
Essayez de spécifier hello Analyseur de requêtes Lucene dans votre code. Hello suivant liens explique comment tooset la recherche des requêtes pour .NET et hello API REST. les liens Hello utilisent une syntaxe simple hello par défaut, vous devez tooapply ce que vous avez appris à partir de cette hello toospecify de l’article **queryType**.

* [Interroger votre Index de recherche Azure à l’aide de hello .NET SDK](search-query-dotnet.md)
* [Interroger votre Index de recherche Azure à l’aide des API REST de hello](search-query-rest-api.md)

## <a name="see-also"></a>Voir aussi

 [Fonctionnement de la recherche en texte intégral dans la Recherche Azure](search-lucene-query-architecture.md)