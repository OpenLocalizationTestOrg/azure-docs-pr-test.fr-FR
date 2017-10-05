---
title: "Surveiller les applications Docker dans Azure Application Insights | Microsoft Docs"
description: "Vous pouvez visualiser les compteurs de performances, les événements et les exceptions Docker dans Application Insights, avec les données de télémétrie des applications en conteneur."
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
ms.openlocfilehash: b082e345ca1bb3b12c548e05e699474d3aa9306c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-docker-applications-in-application-insights"></a><span data-ttu-id="5083b-103">Analyse des applications Docker dans Application Insights</span><span class="sxs-lookup"><span data-stu-id="5083b-103">Monitor Docker applications in Application Insights</span></span>
<span data-ttu-id="5083b-104">Les événements de cycle de vie et les compteurs de performances provenant de conteneurs [Docker](https://www.docker.com/) peuvent être représentés dans Application Insights.</span><span class="sxs-lookup"><span data-stu-id="5083b-104">Lifecycle events and performance counters from [Docker](https://www.docker.com/) containers can be charted on Application Insights.</span></span> <span data-ttu-id="5083b-105">Installez l'image [Application Insights](app-insights-overview.md) dans un conteneur de votre hôte pour afficher les compteurs de performances de l'hôte, ainsi que d'autres images.</span><span class="sxs-lookup"><span data-stu-id="5083b-105">Install the [Application Insights](app-insights-overview.md) image in a container in your host, and it will display performance counters for the host, as well as for the other images.</span></span>

<span data-ttu-id="5083b-106">Avec Docker, vous distribuez vos applications dans des conteneurs légers avec toutes les dépendances.</span><span class="sxs-lookup"><span data-stu-id="5083b-106">With Docker, you distribute your apps in lightweight containers complete with all dependencies.</span></span> <span data-ttu-id="5083b-107">Elles s’exécuteront sur n’importe quelle machine hôte exécutant un moteur Docker.</span><span class="sxs-lookup"><span data-stu-id="5083b-107">They'll run on any host machine that runs a Docker Engine.</span></span>

<span data-ttu-id="5083b-108">Lorsque vous exécutez l’[image Application Insights](https://hub.docker.com/r/microsoft/applicationinsights/) sur l’hôte Docker, vous bénéficiez des avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="5083b-108">When you run the [Application Insights image](https://hub.docker.com/r/microsoft/applicationinsights/) on your Docker host, you get these benefits:</span></span>

* <span data-ttu-id="5083b-109">Télémétrie de cycle de vie de tous les conteneurs en cours d'exécution sur l'hôte : démarrage, arrêt, et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="5083b-109">Lifecycle telemetry about all the containers running on the host - start, stop, and so on.</span></span>
* <span data-ttu-id="5083b-110">Compteurs de performance pour tous les conteneurs.</span><span class="sxs-lookup"><span data-stu-id="5083b-110">Performance counters for all the containers.</span></span> <span data-ttu-id="5083b-111">Processeur, mémoire, utilisation du réseau, et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="5083b-111">CPU, memory, network usage, and more.</span></span>
* <span data-ttu-id="5083b-112">Si vous avez [installé le SDK Application Insights pour Java](app-insights-java-live.md) dans les applications en cours d’exécution dans les conteneurs, toutes les données de télémétrie de ces applications auront des propriétés supplémentaires identifiant l’ordinateur hôte et le conteneur.</span><span class="sxs-lookup"><span data-stu-id="5083b-112">If you [installed Application Insights SDK for Java](app-insights-java-live.md) in the apps running in the containers, all the telemetry of those apps will have additional properties identifying the container and host machine.</span></span> <span data-ttu-id="5083b-113">Par exemple, si vous avez des instances d’une application en cours d’exécution dans plusieurs hôtes, vous pouvez facilement filtrer la télémétrie d’application par hôte.</span><span class="sxs-lookup"><span data-stu-id="5083b-113">So for example, if you have instances of an app running in more than one host, you can easily filter your app telemetry by host.</span></span>

![exemple](./media/app-insights-docker/00.png)

## <a name="set-up-your-application-insights-resource"></a><span data-ttu-id="5083b-115">Configuration de votre ressource Application Insights</span><span class="sxs-lookup"><span data-stu-id="5083b-115">Set up your Application Insights resource</span></span>
1. <span data-ttu-id="5083b-116">Connectez-vous au [portail Microsoft Azure](https://azure.com) et ouvrez la ressource Application Insights pour votre application ou [créez-en une](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="5083b-116">Sign into [Microsoft Azure portal](https://azure.com) and open the Application Insights resource for your app; or [create a new one](app-insights-create-new-resource.md).</span></span> 
   
    <span data-ttu-id="5083b-117">*Quelle ressource dois-je utiliser ?*</span><span class="sxs-lookup"><span data-stu-id="5083b-117">*Which resource should I use?*</span></span> <span data-ttu-id="5083b-118">Si les applications en cours d’exécution sur votre hôte ont été développées par quelqu’un d’autre, vous devez [créer une ressource Application Insights](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="5083b-118">If the apps that you are running on your host were developed by someone else, then you need to [create a new Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="5083b-119">C'est ce qui vous permet d'afficher et d'analyser les données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="5083b-119">This is where you view and analyze the telemetry.</span></span> <span data-ttu-id="5083b-120">(Sélectionnez « Général » comme type d’application.)</span><span class="sxs-lookup"><span data-stu-id="5083b-120">(Select 'General' for the app type.)</span></span>
   
    <span data-ttu-id="5083b-121">Toutefois, si vous êtes le développeur des applications, nous espérons que vous avez [ajouté le Kit SDK Application Insights](app-insights-java-live.md) à chacune d'elles.</span><span class="sxs-lookup"><span data-stu-id="5083b-121">But if you're the developer of the apps, then we hope you [added Application Insights SDK](app-insights-java-live.md) to each of them.</span></span> <span data-ttu-id="5083b-122">Si en fait elles sont toutes des composants d'une application d'entreprise unique, vous pouvez toutes les configurer pour envoyer la télémétrie à une ressource, puis vous utiliserez cette même ressource pour afficher les données de performances et du cycle de vie de Docker.</span><span class="sxs-lookup"><span data-stu-id="5083b-122">If they're all really components of a single business application, then you might configure all of them to send telemetry to one resource, and you'll use that same resource to display the Docker lifecycle and performance data.</span></span> 
   
    <span data-ttu-id="5083b-123">Un troisième scénario est que vous avez développé la plupart des applications, mais vous utilisez des ressources distinctes pour afficher les données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="5083b-123">A third scenario is that you developed most of the apps, but you are using separate resources to display their telemetry.</span></span> <span data-ttu-id="5083b-124">Dans ce cas, vous pouvez créer une ressource distincte pour les données de Docker.</span><span class="sxs-lookup"><span data-stu-id="5083b-124">In that case, you probably also want to create a separate resource for the Docker data.</span></span> 
2. <span data-ttu-id="5083b-125">Ajoutez la mosaïque Docker : choisissez **Ajouter la mosaïque**, faites glisser la mosaïque Docker à partir de la galerie, puis cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="5083b-125">Add the Docker tile: Choose **Add Tile**, drag the Docker tile from the gallery, and then click **Done**.</span></span> 
   
    ![exemple](./media/app-insights-docker/03.png)
3. <span data-ttu-id="5083b-127">Cliquez sur la liste déroulante **Essentials** et sélectionnez la clé d'instrumentation.</span><span class="sxs-lookup"><span data-stu-id="5083b-127">Click the **Essentials** drop-down and copy the Instrumentation Key.</span></span> <span data-ttu-id="5083b-128">Vous l’utilisez pour indiquer au Kit de développement logiciel (SDK) où envoyer ses données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="5083b-128">You use this to tell the SDK where to send its telemetry.</span></span>

    ![exemple](./media/app-insights-docker/02-props.png)

<span data-ttu-id="5083b-130">Ne fermez pas cette fenêtre de navigateur : vous y reviendrez ultérieurement pour consulter vos données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="5083b-130">Keep that browser window handy, as you'll come back to it soon to look at your telemetry.</span></span>

## <a name="run-the-application-insights-monitor-on-your-host"></a><span data-ttu-id="5083b-131">Exécution de l'analyse Application Insights sur votre hôte</span><span class="sxs-lookup"><span data-stu-id="5083b-131">Run the Application Insights monitor on your host</span></span>
<span data-ttu-id="5083b-132">Maintenant que vous avez défini un emplacement pour l'affichage des données de télémétrie, vous pouvez configurer l'application de conteneur qui les recueillera et les enverra.</span><span class="sxs-lookup"><span data-stu-id="5083b-132">Now that you've got somewhere to display the telemetry, you can set up the containerized app that will collect and send it.</span></span>

1. <span data-ttu-id="5083b-133">Connectez-vous à votre hôte Docker.</span><span class="sxs-lookup"><span data-stu-id="5083b-133">Connect to your Docker host.</span></span> 
2. <span data-ttu-id="5083b-134">Modifiez la clé d'instrumentation par cette commande, puis exécutez-la :</span><span class="sxs-lookup"><span data-stu-id="5083b-134">Edit your instrumentation key into this command, and then run it:</span></span>
   
   ```
   
   docker run -v /var/run/docker.sock:/docker.sock -d microsoft/applicationinsights ikey=000000-1111-2222-3333-444444444
   ```

<span data-ttu-id="5083b-135">Une seule image Application Insights est requise par hôte Docker.</span><span class="sxs-lookup"><span data-stu-id="5083b-135">Only one Application Insights image is required per Docker host.</span></span> <span data-ttu-id="5083b-136">Si votre application est déployée sur plusieurs hôtes Docker, répétez la commande sur chaque hôte.</span><span class="sxs-lookup"><span data-stu-id="5083b-136">If your application is deployed on multiple Docker hosts, then repeat the command on every host.</span></span>

## <a name="update-your-app"></a><span data-ttu-id="5083b-137">Mise à jour de votre application</span><span class="sxs-lookup"><span data-stu-id="5083b-137">Update your app</span></span>
<span data-ttu-id="5083b-138">Si votre application est instrumentée avec le [SDK Application Insights pour Java](app-insights-java-get-started.md), ajoutez la ligne suivante dans le fichier ApplicationInsights.xml de votre projet, sous l’élément `<TelemetryInitializers>` :</span><span class="sxs-lookup"><span data-stu-id="5083b-138">If your application is instrumented with the [Application Insights SDK for Java](app-insights-java-get-started.md), add the following line into the ApplicationInsights.xml file in your project, under the `<TelemetryInitializers>` element:</span></span>

```xml

    <Add type="com.microsoft.applicationinsights.extensibility.initializer.docker.DockerContextInitializer"/> 
```

<span data-ttu-id="5083b-139">Ainsi, des informations Docker, telles que le conteneur et l'ID de l'hôte sont ajoutées à chaque élément de télémétrie envoyé à partir de votre application.</span><span class="sxs-lookup"><span data-stu-id="5083b-139">This adds Docker information such as container and host id to every telemetry item sent from your app.</span></span>

## <a name="view-your-telemetry"></a><span data-ttu-id="5083b-140">Affichage de vos données de télémétrie</span><span class="sxs-lookup"><span data-stu-id="5083b-140">View your telemetry</span></span>
<span data-ttu-id="5083b-141">Revenez à votre ressource Application Insights dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5083b-141">Go back to your Application Insights resource in the Azure portal.</span></span>

<span data-ttu-id="5083b-142">Cliquez sur la mosaïque Docker.</span><span class="sxs-lookup"><span data-stu-id="5083b-142">Click through the Docker tile.</span></span>

<span data-ttu-id="5083b-143">Vous verrez bientôt des données arriver à partir de l'application Docker, en particulier si d'autres conteneurs sont en cours d'exécution sur votre moteur Docker.</span><span class="sxs-lookup"><span data-stu-id="5083b-143">You'll shortly see data arriving from the Docker app, especially if you have other containers running on your Docker engine.</span></span>

<span data-ttu-id="5083b-144">Voici quelques-uns des affichages que vous pouvez voir.</span><span class="sxs-lookup"><span data-stu-id="5083b-144">Here are some of the views you can get.</span></span>

### <a name="perf-counters-by-host-activity-by-image"></a><span data-ttu-id="5083b-145">Compteurs de performances par hôte, activité par image</span><span class="sxs-lookup"><span data-stu-id="5083b-145">Perf counters by host, activity by image</span></span>
![exemple](./media/app-insights-docker/10.png)

![exemple](./media/app-insights-docker/11.png)

<span data-ttu-id="5083b-148">Cliquez sur le nom d'un hôte ou d'une image pour plus de détails.</span><span class="sxs-lookup"><span data-stu-id="5083b-148">Click any host or image name for more detail.</span></span>

<span data-ttu-id="5083b-149">Pour personnaliser l’affichage, cliquez sur un graphique ou sur l’en-tête de la grille, ou utilisez l’option Ajouter un graphique.</span><span class="sxs-lookup"><span data-stu-id="5083b-149">To customize the view, click any chart, the grid heading, or use Add Chart.</span></span> 

<span data-ttu-id="5083b-150">[En savoir plus sur Metrics Explorer](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="5083b-150">[Learn more about metrics explorer](app-insights-metrics-explorer.md).</span></span>

### <a name="docker-container-events"></a><span data-ttu-id="5083b-151">Événements du conteneur Docker</span><span class="sxs-lookup"><span data-stu-id="5083b-151">Docker container events</span></span>
![exemple](./media/app-insights-docker/13.png)

<span data-ttu-id="5083b-153">Pour examiner les événements individuels, cliquez sur [Rechercher](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="5083b-153">To investigate individual events, click [Search](app-insights-diagnostic-search.md).</span></span> <span data-ttu-id="5083b-154">Utilisez le système de recherche et de filtre pour rechercher des événements particuliers.</span><span class="sxs-lookup"><span data-stu-id="5083b-154">Search and filter to find the events you want.</span></span> <span data-ttu-id="5083b-155">Cliquez sur un événement pour obtenir plus de détails.</span><span class="sxs-lookup"><span data-stu-id="5083b-155">Click any event to get more detail.</span></span>

### <a name="exceptions-by-container-name"></a><span data-ttu-id="5083b-156">Exceptions par nom de conteneur</span><span class="sxs-lookup"><span data-stu-id="5083b-156">Exceptions by container name</span></span>
![exemple](./media/app-insights-docker/14.png)

### <a name="docker-context-added-to-app-telemetry"></a><span data-ttu-id="5083b-158">Contexte docker ajouté à la télémétrie d'application</span><span class="sxs-lookup"><span data-stu-id="5083b-158">Docker context added to app telemetry</span></span>
<span data-ttu-id="5083b-159">Demande de télémétrie envoyée à partir de l'application instrumentée avec le Kit SDK AI, enrichie avec le contexte de Docker :</span><span class="sxs-lookup"><span data-stu-id="5083b-159">Request telemetry sent from the application instrumented with AI SDK, enriched with Docker context:</span></span>

![exemple](./media/app-insights-docker/16.png)

<span data-ttu-id="5083b-161">Temps du processeur et compteurs de performance mémoire disponible, enrichis et regroupés par nom de conteneur Docker :</span><span class="sxs-lookup"><span data-stu-id="5083b-161">Processor time and available memory performance counters, enriched and grouped by Docker container name:</span></span>

![exemple](./media/app-insights-docker/15.png)

## <a name="q--a"></a><span data-ttu-id="5083b-163">Questions et réponses</span><span class="sxs-lookup"><span data-stu-id="5083b-163">Q & A</span></span>
<span data-ttu-id="5083b-164">*Quelles sont les fonctionnalités d’Application Insights qui ne sont pas disponibles dans Docker ?*</span><span class="sxs-lookup"><span data-stu-id="5083b-164">*What does Application Insights give me that I can't get from Docker?*</span></span>

* <span data-ttu-id="5083b-165">Analyse détaillée des compteurs de performances par conteneur et par image.</span><span class="sxs-lookup"><span data-stu-id="5083b-165">Detailed breakdown of performance counters by container and image.</span></span>
* <span data-ttu-id="5083b-166">Intégration des données de conteneur et d’application dans un tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="5083b-166">Integrate container and app data in one dashboard.</span></span>
* <span data-ttu-id="5083b-167">[Exportation des données de télémétrie](app-insights-export-telemetry.md) pour approfondir l'analyse vers une base de données, Power BI ou un autre tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="5083b-167">[Export telemetry](app-insights-export-telemetry.md) for further analysis to a database, Power BI or other dashboard.</span></span>

<span data-ttu-id="5083b-168">*Comment obtenir des données de télémétrie à partir de l’application elle-même ?*</span><span class="sxs-lookup"><span data-stu-id="5083b-168">*How do I get telemetry from the app itself?*</span></span>

* <span data-ttu-id="5083b-169">Installez le Kit SDK Application Insights dans l’application.</span><span class="sxs-lookup"><span data-stu-id="5083b-169">Install the Application Insights SDK in the app.</span></span> <span data-ttu-id="5083b-170">Découvrez comment faire pour : les [applications web Java](app-insights-java-get-started.md), les [applications web Windows](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="5083b-170">Learn how for: [Java web apps](app-insights-java-get-started.md), [Windows web apps](app-insights-asp-net.md).</span></span>

## <a name="video"></a><span data-ttu-id="5083b-171">Vidéo</span><span class="sxs-lookup"><span data-stu-id="5083b-171">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="5083b-172">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5083b-172">Next steps</span></span>

* [<span data-ttu-id="5083b-173">Application Insights pour Java</span><span class="sxs-lookup"><span data-stu-id="5083b-173">Application Insights for Java</span></span>](app-insights-java-get-started.md)
* [<span data-ttu-id="5083b-174">Application Insights pour Node.js</span><span class="sxs-lookup"><span data-stu-id="5083b-174">Application Insights for Node.js</span></span>](app-insights-nodejs.md)
* [<span data-ttu-id="5083b-175">Application Insights pour ASP.NET</span><span class="sxs-lookup"><span data-stu-id="5083b-175">Application Insights for ASP.NET</span></span>](app-insights-asp-net.md)
