---
title: "échantillonnage aaaTelemetry dans Azure Application Insights | Documents Microsoft"
description: "Comment tookeep hello volume de données de télémétrie sous contrôle de code."
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
ms.openlocfilehash: e19c350d0a5f16736c100322a9922fcfbf5d7b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sampling-in-application-insights"></a><span data-ttu-id="cfe74-103">Échantillonnage dans Application Insights</span><span class="sxs-lookup"><span data-stu-id="cfe74-103">Sampling in Application Insights</span></span>


<span data-ttu-id="cfe74-104">L’échantillonnage est une fonctionnalité dans [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cfe74-104">Sampling is a feature in [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="cfe74-105">Il est recommandé de hello le trafic de façon tooreduce télémétrie et le stockage, tout en conservant une analyse statistique correcte des données d’application.</span><span class="sxs-lookup"><span data-stu-id="cfe74-105">It is hello recommended way tooreduce telemetry traffic and storage, while preserving  a statistically correct analysis of application data.</span></span> <span data-ttu-id="cfe74-106">filtre de Hello sélectionne les éléments associés, afin que vous pouvez naviguer entre des éléments lorsque vous effectuez des investigations en matière de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="cfe74-106">hello filter selects items that are related, so that you can navigate between items when you are doing diagnostic investigations.</span></span>
<span data-ttu-id="cfe74-107">Lorsque les nombres de métriques sont présentés tooyou dans le portail de hello, ils sont renormalisés compte tootake Hello d’échantillonnage, toominimize un effet sur les statistiques de hello.</span><span class="sxs-lookup"><span data-stu-id="cfe74-107">When metric counts are presented tooyou in hello portal, they are renormalized tootake account of hello sampling, toominimize any effect on hello statistics.</span></span>

<span data-ttu-id="cfe74-108">L’échantillonnage réduit les coûts du trafic et des données, et vous aide à éviter les limitations.</span><span class="sxs-lookup"><span data-stu-id="cfe74-108">Sampling reduces traffic and data costs, and helps you avoid throttling.</span></span>

## <a name="in-brief"></a><span data-ttu-id="cfe74-109">En bref :</span><span class="sxs-lookup"><span data-stu-id="cfe74-109">In brief:</span></span>
* <span data-ttu-id="cfe74-110">Échantillonnage conserve 1 dans  *n*  enregistre et ignore le reste de hello.</span><span class="sxs-lookup"><span data-stu-id="cfe74-110">Sampling retains 1 in *n* records and discards hello rest.</span></span> <span data-ttu-id="cfe74-111">Par exemple, il peut conserver 1 événement sur 5, soit un taux d’échantillonnage de 20 %.</span><span class="sxs-lookup"><span data-stu-id="cfe74-111">For example, it might retain 1 in 5 events, a sampling rate of 20%.</span></span> 
* <span data-ttu-id="cfe74-112">L’échantillonnage s’effectue automatiquement si votre application envoie de nombreuses données de télémétrie, dans les applications de serveur web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="cfe74-112">Sampling happens automatically if your application sends a lot of telemetry, in ASP.NET web server apps.</span></span>
* <span data-ttu-id="cfe74-113">Vous pouvez également définir d’échantillonnage manuellement, soit en hello portail sur hello tarification page ; ou dans le Kit de développement ASP.NET dans le fichier .config de hello de hello, tooalso réduire le trafic réseau de hello.</span><span class="sxs-lookup"><span data-stu-id="cfe74-113">You can also set sampling manually, either in hello portal on hello pricing page; or in hello ASP.NET SDK in hello .config file, tooalso reduce hello network traffic.</span></span>
* <span data-ttu-id="cfe74-114">Si vous consignez des événements personnalisés et que vous souhaitez toomake sûr qu’un jeu d’événements est conservé ou ignoré ensemble, assurez-vous qu’ils ont hello même valeur OperationId.</span><span class="sxs-lookup"><span data-stu-id="cfe74-114">If you log custom events and you want toomake sure that a set of events is either retained or discarded together, make sure that they have hello same OperationId value.</span></span>
* <span data-ttu-id="cfe74-115">diviseur d’échantillonnage de Hello  *n*  est signalée dans chaque enregistrement de la propriété de hello `itemCount`, qui, dans la recherche s’affiche sous hello nom convivial « nombre de demande » ou « nombre d’événements ».</span><span class="sxs-lookup"><span data-stu-id="cfe74-115">hello sampling divisor *n* is reported in each record in hello property `itemCount`, which in Search appears under hello friendly name "request count" or "event count".</span></span> <span data-ttu-id="cfe74-116">Lorsque l’échantillonnage n’est pas en cours d’utilisation, `itemCount==1`.</span><span class="sxs-lookup"><span data-stu-id="cfe74-116">When sampling is not in operation, `itemCount==1`.</span></span>
* <span data-ttu-id="cfe74-117">Si vous écrivez des requêtes Analytics, vous devez [tenir compte de l’échantillonnage](app-insights-analytics-tour.md#counting-sampled-data).</span><span class="sxs-lookup"><span data-stu-id="cfe74-117">If you write Analytics queries, you should [take account of sampling](app-insights-analytics-tour.md#counting-sampled-data).</span></span> <span data-ttu-id="cfe74-118">En particulier, au lieu de compter simplement les enregistrements, vous devez utiliser `summarize sum(itemCount)`.</span><span class="sxs-lookup"><span data-stu-id="cfe74-118">In particular, instead of simply counting records, you should use `summarize sum(itemCount)`.</span></span>

## <a name="types-of-sampling"></a><span data-ttu-id="cfe74-119">Types d’échantillonnage</span><span class="sxs-lookup"><span data-stu-id="cfe74-119">Types of sampling</span></span>
<span data-ttu-id="cfe74-120">Il existe trois autres méthodes d’échantillonnage :</span><span class="sxs-lookup"><span data-stu-id="cfe74-120">There are three alternative sampling methods:</span></span>

* <span data-ttu-id="cfe74-121">**Échantillonnage Adaptive** ajuste automatiquement le volume hello de télémétrie envoyé à partir du Kit de développement logiciel de hello dans votre application ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="cfe74-121">**Adaptive sampling** automatically adjusts hello volume of telemetry sent from hello SDK in your ASP.NET app.</span></span> <span data-ttu-id="cfe74-122">Il s’agit du comportement par défaut depuis la version 2.0.0-beta3 du Kit de développement logiciel (SDK).</span><span class="sxs-lookup"><span data-stu-id="cfe74-122">Default from SDK v 2.0.0-beta3.</span></span> <span data-ttu-id="cfe74-123">Actuellement uniquement disponible pour la télémétrie ASP.NET côté serveur.</span><span class="sxs-lookup"><span data-stu-id="cfe74-123">Currently available for ASP.NET server-side telemetry only.</span></span> 
* <span data-ttu-id="cfe74-124">**Échantillonnage de taux fixe** réduit le volume de hello de télémétrie envoyé depuis votre serveur ASP.NET ou à partir de navigateurs de vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="cfe74-124">**Fixed-rate sampling** reduces hello volume of telemetry sent from both your ASP.NET server and from your users' browsers.</span></span> <span data-ttu-id="cfe74-125">Vous définissez des taux de hello.</span><span class="sxs-lookup"><span data-stu-id="cfe74-125">You set hello rate.</span></span> <span data-ttu-id="cfe74-126">Hello client et serveur synchronisera les échantillonnages donc, de recherche, vous pouvez naviguer entre les vues de page associée et des demandes.</span><span class="sxs-lookup"><span data-stu-id="cfe74-126">hello client and server will synchronize their sampling so that, in Search, you can navigate between related page views and requests.</span></span>
* <span data-ttu-id="cfe74-127">**Échantillonnage de l’ingestion** fonctionne Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="cfe74-127">**Ingestion sampling** works in hello Azure portal.</span></span> <span data-ttu-id="cfe74-128">Il ignore certaines des données de télémétrie hello qui arrive à partir de votre application, à une fréquence que vous définissez.</span><span class="sxs-lookup"><span data-stu-id="cfe74-128">It discards some of hello telemetry that arrives from your app, at a rate that you set.</span></span> <span data-ttu-id="cfe74-129">Le trafic des données de télémétrie n’est pas réduit, mais cela vous permet de respecter votre quota mensuel.</span><span class="sxs-lookup"><span data-stu-id="cfe74-129">It doesn't reduce telemetry traffic, but helps you keep within your monthly quota.</span></span> <span data-ttu-id="cfe74-130">Hello présente l’avantage d’échantillonnage d’ingestion est que vous pouvez le définir sans redéployer votre application et uniformément fonctionne pour tous les clients et serveurs.</span><span class="sxs-lookup"><span data-stu-id="cfe74-130">hello big advantage of ingestion sampling is that you can set it without redeploying your app, and it works uniformly for all servers and clients.</span></span> 

<span data-ttu-id="cfe74-131">Si un échantillonnage de débit adaptatif ou fixe est en cours d’utilisation, l’échantillonnage d’ingestion est désactivé.</span><span class="sxs-lookup"><span data-stu-id="cfe74-131">If Adaptive or Fixed rate sampling are in operation, Ingestion sampling is disabled.</span></span>

## <a name="ingestion-sampling"></a><span data-ttu-id="cfe74-132">échantillonnage d’ingestion</span><span class="sxs-lookup"><span data-stu-id="cfe74-132">Ingestion sampling</span></span>
<span data-ttu-id="cfe74-133">Cette forme d’échantillonnage fonctionne au point hello où télémétrie hello à partir de votre serveur web, les navigateurs et périphériques atteint le point de terminaison de service hello Application Insights.</span><span class="sxs-lookup"><span data-stu-id="cfe74-133">This form of sampling operates at hello point where hello telemetry from your web server, browsers, and devices reaches hello Application Insights service endpoint.</span></span> <span data-ttu-id="cfe74-134">Bien qu’elle ne réduit pas le trafic de télémétrie de hello envoyé à partir de votre application, elle réduit hello traitées et conservées (et facturé pour) par Application Insights.</span><span class="sxs-lookup"><span data-stu-id="cfe74-134">Although it doesn't reduce hello telemetry traffic sent from your app, it does reduce hello amount processed and retained (and charged for) by Application Insights.</span></span>

<span data-ttu-id="cfe74-135">Utilisez ce type d’échantillonnage si votre application dépasse souvent son quota mensuel et que vous ne pouvez hello à l’aide d’un des types de basée sur le Kit de développement logiciel hello d’échantillonnage.</span><span class="sxs-lookup"><span data-stu-id="cfe74-135">Use this type of sampling if your app often goes over its monthly quota and you don't have hello option of using either of hello SDK-based types of sampling.</span></span> 

<span data-ttu-id="cfe74-136">Définir le taux d’échantillonnage de hello Bonjour Quotas et panneau de tarification :</span><span class="sxs-lookup"><span data-stu-id="cfe74-136">Set hello sampling rate in hello Quotas and Pricing blade:</span></span>

![À partir du Panneau de vue d’ensemble d’applications de hello, cliquez sur paramètres, des quotas, des échantillons, puis un taux d’échantillonnage et cliquez sur la mise à jour.](./media/app-insights-sampling/04.png)

<span data-ttu-id="cfe74-138">Comme d’autres types d’échantillonnage, algorithme de hello conserve les éléments de télémétrie connexes.</span><span class="sxs-lookup"><span data-stu-id="cfe74-138">Like other types of sampling, hello algorithm retains related telemetry items.</span></span> <span data-ttu-id="cfe74-139">Par exemple, lorsque que vous examinez les données de télémétrie hello dans la recherche, vous serez en mesure de demande de hello toofind liés tooa des exception particulière.</span><span class="sxs-lookup"><span data-stu-id="cfe74-139">For example, when you're inspecting hello telemetry in Search, you'll be able toofind hello request related tooa particular exception.</span></span> <span data-ttu-id="cfe74-140">Les données de mesure telles que les taux de demandes et le taux d’exceptions sont correctement conservées.</span><span class="sxs-lookup"><span data-stu-id="cfe74-140">Metric counts such as request rate and exception rate are correctly retained.</span></span>

<span data-ttu-id="cfe74-141">Les points de données ignorés par l’échantillonnage ne sont disponibles dans aucune fonctionnalité Application Insights, par exemple l’ [exportation continue](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="cfe74-141">Data points that are discarded by sampling are not available in any Application Insights feature such as [Continuous Export](app-insights-export-telemetry.md).</span></span>

<span data-ttu-id="cfe74-142">L’échantillonnage d’ingestion ne fonctionne pas pendant qu’une opération d’échantillonnage adaptatif ou taux fixe basé sur un Kit de développement logiciel (SDK) est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="cfe74-142">Ingestion sampling doesn't operate while SDK-based adaptive or fixed-rate sampling is in operation.</span></span> <span data-ttu-id="cfe74-143">Si le taux d’échantillonnage hello hello SDK est inférieure à 100 %, puis hello taux d’échantillonnage de réception que vous définissez est ignoré.</span><span class="sxs-lookup"><span data-stu-id="cfe74-143">If hello sampling rate at hello SDK is less than 100%, then hello ingestion sampling rate that you set is ignored.</span></span>

> [!WARNING]
> <span data-ttu-id="cfe74-144">valeur de Hello affichée sur la vignette de hello valeur hello que vous définissez pour l’échantillonnage de l’ingestion.</span><span class="sxs-lookup"><span data-stu-id="cfe74-144">hello value shown on hello tile indicates hello value that you set for ingestion sampling.</span></span> <span data-ttu-id="cfe74-145">Il ne représente le taux d’échantillonnage réelle de hello si l’échantillonnage SDK est en opération.</span><span class="sxs-lookup"><span data-stu-id="cfe74-145">It doesn't represent hello actual sampling rate if SDK sampling is in operation.</span></span>
> 
> 

## <a name="adaptive-sampling-at-your-web-server"></a><span data-ttu-id="cfe74-146">Échantillonnage adaptatif sur votre serveur web</span><span class="sxs-lookup"><span data-stu-id="cfe74-146">Adaptive sampling at your web server</span></span>
<span data-ttu-id="cfe74-147">Échantillonnage adaptatif est disponible pour hello Application Insights SDK pour ASP.NET v 2.0.0-beta3 et versions ultérieures et est activé par défaut.</span><span class="sxs-lookup"><span data-stu-id="cfe74-147">Adaptive sampling is available for hello Application Insights SDK for ASP.NET v 2.0.0-beta3 and later, and is enabled by default.</span></span> 

<span data-ttu-id="cfe74-148">Échantillonnage Adaptive affecte volume hello de télémétrie envoyé à partir de votre toohello application du serveur web service Application Insights.</span><span class="sxs-lookup"><span data-stu-id="cfe74-148">Adaptive sampling affects hello volume of telemetry sent from your web server app toohello Application Insights service.</span></span> <span data-ttu-id="cfe74-149">Hello volume est ajusté automatiquement tookeep au sein d’un taux maximum spécifié de trafic.</span><span class="sxs-lookup"><span data-stu-id="cfe74-149">hello volume is adjusted automatically tookeep within a specified maximum rate of traffic.</span></span>

<span data-ttu-id="cfe74-150">Il ne fonctionne pas quand les volumes de données de télémétrie sont bas ; ainsi, une application en mode débogage ou un site web faiblement utilisé ne sont pas affectés.</span><span class="sxs-lookup"><span data-stu-id="cfe74-150">It doesn't operate at low volumes of telemetry, so an app in debugging or a website with low usage won't be affected.</span></span>

<span data-ttu-id="cfe74-151">volume cible tooachieve hello, certaines des données de télémétrie hello générée est ignoré.</span><span class="sxs-lookup"><span data-stu-id="cfe74-151">tooachieve hello target volume, some of hello telemetry generated is discarded.</span></span> <span data-ttu-id="cfe74-152">Mais comme les autres types d’échantillonnage, algorithme de hello conserve les éléments de télémétrie connexes.</span><span class="sxs-lookup"><span data-stu-id="cfe74-152">But like other types of sampling, hello algorithm retains related telemetry items.</span></span> <span data-ttu-id="cfe74-153">Par exemple, lorsque que vous examinez les données de télémétrie hello dans la recherche, vous serez en mesure de demande de hello toofind liés tooa des exception particulière.</span><span class="sxs-lookup"><span data-stu-id="cfe74-153">For example, when you're inspecting hello telemetry in Search, you'll be able toofind hello request related tooa particular exception.</span></span> 

<span data-ttu-id="cfe74-154">Mesure de compte, telles que les taux de demande et exception sont toocompensate ajustée pour hello taux d’échantillonnage, afin qu’elles affichent des valeurs correctes environ dans l’Explorateur de métrique.</span><span class="sxs-lookup"><span data-stu-id="cfe74-154">Metric counts such as request rate and exception rate are adjusted toocompensate for hello sampling rate, so that they show approximately correct values in Metric Explorer.</span></span>

<span data-ttu-id="cfe74-155">**Mettre à jour NuGet de votre projet** packages toohello dernière *préliminaires* version d’Application Insights : avec le bouton droit de projet hello dans l’Explorateur de solutions, cliquez sur Gérer les Packages NuGet, vérifiez **Include version préliminaire** et recherchez Microsoft.ApplicationInsights.Web.</span><span class="sxs-lookup"><span data-stu-id="cfe74-155">**Update your project's NuGet** packages toohello latest *pre-release* version of Application Insights: Right-click hello project in Solution Explorer, choose Manage NuGet Packages, check **Include prerelease** and search for Microsoft.ApplicationInsights.Web.</span></span> 

<span data-ttu-id="cfe74-156">Dans [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), vous pouvez ajuster les paramètres plusieurs Bonjour `AdaptiveSamplingTelemetryProcessor` nœud.</span><span class="sxs-lookup"><span data-stu-id="cfe74-156">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), you can adjust several parameters in hello `AdaptiveSamplingTelemetryProcessor` node.</span></span> <span data-ttu-id="cfe74-157">chiffres Hello indiqués sont les valeurs par défaut hello :</span><span class="sxs-lookup"><span data-stu-id="cfe74-157">hello figures shown are hello default values:</span></span>

* `<MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>`
  
    <span data-ttu-id="cfe74-158">Hello taux cible hello algorithme adaptatif judicieuse s’adresse aux **sur chaque hôte du serveur**.</span><span class="sxs-lookup"><span data-stu-id="cfe74-158">hello target rate that hello adaptive algorithm aims for **on each server host**.</span></span> <span data-ttu-id="cfe74-159">Si votre application web s’exécute sur plusieurs hôtes, réduisez cette valeur ainsi en tooremain au sein de votre taux de cible de trafic sur le portail d’Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="cfe74-159">If your web app runs on many hosts, reduce this value so as tooremain within your target rate of traffic at hello Application Insights portal.</span></span>
* `<EvaluationInterval>00:00:15</EvaluationInterval>` 
  
    <span data-ttu-id="cfe74-160">intervalle de salutation à quels hello taux actuel de télémétrie est réévaluée.</span><span class="sxs-lookup"><span data-stu-id="cfe74-160">hello interval at which hello current rate of telemetry is re-evaluated.</span></span> <span data-ttu-id="cfe74-161">L’évaluation est effectuée sous forme de moyenne mobile.</span><span class="sxs-lookup"><span data-stu-id="cfe74-161">Evaluation is performed as a moving average.</span></span> <span data-ttu-id="cfe74-162">Vous pourriez tooshorten cet intervalle si vos données de télémétrie sont toosudden susceptibles de pics d’activité.</span><span class="sxs-lookup"><span data-stu-id="cfe74-162">You might want tooshorten this interval if your telemetry is liable toosudden bursts.</span></span>
* `<SamplingPercentageDecreaseTimeout>00:02:00</SamplingPercentageDecreaseTimeout>`
  
    <span data-ttu-id="cfe74-163">Lorsque les modifications de valeurs de pourcentage d’échantillonnage, combien de temps après sont nous autorisée toolower à nouveau l’échantillonnage pourcentage toocapture moins de données.</span><span class="sxs-lookup"><span data-stu-id="cfe74-163">When sampling percentage value changes, how soon after are we allowed toolower sampling percentage again toocapture less data.</span></span>
* `<SamplingPercentageIncreaseTimeout>00:15:00</SamplingPercentageIncreaseTimeout>`
  
    <span data-ttu-id="cfe74-164">Lorsque les modifications de valeurs de pourcentage d’échantillonnage, combien de temps après sont nous autorisé tooincrease à nouveau l’échantillonnage pourcentage toocapture davantage de données.</span><span class="sxs-lookup"><span data-stu-id="cfe74-164">When sampling percentage value changes, how soon after are we allowed tooincrease sampling percentage again toocapture more data.</span></span>
* `<MinSamplingPercentage>0.1</MinSamplingPercentage>`
  
    <span data-ttu-id="cfe74-165">Comme l’échantillonnage du pourcentage varie, ce qui est valeur minimale de hello nous sommes autorisés tooset.</span><span class="sxs-lookup"><span data-stu-id="cfe74-165">As sampling percentage varies, what is hello minimum value we're allowed tooset.</span></span>
* `<MaxSamplingPercentage>100.0</MaxSamplingPercentage>`
  
    <span data-ttu-id="cfe74-166">Comme l’échantillonnage du pourcentage varie, ce qui est valeur maximale de hello nous sommes autorisés tooset.</span><span class="sxs-lookup"><span data-stu-id="cfe74-166">As sampling percentage varies, what is hello maximum value we're allowed tooset.</span></span>
* `<MovingAverageRatio>0.25</MovingAverageRatio>` 
  
    <span data-ttu-id="cfe74-167">Dans le calcul hello Hello moyenne mobile, poids de hello affecté toohello valeur la plus récente.</span><span class="sxs-lookup"><span data-stu-id="cfe74-167">In hello calculation of hello moving average, hello weight assigned toohello most recent value.</span></span> <span data-ttu-id="cfe74-168">Utilisez un tooor égale de valeur inférieure à 1.</span><span class="sxs-lookup"><span data-stu-id="cfe74-168">Use a value equal tooor less than 1.</span></span> <span data-ttu-id="cfe74-169">Plus petites valeurs Modifier algorithme de hello moins réactifs toosudden.</span><span class="sxs-lookup"><span data-stu-id="cfe74-169">Smaller values make hello algorithm less reactive toosudden changes.</span></span>
* `<InitialSamplingPercentage>100</InitialSamplingPercentage>`
  
    <span data-ttu-id="cfe74-170">valeur Hello affectée lors de l’application hello vient juste de démarrer.</span><span class="sxs-lookup"><span data-stu-id="cfe74-170">hello value assigned when hello app has just started.</span></span> <span data-ttu-id="cfe74-171">Ne diminuez pas cette valeur pendant le débogage.</span><span class="sxs-lookup"><span data-stu-id="cfe74-171">Don't reduce this while you're debugging.</span></span> 

* `<ExcludedTypes>Trace;Exception</ExcludedTypes>`
  
    <span data-ttu-id="cfe74-172">Un point-virgule liste délimitée par des types que vous ne voulez pas toobe échantillonnée.</span><span class="sxs-lookup"><span data-stu-id="cfe74-172">A semi-colon delimited list of types that you do not want toobe sampled.</span></span> <span data-ttu-id="cfe74-173">Les types reconnus sont : Dependency, Event, Exception, PageView, Request et Trace.</span><span class="sxs-lookup"><span data-stu-id="cfe74-173">Recognized types are: Dependency, Event, Exception, PageView, Request, Trace.</span></span> <span data-ttu-id="cfe74-174">Toutes les instances de hello spécifié de types sont transmis ; types Hello qui ne sont pas spécifiés sont échantillonnés.</span><span class="sxs-lookup"><span data-stu-id="cfe74-174">All instances of hello specified types are transmitted; hello types that are not specified are sampled.</span></span>

* `<IncludedTypes>Request;Dependency</IncludedTypes>`
  
    <span data-ttu-id="cfe74-175">Une liste délimitée par des points-virgules des types que vous souhaitez toobe échantillonnée.</span><span class="sxs-lookup"><span data-stu-id="cfe74-175">A semi-colon delimited list of types that you want toobe sampled.</span></span> <span data-ttu-id="cfe74-176">Les types reconnus sont : Dependency, Event, Exception, PageView, Request et Trace.</span><span class="sxs-lookup"><span data-stu-id="cfe74-176">Recognized types are: Dependency, Event, Exception, PageView, Request, Trace.</span></span> <span data-ttu-id="cfe74-177">Hello spécifié de types sont échantillonnés ; toutes les instances de hello autres types sont toujours transmis.</span><span class="sxs-lookup"><span data-stu-id="cfe74-177">hello specified types are sampled; all instances of hello other types will always be transmitted.</span></span>


<span data-ttu-id="cfe74-178">**tooswitch hors** échantillonnage adaptive, AdaptiveSamplingTelemetryProcessor hello supprimer un nœud à partir d’applicationinsights-config.</span><span class="sxs-lookup"><span data-stu-id="cfe74-178">**tooswitch off** adaptive sampling, remove hello AdaptiveSamplingTelemetryProcessor node from applicationinsights-config.</span></span>

### <a name="alternative-configure-adaptive-sampling-in-code"></a><span data-ttu-id="cfe74-179">Solution alternative : configurer l’échantillonnage adaptatif dans le code</span><span class="sxs-lookup"><span data-stu-id="cfe74-179">Alternative: configure adaptive sampling in code</span></span>
<span data-ttu-id="cfe74-180">Au lieu d’échantillonnage dans le fichier .config de hello, vous pouvez utiliser le code.</span><span class="sxs-lookup"><span data-stu-id="cfe74-180">Instead of adjusting sampling in hello .config file, you can use code.</span></span> <span data-ttu-id="cfe74-181">Cela vous permet de toospecify une fonction de rappel qui est appelée chaque fois que le taux d’échantillonnage de hello est réévaluée.</span><span class="sxs-lookup"><span data-stu-id="cfe74-181">This allows you toospecify a callback function that is invoked whenever hello sampling rate is re-evaluated.</span></span> <span data-ttu-id="cfe74-182">Vous pouvez l’utiliser, par exemple, toofind les taux d’échantillonnage est utilisé.</span><span class="sxs-lookup"><span data-stu-id="cfe74-182">You could use this, for example, toofind out what sampling rate is being used.</span></span>

<span data-ttu-id="cfe74-183">Supprimer hello `AdaptiveSamplingTelemetryProcessor` nœud à partir du fichier .config de hello.</span><span class="sxs-lookup"><span data-stu-id="cfe74-183">Remove hello `AdaptiveSamplingTelemetryProcessor` node from hello .config file.</span></span>

<span data-ttu-id="cfe74-184">*C#*</span><span class="sxs-lookup"><span data-stu-id="cfe74-184">*C#*</span></span>

```C#

    using Microsoft.ApplicationInsights;
    using Microsoft.ApplicationInsights.Extensibility;
    using Microsoft.ApplicationInsights.WindowsServer.Channel.Implementation;
    using Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel;
    ...

    var adaptiveSamplingSettings = new SamplingPercentageEstimatorSettings();

    // Optional: here you can adjust hello settings from their defaults.

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
             // Report hello sampling rate.
             telemetryClient.TrackMetric("samplingPercentage", newSamplingPercentage);
          }
      });

    // If you have other telemetry processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

<span data-ttu-id="cfe74-185">([En savoir plus sur les processeurs de télémétrie](app-insights-api-filtering-sampling.md#filtering).)</span><span class="sxs-lookup"><span data-stu-id="cfe74-185">([Learn about telemetry processors](app-insights-api-filtering-sampling.md#filtering).)</span></span>

<a name="other-web-pages"></a>

## <a name="sampling-for-web-pages-with-javascript"></a><span data-ttu-id="cfe74-186">Échantillonnage pour les pages web avec JavaScript</span><span class="sxs-lookup"><span data-stu-id="cfe74-186">Sampling for web pages with JavaScript</span></span>
<span data-ttu-id="cfe74-187">Vous pouvez configurer des pages Web pour l’échantillonnage à débit fixe à partir de n’importe quel serveur.</span><span class="sxs-lookup"><span data-stu-id="cfe74-187">You can configure web pages for fixed-rate sampling from any server.</span></span> 

<span data-ttu-id="cfe74-188">Lorsque vous [configurer des pages web hello pour Application Insights](app-insights-javascript.md), modifier l’extrait de code hello que vous obtenez à partir du portail d’Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="cfe74-188">When you [configure hello web pages for Application Insights](app-insights-javascript.md), modify hello snippet that you get from hello Application Insights portal.</span></span> <span data-ttu-id="cfe74-189">(Dans les applications ASP.NET, extrait de code hello passe généralement dans _Layout.cshtml.)  Insérer une ligne telle que `samplingPercentage: 10,` avant la clé d’instrumentation hello :</span><span class="sxs-lookup"><span data-stu-id="cfe74-189">(In ASP.NET apps, hello snippet typically goes in _Layout.cshtml.)  Insert a line like `samplingPercentage: 10,` before hello instrumentation key:</span></span>

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

<span data-ttu-id="cfe74-190">Pourcentage d’échantillonnage de hello, choisissez un pourcentage de fermer too100/N où N est un entier.</span><span class="sxs-lookup"><span data-stu-id="cfe74-190">For hello sampling percentage, choose a percentage that is close too100/N where N is an integer.</span></span>  <span data-ttu-id="cfe74-191">L’échantillonnage ne prend actuellement en charge aucune autre valeur.</span><span class="sxs-lookup"><span data-stu-id="cfe74-191">Currently sampling doesn't support other values.</span></span>

<span data-ttu-id="cfe74-192">Si vous activez également d’échantillonnage de taux fixe sur le serveur de hello, serveur et clients de hello synchronise donc, de recherche, vous pouvez naviguer entre les vues de page associée et des demandes.</span><span class="sxs-lookup"><span data-stu-id="cfe74-192">If you also enable fixed-rate sampling at hello server, hello clients and server will synchronize so that, in Search, you can  navigate between related page views and requests.</span></span>

## <a name="fixed-rate-sampling-for-aspnet-web-sites"></a><span data-ttu-id="cfe74-193">Échantillonnage à débit fixe pour les sites web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="cfe74-193">Fixed-rate sampling for ASP.NET web sites</span></span>
<span data-ttu-id="cfe74-194">Taux fixe échantillonnage réduit le trafic de hello envoyé à partir de votre serveur web et les navigateurs web.</span><span class="sxs-lookup"><span data-stu-id="cfe74-194">Fixed rate sampling reduces hello traffic sent from your web server and web browsers.</span></span> <span data-ttu-id="cfe74-195">À la différence de l’échantillonnage adaptatif, il réduit les données de télémétrie à un débit fixe choisi par vos soins.</span><span class="sxs-lookup"><span data-stu-id="cfe74-195">Unlike adaptive sampling, it reduces telemetry at a fixed rate decided by you.</span></span> <span data-ttu-id="cfe74-196">Il synchronise également les clients de hello et échantillonnage du serveur afin que les éléments associés sont conservés - par exemple, afin que si vous examinez un affichage de page dans la recherche, vous pouvez rechercher sa requête connexe.</span><span class="sxs-lookup"><span data-stu-id="cfe74-196">It also synchronizes hello client and server sampling so that related items are retained - for example, so that if you look at a page view in Search, you can find its related request.</span></span>

<span data-ttu-id="cfe74-197">algorithme d’échantillonnage de Hello conserve les éléments associés.</span><span class="sxs-lookup"><span data-stu-id="cfe74-197">hello sampling algorithm retains related items.</span></span> <span data-ttu-id="cfe74-198">Pour chaque événement de requête HTTP, celui-ci et ses événements associés sont ignorés ou transmis.</span><span class="sxs-lookup"><span data-stu-id="cfe74-198">For each HTTP request event, it and its related events are either discarded or transmitted.</span></span> 

<span data-ttu-id="cfe74-199">Dans Metrics Explorer, taux telles que des nombres de demande et de l’exception sont multipliés par un toocompensate de facteur de taux d’échantillonnage de hello, afin qu’ils soient environ corrects.</span><span class="sxs-lookup"><span data-stu-id="cfe74-199">In Metrics Explorer, rates such as request and exception counts are multiplied by a factor toocompensate for hello sampling rate, so that they are approximately correct.</span></span>

1. <span data-ttu-id="cfe74-200">**Mettre à jour les packages NuGet de votre projet** toohello dernière *préliminaires* version d’Application Insights.</span><span class="sxs-lookup"><span data-stu-id="cfe74-200">**Update your project's NuGet packages** toohello latest *pre-release* version of Application Insights.</span></span> <span data-ttu-id="cfe74-201">Cliquez sur projet hello dans l’Explorateur de solutions, cliquez sur Gérer les Packages NuGet, vérifiez **inclure la version préliminaire** et recherchez Microsoft.ApplicationInsights.Web.</span><span class="sxs-lookup"><span data-stu-id="cfe74-201">Right-click hello project in Solution Explorer, choose Manage NuGet Packages, check **Include prerelease** and search for Microsoft.ApplicationInsights.Web.</span></span> 
2. <span data-ttu-id="cfe74-202">**Désactiver l’échantillonnage adaptive**: dans [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), supprimez ou commentez hello `AdaptiveSamplingTelemetryProcessor` nœud.</span><span class="sxs-lookup"><span data-stu-id="cfe74-202">**Disable adaptive sampling**: In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), remove or comment out hello `AdaptiveSamplingTelemetryProcessor` node.</span></span>
   
    ```xml
   
    <TelemetryProcessors>
   
    <!-- Disabled adaptive sampling:
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    -->

    ```

1. <span data-ttu-id="cfe74-203">**Activer le module d’échantillonnage de taux fixe hello.**</span><span class="sxs-lookup"><span data-stu-id="cfe74-203">**Enable hello fixed-rate sampling module.**</span></span> <span data-ttu-id="cfe74-204">Ajoutez cet extrait de code trop[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span><span class="sxs-lookup"><span data-stu-id="cfe74-204">Add this snippet too[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span>
   
    ```XML
   
    <TelemetryProcessors>
     <Add  Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
   
      <!-- Set a percentage close too100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
      <SamplingPercentage>10</SamplingPercentage>
      </Add>
    </TelemetryProcessors>
   
    ```

> [!NOTE]
> <span data-ttu-id="cfe74-205">Pourcentage d’échantillonnage de hello, choisissez un pourcentage de fermer too100/N où N est un entier.</span><span class="sxs-lookup"><span data-stu-id="cfe74-205">For hello sampling percentage, choose a percentage that is close too100/N where N is an integer.</span></span>  <span data-ttu-id="cfe74-206">L’échantillonnage ne prend actuellement en charge aucune autre valeur.</span><span class="sxs-lookup"><span data-stu-id="cfe74-206">Currently sampling doesn't support other values.</span></span>
> 
> 

### <a name="alternative-enable-fixed-rate-sampling-in-your-server-code"></a><span data-ttu-id="cfe74-207">Solution alternative : activez l’échantillonnage à taux fixe dans le code serveur</span><span class="sxs-lookup"><span data-stu-id="cfe74-207">Alternative: enable fixed-rate sampling in your server code</span></span>
<span data-ttu-id="cfe74-208">Au lieu de définir le paramètre d’échantillonnage hello dans le fichier .config de hello, vous pouvez utiliser le code.</span><span class="sxs-lookup"><span data-stu-id="cfe74-208">Instead of setting hello sampling parameter in hello .config file, you can use code.</span></span> 

<span data-ttu-id="cfe74-209">*C#*</span><span class="sxs-lookup"><span data-stu-id="cfe74-209">*C#*</span></span>

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

<span data-ttu-id="cfe74-210">([En savoir plus sur les processeurs de télémétrie](app-insights-api-filtering-sampling.md#filtering).)</span><span class="sxs-lookup"><span data-stu-id="cfe74-210">([Learn about telemetry processors](app-insights-api-filtering-sampling.md#filtering).)</span></span>

## <a name="when-toouse-sampling"></a><span data-ttu-id="cfe74-211">Lors de l’échantillonnage toouse ?</span><span class="sxs-lookup"><span data-stu-id="cfe74-211">When toouse sampling?</span></span>
<span data-ttu-id="cfe74-212">Échantillonnage adaptative est activée automatiquement si vous utilisez hello ASP.NET SDK version 2.0.0-beta3 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="cfe74-212">Adaptive sampling is automatically enabled if you use hello ASP.NET SDK version 2.0.0-beta3 or later.</span></span> <span data-ttu-id="cfe74-213">Quelle que soit la version du Kit de développement logiciel (SDK) que vous utilisez, vous pouvez utiliser l’échantillonnage d’ingestion (sur notre serveur).</span><span class="sxs-lookup"><span data-stu-id="cfe74-213">No matter what SDK version you use, you can use ingestion sampling (at our server).</span></span>

<span data-ttu-id="cfe74-214">L’échantillonnage n’est pas utile pour la plupart des applications de taille petite à moyenne.</span><span class="sxs-lookup"><span data-stu-id="cfe74-214">You don’t need sampling for most small and medium size applications.</span></span> <span data-ttu-id="cfe74-215">les informations de diagnostic Hello plus utiles et des statistiques plus précises sont obtenus en collectant des données sur vos activités de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="cfe74-215">hello most useful diagnostic information and most accurate statistics are obtained by collecting data on all your user activities.</span></span> 

<span data-ttu-id="cfe74-216">principaux avantages de Hello d’échantillonnage sont :</span><span class="sxs-lookup"><span data-stu-id="cfe74-216">hello main advantages of sampling are:</span></span>

* <span data-ttu-id="cfe74-217">Si le service Application Insights supprime (« limite ») des points de données lorsque votre application envoie un taux de télémétrie très élevé dans un court laps de temps.</span><span class="sxs-lookup"><span data-stu-id="cfe74-217">Application Insights service drops ("throttles") data points when your app sends a very high rate of telemetry in short time interval.</span></span> 
* <span data-ttu-id="cfe74-218">tookeep dans hello [quota](app-insights-pricing.md) de points de données pour votre niveau tarifaire.</span><span class="sxs-lookup"><span data-stu-id="cfe74-218">tookeep within hello [quota](app-insights-pricing.md) of data points for your pricing tier.</span></span> 
* <span data-ttu-id="cfe74-219">tooreduce du trafic réseau à partir de la collection hello de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="cfe74-219">tooreduce network traffic from hello collection of telemetry.</span></span> 

### <a name="which-type-of-sampling-should-i-use"></a><span data-ttu-id="cfe74-220">Quel type d’échantillonnage dois-je utiliser ?</span><span class="sxs-lookup"><span data-stu-id="cfe74-220">Which type of sampling should I use?</span></span>
<span data-ttu-id="cfe74-221">**Utiliser l’échantillonnage d’ingestion dans les situations suivantes :**</span><span class="sxs-lookup"><span data-stu-id="cfe74-221">**Use ingestion sampling if:**</span></span>

* <span data-ttu-id="cfe74-222">Vous dépassez souvent votre quota mensuel de données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="cfe74-222">You often go through your monthly quota of telemetry.</span></span>
* <span data-ttu-id="cfe74-223">Vous utilisez une version de hello SDK qui ne prennent en charge d’échantillonnage - par exemple, hello Kit de développement logiciel Java ou les versions d’ASP.NET antérieures à 2.</span><span class="sxs-lookup"><span data-stu-id="cfe74-223">You're using a version of hello SDK that doesn't support sampling - for example, hello Java SDK or ASP.NET versions earlier than 2.</span></span>
* <span data-ttu-id="cfe74-224">Vous obtenez un volume élevé de données de télémétrie des navigateurs web de vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="cfe74-224">You're getting a lot of telemetry from your users' web browsers.</span></span>

<span data-ttu-id="cfe74-225">**Utilisez l’échantillonnage à débit fixe si :**</span><span class="sxs-lookup"><span data-stu-id="cfe74-225">**Use fixed-rate sampling if:**</span></span>

* <span data-ttu-id="cfe74-226">Vous utilisez hello Application Insights SDK pour la version de services web ASP.NET 2.0.0 ou version ultérieure, et</span><span class="sxs-lookup"><span data-stu-id="cfe74-226">You're using hello Application Insights SDK for ASP.NET web services version 2.0.0 or later, and</span></span>
* <span data-ttu-id="cfe74-227">Vous souhaitez un échantillonnage synchronisés entre client et serveur, afin que, lorsque vous recherchez des événements dans [recherche](app-insights-diagnostic-search.md), vous pouvez naviguer entre les événements connexes sur le client de hello et de serveur, telles que les vues de page et de requêtes http.</span><span class="sxs-lookup"><span data-stu-id="cfe74-227">You want synchronized sampling between client and server, so that, when you're investigating events in [Search](app-insights-diagnostic-search.md), you can navigate between related events on hello client and server, such as page views and http requests.</span></span>
* <span data-ttu-id="cfe74-228">Vous êtes certain de pourcentage d’échantillonnage approprié de hello pour votre application.</span><span class="sxs-lookup"><span data-stu-id="cfe74-228">You are confident of hello appropriate sampling percentage for your app.</span></span> <span data-ttu-id="cfe74-229">Il doit être suffisamment élevée tooget des mesures précises, mais ci-dessous hello taux dépasse votre quota de tarification et hello limites.</span><span class="sxs-lookup"><span data-stu-id="cfe74-229">It should be high enough tooget accurate metrics, but below hello rate that exceeds your pricing quota and hello throttling limits.</span></span> 

<span data-ttu-id="cfe74-230">**Utilisez l’échantillonnage adaptatif :**</span><span class="sxs-lookup"><span data-stu-id="cfe74-230">**Use adaptive sampling:**</span></span>

<span data-ttu-id="cfe74-231">Dans le cas contraire, nous vous recommandons d’utiliser l’échantillonnage adaptatif.</span><span class="sxs-lookup"><span data-stu-id="cfe74-231">Otherwise, we recommend adaptive sampling.</span></span> <span data-ttu-id="cfe74-232">Cette option est activée par défaut sur un serveur d’ASP.NET hello SDK, version 2.0.0-beta3 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="cfe74-232">This is enabled by default in hello ASP.NET server SDK, version 2.0.0-beta3 or later.</span></span> <span data-ttu-id="cfe74-233">Comme il ne réduit pas le trafic jusqu’à un certain débit minimum, il n’affecte pas un site peu utilisé.</span><span class="sxs-lookup"><span data-stu-id="cfe74-233">It doesn't reduce traffic until a certain minimum rate, so it won't affect a low-use site.</span></span>

## <a name="how-do-i-know-whether-sampling-is-in-operation"></a><span data-ttu-id="cfe74-234">Comment savoir si l’échantillonnage est utilisé ?</span><span class="sxs-lookup"><span data-stu-id="cfe74-234">How do I know whether sampling is in operation?</span></span>
<span data-ttu-id="cfe74-235">hello toodiscover réel d’échantillonnage taux, quel que soit l’où il a été appliqué, utilisez un [les requête Analytique](app-insights-analytics.md) comme celui-ci :</span><span class="sxs-lookup"><span data-stu-id="cfe74-235">toodiscover hello actual sampling rate no matter where it has been applied, use an [Analytics query](app-insights-analytics.md) such as this:</span></span>

    requests | where timestamp > ago(1d)
    | summarize 100/avg(itemCount) by bin(timestamp, 1h) 
    | render areachart 

<span data-ttu-id="cfe74-236">Chaque enregistrement, conservé `itemCount` indique nombre hello d’origine enregistrements qu’elle représente, too1 égal + nombre de hello d’anciens enregistrements rejetés.</span><span class="sxs-lookup"><span data-stu-id="cfe74-236">In each retained record, `itemCount` indicates hello number of original records that it represents, equal too1 + hello number of previous discarded records.</span></span> 

## <a name="how-does-sampling-work"></a><span data-ttu-id="cfe74-237">Comment fonctionne l’échantillonnage ?</span><span class="sxs-lookup"><span data-stu-id="cfe74-237">How does sampling work?</span></span>
<span data-ttu-id="cfe74-238">Taux fixe et échantillonnage adapté sont une fonctionnalité de hello SDK dans les versions ASP.NET à partir de 2.0.0 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="cfe74-238">Fixed-rate and adaptive sampling are a feature of hello SDK in ASP.NET versions from 2.0.0 onwards.</span></span> <span data-ttu-id="cfe74-239">Échantillonnage de réception est une fonctionnalité de hello service Application Insights et peut être dans l’opération si hello SDK n’effectue pas d’échantillonnage.</span><span class="sxs-lookup"><span data-stu-id="cfe74-239">Ingestion sampling is a feature of hello Application Insights service, and can be in operation if hello SDK is not performing sampling.</span></span> 

<span data-ttu-id="cfe74-240">algorithme d’échantillonnage de Hello décide quelle toodrop d’éléments de télémétrie et le tookeep celles (s’il s’agit dans le Kit de développement logiciel de hello ou dans le service Application Insights hello).</span><span class="sxs-lookup"><span data-stu-id="cfe74-240">hello sampling algorithm decides which telemetry items toodrop, and which ones tookeep (whether it's in hello SDK or in hello Application Insights service).</span></span> <span data-ttu-id="cfe74-241">la décision d’échantillonnage de Hello repose sur plusieurs règles visant toopreserve intact, en conservant une expérience de diagnostic dans Application Insights exploitables et fiable même avec un jeu de données réduit tous les points de données reliées entre elles.</span><span class="sxs-lookup"><span data-stu-id="cfe74-241">hello sampling decision is based on several rules that aim toopreserve all interrelated data points intact, maintaining a diagnostic experience in Application Insights that is actionable and reliable even with a reduced data set.</span></span> <span data-ttu-id="cfe74-242">En cas d’échec d’une requête, par exemple, si votre application envoie d’autres éléments de télémétrie (tels que les exceptions et les traces enregistrées à partir de cette requête), l’échantillonnage ne fractionnera ni cette requête ni les autres éléments de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="cfe74-242">For example, if for a failed request your app sends additional telemetry items (such as exception and traces logged from this request), sampling will not split this request and other telemetry.</span></span> <span data-ttu-id="cfe74-243">Il les conservera ou supprimera ensemble.</span><span class="sxs-lookup"><span data-stu-id="cfe74-243">It either keeps or drops them all together.</span></span> <span data-ttu-id="cfe74-244">Par conséquent, lorsque vous examinez les détails de la demande hello dans Application Insights, vous voyez toujours demande hello, ainsi que ses éléments de télémétrie associée.</span><span class="sxs-lookup"><span data-stu-id="cfe74-244">As a result, when you look at hello request details in Application Insights, you can always see hello request along with its associated telemetry items.</span></span> 

<span data-ttu-id="cfe74-245">Pour les applications qui définissent le « utilisateur » (autrement dit, les applications web les plus typiques), la décision d’échantillonnage de hello repose sur hachage hello de pseudo hello, ce qui signifie que toutes les données de télémétrie pour un utilisateur spécifique sont conservée ou supprimée.</span><span class="sxs-lookup"><span data-stu-id="cfe74-245">For applications that define "user" (that is, most typical web applications), hello sampling decision is based on hello hash of hello user id, which means that all telemetry for any particular user is either preserved or dropped.</span></span> <span data-ttu-id="cfe74-246">Pour les types d’applications que vous ne définissent pas les utilisateurs (tels que les services web) hello la décision d’échantillonnage de hello est basée sur l’id de l’opération de demande de hello hello.</span><span class="sxs-lookup"><span data-stu-id="cfe74-246">For hello types of applications that don't define users (such as web services) hello sampling decision is based on hello operation id of hello request.</span></span> <span data-ttu-id="cfe74-247">Enfin, pour les éléments de télémétrie hello qui n’ont des id utilisateur ni d’opération (pour les exemples d’éléments de télémétrie signalés par les threads asynchrones sans contexte http) échantillonnage capture simplement un pourcentage d’éléments de télémétrie de chaque type.</span><span class="sxs-lookup"><span data-stu-id="cfe74-247">Finally, for hello telemetry items that neither have user nor operation id set (for example telemetry items reported from asynchronous threads with no http context) sampling simply captures a percentage of telemetry items of each type.</span></span> 

<span data-ttu-id="cfe74-248">Lors de la présentation tooyou arrière de télémétrie, hello Application Insights service ajuste les métriques de hello en hello même pourcentage d’échantillonnage qui a été utilisé au moment de hello de collection, toocompensate pourquoi les points de données manquants.</span><span class="sxs-lookup"><span data-stu-id="cfe74-248">When presenting telemetry back tooyou, hello Application Insights service adjusts hello metrics by hello same sampling percentage that was used at hello time of collection, toocompensate for hello missing data points.</span></span> <span data-ttu-id="cfe74-249">Par conséquent, lorsque vous examinez la télémétrie hello dans Application Insights, hello infligés aux utilisateurs des approximations statistique correctes qui sont des nombres réels toohello très proche.</span><span class="sxs-lookup"><span data-stu-id="cfe74-249">Hence, when looking at hello telemetry in Application Insights, hello users are seeing statistically correct approximations that are very close toohello real numbers.</span></span>

<span data-ttu-id="cfe74-250">précision Hello de rapprochement de hello dépend en grande partie de pourcentage d’échantillonnage de hello configuré.</span><span class="sxs-lookup"><span data-stu-id="cfe74-250">hello accuracy of hello approximation largely depends on hello configured sampling percentage.</span></span> <span data-ttu-id="cfe74-251">En outre, une précision hello augmente pour les applications qui gèrent un grand nombre de demandes généralement semblables à partir d’un grand nombre d’utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="cfe74-251">Also, hello accuracy increases for applications that handle a large volume of generally similar requests from lots of users.</span></span> <span data-ttu-id="cfe74-252">Sur hello autre part, pour les applications qui ne fonctionnent pas avec une charge importante, l’échantillonnage n’est pas nécessaire que ces applications peuvent envoyer généralement toutes leurs données de télémétrie tout en restant dans le quota de hello, sans entraîner de perte de données à partir de la limitation.</span><span class="sxs-lookup"><span data-stu-id="cfe74-252">On hello other hand, for applications that don't work with a significant load, sampling is not needed as these applications can usually send all their telemetry while staying within hello quota, without causing data loss from throttling.</span></span> 

<span data-ttu-id="cfe74-253">Notez que Application Insights ne pas échantillonner des Sessions et les métriques des types de télémétrie, depuis pour ces types, la réduction de la précision de hello peut être souhaitable.</span><span class="sxs-lookup"><span data-stu-id="cfe74-253">Note that Application Insights does not sample Metrics and Sessions telemetry types, since for these types, reduction in hello precision can be highly undesirable.</span></span> 

### <a name="adaptive-sampling"></a><span data-ttu-id="cfe74-254">échantillonnage adaptatif</span><span class="sxs-lookup"><span data-stu-id="cfe74-254">Adaptive sampling</span></span>
<span data-ttu-id="cfe74-255">Échantillonnage Adaptive ajoute un composant cette vitesse de transmission pour les analyses hello actuelle hello SDK et ajuste hello d’échantillonnage pourcentage tootry toostay au sein de la vitesse maximale de hello cible.</span><span class="sxs-lookup"><span data-stu-id="cfe74-255">Adaptive sampling adds a component that monitors hello current rate of transmission from hello SDK, and adjusts hello sampling percentage tootry toostay within hello target maximum rate.</span></span> <span data-ttu-id="cfe74-256">l’ajustement Hello est recalculé à intervalles réguliers et est basé sur une moyenne mobile de hello vitesse de transmission de sortie.</span><span class="sxs-lookup"><span data-stu-id="cfe74-256">hello adjustment is recalculated at regular intervals, and is based on a moving average of hello outgoing transmission rate.</span></span>

## <a name="sampling-and-hello-javascript-sdk"></a><span data-ttu-id="cfe74-257">Échantillonnage et hello SDK JavaScript</span><span class="sxs-lookup"><span data-stu-id="cfe74-257">Sampling and hello JavaScript SDK</span></span>
<span data-ttu-id="cfe74-258">Hello côté client (JavaScript) SDK participe échantillonnage taux fixe en conjonction avec hello côté serveur SDK.</span><span class="sxs-lookup"><span data-stu-id="cfe74-258">hello client-side (JavaScript) SDK participates in fixed-rate sampling in conjunction with hello server-side SDK.</span></span> <span data-ttu-id="cfe74-259">pages de Hello instrumenté n’envoie les données de télémétrie côté client de hello aux mêmes utilisateurs pour le hello côté serveur fait son choix trop « sample dans. »</span><span class="sxs-lookup"><span data-stu-id="cfe74-259">hello instrumented pages will only send client-side telemetry from hello same users for which hello server-side made its decision too"sample in."</span></span> <span data-ttu-id="cfe74-260">Cette logique est intégrité toomaintain conçu d’une session utilisateur entre les côtés client et serveur.</span><span class="sxs-lookup"><span data-stu-id="cfe74-260">This logic is designed toomaintain integrity of user session across client- and server-sides.</span></span> <span data-ttu-id="cfe74-261">En partant de n’importe quel élément de télémétrie dans Application Insights, vous retrouverez donc tous les autres éléments de télémétrie associés à l’utilisateur ou à la session en question.</span><span class="sxs-lookup"><span data-stu-id="cfe74-261">As a result, from any particular telemetry item in Application Insights you can find all other telemetry items for this user or session.</span></span> 

<span data-ttu-id="cfe74-262">*Mes données de télémétrie côté client et côté serveur n’affichent pas les échantillons coordonnés que vous décrivez ci-dessus.*</span><span class="sxs-lookup"><span data-stu-id="cfe74-262">*My client and server-side telemetry don't show coordinated samples as you describe above.*</span></span>

* <span data-ttu-id="cfe74-263">Vérifiez que vous avez activé l’échantillonnage à débit fixe à la fois sur le serveur et sur le client.</span><span class="sxs-lookup"><span data-stu-id="cfe74-263">Verify that you enabled fixed-rate sampling both on server and client.</span></span>
* <span data-ttu-id="cfe74-264">Assurez-vous que cette version du Kit de développement logiciel hello est 2.0 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="cfe74-264">Make sure that hello SDK version is 2.0 or above.</span></span>
* <span data-ttu-id="cfe74-265">Vérifiez que vous définissez hello même d’échantillonnage du pourcentage de hello client et le serveur.</span><span class="sxs-lookup"><span data-stu-id="cfe74-265">Check that you set hello same sampling percentage in both hello client and server.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="cfe74-266">Forum Aux Questions (FAQ)</span><span class="sxs-lookup"><span data-stu-id="cfe74-266">Frequently Asked Questions</span></span>
<span data-ttu-id="cfe74-267">*Pourquoi l’échantillonnage ne permet-il pas simplement de « collecter X % de chaque type de télémétrie » ?*</span><span class="sxs-lookup"><span data-stu-id="cfe74-267">*Why isn't sampling a simple "collect X percent of each telemetry type"?*</span></span>

* <span data-ttu-id="cfe74-268">Alors que cette approche d’échantillonnage peuvent fournir une très haute précision des approximations de métriques, il compromettrait capacité toocorrelate des données de diagnostic par l’utilisateur, de session et de demande, ce qui est essentiel pour les diagnostics.</span><span class="sxs-lookup"><span data-stu-id="cfe74-268">While this sampling approach would provide with a very high precision in metric approximations, it would break ability toocorrelate diagnostic data per user, session, and request, which is critical for diagnostics.</span></span> <span data-ttu-id="cfe74-269">L’échantillonnage est donc plus efficace lorsqu’il revient à « collecter tous les éléments de télémétrie pour X % des utilisateurs de l’application » ou à « collecter tous les éléments de télémétrie pour X % des requêtes de l’application ».</span><span class="sxs-lookup"><span data-stu-id="cfe74-269">Therefore, sampling works better with "collect all telemetry items for X percent of app users", or "collect all telemetry for X percent of app requests" logic.</span></span> <span data-ttu-id="cfe74-270">Pour les éléments de télémétrie hello ne pas associés aux demandes de hello (par exemple, le traitement asynchrone d’en arrière-plan) font partie de hello est trop « collecter X % de tous les éléments pour chaque type de données de télémétrie. »</span><span class="sxs-lookup"><span data-stu-id="cfe74-270">For hello telemetry items not associated with hello requests (such as background asynchronous processing), hello fall back is too"collect X percent of all items for each telemetry type."</span></span> 

<span data-ttu-id="cfe74-271">*Pourcentage d’échantillonnage hello permettre changer au fil du temps ?*</span><span class="sxs-lookup"><span data-stu-id="cfe74-271">*Can hello sampling percentage change over time?*</span></span>

* <span data-ttu-id="cfe74-272">Oui, l’échantillonnage adaptive progressivement modifie hello d’échantillonnage, basées sur des pourcentages sur hello actuellement observée volume de données de télémétrie hello.</span><span class="sxs-lookup"><span data-stu-id="cfe74-272">Yes, adaptive sampling gradually changes hello sampling percentage, based on hello currently observed volume of hello telemetry.</span></span>

<span data-ttu-id="cfe74-273">*Si vous utilisez l’échantillonnage taux fixe, comment puis-je savoir quel échantillonnage pourcentage fonctionnera hello mieux à mon application ?*</span><span class="sxs-lookup"><span data-stu-id="cfe74-273">*If I use fixed-rate sampling, how do I know which sampling percentage will work hello best for my app?*</span></span>

* <span data-ttu-id="cfe74-274">Une façon est toostart avec échantillonnage adaptive, découvrez ce que le taux règle sur (voir hello question ci-dessus), puis commutateur toofixed-taux d’échantillonnage à l’aide de ce taux.</span><span class="sxs-lookup"><span data-stu-id="cfe74-274">One way is toostart with adaptive sampling, find out what rate it settles on (see hello above question), and then switch toofixed-rate sampling using that rate.</span></span> 
  
    <span data-ttu-id="cfe74-275">Dans le cas contraire, vous avez tooguess.</span><span class="sxs-lookup"><span data-stu-id="cfe74-275">Otherwise, you have tooguess.</span></span> <span data-ttu-id="cfe74-276">Analyser votre utilisation actuelle de la télémétrie dans AI, observez une limitation qui est en cours et estimation hello volume de télémétrie de hello collectée.</span><span class="sxs-lookup"><span data-stu-id="cfe74-276">Analyze your current telemetry usage in AI, observe any throttling that is occurring, and estimate hello volume of hello collected telemetry.</span></span> <span data-ttu-id="cfe74-277">Ces trois entrées, ainsi que le niveau tarifaire sélectionné, suggèrent combien vous pourriez volume de hello tooreduce de télémétrie de hello collectée.</span><span class="sxs-lookup"><span data-stu-id="cfe74-277">These three inputs, together with your selected pricing tier, suggest how much you might want tooreduce hello volume of hello collected telemetry.</span></span> <span data-ttu-id="cfe74-278">Toutefois, l’augmentation nombre hello de vos utilisateurs ou certaines autres MAJ volume hello de télémétrie peut invalider votre estimation.</span><span class="sxs-lookup"><span data-stu-id="cfe74-278">However, an increase in hello number of your users or some other shift in hello volume of telemetry might invalidate your estimate.</span></span>

<span data-ttu-id="cfe74-279">*Que se passe-t-il si je configure le pourcentage d’échantillonnage à un niveau trop faible ?*</span><span class="sxs-lookup"><span data-stu-id="cfe74-279">*What happens if I configure sampling percentage too low?*</span></span>

* <span data-ttu-id="cfe74-280">Le pourcentage d’échantillonnage excessivement basse (échantillonnage over-aggressive) réduit la précision hello des approximations de hello, lors de l’Application Insights tente de visualisation de hello toocompensate de données hello hello données réduction de volume.</span><span class="sxs-lookup"><span data-stu-id="cfe74-280">Excessively low sampling percentage (over-aggressive sampling) reduces hello accuracy of hello approximations, when Application Insights attempts toocompensate hello visualization of hello data for hello data volume reduction.</span></span> <span data-ttu-id="cfe74-281">En outre, expérience de diagnostic peut-être être réduite, car certaines de hello rarement échouent ou lente aux demandes peuvent être échantillonnés.</span><span class="sxs-lookup"><span data-stu-id="cfe74-281">Also, diagnostic experience might be negatively impacted, as some of hello infrequently failing or slow requests may be sampled out.</span></span>

<span data-ttu-id="cfe74-282">*Que se passe-t-il si je configure un pourcentage d’échantillonnage trop élevé ?*</span><span class="sxs-lookup"><span data-stu-id="cfe74-282">*What happens if I configure sampling percentage too high?*</span></span>

* <span data-ttu-id="cfe74-283">Configuration d’échantillonnage trop élevée pourcentage (pas agressif suffisamment) entraîne une réduction insuffisante dans le volume hello Hello collectées télémétrie.</span><span class="sxs-lookup"><span data-stu-id="cfe74-283">Configuring too high sampling percentage (not aggressive enough) results in an insufficient reduction in hello volume of hello collected telemetry.</span></span> <span data-ttu-id="cfe74-284">Vous pouvez rencontrer une perte de données liées toothrottling et hello le coût de l’utilisation d’Application Insights peuvent être plus élevée que prévu en raison des frais toooverage de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="cfe74-284">You may still experience telemetry data loss related toothrottling, and hello cost of using Application Insights might be higher than you planned due toooverage charges.</span></span>

<span data-ttu-id="cfe74-285">*Sur quelles plates-formes puis-je utiliser l’échantillonnage ?*</span><span class="sxs-lookup"><span data-stu-id="cfe74-285">*On what platforms can I use sampling?*</span></span>

* <span data-ttu-id="cfe74-286">Échantillonnage de réception peut se produire automatiquement pour toutes les données de télémétrie au-dessus d’un certain volume si hello SDK n’effectue pas d’échantillonnage.</span><span class="sxs-lookup"><span data-stu-id="cfe74-286">Ingestion sampling can occur automatically for any telemetry above a certain volume, if hello SDK is not performing sampling.</span></span> <span data-ttu-id="cfe74-287">Cela fonctionne, par exemple, si votre application utilise un serveur Java, ou si vous utilisez une version antérieure de hello Kit de développement ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="cfe74-287">This would work, for example, if your app uses a Java server, or if you are using an older version of hello ASP.NET SDK.</span></span>
* <span data-ttu-id="cfe74-288">Si vous utilisez des versions du Kit de développement ASP.NET 2.0.0 et versions ultérieures (hébergé dans Azure ou sur votre propre serveur), vous obtenez adaptative d’échantillonnage par défaut, mais vous pouvez basculer le taux de toofixed comme décrit ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="cfe74-288">If you're using ASP.NET SDK versions 2.0.0 and above (hosted either in Azure or on your own server), you get adaptive sampling by default, but you can switch toofixed-rate as described above.</span></span> <span data-ttu-id="cfe74-289">Avec un taux fixe échantillonnage, le navigateur hello SDK synchronise automatiquement toosample des événements connexes.</span><span class="sxs-lookup"><span data-stu-id="cfe74-289">With fixed-rate sampling, hello browser SDK automatically synchronizes toosample related events.</span></span> 

<span data-ttu-id="cfe74-290">*Il existe certains événements rares que je veux toujours toosee. Comment puis-je obtenir les au-delà de module d’échantillonnage de hello ?*</span><span class="sxs-lookup"><span data-stu-id="cfe74-290">*There are certain rare events I always want toosee. How can I get them past hello sampling module?*</span></span>

* <span data-ttu-id="cfe74-291">Initialiser une instance distincte de TelemetryClient avec une nouveau TelemetryConfiguration (pas hello par défaut actif).</span><span class="sxs-lookup"><span data-stu-id="cfe74-291">Initialize a separate instance of TelemetryClient with a new TelemetryConfiguration (not hello default Active one).</span></span> <span data-ttu-id="cfe74-292">Utilisez ce toosend vos événements rares.</span><span class="sxs-lookup"><span data-stu-id="cfe74-292">Use that toosend your rare events.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cfe74-293">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cfe74-293">Next steps</span></span>
* <span data-ttu-id="cfe74-294">[filtrage](app-insights-api-filtering-sampling.md) peut fournir un contrôle plus strict de ce que le Kit de développement logiciel (SDK) envoie.</span><span class="sxs-lookup"><span data-stu-id="cfe74-294">[Filtering](app-insights-api-filtering-sampling.md) can provide more strict control of what your SDK sends.</span></span>

