---
title: "Diagnostic des défaillances et des exceptions dans les applications web avec Application Insights | Microsoft Docs"
description: "Capturez des exceptions à partir d’applications ASP.NET, ainsi que des données de télémétrie des demandes."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d1e98390-3ce4-4d04-9351-144314a42aa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 7eeacdc6677ccdebb1653e94a163ecb47090b7ee
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="diagnose-exceptions-in-your-web-apps-with-application-insights"></a><span data-ttu-id="f69c7-103">Diagnostiquez les exceptions dans vos applications web avec Application Insights</span><span class="sxs-lookup"><span data-stu-id="f69c7-103">Diagnose exceptions in your web apps with Application Insights</span></span>
<span data-ttu-id="f69c7-104">Les exceptions dans votre application web dynamique sont signalées par [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f69c7-104">Exceptions in your live web app are reported by [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="f69c7-105">Vous pouvez associer les demandes ayant échoué à des exceptions et à d’autres événements sur le client et le serveur, ce qui vous permet de diagnostiquer rapidement les causes.</span><span class="sxs-lookup"><span data-stu-id="f69c7-105">You can correlate failed requests with exceptions and other events at both the client and server, so that you can quickly diagnose the causes.</span></span>

## <a name="set-up-exception-reporting"></a><span data-ttu-id="f69c7-106">Configurer les rapports d’exceptions</span><span class="sxs-lookup"><span data-stu-id="f69c7-106">Set up exception reporting</span></span>
* <span data-ttu-id="f69c7-107">Pour que les exceptions soient signalées par votre application de serveur :</span><span class="sxs-lookup"><span data-stu-id="f69c7-107">To have exceptions reported from your server app:</span></span>
  * <span data-ttu-id="f69c7-108">Installez le [SDK Application Insights](app-insights-asp-net.md) dans votre code d’application, ou</span><span class="sxs-lookup"><span data-stu-id="f69c7-108">Install [Application Insights SDK](app-insights-asp-net.md) in your app code, or</span></span>
  * <span data-ttu-id="f69c7-109">Serveurs web IIS : exécutez l’[Agent Application Insights](app-insights-monitor-performance-live-website-now.md) ; ou</span><span class="sxs-lookup"><span data-stu-id="f69c7-109">IIS web servers: Run [Application Insights Agent](app-insights-monitor-performance-live-website-now.md); or</span></span>
  * <span data-ttu-id="f69c7-110">Applications web Azure : ajoutez l’[extension Application Insights](app-insights-azure-web-apps.md)</span><span class="sxs-lookup"><span data-stu-id="f69c7-110">Azure web apps: Add the [Application Insights Extension](app-insights-azure-web-apps.md)</span></span>
  * <span data-ttu-id="f69c7-111">Applications web Java : installez l’[agent Java](app-insights-java-agent.md)</span><span class="sxs-lookup"><span data-stu-id="f69c7-111">Java web apps: Install the [Java agent](app-insights-java-agent.md)</span></span>
* <span data-ttu-id="f69c7-112">Installez l’[extrait de code JavaScript](app-insights-javascript.md) dans vos pages web pour intercepter les exceptions du navigateur.</span><span class="sxs-lookup"><span data-stu-id="f69c7-112">Install the [JavaScript snippet](app-insights-javascript.md) in your web pages to catch browser exceptions.</span></span>
* <span data-ttu-id="f69c7-113">Dans certains frameworks d’application ou avec certains paramètres, vous devez prendre des mesures supplémentaires pour intercepter davantage d’exceptions :</span><span class="sxs-lookup"><span data-stu-id="f69c7-113">In some application frameworks or with some settings, you need to take some extra steps to catch more exceptions:</span></span>
  * [<span data-ttu-id="f69c7-114">Web forms</span><span class="sxs-lookup"><span data-stu-id="f69c7-114">Web forms</span></span>](#web-forms)
  * [<span data-ttu-id="f69c7-115">MVC</span><span class="sxs-lookup"><span data-stu-id="f69c7-115">MVC</span></span>](#mvc)
  * [<span data-ttu-id="f69c7-116">API web 1.*</span><span class="sxs-lookup"><span data-stu-id="f69c7-116">Web API 1.*</span></span>](#web-api-1)
  * [<span data-ttu-id="f69c7-117">API web 2.*</span><span class="sxs-lookup"><span data-stu-id="f69c7-117">Web API 2.*</span></span>](#web-api-2)
  * [<span data-ttu-id="f69c7-118">WCF</span><span class="sxs-lookup"><span data-stu-id="f69c7-118">WCF</span></span>](#wcf)

## <a name="diagnosing-exceptions-using-visual-studio"></a><span data-ttu-id="f69c7-119">Diagnostic des exceptions à l’aide de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f69c7-119">Diagnosing exceptions using Visual Studio</span></span>
<span data-ttu-id="f69c7-120">Ouvrez la solution d’application dans Visual Studio pour faciliter le débogage.</span><span class="sxs-lookup"><span data-stu-id="f69c7-120">Open the app solution in Visual Studio to help with debugging.</span></span>

<span data-ttu-id="f69c7-121">Exécutez l’application sur votre serveur ou sur votre ordinateur de développement à l’aide de la touche F5.</span><span class="sxs-lookup"><span data-stu-id="f69c7-121">Run the app, either on your server or on your development machine by using F5.</span></span>

<span data-ttu-id="f69c7-122">Ouvrez la fenêtre de recherche d’Application Insights dans Visual Studio et configurez-la pour afficher les événements depuis votre application.</span><span class="sxs-lookup"><span data-stu-id="f69c7-122">Open the Application Insights Search window in Visual Studio, and set it to display events from your app.</span></span> <span data-ttu-id="f69c7-123">En cours de débogage, il vous suffit de cliquer sur le bouton Application Insights pour effectuer ce paramétrage.</span><span class="sxs-lookup"><span data-stu-id="f69c7-123">While you're debugging, you can do this just by clicking the Application Insights button.</span></span>

![Cliquez avec le bouton droit sur le projet et sélectionnez Application Insights, Ouvrir.](./media/app-insights-asp-net-exceptions/34.png)

<span data-ttu-id="f69c7-125">Notez que vous pouvez filtrer le rapport pour qu’il affiche uniquement les exceptions.</span><span class="sxs-lookup"><span data-stu-id="f69c7-125">Notice that you can filter the report to show just exceptions.</span></span>

<span data-ttu-id="f69c7-126">*Aucune exception ne s’affiche ? Consultez [Capture des exceptions](#exceptions)* </span><span class="sxs-lookup"><span data-stu-id="f69c7-126">*No exceptions showing? See [Capture exceptions](#exceptions).*</span></span>

<span data-ttu-id="f69c7-127">Cliquez sur un rapport d’exception pour afficher sa trace de pile.</span><span class="sxs-lookup"><span data-stu-id="f69c7-127">Click an exception report to show its stack trace.</span></span>
<span data-ttu-id="f69c7-128">Cliquez sur une référence de ligne dans l’arborescence des appels de procédure pour ouvrir le fichier de code approprié.</span><span class="sxs-lookup"><span data-stu-id="f69c7-128">Click a line reference in the stack trace, to open the relevant code file.</span></span>  

<span data-ttu-id="f69c7-129">Dans le code, notez que CodeLens affiche les données sur les exceptions :</span><span class="sxs-lookup"><span data-stu-id="f69c7-129">In the code, notice that CodeLens shows data about the exceptions:</span></span>

![Notification CodeLens des exceptions.](./media/app-insights-asp-net-exceptions/35.png)

## <a name="diagnosing-failures-using-the-azure-portal"></a><span data-ttu-id="f69c7-131">Diagnostic des défaillances à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="f69c7-131">Diagnosing failures using the Azure portal</span></span>
<span data-ttu-id="f69c7-132">Dans la vue d’ensemble Application Insights de votre application, la vignette Défaillances vous montre les graphiques des exceptions et des demandes HTTP ayant échoué ainsi qu’une liste des URL demandées qui entraînent les défaillances les plus fréquentes.</span><span class="sxs-lookup"><span data-stu-id="f69c7-132">From the Application Insights overview of your app, the Failures tile shows you charts of exceptions and failed HTTP requests, together with a list of the request URLs that cause the most frequent failures.</span></span>

![Sélectionnez Paramètres, Défaillances](./media/app-insights-asp-net-exceptions/012-start.png)

<span data-ttu-id="f69c7-134">Cliquez sur l’un des types d’exception ayant échoué dans la liste pour obtenir des occurrences individuelles de l’exception, où vous pouvez afficher les détails et l’arborescence des appels de procédure :</span><span class="sxs-lookup"><span data-stu-id="f69c7-134">Click through one of the failed exception types in the list to get to individual occurrences of the exception, where you can see the details and stack trace:</span></span>

![Sélectionnez l’instance d'une demande ayant échoué et, sous Détails de l'exception, accédez aux instances de l'exception.](./media/app-insights-asp-net-exceptions/030-req-drill.png)

<span data-ttu-id="f69c7-136">**Vous pouvez également** commencer à partir de la liste des requêtes et rechercher les exceptions qui lui sont associées.</span><span class="sxs-lookup"><span data-stu-id="f69c7-136">**Alternatively,** you can start from the list of requests and find exceptions related to it.</span></span>

<span data-ttu-id="f69c7-137">*Aucune exception ne s’affiche ? Consultez [Capture des exceptions](#exceptions)* </span><span class="sxs-lookup"><span data-stu-id="f69c7-137">*No exceptions showing? See [Capture exceptions](#exceptions).*</span></span>


## <a name="custom-tracing-and-log-data"></a><span data-ttu-id="f69c7-138">Suivi personnalisé et données du journal</span><span class="sxs-lookup"><span data-stu-id="f69c7-138">Custom tracing and log data</span></span>
<span data-ttu-id="f69c7-139">Pour obtenir des données de diagnostic propres à votre application, vous pouvez insérer le code pour envoyer vos propres données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="f69c7-139">To get diagnostic data specific to your app, you can insert code to send your own telemetry data.</span></span> <span data-ttu-id="f69c7-140">Ces informations apparaissent dans Recherche de diagnostic avec la demande, une vue de la page et d’autres données automatiquement collectées.</span><span class="sxs-lookup"><span data-stu-id="f69c7-140">This displayed in diagnostic search alongside the request, page view and other automatically-collected data.</span></span>

<span data-ttu-id="f69c7-141">Vous disposez de plusieurs options :</span><span class="sxs-lookup"><span data-stu-id="f69c7-141">You have several options:</span></span>

* <span data-ttu-id="f69c7-142">[TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) sert généralement à surveiller les modèles d’utilisation, mais les données qu’il envoie apparaissent également sous Evénements personnalisés dans Recherche de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="f69c7-142">[TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) is typically used for monitoring usage patterns, but the data it sends also appears under Custom Events in diagnostic search.</span></span> <span data-ttu-id="f69c7-143">Les événements sont nommés et peuvent contenir des propriétés de type chaîne et des métriques numériques sur lesquels vous pouvez [filtrer vos recherches de diagnostic](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="f69c7-143">Events are named, and can carry string properties and numeric metrics on which you can [filter your diagnostic searches](app-insights-diagnostic-search.md).</span></span>
* <span data-ttu-id="f69c7-144">[TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) vous permet d’envoyer des données plus longues telles que des informations POST.</span><span class="sxs-lookup"><span data-stu-id="f69c7-144">[TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) lets you send longer data such as POST information.</span></span>
* <span data-ttu-id="f69c7-145">[TrackException()](#exceptions) envoie des arborescences des appels de procédure.</span><span class="sxs-lookup"><span data-stu-id="f69c7-145">[TrackException()](#exceptions) sends stack traces.</span></span> <span data-ttu-id="f69c7-146">[Plus d’informations sur les exceptions](#exceptions).</span><span class="sxs-lookup"><span data-stu-id="f69c7-146">[More about exceptions](#exceptions).</span></span>
* <span data-ttu-id="f69c7-147">Si vous utilisez déjà un framework de journalisation comme Log4Net ou NLog, vous pouvez [capturer ces journaux](app-insights-asp-net-trace-logs.md) et les visualiser dans Recherche de diagnostic avec les données sur les demandes et les exceptions.</span><span class="sxs-lookup"><span data-stu-id="f69c7-147">If you already use a logging framework like Log4Net or NLog, you can [capture those logs](app-insights-asp-net-trace-logs.md) and see them in diagnostic search alongside request and exception data.</span></span>

<span data-ttu-id="f69c7-148">Pour afficher ces événements, ouvrez [Recherche](app-insights-diagnostic-search.md), ouvrez Filtre, puis choisissez Événement personnalisé, Trace ou Exception.</span><span class="sxs-lookup"><span data-stu-id="f69c7-148">To see these events, open [Search](app-insights-diagnostic-search.md), open Filter, and then choose Custom Event, Trace, or Exception.</span></span>

![Extraire](./media/app-insights-asp-net-exceptions/viewCustomEvents.png)

> [!NOTE]
> <span data-ttu-id="f69c7-150">Si votre application génère un volume important de télémétrie, le module d'échantillonnage adaptatif réduit automatiquement le volume qui est envoyé vers le portail en envoyant uniquement une fraction représentative des événements.</span><span class="sxs-lookup"><span data-stu-id="f69c7-150">If your app generates a lot of telemetry, the adaptive sampling module will automatically reduce the volume that is sent to the portal by sending only a representative fraction of events.</span></span> <span data-ttu-id="f69c7-151">Les événements qui font partie de la même opération seront activés ou désactivés en tant que groupe, afin que vous puissiez naviguer entre les événements connexes.</span><span class="sxs-lookup"><span data-stu-id="f69c7-151">Events that are part of the same operation will be selected or deselected as a group, so that you can navigate between related events.</span></span> [<span data-ttu-id="f69c7-152">En savoir plus sur l'échantillonnage.</span><span class="sxs-lookup"><span data-stu-id="f69c7-152">Learn about sampling.</span></span>](app-insights-sampling.md)
>
>

### <a name="how-to-see-request-post-data"></a><span data-ttu-id="f69c7-153">Affichage des données POST de la demande</span><span class="sxs-lookup"><span data-stu-id="f69c7-153">How to see request POST data</span></span>
<span data-ttu-id="f69c7-154">Les détails de la demande n'incluent pas les données envoyées à votre application dans un appel POST.</span><span class="sxs-lookup"><span data-stu-id="f69c7-154">Request details don't include the data sent to your app in a POST call.</span></span> <span data-ttu-id="f69c7-155">Pour que ces données soient signalées :</span><span class="sxs-lookup"><span data-stu-id="f69c7-155">To have this data reported:</span></span>

* <span data-ttu-id="f69c7-156">[Installez le SDK](app-insights-asp-net.md) dans votre projet d’application.</span><span class="sxs-lookup"><span data-stu-id="f69c7-156">[Install the SDK](app-insights-asp-net.md) in your application project.</span></span>
* <span data-ttu-id="f69c7-157">Insérez du code dans votre application pour appeler [Microsoft.ApplicationInsights.TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace).</span><span class="sxs-lookup"><span data-stu-id="f69c7-157">Insert code in your application to call [Microsoft.ApplicationInsights.TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace).</span></span> <span data-ttu-id="f69c7-158">Envoyez les données POST dans le paramètre du message.</span><span class="sxs-lookup"><span data-stu-id="f69c7-158">Send the POST data in the message parameter.</span></span> <span data-ttu-id="f69c7-159">Il existe une limite à la taille autorisée. Vous pouvez donc essayer d'envoyer uniquement les données essentielles.</span><span class="sxs-lookup"><span data-stu-id="f69c7-159">There is a limit to the permitted size, so you should try to send just the essential data.</span></span>
* <span data-ttu-id="f69c7-160">Lorsque vous examinez une demande ayant échoué, recherchez les traces associées.</span><span class="sxs-lookup"><span data-stu-id="f69c7-160">When you investigate a failed request, find the associated traces.</span></span>  

![Extraire](./media/app-insights-asp-net-exceptions/060-req-related.png)

## <span data-ttu-id="f69c7-162"><a name="exceptions"></a> Capture des exceptions et des données de diagnostic connexes</span><span class="sxs-lookup"><span data-stu-id="f69c7-162"><a name="exceptions"></a> Capturing exceptions and related diagnostic data</span></span>
<span data-ttu-id="f69c7-163">Dans un premier temps, vous ne verrez pas dans le portail toutes les exceptions qui entraînent des défaillances dans votre application.</span><span class="sxs-lookup"><span data-stu-id="f69c7-163">At first, you won't see in the portal all the exceptions that cause failures in your app.</span></span> <span data-ttu-id="f69c7-164">Vous verrez les exceptions du navigateur (si vous utilisez le [SDK JavaScript](app-insights-javascript.md) dans vos pages web).</span><span class="sxs-lookup"><span data-stu-id="f69c7-164">You'll see any browser exceptions (if you're using the [JavaScript SDK](app-insights-javascript.md) in your web pages).</span></span> <span data-ttu-id="f69c7-165">Mais la plupart des exceptions de serveur sont interceptées par IIS et vous devez écrire un peu de code afin de les afficher.</span><span class="sxs-lookup"><span data-stu-id="f69c7-165">But most server exceptions are caught by IIS and you have to write a bit of code to see them.</span></span>

<span data-ttu-id="f69c7-166">Vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="f69c7-166">You can:</span></span>

* <span data-ttu-id="f69c7-167">**Enregistrer explicitement des exceptions** en insérant le code dans les gestionnaires d'exceptions pour signaler ces exceptions.</span><span class="sxs-lookup"><span data-stu-id="f69c7-167">**Log exceptions explicitly** by inserting code in exception handlers to report the exceptions.</span></span>
* <span data-ttu-id="f69c7-168">**Capturer automatiquement des exceptions** en configurant votre infrastructure ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="f69c7-168">**Capture exceptions automatically** by configuring your ASP.NET framework.</span></span> <span data-ttu-id="f69c7-169">Les ajouts nécessaires sont différents selon les différents types d’infrastructure.</span><span class="sxs-lookup"><span data-stu-id="f69c7-169">The necessary additions are different for different types of framework.</span></span>

## <a name="reporting-exceptions-explicitly"></a><span data-ttu-id="f69c7-170">Signalisation explicite des exceptions</span><span class="sxs-lookup"><span data-stu-id="f69c7-170">Reporting exceptions explicitly</span></span>
<span data-ttu-id="f69c7-171">La façon la plus simple consiste à insérer un appel à TrackException() dans un gestionnaire d'exceptions.</span><span class="sxs-lookup"><span data-stu-id="f69c7-171">The simplest way is to insert a call to TrackException() in an exception handler.</span></span>

<span data-ttu-id="f69c7-172">JavaScript</span><span class="sxs-lookup"><span data-stu-id="f69c7-172">JavaScript</span></span>

    try
    { ...
    }
    catch (ex)
    {
      appInsights.trackException(ex, "handler loc",
        {Game: currentGame.Name,
         State: currentGame.State.ToString()});
    }

<span data-ttu-id="f69c7-173">C#</span><span class="sxs-lookup"><span data-stu-id="f69c7-173">C#</span></span>

    var telemetry = new TelemetryClient();
    ...
    try
    { ...
    }
    catch (Exception ex)
    {
       // Set up some properties:
       var properties = new Dictionary <string, string>
         {{"Game", currentGame.Name}};

       var measurements = new Dictionary <string, double>
         {{"Users", currentGame.Users.Count}};

       // Send the exception telemetry:
       telemetry.TrackException(ex, properties, measurements);
    }

<span data-ttu-id="f69c7-174">VB</span><span class="sxs-lookup"><span data-stu-id="f69c7-174">VB</span></span>

    Dim telemetry = New TelemetryClient
    ...
    Try
      ...
    Catch ex as Exception
      ' Set up some properties:
      Dim properties = New Dictionary (Of String, String)
      properties.Add("Game", currentGame.Name)

      Dim measurements = New Dictionary (Of String, Double)
      measurements.Add("Users", currentGame.Users.Count)

      ' Send the exception telemetry:
      telemetry.TrackException(ex, properties, measurements)
    End Try

<span data-ttu-id="f69c7-175">Les paramètres de propriétés et les mesures sont facultatifs, mais sont utiles pour [filtrer et ajouter](app-insights-diagnostic-search.md) des informations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="f69c7-175">The properties and measurements parameters are optional, but are useful for [filtering and adding](app-insights-diagnostic-search.md) extra information.</span></span> <span data-ttu-id="f69c7-176">Par exemple, si vous avez une application qui peut exécuter plusieurs jeux, vous pouvez rechercher tous les rapports d'exception liés à un jeu particulier.</span><span class="sxs-lookup"><span data-stu-id="f69c7-176">For example, if you have an app that can run several games, you could find all the exception reports related to a particular game.</span></span> <span data-ttu-id="f69c7-177">Vous pouvez ajouter autant d'éléments que vous le souhaitez à chaque dictionnaire.</span><span class="sxs-lookup"><span data-stu-id="f69c7-177">You can add as many items as you like to each dictionary.</span></span>

## <a name="browser-exceptions"></a><span data-ttu-id="f69c7-178">Exceptions du navigateur</span><span class="sxs-lookup"><span data-stu-id="f69c7-178">Browser exceptions</span></span>
<span data-ttu-id="f69c7-179">La plupart des exceptions de navigateur sont signalées.</span><span class="sxs-lookup"><span data-stu-id="f69c7-179">Most browser exceptions are reported.</span></span>

<span data-ttu-id="f69c7-180">Si votre page web inclut des fichiers de script à partir de réseaux de distribution de contenu ou d’autres domaines, vérifiez que votre balise de script possède l’attribut ```crossorigin="anonymous"```et que le serveur envoie des [en-têtes CORS](http://enable-cors.org/).</span><span class="sxs-lookup"><span data-stu-id="f69c7-180">If your web page includes script files from content delivery networks or other domains, ensure your script tag has the attribute ```crossorigin="anonymous"```,  and that the server sends [CORS headers](http://enable-cors.org/).</span></span> <span data-ttu-id="f69c7-181">Cela vous permettra d'obtenir une arborescence des appels de procédure et les détails des exceptions JavaScript non gérées à partir de ces ressources.</span><span class="sxs-lookup"><span data-stu-id="f69c7-181">This will allow you to get a stack trace and detail for unhandled JavaScript exceptions from these resources.</span></span>

## <a name="web-forms"></a><span data-ttu-id="f69c7-182">Formulaires web</span><span class="sxs-lookup"><span data-stu-id="f69c7-182">Web forms</span></span>
<span data-ttu-id="f69c7-183">Pour les formulaires web, le module HTTP pourra collecter les exceptions si aucune redirection n’est configurée avec CustomErrors.</span><span class="sxs-lookup"><span data-stu-id="f69c7-183">For web forms, the HTTP Module will be able to collect the exceptions when there are no redirects configured with CustomErrors.</span></span>

<span data-ttu-id="f69c7-184">Mais si vous avez des redirections actives, ajoutez les lignes suivantes à la fonction Application_Error dans Global.asax.cs.</span><span class="sxs-lookup"><span data-stu-id="f69c7-184">But if you have active redirects, add the following lines to the Application_Error function in Global.asax.cs.</span></span> <span data-ttu-id="f69c7-185">(Ajouter un fichier Global.asax si vous n'en avez pas déjà).</span><span class="sxs-lookup"><span data-stu-id="f69c7-185">(Add a Global.asax file if you don't already have one.)</span></span>

<span data-ttu-id="f69c7-186">*C#*</span><span class="sxs-lookup"><span data-stu-id="f69c7-186">*C#*</span></span>

    void Application_Error(object sender, EventArgs e)
    {
      if (HttpContext.Current.IsCustomErrorEnabled && Server.GetLastError  () != null)
      {
         var ai = new TelemetryClient(); // or re-use an existing instance

         ai.TrackException(Server.GetLastError());
      }
    }


## <a name="mvc"></a><span data-ttu-id="f69c7-187">MVC</span><span class="sxs-lookup"><span data-stu-id="f69c7-187">MVC</span></span>
<span data-ttu-id="f69c7-188">Si la configuration de [CustomErrors](https://msdn.microsoft.com/library/h0hfz6fc.aspx) est `Off`, les exceptions seront alors disponibles pour être collectées par le [module HTTP](https://msdn.microsoft.com/library/ms178468.aspx).</span><span class="sxs-lookup"><span data-stu-id="f69c7-188">If the [CustomErrors](https://msdn.microsoft.com/library/h0hfz6fc.aspx) configuration is `Off`, then exceptions will be available for the [HTTP Module](https://msdn.microsoft.com/library/ms178468.aspx) to collect.</span></span> <span data-ttu-id="f69c7-189">Toutefois, si elle est `RemoteOnly` (valeur par défaut), ou `On`, l'exception ne sera alors pas disponible pour être collectée automatiquement par Application Insights.</span><span class="sxs-lookup"><span data-stu-id="f69c7-189">However, if it is `RemoteOnly` (default), or `On`, then the exception will be cleared and not available for Application Insights to automatically collect.</span></span> <span data-ttu-id="f69c7-190">Vous pouvez corriger cela en remplaçant la [classe System.Web.Mvc.HandleErrorAttribute](http://msdn.microsoft.com/library/system.web.mvc.handleerrorattribute.aspx) et en appliquant la classe remplacée comme indiqué pour les différentes versions MVC ci-dessous ([source github](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions/blob/master/MVC2App/Controllers/AiHandleErrorAttribute.cs)) :</span><span class="sxs-lookup"><span data-stu-id="f69c7-190">You can fix that by overriding the [System.Web.Mvc.HandleErrorAttribute class](http://msdn.microsoft.com/library/system.web.mvc.handleerrorattribute.aspx), and applying the overridden class as shown for the different MVC versions below ([github source](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions/blob/master/MVC2App/Controllers/AiHandleErrorAttribute.cs)):</span></span>

    using System;
    using System.Web.Mvc;
    using Microsoft.ApplicationInsights;

    namespace MVC2App.Controllers
    {
      [AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited = true, AllowMultiple = true)]
      public class AiHandleErrorAttribute : HandleErrorAttribute
      {
        public override void OnException(ExceptionContext filterContext)
        {
            if (filterContext != null && filterContext.HttpContext != null && filterContext.Exception != null)
            {
                //If customError is Off, then AI HTTPModule will report the exception
                if (filterContext.HttpContext.IsCustomErrorEnabled)
                {   //or reuse instance (recommended!). see note above  
                    var ai = new TelemetryClient();
                    ai.TrackException(filterContext.Exception);
                }
            }
            base.OnException(filterContext);
        }
      }
    }

#### <a name="mvc-2"></a><span data-ttu-id="f69c7-191">MVC 2</span><span class="sxs-lookup"><span data-stu-id="f69c7-191">MVC 2</span></span>
<span data-ttu-id="f69c7-192">Remplacez l'attribut HandleError par votre nouvel attribut dans vos contrôleurs.</span><span class="sxs-lookup"><span data-stu-id="f69c7-192">Replace the HandleError attribute with your new attribute in your controllers.</span></span>

    namespace MVC2App.Controllers
    {
       [AiHandleError]
       public class HomeController : Controller
       {
    ...

[<span data-ttu-id="f69c7-193">Exemple</span><span class="sxs-lookup"><span data-stu-id="f69c7-193">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions)

#### <a name="mvc-3"></a><span data-ttu-id="f69c7-194">MVC 3</span><span class="sxs-lookup"><span data-stu-id="f69c7-194">MVC 3</span></span>
<span data-ttu-id="f69c7-195">Enregistrez `AiHandleErrorAttribute` en tant que filtre global dans Global.asax.cs :</span><span class="sxs-lookup"><span data-stu-id="f69c7-195">Register `AiHandleErrorAttribute` as a global filter in Global.asax.cs:</span></span>

    public class MyMvcApplication : System.Web.HttpApplication
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
         filters.Add(new AiHandleErrorAttribute());
      }
     ...

[<span data-ttu-id="f69c7-196">Exemple</span><span class="sxs-lookup"><span data-stu-id="f69c7-196">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc3UnhandledExceptionTelemetry)

#### <a name="mvc-4-mvc5"></a><span data-ttu-id="f69c7-197">MVC 4, MVC 5</span><span class="sxs-lookup"><span data-stu-id="f69c7-197">MVC 4, MVC5</span></span>
<span data-ttu-id="f69c7-198">Enregistrez AiHandleErrorAttribute en tant que filtre global dans FilterConfig.cs :</span><span class="sxs-lookup"><span data-stu-id="f69c7-198">Register AiHandleErrorAttribute as a global filter in FilterConfig.cs:</span></span>

    public class FilterConfig
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
        // Default replaced with the override to track unhandled exceptions
        filters.Add(new AiHandleErrorAttribute());
      }
    }

[<span data-ttu-id="f69c7-199">Exemple</span><span class="sxs-lookup"><span data-stu-id="f69c7-199">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc5UnhandledExceptionTelemetry)

## <a name="web-api-1x"></a><span data-ttu-id="f69c7-200">API Web 1.x</span><span class="sxs-lookup"><span data-stu-id="f69c7-200">Web API 1.x</span></span>
<span data-ttu-id="f69c7-201">Remplacez System.Web.Http.Filters.ExceptionFilterAttribute :</span><span class="sxs-lookup"><span data-stu-id="f69c7-201">Override System.Web.Http.Filters.ExceptionFilterAttribute:</span></span>

    using System.Web.Http.Filters;
    using Microsoft.ApplicationInsights;

    namespace WebAPI.App_Start
    {
      public class AiExceptionFilterAttribute : ExceptionFilterAttribute
      {
        public override void OnException(HttpActionExecutedContext actionExecutedContext)
        {
            if (actionExecutedContext != null && actionExecutedContext.Exception != null)
            {  //or reuse instance (recommended!). see note above
                var ai = new TelemetryClient();
                ai.TrackException(actionExecutedContext.Exception);    
            }
            base.OnException(actionExecutedContext);
        }
      }
    }

<span data-ttu-id="f69c7-202">Vous pouvez ajouter cet attribut remplacé à des contrôleurs spécifiques ou l’ajouter à la configuration du filtre global dans la classe WebApiConfig :</span><span class="sxs-lookup"><span data-stu-id="f69c7-202">You could add this overridden attribute to specific controllers, or add it to the global filter configuration in the WebApiConfig class:</span></span>

    using System.Web.Http;
    using WebApi1.x.App_Start;

    namespace WebApi1.x
    {
      public static class WebApiConfig
      {
        public static void Register(HttpConfiguration config)
        {
            config.Routes.MapHttpRoute(name: "DefaultApi", routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional });
            ...
            config.EnableSystemDiagnosticsTracing();

            // Capture exceptions for Application Insights:
            config.Filters.Add(new AiExceptionFilterAttribute());
        }
      }
    }

[<span data-ttu-id="f69c7-203">Exemple</span><span class="sxs-lookup"><span data-stu-id="f69c7-203">Sample</span></span>](https://github.com/AppInsightsSamples/WebApi_1.x_UnhandledExceptions)

<span data-ttu-id="f69c7-204">Il existe un certain nombre de cas que les filtres d'exception ne peuvent pas gérer.</span><span class="sxs-lookup"><span data-stu-id="f69c7-204">There are a number of cases that the exception filters cannot handle.</span></span> <span data-ttu-id="f69c7-205">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="f69c7-205">For example:</span></span>

* <span data-ttu-id="f69c7-206">Les exceptions lancées à partir des constructeurs de contrôleur.</span><span class="sxs-lookup"><span data-stu-id="f69c7-206">Exceptions thrown from controller constructors.</span></span>
* <span data-ttu-id="f69c7-207">Les exceptions lancées à partir des gestionnaires de messages.</span><span class="sxs-lookup"><span data-stu-id="f69c7-207">Exceptions thrown from message handlers.</span></span>
* <span data-ttu-id="f69c7-208">Les exceptions lancées pendant le routage.</span><span class="sxs-lookup"><span data-stu-id="f69c7-208">Exceptions thrown during routing.</span></span>
* <span data-ttu-id="f69c7-209">Les exceptions lancées pendant la sérialisation du contenu de réponse.</span><span class="sxs-lookup"><span data-stu-id="f69c7-209">Exceptions thrown during response content serialization.</span></span>

## <a name="web-api-2x"></a><span data-ttu-id="f69c7-210">API Web 2.x</span><span class="sxs-lookup"><span data-stu-id="f69c7-210">Web API 2.x</span></span>
<span data-ttu-id="f69c7-211">Ajoutez d'une implémentation de IExceptionLogger :</span><span class="sxs-lookup"><span data-stu-id="f69c7-211">Add an implementation of IExceptionLogger:</span></span>

    using System.Web.Http.ExceptionHandling;
    using Microsoft.ApplicationInsights;

    namespace ProductsAppPureWebAPI.App_Start
    {
      public class AiExceptionLogger : ExceptionLogger
      {
        public override void Log(ExceptionLoggerContext context)
        {
            if (context !=null && context.Exception != null)
            {//or reuse instance (recommended!). see note above
                var ai = new TelemetryClient();
                ai.TrackException(context.Exception);
            }
            base.Log(context);
        }
      }
    }

<span data-ttu-id="f69c7-212">Ajoutez cela aux services dans WebApiConfig :</span><span class="sxs-lookup"><span data-stu-id="f69c7-212">Add this to the services in WebApiConfig:</span></span>

    using System.Web.Http;
    using System.Web.Http.ExceptionHandling;
    using ProductsAppPureWebAPI.App_Start;

    namespace WebApi2WithMVC
    {
      public static class WebApiConfig
      {
        public static void Register(HttpConfiguration config)
        {
            // Web API configuration and services

            // Web API routes
            config.MapHttpAttributeRoutes();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );
            config.Services.Add(typeof(IExceptionLogger), new AiExceptionLogger());
        }
      }
  <span data-ttu-id="f69c7-213">}</span><span class="sxs-lookup"><span data-stu-id="f69c7-213">}</span></span>

[<span data-ttu-id="f69c7-214">Exemple</span><span class="sxs-lookup"><span data-stu-id="f69c7-214">Sample</span></span>](https://github.com/AppInsightsSamples/WebApi_2.x_UnhandledExceptions)

<span data-ttu-id="f69c7-215">Alternativement, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="f69c7-215">As alternatives, you could:</span></span>

1. <span data-ttu-id="f69c7-216">Remplacer le seul gestionnaire d’exceptions avec une implémentation personnalisée de IExceptionHandler.</span><span class="sxs-lookup"><span data-stu-id="f69c7-216">Replace the only ExceptionHandler with a custom implementation of IExceptionHandler.</span></span> <span data-ttu-id="f69c7-217">Celle-ci est appelée uniquement lorsque l'infrastructure est toujours en mesure de choisir le message de réponse à envoyer (mais pas lorsque la connexion est abandonnée par exemple)</span><span class="sxs-lookup"><span data-stu-id="f69c7-217">This is only called when the framework is still able to choose which response message to send (not when the connection is aborted for instance)</span></span>
2. <span data-ttu-id="f69c7-218">Les filtres d'exception (comme décrit dans la section sur les contrôleurs API Web 1.x ci-dessus) ne sont pas appelés dans tous les cas.</span><span class="sxs-lookup"><span data-stu-id="f69c7-218">Exception Filters (as described in the section on Web API 1.x controllers above) - not called in all cases.</span></span>

## <a name="wcf"></a><span data-ttu-id="f69c7-219">WCF</span><span class="sxs-lookup"><span data-stu-id="f69c7-219">WCF</span></span>
<span data-ttu-id="f69c7-220">Ajoutez une classe qui étend l'attribut et implémente IErrorHandler et IServiceBehavior.</span><span class="sxs-lookup"><span data-stu-id="f69c7-220">Add a class that extends Attribute and implements IErrorHandler and IServiceBehavior.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.ServiceModel.Description;
    using System.ServiceModel.Dispatcher;
    using System.Web;
    using Microsoft.ApplicationInsights;

    namespace WcfService4.ErrorHandling
    {
      public class AiLogExceptionAttribute : Attribute, IErrorHandler, IServiceBehavior
      {
        public void AddBindingParameters(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase,
            System.Collections.ObjectModel.Collection<ServiceEndpoint> endpoints,
            System.ServiceModel.Channels.BindingParameterCollection bindingParameters)
        {
        }

        public void ApplyDispatchBehavior(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase)
        {
            foreach (ChannelDispatcher disp in serviceHostBase.ChannelDispatchers)
            {
                disp.ErrorHandlers.Add(this);
            }
        }

        public void Validate(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase)
        {
        }

        bool IErrorHandler.HandleError(Exception error)
        {//or reuse instance (recommended!). see note above
            var ai = new TelemetryClient();

            ai.TrackException(error);
            return false;
        }

        void IErrorHandler.ProvideFault(Exception error,
            System.ServiceModel.Channels.MessageVersion version,
            ref System.ServiceModel.Channels.Message fault)
        {
        }
      }
    }

<span data-ttu-id="f69c7-221">Ajoutez l'attribut aux implémentations de service :</span><span class="sxs-lookup"><span data-stu-id="f69c7-221">Add the attribute to the service implementations:</span></span>

    namespace WcfService4
    {
        [AiLogException]
        public class Service1 : IService1
        {
         ...

[<span data-ttu-id="f69c7-222">Exemple</span><span class="sxs-lookup"><span data-stu-id="f69c7-222">Sample</span></span>](https://github.com/AppInsightsSamples/WCFUnhandledExceptions)

## <a name="exception-performance-counters"></a><span data-ttu-id="f69c7-223">Compteurs de performance des exceptions</span><span class="sxs-lookup"><span data-stu-id="f69c7-223">Exception performance counters</span></span>
<span data-ttu-id="f69c7-224">Si vous avez [installé l’agent Application Insights](app-insights-monitor-performance-live-website-now.md) sur votre serveur, vous pouvez obtenir un graphique du taux d’exceptions, mesuré par .NET.</span><span class="sxs-lookup"><span data-stu-id="f69c7-224">If you have [installed the Application Insights Agent](app-insights-monitor-performance-live-website-now.md) on your server, you can get a chart of the exceptions rate, measured by .NET.</span></span> <span data-ttu-id="f69c7-225">Celui-ci comprend les exceptions .NET gérées et non gérées.</span><span class="sxs-lookup"><span data-stu-id="f69c7-225">This includes both handled and unhandled .NET exceptions.</span></span>

<span data-ttu-id="f69c7-226">Ouvrez un panneau d'explorateur de mesures, ajoutez un nouveau graphique, puis sélectionnez **Taux d'exception**sous Compteurs de performances.</span><span class="sxs-lookup"><span data-stu-id="f69c7-226">Open a Metric Explorer blade, add a new chart, and select **Exception rate**, listed under Performance Counters.</span></span>

<span data-ttu-id="f69c7-227">.NET Framework calcule le taux en comptant le nombre d’exceptions sur un intervalle et en divisant ce nombre par la longueur de l’intervalle.</span><span class="sxs-lookup"><span data-stu-id="f69c7-227">The .NET framework calculates the rate by counting the number of exceptions in an interval and dividing by the length of the interval.</span></span>

<span data-ttu-id="f69c7-228">Notez que ce chiffre sera différent du nombre d’« exceptions » calculé par le portail Application Insights, qui est basé sur les rapports TrackException.</span><span class="sxs-lookup"><span data-stu-id="f69c7-228">Note that it will be different from the 'Exceptions' count calculated by the Application Insights portal by counting TrackException reports.</span></span> <span data-ttu-id="f69c7-229">Les intervalles d’échantillonnage sont différents et le Kit de développement logiciel (SDK) n’envoie pas de rapports TrackException pour toutes les exceptions gérées et non gérées.</span><span class="sxs-lookup"><span data-stu-id="f69c7-229">The sampling intervals are different, and the SDK doesn't send TrackException reports for all handled and unhandled exceptions.</span></span>

## <a name="video"></a><span data-ttu-id="f69c7-230">Vidéo</span><span class="sxs-lookup"><span data-stu-id="f69c7-230">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="next-steps"></a><span data-ttu-id="f69c7-231">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f69c7-231">Next steps</span></span>
* [<span data-ttu-id="f69c7-232">Surveiller REST, SQL et les autres appels aux dépendances</span><span class="sxs-lookup"><span data-stu-id="f69c7-232">Monitor REST, SQL and other calls to dependencies</span></span>](app-insights-asp-net-dependencies.md)
* [<span data-ttu-id="f69c7-233">Surveiller les durées de chargement des pages, les exceptions du navigateur et les appels AJAX</span><span class="sxs-lookup"><span data-stu-id="f69c7-233">Monitor page load times, browser exceptions, and AJAX calls</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="f69c7-234">Surveiller les compteurs de performances</span><span class="sxs-lookup"><span data-stu-id="f69c7-234">Monitor performance counters</span></span>](app-insights-performance-counters.md)
