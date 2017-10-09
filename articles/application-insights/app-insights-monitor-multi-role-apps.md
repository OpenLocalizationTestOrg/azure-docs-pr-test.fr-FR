---
title: aaaAzure Application Insights prennent en charge de plusieurs composants, microservices et conteneurs | Documents Microsoft
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
ms.openlocfilehash: 6185eedf32ec450d7541603b94de6c3dcdf64a85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-multi-component-applications-with-application-insights-preview"></a><span data-ttu-id="ead51-103">Surveiller des applications multicomposants avec Application Insights (préversion)</span><span class="sxs-lookup"><span data-stu-id="ead51-103">Monitor multi-component applications with Application Insights (preview)</span></span>

<span data-ttu-id="ead51-104">Vous pouvez surveiller des applications constituées de plusieurs composants serveurs, rôles ou services avec [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ead51-104">You can monitor apps that consist of multiple server components, roles, or services with [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="ead51-105">contrôle d’intégrité Hello des composants de hello et des relations hello entre eux sont affichés sur un seul mappage d’Application.</span><span class="sxs-lookup"><span data-stu-id="ead51-105">hello health of hello components and hello relationships between them are displayed on a single Application Map.</span></span> <span data-ttu-id="ead51-106">Vous pouvez suivre des opérations individuelles à travers plusieurs composants avec une corrélation HTTP automatique.</span><span class="sxs-lookup"><span data-stu-id="ead51-106">You can trace individual operations through multiple components with automatic HTTP correlation.</span></span> <span data-ttu-id="ead51-107">Vous pouvez intégrer et corréler les diagnostics des conteneurs à la télémétrie de l’application.</span><span class="sxs-lookup"><span data-stu-id="ead51-107">Container diagnostics can be integrated and correlated with application telemetry.</span></span> <span data-ttu-id="ead51-108">Utiliser une seule ressource Application Insights pour tous les composants hello de votre application.</span><span class="sxs-lookup"><span data-stu-id="ead51-108">Use a single Application Insights resource for all hello components of your application.</span></span> 

![Plan d’application multicomposant](./media/app-insights-monitor-multi-role-apps/app-map.png)

<span data-ttu-id="ead51-110">Nous utilisons 'composant' toomean ici une partie de fonctionnement d’une application volumineuse.</span><span class="sxs-lookup"><span data-stu-id="ead51-110">We use 'component' here toomean any functioning part of a large application.</span></span> <span data-ttu-id="ead51-111">Par exemple, une application métier classique peut se composer de code client en cours d’exécution dans les navigateurs web, ils s’adressent tooone ou services de fin de plusieurs services d’application web, qui à leur tour utilisent précédent.</span><span class="sxs-lookup"><span data-stu-id="ead51-111">For example, a typical business application may consist of client code running in web browsers, talking tooone or more web app services, which in turn use back end services.</span></span> <span data-ttu-id="ead51-112">Les composants de serveur peuvent être hébergé localement sur dans le cloud de hello, ou des rôles web et de travail Azure peuvent être ou peuvent s’exécuter dans des conteneurs tels que Docker ou Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ead51-112">Server components may be hosted on-premises on in hello cloud, or may be Azure web and worker roles, or may run in containers such as Docker or Service Fabric.</span></span> 

### <a name="sharing-a-single-application-insights-resource"></a><span data-ttu-id="ead51-113">Partage d’une seule ressource Application Insights</span><span class="sxs-lookup"><span data-stu-id="ead51-113">Sharing a single Application Insights resource</span></span> 

<span data-ttu-id="ead51-114">Hello technique clé ici est télémétrie toosend à partir de tous les composants de toohello de votre application même ressource Application Insights, mais utilisez hello `cloud_RoleName` composants de toodistinguish propriété lorsque cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="ead51-114">hello key technique here is toosend telemetry from every component in your application toohello same Application Insights resource, but use hello `cloud_RoleName` property toodistinguish components when necessary.</span></span> <span data-ttu-id="ead51-115">Hello Application Insights SDK ajoute hello `cloud_RoleName` émettre des composants de télémétrie toohello de propriété.</span><span class="sxs-lookup"><span data-stu-id="ead51-115">hello Application Insights SDK adds hello `cloud_RoleName` property toohello telemetry components emit.</span></span> <span data-ttu-id="ead51-116">Par exemple, hello Kit de développement logiciel ajoute un nom de site web, ou toohello de nom de rôle service `cloud_RoleName` propriété.</span><span class="sxs-lookup"><span data-stu-id="ead51-116">For example, hello SDK will add a web site name, or service role name toohello `cloud_RoleName` property.</span></span> <span data-ttu-id="ead51-117">Vous pouvez remplacer cette valeur par un telemetryinitializer.</span><span class="sxs-lookup"><span data-stu-id="ead51-117">You can override this value with a telemetryinitializer.</span></span> <span data-ttu-id="ead51-118">Hello mappage d’Application utilise hello `cloud_RoleName` composants de hello tooidentify de propriété sur la carte de hello.</span><span class="sxs-lookup"><span data-stu-id="ead51-118">hello Application Map uses hello `cloud_RoleName` property tooidentify hello components on hello map.</span></span>

<span data-ttu-id="ead51-119">Pour plus d’informations sur la façon de remplacer hello `cloud_RoleName` propriété Voir [ajouter des propriétés : ITelemetryInitializer](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer).</span><span class="sxs-lookup"><span data-stu-id="ead51-119">For more information about how do override hello `cloud_RoleName` property see [Add properties: ITelemetryInitializer](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer).</span></span>  

<span data-ttu-id="ead51-120">Dans certains cas, cela n’est peut-être pas approprié, et vous pouvez toouse des ressources distinctes pour différents groupes de composants.</span><span class="sxs-lookup"><span data-stu-id="ead51-120">In some cases, this may not be appropriate, and you may prefer toouse separate resources for different groups of components.</span></span> <span data-ttu-id="ead51-121">Par exemple, vous devrez peut-être toouse différentes ressources de la gestion ou à des fins de facturation.</span><span class="sxs-lookup"><span data-stu-id="ead51-121">For example, you might need toouse different resources for management or billing purposes.</span></span> <span data-ttu-id="ead51-122">À l’aide des ressources distinctes signifie que vous ne voyez pas tous les composants hello affichées sur un seul mappage de l’Application ; et que vous ne peut pas interroger les composants dans [Analytique](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="ead51-122">Using separate resources means that you don't see all hello components displayed on a single Application Map; and that you can't query across components in [Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="ead51-123">Vous avez également tooset des ressources distinctes de hello.</span><span class="sxs-lookup"><span data-stu-id="ead51-123">You also have tooset up hello separate resources.</span></span>

<span data-ttu-id="ead51-124">Avec cet inconvénient, nous supposons que dans le reste de hello de ce document que vous souhaitez toosend les données à partir de plusieurs composants tooone ressource Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ead51-124">With that caveat, we'll assume in hello rest of this document that you want toosend data from multiple components tooone Application Insights resource.</span></span>

## <a name="configure-multi-component-applications"></a><span data-ttu-id="ead51-125">Configurer des applications multicomposants</span><span class="sxs-lookup"><span data-stu-id="ead51-125">Configure multi-component applications</span></span>

<span data-ttu-id="ead51-126">mappage d’une application à plusieurs composant tooget, vous devez tooachieve ces objectifs :</span><span class="sxs-lookup"><span data-stu-id="ead51-126">tooget a multi-component application map, you need tooachieve these goals:</span></span>

* <span data-ttu-id="ead51-127">**Installez la version préliminaire hello** package d’Application Insights dans chaque composant d’application hello.</span><span class="sxs-lookup"><span data-stu-id="ead51-127">**Install hello latest pre-release** Application Insights package in each component of hello application.</span></span> 
* <span data-ttu-id="ead51-128">**Partager une seule ressource Application Insights** pour tous les hello des composants de votre application.</span><span class="sxs-lookup"><span data-stu-id="ead51-128">**Share a single Application Insights resource** for all hello components of your application.</span></span>
* <span data-ttu-id="ead51-129">**Activer le mappage d’Application de plusieurs rôles** dans le panneau des aperçus hello.</span><span class="sxs-lookup"><span data-stu-id="ead51-129">**Enable Multi-role Application Map** in hello Previews blade.</span></span>

<span data-ttu-id="ead51-130">Configurez chaque composant de votre application à l’aide de la méthode appropriée de hello pour son type.</span><span class="sxs-lookup"><span data-stu-id="ead51-130">Configure each component of your application using hello appropriate method for its type.</span></span> <span data-ttu-id="ead51-131">([ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), [JavaScript](app-insights-javascript.md).)</span><span class="sxs-lookup"><span data-stu-id="ead51-131">([ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), [JavaScript](app-insights-javascript.md).)</span></span>

### <a name="1-install-hello-latest-pre-release-package"></a><span data-ttu-id="ead51-132">1. Installer le dernier package de version préliminaire hello</span><span class="sxs-lookup"><span data-stu-id="ead51-132">1. Install hello latest pre-release package</span></span>

<span data-ttu-id="ead51-133">Mettre à jour ou installer des packages d’application Insights hello dans projet hello pour chaque composant de serveur.</span><span class="sxs-lookup"><span data-stu-id="ead51-133">Update or install hello Appication Insights packages in hello project for each server component.</span></span> <span data-ttu-id="ead51-134">Si vous utilisez Visual Studio :</span><span class="sxs-lookup"><span data-stu-id="ead51-134">If you're using Visual Studio:</span></span>

1. <span data-ttu-id="ead51-135">Cliquez avec le bouton droit sur un projet et sélectionnez **Gérer les packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="ead51-135">Right-click a project and select **Manage NuGet Packages**.</span></span> 
2. <span data-ttu-id="ead51-136">Sélectionnez **Inclure la préversion**.</span><span class="sxs-lookup"><span data-stu-id="ead51-136">Select **Include prerelease**.</span></span>
3. <span data-ttu-id="ead51-137">Si des packages Application Insights apparaissent dans les mises à jour, sélectionnez-les.</span><span class="sxs-lookup"><span data-stu-id="ead51-137">If Application Insights packages appear in Updates, select them.</span></span> 

    <span data-ttu-id="ead51-138">Sinon, recherchez et installez hello approprié :</span><span class="sxs-lookup"><span data-stu-id="ead51-138">Otherwise, browse for and install hello appropriate package:</span></span>
    
    * <span data-ttu-id="ead51-139">Microsoft.ApplicationInsights.WindowsServer</span><span class="sxs-lookup"><span data-stu-id="ead51-139">Microsoft.ApplicationInsights.WindowsServer</span></span>
    * <span data-ttu-id="ead51-140">Microsoft.ApplicationInsights.ServiceFabric : pour les composants s’exécutant en tant qu’exécutables invités et les conteneurs Docker s’exécutant dans une application Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ead51-140">Microsoft.ApplicationInsights.ServiceFabric - for components running as guest executables and Docker containers running a in Service Fabric application</span></span>
    * <span data-ttu-id="ead51-141">Microsoft.ApplicationInsights.ServiceFabric.Native : pour des services fiables dans les applications Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ead51-141">Microsoft.ApplicationInsights.ServiceFabric.Native - for reliable services in ServiceFabric applications</span></span>
    * <span data-ttu-id="ead51-142">Microsoft.ApplicationInsights.Kubernetes : pour les composants s’exécutant dans Docker sur Kubernetes</span><span class="sxs-lookup"><span data-stu-id="ead51-142">Microsoft.ApplicationInsights.Kubernetes for components running in Docker on Kubernetes</span></span>

### <a name="2-share-a-single-application-insights-resource"></a><span data-ttu-id="ead51-143">2. Partager une même ressource Application Insights</span><span class="sxs-lookup"><span data-stu-id="ead51-143">2. Share a single Application Insights resource</span></span>

* <span data-ttu-id="ead51-144">Dans Visual Studio, cliquez avec le bouton droit sur un projet et sélectionnez **Configurer Application Insights** ou **Application Insights > Configurer**.</span><span class="sxs-lookup"><span data-stu-id="ead51-144">In Visual Studio, right-click a project and select **Configure Application Insights**, or **Application Insights > Configure**.</span></span> <span data-ttu-id="ead51-145">Pour le premier projet de hello, utilisez hello Assistant toocreate une ressource Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ead51-145">For hello first project, use hello wizard toocreate an Application Insights resource.</span></span> <span data-ttu-id="ead51-146">Pour les projets suivants, sélectionnez hello même ressource.</span><span class="sxs-lookup"><span data-stu-id="ead51-146">For subsequent projects, select hello same resource.</span></span>
* <span data-ttu-id="ead51-147">S’il n’existe aucun menu Application Insights, configurez-le manuellement :</span><span class="sxs-lookup"><span data-stu-id="ead51-147">If there is no Application Insights menu, configure manually:</span></span>

   1. <span data-ttu-id="ead51-148">Dans [portail Azure](https://portal,azure.com), ouvrez la ressource d’Application Insights hello vous avez déjà créé pour un autre composant.</span><span class="sxs-lookup"><span data-stu-id="ead51-148">In [Azure portal](https://portal,azure.com), open hello Application Insights resource you already created for another component.</span></span>
   2. <span data-ttu-id="ead51-149">Dans Panneau de vue d’ensemble de hello, onglet de hello ouvrir déroulante Essentials et hello de copie **clé d’Instrumentation.**</span><span class="sxs-lookup"><span data-stu-id="ead51-149">In hello Overview blade, open hello Essentials drop-down tab, and copy hello **Instrumentation Key.**</span></span>
   3. <span data-ttu-id="ead51-150">Dans votre projet, ouvrez ApplicationInsights.config et insérez : `<InstrumentationKey>your copied key</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="ead51-150">In your project, open ApplicationInsights.config and insert: `<InstrumentationKey>your copied key</InstrumentationKey>`</span></span>

![Copier le fichier .config de hello instrumentation toohello clé](./media/app-insights-monitor-multi-role-apps/copy-instrumentation-key.png)


### <a name="3-enable-multi-role-application-map"></a><span data-ttu-id="ead51-152">3. Activer Plan d’une application multirôle</span><span class="sxs-lookup"><span data-stu-id="ead51-152">3. Enable multi-role Application Map</span></span>

<span data-ttu-id="ead51-153">Bonjour portail Azure, ouvrez la ressource hello pour votre application.</span><span class="sxs-lookup"><span data-stu-id="ead51-153">In hello Azure portal, open hello resource for your application.</span></span> <span data-ttu-id="ead51-154">Dans le panneau de versions préliminaires de hello, activez *mappage plusieurs rôles d’Application*.</span><span class="sxs-lookup"><span data-stu-id="ead51-154">In hello Previews blade, enable *Multi-role Application Map*.</span></span>

### <a name="4-enable-docker-metrics-optional"></a><span data-ttu-id="ead51-155">4. Activer les métriques Docker (facultatif)</span><span class="sxs-lookup"><span data-stu-id="ead51-155">4. Enable Docker metrics (Optional)</span></span> 

<span data-ttu-id="ead51-156">Si un composant s’exécute dans une Docker hébergée sur un ordinateur virtuel de Windows Azure, vous pouvez collecter des mesures supplémentaires à partir du conteneur de hello.</span><span class="sxs-lookup"><span data-stu-id="ead51-156">If a component runs in a Docker hosted on an Azure Windows VM, you can collect additional metrics from hello container.</span></span> <span data-ttu-id="ead51-157">Dans votre fichier de configuration [Azure Diagnostics](../monitoring-and-diagnostics/azure-diagnostics.md), insérez ceci :</span><span class="sxs-lookup"><span data-stu-id="ead51-157">Insert this in your [Azure diagnostics](../monitoring-and-diagnostics/azure-diagnostics.md) configuration file:</span></span>

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

## <a name="use-cloudrolename-tooseparate-components"></a><span data-ttu-id="ead51-158">Utiliser des composants de tooseparate cloud_RoleName</span><span class="sxs-lookup"><span data-stu-id="ead51-158">Use cloud_RoleName tooseparate components</span></span>

<span data-ttu-id="ead51-159">Hello `cloud_RoleName` propriété est jointe tooall télémétrie.</span><span class="sxs-lookup"><span data-stu-id="ead51-159">hello `cloud_RoleName` property is attached tooall telemetry.</span></span> <span data-ttu-id="ead51-160">Il identifie le composant hello - rôle de hello ou un service - provenant des données de télémétrie hello.</span><span class="sxs-lookup"><span data-stu-id="ead51-160">It identifies hello component - hello role or service - that originates hello telemetry.</span></span> <span data-ttu-id="ead51-161">(Il est même ne Hello pas en tant que cloud_RoleInstance, qui sépare les rôles identiques qui sont exécutent en parallèle sur plusieurs ordinateurs ou les processus serveur).</span><span class="sxs-lookup"><span data-stu-id="ead51-161">(It is not hello same as cloud_RoleInstance, which separates identical roles that are running in parallel on multiple server processes or machines.)</span></span>

<span data-ttu-id="ead51-162">Dans le portail hello, vous pouvez filtrer ou segment de votre télémétrie à l’aide de cette propriété.</span><span class="sxs-lookup"><span data-stu-id="ead51-162">In hello portal, you can filter or segment your telemetry using this property.</span></span> <span data-ttu-id="ead51-163">Dans cet exemple, le panneau de défaillances de hello est tooshow filtré simplement des informations du service web frontal de hello, filtrant des échecs de hello API CRM principal :</span><span class="sxs-lookup"><span data-stu-id="ead51-163">In this example, hello Failures blade is filtered tooshow just information from hello front-end web service, filtering out failures from hello CRM API backend:</span></span>

![Graphique des métriques segmentées par nom de rôle cloud](./media/app-insights-monitor-multi-role-apps/cloud-role-name.png)

## <a name="trace-operations-between-components"></a><span data-ttu-id="ead51-165">Suivre les opérations entre les composants</span><span class="sxs-lookup"><span data-stu-id="ead51-165">Trace operations between components</span></span>

<span data-ttu-id="ead51-166">Vous pouvez tracer à partir d’un composant tooanother, appels hello lors du traitement d’une opération individuelle.</span><span class="sxs-lookup"><span data-stu-id="ead51-166">You can trace from one component tooanother, hello calls made while processing an individual operation.</span></span>


![Afficher la télémétrie pour une opération](./media/app-insights-monitor-multi-role-apps/show-telemetry-for-operation.png)

<span data-ttu-id="ead51-168">Parcourez la liste corrélés de tooa de télémétrie pour cette opération sur le serveur web frontal de hello et API de serveur principal hello :</span><span class="sxs-lookup"><span data-stu-id="ead51-168">Click through tooa correlated list of telemetry for this operation across hello front-end web server and hello back-end API:</span></span>

![Rechercher dans l’ensemble des composants](./media/app-insights-monitor-multi-role-apps/search-across-components.png)


## <a name="next-steps"></a><span data-ttu-id="ead51-170">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ead51-170">Next steps</span></span>

* [<span data-ttu-id="ead51-171">Télémétrie distincte entre le développement, les tests et la production</span><span class="sxs-lookup"><span data-stu-id="ead51-171">Separate telemetry from Development, Test, and Production</span></span>](app-insights-separate-resources.md)
