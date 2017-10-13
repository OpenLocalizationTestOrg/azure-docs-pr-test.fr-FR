---
title: "Analyser les modèles de navigation utilisateur avec User Flows dans Azure Application Insights | Microsoft Docs"
description: "Analysez la façon dont vos utilisateurs naviguent entre les pages et les fonctionnalités de votre application web."
services: application-insights
documentationcenter: 
author: numberbycolors
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 08/02/2017
ms.author: cfreeman
ms.openlocfilehash: d17ed3dff08f00a1d6a2108608e42b29f95fbd84
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="analyze-user-navigation-patterns-with-user-flows-in-application-insights"></a>Analyser les modèles de navigation utilisateur avec User Flows dans Azure Application Insights

![Outil User Flows d’Application Insights](./media/app-insights-usage-flows/flows.png)

L’outil User Flows permet de visualiser la façon dont vos utilisateurs naviguent entre les pages et les fonctionnalités de votre site. Il est idéal pour répondre à certaines questions que vous vous posez, par exemple :
* Qu’est-ce qui pousse les utilisateurs à quitter une page de votre site ?
* Sur quel contenu d’une page de votre site les utilisateurs cliquent-ils ?
* Sur quelles pages de votre site les utilisateurs finissent le plus souvent par partir ?
* Votre site comporte-t-il des pages où les utilisateurs répètent continuellement la même action ?

L’outil User Flows démarre à partir de la page consultée ou de l’événement initial(e) que vous spécifiez. À partir de cette page consultée ou de cet événement personnalisé, User Flows affiche les pages consultées et les événements personnalisés que les utilisateurs ont envoyés immédiatement après au cours d’une session, puis deux étapes plus loin, et ainsi de suite. Des lignes d’épaisseur variable montrent le nombre de fois où les utilisateurs ont suivi chaque parcours. Des nœuds spéciaux de « fin de session » indiquent combien d’utilisateurs n’ont envoyé aucune page consultée ou aucun événement personnalisé après le nœud précédent, ce qui permet d’identifier les points où les utilisateurs ont probablement quitté votre site.



> [!NOTE]
> Votre ressource Application Insights doit contenir des pages consultées ou des événements personnalisés pour pouvoir utiliser l’outil User Flows. [Découvrez comment configurer votre application pour collecter des vues de page automatiquement à l’aide du Kit de développement logiciel (SDK) JavaScript Application Insights](app-insights-javascript.md).
> 
> 

## <a name="start-by-choosing-an-initial-page-view-or-custom-event"></a>Commencez par choisir une page consultée ou un événement personnalisé initial(e)

![Choisissez un événement initial pour User Flows](./media/app-insights-usage-flows/flows-initial-event.png)

Pour commencer à utiliser l’outil User Flows pour répondre à ces questions, choisissez une page consultée ou un événement personnalisé initial(e) qui servira de point de départ pour la visualisation :
1. Cliquez sur le lien dans le titre « What do users do after... ? » (Que font les utilisateurs après...?) ou cliquez sur le bouton Edit (Édition). 
2. Sélectionnez une page consultée ou un événement personnalisé initial(e) dans la liste déroulante « Initial event » (Événement initial).
3. Cliquez sur « Create graph » (Créer un graphique).

La colonne « Step 1 » (Étape 1) de la visualisation montre les actions les plus fréquentes des utilisateurs juste après l’événement initial, classées de haut en bas de la plus fréquente à la moins fréquente. Les colonnes « Step 2 » (Étape 2) et suivantes indiquent ce que les utilisateurs ont fait ensuite, en créant une image de tous les modes de navigation des utilisateurs sur votre site.

Par défaut, l’outil User Flows échantillonne au hasard uniquement les 24 dernières heures de pages consultées et d’événements personnalisés sur votre site. Vous pouvez augmenter l’intervalle de temps et modifier l’équilibre entre les performances et la précision de l’échantillonnage aléatoire dans le menu d’édition.

Si certaines pages consultées et certains événements personnalisés ne vous semblent pas pertinents, cliquez sur le « X » sur les nœuds que vous souhaitez masquer. Une fois que vous avez sélectionné les nœuds que vous souhaitez masquer, cliquez sur le bouton « Create graph » (Créer un graphique) sous la visualisation. Pour afficher tous les nœuds que vous avez masqués, cliquez sur le bouton Edit (Édition), puis examinez la section « Excluded events » (Événements exclus).

S’il manque des pages consultées ou des événements personnalisés qui devraient normalement apparaître sur la visualisation :
* Consultez la section « Excluded events » (Événements exclus) dans le menu Edit (Édition).
* Utilisez le contrôle « Detail level » (Niveau de détail) dans le menu Edit (Édition) pour inclure les événements les moins fréquents dans la visualisation.
* Si la page consultée ou l’événement personnalisé que vous attendez est rarement envoyé par les utilisateurs, essayez d’augmenter l’intervalle de temps de la visualisation dans le menu Edit (Édition).
* Assurez-vous que la page consultée ou l’événement personnalisé que vous attendez est configuré pour être collecté par le kit de développement logiciel Application Insights dans le code source de votre site. [En savoir plus sur la collecte d’événements personnalisés.](app-insights-api-custom-events-metrics.md)

Si vous souhaitez voir davantage d’étapes dans la visualisation, utilisez le curseur « Number of steps » (Nombre d’étapes) dans le menu Edit (Édition).

