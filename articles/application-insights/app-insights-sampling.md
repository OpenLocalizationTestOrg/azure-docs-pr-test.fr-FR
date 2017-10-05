---
title: "Échantillonnage de données de télémétrie dans Azure Application Insights | Microsoft Docs"
description: "Comment maintenir sous contrôle le volume de télémétrie."
services: application-insights
documentationcenter: windows
author: vgorbenko
manager: carmonm
ms.assetid: 015ab744-d514-42c0-8553-8410eef00368
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bwren
ms.openlocfilehash: ceaeced414c9c302fba335b4578bcdcbfaef0410
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="sampling-in-application-insights"></a><span data-ttu-id="c9c80-103">Échantillonnage dans Application Insights</span><span class="sxs-lookup"><span data-stu-id="c9c80-103">Sampling in Application Insights</span></span>


<span data-ttu-id="c9c80-104">L’échantillonnage est une fonctionnalité dans [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c9c80-104">Sampling is a feature in [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="c9c80-105">Il s’agit de la méthode recommandée pour réduire le trafic et le stockage des données de télémétrie, tout en conservant une analyse statistiquement correcte des données d’application.</span><span class="sxs-lookup"><span data-stu-id="c9c80-105">It is the recommended way to reduce telemetry traffic and storage, while preserving  a statistically correct analysis of application data.</span></span> <span data-ttu-id="c9c80-106">Le filtre sélectionne les éléments associés afin que vous puissiez naviguer entre les éléments lorsque vous effectuez un diagnostic.</span><span class="sxs-lookup"><span data-stu-id="c9c80-106">The filter selects items that are related, so that you can navigate between items when you are doing diagnostic investigations.</span></span>
<span data-ttu-id="c9c80-107">Lorsque les données de mesure apparaissent sur le portail, elles sont renormalisées pour tenir compte de l’échantillonnage, afin de réduire tout effet sur les statistiques.</span><span class="sxs-lookup"><span data-stu-id="c9c80-107">When metric counts are presented to you in the portal, they are renormalized to take account of the sampling, to minimize any effect on the statistics.</span></span>

<span data-ttu-id="c9c80-108">L’échantillonnage réduit les coûts du trafic et des données, et vous aide à éviter les limitations.</span><span class="sxs-lookup"><span data-stu-id="c9c80-108">Sampling reduces traffic and data costs, and helps you avoid throttling.</span></span>

## <a name="in-brief"></a><span data-ttu-id="c9c80-109">En bref :</span><span class="sxs-lookup"><span data-stu-id="c9c80-109">In brief:</span></span>
* <span data-ttu-id="c9c80-110">Échantillonnage conserve 1 dans  *n*  enregistre et ignore le reste.</span><span class="sxs-lookup"><span data-stu-id="c9c80-110">Sampling retains 1 in *n* records and discards the rest.</span></span> <span data-ttu-id="c9c80-111">Par exemple, il peut conserver 1 événement sur 5, soit un taux d’échantillonnage de 20 %.</span><span class="sxs-lookup"><span data-stu-id="c9c80-111">For example, it might retain 1 in 5 events, a sampling rate of 20%.</span></span> 
* <span data-ttu-id="c9c80-112">L’échantillonnage s’effectue automatiquement si votre application envoie de nombreuses données de télémétrie, dans les applications de serveur web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="c9c80-112">Sampling happens automatically if your application sends a lot of telemetry, in ASP.NET web server apps.</span></span>
* <span data-ttu-id="c9c80-113">Vous pouvez également définir l’échantillonnage manuellement, dans le portail sur la page de tarification ou dans le Kit de développement logiciel (SDK) ASP.NET dans le fichier .config, pour réduire également le trafic réseau.</span><span class="sxs-lookup"><span data-stu-id="c9c80-113">You can also set sampling manually, either in the portal on the pricing page; or in the ASP.NET SDK in the .config file, to also reduce the network traffic.</span></span>
* <span data-ttu-id="c9c80-114">Si vous consignez des événements personnalisés et que vous souhaitez vous assurer qu’un ensemble d’événements soit conservé ou ignoré conjointement, faites en sorte qu’ils aient la même valeur OperationId.</span><span class="sxs-lookup"><span data-stu-id="c9c80-114">If you log custom events and you want to make sure that a set of events is either retained or discarded together, make sure that they have the same OperationId value.</span></span>
* <span data-ttu-id="c9c80-115">Le diviseur d’échantillonnage  *n*  est signalée dans chaque enregistrement de la propriété `itemCount`, qui, dans la recherche s’affiche sous le nom convivial « nombre de demande » ou « nombre d’événements ».</span><span class="sxs-lookup"><span data-stu-id="c9c80-115">The sampling divisor *n* is reported in each record in the property `itemCount`, which in Search appears under the friendly name "request count" or "event count".</span></span> <span data-ttu-id="c9c80-116">Lorsque l’échantillonnage n’est pas en cours d’utilisation, `itemCount==1`.</span><span class="sxs-lookup"><span data-stu-id="c9c80-116">When sampling is not in operation, `itemCount==1`.</span></span>
* <span data-ttu-id="c9c80-117">Si vous écrivez des requêtes Analytics, vous devez [tenir compte de l’échantillonnage](app-insights-analytics-tour.md#counting-sampled-data).</span><span class="sxs-lookup"><span data-stu-id="c9c80-117">If you write Analytics queries, you should [take account of sampling](app-insights-analytics-tour.md#counting-sampled-data).</span></span> <span data-ttu-id="c9c80-118">En particulier, au lieu de compter simplement les enregistrements, vous devez utiliser `summarize sum(itemCount)`.</span><span class="sxs-lookup"><span data-stu-id="c9c80-118">In particular, instead of simply counting records, you should use `summarize sum(itemCount)`.</span></span>

## <a name="types-of-sampling"></a><span data-ttu-id="c9c80-119">Types d’échantillonnage</span><span class="sxs-lookup"><span data-stu-id="c9c80-119">Types of sampling</span></span>
<span data-ttu-id="c9c80-120">Il existe trois autres méthodes d’échantillonnage :</span><span class="sxs-lookup"><span data-stu-id="c9c80-120">There are three alternative sampling methods:</span></span>

* <span data-ttu-id="c9c80-121">**échantillonnage adaptatif** ajuste automatiquement le volume de données de télémétrie envoyées à partir du Kit de développement logiciel (SDK) dans votre application ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="c9c80-121">**Adaptive sampling** automatically adjusts the volume of telemetry sent from the SDK in your ASP.NET app.</span></span> <span data-ttu-id="c9c80-122">Il s’agit du comportement par défaut depuis la version 2.0.0-beta3 du Kit de développement logiciel (SDK).</span><span class="sxs-lookup"><span data-stu-id="c9c80-122">Default from SDK v 2.0.0-beta3.</span></span> <span data-ttu-id="c9c80-123">Actuellement uniquement disponible pour la télémétrie ASP.NET côté serveur.</span><span class="sxs-lookup"><span data-stu-id="c9c80-123">Currently available for ASP.NET server-side telemetry only.</span></span> 
* <span data-ttu-id="c9c80-124">**échantillonnage à débit fixe** réduit le volume de données de télémétrie envoyées à partir de votre serveur ASP.NET et des navigateurs de vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="c9c80-124">**Fixed-rate sampling** reduces the volume of telemetry sent from both your ASP.NET server and from your users' browsers.</span></span> <span data-ttu-id="c9c80-125">Vous définissez le débit.</span><span class="sxs-lookup"><span data-stu-id="c9c80-125">You set the rate.</span></span> <span data-ttu-id="c9c80-126">Le client et le serveur synchronisent leur échantillonnage de façon à ce que vous puissiez naviguer entre les demandes et les affichages de pages associés dans Search.</span><span class="sxs-lookup"><span data-stu-id="c9c80-126">The client and server will synchronize their sampling so that, in Search, you can navigate between related page views and requests.</span></span>
* <span data-ttu-id="c9c80-127">**L’échantillonnage d’ingestion** fonctionne dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c9c80-127">**Ingestion sampling** works in the Azure portal.</span></span> <span data-ttu-id="c9c80-128">Il ignore certaines données de télémétrie provenant de votre application, à une fréquence que vous définissez.</span><span class="sxs-lookup"><span data-stu-id="c9c80-128">It discards some of the telemetry that arrives from your app, at a rate that you set.</span></span> <span data-ttu-id="c9c80-129">Le trafic des données de télémétrie n’est pas réduit, mais cela vous permet de respecter votre quota mensuel.</span><span class="sxs-lookup"><span data-stu-id="c9c80-129">It doesn't reduce telemetry traffic, but helps you keep within your monthly quota.</span></span> <span data-ttu-id="c9c80-130">Le grand avantage de l’échantillonnage d’ingestion est que vous pouvez le définir sans avoir à redéployer votre application et qu’il fonctionne uniformément pour tous les clients et serveurs.</span><span class="sxs-lookup"><span data-stu-id="c9c80-130">The big advantage of ingestion sampling is that you can set it without redeploying your app, and it works uniformly for all servers and clients.</span></span> 

<span data-ttu-id="c9c80-131">Si un échantillonnage de débit adaptatif ou fixe est en cours d’utilisation, l’échantillonnage d’ingestion est désactivé.</span><span class="sxs-lookup"><span data-stu-id="c9c80-131">If Adaptive or Fixed rate sampling are in operation, Ingestion sampling is disabled.</span></span>

## <a name="ingestion-sampling"></a><span data-ttu-id="c9c80-132">échantillonnage d’ingestion</span><span class="sxs-lookup"><span data-stu-id="c9c80-132">Ingestion sampling</span></span>
<span data-ttu-id="c9c80-133">Cette forme d’échantillonnage fonctionne au niveau où les données de télémétrie issues de votre serveur web, des navigateurs et des appareils atteignent le point de terminaison du service Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c9c80-133">This form of sampling operates at the point where the telemetry from your web server, browsers, and devices reaches the Application Insights service endpoint.</span></span> <span data-ttu-id="c9c80-134">Bien qu’elle ne réduise pas le trafic des données de télémétrie envoyées à partir de votre application, elle réduit la quantité traitée et conservée (et facturée) par Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c9c80-134">Although it doesn't reduce the telemetry traffic sent from your app, it does reduce the amount processed and retained (and charged for) by Application Insights.</span></span>

<span data-ttu-id="c9c80-135">Utilisez ce type d’échantillonnage si votre application dépasse souvent son quota mensuel et que vous ne pouvez recourir à aucun type d’échantillonnage basé sur le Kit de développement logiciel (SDK).</span><span class="sxs-lookup"><span data-stu-id="c9c80-135">Use this type of sampling if your app often goes over its monthly quota and you don't have the option of using either of the SDK-based types of sampling.</span></span> 

<span data-ttu-id="c9c80-136">Définissez le taux d’échantillonnage dans le panneau Quota + tarification :</span><span class="sxs-lookup"><span data-stu-id="c9c80-136">Set the sampling rate in the Quotas and Pricing blade:</span></span>

![Dans le panneau Vue d’ensemble de l’application, cliquez sur Paramètres, Quota + tarification, Échantillons conservés, sélectionnez un taux d’échantillonnage, puis cliquez sur Mettre à jour.](./media/app-insights-sampling/04.png)

<span data-ttu-id="c9c80-138">Comme d’autres types d’échantillonnage, l’algorithme conserve les éléments de télémétrie associés.</span><span class="sxs-lookup"><span data-stu-id="c9c80-138">Like other types of sampling, the algorithm retains related telemetry items.</span></span> <span data-ttu-id="c9c80-139">Par exemple, quand vous inspectez les données de télémétrie dans Search, vous pouvez trouver la demande liée à une exception spécifique.</span><span class="sxs-lookup"><span data-stu-id="c9c80-139">For example, when you're inspecting the telemetry in Search, you'll be able to find the request related to a particular exception.</span></span> <span data-ttu-id="c9c80-140">Les données de mesure telles que les taux de demandes et le taux d’exceptions sont correctement conservées.</span><span class="sxs-lookup"><span data-stu-id="c9c80-140">Metric counts such as request rate and exception rate are correctly retained.</span></span>

<span data-ttu-id="c9c80-141">Les points de données ignorés par l’échantillonnage ne sont disponibles dans aucune fonctionnalité Application Insights, par exemple l’ [exportation continue](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="c9c80-141">Data points that are discarded by sampling are not available in any Application Insights feature such as [Continuous Export](app-insights-export-telemetry.md).</span></span>

<span data-ttu-id="c9c80-142">L’échantillonnage d’ingestion ne fonctionne pas pendant qu’une opération d’échantillonnage adaptatif ou taux fixe basé sur un Kit de développement logiciel (SDK) est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="c9c80-142">Ingestion sampling doesn't operate while SDK-based adaptive or fixed-rate sampling is in operation.</span></span> <span data-ttu-id="c9c80-143">Si le taux d’échantillonnage dans le Kit de développement logiciel (SDK) est inférieur à 100 %, le taux d’échantillonnage d’ingestion que vous avez défini est ignoré.</span><span class="sxs-lookup"><span data-stu-id="c9c80-143">If the sampling rate at the SDK is less than 100%, then the ingestion sampling rate that you set is ignored.</span></span>

> [!WARNING]
> <span data-ttu-id="c9c80-144">La valeur affichée sur la vignette indique la valeur que vous définissez pour l’échantillonnage d’ingestion.</span><span class="sxs-lookup"><span data-stu-id="c9c80-144">The value shown on the tile indicates the value that you set for ingestion sampling.</span></span> <span data-ttu-id="c9c80-145">Il ne représente pas le taux d’échantillonnage réel si l’échantillonnage du kit de développement logiciel (SDK) est effectué.</span><span class="sxs-lookup"><span data-stu-id="c9c80-145">It doesn't represent the actual sampling rate if SDK sampling is in operation.</span></span>
> 
> 

## <a name="adaptive-sampling-at-your-web-server"></a><span data-ttu-id="c9c80-146">Échantillonnage adaptatif sur votre serveur web</span><span class="sxs-lookup"><span data-stu-id="c9c80-146">Adaptive sampling at your web server</span></span>
<span data-ttu-id="c9c80-147">L’échantillonnage adaptatif est disponible pour le Kit de développement logiciel (SDK) Application Insights pour ASP.NET version 2.0.0-beta3 et ultérieures et est activé par défaut.</span><span class="sxs-lookup"><span data-stu-id="c9c80-147">Adaptive sampling is available for the Application Insights SDK for ASP.NET v 2.0.0-beta3 and later, and is enabled by default.</span></span> 

<span data-ttu-id="c9c80-148">L’échantillonnage adaptatif a une incidence sur le volume de données de télémétrie envoyées à partir de votre application de serveur web au service Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c9c80-148">Adaptive sampling affects the volume of telemetry sent from your web server app to the Application Insights service.</span></span> <span data-ttu-id="c9c80-149">Le volume est automatiquement maintenu en deçà d’un débit de trafic maximal spécifié.</span><span class="sxs-lookup"><span data-stu-id="c9c80-149">The volume is adjusted automatically to keep within a specified maximum rate of traffic.</span></span>

<span data-ttu-id="c9c80-150">Il ne fonctionne pas quand les volumes de données de télémétrie sont bas ; ainsi, une application en mode débogage ou un site web faiblement utilisé ne sont pas affectés.</span><span class="sxs-lookup"><span data-stu-id="c9c80-150">It doesn't operate at low volumes of telemetry, so an app in debugging or a website with low usage won't be affected.</span></span>

<span data-ttu-id="c9c80-151">Pour atteindre le volume cible, certaines des données de télémétrie générées sont ignorées.</span><span class="sxs-lookup"><span data-stu-id="c9c80-151">To achieve the target volume, some of the telemetry generated is discarded.</span></span> <span data-ttu-id="c9c80-152">Toutefois, comme d’autres types d’échantillonnage, l’algorithme conserve les éléments de télémétrie associés.</span><span class="sxs-lookup"><span data-stu-id="c9c80-152">But like other types of sampling, the algorithm retains related telemetry items.</span></span> <span data-ttu-id="c9c80-153">Par exemple, quand vous inspectez les données de télémétrie dans Search, vous pouvez trouver la demande liée à une exception spécifique.</span><span class="sxs-lookup"><span data-stu-id="c9c80-153">For example, when you're inspecting the telemetry in Search, you'll be able to find the request related to a particular exception.</span></span> 

<span data-ttu-id="c9c80-154">Les données de mesure telles que le taux de demandes et le taux d’exceptions sont ajustées pour compenser le taux d’échantillonnage, afin qu’elles affichent des valeurs approximativement correctes dans Metrics Explorer.</span><span class="sxs-lookup"><span data-stu-id="c9c80-154">Metric counts such as request rate and exception rate are adjusted to compensate for the sampling rate, so that they show approximately correct values in Metric Explorer.</span></span>

<span data-ttu-id="c9c80-155">**Mettez à jour les packages NuGet de votre projet** vers la version *préliminaire* d’Application Insights la plus récente : cliquez avec le bouton droit sur le projet dans l’Explorateur de solutions, sélectionnez Gérer les packages NuGet, cochez **Inclure la version préliminaire** et recherchez Microsoft.ApplicationInsights.Web.</span><span class="sxs-lookup"><span data-stu-id="c9c80-155">**Update your project's NuGet** packages to the latest *pre-release* version of Application Insights: Right-click the project in Solution Explorer, choose Manage NuGet Packages, check **Include prerelease** and search for Microsoft.ApplicationInsights.Web.</span></span> 

<span data-ttu-id="c9c80-156">Dans [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), vous pouvez ajuster plusieurs paramètres dans le nœud `AdaptiveSamplingTelemetryProcessor`.</span><span class="sxs-lookup"><span data-stu-id="c9c80-156">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), you can adjust several parameters in the `AdaptiveSamplingTelemetryProcessor` node.</span></span> <span data-ttu-id="c9c80-157">Les chiffres indiqués correspondent aux valeurs par défaut :</span><span class="sxs-lookup"><span data-stu-id="c9c80-157">The figures shown are the default values:</span></span>

* `<MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>`
  
    <span data-ttu-id="c9c80-158">Taux cible que l’algorithme adaptatif tente d’atteindre **sur chaque hôte du serveur**.</span><span class="sxs-lookup"><span data-stu-id="c9c80-158">The target rate that the adaptive algorithm aims for **on each server host**.</span></span> <span data-ttu-id="c9c80-159">Si votre application web s’exécute sur plusieurs hôtes, réduisez cette valeur afin de ne pas dépasser votre débit de trafic cible sur le portail Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c9c80-159">If your web app runs on many hosts, reduce this value so as to remain within your target rate of traffic at the Application Insights portal.</span></span>
* `<EvaluationInterval>00:00:15</EvaluationInterval>` 
  
    <span data-ttu-id="c9c80-160">Intervalle auquel le taux actuel de télémétrie est réévalué.</span><span class="sxs-lookup"><span data-stu-id="c9c80-160">The interval at which the current rate of telemetry is re-evaluated.</span></span> <span data-ttu-id="c9c80-161">L’évaluation est effectuée sous forme de moyenne mobile.</span><span class="sxs-lookup"><span data-stu-id="c9c80-161">Evaluation is performed as a moving average.</span></span> <span data-ttu-id="c9c80-162">Vous souhaiterez peut-être raccourcir cet intervalle si vos données de télémétrie sont soumises à des pics soudains.</span><span class="sxs-lookup"><span data-stu-id="c9c80-162">You might want to shorten this interval if your telemetry is liable to sudden bursts.</span></span>
* `<SamplingPercentageDecreaseTimeout>00:02:00</SamplingPercentageDecreaseTimeout>`
  
    <span data-ttu-id="c9c80-163">En cas de modification du pourcentage d’échantillonnage, délai avant que le pourcentage d’échantillonnage puisse de nouveau être réduit pour capturer moins de données.</span><span class="sxs-lookup"><span data-stu-id="c9c80-163">When sampling percentage value changes, how soon after are we allowed to lower sampling percentage again to capture less data.</span></span>
* `<SamplingPercentageIncreaseTimeout>00:15:00</SamplingPercentageIncreaseTimeout>`
  
    <span data-ttu-id="c9c80-164">En cas de modification du pourcentage d’échantillonnage, délai avant que le pourcentage d’échantillonnage puisse de nouveau être augmenté pour capturer plus de données.</span><span class="sxs-lookup"><span data-stu-id="c9c80-164">When sampling percentage value changes, how soon after are we allowed to increase sampling percentage again to capture more data.</span></span>
* `<MinSamplingPercentage>0.1</MinSamplingPercentage>`
  
    <span data-ttu-id="c9c80-165">Lors des variations du pourcentage d’échantillonnage, valeur minimale autorisée.</span><span class="sxs-lookup"><span data-stu-id="c9c80-165">As sampling percentage varies, what is the minimum value we're allowed to set.</span></span>
* `<MaxSamplingPercentage>100.0</MaxSamplingPercentage>`
  
    <span data-ttu-id="c9c80-166">Lors des variations du pourcentage d’échantillonnage, valeur maximale autorisée.</span><span class="sxs-lookup"><span data-stu-id="c9c80-166">As sampling percentage varies, what is the maximum value we're allowed to set.</span></span>
* `<MovingAverageRatio>0.25</MovingAverageRatio>` 
  
    <span data-ttu-id="c9c80-167">Lors du calcul de la moyenne mobile, poids affecté à la valeur la plus récente.</span><span class="sxs-lookup"><span data-stu-id="c9c80-167">In the calculation of the moving average, the weight assigned to the most recent value.</span></span> <span data-ttu-id="c9c80-168">Utilisez une valeur inférieure ou égale à 1.</span><span class="sxs-lookup"><span data-stu-id="c9c80-168">Use a value equal to or less than 1.</span></span> <span data-ttu-id="c9c80-169">Plus les valeurs sont petites, moins l’algorithme est réactif en cas de modifications brusques.</span><span class="sxs-lookup"><span data-stu-id="c9c80-169">Smaller values make the algorithm less reactive to sudden changes.</span></span>
* `<InitialSamplingPercentage>100</InitialSamplingPercentage>`
  
    <span data-ttu-id="c9c80-170">Valeur affectée lorsque l’application vient de démarrer.</span><span class="sxs-lookup"><span data-stu-id="c9c80-170">The value assigned when the app has just started.</span></span> <span data-ttu-id="c9c80-171">Ne diminuez pas cette valeur pendant le débogage.</span><span class="sxs-lookup"><span data-stu-id="c9c80-171">Don't reduce this while you're debugging.</span></span> 

* `<ExcludedTypes>Trace;Exception</ExcludedTypes>`
  
    <span data-ttu-id="c9c80-172">Une liste délimitée par des points-virgules des types que vous ne souhaitez pas voir échantillonnés.</span><span class="sxs-lookup"><span data-stu-id="c9c80-172">A semi-colon delimited list of types that you do not want to be sampled.</span></span> <span data-ttu-id="c9c80-173">Les types reconnus sont : Dependency, Event, Exception, PageView, Request et Trace.</span><span class="sxs-lookup"><span data-stu-id="c9c80-173">Recognized types are: Dependency, Event, Exception, PageView, Request, Trace.</span></span> <span data-ttu-id="c9c80-174">Toutes les instances des types spécifiés sont transmises ; les types qui ne sont pas spécifiés sont échantillonnés.</span><span class="sxs-lookup"><span data-stu-id="c9c80-174">All instances of the specified types are transmitted; the types that are not specified are sampled.</span></span>

* `<IncludedTypes>Request;Dependency</IncludedTypes>`
  
    <span data-ttu-id="c9c80-175">Une liste délimitée par des points-virgules des types que vous souhaitez échantillonner.</span><span class="sxs-lookup"><span data-stu-id="c9c80-175">A semi-colon delimited list of types that you want to be sampled.</span></span> <span data-ttu-id="c9c80-176">Les types reconnus sont : Dependency, Event, Exception, PageView, Request et Trace.</span><span class="sxs-lookup"><span data-stu-id="c9c80-176">Recognized types are: Dependency, Event, Exception, PageView, Request, Trace.</span></span> <span data-ttu-id="c9c80-177">Les types spécifiés sont échantillonnés ; toutes les instances des autres types sont toujours transmises.</span><span class="sxs-lookup"><span data-stu-id="c9c80-177">The specified types are sampled; all instances of the other types will always be transmitted.</span></span>


<span data-ttu-id="c9c80-178">**Pour désactiver** l’échantillonnage adaptatif, supprimez le nœud AdaptiveSamplingTelemetryProcessor de applicationinsights-config.</span><span class="sxs-lookup"><span data-stu-id="c9c80-178">**To switch off** adaptive sampling, remove the AdaptiveSamplingTelemetryProcessor node from applicationinsights-config.</span></span>

### <a name="alternative-configure-adaptive-sampling-in-code"></a><span data-ttu-id="c9c80-179">Solution alternative : configurer l’échantillonnage adaptatif dans le code</span><span class="sxs-lookup"><span data-stu-id="c9c80-179">Alternative: configure adaptive sampling in code</span></span>
<span data-ttu-id="c9c80-180">Au lieu d’ajuster l’échantillonnage dans le fichier .config, vous pouvez utiliser le code.</span><span class="sxs-lookup"><span data-stu-id="c9c80-180">Instead of adjusting sampling in the .config file, you can use code.</span></span> <span data-ttu-id="c9c80-181">Cela vous permet de spécifier une fonction de rappel qui est appelée chaque fois que le taux d’échantillonnage est réévalué.</span><span class="sxs-lookup"><span data-stu-id="c9c80-181">This allows you to specify a callback function that is invoked whenever the sampling rate is re-evaluated.</span></span> <span data-ttu-id="c9c80-182">Par exemple, vous pouvez utiliser cette fonction pour savoir quel est le taux d’échantillonnage utilisé.</span><span class="sxs-lookup"><span data-stu-id="c9c80-182">You could use this, for example, to find out what sampling rate is being used.</span></span>

<span data-ttu-id="c9c80-183">Supprimer le nœud `AdaptiveSamplingTelemetryProcessor` du fichier .config.</span><span class="sxs-lookup"><span data-stu-id="c9c80-183">Remove the `AdaptiveSamplingTelemetryProcessor` node from the .config file.</span></span>

<span data-ttu-id="c9c80-184">*C#*</span><span class="sxs-lookup"><span data-stu-id="c9c80-184">*C#*</span></span>

```C#

    using Microsoft.ApplicationInsights;
    using Microsoft.ApplicationInsights.Extensibility;
    using Microsoft.ApplicationInsights.WindowsServer.Channel.Implementation;
    using Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel;
    ...

    var adaptiveSamplingSettings = new SamplingPercentageEstimatorSettings();

    // Optional: here you can adjust the settings from their defaults.

    var builder = TelemetryConfiguration.Active.TelemetryProcessorChainBuilder;

    builder.UseAdaptiveSampling(
         adaptiveSamplingSettings,

        // Callback on rate re-evaluation:
        (double afterSamplingTelemetryItemRatePerSecond,
         double currentSamplingPercentage,
         double newSamplingPercentage,
         bool isSamplingPercentageChanged,
         SamplingPercentageEstimatorSettings s
        ) =>
        {
          if (isSamplingPercentageChanged)
          {
             // Report the sampling rate.
             telemetryClient.TrackMetric("samplingPercentage", newSamplingPercentage);
          }
      });

    // If you have other telemetry processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

<span data-ttu-id="c9c80-185">([En savoir plus sur les processeurs de télémétrie](app-insights-api-filtering-sampling.md#filtering).)</span><span class="sxs-lookup"><span data-stu-id="c9c80-185">([Learn about telemetry processors](app-insights-api-filtering-sampling.md#filtering).)</span></span>

<a name="other-web-pages"></a>

## <a name="sampling-for-web-pages-with-javascript"></a><span data-ttu-id="c9c80-186">Échantillonnage pour les pages web avec JavaScript</span><span class="sxs-lookup"><span data-stu-id="c9c80-186">Sampling for web pages with JavaScript</span></span>
<span data-ttu-id="c9c80-187">Vous pouvez configurer des pages Web pour l’échantillonnage à débit fixe à partir de n’importe quel serveur.</span><span class="sxs-lookup"><span data-stu-id="c9c80-187">You can configure web pages for fixed-rate sampling from any server.</span></span> 

<span data-ttu-id="c9c80-188">Lorsque vous [configurez les pages web pour Application Insights](app-insights-javascript.md), modifiez l’extrait de code que vous obtenez à partir du portail Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c9c80-188">When you [configure the web pages for Application Insights](app-insights-javascript.md), modify the snippet that you get from the Application Insights portal.</span></span> <span data-ttu-id="c9c80-189">(Dans les applications ASP.NET, l’extrait de code passe généralement dans _Layout.cshtml.)  Insérez une ligne de type `samplingPercentage: 10,` avant la clé d’instrumentation :</span><span class="sxs-lookup"><span data-stu-id="c9c80-189">(In ASP.NET apps, the snippet typically goes in _Layout.cshtml.)  Insert a line like `samplingPercentage: 10,` before the instrumentation key:</span></span>

    <script>
    var appInsights= ... 
    }({ 


    // Value must be 100/N where N is an integer.
    // Valid examples: 50, 25, 20, 10, 5, 1, 0.1, ...
    samplingPercentage: 10, 

    instrumentationKey:...
    }); 

    window.appInsights=appInsights; 
    appInsights.trackPageView(); 
    </script> 

<span data-ttu-id="c9c80-190">Pour le pourcentage d’échantillonnage, choisissez un pourcentage proche de 100/N, où N est un nombre entier.</span><span class="sxs-lookup"><span data-stu-id="c9c80-190">For the sampling percentage, choose a percentage that is close to 100/N where N is an integer.</span></span>  <span data-ttu-id="c9c80-191">L’échantillonnage ne prend actuellement en charge aucune autre valeur.</span><span class="sxs-lookup"><span data-stu-id="c9c80-191">Currently sampling doesn't support other values.</span></span>

<span data-ttu-id="c9c80-192">Si vous avez activé l’échantillonnage à débit fixe sur le serveur, les clients et le serveur se synchronisent de façon à ce que, dans Recherche, vous puissiez naviguer entre les demandes et les affichages de pages associés.</span><span class="sxs-lookup"><span data-stu-id="c9c80-192">If you also enable fixed-rate sampling at the server, the clients and server will synchronize so that, in Search, you can  navigate between related page views and requests.</span></span>

## <a name="fixed-rate-sampling-for-aspnet-web-sites"></a><span data-ttu-id="c9c80-193">Échantillonnage à débit fixe pour les sites web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="c9c80-193">Fixed-rate sampling for ASP.NET web sites</span></span>
<span data-ttu-id="c9c80-194">L’échantillonnage à débit fixe réduit le trafic envoyé depuis votre serveur web et les navigateurs web.</span><span class="sxs-lookup"><span data-stu-id="c9c80-194">Fixed rate sampling reduces the traffic sent from your web server and web browsers.</span></span> <span data-ttu-id="c9c80-195">À la différence de l’échantillonnage adaptatif, il réduit les données de télémétrie à un débit fixe choisi par vos soins.</span><span class="sxs-lookup"><span data-stu-id="c9c80-195">Unlike adaptive sampling, it reduces telemetry at a fixed rate decided by you.</span></span> <span data-ttu-id="c9c80-196">En outre, il synchronise l’échantillonnage client et serveur afin que les éléments associés soient conservés ; par exemple, si vous examinez un affichage de page dans Search, vous pouvez trouver sa demande associée.</span><span class="sxs-lookup"><span data-stu-id="c9c80-196">It also synchronizes the client and server sampling so that related items are retained - for example, so that if you look at a page view in Search, you can find its related request.</span></span>

<span data-ttu-id="c9c80-197">L’algorithme d’échantillonnage conserve les éléments associés.</span><span class="sxs-lookup"><span data-stu-id="c9c80-197">The sampling algorithm retains related items.</span></span> <span data-ttu-id="c9c80-198">Pour chaque événement de requête HTTP, celui-ci et ses événements associés sont ignorés ou transmis.</span><span class="sxs-lookup"><span data-stu-id="c9c80-198">For each HTTP request event, it and its related events are either discarded or transmitted.</span></span> 

<span data-ttu-id="c9c80-199">Dans Metrics Explorer, les taux tels que le nombre de demandes et d’exceptions sont multipliés par un facteur pour compenser le taux d’échantillonnage, afin qu’ils soient approximativement corrects.</span><span class="sxs-lookup"><span data-stu-id="c9c80-199">In Metrics Explorer, rates such as request and exception counts are multiplied by a factor to compensate for the sampling rate, so that they are approximately correct.</span></span>

1. <span data-ttu-id="c9c80-200">**Mettez à jour les packages NuGet de votre projet** vers la dernière version *préliminaire* d’Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c9c80-200">**Update your project's NuGet packages** to the latest *pre-release* version of Application Insights.</span></span> <span data-ttu-id="c9c80-201">Cliquez avec le bouton droit sur le projet dans l’Explorateur de solutions, sélectionnez Gérer les packages NuGet, cochez **Inclure la version préliminaire** et recherchez Microsoft.ApplicationInsights.Web.</span><span class="sxs-lookup"><span data-stu-id="c9c80-201">Right-click the project in Solution Explorer, choose Manage NuGet Packages, check **Include prerelease** and search for Microsoft.ApplicationInsights.Web.</span></span> 
2. <span data-ttu-id="c9c80-202">**Désactivez l’échantillonnage adaptatif** : dans [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), supprimez ou commentez le nœud `AdaptiveSamplingTelemetryProcessor`.</span><span class="sxs-lookup"><span data-stu-id="c9c80-202">**Disable adaptive sampling**: In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), remove or comment out the `AdaptiveSamplingTelemetryProcessor` node.</span></span>
   
    ```xml
   
    <TelemetryProcessors>
   
    <!-- Disabled adaptive sampling:
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    -->

    ```

1. <span data-ttu-id="c9c80-203">**Activez le module d’échantillonnage à débit fixe.**</span><span class="sxs-lookup"><span data-stu-id="c9c80-203">**Enable the fixed-rate sampling module.**</span></span> <span data-ttu-id="c9c80-204">Ajoutez cet extrait de code à [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span><span class="sxs-lookup"><span data-stu-id="c9c80-204">Add this snippet to [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span>
   
    ```XML
   
    <TelemetryProcessors>
     <Add  Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
   
      <!-- Set a percentage close to 100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
      <SamplingPercentage>10</SamplingPercentage>
      </Add>
    </TelemetryProcessors>
   
    ```

> [!NOTE]
> <span data-ttu-id="c9c80-205">Pour le pourcentage d’échantillonnage, choisissez un pourcentage proche de 100/N, où N est un nombre entier.</span><span class="sxs-lookup"><span data-stu-id="c9c80-205">For the sampling percentage, choose a percentage that is close to 100/N where N is an integer.</span></span>  <span data-ttu-id="c9c80-206">L’échantillonnage ne prend actuellement en charge aucune autre valeur.</span><span class="sxs-lookup"><span data-stu-id="c9c80-206">Currently sampling doesn't support other values.</span></span>
> 
> 

### <a name="alternative-enable-fixed-rate-sampling-in-your-server-code"></a><span data-ttu-id="c9c80-207">Solution alternative : activez l’échantillonnage à taux fixe dans le code serveur</span><span class="sxs-lookup"><span data-stu-id="c9c80-207">Alternative: enable fixed-rate sampling in your server code</span></span>
<span data-ttu-id="c9c80-208">Au lieu de définir le paramètre d’échantillonnage dans le fichier .config, vous pouvez utiliser le code.</span><span class="sxs-lookup"><span data-stu-id="c9c80-208">Instead of setting the sampling parameter in the .config file, you can use code.</span></span> 

<span data-ttu-id="c9c80-209">*C#*</span><span class="sxs-lookup"><span data-stu-id="c9c80-209">*C#*</span></span>

```C#

    using Microsoft.ApplicationInsights.Extensibility;
    using Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel;
    ...

    var builder = TelemetryConfiguration.Active.GetTelemetryProcessorChainBuilder();
    builder.UseSampling(10.0); // percentage

    // If you have other telemetry processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

<span data-ttu-id="c9c80-210">([En savoir plus sur les processeurs de télémétrie](app-insights-api-filtering-sampling.md#filtering).)</span><span class="sxs-lookup"><span data-stu-id="c9c80-210">([Learn about telemetry processors](app-insights-api-filtering-sampling.md#filtering).)</span></span>

## <a name="when-to-use-sampling"></a><span data-ttu-id="c9c80-211">Quand utiliser l’échantillonnage ?</span><span class="sxs-lookup"><span data-stu-id="c9c80-211">When to use sampling?</span></span>
<span data-ttu-id="c9c80-212">L’échantillonnage adaptatif est automatiquement activé si vous utilisez la version 2.0.0-beta3 du Kit de développement logiciel (SDK) ASP.NET, ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="c9c80-212">Adaptive sampling is automatically enabled if you use the ASP.NET SDK version 2.0.0-beta3 or later.</span></span> <span data-ttu-id="c9c80-213">Quelle que soit la version du Kit de développement logiciel (SDK) que vous utilisez, vous pouvez utiliser l’échantillonnage d’ingestion (sur notre serveur).</span><span class="sxs-lookup"><span data-stu-id="c9c80-213">No matter what SDK version you use, you can use ingestion sampling (at our server).</span></span>

<span data-ttu-id="c9c80-214">L’échantillonnage n’est pas utile pour la plupart des applications de taille petite à moyenne.</span><span class="sxs-lookup"><span data-stu-id="c9c80-214">You don’t need sampling for most small and medium size applications.</span></span> <span data-ttu-id="c9c80-215">Pour obtenir les informations de diagnostic les plus utiles et les statistiques les plus précises, le mieux est de collecter les données sur toutes vos activités utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c9c80-215">The most useful diagnostic information and most accurate statistics are obtained by collecting data on all your user activities.</span></span> 

<span data-ttu-id="c9c80-216">Les principaux avantages de l’échantillonnage sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="c9c80-216">The main advantages of sampling are:</span></span>

* <span data-ttu-id="c9c80-217">Si le service Application Insights supprime (« limite ») des points de données lorsque votre application envoie un taux de télémétrie très élevé dans un court laps de temps.</span><span class="sxs-lookup"><span data-stu-id="c9c80-217">Application Insights service drops ("throttles") data points when your app sends a very high rate of telemetry in short time interval.</span></span> 
* <span data-ttu-id="c9c80-218">Pour respecter le [quota](app-insights-pricing.md) de points de données pour votre niveau tarifaire.</span><span class="sxs-lookup"><span data-stu-id="c9c80-218">To keep within the [quota](app-insights-pricing.md) of data points for your pricing tier.</span></span> 
* <span data-ttu-id="c9c80-219">Pour réduire le trafic réseau généré par la collecte de données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="c9c80-219">To reduce network traffic from the collection of telemetry.</span></span> 

### <a name="which-type-of-sampling-should-i-use"></a><span data-ttu-id="c9c80-220">Quel type d’échantillonnage dois-je utiliser ?</span><span class="sxs-lookup"><span data-stu-id="c9c80-220">Which type of sampling should I use?</span></span>
<span data-ttu-id="c9c80-221">**Utiliser l’échantillonnage d’ingestion dans les situations suivantes :**</span><span class="sxs-lookup"><span data-stu-id="c9c80-221">**Use ingestion sampling if:**</span></span>

* <span data-ttu-id="c9c80-222">Vous dépassez souvent votre quota mensuel de données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="c9c80-222">You often go through your monthly quota of telemetry.</span></span>
* <span data-ttu-id="c9c80-223">Vous utilisez une version du Kit de développement logiciel (SDK) qui ne prend pas en charge l’échantillonnage, telle que les versions Java ou ASP.NET antérieures à la version 2.</span><span class="sxs-lookup"><span data-stu-id="c9c80-223">You're using a version of the SDK that doesn't support sampling - for example, the Java SDK or ASP.NET versions earlier than 2.</span></span>
* <span data-ttu-id="c9c80-224">Vous obtenez un volume élevé de données de télémétrie des navigateurs web de vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="c9c80-224">You're getting a lot of telemetry from your users' web browsers.</span></span>

<span data-ttu-id="c9c80-225">**Utilisez l’échantillonnage à débit fixe si :**</span><span class="sxs-lookup"><span data-stu-id="c9c80-225">**Use fixed-rate sampling if:**</span></span>

* <span data-ttu-id="c9c80-226">Vous utilisez la version 2.0.0 ou ultérieure du Kit de développement logiciel (SDK) Application Insights pour les services web ASP.NET, et</span><span class="sxs-lookup"><span data-stu-id="c9c80-226">You're using the Application Insights SDK for ASP.NET web services version 2.0.0 or later, and</span></span>
* <span data-ttu-id="c9c80-227">Vous voulez disposer d’un échantillonnage synchronisé entre le client et le serveur afin de pouvoir naviguer entre les événements connexes sur le client et le serveur (tels que les affichages de pages et les requêtes http) lorsque vous étudiez des événements dans [Search](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="c9c80-227">You want synchronized sampling between client and server, so that, when you're investigating events in [Search](app-insights-diagnostic-search.md), you can navigate between related events on the client and server, such as page views and http requests.</span></span>
* <span data-ttu-id="c9c80-228">Vous êtes sûr du pourcentage d’échantillonnage approprié pour votre application.</span><span class="sxs-lookup"><span data-stu-id="c9c80-228">You are confident of the appropriate sampling percentage for your app.</span></span> <span data-ttu-id="c9c80-229">Il doit être suffisamment élevé pour obtenir des mesures précises, mais inférieur au pourcentage engendrant le dépassement de votre quota de tarification et des limites de limitation.</span><span class="sxs-lookup"><span data-stu-id="c9c80-229">It should be high enough to get accurate metrics, but below the rate that exceeds your pricing quota and the throttling limits.</span></span> 

<span data-ttu-id="c9c80-230">**Utilisez l’échantillonnage adaptatif :**</span><span class="sxs-lookup"><span data-stu-id="c9c80-230">**Use adaptive sampling:**</span></span>

<span data-ttu-id="c9c80-231">Dans le cas contraire, nous vous recommandons d’utiliser l’échantillonnage adaptatif.</span><span class="sxs-lookup"><span data-stu-id="c9c80-231">Otherwise, we recommend adaptive sampling.</span></span> <span data-ttu-id="c9c80-232">Cette option est activée par défaut dans le Kit de développement logiciel (SDK) du serveur ASP.NET, version 2.0.0-beta3 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="c9c80-232">This is enabled by default in the ASP.NET server SDK, version 2.0.0-beta3 or later.</span></span> <span data-ttu-id="c9c80-233">Comme il ne réduit pas le trafic jusqu’à un certain débit minimum, il n’affecte pas un site peu utilisé.</span><span class="sxs-lookup"><span data-stu-id="c9c80-233">It doesn't reduce traffic until a certain minimum rate, so it won't affect a low-use site.</span></span>

## <a name="how-do-i-know-whether-sampling-is-in-operation"></a><span data-ttu-id="c9c80-234">Comment savoir si l’échantillonnage est utilisé ?</span><span class="sxs-lookup"><span data-stu-id="c9c80-234">How do I know whether sampling is in operation?</span></span>
<span data-ttu-id="c9c80-235">Pour découvrir le taux d’échantillonnage réel, indépendamment de l’endroit où il a été appliqué, utilisez une [requête Analytics](app-insights-analytics.md) telle que celle-ci :</span><span class="sxs-lookup"><span data-stu-id="c9c80-235">To discover the actual sampling rate no matter where it has been applied, use an [Analytics query](app-insights-analytics.md) such as this:</span></span>

    requests | where timestamp > ago(1d)
    | summarize 100/avg(itemCount) by bin(timestamp, 1h) 
    | render areachart 

<span data-ttu-id="c9c80-236">Pour chaque enregistrement conservé, `itemCount` indique le nombre d’enregistrements d’origine qu’il représente, soit 1 + le nombre d’enregistrements précédents ignorés.</span><span class="sxs-lookup"><span data-stu-id="c9c80-236">In each retained record, `itemCount` indicates the number of original records that it represents, equal to 1 + the number of previous discarded records.</span></span> 

## <a name="how-does-sampling-work"></a><span data-ttu-id="c9c80-237">Comment fonctionne l’échantillonnage ?</span><span class="sxs-lookup"><span data-stu-id="c9c80-237">How does sampling work?</span></span>
<span data-ttu-id="c9c80-238">L’échantillonnage à taux fixe et l’échantillonnage adaptatif sont des fonctionnalités du Kit de développement logiciel (SDK) dans ASP.NET version 2.0.0 et versions supérieures.</span><span class="sxs-lookup"><span data-stu-id="c9c80-238">Fixed-rate and adaptive sampling are a feature of the SDK in ASP.NET versions from 2.0.0 onwards.</span></span> <span data-ttu-id="c9c80-239">L’échantillonnage d’ingestion est une fonctionnalité du service Application Insights et peut fonctionner si le Kit de développement logiciel (SDK) n’effectue pas d’échantillonnage.</span><span class="sxs-lookup"><span data-stu-id="c9c80-239">Ingestion sampling is a feature of the Application Insights service, and can be in operation if the SDK is not performing sampling.</span></span> 

<span data-ttu-id="c9c80-240">L’algorithme d’échantillonnage sélectionne les éléments de télémétrie à supprimer et ceux à conserver (qu’ils se trouvent dans le Kit de développement logiciel ou le service Application Insights).</span><span class="sxs-lookup"><span data-stu-id="c9c80-240">The sampling algorithm decides which telemetry items to drop, and which ones to keep (whether it's in the SDK or in the Application Insights service).</span></span> <span data-ttu-id="c9c80-241">La décision d’échantillonnage est fondée sur plusieurs règles visant à préserver l’intégrité de tous les points de données reliés entre eux, en conservant dans Application Insights une expérience de diagnostic qui demeure exploitable et fiable, même avec un jeu de données réduit.</span><span class="sxs-lookup"><span data-stu-id="c9c80-241">The sampling decision is based on several rules that aim to preserve all interrelated data points intact, maintaining a diagnostic experience in Application Insights that is actionable and reliable even with a reduced data set.</span></span> <span data-ttu-id="c9c80-242">En cas d’échec d’une requête, par exemple, si votre application envoie d’autres éléments de télémétrie (tels que les exceptions et les traces enregistrées à partir de cette requête), l’échantillonnage ne fractionnera ni cette requête ni les autres éléments de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="c9c80-242">For example, if for a failed request your app sends additional telemetry items (such as exception and traces logged from this request), sampling will not split this request and other telemetry.</span></span> <span data-ttu-id="c9c80-243">Il les conservera ou supprimera ensemble.</span><span class="sxs-lookup"><span data-stu-id="c9c80-243">It either keeps or drops them all together.</span></span> <span data-ttu-id="c9c80-244">C’est pourquoi, lorsque vous examinez les détails de la requête dans Application Insights, la requête s’affichera toujours avec les éléments de télémétrie qui lui sont associés.</span><span class="sxs-lookup"><span data-stu-id="c9c80-244">As a result, when you look at the request details in Application Insights, you can always see the request along with its associated telemetry items.</span></span> 

<span data-ttu-id="c9c80-245">Pour les applications qui définissent « l’utilisateur » (autrement dit, les applications Web les plus courantes), la décision d’échantillonnage est basée sur le hachage de l’identifiant utilisateur, ce qui signifie que tous les éléments de télémétrie associés à n’importe quel utilisateur spécifique seront soit conservés soit supprimés.</span><span class="sxs-lookup"><span data-stu-id="c9c80-245">For applications that define "user" (that is, most typical web applications), the sampling decision is based on the hash of the user id, which means that all telemetry for any particular user is either preserved or dropped.</span></span> <span data-ttu-id="c9c80-246">Pour les types d’applications qui ne définissent pas les utilisateurs (tels que les services Web), la décision d’échantillonnage repose sur l’identifiant d’opération de la requête.</span><span class="sxs-lookup"><span data-stu-id="c9c80-246">For the types of applications that don't define users (such as web services) the sampling decision is based on the operation id of the request.</span></span> <span data-ttu-id="c9c80-247">Enfin, pour les éléments de télémétrie qui ne sont associés ni à un identifiant utilisateur ni à un identifiant d’opération (par exemple, pour des éléments de télémétrie signalés à partir de threads asynchrones sans contexte http), l’échantillonnage capturera simplement un pourcentage d’éléments de télémétrie de chaque type.</span><span class="sxs-lookup"><span data-stu-id="c9c80-247">Finally, for the telemetry items that neither have user nor operation id set (for example telemetry items reported from asynchronous threads with no http context) sampling simply captures a percentage of telemetry items of each type.</span></span> 

<span data-ttu-id="c9c80-248">Lorsque les données de télémétrie vous sont restituées, le service Application Insights ajuste les mesures en fonction du même pourcentage d’échantillonnage que celui utilisé au moment de la collecte, de manière à compenser les points de données manquants.</span><span class="sxs-lookup"><span data-stu-id="c9c80-248">When presenting telemetry back to you, the Application Insights service adjusts the metrics by the same sampling percentage that was used at the time of collection, to compensate for the missing data points.</span></span> <span data-ttu-id="c9c80-249">Par conséquent, lorsqu’ils consultent les données de télémétrie dans Application Insights, les utilisateurs constatent des approximations correctes d’un point de vue statistique et très proches des chiffres réels.</span><span class="sxs-lookup"><span data-stu-id="c9c80-249">Hence, when looking at the telemetry in Application Insights, the users are seeing statistically correct approximations that are very close to the real numbers.</span></span>

<span data-ttu-id="c9c80-250">La précision de l’approximation dépend en grande partie du pourcentage d’échantillonnage configuré.</span><span class="sxs-lookup"><span data-stu-id="c9c80-250">The accuracy of the approximation largely depends on the configured sampling percentage.</span></span> <span data-ttu-id="c9c80-251">Elle est également plus précise pour les applications qui gèrent un grand nombre de requêtes globalement similaires générées par un grand nombre d’utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="c9c80-251">Also, the accuracy increases for applications that handle a large volume of generally similar requests from lots of users.</span></span> <span data-ttu-id="c9c80-252">En revanche, pour les applications qui ne sont pas soumises à une charge importante, l’échantillonnage n’est pas nécessaire, car ces applications peuvent généralement envoyer toutes leurs données de télémétrie sans dépasser leur quota ni entraîner de perte de données liée à une limitation de la bande passante.</span><span class="sxs-lookup"><span data-stu-id="c9c80-252">On the other hand, for applications that don't work with a significant load, sampling is not needed as these applications can usually send all their telemetry while staying within the quota, without causing data loss from throttling.</span></span> 

<span data-ttu-id="c9c80-253">Notez qu’Application Insights n’échantillonne pas les données de télémétrie de type Mesures et Sessions, car il est préférable de disposer d’une bonne précision pour ces types de données.</span><span class="sxs-lookup"><span data-stu-id="c9c80-253">Note that Application Insights does not sample Metrics and Sessions telemetry types, since for these types, reduction in the precision can be highly undesirable.</span></span> 

### <a name="adaptive-sampling"></a><span data-ttu-id="c9c80-254">échantillonnage adaptatif</span><span class="sxs-lookup"><span data-stu-id="c9c80-254">Adaptive sampling</span></span>
<span data-ttu-id="c9c80-255">L’échantillonnage adaptatif ajoute un composant qui contrôle la vitesse de transmission actuelle à partir du Kit de développement logiciel (SDK) et ajuste le pourcentage d’échantillonnage afin de le maintenir en dessous du taux maximal cible.</span><span class="sxs-lookup"><span data-stu-id="c9c80-255">Adaptive sampling adds a component that monitors the current rate of transmission from the SDK, and adjusts the sampling percentage to try to stay within the target maximum rate.</span></span> <span data-ttu-id="c9c80-256">L’ajustement est recalculé à intervalles réguliers en fonction d’une moyenne mobile de la vitesse de transmission sortante.</span><span class="sxs-lookup"><span data-stu-id="c9c80-256">The adjustment is recalculated at regular intervals, and is based on a moving average of the outgoing transmission rate.</span></span>

## <a name="sampling-and-the-javascript-sdk"></a><span data-ttu-id="c9c80-257">Échantillonnage et kit de développement logiciel JavaScript</span><span class="sxs-lookup"><span data-stu-id="c9c80-257">Sampling and the JavaScript SDK</span></span>
<span data-ttu-id="c9c80-258">Le kit de développement logiciel (SDK) côté client (JavaScript) participe à l’échantillonnage à taux fixe parallèlement au kit de développement logiciel (SDK) côté serveur.</span><span class="sxs-lookup"><span data-stu-id="c9c80-258">The client-side (JavaScript) SDK participates in fixed-rate sampling in conjunction with the server-side SDK.</span></span> <span data-ttu-id="c9c80-259">Les pages instrumentées envoient uniquement les données de télémétrie côté client provenant des utilisateurs que le SDK côté serveur a décidé d’échantillonner.</span><span class="sxs-lookup"><span data-stu-id="c9c80-259">The instrumented pages will only send client-side telemetry from the same users for which the server-side made its decision to "sample in."</span></span> <span data-ttu-id="c9c80-260">Cette logique est conçue pour préserver l’intégrité de la session utilisateur côté client et côté serveur.</span><span class="sxs-lookup"><span data-stu-id="c9c80-260">This logic is designed to maintain integrity of user session across client- and server-sides.</span></span> <span data-ttu-id="c9c80-261">En partant de n’importe quel élément de télémétrie dans Application Insights, vous retrouverez donc tous les autres éléments de télémétrie associés à l’utilisateur ou à la session en question.</span><span class="sxs-lookup"><span data-stu-id="c9c80-261">As a result, from any particular telemetry item in Application Insights you can find all other telemetry items for this user or session.</span></span> 

<span data-ttu-id="c9c80-262">*Mes données de télémétrie côté client et côté serveur n’affichent pas les échantillons coordonnés que vous décrivez ci-dessus.*</span><span class="sxs-lookup"><span data-stu-id="c9c80-262">*My client and server-side telemetry don't show coordinated samples as you describe above.*</span></span>

* <span data-ttu-id="c9c80-263">Vérifiez que vous avez activé l’échantillonnage à débit fixe à la fois sur le serveur et sur le client.</span><span class="sxs-lookup"><span data-stu-id="c9c80-263">Verify that you enabled fixed-rate sampling both on server and client.</span></span>
* <span data-ttu-id="c9c80-264">Assurez-vous que vous utilisez bien le kit de développement logiciel version 2.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="c9c80-264">Make sure that the SDK version is 2.0 or above.</span></span>
* <span data-ttu-id="c9c80-265">Vérifiez que vous définissez le même pourcentage d’échantillonnage dans le client et dans le serveur.</span><span class="sxs-lookup"><span data-stu-id="c9c80-265">Check that you set the same sampling percentage in both the client and server.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="c9c80-266">Forum Aux Questions (FAQ)</span><span class="sxs-lookup"><span data-stu-id="c9c80-266">Frequently Asked Questions</span></span>
<span data-ttu-id="c9c80-267">*Pourquoi l’échantillonnage ne permet-il pas simplement de « collecter X % de chaque type de télémétrie » ?*</span><span class="sxs-lookup"><span data-stu-id="c9c80-267">*Why isn't sampling a simple "collect X percent of each telemetry type"?*</span></span>

* <span data-ttu-id="c9c80-268">Bien que cette approche de l’échantillonnage puisse générer des approximations métriques d’une très haute précision, elle ne permettrait pas de mettre en corrélation les données de diagnostic par utilisateur, par session et par requête, ce qui est essentiel pour l’établissement de diagnostics.</span><span class="sxs-lookup"><span data-stu-id="c9c80-268">While this sampling approach would provide with a very high precision in metric approximations, it would break ability to correlate diagnostic data per user, session, and request, which is critical for diagnostics.</span></span> <span data-ttu-id="c9c80-269">L’échantillonnage est donc plus efficace lorsqu’il revient à « collecter tous les éléments de télémétrie pour X % des utilisateurs de l’application » ou à « collecter tous les éléments de télémétrie pour X % des requêtes de l’application ».</span><span class="sxs-lookup"><span data-stu-id="c9c80-269">Therefore, sampling works better with "collect all telemetry items for X percent of app users", or "collect all telemetry for X percent of app requests" logic.</span></span> <span data-ttu-id="c9c80-270">Pour les éléments de télémétrie qui ne sont pas associés aux requêtes (dans le cas, par exemple, d’un traitement asynchrone en arrière-plan), la solution consiste à « collecter X % de tous les éléments de chaque type de télémétrie ».</span><span class="sxs-lookup"><span data-stu-id="c9c80-270">For the telemetry items not associated with the requests (such as background asynchronous processing), the fall back is to "collect X percent of all items for each telemetry type."</span></span> 

<span data-ttu-id="c9c80-271">*Le pourcentage d’échantillonnage peut-il évoluer au fil du temps ?*</span><span class="sxs-lookup"><span data-stu-id="c9c80-271">*Can the sampling percentage change over time?*</span></span>

* <span data-ttu-id="c9c80-272">Oui, l’échantillonnage adaptatif modifie progressivement le pourcentage d’échantillonnage en fonction du volume de données de télémétrie constaté.</span><span class="sxs-lookup"><span data-stu-id="c9c80-272">Yes, adaptive sampling gradually changes the sampling percentage, based on the currently observed volume of the telemetry.</span></span>

<span data-ttu-id="c9c80-273">*Si j’utilise l’échantillonnage à débit fixe, comment déterminer le pourcentage d’échantillonnage optimal pour mon application ?*</span><span class="sxs-lookup"><span data-stu-id="c9c80-273">*If I use fixed-rate sampling, how do I know which sampling percentage will work the best for my app?*</span></span>

* <span data-ttu-id="c9c80-274">Pour cela, vous pouvez commencer par l’échantillonnage adaptatif, identifier le taux obtenu (voir la question précédente) et passer à l’échantillonnage à taux fixe en utilisant ce taux.</span><span class="sxs-lookup"><span data-stu-id="c9c80-274">One way is to start with adaptive sampling, find out what rate it settles on (see the above question), and then switch to fixed-rate sampling using that rate.</span></span> 
  
    <span data-ttu-id="c9c80-275">Autrement, vous devez procéder par tâtonnements.</span><span class="sxs-lookup"><span data-stu-id="c9c80-275">Otherwise, you have to guess.</span></span> <span data-ttu-id="c9c80-276">Analysez votre utilisation actuelle des données de télémétrie dans AI, observez les limitations qui s’appliquent, puis estimez le volume de données de télémétrie collectées.</span><span class="sxs-lookup"><span data-stu-id="c9c80-276">Analyze your current telemetry usage in AI, observe any throttling that is occurring, and estimate the volume of the collected telemetry.</span></span> <span data-ttu-id="c9c80-277">Ces trois entrées, combinées au niveau tarifaire sélectionné, vous indiquent dans quelle mesure vous devrez réduire le volume de données de télémétrie collectées.</span><span class="sxs-lookup"><span data-stu-id="c9c80-277">These three inputs, together with your selected pricing tier, suggest how much you might want to reduce the volume of the collected telemetry.</span></span> <span data-ttu-id="c9c80-278">Toutefois, une augmentation du nombre d’utilisateurs ou toute autre modification au niveau du volume des données de télémétrie peut invalider votre estimation.</span><span class="sxs-lookup"><span data-stu-id="c9c80-278">However, an increase in the number of your users or some other shift in the volume of telemetry might invalidate your estimate.</span></span>

<span data-ttu-id="c9c80-279">*Que se passe-t-il si je configure le pourcentage d’échantillonnage à un niveau trop faible ?*</span><span class="sxs-lookup"><span data-stu-id="c9c80-279">*What happens if I configure sampling percentage too low?*</span></span>

* <span data-ttu-id="c9c80-280">Un pourcentage d’échantillonnage excessivement faible (échantillonnage trop agressif) a pour effet de réduire la précision des approximations lorsqu’Application Insights tente de compenser la visualisation des données pour tenir compte de la réduction du volume de données.</span><span class="sxs-lookup"><span data-stu-id="c9c80-280">Excessively low sampling percentage (over-aggressive sampling) reduces the accuracy of the approximations, when Application Insights attempts to compensate the visualization of the data for the data volume reduction.</span></span> <span data-ttu-id="c9c80-281">Il peut également affecter l’expérience de diagnostic puisque l’échantillonnage peut inclure certaines requêtes rarement sujettes à des problèmes d’échec ou de ralentissement.</span><span class="sxs-lookup"><span data-stu-id="c9c80-281">Also, diagnostic experience might be negatively impacted, as some of the infrequently failing or slow requests may be sampled out.</span></span>

<span data-ttu-id="c9c80-282">*Que se passe-t-il si je configure un pourcentage d’échantillonnage trop élevé ?*</span><span class="sxs-lookup"><span data-stu-id="c9c80-282">*What happens if I configure sampling percentage too high?*</span></span>

* <span data-ttu-id="c9c80-283">Si vous configurez un pourcentage d’échantillonnage trop élevé (c’est-à-dire pas assez agressif), le volume de données de télémétrie collectées n’est pas suffisamment réduit.</span><span class="sxs-lookup"><span data-stu-id="c9c80-283">Configuring too high sampling percentage (not aggressive enough) results in an insufficient reduction in the volume of the collected telemetry.</span></span> <span data-ttu-id="c9c80-284">Vous risquez de perdre des données de télémétrie sous l’effet de la limitation de bande passante et de supporter des coûts plus élevés que prévu pour l’utilisation d’Application Insights en raison des frais de dépassement.</span><span class="sxs-lookup"><span data-stu-id="c9c80-284">You may still experience telemetry data loss related to throttling, and the cost of using Application Insights might be higher than you planned due to overage charges.</span></span>

<span data-ttu-id="c9c80-285">*Sur quelles plates-formes puis-je utiliser l’échantillonnage ?*</span><span class="sxs-lookup"><span data-stu-id="c9c80-285">*On what platforms can I use sampling?*</span></span>

* <span data-ttu-id="c9c80-286">L’échantillonnage d’ingestion peut se produire automatiquement pour toute télémétrie au-dessus d’un certain volume, si le Kit de développement logiciel (SDK)n’effectue pas d’échantillonnage.</span><span class="sxs-lookup"><span data-stu-id="c9c80-286">Ingestion sampling can occur automatically for any telemetry above a certain volume, if the SDK is not performing sampling.</span></span> <span data-ttu-id="c9c80-287">Cela peut être le cas si, par exemple, votre application utilise un serveur Java ou si vous utilisez une version antérieure du Kit de développement logiciel (SDK) ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="c9c80-287">This would work, for example, if your app uses a Java server, or if you are using an older version of the ASP.NET SDK.</span></span>
* <span data-ttu-id="c9c80-288">Si vous utilisez le Kit de développement logiciel (SDK) ASP.NET version 2.0.0 ou une version ultérieure (hébergée dans Azure ou sur votre propre serveur), vous obtenez l’échantillonnage adaptatif par défaut, mais vous pouvez basculer à l’échantillonnage à taux fixe, comme décrit ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="c9c80-288">If you're using ASP.NET SDK versions 2.0.0 and above (hosted either in Azure or on your own server), you get adaptive sampling by default, but you can switch to fixed-rate as described above.</span></span> <span data-ttu-id="c9c80-289">Avec l’échantillonnage à taux fixe, le Kit de développement logiciel (SDK) du navigateur se synchronise automatiquement pour échantillonner les événements connexes.</span><span class="sxs-lookup"><span data-stu-id="c9c80-289">With fixed-rate sampling, the browser SDK automatically synchronizes to sample related events.</span></span> 

<span data-ttu-id="c9c80-290">*Je souhaite que certains événements rares soient toujours affichés. Comment faire en sorte qu’ils soient disponibles hors du module d’échantillonnage ?*</span><span class="sxs-lookup"><span data-stu-id="c9c80-290">*There are certain rare events I always want to see. How can I get them past the sampling module?*</span></span>

* <span data-ttu-id="c9c80-291">Initialisez une instance distincte de TelemetryClient avec une nouvelle instance TelemetryConfiguration (et non la valeur Active par défaut).</span><span class="sxs-lookup"><span data-stu-id="c9c80-291">Initialize a separate instance of TelemetryClient with a new TelemetryConfiguration (not the default Active one).</span></span> <span data-ttu-id="c9c80-292">Utilisez cette instance pour envoyer vos événements rares.</span><span class="sxs-lookup"><span data-stu-id="c9c80-292">Use that to send your rare events.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c9c80-293">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c9c80-293">Next steps</span></span>
* <span data-ttu-id="c9c80-294">[filtrage](app-insights-api-filtering-sampling.md) peut fournir un contrôle plus strict de ce que le Kit de développement logiciel (SDK) envoie.</span><span class="sxs-lookup"><span data-stu-id="c9c80-294">[Filtering](app-insights-api-filtering-sampling.md) can provide more strict control of what your SDK sends.</span></span>

