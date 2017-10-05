---
title: "Analytics, le puissant outil de recherche d’Azure Application Insights | Microsoft Docs"
description: "Présentation d’Analytics, le puissant outil de recherche d’Application Insights. "
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
ms.openlocfilehash: 8174745a00a107eea648b223a00466b6a7f37331
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="analytics-in-application-insights"></a><span data-ttu-id="3770f-103">Analytics dans Application Insights</span><span class="sxs-lookup"><span data-stu-id="3770f-103">Analytics in Application Insights</span></span>
<span data-ttu-id="3770f-104">[Analytics](app-insights-analytics.md) est la fonctionnalité de recherche performante [d’Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3770f-104">[Analytics](app-insights-analytics.md) is the powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="3770f-105">Ces pages décrivent le langage de requête Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="3770f-105">These pages describe the Log Analytics query language.</span></span> 

* <span data-ttu-id="3770f-106">**[Regardez la vidéo d’introduction](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span><span class="sxs-lookup"><span data-stu-id="3770f-106">**[Watch the introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="3770f-107">**[Testez la version d’évaluation d’Analytics sur nos données simulées](https://analytics.applicationinsights.io/demo)** si votre application n’envoie pas encore de données à Application Insights.</span><span class="sxs-lookup"><span data-stu-id="3770f-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data to Application Insights yet.</span></span>
* <span data-ttu-id="3770f-108">**[L’aide-mémoire des utilisateurs de SQL](https://aka.ms/sql-analytics)** traduit les idiomes courants.</span><span class="sxs-lookup"><span data-stu-id="3770f-108">**[SQL-users' cheat sheet](https://aka.ms/sql-analytics)** translates the most common idioms.</span></span>
* <span data-ttu-id="3770f-109">**[Référence du langage](app-insights-analytics-reference.md)** Apprenez à utiliser toutes les puissantes fonctionnalités du langage de requête Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="3770f-109">**[Language Reference](app-insights-analytics-reference.md)** Learn how to use all the powerful features of the Log Analytics query language.</span></span>


## <a name="queries-in-analytics"></a><span data-ttu-id="3770f-110">Requêtes dans Analytics</span><span class="sxs-lookup"><span data-stu-id="3770f-110">Queries in Analytics</span></span>
<span data-ttu-id="3770f-111">Une requête classique est une table *source* suivie d’une série *d’opérateurs* séparés par des `|`.</span><span class="sxs-lookup"><span data-stu-id="3770f-111">A typical query is a *source* table followed by a series of *operators* separated by `|`.</span></span> 

<span data-ttu-id="3770f-112">Par exemple, essayons de découvrir à quelle heure les citoyens de Hyderabad accèdent à notre application web.</span><span class="sxs-lookup"><span data-stu-id="3770f-112">For example, let's find out what time of day the citizens of Hyderabad try our web app.</span></span> <span data-ttu-id="3770f-113">Et parallèlement, découvrons les codes de résultats qui sont retournés à leurs requêtes HTTP.</span><span class="sxs-lookup"><span data-stu-id="3770f-113">And while we're there, let's see what result codes are returned to their HTTP requests.</span></span> 

```AIQL
requests
| where timestamp > ago(30d)
| summarize ClientCount = dcount(client_IP) by bin(timestamp, 1h), resultCode
| extend LocalTime = timestamp - 4h
| order by LocalTime desc
| render barchart
```

<span data-ttu-id="3770f-114">Nous comptons des adresses IP client distinctes, en les regroupant par heure de la journée sur les sept derniers jours.</span><span class="sxs-lookup"><span data-stu-id="3770f-114">We count distinct client IP addresses, grouping them by the hour of the day over the past 7 days.</span></span> 

> [!NOTE]
> <span data-ttu-id="3770f-115">Pour obtenir des résultats en dehors des dernières 24 heures, incluez explicitement « timestamp » dans votre requête ou utiliser le menu déroulant avec la plage de temps.</span><span class="sxs-lookup"><span data-stu-id="3770f-115">To get results outside the previous 24h, either include 'timestamp' explicitly in your query, or use the time range drop-down menu.</span></span>
>

<span data-ttu-id="3770f-116">Affichons les résultats avec la présentation graphique à barres, en choisissant d’empiler les résultats issus de codes de réponse différents :</span><span class="sxs-lookup"><span data-stu-id="3770f-116">Let's display the results with the bar chart presentation, choosing to stack the results from different response codes:</span></span>

![Sélectionnez le graphique à barres, les axes x et y, puis la segmentation](./media/app-insights-analytics/020.png)

<span data-ttu-id="3770f-118">Il semblerait que notre application soit plus populaire lors de la pause déjeuner et à l’heure du coucher à Hyderabad.</span><span class="sxs-lookup"><span data-stu-id="3770f-118">Looks like our app is most popular at lunchtime and bed-time in Hyderabad.</span></span> <span data-ttu-id="3770f-119">(Et nous devrions examiner ces 500 codes).</span><span class="sxs-lookup"><span data-stu-id="3770f-119">(And we should investigate those 500 codes.)</span></span>

<span data-ttu-id="3770f-120">Il existe également des opérations statistiques puissantes :</span><span class="sxs-lookup"><span data-stu-id="3770f-120">There are also powerful statistical operations:</span></span>

![Résultats d’une requête statistique](./media/app-insights-analytics/025.png)

<span data-ttu-id="3770f-122">Le langage possède de nombreuses fonctionnalités attrayantes :</span><span class="sxs-lookup"><span data-stu-id="3770f-122">The language has many attractive features:</span></span>


* <span data-ttu-id="3770f-123">[Filtrer](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) vos données de télémétrie d’application brutes sur tous les champs, y compris les propriétés et métriques personnalisées.</span><span class="sxs-lookup"><span data-stu-id="3770f-123">[Filter](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) your raw app telemetry by any fields, including your custom properties and metrics.</span></span>
* <span data-ttu-id="3770f-124">[Joindre](https://docs.loganalytics.io/queryLanguage/query_language_joinoperator.html) plusieurs tables ; mettez en corrélation les demandes avec les affichages de page, les appels de dépendance, les exceptions et les suivis du journal.</span><span class="sxs-lookup"><span data-stu-id="3770f-124">[Join](https://docs.loganalytics.io/queryLanguage/query_language_joinoperator.html) multiple tables – correlate requests with page views, dependency calls, exceptions and log traces.</span></span>
* <span data-ttu-id="3770f-125">[Agrégations](https://docs.loganalytics.io/learn/tutorials/aggregations.html)statistiques puissantes.</span><span class="sxs-lookup"><span data-stu-id="3770f-125">Powerful statistical [aggregations](https://docs.loganalytics.io/learn/tutorials/aggregations.html).</span></span>
* <span data-ttu-id="3770f-126">Toutes aussi puissantes que SQL, mais beaucoup plus facile pour les requêtes complexes : au lieu d’imbriquer des instructions, vous dirigez les données d’une opération élémentaire à l’autre.</span><span class="sxs-lookup"><span data-stu-id="3770f-126">Just as powerful as SQL, but much easier for complex queries: instead of nesting statements, you pipe the data from one elementary operation to the next.</span></span>
* <span data-ttu-id="3770f-127">Visualisations immédiates et puissantes.</span><span class="sxs-lookup"><span data-stu-id="3770f-127">Immediate and powerful visualizations.</span></span>
* <span data-ttu-id="3770f-128">[Épingler des graphiques sur les tableaux de bord Azure](app-insights-analytics-using.md#pin-to-dashboard).</span><span class="sxs-lookup"><span data-stu-id="3770f-128">[Pin charts to Azure dashboards](app-insights-analytics-using.md#pin-to-dashboard).</span></span>
* <span data-ttu-id="3770f-129">[Exporter des requêtes dans Power BI](app-insights-analytics-using.md#export-to-power-bi).</span><span class="sxs-lookup"><span data-stu-id="3770f-129">[Export queries to Power BI](app-insights-analytics-using.md#export-to-power-bi).</span></span>
* <span data-ttu-id="3770f-130">Il existe une [API REST](https://dev.applicationinsights.io/) que vous pouvez utiliser pour exécuter des requêtes par programme, par exemple à partir de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3770f-130">There's a [REST API](https://dev.applicationinsights.io/) that you can use to run queries programmatically, for example from Powershell.</span></span>


## <a name="connect-to-your-application-insights-data"></a><span data-ttu-id="3770f-131">Connectez-vous à vos données Application Insights</span><span class="sxs-lookup"><span data-stu-id="3770f-131">Connect to your Application Insights data</span></span>
<span data-ttu-id="3770f-132">Ouvrez Analytics à partir du [panneau Vue d’ensemble](app-insights-dashboards.md) de votre application dans Application Insights :</span><span class="sxs-lookup"><span data-stu-id="3770f-132">Open Analytics from your app's [overview blade](app-insights-dashboards.md) in Application Insights:</span></span> 

![Ouvrez portal.azure.com, ouvrez votre ressource Application Insights, puis cliquez sur Analyse.](./media/app-insights-analytics/001.png)


## <a name="video"></a><span data-ttu-id="3770f-134">Vidéo</span><span class="sxs-lookup"><span data-stu-id="3770f-134">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]



## <a name="query-examples"></a><span data-ttu-id="3770f-135">Exemples de requête</span><span class="sxs-lookup"><span data-stu-id="3770f-135">Query examples</span></span>

<span data-ttu-id="3770f-136">Essayez ces procédures pas à pas pour illustrer la puissance de l’utilisation d’Analytics :</span><span class="sxs-lookup"><span data-stu-id="3770f-136">Try these walkthroughs to illustrate the power of using Analytics:</span></span>

 *  [<span data-ttu-id="3770f-137">Diagnostic automatique des pics et sauts d’étape dans les durées des demandes</span><span class="sxs-lookup"><span data-stu-id="3770f-137">Automatic diagnostics of spikes and step jumps in requests durations</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Automatic%20diagnostics%20of%20sudden%20spikes%20or%20step%20jumps%20in%20requests%20duration&shared=true)
 *  [<span data-ttu-id="3770f-138">Analyse des baisses de performances avec l’analyse de séries chronologiques</span><span class="sxs-lookup"><span data-stu-id="3770f-138">Analyzing performance degradations with time series analysis</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20performance%20degradations%20with%20time%20series%20analysis&shared=true)
 *  [<span data-ttu-id="3770f-139">Analyse des défaillances d’application avec le cluster automatique et les modèles différentiels</span><span class="sxs-lookup"><span data-stu-id="3770f-139">Analyzing application failures with autocluster and diffpatterns</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20application%20failures%20with%20autocluster%20and%20diffpatterns&shared=true)
 *  [<span data-ttu-id="3770f-140">Détections de formes avancées avec l’analyse des séries chronologiques</span><span class="sxs-lookup"><span data-stu-id="3770f-140">Advanced shape detections with time series analysis</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Advanced%20shape%20detection%20with%20time%20series%20analysis&shared=true)
 *  [<span data-ttu-id="3770f-141">Utilisation d’opérations de fenêtre glissante pour analyser l’utilisation des applications (déploiement MAU/DAU, etc.)</span><span class="sxs-lookup"><span data-stu-id="3770f-141">Using sliding window operations to analyze application usage (rolling MAU/DAU etc)</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Using%20sliding%20window%20calculations%20to%20analyze%20usage%20metrics:%20rolling%20MAU~2FDAU%20and%20cohorts&shared=true)
 *  <span data-ttu-id="3770f-142">[Détection des interruptions de service en fonction de l’analyse des journaux de débogage](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Detection%20of%20service%20disruptions%20based%20on%20regression%20analysis%20of%20trace%20logs&shared=true) et billet de blog sur le même sujet disponible [ici](https://maximshklar.wordpress.com/2017/02/16/finding-trends-in-traces-with-smart-data-analytics).</span><span class="sxs-lookup"><span data-stu-id="3770f-142">[Detection of service disruptions based on analysis of debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Detection%20of%20service%20disruptions%20based%20on%20regression%20analysis%20of%20trace%20logs&shared=true) and a matching blog post [here](https://maximshklar.wordpress.com/2017/02/16/finding-trends-in-traces-with-smart-data-analytics).</span></span>
 *  <span data-ttu-id="3770f-143">[Profilage des performances des applications à l’aide de simples journaux de débogage](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Profiling%20applications'%20performance%20with%20simple%20debug%20logs&shared=true) et billet de blog sur le même sujet disponible [ici](https://yossiattasblog.wordpress.com/2017/03/13/first-blog-post/)</span><span class="sxs-lookup"><span data-stu-id="3770f-143">[Profiling applications’ performance using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Profiling%20applications'%20performance%20with%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/13/first-blog-post/)</span></span>
 *  <span data-ttu-id="3770f-144">[Mesure de la durée de chaque étape dans votre flux de code à l’aide de simples journaux de débogage](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Measuring%20the%20duration%20of%20each%20step%20in%20your%20code%20flow%20using%20simple%20debug%20logs&shared=true) et billet de blog sur le même sujet disponible [ici](https://yossiattasblog.wordpress.com/2017/03/14/measuring-the-duration-of-each-step-in-your-code-flow-using-simple-debug-logs/)</span><span class="sxs-lookup"><span data-stu-id="3770f-144">[Measuring the duration for each step in your code flow using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Measuring%20the%20duration%20of%20each%20step%20in%20your%20code%20flow%20using%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/14/measuring-the-duration-of-each-step-in-your-code-flow-using-simple-debug-logs/)</span></span>
 *  <span data-ttu-id="3770f-145">[Analyse de l’accès concurrentiel à l’aide de simples journaux de débogage](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Analyzing%20concurrency%20with%20simple%20debug%20logs&shared=true) et billet de blog sur le même sujet disponible [ici](https://yossiattasblog.wordpress.com/2017/03/23/analyzing-concurrency-using-simple-debug-logs/)</span><span class="sxs-lookup"><span data-stu-id="3770f-145">[Analyzing concurrency using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Analyzing%20concurrency%20with%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/23/analyzing-concurrency-using-simple-debug-logs/)</span></span>



## <a name="next-steps"></a><span data-ttu-id="3770f-146">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3770f-146">Next steps</span></span>
* <span data-ttu-id="3770f-147">Nous vous recommandons de commencer par la [visite guidée du langage](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="3770f-147">We recommend you start with the [language tour](app-insights-analytics-tour.md).</span></span> 
* <span data-ttu-id="3770f-148">En savoir plus sur [l’utilisation de l’analytique](app-insights-analytics-using.md).</span><span class="sxs-lookup"><span data-stu-id="3770f-148">More about [using Analytics](app-insights-analytics-using.md).</span></span> 
* <span data-ttu-id="3770f-149">[Informations de référence sur le langage](app-insights-analytics-reference.md).</span><span class="sxs-lookup"><span data-stu-id="3770f-149">[Language reference](app-insights-analytics-reference.md).</span></span> 
