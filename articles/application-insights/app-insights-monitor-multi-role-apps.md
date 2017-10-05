---
title: Prise en charge par Azure Application Insights de plusieurs composants, microservices et conteneurs | Microsoft Docs
description: "Surveillance des performances et de l’utilisation des applications constituées de plusieurs composants ou de plusieurs rôles."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/17/2017
ms.author: bwren
ms.openlocfilehash: ca1bb8ee886c4b4e69be9dd653d6a52b874e1f5a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-multi-component-applications-with-application-insights-preview"></a><span data-ttu-id="df156-103">Surveiller des applications multicomposants avec Application Insights (préversion)</span><span class="sxs-lookup"><span data-stu-id="df156-103">Monitor multi-component applications with Application Insights (preview)</span></span>

<span data-ttu-id="df156-104">Vous pouvez surveiller des applications constituées de plusieurs composants serveurs, rôles ou services avec [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="df156-104">You can monitor apps that consist of multiple server components, roles, or services with [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="df156-105">L’intégrité des composants et des relations entre eux sont affichés dans un même plan d’application.</span><span class="sxs-lookup"><span data-stu-id="df156-105">The health of the components and the relationships between them are displayed on a single Application Map.</span></span> <span data-ttu-id="df156-106">Vous pouvez suivre des opérations individuelles à travers plusieurs composants avec une corrélation HTTP automatique.</span><span class="sxs-lookup"><span data-stu-id="df156-106">You can trace individual operations through multiple components with automatic HTTP correlation.</span></span> <span data-ttu-id="df156-107">Vous pouvez intégrer et corréler les diagnostics des conteneurs à la télémétrie de l’application.</span><span class="sxs-lookup"><span data-stu-id="df156-107">Container diagnostics can be integrated and correlated with application telemetry.</span></span> <span data-ttu-id="df156-108">Utilisez une seule ressource Application Insights pour tous les composants de votre application.</span><span class="sxs-lookup"><span data-stu-id="df156-108">Use a single Application Insights resource for all the components of your application.</span></span> 

![Plan d’application multicomposant](./media/app-insights-monitor-multi-role-apps/app-map.png)

<span data-ttu-id="df156-110">Nous utilisons « composant » ici pour signifier une partie fonctionnelle d’une application de grande taille.</span><span class="sxs-lookup"><span data-stu-id="df156-110">We use 'component' here to mean any functioning part of a large application.</span></span> <span data-ttu-id="df156-111">Par exemple, une application métier classique peut se composer de code client s’exécutant dans des navigateurs web, échangeant avec un ou plusieurs services d’application web, qui à leur tour utilisent des services principaux.</span><span class="sxs-lookup"><span data-stu-id="df156-111">For example, a typical business application may consist of client code running in web browsers, talking to one or more web app services, which in turn use back end services.</span></span> <span data-ttu-id="df156-112">Les composants serveur peuvent être hébergés localement ou dans le cloud, être des rôles web et worker Azure, ou s’exécuter dans des conteneurs comme Docker ou Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="df156-112">Server components may be hosted on-premises on in the cloud, or may be Azure web and worker roles, or may run in containers such as Docker or Service Fabric.</span></span> 

### <a name="sharing-a-single-application-insights-resource"></a><span data-ttu-id="df156-113">Partage d’une seule ressource Application Insights</span><span class="sxs-lookup"><span data-stu-id="df156-113">Sharing a single Application Insights resource</span></span> 

<span data-ttu-id="df156-114">La technique principale consiste à envoyer la télémétrie depuis chaque composant de votre application à la même ressource Application Insights, mais à utiliser la propriété `cloud_RoleName` pour distinguer les composants quand c’est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="df156-114">The key technique here is to send telemetry from every component in your application to the same Application Insights resource, but use the `cloud_RoleName` property to distinguish components when necessary.</span></span> <span data-ttu-id="df156-115">Le SDK Application Insights ajoute la propriété `cloud_RoleName` aux données de télémétrie émises par les composants.</span><span class="sxs-lookup"><span data-stu-id="df156-115">The Application Insights SDK adds the `cloud_RoleName` property to the telemetry components emit.</span></span> <span data-ttu-id="df156-116">Par exemple, le SDK ajoute un nom de site web ou un nom de rôle de service à la propriété `cloud_RoleName`.</span><span class="sxs-lookup"><span data-stu-id="df156-116">For example, the SDK will add a web site name, or service role name to the `cloud_RoleName` property.</span></span> <span data-ttu-id="df156-117">Vous pouvez remplacer cette valeur par un telemetryinitializer.</span><span class="sxs-lookup"><span data-stu-id="df156-117">You can override this value with a telemetryinitializer.</span></span> <span data-ttu-id="df156-118">Le plan d’application utilise la propriété `cloud_RoleName` pour identifier les composants sur le plan.</span><span class="sxs-lookup"><span data-stu-id="df156-118">The Application Map uses the `cloud_RoleName` property to identify the components on the map.</span></span>

<span data-ttu-id="df156-119">Pour plus d’informations sur la façon de remplacer la propriété `cloud_RoleName`, consultez [Ajouter des propriétés : ITelemetryInitializer](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer).</span><span class="sxs-lookup"><span data-stu-id="df156-119">For more information about how do override the `cloud_RoleName` property see [Add properties: ITelemetryInitializer](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer).</span></span>  

<span data-ttu-id="df156-120">Dans certains cas, ceci peut ne pas être approprié et vous pouvez alors préférer utiliser des ressources distinctes pour les différents groupes de composants.</span><span class="sxs-lookup"><span data-stu-id="df156-120">In some cases, this may not be appropriate, and you may prefer to use separate resources for different groups of components.</span></span> <span data-ttu-id="df156-121">Par exemple, vous aurez peut-être besoin de ressources différentes pour la gestion ou la facturation.</span><span class="sxs-lookup"><span data-stu-id="df156-121">For example, you might need to use different resources for management or billing purposes.</span></span> <span data-ttu-id="df156-122">Si vous utilisez des ressources distinctes, vous ne voyez pas tous les composants affichés sur un même plan d’application et vous ne pouvez pas interroger les différents composants dans l’[analytique](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="df156-122">Using separate resources means that you don't see all the components displayed on a single Application Map; and that you can't query across components in [Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="df156-123">Vous devez également configurer les ressources distinctes.</span><span class="sxs-lookup"><span data-stu-id="df156-123">You also have to set up the separate resources.</span></span>

<span data-ttu-id="df156-124">Cela étant, nous supposons pour le reste de ce document que vous voulez envoyer les données de plusieurs composants vers une même ressource Application Insights.</span><span class="sxs-lookup"><span data-stu-id="df156-124">With that caveat, we'll assume in the rest of this document that you want to send data from multiple components to one Application Insights resource.</span></span>

## <a name="configure-multi-component-applications"></a><span data-ttu-id="df156-125">Configurer des applications multicomposants</span><span class="sxs-lookup"><span data-stu-id="df156-125">Configure multi-component applications</span></span>

<span data-ttu-id="df156-126">Pour obtenir le plan d’une application multicomposant, voici ce que vous devez faire :</span><span class="sxs-lookup"><span data-stu-id="df156-126">To get a multi-component application map, you need to achieve these goals:</span></span>

* <span data-ttu-id="df156-127">**Installez la préversion la plus récente** du package Application Insights dans chaque composant de l’application.</span><span class="sxs-lookup"><span data-stu-id="df156-127">**Install the latest pre-release** Application Insights package in each component of the application.</span></span> 
* <span data-ttu-id="df156-128">**Partagez une même ressource Application Insights** pour tous les composants de votre application.</span><span class="sxs-lookup"><span data-stu-id="df156-128">**Share a single Application Insights resource** for all the components of your application.</span></span>
* <span data-ttu-id="df156-129">**Activez Plan d’application multirôle** dans le panneau Préversions.</span><span class="sxs-lookup"><span data-stu-id="df156-129">**Enable Multi-role Application Map** in the Previews blade.</span></span>

<span data-ttu-id="df156-130">Configurez chaque composant de votre application en utilisant la méthode qui convient à son type.</span><span class="sxs-lookup"><span data-stu-id="df156-130">Configure each component of your application using the appropriate method for its type.</span></span> <span data-ttu-id="df156-131">([ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), [JavaScript](app-insights-javascript.md).)</span><span class="sxs-lookup"><span data-stu-id="df156-131">([ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), [JavaScript](app-insights-javascript.md).)</span></span>

### <a name="1-install-the-latest-pre-release-package"></a><span data-ttu-id="df156-132">1. Installer la préversion la plus récente du package</span><span class="sxs-lookup"><span data-stu-id="df156-132">1. Install the latest pre-release package</span></span>

<span data-ttu-id="df156-133">Mettez à jour ou installez les packages Application Insights dans le projet pour chaque composant serveur.</span><span class="sxs-lookup"><span data-stu-id="df156-133">Update or install the Appication Insights packages in the project for each server component.</span></span> <span data-ttu-id="df156-134">Si vous utilisez Visual Studio :</span><span class="sxs-lookup"><span data-stu-id="df156-134">If you're using Visual Studio:</span></span>

1. <span data-ttu-id="df156-135">Cliquez avec le bouton droit sur un projet et sélectionnez **Gérer les packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="df156-135">Right-click a project and select **Manage NuGet Packages**.</span></span> 
2. <span data-ttu-id="df156-136">Sélectionnez **Inclure la préversion**.</span><span class="sxs-lookup"><span data-stu-id="df156-136">Select **Include prerelease**.</span></span>
3. <span data-ttu-id="df156-137">Si des packages Application Insights apparaissent dans les mises à jour, sélectionnez-les.</span><span class="sxs-lookup"><span data-stu-id="df156-137">If Application Insights packages appear in Updates, select them.</span></span> 

    <span data-ttu-id="df156-138">Sinon, recherchez et installez le package approprié :</span><span class="sxs-lookup"><span data-stu-id="df156-138">Otherwise, browse for and install the appropriate package:</span></span>
    
    * <span data-ttu-id="df156-139">Microsoft.ApplicationInsights.WindowsServer</span><span class="sxs-lookup"><span data-stu-id="df156-139">Microsoft.ApplicationInsights.WindowsServer</span></span>
    * <span data-ttu-id="df156-140">Microsoft.ApplicationInsights.ServiceFabric : pour les composants s’exécutant en tant qu’exécutables invités et les conteneurs Docker s’exécutant dans une application Service Fabric</span><span class="sxs-lookup"><span data-stu-id="df156-140">Microsoft.ApplicationInsights.ServiceFabric - for components running as guest executables and Docker containers running a in Service Fabric application</span></span>
    * <span data-ttu-id="df156-141">Microsoft.ApplicationInsights.ServiceFabric.Native : pour des services fiables dans les applications Service Fabric</span><span class="sxs-lookup"><span data-stu-id="df156-141">Microsoft.ApplicationInsights.ServiceFabric.Native - for reliable services in ServiceFabric applications</span></span>
    * <span data-ttu-id="df156-142">Microsoft.ApplicationInsights.Kubernetes : pour les composants s’exécutant dans Docker sur Kubernetes</span><span class="sxs-lookup"><span data-stu-id="df156-142">Microsoft.ApplicationInsights.Kubernetes for components running in Docker on Kubernetes</span></span>

### <a name="2-share-a-single-application-insights-resource"></a><span data-ttu-id="df156-143">2. Partager une même ressource Application Insights</span><span class="sxs-lookup"><span data-stu-id="df156-143">2. Share a single Application Insights resource</span></span>

* <span data-ttu-id="df156-144">Dans Visual Studio, cliquez avec le bouton droit sur un projet et sélectionnez **Configurer Application Insights** ou **Application Insights > Configurer**.</span><span class="sxs-lookup"><span data-stu-id="df156-144">In Visual Studio, right-click a project and select **Configure Application Insights**, or **Application Insights > Configure**.</span></span> <span data-ttu-id="df156-145">Pour le premier projet, utilisez l’Assistant pour créer une ressource Application Insights.</span><span class="sxs-lookup"><span data-stu-id="df156-145">For the first project, use the wizard to create an Application Insights resource.</span></span> <span data-ttu-id="df156-146">Pour les projets suivants, sélectionnez la même ressource.</span><span class="sxs-lookup"><span data-stu-id="df156-146">For subsequent projects, select the same resource.</span></span>
* <span data-ttu-id="df156-147">S’il n’existe aucun menu Application Insights, configurez-le manuellement :</span><span class="sxs-lookup"><span data-stu-id="df156-147">If there is no Application Insights menu, configure manually:</span></span>

   1. <span data-ttu-id="df156-148">Dans le [portail Azure](https://portal,azure.com), ouvrez la ressource Application Insights que vous avez déjà créée pour un autre composant.</span><span class="sxs-lookup"><span data-stu-id="df156-148">In [Azure portal](https://portal,azure.com), open the Application Insights resource you already created for another component.</span></span>
   2. <span data-ttu-id="df156-149">Dans le panneau Vue d’ensemble, ouvrez la liste déroulante Bases et sélectionnez la **clé d’instrumentation**.</span><span class="sxs-lookup"><span data-stu-id="df156-149">In the Overview blade, open the Essentials drop-down tab, and copy the **Instrumentation Key.**</span></span>
   3. <span data-ttu-id="df156-150">Dans votre projet, ouvrez ApplicationInsights.config et insérez : `<InstrumentationKey>your copied key</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="df156-150">In your project, open ApplicationInsights.config and insert: `<InstrumentationKey>your copied key</InstrumentationKey>`</span></span>

![Copiez la clé d’instrumentation dans le fichier .config](./media/app-insights-monitor-multi-role-apps/copy-instrumentation-key.png)


### <a name="3-enable-multi-role-application-map"></a><span data-ttu-id="df156-152">3. Activer Plan d’une application multirôle</span><span class="sxs-lookup"><span data-stu-id="df156-152">3. Enable multi-role Application Map</span></span>

<span data-ttu-id="df156-153">Dans le portail Azure, ouvrez la ressource pour votre application.</span><span class="sxs-lookup"><span data-stu-id="df156-153">In the Azure portal, open the resource for your application.</span></span> <span data-ttu-id="df156-154">Dans le panneau Préversions, activez *Plan d’application multirôle*.</span><span class="sxs-lookup"><span data-stu-id="df156-154">In the Previews blade, enable *Multi-role Application Map*.</span></span>

### <a name="4-enable-docker-metrics-optional"></a><span data-ttu-id="df156-155">4. Activer les métriques Docker (facultatif)</span><span class="sxs-lookup"><span data-stu-id="df156-155">4. Enable Docker metrics (Optional)</span></span> 

<span data-ttu-id="df156-156">Si un composant s’exécute dans un Docker hébergé sur une machine virtuelle Windows Azure, vous pouvez collecter des métriques supplémentaires auprès du conteneur.</span><span class="sxs-lookup"><span data-stu-id="df156-156">If a component runs in a Docker hosted on an Azure Windows VM, you can collect additional metrics from the container.</span></span> <span data-ttu-id="df156-157">Dans votre fichier de configuration [Azure Diagnostics](../monitoring-and-diagnostics/azure-diagnostics.md), insérez ceci :</span><span class="sxs-lookup"><span data-stu-id="df156-157">Insert this in your [Azure diagnostics](../monitoring-and-diagnostics/azure-diagnostics.md) configuration file:</span></span>

```
"DiagnosticMonitorConfiguration": {
        ...
        "sinks": "applicationInsights",
        "DockerSources": {
                "Stats": {
                    "enabled": true,
                    "sampleRate": "PT1M"
                }
            },
        ...
    }
    ...   
    "SinksConfig": {
        "Sink": [{
            "name": "applicationInsights",
            "ApplicationInsights": "<your instrumentation key here>"
        }]
    }
    ...
}

```

## <a name="use-cloudrolename-to-separate-components"></a><span data-ttu-id="df156-158">Utilisez cloud_RoleName pour séparer les composants</span><span class="sxs-lookup"><span data-stu-id="df156-158">Use cloud_RoleName to separate components</span></span>

<span data-ttu-id="df156-159">La propriété `cloud_RoleName` est attachée à toute la télémétrie.</span><span class="sxs-lookup"><span data-stu-id="df156-159">The `cloud_RoleName` property is attached to all telemetry.</span></span> <span data-ttu-id="df156-160">Elle identifie le composant - le rôle ou le service - dont provient la télémétrie.</span><span class="sxs-lookup"><span data-stu-id="df156-160">It identifies the component - the role or service - that originates the telemetry.</span></span> <span data-ttu-id="df156-161">(Elle n’est pas identique à cloud_RoleInstance, qui sépare les rôles identiques qui s’exécutent en parallèle sur plusieurs processus serveur ou sur plusieurs ordinateurs.)</span><span class="sxs-lookup"><span data-stu-id="df156-161">(It is not the same as cloud_RoleInstance, which separates identical roles that are running in parallel on multiple server processes or machines.)</span></span>

<span data-ttu-id="df156-162">Dans le portail, vous pouvez filtrer ou segmenter votre télémétrie à l’aide de cette propriété.</span><span class="sxs-lookup"><span data-stu-id="df156-162">In the portal, you can filter or segment your telemetry using this property.</span></span> <span data-ttu-id="df156-163">Dans cet exemple, le panneau Échecs est filtré pour afficher seulement les informations du service web frontend, en éliminant les échecs du backend de l’API CRM :</span><span class="sxs-lookup"><span data-stu-id="df156-163">In this example, the Failures blade is filtered to show just information from the front-end web service, filtering out failures from the CRM API backend:</span></span>

![Graphique des métriques segmentées par nom de rôle cloud](./media/app-insights-monitor-multi-role-apps/cloud-role-name.png)

## <a name="trace-operations-between-components"></a><span data-ttu-id="df156-165">Suivre les opérations entre les composants</span><span class="sxs-lookup"><span data-stu-id="df156-165">Trace operations between components</span></span>

<span data-ttu-id="df156-166">Vous pouvez suivre les appels d’un composant à un autre effectués lors du traitement d’une opération individuelle.</span><span class="sxs-lookup"><span data-stu-id="df156-166">You can trace from one component to another, the calls made while processing an individual operation.</span></span>


![Afficher la télémétrie pour une opération](./media/app-insights-monitor-multi-role-apps/show-telemetry-for-operation.png)

<span data-ttu-id="df156-168">Cliquez pour obtenir une liste corrélée de la télémétrie pour cette opération entre le serveur web frontend et l’API backend :</span><span class="sxs-lookup"><span data-stu-id="df156-168">Click through to a correlated list of telemetry for this operation across the front-end web server and the back-end API:</span></span>

![Rechercher dans l’ensemble des composants](./media/app-insights-monitor-multi-role-apps/search-across-components.png)


## <a name="next-steps"></a><span data-ttu-id="df156-170">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="df156-170">Next steps</span></span>

* [<span data-ttu-id="df156-171">Télémétrie distincte entre le développement, les tests et la production</span><span class="sxs-lookup"><span data-stu-id="df156-171">Separate telemetry from Development, Test, and Production</span></span>](app-insights-separate-resources.md)
