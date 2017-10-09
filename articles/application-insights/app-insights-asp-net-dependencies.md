---
title: "aaaDependency suivi des modifications dans l’Application Azure Insights | Documents Microsoft"
description: "Analysez l'utilisation, la disponibilité et les performances de votre application web locale ou Microsoft Azure avec Application Insights."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d15c4ca8-4c1a-47ab-a03d-c322b4bb2a9e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: bwren
ms.openlocfilehash: e72f5465462ae8e64363cbbaa62911aff636c504
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-application-insights-dependency-tracking"></a>Configurer Application Insights : suivi des dépendances
Un *dépendance* est un composant externe qui est appelé par votre application. Il s’agit habituellement d’un service appelé à l’aide de HTTP, d’une base de données ou d’un système de fichiers. [Application Insights](app-insights-overview.md) mesure combien de temps votre application attend les dépendances et la fréquence à laquelle un appel de dépendance échoue. Vous pouvez examiner les appels spécifiques et les associer à toorequests et les exceptions.

![Exemples de graphiques](./media/app-insights-asp-net-dependencies/10-intro.png)

Moniteur de dépendance d’out of box Hello indique actuellement types toothese d’appels de dépendances :

* Serveur
  * Bases de données SQL
  * Services web et WCF d’ASP.NET qui utilisent des liaisons HTTP
  * Appels HTTP locaux ou distants
  * Azure Cosmos DB, table, stockage d’objets blob et file d’attente
* Pages web
  * Appels AJAX

