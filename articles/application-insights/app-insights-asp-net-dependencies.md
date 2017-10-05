---
title: "Suivi des dépendances dans Azure Application Insights | Microsoft Docs"
description: "Analysez l'utilisation, la disponibilité et les performances de votre application web locale ou Microsoft Azure avec Application Insights."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d15c4ca8-4c1a-47ab-a03d-c322b4bb2a9e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: bwren
ms.openlocfilehash: 6e0b67ba98af27017901608dde4401600eb9957f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="set-up-application-insights-dependency-tracking"></a><span data-ttu-id="19c30-103">Configurer Application Insights : suivi des dépendances</span><span class="sxs-lookup"><span data-stu-id="19c30-103">Set up Application Insights: Dependency tracking</span></span>
<span data-ttu-id="19c30-104">Un *dépendance* est un composant externe qui est appelé par votre application.</span><span class="sxs-lookup"><span data-stu-id="19c30-104">A *dependency* is an external component that is called by your app.</span></span> <span data-ttu-id="19c30-105">Il s’agit habituellement d’un service appelé à l’aide de HTTP, d’une base de données ou d’un système de fichiers.</span><span class="sxs-lookup"><span data-stu-id="19c30-105">It's typically a service called using HTTP, or a database, or a file system.</span></span> <span data-ttu-id="19c30-106">[Application Insights](app-insights-overview.md) mesure combien de temps votre application attend les dépendances et la fréquence à laquelle un appel de dépendance échoue.</span><span class="sxs-lookup"><span data-stu-id="19c30-106">[Application Insights](app-insights-overview.md) measures how long your application waits for dependencies and how often a dependency call fails.</span></span> <span data-ttu-id="19c30-107">Vous pouvez examiner des appels spécifiques et les associer à des demandes et des exceptions.</span><span class="sxs-lookup"><span data-stu-id="19c30-107">You can investigate specific calls, and relate them to requests and exceptions.</span></span>

![Exemples de graphiques](./media/app-insights-asp-net-dependencies/10-intro.png)

<span data-ttu-id="19c30-109">Le moniteur de dépendance prêt à l’emploi signale les appels aux types de dépendances suivants :</span><span class="sxs-lookup"><span data-stu-id="19c30-109">The out-of-the-box dependency monitor currently reports calls to these  types of dependencies:</span></span>

* <span data-ttu-id="19c30-110">Serveur</span><span class="sxs-lookup"><span data-stu-id="19c30-110">Server</span></span>
  * <span data-ttu-id="19c30-111">Bases de données SQL</span><span class="sxs-lookup"><span data-stu-id="19c30-111">SQL databases</span></span>
  * <span data-ttu-id="19c30-112">Services web et WCF d’ASP.NET qui utilisent des liaisons HTTP</span><span class="sxs-lookup"><span data-stu-id="19c30-112">ASP.NET web and WCF services that use HTTP-based bindings</span></span>
  * <span data-ttu-id="19c30-113">Appels HTTP locaux ou distants</span><span class="sxs-lookup"><span data-stu-id="19c30-113">Local or remote HTTP calls</span></span>
  * <span data-ttu-id="19c30-114">Azure Cosmos DB, table, stockage d’objets blob et file d’attente</span><span class="sxs-lookup"><span data-stu-id="19c30-114">Azure Cosmos DB, table, blob storage, and queue</span></span>
* <span data-ttu-id="19c30-115">Pages web</span><span class="sxs-lookup"><span data-stu-id="19c30-115">Web pages</span></span>
  * <span data-ttu-id="19c30-116">Appels AJAX</span><span class="sxs-lookup"><span data-stu-id="19c30-116">AJAX calls</span></span>

