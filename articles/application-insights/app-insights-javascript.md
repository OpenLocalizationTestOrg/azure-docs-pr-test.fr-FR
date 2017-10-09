---
title: les applications web aaaAzure Application Insights pour JavaScript | Documents Microsoft
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
ms.openlocfilehash: 986db3c3776471f9f8556f4e09f2d02aad022549
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-web-pages"></a><span data-ttu-id="eaccc-104">Application Insights pour les pages web</span><span class="sxs-lookup"><span data-stu-id="eaccc-104">Application Insights for web pages</span></span>
<span data-ttu-id="eaccc-105">Découvrez les performances de hello et d’utilisation de votre page web ou d’une application.</span><span class="sxs-lookup"><span data-stu-id="eaccc-105">Find out about hello performance and usage of your web page or app.</span></span> <span data-ttu-id="eaccc-106">Si vous ajoutez [Application Insights](app-insights-overview.md) tooyour script de page, vous obtenez le minutage de chargement de page et les appels AJAX, les nombres et détails des exceptions du navigateur et les échecs d’AJAX, ainsi que les utilisateurs et les nombres de la session.</span><span class="sxs-lookup"><span data-stu-id="eaccc-106">If you add [Application Insights](app-insights-overview.md) tooyour page script, you get timings of page loads and AJAX calls, counts and details of browser exceptions and AJAX failures, as well as users and session counts.</span></span> <span data-ttu-id="eaccc-107">Toutes ces données peuvent être segmentées par page, par version de système d’exploitation ou de navigateur client, par emplacement géographique et en fonction d’autres aspects.</span><span class="sxs-lookup"><span data-stu-id="eaccc-107">All these can be segmented by page, client OS and browser version, geo location, and other dimensions.</span></span> <span data-ttu-id="eaccc-108">Vous pouvez définir des alertes en cas de dépassement d’un certain nombre d’échecs ou de ralentissement du chargement des pages.</span><span class="sxs-lookup"><span data-stu-id="eaccc-108">You can set alerts on failure counts or slow page loading.</span></span> <span data-ttu-id="eaccc-109">Et en insérant des appels de trace dans votre code JavaScript, vous pouvez suivre l’utilisation des hello différentes fonctionnalités de votre application de la page web.</span><span class="sxs-lookup"><span data-stu-id="eaccc-109">And by inserting trace calls in your JavaScript code, you can track how hello different features of your web page application are used.</span></span>

<span data-ttu-id="eaccc-110">Vous pouvez utiliser Application Insights avec toutes les pages web ; il vous suffit pour cela d’ajouter un court extrait de code JavaScript.</span><span class="sxs-lookup"><span data-stu-id="eaccc-110">Application Insights can be used with any web pages - you just add a short piece of JavaScript.</span></span> <span data-ttu-id="eaccc-111">Si votre service web est [Java](app-insights-java-get-started.md) ou [ASP.NET](app-insights-asp-net.md), vous pouvez intégrer les données de télémétrie de votre serveur et de vos clients.</span><span class="sxs-lookup"><span data-stu-id="eaccc-111">If your web service is [Java](app-insights-java-get-started.md) or [ASP.NET](app-insights-asp-net.md), you can integrate telemetry from your server and clients.</span></span>

![Dans portal.azure.com, ouvrez les ressources de votre application, puis cliquez sur Navigateur](./media/app-insights-javascript/03.png)

