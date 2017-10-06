---
title: aaaDiagnose erreurs et exceptions dans les applications avec Azure Application Insights web | Documents Microsoft
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
ms.openlocfilehash: 8930e6d2b29f83ea635c4ecb7afd11fc1d97d085
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-exceptions-in-your-web-apps-with-application-insights"></a><span data-ttu-id="976a7-103">Diagnostiquez les exceptions dans vos applications web avec Application Insights</span><span class="sxs-lookup"><span data-stu-id="976a7-103">Diagnose exceptions in your web apps with Application Insights</span></span>
<span data-ttu-id="976a7-104">Les exceptions dans votre application web dynamique sont signalées par [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="976a7-104">Exceptions in your live web app are reported by [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="976a7-105">Vous pouvez associer des demandes ayant échoué avec les exceptions et d’autres événements à hello client et le serveur, afin que vous puissiez diagnostiquer rapidement hello causes.</span><span class="sxs-lookup"><span data-stu-id="976a7-105">You can correlate failed requests with exceptions and other events at both hello client and server, so that you can quickly diagnose hello causes.</span></span>

## <a name="set-up-exception-reporting"></a><span data-ttu-id="976a7-106">Configurer les rapports d’exceptions</span><span class="sxs-lookup"><span data-stu-id="976a7-106">Set up exception reporting</span></span>
* <span data-ttu-id="976a7-107">exceptions toohave signalées à partir de votre application de serveur :</span><span class="sxs-lookup"><span data-stu-id="976a7-107">toohave exceptions reported from your server app:</span></span>
  * <span data-ttu-id="976a7-108">Installez le [SDK Application Insights](app-insights-asp-net.md) dans votre code d’application, ou</span><span class="sxs-lookup"><span data-stu-id="976a7-108">Install [Application Insights SDK](app-insights-asp-net.md) in your app code, or</span></span>
  * <span data-ttu-id="976a7-109">Serveurs web IIS : exécutez l’[Agent Application Insights](app-insights-monitor-performance-live-website-now.md) ; ou</span><span class="sxs-lookup"><span data-stu-id="976a7-109">IIS web servers: Run [Application Insights Agent](app-insights-monitor-performance-live-website-now.md); or</span></span>
  * <span data-ttu-id="976a7-110">Les applications web Azure : ajouter hello [Extension Application Insights](app-insights-azure-web-apps.md)</span><span class="sxs-lookup"><span data-stu-id="976a7-110">Azure web apps: Add hello [Application Insights Extension](app-insights-azure-web-apps.md)</span></span>
  * <span data-ttu-id="976a7-111">Applications web Java : installation hello [agent Java](app-insights-java-agent.md)</span><span class="sxs-lookup"><span data-stu-id="976a7-111">Java web apps: Install hello [Java agent](app-insights-java-agent.md)</span></span>
* <span data-ttu-id="976a7-112">Installer hello [extrait de code JavaScript](app-insights-javascript.md) dans vos pages web toocatch les exceptions du navigateur.</span><span class="sxs-lookup"><span data-stu-id="976a7-112">Install hello [JavaScript snippet](app-insights-javascript.md) in your web pages toocatch browser exceptions.</span></span>
* <span data-ttu-id="976a7-113">Dans certaines infrastructures d’application ou avec des paramètres, vous devez tootake toocatch de certaines étapes supplémentaires plus des exceptions :</span><span class="sxs-lookup"><span data-stu-id="976a7-113">In some application frameworks or with some settings, you need tootake some extra steps toocatch more exceptions:</span></span>
  * [<span data-ttu-id="976a7-114">Web forms</span><span class="sxs-lookup"><span data-stu-id="976a7-114">Web forms</span></span>](#web-forms)
  * [<span data-ttu-id="976a7-115">MVC</span><span class="sxs-lookup"><span data-stu-id="976a7-115">MVC</span></span>](#mvc)
  * [<span data-ttu-id="976a7-116">API web 1.*</span><span class="sxs-lookup"><span data-stu-id="976a7-116">Web API 1.*</span></span>](#web-api-1)
  * [<span data-ttu-id="976a7-117">API web 2.*</span><span class="sxs-lookup"><span data-stu-id="976a7-117">Web API 2.*</span></span>](#web-api-2)
  * [<span data-ttu-id="976a7-118">WCF</span><span class="sxs-lookup"><span data-stu-id="976a7-118">WCF</span></span>](#wcf)

## <a name="diagnosing-exceptions-using-visual-studio"></a><span data-ttu-id="976a7-119">Diagnostic des exceptions à l’aide de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="976a7-119">Diagnosing exceptions using Visual Studio</span></span>
<span data-ttu-id="976a7-120">Ouvrez la solution d’application hello dans toohelp Visual Studio avec le débogage.</span><span class="sxs-lookup"><span data-stu-id="976a7-120">Open hello app solution in Visual Studio toohelp with debugging.</span></span>

<span data-ttu-id="976a7-121">Exécutez l’application hello, sur votre serveur ou sur votre ordinateur de développement à l’aide de F5.</span><span class="sxs-lookup"><span data-stu-id="976a7-121">Run hello app, either on your server or on your development machine by using F5.</span></span>

<span data-ttu-id="976a7-122">Ouvrez la fenêtre de recherche Application Insights hello dans Visual Studio et la définir toodisplay événements à partir de votre application.</span><span class="sxs-lookup"><span data-stu-id="976a7-122">Open hello Application Insights Search window in Visual Studio, and set it toodisplay events from your app.</span></span> <span data-ttu-id="976a7-123">Pendant que vous déboguez, faire cela suffit de cliquer sur le bouton d’Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="976a7-123">While you're debugging, you can do this just by clicking hello Application Insights button.</span></span>

![Droit hello projet, puis choisissez Application Insights, ouvrir.](./media/app-insights-asp-net-exceptions/34.png)

<span data-ttu-id="976a7-125">Notez que vous pouvez filtrer les exceptions simplement hello rapport tooshow.</span><span class="sxs-lookup"><span data-stu-id="976a7-125">Notice that you can filter hello report tooshow just exceptions.</span></span>

<span data-ttu-id="976a7-126">*Aucune exception ne s’affiche ? Consultez [Capture des exceptions](#exceptions)* </span><span class="sxs-lookup"><span data-stu-id="976a7-126">*No exceptions showing? See [Capture exceptions](#exceptions).*</span></span>

<span data-ttu-id="976a7-127">Cliquez sur un tooshow de rapport d’exception de trace de la pile.</span><span class="sxs-lookup"><span data-stu-id="976a7-127">Click an exception report tooshow its stack trace.</span></span>
<span data-ttu-id="976a7-128">Cliquez sur une référence de ligne dans la trace de la pile hello, fichier de code approprié tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="976a7-128">Click a line reference in hello stack trace, tooopen hello relevant code file.</span></span>  

<span data-ttu-id="976a7-129">Dans le code hello, notez que CodeLens affiche les données sur les exceptions hello :</span><span class="sxs-lookup"><span data-stu-id="976a7-129">In hello code, notice that CodeLens shows data about hello exceptions:</span></span>

![Notification CodeLens des exceptions.](./media/app-insights-asp-net-exceptions/35.png)

## <a name="diagnosing-failures-using-hello-azure-portal"></a><span data-ttu-id="976a7-131">Diagnostiquer les défaillances à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="976a7-131">Diagnosing failures using hello Azure portal</span></span>
<span data-ttu-id="976a7-132">Vue d’ensemble d’Application Insights hello de votre application, vignette de défaillances hello vous montre des graphiques des exceptions et les demandes HTTP ayant échoué, ainsi que la liste de hello URL de la requête qui provoquent des échecs de hello plus fréquentes.</span><span class="sxs-lookup"><span data-stu-id="976a7-132">From hello Application Insights overview of your app, hello Failures tile shows you charts of exceptions and failed HTTP requests, together with a list of hello request URLs that cause hello most frequent failures.</span></span>

![Sélectionnez Paramètres, Défaillances](./media/app-insights-asp-net-exceptions/012-start.png)

<span data-ttu-id="976a7-134">Cliquez sur un des hello Échec de types d’exceptions dans les occurrences de tooindividual tooget hello liste d’exception hello, où vous pouvez afficher les détails de hello et trace de la pile :</span><span class="sxs-lookup"><span data-stu-id="976a7-134">Click through one of hello failed exception types in hello list tooget tooindividual occurrences of hello exception, where you can see hello details and stack trace:</span></span>

![Sélectionnez une instance de la demande a échoué et sous Détails de l’exception, obtenir tooinstances d’exception de hello.](./media/app-insights-asp-net-exceptions/030-req-drill.png)

<span data-ttu-id="976a7-136">**Vous pouvez également** vous pouvez démarrer à partir de la liste des demandes hello et trouver tooit connexes d’exceptions.</span><span class="sxs-lookup"><span data-stu-id="976a7-136">**Alternatively,** you can start from hello list of requests and find exceptions related tooit.</span></span>

<span data-ttu-id="976a7-137">*Aucune exception ne s’affiche ? Consultez [Capture des exceptions](#exceptions)* </span><span class="sxs-lookup"><span data-stu-id="976a7-137">*No exceptions showing? See [Capture exceptions](#exceptions).*</span></span>


## <a name="custom-tracing-and-log-data"></a><span data-ttu-id="976a7-138">Suivi personnalisé et données du journal</span><span class="sxs-lookup"><span data-stu-id="976a7-138">Custom tracing and log data</span></span>
<span data-ttu-id="976a7-139">application de tooyour spécifique de données de diagnostic tooget, vous pouvez insérer un code toosend vos propres données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="976a7-139">tooget diagnostic data specific tooyour app, you can insert code toosend your own telemetry data.</span></span> <span data-ttu-id="976a7-140">Cela est affiché dans la recherche de diagnostic en même temps que la demande de hello, affichage de page et autres données automatiquement collectées.</span><span class="sxs-lookup"><span data-stu-id="976a7-140">This displayed in diagnostic search alongside hello request, page view and other automatically-collected data.</span></span>

<span data-ttu-id="976a7-141">Vous disposez de plusieurs options :</span><span class="sxs-lookup"><span data-stu-id="976a7-141">You have several options:</span></span>

* <span data-ttu-id="976a7-142">[TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) est généralement utilisé pour l’analyse des tendances d’utilisation, mais il envoie également des données s’affiche sous les événements personnalisés dans la recherche de diagnostic de hello.</span><span class="sxs-lookup"><span data-stu-id="976a7-142">[TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) is typically used for monitoring usage patterns, but hello data it sends also appears under Custom Events in diagnostic search.</span></span> <span data-ttu-id="976a7-143">Les événements sont nommés et peuvent contenir des propriétés de type chaîne et des métriques numériques sur lesquels vous pouvez [filtrer vos recherches de diagnostic](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="976a7-143">Events are named, and can carry string properties and numeric metrics on which you can [filter your diagnostic searches](app-insights-diagnostic-search.md).</span></span>
* <span data-ttu-id="976a7-144">[TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) vous permet d’envoyer des données plus longues telles que des informations POST.</span><span class="sxs-lookup"><span data-stu-id="976a7-144">[TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) lets you send longer data such as POST information.</span></span>
* <span data-ttu-id="976a7-145">[TrackException()](#exceptions) envoie des arborescences des appels de procédure.</span><span class="sxs-lookup"><span data-stu-id="976a7-145">[TrackException()](#exceptions) sends stack traces.</span></span> <span data-ttu-id="976a7-146">[Plus d’informations sur les exceptions](#exceptions).</span><span class="sxs-lookup"><span data-stu-id="976a7-146">[More about exceptions](#exceptions).</span></span>
* <span data-ttu-id="976a7-147">Si vous utilisez déjà un framework de journalisation comme Log4Net ou NLog, vous pouvez [capturer ces journaux](app-insights-asp-net-trace-logs.md) et les visualiser dans Recherche de diagnostic avec les données sur les demandes et les exceptions.</span><span class="sxs-lookup"><span data-stu-id="976a7-147">If you already use a logging framework like Log4Net or NLog, you can [capture those logs](app-insights-asp-net-trace-logs.md) and see them in diagnostic search alongside request and exception data.</span></span>

<span data-ttu-id="976a7-148">Ouvrez de ces événements, toosee [recherche](app-insights-diagnostic-search.md), ouvrez le filtre, puis choisissez Custom Event, de Trace ou d’Exception.</span><span class="sxs-lookup"><span data-stu-id="976a7-148">toosee these events, open [Search](app-insights-diagnostic-search.md), open Filter, and then choose Custom Event, Trace, or Exception.</span></span>

![Extraire](./media/app-insights-asp-net-exceptions/viewCustomEvents.png)

> [!NOTE]
> <span data-ttu-id="976a7-150">Si votre application génère un grand nombre de télémétrie, module d’échantillonnage adaptive hello réduira automatiquement volume hello envoyé toohello portail en envoyant qu’une fraction représentative d’événements.</span><span class="sxs-lookup"><span data-stu-id="976a7-150">If your app generates a lot of telemetry, hello adaptive sampling module will automatically reduce hello volume that is sent toohello portal by sending only a representative fraction of events.</span></span> <span data-ttu-id="976a7-151">Les événements qui font partie de hello même opération sera sélectionnée ou désélectionnée en tant que groupe, afin que vous pouvez naviguer entre les événements connexes.</span><span class="sxs-lookup"><span data-stu-id="976a7-151">Events that are part of hello same operation will be selected or deselected as a group, so that you can navigate between related events.</span></span> [<span data-ttu-id="976a7-152">En savoir plus sur l'échantillonnage.</span><span class="sxs-lookup"><span data-stu-id="976a7-152">Learn about sampling.</span></span>](app-insights-sampling.md)
>
>

### <a name="how-toosee-request-post-data"></a><span data-ttu-id="976a7-153">Comment toosee demander les données de publication</span><span class="sxs-lookup"><span data-stu-id="976a7-153">How toosee request POST data</span></span>
<span data-ttu-id="976a7-154">Détails de la demande n’incluent pas les données hello envoyées tooyour application dans un appel POST.</span><span class="sxs-lookup"><span data-stu-id="976a7-154">Request details don't include hello data sent tooyour app in a POST call.</span></span> <span data-ttu-id="976a7-155">toohave signalés par ces données :</span><span class="sxs-lookup"><span data-stu-id="976a7-155">toohave this data reported:</span></span>

* <span data-ttu-id="976a7-156">[Installer hello SDK](app-insights-asp-net.md) dans votre projet d’application.</span><span class="sxs-lookup"><span data-stu-id="976a7-156">[Install hello SDK](app-insights-asp-net.md) in your application project.</span></span>
* <span data-ttu-id="976a7-157">Insérez le code de votre application toocall [Microsoft.ApplicationInsights.TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace).</span><span class="sxs-lookup"><span data-stu-id="976a7-157">Insert code in your application toocall [Microsoft.ApplicationInsights.TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace).</span></span> <span data-ttu-id="976a7-158">Envoyer les données de publication hello dans le paramètre de message hello.</span><span class="sxs-lookup"><span data-stu-id="976a7-158">Send hello POST data in hello message parameter.</span></span> <span data-ttu-id="976a7-159">Est une limite de taille toohello autorisée, donc vous devez essayer des données essentielles toosend simplement hello.</span><span class="sxs-lookup"><span data-stu-id="976a7-159">There is a limit toohello permitted size, so you should try toosend just hello essential data.</span></span>
* <span data-ttu-id="976a7-160">Lorsque vous examinez une demande ayant échoué, recherchez les traces hello associé.</span><span class="sxs-lookup"><span data-stu-id="976a7-160">When you investigate a failed request, find hello associated traces.</span></span>  

![Extraire](./media/app-insights-asp-net-exceptions/060-req-related.png)

## <span data-ttu-id="976a7-162"><a name="exceptions"></a> Capture des exceptions et des données de diagnostic connexes</span><span class="sxs-lookup"><span data-stu-id="976a7-162"><a name="exceptions"></a> Capturing exceptions and related diagnostic data</span></span>
<span data-ttu-id="976a7-163">Dans un premier temps, vous ne voyez dans le portail de hello toutes les exceptions hello entraînent l’échec de votre application.</span><span class="sxs-lookup"><span data-stu-id="976a7-163">At first, you won't see in hello portal all hello exceptions that cause failures in your app.</span></span> <span data-ttu-id="976a7-164">Vous verrez toutes les exceptions du navigateur (si vous utilisez hello [SDK JavaScript](app-insights-javascript.md) dans vos pages web).</span><span class="sxs-lookup"><span data-stu-id="976a7-164">You'll see any browser exceptions (if you're using hello [JavaScript SDK](app-insights-javascript.md) in your web pages).</span></span> <span data-ttu-id="976a7-165">Mais la plupart des exceptions de serveur sont interceptées par IIS et que vous avez toowrite un peu de code toosee les.</span><span class="sxs-lookup"><span data-stu-id="976a7-165">But most server exceptions are caught by IIS and you have toowrite a bit of code toosee them.</span></span>

<span data-ttu-id="976a7-166">Vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="976a7-166">You can:</span></span>

* <span data-ttu-id="976a7-167">**Enregistrer les exceptions explicitement** en insérant le code dans les exceptions de hello tooreport exception gestionnaires.</span><span class="sxs-lookup"><span data-stu-id="976a7-167">**Log exceptions explicitly** by inserting code in exception handlers tooreport hello exceptions.</span></span>
* <span data-ttu-id="976a7-168">**Capturer automatiquement des exceptions** en configurant votre infrastructure ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="976a7-168">**Capture exceptions automatically** by configuring your ASP.NET framework.</span></span> <span data-ttu-id="976a7-169">les ajouts nécessaires Hello sont différents pour différents types de framework.</span><span class="sxs-lookup"><span data-stu-id="976a7-169">hello necessary additions are different for different types of framework.</span></span>

## <a name="reporting-exceptions-explicitly"></a><span data-ttu-id="976a7-170">Signalisation explicite des exceptions</span><span class="sxs-lookup"><span data-stu-id="976a7-170">Reporting exceptions explicitly</span></span>
<span data-ttu-id="976a7-171">Bonjour façon la plus simple est tooinsert un appel tooTrackException() dans un gestionnaire d’exceptions.</span><span class="sxs-lookup"><span data-stu-id="976a7-171">hello simplest way is tooinsert a call tooTrackException() in an exception handler.</span></span>

<span data-ttu-id="976a7-172">JavaScript</span><span class="sxs-lookup"><span data-stu-id="976a7-172">JavaScript</span></span>

    try
    { ...
    }
    catch (ex)
    {
      appInsights.trackException(ex, "handler loc",
        {Game: currentGame.Name,
         State: currentGame.State.ToString()});
    }

<span data-ttu-id="976a7-173">C#</span><span class="sxs-lookup"><span data-stu-id="976a7-173">C#</span></span>

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

       // Send hello exception telemetry:
       telemetry.TrackException(ex, properties, measurements);
    }

<span data-ttu-id="976a7-174">VB</span><span class="sxs-lookup"><span data-stu-id="976a7-174">VB</span></span>

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

      ' Send hello exception telemetry:
      telemetry.TrackException(ex, properties, measurements)
    End Try

<span data-ttu-id="976a7-175">Hello les mesures et les propriétés de paramètres sont facultatifs, mais sont utiles pour [le filtrage et l’ajout de](app-insights-diagnostic-search.md) des informations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="976a7-175">hello properties and measurements parameters are optional, but are useful for [filtering and adding](app-insights-diagnostic-search.md) extra information.</span></span> <span data-ttu-id="976a7-176">Par exemple, si vous avez une application qui peut exécuter plusieurs jeux, vous pouvez rechercher tous les hello exception rapports connexes tooa jeu particulier.</span><span class="sxs-lookup"><span data-stu-id="976a7-176">For example, if you have an app that can run several games, you could find all hello exception reports related tooa particular game.</span></span> <span data-ttu-id="976a7-177">Vous pouvez ajouter autant d’éléments que vous comme tooeach dictionnaire.</span><span class="sxs-lookup"><span data-stu-id="976a7-177">You can add as many items as you like tooeach dictionary.</span></span>

## <a name="browser-exceptions"></a><span data-ttu-id="976a7-178">Exceptions du navigateur</span><span class="sxs-lookup"><span data-stu-id="976a7-178">Browser exceptions</span></span>
<span data-ttu-id="976a7-179">La plupart des exceptions de navigateur sont signalées.</span><span class="sxs-lookup"><span data-stu-id="976a7-179">Most browser exceptions are reported.</span></span>

<span data-ttu-id="976a7-180">Si votre page web inclut des fichiers de script à partir des réseaux de diffusion de contenu ou d’autres domaines, vérifiez votre balise de script a l’attribut de hello ```crossorigin="anonymous"```, et ce serveur hello envoie [en-têtes CORS](http://enable-cors.org/).</span><span class="sxs-lookup"><span data-stu-id="976a7-180">If your web page includes script files from content delivery networks or other domains, ensure your script tag has hello attribute ```crossorigin="anonymous"```,  and that hello server sends [CORS headers](http://enable-cors.org/).</span></span> <span data-ttu-id="976a7-181">Cela vous permettra de tooget une trace de pile et les détails des exceptions JavaScript non gérées à partir de ces ressources.</span><span class="sxs-lookup"><span data-stu-id="976a7-181">This will allow you tooget a stack trace and detail for unhandled JavaScript exceptions from these resources.</span></span>

## <a name="web-forms"></a><span data-ttu-id="976a7-182">Formulaires web</span><span class="sxs-lookup"><span data-stu-id="976a7-182">Web forms</span></span>
<span data-ttu-id="976a7-183">Pour web forms, hello HTTP Module sera toocollect en mesure des exceptions hello lorsqu’il n’y a aucuns configurée avec CustomErrors de redirection.</span><span class="sxs-lookup"><span data-stu-id="976a7-183">For web forms, hello HTTP Module will be able toocollect hello exceptions when there are no redirects configured with CustomErrors.</span></span>

<span data-ttu-id="976a7-184">Toutefois, si vous avez des redirections actives, ajouter hello suivant lignes toohello Application_Error fonction dans Global.asax.cs.</span><span class="sxs-lookup"><span data-stu-id="976a7-184">But if you have active redirects, add hello following lines toohello Application_Error function in Global.asax.cs.</span></span> <span data-ttu-id="976a7-185">(Ajouter un fichier Global.asax si vous n'en avez pas déjà).</span><span class="sxs-lookup"><span data-stu-id="976a7-185">(Add a Global.asax file if you don't already have one.)</span></span>

<span data-ttu-id="976a7-186">*C#*</span><span class="sxs-lookup"><span data-stu-id="976a7-186">*C#*</span></span>

    void Application_Error(object sender, EventArgs e)
    {
      if (HttpContext.Current.IsCustomErrorEnabled && Server.GetLastError  () != null)
      {
         var ai = new TelemetryClient(); // or re-use an existing instance

         ai.TrackException(Server.GetLastError());
      }
    }


## <a name="mvc"></a><span data-ttu-id="976a7-187">MVC</span><span class="sxs-lookup"><span data-stu-id="976a7-187">MVC</span></span>
<span data-ttu-id="976a7-188">Si hello [CustomErrors](https://msdn.microsoft.com/library/h0hfz6fc.aspx) configuration est `Off`, exceptions seront alors disponibles pour hello [HTTP Module](https://msdn.microsoft.com/library/ms178468.aspx) toocollect.</span><span class="sxs-lookup"><span data-stu-id="976a7-188">If hello [CustomErrors](https://msdn.microsoft.com/library/h0hfz6fc.aspx) configuration is `Off`, then exceptions will be available for hello [HTTP Module](https://msdn.microsoft.com/library/ms178468.aspx) toocollect.</span></span> <span data-ttu-id="976a7-189">Toutefois, si elle est `RemoteOnly` (valeur par défaut), ou `On`, puis hello est désactivée et non disponible pour l’Application Insights tooautomatically collecter.</span><span class="sxs-lookup"><span data-stu-id="976a7-189">However, if it is `RemoteOnly` (default), or `On`, then hello exception will be cleared and not available for Application Insights tooautomatically collect.</span></span> <span data-ttu-id="976a7-190">Vous pouvez résoudre cela en substituant hello [System.Web.Mvc.HandleErrorAttribute classe](http://msdn.microsoft.com/library/system.web.mvc.handleerrorattribute.aspx)et en appliquant la classe hello substitué comme indiqué pour les versions MVC hello différents ci-dessous ([github source](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions/blob/master/MVC2App/Controllers/AiHandleErrorAttribute.cs)) :</span><span class="sxs-lookup"><span data-stu-id="976a7-190">You can fix that by overriding hello [System.Web.Mvc.HandleErrorAttribute class](http://msdn.microsoft.com/library/system.web.mvc.handleerrorattribute.aspx), and applying hello overridden class as shown for hello different MVC versions below ([github source](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions/blob/master/MVC2App/Controllers/AiHandleErrorAttribute.cs)):</span></span>

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
                //If customError is Off, then AI HTTPModule will report hello exception
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

#### <a name="mvc-2"></a><span data-ttu-id="976a7-191">MVC 2</span><span class="sxs-lookup"><span data-stu-id="976a7-191">MVC 2</span></span>
<span data-ttu-id="976a7-192">Remplacer l’attribut de HandleError de hello avec votre nouvel attribut sur vos contrôleurs.</span><span class="sxs-lookup"><span data-stu-id="976a7-192">Replace hello HandleError attribute with your new attribute in your controllers.</span></span>

    namespace MVC2App.Controllers
    {
       [AiHandleError]
       public class HomeController : Controller
       {
    ...

[<span data-ttu-id="976a7-193">Exemple</span><span class="sxs-lookup"><span data-stu-id="976a7-193">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions)

#### <a name="mvc-3"></a><span data-ttu-id="976a7-194">MVC 3</span><span class="sxs-lookup"><span data-stu-id="976a7-194">MVC 3</span></span>
<span data-ttu-id="976a7-195">Enregistrez `AiHandleErrorAttribute` en tant que filtre global dans Global.asax.cs :</span><span class="sxs-lookup"><span data-stu-id="976a7-195">Register `AiHandleErrorAttribute` as a global filter in Global.asax.cs:</span></span>

    public class MyMvcApplication : System.Web.HttpApplication
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
         filters.Add(new AiHandleErrorAttribute());
      }
     ...

[<span data-ttu-id="976a7-196">Exemple</span><span class="sxs-lookup"><span data-stu-id="976a7-196">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc3UnhandledExceptionTelemetry)

#### <a name="mvc-4-mvc5"></a><span data-ttu-id="976a7-197">MVC 4, MVC 5</span><span class="sxs-lookup"><span data-stu-id="976a7-197">MVC 4, MVC5</span></span>
<span data-ttu-id="976a7-198">Enregistrez AiHandleErrorAttribute en tant que filtre global dans FilterConfig.cs :</span><span class="sxs-lookup"><span data-stu-id="976a7-198">Register AiHandleErrorAttribute as a global filter in FilterConfig.cs:</span></span>

    public class FilterConfig
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
        // Default replaced with hello override tootrack unhandled exceptions
        filters.Add(new AiHandleErrorAttribute());
      }
    }

[<span data-ttu-id="976a7-199">Exemple</span><span class="sxs-lookup"><span data-stu-id="976a7-199">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc5UnhandledExceptionTelemetry)

## <a name="web-api-1x"></a><span data-ttu-id="976a7-200">API Web 1.x</span><span class="sxs-lookup"><span data-stu-id="976a7-200">Web API 1.x</span></span>
<span data-ttu-id="976a7-201">Remplacez System.Web.Http.Filters.ExceptionFilterAttribute :</span><span class="sxs-lookup"><span data-stu-id="976a7-201">Override System.Web.Http.Filters.ExceptionFilterAttribute:</span></span>

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

<span data-ttu-id="976a7-202">Vous pourriez ajouter ce contrôleurs de toospecific attribut substituée ou ajouter de configuration de filtres globaux toohello dans la classe WebApiConfig de hello :</span><span class="sxs-lookup"><span data-stu-id="976a7-202">You could add this overridden attribute toospecific controllers, or add it toohello global filter configuration in hello WebApiConfig class:</span></span>

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

[<span data-ttu-id="976a7-203">Exemple</span><span class="sxs-lookup"><span data-stu-id="976a7-203">Sample</span></span>](https://github.com/AppInsightsSamples/WebApi_1.x_UnhandledExceptions)

<span data-ttu-id="976a7-204">Il existe un nombre de cas qui ne peut pas gérer les filtres d’exception hello.</span><span class="sxs-lookup"><span data-stu-id="976a7-204">There are a number of cases that hello exception filters cannot handle.</span></span> <span data-ttu-id="976a7-205">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="976a7-205">For example:</span></span>

* <span data-ttu-id="976a7-206">Les exceptions lancées à partir des constructeurs de contrôleur.</span><span class="sxs-lookup"><span data-stu-id="976a7-206">Exceptions thrown from controller constructors.</span></span>
* <span data-ttu-id="976a7-207">Les exceptions lancées à partir des gestionnaires de messages.</span><span class="sxs-lookup"><span data-stu-id="976a7-207">Exceptions thrown from message handlers.</span></span>
* <span data-ttu-id="976a7-208">Les exceptions lancées pendant le routage.</span><span class="sxs-lookup"><span data-stu-id="976a7-208">Exceptions thrown during routing.</span></span>
* <span data-ttu-id="976a7-209">Les exceptions lancées pendant la sérialisation du contenu de réponse.</span><span class="sxs-lookup"><span data-stu-id="976a7-209">Exceptions thrown during response content serialization.</span></span>

## <a name="web-api-2x"></a><span data-ttu-id="976a7-210">API Web 2.x</span><span class="sxs-lookup"><span data-stu-id="976a7-210">Web API 2.x</span></span>
<span data-ttu-id="976a7-211">Ajoutez d'une implémentation de IExceptionLogger :</span><span class="sxs-lookup"><span data-stu-id="976a7-211">Add an implementation of IExceptionLogger:</span></span>

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

<span data-ttu-id="976a7-212">Ajoutez ce service toohello dans WebApiConfig :</span><span class="sxs-lookup"><span data-stu-id="976a7-212">Add this toohello services in WebApiConfig:</span></span>

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
  <span data-ttu-id="976a7-213">}</span><span class="sxs-lookup"><span data-stu-id="976a7-213">}</span></span>

[<span data-ttu-id="976a7-214">Exemple</span><span class="sxs-lookup"><span data-stu-id="976a7-214">Sample</span></span>](https://github.com/AppInsightsSamples/WebApi_2.x_UnhandledExceptions)

<span data-ttu-id="976a7-215">Alternativement, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="976a7-215">As alternatives, you could:</span></span>

1. <span data-ttu-id="976a7-216">Remplacez hello uniquement ExceptionHandler avec une implémentation personnalisée de IExceptionHandler.</span><span class="sxs-lookup"><span data-stu-id="976a7-216">Replace hello only ExceptionHandler with a custom implementation of IExceptionHandler.</span></span> <span data-ttu-id="976a7-217">Cela est uniquement appelée lorsque l’infrastructure hello est toujours en mesure de toochoose la réponse de message toosend (et non pas au moment de la connexion de hello est abandonnée pour l’instance)</span><span class="sxs-lookup"><span data-stu-id="976a7-217">This is only called when hello framework is still able toochoose which response message toosend (not when hello connection is aborted for instance)</span></span>
2. <span data-ttu-id="976a7-218">Filtres d’exception (comme décrit dans la section hello sur les contrôleurs de 1.x API Web ci-dessus) - ne pas appelées dans tous les cas.</span><span class="sxs-lookup"><span data-stu-id="976a7-218">Exception Filters (as described in hello section on Web API 1.x controllers above) - not called in all cases.</span></span>

## <a name="wcf"></a><span data-ttu-id="976a7-219">WCF</span><span class="sxs-lookup"><span data-stu-id="976a7-219">WCF</span></span>
<span data-ttu-id="976a7-220">Ajoutez une classe qui étend l'attribut et implémente IErrorHandler et IServiceBehavior.</span><span class="sxs-lookup"><span data-stu-id="976a7-220">Add a class that extends Attribute and implements IErrorHandler and IServiceBehavior.</span></span>

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

<span data-ttu-id="976a7-221">Ajoutez les implémentations de service toohello hello attribut :</span><span class="sxs-lookup"><span data-stu-id="976a7-221">Add hello attribute toohello service implementations:</span></span>

    namespace WcfService4
    {
        [AiLogException]
        public class Service1 : IService1
        {
         ...

[<span data-ttu-id="976a7-222">Exemple</span><span class="sxs-lookup"><span data-stu-id="976a7-222">Sample</span></span>](https://github.com/AppInsightsSamples/WCFUnhandledExceptions)

## <a name="exception-performance-counters"></a><span data-ttu-id="976a7-223">Compteurs de performance des exceptions</span><span class="sxs-lookup"><span data-stu-id="976a7-223">Exception performance counters</span></span>
<span data-ttu-id="976a7-224">Si vous avez [installé hello Application Insights Agent](app-insights-monitor-performance-live-website-now.md) sur votre serveur, vous pouvez obtenir un graphique du taux d’exceptions hello, mesurée par .NET.</span><span class="sxs-lookup"><span data-stu-id="976a7-224">If you have [installed hello Application Insights Agent](app-insights-monitor-performance-live-website-now.md) on your server, you can get a chart of hello exceptions rate, measured by .NET.</span></span> <span data-ttu-id="976a7-225">Celui-ci comprend les exceptions .NET gérées et non gérées.</span><span class="sxs-lookup"><span data-stu-id="976a7-225">This includes both handled and unhandled .NET exceptions.</span></span>

<span data-ttu-id="976a7-226">Ouvrez un panneau d'explorateur de mesures, ajoutez un nouveau graphique, puis sélectionnez **Taux d'exception**sous Compteurs de performances.</span><span class="sxs-lookup"><span data-stu-id="976a7-226">Open a Metric Explorer blade, add a new chart, and select **Exception rate**, listed under Performance Counters.</span></span>

<span data-ttu-id="976a7-227">.NET framework de Hello calcule le taux de hello en comptant le nombre hello d’exceptions dans un intervalle et en divisant par la longueur de l’intervalle de salutation hello.</span><span class="sxs-lookup"><span data-stu-id="976a7-227">hello .NET framework calculates hello rate by counting hello number of exceptions in an interval and dividing by hello length of hello interval.</span></span>

<span data-ttu-id="976a7-228">Notez qu’il sera différent de nombre hello « Exceptions » calculé par le portail Application Insights de hello à partir des rapports de TrackException.</span><span class="sxs-lookup"><span data-stu-id="976a7-228">Note that it will be different from hello 'Exceptions' count calculated by hello Application Insights portal by counting TrackException reports.</span></span> <span data-ttu-id="976a7-229">intervalles d’échantillonnage de Hello sont différentes, et hello SDK n’envoie pas de rapports TrackException pour toutes les exceptions gérées et non gérées.</span><span class="sxs-lookup"><span data-stu-id="976a7-229">hello sampling intervals are different, and hello SDK doesn't send TrackException reports for all handled and unhandled exceptions.</span></span>

## <a name="video"></a><span data-ttu-id="976a7-230">Vidéo</span><span class="sxs-lookup"><span data-stu-id="976a7-230">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="next-steps"></a><span data-ttu-id="976a7-231">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="976a7-231">Next steps</span></span>
* [<span data-ttu-id="976a7-232">Surveiller le reste, SQL et autres toodependencies d’appels</span><span class="sxs-lookup"><span data-stu-id="976a7-232">Monitor REST, SQL and other calls toodependencies</span></span>](app-insights-asp-net-dependencies.md)
* [<span data-ttu-id="976a7-233">Surveiller les durées de chargement des pages, les exceptions du navigateur et les appels AJAX</span><span class="sxs-lookup"><span data-stu-id="976a7-233">Monitor page load times, browser exceptions, and AJAX calls</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="976a7-234">Surveiller les compteurs de performances</span><span class="sxs-lookup"><span data-stu-id="976a7-234">Monitor performance counters</span></span>](app-insights-performance-counters.md)
