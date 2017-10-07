---
title: compteurs aaaPerformance dans Application Insights | Documents Microsoft
description: "Surveillez les compteurs de performances système et .NET personnalisés dans Application Insights."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 5b816f4c-a77a-4674-ae36-802ee3a2f56d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/11/2016
ms.author: bwren
ms.openlocfilehash: 0a51c225f1d1124c9e7fe89f34e747cb26a3589e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="system-performance-counters-in-application-insights"></a>Compteurs de performances système dans Application Insights
Windows offre un large éventail de [compteurs de performance](http://www.codeproject.com/Articles/8590/An-Introduction-To-Performance-Counters) tels que le niveau d’occupation du processeur, la mémoire, le disque et l’utilisation du réseau. Vous pouvez également définir les vôtres. [Application Insights](app-insights-overview.md) peut afficher ces compteurs de performances si votre application s’exécute sous IIS sur un toowhich d’ordinateur hôte ou virtuel local vous ont un accès administratif. graphiques de Hello indiquent l’application en temps réel de hello ressources tooyour disponible et peuvent aider à tooidentify équilibrage de charge entre des instances de serveur.

Les compteurs de performance s’affichent dans le panneau de serveurs hello, qui inclut une table qui segmente par instance de serveur.

![Compteurs de performances signalés dans Application Insights](./media/app-insights-performance-counters/counters-by-server-instance.png)

(Les compteurs de performance ne sont pas disponibles pour les applications web Azure. Toutefois, vous pouvez [envoyer des Diagnostics Windows Azure tooApplication Insights](app-insights-azure-diagnostics.md).)

## <a name="view-counters"></a>Afficher des compteurs
Panneau de serveurs Hello affiche un ensemble par défaut des compteurs de performance. 

toosee autres compteurs, modifier des graphiques sur le panneau de serveurs hello hello, ou ouvrez un nouveau [Metrics Explorer](app-insights-metrics-explorer.md) panneau et ajouter des graphiques. 

les compteurs disponibles Hello sont répertoriés en tant que mesures lorsque vous modifiez un graphique.

![Compteurs de performances signalés dans Application Insights](./media/app-insights-performance-counters/choose-performance-counters.png)

Création de tous vos graphiques plus utiles dans un seul emplacement, toosee un [tableau de bord](app-insights-dashboards.md) et les épingler tooit.

## <a name="add-counters"></a>Ajouter des compteurs
Si le compteur de performance hello n’est pas indiqué dans la liste des métriques hello, est que hello Application Insights SDK n’est pas sa collecte sur votre serveur web. Vous pouvez configurer toodo donc.

1. Découvrez les compteurs sont disponibles dans votre serveur à l’aide de cette commande PowerShell sur le serveur de hello :
   
    `Get-Counter -ListSet *`
   
    (Voir [`Get-Counter`](https://technet.microsoft.com/library/hh849685.aspx).)
2. Ouvrez ApplicationInsights.config.
   
   * Si vous avez ajouté Application Insights tooyour application pendant le développement, modifier ApplicationInsights.config dans votre projet, puis le redéployer tooyour serveurs.
   * Si vous avez utilisé le moniteur d’état tooinstrument une application web lors de l’exécution, trouver ApplicationInsights.config dans le répertoire racine de hello de l’application hello dans IIS. Mettez-le à jour dans chaque instance de serveur.
3. Modifiez la directive collecteur de performances hello :
   
```XML
   
    <Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule, Microsoft.AI.PerfCounterCollector">
      <Counters>
        <Add PerformanceCounter="\Objects\Processes"/>
        <Add PerformanceCounter="\Sales(photo)\# Items Sold" ReportAs="Photo sales"/>
      </Counters>
    </Add>

```

Vous pouvez capturer les compteurs standard et ceux que vous avez implémentés vous-même. `\Objects\Processes` est un exemple de compteur standard, disponible sur tous les systèmes Windows. `\Sales(photo)\# Items Sold` est un exemple de compteur personnalisé qui peut être implémenté dans un service web. 

format de Hello est `\Category(instance)\Counter"`, ou pour des catégories n’ayant pas d’instances, tout simplement `\Category\Counter`.

`ReportAs`est requis pour les noms de compteur qui ne correspondent pas `[a-zA-Z()/-_ \.]+` -autrement dit, ils contiennent des caractères qui ne sont pas Bonjour ensembles suivants : lettres, round crochets, une barre oblique, trait d’union, un trait de soulignement, espace, le point.

Si vous spécifiez une instance, il est collecté comme une dimension « CounterInstanceName » de hello indiqué métrique.

### <a name="collecting-performance-counters-in-code"></a>Collecte des compteurs de performances dans le code
compteurs de performances du système toocollect et envoyez-le tooApplication Insights, vous pouvez adapter extrait hello ci-dessous :


``` C#

    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\.NET CLR Memory([replace-with-application-process-name])\# GC Handles", "GC Handles")));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

Ou vous pouvez le faire hello la même chose avec les mesures personnalisées que vous avez créé :

``` C#
    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\Sales(photo)\# Items Sold", "Photo sales"));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

## <a name="performance-counters-in-analytics"></a>Compteurs de performances dans Analytics
Vous pouvez rechercher et afficher des rapports de compteur de performances dans [Analytics](app-insights-analytics.md).

Hello **performanceCounters** schéma expose hello `category`, `counter` nom, et `instance` nom de chaque compteur de performance.  Télémétrie hello pour chaque application, vous voyez uniquement les compteurs de hello pour cette application. Par exemple, toosee les compteurs sont disponibles : 

![Compteurs de performances dans Application Insights Analytics](./media/app-insights-performance-counters/analytics-performance-counters.png)

(« Instance » fait ici référence d’instance de compteur de performance toohello, ne Hello pas de rôle ou machine instance de serveur. Nom instance de compteur de performance Hello généralement segmente les compteurs de temps processeur par nom hello de hello processus ou l’application.)

tooget un graphique de mémoire disponible sur hello période récente : 

![Graphique temporel dans Application Insights Analytics](./media/app-insights-performance-counters/analytics-available-memory.png)

Comme les autres données de télémétrie, **performanceCounters** possède également une colonne `cloud_RoleInstance` qui indique l’identité hello de l’instance de serveur hello hôte sur lequel votre application est en cours d’exécution. Par exemple, toocompare hello des performances de votre application sur des ordinateurs différents hello : 

![Performances segmentées par instances de rôle d’Application Insights Analytics](./media/app-insights-performance-counters/analytics-metrics-role-instance.png)

## <a name="aspnet-and-application-insights-counts"></a>Nombres ASP.NET et Application Insights
*Qu’est la différence hello entre le taux d’Exception hello et des métriques d’Exceptions ?*

* *taux d’exceptions* est un compteur de performances système. Hello CLR compte tous les hello gérées et les exceptions non gérées levées et divisant le total de hello dans un intervalle d’échantillonnage par la longueur de l’intervalle de salutation hello. Hello Application Insights SDK collecte ce résultat et l’envoie toohello portal.
* *Exceptions* est le nombre de hello rapports TrackException reçues par le portail hello dans l’intervalle d’échantillonnage de hello du graphique de hello. Il n’inclut que hello exceptions traitées où vous avez écrit TrackException appelle dans votre code et n’inclut pas tous [les exceptions non gérées](app-insights-asp-net-exceptions.md). 

## <a name="alerts"></a>Alertes
Comme les autres mesures, vous pouvez [définir une alerte](app-insights-alerts.md) toowarn vous si un compteur de performance est en dehors d’une limite que vous spécifiez. Ouvrez le panneau des alertes hello et cliquez sur Ajouter une alerte.

## <a name="next"></a>Étapes suivantes
* [Suivi des dépendances](app-insights-asp-net-dependencies.md)
* [Suivi des exceptions](app-insights-asp-net-exceptions.md)

