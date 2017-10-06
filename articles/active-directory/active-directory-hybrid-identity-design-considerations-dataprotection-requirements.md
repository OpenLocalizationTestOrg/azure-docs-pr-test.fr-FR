---
title: "Considérations de conception pour les identités hybrides aaaAzure Active Directory - déterminer les exigences de protection de données | Documents Microsoft"
description: "Lors de la planification de votre solution d’identité hybride, identifier les exigences de protection des données hello pour votre entreprise et les options disponible toobest respecter ces exigences."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 40dc4baa-fe82-4ab6-a3e4-f36fa9dcd0df
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 189abf9affbc2894c322f362d84222d4e33d472e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="plan-for-enhancing-data-security-through-strong-identity-solution"></a>Planifier l'amélioration de la sécurité des données grâce à une solution d'identité solide
première étape tooprotect hello les données de salutation sont identifier qui peut accéder à ces données et dans le cadre de ce processus, vous devez toohave une solution d’identité qui peut s’intègre à vos capacités d’authentification et d’autorisation de tooprovide système. Authentification et autorisation sont souvent confondues et leurs rôles mal compris. En réalité qu’ils sont très différentes, comme indiqué dans la figure hello ci-dessous :

![](./media/hybrid-id-design-considerations/mobile-devicemgt-lifecycle.png)

**Étapes du cycle de vie de gestion des appareils mobiles**

Lors de la planification de votre solution d’identité hybride, vous devez comprendre exigences de protection des données hello pour votre entreprise et les options disponible toobest respecter ces exigences.

> [!NOTE]
> Une fois que vous avez terminé la planification de la sécurité des données, passez en revue [déterminer les besoins de l’authentification multifacteur](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md) tooensure que vos sélections sur la configuration de l’authentification multifacteur n’étaient pas affectées par les décisions de hello vous avez effectuée dans cette section.
> 
> 

## <a name="determine-data-protection-requirements"></a>Déterminer les exigences de protection des données
Dans la durée de vie de hello de mobilité, la plupart des entreprises ont un objectif commun : activer leur toobe utilisateurs productif sur leurs appareils mobiles, localement ou à distance à partir de n’importe où dans la productivité tooincrease de commande. Alors que cela peut être un objectif commun, sociétés qui disposent de cette exigence sera également le problème concernant le montant hello des menaces qui doivent être atténués dans les données de la société commande tookeep sécurisées et de préserver la confidentialité de l’utilisateur. Chaque entreprise peut avoir des exigences différentes à cet égard ; règles de compatibilité différentes qui varient entreprise hello de secteur conséquente toowhich fait Office de va entraîner des décisions de conception toodifferent. 

Toutefois, il existe de certains aspects de sécurité qui doivent être examinées et validées, quel que soit le secteur d’activité hello, qui sont expliquées dans la section suivante de hello.

## <a name="data-protection-paths"></a>Chemins de protection des données
![](./media/hybrid-id-design-considerations/data-protection-paths.png)

**Chemins de protection des données**

Bonjour diagramme ci-dessus, composant d’identité hello sera hello premier toobe vérifié avant que les données sont accessibles. Toutefois, ces données peuvent être dans différents États au moment de hello qu'auquel il a accédé. Chaque numéro sur ce diagramme représente un chemin dans lequel les données peuvent être situées à un moment donné dans le temps. Ces numéros sont expliqués ci-dessous :

1. Protection des données au niveau du périphérique hello.
2. Protection des données pendant leur transit.
3. Protection des données au repos en local.
4. Protection des données au repos dans le cloud de hello.

Bien que les contrôles techniques hello qui activera les données hello informatique tooprotect lui-même sur chacune de ces phases ne sont pas directement proposés par la solution d’identité hybride hello, il est nécessaire que la solution d’identité hybride hello est capable de tirer parti à la fois localement et gestion de cloud identité ressources hello tooidentify utilisateur avant d’accorder, accéder aux données toohello. Lors de la planification de votre solution d’identité hybride Vérifiez que hello suivant questions sont traitées selon les besoins de l’organisation tooyour :

## <a name="data-protection-at-rest"></a>Protection des données au repos
Indépendamment dans lequel les données de salutation au repos (unité, cloud ou local), il est important de tooperform une organisation de hello toounderstand évaluation doit à cet égard. Pour cette zone, vérifiez que hello suivant questions sont posées :

* Votre entreprise a-t-elle besoin tooprotect des données au repos ?
  * Dans l’affirmative, est-il hello hybride identité solution en mesure de toointegrate avec votre infrastructure locale actuelle
  * Si Oui, vos charges de travail situés dans le cloud de hello est toointegrate en mesure de hello hybride identité solution ?
* Est hello cloud identity management tooprotect en mesure de hello de l’utilisateur et autres données stockées dans le cloud de hello ?

## <a name="data-protection-in-transit"></a>Protection des données en transit
Les données en transit entre les appareils hello et hello datacenter ou entre périphériques de hello et de cloud de hello doivent être protégées. Toutefois, être en transit n'implique pas nécessairement un processus de communication avec un composant en dehors de votre service cloud ; le déplacement se fait en interne, comme entre deux réseaux virtuels. Pour cette zone, vérifiez que hello suivant questions sont posées :

* Votre entreprise a-t-elle besoin tooprotect des données en transit ?
  * Dans l’affirmative, est-il hello hybride identité solution en mesure de toointegrate avec des contrôles sécurisés tels que SSL/TLS
* Gestion des identités cloud hello évite que hello trafic tooand dans hello magasin d’annuaires (dans et entre les centres de données) signé ?

## <a name="compliance"></a>Conformité
Réglementaires, les lois et réglementations varient conséquente industrie toohello appartenant à votre entreprise. Entreprises de secteurs réglementées haute doivent résoudre des problèmes de gestion des identités préoccupations toocompliance connexes. Réglementations telles que Sarbanes-Oxley (SOX), hello Health Insurance Portability et Accountability Act (HIPAA), hello Gramm-Leach-Bliley Act (GLBA) et hello paiement carte Industry Data Security Standard (PCI DSS) sont très strictes concernant les identités et des accès. solution d’identité hybride Hello adoptée par votre société doit avoir des fonctionnalités principales hello répondant aux exigences de hello d’un ou plusieurs de ces réglementations. Pour cette zone, vérifiez que hello suivant questions sont posées :

* Solution d’identité hybride hello est-il conforme aux exigences réglementaires de hello pour votre entreprise
* Solution d’identité hybride a hello intègre des fonctionnalités qui permettent à votre entreprise toobe conforme réglementaires ? 

> [!NOTE]
> Notez que tootake de chacune des réponses et comprendre hello sous-tend hello. [Définir la stratégie de Protection des données](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) passe en revue les options hello disponibles et les avantages et inconvénients de chaque option.  En répondant à chacune de ces questions, vous sélectionnerez l’option correspondant le mieux à vos besoins métier.
> 
> 

## <a name="next-steps"></a>Étapes suivantes
 [Déterminer les exigences de gestion de contenu](active-directory-hybrid-identity-design-considerations-contentmgt-requirements.md)

## <a name="see-also"></a>Voir aussi
[Présentation des considérations relatives à la conception](active-directory-hybrid-identity-design-considerations-overview.md)

