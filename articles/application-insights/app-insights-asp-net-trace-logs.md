---
title: les journaux de suivi de .NET aaaExplore dans Application Insights
description: "Effectuez une recherche dans les journaux générés avec Trace, NLog ou Log4Net."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 0c2a084f-6e71-467b-a6aa-4ab222f17153
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/3/2017
ms.author: bwren
ms.openlocfilehash: 6bfcd9e5751c3656236d7eb2fc09321740171a70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="explore-net-trace-logs-in-application-insights"></a><span data-ttu-id="33dcb-103">Exploration des journaux .NET dans Application Insights</span><span class="sxs-lookup"><span data-stu-id="33dcb-103">Explore .NET trace logs in Application Insights</span></span>
<span data-ttu-id="33dcb-104">Si vous utilisez NLog, log4Net ou System.Diagnostics.Trace pour le suivi de diagnostic dans votre application ASP.NET, vous pouvez avoir vos journaux envoyés trop[Azure Application Insights][start], où vous pouvez Explorer et rechercher les.</span><span class="sxs-lookup"><span data-stu-id="33dcb-104">If you use NLog, log4Net or System.Diagnostics.Trace for diagnostic tracing in your ASP.NET application, you can have your logs sent too[Azure Application Insights][start], where you can explore and search them.</span></span> <span data-ttu-id="33dcb-105">Les journaux sont fusionnées avec hello autres télémétrie en provenance de votre application, afin que vous puissiez identifier hello traces associés à chaque demande de l’utilisateur de maintenance et les mettre en corrélation avec d’autres événements et les rapports d’exception.</span><span class="sxs-lookup"><span data-stu-id="33dcb-105">Your logs will be merged with hello other telemetry coming from your application, so that you can identify hello traces associated with servicing each user request, and correlate them with other events and exception reports.</span></span>

> [!NOTE]
> <span data-ttu-id="33dcb-106">Module de capture de journal hello avez-vous besoin ?</span><span class="sxs-lookup"><span data-stu-id="33dcb-106">Do you need hello log capture module?</span></span> <span data-ttu-id="33dcb-107">Il s’agit d’un adaptateur très utile pour les enregistreurs d’événements tiers. Cependant, si vous n’utilisez pas déjà NLog, log4Net ou System.Diagnostics.Trace, vous pouvez appeler [Application Insights TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) directement.</span><span class="sxs-lookup"><span data-stu-id="33dcb-107">It's a useful adapter for 3rd-party loggers, but if you aren't already using NLog, log4Net or System.Diagnostics.Trace, consider just calling [Application Insights TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) directly.</span></span>
>
>

## <a name="install-logging-on-your-app"></a><span data-ttu-id="33dcb-108">Installation de la journalisation sur votre application</span><span class="sxs-lookup"><span data-stu-id="33dcb-108">Install logging on your app</span></span>
<span data-ttu-id="33dcb-109">Installez votre infrastructure de journalisation choisie dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="33dcb-109">Install your chosen logging framework in your project.</span></span> <span data-ttu-id="33dcb-110">Ceci devrait générer une entrée dans le fichier app.config ou web.config.</span><span class="sxs-lookup"><span data-stu-id="33dcb-110">This should result in an entry in app.config or web.config.</span></span>

<span data-ttu-id="33dcb-111">Si vous utilisez System.Diagnostics.Trace, vous devez tooadd une tooweb.config d’entrée :</span><span class="sxs-lookup"><span data-stu-id="33dcb-111">If you're using System.Diagnostics.Trace, you need tooadd an entry tooweb.config:</span></span>

