---
title: "portail d’inscription aaaSelf-service pour Azure Active Directory B2B collaboration | Documents Microsoft"
description: "Azure Active Directory B2B collaboration prend en charge les relations de votre société croisée en activant tooselectively partenaires commerciaux un accès à vos applications d’entreprise"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/24/2017
ms.author: sasubram
ms.openlocfilehash: c78920ecf812f7efc06a8b54b1fff834c32904f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="self-service-portal-for-azure-ad-b2b-collaboration-sign-up"></a>Portail d’inscription en libre-service pour Azure AD B2B Collaboration

Les clients peuvent faire beaucoup des fonctionnalités intégrées hello qui sont exposées via notre administrateur informatique [portail Azure](https://portal.azure.com) et notre [volet d’accès Application](https://myapps.microsoft.com) pour les utilisateurs finaux. Mais nous sommes également prenant en charge les entreprises doivent flux de travail d’intégration toocustomize hello pour B2B utilisateurs toofit leurs besoins. Elles le peuvent avec [nos API](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation).

En discutant avec nos clients, nous avons constaté un besoin commun de sortir du lot. Hello invitation d’organisation ne sait pas avance qui hello collaborateurs externes individuels sont qui doivent accéder aux ressources de tootheir. Ils voulaient un moyen pour les utilisateurs à partir de sociétés partenaires trop s’inscrire eux-mêmes avec un ensemble de stratégies que hello invitant les contrôles de l’organisation. Ce scénario est possible grâce à nos API. Nous avons donc publié un projet dédié sur GitHub : [exemple de projet GitHub](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).

Notre projet Github montre comment les organisations peuvent utiliser nos API et fournissent une fonctionnalité d’inscription libre-service, basée sur des stratégies pour leurs partenaires approuvés, avec des règles qui déterminent les applications hello ils peuvent accéder à. Les utilisateurs de partenaire peuvent obtenir des accès tooresources quand ils en ont besoin, en toute sécurité, sans nécessiter de hello inviter toomanually organisation intégrer les. Vous pouvez facilement déployer le projet de hello dans un abonnement Azure de votre choix.

## <a name="as-is-code"></a>Code en l’état

N’oubliez pas que ce code est rendu disponible en tant qu’exemple toodemonstrate utilisation de l’invitation hello Azure Active Directory B2B API. Il doit être personnalisé par votre équipe de développement ou un partenaire, et doit être révisé avant tout déploiement en environnement de production.

## <a name="next-steps"></a>Étapes suivantes

Consultez les autres articles sur la collaboration B2B d'Azure AD :
* [Qu’est-ce qu’Azure AD B2B Collaboration ?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Comment les administrateurs Azure Active Directory ajoutent-ils des utilisateurs B2B Collaboration ?](active-directory-b2b-admin-add-users.md)
* [Comment les professionnels de l’information ajoutent-ils des utilisateurs B2B Collaboration ?](active-directory-b2b-iw-add-users.md)
* [éléments Hello Hello e-mail d’invitation B2B collaboration](active-directory-b2b-invitation-email.md)
* [Utilisation d’une invitation B2B Collaboration](active-directory-b2b-redemption-experience.md)
* [Attribution de licences Azure AD B2B Collaboration](active-directory-b2b-licensing.md)
* [Résolution des problèmes d’Azure Active Directory B2B Collaboration](active-directory-b2b-troubleshooting.md)
* [Questions fréquemment posées (FAQ) sur Azure Active Directory B2B Collaboration](active-directory-b2b-faq.md)
* [Authentification multifacteur pour les utilisateurs B2B Collaboration](active-directory-b2b-mfa-instructions.md)
* [Ajouter des utilisateurs B2B Collaboration sans invitation](active-directory-b2b-add-user-without-invite.md)
* [Index d’articles pour la gestion des applications dans Azure Active Directory](active-directory-apps-index.md)