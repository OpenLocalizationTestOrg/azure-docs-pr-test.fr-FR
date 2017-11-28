---
title: "aaaMonitor performances d’application web Azure | Documents Microsoft"
description: "Analyse des performances des applications pour les applications web Azure. Graphique de charge et de temps de réponse, informations de dépendance et alertes sur les performances."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 0b2deb30-6ea8-4bc4-8ed0-26765b85149f
ms.service: azure-portal
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/05/2017
ms.author: bwren
ms.openlocfilehash: d1083254e5c504b18f2ac5ae2368610dc2790436
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-web-app-performance"></a><span data-ttu-id="6fb83-104">Surveillance des performances d'application web Azure</span><span class="sxs-lookup"><span data-stu-id="6fb83-104">Monitor Azure web app performance</span></span>
<span data-ttu-id="6fb83-105">Bonjour [Azure Portal](https://portal.azure.com) vous pouvez configurer d’analyse des performances des applications pour votre [Azure web apps](../app-service-web/app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6fb83-105">In hello [Azure Portal](https://portal.azure.com) you can set up application performance monitoring for your [Azure web apps](../app-service-web/app-service-web-overview.md).</span></span> <span data-ttu-id="6fb83-106">[Azure Application Insights](app-insights-overview.md) instrumente votre application toosend télémétrie relative à son toohello activités service Application Insights, où il est stocké et analysée.</span><span class="sxs-lookup"><span data-stu-id="6fb83-106">[Azure Application Insights](app-insights-overview.md) instruments your app toosend telemetry about its activities toohello Application Insights service, where it is stored and analyzed.</span></span> <span data-ttu-id="6fb83-107">Là, les graphiques de métriques et outils de recherche peuvent être utilisés toohelp diagnostiquer les problèmes, améliorer les performances et évaluer l’utilisation.</span><span class="sxs-lookup"><span data-stu-id="6fb83-107">There, metric charts and search tools can be used toohelp diagnose issues, improve performance, and assess usage.</span></span>

## <a name="run-time-or-build-time"></a><span data-ttu-id="6fb83-108">En cours d’exécution ou en cours de création</span><span class="sxs-lookup"><span data-stu-id="6fb83-108">Run time or build time</span></span>
<span data-ttu-id="6fb83-109">Vous pouvez configurer la surveillance en instrumentant application hello de deux manières :</span><span class="sxs-lookup"><span data-stu-id="6fb83-109">You can configure monitoring by instrumenting hello app in either of two ways:</span></span>

* <span data-ttu-id="6fb83-110">**En cours d’exécution** : vous pouvez sélectionner une extension de surveillance des performances lorsque votre application est déjà active.</span><span class="sxs-lookup"><span data-stu-id="6fb83-110">**Run-time** - You can select a performance monitoring extension when your web app is already live.</span></span> <span data-ttu-id="6fb83-111">Il n’est pas toorebuild nécessaire ou réinstaller votre application.</span><span class="sxs-lookup"><span data-stu-id="6fb83-111">It isn't necessary toorebuild or re-install your app.</span></span> <span data-ttu-id="6fb83-112">Vous obtenez un ensemble standard de packages qui analyse les temps de réponse, les taux de réussite, les exceptions, les dépendances, etc.</span><span class="sxs-lookup"><span data-stu-id="6fb83-112">You get a standard set of packages that monitor response times, success rates, exceptions, dependencies, and so on.</span></span> 
* <span data-ttu-id="6fb83-113">**En cours de création** : vous pouvez installer un package dans votre application en cours de développement.</span><span class="sxs-lookup"><span data-stu-id="6fb83-113">**Build time** - You can install a package in your app in development.</span></span> <span data-ttu-id="6fb83-114">Cette option est plus souple.</span><span class="sxs-lookup"><span data-stu-id="6fb83-114">This option is more versatile.</span></span> <span data-ttu-id="6fb83-115">En outre toohello mêmes packages standard, vous pouvez écrire des données de télémétrie code toocustomize hello ou toosend vos propres données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="6fb83-115">In addition toohello same standard packages, you can write code toocustomize hello telemetry or toosend your own telemetry.</span></span> <span data-ttu-id="6fb83-116">Vous pouvez enregistrer des activités spécifiques ou enregistrer les événements selon la sémantique de toohello de votre domaine d’application.</span><span class="sxs-lookup"><span data-stu-id="6fb83-116">You can log specific activities or record events according toohello semantics of your app domain.</span></span> 

## <a name="run-time-instrumentation-with-application-insights"></a><span data-ttu-id="6fb83-117">Instrumentation d’exécution avec Application Insights</span><span class="sxs-lookup"><span data-stu-id="6fb83-117">Run time instrumentation with Application Insights</span></span>
<span data-ttu-id="6fb83-118">Si vous exécutez déjà une application web dans Azure, vous obtenez déjà certains éléments de surveillance, tels que le taux de demande et d’erreur.</span><span class="sxs-lookup"><span data-stu-id="6fb83-118">If you're already running a web app in Azure, you already get some monitoring: request and error rates.</span></span> <span data-ttu-id="6fb83-119">Ajouter Application Insights tooget de plus, telles que le temps de réponse, la surveillance toodependencies d’appels, détection active et puissant langage de requête Analytique de journal hello.</span><span class="sxs-lookup"><span data-stu-id="6fb83-119">Add Application Insights tooget more, such as response times, monitoring calls toodependencies, smart detection, and hello powerful Log Analytics query language.</span></span> 

1. <span data-ttu-id="6fb83-120">**Sélectionnez l’Application Insights** dans hello Azure le panneau de configuration pour votre application web.</span><span class="sxs-lookup"><span data-stu-id="6fb83-120">**Select Application Insights** in hello Azure control panel for your web app.</span></span>
   
    ![Sous Surveillance, choisissez Application Insights](./media/app-insights-azure-web-apps/05-extend.png)
   
   * <span data-ttu-id="6fb83-122">Choisissez toocreate une nouvelle ressource, sauf si vous avez déjà défini une ressource Application Insights pour cette application par un autre itinéraire.</span><span class="sxs-lookup"><span data-stu-id="6fb83-122">Choose toocreate a new resource, unless you already set up an Application Insights resource for this app by another route.</span></span>
2. <span data-ttu-id="6fb83-123">**Instrumentez votre application web** après l’installation d’Application Insights.</span><span class="sxs-lookup"><span data-stu-id="6fb83-123">**Instrument your web app** after Application Insights has been installed.</span></span> 
   
    ![Instrumenter votre application web](./media/app-insights-azure-web-apps/restart-web-app-for-insights.png)

   <span data-ttu-id="6fb83-125">**Activer l’analyse côté client** pour la consultation de page et la télémétrie de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6fb83-125">**Enable client side monitoring** for page view and user telemetry.</span></span>

   * <span data-ttu-id="6fb83-126">Cliquez sur Paramètres > Paramètres de l’application</span><span class="sxs-lookup"><span data-stu-id="6fb83-126">Select Settings > Application Settings</span></span>
   * <span data-ttu-id="6fb83-127">Sous Paramètres de l’application, ajoutez une nouvelle paire clé/valeur :</span><span class="sxs-lookup"><span data-stu-id="6fb83-127">Under App Settings, add a new key value pair:</span></span> 
   
    <span data-ttu-id="6fb83-128">Clé :`APPINSIGHTS_JAVASCRIPT_ENABLED`</span><span class="sxs-lookup"><span data-stu-id="6fb83-128">Key: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span></span> 
    
    <span data-ttu-id="6fb83-129">Valeur: `true`</span><span class="sxs-lookup"><span data-stu-id="6fb83-129">Value: `true`</span></span>
   * <span data-ttu-id="6fb83-130">**Enregistrer** hello paramètres et **redémarrer** votre application.</span><span class="sxs-lookup"><span data-stu-id="6fb83-130">**Save** hello settings and **Restart** your app.</span></span>
3. <span data-ttu-id="6fb83-131">**Surveillez votre application web**.</span><span class="sxs-lookup"><span data-stu-id="6fb83-131">**Monitor your app**.</span></span>  <span data-ttu-id="6fb83-132">[Les données de salutation Expore](#explore-the-data).</span><span class="sxs-lookup"><span data-stu-id="6fb83-132">[Expore hello data](#explore-the-data).</span></span>

<span data-ttu-id="6fb83-133">Une version ultérieure, vous pouvez générer application hello avec Application Insights si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="6fb83-133">Later, you can build hello app with Application Insights if you want.</span></span>

<span data-ttu-id="6fb83-134">*Comment supprimer l’Application Insights, ou basculez toosending tooanother ressource ?*</span><span class="sxs-lookup"><span data-stu-id="6fb83-134">*How do I remove Application Insights, or switch toosending tooanother resource?*</span></span>

* <span data-ttu-id="6fb83-135">Dans Azure, le panneau de contrôle web application hello ouvert et sous Outils de développement, ouvrez **Extensions**.</span><span class="sxs-lookup"><span data-stu-id="6fb83-135">In Azure, open hello web app control blade, and under Development Tools, open **Extensions**.</span></span> <span data-ttu-id="6fb83-136">Suppression de l’extension d’Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="6fb83-136">Delete hello Application Insights extension.</span></span> <span data-ttu-id="6fb83-137">Puis sous analyse, choisissez Application Insights et créez ou sélectionnez la ressource hello souhaitée.</span><span class="sxs-lookup"><span data-stu-id="6fb83-137">Then under Monitoring, choose Application Insights and create or select hello resource you want.</span></span>

## <a name="build-hello-app-with-application-insights"></a><span data-ttu-id="6fb83-138">Générez l’application hello avec Application Insights</span><span class="sxs-lookup"><span data-stu-id="6fb83-138">Build hello app with Application Insights</span></span>
<span data-ttu-id="6fb83-139">Application Insights peut fournir des données de télémétrie détaillée par l’installation d’un SDK dans votre application.</span><span class="sxs-lookup"><span data-stu-id="6fb83-139">Application Insights can provide more detailed telemetry by installing an SDK into your app.</span></span> <span data-ttu-id="6fb83-140">En particulier, vous pouvez collecter les journaux de suivi, [écrire une télémétrie personnalisée](app-insights-api-custom-events-metrics.md), et obtenir des rapports d’exception plus détaillées.</span><span class="sxs-lookup"><span data-stu-id="6fb83-140">In particular, you can collect trace logs, [write custom telemetry](app-insights-api-custom-events-metrics.md), and get more detailed exception reports.</span></span>

1. <span data-ttu-id="6fb83-141">**Dans Visual Studio** (2013 mise à jour 2 ou ultérieure), configurez Application Insights pour votre projet.</span><span class="sxs-lookup"><span data-stu-id="6fb83-141">**In Visual Studio** (2013 update 2 or later), configure Application Insights for your project.</span></span>

    <span data-ttu-id="6fb83-142">Droit hello web projet, puis sélectionnez **Ajouter > Application Insights** ou **configurer Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="6fb83-142">Right-click hello web project, and select **Add > Application Insights** or **Configure Application Insights**.</span></span>
   
    ![Droit hello web projet, puis choisissez Ajouter ou configurer Application Insights](./media/app-insights-azure-web-apps/03-add.png)
   
    <span data-ttu-id="6fb83-144">Si vous êtes invité toosign dans, utiliser les informations d’identification de l’hello pour votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="6fb83-144">If you're asked toosign in, use hello credentials for your Azure account.</span></span>
   
    <span data-ttu-id="6fb83-145">opération de Hello a deux effets :</span><span class="sxs-lookup"><span data-stu-id="6fb83-145">hello operation has two effects:</span></span>
   
   1. <span data-ttu-id="6fb83-146">Création d’une ressource Application Insights dans Azure, à l’endroit où vos données de télémétrie sont stockées, analysées et affichées.</span><span class="sxs-lookup"><span data-stu-id="6fb83-146">Creates an Application Insights resource in Azure, where telemetry is stored, analyzed and displayed.</span></span>
   2. <span data-ttu-id="6fb83-147">Ajoute hello NuGet Application Insights tooyour code du package (si elle n’existait pas déjà) et il configure toosend télémétrie toohello ressource Azure.</span><span class="sxs-lookup"><span data-stu-id="6fb83-147">Adds hello Application Insights NuGet package tooyour code (if it isn't there already), and configures it toosend telemetry toohello Azure resource.</span></span>
2. <span data-ttu-id="6fb83-148">**Tester les données de télémétrie hello** par application de hello en cours d’exécution sur votre ordinateur de développement (F5).</span><span class="sxs-lookup"><span data-stu-id="6fb83-148">**Test hello telemetry** by running hello app in your development machine (F5).</span></span>
3. <span data-ttu-id="6fb83-149">**Publier l’application hello** tooAzure Bonjour normalement.</span><span class="sxs-lookup"><span data-stu-id="6fb83-149">**Publish hello app** tooAzure in hello usual way.</span></span> 

<span data-ttu-id="6fb83-150">*Comment modifier les ressources d’Application Insights différent toosending tooa ?*</span><span class="sxs-lookup"><span data-stu-id="6fb83-150">*How do I switch toosending tooa different Application Insights resource?*</span></span>

* <span data-ttu-id="6fb83-151">Dans le projet Visual Studio, avec le bouton hello, choisissez **configurer Application Insights** et choisissez la ressource hello souhaitée.</span><span class="sxs-lookup"><span data-stu-id="6fb83-151">In Visual Studio, right-click hello project, choose **Configure Application Insights** and choose hello resource you want.</span></span> <span data-ttu-id="6fb83-152">Vous obtenez hello option toocreate une nouvelle ressource.</span><span class="sxs-lookup"><span data-stu-id="6fb83-152">You get hello option toocreate a new resource.</span></span> <span data-ttu-id="6fb83-153">Procédez maintenant à la régénération et au redéploiement.</span><span class="sxs-lookup"><span data-stu-id="6fb83-153">Rebuild and redeploy.</span></span>

## <a name="explore-hello-data"></a><span data-ttu-id="6fb83-154">Explorer les données de hello</span><span class="sxs-lookup"><span data-stu-id="6fb83-154">Explore hello data</span></span>
1. <span data-ttu-id="6fb83-155">Sur le panneau d’Application Insights hello de votre Panneau de configuration web app, vous voyez des mesures en direct, qui affiche le nombre d’échecs et les demandes au sein d’une seconde ou deux d'entre eux qui se produisent.</span><span class="sxs-lookup"><span data-stu-id="6fb83-155">On hello Application Insights blade of your web app control panel, you see Live Metrics, which shows requests and failures within a second or two of them occurring.</span></span> <span data-ttu-id="6fb83-156">L’affichage de ces informations est très utile lorsque vous republiez votre application. Vous pouvez voir immédiatement les problèmes.</span><span class="sxs-lookup"><span data-stu-id="6fb83-156">It's very useful display when you're republishing your app - you can see any problems immediately.</span></span>
2. <span data-ttu-id="6fb83-157">Cliquez sur les ressources Application Insights complet toohello.</span><span class="sxs-lookup"><span data-stu-id="6fb83-157">Click through toohello full Application Insights resource.</span></span>

    ![Cliquez sur](./media/app-insights-azure-web-apps/view-in-application-insights.png)

    <span data-ttu-id="6fb83-159">Vous pouvez également y accéder directement à partir de la navigation dans les ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="6fb83-159">You can also go there either directly from Azure resource navigation.</span></span>

1. <span data-ttu-id="6fb83-160">Cliquez sur n’importe quel tooget graphique plus en détail :</span><span class="sxs-lookup"><span data-stu-id="6fb83-160">Click through any chart tooget more detail:</span></span>
   
    ![Dans Panneau de vue d’ensemble hello Application Insights, cliquez sur un graphique](./media/app-insights-azure-web-apps/07-dependency.png)
   
    <span data-ttu-id="6fb83-162">Vous pouvez [personnaliser les panneaux de mesures](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="6fb83-162">You can [customize metrics blades](app-insights-metrics-explorer.md).</span></span>
2. <span data-ttu-id="6fb83-163">Parcourez les plus toosee des événements individuels et leurs propriétés :</span><span class="sxs-lookup"><span data-stu-id="6fb83-163">Click through further toosee individual events and their properties:</span></span>
   
    ![Cliquez sur un tooopen de type d’événement filtrée par une recherche sur ce type](./media/app-insights-azure-web-apps/08-requests.png)
   
    <span data-ttu-id="6fb83-165">Notez que hello tooopen du lien «... » toutes les propriétés.</span><span class="sxs-lookup"><span data-stu-id="6fb83-165">Notice hello "..." link tooopen all properties.</span></span>
   
    <span data-ttu-id="6fb83-166">Vous pouvez [personnaliser les recherches](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="6fb83-166">You can [customize searches](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="6fb83-167">Pour les recherches plus puissantes sur vos données de télémétrie, utilisez hello [de langage de requête Analytique de journal](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="6fb83-167">For more powerful searches over your telemetry, use hello [Log Analytics query language](app-insights-analytics-tour.md).</span></span>

## <a name="more-telemetry"></a><span data-ttu-id="6fb83-168">Données de télémétrie supplémentaires</span><span class="sxs-lookup"><span data-stu-id="6fb83-168">More telemetry</span></span>

* [<span data-ttu-id="6fb83-169">Données de chargement de pages web</span><span class="sxs-lookup"><span data-stu-id="6fb83-169">Web page load data</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="6fb83-170">Télémétrie personnalisée</span><span class="sxs-lookup"><span data-stu-id="6fb83-170">Custom telemetry</span></span>](app-insights-api-custom-events-metrics.md)

## <a name="video"></a><span data-ttu-id="6fb83-171">Vidéo</span><span class="sxs-lookup"><span data-stu-id="6fb83-171">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="6fb83-172">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6fb83-172">Next steps</span></span>
* <span data-ttu-id="6fb83-173">[Exécuter le Générateur de profils hello sur votre application en temps réel](app-insights-profiler.md).</span><span class="sxs-lookup"><span data-stu-id="6fb83-173">[Run hello profiler on your live app](app-insights-profiler.md).</span></span>
* <span data-ttu-id="6fb83-174">[Azure Functions](https://github.com/christopheranderson/azure-functions-app-insights-sample) - analyse les fonctions Azure avec Application Insights</span><span class="sxs-lookup"><span data-stu-id="6fb83-174">[Azure Functions](https://github.com/christopheranderson/azure-functions-app-insights-sample) - monitor Azure Functions with Application Insights</span></span>
* <span data-ttu-id="6fb83-175">[Activer les diagnostics Azure](app-insights-azure-diagnostics.md) toobe envoyé tooApplication Insights.</span><span class="sxs-lookup"><span data-stu-id="6fb83-175">[Enable Azure diagnostics](app-insights-azure-diagnostics.md) toobe sent tooApplication Insights.</span></span>
* <span data-ttu-id="6fb83-176">[Surveiller les mesures de contrôle d’intégrité de service](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) toomake que votre service est disponible et réactive.</span><span class="sxs-lookup"><span data-stu-id="6fb83-176">[Monitor service health metrics](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) toomake sure your service is available and responsive.</span></span>
* <span data-ttu-id="6fb83-177">[Réceptions de notifications d’alerte](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) lorsque des événements opérationnels se produisent ou que des mesures dépassent un seuil.</span><span class="sxs-lookup"><span data-stu-id="6fb83-177">[Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) whenever operational events happen or metrics cross a threshold.</span></span>
* <span data-ttu-id="6fb83-178">Utilisez [Application Insights pour les applications JavaScript avec des pages web](app-insights-javascript.md) télémétrie de client tooget à partir de navigateurs hello visiter une page web.</span><span class="sxs-lookup"><span data-stu-id="6fb83-178">Use [Application Insights for JavaScript apps and web pages](app-insights-javascript.md) tooget client telemetry from hello browsers that visit a web page.</span></span>
* <span data-ttu-id="6fb83-179">[Configurer des tests web de disponibilité](app-insights-monitor-web-app-availability.md) toobe alerté si votre site est arrêté.</span><span class="sxs-lookup"><span data-stu-id="6fb83-179">[Set up Availability web tests](app-insights-monitor-web-app-availability.md) toobe alerted if your site is down.</span></span>

