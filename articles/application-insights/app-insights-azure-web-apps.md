---
title: "Surveillance des performances d’application web Azure | Microsoft Docs"
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
ms.openlocfilehash: f2bbadfbcb93873ed910aeff050bd6896e2e8fec
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-azure-web-app-performance"></a><span data-ttu-id="8d9e4-104">Surveillance des performances d'application web Azure</span><span class="sxs-lookup"><span data-stu-id="8d9e4-104">Monitor Azure web app performance</span></span>
<span data-ttu-id="8d9e4-105">Dans le [portail Azure](https://portal.azure.com), vous pouvez configurer la surveillance des performances d’application pour vos [applications web Azure](../app-service-web/app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8d9e4-105">In the [Azure Portal](https://portal.azure.com) you can set up application performance monitoring for your [Azure web apps](../app-service-web/app-service-web-overview.md).</span></span> <span data-ttu-id="8d9e4-106">[Azure Application Insights](app-insights-overview.md) instrumente votre application afin qu’elle envoie des données de télémétrie concernant ses activités au service Application Insights, où elles sont stockées et analysées.</span><span class="sxs-lookup"><span data-stu-id="8d9e4-106">[Azure Application Insights](app-insights-overview.md) instruments your app to send telemetry about its activities to the Application Insights service, where it is stored and analyzed.</span></span> <span data-ttu-id="8d9e4-107">Les graphiques de mesure et les outils de recherche peuvent alors être utilisés pour aider à diagnostiquer les problèmes, améliorer les performances et évaluer l’utilisation.</span><span class="sxs-lookup"><span data-stu-id="8d9e4-107">There, metric charts and search tools can be used to help diagnose issues, improve performance, and assess usage.</span></span>

## <a name="run-time-or-build-time"></a><span data-ttu-id="8d9e4-108">En cours d’exécution ou en cours de création</span><span class="sxs-lookup"><span data-stu-id="8d9e4-108">Run time or build time</span></span>
<span data-ttu-id="8d9e4-109">Vous pouvez configurer la surveillance par l’instrumentation de l’application de deux manières :</span><span class="sxs-lookup"><span data-stu-id="8d9e4-109">You can configure monitoring by instrumenting the app in either of two ways:</span></span>

* <span data-ttu-id="8d9e4-110">**En cours d’exécution** : vous pouvez sélectionner une extension de surveillance des performances lorsque votre application est déjà active.</span><span class="sxs-lookup"><span data-stu-id="8d9e4-110">**Run-time** - You can select a performance monitoring extension when your web app is already live.</span></span> <span data-ttu-id="8d9e4-111">Il n’est pas nécessaire de reconstruire ou de réinstaller votre application.</span><span class="sxs-lookup"><span data-stu-id="8d9e4-111">It isn't necessary to rebuild or re-install your app.</span></span> <span data-ttu-id="8d9e4-112">Vous obtenez un ensemble standard de packages qui analyse les temps de réponse, les taux de réussite, les exceptions, les dépendances, etc.</span><span class="sxs-lookup"><span data-stu-id="8d9e4-112">You get a standard set of packages that monitor response times, success rates, exceptions, dependencies, and so on.</span></span> 
* <span data-ttu-id="8d9e4-113">**En cours de création** : vous pouvez installer un package dans votre application en cours de développement.</span><span class="sxs-lookup"><span data-stu-id="8d9e4-113">**Build time** - You can install a package in your app in development.</span></span> <span data-ttu-id="8d9e4-114">Cette option est plus souple.</span><span class="sxs-lookup"><span data-stu-id="8d9e4-114">This option is more versatile.</span></span> <span data-ttu-id="8d9e4-115">Outre les mêmes packages standard, vous pouvez écrire du code pour personnaliser les données de télémétrie ou pour envoyer vos propres données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="8d9e4-115">In addition to the same standard packages, you can write code to customize the telemetry or to send your own telemetry.</span></span> <span data-ttu-id="8d9e4-116">Vous pouvez consigner des activités spécifiques ou enregistrer les événements en fonction de la sémantique de votre domaine d’application.</span><span class="sxs-lookup"><span data-stu-id="8d9e4-116">You can log specific activities or record events according to the semantics of your app domain.</span></span> 

## <a name="run-time-instrumentation-with-application-insights"></a><span data-ttu-id="8d9e4-117">Instrumentation d’exécution avec Application Insights</span><span class="sxs-lookup"><span data-stu-id="8d9e4-117">Run time instrumentation with Application Insights</span></span>
<span data-ttu-id="8d9e4-118">Si vous exécutez déjà une application web dans Azure, vous obtenez déjà certains éléments de surveillance, tels que le taux de demande et d’erreur.</span><span class="sxs-lookup"><span data-stu-id="8d9e4-118">If you're already running a web app in Azure, you already get some monitoring: request and error rates.</span></span> <span data-ttu-id="8d9e4-119">Ajoutez Application Insights pour bénéficier d’un plus grand nombre de fonctionnalités, telles que les temps de réponse, la surveillance des appels vers les dépendances, la détection intelligente et le puissant langage de requête Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="8d9e4-119">Add Application Insights to get more, such as response times, monitoring calls to dependencies, smart detection, and the powerful Log Analytics query language.</span></span> 

1. <span data-ttu-id="8d9e4-120">**Sélectionnez Application Insights** dans le panneau de configuration Azure pour votre application web.</span><span class="sxs-lookup"><span data-stu-id="8d9e4-120">**Select Application Insights** in the Azure control panel for your web app.</span></span>
   
    ![Sous Surveillance, choisissez Application Insights](./media/app-insights-azure-web-apps/05-extend.png)
   
   * <span data-ttu-id="8d9e4-122">Choisissez de créer une nouvelle ressource, sauf si vous avez déjà configuré une ressource Application Insights pour cette application par un autre itinéraire.</span><span class="sxs-lookup"><span data-stu-id="8d9e4-122">Choose to create a new resource, unless you already set up an Application Insights resource for this app by another route.</span></span>
2. <span data-ttu-id="8d9e4-123">**Instrumentez votre application web** après l’installation d’Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8d9e4-123">**Instrument your web app** after Application Insights has been installed.</span></span> 
   
    ![Instrumenter votre application web](./media/app-insights-azure-web-apps/restart-web-app-for-insights.png)

   <span data-ttu-id="8d9e4-125">**Activer l’analyse côté client** pour la consultation de page et la télémétrie de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8d9e4-125">**Enable client side monitoring** for page view and user telemetry.</span></span>

   * <span data-ttu-id="8d9e4-126">Cliquez sur Paramètres > Paramètres de l’application</span><span class="sxs-lookup"><span data-stu-id="8d9e4-126">Select Settings > Application Settings</span></span>
   * <span data-ttu-id="8d9e4-127">Sous Paramètres de l’application, ajoutez une nouvelle paire clé/valeur :</span><span class="sxs-lookup"><span data-stu-id="8d9e4-127">Under App Settings, add a new key value pair:</span></span> 
   
    <span data-ttu-id="8d9e4-128">Clé :`APPINSIGHTS_JAVASCRIPT_ENABLED`</span><span class="sxs-lookup"><span data-stu-id="8d9e4-128">Key: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span></span> 
    
    <span data-ttu-id="8d9e4-129">Valeur: `true`</span><span class="sxs-lookup"><span data-stu-id="8d9e4-129">Value: `true`</span></span>
   * <span data-ttu-id="8d9e4-130">**Enregistrez** les paramètres et **Redémarrez** votre application.</span><span class="sxs-lookup"><span data-stu-id="8d9e4-130">**Save** the settings and **Restart** your app.</span></span>
3. <span data-ttu-id="8d9e4-131">**Surveillez votre application web**.</span><span class="sxs-lookup"><span data-stu-id="8d9e4-131">**Monitor your app**.</span></span>  <span data-ttu-id="8d9e4-132">[Explorez les données](#explore-the-data).</span><span class="sxs-lookup"><span data-stu-id="8d9e4-132">[Expore the data](#explore-the-data).</span></span>

<span data-ttu-id="8d9e4-133">Par la suite, vous pourrez, si vous le souhaitez, générer l’application avec Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8d9e4-133">Later, you can build the app with Application Insights if you want.</span></span>

<span data-ttu-id="8d9e4-134">*Comment supprimer Application Insights, ou basculer vers l’envoi vers une autre ressource ?*</span><span class="sxs-lookup"><span data-stu-id="8d9e4-134">*How do I remove Application Insights, or switch to sending to another resource?*</span></span>

* <span data-ttu-id="8d9e4-135">Dans Azure, ouvrez le panneau de contrôle de l’application web, puis sous Outils, ouvrez **Extensions**.</span><span class="sxs-lookup"><span data-stu-id="8d9e4-135">In Azure, open the web app control blade, and under Development Tools, open **Extensions**.</span></span> <span data-ttu-id="8d9e4-136">Supprimez l’extension Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8d9e4-136">Delete the Application Insights extension.</span></span> <span data-ttu-id="8d9e4-137">Puis sous Surveillance, sélectionnez Application Insights et créez ou sélectionnez la ressource souhaitée.</span><span class="sxs-lookup"><span data-stu-id="8d9e4-137">Then under Monitoring, choose Application Insights and create or select the resource you want.</span></span>

## <a name="build-the-app-with-application-insights"></a><span data-ttu-id="8d9e4-138">Générez l’application avec Application Insights</span><span class="sxs-lookup"><span data-stu-id="8d9e4-138">Build the app with Application Insights</span></span>
<span data-ttu-id="8d9e4-139">Application Insights peut fournir des données de télémétrie détaillée par l’installation d’un SDK dans votre application.</span><span class="sxs-lookup"><span data-stu-id="8d9e4-139">Application Insights can provide more detailed telemetry by installing an SDK into your app.</span></span> <span data-ttu-id="8d9e4-140">En particulier, vous pouvez collecter les journaux de suivi, [écrire une télémétrie personnalisée](app-insights-api-custom-events-metrics.md), et obtenir des rapports d’exception plus détaillées.</span><span class="sxs-lookup"><span data-stu-id="8d9e4-140">In particular, you can collect trace logs, [write custom telemetry](app-insights-api-custom-events-metrics.md), and get more detailed exception reports.</span></span>

1. <span data-ttu-id="8d9e4-141">**Dans Visual Studio** (2013 mise à jour 2 ou ultérieure), configurez Application Insights pour votre projet.</span><span class="sxs-lookup"><span data-stu-id="8d9e4-141">**In Visual Studio** (2013 update 2 or later), configure Application Insights for your project.</span></span>

    <span data-ttu-id="8d9e4-142">Cliquez avec le bouton droit sur le projet web et sélectionnez **Ajouter > Application Insights** ou **Configurer Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="8d9e4-142">Right-click the web project, and select **Add > Application Insights** or **Configure Application Insights**.</span></span>
   
    ![Cliquez avec le bouton droit sur le projet web et sélectionnez Ajouter ou Configurer Application Insights.](./media/app-insights-azure-web-apps/03-add.png)
   
    <span data-ttu-id="8d9e4-144">Si vous êtes invité à vous connecter, utilisez les informations d'identification de votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="8d9e4-144">If you're asked to sign in, use the credentials for your Azure account.</span></span>
   
    <span data-ttu-id="8d9e4-145">Cette opération a deux effets :</span><span class="sxs-lookup"><span data-stu-id="8d9e4-145">The operation has two effects:</span></span>
   
   1. <span data-ttu-id="8d9e4-146">Création d’une ressource Application Insights dans Azure, à l’endroit où vos données de télémétrie sont stockées, analysées et affichées.</span><span class="sxs-lookup"><span data-stu-id="8d9e4-146">Creates an Application Insights resource in Azure, where telemetry is stored, analyzed and displayed.</span></span>
   2. <span data-ttu-id="8d9e4-147">Ajout du package NuGet Application Insights à votre code (si ce n’est pas déjà fait), et configuration du package pour l’envoi de données de télémétrie à la ressource Azure.</span><span class="sxs-lookup"><span data-stu-id="8d9e4-147">Adds the Application Insights NuGet package to your code (if it isn't there already), and configures it to send telemetry to the Azure resource.</span></span>
2. <span data-ttu-id="8d9e4-148">**Testez la télémétrie** en exécutant l’application sur votre ordinateur de développement (F5).</span><span class="sxs-lookup"><span data-stu-id="8d9e4-148">**Test the telemetry** by running the app in your development machine (F5).</span></span>
3. <span data-ttu-id="8d9e4-149">**Publiez l’application** sur Azure comme d’habitude.</span><span class="sxs-lookup"><span data-stu-id="8d9e4-149">**Publish the app** to Azure in the usual way.</span></span> 

<span data-ttu-id="8d9e4-150">*Comment modifier la configuration pour envoyer des données vers une autre ressource Application Insights ?*</span><span class="sxs-lookup"><span data-stu-id="8d9e4-150">*How do I switch to sending to a different Application Insights resource?*</span></span>

* <span data-ttu-id="8d9e4-151">Dans Visual Studio, cliquez avec le bouton droit sur le projet, choisissez **Configurer Application Insights** et sélectionnez la ressource de votre choix.</span><span class="sxs-lookup"><span data-stu-id="8d9e4-151">In Visual Studio, right-click the project, choose **Configure Application Insights** and choose the resource you want.</span></span> <span data-ttu-id="8d9e4-152">Vous avez la possibilité de créer une nouvelle ressource.</span><span class="sxs-lookup"><span data-stu-id="8d9e4-152">You get the option to create a new resource.</span></span> <span data-ttu-id="8d9e4-153">Procédez maintenant à la régénération et au redéploiement.</span><span class="sxs-lookup"><span data-stu-id="8d9e4-153">Rebuild and redeploy.</span></span>

## <a name="explore-the-data"></a><span data-ttu-id="8d9e4-154">Exploration des données</span><span class="sxs-lookup"><span data-stu-id="8d9e4-154">Explore the data</span></span>
1. <span data-ttu-id="8d9e4-155">Dans le panneau Application Insights du panneau de configuration de l’application web, des mesures actives, indiquant les demandes et les échecs ou les deux survenant au cours d’une seconde, s’affichent.</span><span class="sxs-lookup"><span data-stu-id="8d9e4-155">On the Application Insights blade of your web app control panel, you see Live Metrics, which shows requests and failures within a second or two of them occurring.</span></span> <span data-ttu-id="8d9e4-156">L’affichage de ces informations est très utile lorsque vous republiez votre application. Vous pouvez voir immédiatement les problèmes.</span><span class="sxs-lookup"><span data-stu-id="8d9e4-156">It's very useful display when you're republishing your app - you can see any problems immediately.</span></span>
2. <span data-ttu-id="8d9e4-157">Cliquez sur la ressource Application Insights complète.</span><span class="sxs-lookup"><span data-stu-id="8d9e4-157">Click through to the full Application Insights resource.</span></span>

    ![Cliquez sur](./media/app-insights-azure-web-apps/view-in-application-insights.png)

    <span data-ttu-id="8d9e4-159">Vous pouvez également y accéder directement à partir de la navigation dans les ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="8d9e4-159">You can also go there either directly from Azure resource navigation.</span></span>

1. <span data-ttu-id="8d9e4-160">Cliquez sur n’importe quel graphique pour afficher plus de détails :</span><span class="sxs-lookup"><span data-stu-id="8d9e4-160">Click through any chart to get more detail:</span></span>
   
    ![Dans le panneau de vue d’ensemble d’Application Insights, cliquez sur un graphique](./media/app-insights-azure-web-apps/07-dependency.png)
   
    <span data-ttu-id="8d9e4-162">Vous pouvez [personnaliser les panneaux de mesures](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="8d9e4-162">You can [customize metrics blades](app-insights-metrics-explorer.md).</span></span>
2. <span data-ttu-id="8d9e4-163">Cliquez de nouveau pour afficher des événements ainsi que leurs propriétés :</span><span class="sxs-lookup"><span data-stu-id="8d9e4-163">Click through further to see individual events and their properties:</span></span>
   
    ![Cliquez sur un type d’événement pour ouvrir une recherche filtrée sur ce type](./media/app-insights-azure-web-apps/08-requests.png)
   
    <span data-ttu-id="8d9e4-165">Notez le lien «...» qui permet d’ouvrir toutes les propriétés.</span><span class="sxs-lookup"><span data-stu-id="8d9e4-165">Notice the "..." link to open all properties.</span></span>
   
    <span data-ttu-id="8d9e4-166">Vous pouvez [personnaliser les recherches](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="8d9e4-166">You can [customize searches](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="8d9e4-167">Pour des recherches plus abouties sur vos données de télémétrie, utilisez le [langage de requête Log Analytics](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="8d9e4-167">For more powerful searches over your telemetry, use the [Log Analytics query language](app-insights-analytics-tour.md).</span></span>

## <a name="more-telemetry"></a><span data-ttu-id="8d9e4-168">Données de télémétrie supplémentaires</span><span class="sxs-lookup"><span data-stu-id="8d9e4-168">More telemetry</span></span>

* [<span data-ttu-id="8d9e4-169">Données de chargement de pages web</span><span class="sxs-lookup"><span data-stu-id="8d9e4-169">Web page load data</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="8d9e4-170">Télémétrie personnalisée</span><span class="sxs-lookup"><span data-stu-id="8d9e4-170">Custom telemetry</span></span>](app-insights-api-custom-events-metrics.md)

## <a name="video"></a><span data-ttu-id="8d9e4-171">Vidéo</span><span class="sxs-lookup"><span data-stu-id="8d9e4-171">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="8d9e4-172">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8d9e4-172">Next steps</span></span>
* <span data-ttu-id="8d9e4-173">[Exécuter le profileur sur une application dynamique](app-insights-profiler.md).</span><span class="sxs-lookup"><span data-stu-id="8d9e4-173">[Run the profiler on your live app](app-insights-profiler.md).</span></span>
* <span data-ttu-id="8d9e4-174">[Azure Functions](https://github.com/christopheranderson/azure-functions-app-insights-sample) - analyse les fonctions Azure avec Application Insights</span><span class="sxs-lookup"><span data-stu-id="8d9e4-174">[Azure Functions](https://github.com/christopheranderson/azure-functions-app-insights-sample) - monitor Azure Functions with Application Insights</span></span>
* <span data-ttu-id="8d9e4-175">[Autorisation de l’envoi de diagnostics Azure](app-insights-azure-diagnostics.md) vers Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8d9e4-175">[Enable Azure diagnostics](app-insights-azure-diagnostics.md) to be sent to Application Insights.</span></span>
* <span data-ttu-id="8d9e4-176">[Analyse des mesures d’intégrité du service](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) pour vous assurer que votre service est disponible et réactif.</span><span class="sxs-lookup"><span data-stu-id="8d9e4-176">[Monitor service health metrics](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) to make sure your service is available and responsive.</span></span>
* <span data-ttu-id="8d9e4-177">[Réceptions de notifications d’alerte](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) lorsque des événements opérationnels se produisent ou que des mesures dépassent un seuil.</span><span class="sxs-lookup"><span data-stu-id="8d9e4-177">[Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) whenever operational events happen or metrics cross a threshold.</span></span>
* <span data-ttu-id="8d9e4-178">Utilisation [d’Application Insights pour les pages Web et les applications JavaScript](app-insights-javascript.md) pour obtenir les données de télémétrie du client à partir des navigateurs qui consultent une page web.</span><span class="sxs-lookup"><span data-stu-id="8d9e4-178">Use [Application Insights for JavaScript apps and web pages](app-insights-javascript.md) to get client telemetry from the browsers that visit a web page.</span></span>
* <span data-ttu-id="8d9e4-179">[Configuration des tests de disponibilité web](app-insights-monitor-web-app-availability.md) , pour recevoir des alertes en cas d’interruption de votre site.</span><span class="sxs-lookup"><span data-stu-id="8d9e4-179">[Set up Availability web tests](app-insights-monitor-web-app-availability.md) to be alerted if your site is down.</span></span>

