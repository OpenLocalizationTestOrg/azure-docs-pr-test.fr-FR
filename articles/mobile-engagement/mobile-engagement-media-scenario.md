---
title: "implémentation de Mobile Engagement aaaAzure pour une application multimédia"
description: "Support application scénario tooimplement Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 48201cc8-4e04-485c-a8dc-d6406d23f3ed
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 6a495eb790993a30d5c03802aa9e6404fea983d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="implement-mobile-engagement-with-media-app"></a>Mise en œuvre de Mobile Engagement avec une application multimédia
## <a name="overview"></a>Vue d'ensemble
John est chef de projet mobile pour une grande société multimédia. Il a récemment lancé une nouvelle application qui enregistre un grand nombre de téléchargements. Bien qu’il ait atteint ses objectifs en matière de téléchargements, son retour sur investissement (ROI) par utilisateur n’est pas encore à la hauteur de ses espérances. 

John a déjà identifié les raisons pour lesquelles le retour sur investissement est si faible. Les utilisateurs arrêtent d’utiliser son application au bout de seulement 2 semaines, et la plupart d’entre eux ne revient jamais. Il souhaite que rétention de hello tooincrease de son application.

Après quelques tests initiaux, il a appris quand il est exigé ses utilisateurs avec des notifications push, ils ont tendance toocontinue à l’aide de son application. Les utilisateurs qui ont été inactives souvent retourne également application toohello selon qu’il les envoie des notifications. John décide tooinvest dans un type de programme de l’Engagement pour son application qui utilise le ciblage avancé avec des notifications push.

John a lu récemment hello [Azure Mobile Engagement - Guide de démarrage avec les meilleures pratiques](mobile-engagement-getting-started-best-practices.md) et a décidé de recommandations de hello tooimplement du guide de hello.

## <a name="objectives-and-kpis"></a>Objectifs et indicateurs clés de performance
Rencontre entre les différentes parties prenantes de l’application de John. Les recettes sont générées par les clics sur les annonces au fur et à mesure que les utilisateurs utilisent les médias En augmentant le contenu consommé par utilisateur, John accroît son chiffre d’affaires. Tous sont d’accord sur l’un des objectifs principaux : ventes tooincrease à partir des annonces de 25 %. Ils créent lecteur et entreprise indicateurs de Performance clés (KPI) toomeasure cet objectif

* Nombre de clics sur les annonces par utilisateur
* Nombre de pages d’articles visitées (par utilisateur/par session/par semaine/par mois...)
* Quelles sont les catégories favorites

À la suite de la réunion de John avec les différentes parties prenantes, des indicateurs clés de performance sont définis. Il suit la partie 1 sur hello [Azure Mobile Engagement - Guide de démarrage avec les meilleures pratiques](mobile-engagement-getting-started-best-practices.md). 

Ensuite, il crée hello suivant tooensure d’indicateurs de performance clés Engagement que des objectifs :

* Analyser de rétention sur hello suivant des intervalles : quotidienne, hebdomadaire, bimensuelle et mensuelle.
* Comptes d’utilisateurs actifs
* classification des applications dans l’application hello Hello stocke

Selon les recommandations de l’équipe informatique de hello, hello suivant technique indicateurs de performance clés ont été ajoutée hello tooanswer suivant questions :

* Quel est mon parcours utilisateur (pages visitées, temps passé dessus par l’utilisateur) ?
* Quel est le nombre de pannes ou de bogues par session ?
* Quelles sont les versions de système d’exploitation exécutées par mes utilisateurs ?
* Quelle est hello de taille moyenne de l’écran pour mes utilisateurs ?
* De quels types de connexions Internet mes utilisateurs doivent-ils disposer ?

Pour chaque indicateur de performance clé, il répartit les données hello requises et il l’enregistre dans l’emplacement approprié de hello de son manuel.

## <a name="engagement-program-and-integration"></a>Programme d’engagement et intégration
Maintenant que John a terminé de définir ses indicateurs clés de performance, il entame la phase de stratégie d’engagement en définissant 4 programmes d’engagement et les objectifs associés : ![][1]

