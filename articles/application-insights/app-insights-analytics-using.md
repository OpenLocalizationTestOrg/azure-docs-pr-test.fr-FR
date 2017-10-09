---
title: "aaaUsing Analytique - hello puissant outil de recherche de l’Application Azure Insights | Documents Microsoft"
description: "À l’aide de hello Analytique, hello diagnostic outil puissant d’Application Insights. "
services: application-insights
documentationcenter: 
author: danhadari
manager: carmonm
ms.assetid: c3b34430-f592-4c32-b900-e9f50ca096b3
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 6e0246848457db368c57d08c47b5bf73f4e5e3a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-analytics-in-application-insights"></a><span data-ttu-id="8ab71-103">Utilisation d’Analytics dans Application Insights</span><span class="sxs-lookup"><span data-stu-id="8ab71-103">Using Analytics in Application Insights</span></span>
<span data-ttu-id="8ab71-104">[Analytique](app-insights-analytics.md) fonctionnalité de recherche puissant de hello de [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8ab71-104">[Analytics](app-insights-analytics.md) is hello powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="8ab71-105">Ces pages décrivent le langage de requête Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="8ab71-105">These pages describe the Log Analytics query language.</span></span>

* <span data-ttu-id="8ab71-106">**[Regardez la vidéo de présentation hello](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span><span class="sxs-lookup"><span data-stu-id="8ab71-106">**[Watch hello introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="8ab71-107">**[Testez l’Analytique sur nos données simulées](https://analytics.applicationinsights.io/demo)**  si votre application n’envoie pas de données tooApplication Insights encore.</span><span class="sxs-lookup"><span data-stu-id="8ab71-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data tooApplication Insights yet.</span></span>

## <a name="open-analytics"></a><span data-ttu-id="8ab71-108">Ouverture de la fonctionnalité Analytics</span><span class="sxs-lookup"><span data-stu-id="8ab71-108">Open Analytics</span></span>
<span data-ttu-id="8ab71-109">À partir de la ressource de base de votre application dans Application Insights, cliquez sur Analytics.</span><span class="sxs-lookup"><span data-stu-id="8ab71-109">From your app's home resource in Application Insights, click Analytics.</span></span>

![Ouvrez portal.azure.com, ouvrez votre ressource Application Insights, puis cliquez sur Analyse.](./media/app-insights-analytics-using/001.png)

<span data-ttu-id="8ab71-111">didacticiel d’inline Hello vous donne quelques idées sur ce que vous pouvez faire.</span><span class="sxs-lookup"><span data-stu-id="8ab71-111">hello inline tutorial gives you some ideas about what you can do.</span></span>

<span data-ttu-id="8ab71-112">Vous pouvez cependant consulter [ici une présentation approfondie](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="8ab71-112">There's a [more extensive tour here](app-insights-analytics-tour.md).</span></span>

## <a name="query-your-telemetry"></a><span data-ttu-id="8ab71-113">Interrogation de votre télémétrie</span><span class="sxs-lookup"><span data-stu-id="8ab71-113">Query your telemetry</span></span>
### <a name="write-a-query"></a><span data-ttu-id="8ab71-114">Écrivez votre requête.</span><span class="sxs-lookup"><span data-stu-id="8ab71-114">Write a query</span></span>
![Affichage du schéma](./media/app-insights-analytics-using/150.png)

<span data-ttu-id="8ab71-116">Commencer avec des noms de toutes les tables hello figurant sur la gauche de hello hello (ou hello [plage](https://docs.loganalytics.io/queryLanguage/query_language_rangeoperator.html) ou [union](https://docs.loganalytics.io/queryLanguage/query_language_unionoperator.html) opérateurs).</span><span class="sxs-lookup"><span data-stu-id="8ab71-116">Begin with hello names of any of hello tables listed on hello left (or hello [range](https://docs.loganalytics.io/queryLanguage/query_language_rangeoperator.html) or [union](https://docs.loganalytics.io/queryLanguage/query_language_unionoperator.html) operators).</span></span> <span data-ttu-id="8ab71-117">Utilisez `|` toocreate un pipeline de [opérateurs](https://docs.loganalytics.io/learn/cheatsheets/useful_operators.html).</span><span class="sxs-lookup"><span data-stu-id="8ab71-117">Use `|` toocreate a pipeline of [operators](https://docs.loganalytics.io/learn/cheatsheets/useful_operators.html).</span></span> 

<span data-ttu-id="8ab71-118">IntelliSense affiche les opérateurs hello et éléments d’expression hello que vous pouvez utiliser.</span><span class="sxs-lookup"><span data-stu-id="8ab71-118">IntelliSense prompts you with hello operators and hello expression elements that you can use.</span></span> <span data-ttu-id="8ab71-119">Cliquez sur icône d’information hello (ou appuyez sur CTRL + espace) tooget une description plus détaillée et des exemples de toouse chaque élément.</span><span class="sxs-lookup"><span data-stu-id="8ab71-119">Click hello information icon (or press CTRL+Space) tooget a longer description and examples of how toouse each element.</span></span>

<span data-ttu-id="8ab71-120">Consultez hello [visite guidée du langage Analytique](app-insights-analytics-tour.md) et [référence du langage](app-insights-analytics-reference.md).</span><span class="sxs-lookup"><span data-stu-id="8ab71-120">See hello [Analytics language tour](app-insights-analytics-tour.md) and [language reference](app-insights-analytics-reference.md).</span></span>

### <a name="run-a-query"></a><span data-ttu-id="8ab71-121">Exécution d’une requête</span><span class="sxs-lookup"><span data-stu-id="8ab71-121">Run a query</span></span>
![Exécution d’une requête](./media/app-insights-analytics-using/130.png)

1. <span data-ttu-id="8ab71-123">Vous pouvez utiliser des sauts de ligne uniques dans une requête.</span><span class="sxs-lookup"><span data-stu-id="8ab71-123">You can use single line breaks in a query.</span></span>
2. <span data-ttu-id="8ab71-124">Placez le curseur hello à l’intérieur ou à fin hello de requête hello toorun.</span><span class="sxs-lookup"><span data-stu-id="8ab71-124">Put hello cursor inside or at hello end of hello query you want toorun.</span></span>
3. <span data-ttu-id="8ab71-125">Vérifiez la plage de temps hello de votre requête.</span><span class="sxs-lookup"><span data-stu-id="8ab71-125">Check hello time range of your query.</span></span> <span data-ttu-id="8ab71-126">(Vous pouvez le modifier ou le remplacer en incluant votre propre clause [`where...timestamp...`](https://docs.loganalytics.io/concepts/concepts_datatypes_timespan.html) dans la requête.)</span><span class="sxs-lookup"><span data-stu-id="8ab71-126">(You can change it, or override it by including your own [`where...timestamp...`](https://docs.loganalytics.io/concepts/concepts_datatypes_timespan.html) clause in your query.)</span></span>
3. <span data-ttu-id="8ab71-127">Cliquez sur OK toorun hello la requête.</span><span class="sxs-lookup"><span data-stu-id="8ab71-127">Click Go toorun hello query.</span></span>
4. <span data-ttu-id="8ab71-128">N’insérez pas de lignes vides dans votre requête.</span><span class="sxs-lookup"><span data-stu-id="8ab71-128">Don't put blank lines in your query.</span></span> <span data-ttu-id="8ab71-129">Vous pouvez conserver plusieurs requêtes séparées dans un onglet de requête en les séparant par des lignes vides.</span><span class="sxs-lookup"><span data-stu-id="8ab71-129">You can keep several separated queries in one query tab by separating them with blank lines.</span></span> <span data-ttu-id="8ab71-130">Uniquement les requêtes de hello dont le curseur de hello s’exécute.</span><span class="sxs-lookup"><span data-stu-id="8ab71-130">Only hello query that has hello cursor runs.</span></span>

### <a name="save-a-query"></a><span data-ttu-id="8ab71-131">Enregistrement d’une requête</span><span class="sxs-lookup"><span data-stu-id="8ab71-131">Save a query</span></span>
![Enregistrement d’une requête](./media/app-insights-analytics-using/140.png)

1. <span data-ttu-id="8ab71-133">Enregistrer le fichier de requête en cours hello.</span><span class="sxs-lookup"><span data-stu-id="8ab71-133">Save hello current query file.</span></span>
2. <span data-ttu-id="8ab71-134">Ouvrez un fichier de requête enregistré.</span><span class="sxs-lookup"><span data-stu-id="8ab71-134">Open a saved query file.</span></span>
3. <span data-ttu-id="8ab71-135">Créez un fichier de requête.</span><span class="sxs-lookup"><span data-stu-id="8ab71-135">Create a new query file.</span></span>

## <a name="see-hello-details"></a><span data-ttu-id="8ab71-136">Afficher les détails de hello</span><span class="sxs-lookup"><span data-stu-id="8ab71-136">See hello details</span></span>
<span data-ttu-id="8ab71-137">Développez toute ligne dans hello résultats toosee sa liste complète des propriétés.</span><span class="sxs-lookup"><span data-stu-id="8ab71-137">Expand any row in hello results toosee its complete list of properties.</span></span> <span data-ttu-id="8ab71-138">Vous pouvez développer davantage de toute propriété qui est une valeur structurée - par exemple, des dimensions personnalisées ou pile hello dans une exception.</span><span class="sxs-lookup"><span data-stu-id="8ab71-138">You can further expand any property that is a structured value - for example, custom dimensions, or hello stack listing in an exception.</span></span>

![Extension d’une ligne](./media/app-insights-analytics-using/070.png)

## <a name="arrange-hello-results"></a><span data-ttu-id="8ab71-140">Organiser les résultats de hello</span><span class="sxs-lookup"><span data-stu-id="8ab71-140">Arrange hello results</span></span>
<span data-ttu-id="8ab71-141">Vous pouvez trier, filtrer, paginer et regrouper les résultats hello retournés à partir de votre requête.</span><span class="sxs-lookup"><span data-stu-id="8ab71-141">You can sort, filter, paginate, and group hello results returned from your query.</span></span>

> [!NOTE]
> <span data-ttu-id="8ab71-142">Tri, regroupement et filtrage dans le navigateur de hello ne réexécutez votre requête.</span><span class="sxs-lookup"><span data-stu-id="8ab71-142">Sorting, grouping, and filtering in hello browser don't re-run your query.</span></span> <span data-ttu-id="8ab71-143">Ils réorganiser uniquement les résultats de hello qui ont été renvoyés par votre dernière requête.</span><span class="sxs-lookup"><span data-stu-id="8ab71-143">They only rearrange hello results that were returned by your last query.</span></span> 
> 
> <span data-ttu-id="8ab71-144">tooperform ces tâches dans le serveur hello hello résultats sont retournés, avant d’écrire votre requête avec hello [tri](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html), [résumer](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) et [où](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) opérateurs.</span><span class="sxs-lookup"><span data-stu-id="8ab71-144">tooperform these tasks in hello server before hello results are returned, write your query with hello [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html), [summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) and [where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) operators.</span></span>
> 
> 

<span data-ttu-id="8ab71-145">Choisir des colonnes hello vous le feriez pour tout comme toosee, faire glisser toorearrange des en-têtes de colonne, ainsi que les colonnes de redimensionnement en faisant glisser ses bordures.</span><span class="sxs-lookup"><span data-stu-id="8ab71-145">Pick hello columns you'd like toosee, drag column headers toorearrange them, and resize columns by dragging their borders.</span></span>

![Réorganisation de colonnes](./media/app-insights-analytics-using/030.png)

### <a name="sort-and-filter-items"></a><span data-ttu-id="8ab71-147">Tri et filtrage d’éléments</span><span class="sxs-lookup"><span data-stu-id="8ab71-147">Sort and filter items</span></span>
<span data-ttu-id="8ab71-148">Trier les résultats en cliquant sur head hello d’une colonne.</span><span class="sxs-lookup"><span data-stu-id="8ab71-148">Sort your results by clicking hello head of a column.</span></span> <span data-ttu-id="8ab71-149">Cliquez de nouveau sur toosort hello autre façon, et cliquez une troisième fois toorevert toohello tri d’origine retourné par la requête.</span><span class="sxs-lookup"><span data-stu-id="8ab71-149">Click again toosort hello other way, and click a third time toorevert toohello original ordering returned by your query.</span></span>

<span data-ttu-id="8ab71-150">Utilisez hello filtre icône toonarrow votre recherche.</span><span class="sxs-lookup"><span data-stu-id="8ab71-150">Use hello filter icon toonarrow your search.</span></span>

![Tri et filtrage de colonnes](./media/app-insights-analytics-using/040.png)

### <a name="group-items"></a><span data-ttu-id="8ab71-152">Regroupement d’éléments</span><span class="sxs-lookup"><span data-stu-id="8ab71-152">Group items</span></span>
<span data-ttu-id="8ab71-153">toosort par plusieurs colonnes, utilisez le regroupement.</span><span class="sxs-lookup"><span data-stu-id="8ab71-153">toosort by more than one column, use grouping.</span></span> <span data-ttu-id="8ab71-154">Tout d’abord l’activer, puis faites glisser les en-têtes de colonne dans l’espace hello au-dessus de table de hello.</span><span class="sxs-lookup"><span data-stu-id="8ab71-154">First enable it, and then drag column headers into hello space above hello table.</span></span>

![Groupe](./media/app-insights-analytics-using/060.png)

### <a name="missing-some-results"></a><span data-ttu-id="8ab71-156">Certains résultats manquent ?</span><span class="sxs-lookup"><span data-stu-id="8ab71-156">Missing some results?</span></span>

<span data-ttu-id="8ab71-157">Si vous pensez que vous ne voyez pas tous les résultats hello prévu, il existe plusieurs raisons possibles.</span><span class="sxs-lookup"><span data-stu-id="8ab71-157">If you think you're not seeing all hello results you expected, there are a couple of possible reasons.</span></span>

* <span data-ttu-id="8ab71-158">**Filtre d'intervalle de temps**.</span><span class="sxs-lookup"><span data-stu-id="8ab71-158">**Time range filter**.</span></span> <span data-ttu-id="8ab71-159">Par défaut, vous verrez seulement les résultats à partir de hello des dernières 24 heures.</span><span class="sxs-lookup"><span data-stu-id="8ab71-159">By default, you will only see results from hello last 24 hours.</span></span> <span data-ttu-id="8ab71-160">Il existe un filtre automatique qui limite la plage hello de résultats qui sont récupérés à partir des tables de source de hello.</span><span class="sxs-lookup"><span data-stu-id="8ab71-160">There is an automatic filter that limits hello range of results that are retrieved from hello source tables.</span></span> 

    <span data-ttu-id="8ab71-161">Toutefois, vous pouvez modifier l’intervalle de temps hello filtre à l’aide du menu déroulant de hello.</span><span class="sxs-lookup"><span data-stu-id="8ab71-161">However, you can change hello time range filter by using hello drop-down menu.</span></span>

    <span data-ttu-id="8ab71-162">Ou vous pouvez remplacer la plage d’automatique hello en incluant votre propre [ `where  ... timestamp ...` clause](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) dans votre requête.</span><span class="sxs-lookup"><span data-stu-id="8ab71-162">Or you can override hello automatic range by including your own [`where  ... timestamp ...` clause](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) into your query.</span></span> <span data-ttu-id="8ab71-163">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="8ab71-163">For example:</span></span>

    `requests | where timestamp > ago('2d')`

* <span data-ttu-id="8ab71-164">**Limite de résultats**.</span><span class="sxs-lookup"><span data-stu-id="8ab71-164">**Results limit**.</span></span> <span data-ttu-id="8ab71-165">Il existe une limite de lignes environ 10 k hello de résultats à partir du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="8ab71-165">There's a limit of about 10k rows on hello results returned from hello portal.</span></span> <span data-ttu-id="8ab71-166">Un avertissement apparaît si vous passez la limite hello.</span><span class="sxs-lookup"><span data-stu-id="8ab71-166">A warning shows if you go over hello limit.</span></span> <span data-ttu-id="8ab71-167">Si cela se produit, vos résultats dans la table de hello de tri ne sont pas toujours afficher vous tous les hello réel premier ou derniers résultats.</span><span class="sxs-lookup"><span data-stu-id="8ab71-167">If that happens, sorting your results in hello table won't always show you all hello actual first or last results.</span></span> 

    <span data-ttu-id="8ab71-168">Il s’agit de limite de bonnes pratiques tooavoid atteinte hello.</span><span class="sxs-lookup"><span data-stu-id="8ab71-168">It's good practice tooavoid hitting hello limit.</span></span> <span data-ttu-id="8ab71-169">Utilisez le filtre d’intervalle de temps hello, ou utiliser des opérateurs tels que :</span><span class="sxs-lookup"><span data-stu-id="8ab71-169">Use hello time range filter, or use operators such as:</span></span>

  * [<span data-ttu-id="8ab71-170">top 100 by timestamp</span><span class="sxs-lookup"><span data-stu-id="8ab71-170">top 100 by timestamp</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) 
  * [<span data-ttu-id="8ab71-171">take 100</span><span class="sxs-lookup"><span data-stu-id="8ab71-171">take 100</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html)
  * [<span data-ttu-id="8ab71-172">summarize </span><span class="sxs-lookup"><span data-stu-id="8ab71-172">summarize </span></span>](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) 
  * [<span data-ttu-id="8ab71-173">where timestamp &gt; ago(3d)</span><span class="sxs-lookup"><span data-stu-id="8ab71-173">where timestamp > ago(3d)</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html)

<span data-ttu-id="8ab71-174">(Vous voulez plus de 10 000 lignes ?</span><span class="sxs-lookup"><span data-stu-id="8ab71-174">(Want more than 10k rows?</span></span> <span data-ttu-id="8ab71-175">Utilisez plutôt l'[exportation continue](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="8ab71-175">Consider using [Continuous Export](app-insights-export-telemetry.md) instead.</span></span> <span data-ttu-id="8ab71-176">Analytics est conçu pour l'analyse plutôt que pour la récupération de données brutes.)</span><span class="sxs-lookup"><span data-stu-id="8ab71-176">Analytics is designed for analysis, rather than retrieving raw data.)</span></span>

## <a name="diagrams"></a><span data-ttu-id="8ab71-177">Diagrammes</span><span class="sxs-lookup"><span data-stu-id="8ab71-177">Diagrams</span></span>
<span data-ttu-id="8ab71-178">Sélectionnez le type hello du diagramme que vous souhaitez :</span><span class="sxs-lookup"><span data-stu-id="8ab71-178">Select hello type of diagram you'd like:</span></span>

![Sélectionnez un type de diagramme](./media/app-insights-analytics-using/230.png)

<span data-ttu-id="8ab71-180">Si vous avez plusieurs colonnes de types de droite hello, vous pouvez choisir hello x et y axes et une colonne de résultats de hello toosplit dimensions par.</span><span class="sxs-lookup"><span data-stu-id="8ab71-180">If you have several columns of hello right types, you can choose hello x and y axes, and a column of dimensions toosplit hello results by.</span></span>

<span data-ttu-id="8ab71-181">Par défaut, les résultats sont initialement affichés sous forme de table, et sélectionne diagramme de hello.</span><span class="sxs-lookup"><span data-stu-id="8ab71-181">By default, results are initially displayed as a table, and you select hello diagram manually.</span></span> <span data-ttu-id="8ab71-182">Mais vous pouvez utiliser hello [restituer la directive](https://docs.loganalytics.io/queryLanguage/query_language_renderoperator.html) à fin hello d’une requête de tooselect un diagramme.</span><span class="sxs-lookup"><span data-stu-id="8ab71-182">But you can use hello [render directive](https://docs.loganalytics.io/queryLanguage/query_language_renderoperator.html) at hello end of a query tooselect a diagram.</span></span>

### <a name="analytics-diagnostics"></a><span data-ttu-id="8ab71-183">Diagnostic analytique</span><span class="sxs-lookup"><span data-stu-id="8ab71-183">Analytics diagnostics</span></span>


<span data-ttu-id="8ab71-184">Sur un timechart, s’il existe un pic soudain ou une étape dans vos données, vous pouvez voir un point de mise en surbrillance sur la ligne de hello.</span><span class="sxs-lookup"><span data-stu-id="8ab71-184">On a timechart, if there is a sudden spike or step in your data, you may see a highlighted point on hello line.</span></span> <span data-ttu-id="8ab71-185">Cela indique que les Diagnostics Analytique a identifié une combinaison des propriétés qui filtrent les modifications soudaines hello.</span><span class="sxs-lookup"><span data-stu-id="8ab71-185">This indicates that Analytics Diagnostics has identified a combination of properties that filter out hello sudden change.</span></span> <span data-ttu-id="8ab71-186">Cliquez sur hello point tooget plus de détails sur le filtrage de hello et version filtrée de toosee hello.</span><span class="sxs-lookup"><span data-stu-id="8ab71-186">Click hello point tooget more detail on hello filter, and toosee hello filtered version.</span></span> <span data-ttu-id="8ab71-187">Cela peut vous aider à identifier le changement de hello dû.</span><span class="sxs-lookup"><span data-stu-id="8ab71-187">This may help you identify what caused hello change.</span></span> 

[<span data-ttu-id="8ab71-188">En savoir plus sur le diagnostic analytique</span><span class="sxs-lookup"><span data-stu-id="8ab71-188">Learn more about Analytics Diagnostics</span></span>](app-insights-analytics-diagnostics.md)


![Diagnostic analytique](./media/app-insights-analytics-using/analytics-diagnostics.png)

## <a name="pin-toodashboard"></a><span data-ttu-id="8ab71-190">Code confidentiel toodashboard</span><span class="sxs-lookup"><span data-stu-id="8ab71-190">Pin toodashboard</span></span>
<span data-ttu-id="8ab71-191">Vous pouvez épingler un tooone de schéma ou une table de votre [partagé des tableaux de bord](app-insights-dashboards.md) -cliquez simplement le code confidentiel de hello.</span><span class="sxs-lookup"><span data-stu-id="8ab71-191">You can pin a diagram or table tooone of your [shared dashboards](app-insights-dashboards.md) - just click hello pin.</span></span> <span data-ttu-id="8ab71-192">(Vous devrez peut-être trop[mise d’à niveau votre application de tarification du package](app-insights-pricing.md) tooturn sur cette fonctionnalité.)</span><span class="sxs-lookup"><span data-stu-id="8ab71-192">(You might need too[upgrade your app's pricing package](app-insights-pricing.md) tooturn on this feature.)</span></span> 

![Cliquez sur le code confidentiel de hello](./media/app-insights-analytics-using/pin-01.png)

<span data-ttu-id="8ab71-194">Cela signifie que, lorsque vous placez ensemble un toohelp de tableau de bord que vous surveillez les performances hello ou l’utilisation de vos services web, vous pouvez inclure une analyse complexe en même temps que hello autres métriques.</span><span class="sxs-lookup"><span data-stu-id="8ab71-194">This means that, when you put together a dashboard toohelp you monitor hello performance or usage of your web services, you can include quite complex analysis alongside hello other metrics.</span></span> 

<span data-ttu-id="8ab71-195">Vous pouvez épingler un tableau de bord toohello de table, si elle a moins de quatre colonnes.</span><span class="sxs-lookup"><span data-stu-id="8ab71-195">You can pin a table toohello dashboard, if it has four or fewer columns.</span></span> <span data-ttu-id="8ab71-196">Uniquement hello sept premières lignes sont affichés.</span><span class="sxs-lookup"><span data-stu-id="8ab71-196">Only hello top seven rows are displayed.</span></span>

### <a name="dashboard-refresh"></a><span data-ttu-id="8ab71-197">Actualisation du tableau de bord</span><span class="sxs-lookup"><span data-stu-id="8ab71-197">Dashboard refresh</span></span>
<span data-ttu-id="8ab71-198">tableau de bord toohello Hello graphique épinglé est actualisé automatiquement par la nouvelle exécution de requête de hello environ toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="8ab71-198">hello chart pinned toohello dashboard is refreshed automatically by re-running hello query approximately every hours.</span></span> <span data-ttu-id="8ab71-199">Vous pouvez également cliquer sur le bouton d’actualisation hello.</span><span class="sxs-lookup"><span data-stu-id="8ab71-199">You can also click hello Refresh button.</span></span>

### <a name="automatic-simplifications"></a><span data-ttu-id="8ab71-200">Simplifications automatiques</span><span class="sxs-lookup"><span data-stu-id="8ab71-200">Automatic simplifications</span></span>

<span data-ttu-id="8ab71-201">Certaines simplifications sont appliqués tooa graphique quand vous l’épinglez tooa le tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="8ab71-201">Certain simplifications are applied tooa chart when you pin it tooa dashboard.</span></span>

<span data-ttu-id="8ab71-202">**Restriction de temps :** requêtes sont automatiquement limité toohello cours des 14 derniers jours.</span><span class="sxs-lookup"><span data-stu-id="8ab71-202">**Time restriction:** Queries are automatically limited toohello past 14 days.</span></span> <span data-ttu-id="8ab71-203">Hello effet est hello identique comme si votre requête inclut `where timestamp > ago(14d)`.</span><span class="sxs-lookup"><span data-stu-id="8ab71-203">hello effect is hello same as if your query includes `where timestamp > ago(14d)`.</span></span>

<span data-ttu-id="8ab71-204">**Restriction relative au nombre de compartimenter :** si vous affichez un graphique qui possède un grand nombre d’emplacements discrets (en général, un graphique à barres), hello moins remplis emplacements sont automatiquement regroupés en un seul « d’autres » bin.</span><span class="sxs-lookup"><span data-stu-id="8ab71-204">**Bin count restriction:** If you display a chart that has a lot of discrete bins (typically a bar chart), hello less populated bins are automatically grouped into a single "others" bin.</span></span> <span data-ttu-id="8ab71-205">Par exemple, cette requête :</span><span class="sxs-lookup"><span data-stu-id="8ab71-205">For example, this query:</span></span>

    requests | summarize count_search = count() by client_CountryOrRegion

<span data-ttu-id="8ab71-206">se présente sous la forme suivante dans Analytics :</span><span class="sxs-lookup"><span data-stu-id="8ab71-206">looks like this in Analytics:</span></span>

![Graphique à longue traîne](./media/app-insights-analytics-using/pin-07.png)

<span data-ttu-id="8ab71-208">mais lorsque vous l’épinglez tooa le tableau de bord, il ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="8ab71-208">but when you pin it tooa dashboard, it looks like this:</span></span>

![Graphique comportant des emplacements limités](./media/app-insights-analytics-using/pin-08.png)

## <a name="export-tooexcel"></a><span data-ttu-id="8ab71-210">Exportation tooExcel</span><span class="sxs-lookup"><span data-stu-id="8ab71-210">Export tooExcel</span></span>
<span data-ttu-id="8ab71-211">Une fois votre requête exécutée, vous pouvez télécharger un fichier .csv.</span><span class="sxs-lookup"><span data-stu-id="8ab71-211">After you've run a query, you can download a .csv file.</span></span> <span data-ttu-id="8ab71-212">Cliquez sur **Exporter, Excel**.</span><span class="sxs-lookup"><span data-stu-id="8ab71-212">Click **Export,  Excel**.</span></span>

## <a name="export-toopower-bi"></a><span data-ttu-id="8ab71-213">Exportation tooPower BI</span><span class="sxs-lookup"><span data-stu-id="8ab71-213">Export tooPower BI</span></span>
<span data-ttu-id="8ab71-214">Placez le curseur à hello dans une requête et choisissez **exporter, Power BI**.</span><span class="sxs-lookup"><span data-stu-id="8ab71-214">Put hello cursor in a query and choose **Export, Power BI**.</span></span>

![Exporter à partir de l’Analytique tooPower BI](./media/app-insights-analytics-using/240.png)

<span data-ttu-id="8ab71-216">Exécution de requête de hello dans Power BI.</span><span class="sxs-lookup"><span data-stu-id="8ab71-216">You run hello query in Power BI.</span></span> <span data-ttu-id="8ab71-217">Vous pouvez définir toorefresh selon une planification.</span><span class="sxs-lookup"><span data-stu-id="8ab71-217">You can set it toorefresh on a schedule.</span></span>

<span data-ttu-id="8ab71-218">Avec Power BI, vous pouvez créer des tableaux de bord qui rassemblent les données issues d’un large éventail de sources.</span><span class="sxs-lookup"><span data-stu-id="8ab71-218">With Power BI, you can create dashboards that bring together data from a wide variety of sources.</span></span>

[<span data-ttu-id="8ab71-219">En savoir plus sur l’exportation tooPower BI</span><span class="sxs-lookup"><span data-stu-id="8ab71-219">Learn more about export tooPower BI</span></span>](app-insights-export-power-bi.md)

## <a name="deep-link"></a><span data-ttu-id="8ab71-220">Lien ciblé</span><span class="sxs-lookup"><span data-stu-id="8ab71-220">Deep link</span></span>

<span data-ttu-id="8ab71-221">Obtenez un lien sous **exportation, liaison de partage** que vous pouvez envoyer tooanother utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8ab71-221">Get a link under **Export, Share link** that you can send tooanother user.</span></span> <span data-ttu-id="8ab71-222">Condition hello utilisateur a [groupe de ressources accès tooyour](app-insights-resources-roles-access-control.md), requête de hello s’ouvre dans hello l’interface utilisateur de l’Analytique.</span><span class="sxs-lookup"><span data-stu-id="8ab71-222">Provided hello user has [access tooyour resource group](app-insights-resources-roles-access-control.md), hello query will open in hello Analytics UI.</span></span>

<span data-ttu-id="8ab71-223">(Dans le lien de hello, le texte de requête hello apparaît après « ? q = », compressés gzip et codé en base 64.</span><span class="sxs-lookup"><span data-stu-id="8ab71-223">(In hello link, hello query text appears after "?q=", gzip compressed and base-64 encoded.</span></span> <span data-ttu-id="8ab71-224">Vous pouvez écrire des liens profonds toogenerate de code que vous fournissez toousers.</span><span class="sxs-lookup"><span data-stu-id="8ab71-224">You could write code toogenerate deep links that you provide toousers.</span></span> <span data-ttu-id="8ab71-225">Toutefois, hello recommandé est de façon toorun Analytique à partir du code à l’aide de hello [API REST](https://dev.applicationinsights.io/).)</span><span class="sxs-lookup"><span data-stu-id="8ab71-225">However, hello recommended way toorun Analytics from code is by using hello [REST API](https://dev.applicationinsights.io/).)</span></span>


## <a name="automation"></a><span data-ttu-id="8ab71-226">Automatisation</span><span class="sxs-lookup"><span data-stu-id="8ab71-226">Automation</span></span>

<span data-ttu-id="8ab71-227">Hello d’utilisation [données accès REST API](https://dev.applicationinsights.io/) toorun des requêtes Analytique.</span><span class="sxs-lookup"><span data-stu-id="8ab71-227">Use hello  [Data Access REST API](https://dev.applicationinsights.io/) toorun Analytics queries.</span></span> <span data-ttu-id="8ab71-228">[Par exemple](https://dev.applicationinsights.io/apiexplorer/query?appId=DEMO_APP&apiKey=DEMO_KEY&query=requests%0A%7C%20where%20timestamp%20%3E%3D%20ago%2824h%29%0A%7C%20count) (à l’aide de PowerShell) :</span><span class="sxs-lookup"><span data-stu-id="8ab71-228">[For example](https://dev.applicationinsights.io/apiexplorer/query?appId=DEMO_APP&apiKey=DEMO_KEY&query=requests%0A%7C%20where%20timestamp%20%3E%3D%20ago%2824h%29%0A%7C%20count) (using PowerShell):</span></span>

```PS
curl "https://api.applicationinsights.io/beta/apps/DEMO_APP/query?query=requests%7C%20where%20timestamp%20%3E%3D%20ago(24h)%7C%20count" -H "x-api-key: DEMO_KEY"
```

<span data-ttu-id="8ab71-229">Contrairement à l’interface utilisateur de l’Analytique de hello, hello API REST n’ajoute pas automatiquement les requêtes tooyour de limitation timestamp.</span><span class="sxs-lookup"><span data-stu-id="8ab71-229">Unlike hello Analytics UI, hello REST API does not automatically add any timestamp limitation tooyour queries.</span></span> <span data-ttu-id="8ab71-230">N’oubliez pas de tooadd votre propre clause where, tooavoid obtenir des réponses énormes.</span><span class="sxs-lookup"><span data-stu-id="8ab71-230">Remember tooadd your own where-clause, tooavoid getting huge responses.</span></span>



## <a name="import-data"></a><span data-ttu-id="8ab71-231">Importer des données</span><span class="sxs-lookup"><span data-stu-id="8ab71-231">Import data</span></span>

<span data-ttu-id="8ab71-232">Vous pouvez importer des données à partir d’un fichier CSV.</span><span class="sxs-lookup"><span data-stu-id="8ab71-232">You can import data from a CSV file.</span></span> <span data-ttu-id="8ab71-233">Une utilisation classique est tooimport les données statiques que vous pouvez joindre des tables à partir de votre télémétrie.</span><span class="sxs-lookup"><span data-stu-id="8ab71-233">A typical usage is tooimport static data that you can join with tables from your telemetry.</span></span> 

<span data-ttu-id="8ab71-234">Par exemple, si les utilisateurs authentifiés sont identifiées dans vos données de télémétrie à un id obscurci ou un alias, vous pouvez importer une table qui mappe les noms d’alias tooreal.</span><span class="sxs-lookup"><span data-stu-id="8ab71-234">For example, if authenticated users are identified in your telemetry by an alias or obfuscated id, you could import a table that maps aliases tooreal names.</span></span> <span data-ttu-id="8ab71-235">En effectuant une jointure sur la télémétrie des requêtes hello, vous pouvez identifier les utilisateurs par leur nom réel dans les rapports d’Analytique hello.</span><span class="sxs-lookup"><span data-stu-id="8ab71-235">By performing a join on hello request telemetry, you can identify users by their real names in hello Analytics reports.</span></span>

### <a name="define-your-data-schema"></a><span data-ttu-id="8ab71-236">Définir votre schéma de données</span><span class="sxs-lookup"><span data-stu-id="8ab71-236">Define your data schema</span></span>

1. <span data-ttu-id="8ab71-237">Cliquez sur **Paramètres** (en haut à gauche), puis sur **Sources de données**.</span><span class="sxs-lookup"><span data-stu-id="8ab71-237">Click **Settings** (at top left) and then **Data Sources**.</span></span> 
2. <span data-ttu-id="8ab71-238">Ajouter une source de données, en suivant les instructions hello.</span><span class="sxs-lookup"><span data-stu-id="8ab71-238">Add a data source, following hello instructions.</span></span> <span data-ttu-id="8ab71-239">Vous êtes invité à toosupply un échantillon de données hello, qui doivent inclure au moins dix lignes.</span><span class="sxs-lookup"><span data-stu-id="8ab71-239">You are asked toosupply a sample of hello data, which should include at least ten rows.</span></span> <span data-ttu-id="8ab71-240">Vous corrigez ensuite le schéma de hello.</span><span class="sxs-lookup"><span data-stu-id="8ab71-240">You then correct hello schema.</span></span>

<span data-ttu-id="8ab71-241">Définit une source de données, vous pouvez ensuite utiliser tooimport des tables individuelles.</span><span class="sxs-lookup"><span data-stu-id="8ab71-241">This defines a data source, which you can then use tooimport individual tables.</span></span>

### <a name="import-a-table"></a><span data-ttu-id="8ab71-242">Importer une table</span><span class="sxs-lookup"><span data-stu-id="8ab71-242">Import a table</span></span>

1. <span data-ttu-id="8ab71-243">Ouvrez votre définition de source de données à partir de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="8ab71-243">Open your data source definition from hello list.</span></span>
2. <span data-ttu-id="8ab71-244">Cliquez sur « Télécharger » et suivre la table de hello instructions tooupload hello.</span><span class="sxs-lookup"><span data-stu-id="8ab71-244">Click "Upload" and follow hello instructions tooupload hello table.</span></span> <span data-ttu-id="8ab71-245">Cela implique un tooa appel API REST, et il est donc facile tooautomate.</span><span class="sxs-lookup"><span data-stu-id="8ab71-245">This involves a call tooa REST API, and so it is easy tooautomate.</span></span> 

<span data-ttu-id="8ab71-246">Votre table est désormais disponible pour une utilisation dans des requêtes Analytics.</span><span class="sxs-lookup"><span data-stu-id="8ab71-246">Your table is now available for use in Analytics queries.</span></span> <span data-ttu-id="8ab71-247">Elle apparaîtra dans Analytics</span><span class="sxs-lookup"><span data-stu-id="8ab71-247">It will appear in Analytics</span></span> 

### <a name="use-hello-table"></a><span data-ttu-id="8ab71-248">Utilisez la table de hello</span><span class="sxs-lookup"><span data-stu-id="8ab71-248">Use hello table</span></span>

<span data-ttu-id="8ab71-249">Supposons que votre définition de source de données s'appelle `usermap` et comporte deux champs, `realName` et `user_AuthenticatedId`.</span><span class="sxs-lookup"><span data-stu-id="8ab71-249">Let's suppose your data source definition is called `usermap`, and that it has two fields, `realName` and `user_AuthenticatedId`.</span></span> <span data-ttu-id="8ab71-250">Hello `requests` table possède également un champ nommé `user_AuthenticatedId`, par conséquent, il est facile toojoin les :</span><span class="sxs-lookup"><span data-stu-id="8ab71-250">hello `requests` table also has a field named `user_AuthenticatedId`, so it's easy toojoin them:</span></span>

```AIQL

    requests
    | where notempty(user_AuthenticatedId) | take 10
    | join kind=leftouter ( usermap ) on user_AuthenticatedId 
```
<span data-ttu-id="8ab71-251">la table résultante de demandes Hello a une colonne supplémentaire, `realName`.</span><span class="sxs-lookup"><span data-stu-id="8ab71-251">hello resulting table of requests has an additional column, `realName`.</span></span>

### <a name="import-from-logstash"></a><span data-ttu-id="8ab71-252">Importer à partir de LogStash</span><span class="sxs-lookup"><span data-stu-id="8ab71-252">Import from LogStash</span></span>

<span data-ttu-id="8ab71-253">Si vous utilisez [LogStash](https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html), vous pouvez utiliser Analytique tooquery vos journaux.</span><span class="sxs-lookup"><span data-stu-id="8ab71-253">If you use [LogStash](https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html), you can use Analytics tooquery your logs.</span></span> <span data-ttu-id="8ab71-254">Hello d’utilisation [plug-in qui envoie des données dans Analytique](https://github.com/Microsoft/logstash-output-application-insights).</span><span class="sxs-lookup"><span data-stu-id="8ab71-254">Use hello [plugin that pipes data into Analytics](https://github.com/Microsoft/logstash-output-application-insights).</span></span> 

## <a name="video"></a><span data-ttu-id="8ab71-255">Vidéo</span><span class="sxs-lookup"><span data-stu-id="8ab71-255">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

