---
pageTitle: Synonyms in Azure Search (preview) | Microsoft Docs
description: "Documentation préliminaire pour la fonction Synonymes (version préliminaire) exposée dans l’API REST Azure Search."
services: search
documentationCenter: 
authors: mhko
manager: pablocas
editor: 
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/07/2016
ms.author: nateko
ms.openlocfilehash: 739a0ad77c68ea74ec25bc80c7539ac8b3f18201
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="synonyms-in-azure-search-preview"></a><span data-ttu-id="6457a-102">Synonymes dans Azure Search (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="6457a-102">Synonyms in Azure Search (preview)</span></span>

<span data-ttu-id="6457a-103">Dans les moteurs de recherche, les synonymes associent des termes équivalents qui élargissent implicitement l’étendue d’une requête, sans que l’utilisateur ait à fournir le terme.</span><span class="sxs-lookup"><span data-stu-id="6457a-103">Synonyms in search engines associate equivalent terms that implicitly expand the scope of a query, without the user having to actually provide the term.</span></span> <span data-ttu-id="6457a-104">Par exemple, si l’on considère le terme « chien » et les associations de synonymes « canin » et « chiot », tous les documents contenant « chien », « canin » ou « chiot » seront pris en compte dans la requête.</span><span class="sxs-lookup"><span data-stu-id="6457a-104">For example, given the term "dog" and synonym associations of "canine" and "puppy", any documents containing "dog", "canine" or "puppy" will fall within the scope of the query.</span></span>

<span data-ttu-id="6457a-105">Dans Azure Search, l’expansion des synonymes est effectuée au moment de la requête.</span><span class="sxs-lookup"><span data-stu-id="6457a-105">In Azure Search, synonym expansion is done at query time.</span></span> <span data-ttu-id="6457a-106">Vous pouvez ajouter des cartes de synonymes à un service sans interrompre les opérations existantes.</span><span class="sxs-lookup"><span data-stu-id="6457a-106">You can add synonym maps to a service with no disruption to existing operations.</span></span> <span data-ttu-id="6457a-107">Vous pouvez ajouter une propriété **synonymMaps** à une définition de champ sans avoir à reconstruire l’index.</span><span class="sxs-lookup"><span data-stu-id="6457a-107">You can add a  **synonymMaps** property to a field definition without having to rebuild the index.</span></span> <span data-ttu-id="6457a-108">Pour plus d’informations, consultez [Mise à jour d’index](https://docs.microsoft.com/rest/api/searchservice/update-index).</span><span class="sxs-lookup"><span data-stu-id="6457a-108">For more information, see [Update Index](https://docs.microsoft.com/rest/api/searchservice/update-index).</span></span>

## <a name="feature-availability"></a><span data-ttu-id="6457a-109">Disponibilité des fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="6457a-109">Feature availability</span></span>

<span data-ttu-id="6457a-110">La fonctionnalité de synonymes est actuellement en version préliminaire et prise en charge uniquement dans les dernières versions d’API préliminaires (api-version=2016-09-01-Preview).</span><span class="sxs-lookup"><span data-stu-id="6457a-110">The synonyms feature is currently in preview and only supported in the latest preview api-version (api-version=2016-09-01-Preview).</span></span> <span data-ttu-id="6457a-111">Il n’existe aucune prise en charge sur le portail Azure pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="6457a-111">There is no Azure portal support at this time.</span></span> <span data-ttu-id="6457a-112">Comme la version de l’API est spécifiée dans la requête, il est possible de combiner les API mises à la disposition générale (GA) et les API en version préliminaire disponibles dans la même application.</span><span class="sxs-lookup"><span data-stu-id="6457a-112">Because the API version is specified on the request, it's possible to combine generally available (GA) and preview APIs in the same app.</span></span> <span data-ttu-id="6457a-113">Cependant, les API de versions préliminaires ne sont pas soumises à un contrat SLA, et les fonctionnalités peuvent changer ; par conséquent, nous ne recommandons pas de les utiliser dans des applications de production.</span><span class="sxs-lookup"><span data-stu-id="6457a-113">However, preview APIs are not under SLA and features may change, so we do not recommend using them in production applications.</span></span>

## <a name="how-to-use-synonyms-in-azure-search"></a><span data-ttu-id="6457a-114">Guide pratique pour utiliser des synonymes dans Azure Search</span><span class="sxs-lookup"><span data-stu-id="6457a-114">How to use synonyms in Azure search</span></span>

<span data-ttu-id="6457a-115">Dans Azure Search, la prise en charge des synonymes repose sur des cartes de synonymes que vous définissez et chargez sur votre service.</span><span class="sxs-lookup"><span data-stu-id="6457a-115">In Azure Search, synonym support is based on synonym maps that you define and upload to your service.</span></span> <span data-ttu-id="6457a-116">Ces cartes constituent des ressources indépendantes (telles que des index ou des sources de données) et peuvent être utilisées par n’importe quel champ de recherche dans un index de votre service de recherche.</span><span class="sxs-lookup"><span data-stu-id="6457a-116">These maps constitute an independent resource (like indexes or data sources), and can be used by any searchable field in any index in your search service.</span></span>

<span data-ttu-id="6457a-117">Les cartes de synonymes et les index sont gérés de manière indépendante.</span><span class="sxs-lookup"><span data-stu-id="6457a-117">Synonym maps and indexes are maintained independently.</span></span> <span data-ttu-id="6457a-118">Une fois que vous définissez une carte de synonymes et la téléchargez sur votre service, vous pouvez activer la fonctionnalité de synonyme sur un champ en ajoutant une nouvelle propriété nommée **synonymMaps** dans la définition du champ.</span><span class="sxs-lookup"><span data-stu-id="6457a-118">Once you define a synonym map and upload it to your service, you can enable the synonym feature on a field by adding a new property called **synonymMaps** in the field definition.</span></span> <span data-ttu-id="6457a-119">La création, la mise à jour et la suppression d’une carte de synonymes constituent des opérations qui s’appliquent au document entier, ce qui signifie que vous ne peut pas créer, mettre à jour ou supprimer des parties de la carte de synonyme de façon incrémentielle.</span><span class="sxs-lookup"><span data-stu-id="6457a-119">Creating, updating, and deleting a synonym map is always a whole-document operation, meaning that you cannot create, update or delete parts of the synonym map incrementally.</span></span> <span data-ttu-id="6457a-120">Même la mise à jour d’une seule entrée nécessite un rechargement.</span><span class="sxs-lookup"><span data-stu-id="6457a-120">Updating even a single entry requires a reload.</span></span>

<span data-ttu-id="6457a-121">L’incorporation de synonymes dans votre application de recherche est un processus en deux étapes :</span><span class="sxs-lookup"><span data-stu-id="6457a-121">Incorporating synonyms into your search application is a two-step process:</span></span>

1.  <span data-ttu-id="6457a-122">Ajoutez une carte de synonymes à votre service de recherche via les API ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="6457a-122">Add a synonym map to your search service through the APIs below.</span></span>  

2.  <span data-ttu-id="6457a-123">Configurez un champ pouvant faire l’objet d’une recherche pour utiliser la carte de synonymes dans la définition d’index.</span><span class="sxs-lookup"><span data-stu-id="6457a-123">Configure a searchable field to use the synonym map in the index definition.</span></span>

### <a name="synonymmaps-resource-apis"></a><span data-ttu-id="6457a-124">API de ressources SynonymMaps</span><span class="sxs-lookup"><span data-stu-id="6457a-124">SynonymMaps Resource APIs</span></span>

#### <a name="add-or-update-a-synonym-map-under-your-service-using-post-or-put"></a><span data-ttu-id="6457a-125">Ajoutez ou mettez à jour une carte de synonymes dans votre service à l’aide d’une requête POST ou PUT.</span><span class="sxs-lookup"><span data-stu-id="6457a-125">Add or update a synonym map under your service, using POST or PUT.</span></span>

<span data-ttu-id="6457a-126">Les cartes de synonymes sont téléchargées sur le service via une requête POST ou PUT.</span><span class="sxs-lookup"><span data-stu-id="6457a-126">Synonym maps are uploaded to the service via POST or PUT.</span></span> <span data-ttu-id="6457a-127">Chaque règle doit être délimitée par le caractère de nouvelle ligne ('\n').</span><span class="sxs-lookup"><span data-stu-id="6457a-127">Each rule must be delimited by the new line character ('\n').</span></span> <span data-ttu-id="6457a-128">Vous pouvez définir jusqu'à 5 000 règles par carte de synonymes dans un service gratuit et 10 000 règles dans toutes les autres références (SKU).</span><span class="sxs-lookup"><span data-stu-id="6457a-128">You can define up to 5,000 rules per synonym map in a free service and 10,000 rules in all other SKUs.</span></span> <span data-ttu-id="6457a-129">Chaque règle peut avoir jusqu'à 20 extensions.</span><span class="sxs-lookup"><span data-stu-id="6457a-129">Each rule can have up to 20 expansions.</span></span>

<span data-ttu-id="6457a-130">Dans cette version préliminaire, les cartes de synonymes doivent être au format Apache Solr décrit ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="6457a-130">In this preview, synonym maps must be in the Apache Solr format which is explained below.</span></span> <span data-ttu-id="6457a-131">Si vous disposez d’un dictionnaire de synonymes existant dans un autre format et souhaitez l’utiliser directement, faites-le-nous savoir sur [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span><span class="sxs-lookup"><span data-stu-id="6457a-131">If you have an existing synonym dictionary in a different format and want to use it directly, please let us know on [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span></span>

<span data-ttu-id="6457a-132">Vous pouvez créer une nouvelle carte de synonymes à l’aide d’une requête HTTP POST, comme dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="6457a-132">You can create a new synonym map using HTTP POST, as in the following example:</span></span>

    POST https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "name":"mysynonymmap",
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

<span data-ttu-id="6457a-133">Vous pouvez également utiliser une requête PUT en spécifiant le nom de la carte de synonymes sur l'URI.</span><span class="sxs-lookup"><span data-stu-id="6457a-133">Alternatively, you can use PUT and specify the synonym map name on the URI.</span></span> <span data-ttu-id="6457a-134">Si la carte de synonymes n'existe pas, elle est créée.</span><span class="sxs-lookup"><span data-stu-id="6457a-134">If the synonym map does not exist, it will be created.</span></span>

    PUT https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

##### <a name="apache-solr-synonym-format"></a><span data-ttu-id="6457a-135">Format de synonymes Apache Solr</span><span class="sxs-lookup"><span data-stu-id="6457a-135">Apache Solr synonym format</span></span>

<span data-ttu-id="6457a-136">Le format Solr prend en charge les cartes de synonymes équivalentes et explicites.</span><span class="sxs-lookup"><span data-stu-id="6457a-136">The Solr format supports equivalent and explicit synonym mappings.</span></span> <span data-ttu-id="6457a-137">Les règles de mappage respectent la spécification de filtre de synonyme open source d’Apache Solr, décrite dans ce document : [SynonymFilter](https://cwiki.apache.org/confluence/display/solr/Filter+Descriptions#FilterDescriptions-SynonymFilter).</span><span class="sxs-lookup"><span data-stu-id="6457a-137">Mapping rules adhere to the open source synonym filter specification of Apache Solr, described in this document: [SynonymFilter](https://cwiki.apache.org/confluence/display/solr/Filter+Descriptions#FilterDescriptions-SynonymFilter).</span></span> <span data-ttu-id="6457a-138">Voici un exemple de règle pour des synonymes équivalents.</span><span class="sxs-lookup"><span data-stu-id="6457a-138">Below is a sample rule for equivalent synonyms.</span></span>
```
              USA, United States, United States of America
```

<span data-ttu-id="6457a-139">Avec la règle ci-dessus, une requête de recherche « USA » s’étendra à « USA » OR « United States » OR « United States of America ».</span><span class="sxs-lookup"><span data-stu-id="6457a-139">With the rule above, a search query "USA" will expand to "USA" OR "United States" OR "United States of America".</span></span>

<span data-ttu-id="6457a-140">Un mappage explicite est indiqué par une flèche « => ».</span><span class="sxs-lookup"><span data-stu-id="6457a-140">Explicit mapping is denoted by an arrow "=>".</span></span> <span data-ttu-id="6457a-141">Lorsqu’elle spécifiée, une séquence de termes d’une requête de recherche qui correspond à la partie gauche de « => » est remplacée par les alternatives sur la partie droite.</span><span class="sxs-lookup"><span data-stu-id="6457a-141">When specified, a term sequence of a search query that matches the left hand side of "=>" will be replaced with the alternatives on the right hand side.</span></span> <span data-ttu-id="6457a-142">Étant donné la règle ci-dessous, les requêtes de recherche « Washington », « Wash. »</span><span class="sxs-lookup"><span data-stu-id="6457a-142">Given the rule below, search queries "Washington", "Wash."</span></span> <span data-ttu-id="6457a-143">ou « WA » seront réécrites « WA ».</span><span class="sxs-lookup"><span data-stu-id="6457a-143">or "WA" will all be rewritten to "WA".</span></span> <span data-ttu-id="6457a-144">Le mappage explicite s’applique dans le sens spécifié uniquement et ne réécrit pas la requête « WA » en « Washington » dans ce cas.</span><span class="sxs-lookup"><span data-stu-id="6457a-144">Explicit mapping only applies in the direction specified and does not rewrite the query "WA" to "Washington" in this case.</span></span>
```
              Washington, Wash., WA => WA
```

#### <a name="list-synonym-maps-under-your-service"></a><span data-ttu-id="6457a-145">Répertorier les cartes de synonymes de votre service.</span><span class="sxs-lookup"><span data-stu-id="6457a-145">List synonym maps under your service.</span></span>

    GET https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="get-a-synonym-map-under-your-service"></a><span data-ttu-id="6457a-146">Obtenir une carte de synonymes pour votre service.</span><span class="sxs-lookup"><span data-stu-id="6457a-146">Get a synonym map under your service.</span></span>

    GET https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="delete-a-synonyms-map-under-your-service"></a><span data-ttu-id="6457a-147">Supprimer une carte de synonymes de votre service.</span><span class="sxs-lookup"><span data-stu-id="6457a-147">Delete a synonyms map under your service.</span></span>

    DELETE https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

### <a name="configure-a-searchable-field-to-use-the-synonym-map-in-the-index-definition"></a><span data-ttu-id="6457a-148">Configurez un champ pouvant faire l’objet d’une recherche pour utiliser la carte de synonymes dans la définition d’index.</span><span class="sxs-lookup"><span data-stu-id="6457a-148">Configure a searchable field to use the synonym map in the index definition.</span></span>

<span data-ttu-id="6457a-149">Une nouvelle propriété de champ **synonymMaps** permet de spécifier une carte de synonymes à utiliser pour un champ pouvant faire l’objet d’une recherche.</span><span class="sxs-lookup"><span data-stu-id="6457a-149">A new field property **synonymMaps** can be used to specify a synonym map to use for a searchable field.</span></span> <span data-ttu-id="6457a-150">Les cartes de synonymes sont des ressources de niveau de service et peuvent être référencées selon n’importe quel champ d’index dans le service.</span><span class="sxs-lookup"><span data-stu-id="6457a-150">Synonym maps are service level resources and can be referenced by any field of an index under the service.</span></span>

    POST https://[servicename].search.windows.net/indexes?api-version=2016-09-01-Preview
    api-key: [admin key]

    {
       "name":"myindex",
       "fields":[
          {
             "name":"id",
             "type":"Edm.String",
             "key":true
          },
          {
             "name":"name",
             "type":"Edm.String",
             "searchable":true,
             "analyzer":"en.lucene",
             "synonymMaps":[
                "mysynonymmap"
             ]
          },
          {
             "name":"name_jp",
             "type":"Edm.String",
             "searchable":true,
             "analyzer":"ja.microsoft",
             "synonymMaps":[
                "japanesesynonymmap"
             ]
          }
       ]
    }

<span data-ttu-id="6457a-151">**synonymMaps** peut être spécifié pour les champs pouvant faire l’objet d’une recherche de type « Edm.String » ou « Collection(Edm.String) ».</span><span class="sxs-lookup"><span data-stu-id="6457a-151">**synonymMaps** can be specified for searchable fields of the type 'Edm.String' or 'Collection(Edm.String)'.</span></span>

> [!NOTE]
> <span data-ttu-id="6457a-152">Dans cette version préliminaire, vous pouvez uniquement utiliser une carte de synonymes par champ.</span><span class="sxs-lookup"><span data-stu-id="6457a-152">In this preview, you can only have one synonym map per field.</span></span> <span data-ttu-id="6457a-153">Si vous souhaitez utiliser plusieurs cartes de synonymes, faites-le-nous savoir sur [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span><span class="sxs-lookup"><span data-stu-id="6457a-153">If you want to use multiple synonym maps, please let us know on [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span></span>

## <a name="impact-of-synonyms-on-other-search-features"></a><span data-ttu-id="6457a-154">Impact des synonymes sur les autres fonctionnalités de recherche</span><span class="sxs-lookup"><span data-stu-id="6457a-154">Impact of synonyms on other search features</span></span>

<span data-ttu-id="6457a-155">La fonctionnalité de synonymes réécrit la requête d’origine avec des synonymes utilisant l’opérateur OR.</span><span class="sxs-lookup"><span data-stu-id="6457a-155">The synonyms feature rewrites the original query with synonyms with the OR operator.</span></span> <span data-ttu-id="6457a-156">Pour cette raison, la mise en surbrillance des correspondances et les profils de score traitent les synonymes et le terme d’origine comme équivalents.</span><span class="sxs-lookup"><span data-stu-id="6457a-156">For this reason, hit highlighting and scoring profiles treat the original term and synonyms as equivalent.</span></span>

<span data-ttu-id="6457a-157">La fonctionnalité de synonymes s’applique aux requêtes de recherche et non aux filtres ou facettes.</span><span class="sxs-lookup"><span data-stu-id="6457a-157">Synonym feature applies to search queries and does not apply to filters or facets.</span></span> <span data-ttu-id="6457a-158">De même, les suggestions sont basées uniquement sur le terme d’origine : les correspondances de synonymes n’apparaissent pas dans la réponse.</span><span class="sxs-lookup"><span data-stu-id="6457a-158">Similarly, suggestions are based only on the original term; synonym matches do not appear in the response.</span></span>

<span data-ttu-id="6457a-159">Les extensions de synonymes ne s’appliquent pas aux termes de recherche génériques : les préfixes, correspondances partielles et les expressions régulières ne sont pas étendus.</span><span class="sxs-lookup"><span data-stu-id="6457a-159">Synonym expansions do not apply to wildcard search terms; prefix, fuzzy, and regex terms aren't expanded.</span></span>

## <a name="tips-for-building-a-synonym-map"></a><span data-ttu-id="6457a-160">Conseils pour créer une carte de synonymes</span><span class="sxs-lookup"><span data-stu-id="6457a-160">Tips for building a synonym map</span></span>

- <span data-ttu-id="6457a-161">Une carte de synonymes claire et précise est plus efficace qu’une liste exhaustive des correspondances possibles.</span><span class="sxs-lookup"><span data-stu-id="6457a-161">A concise, well-designed synonym map is more efficient than an exhaustive list of possible matches.</span></span> <span data-ttu-id="6457a-162">Les dictionnaires très volumineux ou complexes prennent plus de temps à analyser et affectent la latence des requêtes si la requête s’étend sur plusieurs synonymes.</span><span class="sxs-lookup"><span data-stu-id="6457a-162">Excessively large or complex dictionaries take longer to parse and affect the query latency if the query expands to many synonyms.</span></span> <span data-ttu-id="6457a-163">Au lieu de deviner les termes qui peuvent être utilisés, vous pouvez obtenir les termes réels via un [rapport d’analyse du trafic de recherche](search-traffic-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="6457a-163">Rather than guess at which terms might be used, you can get the actual terms via a [search traffic analysis report](search-traffic-analytics.md).</span></span>

- <span data-ttu-id="6457a-164">Comme exercice préliminaire et de validation, activez et utilisez ce rapport pour déterminer avec précision les termes les plus propices à une carte de synonymes, puis continuez à utiliser ces termes pour valider le fait que votre carte de synonymes génère un meilleur résultat.</span><span class="sxs-lookup"><span data-stu-id="6457a-164">As both a preliminary and validation exercise, enable and then use this report to precisely determine which terms will benefit from a synonym match, and then continue to use it as validation that your synonym map is producing a better outcome.</span></span> <span data-ttu-id="6457a-165">Dans le rapport prédéfini, les titres « Requêtes de recherche courantes » et « Requêtes de recherche sans résultats » vous fourniront les informations nécessaires.</span><span class="sxs-lookup"><span data-stu-id="6457a-165">In the predefined report, the tiles "Most common search queries" and "Zero-result search queries" will give you the necessary information.</span></span>

- <span data-ttu-id="6457a-166">Vous pouvez créer plusieurs cartes de synonymes pour votre application de recherche (par exemple, par langue si votre application prend en charge une base de clients multilingue).</span><span class="sxs-lookup"><span data-stu-id="6457a-166">You can create multiple synonym maps for your search application (for example, by language if your application supports a multi-lingual customer base).</span></span> <span data-ttu-id="6457a-167">Actuellement, un champ peut uniquement utiliser une de ces deux méthodes.</span><span class="sxs-lookup"><span data-stu-id="6457a-167">Currently, a field can only use one of them.</span></span> <span data-ttu-id="6457a-168">Vous pouvez mettre à jour la propriété synonymMaps d’un champ à tout moment.</span><span class="sxs-lookup"><span data-stu-id="6457a-168">You can update a field's synonymMaps property at any time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6457a-169">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6457a-169">Next Steps</span></span>

- <span data-ttu-id="6457a-170">Si vous avez un index existant dans un environnement de déploiement (non production), faites des essais avec un petit dictionnaire pour voir comment l’ajout de synonymes modifie l’expérience de recherche, notamment son impact sur les profils de score, la mise en surbrillance des correspondances et les suggestions.</span><span class="sxs-lookup"><span data-stu-id="6457a-170">If you have an existing index in a development (non-production) environment, experiment with a small dictionary to see how the addition of synonyms changes the search experience, including impact on scoring profiles, hit highlighting, and suggestions.</span></span>

- <span data-ttu-id="6457a-171">[Activez l’analyse du trafic des recherches](search-traffic-analytics.md) et utilisez le rapport Power BI prédéfini pour connaître les termes les plus utilisés, et ceux qui ne renvoient aucun document.</span><span class="sxs-lookup"><span data-stu-id="6457a-171">[Enable search traffic analytics](search-traffic-analytics.md) and use the predefined Power BI report to learn which terms are used the most, and which ones return zero documents.</span></span> <span data-ttu-id="6457a-172">Grâce à ces informations, modifiez le dictionnaire afin d’inclure les synonymes pour les requêtes non productives qui devraient être associées à des documents dans l’index.</span><span class="sxs-lookup"><span data-stu-id="6457a-172">Armed with these insights, revise the dictionary to include synonyms for unproductive queries that should be resolving to documents in your index.</span></span>
