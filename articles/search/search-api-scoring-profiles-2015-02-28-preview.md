---
title: "profils d’aaaScoring (Azure Search REST API Version 2015-02-28-Preview) | Documents Microsoft"
description: "Azure Search est un service de recherche cloud hébergé qui prend en charge le paramétrage des résultats classés en fonction des profils de score définis par l'utilisateur."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
ms.assetid: bfd62649-13d7-40b3-a8fa-85521a15084d
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.author: heidist
ms.date: 10/27/2016
ms.openlocfilehash: 17f83fdf6818dc6ffcc3e04f5d0185c6f646b63d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="scoring-profiles-azure-search-rest-api-version-2015-02-28-preview"></a>Profils de score (API REST Azure Search Version 2015-02-28-Preview)
> [!NOTE]
> Cet article décrit des profils de calcul de score dans hello [2015-02-28-Preview](search-api-2015-02-28-preview.md). Il n’existe actuellement aucune différence entre hello `2016-09-01` version décrite sur [MSDN](http://msdn.microsoft.com/library/azure/mt183328.aspx) et hello `2015-02-28-Preview` version décrites ici, mais nous offrons tout de même ce document dans la couverture du document de commande tooprovide entre hello API entière.
>
>

## <a name="overview"></a>Vue d'ensemble
Calcul de score fait référence toohello le calcul d’un score de recherche pour chaque élément renvoyé dans les résultats de la recherche. score de Hello est un indicateur de la pertinence d’un élément dans le contexte hello d’opération de recherche en cours hello. Hello score hello est élevé, hello plus article hello. Dans les résultats de recherche, les éléments sont toolow élevée, en fonction de score de recherche hello calculée pour chaque article classés par ordre décroissant.

Azure Search utilise par défaut de calcul de score toocompute un score initial, mais vous pouvez personnaliser le mode de calcul de hello à un profil de score. Profils de calcul de score vous donnent un plus grand contrôle sur le classement hello d’éléments dans les résultats de la recherche. Par exemple, vous pourrez tooboost les éléments en fonction de leur revenu potentiel, promouvoir les éléments les plus récents ou peut-être privilégier des éléments qui ont été trop longtemps en stock.

Un profil de score fait partie de la définition de l’index hello, composée de champs, des fonctions et des paramètres.

toogive vous une idée de ce que le profil de score ressemble, hello suivant montre un simple profil « géographique ». Celui-ci privilégie les éléments qui ont un terme de recherche hello Bonjour `hotelName` champ. Il utilise également hello `distance` toofavor les éléments qui se trouvent dans les dix kilomètres de l’emplacement actuel de hello de fonction. Si un utilisateur effectue une recherche sur le terme hello « inn » et « inn » produit la partie toobe du nom d’hôtel hello, documents dont « inn » apparaissent en hauts dans les résultats de recherche hello.

    "scoringProfiles": [
      {
        "name": "geo",
        "text": {
          "weights": { "hotelName": 5 }
        },
        "functions": [
          {
            "type": "distance",
            "boost": 5,
            "fieldName": "location",
            "interpolation": "logarithmic",
            "distance": {
              "referencePointParameter": "currentLocation",
              "boostingDistance": 10
            }
          }
        ]
      }
    ]

toouse que ce profil de score, votre requête est formulée de profil de hello toospecify hello chaîne de requête. Dans la requête de hello ci-dessous, notez le paramètre de requête hello `scoringProfile=geo` dans la demande hello.

    GET /indexes/hotels/docs?search=inn&scoringProfile=geo&scoringParameter=currentLocation--122.123,44.77233&api-version=2015-02-28-Preview

Cette requête effectue une recherche sur le terme hello « inn » et passe dans l’emplacement actuel de hello. Notez que cette requête inclut d'autres paramètres, tel que `scoringParameter`. Les paramètres de requête sont décrits dans [Recherche dans des documents (API Azure Search)](search-api-2015-02-28-preview.md#SearchDocs).

Cliquez sur [exemple](#example) tooreview un exemple plus détaillé d’un profil de score.

## <a name="what-is-default-scoring"></a>Qu'est-ce qu'un calcul de score par défaut ?
Un calcul de score détermine un score de recherche pour chaque élément dans un jeu de résultats classés par rang. Chaque élément dans un jeu de résultats de recherche est attribué un score de recherche, puis classé toolowest la plus élevée. Éléments avec des scores de hello plus élevés sont renvoyés toohello application. Par défaut, hello des 50 premiers sont retournés, mais vous pouvez utiliser hello `$top` paramètre tooreturn un nombre supérieur ou inférieur d’éléments (too1000 dans une seule réponse).

Par défaut, un score de recherche est calculé en fonction des propriétés statistiques des données de hello et requête de hello. Azure Search trouve les documents qui contiennent des termes de recherche hello dans la chaîne de requête hello (tout ou partie, en fonction de `searchMode`), en favorisant les documents qui contiennent de nombreuses instances hello du terme de recherche. Hello score de recherche augmente encore plus élevé si le terme de hello est rare dans corpus de données hello, mais courant dans le document de hello. base Hello pour cette pertinence de toocomputing approche est appelée TF-IDF ou (fréquence des termes inverse de la fréquence de document).

En supposant qu’il n’existe pas de tri personnalisé, les résultats sont classés par score de recherche avant d’être renvoyés toohello application d’appel. Si `$top` n’est pas spécifié, 50 éléments dont la recherche de la plus élevée de hello score est retourné.

Des valeurs de score de recherche peuvent être répétées dans un jeu de résultats. Par exemple, vous pouvez avoir dix éléments dont le score est 1,2, vingt éléments dont le score est 1,0, et vingt éléments dont le score est 0,5. Lorsque plusieurs correspondances ont hello même score de recherche, hello classement des mêmes éléments score n’est pas défini et n’est pas stable. Réexécutez la requête de hello, et vous pouvez voir des éléments changent de position. Si deux éléments ont un score identique, il est impossible de prédire celui qui apparaîtra en première position.

## <a name="when-toouse-custom-scoring"></a>Lors de la toouse de calcul de score personnalisé
Vous devez créer un ou plusieurs profils de calcul de score lorsque le comportement de classement de la valeur par défaut hello n’accédez suffisamment dans répond bien aux objectifs de votre entreprise. Par exemple, vous pouvez décider que la pertinence de la recherche doit privilégier les éléments récemment ajoutés. De même, il se peut qu'un champ affiche une marge bénéficiaire, ou un autre un revenu potentiel. Renforçant les correspondances qui génèrent des avantages tooyour entreprise peut être un facteur important de décider toouse profils de calcul de score.

Un classement basé sur la pertinence peut également être mis en œuvre par l'intermédiaire de profils de calcul de score. Envisagez de pages que vous avez utilisé dans hello précédente qui vous permettent de trier par prix, date, évaluation ou pertinence des résultats de recherche. Dans Azure Search, les profils de calcul de score lecteur option « pertinence » de hello. Hello définition de la pertinence est contrôlé par vous, basée sur des objectifs commerciaux et de type hello d’expérience de recherche que vous souhaitez toodeliver.

<a name="example"></a>

## <a name="example"></a>Exemple
Comme indiqué précédemment, un calcul de score personnalisé est mis en œuvre à l'aide d'un ou de plusieurs profils de calcul de score définis dans un schéma d'index.

Cet exemple affiche hello schéma d’un index avec deux profils de calcul de score (`boostGenre`, `newAndHighlyRated`). Toute requête sur cet index, qui inclut un profil comme un paramètre de requête utilisera le jeu de résultats hello profil tooscore hello.

    {
      "name": "musicstoreindex",
      "fields": [
        { "name": "key", "type": "Edm.String", "key": true },
        { "name": "albumTitle", "type": "Edm.String" },
        { "name": "albumUrl", "type": "Edm.String", "filterable": false },
        { "name": "genre", "type": "Edm.String" },
        { "name": "genreDescription", "type": "Edm.String", "filterable": false },
        { "name": "artistName", "type": "Edm.String" },
        { "name": "orderableOnline", "type": "Edm.Boolean" },
        { "name": "rating", "type": "Edm.Int32" },
        { "name": "tags", "type": "Collection(Edm.String)" },
        { "name": "price", "type": "Edm.Double", "filterable": false },
        { "name": "margin", "type": "Edm.Int32", "retrievable": false },
        { "name": "inventory", "type": "Edm.Int32" },
        { "name": "lastUpdated", "type": "Edm.DateTimeOffset" }
      ],
      "scoringProfiles": [
        {
          "name": "boostGenre",
          "text": {
            "weights": {
              "albumTitle": 1.5,
              "genre": 5,
              "artistName": 2
            }
          }
        },
        {
          "name": "newAndHighlyRated",
          "functions": [
            {
              "type": "freshness",
              "fieldName": "lastUpdated",
              "boost": 10,
              "interpolation": "quadratic",
              "freshness": {
                "boostingDuration": "P365D"
              }
            },
            {
              "type": "magnitude",
              "fieldName": "rating",
              "boost": 10,
              "interpolation": "linear",
              "magnitude": {
                "boostingRangeStart": 1,
                "boostingRangeEnd": 5,
                "constantBoostBeyondRange": false
              }
            }
          ]
        }
      ],
      "suggesters": [
        {
          "name": "sg",
          "searchMode": "analyzingInfixMatching",
          "sourceFields": ["albumTitle", "artistName"]
        }
      ]
    }


## <a name="workflow"></a>Workflow
tooimplement personnalisé calcul du score du comportement, ajoutez un calcul de score toohello schéma de profil qui définit l’index de hello. Vous pouvez avoir des profils de calcul de score too16 dans un index (voir [limites de Service](search-limits-quotas-capacity.md)), mais vous ne pouvez spécifier qu’un seul profil au moment dans une requête donnée.

Démarrer avec hello [modèle](#bkmk_template) fournies dans cette rubrique.

Donnez-lui un nom. Profils de calcul de score sont facultatifs, mais si vous ajoutez un, nom de hello est obligatoire. Être toofollow que les conventions d’affectation de noms hello pour les champs (commence par une lettre et évite les caractères spéciaux et les mots réservés). Pour en savoir plus sur les règles d'affectation des noms, consultez [Règles d'affectation des noms](http://msdn.microsoft.com/library/azure/dn857353.aspx) .

corps Hello Hello profil de calcul de score est construit à partir des champs et fonctions pondérés.

### <a name="weights"></a>Weights
Hello `weights` propriété d’un profil de score spécifie des paires nom-valeur affecter un champ tooa de pondération relative. Bonjour [exemple](#example), les champs albumTitle, genre et artistName hello sont augmentés 1.5, 5 et 2, respectivement. Pourquoi est genre augmenté est-elle beaucoup plus élevée que d’autres hello ? Si la recherche est effectuée sur des données est quelque peu homogènes (comme hello 'genre' Bonjour `musicstoreindex`), vous devrez peut-être une variance plus importante dans le poids relatif de hello. Par exemple, dans hello `musicstoreindex`, « rock » apparaît en tant que les deux un genre et dans les descriptions de genre formulées de façon identique. Si vous souhaitez la description de genre toooutweigh genre, champ de genre hello devez une pondération relative beaucoup plus élevée.

### <a name="functions"></a>Fonctions
Les fonctions sont utilisées quand des calculs supplémentaires sont nécessaires dans des contextes spécifiques. Les types de fonction valides sont `freshness`, `magnitude`, `distance` et `tag`. Chaque fonction a des paramètres qui sont tooit unique.

* `freshness`doit être utilisé lorsque vous souhaitez tooboost par un élément comment nouveau ou ancien est. Cette fonction peut être utilisée uniquement avec des champs datetime (`Edm.DataTimeOffset`). Hello de note `boostingDuration` attribut est utilisé uniquement avec la fonction d’actualisation hello.
* `magnitude`doit être utilisé lorsque vous souhaitez tooboost basé sur élevé ou faible de la valeur numérique est. Parmi les scénarios qui appellent cette fonction figurent la valorisation de la marge bénéficiaire, du prix le plus élevé, du prix le plus bas ou du nombre de téléchargements. Vous pouvez inverser la plage de hello toolow élevée, si vous souhaitez que le modèle de hello inverse (par exemple, tooboost moins chers supérieur à un prix plus élevé d’éléments). Étant donné une gamme de prix de 100 $ trop$ 1, vous devez définir `boostingRangeStart` à 100 et `boostingRangeEnd` à 1 tooboost hello moins chers. Cette fonction peut être utilisée uniquement avec des champs double et integer.
* `distance`doit être utilisé lorsque vous souhaitez tooboost par emplacement géographique ou une proximité. Cette fonction peut être utilisée uniquement avec des champs `Edm.GeographyPoint` .
* `tag`doit être utilisé lorsque vous souhaitez tooboost par des balises en commun entre des documents et des requêtes de recherche. Cette fonction peut être utilisée uniquement avec les champs `Edm.String` et `Collection(Edm.String)`.

#### <a name="rules-for-using-functions"></a>Règles d'utilisation des fonctions
* Le type de fonction (freshness, magnitude, distance, tag) doit être en lettres minuscules.
* Les fonctions ne peuvent pas contenir de valeurs null ou vides. En particulier, si vous incluez fieldname, vous devez tooset il toosomething.
* Les fonctions peuvent être uniquement appliqué toofilterable champs. Pour plus d’informations sur les champs filtrables, consultez [Création d’index](search-api-2015-02-28-preview.md#CreateIndex) .
* Les fonctions peuvent être uniquement appliqué toofields qui sont définies dans la collection de champs hello d’un index.

Après que hello index est défini, la génération des index de hello en téléchargeant le schéma d’index hello, suivi des documents. Pour obtenir des instructions sur ces opérations, consultez [Création d’index](search-api-2015-02-28-preview.md#CreateIndex) et [Ajout, mise à jour ou suppression de documents](search-api-2015-02-28-preview.md#AddOrUpdateDocuments). Une fois les index hello est généré, vous devez disposer d’un profil de score fonctionnel qui fonctionne avec vos données de recherche.

<a name="bkmk_template"></a>

## <a name="template"></a>Modèle
Cette section présente la syntaxe de hello et de modèle pour les profils de calcul de score. Consultez trop[référence de l’attribut d’Index](#bkmk_indexref) dans la section suivante de hello pour obtenir une description des attributs de hello.

    ...
    "scoringProfiles": [
      {
        "name": "name of scoring profile",
        "text": (optional, only applies toosearchable fields) {
          "weights": {
            "searchable_field_name": relative_weight_value (positive #'s),
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
            }

            // (- or -)

            "freshness": {
              "boostingDuration": "..." (value representing timespan over which boosting occurs)
            }

            // (- or -)

            "distance": {
              "referencePointParameter": "...", (parameter toobe passed in queries toouse as reference location)
              "boostingDistance": # (hello distance in kilometers from hello reference location where hello boosting range ends)
            }

            // (- or -)

            "tag": {
              "tagsParameter": "..." (parameter toobe passed in queries toospecify list of tags toocompare against target field)
            }
          }
        ],
        "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
      }
    ],
    "defaultScoringProfile": (optional) "...",
    ...

<a name="bkmk_indexref"></a>

## <a name="scoring-profile-property-reference"></a>Référence de propriété des profils de score
> [!NOTE]
> Une fonction de calcul de score peut uniquement être appliqué toofields filtrables.
>
>

| Propriété | Description |
| --- | --- |
| `name` |Obligatoire. Il s’agit de nom hello Hello profil de calcul de score. Il suit hello les mêmes conventions d’affectation de noms d’un champ. Il doit commencer par une lettre, ne peut pas contenir de points, deux-points ou @ et ne peut pas commencer par une expression de hello « azureSearch » (respectant la casse). |
| `text` |Contient la propriété de poids hello. |
| `weights` |facultatif. Paire nom-valeur spécifiant un nom de champ et une pondération relative. La pondération relative doit être un entier positif ou un nombre à virgule flottante. Vous pouvez spécifier le nom du champ hello sans pondération correspondante. Poids sont l’importance de hello utilisé tooindicate de tooanother relatif d’un champ. |
| `functions` |facultatif. Notez qu’une fonction de calcul de score peut uniquement appliqué toofields filtrables. |
| `type` |Obligatoire pour les fonctions de calcul de score. Indique le type hello de fonction toouse. Les valeurs autorisées sont `magnitude`, `freshness`, `distance` et `tag`. Vous pouvez inclure plusieurs fonctions dans chaque profil de calcul de score. nom de la fonction Hello doit être en minuscules. |
| `boost` |Obligatoire pour les fonctions de calcul de score. Nombre positif utilisé comme multiplicateur pour le score brut. Il ne peut pas être égal too1. |
| `fieldName` |Obligatoire pour les fonctions de calcul de score. Une fonction de calcul de score peut uniquement être appliqué toofields qui font partie de la collection de champs hello d’index de hello, et qui sont filtrables. De plus, chaque type de fonction fait l'objet de restrictions supplémentaires (la valeur freshness est utilisée avec des champs datetime, la valeur amplitude avec des champs integer ou double, la valeur distance avec des champs location et la valeur tag avec des champs string ou string collection). Vous pouvez spécifier un seul champ par définition de fonction. Pour exemple, la grandeur toouse deux fois de hello même profil, vous devez grandeur tooinclude deux définitions, un pour chaque champ. |
| `interpolation` |Obligatoire pour les fonctions de calcul de score. Définit la pente hello pour le hello renforcement du score augmente du début hello de fin de toohello la plage hello de plage de hello. Les valeurs autorisées sont `linear` (par défaut), `constant`, `quadratic` et `logarithmic`. Consultez la rubrique [Définition d’interpolations](#bkmk_interpolation) pour plus d’informations. |
| `magnitude` |grandeur Hello fonction de calcul de score est classements tooalter utilisés selon hello plage de valeurs pour un champ numérique. Certains des exemples d’utilisation les plus courants hello de ce sont :<ul><li>Évaluations : calcul de score hello Alter basé sur la valeur hello dans le champ « Évaluation » de hello. Lorsque deux éléments sont pertinents, élément hello avec contrôle d’accès supérieur hello est affichée en premier.</li><li>Marge : Lorsque deux documents sont pertinents, un détaillant souhaitera peut-être tooboost les documents qui ont tout d’abord les marges plus élevées.</li><li>Nombres de clics : pour les applications qui effectuent le suivi, cliquez sur dans tooproducts d’actions ou les pages, vous pouvez utiliser des éléments tooboost grandeur qui ont tendance à tooget hello plus de trafic.</li><li>Nombres de téléchargements : pour les applications qui effectuent le suivi des téléchargements, hello fonction magnitude permet de vous privilégier des éléments qui ont hello la plupart des téléchargements.</li></ul> |
| `magnitude:boostingRangeStart` |Hello de jeux valeur de début de plage hello sur laquelle la magnitude est calculé. valeur de Hello doit être un entier ou un nombre à virgule flottante. Pour des évaluations de 1 à 4, il s'agit de 1. Pour des marges de plus de 50 %, il s'agit de 50. |
| `magnitude:boostingRangeEnd` |Définit la valeur de fin de hello de plage hello sur laquelle la magnitude est calculé. valeur de Hello doit être un entier ou un nombre à virgule flottante. Pour les évaluations de 1 à 4, il s'agit de 4. |
| `magnitude:constantBoostBeyondRange` |Les valeurs autorisées sont true ou false (par défaut). Lorsque la valeur tootrue, hello les renforcement intégral continue de toodocuments tooapply qui ont une valeur pour le champ cible hello est supérieure à la limite supérieure de la plage de hello hello. Si la valeur est false, le renforcement hello de cette fonction n’est pas appliqué toodocuments dont la valeur pour le champ cible hello qui se situe en dehors de la plage de hello. |
| `freshness` |actualisation Hello fonction de calcul de score est utilisé tooalter classement des scores pour les éléments en fonction des valeurs des champs DateTimeOffset. Par exemple, un élément dont la date est plus récente peut être classé plus haut que des éléments plus anciens. (Remarque qu’il est également possible toorank éléments telles que des événements du calendrier avec des dates futures telles que toohello de plus près des éléments présents peut être classé supérieure à celle des éléments plus Bonjour futures.) Dans la version actuelle du service hello, une extrémité d’une plage de hello sera résolue toohello heure actuelle. Hello autre extrémité est une heure Bonjour passées selon hello `boostingDuration`. tooboost une plage d’heures Bonjour futures utiliser négatif `boostingDuration`. taux de Hello à quels hello renforçant les modifications à partir d’une plage minimale et maximale est déterminée par toohello d’Interpolation appliquée hello profil de calcul de score (voir figure hello ci-dessous). tooreverse hello facteur d’amplification appliqué, choisissez un facteur inférieur à 1. |
| `freshness:boostingDuration` |Définit une période d'expiration après laquelle la valorisation s'arrête pour un document spécifique. Consultez [définir boostingDuration](#bkmk_boostdur) dans la section suivante pour la syntaxe et des exemples de hello. |
| `distance` |distance Hello fonction de calcul de score est hello tooaffect utilisé score des documents en fonction de la ferme ou bien qu’ils sont emplacement géographique de référence tooa relatif. emplacement de référence Hello est indiqué en tant que partie de la requête hello dans un paramètre (à l’aide de hello `scoringParameter` paramètre de requête) comme un argument lon, LAT.. |
| `distance:referencePointParameter` |Un toobe paramètre passé dans les requêtes toouse en tant qu’emplacement de référence. scoringParameter est un paramètre de requête. Pour obtenir une description des paramètres de requête, consultez [Rechercher des documents](search-api-2015-02-28-preview.md#SearchDocs) . |
| `distance:boostingDistance` |Nombre qui indique la distance en kilomètres depuis l’emplacement de référence hello où hello plage de renforcement se termine hello. |
| `tag` |Hello balise fonction de calcul de score est utilisée en fonction de score de hello tooaffect des documents sur les balises dans des documents et des requêtes de recherche. Les documents qui ont des balises en commun avec la requête de recherche hello seront être renforcées. Hello des balises pour la requête de recherche hello est fournie comme paramètre de calcul de score dans chaque demande de recherche (à l’aide de hello `scoringParameter` paramètre de requête). |
| `tag:tagsParameter` |Un toobe paramètre passé dans les requêtes toospecify des balises pour une requête particulière. `scoringParameter` est un paramètre de requête. Pour obtenir une description des paramètres de requête, consultez [Rechercher des documents](search-api-2015-02-28-preview.md#SearchDocs) . |
| `functionAggregation` |facultatif. S'applique uniquement quand des fonctions sont spécifiées. Les valeurs autorisées sont `sum` (par défaut), `average`, `minimum`, `maximum` et `firstMatching`. Un score de recherche est une valeur unique calculée à partir de plusieurs variables, notamment plusieurs fonctions. Cet attribut indique comment les valorisations hello de toutes les fonctions hello sont combinées en un renforcement d’agrégation unique qui est ensuite appliqué toohello score du document de base. score de base Hello est basé sur la valeur de tf-idf hello est calculé à partir de documents de hello et requête de recherche hello. |
| `defaultScoringProfile` |Lors de l'exécution d'une demande de recherche, le calcul de score par défaut est utilisé (tf-idf uniquement) si aucun profil de calcul de score n'est spécifié. Nom du profil de calcul de score par défaut peut être définie ici, à l’origine de Azure Search toouse ce profil lorsque aucun profil spécifique n’est fournie dans la demande de recherche hello. |

<a name="bkmk_interpolation"></a>

## <a name="set-interpolations"></a>Définition d’interpolations
Les interpolations permettent la pente de hello toodefine pour le hello renforcement du score augmente du début hello de fin de toohello la plage hello de plage de hello. Hello suivant interpolations peut être utilisé :

* `Linear`: Pour les éléments qui sont dans hello max et min, hello valorisation appliquée toohello élément est effectuée dans un délai décroît. Linéaire est d’interpolation pour un profil de score par défaut hello.
* `Constant`: Pour les éléments qui se trouvent dans le début de hello et la fin de la plage, une valorisation constante sera appliqué toohello résultats.
* `Quadratic`: Dans la comparaison tooa utilisant une interpolation linéaire dont la valorisation décroît, Quadratic initialement à un rythme plus petit, puis en approchant de plage de fin hello, il diminue à intervalles beaucoup plus élevée. Cette option d'interpolation n'est pas autorisée dans les fonctions de calcul de score de balises.
* `Logarithmic`: Dans la comparaison tooa utilisant une interpolation linéaire dont la valorisation décroît, logarithmique initialement plus rapidement, en approchant de plage de fin hello, il revient ensuite à un intervalle de plus petit quantité. Cette option d'interpolation n'est pas autorisée dans les fonctions de calcul de score de balises.

<a name="Figure1"></a>![][1]

<a name="bkmk_boostdur"></a>

## <a name="set-boostingduration"></a>Définition de boostingDuration
`boostingDuration`est un attribut de la fonction d’actualisation hello. Vous utiliser tooset une période d’expiration après laquelle le renforcement cessera pour un document particulier. Par exemple, tooboost une ligne de produits ou nom de marque pour une période promotionnelle de 10 jours, vous devez spécifier hello 10 jours en tant que « P10D » pour les documents. Ou spécifient des événements à venir tooboost Bonjour semaine suivante «-P7D ».

`boostingDuration` doit être au format « dayTimeDuration » XSD (sous-ensemble limité d'une valeur de durée ISO 8601). modèle Hello pour cela est : `[-]P[nD][T[nH][nM][nS]]`.

Hello tableau suivant fournit plusieurs exemples.

| Duration | boostingDuration |
| --- | --- |
| 1 jour |« P1D » |
| 2 jours et 12 heures |« P2DT12H » |
| 15 minutes |« PT15M » |
| 30 jours, 5 heures 10 minutes, et 6 334 secondes |« P30DT5H10M6.334S » |

Pour plus d'exemples, consultez [Schéma XML : types de données (site Web W3.org)](http://www.w3.org/TR/xmlschema11-2/).

**Consultez également**
[API REST du service de Recherche Azure](http://msdn.microsoft.com/library/azure/dn798935.aspx) sur MSDN <br/>
[Création d’index (API de Recherche Azure)](http://msdn.microsoft.com/library/azure/dn798941.aspx) sur MSDN<br/>
[Ajouter un index de recherche tooa profil score](http://msdn.microsoft.com/library/azure/dn798928.aspx) sur MSDN<br/>

<!--Image references-->
[1]: ./media/search-api-scoring-profiles-2015-02-28-Preview/scoring_interpolations.png
