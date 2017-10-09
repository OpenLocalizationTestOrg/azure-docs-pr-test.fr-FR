---
title: "modèles de navigation aaaAnalyze utilisateur avec le flux de l’utilisateur dans Azure Application Insights | Documents Microsoft"
description: "Analyser la façon dont les utilisateurs naviguent entre les pages hello et les fonctionnalités de votre application web."
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
ms.openlocfilehash: d3f35dc78e9874e4b7974604bf91c40a5e5b78eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-user-navigation-patterns-with-user-flows-in-application-insights"></a>Analyser les modèles de navigation utilisateur avec User Flows dans Azure Application Insights

![Outil User Flows d’Application Insights](./media/app-insights-usage-flows/flows.png)

outil d’utilisateur flux Hello visualise la façon dont les utilisateurs naviguent entre les pages hello et les fonctionnalités de votre site. Il est idéal pour répondre à certaines questions que vous vous posez, par exemple :
* Qu’est-ce qui pousse les utilisateurs à quitter une page de votre site ?
* Sur quel contenu d’une page de votre site les utilisateurs cliquent-ils ?
* Où sont hello place que les utilisateurs évolution du meilleur parti de votre site ?
* Existe-t-il des emplacements où les utilisateurs répétition hello même action continuellement ?

outil d’utilisateur flux Hello démarre à partir d’un affichage de page initial ou un événement que vous spécifiez. Étant donné cette vue de page ou d’un événement personnalisé, flux d’utilisateur affiche hello vues de page et les événements personnalisés que les utilisateurs envoyés immédiatement par la suite pendant une session, deux étapes par la suite, et ainsi de suite. Des lignes d’épaisseur variable montrent le nombre de fois où les utilisateurs ont suivi chaque parcours. Nœuds spéciaux de « Session s’est terminée » indiquent combien d’utilisateurs envoyé sans les vues de page ou les événements personnalisés après hello précédant le nœud, là où les utilisateurs se probablement votre site de la mise en surbrillance.



> [!NOTE]
> Votre ressource Application Insights doit contenir des vues de page ou outil de flux de l’utilisateur des événements personnalisés toouse hello. [Découvrez comment tooset votre page de toocollect application affiche automatiquement par hello Application Insights JavaScript SDK](app-insights-javascript.md).
> 
> 

## <a name="start-by-choosing-an-initial-page-view-or-custom-event"></a>Commencez par choisir une page consultée ou un événement personnalisé initial(e)

![Choisissez un événement initial pour User Flows](./media/app-insights-usage-flows/flows-initial-event.png)

tooget démarré les réponses aux questions avec l’outil d’utilisateur flux hello, choisissez un affichage de page initial ou un événement personnalisé tooserve en tant que point de départ pour la visualisation de hello de hello :
1. Cliquez sur le lien hello Bonjour » que les utilisateurs faire après... ? » titre, ou cliquez sur le bouton Modifier de hello. 
2. Sélectionnez un affichage de page ou d’un événement personnalisé à partir de la liste déroulante de « Événement Initial » hello.
3. Cliquez sur « Create graph » (Créer un graphique).

colonne de « Étape 1 » de Hello de visualisation de hello indique ce que les utilisateurs fait plus souvent juste après l’événement initial hello, classés de haut en bas à partir de la plupart tooleast fréquentes. Hello « Étape 2 » et les colonnes suivantes indiquent quels utilisateurs a par la suite, la création d’une image de tous les utilisateurs de façons hello ont accédé à votre site.

Par défaut, l’outil d’utilisateur flux hello échantillonne hello uniquement des dernières 24 heures de vues de page et l’événement personnalisé à partir de votre site. Vous pouvez augmenter l’intervalle de temps hello et modifier hello équilibre entre les performances et la précision de l’échantillonnage aléatoire dans le menu Edition de hello.

Si certaines des vues de page hello et événements personnalisés ne sont pas pertinentes tooyou, cliquez sur hello « X » sur les nœuds hello souhaité toohide. Une fois que vous avez sélectionné les nœuds hello toohide, cliquez sur bouton « Graphique de créer » hello visualisation de hello. toosee tous les nœuds hello vous avez masqués, cliquez sur le bouton Modifier de hello, puis examinez la section de « Exclure les événements » hello.

Si les vues de page ou des événements personnalisés sont manquants escompté toosee de visualisation de hello :
* Vérifiez hello « Exclure les événements » section dans le menu Edition de hello.
* Utiliser le contrôle de « Niveau de détail » hello hello modifier menu tooinclude moins fréquentes dans les événements dans la visualisation de hello.
* Si l’affichage de page hello ou un événement personnalisé souhaitées est rarement envoyé par les utilisateurs, essayez de plage de temps hello croissante de visualisation hello dans le menu Edition de hello.
* Assurez-vous qu’affichage de page hello ou un événement personnalisé souhaitées toobe collecté par hello Application Insights SDK dans le code source de hello de votre site est configurée. [En savoir plus sur la collecte d’événements personnalisés.](app-insights-api-custom-events-metrics.md)

Si vous souhaitez toosee plusieurs étapes dans la visualisation hello, utilisez hello « Nombre d’étapes » curseur Bonjour menu Edition.