La surveillance fonctionne en utilisant l’[instrumentation de code octet](https://msdn.microsoft.com/library/z9z62c29.aspx) autour des méthodes sélectionnées. La surcharge de performances est minime.

Vous pouvez également écrire votre propre SDK appelle toomonitor autres dépendances, à la fois dans le code client et serveur de hello, à l’aide de hello [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).

## <a name="set-up-dependency-monitoring"></a>Configurer la surveillance des dépendances
Informations de dépendance partiel sont automatiquement collectées par hello [Application Insights SDK](app-insights-asp-net.md). tooget complète des données, installez agent approprié de hello pour le serveur hôte de hello.

| Plateforme | Installer |
| --- | --- |
| Serveur IIS |Soit [installer Status Monitor sur votre serveur](app-insights-monitor-performance-live-website-now.md) ou [mise à niveau de votre infrastructure d’application too.NET 4.6 ou version ultérieure](http://go.microsoft.com/fwlink/?LinkId=528259) et installer hello [Application Insights SDK](app-insights-asp-net.md) dans votre application. |
| Application web Azure |Dans le panneau de configuration web app, [panneau d’Application Insights hello ouvert dans le panneau de configuration web application](app-insights-azure-web-apps.md) et choisir l’installation si vous y êtes invité. |
| Service cloud Azure |[Utilisez une tâche de démarrage](app-insights-cloudservices.md) ou [installez le .NET Framework version 4.6 ou ultérieure](../cloud-services/cloud-services-dotnet-install-dotnet.md). |

## <a name="where-toofind-dependency-data"></a>Où les données de dépendance toofind
* [Mise en correspondance d’applications](#application-map) visualise les dépendances entre votre application et les composants voisins.
* [Les panneaux de performances, de navigateurs et d’échecs](#performance-and-blades) affichent les données sur les dépendances de serveur.
* [Les panneaux de navigateurs](#ajax-calls) montrent les appels AJAX provenant des navigateurs de vos utilisateurs.
* [Parcourez les requêtes lents ou ayant échoué](#diagnose-slow-requests) toocheck appelle de leurs dépendances.
* [Analytique](#analytics) peuvent être des données de dépendance tooquery utilisé.

## <a name="application-map"></a>Plan de l’application
Mappage d’application agit comme un dépendances de toodiscovering aide visuelle entre les composants hello de votre application. Il est automatiquement généré à partir de la télémétrie hello à partir de votre application. Cet exemple montre les appels AJAX à partir de scripts de navigateur hello et reste à partir du serveur de hello services externes d’application tootwo.

![Plan de l’application](./media/app-insights-asp-net-dependencies/08.png)

* **Accédez à partir de boîtes de hello** toorelevant dépendance et autres graphiques.
* **Mappage de code confidentiel hello** toohello [tableau de bord](app-insights-dashboards.md), où il ne sera pas complètement fonctionnelle.

[En savoir plus](app-insights-app-map.md).

## <a name="performance-and-failure-blades"></a>Panneaux de performances et d’échecs
Panneau de performances Hello montre la durée hello d’appels de dépendance effectués par l’application de serveur hello. Il existe un graphique de synthèse et un tableau segmenté par appel.

![Graphiques de dépendances du panneau de performances](./media/app-insights-asp-net-dependencies/dependencies-in-performance-blade.png)

Cliquez sur les graphiques de résumé hello ou hello table éléments toosearch brut occurrences de ces appels.

![Instances d’appels de dépendances](./media/app-insights-asp-net-dependencies/dependency-call-instance.png)

**Nombre d’échecs** figurent sur hello **échecs** panneau. Une défaillance est tout code de retour n’est pas de hello plage 200-399, ou inconnu.

> [!NOTE]
> **100 % d’échecs ?** Cela signifie probablement que vous obtenez uniquement des données de dépendances partielles. Vous devez trop[configurer tooyour approprié plateforme d’analyse de dépendance](#set-up-dependency-monitoring).
>
>

## <a name="ajax-calls"></a>Appels AJAX
Panneau de navigateurs Hello montre la durée de hello et taux d’échec d’AJAX appelle à partir de [JavaScript dans vos pages web](app-insights-javascript.md). Ils sont affichés en tant que dépendances.

## <a name="diagnosis"></a> Diagnostiquer les demandes lentes
Chaque événement de requête est associé à des appels de dépendance hello, exceptions et autres événements qui sont suivies lors du traitement de votre application hello demande. Si vous effectuant certaines demandes mal, vous pouvez trouver si elle est en raison de réponses tooslow à partir d’une dépendance.

Prenons un exemple.

### <a name="tracing-from-requests-toodependencies"></a>Le suivi de demandes toodependencies
Ouvrez le panneau de performances hello et observez la grille hello de demandes :

![Liste de demandes avec moyennes et nombres](./media/app-insights-asp-net-dependencies/02-reqs.png)

haut Hello un est très longue. Voyons si nous pouvons découvrir où hello durée.

Cliquez sur cette ligne toosee les événements de demande individuelle :

![Liste des occurrences de demande](./media/app-insights-asp-net-dependencies/03-instances.png)

Cliquez sur n’importe quel tooinspect d’instance longue il plus et faites défiler toohello dépendance distant appels connexes toothis demande :

![Rechercher des dépendances de tooRemote d’appels, d’identifier la durée inhabituelle](./media/app-insights-asp-net-dependencies/04-dependencies.png)

Il semble que la plupart des hello maintenance de temps passé à cette demande dans un service d’appel tooa local.

Sélectionnez cette ligne de tooget plus d’informations :

![Parcourez cette dépendance à distance tooidentify hello soient à l’origine](./media/app-insights-asp-net-dependencies/05-detail.png)

Il semble que c’est là problème de hello. Nous avez correspondant à des problème de hello, donc maintenant nous juste besoin toofind out pourquoi cet appel prend autant de temps.

### <a name="request-timeline"></a>Chronologie de demande
Dans un autre cas, aucun appel de dépendance n’est particulièrement long. Mais en basculant l’affichage de la chronologie toohello, nous pouvons voir où le délai de hello s’est produite dans notre traitement interne :

![Rechercher des dépendances de tooRemote d’appels, d’identifier la durée inhabituelle](./media/app-insights-asp-net-dependencies/04-1.png)

Il semble toobe un grand écart après le premier appel de dépendance hello, donc nous devons examiner notre toosee code pourquoi qui est.

### <a name="profile-your-live-site"></a>Profiler votre site en ligne

Aucune idée où des temps de hello ? Hello [profileur d’Application Insights](app-insights-profiler.md) suivis HTTP appelle tooyour site en ligne et vous montre les fonctions dans votre code a duré plus longtemps hello.

## <a name="failed-requests"></a>Demandes ayant échoué
Demandes ayant échoué peuvent également être associées toodependencies d’appels ayant échoué. Là encore, nous pouvons cliquer tootrack problème de hello.

![Cliquez sur le graphique de demandes ayant échoué hello](./media/app-insights-asp-net-dependencies/06-fail.png)

Parcourez occurrence tooan d’une demande ayant échouée et consulter ses événements associés.

![Cliquez sur un type de requête, cliquez sur hello tooget tooa autre vue d’instance de hello même instance, cliquez dessus tooget détails de l’exception.](./media/app-insights-asp-net-dependencies/07-faildetail.png)

## <a name="analytics"></a>Analyse
Vous pouvez suivre les dépendances dans hello [de langage de requête Analytique de journal](https://docs.loganalytics.io/). Voici quelques exemples.

* Rechercher les appels de dépendances ayant échoué :

```

    dependencies | where success != "True" | take 10
```

* Rechercher les appels AJAX :

```

    dependencies | where client_Type == "Browser" | take 10
```

* Rechercher les appels de dépendances associés aux demandes :

```

    dependencies
    | where timestamp > ago(1d) and  client_Type != "Browser"
    | join (requests | where timestamp > ago(1d))
      on operation_Id  
```


* Rechercher les appels AJAX associés à des pages consultées :

```

    dependencies
    | where timestamp > ago(1d) and  client_Type == "Browser"
    | join (browserTimings | where timestamp > ago(1d))
      on operation_Id
```



## <a name="custom-dependency-tracking"></a>Suivi personnalisé des dépendances
module de suivi de la dépendance standard Hello découvre automatiquement les dépendances externes telles que les bases de données et les API REST. Toutefois, vous pouvez toobe de certains composants supplémentaires traité Bonjour même façon.

Vous pouvez écrire du code qui envoie des informations de dépendance, à l’aide de hello même [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency) qui est utilisé par les modules standard hello.

Par exemple, si vous générez votre code avec un assembly que vous n’avez pas l’écrire vous-même, tous les tooit d’appels hello impossible du temps, toofind effectue la contribution il tooyour réponse délai d’attente. envoyer des données affichées dans les graphiques de dépendance hello dans Application Insights, toohave à l’aide de `TrackDependency`.

```C#

            var startTime = DateTime.UtcNow;
            var timer = System.Diagnostics.Stopwatch.StartNew();
            try
            {
                success = dependency.Call();
            }
            finally
            {
                timer.Stop();
                telemetry.TrackDependency("myDependency", "myCall", startTime, timer.Elapsed, success);
            }
```

Si vous souhaitez tooswitch désactiver le module de suivi hello dépendance standard, supprimez tooDependencyTrackingTelemetryModule de référence hello dans [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md).

## <a name="troubleshooting"></a>Résolution des problèmes
*L’indicateur de réussite de la dépendance affiche toujours True ou False.*

*La requête SQL n’est pas affichée en entier.*

* Mettre à niveau la version la plus récente du Kit de développement logiciel de hello toohello. Si votre version de .NET est inférieur à 4.6 :
  * Hôte IIS : installer [Application Insights Agent](app-insights-monitor-performance-live-website-now.md) sur les serveurs hôtes de hello.
  * Application web Azure : ouvrir Application Insights onglet hello web application le panneau de configuration et installez Application Insights.

## <a name="video"></a>Vidéo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>Étapes suivantes
* [Exceptions](app-insights-asp-net-exceptions.md)
* [Données utilisateur et de page](app-insights-javascript.md)
* [Disponibilité](app-insights-monitor-web-app-availability.md)