```XML

    <configuration>
     <system.diagnostics>
       <trace autoflush="false" indentsize="4">
         <listeners>
           <add name="myListener"
             type="System.Diagnostics.TextWriterTraceListener"
             initializeData="TextWriterOutput.log" />
           <remove name="Default" />
         </listeners>
       </trace>
     </system.diagnostics>
   </configuration>
```
## <a name="configure-application-insights-toocollect-logs"></a><span data-ttu-id="33dcb-112">Configurer les journaux d’Application Insights toocollect</span><span class="sxs-lookup"><span data-stu-id="33dcb-112">Configure Application Insights toocollect logs</span></span>
<span data-ttu-id="33dcb-113">**[Ajouter le projet d’Application Insights tooyour](app-insights-asp-net.md)**  si vous n’avez pas encore fait.</span><span class="sxs-lookup"><span data-stu-id="33dcb-113">**[Add Application Insights tooyour project](app-insights-asp-net.md)** if you haven't done that yet.</span></span> <span data-ttu-id="33dcb-114">Vous verrez un collecteur de journaux option tooinclude hello.</span><span class="sxs-lookup"><span data-stu-id="33dcb-114">You'll see an option tooinclude hello log collector.</span></span>

<span data-ttu-id="33dcb-115">Ou **configurez Application Insights** en cliquant avec le bouton droit dans l’Explorateur de solutions.</span><span class="sxs-lookup"><span data-stu-id="33dcb-115">Or **Configure Application Insights** by right-clicking your project in Solution Explorer.</span></span> <span data-ttu-id="33dcb-116">L’option hello trop**configurer la collecte de trace**.</span><span class="sxs-lookup"><span data-stu-id="33dcb-116">Select hello option too**Configure trace collection**.</span></span>

