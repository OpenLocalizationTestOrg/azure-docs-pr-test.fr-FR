---
title: "Visite guidée d’Analytics dans Azure Application Insights | Microsoft Docs"
description: "Courts exemples de toutes les requêtes principales dans Analytics, outil de recherche puissant d’Application Insights."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: bddf4a6d-ea8d-4607-8531-1fe197cc57ad
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/06/2017
ms.author: bwren
ms.openlocfilehash: f5650d212eb2f8c460f062b3c11ae14c1e026ba6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="a-tour-of-analytics-in-application-insights"></a><span data-ttu-id="8d3ef-103">Visite guidée d’Analytics dans Application Insights</span><span class="sxs-lookup"><span data-stu-id="8d3ef-103">A tour of Analytics in Application Insights</span></span>
<span data-ttu-id="8d3ef-104">[Analytics](app-insights-analytics.md) est la fonctionnalité de recherche performante [d’Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8d3ef-104">[Analytics](app-insights-analytics.md) is the powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="8d3ef-105">Ces pages décrivent le langage de requête Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-105">These pages describe the Log Analytics query language.</span></span>

* <span data-ttu-id="8d3ef-106">**[Regardez la vidéo d’introduction](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-106">**[Watch the introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="8d3ef-107">**[Testez la version d’évaluation d’Analytics sur nos données simulées](https://analytics.applicationinsights.io/demo)** si votre application n’envoie pas encore de données à Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data to Application Insights yet.</span></span>
* <span data-ttu-id="8d3ef-108">**[L’aide-mémoire des utilisateurs de SQL](https://aka.ms/sql-analytics)** traduit les idiomes courants.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-108">**[SQL-users' cheat sheet](https://aka.ms/sql-analytics)** translates the most common idioms.</span></span>

<span data-ttu-id="8d3ef-109">Pour vous aider à démarrer, examinons certaines requêtes de base.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-109">Let's take a walk through some basic queries to get you started.</span></span>

## <a name="connect-to-your-application-insights-data"></a><span data-ttu-id="8d3ef-110">Connectez-vous à vos données Application Insights</span><span class="sxs-lookup"><span data-stu-id="8d3ef-110">Connect to your Application Insights data</span></span>
<span data-ttu-id="8d3ef-111">Ouvrez Analytics à partir du [panneau Vue d’ensemble](app-insights-dashboards.md) de votre application dans Application Insights :</span><span class="sxs-lookup"><span data-stu-id="8d3ef-111">Open Analytics from your app's [overview blade](app-insights-dashboards.md) in Application Insights:</span></span>

![Ouvrez portal.azure.com, ouvrez votre ressource Application Insights, puis cliquez sur Analyse.](./media/app-insights-analytics-tour/001.png)

## <a name="takehttpsdocsloganalyticsioquerylanguagequerylanguagetakeoperatorhtml-show-me-n-rows"></a><span data-ttu-id="8d3ef-113">[Take](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html): afficher n lignes</span><span class="sxs-lookup"><span data-stu-id="8d3ef-113">[Take](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html): show me n rows</span></span>
<span data-ttu-id="8d3ef-114">Les points de données qui consignent les opérations des utilisateurs (généralement des requêtes HTTP reçues par votre application web) sont stockés dans une table appelée `requests`.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-114">Data points that log user operations (typically HTTP requests received by your web app) are stored in a table called `requests`.</span></span> <span data-ttu-id="8d3ef-115">Chaque ligne est un point de données de télémétrie provenant du Kit de développement logiciel (SDK) Application Insights dans votre application.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-115">Each row is a telemetry data point received from the Application Insights SDK in your app.</span></span>

<span data-ttu-id="8d3ef-116">Commençons par examiner quelques exemples de lignes de la table :</span><span class="sxs-lookup"><span data-stu-id="8d3ef-116">Let's start by examining a few sample rows of the table:</span></span>

![results](./media/app-insights-analytics-tour/010.png)

> [!NOTE]
> <span data-ttu-id="8d3ef-118">Placez le curseur quelque part dans l’instruction avant de cliquer sur OK.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-118">Put the cursor somewhere in the statement before you click Go.</span></span> <span data-ttu-id="8d3ef-119">Vous pouvez répartir une instruction sur plusieurs lignes, mais ne placez pas de lignes vides dans une instruction.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-119">You can split a statement over more than one line, but don't put blank lines in a statement.</span></span> <span data-ttu-id="8d3ef-120">Pour conserver plusieurs requêtes dans la fenêtre, séparez-les par des lignes vides.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-120">Blank lines are a convenient way to keep several separate queries in the window.</span></span>
>
>

<span data-ttu-id="8d3ef-121">Choisissez les colonnes, faites-les glisser, groupez-les par colonnes et filtrez :</span><span class="sxs-lookup"><span data-stu-id="8d3ef-121">Choose columns, drag them, group by columns, and filter:</span></span>

![Cliquez sur le sélecteur de colonnes en haut à droite des résultats](./media/app-insights-analytics-tour/030.png)

<span data-ttu-id="8d3ef-123">Développez un élément pour afficher les détails :</span><span class="sxs-lookup"><span data-stu-id="8d3ef-123">Expand any item to see the detail:</span></span>

![Choisissez la vue de table et utilisez Configurer les colonnes](./media/app-insights-analytics-tour/040.png)

> [!NOTE]
> <span data-ttu-id="8d3ef-125">Cliquez sur l’en-tête d’une colonne pour trier à nouveau les résultats disponibles dans le navigateur web.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-125">Click the head of a column to re-order the results available in the web browser.</span></span> <span data-ttu-id="8d3ef-126">Sachez toutefois que, pour un jeu de résultats volumineux, le système limite le nombre de lignes téléchargées vers le navigateur.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-126">But be aware that for a large result set, the number of rows downloaded to the browser is limited.</span></span> <span data-ttu-id="8d3ef-127">L’utilisation de cette méthode de tri ne vous permet pas toujours d’obtenir effectivement les éléments dans l’ordre croissant ou décroissant.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-127">Sorting this way doesn't always show you the actual highest or lowest items.</span></span> <span data-ttu-id="8d3ef-128">Pour trier les éléments de manière fiable, utilisez l’opérateur `top` ou `sort`.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-128">To sort items reliably, use the `top` or `sort` operator.</span></span>
>
>

## <a name="tophttpsdocsloganalyticsioquerylanguagequerylanguagetopoperatorhtml-and-sorthttpsdocsloganalyticsioquerylanguagequerylanguagesortoperatorhtml"></a><span data-ttu-id="8d3ef-129">[Top](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) et [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html)</span><span class="sxs-lookup"><span data-stu-id="8d3ef-129">[Top](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) and [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html)</span></span>
<span data-ttu-id="8d3ef-130">`take` est utile pour obtenir un exemple rapide d’un résultat, mais il n’affiche pas les lignes de la table dans un ordre particulier.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-130">`take` is useful to get a quick sample of a result, but it shows rows from the table in no particular order.</span></span> <span data-ttu-id="8d3ef-131">Pour obtenir un affichage ordonné, utilisez `top` (pour un échantillon) ou `sort` (qui porte sur la table entière).</span><span class="sxs-lookup"><span data-stu-id="8d3ef-131">To get an ordered view, use `top` (for a sample) or `sort` (over the whole table).</span></span>

<span data-ttu-id="8d3ef-132">Afficher les n premières lignes, classées par une colonne particulière :</span><span class="sxs-lookup"><span data-stu-id="8d3ef-132">Show me the first n rows, ordered by a particular column:</span></span>

```AIQL

    requests | top 10 by timestamp desc
```

* <span data-ttu-id="8d3ef-133">*Syntaxe :* la plupart des opérateurs ont des paramètres de mot clé comme `by`.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-133">*Syntax:* Most operators have keyword parameters such as `by`.</span></span>
* <span data-ttu-id="8d3ef-134">`desc` = ordre décroissant, `asc` = ordre croissant.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-134">`desc` = descending order, `asc` = ascending.</span></span>

![](./media/app-insights-analytics-tour/260.png)

<span data-ttu-id="8d3ef-135">`top...` est une manière plus performante d’exprimer `sort ... | take...`.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-135">`top...` is a more performant way of saying `sort ... | take...`.</span></span> <span data-ttu-id="8d3ef-136">Nous aurions pu écrire :</span><span class="sxs-lookup"><span data-stu-id="8d3ef-136">We could have written:</span></span>

```AIQL

    requests | sort by timestamp desc | take 10
```

<span data-ttu-id="8d3ef-137">Le résultat serait le même, mais l’exécution de la requête serait un peu plus lente.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-137">The result would be the same, but it would run a bit more slowly.</span></span> <span data-ttu-id="8d3ef-138">(Vous pouvez également écrire `order`, qui est un alias de `sort`.)</span><span class="sxs-lookup"><span data-stu-id="8d3ef-138">(You could also write `order`, which is an alias of `sort`.)</span></span>

<span data-ttu-id="8d3ef-139">Les en-têtes de colonne dans la vue de table peuvent également servir à trier les résultats sur l’écran.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-139">The column headers in the table view can also be used to sort the results on the screen.</span></span> <span data-ttu-id="8d3ef-140">Mais, bien sûr, si vous avez utilisé `take` ou `top` pour récupérer une partie seulement d’une table, vous devez uniquement trier de nouveau les enregistrements que vous avez récupérés.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-140">But of course, if you've used `take` or `top` to retrieve just part of a table, you'll only re-order the records you've retrieved.</span></span>

## <a name="wherehttpsdocsloganalyticsioquerylanguagequerylanguagewhereoperatorhtml-filtering-on-a-condition"></a><span data-ttu-id="8d3ef-141">[Where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html): filtrage sur une condition</span><span class="sxs-lookup"><span data-stu-id="8d3ef-141">[Where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html): filtering on a condition</span></span>

<span data-ttu-id="8d3ef-142">Concentrons-nous sur les requêtes qui ont renvoyé un code de résultat particulier :</span><span class="sxs-lookup"><span data-stu-id="8d3ef-142">Let's see just requests that returned a particular result code:</span></span>

```AIQL

    requests
    | where resultCode  == "404"
    | take 10
```

![](./media/app-insights-analytics-tour/250.png)

<span data-ttu-id="8d3ef-143">L’opérateur `where` utilise une expression booléenne.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-143">The `where` operator takes a Boolean expression.</span></span> <span data-ttu-id="8d3ef-144">Voici quelques points clés les concernant :</span><span class="sxs-lookup"><span data-stu-id="8d3ef-144">Here are some key points about them:</span></span>

* <span data-ttu-id="8d3ef-145">`and`, `or` : opérateurs booléens</span><span class="sxs-lookup"><span data-stu-id="8d3ef-145">`and`, `or`: Boolean operators</span></span>
* <span data-ttu-id="8d3ef-146">`==`, `<>`, `!=` : égal à et différent de</span><span class="sxs-lookup"><span data-stu-id="8d3ef-146">`==`, `<>`, `!=` : equal and not equal</span></span>
* <span data-ttu-id="8d3ef-147">`=~`, `!~` : chaîne ne respectant pas la casse (égal à et différent de).</span><span class="sxs-lookup"><span data-stu-id="8d3ef-147">`=~`, `!~` : case-insensitive string equal and not equal.</span></span> <span data-ttu-id="8d3ef-148">Il existe de nombreux autres opérateurs de comparaison de chaîne.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-148">There are lots more string comparison operators.</span></span>

<!---Read all about [scalar expressions]().--->

### <a name="getting-the-right-type"></a><span data-ttu-id="8d3ef-149">Trouver le bon type</span><span class="sxs-lookup"><span data-stu-id="8d3ef-149">Getting the right type</span></span>
<span data-ttu-id="8d3ef-150">Rechercher les requêtes ayant échoué :</span><span class="sxs-lookup"><span data-stu-id="8d3ef-150">Find unsuccessful requests:</span></span>

```AIQL

    requests
    | where isnotempty(resultCode) and toint(resultCode) >= 400
```
<!---
`resultCode` has type string, so we must cast it app-insights-analytics-reference.md#casts for a numeric comparison.
--->

## <a name="time"></a><span data-ttu-id="8d3ef-151">Time</span><span class="sxs-lookup"><span data-stu-id="8d3ef-151">Time</span></span>

<span data-ttu-id="8d3ef-152">Par défaut, vos requêtes sont limitées aux dernières 24 heures.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-152">By default, your queries are restricted to the last 24 hours.</span></span> <span data-ttu-id="8d3ef-153">Mais vous pouvez modifier cette plage :</span><span class="sxs-lookup"><span data-stu-id="8d3ef-153">But you can change this range:</span></span>

![](./media/app-insights-analytics-tour/change-time-range.png)

<span data-ttu-id="8d3ef-154">Remplacez l’intervalle de temps en écrivant une requête qui mentionne `timestamp` dans une clause where.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-154">Override the time range by writing any query that mentions `timestamp` in a where-clause.</span></span> <span data-ttu-id="8d3ef-155">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="8d3ef-155">For example:</span></span>

```AIQL

    // What were the slowest requests over the past 3 days?
    requests
    | where timestamp > ago(3d)  // Override the time range
    | top 5 by duration
```

<span data-ttu-id="8d3ef-156">La fonctionnalité d’intervalle de temps est équivalente à une clause « where » insérée après chaque mention d’une des tables sources.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-156">The time range feature is equivalent to a 'where' clause inserted after each mention of one of the source tables.</span></span>

<span data-ttu-id="8d3ef-157">`ago(3d)` signifie « il y a trois jours ».</span><span class="sxs-lookup"><span data-stu-id="8d3ef-157">`ago(3d)` means 'three days ago'.</span></span> <span data-ttu-id="8d3ef-158">Il existe d’autres unités de temps, par exemple les heures (`2h`, `2.5h`), les minutes (`25m`) et les secondes (`10s`).</span><span class="sxs-lookup"><span data-stu-id="8d3ef-158">Other units of time include hours (`2h`, `2.5h`), minutes (`25m`), and seconds (`10s`).</span></span>

<span data-ttu-id="8d3ef-159">Autres exemples :</span><span class="sxs-lookup"><span data-stu-id="8d3ef-159">Other examples:</span></span>

```AIQL

    // Last calendar week:
    requests
    | where timestamp > startofweek(now()-7d)
        and timestamp < startofweek(now())
    | top 5 by duration

    // First hour of every day in past seven days:
    requests
    | where timestamp > ago(7d) and timestamp % 1d < 1h
    | top 5 by duration

    // Specific dates:
    requests
    | where timestamp > datetime(2016-11-19) and timestamp < datetime(2016-11-21)
    | top 5 by duration

```

<span data-ttu-id="8d3ef-160">[Référence sur les dates et les heures](https://docs.loganalytics.io/concepts/concepts_datatypes_datetime.html).</span><span class="sxs-lookup"><span data-stu-id="8d3ef-160">[Dates and times reference](https://docs.loganalytics.io/concepts/concepts_datatypes_datetime.html).</span></span>


## <a name="projecthttpsdocsloganalyticsioquerylanguagequerylanguageprojectoperatorhtml-select-rename-and-compute-columns"></a><span data-ttu-id="8d3ef-161">[Projet](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) : sélectionnez, renommez et calculez des colonnes</span><span class="sxs-lookup"><span data-stu-id="8d3ef-161">[Project](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html): select, rename, and compute columns</span></span>
<span data-ttu-id="8d3ef-162">Utilisez [`project`](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) pour choisir uniquement les colonnes qui vous intéressent :</span><span class="sxs-lookup"><span data-stu-id="8d3ef-162">Use [`project`](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) to pick out just the columns you want:</span></span>

```AIQL

    requests | top 10 by timestamp desc
             | project timestamp, name, resultCode
```

![](./media/app-insights-analytics-tour/240.png)

<span data-ttu-id="8d3ef-163">Vous pouvez également renommer des colonnes et en définir de nouvelles :</span><span class="sxs-lookup"><span data-stu-id="8d3ef-163">You can also rename columns and define new ones:</span></span>

```AIQL

    requests
    | top 10 by timestamp desc
    | project  
            name,
            response = resultCode,
            timestamp,
            ['time of day'] = floor(timestamp % 1d, 1s)
```

![result](./media/app-insights-analytics-tour/270.png)

* <span data-ttu-id="8d3ef-165">Les noms de colonnes peuvent contenir des espaces ou des symboles s’ils sont placés entre crochets comme suit : `['...']` ou `["..."]`</span><span class="sxs-lookup"><span data-stu-id="8d3ef-165">Column names can include spaces or symbols if they are bracketed like this: `['...']` or `["..."]`</span></span>
* <span data-ttu-id="8d3ef-166">`%` est l’opérateur modulo habituel.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-166">`%` is the usual modulo operator.</span></span>
* <span data-ttu-id="8d3ef-167">`1d` (le chiffre un, suivi de la lettre d) est un littéral d’intervalle de temps qui signifie un jour.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-167">`1d` (that's a digit one, then a 'd') is a timespan literal meaning one day.</span></span> <span data-ttu-id="8d3ef-168">Voici d’autres littéraux d’intervalle de temps : `12h`, `30m`, `10s`, `0.01s`.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-168">Here are some more timespan literals: `12h`, `30m`, `10s`, `0.01s`.</span></span>
* <span data-ttu-id="8d3ef-169">`floor` (alias `bin`) arrondit une valeur au multiple inférieur le plus proche de la valeur de base que vous fournissez.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-169">`floor` (alias `bin`) rounds a value down to the nearest multiple of the base value you provide.</span></span> <span data-ttu-id="8d3ef-170">Ainsi, `floor(aTime, 1s)` arrondit une heure vers le bas à la seconde la plus proche.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-170">So `floor(aTime, 1s)` rounds a time down to the nearest second.</span></span>

<span data-ttu-id="8d3ef-171">Les expressions peuvent inclure tous les opérateurs habituels (`+`, `-`, etc.), et il existe une gamme de fonctions utiles.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-171">Expressions can include all the usual operators (`+`, `-`, ...), and there's a range of useful functions.</span></span>

## <a name="extend"></a><span data-ttu-id="8d3ef-172">Extend</span><span class="sxs-lookup"><span data-stu-id="8d3ef-172">Extend</span></span>
<span data-ttu-id="8d3ef-173">Si vous souhaitez simplement ajouter des colonnes à des colonnes existantes, utilisez [`extend`](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html):</span><span class="sxs-lookup"><span data-stu-id="8d3ef-173">If you just want to add columns to the existing ones, use [`extend`](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html):</span></span>

```AIQL

    requests
    | top 10 by timestamp desc
    | extend timeOfDay = floor(timestamp % 1d, 1s)
```

<span data-ttu-id="8d3ef-174">Utiliser [`extend`](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html) est plus concis que [`project`](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) si vous souhaitez conserver toutes les colonnes existantes.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-174">Using [`extend`](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html) is less verbose than [`project`](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) if you want to keep all the existing columns.</span></span>

### <a name="convert-to-local-time"></a><span data-ttu-id="8d3ef-175">Convertir en heure locale</span><span class="sxs-lookup"><span data-stu-id="8d3ef-175">Convert to local time</span></span>

<span data-ttu-id="8d3ef-176">Les timestamps sont toujours exprimés en UTC.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-176">Timestamps are always in UTC.</span></span> <span data-ttu-id="8d3ef-177">Par conséquent, si vous vous trouvez sur la côte Pacifique des États-Unis et que c’est l’hiver, ceci pourrait vous intéresser :</span><span class="sxs-lookup"><span data-stu-id="8d3ef-177">So if you're on the US Pacific coast and it's winter, you might like this:</span></span>

```AIQL

    requests
    | top 10 by timestamp desc
    | extend localTime = timestamp - 8h
```


## <a name="summarizehttpsdocsloganalyticsioquerylanguagequerylanguagesummarizeoperatorhtml-aggregate-groups-of-rows"></a><span data-ttu-id="8d3ef-178">[Summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html): agréger des groupes de lignes</span><span class="sxs-lookup"><span data-stu-id="8d3ef-178">[Summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html): aggregate groups of rows</span></span>
<span data-ttu-id="8d3ef-179">`Summarize` applique une *fonction d’agrégation* spécifiée sur des groupes de lignes.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-179">`Summarize` applies a specified *aggregation function* over groups of rows.</span></span>

<span data-ttu-id="8d3ef-180">Par exemple, le temps que met votre application web à répondre à une requête est reporté dans le champ `duration`.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-180">For example, the time your web app takes to respond to a request is reported in the field `duration`.</span></span> <span data-ttu-id="8d3ef-181">Observons le temps de réponse moyen pour toutes les demandes :</span><span class="sxs-lookup"><span data-stu-id="8d3ef-181">Let's see the average response time to all requests:</span></span>

![](./media/app-insights-analytics-tour/410.png)

<span data-ttu-id="8d3ef-182">Nous pouvons également séparer les résultats en requêtes de noms différents :</span><span class="sxs-lookup"><span data-stu-id="8d3ef-182">Or we could separate the result into requests of different names:</span></span>

![](./media/app-insights-analytics-tour/420.png)

<span data-ttu-id="8d3ef-183">`Summarize` regroupe les points de données du flux que la clause `by` évalue équitablement.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-183">`Summarize` collects the data points in the stream into groups for which the `by` clause evaluates equally.</span></span> <span data-ttu-id="8d3ef-184">Chaque valeur de l’expression `by` (chaque nom d’opération dans l’exemple ci-dessus) génère une ligne dans la table des résultats.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-184">Each value in the `by` expression - each operation name in the above example - results in a row in the result table.</span></span>

<span data-ttu-id="8d3ef-185">Nous pouvons également regrouper les résultats par heure :</span><span class="sxs-lookup"><span data-stu-id="8d3ef-185">Or we could group results by time of day:</span></span>

![](./media/app-insights-analytics-tour/430.png)

<span data-ttu-id="8d3ef-186">Notez que nous utilisons la fonction `bin` (également appelée `floor`).</span><span class="sxs-lookup"><span data-stu-id="8d3ef-186">Notice how we're using the `bin` function (aka `floor`).</span></span> <span data-ttu-id="8d3ef-187">Si nous avions simplement utilisé `by timestamp`, chaque ligne d’entrée apparaîtrait dans un groupe individuel.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-187">If we just used `by timestamp`, every input row would end up in its own little group.</span></span> <span data-ttu-id="8d3ef-188">Pour des valeurs scalaires continues telles que des heures ou des nombres, nous devons diviser la plage continue en un nombre gérable de valeurs discrètes.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-188">For any continuous scalar like times or numbers, we have to break the continuous range into a manageable number of discrete values.</span></span> <span data-ttu-id="8d3ef-189">`bin` (qui représente simplement la fonction `floor` habituelle d’arrondi à la valeur inférieure) est le plus simple moyen d’y parvenir.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-189">`bin` - which is just the familiar rounding-down `floor` function - is the easiest way to do that.</span></span>

<span data-ttu-id="8d3ef-190">Nous pouvons utiliser la même technique pour réduire les plages de chaînes :</span><span class="sxs-lookup"><span data-stu-id="8d3ef-190">We can use the same technique to reduce ranges of strings:</span></span>

![](./media/app-insights-analytics-tour/440.png)

<span data-ttu-id="8d3ef-191">Notez que vous pouvez utiliser `name=` pour définir le nom d’une colonne de résultat, dans les expressions d’agrégation ou dans la clause by.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-191">Notice that you can use `name=` to set the name of a result column, either in the aggregation expressions or the by-clause.</span></span>

## <a name="counting-sampled-data"></a><span data-ttu-id="8d3ef-192">Décompte des données échantillonnées</span><span class="sxs-lookup"><span data-stu-id="8d3ef-192">Counting sampled data</span></span>
<span data-ttu-id="8d3ef-193">`sum(itemCount)` est l’agrégation recommandée pour le comptage des événements.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-193">`sum(itemCount)` is the recommended aggregation to count events.</span></span> <span data-ttu-id="8d3ef-194">Dans de nombreux cas, étant donné que itemCount==1, la fonction compte simplement le nombre de lignes dans le groupe.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-194">In many cases, itemCount==1, so the function simply counts up the number of rows in the group.</span></span> <span data-ttu-id="8d3ef-195">En revanche, quand [l’échantillonnage](app-insights-sampling.md) est en cours, seule une fraction des événements d’origine est conservée comme point de données dans Application Insights. Ainsi, pour chaque point de données que vous voyez, il existe `itemCount` événements.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-195">But when [sampling](app-insights-sampling.md) is in operation, only a fraction of the original events are retained as data points in Application Insights, so that for each data point you see, there are `itemCount` events.</span></span>

<span data-ttu-id="8d3ef-196">Par exemple, si l’échantillonnage ignore 75 % des événements d’origine, itemCount == 4 dans les enregistrements conservés. Autrement dit, pour chaque enregistrement conservé, il existe quatre enregistrements d’origine.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-196">For example, if sampling discards 75% of the original events, then itemCount==4 in the retained records - that is, for every retained record, there were four original records.</span></span>

<span data-ttu-id="8d3ef-197">L’échantillonnage adaptatif rend la valeur itemCount supérieure lors des périodes pendant lesquelles votre application est utilisée de façon intensive.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-197">Adaptive sampling causes itemCount to be higher during periods when your application is being heavily used.</span></span>

<span data-ttu-id="8d3ef-198">Par conséquent, le fait de résumer itemCount donne une bonne estimation du nombre d’événements d’origine.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-198">Summing up itemCount therefore gives a good estimate of the original number of events.</span></span>

![](./media/app-insights-analytics-tour/510.png)

<span data-ttu-id="8d3ef-199">Il existe également une agrégation `count()` (et une opération de comptage), pour les cas où vous souhaitez réellement compter le nombre de lignes dans un groupe.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-199">There's also a `count()` aggregation (and a count operation), for cases where you really do want to count the number of rows in a group.</span></span>

<span data-ttu-id="8d3ef-200">Il existe toute une gamme de [fonctions d’agrégation](https://docs.loganalytics.io/learn/tutorials/aggregations.html).</span><span class="sxs-lookup"><span data-stu-id="8d3ef-200">There's a range of [aggregation functions](https://docs.loganalytics.io/learn/tutorials/aggregations.html).</span></span>

## <a name="charting-the-results"></a><span data-ttu-id="8d3ef-201">Affichage des résultats dans un graphique</span><span class="sxs-lookup"><span data-stu-id="8d3ef-201">Charting the results</span></span>
```AIQL

    exceptions
       | summarize count=sum(itemCount)  
         by bin(timestamp, 1h)
```

<span data-ttu-id="8d3ef-202">Par défaut, les résultats sont affichés sous forme de table :</span><span class="sxs-lookup"><span data-stu-id="8d3ef-202">By default, results display as a table:</span></span>

![](./media/app-insights-analytics-tour/225.png)

<span data-ttu-id="8d3ef-203">Nous pouvons aller au-delà de la vue de table.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-203">We can do better than the table view.</span></span> <span data-ttu-id="8d3ef-204">Examinons les résultats dans la vue graphique avec l’option barres verticales :</span><span class="sxs-lookup"><span data-stu-id="8d3ef-204">Let's look at the results in the chart view with the vertical bar option:</span></span>

![Cliquez sur la vue graphique, puis choisissez le graphique à barres verticales et affectez les axes x et y](./media/app-insights-analytics-tour/230.png)

<span data-ttu-id="8d3ef-206">Bien que nous n’ayons pas trié les résultats par heure (comme le montre l’affichage de table), le graphique affiche toujours les dates dans l’ordre approprié.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-206">Notice that although we didn't sort the results by time (as you can see in the table display), the chart display always shows datetimes in correct order.</span></span>


## <a name="timecharts"></a><span data-ttu-id="8d3ef-207">Graphiques temporels</span><span class="sxs-lookup"><span data-stu-id="8d3ef-207">Timecharts</span></span>
<span data-ttu-id="8d3ef-208">Afficher le nombre d’événements qui se produisent chaque heure :</span><span class="sxs-lookup"><span data-stu-id="8d3ef-208">Show how many events there are each hour:</span></span>

```AIQL

    requests
      | summarize event_count=sum(itemCount)
        by bin(timestamp, 1h)
```

<span data-ttu-id="8d3ef-209">Sélectionnez l’option d’affichage graphique :</span><span class="sxs-lookup"><span data-stu-id="8d3ef-209">Select the Chart display option:</span></span>

![Graphique temporel](./media/app-insights-analytics-tour/080.png)

## <a name="multiple-series"></a><span data-ttu-id="8d3ef-211">Séries multiples</span><span class="sxs-lookup"><span data-stu-id="8d3ef-211">Multiple series</span></span>
<span data-ttu-id="8d3ef-212">La présence de plusieurs expressions dans la clause `summarize` crée plusieurs colonnes.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-212">Multiple expressions in the `summarize` clause creates multiple columns.</span></span>

<span data-ttu-id="8d3ef-213">Plusieurs expressions de la clause `by` créent plusieurs lignes, une pour chaque combinaison de valeurs.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-213">Multiple expressions in the `by` clause creates multiple rows, one for each combination of values.</span></span>

```AIQL

    requests
    | summarize count_=sum(itemCount), avg(duration)
      by bin(timestamp, 1h), client_StateOrProvince, client_City
    | order by timestamp asc, client_StateOrProvince, client_City
```

![Tableau de demandes par heure et par emplacement](./media/app-insights-analytics-tour/090.png)

### <a name="segment-a-chart-by-dimensions"></a><span data-ttu-id="8d3ef-215">Segmentez un graphique par dimensions</span><span class="sxs-lookup"><span data-stu-id="8d3ef-215">Segment a chart by dimensions</span></span>
<span data-ttu-id="8d3ef-216">Si vous tracez un tableau comportant une colonne de type chaîne et une colonne numérique, la chaîne peut être utilisée pour fractionner les données numériques en séries de points distinctes.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-216">If you chart a table that has a string column and a numeric column, the string can be used to split the numeric data into separate series of points.</span></span> <span data-ttu-id="8d3ef-217">S’il existe plusieurs colonnes de type chaîne, vous pouvez choisir la colonne à utiliser comme discriminant.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-217">If there's more than one string column, you can choose which column to use as the discriminator.</span></span>

![Segmenter un tableau d’analyse](./media/app-insights-analytics-tour/100.png)

#### <a name="bounce-rate"></a><span data-ttu-id="8d3ef-219">Taux de rebond</span><span class="sxs-lookup"><span data-stu-id="8d3ef-219">Bounce rate</span></span>

<span data-ttu-id="8d3ef-220">Convertir un booléen en une chaîne à utiliser comme discriminant :</span><span class="sxs-lookup"><span data-stu-id="8d3ef-220">Convert a boolean to a string to use it as a discriminator:</span></span>

```AIQL

    // Bounce rate: sessions with only one page view
    requests
    | where notempty(session_Id)
    | where tostring(operation_SyntheticSource) == "" // real users
    | summarize pagesInSession=sum(itemCount), sessionEnd=max(timestamp)
               by session_Id
    | extend isbounce= pagesInSession == 1
    | summarize count()
               by tostring(isbounce), bin (sessionEnd, 1h)
    | render timechart
```

### <a name="display-multiple-metrics"></a><span data-ttu-id="8d3ef-221">Afficher plusieurs mesures</span><span class="sxs-lookup"><span data-stu-id="8d3ef-221">Display multiple metrics</span></span>
<span data-ttu-id="8d3ef-222">Si vous tracez un tableau comportant plusieurs colonnes numériques, en plus du timestamp, vous pouvez afficher n’importe quelle combinaison de celles-ci.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-222">If you chart a table that has more than one numeric column, in addition to the timestamp, you can display any combination of them.</span></span>

![Segmenter un tableau d’analyse](./media/app-insights-analytics-tour/110.png)

<span data-ttu-id="8d3ef-224">Vous devez sélectionner **Ne pas fractionner** avant de pouvoir sélectionner plusieurs colonnes numériques.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-224">You must select **Don't Split** before you can select multiple numeric columns.</span></span> <span data-ttu-id="8d3ef-225">Vous ne pouvez fractionner par colonne de chaîne tout en affichant plusieurs colonnes numériques.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-225">You can't split by a string column at the same time as displaying more than one numeric column.</span></span>

## <a name="daily-average-cycle"></a><span data-ttu-id="8d3ef-226">Cycle moyen quotidien</span><span class="sxs-lookup"><span data-stu-id="8d3ef-226">Daily average cycle</span></span>
<span data-ttu-id="8d3ef-227">Dans quelle mesure l’utilisation varie-t-elle dans un jour moyen ?</span><span class="sxs-lookup"><span data-stu-id="8d3ef-227">How does usage vary over the average day?</span></span>

<span data-ttu-id="8d3ef-228">Compter les requêtes en prenant un jour comme modulo de temps et en fractionnant le résultat par heure :</span><span class="sxs-lookup"><span data-stu-id="8d3ef-228">Count requests by the time modulo one day, binned into hours:</span></span>

```AIQL

    requests
    | where timestamp > ago(30d)  // Override "Last 24h"
    | where tostring(operation_SyntheticSource) == "" // real users
    | extend hour = bin(timestamp % 1d , 1h)
          + datetime("2016-01-01") // Allow render on line chart
    | summarize event_count=sum(itemCount) by hour
```

![Graphique en courbes des heures dans une journée moyenne](./media/app-insights-analytics-tour/120.png)

> [!NOTE]
> <span data-ttu-id="8d3ef-230">Remarquez que nous devons convertir les durées en dates pour afficher les résultats sur un graphique en courbes.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-230">Notice that we currently have to convert time durations to datetimes in order to display on a line chart.</span></span>
>
>

## <a name="compare-multiple-daily-series"></a><span data-ttu-id="8d3ef-231">Comparer plusieurs séries quotidiennes</span><span class="sxs-lookup"><span data-stu-id="8d3ef-231">Compare multiple daily series</span></span>
<span data-ttu-id="8d3ef-232">Dans quelle mesure l’utilisation varie-t-elle au fil de la journée dans différents pays ?</span><span class="sxs-lookup"><span data-stu-id="8d3ef-232">How does usage vary over the time of day in different countries?</span></span>

```AIQL

     requests  
     | where timestamp > ago(30d)  // Override "Last 24h"
     | where tostring(operation_SyntheticSource) == "" // real users
     | extend hour= floor( timestamp % 1d , 1h)
           + datetime("2001-01-01")
     | summarize event_count=sum(itemCount)
       by hour, client_CountryOrRegion
     | render timechart
```

![Fractionner par client_CountryOrRegion](./media/app-insights-analytics-tour/130.png)

## <a name="plot-a-distribution"></a><span data-ttu-id="8d3ef-234">Tracer une distribution</span><span class="sxs-lookup"><span data-stu-id="8d3ef-234">Plot a distribution</span></span>
<span data-ttu-id="8d3ef-235">Combien existe-t-il de sessions de différentes longueurs ?</span><span class="sxs-lookup"><span data-stu-id="8d3ef-235">How many sessions are there of different lengths?</span></span>

```AIQL

    requests
    | where timestamp > ago(30d) // override "Last 24h"
    | where isnotnull(session_Id) and isnotempty(session_Id)
    | summarize min(timestamp), max(timestamp)
      by session_Id
    | extend sessionDuration = max_timestamp - min_timestamp
    | where sessionDuration > 1s and sessionDuration < 3m
    | summarize count() by floor(sessionDuration, 3s)
    | project d = sessionDuration + datetime("2016-01-01"), count_
```

<span data-ttu-id="8d3ef-236">La dernière ligne est nécessaire pour la conversion en datetime.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-236">The last line is required to convert to datetime.</span></span> <span data-ttu-id="8d3ef-237">Actuellement l’axe x d’un graphique est affiché sous forme scalaire uniquement s’il s’agit d’une valeur datetime.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-237">Currently the x axis of a chart is displayed as a scalar only if it is a datetime.</span></span>

<span data-ttu-id="8d3ef-238">La clause `where` exclut les sessions à déclenchement unique (sessionDuration==0) et définit la longueur de l’axe X.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-238">The `where` clause excludes one-shot sessions (sessionDuration==0) and sets the length of the x-axis.</span></span>

![](./media/app-insights-analytics-tour/290.png)

## <a name="percentileshttpsdocsloganalyticsioquerylanguagequerylanguagepercentilesaggfunctionhtml"></a>[<span data-ttu-id="8d3ef-239">Centiles</span><span class="sxs-lookup"><span data-stu-id="8d3ef-239">Percentiles</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_percentiles_aggfunction.html)
<span data-ttu-id="8d3ef-240">Quelles sont les plages de durées qui couvrent différents pourcentages de sessions ?</span><span class="sxs-lookup"><span data-stu-id="8d3ef-240">What ranges of durations cover different percentages of sessions?</span></span>

<span data-ttu-id="8d3ef-241">Utilisez la requête ci-dessus, mais remplacez la dernière ligne :</span><span class="sxs-lookup"><span data-stu-id="8d3ef-241">Use the above query, but replace the last line:</span></span>

```AIQL

    requests
    | where isnotnull(session_Id) and isnotempty(session_Id)
    | summarize min(timestamp), max(timestamp)
      by session_Id
    | extend sesh = max_timestamp - min_timestamp
    | where sesh > 1s
    | summarize count() by floor(sesh, 3s)
    | summarize percentiles(sesh, 5, 20, 50, 80, 95)
```

<span data-ttu-id="8d3ef-242">Nous avons également supprimé la limite supérieure dans la clause where, afin d’obtenir des chiffres corrects englobant toutes les sessions avec plusieurs requêtes :</span><span class="sxs-lookup"><span data-stu-id="8d3ef-242">We also removed the upper limit in the where clause, in order to get correct figures including all sessions with more than one request:</span></span>

![result](./media/app-insights-analytics-tour/180.png)

<span data-ttu-id="8d3ef-244">Nous pouvons voir que :</span><span class="sxs-lookup"><span data-stu-id="8d3ef-244">From which we can see that:</span></span>

* <span data-ttu-id="8d3ef-245">5 % des sessions durent moins de 3 minutes 34 s ;</span><span class="sxs-lookup"><span data-stu-id="8d3ef-245">5% of sessions have a duration of less than 3 minutes 34s;</span></span>
* <span data-ttu-id="8d3ef-246">50 % des sessions durent moins de 36 minutes ;</span><span class="sxs-lookup"><span data-stu-id="8d3ef-246">50% of sessions last less than 36 minutes;</span></span>
* <span data-ttu-id="8d3ef-247">5 % des sessions durent plus de 7 jours.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-247">5% of sessions last more than 7 days</span></span>

<span data-ttu-id="8d3ef-248">Pour obtenir une répartition distincte pour chaque pays, il suffit simplement d’intégrer la colonne client_CountryOrRegion séparément par le biais des deux opérateurs summarize :</span><span class="sxs-lookup"><span data-stu-id="8d3ef-248">To get a separate breakdown for each country, we just have to bring the client_CountryOrRegion column separately through both summarize operators:</span></span>

```AIQL

    requests
    | where isnotnull(session_Id) and isnotempty(session_Id)
    | summarize min(timestamp), max(timestamp)
      by session_Id, client_CountryOrRegion
    | extend sesh = max_timestamp - min_timestamp
    | where sesh > 1s
    | summarize count() by floor(sesh, 3s), client_CountryOrRegion
    | summarize percentiles(sesh, 5, 20, 50, 80, 95)
      by client_CountryOrRegion
```

![](./media/app-insights-analytics-tour/190.png)

## <a name="join"></a><span data-ttu-id="8d3ef-249">Join</span><span class="sxs-lookup"><span data-stu-id="8d3ef-249">Join</span></span>
<span data-ttu-id="8d3ef-250">Nous avons accès à plusieurs tables, y compris les demandes et les exceptions.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-250">We have access to several tables, including requests and exceptions.</span></span>

<span data-ttu-id="8d3ef-251">Pour rechercher les exceptions liées à une requête qui a renvoyé une réponse d’échec, nous pouvons joindre les tables sur `session_Id`:</span><span class="sxs-lookup"><span data-stu-id="8d3ef-251">To find the exceptions related to a request that returned a failure response, we can join the tables on `session_Id`:</span></span>

```AIQL

    requests
    | where toint(resultCode) >= 500
    | join (exceptions) on operation_Id
    | take 30
```


<span data-ttu-id="8d3ef-252">Avant d’effectuer la jointure, nous pouvons utiliser `project` pour sélectionner uniquement les colonnes dont nous avons besoin.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-252">It's good practice to use `project` to select just the columns we need before performing the join.</span></span>
<span data-ttu-id="8d3ef-253">Dans les mêmes clauses, nous renommons la colonne timestamp.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-253">In the same clauses, we rename the timestamp column.</span></span>

## <a name="lethttpsdocsloganalyticsioquerylanguagequerylanguageletstatementhtml-assign-a-result-to-a-variable"></a><span data-ttu-id="8d3ef-254">[Let](https://docs.loganalytics.io/queryLanguage/query_language_letstatement.html): affecter un résultat à une variable</span><span class="sxs-lookup"><span data-stu-id="8d3ef-254">[Let](https://docs.loganalytics.io/queryLanguage/query_language_letstatement.html): Assign a result to a variable</span></span>

<span data-ttu-id="8d3ef-255">Utilisez `let` pour séparer les parties de l’expression précédente.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-255">Use `let` to separate out the parts of the previous expression.</span></span> <span data-ttu-id="8d3ef-256">Les résultats sont identiques :</span><span class="sxs-lookup"><span data-stu-id="8d3ef-256">The results are unchanged:</span></span>

```AIQL

    let bad_requests =
      requests
        | where  toint(resultCode) >= 500  ;
    bad_requests
    | join (exceptions) on session_Id
    | take 30
```

> [!Tip] 
> <span data-ttu-id="8d3ef-257">Dans le client Analytics, ne placez pas de lignes vides entre les différentes parties de la requête.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-257">In the Analytics client, don't put blank lines between the parts of the query.</span></span> <span data-ttu-id="8d3ef-258">Exécutez-la en totalité.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-258">Make sure to execute all of it.</span></span>
>

<span data-ttu-id="8d3ef-259">Utilisez `toscalar` pour convertir une cellule de tableau en une valeur :</span><span class="sxs-lookup"><span data-stu-id="8d3ef-259">Use `toscalar` to convert a single table cell to a value:</span></span>

```AIQL
let topCities =  toscalar (
   requests
   | summarize count() by client_City 
   | top n by count_ 
   | summarize makeset(client_City));
requests
| where client_City in (topCities(3)) 
| summarize count() by client_City;
```


### <a name="functions"></a><span data-ttu-id="8d3ef-260">Fonctions</span><span class="sxs-lookup"><span data-stu-id="8d3ef-260">Functions</span></span>

<span data-ttu-id="8d3ef-261">Utilisez *Let* pour définir une fonction :</span><span class="sxs-lookup"><span data-stu-id="8d3ef-261">Use *Let* to define a function:</span></span>

```AIQL

    let usdate = (t:datetime)
    {
      strcat(getmonth(t), "/", dayofmonth(t),"/", getyear(t), " ",
      bin((t-1h)%12h+1h,1s), iff(t%24h<12h, "AM", "PM"))
    };
    requests  
    | extend PST = usdate(timestamp-8h)
```

## <a name="accessing-nested-objects"></a><span data-ttu-id="8d3ef-262">Accès à des objets imbriqués</span><span class="sxs-lookup"><span data-stu-id="8d3ef-262">Accessing nested objects</span></span>
<span data-ttu-id="8d3ef-263">Les objets imbriqués sont faciles d’accès.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-263">Nested objects can be accessed easily.</span></span> <span data-ttu-id="8d3ef-264">Par exemple, dans le flux d’exceptions, vous pouvez voir des objets structurés comme suit :</span><span class="sxs-lookup"><span data-stu-id="8d3ef-264">For example, in the exceptions stream you can see structured objects like this:</span></span>

![result](./media/app-insights-analytics-tour/520.png)

<span data-ttu-id="8d3ef-266">Vous pouvez les aplatir en choisissant les propriétés qui vous intéressent :</span><span class="sxs-lookup"><span data-stu-id="8d3ef-266">You can flatten it by choosing the properties you're interested in:</span></span>

```AIQL

    exceptions | take 10
    | extend method1 = tostring(details[0].parsedStack[1].method)
```

<span data-ttu-id="8d3ef-267">Vous devez effectuer une conversion de type vers le type approprié.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-267">Note that you need to cast the result to the appropriate type.</span></span>


## <a name="custom-properties-and-measurements"></a><span data-ttu-id="8d3ef-268">Mesures et propriétés personnalisées</span><span class="sxs-lookup"><span data-stu-id="8d3ef-268">Custom properties and measurements</span></span>
<span data-ttu-id="8d3ef-269">Si votre application attache [des dimensions (propriétés) personnalisées et des mesures personnalisées](app-insights-api-custom-events-metrics.md#properties) à des événements, elles seront visibles dans les objets `customDimensions` et `customMeasurements`.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-269">If your application attaches [custom dimensions (properties) and custom measurements](app-insights-api-custom-events-metrics.md#properties) to events, then you will see them in the `customDimensions` and `customMeasurements` objects.</span></span>

<span data-ttu-id="8d3ef-270">Par exemple, si votre application inclut :</span><span class="sxs-lookup"><span data-stu-id="8d3ef-270">For example, if your app includes:</span></span>

```C#

    var dimensions = new Dictionary<string, string>
                     {{"p1", "v1"},{"p2", "v2"}};
    var measurements = new Dictionary<string, double>
                     {{"m1", 42.0}, {"m2", 43.2}};
    telemetryClient.TrackEvent("myEvent", dimensions, measurements);
```

<span data-ttu-id="8d3ef-271">Pour extraire ces valeurs dans Analytics :</span><span class="sxs-lookup"><span data-stu-id="8d3ef-271">To extract these values in Analytics:</span></span>

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      m1 = todouble(customMeasurements.m1) // cast to expected type

```

<span data-ttu-id="8d3ef-272">Pour vérifier si une dimension personnalisée est d’un type particulier :</span><span class="sxs-lookup"><span data-stu-id="8d3ef-272">To verify whether a custom dimension is of a particular type:</span></span>

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      iff(notnull(todouble(customMeasurements.m1)), ...
```

## <a name="dashboards"></a><span data-ttu-id="8d3ef-273">Tableaux de bord</span><span class="sxs-lookup"><span data-stu-id="8d3ef-273">Dashboards</span></span>
<span data-ttu-id="8d3ef-274">Vous pouvez épingler vos résultats à un tableau de bord afin de rassembler tous vos tableaux et graphiques les plus importants.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-274">You can pin your results to a dashboard in order to bring together all your most important charts and tables.</span></span>

* <span data-ttu-id="8d3ef-275">[Tableau de bord partagé Azure](app-insights-dashboards.md#share-dashboards) : cliquez sur l’icône d’épingle.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-275">[Azure shared dashboard](app-insights-dashboards.md#share-dashboards): Click the pin icon.</span></span> <span data-ttu-id="8d3ef-276">Avant cela, vous devez disposer d’un tableau de bord partagé.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-276">Before you do this, you must have a shared dashboard.</span></span> <span data-ttu-id="8d3ef-277">Dans le portail Azure, ouvrez ou créez un tableau de bord et cliquez sur Partager.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-277">In the Azure portal, open or create a dashboard and click Share.</span></span>
* <span data-ttu-id="8d3ef-278">[Tableau de bord Power BI](app-insights-export-power-bi.md) : cliquez sur Exporter, Requête Power BI.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-278">[Power BI dashboard](app-insights-export-power-bi.md): Click Export, Power BI Query.</span></span> <span data-ttu-id="8d3ef-279">L’avantage de cette solution est que vous pouvez afficher votre requête avec d’autres résultats issus d’un large éventail de sources.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-279">An advantage of this alternative is that you can display your query alongside other results from a wide range of sources.</span></span>

## <a name="combine-with-imported-data"></a><span data-ttu-id="8d3ef-280">Combiner avec des données importées</span><span class="sxs-lookup"><span data-stu-id="8d3ef-280">Combine with imported data</span></span>

<span data-ttu-id="8d3ef-281">Les rapports d’analyse sont du plus bel effet sur le tableau de bord mais il peut arriver que vous souhaitiez convertir les données dans un format plus digeste.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-281">Analytics reports look great on the dashboard, but sometimes you want to translate the data to a more digestible form.</span></span> <span data-ttu-id="8d3ef-282">Par exemple, supposons que vos utilisateurs authentifiés sont identifiés dans les données de télémétrie par un alias.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-282">For example, suppose your authenticated users are identified in the telemetry by an alias.</span></span> <span data-ttu-id="8d3ef-283">Vous souhaitez afficher leurs vrais noms dans vos résultats.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-283">You'd like to show their real names in your results.</span></span> <span data-ttu-id="8d3ef-284">Pour cela, vous avez besoin d’un fichier CSV qui fait correspondre les alias aux véritables noms.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-284">To do this, you need a CSV file that maps from the aliases to the real names.</span></span>

<span data-ttu-id="8d3ef-285">Vous pouvez importer un fichier de données et l’utiliser comme une table standard (requêtes, exceptions et ainsi de suite).</span><span class="sxs-lookup"><span data-stu-id="8d3ef-285">You can import a data file and use it just like any of the standard tables (requests, exceptions, and so on).</span></span> <span data-ttu-id="8d3ef-286">Interrogez-la individuellement ou joignez-la à d’autres tables.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-286">Either query it on its own, or join it with other tables.</span></span> <span data-ttu-id="8d3ef-287">Par exemple, si vous disposez d’une table nommée usermap et qu’elle contient des colonnes `realName` et `userId`, vous pouvez l’utiliser pour traduire le champ `user_AuthenticatedId` dans les données de télémétrie de la requête :</span><span class="sxs-lookup"><span data-stu-id="8d3ef-287">For example, if you have a table named usermap, and it has columns `realName` and `userId`, then you can use it to translate the `user_AuthenticatedId` field in the request telemetry:</span></span>

```AIQL

    requests
    | where notempty(user_AuthenticatedId)
    | project userId = user_AuthenticatedId
      // get the realName field from the usermap table:
    | join kind=leftouter ( usermap ) on userId
      // count transactions by name:
    | summarize count() by realName
```

<span data-ttu-id="8d3ef-288">Pour importer une table, dans le panneau Schéma, sous **Autres sources de données**, suivez les instructions pour ajouter une nouvelle source de données en téléchargeant un échantillon de vos données.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-288">To import a table, in the Schema blade, under **Other Data Sources**, follow the instructions to add a new data source, by uploading a sample of your data.</span></span> <span data-ttu-id="8d3ef-289">Vous pouvez utiliser cette définition permet de charger des tables.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-289">Then you can use this definition to upload tables.</span></span>

<span data-ttu-id="8d3ef-290">La fonctionnalité d’importation est actuellement en version préliminaire, vous verrez donc initialement un lien « Nous contacter » sous « Autres sources de données ».</span><span class="sxs-lookup"><span data-stu-id="8d3ef-290">The import feature is currently in preview, so you will initially see a "Contact us" link under "Other data sources."</span></span> <span data-ttu-id="8d3ef-291">Utilisez-le pour vous inscrire au programme d’évaluation, et le lien sera alors remplacé par un bouton « Ajouter une nouvelle source de données ».</span><span class="sxs-lookup"><span data-stu-id="8d3ef-291">Use this to sign up to the preview program, and the link will then be replaced by an "Add new data source" button.</span></span>


## <a name="tables"></a><span data-ttu-id="8d3ef-292">Tables</span><span class="sxs-lookup"><span data-stu-id="8d3ef-292">Tables</span></span>
<span data-ttu-id="8d3ef-293">Le flux de données de télémétrie provenant de votre application est accessible par le biais de plusieurs tables.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-293">The stream of telemetry received from your app is accessible through several tables.</span></span> <span data-ttu-id="8d3ef-294">Le schéma des propriétés disponibles pour chaque table est visible à la gauche de la fenêtre.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-294">The schema of properties available for each table is visible at the left of the window.</span></span>

### <a name="requests-table"></a><span data-ttu-id="8d3ef-295">Table de requêtes</span><span class="sxs-lookup"><span data-stu-id="8d3ef-295">Requests table</span></span>
<span data-ttu-id="8d3ef-296">Compter le nombre de requêtes HTTP envoyées à votre application web et les segmenter par nom de page :</span><span class="sxs-lookup"><span data-stu-id="8d3ef-296">Count HTTP requests to your web app and segment by page name:</span></span>

![Compter les requêtes segmentées par nom](./media/app-insights-analytics-tour/analytics-count-requests.png)

<span data-ttu-id="8d3ef-298">Rechercher les requêtes qui échouent le plus :</span><span class="sxs-lookup"><span data-stu-id="8d3ef-298">Find the requests that fail most:</span></span>

![Compter les requêtes segmentées par nom](./media/app-insights-analytics-tour/analytics-failed-requests.png)

### <a name="custom-events-table"></a><span data-ttu-id="8d3ef-300">Table des événements personnalisés</span><span class="sxs-lookup"><span data-stu-id="8d3ef-300">Custom events table</span></span>
<span data-ttu-id="8d3ef-301">Si vous utilisez [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) pour envoyer vos propres événements, vous pouvez les lire depuis cette table.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-301">If you use [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) to send your own events, you can read them from this table.</span></span>

<span data-ttu-id="8d3ef-302">Prenons un exemple dans lequel le code de votre application contient les lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="8d3ef-302">Let's take an example where your app code contains these lines:</span></span>

```C#

    telemetry.TrackEvent("Query",
       new Dictionary<string,string> {{"query", sqlCmd}},
       new Dictionary<string,double> {
           {"retry", retryCount},
           {"querytime", totalTime}})
```

<span data-ttu-id="8d3ef-303">Afficher la fréquence de ces événements :</span><span class="sxs-lookup"><span data-stu-id="8d3ef-303">Display the frequency of these events:</span></span>

![Afficher la fréquence des événements personnalisés](./media/app-insights-analytics-tour/analytics-custom-events-rate.png)

<span data-ttu-id="8d3ef-305">Extraire des mesures et des dimensions de ces événements :</span><span class="sxs-lookup"><span data-stu-id="8d3ef-305">Extract measurements and dimensions from the events:</span></span>

![Afficher la fréquence des événements personnalisés](./media/app-insights-analytics-tour/analytics-custom-events-dimensions.png)

### <a name="custom-metrics-table"></a><span data-ttu-id="8d3ef-307">Table des mesures personnalisées</span><span class="sxs-lookup"><span data-stu-id="8d3ef-307">Custom metrics table</span></span>
<span data-ttu-id="8d3ef-308">Si vous utilisez [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) pour envoyer vos propres valeurs métriques, vous trouverez ses résultats dans le flux **customMetrics**.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-308">If you are using [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) to send your own metric values, you’ll find its results in the **customMetrics** stream.</span></span> <span data-ttu-id="8d3ef-309">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="8d3ef-309">For example:</span></span>  

![Mesures personnalisées dans Application Insights Analytics](./media/app-insights-analytics-tour/analytics-custom-metrics.png)

> [!NOTE]
> <span data-ttu-id="8d3ef-311">Dans [Metrics Explorer](app-insights-metrics-explorer.md), toutes les mesures personnalisées attachées à une télémétrie, quel que soit son type, apparaissent dans le panneau de métriques avec les métriques envoyées à l’aide de `TrackMetric()`.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-311">In [Metrics Explorer](app-insights-metrics-explorer.md), all custom measurements attached to any type of telemetry appear together in the metrics blade along with metrics sent using `TrackMetric()`.</span></span> <span data-ttu-id="8d3ef-312">Dans Analytics, en revanche, les mesures personnalisées restent attachées à leur type de télémétrie d’origine (événements, requêtes, etc.) alors que les métriques envoyées par TrackMetric apparaissent dans leur propre flux.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-312">But in Analytics, custom measurements are still attached to whichever type of telemetry they were carried on - events or requests, and so on - while metrics sent by TrackMetric appear in their own stream.</span></span>
>
>

### <a name="performance-counters-table"></a><span data-ttu-id="8d3ef-313">Table des compteurs de performances</span><span class="sxs-lookup"><span data-stu-id="8d3ef-313">Performance counters table</span></span>
<span data-ttu-id="8d3ef-314">[Les compteurs de performances](app-insights-performance-counters.md) vous indiquent les métriques système de base pour votre application, notamment le processeur, la mémoire et l’utilisation du réseau.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-314">[Performance counters](app-insights-performance-counters.md) show you basic system metrics for your app, such as CPU, memory, and network utilization.</span></span> <span data-ttu-id="8d3ef-315">Vous pouvez configurer le Kit de développement logiciel (SDK) pour l’envoi de compteurs supplémentaires, notamment vos propres compteurs personnalisés.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-315">You can configure the SDK to send additional counters, including your own custom counters.</span></span>

<span data-ttu-id="8d3ef-316">Le schéma **compteur de performances** expose les noms `category`, `counter` et `instance` nom de chaque compteur de performance.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-316">The **performanceCounters** schema exposes the `category`, `counter` name, and `instance` name of each performance counter.</span></span> <span data-ttu-id="8d3ef-317">Les noms d’instance de compteur sont uniquement applicables à certains compteurs de performance et indiquent généralement le nom du processus auquel le comptage se rapporte.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-317">Counter instance names are only applicable to some performance counters, and typically indicate the name of the process to which the count relates.</span></span> <span data-ttu-id="8d3ef-318">Dans les données de télémétrie pour chaque application, vous ne verrez que les compteurs pour cette application.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-318">In the telemetry for each application, you’ll see only the counters for that application.</span></span> <span data-ttu-id="8d3ef-319">Par exemple, pour voir les compteurs disponibles :</span><span class="sxs-lookup"><span data-stu-id="8d3ef-319">For example, to see what counters are available:</span></span>

![Compteurs de performances dans Application Insights Analytics](./media/app-insights-analytics-tour/analytics-performance-counters.png)

<span data-ttu-id="8d3ef-321">Pour obtenir un graphique présentant la mémoire disponible sur la période sélectionnée :</span><span class="sxs-lookup"><span data-stu-id="8d3ef-321">To get a chart of available memory over the selected period:</span></span>

![Graphique temporel dans Application Insights Analytics](./media/app-insights-analytics-tour/analytics-available-memory.png)

<span data-ttu-id="8d3ef-323">Comme les autres données de télémétrie, **performanceCounters** possède également une colonne `cloud_RoleInstance` qui indique l’identité de l’ordinateur hôte sur lequel votre application est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-323">Like other telemetry, **performanceCounters** also has a column `cloud_RoleInstance` that indicates the identity of the host machine on which your app is running.</span></span> <span data-ttu-id="8d3ef-324">Par exemple, pour comparer les performances de votre application sur des ordinateurs différents :</span><span class="sxs-lookup"><span data-stu-id="8d3ef-324">For example, to compare the performance of your app on the different machines:</span></span>

![Performances segmentées par instances de rôle d’Application Insights Analytics](./media/app-insights-analytics-tour/analytics-metrics-role-instance.png)

### <a name="exceptions-table"></a><span data-ttu-id="8d3ef-326">Table des exceptions</span><span class="sxs-lookup"><span data-stu-id="8d3ef-326">Exceptions table</span></span>
<span data-ttu-id="8d3ef-327">[Les exceptions signalées par votre application](app-insights-asp-net-exceptions.md) sont disponibles dans cette table.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-327">[Exceptions reported by your app](app-insights-asp-net-exceptions.md) are available in this table.</span></span>

<span data-ttu-id="8d3ef-328">Pour rechercher la requête HTTP que votre application traitait lorsque l’exception a été levée, ajoutez l’operation_Id :</span><span class="sxs-lookup"><span data-stu-id="8d3ef-328">To find the HTTP request that your app was handling when the exception was raised, join on operation_Id:</span></span>

![Ajoutez des exceptions avec des requêtes operation_Id](./media/app-insights-analytics-tour/analytics-exception-request.png)

### <a name="browser-timings-table"></a><span data-ttu-id="8d3ef-330">Table des délais de chargement dans le navigateur</span><span class="sxs-lookup"><span data-stu-id="8d3ef-330">Browser timings table</span></span>
<span data-ttu-id="8d3ef-331">`browserTimings` affiche les données de chargement de pages collectées dans les navigateurs de vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-331">`browserTimings` shows page load data collected in your users' browsers.</span></span>

<span data-ttu-id="8d3ef-332">[Configurez votre application pour la télémétrie côté client](app-insights-javascript.md) afin de voir ces métriques.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-332">[Set up your app for client-side telemetry](app-insights-javascript.md) in order to see these metrics.</span></span>

<span data-ttu-id="8d3ef-333">Le schéma inclut [les métriques indiquant les longueurs des différentes étapes du processus de chargement de pages](app-insights-javascript.md#page-load-performance)</span><span class="sxs-lookup"><span data-stu-id="8d3ef-333">The schema includes [metrics indicating the lengths of different stages of the page loading process](app-insights-javascript.md#page-load-performance).</span></span> <span data-ttu-id="8d3ef-334">(elles n’indiquent pas la durée de fois vos utilisateurs lisent une page).</span><span class="sxs-lookup"><span data-stu-id="8d3ef-334">(They don’t indicate the length of time your users read a page.)</span></span>  

<span data-ttu-id="8d3ef-335">Afficher les popularités de différentes pages et les délais de chargement pour chaque page :</span><span class="sxs-lookup"><span data-stu-id="8d3ef-335">Show the popularities of different pages, and load times for each page:</span></span>

![Délai de chargement de page dans Analytics](./media/app-insights-analytics-tour/analytics-page-load.png)

### <a name="availability-results-table"></a><span data-ttu-id="8d3ef-337">Tableau de résultats de la disponibilité</span><span class="sxs-lookup"><span data-stu-id="8d3ef-337">Availability results table</span></span>
<span data-ttu-id="8d3ef-338">`availabilityResults` affiche les résultats de votre [tests web](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="8d3ef-338">`availabilityResults` shows the results of your [web tests](app-insights-monitor-web-app-availability.md).</span></span> <span data-ttu-id="8d3ef-339">Chaque exécution de vos tests à partir de chaque emplacement est déclarée séparément.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-339">Each run of your tests from each test location is reported separately.</span></span>

![Délai de chargement de page dans Analytics](./media/app-insights-analytics-tour/analytics-availability.png)

### <a name="dependencies-table"></a><span data-ttu-id="8d3ef-341">Table des dépendances</span><span class="sxs-lookup"><span data-stu-id="8d3ef-341">Dependencies table</span></span>
<span data-ttu-id="8d3ef-342">Contient les résultats d’appels que votre application effectue vers des bases de données et des API REST et d’autres appels vers TrackDependency().</span><span class="sxs-lookup"><span data-stu-id="8d3ef-342">Contains results of calls that your app makes to databases and REST APIs, and other calls to TrackDependency().</span></span> <span data-ttu-id="8d3ef-343">Inclut également les appels AJAX effectués à partir du navigateur.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-343">Also includes AJAX calls made from the browser.</span></span>

<span data-ttu-id="8d3ef-344">Appels AJAX à partir du navigateur :</span><span class="sxs-lookup"><span data-stu-id="8d3ef-344">AJAX calls from the browser:</span></span>

```AIQL

    dependencies | where client_Type == "Browser"
    | take 10
```

<span data-ttu-id="8d3ef-345">Appels de dépendance à partir du serveur :</span><span class="sxs-lookup"><span data-stu-id="8d3ef-345">Dependency calls from the server:</span></span>

```AIQL

    dependencies | where client_Type == "PC"
    | take 10
```

<span data-ttu-id="8d3ef-346">Les résultats de la dépendance côté serveur indiquent toujours `success==False` si l’agent Application Insights n’est pas installé.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-346">Server-side dependency results always show `success==False` if the Application Insights Agent is not installed.</span></span> <span data-ttu-id="8d3ef-347">Toutefois, les autres données sont correctes.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-347">However, the other data are correct.</span></span>

### <a name="traces-table"></a><span data-ttu-id="8d3ef-348">Table des traces</span><span class="sxs-lookup"><span data-stu-id="8d3ef-348">Traces table</span></span>
<span data-ttu-id="8d3ef-349">Contient les données de télémétrie envoyées par votre application à l’aide de TrackTrace(), ou [d’autres frameworks de journalisation](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="8d3ef-349">Contains the telemetry sent by your app using TrackTrace(), or [other logging frameworks](app-insights-asp-net-trace-logs.md).</span></span>

## <a name="video"></a><span data-ttu-id="8d3ef-350">Vidéo</span><span class="sxs-lookup"><span data-stu-id="8d3ef-350">Video</span></span> 

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

<span data-ttu-id="8d3ef-351">Requêtes avancées :</span><span class="sxs-lookup"><span data-stu-id="8d3ef-351">Advanced queries:</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Build/2016/P591/player]


## <a name="next-steps"></a><span data-ttu-id="8d3ef-352">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8d3ef-352">Next steps</span></span>
* [<span data-ttu-id="8d3ef-353">Référence sur le langage Analytics</span><span class="sxs-lookup"><span data-stu-id="8d3ef-353">Analytics language reference</span></span>](app-insights-analytics-reference.md)
* <span data-ttu-id="8d3ef-354">[L’aide-mémoire des utilisateurs de SQL](https://aka.ms/sql-analytics) traduit les idiomes courants.</span><span class="sxs-lookup"><span data-stu-id="8d3ef-354">[SQL-users' cheat sheet](https://aka.ms/sql-analytics) translates the most common idioms.</span></span>

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]
