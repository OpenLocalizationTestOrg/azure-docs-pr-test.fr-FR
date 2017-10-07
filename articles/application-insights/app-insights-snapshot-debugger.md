---
title: "aaaAzure Application Insights instantané débogueur pour les applications .NET | Documents Microsoft"
description: "Des captures instantanées de débogage sont collectées automatiquement lorsque des exceptions sont levées dans des applications .NET de production"
services: application-insights
documentationcenter: 
author: qubitron
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: bwren
ms.openlocfilehash: f0173a752b5795d934fbab1bd53eb077433edc90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-snapshots-on-exceptions-in-net-apps"></a><span data-ttu-id="3e68c-103">Captures instantanées de débogage sur exceptions levées dans des applications .NET</span><span class="sxs-lookup"><span data-stu-id="3e68c-103">Debug snapshots on exceptions in .NET apps</span></span>

<span data-ttu-id="3e68c-104">Quand une exception se produit, vous pouvez collecter automatiquement une capture instantanée de débogage à partir de votre application web dynamique.</span><span class="sxs-lookup"><span data-stu-id="3e68c-104">When an exception occurs, you can automatically collect a debug snapshot from your live web application.</span></span> <span data-ttu-id="3e68c-105">l’instantané Hello affiche état hello du code source et les variables à l’exception de hello moment hello a été levée.</span><span class="sxs-lookup"><span data-stu-id="3e68c-105">hello snapshot shows hello state of source code and variables at hello moment hello exception was thrown.</span></span> <span data-ttu-id="3e68c-106">Hello instantané débogueur (version préliminaire) dans [Azure Application Insights](app-insights-overview.md) surveille la télémétrie des exceptions à partir de votre application web.</span><span class="sxs-lookup"><span data-stu-id="3e68c-106">hello Snapshot Debugger (preview) in [Azure Application Insights](app-insights-overview.md) monitors exception telemetry from your web app.</span></span> <span data-ttu-id="3e68c-107">Il collecte des captures instantanées sur vos exceptions levées en haut afin que les informations hello problèmes toodiagnose en production.</span><span class="sxs-lookup"><span data-stu-id="3e68c-107">It collects snapshots on your top-throwing exceptions so that you have hello information you need toodiagnose issues in production.</span></span> <span data-ttu-id="3e68c-108">Inclure hello [package NuGet de collecteur instantané](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) dans votre application et éventuellement configurer les paramètres de collecte dans [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). Instantanés apparaissent sur [exceptions](app-insights-asp-net-exceptions.md) portail Application Insights de hello.</span><span class="sxs-lookup"><span data-stu-id="3e68c-108">Include hello [Snapshot collector NuGet package](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) in your application, and optionally configure collection parameters in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). Snapshots appear on [exceptions](app-insights-asp-net-exceptions.md) in hello Application Insights portal.</span></span>

