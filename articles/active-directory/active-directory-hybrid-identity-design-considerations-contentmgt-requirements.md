---
title: "Considérations de conception pour les identités hybrides aaaAzure Active Directory - déterminer les besoins de gestion de contenu | Documents Microsoft"
description: "Permet de comprendre comment toodetermine hello les besoins de gestion de contenu de votre entreprise. Généralement lorsqu’un utilisateur possède son propre appareil qu’il devra peut-être également plusieurs informations d’identification en alternance conséquente application toohello qu’il utilise. Il est important toodifferentiate contenu qui a été créé à l’aide des informations d’identification personnelles et hello ceux créés à l’aide des informations d’identification d’entreprise. Votre solution d’identité doit être en mesure de toointeract avec tooprovide de services de cloud une expérience transparente toohello les utilisateurs lors de garantir sa confidentialité et de renforcer la protection de hello contre les fuites de données."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: dd1ef776-db4d-4ab8-9761-2adaa5a4f004
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 607d366633c37b65ec5cf8ae5c64d73ca1cc96b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="determine-content-management-requirements-for-your-hybrid-identity-solution"></a>Déterminer les exigences de gestion de contenu pour votre solution d'identité hybride
Présentation des exigences de gestion de contenu hello pour votre entreprise peut diriger influencer votre décision sur le toouse de solution d’identité hybride. Avec hello prolifération de plusieurs appareils et de la capacité de hello d’utilisateurs toobring leurs propres appareils ([BYOD](http://aka.ms/byodcg)), société de hello doit protéger ses propres données, mais il également doit préserver la confidentialité de l’utilisateur consécutifs. Généralement lorsqu’un utilisateur possède son propre appareil qu’il devra peut-être également plusieurs informations d’identification en alternance conséquente application toohello qu’il utilise. Il est important toodifferentiate contenu qui a été créé à l’aide des informations d’identification personnelles et hello ceux créés à l’aide des informations d’identification d’entreprise. Votre solution d’identité doit être en mesure de toointeract avec tooprovide de services de cloud une expérience transparente toohello les utilisateurs lors de garantir sa confidentialité et de renforcer la protection de hello contre les fuites de données. 

Votre solution d’identité est exploitée par les différents contrôles techniques de gestion de contenu de commande tooprovide comme indiqué dans la figure hello ci-dessous :

![](./media/hybrid-id-design-considerations/securitycontrols.png)

**Contrôles de sécurité qui exploiteront votre système de gestion d'identité**

En général, les exigences de gestion de contenu reposera sur votre système de gestion d’identité Bonjour suivant de zones :

* Confidentialité : identifiant utilisateur hello qui possède une ressource et en appliquant l’intégrité de toomaintain hello contrôles appropriés.
* Classification des données : identifier les utilisateur hello ou de groupe et de niveau de l’objet tooan d’accès en fonction de classification de tooits. 
* Protection contre la perte de données : les contrôles de sécurité incombe de protéger la fuite des données tooavoid devez toointeract avec hello identité système toovalidate hello identité de l’utilisateur. Ceci est également important pour objectif de piste d'audit.

> [!NOTE]
> Lire [Classification des données pour l'adoption du cloud](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) pour plus d'informations sur les meilleures pratiques et directives de classification des données.
> 
> 

Lors de la planification de votre solution d’identité hybride Vérifiez que hello suivant questions sont traitées selon les besoins de l’organisation tooyour :

* Votre entreprise a-t-elle des contrôles de sécurité de la confidentialité des données tooenforce place ?
  * Si Oui, ces contrôles de sécurité seront en mesure de toointegrate avec la solution d’identité hybride hello que vous êtes continu tooadopt ?
* Votre entreprise utilise-t-elle la classification des données ?
  * Si Oui, est hello actuel toointegrate en mesure de solution avec la solution d’identité hybride hello que vous êtes continu tooadopt ?
* Votre entreprise a-t-elle actuellement une solution contre la fuite de données ? 
  * Si Oui, est hello actuel toointegrate en mesure de solution avec la solution d’identité hybride hello que vous êtes continu tooadopt ?
* Votre entreprise a-t-elle besoin tooaudit accès tooresources ?
  * Si oui, de quel type de ressources ?
  * Si oui, quel est le niveau d'information nécessaire ?
  * Si Oui, le journal d’audit de hello doit où résident ? Local ou dans le cloud de hello ?
* Votre entreprise a-t-elle besoin tooencrypt d’e-mails qui contiennent des données sensibles (numéros de sécurité sociale, numéros de carte de crédit, etc.) ?
* Votre entreprise a-t-elle besoin tooencrypt tous les documents/contenu partagé avec les partenaires externes de l’entreprise ?
* Votre entreprise a-t-elle besoin tooenforce des stratégies d’entreprise sur certains types de messages électroniques (ne pas répondre à tous, ne pas transférer) ?

> [!NOTE]
> Notez que tootake de chacune des réponses et comprendre hello sous-tend hello. [Définir la stratégie de Protection des données](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) passe en revue les options hello disponibles et les avantages et inconvénients de chaque option.  En répondant à chacune de ces questions, vous sélectionnerez l’option correspondant le mieux à vos besoins métier.
> 
> 

## <a name="next-steps"></a>Étapes suivantes
[Déterminer les exigences de contrôle d’accès](active-directory-hybrid-identity-design-considerations-accesscontrol-requirements.md)

## <a name="see-also"></a>Voir aussi
[Présentation des considérations relatives à la conception](active-directory-hybrid-identity-design-considerations-overview.md)

