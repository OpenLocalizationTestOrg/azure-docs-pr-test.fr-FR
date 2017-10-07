---
title: "aaaInvestigate et le partage des données d’utilisation avec des classeurs interactifs dans Azure Application Insights | Documents Microsoft"
description: "Analyse démographique des utilisateurs de votre application web."
services: application-insights
documentationcenter: 
author: numberbycolors
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 06/12/2017
ms.author: bwren
ms.openlocfilehash: bdcebe0f97fdad0a0b301df5950dc09698f5a4dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="investigate-and-share-usage-data-with-interactive-workbooks-in-application-insights"></a>Examiner et de partager des données d’utilisation avec des classeurs interactifs dans Azure Application Insights

Les classeurs associent des visualisations de données [Azure Application Insights](app-insights-overview.md), [des requêtes Analytics](app-insights-analytics.md)et du texte dans des documents interactifs. Les classeurs sont modifiables par les autres membres de l’équipe avec accès toohello même ressource Azure. Cela signifie hello des requêtes et des contrôles utilisé toocreate un classeur sont disponibles tooother visiteurs de classeur de hello, ce qui les rend facile tooexplore, étendre et recherchez les erreurs.

Les classeurs sont utiles pour :

* Explorer l’utilisation de hello de votre application lorsque vous ne connaissez pas les métriques hello d’intérêt à l’avance : nombre d’utilisateurs, les taux de rétention, les taux de conversion, etc.. Contrairement à d’autres outils d’analyse d’utilisation d’Application Insights, les classeurs vous permettent de combiner plusieurs types de visualisations et d’analyses, ce qui les rend très utile pour ce type d’exploration sous forme libre.
* Expliquant l’équipe tooyour fonctionne d’une fonctionnalité qui vient d’être publiée, en affichant l’utilisateur compte pour les interactions clées et d’autres métriques.
* Partage des résultats hello d’un A / B expérience suivant dans votre application avec d’autres membres de votre équipe. Vous pouvez expliquer les objectifs hello pour hello faire des essais avec le texte, puis affichent les métriques d’utilisation et les requête Analytique utilisé tooevaluate l’expérience hello, ainsi que d’effacer des légendes pour indiquer si chaque mesure a été au-dessus ou au-dessous-cible.
* Création de rapports impact hello d’une panne sur l’utilisation de hello de votre application, en combinant des données, explication du texte et une description des pannes de tooprevent étapes suivants Bonjour futures.

> [!NOTE]
> Votre ressource Application Insights doit contenir des vues de page ou les classeurs toouse événements personnalisés. [Découvrez comment tooset votre page de toocollect application affiche automatiquement par hello Application Insights JavaScript SDK](app-insights-javascript.md).
> 
> 

## <a name="editing-rearranging-cloning-and-deleting-workbook-sections"></a>Modifier, réorganiser, cloner et supprimer des sections de classeur

Un classeur est composé de sections : visualisations d’utilisation, graphiques, tables, texte ou résultats de requête Analytics modifiables de manière indépendante.

contenu de hello tooedit d’une section du classeur, cliquez sur hello **modifier** bouton ci-dessous et toohello à droite de la section de classeur hello.

![Commandes d’édition de la section Workbooks d’Application Insights](./media/app-insights-usage-workbooks/editing-controls.png)

1. Lorsque vous avez terminé une section, cliquez sur **fait modification** dans hello coin inférieur gauche de la section de hello.

2. toocreate un doublon d’une section, cliquez sur hello **cloner cette section** icône. Création de sections en double est un tooiterate tooway excellent sur une requête sans perdre les itérations précédentes.

3. toomove une section dans un classeur, cliquez sur hello **monter** ou **Descendre** icône.

4. tooremove une section cliquez définitivement, hello **supprimer** icône.

## <a name="adding-usage-data-visualization-sections"></a>Ajout de sections de visualisation de données d’utilisation

Les classeurs proposent quatre types de visualisations d’analyse d’utilisation intégrées. Chacune des réponses une question fréquente concernant l’utilisation de hello de votre application. tooadd tables et graphiques de ces quatre sections, ajoutez des sections de requête Analytique (voir ci-dessous).

tooadd les utilisateurs, des Sessions, des événements ou rétention section classeur tooyour, utilisez hello **ajouter des utilisateurs** ou autres bouton correspondant au bas hello du classeur de hello ou au bas hello de toute section.

![Section Utilisateurs dans Workbooks](./media/app-insights-usage-workbooks/users-section.png)

Les sections **Utilisateurs** répondent à la question « Combien d’utilisateurs ont visualisé une page ou utilisé une certaine fonctionnalité de mon site ? »

Les sections **Sessions** répondent à la question « Combien de sessions les utilisateurs ont-ils passé à afficher une page ou à utiliser certaines fonctionnalités de mon site ? »

Les sections **Événements** répondent à la question « Combien de fois les utilisateurs ont-ils affiché une page ou utilisé certaines fonctionnalités de mon site ? »

Chacun de ces types de trois sections offre hello mêmes jeux de contrôles et de visualisations :

