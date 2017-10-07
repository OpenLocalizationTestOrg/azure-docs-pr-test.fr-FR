---
title: applications de Docker aaaMonitor dans Azure Application Insights | Documents Microsoft
description: "Exceptions, événements et compteurs de performance docker peuvent être affichées sur Application Insights, ainsi que les données de télémétrie hello à partir d’applications de hello placées dans des conteneurs."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 27a3083d-d67f-4a07-8f3c-4edb65a0a685
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 9aaf1076bae25485a396db1bb3dcd13bccd87c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-docker-applications-in-application-insights"></a><span data-ttu-id="037b7-103">Analyse des applications Docker dans Application Insights</span><span class="sxs-lookup"><span data-stu-id="037b7-103">Monitor Docker applications in Application Insights</span></span>
<span data-ttu-id="037b7-104">Les événements de cycle de vie et les compteurs de performances provenant de conteneurs [Docker](https://www.docker.com/) peuvent être représentés dans Application Insights.</span><span class="sxs-lookup"><span data-stu-id="037b7-104">Lifecycle events and performance counters from [Docker](https://www.docker.com/) containers can be charted on Application Insights.</span></span> <span data-ttu-id="037b7-105">Installer hello [Application Insights](app-insights-overview.md) image dans un conteneur dans votre hôte et il affiche les compteurs de performance pour l’hôte de hello, que bien que pour hello autres images.</span><span class="sxs-lookup"><span data-stu-id="037b7-105">Install hello [Application Insights](app-insights-overview.md) image in a container in your host, and it will display performance counters for hello host, as well as for hello other images.</span></span>

<span data-ttu-id="037b7-106">Avec Docker, vous distribuez vos applications dans des conteneurs légers avec toutes les dépendances.</span><span class="sxs-lookup"><span data-stu-id="037b7-106">With Docker, you distribute your apps in lightweight containers complete with all dependencies.</span></span> <span data-ttu-id="037b7-107">Elles s’exécuteront sur n’importe quelle machine hôte exécutant un moteur Docker.</span><span class="sxs-lookup"><span data-stu-id="037b7-107">They'll run on any host machine that runs a Docker Engine.</span></span>

<span data-ttu-id="037b7-108">Lorsque vous exécutez hello [image d’Application Insights](https://hub.docker.com/r/microsoft/applicationinsights/) sur l’hôte Docker, vous obtenez ces avantages :</span><span class="sxs-lookup"><span data-stu-id="037b7-108">When you run hello [Application Insights image](https://hub.docker.com/r/microsoft/applicationinsights/) on your Docker host, you get these benefits:</span></span>

* <span data-ttu-id="037b7-109">Cycle de vie des données de télémétrie sur tous les conteneurs hello en cours d’exécution sur l’ordinateur hôte de hello - Démarrer, arrêter et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="037b7-109">Lifecycle telemetry about all hello containers running on hello host - start, stop, and so on.</span></span>
* <span data-ttu-id="037b7-110">Compteurs de performances pour tous les conteneurs hello.</span><span class="sxs-lookup"><span data-stu-id="037b7-110">Performance counters for all hello containers.</span></span> <span data-ttu-id="037b7-111">Processeur, mémoire, utilisation du réseau, et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="037b7-111">CPU, memory, network usage, and more.</span></span>
* <span data-ttu-id="037b7-112">Si vous [installé le Kit de développement Application Insights pour Java](app-insights-java-live.md) dans les applications hello en cours d’exécution dans des conteneurs de hello, toutes les données de télémétrie hello de ces applications ont des propriétés supplémentaires identifiant le conteneur de hello et l’ordinateur hôte.</span><span class="sxs-lookup"><span data-stu-id="037b7-112">If you [installed Application Insights SDK for Java](app-insights-java-live.md) in hello apps running in hello containers, all hello telemetry of those apps will have additional properties identifying hello container and host machine.</span></span> <span data-ttu-id="037b7-113">Par exemple, si vous avez des instances d’une application en cours d’exécution dans plusieurs hôtes, vous pouvez facilement filtrer la télémétrie d’application par hôte.</span><span class="sxs-lookup"><span data-stu-id="037b7-113">So for example, if you have instances of an app running in more than one host, you can easily filter your app telemetry by host.</span></span>

![exemple](./media/app-insights-docker/00.png)

## <a name="set-up-your-application-insights-resource"></a><span data-ttu-id="037b7-115">Configuration de votre ressource Application Insights</span><span class="sxs-lookup"><span data-stu-id="037b7-115">Set up your Application Insights resource</span></span>
1. <span data-ttu-id="037b7-116">Connectez-vous à [portail Microsoft Azure](https://azure.com) et ouvrir la ressource d’Application Insights hello pour votre application ; ou [créer un nouveau](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="037b7-116">Sign into [Microsoft Azure portal](https://azure.com) and open hello Application Insights resource for your app; or [create a new one](app-insights-create-new-resource.md).</span></span> 
   
    <span data-ttu-id="037b7-117">*Quelle ressource dois-je utiliser ?*</span><span class="sxs-lookup"><span data-stu-id="037b7-117">*Which resource should I use?*</span></span> <span data-ttu-id="037b7-118">Si des applications hello qui vous sont en cours d’exécution sur votre ordinateur hôte ont été développées par quelqu'un d’autre, vous devez trop[créer une ressource Application Insights](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="037b7-118">If hello apps that you are running on your host were developed by someone else, then you need too[create a new Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="037b7-119">Il s’agit où vous permet d’afficher et analysez les données de télémétrie hello.</span><span class="sxs-lookup"><span data-stu-id="037b7-119">This is where you view and analyze hello telemetry.</span></span> <span data-ttu-id="037b7-120">(Sélectionnez « Général » pour le type d’application hello).</span><span class="sxs-lookup"><span data-stu-id="037b7-120">(Select 'General' for hello app type.)</span></span>
   
    <span data-ttu-id="037b7-121">Mais si vous êtes développeur hello des applications de hello, puis nous espérons que vous [ajouté Application Insights SDK](app-insights-java-live.md) tooeach d'entre eux.</span><span class="sxs-lookup"><span data-stu-id="037b7-121">But if you're hello developer of hello apps, then we hope you [added Application Insights SDK](app-insights-java-live.md) tooeach of them.</span></span> <span data-ttu-id="037b7-122">S’ils sont tous les composants réellement d’une application métier unique, puis vous pouvez configurer toutes les ressources de tooone toosend télémétrie, et vous utilisez ces même ressource toodisplay hello Docker du cycle de vie et les performances des données.</span><span class="sxs-lookup"><span data-stu-id="037b7-122">If they're all really components of a single business application, then you might configure all of them toosend telemetry tooone resource, and you'll use that same resource toodisplay hello Docker lifecycle and performance data.</span></span> 
   
    <span data-ttu-id="037b7-123">Un troisième scénario est que vous avez développé la plupart des applications de hello, mais que vous utilisez des ressources distinctes toodisplay leurs données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="037b7-123">A third scenario is that you developed most of hello apps, but you are using separate resources toodisplay their telemetry.</span></span> <span data-ttu-id="037b7-124">Dans ce cas, vous probablement aussi que vous souhaitez toocreate une ressource distincte pour hello des données de Docker.</span><span class="sxs-lookup"><span data-stu-id="037b7-124">In that case, you probably also want toocreate a separate resource for hello Docker data.</span></span> 
2. <span data-ttu-id="037b7-125">Ajouter une vignette Docker hello : choisissez **ajouter vignette**, faites glisser de la vignette de Docker hello à partir de la galerie de hello, puis cliquez sur **fait**.</span><span class="sxs-lookup"><span data-stu-id="037b7-125">Add hello Docker tile: Choose **Add Tile**, drag hello Docker tile from hello gallery, and then click **Done**.</span></span> 
   
    ![exemple](./media/app-insights-docker/03.png)
3. <span data-ttu-id="037b7-127">Cliquez sur hello **Essentials** liste déroulante et copiez la clé d’Instrumentation de hello.</span><span class="sxs-lookup"><span data-stu-id="037b7-127">Click hello **Essentials** drop-down and copy hello Instrumentation Key.</span></span> <span data-ttu-id="037b7-128">Vous utilisez ce Kit de développement logiciel de hello tootell où toosend ses données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="037b7-128">You use this tootell hello SDK where toosend its telemetry.</span></span>

    ![exemple](./media/app-insights-docker/02-props.png)

<span data-ttu-id="037b7-130">Gardez cette fenêtre de navigateur pratique, que vous y reviendrons tooit bientôt toolook au niveau de votre télémétrie.</span><span class="sxs-lookup"><span data-stu-id="037b7-130">Keep that browser window handy, as you'll come back tooit soon toolook at your telemetry.</span></span>

## <a name="run-hello-application-insights-monitor-on-your-host"></a><span data-ttu-id="037b7-131">Exécuter le moniteur de Application Insights hello sur votre ordinateur hôte</span><span class="sxs-lookup"><span data-stu-id="037b7-131">Run hello Application Insights monitor on your host</span></span>
<span data-ttu-id="037b7-132">Maintenant que vous avez quelque part télémétrie de hello toodisplay, vous pouvez définir l’application en conteneur hello qui recueille et envoyez-le.</span><span class="sxs-lookup"><span data-stu-id="037b7-132">Now that you've got somewhere toodisplay hello telemetry, you can set up hello containerized app that will collect and send it.</span></span>

1. <span data-ttu-id="037b7-133">Connecter l’hôte de Docker tooyour.</span><span class="sxs-lookup"><span data-stu-id="037b7-133">Connect tooyour Docker host.</span></span> 
2. <span data-ttu-id="037b7-134">Modifiez la clé d'instrumentation par cette commande, puis exécutez-la :</span><span class="sxs-lookup"><span data-stu-id="037b7-134">Edit your instrumentation key into this command, and then run it:</span></span>
   
   ```
   
   docker run -v /var/run/docker.sock:/docker.sock -d microsoft/applicationinsights ikey=000000-1111-2222-3333-444444444
   ```

<span data-ttu-id="037b7-135">Une seule image Application Insights est requise par hôte Docker.</span><span class="sxs-lookup"><span data-stu-id="037b7-135">Only one Application Insights image is required per Docker host.</span></span> <span data-ttu-id="037b7-136">Si votre application est déployée sur plusieurs hôtes de Docker, puis répétez la commande hello sur chaque hôte.</span><span class="sxs-lookup"><span data-stu-id="037b7-136">If your application is deployed on multiple Docker hosts, then repeat hello command on every host.</span></span>

## <a name="update-your-app"></a><span data-ttu-id="037b7-137">Mise à jour de votre application</span><span class="sxs-lookup"><span data-stu-id="037b7-137">Update your app</span></span>
<span data-ttu-id="037b7-138">Si votre application est instrumentée avec hello [Application Insights SDK pour Java](app-insights-java-get-started.md), ajouter hello ligne suivante dans fichier de ApplicationInsights.xml hello dans votre projet, sous hello `<TelemetryInitializers>` élément :</span><span class="sxs-lookup"><span data-stu-id="037b7-138">If your application is instrumented with hello [Application Insights SDK for Java](app-insights-java-get-started.md), add hello following line into hello ApplicationInsights.xml file in your project, under hello `<TelemetryInitializers>` element:</span></span>

```xml

    <Add type="com.microsoft.applicationinsights.extensibility.initializer.docker.DockerContextInitializer"/> 
```

<span data-ttu-id="037b7-139">Cela ajoute des informations de Docker comme conteneur hôte id tooevery télémétrie élément et envoyé à partir de votre application.</span><span class="sxs-lookup"><span data-stu-id="037b7-139">This adds Docker information such as container and host id tooevery telemetry item sent from your app.</span></span>

## <a name="view-your-telemetry"></a><span data-ttu-id="037b7-140">Affichage de vos données de télémétrie</span><span class="sxs-lookup"><span data-stu-id="037b7-140">View your telemetry</span></span>
<span data-ttu-id="037b7-141">Retournez une ressource d’Application Insights tooyour Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="037b7-141">Go back tooyour Application Insights resource in hello Azure portal.</span></span>

<span data-ttu-id="037b7-142">Cliquez dans la vignette de Docker hello.</span><span class="sxs-lookup"><span data-stu-id="037b7-142">Click through hello Docker tile.</span></span>

<span data-ttu-id="037b7-143">Vous verrez peu de temps des données en provenance de l’application de Docker hello, surtout si vous avez d’autres conteneurs exécutés sur votre moteur Docker.</span><span class="sxs-lookup"><span data-stu-id="037b7-143">You'll shortly see data arriving from hello Docker app, especially if you have other containers running on your Docker engine.</span></span>

<span data-ttu-id="037b7-144">Voici certaines des vues hello que vous pouvez obtenir.</span><span class="sxs-lookup"><span data-stu-id="037b7-144">Here are some of hello views you can get.</span></span>

### <a name="perf-counters-by-host-activity-by-image"></a><span data-ttu-id="037b7-145">Compteurs de performances par hôte, activité par image</span><span class="sxs-lookup"><span data-stu-id="037b7-145">Perf counters by host, activity by image</span></span>
![exemple](./media/app-insights-docker/10.png)

![exemple](./media/app-insights-docker/11.png)

<span data-ttu-id="037b7-148">Cliquez sur le nom d'un hôte ou d'une image pour plus de détails.</span><span class="sxs-lookup"><span data-stu-id="037b7-148">Click any host or image name for more detail.</span></span>

<span data-ttu-id="037b7-149">toocustomize hello, cliquez sur n’importe quel graphique, la grille hello titre ou ajouter un graphique.</span><span class="sxs-lookup"><span data-stu-id="037b7-149">toocustomize hello view, click any chart, hello grid heading, or use Add Chart.</span></span> 

<span data-ttu-id="037b7-150">[En savoir plus sur Metrics Explorer](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="037b7-150">[Learn more about metrics explorer](app-insights-metrics-explorer.md).</span></span>

### <a name="docker-container-events"></a><span data-ttu-id="037b7-151">Événements du conteneur Docker</span><span class="sxs-lookup"><span data-stu-id="037b7-151">Docker container events</span></span>
![exemple](./media/app-insights-docker/13.png)

<span data-ttu-id="037b7-153">tooinvestigate des événements individuels, cliquez sur [recherche](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="037b7-153">tooinvestigate individual events, click [Search](app-insights-diagnostic-search.md).</span></span> <span data-ttu-id="037b7-154">Rechercher et filtrer les événements de hello toofind souhaités.</span><span class="sxs-lookup"><span data-stu-id="037b7-154">Search and filter toofind hello events you want.</span></span> <span data-ttu-id="037b7-155">Cliquez sur n’importe quel tooget événement plus en détail.</span><span class="sxs-lookup"><span data-stu-id="037b7-155">Click any event tooget more detail.</span></span>

### <a name="exceptions-by-container-name"></a><span data-ttu-id="037b7-156">Exceptions par nom de conteneur</span><span class="sxs-lookup"><span data-stu-id="037b7-156">Exceptions by container name</span></span>
![exemple](./media/app-insights-docker/14.png)

### <a name="docker-context-added-tooapp-telemetry"></a><span data-ttu-id="037b7-158">Contexte de docker ajouté tooapp télémétrie</span><span class="sxs-lookup"><span data-stu-id="037b7-158">Docker context added tooapp telemetry</span></span>
<span data-ttu-id="037b7-159">Télémétrie des requêtes envoyée à partir de l’application hello instrumentée avec le Kit de développement logiciel AI, enrichie avec le contexte de Docker :</span><span class="sxs-lookup"><span data-stu-id="037b7-159">Request telemetry sent from hello application instrumented with AI SDK, enriched with Docker context:</span></span>

![exemple](./media/app-insights-docker/16.png)

<span data-ttu-id="037b7-161">Temps du processeur et compteurs de performance mémoire disponible, enrichis et regroupés par nom de conteneur Docker :</span><span class="sxs-lookup"><span data-stu-id="037b7-161">Processor time and available memory performance counters, enriched and grouped by Docker container name:</span></span>

![exemple](./media/app-insights-docker/15.png)

## <a name="q--a"></a><span data-ttu-id="037b7-163">Questions et réponses</span><span class="sxs-lookup"><span data-stu-id="037b7-163">Q & A</span></span>
<span data-ttu-id="037b7-164">*Quelles sont les fonctionnalités d’Application Insights qui ne sont pas disponibles dans Docker ?*</span><span class="sxs-lookup"><span data-stu-id="037b7-164">*What does Application Insights give me that I can't get from Docker?*</span></span>

* <span data-ttu-id="037b7-165">Analyse détaillée des compteurs de performances par conteneur et par image.</span><span class="sxs-lookup"><span data-stu-id="037b7-165">Detailed breakdown of performance counters by container and image.</span></span>
* <span data-ttu-id="037b7-166">Intégration des données de conteneur et d’application dans un tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="037b7-166">Integrate container and app data in one dashboard.</span></span>
* <span data-ttu-id="037b7-167">[Exporter les données de télémétrie](app-insights-export-telemetry.md) pour l’autre base de données analysis tooa, Power BI ou tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="037b7-167">[Export telemetry](app-insights-export-telemetry.md) for further analysis tooa database, Power BI or other dashboard.</span></span>

<span data-ttu-id="037b7-168">*Comment obtenir des données de télémétrie à partir de l’application hello proprement dit ?*</span><span class="sxs-lookup"><span data-stu-id="037b7-168">*How do I get telemetry from hello app itself?*</span></span>

* <span data-ttu-id="037b7-169">Installez hello Application Insights SDK dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="037b7-169">Install hello Application Insights SDK in hello app.</span></span> <span data-ttu-id="037b7-170">Découvrez comment faire pour : les [applications web Java](app-insights-java-get-started.md), les [applications web Windows](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="037b7-170">Learn how for: [Java web apps](app-insights-java-get-started.md), [Windows web apps](app-insights-asp-net.md).</span></span>

## <a name="video"></a><span data-ttu-id="037b7-171">Vidéo</span><span class="sxs-lookup"><span data-stu-id="037b7-171">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="037b7-172">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="037b7-172">Next steps</span></span>

* [<span data-ttu-id="037b7-173">Application Insights pour Java</span><span class="sxs-lookup"><span data-stu-id="037b7-173">Application Insights for Java</span></span>](app-insights-java-get-started.md)
* [<span data-ttu-id="037b7-174">Application Insights pour Node.js</span><span class="sxs-lookup"><span data-stu-id="037b7-174">Application Insights for Node.js</span></span>](app-insights-nodejs.md)
* [<span data-ttu-id="037b7-175">Application Insights pour ASP.NET</span><span class="sxs-lookup"><span data-stu-id="037b7-175">Application Insights for ASP.NET</span></span>](app-insights-asp-net.md)
