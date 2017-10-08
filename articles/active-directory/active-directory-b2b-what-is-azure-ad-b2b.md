---
title: "aaaWhat est Azure Active Directory B2B collaboration ? | Microsoft Docs"
description: "Azure Active Directory B2B collaboration prend en charge les relations de votre société croisée en activant tooselectively partenaires commerciaux un accès à vos applications d’entreprise."
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 1464387b-ee8b-4c7c-94b3-2c5567224c27
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 06/27/2017
ms.author: curtand
ms.custom: aaddev
ms.reviewer: sasubram
ms.openlocfilehash: 359989b66f3d012c306e8748a607662fffacb919
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-ad-b2b-collaboration"></a>Qu’est-ce qu’Azure AD B2B Collaboration ?

<iframe width="560" height="315" src="https://www.youtube.com/embed/AhwrweCBdsc" frameborder="0" allowfullscreen></iframe>

Fonctionnalités de collaboration Azure AD-interentreprises (B2B) activer toutes les organisations à l’aide de Azure AD toowork en toute sécurité avec des utilisateurs à partir de n’importe quel autre organisation, petite ou grande. Ces organisations peuvent être avec ou sans Azure AD, avec ou sans service informatique. 

Les organisations à l’aide d’Azure AD peuvent d’accéder toodocuments, les ressources et applications partenaires tootheir, tout en conservant le contrôle complet sur leurs propres données d’entreprise. Les développeurs peuvent utiliser des applications de toowrite hello Azure AD business-to-business API qui rapprochent les deux organisations plus en toute sécurité. En outre, il est assez facile pour les utilisateurs finaux toonavigate.

97 % de nos clients nous ont dit Azure AD B2B collaboration est très important toothem.

![Graphique à secteurs](media/active-directory-b2b-what-is-azure-ad-b2b/97-percent-support.png)

Dès début avril 2017, nous avions déjà près de trois millions d’utilisateurs bénéficiant des fonctionnalités d’Azure AD B2B Collaboration. Et plus de 23 % des organisations Azure AD comptant plus de 10 utilisateurs tirent déjà parti de ces fonctionnalités.

## <a name="hello-key-benefits-of-azure-ad-b2b-collaboration-tooyour-organization"></a>Hello principaux avantages d’organisation de tooyour Azure AD B2B collaboration

### <a name="work-with-any-user-from-any-partner"></a>Travaillez avec n’importe quel utilisateur de n’importe quel partenaire

* Les partenaires utilisent leurs propres informations d’identification

* Aucune configuration requise pour les partenaires toouse Azure AD

* Aucun répertoire externe ou configuration complexe requis

### <a name="simple-and-secure-collaboration"></a>Collaboration simple et sécurisée

* Fournissent des applications d’entreprise de tooany accès ou des données, lors de l’application de stratégies d’autorisation AD alimentés sophistiquées, Azure

* Simplicité pour les utilisateurs

* Sécurité d’entreprise pour les applications et les données

### <a name="no-management-overhead"></a>Aucune surcharge de gestion

* Aucune gestion de compte ou mot de passe externe

* Aucune gestion manuelle des synchronisations ou du cycle de vie des comptes

* Aucune surcharge administrative externe

## <a name="you-can-easily-add-b2b-collaboration-users-tooyour-organization"></a>Vous pouvez ajouter facilement de l’organisation de tooyour utilisateurs B2B collaboration

