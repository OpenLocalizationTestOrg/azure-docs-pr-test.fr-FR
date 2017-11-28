---
title: "aaaMonitor de votre application l’intégrité et l’utilisation avec Application Insights"
description: Prise en main d'Application Insights. Analyze usage, availability and performance of your on-premises or Microsoft Azure applications.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 40650472-e860-4c1b-a589-9956245df307
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/25/2015
ms.author: bwren
ms.openlocfilehash: 9230a6e65e5afb00c36122ff1d1de01ba19cd7f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-performance-in-web-applications"></a><span data-ttu-id="e7c7f-104">Analyse des performances dans les applications web</span><span class="sxs-lookup"><span data-stu-id="e7c7f-104">Monitor performance in web applications</span></span>


<span data-ttu-id="e7c7f-105">Assurez-vous que votre application fonctionne correctement et identifiez rapidement toutes les défaillances éventuelles.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-105">Make sure your application is performing well, and find out quickly about any failures.</span></span> <span data-ttu-id="e7c7f-106">[Application Insights] [ start] sera vous indiquent des problèmes de performances et des exceptions, et les aident à identifier et de diagnostiquer hello causes.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-106">[Application Insights][start] will tell you about any performance issues and exceptions, and help you find and diagnose hello root causes.</span></span>

<span data-ttu-id="e7c7f-107">Application Insights peut surveiller les services WCF, ainsi que les applications et services web Java et ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-107">Application Insights can monitor both Java and ASP.NET web applications and services, WCF services.</span></span> <span data-ttu-id="e7c7f-108">Ils peuvent être hébergés localement, sur des machines virtuelles, ou en tant que sites web Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-108">They can be hosted on-premises, on virtual machines, or as Microsoft Azure websites.</span></span> 

<span data-ttu-id="e7c7f-109">Côté client de hello, Application Insights peut prendre de télémétrie à partir des pages web et un large éventail de périphériques, notamment iOS, Android et les applications du Windows Store.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-109">On hello client side, Application Insights can take telemetry from web pages and a wide variety of devices including iOS, Android and Windows Store apps.</span></span>

>[!Note]
> <span data-ttu-id="e7c7f-110">Nous proposons une nouvelle expérience pour identifier les pages qui ralentissent votre application web.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-110">We have made a new experience available for finding slow performing pages in your web application.</span></span> <span data-ttu-id="e7c7f-111">Si vous n’avez pas accès tooit, activez-le en configurant les options de votre version d’évaluation avec hello [panneau d’aperçu](app-insights-previews.md).</span><span class="sxs-lookup"><span data-stu-id="e7c7f-111">If you don't have access tooit, enable it by configuring your preview options with hello [Preview blade](app-insights-previews.md).</span></span> <span data-ttu-id="e7c7f-112">En savoir plus sur cette nouvelle expérience dans [rechercher et résoudre les goulots d’étranglement de performances avec un examen des performances interactif de hello](#Find-and-fix-performance-bottlenecks-with-an-interactive-Performance-investigation).</span><span class="sxs-lookup"><span data-stu-id="e7c7f-112">Read about this new experience in [Find and fix performance bottlenecks with hello interactive Performance investigation](#Find-and-fix-performance-bottlenecks-with-an-interactive-Performance-investigation).</span></span>

## <span data-ttu-id="e7c7f-113"><a name="setup"></a>Configurer la surveillance des performances</span><span class="sxs-lookup"><span data-stu-id="e7c7f-113"><a name="setup"></a>Set up performance monitoring</span></span>
<span data-ttu-id="e7c7f-114">Si vous n’avez pas encore ajouté Application Insights tooyour (autrement dit, s’il n’a pas ApplicationInsights.config) du projet, choisissez une des manières suivantes tooget démarré :</span><span class="sxs-lookup"><span data-stu-id="e7c7f-114">If you haven't yet added Application Insights tooyour project (that is, if it doesn't have ApplicationInsights.config), choose one of these ways tooget started:</span></span>

* [<span data-ttu-id="e7c7f-115">Applications web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="e7c7f-115">ASP.NET web apps</span></span>](app-insights-asp-net.md)
  * [<span data-ttu-id="e7c7f-116">Ajout de la surveillance des exceptions</span><span class="sxs-lookup"><span data-stu-id="e7c7f-116">Add exception monitoring</span></span>](app-insights-asp-net-exceptions.md)
  * [<span data-ttu-id="e7c7f-117">Ajout de la surveillance des dépendances</span><span class="sxs-lookup"><span data-stu-id="e7c7f-117">Add dependency monitoring</span></span>](app-insights-monitor-performance-live-website-now.md)
