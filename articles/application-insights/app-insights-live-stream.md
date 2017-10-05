---
title: "Flux de métriques temps réel avec des métriques et des diagnostics personnalisés dans Azure Application Insights | Microsoft Docs"
description: "Surveillez votre application web en temps réel avec des métriques personnalisées, et diagnostiquez les problèmes avec un flux temps réel des échecs, des traces et des événements."
services: application-insights
documentationcenter: 
author: SoubhagyaDash
manager: carmonm
ms.assetid: 1f471176-38f3-40b3-bc6d-3f47d0cbaaa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: bwren
ms.openlocfilehash: 1eb2e0c467d4fb4cb263047caf58d36231578d9a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="live-metrics-stream-monitor--diagnose-with-1-second-latency"></a><span data-ttu-id="aa2bd-103">Flux de métriques temps réel : Surveiller et diagnostiquer avec une latence de 1 seconde</span><span class="sxs-lookup"><span data-stu-id="aa2bd-103">Live Metrics Stream: Monitor & Diagnose with 1-second latency</span></span> 

<span data-ttu-id="aa2bd-104">Sondez le cœur de votre application web dynamique en production en utilisant les flux de métriques temps réel depuis [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="aa2bd-104">Probe the beating heart of your live, in-production web application by using Live Metrics Stream from [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="aa2bd-105">Sélectionnez et filtrez les métriques et les compteurs de performances à surveiller en temps réel, sans aucune perturbation de votre service.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-105">Select and filter metrics and performance counters to watch in real time, without any disturbance to your service.</span></span> <span data-ttu-id="aa2bd-106">Inspectez les traces de pile à partir d’échantillons de demandes en échec et d’exceptions.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-106">Inspect stack traces from sample failed requests and exceptions.</span></span> <span data-ttu-id="aa2bd-107">En combinaison avec le [profileur](app-insights-profiler.md), le [débogueur d’instantané](app-insights-snapshot-debugger.md) et les [tests de performances](app-insights-monitor-web-app-availability.md#performance-tests), les flux de métriques temps réel constituent un outil de diagnostic puissant et non invasif pour votre site web dynamique.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-107">Together with [Profiler](app-insights-profiler.md), [Snapshot debugger](app-insights-snapshot-debugger.md), and [performance testing](app-insights-monitor-web-app-availability.md#performance-tests),  Live Metrics Stream provides a powerful and non-invasive diagnostic tool for your live web site.</span></span>

<span data-ttu-id="aa2bd-108">Avec les flux de métriques temps réel, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="aa2bd-108">With Live Metrics Stream, you can:</span></span>

* <span data-ttu-id="aa2bd-109">Valider un correctif lors de sa publication, en observant les performances et les nombres d’échecs.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-109">Validate a fix while it is released, by watching performance and failure counts.</span></span>
* <span data-ttu-id="aa2bd-110">Observer l’effet des tests de charge et diagnostiquer les problèmes de façon dynamique.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-110">Watch the effect of test loads, and diagnose issues live.</span></span> 
* <span data-ttu-id="aa2bd-111">Vous concentrer sur des sessions de tests particulières ou filtrer les problèmes connus, en sélectionnant et en filtrant les mesures que vous voulez observer.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-111">Focus on particular test sessions or filter out known issues, by selecting and filtering the metrics you want to watch.</span></span>
* <span data-ttu-id="aa2bd-112">Obtenir les traces des exceptions quand elles se produisent.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-112">Get exception traces as they happen.</span></span>
* <span data-ttu-id="aa2bd-113">Faites des essais avec les filtres pour rechercher les indicateurs de performance clés les plus pertinents.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-113">Experiment with filters to find the most relevant KPIs.</span></span>
* <span data-ttu-id="aa2bd-114">Surveiller en temps réel des compteurs de performances Windows.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-114">Monitor any Windows performance counter live.</span></span>
* <span data-ttu-id="aa2bd-115">Identifiez plus facilement un serveur qui rencontre des problèmes et filtrez tous les indicateurs de performance clés/flux en temps réel sur ce serveur uniquement.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-115">Easily identify a server that is having issues, and filter all the KPI/live feed to just that server.</span></span>

<span data-ttu-id="aa2bd-116">[![Vidéo sur les flux de métriques temps réel](./media/app-insights-live-stream/youtube.png)](https://www.youtube.com/watch?v=zqfHf1Oi5PY)</span><span class="sxs-lookup"><span data-stu-id="aa2bd-116">[![Live Metrics Stream video](./media/app-insights-live-stream/youtube.png)](https://www.youtube.com/watch?v=zqfHf1Oi5PY)</span></span>

<span data-ttu-id="aa2bd-117">Les flux de métriques temps réel sont actuellement disponibles sur les applications ASP.NET exécutées localement ou dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-117">Live Metrics Stream is currently available on ASP.NET apps running on-premises or in the Cloud.</span></span> 

## <a name="get-started"></a><span data-ttu-id="aa2bd-118">Prise en main</span><span class="sxs-lookup"><span data-stu-id="aa2bd-118">Get started</span></span>

1. <span data-ttu-id="aa2bd-119">Si vous ne l’avez pas encore fait, [installez Application Insights](app-insights-asp-net.md) dans votre application web ASP.NET ou dans votre [application de serveur Windows](app-insights-windows-services.md).</span><span class="sxs-lookup"><span data-stu-id="aa2bd-119">If you haven't yet [installed Application Insights](app-insights-asp-net.md) in your ASP.NET web app or [Windows server app](app-insights-windows-services.md), do that now.</span></span> 
2. <span data-ttu-id="aa2bd-120">**Mettez à jour vers la dernière version** du package Application Insights.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-120">**Update to the latest version** of the Application Insights package.</span></span> <span data-ttu-id="aa2bd-121">Dans Visual Studio, cliquez avec le bouton droit sur votre projet et choisissez **Gérer les packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-121">In Visual Studio, right-click your project and choose **Manage Nuget packages**.</span></span> <span data-ttu-id="aa2bd-122">Ouvrez l’onglet **Mises à jour**, cochez **Inclure la version préliminaire** et sélectionnez tous les packages Microsoft.ApplicationInsights.*.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-122">Open the **Updates** tab, check **Include prerelease**, and select all the Microsoft.ApplicationInsights.* packages.</span></span>

    <span data-ttu-id="aa2bd-123">Redéployez votre application.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-123">Redeploy your app.</span></span>

3. <span data-ttu-id="aa2bd-124">Dans le [portail Azure](https://portal.azure.com), ouvrez la ressource Application Insights pour votre application puis ouvrez Flux temps réel.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-124">In the [Azure portal](https://portal.azure.com), open the Application Insights resource for your app, and then open Live Stream.</span></span>

4. <span data-ttu-id="aa2bd-125">[Sécurisez le canal de contrôle](#secure-the-control-channel) si vous utilisez des données sensibles comme des noms de clients dans vos filtres.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-125">[Secure the control channel](#secure-the-control-channel) if you might use sensitive data such as customer names in your filters.</span></span>


![Dans le panneau Vue d'ensemble, cliquez sur Live Stream](./media/app-insights-live-stream/live-stream-2.png)

### <a name="no-data-check-your-server-firewall"></a><span data-ttu-id="aa2bd-127">Pas de données ?</span><span class="sxs-lookup"><span data-stu-id="aa2bd-127">No data?</span></span> <span data-ttu-id="aa2bd-128">Vérifier le pare-feu de votre serveur</span><span class="sxs-lookup"><span data-stu-id="aa2bd-128">Check your server firewall</span></span>

<span data-ttu-id="aa2bd-129">Vérifiez que les [ports sortants pour le flux de métriques temps réel](app-insights-ip-addresses.md#outgoing-ports) sont ouverts dans le pare-feu de vos serveurs.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-129">Check the [outgoing ports for Live Metrics Stream](app-insights-ip-addresses.md#outgoing-ports) are open in the firewall of your servers.</span></span> 


## <a name="how-does-live-metrics-stream-differ-from-metrics-explorer-and-analytics"></a><span data-ttu-id="aa2bd-130">En quoi les flux de métriques temps réel diffèrent-ils de Metrics Explorer et d’Analytique ?</span><span class="sxs-lookup"><span data-stu-id="aa2bd-130">How does Live Metrics Stream differ from Metrics Explorer and Analytics?</span></span>

| |<span data-ttu-id="aa2bd-131">Flux temps réel</span><span class="sxs-lookup"><span data-stu-id="aa2bd-131">Live Stream</span></span> | <span data-ttu-id="aa2bd-132">Metrics Explorer et Analytique</span><span class="sxs-lookup"><span data-stu-id="aa2bd-132">Metrics Explorer and Analytics</span></span> |
|---|---|---|
|<span data-ttu-id="aa2bd-133">Latence</span><span class="sxs-lookup"><span data-stu-id="aa2bd-133">Latency</span></span>|<span data-ttu-id="aa2bd-134">Données affichées en une seconde</span><span class="sxs-lookup"><span data-stu-id="aa2bd-134">Data displayed within one second</span></span>|<span data-ttu-id="aa2bd-135">Agrégé sur plusieurs minutes</span><span class="sxs-lookup"><span data-stu-id="aa2bd-135">Aggregated over minutes</span></span>|
|<span data-ttu-id="aa2bd-136">Pas de conservation</span><span class="sxs-lookup"><span data-stu-id="aa2bd-136">No retention</span></span>|<span data-ttu-id="aa2bd-137">Les données persistent tant qu’elles se trouvent sur le graphique puis elles sont abandonnées.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-137">Data persists while it's on the chart, and is then discarded</span></span>|[<span data-ttu-id="aa2bd-138">Données conservées pendant 90 jours</span><span class="sxs-lookup"><span data-stu-id="aa2bd-138">Data retained for 90 days</span></span>](app-insights-data-retention-privacy.md#how-long-is-the-data-kept)|
|<span data-ttu-id="aa2bd-139">À la demande</span><span class="sxs-lookup"><span data-stu-id="aa2bd-139">On demand</span></span>|<span data-ttu-id="aa2bd-140">Les données sont diffusées dès que vous ouvrez les métriques temps réel</span><span class="sxs-lookup"><span data-stu-id="aa2bd-140">Data is streamed while you open Live Metrics</span></span>|<span data-ttu-id="aa2bd-141">Les données sont envoyées quand le SDK est installé et activé</span><span class="sxs-lookup"><span data-stu-id="aa2bd-141">Data is sent whenever the SDK is installed and enabled</span></span>|
|<span data-ttu-id="aa2bd-142">Gratuit</span><span class="sxs-lookup"><span data-stu-id="aa2bd-142">Free</span></span>|<span data-ttu-id="aa2bd-143">Pas de facturation pour les données du flux temps réel</span><span class="sxs-lookup"><span data-stu-id="aa2bd-143">There is no charge for Live Stream data</span></span>|<span data-ttu-id="aa2bd-144">Soumis à [tarification](app-insights-pricing.md)</span><span class="sxs-lookup"><span data-stu-id="aa2bd-144">Subject to [pricing](app-insights-pricing.md)</span></span>
|<span data-ttu-id="aa2bd-145">Échantillonnage</span><span class="sxs-lookup"><span data-stu-id="aa2bd-145">Sampling</span></span>|<span data-ttu-id="aa2bd-146">Tous les compteurs et métriques sélectionnés sont transmis.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-146">All selected metrics and counters are transmitted.</span></span> <span data-ttu-id="aa2bd-147">Les échecs et les traces de pile sont échantillonnés.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-147">Failures and stack traces are sampled.</span></span> <span data-ttu-id="aa2bd-148">Les processeurs de télémétrie ne sont pas appliqués.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-148">TelemetryProcessors are not applied.</span></span>|<span data-ttu-id="aa2bd-149">Les événements peuvent être [échantillonnés](app-insights-api-filtering-sampling.md)</span><span class="sxs-lookup"><span data-stu-id="aa2bd-149">Events may be [sampled](app-insights-api-filtering-sampling.md)</span></span>|
|<span data-ttu-id="aa2bd-150">Canal de contrôle</span><span class="sxs-lookup"><span data-stu-id="aa2bd-150">Control channel</span></span>|<span data-ttu-id="aa2bd-151">Les signaux de contrôle de filtre sont envoyés au SDK.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-151">Filter control signals are sent to the SDK.</span></span> <span data-ttu-id="aa2bd-152">Nous vous recommandons de [sécuriser ce canal](#secure-channel).</span><span class="sxs-lookup"><span data-stu-id="aa2bd-152">We recommend you [secure this channel](#secure-channel).</span></span>|<span data-ttu-id="aa2bd-153">La communication est unidirectionnelle vers le portail</span><span class="sxs-lookup"><span data-stu-id="aa2bd-153">Communication is one-way, to the portal</span></span>|


## <a name="select-and-filter-your-metrics"></a><span data-ttu-id="aa2bd-154">Sélectionner et filtrer vos métriques</span><span class="sxs-lookup"><span data-stu-id="aa2bd-154">Select and filter your metrics</span></span>

<span data-ttu-id="aa2bd-155">(Disponible sur les applications ASP.NET classiques avec la dernière version du SDK.)</span><span class="sxs-lookup"><span data-stu-id="aa2bd-155">(Available on classic ASP.NET apps with the latest SDK.)</span></span>

<span data-ttu-id="aa2bd-156">Vous pouvez surveiller un KPI personnalisé en temps réel en appliquant des filtres arbitraires sur les données de télémétrie Application Insights à partir du portail.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-156">You can monitor custom KPI live by applying arbitrary filters on any Application Insights telemetry from the portal.</span></span> <span data-ttu-id="aa2bd-157">Cliquez sur la commande de filtre qui s’affiche lorsque vous passez la souris sur un graphique.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-157">Click the filter control that shows when you mouse-over any of the charts.</span></span> <span data-ttu-id="aa2bd-158">Le graphique suivant indique un KPI de nombre de demandes personnalisé avec des filtres sur les attributs d’URL et de durée.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-158">The following chart is plotting a custom Request count KPI with filters on URL and Duration attributes.</span></span> <span data-ttu-id="aa2bd-159">Vérifiez vos filtres grâce à la section Vue d’ensemble du flux qui affiche un flux en temps réel de télémétrie correspondant aux critères que vous avez spécifiés.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-159">Validate your filters with the Stream Preview section that shows a live feed of telemetry that matches the criteria you have specified at any point in time.</span></span> 

![Indicateur de performance clé (KPI) de demande personnalisé](./media/app-insights-live-stream/live-stream-filteredMetric.png)

<span data-ttu-id="aa2bd-161">Vous pouvez surveiller une valeur autre qu’un nombre.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-161">You can monitor a value different from Count.</span></span> <span data-ttu-id="aa2bd-162">Les options varient selon le type de flux, qui peut être n’importe quelle télémétrie Application Insights : demandes, dépendances, exceptions, suivis, événements ou métriques.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-162">The options depend on the type of stream, which could be any Application Insights telemetry: requests, dependencies, exceptions, traces, events, or metrics.</span></span> <span data-ttu-id="aa2bd-163">Il peut s’agir d’une [mesure personnalisée](app-insights-api-custom-events-metrics.md#properties) :</span><span class="sxs-lookup"><span data-stu-id="aa2bd-163">It can be your own [custom measurement](app-insights-api-custom-events-metrics.md#properties):</span></span>

![Options de valeur](./media/app-insights-live-stream/live-stream-valueoptions.png)

<span data-ttu-id="aa2bd-165">En plus des données de télémétrie Application Insights, vous pouvez également surveiller n’importe quel compteur de performances Windows en le sélectionnant dans les options de flux et en fournissant le nom du compteur de performances.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-165">In addition to Application Insights telemetry, you can also monitor any Windows performance counter by selecting that from the stream options, and providing the name of the performance counter.</span></span>

<span data-ttu-id="aa2bd-166">Les métriques temps réel sont agrégées à deux endroits : localement sur chaque serveur, puis sur tous les serveurs.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-166">Live metrics are aggregated at two points: locally on each server, and then across all servers.</span></span> <span data-ttu-id="aa2bd-167">Vous pouvez modifier la valeur par défaut en sélectionnant d’autres options dans les listes déroulantes respectives.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-167">You can change the default at either by selecting other options in the respective drop-downs.</span></span>

## <a name="sample-telemetry-custom-live-diagnostic-events"></a><span data-ttu-id="aa2bd-168">Exemple de télémétrie : événements de diagnostic temps réel personnalisés</span><span class="sxs-lookup"><span data-stu-id="aa2bd-168">Sample Telemetry: Custom Live Diagnostic Events</span></span>
<span data-ttu-id="aa2bd-169">Par défaut, le flux d’événements temps réel présente des exemples de demandes ayant échoué et d’appels de dépendance, d’exceptions, d’événements et de suivis.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-169">By default, the live feed of events shows samples of failed requests and dependency calls, exceptions, events, and traces.</span></span> <span data-ttu-id="aa2bd-170">Cliquez sur l’icône de filtre pour afficher les critères appliqués.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-170">Click the filter icon to see the applied criteria at any point in time.</span></span> 

![Flux temps réel par défaut](./media/app-insights-live-stream/live-stream-eventsdefault.png)

<span data-ttu-id="aa2bd-172">Comme avec les métriques, vous pouvez spécifier un critère arbitraire sur les types de données de télémétrie Application Insights.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-172">As with metrics, you can specify any arbitrary criteria to any of the Application Insights telemetry types.</span></span> <span data-ttu-id="aa2bd-173">Dans cet exemple, nous sélectionnons des échecs de demande, des suivis et des événements spécifiques.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-173">In this example, we are selecting specific request failures, traces, and events.</span></span> <span data-ttu-id="aa2bd-174">Nous sélectionnons également toutes les exceptions et tous les échecs de dépendance.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-174">We are also selecting all exceptions and dependency failures.</span></span>

![Flux temps réel personnalisé](./media/app-insights-live-stream/live-stream-events.png)

<span data-ttu-id="aa2bd-176">Remarque : pour les critères basés sur un message d’exception, utilisez le message d’exception le plus à l’extérieur.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-176">Note: Currently, for Exception message-based criteria, use the outermost exception message.</span></span> <span data-ttu-id="aa2bd-177">Dans l’exemple précédent, pour éliminer l’exception sans gravité avec le message d’exception interne (après le délimiteur « <-- ») « Client déconnecté ».</span><span class="sxs-lookup"><span data-stu-id="aa2bd-177">In the preceding example, to filter out the benign exception with inner exception message (follows the "<--" delimiter) "The client disconnected."</span></span> <span data-ttu-id="aa2bd-178">utilisez un critère de message ne contenant pas « Erreur de lecture du contenu de la demande ».</span><span class="sxs-lookup"><span data-stu-id="aa2bd-178">use a message not-contains "Error reading request content" criteria.</span></span>

<span data-ttu-id="aa2bd-179">Consultez les informations détaillées d’un élément dans le flux temps réel en cliquant dessus.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-179">See the details of an item in the live feed by clicking it.</span></span> <span data-ttu-id="aa2bd-180">Vous pouvez interrompre le flux en cliquant sur **Suspendre**, en faisant simplement défiler ou en cliquant sur un élément.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-180">You can pause the feed either by clicking **Pause** or simply scrolling down, or clicking an item.</span></span> <span data-ttu-id="aa2bd-181">Le flux temps réel reprend lorsque vous refaites défiler vers le haut, ou en cliquant sur le compteur d’éléments collectés alors qu’il était suspendu.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-181">Live feed will resume after you scroll back to the top, or by clicking the counter of items collected while it was paused.</span></span>

![Échecs dynamiques échantillonnés](./media/app-insights-live-stream/live-metrics-eventdetail.png)

## <a name="filter-by-server-instance"></a><span data-ttu-id="aa2bd-183">Filtrer par instance de serveur</span><span class="sxs-lookup"><span data-stu-id="aa2bd-183">Filter by server instance</span></span>

<span data-ttu-id="aa2bd-184">Si vous voulez surveiller une instance de rôle serveur spécifique, vous pouvez appliquer un filtre par serveur.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-184">If you want to monitor a particular server role instance, you can filter by server.</span></span>

![Échecs dynamiques échantillonnés](./media/app-insights-live-stream/live-stream-filter.png)

## <a name="sdk-requirements"></a><span data-ttu-id="aa2bd-186">Configuration requise du Kit de développement logiciel (SDK)</span><span class="sxs-lookup"><span data-stu-id="aa2bd-186">SDK Requirements</span></span>
<span data-ttu-id="aa2bd-187">Le flux de métriques temps réel personnalisé est disponible avec la version 2.4.0-beta2 ou plus récente du [Kit de développement logiciel (SDK) Application Insights pour le web](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span><span class="sxs-lookup"><span data-stu-id="aa2bd-187">Custom Live Metrics Stream is available with version 2.4.0-beta2 or newer of [Application Insights SDK for web](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span></span> <span data-ttu-id="aa2bd-188">N’oubliez pas de sélectionner l’option « Inclure la version préliminaire » dans le gestionnaire de package NuGet.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-188">Remember to select "Include Prerelease" option from NuGet package manager.</span></span>

## <a name="secure-the-control-channel"></a><span data-ttu-id="aa2bd-189">Sécuriser le canal de contrôle</span><span class="sxs-lookup"><span data-stu-id="aa2bd-189">Secure the control channel</span></span>
<span data-ttu-id="aa2bd-190">Les critères de filtres personnalisés que vous spécifiez sont renvoyés au composant de métriques temps réel dans le Kit de développement logiciel (SDK) Application Insights.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-190">The custom filters criteria you specify are sent back to the Live Metrics component in the Application Insights SDK.</span></span> <span data-ttu-id="aa2bd-191">Les filtres peuvent potentiellement contenir des informations sensibles telles que des ID clients.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-191">The filters could potentially contain sensitive information such as customerIDs.</span></span> <span data-ttu-id="aa2bd-192">Vous pouvez sécuriser le canal avec une clé API secrète en plus de la clé d’instrumentation.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-192">You can make the channel secure with a secret API key in addition to the instrumentation key.</span></span>
### <a name="create-an-api-key"></a><span data-ttu-id="aa2bd-193">Création d’une clé API</span><span class="sxs-lookup"><span data-stu-id="aa2bd-193">Create an API Key</span></span>

![Création d’une clé API](./media/app-insights-live-stream/live-metrics-apikeycreate.png)

### <a name="add-api-key-to-configuration"></a><span data-ttu-id="aa2bd-195">Ajout d’une clé API à la configuration</span><span class="sxs-lookup"><span data-stu-id="aa2bd-195">Add API key to Configuration</span></span>
<span data-ttu-id="aa2bd-196">Dans le fichier applicationinsights.config, ajoutez AuthenticationApiKey à QuickPulseTelemetryModule :</span><span class="sxs-lookup"><span data-stu-id="aa2bd-196">In the applicationinsights.config file, add the AuthenticationApiKey to the QuickPulseTelemetryModule:</span></span>
``` XML

<Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.QuickPulse.QuickPulseTelemetryModule, Microsoft.AI.PerfCounterCollector">
      <AuthenticationApiKey>YOUR-API-KEY-HERE</AuthenticationApiKey>
</Add> 

```
<span data-ttu-id="aa2bd-197">Ou dans le code, définissez-la sur QuickPulseTelemetryModule :</span><span class="sxs-lookup"><span data-stu-id="aa2bd-197">Or in code, set it on the QuickPulseTelemetryModule:</span></span>

``` C#

    module.AuthenticationApiKey = "YOUR-API-KEY-HERE";

```

<span data-ttu-id="aa2bd-198">Toutefois, si vous connaissez et faites confiance à tous les serveurs connectés, vous pouvez essayer les filtres personnalisés sans le canal authentifié.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-198">However, if you recognize and trust all the connected servers, you can try the custom filters without the authenticated channel.</span></span> <span data-ttu-id="aa2bd-199">Cette option est disponible pour six mois.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-199">This option is available for six months.</span></span> <span data-ttu-id="aa2bd-200">Ce remplacement est nécessaire à chaque nouvelle session, ou lorsqu’un nouveau serveur est en ligne.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-200">This override is required once every new session, or when a new server comes online.</span></span>

![Options d’authentification de métriques temps réel](./media/app-insights-live-stream/live-stream-auth.png)

>[!NOTE]
><span data-ttu-id="aa2bd-202">Nous vous recommandons vivement de configurer le canal authentifié avant d’entrer des informations potentiellement sensibles comme un ID client dans les critères de filtre.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-202">We strongly recommend that you set up the authenticated channel before entering potentially sensitive information like CustomerID in the filter criteria.</span></span>
>

## <a name="generating-a-performance-test-load"></a><span data-ttu-id="aa2bd-203">Génération d’un test de performances de charge</span><span class="sxs-lookup"><span data-stu-id="aa2bd-203">Generating a performance test load</span></span>

<span data-ttu-id="aa2bd-204">Si vous voulez observer l’effet d’une augmentation de la charge, utilisez le panneau Test de performances.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-204">If you want to watch the effect of a load increase, use the Performance Test blade.</span></span> <span data-ttu-id="aa2bd-205">Il simule des demandes à partir d’un certain nombre d’utilisateurs simultanés.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-205">It simulates requests from a number of simultaneous users.</span></span> <span data-ttu-id="aa2bd-206">Il peut s’exécuter des « tests manuels » (tests de ping) d’une URL unique, ou il peut exécuter un [test de performances web multi-étape](app-insights-monitor-web-app-availability.md#multi-step-web-tests) que vous chargez (de la même façon qu’un test de disponibilité).</span><span class="sxs-lookup"><span data-stu-id="aa2bd-206">It can run either "manual tests" (ping tests) of a single URL, or it can run a [multi-step web performance test](app-insights-monitor-web-app-availability.md#multi-step-web-tests) that you upload (in the same way as an availability test).</span></span>

> [!TIP]
> <span data-ttu-id="aa2bd-207">Après avoir créé le test de performances, ouvrez le test et le panneau Flux temps réel dans des fenêtres distinctes.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-207">After you create the performance test, open the test and the Live Stream blade in separate windows.</span></span> <span data-ttu-id="aa2bd-208">Vous pouvez voir quand le test de performances en file d’attente démarre, et observer le flux dynamique en même temps.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-208">You can see when the queued performance test starts, and watch live stream at the same time.</span></span>
>


## <a name="troubleshooting"></a><span data-ttu-id="aa2bd-209">résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="aa2bd-209">Troubleshooting</span></span>

<span data-ttu-id="aa2bd-210">Pas de données ?</span><span class="sxs-lookup"><span data-stu-id="aa2bd-210">No data?</span></span> <span data-ttu-id="aa2bd-211">Si votre application se trouve dans un réseau protégé : le Flux de métriques temps réel utilise des adresses IP différentes d’autres données de télémétrie Application Insights.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-211">If your application is in a protected network: Live Metrics Stream uses a different IP addresses than other Application Insights telemetry.</span></span> <span data-ttu-id="aa2bd-212">Assurez-vous que [ces adresses IP](app-insights-ip-addresses.md) sont ouvertes dans votre pare-feu.</span><span class="sxs-lookup"><span data-stu-id="aa2bd-212">Make sure [those IP addresses](app-insights-ip-addresses.md) are open in your firewall.</span></span>



## <a name="next-steps"></a><span data-ttu-id="aa2bd-213">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="aa2bd-213">Next steps</span></span>
* [<span data-ttu-id="aa2bd-214">Surveillance de l’utilisation avec Application Insights</span><span class="sxs-lookup"><span data-stu-id="aa2bd-214">Monitoring usage with Application Insights</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="aa2bd-215">Utilisation de Diagnostic Search</span><span class="sxs-lookup"><span data-stu-id="aa2bd-215">Using Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="aa2bd-216">Profileur</span><span class="sxs-lookup"><span data-stu-id="aa2bd-216">Profiler</span></span>](app-insights-profiler.md)
* [<span data-ttu-id="aa2bd-217">Débogueur de capture instantanée</span><span class="sxs-lookup"><span data-stu-id="aa2bd-217">Snapshot debugger</span></span>](app-insights-snapshot-debugger.md)