## <a name="after-visiting-a-page-or-feature-where-do-users-go-and-what-do-they-click"></a>Après avoir consulté une page ou une fonctionnalité, où vont les utilisateurs et sur quoi cliquent-ils ?

![Utilisez toounderstand de flux de l’utilisateur dans lequel les utilisateurs cliquent sur](./media/app-insights-usage-flows/flows-one-step.png)

Si votre événement initial est un affichage de page, hello la première colonne (« étape 1 ») de visualisation de hello est un toounderstand rapidement quels utilisateurs a immédiatement après la visite de page de hello. Essayez d’ouvrir votre site dans un flux d’utilisateur de visualisation de toohello suivant fenêtre. Comparez vos attentes en matière d’interagissent des utilisateurs avec liste des toohello page hello d’événements dans la colonne « Étape 1 » de hello. Souvent, un élément d’interface utilisateur sur la page hello qui semble non significatifs tooyour team peut être entre hello utilisés dans la page de hello. Il peut être un excellent point de départ pour le site de tooyour améliorations de conception.

Si votre événement initial est un événement personnalisé, hello première colonne montre ce que les utilisateurs fait juste après l’exécution de cette action. Comme avec les vues de page, considérez si hello observé le comportement de vos utilisateurs correspond aux objectifs et des attentes de votre équipe. Si votre événement initial sélectionné est « Added élément tooShopping panier », par exemple, recherchez toosee si « Atteindre tooCheckout » et « Achat terminée » s’affichent dans la visualisation de hello peu de temps après. Si le comportement de l’utilisateur est très différent de vos attentes, utilisez toounderstand de visualisation hello comment les utilisateurs sont mise en route » interceptées « conception d’actuelle de votre site.

## <a name="where-are-hello-places-that-users-churn-most-from-your-site"></a>Où sont hello place que les utilisateurs évolution du meilleur parti de votre site ?

Espion pour les nœuds « Session s’est terminée » qui s’affichent à distance haute dans une colonne dans la visualisation hello, en particulier au début d’un flux. Cela signifie que de nombreux utilisateurs probablement modifiées à partir de votre site après que suivant hello chemin d’accès précédent de pages et les interactions de l’interface utilisateur. On s’attend parfois très logiquement à ce qu’un utilisateur quitte un site, par exemple après avoir effectué un achat sur un site de commerce électronique. Mais le départ d’un site est aussi révélateur de problèmes de conception, de performances médiocres ou d’autres problèmes liés à votre site et qui peuvent être améliorés.

Gardez à l’esprit que les nœuds « Fin de session » sont basés uniquement sur les données de télémétrie collectées par cette ressource Application Insights. Si l’Application Insights ne reçoit pas les données de télémétrie pour certaines des interactions utilisateur, les utilisateurs peuvent toujours ont d’interagir avec votre site dans les cas une fois que l’outil d’utilisateur flux hello indique hello session s’est terminée.

## <a name="are-there-places-where-users-repeat-hello-same-action-over-and-over"></a>Existe-t-il des emplacements où les utilisateurs répétition hello même action continuellement ?

Recherchez un affichage de page ou d’un événement personnalisé qui est répétée dans les étapes suivantes dans la visualisation de hello par de nombreux utilisateurs. Cela signifie généralement que les utilisateurs effectuent des actions répétitives sur votre site. Si vous trouvez la répétition, pensez à la modification de conception hello de votre site ou l’ajout de répétition de tooreduce nouvelle fonctionnalité. Par exemple, ajoutez une fonctionnalité de modification en bloc si vous constatez que des utilisateurs effectuent des actions répétitives sur chaque ligne d’un élément de table.

## <a name="common-questions"></a>Questions courantes

### <a name="why-do-steps-appear-disconnected"></a>Pourquoi les étapes apparaissent-elles comme déconnectées ?

![User Flows avec étapes déconnectées](./media/app-insights-usage-flows/flows-disconnected.png)

Si les étapes (colonnes) dans une visualisation transite par utilisateur sont déconnectées, cela signifie aucun des chemins d’accès hello prises par les utilisateurs entre les étapes de hello suffisamment fréquente toobe indiqué. tooshow moins fréquents événements sur la visualisation de hello les étapes de hello apparaissent donc connectés, ajustez le curseur de « Niveau de détail » de hello dans le menu Edition de hello.

### <a name="does-hello-initial-event-represent-hello-first-time-hello-event-appears-in-a-session-or-any-time-it-appears-in-a-session"></a>Hello initiale représentent hello première heure hello d’événement apparaît dans une session, ou n’importe quel moment il apparaît dans une session ?

événement initial de Hello sur la visualisation de hello représente uniquement hello première fois, qu'un utilisateur a envoyé cette vue de page ou d’un événement personnalisé pendant une session. Si les utilisateurs peuvent envoyer un événement initial de hello plusieurs fois dans une session, colonne de « Étape 1 » hello affiche uniquement le comportement des utilisateurs après hello *premier* instance d’événement initial, pas toutes les instances.

## <a name="next-steps"></a>Étapes suivantes

* [Vue d’ensemble de l’utilisation](app-insights-usage-overview.md)
* [Utilisateurs, Sessions et Événements](app-insights-usage-segmentation.md)
* [Rétention](app-insights-usage-retention.md)
* [Ajout d’événements personnalisés tooyour app](app-insights-api-custom-events-metrics.md)
