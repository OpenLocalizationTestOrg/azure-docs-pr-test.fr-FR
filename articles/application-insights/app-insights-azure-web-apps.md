---
title: "aaaMonitor performances d’application web Azure | Documents Microsoft"
description: "Analyse des performances des applications pour les applications web Azure. Graphique de charge et de temps de réponse, informations de dépendance et alertes sur les performances."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 0b2deb30-6ea8-4bc4-8ed0-26765b85149f
ms.service: azure-portal
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/05/2017
ms.author: bwren
ms.openlocfilehash: d1083254e5c504b18f2ac5ae2368610dc2790436
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-web-app-performance"></a>Surveillance des performances d'application web Azure
Bonjour [Azure Portal](https://portal.azure.com) vous pouvez configurer d’analyse des performances des applications pour votre [Azure web apps](../app-service-web/app-service-web-overview.md). [Azure Application Insights](app-insights-overview.md) instrumente votre application toosend télémétrie relative à son toohello activités service Application Insights, où il est stocké et analysée. Là, les graphiques de métriques et outils de recherche peuvent être utilisés toohelp diagnostiquer les problèmes, améliorer les performances et évaluer l’utilisation.

## <a name="run-time-or-build-time"></a>En cours d’exécution ou en cours de création
Vous pouvez configurer la surveillance en instrumentant application hello de deux manières :

* **En cours d’exécution** : vous pouvez sélectionner une extension de surveillance des performances lorsque votre application est déjà active. Il n’est pas toorebuild nécessaire ou réinstaller votre application. Vous obtenez un ensemble standard de packages qui analyse les temps de réponse, les taux de réussite, les exceptions, les dépendances, etc. 
* **En cours de création** : vous pouvez installer un package dans votre application en cours de développement. Cette option est plus souple. En outre toohello mêmes packages standard, vous pouvez écrire des données de télémétrie code toocustomize hello ou toosend vos propres données de télémétrie. Vous pouvez enregistrer des activités spécifiques ou enregistrer les événements selon la sémantique de toohello de votre domaine d’application. 

## <a name="run-time-instrumentation-with-application-insights"></a>Instrumentation d’exécution avec Application Insights
Si vous exécutez déjà une application web dans Azure, vous obtenez déjà certains éléments de surveillance, tels que le taux de demande et d’erreur. Ajouter Application Insights tooget de plus, telles que le temps de réponse, la surveillance toodependencies d’appels, détection active et puissant langage de requête Analytique de journal hello. 

1. **Sélectionnez l’Application Insights** dans hello Azure le panneau de configuration pour votre application web.
   
    ![Sous Surveillance, choisissez Application Insights](./media/app-insights-azure-web-apps/05-extend.png)
   
   * Choisissez toocreate une nouvelle ressource, sauf si vous avez déjà défini une ressource Application Insights pour cette application par un autre itinéraire.
2. **Instrumentez votre application web** après l’installation d’Application Insights. 
   
    ![Instrumenter votre application web](./media/app-insights-azure-web-apps/restart-web-app-for-insights.png)

   **Activer l’analyse côté client** pour la consultation de page et la télémétrie de l’utilisateur.

   * Cliquez sur Paramètres > Paramètres de l’application
   * Sous Paramètres de l’application, ajoutez une nouvelle paire clé/valeur : 
   
    Clé :`APPINSIGHTS_JAVASCRIPT_ENABLED` 
    
    Valeur: `true`
   * **Enregistrer** hello paramètres et **redémarrer** votre application.
3. **Surveillez votre application web**.  [Les données de salutation Expore](#explore-the-data).

Une version ultérieure, vous pouvez générer application hello avec Application Insights si vous le souhaitez.

*Comment supprimer l’Application Insights, ou basculez toosending tooanother ressource ?*

* Dans Azure, le panneau de contrôle web application hello ouvert et sous Outils de développement, ouvrez **Extensions**. Suppression de l’extension d’Application Insights hello. Puis sous analyse, choisissez Application Insights et créez ou sélectionnez la ressource hello souhaitée.

## <a name="build-hello-app-with-application-insights"></a>Générez l’application hello avec Application Insights
Application Insights peut fournir des données de télémétrie détaillée par l’installation d’un SDK dans votre application. En particulier, vous pouvez collecter les journaux de suivi, [écrire une télémétrie personnalisée](app-insights-api-custom-events-metrics.md), et obtenir des rapports d’exception plus détaillées.

1. **Dans Visual Studio** (2013 mise à jour 2 ou ultérieure), configurez Application Insights pour votre projet.

    Droit hello web projet, puis sélectionnez **Ajouter > Application Insights** ou **configurer Application Insights**.
   
    ![Droit hello web projet, puis choisissez Ajouter ou configurer Application Insights](./media/app-insights-azure-web-apps/03-add.png)
   
    Si vous êtes invité toosign dans, utiliser les informations d’identification de l’hello pour votre compte Azure.
   
    opération de Hello a deux effets :
   
   1. Création d’une ressource Application Insights dans Azure, à l’endroit où vos données de télémétrie sont stockées, analysées et affichées.
   2. Ajoute hello NuGet Application Insights tooyour code du package (si elle n’existait pas déjà) et il configure toosend télémétrie toohello ressource Azure.
2. **Tester les données de télémétrie hello** par application de hello en cours d’exécution sur votre ordinateur de développement (F5).
3. **Publier l’application hello** tooAzure Bonjour normalement. 

*Comment modifier les ressources d’Application Insights différent toosending tooa ?*

* Dans le projet Visual Studio, avec le bouton hello, choisissez **configurer Application Insights** et choisissez la ressource hello souhaitée. Vous obtenez hello option toocreate une nouvelle ressource. Procédez maintenant à la régénération et au redéploiement.

## <a name="explore-hello-data"></a>Explorer les données de hello
1. Sur le panneau d’Application Insights hello de votre Panneau de configuration web app, vous voyez des mesures en direct, qui affiche le nombre d’échecs et les demandes au sein d’une seconde ou deux d'entre eux qui se produisent. L’affichage de ces informations est très utile lorsque vous republiez votre application. Vous pouvez voir immédiatement les problèmes.
2. Cliquez sur les ressources Application Insights complet toohello.

    ![Cliquez sur](./media/app-insights-azure-web-apps/view-in-application-insights.png)

    Vous pouvez également y accéder directement à partir de la navigation dans les ressources Azure.

1. Cliquez sur n’importe quel tooget graphique plus en détail :
   
    ![Dans Panneau de vue d’ensemble hello Application Insights, cliquez sur un graphique](./media/app-insights-azure-web-apps/07-dependency.png)
   
    Vous pouvez [personnaliser les panneaux de mesures](app-insights-metrics-explorer.md).
2. Parcourez les plus toosee des événements individuels et leurs propriétés :
   
    ![Cliquez sur un tooopen de type d’événement filtrée par une recherche sur ce type](./media/app-insights-azure-web-apps/08-requests.png)
   
    Notez que hello tooopen du lien «... » toutes les propriétés.
   
    Vous pouvez [personnaliser les recherches](app-insights-diagnostic-search.md).

Pour les recherches plus puissantes sur vos données de télémétrie, utilisez hello [de langage de requête Analytique de journal](app-insights-analytics-tour.md).

## <a name="more-telemetry"></a>Données de télémétrie supplémentaires

* [Données de chargement de pages web](app-insights-javascript.md)
* [Télémétrie personnalisée](app-insights-api-custom-events-metrics.md)

## <a name="video"></a>Vidéo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>Étapes suivantes
* [Exécuter le Générateur de profils hello sur votre application en temps réel](app-insights-profiler.md).
* [Azure Functions](https://github.com/christopheranderson/azure-functions-app-insights-sample) - analyse les fonctions Azure avec Application Insights
* [Activer les diagnostics Azure](app-insights-azure-diagnostics.md) toobe envoyé tooApplication Insights.
* [Surveiller les mesures de contrôle d’intégrité de service](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) toomake que votre service est disponible et réactive.
* [Réceptions de notifications d’alerte](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) lorsque des événements opérationnels se produisent ou que des mesures dépassent un seuil.
* Utilisez [Application Insights pour les applications JavaScript avec des pages web](app-insights-javascript.md) télémétrie de client tooget à partir de navigateurs hello visiter une page web.
* [Configurer des tests web de disponibilité](app-insights-monitor-web-app-availability.md) toobe alerté si votre site est arrêté.

