---
title: "Analyse de la rétention utilisateur des applications web avec Azure Application Insights | Microsoft Docs"
description: "Combien d’utilisateurs reviennent vers votre application ?"
services: application-insights
documentationcenter: 
author: botatoes
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/03/2017
ms.author: bwren
ms.openlocfilehash: 7f7ca19ab171278bbd82f68e3822bc650b25373d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="user-retention-analysis-for-web-applications-with-application-insights"></a>Analyse de la rétention utilisateur des applications web avec Azure Application Insights

La fonction de rétention [d’Azure Application Insights](app-insights-overview.md) vous aide à analyser le nombre d’utilisateurs qui reviennent vers votre application et la fréquence à laquelle ils exécutent des tâches particulières ou atteignent des objectifs. Par exemple, si vous exécutez un site de jeu, vous pouvez comparer le nombre d’utilisateurs qui reviennent sur le site après avoir perdu à un jeu avec le nombre d’utilisateurs qui reviennent après avoir gagné. Cette information peut vous aider à améliorer l’expérience de vos utilisateurs et votre stratégie commerciale.

## <a name="get-started"></a>Prise en main

Si aucune donnée n’apparaît dans l’outil de rétention du portail Application Insights, [découvrez comment prendre en main les outils d’utilisation](app-insights-usage-overview.md).

## <a name="the-retention-tool"></a>Outil de rétention

![Outil de rétention](./media/app-insights-usage-retention/retention.png)

1. La barre d’outils permet aux utilisateurs de créer des rapports de rétention, d’ouvrir les rapports de rétention existants, d’enregistrer le rapport de rétention en cours directement ou à un autre emplacement, d’annuler les modifications apportées aux rapports enregistrés, d’actualiser les données du rapport, de partager des rapports par e-mail ou lien direct, et d’accéder à la page de documentation. 
2. Par défaut, la rétention affiche tous les utilisateurs qui ont effectué une action, puis sont revenus et ont effectué une autre action sur une période donnée. Vous pouvez choisir une combinaison différente d’événements afin de filtrer des activités utilisateur particulières.
3. Ajoutez un ou plusieurs filtres sur les propriétés. Par exemple, vous pouvez cibler les utilisateurs d’un pays ou d’une région spécifique. Cliquez sur **Mettre à jour** après avoir défini les filtres. 
4. Le graphique de rétention globale récapitule la rétention utilisateur sur la période sélectionnée. 
5. La grille affiche le nombre d’utilisateurs conservés en fonction du générateur de requêtes au point 2. Chaque ligne représente une cohorte d’utilisateurs ayant effectué l’un des événements pendant la période de temps indiquée. Chaque cellule de la ligne indique combien de cette cohorte sont revenus au moins une fois pendant une période ultérieure. Certains utilisateurs peuvent revenir pendant plusieurs périodes. 
6. Les cartes d’aperçu affichent les cinq principaux événements de lancement et les cinq principaux événements renvoyés pour aider les utilisateurs à mieux comprendre leur rapport de rétention. 

![Passage de la souris sur la fonction de rétention](./media/app-insights-usage-retention/hover.png)

Les utilisateurs peuvent survoler les cellules de l’outil de rétention pour accéder au bouton Analytics ainsi qu’à des info-bulles qui expliquent la signification de la cellule. Le bouton Analytics redirige les utilisateurs vers l’outil Analytics avec une requête prédéfinie pour générer des utilisateurs à partir de la cellule. 

## <a name="use-business-events-to-track-retention"></a>Utiliser des événements commerciaux pour suivre la rétention

Pour obtenir l’analyse de rétention la plus utile, mesurez les événements qui représentent des activités commerciales significatives. 

Par exemple, un grand nombre d’utilisateurs peuvent ouvrir une page dans votre application sans jouer au jeu qu’elle affiche. Le suivi des vues de pages uniquement fournit ainsi une estimation inexacte du nombre de personnes qui reviennent pour jouer au jeu auquel ont déjà joué. Pour obtenir une vision claire des lecteurs qui reviennent, votre application doit envoyer un événement personnalisé lorsqu’un utilisateur joue réellement.  

Il est recommandé de coder les événements personnalisés qui représentent des actions commerciales clés et de les utiliser pour votre analyse de rétention. Pour capturer le résultat du jeu, vous devez écrire une ligne de code pour envoyer un événement personnalisé à Application Insights. Si vous l’écrivez dans le code de page web ou en Node.JS, voici à quoi il ressemble :

```JavaScript
    appinsights.trackEvent("won game");
```

Ou dans le code de serveur ASP.NET :

```C#
   telemetry.TrackEvent("won game");
```

[Familiarisez-vous avec l’écriture d’événements personnalisés](app-insights-api-custom-events-metrics.md#trackevent).


## <a name="next-steps"></a>Étapes suivantes
- Pour activer les expériences d’utilisation, commencez à envoyer des [événements personnalisés](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) ou des [affichages de page](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).
- Si vous envoyez déjà des événements personnalisés ou des affichages de page, explorez les outils d’utilisation pour savoir comment les utilisateurs emploient votre service.
    - [Utilisateurs, sessions, événements](app-insights-usage-segmentation.md)
    - [Entonnoirs](usage-funnels.md)
    - [Flux d’utilisateurs](app-insights-usage-flows.md)
    - [Classeurs](app-insights-usage-workbooks.md)
    - [Ajouter du contexte utilisateur](app-insights-usage-send-user-context.md)


