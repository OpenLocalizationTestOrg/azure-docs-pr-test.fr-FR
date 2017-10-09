---
title: aaaAzure Application Insights pour ASP.NET Core | Documents Microsoft
description: "Surveiller la disponibilité, les performances et l’utilisation.des applications Web."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 3b722e47-38bd-4667-9ba4-65b7006c074c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: a7a27f9eef1daec5b0deae9fd88906e646980659
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-aspnet-core"></a>Application Insights pour ASP.NET Core
[Application Insights](app-insights-overview.md) permet d’analyser la disponibilité, les performances et l’utilisation de votre application web. Avec commentaires hello que vous obtenez sur les performances de hello et l’efficacité de votre application Bonjour générique, vous pouvez rendre des décisions avisées sur la direction hello de conception de hello dans chaque cycle de vie de développement.

![Exemple](./media/app-insights-asp-net-core/sample.png)

Tout d’abord, vous avez besoin d’un abonnement à [Microsoft Azure](http://azure.com). Connectez-vous avec un compte Microsoft, que vous pouvez avoir pour Windows, XBox Live ou d’autres services cloud de Microsoft. Votre équipe peut avoir un abonnement d’organisation de tooAzure : demander hello propriétaire tooadd tooit à l’aide de votre compte Microsoft.

## <a name="getting-started"></a>Prise en main

* Dans l’Explorateur de solutions Visual Studio, cliquez avec le bouton droit sur votre projet et sélectionnez **Configurer Application Insights**, ou **Ajouter > Application Insights**. [En savoir plus](app-insights-asp-net.md).
* Si vous ne voyez pas ces commandes de menu, suivez hello [manuel guide Mise en route de démarré](https://github.com/Microsoft/ApplicationInsights-aspnetcore/wiki/Getting-Started). Vous devrez peut-être toodo cela si votre projet a été créé avec une version de Visual Studio avant 2017.

## <a name="using-application-insights"></a>Utilisation d’Application Insights
L’authentification à hello [portail Microsoft Azure](https://portal.azure.com), sélectionnez **toutes les ressources** ou **Application Insights**, puis sélectionnez les ressources hello vous avez créé toomonitor votre application.

Dans une fenêtre de navigateur distincte, utilisez votre application pendant un certain temps. Vous verrez les données figurant dans les graphiques d’Application Insights hello. (Vous devez peut-être tooclick actualisation.) Il y aura seulement une petite quantité de données pendant que vous effectuerez le développement, mais ces graphiques seront vraiment actifs lorsque vous publierez votre application et que vous aurez de nombreux utilisateurs. 

page Vue d’ensemble de Hello montre des graphiques de performances clés : temps de réponse de serveur, les temps de chargement de page et le nombre de demandes ayant échoué. Cliquez sur n’importe quel toosee graphique plusieurs graphiques et les données.

Vues dans le portail de hello se répartissent en trois catégories principales :

* [Metrics Explorer](app-insights-metrics-explorer.md) montre des graphiques et des tables de mesures et les nombres, tels que les temps de réponse, les taux d’échec ou les métriques vous créez vous-même avec hello [API](app-insights-api-custom-events-metrics.md). Filtre et le segment de données hello par tooget de valeurs de propriété une meilleure compréhension de votre application et ses utilisateurs.
* [L’Explorateur de recherche](app-insights-diagnostic-search.md) répertorie les événements individuels, tels que des requêtes spécifiques, des exceptions, des suivis de journal ou des événements que vous avez créées avec hello [API](app-insights-api-custom-events-metrics.md). Filtrer et rechercher dans les événements hello et naviguer entre les problèmes de tooinvestigate événements connexes.
* [Analytics](app-insights-analytics.md) vous permet d’exécuter des requêtes SQL sur vos données de télémétrie. Il s’agit d’un puissant outil d’analyse et de diagnostic.

## <a name="alerts"></a>Alertes
* Vous obtenez automatiquement des [alertes de diagnostic proactives](app-insights-proactive-diagnostics.md) qui vous informent de modifications anormales des taux d’échec et d’autres mesures.
* Configurer [les tests de disponibilité](app-insights-monitor-web-app-availability.md) tootest votre site Web en permanence à partir d’emplacements dans le monde et get envoie par courrier électronique dès qu’un test échoue.
* Configurer [alertes métriques](app-insights-monitor-web-app-availability.md) tooknow si les métriques telles que le temps de réponse ou taux d’exception accédez situent hors des limites acceptables.

## <a name="video"></a>Vidéo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player] 

## <a name="open-source"></a>Open source
[Lire et y contribuer toohello code](https://github.com/Microsoft/ApplicationInsights-aspnetcore#recent-updates)


## <a name="next-steps"></a>Étapes suivantes
* [Ajouter des pages web télémétrie tooyour](app-insights-javascript.md) toomonitor page performances et utilisation.
* [Surveiller les dépendances](app-insights-asp-net-dependencies.md) toosee si REST, SQL ou autres ressources externes ralentissent vous.
* [Utilisez les API hello](app-insights-api-custom-events-metrics.md) toosend vos propres mesures pour une vue plus détaillée des performances et d’utilisation de votre application et les événements.
* [Tests de disponibilité](app-insights-monitor-web-app-availability.md) Vérifiez votre application en permanence à partir de monde hello. 

