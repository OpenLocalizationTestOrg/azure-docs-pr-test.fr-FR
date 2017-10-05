---
title: Exploration des journaux .NET dans Application Insights
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
ms.openlocfilehash: 68e03bf10167ecde675d62782de7063aea9e81d9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="explore-net-trace-logs-in-application-insights"></a><span data-ttu-id="1a77e-103">Exploration des journaux .NET dans Application Insights</span><span class="sxs-lookup"><span data-stu-id="1a77e-103">Explore .NET trace logs in Application Insights</span></span>
<span data-ttu-id="1a77e-104">Si vous utilisez NLog, log4Net ou System.Diagnostics.Trace pour le suivi de diagnostic dans votre application ASP.NET, les journaux peuvent être envoyés à [Azure Application Insights][start], où vous pouvez les explorer et les rechercher.</span><span class="sxs-lookup"><span data-stu-id="1a77e-104">If you use NLog, log4Net or System.Diagnostics.Trace for diagnostic tracing in your ASP.NET application, you can have your logs sent to [Azure Application Insights][start], where you can explore and search them.</span></span> <span data-ttu-id="1a77e-105">Les journaux sont fusionnés avec la télémétrie provenant de votre application, afin que vous puissiez identifier les traces associées au traitement des demandes de l’utilisateur et les mettre en corrélation avec d’autres événements et des rapports d’exception.</span><span class="sxs-lookup"><span data-stu-id="1a77e-105">Your logs will be merged with the other telemetry coming from your application, so that you can identify the traces associated with servicing each user request, and correlate them with other events and exception reports.</span></span>

> [!NOTE]
> <span data-ttu-id="1a77e-106">Avez-vous besoin du module de collecte de journaux ?</span><span class="sxs-lookup"><span data-stu-id="1a77e-106">Do you need the log capture module?</span></span> <span data-ttu-id="1a77e-107">Il s’agit d’un adaptateur très utile pour les enregistreurs d’événements tiers. Cependant, si vous n’utilisez pas déjà NLog, log4Net ou System.Diagnostics.Trace, vous pouvez appeler [Application Insights TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) directement.</span><span class="sxs-lookup"><span data-stu-id="1a77e-107">It's a useful adapter for 3rd-party loggers, but if you aren't already using NLog, log4Net or System.Diagnostics.Trace, consider just calling [Application Insights TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) directly.</span></span>
>
>

## <a name="install-logging-on-your-app"></a><span data-ttu-id="1a77e-108">Installation de la journalisation sur votre application</span><span class="sxs-lookup"><span data-stu-id="1a77e-108">Install logging on your app</span></span>
<span data-ttu-id="1a77e-109">Installez votre infrastructure de journalisation choisie dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="1a77e-109">Install your chosen logging framework in your project.</span></span> <span data-ttu-id="1a77e-110">Ceci devrait générer une entrée dans le fichier app.config ou web.config.</span><span class="sxs-lookup"><span data-stu-id="1a77e-110">This should result in an entry in app.config or web.config.</span></span>

<span data-ttu-id="1a77e-111">Vous devez ajouter une entrée au fichier web.config si vous utilisez System.Diagnostics.Trace.</span><span class="sxs-lookup"><span data-stu-id="1a77e-111">If you're using System.Diagnostics.Trace, you need to add an entry to web.config:</span></span>

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
## <a name="configure-application-insights-to-collect-logs"></a><span data-ttu-id="1a77e-112">Configuration d’Application Insights pour la collecte des journaux</span><span class="sxs-lookup"><span data-stu-id="1a77e-112">Configure Application Insights to collect logs</span></span>
<span data-ttu-id="1a77e-113">Si vous ne l’avez pas encore fait, **[ajoutez Application Insights à votre projet](app-insights-asp-net.md)**.</span><span class="sxs-lookup"><span data-stu-id="1a77e-113">**[Add Application Insights to your project](app-insights-asp-net.md)** if you haven't done that yet.</span></span> <span data-ttu-id="1a77e-114">Une option permettant d’inclure le collecteur de journaux doit s’afficher.</span><span class="sxs-lookup"><span data-stu-id="1a77e-114">You'll see an option to include the log collector.</span></span>

