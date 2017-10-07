---
title: compteurs aaaPerformance dans Application Insights | Documents Microsoft
description: "Surveillez les compteurs de performances système et .NET personnalisés dans Application Insights."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 5b816f4c-a77a-4674-ae36-802ee3a2f56d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/11/2016
ms.author: bwren
ms.openlocfilehash: 0a51c225f1d1124c9e7fe89f34e747cb26a3589e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="system-performance-counters-in-application-insights"></a><span data-ttu-id="c17d1-103">Compteurs de performances système dans Application Insights</span><span class="sxs-lookup"><span data-stu-id="c17d1-103">System performance counters in Application Insights</span></span>
<span data-ttu-id="c17d1-104">Windows offre un large éventail de [compteurs de performance](http://www.codeproject.com/Articles/8590/An-Introduction-To-Performance-Counters) tels que le niveau d’occupation du processeur, la mémoire, le disque et l’utilisation du réseau.</span><span class="sxs-lookup"><span data-stu-id="c17d1-104">Windows provides a wide variety of [performance counters](http://www.codeproject.com/Articles/8590/An-Introduction-To-Performance-Counters) such as CPU occupancy, memory, disk, and network usage.</span></span> <span data-ttu-id="c17d1-105">Vous pouvez également définir les vôtres.</span><span class="sxs-lookup"><span data-stu-id="c17d1-105">You can also define your own.</span></span> <span data-ttu-id="c17d1-106">[Application Insights](app-insights-overview.md) peut afficher ces compteurs de performances si votre application s’exécute sous IIS sur un toowhich d’ordinateur hôte ou virtuel local vous ont un accès administratif.</span><span class="sxs-lookup"><span data-stu-id="c17d1-106">[Application Insights](app-insights-overview.md) can show these performance counters if your application is running under IIS on an on-premises host or virtual machine toowhich you have administrative access.</span></span> <span data-ttu-id="c17d1-107">graphiques de Hello indiquent l’application en temps réel de hello ressources tooyour disponible et peuvent aider à tooidentify équilibrage de charge entre des instances de serveur.</span><span class="sxs-lookup"><span data-stu-id="c17d1-107">hello charts indicate hello resources available tooyour live application, and can help tooidentify unbalanced load between server instances.</span></span>

<span data-ttu-id="c17d1-108">Les compteurs de performance s’affichent dans le panneau de serveurs hello, qui inclut une table qui segmente par instance de serveur.</span><span class="sxs-lookup"><span data-stu-id="c17d1-108">Performance counters appear in hello Servers blade, which includes a table that segments by server instance.</span></span>

![Compteurs de performances signalés dans Application Insights](./media/app-insights-performance-counters/counters-by-server-instance.png)

<span data-ttu-id="c17d1-110">(Les compteurs de performance ne sont pas disponibles pour les applications web Azure.</span><span class="sxs-lookup"><span data-stu-id="c17d1-110">(Performance counters aren't available for Azure Web Apps.</span></span> <span data-ttu-id="c17d1-111">Toutefois, vous pouvez [envoyer des Diagnostics Windows Azure tooApplication Insights](app-insights-azure-diagnostics.md).)</span><span class="sxs-lookup"><span data-stu-id="c17d1-111">But you can [send Azure Diagnostics tooApplication Insights](app-insights-azure-diagnostics.md).)</span></span>

## <a name="view-counters"></a><span data-ttu-id="c17d1-112">Afficher des compteurs</span><span class="sxs-lookup"><span data-stu-id="c17d1-112">View counters</span></span>
<span data-ttu-id="c17d1-113">Panneau de serveurs Hello affiche un ensemble par défaut des compteurs de performance.</span><span class="sxs-lookup"><span data-stu-id="c17d1-113">hello Servers blade shows a default set of performance counters.</span></span> 

<span data-ttu-id="c17d1-114">toosee autres compteurs, modifier des graphiques sur le panneau de serveurs hello hello, ou ouvrez un nouveau [Metrics Explorer](app-insights-metrics-explorer.md) panneau et ajouter des graphiques.</span><span class="sxs-lookup"><span data-stu-id="c17d1-114">toosee other counters, either edit hello charts on hello Servers blade, or open a new [Metrics Explorer](app-insights-metrics-explorer.md) blade and add new charts.</span></span> 

<span data-ttu-id="c17d1-115">les compteurs disponibles Hello sont répertoriés en tant que mesures lorsque vous modifiez un graphique.</span><span class="sxs-lookup"><span data-stu-id="c17d1-115">hello available counters are listed as metrics when you edit a chart.</span></span>

![Compteurs de performances signalés dans Application Insights](./media/app-insights-performance-counters/choose-performance-counters.png)

<span data-ttu-id="c17d1-117">Création de tous vos graphiques plus utiles dans un seul emplacement, toosee un [tableau de bord](app-insights-dashboards.md) et les épingler tooit.</span><span class="sxs-lookup"><span data-stu-id="c17d1-117">toosee all your most useful charts in one place, create a [dashboard](app-insights-dashboards.md) and pin them tooit.</span></span>

## <a name="add-counters"></a><span data-ttu-id="c17d1-118">Ajouter des compteurs</span><span class="sxs-lookup"><span data-stu-id="c17d1-118">Add counters</span></span>
<span data-ttu-id="c17d1-119">Si le compteur de performance hello n’est pas indiqué dans la liste des métriques hello, est que hello Application Insights SDK n’est pas sa collecte sur votre serveur web.</span><span class="sxs-lookup"><span data-stu-id="c17d1-119">If hello performance counter you want isn't shown in hello list of metrics, that's because hello Application Insights SDK isn't collecting it in your web server.</span></span> <span data-ttu-id="c17d1-120">Vous pouvez configurer toodo donc.</span><span class="sxs-lookup"><span data-stu-id="c17d1-120">You can configure it toodo so.</span></span>

1. <span data-ttu-id="c17d1-121">Découvrez les compteurs sont disponibles dans votre serveur à l’aide de cette commande PowerShell sur le serveur de hello :</span><span class="sxs-lookup"><span data-stu-id="c17d1-121">Find out what counters are available in your server by using this PowerShell command at hello server:</span></span>
   
    `Get-Counter -ListSet *`
   
    <span data-ttu-id="c17d1-122">(Voir [`Get-Counter`](https://technet.microsoft.com/library/hh849685.aspx).)</span><span class="sxs-lookup"><span data-stu-id="c17d1-122">(See [`Get-Counter`](https://technet.microsoft.com/library/hh849685.aspx).)</span></span>
2. <span data-ttu-id="c17d1-123">Ouvrez ApplicationInsights.config.</span><span class="sxs-lookup"><span data-stu-id="c17d1-123">Open ApplicationInsights.config.</span></span>
   
   * <span data-ttu-id="c17d1-124">Si vous avez ajouté Application Insights tooyour application pendant le développement, modifier ApplicationInsights.config dans votre projet, puis le redéployer tooyour serveurs.</span><span class="sxs-lookup"><span data-stu-id="c17d1-124">If you added Application Insights tooyour app during development, edit ApplicationInsights.config in your project, and then re-deploy it tooyour servers.</span></span>
   * <span data-ttu-id="c17d1-125">Si vous avez utilisé le moniteur d’état tooinstrument une application web lors de l’exécution, trouver ApplicationInsights.config dans le répertoire racine de hello de l’application hello dans IIS.</span><span class="sxs-lookup"><span data-stu-id="c17d1-125">If you used Status Monitor tooinstrument a web app at runtime, find ApplicationInsights.config in hello root directory of hello app in IIS.</span></span> <span data-ttu-id="c17d1-126">Mettez-le à jour dans chaque instance de serveur.</span><span class="sxs-lookup"><span data-stu-id="c17d1-126">Update it there in each server instance.</span></span>
3. <span data-ttu-id="c17d1-127">Modifiez la directive collecteur de performances hello :</span><span class="sxs-lookup"><span data-stu-id="c17d1-127">Edit hello performance collector directive:</span></span>
   
```XML
   
    <Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule, Microsoft.AI.PerfCounterCollector">
      <Counters>
        <Add PerformanceCounter="\Objects\Processes"/>
        <Add PerformanceCounter="\Sales(photo)\# Items Sold" ReportAs="Photo sales"/>
      </Counters>
    </Add>

```

<span data-ttu-id="c17d1-128">Vous pouvez capturer les compteurs standard et ceux que vous avez implémentés vous-même.</span><span class="sxs-lookup"><span data-stu-id="c17d1-128">You can capture both standard counters and those you have implemented yourself.</span></span> <span data-ttu-id="c17d1-129">`\Objects\Processes` est un exemple de compteur standard, disponible sur tous les systèmes Windows.</span><span class="sxs-lookup"><span data-stu-id="c17d1-129">`\Objects\Processes` is an example of a standard counter, available on all Windows systems.</span></span> <span data-ttu-id="c17d1-130">`\Sales(photo)\# Items Sold` est un exemple de compteur personnalisé qui peut être implémenté dans un service web.</span><span class="sxs-lookup"><span data-stu-id="c17d1-130">`\Sales(photo)\# Items Sold` is an example of a custom counter that might be implemented in a web service.</span></span> 

<span data-ttu-id="c17d1-131">format de Hello est `\Category(instance)\Counter"`, ou pour des catégories n’ayant pas d’instances, tout simplement `\Category\Counter`.</span><span class="sxs-lookup"><span data-stu-id="c17d1-131">hello format is `\Category(instance)\Counter"`, or for categories that don't have instances, just `\Category\Counter`.</span></span>

<span data-ttu-id="c17d1-132">`ReportAs`est requis pour les noms de compteur qui ne correspondent pas `[a-zA-Z()/-_ \.]+` -autrement dit, ils contiennent des caractères qui ne sont pas Bonjour ensembles suivants : lettres, round crochets, une barre oblique, trait d’union, un trait de soulignement, espace, le point.</span><span class="sxs-lookup"><span data-stu-id="c17d1-132">`ReportAs` is required for counter names that do not match `[a-zA-Z()/-_ \.]+` - that is, they contain characters that are not in hello following sets: letters, round brackets, forward slash, hyphen, underscore, space, dot.</span></span>

<span data-ttu-id="c17d1-133">Si vous spécifiez une instance, il est collecté comme une dimension « CounterInstanceName » de hello indiqué métrique.</span><span class="sxs-lookup"><span data-stu-id="c17d1-133">If you specify an instance, it will be collected as a dimension "CounterInstanceName" of hello reported metric.</span></span>

### <a name="collecting-performance-counters-in-code"></a><span data-ttu-id="c17d1-134">Collecte des compteurs de performances dans le code</span><span class="sxs-lookup"><span data-stu-id="c17d1-134">Collecting performance counters in code</span></span>
<span data-ttu-id="c17d1-135">compteurs de performances du système toocollect et envoyez-le tooApplication Insights, vous pouvez adapter extrait hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="c17d1-135">toocollect system performance counters and send them tooApplication Insights, you can adapt hello snippet below:</span></span>


``` C#

    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\.NET CLR Memory([replace-with-application-process-name])\# GC Handles", "GC Handles")));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

<span data-ttu-id="c17d1-136">Ou vous pouvez le faire hello la même chose avec les mesures personnalisées que vous avez créé :</span><span class="sxs-lookup"><span data-stu-id="c17d1-136">Or you can do hello same thing with custom metrics you created:</span></span>

``` C#
    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\Sales(photo)\# Items Sold", "Photo sales"));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

## <a name="performance-counters-in-analytics"></a><span data-ttu-id="c17d1-137">Compteurs de performances dans Analytics</span><span class="sxs-lookup"><span data-stu-id="c17d1-137">Performance counters in Analytics</span></span>
<span data-ttu-id="c17d1-138">Vous pouvez rechercher et afficher des rapports de compteur de performances dans [Analytics](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="c17d1-138">You can search and display performance counter reports in [Analytics](app-insights-analytics.md).</span></span>

<span data-ttu-id="c17d1-139">Hello **performanceCounters** schéma expose hello `category`, `counter` nom, et `instance` nom de chaque compteur de performance.</span><span class="sxs-lookup"><span data-stu-id="c17d1-139">hello **performanceCounters** schema exposes hello `category`, `counter` name, and `instance` name of each performance counter.</span></span>  <span data-ttu-id="c17d1-140">Télémétrie hello pour chaque application, vous voyez uniquement les compteurs de hello pour cette application.</span><span class="sxs-lookup"><span data-stu-id="c17d1-140">In hello telemetry for each application, you’ll see only hello counters for that application.</span></span> <span data-ttu-id="c17d1-141">Par exemple, toosee les compteurs sont disponibles :</span><span class="sxs-lookup"><span data-stu-id="c17d1-141">For example, toosee what counters are available:</span></span> 

![Compteurs de performances dans Application Insights Analytics](./media/app-insights-performance-counters/analytics-performance-counters.png)

<span data-ttu-id="c17d1-143">(« Instance » fait ici référence d’instance de compteur de performance toohello, ne Hello pas de rôle ou machine instance de serveur.</span><span class="sxs-lookup"><span data-stu-id="c17d1-143">('Instance' here refers toohello performance counter instance,  not hello role or server machine instance.</span></span> <span data-ttu-id="c17d1-144">Nom instance de compteur de performance Hello généralement segmente les compteurs de temps processeur par nom hello de hello processus ou l’application.)</span><span class="sxs-lookup"><span data-stu-id="c17d1-144">hello performance counter instance name typically segments counters such as processor time by hello name of hello process or application.)</span></span>

<span data-ttu-id="c17d1-145">tooget un graphique de mémoire disponible sur hello période récente :</span><span class="sxs-lookup"><span data-stu-id="c17d1-145">tooget a chart of available memory over hello recent period:</span></span> 

![Graphique temporel dans Application Insights Analytics](./media/app-insights-performance-counters/analytics-available-memory.png)

<span data-ttu-id="c17d1-147">Comme les autres données de télémétrie, **performanceCounters** possède également une colonne `cloud_RoleInstance` qui indique l’identité hello de l’instance de serveur hello hôte sur lequel votre application est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="c17d1-147">Like other telemetry, **performanceCounters** also has a column `cloud_RoleInstance` that indicates hello identity of hello host server instance on which your app is running.</span></span> <span data-ttu-id="c17d1-148">Par exemple, toocompare hello des performances de votre application sur des ordinateurs différents hello :</span><span class="sxs-lookup"><span data-stu-id="c17d1-148">For example, toocompare hello performance of your app on hello different machines:</span></span> 

![Performances segmentées par instances de rôle d’Application Insights Analytics](./media/app-insights-performance-counters/analytics-metrics-role-instance.png)

## <a name="aspnet-and-application-insights-counts"></a><span data-ttu-id="c17d1-150">Nombres ASP.NET et Application Insights</span><span class="sxs-lookup"><span data-stu-id="c17d1-150">ASP.NET and Application Insights counts</span></span>
<span data-ttu-id="c17d1-151">*Qu’est la différence hello entre le taux d’Exception hello et des métriques d’Exceptions ?*</span><span class="sxs-lookup"><span data-stu-id="c17d1-151">*What's hello difference between hello Exception rate and Exceptions metrics?*</span></span>

* <span data-ttu-id="c17d1-152">*taux d’exceptions* est un compteur de performances système.</span><span class="sxs-lookup"><span data-stu-id="c17d1-152">*Exception rate* is a system performance counter.</span></span> <span data-ttu-id="c17d1-153">Hello CLR compte tous les hello gérées et les exceptions non gérées levées et divisant le total de hello dans un intervalle d’échantillonnage par la longueur de l’intervalle de salutation hello.</span><span class="sxs-lookup"><span data-stu-id="c17d1-153">hello CLR counts all hello handled and unhandled exceptions that are thrown, and divides hello total in a sampling interval by hello length of hello interval.</span></span> <span data-ttu-id="c17d1-154">Hello Application Insights SDK collecte ce résultat et l’envoie toohello portal.</span><span class="sxs-lookup"><span data-stu-id="c17d1-154">hello Application Insights SDK collects this result and sends it toohello portal.</span></span>
* <span data-ttu-id="c17d1-155">*Exceptions* est le nombre de hello rapports TrackException reçues par le portail hello dans l’intervalle d’échantillonnage de hello du graphique de hello.</span><span class="sxs-lookup"><span data-stu-id="c17d1-155">*Exceptions* is a count of hello TrackException reports received by hello portal in hello sampling interval of hello chart.</span></span> <span data-ttu-id="c17d1-156">Il n’inclut que hello exceptions traitées où vous avez écrit TrackException appelle dans votre code et n’inclut pas tous [les exceptions non gérées](app-insights-asp-net-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="c17d1-156">It includes only hello handled exceptions where you have written TrackException calls in your code, and doesn't include all [unhandled exceptions](app-insights-asp-net-exceptions.md).</span></span> 

## <a name="alerts"></a><span data-ttu-id="c17d1-157">Alertes</span><span class="sxs-lookup"><span data-stu-id="c17d1-157">Alerts</span></span>
<span data-ttu-id="c17d1-158">Comme les autres mesures, vous pouvez [définir une alerte](app-insights-alerts.md) toowarn vous si un compteur de performance est en dehors d’une limite que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="c17d1-158">Like other metrics, you can [set an alert](app-insights-alerts.md) toowarn you if a performance counter goes outside a limit you specify.</span></span> <span data-ttu-id="c17d1-159">Ouvrez le panneau des alertes hello et cliquez sur Ajouter une alerte.</span><span class="sxs-lookup"><span data-stu-id="c17d1-159">Open hello Alerts blade and click Add Alert.</span></span>

## <span data-ttu-id="c17d1-160"><a name="next"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c17d1-160"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="c17d1-161">Suivi des dépendances</span><span class="sxs-lookup"><span data-stu-id="c17d1-161">Dependency tracking</span></span>](app-insights-asp-net-dependencies.md)
* [<span data-ttu-id="c17d1-162">Suivi des exceptions</span><span class="sxs-lookup"><span data-stu-id="c17d1-162">Exception tracking</span></span>](app-insights-asp-net-exceptions.md)

