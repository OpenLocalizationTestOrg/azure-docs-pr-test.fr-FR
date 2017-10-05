---
title: "API Application Insights pour les événements et les métriques personnalisés | Microsoft Docs"
description: "Insérez quelques lignes de code dans votre application de périphérique ou de bureau, votre page web ou votre service pour suivre l'utilisation et diagnostiquer les problèmes."
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
ms.openlocfilehash: e94c50de51612243386d89c5e0b3178a4f9cbd38
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="application-insights-api-for-custom-events-and-metrics"></a><span data-ttu-id="9e4e1-103">API Application Insights pour les événements et les mesures personnalisés</span><span class="sxs-lookup"><span data-stu-id="9e4e1-103">Application Insights API for custom events and metrics</span></span>

<span data-ttu-id="9e4e1-104">Insérez quelques lignes de code dans votre application pour découvrir ce qu’en font les utilisateurs ou pour faciliter le diagnostic des problèmes.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-104">Insert a few lines of code in your application to find out what users are doing with it, or to help diagnose issues.</span></span> <span data-ttu-id="9e4e1-105">Vous pouvez envoyer la télémétrie depuis des applications de périphérique et de bureau, des clients web et des serveurs web.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-105">You can send telemetry from device and desktop apps, web clients, and web servers.</span></span> <span data-ttu-id="9e4e1-106">Utilisez l’API des données de télémétrie principales [Azure Application Insights](app-insights-overview.md) pour envoyer des événements et métriques personnalisés, ainsi que vos propres versions de la télémétrie standard.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-106">Use the [Azure Application Insights](app-insights-overview.md) core telemetry API to send custom events and metrics, and your own versions of standard telemetry.</span></span> <span data-ttu-id="9e4e1-107">Cette API est la même que celle utilisée par les collecteurs de données standard d’Application Insights.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-107">This API is the same API that the standard Application Insights data collectors use.</span></span>

## <a name="api-summary"></a><span data-ttu-id="9e4e1-108">API summary</span><span class="sxs-lookup"><span data-stu-id="9e4e1-108">API summary</span></span>
<span data-ttu-id="9e4e1-109">L’API est uniforme sur toutes les plateformes, à l’exception de quelques petites variations.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-109">The API is uniform across all platforms, apart from a few small variations.</span></span>

