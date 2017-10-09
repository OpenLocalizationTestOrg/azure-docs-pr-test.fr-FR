---
title: aaaHow tooimplement une navigation par facettes dans Azure Search | Documents Microsoft
description: "Ajoutez une navigation par facettes tooapplications qui s’intègrent à Azure Search, un service de recherche de nuage hébergé sur Microsoft Azure."
services: search
documentationcenter: 
author: HeidiSteen
manager: mblythe
editor: 
ms.assetid: cdf98fd4-63fd-4b50-b0b0-835cb08ad4d3
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 3/10/2017
ms.author: heidist
ms.openlocfilehash: c1e6bf9dc55d0044525db79e37d35a50ded5a736
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimplement-faceted-navigation-in-azure-search"></a>Comment tooimplement une navigation par facettes dans Azure Search
La navigation à facettes est un mécanisme de filtrage qui fournit une navigation autonome d'extraction dans les applications de recherche. le terme Hello 'une navigation par facettes' peut-être être peu, mais vous avez probablement utilisé. En tant que hello suivant montre l’exemple, une navigation par facettes est rien de plus de résultats de toofilter hello catégories utilisées.

 ![Démonstration du portail de recrutement Recherche Azure][1]

Navigation par facettes est un toosearch de point d’entrée autre. Il offre une pratique tootyping autres expressions de recherche complexe manuellement. Les facettes peuvent vous aider à trouver ce que vous recherchez, tout en vous assurant d’obtenir au moins un résultat. En tant que développeur, les facettes vous permettent d’exposer des critères de recherche plus utiles hello pour naviguer dans votre corpus de recherche. Dans les applications de vente au détail en ligne, la navigation à facettes repose souvent sur les marques, les catégories (chaussures pour enfants), la taille, le prix, la popularité et les évaluations. 

L’implémentation de la navigation par facettes varie en fonction des technologies de recherche. Dans Recherche Azure, la navigation à facettes est créée au moment de la requête, à l’aide de champs précédemment attribués dans votre schéma.

-   Dans les requêtes de hello votre application se génère une requête doit envoyer *les paramètres de requête de facette* jeu de résultats de valeurs de filtre tooget hello facette disponibles pour ce document.

-   tooactually supprimer le jeu de résultats de document hello, application hello doit également appliquer un `$filter` expression.

Dans le développement de votre application, l’écriture de code qui crée des requêtes constitue en bloc de hello du travail de hello. Grand nombre des comportements d’application hello que vous pourriez attendre d’une navigation par facettes sont fournies par le service de hello, y compris la prise en charge intégrée pour définir des plages et l’obtention des nombres pour les résultats de facette. Hello comprend également des valeurs par défaut qui vous aident à éviter les structures de navigation lourde. 

## <a name="sample-code-and-demo"></a>Exemple de code et démonstration
Cet article prend l’exemple d’un portail de recrutement. exemple de Hello est implémenté comme une application ASP.NET MVC.

