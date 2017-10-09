---
title: "aaaApplication API d’aperçu pour les événements personnalisés et les métriques | Documents Microsoft"
description: "Insérer quelques lignes de code dans votre utilisation tootrack périphérique ou application de bureau, page Web ou service et diagnostiquer les problèmes."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 80400495-c67b-4468-a92e-abf49793a54d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/17/2017
ms.author: bwren
ms.openlocfilehash: f3d207a47bb4825efda806a19dd0c26540db7bdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-api-for-custom-events-and-metrics"></a><span data-ttu-id="db191-103">API Application Insights pour les événements et les mesures personnalisés</span><span class="sxs-lookup"><span data-stu-id="db191-103">Application Insights API for custom events and metrics</span></span>

<span data-ttu-id="db191-104">Insérer quelques lignes de code dans votre toofind d’application à ce que les utilisateurs sont en servent, ou toohelp diagnostiquer les problèmes.</span><span class="sxs-lookup"><span data-stu-id="db191-104">Insert a few lines of code in your application toofind out what users are doing with it, or toohelp diagnose issues.</span></span> <span data-ttu-id="db191-105">Vous pouvez envoyer la télémétrie depuis des applications de périphérique et de bureau, des clients web et des serveurs web.</span><span class="sxs-lookup"><span data-stu-id="db191-105">You can send telemetry from device and desktop apps, web clients, and web servers.</span></span> <span data-ttu-id="db191-106">Hello d’utilisation [Azure Application Insights](app-insights-overview.md) vos propres versions de télémétrie standard et des métriques et des événements personnalisés de toosend API de télémétrie de base.</span><span class="sxs-lookup"><span data-stu-id="db191-106">Use hello [Azure Application Insights](app-insights-overview.md) core telemetry API toosend custom events and metrics, and your own versions of standard telemetry.</span></span> <span data-ttu-id="db191-107">Cette API est hello même API standard hello utilisent des collecteurs de données d’Application Insights.</span><span class="sxs-lookup"><span data-stu-id="db191-107">This API is hello same API that hello standard Application Insights data collectors use.</span></span>

## <a name="api-summary"></a><span data-ttu-id="db191-108">Résumé des API</span><span class="sxs-lookup"><span data-stu-id="db191-108">API summary</span></span>
<span data-ttu-id="db191-109">Hello API est uniforme sur toutes les plateformes, indépendamment des quelques légères variantes.</span><span class="sxs-lookup"><span data-stu-id="db191-109">hello API is uniform across all platforms, apart from a few small variations.</span></span>

