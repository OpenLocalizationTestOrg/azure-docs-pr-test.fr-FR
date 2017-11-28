---
title: "Comment... dans Azure Application Insights | Microsoft Docs"
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
ms.openlocfilehash: ef63e06c0621753e0a706d6efb709b943e38ee42
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="how-do-i--in-application-insights"></a><span data-ttu-id="79109-103">Comment ... dans Application Insights ?</span><span class="sxs-lookup"><span data-stu-id="79109-103">How do I ... in Application Insights?</span></span>
## <a name="get-an-email-when-"></a><span data-ttu-id="79109-104">Recevoir un message électronique quand...</span><span class="sxs-lookup"><span data-stu-id="79109-104">Get an email when ...</span></span>
### <a name="email-if-my-site-goes-down"></a><span data-ttu-id="79109-105">Envoyer un message électronique si mon site tombe en panne</span><span class="sxs-lookup"><span data-stu-id="79109-105">Email if my site goes down</span></span>
<span data-ttu-id="79109-106">Définissez un [test web de disponibilité](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="79109-106">Set an [availability web test](app-insights-monitor-web-app-availability.md).</span></span>

### <a name="email-if-my-site-is-overloaded"></a><span data-ttu-id="79109-107">Envoyer un message électronique si mon site est surchargé</span><span class="sxs-lookup"><span data-stu-id="79109-107">Email if my site is overloaded</span></span>
<span data-ttu-id="79109-108">Définissez une [alerte](app-insights-alerts.md) sur le **Temps de réponse du serveur**.</span><span class="sxs-lookup"><span data-stu-id="79109-108">Set an [alert](app-insights-alerts.md) on **Server response time**.</span></span> <span data-ttu-id="79109-109">Un seuil compris entre 1 et 2 secondes doit fonctionner.</span><span class="sxs-lookup"><span data-stu-id="79109-109">A threshold between 1 and 2 seconds should work.</span></span>

![](./media/app-insights-how-do-i/030-server.png)

<span data-ttu-id="79109-110">Votre application peut également indiquer des signes de surcharge en retournant des codes d’erreur.</span><span class="sxs-lookup"><span data-stu-id="79109-110">Your app might also show signs of strain by returning failure codes.</span></span> <span data-ttu-id="79109-111">Définissez une alerte sur les **Demandes ayant échoué**.</span><span class="sxs-lookup"><span data-stu-id="79109-111">Set an alert on **Failed requests**.</span></span>

<span data-ttu-id="79109-112">Si vous voulez définir une alerte sur les **Exceptions du serveur**, vous devrez peut-être effectuer une [installation supplémentaire](app-insights-asp-net-exceptions.md) pour afficher les données.</span><span class="sxs-lookup"><span data-stu-id="79109-112">If you want to set an alert on **Server exceptions**, you might have to do [some additional setup](app-insights-asp-net-exceptions.md) in order to see data.</span></span>

### <a name="email-on-exceptions"></a><span data-ttu-id="79109-113">Envoyer un message électronique en cas d’exceptions</span><span class="sxs-lookup"><span data-stu-id="79109-113">Email on exceptions</span></span>
1. [<span data-ttu-id="79109-114">Configurer la surveillance des exceptions</span><span class="sxs-lookup"><span data-stu-id="79109-114">Set up exception monitoring</span></span>](app-insights-asp-net-exceptions.md)
2. <span data-ttu-id="79109-115">[Définir une alerte](app-insights-alerts.md) sur la métrique Nombre d’exceptions</span><span class="sxs-lookup"><span data-stu-id="79109-115">[Set an alert](app-insights-alerts.md) on the Exception count metric</span></span>

### <a name="email-on-an-event-in-my-app"></a><span data-ttu-id="79109-116">Envoyer un message électronique en réponse à un événement dans mon application</span><span class="sxs-lookup"><span data-stu-id="79109-116">Email on an event in my app</span></span>
<span data-ttu-id="79109-117">Supposons que vous vouliez recevoir un e-mail quand un événement spécifique se produit.</span><span class="sxs-lookup"><span data-stu-id="79109-117">Let's suppose you'd like to get an email when a specific event occurs.</span></span> <span data-ttu-id="79109-118">Application Insights ne fournit pas directement cette fonctionnalité, mais peut [envoyer une alerte quand une métrique dépasse un seuil](app-insights-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="79109-118">Application Insights doesn't provide this facility directly, but it can [send an alert when a metric crosses a threshold](app-insights-alerts.md).</span></span>

<span data-ttu-id="79109-119">Les alertes peuvent être définies sur des [métriques personnalisées](app-insights-api-custom-events-metrics.md#trackmetric), et non sur des événements personnalisés.</span><span class="sxs-lookup"><span data-stu-id="79109-119">Alerts can be set on [custom metrics](app-insights-api-custom-events-metrics.md#trackmetric), though not custom events.</span></span> <span data-ttu-id="79109-120">Écrivez du code pour augmenter une métrique quand l’événement se produit :</span><span class="sxs-lookup"><span data-stu-id="79109-120">Write some code to increase a metric when the event occurs:</span></span>

    telemetry.TrackMetric("Alarm", 10);

<span data-ttu-id="79109-121">ou :</span><span class="sxs-lookup"><span data-stu-id="79109-121">or:</span></span>

    var measurements = new Dictionary<string,double>();
    measurements ["Alarm"] = 10;
    telemetry.TrackEvent("status", null, measurements);

<span data-ttu-id="79109-122">Les alertes ayant deux états, vous devez envoyer une valeur faible quand vous considérez que l’alerte est terminée :</span><span class="sxs-lookup"><span data-stu-id="79109-122">Because alerts have two states, you have to send a low value when you consider the alert to have ended:</span></span>

    telemetry.TrackMetric("Alarm", 0.5);

<span data-ttu-id="79109-123">Créez un graphique dans [Metrics Explorer](app-insights-metrics-explorer.md) pour afficher votre alarme :</span><span class="sxs-lookup"><span data-stu-id="79109-123">Create a chart in [metric explorer](app-insights-metrics-explorer.md) to see your alarm:</span></span>

![](./media/app-insights-how-do-i/010-alarm.png)

<span data-ttu-id="79109-124">Maintenant, définissez une alerte qui se déclenche quand la métrique dépasse une valeur moyenne pendant une courte période :</span><span class="sxs-lookup"><span data-stu-id="79109-124">Now set an alert to fire when the metric goes above a mid value for a short period:</span></span>

![](./media/app-insights-how-do-i/020-threshold.png)

<span data-ttu-id="79109-125">Définissez la durée moyenne sur la valeur minimale.</span><span class="sxs-lookup"><span data-stu-id="79109-125">Set the averaging period to the minimum.</span></span>

<span data-ttu-id="79109-126">Vous recevrez des messages électroniques quand la métrique est supérieure et inférieure au seuil.</span><span class="sxs-lookup"><span data-stu-id="79109-126">You'll get emails both when the metric goes above and below the threshold.</span></span>

<span data-ttu-id="79109-127">Éléments à prendre en considération :</span><span class="sxs-lookup"><span data-stu-id="79109-127">Some points to consider:</span></span>

* <span data-ttu-id="79109-128">Une alerte possède deux états (« alerte » et « intègre »).</span><span class="sxs-lookup"><span data-stu-id="79109-128">An alert has two states ("alert" and "healthy").</span></span> <span data-ttu-id="79109-129">L’état est évalué uniquement quand une métrique est reçue.</span><span class="sxs-lookup"><span data-stu-id="79109-129">The state is evaluated only when a metric is received.</span></span>
* <span data-ttu-id="79109-130">Un message électronique est envoyé uniquement quand l’état change.</span><span class="sxs-lookup"><span data-stu-id="79109-130">An email is sent only when the state changes.</span></span> <span data-ttu-id="79109-131">C’est pourquoi vous devez envoyer à la fois des métriques de valeur haute et faible.</span><span class="sxs-lookup"><span data-stu-id="79109-131">This is why you have to send both high and low-value metrics.</span></span>
* <span data-ttu-id="79109-132">Pour évaluer l’alerte, la moyenne est calculée à partir des valeurs reçues pendant la période précédente.</span><span class="sxs-lookup"><span data-stu-id="79109-132">To evaluate the alert, the average is taken of the received values over the preceding period.</span></span> <span data-ttu-id="79109-133">Comme cela se produit chaque fois qu’une métrique est reçue, des messages électroniques peuvent être envoyés plus fréquemment que la période que vous avez définie.</span><span class="sxs-lookup"><span data-stu-id="79109-133">This occurs every time a metric is received, so emails can be sent more frequently than the period you set.</span></span>
* <span data-ttu-id="79109-134">Étant donné que les messages électroniques sont envoyés à la fois pour les états « alerte » et « intègre », vous devrez peut-être remplacer votre événement à déclenchement unique par une condition à deux états.</span><span class="sxs-lookup"><span data-stu-id="79109-134">Since emails are sent both on "alert" and "healthy", you might want to consider re-thinking your one-shot event as a two-state condition.</span></span> <span data-ttu-id="79109-135">Par exemple, au lieu d’un événement « tâche terminée », définissez une condition « tâche en cours », pour laquelle vous obtenez des messages électroniques au début et à la fin d’une tâche.</span><span class="sxs-lookup"><span data-stu-id="79109-135">For example, instead of a "job completed" event, have a "job in progress" condition, where you get emails at the start and end of a job.</span></span>

### <a name="set-up-alerts-automatically"></a><span data-ttu-id="79109-136">Configurer automatiquement des alertes</span><span class="sxs-lookup"><span data-stu-id="79109-136">Set up alerts automatically</span></span>
[<span data-ttu-id="79109-137">Utiliser PowerShell pour créer des alertes</span><span class="sxs-lookup"><span data-stu-id="79109-137">Use PowerShell to create new alerts</span></span>](app-insights-alerts.md#automation)

## <a name="use-powershell-to-manage-application-insights"></a><span data-ttu-id="79109-138">Utiliser PowerShell pour gérer Application Insights</span><span class="sxs-lookup"><span data-stu-id="79109-138">Use PowerShell to Manage Application Insights</span></span>
* [<span data-ttu-id="79109-139">Créer des ressources</span><span class="sxs-lookup"><span data-stu-id="79109-139">Create new resources</span></span>](app-insights-powershell-script-create-resource.md)
* [<span data-ttu-id="79109-140">Créer des alertes</span><span class="sxs-lookup"><span data-stu-id="79109-140">Create new alerts</span></span>](app-insights-alerts.md#automation)

## <a name="separate-telemetry-from-different-versions"></a><span data-ttu-id="79109-141">Télémétrie distincte des différentes versions</span><span class="sxs-lookup"><span data-stu-id="79109-141">Separate telemetry from different versions</span></span>

* <span data-ttu-id="79109-142">Plusieurs rôles dans une application : utiliser une seule ressource Application Insights et filtrez sur cloud_Rolename.</span><span class="sxs-lookup"><span data-stu-id="79109-142">Multiple roles in an app: Use a single Application Insights resource, and filter on cloud_Rolename.</span></span> [<span data-ttu-id="79109-143">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="79109-143">Learn more</span></span>](app-insights-monitor-multi-role-apps.md)
* <span data-ttu-id="79109-144">Séparation des versions de développement, de test et de publication : utiliser différentes ressources d’Application Insights.</span><span class="sxs-lookup"><span data-stu-id="79109-144">Separating development, test, and release versions: Use different Application Insights resources.</span></span> <span data-ttu-id="79109-145">Sélectionnez les clés d’instrumentation à partir de web.config. [En savoir plus](app-insights-separate-resources.md)</span><span class="sxs-lookup"><span data-stu-id="79109-145">Pick up the instrumentation keys from web.config. [Learn more](app-insights-separate-resources.md)</span></span>
* <span data-ttu-id="79109-146">Génération de rapports sur les versions : ajouter une propriété à l’aide d’un initialiseur de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="79109-146">Reporting build versions: Add a property using a telemetry initializer.</span></span> [<span data-ttu-id="79109-147">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="79109-147">Learn more</span></span>](app-insights-separate-resources.md)

## <a name="monitor-backend-servers-and-desktop-apps"></a><span data-ttu-id="79109-148">Surveiller les serveurs principaux et les applications de bureau</span><span class="sxs-lookup"><span data-stu-id="79109-148">Monitor backend servers and desktop apps</span></span>
<span data-ttu-id="79109-149">[Utilisez le module du Kit de développement logiciel (SDK) Windows Server](app-insights-windows-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="79109-149">[Use the Windows Server SDK module](app-insights-windows-desktop.md).</span></span>

## <a name="visualize-data"></a><span data-ttu-id="79109-150">Visualiser les données</span><span class="sxs-lookup"><span data-stu-id="79109-150">Visualize data</span></span>
#### <a name="dashboard-with-metrics-from-multiple-apps"></a><span data-ttu-id="79109-151">Tableau de bord avec des métriques de plusieurs applications</span><span class="sxs-lookup"><span data-stu-id="79109-151">Dashboard with metrics from multiple apps</span></span>
* <span data-ttu-id="79109-152">Dans [Metrics Explorer](app-insights-metrics-explorer.md), personnalisez votre graphique et enregistrez-le en tant que favori.</span><span class="sxs-lookup"><span data-stu-id="79109-152">In [Metric Explorer](app-insights-metrics-explorer.md), customize your chart and save it as a favorite.</span></span> <span data-ttu-id="79109-153">Épinglez-le au tableau de bord Azure.</span><span class="sxs-lookup"><span data-stu-id="79109-153">Pin it to the Azure dashboard.</span></span>

#### <a name="dashboard-with-data-from-other-sources-and-application-insights"></a><span data-ttu-id="79109-154">Tableau de bord avec des données provenant d’autres sources et d’Application Insights</span><span class="sxs-lookup"><span data-stu-id="79109-154">Dashboard with data from other sources and Application Insights</span></span>
* <span data-ttu-id="79109-155">[Exportez la télémétrie dans Power BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="79109-155">[Export telemetry to Power BI](app-insights-export-power-bi.md).</span></span>

<span data-ttu-id="79109-156">Ou</span><span class="sxs-lookup"><span data-stu-id="79109-156">Or</span></span>

* <span data-ttu-id="79109-157">Utilisez SharePoint comme tableau de bord, pour afficher les données des composants WebPart de SharePoint.</span><span class="sxs-lookup"><span data-stu-id="79109-157">Use SharePoint as your dashboard, displaying data in SharePoint web parts.</span></span> <span data-ttu-id="79109-158">[Utilisez l’exportation continue et Stream Analytics pour exporter vers SQL](app-insights-code-sample-export-sql-stream-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="79109-158">[Use continuous export and Stream Analytics to export to SQL](app-insights-code-sample-export-sql-stream-analytics.md).</span></span>  <span data-ttu-id="79109-159">Utilisez PowerView pour examiner la base de données et créer un composant WebPart de SharePoint pour PowerView.</span><span class="sxs-lookup"><span data-stu-id="79109-159">Use PowerView to examine the database, and create a SharePoint web part for PowerView.</span></span>

<a name="search-specific-users"></a>

### <a name="filter-out-anonymous-or-authenticated-users"></a><span data-ttu-id="79109-160">Filtrer les utilisateurs authentifiés ou anonymes</span><span class="sxs-lookup"><span data-stu-id="79109-160">Filter out anonymous or authenticated users</span></span>
<span data-ttu-id="79109-161">Si vos utilisateurs se connectent, vous pouvez définir l’ [ID d’utilisateur authentifié](app-insights-api-custom-events-metrics.md#authenticated-users). (Cela n’est pas automatique.)</span><span class="sxs-lookup"><span data-stu-id="79109-161">If your users sign in, you can set the [authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users). (It doesn't happen automatically.)</span></span>

<span data-ttu-id="79109-162">Vous pouvez ensuite effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="79109-162">You can then:</span></span>

* <span data-ttu-id="79109-163">Rechercher des ID d’utilisateur spécifiques</span><span class="sxs-lookup"><span data-stu-id="79109-163">Search on specific user ids</span></span>

![](./media/app-insights-how-do-i/110-search.png)

* <span data-ttu-id="79109-164">Filtrer des métriques sur les utilisateurs anonymes ou authentifiés</span><span class="sxs-lookup"><span data-stu-id="79109-164">Filter metrics to either anonymous or authenticated users</span></span>

![](./media/app-insights-how-do-i/115-metrics.png)

## <a name="modify-property-names-or-values"></a><span data-ttu-id="79109-165">Modification de noms ou de valeurs de propriété</span><span class="sxs-lookup"><span data-stu-id="79109-165">Modify property names or values</span></span>
<span data-ttu-id="79109-166">Créez un [filtre](app-insights-api-filtering-sampling.md#filtering).</span><span class="sxs-lookup"><span data-stu-id="79109-166">Create a [filter](app-insights-api-filtering-sampling.md#filtering).</span></span> <span data-ttu-id="79109-167">Cela vous permet de modifier ou de filtrer la télémétrie avant son envoi depuis votre application vers Application Insights.</span><span class="sxs-lookup"><span data-stu-id="79109-167">This lets you modify or filter telemetry before it is sent from your app to Application Insights.</span></span>

## <a name="list-specific-users-and-their-usage"></a><span data-ttu-id="79109-168">Répertorier les utilisateurs spécifiques et leur utilisation</span><span class="sxs-lookup"><span data-stu-id="79109-168">List specific users and their usage</span></span>
<span data-ttu-id="79109-169">Si vous voulez simplement [rechercher des utilisateurs spécifiques](#search-specific-users), vous pouvez définir [l’identifiant utilisateur authentifié](app-insights-api-custom-events-metrics.md#authenticated-users).</span><span class="sxs-lookup"><span data-stu-id="79109-169">If you just want to [search for specific users](#search-specific-users), you can set the [authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users).</span></span>

<span data-ttu-id="79109-170">Si vous voulez une liste des utilisateurs avec des données telles que les pages qu’ils ont consultées ou leur fréquence de connexion, deux options s’offrent à vous :</span><span class="sxs-lookup"><span data-stu-id="79109-170">If you want a list of users with data such as what pages they look at or how often they log in, you have two options:</span></span>

* <span data-ttu-id="79109-171">[Définissez l’identifiant utilisateur authentifié](app-insights-api-custom-events-metrics.md#authenticated-users), [exportez vers une base de données](app-insights-code-sample-export-sql-stream-analytics.md) et utilisez des outils pour analyser vos données utilisateur.</span><span class="sxs-lookup"><span data-stu-id="79109-171">[Set authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users), [export to a database](app-insights-code-sample-export-sql-stream-analytics.md) and use suitable tools to analyze your user data there.</span></span>
* <span data-ttu-id="79109-172">Si vous ne disposez que d’un petit nombre d’utilisateurs, envoyez des événements ou des métriques personnalisés, en utilisant les données d’intérêt comme le nom de l’événement ou la valeur de la métrique et en définissant l’id d’utilisateur en tant que propriété.</span><span class="sxs-lookup"><span data-stu-id="79109-172">If you have only a small number of users, send custom events or metrics, using the data of interest as the metric value or event name, and setting the user id as a property.</span></span> <span data-ttu-id="79109-173">Pour analyser les vues de page, remplacez l’appel standard de trackPageView JavaScript.</span><span class="sxs-lookup"><span data-stu-id="79109-173">To analyze page views, replace the standard JavaScript trackPageView call.</span></span> <span data-ttu-id="79109-174">Pour analyser la télémétrie côté serveur, utilisez un initialiseur de télémétrie pour ajouter l’id d’utilisateur à toute la télémétrie de serveur.</span><span class="sxs-lookup"><span data-stu-id="79109-174">To analyze server-side telemetry, use a telemetry initializer to add the user id to all server telemetry.</span></span> <span data-ttu-id="79109-175">Vous pouvez ensuite filtrer et segmenter les métriques et les recherches sur l’id d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="79109-175">You can then filter and segment metrics and searches on the user id.</span></span>

## <a name="reduce-traffic-from-my-app-to-application-insights"></a><span data-ttu-id="79109-176">Réduire le trafic de mon application vers Application Insights</span><span class="sxs-lookup"><span data-stu-id="79109-176">Reduce traffic from my app to Application Insights</span></span>
* <span data-ttu-id="79109-177">Dans [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), désactivez tous les modules dont vous n’avez pas besoin, comme le collecteur de compteurs de performances.</span><span class="sxs-lookup"><span data-stu-id="79109-177">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), disable any modules you don't need, such the performance counter collector.</span></span>
* <span data-ttu-id="79109-178">Utilisez [Échantillonnage et filtrage](app-insights-api-filtering-sampling.md) dans le Kit de développement logiciel (SDK).</span><span class="sxs-lookup"><span data-stu-id="79109-178">Use [Sampling and filtering](app-insights-api-filtering-sampling.md) at the SDK.</span></span>
* <span data-ttu-id="79109-179">Dans vos pages web, limitez le nombre d'appels Ajax signalés pour chaque affichage de page.</span><span class="sxs-lookup"><span data-stu-id="79109-179">In your web pages, Limit the number of Ajax calls reported for every page view.</span></span> <span data-ttu-id="79109-180">Dans l(extrait de script après `instrumentationKey:...`, insérez : `,maxAjaxCallsPerView:3` (ou un nombre approprié).</span><span class="sxs-lookup"><span data-stu-id="79109-180">In the script snippet after `instrumentationKey:...` , insert: `,maxAjaxCallsPerView:3` (or a suitable number).</span></span>
* <span data-ttu-id="79109-181">Si vous utilisez [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric), calculez l’agrégat des lots de valeurs de métriques avant d’envoyer le résultat.</span><span class="sxs-lookup"><span data-stu-id="79109-181">If you're using [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric), compute the aggregate of batches of metric values before sending the result.</span></span> <span data-ttu-id="79109-182">Il existe une surcharge de TrackMetric() qui se charge de cette tâche.</span><span class="sxs-lookup"><span data-stu-id="79109-182">There's an overload of TrackMetric() that provides for that.</span></span>

<span data-ttu-id="79109-183">En savoir plus sur la [tarification et les quotas](app-insights-pricing.md).</span><span class="sxs-lookup"><span data-stu-id="79109-183">Learn more about [pricing and quotas](app-insights-pricing.md).</span></span>

## <a name="disable-telemetry"></a><span data-ttu-id="79109-184">Désactiver la télémétrie</span><span class="sxs-lookup"><span data-stu-id="79109-184">Disable telemetry</span></span>
<span data-ttu-id="79109-185">Pour **arrêter et démarrer dynamiquement** la collecte et la transmission de la télémétrie à partir du serveur :</span><span class="sxs-lookup"><span data-stu-id="79109-185">To **dynamically stop and start** the collection and transmission of telemetry from the server:</span></span>

```

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```



<span data-ttu-id="79109-186">Pour **désactiver les collecteurs standard sélectionnés** (par exemple, les compteurs de performances, les requêtes HTTP ou les dépendances), supprimez ou commentez les lignes correspondantes dans [ApplicationInsights.config](app-insights-api-custom-events-metrics.md). Par exemple, vous pouvez faire cela si vous souhaitez envoyer vos propres données TrackRequest.</span><span class="sxs-lookup"><span data-stu-id="79109-186">To **disable selected standard collectors** - for example, performance counters, HTTP requests, or dependencies - delete or comment out the relevant lines in [ApplicationInsights.config](app-insights-api-custom-events-metrics.md). You could do this, for example, if you want to send your own TrackRequest data.</span></span>

## <a name="view-system-performance-counters"></a><span data-ttu-id="79109-187">Afficher les compteurs de performances système</span><span class="sxs-lookup"><span data-stu-id="79109-187">View system performance counters</span></span>
<span data-ttu-id="79109-188">Parmi les métriques que vous pouvez afficher dans Metrics Explorer, il existe un ensemble de compteurs de performances système.</span><span class="sxs-lookup"><span data-stu-id="79109-188">Among the metrics you can show in metrics explorer are a set of system performance counters.</span></span> <span data-ttu-id="79109-189">Un panneau prédéfini intitulé **Serveurs** affiche plusieurs d'entre eux.</span><span class="sxs-lookup"><span data-stu-id="79109-189">There's a predefined blade titled **Servers** that displays several of them.</span></span>

![Ouvrez votre ressource Application Insights et cliquez sur Serveurs.](./media/app-insights-how-do-i/121-servers.png)

### <a name="if-you-see-no-performance-counter-data"></a><span data-ttu-id="79109-191">Si aucune donnée de compteur de performances ne s’affiche</span><span class="sxs-lookup"><span data-stu-id="79109-191">If you see no performance counter data</span></span>
* <span data-ttu-id="79109-192">**Serveur IIS** sur votre propre ordinateur ou sur une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="79109-192">**IIS server** on your own machine or on a VM.</span></span> <span data-ttu-id="79109-193">[Installer Status Monitor](app-insights-monitor-performance-live-website-now.md).</span><span class="sxs-lookup"><span data-stu-id="79109-193">[Install Status Monitor](app-insights-monitor-performance-live-website-now.md).</span></span>
* <span data-ttu-id="79109-194">**Site Web Azure** : nous ne prenons pas encore en charge les compteurs de performances.</span><span class="sxs-lookup"><span data-stu-id="79109-194">**Azure web site** - we don't support performance counters yet.</span></span> <span data-ttu-id="79109-195">Il existe plusieurs métriques que vous pouvez obtenir de manière standard dans le panneau de configuration des sites web Azure.</span><span class="sxs-lookup"><span data-stu-id="79109-195">There are several metrics you can get as a standard part of the Azure web site control panel.</span></span>
* <span data-ttu-id="79109-196">**Serveur Unix** - [installer collectd](app-insights-java-collectd.md)</span><span class="sxs-lookup"><span data-stu-id="79109-196">**Unix server** - [Install collectd](app-insights-java-collectd.md)</span></span>

### <a name="to-display-more-performance-counters"></a><span data-ttu-id="79109-197">Pour afficher davantage de compteurs de performances</span><span class="sxs-lookup"><span data-stu-id="79109-197">To display more performance counters</span></span>
* <span data-ttu-id="79109-198">Tout d’abord, [ajoutez un nouveau graphique](app-insights-metrics-explorer.md) et vérifiez si le compteur se trouve dans le jeu de base que nous offrons.</span><span class="sxs-lookup"><span data-stu-id="79109-198">First, [add a new chart](app-insights-metrics-explorer.md) and see if the counter is in the basic set that we offer.</span></span>
* <span data-ttu-id="79109-199">Dans le cas contraire, [ajoutez le compteur au jeu collecté par le module de compteur de performances](app-insights-performance-counters.md).</span><span class="sxs-lookup"><span data-stu-id="79109-199">If not, [add the counter to the set collected by the performance counter module](app-insights-performance-counters.md).</span></span>
