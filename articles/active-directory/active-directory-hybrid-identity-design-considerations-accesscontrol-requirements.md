---
title: "Considérations de conception pour les identités hybrides aaaAzure Active Directory - déterminer les exigences de contrôle d’accès | Documents Microsoft"
description: "Couvre hello piliers d’identité et d’identification conditions d’accès pour les ressources pour les utilisateurs dans un environnement hybride."
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
ms.openlocfilehash: f0c22629f732a4c13ee7a24456651bec7637c387
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="determine-access-control-requirements-for-your-hybrid-identity-solution"></a>Déterminer les besoins de contrôle d'accès pour votre solution d'identité hybride
Lors de la conception d’une organisation leur solution d’identité hybride ils peuvent également utiliser cette tooreview opportunité accéder aux spécifications pour les ressources de hello qu’ils planifient toomake disponibles pour les utilisateurs. accès aux données de Hello croisée toutes les quatre piliers d’identité, qui sont :

* Administration
* Authentification
* Autorisation
* Audit

les sections Hello qui suit couvre l’authentification et l’autorisation dans plus de détails, d’administration et de l’audit font partie du cycle de vie des identités hybrides hello. Lire [Déterminer les tâches de gestion des identités hybrides](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md) pour plus d'informations sur ces fonctionnalités.

> [!NOTE]
> Lecture [hello quatre piliers suivants de l’identité - gestion des identités dans hello âge d’informatique hybride](http://social.technet.microsoft.com/wiki/contents/articles/15530.the-four-pillars-of-identity-identity-management-in-the-age-of-hybrid-it.aspx) pour plus d’informations sur chacune de ces colonnes.
> 
> 

## <a name="authentication-and-authorization"></a>Authentification et autorisation
Il existe différents scénarios pour l’authentification et d’autorisation, ces scénarios aura des exigences spécifiques qui doivent être remplies par la solution d’identité hybride hello que société de hello est continu tooadopt. Les scénarios impliquant des tooBusiness d’entreprise (B2B) communication peut ajouter une stimulation supplémentaires pour les administrateurs informatiques, car ils devront tooensure méthode d’authentification et d’autorisation hello utilisé par l’organisation de hello capable de communiquer avec leurs partenaires commerciaux. Lors de l’hello conception de processus pour les exigences d’authentification et d’autorisation, assurez-vous que hello suivant questions sont traitées :

* Votre organisation authentifiera et autorisera-t-elle uniquement des utilisateurs se trouvant sur son système de gestion d'identité ?
  * Existe-t-il des plans pour les scénarios B2B ?
  * Si Oui, déjà savez-vous quels protocoles (SAML, OAuth, Kerberos, les jetons ou des certificats) seront être tooconnect utilisé les deux entreprises ?
* Solution d’identité hybride hello que vous allez tooadopt prend en charge ces protocoles ?

Un autre tooconsider point important est où se trouvera référentiel authentification hello qui sera utilisé par les utilisateurs et les partenaires et hello toobe de modèle d’administration utilisé. Tenez compte des hello deux options de base suivantes :

* Centralisée : Bonjour de ce modèle informations d’identification de l’utilisateur, les stratégies et l’administration peuvent être centralisée sur site ou dans le cloud de hello.
* Hybride : Bonjour de ce modèle informations d’identification de l’utilisateur, les stratégies et l’administration seront local centralisé et une répliquées dans le cloud de hello.

Quel modèle de votre organisation adopte varie en fonction des besoins tootheir, que vous souhaitiez hello tooanswer suivant tooidentify questions où le système de gestion d’identité hello réside et hello toouse du mode d’administration :

* Votre entreprise dispose-t-elle actuellement d'une gestion des identités locale ?
  * Dans l’affirmative, ils envisagez-vous tookeep il ?
  * Sont les exigences réglementaires et de conformité que votre organisation doit suivre qui détermine où doit résider le système de gestion d’identité hello ?
* Votre organisation utilise-t-elle l’authentification unique pour les applications sur site ou dans le cloud de hello ?
  * Si Oui, adoption hello d’un modèle d’identité hybride affecte-t-elle ce processus ?

## <a name="access-control"></a>Contrôle d’accès
Lors de l’authentification et autorisation sont les principaux éléments tooenable accès des données toocorporate via la validation de l’utilisateur, il est également important toocontrol hello niveau d’accès à ces utilisateurs auront et dotés de niveau hello des administrateurs d’accès sur hello ressources qu’ils gèrent. Votre solution d’identité hybride doit être en mesure de tooprovide un accès granulaire tooresources, contrôle d’accès de base de rôles et de délégation. Vérifiez que hello suivant question reçoivent une réponse concernant le contrôle d’accès :

* Votre entreprise dispose plus d’un utilisateur avec des privilèges élevés toomanage votre système d’identité ?
  * Si Oui, chaque utilisateur a besoin hello même niveau d’accès ?
* Aurait nécessité toodelegate accès toousers toomanage des ressources de votre entreprise ?
  * Si oui, à quelle fréquence ?
* Votre entreprise doit toointegrate des fonctionnalités de contrôle d’accès entre locaux et cloud ressources ?
* Votre entreprise doit toolimit tooresources de l’accès en fonction de conditions de toosome ?
* Votre entreprise aurait toute application qui nécessite des ressources de toosome accès contrôle personnalisé ?
  * Si Oui, où ces applications se trouvent (localement ou dans le cloud de hello) ?
  * Si Oui, où sont les ressources cibles situés (localement ou dans le cloud de hello) ?

> [!NOTE]
> Notez que tootake de chacune des réponses et comprendre hello sous-tend hello. [Définir la stratégie de Protection des données](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) passe en revue les options hello disponibles et les avantages et inconvénients de chaque option.  En répondant à ces questions, vous sélectionnerez l’option la mieux adaptée à vos besoins métier.
> 
> 

## <a name="next-steps"></a>Étapes suivantes
[Déterminer les exigences de réponse aux incidents](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md)

## <a name="see-also"></a>Voir aussi
[Présentation des considérations relatives à la conception](active-directory-hybrid-identity-design-considerations-overview.md)

