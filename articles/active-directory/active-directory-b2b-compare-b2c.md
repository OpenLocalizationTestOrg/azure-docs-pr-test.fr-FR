---
title: aaaCompare B2B collaboration et B2C dans Azure Active Directory | Documents Microsoft
description: "Qu’est la différence de hello entre Azure Active Directory B2B collaboration et Azure AD B2C ?"
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
ms.date: 03/15/2017
ms.author: sasubram
ms.openlocfilehash: 34d88b9a7d023e077568e8df3d5e1610ae05b361
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="compare-b2b-collaboration-and-b2c-in-azure-active-directory"></a>Comparer B2B Collaboration et B2C dans Azure Active Directory

Azure Active Directory (Azure AD) B2B collaboration et Azure AD B2C permettent toowork avec des utilisateurs externes dans Azure AD. En quoi se différencient-ils ?


Fonctionnalités de B2B Collaboration |     Offre autonome d’Azure AD B2C
-------- | --------
Destinés : organisations que les utilisateurs en mesure de tooauthenticate de toobe à partir d’une organisation partenaire, quel que soit le fournisseur d’identité. | Public visé : inviter les clients de vos appareils mobiles et applications web, qu’il s’agisse d’individus, d’institutions ou d’organisations dans votre Azure AD.
Identités prises en charge : employés ou partenaires disposant d’un compte professionnel ou scolaire ou n’importe quelle adresse de messagerie. Bientôt toosupport fédération.  | Identités prises en charge : utilisateurs consommateurs disposant de comptes d’application locaux (n’importe quel nom d’utilisateur ou adresse de messagerie) ou toute identité sociale prenant en charge la fédération directe.
Les utilisateurs de partenaire directory hello dans : partenaire à partir de l’organisation externe de hello, les utilisateurs sont gérés dans hello même répertoire que les employés, mais annoté spécialement. Ils peuvent être gérés hello même comme employés, peut être ajouté toohello mêmes groupes et ainsi de suite  | Qui sont dans des entités d’annuaire hello client utilisateur : dans le répertoire de l’application hello. Géré séparément de l’annuaire d’employés et partenaires hello organisation (le cas échéant.
Single sign-on (SSO) tooall Azure applications connectées d’Active Directory est prise en charge. Par exemple, vous pouvez fournir accès tooOffice 365 ou applications sur site et tooother les applications SaaS telles que Salesforce ou de la journée de travail.  |  La propriété SSO toocustomer applications dans les locataires Azure AD B2C de hello est pris en charge. L’authentification unique tooOffice 365 ou tooother les applications SaaS non-Microsoft et Microsoft n’est pas pris en charge.
Cycle de vie du partenaire : gérés par hello hôte/invitation de l’organisation.  | Cycle de vie client : libre-service ou gérées par l’application hello.
Stratégie de sécurité et conformité : gérés par hello hôte/invitation de l’organisation.  | Stratégie de sécurité et conformité : géré par l’application hello.
Marque : la marque de l’organisation hôte/qui invite est utilisée.  |    Marque : gérée par l’application. En règle générale, a tendance produit toobe marquée atténuant d’organisation hello en arrière-plan de hello.
Plus d’informations : [Billet de blog](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/01/azure-ad-b2b-new-updates-make-cross-business-collab-easy/), [Documentation](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b)  | Plus d’informations : [Page produit](https://azure.microsoft.com/en-us/services/active-directory-b2c/), [Documentation](https://docs.microsoft.com/en-us/azure/active-directory-b2c/)


### <a name="next-steps"></a>Étapes suivantes

Consultez les autres articles sur la collaboration B2B d'Azure AD :

* [Qu’est-ce qu’Azure AD B2B Collaboration ?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Propriétés de l’utilisateur B2B Collaboration](active-directory-b2b-user-properties.md)
* [Ajout d’un rôle tooa B2B collaboration](active-directory-b2b-add-guest-to-role.md)
* [Déléguer des invitations B2B Collaboration](active-directory-b2b-delegate-invitations.md)
* [Groupes dynamiques et B2B Collaboration](active-directory-b2b-dynamic-groups.md)
* [Configurer des applications SaaS pour B2B Collaboration](active-directory-b2b-configure-saas-apps.md)
* [Jetons utilisateur B2B Collaboration](active-directory-b2b-user-token.md)
* [Mappage des revendications utilisateur B2B Collaboration](active-directory-b2b-claims-mapping.md)
* [Partage externe d’Office 365](active-directory-b2b-o365-external-user.md)
* [Limitations actuelles de B2B Collaboration](active-directory-b2b-current-limitations.md)
* [Obtention de la prise en charge pour B2B Collaboration](active-directory-b2b-support.md)