<span data-ttu-id="33dcb-117">*Menu Application Insights non disponible ou aucune option pour le collecteur de journaux ?*</span><span class="sxs-lookup"><span data-stu-id="33dcb-117">*No Application Insights menu or log collector option?*</span></span> <span data-ttu-id="33dcb-118">Consultez la [Résolution des problèmes](#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="33dcb-118">Try [Troubleshooting](#troubleshooting).</span></span>

## <a name="manual-installation"></a><span data-ttu-id="33dcb-119">Installation manuelle</span><span class="sxs-lookup"><span data-stu-id="33dcb-119">Manual installation</span></span>
<span data-ttu-id="33dcb-120">Utilisez cette méthode si votre type de projet n’est pas pris en charge par le programme d’installation de l’Application Insights hello (par exemple un projet de bureau Windows).</span><span class="sxs-lookup"><span data-stu-id="33dcb-120">Use this method if your project type isn't supported by hello Application Insights installer (for example a Windows desktop project).</span></span>

1. <span data-ttu-id="33dcb-121">Si vous envisagez de toouse log4Net ou NLog, l’installer dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="33dcb-121">If you plan toouse log4Net or NLog, install it in your project.</span></span>
2. <span data-ttu-id="33dcb-122">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur le projet, puis sélectionnez **Gérer les packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="33dcb-122">In Solution Explorer, right-click your project and choose **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="33dcb-123">Recherchez « Application Insights »</span><span class="sxs-lookup"><span data-stu-id="33dcb-123">Search for "Application Insights"</span></span>
4. <span data-ttu-id="33dcb-124">Sélectionnez le package approprié de hello - un des :</span><span class="sxs-lookup"><span data-stu-id="33dcb-124">Select hello appropriate package - one of:</span></span>

   * <span data-ttu-id="33dcb-125">Microsoft.ApplicationInsights.TraceListener (appels de System.Diagnostics.Trace toocapture)</span><span class="sxs-lookup"><span data-stu-id="33dcb-125">Microsoft.ApplicationInsights.TraceListener (toocapture System.Diagnostics.Trace calls)</span></span>
   * <span data-ttu-id="33dcb-126">Microsoft.ApplicationInsights.EventSourceListener (événements EventSource de toocapture)</span><span class="sxs-lookup"><span data-stu-id="33dcb-126">Microsoft.ApplicationInsights.EventSourceListener (toocapture EventSource events)</span></span>
   * <span data-ttu-id="33dcb-127">Microsoft.ApplicationInsights.EtwListener (événements ETW de toocapture)</span><span class="sxs-lookup"><span data-stu-id="33dcb-127">Microsoft.ApplicationInsights.EtwListener (toocapture ETW events)</span></span>
   * <span data-ttu-id="33dcb-128">Microsoft.ApplicationInsights.NLogTarget</span><span class="sxs-lookup"><span data-stu-id="33dcb-128">Microsoft.ApplicationInsights.NLogTarget</span></span>
   * <span data-ttu-id="33dcb-129">Microsoft.ApplicationInsights.Log4NetAppender</span><span class="sxs-lookup"><span data-stu-id="33dcb-129">Microsoft.ApplicationInsights.Log4NetAppender</span></span>

<span data-ttu-id="33dcb-130">package NuGet de Hello installe les assemblys nécessaires hello et modifie également le fichier web.config ou app.config.</span><span class="sxs-lookup"><span data-stu-id="33dcb-130">hello NuGet package installs hello necessary assemblies, and also modifies web.config or app.config.</span></span>

## <a name="insert-diagnostic-log-calls"></a><span data-ttu-id="33dcb-131">Insertion d'appels de journaux de diagnostic</span><span class="sxs-lookup"><span data-stu-id="33dcb-131">Insert diagnostic log calls</span></span>
<span data-ttu-id="33dcb-132">Si vous utilisez System.Diagnostics.Trace, un appel standard serait :</span><span class="sxs-lookup"><span data-stu-id="33dcb-132">If you use System.Diagnostics.Trace, a typical call would be:</span></span>

    System.Diagnostics.Trace.TraceWarning("Slow response - database01");

<span data-ttu-id="33dcb-133">Si vous préférez log4net ou NLog :</span><span class="sxs-lookup"><span data-stu-id="33dcb-133">If you prefer log4net or NLog:</span></span>

    logger.Warn("Slow response - database01");

## <a name="using-eventsource-events"></a><span data-ttu-id="33dcb-134">Utilisation des événements EventSource</span><span class="sxs-lookup"><span data-stu-id="33dcb-134">Using EventSource events</span></span>
<span data-ttu-id="33dcb-135">Vous pouvez configurer [System.Diagnostics.Tracing.EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) événements toobe envoyé tooApplication Insights en tant que les traces.</span><span class="sxs-lookup"><span data-stu-id="33dcb-135">You can configure [System.Diagnostics.Tracing.EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) events toobe sent tooApplication Insights as traces.</span></span> <span data-ttu-id="33dcb-136">Pour commencer, installez hello `Microsoft.ApplicationInsights.EventSourceListener` package NuGet.</span><span class="sxs-lookup"><span data-stu-id="33dcb-136">First, install hello `Microsoft.ApplicationInsights.EventSourceListener` NuGet package.</span></span> <span data-ttu-id="33dcb-137">Puis modifiez `TelemetryModules` section Hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) fichier.</span><span class="sxs-lookup"><span data-stu-id="33dcb-137">Then edit `TelemetryModules` section of hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule, Microsoft.ApplicationInsights.EventSourceListener">
      <Sources>
        <Add Name="MyCompany" Level="Verbose" />
      </Sources>
    </Add>