## <a name="after-visiting-a-page-or-feature-where-do-users-go-and-what-do-they-click"></a>Après avoir consulté une page ou une fonctionnalité, où vont les utilisateurs et sur quoi cliquent-ils ?

![Utiliser User Flows pour savoir où cliquent les utilisateurs](./media/app-insights-usage-flows/flows-one-step.png)

Si votre événement initial est une page consultée, la première colonne, « Step 1 » (Étape 1) de la visualisation permet de comprendre rapidement ce que les utilisateurs ont fait immédiatement après avoir consulté la page. Essayez d’ouvrir votre site dans une fenêtre en regard de la visualisation User Flows. Comparez ce que vous attendez des interactions de vos utilisateurs avec la page à la liste des événements contenue dans la colonne « Step 1 » (Étape 1). Bien souvent, un élément d’interface utilisateur sur la page qui semble sans importance pour votre équipe peut compter parmi les fonctionnalités les plus utilisées de la page. Cela peut constituer un excellent point de départ pour améliorer la conception de votre site.

Si votre événement initial est un événement personnalisé, la première colonne montre ce que les utilisateurs ont fait juste après avoir exécuté cette action. Comme pour les pages consultées, regardez si le comportement observé de vos utilisateurs correspond aux objectifs et aux attentes de votre équipe. Si l’événement initial que vous avez sélectionné est « Article ajouté au panier », par exemple, vérifiez si les actions « Passer au paiement » et « Achat terminé » s’affichent dans la visualisation peu de temps après. Si le comportement de l’utilisateur est très différent de vos attentes, utilisez la visualisation pour comprendre comment les utilisateurs sont « piégés » par la conception actuelle de votre site.

## <a name="where-are-the-places-that-users-churn-most-from-your-site"></a>Sur quelles pages de votre site les utilisateurs finissent le plus souvent par partir ?

Observez les nœuds « Fin de session » qui s’affichent en haut d’une colonne dans la visualisation, en particulier au début d’un flux. Cela signifie que de nombreux utilisateurs ont probablement quitté votre site après avoir suivi le parcours précédent de pages et d’interactions avec l’interface utilisateur. On s’attend parfois très logiquement à ce qu’un utilisateur quitte un site, par exemple après avoir effectué un achat sur un site de commerce électronique. Mais le départ d’un site est aussi révélateur de problèmes de conception, de performances médiocres ou d’autres problèmes liés à votre site et qui peuvent être améliorés.

Gardez à l’esprit que les nœuds « Fin de session » sont basés uniquement sur les données de télémétrie collectées par cette ressource Application Insights. Si Application Insights ne reçoit pas de données de télémétrie pour certaines interactions de l’utilisateur, il est possible que les utilisateurs aient continué d’interagir avec votre site après que l’outil User Flows a signalé la fin de la session.

## <a name="are-there-places-where-users-repeat-the-same-action-over-and-over"></a>Votre site comporte-t-il des pages où les utilisateurs répètent continuellement la même action ?

Recherchez une page consultée ou un événement personnalisé répété(e) par de nombreux utilisateurs dans les étapes suivantes de la visualisation. Cela signifie généralement que les utilisateurs effectuent des actions répétitives sur votre site. Si vous identifiez une répétition, pensez à modifier la conception de votre site ou à ajouter de nouvelles fonctionnalités permettant de réduire cette répétition. Par exemple, ajoutez une fonctionnalité de modification en bloc si vous constatez que des utilisateurs effectuent des actions répétitives sur chaque ligne d’un élément de table.

## <a name="common-questions"></a>Questions courantes

### <a name="why-do-steps-appear-disconnected"></a>Pourquoi les étapes apparaissent-elles comme déconnectées ?

![User Flows avec étapes déconnectées](./media/app-insights-usage-flows/flows-disconnected.png)

Si des étapes (colonnes) dans une visualisation User Flows sont déconnectées, cela signifie qu’aucun des parcours suivis par les utilisateurs entre les étapes n’a été suffisamment fréquent pour être affiché. Pour afficher les événements moins fréquents sur la visualisation de manière à faire apparaître les étapes comme connectées, ajustez le curseur « Detail level » (Niveau de détail) dans le menu Edit (Édition).

### <a name="does-the-initial-event-represent-the-first-time-the-event-appears-in-a-session-or-any-time-it-appears-in-a-session"></a>L’événement initial représente-t-il la première occurrence de l’événement dans une session ou bien n’importe quel moment où l’événement se produit au cours d’une session ?

L’événement initial sur la visualisation représente uniquement la première fois qu’un utilisateur a envoyé cette page consultée ou cet événement personnalisé au cours d’une session. Si les utilisateurs peuvent envoyer l’événement initial plusieurs fois pendant une session, la colonne « Step 1 » (Étape 1) affiche uniquement le comportement des utilisateurs après la *première* instance de l’événement initial, et non pas toutes les instances.

## <a name="next-steps"></a>Étapes suivantes

* [Vue d’ensemble de l’utilisation](app-insights-usage-overview.md)
* [Utilisateurs, Sessions et Événements](app-insights-usage-segmentation.md)
* [Rétention](app-insights-usage-retention.md)
* [Ajout d’événements personnalisés à votre application](app-insights-api-custom-events-metrics.md)