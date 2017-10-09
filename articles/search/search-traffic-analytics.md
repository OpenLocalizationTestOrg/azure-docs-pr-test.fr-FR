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
# <a name="what-is-search-traffic-analytics"></a>Présentation de la recherche de l’analyse du trafic
La recherche de l’analyse du trafic est un modèle qui implémente une boucle de rétroaction pour votre service de recherche. Ce modèle décrit les données nécessaires hello et comment toocollect à l’aide d’Application Insights, un leader pour l’analyse des services sur plusieurs plateformes.

La recherche de l’analyse du trafic vous permet de gagner en visibilité dans votre service de recherche et de dévoiler des informations sur les utilisateurs et leur comportement. En ayant des données relatives à ce que vos utilisateurs choisissent, il est décisions possibles toomake améliorent votre expérience de recherche, puis tooback hors tension lorsque hello résultats ne sont pas ce qui est attendu.

Azure Search offre une solution de télémétrie qui intègre l’Application Azure Insights et Power BI tooprovide une analyse approfondie et le suivi. Étant donné que l’interaction avec Azure Search est uniquement via des API, les données de télémétrie hello doivent être implémentée par hello les développeurs à l’aide de la recherche, suivant les instructions de hello dans cette page.

## <a name="identify-hello-relevant-search-data"></a>Identifier les données de recherche pertinents hello

toohave des mesures de recherche, il est nécessaire toolog certaines signale aux utilisateurs de hello hello application de recherche. Ces signaux indiquent le contenu qui sont intéressés par les utilisateurs et qui sont considérées comme pertinentes tootheir a besoin.

La fonctionnalité Rechercher l’analyse du trafic repose sur deux signaux :

1. Événements de recherche générés par l’utilisateur : ce signal se concentre uniquement sur les requêtes de recherche lancées par un utilisateur. Recherche les demandes utilisés toopopulate facettes, contenu supplémentaire ou des informations internes, ne sont pas importantes et incliner et transformer vos résultats.

2. Événements de clic généré par l’utilisateur : par clics dans ce document, nous nous référons utilisateur tooa en sélectionnant un résultat de recherche spécifique retourné à partir d’une requête de recherche. Un clic signifie généralement qu’un document est un résultat pertinent pour une requête de recherche spécifique.

En liant la recherche et cliquez sur les événements avec un id de corrélation, il est possible tooanalyze les comportements de hello des utilisateurs de votre application. Ces informations de recherche sont impossible tooobtain avec recherche uniquement les journaux de trafic.

## <a name="how-tooimplement-search-traffic-analytics"></a>Comment tooimplement recherche analytique de trafic

les signaux Hello mentionné dans hello précédente section doive être collectée à partir de l’application de recherche hello comme hello utilisateur interagit avec lui. Application Insights est une solution d’analyse extensible, disponible pour plusieurs plateformes et qui intègre des options d’instrumentation flexibles. L’utilisation de l’Application Insights vous permet de tirer parti des rapports de recherche de Power BI hello créé par une analyse Azure Search toomake hello des données plus facilement.

