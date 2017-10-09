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
# <a name="how-do-i--in-application-insights"></a>Comment ... dans Application Insights ?
## <a name="get-an-email-when-"></a>Recevoir un message électronique quand...
### <a name="email-if-my-site-goes-down"></a>Envoyer un message électronique si mon site tombe en panne
Définissez un [test web de disponibilité](app-insights-monitor-web-app-availability.md).

### <a name="email-if-my-site-is-overloaded"></a>Envoyer un message électronique si mon site est surchargé
Définissez une [alerte](app-insights-alerts.md) sur le **Temps de réponse du serveur**. Un seuil compris entre 1 et 2 secondes doit fonctionner.

![](./media/app-insights-how-do-i/030-server.png)

Votre application peut également indiquer des signes de surcharge en retournant des codes d’erreur. Définissez une alerte sur les **Demandes ayant échoué**.

Si vous souhaitez tooset une alerte sur **exceptions du serveur**, vous pouvez avoir toodo [une installation supplémentaire](app-insights-asp-net-exceptions.md) données de commandes toosee.

### <a name="email-on-exceptions"></a>Envoyer un message électronique en cas d’exceptions
1. [Configurer la surveillance des exceptions](app-insights-asp-net-exceptions.md)
2. [Définir une alerte](app-insights-alerts.md) sur hello Exception compter métrique

### <a name="email-on-an-event-in-my-app"></a>Envoyer un message électronique en réponse à un événement dans mon application
Supposons que vous aimeriez tooget un message électronique lorsqu’un événement spécifique se produit. Application Insights ne fournit pas directement cette fonctionnalité, mais peut [envoyer une alerte quand une métrique dépasse un seuil](app-insights-alerts.md).

