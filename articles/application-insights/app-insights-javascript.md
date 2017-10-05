---
title: Azure Application Insights pour les applications web JavaScript | Microsoft Docs
description: "Obtention des décomptes de sessions et d’affichages de pages, des données de client web et suivi des modèles d’utilisation. Détection des problèmes de performances et des exceptions dans les pages Web JavaScript."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 3b710d09-6ab4-4004-b26a-4fa840039500
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 4e8a77e3644bb726d1b8e2050dab61893ccfa3c9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="application-insights-for-web-pages"></a><span data-ttu-id="5e4fe-104">Application Insights pour les pages web</span><span class="sxs-lookup"><span data-stu-id="5e4fe-104">Application Insights for web pages</span></span>
<span data-ttu-id="5e4fe-105">Apprenez-en plus sur les performances et l’utilisation de votre page web ou de votre application.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-105">Find out about the performance and usage of your web page or app.</span></span> <span data-ttu-id="5e4fe-106">Ajoutez [Application Insights](app-insights-overview.md) à votre script de page pour obtenir le minutage des chargements de page et des appels AJAX, le nombre d’exceptions du navigateur et d’échecs d’AJAX et leurs détails, ainsi que le nombre d’utilisateurs et de sessions.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-106">If you add [Application Insights](app-insights-overview.md) to your page script, you get timings of page loads and AJAX calls, counts and details of browser exceptions and AJAX failures, as well as users and session counts.</span></span> <span data-ttu-id="5e4fe-107">Toutes ces données peuvent être segmentées par page, par version de système d’exploitation ou de navigateur client, par emplacement géographique et en fonction d’autres aspects.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-107">All these can be segmented by page, client OS and browser version, geo location, and other dimensions.</span></span> <span data-ttu-id="5e4fe-108">Vous pouvez définir des alertes en cas de dépassement d’un certain nombre d’échecs ou de ralentissement du chargement des pages.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-108">You can set alerts on failure counts or slow page loading.</span></span> <span data-ttu-id="5e4fe-109">Et en insérant des suivis d’appel dans votre code JavaScript, vous pouvez suivre l’utilisation des différentes fonctionnalités de votre application de page web.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-109">And by inserting trace calls in your JavaScript code, you can track how the different features of your web page application are used.</span></span>

<span data-ttu-id="5e4fe-110">Vous pouvez utiliser Application Insights avec toutes les pages web ; il vous suffit pour cela d’ajouter un court extrait de code JavaScript.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-110">Application Insights can be used with any web pages - you just add a short piece of JavaScript.</span></span> <span data-ttu-id="5e4fe-111">Si votre service web est [Java](app-insights-java-get-started.md) ou [ASP.NET](app-insights-asp-net.md), vous pouvez intégrer les données de télémétrie de votre serveur et de vos clients.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-111">If your web service is [Java](app-insights-java-get-started.md) or [ASP.NET](app-insights-asp-net.md), you can integrate telemetry from your server and clients.</span></span>

![Dans portal.azure.com, ouvrez les ressources de votre application, puis cliquez sur Navigateur](./media/app-insights-javascript/03.png)