-   Consultez et tester la démonstration travail hello en ligne à [démonstration d’Azure Search travail Portal](http://azjobsdemo.azurewebsites.net/).

-   Télécharger le code de hello de hello [dépôt d’exemples de Azure sur GitHub](https://github.com/Azure-Samples/search-dotnet-asp-net-mvc-jobs).

## <a name="get-started"></a>Prise en main
Si vous êtes de nouveau développement toosearch, hello meilleure manière toothink de navigation par facettes est qu’elle affiche les possibilités de hello pour la recherche autonome. Il s'agit d'un type d'expérience de recherche détaillée, en fonction de filtres prédéfinis, utilisés pour limiter rapidement les résultats de la recherche à l'aide d'actions de type pointer et cliquer. 

### <a name="interaction-model"></a>Modèle d’interaction

expérience de recherche Hello pour la navigation par facettes est itératif, par conséquent, nous allons commencer par comprendre il comme une séquence de requêtes qui se déroulent dans les actions de réponse toouser.

point de départ de Hello est une page d’application qui fournit une navigation par facettes, généralement placée sur la périphérie de hello. La navigation à facettes est souvent présentée sous forme d'arborescence avec des cases à cocher pour chaque valeur ou du texte interactif. 

1. Une requête envoyée tooAzure recherche spécifie la structure de navigation par facettes hello via un ou plusieurs paramètres de requête de facette. Par exemple, la requête de hello peut inclure `facet=Rating`, éventuellement avec un `:values` ou `:sort` option toofurther affiner la présentation de hello.
2. couche de présentation Hello restitue une page de recherche qui fournit une navigation par facettes, à l’aide de facettes hello spécifiés dans la demande hello.
3. Étant donné une structure de navigation par facettes qui inclut l’évaluation, cliquez sur « 4 » tooindicate à afficher uniquement les produits dont le niveau est supérieur ou égal à 4. 
4. En réponse, application hello envoie une requête qui inclut`$filter=Rating ge 4` 
5. page de hello Hello présentation couche mises à jour un ensemble de résultats réduit, contenant uniquement les éléments qui répondent aux critères de nouveau hello (dans ce cas, les produits évalués 4 et ultérieures).

Une facette est un paramètre de requête, mais ne la confondez pas avec l'entrée de requête. Elle n'est jamais utilisée comme critère de sélection dans une requête. Au lieu de cela, pensez facette paramètres de requête en tant que structure de navigation toohello entrées renvoyées dans la réponse de hello. Pour chaque paramètre de requête de facette que vous fournissez, Azure Search évalue le nombre de documents est dans des résultats partiels hello pour chaque valeur de la facette.

Hello d’avis `$filter` à l’étape 4. filtre de Hello est un aspect important de navigation par facettes. Bien que les facettes et les filtres sont indépendants Bonjour API, vous devez les deux expérience de hello toodeliver que vous avez l’intention. 

### <a name="app-design-pattern"></a>Modèle de conception de l’application

Dans le code d’application, le modèle de hello est toouse facette requête tooreturn hello une navigation par facettes structure des paramètres, ainsi que les résultats de facette, ainsi qu’une expression $filter.  Hello filtre expression handles hello cliquez sur l’événement sur la valeur de la facette hello. Pensez à hello `$filter` d’expression en tant que code hello derrière la suppression réelle de hello des résultats de recherche a retourné la couche de présentation toohello. Étant donné une facette de couleurs, en cliquant sur hello couleur rouge est implémentée via un `$filter` expression qui sélectionne uniquement les éléments qui ont une couleur rouge. 

### <a name="query-basics"></a>Principes de base des requêtes

Dans Azure Search, une requête est spécifiée par le biais d'un ou de plusieurs paramètres de requête (consultez [Rechercher des documents](http://msdn.microsoft.com/library/azure/dn798927.aspx) pour obtenir une description de chacun d'eux). Aucun des paramètres de requête hello sont requis, mais vous devez avoir au moins un ordre pour un toobe de requête valide.

Précision compris comme hello toofilter de capacité des accès non pertinentes, est possible grâce à un ou deux de ces expressions :

-   **search=**  
    valeur Hello de ce paramètre constitue une expression de recherche hello. Il peut s'agir d'une portion de texte unique ou d'une expression de recherche complexe qui comprend plusieurs termes et opérateurs. Sur le serveur de hello, une expression de recherche est utilisée pour la recherche en texte intégral, interrogation des champs de recherche dans les index hello pour la correspondance des termes du contrat, de retourner des résultats dans l’ordre de classement. Si vous définissez `search` toonull, est de l’exécution des requêtes sur la totalité de l’index hello (autrement dit, `search=*`). In this case, autres éléments de hello de requête, comme un `$filter` ou profil de calcul de score, est des principaux facteurs qui affectent les documents sont retournés hello `($filter`) et dans quel ordre (`scoringProfile` ou `$orderby`).

-   **$filter =**  
    Un filtre est un mécanisme puissant pour limiter la taille de hello des résultats de recherche en fonction des valeurs hello d’attributs de document spécifique. A `$filter` est évaluée en premier, suivie de la logique des facettes qui génère les valeurs disponibles hello et les nombres correspondants pour chaque valeur

Expressions de recherche complexe diminuer les performances de hello de requête de hello. Lorsque cela est possible, utilisez filtre bien construite expressions tooincrease précision et améliorer les performances des requêtes.

toobetter comprendre comment un filtre ajoute plus de précision, comparer un tooone d’expression de recherche complexe qui inclut une expression de filtre :

-   `GET /indexes/hotel/docs?search=lodging budget +Seattle –motel +parking`
-   `GET /indexes/hotel/docs?search=lodging&$filter=City eq ‘Seattle’ and Parking and Type ne ‘motel’`

Les deux requêtes sont valides, mais ensuite hello est supérieur si vous recherchez non motels avec stationnement à Seattle.
-   requête de première Hello s’appuie sur les mots spécifiques qui est mentionné ou non mentionnées dans les champs de type chaîne comme nom, Description et tout autre champ contenant des données de recherche.
-   seconde Hello recherche des correspondances précises sur les données structurées et est probablement toobe beaucoup plus précise.

Dans les applications qui incluent la navigation à facettes, veillez à ce que chaque action de l’utilisateur sur une structure de navigation à facettes soit accompagnée d’une réduction du champ des résultats de recherche. toonarrow des résultats, utilisez une expression de filtre.

<a name="howtobuildit"></a>

## <a name="build-a-faceted-navigation-app"></a>Créer une application de navigation à facettes
Vous implémentez une navigation par facettes avec Azure Search dans votre code d’application qui génère la demande de recherche hello. une navigation par facettes Hello s’appuie sur les éléments dans le schéma que vous avez défini précédemment.

Prédéfinies dans votre index de recherche est hello `Facetable [true|false]` attribut d’index, de définir sur les champs sélectionnés tooenable ou de désactiver leur utilisation dans une structure de navigation par facettes. Sans `"Facetable" = true`, un champ ne peut pas être utilisé dans la navigation à facettes.

couche de présentation Hello dans votre code fournit l’expérience utilisateur hello. Elle doit répertorier les éléments constitutifs de hello de navigation par facettes hello, telles que l’étiquette de hello, les valeurs, les cases à cocher et les nombre de hello. Hello API REST Azure Search est indépendant de la plateforme, alors utilisez la plateforme que vous souhaitez et toute langue. Hello est important tooinclude des éléments d’interface utilisateur qui prennent en charge incrémentielle Actualiser, avec l’état de l’interface utilisateur mis à jour car chaque facette supplémentaire est sélectionné. 

Au moment de la requête, votre code d’application crée une demande qui inclut `facet=[string]`, un paramètre de requête qui fournit des toofacet de champ hello par. Une requête peut avoir plusieurs facettes, comme `&facet=color&facet=category&facet=rating`, chaque facette étant séparée par un caractère d'esperluette (&).

Code de l’application doit également construire un `$filter` hello de toohandle expression événements de clic dans une navigation par facettes. A `$filter` réduit les résultats de la recherche hello, à l’aide de la valeur de la facette hello comme critères de filtre.

Azure renvoie les résultats de recherche hello, basés sur un ou plusieurs termes que vous entrez, ainsi que de la structure de navigation par facettes toohello mises à jour. Dans Azure Search, la navigation à facettes est une construction à niveau unique, avec des valeurs de facettes et des décomptes des résultats trouvés pour chaque.

Dans les sections suivantes de hello, nous examinons proche procédure toobuild chaque partie.

<a name="buildindex"></a>

## <a name="build-hello-index"></a>Créer des index de hello
Des facettes sont activé sur une base de champ par champ dans les index hello, via cet attribut d’index : `"Facetable": true`.  
Tous les types de champs pouvant être utilisés dans la navigation à facettes sont `Facetable` par défaut. Ces types de champ incluent `Edm.String`, `Edm.DateTimeOffset`, et tous les hello des types de champs numériques (tous les types de champ sont essentiellement des facetable sauf `Edm.GeographyPoint`, qui ne peut pas être utilisé dans une navigation par facettes). 

Lorsque vous créez un index, une meilleure pratique pour la navigation par facettes est tooexplicitly, activer des facettes désactivée pour les champs qui ne doivent jamais être utilisés comme une facette.  En particulier, les champs de type chaîne pour les valeurs de singleton, par exemple un nom de produit ou d’ID doivent être définis trop`"Facetable": false` tooprevent leurs accidentelle (et inefficace) utiliser dans une navigation par facettes. L’activation des facettes off où vous n’avez pas besoin qu’il permet de maintenir une taille d’index de hello hello réduite et améliore généralement les performances.

Suivant fait partie du schéma de hello pour hello démonstration de portail de projet exemple d’application, de taille hello tooreduce attributs supprimé :

```json
{
  ...
  "name": "nycjobs",
  "fields": [
    { “name”: "id",                 "type": "Edm.String",              "searchable": false, "filterable": false, ... "facetable": false, ... },
    { “name”: "job_id",             "type": "Edm.String",              "searchable": false, "filterable": false, ... "facetable": false, ... },
    { “name”: "agency",              "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "posting_type",        "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "num_of_positions",    "type": "Edm.Int32",              "searchable": false, "filterable": true, ...  "facetable": true, ...  },
    { “name”: "business_title",      "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "civil_service_title", "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "title_code_no",       "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "level",               "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "salary_range_from",   "type": "Edm.Int32",              "searchable": false, "filterable": true, ...  "facetable": true, ...  },
    { “name”: "salary_range_to",     "type": "Edm.Int32",              "searchable": false, "filterable": true, ...  "facetable": true, ...  },
    { “name”: "salary_frequency",    "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "work_location",       "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
…
    { “name”: "geo_location",        "type": "Edm.GeographyPoint",     "searchable": false, "filterable": true, ...  "facetable": false, ... },
    { “name”: "tags",                "type": "Collection(Edm.String)", "searchable": true,  "filterable": true, ...  "facetable": true, ...  }
  ],
…
}
```

Comme vous pouvez le voir dans le schéma de l’exemple hello `Facetable` est désactivée pour les champs ne doivent pas être utilisées en tant que facettes, telles que des valeurs d’ID de chaîne. L’activation des facettes off où vous n’avez pas besoin qu’il permet de maintenir une taille d’index de hello hello réduite et améliore généralement les performances.

> [!TIP]
> En tant que meilleure pratique, comporter hello complète des attributs d’index pour chaque champ. Bien que `Facetable` est activé par défaut pour presque tous les champs, volontairement définissant chaque attribut, vous pouvez imaginer les implications en matière de hello de chaque décision de schéma. 

<a name="checkdata"></a>

## <a name="check-hello-data"></a>Vérifier les données hello
la qualité de vos données Hello a un effet direct sur si la structure de navigation par facettes hello matérialise comme vous le souhaitez. Elle affecte également la convivialité de construction de jeu de résultats de filtres tooreduce hello hello.

Si vous souhaitez toofacet par la marque ou le prix, chaque document doit contenir des valeurs pour *nom du produit* et *ProductPrice* qui sont valides, cohérentes et productifs comme option de filtre.

Voici quelques rappels de quel tooscrub pour :

* Pour chaque champ que vous souhaitez toofacet par, demandez-vous si elle contient des valeurs qui conviennent en tant que filtres dans la recherche autonome. les valeurs Hello doivent être court et descriptif suffisamment distinctive toooffer un choix clair entre les options concurrents.
* Fautes d'orthographe ou valeurs presque correspondantes. Si vous facette de couleur et les valeurs de champ incluent Orange et Ornage (une faute d’orthographe), d’une facette basée sur le champ de couleur hello choisit les deux.
* Le texte à casse mixte peut également causer des dégâts dans la navigation à facettes, où orange et Orange s'afficheraient comme deux valeurs différentes. 
* Versions uniques et au pluriel de hello même valeur peut entraîner une facette distincte pour chaque.

Comme vous pouvez l’imaginer, diligence lors de la préparation des données de salutation est un aspect essentiel de la navigation par facettes efficace.

<a name="presentationlayer"></a>

## <a name="build-hello-ui"></a>Générer l’interface utilisateur de hello
Utilisation de la couche de présentation hello peut aide vous découvrez les spécifications peuvent être omies dans le cas contraire et comprennent quelles sont les fonctionnalités essentiel toohello expérience de recherche.

En termes de navigation par facettes, votre page web ou une application affiche la structure de navigation par facettes hello détecte une entrée d’utilisateur sur la page de hello et insère les éléments hello modifié. 

Pour les applications web, AJAX est souvent utilisé dans la couche de présentation hello, car elle vous permet de toorefresh les modifications incrémentielles. Vous pouvez également utiliser ASP.NET MVC ou n’importe quelle autre plateforme de visualisation qui peut se connecter tooan service Azure Search via HTTP. exemple d’application Hello référencés tout au long de cet article : hello **démonstration d’Azure Search travail portail** – se produit toobe une application ASP.NET MVC.

Dans l’exemple hello, navigation par facettes est générée dans la page de résultats hello. Hello suivants exemple tiré de hello `index.cshtml` page de résultats du fichier de l’application d’exemple hello, structure statique HTML affiche hello pour l’affichage d’une navigation par facettes sur la recherche de hello. liste Hello de facettes est générée ou reconstruction dynamique lorsque vous envoyez un terme à rechercher, ou activez ou désactivez une facette.

```html
<div class="widget sidebar-widget jobs-filter-widget">
  <h5 class="widget-title">Filter Results</h5>
    <p id="filterReset"></p>
    <div class="widget-content">

      <h6 id="businessTitleFacetTitle">Business Title</h6>
      <ul class="filter-list" id="business_title_facets">
      </ul>

      <h6>Location</h6>
      <ul class="filter-list" id="posting_type_facets">
      </ul>

      <h6>Posting Type</h6>
      <ul class="filter-list" id="posting_type_facets"></ul>

      <h6>Minimum Salary</h6>
      <ul class="filter-list" id="salary_range_facets">
      </ul>

  </div>
</div>
```

Hello suivant extrait de code à partir de hello `index.cshtml` page crée dynamiquement hello HTML toodisplay hello première facette du, titre de l’entreprise. Des fonctions similaires générer de façon dynamique hello HTML pour hello autres facettes. Chaque facette a une étiquette et un nombre, qui affiche le nombre de hello d’éléments trouvé pour ce résultat de la facette.

```js
function UpdateBusinessTitleFacets(data) {
  var facetResultsHTML = '';
  for (var i = 0; i < data.length; i++) {
    facetResultsHTML += '<li><a href="javascript:void(0)" onclick="ChooseBusinessTitleFacet(\'' + data[i].Value + '\');">' + data[i].Value + ' (' + data[i].Count + ')</span></a></li>';
  }

  $("#business_title_facets").html(facetResultsHTML);
}
```

> [!TIP]
> Lorsque vous concevez la page de résultats hello, n’oubliez pas tooadd un mécanisme de compensation des facettes. Si vous ajoutez des cases à cocher, vous pouvez facilement voir comment les filtres tooclear hello. Pour les autres dispositions, vous devrez peut-être utiliser un modèle de navigation ou une autre approche créative. Par exemple, dans hello application d’exemple de portail de recherche de travail, vous pouvez cliquer sur hello `[X]` après une facette de hello tooclear facette sélectionnée.

<a name="buildquery"></a>

## <a name="build-hello-query"></a>Générer la requête de hello
code Hello que vous écrivez pour la création de requêtes doit spécifier toutes les parties d’une requête valide, y compris des expressions de recherche, les facettes, les filtres, de calcul de score profils – tout élément utilisé tooformulate une demande. Dans cette section, nous explorons où facettes tenir dans une requête, et comment les filtres sont utilisés avec les facettes toodeliver réduits jeu de résultats.

Notez que les facettes font partie intégrante de cet exemple d'application. expérience de recherche Hello Bonjour démonstration de portail de projet est conçu autour de filtres et de navigation par facettes. la sélection élective visible de Hello de navigation par facettes sur la page de hello illustre son importance. 

Un exemple est souvent un toobegin parfait. Hello suivants exemple tiré de hello `JobsSearch.cs` fichier, une demande qui crée la navigation de la facette basée sur le titre de l’entreprise, l’emplacement, Type de validation et Minimum salaire des builds. 

```cs
SearchParameters sp = new SearchParameters()
{
  ...
  // Add facets
  Facets = new List<String>() { "business_title", "posting_type", "level", "salary_range_from,interval:50000" },
};
```

Un paramètre de requête de facette a la valeur tooa champ et selon le type de données hello, peut être davantage paramétrable par liste délimitée par des virgules qui inclut `count:<integer>`, `sort:<>`, `interval:<integer>`, et `values:<list>`. Une liste de valeurs est prise en charge pour les données numériques lors de la définition de plages. Consultez [Rechercher des documents (API Azure Search)](http://msdn.microsoft.com/library/azure/dn798927.aspx) pour obtenir des détails sur l'utilisation.

En même temps que les facettes, demande hello formulée par votre application doit également s’appuyer toonarrow filtres vers le bas ensemble hello de documents candidats selon une sélection de valeur de facette. Pour un magasin de vélos, navigation par facettes fournit comme des indices tooquestions *les couleurs, les constructeurs et les types de vélos sont disponibles ?*. Le filtrage permet de répondre à des questions du type *Quels sont les vélos de type VTT et de couleur rouge dans cette gamme de prix ?*. Lorsque vous cliquez sur « Rouge » tooindicate à afficher uniquement les produits de couleur rouge, application de hello de requête suivante hello envoie inclut `$filter=Color eq ‘Red’`.

Hello suivant extrait de code à partir de hello `JobsSearch.cs` page ajoute hello sélectionné profession toohello filtre si vous sélectionnez une valeur de facette de profession hello.

```cs
if (businessTitleFacet != "")
  filter = "business_title eq '" + businessTitleFacet + "'";
```

<a name="tips"></a> 

## <a name="tips-and-best-practices"></a>Conseils et meilleures pratiques

### <a name="indexing-tips"></a>Conseils d’indexation
**Améliorer l’efficacité des index si vous n’utilisez pas de zone de recherche**

Si votre application utilise une navigation par facettes exclusivement (autrement dit, aucune zone de recherche), vous pouvez marquer le champ hello comme `searchable=false`, `facetable=true` tooproduce un index plus compact. En outre, l’indexation se produit uniquement sur des valeurs de facettes entier, avec aucune coupure de mots ou de l’indexation des composants hello d’une valeur de plusieurs mot.

**Spécifier les champs qui peuvent servir de facettes**

Rappelez-vous que hello schéma d’index de hello détermine les champs disponible toouse comme une facette. En supposant qu’un champ est facetable, les requêtes hello spécifie quels toofacet de champs par. champ Hello qui vous sont des facettes fournit des valeurs hello qui apparaissent sous l’étiquette de hello. 

les valeurs de Hello qui s’affichent sous chaque étiquette sont récupérées à partir de l’index de hello. Par exemple, si hello champ de facette est *couleur*, valeurs hello disponibles pour le filtrage supplémentaires sont hello valeurs pour ce champ - rouge, noir et ainsi de suite.

Pour les valeurs numériques et de date/heure uniquement, vous pouvez définir explicitement des valeurs de champ de facette hello (par exemple, `facet=Rating,values:1|2|3|4|5`). Une liste de valeurs est autorisée pour ces champs types toosimplify hello séparation des résultats de facette dans des plages contiguës (deux plages en fonction des valeurs numériques ou des périodes de temps). 

**Par défaut, vous ne pouvez avoir qu’un seul niveau de navigation par facettes** 

Comme mentionné, il n'existe aucune prise en charge directe de l'imbrication des facettes dans une hiérarchie. Par défaut, la navigation à facettes dans Recherche Azure ne prend en charge qu’un seul niveau de filtres. Toutefois, des solutions de contournement existent. Vous pouvez encoder une structure hiérarchique de facette dans une `Collection(Edm.String)` avec un point d'entrée par hiérarchie. L’implémentation de cette solution de contournement est abordée dans cet article hello. 

### <a name="querying-tips"></a>Conseils d’interrogation
**Validation des champs**

Si vous générez la liste de hello de facettes dynamiquement en fonction de l’entrée d’utilisateur non fiable, valider que hello des noms de champs à facettes de hello sont valides. Ou, échapper les noms hello lors de la génération d’URL à l’aide `Uri.EscapeDataString()` dans .NET ou hello équivalent dans votre plateforme de choix.

### <a name="filtering-tips"></a>Conseils de filtrage
**Augmenter la précision de la recherche avec des filtres**

Utilisation de filtres. Si vous comptez sur simplement des expressions de recherche uniquement, la recherche de radical peut entraîner un toobe document retourné qui n’a pas valeur de la facette précis hello dans un de ses champs.

**Augmenter les performances de recherche avec des filtres**

Les filtres cerner ensemble hello de documents candidats pour la recherche et les exclure de classement. Pour les grands jeux de documents, l’utilisation d’une exploration à facettes sélective offre souvent de meilleures performances.
  
**Filtrer uniquement les champs à facettes hello**

Dans l’exploration à facettes, il est souhaitable de tooonly incluent des documents dont la valeur de la facette hello dans un champ spécifique (facettes), pas n’importe où pour tous les champs de recherche. Ajout d’un filtre de renforce la champ cible de hello en dirigeant toosearch de service hello uniquement dans le champ à facettes de hello pour une valeur correspondante.

**Tronquer les résultats de facettes avec d’autres filtres**

Résultats de facette sont des documents trouvés dans les résultats de recherche hello qui correspondent à un terme de la facette. Bonjour, exemple, dans les résultats de recherche pour *du cloud computing*, 254 éléments ont également *spécification interne* comme un type de contenu. Les éléments ne sont pas nécessairement mutuellement exclusifs. Si un élément répond aux critères hello de deux filtres, il est compté dans chacun d’eux. Cette duplication est possible lorsque des facettes sur `Collection(Edm.String)` le balisage de document tooimplement les champs, qui sont souvent utilisés.

        Search term: "cloud computing"
        Content type
           Internal specification (254)
           Video (10) 

En règle générale, si vous trouvez que les résultats de facette constamment trop volumineux, nous vous recommandons que vous ajoutez plus filtre toogive utilisateurs davantage d’options pour affiner la recherche de hello.

### <a name="tips-about-result-count"></a>Conseils sur le décompte des résultats

**Limiter le nombre d’éléments de navigation de facette hello hello**

Pour chaque champ à facettes dans l’arborescence de navigation hello, il existe une limite par défaut de 10 valeurs. Cette valeur par défaut appropriée pour les structures de navigation, car il conserve les valeurs hello taille gérable de tooa la liste. Vous pouvez remplacer la valeur par défaut hello en assignant une valeur toocount.

* `&facet=city,count:5`Spécifie que seules hello cinq premières villes trouvés dans le haut hello classé les résultats sont retournés sous la forme d’un résultat de la facette. Imaginez un exemple de requête affichant le terme de recherche « aéroport » et 32 correspondances. Si la requête de hello spécifie `&facet=city,count:5`, seuls hello cinq premières unique villes avec hello la plupart des documents dans les résultats de recherche de hello sont inclus dans hello résultats de facette.

Avis hello distinguer les résultats de recherche et les résultats de facette. Résultats de la recherche sont tous les documents hello qui correspondent à la requête de hello. Résultats de facette sont hello de correspondances pour chaque valeur de la facette. Dans l’exemple de hello, les résultats de recherche comprennent les noms de ville qui ne sont pas dans la liste de classification de facette hello (5 dans notre exemple). Les résultats filtrés par le biais de la navigation à facettes deviennent visibles lorsque vous effacez les facettes ou choisissez d’autres facettes en plus de Ville. 

> [!NOTE]
> Traiter de `count` lorsqu'il existe plus d'un type peut prêter à confusion. Hello tableau suivant offre un bref résumé de l’utilisation du terme de hello dans l’API Azure Search, exemple de code et la documentation. 

* `@colorFacet.count`<br/>
  Dans le code de présentation, vous devez voir un paramètre du nombre sur facette hello, nombre de hello toodisplay utilisé des résultats de la facette. Dans les résultats de facette, nombre indique le nombre de hello de documents qui correspondent au terme de facette hello ou plage.
* `&facet=City,count:12`<br/>
  Dans une requête de facette, vous pouvez définir la valeur du nombre de tooa.  par défaut de Hello est 10, mais vous pouvez la définir supérieure ou inférieure. Paramètre `count:12` obtient hello premières 12 correspondances dans les résultats de facette par nombre de documents.
* "`@odata.count`"<br/>
  En réponse aux requêtes hello, cette valeur indique le nombre hello des éléments correspondants dans les résultats de recherche hello. En moyenne, il est plus importante que somme hello de tous les résultats de facette combinées, en raison de la présence de toohello d’éléments qui correspondent au terme de recherche hello, mais aucune correspondance de valeur de facette.

**Obtenir les décomptes dans les résultats de facettes**

Lorsque vous ajoutez une requête à facettes tooa de filtre, vous pourriez l’instruction de facette hello tooretain (par exemple, `facet=Rating&$filter=Rating ge 4`). Techniquement, facette = évaluation n’est pas nécessaire, mais conserver retourne des nombres hello de valeurs de facettes pour le contrôle d’accès 4 et versions ultérieures. Par exemple, si vous cliquez sur « 4 » et hello requête inclut un filtre pour supérieure ou égale trop « 4 », les nombres sont retournés pour chaque évaluation est 4 et versions ultérieures.  

**Vérifier que les nombres de facettes sont exacts**

Dans certaines circonstances, vous constaterez peut-être que des nombres de facettes ne correspondent pas les jeux de résultats hello (consultez [une navigation par facettes dans Azure Search (billet de forum)](https://social.msdn.microsoft.com/Forums/azure/06461173-ea26-4e6a-9545-fbbd7ee61c8f/faceting-on-azure-search?forum=azuresearch)).

Le nombre de facette peut être incorrect en raison de l’architecture de partitionnement toohello. Chaque index de recherche a plusieurs partitions, et chaque partition signale les facettes de N premiers hello en nombre de documents, qui est ensuite combiné en un seul résultat. Si certaines partitions ont de nombreuses valeurs correspondantes, tandis que d’autres moins, vous découvrirez peut-être que certaines valeurs de facettes sont manquants ou sous-comptabilisées dans les résultats de hello.

Bien que ce comportement peut changer à tout moment, si vous rencontrez ce problème aujourd'hui, vous pouvez contourner il en artificiellement gonfler nombre de hello :<number> tooa grand nombre tooenforce complète de création de rapports à partir de chaque partition. Si hello la valeur du nombre : est supérieure ou égale toohello nombre de valeurs uniques dans le champ de hello, vous avez la garantie des résultats précis. Toutefois, lorsque les décomptes de documents sont élevés, les performances baissent, alors utilisez cette option judicieusement.

### <a name="user-interface-tips"></a>Conseils sur l’interface utilisateur
**Ajouter des étiquettes pour chaque champ dans la navigation à facettes**

Les étiquettes sont généralement définies dans hello HTML ou un formulaire (`index.cshtml` dans l’exemple d’application hello). Il n’existe aucune API dans Recherche Azure pour les étiquettes de navigation à facettes ou tout autre type de métadonnées.

<a name="rangefacets"></a>

## <a name="filter-based-on-a-range"></a>Filtrer sur une plage de valeurs
L’utilisation de facettes sur des plages de valeurs est une condition d’application de recherche courante. Les plages sont prises en charge pour les données numériques et les valeurs DateHeure. Vous pouvez en savoir plus sur chaque approche dans [Rechercher des documents (API Azure Search)](http://msdn.microsoft.com/library/azure/dn798927.aspx).

Azure Search simplifie la création de plage en fournissant deux approches pour calculer une plage. Pour les deux approches, Azure Search crée hello donnés d’entrées hello que vous avez fourni les plages appropriées. Par exemple, si vous spécifiez des valeurs de plage de 10|20|30, Recherche Azure crée automatiquement les plages 0-10, 10-20, 20-30. Votre application peut éventuellement supprimer les intervalles vides. 

**Méthode 1 : Utiliser le paramètre d’intervalle hello**  
facettes de prix tooset par incréments de 10 $, vous devez spécifier :`&facet=price,interval:10`

**Approche 2 : utiliser une liste de valeurs**  
Pour les données numériques, vous pouvez utiliser une liste de valeurs.  Envisagez de plage de facette hello pour un `listPrice` champ, restituée comme suit :

  ![Exemple de liste de valeurs][5]

toospecify une plage de facette comme hello dans hello précédant la capture d’écran, utilisez une liste de valeurs :

    facet=listPrice,values:10|25|100|500|1000|2500

Chaque plage est construit à l’aide de 0 comme point de départ, une valeur de liste de hello comme un point de terminaison, puis de hello précédente toocreate discrète intervalles de plage. Recherche Azure effectue cette opération dans le cadre de la navigation à facettes. Vous n’avez pas de code toowrite de structuration de chaque intervalle.

### <a name="build-a-filter-for-a-range"></a>Créer un filtre pour une plage
documents toofilter basés sur une plage que vous sélectionnez, vous pouvez utiliser hello `"ge"` et `"lt"` opérateurs dans une expression en deux parties qui définit les points de terminaison hello de plage de hello de filtre. Par exemple, si vous choisissez hello plage 10 à 25 pour un `listPrice` champ, filtre de hello serait `$filter=listPrice ge 10 and listPrice lt 25`. Dans l’exemple de code hello, expression de filtre hello utilise **prix** et **priceTo** points de terminaison de paramètres tooset hello. 

  ![Requête pour une plage de valeurs][6]

<a name="geofacets"></a> 

## <a name="filter-based-on-distance"></a>Filtrer en fonction de la distance
Toosee commune ses filtres qui vous aident à choisir une banque, restaurant ou en fonction de son emplacement actuel de proximité tooyour de destination. Ce type de filtre peut ressembler à la navigation à facettes, mais c’est tout simplement un filtre. Nous le mentionnons ici pour ceux d'entre vous qui recherchent spécifiquement des conseils d'implémentation pour ce problème de conception particulier.

Il existe deux fonctions géospatiales dans la Recherche Azure, **geo.distance** et **geo.intersects**.

* Hello **geo.distance** fonction retourne la distance hello kilométrique entre deux points. Un point est un champ et autre constante transmise en tant que partie du filtre de hello. 
* Hello **geo.intersects** fonction retourne true si un point donné figure dans un polygone donné. Hello point est un champ et les polygones hello sont spécifié comme une liste de constante de coordonnées passées en tant que partie du filtre de hello.

Vous trouverez des exemples de filtres dans [Syntaxe d'expression OData (Azure Search)](http://msdn.microsoft.com/library/azure/dn798921.aspx).

<a name="tryitout"></a>

## <a name="try-hello-demo"></a>Essayez hello démonstration
Hello démonstration d’Azure Search travail portail contient des exemples de hello référencées dans cet article.

-   Consultez et tester la démonstration travail hello en ligne à [démonstration d’Azure Search travail Portal](http://azjobsdemo.azurewebsites.net/).

-   Télécharger le code de hello de hello [dépôt d’exemples de Azure sur GitHub](https://github.com/Azure-Samples/search-dotnet-asp-net-mvc-jobs).

Lorsque vous travaillez avec les résultats de la recherche, regardez les URL hello les modifications apportées à la construction de la requête. Cette application produit tooappend facettes toohello URI que vous sélectionnez chacune d’elles.

1. fonctionnalité de cartographie hello toouse de l’application de démonstration hello, obtenir une clé Bing Maps hello [centre de développement de Bing Maps](https://www.bingmapsportal.com/). Collez-la sur la clé existante de hello Bonjour `index.cshtml` page. Hello `BingApiKey` paramètre Bonjour `Web.config` fichier n’est pas utilisé. 

2. Exécutez l’application hello. Visite guidée hello facultatif ou fermer la boîte de dialogue hello.
   
3. Entrez un terme de recherche, tels que « analyste », puis cliquez sur recherche hello. requête de Hello s’exécute rapidement.
   
   Une structure de navigation par facettes est également retournée avec les résultats de recherche hello. Dans la page de résultats de recherche de hello, structure de navigation par facettes hello inclut les nombres pour chaque résultat de la facette. Aucune facette n’est sélectionnée : tous les résultats correspondants sont donc renvoyés.
   
   ![Résultats de recherche avant la sélection des facettes][11]

4. Cliquez sur une Fonction, un Lieu ou un Salaire minimal. Facettes étaient null sur la recherche initiale de hello, mais qu’ils prennent des valeurs, les résultats de recherche de hello sont supprimés des éléments qui ne correspondent plus.
   
   ![Résultats de recherche après la sélection des facettes][12]

5. requête à facettes de hello tooclear afin que vous pouvez essayer de comportements de requête différents, cliquez sur hello `[X]` après hello sélectionné facettes de facettes tooclear hello.
   
<a name="nextstep"></a>

## <a name="learn-more"></a>En savoir plus
Regardez la [Présentation approfondie de la Recherche Azure](http://channel9.msdn.com/Events/TechEd/Europe/2014/DBI-B410). En 45:25, vous trouverez une démonstration sur la façon de facettes de tooimplement.

Pour plus d’informations sur les principes de conception pour la navigation par facettes, nous vous recommandons de hello suivant liens :

* [Conception pour la recherche à facettes](http://www.uie.com/articles/faceted_search/)
* [Modèles de conception : navigation à facettes](http://alistapart.com/article/design-patterns-faceted-navigation)


<!--Anchors-->
[How toobuild it]: #howtobuildit
[Build hello presentation layer]: #presentationlayer
[Build hello index]: #buildindex
[Check for data quality]: #checkdata
[Build hello query]: #buildquery
[Tips on how toocontrol faceted navigation]: #tips
[Faceted navigation based on range values]: #rangefacets
[Faceted navigation based on GeoPoints]: #geofacets
[Try it out]: #tryitout

<!--Image references-->
[1]: ./media/search-faceted-navigation/azure-search-faceting-example.PNG
[2]: ./media/search-faceted-navigation/Facet-2-CSHTML.PNG
[3]: ./media/search-faceted-navigation/Facet-3-schema.PNG
[4]: ./media/search-faceted-navigation/Facet-4-SearchMethod.PNG
[5]: ./media/search-faceted-navigation/Facet-5-Prices.PNG
[6]: ./media/search-faceted-navigation/Facet-6-buildfilter.PNG
[7]: ./media/search-faceted-navigation/Facet-7-appstart.png
[8]: ./media/search-faceted-navigation/Facet-8-appbike.png
[9]: ./media/search-faceted-navigation/Facet-9-appbikefaceted.png
[10]: ./media/search-faceted-navigation/Facet-10-appTitle.png
[11]: ./media/search-faceted-navigation/faceted-search-before-facets.png
[12]: ./media/search-faceted-navigation/faceted-search-after-facets.png

<!--Link references-->
[Designing for Faceted Search]: http://www.uie.com/articles/faceted_search/
[Design Patterns: Faceted Navigation]: http://alistapart.com/article/design-patterns-faceted-navigation
[Create your first application]: search-create-first-solution.md
[OData expression syntax (Azure Search)]: http://msdn.microsoft.com/library/azure/dn798921.aspx
[Azure Search Adventure Works Demo]: https://azuresearchadventureworksdemo.codeplex.com/
[http://www.odata.org/documentation/odata-version-2-0/overview/]: http://www.odata.org/documentation/odata-version-2-0/overview/ 
[Faceting on Azure Search forum post]: ../faceting-on-azure-search.md?forum=azuresearch
[Search Documents (Azure Search API)]: http://msdn.microsoft.com/library/azure/dn798927.aspx

