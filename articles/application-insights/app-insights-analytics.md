---
title: "aaaAnalytics - hello puissant outil de recherche de l’Application Azure Insights | Documents Microsoft"
description: "Vue d’ensemble de l’Analytique, hello diagnostic outil puissant d’Application Insights. "
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 0a2f6011-5bcf-47b7-8450-40f284274b24
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: d2b41e2fff7cc786e11fa3dfe94fc46f1b86e9eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="analytics-in-application-insights"></a><span data-ttu-id="eeab3-103">Analytics dans Application Insights</span><span class="sxs-lookup"><span data-stu-id="eeab3-103">Analytics in Application Insights</span></span>
<span data-ttu-id="eeab3-104">[Analytique](app-insights-analytics.md) fonctionnalité de recherche puissant de hello de [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="eeab3-104">[Analytics](app-insights-analytics.md) is hello powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="eeab3-105">Ces pages décrivent le langage de requête Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="eeab3-105">These pages describe the Log Analytics query language.</span></span> 

* <span data-ttu-id="eeab3-106">**[Regardez la vidéo de présentation hello](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span><span class="sxs-lookup"><span data-stu-id="eeab3-106">**[Watch hello introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="eeab3-107">**[Testez l’Analytique sur nos données simulées](https://analytics.applicationinsights.io/demo)**  si votre application n’envoie pas de données tooApplication Insights encore.</span><span class="sxs-lookup"><span data-stu-id="eeab3-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data tooApplication Insights yet.</span></span>
* <span data-ttu-id="eeab3-108">**[Feuille de graphique SQL utilisateurs](https://aka.ms/sql-analytics)**  traduit idiomes courants de hello.</span><span class="sxs-lookup"><span data-stu-id="eeab3-108">**[SQL-users' cheat sheet](https://aka.ms/sql-analytics)** translates hello most common idioms.</span></span>
* <span data-ttu-id="eeab3-109">**[Référence du langage](app-insights-analytics-reference.md)**  apprendre comment toouse tous les hello puissantes fonctionnalités de langage de requête Analytique de journal de hello.</span><span class="sxs-lookup"><span data-stu-id="eeab3-109">**[Language Reference](app-insights-analytics-reference.md)** Learn how toouse all hello powerful features of hello Log Analytics query language.</span></span>


## <a name="queries-in-analytics"></a><span data-ttu-id="eeab3-110">Requêtes dans Analytics</span><span class="sxs-lookup"><span data-stu-id="eeab3-110">Queries in Analytics</span></span>
<span data-ttu-id="eeab3-111">Une requête classique est une table *source* suivie d’une série *d’opérateurs* séparés par des `|`.</span><span class="sxs-lookup"><span data-stu-id="eeab3-111">A typical query is a *source* table followed by a series of *operators* separated by `|`.</span></span> 

<span data-ttu-id="eeab3-112">Par exemple, voyons quelle heure du jour hello éléments de premier ordre de Hyderabad Essayez notre application web.</span><span class="sxs-lookup"><span data-stu-id="eeab3-112">For example, let's find out what time of day hello citizens of Hyderabad try our web app.</span></span> <span data-ttu-id="eeab3-113">Et pendant que nous sommes il, nous allons voir les codes de résultat sont retournées les demandes tootheir HTTP.</span><span class="sxs-lookup"><span data-stu-id="eeab3-113">And while we're there, let's see what result codes are returned tootheir HTTP requests.</span></span> 

```AIQL
requests
| where timestamp > ago(30d)
| summarize ClientCount = dcount(client_IP) by bin(timestamp, 1h), resultCode
| extend LocalTime = timestamp - 4h
| order by LocalTime desc
| render barchart
```

<span data-ttu-id="eeab3-114">Nous compter les adresses IP de client distincts, les regrouper par hello heure hello sur hello des 7 derniers jours.</span><span class="sxs-lookup"><span data-stu-id="eeab3-114">We count distinct client IP addresses, grouping them by hello hour of hello day over hello past 7 days.</span></span> 

> [!NOTE]
> <span data-ttu-id="eeab3-115">résultats tooget en dehors de hello précédente 24h, inclure explicitement des « timestamp » dans votre requête, ou utilisez le menu de liste déroulante de plage de temps hello.</span><span class="sxs-lookup"><span data-stu-id="eeab3-115">tooget results outside hello previous 24h, either include 'timestamp' explicitly in your query, or use hello time range drop-down menu.</span></span>
>

<span data-ttu-id="eeab3-116">Résultats hello avec hello barre présentation graphique, en sélectionnant toostack hello les résultats à partir des codes de réponse différents s’affichent :</span><span class="sxs-lookup"><span data-stu-id="eeab3-116">Let's display hello results with hello bar chart presentation, choosing toostack hello results from different response codes:</span></span>

![Sélectionnez le graphique à barres, les axes x et y, puis la segmentation](./media/app-insights-analytics/020.png)

<span data-ttu-id="eeab3-118">Il semblerait que notre application soit plus populaire lors de la pause déjeuner et à l’heure du coucher à Hyderabad.</span><span class="sxs-lookup"><span data-stu-id="eeab3-118">Looks like our app is most popular at lunchtime and bed-time in Hyderabad.</span></span> <span data-ttu-id="eeab3-119">(Et nous devrions examiner ces 500 codes).</span><span class="sxs-lookup"><span data-stu-id="eeab3-119">(And we should investigate those 500 codes.)</span></span>

<span data-ttu-id="eeab3-120">Il existe également des opérations statistiques puissantes :</span><span class="sxs-lookup"><span data-stu-id="eeab3-120">There are also powerful statistical operations:</span></span>

![Résultats d’une requête statistique](./media/app-insights-analytics/025.png)

<span data-ttu-id="eeab3-122">langue de Hello propose de nombreuses fonctionnalités intéressante :</span><span class="sxs-lookup"><span data-stu-id="eeab3-122">hello language has many attractive features:</span></span>


* <span data-ttu-id="eeab3-123">[Filtrer](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) vos données de télémétrie d’application brutes sur tous les champs, y compris les propriétés et métriques personnalisées.</span><span class="sxs-lookup"><span data-stu-id="eeab3-123">[Filter](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) your raw app telemetry by any fields, including your custom properties and metrics.</span></span>
* <span data-ttu-id="eeab3-124">[Joindre](https://docs.loganalytics.io/queryLanguage/query_language_joinoperator.html) plusieurs tables ; mettez en corrélation les demandes avec les affichages de page, les appels de dépendance, les exceptions et les suivis du journal.</span><span class="sxs-lookup"><span data-stu-id="eeab3-124">[Join](https://docs.loganalytics.io/queryLanguage/query_language_joinoperator.html) multiple tables – correlate requests with page views, dependency calls, exceptions and log traces.</span></span>
* <span data-ttu-id="eeab3-125">[Agrégations](https://docs.loganalytics.io/learn/tutorials/aggregations.html)statistiques puissantes.</span><span class="sxs-lookup"><span data-stu-id="eeab3-125">Powerful statistical [aggregations](https://docs.loganalytics.io/learn/tutorials/aggregations.html).</span></span>
* <span data-ttu-id="eeab3-126">Tout aussi puissantes que SQL, mais il est beaucoup plus facile pour les requêtes complexes : au lieu de l’imbrication d’instructions, vous diriger les données de salutation à partir d’une opération élémentaire toohello ensuite.</span><span class="sxs-lookup"><span data-stu-id="eeab3-126">Just as powerful as SQL, but much easier for complex queries: instead of nesting statements, you pipe hello data from one elementary operation toohello next.</span></span>
* <span data-ttu-id="eeab3-127">Visualisations immédiates et puissantes.</span><span class="sxs-lookup"><span data-stu-id="eeab3-127">Immediate and powerful visualizations.</span></span>
* <span data-ttu-id="eeab3-128">[Code confidentiel graphiques des tableaux de bord tooAzure](app-insights-analytics-using.md#pin-to-dashboard).</span><span class="sxs-lookup"><span data-stu-id="eeab3-128">[Pin charts tooAzure dashboards](app-insights-analytics-using.md#pin-to-dashboard).</span></span>
* <span data-ttu-id="eeab3-129">[Exporter des requêtes tooPower BI](app-insights-analytics-using.md#export-to-power-bi).</span><span class="sxs-lookup"><span data-stu-id="eeab3-129">[Export queries tooPower BI](app-insights-analytics-using.md#export-to-power-bi).</span></span>
* <span data-ttu-id="eeab3-130">Il existe un [API REST](https://dev.applicationinsights.io/) que vous pouvez utiliser les requêtes toorun par programme, par exemple à partir de Powershell.</span><span class="sxs-lookup"><span data-stu-id="eeab3-130">There's a [REST API](https://dev.applicationinsights.io/) that you can use toorun queries programmatically, for example from Powershell.</span></span>


## <a name="connect-tooyour-application-insights-data"></a><span data-ttu-id="eeab3-131">Connecter des données d’Application Insights tooyour</span><span class="sxs-lookup"><span data-stu-id="eeab3-131">Connect tooyour Application Insights data</span></span>
<span data-ttu-id="eeab3-132">Ouvrez Analytics à partir du [panneau Vue d’ensemble](app-insights-dashboards.md) de votre application dans Application Insights :</span><span class="sxs-lookup"><span data-stu-id="eeab3-132">Open Analytics from your app's [overview blade](app-insights-dashboards.md) in Application Insights:</span></span> 

![Ouvrez portal.azure.com, ouvrez votre ressource Application Insights, puis cliquez sur Analyse.](./media/app-insights-analytics/001.png)


## <a name="video"></a><span data-ttu-id="eeab3-134">Vidéo</span><span class="sxs-lookup"><span data-stu-id="eeab3-134">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]



## <a name="query-examples"></a><span data-ttu-id="eeab3-135">Exemples de requête</span><span class="sxs-lookup"><span data-stu-id="eeab3-135">Query examples</span></span>

<span data-ttu-id="eeab3-136">Essayez ces puissance hello tooillustrate procédures pas à pas à l’aide d’Analytique :</span><span class="sxs-lookup"><span data-stu-id="eeab3-136">Try these walkthroughs tooillustrate hello power of using Analytics:</span></span>

 *  [<span data-ttu-id="eeab3-137">Diagnostic automatique des pics et sauts d’étape dans les durées des demandes</span><span class="sxs-lookup"><span data-stu-id="eeab3-137">Automatic diagnostics of spikes and step jumps in requests durations</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Automatic%20diagnostics%20of%20sudden%20spikes%20or%20step%20jumps%20in%20requests%20duration&shared=true)
 *  [<span data-ttu-id="eeab3-138">Analyse des baisses de performances avec l’analyse de séries chronologiques</span><span class="sxs-lookup"><span data-stu-id="eeab3-138">Analyzing performance degradations with time series analysis</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20performance%20degradations%20with%20time%20series%20analysis&shared=true)
 *  [<span data-ttu-id="eeab3-139">Analyse des défaillances d’application avec le cluster automatique et les modèles différentiels</span><span class="sxs-lookup"><span data-stu-id="eeab3-139">Analyzing application failures with autocluster and diffpatterns</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20application%20failures%20with%20autocluster%20and%20diffpatterns&shared=true)
 *  [<span data-ttu-id="eeab3-140">Détections de formes avancées avec l’analyse des séries chronologiques</span><span class="sxs-lookup"><span data-stu-id="eeab3-140">Advanced shape detections with time series analysis</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Advanced%20shape%20detection%20with%20time%20series%20analysis&shared=true)
 *  [<span data-ttu-id="eeab3-141">À l’aide de glissante fenêtre opérations tooanalyze l’utilisation des applications (déploiement de MAU/DAU etc.)</span><span class="sxs-lookup"><span data-stu-id="eeab3-141">Using sliding window operations tooanalyze application usage (rolling MAU/DAU etc)</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Using%20sliding%20window%20calculations%20to%20analyze%20usage%20metrics:%20rolling%20MAU~2FDAU%20and%20cohorts&shared=true)
 *  <span data-ttu-id="eeab3-142">[Détection des interruptions de service en fonction de l’analyse des journaux de débogage](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Detection%20of%20service%20disruptions%20based%20on%20regression%20analysis%20of%20trace%20logs&shared=true) et billet de blog sur le même sujet disponible [ici](https://maximshklar.wordpress.com/2017/02/16/finding-trends-in-traces-with-smart-data-analytics).</span><span class="sxs-lookup"><span data-stu-id="eeab3-142">[Detection of service disruptions based on analysis of debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Detection%20of%20service%20disruptions%20based%20on%20regression%20analysis%20of%20trace%20logs&shared=true) and a matching blog post [here](https://maximshklar.wordpress.com/2017/02/16/finding-trends-in-traces-with-smart-data-analytics).</span></span>
 *  <span data-ttu-id="eeab3-143">[Profilage des performances des applications à l’aide de simples journaux de débogage](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Profiling%20applications'%20performance%20with%20simple%20debug%20logs&shared=true) et billet de blog sur le même sujet disponible [ici](https://yossiattasblog.wordpress.com/2017/03/13/first-blog-post/)</span><span class="sxs-lookup"><span data-stu-id="eeab3-143">[Profiling applications’ performance using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Profiling%20applications'%20performance%20with%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/13/first-blog-post/)</span></span>
 *  <span data-ttu-id="eeab3-144">[Mesure la durée hello pour chaque étape dans votre flux de code à l’aide des journaux de débogage simple](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Measuring%20the%20duration%20of%20each%20step%20in%20your%20code%20flow%20using%20simple%20debug%20logs&shared=true) et un billet de blog correspondant [ici](https://yossiattasblog.wordpress.com/2017/03/14/measuring-the-duration-of-each-step-in-your-code-flow-using-simple-debug-logs/)</span><span class="sxs-lookup"><span data-stu-id="eeab3-144">[Measuring hello duration for each step in your code flow using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Measuring%20the%20duration%20of%20each%20step%20in%20your%20code%20flow%20using%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/14/measuring-the-duration-of-each-step-in-your-code-flow-using-simple-debug-logs/)</span></span>
 *  <span data-ttu-id="eeab3-145">[Analyse de l’accès concurrentiel à l’aide de simples journaux de débogage](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Analyzing%20concurrency%20with%20simple%20debug%20logs&shared=true) et billet de blog sur le même sujet disponible [ici](https://yossiattasblog.wordpress.com/2017/03/23/analyzing-concurrency-using-simple-debug-logs/)</span><span class="sxs-lookup"><span data-stu-id="eeab3-145">[Analyzing concurrency using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Analyzing%20concurrency%20with%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/23/analyzing-concurrency-using-simple-debug-logs/)</span></span>



## <a name="next-steps"></a><span data-ttu-id="eeab3-146">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="eeab3-146">Next steps</span></span>
* <span data-ttu-id="eeab3-147">Nous vous recommandons de commencer par hello [visite guidée du langage](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="eeab3-147">We recommend you start with hello [language tour](app-insights-analytics-tour.md).</span></span> 
* <span data-ttu-id="eeab3-148">En savoir plus sur [l’utilisation de l’analytique](app-insights-analytics-using.md).</span><span class="sxs-lookup"><span data-stu-id="eeab3-148">More about [using Analytics](app-insights-analytics-using.md).</span></span> 
* <span data-ttu-id="eeab3-149">[Informations de référence sur le langage](app-insights-analytics-reference.md).</span><span class="sxs-lookup"><span data-stu-id="eeab3-149">[Language reference](app-insights-analytics-reference.md).</span></span> 
