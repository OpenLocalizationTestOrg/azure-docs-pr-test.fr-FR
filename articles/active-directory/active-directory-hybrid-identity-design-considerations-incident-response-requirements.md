---
title: "Considérations de conception pour les identités hybrides aaaAzure Active Directory - déterminer les besoins de l’incident rResponse | Documents Microsoft"
description: "Déterminer les fonctionnalités de surveillance et création de rapports pour la solution d’identité hybride hello qui peuvent être exploitées par le service informatique tootake actions tooidentify et atténuer les menaces potentielles un"
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: a3d2a459-599b-4b67-8e51-7369ee25082d
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 7084096f318ef461e8331fb6edde1b77d4108466
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="determine-incident-response-requirements-for-your-hybrid-identity-solution"></a>Déterminer les exigences de réponse aux incidents pour votre solution d'identité hybride
Les organisations de taille moyennes ou grandes très probablement aura un [réponse aux incidents de sécurité](https://technet.microsoft.com/library/cc700825.aspx) dans place toohelp informatique prendre des mesures en conséquence niveau toohello d’incident. le système de gestion d’identité Hello est un composant important dans le processus de réponse aux incidents hello, car il peut être utilisé toohelp identifier qui a effectué une action spécifique par rapport à la cible de hello. solution d’identité hybride Hello doit être en mesure de tooprovide analyse et rapports de fonctionnalités qui peuvent être exploitées par le service informatique tootake actions tooidentify et atténuer une menace potentielle. Dans un plan de réponse aux incidents, vous aurez hello suivant des phases dans le cadre du plan de hello :

1. Évaluation initiale.
2. Communication de l'incident.
3. Contrôle des dommages et réduction des risques.
4. Identification de la compromission et de la gravité.
5. Conservation des preuves.
6. Parties de tooappropriate de notification.
7. Récupération du système.
8. Documentation.
9. Évaluation des dommages et des coûts.
10. Révision des processus et du plan.

Pendant l’identification hello de ce qu’il a été compromis et phase de gravité, il sera nécessaire tooidentify hello systèmes ont été compromis, les fichiers qui ont accédé et déterminent la sensibilité hello de ces fichiers. Votre système d’identité hybride doit être en mesure de toofulfill tooassist de ces besoins vous identifiant utilisateur hello qui a effectué ces modifications. 

## <a name="monitoring-and-reporting"></a>Surveillance et création de rapports
Système d’identité hello autant de fois peut également aider dans la phase d’évaluation initiale principalement si le système de hello a généré dans l’audit et de génération de rapports. Au cours de l’évaluation initiale de hello, administrateur informatique doit être en mesure de tooidentify une activité suspecte ou système de hello doit être en mesure de tootrigger qu'il automatiquement basé sur une tâche préconfigurée. De nombreuses activités peuvent indiquer une attaque possible, mais dans d’autres cas, un système mal configuré peut entraîner des nombre tooa de faux positifs dans un système de détection d’intrusion. 

le système de gestion d’identité Hello doit aider tooidentify des administrateurs informatiques et les activités suspectes de rapports. Il est généralement possible de satisfaire à ces exigences techniques en surveillant tous les systèmes et en disposant d'une fonctionnalité de création de rapports pouvant mettre en évidence les menaces potentielles. Utiliser les questions de hello ci-dessous toohelp vous concevez votre solution d’identité hybride en tenant compte d’exigences réponse aux incidents :

* Votre entreprise a-t-elle mis en place une réponse aux incidents de sécurité ?
  * Si Oui, est hello système de gestion d’identité actuel utilisé dans le cadre du processus de hello ?
* Votre entreprise a-t-elle besoin tooidentify suspectes tentatives de connexion des utilisateurs sur les différents appareils ?
* Votre entreprise a-t-elle besoin toodetect potentielle compromis de l’utilisateur ?
* Votre entreprise doit-elle accéder et action de l’utilisateur tooaudit ?
* Votre entreprise a-t-elle besoin tooknow lorsqu’un utilisateur de réinitialiser son mot de passe ?

## <a name="policy-enforcement"></a>Application de stratégies
Pendant la phase de réduction des risques et de limitation des dommages, il est important de tooquickly réduire les effets de hello effective et potentielle d’une attaque. Cette action vous prendrez à ce stade peut faire hello différence entre un mineure et majeure. réponse exacte de Hello dépendent de votre organisation et la nature hello d’attaque hello auxquels vous êtes confronté. Si l’évaluation initiale de hello conclu qu’un compte a été compromis, vous devez tooenforce stratégie tooblock ce compte. C’est qu’un exemple où le système de gestion d’identité hello est exploité. Utiliser les questions de hello ci-dessous toohelp que vous concevez votre solution d’identité hybride lors en prenant en compte la façon dont les stratégies seront appliquée incident en cours de tooreact tooan :

* Votre entreprise a-t-elle des stratégies dans les utilisateurs de tooblock sur place à partir du réseau de hello accès si nécessaire ?
  * Si Oui, hello actuel solution s’intègre-t-elle avec système de gestion hello hybride identité que vous êtes continu tooadopt ?
* Votre entreprise a-t-elle besoin tooenforce l’accès conditionnel pour les utilisateurs qui se trouvent dans la mise en quarantaine ? 

> [!NOTE]
> Notez que tootake de chacune des réponses et comprendre hello sous-tend hello. [Définir la stratégie de protection des données](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) passe en revue les options hello disponibles et les avantages et inconvénients de chaque option.  En répondant à chacune de ces questions, vous sélectionnerez l’option correspondant le mieux à vos besoins métier.
> 
> 

## <a name="next-steps"></a>Étapes suivantes
[Définir les options de protection des données](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md)

## <a name="see-also"></a>Voir aussi
[Présentation des considérations relatives à la conception](active-directory-hybrid-identity-design-considerations-overview.md)