<span data-ttu-id="3e68c-109">Vous pouvez afficher des instantanés de débogage dans la pile des appels hello toosee portail hello et inspecter des variables à chaque frame de pile des appels.</span><span class="sxs-lookup"><span data-stu-id="3e68c-109">You can view debug snapshots in hello portal toosee hello call stack and inspect variables at each call stack frame.</span></span> <span data-ttu-id="3e68c-110">tooget une expérience de débogage plus puissante avec code source, ouvrez instantanés avec Visual Studio 2017 Enterprise par [télécharger l’extension de débogueur de l’instantané hello pour Visual Studio](https://aka.ms/snapshotdebugger).</span><span class="sxs-lookup"><span data-stu-id="3e68c-110">tooget a more powerful debugging experience with source code, open snapshots with Visual Studio 2017 Enterprise by [downloading hello Snapshot Debugger extension for Visual Studio](https://aka.ms/snapshotdebugger).</span></span>

<span data-ttu-id="3e68c-111">La collecte de captures instantanées est disponible pour :</span><span class="sxs-lookup"><span data-stu-id="3e68c-111">Snapshot collection is available for:</span></span>
* <span data-ttu-id="3e68c-112">les applications .NET framework et ASP.NET exécutant .NET Framework 4.5 ou version ultérieure ;</span><span class="sxs-lookup"><span data-stu-id="3e68c-112">.NET Framework and ASP.NET applications running .NET Framework 4.5 or later.</span></span>
* <span data-ttu-id="3e68c-113">les applications .NET core 2.0 et ASP.NET Core 2.0 s’exécutant sous Windows.</span><span class="sxs-lookup"><span data-stu-id="3e68c-113">.NET Core 2.0 and ASP.NET Core 2.0 applications running on Windows.</span></span>

### <a name="configure-snapshot-collection-for-aspnet-applications"></a><span data-ttu-id="3e68c-114">Configurer la collecte de captures instantanées pour les applications ASP.NET</span><span class="sxs-lookup"><span data-stu-id="3e68c-114">Configure snapshot collection for ASP.NET applications</span></span>

1. <span data-ttu-id="3e68c-115">Si vous ne l’avez pas encore fait, [Activez Application Insights dans votre application web](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="3e68c-115">[Enable Application Insights in your web app](app-insights-asp-net.md), if you haven't done it yet.</span></span>

2. <span data-ttu-id="3e68c-116">Inclure hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) package NuGet dans votre application.</span><span class="sxs-lookup"><span data-stu-id="3e68c-116">Include hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span> 

3. <span data-ttu-id="3e68c-117">Passez en revue les options par défaut hello hello package ajouté trop[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span><span class="sxs-lookup"><span data-stu-id="3e68c-117">Review hello default options that hello package added too[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span>

    ```xml
    <TelemetryProcessors>
        <Add Type="Microsoft.ApplicationInsights.SnapshotCollector.SnapshotCollectorTelemetryProcessor, Microsoft.ApplicationInsights.SnapshotCollector">
        <!-- hello default is true, but you can disable Snapshot Debugging by setting it toofalse -->
        <IsEnabled>true</IsEnabled>
        <!-- Snapshot Debugging is usually disabled in developer mode, but you can enable it by setting this tootrue. -->
        <!-- DeveloperMode is a property on hello active TelemetryChannel. -->
        <IsEnabledInDeveloperMode>false</IsEnabledInDeveloperMode>
        <!-- How many times we need toosee an exception before we ask for snapshots. -->
        <ThresholdForSnapshotting>5</ThresholdForSnapshotting>
        <!-- hello maximum number of examples we create for a single problem. -->
        <MaximumSnapshotsRequired>3</MaximumSnapshotsRequired>
        <!-- hello maximum number of problems that we can be tracking at any time. -->
        <MaximumCollectionPlanSize>50</MaximumCollectionPlanSize>
        <!-- How often tooreset problem counters. -->
        <ProblemCounterResetInterval>06:00:00</ProblemCounterResetInterval>
        <!-- hello maximum number of snapshots allowed in one minute. -->
        <SnapshotsPerMinuteLimit>2</SnapshotsPerMinuteLimit>
        <!-- hello maximum number of snapshots allowed per day. -->
        <SnapshotsPerDayLimit>50</SnapshotsPerDayLimit>
        </Add>
    </TelemetryProcessors>
    ```

4. <span data-ttu-id="3e68c-118">Les instantanés sont collectés uniquement sur les exceptions qui sont signalés tooApplication Insights.</span><span class="sxs-lookup"><span data-stu-id="3e68c-118">Snapshots are collected only on exceptions that are reported tooApplication Insights.</span></span> <span data-ttu-id="3e68c-119">Dans certains cas (par exemple, les anciennes versions de la plateforme .NET de hello), vous devrez peut-être trop[configurer la collection d’exceptions](app-insights-asp-net-exceptions.md#exceptions) exceptions toosee avec des instantanés dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="3e68c-119">In some cases (for example, older versions of hello .NET platform), you might need too[configure exception collection](app-insights-asp-net-exceptions.md#exceptions) toosee exceptions with snapshots in hello portal.</span></span>


### <a name="configure-snapshot-collection-for-aspnet-core-20-applications"></a><span data-ttu-id="3e68c-120">Configurer la collecte de captures instantanées pour les applications ASP.NET Core 2.0</span><span class="sxs-lookup"><span data-stu-id="3e68c-120">Configure snapshot collection for ASP.NET Core 2.0 applications</span></span>

1. <span data-ttu-id="3e68c-121">Si vous ne l’avez pas encore fait, [Activez Application Insights dans votre application web ASP.NET Core](app-insights-asp-net-core.md).</span><span class="sxs-lookup"><span data-stu-id="3e68c-121">[Enable Application Insights in your ASP.NET Core web app](app-insights-asp-net-core.md), if you haven't done it yet.</span></span>

2. <span data-ttu-id="3e68c-122">Inclure hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) package NuGet dans votre application.</span><span class="sxs-lookup"><span data-stu-id="3e68c-122">Include hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span>

3. <span data-ttu-id="3e68c-123">Modifier hello `ConfigureServices` méthode dans votre application `Startup` classe du processeur de télémétrie du collecteur instantané tooadd hello.</span><span class="sxs-lookup"><span data-stu-id="3e68c-123">Modify hello `ConfigureServices` method in your application's `Startup` class tooadd hello Snapshot Collector's telemetry processor.</span></span> <span data-ttu-id="3e68c-124">code Hello que vous devez ajouter dépend de la version de référencé de hello Hello package NuGet de Microsoft.ApplicationInsights.ASPNETCore.</span><span class="sxs-lookup"><span data-stu-id="3e68c-124">hello code you should add depends on hello referenced version of hello Microsoft.ApplicationInsights.ASPNETCore NuGet package.</span></span>

   <span data-ttu-id="3e68c-125">Pour Microsoft.ApplicationInsights.AspNetCore 2.1.0, ajoutez :</span><span class="sxs-lookup"><span data-stu-id="3e68c-125">For Microsoft.ApplicationInsights.AspNetCore 2.1.0 add:</span></span>
   ```C#
   using Microsoft.ApplicationInsights.SnapshotCollector;
   ...
   class Startup
   {
       // This method is called by hello runtime. Use it tooadd services toohello container.
       public void ConfigureServices(IServiceCollection services)
       {
           services.AddSingleton<Func<ITelemetryProcessor, ITelemetryProcessor>>(next => new SnapshotCollectorTelemetryProcessor(next));
           // TODO: Add any other services your application needs here.
       }
   }
   ```

   <span data-ttu-id="3e68c-126">Pour Microsoft.ApplicationInsights.AspNetCore 2.1.1, ajoutez :</span><span class="sxs-lookup"><span data-stu-id="3e68c-126">For Microsoft.ApplicationInsights.AspNetCore 2.1.1 add:</span></span>
   ```C#
   using Microsoft.ApplicationInsights.SnapshotCollector;
   ...
   class Startup
   {
       private class SnapshotCollectorTelemetryProcessorFactory : ITelemetryProcessorFactory
       {
           public ITelemetryProcessor Create(ITelemetryProcessor next) =>
               new SnapshotCollectorTelemetryProcessor(next);
       }

       // This method is called by hello runtime. Use it tooadd services toohello container.
       public void ConfigureServices(IServiceCollection services)
       {
            services.AddSingleton<ITelemetryProcessorFactory>(new SnapshotCollectorTelemetryProcessorFactory());
           // TODO: Add any other services your application needs here.
       }
   }
   ```

### <a name="configure-snapshot-collection-for-other-net-applications"></a><span data-ttu-id="3e68c-127">Configurer la collecte de captures instantanées pour d’autres applications .NET</span><span class="sxs-lookup"><span data-stu-id="3e68c-127">Configure snapshot collection for other .NET applications</span></span>

1. <span data-ttu-id="3e68c-128">Si votre application n’est pas déjà instrumentée avec Application Insights, commencez par [l’activation d’Application Insights et clé d’instrumentation paramètre hello](app-insights-windows-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="3e68c-128">If your application is not already instrumented with Application Insights, get started by [enabling Application Insights and setting hello instrumentation key](app-insights-windows-desktop.md).</span></span>

2. <span data-ttu-id="3e68c-129">Ajouter hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) package NuGet dans votre application.</span><span class="sxs-lookup"><span data-stu-id="3e68c-129">Add hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span>

3. <span data-ttu-id="3e68c-130">Les instantanés sont collectés uniquement sur les exceptions qui sont signalés tooApplication Insights.</span><span class="sxs-lookup"><span data-stu-id="3e68c-130">Snapshots are collected only on exceptions that are reported tooApplication Insights.</span></span> <span data-ttu-id="3e68c-131">Vous devrez peut-être toomodify tooreport de votre code les.</span><span class="sxs-lookup"><span data-stu-id="3e68c-131">You may need toomodify your code tooreport them.</span></span> <span data-ttu-id="3e68c-132">code de gestion des exceptions de Hello dépend de la structure de hello de votre application, mais voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="3e68c-132">hello exception handling code depends on hello structure of your application, but an example is below:</span></span>
    ```C#
   TelemetryClient _telemetryClient = new TelemetryClient();

   void ExampleRequest()
   {
        try
        {
            // TODO: Handle hello request.
        }
        catch (Exception ex)
        {
            // Report hello exception tooApplication Insights.
            _telemetryClient.TrackException(ex);

            // TODO: Rethrow hello exception if desired.
        }
   }
    ```
    
## <a name="grant-permissions"></a><span data-ttu-id="3e68c-133">Accorder des autorisations</span><span class="sxs-lookup"><span data-stu-id="3e68c-133">Grant permissions</span></span>

<span data-ttu-id="3e68c-134">Les propriétaires de hello abonnement Azure peuvent inspecter des instantanés.</span><span class="sxs-lookup"><span data-stu-id="3e68c-134">Owners of hello Azure subscription can inspect snapshots.</span></span> <span data-ttu-id="3e68c-135">Les autres utilisateurs doivent y être autorisés par un propriétaire.</span><span class="sxs-lookup"><span data-stu-id="3e68c-135">Other users must be granted permission by an owner.</span></span>

<span data-ttu-id="3e68c-136">autorisation toogrant, affecter hello `Application Insights Snapshot Debugger` toousers de rôle qui inspecte instantanés.</span><span class="sxs-lookup"><span data-stu-id="3e68c-136">toogrant permission, assign hello `Application Insights Snapshot Debugger` role toousers who will inspect snapshots.</span></span> <span data-ttu-id="3e68c-137">Ce rôle peut être attribué tooindividual utilisateurs ou groupes de propriétaires d’abonnements pour la cible de hello ressource Application Insights ou son groupe de ressources ou l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="3e68c-137">This role can be assigned tooindividual users or groups by subscription owners for hello target Application Insights resource or its resource group or subscription.</span></span>

1. <span data-ttu-id="3e68c-138">Ouvrez le panneau de contrôle d’accès (IAM) hello.</span><span class="sxs-lookup"><span data-stu-id="3e68c-138">Open hello Access Control (IAM) blade.</span></span>
1. <span data-ttu-id="3e68c-139">Cliquez sur hello + bouton Ajouter.</span><span class="sxs-lookup"><span data-stu-id="3e68c-139">Click hello +Add button.</span></span>
1. <span data-ttu-id="3e68c-140">Sélectionnez l’Application Insights instantané débogueur à partir de la liste déroulante de rôles hello.</span><span class="sxs-lookup"><span data-stu-id="3e68c-140">Select Application Insights Snapshot Debugger from hello Roles drop-down list.</span></span>
1. <span data-ttu-id="3e68c-141">Recherchez et entrez un nom pour hello utilisateur tooadd.</span><span class="sxs-lookup"><span data-stu-id="3e68c-141">Search for and enter a name for hello user tooadd.</span></span>
1. <span data-ttu-id="3e68c-142">Cliquez sur le rôle d’utilisateur toohello hello hello enregistrer bouton tooadd.</span><span class="sxs-lookup"><span data-stu-id="3e68c-142">Click hello Save button tooadd hello user toohello role.</span></span>


[!IMPORTANT]
    <span data-ttu-id="3e68c-143">Les captures instantanées des valeurs de variables et de paramètres peuvent contenir des informations personnelles ou sensibles.</span><span class="sxs-lookup"><span data-stu-id="3e68c-143">Snapshots can potentially contain personal and other sensitive information in variable and parameter values.</span></span>

## <a name="debug-snapshots-in-hello-application-insights-portal"></a><span data-ttu-id="3e68c-144">Déboguer des instantanés dans le portail Application Insights de hello</span><span class="sxs-lookup"><span data-stu-id="3e68c-144">Debug snapshots in hello Application Insights portal</span></span>

<span data-ttu-id="3e68c-145">Si un instantané est disponible pour une exception donnée ou un ID de problème, un **ouvrir l’instantané déboguer** bouton s’affiche sur hello [exception](app-insights-asp-net-exceptions.md) portail Application Insights de hello.</span><span class="sxs-lookup"><span data-stu-id="3e68c-145">If a snapshot is available for a given exception or a problem ID, an **Open Debug Snapshot** button appears on hello [exception](app-insights-asp-net-exceptions.md) in hello Application Insights portal.</span></span>

![Bouton Ouvrir la capture instantanée de débogage sur l’exception](./media/app-insights-snapshot-debugger/snapshot-on-exception.png)

<span data-ttu-id="3e68c-147">Bonjour déboguer un instantané, vous consultez une pile des appels et un volet variables.</span><span class="sxs-lookup"><span data-stu-id="3e68c-147">In hello Debug Snapshot view, you see a call stack and a variables pane.</span></span> <span data-ttu-id="3e68c-148">Lorsque vous sélectionnez les frames d’appel de hello de pile dans le volet de pile d’appel hello, vous pouvez afficher les variables locales et appellent des paramètres pour cette fonction dans le volet des variables hello.</span><span class="sxs-lookup"><span data-stu-id="3e68c-148">When you select frames of hello call stack in hello call stack pane, you can view local variables and parameters for that function call in hello variables pane.</span></span>

![Afficher l’instantané de débogage dans le portail de hello](./media/app-insights-snapshot-debugger/open-snapshot-portal.png)

<span data-ttu-id="3e68c-150">Les captures instantanées peuvent contenir des informations sensibles qui, par défaut, ne sont pas visibles.</span><span class="sxs-lookup"><span data-stu-id="3e68c-150">Snapshots might contain sensitive information, and by default they are not viewable.</span></span> <span data-ttu-id="3e68c-151">tooview des instantanés, vous devez avoir hello `Application Insights Snapshot Debugger` tooyou du rôle assigné.</span><span class="sxs-lookup"><span data-stu-id="3e68c-151">tooview snapshots, you must have hello `Application Insights Snapshot Debugger` role assigned tooyou.</span></span>

## <a name="debug-snapshots-with-visual-studio-2017-enterprise"></a><span data-ttu-id="3e68c-152">Déboguer des captures instantanées avec Visual Studio 2017 Enterprise</span><span class="sxs-lookup"><span data-stu-id="3e68c-152">Debug snapshots with Visual Studio 2017 Enterprise</span></span>
1. <span data-ttu-id="3e68c-153">Cliquez sur hello **télécharger un instantané** toodownload de bouton un `.diagsession` fichier, qui peut être ouverte par Visual Studio 2017 Enterprise.</span><span class="sxs-lookup"><span data-stu-id="3e68c-153">Click hello **Download Snapshot** button toodownload a `.diagsession` file, which can be opened by Visual Studio 2017 Enterprise.</span></span> 

2. <span data-ttu-id="3e68c-154">tooopen hello `.diagsession` fichier, vous devez d’abord [télécharger et installer l’extension de débogueur de l’instantané hello pour Visual Studio](https://aka.ms/snapshotdebugger).</span><span class="sxs-lookup"><span data-stu-id="3e68c-154">tooopen hello `.diagsession` file, you must first [download and install hello Snapshot Debugger extension for Visual Studio](https://aka.ms/snapshotdebugger).</span></span>

3. <span data-ttu-id="3e68c-155">Après avoir ouvert le fichier d’instantané hello, page de débogage de Minidump hello dans Visual Studio s’affiche.</span><span class="sxs-lookup"><span data-stu-id="3e68c-155">After you open hello snapshot file, hello Minidump Debugging page in Visual Studio appears.</span></span> <span data-ttu-id="3e68c-156">Cliquez sur **déboguer du Code managé** toostart instantané d’hello de débogage.</span><span class="sxs-lookup"><span data-stu-id="3e68c-156">Click **Debug Managed Code** toostart debugging hello snapshot.</span></span> <span data-ttu-id="3e68c-157">instantané d’Hello ouvre ligne toohello de code où hello de l’exception afin que vous puissiez déboguer état actuel de hello du processus de hello.</span><span class="sxs-lookup"><span data-stu-id="3e68c-157">hello snapshot opens toohello line of code where hello exception was thrown so that you can debug hello current state of hello process.</span></span>

    ![Afficher la capture instantanée de débogage dans Visual Studio](./media/app-insights-snapshot-debugger/open-snapshot-visualstudio.png)

<span data-ttu-id="3e68c-159">les instantanés téléchargés Hello contient tous les fichiers de symboles qui ont été trouvées sur votre serveur d’applications web.</span><span class="sxs-lookup"><span data-stu-id="3e68c-159">hello downloaded snapshot contains any symbol files that were found on your web application server.</span></span> <span data-ttu-id="3e68c-160">Ces fichiers de symboles sont requis tooassociate les données d’instantané avec le code source.</span><span class="sxs-lookup"><span data-stu-id="3e68c-160">These symbol files are required tooassociate snapshot data with source code.</span></span> <span data-ttu-id="3e68c-161">Pour les applications de Service d’applications, assurez-vous que déploiement de symbole tooenable lors de la publication de vos applications web.</span><span class="sxs-lookup"><span data-stu-id="3e68c-161">For App Service apps, make sure tooenable symbol deployment when you publish your web apps.</span></span>

## <a name="how-snapshots-work"></a><span data-ttu-id="3e68c-162">Fonctionnement des captures instantanées</span><span class="sxs-lookup"><span data-stu-id="3e68c-162">How snapshots work</span></span>

<span data-ttu-id="3e68c-163">Au démarrage de votre application, un processus distinct de chargeur de captures instantanées qui surveille les demandes de captures instantanées de votre application est créé.</span><span class="sxs-lookup"><span data-stu-id="3e68c-163">When your application starts, a separate snapshot uploader process is created that monitors your application for snapshot requests.</span></span> <span data-ttu-id="3e68c-164">Lorsqu’un instantané est demandé, un cliché instantané d’hello processus en cours d’exécution est effectué dans les too20 environ 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="3e68c-164">When a snapshot is requested, a shadow copy of hello running process is made in about 10 too20 minutes.</span></span> <span data-ttu-id="3e68c-165">processus de clichés instantanés Hello est ensuite analysé et un instantané est créé sans interrompre le processus principal hello toorun et traiter le trafic toousers.</span><span class="sxs-lookup"><span data-stu-id="3e68c-165">hello shadow process is then analyzed, and a snapshot is created while hello main process continues toorun and serve traffic toousers.</span></span> <span data-ttu-id="3e68c-166">Bonjour instantané est ensuite téléchargée tooApplication Insights, ainsi que tous les fichiers de symbole (.pdb) qui sont nécessaires tooview instantané d’hello.</span><span class="sxs-lookup"><span data-stu-id="3e68c-166">hello snapshot is then uploaded tooApplication Insights along with any relevant symbol (.pdb) files that are needed tooview hello snapshot.</span></span>

## <a name="current-limitations"></a><span data-ttu-id="3e68c-167">Limitations actuelles</span><span class="sxs-lookup"><span data-stu-id="3e68c-167">Current limitations</span></span>

### <a name="publish-symbols"></a><span data-ttu-id="3e68c-168">Publier des symboles</span><span class="sxs-lookup"><span data-stu-id="3e68c-168">Publish symbols</span></span>
<span data-ttu-id="3e68c-169">Hello instantané débogueur requiert des fichiers de symboles sur les variables de toodecode de serveur de production hello et tooprovide une expérience de débogage dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3e68c-169">hello Snapshot Debugger requires symbol files on hello production server toodecode variables and tooprovide a debugging experience in Visual Studio.</span></span> <span data-ttu-id="3e68c-170">version de Hello 15,2 de Visual Studio 2017 publie des symboles pour les versions release par défaut lorsqu’il publie tooApp Service.</span><span class="sxs-lookup"><span data-stu-id="3e68c-170">hello 15.2 release of Visual Studio 2017 publishes symbols for release builds by default when it publishes tooApp Service.</span></span> <span data-ttu-id="3e68c-171">Dans les versions antérieures, vous devez suivant de hello tooadd ligne tooyour le profil de publication `.pubxml` fichiers afin que les symboles sont publiés en mode release :</span><span class="sxs-lookup"><span data-stu-id="3e68c-171">In prior versions, you need tooadd hello following line tooyour publish profile `.pubxml` file so that symbols are published in release mode:</span></span>

```xml
    <ExcludeGeneratedDebugSymbol>False</ExcludeGeneratedDebugSymbol>
```

<span data-ttu-id="3e68c-172">Calcul Azure et d’autres types, assurez-vous que les fichiers de symboles hello sont hello même dossier du fichier .dll de principale de l’application hello (en règle générale, `wwwroot/bin`) ou sont disponibles sur le chemin d’accès actuel de hello.</span><span class="sxs-lookup"><span data-stu-id="3e68c-172">For Azure Compute and other types, ensure that hello symbol files are in hello same folder of hello main application .dll (typically, `wwwroot/bin`) or are available on hello current path.</span></span>

### <a name="optimized-builds"></a><span data-ttu-id="3e68c-173">Optimisation des versions</span><span class="sxs-lookup"><span data-stu-id="3e68c-173">Optimized builds</span></span>
<span data-ttu-id="3e68c-174">Dans certains cas, les variables locales ne peut pas être affichés dans les versions release en raison d’optimisations qui sont appliquées au cours du processus de génération hello.</span><span class="sxs-lookup"><span data-stu-id="3e68c-174">In some cases, local variables cannot be viewed in release builds because of optimizations that are applied during hello build process.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="3e68c-175">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="3e68c-175">Troubleshooting</span></span>

<span data-ttu-id="3e68c-176">Les conseils suivants vous aider à résoudre les problèmes de hello débogueur de l’instantané.</span><span class="sxs-lookup"><span data-stu-id="3e68c-176">These tips help you troubleshoot problems with hello Snapshot Debugger.</span></span>

### <a name="verify-hello-instrumentation-key"></a><span data-ttu-id="3e68c-177">Vérifiez la clé d’instrumentation hello</span><span class="sxs-lookup"><span data-stu-id="3e68c-177">Verify hello instrumentation key</span></span>

<span data-ttu-id="3e68c-178">Assurez-vous que vous utilisez une clé d’instrumentation correct hello dans votre application publiée.</span><span class="sxs-lookup"><span data-stu-id="3e68c-178">Make sure that you're using hello correct instrumentation key in your published application.</span></span> <span data-ttu-id="3e68c-179">En règle générale, Application Insights lit clé d’instrumentation hello hello ApplicationInsights.config du fichier.</span><span class="sxs-lookup"><span data-stu-id="3e68c-179">Usually, Application Insights reads hello instrumentation key from hello ApplicationInsights.config file.</span></span> <span data-ttu-id="3e68c-180">Vérifiez que la valeur de hello même hello en tant que clé d’instrumentation hello pour la ressource d’Application Insights hello que vous voyez dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="3e68c-180">Verify that hello value is hello same as hello instrumentation key for hello Application Insights resource that you see in hello portal.</span></span>

### <a name="check-hello-uploader-logs"></a><span data-ttu-id="3e68c-181">Vérifiez les journaux du téléchargeur hello</span><span class="sxs-lookup"><span data-stu-id="3e68c-181">Check hello uploader logs</span></span>

<span data-ttu-id="3e68c-182">Une fois une capture instantanée créée, un fichier minidump (.dmp) est créé sur le disque.</span><span class="sxs-lookup"><span data-stu-id="3e68c-182">After a snapshot is created, a minidump file (.dmp) is created on disk.</span></span> <span data-ttu-id="3e68c-183">Un processus distinct du chargeur prend ce fichier minidump, télécharger, ainsi que toutes les fichiers pdb associé, tooApplication stockage du débogueur d’instantané Insights.</span><span class="sxs-lookup"><span data-stu-id="3e68c-183">A separate uploader process takes that minidump file and uploads it, along with any associated PDBs, tooApplication Insights Snapshot Debugger storage.</span></span> <span data-ttu-id="3e68c-184">Une fois les minidump hello a été téléchargé correctement, elle est supprimée à partir du disque.</span><span class="sxs-lookup"><span data-stu-id="3e68c-184">After hello minidump has uploaded successfully, it is deleted from disk.</span></span> <span data-ttu-id="3e68c-185">fichiers journaux Hello téléchargeur de minidump hello sont conservés sur le disque.</span><span class="sxs-lookup"><span data-stu-id="3e68c-185">hello log files for hello minidump uploader are retained on disk.</span></span> <span data-ttu-id="3e68c-186">Dans un environnement App Service, vous pouvez trouver ces fichiers journaux dans `D:\Home\LogFiles\Uploader_*.log`.</span><span class="sxs-lookup"><span data-stu-id="3e68c-186">In an App Service environment, you can find these logs in `D:\Home\LogFiles\Uploader_*.log`.</span></span> <span data-ttu-id="3e68c-187">Utiliser le site Administration Kudu hello pour le Service d’applications toofind ces fichiers journaux.</span><span class="sxs-lookup"><span data-stu-id="3e68c-187">Use hello Kudu management site for App Service toofind these log files.</span></span>

1. <span data-ttu-id="3e68c-188">Bonjour portail Azure, ouvrez votre application de Service de l’application.</span><span class="sxs-lookup"><span data-stu-id="3e68c-188">Open your App Service application in hello Azure portal.</span></span>

2. <span data-ttu-id="3e68c-189">Sélectionnez hello **outils avancés** panneau ou recherchez **Kudu**.</span><span class="sxs-lookup"><span data-stu-id="3e68c-189">Select hello **Advanced Tools** blade, or search for **Kudu**.</span></span>
3. <span data-ttu-id="3e68c-190">Cliquez sur **Atteindre**.</span><span class="sxs-lookup"><span data-stu-id="3e68c-190">Click **Go**.</span></span>
4. <span data-ttu-id="3e68c-191">Bonjour **console de débogage** zone de liste déroulante, sélectionnez **CMD**.</span><span class="sxs-lookup"><span data-stu-id="3e68c-191">In hello **Debug console** drop-down list box, select **CMD**.</span></span>
5. <span data-ttu-id="3e68c-192">Cliquez sur **LogFiles**.</span><span class="sxs-lookup"><span data-stu-id="3e68c-192">Click **LogFiles**.</span></span>

<span data-ttu-id="3e68c-193">Vous devriez voir au moins un fichier dont le nom commence par `Uploader_` et dont l’extension est `.log`.</span><span class="sxs-lookup"><span data-stu-id="3e68c-193">You should see at least one file with a name that begins with `Uploader_` and a `.log` extension.</span></span> <span data-ttu-id="3e68c-194">Cliquez sur toodownload d’icône appropriée hello tous les fichiers journaux ou les ouvrir dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="3e68c-194">Click hello appropriate icon toodownload any log files or open them in a browser.</span></span>
<span data-ttu-id="3e68c-195">nom de fichier Hello inclut le nom de l’ordinateur hello.</span><span class="sxs-lookup"><span data-stu-id="3e68c-195">hello file name includes hello machine name.</span></span> <span data-ttu-id="3e68c-196">Si votre instance App Service est hébergée sur plusieurs machines, il existe des fichiers journaux distincts pour chacune d’elles.</span><span class="sxs-lookup"><span data-stu-id="3e68c-196">If your App Service instance is hosted on more than one machine, there are separate log files for each machine.</span></span> <span data-ttu-id="3e68c-197">Lorsque le Téléchargeur de hello détecte un fichier minidump, elle est enregistrée dans le fichier journal de hello.</span><span class="sxs-lookup"><span data-stu-id="3e68c-197">When hello uploader detects a new minidump file, it is recorded in hello log file.</span></span> <span data-ttu-id="3e68c-198">Voici un exemple chargement réussi :</span><span class="sxs-lookup"><span data-stu-id="3e68c-198">Here's an example of a successful upload:</span></span>

```
MinidumpUploader.exe Information: 0 : Dump available 139e411a23934dc0b9ea08a626db16c5.dmp
    DateTime=2017-05-25T14:25:08.0349846Z
MinidumpUploader.exe Information: 0 : Uploading D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp, 329.12 MB
    DateTime=2017-05-25T14:25:16.0145444Z
MinidumpUploader.exe Information: 0 : Upload successful.
    DateTime=2017-05-25T14:25:42.9164120Z
MinidumpUploader.exe Information: 0 : Extracting PDB info from D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp.
    DateTime=2017-05-25T14:25:42.9164120Z
MinidumpUploader.exe Information: 0 : Matched 2 PDB(s) with local files.
    DateTime=2017-05-25T14:25:44.2310982Z
MinidumpUploader.exe Information: 0 : Stamp does not want any of our matched PDBs.
    DateTime=2017-05-25T14:25:44.5435948Z
MinidumpUploader.exe Information: 0 : Deleted D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp
    DateTime=2017-05-25T14:25:44.6095821Z
```

<span data-ttu-id="3e68c-199">Dans l’exemple précédent de hello, clé d’instrumentation hello est `c12a605e73c44346a984e00000000000`.</span><span class="sxs-lookup"><span data-stu-id="3e68c-199">In hello previous example, hello instrumentation key is `c12a605e73c44346a984e00000000000`.</span></span> <span data-ttu-id="3e68c-200">Cette valeur doit correspondre à clé d’instrumentation hello pour votre application.</span><span class="sxs-lookup"><span data-stu-id="3e68c-200">This value should match hello instrumentation key for your application.</span></span>
<span data-ttu-id="3e68c-201">minidump de Hello est associé à un instantané avec l’ID de hello `139e411a23934dc0b9ea08a626db16c5`.</span><span class="sxs-lookup"><span data-stu-id="3e68c-201">hello minidump is associated with a snapshot with hello ID `139e411a23934dc0b9ea08a626db16c5`.</span></span> <span data-ttu-id="3e68c-202">Vous pouvez utiliser cet ID ultérieure toolocate hello associés télémétrie des exceptions dans Application Insights Analytique.</span><span class="sxs-lookup"><span data-stu-id="3e68c-202">You can use this ID later toolocate hello associated exception telemetry in Application Insights Analytics.</span></span>

<span data-ttu-id="3e68c-203">Téléchargeur de Hello analyse les nouveaux fichiers PDB sur toutes les 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="3e68c-203">hello uploader scans for new PDBs about once every 15 minutes.</span></span> <span data-ttu-id="3e68c-204">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="3e68c-204">Here's an example:</span></span>

```
MinidumpUploader.exe Information: 0 : PDB rescan requested.
    DateTime=2017-05-25T15:11:38.8003886Z
MinidumpUploader.exe Information: 0 : Scanning D:\home\site\wwwroot\ for local PDBs.
    DateTime=2017-05-25T15:11:38.8003886Z
MinidumpUploader.exe Information: 0 : Scanning D:\local\Temporary ASP.NET Files\root\a6554c94\e3ad6f22\assembly\dl3\81d5008b\00b93cc8_dec5d201 for local PDBs.
    DateTime=2017-05-25T15:11:38.8160276Z
MinidumpUploader.exe Information: 0 : Local PDB scan complete. Found 2 PDB(s).
    DateTime=2017-05-25T15:11:38.8316450Z
MinidumpUploader.exe Information: 0 : Deleted PDB scan marker D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\.pdbscan.
    DateTime=2017-05-25T15:11:38.8316450Z
```

<span data-ttu-id="3e68c-205">Pour les applications qui sont _pas_ hébergé dans le Service d’applications, les journaux téléchargeur hello sont Bonjour même dossier que les minidumps hello : `%TEMP%\Dumps\<ikey>` (où `<ikey>` est votre clé d’instrumentation).</span><span class="sxs-lookup"><span data-stu-id="3e68c-205">For applications that are _not_ hosted in App Service, hello uploader logs are in hello same folder as hello minidumps: `%TEMP%\Dumps\<ikey>` (where `<ikey>` is your instrumentation key).</span></span>

### <a name="use-application-insights-search-toofind-exceptions-with-snapshots"></a><span data-ttu-id="3e68c-206">Utilisez Application Insights rechercher les exceptions toofind avec des instantanés</span><span class="sxs-lookup"><span data-stu-id="3e68c-206">Use Application Insights search toofind exceptions with snapshots</span></span>

<span data-ttu-id="3e68c-207">Lorsqu’un instantané est créé, hello lever exception est marqué avec un ID d’instantané.</span><span class="sxs-lookup"><span data-stu-id="3e68c-207">When a snapshot is created, hello throwing exception is tagged with a snapshot ID.</span></span> <span data-ttu-id="3e68c-208">Lors de la télémétrie des exceptions hello est signalé tooApplication Insights, cet ID d’instantané est inclus comme une propriété personnalisée.</span><span class="sxs-lookup"><span data-stu-id="3e68c-208">When hello exception telemetry is reported tooApplication Insights, that snapshot ID is included as a custom property.</span></span> <span data-ttu-id="3e68c-209">Panneau de recherche hello dans Application Insights, vous pouvez rechercher toutes les données de télémétrie avec hello `ai.snapshot.id` propriété personnalisée.</span><span class="sxs-lookup"><span data-stu-id="3e68c-209">Using hello Search blade in Application Insights, you can find all telemetry with hello `ai.snapshot.id` custom property.</span></span>

1. <span data-ttu-id="3e68c-210">Parcourir les ressources d’Application Insights tooyour Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3e68c-210">Browse tooyour Application Insights resource in hello Azure portal.</span></span>
2. <span data-ttu-id="3e68c-211">Cliquez sur **Rechercher**.</span><span class="sxs-lookup"><span data-stu-id="3e68c-211">Click **Search**.</span></span>
3. <span data-ttu-id="3e68c-212">Type `ai.snapshot.id` hello de zone de texte Rechercher et appuyez sur ENTRÉE.</span><span class="sxs-lookup"><span data-stu-id="3e68c-212">Type `ai.snapshot.id` in hello Search text box and press Enter.</span></span>

![Recherche de télémétrie avec un ID d’instantané dans le portail de hello](./media/app-insights-snapshot-debugger/search-snapshot-portal.png)

<span data-ttu-id="3e68c-214">Si cette recherche ne retourne aucun résultat, aucun instantané n’ont été Insights tooApplication signalé pour votre application dans la plage de temps hello sélectionné.</span><span class="sxs-lookup"><span data-stu-id="3e68c-214">If this search returns no results, then no snapshots were reported tooApplication Insights for your application in hello selected time range.</span></span>

<span data-ttu-id="3e68c-215">toosearch pour un instantané spécifique à partir de journaux de téléchargeur hello, tapez ce code dans la zone de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="3e68c-215">toosearch for a specific snapshot ID from hello Uploader logs, type that ID in hello Search box.</span></span> <span data-ttu-id="3e68c-216">Si vous ne trouvez la télémétrie d’une capture instantanée dont vous savez qu’elle a été chargée, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="3e68c-216">If you can't find telemetry for a snapshot that you know was uploaded, follow these steps:</span></span>

1. <span data-ttu-id="3e68c-217">Vérifiez que vous envisagez d’utiliser les ressources Application Insights droite hello en vérifiant la clé d’instrumentation hello.</span><span class="sxs-lookup"><span data-stu-id="3e68c-217">Double-check that you're looking at hello right Application Insights resource by verifying hello instrumentation key.</span></span>

2. <span data-ttu-id="3e68c-218">À l’aide d’horodatage hello du journal du téléchargeur hello, du filtre de plage de temps hello de hello recherche toocover régler cet intervalle de temps.</span><span class="sxs-lookup"><span data-stu-id="3e68c-218">Using hello timestamp from hello Uploader log, adjust hello Time Range filter of hello search toocover that time range.</span></span>

<span data-ttu-id="3e68c-219">Si vous ne voyez pas une exception avec cet ID d’instantané, puis télémétrie des exceptions hello n’a pas été signalé tooApplication Insights.</span><span class="sxs-lookup"><span data-stu-id="3e68c-219">If you still don't see an exception with that snapshot ID, then hello exception telemetry wasn't reported tooApplication Insights.</span></span> <span data-ttu-id="3e68c-220">Cette situation peut se produire si votre application est tombé en panne après l’instantané d’hello nécessaire, mais avant qu’elles consignées télémétrie des exceptions hello.</span><span class="sxs-lookup"><span data-stu-id="3e68c-220">This situation can happen if your application crashed after it took hello snapshot but before it reported hello exception telemetry.</span></span> <span data-ttu-id="3e68c-221">Dans ce cas, recherchez hello App Service se connecte sous `Diagnose and solve problems` toosee si elle existait inattendue redémarre ou les exceptions non gérées.</span><span class="sxs-lookup"><span data-stu-id="3e68c-221">In this case, check hello App Service logs under `Diagnose and solve problems` toosee if there were unexpected restarts or unhandled exceptions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e68c-222">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3e68c-222">Next steps</span></span>

* <span data-ttu-id="3e68c-223">[Définissez snappoints dans votre code](https://azure.microsoft.com/blog/snapshot-debugger-for-azure/) instantanés tooget sans attendre d’une exception.</span><span class="sxs-lookup"><span data-stu-id="3e68c-223">[Set snappoints in your code](https://azure.microsoft.com/blog/snapshot-debugger-for-azure/) tooget snapshots without waiting for an exception.</span></span>
* <span data-ttu-id="3e68c-224">[Diagnostiquer des exceptions dans vos applications web](app-insights-asp-net-exceptions.md) explique comment toomake plusieurs exceptions tooApplication visible Insights.</span><span class="sxs-lookup"><span data-stu-id="3e68c-224">[Diagnose exceptions in your web apps](app-insights-asp-net-exceptions.md) explains how toomake more exceptions visible tooApplication Insights.</span></span> 
* <span data-ttu-id="3e68c-225">[Détection intelligente](app-insights-proactive-diagnostics.md) permet de détecter automatiquement les anomalies relatives aux performances.</span><span class="sxs-lookup"><span data-stu-id="3e68c-225">[Smart Detection](app-insights-proactive-diagnostics.md) automatically discovers performance anomalies.</span></span>