<span data-ttu-id="5e4fe-113">Vous devrez vous abonner à [Microsoft Azure](https://azure.com).</span><span class="sxs-lookup"><span data-stu-id="5e4fe-113">You need a subscription to [Microsoft Azure](https://azure.com).</span></span> <span data-ttu-id="5e4fe-114">Si votre équipe dispose d’un abonnement d’organisation, demandez à son propriétaire d’y ajouter votre compte Microsoft.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-114">If your team has an organizational subscription, ask the owner to add your Microsoft Account to it.</span></span> <span data-ttu-id="5e4fe-115">Le développement et l’utilisation à petite échelle ne coûtent rien.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-115">Development and small-scale use won't cost anything.</span></span>

## <a name="set-up-application-insights-for-your-web-page"></a><span data-ttu-id="5e4fe-116">Configurer Application Insights pour votre page web</span><span class="sxs-lookup"><span data-stu-id="5e4fe-116">Set up Application Insights for your web page</span></span>
<span data-ttu-id="5e4fe-117">Ajoutez l’extrait de code de chargeur à vos pages web, comme suit.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-117">Add the loader code snippet to your web pages, as follows.</span></span>

### <a name="open-or-create-application-insights-resource"></a><span data-ttu-id="5e4fe-118">Ouverture ou création d’une ressource Application Insights dans Azure</span><span class="sxs-lookup"><span data-stu-id="5e4fe-118">Open or create Application Insights resource</span></span>
<span data-ttu-id="5e4fe-119">La ressource Application Insights est l’endroit où les données de performance et d’utilisation de votre page s’affichent.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-119">The Application Insights resource is where data about your page's performance and usage is displayed.</span></span> 

<span data-ttu-id="5e4fe-120">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5e4fe-120">Sign into [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="5e4fe-121">Si vous avez déjà défini la surveillance pour le côté serveur de votre application, vous aurez déjà une ressource :</span><span class="sxs-lookup"><span data-stu-id="5e4fe-121">If you already set up monitoring for the server side of your app, you already have a resource:</span></span>

![Cliquez sur Parcourir, Services de développement, Application Insights.](./media/app-insights-javascript/01-find.png)

<span data-ttu-id="5e4fe-123">Si vous n'en avez pas, créez-la.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-123">If you don't have one, create it:</span></span>

![Cliquez sur Nouveau, Services de développement, Application Insights.](./media/app-insights-javascript/01-create.png)

<span data-ttu-id="5e4fe-125">*Vous avez déjà des questions ?*</span><span class="sxs-lookup"><span data-stu-id="5e4fe-125">*Questions already?*</span></span> <span data-ttu-id="5e4fe-126">[Plus d’informations sur la création d’une ressource](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="5e4fe-126">[More about creating a resource](app-insights-create-new-resource.md).</span></span>

### <a name="add-the-sdk-script-to-your-app-or-web-pages"></a><span data-ttu-id="5e4fe-127">Ajoutez le script du Kit de développement logiciel (SDK) à votre application ou vos pages web</span><span class="sxs-lookup"><span data-stu-id="5e4fe-127">Add the SDK script to your app or web pages</span></span>
<span data-ttu-id="5e4fe-128">Dans Démarrage rapide, récupérez le script pour les pages Web :</span><span class="sxs-lookup"><span data-stu-id="5e4fe-128">In Quick Start, get the script for web pages:</span></span>

![Dans le panneau de vue d’ensemble de l’application, cliquez sur Démarrage rapide, Obtenir le code pour analyser mes pages web.](./media/app-insights-javascript/02-monitor-web-page.png)

<span data-ttu-id="5e4fe-131">Insérez-le juste avant la balise `</head>` de chaque page que vous voulez suivre. Si votre site Web possède une page maître, vous pouvez y placer le script.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-131">Insert the script just before the `</head>` tag of every page you want to track. If your website has a master page, you can put the script there.</span></span> <span data-ttu-id="5e4fe-132">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="5e4fe-132">For example:</span></span>

* <span data-ttu-id="5e4fe-133">Dans un projet ASP.NET MVC, vous devez placer le script dans `View\Shared\_Layout.cshtml`</span><span class="sxs-lookup"><span data-stu-id="5e4fe-133">In an ASP.NET MVC project, you'd put it in `View\Shared\_Layout.cshtml`</span></span>
* <span data-ttu-id="5e4fe-134">Dans un site SharePoint, dans le panneau de configuration, ouvrez [Paramètres du site/Page maître](app-insights-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="5e4fe-134">In a SharePoint site, on the control panel, open [Site Settings / Master Page](app-insights-sharepoint.md).</span></span>

<span data-ttu-id="5e4fe-135">Le script contient la clé d’instrumentation qui dirige les données vers votre ressource Application Insights.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-135">The script contains the instrumentation key that directs the data to your Application Insights resource.</span></span> 

<span data-ttu-id="5e4fe-136">([Explication approfondie du script.](http://apmtips.com/blog/2015/03/18/javascript-snippet-explained/))</span><span class="sxs-lookup"><span data-stu-id="5e4fe-136">([Deeper explanation of the script.](http://apmtips.com/blog/2015/03/18/javascript-snippet-explained/))</span></span>

<span data-ttu-id="5e4fe-137">*(Si vous utilisez une infrastructure de page web connue, cherchez des adaptateurs Application Insights. Par exemple, il existe [un module AngularJS](http://ngmodules.org/modules/angular-appinsights).)*</span><span class="sxs-lookup"><span data-stu-id="5e4fe-137">*(If you're using a well-known web page framework, look around for Application Insights adaptors. For example, there's [an AngularJS module](http://ngmodules.org/modules/angular-appinsights).)*</span></span>

## <a name="detailed-configuration"></a><span data-ttu-id="5e4fe-138">Configuration détaillée</span><span class="sxs-lookup"><span data-stu-id="5e4fe-138">Detailed configuration</span></span>
<span data-ttu-id="5e4fe-139">Bien que vous puissiez définir plusieurs [paramètres](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) , vous ne devriez pas avoir besoin de le faire dans la plupart des cas.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-139">There are several [parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) you can set, though in most cases, you shouldn't need to.</span></span> <span data-ttu-id="5e4fe-140">Par exemple, vous pouvez désactiver ou limiter le nombre d’appels Ajax signalés par page vue (afin de réduire le trafic).</span><span class="sxs-lookup"><span data-stu-id="5e4fe-140">For example, you can disable or limit the number of Ajax calls reported per page view (to reduce traffic).</span></span> <span data-ttu-id="5e4fe-141">Sinon, vous pouvez définir le mode de débogage pour que les données de télémétrie transitent rapidement à travers le pipeline sans être traitées par lot.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-141">Or you can set debug mode to have telemetry move rapidly through the pipeline without being batched.</span></span>

<span data-ttu-id="5e4fe-142">Pour définir ces paramètres, recherchez cette ligne dans l’extrait de code et ajoutez des éléments séparés par des virgules à la suite de celle-ci :</span><span class="sxs-lookup"><span data-stu-id="5e4fe-142">To set these parameters, look for this line in the code snippet, and add more comma-separated items after it:</span></span>

    })({
      instrumentationKey: "..."
      // Insert here
    });

<span data-ttu-id="5e4fe-143">Les [paramètres disponibles](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) incluent :</span><span class="sxs-lookup"><span data-stu-id="5e4fe-143">The [available parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) include:</span></span>

    // Send telemetry immediately without batching.
    // Remember to remove this when no longer required, as it
    // can affect browser performance.
    enableDebug: boolean,

    // Don't log browser exceptions.
    disableExceptionTracking: boolean,

    // Don't log ajax calls.
    disableAjaxTracking: boolean,

    // Limit number of Ajax calls logged, to reduce traffic.
    maxAjaxCallsPerView: 10, // default is 500

    // Time page load up to execution of first trackPageView().
    overridePageViewDuration: boolean,

    // Set these dynamically for an authenticated user.
    appUserId: string,
    accountId: string,



## <span data-ttu-id="5e4fe-144"><a name="run"></a>Exécution de votre application</span><span class="sxs-lookup"><span data-stu-id="5e4fe-144"><a name="run"></a>Run your app</span></span>
<span data-ttu-id="5e4fe-145">Exécutez votre application web, utilisez-la un certain temps pour générer de la télémétrie et attendez quelques secondes.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-145">Run your web app, use it a while to generate telemetry, and wait a few seconds.</span></span> <span data-ttu-id="5e4fe-146">Vous pouvez l’exécuter en appuyant sur la touche **F5** de votre machine de développement, ou la publier et laisser les utilisateurs s’en servir.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-146">You can either run it using the **F5** key on your development machine, or publish it and let users play with it.</span></span>

<span data-ttu-id="5e4fe-147">Si vous souhaitez vérifier la télémétrie qu’une application web envoie à Application Insights, utilisez les outils de débogage de votre navigateur (**F12** sur de nombreux navigateurs).</span><span class="sxs-lookup"><span data-stu-id="5e4fe-147">If you want to check the telemetry that a web app is sending to Application Insights, use your browser's debugging tools (**F12** on many browsers).</span></span> <span data-ttu-id="5e4fe-148">Les données sont envoyées à dc.services.visualstudio.com.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-148">Data is sent to dc.services.visualstudio.com.</span></span>

## <a name="explore-your-browser-performance-data"></a><span data-ttu-id="5e4fe-149">Exploration de vos données de performances dans les navigateurs</span><span class="sxs-lookup"><span data-stu-id="5e4fe-149">Explore your browser performance data</span></span>
<span data-ttu-id="5e4fe-150">Ouvrez le panneau Navigateurs pour afficher la synthèse des données de performances issues des navigateurs des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-150">Open the Browser blade to show aggregated performance data from your users' browsers.</span></span>

![Dans portal.azure.com, ouvrez les ressources de votre application, puis cliquez sur Paramètres, Navigateur.](./media/app-insights-javascript/03.png)

<span data-ttu-id="5e4fe-152">*Pas de données pour le moment ? Cliquez sur **Actualiser** en haut de la page. Toujours rien ? Consultez la rubrique [Résolution des problèmes](app-insights-troubleshoot-faq.md).*</span><span class="sxs-lookup"><span data-stu-id="5e4fe-152">*No data yet? Click **Refresh** at the top of the page. Still nothing? See [Troubleshooting](app-insights-troubleshoot-faq.md).*</span></span>

<span data-ttu-id="5e4fe-153">Le panneau navigateur est un [Panneau Metrics Explorer](app-insights-metrics-explorer.md) avec filtres prédéfinis et des sélections de graphique.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-153">The Browser blade is a [Metrics Explorer blade](app-insights-metrics-explorer.md) with preset filters and chart selections.</span></span> <span data-ttu-id="5e4fe-154">Si vous le souhaitez, vous pouvez modifier l’intervalle de temps, les filtres et la configuration des graphiques, puis enregistrer le résultat en tant que favori.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-154">You can edit the time range, filters, and chart configuration if you want, and save the result as a favorite.</span></span> <span data-ttu-id="5e4fe-155">Cliquez sur **Paramètres par défaut** pour revenir à la configuration d’origine du panneau.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-155">Click **Restore defaults** to get back to the original blade configuration.</span></span>

## <a name="page-load-performance"></a><span data-ttu-id="5e4fe-156">Performances de chargement des pages</span><span class="sxs-lookup"><span data-stu-id="5e4fe-156">Page load performance</span></span>
<span data-ttu-id="5e4fe-157">Dans la partie supérieure se trouve un graphique segmenté illustrant le temps de chargement des pages.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-157">At the top is a segmented chart of page load times.</span></span> <span data-ttu-id="5e4fe-158">La hauteur totale du graphique représente la durée moyenne nécessaire pour charger et afficher les pages de votre application dans les navigateurs de vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-158">The total height of the chart represents the average time to load and display pages from your app in your users' browsers.</span></span> <span data-ttu-id="5e4fe-159">La durée est mesurée entre le moment où le navigateur envoie la requête HTTP initiale et le moment où tous les événements de chargement synchrones ont été traités, y compris la mise en page et l’exécution des scripts.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-159">The time is measured from when the browser sends the initial HTTP request until all synchronous load events have been processed, including layout and running scripts.</span></span> <span data-ttu-id="5e4fe-160">Elle n’inclut pas les tâches asynchrones telles que le chargement des composants web à partir des appels AJAX.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-160">It doesn't include asynchronous tasks such as loading web parts from AJAX calls.</span></span>

<span data-ttu-id="5e4fe-161">Le graphique segmente le temps de chargement total des pages suivant les [durées standard définies par le consortium W3C](http://www.w3.org/TR/navigation-timing/#processing-model).</span><span class="sxs-lookup"><span data-stu-id="5e4fe-161">The chart segments the total page load time into the [standard timings defined by W3C](http://www.w3.org/TR/navigation-timing/#processing-model).</span></span> 

![](./media/app-insights-javascript/08-client-split.png)

<span data-ttu-id="5e4fe-162">Notez que la durée de *connexion réseau* est souvent plus faible que prévue, car il s’agit d’une moyenne de toutes les demandes du navigateur au serveur.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-162">Note that the *network connect* time is often lower than you might expect, because it's an average over all requests from the browser to the server.</span></span> <span data-ttu-id="5e4fe-163">De nombreuses requêtes individuelles ont un temps de connexion de 0, car il existe déjà une connexion active au serveur.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-163">Many individual requests have a connect time of 0 because there is already an active connection to the server.</span></span>

### <a name="slow-loading"></a><span data-ttu-id="5e4fe-164">Le chargement est lent ?</span><span class="sxs-lookup"><span data-stu-id="5e4fe-164">Slow loading?</span></span>
<span data-ttu-id="5e4fe-165">Les pages qui mettent du temps à se charger constituent une source de mécontentement majeure pour vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-165">Slow page loads are a major source of dissatisfaction for your users.</span></span> <span data-ttu-id="5e4fe-166">Si le graphique indique des chargements de page lents, il est facile de faire des recherches pour diagnostiquer le problème.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-166">If the chart indicates slow page loads, it's easy to do some diagnostic research.</span></span>

<span data-ttu-id="5e4fe-167">Le graphique illustre la moyenne de tous les chargements de page dans votre application.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-167">The chart shows the average of all page loads in your app.</span></span> <span data-ttu-id="5e4fe-168">Pour voir si le problème est limité à certaines pages, regardez plus bas dans le panneau, où vous trouverez une grille segmentée par URL de page :</span><span class="sxs-lookup"><span data-stu-id="5e4fe-168">To see if the problem is confined to particular pages, look further down the blade, where there's a grid segmented by page URL:</span></span>

![](./media/app-insights-javascript/09-page-perf.png)

<span data-ttu-id="5e4fe-169">Observez le nombre d’affichages de page et l’écart type.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-169">Notice the page view count and standard deviation.</span></span> <span data-ttu-id="5e4fe-170">Si le nombre de pages est très faible, alors le problème n’a pas un impact important sur les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-170">If the page count is very low, then the issue isn't affecting users much.</span></span> <span data-ttu-id="5e4fe-171">Un écart type élevé (comparable à la moyenne elle-même) indique une variation considérable entre les mesures individuelles.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-171">A high standard deviation (comparable to the average itself) indicates a lot of variation between individual measurements.</span></span>

<span data-ttu-id="5e4fe-172">**Zoomez sur une URL et un affichage de page.**</span><span class="sxs-lookup"><span data-stu-id="5e4fe-172">**Zoom in on one URL and one page view.**</span></span> <span data-ttu-id="5e4fe-173">Cliquez sur n’importe quel nom de page pour afficher un panneau de graphiques de navigateur filtrés en fonction de cette URL, puis sur une instance d’un affichage de page.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-173">Click any page name to see a blade of browser charts filtered just to that URL; and then on an instance of a page view.</span></span>

![](./media/app-insights-javascript/35.png)

<span data-ttu-id="5e4fe-174">Cliquez sur `...` pour obtenir une liste complète des propriétés de cet événement ou examinez les appels Ajax et les événements associés.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-174">Click `...` for a full list of properties for that event, or inspect the Ajax calls and related events.</span></span> <span data-ttu-id="5e4fe-175">S’ils sont synchrones, les appels Ajax lents ont un impact sur le temps de chargement de l’ensemble de la page.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-175">Slow Ajax calls affect the overall page load time if they are synchronous.</span></span> <span data-ttu-id="5e4fe-176">Les événements associés incluent les requêtes de serveur pour la même URL (si vous avez configuré Application Insights sur votre serveur web).</span><span class="sxs-lookup"><span data-stu-id="5e4fe-176">Related events include server requests for the same URL (if you've set up Application Insights on your web server).</span></span>

<span data-ttu-id="5e4fe-177">**Historique des performances de la page.**</span><span class="sxs-lookup"><span data-stu-id="5e4fe-177">**Page performance over time.**</span></span> <span data-ttu-id="5e4fe-178">Dans le panneau Navigateurs, convertissez la grille Temps de chargement de la page consultée en graphique en courbes pour voir s’il y a des pics à des moments spécifiques :</span><span class="sxs-lookup"><span data-stu-id="5e4fe-178">Back at the Browsers blade, change the Page View Load Time grid into a line chart to see if there were peaks at particular times:</span></span>

![Cliquez sur l’en-tête de la grille et sélectionnez un nouveau type de graphique.](./media/app-insights-javascript/10-page-perf-area.png)

<span data-ttu-id="5e4fe-180">**Segmentation en fonction d’autres aspects.**</span><span class="sxs-lookup"><span data-stu-id="5e4fe-180">**Segment by other dimensions.**</span></span> <span data-ttu-id="5e4fe-181">Vos pages mettent peut-être plus de temps à se charger sur un navigateur ou un système d’exploitation spécifiques, ou encore selon l’emplacement géographique de l’utilisateur ?</span><span class="sxs-lookup"><span data-stu-id="5e4fe-181">Maybe your pages are slower to load on a particular browser, client OS, or user locality?</span></span> <span data-ttu-id="5e4fe-182">Ajoutez un nouveau graphique et faites des essais avec l’option **Grouper par** .</span><span class="sxs-lookup"><span data-stu-id="5e4fe-182">Add a new chart and experiment with the **Group-by** dimension.</span></span>

![](./media/app-insights-javascript/21.png)

## <a name="ajax-performance"></a><span data-ttu-id="5e4fe-183">Performances AJAX</span><span class="sxs-lookup"><span data-stu-id="5e4fe-183">AJAX Performance</span></span>
<span data-ttu-id="5e4fe-184">Assurez-vous que tous les appels AJAX dans vos pages web fonctionnent correctement.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-184">Make sure any AJAX calls in your web pages are performing well.</span></span> <span data-ttu-id="5e4fe-185">Ils sont souvent utilisés pour remplir des parties de votre page de façon asynchrone.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-185">They are often used to fill parts of your page asynchronously.</span></span> <span data-ttu-id="5e4fe-186">Même si l’ensemble de la page se charge rapidement, vos utilisateurs pourraient être frustrés d’avoir à attendre que les données apparaissent dans des parties vides de la page.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-186">Although the overall page might load promptly, your users could be frustrated by staring at blank web parts, waiting for data to appear in them.</span></span>

<span data-ttu-id="5e4fe-187">Les appels AJAX effectués à partir de votre page web sont affichés dans le panneau Navigateurs en tant que dépendances.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-187">AJAX calls made from your web page are shown on the Browsers blade as dependencies.</span></span>

<span data-ttu-id="5e4fe-188">Vous trouverez des graphiques récapitulatifs dans la partie supérieure du panneau :</span><span class="sxs-lookup"><span data-stu-id="5e4fe-188">There are summary charts in the upper part of the blade:</span></span>

![](./media/app-insights-javascript/31.png)

<span data-ttu-id="5e4fe-189">et des grilles détaillées plus bas :</span><span class="sxs-lookup"><span data-stu-id="5e4fe-189">and detailed grids lower down:</span></span>

![](./media/app-insights-javascript/33.png)

<span data-ttu-id="5e4fe-190">Cliquez sur n’importe quelle ligne pour obtenir des détails spécifiques.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-190">Click any row for specific details.</span></span>

> [!NOTE]
> <span data-ttu-id="5e4fe-191">Si vous supprimez le filtre Navigateurs du panneau, les dépendances de serveur et AJAX figureront dans ces graphiques.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-191">If you delete the Browsers filter on the blade, both server and AJAX dependencies are included in these charts.</span></span> <span data-ttu-id="5e4fe-192">Cliquez sur Paramètres par défaut pour reconfigurer le filtre.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-192">Click Restore Defaults to reconfigure the filter.</span></span>
> 
> 

<span data-ttu-id="5e4fe-193">**Pour explorer les appels Ajax ayant échoué** , faites défiler l’écran jusqu’à la grille Échecs de dépendance, puis cliquez sur une ligne afin d’afficher des instances spécifiques.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-193">**To drill into failed Ajax calls** scroll down to the Dependency failures grid, and then click a row to see specific instances.</span></span>

![](./media/app-insights-javascript/37.png)


<span data-ttu-id="5e4fe-194">Cliquez sur `...` pour obtenir les données de télémétrie complètes d’un appel Ajax.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-194">Click `...` for the full telemetry for an Ajax call.</span></span>

### <a name="no-ajax-calls-reported"></a><span data-ttu-id="5e4fe-195">Aucun appel Ajax n’est signalé ?</span><span class="sxs-lookup"><span data-stu-id="5e4fe-195">No Ajax calls reported?</span></span>
<span data-ttu-id="5e4fe-196">Les appels AJAX incluent tous les appels HTTP/HTTPS effectués à partir du script de votre page web.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-196">Ajax calls include any HTTP/HTTPS  calls made from the script of your web page.</span></span> <span data-ttu-id="5e4fe-197">S’ils ne sont pas signalés, vérifiez que l’extrait de code ne définit pas les [paramètres](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) `disableAjaxTracking` ou `maxAjaxCallsPerView`.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-197">If you don't see them reported, check that the code snippet doesn't set the `disableAjaxTracking` or `maxAjaxCallsPerView` [parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span></span>

## <a name="browser-exceptions"></a><span data-ttu-id="5e4fe-198">Exceptions du navigateur</span><span class="sxs-lookup"><span data-stu-id="5e4fe-198">Browser exceptions</span></span>
<span data-ttu-id="5e4fe-199">Le panneau Navigateurs présente un graphique récapitulatif des exceptions, ainsi qu’une grille des types d’exception plus bas.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-199">On the Browsers blade, there's an exceptions summary chart, and a grid of exception types further down the blade.</span></span>

![](./media/app-insights-javascript/39.png)

<span data-ttu-id="5e4fe-200">Si les exceptions de navigateur ne sont pas signalées, vérifiez que l’extrait de code ne définit pas le [paramètre](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) `disableExceptionTracking`.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-200">If you don't see browser exceptions reported, check that the code snippet doesn't set the `disableExceptionTracking` [parameter](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span></span>

## <a name="inspect-individual-page-view-events"></a><span data-ttu-id="5e4fe-201">Inspection des événements d’affichage de page individuels</span><span class="sxs-lookup"><span data-stu-id="5e4fe-201">Inspect individual page view events</span></span>

<span data-ttu-id="5e4fe-202">La télémétrie de l'affichage de page est généralement analysée par Application Insights, et vous ne consultez que des rapports cumulés, avec une moyenne entre tous les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-202">Usually page view telemetry is analyzed by Application Insights and you see only cumulative reports, averaged over all your users.</span></span> <span data-ttu-id="5e4fe-203">Toutefois, à des fins de débogage, vous pouvez également consulter des événements d'affichage de page individuels.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-203">But for debugging purposes, you can also look at individual page view events.</span></span>

<span data-ttu-id="5e4fe-204">Dans le volet Recherche de diagnostic, définissez Filtres sur Affichage de page.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-204">In the Diagnostic Search blade, set Filters to Page View.</span></span>

![](./media/app-insights-javascript/12-search-pages.png)

<span data-ttu-id="5e4fe-205">Sélectionnez n'importe quel événement pour afficher plus de détails.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-205">Select any event to see more detail.</span></span> <span data-ttu-id="5e4fe-206">Dans la page des détails, cliquez sur «... » pour voir davantage de détails.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-206">In the details page, click "..." to see even more detail.</span></span>

> [!NOTE]
> <span data-ttu-id="5e4fe-207">Si vous utilisez [Rechercher](app-insights-diagnostic-search.md), notez que vous devez faire correspondre les mots entiers : « à propo » et « propos » ne correspondent pas à « À propos ».</span><span class="sxs-lookup"><span data-stu-id="5e4fe-207">If you use [Search](app-insights-diagnostic-search.md), notice that you have to match whole words: "Abou" and "bout" do not match "About".</span></span>
> 
> 

<span data-ttu-id="5e4fe-208">Vous pouvez également utiliser le puissant [langage de requête Log Analytics](https://docs.microsoft.com/azure/application-insights/app-insights-analytics-tour#browser-timings-table) pour effectuer des recherches dans les vues de pages.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-208">You can also use the powerful [Log Analytics query language](https://docs.microsoft.com/azure/application-insights/app-insights-analytics-tour#browser-timings-table) to search page views.</span></span>

### <a name="page-view-properties"></a><span data-ttu-id="5e4fe-209">Propriétés d'affichage de la page</span><span class="sxs-lookup"><span data-stu-id="5e4fe-209">Page view properties</span></span>
* <span data-ttu-id="5e4fe-210">**Durée d’affichage de la page**</span><span class="sxs-lookup"><span data-stu-id="5e4fe-210">**Page view duration**</span></span> 
  
  * <span data-ttu-id="5e4fe-211">Par défaut, le temps nécessaire au chargement de la page, depuis la requête du client jusqu’à son chargement complet (y compris les fichiers auxiliaires, mais à l’exception des tâches asynchrones telles que les appels Ajax).</span><span class="sxs-lookup"><span data-stu-id="5e4fe-211">By default, the time it takes to load the page, from client request to full load (including auxiliary files but excluding asynchronous tasks such as Ajax calls).</span></span> 
  * <span data-ttu-id="5e4fe-212">Si vous définissez `overridePageViewDuration` dans la [configuration de la page](#detailed-configuration), il s’agit de l’intervalle entre la requête du client et l’exécution du premier `trackPageView`.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-212">If you set `overridePageViewDuration` in the [page configuration](#detailed-configuration), the interval between client request to execution of the first `trackPageView`.</span></span> <span data-ttu-id="5e4fe-213">Si vous avez déplacé trackPageView de sa position habituelle après l'initialisation du script, il affiche une autre valeur.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-213">If you moved trackPageView from its usual position after the initialization of the script, it will reflect a different value.</span></span>
  * <span data-ttu-id="5e4fe-214">Si `overridePageViewDuration` est défini et qu’un argument Duration est fourni dans l’appel `trackPageView()`, la valeur d’argument sera utilisée à la place.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-214">If `overridePageViewDuration` is set and a duration argument is provided in the `trackPageView()` call, then the argument value is used instead.</span></span> 

## <a name="custom-page-counts"></a><span data-ttu-id="5e4fe-215">Compteurs de page personnalisés</span><span class="sxs-lookup"><span data-stu-id="5e4fe-215">Custom page counts</span></span>
<span data-ttu-id="5e4fe-216">Par défaut, un compteur de page est activé chaque fois qu'une nouvelle page est chargée dans le navigateur client.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-216">By default, a page count occurs each time a new page loads into the client browser.</span></span>  <span data-ttu-id="5e4fe-217">Mais vous pouvez vouloir consulter d'autres affichages de page.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-217">But you might want to count additional page views.</span></span> <span data-ttu-id="5e4fe-218">Par exemple, si une page affiche son contenu dans des onglets, il se peut que vous désiriez compter une page lorsque l'utilisateur passe d'un onglet à l'autre.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-218">For example, a page might display its content in tabs and you want to count a page when the user switches tabs.</span></span> <span data-ttu-id="5e4fe-219">Ou il se peut que le code JavaScript dans une page charge du nouveau contenu sans modifier l'URL du navigateur.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-219">Or JavaScript code in the page might load new content without changing the browser's URL.</span></span>

<span data-ttu-id="5e4fe-220">Insérez par exemple l'appel JavaScript suivant à l'emplacement approprié dans votre code client :</span><span class="sxs-lookup"><span data-stu-id="5e4fe-220">Insert a JavaScript call like this at the appropriate point in your client code:</span></span>

    appInsights.trackPageView(myPageName);

<span data-ttu-id="5e4fe-221">Le nom d'une page peut contenir les mêmes caractères qu'une URL, mais tout ce qui se trouve après « # » ou « ? » sera ignoré.</span><span class="sxs-lookup"><span data-stu-id="5e4fe-221">The page name can contain the same characters as a URL, but anything after "#" or "?" is ignored.</span></span>

## <a name="usage-tracking"></a><span data-ttu-id="5e4fe-222">Suivi de l’utilisation</span><span class="sxs-lookup"><span data-stu-id="5e4fe-222">Usage tracking</span></span>
<span data-ttu-id="5e4fe-223">Vous souhaitez savoir ce que vos utilisateurs font avec votre application ?</span><span class="sxs-lookup"><span data-stu-id="5e4fe-223">Want to find out what your users do with your app?</span></span>

* [<span data-ttu-id="5e4fe-224">En savoir plus sur le suivi de l’utilisation</span><span class="sxs-lookup"><span data-stu-id="5e4fe-224">Learn about usage tracking</span></span>](app-insights-web-track-usage.md)
* <span data-ttu-id="5e4fe-225">[En savoir plus sur les événements personnalisés et les API de métriques](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="5e4fe-225">[Learn about custom events and metrics API](app-insights-api-custom-events-metrics.md).</span></span>

## <span data-ttu-id="5e4fe-226"><a name="video"></a> Vidéo</span><span class="sxs-lookup"><span data-stu-id="5e4fe-226"><a name="video"></a> Video</span></span>


> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]



## <span data-ttu-id="5e4fe-227"><a name="next"></a> Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5e4fe-227"><a name="next"></a> Next steps</span></span>
* [<span data-ttu-id="5e4fe-228">Suivi de l'utilisation</span><span class="sxs-lookup"><span data-stu-id="5e4fe-228">Track usage</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="5e4fe-229">Mesures et événements personnalisés</span><span class="sxs-lookup"><span data-stu-id="5e4fe-229">Custom events and metrics</span></span>](app-insights-api-custom-events-metrics.md)
* [<span data-ttu-id="5e4fe-230">Développer-mesurer-apprendre</span><span class="sxs-lookup"><span data-stu-id="5e4fe-230">Build-measure-learn</span></span>](app-insights-web-track-usage.md)

