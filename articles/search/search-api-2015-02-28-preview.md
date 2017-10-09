---
title: aaaAzure Search Service REST API Version 2015-02-28-Preview | Documents Microsoft
description: "L'API REST du service Azure Search version 2015-02-28-Preview comprend des fonctionnalités expérimentales telles que des analyseurs de langage naturel et des recherches moreLikeThis."
services: search
documentationcenter: na
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 3dba3bf8-9c83-42f6-82bc-04727bd11037
ms.service: search
ms.devlang: rest-api
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: search
ms.date: 05/01/2017
ms.author: brjohnst
ms.openlocfilehash: 63cb30b7f43a42552c6744ea087afea947857224
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-search-service-rest-api-version-2015-02-28-preview"></a>API REST du service Azure Search : version 2015-02-28-Preview
Cet article est la documentation de référence hello pour `api-version=2015-02-28-Preview`. Cette version préliminaire étend la version actuelle disponible de manière générale la hello, [api-version = 2015-02-28](https://msdn.microsoft.com/library/dn798935.aspx), en fournissant hello suivant les fonctionnalités expérimentales :

* `moreLikeThis`paramètre hello requête [recherche de Documents](#SearchDocs) API. Il recherche d’autres documents qui sont pertinentes tooanother des documents spécifiques.

Quelques éléments supplémentaires de hello `2015-02-28-Preview` API REST sont documentées séparément. Vous avez notamment vu les points suivants :

* [Profils de calcul de score](search-api-scoring-profiles-2015-02-28-preview.md)
* [Indexeurs](search-api-indexers-2015-02-28-preview.md)

Le service Azure Search est disponible dans plusieurs versions. Reportez-vous trop[recherche Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) pour plus d’informations.

## <a name="apis-in-this-document"></a>API dans ce document
L’API du service Azure Search prend en charge deux syntaxes d’URL pour les opérations d’API : simple et OData. Pour plus d’informations, consultez [Prise en charge d’OData (API Azure Search)](http://msdn.microsoft.com/library/azure/dn798932.aspx). Hello liste suivante présente une syntaxe simple hello.

[Création d'index](#CreateIndex)

    POST /indexes?api-version=2015-02-28-Preview

[Mise à jour d'index](#UpdateIndex)

    PUT /indexes/[index name]?api-version=2015-02-28-Preview

[Obtention d'index](#GetIndex)

    GET /indexes/[index name]?api-version=2015-02-28-Preview

[Liste des index](#ListIndexes)

    GET /indexes?api-version=2015-02-28-Preview

[Obtention de statistiques d'index](#GetIndexStats)

    GET /indexes/[index name]/stats?api-version=2015-02-28-Preview

[Tester l’analyseur](#TestAnalyzer)

    POST /indexes/[index name]/analyze?api-version=2015-02-28-Preview

[Suppression d'index](#DeleteIndex)

    DELETE /indexes/[index name]?api-version=2015-02-28-Preview

[Ajout, suppression et mise à jour de données dans un index](#AddOrUpdateDocuments)

    POST /indexes/[index name]/docs/index?api-version=2015-02-28-Preview

[Recherche dans des documents](#SearchDocs)

    GET /indexes/[index name]/docs?[query parameters]
    POST /indexes/[index name]/docs/search?api-version=2015-02-28-Preview

[Recherche de document](#LookupAPI)

     GET /indexes/[index name]/docs/[key]?[query parameters]

[Nombre de documents](#CountDocs)

    GET /indexes/[index name]/docs/$count?api-version=2015-02-28-Preview

[Suggestions](#Suggestions)

    GET /indexes/[index name]/docs/suggest?[query parameters]
    POST /indexes/[index name]/docs/suggest?api-version=2015-02-28-Preview

- - -
<a name="IndexOps"></a>

## <a name="index-operations"></a>Opérations d'index
Vous pouvez créer et gérer des index dans le service Azure Search via de simples requêtes HTTP (POST, GET, PUT, DELETE) sur une ressource d'index donnée. toocreate un index, vous commencez par publier un document JSON qui décrit le schéma d’index hello. schéma de Hello définit les champs de hello de hello index, leurs types de données, et comment elles peuvent être utilisées (par exemple, dans les recherches en texte intégral, filtres, de tri ou des facettes). Il définit également des profils de calcul de score, générateurs de suggestions et d’autres comportements de hello tooconfigure attributs d’index de hello.

Hello exemple suivant fournit une illustration d’un schéma utilisé pour la recherche sur les informations d’hôtel avec le champ de Description hello défini dans deux langues. Notez comment les attributs contrôlent comment le champ de hello est utilisée. Par exemple hello `hotelId` est utilisé comme clé de document hello (`"key": true`) et est exclu des recherches en texte intégral (`"searchable": false`).

    {
    "name": "hotels",  
    "fields": [
      {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false},
      {"name": "baseRate", "type": "Edm.Double"},
      {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
      {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
      {"name": "hotelName", "type": "Edm.String"},
      {"name": "category", "type": "Edm.String"},
      {"name": "tags", "type": "Collection(Edm.String)"},
      {"name": "parkingIncluded", "type": "Edm.Boolean"},
      {"name": "smokingAllowed", "type": "Edm.Boolean"},
      {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
      {"name": "rating", "type": "Edm.Int32"},
      {"name": "location", "type": "Edm.GeographyPoint"}
     ],
     "suggesters": [
      {
       "name": "sg",
       "searchMode": "analyzingInfixMatching",
       "sourceFields": ["hotelName"]
      }
     ]
    }

Après la création d’index de hello, vous allez télécharger des documents qui remplissent les index hello. Pour cette étape, consultez [Ajout ou mise à jour de documents](#AddOrUpdateDocuments) .

Pour une vidéo de présentation tooindexing dans Azure Search, consultez hello [épisode de Channel 9 Cloud Cover sur Azure Search](http://go.microsoft.com/fwlink/p/?LinkId=511509).

<a name="CreateIndex"></a>

## <a name="create-index"></a>Création d'index
Un index est le moyen principal de hello d’organisation et de recherche de documents dans Azure Search, toohow comme une table organise les enregistrements dans une base de données. Chaque index a un ensemble de documents que tout est conforme toohello schéma d’index (noms de champs, types de données et propriétés), mais spécifie également des constructions supplémentaires (générateurs de suggestions, profils de calcul de score et les options CORS) qui définissent d’autres comportements de recherche.

Vous pouvez créer un index dans un service Azure Search à l'aide d'une requête HTTP POST ou PUT. corps de Hello de demande de hello est un schéma JSON qui spécifie les informations d’index et la configuration hello.

    POST https://[service name].search.windows.net/indexes?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

Vous pouvez également utiliser une requête PUT et spécifiez le nom de l’index hello sur hello URI. Si les index hello n’existe pas, il sera créé.

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]

Création d’un index détermine la structure hello de hello documents stockés et utilisés dans les opérations de recherche. Index de remplissage hello est une opération distincte. Pour cette étape, vous pouvez utiliser un [indexeur](https://msdn.microsoft.com/library/azure/mt183328.aspx) (disponible pour les sources de données prises en charge) ou une opération [Ajout, mise à jour ou suppression de documents](https://msdn.microsoft.com/library/azure/dn798930.aspx). index de Hello inversé est généré lors de la validation des documents de hello.

**Remarque**: nombre maximal de hello d’index autorisé varie selon le niveau de tarification. service gratuit de Hello permet des index de too3. Le service standard autorise 50 index par service de recherche. Pour plus d'informations, consultez [Limites et contraintes](http://msdn.microsoft.com/library/azure/dn798934.aspx) .

**Requête**

Le protocole HTTPS est requis pour toutes les requêtes de service. Hello **Create Index** demande peut être construite à l’aide d’une méthode POST ou PUT. Lors de l’utilisation de POST, vous devez fournir un nom d’index dans le corps de la demande, ainsi que la définition de schéma d’index hello hello. Avec PUT, nom de l’index hello fait partie de l’URL de hello. Si les index hello n’existe pas, il est créé. S’il existe déjà, il est mis à jour toohello nouvelle définition.

Hello nom d’index doit être en minuscules, commencer par une lettre ou un chiffre, contenir sans barres obliques ni points et être inférieure à 128 caractères. Après avoir démarré le nom de l’index hello par une lettre ou un chiffre, reste hello du nom de hello peut inclure toute lettre, le numéro et des tirets, tant que les tirets hello ne soient pas contigus.

Hello `api-version` est requis. Pour obtenir la liste des versions disponibles, consultez [Contrôle de version du service Search](http://msdn.microsoft.com/library/azure/dn864560.aspx) .

**En-têtes de requête**

Hello suivant liste décrit hello requis et les en-têtes de demande facultatif.

* `Content-Type`: requis. Définissez cette propriété trop`application/json`
* `api-key`: obligatoire. Hello `api-key` est utilisé pour
* authentifier le service de recherche tooyour hello demande. Il s’agit d’une valeur de chaîne, d’un service de tooyour unique. Hello **Create Index** demande doit inclure un `api-key` en-tête défini la clé d’administration tooyour (en tant que clé de requête tooa exécutée).

Vous devez également les URL de demande du nom tooconstruct hello hello service. Vous pouvez obtenir le nom du service hello et `api-key` à partir de votre tableau de bord de service Bonjour portail Azure. Consultez [créer un service Azure Search dans le portail de hello](search-create-service-portal.md) de l’aide de navigation de page.

<a name="RequestData"></a>
**Syntaxe du corps de la requête**

corps de Hello de demande de hello contient une définition de schéma, qui inclut la liste hello des champs de données de documents qui alimenteront cet index, les types de données, attributs, ainsi que d’une liste facultative de l’évaluation des profils qui est utilisé tooscore mise en correspondance des documents au heure de la requête.

Notez que pour une demande POST, vous devez spécifier nom d’index hello dans le corps de la demande hello.

Il peut être uniquement un champ clé dans l’index de hello. Il a toobe un champ de chaîne. Ce champ représente l’identificateur unique de hello pour chaque document stocké dans les index hello.

parties principales Hello un index hello suivants :

* `name`
* `fields` qui alimenteront cet index, y compris le nom, le type de données et les propriétés qui définissent les actions autorisées sur ce champ.
* `suggesters` utilisés pour les requêtes prédictives ou avec saisie semi-automatique.
* `scoringProfiles` utilisés pour le classement personnalisé des scores de recherche. Pour plus d'informations, consultez [Ajout de profils de calcul de score](https://msdn.microsoft.com/library/azure/dn798928.aspx) .
* `analyzers`, `charFilters`, `tokenizers`, `tokenFilters` utilisé toodefine comment vos documents/requêtes sont divisées en jetons indexables/de recherche. Consultez [Analyse dans Azure Search](https://aka.ms//azsanalysis) pour plus d’informations.
* `defaultScoringProfile`utilisé par défaut de hello toooverwrite comportements de calcul de score.
* `corsOptions`requêtes de cross-origin tooallow par rapport à votre index.

syntaxe Hello pour structurer la charge utile de demande hello est comme suit. Vous trouverez un exemple de requête dans cette rubrique.

    {
      "name": (optional on PUT; required on POST) "name_of_index",
      "fields": [
        {
          "name": "name_of_field",
          "type": "Edm.String | Collection(Edm.String) | Edm.Int32 | Edm.Int64 | Edm.Double | Edm.Boolean | Edm.DateTimeOffset | Edm.GeographyPoint",
          "searchable": true (default where applicable) | false (only Edm.String and Collection(Edm.String) fields can be searchable),
          "filterable": true (default) | false,
          "sortable": true (default where applicable) | false (Collection(Edm.String) fields cannot be sortable),
          "facetable": true (default where applicable) | false (Edm.GeographyPoint fields cannot be facetable),
          "key": true | false (default, only Edm.String fields can be keys),
          "retrievable": true (default) | false,              
          "analyzer": "name of hello analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of hello search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of hello indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in hello future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies toosearchable fields) {
            "weights": {
              "searchable_field_name": relative_weight_value (positive numbers),
              ...
            }
          },
          "functions": (optional) [
            {
              "type": "magnitude | freshness | distance | tag",
              "boost": # (positive number used as multiplier for raw score != 1),
              "fieldName": "...",
              "interpolation": "constant | linear (default) | quadratic | logarithmic",
              "magnitude": {
                "boostingRangeStart": #,
                "boostingRangeEnd": #,
                "constantBoostBeyondRange": true | false (default)
              },
              "freshness": {
                "boostingDuration": "..." (value representing timespan leading toonow over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter toobe passed in queries toouse as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (hello distance in kilometers from hello reference location where hello boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter toobe passed in queries toospecify list of tags toocompare against target field, see "scoringParameter" for syntax details)
              }
            }
          ],
          "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
        }
      ],
      "analyzers":(optional)[ ... ],
      "charFilters":(optional)[ ... ],
      "tokenizers":(optional)[ ... ],
      "tokenFilters":(optional)[ ... ],
      "defaultScoringProfile": (optional) "...",
      "corsOptions": (optional) {
        "allowedOrigins": ["*"] | ["origin_1", "origin_2", ...],
        "maxAgeInSeconds": (optional) max_age_in_seconds (non-negative integer)
      }
    }

**Attributs d'index**

Hello attributs suivants peuvent être définis lors de la création d’un index. Pour plus d'informations sur le calcul de score et les profils de calcul de score, consultez [Ajout de profils de calcul de score](https://msdn.microsoft.com/library/azure/dn798928.aspx).

`name`-Jeux hello nom du champ de hello.

`type`-Jeux hello le type de données pour le champ de hello.

`searchable`-Marque hello champ de texte intégral en mesure de recherche. Cela signifie qu'il fera l'objet d'une analyse, par exemple lexicale, lors de l'indexation. Si vous définissez un `searchable` champ tooa valeur comme « journée ensoleillée », en interne il sera fractionné en jetons individuels de hello « jour » et « ensoleillée ». Cela permet d'effectuer des recherches en texte intégral de ces termes. Les champs de type `Edm.String` ou `Collection(Edm.String)` sont `searchable` par défaut. Les autres types de champs ne peuvent pas être `searchable`.

* **Remarque**: `searchable` champs consomment davantage d’espace dans votre index, car Azure Search stocke une version supplémentaire sous forme de jeton de valeur du champ hello pour les recherches en texte intégral. Si vous souhaitez toosave espace dans votre index et que vous n’avez pas besoin une toobe champ inclus dans les recherches, définissez `searchable` trop`false`.

`filterable`-Permet de hello toobe de champ référencé dans `$filter` requêtes. `filterable` diffère de `searchable` du point de vue du mode de traitement des chaînes. Les champs de type `Edm.String` ou `Collection(Edm.String)` qui sont `filterable` ne font pas l'objet d'une analyse lexicale, les comparaisons ne concernent donc que les correspondances exactes. Par exemple, si vous définissez un tel champ `f` trop « journée ensoleillée », `$filter=f eq 'sunny'` ne trouve aucune correspondance, mais `$filter=f eq 'sunny day'` sera. Tous les champs sont `filterable` par défaut.

`sortable`-Par défaut système de hello trie les résultats par score, mais il est souvent les utilisateurs que toosort par les champs dans les documents de hello. Les champs de type `Collection(Edm.String)` ne peuvent pas être `sortable`. Tous les autres champs sont `sortable` par défaut.

`facetable`: généralement utilisé dans une présentation des résultats de recherche qui inclut le nombre d'accès par catégorie (par exemple, vous recherchez des appareils photo numériques et regardez le nombre d'accès par marque, mégapixels, prix, etc.). Cette option ne peut pas être utilisée avec des champs de type `Edm.GeographyPoint`. Tous les autres champs sont `facetable` par défaut.

* **Remarque** : les champs de type `Edm.String` qui sont `filterable`, `sortable` ou `facetable` ne doivent pas dépasser 32 Ko de longueur. Il s’agit, car ces champs sont traités comme un terme de recherche et la longueur maximale de hello d’un terme dans Azure Search est de 32 Ko. Si vous devez toostore davantage de texte dans un champ de chaîne, vous devez tooexplicitly définir `filterable`, `sortable`, et `facetable` trop`false` dans votre définition d’index.
* **Remarque**: si un champ n’a aucun Hello ci-dessus attributs définis trop`true` (`searchable`, `filterable`, `sortable`, ou`facetable`) hello champ est effectivement exclu de l’index de hello inversé. Cette option est utile pour les champs qui ne sont pas utilisés dans les requêtes, mais qui sont nécessaires dans les résultats de recherche. À l’exclusion de ces champs à partir de l’index de hello améliore les performances.

`key`-Marques hello champ comme contenant des identificateurs uniques pour les documents dans l’index de hello. Un seul champ doit être choisi comme hello `key` champ et il doit être de type `Edm.String`. Champs clés peuvent être utilisé toolook des documents directement par le biais de hello [API de recherche](#LookupAPI).

`retrievable`-Définit si le champ de hello peut être retournée dans un résultat de recherche.  Cela est utile lorsque vous souhaitez toouse un champ (par exemple, marge) en tant que filtre, de tri ou de mécanisme de calcul de score mais que vous ne voulez pas que des utilisateurs finaux de hello champ toobe toohello visible. Il doit être `true` for `key` .

`analyzer`-Jeux hello nom de hello analyseur toouse hello champ au moment de la recherche au moment de l’indexation. Pourquoi autorisée du jeu de valeurs, consultez [analyseurs](https://msdn.microsoft.com/library/mt605304.aspx). Cette option ne peut être utilisée qu’avec les champs `searchable` et ne peut être associée à `searchAnalyzer` ou `indexAnalyzer`.  Une fois que l’Analyseur de hello est choisie, il ne peut pas être modifié pour le champ de hello.

`searchAnalyzer`-Jeux hello nom de l’analyseur hello utilisée au moment de la recherche pour le champ de hello. Pourquoi autorisée du jeu de valeurs, consultez [analyseurs](https://msdn.microsoft.com/library/mt605304.aspx). Cette option peut être utilisée uniquement avec les champs `searchable` . Elle doit être définie avec `indexAnalyzer` et ne peut pas être définie avec hello `analyzer` option. Cet analyseur peut être mis à jour sur un champ existant.

`indexAnalyzer`-Jeux hello nom de l’analyseur hello utilisée au moment de l’indexation pour le champ de hello. Pourquoi autorisée du jeu de valeurs, consultez [analyseurs](https://msdn.microsoft.com/library/mt605304.aspx). Cette option peut être utilisée uniquement avec les champs `searchable` . Elle doit être définie avec `searchAnalyzer` et ne peut pas être définie avec hello `analyzer` option. Une fois que l’Analyseur de hello est choisie, il ne peut pas être modifié pour le champ de hello.

`suggesters`-Jeux hello mode de recherche et les champs qui sont source de hello du contenu hello pour obtenir des suggestions. Pour plus d'informations, consultez [Générateurs de suggestions](#Suggesters) .

`scoringProfiles` : définit les comportements de calcul de score personnalisés qui vous permettent de choisir les éléments qui s'affichent en haut des résultats de recherche. Les profils de calcul de score sont constitués de pondérations et de fonctions de champ. Consultez [ajouter les profils de calcul de score](https://msdn.microsoft.com/library/azure/dn798928.aspx) pour plus d’informations sur les attributs hello utilisés dans un profil de score.

<!-- This is a standalone topic in MSDN -->
<a name="LanguageSupport"></a>
**Support multilingue**

Les champs pouvant faire l'objet d'une recherche subissent une analyse qui implique la plupart du temps une analyse lexicale, la normalisation du texte et le filtrage des termes. Par défaut, les champs interrogeables dans Azure Search sont analysés par hello [analyseur Apache Lucene Standard](http://lucene.apache.org/core/4_9_0/analyzers-common/index.html) qui découpe le texte en suivant le[« Unicode Text Segmentation »](http://unicode.org/reports/tr29/) règles. En outre, analyseur standard de hello convertit écran minuscules de tous les caractères tootheir. Les documents indexés et les termes de recherche accédez par l’analyse de hello durant l’indexation et de traitement des requêtes.

Azure Search prend en charge l’indexation des champs dans plusieurs langues. Chaque langue requiert un analyseur de texte non standard qui tient compte des caractéristiques d'une langue donnée. Azure Search propose deux types d'analyseurs :

* 35 analyseurs pris en charge par Lucene.
* 50 analyseurs pris en charge par la technologie de traitement du langage naturel Microsoft propriétaire utilisée dans Office et Bing.

Certains développeurs préfèrent hello solution open source, simple et plus facile de Lucene. Analyseurs Lucene sont plus rapides, mais les analyseurs de Microsoft hello ont fonctionnalités avancées, telles que lemmatisation, word decompounding (dans les langues telles que l’allemand, danois, néerlandais, suédois, norvégien, estonien, terminer, hongrois, slovaque) et reconnaissance d’entité (URL des messages électroniques, des dates, des nombres). Si possible, vous devez exécuter les comparaisons de deux hello Microsoft et Lucene analyseurs toodecide celui qui est plus adaptée.

***Comparatif***

Analyseur de Lucene Hello pour l’anglais étend l’analyseur standard de hello. Il supprime la marque du possessif (le « ’s ») à la fin des mots, applique la recherche de radical conformément à [l’algorithme de recherche de radical de Porter](http://tartarus.org/~martin/PorterStemmer/) et supprime les [mots vides](http://en.wikipedia.org/wiki/Stop_words) de l’anglais.

En comparaison, analyseur de Microsoft hello effectue lemmatisation au lieu de la recherche de radical. Cela signifie qu’il peut bien mieux gérer des mots infléchis et de formes irrégulières, ce qui donne des résultats de recherche plus pertinents (module espion 7 de [Présentation MVA d’Azure Search](http://www.microsoftvirtualacademy.com/training-courses/adding-microsoft-azure-search-to-your-websites-and-apps) pour plus de détails).

L’indexation avec des analyseurs de Microsoft est en moyenne deux fois toothree plus lentes que leurs équivalents Lucene, en fonction du langage de hello. Les performances de recherche ne doivent pas être trop affectées pour les requêtes de taille moyenne.

***Configuration***

Pour chaque champ dans la définition de l’index hello, vous pouvez définir hello `analyzer` nom de l’analyseur tooan propriété qui spécifie la langue et le fournisseur. Hello analyseur même sera appliqué lors de l’indexation et de recherche pour ce champ.
Par exemple, vous pouvez avoir des champs distincts pour des descriptions d’hôtel anglais, espagnol et Français qui existent côte à côte dans hello même index. Hello d’utilisation ['searchFields' paramètre de requête](#SearchQueryParameters) toospecify le toosearch spécifiques au langage champ contre dans vos requêtes. Vous pouvez consulter des exemples de requêtes qui incluent hello `analyzer` propriété dans [recherche de Documents](#SearchDocs). 

***Liste d’analyseurs***

Vous trouverez ci-dessous la liste de hello des langues prises en charge avec les noms d’analyseur Lucene et Microsoft.

<table style="font-size:12">
    <tr>
        <th>language</th>
        <th>Nom de l’analyseur Microsoft</th>
        <th>Nom de l’analyseur Lucene</th>
    </tr>
    <tr>
        <td>Arabe</td>
        <td>ar.microsoft</td>
        <td>ar.lucene</td>        
    </tr>
    <tr>
        <td>Arménien</td>
        <td></td>
        <td>hy.lucene</td>
      </tr>
    <tr>
        <td>Bangla</td>
        <td>bn.microsoft</td>
        <td></td>
    </tr>
      <tr>
        <td>Basque</td>
        <td></td>
        <td>eu.lucene</td>
    </tr>
      <tr>
         <td>Bulgare</td>
        <td>bg.microsoft</td>
        <td>bg.lucene</td>
      </tr>
      <tr>
        <td>Catalan</td>
        <td>ca.microsoft</td>
        <td>ca.lucene</td>          
      </tr>
    <tr>
        <td>Chinois simplifié</td>
        <td>zh-Hans.microsoft</td>
        <td>zh-Hans.lucene</td>        
    </tr>
    <tr>
        <td>Chinois traditionnel</td>
        <td>zh-Hant.microsoft</td>
        <td>zh-Hant.lucene</td>        
    <tr>
    <tr>
        <td>Croate</td>
        <td>hr.microsoft</td>
        <td/></td>
    </tr>
    <tr>
        <td>Tchèque</td>
        <td>cs.microsoft</td>
        <td>cs.lucene</td>        
    </tr>    
    <tr>
        <td>Danois</td>
        <td>da.microsoft</td>
        <td>da.lucene</td>        
    </tr>    
    <tr>
        <td>Néerlandais</td>
        <td>nl.microsoft</td>
        <td>nl.lucene</td>    
    </tr>    
    <tr>
        <td>Français</td>        
        <td>en.microsoft</td>
        <td>en.lucene</td>        
    </tr>
    <tr>
        <td>Estonien</td>
        <td>et.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Finnois</td>
        <td>fi.microsoft</td>
        <td>fi.lucene</td>        
    </tr>    
    <tr>
        <td>Français</td>
        <td>fr.Microsoft</td>
        <td>fr.lucene</td>        
    </tr>
    <tr>
        <td>Galicien</td>
        <td></td>
        <td>gl.lucene</td>        
      </tr>
    <tr>
        <td>Allemand</td>
        <td>de.Microsoft</td>
        <td>de.lucene</td>        
    </tr>
    <tr>
        <td>Grec</td>
        <td>el.microsoft</td>
        <td>el.lucene</td>        
    </tr>
    <tr>
        <td>Goudjrati</td>
        <td>gu.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Hébreu</td>
        <td>he.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Hindi</td>
        <td>hi.microsoft</td>
        <td>hi.lucene</td>        
    </tr>
    <tr>
        <td>Hongrois</td>        
        <td>hu.microsoft</td>
        <td>hu.lucene</td>
    </tr>
    <tr>
        <td>Islandais</td>
        <td>is.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Indonésien</td>
        <td>id.microsoft</td>
        <td>id.lucene</td>        
    </tr>
    <tr>
        <td>Irlandais</td>
        <td></td>
          <td>ga.lucene</td>
    </tr>
    <tr>
        <td>Italien</td>
        <td>it.microsoft</td>
        <td>it.lucene</td>        
    </tr>
    <tr>
        <td>Japonais</td>
        <td>ja.Microsoft</td>
        <td>ja.lucene</td>

    </tr>
    <tr>
        <td>Kannada</td>
        <td>ka.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Coréen</td>
        <td>ko.microsoft</td>
        <td>ko.lucene</td>
    </tr>
    <tr>
        <td>Letton</td>        
        <td>lv.microsoft</td>
        <td>lv.lucene</td>    
    </tr>
    <tr>
        <td>Lituanien</td>
        <td>lt.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Malayalam</td>
        <td>ml.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Malais (latin)</td>
        <td>ms.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Marathi</td>
        <td>mr.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Norvégien</td>
        <td>nb.Microsoft</td>
        <td>no.lucene</td>        
    </tr>
      <tr>
        <td>Persan</td>
        <td></td>
        <td>fa.lucene</td>        
      </tr>
    <tr>
        <td>Polonais</td>
        <td>pl.microsoft</td>
        <td>pl.lucene</td>        
    </tr>
    <tr>
        <td>Portugais (Brésil)</td>
        <td>pt-Br.microsoft</td>
        <td>pt-Br.lucene</td>        
    </tr>
    <tr>
        <td>Portugais (Portugal)</td>
        <td>pt-Pt.microsoft</td>        
        <td>pt-Pt.lucene</td>
    </tr>
    <tr>
        <td>Pendjabi</td>
        <td>pa.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Roumain</td>
        <td>ro.microsoft</td>
        <td>ro.lucene</td>
    </tr>
    <tr>
        <td>Russe</td>
        <td>ru.microsoft</td>
        <td>ru.lucene</td>    
    </tr>
    <tr>
        <td>Serbe (cyrillique)</td>
        <td>sr-cyrillic.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Serbe (latin)</td>
        <td>sr-latin.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Slovaque</td>
        <td>sk.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Slovène</td>
        <td>sl.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Espagnol</td>
        <td>es.Microsoft</td>
        <td>es.lucene</td>
    </tr>
    <tr>
        <td>Suédois</td>
        <td>sv.microsoft</td>
        <td>sv.lucene</td>
    </tr>

    <tr>
        <td>Tamoul</td>
        <td>ta.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Télougou</td>
        <td>te.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Thaï</td>
        <td>th.microsoft</td>
        <td>th.lucene</td>
    </tr>
    <tr>
        <td>Turc</td>
        <td>tr.microsoft</td>
        <td>tr.lucene</td>        
    </tr>
    <tr>
        <td>Ukrainien</td>
        <td>uk.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Ourdou</td>
        <td>ur.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Vietnamien</td>
        <td>vi.microsoft</td>
        <td></td>
    </tr>
    <td colspan="3">En outre, Azure Search fournit des configurations d'analyseur sans langage spécifié</td>
    <tr>
        <td>Pliage ASCII standard</td>
        <td>standardasciifolding.lucene</td>
        <td>
        <ul>
            <li>Segmentation de texte Unicode (générateur de jetons standard)</li>
            <li>Filtre de pliage ASCII - convertit les caractères Unicode qui n’appartiennent pas ensemble toohello de 127 premiers caractères ASCII dans leurs équivalents ASCII. Cela est utile pour supprimer les signes diacritiques.</li>
        </ul>
        </td>
    </tr>
</table>

Tous les analyseurs dont les noms sont annotés avec <i>lucene</i> s’appuient sur les [analyseurs de langue d’Apache Lucene](http://lucene.apache.org/core/4_9_0/analyzers-common/overview-summary.html). Plus d’informations sur le filtre pliage ASCII de hello trouverez [ici](http://lucene.apache.org/core/4_9_0/analyzers-common/org/apache/lucene/analysis/miscellaneous/ASCIIFoldingFilter.html).

**Générateurs de suggestions**

A `suggester` définit les champs dans un index sont utilisé toosupport saisie semi-automatique dans les recherches. En général, les chaînes de recherche partielles sont envoyées toohello [Suggestions API](#Suggestions) pendant hello saisie d’une requête de recherche, et hello API renvoie un ensemble d’expressions suggérées. Un générateur de suggestions que vous définissez dans les index hello détermine quels champs sont des termes de recherche prédictives hello toobuild utilisé. Consultez [Générateurs de suggestion](#Suggesters) pour plus de détails sur la configuration.

**Profils de score**

A `scoringProfile` définit le calcul de score des comportements personnalisés qui vous permettent d’influencer les éléments qui apparaissent plus dans les résultats de recherche hello. Les profils de calcul de score sont constitués de pondérations et de fonctions de champ. toouse les, vous spécifiez un profil par nom de chaîne de requête hello.

Profil de calcul de score par défaut fonctionne derrière hello scènes toocompute un score de recherche pour chaque élément dans un jeu de résultats. Vous pouvez utiliser hello interne, sans nom, le profil de score. Vous pouvez également définir `defaultScoringProfile` toouse un profil personnalisé comme valeur par défaut de hello, appelé chaque fois qu’un profil personnalisé n’est pas spécifié dans la chaîne de requête hello.

Consultez [ajouter score profils tooa des index de recherche (API REST Service Azure Search)](search-api-scoring-profiles-2015-02-28-preview.md) pour plus d’informations.

**Options CORS**

Javascript côté client ne peut pas appeler des API par défaut étant donné que hello navigateur empêche toutes les demandes cross-origin. Activer les CORS (partage des ressources Cross-Origin) en définissant les hello `corsOptions` index d’attribut tooallow requêtes cross-origin tooyour. Notez que, pour des raisons de sécurité, seules les API de requête prennent en charge CORS. Hello options suivantes peut être définie pour CORS :

* `allowedOrigins`(obligatoire) : il s’agit d’une liste d’origines qui sera octroyé l’index tooyour access. Cela signifie que tout code Javascript servi à partir de ces origines sera autorisé tooquery votre index (en supposant qu’il fournit la clé d’API correcte hello). Chaque origine est en général sous forme de hello `protocol://fully-qualified-domain-name:port` bien que hello port est souvent omis. Consultez [cet article](http://go.microsoft.com/fwlink/?LinkId=330822) pour plus de détails.
  * Si vous souhaitez origines de tooall accès tooallow, inclure `*` comme un seul élément Bonjour `allowedOrigins` tableau. Notez que **cette pratique est déconseillée pour les services de recherche de production.** Toutefois, elle peut être utile à des fins de développement ou de débogage.
* `maxAgeInSeconds`(facultatif) : les navigateurs utilisent cette valeur toodetermine hello durée (en secondes) toocache réponses préliminaires CORS. Il doit s'agir d'un entier non négatif. Hello plu que cette valeur est, améliorer les performances hello, mais hello plus long, qu'il aura pour effet de tootake de modifications de stratégie CORS. Si la valeur n'est pas définie, une durée par défaut de 5 minutes est utilisée.

<a name="CreateUpdateIndexExample"></a>
**Exemple de corps de requête**

    {
      "name": "hotels",  
      "fields": [
        {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false},
        {"name": "baseRate", "type": "Edm.Double"},
        {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
        {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
        {"name": "hotelName", "type": "Edm.String"},
        {"name": "category", "type": "Edm.String"},
        {"name": "tags", "type": "Collection(Edm.String)"},
        {"name": "parkingIncluded", "type": "Edm.Boolean"},
        {"name": "smokingAllowed", "type": "Edm.Boolean"},
        {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
        {"name": "rating", "type": "Edm.Int32"},
        {"name": "location", "type": "Edm.GeographyPoint"}
      ],
      "suggesters": [
        {
          "name": "sg",
          "searchMode": "analyzingInfixMatching",
          "sourceFields": ["hotelName"]
        }
      ]
    }

**Réponse**

Pour une requête correcte : « 201 Créé ».

Par défaut, les corps de réponse hello contiendra hello JSON pour la définition de l’index hello qui a été créée. Si hello `Prefer` en-tête de demande est défini trop`return=minimal`, corps de réponse hello sera vide et le code d’état de réussite hello sera « 204 pas de contenu » au lieu de « 201 créé ». Cela est vrai, que soient PUT ou POST index de hello toocreate utilisé.

**Remarques**

Actuellement, la prise en charge des mises à jour de schéma d'index est limitée. Les mises à jour de schéma qui nécessitent une réindexation, par exemple la modification des types de champs, ne sont pas prises en charge pour le moment. Bien que les champs existants ne peut pas être modifiés ou supprimés, les nouveaux champs peuvent être ajoutés à l’index existant tooan à tout moment. Lorsqu’un nouveau champ est ajouté, tous les documents existants dans les index hello auront automatiquement une valeur null pour ce champ. Aucun espace de stockage supplémentaires n’est consommée jusqu'à ce que les nouveaux documents sont ajoutés toohello index.

<a name="Suggesters"></a>

## <a name="suggesters"></a>Générateurs de suggestions
fonctionnalité de suggestions Hello dans Azure Search est une fonctionnalité de requête prédictives ou semi-automatique, en fournissant une liste de termes recherchés potentiels dans les entrées de chaîne toopartial de réponse entrées dans une zone de recherche. Vous avez probablement remarqué des suggestions de requête lors de l’utilisation de moteurs de recherche web commerciaux : la saisie de « NET » dans Bing génère une liste de termes pour « .NET 4.5 », « .NET Framework 3.5 », etc. Lorsque vous utilisez l’API REST du service de recherche hello, implémentation de suggestions dans une application Azure Search personnalisée requiert des hello qui suit :

* Activer les suggestions en ajoutant un **suggestions** construction dans votre index, en fournissant le nom de hello, mode de recherche et une liste de champs pour lequel prédictives est appelée. Par exemple, si vous spécifiez « cityName » comme un champ source, en tapant une chaîne de recherche partielle de « Sea » entraîne « Seattle », « Seaside » et « Seatac » (les trois sont des noms de ville) offerts dans les en tant qu’utilisateur de toohello des suggestions de requête.
* Demander des suggestions en appelant hello [Suggestions API](#Suggestions) dans votre code d’application. En général, les chaînes de recherche partielle sont envoyées toohello service pendant hello saisie d’une requête de recherche, et cette API renvoie un ensemble d’expressions suggérées.

Cet article explique comment tooconfigure un **suggestions**. Vous devez également examiner hello [Suggestions API](#Suggestions) pour plus d’informations sur l’utilisation d’un générateur de suggestions.

**Utilisation**

`Suggesters`sont créés dans les index hello et optimale des documents spécifiques de toosuggest plutôt que des termes ou expressions. champs Hello les plus appropriés sont les titres, les noms et les autres expressions relativement courtes pouvant identifier un élément. Les champs les moins efficaces sont les champs répétitifs, tels que les catégories et les balises, ou les champs très longs, tels que les champs des descriptions ou des commentaires.

Dans le cadre de la définition de l’index hello, vous pouvez ajouter un toohello unique suggestions `suggesters` collection. Les propriétés qui définissent un générateur de suggestions hello suivants :

* `name`: nom de hello du Générateur de suggestions hello. Vous utilisez le nom hello du Générateur de suggestions hello lors de l’appel hello `suggest` API.
* `searchMode`: hello toosearch stratégie utilisée pour les expressions candidates. Bonjour seul mode actuellement pris en charge est `analyzingInfixMatching`, qui effectue des correspondances souples au début de hello ou au milieu de hello de phrases.
* `sourceFields`: Liste d’un ou plusieurs champs qui sont source de hello du contenu hello pour obtenir des suggestions. Seuls les champs de type `Edm.String` et `Collection(Edm.String)` peuvent être des sources pour des suggestions. Seuls les champs qui n’ont pas un analyseur de langue personnalisé défini peuvent être utilisés.

**Exemple de générateur de suggestions**

Un générateur de suggestions fait partie de l’index de hello. Générateur de suggestions qu’une seule peut exister dans hello `suggesters` collection de champs de regroupement dans la version actuelle de hello, en même temps que hello et `scoringProfiles`.

        {
          "name": "hotels",
          "fields": [
             . . .
           ],
          "suggesters": [
            {
            "name": "sg",
            "searchMode": "analyzingInfixMatching",
            "sourceFields: ["hotelName", "category"]
            }
          ],
          "scoringProfiles": [
             . . .
          ]
        }

> [!NOTE]
> Si vous avez utilisé la version préliminaire publique de hello d’Azure Search, `suggesters` remplace une ancienne propriété booléenne (`"suggestions": false`) qui pris en charge uniquement des suggestions de préfixe pour les chaînes courtes (de 3 à 25 caractères). Solution de remplacement, `suggesters`, prend en charge les correspondances infixes qui recherchent des termes au début de hello ou au milieu de hello du contenu du champ, avec une meilleure tolérance aux erreurs dans les chaînes de recherche. À compter de version généralement disponible de hello, il s’agit désormais hello uniquement implémentation de l’API des suggestions hello. Hello plus anciens `suggestions` propriété qui a été introduite dans `api-version=2014-07-31-Preview` continue toowork dans cette version, mais n’est pas opérationnel Bonjour `2015-02-28` ou une version ultérieure d’Azure Search.
> 
> 

<a name="UpdateIndex"></a>

## <a name="update-index"></a>Mise à jour d'index
Vous pouvez mettre à jour un index existant dans Azure Search à l'aide d'une requête HTTP PUT. Les mises à jour peuvent inclure l’ajout de nouveaux champs toohello schéma existant, la modification des Cors et la modification des profils de calcul de score. Pour plus d'informations, consultez [Ajout de profils de calcul de score](https://msdn.microsoft.com/library/azure/dn798928.aspx) . Vous spécifiez le nom hello de hello index tooupdate sur l’URI de la demande hello :

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

**Important :** prise en charge des mises à jour de schéma index est toooperations limitées qui ne nécessitent pas la reconstruction d’index de recherche hello. Les mises à jour de schéma qui nécessitent une réindexation, par exemple la modification des types de champs, ne sont pas prises en charge pour le moment. De nouveaux champs peuvent être ajoutés à tout moment, mais les champs existants ne peuvent pas être modifiés ni supprimés. Hello valable trop`suggesters`. Ajouter de nouveaux champs suggestions tooa au niveau des champs hello hello sont ajoutés, mais les champs ne peuvent pas être supprimés de `suggesters` et champs existants ne peuvent pas être ajoutés trop`suggesters`.

Lorsque vous ajoutez un nouvel index tooan de champ, tous les documents existants dans les index hello auront automatiquement une valeur null pour ce champ. Aucun espace de stockage supplémentaires n’est consommée jusqu'à ce que les nouveaux documents sont ajoutés toohello index.

**Requête**

Le protocole HTTPS est requis pour toutes les requêtes de service. Hello **Index de mise à jour** demande est construite à l’aide de HTTP PUT. Avec PUT, nom de l’index hello fait partie de l’URL de hello. Si les index hello n’existe pas, il est créé. Si l’index hello existe déjà, il est mis à jour toohello nouvelle définition.

Hello nom d’index doit être en minuscules, commencer par une lettre ou un chiffre, contenir sans barres obliques ni points et être inférieure à 128 caractères. Après avoir démarré le nom de l’index hello par une lettre ou un chiffre, reste hello du nom de hello peut inclure toute lettre, le numéro et des tirets, tant que les tirets hello ne soient pas contigus.

`api-version=[string]` (obligatoire). version d’évaluation Hello `api-version=2015-02-28-Preview`. Pour plus d'informations, y compris sur d'autres versions, consultez [Contrôle de version de service Azure Search](http://msdn.microsoft.com/library/azure/dn864560.aspx) .

**En-têtes de requête**

Hello suivant liste décrit hello requis et les en-têtes de demande facultatif.

* `Content-Type`: requis. Définissez cette propriété trop`application/json`
* `api-key`: obligatoire. Hello `api-key` est utilisé tooauthenticate hello demande tooyour service de recherche. Il s’agit d’une valeur de chaîne, d’un service de tooyour unique. Hello **Index de mise à jour** demande doit inclure un `api-key` en-tête défini la clé d’administration tooyour (en tant que clé de requête tooa exécutée).

Vous devez également les URL de demande du nom tooconstruct hello hello service. Vous pouvez obtenir le nom du service hello et `api-key` à partir de votre tableau de bord de service Bonjour portail Azure. Consultez [créer un service Azure Search dans le portail de hello](search-create-service-portal.md) de l’aide de navigation de page.

**Syntaxe du corps de la requête**

Lors de la mise à jour d’un index existant, les corps hello doivent inclure la définition de schéma d’origine hello plus hello nouveaux champs que vous ajoutez ainsi hello modifié des profils de calcul de score, générateurs de suggestions et les options CORS, le cas échéant. Si vous ne modifiez pas les profils de calcul de score hello et les options CORS, vous devez inclure les originaux hello lorsque les index hello a été créé. En général hello meilleur modèle toouse des mises à jour est la définition d’index hello tooretrieve avec une commande GET, modifiez-le, puis mettez-le à jour avec une méthode PUT.

syntaxe de schéma Hello utilisé toocreate qu'un index est reproduit ici par commodité. Consultez la section [Création d'index](#CreateIndex) pour plus de détails.

    {
      "name": (optional) "name_of_index",
      "fields": [
        {
          "name": "name_of_field",
          "type": "Edm.String | Collection(Edm.String) | Edm.Int32 | Edm.Int64 | Edm.Double | Edm.Boolean | Edm.DateTimeOffset | Edm.GeographyPoint",
          "searchable": true (default where applicable) | false (only Edm.String and Collection(Edm.String) fields can be searchable),
          "filterable": true (default) | false,
          "sortable": true (default where applicable) | false (Collection(Edm.String) fields cannot be sortable),
          "facetable": true (default where applicable) | false (Edm.GeographyPoint fields cannot be facetable),
          "key": true | false (default, only Edm.String fields can be keys),
          "retrievable": true (default) | false, 
          "analyzer": "name of hello analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of hello search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of hello indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in hello future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies toosearchable fields) {
            "weights": {
              "searchable_field_name": relative_weight_value (positive numbers),
              ...
            }
          },
          "functions": (optional) [
            {
              "type": "magnitude | freshness | distance | tag",
              "boost": # (positive number used as multiplier for raw score != 1),
              "fieldName": "...",
              "interpolation": "constant | linear (default) | quadratic | logarithmic",
              "magnitude": {
                "boostingRangeStart": #,
                "boostingRangeEnd": #,
                "constantBoostBeyondRange": true | false (default)
              },
              "freshness": {
                "boostingDuration": "..." (value representing timespan leading toonow over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter toobe passed in queries toouse as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (hello distance in kilometers from hello reference location where hello boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter toobe passed in queries toospecify list of tags toocompare against target field, see "scoringParameter" for syntax details)
              }
            }
          ],
          "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
        }
      ],
      "analyzers":(optional)[ ... ],
      "charFilters":(optional)[ ... ],
      "tokenizers":(optional)[ ... ],
      "tokenFilters":(optional)[ ... ],
      "defaultScoringProfile": (optional) "...",
      "corsOptions": (optional) {
        "allowedOrigins": ["*"] | ["origin_1", "origin_2", ...],
        "maxAgeInSeconds": (optional) max_age_in_seconds (non-negative integer)
      }
    }


**Réponse**

Pour une requête correcte : « 204 Pas de contenu ».

Par défaut, les corps de réponse hello sera vide. Toutefois, si hello `Prefer` en-tête de demande est défini trop`return=representation`, corps de réponse hello contiendra hello JSON pour la définition de l’index hello qui a été mis à jour. Dans ce cas, le code d’état de réussite hello sera « 200 OK ».

**Mise à jour de la définition d’index avec des analyseurs personnalisés**

Une fois défini, un analyseur, un générateur de jetons, un filtre de jetons ou un filtre de caractères ne peut pas être modifié. Nouveaux peut être ajoutés les index existants tooan uniquement si hello `allowIndexDowntime` indicateur a la valeur tootrue dans la demande de mise à jour d’index hello : 

`PUT https://[search service name].search.windows.net/indexes/[index name]?api-version=[api-version]&allowIndexDowntime=true`

Notez que cette opération mettra votre index hors connexion au moins de quelques secondes, à l’origine de votre indexation et de requête demande toofail. Disponibilité de performances et d’écriture de l’index de hello peut être altérée pendant plusieurs minutes après hello est mis à jour, ou plus de temps pour les très grands index.

<a name="ListIndexes"></a>

## <a name="list-indexes"></a>Liste des index
Hello **liste des index** opération renvoie une liste des index de hello actuellement dans votre service Azure Search.

    GET https://[service name].search.windows.net/indexes?api-version=[api-version]
    api-key: [admin key]

**Requête**

Le protocole HTTPS est requis pour toutes les requêtes de service. Hello **liste des index** demande peut être construite à l’aide de la méthode GET de hello.

`api-version=[string]` (obligatoire). version d’évaluation Hello `api-version=2015-02-28-Preview`. Pour plus d'informations, y compris sur d'autres versions, consultez [Contrôle de version de service Azure Search](http://msdn.microsoft.com/library/azure/dn864560.aspx) .

**En-têtes de requête**

Hello suivant liste décrit hello requis et les en-têtes de demande facultatif.

* `api-key`: obligatoire. Hello `api-key` est utilisé tooauthenticate hello demande tooyour service de recherche. Il s’agit d’une valeur de chaîne, d’un service de tooyour unique. Hello **liste des index** demande doit inclure un `api-key` clé d’administration tooan ensemble (en tant que clé de requête tooa exécutée).

Vous devez également les URL de demande du nom tooconstruct hello hello service. Vous pouvez obtenir le nom du service hello et `api-key` à partir de votre tableau de bord de service Bonjour portail Azure. Consultez [créer un service Azure Search dans le portail de hello](search-create-service-portal.md) de l’aide de navigation de page.

**Corps de la requête**

Aucune.

**Réponse**

Code d'état : 200 OK est retourné pour une réponse correcte.

Voici un exemple de corps de réponse :

    {
      "value": [
        {
          "name": "Books",
          "fields": [
            {"name": "ISBN", ...},
            ...
          ]
        },
        {
          "name": "Games",
          ...
        },
        ...
      ]
    }

Notez que vous pouvez filtrer la réponse hello vers le bas les propriétés de hello toojust que vous intéresse. Par exemple, si vous souhaitez uniquement la liste des noms d’index, utilisez hello OData `$select` option de requête :

    GET /indexes?api-version=2015-02-28-Preview&$select=name

Dans ce cas, réponse hello hello exemple ci-dessus apparaît comme suit :

    {
      "value": [
        {"name": "Books"},
        {"name": "Games"},
        ...
      ]
    }

Il s’agit d’une bande de passante toosave technique utile si vous avez un grand nombre d’index dans votre service de recherche.

<a name="GetIndex"></a>

## <a name="get-index"></a>Obtention d'index
Hello **obtenir l’Index** opération Obtient la définition de l’index hello à partir d’Azure Search.

    GET https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

**Requête**

Le protocole HTTPS est requis pour les requêtes de service. Hello **obtenir l’Index** demande peut être construite à l’aide de la méthode GET de hello.

Bonjour [nom de l’index] dans l’URI de la demande hello spécifie quels tooreturn index à partir de la collection d’index hello.

`api-version=[string]` (obligatoire). version d’évaluation Hello `api-version=2015-02-28-Preview`. Pour plus d'informations, y compris sur d'autres versions, consultez [Contrôle de version de service Azure Search](http://msdn.microsoft.com/library/azure/dn864560.aspx) .

**En-têtes de requête**

Hello suivant liste décrit hello requis et les en-têtes de demande facultatif.

* `api-key`: hello `api-key` est utilisé tooauthenticate hello demande tooyour service de recherche. Il s’agit d’une valeur de chaîne, d’un service de tooyour unique. Hello **obtenir l’Index** demande doit inclure un `api-key` clé d’administration tooan ensemble (en tant que clé de requête tooa exécutée).

Vous devez également les URL de demande du nom tooconstruct hello hello service. Vous pouvez obtenir le nom du service hello et `api-key` à partir de votre tableau de bord de service Bonjour portail Azure. Consultez [créer un service Azure Search dans le portail de hello](search-create-service-portal.md) de l’aide de navigation de page.

**Corps de la requête**

Aucune.

**Réponse**

Code d'état : 200 OK est retourné pour une réponse correcte.

Consultez l’exemple hello JSON dans [création et mise à jour d’un Index](#CreateUpdateIndexExample) pour obtenir un exemple de charge utile de réponse hello.

<a name="DeleteIndex"></a>

## <a name="delete-index"></a>Suppression d'index
Hello **supprimer l’Index** opération supprime un index et les documents associés à partir de votre service Azure Search. Vous pouvez obtenir le nom de l’index hello à partir du tableau de bord de service hello Bonjour portail Azure ou hello API. Consultez la section [List Indexes](#ListIndexes) pour plus d'informations.

    DELETE https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

**Requête**

Le protocole HTTPS est requis pour les requêtes de service. Hello **supprimer l’Index** demande peut être construite à l’aide de la méthode de suppression hello.

Bonjour [nom de l’index] dans l’URI de la demande hello spécifie quels toodelete index à partir de la collection d’index hello.

`api-version=[string]` (obligatoire). version d’évaluation Hello `api-version=2015-02-28-Preview`. Pour plus d'informations, y compris sur d'autres versions, consultez [Contrôle de version de service Azure Search](http://msdn.microsoft.com/library/azure/dn864560.aspx) .

**En-têtes de requête**

Hello suivant liste décrit hello requis et les en-têtes de demande facultatif.

* `api-key`: obligatoire. Hello `api-key` est utilisé tooauthenticate hello demande tooyour service de recherche. Il est une valeur de chaîne URL du service tooyour unique. Hello **supprimer l’Index** demande doit inclure un `api-key` en-tête défini la clé d’administration tooyour (en tant que clé de requête tooa exécutée).

Vous devez également les URL de demande du nom tooconstruct hello hello service. Vous pouvez obtenir le nom du service hello et `api-key` à partir de votre tableau de bord de service Bonjour portail Azure. Consultez [créer un service Azure Search dans le portail de hello](search-create-service-portal.md) de l’aide de navigation de page.

**Corps de la requête**

Aucune.

**Réponse**

Code d'état : 204 Pas de contenu est renvoyé en cas de réponse correcte.

<a name="GetIndexStats"></a>

## <a name="get-index-statistics"></a>Obtention de statistiques d'index
Hello **obtenir des statistiques d’Index** opération renvoie à partir d’Azure Search un nombre de documents pour les index en cours de hello, ainsi que l’utilisation du stockage.

    GET https://[service name].search.windows.net/indexes/[index name]/stats?api-version=[api-version]
    api-key: [admin key]

> [!NOTE]
> Les statistiques sur le nombre de documents et la taille du stockage sont collectées à intervalles de quelques minutes, pas en temps réel. Par conséquent, les statistiques hello retournés par cette API peut ne pas reflètent modifications dû à des opérations d’indexation récentes.
> 
> 

**Requête**

Le protocole HTTPS est requis pour toutes les requêtes de services. Hello **obtenir des statistiques d’Index** demande peut être construite à l’aide de la méthode GET de hello.

Bonjour [nom de l’index] dans l’URI de la demande hello indique hello service tooreturn des statistiques d’index pour l’index spécifié de hello.

`api-version=[string]` (obligatoire). version d’évaluation Hello `api-version=2015-02-28-Preview`. Pour plus d'informations, y compris sur d'autres versions, consultez [Contrôle de version de service Azure Search](http://msdn.microsoft.com/library/azure/dn864560.aspx) .

**En-têtes de requête**

Hello suivant liste décrit hello requis et les en-têtes de demande facultatif.

* `api-key`: hello `api-key` est utilisé tooauthenticate hello demande tooyour service de recherche. Il s’agit d’une valeur de chaîne, d’un service de tooyour unique. Hello **obtenir des statistiques d’Index** demande doit inclure un `api-key` clé d’administration tooan ensemble (en tant que clé de requête tooa exécutée).

Vous devez également les URL de demande du nom tooconstruct hello hello service. Vous pouvez obtenir le nom du service hello et `api-key` à partir de votre tableau de bord de service Bonjour portail Azure. Consultez [créer un service Azure Search dans le portail de hello](search-create-service-portal.md) de l’aide de navigation de page.

**Corps de la requête**

Aucune.

**Réponse**

Code d'état : 200 OK est retourné pour une réponse correcte.

corps de réponse Hello est Bonjour suivant le format :

    {
      "documentCount": number,
      "storageSize": number (size of hello index in bytes)
    }

<a name="TestAnalyzer"></a>

## <a name="test-analyzer"></a>Tester l’analyseur
Hello **analyser les API** montre comment un analyseur découpe le texte en jetons.

    POST https://[service name].search.windows.net/indexes/[index name]/analyze?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

**Requête**

Le protocole HTTPS est requis pour toutes les requêtes de services. Hello **analyser les API** demande peut être construite à l’aide de la méthode POST de hello.

`api-version=[string]` (obligatoire). version d’évaluation Hello `api-version=2015-02-28-Preview`. Pour plus d'informations, y compris sur d'autres versions, consultez [Contrôle de version de service Azure Search](http://msdn.microsoft.com/library/azure/dn864560.aspx) .

**En-têtes de requête**

Hello suivant liste décrit hello requis et les en-têtes de demande facultatif.

* `api-key`: hello `api-key` est utilisé tooauthenticate hello demande tooyour service de recherche. Il s’agit d’une valeur de chaîne, d’un service de tooyour unique. Hello **analyser les API** demande doit inclure un `api-key` clé d’administration tooan ensemble (en tant que clé de requête tooa exécutée).

Vous devez également nom de l’index hello et URL de demande du nom tooconstruct hello hello service. Vous pouvez obtenir le nom du service hello et `api-key` à partir de votre tableau de bord de service Bonjour portail Azure. Consultez [créer un service Azure Search dans le portail de hello](search-create-service-portal.md) de l’aide de navigation de page.

**Corps de la requête**

    {
      "text": "Text tooanalyze",
      "analyzer": "analyzer_name"
    }

ou

    {
      "text": "Text tooanalyze",
      "tokenizer": "tokenizer_name",
      "tokenFilters": (optional) [ "token_filter_name" ],
      "charFilters": (optional) [ "char_filter_name" ]
    }

Hello `analyzer_name`, `tokenizer_name`, `token_filter_name` et `char_filter_name` que les noms valides de toobe d’analyseurs prédéfinies ou personnalisées, générateurs de jetons, filtres de jeton et char pour les index de hello. toolearn d’informations sur les processus hello de l’analyse lexicale, consultez [Analysis dans Azure Search](https://aka.ms/azsanalysis).

**Réponse**

Code d'état : 200 OK est retourné pour une réponse correcte.

corps de réponse Hello est Bonjour suivant le format :

    {
      "tokens": [
        {
          "token": string (token),
          "startOffset": number (index of hello first character of hello token),
          "endOffset": number (index of hello last character of hello token),
          "position": number (position of hello token in hello input text)
        },
        ...
      ]
    }

**Exemple d’API Analyser**

**Requête**

    {
      "text": "Text tooanalyze",
      "analyzer": "standard"
    }

**Réponse**

    {
      "tokens": [
        {
          "token": "text",
          "startOffset": 0,
          "endOffset": 4,
          "position": 0
        },
        {
          "token": "to",
          "startOffset": 5,
          "endOffset": 7,
          "position": 1
        },
        {
          "token": "analyze",
          "startOffset": 8,
          "endOffset": 15,
          "position": 2
        }
      ]
    }

- - -
<a name="DocOps"></a>

## <a name="document-operations"></a>Opérations de document
Dans Azure Search, un index est stocké dans le cloud de hello et remplis à l’aide de documents JSON que vous téléchargez toohello service. Tous les documents hello que vous chargez comprennent le corpus de hello de vos données de recherche. Les documents contiennent des champs, dont certains sont tokenisés dans les termes de recherche à mesure qu'ils sont téléchargés. Hello `/docs` segment d’URL Bonjour API Azure Search représente la collection de hello de documents dans un index. Toutes les opérations effectuées sur le regroupement de hello telles que le téléchargement, la fusion, la suppression ou l’interrogation de documents prendre place dans le contexte de hello d’un index unique, c’est le cas hello URL pour que ces opérations commencent toujours par `/indexes/[index name]/docs` pour un nom de l’index donné.

Code de votre application doit générer JSON documents tooupload tooAzure recherche ou vous pouvez utiliser un [indexeur](https://msdn.microsoft.com/library/dn946891.aspx) tooload documents si la source de données hello est la base de données SQL Azure ou base de données Azure Cosmos. En règle générale, les index sont remplis à partir d'un jeu de données unique que vous fournissez.

Vous devez prévoir un document pour chaque élément que vous souhaitez toosearch. Une application de location de films peut avoir un document par film, une application vitrine peut avoir un document par référence, une application de formation en ligne peut avoir un document par cours, un cabinet de recherche peut avoir un document pour chaque document académique de son référentiel, etc.

Les documents sont constitués d'un ou de plusieurs champs. Les champs peuvent contenir du texte tokenisé par Azure Search dans des termes de recherche, ainsi que des valeurs non tokenisées ou non textuelles pouvant être utilisées dans des filtres ou des profils de calcul de score. Hello noms, types de données et les fonctionnalités de recherche pris en charge pour chaque champ sont déterminées par le schéma d’index hello. Un des champs hello dans chaque schéma d’index doit être désigné en tant qu’ID, et chaque document doit avoir une valeur pour le champ hello ID qui identifie de façon unique ce document dans l’index de hello. Tous les autres champs de document sont facultatifs et par défaut tooa les valeur null si non définie. Notez que les valeurs null n’occupent pas d’espace dans les index de recherche hello.

Avant de pouvoir télécharger des documents, vous devez avoir déjà créé les index hello sur le service de hello. Consultez la section [Création d'index](#CreateIndex) pour plus d'informations sur cette première étape.

<a name="AddOrUpdateDocuments"></a>

## <a name="add-update-or-delete-documents"></a>Ajout, mise à jour ou suppression de documents
Vous pouvez télécharger, fusionner, fusionner-ou-télécharger ou supprimer des documents à partir d'un index spécifié à l'aide de la requête HTTP POST. Pour un grand nombre de mises à jour, le traitement par lot des documents (too1000 documents par lot) ou 16 Mo par lot est recommandé.

    POST https://[service name].search.windows.net/indexes/[index name]/docs/index?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

**Requête**

Le protocole HTTPS est requis pour toutes les requêtes de service. Vous pouvez télécharger, fusionner, fusionner-ou-télécharger ou supprimer des documents à partir d'un index spécifié à l'aide de la requête HTTP POST.

Hello URI de requête inclut [nom de l’index], en spécifiant les index des documents toopost. Vous ne pouvez valider que les index de tooone de documents à la fois.

`api-version=[string]` (obligatoire). version d’évaluation Hello `api-version=2015-02-28-Preview`. Pour plus d'informations, y compris sur d'autres versions, consultez [Contrôle de version de service Azure Search](http://msdn.microsoft.com/library/azure/dn864560.aspx) .

**En-têtes de requête**

Hello suivant liste décrit hello requis et les en-têtes de demande facultatif.

* `Content-Type`: requis. Définissez cette propriété trop`application/json`
* `api-key`: obligatoire. Hello `api-key` est utilisé tooauthenticate hello demande tooyour service de recherche. Il s’agit d’une valeur de chaîne, d’un service de tooyour unique. Hello **ajouter des Documents** demande doit inclure un `api-key` en-tête défini la clé d’administration tooyour (en tant que clé de requête tooa exécutée).

Vous devez également les URL de demande du nom tooconstruct hello hello service. Vous pouvez obtenir le nom du service hello et `api-key` à partir de votre tableau de bord de service Bonjour portail Azure. Consultez [créer un service Azure Search dans le portail de hello](search-create-service-portal.md) de l’aide de navigation de page.

**Corps de la requête**

corps Hello de demande de hello contient un ou plusieurs documents toobe indexé. Les documents sont identifiés par une clé unique. Chaque document est associé à une action : upload, merge, mergeOrUpload ou delete. Demande de téléchargement doit inclure les données du document hello comme un ensemble de paires clé/valeur.

    {
      "value": [
        {
          "@search.action": "upload (default) | merge | mergeOrUpload | delete",
          "key_field_name": "unique_key_of_document", (key/value pair for key field from index schema)
          "field_name": field_value (key/value pairs matching index schema)
            ...
        },
        ...
      ]
    }

> [!NOTE]
> Les clés de document ne peuvent contenir que des lettres, des chiffres, des tirets (« - »), des traits de soulignement (« _ ») et les signes égal (« = »). Pour plus d’informations, consultez les [Règles d’affectation des noms](https://msdn.microsoft.com/library/azure/dn857353.aspx).
> 
> 

**Actions de document**

* `upload`: Une action de chargement est similaire tooan « upsert » où le document de hello sera inséré s’il est nouveau et mis à jour/remplacé s’il existe. Notez que tous les champs sont remplacés en cas de mise à jour hello.
* `merge`: Mises à jour fusion existant de document avec hello spécifié des champs. Si le document de hello n’existe pas, la fusion de hello échoue. N’importe quel champ que vous spécifiez dans une fusion remplace le champ existant de hello dans le document de hello. Cela inclut les champs de type `Collection(Edm.String)`. Par exemple, si hello document contient un champ « indicateurs » avec la valeur `["budget"]` et que vous exécutez une fusion avec la valeur `["economy", "pool"]` pour « balises », hello dernière valeur de champ hello « balises » sera `["economy", "pool"]`. Elle ne doit **pas** être `["budget", "economy", "pool"]`.
* `mergeOrUpload`: se comporte comme `merge` si un document avec hello donné clé déjà existe dans les index hello. Si le document de hello n’existe pas qu’il se comporte comme `upload` avec un nouveau document.
* `delete`: Delete Supprime document spécifié de hello à partir de l’index de hello. Notez que tous les champs que vous spécifiez dans un `delete` opération autre que du champ de clé hello sera ignorée. Si vous souhaitez tooremove un champ individuel à partir d’un document, utilisez `merge` à la place et simplement définir hello champ explicitement trop`null`.

**Réponse**

Code d’état : 200 (OK) est retourné pour une réponse correcte, ce qui signifie que tous les éléments ont été indexés. Cela est indiqué par hello `status` propriété définie tootrue pour tous les éléments, ainsi que les hello `statusCode` propriété définie tooeither 201 (pour les documents qui vient d’être téléchargés) ou 200 (pour les documents fusionnés ou supprimés) :

    {
      "value": [
        {
          "key": "unique_key_of_new_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 201
        },
        {
          "key": "unique_key_of_merged_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 200
        },
        {
          "key": "unique_key_of_deleted_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 200
        }
      ]
    }  

Un code d’état 207 (Multi-état) est renvoyé lorsqu’au moins un élément n’a pas été correctement indexé. Les éléments qui n’ont pas été indexées ont hello `status` toofalse ensemble de champs. Hello `errorMessage` et `statusCode` propriétés indique la raison de hello hello erreur d’indexation :

    {
      "value": [
        {
          "key": "unique_key_of_document_1",
          "status": false,
          "errorMessage": "hello search service is too busy tooprocess this document. Please try again later.",
          "statusCode": 503
        },
        {
          "key": "unique_key_of_document_2",
          "status": false,
          "errorMessage": "Document not found.",
          "statusCode": 404
        },
        {
          "key": "unique_key_of_document_3",
          "status": false,
          "errorMessage": "Index is temporarily unavailable because it was updated with hello 'allowIndexDowntime' flag set too'true'. Please try again later.",
          "statusCode": 422
        }
      ]
    }  

Hello tableau suivant explique hello différentes par document codes d’état qui peuvent être retournées dans la réponse de hello. Notez que certains indiquent des problèmes avec la demande hello elle-même, alors que d’autres conditions d’erreur temporaire. Hello ce dernier que vous devriez réessayer après un certain délai.

<table style="font-size:12">
    <tr>
        <th>Code d’état</th>
        <th>Signification</th>
        <th>Nouvelle tentative possible</th>
        <th>Remarques</th>
    </tr>
    <tr>
        <td>200</td>
        <td>Le document a été correctement modifié ou supprimé.</td>
        <td>n/a</td>
        <td>Les opérations de suppression sont <a href="https://en.wikipedia.org/wiki/Idempotence">idempotentes</a>. Autrement dit, même si une clé de document n’existe pas dans l’index de hello, essayez d’une opération de suppression avec cette clé entraîne un code de 200 état.</td>
    </tr>
    <tr>
        <td>201</td>
        <td>Le document a été créé avec succès.</td>
        <td>n/a</td>
        <td></td>
    </tr>
    <tr>
        <td>400</td>
        <td>Une erreur s’est produite dans le document hello qui l’a empêché d’en cours d’indexation.</td>
        <td>Non</td>
        <td>message d’erreur Hello en réponse de hello indique quel est le problème avec le document de hello.</td>
    </tr>
    <tr>
        <td>404</td>
        <td>Impossible de fusionner les documents Hello hello clé n’existe pas dans les index hello.</td>
        <td>Non</td>
        <td>Cette erreur ne s’applique pas aux téléchargements dans la mesure où ils créent de nouveaux documents, de même qu’elle ne se produit pas pour les suppressions, car elles sont <a href="https://en.wikipedia.org/wiki/Idempotence">idempotentes</a>.</td>
    </tr>
    <tr>
        <td>409</td>
        <td>Un conflit de version a été détecté lors de la tentative de tooindex un document.</td>
        <td>Oui</td>
        <td>Cela peut se produire quand vous essayez de hello tooindex même document plusieurs fois simultanément.</td>
    </tr>
    <tr>
        <td>422</td>
        <td>index de Hello est temporairement indisponible, car il a été mis à jour avec hello 'allowIndexDowntime' indicateur ensemble too'true'.</td>
        <td>Oui</td>
        <td></td>
    </tr>
    <tr>
        <td>503</td>
        <td>Votre service de recherche est temporairement indisponible, probablement en raison de la charge de tooheavy.</td>
        <td>Oui</td>
        <td>Votre code doit attendre avant de réessayer dans ce cas, ou vous risquez de prolonger l’indisponibilité de service hello.</td>
    </tr>
</table> 

**Remarque**: Si votre code client rencontre fréquemment une réponse 207, due au fait que le système de hello est sous charge. Vous pouvez le vérifier en vérifiant hello `statusCode` propriété 503. Si cela est le cas de hello, nous vous recommandons de ***la limitation des demandes d’indexation***. Sinon, si le trafic d’indexation ne diminue pas, système de hello pourrait commencer à rejeter toutes les demandes avec des 503 erreurs.

Code d’état 429 indique que vous avez dépassé votre quota de nombre hello de documents par index. Vous devez créer un autre index ou effectuer une mise à niveau pour bénéficier de limites de capacité supérieures.

**Exemple :**

    {
      "value": [
        {
          "@search.action": "upload",
          "hotelId": "1",
          "baseRate": 199.0,
          "description": "Best hotel in town",
          "description_fr": "Meilleur hôtel en ville",
          "hotelName": "Fancy Stay",
          "category": "Luxury",
          "tags": ["pool", "view", "wifi", "concierge"],
          "parkingIncluded": false,
          "smokingAllowed": false,
          "lastRenovationDate": "2010-06-27T00:00:00Z",
          "rating": 5,
          "location": { "type": "Point", "coordinates": [-122.131577, 47.678581] }
        },
        {
          "@search.action": "upload",
          "hotelId": "2",
          "baseRate": 79.99,
          "description": "Cheapest hotel in town",
          "description_fr": "Hôtel le moins cher en ville",
          "hotelName": "Roach Motel",
          "category": "Budget",
          "tags": ["motel", "budget"],
          "parkingIncluded": true,
          "smokingAllowed": true,
          "lastRenovationDate": "1982-04-28T00:00:00Z",
          "rating": 1,
          "location": { "type": "Point", "coordinates": [-122.131577, 49.678581] }
        },
        {
          "@search.action": "merge",
          "hotelId": "3",
          "baseRate": 279.99,
          "description": "Surprisingly expensive",
          "lastRenovationDate": null
        },
        {
          "@search.action": "delete",
          "hotelId": "4"
        }
      ]
    }
- - -
<a name="SearchDocs"></a>

## <a name="search-documents"></a>Search Documents
A **recherche** opération s’affiche comme une demande GET ou POST et spécifie les paramètres qui contiennent des critères de hello pour la sélection des documents correspondants.

    GET https://[service name].search.windows.net/indexes/[index name]/docs?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/search?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

**Lorsque toouse VALIDEZ au lieu de GET**

Lorsque vous utilisez HTTP GET les hello toocall **recherche** API, vous devez toobe conscient que hello hello URL de demande ne peut pas dépasser 8 Ko. Cela est généralement suffisamment pour la plupart des applications. Toutefois, certaines applications produisent des requêtes très volumineuses ou des expressions de filtre OData. Pour ces applications, il est recommandé d'utiliser HTTP POST, car cela permet d'obtenir des filtres et des requêtes plus volumineux que GET. Avec POST, nombre hello des clauses dans une requête hello limitent facteur, la taille de hello pas des requêtes brutes de hello, car la limite de taille de demande de hello POST est d’environ 16 Mo.

> [!NOTE]
> Bien que la limite de taille de demande POST hello est très important, les requêtes de recherche et les expressions de filtre ne peut pas être arbitrairement complexes. Consultez [Syntaxe de requête Lucene](https://msdn.microsoft.com/library/mt589323.aspx) et [Syntaxe d’expression OData](https://msdn.microsoft.com/library/dn798921.aspx) pour plus d’informations sur les limites de la complexité des filtres et des requêtes de recherche.
> 
> 

**Requête**

Le protocole HTTPS est requis pour les requêtes de service. Hello **recherche** demande peut être construite à l’aide de hello GET ou la méthode POST.

URI de demande Hello spécifie quels index tooquery, pour tous les documents qui correspondent aux paramètres de hello. Paramètres sont spécifiés dans la chaîne de requête hello dans les cas de hello de demandes GET, et dans la demande hello corps dans les cas de hello de demande.

Comme meilleure pratique lors de la création de demandes GET, n’oubliez pas trop[encoder en URL](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) paramètres lors de l’appel hello directement les API REST de requête spécifique. Pour les opérations de **recherche** , cela inclut :

* `$filter`
* `facet`
* `highlightPreTag`
* `highlightPostTag`
* `search`
* `moreLikeThis`

L’encodage d’URL est recommandée uniquement sur hello au-dessus de paramètres de requête. Si vous par inadvertance encoder en URL hello la chaîne de requête entière (tout ce qui suit hello ?), les demandes s’interrompent.

En outre, l’encodage d’URL est nécessaire uniquement lors de l’appel hello obtenir de l’API REST directement à l’aide. Aucun encodage d’URL n’est nécessaire lors de l’appel **recherche** à l’aide de POST, ou lorsque vous utilisez hello [bibliothèque cliente .NET](https://msdn.microsoft.com/library/dn951165.aspx), qui gère l’encodage d’URL pour vous.

<a name="SearchQueryParameters"></a>
**Paramètres de requête**

**Search** accepte plusieurs paramètres qui fournissent les critères de la requête et qui spécifient également le comportement de la recherche. Vous fournissez ces paramètres dans l’URL de hello la chaîne de requête lors de l’appel **recherche** via GET et en tant que propriétés JSON dans le corps de la demande hello lors de l’appel **recherche** via la publication. syntaxe Hello pour certains paramètres est légèrement différente entre GET et POST. Ces différences sont indiquées ci-dessous :

`search=[string]`(facultatif) : hello toosearch de texte pour. Tous les champs `searchable` sont interrogés par défaut, sauf si `searchFields` est spécifié. Lors de la recherche `searchable` champs, rechercher du texte hello lui-même est tokenisé plusieurs termes peuvent être séparés par un espace blanc (par exemple : `search=hello world`). utilisation de tout terme, toomatch `*` (qui peut être utile pour les requêtes de filtre booléen). L’omission de ce paramètre est hello même effet que sa définition trop`*`. Consultez [syntaxe de requête Simple](https://msdn.microsoft.com/library/dn798920.aspx) pour plus de détails sur la syntaxe de recherche hello.

* **Remarque**: hello résultats peuvent parfois être surprenant lors de l’interrogation sur `searchable` champs. Générateur de jetons Hello inclut logique toohandle cas courants tooEnglish texte tels que les apostrophes, les virgules des nombres, etc.. Par exemple, `search=123,456` correspond à un terme 123,456 plutôt que des termes hello 123 et 456, étant donné que les virgules sont utilisées comme séparateurs de milliers de grands nombres en anglais. Pour cette raison, nous recommandons d’utiliser un espace blanc plutôt que des termes du contrat de ponctuation tooseparate Bonjour `search` paramètre.

`searchMode=any|all`(facultatif, par défaut est trop`any`) : indique si tout ou partie des termes de recherche hello doivent correspondre dans le document de hello toocount commande comme une correspondance.

`searchFields=[string]`(facultatif) : liste hello de toosearch de noms de champ séparées par des virgules pour hello le texte spécifié. Les champs cibles doivent être marqués comme `searchable`.

`queryType=simple|full`(facultatif, par défaut est trop`simple`) : lorsque le texte du jeu de recherche trop « simple » est interprété à l’aide d’un langage de requête simple qui permet des symboles, tels que +, * et « ». Les requêtes sont évaluées pour tous les champs pouvant faire l’objet d’une recherche (ou les champs indiqués dans `searchFields`) dans chaque document par défaut. Lorsque le type de requête hello est défini trop`full` rechercher du texte est interprété à l’aide du langage de requête Lucene hello qui permet des recherches spécifiques aux champs et pondérées. Consultez [syntaxe de requête Simple](https://msdn.microsoft.com/library/dn798920.aspx) et [syntaxe de requête Lucene](https://msdn.microsoft.com/library/mt589323.aspx) pour plus de détails sur les syntaxes de recherche hello. 

> [!NOTE]
> Plage recherche Bonjour Lucene langage de requête n’est pas pris en charge en faveur $filter qui offre des fonctionnalités similaires.
> 
> 

`moreLikeThis=[key]` (facultatif) **Important :** cette fonctionnalité est uniquement disponible dans `2015-02-28-Preview`. Cette option ne peut pas être utilisée dans une requête qui contient le paramètre de recherche de texte hello, `search=[string]`. Hello `moreLikeThis` paramètre trouve les documents qui sont similaires toohello document spécifié par la clé de document hello. Lorsqu’une demande de recherche est effectuée avec `moreLikeThis`, une liste de termes de recherche est générée en fonction de la fréquence de hello et rareté de termes dans le document d’origine hello. Ces termes sont utilisé toomake hello demande. Par défaut, hello le contenu de tous les `searchable` champs sont considérés comme sauf si `searchFields` est utilisé toorestrict des champs de recherche.  

`$skip=#`(facultatif) : nombre de hello de recherche résultats tooskip ; Ne peut pas être supérieur à 100 000. Si vous devez tooscan des documents dans l’ordre, mais ne pouvez pas utiliser `$skip` en raison de la limitation de toothis, envisagez d’utiliser `$orderby` sur une clé totalement ordonnée et `$filter` avec une plage de requête à la place.

> [!NOTE]
> Lors de l’appel de **Search** à l’aide de POST, ce paramètre est nommé `skip` au lieu de `$skip`.
> 
> 

`$top=#`(facultatif) : nombre de hello de recherche résultats tooretrieve. Cela peut être utilisé conjointement avec `$skip` tooimplement une pagination côté client des résultats de recherche.

> [!NOTE]
> Lors de l’appel de **Search** à l’aide de POST, ce paramètre est nommé `top` au lieu de `$top`.
> 
> 

`$count=true|false`(facultatif, par défaut est trop`false`)-Spécifie si toofetch hello nombre total de résultats. Il s’agit nombre hello de tous les documents qui correspondent aux hello `search` et `$filter` paramètres, en ignorant `$top` et `$skip`. Ce paramètre trop`true` peut avoir un impact sur les performances. Notez que le nombre de hello retourné est une approximation.

> [!NOTE]
> Lors de l’appel de **Search** à l’aide de POST, ce paramètre est nommé `count` au lieu de `$count`.
> 
> 

`$orderby=[string]`(facultatif) : une liste de résultats de hello toosort séparées par des virgules des expressions par. Chaque expression peut être un nom de champ ou d’un appel toohello `geo.distance()` (fonction). Chaque expression peut être suivie `asc` tooindicated par ordre croissant, et `desc` tooindicate décroissant. valeur par défaut Hello est l’ordre croissant. Les liens sont rompus par scores de correspondance hello de documents. Si aucun `$orderby` est spécifié, l’ordre de tri par défaut hello décroissant par score de correspondance. Il existe une limite de 32 clauses pour `$orderby`.

> [!NOTE]
> Lors de l’appel de **Search** à l’aide de POST, ce paramètre est nommé `orderby` au lieu de `$orderby`.
> 
> 

`$select=[string]`(facultatif) : une liste de champs séparés par des virgules tooretrieve. Si non spécifié, tous les champs marqués comme récupérables dans le schéma de hello sont inclus. Vous pouvez également demander explicitement tous les champs en définissant ce paramètre trop`*`.

> [!NOTE]
> Lors de l’appel de **Search** à l’aide de POST, ce paramètre est nommé `select` au lieu de `$select`.
> 
> 

`facet=[string]`(zéro ou plus) - un toofacet de champ par. Chaîne de hello peut contenir des facettes hello paramètres toocustomize exprimée sous la forme séparées par des virgules `name:value` paires. Les paramètres valides sont les suivants :

* `count` (nombre maximal de termes de facette ; la valeur par défaut est 10). Il n’existe pas de maximum, mais les valeurs plus élevées entraînent une baisse des performances correspondante, en particulier si le champ à facettes de hello contient un grand nombre de termes uniques.
  * Par exemple : `facet=category,count:5` obtient hello cinq catégories dans les résultats de facette.  
  * **Remarque**: si hello `count` paramètre est inférieur au nombre de hello de termes uniques, les résultats de hello ne peuvent pas être précis. Il s’agit en raison de la façon de toohello les requêtes par facettes sont distribuées entre plusieurs partitions. Augmentation `count` généralement augmente hello précision hello des nombres de termes, mais au détriment des performances.
* `sort`(un des `count` toosort *décroissant* par nombre, `-count` toosort *croissant* par nombre, `value` toosort *croissant* par valeur, ou `-value` toosort *décroissant* par valeur)
  * Par exemple : `facet=category,count:3,sort:count` obtient hello trois premières catégories dans les résultats de facette dans l’ordre décroissant par numéro hello de documents contenant le nom de chaque ville. Par exemple, si hello trois premières catégories sont Budget, hôtel et luxe, Budget recueille 5 correspondances, hôtel 6, et luxe 4, puis hello compartiments sera dans l’ordre de hello hôtel, Budget et luxe.
  * Par exemple : `facet=rating,sort:-value` génère des compartiments pour tous les classements possibles, triés par ordre décroissant des valeurs. Par exemple, si les évaluations de hello vont de 1 too5, hello ordre des compartiments est 5, 4, 3, 2, 1, quel que soit le nombre de documents correspondant à chaque évaluation.
* `values` (valeur numérique délimitée une barre verticale ou valeurs `Edm.DateTimeOffset` qui spécifient un ensemble dynamique de valeurs d'entrée de facette)
  * Par exemple : `facet=baseRate,values:10|20` produit trois compartiments : une pour le taux de base 0 des toobut non compris 10, l’autre pour 10 haut toobut non compris 20 et pour supérieur ou égal à 20.
  * Par exemple : `facet=lastRenovationDate,values:2010-02-01T00:00:00Z` génère deux compartiments : un pour les hôtels rénovés avant février 2010 et un pour les hôtels rénovés à partir du 1er février 2010.
* `interval` (intervalle d'entiers supérieur à 0 pour les nombres ou `minute`, `hour`, `day`, `week`, `month`, `quarter`, `year` pour les valeurs de date et heure)
  * Par exemple : `facet=baseRate,interval:100` génère des compartiments basés sur des plages de taux de base comprenant 100 valeurs. Par exemple, si les taux de base sont tous compris entre 60 dollars et 600 dollars, il y aura les compartiments suivants : 0-100, 100-200, 200-300, 300-400, 400-500 et 500-600.
  * Par exemple : `facet=lastRenovationDate,interval:year` génère un compartiment pour chaque année de rénovation des hôtels.
* `timeoffset` ([+-]hh:mm, [+-]hhmm, ou [+-]hh) `timeoffset` est facultatif. Il peut uniquement être combiné avec hello `interval` option et uniquement lorsqu’un champ de type tooa appliqué `Edm.DateTimeOffset`. valeur de Hello spécifie tooaccount de décalage de temps hello UTC pour lors de la définition des limites de temps.
  * Par exemple : `facet=lastRenovationDate,interval:day,timeoffset:-01:00` utilise hello limite jour commençant à 01:00:00 UTC (minuit sur fuseau horaire de hello cible)
* **Remarque**: `count` et `sort` peuvent être combinés dans hello même spécification de facette, mais ils ne peuvent pas être combiné avec `interval` ou `values`, et `interval` et `values` ne peut pas être combinées.
* **Remarque** : les facettes d’intervalle de date et d’heure sont calculées en fonction de l’heure UTC si `timeoffset` n’est pas spécifié. Par exemple : pour `facet=lastRenovationDate,interval:day`, limite de jour hello commence à 00:00:00 UTC. 

> [!NOTE]
> Lors de l’appel de **Search** à l’aide de POST, ce paramètre est nommé `facets` au lieu de `facet`. En outre, vous le spécifiez sous forme de tableau JSON de chaînes où chaque chaîne est une expression de facette distincte.
> 
> 

`$filter=[string]` (facultatif) : expression de recherche structurée avec une syntaxe OData standard.

> [!NOTE]
> Lors de l’appel de **Search** à l’aide de POST, ce paramètre est nommé `filter` au lieu de `$filter`.
> 
> 

`highlight=[string]` (facultatif) : ensemble de noms de champ séparés par des virgules pour la mise en surbrillance des correspondances. Seuls les champs `searchable` peuvent être utilisés pour la mise en surbrillance des correspondances.

`highlightPreTag=[string]`(facultatif, par défaut est trop`<em>`) - une balise qui ajoute des mises en surbrillance toohit de chaîne. Doit être défini avec `highlightPostTag`.

> [!NOTE]
> Lors de l’appel **recherche** à l’aide de GET, les caractères réservés dans les URL hello doivent être encodés en pourcentage (par exemple, %23 au lieu de #).
> 
> 

`highlightPostTag=[string]`(facultatif, par défaut est trop`</em>`)-une balise de chaîne qui ajoute des mises en surbrillance toohit. Doit être défini avec `highlightPreTag`.

> [!NOTE]
> Lors de l’appel **recherche** à l’aide de GET, les caractères réservés dans les URL hello doivent être encodés en pourcentage (par exemple, %23 au lieu de #).
> 
> 

`scoringProfile=[string]`(facultatif) - nom hello d’un calcul de score tooevaluate de profil mettre en correspondance les scores de correspondance des documents dans les résultats de commande toosort hello.

`scoringParameter=[string]`(zéro ou plus) - indique les valeurs hello pour chaque paramètre défini dans une fonction de calcul de score (par exemple, `referencePointParameter`) à l’aide du format de hello `name-value1,value2,...`.

* Par exemple, si hello profil de calcul de score définit une fonction avec un paramètre appelé l’option de chaîne de requête « mylocation » hello serait `&scoringParameter=mylocation--122.2,44.8`. tiret de première Hello sépare les nom de hello à partir de la liste des valeurs hello, tandis que le tiret de deuxième hello fait partie de la première valeur de hello (longitude dans cet exemple).
* Pour les paramètres de calcul de score comme balise boosting qui peut contenir des virgules, échapper tout ces valeurs dans la liste de hello à l’aide de guillemets simples. Si les valeurs hello elles-mêmes contiennent des guillemets simples, vous pouvez d’échappement en doublant.
  * Par exemple, si vous disposez d’une balise de renforcement de paramètre nommé « mytag » et que vous souhaitez tooboost sur la balise de hello les valeurs « Hello, o ' Brien » et « Smith », la requête de hello chaîne option serait `&scoringParameter=mytag-'Hello, O''Brien',Smith`. Notez que les guillemets sont uniquement requis pour les valeurs qui contiennent des virgules.

> [!NOTE]
> Lors de l’appel de **Search** à l’aide de POST, ce paramètre est nommé `scoringParameters` au lieu de `scoringParameter`. En outre, vous le spécifiez sous forme de tableau JSON de chaînes où chaque chaîne est une paire `name-values` distincte.
> 
> 

`minimumCoverage`(facultatif, par défaut est too100) - un nombre compris entre 0 et 100 qui indique le pourcentage hello d’index hello qui doit être couvert par une requête de recherche dans l’ordre pour hello requête toobe signalée comme un succès. Par défaut, la totalité de l’index hello doit être disponible ou `Search` renvoie le code d’état HTTP 503. Si vous définissez `minimumCoverage` et `Search` réussit, elle retourne HTTP 200 et inclure une `@search.coverage` valeur dans la réponse hello indiquant le pourcentage de hello d’index hello qui a été inclus dans la requête de hello.

> [!NOTE]
> Ce paramètre paramètre tooa inférieur à 100 peut être utile pour garantir la disponibilité de recherche même pour les services avec un seul. Toutefois, pas tous les documents correspondants sont garanties toobe présent dans les résultats de recherche hello. Si le rappel de recherche est l’application tooyour plus importante que la disponibilité, il est meilleure tooleave `minimumCoverage` sa valeur par défaut de 100.
> 
> 

`api-version=[string]` (obligatoire). version d’évaluation Hello `api-version=2015-02-28-Preview`. Pour plus d'informations, y compris sur d'autres versions, consultez [Contrôle de version de service Azure Search](http://msdn.microsoft.com/library/azure/dn864560.aspx) .

Remarque : Pour cette opération, hello `api-version` est spécifié comme un paramètre de requête dans l’URL de hello indépendamment de si vous appelez **recherche** POST ou GET.

**En-têtes de requête**

Hello suivant liste décrit hello requis et les en-têtes de demande facultatif.

* `api-key`: hello `api-key` est utilisé tooauthenticate hello demande tooyour service de recherche. Il est une valeur de chaîne URL du service tooyour unique. Hello **recherche** demande peut spécifier une clé d’administration ou une clé de requête pour `api-key`.

Vous devez également les URL de demande du nom tooconstruct hello hello service. Vous pouvez obtenir le nom du service hello et `api-key` à partir de votre tableau de bord de service Bonjour portail Azure. Consultez [créer un service Azure Search dans le portail de hello](search-create-service-portal.md) de l’aide de navigation de page.

**Corps de la requête**

Pour GET : aucun.

Pour POST :

    {
      "count": true | false (default),
      "facets": [ "facet_expression_1", "facet_expression_2", ... ],
      "filter": "odata_filter_expression",
      "highlight": "highlight_field_1, highlight_field_2, ...",
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered toodeclare query successful; default 100),
      "moreLikeThis": "document_key" (mutually exclusive with "search" parameter),
      "orderby": "orderby_expression",
      "scoringParameters": [ "scoring_parameter_1", "scoring_parameter_2", ... ],
      "scoringProfile": "scoring_profile_name",
      "search": "simple_query_expression",
      "searchFields": "field_name_1, field_name_2, ...",
      "searchMode": "any" (default) | "all",
      "select": "field_name_1, field_name_2, ...",
      "skip": # (default 0),
      "top": #
    }

**Continuation des réponses de recherche partielle**

Parfois, Azure Search ne peut pas retourner que toutes les hello résultats demandés dans une réponse de recherche unique. Cela peut se produire pour différentes raisons, telles que lorsque hello requête trop grand nombre de documents en ne spécifiant `$top` ou en spécifiant une valeur pour `$top` qui est trop grande. Dans ce cas, Azure Search inclura hello `@odata.nextLink` annotation dans le corps de réponse hello et également `@search.nextPageParameters` s’il s’agissait d’une demande POST. Vous pouvez utiliser les valeurs de ces tooformulate annotations hello une autre recherche demande tooget hello partie suivante de la réponse de recherche hello. Cela s’appelle un ***continuation*** de demande de recherche d’origine hello et hello annotations sont généralement appelées ***jetons de continuation***. Consultez [exemple hello ci-dessous](#SearchResponse) pour plus d’informations sur la syntaxe hello de ces annotations et où ils apparaissent dans le corps de la réponse hello. 

raisons Hello pourquoi Azure Search peut renvoyer des jetons de continuation sont spécifiques à l’implémentation et l’objet toochange. Les clients robustes doivent toujours être prêt toohandle cas où les documents moins que prévu sont retournés et un jeton de liaison toocontinue inclus, la récupération de documents. Également Notez que vous devez utiliser hello même méthode HTTP en tant que requête d’origine de hello dans l’ordre toocontinue. Par exemple, si vous avez envoyé une demande GET, toutes les demandes de continuation que vous envoyez doivent également utiliser GET (y compris pour POST).

<a name="SearchResponse"></a>
**Réponse**

Code d'état : 200 OK est retourné pour une réponse correcte.

    {
      "@odata.count": # (if $count=true was provided in hello query),
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "@search.facets": { (if faceting was specified in hello query)
        "facet_field": [
          {
            "value": facet_entry_value (for non-range facets),
            "from": facet_entry_value (for range facets),
            "to": facet_entry_value (for range facets),
            "count": number_of_documents
          }
        ],
        ...
      },
      "@search.nextPageParameters": { (request body toofetch hello next page of results if not all results could be returned in this response and Search was called with POST)
        "count": ... (value from request body if present),
        "facets": ... (value from request body if present),
        "filter": ... (value from request body if present),
        "highlight": ... (value from request body if present),
        "highlightPreTag": ... (value from request body if present),
        "highlightPostTag": ... (value from request body if present),
        "minimumCoverage": ... (value from request body if present),
        "moreLikeThis": ... (value from request body if present),
        "orderby": ... (value from request body if present),
        "scoringParameters": ... (value from request body if present),
        "scoringProfile": ... (value from request body if present),
        "search": ... (value from request body if present),
        "searchFields": ... (value from request body if present),
        "searchMode": ... (value from request body if present),
        "select": ... (value from request body if present),
        "skip": ... (page size plus value from request body if present),
        "top": ... (value from request body if present minus page size),
      },
      "value": [
        {
          "@search.score": document_score (if a text query was provided),
          "@search.highlights": {
            field_name: [ subset of text, ... ],
            ...
          },
          key_field_name: document_key,
          field_name: field_value (retrievable fields or specified projection),
          ...
        },
        ...
      ],
      "@odata.nextLink": (URL toofetch hello next page of results if not all results could be returned in this response; Applies tooboth GET and POST)
    }

**Exemples :**

Vous trouverez des exemples supplémentaires sur hello [syntaxe d’Expression OData pour Azure Search](https://msdn.microsoft.com/library/azure/dn798921.aspx) page.

1)    Hello de recherche Index triés par ordre décroissant par date.

    GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "orderby": "lastRenovationDate desc" }

2)    Dans une recherche à facettes, rechercher les index hello et récupérer des facettes de catégories, évaluation, balises, ainsi que les éléments avec la valeur baserate s’inscrit dans des plages spécifiques :

    GET /indexes/hotels/docs?search=test&facet=category&facet=rating&facet=tags&facet=baseRate,values:80|150|220&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "category", "rating", "tags", "baseRate,values:80|150|220" ] }

3)    À l’aide d’un filtre, affiner les résultats de requête à facettes précédents hello après hello utilisateur clique sur évaluation 3 et la catégorie « Motel » :

    GET /indexes/hotels/docs?search=test&facet=tags&facet=baseRate,values:80|150|220&$filter=rating eq 3 and category eq 'Motel'&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "tags", "baseRate,values:80|150|220" ], "filter": "rating eq 3 and category eq 'Motel'" }

4) Dans une recherche à facettes, définir une limite supérieure sur des termes uniques retournés dans une requête. Hello par défaut 10, mais vous pouvez augmenter ou diminuer cette valeur à l’aide de hello `count` paramètre sur hello `facet` attribut :

    GET /indexes/hotels/docs?search=test&facet=city,count:5&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "test",    "facets": [ "city,count:5" ]  }

5)    Rechercher hello Index dans des domaines spécifiques. Par exemple, il s’agit d’un champ spécifique au langage :

    GET /indexes/hotels/docs?search=hôtel&searchFields=description_fr&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "hôtel", "searchFields": "description_fr" }

6) Hello Index dans plusieurs champs de recherche. Par exemple, vous pouvez stocker et champs de requête recherche dans plusieurs langues, toutes les tâches dans hello même index.  Si des descriptions en anglais et Français coexistent dans hello même document, vous pouvez retourner tout ou partie hello dans résultats de la requête :

    GET /indexes/hotels/docs?search=hotel&searchFields=description,description_fr&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "hotel",    "searchFields": "description, description_fr"  }

Notez que vous pouvez interroger uniquement un index à la fois. Ne créez pas plusieurs index pour chaque langue, sauf si vous prévoyez tooquery une à la fois.

7)    Pagination - Get hello 1ère page d’éléments (taille de page est 10) :

    GET /indexes/hotels/docs?search=*&$skip=0&$top=10&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 0, "top": 10 }

8)    Pagination - Get hello 2ème page d’éléments (taille de page est 10) :

    GET /indexes/hotels/docs?search=*&$skip=10&$top=10&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 10, "top": 10 }

9)    Récupérer un ensemble spécifique de champs :

    GET /indexes/hotels/docs?search=*&$select=hotelName,description&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "select": "hotelName, description" }

10)  Récupérer les documents correspondant à une expression de filtre spécifique :

    GET /indexes/hotels/docs?$filter=(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {  "filter": "(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'" }

11) Index de recherche hello et des fragments de retournés avec des surlignages

    GET /indexes/hotels/docs?search=something&highlight=description&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "highlight": "description" }

12) Index de recherche hello et documents triés du plus proche toofarther en dehors d’un emplacement de référence de retour

    GET /indexes/hotels/docs?search=something&$orderby=geo.distance(location, geography'POINT(-122.12315 47.88121)')&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "orderby": "geo.distance(location, geography'POINT(-122.12315 47.88121)')" }

13) Recherche hello index en supposant qu’il est un profil de score appelé « geo » avec deux fonctions de score de distance, une définition d’un paramètre nommé « currentlocation » et une définition d’un paramètre nommé « lastLocation »

    GET /indexes/hotels/docs?search=something&scoringProfile=geo&scoringParameter=currentLocation--122.123,44.77233&scoringParameter=lastLocation--121.499,44.2113&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "scoringProfile": "geo",   "scoringParameters": [ "currentLocation--122.123,44.77233", "lastLocation--121.499,44.2113" ] }

14) Rechercher des documents à l’aide d’index hello [syntaxe de requête simple](https://msdn.microsoft.com/library/dn798920.aspx). Cette requête renvoie les hôtels où les champs interrogeables contiennent hello termes « comfort » et « location » mais pas « motel » :

    GET /indexes/hotels/docs?search=comfort +location -motel&searchMode=all&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "comfort +location -motel",   "searchMode": "all" }

Notez que hello `searchMode=all` ci-dessus. Ce paramètre remplace hello comme valeur par défaut `searchMode=any`, en s’assurant que `-motel` signifie « Et pas » au lieu de « OR NOT ». Sans `searchMode=all`, vous obtenez « OR NOT » qui s’étend au lieu de limite les résultats de recherche, et cela peut être contre-intuitif toosome utilisateurs.

15) Rechercher des documents à l’aide d’index hello [syntaxe de requête lucene](https://msdn.microsoft.com/library/mt589323.aspx). Cette requête renvoie les hôtels où le champ de catégorie hello contient le terme hello « budget » et tous les champs contenant la phrase hello « récemment rénovée ». Les documents contenant « récemment rénovée » de la phrase hello rang supérieur à la suite de valeur de renforcement de terme hello (3)

    GET /indexes/hotels/docs?search=category:budget AND \"recently renovated\"^3&searchMode=all&api-version=2015-02-28-Preview&querytype=full

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "category:budget AND \"recently renovated\"^3",   "queryType": "full",   "searchMode": "all" }

<a name="LookupAPI"></a>

## <a name="lookup-document"></a>Recherche de document
Hello **recherche de Document** opération récupère un document à partir d’Azure Search. Cela est utile lorsqu’un utilisateur clique sur un résultat de recherche, et que vous souhaitez toolook des détails spécifiques sur ce document.

    GET https://[service name].search.windows.net/indexes/[index name]/docs/[key]?[query parameters]
    api-key: [admin or query key]

**Requête**

Le protocole HTTPS est requis pour les requêtes de service. Hello **recherche de Document** demande peut être construite comme suit.

    GET /indexes/[index name]/docs/key?[query parameters]

Vous pouvez également utiliser la syntaxe OData traditionnelle de hello pour la recherche de clé :

    GET /indexes('[index name]')/docs('[key]')?[query parameters]

Hello URI de requête inclut un [nom d’index] et [clé], en spécifiant le tooretrieve de document à partir de l’index. Vous ne pouvez obtenir qu'un seul document à la fois. Utilisez **recherche** tooget plusieurs documents dans une demande unique.

**Paramètres de requête**

`$select=[string]`(facultatif) : une liste de champs séparés par des virgules tooretrieve. Si non spécifié ou défini trop`*`, tous les champs marqués comme récupérables dans le schéma de hello sont inclus dans la projection de hello.

`api-version=[string]` (obligatoire). version d’évaluation Hello `api-version=2015-02-28-Preview`. Pour plus d'informations, y compris sur d'autres versions, consultez [Contrôle de version de service Azure Search](http://msdn.microsoft.com/library/azure/dn864560.aspx) .

Remarque : Pour cette opération, hello `api-version` est spécifié comme un paramètre de requête.

**En-têtes de requête**

Hello suivant liste décrit hello requis et les en-têtes de demande facultatif.

* `api-key`: hello `api-key` est utilisé tooauthenticate hello demande tooyour service de recherche. Il est une valeur de chaîne URL du service tooyour unique. Hello **recherche de Document** demande peut spécifier une clé d’administration ou une clé de requête pour `api-key`.

Vous devez également les URL de demande du nom tooconstruct hello hello service. Vous pouvez obtenir le nom du service hello et `api-key` à partir de votre tableau de bord de service Bonjour portail Azure. Consultez [créer un service Azure Search dans le portail de hello](search-create-service-portal.md) de l’aide de navigation de page.

**Corps de la requête**

Aucune.

**Réponse**

Code d'état : 200 OK est retourné pour une réponse correcte.

    {
      field_name: field_value (fields matching hello default or specified projection)
    }

**Exemple**

Recherche de document hello ayant la clé « 2 »

    GET /indexes/hotels/docs/2?api-version=2015-02-28-Preview

Recherche de document hello ayant la clé « 3 » à l’aide de la syntaxe OData :

    GET /indexes('hotels')/docs('3')?api-version=2015-02-28-Preview

<a name="CountDocs"></a>

## <a name="count-documents"></a>Nombre de documents
Hello **nombre de Documents** opération récupère le nombre de hello de documents dans un index de recherche. Hello `$count` syntaxe fait partie du protocole OData de hello.

    GET https://[service name].search.windows.net/indexes/[index name]/docs/$count?api-version=[api-version]
    Accept: text/plain
    api-key: [admin or query key]

**Requête**

Le protocole HTTPS est requis pour les requêtes de service. Hello **nombre de Documents** demande peut être construite à l’aide de la méthode GET de hello.

Bonjour [nom de l’index] dans l’URI de la demande hello indique hello service tooreturn un nombre de tous les éléments dans la collection de documents hello de l’index spécifié de hello.

`api-version=[string]` (obligatoire). version d’évaluation Hello `api-version=2015-02-28-Preview`. Pour plus d'informations, y compris sur d'autres versions, consultez [Contrôle de version de service Azure Search](http://msdn.microsoft.com/library/azure/dn864560.aspx) .

**En-têtes de requête**

Hello suivant liste décrit hello requis et les en-têtes de demande facultatif.

* `Accept`: Cette valeur doit être définie trop`text/plain`.
* `api-key`: hello `api-key` est utilisé tooauthenticate hello demande tooyour service de recherche. Il est une valeur de chaîne URL du service tooyour unique. Hello **nombre de Documents** demande peut spécifier une clé d’administration ou une clé de requête pour `api-key`.

Vous devez également les URL de demande du nom tooconstruct hello hello service. Vous pouvez obtenir le nom du service hello et `api-key` à partir de votre tableau de bord de service Bonjour portail Azure. Consultez [créer un service Azure Search dans le portail de hello](search-create-service-portal.md) de l’aide de navigation de page.

**Corps de la requête**

Aucune.

**Réponse**

Code d'état : 200 OK est retourné pour une réponse correcte.

corps de réponse de Hello contient la valeur du nombre de hello en tant qu’entier au format texte brut.

<a name="Suggestions"></a>

## <a name="suggestions"></a>Suggestions
Hello **Suggestions** opération récupère des suggestions basées sur l’entrée de recherche partielle. Il est généralement utilisé dans les suggestions de recherche boîtes tooprovide prédictives que les utilisateurs entrent des termes de recherche.

Demandes de suggestions visant à suggérer des documents cibles, donc hello suggéré de texte peut être répété si plusieurs documents candidats correspondent hello même entrée de recherche. Vous pouvez utiliser `$select` tooretrieve autres champs (y compris la clé de document hello) de document afin que vous sachiez quel document constitue la source de hello de chaque suggestion.

Une opération **Suggestions** est publiée en tant que requête GET ou POST.

    GET https://[service name].search.windows.net/indexes/[index name]/docs/suggest?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/suggest?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

**Lorsque toouse VALIDEZ au lieu de GET**

Lorsque vous utilisez HTTP GET les hello toocall **Suggestions** API, vous devez toobe conscient que hello hello URL de demande ne peut pas dépasser 8 Ko. Cela est généralement suffisamment pour la plupart des applications. Toutefois, certaines applications produisent des requêtes très volumineuses, en particulier les expressions de filtre OData. Pour ces applications, il est recommandé d'utiliser HTTP POST, car cela permet d'obtenir des filtres plus volumineux que GET. Avec POST, hello de clauses dans un filtre de facteur de limitation hello, ne Hello pas de taille de la chaîne de filtre brutes hello, car la limite de taille de demande de hello POST est d’environ 16 Mo.

> [!NOTE]
> Bien que la limite de taille de demande POST hello est très volumineux, les expressions de filtre ne peut pas être arbitrairement complexes. Consultez [Syntaxe d’expression OData](https://msdn.microsoft.com/library/dn798921.aspx) pour plus d’informations sur les limites de complexité des filtres.
> 
> 

**Requête**

Le protocole HTTPS est requis pour les requêtes de service. Hello **Suggestions** demande peut être construite à l’aide de hello GET ou la méthode POST.

URI de demande Hello Spécifie le nom hello de hello index tooquery. Paramètres, tels que terme recherché partiellement entré de hello, sont spécifiés dans la chaîne de requête hello dans les cas de hello de demandes GET, et dans la demande hello corps dans les cas de hello de demande.

Comme meilleure pratique lors de la création de demandes GET, n’oubliez pas trop[encoder en URL](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) paramètres lors de l’appel hello directement les API REST de requête spécifique. Pour les opérations **Suggestions** , cela inclut :

* `$filter`
* `highlightPreTag`
* `highlightPostTag`
* `search`

L’encodage d’URL est recommandée uniquement sur hello au-dessus de paramètres de requête. Si vous par inadvertance encoder en URL hello la chaîne de requête entière (tout ce qui suit hello ?), les demandes s’interrompent.

En outre, l’encodage d’URL est nécessaire uniquement lors de l’appel hello obtenir de l’API REST directement à l’aide. Aucun encodage d’URL n’est nécessaire lors de l’appel **Suggestions** à l’aide de POST, ou lorsque vous utilisez hello [bibliothèque cliente .NET](https://msdn.microsoft.com/library/dn951165.aspx), qui gère l’encodage d’URL pour vous.

**Paramètres de requête**

**Suggestions** accepte plusieurs paramètres qui fournissent les critères de la requête et qui spécifient également le comportement de la recherche. Vous fournissez ces paramètres dans l’URL de hello la chaîne de requête lors de l’appel **Suggestions** via GET et en tant que propriétés JSON dans le corps de la demande hello lors de l’appel **Suggestions** via la publication. syntaxe Hello pour certains paramètres est légèrement différente entre GET et POST. Ces différences sont indiquées ci-dessous :

`search=[string]`-hello texte toouse toosuggest requêtes. Doit comprendre 1 caractère au minimum et 100 caractères au maximum.

`highlightPreTag=[string]`(facultatif) : balise de chaîne qui ajoute des présences dans le toosearch. Doit être défini avec `highlightPostTag`.

> [!NOTE]
> Lors de l’appel **Suggestions** à l’aide de GET, les caractères réservés dans les URL hello doivent être encodés en pourcentage (par exemple, %23 au lieu de #).
> 
> 

`highlightPostTag=[string]`(facultatif) : balise de chaîne qui ajoute des présences dans le toosearch. Doit être défini avec `highlightPreTag`.

> [!NOTE]
> Lors de l’appel **Suggestions** à l’aide de GET, les caractères réservés dans les URL hello doivent être encodés en pourcentage (par exemple, %23 au lieu de #).
> 
> 

`suggesterName=[string]`-nom hello de suggestion spécifié dans hello hello `suggesters` collection qui fait partie de la définition de l’index hello. Un `suggester` détermine les champs qui sont analysés pour les termes de requête suggérés. Pour plus d'informations, consultez [Générateurs de suggestions](#Suggesters) .

`fuzzy=[boolean]`(facultatif, par défaut = false)-lorsque la valeur tootrue cette API trouve des suggestions même s’il existe un caractère erroné ou manquant dans le texte de recherche hello. Bien qu'il en résulte une meilleure expérience, dans certains cas cela a un impact négatif sur les performances, car les recherches de suggestions approximatives sont plus lentes et consomment davantage de ressources.

`searchFields=[string]`(facultatif) : liste hello de toosearch de noms de champ séparées par des virgules pour hello spécifié Rechercher du texte. Les champs cibles doivent être activés pour les suggestions.

`$top=#`(facultatif, par défaut = 5)-nombre de suggestions tooretrieve de hello. Doit être un nombre compris entre 1 et 100.

> [!NOTE]
> Pendant l’appel de **Suggestions** à l’aide de POST, ce paramètre est nommé `top` au lieu de `$top`.
> 
> 

`$filter=[string]`(facultatif) : une expression qui filtre les documents hello pris en compte pour obtenir des suggestions.

> [!NOTE]
> Pendant l’appel de **Suggestions** à l’aide de POST, ce paramètre est nommé `filter` au lieu de `$filter`.
> 
> 

`$orderby=[string]`(facultatif) : une liste de résultats de hello toosort séparées par des virgules des expressions par. Chaque expression peut être un nom de champ ou d’un appel toohello `geo.distance()` (fonction). Chaque expression peut être suivie `asc` tooindicated par ordre croissant, et `desc` tooindicate décroissant. valeur par défaut Hello est l’ordre croissant. Il existe une limite de 32 clauses pour `$orderby`.

> [!NOTE]
> Pendant l’appel de **Suggestions** à l’aide de POST, ce paramètre est nommé `orderby` au lieu de `$orderby`.
> 
> 

`$select=[string]`(facultatif) : une liste de champs séparés par des virgules tooretrieve. Si non spécifié, hello uniquement de clé de document et le texte de la suggestion est renvoyé. Vous pouvez demander explicitement tous les champs en définissant ce paramètre trop`*`.

> [!NOTE]
> Pendant l’appel de **Suggestions** à l’aide de POST, ce paramètre est nommé `select` au lieu de `$select`.
> 
> 

`minimumCoverage`(facultatif, par défaut est too80) - un nombre compris entre 0 et 100 qui indique le pourcentage hello d’index hello qui doit être couvert par une requête de suggestions dans l’ordre pour hello requête toobe signalée comme un succès. Par défaut, au moins 80 % de l’index de hello doit être disponible ou `Suggest` renvoie le code d’état HTTP 503. Si vous définissez `minimumCoverage` et `Suggest` réussit, elle retourne HTTP 200 et inclure une `@search.coverage` valeur dans la réponse hello indiquant le pourcentage de hello d’index hello qui a été inclus dans la requête de hello.

> [!NOTE]
> Ce paramètre paramètre tooa inférieur à 100 peut être utile pour garantir la disponibilité de recherche même pour les services avec un seul. Toutefois, pas toutes les suggestions de correspondance sont garanties toobe présent dans les résultats de hello. Si le rappel est l’application tooyour plus importante que la disponibilité, puis ses ne meilleures pas toolower `minimumCoverage` sous sa valeur par défaut 80.
> 
> 

`api-version=[string]` (obligatoire). version d’évaluation Hello `api-version=2015-02-28-Preview`. Pour plus d'informations, y compris sur d'autres versions, consultez [Contrôle de version de service Azure Search](http://msdn.microsoft.com/library/azure/dn864560.aspx) .

Remarque : Pour cette opération, hello `api-version` est spécifié comme un paramètre de requête dans l’URL de hello indépendamment de si vous appelez **Suggestions** POST ou GET.

**En-têtes de requête**

Hello suivant liste décrit hello requis et les en-têtes de demande facultatif

* `api-key`: hello `api-key` est utilisé tooauthenticate hello demande tooyour service de recherche. Il est une valeur de chaîne URL du service tooyour unique. Hello **Suggestions** demande peut spécifier une clé d’administration ou une clé de requête en tant que hello `api-key`.

Vous devez également les URL de demande du nom tooconstruct hello hello service. Vous pouvez obtenir le nom du service hello et `api-key` à partir de votre tableau de bord de service Bonjour portail Azure. Consultez [créer un service Azure Search dans le portail de hello](search-create-service-portal.md) de l’aide de navigation de page.

**Corps de la requête**

Pour GET : aucun.

Pour POST :

    {
      "filter": "odata_filter_expression",
      "fuzzy": true | false (default),
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered toodeclare query successful; default 80),
      "orderby": "orderby_expression",
      "search": "partial_search_input",
      "searchFields": "field_name_1, field_name_2, ...",
      "select": "field_name_1, field_name_2, ...",
      "suggesterName": "suggester_name",
      "top": # (default 5)
    }

**Réponse**

Code d'état : 200 OK est retourné pour une réponse correcte.

    {
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
        },
        ...
      ]
    }

Si l’option de projection hello est utilisé tooretrieve champs, ils sont inclus dans chaque élément du tableau de hello :

    {
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
          <other projected data fields>
        },
        ...
      ]
    }

**Exemple**

Récupérer 5 suggestions où entrée de recherche partielle hello est « lux »

    GET /indexes/hotels/docs/suggest?search=lux&$top=5&suggesterName=sg&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/suggest?api-version=2015-02-28-Preview
    {
      "search": "lux",
      "top": 5,
      "suggesterName": "sg"
    }
