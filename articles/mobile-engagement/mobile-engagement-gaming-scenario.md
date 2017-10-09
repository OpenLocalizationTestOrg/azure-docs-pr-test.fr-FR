---
title: "implémentation de Mobile Engagement aaaAzure pour l’application de jeu"
description: "Jeu tooimplement de scénario d’application Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2cafc044-4902-4058-8037-49399bf6bf7f
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: b82b4a868a33f42e5b759e43e66103556c097f9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="implement-mobile-engagement-with-gaming-app"></a>Mise en œuvre de Mobile Engagement avec une application de jeu
## <a name="overview"></a>Vue d'ensemble
Une jeune entreprise spécialisée dans les jeux a lancé un nouveau jeu de rôle/de stratégie sur le thème de la pêche. jeu de Hello est en cours d’exécution pendant 6 mois. Ce jeu est un succès considérable et il a des millions de téléchargements et la rétention de hello est applications de jeu de démarrage très élevé tooother comparés. À la réunion de révision de tous les trimestres de hello, les parties prenantes estiment que dont ils ont besoin de chiffre d’affaires moyen tooincrease par l’utilisateur (revenu moyen par abonné). Des packages au sein du jeu sont disponibles sous forme d’offres spéciales. Ces packs jeu autoriser l’apparence de hello tooupgrade les utilisateurs et les performances de leurs lignes de pêche et appâts ou de s’attaque dans le jeu de hello. Toutefois, les ventes de package sont très faibles. Afin de déterminer leur premier tooanalyze hello de l’expérience utilisateur avec un outil analytique, et puis toodevelop un engagement programme tooincrease ventes à l’aide de gestion avancée segmentation.

En fonction de hello [Azure Mobile Engagement - Guide de démarrage avec les meilleures pratiques](mobile-engagement-getting-started-best-practices.md) qu’ils génèrent une stratégie d’engagement.

## <a name="objectives-and-kpis"></a>Objectifs et indicateurs clés de performance
Principales parties prenantes pour répondre aux jeux de hello. Tous les s’accorder sur un objectif principal - ventes de package tooincrease premium de 15 %. Ils créent lecteur et entreprise indicateurs de Performance clés (KPI) toomeasure cet objectif

* Sur quel niveau de jeu de hello ces packages sont achetés ?
* Quel est le chiffre d’affaires hello par utilisateur, par session, par semaine et par mois ?
* Quels sont les types de fournisseur favori hello ?

Partie 1 sur hello [Getting Started Guide](mobile-engagement-getting-started-best-practices.md) explique comment toodefine hello objectifs et des indicateurs de performance clés. 

Hello de qu'indicateurs de performance clés Business est maintenant défini, hello Mobile Product Manager crée rétention et les tendances des utilisateurs nouveaux indicateurs de performance clés Engagement toodetermine.

* Rétention de surveiller et d’utiliser le sur hello suivant des intervalles : tous les jours, toutes les 2 jours, hebdomadaire, mensuelle et tous les 3 mois
* Nombre d’utilisateurs actifs
* classification des applications Hello Bonjour stocker

Selon les recommandations de l’équipe informatique de hello, hello suivant techniques indicateurs de performance clés ont été ajoutée hello tooanswer suivant questions :

* Quel est mon parcours utilisateur (page visitée, temps passé dessus par l’utilisateur) ?
* Quel est le nombre de pannes ou de bogues par session ?
* Quelles sont les versions de système d’exploitation exécutées par mes utilisateurs ?
* Quelle est hello de taille moyenne de l’écran pour mes utilisateurs ?
* De quels types de connectivité Internet mes utilisateurs doivent-ils disposer ?

Pour chaque indicateur de performance clé hello Mobile Product Manager spécifie les données de hello dont elle a besoin et où il se trouve dans son manuel.

## <a name="engagement-program-and-integration"></a>Programme d’engagement et intégration
Avant de générer un programme engagement avancées, hello directeur du projet Mobile responsable de projet de hello doit avoir une compréhension approfondie des quand et comment les produits sont consommés par les utilisateurs de hello.

Après 3 mois, hello directeur du projet Mobile a collecté suffisamment tooenhance données ses ventes de notification par envoi de données dans l’application. Il a notamment appris que :

* premier achat de Hello se produit généralement au niveau de hello 14. Pour 90 % des cas, achat de hello est nouvelles armes reposant pour $3.
* De 80 % des cas, les utilisateurs qui ont effectué un achat, continuez avec le produit de hello et effectuez plusieurs achats.
* Les utilisateurs qui ont passé le niveau hello 20, démarrer toospend plus de 10 $par semaine.
* Les utilisateurs ont tendance à toobuy les packages premium au niveau 16, 24 et 32.

Merci d’analyse toothis hello directeur du projet Mobile décide toocreate push spécifique notification séquences tooincrease dans les ventes de l’application. Il crée trois séquences Push qu’il nomme respectivement Bienvenue dans le programme, Programme commercial et Programme inactif. Pour plus d’informations, consultez toohello [règles](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks)![][1]

<!--Image references-->

[1]: ./media/mobile-engagement-game-scenario/notification-scenario.png

<!--Link references-->
