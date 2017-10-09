---
title: aaaHow faire... dans Azure Application Insights | Documents Microsoft
description: FAQ dans Application Insights
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 48b2b644-92e4-44c3-bc14-068f1bbedd22
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: bwren
ms.openlocfilehash: 89294c3583b7c4e7998143be6d359f2deb3c8f49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-do-i--in-application-insights"></a><span data-ttu-id="37eb9-103">Comment ... dans Application Insights ?</span><span class="sxs-lookup"><span data-stu-id="37eb9-103">How do I ... in Application Insights?</span></span>
## <a name="get-an-email-when-"></a><span data-ttu-id="37eb9-104">Recevoir un message électronique quand...</span><span class="sxs-lookup"><span data-stu-id="37eb9-104">Get an email when ...</span></span>
### <a name="email-if-my-site-goes-down"></a><span data-ttu-id="37eb9-105">Envoyer un message électronique si mon site tombe en panne</span><span class="sxs-lookup"><span data-stu-id="37eb9-105">Email if my site goes down</span></span>
<span data-ttu-id="37eb9-106">Définissez un [test web de disponibilité](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="37eb9-106">Set an [availability web test](app-insights-monitor-web-app-availability.md).</span></span>

### <a name="email-if-my-site-is-overloaded"></a><span data-ttu-id="37eb9-107">Envoyer un message électronique si mon site est surchargé</span><span class="sxs-lookup"><span data-stu-id="37eb9-107">Email if my site is overloaded</span></span>
<span data-ttu-id="37eb9-108">Définissez une [alerte](app-insights-alerts.md) sur le **Temps de réponse du serveur**.</span><span class="sxs-lookup"><span data-stu-id="37eb9-108">Set an [alert](app-insights-alerts.md) on **Server response time**.</span></span> <span data-ttu-id="37eb9-109">Un seuil compris entre 1 et 2 secondes doit fonctionner.</span><span class="sxs-lookup"><span data-stu-id="37eb9-109">A threshold between 1 and 2 seconds should work.</span></span>

![](./media/app-insights-how-do-i/030-server.png)

<span data-ttu-id="37eb9-110">Votre application peut également indiquer des signes de surcharge en retournant des codes d’erreur.</span><span class="sxs-lookup"><span data-stu-id="37eb9-110">Your app might also show signs of strain by returning failure codes.</span></span> <span data-ttu-id="37eb9-111">Définissez une alerte sur les **Demandes ayant échoué**.</span><span class="sxs-lookup"><span data-stu-id="37eb9-111">Set an alert on **Failed requests**.</span></span>

<span data-ttu-id="37eb9-112">Si vous souhaitez tooset une alerte sur **exceptions du serveur**, vous pouvez avoir toodo [une installation supplémentaire](app-insights-asp-net-exceptions.md) données de commandes toosee.</span><span class="sxs-lookup"><span data-stu-id="37eb9-112">If you want tooset an alert on **Server exceptions**, you might have toodo [some additional setup](app-insights-asp-net-exceptions.md) in order toosee data.</span></span>

### <a name="email-on-exceptions"></a><span data-ttu-id="37eb9-113">Envoyer un message électronique en cas d’exceptions</span><span class="sxs-lookup"><span data-stu-id="37eb9-113">Email on exceptions</span></span>
1. [<span data-ttu-id="37eb9-114">Configurer la surveillance des exceptions</span><span class="sxs-lookup"><span data-stu-id="37eb9-114">Set up exception monitoring</span></span>](app-insights-asp-net-exceptions.md)
2. <span data-ttu-id="37eb9-115">[Définir une alerte](app-insights-alerts.md) sur hello Exception compter métrique</span><span class="sxs-lookup"><span data-stu-id="37eb9-115">[Set an alert](app-insights-alerts.md) on hello Exception count metric</span></span>

### <a name="email-on-an-event-in-my-app"></a><span data-ttu-id="37eb9-116">Envoyer un message électronique en réponse à un événement dans mon application</span><span class="sxs-lookup"><span data-stu-id="37eb9-116">Email on an event in my app</span></span>
<span data-ttu-id="37eb9-117">Supposons que vous aimeriez tooget un message électronique lorsqu’un événement spécifique se produit.</span><span class="sxs-lookup"><span data-stu-id="37eb9-117">Let's suppose you'd like tooget an email when a specific event occurs.</span></span> <span data-ttu-id="37eb9-118">Application Insights ne fournit pas directement cette fonctionnalité, mais peut [envoyer une alerte quand une métrique dépasse un seuil](app-insights-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="37eb9-118">Application Insights doesn't provide this facility directly, but it can [send an alert when a metric crosses a threshold](app-insights-alerts.md).</span></span>

<span data-ttu-id="37eb9-119">Les alertes peuvent être définies sur des [métriques personnalisées](app-insights-api-custom-events-metrics.md#trackmetric), et non sur des événements personnalisés.</span><span class="sxs-lookup"><span data-stu-id="37eb9-119">Alerts can be set on [custom metrics](app-insights-api-custom-events-metrics.md#trackmetric), though not custom events.</span></span> <span data-ttu-id="37eb9-120">Écrire certaines tooincrease code une métrique lorsque hello événement se produit :</span><span class="sxs-lookup"><span data-stu-id="37eb9-120">Write some code tooincrease a metric when hello event occurs:</span></span>

    telemetry.TrackMetric("Alarm", 10);

<span data-ttu-id="37eb9-121">ou :</span><span class="sxs-lookup"><span data-stu-id="37eb9-121">or:</span></span>

    var measurements = new Dictionary<string,double>();
    measurements ["Alarm"] = 10;
    telemetry.TrackEvent("status", null, measurements);

<span data-ttu-id="37eb9-122">Étant donné que les alertes ont deux États, vous avez toosend une valeur faible lorsque vous envisagez d’alerte hello toohave s’est terminée :</span><span class="sxs-lookup"><span data-stu-id="37eb9-122">Because alerts have two states, you have toosend a low value when you consider hello alert toohave ended:</span></span>

    telemetry.TrackMetric("Alarm", 0.5);

<span data-ttu-id="37eb9-123">Créer un graphique dans [explorer métrique](app-insights-metrics-explorer.md) toosee votre alarme :</span><span class="sxs-lookup"><span data-stu-id="37eb9-123">Create a chart in [metric explorer](app-insights-metrics-explorer.md) toosee your alarm:</span></span>

![](./media/app-insights-how-do-i/010-alarm.png)

<span data-ttu-id="37eb9-124">Maintenant définir une alerte toofire lors de la métrique de hello dépasse une valeur moyenne pendant une courte période :</span><span class="sxs-lookup"><span data-stu-id="37eb9-124">Now set an alert toofire when hello metric goes above a mid value for a short period:</span></span>

![](./media/app-insights-how-do-i/020-threshold.png)

<span data-ttu-id="37eb9-125">Définissez hello moyenne toohello période minimum.</span><span class="sxs-lookup"><span data-stu-id="37eb9-125">Set hello averaging period toohello minimum.</span></span>

<span data-ttu-id="37eb9-126">Vous allez recevoir des messages électroniques lorsque la métrique de hello passe au-dessus et sous le seuil de hello.</span><span class="sxs-lookup"><span data-stu-id="37eb9-126">You'll get emails both when hello metric goes above and below hello threshold.</span></span>

<span data-ttu-id="37eb9-127">Certains tooconsider points :</span><span class="sxs-lookup"><span data-stu-id="37eb9-127">Some points tooconsider:</span></span>

* <span data-ttu-id="37eb9-128">Une alerte possède deux états (« alerte » et « intègre »).</span><span class="sxs-lookup"><span data-stu-id="37eb9-128">An alert has two states ("alert" and "healthy").</span></span> <span data-ttu-id="37eb9-129">état de Hello est évalué uniquement lorsqu’une mesure est reçue.</span><span class="sxs-lookup"><span data-stu-id="37eb9-129">hello state is evaluated only when a metric is received.</span></span>
* <span data-ttu-id="37eb9-130">Un message électronique est envoyé uniquement lorsque l’état hello change.</span><span class="sxs-lookup"><span data-stu-id="37eb9-130">An email is sent only when hello state changes.</span></span> <span data-ttu-id="37eb9-131">C’est pourquoi vous avez toosend haute et faible valeur métriques.</span><span class="sxs-lookup"><span data-stu-id="37eb9-131">This is why you have toosend both high and low-value metrics.</span></span>
* <span data-ttu-id="37eb9-132">alerte de hello tooevaluate, moyenne de hello est repris des valeurs de salutation reçue hello précédant la période.</span><span class="sxs-lookup"><span data-stu-id="37eb9-132">tooevaluate hello alert, hello average is taken of hello received values over hello preceding period.</span></span> <span data-ttu-id="37eb9-133">Cela se produit chaque fois qu’une mesure est reçue, les messages électroniques peuvent être envoyées plus fréquemment que la période de hello que vous définissez.</span><span class="sxs-lookup"><span data-stu-id="37eb9-133">This occurs every time a metric is received, so emails can be sent more frequently than hello period you set.</span></span>
* <span data-ttu-id="37eb9-134">Étant donné que les messages électroniques sont envoyés à la fois « alerte » et « sain », vous pourriez tooconsider nouveau considérant votre événement Shot comme une condition de deux États.</span><span class="sxs-lookup"><span data-stu-id="37eb9-134">Since emails are sent both on "alert" and "healthy", you might want tooconsider re-thinking your one-shot event as a two-state condition.</span></span> <span data-ttu-id="37eb9-135">Par exemple, au lieu d’un événement « terminée », ont une condition « tâche en cours d’exécution », où vous obtenez des messages électroniques au début de hello et de fin d’une tâche.</span><span class="sxs-lookup"><span data-stu-id="37eb9-135">For example, instead of a "job completed" event, have a "job in progress" condition, where you get emails at hello start and end of a job.</span></span>

### <a name="set-up-alerts-automatically"></a><span data-ttu-id="37eb9-136">Configurer automatiquement des alertes</span><span class="sxs-lookup"><span data-stu-id="37eb9-136">Set up alerts automatically</span></span>
[<span data-ttu-id="37eb9-137">Utilisez PowerShell toocreate nouvelles alertes</span><span class="sxs-lookup"><span data-stu-id="37eb9-137">Use PowerShell toocreate new alerts</span></span>](app-insights-alerts.md#automation)

## <a name="use-powershell-toomanage-application-insights"></a><span data-ttu-id="37eb9-138">Utilisez PowerShell tooManage Application Insights</span><span class="sxs-lookup"><span data-stu-id="37eb9-138">Use PowerShell tooManage Application Insights</span></span>
* [<span data-ttu-id="37eb9-139">Créer des ressources</span><span class="sxs-lookup"><span data-stu-id="37eb9-139">Create new resources</span></span>](app-insights-powershell-script-create-resource.md)
* [<span data-ttu-id="37eb9-140">Créer des alertes</span><span class="sxs-lookup"><span data-stu-id="37eb9-140">Create new alerts</span></span>](app-insights-alerts.md#automation)

## <a name="separate-telemetry-from-different-versions"></a><span data-ttu-id="37eb9-141">Télémétrie distincte des différentes versions</span><span class="sxs-lookup"><span data-stu-id="37eb9-141">Separate telemetry from different versions</span></span>

* <span data-ttu-id="37eb9-142">Plusieurs rôles dans une application : utiliser une seule ressource Application Insights et filtrez sur cloud_Rolename.</span><span class="sxs-lookup"><span data-stu-id="37eb9-142">Multiple roles in an app: Use a single Application Insights resource, and filter on cloud_Rolename.</span></span> [<span data-ttu-id="37eb9-143">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="37eb9-143">Learn more</span></span>](app-insights-monitor-multi-role-apps.md)
* <span data-ttu-id="37eb9-144">Séparation des versions de développement, de test et de publication : utiliser différentes ressources d’Application Insights.</span><span class="sxs-lookup"><span data-stu-id="37eb9-144">Separating development, test, and release versions: Use different Application Insights resources.</span></span> <span data-ttu-id="37eb9-145">Sélectionnez des clés d’instrumentation hello à partir de web.config. [En savoir plus](app-insights-separate-resources.md)</span><span class="sxs-lookup"><span data-stu-id="37eb9-145">Pick up hello instrumentation keys from web.config. [Learn more](app-insights-separate-resources.md)</span></span>
* <span data-ttu-id="37eb9-146">Génération de rapports sur les versions : ajouter une propriété à l’aide d’un initialiseur de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="37eb9-146">Reporting build versions: Add a property using a telemetry initializer.</span></span> [<span data-ttu-id="37eb9-147">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="37eb9-147">Learn more</span></span>](app-insights-separate-resources.md)

## <a name="monitor-backend-servers-and-desktop-apps"></a><span data-ttu-id="37eb9-148">Surveiller les serveurs principaux et les applications de bureau</span><span class="sxs-lookup"><span data-stu-id="37eb9-148">Monitor backend servers and desktop apps</span></span>
<span data-ttu-id="37eb9-149">[Utiliser le module hello SDK Windows Server](app-insights-windows-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="37eb9-149">[Use hello Windows Server SDK module](app-insights-windows-desktop.md).</span></span>

## <a name="visualize-data"></a><span data-ttu-id="37eb9-150">Visualiser les données</span><span class="sxs-lookup"><span data-stu-id="37eb9-150">Visualize data</span></span>
#### <a name="dashboard-with-metrics-from-multiple-apps"></a><span data-ttu-id="37eb9-151">Tableau de bord avec des métriques de plusieurs applications</span><span class="sxs-lookup"><span data-stu-id="37eb9-151">Dashboard with metrics from multiple apps</span></span>
* <span data-ttu-id="37eb9-152">Dans [Metrics Explorer](app-insights-metrics-explorer.md), personnalisez votre graphique et enregistrez-le en tant que favori.</span><span class="sxs-lookup"><span data-stu-id="37eb9-152">In [Metric Explorer](app-insights-metrics-explorer.md), customize your chart and save it as a favorite.</span></span> <span data-ttu-id="37eb9-153">Épingler toohello tableau de bord Azure.</span><span class="sxs-lookup"><span data-stu-id="37eb9-153">Pin it toohello Azure dashboard.</span></span>

#### <a name="dashboard-with-data-from-other-sources-and-application-insights"></a><span data-ttu-id="37eb9-154">Tableau de bord avec des données provenant d’autres sources et d’Application Insights</span><span class="sxs-lookup"><span data-stu-id="37eb9-154">Dashboard with data from other sources and Application Insights</span></span>
* <span data-ttu-id="37eb9-155">[Exporter les données de télémétrie tooPower BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="37eb9-155">[Export telemetry tooPower BI](app-insights-export-power-bi.md).</span></span>

<span data-ttu-id="37eb9-156">Ou</span><span class="sxs-lookup"><span data-stu-id="37eb9-156">Or</span></span>

* <span data-ttu-id="37eb9-157">Utilisez SharePoint comme tableau de bord, pour afficher les données des composants WebPart de SharePoint.</span><span class="sxs-lookup"><span data-stu-id="37eb9-157">Use SharePoint as your dashboard, displaying data in SharePoint web parts.</span></span> <span data-ttu-id="37eb9-158">[Utiliser l’exportation continue et flux de données Analytique tooexport tooSQL](app-insights-code-sample-export-sql-stream-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="37eb9-158">[Use continuous export and Stream Analytics tooexport tooSQL](app-insights-code-sample-export-sql-stream-analytics.md).</span></span>  <span data-ttu-id="37eb9-159">Utiliser la base de données PowerView tooexamine hello et créer un composant WebPart SharePoint pour PowerView.</span><span class="sxs-lookup"><span data-stu-id="37eb9-159">Use PowerView tooexamine hello database, and create a SharePoint web part for PowerView.</span></span>

<a name="search-specific-users"></a>

### <a name="filter-out-anonymous-or-authenticated-users"></a><span data-ttu-id="37eb9-160">Filtrer les utilisateurs authentifiés ou anonymes</span><span class="sxs-lookup"><span data-stu-id="37eb9-160">Filter out anonymous or authenticated users</span></span>
<span data-ttu-id="37eb9-161">Si vos utilisateurs se connectent, vous pouvez définir hello [id de l’utilisateur authentifié](app-insights-api-custom-events-metrics.md#authenticated-users). (Cela n’est pas automatique.)</span><span class="sxs-lookup"><span data-stu-id="37eb9-161">If your users sign in, you can set hello [authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users). (It doesn't happen automatically.)</span></span>

<span data-ttu-id="37eb9-162">Vous pouvez ensuite effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="37eb9-162">You can then:</span></span>

* <span data-ttu-id="37eb9-163">Rechercher des ID d’utilisateur spécifiques</span><span class="sxs-lookup"><span data-stu-id="37eb9-163">Search on specific user ids</span></span>

![](./media/app-insights-how-do-i/110-search.png)

* <span data-ttu-id="37eb9-164">Filtrer les utilisateurs anonymes ou authentifiés du tooeither métriques</span><span class="sxs-lookup"><span data-stu-id="37eb9-164">Filter metrics tooeither anonymous or authenticated users</span></span>

![](./media/app-insights-how-do-i/115-metrics.png)

## <a name="modify-property-names-or-values"></a><span data-ttu-id="37eb9-165">Modification de noms ou de valeurs de propriété</span><span class="sxs-lookup"><span data-stu-id="37eb9-165">Modify property names or values</span></span>
<span data-ttu-id="37eb9-166">Créez un [filtre](app-insights-api-filtering-sampling.md#filtering).</span><span class="sxs-lookup"><span data-stu-id="37eb9-166">Create a [filter](app-insights-api-filtering-sampling.md#filtering).</span></span> <span data-ttu-id="37eb9-167">Cela vous permet de modifier ou de filtrer les données de télémétrie avant d’être envoyée à partir de votre tooApplication application Insights.</span><span class="sxs-lookup"><span data-stu-id="37eb9-167">This lets you modify or filter telemetry before it is sent from your app tooApplication Insights.</span></span>

## <a name="list-specific-users-and-their-usage"></a><span data-ttu-id="37eb9-168">Répertorier les utilisateurs spécifiques et leur utilisation</span><span class="sxs-lookup"><span data-stu-id="37eb9-168">List specific users and their usage</span></span>
<span data-ttu-id="37eb9-169">Si vous souhaitez simplement trop[recherche pour des utilisateurs spécifiques](#search-specific-users), vous pouvez définir hello [id de l’utilisateur authentifié](app-insights-api-custom-events-metrics.md#authenticated-users).</span><span class="sxs-lookup"><span data-stu-id="37eb9-169">If you just want too[search for specific users](#search-specific-users), you can set hello [authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users).</span></span>

<span data-ttu-id="37eb9-170">Si vous voulez une liste des utilisateurs avec des données telles que les pages qu’ils ont consultées ou leur fréquence de connexion, deux options s’offrent à vous :</span><span class="sxs-lookup"><span data-stu-id="37eb9-170">If you want a list of users with data such as what pages they look at or how often they log in, you have two options:</span></span>

* <span data-ttu-id="37eb9-171">[Id de l’utilisateur authentifié ensemble](app-insights-api-custom-events-metrics.md#authenticated-users), [exporter la base de données tooa](app-insights-code-sample-export-sql-stream-analytics.md) et utilisation appropriée des outils tooanalyze vos données utilisateur.</span><span class="sxs-lookup"><span data-stu-id="37eb9-171">[Set authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users), [export tooa database](app-insights-code-sample-export-sql-stream-analytics.md) and use suitable tools tooanalyze your user data there.</span></span>
* <span data-ttu-id="37eb9-172">Si vous avez uniquement un petit nombre d’utilisateurs, envoyer des événements personnalisés ou des mesures, à l’aide de données hello d’intérêt que hello valeur métrique ou nom de l’événement et id d’utilisateur paramètre hello en tant que propriété.</span><span class="sxs-lookup"><span data-stu-id="37eb9-172">If you have only a small number of users, send custom events or metrics, using hello data of interest as hello metric value or event name, and setting hello user id as a property.</span></span> <span data-ttu-id="37eb9-173">tooanalyze des vues de page, remplacez l’appel trackPageView JavaScript standard de hello.</span><span class="sxs-lookup"><span data-stu-id="37eb9-173">tooanalyze page views, replace hello standard JavaScript trackPageView call.</span></span> <span data-ttu-id="37eb9-174">données de télémétrie tooanalyze côté serveur, utilisez une télémétrie initialiseur tooadd hello id tooall server télémétrie d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="37eb9-174">tooanalyze server-side telemetry, use a telemetry initializer tooadd hello user id tooall server telemetry.</span></span> <span data-ttu-id="37eb9-175">Vous pouvez ensuite les métriques de filtre et de segment et les recherches sur les id d’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="37eb9-175">You can then filter and segment metrics and searches on hello user id.</span></span>

## <a name="reduce-traffic-from-my-app-tooapplication-insights"></a><span data-ttu-id="37eb9-176">Réduire le trafic à partir de mon tooApplication application Insights</span><span class="sxs-lookup"><span data-stu-id="37eb9-176">Reduce traffic from my app tooApplication Insights</span></span>
* <span data-ttu-id="37eb9-177">Dans [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), désactivez tous les modules que vous n’avez pas besoin, ce collecteur hello du compteur de performance.</span><span class="sxs-lookup"><span data-stu-id="37eb9-177">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), disable any modules you don't need, such hello performance counter collector.</span></span>
* <span data-ttu-id="37eb9-178">Utilisez [d’échantillonnage et le filtrage](app-insights-api-filtering-sampling.md) à hello SDK.</span><span class="sxs-lookup"><span data-stu-id="37eb9-178">Use [Sampling and filtering](app-insights-api-filtering-sampling.md) at hello SDK.</span></span>
* <span data-ttu-id="37eb9-179">Dans vos pages web, limitez le nombre de hello des appels Ajax signalé pour chaque vue de la page.</span><span class="sxs-lookup"><span data-stu-id="37eb9-179">In your web pages, Limit hello number of Ajax calls reported for every page view.</span></span> <span data-ttu-id="37eb9-180">Dans l’extrait de code hello script après `instrumentationKey:...` , insérer : `,maxAjaxCallsPerView:3` (ou un nombre approprié).</span><span class="sxs-lookup"><span data-stu-id="37eb9-180">In hello script snippet after `instrumentationKey:...` , insert: `,maxAjaxCallsPerView:3` (or a suitable number).</span></span>
* <span data-ttu-id="37eb9-181">Si vous utilisez [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric), agrégat hello de lots de valeurs de mesure de calcul avant d’envoyer le résultat de hello.</span><span class="sxs-lookup"><span data-stu-id="37eb9-181">If you're using [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric), compute hello aggregate of batches of metric values before sending hello result.</span></span> <span data-ttu-id="37eb9-182">Il existe une surcharge de TrackMetric() qui se charge de cette tâche.</span><span class="sxs-lookup"><span data-stu-id="37eb9-182">There's an overload of TrackMetric() that provides for that.</span></span>

<span data-ttu-id="37eb9-183">En savoir plus sur la [tarification et les quotas](app-insights-pricing.md).</span><span class="sxs-lookup"><span data-stu-id="37eb9-183">Learn more about [pricing and quotas](app-insights-pricing.md).</span></span>

## <a name="disable-telemetry"></a><span data-ttu-id="37eb9-184">Désactiver la télémétrie</span><span class="sxs-lookup"><span data-stu-id="37eb9-184">Disable telemetry</span></span>
<span data-ttu-id="37eb9-185">trop**dynamiquement arrêter et démarrer** hello collecte et transmission des données de télémétrie à partir du serveur de hello :</span><span class="sxs-lookup"><span data-stu-id="37eb9-185">too**dynamically stop and start** hello collection and transmission of telemetry from hello server:</span></span>

```

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```



<span data-ttu-id="37eb9-186">trop**désactiver les collecteurs standards sélectionnés** - par exemple, les compteurs de performance, les requêtes HTTP ou les dépendances - supprimez ou commentez les lignes concernées hello [ApplicationInsights.config](app-insights-api-custom-events-metrics.md). Procéder, par exemple, si vous souhaitez toosend vos propres données TrackRequest.</span><span class="sxs-lookup"><span data-stu-id="37eb9-186">too**disable selected standard collectors** - for example, performance counters, HTTP requests, or dependencies - delete or comment out hello relevant lines in [ApplicationInsights.config](app-insights-api-custom-events-metrics.md). You could do this, for example, if you want toosend your own TrackRequest data.</span></span>

## <a name="view-system-performance-counters"></a><span data-ttu-id="37eb9-187">Afficher les compteurs de performances système</span><span class="sxs-lookup"><span data-stu-id="37eb9-187">View system performance counters</span></span>
<span data-ttu-id="37eb9-188">Parmi les hello métriques que vous pouvez afficher dans l’Explorateur de métriques sont un ensemble de compteurs de performances système.</span><span class="sxs-lookup"><span data-stu-id="37eb9-188">Among hello metrics you can show in metrics explorer are a set of system performance counters.</span></span> <span data-ttu-id="37eb9-189">Un panneau prédéfini intitulé **Serveurs** affiche plusieurs d'entre eux.</span><span class="sxs-lookup"><span data-stu-id="37eb9-189">There's a predefined blade titled **Servers** that displays several of them.</span></span>

![Ouvrez votre ressource Application Insights et cliquez sur Serveurs.](./media/app-insights-how-do-i/121-servers.png)

### <a name="if-you-see-no-performance-counter-data"></a><span data-ttu-id="37eb9-191">Si aucune donnée de compteur de performances ne s’affiche</span><span class="sxs-lookup"><span data-stu-id="37eb9-191">If you see no performance counter data</span></span>
* <span data-ttu-id="37eb9-192">**Serveur IIS** sur votre propre ordinateur ou sur une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="37eb9-192">**IIS server** on your own machine or on a VM.</span></span> <span data-ttu-id="37eb9-193">[Installer Status Monitor](app-insights-monitor-performance-live-website-now.md).</span><span class="sxs-lookup"><span data-stu-id="37eb9-193">[Install Status Monitor](app-insights-monitor-performance-live-website-now.md).</span></span>
* <span data-ttu-id="37eb9-194">**Site Web Azure** : nous ne prenons pas encore en charge les compteurs de performances.</span><span class="sxs-lookup"><span data-stu-id="37eb9-194">**Azure web site** - we don't support performance counters yet.</span></span> <span data-ttu-id="37eb9-195">Il existe plusieurs mesures, que vous pouvez obtenir comme une partie standard du Panneau de contrôle de site web Azure hello.</span><span class="sxs-lookup"><span data-stu-id="37eb9-195">There are several metrics you can get as a standard part of hello Azure web site control panel.</span></span>
* <span data-ttu-id="37eb9-196">**Serveur Unix** - [installer collectd](app-insights-java-collectd.md)</span><span class="sxs-lookup"><span data-stu-id="37eb9-196">**Unix server** - [Install collectd](app-insights-java-collectd.md)</span></span>

### <a name="toodisplay-more-performance-counters"></a><span data-ttu-id="37eb9-197">toodisplay des compteurs de performance</span><span class="sxs-lookup"><span data-stu-id="37eb9-197">toodisplay more performance counters</span></span>
* <span data-ttu-id="37eb9-198">Tout d’abord, [ajouter un nouveau graphique](app-insights-metrics-explorer.md) et voyez si hello est Bonjour base ensemble de compteurs que nous proposons.</span><span class="sxs-lookup"><span data-stu-id="37eb9-198">First, [add a new chart](app-insights-metrics-explorer.md) and see if hello counter is in hello basic set that we offer.</span></span>
* <span data-ttu-id="37eb9-199">Si ce n’est pas le cas, [ajouter hello compteur toohello jeu collecté par le module compteur de performances hello](app-insights-performance-counters.md).</span><span class="sxs-lookup"><span data-stu-id="37eb9-199">If not, [add hello counter toohello set collected by hello performance counter module](app-insights-performance-counters.md).</span></span>