<span data-ttu-id="eaccc-113">Vous avez besoin d’un abonnement trop[Microsoft Azure](https://azure.com).</span><span class="sxs-lookup"><span data-stu-id="eaccc-113">You need a subscription too[Microsoft Azure](https://azure.com).</span></span> <span data-ttu-id="eaccc-114">Si votre équipe dispose d’un abonnement d’organisation, vous pouvez demander hello propriétaire tooadd votre tooit Account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="eaccc-114">If your team has an organizational subscription, ask hello owner tooadd your Microsoft Account tooit.</span></span> <span data-ttu-id="eaccc-115">Le développement et l’utilisation à petite échelle ne coûtent rien.</span><span class="sxs-lookup"><span data-stu-id="eaccc-115">Development and small-scale use won't cost anything.</span></span>

## <a name="set-up-application-insights-for-your-web-page"></a><span data-ttu-id="eaccc-116">Configurer Application Insights pour votre page web</span><span class="sxs-lookup"><span data-stu-id="eaccc-116">Set up Application Insights for your web page</span></span>
<span data-ttu-id="eaccc-117">Ajouter hello chargeur code extrait tooyour des pages web, comme suit.</span><span class="sxs-lookup"><span data-stu-id="eaccc-117">Add hello loader code snippet tooyour web pages, as follows.</span></span>

### <a name="open-or-create-application-insights-resource"></a><span data-ttu-id="eaccc-118">Ouverture ou création d’une ressource Application Insights dans Azure</span><span class="sxs-lookup"><span data-stu-id="eaccc-118">Open or create Application Insights resource</span></span>
<span data-ttu-id="eaccc-119">Hello ressource Application Insights est où les données sur les performances et d’utilisation de votre page s’affiche.</span><span class="sxs-lookup"><span data-stu-id="eaccc-119">hello Application Insights resource is where data about your page's performance and usage is displayed.</span></span> 

<span data-ttu-id="eaccc-120">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="eaccc-120">Sign into [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="eaccc-121">Si vous avez déjà défini la surveillance pour le côté du serveur hello de votre application, vous disposez déjà d’une ressource :</span><span class="sxs-lookup"><span data-stu-id="eaccc-121">If you already set up monitoring for hello server side of your app, you already have a resource:</span></span>

![Cliquez sur Parcourir, Services de développement, Application Insights.](./media/app-insights-javascript/01-find.png)

<span data-ttu-id="eaccc-123">Si vous n'en avez pas, créez-la.</span><span class="sxs-lookup"><span data-stu-id="eaccc-123">If you don't have one, create it:</span></span>

![Cliquez sur Nouveau, Services de développement, Application Insights.](./media/app-insights-javascript/01-create.png)

<span data-ttu-id="eaccc-125">*Vous avez déjà des questions ?*</span><span class="sxs-lookup"><span data-stu-id="eaccc-125">*Questions already?*</span></span> <span data-ttu-id="eaccc-126">[Plus d’informations sur la création d’une ressource](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="eaccc-126">[More about creating a resource](app-insights-create-new-resource.md).</span></span>

### <a name="add-hello-sdk-script-tooyour-app-or-web-pages"></a><span data-ttu-id="eaccc-127">Ajouter une application de tooyour script hello SDK ou des pages web</span><span class="sxs-lookup"><span data-stu-id="eaccc-127">Add hello SDK script tooyour app or web pages</span></span>
<span data-ttu-id="eaccc-128">Dans le démarrage rapide, obtenir le script de hello pour les pages web :</span><span class="sxs-lookup"><span data-stu-id="eaccc-128">In Quick Start, get hello script for web pages:</span></span>

![Sur votre Panneau de vue d’ensemble des applications, sélectionnez Démarrage rapide, obtenir code toomonitor Mes pages web.](./media/app-insights-javascript/02-monitor-web-page.png)

<span data-ttu-id="eaccc-131">Insérer un script hello juste avant hello `</head>` balise de chaque page, vous souhaitez tootrack.</span><span class="sxs-lookup"><span data-stu-id="eaccc-131">Insert hello script just before hello `</head>` tag of every page you want tootrack.</span></span> <span data-ttu-id="eaccc-132">Si votre site Web dispose d’une page maître, vous pouvez placer les script hello il.</span><span class="sxs-lookup"><span data-stu-id="eaccc-132">If your website has a master page, you can put hello script there.</span></span> <span data-ttu-id="eaccc-133">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="eaccc-133">For example:</span></span>

* <span data-ttu-id="eaccc-134">Dans un projet ASP.NET MVC, vous devez placer le script dans `View\Shared\_Layout.cshtml`</span><span class="sxs-lookup"><span data-stu-id="eaccc-134">In an ASP.NET MVC project, you'd put it in `View\Shared\_Layout.cshtml`</span></span>
* <span data-ttu-id="eaccc-135">Dans un site SharePoint, dans le panneau de configuration hello, ouvrez [paramètres du Site / Page maître](app-insights-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="eaccc-135">In a SharePoint site, on hello control panel, open [Site Settings / Master Page](app-insights-sharepoint.md).</span></span>

<span data-ttu-id="eaccc-136">script de Hello contient la clé d’instrumentation hello qui dirige la ressource d’Application Insights hello données tooyour.</span><span class="sxs-lookup"><span data-stu-id="eaccc-136">hello script contains hello instrumentation key that directs hello data tooyour Application Insights resource.</span></span> 

<span data-ttu-id="eaccc-137">([Une explication plus approfondie du script de hello. ](http://apmtips.com/blog/2015/03/18/javascript-snippet-explained/))</span><span class="sxs-lookup"><span data-stu-id="eaccc-137">([Deeper explanation of hello script.](http://apmtips.com/blog/2015/03/18/javascript-snippet-explained/))</span></span>

<span data-ttu-id="eaccc-138">*(Si vous utilisez une infrastructure de page web connue, cherchez des adaptateurs Application Insights. Par exemple, il existe [un module AngularJS](http://ngmodules.org/modules/angular-appinsights).)*</span><span class="sxs-lookup"><span data-stu-id="eaccc-138">*(If you're using a well-known web page framework, look around for Application Insights adaptors. For example, there's [an AngularJS module](http://ngmodules.org/modules/angular-appinsights).)*</span></span>

## <a name="detailed-configuration"></a><span data-ttu-id="eaccc-139">Configuration détaillée</span><span class="sxs-lookup"><span data-stu-id="eaccc-139">Detailed configuration</span></span>
<span data-ttu-id="eaccc-140">Bien que vous puissiez définir plusieurs [paramètres](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) , vous ne devriez pas avoir besoin de le faire dans la plupart des cas.</span><span class="sxs-lookup"><span data-stu-id="eaccc-140">There are several [parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) you can set, though in most cases, you shouldn't need to.</span></span> <span data-ttu-id="eaccc-141">Par exemple, vous pouvez désactiver ou limiter le nombre de hello des appels Ajax signalées par l’affichage de page (trafic tooreduce).</span><span class="sxs-lookup"><span data-stu-id="eaccc-141">For example, you can disable or limit hello number of Ajax calls reported per page view (tooreduce traffic).</span></span> <span data-ttu-id="eaccc-142">Ou bien, vous pouvez définir debug mode toohave télémétrie déplacer rapidement au pipeline de hello sans être traités par lot.</span><span class="sxs-lookup"><span data-stu-id="eaccc-142">Or you can set debug mode toohave telemetry move rapidly through hello pipeline without being batched.</span></span>

<span data-ttu-id="eaccc-143">tooset ces paramètres, recherchez la ligne dans l’extrait de code hello et ajouter davantage d’éléments séparés par des virgules :</span><span class="sxs-lookup"><span data-stu-id="eaccc-143">tooset these parameters, look for this line in hello code snippet, and add more comma-separated items after it:</span></span>

    })({
      instrumentationKey: "..."
      // Insert here
    });

<span data-ttu-id="eaccc-144">Hello [paramètres disponibles](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) incluent :</span><span class="sxs-lookup"><span data-stu-id="eaccc-144">hello [available parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) include:</span></span>

    // Send telemetry immediately without batching.
    // Remember tooremove this when no longer required, as it
    // can affect browser performance.
    enableDebug: boolean,

    // Don't log browser exceptions.
    disableExceptionTracking: boolean,

    // Don't log ajax calls.
    disableAjaxTracking: boolean,

    // Limit number of Ajax calls logged, tooreduce traffic.
    maxAjaxCallsPerView: 10, // default is 500

    // Time page load up tooexecution of first trackPageView().
    overridePageViewDuration: boolean,

    // Set these dynamically for an authenticated user.
    appUserId: string,
    accountId: string,



## <span data-ttu-id="eaccc-145"><a name="run"></a>Exécution de votre application</span><span class="sxs-lookup"><span data-stu-id="eaccc-145"><a name="run"></a>Run your app</span></span>
<span data-ttu-id="eaccc-146">Exécuter votre application web, utiliser un lors de la télémétrie de toogenerate et patientez quelques secondes.</span><span class="sxs-lookup"><span data-stu-id="eaccc-146">Run your web app, use it a while toogenerate telemetry, and wait a few seconds.</span></span> <span data-ttu-id="eaccc-147">Vous pouvez exécuter à l’aide de hello **F5** clés sur votre ordinateur de développement, ou publier et permettre aux utilisateurs de le manipuler.</span><span class="sxs-lookup"><span data-stu-id="eaccc-147">You can either run it using hello **F5** key on your development machine, or publish it and let users play with it.</span></span>

<span data-ttu-id="eaccc-148">Si vous souhaitez que les données de télémétrie toocheck hello qu’une application web envoie tooApplication Insights, utilisez les outils de débogage de votre navigateur (**F12** sur de nombreux navigateurs).</span><span class="sxs-lookup"><span data-stu-id="eaccc-148">If you want toocheck hello telemetry that a web app is sending tooApplication Insights, use your browser's debugging tools (**F12** on many browsers).</span></span> <span data-ttu-id="eaccc-149">Données sont envoyées toodc.services.visualstudio.com.</span><span class="sxs-lookup"><span data-stu-id="eaccc-149">Data is sent toodc.services.visualstudio.com.</span></span>

## <a name="explore-your-browser-performance-data"></a><span data-ttu-id="eaccc-150">Exploration de vos données de performances dans les navigateurs</span><span class="sxs-lookup"><span data-stu-id="eaccc-150">Explore your browser performance data</span></span>
<span data-ttu-id="eaccc-151">Ouvrez hello navigateur panneau tooshow agrégée les données de performances à partir de navigateurs de vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="eaccc-151">Open hello Browser blade tooshow aggregated performance data from your users' browsers.</span></span>

![Dans portal.azure.com, ouvrez les ressources de votre application, puis cliquez sur Paramètres, Navigateur.](./media/app-insights-javascript/03.png)

<span data-ttu-id="eaccc-153">*Pas de données pour le moment ? Cliquez sur **Actualiser** en hello haut hello. Toujours rien ? Consultez la rubrique [Résolution des problèmes](app-insights-troubleshoot-faq.md).*</span><span class="sxs-lookup"><span data-stu-id="eaccc-153">*No data yet? Click **Refresh** at hello top of hello page. Still nothing? See [Troubleshooting](app-insights-troubleshoot-faq.md).*</span></span>

<span data-ttu-id="eaccc-154">Panneau de navigateur Hello est un [panneau Metrics Explorer](app-insights-metrics-explorer.md) avec des filtres prédéfinis et les sélections de graphique.</span><span class="sxs-lookup"><span data-stu-id="eaccc-154">hello Browser blade is a [Metrics Explorer blade](app-insights-metrics-explorer.md) with preset filters and chart selections.</span></span> <span data-ttu-id="eaccc-155">Vous pouvez modifier la plage de temps hello, de filtres et de configuration des graphiques si vous le souhaitez et enregistrez le résultat de hello en tant que favori.</span><span class="sxs-lookup"><span data-stu-id="eaccc-155">You can edit hello time range, filters, and chart configuration if you want, and save hello result as a favorite.</span></span> <span data-ttu-id="eaccc-156">Cliquez sur **restaurer les valeurs par défaut** configuration du panneau tooget toohello arrière d’origine.</span><span class="sxs-lookup"><span data-stu-id="eaccc-156">Click **Restore defaults** tooget back toohello original blade configuration.</span></span>

## <a name="page-load-performance"></a><span data-ttu-id="eaccc-157">Performances de chargement des pages</span><span class="sxs-lookup"><span data-stu-id="eaccc-157">Page load performance</span></span>
<span data-ttu-id="eaccc-158">À hello haut est un graphique segmenté de temps de chargement de page.</span><span class="sxs-lookup"><span data-stu-id="eaccc-158">At hello top is a segmented chart of page load times.</span></span> <span data-ttu-id="eaccc-159">hauteur totale de Hello du graphique de hello représente des pages de tooload et l’affichage de la durée moyenne hello à partir de votre application dans les navigateurs de vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="eaccc-159">hello total height of hello chart represents hello average time tooload and display pages from your app in your users' browsers.</span></span> <span data-ttu-id="eaccc-160">temps de Hello est mesuré à partir de lorsque le navigateur de hello envoie la requête HTTP initiale de hello jusqu'à ce que la charge synchrone tous les événements ont été traités, y compris la mise en page et d’exécution de scripts.</span><span class="sxs-lookup"><span data-stu-id="eaccc-160">hello time is measured from when hello browser sends hello initial HTTP request until all synchronous load events have been processed, including layout and running scripts.</span></span> <span data-ttu-id="eaccc-161">Elle n’inclut pas les tâches asynchrones telles que le chargement des composants web à partir des appels AJAX.</span><span class="sxs-lookup"><span data-stu-id="eaccc-161">It doesn't include asynchronous tasks such as loading web parts from AJAX calls.</span></span>

<span data-ttu-id="eaccc-162">graphique de Hello segmente les temps de chargement du nombre total de pages hello en hello [minutages standards définis par le W3C](http://www.w3.org/TR/navigation-timing/#processing-model).</span><span class="sxs-lookup"><span data-stu-id="eaccc-162">hello chart segments hello total page load time into hello [standard timings defined by W3C](http://www.w3.org/TR/navigation-timing/#processing-model).</span></span> 

![](./media/app-insights-javascript/08-client-split.png)

<span data-ttu-id="eaccc-163">Notez que hello *de connexion réseau* heure est souvent inférieure à ce que vous pourriez vous attendre, car elle est une moyenne de toutes les demandes d’hello navigateur toohello le serveur.</span><span class="sxs-lookup"><span data-stu-id="eaccc-163">Note that hello *network connect* time is often lower than you might expect, because it's an average over all requests from hello browser toohello server.</span></span> <span data-ttu-id="eaccc-164">Nombre de requêtes individuelles ont une durée de connexion 0, car il existe déjà un serveur de toohello de connexion active.</span><span class="sxs-lookup"><span data-stu-id="eaccc-164">Many individual requests have a connect time of 0 because there is already an active connection toohello server.</span></span>

### <a name="slow-loading"></a><span data-ttu-id="eaccc-165">Le chargement est lent ?</span><span class="sxs-lookup"><span data-stu-id="eaccc-165">Slow loading?</span></span>
<span data-ttu-id="eaccc-166">Les pages qui mettent du temps à se charger constituent une source de mécontentement majeure pour vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="eaccc-166">Slow page loads are a major source of dissatisfaction for your users.</span></span> <span data-ttu-id="eaccc-167">Si le graphique de hello indique le chargement de page lente, il est facile toodo des recherches de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="eaccc-167">If hello chart indicates slow page loads, it's easy toodo some diagnostic research.</span></span>

<span data-ttu-id="eaccc-168">graphique de Hello montre toutes les charges de page moyenne hello dans votre application.</span><span class="sxs-lookup"><span data-stu-id="eaccc-168">hello chart shows hello average of all page loads in your app.</span></span> <span data-ttu-id="eaccc-169">toosee si le problème de hello est limitée tooparticular pages, plus détaillée de panneau de hello, dans lequel il existe une grille segmentée par une URL de la page :</span><span class="sxs-lookup"><span data-stu-id="eaccc-169">toosee if hello problem is confined tooparticular pages, look further down hello blade, where there's a grid segmented by page URL:</span></span>

![](./media/app-insights-javascript/09-page-perf.png)

<span data-ttu-id="eaccc-170">Notez le nombre de vues de page hello et l’écart.</span><span class="sxs-lookup"><span data-stu-id="eaccc-170">Notice hello page view count and standard deviation.</span></span> <span data-ttu-id="eaccc-171">Si le nombre de pages hello est très faible, puis problème de hello n’est pas affecter d’utilisateurs beaucoup.</span><span class="sxs-lookup"><span data-stu-id="eaccc-171">If hello page count is very low, then hello issue isn't affecting users much.</span></span> <span data-ttu-id="eaccc-172">Un écart type élevé (moyenne toohello comparables lui-même) indique un grand nombre de variation entre des mesures individuelles.</span><span class="sxs-lookup"><span data-stu-id="eaccc-172">A high standard deviation (comparable toohello average itself) indicates a lot of variation between individual measurements.</span></span>

<span data-ttu-id="eaccc-173">**Zoomez sur une URL et un affichage de page.**</span><span class="sxs-lookup"><span data-stu-id="eaccc-173">**Zoom in on one URL and one page view.**</span></span> <span data-ttu-id="eaccc-174">Cliquez sur n’importe quel toosee de nom de page une lame de navigateur graphiques filtrés toothat simplement URL ; puis sur une instance d’un affichage de page.</span><span class="sxs-lookup"><span data-stu-id="eaccc-174">Click any page name toosee a blade of browser charts filtered just toothat URL; and then on an instance of a page view.</span></span>

![](./media/app-insights-javascript/35.png)

<span data-ttu-id="eaccc-175">Cliquez sur `...` pour une liste complète des propriétés pour cet événement, ou examiner les appels Ajax hello et événements connexes.</span><span class="sxs-lookup"><span data-stu-id="eaccc-175">Click `...` for a full list of properties for that event, or inspect hello Ajax calls and related events.</span></span> <span data-ttu-id="eaccc-176">Appels Ajax lents affectent hello page global des temps de chargement s’ils sont synchrones.</span><span class="sxs-lookup"><span data-stu-id="eaccc-176">Slow Ajax calls affect hello overall page load time if they are synchronous.</span></span> <span data-ttu-id="eaccc-177">Liées événements incluent des requêtes au serveur pour hello même URL (si vous avez configuré Application Insights sur votre serveur web).</span><span class="sxs-lookup"><span data-stu-id="eaccc-177">Related events include server requests for hello same URL (if you've set up Application Insights on your web server).</span></span>

<span data-ttu-id="eaccc-178">**Historique des performances de la page.**</span><span class="sxs-lookup"><span data-stu-id="eaccc-178">**Page performance over time.**</span></span> <span data-ttu-id="eaccc-179">Revenir au panneau de navigateurs hello, transformer grille de temps de chargement de Page vue hello une toosee graphique de ligne s’il y a des pics à des moments :</span><span class="sxs-lookup"><span data-stu-id="eaccc-179">Back at hello Browsers blade, change hello Page View Load Time grid into a line chart toosee if there were peaks at particular times:</span></span>

![Cliquez sur en-tête hello de grille de hello et sélectionnez un nouveau type de graphique](./media/app-insights-javascript/10-page-perf-area.png)

<span data-ttu-id="eaccc-181">**Segmentation en fonction d’autres aspects.**</span><span class="sxs-lookup"><span data-stu-id="eaccc-181">**Segment by other dimensions.**</span></span> <span data-ttu-id="eaccc-182">Peut-être que vos pages sont tooload plus lent sur un emplacement spécifique de navigateur, du système d’exploitation client ou utilisateur ?</span><span class="sxs-lookup"><span data-stu-id="eaccc-182">Maybe your pages are slower tooload on a particular browser, client OS, or user locality?</span></span> <span data-ttu-id="eaccc-183">Ajouter un nouveau graphique et faire des essais avec hello **Group by** dimension.</span><span class="sxs-lookup"><span data-stu-id="eaccc-183">Add a new chart and experiment with hello **Group-by** dimension.</span></span>

![](./media/app-insights-javascript/21.png)

## <a name="ajax-performance"></a><span data-ttu-id="eaccc-184">Performances AJAX</span><span class="sxs-lookup"><span data-stu-id="eaccc-184">AJAX Performance</span></span>
<span data-ttu-id="eaccc-185">Assurez-vous que tous les appels AJAX dans vos pages web fonctionnent correctement.</span><span class="sxs-lookup"><span data-stu-id="eaccc-185">Make sure any AJAX calls in your web pages are performing well.</span></span> <span data-ttu-id="eaccc-186">Il s’agit souvent utilisé toofill des parties de votre page de façon asynchrone.</span><span class="sxs-lookup"><span data-stu-id="eaccc-186">They are often used toofill parts of your page asynchronously.</span></span> <span data-ttu-id="eaccc-187">Bien que hello page globale peut charger rapidement, vos utilisateurs pourraient confrontés veut WebPart vide, en attente de tooappear de données dans les.</span><span class="sxs-lookup"><span data-stu-id="eaccc-187">Although hello overall page might load promptly, your users could be frustrated by staring at blank web parts, waiting for data tooappear in them.</span></span>

<span data-ttu-id="eaccc-188">Appels AJAX effectuées à partir de votre page web sont affichés sur le panneau de navigateurs hello en tant que dépendances.</span><span class="sxs-lookup"><span data-stu-id="eaccc-188">AJAX calls made from your web page are shown on hello Browsers blade as dependencies.</span></span>

<span data-ttu-id="eaccc-189">Il existe des graphiques de résumé dans la partie supérieure de hello du Panneau de hello :</span><span class="sxs-lookup"><span data-stu-id="eaccc-189">There are summary charts in hello upper part of hello blade:</span></span>

![](./media/app-insights-javascript/31.png)

<span data-ttu-id="eaccc-190">et des grilles détaillées plus bas :</span><span class="sxs-lookup"><span data-stu-id="eaccc-190">and detailed grids lower down:</span></span>

![](./media/app-insights-javascript/33.png)

<span data-ttu-id="eaccc-191">Cliquez sur n’importe quelle ligne pour obtenir des détails spécifiques.</span><span class="sxs-lookup"><span data-stu-id="eaccc-191">Click any row for specific details.</span></span>

> [!NOTE]
> <span data-ttu-id="eaccc-192">Si vous supprimez le filtre de navigateurs hello sur le panneau de hello, serveur et dépendances AJAX sont inclus dans ces graphiques.</span><span class="sxs-lookup"><span data-stu-id="eaccc-192">If you delete hello Browsers filter on hello blade, both server and AJAX dependencies are included in these charts.</span></span> <span data-ttu-id="eaccc-193">Cliquez sur le filtre de hello tooreconfigure de paramètres par défaut.</span><span class="sxs-lookup"><span data-stu-id="eaccc-193">Click Restore Defaults tooreconfigure hello filter.</span></span>
> 
> 

<span data-ttu-id="eaccc-194">**toodrill dans des échecs d’appels Ajax** défiler la grille de défaillances de dépendance toohello, puis cliquez sur une instance spécifique de toosee de ligne.</span><span class="sxs-lookup"><span data-stu-id="eaccc-194">**toodrill into failed Ajax calls** scroll down toohello Dependency failures grid, and then click a row toosee specific instances.</span></span>

![](./media/app-insights-javascript/37.png)


<span data-ttu-id="eaccc-195">Cliquez sur `...` de télémétrie complète de hello pour un appel Ajax.</span><span class="sxs-lookup"><span data-stu-id="eaccc-195">Click `...` for hello full telemetry for an Ajax call.</span></span>

### <a name="no-ajax-calls-reported"></a><span data-ttu-id="eaccc-196">Aucun appel Ajax n’est signalé ?</span><span class="sxs-lookup"><span data-stu-id="eaccc-196">No Ajax calls reported?</span></span>
<span data-ttu-id="eaccc-197">Appels AJAX incluent tous les appels HTTP/HTTPS effectuées à partir du script hello de votre page web.</span><span class="sxs-lookup"><span data-stu-id="eaccc-197">Ajax calls include any HTTP/HTTPS  calls made from hello script of your web page.</span></span> <span data-ttu-id="eaccc-198">Si vous ne voyez pas les signalé, vérifiez hello ne définit pas cet extrait de code hello `disableAjaxTracking` ou `maxAjaxCallsPerView` [paramètres](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span><span class="sxs-lookup"><span data-stu-id="eaccc-198">If you don't see them reported, check that hello code snippet doesn't set hello `disableAjaxTracking` or `maxAjaxCallsPerView` [parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span></span>

## <a name="browser-exceptions"></a><span data-ttu-id="eaccc-199">Exceptions du navigateur</span><span class="sxs-lookup"><span data-stu-id="eaccc-199">Browser exceptions</span></span>
<span data-ttu-id="eaccc-200">Dans Panneau de navigateurs hello, il existe un graphique de synthèse des exceptions et une grille des types d’exception plus bas le panneau de hello.</span><span class="sxs-lookup"><span data-stu-id="eaccc-200">On hello Browsers blade, there's an exceptions summary chart, and a grid of exception types further down hello blade.</span></span>

![](./media/app-insights-javascript/39.png)

<span data-ttu-id="eaccc-201">Si vous ne voyez pas les exceptions de navigateur signalées, vérifiez hello ne définit pas cet extrait de code hello `disableExceptionTracking` [paramètre](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span><span class="sxs-lookup"><span data-stu-id="eaccc-201">If you don't see browser exceptions reported, check that hello code snippet doesn't set hello `disableExceptionTracking` [parameter](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span></span>

## <a name="inspect-individual-page-view-events"></a><span data-ttu-id="eaccc-202">Inspection des événements d’affichage de page individuels</span><span class="sxs-lookup"><span data-stu-id="eaccc-202">Inspect individual page view events</span></span>

<span data-ttu-id="eaccc-203">La télémétrie de l'affichage de page est généralement analysée par Application Insights, et vous ne consultez que des rapports cumulés, avec une moyenne entre tous les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="eaccc-203">Usually page view telemetry is analyzed by Application Insights and you see only cumulative reports, averaged over all your users.</span></span> <span data-ttu-id="eaccc-204">Toutefois, à des fins de débogage, vous pouvez également consulter des événements d'affichage de page individuels.</span><span class="sxs-lookup"><span data-stu-id="eaccc-204">But for debugging purposes, you can also look at individual page view events.</span></span>

<span data-ttu-id="eaccc-205">Dans le panneau de recherche Diagnostic hello, définir les filtres tooPage vue.</span><span class="sxs-lookup"><span data-stu-id="eaccc-205">In hello Diagnostic Search blade, set Filters tooPage View.</span></span>

![](./media/app-insights-javascript/12-search-pages.png)

<span data-ttu-id="eaccc-206">Sélectionnez n’importe quel toosee événement plus en détail.</span><span class="sxs-lookup"><span data-stu-id="eaccc-206">Select any event toosee more detail.</span></span> <span data-ttu-id="eaccc-207">Dans la page de détails de hello, cliquez sur «... » toosee encore plus de détails.</span><span class="sxs-lookup"><span data-stu-id="eaccc-207">In hello details page, click "..." toosee even more detail.</span></span>

> [!NOTE]
> <span data-ttu-id="eaccc-208">Si vous utilisez [recherche](app-insights-diagnostic-search.md), notez que vous disposez des mots entiers toomatch : « Ropos » et « à propos de » ne correspondent pas « About ».</span><span class="sxs-lookup"><span data-stu-id="eaccc-208">If you use [Search](app-insights-diagnostic-search.md), notice that you have toomatch whole words: "Abou" and "bout" do not match "About".</span></span>
> 
> 

<span data-ttu-id="eaccc-209">Vous pouvez également utiliser hello puissant [de langage de requête Analytique de journal](https://docs.microsoft.com/azure/application-insights/app-insights-analytics-tour#browser-timings-table) toosearch les vues de page.</span><span class="sxs-lookup"><span data-stu-id="eaccc-209">You can also use hello powerful [Log Analytics query language](https://docs.microsoft.com/azure/application-insights/app-insights-analytics-tour#browser-timings-table) toosearch page views.</span></span>

### <a name="page-view-properties"></a><span data-ttu-id="eaccc-210">Propriétés d'affichage de la page</span><span class="sxs-lookup"><span data-stu-id="eaccc-210">Page view properties</span></span>
* <span data-ttu-id="eaccc-211">**Durée d’affichage de la page**</span><span class="sxs-lookup"><span data-stu-id="eaccc-211">**Page view duration**</span></span> 
  
  * <span data-ttu-id="eaccc-212">Par défaut, hello fois qu’il prend tooload hello page, à partir du client demande toofull charger (y compris les fichiers auxiliaires mais à l’exclusion des tâches asynchrones tels que les appels Ajax).</span><span class="sxs-lookup"><span data-stu-id="eaccc-212">By default, hello time it takes tooload hello page, from client request toofull load (including auxiliary files but excluding asynchronous tasks such as Ajax calls).</span></span> 
  * <span data-ttu-id="eaccc-213">Si vous définissez `overridePageViewDuration` Bonjour [configuration de la page](#detailed-configuration), hello intervalle entre tooexecution de demande client Hello tout d’abord `trackPageView`.</span><span class="sxs-lookup"><span data-stu-id="eaccc-213">If you set `overridePageViewDuration` in hello [page configuration](#detailed-configuration), hello interval between client request tooexecution of hello first `trackPageView`.</span></span> <span data-ttu-id="eaccc-214">Si vous avez déplacé trackPageView depuis sa position habituelle après l’initialisation de hello du script de hello, il reflète une valeur différente.</span><span class="sxs-lookup"><span data-stu-id="eaccc-214">If you moved trackPageView from its usual position after hello initialization of hello script, it will reflect a different value.</span></span>
  * <span data-ttu-id="eaccc-215">Si `overridePageViewDuration` est défini et une durée d’argument est fourni dans hello `trackPageView()` appeler, puis de la valeur de l’argument hello est utilisée à la place.</span><span class="sxs-lookup"><span data-stu-id="eaccc-215">If `overridePageViewDuration` is set and a duration argument is provided in hello `trackPageView()` call, then hello argument value is used instead.</span></span> 

## <a name="custom-page-counts"></a><span data-ttu-id="eaccc-216">Compteurs de page personnalisés</span><span class="sxs-lookup"><span data-stu-id="eaccc-216">Custom page counts</span></span>
<span data-ttu-id="eaccc-217">Par défaut, un nombre de pages se produit chaque fois qu'une nouvelle page est chargée dans le navigateur du client hello.</span><span class="sxs-lookup"><span data-stu-id="eaccc-217">By default, a page count occurs each time a new page loads into hello client browser.</span></span>  <span data-ttu-id="eaccc-218">Toutefois, vous pouvez toocount les vues de page supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="eaccc-218">But you might want toocount additional page views.</span></span> <span data-ttu-id="eaccc-219">Par exemple, une page peut afficher son contenu dans les onglets et vous toocount une page lorsque les utilisateur hello bascule onglets.</span><span class="sxs-lookup"><span data-stu-id="eaccc-219">For example, a page might display its content in tabs and you want toocount a page when hello user switches tabs.</span></span> <span data-ttu-id="eaccc-220">Ou le code JavaScript dans la page de hello peut charger de nouveau contenu sans modifier l’URL du navigateur hello.</span><span class="sxs-lookup"><span data-stu-id="eaccc-220">Or JavaScript code in hello page might load new content without changing hello browser's URL.</span></span>

<span data-ttu-id="eaccc-221">Insérer un appel JavaScript comme suit à point hello dans votre code client :</span><span class="sxs-lookup"><span data-stu-id="eaccc-221">Insert a JavaScript call like this at hello appropriate point in your client code:</span></span>

    appInsights.trackPageView(myPageName);

<span data-ttu-id="eaccc-222">nom de la page Hello peut contenir hello même caractères en tant qu’URL, mais n’est pas défini après « # » ou « ? » est ignoré.</span><span class="sxs-lookup"><span data-stu-id="eaccc-222">hello page name can contain hello same characters as a URL, but anything after "#" or "?" is ignored.</span></span>

## <a name="usage-tracking"></a><span data-ttu-id="eaccc-223">Suivi de l’utilisation</span><span class="sxs-lookup"><span data-stu-id="eaccc-223">Usage tracking</span></span>
<span data-ttu-id="eaccc-224">Vous souhaitez toofind les opérations de vos utilisateurs avec votre application ?</span><span class="sxs-lookup"><span data-stu-id="eaccc-224">Want toofind out what your users do with your app?</span></span>

* [<span data-ttu-id="eaccc-225">En savoir plus sur le suivi de l’utilisation</span><span class="sxs-lookup"><span data-stu-id="eaccc-225">Learn about usage tracking</span></span>](app-insights-web-track-usage.md)
* <span data-ttu-id="eaccc-226">[En savoir plus sur les événements personnalisés et les API de métriques](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="eaccc-226">[Learn about custom events and metrics API](app-insights-api-custom-events-metrics.md).</span></span>

## <span data-ttu-id="eaccc-227"><a name="video"></a> Vidéo</span><span class="sxs-lookup"><span data-stu-id="eaccc-227"><a name="video"></a> Video</span></span>


> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]



## <span data-ttu-id="eaccc-228"><a name="next"></a> Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="eaccc-228"><a name="next"></a> Next steps</span></span>
* [<span data-ttu-id="eaccc-229">Suivi de l'utilisation</span><span class="sxs-lookup"><span data-stu-id="eaccc-229">Track usage</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="eaccc-230">Mesures et événements personnalisés</span><span class="sxs-lookup"><span data-stu-id="eaccc-230">Custom events and metrics</span></span>](app-insights-api-custom-events-metrics.md)
* [<span data-ttu-id="eaccc-231">Développer-mesurer-apprendre</span><span class="sxs-lookup"><span data-stu-id="eaccc-231">Build-measure-learn</span></span>](app-insights-web-track-usage.md)

