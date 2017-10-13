---
title: "Considérations relatives à la conception d’identités hybrides Azure Active Directory : déterminer les exigences en matière de contrôle d’accès | Microsoft Docs"
description: "Couvre les piliers de l'identité et l'identification des conditions d'accès aux ressources pour les utilisateurs dans un environnement hybride."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: e3b3b984-0d15-4654-93be-a396324b9f5e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 6404940da460461632616fe49f055d50c2a7aba3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="determine-access-control-requirements-for-your-hybrid-identity-solution"></a>Déterminer les besoins de contrôle d'accès pour votre solution d'identité hybride
Lorsqu'une organisation conçoit sa solution d'identité hybride, elle peut également profiter de cette opportunité pour passer en revue les exigences d'accès pour les ressources qu'elle envisage de mettre à la disposition des utilisateurs. L'accès aux données couvre les quatre piliers suivants de l'identité :

* Administration
* Authentification
* Autorisation
* Audit

Les sections suivantes couvriront l'authentification et l'autorisation de manière plus détaillée, l'administration et l'audit font partie du cycle de vie de l'identité hybride. Lire [Déterminer les tâches de gestion des identités hybrides](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md) pour plus d'informations sur ces fonctionnalités.

> [!NOTE]
> Lire [Les quatre piliers de l'identité - Gestion des identités à l'ère de l'informatique hybride](http://social.technet.microsoft.com/wiki/contents/articles/15530.the-four-pillars-of-identity-identity-management-in-the-age-of-hybrid-it.aspx) pour plus d'informations sur chacun de ces piliers.
> 
> 

## <a name="authentication-and-authorization"></a>Authentification et autorisation
Il existe différents scénarios d'authentification et d'autorisation aux exigences spécifiques desquelles la solution d'identité hybride que l'entreprise va adopter devra satisfaire. Les scénarios impliquant une communication interentreprises (B2B) peuvent constituer un défi supplémentaire pour les administrateurs informatiques, qui devront s'assurer que la méthode d'authentification et d'autorisation utilisée par l'organisation peut communiquer avec leurs partenaires commerciaux. Pendant le processus de conception des exigences d'authentification et d'autorisation, vérifiez que les questions suivantes sont traitées :

* Votre organisation authentifiera et autorisera-t-elle uniquement des utilisateurs se trouvant sur son système de gestion d'identité ?
  * Existe-t-il des plans pour les scénarios B2B ?
  * Si oui, savez-vous déjà quels protocoles (SAML, OAuth, Kerberos, jetons ou certificats) seront utilisés pour connecter les deux entreprises ?
* La solution d'identité hybride que vous vous apprêtez à adopter prend-elle en charge ces protocoles ?

Un autre point important à prendre en compte est l'endroit où se trouvera le référentiel d'authentification qui sera utilisé par les utilisateurs et les partenaires et le modèle d'administration à utiliser. Examinez les deux options principales suivantes :

* Centralisée : dans ce modèle, les informations d’identification de l’utilisateur, les stratégies et l’administration peuvent être centralisées localement ou dans le cloud.
* Hybride : dans ce modèle, les informations d’identification de l’utilisateur, les stratégies et l’administration peuvent être centralisées localement et répliquées dans le cloud.

Le modèle adopté par votre organisation variera en fonction de ses besoins métiers. Veuillez répondre aux questions suivantes pour identifier où le système de gestion d'identité se trouvera et quel mode d'administration devra être utilisé :

* Votre entreprise dispose-t-elle actuellement d'une gestion des identités locale ?
  * Si oui, prévoit-elle de la conserver ?
  * Existe-t-il des exigences réglementaires et de conformité auxquelles votre organisation doit satisfaire qui déterminent où doit résider le système de gestion d'identité ?
* Votre organisation utilise-t-elle l'authentification unique pour les applications locales ou dans le cloud ?
  * Si oui, l'adoption d'un modèle d'identité hybride affecte-t-elle ce processus ?

## <a name="access-control"></a>Contrôle d’accès
Bien que l'authentification et l'autorisation soient des éléments essentiels pour activer l'accès aux données d'entreprise grâce à la validation de l'utilisateur, il est également important de contrôler le niveau d'accès de ces utilisateurs, ainsi que le niveau d'accès des administrateurs aux ressources qu'ils gèrent. Votre solution d'identité hybride doit être en mesure de fournir un accès granulaire aux ressources, la délégation et le contrôle d'accès basé sur les rôles. Assurez-vous que les questions suivantes sur le contrôle d'accès ont fait l'objet d'une réponse :

* Votre entreprise a-t-elle plus d'un utilisateur avec des privilèges élevés pour gérer votre système d'identité ?
  * Si oui, chaque utilisateur a-t-il besoin du même niveau d'accès ?
* Votre entreprise devrait-elle déléguer l'accès aux utilisateurs pour gérer des ressources spécifiques ?
  * Si oui, à quelle fréquence ?
* Votre entreprise devrait-elle intégrer les fonctionnalités de contrôle d'accès entre les ressources locales site et de cloud ?
* Votre entreprise devrait-elle limiter l'accès aux ressources sous certaines conditions ?
* Votre entreprise aurait-elle une application qui nécessite un accès avec contrôle personnalisé à certaines ressources ?
  * Si oui, où se trouvent ces applications (locales ou dans le cloud) ?
  * Si oui, où se trouvent ces ressources cibles (locales ou dans le cloud) ?

> [!NOTE]
> Veillez à noter chaque réponse et à comprendre le raisonnement derrière la réponse. [Définir la stratégie de protection des données](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) examinera les options disponibles et les avantages/inconvénients de chaque option.  En répondant à ces questions, vous sélectionnerez l’option la mieux adaptée à vos besoins métier.
> 
> 

## <a name="next-steps"></a>Étapes suivantes
[Déterminer les exigences de réponse aux incidents](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md)

## <a name="see-also"></a>Voir aussi
[Présentation des considérations relatives à la conception](active-directory-hybrid-identity-design-considerations-overview.md)