* [En savoir plus sur la modification des sections Utilisateurs, Sessions et Événements](app-insights-usage-segmentation.md)
* Activer/désactiver le graphique principal de hello, grilles d’histogramme, insights automatique et visualisations dans les utilisateurs exemple hello **afficher le graphique**, **afficher la grille de**, **afficher les analyses**et **De ces utilisateurs** cases à cocher en haut de hello de chaque section.

![Section Rétention dans Workbooks](./media/app-insights-usage-workbooks/retention-section.png)

Les sections **Rétention** répondent à la question « Sur les personnes ayant affiché une page ou utilisé des fonctionnalités un jour ou une semaine donnée, combien sont revenues le jour ou la semaine suivante ? »

* [En savoir plus sur la modification des sections Rétention](app-insights-usage-retention.md)
* Graphique rétention globale facultatif hello bascule à l’aide de hello **afficher le graphique de rétention global** case à cocher en haut de hello de section de hello.

## <a name="adding-application-insights-analytics-sections"></a>Ajout de sections Application Insights Analytics

![Section Analytics dans Workbooks](./media/app-insights-usage-workbooks/analytics-section.png)

tooadd un classeur Application Insights Analytique requête section tooyour, utilisez hello **requête d’ajouter l’Analytique** bouton bas hello du classeur de hello, ou en bas de hello de n’importe quelle section.

Les sections de requête Analytics vous permettent d’ajouter des requêtes arbitraires sur vos données Application Insights dans les classeurs. Cette flexibilité signifie sections de requête Analytique doivent être votre go-toofor répondre aux questions relatives à votre site autre que hello quatre répertoriés ci-dessus pour les utilisateurs, les Sessions, les événements et rétention, telles que :

* Nombre d’exceptions a votre lève site pendant hello même période comme une baisse de l’utilisation ?
* Quel était distribution hello de temps de chargement de page pour les utilisateurs à afficher une page ?
* Combien d’utilisateurs ont affiché certaines pages de votre site en particulier ? Cela peut être utile toounderstand si vous avez des groupes d’utilisateurs qui utilisent différents sous-ensembles de la fonctionnalité de votre site (utilisez hello `join` opérateur avec hello `kind=leftanti` modificateur Bonjour langage de requête Analytique de journal).

Hello d’utilisation [référence du langage de requête Analytique de journal](https://docs.loganalytics.io/) toolearn plus d’informations sur l’écriture de requêtes.

## <a name="adding-text-and-markdown-sections"></a>Ajout de texte et de sections Markdown

Ajout des en-têtes, des explications et des classeurs tooyour commentaires permet de transformer un ensemble de tables et graphiques une narration. Prend en charge les sections de texte dans les classeurs hello [syntaxe Markdown](https://daringfireball.net/projects/markdown/) pour la mise en forme, telles que des en-têtes, gras, italique et les listes à puces.

tooadd un classeur tooyour de la section de texte, utilisez hello **ajouter du texte** bouton bas hello du classeur de hello, ou en bas de hello de n’importe quelle section.

## <a name="saving-and-sharing-workbooks-with-your-team"></a>Enregistrer et partager des classeurs avec votre équipe

Les classeurs sont enregistrés au sein d’une ressource Application Insights, Bonjour **Mes rapports** section tooyou privé ou Bonjour **des rapports partagés** section qui est accessible tooeveryone avec accès toohello ressource Application Insights. tooview tous les classeurs hello dans la ressource de hello, cliquez sur hello **ouvrir** bouton dans la barre d’action hello.

un classeur qui n’est en cours de tooshare **Mes rapports**:

1. Cliquez sur **ouvrir** dans la barre d’action hello
2. Cliquez sur le bouton «... » hello en regard de classeur de hello souhaité tooshare
3. Cliquez sur **déplacer tooShared rapports**.

tooshare un classeur avec un lien ou par courrier électronique, cliquez sur **partage** dans la barre d’action hello. Gardez à l’esprit que les destinataires de lien de hello besoin d’accès toothis des ressources dans le classeur de hello hello tooview portail Azure. toomake les modifications, les destinataires doivent disposer au moins des autorisations de collaborateur pour la ressource de hello.

toopin un tooan de classeur tooa lien du tableau de bord Azure :

1. Cliquez sur **ouvrir** dans la barre d’action hello
2. Cliquez sur le bouton «... » hello en regard de classeur de hello souhaité toopin
3. Cliquez sur **toodashboard du code confidentiel**.

## <a name="next-steps"></a>Étapes suivantes

## <a name="next-steps"></a>Étapes suivantes
- l’utilisation de tooenable rencontre, démarrer l’envoi de [événements personnalisés](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) ou [des consultations de page](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).
- Si vous envoyez déjà hello l’utilisation des outils toolearn Explorer les événements personnalisés ou des vues de la page, comment les utilisateurs utiliser votre service.
    - [Utilisateurs, sessions, événements](app-insights-usage-segmentation.md)
    - [Entonnoirs](usage-funnels.md)
    - [Rétention](app-insights-usage-retention.md)
    - [Flux d’utilisateurs](app-insights-usage-flows.md)
    - [Ajouter du contexte utilisateur](app-insights-usage-send-user-context.md)
    