Administrateurs peuvent ajouter des utilisateurs de collaboration (invité) B2B Bonjour [portail Azure](https://portal.azure.com).

![ajouter des utilisateurs invités](media/active-directory-b2b-what-is-azure-ad-b2b/adding-b2b-users-admin.png)

### <a name="enable-your-collaborators-toobring-their-own-identity"></a>Activer votre toobring collaborateurs leur propre identité.

Les collaborateurs B2B peuvent se connecter avec l’identité de leur choix. Si l’utilisateur de hello n’a pas un compte Microsoft ou un compte Azure AD : un est créé pour eux en toute transparence au moment de hello d’échange de l’offre.

![choix de l’identité à la connexion](media/active-directory-b2b-what-is-azure-ad-b2b/sign-in-identity-choice.png)

### <a name="delegate-tooapplication-and-group-owners"></a>Propriétaires de tooapplication et de groupe de délégué 
Application et les propriétaires de groupe peuvent ajouter des utilisateurs de B2B tooany directement les applications qui vous intéressent, s’il s’agit d’une application Microsoft ou non. Administrateurs peuvent déléguer toonon les utilisateurs administrateurs autorisation tooadd B2B. Que les administrateurs peuvent utiliser hello [le volet d’accès Application Azure AD](https://myapps.microsoft.com) tooadd B2B collaboration utilisateurs tooapplications ou des groupes.

![volet d’accès](media/active-directory-b2b-what-is-azure-ad-b2b/access-panel.png)

![ajout d’un membre](media/active-directory-b2b-what-is-azure-ad-b2b/add-member.png)

### <a name="authorization-policies-protect-your-corporate-content"></a>Les stratégies d’autorisation protègent votre contenu d’entreprise

Les stratégies d’accès conditionnel, telles que l’authentification multifacteur, peuvent être appliquées :
- Au niveau du client hello
- Au niveau de l’application hello
- Pour les données et les applications d’entreprise de tooprotect des utilisateurs spécifiques

![ajout d’un membre](media/active-directory-b2b-what-is-azure-ad-b2b/add-member.png)

### <a name="use-our-apis-and-sample-code-tooeasily-build-applications-tooonboard"></a>Utiliser nos API et les exemples de code tooeasily build applications tooonboard
Mettez vos partenaires externes sur le bord de manières personnalisées tooyour besoins.

À l’aide de hello [invitation de collaboration B2B API](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation), vous pouvez personnaliser votre expérience d’intégration, y compris la création des portails en libre service d’inscription. Nous fournissons un exemple de code pour un portail libre-service [sur Github](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).

![portail d’inscription](media/active-directory-b2b-what-is-azure-ad-b2b/sign-up-portal.png)

Avec Azure AD B2B collaboration, vous pouvez obtenir de puissance d’Azure AD tooprotect hello vos relations avec les partenaires d’une manière simple et intuitive de trouver les utilisateurs finaux. Profitez-en, hello de jointure des milliers d’organisations qui utilisent déjà Azure AD B2B pour leur collaboration externe !

## <a name="next-steps"></a>Étapes suivantes

* Expérience de l’administrateur se trouvent dans hello [portail Azure](https://portal.azure.com).

* Expériences de travail informations sont disponibles dans hello [volet d’accès](https://myapps.microsoft.com).

* Et, comme toujours, connectez-vous avec l’équipe de produit hello pour les commentaires, les discussions et les suggestions via notre [communauté technique de Microsoft](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B/bd-p/AzureAD_B2b).

Consultez les autres articles sur la collaboration B2B d'Azure AD :

* [Comment les administrateurs Azure Active Directory ajoutent-ils des utilisateurs B2B Collaboration ?](active-directory-b2b-admin-add-users.md)
* [Comment les professionnels de l’information ajoutent-ils des utilisateurs B2B Collaboration ?](active-directory-b2b-iw-add-users.md)
* [éléments Hello Hello e-mail d’invitation B2B collaboration](active-directory-b2b-invitation-email.md)
* [Utilisation d’une invitation B2B Collaboration](active-directory-b2b-redemption-experience.md)
* [Attribution de licences Azure AD B2B Collaboration](active-directory-b2b-licensing.md)
* [Résolution des problèmes d’Azure Active Directory B2B Collaboration](active-directory-b2b-troubleshooting.md)
* [Questions fréquemment posées (FAQ) sur Azure Active Directory B2B Collaboration](active-directory-b2b-faq.md)
* [API et personnalisation d’Azure Active Directory B2B Collaboration](active-directory-b2b-api.md)
* [Authentification multifacteur pour les utilisateurs B2B Collaboration](active-directory-b2b-mfa-instructions.md)
* [Ajouter des utilisateurs B2B Collaboration sans invitation](active-directory-b2b-add-user-without-invite.md)
* [B2B collaboration user auditing and reporting](active-directory-b2b-auditing-and-reporting.md) (Audit et création de rapports relatifs aux utilisateurs B2B Collaboration)
* [Index d’articles pour la gestion des applications dans Azure Active Directory](active-directory-apps-index.md)