| <span data-ttu-id="db191-110">Méthode</span><span class="sxs-lookup"><span data-stu-id="db191-110">Method</span></span> | <span data-ttu-id="db191-111">Utilisé pour</span><span class="sxs-lookup"><span data-stu-id="db191-111">Used for</span></span> |
| --- | --- |
| [`TrackPageView`](#page-views) |<span data-ttu-id="db191-112">Pages, écrans, panneaux ou formes.</span><span class="sxs-lookup"><span data-stu-id="db191-112">Pages, screens, blades, or forms.</span></span> |
| [`TrackEvent`](#trackevent) |<span data-ttu-id="db191-113">Actions de l’utilisateur et autres événements.</span><span class="sxs-lookup"><span data-stu-id="db191-113">User actions and other events.</span></span> <span data-ttu-id="db191-114">Tootrack utilisé toomonitor comportement ou les performances de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="db191-114">Used tootrack user behavior or toomonitor performance.</span></span> |
| [`TrackMetric`](#trackmetric) |<span data-ttu-id="db191-115">Les mesures de performances telles que les files d’attente les événements de toospecific pas associés.</span><span class="sxs-lookup"><span data-stu-id="db191-115">Performance measurements such as queue lengths not related toospecific events.</span></span> |
| [`TrackException`](#trackexception) |<span data-ttu-id="db191-116">Exceptions de journal pour des diagnostics.</span><span class="sxs-lookup"><span data-stu-id="db191-116">Logging exceptions for diagnosis.</span></span> <span data-ttu-id="db191-117">Suivi lorsqu’ils se produisent dans les événements de relation tooother et examinez les traces de pile.</span><span class="sxs-lookup"><span data-stu-id="db191-117">Trace where they occur in relation tooother events and examine stack traces.</span></span> |
| [`TrackRequest`](#trackrequest) |<span data-ttu-id="db191-118">Fréquence de hello et la durée des demandes de serveur pour l’analyse des performances de la journalisation.</span><span class="sxs-lookup"><span data-stu-id="db191-118">Logging hello frequency and duration of server requests for performance analysis.</span></span> |
| [`TrackTrace`](#tracktrace) |<span data-ttu-id="db191-119">Messages du journal de diagnostic</span><span class="sxs-lookup"><span data-stu-id="db191-119">Diagnostic log messages.</span></span> <span data-ttu-id="db191-120">Vous pouvez également capturer des journaux tiers.</span><span class="sxs-lookup"><span data-stu-id="db191-120">You can also capture third-party logs.</span></span> |
| [`TrackDependency`](#trackdependency) |<span data-ttu-id="db191-121">Durée hello de journalisation et la fréquence des composants de tooexternal d’appels qui dépend de votre application.</span><span class="sxs-lookup"><span data-stu-id="db191-121">Logging hello duration and frequency of calls tooexternal components that your app depends on.</span></span> |

<span data-ttu-id="db191-122">Vous pouvez [attacher des propriétés et des mesures](#properties) toomost de ces appels de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="db191-122">You can [attach properties and metrics](#properties) toomost of these telemetry calls.</span></span>

## <span data-ttu-id="db191-123"><a name="prep"></a>Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="db191-123"><a name="prep"></a>Before you start</span></span>
<span data-ttu-id="db191-124">Si vous n’avez pas encore de référence sur le kit SDK Application Insights :</span><span class="sxs-lookup"><span data-stu-id="db191-124">If you don't have a reference on Application Insights SDK yet:</span></span>

* <span data-ttu-id="db191-125">Ajouter hello Application Insights SDK tooyour projet :</span><span class="sxs-lookup"><span data-stu-id="db191-125">Add hello Application Insights SDK tooyour project:</span></span>

  * [<span data-ttu-id="db191-126">Projet ASP.NET</span><span class="sxs-lookup"><span data-stu-id="db191-126">ASP.NET project</span></span>](app-insights-asp-net.md)
  * [<span data-ttu-id="db191-127">Projet Java</span><span class="sxs-lookup"><span data-stu-id="db191-127">Java project</span></span>](app-insights-java-get-started.md)
  * [<span data-ttu-id="db191-128">JavaScript dans chaque page web</span><span class="sxs-lookup"><span data-stu-id="db191-128">JavaScript in each webpage</span></span>](app-insights-javascript.md) 
* <span data-ttu-id="db191-129">Ajoutez au code de votre périphérique ou de votre serveur web :</span><span class="sxs-lookup"><span data-stu-id="db191-129">In your device or web server code, include:</span></span>

    <span data-ttu-id="db191-130">*C# :*`using Microsoft.ApplicationInsights;`</span><span class="sxs-lookup"><span data-stu-id="db191-130">*C#:* `using Microsoft.ApplicationInsights;`</span></span>

    <span data-ttu-id="db191-131">*Visual Basic :*`Imports Microsoft.ApplicationInsights`</span><span class="sxs-lookup"><span data-stu-id="db191-131">*Visual Basic:* `Imports Microsoft.ApplicationInsights`</span></span>

    <span data-ttu-id="db191-132">*Java:*`import com.microsoft.applicationinsights.TelemetryClient;`</span><span class="sxs-lookup"><span data-stu-id="db191-132">*Java:* `import com.microsoft.applicationinsights.TelemetryClient;`</span></span>

## <a name="constructing-a-telemetryclient-instance"></a><span data-ttu-id="db191-133">Construction d’une instance de TelemetryClient</span><span class="sxs-lookup"><span data-stu-id="db191-133">Constructing a TelemetryClient instance</span></span>
<span data-ttu-id="db191-134">Construisez une instance de `TelemetryClient` (sauf en JavaScript dans les pages web) :</span><span class="sxs-lookup"><span data-stu-id="db191-134">Construct an instance of `TelemetryClient` (except in JavaScript in webpages):</span></span>

<span data-ttu-id="db191-135">*C#*</span><span class="sxs-lookup"><span data-stu-id="db191-135">*C#*</span></span>

    private TelemetryClient telemetry = new TelemetryClient();

<span data-ttu-id="db191-136">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="db191-136">*Visual Basic*</span></span>

    Private Dim telemetry As New TelemetryClient

<span data-ttu-id="db191-137">*Java*</span><span class="sxs-lookup"><span data-stu-id="db191-137">*Java*</span></span>

    private TelemetryClient telemetry = new TelemetryClient();

<span data-ttu-id="db191-138">TelemetryClient est thread-safe.</span><span class="sxs-lookup"><span data-stu-id="db191-138">TelemetryClient is thread-safe.</span></span>

<span data-ttu-id="db191-139">Nous vous recommandons d’utiliser une instance de TelemetryClient pour chaque module de votre application.</span><span class="sxs-lookup"><span data-stu-id="db191-139">We recommend that you use an instance of TelemetryClient for each module of your app.</span></span> <span data-ttu-id="db191-140">Par exemple, vous avez peut-être une seule instance TelemetryClient dans vos requêtes HTTP entrantes tooreport web service et l’autre dans un intergiciel (middleware) classe tooreport business les événements de logique.</span><span class="sxs-lookup"><span data-stu-id="db191-140">For instance, you may have one TelemetryClient instance in your web service tooreport incoming HTTP requests, and another in a middleware class tooreport business logic events.</span></span> <span data-ttu-id="db191-141">Vous pouvez définir des propriétés telles que `TelemetryClient.Context.User.Id` tootrack utilisateurs et des sessions, ou `TelemetryClient.Context.Device.Id` machine de hello tooidentify.</span><span class="sxs-lookup"><span data-stu-id="db191-141">You can set properties such as `TelemetryClient.Context.User.Id` tootrack users and sessions, or `TelemetryClient.Context.Device.Id` tooidentify hello machine.</span></span> <span data-ttu-id="db191-142">Ces informations sont les événements attachés tooall hello envoie d’instance.</span><span class="sxs-lookup"><span data-stu-id="db191-142">This information is attached tooall events that hello instance sends.</span></span>

## <a name="trackevent"></a><span data-ttu-id="db191-143">TrackEvent</span><span class="sxs-lookup"><span data-stu-id="db191-143">TrackEvent</span></span>
<span data-ttu-id="db191-144">Dans Application Insights, un *événement personnalisé* est un point de données que vous pouvez afficher dans [Metrics Explorer](app-insights-metrics-explorer.md) en tant que nombre agrégé et dans [Recherche de diagnostic](app-insights-diagnostic-search.md) en tant qu’occurrences individuelles.</span><span class="sxs-lookup"><span data-stu-id="db191-144">In Application Insights, a *custom event* is a data point that you can display in [Metrics Explorer](app-insights-metrics-explorer.md) as an aggregated count, and in [Diagnostic Search](app-insights-diagnostic-search.md) as individual occurrences.</span></span> <span data-ttu-id="db191-145">(Il n’est pas tooMVC connexe ou autres framework « événements ».)</span><span class="sxs-lookup"><span data-stu-id="db191-145">(It isn't related tooMVC or other framework "events.")</span></span>

<span data-ttu-id="db191-146">Insérer `TrackEvent` appelle dans votre code toocount différents événements.</span><span class="sxs-lookup"><span data-stu-id="db191-146">Insert `TrackEvent` calls in your code toocount various events.</span></span> <span data-ttu-id="db191-147">Par exemple, la fréquence à laquelle les utilisateurs choisissent une fonctionnalité particulière, la fréquence à laquelle ils atteignent des objectifs particuliers ou à laquelle ils commettent éventuellement des types d’erreurs particuliers.</span><span class="sxs-lookup"><span data-stu-id="db191-147">How often users choose a particular feature, how often they achieve particular goals, or maybe how often they make particular types of mistakes.</span></span>

<span data-ttu-id="db191-148">Par exemple, dans une application de jeu, vous devez envoyer un événement chaque fois qu’un utilisateur wins jeu de hello :</span><span class="sxs-lookup"><span data-stu-id="db191-148">For example, in a game app, send an event whenever a user wins hello game:</span></span>

<span data-ttu-id="db191-149">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="db191-149">*JavaScript*</span></span>

    appInsights.trackEvent("WinGame");

<span data-ttu-id="db191-150">*C#*</span><span class="sxs-lookup"><span data-stu-id="db191-150">*C#*</span></span>

    telemetry.TrackEvent("WinGame");

<span data-ttu-id="db191-151">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="db191-151">*Visual Basic*</span></span>

    telemetry.TrackEvent("WinGame")

<span data-ttu-id="db191-152">*Java*</span><span class="sxs-lookup"><span data-stu-id="db191-152">*Java*</span></span>

    telemetry.trackEvent("WinGame");

### <a name="view-your-events-in-hello-microsoft-azure-portal"></a><span data-ttu-id="db191-153">Afficher les événements dans le portail de Microsoft Azure hello</span><span class="sxs-lookup"><span data-stu-id="db191-153">View your events in hello Microsoft Azure portal</span></span>
<span data-ttu-id="db191-154">toosee un nombre de vos événements, ouvrez un [Metrics Explorer](app-insights-metrics-explorer.md) panneau, ajouter un nouveau graphique, puis sélectionnez **événements**.</span><span class="sxs-lookup"><span data-stu-id="db191-154">toosee a count of your events, open a [Metrics Explorer](app-insights-metrics-explorer.md) blade, add a new chart, and select **Events**.</span></span>  

![Afficher un nombre d’événements personnalisés](./media/app-insights-api-custom-events-metrics/01-custom.png)

<span data-ttu-id="db191-156">nombres de hello toocompare d’événements, définir le type de graphique hello trop**grille**et de groupe par le nom de l’événement :</span><span class="sxs-lookup"><span data-stu-id="db191-156">toocompare hello counts of different events, set hello chart type too**Grid**, and group by event name:</span></span>

![Définir le type de graphique de hello et regroupement](./media/app-insights-api-custom-events-metrics/07-grid.png)

<span data-ttu-id="db191-158">Sur la grille de hello, cliquez sur un événement nom toosee des occurrences individuelles de cet événement.</span><span class="sxs-lookup"><span data-stu-id="db191-158">On hello grid, click through an event name toosee individual occurrences of that event.</span></span> <span data-ttu-id="db191-159">toosee plus de détails - cliquez sur n’importe quelle occurrence dans la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="db191-159">toosee more detail - click any occurrence in hello list.</span></span>

![Extraire les événements hello](./media/app-insights-api-custom-events-metrics/03-instances.png)

<span data-ttu-id="db191-161">toofocus sur des événements spécifiques dans la recherche ou Metrics Explorer, toohello événement les noms des filtres du panneau ensemble hello qui vous intéresse :</span><span class="sxs-lookup"><span data-stu-id="db191-161">toofocus on specific events in either Search or Metrics Explorer, set hello blade's filter toohello event names that you're interested in:</span></span>

![Ouvrez Filtres, développez Nom de l'événement et sélectionnez une ou plusieurs valeurs](./media/app-insights-api-custom-events-metrics/06-filter.png)

### <a name="custom-events-in-analytics"></a><span data-ttu-id="db191-163">Événements personnalisés dans l’analytique</span><span class="sxs-lookup"><span data-stu-id="db191-163">Custom events in Analytics</span></span>

<span data-ttu-id="db191-164">les données de télémétrie Hello est disponible dans hello `customEvents` table [Application Insights Analytique](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="db191-164">hello telemetry is available in hello `customEvents` table in [Application Insights Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="db191-165">Chaque ligne représente un appel trop`trackEvent(..)` dans votre application.</span><span class="sxs-lookup"><span data-stu-id="db191-165">Each row represents a call too`trackEvent(..)` in your app.</span></span> 

<span data-ttu-id="db191-166">Si [échantillonnage](app-insights-sampling.md) est en opération, la propriété itemCount hello affiche une valeur supérieure à 1.</span><span class="sxs-lookup"><span data-stu-id="db191-166">If [sampling](app-insights-sampling.md) is in operation, hello itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="db191-167">Pour exemple itemCount == 10 signifie que de 10 appels tootrackEvent(), processus d’échantillonnage hello transmises uniquement un d’eux.</span><span class="sxs-lookup"><span data-stu-id="db191-167">For example itemCount==10 means that of 10 calls tootrackEvent(), hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="db191-168">tooget un nombre correct d’événements personnalisés, vous devez utiliser par conséquent utiliser du code comme `customEvent | summarize sum(itemCount)`.</span><span class="sxs-lookup"><span data-stu-id="db191-168">tooget a correct count of custom events, you should use therefore use code such as `customEvent | summarize sum(itemCount)`.</span></span>


## <a name="trackmetric"></a><span data-ttu-id="db191-169">TrackMetric</span><span class="sxs-lookup"><span data-stu-id="db191-169">TrackMetric</span></span>

<span data-ttu-id="db191-170">Application Insights peuvent graphique des métriques qui ne sont pas attachés tooparticular événements.</span><span class="sxs-lookup"><span data-stu-id="db191-170">Application Insights can chart metrics that are not attached tooparticular events.</span></span> <span data-ttu-id="db191-171">Par exemple, vous pouvez analyser la longueur d’une file d'attente à des intervalles réguliers.</span><span class="sxs-lookup"><span data-stu-id="db191-171">For example, you could monitor a queue length at regular intervals.</span></span> <span data-ttu-id="db191-172">Avec des mesures, des mesures individuelles hello sont moins importantes que les variations hello et les tendances et graphiques par conséquent, les statistiques sont utiles.</span><span class="sxs-lookup"><span data-stu-id="db191-172">With metrics, hello individual measurements are of less interest than hello variations and trends, and so statistical charts are useful.</span></span>

<span data-ttu-id="db191-173">Dans commande toosend métriques tooApplication Insights, vous pouvez utiliser hello `TrackMetric(..)` API.</span><span class="sxs-lookup"><span data-stu-id="db191-173">In order toosend metrics tooApplication Insights, you can use hello `TrackMetric(..)` API.</span></span> <span data-ttu-id="db191-174">Il existe deux façons toosend une mesure de :</span><span class="sxs-lookup"><span data-stu-id="db191-174">There are two ways toosend a metric:</span></span> 

* <span data-ttu-id="db191-175">Valeur unique.</span><span class="sxs-lookup"><span data-stu-id="db191-175">Single value.</span></span> <span data-ttu-id="db191-176">Chaque fois que vous effectuez une mesure dans votre application, vous envoyez valeur hello tooApplication Insights.</span><span class="sxs-lookup"><span data-stu-id="db191-176">Every time you perform a measurement in your application, you send hello corresponding value tooApplication Insights.</span></span> <span data-ttu-id="db191-177">Par exemple, supposons que vous disposez d’une mesure de nombre hello d’éléments dans un conteneur.</span><span class="sxs-lookup"><span data-stu-id="db191-177">For example, assume that you have a metric describing hello number of items in a container.</span></span> <span data-ttu-id="db191-178">Pendant une période donnée, vous commencez par mettre trois éléments dans le conteneur de hello, puis vous supprimez deux éléments.</span><span class="sxs-lookup"><span data-stu-id="db191-178">During a particular time period, you first put three items into hello container and then you remove two items.</span></span> <span data-ttu-id="db191-179">En conséquence, vous appelez `TrackMetric` à deux reprises : tout d’abord en passant la valeur de hello `3` et puis hello valeur `-2`.</span><span class="sxs-lookup"><span data-stu-id="db191-179">Accordingly, you would call `TrackMetric` twice: first passing hello value `3` and then hello value `-2`.</span></span> <span data-ttu-id="db191-180">Application Insights stocke les deux valeurs pour votre compte.</span><span class="sxs-lookup"><span data-stu-id="db191-180">Application Insights stores both values on your behalf.</span></span> 

* <span data-ttu-id="db191-181">Agrégation.</span><span class="sxs-lookup"><span data-stu-id="db191-181">Aggregation.</span></span> <span data-ttu-id="db191-182">Quand vous travaillez avec des métriques, chaque mesure individuelle est rarement intéressante.</span><span class="sxs-lookup"><span data-stu-id="db191-182">When working with metrics, every single measurement is rarely of interest.</span></span> <span data-ttu-id="db191-183">Au lieu de cela, un récapitulatif de ce qui s’est passé au cours d’une période donnée est important.</span><span class="sxs-lookup"><span data-stu-id="db191-183">Instead a summary of what happened during a particular time period is important.</span></span> <span data-ttu-id="db191-184">Un tel récapitulatif est appelé _agrégation_.</span><span class="sxs-lookup"><span data-stu-id="db191-184">Such a summary is called _aggregation_.</span></span> <span data-ttu-id="db191-185">Bonjour exemple ci-dessus, hello métrique somme pour cette période est `1` et hello de valeurs de mesure hello est `2`.</span><span class="sxs-lookup"><span data-stu-id="db191-185">In hello above example, hello aggregate metric sum for that time period is `1` and hello count of hello metric values is `2`.</span></span> <span data-ttu-id="db191-186">Lorsque vous utilisez l’approche d’agrégation hello, vous appelez uniquement `TrackMetric` une fois toutes les valeurs d’agrégation hello envoi et de période de temps.</span><span class="sxs-lookup"><span data-stu-id="db191-186">When using hello aggregation approach, you only invoke `TrackMetric` once per time period and send hello aggregate values.</span></span> <span data-ttu-id="db191-187">Il s’agit de hello approche recommandée étant donné qu’elle peut réduire considérablement le coût de hello et performances surcharge par envoi de données moins tooApplication Insights, lors de la collecte de toujours toutes les informations pertinentes.</span><span class="sxs-lookup"><span data-stu-id="db191-187">This is hello recommended approach since it can significantly reduce hello cost and performance overhead by sending fewer data points tooApplication Insights, while still collecting all relevant information.</span></span>

### <a name="examples"></a><span data-ttu-id="db191-188">Exemples :</span><span class="sxs-lookup"><span data-stu-id="db191-188">Examples:</span></span>

#### <a name="single-values"></a><span data-ttu-id="db191-189">Valeurs uniques</span><span class="sxs-lookup"><span data-stu-id="db191-189">Single values</span></span>

<span data-ttu-id="db191-190">toosend une valeur métrique unique :</span><span class="sxs-lookup"><span data-stu-id="db191-190">toosend a single metric value:</span></span>

<span data-ttu-id="db191-191">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="db191-191">*JavaScript*</span></span>

 ```Javascript
     appInsights.trackMetric("queueLength", 42.0);
 ```

<span data-ttu-id="db191-192">*C#, Java*</span><span class="sxs-lookup"><span data-stu-id="db191-192">*C#, Java*</span></span>

```C#
    var sample = new MetricTelemetry();
    sample.Name = "metric name";
    sample.Value = 42.3;
    telemetryClient.TrackMetric(sample);
```

#### <a name="aggregating-metrics"></a><span data-ttu-id="db191-193">Agrégation des métriques</span><span class="sxs-lookup"><span data-stu-id="db191-193">Aggregating metrics</span></span>

<span data-ttu-id="db191-194">Il est recommandé de métriques de tooaggregate avant de les envoyer à partir de votre application, de la bande passante tooreduce, de coût et tooimprove les performances.</span><span class="sxs-lookup"><span data-stu-id="db191-194">It is recommended tooaggregate metrics before sending them from your app, tooreduce bandwidth, cost and tooimprove performance.</span></span>
<span data-ttu-id="db191-195">Voici un exemple de code d’agrégation :</span><span class="sxs-lookup"><span data-stu-id="db191-195">Here is an example of aggregating code:</span></span>

<span data-ttu-id="db191-196">*C#*</span><span class="sxs-lookup"><span data-stu-id="db191-196">*C#*</span></span>

```C#
using System;
using System.Threading;
using System.Threading.Tasks;

using Microsoft.ApplicationInsights;
using Microsoft.ApplicationInsights.DataContracts;

namespace MetricAggregationExample
{
    /// <summary>
    /// Aggregates metric values for a single time period.
    /// </summary>
    internal class MetricAggregator
    {
        private SpinLock _trackLock = new SpinLock();

        public DateTimeOffset StartTimestamp    { get; }
        public int Count                        { get; private set; }
        public double Sum                       { get; private set; }
        public double SumOfSquares              { get; private set; }
        public double Min                       { get; private set; }
        public double Max                       { get; private set; }
        public double Average                   { get { return (Count == 0) ? 0 : (Sum / Count); } }
        public double Variance                  { get { return (Count == 0) ? 0 : (SumOfSquares / Count)
                                                                                  - (Average * Average); } }
        public double StandardDeviation         { get { return Math.Sqrt(Variance); } }

        public MetricAggregator(DateTimeOffset startTimestamp)
        {
            this.StartTimestamp = startTimestamp;
        }

        public void TrackValue(double value)
        {
            bool lockAcquired = false;

            try
            {
                _trackLock.Enter(ref lockAcquired);

                if ((Count == 0) || (value < Min))  { Min = value; }
                if ((Count == 0) || (value > Max))  { Max = value; }
                Count++;
                Sum += value;
                SumOfSquares += value * value;
            }
            finally
            {
                if (lockAcquired)
                {
                    _trackLock.Exit();
                }
            }
        }
    }   // internal class MetricAggregator

    /// <summary>
    /// Accepts metric values and sends hello aggregated values at 1-minute intervals.
    /// </summary>
    public sealed class Metric : IDisposable
    {
        private static readonly TimeSpan AggregationPeriod = TimeSpan.FromSeconds(60);

        private bool _isDisposed = false;
        private MetricAggregator _aggregator = null;
        private readonly TelemetryClient _telemetryClient;

        public string Name { get; }

        public Metric(string name, TelemetryClient telemetryClient)
        {
            this.Name = name ?? "null";
            this._aggregator = new MetricAggregator(DateTimeOffset.UtcNow);
            this._telemetryClient = telemetryClient ?? throw new ArgumentNullException(nameof(telemetryClient));

            Task.Run(this.AggregatorLoopAsync);
        }

        public void TrackValue(double value)
        {
            MetricAggregator currAggregator = _aggregator;
            if (currAggregator != null)
            {
                currAggregator.TrackValue(value);
            }
        }

        private async Task AggregatorLoopAsync()
        {
            while (_isDisposed == false)
            {
                try
                {
                    // Wait for end end of hello aggregation period:
                    await Task.Delay(AggregationPeriod).ConfigureAwait(continueOnCapturedContext: false);

                    // Atomically snap hello current aggregation:
                    MetricAggregator nextAggregator = new MetricAggregator(DateTimeOffset.UtcNow);
                    MetricAggregator prevAggregator = Interlocked.Exchange(ref _aggregator, nextAggregator);

                    // Only send anything is at least one value was measured:
                    if (prevAggregator != null && prevAggregator.Count > 0)
                    {
                        // Compute hello actual aggregation period length:
                        TimeSpan aggPeriod = nextAggregator.StartTimestamp - prevAggregator.StartTimestamp;
                        if (aggPeriod.TotalMilliseconds < 1)
                        {
                            aggPeriod = TimeSpan.FromMilliseconds(1);
                        }

                        // Construct hello metric telemetry item and send:
                        var aggregatedMetricTelemetry = new MetricTelemetry(
                                Name,
                                prevAggregator.Count,
                                prevAggregator.Sum,
                                prevAggregator.Min,
                                prevAggregator.Max,
                                prevAggregator.StandardDeviation);
                        aggregatedMetricTelemetry.Properties["AggregationPeriod"] = aggPeriod.ToString("c");

                        _telemetryClient.Track(aggregatedMetricTelemetry);
                    }
                }
                catch(Exception ex)
                {
                    // log ex as appropriate for your application
                }
            }
        }

        void IDisposable.Dispose()
        {
            _isDisposed = true;
            _aggregator = null;
        }
    }   // public sealed class Metric
}
```

### <a name="custom-metrics-in-metrics-explorer"></a><span data-ttu-id="db191-197">Métriques personnalisées dans Metrics Explorer</span><span class="sxs-lookup"><span data-stu-id="db191-197">Custom metrics in Metrics Explorer</span></span>

<span data-ttu-id="db191-198">résultats de hello toosee, ouvrez l’Explorateur de métriques et ajouter un nouveau graphique.</span><span class="sxs-lookup"><span data-stu-id="db191-198">toosee hello results, open Metrics Explorer and add a new chart.</span></span> <span data-ttu-id="db191-199">Modifier hello graphique tooshow votre mesure.</span><span class="sxs-lookup"><span data-stu-id="db191-199">Edit hello chart tooshow your metric.</span></span>

> [!NOTE]
> <span data-ttu-id="db191-200">Votre métrique personnalisée peut prendre plusieurs minutes tooappear liste hello de métriques disponibles.</span><span class="sxs-lookup"><span data-stu-id="db191-200">Your custom metric might take several minutes tooappear in hello list of available metrics.</span></span>
>

![Ajouter un nouveau graphique ou sélectionnez un graphique et sélectionnez votre métrique sous Personnalisé](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

### <a name="custom-metrics-in-analytics"></a><span data-ttu-id="db191-202">Métriques personnalisées dans Analytics</span><span class="sxs-lookup"><span data-stu-id="db191-202">Custom metrics in Analytics</span></span>

<span data-ttu-id="db191-203">les données de télémétrie Hello est disponible dans hello `customMetrics` table [Application Insights Analytique](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="db191-203">hello telemetry is available in hello `customMetrics` table in [Application Insights Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="db191-204">Chaque ligne représente un appel trop`trackMetric(..)` dans votre application.</span><span class="sxs-lookup"><span data-stu-id="db191-204">Each row represents a call too`trackMetric(..)` in your app.</span></span>
* <span data-ttu-id="db191-205">`valueSum`-C’est la somme de hello des mesures de hello.</span><span class="sxs-lookup"><span data-stu-id="db191-205">`valueSum` - This is hello sum of hello measurements.</span></span> <span data-ttu-id="db191-206">valeur moyenne tooget hello, de division par `valueCount`.</span><span class="sxs-lookup"><span data-stu-id="db191-206">tooget hello mean value, divide by `valueCount`.</span></span>
* <span data-ttu-id="db191-207">`valueCount`-hello du nombre de mesures qui ont été regroupés dans ce `trackMetric(..)` appeler.</span><span class="sxs-lookup"><span data-stu-id="db191-207">`valueCount` - hello number of measurements that were aggregated into this `trackMetric(..)` call.</span></span>

## <a name="page-views"></a><span data-ttu-id="db191-208">Affichages de page</span><span class="sxs-lookup"><span data-stu-id="db191-208">Page views</span></span>
<span data-ttu-id="db191-209">Dans un périphérique ou une application de page web, la télémétrie d'affichage de page est envoyée par défaut lorsque chaque écran ou page est chargé.</span><span class="sxs-lookup"><span data-stu-id="db191-209">In a device or webpage app, page view telemetry is sent by default when each screen or page is loaded.</span></span> <span data-ttu-id="db191-210">Mais vous pouvez modifier les vues de cette page tootrack à des moments supplémentaires ou différents.</span><span class="sxs-lookup"><span data-stu-id="db191-210">But you can change that tootrack page views at additional or different times.</span></span> <span data-ttu-id="db191-211">Par exemple, dans une application qui affiche les onglets ou les panneaux, vous pourriez tootrack une page chaque fois que l’utilisateur de hello ouvre un nouveau panneau.</span><span class="sxs-lookup"><span data-stu-id="db191-211">For example, in an app that displays tabs or blades, you might want tootrack a page whenever hello user opens a new blade.</span></span>

![Filtre d'utilisation dans le panneau Vue d'ensemble](./media/app-insights-api-custom-events-metrics/appinsights-47usage-2.png)

<span data-ttu-id="db191-213">Les données utilisateur et la session sont envoyées comme propriétés ainsi que les vues de page, hello donc graphiques utilisateur et session vivantes lors de la télémétrie des consultations de page.</span><span class="sxs-lookup"><span data-stu-id="db191-213">User and session data is sent as properties along with page views, so hello user and session charts come alive when there is page view telemetry.</span></span>

### <a name="custom-page-views"></a><span data-ttu-id="db191-214">Affichages de pages personnalisées</span><span class="sxs-lookup"><span data-stu-id="db191-214">Custom page views</span></span>
<span data-ttu-id="db191-215">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="db191-215">*JavaScript*</span></span>

    appInsights.trackPageView("tab1");

<span data-ttu-id="db191-216">*C#*</span><span class="sxs-lookup"><span data-stu-id="db191-216">*C#*</span></span>

    telemetry.TrackPageView("GameReviewPage");

<span data-ttu-id="db191-217">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="db191-217">*Visual Basic*</span></span>

    telemetry.TrackPageView("GameReviewPage")


<span data-ttu-id="db191-218">Si vous avez plusieurs onglets dans différentes pages HTML, vous pouvez spécifier des URL de hello trop :</span><span class="sxs-lookup"><span data-stu-id="db191-218">If you have several tabs within different HTML pages, you can specify hello URL too:</span></span>

    appInsights.trackPageView("tab1", "http://fabrikam.com/page1.htm");

### <a name="timing-page-views"></a><span data-ttu-id="db191-219">Affichages de la page de durée</span><span class="sxs-lookup"><span data-stu-id="db191-219">Timing page views</span></span>
<span data-ttu-id="db191-220">Par défaut, les temps de hello déclarés en tant que **temps de chargement de Page vue** sont mesurées à partir de lorsque le navigateur de hello envoie la demande de hello, jusqu'à ce que l’événement de chargement de page du navigateur hello est appelée.</span><span class="sxs-lookup"><span data-stu-id="db191-220">By default, hello times reported as **Page view load time** are measured from when hello browser sends hello request, until hello browser's page load event is called.</span></span>

<span data-ttu-id="db191-221">Au lieu de cela, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="db191-221">Instead, you can either:</span></span>

* <span data-ttu-id="db191-222">Définir une durée explicite dans hello [trackPageView](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#trackpageview) appeler : `appInsights.trackPageView("tab1", null, null, null, durationInMilliseconds);`.</span><span class="sxs-lookup"><span data-stu-id="db191-222">Set an explicit duration in hello [trackPageView](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#trackpageview) call: `appInsights.trackPageView("tab1", null, null, null, durationInMilliseconds);`.</span></span>
* <span data-ttu-id="db191-223">Utiliser les appels de minutage hello page vue `startTrackPage` et `stopTrackPage`.</span><span class="sxs-lookup"><span data-stu-id="db191-223">Use hello page view timing calls `startTrackPage` and `stopTrackPage`.</span></span>

<span data-ttu-id="db191-224">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="db191-224">*JavaScript*</span></span>

    // toostart timing a page:
    appInsights.startTrackPage("Page1");

<span data-ttu-id="db191-225">...</span><span class="sxs-lookup"><span data-stu-id="db191-225">...</span></span>

    // toostop timing and log hello page:
    appInsights.stopTrackPage("Page1", url, properties, measurements);

<span data-ttu-id="db191-226">Hello nom que vous utilisez comme premier paramètre de hello associe le début de hello et arrêter des appels.</span><span class="sxs-lookup"><span data-stu-id="db191-226">hello name that you use as hello first parameter associates hello start and stop calls.</span></span> <span data-ttu-id="db191-227">Nom de la page actuelle toohello la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="db191-227">It defaults toohello current page name.</span></span>

<span data-ttu-id="db191-228">intervalle hello entre hello proviennent des durées affichées dans Metrics Explorer le chargement des pages qui en résulte Hello démarrer et arrêter des appels.</span><span class="sxs-lookup"><span data-stu-id="db191-228">hello resulting page load durations displayed in Metrics Explorer are derived from hello interval between hello start and stop calls.</span></span> <span data-ttu-id="db191-229">C’est tooyou quel intervalle de temps réellement.</span><span class="sxs-lookup"><span data-stu-id="db191-229">It's up tooyou what interval you actually time.</span></span>

### <a name="page-telemetry-in-analytics"></a><span data-ttu-id="db191-230">Télémétrie des pages dans Analytique</span><span class="sxs-lookup"><span data-stu-id="db191-230">Page telemetry in Analytics</span></span>

<span data-ttu-id="db191-231">Dans [Analytique](app-insights-analytics.md), deux tables affichent les données des opérations du navigateur :</span><span class="sxs-lookup"><span data-stu-id="db191-231">In [Analytics](app-insights-analytics.md) two tables show data from browser operations:</span></span>

* <span data-ttu-id="db191-232">Hello `pageViews` table contient des données sur le titre de page et les URL de hello</span><span class="sxs-lookup"><span data-stu-id="db191-232">hello `pageViews` table contains data about hello URL and page title</span></span>
* <span data-ttu-id="db191-233">Hello `browserTimings` table contient des données sur les performances du client, telles que hello durée tooprocess hello les données entrantes</span><span class="sxs-lookup"><span data-stu-id="db191-233">hello `browserTimings` table contains data about client performance, such as hello time taken tooprocess hello incoming data</span></span>

<span data-ttu-id="db191-234">toofind combien de navigateur de hello prend tooprocess différentes pages :</span><span class="sxs-lookup"><span data-stu-id="db191-234">toofind how long hello browser takes tooprocess different pages:</span></span>

```
browserTimings | summarize avg(networkDuration), avg(processingDuration), avg(totalDuration) by name 
```

<span data-ttu-id="db191-235">toodiscover popularities de hello de différents navigateurs :</span><span class="sxs-lookup"><span data-stu-id="db191-235">toodiscover hello popularities of different browsers:</span></span>

```
pageViews | summarize count() by client_Browser
```

<span data-ttu-id="db191-236">appels de tooAJAX tooassociate page vues, joindre avec des dépendances :</span><span class="sxs-lookup"><span data-stu-id="db191-236">tooassociate page views tooAJAX calls, join with dependencies:</span></span>

```
pageViews | join (dependencies) on operation_Id 
```

## <a name="trackrequest"></a><span data-ttu-id="db191-237">TrackRequest</span><span class="sxs-lookup"><span data-stu-id="db191-237">TrackRequest</span></span>
<span data-ttu-id="db191-238">le serveur de Hello SDK utilise les requêtes HTTP TrackRequest toolog.</span><span class="sxs-lookup"><span data-stu-id="db191-238">hello server SDK uses TrackRequest toolog HTTP requests.</span></span>

<span data-ttu-id="db191-239">Vous pouvez également l’appeler vous-même si vous souhaitez que les demandes de toosimulate dans un contexte où vous n’avez pas hello web service module en cours.</span><span class="sxs-lookup"><span data-stu-id="db191-239">You can also call it yourself if you want toosimulate requests in a context where you don't have hello web service module running.</span></span>

<span data-ttu-id="db191-240">Toutefois, hello recommandé est de télémétrie des requêtes de façon toosend où la demande de hello agit comme un <a href="#operation-context">contexte d’opération</a>.</span><span class="sxs-lookup"><span data-stu-id="db191-240">However, hello recommended way toosend request telemetry is where hello request acts as an <a href="#operation-context">operation context</a>.</span></span>

## <a name="operation-context"></a><span data-ttu-id="db191-241">Contexte de l’opération</span><span class="sxs-lookup"><span data-stu-id="db191-241">Operation context</span></span>
<span data-ttu-id="db191-242">Vous pouvez associer des éléments de télémétrie ensemble en attachant toothem un ID d’opération courantes.</span><span class="sxs-lookup"><span data-stu-id="db191-242">You can associate telemetry items together by attaching toothem a common operation ID.</span></span> <span data-ttu-id="db191-243">module de suivi des demandes standard Hello effectue cette opération pour les exceptions et les autres événements qui sont envoyées pendant le traitement d’une requête HTTP.</span><span class="sxs-lookup"><span data-stu-id="db191-243">hello standard request-tracking module does this for exceptions and other events that are sent while an HTTP request is being processed.</span></span> <span data-ttu-id="db191-244">Dans [recherche](app-insights-diagnostic-search.md) et [Analytique](app-insights-analytics.md), vous pouvez utiliser hello ID tooeasily rechercher tous les événements associés à la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="db191-244">In [Search](app-insights-diagnostic-search.md) and [Analytics](app-insights-analytics.md), you can use hello ID tooeasily find any events associated with hello request.</span></span>

<span data-ttu-id="db191-245">ID de Hello plus simple façon tooset hello est tooset un contexte d’opération à l’aide de ce modèle :</span><span class="sxs-lookup"><span data-stu-id="db191-245">hello easiest way tooset hello ID is tooset an operation context by using this pattern:</span></span>

<span data-ttu-id="db191-246">*C#*</span><span class="sxs-lookup"><span data-stu-id="db191-246">*C#*</span></span>

```C#
// Establish an operation context and associated telemetry item:
using (var operation = telemetry.StartOperation<RequestTelemetry>("operationName"))
{
    // Telemetry sent in here will use hello same operation ID.
    ...
    telemetry.TrackTrace(...); // or other Track* calls
    ...
    // Set properties of containing telemetry item--for example:
    operation.Telemetry.ResponseCode = "200";

    // Optional: explicitly send telemetry item:
    telemetry.StopOperation(operation);

} // When operation is disposed, telemetry item is sent.
```

<span data-ttu-id="db191-247">Outre la définition d’un contexte d’opération, `StartOperation` crée un élément de données de télémétrie de type hello que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="db191-247">Along with setting an operation context, `StartOperation` creates a telemetry item of hello type that you specify.</span></span> <span data-ttu-id="db191-248">Il envoie des données de télémétrie hello élément lorsque vous supprimez l’opération de hello, ou si vous appelez explicitement `StopOperation`.</span><span class="sxs-lookup"><span data-stu-id="db191-248">It sends hello telemetry item when you dispose hello operation, or if you explicitly call `StopOperation`.</span></span> <span data-ttu-id="db191-249">Si vous utilisez `RequestTelemetry` comme type de données de télémétrie hello, sa durée est définie à intervalle toohello a dépassé le délai entre le début et de fin.</span><span class="sxs-lookup"><span data-stu-id="db191-249">If you use `RequestTelemetry` as hello telemetry type, its duration is set toohello timed interval between start and stop.</span></span>

<span data-ttu-id="db191-250">Les contextes de l’opération ne peuvent pas être imbriqués.</span><span class="sxs-lookup"><span data-stu-id="db191-250">Operation contexts can't be nested.</span></span> <span data-ttu-id="db191-251">Si un contexte d’opération existe déjà, son ID est associé à tous les éléments hello contenu, y compris les élément hello créé avec `StartOperation`.</span><span class="sxs-lookup"><span data-stu-id="db191-251">If there is already an operation context, then its ID is associated with all hello contained items, including hello item created with `StartOperation`.</span></span>

<span data-ttu-id="db191-252">Dans la recherche, contexte d’opération hello est utilisé toocreate hello **éléments connexes** liste :</span><span class="sxs-lookup"><span data-stu-id="db191-252">In Search, hello operation context is used toocreate hello **Related Items** list:</span></span>

![Éléments connexes](./media/app-insights-api-custom-events-metrics/21.png)

<span data-ttu-id="db191-254">Pour plus d’informations sur le suivi des opérations personnalisées, consultez [application-insights-custom-operations-tracking.md].</span><span class="sxs-lookup"><span data-stu-id="db191-254">See [application-insights-custom-operations-tracking.md] for more information on custom operations tracking.</span></span>

### <a name="requests-in-analytics"></a><span data-ttu-id="db191-255">Requêtes dans Analytique</span><span class="sxs-lookup"><span data-stu-id="db191-255">Requests in Analytics</span></span> 

<span data-ttu-id="db191-256">Dans [Application Insights Analytique](app-insights-analytics.md), afficher les demandes des Bonjour `requests` table.</span><span class="sxs-lookup"><span data-stu-id="db191-256">In [Application Insights Analytics](app-insights-analytics.md), requests show up in hello `requests` table.</span></span>

<span data-ttu-id="db191-257">Si [échantillonnage](app-insights-sampling.md) est en opération, la propriété itemCount hello affichera une valeur supérieure à 1.</span><span class="sxs-lookup"><span data-stu-id="db191-257">If [sampling](app-insights-sampling.md) is in operation, hello itemCount property will show a value greater than 1.</span></span> <span data-ttu-id="db191-258">Pour exemple itemCount == 10 signifie que de 10 appels tootrackRequest(), processus d’échantillonnage hello transmises uniquement un d’eux.</span><span class="sxs-lookup"><span data-stu-id="db191-258">For example itemCount==10 means that of 10 calls tootrackRequest(), hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="db191-259">tooget un nombre correct de demandes et la durée moyenne segmentés par des noms de la demande, utilisez un code tel que :</span><span class="sxs-lookup"><span data-stu-id="db191-259">tooget a correct count of requests and average duration segmented by request names, use code such as:</span></span>

```AIQL
requests | summarize count = sum(itemCount), avgduration = avg(duration) by name
```


## <a name="trackexception"></a><span data-ttu-id="db191-260">TrackException</span><span class="sxs-lookup"><span data-stu-id="db191-260">TrackException</span></span>
<span data-ttu-id="db191-261">Envoyer les exceptions tooApplication Insights :</span><span class="sxs-lookup"><span data-stu-id="db191-261">Send exceptions tooApplication Insights:</span></span>

* <span data-ttu-id="db191-262">trop[les compter](app-insights-metrics-explorer.md), comme une indication de la fréquence de hello d’un problème.</span><span class="sxs-lookup"><span data-stu-id="db191-262">too[count them](app-insights-metrics-explorer.md), as an indication of hello frequency of a problem.</span></span>
* <span data-ttu-id="db191-263">trop[examiner des occurrences individuelles](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="db191-263">too[examine individual occurrences](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="db191-264">les rapports de Hello incluent les traces de pile hello.</span><span class="sxs-lookup"><span data-stu-id="db191-264">hello reports include hello stack traces.</span></span>

<span data-ttu-id="db191-265">*C#*</span><span class="sxs-lookup"><span data-stu-id="db191-265">*C#*</span></span>

    try
    {
        ...
    }
    catch (Exception ex)
    {
       telemetry.TrackException(ex);
    }

<span data-ttu-id="db191-266">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="db191-266">*JavaScript*</span></span>

    try
    {
       ...
    }
    catch (ex)
    {
       appInsights.trackException(ex);
    }

<span data-ttu-id="db191-267">Kits de développement logiciel Hello interceptent de nombreuses exceptions automatiquement, donc vous n’avez toujours pas toocall TrackException explicitement.</span><span class="sxs-lookup"><span data-stu-id="db191-267">hello SDKs catch many exceptions automatically, so you don't always have toocall TrackException explicitly.</span></span>

* <span data-ttu-id="db191-268">ASP.NET : [écrire du code toocatch exceptions](app-insights-asp-net-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="db191-268">ASP.NET: [Write code toocatch exceptions](app-insights-asp-net-exceptions.md).</span></span>
* <span data-ttu-id="db191-269">J2EE : [les exceptions sont interceptées automatiquement](app-insights-java-get-started.md#exceptions-and-request-failures).</span><span class="sxs-lookup"><span data-stu-id="db191-269">J2EE: [Exceptions are caught automatically](app-insights-java-get-started.md#exceptions-and-request-failures).</span></span>
* <span data-ttu-id="db191-270">JavaScript : les exceptions sont interceptées automatiquement.</span><span class="sxs-lookup"><span data-stu-id="db191-270">JavaScript: Exceptions are caught automatically.</span></span> <span data-ttu-id="db191-271">Si vous souhaitez collecte automatique des toodisable, ajoutez un extrait de code toohello ligne que vous insérez dans vos pages Web :</span><span class="sxs-lookup"><span data-stu-id="db191-271">If you want toodisable automatic collection, add a line toohello code snippet that you insert in your webpages:</span></span>

    ```
    ({
      instrumentationKey: "your key"
      , disableExceptionTracking: true
    })
    ```

### <a name="exceptions-in-analytics"></a><span data-ttu-id="db191-272">Exceptions dans Analytique</span><span class="sxs-lookup"><span data-stu-id="db191-272">Exceptions in Analytics</span></span>

<span data-ttu-id="db191-273">Dans [Application Insights Analytique](app-insights-analytics.md), exceptions s’afficheront dans hello `exceptions` table.</span><span class="sxs-lookup"><span data-stu-id="db191-273">In [Application Insights Analytics](app-insights-analytics.md), exceptions show up in hello `exceptions` table.</span></span>

<span data-ttu-id="db191-274">Si [échantillonnage](app-insights-sampling.md) est en opération, hello `itemCount` propriété indique une valeur supérieure à 1.</span><span class="sxs-lookup"><span data-stu-id="db191-274">If [sampling](app-insights-sampling.md) is in operation, hello `itemCount` property shows a value greater than 1.</span></span> <span data-ttu-id="db191-275">Pour exemple itemCount == 10 signifie que de 10 appels tootrackException(), processus d’échantillonnage hello transmises uniquement un d’eux.</span><span class="sxs-lookup"><span data-stu-id="db191-275">For example itemCount==10 means that of 10 calls tootrackException(), hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="db191-276">tooget un nombre correct d’exceptions segmentées par type d’exception, utilisez un code tel que :</span><span class="sxs-lookup"><span data-stu-id="db191-276">tooget a correct count of exceptions segmented by type of exception, use code such as:</span></span>

```
exceptions | summarize sum(itemCount) by type
```

<span data-ttu-id="db191-277">La plupart des hello en important les informations de pile sont déjà extrait dans des variables distinctes, mais vous pouvez extraire hello éloigné `details` tooget structure plus.</span><span class="sxs-lookup"><span data-stu-id="db191-277">Most of hello important stack information is already extracted into separate variables, but you can pull apart hello `details` structure tooget more.</span></span> <span data-ttu-id="db191-278">Étant donné que cette structure est dynamique, vous devez effectuer un cast de type de toohello hello résultat escompté.</span><span class="sxs-lookup"><span data-stu-id="db191-278">Since this structure is dynamic, you should cast hello result toohello type you expect.</span></span> <span data-ttu-id="db191-279">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="db191-279">For example:</span></span>

```AIQL
exceptions
| extend method2 = tostring(details[0].parsedStack[1].method)
```

<span data-ttu-id="db191-280">exceptions tooassociate avec leurs demandes associées, utilisez une jointure :</span><span class="sxs-lookup"><span data-stu-id="db191-280">tooassociate exceptions with their related requests, use a join:</span></span>

```
exceptions
| join (requests) on operation_Id 
```

## <a name="tracktrace"></a><span data-ttu-id="db191-281">TrackTrace</span><span class="sxs-lookup"><span data-stu-id="db191-281">TrackTrace</span></span>
<span data-ttu-id="db191-282">Utilisez TrackTrace toohelp diagnostiquer les problèmes en envoyant une tooApplication « cheminement de navigation » Insights.</span><span class="sxs-lookup"><span data-stu-id="db191-282">Use TrackTrace toohelp diagnose problems by sending a "breadcrumb trail" tooApplication Insights.</span></span> <span data-ttu-id="db191-283">Vous pouvez envoyer des blocs de données de diagnostic et les examiner dans la [Recherche de diagnostic](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="db191-283">You can send chunks of diagnostic data and inspect them in [Diagnostic Search](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="db191-284">[Connecter des adaptateurs](app-insights-asp-net-trace-logs.md) utiliser ce portail de toohello API toosend les journaux tierce.</span><span class="sxs-lookup"><span data-stu-id="db191-284">[Log adapters](app-insights-asp-net-trace-logs.md) use this API toosend third-party logs toohello portal.</span></span>

<span data-ttu-id="db191-285">*C#*</span><span class="sxs-lookup"><span data-stu-id="db191-285">*C#*</span></span>

    telemetry.TrackTrace(message, SeverityLevel.Warning, properties);


<span data-ttu-id="db191-286">Vous pouvez effectuer une recherche dans le contenu du message, mais (contrairement aux valeurs de propriété), vous ne pouvez pas les filtrer.</span><span class="sxs-lookup"><span data-stu-id="db191-286">You can search on message content, but (unlike property values) you can't filter on it.</span></span>

<span data-ttu-id="db191-287">limite de taille Hello sur `message` est plus importante que la limite de hello sur les propriétés.</span><span class="sxs-lookup"><span data-stu-id="db191-287">hello size limit on `message` is much higher than hello limit on properties.</span></span>
<span data-ttu-id="db191-288">L’avantage de TrackTrace est que vous pouvez placer des données relativement longues dans le message de type hello.</span><span class="sxs-lookup"><span data-stu-id="db191-288">An advantage of TrackTrace is that you can put relatively long data in hello message.</span></span> <span data-ttu-id="db191-289">Par exemple, vous pourriez y encoder des données POST.</span><span class="sxs-lookup"><span data-stu-id="db191-289">For example, you can encode POST data there.</span></span>  

<span data-ttu-id="db191-290">En outre, vous pouvez ajouter un message tooyour au niveau de gravité.</span><span class="sxs-lookup"><span data-stu-id="db191-290">In addition, you can add a severity level tooyour message.</span></span> <span data-ttu-id="db191-291">Et, comme les autres données de télémétrie, vous pouvez ajouter toohelp de valeurs de propriété que vous filtrez ou de recherche pour différents ensembles de traces.</span><span class="sxs-lookup"><span data-stu-id="db191-291">And, like other telemetry, you can add property values toohelp you filter or search for different sets of traces.</span></span> <span data-ttu-id="db191-292">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="db191-292">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

<span data-ttu-id="db191-293">Dans [recherche](app-insights-diagnostic-search.md), vous pouvez ensuite facilement filtrer tous les messages hello d’un niveau de gravité spécifique qui se rapportent tooa la base de données particulière.</span><span class="sxs-lookup"><span data-stu-id="db191-293">In [Search](app-insights-diagnostic-search.md), you can then easily filter out all hello messages of a particular severity level that relate tooa particular database.</span></span>


### <a name="traces-in-analytics"></a><span data-ttu-id="db191-294">Traces dans Analytique</span><span class="sxs-lookup"><span data-stu-id="db191-294">Traces in Analytics</span></span>

<span data-ttu-id="db191-295">Dans [Application Insights Analytique](app-insights-analytics.md), appelle tooTrackTrace afficher Bonjour `traces` table.</span><span class="sxs-lookup"><span data-stu-id="db191-295">In [Application Insights Analytics](app-insights-analytics.md), calls tooTrackTrace show up in hello `traces` table.</span></span>

<span data-ttu-id="db191-296">Si [échantillonnage](app-insights-sampling.md) est en opération, la propriété itemCount hello affiche une valeur supérieure à 1.</span><span class="sxs-lookup"><span data-stu-id="db191-296">If [sampling](app-insights-sampling.md) is in operation, hello itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="db191-297">Pour exemple itemCount == 10 signifie que 10 appelle trop`trackTrace()`, processus d’échantillonnage hello transmis uniquement un d’eux.</span><span class="sxs-lookup"><span data-stu-id="db191-297">For example itemCount==10 means that of 10 calls too`trackTrace()`, hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="db191-298">tooget un nombre approprié de suivi des appels, vous devez utiliser par conséquent code tel que `traces | summarize sum(itemCount)`.</span><span class="sxs-lookup"><span data-stu-id="db191-298">tooget a correct count of trace calls, you should use therefore code such as `traces | summarize sum(itemCount)`.</span></span>

## <a name="trackdependency"></a><span data-ttu-id="db191-299">TrackDependency</span><span class="sxs-lookup"><span data-stu-id="db191-299">TrackDependency</span></span>
<span data-ttu-id="db191-300">Hello d’utilisation TrackDependency appeler le temps de réponse tootrack hello et taux de réussite de la partie externe de tooan appelle du code.</span><span class="sxs-lookup"><span data-stu-id="db191-300">Use hello TrackDependency call tootrack hello response times and success rates of calls tooan external piece of code.</span></span> <span data-ttu-id="db191-301">résultats de Hello s’affichent dans les graphiques de dépendance hello dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="db191-301">hello results appear in hello dependency charts in hello portal.</span></span>

```C#
var success = false;
var startTime = DateTime.UtcNow;
var timer = System.Diagnostics.Stopwatch.StartNew();
try
{
    success = dependency.Call();
}
finally
{
    timer.Stop();
    telemetry.TrackDependency("myDependency", "myCall", startTime, timer.Elapsed, success);
}
```

<span data-ttu-id="db191-302">N’oubliez pas de ce serveur hello kits de développement incluent un [module de dépendance](app-insights-asp-net-dependencies.md) qui détecte et effectue le suivi de certains appels de dépendance automatiquement--par exemple, toodatabases et API REST.</span><span class="sxs-lookup"><span data-stu-id="db191-302">Remember that hello server SDKs include a [dependency module](app-insights-asp-net-dependencies.md) that discovers and tracks certain dependency calls automatically--for example, toodatabases and REST APIs.</span></span> <span data-ttu-id="db191-303">Vous avez tooinstall un agent sur le module de hello toomake serveur fonctionne.</span><span class="sxs-lookup"><span data-stu-id="db191-303">You have tooinstall an agent on your server toomake hello module work.</span></span> <span data-ttu-id="db191-304">Vous utilisez cet appel si vous voulez n’intercepte pas les appels tootrack hello suivi automatique, ou si vous ne souhaitez pas l’agent de tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="db191-304">You use this call if you want tootrack calls that hello automated tracking doesn't catch, or if you don't want tooinstall hello agent.</span></span>

<span data-ttu-id="db191-305">tooturn off hello standard dépendance-module de suivi, modifier [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) et supprimer la référence de hello trop`DependencyCollector.DependencyTrackingTelemetryModule`.</span><span class="sxs-lookup"><span data-stu-id="db191-305">tooturn off hello standard dependency-tracking module, edit [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) and delete hello reference too`DependencyCollector.DependencyTrackingTelemetryModule`.</span></span>

### <a name="dependencies-in-analytics"></a><span data-ttu-id="db191-306">Dépendances dans Analytique</span><span class="sxs-lookup"><span data-stu-id="db191-306">Dependencies in Analytics</span></span>

<span data-ttu-id="db191-307">Dans [Application Insights Analytique](app-insights-analytics.md), trackDependency appels apparaissent dans hello `dependencies` table.</span><span class="sxs-lookup"><span data-stu-id="db191-307">In [Application Insights Analytics](app-insights-analytics.md), trackDependency calls show up in hello `dependencies` table.</span></span>

<span data-ttu-id="db191-308">Si [échantillonnage](app-insights-sampling.md) est en opération, la propriété itemCount hello affiche une valeur supérieure à 1.</span><span class="sxs-lookup"><span data-stu-id="db191-308">If [sampling](app-insights-sampling.md) is in operation, hello itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="db191-309">Pour exemple itemCount == 10 signifie que de 10 appels tootrackDependency(), processus d’échantillonnage hello transmises uniquement un d’eux.</span><span class="sxs-lookup"><span data-stu-id="db191-309">For example itemCount==10 means that of 10 calls tootrackDependency(), hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="db191-310">tooget un nombre correct de dépendances segmentées par le composant cible, utilisez un code tel que :</span><span class="sxs-lookup"><span data-stu-id="db191-310">tooget a correct count of dependencies segmented by target component, use code such as:</span></span>

```
dependencies | summarize sum(itemCount) by target
```

<span data-ttu-id="db191-311">dépendances de tooassociate avec leurs requêtes connexes, utilisez une jointure :</span><span class="sxs-lookup"><span data-stu-id="db191-311">tooassociate dependencies with their related requests, use a join:</span></span>

```
dependencies
| join (requests) on operation_Id 
```

## <a name="flushing-data"></a><span data-ttu-id="db191-312">Vidage des données</span><span class="sxs-lookup"><span data-stu-id="db191-312">Flushing data</span></span>
<span data-ttu-id="db191-313">Normalement, hello Kit de développement logiciel envoie des données à des moments choisies un impact hello toominimize sur utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="db191-313">Normally, hello SDK sends data at times chosen toominimize hello impact on hello user.</span></span> <span data-ttu-id="db191-314">Toutefois, dans certains cas, vous pourriez tooflush mémoire tampon de hello--par exemple, si vous utilisez hello SDK dans une application s’arrête.</span><span class="sxs-lookup"><span data-stu-id="db191-314">However, in some cases, you might want tooflush hello buffer--for example, if you are using hello SDK in an application that shuts down.</span></span>

<span data-ttu-id="db191-315">*C#*</span><span class="sxs-lookup"><span data-stu-id="db191-315">*C#*</span></span>

    telemetry.Flush();

    // Allow some time for flushing before shutdown.
    System.Threading.Thread.Sleep(1000);

<span data-ttu-id="db191-316">Notez que la fonction hello est asynchrone pour hello [canal de télémétrie serveur](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel/).</span><span class="sxs-lookup"><span data-stu-id="db191-316">Note that hello function is asynchronous for hello [server telemetry channel](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel/).</span></span>

## <a name="authenticated-users"></a><span data-ttu-id="db191-317">Utilisateurs authentifiés</span><span class="sxs-lookup"><span data-stu-id="db191-317">Authenticated users</span></span>
<span data-ttu-id="db191-318">Dans une application web, les utilisateurs sont identifiés par des cookies par défaut.</span><span class="sxs-lookup"><span data-stu-id="db191-318">In a web app, users are (by default) identified by cookies.</span></span> <span data-ttu-id="db191-319">Un utilisateur peut être compté plusieurs fois s’il accède à votre application à partir d’un autre ordinateur ou navigateur, ou s’il supprime des cookies.</span><span class="sxs-lookup"><span data-stu-id="db191-319">A user might be counted more than once if they access your app from a different machine or browser, or if they delete cookies.</span></span>

<span data-ttu-id="db191-320">Si les utilisateurs se connectent tooyour application, vous pouvez obtenir un nombre plus précis en définissant des ID d’utilisateur hello authentifié dans le code hello navigateur :</span><span class="sxs-lookup"><span data-stu-id="db191-320">If users sign in tooyour app, you can get a more accurate count by setting hello authenticated user ID in hello browser code:</span></span>

<span data-ttu-id="db191-321">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="db191-321">*JavaScript*</span></span>

```JS
// Called when my app has identified hello user.
function Authenticated(signInId) {
    var validatedId = signInId.replace(/[,;=| ]+/g, "_");
    appInsights.setAuthenticatedUserContext(validatedId);
    ...
}
```

<span data-ttu-id="db191-322">Dans une application MVC Web ASP.NET, par exemple :</span><span class="sxs-lookup"><span data-stu-id="db191-322">In an ASP.NET web MVC application, for example:</span></span>

<span data-ttu-id="db191-323">*Razor*</span><span class="sxs-lookup"><span data-stu-id="db191-323">*Razor*</span></span>

        @if (Request.IsAuthenticated)
        {
            <script>
                appInsights.setAuthenticatedUserContext("@User.Identity.Name
                   .Replace("\\", "\\\\")"
                   .replace(/[,;=| ]+/g, "_"));
            </script>
        }

<span data-ttu-id="db191-324">Il n’est pas le nom de connexion réel de l’utilisateur nécessaire toouse hello.</span><span class="sxs-lookup"><span data-stu-id="db191-324">It isn't necessary toouse hello user's actual sign-in name.</span></span> <span data-ttu-id="db191-325">Il ne possède que toobe un ID unique toothat utilisateur.</span><span class="sxs-lookup"><span data-stu-id="db191-325">It only has toobe an ID that is unique toothat user.</span></span> <span data-ttu-id="db191-326">Il ne doit pas inclure des espaces ou les caractères de hello `,;=|`.</span><span class="sxs-lookup"><span data-stu-id="db191-326">It must not include spaces or any of hello characters `,;=|`.</span></span>

<span data-ttu-id="db191-327">ID d’utilisateur Hello est également défini dans un cookie de session et envoyé toohello serveur.</span><span class="sxs-lookup"><span data-stu-id="db191-327">hello user ID is also set in a session cookie and sent toohello server.</span></span> <span data-ttu-id="db191-328">Si le serveur hello SDK est installé, hello les ID est envoyé en tant que partie des propriétés de contexte hello de télémétrie de client et le serveur de l’utilisateur authentifié.</span><span class="sxs-lookup"><span data-stu-id="db191-328">If hello server SDK is installed, hello authenticated user ID is sent as part of hello context properties of both client and server telemetry.</span></span> <span data-ttu-id="db191-329">Vous pouvez ensuite filtrer et rechercher dessus.</span><span class="sxs-lookup"><span data-stu-id="db191-329">You can then filter and search on it.</span></span>

<span data-ttu-id="db191-330">Si votre application regroupe les utilisateurs dans des comptes, vous pouvez également passer un identificateur pour le compte de hello (hello avec les mêmes restrictions de caractères).</span><span class="sxs-lookup"><span data-stu-id="db191-330">If your app groups users into accounts, you can also pass an identifier for hello account (with hello same character restrictions).</span></span>

      appInsights.setAuthenticatedUserContext(validatedId, accountId);

<span data-ttu-id="db191-331">Dans [Metrics Explorer](app-insights-metrics-explorer.md), vous pouvez créer un graphique qui compte les **Utilisateurs authentifiés** et les **Comptes d’utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="db191-331">In [Metrics Explorer](app-insights-metrics-explorer.md), you can create a chart that counts **Users, Authenticated**, and **User accounts**.</span></span>

<span data-ttu-id="db191-332">Vous pouvez également [rechercher](app-insights-diagnostic-search.md) les points de données client avec des comptes et des noms d'utilisateur spécifiques.</span><span class="sxs-lookup"><span data-stu-id="db191-332">You can also [search](app-insights-diagnostic-search.md) for client data points with specific user names and accounts.</span></span>

## <span data-ttu-id="db191-333"><a name="properties"></a>Filtrage, recherche et segmentation de vos données à l’aide des propriétés</span><span class="sxs-lookup"><span data-stu-id="db191-333"><a name="properties"></a>Filtering, searching, and segmenting your data by using properties</span></span>
<span data-ttu-id="db191-334">Vous pouvez joindre des propriétés et des mesures tooyour événements (et également toometrics, vues de page, des exceptions et autres données de télémétrie).</span><span class="sxs-lookup"><span data-stu-id="db191-334">You can attach properties and measurements tooyour events (and also toometrics, page views, exceptions, and other telemetry data).</span></span>

<span data-ttu-id="db191-335">*Propriétés* sont des valeurs de chaîne que vous pouvez utiliser toofilter votre télémétrie dans les rapports d’utilisation hello.</span><span class="sxs-lookup"><span data-stu-id="db191-335">*Properties* are string values that you can use toofilter your telemetry in hello usage reports.</span></span> <span data-ttu-id="db191-336">Par exemple, si votre application fournit plusieurs jeux, vous pouvez attacher nom hello d’événement de jeu tooeach hello afin que vous pouvez voir les jeux sont plus populaires.</span><span class="sxs-lookup"><span data-stu-id="db191-336">For example, if your app provides several games, you can attach hello name of hello game tooeach event so that you can see which games are more popular.</span></span>

<span data-ttu-id="db191-337">Il existe une limite de 8 192 sur la longueur de la chaîne hello.</span><span class="sxs-lookup"><span data-stu-id="db191-337">There's a limit of 8192 on hello string length.</span></span> <span data-ttu-id="db191-338">(Si vous souhaitez toosend de grandes quantités de données, utilisez le paramètre de message hello de [TrackTrace](#track-trace).)</span><span class="sxs-lookup"><span data-stu-id="db191-338">(If you want toosend large chunks of data, use hello message parameter of [TrackTrace](#track-trace).)</span></span>

<span data-ttu-id="db191-339">*mesures* sont des valeurs numériques qui peuvent être représentées sous forme graphique.</span><span class="sxs-lookup"><span data-stu-id="db191-339">*Metrics* are numeric values that can be presented graphically.</span></span> <span data-ttu-id="db191-340">Par exemple, vous pourriez toosee s’il existe une augmentation progressive de scores de hello votre joueurs atteindre.</span><span class="sxs-lookup"><span data-stu-id="db191-340">For example, you might want toosee if there's a gradual increase in hello scores that your gamers achieve.</span></span> <span data-ttu-id="db191-341">graphiques de Hello peuvent être segmentées par hello séparer les propriétés qui sont envoyées avec les événements de hello, qui vous pouvez d’obtenir ou empilées graphiques pour jeux différents.</span><span class="sxs-lookup"><span data-stu-id="db191-341">hello graphs can be segmented by hello properties that are sent with hello event, so that you can get separate or stacked graphs for different games.</span></span>

<span data-ttu-id="db191-342">Pour toobe de valeurs de mesure affiché correctement, ils doivent être too0 égal ou supérieur.</span><span class="sxs-lookup"><span data-stu-id="db191-342">For metric values toobe correctly displayed, they should be greater than or equal too0.</span></span>

<span data-ttu-id="db191-343">Il existe quelques [limites nombre hello de propriétés, les valeurs de propriété et les métriques](#limits) que vous pouvez utiliser.</span><span class="sxs-lookup"><span data-stu-id="db191-343">There are some [limits on hello number of properties, property values, and metrics](#limits) that you can use.</span></span>

<span data-ttu-id="db191-344">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="db191-344">*JavaScript*</span></span>

    appInsights.trackEvent
      ("WinGame",
         // String properties:
         {Game: currentGame.name, Difficulty: currentGame.difficulty},
         // Numeric metrics:
         {Score: currentGame.score, Opponents: currentGame.opponentCount}
         );

    appInsights.trackPageView
        ("page name", "http://fabrikam.com/pageurl.html",
          // String properties:
         {Game: currentGame.name, Difficulty: currentGame.difficulty},
         // Numeric metrics:
         {Score: currentGame.score, Opponents: currentGame.opponentCount}
         );


<span data-ttu-id="db191-345">*C#*</span><span class="sxs-lookup"><span data-stu-id="db191-345">*C#*</span></span>

    // Set up some properties and metrics:
    var properties = new Dictionary <string, string>
       {{"game", currentGame.Name}, {"difficulty", currentGame.Difficulty}};
    var metrics = new Dictionary <string, double>
       {{"Score", currentGame.Score}, {"Opponents", currentGame.OpponentCount}};

    // Send hello event:
    telemetry.TrackEvent("WinGame", properties, metrics);


<span data-ttu-id="db191-346">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="db191-346">*Visual Basic*</span></span>

    ' Set up some properties:
    Dim properties = New Dictionary (Of String, String)
    properties.Add("game", currentGame.Name)
    properties.Add("difficulty", currentGame.Difficulty)

    Dim metrics = New Dictionary (Of String, Double)
    metrics.Add("Score", currentGame.Score)
    metrics.Add("Opponents", currentGame.OpponentCount)

    ' Send hello event:
    telemetry.TrackEvent("WinGame", properties, metrics)


<span data-ttu-id="db191-347">*Java*</span><span class="sxs-lookup"><span data-stu-id="db191-347">*Java*</span></span>

    Map<String, String> properties = new HashMap<String, String>();
    properties.put("game", currentGame.getName());
    properties.put("difficulty", currentGame.getDifficulty());

    Map<String, Double> metrics = new HashMap<String, Double>();
    metrics.put("Score", currentGame.getScore());
    metrics.put("Opponents", currentGame.getOpponentCount());

    telemetry.trackEvent("WinGame", properties, metrics);


> [!NOTE]
> <span data-ttu-id="db191-348">Prenez soin toolog pas les informations personnelles dans les propriétés.</span><span class="sxs-lookup"><span data-stu-id="db191-348">Take care not toolog personally identifiable information in properties.</span></span>
>
>

<span data-ttu-id="db191-349">*Si vous avez utilisé des métriques*, ouvrez Metrics Explorer et sélectionnez des mesures de hello de hello **personnalisé** groupe :</span><span class="sxs-lookup"><span data-stu-id="db191-349">*If you used metrics*, open Metrics Explorer and select hello metric from hello **Custom** group:</span></span>

![Ouvrez l’Explorateur de métriques, graphique de hello select et sélectionnez hello métrique](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

> [!NOTE]
> <span data-ttu-id="db191-351">Si votre métrique n’apparaît pas, ou si hello **personnalisé** en-tête n’est pas présent, panneau de sélection de fermer hello et réessayez ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="db191-351">If your metric doesn't appear, or if hello **Custom** heading isn't there, close hello selection blade and try again later.</span></span> <span data-ttu-id="db191-352">Métriques peuvent parfois prendre une heure toobe agrégées via le pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="db191-352">Metrics can sometimes take an hour toobe aggregated through hello pipeline.</span></span>

<span data-ttu-id="db191-353">*Si vous avez utilisé des propriétés et des mesures*, segment métrique de hello par la propriété de hello :</span><span class="sxs-lookup"><span data-stu-id="db191-353">*If you used properties and metrics*, segment hello metric by hello property:</span></span>

![Définir le regroupement, puis sélectionnez la propriété hello sous Group by](./media/app-insights-api-custom-events-metrics/04-segment-metric-event.png)

<span data-ttu-id="db191-355">*Dans la recherche de Diagnostic*, vous pouvez afficher les propriétés de hello et les métriques des occurrences individuelles d’un événement.</span><span class="sxs-lookup"><span data-stu-id="db191-355">*In Diagnostic Search*, you can view hello properties and metrics of individual occurrences of an event.</span></span>

![Sélectionnez une instance, puis sélectionnez « ... »](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-4.png)

<span data-ttu-id="db191-357">Hello d’utilisation **recherche** champ toosee des occurrences d’événements qui ont une valeur de propriété particulière.</span><span class="sxs-lookup"><span data-stu-id="db191-357">Use hello **Search** field toosee event occurrences that have a particular property value.</span></span>

![Tapez un terme dans Rechercher](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-5.png)

<span data-ttu-id="db191-359">[En savoir plus sur les expressions de recherche](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="db191-359">[Learn more about search expressions](app-insights-diagnostic-search.md).</span></span>

### <a name="alternative-way-tooset-properties-and-metrics"></a><span data-ttu-id="db191-360">Mesures et les propriétés de tooset autre moyen</span><span class="sxs-lookup"><span data-stu-id="db191-360">Alternative way tooset properties and metrics</span></span>
<span data-ttu-id="db191-361">S’il est plus pratique, vous pouvez collecter les paramètres d’un événement dans un objet séparé hello :</span><span class="sxs-lookup"><span data-stu-id="db191-361">If it's more convenient, you can collect hello parameters of an event in a separate object:</span></span>

    var event = new EventTelemetry();

    event.Name = "WinGame";
    event.Metrics["processingTime"] = stopwatch.Elapsed.TotalMilliseconds;
    event.Properties["game"] = currentGame.Name;
    event.Properties["difficulty"] = currentGame.Difficulty;
    event.Metrics["Score"] = currentGame.Score;
    event.Metrics["Opponents"] = currentGame.Opponents.Length;

    telemetry.TrackEvent(event);

> [!WARNING]
> <span data-ttu-id="db191-362">Ne réutilisez pas hello même instance d’élément de données de télémétrie (`event` dans cet exemple) toocall Track*() plusieurs fois.</span><span class="sxs-lookup"><span data-stu-id="db191-362">Don't reuse hello same telemetry item instance (`event` in this example) toocall Track*() multiple times.</span></span> <span data-ttu-id="db191-363">Cela peut entraîner des toobe de télémétrie envoyé avec une configuration incorrecte.</span><span class="sxs-lookup"><span data-stu-id="db191-363">This may cause telemetry toobe sent with incorrect configuration.</span></span>
>
>

### <a name="custom-measurements-and-properties-in-analytics"></a><span data-ttu-id="db191-364">Mesures et propriétés personnalisées dans Analytique</span><span class="sxs-lookup"><span data-stu-id="db191-364">Custom measurements and properties in Analytics</span></span>

<span data-ttu-id="db191-365">Dans [Analytique](app-insights-analytics.md), affichent les mesures personnalisées et les propriétés Bonjour `customMeasurements` et `customDimensions` les attributs de chaque enregistrement de données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="db191-365">In [Analytics](app-insights-analytics.md), custom metrics and properties show in hello `customMeasurements` and `customDimensions` attributes of each telemetry record.</span></span>

<span data-ttu-id="db191-366">Par exemple, si vous avez ajouté une propriété nommée « jeu » tooyour télémétrie des requêtes, cette requête compte les occurrences de hello de différentes valeurs de « jeu » et afficher moyenne hello Hello métrique personnalisé « score » :</span><span class="sxs-lookup"><span data-stu-id="db191-366">For example, if you have added a property named "game" tooyour request telemetry, this query counts hello occurrences of different values of "game", and show hello average of hello custom metric "score":</span></span>

```
requests
| summarize sum(itemCount), avg(todouble(customMeasurements.score)) by tostring(customDimensions.game) 
```

<span data-ttu-id="db191-367">Notez que :</span><span class="sxs-lookup"><span data-stu-id="db191-367">Notice that:</span></span>

* <span data-ttu-id="db191-368">Lorsque vous extrayez une valeur de hello customDimensions ou customMeasurements JSON, il a le type dynamique, et par conséquent, vous devez effectuer un cast `tostring` ou `todouble`.</span><span class="sxs-lookup"><span data-stu-id="db191-368">When you extract a value from hello customDimensions or customMeasurements JSON, it has dynamic type, and so you must cast it `tostring` or `todouble`.</span></span>
* <span data-ttu-id="db191-369">compte tootake de possibilité de hello de [échantillonnage](app-insights-sampling.md), vous devez utiliser `sum(itemCount)`, et non `count()`.</span><span class="sxs-lookup"><span data-stu-id="db191-369">tootake account of hello possibility of [sampling](app-insights-sampling.md), you should use `sum(itemCount)`, not `count()`.</span></span>



## <span data-ttu-id="db191-370"><a name="timed"></a> Événements de durée</span><span class="sxs-lookup"><span data-stu-id="db191-370"><a name="timed"></a> Timing events</span></span>
<span data-ttu-id="db191-371">Vous pouvez souhaiter que toochart la durée pendant laquelle il effectue tooperform une action.</span><span class="sxs-lookup"><span data-stu-id="db191-371">Sometimes you want toochart how long it takes tooperform an action.</span></span> <span data-ttu-id="db191-372">Par exemple, vous pourriez tooknow la durée pendant laquelle les utilisateurs prennent tooconsider choix dans un jeu.</span><span class="sxs-lookup"><span data-stu-id="db191-372">For example, you might want tooknow how long users take tooconsider choices in a game.</span></span> <span data-ttu-id="db191-373">Vous pouvez utiliser le paramètre de mesure hello pour cela.</span><span class="sxs-lookup"><span data-stu-id="db191-373">You can use hello measurement parameter for this.</span></span>

<span data-ttu-id="db191-374">*C#*</span><span class="sxs-lookup"><span data-stu-id="db191-374">*C#*</span></span>

    var stopwatch = System.Diagnostics.Stopwatch.StartNew();

    // ... perform hello timed action ...

    stopwatch.Stop();

    var metrics = new Dictionary <string, double>
       {{"processingTime", stopwatch.Elapsed.TotalMilliseconds}};

    // Set up some properties:
    var properties = new Dictionary <string, string>
       {{"signalSource", currentSignalSource.Name}};

    // Send hello event:
    telemetry.TrackEvent("SignalProcessed", properties, metrics);



## <span data-ttu-id="db191-375"><a name="defaults"></a>Propriétés par défaut pour la télémétrie personnalisée</span><span class="sxs-lookup"><span data-stu-id="db191-375"><a name="defaults"></a>Default properties for custom telemetry</span></span>
<span data-ttu-id="db191-376">Si vous souhaitez que les valeurs de propriété par défaut tooset pour certaines des événements personnalisés hello que vous écrivez, vous pouvez les définir dans une instance de TelemetryClient.</span><span class="sxs-lookup"><span data-stu-id="db191-376">If you want tooset default property values for some of hello custom events that you write, you can set them in a TelemetryClient instance.</span></span> <span data-ttu-id="db191-377">Ils sont des éléments de télémétrie tooevery jointe qui sont envoyé à partir de ce client.</span><span class="sxs-lookup"><span data-stu-id="db191-377">They are attached tooevery telemetry item that's sent from that client.</span></span>

<span data-ttu-id="db191-378">*C#*</span><span class="sxs-lookup"><span data-stu-id="db191-378">*C#*</span></span>

    using Microsoft.ApplicationInsights.DataContracts;

    var gameTelemetry = new TelemetryClient();
    gameTelemetry.Context.Properties["Game"] = currentGame.Name;
    // Now all telemetry will automatically be sent with hello context property:
    gameTelemetry.TrackEvent("WinGame");

<span data-ttu-id="db191-379">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="db191-379">*Visual Basic*</span></span>

    Dim gameTelemetry = New TelemetryClient()
    gameTelemetry.Context.Properties("Game") = currentGame.Name
    ' Now all telemetry will automatically be sent with hello context property:
    gameTelemetry.TrackEvent("WinGame")

<span data-ttu-id="db191-380">*Java*</span><span class="sxs-lookup"><span data-stu-id="db191-380">*Java*</span></span>

    import com.microsoft.applicationinsights.TelemetryClient;
    import com.microsoft.applicationinsights.TelemetryContext;
    ...


    TelemetryClient gameTelemetry = new TelemetryClient();
    TelemetryContext context = gameTelemetry.getContext();
    context.getProperties().put("Game", currentGame.Name);

    gameTelemetry.TrackEvent("WinGame");



<span data-ttu-id="db191-381">Appels de télémétrie individuels peuvent remplacer des valeurs de par défaut de hello dans les dictionnaires de leurs propriétés.</span><span class="sxs-lookup"><span data-stu-id="db191-381">Individual telemetry calls can override hello default values in their property dictionaries.</span></span>

<span data-ttu-id="db191-382">*Pour les clients Web JavaScript*, [utilisez des initialiseurs de télémétrie JavaScript](#js-initializer).</span><span class="sxs-lookup"><span data-stu-id="db191-382">*For JavaScript web clients*, [use JavaScript telemetry initializers](#js-initializer).</span></span>

<span data-ttu-id="db191-383">*données de télémétrie tooadd propriétés tooall*, y compris les données hello à partir des modules de collection standard, [implémenter `ITelemetryInitializer` ](app-insights-api-filtering-sampling.md#add-properties).</span><span class="sxs-lookup"><span data-stu-id="db191-383">*tooadd properties tooall telemetry*, including hello data from standard collection modules, [implement `ITelemetryInitializer`](app-insights-api-filtering-sampling.md#add-properties).</span></span>

## <a name="sampling-filtering-and-processing-telemetry"></a><span data-ttu-id="db191-384">Échantillonnage, filtrage et traitement de la télémétrie</span><span class="sxs-lookup"><span data-stu-id="db191-384">Sampling, filtering, and processing telemetry</span></span>
<span data-ttu-id="db191-385">Vous pouvez écrire tooprocess de code de votre télémétrie avant d’être envoyée à partir de hello SDK.</span><span class="sxs-lookup"><span data-stu-id="db191-385">You can write code tooprocess your telemetry before it's sent from hello SDK.</span></span> <span data-ttu-id="db191-386">le traitement de Hello comprend des données envoyées à partir de modules de télémétrie standard hello, telles que la collection de requêtes HTTP et de la collection de dépendances.</span><span class="sxs-lookup"><span data-stu-id="db191-386">hello processing includes data that's sent from hello standard telemetry modules, such as HTTP request collection and dependency collection.</span></span>

<span data-ttu-id="db191-387">[Ajouter des propriétés](app-insights-api-filtering-sampling.md#add-properties) tootelemetry en implémentant `ITelemetryInitializer`.</span><span class="sxs-lookup"><span data-stu-id="db191-387">[Add properties](app-insights-api-filtering-sampling.md#add-properties) tootelemetry by implementing `ITelemetryInitializer`.</span></span> <span data-ttu-id="db191-388">Par exemple, vous pouvez ajouter des numéros de version ou des valeurs calculées à partir d'autres propriétés.</span><span class="sxs-lookup"><span data-stu-id="db191-388">For example, you can add version numbers or values that are calculated from other properties.</span></span>

<span data-ttu-id="db191-389">[Le filtrage](app-insights-api-filtering-sampling.md#filtering) peut modifier ou ignorer les données de télémétrie avant d’être envoyée à partir de hello SDK en implémentant `ITelemetryProcesor`.</span><span class="sxs-lookup"><span data-stu-id="db191-389">[Filtering](app-insights-api-filtering-sampling.md#filtering) can modify or discard telemetry before it's sent from hello SDK by implementing `ITelemetryProcesor`.</span></span> <span data-ttu-id="db191-390">Vous contrôlez ce qui est envoyé ou rejeté, mais vous avez tooaccount pour effet de hello sur vos mesures.</span><span class="sxs-lookup"><span data-stu-id="db191-390">You control what is sent or discarded, but you have tooaccount for hello effect on your metrics.</span></span> <span data-ttu-id="db191-391">En fonction de la façon dont vous ignorez les éléments, vous risquez de perdre toonavigate de capacité hello entre des éléments connexes.</span><span class="sxs-lookup"><span data-stu-id="db191-391">Depending on how you discard items, you might lose hello ability toonavigate between related items.</span></span>

<span data-ttu-id="db191-392">[Échantillonnage](app-insights-api-filtering-sampling.md) est un volume de hello tooreduce offre groupée de données qui sont envoyés à partir de votre portail toohello d’application.</span><span class="sxs-lookup"><span data-stu-id="db191-392">[Sampling](app-insights-api-filtering-sampling.md) is a packaged solution tooreduce hello volume of data that's sent from your app toohello portal.</span></span> <span data-ttu-id="db191-393">Il le fait sans affecter les métriques hello affiché.</span><span class="sxs-lookup"><span data-stu-id="db191-393">It does so without affecting hello displayed metrics.</span></span> <span data-ttu-id="db191-394">Et il le fait sans affecter vos problèmes de toodiagnose de capacité en naviguant entre les éléments connexes tels que les exceptions, les demandes et les vues de page.</span><span class="sxs-lookup"><span data-stu-id="db191-394">And it does so without affecting your ability toodiagnose problems by navigating between related items such as exceptions, requests, and page views.</span></span>

<span data-ttu-id="db191-395">[En savoir plus](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="db191-395">[Learn more](app-insights-api-filtering-sampling.md).</span></span>

## <a name="disabling-telemetry"></a><span data-ttu-id="db191-396">Désactivation de la télémétrie</span><span class="sxs-lookup"><span data-stu-id="db191-396">Disabling telemetry</span></span>
<span data-ttu-id="db191-397">trop*dynamiquement arrêter et démarrer* hello collecte et transmission des données de télémétrie :</span><span class="sxs-lookup"><span data-stu-id="db191-397">too*dynamically stop and start* hello collection and transmission of telemetry:</span></span>

<span data-ttu-id="db191-398">*C#*</span><span class="sxs-lookup"><span data-stu-id="db191-398">*C#*</span></span>

```C#

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```

<span data-ttu-id="db191-399">trop*désactiver les collecteurs standards sélectionnés*--par exemple, les compteurs de performance, les requêtes HTTP ou dépendances--supprimer ou commenter les lignes concernées hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). Vous pouvez cela, par exemple, si vous souhaitez toosend vos propres données TrackRequest.</span><span class="sxs-lookup"><span data-stu-id="db191-399">too*disable selected standard collectors*--for example, performance counters, HTTP requests, or dependencies--delete or comment out hello relevant lines in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). You can do this, for example, if you want toosend your own TrackRequest data.</span></span>

## <span data-ttu-id="db191-400"><a name="debug"></a>Mode Développeur :</span><span class="sxs-lookup"><span data-stu-id="db191-400"><a name="debug"></a>Developer mode</span></span>
<span data-ttu-id="db191-401">Pendant le débogage, il est utile toohave votre télémétrie expédié via le pipeline de hello afin que vous pouvez voir immédiatement les résultats.</span><span class="sxs-lookup"><span data-stu-id="db191-401">During debugging, it's useful toohave your telemetry expedited through hello pipeline so that you can see results immediately.</span></span> <span data-ttu-id="db191-402">Vous get également des messages supplémentaires qui vous permettent de suivi des problèmes avec les données de télémétrie hello.</span><span class="sxs-lookup"><span data-stu-id="db191-402">You also get additional messages that help you trace any problems with hello telemetry.</span></span> <span data-ttu-id="db191-403">Désactivez-les lors de la production, car ils peuvent ralentir votre application.</span><span class="sxs-lookup"><span data-stu-id="db191-403">Switch it off in production, because it may slow down your app.</span></span>

<span data-ttu-id="db191-404">*C#*</span><span class="sxs-lookup"><span data-stu-id="db191-404">*C#*</span></span>

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = true;

<span data-ttu-id="db191-405">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="db191-405">*Visual Basic*</span></span>

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = True


## <span data-ttu-id="db191-406"><a name="ikey"></a>Définition de clé d’instrumentation de hello pour une télémétrie personnalisée sélectionnée</span><span class="sxs-lookup"><span data-stu-id="db191-406"><a name="ikey"></a> Setting hello instrumentation key for selected custom telemetry</span></span>
<span data-ttu-id="db191-407">*C#*</span><span class="sxs-lookup"><span data-stu-id="db191-407">*C#*</span></span>

    var telemetry = new TelemetryClient();
    telemetry.InstrumentationKey = "---my key---";
    // ...


## <span data-ttu-id="db191-408"><a name="dynamic-ikey"></a> Clé d'instrumentation dynamique</span><span class="sxs-lookup"><span data-stu-id="db191-408"><a name="dynamic-ikey"></a> Dynamic instrumentation key</span></span>
<span data-ttu-id="db191-409">tooavoid mélange de télémétrie de développement, de test et environnements de production, vous pouvez [créer des ressources Application Insights distinctes](app-insights-create-new-resource.md) et modifier leurs clés, en fonction de l’environnement de hello.</span><span class="sxs-lookup"><span data-stu-id="db191-409">tooavoid mixing up telemetry from development, test, and production environments, you can [create separate Application Insights resources](app-insights-create-new-resource.md) and change their keys, depending on hello environment.</span></span>

<span data-ttu-id="db191-410">Au lieu d’obtenir la clé d’instrumentation hello hello fichier de configuration, vous pouvez la définir dans votre code.</span><span class="sxs-lookup"><span data-stu-id="db191-410">Instead of getting hello instrumentation key from hello configuration file, you can set it in your code.</span></span> <span data-ttu-id="db191-411">Clé d’ensemble hello dans une méthode d’initialisation, par exemple global.aspx.cs dans un service ASP.NET :</span><span class="sxs-lookup"><span data-stu-id="db191-411">Set hello key in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

<span data-ttu-id="db191-412">*C#*</span><span class="sxs-lookup"><span data-stu-id="db191-412">*C#*</span></span>

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      ...

<span data-ttu-id="db191-413">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="db191-413">*JavaScript*</span></span>

    appInsights.config.instrumentationKey = myKey;



<span data-ttu-id="db191-414">Dans les pages Web, vous pourriez tooset à partir du serveur hello web état, plutôt que par codage il littéralement dans le script de hello.</span><span class="sxs-lookup"><span data-stu-id="db191-414">In webpages, you might want tooset it from hello web server's state, rather than coding it literally into hello script.</span></span> <span data-ttu-id="db191-415">Par exemple, dans une page web générée dans une application ASP.NET :</span><span class="sxs-lookup"><span data-stu-id="db191-415">For example, in a webpage generated in an ASP.NET app:</span></span>

<span data-ttu-id="db191-416">*JavaScript dans Razor*</span><span class="sxs-lookup"><span data-stu-id="db191-416">*JavaScript in Razor*</span></span>

    <script type="text/javascript">
    // Standard Application Insights webpage script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      @Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="telemetrycontext"></a><span data-ttu-id="db191-417">TelemetryContext</span><span class="sxs-lookup"><span data-stu-id="db191-417">TelemetryContext</span></span>
<span data-ttu-id="db191-418">TelemetryClient a une propriété de contexte contenant les valeurs qui sont envoyées avec toutes les données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="db191-418">TelemetryClient has a Context property, which contains values that are sent along with all telemetry data.</span></span> <span data-ttu-id="db191-419">Ils sont normalement définies par les modules de télémétrie standard hello, mais vous pouvez également les définir vous-même.</span><span class="sxs-lookup"><span data-stu-id="db191-419">They are normally set by hello standard telemetry modules, but you can also set them yourself.</span></span> <span data-ttu-id="db191-420">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="db191-420">For example:</span></span>

    telemetry.Context.Operation.Name = "MyOperationName";

<span data-ttu-id="db191-421">Si vous définissez une de ces valeurs vous-même, envisagez de supprimer la ligne hello pertinentes [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), de sorte que vos valeurs et hello standard ne pas dérouter.</span><span class="sxs-lookup"><span data-stu-id="db191-421">If you set any of these values yourself, consider removing hello relevant line from [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), so that your values and hello standard values don't get confused.</span></span>

* <span data-ttu-id="db191-422">**Composant**: hello application et sa version.</span><span class="sxs-lookup"><span data-stu-id="db191-422">**Component**: hello app and its version.</span></span>
* <span data-ttu-id="db191-423">**APPAREIL**: les données sur l’appareil hello où l’application hello est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="db191-423">**Device**: Data about hello device where hello app is running.</span></span> <span data-ttu-id="db191-424">(Dans les applications web, voici hello serveur ou dispositif envoyées par les données de télémétrie hello.)</span><span class="sxs-lookup"><span data-stu-id="db191-424">(In web apps, this is hello server or client device that hello telemetry is sent from.)</span></span>
* <span data-ttu-id="db191-425">**InstrumentationKey**: hello ressource Application Insights dans Azure où apparaissent les données de télémétrie hello.</span><span class="sxs-lookup"><span data-stu-id="db191-425">**InstrumentationKey**: hello Application Insights resource in Azure where hello telemetry appear.</span></span> <span data-ttu-id="db191-426">Elle est généralement récupérée dans ApplicationInsights.config.</span><span class="sxs-lookup"><span data-stu-id="db191-426">It's usually picked up from ApplicationInsights.config.</span></span>
* <span data-ttu-id="db191-427">**Emplacement**: hello emplacement géographique de hello appareil.</span><span class="sxs-lookup"><span data-stu-id="db191-427">**Location**: hello geographic location of hello device.</span></span>
* <span data-ttu-id="db191-428">**Opération**: dans les applications web, hello la requête HTTP actuelle.</span><span class="sxs-lookup"><span data-stu-id="db191-428">**Operation**: In web apps, hello current HTTP request.</span></span> <span data-ttu-id="db191-429">Dans d’autres types d’application, vous pouvez définir cette événements toogroup ensemble.</span><span class="sxs-lookup"><span data-stu-id="db191-429">In other app types, you can set this toogroup events together.</span></span>
  * <span data-ttu-id="db191-430">**ID**: une valeur générée qui met en relation différents événements de manière à ce que vous trouviez les « Éléments associés » lorsque vous inspectez un événement dans la Recherche de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="db191-430">**Id**: A generated value that correlates different events, so that when you inspect any event in Diagnostic Search, you can find related items.</span></span>
  * <span data-ttu-id="db191-431">**Nom**: un identificateur, généralement hello URL de demande de hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="db191-431">**Name**: An identifier, usually hello URL of hello HTTP request.</span></span>
  * <span data-ttu-id="db191-432">**SyntheticSource**: si non null ou vide, une chaîne indiquant que cette source de hello de demande de hello a été identifiée comme un test web ou le robot.</span><span class="sxs-lookup"><span data-stu-id="db191-432">**SyntheticSource**: If not null or empty, a string that indicates that hello source of hello request has been identified as a robot or web test.</span></span> <span data-ttu-id="db191-433">Par défaut, elle est exclue des calculs dans Metrics Explorer.</span><span class="sxs-lookup"><span data-stu-id="db191-433">By default, it is excluded from calculations in Metrics Explorer.</span></span>
* <span data-ttu-id="db191-434">**Propriétés** : ce sont les propriétés qui sont envoyées avec toutes les données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="db191-434">**Properties**: Properties that are sent with all telemetry data.</span></span> <span data-ttu-id="db191-435">Elles peuvent être remplacées dans les appels Track* individuels.</span><span class="sxs-lookup"><span data-stu-id="db191-435">It can be overridden in individual Track* calls.</span></span>
* <span data-ttu-id="db191-436">**Session**: hello session utilisateur.</span><span class="sxs-lookup"><span data-stu-id="db191-436">**Session**: hello user's session.</span></span> <span data-ttu-id="db191-437">Hello ID a la valeur tooa généré, ce qui est modifiée lorsque l’utilisateur de hello n’a pas été active pendant un certain temps.</span><span class="sxs-lookup"><span data-stu-id="db191-437">hello ID is set tooa generated value, which is changed when hello user has not been active for a while.</span></span>
* <span data-ttu-id="db191-438">**Utilisateur** : Informations utilisateur.</span><span class="sxs-lookup"><span data-stu-id="db191-438">**User**: User information.</span></span>

## <a name="limits"></a><span data-ttu-id="db191-439">limites</span><span class="sxs-lookup"><span data-stu-id="db191-439">Limits</span></span>
[!INCLUDE [application-insights-limits](../../includes/application-insights-limits.md)]

<span data-ttu-id="db191-440">tooavoid atteint la limite de débit hello, utilisez [échantillonnage](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="db191-440">tooavoid hitting hello data rate limit, use [sampling](app-insights-sampling.md).</span></span>

<span data-ttu-id="db191-441">toodetermine comment les données de type long sont conservées, consultez [rétention des données et confidentialité](app-insights-data-retention-privacy.md).</span><span class="sxs-lookup"><span data-stu-id="db191-441">toodetermine how long data is kept, see [Data retention and privacy](app-insights-data-retention-privacy.md).</span></span>

## <a name="reference-docs"></a><span data-ttu-id="db191-442">Documents de référence</span><span class="sxs-lookup"><span data-stu-id="db191-442">Reference docs</span></span>
* [<span data-ttu-id="db191-443">Référence ASP.NET</span><span class="sxs-lookup"><span data-stu-id="db191-443">ASP.NET reference</span></span>](https://msdn.microsoft.com/library/dn817570.aspx)
* [<span data-ttu-id="db191-444">Référence Java</span><span class="sxs-lookup"><span data-stu-id="db191-444">Java reference</span></span>](http://dl.windowsazure.com/applicationinsights/javadoc/)
* [<span data-ttu-id="db191-445">Référence JavaScript</span><span class="sxs-lookup"><span data-stu-id="db191-445">JavaScript reference</span></span>](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md)
* [<span data-ttu-id="db191-446">Kit de développement logiciel Android</span><span class="sxs-lookup"><span data-stu-id="db191-446">Android SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-Android)
* [<span data-ttu-id="db191-447">Kit de développement logiciel (SDK) iOS</span><span class="sxs-lookup"><span data-stu-id="db191-447">iOS SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-iOS)

## <a name="sdk-code"></a><span data-ttu-id="db191-448">Code de Kit de développement logiciel (SDK)</span><span class="sxs-lookup"><span data-stu-id="db191-448">SDK code</span></span>
* [<span data-ttu-id="db191-449">Kit de développement logiciel (SDK) principal ASP.NET</span><span class="sxs-lookup"><span data-stu-id="db191-449">ASP.NET Core SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [<span data-ttu-id="db191-450">ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="db191-450">ASP.NET 5</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [<span data-ttu-id="db191-451">Packages Windows Server</span><span class="sxs-lookup"><span data-stu-id="db191-451">Windows Server packages</span></span>](https://github.com/Microsoft/applicationInsights-dotnet-server)
* [<span data-ttu-id="db191-452">Kit SDK Java</span><span class="sxs-lookup"><span data-stu-id="db191-452">Java SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-Java)
* [<span data-ttu-id="db191-453">Kit de développement logiciel (SDK) JavaScript</span><span class="sxs-lookup"><span data-stu-id="db191-453">JavaScript SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-JS)
* [<span data-ttu-id="db191-454">Toutes les plateformes</span><span class="sxs-lookup"><span data-stu-id="db191-454">All platforms</span></span>](https://github.com/Microsoft?utf8=%E2%9C%93&query=applicationInsights)

## <a name="questions"></a><span data-ttu-id="db191-455">Questions</span><span class="sxs-lookup"><span data-stu-id="db191-455">Questions</span></span>
* <span data-ttu-id="db191-456">*Quelles exceptions peuvent être lancées par les appels Track_() ?*</span><span class="sxs-lookup"><span data-stu-id="db191-456">*What exceptions might Track_() calls throw?*</span></span>

    <span data-ttu-id="db191-457">Aucune.</span><span class="sxs-lookup"><span data-stu-id="db191-457">None.</span></span> <span data-ttu-id="db191-458">Vous n’avez pas besoin de toowrap dans les clauses try-catch.</span><span class="sxs-lookup"><span data-stu-id="db191-458">You don't need toowrap them in try-catch clauses.</span></span> <span data-ttu-id="db191-459">Si le Kit de développement logiciel de hello rencontre des problèmes, il enregistrera les messages dans la sortie de console de débogage hello et--si hello messages obtenir via--dans la recherche de Diagnostic.</span><span class="sxs-lookup"><span data-stu-id="db191-459">If hello SDK encounters problems, it will log messages in hello debug console output and--if hello messages get through--in Diagnostic Search.</span></span>
* <span data-ttu-id="db191-460">*Existe-t-il un tooget de données API REST à partir du portail de hello ?*</span><span class="sxs-lookup"><span data-stu-id="db191-460">*Is there a REST API tooget data from hello portal?*</span></span>

    <span data-ttu-id="db191-461">Oui, hello [API d’accès aux données](https://dev.applicationinsights.io/).</span><span class="sxs-lookup"><span data-stu-id="db191-461">Yes, hello [data access API](https://dev.applicationinsights.io/).</span></span> <span data-ttu-id="db191-462">Incluent d’autres données tooextract [exporter à partir de l’Analytique tooPower BI](app-insights-export-power-bi.md) et [exportation continue](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="db191-462">Other ways tooextract data include [export from Analytics tooPower BI](app-insights-export-power-bi.md) and [continuous export](app-insights-export-telemetry.md).</span></span>

## <span data-ttu-id="db191-463"><a name="next"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="db191-463"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="db191-464">Recherche d’événements et de journaux</span><span class="sxs-lookup"><span data-stu-id="db191-464">Search events and logs</span></span>](app-insights-diagnostic-search.md)

* [<span data-ttu-id="db191-465">Dépannage</span><span class="sxs-lookup"><span data-stu-id="db191-465">Troubleshooting</span></span>](app-insights-troubleshoot-faq.md)


