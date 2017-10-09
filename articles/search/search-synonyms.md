---
pageTitle: Synonyms in Azure Search (preview) | Microsoft Docs
description: "Documentation préliminaire concernant hello synonymes (version préliminaire), exposée dans hello API REST Azure Search."
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
ms.openlocfilehash: 2695139d2b298fa2e7c1814715fdf96729f594ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="synonyms-in-azure-search-preview"></a><span data-ttu-id="fcf4a-102">Synonymes dans Azure Search (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="fcf4a-102">Synonyms in Azure Search (preview)</span></span>

<span data-ttu-id="fcf4a-103">Synonymes dans les moteurs de recherche associent un terme équivalent implicitement développez étendue hello d’une requête, sans hello utilisateur tooactually fournissent les termes hello.</span><span class="sxs-lookup"><span data-stu-id="fcf4a-103">Synonyms in search engines associate equivalent terms that implicitly expand hello scope of a query, without hello user having tooactually provide hello term.</span></span> <span data-ttu-id="fcf4a-104">Par exemple, le terme donné hello « dog » et les associations de synonymes de « canine » et « chien », tous les documents contenant « dog », « canine » ou « chien » appartiennent relevant de requête de hello hello.</span><span class="sxs-lookup"><span data-stu-id="fcf4a-104">For example, given hello term "dog" and synonym associations of "canine" and "puppy", any documents containing "dog", "canine" or "puppy" will fall within hello scope of hello query.</span></span>

<span data-ttu-id="fcf4a-105">Dans Azure Search, l’expansion des synonymes est effectuée au moment de la requête.</span><span class="sxs-lookup"><span data-stu-id="fcf4a-105">In Azure Search, synonym expansion is done at query time.</span></span> <span data-ttu-id="fcf4a-106">Vous pouvez ajouter le synonyme maps tooa service sans aucune opération de tooexisting d’interruption de service.</span><span class="sxs-lookup"><span data-stu-id="fcf4a-106">You can add synonym maps tooa service with no disruption tooexisting operations.</span></span> <span data-ttu-id="fcf4a-107">Vous pouvez ajouter un **synonymMaps** définition de champ de propriété tooa sans avoir d’index de hello toorebuild.</span><span class="sxs-lookup"><span data-stu-id="fcf4a-107">You can add a  **synonymMaps** property tooa field definition without having toorebuild hello index.</span></span> <span data-ttu-id="fcf4a-108">Pour plus d’informations, consultez [Mise à jour d’index](https://docs.microsoft.com/rest/api/searchservice/update-index).</span><span class="sxs-lookup"><span data-stu-id="fcf4a-108">For more information, see [Update Index](https://docs.microsoft.com/rest/api/searchservice/update-index).</span></span>

## <a name="feature-availability"></a><span data-ttu-id="fcf4a-109">Disponibilité des fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="fcf4a-109">Feature availability</span></span>

<span data-ttu-id="fcf4a-110">afficher un aperçu de synonymes Hello fonctionnalité n’est en cours et uniquement pris en charge dans hello dernière api-version d’évaluation (api-version = 2016-09-01-Preview).</span><span class="sxs-lookup"><span data-stu-id="fcf4a-110">hello synonyms feature is currently in preview and only supported in hello latest preview api-version (api-version=2016-09-01-Preview).</span></span> <span data-ttu-id="fcf4a-111">Il n’existe aucune prise en charge sur le portail Azure pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="fcf4a-111">There is no Azure portal support at this time.</span></span> <span data-ttu-id="fcf4a-112">Étant donné que la version de l’API de hello est spécifiée sur la demande de hello, il est possible toocombine disposition générale (GA) et les API préliminaires Bonjour même application.</span><span class="sxs-lookup"><span data-stu-id="fcf4a-112">Because hello API version is specified on hello request, it's possible toocombine generally available (GA) and preview APIs in hello same app.</span></span> <span data-ttu-id="fcf4a-113">Cependant, les API de versions préliminaires ne sont pas soumises à un contrat SLA, et les fonctionnalités peuvent changer ; par conséquent, nous ne recommandons pas de les utiliser dans des applications de production.</span><span class="sxs-lookup"><span data-stu-id="fcf4a-113">However, preview APIs are not under SLA and features may change, so we do not recommend using them in production applications.</span></span>

## <a name="how-toouse-synonyms-in-azure-search"></a><span data-ttu-id="fcf4a-114">Comment rechercher les synonymes toouse dans Azure</span><span class="sxs-lookup"><span data-stu-id="fcf4a-114">How toouse synonyms in Azure search</span></span>

<span data-ttu-id="fcf4a-115">Dans Azure Search, prise en charge de synonyme est basée sur des cartes de synonyme que vous définissez et téléchargez tooyour service.</span><span class="sxs-lookup"><span data-stu-id="fcf4a-115">In Azure Search, synonym support is based on synonym maps that you define and upload tooyour service.</span></span> <span data-ttu-id="fcf4a-116">Ces cartes constituent des ressources indépendantes (telles que des index ou des sources de données) et peuvent être utilisées par n’importe quel champ de recherche dans un index de votre service de recherche.</span><span class="sxs-lookup"><span data-stu-id="fcf4a-116">These maps constitute an independent resource (like indexes or data sources), and can be used by any searchable field in any index in your search service.</span></span>

<span data-ttu-id="fcf4a-117">Les cartes de synonymes et les index sont gérés de manière indépendante.</span><span class="sxs-lookup"><span data-stu-id="fcf4a-117">Synonym maps and indexes are maintained independently.</span></span> <span data-ttu-id="fcf4a-118">Une fois que vous définissez un mappage de synonyme et téléchargez tooyour service, vous pouvez activer la fonctionnalité de synonyme hello sur un champ en ajoutant une nouvelle propriété nommée **synonymMaps** dans la définition de champ hello.</span><span class="sxs-lookup"><span data-stu-id="fcf4a-118">Once you define a synonym map and upload it tooyour service, you can enable hello synonym feature on a field by adding a new property called **synonymMaps** in hello field definition.</span></span> <span data-ttu-id="fcf4a-119">Création, mise à jour et suppression de qu'un mappage de synonyme est toujours une opération du document dans son ensemble, ce qui signifie que que vous ne pouvez pas créer, mettre à jour ou supprimer des éléments de mappage de synonyme hello de façon incrémentielle.</span><span class="sxs-lookup"><span data-stu-id="fcf4a-119">Creating, updating, and deleting a synonym map is always a whole-document operation, meaning that you cannot create, update or delete parts of hello synonym map incrementally.</span></span> <span data-ttu-id="fcf4a-120">Même la mise à jour d’une seule entrée nécessite un rechargement.</span><span class="sxs-lookup"><span data-stu-id="fcf4a-120">Updating even a single entry requires a reload.</span></span>

<span data-ttu-id="fcf4a-121">L’incorporation de synonymes dans votre application de recherche est un processus en deux étapes :</span><span class="sxs-lookup"><span data-stu-id="fcf4a-121">Incorporating synonyms into your search application is a two-step process:</span></span>

1.  <span data-ttu-id="fcf4a-122">Ajouter un service de recherche de synonyme carte tooyour via hello API ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="fcf4a-122">Add a synonym map tooyour search service through hello APIs below.</span></span>  

2.  <span data-ttu-id="fcf4a-123">Configurer un mappage de champ interrogeable toouse hello synonyme dans la définition de l’index hello.</span><span class="sxs-lookup"><span data-stu-id="fcf4a-123">Configure a searchable field toouse hello synonym map in hello index definition.</span></span>

### <a name="synonymmaps-resource-apis"></a><span data-ttu-id="fcf4a-124">API de ressources SynonymMaps</span><span class="sxs-lookup"><span data-stu-id="fcf4a-124">SynonymMaps Resource APIs</span></span>

#### <a name="add-or-update-a-synonym-map-under-your-service-using-post-or-put"></a><span data-ttu-id="fcf4a-125">Ajoutez ou mettez à jour une carte de synonymes dans votre service à l’aide d’une requête POST ou PUT.</span><span class="sxs-lookup"><span data-stu-id="fcf4a-125">Add or update a synonym map under your service, using POST or PUT.</span></span>

<span data-ttu-id="fcf4a-126">Mappages de synonyme sont téléchargés service toohello via POST ou PUT.</span><span class="sxs-lookup"><span data-stu-id="fcf4a-126">Synonym maps are uploaded toohello service via POST or PUT.</span></span> <span data-ttu-id="fcf4a-127">Chaque règle doit être délimité par hello caractère de nouvelle ligne ('\n').</span><span class="sxs-lookup"><span data-stu-id="fcf4a-127">Each rule must be delimited by hello new line character ('\n').</span></span> <span data-ttu-id="fcf4a-128">Vous pouvez définir des too5, des règles 000 par mappage de synonyme dans un service gratuit et 10 000 règles dans tous les autres références (SKU).</span><span class="sxs-lookup"><span data-stu-id="fcf4a-128">You can define up too5,000 rules per synonym map in a free service and 10,000 rules in all other SKUs.</span></span> <span data-ttu-id="fcf4a-129">Chaque règle peut avoir des expansions de too20.</span><span class="sxs-lookup"><span data-stu-id="fcf4a-129">Each rule can have up too20 expansions.</span></span>

<span data-ttu-id="fcf4a-130">Dans cette version préliminaire, synonyme maps doivent respecter le format hello Apache Solr qui est expliquée ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="fcf4a-130">In this preview, synonym maps must be in hello Apache Solr format which is explained below.</span></span> <span data-ttu-id="fcf4a-131">Si vous disposez d’un dictionnaire de synonyme existant dans un format différent et que vous souhaitez toouse il directement, faites-le nous savoir sur [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span><span class="sxs-lookup"><span data-stu-id="fcf4a-131">If you have an existing synonym dictionary in a different format and want toouse it directly, please let us know on [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span></span>

<span data-ttu-id="fcf4a-132">Vous pouvez créer un nouveau mappage de synonyme à l’aide de la requête HTTP POST, comme dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="fcf4a-132">You can create a new synonym map using HTTP POST, as in hello following example:</span></span>

    POST https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "name":"mysynonymmap",
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

<span data-ttu-id="fcf4a-133">Vous pouvez également utiliser une requête PUT et spécifiez le nom de mappage de synonyme de hello sur hello URI.</span><span class="sxs-lookup"><span data-stu-id="fcf4a-133">Alternatively, you can use PUT and specify hello synonym map name on hello URI.</span></span> <span data-ttu-id="fcf4a-134">Si le mappage de synonyme hello n’existe pas, il sera créé.</span><span class="sxs-lookup"><span data-stu-id="fcf4a-134">If hello synonym map does not exist, it will be created.</span></span>

    PUT https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

##### <a name="apache-solr-synonym-format"></a><span data-ttu-id="fcf4a-135">Format de synonymes Apache Solr</span><span class="sxs-lookup"><span data-stu-id="fcf4a-135">Apache Solr synonym format</span></span>

<span data-ttu-id="fcf4a-136">format de Solr Hello prend en charge les mappages de synonyme équivalent et explicite.</span><span class="sxs-lookup"><span data-stu-id="fcf4a-136">hello Solr format supports equivalent and explicit synonym mappings.</span></span> <span data-ttu-id="fcf4a-137">Règles de mappage de respectent la spécification de filtre du synonyme toohello open source d’Apache Solr, décrites dans ce document : [SynonymFilter](https://cwiki.apache.org/confluence/display/solr/Filter+Descriptions#FilterDescriptions-SynonymFilter).</span><span class="sxs-lookup"><span data-stu-id="fcf4a-137">Mapping rules adhere toohello open source synonym filter specification of Apache Solr, described in this document: [SynonymFilter](https://cwiki.apache.org/confluence/display/solr/Filter+Descriptions#FilterDescriptions-SynonymFilter).</span></span> <span data-ttu-id="fcf4a-138">Voici un exemple de règle pour des synonymes équivalents.</span><span class="sxs-lookup"><span data-stu-id="fcf4a-138">Below is a sample rule for equivalent synonyms.</span></span>
```
              USA, United States, United States of America
```

<span data-ttu-id="fcf4a-139">Règle de hello ci-dessus, une requête de recherche « USA » se développe trop « USA » ou « United States » ou « États-Unis ».</span><span class="sxs-lookup"><span data-stu-id="fcf4a-139">With hello rule above, a search query "USA" will expand too"USA" OR "United States" OR "United States of America".</span></span>

<span data-ttu-id="fcf4a-140">Un mappage explicite est indiqué par une flèche « => ».</span><span class="sxs-lookup"><span data-stu-id="fcf4a-140">Explicit mapping is denoted by an arrow "=>".</span></span> <span data-ttu-id="fcf4a-141">Si spécifié, une séquence de terme d’une requête de recherche qui correspond à la partie gauche de hello de « = > » sera remplacé par alternatives hello sur le côté droit hello.</span><span class="sxs-lookup"><span data-stu-id="fcf4a-141">When specified, a term sequence of a search query that matches hello left hand side of "=>" will be replaced with hello alternatives on hello right hand side.</span></span> <span data-ttu-id="fcf4a-142">Compte tenu de règle hello ci-dessous, les requêtes de recherche « Washington », « Washington »</span><span class="sxs-lookup"><span data-stu-id="fcf4a-142">Given hello rule below, search queries "Washington", "Wash."</span></span> <span data-ttu-id="fcf4a-143">ou « WA » tous copiera trop « WA ».</span><span class="sxs-lookup"><span data-stu-id="fcf4a-143">or "WA" will all be rewritten too"WA".</span></span> <span data-ttu-id="fcf4a-144">Seul le mappage explicite s’applique dans le sens hello spécifié et ne réécrit pas trop de requête hello « WA » « Washington » dans ce cas.</span><span class="sxs-lookup"><span data-stu-id="fcf4a-144">Explicit mapping only applies in hello direction specified and does not rewrite hello query "WA" too"Washington" in this case.</span></span>
```
              Washington, Wash., WA => WA
```

#### <a name="list-synonym-maps-under-your-service"></a><span data-ttu-id="fcf4a-145">Répertorier les cartes de synonymes de votre service.</span><span class="sxs-lookup"><span data-stu-id="fcf4a-145">List synonym maps under your service.</span></span>

    GET https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="get-a-synonym-map-under-your-service"></a><span data-ttu-id="fcf4a-146">Obtenir une carte de synonymes pour votre service.</span><span class="sxs-lookup"><span data-stu-id="fcf4a-146">Get a synonym map under your service.</span></span>

    GET https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="delete-a-synonyms-map-under-your-service"></a><span data-ttu-id="fcf4a-147">Supprimer une carte de synonymes de votre service.</span><span class="sxs-lookup"><span data-stu-id="fcf4a-147">Delete a synonyms map under your service.</span></span>

    DELETE https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

### <a name="configure-a-searchable-field-toouse-hello-synonym-map-in-hello-index-definition"></a><span data-ttu-id="fcf4a-148">Configurer un mappage de champ interrogeable toouse hello synonyme dans la définition de l’index hello.</span><span class="sxs-lookup"><span data-stu-id="fcf4a-148">Configure a searchable field toouse hello synonym map in hello index definition.</span></span>

<span data-ttu-id="fcf4a-149">Une nouvelle propriété de champ **synonymMaps** peut être utilisé toospecify un toouse de carte de synonyme pour un champ de recherche.</span><span class="sxs-lookup"><span data-stu-id="fcf4a-149">A new field property **synonymMaps** can be used toospecify a synonym map toouse for a searchable field.</span></span> <span data-ttu-id="fcf4a-150">Mappages de synonyme sont des ressources de niveau de service et peuvent être référencées par n’importe quel champ d’un index sous le service hello.</span><span class="sxs-lookup"><span data-stu-id="fcf4a-150">Synonym maps are service level resources and can be referenced by any field of an index under hello service.</span></span>

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

<span data-ttu-id="fcf4a-151">**synonymMaps** peut être spécifié pour les champs de recherche de type de hello 'Edm.String' ou 'Collection (EDM.String)'.</span><span class="sxs-lookup"><span data-stu-id="fcf4a-151">**synonymMaps** can be specified for searchable fields of hello type 'Edm.String' or 'Collection(Edm.String)'.</span></span>

> [!NOTE]
> <span data-ttu-id="fcf4a-152">Dans cette version préliminaire, vous pouvez uniquement utiliser une carte de synonymes par champ.</span><span class="sxs-lookup"><span data-stu-id="fcf4a-152">In this preview, you can only have one synonym map per field.</span></span> <span data-ttu-id="fcf4a-153">Si vous souhaitez toouse plusieurs mappages de synonyme, faites-le nous savoir sur [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span><span class="sxs-lookup"><span data-stu-id="fcf4a-153">If you want toouse multiple synonym maps, please let us know on [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span></span>

## <a name="impact-of-synonyms-on-other-search-features"></a><span data-ttu-id="fcf4a-154">Impact des synonymes sur les autres fonctionnalités de recherche</span><span class="sxs-lookup"><span data-stu-id="fcf4a-154">Impact of synonyms on other search features</span></span>

<span data-ttu-id="fcf4a-155">fonctionnalité de synonymes Hello réécrit requête d’origine de hello avec des synonymes par hello opérateur OR.</span><span class="sxs-lookup"><span data-stu-id="fcf4a-155">hello synonyms feature rewrites hello original query with synonyms with hello OR operator.</span></span> <span data-ttu-id="fcf4a-156">Pour cette raison, mise en surbrillance et les profils d’accès traitent des terme d’origine de hello et synonymes comme équivalents.</span><span class="sxs-lookup"><span data-stu-id="fcf4a-156">For this reason, hit highlighting and scoring profiles treat hello original term and synonyms as equivalent.</span></span>

<span data-ttu-id="fcf4a-157">Fonctionnalité de synonyme s’applique toosearch requêtes et ne s’applique pas toofilters ou facettes.</span><span class="sxs-lookup"><span data-stu-id="fcf4a-157">Synonym feature applies toosearch queries and does not apply toofilters or facets.</span></span> <span data-ttu-id="fcf4a-158">De même, les suggestions sont basées uniquement sur le terme d’origine de hello ; correspondances de synonyme n’apparaissent pas dans la réponse de hello.</span><span class="sxs-lookup"><span data-stu-id="fcf4a-158">Similarly, suggestions are based only on hello original term; synonym matches do not appear in hello response.</span></span>

<span data-ttu-id="fcf4a-159">Les expansions de synonyme ne s’appliquent pas les termes de recherche toowildcard ; préfixe, floue et les termes du contrat de l’expression régulière ne sont pas développées.</span><span class="sxs-lookup"><span data-stu-id="fcf4a-159">Synonym expansions do not apply toowildcard search terms; prefix, fuzzy, and regex terms aren't expanded.</span></span>

## <a name="tips-for-building-a-synonym-map"></a><span data-ttu-id="fcf4a-160">Conseils pour créer une carte de synonymes</span><span class="sxs-lookup"><span data-stu-id="fcf4a-160">Tips for building a synonym map</span></span>

- <span data-ttu-id="fcf4a-161">Une carte de synonymes claire et précise est plus efficace qu’une liste exhaustive des correspondances possibles.</span><span class="sxs-lookup"><span data-stu-id="fcf4a-161">A concise, well-designed synonym map is more efficient than an exhaustive list of possible matches.</span></span> <span data-ttu-id="fcf4a-162">Dictionnaires très volumineux ou complexes prennent plus de temps tooparse et affectent la latence requête hello si la requête de hello développe les synonymes de réduire.</span><span class="sxs-lookup"><span data-stu-id="fcf4a-162">Excessively large or complex dictionaries take longer tooparse and affect hello query latency if hello query expands toomany synonyms.</span></span> <span data-ttu-id="fcf4a-163">Au lieu d’estimation à laquelle les termes du contrat peut être utilisé, vous pouvez obtenir des termes du contrat de réel hello via un [rechercher le rapport d’analyse du trafic](search-traffic-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="fcf4a-163">Rather than guess at which terms might be used, you can get hello actual terms via a [search traffic analysis report](search-traffic-analytics.md).</span></span>

- <span data-ttu-id="fcf4a-164">En version préliminaire et la validation d’exercice, activer et ensuite utiliser cette tooprecisely rapport déterminent le termes du contrat de bénéficier d’une correspondance de synonyme et puis continuer toouse en tant que validation que votre mappage synonyme produit les meilleurs résultats.</span><span class="sxs-lookup"><span data-stu-id="fcf4a-164">As both a preliminary and validation exercise, enable and then use this report tooprecisely determine which terms will benefit from a synonym match, and then continue toouse it as validation that your synonym map is producing a better outcome.</span></span> <span data-ttu-id="fcf4a-165">Dans les rapports hello prédéfini, hello vignettes « requêtes de recherche les plus courantes » et « requêtes de recherche de résultat zéro » vous donnera hello les informations nécessaires.</span><span class="sxs-lookup"><span data-stu-id="fcf4a-165">In hello predefined report, hello tiles "Most common search queries" and "Zero-result search queries" will give you hello necessary information.</span></span>

- <span data-ttu-id="fcf4a-166">Vous pouvez créer plusieurs cartes de synonymes pour votre application de recherche (par exemple, par langue si votre application prend en charge une base de clients multilingue).</span><span class="sxs-lookup"><span data-stu-id="fcf4a-166">You can create multiple synonym maps for your search application (for example, by language if your application supports a multi-lingual customer base).</span></span> <span data-ttu-id="fcf4a-167">Actuellement, un champ peut uniquement utiliser une de ces deux méthodes.</span><span class="sxs-lookup"><span data-stu-id="fcf4a-167">Currently, a field can only use one of them.</span></span> <span data-ttu-id="fcf4a-168">Vous pouvez mettre à jour la propriété synonymMaps d’un champ à tout moment.</span><span class="sxs-lookup"><span data-stu-id="fcf4a-168">You can update a field's synonymMaps property at any time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fcf4a-169">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fcf4a-169">Next Steps</span></span>

- <span data-ttu-id="fcf4a-170">Si vous avez un index existant dans un environnement de (hors production) de développement, faites des essais avec un petit dictionnaire toosee comment addition hello de synonymes change hello expérience de recherche, notamment l’impact sur les profils d’accès mise en surbrillance et des suggestions.</span><span class="sxs-lookup"><span data-stu-id="fcf4a-170">If you have an existing index in a development (non-production) environment, experiment with a small dictionary toosee how hello addition of synonyms changes hello search experience, including impact on scoring profiles, hit highlighting, and suggestions.</span></span>

- <span data-ttu-id="fcf4a-171">[Activer la recherche du trafic analytique](search-traffic-analytics.md) et utilisez hello prédéfinies rapport Power BI toolearn les termes utilisés la plupart des et les types retour hello zéro documents.</span><span class="sxs-lookup"><span data-stu-id="fcf4a-171">[Enable search traffic analytics](search-traffic-analytics.md) and use hello predefined Power BI report toolearn which terms are used hello most, and which ones return zero documents.</span></span> <span data-ttu-id="fcf4a-172">Grâce à ces aperçus, modifiez les synonymes de tooinclude dictionnaire hello pour les requêtes non productives qui doivent être résolution toodocuments dans votre index.</span><span class="sxs-lookup"><span data-stu-id="fcf4a-172">Armed with these insights, revise hello dictionary tooinclude synonyms for unproductive queries that should be resolving toodocuments in your index.</span></span>