Bonjour [portal](https://portal.azure.com) page de votre service Azure Search, panneau de recherche le trafic Analytique hello contient un aide-mémoire pour suivre ce modèle de données de télémétrie. Vous pouvez également sélectionner ou créer une ressource Application Insights et afficher des données de hello nécessaire, au même endroit.

![Instructions relatives à la recherche de l’analyse du trafic][1]

### <a name="1-select-an-application-insights-resource"></a>1. Sélectionner une ressource Application Insights

Vous devez tooselect une toouse de ressource Application Insights ou en créez un, si vous n’avez pas déjà. Vous pouvez utiliser une ressource qui a déjà utiliser toolog Bonjour requis des événements personnalisés.

Lorsque vous créez une nouvelle ressource Application Insights, tous les types d’application sont valides pour ce scénario. Sélectionnez hello un qui correspond le mieux à la plateforme hello que vous utilisez.

Vous devez la clé d’instrumentation hello pour la création de client de télémétrie hello pour votre application. Vous pouvez l’obtenir à partir du tableau de bord portail hello Application Insights, ou vous pouvez l’obtenir à partir de la page de recherche du trafic Analytique hello, sélection d’instance hello souhaité toouse.

### <a name="2-instrument-your-application"></a>2. Instrumenter votre application

Cette phase est où vous instrumentez votre propre application de recherche, à l’aide de la ressource d’Application Insights hello votre hello créé dans l’étape ci-dessus. Il existe quatre étapes toothis processus :

**I. Créer un client de télémétrie** il s’agit d’objet hello qui envoie les événements toohello ressource Application Insights.

*C#*

    private TelemetryClient telemetryClient = new TelemetryClient();
    telemetryClient.InstrumentationKey = "<YOUR INSTRUMENTATION KEY>";

*JavaScript*

    <script type="text/javascript">var appInsights=window.appInsights||function(config){function r(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},u=document,e=window,o="script",s=u.createElement(o),i,f;s.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js";u.getElementsByTagName(o)[0].parentNode.appendChild(s);try{t.cookie=u.cookie}catch(h){}for(t.queue=[],i=["Event","Exception","Metric","PageView","Trace","Dependency"];i.length;)r("track"+i.pop());return r("setAuthenticatedUserContext"),r("clearAuthenticatedUserContext"),config.disableExceptionTracking||(i="onerror",r("_"+i),f=e[i],e[i]=function(config,r,u,e,o){var s=f&&f(config,r,u,e,o);return s!==!0&&t["_"+i](config,r,u,e,o),s}),t}
    ({
    instrumentationKey: "<YOUR INSTRUMENTATION KEY>"
    });
    window.appInsights=appInsights;
    </script>

Pour d’autres langages et les plateformes, consultez hello complète [liste](https://docs.microsoft.com/azure/application-insights/app-insights-platforms).

**II. Un ID de recherche pour la corrélation de demande** toocorrelate recherche les demandes en clics, il est nécessaire toohave un id de corrélation qui lie ces deux événements distincts. La Recherche Azure vous fournit un ID de recherche avec un en-tête :

*C#*

    // This sample uses hello Azure Search .NET SDK https://www.nuget.org/packages/Microsoft.Azure.Search

    var client = new SearchIndexClient(<ServiceName>, <IndexName>, new SearchCredentials(<QueryKey>)
    var headers = new Dictionary<string, List<string>>() { { "x-ms-azs-return-searchid", new List<string>() { "true" } } };
    var response = await client.Documents.SearchWithHttpMessagesAsync(searchText: searchText, searchParameters: parameters, customHeaders: headers);
    IEnumerable<string> headerValues;
    string searchId = string.Empty;
    if (response.Response.Headers.TryGetValues("x-ms-azs-searchid", out headerValues)){
     searchId = headerValues.FirstOrDefault();
    }

*JavaScript*

    request.setRequestHeader("x-ms-azs-return-searchid", "true");
    request.setRequestHeader("Access-Control-Expose-Headers", "x-ms-azs-searchid");
    var searchId = request.getResponseHeader('x-ms-azs-searchid');

**III. Consigner les événements de recherche**

Chaque fois qu’une demande de recherche est émise par un utilisateur, vous devez vous connecter que comme un événement de recherche avec hello suivant de schéma sur un événement personnalisé Application Insights :

**ServiceName**: nom de service de recherche (string) **SearchId**: identificateur d’unique (guid) de la requête de recherche hello (qui est fourni dans la réponse de recherche hello) **IndexName**: index de service de recherche (chaîne) toobe interrogée **QueryTerms**: les termes de recherche (string) entrés par l’utilisateur de hello **ResultCount**: nombre (entier) de documents qui ont été retournés (fourni dans la réponse de recherche hello)  **ScoringProfile**: nom de hello score profil utilisé, le cas échéant (chaîne)

> [!NOTE]
> Nombre de demandes sur des requêtes généré par l’utilisateur en ajoutant $count = true tooyour la requête de recherche. Plus d’informations, cliquez [ici](https://docs.microsoft.com/rest/api/searchservice/search-documents#request)
>

> [!NOTE]
> N’oubliez pas de requêtes de recherche de journal tooonly qui sont générés par les utilisateurs.
>

*C#*

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search Id>},
    {"IndexName", <index name>},
    {"QueryTerms", <search terms>},
    {"ResultCount", <results count>},
    {"ScoringProfile", <scoring profile used>}
    };
    telemetryClient.TrackEvent("Search", properties);

*JavaScript*

    appInsights.trackEvent("Search", {
    SearchServiceName: <service name>,
    SearchId: <search id>,
    IndexName: <index name>,
    QueryTerms: <search terms>,
    ResultCount: <results count>,
    ScoringProfile: <scoring profile used>
    });

**IV. Consigner les événements de clic**

Chaque fois qu’un utilisateur clique sur un document, vous obtenez un signal qui doit être consigné afin d’analyser la recherche. Utilisez Application Insights événements personnalisés toolog ces événements avec hello suivant le schéma :

**ServiceName**: nom de service de recherche (string) **SearchId**: identificateur d’unique (guid) de requête de recherche connexes hello **DocId**: identificateur de document (string) **Position** : page de résultats de rang (int) du document hello dans la recherche de hello

> [!NOTE]
> Position fait référence ordre toohello cardinale dans votre application. Vous êtes libre tooset ce nombre, tant qu’il a toujours hello identiques, tooallow pour la comparaison.
>

*C#*

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search id>},
    {"ClickedDocId", <clicked document id>},
    {"Rank", <clicked document position>}
    };
    telemetryClient.TrackEvent("Click", properties);

*JavaScript*

    appInsights.TrackEvent("Click", {
        SearchServiceName: <service name>,
        SearchId: <search id>,
        ClickedDocId: <clicked document id>,
        Rank: <clicked document position>
    });

### <a name="3-analyze-with-power-bi-desktop"></a>3. Analyser avec Power BI Desktop

Après avoir instrumenté votre application et vérifiez que votre application est correctement connecté tooApplication Insights, vous pouvez utiliser un modèle prédéfini créé par Azure Search pour Power BI desktop.
Ce modèle contient des graphiques et tables qui vous aident à rendent tooimprove de décisions éclairée vos performances de recherche et la pertinence.

tooinstantiate hello Power BI un modèle de bureau, vous avez besoin de trois informations sur Application Insights. Ces données sont accessibles dans la page de recherche du trafic Analytique hello, lorsque vous sélectionnez hello ressource toouse

![Données d’application Insights dans le panneau de recherche le trafic Analytique hello][2]

Mesures inclus dans le modèle de bureau hello Power BI :

*   Cliquez sur via le taux (CTR) : rapport entre les utilisateurs qui cliquent sur un nombre de toohello document spécifique du nombre total de recherches.
*   Recherches sans clic : termes renvoyant aux principales requêtes qui n’enregistrent aucun clic
*   Un clic sur plus de documents : plus un clic sur des documents par ID Bonjour des dernières 24 heures, des 7 derniers jours et 30 jours.
*   Les paires de terme-documents les plus courants : les conditions qui entraînent une hello même document un clic, classés par clics.
*   Heure tooclick : clics leur durée écoulée depuis la requête de recherche hello

![Modèle Power BI pour lire à partir d’Application Insights][3]


## <a name="next-steps"></a>Étapes suivantes
Instrumenter votre application tooget intéressante et puissantes données de recherche sur votre service de recherche.

Pour plus d’informations sur Application Insights, cliquez [ici](https://go.microsoft.com/fwlink/?linkid=842905). Visitez Application Insights [page de tarification](https://azure.microsoft.com/pricing/details/application-insights/) toolearn plus d’informations sur les différents niveaux de service.

En savoir plus sur la création de rapports exceptionnels. Pour plus d’informations, consultez [Prise en main de Power BI Desktop](https://powerbi.microsoft.com/en-us/documentation/powerbi-desktop-getting-started/).

<!--Image references-->
[1]: ./media/search-traffic-analytics/AzureSearch-TrafficAnalytics.png
[2]: ./media/search-traffic-analytics/AzureSearch-AppInsightsData.png
[3]: ./media/search-traffic-analytics/AzureSearch-PBITemplate.png