Les alertes peuvent être définies sur des [métriques personnalisées](app-insights-api-custom-events-metrics.md#trackmetric), et non sur des événements personnalisés. Écrire certaines tooincrease code une métrique lorsque hello événement se produit :

    telemetry.TrackMetric("Alarm", 10);

ou :

    var measurements = new Dictionary<string,double>();
    measurements ["Alarm"] = 10;
    telemetry.TrackEvent("status", null, measurements);

Étant donné que les alertes ont deux États, vous avez toosend une valeur faible lorsque vous envisagez d’alerte hello toohave s’est terminée :

    telemetry.TrackMetric("Alarm", 0.5);

Créer un graphique dans [explorer métrique](app-insights-metrics-explorer.md) toosee votre alarme :

![](./media/app-insights-how-do-i/010-alarm.png)

Maintenant définir une alerte toofire lors de la métrique de hello dépasse une valeur moyenne pendant une courte période :

![](./media/app-insights-how-do-i/020-threshold.png)

Définissez hello moyenne toohello période minimum.

Vous allez recevoir des messages électroniques lorsque la métrique de hello passe au-dessus et sous le seuil de hello.

Certains tooconsider points :

* Une alerte possède deux états (« alerte » et « intègre »). état de Hello est évalué uniquement lorsqu’une mesure est reçue.
* Un message électronique est envoyé uniquement lorsque l’état hello change. C’est pourquoi vous avez toosend haute et faible valeur métriques.
* alerte de hello tooevaluate, moyenne de hello est repris des valeurs de salutation reçue hello précédant la période. Cela se produit chaque fois qu’une mesure est reçue, les messages électroniques peuvent être envoyées plus fréquemment que la période de hello que vous définissez.
* Étant donné que les messages électroniques sont envoyés à la fois « alerte » et « sain », vous pourriez tooconsider nouveau considérant votre événement Shot comme une condition de deux États. Par exemple, au lieu d’un événement « terminée », ont une condition « tâche en cours d’exécution », où vous obtenez des messages électroniques au début de hello et de fin d’une tâche.

### <a name="set-up-alerts-automatically"></a>Configurer automatiquement des alertes
[Utilisez PowerShell toocreate nouvelles alertes](app-insights-alerts.md#automation)

## <a name="use-powershell-toomanage-application-insights"></a>Utilisez PowerShell tooManage Application Insights
* [Créer des ressources](app-insights-powershell-script-create-resource.md)
* [Créer des alertes](app-insights-alerts.md#automation)

## <a name="separate-telemetry-from-different-versions"></a>Télémétrie distincte des différentes versions

* Plusieurs rôles dans une application : utiliser une seule ressource Application Insights et filtrez sur cloud_Rolename. [En savoir plus](app-insights-monitor-multi-role-apps.md)
* Séparation des versions de développement, de test et de publication : utiliser différentes ressources d’Application Insights. Sélectionnez des clés d’instrumentation hello à partir de web.config. [En savoir plus](app-insights-separate-resources.md)
* Génération de rapports sur les versions : ajouter une propriété à l’aide d’un initialiseur de télémétrie. [En savoir plus](app-insights-separate-resources.md)

## <a name="monitor-backend-servers-and-desktop-apps"></a>Surveiller les serveurs principaux et les applications de bureau
[Utiliser le module hello SDK Windows Server](app-insights-windows-desktop.md).

## <a name="visualize-data"></a>Visualiser les données
#### <a name="dashboard-with-metrics-from-multiple-apps"></a>Tableau de bord avec des métriques de plusieurs applications
* Dans [Metrics Explorer](app-insights-metrics-explorer.md), personnalisez votre graphique et enregistrez-le en tant que favori. Épingler toohello tableau de bord Azure.

#### <a name="dashboard-with-data-from-other-sources-and-application-insights"></a>Tableau de bord avec des données provenant d’autres sources et d’Application Insights
* [Exporter les données de télémétrie tooPower BI](app-insights-export-power-bi.md).

Ou

* Utilisez SharePoint comme tableau de bord, pour afficher les données des composants WebPart de SharePoint. [Utiliser l’exportation continue et flux de données Analytique tooexport tooSQL](app-insights-code-sample-export-sql-stream-analytics.md).  Utiliser la base de données PowerView tooexamine hello et créer un composant WebPart SharePoint pour PowerView.

<a name="search-specific-users"></a>

### <a name="filter-out-anonymous-or-authenticated-users"></a>Filtrer les utilisateurs authentifiés ou anonymes
Si vos utilisateurs se connectent, vous pouvez définir hello [id de l’utilisateur authentifié](app-insights-api-custom-events-metrics.md#authenticated-users). (Cela n’est pas automatique.)

Vous pouvez ensuite effectuer les opérations suivantes :

* Rechercher des ID d’utilisateur spécifiques

![](./media/app-insights-how-do-i/110-search.png)

* Filtrer les utilisateurs anonymes ou authentifiés du tooeither métriques

![](./media/app-insights-how-do-i/115-metrics.png)

## <a name="modify-property-names-or-values"></a>Modification de noms ou de valeurs de propriété
Créez un [filtre](app-insights-api-filtering-sampling.md#filtering). Cela vous permet de modifier ou de filtrer les données de télémétrie avant d’être envoyée à partir de votre tooApplication application Insights.

## <a name="list-specific-users-and-their-usage"></a>Répertorier les utilisateurs spécifiques et leur utilisation
Si vous souhaitez simplement trop[recherche pour des utilisateurs spécifiques](#search-specific-users), vous pouvez définir hello [id de l’utilisateur authentifié](app-insights-api-custom-events-metrics.md#authenticated-users).

Si vous voulez une liste des utilisateurs avec des données telles que les pages qu’ils ont consultées ou leur fréquence de connexion, deux options s’offrent à vous :

* [Id de l’utilisateur authentifié ensemble](app-insights-api-custom-events-metrics.md#authenticated-users), [exporter la base de données tooa](app-insights-code-sample-export-sql-stream-analytics.md) et utilisation appropriée des outils tooanalyze vos données utilisateur.
* Si vous avez uniquement un petit nombre d’utilisateurs, envoyer des événements personnalisés ou des mesures, à l’aide de données hello d’intérêt que hello valeur métrique ou nom de l’événement et id d’utilisateur paramètre hello en tant que propriété. tooanalyze des vues de page, remplacez l’appel trackPageView JavaScript standard de hello. données de télémétrie tooanalyze côté serveur, utilisez une télémétrie initialiseur tooadd hello id tooall server télémétrie d’utilisateur. Vous pouvez ensuite les métriques de filtre et de segment et les recherches sur les id d’utilisateur hello.

## <a name="reduce-traffic-from-my-app-tooapplication-insights"></a>Réduire le trafic à partir de mon tooApplication application Insights
* Dans [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), désactivez tous les modules que vous n’avez pas besoin, ce collecteur hello du compteur de performance.
* Utilisez [d’échantillonnage et le filtrage](app-insights-api-filtering-sampling.md) à hello SDK.
* Dans vos pages web, limitez le nombre de hello des appels Ajax signalé pour chaque vue de la page. Dans l’extrait de code hello script après `instrumentationKey:...` , insérer : `,maxAjaxCallsPerView:3` (ou un nombre approprié).
* Si vous utilisez [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric), agrégat hello de lots de valeurs de mesure de calcul avant d’envoyer le résultat de hello. Il existe une surcharge de TrackMetric() qui se charge de cette tâche.

En savoir plus sur la [tarification et les quotas](app-insights-pricing.md).

## <a name="disable-telemetry"></a>Désactiver la télémétrie
trop**dynamiquement arrêter et démarrer** hello collecte et transmission des données de télémétrie à partir du serveur de hello :

```

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```



trop**désactiver les collecteurs standards sélectionnés** - par exemple, les compteurs de performance, les requêtes HTTP ou les dépendances - supprimez ou commentez les lignes concernées hello [ApplicationInsights.config](app-insights-api-custom-events-metrics.md). Procéder, par exemple, si vous souhaitez toosend vos propres données TrackRequest.

## <a name="view-system-performance-counters"></a>Afficher les compteurs de performances système
Parmi les hello métriques que vous pouvez afficher dans l’Explorateur de métriques sont un ensemble de compteurs de performances système. Un panneau prédéfini intitulé **Serveurs** affiche plusieurs d'entre eux.

![Ouvrez votre ressource Application Insights et cliquez sur Serveurs.](./media/app-insights-how-do-i/121-servers.png)

### <a name="if-you-see-no-performance-counter-data"></a>Si aucune donnée de compteur de performances ne s’affiche
* **Serveur IIS** sur votre propre ordinateur ou sur une machine virtuelle. [Installer Status Monitor](app-insights-monitor-performance-live-website-now.md).
* **Site Web Azure** : nous ne prenons pas encore en charge les compteurs de performances. Il existe plusieurs mesures, que vous pouvez obtenir comme une partie standard du Panneau de contrôle de site web Azure hello.
* **Serveur Unix** - [installer collectd](app-insights-java-collectd.md)

### <a name="toodisplay-more-performance-counters"></a>toodisplay des compteurs de performance
* Tout d’abord, [ajouter un nouveau graphique](app-insights-metrics-explorer.md) et voyez si hello est Bonjour base ensemble de compteurs que nous proposons.
* Si ce n’est pas le cas, [ajouter hello compteur toohello jeu collecté par le module compteur de performances hello](app-insights-performance-counters.md).