| <span data-ttu-id="9e4e1-110">Méthode</span><span class="sxs-lookup"><span data-stu-id="9e4e1-110">Method</span></span> | <span data-ttu-id="9e4e1-111">Utilisé pour</span><span class="sxs-lookup"><span data-stu-id="9e4e1-111">Used for</span></span> |
| --- | --- |
| [`TrackPageView`](#page-views) |<span data-ttu-id="9e4e1-112">Pages, écrans, panneaux ou formes.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-112">Pages, screens, blades, or forms.</span></span> |
| [`TrackEvent`](#trackevent) |<span data-ttu-id="9e4e1-113">Actions de l’utilisateur et autres événements.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-113">User actions and other events.</span></span> <span data-ttu-id="9e4e1-114">Utilisé pour suivre le comportement de l’utilisateur ou pour analyser les performances.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-114">Used to track user behavior or to monitor performance.</span></span> |
| [`TrackMetric`](#trackmetric) |<span data-ttu-id="9e4e1-115">Mesures de performances telles que la longueur des files d’attente non liées à des événements spécifiques.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-115">Performance measurements such as queue lengths not related to specific events.</span></span> |
| [`TrackException`](#trackexception) |<span data-ttu-id="9e4e1-116">Exceptions de journal pour des diagnostics.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-116">Logging exceptions for diagnosis.</span></span> <span data-ttu-id="9e4e1-117">Effectuez un suivi lorsqu’ils se produisent par rapport à d’autres événements et examinez les arborescences des appels de procédure.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-117">Trace where they occur in relation to other events and examine stack traces.</span></span> |
| [`TrackRequest`](#trackrequest) |<span data-ttu-id="9e4e1-118">Notez la fréquence et la durée des requêtes du serveur pour l’analyse des performances.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-118">Logging the frequency and duration of server requests for performance analysis.</span></span> |
| [`TrackTrace`](#tracktrace) |<span data-ttu-id="9e4e1-119">Messages du journal de diagnostic</span><span class="sxs-lookup"><span data-stu-id="9e4e1-119">Diagnostic log messages.</span></span> <span data-ttu-id="9e4e1-120">Vous pouvez également capturer des journaux tiers.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-120">You can also capture third-party logs.</span></span> |
| [`TrackDependency`](#trackdependency) |<span data-ttu-id="9e4e1-121">La journalisation de la durée et de la fréquence des appels vers les composants externes dont dépend votre application.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-121">Logging the duration and frequency of calls to external components that your app depends on.</span></span> |

<span data-ttu-id="9e4e1-122">Vous pouvez [associer des propriétés et des mesures](#properties) à la plupart de ces appels de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-122">You can [attach properties and metrics](#properties) to most of these telemetry calls.</span></span>

## <span data-ttu-id="9e4e1-123"><a name="prep"></a>Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="9e4e1-123"><a name="prep"></a>Before you start</span></span>
<span data-ttu-id="9e4e1-124">Si vous n’avez pas encore de référence sur le kit SDK Application Insights :</span><span class="sxs-lookup"><span data-stu-id="9e4e1-124">If you don't have a reference on Application Insights SDK yet:</span></span>

* <span data-ttu-id="9e4e1-125">Ajoutez le Kit de développement logiciel (SDK) Application Insights à votre projet :</span><span class="sxs-lookup"><span data-stu-id="9e4e1-125">Add the Application Insights SDK to your project:</span></span>

  * [<span data-ttu-id="9e4e1-126">Projet ASP.NET</span><span class="sxs-lookup"><span data-stu-id="9e4e1-126">ASP.NET project</span></span>](app-insights-asp-net.md)
  * [<span data-ttu-id="9e4e1-127">Projet Java</span><span class="sxs-lookup"><span data-stu-id="9e4e1-127">Java project</span></span>](app-insights-java-get-started.md)
  * [<span data-ttu-id="9e4e1-128">JavaScript dans chaque page web</span><span class="sxs-lookup"><span data-stu-id="9e4e1-128">JavaScript in each webpage</span></span>](app-insights-javascript.md) 
* <span data-ttu-id="9e4e1-129">Ajoutez au code de votre périphérique ou de votre serveur web :</span><span class="sxs-lookup"><span data-stu-id="9e4e1-129">In your device or web server code, include:</span></span>

    <span data-ttu-id="9e4e1-130">*C# :* `using Microsoft.ApplicationInsights;`</span><span class="sxs-lookup"><span data-stu-id="9e4e1-130">*C#:* `using Microsoft.ApplicationInsights;`</span></span>

    <span data-ttu-id="9e4e1-131">*Visual Basic :* `Imports Microsoft.ApplicationInsights`</span><span class="sxs-lookup"><span data-stu-id="9e4e1-131">*Visual Basic:* `Imports Microsoft.ApplicationInsights`</span></span>

    <span data-ttu-id="9e4e1-132">*Java:* `import com.microsoft.applicationinsights.TelemetryClient;`</span><span class="sxs-lookup"><span data-stu-id="9e4e1-132">*Java:* `import com.microsoft.applicationinsights.TelemetryClient;`</span></span>

## <a name="constructing-a-telemetryclient-instance"></a><span data-ttu-id="9e4e1-133">Construction d’une instance de TelemetryClient</span><span class="sxs-lookup"><span data-stu-id="9e4e1-133">Constructing a TelemetryClient instance</span></span>
<span data-ttu-id="9e4e1-134">Construisez une instance de `TelemetryClient` (sauf en JavaScript dans les pages web) :</span><span class="sxs-lookup"><span data-stu-id="9e4e1-134">Construct an instance of `TelemetryClient` (except in JavaScript in webpages):</span></span>

<span data-ttu-id="9e4e1-135">*C#*</span><span class="sxs-lookup"><span data-stu-id="9e4e1-135">*C#*</span></span>

    private TelemetryClient telemetry = new TelemetryClient();

<span data-ttu-id="9e4e1-136">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="9e4e1-136">*Visual Basic*</span></span>

    Private Dim telemetry As New TelemetryClient

<span data-ttu-id="9e4e1-137">*Java*</span><span class="sxs-lookup"><span data-stu-id="9e4e1-137">*Java*</span></span>

    private TelemetryClient telemetry = new TelemetryClient();

<span data-ttu-id="9e4e1-138">TelemetryClient est thread-safe.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-138">TelemetryClient is thread-safe.</span></span>

<span data-ttu-id="9e4e1-139">Nous vous recommandons d’utiliser une instance de TelemetryClient pour chaque module de votre application.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-139">We recommend that you use an instance of TelemetryClient for each module of your app.</span></span> <span data-ttu-id="9e4e1-140">Par exemple, vous pouvez avoir une instance de TelemetryClient dans votre service web pour signaler les requêtes HTTP entrantes et une autre instance dans une classe d’intergiciels pour signaler les événements de logique métier.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-140">For instance, you may have one TelemetryClient instance in your web service to report incoming HTTP requests, and another in a middleware class to report business logic events.</span></span> <span data-ttu-id="9e4e1-141">Vous pouvez définir des propriétés telles que `TelemetryClient.Context.User.Id` pour assurer le suivi des utilisateurs et des sessions ou `TelemetryClient.Context.Device.Id` pour identifier l’ordinateur.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-141">You can set properties such as `TelemetryClient.Context.User.Id` to track users and sessions, or `TelemetryClient.Context.Device.Id` to identify the machine.</span></span> <span data-ttu-id="9e4e1-142">Cette information est associée à tous les événements envoyés par l'instance.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-142">This information is attached to all events that the instance sends.</span></span>

## <a name="trackevent"></a><span data-ttu-id="9e4e1-143">TrackEvent</span><span class="sxs-lookup"><span data-stu-id="9e4e1-143">TrackEvent</span></span>
<span data-ttu-id="9e4e1-144">Dans Application Insights, un *événement personnalisé* est un point de données que vous pouvez afficher dans [Metrics Explorer](app-insights-metrics-explorer.md) en tant que nombre agrégé et dans [Recherche de diagnostic](app-insights-diagnostic-search.md) en tant qu’occurrences individuelles.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-144">In Application Insights, a *custom event* is a data point that you can display in [Metrics Explorer](app-insights-metrics-explorer.md) as an aggregated count, and in [Diagnostic Search](app-insights-diagnostic-search.md) as individual occurrences.</span></span> <span data-ttu-id="9e4e1-145">(Il n’est pas lié à des « événements » de type MVC ou autres.)</span><span class="sxs-lookup"><span data-stu-id="9e4e1-145">(It isn't related to MVC or other framework "events.")</span></span>

<span data-ttu-id="9e4e1-146">Insérez des appels `TrackEvent` dans votre code pour compter les différents événements.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-146">Insert `TrackEvent` calls in your code to count various events.</span></span> <span data-ttu-id="9e4e1-147">Par exemple, la fréquence à laquelle les utilisateurs choisissent une fonctionnalité particulière, la fréquence à laquelle ils atteignent des objectifs particuliers ou à laquelle ils commettent éventuellement des types d’erreurs particuliers.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-147">How often users choose a particular feature, how often they achieve particular goals, or maybe how often they make particular types of mistakes.</span></span>

<span data-ttu-id="9e4e1-148">Par exemple, dans une application de jeu, envoyez un événement chaque fois qu'un utilisateur gagne le jeu :</span><span class="sxs-lookup"><span data-stu-id="9e4e1-148">For example, in a game app, send an event whenever a user wins the game:</span></span>

<span data-ttu-id="9e4e1-149">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="9e4e1-149">*JavaScript*</span></span>

    appInsights.trackEvent("WinGame");

<span data-ttu-id="9e4e1-150">*C#*</span><span class="sxs-lookup"><span data-stu-id="9e4e1-150">*C#*</span></span>

    telemetry.TrackEvent("WinGame");

<span data-ttu-id="9e4e1-151">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="9e4e1-151">*Visual Basic*</span></span>

    telemetry.TrackEvent("WinGame")

<span data-ttu-id="9e4e1-152">*Java*</span><span class="sxs-lookup"><span data-stu-id="9e4e1-152">*Java*</span></span>

    telemetry.trackEvent("WinGame");

### <a name="view-your-events-in-the-microsoft-azure-portal"></a><span data-ttu-id="9e4e1-153">Afficher vos événements sur le portail Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="9e4e1-153">View your events in the Microsoft Azure portal</span></span>
<span data-ttu-id="9e4e1-154">Pour voir un nombre de vos événements, ouvrez un panneau [Metrics Explorer](app-insights-metrics-explorer.md) , ajoutez un nouveau graphique, puis sélectionnez **Événements**.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-154">To see a count of your events, open a [Metrics Explorer](app-insights-metrics-explorer.md) blade, add a new chart, and select **Events**.</span></span>  

![Afficher un nombre d’événements personnalisés](./media/app-insights-api-custom-events-metrics/01-custom.png)

<span data-ttu-id="9e4e1-156">Pour comparer le nombre d'événements différents, définissez le type de graphique sur **Grille** et groupez par nom d'événement :</span><span class="sxs-lookup"><span data-stu-id="9e4e1-156">To compare the counts of different events, set the chart type to **Grid**, and group by event name:</span></span>

![Définition du type de graphique et du regroupement](./media/app-insights-api-custom-events-metrics/07-grid.png)

<span data-ttu-id="9e4e1-158">Dans la grille, cliquez sur un nom d'événement pour voir les occurrences individuelles de cet événement.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-158">On the grid, click through an event name to see individual occurrences of that event.</span></span> <span data-ttu-id="9e4e1-159">Pour afficher plus de détails, cliquez sur n’importe quelle occurrence de la liste.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-159">To see more detail - click any occurrence in the list.</span></span>

![Extrayez les événements](./media/app-insights-api-custom-events-metrics/03-instances.png)

<span data-ttu-id="9e4e1-161">Pour vous concentrer sur des événements spécifiques dans la recherche ou Metrics Explorer, définissez le filtre du panneau sur les noms d'événements qui vous intéressent :</span><span class="sxs-lookup"><span data-stu-id="9e4e1-161">To focus on specific events in either Search or Metrics Explorer, set the blade's filter to the event names that you're interested in:</span></span>

![Ouvrez Filtres, développez Nom de l'événement et sélectionnez une ou plusieurs valeurs](./media/app-insights-api-custom-events-metrics/06-filter.png)

### <a name="custom-events-in-analytics"></a><span data-ttu-id="9e4e1-163">Événements personnalisés dans l’analytique</span><span class="sxs-lookup"><span data-stu-id="9e4e1-163">Custom events in Analytics</span></span>

<span data-ttu-id="9e4e1-164">La télémétrie est disponible dans la table `customEvents` dans [Application Insights - Analytique](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="9e4e1-164">The telemetry is available in the `customEvents` table in [Application Insights Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="9e4e1-165">Chaque ligne représente un appel à `trackEvent(..)` dans votre application.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-165">Each row represents a call to `trackEvent(..)` in your app.</span></span> 

<span data-ttu-id="9e4e1-166">Si un [échantillonnage](app-insights-sampling.md) est en cours, la propriété itemCount affiche une valeur supérieure à 1.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-166">If [sampling](app-insights-sampling.md) is in operation, the itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="9e4e1-167">Par exemple, itemCount==10 signifie que sur 10 appels à trackEvent(), le processus d’échantillonnage n’en a transmis qu’un seul.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-167">For example itemCount==10 means that of 10 calls to trackEvent(), the sampling process only transmitted one of them.</span></span> <span data-ttu-id="9e4e1-168">Pour obtenir un nombre correct d’événements personnalisés, vous devez utiliser un code similaire à `customEvent | summarize sum(itemCount)`.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-168">To get a correct count of custom events, you should use therefore use code such as `customEvent | summarize sum(itemCount)`.</span></span>


## <a name="trackmetric"></a><span data-ttu-id="9e4e1-169">TrackMetric</span><span class="sxs-lookup"><span data-stu-id="9e4e1-169">TrackMetric</span></span>

<span data-ttu-id="9e4e1-170">Application Insight peut représenter des mesures qui ne sont pas associées à des événements particuliers.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-170">Application Insights can chart metrics that are not attached to particular events.</span></span> <span data-ttu-id="9e4e1-171">Par exemple, vous pouvez analyser la longueur d’une file d'attente à des intervalles réguliers.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-171">For example, you could monitor a queue length at regular intervals.</span></span> <span data-ttu-id="9e4e1-172">Avec les mesures, les mesures individuelles sont moins intéressantes que les variations et tendances, ainsi les graphiques statistiques sont utiles.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-172">With metrics, the individual measurements are of less interest than the variations and trends, and so statistical charts are useful.</span></span>

<span data-ttu-id="9e4e1-173">Pour pouvoir envoyer des métriques à Application Insights, vous pouvez utiliser l’API `TrackMetric(..)`.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-173">In order to send metrics to Application Insights, you can use the `TrackMetric(..)` API.</span></span> <span data-ttu-id="9e4e1-174">Il existe deux façons d’envoyer une métrique :</span><span class="sxs-lookup"><span data-stu-id="9e4e1-174">There are two ways to send a metric:</span></span> 

* <span data-ttu-id="9e4e1-175">Valeur unique.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-175">Single value.</span></span> <span data-ttu-id="9e4e1-176">Chaque fois que vous effectuez une mesure dans votre application, vous envoyez la valeur correspondante à Application Insights.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-176">Every time you perform a measurement in your application, you send the corresponding value to Application Insights.</span></span> <span data-ttu-id="9e4e1-177">Par exemple, supposons que vous avez une mesure décrivant le nombre d’éléments dans un conteneur.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-177">For example, assume that you have a metric describing the number of items in a container.</span></span> <span data-ttu-id="9e4e1-178">Pendant une période donnée, vous placez d’abord trois éléments dans le conteneur puis vous en supprimez deux.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-178">During a particular time period, you first put three items into the container and then you remove two items.</span></span> <span data-ttu-id="9e4e1-179">En conséquence, vous appelez `TrackMetric` à deux reprises : d’abord en passant la valeur `3` puis la valeur `-2`.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-179">Accordingly, you would call `TrackMetric` twice: first passing the value `3` and then the value `-2`.</span></span> <span data-ttu-id="9e4e1-180">Application Insights stocke les deux valeurs pour votre compte.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-180">Application Insights stores both values on your behalf.</span></span> 

* <span data-ttu-id="9e4e1-181">Agrégation.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-181">Aggregation.</span></span> <span data-ttu-id="9e4e1-182">Quand vous travaillez avec des métriques, chaque mesure individuelle est rarement intéressante.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-182">When working with metrics, every single measurement is rarely of interest.</span></span> <span data-ttu-id="9e4e1-183">Au lieu de cela, un récapitulatif de ce qui s’est passé au cours d’une période donnée est important.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-183">Instead a summary of what happened during a particular time period is important.</span></span> <span data-ttu-id="9e4e1-184">Un tel récapitulatif est appelé _agrégation_.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-184">Such a summary is called _aggregation_.</span></span> <span data-ttu-id="9e4e1-185">Dans l’exemple ci-dessus, la somme totale des métriques pour cette période est `1` et le nombre de valeurs des métriques est `2`.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-185">In the above example, the aggregate metric sum for that time period is `1` and the count of the metric values is `2`.</span></span> <span data-ttu-id="9e4e1-186">Quand vous utilisez l’approche par agrégation, vous appelez `TrackMetric` une seule fois par période et vous envoyez les valeurs agrégées.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-186">When using the aggregation approach, you only invoke `TrackMetric` once per time period and send the aggregate values.</span></span> <span data-ttu-id="9e4e1-187">C’est l’approche recommandée, car elle peut réduire considérablement le coût et les problèmes de performances en envoyant moins de points de données à Application Insights, tout en collectant néanmoins toutes les informations pertinentes.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-187">This is the recommended approach since it can significantly reduce the cost and performance overhead by sending fewer data points to Application Insights, while still collecting all relevant information.</span></span>

### <a name="examples"></a><span data-ttu-id="9e4e1-188">Exemples :</span><span class="sxs-lookup"><span data-stu-id="9e4e1-188">Examples:</span></span>

#### <a name="single-values"></a><span data-ttu-id="9e4e1-189">Valeurs uniques</span><span class="sxs-lookup"><span data-stu-id="9e4e1-189">Single values</span></span>

<span data-ttu-id="9e4e1-190">Pour envoyer une seule valeur métrique :</span><span class="sxs-lookup"><span data-stu-id="9e4e1-190">To send a single metric value:</span></span>

<span data-ttu-id="9e4e1-191">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="9e4e1-191">*JavaScript*</span></span>

 ```Javascript
     appInsights.trackMetric("queueLength", 42.0);
 ```

<span data-ttu-id="9e4e1-192">*C#, Java*</span><span class="sxs-lookup"><span data-stu-id="9e4e1-192">*C#, Java*</span></span>

```C#
    var sample = new MetricTelemetry();
    sample.Name = "metric name";
    sample.Value = 42.3;
    telemetryClient.TrackMetric(sample);
```

#### <a name="aggregating-metrics"></a><span data-ttu-id="9e4e1-193">Agrégation des métriques</span><span class="sxs-lookup"><span data-stu-id="9e4e1-193">Aggregating metrics</span></span>

<span data-ttu-id="9e4e1-194">Il est recommandé d’agréger les mesures avant de les envoyer à partir de votre application, de façon à réduire la bande passante et le coût, et à améliorer les performances.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-194">It is recommended to aggregate metrics before sending them from your app, to reduce bandwidth, cost and to improve performance.</span></span>
<span data-ttu-id="9e4e1-195">Voici un exemple de code d’agrégation :</span><span class="sxs-lookup"><span data-stu-id="9e4e1-195">Here is an example of aggregating code:</span></span>

<span data-ttu-id="9e4e1-196">*C#*</span><span class="sxs-lookup"><span data-stu-id="9e4e1-196">*C#*</span></span>

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
    /// Accepts metric values and sends the aggregated values at 1-minute intervals.
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
                    // Wait for end end of the aggregation period:
                    await Task.Delay(AggregationPeriod).ConfigureAwait(continueOnCapturedContext: false);

                    // Atomically snap the current aggregation:
                    MetricAggregator nextAggregator = new MetricAggregator(DateTimeOffset.UtcNow);
                    MetricAggregator prevAggregator = Interlocked.Exchange(ref _aggregator, nextAggregator);

                    // Only send anything is at least one value was measured:
                    if (prevAggregator != null && prevAggregator.Count > 0)
                    {
                        // Compute the actual aggregation period length:
                        TimeSpan aggPeriod = nextAggregator.StartTimestamp - prevAggregator.StartTimestamp;
                        if (aggPeriod.TotalMilliseconds < 1)
                        {
                            aggPeriod = TimeSpan.FromMilliseconds(1);
                        }

                        // Construct the metric telemetry item and send:
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

### <a name="custom-metrics-in-metrics-explorer"></a><span data-ttu-id="9e4e1-197">Métriques personnalisées dans Metrics Explorer</span><span class="sxs-lookup"><span data-stu-id="9e4e1-197">Custom metrics in Metrics Explorer</span></span>

<span data-ttu-id="9e4e1-198">Pour afficher les résultats, ouvrez Metrics Explorer et ajoutez un nouveau graphique.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-198">To see the results, open Metrics Explorer and add a new chart.</span></span> <span data-ttu-id="9e4e1-199">Modifiez le graphique pour afficher votre mesure.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-199">Edit the chart to show your metric.</span></span>

> [!NOTE]
> <span data-ttu-id="9e4e1-200">L’affichage de votre mesure personnalisée dans la liste des mesures disponibles peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-200">Your custom metric might take several minutes to appear in the list of available metrics.</span></span>
>

![Ajouter un nouveau graphique ou sélectionnez un graphique et sélectionnez votre métrique sous Personnalisé](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

### <a name="custom-metrics-in-analytics"></a><span data-ttu-id="9e4e1-202">Métriques personnalisées dans Analytics</span><span class="sxs-lookup"><span data-stu-id="9e4e1-202">Custom metrics in Analytics</span></span>

<span data-ttu-id="9e4e1-203">La télémétrie est disponible dans la table `customMetrics` dans [Application Insights - Analytique](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="9e4e1-203">The telemetry is available in the `customMetrics` table in [Application Insights Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="9e4e1-204">Chaque ligne représente un appel à `trackMetric(..)` dans votre application.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-204">Each row represents a call to `trackMetric(..)` in your app.</span></span>
* <span data-ttu-id="9e4e1-205">`valueSum` - Il s’agit de la somme des mesures.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-205">`valueSum` - This is the sum of the measurements.</span></span> <span data-ttu-id="9e4e1-206">Pour obtenir la valeur moyenne, divisez par `valueCount`.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-206">To get the mean value, divide by `valueCount`.</span></span>
* <span data-ttu-id="9e4e1-207">`valueCount` : le nombre de mesures qui ont été agrégées dans cet appel de `trackMetric(..)`.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-207">`valueCount` - The number of measurements that were aggregated into this `trackMetric(..)` call.</span></span>

## <a name="page-views"></a><span data-ttu-id="9e4e1-208">Affichages de page</span><span class="sxs-lookup"><span data-stu-id="9e4e1-208">Page views</span></span>
<span data-ttu-id="9e4e1-209">Dans un périphérique ou une application de page web, la télémétrie d'affichage de page est envoyée par défaut lorsque chaque écran ou page est chargé.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-209">In a device or webpage app, page view telemetry is sent by default when each screen or page is loaded.</span></span> <span data-ttu-id="9e4e1-210">Mais vous pouvez modifier cela pour suivre les affichages de page à différents moments.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-210">But you can change that to track page views at additional or different times.</span></span> <span data-ttu-id="9e4e1-211">Par exemple, dans une application qui affiche les onglets ou les panneaux, vous pouvez effectuer le suivi d'une « page » chaque fois que l'utilisateur ouvre un nouveau panneau.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-211">For example, in an app that displays tabs or blades, you might want to track a page whenever the user opens a new blade.</span></span>

![Filtre d'utilisation dans le panneau Vue d'ensemble](./media/app-insights-api-custom-events-metrics/appinsights-47usage-2.png)

<span data-ttu-id="9e4e1-213">Les données d’utilisateur et de session sont envoyées en tant que propriétés avec les affichages de page, de façon à ce que les graphiques d’utilisateur et de session soient actifs s’il existe une télémétrie de l’affichage de page.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-213">User and session data is sent as properties along with page views, so the user and session charts come alive when there is page view telemetry.</span></span>

### <a name="custom-page-views"></a><span data-ttu-id="9e4e1-214">Affichages de pages personnalisées</span><span class="sxs-lookup"><span data-stu-id="9e4e1-214">Custom page views</span></span>
<span data-ttu-id="9e4e1-215">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="9e4e1-215">*JavaScript*</span></span>

    appInsights.trackPageView("tab1");

<span data-ttu-id="9e4e1-216">*C#*</span><span class="sxs-lookup"><span data-stu-id="9e4e1-216">*C#*</span></span>

    telemetry.TrackPageView("GameReviewPage");

<span data-ttu-id="9e4e1-217">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="9e4e1-217">*Visual Basic*</span></span>

    telemetry.TrackPageView("GameReviewPage")


<span data-ttu-id="9e4e1-218">Si vous avez plusieurs onglets dans différentes pages HTML, vous pouvez aussi spécifier l'URL :</span><span class="sxs-lookup"><span data-stu-id="9e4e1-218">If you have several tabs within different HTML pages, you can specify the URL too:</span></span>

    appInsights.trackPageView("tab1", "http://fabrikam.com/page1.htm");

### <a name="timing-page-views"></a><span data-ttu-id="9e4e1-219">Affichages de la page de durée</span><span class="sxs-lookup"><span data-stu-id="9e4e1-219">Timing page views</span></span>
<span data-ttu-id="9e4e1-220">Par défaut, les heures déclarées **Temps de chargement de l’affichage de la page** sont mesurées à partir du moment où le navigateur envoie la demande, jusqu’à ce que l’événement de chargement de la page du navigateur soit appelé.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-220">By default, the times reported as **Page view load time** are measured from when the browser sends the request, until the browser's page load event is called.</span></span>

<span data-ttu-id="9e4e1-221">Au lieu de cela, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="9e4e1-221">Instead, you can either:</span></span>

* <span data-ttu-id="9e4e1-222">Définir une durée explicite dans l’appel [trackPageView](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#trackpageview) : `appInsights.trackPageView("tab1", null, null, null, durationInMilliseconds);`.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-222">Set an explicit duration in the [trackPageView](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#trackpageview) call: `appInsights.trackPageView("tab1", null, null, null, durationInMilliseconds);`.</span></span>
* <span data-ttu-id="9e4e1-223">Utiliser les appels de minutage d’affichage de la page `startTrackPage` et `stopTrackPage`.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-223">Use the page view timing calls `startTrackPage` and `stopTrackPage`.</span></span>

<span data-ttu-id="9e4e1-224">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="9e4e1-224">*JavaScript*</span></span>

    // To start timing a page:
    appInsights.startTrackPage("Page1");

<span data-ttu-id="9e4e1-225">...</span><span class="sxs-lookup"><span data-stu-id="9e4e1-225">...</span></span>

    // To stop timing and log the page:
    appInsights.stopTrackPage("Page1", url, properties, measurements);

<span data-ttu-id="9e4e1-226">Le nom que vous utilisez comme premier paramètre associe les appels de démarrage et d’arrêt.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-226">The name that you use as the first parameter associates the start and stop calls.</span></span> <span data-ttu-id="9e4e1-227">Le nom de la page actuelle est utilisé par défaut.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-227">It defaults to the current page name.</span></span>

<span data-ttu-id="9e4e1-228">Les durées de chargement de la page résultantes affichées dans Metrics Explorer sont dérivées de l’intervalle entre les appels de démarrage et d’arrêt.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-228">The resulting page load durations displayed in Metrics Explorer are derived from the interval between the start and stop calls.</span></span> <span data-ttu-id="9e4e1-229">C’est à vous de décider quel intervalle de temps vous voulez mesurer.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-229">It's up to you what interval you actually time.</span></span>

### <a name="page-telemetry-in-analytics"></a><span data-ttu-id="9e4e1-230">Télémétrie des pages dans Analytique</span><span class="sxs-lookup"><span data-stu-id="9e4e1-230">Page telemetry in Analytics</span></span>

<span data-ttu-id="9e4e1-231">Dans [Analytique](app-insights-analytics.md), deux tables affichent les données des opérations du navigateur :</span><span class="sxs-lookup"><span data-stu-id="9e4e1-231">In [Analytics](app-insights-analytics.md) two tables show data from browser operations:</span></span>

* <span data-ttu-id="9e4e1-232">La table `pageViews` contient des données sur l’URL et le titre de la page.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-232">The `pageViews` table contains data about the URL and page title</span></span>
* <span data-ttu-id="9e4e1-233">La table `browserTimings` contient des données sur les performances du client, comme le temps nécessaire pour traiter les données entrantes.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-233">The `browserTimings` table contains data about client performance, such as the time taken to process the incoming data</span></span>

<span data-ttu-id="9e4e1-234">Pour trouver le temps mis par le navigateur pour traiter différentes pages :</span><span class="sxs-lookup"><span data-stu-id="9e4e1-234">To find how long the browser takes to process different pages:</span></span>

```
browserTimings | summarize avg(networkDuration), avg(processingDuration), avg(totalDuration) by name 
```

<span data-ttu-id="9e4e1-235">Pour découvrir la popularité de différents navigateurs :</span><span class="sxs-lookup"><span data-stu-id="9e4e1-235">To discover the popularities of different browsers:</span></span>

```
pageViews | summarize count() by client_Browser
```

<span data-ttu-id="9e4e1-236">Pour associer des vues de pages à des appels AJAX, joindre à des dépendances :</span><span class="sxs-lookup"><span data-stu-id="9e4e1-236">To associate page views to AJAX calls, join with dependencies:</span></span>

```
pageViews | join (dependencies) on operation_Id 
```

## <a name="trackrequest"></a><span data-ttu-id="9e4e1-237">TrackRequest</span><span class="sxs-lookup"><span data-stu-id="9e4e1-237">TrackRequest</span></span>
<span data-ttu-id="9e4e1-238">Le kit de développement logiciel de serveur utilise TrackRequest pour consigner les requêtes HTTP.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-238">The server SDK uses TrackRequest to log HTTP requests.</span></span>

<span data-ttu-id="9e4e1-239">Vous pouvez également l'appeler vous-même si vous souhaitez simuler des requêtes dans le cas où le module du service web n’est pas en cours d'exécution.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-239">You can also call it yourself if you want to simulate requests in a context where you don't have the web service module running.</span></span>

<span data-ttu-id="9e4e1-240">Toutefois, le moyen recommandé d’envoyer la télémétrie de la demande est là où la demande agit comme un <a href="#operation-context">contexte d’opération</a>.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-240">However, the recommended way to send request telemetry is where the request acts as an <a href="#operation-context">operation context</a>.</span></span>

## <a name="operation-context"></a><span data-ttu-id="9e4e1-241">Contexte de l’opération</span><span class="sxs-lookup"><span data-stu-id="9e4e1-241">Operation context</span></span>
<span data-ttu-id="9e4e1-242">Vous pouvez associer les éléments de télémétrie en leur joignant un ID d’opération commun.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-242">You can associate telemetry items together by attaching to them a common operation ID.</span></span> <span data-ttu-id="9e4e1-243">Le module de suivi de requête standard effectue cette opération pour les exceptions et les autres événements envoyés lors du traitement d’une requête HTTP.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-243">The standard request-tracking module does this for exceptions and other events that are sent while an HTTP request is being processed.</span></span> <span data-ttu-id="9e4e1-244">Dans [Recherche](app-insights-diagnostic-search.md) et [Analytique](app-insights-analytics.md), vous pouvez utiliser l’ID pour trouver facilement tous les événements associés à la requête.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-244">In [Search](app-insights-diagnostic-search.md) and [Analytics](app-insights-analytics.md), you can use the ID to easily find any events associated with the request.</span></span>

<span data-ttu-id="9e4e1-245">Pour définir l’ID, le plus simple consiste à définir un contexte d’opération à l’aide de ce modèle :</span><span class="sxs-lookup"><span data-stu-id="9e4e1-245">The easiest way to set the ID is to set an operation context by using this pattern:</span></span>

<span data-ttu-id="9e4e1-246">*C#*</span><span class="sxs-lookup"><span data-stu-id="9e4e1-246">*C#*</span></span>

```C#
// Establish an operation context and associated telemetry item:
using (var operation = telemetry.StartOperation<RequestTelemetry>("operationName"))
{
    // Telemetry sent in here will use the same operation ID.
    ...
    telemetry.TrackTrace(...); // or other Track* calls
    ...
    // Set properties of containing telemetry item--for example:
    operation.Telemetry.ResponseCode = "200";

    // Optional: explicitly send telemetry item:
    telemetry.StopOperation(operation);

} // When operation is disposed, telemetry item is sent.
```

<span data-ttu-id="9e4e1-247">Outre la définition d’un contexte d’opération, `StartOperation` crée un élément de télémétrie du type que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-247">Along with setting an operation context, `StartOperation` creates a telemetry item of the type that you specify.</span></span> <span data-ttu-id="9e4e1-248">Il envoie l’élément de télémétrie lorsque vous libérez l’opération, ou si vous appelez explicitement `StopOperation`.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-248">It sends the telemetry item when you dispose the operation, or if you explicitly call `StopOperation`.</span></span> <span data-ttu-id="9e4e1-249">Si vous utilisez `RequestTelemetry` comme type de télémétrie, alors sa durée est définie sur l’intervalle compris entre le début et la fin.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-249">If you use `RequestTelemetry` as the telemetry type, its duration is set to the timed interval between start and stop.</span></span>

<span data-ttu-id="9e4e1-250">Les contextes de l’opération ne peuvent pas être imbriqués.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-250">Operation contexts can't be nested.</span></span> <span data-ttu-id="9e4e1-251">S’il existe déjà un contexte d’opération, son ID est associé à tous les éléments de contenu, y compris l’élément créé avec `StartOperation`.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-251">If there is already an operation context, then its ID is associated with all the contained items, including the item created with `StartOperation`.</span></span>

<span data-ttu-id="9e4e1-252">Dans Recherche, le contexte d’opération est utilisé pour créer la liste **Éléments connexes** :</span><span class="sxs-lookup"><span data-stu-id="9e4e1-252">In Search, the operation context is used to create the **Related Items** list:</span></span>

![Éléments connexes](./media/app-insights-api-custom-events-metrics/21.png)

<span data-ttu-id="9e4e1-254">Pour plus d’informations sur le suivi des opérations personnalisées, consultez [application-insights-custom-operations-tracking.md].</span><span class="sxs-lookup"><span data-stu-id="9e4e1-254">See [application-insights-custom-operations-tracking.md] for more information on custom operations tracking.</span></span>

### <a name="requests-in-analytics"></a><span data-ttu-id="9e4e1-255">Requêtes dans Analytique</span><span class="sxs-lookup"><span data-stu-id="9e4e1-255">Requests in Analytics</span></span> 

<span data-ttu-id="9e4e1-256">Dans [Application Insights - Analytique](app-insights-analytics.md), les demandes s’affichent dans la table `requests`.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-256">In [Application Insights Analytics](app-insights-analytics.md), requests show up in the `requests` table.</span></span>

<span data-ttu-id="9e4e1-257">Si [l’échantillonnage](app-insights-sampling.md) est en cours, la propriété itemCount affiche une valeur supérieure à 1.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-257">If [sampling](app-insights-sampling.md) is in operation, the itemCount property will show a value greater than 1.</span></span> <span data-ttu-id="9e4e1-258">Par exemple, itemCount==10 signifie que sur 10 appels à trackRequest(), le processus d’échantillonnage n’en a transmis qu’un seul.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-258">For example itemCount==10 means that of 10 calls to trackRequest(), the sampling process only transmitted one of them.</span></span> <span data-ttu-id="9e4e1-259">Pour obtenir un nombre correct de demandes et une durée moyenne segmentée par nom des demandes, utilisez un code similaire à celui-ci :</span><span class="sxs-lookup"><span data-stu-id="9e4e1-259">To get a correct count of requests and average duration segmented by request names, use code such as:</span></span>

```AIQL
requests | summarize count = sum(itemCount), avgduration = avg(duration) by name
```


## <a name="trackexception"></a><span data-ttu-id="9e4e1-260">TrackException</span><span class="sxs-lookup"><span data-stu-id="9e4e1-260">TrackException</span></span>
<span data-ttu-id="9e4e1-261">Envoi d’exceptions à Application Insights :</span><span class="sxs-lookup"><span data-stu-id="9e4e1-261">Send exceptions to Application Insights:</span></span>

* <span data-ttu-id="9e4e1-262">Pour [les compter](app-insights-metrics-explorer.md), comme une indication de la fréquence d’un problème.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-262">To [count them](app-insights-metrics-explorer.md), as an indication of the frequency of a problem.</span></span>
* <span data-ttu-id="9e4e1-263">Pour [inspecter les occurrences individuelles](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="9e4e1-263">To [examine individual occurrences](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="9e4e1-264">Les rapports incluent des arborescences des appels de procédure.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-264">The reports include the stack traces.</span></span>

<span data-ttu-id="9e4e1-265">*C#*</span><span class="sxs-lookup"><span data-stu-id="9e4e1-265">*C#*</span></span>

    try
    {
        ...
    }
    catch (Exception ex)
    {
       telemetry.TrackException(ex);
    }

<span data-ttu-id="9e4e1-266">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="9e4e1-266">*JavaScript*</span></span>

    try
    {
       ...
    }
    catch (ex)
    {
       appInsights.trackException(ex);
    }

<span data-ttu-id="9e4e1-267">Les Kits de développement logiciel (SDK) interceptent de nombreuses exceptions automatiquement, ce qui vous évite ainsi d’avoir toujours à appeler TrackException explicitement.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-267">The SDKs catch many exceptions automatically, so you don't always have to call TrackException explicitly.</span></span>

* <span data-ttu-id="9e4e1-268">ASP.NET : [écriture d'un code pour intercepter les exceptions](app-insights-asp-net-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="9e4e1-268">ASP.NET: [Write code to catch exceptions](app-insights-asp-net-exceptions.md).</span></span>
* <span data-ttu-id="9e4e1-269">J2EE : [les exceptions sont interceptées automatiquement](app-insights-java-get-started.md#exceptions-and-request-failures).</span><span class="sxs-lookup"><span data-stu-id="9e4e1-269">J2EE: [Exceptions are caught automatically](app-insights-java-get-started.md#exceptions-and-request-failures).</span></span>
* <span data-ttu-id="9e4e1-270">JavaScript : les exceptions sont interceptées automatiquement.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-270">JavaScript: Exceptions are caught automatically.</span></span> <span data-ttu-id="9e4e1-271">Si vous souhaitez désactiver la collecte automatique, ajoutez une ligne dans l'extrait de code que vous insérez dans vos pages web :</span><span class="sxs-lookup"><span data-stu-id="9e4e1-271">If you want to disable automatic collection, add a line to the code snippet that you insert in your webpages:</span></span>

    ```
    ({
      instrumentationKey: "your key"
      , disableExceptionTracking: true
    })
    ```

### <a name="exceptions-in-analytics"></a><span data-ttu-id="9e4e1-272">Exceptions dans Analytique</span><span class="sxs-lookup"><span data-stu-id="9e4e1-272">Exceptions in Analytics</span></span>

<span data-ttu-id="9e4e1-273">Dans [Application Insights - Analytique](app-insights-analytics.md), les exceptions s’affichent dans la table `exceptions`.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-273">In [Application Insights Analytics](app-insights-analytics.md), exceptions show up in the `exceptions` table.</span></span>

<span data-ttu-id="9e4e1-274">Si un [échantillonnage](app-insights-sampling.md) est en cours, la propriété `itemCount` affiche une valeur supérieure à 1.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-274">If [sampling](app-insights-sampling.md) is in operation, the `itemCount` property shows a value greater than 1.</span></span> <span data-ttu-id="9e4e1-275">Par exemple, itemCount==10 signifie que sur 10 appels à trackException(), le processus d’échantillonnage n’en a transmis qu’un seul.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-275">For example itemCount==10 means that of 10 calls to trackException(), the sampling process only transmitted one of them.</span></span> <span data-ttu-id="9e4e1-276">Pour obtenir un nombre correct d’exceptions segmentées par type d’exception, utilisez un code similaire à celui-ci :</span><span class="sxs-lookup"><span data-stu-id="9e4e1-276">To get a correct count of exceptions segmented by type of exception, use code such as:</span></span>

```
exceptions | summarize sum(itemCount) by type
```

<span data-ttu-id="9e4e1-277">La plupart des informations importantes sur la pile sont déjà extraites dans des variables distinctes, mais vous pouvez extraire séparément la structure `details` pour en savoir plus.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-277">Most of the important stack information is already extracted into separate variables, but you can pull apart the `details` structure to get more.</span></span> <span data-ttu-id="9e4e1-278">Comme cette structure est dynamique, vous devez effectuer une conversion de type (transtypage) du résultat vers le type attendu.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-278">Since this structure is dynamic, you should cast the result to the type you expect.</span></span> <span data-ttu-id="9e4e1-279">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="9e4e1-279">For example:</span></span>

```AIQL
exceptions
| extend method2 = tostring(details[0].parsedStack[1].method)
```

<span data-ttu-id="9e4e1-280">Pour associer des exceptions aux demandes qui s’y rapportent, utilisez une jointure :</span><span class="sxs-lookup"><span data-stu-id="9e4e1-280">To associate exceptions with their related requests, use a join:</span></span>

```
exceptions
| join (requests) on operation_Id 
```

## <a name="tracktrace"></a><span data-ttu-id="9e4e1-281">TrackTrace</span><span class="sxs-lookup"><span data-stu-id="9e4e1-281">TrackTrace</span></span>
<span data-ttu-id="9e4e1-282">Utilisez TrackTrace pour diagnostiquer des problèmes en envoyant une « piste de navigation » à Application Insights.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-282">Use TrackTrace to help diagnose problems by sending a "breadcrumb trail" to Application Insights.</span></span> <span data-ttu-id="9e4e1-283">Vous pouvez envoyer des blocs de données de diagnostic et les examiner dans la [Recherche de diagnostic](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="9e4e1-283">You can send chunks of diagnostic data and inspect them in [Diagnostic Search](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="9e4e1-284">Les [adaptateurs de journaux](app-insights-asp-net-trace-logs.md) utilisent cette API pour envoyer des journaux tiers au portail.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-284">[Log adapters](app-insights-asp-net-trace-logs.md) use this API to send third-party logs to the portal.</span></span>

<span data-ttu-id="9e4e1-285">*C#*</span><span class="sxs-lookup"><span data-stu-id="9e4e1-285">*C#*</span></span>

    telemetry.TrackTrace(message, SeverityLevel.Warning, properties);


<span data-ttu-id="9e4e1-286">Vous pouvez effectuer une recherche dans le contenu du message, mais (contrairement aux valeurs de propriété), vous ne pouvez pas les filtrer.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-286">You can search on message content, but (unlike property values) you can't filter on it.</span></span>

<span data-ttu-id="9e4e1-287">La limite de taille sur `message` est plus importante que la limite des propriétés.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-287">The size limit on `message` is much higher than the limit on properties.</span></span>
<span data-ttu-id="9e4e1-288">l’un des avantages de TrackTrace est que vous pouvez insérer des données relativement longues dans le message.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-288">An advantage of TrackTrace is that you can put relatively long data in the message.</span></span> <span data-ttu-id="9e4e1-289">Par exemple, vous pourriez y encoder des données POST.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-289">For example, you can encode POST data there.</span></span>  

<span data-ttu-id="9e4e1-290">Par ailleurs, vous pouvez ajouter un niveau de gravité à votre message.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-290">In addition, you can add a severity level to your message.</span></span> <span data-ttu-id="9e4e1-291">Comme pour les autres données de télémétrie, vous pouvez également ajouter des valeurs de propriété qui permettent de filtrer ou rechercher différents jeux de traces.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-291">And, like other telemetry, you can add property values to help you filter or search for different sets of traces.</span></span> <span data-ttu-id="9e4e1-292">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="9e4e1-292">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

<span data-ttu-id="9e4e1-293">Dans [Recherche](app-insights-diagnostic-search.md), vous pouvez filtrer facilement tous les messages d’un niveau de gravité particulier portant sur une certaine base de données.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-293">In [Search](app-insights-diagnostic-search.md), you can then easily filter out all the messages of a particular severity level that relate to a particular database.</span></span>


### <a name="traces-in-analytics"></a><span data-ttu-id="9e4e1-294">Traces dans Analytique</span><span class="sxs-lookup"><span data-stu-id="9e4e1-294">Traces in Analytics</span></span>

<span data-ttu-id="9e4e1-295">Dans [Application Insights - Analytique](app-insights-analytics.md), les appels à TrackTrace s’affichent dans la table `traces`.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-295">In [Application Insights Analytics](app-insights-analytics.md), calls to TrackTrace show up in the `traces` table.</span></span>

<span data-ttu-id="9e4e1-296">Si un [échantillonnage](app-insights-sampling.md) est en cours, la propriété itemCount affiche une valeur supérieure à 1.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-296">If [sampling](app-insights-sampling.md) is in operation, the itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="9e4e1-297">Par exemple, itemCount==10 signifie que sur 10 appels à `trackTrace()`, le processus d’échantillonnage n’en a transmis qu’un seul.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-297">For example itemCount==10 means that of 10 calls to `trackTrace()`, the sampling process only transmitted one of them.</span></span> <span data-ttu-id="9e4e1-298">Pour obtenir un nombre correct d’appels de trace, vous devez utiliser un code similaire à `traces | summarize sum(itemCount)`.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-298">To get a correct count of trace calls, you should use therefore code such as `traces | summarize sum(itemCount)`.</span></span>

## <a name="trackdependency"></a><span data-ttu-id="9e4e1-299">TrackDependency</span><span class="sxs-lookup"><span data-stu-id="9e4e1-299">TrackDependency</span></span>
<span data-ttu-id="9e4e1-300">Utilisez l’appel à TrackDependency pour suivre les temps de réponse et les taux de réussite des appels vers un bloc de code externe.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-300">Use the TrackDependency call to track the response times and success rates of calls to an external piece of code.</span></span> <span data-ttu-id="9e4e1-301">Les résultats s'affichent dans les graphiques de dépendance sur le portail.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-301">The results appear in the dependency charts in the portal.</span></span>

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

<span data-ttu-id="9e4e1-302">N’oubliez pas que les kits SDK de serveur incluent un [module de dépendance](app-insights-asp-net-dependencies.md) qui détecte certains appels de dépendance et en effectue le suivi automatiquement. C’est notamment le cas des bases de données et des API REST.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-302">Remember that the server SDKs include a [dependency module](app-insights-asp-net-dependencies.md) that discovers and tracks certain dependency calls automatically--for example, to databases and REST APIs.</span></span> <span data-ttu-id="9e4e1-303">Vous devez installer un agent sur votre serveur pour que le module fonctionne.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-303">You have to install an agent on your server to make the module work.</span></span> <span data-ttu-id="9e4e1-304">Vous utiliserez cet appel si vous souhaitez effectuer le suivi des appels qui ne sont pas interceptés par le système de suivi automatisé, ou si vous ne souhaitez pas installer l'agent.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-304">You use this call if you want to track calls that the automated tracking doesn't catch, or if you don't want to install the agent.</span></span>

<span data-ttu-id="9e4e1-305">Pour désactiver le module de suivi des dépendances standard, modifiez le fichier [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) et supprimez la référence à `DependencyCollector.DependencyTrackingTelemetryModule`.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-305">To turn off the standard dependency-tracking module, edit [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) and delete the reference to `DependencyCollector.DependencyTrackingTelemetryModule`.</span></span>

### <a name="dependencies-in-analytics"></a><span data-ttu-id="9e4e1-306">Dépendances dans Analytique</span><span class="sxs-lookup"><span data-stu-id="9e4e1-306">Dependencies in Analytics</span></span>

<span data-ttu-id="9e4e1-307">Dans [Application Insights - Analytique](app-insights-analytics.md), les appels de trackDependency s’affichent dans la table `dependencies`.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-307">In [Application Insights Analytics](app-insights-analytics.md), trackDependency calls show up in the `dependencies` table.</span></span>

<span data-ttu-id="9e4e1-308">Si un [échantillonnage](app-insights-sampling.md) est en cours, la propriété itemCount affiche une valeur supérieure à 1.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-308">If [sampling](app-insights-sampling.md) is in operation, the itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="9e4e1-309">Par exemple, itemCount==10 signifie que sur 10 appels à trackDependency(), le processus d’échantillonnage n’en a transmis qu’un seul.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-309">For example itemCount==10 means that of 10 calls to trackDependency(), the sampling process only transmitted one of them.</span></span> <span data-ttu-id="9e4e1-310">Pour obtenir un nombre correct de dépendances segmentées par composant cible, utilisez un code similaire à celui-ci :</span><span class="sxs-lookup"><span data-stu-id="9e4e1-310">To get a correct count of dependencies segmented by target component, use code such as:</span></span>

```
dependencies | summarize sum(itemCount) by target
```

<span data-ttu-id="9e4e1-311">Pour associer des dépendances aux demandes qui s’y rapportent, utilisez une jointure :</span><span class="sxs-lookup"><span data-stu-id="9e4e1-311">To associate dependencies with their related requests, use a join:</span></span>

```
dependencies
| join (requests) on operation_Id 
```

## <a name="flushing-data"></a><span data-ttu-id="9e4e1-312">Vidage des données</span><span class="sxs-lookup"><span data-stu-id="9e4e1-312">Flushing data</span></span>
<span data-ttu-id="9e4e1-313">Normalement, le kit SDK envoie des données à des moments choisis pour minimiser l'impact sur l'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-313">Normally, the SDK sends data at times chosen to minimize the impact on the user.</span></span> <span data-ttu-id="9e4e1-314">Toutefois, dans certains cas vous pouvez vider la mémoire tampon - par exemple, si vous utilisez le kit SDK dans une application qui s'arrête.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-314">However, in some cases, you might want to flush the buffer--for example, if you are using the SDK in an application that shuts down.</span></span>

<span data-ttu-id="9e4e1-315">*C#*</span><span class="sxs-lookup"><span data-stu-id="9e4e1-315">*C#*</span></span>

    telemetry.Flush();

    // Allow some time for flushing before shutdown.
    System.Threading.Thread.Sleep(1000);

<span data-ttu-id="9e4e1-316">Notez que la fonction est asynchrone pour le [canal de télémétrie du serveur](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel/).</span><span class="sxs-lookup"><span data-stu-id="9e4e1-316">Note that the function is asynchronous for the [server telemetry channel](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel/).</span></span>

## <a name="authenticated-users"></a><span data-ttu-id="9e4e1-317">Utilisateurs authentifiés</span><span class="sxs-lookup"><span data-stu-id="9e4e1-317">Authenticated users</span></span>
<span data-ttu-id="9e4e1-318">Dans une application web, les utilisateurs sont identifiés par des cookies par défaut.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-318">In a web app, users are (by default) identified by cookies.</span></span> <span data-ttu-id="9e4e1-319">Un utilisateur peut être compté plusieurs fois s’il accède à votre application à partir d’un autre ordinateur ou navigateur, ou s’il supprime des cookies.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-319">A user might be counted more than once if they access your app from a different machine or browser, or if they delete cookies.</span></span>

<span data-ttu-id="9e4e1-320">Mais si les utilisateurs se connectent à votre application, vous pouvez obtenir un nombre plus précis en définissant l’ID de l’utilisateur authentifié dans le code du navigateur :</span><span class="sxs-lookup"><span data-stu-id="9e4e1-320">If users sign in to your app, you can get a more accurate count by setting the authenticated user ID in the browser code:</span></span>

<span data-ttu-id="9e4e1-321">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="9e4e1-321">*JavaScript*</span></span>

```JS
// Called when my app has identified the user.
function Authenticated(signInId) {
    var validatedId = signInId.replace(/[,;=| ]+/g, "_");
    appInsights.setAuthenticatedUserContext(validatedId);
    ...
}
```

<span data-ttu-id="9e4e1-322">Dans une application MVC Web ASP.NET, par exemple :</span><span class="sxs-lookup"><span data-stu-id="9e4e1-322">In an ASP.NET web MVC application, for example:</span></span>

<span data-ttu-id="9e4e1-323">*Razor*</span><span class="sxs-lookup"><span data-stu-id="9e4e1-323">*Razor*</span></span>

        @if (Request.IsAuthenticated)
        {
            <script>
                appInsights.setAuthenticatedUserContext("@User.Identity.Name
                   .Replace("\\", "\\\\")"
                   .replace(/[,;=| ]+/g, "_"));
            </script>
        }

<span data-ttu-id="9e4e1-324">Il n’est pas nécessaire d’utiliser le nom de connexion réel de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-324">It isn't necessary to use the user's actual sign-in name.</span></span> <span data-ttu-id="9e4e1-325">Il doit uniquement s’agir d’un ID unique pour cet utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-325">It only has to be an ID that is unique to that user.</span></span> <span data-ttu-id="9e4e1-326">Il ne doit pas inclure d'espaces ni l'un des caractères suivants : `,;=|`.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-326">It must not include spaces or any of the characters `,;=|`.</span></span>

<span data-ttu-id="9e4e1-327">L’ID d’utilisateur est également défini dans un cookie de session et envoyé au serveur.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-327">The user ID is also set in a session cookie and sent to the server.</span></span> <span data-ttu-id="9e4e1-328">Si le kit SDK de serveur est installé, l’ID d’utilisateur authentifié est envoyé dans le cadre des propriétés de contexte de télémétrie client et serveur.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-328">If the server SDK is installed, the authenticated user ID is sent as part of the context properties of both client and server telemetry.</span></span> <span data-ttu-id="9e4e1-329">Vous pouvez ensuite filtrer et rechercher dessus.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-329">You can then filter and search on it.</span></span>

<span data-ttu-id="9e4e1-330">Si votre application regroupe les utilisateurs par comptes, vous pouvez également fournir un identificateur pour ce compte (avec les mêmes restrictions de caractères).</span><span class="sxs-lookup"><span data-stu-id="9e4e1-330">If your app groups users into accounts, you can also pass an identifier for the account (with the same character restrictions).</span></span>

      appInsights.setAuthenticatedUserContext(validatedId, accountId);

<span data-ttu-id="9e4e1-331">Dans [Metrics Explorer](app-insights-metrics-explorer.md), vous pouvez créer un graphique qui compte les **Utilisateurs authentifiés** et les **Comptes d’utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-331">In [Metrics Explorer](app-insights-metrics-explorer.md), you can create a chart that counts **Users, Authenticated**, and **User accounts**.</span></span>

<span data-ttu-id="9e4e1-332">Vous pouvez également [rechercher](app-insights-diagnostic-search.md) les points de données client avec des comptes et des noms d'utilisateur spécifiques.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-332">You can also [search](app-insights-diagnostic-search.md) for client data points with specific user names and accounts.</span></span>

## <span data-ttu-id="9e4e1-333"><a name="properties"></a>Filtrage, recherche et segmentation de vos données à l’aide des propriétés</span><span class="sxs-lookup"><span data-stu-id="9e4e1-333"><a name="properties"></a>Filtering, searching, and segmenting your data by using properties</span></span>
<span data-ttu-id="9e4e1-334">Vous pouvez associer des propriétés et des mesures à vos événements (et également à des mesures, des affichages de page, des exceptions et d'autres données de télémétrie).</span><span class="sxs-lookup"><span data-stu-id="9e4e1-334">You can attach properties and measurements to your events (and also to metrics, page views, exceptions, and other telemetry data).</span></span>

<span data-ttu-id="9e4e1-335">*propriétés* sont des valeurs de chaîne que vous pouvez utiliser pour filtrer votre télémétrie dans les rapports d'utilisation.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-335">*Properties* are string values that you can use to filter your telemetry in the usage reports.</span></span> <span data-ttu-id="9e4e1-336">Par exemple, si votre application fournit plusieurs jeux, vous pouvez attacher le nom du jeu à chaque événement pour vous permettre de savoir quels sont les jeux les plus populaires.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-336">For example, if your app provides several games, you can attach the name of the game to each event so that you can see which games are more popular.</span></span>

<span data-ttu-id="9e4e1-337">Il existe une limite de 8192 sur la longueur de chaîne.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-337">There's a limit of 8192 on the string length.</span></span> <span data-ttu-id="9e4e1-338">(Si vous souhaitez envoyer d’importants blocs de données, utilisez le paramètre de message de [TrackTrace](#track-trace).)</span><span class="sxs-lookup"><span data-stu-id="9e4e1-338">(If you want to send large chunks of data, use the message parameter of [TrackTrace](#track-trace).)</span></span>

<span data-ttu-id="9e4e1-339">*mesures* sont des valeurs numériques qui peuvent être représentées sous forme graphique.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-339">*Metrics* are numeric values that can be presented graphically.</span></span> <span data-ttu-id="9e4e1-340">Par exemple, observez s'il existe une augmentation progressive des scores atteints par vos joueurs.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-340">For example, you might want to see if there's a gradual increase in the scores that your gamers achieve.</span></span> <span data-ttu-id="9e4e1-341">Les graphes peuvent être segmentés par les propriétés envoyées avec l'événement pour vous permettre d’obtenir des graphes distincts ou empilés pour différents jeux.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-341">The graphs can be segmented by the properties that are sent with the event, so that you can get separate or stacked graphs for different games.</span></span>

<span data-ttu-id="9e4e1-342">Pour que les valeurs de mesure s’affichent correctement, elles doivent être supérieures ou égales à 0.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-342">For metric values to be correctly displayed, they should be greater than or equal to 0.</span></span>

<span data-ttu-id="9e4e1-343">Il existe certaines [limites au nombre de propriétés, de valeurs de propriété et de mesures](#limits) que vous pouvez utiliser.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-343">There are some [limits on the number of properties, property values, and metrics](#limits) that you can use.</span></span>

<span data-ttu-id="9e4e1-344">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="9e4e1-344">*JavaScript*</span></span>

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


<span data-ttu-id="9e4e1-345">*C#*</span><span class="sxs-lookup"><span data-stu-id="9e4e1-345">*C#*</span></span>

    // Set up some properties and metrics:
    var properties = new Dictionary <string, string>
       {{"game", currentGame.Name}, {"difficulty", currentGame.Difficulty}};
    var metrics = new Dictionary <string, double>
       {{"Score", currentGame.Score}, {"Opponents", currentGame.OpponentCount}};

    // Send the event:
    telemetry.TrackEvent("WinGame", properties, metrics);


<span data-ttu-id="9e4e1-346">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="9e4e1-346">*Visual Basic*</span></span>

    ' Set up some properties:
    Dim properties = New Dictionary (Of String, String)
    properties.Add("game", currentGame.Name)
    properties.Add("difficulty", currentGame.Difficulty)

    Dim metrics = New Dictionary (Of String, Double)
    metrics.Add("Score", currentGame.Score)
    metrics.Add("Opponents", currentGame.OpponentCount)

    ' Send the event:
    telemetry.TrackEvent("WinGame", properties, metrics)


<span data-ttu-id="9e4e1-347">*Java*</span><span class="sxs-lookup"><span data-stu-id="9e4e1-347">*Java*</span></span>

    Map<String, String> properties = new HashMap<String, String>();
    properties.put("game", currentGame.getName());
    properties.put("difficulty", currentGame.getDifficulty());

    Map<String, Double> metrics = new HashMap<String, Double>();
    metrics.put("Score", currentGame.getScore());
    metrics.put("Opponents", currentGame.getOpponentCount());

    telemetry.trackEvent("WinGame", properties, metrics);


> [!NOTE]
> <span data-ttu-id="9e4e1-348">Veillez à ne pas journaliser des informations personnelles dans les propriétés.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-348">Take care not to log personally identifiable information in properties.</span></span>
>
>

<span data-ttu-id="9e4e1-349">*Si vous avez utilisé des mesures*, ouvrez Metrics Explorer et sélectionnez la mesure à partir du groupe **personnalisé** :</span><span class="sxs-lookup"><span data-stu-id="9e4e1-349">*If you used metrics*, open Metrics Explorer and select the metric from the **Custom** group:</span></span>

![Ouvrez Metrics Explorer, sélectionnez le graphique puis sélectionnez la mesure](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

> [!NOTE]
> <span data-ttu-id="9e4e1-351">Si votre mesure n'apparaît pas, ou si l'en-tête **personnalisé** n'y figure pas, fermez le panneau de sélection et réessayez ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-351">If your metric doesn't appear, or if the **Custom** heading isn't there, close the selection blade and try again later.</span></span> <span data-ttu-id="9e4e1-352">L’agrégation des mesures via le pipeline peut parfois prendre une heure.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-352">Metrics can sometimes take an hour to be aggregated through the pipeline.</span></span>

<span data-ttu-id="9e4e1-353">*Si vous avez utilisé des propriétés et des mesures*, segmentez la mesure par la propriété :</span><span class="sxs-lookup"><span data-stu-id="9e4e1-353">*If you used properties and metrics*, segment the metric by the property:</span></span>

![Définissez le groupe, puis sélectionnez la propriété sous Grouper par](./media/app-insights-api-custom-events-metrics/04-segment-metric-event.png)

<span data-ttu-id="9e4e1-355">Dans *Recherche de diagnostic*, vous pouvez afficher les propriétés et les mesures des occurrences individuelles d’un événement.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-355">*In Diagnostic Search*, you can view the properties and metrics of individual occurrences of an event.</span></span>

![Sélectionnez une instance, puis sélectionnez « ... »](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-4.png)

<span data-ttu-id="9e4e1-357">Utilisez le champ **Rechercher** pour voir les occurrences de l'événement présentant une valeur de propriété particulière.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-357">Use the **Search** field to see event occurrences that have a particular property value.</span></span>

![Tapez un terme dans Rechercher](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-5.png)

<span data-ttu-id="9e4e1-359">[En savoir plus sur les expressions de recherche](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="9e4e1-359">[Learn more about search expressions](app-insights-diagnostic-search.md).</span></span>

### <a name="alternative-way-to-set-properties-and-metrics"></a><span data-ttu-id="9e4e1-360">Autre façon de définir des propriétés et des mesures</span><span class="sxs-lookup"><span data-stu-id="9e4e1-360">Alternative way to set properties and metrics</span></span>
<span data-ttu-id="9e4e1-361">Si cela est plus pratique, vous pouvez collecter les paramètres d'un événement dans un objet séparé :</span><span class="sxs-lookup"><span data-stu-id="9e4e1-361">If it's more convenient, you can collect the parameters of an event in a separate object:</span></span>

    var event = new EventTelemetry();

    event.Name = "WinGame";
    event.Metrics["processingTime"] = stopwatch.Elapsed.TotalMilliseconds;
    event.Properties["game"] = currentGame.Name;
    event.Properties["difficulty"] = currentGame.Difficulty;
    event.Metrics["Score"] = currentGame.Score;
    event.Metrics["Opponents"] = currentGame.Opponents.Length;

    telemetry.TrackEvent(event);

> [!WARNING]
> <span data-ttu-id="9e4e1-362">Ne réutilisez pas la même instance d’élément de télémétrie (`event` dans cet exemple) pour appeler Track*() plusieurs fois.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-362">Don't reuse the same telemetry item instance (`event` in this example) to call Track*() multiple times.</span></span> <span data-ttu-id="9e4e1-363">Cela peut provoquer un envoi de données de télémétrie configurées de façon incorrecte.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-363">This may cause telemetry to be sent with incorrect configuration.</span></span>
>
>

### <a name="custom-measurements-and-properties-in-analytics"></a><span data-ttu-id="9e4e1-364">Mesures et propriétés personnalisées dans Analytique</span><span class="sxs-lookup"><span data-stu-id="9e4e1-364">Custom measurements and properties in Analytics</span></span>

<span data-ttu-id="9e4e1-365">Dans [Analytique](app-insights-analytics.md), les mesures et les propriétés personnalisées s’affichent dans les attributs `customMeasurements` et `customDimensions` de chaque enregistrement de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-365">In [Analytics](app-insights-analytics.md), custom metrics and properties show in the `customMeasurements` and `customDimensions` attributes of each telemetry record.</span></span>

<span data-ttu-id="9e4e1-366">Par exemple, si vous avez ajouté une propriété nommée « game » à votre télémétrie des demandes, cette requête compte les occurrences des différentes valeurs de « game » et affiche la moyenne de la métrique personnalisée « score » :</span><span class="sxs-lookup"><span data-stu-id="9e4e1-366">For example, if you have added a property named "game" to your request telemetry, this query counts the occurrences of different values of "game", and show the average of the custom metric "score":</span></span>

```
requests
| summarize sum(itemCount), avg(todouble(customMeasurements.score)) by tostring(customDimensions.game) 
```

<span data-ttu-id="9e4e1-367">Notez que :</span><span class="sxs-lookup"><span data-stu-id="9e4e1-367">Notice that:</span></span>

* <span data-ttu-id="9e4e1-368">Quand vous extrayez une valeur du JSON la customDimensions ou customMeasurements, elle est de type dynamique et par conséquent, vous devez la transtyper en `tostring` ou `todouble`.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-368">When you extract a value from the customDimensions or customMeasurements JSON, it has dynamic type, and so you must cast it `tostring` or `todouble`.</span></span>
* <span data-ttu-id="9e4e1-369">Pour tenir compte de la possibilité [d’échantillonnage](app-insights-sampling.md), vous devez utiliser `sum(itemCount)`, et non pas `count()`.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-369">To take account of the possibility of [sampling](app-insights-sampling.md), you should use `sum(itemCount)`, not `count()`.</span></span>



## <span data-ttu-id="9e4e1-370"><a name="timed"></a> Événements de durée</span><span class="sxs-lookup"><span data-stu-id="9e4e1-370"><a name="timed"></a> Timing events</span></span>
<span data-ttu-id="9e4e1-371">Vous avez parfois besoin d’obtenir une représentation graphique de la durée nécessaire à la réalisation d’une action.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-371">Sometimes you want to chart how long it takes to perform an action.</span></span> <span data-ttu-id="9e4e1-372">Par exemple, vous souhaitez savoir de combien de temps les utilisateurs ont besoin pour évaluer leurs choix dans un jeu.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-372">For example, you might want to know how long users take to consider choices in a game.</span></span> <span data-ttu-id="9e4e1-373">Vous pouvez utiliser le paramètre de mesure pour cela.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-373">You can use the measurement parameter for this.</span></span>

<span data-ttu-id="9e4e1-374">*C#*</span><span class="sxs-lookup"><span data-stu-id="9e4e1-374">*C#*</span></span>

    var stopwatch = System.Diagnostics.Stopwatch.StartNew();

    // ... perform the timed action ...

    stopwatch.Stop();

    var metrics = new Dictionary <string, double>
       {{"processingTime", stopwatch.Elapsed.TotalMilliseconds}};

    // Set up some properties:
    var properties = new Dictionary <string, string>
       {{"signalSource", currentSignalSource.Name}};

    // Send the event:
    telemetry.TrackEvent("SignalProcessed", properties, metrics);



## <span data-ttu-id="9e4e1-375"><a name="defaults"></a>Propriétés par défaut pour la télémétrie personnalisée</span><span class="sxs-lookup"><span data-stu-id="9e4e1-375"><a name="defaults"></a>Default properties for custom telemetry</span></span>
<span data-ttu-id="9e4e1-376">Si vous souhaitez définir des valeurs de propriété par défaut pour certains des événements personnalisés que vous écrivez, vous pouvez les définir dans une instance de TelemetryClient.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-376">If you want to set default property values for some of the custom events that you write, you can set them in a TelemetryClient instance.</span></span> <span data-ttu-id="9e4e1-377">Ils sont associés à chaque élément de télémétrie envoyée à partir de ce client.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-377">They are attached to every telemetry item that's sent from that client.</span></span>

<span data-ttu-id="9e4e1-378">*C#*</span><span class="sxs-lookup"><span data-stu-id="9e4e1-378">*C#*</span></span>

    using Microsoft.ApplicationInsights.DataContracts;

    var gameTelemetry = new TelemetryClient();
    gameTelemetry.Context.Properties["Game"] = currentGame.Name;
    // Now all telemetry will automatically be sent with the context property:
    gameTelemetry.TrackEvent("WinGame");

<span data-ttu-id="9e4e1-379">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="9e4e1-379">*Visual Basic*</span></span>

    Dim gameTelemetry = New TelemetryClient()
    gameTelemetry.Context.Properties("Game") = currentGame.Name
    ' Now all telemetry will automatically be sent with the context property:
    gameTelemetry.TrackEvent("WinGame")

<span data-ttu-id="9e4e1-380">*Java*</span><span class="sxs-lookup"><span data-stu-id="9e4e1-380">*Java*</span></span>

    import com.microsoft.applicationinsights.TelemetryClient;
    import com.microsoft.applicationinsights.TelemetryContext;
    ...


    TelemetryClient gameTelemetry = new TelemetryClient();
    TelemetryContext context = gameTelemetry.getContext();
    context.getProperties().put("Game", currentGame.Name);

    gameTelemetry.TrackEvent("WinGame");



<span data-ttu-id="9e4e1-381">Les appels de télémétrie individuels peuvent remplacer les valeurs par défaut dans leurs dictionnaires de propriété.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-381">Individual telemetry calls can override the default values in their property dictionaries.</span></span>

<span data-ttu-id="9e4e1-382">*Pour les clients Web JavaScript*, [utilisez des initialiseurs de télémétrie JavaScript](#js-initializer).</span><span class="sxs-lookup"><span data-stu-id="9e4e1-382">*For JavaScript web clients*, [use JavaScript telemetry initializers](#js-initializer).</span></span>

<span data-ttu-id="9e4e1-383">*Pour ajouter des propriétés à toutes les données de télémétrie*, notamment les données des modules de collecte standard, [implémentez `ITelemetryInitializer`](app-insights-api-filtering-sampling.md#add-properties).</span><span class="sxs-lookup"><span data-stu-id="9e4e1-383">*To add properties to all telemetry*, including the data from standard collection modules, [implement `ITelemetryInitializer`](app-insights-api-filtering-sampling.md#add-properties).</span></span>

## <a name="sampling-filtering-and-processing-telemetry"></a><span data-ttu-id="9e4e1-384">Échantillonnage, filtrage et traitement de la télémétrie</span><span class="sxs-lookup"><span data-stu-id="9e4e1-384">Sampling, filtering, and processing telemetry</span></span>
<span data-ttu-id="9e4e1-385">Vous pouvez écrire du code pour traiter votre télémétrie avant de l’envoyer à partir du Kit de développement logiciel (SDK).</span><span class="sxs-lookup"><span data-stu-id="9e4e1-385">You can write code to process your telemetry before it's sent from the SDK.</span></span> <span data-ttu-id="9e4e1-386">Le traitement inclut les données envoyées par les modules de télémétrie standard, telles que la collection de requêtes HTTP et la collection de dépendances.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-386">The processing includes data that's sent from the standard telemetry modules, such as HTTP request collection and dependency collection.</span></span>

<span data-ttu-id="9e4e1-387">[Ajoutez des propriétés](app-insights-api-filtering-sampling.md#add-properties) à la télémétrie en implémentant `ITelemetryInitializer`.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-387">[Add properties](app-insights-api-filtering-sampling.md#add-properties) to telemetry by implementing `ITelemetryInitializer`.</span></span> <span data-ttu-id="9e4e1-388">Par exemple, vous pouvez ajouter des numéros de version ou des valeurs calculées à partir d'autres propriétés.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-388">For example, you can add version numbers or values that are calculated from other properties.</span></span>

<span data-ttu-id="9e4e1-389">[Le filtrage](app-insights-api-filtering-sampling.md#filtering) peut modifier ou abandonner des données de télémétrie avant leur envoi depuis le SDK en implémentant `ITelemetryProcesor`.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-389">[Filtering](app-insights-api-filtering-sampling.md#filtering) can modify or discard telemetry before it's sent from the SDK by implementing `ITelemetryProcesor`.</span></span> <span data-ttu-id="9e4e1-390">Vous contrôlez ce qui est envoyé ou rejeté, mais vous devez prendre en compte l’impact sur vos mesures.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-390">You control what is sent or discarded, but you have to account for the effect on your metrics.</span></span> <span data-ttu-id="9e4e1-391">Suivant la façon dont vous ignorez les éléments, vous risquez de ne plus pouvoir naviguer entre des éléments connexes.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-391">Depending on how you discard items, you might lose the ability to navigate between related items.</span></span>

<span data-ttu-id="9e4e1-392">[L’échantillonnage](app-insights-api-filtering-sampling.md) est une solution intégrée pour réduire le volume des données envoyées à partir de votre application vers le portail.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-392">[Sampling](app-insights-api-filtering-sampling.md) is a packaged solution to reduce the volume of data that's sent from your app to the portal.</span></span> <span data-ttu-id="9e4e1-393">Cela n’affecte pas les mesures affichées.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-393">It does so without affecting the displayed metrics.</span></span> <span data-ttu-id="9e4e1-394">Et il n’affecte pas votre capacité à diagnostiquer les problèmes en navigant entre des éléments connexes, tels que les exceptions, les requêtes et les affichages de page.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-394">And it does so without affecting your ability to diagnose problems by navigating between related items such as exceptions, requests, and page views.</span></span>

<span data-ttu-id="9e4e1-395">[Plus d’informations](app-insights-api-filtering-sampling.md)</span><span class="sxs-lookup"><span data-stu-id="9e4e1-395">[Learn more](app-insights-api-filtering-sampling.md).</span></span>

## <a name="disabling-telemetry"></a><span data-ttu-id="9e4e1-396">Désactivation de la télémétrie</span><span class="sxs-lookup"><span data-stu-id="9e4e1-396">Disabling telemetry</span></span>
<span data-ttu-id="9e4e1-397">Pour *arrêter et démarrer dynamiquement* la collecte et la transmission de la télémétrie :</span><span class="sxs-lookup"><span data-stu-id="9e4e1-397">To *dynamically stop and start* the collection and transmission of telemetry:</span></span>

<span data-ttu-id="9e4e1-398">*C#*</span><span class="sxs-lookup"><span data-stu-id="9e4e1-398">*C#*</span></span>

```C#

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```

<span data-ttu-id="9e4e1-399">Pour *désactiver les collecteurs standard sélectionnés* (par exemple, les compteurs de performances, les requêtes HTTP ou les dépendances), supprimez ou commentez les lignes correspondantes dans [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). Par exemple, vous pouvez faire cela si vous souhaitez envoyer vos propres données TrackRequest.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-399">To *disable selected standard collectors*--for example, performance counters, HTTP requests, or dependencies--delete or comment out the relevant lines in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). You can do this, for example, if you want to send your own TrackRequest data.</span></span>

## <span data-ttu-id="9e4e1-400"><a name="debug"></a>Mode Développeur :</span><span class="sxs-lookup"><span data-stu-id="9e4e1-400"><a name="debug"></a>Developer mode</span></span>
<span data-ttu-id="9e4e1-401">Pendant le débogage, il est utile d'avoir votre télémétrie envoyée par le pipeline afin que vous puissiez voir immédiatement les résultats.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-401">During debugging, it's useful to have your telemetry expedited through the pipeline so that you can see results immediately.</span></span> <span data-ttu-id="9e4e1-402">Vous obtenez également des messages supplémentaires qui vous permettent de suivre tout problème relatif à la télémétrie.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-402">You also get additional messages that help you trace any problems with the telemetry.</span></span> <span data-ttu-id="9e4e1-403">Désactivez-les lors de la production, car ils peuvent ralentir votre application.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-403">Switch it off in production, because it may slow down your app.</span></span>

<span data-ttu-id="9e4e1-404">*C#*</span><span class="sxs-lookup"><span data-stu-id="9e4e1-404">*C#*</span></span>

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = true;

<span data-ttu-id="9e4e1-405">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="9e4e1-405">*Visual Basic*</span></span>

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = True


## <span data-ttu-id="9e4e1-406"><a name="ikey"></a> Définition de la touche d’instrumentation pour la télémétrie personnalisée sélectionnée</span><span class="sxs-lookup"><span data-stu-id="9e4e1-406"><a name="ikey"></a> Setting the instrumentation key for selected custom telemetry</span></span>
<span data-ttu-id="9e4e1-407">*C#*</span><span class="sxs-lookup"><span data-stu-id="9e4e1-407">*C#*</span></span>

    var telemetry = new TelemetryClient();
    telemetry.InstrumentationKey = "---my key---";
    // ...


## <span data-ttu-id="9e4e1-408"><a name="dynamic-ikey"></a> Clé d'instrumentation dynamique</span><span class="sxs-lookup"><span data-stu-id="9e4e1-408"><a name="dynamic-ikey"></a> Dynamic instrumentation key</span></span>
<span data-ttu-id="9e4e1-409">Pour éviter de mélanger la télémétrie fournie par les environnements de développement, de test et de production, vous pouvez [créer des ressources Application Insights distinctes](app-insights-create-new-resource.md) et modifier leurs clés en fonction de l’environnement.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-409">To avoid mixing up telemetry from development, test, and production environments, you can [create separate Application Insights resources](app-insights-create-new-resource.md) and change their keys, depending on the environment.</span></span>

<span data-ttu-id="9e4e1-410">Au lieu de récupérer la clé d'instrumentation à partir du fichier de configuration, vous pouvez la définir dans votre code.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-410">Instead of getting the instrumentation key from the configuration file, you can set it in your code.</span></span> <span data-ttu-id="9e4e1-411">Définissez la clé dans une méthode d'initialisation, par exemple global.aspx.cs dans un service ASP.NET :</span><span class="sxs-lookup"><span data-stu-id="9e4e1-411">Set the key in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

<span data-ttu-id="9e4e1-412">*C#*</span><span class="sxs-lookup"><span data-stu-id="9e4e1-412">*C#*</span></span>

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      ...

<span data-ttu-id="9e4e1-413">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="9e4e1-413">*JavaScript*</span></span>

    appInsights.config.instrumentationKey = myKey;



<span data-ttu-id="9e4e1-414">Dans les pages web, vous pouvez la définir depuis l'état du serveur web au lieu de la coder littéralement dans le script.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-414">In webpages, you might want to set it from the web server's state, rather than coding it literally into the script.</span></span> <span data-ttu-id="9e4e1-415">Par exemple, dans une page web générée dans une application ASP.NET :</span><span class="sxs-lookup"><span data-stu-id="9e4e1-415">For example, in a webpage generated in an ASP.NET app:</span></span>

<span data-ttu-id="9e4e1-416">*JavaScript dans Razor*</span><span class="sxs-lookup"><span data-stu-id="9e4e1-416">*JavaScript in Razor*</span></span>

    <script type="text/javascript">
    // Standard Application Insights webpage script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      @Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="telemetrycontext"></a><span data-ttu-id="9e4e1-417">TelemetryContext</span><span class="sxs-lookup"><span data-stu-id="9e4e1-417">TelemetryContext</span></span>
<span data-ttu-id="9e4e1-418">TelemetryClient a une propriété de contexte contenant les valeurs qui sont envoyées avec toutes les données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-418">TelemetryClient has a Context property, which contains values that are sent along with all telemetry data.</span></span> <span data-ttu-id="9e4e1-419">Elles sont normalement définies par les modules de télémétrie standard, mais vous pouvez également les définir vous-même.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-419">They are normally set by the standard telemetry modules, but you can also set them yourself.</span></span> <span data-ttu-id="9e4e1-420">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="9e4e1-420">For example:</span></span>

    telemetry.Context.Operation.Name = "MyOperationName";

<span data-ttu-id="9e4e1-421">Si vous définissez une de ces valeurs vous-même, supprimez la ligne appropriée dans [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), pour ne pas mélanger vos valeurs et les valeurs standard.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-421">If you set any of these values yourself, consider removing the relevant line from [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), so that your values and the standard values don't get confused.</span></span>

* <span data-ttu-id="9e4e1-422">**Composant** : l'application et sa version.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-422">**Component**: The app and its version.</span></span>
* <span data-ttu-id="9e4e1-423">**Appareil** : données concernant l’appareil sur lequel l’application s’exécute.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-423">**Device**: Data about the device where the app is running.</span></span> <span data-ttu-id="9e4e1-424">(dans les applications web, il s’agit du serveur ou de l’appareil client depuis lequel la télémétrie est envoyée.)</span><span class="sxs-lookup"><span data-stu-id="9e4e1-424">(In web apps, this is the server or client device that the telemetry is sent from.)</span></span>
* <span data-ttu-id="9e4e1-425">**InstrumentationKey** : la ressource Application Insights dans Azure dans laquelle la télémétrie s’affiche.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-425">**InstrumentationKey**: The Application Insights resource in Azure where the telemetry appear.</span></span> <span data-ttu-id="9e4e1-426">Elle est généralement récupérée dans ApplicationInsights.config.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-426">It's usually picked up from ApplicationInsights.config.</span></span>
* <span data-ttu-id="9e4e1-427">**Emplacement** : emplacement géographique de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-427">**Location**: The geographic location of the device.</span></span>
* <span data-ttu-id="9e4e1-428">**Opération** : dans les applications web, il s’agit de la requête HTTP actuelle.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-428">**Operation**: In web apps, the current HTTP request.</span></span> <span data-ttu-id="9e4e1-429">Dans d'autres types d'application, vous pouvez définir celle-ci sur les événements regroupés.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-429">In other app types, you can set this to group events together.</span></span>
  * <span data-ttu-id="9e4e1-430">**ID**: une valeur générée qui met en relation différents événements de manière à ce que vous trouviez les « Éléments associés » lorsque vous inspectez un événement dans la Recherche de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-430">**Id**: A generated value that correlates different events, so that when you inspect any event in Diagnostic Search, you can find related items.</span></span>
  * <span data-ttu-id="9e4e1-431">**Nom**: un identificateur, généralement l'URL de la requête HTTP.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-431">**Name**: An identifier, usually the URL of the HTTP request.</span></span>
  * <span data-ttu-id="9e4e1-432">**SyntheticSource**: si elle est non nulle ou vide, cette chaîne indique que la source de la requête a été identifiée en tant que robot ou test web.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-432">**SyntheticSource**: If not null or empty, a string that indicates that the source of the request has been identified as a robot or web test.</span></span> <span data-ttu-id="9e4e1-433">Par défaut, elle est exclue des calculs dans Metrics Explorer.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-433">By default, it is excluded from calculations in Metrics Explorer.</span></span>
* <span data-ttu-id="9e4e1-434">**Propriétés** : ce sont les propriétés qui sont envoyées avec toutes les données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-434">**Properties**: Properties that are sent with all telemetry data.</span></span> <span data-ttu-id="9e4e1-435">Elles peuvent être remplacées dans les appels Track* individuels.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-435">It can be overridden in individual Track* calls.</span></span>
* <span data-ttu-id="9e4e1-436">**Session** : la session utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-436">**Session**: The user's session.</span></span> <span data-ttu-id="9e4e1-437">L'ID est définie sur une valeur générée qui est modifiée lorsque l'utilisateur n'a pas été actif pendant un certain temps.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-437">The ID is set to a generated value, which is changed when the user has not been active for a while.</span></span>
* <span data-ttu-id="9e4e1-438">**Utilisateur** : Informations utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-438">**User**: User information.</span></span>

## <a name="limits"></a><span data-ttu-id="9e4e1-439">limites</span><span class="sxs-lookup"><span data-stu-id="9e4e1-439">Limits</span></span>
[!INCLUDE [application-insights-limits](../../includes/application-insights-limits.md)]

<span data-ttu-id="9e4e1-440">Pour éviter d'atteindre la limite de débit de données, utilisez [l’échantillonnage](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="9e4e1-440">To avoid hitting the data rate limit, use [sampling](app-insights-sampling.md).</span></span>

<span data-ttu-id="9e4e1-441">Pour déterminer la durée de conservation des données, consultez [Rétention des données et confidentialité](app-insights-data-retention-privacy.md).</span><span class="sxs-lookup"><span data-stu-id="9e4e1-441">To determine how long data is kept, see [Data retention and privacy](app-insights-data-retention-privacy.md).</span></span>

## <a name="reference-docs"></a><span data-ttu-id="9e4e1-442">Documents de référence</span><span class="sxs-lookup"><span data-stu-id="9e4e1-442">Reference docs</span></span>
* [<span data-ttu-id="9e4e1-443">Référence ASP.NET</span><span class="sxs-lookup"><span data-stu-id="9e4e1-443">ASP.NET reference</span></span>](https://msdn.microsoft.com/library/dn817570.aspx)
* [<span data-ttu-id="9e4e1-444">Référence Java</span><span class="sxs-lookup"><span data-stu-id="9e4e1-444">Java reference</span></span>](http://dl.windowsazure.com/applicationinsights/javadoc/)
* [<span data-ttu-id="9e4e1-445">Référence JavaScript</span><span class="sxs-lookup"><span data-stu-id="9e4e1-445">JavaScript reference</span></span>](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md)
* [<span data-ttu-id="9e4e1-446">Kit de développement logiciel Android</span><span class="sxs-lookup"><span data-stu-id="9e4e1-446">Android SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-Android)
* [<span data-ttu-id="9e4e1-447">Kit de développement logiciel (SDK) iOS</span><span class="sxs-lookup"><span data-stu-id="9e4e1-447">iOS SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-iOS)

## <a name="sdk-code"></a><span data-ttu-id="9e4e1-448">Code de Kit de développement logiciel (SDK)</span><span class="sxs-lookup"><span data-stu-id="9e4e1-448">SDK code</span></span>
* [<span data-ttu-id="9e4e1-449">Kit de développement logiciel (SDK) principal ASP.NET</span><span class="sxs-lookup"><span data-stu-id="9e4e1-449">ASP.NET Core SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [<span data-ttu-id="9e4e1-450">ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="9e4e1-450">ASP.NET 5</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [<span data-ttu-id="9e4e1-451">Packages Windows Server</span><span class="sxs-lookup"><span data-stu-id="9e4e1-451">Windows Server packages</span></span>](https://github.com/Microsoft/applicationInsights-dotnet-server)
* [<span data-ttu-id="9e4e1-452">Kit SDK Java</span><span class="sxs-lookup"><span data-stu-id="9e4e1-452">Java SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-Java)
* [<span data-ttu-id="9e4e1-453">Kit de développement logiciel (SDK) JavaScript</span><span class="sxs-lookup"><span data-stu-id="9e4e1-453">JavaScript SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-JS)
* [<span data-ttu-id="9e4e1-454">Toutes les plateformes</span><span class="sxs-lookup"><span data-stu-id="9e4e1-454">All platforms</span></span>](https://github.com/Microsoft?utf8=%E2%9C%93&query=applicationInsights)

## <a name="questions"></a><span data-ttu-id="9e4e1-455">Questions</span><span class="sxs-lookup"><span data-stu-id="9e4e1-455">Questions</span></span>
* <span data-ttu-id="9e4e1-456">*Quelles exceptions peuvent être lancées par les appels Track_() ?*</span><span class="sxs-lookup"><span data-stu-id="9e4e1-456">*What exceptions might Track_() calls throw?*</span></span>

    <span data-ttu-id="9e4e1-457">Aucune.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-457">None.</span></span> <span data-ttu-id="9e4e1-458">Vous n’avez pas besoin de les inclure dans des clauses try-catch.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-458">You don't need to wrap them in try-catch clauses.</span></span> <span data-ttu-id="9e4e1-459">Si le Kit de développement logiciel (SDK) rencontre des problèmes, il enregistrera des messages dans la sortie de la console de débogage et, si les messages aboutissent, dans la recherche de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="9e4e1-459">If the SDK encounters problems, it will log messages in the debug console output and--if the messages get through--in Diagnostic Search.</span></span>
* <span data-ttu-id="9e4e1-460">*Existe-t-il une API REST pour obtenir des données à partir du portail ?*</span><span class="sxs-lookup"><span data-stu-id="9e4e1-460">*Is there a REST API to get data from the portal?*</span></span>

    <span data-ttu-id="9e4e1-461">Oui, [l’API d’accès aux données](https://dev.applicationinsights.io/).</span><span class="sxs-lookup"><span data-stu-id="9e4e1-461">Yes, the [data access API](https://dev.applicationinsights.io/).</span></span> <span data-ttu-id="9e4e1-462">Les autres méthodes d’extraction des données sont [l’exportation d’Analytics vers Power BI](app-insights-export-power-bi.md) et [l’exportation continue](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="9e4e1-462">Other ways to extract data include [export from Analytics to Power BI](app-insights-export-power-bi.md) and [continuous export](app-insights-export-telemetry.md).</span></span>

## <span data-ttu-id="9e4e1-463"><a name="next"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9e4e1-463"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="9e4e1-464">Recherche d’événements et de journaux</span><span class="sxs-lookup"><span data-stu-id="9e4e1-464">Search events and logs</span></span>](app-insights-diagnostic-search.md)

* [<span data-ttu-id="9e4e1-465">Dépannage</span><span class="sxs-lookup"><span data-stu-id="9e4e1-465">Troubleshooting</span></span>](app-insights-troubleshoot-faq.md)