<span data-ttu-id="19c30-117">La surveillance fonctionne en utilisant l’[instrumentation de code octet](https://msdn.microsoft.com/library/z9z62c29.aspx) autour des méthodes sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="19c30-117">Monitoring works by using [byte code instrumentation](https://msdn.microsoft.com/library/z9z62c29.aspx) around selected methods.</span></span> <span data-ttu-id="19c30-118">La surcharge de performances est minime.</span><span class="sxs-lookup"><span data-stu-id="19c30-118">Performance overhead is minimal.</span></span>

<span data-ttu-id="19c30-119">Vous pouvez écrire vos propres appels de SDK pour surveiller d’autres dépendances, à la fois dans le code client et serveur, à l’aide de l’[API TrackDependency](app-insights-api-custom-events-metrics.md#trackdependency).</span><span class="sxs-lookup"><span data-stu-id="19c30-119">You can also write your own SDK calls to monitor other dependencies, both in the client and server code, using the [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span></span>

## <a name="set-up-dependency-monitoring"></a><span data-ttu-id="19c30-120">Configurer la surveillance des dépendances</span><span class="sxs-lookup"><span data-stu-id="19c30-120">Set up dependency monitoring</span></span>
<span data-ttu-id="19c30-121">Les informations sur les dépendances partielles sont collectées automatiquement par le [SDK Application Insights](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="19c30-121">Partial dependency information is collected automatically by the [Application Insights SDK](app-insights-asp-net.md).</span></span> <span data-ttu-id="19c30-122">Pour obtenir des données complètes, installez l’agent approprié pour le serveur hôte.</span><span class="sxs-lookup"><span data-stu-id="19c30-122">To get complete data, install the appropriate agent for the host server.</span></span>

| <span data-ttu-id="19c30-123">Plateforme</span><span class="sxs-lookup"><span data-stu-id="19c30-123">Platform</span></span> | <span data-ttu-id="19c30-124">Installer</span><span class="sxs-lookup"><span data-stu-id="19c30-124">Install</span></span> |
| --- | --- |
| <span data-ttu-id="19c30-125">Serveur IIS</span><span class="sxs-lookup"><span data-stu-id="19c30-125">IIS Server</span></span> |<span data-ttu-id="19c30-126">[Installez Status Monitor sur votre serveur](app-insights-monitor-performance-live-website-now.md) ou [mettez à niveau votre application avec .NET Framework version 4.6 ou ultérieure](http://go.microsoft.com/fwlink/?LinkId=528259) et installez le [SDK Application Insights](app-insights-asp-net.md) dans votre application.</span><span class="sxs-lookup"><span data-stu-id="19c30-126">Either [install Status Monitor on your server](app-insights-monitor-performance-live-website-now.md) or [Upgrade your application to .NET framework 4.6 or later](http://go.microsoft.com/fwlink/?LinkId=528259) and install the [Application Insights SDK](app-insights-asp-net.md)  in your app.</span></span> |
| <span data-ttu-id="19c30-127">Application web Azure</span><span class="sxs-lookup"><span data-stu-id="19c30-127">Azure Web App</span></span> |<span data-ttu-id="19c30-128">Dans le panneau de configuration de votre application web, [ouvrez le panneau Application Insights](app-insights-azure-web-apps.md) et choisissez l’installation si vous y êtes invité.</span><span class="sxs-lookup"><span data-stu-id="19c30-128">In your web app control panel, [open the Application Insights blade in your web app control panel](app-insights-azure-web-apps.md) and choose Install if prompted.</span></span> |
| <span data-ttu-id="19c30-129">Service cloud Azure</span><span class="sxs-lookup"><span data-stu-id="19c30-129">Azure Cloud Service</span></span> |<span data-ttu-id="19c30-130">[Utilisez une tâche de démarrage](app-insights-cloudservices.md) ou [installez le .NET Framework version 4.6 ou ultérieure](../cloud-services/cloud-services-dotnet-install-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="19c30-130">[Use startup task](app-insights-cloudservices.md) or [Install .NET framework 4.6+](../cloud-services/cloud-services-dotnet-install-dotnet.md)</span></span> |

## <a name="where-to-find-dependency-data"></a><span data-ttu-id="19c30-131">Où trouver des données sur les dépendances</span><span class="sxs-lookup"><span data-stu-id="19c30-131">Where to find dependency data</span></span>
* <span data-ttu-id="19c30-132">[Mise en correspondance d’applications](#application-map) visualise les dépendances entre votre application et les composants voisins.</span><span class="sxs-lookup"><span data-stu-id="19c30-132">[Application Map](#application-map) visualizes dependencies between your app and neighbouring components.</span></span>
* <span data-ttu-id="19c30-133">[Les panneaux de performances, de navigateurs et d’échecs](#performance-and-blades) affichent les données sur les dépendances de serveur.</span><span class="sxs-lookup"><span data-stu-id="19c30-133">[Performance, browser, and failure blades](#performance-and-blades) show server dependency data.</span></span>
* <span data-ttu-id="19c30-134">[Les panneaux de navigateurs](#ajax-calls) montrent les appels AJAX provenant des navigateurs de vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="19c30-134">[Browsers blade](#ajax-calls) shows AJAX calls from your users' browsers.</span></span>
* <span data-ttu-id="19c30-135">[Parcourez les requêtes lentes ou ayant échoué](#diagnose-slow-requests) pour vérifier leurs appels de dépendances.</span><span class="sxs-lookup"><span data-stu-id="19c30-135">[Click through from slow or failed requests](#diagnose-slow-requests) to check their dependency calls.</span></span>
* <span data-ttu-id="19c30-136">Vous pouvez utiliser [Analytics](#analytics) pour interroger des données de dépendances.</span><span class="sxs-lookup"><span data-stu-id="19c30-136">[Analytics](#analytics) can be used to query dependency data.</span></span>

## <a name="application-map"></a><span data-ttu-id="19c30-137">Mise en correspondance d'applications</span><span class="sxs-lookup"><span data-stu-id="19c30-137">Application Map</span></span>
<span data-ttu-id="19c30-138">Mise en correspondance d'applications fonctionne comme une aide visuelle pour découvrir les dépendances entre les composants de votre application.</span><span class="sxs-lookup"><span data-stu-id="19c30-138">Application Map acts as a visual aid to discovering dependencies between the components of your application.</span></span> <span data-ttu-id="19c30-139">Il est généré automatiquement à partir de la télémétrie de votre application.</span><span class="sxs-lookup"><span data-stu-id="19c30-139">It is automatically generated from the telemetry from your app.</span></span> <span data-ttu-id="19c30-140">Cet exemple montre les appels AJAX provenant des scripts de navigateur et les appels REST de l’application serveur à deux services externes.</span><span class="sxs-lookup"><span data-stu-id="19c30-140">This example shows AJAX calls from the browser scripts and REST calls from the server app to two external services.</span></span>

![Mise en correspondance d'applications](./media/app-insights-asp-net-dependencies/08.png)

* <span data-ttu-id="19c30-142">**Accédez à partir des zones** aux graphiques de dépendances pertinents et d’autres graphiques.</span><span class="sxs-lookup"><span data-stu-id="19c30-142">**Navigate from the boxes** to relevant dependency and other charts.</span></span>
* <span data-ttu-id="19c30-143">**Épinglez la mise en correspondance** sur le [tableau de bord](app-insights-dashboards.md), où elle sera entièrement opérationnelle.</span><span class="sxs-lookup"><span data-stu-id="19c30-143">**Pin the map** to the [dashboard](app-insights-dashboards.md), where it will be fully functional.</span></span>

<span data-ttu-id="19c30-144">[En savoir plus](app-insights-app-map.md).</span><span class="sxs-lookup"><span data-stu-id="19c30-144">[Learn more](app-insights-app-map.md).</span></span>

## <a name="performance-and-failure-blades"></a><span data-ttu-id="19c30-145">Panneaux de performances et d’échecs</span><span class="sxs-lookup"><span data-stu-id="19c30-145">Performance and failure blades</span></span>
<span data-ttu-id="19c30-146">Le panneau de performances indique la durée des appels de dépendances effectués par l’application serveur.</span><span class="sxs-lookup"><span data-stu-id="19c30-146">The performance blade shows the duration of dependency calls made by the server app.</span></span> <span data-ttu-id="19c30-147">Il existe un graphique de synthèse et un tableau segmenté par appel.</span><span class="sxs-lookup"><span data-stu-id="19c30-147">There's a summary chart and a table segmented by call.</span></span>

![Graphiques de dépendances du panneau de performances](./media/app-insights-asp-net-dependencies/dependencies-in-performance-blade.png)

<span data-ttu-id="19c30-149">Parcourez les graphiques de synthèses ou les éléments du tableau pour rechercher les occurrences brutes de ces appels.</span><span class="sxs-lookup"><span data-stu-id="19c30-149">Click through the summary charts or the table items to search raw occurrences of these calls.</span></span>

![Instances d’appels de dépendances](./media/app-insights-asp-net-dependencies/dependency-call-instance.png)

<span data-ttu-id="19c30-151">Le **Nombre d’échecs** est affiché dans le panneau **Échecs**.</span><span class="sxs-lookup"><span data-stu-id="19c30-151">**Failure counts** are shown on the **Failures** blade.</span></span> <span data-ttu-id="19c30-152">Un échec est tout code de retour non compris dans la plage 200-399 ou inconnu.</span><span class="sxs-lookup"><span data-stu-id="19c30-152">A failure is any return code that is not in the range 200-399, or unknown.</span></span>

> [!NOTE]
> <span data-ttu-id="19c30-153">**100 % d’échecs ?**</span><span class="sxs-lookup"><span data-stu-id="19c30-153">**100% failures?**</span></span> <span data-ttu-id="19c30-154">Cela signifie probablement que vous obtenez uniquement des données de dépendances partielles.</span><span class="sxs-lookup"><span data-stu-id="19c30-154">- This probably indicates that you are only getting partial dependency data.</span></span> <span data-ttu-id="19c30-155">Vous devez [configurer une surveillance des dépendances adaptée à votre plateforme](#set-up-dependency-monitoring).</span><span class="sxs-lookup"><span data-stu-id="19c30-155">You need to [set up dependency monitoring appropriate to your platform](#set-up-dependency-monitoring).</span></span>
>
>

## <a name="ajax-calls"></a><span data-ttu-id="19c30-156">Appels AJAX</span><span class="sxs-lookup"><span data-stu-id="19c30-156">AJAX Calls</span></span>
<span data-ttu-id="19c30-157">Le panneau Navigateurs affiche la durée et le taux d’échec des appels AJAX à partir de [JavaScript dans vos pages web](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="19c30-157">The Browsers blade shows the duration and failure rate of AJAX calls from [JavaScript in your web pages](app-insights-javascript.md).</span></span> <span data-ttu-id="19c30-158">Ils sont affichés en tant que dépendances.</span><span class="sxs-lookup"><span data-stu-id="19c30-158">They are shown as Dependencies.</span></span>

## <span data-ttu-id="19c30-159"><a name="diagnosis"></a> Diagnostiquer les demandes lentes</span><span class="sxs-lookup"><span data-stu-id="19c30-159"><a name="diagnosis"></a> Diagnose slow requests</span></span>
<span data-ttu-id="19c30-160">Chaque événement de demande est associé aux appels de dépendances, exceptions et autres événements qui sont suivis pendant que votre application traite la demande.</span><span class="sxs-lookup"><span data-stu-id="19c30-160">Each request event is associated with the dependency calls, exceptions and other events that are tracked while your app is processing the request.</span></span> <span data-ttu-id="19c30-161">Ainsi, si certaines demandes présentent de médiocres performances, vous pouvez savoir si cela est dû à la lenteur des réponses d’une dépendance.</span><span class="sxs-lookup"><span data-stu-id="19c30-161">So if some requests are performing badly, you can find out whether it's due to slow responses from a dependency.</span></span>

<span data-ttu-id="19c30-162">Prenons un exemple.</span><span class="sxs-lookup"><span data-stu-id="19c30-162">Let's walk through an example of that.</span></span>

### <a name="tracing-from-requests-to-dependencies"></a><span data-ttu-id="19c30-163">Traçage des demandes aux dépendances</span><span class="sxs-lookup"><span data-stu-id="19c30-163">Tracing from requests to dependencies</span></span>
<span data-ttu-id="19c30-164">Ouvrez le panneau Performances et examinez la grille des demandes :</span><span class="sxs-lookup"><span data-stu-id="19c30-164">Open the Performance blade, and look at the grid of requests:</span></span>

![Liste de demandes avec moyennes et nombres](./media/app-insights-asp-net-dependencies/02-reqs.png)

<span data-ttu-id="19c30-166">La durée de la première est très longue.</span><span class="sxs-lookup"><span data-stu-id="19c30-166">The top one is taking very long.</span></span> <span data-ttu-id="19c30-167">Examinons-la pour en savoir plus.</span><span class="sxs-lookup"><span data-stu-id="19c30-167">Let's see if we can find out where the time is spent.</span></span>

<span data-ttu-id="19c30-168">Cliquez sur cette ligne pour afficher les événements de la demande :</span><span class="sxs-lookup"><span data-stu-id="19c30-168">Click that row to see individual request events:</span></span>

![Liste des occurrences de demande](./media/app-insights-asp-net-dependencies/03-instances.png)

<span data-ttu-id="19c30-170">Cliquez sur n’importe quelle instance de longue durée pour l’examiner de plus près, et faites défiler la page jusqu’aux appels de dépendances distantes associés à cette demande :</span><span class="sxs-lookup"><span data-stu-id="19c30-170">Click any long-running instance to inspect it further, and scroll down to the remote dependency calls related to this request:</span></span>

![Rechercher des appels de dépendances distantes, identifier une durée anormale](./media/app-insights-asp-net-dependencies/04-dependencies.png)

<span data-ttu-id="19c30-172">Il semble que la plupart du temps passé au traitement de cette demande ait été consacré à l’appel d’un service local.</span><span class="sxs-lookup"><span data-stu-id="19c30-172">It looks like most of the time servicing this request was spent in a call to a local service.</span></span>

<span data-ttu-id="19c30-173">Sélectionnez cette ligne pour obtenir plus d’informations :</span><span class="sxs-lookup"><span data-stu-id="19c30-173">Select that row to get more information:</span></span>

![Cliquez sur cette dépendance distante pour identifier la cause](./media/app-insights-asp-net-dependencies/05-detail.png)

<span data-ttu-id="19c30-175">Il semblerait que ce soit la cause du problème.</span><span class="sxs-lookup"><span data-stu-id="19c30-175">Looks like this is where the problem is.</span></span> <span data-ttu-id="19c30-176">Maintenant que nous avons identifié le problème, il nous suffit de découvrir pourquoi cet appel est si lent.</span><span class="sxs-lookup"><span data-stu-id="19c30-176">We've pinpointed the problem, so now we just need to find out why that call is taking so long.</span></span>

### <a name="request-timeline"></a><span data-ttu-id="19c30-177">Chronologie de demande</span><span class="sxs-lookup"><span data-stu-id="19c30-177">Request timeline</span></span>
<span data-ttu-id="19c30-178">Dans un autre cas, aucun appel de dépendance n’est particulièrement long.</span><span class="sxs-lookup"><span data-stu-id="19c30-178">In a different case, there is no dependency call that is particularly long.</span></span> <span data-ttu-id="19c30-179">Mais en basculant vers la vue chronologique, nous pouvons voir où le délai s’est produit dans notre traitement interne :</span><span class="sxs-lookup"><span data-stu-id="19c30-179">But by switching to the timeline view, we can see where the delay occurred in our internal processing:</span></span>

![Rechercher des appels de dépendances distantes, identifier une durée anormale](./media/app-insights-asp-net-dependencies/04-1.png)

<span data-ttu-id="19c30-181">Il semble y avoir un long délai après le premier appel de dépendance. Nous devons examiner notre code pour savoir pourquoi.</span><span class="sxs-lookup"><span data-stu-id="19c30-181">There seems to be a big gap after the first dependency call, so we should look at our code to see why that is.</span></span>

### <a name="profile-your-live-site"></a><span data-ttu-id="19c30-182">Profiler votre site en ligne</span><span class="sxs-lookup"><span data-stu-id="19c30-182">Profile your live site</span></span>

<span data-ttu-id="19c30-183">Vous voulez savoir à quoi tout ce temps a été consacré ?</span><span class="sxs-lookup"><span data-stu-id="19c30-183">No idea where the time goes?</span></span> <span data-ttu-id="19c30-184">Le [profileur d’Application Insights](app-insights-profiler.md) effectue le suivi des appels HTTP vers votre site dynamique et vous indique les fonctions de votre code qui ont pris le plus de temps.</span><span class="sxs-lookup"><span data-stu-id="19c30-184">The [Application Insights profiler](app-insights-profiler.md) traces HTTP calls to your live site and shows you which functions in your code took the longest time.</span></span>

## <a name="failed-requests"></a><span data-ttu-id="19c30-185">Demandes ayant échoué</span><span class="sxs-lookup"><span data-stu-id="19c30-185">Failed requests</span></span>
<span data-ttu-id="19c30-186">Les échecs de demandes peuvent également être associés à des échecs d’appels de dépendances.</span><span class="sxs-lookup"><span data-stu-id="19c30-186">Failed requests might also be associated with failed calls to dependencies.</span></span> <span data-ttu-id="19c30-187">Là encore, nous pouvons tout parcourir d’un simple clic pour localiser le problème.</span><span class="sxs-lookup"><span data-stu-id="19c30-187">Again, we can click through to track down the problem.</span></span>

![Cliquez sur le graphique des demandes ayant échoué](./media/app-insights-asp-net-dependencies/06-fail.png)

<span data-ttu-id="19c30-189">Accédez à une occurrence d’une demande ayant échoué et examinez les événements associés.</span><span class="sxs-lookup"><span data-stu-id="19c30-189">Click through to an occurrence of a failed request, and look at its associated events.</span></span>

![Cliquez sur un type de demande, cliquez sur l’instance pour obtenir une vue différente de la même instance, cliquez dessus pour obtenir des informations relatives à l’exception.](./media/app-insights-asp-net-dependencies/07-faildetail.png)

## <a name="analytics"></a><span data-ttu-id="19c30-191">Analyse</span><span class="sxs-lookup"><span data-stu-id="19c30-191">Analytics</span></span>
<span data-ttu-id="19c30-192">Vous pouvez suivre les dépendances dans le [langage de requête Log Analytics](https://docs.loganalytics.io/).</span><span class="sxs-lookup"><span data-stu-id="19c30-192">You can track dependencies in the [Log Analytics query language](https://docs.loganalytics.io/).</span></span> <span data-ttu-id="19c30-193">Voici quelques exemples.</span><span class="sxs-lookup"><span data-stu-id="19c30-193">Here are some examples.</span></span>

* <span data-ttu-id="19c30-194">Rechercher les appels de dépendances ayant échoué :</span><span class="sxs-lookup"><span data-stu-id="19c30-194">Find any failed dependency calls:</span></span>

```

    dependencies | where success != "True" | take 10
```

* <span data-ttu-id="19c30-195">Rechercher les appels AJAX :</span><span class="sxs-lookup"><span data-stu-id="19c30-195">Find AJAX calls:</span></span>

```

    dependencies | where client_Type == "Browser" | take 10
```

* <span data-ttu-id="19c30-196">Rechercher les appels de dépendances associés aux demandes :</span><span class="sxs-lookup"><span data-stu-id="19c30-196">Find dependency calls associated with requests:</span></span>

```

    dependencies
    | where timestamp > ago(1d) and  client_Type != "Browser"
    | join (requests | where timestamp > ago(1d))
      on operation_Id  
```


* <span data-ttu-id="19c30-197">Rechercher les appels AJAX associés à des pages consultées :</span><span class="sxs-lookup"><span data-stu-id="19c30-197">Find AJAX calls associated with page views:</span></span>

```

    dependencies
    | where timestamp > ago(1d) and  client_Type == "Browser"
    | join (browserTimings | where timestamp > ago(1d))
      on operation_Id
```



## <a name="custom-dependency-tracking"></a><span data-ttu-id="19c30-198">Suivi personnalisé des dépendances</span><span class="sxs-lookup"><span data-stu-id="19c30-198">Custom dependency tracking</span></span>
<span data-ttu-id="19c30-199">Le module de suivi des dépendances standard découvre automatiquement les dépendances externes, telles que des bases de données et des API REST.</span><span class="sxs-lookup"><span data-stu-id="19c30-199">The standard dependency-tracking module automatically discovers external dependencies such as databases and REST APIs.</span></span> <span data-ttu-id="19c30-200">Mais vous souhaiterez peut-être traiter d’autres composants de la même façon.</span><span class="sxs-lookup"><span data-stu-id="19c30-200">But you might want some additional components to be treated in the same way.</span></span>

<span data-ttu-id="19c30-201">Vous pouvez écrire du code qui envoie des informations de dépendance, en utilisant la même [API TrackDependency](app-insights-api-custom-events-metrics.md#trackdependency) que celle utilisée par les modules standard.</span><span class="sxs-lookup"><span data-stu-id="19c30-201">You can write code that sends dependency information, using the same [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency) that is used by the standard modules.</span></span>

<span data-ttu-id="19c30-202">Par exemple, si vous générez votre code avec un assembly que vous n’avez pas écrit vous-même, vous pouvez minuter tous les appels vers cet assembly afin de déterminer sa contribution dans votre temps de réponse.</span><span class="sxs-lookup"><span data-stu-id="19c30-202">For example, if you build your code with an assembly that you didn't write yourself, you could time all the calls to it, to find out what contribution it makes to your response times.</span></span> <span data-ttu-id="19c30-203">Pour afficher ces données dans les graphiques de dépendance d’Application Insights, envoyez-les en utilisant `TrackDependency`.</span><span class="sxs-lookup"><span data-stu-id="19c30-203">To have this data displayed in the dependency charts in Application Insights, send it using `TrackDependency`.</span></span>

```C#

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

<span data-ttu-id="19c30-204">Si vous souhaitez désactiver le module de suivi des dépendances standard, supprimez la référence à DependencyTrackingTelemetryModule dans [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md).</span><span class="sxs-lookup"><span data-stu-id="19c30-204">If you want to switch off the standard dependency tracking module, remove the reference to DependencyTrackingTelemetryModule in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="19c30-205">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="19c30-205">Troubleshooting</span></span>
<span data-ttu-id="19c30-206">*L’indicateur de réussite de la dépendance affiche toujours True ou False.*</span><span class="sxs-lookup"><span data-stu-id="19c30-206">*Dependency success flag always shows either true or false.*</span></span>

<span data-ttu-id="19c30-207">*La requête SQL n’est pas affichée en entier.*</span><span class="sxs-lookup"><span data-stu-id="19c30-207">*SQL query not shown in full.*</span></span>

* <span data-ttu-id="19c30-208">Effectuez une mise à niveau vers la dernière version du Kit de développement logiciel (SDK).</span><span class="sxs-lookup"><span data-stu-id="19c30-208">Upgrade to the latest version of the SDK.</span></span> <span data-ttu-id="19c30-209">Si votre version de .NET est inférieur à 4.6 :</span><span class="sxs-lookup"><span data-stu-id="19c30-209">If your .NET version is less than 4.6:</span></span>
  * <span data-ttu-id="19c30-210">Hôte IIS : installez l’[Agent Application Insights](app-insights-monitor-performance-live-website-now.md) sur les serveurs hôtes.</span><span class="sxs-lookup"><span data-stu-id="19c30-210">IIS host: Install [Application Insights Agent](app-insights-monitor-performance-live-website-now.md) on the host servers.</span></span>
  * <span data-ttu-id="19c30-211">Application web Azure : ouvrez l’onglet Application Insights dans le panneau de configuration de l’application web et installez Application Insights.</span><span class="sxs-lookup"><span data-stu-id="19c30-211">Azure web app: Open Application Insights tab in the web app control panel, and install Application Insights.</span></span>

## <a name="video"></a><span data-ttu-id="19c30-212">Vidéo</span><span class="sxs-lookup"><span data-stu-id="19c30-212">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="19c30-213">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="19c30-213">Next steps</span></span>
* [<span data-ttu-id="19c30-214">Exceptions</span><span class="sxs-lookup"><span data-stu-id="19c30-214">Exceptions</span></span>](app-insights-asp-net-exceptions.md)
* [<span data-ttu-id="19c30-215">Données utilisateur et de page</span><span class="sxs-lookup"><span data-stu-id="19c30-215">User & page data</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="19c30-216">Disponibilité</span><span class="sxs-lookup"><span data-stu-id="19c30-216">Availability</span></span>](app-insights-monitor-web-app-availability.md)
