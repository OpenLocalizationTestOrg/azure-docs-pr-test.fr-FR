---
title: "analyse de rétention aaaUser pour les applications web avec Azure Application Insights | Documents Microsoft"
description: "Nombre d’utilisateurs retourne tooyour application ?"
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
ms.openlocfilehash: 8bcee5f1611afbd69016ec3eef27832c304762a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="user-retention-analysis-for-web-applications-with-application-insights"></a>Analyse de la rétention utilisateur des applications web avec Azure Application Insights

fonctionnalité de rétention Hello [Azure Application Insights](app-insights-overview.md) vous aide à vous analysez le nombre d’utilisateurs retourner tooyour application, et la fréquence à laquelle effectuer des tâches particulières ou objectifs. Par exemple, si vous exécutez un site de jeu, vous pouvez comparer les numéros de hello d’utilisateurs qui retournent des toohello site après la perte d’un jeu avec un nombre de hello retournent après gagnante. Cette information peut vous aider à améliorer l’expérience de vos utilisateurs et votre stratégie commerciale.

## <a name="get-started"></a>Prise en main

Si vous ne voyez encore des données dans l’outil de rétention hello dans le portail Application Insights hello, [apprendre comment tooget démarrer avec les outils de l’utilisation de hello](app-insights-usage-overview.md).

## <a name="hello-retention-tool"></a>outil de conservation Hello

![Outil de rétention](./media/app-insights-usage-retention/retention.png)

1. barre d’outils Hello permet aux utilisateurs des rapports de rétention toocreate, ouvrir les rapports existants de rétention, enregistrer le rapport de rétention actuelle ou enregistrer sous, rétablir les modifications apportées toosaved rapports, actualiser les données sur le rapport de hello, partage un rapport par e-mail ou un lien direct et hello d’accès page de la documentation. 
2. Par défaut, la rétention affiche tous les utilisateurs qui ont effectué une action, puis sont revenus et ont effectué une autre action sur une période donnée. Vous pouvez sélectionner une combinaison différente des événements toonarrow hello se concentrer sur les activités des utilisateurs spécifiques.
3. Ajoutez un ou plusieurs filtres sur les propriétés. Par exemple, vous pouvez cibler les utilisateurs d’un pays ou d’une région spécifique. Cliquez sur **mise à jour** après avoir défini les filtres hello. 
4. Hello graphique de rétention globale affiche un résumé de la rétention de l’utilisateur entre hello période sélectionnée. 
5. grille de Hello montre nombre hello d’utilisateurs retenu conséquente Générateur de requêtes toohello # 2. Chaque ligne représente une cohorte d’utilisateurs ayant exécuté n’importe quel événement dans le temps de hello période affichée. Chaque cellule dans la ligne de hello montre retournée, combien de que cohorte au moins une fois dans une période ultérieure. Certains utilisateurs peuvent revenir pendant plusieurs périodes. 
6. les cartes insights Hello affichent les cinq principaux événements initiateur et cinq premiers retournée aux utilisateurs de toogive événements une meilleure compréhension de leur rapport de rétention. 

![Passage de la souris sur la fonction de rétention](./media/app-insights-usage-retention/hover.png)

Les utilisateurs peuvent pointer sur les cellules de bouton de hello rétention outil tooaccess hello analytique et signifie que les info-bulles expliquant quelle cellule hello. bouton d’Analytique Hello prend outil d’Analytique toohello utilisateurs avec des utilisateurs toogenerate requête prédéfinie à partir de la cellule de hello. 

## <a name="use-business-events-tootrack-retention"></a>Utiliser la rétention de tootrack événements business

tooget hello plus utiles rétention analysis, des événements de mesures qui représentent des activités d’entreprise importantes. 

Par exemple, de nombreux utilisateurs peuvent ouvrir une page dans votre application sans jeu hello qu’il affiche. Suivi uniquement les vues de page hello fournirait une estimation inexacte de combien de personnes retourne tooplay jeu de hello après elle précédemment. tooget une image claire de retourner des lecteurs, votre application doit envoyer un événement personnalisé lorsqu’un utilisateur est lu réellement.  

Il est conseillé toocode des événements personnalisés qui représentent des actions de la clé d’entreprise et les utilisent pour votre analyse de rétention. résultat de jeu hello toocapture, vous devez toowrite une ligne de code toosend une tooApplication d’événement personnalisé Insights. Si vous l’écrire dans le code de page web hello ou Node.JS, il ressemble à ceci :

```JavaScript
    appinsights.trackEvent("won game");
```

Ou dans le code de serveur ASP.NET :

```C#
   telemetry.TrackEvent("won game");
```

[Familiarisez-vous avec l’écriture d’événements personnalisés](app-insights-api-custom-events-metrics.md#trackevent).


## <a name="next-steps"></a>Étapes suivantes
- l’utilisation de tooenable rencontre, démarrer l’envoi de [événements personnalisés](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) ou [des consultations de page](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).
- Si vous envoyez déjà hello l’utilisation des outils toolearn Explorer les événements personnalisés ou des vues de la page, comment les utilisateurs utiliser votre service.
    - [Utilisateurs, sessions, événements](app-insights-usage-segmentation.md)
    - [Entonnoirs](usage-funnels.md)
    - [Flux d’utilisateurs](app-insights-usage-flows.md)
    - [Classeurs](app-insights-usage-workbooks.md)
    - [Ajouter du contexte utilisateur](app-insights-usage-send-user-context.md)