```

<span data-ttu-id="33dcb-138">Pour chaque source, vous pouvez définir hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="33dcb-138">For each source, you can set hello following parameters:</span></span>
 * <span data-ttu-id="33dcb-139">`Name`Spécifie le nom hello de hello EventSource toocollect.</span><span class="sxs-lookup"><span data-stu-id="33dcb-139">`Name` specifies hello name of hello EventSource toocollect.</span></span>
 * <span data-ttu-id="33dcb-140">`Level`Spécifie les hello toocollect au niveau de journalisation.</span><span class="sxs-lookup"><span data-stu-id="33dcb-140">`Level` specifies hello logging level toocollect.</span></span> <span data-ttu-id="33dcb-141">Peut être `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span><span class="sxs-lookup"><span data-stu-id="33dcb-141">Can be one of `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span></span>
 * <span data-ttu-id="33dcb-142">`Keywords`(Facultatif) spécifie la valeur entière hello toouse de combinaisons de mots clés.</span><span class="sxs-lookup"><span data-stu-id="33dcb-142">`Keywords` (Optional) specifies hello integer value of keywords combinations toouse.</span></span>

## <a name="using-diagnosticsource-events"></a><span data-ttu-id="33dcb-143">Utilisation des événements DiagnosticSource</span><span class="sxs-lookup"><span data-stu-id="33dcb-143">Using DiagnosticSource events</span></span>
<span data-ttu-id="33dcb-144">Vous pouvez configurer [System.Diagnostics.DiagnosticSource](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md) événements toobe envoyé tooApplication Insights en tant que les traces.</span><span class="sxs-lookup"><span data-stu-id="33dcb-144">You can configure [System.Diagnostics.DiagnosticSource](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md) events toobe sent tooApplication Insights as traces.</span></span> <span data-ttu-id="33dcb-145">Pour commencer, installez hello [ `Microsoft.ApplicationInsights.DiagnosticSourceListener` ](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DiagnosticSourceListener) package NuGet.</span><span class="sxs-lookup"><span data-stu-id="33dcb-145">First, install hello [`Microsoft.ApplicationInsights.DiagnosticSourceListener`](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DiagnosticSourceListener) NuGet package.</span></span> <span data-ttu-id="33dcb-146">Puis modifiez hello `TelemetryModules` section Hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) fichier.</span><span class="sxs-lookup"><span data-stu-id="33dcb-146">Then edit hello `TelemetryModules` section of hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.DiagnsoticSourceListener.DiagnosticSourceTelemetryModule, Microsoft.ApplicationInsights.DiagnosticSourceListener">
      <Sources>
        <Add Name="MyDiagnosticSourceName" />
      </Sources>
    </Add>
```

<span data-ttu-id="33dcb-147">Pour chaque DiagnosticSource vous souhaitez tootrace, ajoutez une entrée avec hello `Name` attribut nommez toohello votre DiagnosticSource.</span><span class="sxs-lookup"><span data-stu-id="33dcb-147">For each DiagnosticSource you want tootrace, add an entry with hello `Name` attribute  set toohello name of your DiagnosticSource.</span></span>

## <a name="using-etw-events"></a><span data-ttu-id="33dcb-148">Utilisation des événements ETW</span><span class="sxs-lookup"><span data-stu-id="33dcb-148">Using ETW events</span></span>
<span data-ttu-id="33dcb-149">Vous pouvez configurer toobe d’événements ETW envoyé tooApplication Insights en tant que les traces.</span><span class="sxs-lookup"><span data-stu-id="33dcb-149">You can configure ETW events toobe sent tooApplication Insights as traces.</span></span> <span data-ttu-id="33dcb-150">Pour commencer, installez hello `Microsoft.ApplicationInsights.EtwCollector` package NuGet.</span><span class="sxs-lookup"><span data-stu-id="33dcb-150">First, install hello `Microsoft.ApplicationInsights.EtwCollector` NuGet package.</span></span> <span data-ttu-id="33dcb-151">Puis modifiez `TelemetryModules` section Hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) fichier.</span><span class="sxs-lookup"><span data-stu-id="33dcb-151">Then edit `TelemetryModules` section of hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

> [!NOTE] 
> <span data-ttu-id="33dcb-152">Événements ETW peuvent uniquement être collectés si hello hébergement du processus hello SDK s’exécute sous une identité qui est un membre de « Utilisateurs du journal de performances » ou les administrateurs.</span><span class="sxs-lookup"><span data-stu-id="33dcb-152">ETW events can only be collected if hello process hosting hello SDK is running under an identity that is a member of "Performance Log Users" or Administrators.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule, Microsoft.ApplicationInsights.EtwCollector">
      <Sources>
        <Add ProviderName="MyCompanyEventSourceName" Level="Verbose" />
      </Sources>
    </Add>
