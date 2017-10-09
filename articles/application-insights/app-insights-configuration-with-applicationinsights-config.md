---
title: "référence aaaApplicationInsights.config - Azure | Documents Microsoft"
description: "Activez ou désactivez les modules de collecte de données et ajoutez des compteurs de performances et d’autres paramètres."
services: application-insights
documentationcenter: 
author: OlegAnaniev-MSFT
editor: alancameronwills
manager: carmonm
ms.assetid: 6e397752-c086-46e9-8648-a1196e8078c2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/3/2017
ms.author: bwren
ms.openlocfilehash: 76cb11349d87dfc508ec8b1c454259a0b079c48a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-hello-application-insights-sdk-with-applicationinsightsconfig-or-xml"></a><span data-ttu-id="f9f09-103">Configuration de l’Application Insights SDK de hello avec ApplicationInsights.config ou .xml</span><span class="sxs-lookup"><span data-stu-id="f9f09-103">Configuring hello Application Insights SDK with ApplicationInsights.config or .xml</span></span>
<span data-ttu-id="f9f09-104">Hello Application Insights .NET SDK se compose d’un nombre de packages NuGet.</span><span class="sxs-lookup"><span data-stu-id="f9f09-104">hello Application Insights .NET SDK consists of a number of NuGet packages.</span></span> <span data-ttu-id="f9f09-105">Le [package core](http://www.nuget.org/packages/Microsoft.ApplicationInsights) fournit les API hello pour l’envoi de données de télémétrie Hello Application Insights.</span><span class="sxs-lookup"><span data-stu-id="f9f09-105">The [core package](http://www.nuget.org/packages/Microsoft.ApplicationInsights) provides hello API for sending telemetry to hello Application Insights.</span></span> <span data-ttu-id="f9f09-106">Des [packages supplémentaires](http://www.nuget.org/packages?q=Microsoft.ApplicationInsights) fournissent les *modules* et les *initialiseurs* de télémétrie pour le suivi télémétrique automatique de votre application et de son contexte.</span><span class="sxs-lookup"><span data-stu-id="f9f09-106">[Additional packages](http://www.nuget.org/packages?q=Microsoft.ApplicationInsights) provide telemetry *modules* and *initializers* for automatically tracking telemetry from your application and its context.</span></span> <span data-ttu-id="f9f09-107">En ajustant le fichier de configuration hello, vous pouvez activer ou désactiver les initialiseurs et les modules de télémétrie et définir les paramètres pour certains d'entre eux.</span><span class="sxs-lookup"><span data-stu-id="f9f09-107">By adjusting hello configuration file, you can enable or disable telemetry modules and initializers, and set parameters for some of them.</span></span>

<span data-ttu-id="f9f09-108">fichier de configuration Hello est nommé `ApplicationInsights.config` ou `ApplicationInsights.xml`, en fonction de type hello de votre application.</span><span class="sxs-lookup"><span data-stu-id="f9f09-108">hello configuration file is named `ApplicationInsights.config` or `ApplicationInsights.xml`, depending on hello type of your application.</span></span> <span data-ttu-id="f9f09-109">Il est automatiquement ajouté tooyour projet lorsque vous [installer la plupart des versions du Kit de développement logiciel de hello][start].</span><span class="sxs-lookup"><span data-stu-id="f9f09-109">It is automatically added tooyour project when you [install most versions of hello SDK][start].</span></span> <span data-ttu-id="f9f09-110">Il est également ajouté application web de tooa par [Status Monitor sur un serveur IIS][redfield], ou lorsque vous sélectionnez hello importe quelle application Insights [extension pour une machine virtuelle ou un site Web Azure](app-insights-azure-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="f9f09-110">It is also added tooa web app by [Status Monitor on an IIS server][redfield], or when you select hello Appplication Insights [extension for an Azure website or VM](app-insights-azure-web-apps.md).</span></span>

<span data-ttu-id="f9f09-111">Il n’est pas un hello toocontrol de fichier équivalent [SDK dans une page web][client].</span><span class="sxs-lookup"><span data-stu-id="f9f09-111">There isn't an equivalent file toocontrol hello [SDK in a web page][client].</span></span>

<span data-ttu-id="f9f09-112">Ce document décrit les sections hello que vous consultez dans la configuration de hello du fichier, la gestion des composants hello Hello SDK, et les packages NuGet chargement ces composants.</span><span class="sxs-lookup"><span data-stu-id="f9f09-112">This document describes hello sections you see in hello configuration file, how they control hello components of hello SDK, and which NuGet packages load those components.</span></span>

## <a name="telemetry-modules-aspnet"></a><span data-ttu-id="f9f09-113">Modules de télémétrie (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="f9f09-113">Telemetry Modules (ASP.NET)</span></span>
<span data-ttu-id="f9f09-114">Chaque module de télémétrie collecte un type de données spécifique et utilise des noyaux de hello données d’API toosend hello.</span><span class="sxs-lookup"><span data-stu-id="f9f09-114">Each telemetry module collects a specific type of data and uses hello core API toosend hello data.</span></span> <span data-ttu-id="f9f09-115">modules de Hello sont installés à différents packages NuGet, ce qui est également ajouter le fichier .config de hello lignes requises toohello.</span><span class="sxs-lookup"><span data-stu-id="f9f09-115">hello modules are installed by different NuGet packages, which also add hello required lines toohello .config file.</span></span>

<span data-ttu-id="f9f09-116">Il existe un nœud dans le fichier de configuration hello pour chaque module.</span><span class="sxs-lookup"><span data-stu-id="f9f09-116">There's a node in hello configuration file for each module.</span></span> <span data-ttu-id="f9f09-117">toodisable un module, supprimez le nœud de hello ou commentez-le.</span><span class="sxs-lookup"><span data-stu-id="f9f09-117">toodisable a module, delete hello node or comment it out.</span></span>

### <a name="dependency-tracking"></a><span data-ttu-id="f9f09-118">Suivi des dépendances</span><span class="sxs-lookup"><span data-stu-id="f9f09-118">Dependency Tracking</span></span>
<span data-ttu-id="f9f09-119">[Le suivi des dépendances](app-insights-asp-net-dependencies.md) collecte une télémétrie sur les appels de votre application toodatabases et les services externes et les bases de données.</span><span class="sxs-lookup"><span data-stu-id="f9f09-119">[Dependency tracking](app-insights-asp-net-dependencies.md) collects telemetry about calls your app makes toodatabases and external services and databases.</span></span> <span data-ttu-id="f9f09-120">tooallow toowork de ce module dans un serveur IIS, vous devez trop[installer Status Monitor][redfield].</span><span class="sxs-lookup"><span data-stu-id="f9f09-120">tooallow this module toowork in an IIS server, you need too[install Status Monitor][redfield].</span></span> <span data-ttu-id="f9f09-121">toouse dans les applications web Azure ou des machines virtuelles, [sélectionner l’extension d’Application Insights hello](app-insights-azure-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="f9f09-121">toouse it in Azure web apps or VMs, [select hello Application Insights extension](app-insights-azure-web-apps.md).</span></span>

<span data-ttu-id="f9f09-122">Vous pouvez également écrire votre propre dépendance suivi du code à l’aide de hello [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span><span class="sxs-lookup"><span data-stu-id="f9f09-122">You can also write your own dependency tracking code using hello [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span></span>

* `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule`
* <span data-ttu-id="f9f09-123">[Microsoft.ApplicationInsights.DependencyCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) .</span><span class="sxs-lookup"><span data-stu-id="f9f09-123">[Microsoft.ApplicationInsights.DependencyCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) NuGet package.</span></span>

### <a name="performance-collector"></a><span data-ttu-id="f9f09-124">Collecteur de performances</span><span class="sxs-lookup"><span data-stu-id="f9f09-124">Performance collector</span></span>
<span data-ttu-id="f9f09-125">[Collecte les compteurs de performances système](app-insights-performance-counters.md), notamment l’UC, la mémoire et la charge réseau, à partir des installations IIS.</span><span class="sxs-lookup"><span data-stu-id="f9f09-125">[Collects system performance counters](app-insights-performance-counters.md) such as CPU, memory and network load from IIS installations.</span></span> <span data-ttu-id="f9f09-126">Vous pouvez spécifier le compteurs toocollect, y compris les compteurs de performance que vous avez configuré vous-même.</span><span class="sxs-lookup"><span data-stu-id="f9f09-126">You can specify which counters toocollect, including performance counters you have set up yourself.</span></span>

* `Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule`
* <span data-ttu-id="f9f09-127">[Microsoft.ApplicationInsights.PerfCounterCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector) .</span><span class="sxs-lookup"><span data-stu-id="f9f09-127">[Microsoft.ApplicationInsights.PerfCounterCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector) NuGet package.</span></span>

### <a name="application-insights-diagnostics-telemetry"></a><span data-ttu-id="f9f09-128">Télémétrie des diagnostics Application Insights</span><span class="sxs-lookup"><span data-stu-id="f9f09-128">Application Insights Diagnostics Telemetry</span></span>
<span data-ttu-id="f9f09-129">Hello `DiagnosticsTelemetryModule` signale les erreurs dans hello le code d’instrumentation Application Insights lui-même.</span><span class="sxs-lookup"><span data-stu-id="f9f09-129">hello `DiagnosticsTelemetryModule` reports errors in hello Application Insights instrumentation code itself.</span></span> <span data-ttu-id="f9f09-130">Par exemple, si le code de hello ne peut pas accéder aux compteurs de performance ou si un `ITelemetryInitializer` lève une exception.</span><span class="sxs-lookup"><span data-stu-id="f9f09-130">For example, if hello code cannot access performance counters or if an `ITelemetryInitializer` throws an exception.</span></span> <span data-ttu-id="f9f09-131">Télémétrie des traces suivie par ce module s’affiche dans hello [recherche Diagnostic][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="f9f09-131">Trace telemetry tracked by this module appears in hello [Diagnostic Search][diagnostic].</span></span> <span data-ttu-id="f9f09-132">Envoie des données de diagnostic toodc.services.vsallin.net.</span><span class="sxs-lookup"><span data-stu-id="f9f09-132">Sends diagnostic data toodc.services.vsallin.net.</span></span>

* `Microsoft.ApplicationInsights.Extensibility.Implementation.Tracing.DiagnosticsTelemetryModule`
* <span data-ttu-id="f9f09-133">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) .</span><span class="sxs-lookup"><span data-stu-id="f9f09-133">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet package.</span></span> <span data-ttu-id="f9f09-134">Si vous installez uniquement ce package, fichier ApplicationInsights.config de hello n’est pas créé automatiquement.</span><span class="sxs-lookup"><span data-stu-id="f9f09-134">If you only install this package, hello ApplicationInsights.config file is not automatically created.</span></span>

### <a name="developer-mode"></a><span data-ttu-id="f9f09-135">Mode développeur</span><span class="sxs-lookup"><span data-stu-id="f9f09-135">Developer Mode</span></span>
<span data-ttu-id="f9f09-136">`DeveloperModeWithDebuggerAttachedTelemetryModule`force hello Application Insights `TelemetryChannel` toosend immédiatement les données, les éléments d’un télémétrie à la fois, quand un débogueur est attaché toohello processus d’application.</span><span class="sxs-lookup"><span data-stu-id="f9f09-136">`DeveloperModeWithDebuggerAttachedTelemetryModule` forces hello Application Insights `TelemetryChannel` toosend data immediately, one telemetry item at a time, when a debugger is attached toohello application process.</span></span> <span data-ttu-id="f9f09-137">Cela réduit la durée hello entre le moment de hello lorsque votre application effectue le suivi des données de télémétrie et lorsqu’il apparaît sur le portail Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="f9f09-137">This reduces hello amount of time between hello moment when your application tracks telemetry and when it appears on hello Application Insights portal.</span></span> <span data-ttu-id="f9f09-138">Cela cause une surcharge importante au niveau de l'UC et de la bande passante réseau.</span><span class="sxs-lookup"><span data-stu-id="f9f09-138">It causes significant overhead in CPU and network bandwidth.</span></span>

* `Microsoft.ApplicationInsights.WindowsServer.DeveloperModeWithDebuggerAttachedTelemetryModule`
* <span data-ttu-id="f9f09-139">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/)</span><span class="sxs-lookup"><span data-stu-id="f9f09-139">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet package</span></span>

### <a name="web-request-tracking"></a><span data-ttu-id="f9f09-140">Suivi des requêtes web</span><span class="sxs-lookup"><span data-stu-id="f9f09-140">Web Request Tracking</span></span>
<span data-ttu-id="f9f09-141">Hello de rapports [code d’heure et les résultats de réponse](app-insights-asp-net.md) de requêtes HTTP.</span><span class="sxs-lookup"><span data-stu-id="f9f09-141">Reports hello [response time and result code](app-insights-asp-net.md) of HTTP requests.</span></span>

* `Microsoft.ApplicationInsights.Web.RequestTrackingTelemetryModule`
* <span data-ttu-id="f9f09-142">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web)</span><span class="sxs-lookup"><span data-stu-id="f9f09-142">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet package</span></span>

### <a name="exception-tracking"></a><span data-ttu-id="f9f09-143">Suivi des exceptions</span><span class="sxs-lookup"><span data-stu-id="f9f09-143">Exception tracking</span></span>
<span data-ttu-id="f9f09-144">`ExceptionTrackingTelemetryModule` comptabilise le nombre d’exceptions non traitées dans votre application web.</span><span class="sxs-lookup"><span data-stu-id="f9f09-144">`ExceptionTrackingTelemetryModule` tracks unhandled exceptions in your web app.</span></span> <span data-ttu-id="f9f09-145">Consultez [Échecs et exceptions][exceptions].</span><span class="sxs-lookup"><span data-stu-id="f9f09-145">See [Failures and exceptions][exceptions].</span></span>

* `Microsoft.ApplicationInsights.Web.ExceptionTrackingTelemetryModule`
* <span data-ttu-id="f9f09-146">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web)</span><span class="sxs-lookup"><span data-stu-id="f9f09-146">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet package</span></span>
* <span data-ttu-id="f9f09-147">`Microsoft.ApplicationInsights.WindowsServer.UnobservedExceptionTelemetryModule` - suit [les exceptions de tâche non prises en charge](http://blogs.msdn.com/b/pfxteam/archive/2011/09/28/task-exception-handling-in-net-4-5.aspx).</span><span class="sxs-lookup"><span data-stu-id="f9f09-147">`Microsoft.ApplicationInsights.WindowsServer.UnobservedExceptionTelemetryModule` - tracks [unobserved task exceptions](http://blogs.msdn.com/b/pfxteam/archive/2011/09/28/task-exception-handling-in-net-4-5.aspx).</span></span>
* <span data-ttu-id="f9f09-148">`Microsoft.ApplicationInsights.WindowsServer.UnhandledExceptionTelemetryModule` - suit les exceptions non gérées pour les rôles de travail, les services Windows et les applications de console.</span><span class="sxs-lookup"><span data-stu-id="f9f09-148">`Microsoft.ApplicationInsights.WindowsServer.UnhandledExceptionTelemetryModule` - tracks unhandled exceptions for worker roles, windows services, and console applications.</span></span>
* <span data-ttu-id="f9f09-149">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) .</span><span class="sxs-lookup"><span data-stu-id="f9f09-149">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet package.</span></span>

### <a name="eventsource-tracking"></a><span data-ttu-id="f9f09-150">Suivi EventSource</span><span class="sxs-lookup"><span data-stu-id="f9f09-150">EventSource Tracking</span></span>
<span data-ttu-id="f9f09-151">`EventSourceTelemetryModule`vous permet de tooconfigure toobe d’événements EventSource envoyé tooApplication Insights en tant que les traces.</span><span class="sxs-lookup"><span data-stu-id="f9f09-151">`EventSourceTelemetryModule` allows you tooconfigure EventSource events toobe sent tooApplication Insights as traces.</span></span> <span data-ttu-id="f9f09-152">Pour plus d’informations sur le suivi des événements EventSource, consultez [Utilisation d’événements EventSource](app-insights-asp-net-trace-logs.md#using-eventsource-events).</span><span class="sxs-lookup"><span data-stu-id="f9f09-152">For information on tracking EventSource events, see [Using EventSource Events](app-insights-asp-net-trace-logs.md#using-eventsource-events).</span></span>

* `Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule`
* [<span data-ttu-id="f9f09-153">Microsoft.ApplicationInsights.EventSourceListener</span><span class="sxs-lookup"><span data-stu-id="f9f09-153">Microsoft.ApplicationInsights.EventSourceListener</span></span>](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EventSourceListener) 

### <a name="etw-event-tracking"></a><span data-ttu-id="f9f09-154">Suivi des événements ETW</span><span class="sxs-lookup"><span data-stu-id="f9f09-154">ETW Event Tracking</span></span>
<span data-ttu-id="f9f09-155">`EtwCollectorTelemetryModule`vous permet d’événements tooconfigure toobe de fournisseurs ETW envoyé tooApplication Insights en tant que les traces.</span><span class="sxs-lookup"><span data-stu-id="f9f09-155">`EtwCollectorTelemetryModule` allows you tooconfigure events from ETW providers toobe sent tooApplication Insights as traces.</span></span> <span data-ttu-id="f9f09-156">Pour plus d’informations sur le suivi des événements ETW, consultez [Utilisation d’événements ETW](app-insights-asp-net-trace-logs.md#using-etw-events).</span><span class="sxs-lookup"><span data-stu-id="f9f09-156">For information on tracking ETW events, see [Using ETW Events](app-insights-asp-net-trace-logs.md#using-etw-events).</span></span>

* `Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule`
* [<span data-ttu-id="f9f09-157">Microsoft.ApplicationInsights.EtwCollector</span><span class="sxs-lookup"><span data-stu-id="f9f09-157">Microsoft.ApplicationInsights.EtwCollector</span></span>](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EtwCollector) 

### <a name="microsoftapplicationinsights"></a><span data-ttu-id="f9f09-158">Microsoft.ApplicationInsights</span><span class="sxs-lookup"><span data-stu-id="f9f09-158">Microsoft.ApplicationInsights</span></span>
<span data-ttu-id="f9f09-159">Hello Microsoft.ApplicationInsights offre hello [core API](https://msdn.microsoft.com/library/mt420197.aspx) Hello SDK.</span><span class="sxs-lookup"><span data-stu-id="f9f09-159">hello Microsoft.ApplicationInsights package provides hello [core API](https://msdn.microsoft.com/library/mt420197.aspx) of hello SDK.</span></span> <span data-ttu-id="f9f09-160">Hello autres modules de télémétrie utilisent, et vous pouvez également [toodefine l’utiliser vos propres données de télémétrie](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="f9f09-160">hello other telemetry modules use this, and you can also [use it toodefine your own telemetry](app-insights-api-custom-events-metrics.md).</span></span>

* <span data-ttu-id="f9f09-161">Aucune entrée dans ApplicationInsights.config.</span><span class="sxs-lookup"><span data-stu-id="f9f09-161">No entry in ApplicationInsights.config.</span></span>
* <span data-ttu-id="f9f09-162">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) .</span><span class="sxs-lookup"><span data-stu-id="f9f09-162">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet package.</span></span> <span data-ttu-id="f9f09-163">Si vous installez simplement ce package NuGet, aucun fichier .config n'est créé.</span><span class="sxs-lookup"><span data-stu-id="f9f09-163">If you just install this NuGet, no .config file is generated.</span></span>

## <a name="telemetry-channel"></a><span data-ttu-id="f9f09-164">Canal de télémétrie</span><span class="sxs-lookup"><span data-stu-id="f9f09-164">Telemetry Channel</span></span>
<span data-ttu-id="f9f09-165">canal de données de télémétrie Hello gère la mise en mémoire tampon et la transmission des données de télémétrie toohello service Application Insights.</span><span class="sxs-lookup"><span data-stu-id="f9f09-165">hello telemetry channel manages buffering and transmission of telemetry toohello Application Insights service.</span></span>

* <span data-ttu-id="f9f09-166">`Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.ServerTelemetryChannel`est le canal par défaut de hello pour les services.</span><span class="sxs-lookup"><span data-stu-id="f9f09-166">`Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.ServerTelemetryChannel` is hello default channel for services.</span></span> <span data-ttu-id="f9f09-167">Il met les données en mémoire.</span><span class="sxs-lookup"><span data-stu-id="f9f09-167">It buffers data in memory.</span></span>
* <span data-ttu-id="f9f09-168">`Microsoft.ApplicationInsights.PersistenceChannel` est une alternative pour les applications de console.</span><span class="sxs-lookup"><span data-stu-id="f9f09-168">`Microsoft.ApplicationInsights.PersistenceChannel` is an alternative for console applications.</span></span> <span data-ttu-id="f9f09-169">Il peut enregistrer n’importe quel stockage toopersistent de données vidées lorsque votre application ferme et enverra lors de l’application hello démarre à nouveau.</span><span class="sxs-lookup"><span data-stu-id="f9f09-169">It can save any unflushed data toopersistent storage when your app closes down, and will send it when hello app starts again.</span></span>

## <a name="telemetry-initializers-aspnet"></a><span data-ttu-id="f9f09-170">Initialiseurs de télémétrie (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="f9f09-170">Telemetry Initializers (ASP.NET)</span></span>
<span data-ttu-id="f9f09-171">Les initialiseurs de télémétrie définissent les propriétés de contexte envoyées avec chaque élément de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="f9f09-171">Telemetry initializers set context properties that are sent along with every item of telemetry.</span></span>

<span data-ttu-id="f9f09-172">Vous pouvez [écrire vos propres initialiseurs](app-insights-api-filtering-sampling.md#add-properties) tooset les propriétés de contexte.</span><span class="sxs-lookup"><span data-stu-id="f9f09-172">You can [write your own initializers](app-insights-api-filtering-sampling.md#add-properties) tooset context properties.</span></span>

<span data-ttu-id="f9f09-173">les initialiseurs standard Hello sont tous définis en hello Web ou WindowsServer NuGet packages :</span><span class="sxs-lookup"><span data-stu-id="f9f09-173">hello standard initializers are all set either by hello Web or WindowsServer NuGet packages:</span></span>

* <span data-ttu-id="f9f09-174">`AccountIdTelemetryInitializer`définit la propriété d’ID de compte hello.</span><span class="sxs-lookup"><span data-stu-id="f9f09-174">`AccountIdTelemetryInitializer` sets hello AccountId property.</span></span>
* <span data-ttu-id="f9f09-175">`AuthenticatedUserIdTelemetryInitializer`définit la propriété AuthenticatedUserId de hello en tant que jeu par hello SDK JavaScript.</span><span class="sxs-lookup"><span data-stu-id="f9f09-175">`AuthenticatedUserIdTelemetryInitializer` sets hello AuthenticatedUserId property as set by hello JavaScript SDK.</span></span>
* <span data-ttu-id="f9f09-176">`AzureRoleEnvironmentTelemetryInitializer`hello de mises à jour `RoleName` et `RoleInstance` propriétés Hello `Device` contexte pour tous les éléments de télémétrie avec des informations extraites de l’environnement d’exécution Azure hello.</span><span class="sxs-lookup"><span data-stu-id="f9f09-176">`AzureRoleEnvironmentTelemetryInitializer` updates hello `RoleName` and `RoleInstance` properties of hello `Device` context for all telemetry items with information extracted from hello Azure runtime environment.</span></span>
* <span data-ttu-id="f9f09-177">`BuildInfoConfigComponentVersionTelemetryInitializer`hello de mises à jour `Version` propriété Hello `Component` contexte pour tous les éléments de télémétrie avec la valeur hello extraites hello `BuildInfo.config` fichier produit par MS Build.</span><span class="sxs-lookup"><span data-stu-id="f9f09-177">`BuildInfoConfigComponentVersionTelemetryInitializer` updates hello `Version` property of hello `Component` context for all telemetry items with hello value extracted from hello `BuildInfo.config` file produced by MS Build.</span></span>
* <span data-ttu-id="f9f09-178">`ClientIpHeaderTelemetryInitializer`les mises à jour `Ip` propriété Hello `Location` le contexte de tous les éléments de télémétrie en fonction hello `X-Forwarded-For` en-tête HTTP de la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="f9f09-178">`ClientIpHeaderTelemetryInitializer` updates `Ip` property of hello `Location` context of all telemetry items based on hello `X-Forwarded-For` HTTP header of hello request.</span></span>
* <span data-ttu-id="f9f09-179">`DeviceTelemetryInitializer`hello mises à jour les propriétés de hello suivantes `Device` contexte pour tous les éléments de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="f9f09-179">`DeviceTelemetryInitializer` updates hello following properties of hello `Device` context for all telemetry items.</span></span>
  * <span data-ttu-id="f9f09-180">`Type`est défini trop « PC »</span><span class="sxs-lookup"><span data-stu-id="f9f09-180">`Type` is set too"PC"</span></span>
  * <span data-ttu-id="f9f09-181">`Id`a la valeur toohello nom de domaine de l’ordinateur de hello où l’application web de hello est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="f9f09-181">`Id` is set toohello domain name of hello computer where hello web application is running.</span></span>
  * <span data-ttu-id="f9f09-182">`OemName`a la valeur toohello extraite hello `Win32_ComputerSystem.Manufacturer` champ à l’aide de WMI.</span><span class="sxs-lookup"><span data-stu-id="f9f09-182">`OemName` is set toohello value extracted from hello `Win32_ComputerSystem.Manufacturer` field using WMI.</span></span>
  * <span data-ttu-id="f9f09-183">`Model`a la valeur toohello extraite hello `Win32_ComputerSystem.Model` champ à l’aide de WMI.</span><span class="sxs-lookup"><span data-stu-id="f9f09-183">`Model` is set toohello value extracted from hello `Win32_ComputerSystem.Model` field using WMI.</span></span>
  * <span data-ttu-id="f9f09-184">`NetworkType`a la valeur toohello extraite hello `NetworkInterface`.</span><span class="sxs-lookup"><span data-stu-id="f9f09-184">`NetworkType` is set toohello value extracted from hello `NetworkInterface`.</span></span>
  * <span data-ttu-id="f9f09-185">`Language`a la valeur nom toohello Hello `CurrentCulture`.</span><span class="sxs-lookup"><span data-stu-id="f9f09-185">`Language` is set toohello name of hello `CurrentCulture`.</span></span>
* <span data-ttu-id="f9f09-186">`DomainNameRoleInstanceTelemetryInitializer`hello de mises à jour `RoleInstance` propriété Hello `Device` contexte pour tous les éléments de télémétrie avec le nom de domaine hello d’ordinateur hello où l’application web de hello est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="f9f09-186">`DomainNameRoleInstanceTelemetryInitializer` updates hello `RoleInstance` property of hello `Device` context for all telemetry items with hello domain name of hello computer where hello web application is running.</span></span>
* <span data-ttu-id="f9f09-187">`OperationNameTelemetryInitializer`hello de mises à jour `Name` propriété Hello `RequestTelemetry` et hello `Name` propriété Hello `Operation` contexte de tous les éléments de télémétrie en fonction de la méthode hello HTTP, ainsi que leurs noms de hello de tooprocess appelé contrôleur et d’action ASP.NET MVC demande.</span><span class="sxs-lookup"><span data-stu-id="f9f09-187">`OperationNameTelemetryInitializer` updates hello `Name` property of hello `RequestTelemetry` and hello `Name` property of hello `Operation` context of all telemetry items based on hello HTTP method, as well as names of ASP.NET MVC controller and action invoked tooprocess hello request.</span></span>
* <span data-ttu-id="f9f09-188">`OperationIdTelemetryInitializer`ou `OperationCorrelationTelemetryInitializer` hello de mises à jour `Operation.Id` propriété de contexte de tous les éléments de télémétrie suivies lors du traitement d’une demande avec hello généré automatiquement `RequestTelemetry.Id`.</span><span class="sxs-lookup"><span data-stu-id="f9f09-188">`OperationIdTelemetryInitializer` or `OperationCorrelationTelemetryInitializer` updates hello `Operation.Id` context property of all telemetry items tracked while handling a request with hello automatically generated `RequestTelemetry.Id`.</span></span>
* <span data-ttu-id="f9f09-189">`SessionTelemetryInitializer`hello de mises à jour `Id` propriété Hello `Session` contexte pour tous les éléments de télémétrie avec la valeur extraite de hello `ai_session` cookie généré par hello le code d’instrumentation ApplicationInsights JavaScript en cours d’exécution dans le navigateur de l’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="f9f09-189">`SessionTelemetryInitializer` updates hello `Id` property of hello `Session` context for all telemetry items with value extracted from hello `ai_session` cookie generated by hello ApplicationInsights JavaScript instrumentation code running in hello user's browser.</span></span>
* <span data-ttu-id="f9f09-190">`SyntheticTelemetryInitializer`ou `SyntheticUserAgentTelemetryInitializer` hello de mises à jour `User`, `Session` et `Operation` des propriétés de contextes de tous les éléments de télémétrie suivies lors du traitement d’une demande émanant d’une source synthétique, comme une disponibilité de test ou robot de moteur de recherche.</span><span class="sxs-lookup"><span data-stu-id="f9f09-190">`SyntheticTelemetryInitializer` or `SyntheticUserAgentTelemetryInitializer` updates hello `User`, `Session` and `Operation` contexts properties of all telemetry items tracked when handling a request from a synthetic source, such as an availability test or search engine bot.</span></span> <span data-ttu-id="f9f09-191">Par défaut, [Metrics Explorer](app-insights-metrics-explorer.md) n'affiche pas la télémétrie synthétique.</span><span class="sxs-lookup"><span data-stu-id="f9f09-191">By default, [Metrics Explorer](app-insights-metrics-explorer.md) does not display synthetic telemetry.</span></span>

    <span data-ttu-id="f9f09-192">Hello `<Filters>` définir l’identification des propriétés de demandes de hello.</span><span class="sxs-lookup"><span data-stu-id="f9f09-192">hello `<Filters>` set identifying properties of hello requests.</span></span>
* <span data-ttu-id="f9f09-193">`UserAgentTelemetryInitializer`hello de mises à jour `UserAgent` propriété Hello `User` le contexte de tous les éléments de télémétrie en fonction hello `User-Agent` en-tête HTTP de la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="f9f09-193">`UserAgentTelemetryInitializer` updates hello `UserAgent` property of hello `User` context of all telemetry items based on hello `User-Agent` HTTP header of hello request.</span></span>
* <span data-ttu-id="f9f09-194">`UserTelemetryInitializer`hello de mises à jour `Id` et `AcquisitionDate` propriétés de `User` contexte pour tous les éléments de télémétrie avec des valeurs extraites hello `ai_user` cookie généré par le code d’instrumentation Application Insights JavaScript hello en hello navigateur de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f9f09-194">`UserTelemetryInitializer` updates hello `Id` and `AcquisitionDate` properties of `User` context for all telemetry items with values extracted from hello `ai_user` cookie generated by hello Application Insights JavaScript instrumentation code running in hello user's browser.</span></span>
* <span data-ttu-id="f9f09-195">`WebTestTelemetryInitializer`jeux de hello id utilisateur, les id de session et les propriétés de la source de synthèse pour des requêtes HTTP provenant de [les tests de disponibilité](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="f9f09-195">`WebTestTelemetryInitializer` sets hello user id, session id and synthetic source properties for HTTP requests that come from [availability tests](app-insights-monitor-web-app-availability.md).</span></span>
  <span data-ttu-id="f9f09-196">Hello `<Filters>` définir l’identification des propriétés de demandes de hello.</span><span class="sxs-lookup"><span data-stu-id="f9f09-196">hello `<Filters>` set identifying properties of hello requests.</span></span>

<span data-ttu-id="f9f09-197">Pour les applications .NET en cours d’exécution dans l’infrastructure de Service, vous pouvez inclure hello `Microsoft.ApplicationInsights.ServiceFabric` package NuGet.</span><span class="sxs-lookup"><span data-stu-id="f9f09-197">For .NET applications running in Service Fabric, you can include hello `Microsoft.ApplicationInsights.ServiceFabric` NuGet package.</span></span> <span data-ttu-id="f9f09-198">Ce package comprend un `FabricTelemetryInitializer`, qui ajoute des éléments de tootelemetry de propriétés de l’infrastructure de Service.</span><span class="sxs-lookup"><span data-stu-id="f9f09-198">This package includes a `FabricTelemetryInitializer`, which adds Service Fabric properties tootelemetry items.</span></span> <span data-ttu-id="f9f09-199">Pour plus d’informations, consultez hello [page GitHub](https://go.microsoft.com/fwlink/?linkid=848457) sur les propriétés hello ajoutées par ce package NuGet.</span><span class="sxs-lookup"><span data-stu-id="f9f09-199">For more information, see hello [GitHub page](https://go.microsoft.com/fwlink/?linkid=848457) about hello properties added by this NuGet package.</span></span>

## <a name="telemetry-processors-aspnet"></a><span data-ttu-id="f9f09-200">Processeurs de télémétrie (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="f9f09-200">Telemetry Processors (ASP.NET)</span></span>
<span data-ttu-id="f9f09-201">Processeurs de télémétrie peuvent filtrer et modifier chaque élément de données de télémétrie juste avant d’être envoyée à partir du portail de toohello hello Kit de développement logiciel.</span><span class="sxs-lookup"><span data-stu-id="f9f09-201">Telemetry processors can filter and modify each telemetry item just before it is sent from hello SDK toohello portal.</span></span>

<span data-ttu-id="f9f09-202">Vous pouvez [écrire vos propres processeurs de télémétrie](app-insights-api-filtering-sampling.md#filtering).</span><span class="sxs-lookup"><span data-stu-id="f9f09-202">You can [write your own telemetry processors](app-insights-api-filtering-sampling.md#filtering).</span></span>

#### <a name="adaptive-sampling-telemetry-processor-from-200-beta3"></a><span data-ttu-id="f9f09-203">Processeur de télémétrie d'échantillonnage adaptatif (à partir de 2.0.0-beta3)</span><span class="sxs-lookup"><span data-stu-id="f9f09-203">Adaptive sampling telemetry processor (from 2.0.0-beta3)</span></span>
<span data-ttu-id="f9f09-204">Cette option est activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="f9f09-204">This is enabled by default.</span></span> <span data-ttu-id="f9f09-205">Si votre application envoie beaucoup de télémétrie, ce processeur en supprime une partie.</span><span class="sxs-lookup"><span data-stu-id="f9f09-205">If your app sends a lot of telemetry, this processor removes some of it.</span></span>

```xml

    <TelemetryProcessors>
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    </TelemetryProcessors>

```

<span data-ttu-id="f9f09-206">paramètre Hello fournit cible hello hello algorithme tente tooachieve.</span><span class="sxs-lookup"><span data-stu-id="f9f09-206">hello parameter provides hello target that hello algorithm tries tooachieve.</span></span> <span data-ttu-id="f9f09-207">Chaque instance de hello SDK fonctionne indépendamment, afin que si votre serveur est un cluster de plusieurs ordinateurs, volume effectif hello télémétrie sera multiplié en conséquence.</span><span class="sxs-lookup"><span data-stu-id="f9f09-207">Each instance of hello SDK works independently, so if your server is a cluster of several machines, hello actual volume of telemetry will be multiplied accordingly.</span></span>

<span data-ttu-id="f9f09-208">[En savoir plus sur l'échantillonnage](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="f9f09-208">[Learn more about sampling](app-insights-sampling.md).</span></span>

#### <a name="fixed-rate-sampling-telemetry-processor-from-200-beta1"></a><span data-ttu-id="f9f09-209">Processeur de télémétrie d'échantillonnage à taux fixe (à partir de 2.0.0-beta1)</span><span class="sxs-lookup"><span data-stu-id="f9f09-209">Fixed-rate sampling telemetry processor (from 2.0.0-beta1)</span></span>
<span data-ttu-id="f9f09-210">Il existe également un [processeur de télémétrie d’échantillonnage](app-insights-api-filtering-sampling.md) standard (à partir de 2.0.1) :</span><span class="sxs-lookup"><span data-stu-id="f9f09-210">There is also a standard [sampling telemetry processor](app-insights-api-filtering-sampling.md) (from 2.0.1):</span></span>

```XML

    <TelemetryProcessors>
     <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">

     <!-- Set a percentage close too100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
     <SamplingPercentage>10</SamplingPercentage>
     </Add>
   </TelemetryProcessors>

```



## <a name="channel-parameters-java"></a><span data-ttu-id="f9f09-211">Paramètres de canal (Java)</span><span class="sxs-lookup"><span data-stu-id="f9f09-211">Channel parameters (Java)</span></span>
<span data-ttu-id="f9f09-212">Ces paramètres affectent la hello Kit de développement logiciel Java doit stocker et vider les données de télémétrie hello qu’il collecte.</span><span class="sxs-lookup"><span data-stu-id="f9f09-212">These parameters affect how hello Java SDK should store and flush hello telemetry data that it collects.</span></span>

#### <a name="maxtelemetrybuffercapacity"></a><span data-ttu-id="f9f09-213">MaxTelemetryBufferCapacity</span><span class="sxs-lookup"><span data-stu-id="f9f09-213">MaxTelemetryBufferCapacity</span></span>
<span data-ttu-id="f9f09-214">nombre de Hello d’éléments de télémétrie qui peuvent être stockées dans le stockage en mémoire du Kit de développement hello.</span><span class="sxs-lookup"><span data-stu-id="f9f09-214">hello number of telemetry items that can be stored in hello SDK's in-memory storage.</span></span> <span data-ttu-id="f9f09-215">Lorsque ce nombre est atteint, mémoire tampon de données de télémétrie hello est vidé, autrement dit, les éléments de télémétrie hello sont envoyés de serveur d’Application Insights toohello.</span><span class="sxs-lookup"><span data-stu-id="f9f09-215">When this number is reached, hello telemetry buffer is flushed - that is, hello telemetry items are sent toohello Application Insights server.</span></span>

* <span data-ttu-id="f9f09-216">Min : 1</span><span class="sxs-lookup"><span data-stu-id="f9f09-216">Min: 1</span></span>
* <span data-ttu-id="f9f09-217">Max : 1000</span><span class="sxs-lookup"><span data-stu-id="f9f09-217">Max: 1000</span></span>
* <span data-ttu-id="f9f09-218">Valeur par défaut : 500</span><span class="sxs-lookup"><span data-stu-id="f9f09-218">Default: 500</span></span>

```

  <ApplicationInsights>
      ...
      <Channel>
       <MaxTelemetryBufferCapacity>100</MaxTelemetryBufferCapacity>
      </Channel>
      ...
  </ApplicationInsights>
```

#### <a name="flushintervalinseconds"></a><span data-ttu-id="f9f09-219">FlushIntervalInSeconds</span><span class="sxs-lookup"><span data-stu-id="f9f09-219">FlushIntervalInSeconds</span></span>
<span data-ttu-id="f9f09-220">Détermine la fréquence à laquelle hello les données stockées dans le stockage en mémoire hello doivent être vidée (une tooApplication envoyée Insights).</span><span class="sxs-lookup"><span data-stu-id="f9f09-220">Determines how often hello data that is stored in hello in-memory storage should be flushed (sent tooApplication Insights).</span></span>

* <span data-ttu-id="f9f09-221">Min : 1</span><span class="sxs-lookup"><span data-stu-id="f9f09-221">Min: 1</span></span>
* <span data-ttu-id="f9f09-222">Max : 300</span><span class="sxs-lookup"><span data-stu-id="f9f09-222">Max: 300</span></span>
* <span data-ttu-id="f9f09-223">Valeur par défaut : 5</span><span class="sxs-lookup"><span data-stu-id="f9f09-223">Default: 5</span></span>

```

    <ApplicationInsights>
      ...
      <Channel>
        <FlushIntervalInSeconds>100</FlushIntervalInSeconds>
      </Channel>
      ...
    </ApplicationInsights>
```

#### <a name="maxtransmissionstoragecapacityinmb"></a><span data-ttu-id="f9f09-224">MaxTransmissionStorageCapacityInMB</span><span class="sxs-lookup"><span data-stu-id="f9f09-224">MaxTransmissionStorageCapacityInMB</span></span>
<span data-ttu-id="f9f09-225">Détermine la taille maximale de hello en Mo allouée toohello le stockage persistant sur le disque local hello.</span><span class="sxs-lookup"><span data-stu-id="f9f09-225">Determines hello maximum size in MB that is allotted toohello persistent storage on hello local disk.</span></span> <span data-ttu-id="f9f09-226">Ce stockage est utilisé pour les éléments de télémétrie persistants qui ont échoué le point de terminaison toobe transmis toohello Application Insights.</span><span class="sxs-lookup"><span data-stu-id="f9f09-226">This storage is used for persisting telemetry items that failed toobe transmitted toohello Application Insights endpoint.</span></span> <span data-ttu-id="f9f09-227">Lorsque la taille de stockage hello a été rencontrée, les nouveaux éléments de télémétrie seront ignorées.</span><span class="sxs-lookup"><span data-stu-id="f9f09-227">When hello storage size has been met, new telemetry items will be discarded.</span></span>

* <span data-ttu-id="f9f09-228">Min : 1</span><span class="sxs-lookup"><span data-stu-id="f9f09-228">Min: 1</span></span>
* <span data-ttu-id="f9f09-229">Max : 100</span><span class="sxs-lookup"><span data-stu-id="f9f09-229">Max: 100</span></span>
* <span data-ttu-id="f9f09-230">Valeur par défaut : 10</span><span class="sxs-lookup"><span data-stu-id="f9f09-230">Default: 10</span></span>

```

   <ApplicationInsights>
      ...
      <Channel>
        <MaxTransmissionStorageCapacityInMB>50</MaxTransmissionStorageCapacityInMB>
      </Channel>
      ...
   </ApplicationInsights>
```



## <a name="instrumentationkey"></a><span data-ttu-id="f9f09-231">InstrumentationKey</span><span class="sxs-lookup"><span data-stu-id="f9f09-231">InstrumentationKey</span></span>
<span data-ttu-id="f9f09-232">Cela détermine la ressource d’Application Insights hello dans lequel vos données s’affiche.</span><span class="sxs-lookup"><span data-stu-id="f9f09-232">This determines hello Application Insights resource in which your data appears.</span></span> <span data-ttu-id="f9f09-233">En général, vous créez une ressource séparée, avec une clé distincte, pour chacune de vos applications.</span><span class="sxs-lookup"><span data-stu-id="f9f09-233">Typically you create a separate resource, with a separate key, for each of your applications.</span></span>

<span data-ttu-id="f9f09-234">Si vous souhaitez tooset hello clé dynamiquement, par exemple si vous souhaitez que les résultats de toosend à partir de vos ressources d’application toodifferent - vous pouvez omettre la clé hello à partir du fichier de configuration hello et définir dans le code.</span><span class="sxs-lookup"><span data-stu-id="f9f09-234">If you want tooset hello key dynamically - for example if you want toosend results from your application toodifferent resources - you can omit hello key from hello configuration file, and set it in code instead.</span></span>

<span data-ttu-id="f9f09-235">clé de hello tooset pour toutes les instances de TelemetryClient, y compris les modules de télémétrie standard, définie des clé de hello dans TelemetryConfiguration.Active.</span><span class="sxs-lookup"><span data-stu-id="f9f09-235">tooset hello key for all instances of TelemetryClient, including standard telemetry modules, set hello key in TelemetryConfiguration.Active.</span></span> <span data-ttu-id="f9f09-236">Définissez-la dans une méthode d’initialisation, telle que global.aspx.cs dans un service ASP.NET :</span><span class="sxs-lookup"><span data-stu-id="f9f09-236">Do this in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

```C#

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      //...
```

<span data-ttu-id="f9f09-237">Si vous souhaitez simplement toosend un ensemble spécifique de ressources de différents événements tooa, vous pouvez définir la clé de hello pour un TelemetryClient spécifique :</span><span class="sxs-lookup"><span data-stu-id="f9f09-237">If you just want toosend a specific set of events tooa different resource, you can set hello key for a specific TelemetryClient:</span></span>

```C#

    var tc = new TelemetryClient();
    tc.Context.InstrumentationKey = "----- my key ----";
    tc.TrackEvent("myEvent");
    // ...

```

<span data-ttu-id="f9f09-238">une nouvelle clé de tooget [créer une ressource dans le portail d’Application Insights hello][new].</span><span class="sxs-lookup"><span data-stu-id="f9f09-238">tooget a new key, [create a new resource in hello Application Insights portal][new].</span></span>

## <a name="next-steps"></a><span data-ttu-id="f9f09-239">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f9f09-239">Next steps</span></span>
<span data-ttu-id="f9f09-240">[En savoir plus sur les API de hello][api].</span><span class="sxs-lookup"><span data-stu-id="f9f09-240">[Learn more about hello API][api].</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[netlogs]: app-insights-asp-net-trace-logs.md
[new]: app-insights-create-new-resource.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
