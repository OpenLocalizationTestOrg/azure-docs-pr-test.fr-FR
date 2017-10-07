---
title: "aaaAzure identité hybride de Active Directory des considérations de conception : déterminer les tâches de gestion des identités hybrides | Documents Microsoft"
description: "Avec le contrôle d’accès conditionnel, Azure Active Directory vérifie les conditions spécifiques hello que vous choisissez lors de l’authentification utilisateur de hello et avant d’autoriser l’accès toohello application. Lorsque ces conditions sont réunies, hello utilisateur authentifié et autorisé accès toohello application."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 65f80aea-0426-4072-83e1-faf5b76df034
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: d3c0e9b23f43127b3d8e0b3a4e8f03d4bc148c27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="plan-for-hybrid-identity-lifecycle"></a>Planifier le cycle de vie des identités hybrides
Identité est un des fondements de hello de votre stratégie d’accès enterprise mobility et d’application. Si vous vous connectez sur les appareils mobiles tooyour ou application SaaS, votre identité est hello toogaining clé accès tooeverything. À son niveau le plus élevé, une solution de gestion des identités englobe unifier et la synchronisation entre vos espaces de stockage qui inclut l’automatisation et la centralisation des processus hello de provisionnement des ressources. solution d’identité Hello doit être une identité centralisée entre locaux et cloud également utiliser une forme d’une authentification centralisée identity federation toomaintain et en toute sécurité et de partager avec les entreprises et les utilisateurs externes. Plage de ressources à partir des systèmes d’exploitation et applications toopeople ou sont associée à une organisation. Structure d’organisation peut être modifiée tooaccommodate stratégies de configuration hello et les procédures.

Il est également important de toohave une solution d’identité axées tooempower vos utilisateurs en leur fournissant des expériences de libre-service tookeep leur productivité. Votre solution d’identité est plus robuste, si elle permet l’authentification unique pour les utilisateurs sur toutes les ressources hello que dont ils ont besoin d’accéder aux administrateurs tout niveaux peuvent utiliser les procédures standard pour la gestion des informations d’identification de l’utilisateur. Certains niveaux d’administration peut être réduit ou éliminé, en fonction de l’ampleur hello Hello solution de gestion de configuration. En outre, vous pouvez en toute sécurité distribuer les capacités d'administration, manuellement ou automatiquement, entre différentes organisations. Par exemple, un administrateur de domaine peut traiter uniquement des personnes de hello et des ressources de ce domaine. Cet utilisateur peut exécuter des tâches d’administration et de configuration, mais est toodo non autorisé des tâches de configuration, telles que la création de flux de travail.

## <a name="determine-hybrid-identity-management-tasks"></a>Déterminer les tâches de gestion des identités hybrides
Distribuer des tâches d’administration dans votre organisation améliore la précision de hello et l’efficacité de l’administration et améliore le solde hello de charge de travail hello d’une organisation. Voici les tableaux croisés dynamiques hello qui définissent un système de gestion d’identité fiable.

 ![](./media/hybrid-id-design-considerations/Identity_management_considerations.png)

toodefine tâches de gestion d’identité hybride, vous devez comprendre certaines caractéristiques essentielles d’une organisation hello qui va être adopté identité hybride. Il est utilisés pour les sources de l’identité des référentiels actuelle hello toounderstand important. Connaître les éléments de base, vous aurez besoins fondamentaux de hello et selon que vous devez tooask plus granulaire aux questions qui vous guideront tooa meilleure décision de conception de votre solution d’identité.  

Lorsque vous définissez ces exigences, vérifiez que hello au moins suivant questions sont traitées.

* Options d’approvisionnement : 
  
  * Solution d’identité hybride hello prend-il en charge un système de configuration et de gestion de l’accès robuste ?
  * Comment sont des utilisateurs, groupes et les mots de passe va toobe géré ?
  * Gestion du cycle de vie des identités hello est-elle réactive 
    * Combien de temps prend la suspension du compte de mises à jour du mot de passe ?
* Gestion des licences : 
  
  * Hello gestion des licences handles hybride identité solution ?
    * Si oui, quelles sont les fonctionnalités disponibles ?
* Hello solution basée sur le groupe de licences gérer ? 
  
      - Si Oui, il est possible de tooassign un tooit de groupe de sécurité ? 
       - Si Oui, annuaire de cloud hello attribue automatiquement des licences tooall des membres de hello du groupe de hello ? 
        - Que se passe-t-il si un utilisateur est ensuite ajouté ou supprimé du groupe de hello, sera une licence automatiquement attribuée ou supprimée le cas échéant ? 
* Intégration avec des fournisseurs d'identité tiers :
* Cette solution hybride peut être intégrée avec identité tiers fournisseurs tooimplement l’authentification unique ?
* Il est possible de toounify tous hello différents fournisseurs d’identité dans un système d’identité cohérente ?
* Si oui, comment, qui sont-ils et quelles fonctionnalités sont disponibles ?

## <a name="synchronization-management"></a>Gestion de la synchronisation
Un des objectifs de hello d’un gestionnaire d’identité, toobring en mesure de toobe tous hello fournisseurs d’identité et les garder synchronisés. Vous conservez les données hello synchronisées basée sur un fournisseur d’identité maître faisant autorité. Dans un scénario d’identité hybride, avec un modèle d’administration synchronisés, vous gérez toutes les identités d’utilisateur et appareil dans un serveur local et synchronisez les comptes hello et, éventuellement, cloud toohello de mots de passe. utilisateur de Hello entre des hello même mot de passe local comme il le fait dans le cloud de hello et à la connexion, hello mot de passe est vérifié par une solution d’identité hello. Ce modèle utilise un outil de synchronisation d'annuaire.

![](./media/hybrid-id-design-considerations/Directory_synchronization.png)synchronisation de hello tooproper conception de votre solution d’identité hybride vous assurer que hello suivant questions sont traités : • quelles sont les solutions de synchronisation hello disponibles pour la solution d’identité hybride hello ?
• Quels sont l’authentification unique hello fonctionnalités disponibles ?
• Quelles sont les options de hello pour la fédération des identités entre B2B et B2C ?

## <a name="next-steps"></a>Étapes suivantes
[Déterminer la stratégie d’adoption de la gestion des identités hybrides](active-directory-hybrid-identity-design-considerations-lifecycle-adoption-strategy.md)

## <a name="see-also"></a>Voir aussi
[Présentation des considérations relatives à la conception](active-directory-hybrid-identity-design-considerations-overview.md)

