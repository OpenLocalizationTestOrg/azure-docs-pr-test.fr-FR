---
title: aaaSearch Analytique de trafic pour Azure Search | Documents Microsoft
description: "Activer analytique le trafic de recherche pour Azure Search, un service de recherche de nuage hébergé sur Microsoft Azure, insights toounlock sur vos données et vos utilisateurs."
services: search
documentationcenter: 
author: bernitorres
manager: jlembicz
editor: 
ms.assetid: b31d79cf-5924-4522-9276-a1bb5d527b13
ms.service: search
ms.devlang: multiple
ms.workload: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/05/2017
ms.author: betorres
ms.openlocfilehash: 1d16aa63d05c1c3df1bbfbb4f09ac77705ed9d9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-search-traffic-analytics"></a><span data-ttu-id="91423-103">Présentation de la recherche de l’analyse du trafic</span><span class="sxs-lookup"><span data-stu-id="91423-103">What is search traffic analytics</span></span>
<span data-ttu-id="91423-104">La recherche de l’analyse du trafic est un modèle qui implémente une boucle de rétroaction pour votre service de recherche.</span><span class="sxs-lookup"><span data-stu-id="91423-104">Search traffic analytics is a pattern for implementing a feedback loop for your search service.</span></span> <span data-ttu-id="91423-105">Ce modèle décrit les données nécessaires hello et comment toocollect à l’aide d’Application Insights, un leader pour l’analyse des services sur plusieurs plateformes.</span><span class="sxs-lookup"><span data-stu-id="91423-105">This pattern describes hello necessary data and how toocollect it using Application Insights, an industry leader for monitoring services in multiple platforms.</span></span>

<span data-ttu-id="91423-106">La recherche de l’analyse du trafic vous permet de gagner en visibilité dans votre service de recherche et de dévoiler des informations sur les utilisateurs et leur comportement.</span><span class="sxs-lookup"><span data-stu-id="91423-106">Search traffic analytics lets you gain visibility into your search service and unlock insights about your users and their behavior.</span></span> <span data-ttu-id="91423-107">En ayant des données relatives à ce que vos utilisateurs choisissent, il est décisions possibles toomake améliorent votre expérience de recherche, puis tooback hors tension lorsque hello résultats ne sont pas ce qui est attendu.</span><span class="sxs-lookup"><span data-stu-id="91423-107">By having data about what your users choose, it's possible toomake decisions that further improve your search experience, and tooback off when hello results are not what expected.</span></span>

<span data-ttu-id="91423-108">Azure Search offre une solution de télémétrie qui intègre l’Application Azure Insights et Power BI tooprovide une analyse approfondie et le suivi.</span><span class="sxs-lookup"><span data-stu-id="91423-108">Azure Search offers a telemetry solution that integrates Azure Application Insights and Power BI tooprovide in-depth monitoring and tracking.</span></span> <span data-ttu-id="91423-109">Étant donné que l’interaction avec Azure Search est uniquement via des API, les données de télémétrie hello doivent être implémentée par hello les développeurs à l’aide de la recherche, suivant les instructions de hello dans cette page.</span><span class="sxs-lookup"><span data-stu-id="91423-109">Because interaction with Azure Search is only through APIs, hello telemetry must be implemented by hello developers using search, following hello instructions in this page.</span></span>

## <a name="identify-hello-relevant-search-data"></a><span data-ttu-id="91423-110">Identifier les données de recherche pertinents hello</span><span class="sxs-lookup"><span data-stu-id="91423-110">Identify hello relevant search data</span></span>

<span data-ttu-id="91423-111">toohave des mesures de recherche, il est nécessaire toolog certaines signale aux utilisateurs de hello hello application de recherche.</span><span class="sxs-lookup"><span data-stu-id="91423-111">toohave useful search metrics, it's necessary toolog some signals from hello users of hello search application.</span></span> <span data-ttu-id="91423-112">Ces signaux indiquent le contenu qui sont intéressés par les utilisateurs et qui sont considérées comme pertinentes tootheir a besoin.</span><span class="sxs-lookup"><span data-stu-id="91423-112">These signals signify content that users are interested in and that they consider relevant tootheir needs.</span></span>

<span data-ttu-id="91423-113">La fonctionnalité Rechercher l’analyse du trafic repose sur deux signaux :</span><span class="sxs-lookup"><span data-stu-id="91423-113">There are two signals Search Traffic Analytics needs:</span></span>

1. <span data-ttu-id="91423-114">Événements de recherche générés par l’utilisateur : ce signal se concentre uniquement sur les requêtes de recherche lancées par un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="91423-114">User generated search events: only search queries initiated by a user are interesting.</span></span> <span data-ttu-id="91423-115">Recherche les demandes utilisés toopopulate facettes, contenu supplémentaire ou des informations internes, ne sont pas importantes et incliner et transformer vos résultats.</span><span class="sxs-lookup"><span data-stu-id="91423-115">Search requests used toopopulate facets, additional content or any internal information, are not important and they skew and bias your results.</span></span>

2. <span data-ttu-id="91423-116">Événements de clic généré par l’utilisateur : par clics dans ce document, nous nous référons utilisateur tooa en sélectionnant un résultat de recherche spécifique retourné à partir d’une requête de recherche.</span><span class="sxs-lookup"><span data-stu-id="91423-116">User generated click events: By clicks in this document, we refer tooa user selecting a particular search result returned from a search query.</span></span> <span data-ttu-id="91423-117">Un clic signifie généralement qu’un document est un résultat pertinent pour une requête de recherche spécifique.</span><span class="sxs-lookup"><span data-stu-id="91423-117">A click generally means that a document is a relevant result for a specific search query.</span></span>

<span data-ttu-id="91423-118">En liant la recherche et cliquez sur les événements avec un id de corrélation, il est possible tooanalyze les comportements de hello des utilisateurs de votre application.</span><span class="sxs-lookup"><span data-stu-id="91423-118">By linking search and click events with a correlation id, it's possible tooanalyze hello behaviors of users on your application.</span></span> <span data-ttu-id="91423-119">Ces informations de recherche sont impossible tooobtain avec recherche uniquement les journaux de trafic.</span><span class="sxs-lookup"><span data-stu-id="91423-119">These search insights are impossible tooobtain with only search traffic logs.</span></span>

## <a name="how-tooimplement-search-traffic-analytics"></a><span data-ttu-id="91423-120">Comment tooimplement recherche analytique de trafic</span><span class="sxs-lookup"><span data-stu-id="91423-120">How tooimplement search traffic analytics</span></span>

<span data-ttu-id="91423-121">les signaux Hello mentionné dans hello précédente section doive être collectée à partir de l’application de recherche hello comme hello utilisateur interagit avec lui.</span><span class="sxs-lookup"><span data-stu-id="91423-121">hello signals mentioned in hello preceding section must be gathered from hello search application as hello user interacts with it.</span></span> <span data-ttu-id="91423-122">Application Insights est une solution d’analyse extensible, disponible pour plusieurs plateformes et qui intègre des options d’instrumentation flexibles.</span><span class="sxs-lookup"><span data-stu-id="91423-122">Application Insights is an extensible monitoring solution, available for multiple platforms, with flexible instrumentation options.</span></span> <span data-ttu-id="91423-123">L’utilisation de l’Application Insights vous permet de tirer parti des rapports de recherche de Power BI hello créé par une analyse Azure Search toomake hello des données plus facilement.</span><span class="sxs-lookup"><span data-stu-id="91423-123">Usage of Application Insights lets you take advantage of hello Power BI search reports created by Azure Search toomake hello analysis of data easier.</span></span>

<span data-ttu-id="91423-124">Bonjour [portal](https://portal.azure.com) page de votre service Azure Search, panneau de recherche le trafic Analytique hello contient un aide-mémoire pour suivre ce modèle de données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="91423-124">In hello [portal](https://portal.azure.com) page for your Azure Search service, hello Search Traffic Analytics blade contains a cheat sheet for following this telemetry pattern.</span></span> <span data-ttu-id="91423-125">Vous pouvez également sélectionner ou créer une ressource Application Insights et afficher des données de hello nécessaire, au même endroit.</span><span class="sxs-lookup"><span data-stu-id="91423-125">You can also select or create an Application Insights resource, and see hello necessary data, all in one place.</span></span>

![Instructions relatives à la recherche de l’analyse du trafic][1]

### <a name="1-select-an-application-insights-resource"></a><span data-ttu-id="91423-127">1. Sélectionner une ressource Application Insights</span><span class="sxs-lookup"><span data-stu-id="91423-127">1. Select an Application Insights resource</span></span>

<span data-ttu-id="91423-128">Vous devez tooselect une toouse de ressource Application Insights ou en créez un, si vous n’avez pas déjà.</span><span class="sxs-lookup"><span data-stu-id="91423-128">You need tooselect an Application Insights resource toouse or create one if you don't have one already.</span></span> <span data-ttu-id="91423-129">Vous pouvez utiliser une ressource qui a déjà utiliser toolog Bonjour requis des événements personnalisés.</span><span class="sxs-lookup"><span data-stu-id="91423-129">You can use a resource that's already in use toolog hello required custom events.</span></span>

<span data-ttu-id="91423-130">Lorsque vous créez une nouvelle ressource Application Insights, tous les types d’application sont valides pour ce scénario.</span><span class="sxs-lookup"><span data-stu-id="91423-130">When creating a new Application Insights resource, all application types are valid for this scenario.</span></span> <span data-ttu-id="91423-131">Sélectionnez hello un qui correspond le mieux à la plateforme hello que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="91423-131">Select hello one that best fits hello platform you are using.</span></span>

<span data-ttu-id="91423-132">Vous devez la clé d’instrumentation hello pour la création de client de télémétrie hello pour votre application.</span><span class="sxs-lookup"><span data-stu-id="91423-132">You need hello instrumentation key for creating hello telemetry client for your application.</span></span> <span data-ttu-id="91423-133">Vous pouvez l’obtenir à partir du tableau de bord portail hello Application Insights, ou vous pouvez l’obtenir à partir de la page de recherche du trafic Analytique hello, sélection d’instance hello souhaité toouse.</span><span class="sxs-lookup"><span data-stu-id="91423-133">You can get it from hello Application Insights portal dashboard, or you can get it from hello Search Traffic Analytics page, selecting hello instance you want toouse.</span></span>

### <a name="2-instrument-your-application"></a><span data-ttu-id="91423-134">2. Instrumenter votre application</span><span class="sxs-lookup"><span data-stu-id="91423-134">2. Instrument your application</span></span>

<span data-ttu-id="91423-135">Cette phase est où vous instrumentez votre propre application de recherche, à l’aide de la ressource d’Application Insights hello votre hello créé dans l’étape ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="91423-135">This phase is where you instrument your own search application, using hello Application Insights resource your created in hello step above.</span></span> <span data-ttu-id="91423-136">Il existe quatre étapes toothis processus :</span><span class="sxs-lookup"><span data-stu-id="91423-136">There are four steps toothis process:</span></span>

<span data-ttu-id="91423-137">**I. Créer un client de télémétrie** il s’agit d’objet hello qui envoie les événements toohello ressource Application Insights.</span><span class="sxs-lookup"><span data-stu-id="91423-137">**I. Create a telemetry client** This is hello object that sends events toohello Application Insights Resource.</span></span>

<span data-ttu-id="91423-138">*C#*</span><span class="sxs-lookup"><span data-stu-id="91423-138">*C#*</span></span>

    private TelemetryClient telemetryClient = new TelemetryClient();
    telemetryClient.InstrumentationKey = "<YOUR INSTRUMENTATION KEY>";

<span data-ttu-id="91423-139">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="91423-139">*JavaScript*</span></span>

    <script type="text/javascript">var appInsights=window.appInsights||function(config){function r(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},u=document,e=window,o="script",s=u.createElement(o),i,f;s.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js";u.getElementsByTagName(o)[0].parentNode.appendChild(s);try{t.cookie=u.cookie}catch(h){}for(t.queue=[],i=["Event","Exception","Metric","PageView","Trace","Dependency"];i.length;)r("track"+i.pop());return r("setAuthenticatedUserContext"),r("clearAuthenticatedUserContext"),config.disableExceptionTracking||(i="onerror",r("_"+i),f=e[i],e[i]=function(config,r,u,e,o){var s=f&&f(config,r,u,e,o);return s!==!0&&t["_"+i](config,r,u,e,o),s}),t}
    ({
    instrumentationKey: "<YOUR INSTRUMENTATION KEY>"
    });
    window.appInsights=appInsights;
    </script>

<span data-ttu-id="91423-140">Pour d’autres langages et les plateformes, consultez hello complète [liste](https://docs.microsoft.com/azure/application-insights/app-insights-platforms).</span><span class="sxs-lookup"><span data-stu-id="91423-140">For other languages and platforms, see hello complete [list](https://docs.microsoft.com/azure/application-insights/app-insights-platforms).</span></span>

<span data-ttu-id="91423-141">**II. Un ID de recherche pour la corrélation de demande** toocorrelate recherche les demandes en clics, il est nécessaire toohave un id de corrélation qui lie ces deux événements distincts.</span><span class="sxs-lookup"><span data-stu-id="91423-141">**II. Request a Search ID for correlation** toocorrelate search requests with clicks, it's necessary toohave a correlation id that relates these two distinct events.</span></span> <span data-ttu-id="91423-142">La Recherche Azure vous fournit un ID de recherche avec un en-tête :</span><span class="sxs-lookup"><span data-stu-id="91423-142">Azure Search provides you with a Search Id when you request it with a header:</span></span>

<span data-ttu-id="91423-143">*C#*</span><span class="sxs-lookup"><span data-stu-id="91423-143">*C#*</span></span>

    // This sample uses hello Azure Search .NET SDK https://www.nuget.org/packages/Microsoft.Azure.Search

    var client = new SearchIndexClient(<ServiceName>, <IndexName>, new SearchCredentials(<QueryKey>)
    var headers = new Dictionary<string, List<string>>() { { "x-ms-azs-return-searchid", new List<string>() { "true" } } };
    var response = await client.Documents.SearchWithHttpMessagesAsync(searchText: searchText, searchParameters: parameters, customHeaders: headers);
    IEnumerable<string> headerValues;
    string searchId = string.Empty;
    if (response.Response.Headers.TryGetValues("x-ms-azs-searchid", out headerValues)){
     searchId = headerValues.FirstOrDefault();
    }

<span data-ttu-id="91423-144">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="91423-144">*JavaScript*</span></span>

    request.setRequestHeader("x-ms-azs-return-searchid", "true");
    request.setRequestHeader("Access-Control-Expose-Headers", "x-ms-azs-searchid");
    var searchId = request.getResponseHeader('x-ms-azs-searchid');

<span data-ttu-id="91423-145">**III. Consigner les événements de recherche**</span><span class="sxs-lookup"><span data-stu-id="91423-145">**III. Log Search events**</span></span>

<span data-ttu-id="91423-146">Chaque fois qu’une demande de recherche est émise par un utilisateur, vous devez vous connecter que comme un événement de recherche avec hello suivant de schéma sur un événement personnalisé Application Insights :</span><span class="sxs-lookup"><span data-stu-id="91423-146">Every time that a search request is issued by a user, you should log that as a search event with hello following schema on an Application Insights custom event:</span></span>

<span data-ttu-id="91423-147">**ServiceName**: nom de service de recherche (string) **SearchId**: identificateur d’unique (guid) de la requête de recherche hello (qui est fourni dans la réponse de recherche hello) **IndexName**: index de service de recherche (chaîne) toobe interrogée **QueryTerms**: les termes de recherche (string) entrés par l’utilisateur de hello **ResultCount**: nombre (entier) de documents qui ont été retournés (fourni dans la réponse de recherche hello)  **ScoringProfile**: nom de hello score profil utilisé, le cas échéant (chaîne)</span><span class="sxs-lookup"><span data-stu-id="91423-147">**ServiceName**: (string) search service name **SearchId**: (guid) unique identifier of hello search query (comes in hello search response) **IndexName**: (string) search service index toobe queried **QueryTerms**: (string) search terms entered by hello user **ResultCount**: (int) number of documents that were returned (comes in hello search response) **ScoringProfile**: (string) name of hello scoring profile used, if any</span></span>

> [!NOTE]
> <span data-ttu-id="91423-148">Nombre de demandes sur des requêtes généré par l’utilisateur en ajoutant $count = true tooyour la requête de recherche.</span><span class="sxs-lookup"><span data-stu-id="91423-148">Request count on user generated queries by adding $count=true tooyour search query.</span></span> <span data-ttu-id="91423-149">Plus d’informations, cliquez [ici](https://docs.microsoft.com/rest/api/searchservice/search-documents#request)</span><span class="sxs-lookup"><span data-stu-id="91423-149">See more information [here](https://docs.microsoft.com/rest/api/searchservice/search-documents#request)</span></span>
>

> [!NOTE]
> <span data-ttu-id="91423-150">N’oubliez pas de requêtes de recherche de journal tooonly qui sont générés par les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="91423-150">Remember tooonly log search queries that are generated by users.</span></span>
>

<span data-ttu-id="91423-151">*C#*</span><span class="sxs-lookup"><span data-stu-id="91423-151">*C#*</span></span>

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search Id>},
    {"IndexName", <index name>},
    {"QueryTerms", <search terms>},
    {"ResultCount", <results count>},
    {"ScoringProfile", <scoring profile used>}
    };
    telemetryClient.TrackEvent("Search", properties);

<span data-ttu-id="91423-152">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="91423-152">*JavaScript*</span></span>

    appInsights.trackEvent("Search", {
    SearchServiceName: <service name>,
    SearchId: <search id>,
    IndexName: <index name>,
    QueryTerms: <search terms>,
    ResultCount: <results count>,
    ScoringProfile: <scoring profile used>
    });

<span data-ttu-id="91423-153">**IV. Consigner les événements de clic**</span><span class="sxs-lookup"><span data-stu-id="91423-153">**IV. Log Click events**</span></span>

<span data-ttu-id="91423-154">Chaque fois qu’un utilisateur clique sur un document, vous obtenez un signal qui doit être consigné afin d’analyser la recherche.</span><span class="sxs-lookup"><span data-stu-id="91423-154">Every time that a user clicks on a document, that's a signal that must be logged for search analysis purposes.</span></span> <span data-ttu-id="91423-155">Utilisez Application Insights événements personnalisés toolog ces événements avec hello suivant le schéma :</span><span class="sxs-lookup"><span data-stu-id="91423-155">Use Application Insights custom events toolog these events with hello following schema:</span></span>

<span data-ttu-id="91423-156">**ServiceName**: nom de service de recherche (string) **SearchId**: identificateur d’unique (guid) de requête de recherche connexes hello **DocId**: identificateur de document (string) **Position** : page de résultats de rang (int) du document hello dans la recherche de hello</span><span class="sxs-lookup"><span data-stu-id="91423-156">**ServiceName**: (string) search service name **SearchId**: (guid) unique identifier of hello related search query **DocId**: (string) document identifier **Position**: (int) rank of hello document in hello search results page</span></span>

> [!NOTE]
> <span data-ttu-id="91423-157">Position fait référence ordre toohello cardinale dans votre application.</span><span class="sxs-lookup"><span data-stu-id="91423-157">Position refers toohello cardinal order in your application.</span></span> <span data-ttu-id="91423-158">Vous êtes libre tooset ce nombre, tant qu’il a toujours hello identiques, tooallow pour la comparaison.</span><span class="sxs-lookup"><span data-stu-id="91423-158">You are free tooset this number, as long as it's always hello same, tooallow for comparison.</span></span>
>

<span data-ttu-id="91423-159">*C#*</span><span class="sxs-lookup"><span data-stu-id="91423-159">*C#*</span></span>

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search id>},
    {"ClickedDocId", <clicked document id>},
    {"Rank", <clicked document position>}
    };
    telemetryClient.TrackEvent("Click", properties);

<span data-ttu-id="91423-160">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="91423-160">*JavaScript*</span></span>

    appInsights.TrackEvent("Click", {
        SearchServiceName: <service name>,
        SearchId: <search id>,
        ClickedDocId: <clicked document id>,
        Rank: <clicked document position>
    });

### <a name="3-analyze-with-power-bi-desktop"></a><span data-ttu-id="91423-161">3. Analyser avec Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="91423-161">3. Analyze with Power BI Desktop</span></span>

<span data-ttu-id="91423-162">Après avoir instrumenté votre application et vérifiez que votre application est correctement connecté tooApplication Insights, vous pouvez utiliser un modèle prédéfini créé par Azure Search pour Power BI desktop.</span><span class="sxs-lookup"><span data-stu-id="91423-162">After you have instrumented your app and verified your application is correctly connected tooApplication Insights, you can use a predefined template created by Azure Search for Power BI desktop.</span></span>
<span data-ttu-id="91423-163">Ce modèle contient des graphiques et tables qui vous aident à rendent tooimprove de décisions éclairée vos performances de recherche et la pertinence.</span><span class="sxs-lookup"><span data-stu-id="91423-163">This template contains charts and tables that help you make more informed decisions tooimprove your search performance and relevance.</span></span>

<span data-ttu-id="91423-164">tooinstantiate hello Power BI un modèle de bureau, vous avez besoin de trois informations sur Application Insights.</span><span class="sxs-lookup"><span data-stu-id="91423-164">tooinstantiate hello Power BI desktop template, you need three pieces of information about Application Insights.</span></span> <span data-ttu-id="91423-165">Ces données sont accessibles dans la page de recherche du trafic Analytique hello, lorsque vous sélectionnez hello ressource toouse</span><span class="sxs-lookup"><span data-stu-id="91423-165">This data can be found in hello Search Traffic Analytics page, when you select hello resource toouse</span></span>

![Données d’application Insights dans le panneau de recherche le trafic Analytique hello][2]

<span data-ttu-id="91423-167">Mesures inclus dans le modèle de bureau hello Power BI :</span><span class="sxs-lookup"><span data-stu-id="91423-167">Metrics included in hello Power BI desktop template:</span></span>

*   <span data-ttu-id="91423-168">Cliquez sur via le taux (CTR) : rapport entre les utilisateurs qui cliquent sur un nombre de toohello document spécifique du nombre total de recherches.</span><span class="sxs-lookup"><span data-stu-id="91423-168">Click through Rate (CTR): ratio of users who click on a specific document toohello number of total searches.</span></span>
*   <span data-ttu-id="91423-169">Recherches sans clic : termes renvoyant aux principales requêtes qui n’enregistrent aucun clic</span><span class="sxs-lookup"><span data-stu-id="91423-169">Searches without clicks: terms for top queries that register no clicks</span></span>
*   <span data-ttu-id="91423-170">Un clic sur plus de documents : plus un clic sur des documents par ID Bonjour des dernières 24 heures, des 7 derniers jours et 30 jours.</span><span class="sxs-lookup"><span data-stu-id="91423-170">Most clicked documents: most clicked documents by ID in hello last 24 hours, 7 days, and 30 days.</span></span>
*   <span data-ttu-id="91423-171">Les paires de terme-documents les plus courants : les conditions qui entraînent une hello même document un clic, classés par clics.</span><span class="sxs-lookup"><span data-stu-id="91423-171">Popular term-document pairs: terms that result in hello same document clicked, ordered by clicks.</span></span>
*   <span data-ttu-id="91423-172">Heure tooclick : clics leur durée écoulée depuis la requête de recherche hello</span><span class="sxs-lookup"><span data-stu-id="91423-172">Time tooclick: clicks bucketed by time since hello search query</span></span>

![Modèle Power BI pour lire à partir d’Application Insights][3]


## <a name="next-steps"></a><span data-ttu-id="91423-174">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="91423-174">Next Steps</span></span>
<span data-ttu-id="91423-175">Instrumenter votre application tooget intéressante et puissantes données de recherche sur votre service de recherche.</span><span class="sxs-lookup"><span data-stu-id="91423-175">Instrument your search application tooget powerful and insightful data about your search service.</span></span>

<span data-ttu-id="91423-176">Pour plus d’informations sur Application Insights, cliquez [ici](https://go.microsoft.com/fwlink/?linkid=842905).</span><span class="sxs-lookup"><span data-stu-id="91423-176">You can find more information on Application Insights [here](https://go.microsoft.com/fwlink/?linkid=842905).</span></span> <span data-ttu-id="91423-177">Visitez Application Insights [page de tarification](https://azure.microsoft.com/pricing/details/application-insights/) toolearn plus d’informations sur les différents niveaux de service.</span><span class="sxs-lookup"><span data-stu-id="91423-177">Visit Application Insights [pricing page](https://azure.microsoft.com/pricing/details/application-insights/) toolearn more about their different service tiers.</span></span>

<span data-ttu-id="91423-178">En savoir plus sur la création de rapports exceptionnels.</span><span class="sxs-lookup"><span data-stu-id="91423-178">Learn more about creating amazing reports.</span></span> <span data-ttu-id="91423-179">Pour plus d’informations, consultez [Prise en main de Power BI Desktop](https://powerbi.microsoft.com/en-us/documentation/powerbi-desktop-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="91423-179">See [Getting started with Power BI Desktop](https://powerbi.microsoft.com/en-us/documentation/powerbi-desktop-getting-started/) for details</span></span>

<!--Image references-->
[1]: ./media/search-traffic-analytics/AzureSearch-TrafficAnalytics.png
[2]: ./media/search-traffic-analytics/AzureSearch-AppInsightsData.png
[3]: ./media/search-traffic-analytics/AzureSearch-PBITemplate.png