```

<span data-ttu-id="33dcb-153">Pour chaque source, vous pouvez définir hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="33dcb-153">For each source, you can set hello following parameters:</span></span>
 * <span data-ttu-id="33dcb-154">`ProviderName`désigne hello toocollect de fournisseur ETW hello.</span><span class="sxs-lookup"><span data-stu-id="33dcb-154">`ProviderName` is hello name of hello ETW provider toocollect.</span></span>
 * <span data-ttu-id="33dcb-155">`ProviderGuid`Spécifie les hello GUID de hello toocollect de fournisseur ETW, peut être utilisé à la place de `ProviderName`.</span><span class="sxs-lookup"><span data-stu-id="33dcb-155">`ProviderGuid` specifies hello GUID of hello ETW provider toocollect, can be used instead of `ProviderName`.</span></span>
 * <span data-ttu-id="33dcb-156">`Level`définit hello toocollect au niveau de journalisation.</span><span class="sxs-lookup"><span data-stu-id="33dcb-156">`Level` sets hello logging level toocollect.</span></span> <span data-ttu-id="33dcb-157">Peut être `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span><span class="sxs-lookup"><span data-stu-id="33dcb-157">Can be one of `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span></span>
 * <span data-ttu-id="33dcb-158">`Keywords`(Facultatif) définit hello entier toouse de combinaisons de mot clé.</span><span class="sxs-lookup"><span data-stu-id="33dcb-158">`Keywords` (Optional) sets hello integer value of keyword combinations toouse.</span></span>

## <a name="using-hello-trace-api-directly"></a><span data-ttu-id="33dcb-159">À l’aide de hello Trace API directement</span><span class="sxs-lookup"><span data-stu-id="33dcb-159">Using hello Trace API directly</span></span>
<span data-ttu-id="33dcb-160">Vous pouvez appeler directement les API de suivi d’Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="33dcb-160">You can call hello Application Insights trace API directly.</span></span> <span data-ttu-id="33dcb-161">adaptateurs de journalisation Hello utilisent cette API.</span><span class="sxs-lookup"><span data-stu-id="33dcb-161">hello logging adapters use this API.</span></span>

<span data-ttu-id="33dcb-162">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="33dcb-162">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow response - database01");

<span data-ttu-id="33dcb-163">L’avantage de TrackTrace est que vous pouvez placer des données relativement longues dans le message de type hello.</span><span class="sxs-lookup"><span data-stu-id="33dcb-163">An advantage of TrackTrace is that you can put relatively long data in hello message.</span></span> <span data-ttu-id="33dcb-164">Par exemple, vous pourriez y encoder des données POST.</span><span class="sxs-lookup"><span data-stu-id="33dcb-164">For example, you could encode POST data there.</span></span>

<span data-ttu-id="33dcb-165">En outre, vous pouvez ajouter un message tooyour au niveau de gravité.</span><span class="sxs-lookup"><span data-stu-id="33dcb-165">In addition, you can add a severity level tooyour message.</span></span> <span data-ttu-id="33dcb-166">Et, comme les autres données de télémétrie, vous pouvez ajouter des valeurs de propriété que vous pouvez utiliser le filtre de toohelp ou de recherche pour différents ensembles de traces.</span><span class="sxs-lookup"><span data-stu-id="33dcb-166">And, like other telemetry, you can add property values that you can use toohelp filter or search for different sets of traces.</span></span> <span data-ttu-id="33dcb-167">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="33dcb-167">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

<span data-ttu-id="33dcb-168">Cela vous permettrait, dans [recherche][diagnostic], filtre tooeasily tous les messages hello d’un niveau de gravité spécifique concernant tooa la base de données particulière.</span><span class="sxs-lookup"><span data-stu-id="33dcb-168">This would enable you, in [Search][diagnostic], tooeasily filter out all hello messages of a particular severity level relating tooa particular database.</span></span>

## <a name="explore-your-logs"></a><span data-ttu-id="33dcb-169">Exploration de vos journaux</span><span class="sxs-lookup"><span data-stu-id="33dcb-169">Explore your logs</span></span>
<span data-ttu-id="33dcb-170">Exécutez votre application en mode débogage ou déployez-la en direct.</span><span class="sxs-lookup"><span data-stu-id="33dcb-170">Run your app, either in debug mode or deploy it live.</span></span>

<span data-ttu-id="33dcb-171">Dans le panneau de vue d’ensemble de votre application dans [portail Application Insights de hello][portal], choisissez [recherche][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="33dcb-171">In your app's overview blade in [hello Application Insights portal][portal], choose [Search][diagnostic].</span></span>

![Dans Application Insights, cliquez sur Recherche.](./media/app-insights-asp-net-trace-logs/020-diagnostic-search.png)

![Recherche](./media/app-insights-asp-net-trace-logs/10-diagnostics.png)

<span data-ttu-id="33dcb-174">Vous pouvez par exemple :</span><span class="sxs-lookup"><span data-stu-id="33dcb-174">You can, for example:</span></span>

* <span data-ttu-id="33dcb-175">Filtrer selon les traces de journal ou les éléments avec des propriétés spécifiques</span><span class="sxs-lookup"><span data-stu-id="33dcb-175">Filter on log traces, or on items with specific properties</span></span>
* <span data-ttu-id="33dcb-176">Inspecter un élément spécifique en détail</span><span class="sxs-lookup"><span data-stu-id="33dcb-176">Inspect a specific item in detail.</span></span>
* <span data-ttu-id="33dcb-177">Rechercher d’autres données de télémétrie relatives toohello même demande de l’utilisateur (autrement dit, avec hello même OperationId)</span><span class="sxs-lookup"><span data-stu-id="33dcb-177">Find other telemetry relating toohello same user request (that is, with hello same OperationId)</span></span>
* <span data-ttu-id="33dcb-178">Enregistrer la configuration de hello de cette page en tant que favori</span><span class="sxs-lookup"><span data-stu-id="33dcb-178">Save hello configuration of this page as a Favorite</span></span>

> [!NOTE]
> <span data-ttu-id="33dcb-179">**Échantillonnage.**</span><span class="sxs-lookup"><span data-stu-id="33dcb-179">**Sampling.**</span></span> <span data-ttu-id="33dcb-180">Si votre application envoie une grande quantité de données et que vous utilisez hello Application Insights SDK pour ASP.NET version 2.0.0-beta3 ou version ultérieure, fonctionnalité d’adaptative d’échantillonnage de hello peut fonctionner et envoyer seulement un pourcentage de votre télémétrie.</span><span class="sxs-lookup"><span data-stu-id="33dcb-180">If your application sends a lot of data and you are using hello Application Insights SDK for ASP.NET version 2.0.0-beta3 or later, hello adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> [<span data-ttu-id="33dcb-181">En savoir plus sur l’échantillonnage.</span><span class="sxs-lookup"><span data-stu-id="33dcb-181">Learn more about sampling.</span></span>](app-insights-sampling.md)
>
>

## <a name="next-steps"></a><span data-ttu-id="33dcb-182">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="33dcb-182">Next steps</span></span>
<span data-ttu-id="33dcb-183">[Diagnostiquer les défaillances et les exceptions dans ASP.NET][exceptions]</span><span class="sxs-lookup"><span data-stu-id="33dcb-183">[Diagnose failures and exceptions in ASP.NET][exceptions]</span></span>

<span data-ttu-id="33dcb-184">[En savoir plus sur Recherche][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="33dcb-184">[Learn more about Search][diagnostic].</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="33dcb-185">résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="33dcb-185">Troubleshooting</span></span>
### <a name="how-do-i-do-this-for-java"></a><span data-ttu-id="33dcb-186">Comment faire pour Java ?</span><span class="sxs-lookup"><span data-stu-id="33dcb-186">How do I do this for Java?</span></span>
<span data-ttu-id="33dcb-187">Hello d’utilisation [cartes de journal Java](app-insights-java-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="33dcb-187">Use hello [Java log adapters](app-insights-java-trace-logs.md).</span></span>

### <a name="theres-no-application-insights-option-on-hello-project-context-menu"></a><span data-ttu-id="33dcb-188">Il n’existe aucune option d’Application Insights sur le menu contextuel du projet hello</span><span class="sxs-lookup"><span data-stu-id="33dcb-188">There's no Application Insights option on hello project context menu</span></span>
* <span data-ttu-id="33dcb-189">Vérifiez que les outils Application Insights sont installés sur cet ordinateur de développement.</span><span class="sxs-lookup"><span data-stu-id="33dcb-189">Check Application Insights tools is installed on this development machine.</span></span> <span data-ttu-id="33dcb-190">Dans le menu Outils, Extensions et mises à jour de Visual Studio, recherchez les outils Application Insights.</span><span class="sxs-lookup"><span data-stu-id="33dcb-190">In Visual Studio menu Tools, Extensions and Updates, look for Application Insights Tools.</span></span> <span data-ttu-id="33dcb-191">Si elle n’est pas dans l’onglet de hello installé, ouvrez hello en ligne onglet et installez-le.</span><span class="sxs-lookup"><span data-stu-id="33dcb-191">If it isn't in hello Installed tab, open hello Online tab and install it.</span></span>
* <span data-ttu-id="33dcb-192">Il peut s’agir d’un type de projet non pris en charge par les outils Application Insights.</span><span class="sxs-lookup"><span data-stu-id="33dcb-192">This might be a type of project not supported by Application Insights tools.</span></span> <span data-ttu-id="33dcb-193">Utilisez [l’installation manuelle](#manual-installation).</span><span class="sxs-lookup"><span data-stu-id="33dcb-193">Use [manual installation](#manual-installation).</span></span>

### <a name="no-log-adapter-option-in-hello-configuration-tool"></a><span data-ttu-id="33dcb-194">Aucune option de carte de journal dans l’outil de configuration hello</span><span class="sxs-lookup"><span data-stu-id="33dcb-194">No log adapter option in hello configuration tool</span></span>
* <span data-ttu-id="33dcb-195">Vous devez tout d’abord tooinstall hello journalisation.</span><span class="sxs-lookup"><span data-stu-id="33dcb-195">You need tooinstall hello logging framework first.</span></span>
* <span data-ttu-id="33dcb-196">Si vous utilisez System.Diagnostics.Trace, assurez-vous que vous l’avez [configuré dans `web.config`](https://msdn.microsoft.com/library/system.diagnostics.eventlogtracelistener.aspx).</span><span class="sxs-lookup"><span data-stu-id="33dcb-196">If you're using System.Diagnostics.Trace, make sure you [configured it in `web.config`](https://msdn.microsoft.com/library/system.diagnostics.eventlogtracelistener.aspx).</span></span>
* <span data-ttu-id="33dcb-197">Avez-vous hello dernière version d’Application Insights ?</span><span class="sxs-lookup"><span data-stu-id="33dcb-197">Have you got hello latest version of Application Insights?</span></span> <span data-ttu-id="33dcb-198">Dans Visual Studio **outils** menu, choisissez **Extensions et mises à jour**et ouvrez hello **mises à jour** onglet. Si les outils de développement Analytique n’y figure, cliquez sur tooupdate il.</span><span class="sxs-lookup"><span data-stu-id="33dcb-198">In Visual Studio **Tools** menu, choose **Extensions and Updates**, and open hello **Updates** tab. If Developer Analytics tools is there, click tooupdate it.</span></span>

### <span data-ttu-id="33dcb-199"><a name="emptykey"></a>J’obtiens une erreur « La clé d’instrumentation ne peut pas être vide ».</span><span class="sxs-lookup"><span data-stu-id="33dcb-199"><a name="emptykey"></a>I get an error "Instrumentation key cannot be empty"</span></span>
<span data-ttu-id="33dcb-200">Il semble que vous avez installé hello journalisation de package Nuget de la carte sans installer Application Insights.</span><span class="sxs-lookup"><span data-stu-id="33dcb-200">Looks like you installed hello logging adapter Nuget package without installing Application Insights.</span></span>

<span data-ttu-id="33dcb-201">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur `ApplicationInsights.config` , puis sélectionnez **Mettre à jour Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="33dcb-201">In Solution Explorer, right-click `ApplicationInsights.config` and choose **Update Application Insights**.</span></span> <span data-ttu-id="33dcb-202">Vous obtenez une boîte de dialogue qui vous invite toosign dans tooAzure et créez une ressource Application Insights, ou réutiliser un existant.</span><span class="sxs-lookup"><span data-stu-id="33dcb-202">You'll get a dialog that invites you toosign in tooAzure and either create an Application Insights resource, or re-use an existing one.</span></span> <span data-ttu-id="33dcb-203">Ceci devrait résoudre le problème.</span><span class="sxs-lookup"><span data-stu-id="33dcb-203">That should fix it.</span></span>

### <a name="i-can-see-traces-in-diagnostic-search-but-not-hello-other-events"></a><span data-ttu-id="33dcb-204">Je peux voir les traces dans la recherche de diagnostic, mais pas hello autres événements</span><span class="sxs-lookup"><span data-stu-id="33dcb-204">I can see traces in diagnostic search, but not hello other events</span></span>
<span data-ttu-id="33dcb-205">Il peut parfois prendre un certain temps pour tous les tooget d’événements et les demandes de hello via le pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="33dcb-205">It can sometimes take a while for all hello events and requests tooget through hello pipeline.</span></span>

### <span data-ttu-id="33dcb-206"><a name="limits"></a>Quelle est la quantité de données conservée ?</span><span class="sxs-lookup"><span data-stu-id="33dcb-206"><a name="limits"></a>How much data is retained?</span></span>
<span data-ttu-id="33dcb-207">Plusieurs critères influent sur la quantité de hello de conservation des données.</span><span class="sxs-lookup"><span data-stu-id="33dcb-207">Several factors impact hello amount of data retained.</span></span> <span data-ttu-id="33dcb-208">Consultez hello [limites](app-insights-api-custom-events-metrics.md#limits) section de page de métriques hello client événements pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="33dcb-208">See hello [limits](app-insights-api-custom-events-metrics.md#limits) section of hello customer event metrics page for more information.</span></span> 

### <a name="im-not-seeing-some-of-hello-log-entries-that-i-expect"></a><span data-ttu-id="33dcb-209">Je ne vois pas d’entrées de journal hello attendus</span><span class="sxs-lookup"><span data-stu-id="33dcb-209">I'm not seeing some of hello log entries that I expect</span></span>
<span data-ttu-id="33dcb-210">Si votre application envoie une grande quantité de données et que vous utilisez hello Application Insights SDK pour ASP.NET version 2.0.0-beta3 ou version ultérieure, fonctionnalité d’adaptative d’échantillonnage de hello peut fonctionner et envoyer seulement un pourcentage de votre télémétrie.</span><span class="sxs-lookup"><span data-stu-id="33dcb-210">If your application sends a lot of data and you are using hello Application Insights SDK for ASP.NET version 2.0.0-beta3 or later, hello adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> [<span data-ttu-id="33dcb-211">En savoir plus sur l’échantillonnage.</span><span class="sxs-lookup"><span data-stu-id="33dcb-211">Learn more about sampling.</span></span>](app-insights-sampling.md)

## <span data-ttu-id="33dcb-212"><a name="add"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="33dcb-212"><a name="add"></a>Next steps</span></span>
* <span data-ttu-id="33dcb-213">[Configuration des tests de disponibilité et de réactivité][availability]</span><span class="sxs-lookup"><span data-stu-id="33dcb-213">[Set up availability and responsiveness tests][availability]</span></span>
* <span data-ttu-id="33dcb-214">[Résolution des problèmes][qna]</span><span class="sxs-lookup"><span data-stu-id="33dcb-214">[Troubleshooting][qna]</span></span>

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[portal]: https://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[start]: app-insights-overview.md