* [<span data-ttu-id="e7c7f-118">Applications web J2EE</span><span class="sxs-lookup"><span data-stu-id="e7c7f-118">J2EE web apps</span></span>](app-insights-java-get-started.md)
  * [<span data-ttu-id="e7c7f-119">Ajout de la surveillance des dépendances</span><span class="sxs-lookup"><span data-stu-id="e7c7f-119">Add dependency monitoring</span></span>](app-insights-java-agent.md)

## <span data-ttu-id="e7c7f-120"><a name="view"></a>Exploration des mesures de performances</span><span class="sxs-lookup"><span data-stu-id="e7c7f-120"><a name="view"></a>Exploring performance metrics</span></span>
<span data-ttu-id="e7c7f-121">Dans [hello portail Azure](https://portal.azure.com), recherchez la ressource Application Insights toohello que vous avez configurée pour votre application.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-121">In [hello Azure portal](https://portal.azure.com), browse toohello Application Insights resource that you set up for your application.</span></span> <span data-ttu-id="e7c7f-122">Panneau de vue d’ensemble de Hello affiche des données de performances de base :</span><span class="sxs-lookup"><span data-stu-id="e7c7f-122">hello overview blade shows basic performance data:</span></span>

<span data-ttu-id="e7c7f-123">Cliquez sur n’importe quel toosee graphique plus en détail et les résultats de toosee pour une période plus longue.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-123">Click any chart toosee more detail, and toosee results for a longer period.</span></span> <span data-ttu-id="e7c7f-124">Par exemple, cliquez sur la vignette de demandes hello, puis sélectionnez une plage de temps :</span><span class="sxs-lookup"><span data-stu-id="e7c7f-124">For example, click hello Requests tile and then select a time range:</span></span>

![Parcourez les données toomore et sélectionnez une plage de temps](./media/app-insights-web-monitor-performance/appinsights-48metrics.png)

<span data-ttu-id="e7c7f-126">Cliquez sur un graphique toochoose les métriques, il s’affiche, ou ajouter un nouveau graphique et sélectionnez ses mesures :</span><span class="sxs-lookup"><span data-stu-id="e7c7f-126">Click a chart toochoose which metrics it displays, or add a new chart and select its metrics:</span></span>

![Cliquez sur une métrique de toochoose graphique](./media/app-insights-web-monitor-performance/appinsights-61perfchoices.png)

> [!NOTE]
> <span data-ttu-id="e7c7f-128">**Désactivez toutes les métriques hello** sélection complète toosee hello qui est disponible.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-128">**Uncheck all hello metrics** toosee hello full selection that is available.</span></span> <span data-ttu-id="e7c7f-129">métriques de Hello sont répartis en groupes ; Lorsqu’un membre d’un groupe est sélectionné, seuls hello autres membres de ce groupe s’affichent.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-129">hello metrics fall into groups; when any member of a group is selected, only hello other members of that group appear.</span></span>

## <span data-ttu-id="e7c7f-130"><a name="metrics"></a>Signification</span><span class="sxs-lookup"><span data-stu-id="e7c7f-130"><a name="metrics"></a>What does it all mean?</span></span> <span data-ttu-id="e7c7f-131">Vignettes de performances et rapports</span><span class="sxs-lookup"><span data-stu-id="e7c7f-131">Performance tiles and reports</span></span>
<span data-ttu-id="e7c7f-132">Vous pouvez obtenir plusieurs indicateurs de performance.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-132">There are various performance metrics you can get.</span></span> <span data-ttu-id="e7c7f-133">Commençons par ceux qui s’affichent par défaut sur le panneau des applications hello.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-133">Let's start with those that appear by default on hello application blade.</span></span>

### <a name="requests"></a><span data-ttu-id="e7c7f-134">Requests</span><span class="sxs-lookup"><span data-stu-id="e7c7f-134">Requests</span></span>
<span data-ttu-id="e7c7f-135">nombre de Hello de requêtes HTTP reçues pendant la période spécifiée.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-135">hello number of HTTP requests received in a specified period.</span></span> <span data-ttu-id="e7c7f-136">Comparer avec les résultats de hello en autres toosee rapports comment votre application se comporte comme hello charge varie.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-136">Compare this with hello results on other reports toosee how your app behaves as hello load varies.</span></span>

<span data-ttu-id="e7c7f-137">Les demandes HTTP incluent toutes les demandes GET ou POST de pages, données et images.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-137">HTTP requests include all GET or POST requests for pages, data, and images.</span></span>

<span data-ttu-id="e7c7f-138">Cliquez sur le nombre de tooget vignette hello d’URL spécifiques.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-138">Click on hello tile tooget counts for specific URLs.</span></span>

### <a name="average-response-time"></a><span data-ttu-id="e7c7f-139">Temps de réponse moyen</span><span class="sxs-lookup"><span data-stu-id="e7c7f-139">Average response time</span></span>
<span data-ttu-id="e7c7f-140">Mesure le temps hello entre une demande web entrant dans votre réponse d’application et hello qui est retourné.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-140">Measures hello time between a web request entering your application and hello response being returned.</span></span>

<span data-ttu-id="e7c7f-141">points de Hello indiquent le déplacement d’une moyenne.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-141">hello points show a moving average.</span></span> <span data-ttu-id="e7c7f-142">S’il existe un grand nombre de requêtes, il peut certaines écarter moyenne hello sans un pic évident ou plonger dans le graphique de hello.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-142">If there are a lot of requests, there might be some that deviate from hello average without an obvious peak or dip in hello graph.</span></span>

<span data-ttu-id="e7c7f-143">Recherchez les pics inhabituels.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-143">Look for unusual peaks.</span></span> <span data-ttu-id="e7c7f-144">En règle générale, vous attendre toorise de temps de réponse avec une augmentation des demandes.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-144">In general, expect response time toorise with a rise in requests.</span></span> <span data-ttu-id="e7c7f-145">Si l’augmentation de hello est disproportionnée, votre application peut être en appuyant sur une limite de ressource telles que de la capacité d’UC ou de hello d’un service, qu'il utilise.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-145">If hello rise is disproportionate, your app might be hitting a resource limit such as CPU or hello capacity of a service it uses.</span></span>

<span data-ttu-id="e7c7f-146">Cliquez sur heures de tooget hello vignette d’URL spécifiques.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-146">Click hello tile tooget times for specific URLs.</span></span>

![](./media/app-insights-web-monitor-performance/appinsights-42reqs.png)

### <a name="slowest-requests"></a><span data-ttu-id="e7c7f-147">Demandes les plus lentes</span><span class="sxs-lookup"><span data-stu-id="e7c7f-147">Slowest requests</span></span>
![](./media/app-insights-web-monitor-performance/appinsights-44slowest.png)

<span data-ttu-id="e7c7f-148">Indique les demandes dont les performances doivent probablement être améliorées.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-148">Shows which requests might need performance tuning.</span></span>

### <a name="failed-requests"></a><span data-ttu-id="e7c7f-149">Demandes ayant échoué</span><span class="sxs-lookup"><span data-stu-id="e7c7f-149">Failed requests</span></span>
![](./media/app-insights-web-monitor-performance/appinsights-46failed.png)

<span data-ttu-id="e7c7f-150">Décompte des demandes qui ont généré des exceptions non interceptées.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-150">A count of requests that threw uncaught exceptions.</span></span>

<span data-ttu-id="e7c7f-151">Cliquez sur hello vignette toosee hello détails des erreurs spécifiques, puis sélectionnez un toosee demande individuelle ses détails.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-151">Click hello tile toosee hello details of specific failures, and select an individual request toosee its detail.</span></span> 

<span data-ttu-id="e7c7f-152">Seul un échantillon représentatif des échecs est prélevé pour chaque inspection individuelle.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-152">Only a representative sample of failures is retained for individual inspection.</span></span>

### <a name="other-metrics"></a><span data-ttu-id="e7c7f-153">Autres métriques</span><span class="sxs-lookup"><span data-stu-id="e7c7f-153">Other metrics</span></span>
<span data-ttu-id="e7c7f-154">toosee les autres métriques que vous pouvez afficher et cliquez sur un graphique, puis désélectionnez hello métriques toosee hello disponible définis.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-154">toosee what other metrics you can display, click a graph, and then deselect all hello metrics toosee hello full available set.</span></span> <span data-ttu-id="e7c7f-155">Cliquez sur (i) toosee les définition de chaque mesure.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-155">Click (i) toosee each metric's definition.</span></span>

![Désélectionnez l’option jeu toutes les métriques toosee hello entier](./media/app-insights-web-monitor-performance/appinsights-62allchoices.png)

<span data-ttu-id="e7c7f-157">En sélectionnant les hello métrique désactive d’autres qui ne peut pas apparaître sur hello même graphique.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-157">Selecting any metric disables hello others that can't appear on hello same chart.</span></span>

## <a name="set-alerts"></a><span data-ttu-id="e7c7f-158">Définir des alertes</span><span class="sxs-lookup"><span data-stu-id="e7c7f-158">Set alerts</span></span>
<span data-ttu-id="e7c7f-159">toobe informé par courrier électronique de valeurs inhabituelles de toute mesure, ajouter une alerte.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-159">toobe notified by email of unusual values of any metric, add an alert.</span></span> <span data-ttu-id="e7c7f-160">Vous pouvez choisir des administrateurs de comptes toohello toosend hello par courrier électronique, ou d’adresses de messagerie toospecific.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-160">You can choose either toosend hello email toohello account administrators, or toospecific email addresses.</span></span>

![](./media/app-insights-web-monitor-performance/appinsights-413setMetricAlert.png)

<span data-ttu-id="e7c7f-161">Ressource hello hello avant de définir d’autres propriétés.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-161">Set hello resource before hello other properties.</span></span> <span data-ttu-id="e7c7f-162">Ne choisissez pas les ressources de test Web hello si vous souhaitez que les alertes tooset sur les performances ou métriques d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-162">Don't choose hello webtest resources if you want tooset alerts on performance or usage metrics.</span></span>

<span data-ttu-id="e7c7f-163">Être prudent toonote unités de hello dans lequel vous êtes invité à valeur de seuil tooenter hello.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-163">Be careful toonote hello units in which you're asked tooenter hello threshold value.</span></span>

<span data-ttu-id="e7c7f-164">*Je ne vois pas bouton alerte de hello ajouter.*</span><span class="sxs-lookup"><span data-stu-id="e7c7f-164">*I don't see hello Add Alert button.*</span></span> <span data-ttu-id="e7c7f-165">-S’agit-il d’un toowhich de compte de groupe vous avez accès en lecture seule ?</span><span class="sxs-lookup"><span data-stu-id="e7c7f-165">- Is this a group account toowhich you have read-only access?</span></span> <span data-ttu-id="e7c7f-166">Consultez l’administrateur de compte hello.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-166">Check with hello account administrator.</span></span>

## <span data-ttu-id="e7c7f-167"><a name="diagnosis"></a>Problèmes de diagnostic</span><span class="sxs-lookup"><span data-stu-id="e7c7f-167"><a name="diagnosis"></a>Diagnosing issues</span></span>
<span data-ttu-id="e7c7f-168">Voici quelques conseils pour identifier et diagnostiquer les problèmes de performances :</span><span class="sxs-lookup"><span data-stu-id="e7c7f-168">Here are a few tips for finding and diagnosing performance issues:</span></span>

* <span data-ttu-id="e7c7f-169">Configurer [tests web] [ availability] toobe averti si votre site web tombe en panne ou répond lentement ou de façon incorrecte.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-169">Set up [web tests][availability] toobe alerted if your web site goes down or responds incorrectly or slowly.</span></span> 
* <span data-ttu-id="e7c7f-170">Comparer le nombre de demandes hello avec d’autres toosee de métriques si les échecs ou les temps de réponse sont tooload connexe.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-170">Compare hello Request count with other metrics toosee if failures or slow response are related tooload.</span></span>
* <span data-ttu-id="e7c7f-171">[Insérer et rechercher les instructions de trace] [ diagnostic] dans votre code toohelp identifie les problèmes.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-171">[Insert and search trace statements][diagnostic] in your code toohelp pinpoint problems.</span></span>
* <span data-ttu-id="e7c7f-172">Surveillez votre application Web en cours avec le [Flux de métriques temps réel][livestream].</span><span class="sxs-lookup"><span data-stu-id="e7c7f-172">Monitor your Web app in operation with [Live Metrics Stream][livestream].</span></span>
* <span data-ttu-id="e7c7f-173">Capturer l’état hello de votre application .net avec [instantané débogueur][snapshot].</span><span class="sxs-lookup"><span data-stu-id="e7c7f-173">Capture hello state of your .Net application with [Snapshot Debugger][snapshot].</span></span>

## <a name="find-and-fix-performance-bottlenecks-with-an-interactive-performance-investigation"></a><span data-ttu-id="e7c7f-174">Rechercher et corriger les goulots d’étranglement avec une analyse de performances interactive</span><span class="sxs-lookup"><span data-stu-id="e7c7f-174">Find and fix performance bottlenecks with an interactive performance investigation</span></span>

<span data-ttu-id="e7c7f-175">Vous pouvez utiliser hello nouvelle Application Insights interactif enquête toolocate domaines de performances de votre application Web qui ralentissent les performances globales.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-175">You can use hello new Application Insights interactive performance investigation toolocate areas of your Web app that are slowing down overall performance.</span></span> <span data-ttu-id="e7c7f-176">Vous pouvez rapidement rechercher des pages spécifiques qui sont ralentir et utilisent hello [outil de profilage](app-insights-profiler.md) toosee s’il existe une corrélation entre ces pages.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-176">You can quickly find specific pages that are slowing down, and use hello [Profiling tool](app-insights-profiler.md) toosee if there is a correlation between these pages.</span></span>

### <a name="create-a-list-of-slow-performing-pages"></a><span data-ttu-id="e7c7f-177">Créer la liste des pages lentes</span><span class="sxs-lookup"><span data-stu-id="e7c7f-177">Create a list of slow performing pages</span></span> 

<span data-ttu-id="e7c7f-178">première étape de Hello pour détecter les problèmes de performances est tooget une liste de hello lente à répondre de pages.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-178">hello first step for finding performance issues is tooget a list of hello slow responding pages.</span></span> <span data-ttu-id="e7c7f-179">Hello capture d’écran ci-dessous illustre l’utilisation de hello performances panneau tooget une liste de potentiels tooinvestigate pages supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-179">hello screen shot below demonstrates using hello Performance blade tooget a list of potential pages tooinvestigate further.</span></span> <span data-ttu-id="e7c7f-180">Vous pouvez rapidement voir à partir de cette page qu’il a été un ralentissement hello temps de réponse de l’application hello à environ 6 h 00 et à nouveau à environ 10 PM.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-180">You can quickly see from this page that there was a slow-down in hello response time of hello app at approximately 6:00 PM and again at approximately 10 PM.</span></span> <span data-ttu-id="e7c7f-181">Vous pouvez également voir que l’opération de client/détails hello GET a rencontré quelques opérations longues avec un temps de réponse médian de 507.05 millisecondes.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-181">You can also see that hello GET customer/details operation had some long running operations with a median response time of 507.05 milliseconds.</span></span> 

![Performances interactives d’Application Insights](./media/app-insights-web-monitor-performance/performance1.png)

### <a name="drill-down-on-specific-pages"></a><span data-ttu-id="e7c7f-183">Examen approfondi de pages</span><span class="sxs-lookup"><span data-stu-id="e7c7f-183">Drill down on specific pages</span></span>

<span data-ttu-id="e7c7f-184">Dès que vous avez un instantané des performances de votre application, vous pouvez obtenir plus d’informations sur les certaines opérations lentes.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-184">Once you have a snapshot of your app's performance, you can get more details on specific slow-performing operations.</span></span> <span data-ttu-id="e7c7f-185">Cliquez sur une quelconque opération hello liste toosee hello détails comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-185">Click on any operation in hello list toosee hello details as shown below.</span></span> <span data-ttu-id="e7c7f-186">Graphique de hello, vous pouvez voir si les performances de hello était basée sur une dépendance.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-186">From hello chart you can see if hello performance was based on a dependency.</span></span> <span data-ttu-id="e7c7f-187">Vous pouvez également voir combien hello expérimentés d’utilisateurs différents temps de réponse.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-187">You can also see how many users experienced hello various response times.</span></span> 

![Panneau des opérations d’Application Insights](./media/app-insights-web-monitor-performance/performance5.png)

### <a name="drill-down-on-a-specific-time-period"></a><span data-ttu-id="e7c7f-189">Examen approfondi d’une période</span><span class="sxs-lookup"><span data-stu-id="e7c7f-189">Drill down on a specific time period</span></span>

<span data-ttu-id="e7c7f-190">Après avoir identifié une limite dans le temps tooinvestigate, descendez encore plu toolook à des opérations spécifiques hello ayant pu causer un ralentissement des performances hello.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-190">After you have identified a point in time tooinvestigate, drill down even further toolook at hello specific operations that might have caused hello performance slow-down.</span></span> <span data-ttu-id="e7c7f-191">Lorsque vous cliquez sur un point spécifique dans le temps vous obtenez les détails de hello de page hello comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-191">When you click on a specific point in time you get hello details of hello page as shown below.</span></span> <span data-ttu-id="e7c7f-192">Bonjour exemple ci-dessous, vous pouvez voir les opérations hello répertoriées pour une période donnée, ainsi que les codes de réponse du serveur hello et la durée d’une opération hello.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-192">In hello example below you can see hello operations listed for a given time period along with hello server response codes and hello operation duration.</span></span> <span data-ttu-id="e7c7f-193">Vous avez également hello url pour l’ouverture d’un élément de travail TFS si vous avez besoin toosend cette équipe de développement tooyour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-193">You also have hello url for opening a TFS work item if you need toosend this information tooyour development team.</span></span>

![Tranche horaire d’Application Insights](./media/app-insights-web-monitor-performance/performance2.png)

### <a name="drill-down-on-a-specific-operation"></a><span data-ttu-id="e7c7f-195">Examen approfondi d’une opération</span><span class="sxs-lookup"><span data-stu-id="e7c7f-195">Drill down on a specific operation</span></span>

<span data-ttu-id="e7c7f-196">Après avoir identifié une limite dans le temps tooinvestigate, descendez encore plu toolook à des opérations spécifiques hello ayant pu causer un ralentissement des performances hello.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-196">After you have identified a point in time tooinvestigate, drill down even further toolook at hello specific operations that might have caused hello performance slow-down.</span></span> <span data-ttu-id="e7c7f-197">Cliquez sur une opération de hello répertorier toosee hello les détails de l’opération hello comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-197">Click on an operation from hello list toosee hello details of hello operation as shown below.</span></span> <span data-ttu-id="e7c7f-198">Dans cet exemple, que vous pouvez voir que hello opération a échoué, et Application Insights a fourni les informations de hello Hello a généré l’application de hello d’exception.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-198">In this example you can see that hello operation failed, and Application Insights has provided hello details of hello exception hello application threw.</span></span> <span data-ttu-id="e7c7f-199">Là encore, vous pouvez facilement créer un élément de travail TFS à partir de ce panneau.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-199">Again, you can easily create a TFS work item from this blade.</span></span>

![Panneau des opérations d’Application Insights](./media/app-insights-web-monitor-performance/performance3.png)


## <span data-ttu-id="e7c7f-201"><a name="next"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e7c7f-201"><a name="next"></a>Next steps</span></span>
<span data-ttu-id="e7c7f-202">[Tests Web] [ availability] -demandes web ont envoyés tooyour application à intervalles réguliers à partir de monde hello.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-202">[Web tests][availability] - Have web requests sent tooyour application at regular intervals from around hello world.</span></span>

<span data-ttu-id="e7c7f-203">[Capturer et rechercher les traces de diagnostic] [ diagnostic] - insérer le suivi des appels et passer en revue les problèmes de toopinpoint résultats hello.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-203">[Capture and search diagnostic traces][diagnostic] - Insert trace calls and sift through hello results toopinpoint issues.</span></span>

<span data-ttu-id="e7c7f-204">[Suivi de l’utilisation][usage] : découvrez comment ce que les utilisateurs font avec votre application.</span><span class="sxs-lookup"><span data-stu-id="e7c7f-204">[Usage tracking][usage] - Find out how people use your application.</span></span>

<span data-ttu-id="e7c7f-205">[Résolution des problèmes][qna] et Questions et réponses</span><span class="sxs-lookup"><span data-stu-id="e7c7f-205">[Troubleshooting][qna] - and Q & A</span></span>



<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
[usage]: app-insights-web-track-usage.md
[livestream]: app-insights-live-stream.md
[snapshot]: app-insights-snapshot-debugger.md