<span data-ttu-id="1a77e-115">Ou **configurez Application Insights** en cliquant avec le bouton droit dans l’Explorateur de solutions.</span><span class="sxs-lookup"><span data-stu-id="1a77e-115">Or **Configure Application Insights** by right-clicking your project in Solution Explorer.</span></span> <span data-ttu-id="1a77e-116">Sélectionnez l’option **Configurer la collecte des traces**.</span><span class="sxs-lookup"><span data-stu-id="1a77e-116">Select the option to **Configure trace collection**.</span></span>

<span data-ttu-id="1a77e-117">*Menu Application Insights non disponible ou aucune option pour le collecteur de journaux ?*</span><span class="sxs-lookup"><span data-stu-id="1a77e-117">*No Application Insights menu or log collector option?*</span></span> <span data-ttu-id="1a77e-118">Consultez la [Résolution des problèmes](#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="1a77e-118">Try [Troubleshooting](#troubleshooting).</span></span>

## <a name="manual-installation"></a><span data-ttu-id="1a77e-119">Installation manuelle</span><span class="sxs-lookup"><span data-stu-id="1a77e-119">Manual installation</span></span>
<span data-ttu-id="1a77e-120">Utilisez cette méthode si votre type de projet n’est pas pris en charge par le programme d’installation Application Insights (par exemple, un projet de bureau Windows).</span><span class="sxs-lookup"><span data-stu-id="1a77e-120">Use this method if your project type isn't supported by the Application Insights installer (for example a Windows desktop project).</span></span>

1. <span data-ttu-id="1a77e-121">Si vous prévoyez d'utiliser log4Net ou NLog, installez-le dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="1a77e-121">If you plan to use log4Net or NLog, install it in your project.</span></span>
2. <span data-ttu-id="1a77e-122">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur le projet, puis sélectionnez **Gérer les packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="1a77e-122">In Solution Explorer, right-click your project and choose **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="1a77e-123">Recherchez « Application Insights »</span><span class="sxs-lookup"><span data-stu-id="1a77e-123">Search for "Application Insights"</span></span>
4. <span data-ttu-id="1a77e-124">Sélectionnez le package approprié parmi :</span><span class="sxs-lookup"><span data-stu-id="1a77e-124">Select the appropriate package - one of:</span></span>

   * <span data-ttu-id="1a77e-125">Microsoft.ApplicationInsights.TraceListener (pour capturer les appels System.Diagnostics.Trace)</span><span class="sxs-lookup"><span data-stu-id="1a77e-125">Microsoft.ApplicationInsights.TraceListener (to capture System.Diagnostics.Trace calls)</span></span>
   * <span data-ttu-id="1a77e-126">Microsoft.ApplicationInsights.EventSourceListener (pour capturer les événements EventSource)</span><span class="sxs-lookup"><span data-stu-id="1a77e-126">Microsoft.ApplicationInsights.EventSourceListener (to capture EventSource events)</span></span>
   * <span data-ttu-id="1a77e-127">Microsoft.ApplicationInsights.EtwListener (pour capturer les événements ETW)</span><span class="sxs-lookup"><span data-stu-id="1a77e-127">Microsoft.ApplicationInsights.EtwListener (to capture ETW events)</span></span>
   * <span data-ttu-id="1a77e-128">Microsoft.ApplicationInsights.NLogTarget</span><span class="sxs-lookup"><span data-stu-id="1a77e-128">Microsoft.ApplicationInsights.NLogTarget</span></span>
   * <span data-ttu-id="1a77e-129">Microsoft.ApplicationInsights.Log4NetAppender</span><span class="sxs-lookup"><span data-stu-id="1a77e-129">Microsoft.ApplicationInsights.Log4NetAppender</span></span>

<span data-ttu-id="1a77e-130">Le package NuGet installe les assemblys nécessaires et modifie également le fichier web.config ou app.config.</span><span class="sxs-lookup"><span data-stu-id="1a77e-130">The NuGet package installs the necessary assemblies, and also modifies web.config or app.config.</span></span>

## <a name="insert-diagnostic-log-calls"></a><span data-ttu-id="1a77e-131">Insertion d'appels de journaux de diagnostic</span><span class="sxs-lookup"><span data-stu-id="1a77e-131">Insert diagnostic log calls</span></span>
<span data-ttu-id="1a77e-132">Si vous utilisez System.Diagnostics.Trace, un appel standard serait :</span><span class="sxs-lookup"><span data-stu-id="1a77e-132">If you use System.Diagnostics.Trace, a typical call would be:</span></span>

    System.Diagnostics.Trace.TraceWarning("Slow response - database01");

<span data-ttu-id="1a77e-133">Si vous préférez log4net ou NLog :</span><span class="sxs-lookup"><span data-stu-id="1a77e-133">If you prefer log4net or NLog:</span></span>

    logger.Warn("Slow response - database01");

## <a name="using-eventsource-events"></a><span data-ttu-id="1a77e-134">Utilisation des événements EventSource</span><span class="sxs-lookup"><span data-stu-id="1a77e-134">Using EventSource events</span></span>
<span data-ttu-id="1a77e-135">Vous pouvez configurer les événements [System.Diagnostics.Tracing.EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) à envoyer à Application Insights en tant que traces.</span><span class="sxs-lookup"><span data-stu-id="1a77e-135">You can configure [System.Diagnostics.Tracing.EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) events to be sent to Application Insights as traces.</span></span> <span data-ttu-id="1a77e-136">D’abord, installez le package NuGet `Microsoft.ApplicationInsights.EventSourceListener`.</span><span class="sxs-lookup"><span data-stu-id="1a77e-136">First, install the `Microsoft.ApplicationInsights.EventSourceListener` NuGet package.</span></span> <span data-ttu-id="1a77e-137">Ensuite, modifiez la section `TelemetryModules` du fichier [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md).</span><span class="sxs-lookup"><span data-stu-id="1a77e-137">Then edit `TelemetryModules` section of the [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule, Microsoft.ApplicationInsights.EventSourceListener">
      <Sources>
        <Add Name="MyCompany" Level="Verbose" />
      </Sources>
    </Add>
```

<span data-ttu-id="1a77e-138">Pour chaque source, vous pouvez définir les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="1a77e-138">For each source, you can set the following parameters:</span></span>
 * <span data-ttu-id="1a77e-139">`Name` spécifie le nom de l’événement EventSource à collecter.</span><span class="sxs-lookup"><span data-stu-id="1a77e-139">`Name` specifies the name of the EventSource to collect.</span></span>
 * <span data-ttu-id="1a77e-140">`Level` spécifie le niveau de journalisation à collecter.</span><span class="sxs-lookup"><span data-stu-id="1a77e-140">`Level` specifies the logging level to collect.</span></span> <span data-ttu-id="1a77e-141">Peut être `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span><span class="sxs-lookup"><span data-stu-id="1a77e-141">Can be one of `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span></span>
 * <span data-ttu-id="1a77e-142">`Keywords` (Facultatif) spécifie la valeur entière de combinaisons de mots clés à utiliser.</span><span class="sxs-lookup"><span data-stu-id="1a77e-142">`Keywords` (Optional) specifies the integer value of keywords combinations to use.</span></span>

## <a name="using-diagnosticsource-events"></a><span data-ttu-id="1a77e-143">Utilisation des événements DiagnosticSource</span><span class="sxs-lookup"><span data-stu-id="1a77e-143">Using DiagnosticSource events</span></span>
<span data-ttu-id="1a77e-144">Vous pouvez configurer les événements [System.Diagnostics.Tracing.EventSource](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md) de façon à les envoyer à Application Insights en tant que traces.</span><span class="sxs-lookup"><span data-stu-id="1a77e-144">You can configure [System.Diagnostics.DiagnosticSource](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md) events to be sent to Application Insights as traces.</span></span> <span data-ttu-id="1a77e-145">Commencez par installer le package NuGet [`Microsoft.ApplicationInsights.DiagnosticSourceListener`](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DiagnosticSourceListener).</span><span class="sxs-lookup"><span data-stu-id="1a77e-145">First, install the [`Microsoft.ApplicationInsights.DiagnosticSourceListener`](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DiagnosticSourceListener) NuGet package.</span></span> <span data-ttu-id="1a77e-146">Ensuite, modifiez la section `TelemetryModules` du fichier [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md).</span><span class="sxs-lookup"><span data-stu-id="1a77e-146">Then edit the `TelemetryModules` section of the [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.DiagnsoticSourceListener.DiagnosticSourceTelemetryModule, Microsoft.ApplicationInsights.DiagnosticSourceListener">
      <Sources>
        <Add Name="MyDiagnosticSourceName" />
      </Sources>
    </Add>
```

<span data-ttu-id="1a77e-147">Pour chaque DiagnosticSource à tracer, ajoutez une entrée avec l’attribut `Name` défini sur le nom de votre DiagnosticSource.</span><span class="sxs-lookup"><span data-stu-id="1a77e-147">For each DiagnosticSource you want to trace, add an entry with the `Name` attribute  set to the name of your DiagnosticSource.</span></span>

## <a name="using-etw-events"></a><span data-ttu-id="1a77e-148">Utilisation des événements ETW</span><span class="sxs-lookup"><span data-stu-id="1a77e-148">Using ETW events</span></span>
<span data-ttu-id="1a77e-149">Vous pouvez configurer les événements ETW à envoyer à Application Insights en tant que traces.</span><span class="sxs-lookup"><span data-stu-id="1a77e-149">You can configure ETW events to be sent to Application Insights as traces.</span></span> <span data-ttu-id="1a77e-150">D’abord, installez le package NuGet `Microsoft.ApplicationInsights.EtwCollector`.</span><span class="sxs-lookup"><span data-stu-id="1a77e-150">First, install the `Microsoft.ApplicationInsights.EtwCollector` NuGet package.</span></span> <span data-ttu-id="1a77e-151">Ensuite, modifiez la section `TelemetryModules` du fichier [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md).</span><span class="sxs-lookup"><span data-stu-id="1a77e-151">Then edit `TelemetryModules` section of the [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

> [!NOTE] 
> <span data-ttu-id="1a77e-152">Les événements ETW peuvent uniquement être collectés si le processus hébergeant le Kit de développement logiciel (SDK) s’exécute sous une identité qui membre des « Utilisateurs du journal de performances » ou des administrateurs.</span><span class="sxs-lookup"><span data-stu-id="1a77e-152">ETW events can only be collected if the process hosting the SDK is running under an identity that is a member of "Performance Log Users" or Administrators.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule, Microsoft.ApplicationInsights.EtwCollector">
      <Sources>
        <Add ProviderName="MyCompanyEventSourceName" Level="Verbose" />
      </Sources>
    </Add>
```

<span data-ttu-id="1a77e-153">Pour chaque source, vous pouvez définir les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="1a77e-153">For each source, you can set the following parameters:</span></span>
 * <span data-ttu-id="1a77e-154">`ProviderName` est le nom du fournisseur ETW à collecter.</span><span class="sxs-lookup"><span data-stu-id="1a77e-154">`ProviderName` is the name of the ETW provider to collect.</span></span>
 * <span data-ttu-id="1a77e-155">`ProviderGuid` spécifie le GUID du fournisseur ETW à collecter, peut être utilisé à la place de `ProviderName`.</span><span class="sxs-lookup"><span data-stu-id="1a77e-155">`ProviderGuid` specifies the GUID of the ETW provider to collect, can be used instead of `ProviderName`.</span></span>
 * <span data-ttu-id="1a77e-156">`Level` définit le niveau de journalisation à collecter.</span><span class="sxs-lookup"><span data-stu-id="1a77e-156">`Level` sets the logging level to collect.</span></span> <span data-ttu-id="1a77e-157">Peut être `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span><span class="sxs-lookup"><span data-stu-id="1a77e-157">Can be one of `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span></span>
 * <span data-ttu-id="1a77e-158">`Keywords` (Facultatif) définit la valeur entière de combinaisons de mots clés à utiliser.</span><span class="sxs-lookup"><span data-stu-id="1a77e-158">`Keywords` (Optional) sets the integer value of keyword combinations to use.</span></span>

## <a name="using-the-trace-api-directly"></a><span data-ttu-id="1a77e-159">Utilisation de l’API de suivi directement</span><span class="sxs-lookup"><span data-stu-id="1a77e-159">Using the Trace API directly</span></span>
<span data-ttu-id="1a77e-160">Vous pouvez appeler directement l’API de suivi d’Application Insights.</span><span class="sxs-lookup"><span data-stu-id="1a77e-160">You can call the Application Insights trace API directly.</span></span> <span data-ttu-id="1a77e-161">Les adaptateurs de journalisation utilisent cette API.</span><span class="sxs-lookup"><span data-stu-id="1a77e-161">The logging adapters use this API.</span></span>

<span data-ttu-id="1a77e-162">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="1a77e-162">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow response - database01");

<span data-ttu-id="1a77e-163">l’un des avantages de TrackTrace est que vous pouvez insérer des données relativement longues dans le message.</span><span class="sxs-lookup"><span data-stu-id="1a77e-163">An advantage of TrackTrace is that you can put relatively long data in the message.</span></span> <span data-ttu-id="1a77e-164">Par exemple, vous pourriez y encoder des données POST.</span><span class="sxs-lookup"><span data-stu-id="1a77e-164">For example, you could encode POST data there.</span></span>

<span data-ttu-id="1a77e-165">Par ailleurs, vous pouvez ajouter un niveau de gravité à votre message.</span><span class="sxs-lookup"><span data-stu-id="1a77e-165">In addition, you can add a severity level to your message.</span></span> <span data-ttu-id="1a77e-166">Comme pour les autres données de télémétrie, vous pouvez également ajouter des valeurs de propriété que vous pouvez utiliser pour filtrer ou rechercher différents jeux de traces.</span><span class="sxs-lookup"><span data-stu-id="1a77e-166">And, like other telemetry, you can add property values that you can use to help filter or search for different sets of traces.</span></span> <span data-ttu-id="1a77e-167">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="1a77e-167">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

<span data-ttu-id="1a77e-168">Cela vous permettrait, dans [Recherche][diagnostic], de filtrer facilement tous les messages d’un niveau de gravité particulier portant sur une certaine base de données.</span><span class="sxs-lookup"><span data-stu-id="1a77e-168">This would enable you, in [Search][diagnostic], to easily filter out all the messages of a particular severity level relating to a particular database.</span></span>

## <a name="explore-your-logs"></a><span data-ttu-id="1a77e-169">Exploration de vos journaux</span><span class="sxs-lookup"><span data-stu-id="1a77e-169">Explore your logs</span></span>
<span data-ttu-id="1a77e-170">Exécutez votre application en mode débogage ou déployez-la en direct.</span><span class="sxs-lookup"><span data-stu-id="1a77e-170">Run your app, either in debug mode or deploy it live.</span></span>

<span data-ttu-id="1a77e-171">Dans le panneau Vue d’ensemble de votre application du [portail Application Insights][portal], choisissez [Rechercher][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="1a77e-171">In your app's overview blade in [the Application Insights portal][portal], choose [Search][diagnostic].</span></span>

![Dans Application Insights, cliquez sur Recherche.](./media/app-insights-asp-net-trace-logs/020-diagnostic-search.png)

![Recherche](./media/app-insights-asp-net-trace-logs/10-diagnostics.png)

<span data-ttu-id="1a77e-174">Vous pouvez par exemple :</span><span class="sxs-lookup"><span data-stu-id="1a77e-174">You can, for example:</span></span>

* <span data-ttu-id="1a77e-175">Filtrer selon les traces de journal ou les éléments avec des propriétés spécifiques</span><span class="sxs-lookup"><span data-stu-id="1a77e-175">Filter on log traces, or on items with specific properties</span></span>
* <span data-ttu-id="1a77e-176">Inspecter un élément spécifique en détail</span><span class="sxs-lookup"><span data-stu-id="1a77e-176">Inspect a specific item in detail.</span></span>
* <span data-ttu-id="1a77e-177">Rechercher d’autres données de télémétrie relatives à la même demande utilisateur (autrement dit, avec la même OperationId)</span><span class="sxs-lookup"><span data-stu-id="1a77e-177">Find other telemetry relating to the same user request (that is, with the same OperationId)</span></span>
* <span data-ttu-id="1a77e-178">Enregistrer la configuration de cette page en tant que favori</span><span class="sxs-lookup"><span data-stu-id="1a77e-178">Save the configuration of this page as a Favorite</span></span>

> [!NOTE]
> <span data-ttu-id="1a77e-179">**Échantillonnage.**</span><span class="sxs-lookup"><span data-stu-id="1a77e-179">**Sampling.**</span></span> <span data-ttu-id="1a77e-180">Si votre application envoie des données en grand nombre et si vous utilisez le Kit de développement logiciel Application Insights pour ASP.NET version 2.0.0-beta3 ou ultérieure, la fonctionnalité d’échantillonnage adaptatif peut fonctionner et transmettre uniquement un pourcentage de vos données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="1a77e-180">If your application sends a lot of data and you are using the Application Insights SDK for ASP.NET version 2.0.0-beta3 or later, the adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> [<span data-ttu-id="1a77e-181">En savoir plus sur l’échantillonnage.</span><span class="sxs-lookup"><span data-stu-id="1a77e-181">Learn more about sampling.</span></span>](app-insights-sampling.md)
>
>

## <a name="next-steps"></a><span data-ttu-id="1a77e-182">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1a77e-182">Next steps</span></span>
<span data-ttu-id="1a77e-183">[Diagnostiquer les défaillances et les exceptions dans ASP.NET][exceptions]</span><span class="sxs-lookup"><span data-stu-id="1a77e-183">[Diagnose failures and exceptions in ASP.NET][exceptions]</span></span>

<span data-ttu-id="1a77e-184">[En savoir plus sur Recherche][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="1a77e-184">[Learn more about Search][diagnostic].</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="1a77e-185">résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="1a77e-185">Troubleshooting</span></span>
### <a name="how-do-i-do-this-for-java"></a><span data-ttu-id="1a77e-186">Comment faire pour Java ?</span><span class="sxs-lookup"><span data-stu-id="1a77e-186">How do I do this for Java?</span></span>
<span data-ttu-id="1a77e-187">Utilisez les [adaptateurs de journaux Java](app-insights-java-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="1a77e-187">Use the [Java log adapters](app-insights-java-trace-logs.md).</span></span>

### <a name="theres-no-application-insights-option-on-the-project-context-menu"></a><span data-ttu-id="1a77e-188">Le menu contextuel du projet ne contient aucune option Application Insights</span><span class="sxs-lookup"><span data-stu-id="1a77e-188">There's no Application Insights option on the project context menu</span></span>
* <span data-ttu-id="1a77e-189">Vérifiez que les outils Application Insights sont installés sur cet ordinateur de développement.</span><span class="sxs-lookup"><span data-stu-id="1a77e-189">Check Application Insights tools is installed on this development machine.</span></span> <span data-ttu-id="1a77e-190">Dans le menu Outils, Extensions et mises à jour de Visual Studio, recherchez les outils Application Insights.</span><span class="sxs-lookup"><span data-stu-id="1a77e-190">In Visual Studio menu Tools, Extensions and Updates, look for Application Insights Tools.</span></span> <span data-ttu-id="1a77e-191">S’ils ne sont pas dans l’onglet Installé, ouvrez l’onglet En ligne et installez-les.</span><span class="sxs-lookup"><span data-stu-id="1a77e-191">If it isn't in the Installed tab, open the Online tab and install it.</span></span>
* <span data-ttu-id="1a77e-192">Il peut s’agir d’un type de projet non pris en charge par les outils Application Insights.</span><span class="sxs-lookup"><span data-stu-id="1a77e-192">This might be a type of project not supported by Application Insights tools.</span></span> <span data-ttu-id="1a77e-193">Utilisez [l’installation manuelle](#manual-installation).</span><span class="sxs-lookup"><span data-stu-id="1a77e-193">Use [manual installation](#manual-installation).</span></span>

### <a name="no-log-adapter-option-in-the-configuration-tool"></a><span data-ttu-id="1a77e-194">Aucune option d’adaptateur dans l’outil de configuration</span><span class="sxs-lookup"><span data-stu-id="1a77e-194">No log adapter option in the configuration tool</span></span>
* <span data-ttu-id="1a77e-195">Vous devez d’abord installer l’infrastructure de journalisation.</span><span class="sxs-lookup"><span data-stu-id="1a77e-195">You need to install the logging framework first.</span></span>
* <span data-ttu-id="1a77e-196">Si vous utilisez System.Diagnostics.Trace, assurez-vous que vous l’avez [configuré dans `web.config`](https://msdn.microsoft.com/library/system.diagnostics.eventlogtracelistener.aspx).</span><span class="sxs-lookup"><span data-stu-id="1a77e-196">If you're using System.Diagnostics.Trace, make sure you [configured it in `web.config`](https://msdn.microsoft.com/library/system.diagnostics.eventlogtracelistener.aspx).</span></span>
* <span data-ttu-id="1a77e-197">Disposez-vous de la dernière version d’Application Insights ?</span><span class="sxs-lookup"><span data-stu-id="1a77e-197">Have you got the latest version of Application Insights?</span></span> <span data-ttu-id="1a77e-198">Dans le menu **Outils** de Visual Studio, choisissez **Extensions et mises à jour**, puis ouvrez l’onglet **Mises à jour**. Si les outils Developer Analytics sont visibles, cliquez dessus pour les mettre à jour.</span><span class="sxs-lookup"><span data-stu-id="1a77e-198">In Visual Studio **Tools** menu, choose **Extensions and Updates**, and open the **Updates** tab. If Developer Analytics tools is there, click to update it.</span></span>

### <span data-ttu-id="1a77e-199"><a name="emptykey"></a>J’obtiens une erreur « La clé d’instrumentation ne peut pas être vide ».</span><span class="sxs-lookup"><span data-stu-id="1a77e-199"><a name="emptykey"></a>I get an error "Instrumentation key cannot be empty"</span></span>
<span data-ttu-id="1a77e-200">Vous avez peut-être installé le package Nuget de l'enregistreur de données sans installer Application Insights.</span><span class="sxs-lookup"><span data-stu-id="1a77e-200">Looks like you installed the logging adapter Nuget package without installing Application Insights.</span></span>

<span data-ttu-id="1a77e-201">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur `ApplicationInsights.config` , puis sélectionnez **Mettre à jour Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="1a77e-201">In Solution Explorer, right-click `ApplicationInsights.config` and choose **Update Application Insights**.</span></span> <span data-ttu-id="1a77e-202">Une boîte de dialogue vous invite à vous connecter à Azure et à créer une ressource Application Insights, ou à réutiliser une ressource existante.</span><span class="sxs-lookup"><span data-stu-id="1a77e-202">You'll get a dialog that invites you to sign in to Azure and either create an Application Insights resource, or re-use an existing one.</span></span> <span data-ttu-id="1a77e-203">Ceci devrait résoudre le problème.</span><span class="sxs-lookup"><span data-stu-id="1a77e-203">That should fix it.</span></span>

### <a name="i-can-see-traces-in-diagnostic-search-but-not-the-other-events"></a><span data-ttu-id="1a77e-204">Je peux voir des suivis dans la recherche de diagnostic, mais pas les autres événements</span><span class="sxs-lookup"><span data-stu-id="1a77e-204">I can see traces in diagnostic search, but not the other events</span></span>
<span data-ttu-id="1a77e-205">Le passage des événements et des demandes dans le pipeline peut prendre un certain temps.</span><span class="sxs-lookup"><span data-stu-id="1a77e-205">It can sometimes take a while for all the events and requests to get through the pipeline.</span></span>

### <span data-ttu-id="1a77e-206"><a name="limits"></a>Quelle est la quantité de données conservée ?</span><span class="sxs-lookup"><span data-stu-id="1a77e-206"><a name="limits"></a>How much data is retained?</span></span>
<span data-ttu-id="1a77e-207">Plusieurs facteurs affectent la quantité de données conservées.</span><span class="sxs-lookup"><span data-stu-id="1a77e-207">Several factors impact the amount of data retained.</span></span> <span data-ttu-id="1a77e-208">Consultez la section [Limites](app-insights-api-custom-events-metrics.md#limits) de la page sur les métriques d’événement client pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="1a77e-208">See the [limits](app-insights-api-custom-events-metrics.md#limits) section of the customer event metrics page for more information.</span></span> 

### <a name="im-not-seeing-some-of-the-log-entries-that-i-expect"></a><span data-ttu-id="1a77e-209">Certaines entrées du journal ne sont pas affichées</span><span class="sxs-lookup"><span data-stu-id="1a77e-209">I'm not seeing some of the log entries that I expect</span></span>
<span data-ttu-id="1a77e-210">Si votre application envoie des données en grand nombre et si vous utilisez le Kit de développement logiciel Application Insights pour ASP.NET version 2.0.0-beta3 ou ultérieure, la fonctionnalité d’échantillonnage adaptatif peut fonctionner et transmettre uniquement un pourcentage de vos données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="1a77e-210">If your application sends a lot of data and you are using the Application Insights SDK for ASP.NET version 2.0.0-beta3 or later, the adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> [<span data-ttu-id="1a77e-211">En savoir plus sur l’échantillonnage.</span><span class="sxs-lookup"><span data-stu-id="1a77e-211">Learn more about sampling.</span></span>](app-insights-sampling.md)

## <span data-ttu-id="1a77e-212"><a name="add"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1a77e-212"><a name="add"></a>Next steps</span></span>
* <span data-ttu-id="1a77e-213">[Configuration des tests de disponibilité et de réactivité][availability]</span><span class="sxs-lookup"><span data-stu-id="1a77e-213">[Set up availability and responsiveness tests][availability]</span></span>
* <span data-ttu-id="1a77e-214">[Résolution des problèmes][qna]</span><span class="sxs-lookup"><span data-stu-id="1a77e-214">[Troubleshooting][qna]</span></span>

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[portal]: https://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[start]: app-insights-overview.md
