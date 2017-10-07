---
title: "aaaA guidée Analytique dans Azure Application Insights | Documents Microsoft"
description: "Exemples courts de toutes les requêtes principales hello Analytique, hello puissant outil de recherche de l’Application Insights."
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
ms.openlocfilehash: c268e26c6bf93ac2ee2a9d5e83613150dcf90b04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="a-tour-of-analytics-in-application-insights"></a><span data-ttu-id="b1288-103">Visite guidée d’Analytics dans Application Insights</span><span class="sxs-lookup"><span data-stu-id="b1288-103">A tour of Analytics in Application Insights</span></span>
<span data-ttu-id="b1288-104">[Analytique](app-insights-analytics.md) fonctionnalité de recherche puissant de hello de [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b1288-104">[Analytics](app-insights-analytics.md) is hello powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="b1288-105">Ces pages décrivent le langage de requête Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="b1288-105">These pages describe the Log Analytics query language.</span></span>

* <span data-ttu-id="b1288-106">**[Regardez la vidéo de présentation hello](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span><span class="sxs-lookup"><span data-stu-id="b1288-106">**[Watch hello introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="b1288-107">**[Testez l’Analytique sur nos données simulées](https://analytics.applicationinsights.io/demo)**  si votre application n’envoie pas de données tooApplication Insights encore.</span><span class="sxs-lookup"><span data-stu-id="b1288-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data tooApplication Insights yet.</span></span>
* <span data-ttu-id="b1288-108">**[Feuille de graphique SQL utilisateurs](https://aka.ms/sql-analytics)**  traduit idiomes courants de hello.</span><span class="sxs-lookup"><span data-stu-id="b1288-108">**[SQL-users' cheat sheet](https://aka.ms/sql-analytics)** translates hello most common idioms.</span></span>

<span data-ttu-id="b1288-109">Nous allons vous guide dans certaines tooget de requêtes de base que vous avez démarré.</span><span class="sxs-lookup"><span data-stu-id="b1288-109">Let's take a walk through some basic queries tooget you started.</span></span>

## <a name="connect-tooyour-application-insights-data"></a><span data-ttu-id="b1288-110">Connecter des données d’Application Insights tooyour</span><span class="sxs-lookup"><span data-stu-id="b1288-110">Connect tooyour Application Insights data</span></span>
<span data-ttu-id="b1288-111">Ouvrez Analytics à partir du [panneau Vue d’ensemble](app-insights-dashboards.md) de votre application dans Application Insights :</span><span class="sxs-lookup"><span data-stu-id="b1288-111">Open Analytics from your app's [overview blade](app-insights-dashboards.md) in Application Insights:</span></span>

![Ouvrez portal.azure.com, ouvrez votre ressource Application Insights, puis cliquez sur Analyse.](./media/app-insights-analytics-tour/001.png)

## <a name="takehttpsdocsloganalyticsioquerylanguagequerylanguagetakeoperatorhtml-show-me-n-rows"></a><span data-ttu-id="b1288-113">[Take](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html): afficher n lignes</span><span class="sxs-lookup"><span data-stu-id="b1288-113">[Take](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html): show me n rows</span></span>
<span data-ttu-id="b1288-114">Les points de données qui consignent les opérations des utilisateurs (généralement des requêtes HTTP reçues par votre application web) sont stockés dans une table appelée `requests`.</span><span class="sxs-lookup"><span data-stu-id="b1288-114">Data points that log user operations (typically HTTP requests received by your web app) are stored in a table called `requests`.</span></span> <span data-ttu-id="b1288-115">Chaque ligne est un point de données de télémétrie reçu de hello Application Insights SDK dans votre application.</span><span class="sxs-lookup"><span data-stu-id="b1288-115">Each row is a telemetry data point received from hello Application Insights SDK in your app.</span></span>

<span data-ttu-id="b1288-116">Nous pouvons commencer en examinant quelques exemples de lignes de table de hello :</span><span class="sxs-lookup"><span data-stu-id="b1288-116">Let's start by examining a few sample rows of hello table:</span></span>

![results](./media/app-insights-analytics-tour/010.png)

> [!NOTE]
> <span data-ttu-id="b1288-118">Placez curseur à hello quelque part dans l’instruction de hello avant de cliquer sur OK.</span><span class="sxs-lookup"><span data-stu-id="b1288-118">Put hello cursor somewhere in hello statement before you click Go.</span></span> <span data-ttu-id="b1288-119">Vous pouvez répartir une instruction sur plusieurs lignes, mais ne placez pas de lignes vides dans une instruction.</span><span class="sxs-lookup"><span data-stu-id="b1288-119">You can split a statement over more than one line, but don't put blank lines in a statement.</span></span> <span data-ttu-id="b1288-120">Lignes vides sont un moyen pratique de tookeep plusieurs séparer les requêtes dans la fenêtre hello.</span><span class="sxs-lookup"><span data-stu-id="b1288-120">Blank lines are a convenient way tookeep several separate queries in hello window.</span></span>
>
>

<span data-ttu-id="b1288-121">Choisissez les colonnes, faites-les glisser, groupez-les par colonnes et filtrez :</span><span class="sxs-lookup"><span data-stu-id="b1288-121">Choose columns, drag them, group by columns, and filter:</span></span>

![Cliquez sur le sélecteur de colonnes en haut à droite des résultats](./media/app-insights-analytics-tour/030.png)

<span data-ttu-id="b1288-123">Développez les détails toosee hello :</span><span class="sxs-lookup"><span data-stu-id="b1288-123">Expand any item toosee hello detail:</span></span>

![Choisissez la vue de table et utilisez Configurer les colonnes](./media/app-insights-analytics-tour/040.png)

> [!NOTE]
> <span data-ttu-id="b1288-125">Cliquez sur en-tête hello d’une colonne toore-trier hello les résultats disponibles dans le navigateur web de hello.</span><span class="sxs-lookup"><span data-stu-id="b1288-125">Click hello head of a column toore-order hello results available in hello web browser.</span></span> <span data-ttu-id="b1288-126">Mais gardez à l’esprit que, pour un grand jeu de résultats, nombre de hello du navigateur toohello téléchargé de lignes est limité.</span><span class="sxs-lookup"><span data-stu-id="b1288-126">But be aware that for a large result set, hello number of rows downloaded toohello browser is limited.</span></span> <span data-ttu-id="b1288-127">Tri de cette manière n’affiche toujours pas vous hello réel le plus élevé ou les éléments de la plus basse.</span><span class="sxs-lookup"><span data-stu-id="b1288-127">Sorting this way doesn't always show you hello actual highest or lowest items.</span></span> <span data-ttu-id="b1288-128">les éléments toosort utilisent de manière fiable, hello `top` ou `sort` opérateur.</span><span class="sxs-lookup"><span data-stu-id="b1288-128">toosort items reliably, use hello `top` or `sort` operator.</span></span>
>
>

## <a name="tophttpsdocsloganalyticsioquerylanguagequerylanguagetopoperatorhtml-and-sorthttpsdocsloganalyticsioquerylanguagequerylanguagesortoperatorhtml"></a><span data-ttu-id="b1288-129">[Top](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) et [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html)</span><span class="sxs-lookup"><span data-stu-id="b1288-129">[Top](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) and [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html)</span></span>
<span data-ttu-id="b1288-130">`take`est utile tooget un exemple rapide d’un résultat, mais il affiche des lignes de table de hello dans aucun ordre particulier.</span><span class="sxs-lookup"><span data-stu-id="b1288-130">`take` is useful tooget a quick sample of a result, but it shows rows from hello table in no particular order.</span></span> <span data-ttu-id="b1288-131">tooget un affichage ordonné, utilisez `top` (pour obtenir un exemple) ou `sort` (sur la table entière de hello).</span><span class="sxs-lookup"><span data-stu-id="b1288-131">tooget an ordered view, use `top` (for a sample) or `sort` (over hello whole table).</span></span>

<span data-ttu-id="b1288-132">Afficher hello n premières lignes, classés par une colonne particulière :</span><span class="sxs-lookup"><span data-stu-id="b1288-132">Show me hello first n rows, ordered by a particular column:</span></span>

```AIQL

    requests | top 10 by timestamp desc
```

* <span data-ttu-id="b1288-133">*Syntaxe :* la plupart des opérateurs ont des paramètres de mot clé comme `by`.</span><span class="sxs-lookup"><span data-stu-id="b1288-133">*Syntax:* Most operators have keyword parameters such as `by`.</span></span>
* <span data-ttu-id="b1288-134">`desc` = ordre décroissant, `asc` = ordre croissant.</span><span class="sxs-lookup"><span data-stu-id="b1288-134">`desc` = descending order, `asc` = ascending.</span></span>

![](./media/app-insights-analytics-tour/260.png)

<span data-ttu-id="b1288-135">`top...` est une manière plus performante d’exprimer `sort ... | take...`.</span><span class="sxs-lookup"><span data-stu-id="b1288-135">`top...` is a more performant way of saying `sort ... | take...`.</span></span> <span data-ttu-id="b1288-136">Nous aurions pu écrire :</span><span class="sxs-lookup"><span data-stu-id="b1288-136">We could have written:</span></span>

```AIQL

    requests | sort by timestamp desc | take 10
```

<span data-ttu-id="b1288-137">résultat de Hello serait hello identiques, mais elle sera exécutée un peu plus lentement.</span><span class="sxs-lookup"><span data-stu-id="b1288-137">hello result would be hello same, but it would run a bit more slowly.</span></span> <span data-ttu-id="b1288-138">(Vous pouvez également écrire `order`, qui est un alias de `sort`.)</span><span class="sxs-lookup"><span data-stu-id="b1288-138">(You could also write `order`, which is an alias of `sort`.)</span></span>

<span data-ttu-id="b1288-139">les en-têtes de colonne Hello dans la vue de table hello peuvent également être utilisé toosort les résultats de hello sur l’écran hello.</span><span class="sxs-lookup"><span data-stu-id="b1288-139">hello column headers in hello table view can also be used toosort hello results on hello screen.</span></span> <span data-ttu-id="b1288-140">Mais bien entendu, si vous avez utilisé `take` ou `top` tooretrieve une partie seulement d’une table, vous allez uniquement réorganiser hello les enregistrements que vous avez récupéré.</span><span class="sxs-lookup"><span data-stu-id="b1288-140">But of course, if you've used `take` or `top` tooretrieve just part of a table, you'll only re-order hello records you've retrieved.</span></span>

## <a name="wherehttpsdocsloganalyticsioquerylanguagequerylanguagewhereoperatorhtml-filtering-on-a-condition"></a><span data-ttu-id="b1288-141">[Where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html): filtrage sur une condition</span><span class="sxs-lookup"><span data-stu-id="b1288-141">[Where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html): filtering on a condition</span></span>

<span data-ttu-id="b1288-142">Concentrons-nous sur les requêtes qui ont renvoyé un code de résultat particulier :</span><span class="sxs-lookup"><span data-stu-id="b1288-142">Let's see just requests that returned a particular result code:</span></span>

```AIQL

    requests
    | where resultCode  == "404"
    | take 10
```

![](./media/app-insights-analytics-tour/250.png)

<span data-ttu-id="b1288-143">Hello `where` l’opérateur accepte une expression booléenne.</span><span class="sxs-lookup"><span data-stu-id="b1288-143">hello `where` operator takes a Boolean expression.</span></span> <span data-ttu-id="b1288-144">Voici quelques points clés les concernant :</span><span class="sxs-lookup"><span data-stu-id="b1288-144">Here are some key points about them:</span></span>

* <span data-ttu-id="b1288-145">`and`, `or` : opérateurs booléens</span><span class="sxs-lookup"><span data-stu-id="b1288-145">`and`, `or`: Boolean operators</span></span>
* <span data-ttu-id="b1288-146">`==`, `<>`, `!=` : égal à et différent de</span><span class="sxs-lookup"><span data-stu-id="b1288-146">`==`, `<>`, `!=` : equal and not equal</span></span>
* <span data-ttu-id="b1288-147">`=~`, `!~` : chaîne ne respectant pas la casse (égal à et différent de).</span><span class="sxs-lookup"><span data-stu-id="b1288-147">`=~`, `!~` : case-insensitive string equal and not equal.</span></span> <span data-ttu-id="b1288-148">Il existe de nombreux autres opérateurs de comparaison de chaîne.</span><span class="sxs-lookup"><span data-stu-id="b1288-148">There are lots more string comparison operators.</span></span>

<!---Read all about [scalar expressions]().--->

### <a name="getting-hello-right-type"></a><span data-ttu-id="b1288-149">Mise en route du type approprié de hello</span><span class="sxs-lookup"><span data-stu-id="b1288-149">Getting hello right type</span></span>
<span data-ttu-id="b1288-150">Rechercher les requêtes ayant échoué :</span><span class="sxs-lookup"><span data-stu-id="b1288-150">Find unsuccessful requests:</span></span>

```AIQL

    requests
    | where isnotempty(resultCode) and toint(resultCode) >= 400
```
<!---
`resultCode` has type string, so we must cast it app-insights-analytics-reference.md#casts for a numeric comparison.
--->

## <a name="time"></a><span data-ttu-id="b1288-151">Temps</span><span class="sxs-lookup"><span data-stu-id="b1288-151">Time</span></span>

<span data-ttu-id="b1288-152">Par défaut, vos requêtes sont restreinte toohello des dernières 24 heures.</span><span class="sxs-lookup"><span data-stu-id="b1288-152">By default, your queries are restricted toohello last 24 hours.</span></span> <span data-ttu-id="b1288-153">Mais vous pouvez modifier cette plage :</span><span class="sxs-lookup"><span data-stu-id="b1288-153">But you can change this range:</span></span>

![](./media/app-insights-analytics-tour/change-time-range.png)

<span data-ttu-id="b1288-154">Remplacer l’intervalle de temps hello en écrivant une requête qui mentionne `timestamp` dans une clause where.</span><span class="sxs-lookup"><span data-stu-id="b1288-154">Override hello time range by writing any query that mentions `timestamp` in a where-clause.</span></span> <span data-ttu-id="b1288-155">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="b1288-155">For example:</span></span>

```AIQL

    // What were hello slowest requests over hello past 3 days?
    requests
    | where timestamp > ago(3d)  // Override hello time range
    | top 5 by duration
```

<span data-ttu-id="b1288-156">fonction de plage de temps Hello est équivalent tooa 'where' clause inséré après chaque mention d’une des tables de source de hello.</span><span class="sxs-lookup"><span data-stu-id="b1288-156">hello time range feature is equivalent tooa 'where' clause inserted after each mention of one of hello source tables.</span></span>

<span data-ttu-id="b1288-157">`ago(3d)` signifie « il y a trois jours ».</span><span class="sxs-lookup"><span data-stu-id="b1288-157">`ago(3d)` means 'three days ago'.</span></span> <span data-ttu-id="b1288-158">Il existe d’autres unités de temps, par exemple les heures (`2h`, `2.5h`), les minutes (`25m`) et les secondes (`10s`).</span><span class="sxs-lookup"><span data-stu-id="b1288-158">Other units of time include hours (`2h`, `2.5h`), minutes (`25m`), and seconds (`10s`).</span></span>

<span data-ttu-id="b1288-159">Autres exemples :</span><span class="sxs-lookup"><span data-stu-id="b1288-159">Other examples:</span></span>

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

<span data-ttu-id="b1288-160">[Référence sur les dates et les heures](https://docs.loganalytics.io/concepts/concepts_datatypes_datetime.html).</span><span class="sxs-lookup"><span data-stu-id="b1288-160">[Dates and times reference](https://docs.loganalytics.io/concepts/concepts_datatypes_datetime.html).</span></span>


## <a name="projecthttpsdocsloganalyticsioquerylanguagequerylanguageprojectoperatorhtml-select-rename-and-compute-columns"></a><span data-ttu-id="b1288-161">[Projet](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) : sélectionnez, renommez et calculez des colonnes</span><span class="sxs-lookup"><span data-stu-id="b1288-161">[Project](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html): select, rename, and compute columns</span></span>
<span data-ttu-id="b1288-162">Utilisez [ `project` ](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) toopick simplement les colonnes hello souhaité :</span><span class="sxs-lookup"><span data-stu-id="b1288-162">Use [`project`](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) toopick out just hello columns you want:</span></span>

```AIQL

    requests | top 10 by timestamp desc
             | project timestamp, name, resultCode
```

![](./media/app-insights-analytics-tour/240.png)

<span data-ttu-id="b1288-163">Vous pouvez également renommer des colonnes et en définir de nouvelles :</span><span class="sxs-lookup"><span data-stu-id="b1288-163">You can also rename columns and define new ones:</span></span>

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

* <span data-ttu-id="b1288-165">Les noms de colonnes peuvent contenir des espaces ou des symboles s’ils sont placés entre crochets comme suit : `['...']` ou `["..."]`</span><span class="sxs-lookup"><span data-stu-id="b1288-165">Column names can include spaces or symbols if they are bracketed like this: `['...']` or `["..."]`</span></span>
* <span data-ttu-id="b1288-166">`%`est hello habituel opérateur modulo.</span><span class="sxs-lookup"><span data-stu-id="b1288-166">`%` is hello usual modulo operator.</span></span>
* <span data-ttu-id="b1288-167">`1d` (le chiffre un, suivi de la lettre d) est un littéral d’intervalle de temps qui signifie un jour.</span><span class="sxs-lookup"><span data-stu-id="b1288-167">`1d` (that's a digit one, then a 'd') is a timespan literal meaning one day.</span></span> <span data-ttu-id="b1288-168">Voici d’autres littéraux d’intervalle de temps : `12h`, `30m`, `10s`, `0.01s`.</span><span class="sxs-lookup"><span data-stu-id="b1288-168">Here are some more timespan literals: `12h`, `30m`, `10s`, `0.01s`.</span></span>
* <span data-ttu-id="b1288-169">`floor`(alias `bin`) Arrondit une valeur vers le bas toohello multiple de valeur de base hello vous fournissez le plus proche.</span><span class="sxs-lookup"><span data-stu-id="b1288-169">`floor` (alias `bin`) rounds a value down toohello nearest multiple of hello base value you provide.</span></span> <span data-ttu-id="b1288-170">Par conséquent, `floor(aTime, 1s)` Arrondit vers le bas toohello plus proche de la seconde fois.</span><span class="sxs-lookup"><span data-stu-id="b1288-170">So `floor(aTime, 1s)` rounds a time down toohello nearest second.</span></span>

<span data-ttu-id="b1288-171">Les expressions peuvent inclure tous les opérateurs habituels hello (`+`, `-`,...), et il existe une gamme de fonctions utiles.</span><span class="sxs-lookup"><span data-stu-id="b1288-171">Expressions can include all hello usual operators (`+`, `-`, ...), and there's a range of useful functions.</span></span>

## <a name="extend"></a><span data-ttu-id="b1288-172">Extend</span><span class="sxs-lookup"><span data-stu-id="b1288-172">Extend</span></span>
<span data-ttu-id="b1288-173">Si vous souhaitez simplement tooadd toohello de colonnes des groupes existants, utilisez [ `extend` ](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html):</span><span class="sxs-lookup"><span data-stu-id="b1288-173">If you just want tooadd columns toohello existing ones, use [`extend`](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html):</span></span>

```AIQL

    requests
    | top 10 by timestamp desc
    | extend timeOfDay = floor(timestamp % 1d, 1s)
```

<span data-ttu-id="b1288-174">À l’aide de [ `extend` ](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html) est moins détaillé que [ `project` ](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) si vous souhaitez tookeep tous hello colonnes existantes.</span><span class="sxs-lookup"><span data-stu-id="b1288-174">Using [`extend`](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html) is less verbose than [`project`](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) if you want tookeep all hello existing columns.</span></span>

### <a name="convert-toolocal-time"></a><span data-ttu-id="b1288-175">Convertir l’heure de toolocal</span><span class="sxs-lookup"><span data-stu-id="b1288-175">Convert toolocal time</span></span>

<span data-ttu-id="b1288-176">Les timestamps sont toujours exprimés en UTC.</span><span class="sxs-lookup"><span data-stu-id="b1288-176">Timestamps are always in UTC.</span></span> <span data-ttu-id="b1288-177">Par conséquent, si vous êtes sur hello nous Nord, et il s’agit d’hiver, vous pouvez comme ceci :</span><span class="sxs-lookup"><span data-stu-id="b1288-177">So if you're on hello US Pacific coast and it's winter, you might like this:</span></span>

```AIQL

    requests
    | top 10 by timestamp desc
    | extend localTime = timestamp - 8h
```


## <a name="summarizehttpsdocsloganalyticsioquerylanguagequerylanguagesummarizeoperatorhtml-aggregate-groups-of-rows"></a><span data-ttu-id="b1288-178">[Summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html): agréger des groupes de lignes</span><span class="sxs-lookup"><span data-stu-id="b1288-178">[Summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html): aggregate groups of rows</span></span>
<span data-ttu-id="b1288-179">`Summarize` applique une *fonction d’agrégation* spécifiée sur des groupes de lignes.</span><span class="sxs-lookup"><span data-stu-id="b1288-179">`Summarize` applies a specified *aggregation function* over groups of rows.</span></span>

<span data-ttu-id="b1288-180">Par exemple, le temps de hello votre application web prend toorespond tooa demande est indiqué dans le champ de hello `duration`.</span><span class="sxs-lookup"><span data-stu-id="b1288-180">For example, hello time your web app takes toorespond tooa request is reported in hello field `duration`.</span></span> <span data-ttu-id="b1288-181">Voyons de réponse moyen de hello tooall demandes de temps :</span><span class="sxs-lookup"><span data-stu-id="b1288-181">Let's see hello average response time tooall requests:</span></span>

![](./media/app-insights-analytics-tour/410.png)

<span data-ttu-id="b1288-182">Ou bien, nous avons séparer le résultat de hello dans des demandes de noms différents :</span><span class="sxs-lookup"><span data-stu-id="b1288-182">Or we could separate hello result into requests of different names:</span></span>

![](./media/app-insights-analytics-tour/420.png)

<span data-ttu-id="b1288-183">`Summarize`collecte hello des points de données dans le flux de hello en groupes pour le hello `by` clause évalue également.</span><span class="sxs-lookup"><span data-stu-id="b1288-183">`Summarize` collects hello data points in hello stream into groups for which hello `by` clause evaluates equally.</span></span> <span data-ttu-id="b1288-184">Chaque valeur Bonjour `by` expression - chaque nom de l’opération Bonjour exemple ci-dessus - génère une ligne dans la table de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="b1288-184">Each value in hello `by` expression - each operation name in hello above example - results in a row in hello result table.</span></span>

<span data-ttu-id="b1288-185">Nous pouvons également regrouper les résultats par heure :</span><span class="sxs-lookup"><span data-stu-id="b1288-185">Or we could group results by time of day:</span></span>

![](./media/app-insights-analytics-tour/430.png)

<span data-ttu-id="b1288-186">Notez la façon dont nous utilisons hello `bin` (fonction) (également appelé `floor`).</span><span class="sxs-lookup"><span data-stu-id="b1288-186">Notice how we're using hello `bin` function (aka `floor`).</span></span> <span data-ttu-id="b1288-187">Si nous avions simplement utilisé `by timestamp`, chaque ligne d’entrée apparaîtrait dans un groupe individuel.</span><span class="sxs-lookup"><span data-stu-id="b1288-187">If we just used `by timestamp`, every input row would end up in its own little group.</span></span> <span data-ttu-id="b1288-188">Pour n’importe quel scalaire continue like heures ou des nombres, nous avons plage continue de toobreak hello dans un nombre raisonnable de valeurs discrètes.</span><span class="sxs-lookup"><span data-stu-id="b1288-188">For any continuous scalar like times or numbers, we have toobreak hello continuous range into a manageable number of discrete values.</span></span> <span data-ttu-id="b1288-189">`bin`-qui est simplement hello familiers arrondi vers le bas `floor` fonction - est toodo de façon plus simple de hello qui.</span><span class="sxs-lookup"><span data-stu-id="b1288-189">`bin` - which is just hello familiar rounding-down `floor` function - is hello easiest way toodo that.</span></span>

<span data-ttu-id="b1288-190">Nous pouvons utiliser hello même plages de tooreduce technique de chaînes :</span><span class="sxs-lookup"><span data-stu-id="b1288-190">We can use hello same technique tooreduce ranges of strings:</span></span>

![](./media/app-insights-analytics-tour/440.png)

<span data-ttu-id="b1288-191">Notez que vous pouvez utiliser `name=` nom de hello tooset d’une colonne de résultats, dans les expressions d’agrégation hello ou la clause by hello.</span><span class="sxs-lookup"><span data-stu-id="b1288-191">Notice that you can use `name=` tooset hello name of a result column, either in hello aggregation expressions or hello by-clause.</span></span>

## <a name="counting-sampled-data"></a><span data-ttu-id="b1288-192">Décompte des données échantillonnées</span><span class="sxs-lookup"><span data-stu-id="b1288-192">Counting sampled data</span></span>
<span data-ttu-id="b1288-193">`sum(itemCount)`est hello recommandée toocount événements d’agrégation.</span><span class="sxs-lookup"><span data-stu-id="b1288-193">`sum(itemCount)` is hello recommended aggregation toocount events.</span></span> <span data-ttu-id="b1288-194">Dans de nombreux cas, itemCount == 1, afin de la fonction hello compte simplement nombre de hello de lignes dans le groupe de hello.</span><span class="sxs-lookup"><span data-stu-id="b1288-194">In many cases, itemCount==1, so hello function simply counts up hello number of rows in hello group.</span></span> <span data-ttu-id="b1288-195">Mais lorsque [échantillonnage](app-insights-sampling.md) est dans l’opération, seule une fraction d’événements d’origine de hello sont conservées en tant que points de données d’Application Insights, de sorte que pour chaque point de données que vous voyez, `itemCount` événements.</span><span class="sxs-lookup"><span data-stu-id="b1288-195">But when [sampling](app-insights-sampling.md) is in operation, only a fraction of hello original events are retained as data points in Application Insights, so that for each data point you see, there are `itemCount` events.</span></span>

<span data-ttu-id="b1288-196">Par exemple, si l’échantillonnage ignore 75 % des événements d’origine de hello, puis itemCount == 4 dans les enregistrements hello conservée - autrement dit, pour chaque enregistrement de retenue, il existait quatre enregistrements d’origine.</span><span class="sxs-lookup"><span data-stu-id="b1288-196">For example, if sampling discards 75% of hello original events, then itemCount==4 in hello retained records - that is, for every retained record, there were four original records.</span></span>

<span data-ttu-id="b1288-197">Échantillonnage Adaptive entraîne toobe itemCount plus élevé pendant les périodes lorsque votre application est utilisée de manière intensive.</span><span class="sxs-lookup"><span data-stu-id="b1288-197">Adaptive sampling causes itemCount toobe higher during periods when your application is being heavily used.</span></span>

<span data-ttu-id="b1288-198">Cumulant itemCount donne donc une bonne estimation du nombre d’origine de hello d’événements.</span><span class="sxs-lookup"><span data-stu-id="b1288-198">Summing up itemCount therefore gives a good estimate of hello original number of events.</span></span>

![](./media/app-insights-analytics-tour/510.png)

<span data-ttu-id="b1288-199">Il existe également un `count()` d’agrégation (et une opération count), pour les cas où vous vraiment voulez nombre de hello toocount de lignes dans un groupe.</span><span class="sxs-lookup"><span data-stu-id="b1288-199">There's also a `count()` aggregation (and a count operation), for cases where you really do want toocount hello number of rows in a group.</span></span>

<span data-ttu-id="b1288-200">Il existe toute une gamme de [fonctions d’agrégation](https://docs.loganalytics.io/learn/tutorials/aggregations.html).</span><span class="sxs-lookup"><span data-stu-id="b1288-200">There's a range of [aggregation functions](https://docs.loganalytics.io/learn/tutorials/aggregations.html).</span></span>

## <a name="charting-hello-results"></a><span data-ttu-id="b1288-201">Graphique des résultats de hello</span><span class="sxs-lookup"><span data-stu-id="b1288-201">Charting hello results</span></span>
```AIQL

    exceptions
       | summarize count=sum(itemCount)  
         by bin(timestamp, 1h)
```

<span data-ttu-id="b1288-202">Par défaut, les résultats sont affichés sous forme de table :</span><span class="sxs-lookup"><span data-stu-id="b1288-202">By default, results display as a table:</span></span>

![](./media/app-insights-analytics-tour/225.png)

<span data-ttu-id="b1288-203">Nous pouvons faire de meilleures performances que la vue de table hello.</span><span class="sxs-lookup"><span data-stu-id="b1288-203">We can do better than hello table view.</span></span> <span data-ttu-id="b1288-204">Examinons les résultats hello dans la vue du graphique hello avec l’option de barre verticale hello :</span><span class="sxs-lookup"><span data-stu-id="b1288-204">Let's look at hello results in hello chart view with hello vertical bar option:</span></span>

![Cliquez sur la vue graphique, puis choisissez le graphique à barres verticales et affectez les axes x et y](./media/app-insights-analytics-tour/230.png)

<span data-ttu-id="b1288-206">Notez que bien que nous n’avez pas trier les résultats de hello par heure (comme vous pouvez le voir dans l’affichage de la table hello), affichage du graphique hello affiche toujours les dates/heures dans le bon ordre.</span><span class="sxs-lookup"><span data-stu-id="b1288-206">Notice that although we didn't sort hello results by time (as you can see in hello table display), hello chart display always shows datetimes in correct order.</span></span>


## <a name="timecharts"></a><span data-ttu-id="b1288-207">Graphiques temporels</span><span class="sxs-lookup"><span data-stu-id="b1288-207">Timecharts</span></span>
<span data-ttu-id="b1288-208">Afficher le nombre d’événements qui se produisent chaque heure :</span><span class="sxs-lookup"><span data-stu-id="b1288-208">Show how many events there are each hour:</span></span>

```AIQL

    requests
      | summarize event_count=sum(itemCount)
        by bin(timestamp, 1h)
```

<span data-ttu-id="b1288-209">Sélectionnez l’option d’affichage graphique hello :</span><span class="sxs-lookup"><span data-stu-id="b1288-209">Select hello Chart display option:</span></span>

![Graphique temporel](./media/app-insights-analytics-tour/080.png)

## <a name="multiple-series"></a><span data-ttu-id="b1288-211">Séries multiples</span><span class="sxs-lookup"><span data-stu-id="b1288-211">Multiple series</span></span>
<span data-ttu-id="b1288-212">Plusieurs expressions Bonjour `summarize` clause crée plusieurs colonnes.</span><span class="sxs-lookup"><span data-stu-id="b1288-212">Multiple expressions in hello `summarize` clause creates multiple columns.</span></span>

<span data-ttu-id="b1288-213">Plusieurs expressions Bonjour `by` clause crée plusieurs lignes, une pour chaque combinaison de valeurs.</span><span class="sxs-lookup"><span data-stu-id="b1288-213">Multiple expressions in hello `by` clause creates multiple rows, one for each combination of values.</span></span>

```AIQL

    requests
    | summarize count_=sum(itemCount), avg(duration)
      by bin(timestamp, 1h), client_StateOrProvince, client_City
    | order by timestamp asc, client_StateOrProvince, client_City
```

![Tableau de demandes par heure et par emplacement](./media/app-insights-analytics-tour/090.png)

### <a name="segment-a-chart-by-dimensions"></a><span data-ttu-id="b1288-215">Segmentez un graphique par dimensions</span><span class="sxs-lookup"><span data-stu-id="b1288-215">Segment a chart by dimensions</span></span>
<span data-ttu-id="b1288-216">Si graphique sur une table qui comporte une colonne de chaîne et une colonne numérique, chaîne de hello peut être utilisé toosplit hello des données numériques en séries distinctes de points.</span><span class="sxs-lookup"><span data-stu-id="b1288-216">If you chart a table that has a string column and a numeric column, hello string can be used toosplit hello numeric data into separate series of points.</span></span> <span data-ttu-id="b1288-217">S’il existe plusieurs colonnes de chaîne, vous pouvez choisir quels toouse de colonne en tant que discriminateur de hello.</span><span class="sxs-lookup"><span data-stu-id="b1288-217">If there's more than one string column, you can choose which column toouse as hello discriminator.</span></span>

![Segmenter un tableau d’analyse](./media/app-insights-analytics-tour/100.png)

#### <a name="bounce-rate"></a><span data-ttu-id="b1288-219">Taux de rebond</span><span class="sxs-lookup"><span data-stu-id="b1288-219">Bounce rate</span></span>

<span data-ttu-id="b1288-220">Convertir un toouse de chaîne booléenne tooa comme un discriminateur :</span><span class="sxs-lookup"><span data-stu-id="b1288-220">Convert a boolean tooa string toouse it as a discriminator:</span></span>

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

### <a name="display-multiple-metrics"></a><span data-ttu-id="b1288-221">Afficher plusieurs mesures</span><span class="sxs-lookup"><span data-stu-id="b1288-221">Display multiple metrics</span></span>
<span data-ttu-id="b1288-222">Si vous représenter une table qui comporte plus d’une colonne numérique, dans Ajout toohello timestamp, vous pouvez afficher n’importe quelle combinaison d’eux.</span><span class="sxs-lookup"><span data-stu-id="b1288-222">If you chart a table that has more than one numeric column, in addition toohello timestamp, you can display any combination of them.</span></span>

![Segmenter un tableau d’analyse](./media/app-insights-analytics-tour/110.png)

<span data-ttu-id="b1288-224">Vous devez sélectionner **Ne pas fractionner** avant de pouvoir sélectionner plusieurs colonnes numériques.</span><span class="sxs-lookup"><span data-stu-id="b1288-224">You must select **Don't Split** before you can select multiple numeric columns.</span></span> <span data-ttu-id="b1288-225">Vous ne peut pas fractionner en une colonne de chaîne à hello même temps en tant que l’affichage de plusieurs colonnes numériques.</span><span class="sxs-lookup"><span data-stu-id="b1288-225">You can't split by a string column at hello same time as displaying more than one numeric column.</span></span>

## <a name="daily-average-cycle"></a><span data-ttu-id="b1288-226">Cycle moyen quotidien</span><span class="sxs-lookup"><span data-stu-id="b1288-226">Daily average cycle</span></span>
<span data-ttu-id="b1288-227">Dans quelle mesure l’utilisation de fonction sur une journée moyenne et hello ?</span><span class="sxs-lookup"><span data-stu-id="b1288-227">How does usage vary over hello average day?</span></span>

<span data-ttu-id="b1288-228">Demandes de nombre par heure hello modulo une journée, placées dans heures :</span><span class="sxs-lookup"><span data-stu-id="b1288-228">Count requests by hello time modulo one day, binned into hours:</span></span>

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
> <span data-ttu-id="b1288-230">Notez que nous disposons tooconvert temps durées toodatetimes dans l’ordre toodisplay sur un graphique en courbes.</span><span class="sxs-lookup"><span data-stu-id="b1288-230">Notice that we currently have tooconvert time durations toodatetimes in order toodisplay on a line chart.</span></span>
>
>

## <a name="compare-multiple-daily-series"></a><span data-ttu-id="b1288-231">Comparer plusieurs séries quotidiennes</span><span class="sxs-lookup"><span data-stu-id="b1288-231">Compare multiple daily series</span></span>
<span data-ttu-id="b1288-232">Comment l’utilisation de varier au fil du temps hello du jour dans différents pays ?</span><span class="sxs-lookup"><span data-stu-id="b1288-232">How does usage vary over hello time of day in different countries?</span></span>

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

## <a name="plot-a-distribution"></a><span data-ttu-id="b1288-234">Tracer une distribution</span><span class="sxs-lookup"><span data-stu-id="b1288-234">Plot a distribution</span></span>
<span data-ttu-id="b1288-235">Combien existe-t-il de sessions de différentes longueurs ?</span><span class="sxs-lookup"><span data-stu-id="b1288-235">How many sessions are there of different lengths?</span></span>

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

<span data-ttu-id="b1288-236">Hello dernière ligne est requis tooconvert toodatetime.</span><span class="sxs-lookup"><span data-stu-id="b1288-236">hello last line is required tooconvert toodatetime.</span></span> <span data-ttu-id="b1288-237">Axe hello x d’un graphique est actuellement affiché en tant qu’une valeur scalaire uniquement s’il est une valeur datetime.</span><span class="sxs-lookup"><span data-stu-id="b1288-237">Currently hello x axis of a chart is displayed as a scalar only if it is a datetime.</span></span>

<span data-ttu-id="b1288-238">Hello `where` clause exclut les sessions Shot (Durée_de_la_session == 0) et jeux hello longueur de l’axe des abscisses hello.</span><span class="sxs-lookup"><span data-stu-id="b1288-238">hello `where` clause excludes one-shot sessions (sessionDuration==0) and sets hello length of hello x-axis.</span></span>

![](./media/app-insights-analytics-tour/290.png)

## <a name="percentileshttpsdocsloganalyticsioquerylanguagequerylanguagepercentilesaggfunctionhtml"></a>[<span data-ttu-id="b1288-239">Centiles</span><span class="sxs-lookup"><span data-stu-id="b1288-239">Percentiles</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_percentiles_aggfunction.html)
<span data-ttu-id="b1288-240">Quelles sont les plages de durées qui couvrent différents pourcentages de sessions ?</span><span class="sxs-lookup"><span data-stu-id="b1288-240">What ranges of durations cover different percentages of sessions?</span></span>

<span data-ttu-id="b1288-241">Utilisez hello au-dessus de requête, mais remplacez hello dernière ligne :</span><span class="sxs-lookup"><span data-stu-id="b1288-241">Use hello above query, but replace hello last line:</span></span>

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

<span data-ttu-id="b1288-242">Nous avons supprimé également limite supérieure de hello Bonjour où clause, dans l’ordre tooget corriger des chiffres, y compris toutes les sessions avec plusieurs demandes :</span><span class="sxs-lookup"><span data-stu-id="b1288-242">We also removed hello upper limit in hello where clause, in order tooget correct figures including all sessions with more than one request:</span></span>

![result](./media/app-insights-analytics-tour/180.png)

<span data-ttu-id="b1288-244">Nous pouvons voir que :</span><span class="sxs-lookup"><span data-stu-id="b1288-244">From which we can see that:</span></span>

* <span data-ttu-id="b1288-245">5 % des sessions durent moins de 3 minutes 34 s ;</span><span class="sxs-lookup"><span data-stu-id="b1288-245">5% of sessions have a duration of less than 3 minutes 34s;</span></span>
* <span data-ttu-id="b1288-246">50 % des sessions durent moins de 36 minutes ;</span><span class="sxs-lookup"><span data-stu-id="b1288-246">50% of sessions last less than 36 minutes;</span></span>
* <span data-ttu-id="b1288-247">5 % des sessions durent plus de 7 jours.</span><span class="sxs-lookup"><span data-stu-id="b1288-247">5% of sessions last more than 7 days</span></span>

<span data-ttu-id="b1288-248">tooget une répartition distincte pour chaque pays, nous avons simplement avoir toobring hello client_CountryOrRegion colonne séparément à la fois résumer les opérateurs :</span><span class="sxs-lookup"><span data-stu-id="b1288-248">tooget a separate breakdown for each country, we just have toobring hello client_CountryOrRegion column separately through both summarize operators:</span></span>

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

## <a name="join"></a><span data-ttu-id="b1288-249">Join</span><span class="sxs-lookup"><span data-stu-id="b1288-249">Join</span></span>
<span data-ttu-id="b1288-250">Nous avons accès tooseveral tables, y compris les demandes et les exceptions.</span><span class="sxs-lookup"><span data-stu-id="b1288-250">We have access tooseveral tables, including requests and exceptions.</span></span>

<span data-ttu-id="b1288-251">Nous pouvons toofind hello exceptions connexes tooa demande a renvoyé une réponse d’échec, joindre des tables de hello sur `session_Id`:</span><span class="sxs-lookup"><span data-stu-id="b1288-251">toofind hello exceptions related tooa request that returned a failure response, we can join hello tables on `session_Id`:</span></span>

```AIQL

    requests
    | where toint(resultCode) >= 500
    | join (exceptions) on operation_Id
    | take 30
```


<span data-ttu-id="b1288-252">Il est conseillé toouse `project` tooselect les colonnes hello simplement nous avons besoin avant d’effectuer hello jointure.</span><span class="sxs-lookup"><span data-stu-id="b1288-252">It's good practice toouse `project` tooselect just hello columns we need before performing hello join.</span></span>
<span data-ttu-id="b1288-253">Bonjour les clauses de mêmes, nous renommer la colonne de type timestamp hello.</span><span class="sxs-lookup"><span data-stu-id="b1288-253">In hello same clauses, we rename hello timestamp column.</span></span>

## <a name="lethttpsdocsloganalyticsioquerylanguagequerylanguageletstatementhtml-assign-a-result-tooa-variable"></a><span data-ttu-id="b1288-254">[Laisser](https://docs.loganalytics.io/queryLanguage/query_language_letstatement.html): assignez une variable tooa de résultat</span><span class="sxs-lookup"><span data-stu-id="b1288-254">[Let](https://docs.loganalytics.io/queryLanguage/query_language_letstatement.html): Assign a result tooa variable</span></span>

<span data-ttu-id="b1288-255">Utilisez `let` tooseparate parties hello de l’expression précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="b1288-255">Use `let` tooseparate out hello parts of hello previous expression.</span></span> <span data-ttu-id="b1288-256">résultats de Hello sont identiques :</span><span class="sxs-lookup"><span data-stu-id="b1288-256">hello results are unchanged:</span></span>

```AIQL

    let bad_requests =
      requests
        | where  toint(resultCode) >= 500  ;
    bad_requests
    | join (exceptions) on session_Id
    | take 30
```

> [!Tip] 
> <span data-ttu-id="b1288-257">Dans le client d’Analytique hello, ne placez pas de lignes vides entre les parties hello de requête de hello.</span><span class="sxs-lookup"><span data-stu-id="b1288-257">In hello Analytics client, don't put blank lines between hello parts of hello query.</span></span> <span data-ttu-id="b1288-258">Vérifiez que tooexecute tous les de celui-ci.</span><span class="sxs-lookup"><span data-stu-id="b1288-258">Make sure tooexecute all of it.</span></span>
>

<span data-ttu-id="b1288-259">Utilisez `toscalar` tooconvert une valeur de tooa de cellule de table unique :</span><span class="sxs-lookup"><span data-stu-id="b1288-259">Use `toscalar` tooconvert a single table cell tooa value:</span></span>

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


### <a name="functions"></a><span data-ttu-id="b1288-260">Fonctions</span><span class="sxs-lookup"><span data-stu-id="b1288-260">Functions</span></span>

<span data-ttu-id="b1288-261">Utilisez *permettent* toodefine une fonction :</span><span class="sxs-lookup"><span data-stu-id="b1288-261">Use *Let* toodefine a function:</span></span>

```AIQL

    let usdate = (t:datetime)
    {
      strcat(getmonth(t), "/", dayofmonth(t),"/", getyear(t), " ",
      bin((t-1h)%12h+1h,1s), iff(t%24h<12h, "AM", "PM"))
    };
    requests  
    | extend PST = usdate(timestamp-8h)
```

## <a name="accessing-nested-objects"></a><span data-ttu-id="b1288-262">Accès à des objets imbriqués</span><span class="sxs-lookup"><span data-stu-id="b1288-262">Accessing nested objects</span></span>
<span data-ttu-id="b1288-263">Les objets imbriqués sont faciles d’accès.</span><span class="sxs-lookup"><span data-stu-id="b1288-263">Nested objects can be accessed easily.</span></span> <span data-ttu-id="b1288-264">Par exemple, dans le flux d’exceptions hello, vous pouvez voir des objets structurés comme suit :</span><span class="sxs-lookup"><span data-stu-id="b1288-264">For example, in hello exceptions stream you can see structured objects like this:</span></span>

![result](./media/app-insights-analytics-tour/520.png)

<span data-ttu-id="b1288-266">Vous pouvez aplatir en choisissant Propriétés hello que vous intéresse :</span><span class="sxs-lookup"><span data-stu-id="b1288-266">You can flatten it by choosing hello properties you're interested in:</span></span>

```AIQL

    exceptions | take 10
    | extend method1 = tostring(details[0].parsedStack[1].method)
```

<span data-ttu-id="b1288-267">Notez que vous devez toocast hello résultat toohello approprié de type.</span><span class="sxs-lookup"><span data-stu-id="b1288-267">Note that you need toocast hello result toohello appropriate type.</span></span>


## <a name="custom-properties-and-measurements"></a><span data-ttu-id="b1288-268">Mesures et propriétés personnalisées</span><span class="sxs-lookup"><span data-stu-id="b1288-268">Custom properties and measurements</span></span>
<span data-ttu-id="b1288-269">Si votre application se connecte [dimensions personnalisées (propriétés) et des mesures personnalisées](app-insights-api-custom-events-metrics.md#properties) tooevents, puis vous les voyez dans hello `customDimensions` et `customMeasurements` objets.</span><span class="sxs-lookup"><span data-stu-id="b1288-269">If your application attaches [custom dimensions (properties) and custom measurements](app-insights-api-custom-events-metrics.md#properties) tooevents, then you will see them in hello `customDimensions` and `customMeasurements` objects.</span></span>

<span data-ttu-id="b1288-270">Par exemple, si votre application inclut :</span><span class="sxs-lookup"><span data-stu-id="b1288-270">For example, if your app includes:</span></span>

```C#

    var dimensions = new Dictionary<string, string>
                     {{"p1", "v1"},{"p2", "v2"}};
    var measurements = new Dictionary<string, double>
                     {{"m1", 42.0}, {"m2", 43.2}};
    telemetryClient.TrackEvent("myEvent", dimensions, measurements);
```

<span data-ttu-id="b1288-271">tooextract ces valeurs dans Analytique :</span><span class="sxs-lookup"><span data-stu-id="b1288-271">tooextract these values in Analytics:</span></span>

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      m1 = todouble(customMeasurements.m1) // cast tooexpected type

```

<span data-ttu-id="b1288-272">tooverify si une dimension personnalisée est d’un type particulier :</span><span class="sxs-lookup"><span data-stu-id="b1288-272">tooverify whether a custom dimension is of a particular type:</span></span>

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      iff(notnull(todouble(customMeasurements.m1)), ...
```

## <a name="dashboards"></a><span data-ttu-id="b1288-273">Tableaux de bord</span><span class="sxs-lookup"><span data-stu-id="b1288-273">Dashboards</span></span>
<span data-ttu-id="b1288-274">Vous pouvez épingler votre tableau de bord de tooa de résultats dans l’ordre toobring ensemble toutes vos tables et graphiques plus importantes.</span><span class="sxs-lookup"><span data-stu-id="b1288-274">You can pin your results tooa dashboard in order toobring together all your most important charts and tables.</span></span>

* <span data-ttu-id="b1288-275">[Tableau de bord partagé Azure](app-insights-dashboards.md#share-dashboards): cliquez sur l’icône d’épingle hello.</span><span class="sxs-lookup"><span data-stu-id="b1288-275">[Azure shared dashboard](app-insights-dashboards.md#share-dashboards): Click hello pin icon.</span></span> <span data-ttu-id="b1288-276">Avant cela, vous devez disposer d’un tableau de bord partagé.</span><span class="sxs-lookup"><span data-stu-id="b1288-276">Before you do this, you must have a shared dashboard.</span></span> <span data-ttu-id="b1288-277">Bonjour portail Azure, ouvrez ou créez un tableau de bord, puis cliquez sur Partager.</span><span class="sxs-lookup"><span data-stu-id="b1288-277">In hello Azure portal, open or create a dashboard and click Share.</span></span>
* <span data-ttu-id="b1288-278">[Tableau de bord Power BI](app-insights-export-power-bi.md) : cliquez sur Exporter, Requête Power BI.</span><span class="sxs-lookup"><span data-stu-id="b1288-278">[Power BI dashboard](app-insights-export-power-bi.md): Click Export, Power BI Query.</span></span> <span data-ttu-id="b1288-279">L’avantage de cette solution est que vous pouvez afficher votre requête avec d’autres résultats issus d’un large éventail de sources.</span><span class="sxs-lookup"><span data-stu-id="b1288-279">An advantage of this alternative is that you can display your query alongside other results from a wide range of sources.</span></span>

## <a name="combine-with-imported-data"></a><span data-ttu-id="b1288-280">Combiner avec des données importées</span><span class="sxs-lookup"><span data-stu-id="b1288-280">Combine with imported data</span></span>

<span data-ttu-id="b1288-281">Analytique rapports superbes sur tableau de bord hello, mais vous pouvez souhaiter tootranslate hello données tooa formulaire digestibles plus.</span><span class="sxs-lookup"><span data-stu-id="b1288-281">Analytics reports look great on hello dashboard, but sometimes you want tootranslate hello data tooa more digestible form.</span></span> <span data-ttu-id="b1288-282">Par exemple, supposons que vos utilisateurs authentifiés sont identifiés dans les données de télémétrie hello par un alias.</span><span class="sxs-lookup"><span data-stu-id="b1288-282">For example, suppose your authenticated users are identified in hello telemetry by an alias.</span></span> <span data-ttu-id="b1288-283">Vous aimeriez tooshow leur réel des noms dans les résultats.</span><span class="sxs-lookup"><span data-stu-id="b1288-283">You'd like tooshow their real names in your results.</span></span> <span data-ttu-id="b1288-284">toodo, vous avez besoin d’un fichier CSV qui mappe les noms réels des toohello alias hello.</span><span class="sxs-lookup"><span data-stu-id="b1288-284">toodo this, you need a CSV file that maps from hello aliases toohello real names.</span></span>

<span data-ttu-id="b1288-285">Vous pouvez importer un fichier de données et l’utiliser comme une des tables standard de hello (demandes, exceptions et ainsi de suite).</span><span class="sxs-lookup"><span data-stu-id="b1288-285">You can import a data file and use it just like any of hello standard tables (requests, exceptions, and so on).</span></span> <span data-ttu-id="b1288-286">Interrogez-la individuellement ou joignez-la à d’autres tables.</span><span class="sxs-lookup"><span data-stu-id="b1288-286">Either query it on its own, or join it with other tables.</span></span> <span data-ttu-id="b1288-287">Par exemple, si vous disposez d’une table nommée usermap, et il a des colonnes `realName` et `userId`, vous pouvez utiliser tootranslate hello `user_AuthenticatedId` de télémétrie des requêtes hello :</span><span class="sxs-lookup"><span data-stu-id="b1288-287">For example, if you have a table named usermap, and it has columns `realName` and `userId`, then you can use it tootranslate hello `user_AuthenticatedId` field in hello request telemetry:</span></span>

```AIQL

    requests
    | where notempty(user_AuthenticatedId)
    | project userId = user_AuthenticatedId
      // get hello realName field from hello usermap table:
    | join kind=leftouter ( usermap ) on userId
      // count transactions by name:
    | summarize count() by realName
```

<span data-ttu-id="b1288-288">tooimport une table, dans le panneau de schéma hello, sous **autres Sources de données**, suivez hello instructions tooadd une nouvelle source de données, en téléchargeant un échantillon de vos données.</span><span class="sxs-lookup"><span data-stu-id="b1288-288">tooimport a table, in hello Schema blade, under **Other Data Sources**, follow hello instructions tooadd a new data source, by uploading a sample of your data.</span></span> <span data-ttu-id="b1288-289">Ensuite, vous pouvez utiliser les tables de tooupload de cette définition.</span><span class="sxs-lookup"><span data-stu-id="b1288-289">Then you can use this definition tooupload tables.</span></span>

<span data-ttu-id="b1288-290">fonctionnalité d’importation Hello étant actuellement en version préliminaire, vous verrez initialement un lien « Contactez-nous » sous « Autres sources de données ».</span><span class="sxs-lookup"><span data-stu-id="b1288-290">hello import feature is currently in preview, so you will initially see a "Contact us" link under "Other data sources."</span></span> <span data-ttu-id="b1288-291">Utilisez cette toosign de programme d’évaluation toohello et lien de hello est alors remplacé par un bouton « Ajouter une nouvelle source de données ».</span><span class="sxs-lookup"><span data-stu-id="b1288-291">Use this toosign up toohello preview program, and hello link will then be replaced by an "Add new data source" button.</span></span>


## <a name="tables"></a><span data-ttu-id="b1288-292">Tables</span><span class="sxs-lookup"><span data-stu-id="b1288-292">Tables</span></span>
<span data-ttu-id="b1288-293">flux Hello de télémétrie reçu à partir de votre application est accessible par plusieurs tables.</span><span class="sxs-lookup"><span data-stu-id="b1288-293">hello stream of telemetry received from your app is accessible through several tables.</span></span> <span data-ttu-id="b1288-294">schéma Hello des propriétés disponibles pour chaque table est visible à gauche de hello de fenêtre hello.</span><span class="sxs-lookup"><span data-stu-id="b1288-294">hello schema of properties available for each table is visible at hello left of hello window.</span></span>

### <a name="requests-table"></a><span data-ttu-id="b1288-295">Table de requêtes</span><span class="sxs-lookup"><span data-stu-id="b1288-295">Requests table</span></span>
<span data-ttu-id="b1288-296">Nombre de requêtes HTTP tooyour web app et le segment par nom de page :</span><span class="sxs-lookup"><span data-stu-id="b1288-296">Count HTTP requests tooyour web app and segment by page name:</span></span>

![Compter les requêtes segmentées par nom](./media/app-insights-analytics-tour/analytics-count-requests.png)

<span data-ttu-id="b1288-298">Recherche les demandes de hello qui échouent le plus :</span><span class="sxs-lookup"><span data-stu-id="b1288-298">Find hello requests that fail most:</span></span>

![Compter les requêtes segmentées par nom](./media/app-insights-analytics-tour/analytics-failed-requests.png)

### <a name="custom-events-table"></a><span data-ttu-id="b1288-300">Table des événements personnalisés</span><span class="sxs-lookup"><span data-stu-id="b1288-300">Custom events table</span></span>
<span data-ttu-id="b1288-301">Si vous utilisez [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) toosend vos propres événements, vous pouvez les lire à partir de cette table.</span><span class="sxs-lookup"><span data-stu-id="b1288-301">If you use [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) toosend your own events, you can read them from this table.</span></span>

<span data-ttu-id="b1288-302">Prenons un exemple dans lequel le code de votre application contient les lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="b1288-302">Let's take an example where your app code contains these lines:</span></span>

```C#

    telemetry.TrackEvent("Query",
       new Dictionary<string,string> {{"query", sqlCmd}},
       new Dictionary<string,double> {
           {"retry", retryCount},
           {"querytime", totalTime}})
```

<span data-ttu-id="b1288-303">Affichage de la fréquence de hello de ces événements :</span><span class="sxs-lookup"><span data-stu-id="b1288-303">Display hello frequency of these events:</span></span>

![Afficher la fréquence des événements personnalisés](./media/app-insights-analytics-tour/analytics-custom-events-rate.png)

<span data-ttu-id="b1288-305">Extraire les événements hello mesures et dimensions :</span><span class="sxs-lookup"><span data-stu-id="b1288-305">Extract measurements and dimensions from hello events:</span></span>

![Afficher la fréquence des événements personnalisés](./media/app-insights-analytics-tour/analytics-custom-events-dimensions.png)

### <a name="custom-metrics-table"></a><span data-ttu-id="b1288-307">Table des mesures personnalisées</span><span class="sxs-lookup"><span data-stu-id="b1288-307">Custom metrics table</span></span>
<span data-ttu-id="b1288-308">Si vous utilisez [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) toosend vos propres valeurs de mesure, vous trouverez ses résultats dans hello **customMetrics** flux.</span><span class="sxs-lookup"><span data-stu-id="b1288-308">If you are using [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) toosend your own metric values, you’ll find its results in hello **customMetrics** stream.</span></span> <span data-ttu-id="b1288-309">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="b1288-309">For example:</span></span>  

![Mesures personnalisées dans Application Insights Analytics](./media/app-insights-analytics-tour/analytics-custom-metrics.png)

> [!NOTE]
> <span data-ttu-id="b1288-311">Dans [Metrics Explorer](app-insights-metrics-explorer.md), toutes les mesures personnalisées type tooany joint de télémétrie apparaissent ensemble dans Panneau de métriques hello avec envoyé à l’aide de mesures `TrackMetric()`.</span><span class="sxs-lookup"><span data-stu-id="b1288-311">In [Metrics Explorer](app-insights-metrics-explorer.md), all custom measurements attached tooany type of telemetry appear together in hello metrics blade along with metrics sent using `TrackMetric()`.</span></span> <span data-ttu-id="b1288-312">Mais, dans Analytique, des mesures personnalisées sont toujours attachés type toowhichever de télémétrie qu’ils ont été effectuées sur les événements ou les demandes et ainsi de suite - tandis que les métriques envoyés par TrackMetric s’affichent dans leur propre flux de données.</span><span class="sxs-lookup"><span data-stu-id="b1288-312">But in Analytics, custom measurements are still attached toowhichever type of telemetry they were carried on - events or requests, and so on - while metrics sent by TrackMetric appear in their own stream.</span></span>
>
>

### <a name="performance-counters-table"></a><span data-ttu-id="b1288-313">Table des compteurs de performances</span><span class="sxs-lookup"><span data-stu-id="b1288-313">Performance counters table</span></span>
<span data-ttu-id="b1288-314">[Les compteurs de performances](app-insights-performance-counters.md) vous indiquent les métriques système de base pour votre application, notamment le processeur, la mémoire et l’utilisation du réseau.</span><span class="sxs-lookup"><span data-stu-id="b1288-314">[Performance counters](app-insights-performance-counters.md) show you basic system metrics for your app, such as CPU, memory, and network utilization.</span></span> <span data-ttu-id="b1288-315">Vous pouvez configurer hello SDK toosend compteurs supplémentaires, y compris vos propres compteurs personnalisés.</span><span class="sxs-lookup"><span data-stu-id="b1288-315">You can configure hello SDK toosend additional counters, including your own custom counters.</span></span>

<span data-ttu-id="b1288-316">Hello **performanceCounters** schéma expose hello `category`, `counter` nom, et `instance` nom de chaque compteur de performance.</span><span class="sxs-lookup"><span data-stu-id="b1288-316">hello **performanceCounters** schema exposes hello `category`, `counter` name, and `instance` name of each performance counter.</span></span> <span data-ttu-id="b1288-317">Noms d’instance de compteur toosome applicables uniquement les compteurs de performances et indiquent généralement le nom hello de hello processus toowhich hello count est lié.</span><span class="sxs-lookup"><span data-stu-id="b1288-317">Counter instance names are only applicable toosome performance counters, and typically indicate hello name of hello process toowhich hello count relates.</span></span> <span data-ttu-id="b1288-318">Télémétrie hello pour chaque application, vous voyez uniquement les compteurs de hello pour cette application.</span><span class="sxs-lookup"><span data-stu-id="b1288-318">In hello telemetry for each application, you’ll see only hello counters for that application.</span></span> <span data-ttu-id="b1288-319">Par exemple, toosee les compteurs sont disponibles :</span><span class="sxs-lookup"><span data-stu-id="b1288-319">For example, toosee what counters are available:</span></span>

![Compteurs de performances dans Application Insights Analytics](./media/app-insights-analytics-tour/analytics-performance-counters.png)

<span data-ttu-id="b1288-321">tooget un graphique de mémoire disponible sur hello sélectionné période :</span><span class="sxs-lookup"><span data-stu-id="b1288-321">tooget a chart of available memory over hello selected period:</span></span>

![Graphique temporel dans Application Insights Analytics](./media/app-insights-analytics-tour/analytics-available-memory.png)

<span data-ttu-id="b1288-323">Comme les autres données de télémétrie, **performanceCounters** possède également une colonne `cloud_RoleInstance` qui indique l’identité hello de l’ordinateur hôte de hello sur lequel votre application est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="b1288-323">Like other telemetry, **performanceCounters** also has a column `cloud_RoleInstance` that indicates hello identity of hello host machine on which your app is running.</span></span> <span data-ttu-id="b1288-324">Par exemple, toocompare hello des performances de votre application sur des ordinateurs différents hello :</span><span class="sxs-lookup"><span data-stu-id="b1288-324">For example, toocompare hello performance of your app on hello different machines:</span></span>

![Performances segmentées par instances de rôle d’Application Insights Analytics](./media/app-insights-analytics-tour/analytics-metrics-role-instance.png)

### <a name="exceptions-table"></a><span data-ttu-id="b1288-326">Table des exceptions</span><span class="sxs-lookup"><span data-stu-id="b1288-326">Exceptions table</span></span>
<span data-ttu-id="b1288-327">[Les exceptions signalées par votre application](app-insights-asp-net-exceptions.md) sont disponibles dans cette table.</span><span class="sxs-lookup"><span data-stu-id="b1288-327">[Exceptions reported by your app](app-insights-asp-net-exceptions.md) are available in this table.</span></span>

<span data-ttu-id="b1288-328">toofind hello demande HTTP qui gère votre application lorsque hello exception a été levée, joindre sur identifiant_opération :</span><span class="sxs-lookup"><span data-stu-id="b1288-328">toofind hello HTTP request that your app was handling when hello exception was raised, join on operation_Id:</span></span>

![Ajoutez des exceptions avec des requêtes operation_Id](./media/app-insights-analytics-tour/analytics-exception-request.png)

### <a name="browser-timings-table"></a><span data-ttu-id="b1288-330">Table des délais de chargement dans le navigateur</span><span class="sxs-lookup"><span data-stu-id="b1288-330">Browser timings table</span></span>
<span data-ttu-id="b1288-331">`browserTimings` affiche les données de chargement de pages collectées dans les navigateurs de vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="b1288-331">`browserTimings` shows page load data collected in your users' browsers.</span></span>

<span data-ttu-id="b1288-332">[Configurer votre application pour les données de télémétrie côté client](app-insights-javascript.md) commander toosee ces mesures.</span><span class="sxs-lookup"><span data-stu-id="b1288-332">[Set up your app for client-side telemetry](app-insights-javascript.md) in order toosee these metrics.</span></span>

<span data-ttu-id="b1288-333">schéma de Hello inclut [métriques indiquant les longueurs de hello des différentes étapes du processus de chargement de la page hello](app-insights-javascript.md#page-load-performance).</span><span class="sxs-lookup"><span data-stu-id="b1288-333">hello schema includes [metrics indicating hello lengths of different stages of hello page loading process](app-insights-javascript.md#page-load-performance).</span></span> <span data-ttu-id="b1288-334">(Ils n’indiquent pas la durée hello que vos utilisateurs lire une page.)</span><span class="sxs-lookup"><span data-stu-id="b1288-334">(They don’t indicate hello length of time your users read a page.)</span></span>  

<span data-ttu-id="b1288-335">Afficher popularities hello de différentes pages et temps pour chaque page de chargement :</span><span class="sxs-lookup"><span data-stu-id="b1288-335">Show hello popularities of different pages, and load times for each page:</span></span>

![Délai de chargement de page dans Analytics](./media/app-insights-analytics-tour/analytics-page-load.png)

### <a name="availability-results-table"></a><span data-ttu-id="b1288-337">Tableau de résultats de la disponibilité</span><span class="sxs-lookup"><span data-stu-id="b1288-337">Availability results table</span></span>
<span data-ttu-id="b1288-338">`availabilityResults`affiche hello les résultats de votre [tests web](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="b1288-338">`availabilityResults` shows hello results of your [web tests](app-insights-monitor-web-app-availability.md).</span></span> <span data-ttu-id="b1288-339">Chaque exécution de vos tests à partir de chaque emplacement est déclarée séparément.</span><span class="sxs-lookup"><span data-stu-id="b1288-339">Each run of your tests from each test location is reported separately.</span></span>

![Délai de chargement de page dans Analytics](./media/app-insights-analytics-tour/analytics-availability.png)

### <a name="dependencies-table"></a><span data-ttu-id="b1288-341">Table des dépendances</span><span class="sxs-lookup"><span data-stu-id="b1288-341">Dependencies table</span></span>
<span data-ttu-id="b1288-342">Contient les résultats des appels de que votre application effectue des toodatabases et API REST appelle tooTrackDependency().</span><span class="sxs-lookup"><span data-stu-id="b1288-342">Contains results of calls that your app makes toodatabases and REST APIs, and other calls tooTrackDependency().</span></span> <span data-ttu-id="b1288-343">Inclut également les appels AJAX effectuées à partir du navigateur de hello.</span><span class="sxs-lookup"><span data-stu-id="b1288-343">Also includes AJAX calls made from hello browser.</span></span>

<span data-ttu-id="b1288-344">Appels AJAX à partir du navigateur de hello :</span><span class="sxs-lookup"><span data-stu-id="b1288-344">AJAX calls from hello browser:</span></span>

```AIQL

    dependencies | where client_Type == "Browser"
    | take 10
```

<span data-ttu-id="b1288-345">Appels de dépendance à partir du serveur de hello :</span><span class="sxs-lookup"><span data-stu-id="b1288-345">Dependency calls from hello server:</span></span>

```AIQL

    dependencies | where client_Type == "PC"
    | take 10
```

<span data-ttu-id="b1288-346">Toujours affichent les résultats de la dépendance du côté serveur `success==False` si hello Application Insights Agent n’est pas installé.</span><span class="sxs-lookup"><span data-stu-id="b1288-346">Server-side dependency results always show `success==False` if hello Application Insights Agent is not installed.</span></span> <span data-ttu-id="b1288-347">Toutefois, hello autres données sont correctes.</span><span class="sxs-lookup"><span data-stu-id="b1288-347">However, hello other data are correct.</span></span>

### <a name="traces-table"></a><span data-ttu-id="b1288-348">Table des traces</span><span class="sxs-lookup"><span data-stu-id="b1288-348">Traces table</span></span>
<span data-ttu-id="b1288-349">Contient les données de télémétrie hello envoyées par votre application à l’aide de TrackTrace(), ou [autres infrastructures de journalisation](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="b1288-349">Contains hello telemetry sent by your app using TrackTrace(), or [other logging frameworks](app-insights-asp-net-trace-logs.md).</span></span>

## <a name="video"></a><span data-ttu-id="b1288-350">Vidéo</span><span class="sxs-lookup"><span data-stu-id="b1288-350">Video</span></span> 

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

<span data-ttu-id="b1288-351">Requêtes avancées :</span><span class="sxs-lookup"><span data-stu-id="b1288-351">Advanced queries:</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Build/2016/P591/player]


## <a name="next-steps"></a><span data-ttu-id="b1288-352">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b1288-352">Next steps</span></span>
* [<span data-ttu-id="b1288-353">Référence sur le langage Analytics</span><span class="sxs-lookup"><span data-stu-id="b1288-353">Analytics language reference</span></span>](app-insights-analytics-reference.md)
* <span data-ttu-id="b1288-354">[Feuille de graphique SQL utilisateurs](https://aka.ms/sql-analytics) traduit idiomes courants de hello.</span><span class="sxs-lookup"><span data-stu-id="b1288-354">[SQL-users' cheat sheet](https://aka.ms/sql-analytics) translates hello most common idioms.</span></span>

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]
