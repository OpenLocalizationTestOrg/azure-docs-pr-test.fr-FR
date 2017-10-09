---
title: "aaaDependency suivi des modifications dans l’Application Azure Insights | Documents Microsoft"
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
ms.openlocfilehash: e72f5465462ae8e64363cbbaa62911aff636c504
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-application-insights-dependency-tracking"></a><span data-ttu-id="fa7a0-103">Configurer Application Insights : suivi des dépendances</span><span class="sxs-lookup"><span data-stu-id="fa7a0-103">Set up Application Insights: Dependency tracking</span></span>
<span data-ttu-id="fa7a0-104">Un *dépendance* est un composant externe qui est appelé par votre application.</span><span class="sxs-lookup"><span data-stu-id="fa7a0-104">A *dependency* is an external component that is called by your app.</span></span> <span data-ttu-id="fa7a0-105">Il s’agit habituellement d’un service appelé à l’aide de HTTP, d’une base de données ou d’un système de fichiers.</span><span class="sxs-lookup"><span data-stu-id="fa7a0-105">It's typically a service called using HTTP, or a database, or a file system.</span></span> <span data-ttu-id="fa7a0-106">[Application Insights](app-insights-overview.md) mesure combien de temps votre application attend les dépendances et la fréquence à laquelle un appel de dépendance échoue.</span><span class="sxs-lookup"><span data-stu-id="fa7a0-106">[Application Insights](app-insights-overview.md) measures how long your application waits for dependencies and how often a dependency call fails.</span></span> <span data-ttu-id="fa7a0-107">Vous pouvez examiner les appels spécifiques et les associer à toorequests et les exceptions.</span><span class="sxs-lookup"><span data-stu-id="fa7a0-107">You can investigate specific calls, and relate them toorequests and exceptions.</span></span>

![Exemples de graphiques](./media/app-insights-asp-net-dependencies/10-intro.png)

<span data-ttu-id="fa7a0-109">Moniteur de dépendance d’out of box Hello indique actuellement types toothese d’appels de dépendances :</span><span class="sxs-lookup"><span data-stu-id="fa7a0-109">hello out-of-the-box dependency monitor currently reports calls toothese  types of dependencies:</span></span>

* <span data-ttu-id="fa7a0-110">Serveur</span><span class="sxs-lookup"><span data-stu-id="fa7a0-110">Server</span></span>
  * <span data-ttu-id="fa7a0-111">Bases de données SQL</span><span class="sxs-lookup"><span data-stu-id="fa7a0-111">SQL databases</span></span>
  * <span data-ttu-id="fa7a0-112">Services web et WCF d’ASP.NET qui utilisent des liaisons HTTP</span><span class="sxs-lookup"><span data-stu-id="fa7a0-112">ASP.NET web and WCF services that use HTTP-based bindings</span></span>
  * <span data-ttu-id="fa7a0-113">Appels HTTP locaux ou distants</span><span class="sxs-lookup"><span data-stu-id="fa7a0-113">Local or remote HTTP calls</span></span>
  * <span data-ttu-id="fa7a0-114">Azure Cosmos DB, table, stockage d’objets blob et file d’attente</span><span class="sxs-lookup"><span data-stu-id="fa7a0-114">Azure Cosmos DB, table, blob storage, and queue</span></span>
* <span data-ttu-id="fa7a0-115">Pages web</span><span class="sxs-lookup"><span data-stu-id="fa7a0-115">Web pages</span></span>
  * <span data-ttu-id="fa7a0-116">Appels AJAX</span><span class="sxs-lookup"><span data-stu-id="fa7a0-116">AJAX calls</span></span>

<span data-ttu-id="fa7a0-117">La surveillance fonctionne en utilisant l’[instrumentation de code octet](https://msdn.microsoft.com/library/z9z62c29.aspx) autour des méthodes sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="fa7a0-117">Monitoring works by using [byte code instrumentation](https://msdn.microsoft.com/library/z9z62c29.aspx) around selected methods.</span></span> <span data-ttu-id="fa7a0-118">La surcharge de performances est minime.</span><span class="sxs-lookup"><span data-stu-id="fa7a0-118">Performance overhead is minimal.</span></span>

<span data-ttu-id="fa7a0-119">Vous pouvez également écrire votre propre SDK appelle toomonitor autres dépendances, à la fois dans le code client et serveur de hello, à l’aide de hello [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span><span class="sxs-lookup"><span data-stu-id="fa7a0-119">You can also write your own SDK calls toomonitor other dependencies, both in hello client and server code, using hello [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span></span>

## <a name="set-up-dependency-monitoring"></a><span data-ttu-id="fa7a0-120">Configurer la surveillance des dépendances</span><span class="sxs-lookup"><span data-stu-id="fa7a0-120">Set up dependency monitoring</span></span>
<span data-ttu-id="fa7a0-121">Informations de dépendance partiel sont automatiquement collectées par hello [Application Insights SDK](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="fa7a0-121">Partial dependency information is collected automatically by hello [Application Insights SDK](app-insights-asp-net.md).</span></span> <span data-ttu-id="fa7a0-122">tooget complète des données, installez agent approprié de hello pour le serveur hôte de hello.</span><span class="sxs-lookup"><span data-stu-id="fa7a0-122">tooget complete data, install hello appropriate agent for hello host server.</span></span>

| <span data-ttu-id="fa7a0-123">Plateforme</span><span class="sxs-lookup"><span data-stu-id="fa7a0-123">Platform</span></span> | <span data-ttu-id="fa7a0-124">Installer</span><span class="sxs-lookup"><span data-stu-id="fa7a0-124">Install</span></span> |
| --- | --- |
| <span data-ttu-id="fa7a0-125">Serveur IIS</span><span class="sxs-lookup"><span data-stu-id="fa7a0-125">IIS Server</span></span> |<span data-ttu-id="fa7a0-126">Soit [installer Status Monitor sur votre serveur](app-insights-monitor-performance-live-website-now.md) ou [mise à niveau de votre infrastructure d’application too.NET 4.6 ou version ultérieure](http://go.microsoft.com/fwlink/?LinkId=528259) et installer hello [Application Insights SDK](app-insights-asp-net.md) dans votre application.</span><span class="sxs-lookup"><span data-stu-id="fa7a0-126">Either [install Status Monitor on your server](app-insights-monitor-performance-live-website-now.md) or [Upgrade your application too.NET framework 4.6 or later](http://go.microsoft.com/fwlink/?LinkId=528259) and install hello [Application Insights SDK](app-insights-asp-net.md)  in your app.</span></span> |
| <span data-ttu-id="fa7a0-127">Application web Azure</span><span class="sxs-lookup"><span data-stu-id="fa7a0-127">Azure Web App</span></span> |<span data-ttu-id="fa7a0-128">Dans le panneau de configuration web app, [panneau d’Application Insights hello ouvert dans le panneau de configuration web application](app-insights-azure-web-apps.md) et choisir l’installation si vous y êtes invité.</span><span class="sxs-lookup"><span data-stu-id="fa7a0-128">In your web app control panel, [open hello Application Insights blade in your web app control panel](app-insights-azure-web-apps.md) and choose Install if prompted.</span></span> |
| <span data-ttu-id="fa7a0-129">Service cloud Azure</span><span class="sxs-lookup"><span data-stu-id="fa7a0-129">Azure Cloud Service</span></span> |<span data-ttu-id="fa7a0-130">[Utilisez une tâche de démarrage](app-insights-cloudservices.md) ou [installez le .NET Framework version 4.6 ou ultérieure](../cloud-services/cloud-services-dotnet-install-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="fa7a0-130">[Use startup task](app-insights-cloudservices.md) or [Install .NET framework 4.6+](../cloud-services/cloud-services-dotnet-install-dotnet.md)</span></span> |

## <a name="where-toofind-dependency-data"></a><span data-ttu-id="fa7a0-131">Où les données de dépendance toofind</span><span class="sxs-lookup"><span data-stu-id="fa7a0-131">Where toofind dependency data</span></span>
* <span data-ttu-id="fa7a0-132">[Mise en correspondance d’applications](#application-map) visualise les dépendances entre votre application et les composants voisins.</span><span class="sxs-lookup"><span data-stu-id="fa7a0-132">[Application Map](#application-map) visualizes dependencies between your app and neighbouring components.</span></span>
* <span data-ttu-id="fa7a0-133">[Les panneaux de performances, de navigateurs et d’échecs](#performance-and-blades) affichent les données sur les dépendances de serveur.</span><span class="sxs-lookup"><span data-stu-id="fa7a0-133">[Performance, browser, and failure blades](#performance-and-blades) show server dependency data.</span></span>
* <span data-ttu-id="fa7a0-134">[Les panneaux de navigateurs](#ajax-calls) montrent les appels AJAX provenant des navigateurs de vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="fa7a0-134">[Browsers blade](#ajax-calls) shows AJAX calls from your users' browsers.</span></span>
* <span data-ttu-id="fa7a0-135">[Parcourez les requêtes lents ou ayant échoué](#diagnose-slow-requests) toocheck appelle de leurs dépendances.</span><span class="sxs-lookup"><span data-stu-id="fa7a0-135">[Click through from slow or failed requests](#diagnose-slow-requests) toocheck their dependency calls.</span></span>
* <span data-ttu-id="fa7a0-136">[Analytique](#analytics) peuvent être des données de dépendance tooquery utilisé.</span><span class="sxs-lookup"><span data-stu-id="fa7a0-136">[Analytics](#analytics) can be used tooquery dependency data.</span></span>

## <a name="application-map"></a><span data-ttu-id="fa7a0-137">Plan de l’application</span><span class="sxs-lookup"><span data-stu-id="fa7a0-137">Application Map</span></span>
<span data-ttu-id="fa7a0-138">Mappage d’application agit comme un dépendances de toodiscovering aide visuelle entre les composants hello de votre application.</span><span class="sxs-lookup"><span data-stu-id="fa7a0-138">Application Map acts as a visual aid toodiscovering dependencies between hello components of your application.</span></span> <span data-ttu-id="fa7a0-139">Il est automatiquement généré à partir de la télémétrie hello à partir de votre application.</span><span class="sxs-lookup"><span data-stu-id="fa7a0-139">It is automatically generated from hello telemetry from your app.</span></span> <span data-ttu-id="fa7a0-140">Cet exemple montre les appels AJAX à partir de scripts de navigateur hello et reste à partir du serveur de hello services externes d’application tootwo.</span><span class="sxs-lookup"><span data-stu-id="fa7a0-140">This example shows AJAX calls from hello browser scripts and REST calls from hello server app tootwo external services.</span></span>

![Plan de l’application](./media/app-insights-asp-net-dependencies/08.png)

* <span data-ttu-id="fa7a0-142">**Accédez à partir de boîtes de hello** toorelevant dépendance et autres graphiques.</span><span class="sxs-lookup"><span data-stu-id="fa7a0-142">**Navigate from hello boxes** toorelevant dependency and other charts.</span></span>
* <span data-ttu-id="fa7a0-143">**Mappage de code confidentiel hello** toohello [tableau de bord](app-insights-dashboards.md), où il ne sera pas complètement fonctionnelle.</span><span class="sxs-lookup"><span data-stu-id="fa7a0-143">**Pin hello map** toohello [dashboard](app-insights-dashboards.md), where it will be fully functional.</span></span>

<span data-ttu-id="fa7a0-144">[En savoir plus](app-insights-app-map.md).</span><span class="sxs-lookup"><span data-stu-id="fa7a0-144">[Learn more](app-insights-app-map.md).</span></span>

## <a name="performance-and-failure-blades"></a><span data-ttu-id="fa7a0-145">Panneaux de performances et d’échecs</span><span class="sxs-lookup"><span data-stu-id="fa7a0-145">Performance and failure blades</span></span>
<span data-ttu-id="fa7a0-146">Panneau de performances Hello montre la durée hello d’appels de dépendance effectués par l’application de serveur hello.</span><span class="sxs-lookup"><span data-stu-id="fa7a0-146">hello performance blade shows hello duration of dependency calls made by hello server app.</span></span> <span data-ttu-id="fa7a0-147">Il existe un graphique de synthèse et un tableau segmenté par appel.</span><span class="sxs-lookup"><span data-stu-id="fa7a0-147">There's a summary chart and a table segmented by call.</span></span>

![Graphiques de dépendances du panneau de performances](./media/app-insights-asp-net-dependencies/dependencies-in-performance-blade.png)

<span data-ttu-id="fa7a0-149">Cliquez sur les graphiques de résumé hello ou hello table éléments toosearch brut occurrences de ces appels.</span><span class="sxs-lookup"><span data-stu-id="fa7a0-149">Click through hello summary charts or hello table items toosearch raw occurrences of these calls.</span></span>

![Instances d’appels de dépendances](./media/app-insights-asp-net-dependencies/dependency-call-instance.png)

<span data-ttu-id="fa7a0-151">**Nombre d’échecs** figurent sur hello **échecs** panneau.</span><span class="sxs-lookup"><span data-stu-id="fa7a0-151">**Failure counts** are shown on hello **Failures** blade.</span></span> <span data-ttu-id="fa7a0-152">Une défaillance est tout code de retour n’est pas de hello plage 200-399, ou inconnu.</span><span class="sxs-lookup"><span data-stu-id="fa7a0-152">A failure is any return code that is not in hello range 200-399, or unknown.</span></span>

> [!NOTE]
> <span data-ttu-id="fa7a0-153">**100 % d’échecs ?**</span><span class="sxs-lookup"><span data-stu-id="fa7a0-153">**100% failures?**</span></span> <span data-ttu-id="fa7a0-154">Cela signifie probablement que vous obtenez uniquement des données de dépendances partielles.</span><span class="sxs-lookup"><span data-stu-id="fa7a0-154">- This probably indicates that you are only getting partial dependency data.</span></span> <span data-ttu-id="fa7a0-155">Vous devez trop[configurer tooyour approprié plateforme d’analyse de dépendance](#set-up-dependency-monitoring).</span><span class="sxs-lookup"><span data-stu-id="fa7a0-155">You need too[set up dependency monitoring appropriate tooyour platform](#set-up-dependency-monitoring).</span></span>
>
>

## <a name="ajax-calls"></a><span data-ttu-id="fa7a0-156">Appels AJAX</span><span class="sxs-lookup"><span data-stu-id="fa7a0-156">AJAX Calls</span></span>
<span data-ttu-id="fa7a0-157">Panneau de navigateurs Hello montre la durée de hello et taux d’échec d’AJAX appelle à partir de [JavaScript dans vos pages web](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="fa7a0-157">hello Browsers blade shows hello duration and failure rate of AJAX calls from [JavaScript in your web pages](app-insights-javascript.md).</span></span> <span data-ttu-id="fa7a0-158">Ils sont affichés en tant que dépendances.</span><span class="sxs-lookup"><span data-stu-id="fa7a0-158">They are shown as Dependencies.</span></span>

## <span data-ttu-id="fa7a0-159"><a name="diagnosis"></a> Diagnostiquer les demandes lentes</span><span class="sxs-lookup"><span data-stu-id="fa7a0-159"><a name="diagnosis"></a> Diagnose slow requests</span></span>
<span data-ttu-id="fa7a0-160">Chaque événement de requête est associé à des appels de dépendance hello, exceptions et autres événements qui sont suivies lors du traitement de votre application hello demande.</span><span class="sxs-lookup"><span data-stu-id="fa7a0-160">Each request event is associated with hello dependency calls, exceptions and other events that are tracked while your app is processing hello request.</span></span> <span data-ttu-id="fa7a0-161">Si vous effectuant certaines demandes mal, vous pouvez trouver si elle est en raison de réponses tooslow à partir d’une dépendance.</span><span class="sxs-lookup"><span data-stu-id="fa7a0-161">So if some requests are performing badly, you can find out whether it's due tooslow responses from a dependency.</span></span>

<span data-ttu-id="fa7a0-162">Prenons un exemple.</span><span class="sxs-lookup"><span data-stu-id="fa7a0-162">Let's walk through an example of that.</span></span>

### <a name="tracing-from-requests-toodependencies"></a><span data-ttu-id="fa7a0-163">Le suivi de demandes toodependencies</span><span class="sxs-lookup"><span data-stu-id="fa7a0-163">Tracing from requests toodependencies</span></span>
<span data-ttu-id="fa7a0-164">Ouvrez le panneau de performances hello et observez la grille hello de demandes :</span><span class="sxs-lookup"><span data-stu-id="fa7a0-164">Open hello Performance blade, and look at hello grid of requests:</span></span>

![Liste de demandes avec moyennes et nombres](./media/app-insights-asp-net-dependencies/02-reqs.png)

<span data-ttu-id="fa7a0-166">haut Hello un est très longue.</span><span class="sxs-lookup"><span data-stu-id="fa7a0-166">hello top one is taking very long.</span></span> <span data-ttu-id="fa7a0-167">Voyons si nous pouvons découvrir où hello durée.</span><span class="sxs-lookup"><span data-stu-id="fa7a0-167">Let's see if we can find out where hello time is spent.</span></span>

<span data-ttu-id="fa7a0-168">Cliquez sur cette ligne toosee les événements de demande individuelle :</span><span class="sxs-lookup"><span data-stu-id="fa7a0-168">Click that row toosee individual request events:</span></span>

![Liste des occurrences de demande](./media/app-insights-asp-net-dependencies/03-instances.png)

<span data-ttu-id="fa7a0-170">Cliquez sur n’importe quel tooinspect d’instance longue il plus et faites défiler toohello dépendance distant appels connexes toothis demande :</span><span class="sxs-lookup"><span data-stu-id="fa7a0-170">Click any long-running instance tooinspect it further, and scroll down toohello remote dependency calls related toothis request:</span></span>

![Rechercher des dépendances de tooRemote d’appels, d’identifier la durée inhabituelle](./media/app-insights-asp-net-dependencies/04-dependencies.png)

<span data-ttu-id="fa7a0-172">Il semble que la plupart des hello maintenance de temps passé à cette demande dans un service d’appel tooa local.</span><span class="sxs-lookup"><span data-stu-id="fa7a0-172">It looks like most of hello time servicing this request was spent in a call tooa local service.</span></span>

<span data-ttu-id="fa7a0-173">Sélectionnez cette ligne de tooget plus d’informations :</span><span class="sxs-lookup"><span data-stu-id="fa7a0-173">Select that row tooget more information:</span></span>

![Parcourez cette dépendance à distance tooidentify hello soient à l’origine](./media/app-insights-asp-net-dependencies/05-detail.png)

<span data-ttu-id="fa7a0-175">Il semble que c’est là problème de hello.</span><span class="sxs-lookup"><span data-stu-id="fa7a0-175">Looks like this is where hello problem is.</span></span> <span data-ttu-id="fa7a0-176">Nous avez correspondant à des problème de hello, donc maintenant nous juste besoin toofind out pourquoi cet appel prend autant de temps.</span><span class="sxs-lookup"><span data-stu-id="fa7a0-176">We've pinpointed hello problem, so now we just need toofind out why that call is taking so long.</span></span>

### <a name="request-timeline"></a><span data-ttu-id="fa7a0-177">Chronologie de demande</span><span class="sxs-lookup"><span data-stu-id="fa7a0-177">Request timeline</span></span>
<span data-ttu-id="fa7a0-178">Dans un autre cas, aucun appel de dépendance n’est particulièrement long.</span><span class="sxs-lookup"><span data-stu-id="fa7a0-178">In a different case, there is no dependency call that is particularly long.</span></span> <span data-ttu-id="fa7a0-179">Mais en basculant l’affichage de la chronologie toohello, nous pouvons voir où le délai de hello s’est produite dans notre traitement interne :</span><span class="sxs-lookup"><span data-stu-id="fa7a0-179">But by switching toohello timeline view, we can see where hello delay occurred in our internal processing:</span></span>

![Rechercher des dépendances de tooRemote d’appels, d’identifier la durée inhabituelle](./media/app-insights-asp-net-dependencies/04-1.png)

<span data-ttu-id="fa7a0-181">Il semble toobe un grand écart après le premier appel de dépendance hello, donc nous devons examiner notre toosee code pourquoi qui est.</span><span class="sxs-lookup"><span data-stu-id="fa7a0-181">There seems toobe a big gap after hello first dependency call, so we should look at our code toosee why that is.</span></span>

### <a name="profile-your-live-site"></a><span data-ttu-id="fa7a0-182">Profiler votre site en ligne</span><span class="sxs-lookup"><span data-stu-id="fa7a0-182">Profile your live site</span></span>

<span data-ttu-id="fa7a0-183">Aucune idée où des temps de hello ? Hello [profileur d’Application Insights](app-insights-profiler.md) suivis HTTP appelle tooyour site en ligne et vous montre les fonctions dans votre code a duré plus longtemps hello.</span><span class="sxs-lookup"><span data-stu-id="fa7a0-183">No idea where hello time goes? hello [Application Insights profiler](app-insights-profiler.md) traces HTTP calls tooyour live site and shows you which functions in your code took hello longest time.</span></span>

## <a name="failed-requests"></a><span data-ttu-id="fa7a0-184">Demandes ayant échoué</span><span class="sxs-lookup"><span data-stu-id="fa7a0-184">Failed requests</span></span>
<span data-ttu-id="fa7a0-185">Demandes ayant échoué peuvent également être associées toodependencies d’appels ayant échoué.</span><span class="sxs-lookup"><span data-stu-id="fa7a0-185">Failed requests might also be associated with failed calls toodependencies.</span></span> <span data-ttu-id="fa7a0-186">Là encore, nous pouvons cliquer tootrack problème de hello.</span><span class="sxs-lookup"><span data-stu-id="fa7a0-186">Again, we can click through tootrack down hello problem.</span></span>

![Cliquez sur le graphique de demandes ayant échoué hello](./media/app-insights-asp-net-dependencies/06-fail.png)

<span data-ttu-id="fa7a0-188">Parcourez occurrence tooan d’une demande ayant échouée et consulter ses événements associés.</span><span class="sxs-lookup"><span data-stu-id="fa7a0-188">Click through tooan occurrence of a failed request, and look at its associated events.</span></span>

![Cliquez sur un type de requête, cliquez sur hello tooget tooa autre vue d’instance de hello même instance, cliquez dessus tooget détails de l’exception.](./media/app-insights-asp-net-dependencies/07-faildetail.png)

## <a name="analytics"></a><span data-ttu-id="fa7a0-190">Analyse</span><span class="sxs-lookup"><span data-stu-id="fa7a0-190">Analytics</span></span>
<span data-ttu-id="fa7a0-191">Vous pouvez suivre les dépendances dans hello [de langage de requête Analytique de journal](https://docs.loganalytics.io/).</span><span class="sxs-lookup"><span data-stu-id="fa7a0-191">You can track dependencies in hello [Log Analytics query language](https://docs.loganalytics.io/).</span></span> <span data-ttu-id="fa7a0-192">Voici quelques exemples.</span><span class="sxs-lookup"><span data-stu-id="fa7a0-192">Here are some examples.</span></span>

* <span data-ttu-id="fa7a0-193">Rechercher les appels de dépendances ayant échoué :</span><span class="sxs-lookup"><span data-stu-id="fa7a0-193">Find any failed dependency calls:</span></span>

```

    dependencies | where success != "True" | take 10
```

* <span data-ttu-id="fa7a0-194">Rechercher les appels AJAX :</span><span class="sxs-lookup"><span data-stu-id="fa7a0-194">Find AJAX calls:</span></span>

```

    dependencies | where client_Type == "Browser" | take 10
```

* <span data-ttu-id="fa7a0-195">Rechercher les appels de dépendances associés aux demandes :</span><span class="sxs-lookup"><span data-stu-id="fa7a0-195">Find dependency calls associated with requests:</span></span>

```

    dependencies
    | where timestamp > ago(1d) and  client_Type != "Browser"
    | join (requests | where timestamp > ago(1d))
      on operation_Id  
```


* <span data-ttu-id="fa7a0-196">Rechercher les appels AJAX associés à des pages consultées :</span><span class="sxs-lookup"><span data-stu-id="fa7a0-196">Find AJAX calls associated with page views:</span></span>

```

    dependencies
    | where timestamp > ago(1d) and  client_Type == "Browser"
    | join (browserTimings | where timestamp > ago(1d))
      on operation_Id
```



## <a name="custom-dependency-tracking"></a><span data-ttu-id="fa7a0-197">Suivi personnalisé des dépendances</span><span class="sxs-lookup"><span data-stu-id="fa7a0-197">Custom dependency tracking</span></span>
<span data-ttu-id="fa7a0-198">module de suivi de la dépendance standard Hello découvre automatiquement les dépendances externes telles que les bases de données et les API REST.</span><span class="sxs-lookup"><span data-stu-id="fa7a0-198">hello standard dependency-tracking module automatically discovers external dependencies such as databases and REST APIs.</span></span> <span data-ttu-id="fa7a0-199">Toutefois, vous pouvez toobe de certains composants supplémentaires traité Bonjour même façon.</span><span class="sxs-lookup"><span data-stu-id="fa7a0-199">But you might want some additional components toobe treated in hello same way.</span></span>

<span data-ttu-id="fa7a0-200">Vous pouvez écrire du code qui envoie des informations de dépendance, à l’aide de hello même [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency) qui est utilisé par les modules standard hello.</span><span class="sxs-lookup"><span data-stu-id="fa7a0-200">You can write code that sends dependency information, using hello same [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency) that is used by hello standard modules.</span></span>

<span data-ttu-id="fa7a0-201">Par exemple, si vous générez votre code avec un assembly que vous n’avez pas l’écrire vous-même, tous les tooit d’appels hello impossible du temps, toofind effectue la contribution il tooyour réponse délai d’attente.</span><span class="sxs-lookup"><span data-stu-id="fa7a0-201">For example, if you build your code with an assembly that you didn't write yourself, you could time all hello calls tooit, toofind out what contribution it makes tooyour response times.</span></span> <span data-ttu-id="fa7a0-202">envoyer des données affichées dans les graphiques de dépendance hello dans Application Insights, toohave à l’aide de `TrackDependency`.</span><span class="sxs-lookup"><span data-stu-id="fa7a0-202">toohave this data displayed in hello dependency charts in Application Insights, send it using `TrackDependency`.</span></span>

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

<span data-ttu-id="fa7a0-203">Si vous souhaitez tooswitch désactiver le module de suivi hello dépendance standard, supprimez tooDependencyTrackingTelemetryModule de référence hello dans [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md).</span><span class="sxs-lookup"><span data-stu-id="fa7a0-203">If you want tooswitch off hello standard dependency tracking module, remove hello reference tooDependencyTrackingTelemetryModule in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="fa7a0-204">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="fa7a0-204">Troubleshooting</span></span>
<span data-ttu-id="fa7a0-205">*L’indicateur de réussite de la dépendance affiche toujours True ou False.*</span><span class="sxs-lookup"><span data-stu-id="fa7a0-205">*Dependency success flag always shows either true or false.*</span></span>

<span data-ttu-id="fa7a0-206">*La requête SQL n’est pas affichée en entier.*</span><span class="sxs-lookup"><span data-stu-id="fa7a0-206">*SQL query not shown in full.*</span></span>

* <span data-ttu-id="fa7a0-207">Mettre à niveau la version la plus récente du Kit de développement logiciel de hello toohello.</span><span class="sxs-lookup"><span data-stu-id="fa7a0-207">Upgrade toohello latest version of hello SDK.</span></span> <span data-ttu-id="fa7a0-208">Si votre version de .NET est inférieur à 4.6 :</span><span class="sxs-lookup"><span data-stu-id="fa7a0-208">If your .NET version is less than 4.6:</span></span>
  * <span data-ttu-id="fa7a0-209">Hôte IIS : installer [Application Insights Agent](app-insights-monitor-performance-live-website-now.md) sur les serveurs hôtes de hello.</span><span class="sxs-lookup"><span data-stu-id="fa7a0-209">IIS host: Install [Application Insights Agent](app-insights-monitor-performance-live-website-now.md) on hello host servers.</span></span>
  * <span data-ttu-id="fa7a0-210">Application web Azure : ouvrir Application Insights onglet hello web application le panneau de configuration et installez Application Insights.</span><span class="sxs-lookup"><span data-stu-id="fa7a0-210">Azure web app: Open Application Insights tab in hello web app control panel, and install Application Insights.</span></span>

## <a name="video"></a><span data-ttu-id="fa7a0-211">Vidéo</span><span class="sxs-lookup"><span data-stu-id="fa7a0-211">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="fa7a0-212">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fa7a0-212">Next steps</span></span>
* [<span data-ttu-id="fa7a0-213">Exceptions</span><span class="sxs-lookup"><span data-stu-id="fa7a0-213">Exceptions</span></span>](app-insights-asp-net-exceptions.md)
* [<span data-ttu-id="fa7a0-214">Données utilisateur et de page</span><span class="sxs-lookup"><span data-stu-id="fa7a0-214">User & page data</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="fa7a0-215">Disponibilité</span><span class="sxs-lookup"><span data-stu-id="fa7a0-215">Availability</span></span>](app-insights-monitor-web-app-availability.md)
