---
title: "aaaSmart détection dans Azure Application Insights | Documents Microsoft"
description: "Application Insights réalise une analyse télémétrique approfondie automatique de votre application et vous avertit des éventuels problèmes de performances."
services: application-insights
documentationcenter: windows
author: rakefetj
manager: carmonm
ms.assetid: 2eeb4a35-c7a1-49f7-9b68-4f4b860938b2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: bwren
ms.openlocfilehash: f794476088fc69154eda2077b7a5cdc769fab3a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="smart-detection-in-application-insights"></a>Détection intelligente dans Application Insights
 La détection intelligente vous informe automatiquement des éventuels problèmes de performances dans votre application web. Il effectue une analyse proactive de télémétrie hello que votre application envoie trop[Application Insights](app-insights-overview.md). S’ils détectent une augmentation soudaine du taux d’échec, ou des modèles anormaux de performances client ou serveur, vous recevez une alerte. Cette fonctionnalité ne nécessite aucune configuration. Elle fonctionne si votre application envoie suffisamment de données de télémétrie.

Vous pouvez accéder à des alertes de détection actives à la fois à partir de messages hello et à partir du Panneau de Smart détection hello.

## <a name="review-your-smart-detections"></a>Passer en revue vos détections intelligentes
Vous pouvez découvrir des détections de deux manières :

* **Vous recevez un message électronique** de la part d’Application Insights. Voici un exemple typique :
  
    ![Alerte par courrier électronique](./media/app-insights-proactive-diagnostics/03.png)
  
    Cliquez sur hello grand bouton tooopen plus en détail dans le portail de hello.
* **vignette de détection actives Hello** sur une vue d’ensemble de votre application panneau affiche un nombre d’alertes récentes. Cliquez sur hello vignette toosee une liste des alertes récentes.

![Afficher les détections récentes](./media/app-insights-proactive-diagnostics/04.png)

Sélectionnez une alerte toosee ses détails.

## <a name="what-problems-are-detected"></a>Quels sont les problèmes détectés ?
Il existe trois types de détection :

* [Détection intelligente des anomalies de type échec](app-insights-proactive-failure-diagnostics.md). Nous utilisons apprentissage tooset les taux de hello attendu de demandes ayant échoué pour votre application, la mise en corrélation avec la charge et d’autres facteurs. Si le taux d’échec hello est en dehors de l’enveloppe attendu de hello, nous envoyer une alerte.
* [Détection intelligente des anomalies de performances](app-insights-proactive-performance-diagnostics.md). Pour obtenir des notifications si le temps de réponse d’une durée de l’opération ou la dépendance est ralentissent toohistorical comparés de ligne de base ou si nous d’identifier un modèle anormal dans le temps de réponse ou de temps de chargement de page.   
* [Détection intelligente - Dépannage de problèmes de service cloud Azure](https://azure.microsoft.com/blog/proactive-notifications-on-cloud-service-issues-with-azure-diagnostics-and-application-insights/). Vous recevez des alertes si votre application est hébergée dans Azure Cloud Services et qu’une instance de rôle présente des échecs de démarrage, un recyclage fréquent ou des erreurs d’exécution.

(liens d’aide hello dans chaque notification vous prennent les articles pertinents toohello.)

## <a name="video"></a>Vidéo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>Étapes suivantes
Ces outils de diagnostic vous aident à inspecter les données de télémétrie hello à partir de votre application :

* [Metrics Explorer](app-insights-metrics-explorer.md)
* [Navigateur de recherche](app-insights-diagnostic-search.md)
* [Analytics : un puissant langage de requête](app-insights-analytics-tour.md)

La détection intelligente est entièrement automatique. Mais peut-être voudriez-vous tooset certaines alertes plus ?

* [Alertes de mesures configurées manuellement](app-insights-alerts.md)
* [Tests web de disponibilité](app-insights-monitor-web-app-availability.md) 