John approfondit ensuite en détaillant des notifications Push pour chaque programme. Les notifications Push sont définies par cinq éléments :

1. Objectif : nouveautés objectif hello de notification de hello
2. Comment les objectif hello seront atteinte
3. Cible : qui doit recevoir des notifications de hello ?
4. Contenu : Qu’est libellé de hello et format hello de notification de hello (dans App/Out de l’application)
5. Quand : qu’est hello meilleur moment toosend cette notification push
   
    ![][2]

Pour plus d’informations, consultez toohello [règles](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks).

En fonction de toohello partie 2 de livre blanc hello que John utilise cible section toodefine les données qu’il a toocollect et écrit son étiquette Plan conjointement avec la solution de hello tooimplement informatique team. Après 1 semaine de mise en œuvre et de tests d’acceptation des utilisateurs, John peut enfin lancer ses programmes.

## <a name="program-results"></a>Résultats du programme
4 mois plus tard, John examine les performances des programmes. Hello programme Bienvenue et hello programme hebdomadaire atteignez ses objectifs. nombre de Hello d’utilisateur avec une seule session diminue, davantage de fonctionnalités de l’application hello est utilisées et nombre hello de connexions par semaine a doublé.

Hello **programme Inactive** contribue John comprendre les tendances de l’utilisateur. Il semble que 15 % des utilisateurs inactifs hello revenir toohello application. Toutefois, la plupart d’entre eux ne restent pas actifs plus de 1 mois. John prévoit une optimisation de cette séquence avec des notifications supplémentaires et le développement du choix de contenu.

Hello **découvrir un programme** ne fonctionne pas correctement. Elle augmente entre la vente, mais n’est pas suffisant tooreach ses objectifs. John identifie qu’il a n’ont suffisamment toomake données pertinentes ciblage et proposer du contenu approprié. Il arrête ce programme et se concentre sur l’envoi de « notifications Push éditoriales » avec Azure Mobile Engagement. Son journalistes ont déjà les notifications de transmission toosend une solution CMS et ils ne souhaitent pas toochange.

John décide toouse hello API couverture, qui est une API REST HTTP qui permet de gérer des couvertures campagne sans avoir d’interface de AZME Web toouse. Avec cette approche John peut collecter des données de hello qu’il a besoin et autorise son writers tookeep à l’aide de la solution CMS hello.

tooensure que la fonctionnalité fonctionne correctement, John demande toobe d’équipe informatique vigilant sur hello les points suivants :

1. **Les systèmes d’exploitation** : ils ont tous leurs propres règles tooadministrate les notifications de transmission, Jean décide de toolist tous les cas et vérifie si hello API la gérer.
   Par exemple : Système Android push permet de présentation qui n’est pas cas hello avec iOS.
2. **Intervalle de temps**: John souhaite une API qui a défini le laps de temps hello et un toocampaigns de fin. Il souhaite que les utilisateurs toopreserve à partir de n’importe quel bombing notification sans interruption.
3. **Catégories**: l’équipe Marketing prépare un modèle pour chaque type d’alerte. John demande des catégories de tooset équipe informatique à l’intérieur de hello API.

Après quelques essais, John est satisfait. API de toothis Merci, journalistes peuvent toujours envoyer des notifications push avec leurs CMS et Azure Mobile Engagement collecte toutes les données de comportement pour les

Après ces 4 premiers mois, les résultats concluent à de bonnes performances générales. John et son équipe sont confiants ; le ROI par utilisateur a augmenté de 15 % et les ventes mobiles représentent 17,5 % du total des ventes, soit une augmentation de 7,5 % en seulement quatre mois.

<!--Image references-->
[1]: ./media/mobile-engagement-media-scenario/engagement-strategy.png
[2]: ./media/mobile-engagement-media-scenario/push-scenarios.png

<!--Link references-->
[Media Playbook link]: https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks
