---
title: "Azure AD Connect : authentification directe | Microsoft Docs"
description: "Cet article présente l’authentification directe Azure Active Directory (Azure AD) et explique comment l’utiliser pour autoriser les connexions à Azure AD en validant les mots de passe des utilisateurs à partir d’Active Directory local."
services: active-directory
keywords: "qu’est-ce que l’authentification directe Azure AD Connect, installation d’Active Directory, composants requis pour Azure AD, SSO, Authentification unique"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: billmath
ms.openlocfilehash: 56cfb2c4f4afc7d46c926a392ae6ec01e96224d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="user-sign-in-with-azure-active-directory-pass-through-authentication"></a>Connexion de l’utilisateur avec l’authentification directe Azure Active Directory

## <a name="what-is-azure-active-directory-pass-through-authentication"></a>Qu’est-ce que l’authentification directe Azure Active Directory ?

Azure Active Directory (Azure AD) pass-through Authentication permet à votre toosign utilisateurs tooboth locaux et les applications cloud à l’aide de hello mêmes mots de passe. Cette fonctionnalité offre aux utilisateurs une meilleure expérience - un moins tooremember de mot de passe et réduit les coûts de support technique informatique étant donné que vos utilisateurs sont moins susceptibles de tooforget comment toosign dans. Lorsque les utilisateurs se connectent à l’aide d’Azure AD, cette fonctionnalité valide les mots de passe utilisateurs directement à partir d’Active Directory local.

Cette fonctionnalité est une alternative trop[synchronisation du hachage de mot de passe Azure AD](active-directory-aadconnectsync-implement-password-synchronization.md), qui fournit hello même avantage de tooorganizations de l’authentification cloud. Toutefois, les stratégies de conformité et de sécurité de certaines organisations ne permettent pas ces organisations toosend mot de passe, même dans un format haché, en dehors de leurs limites internes. Authentification directe est hello bonne solution pour ces organisations.

![Authentification directe Azure AD](./media/active-directory-aadconnect-pass-through-authentication/pta1.png)

Vous pouvez combiner l’authentification directe avec hello [transparente Single Sign-On](active-directory-aadconnect-sso.md) fonctionnalité. Ainsi, lorsque vos utilisateurs accèdent à des applications sur leurs ordinateurs d’entreprise à l’intérieur de votre réseau d’entreprise, tootype dans leur toosign des mots de passe dans n’est nécessaire.

>[!IMPORTANT]
>L’authentification directe Azure AD est actuellement en préversion.

## <a name="key-benefits-of-using-azure-ad-pass-through-authentication"></a>Avantages clés de utilisation de l’authentification directe Azure AD

- *Une meilleure expérience utilisateur*
  - Les utilisateurs utilisent hello même toosign des mots de passe en local et les applications cloud.
  - Les utilisateurs passent moins de temps ils s’adressent toohello technique informatique résolution des problèmes liés au mot de passe.
  - Les utilisateurs peuvent effectuer [gestion de mot de passe libre-service](../active-directory-passwords-overview.md) tâches dans le cloud de hello.
- *Toodeploy facile & administrer*
  - Des déploiements locaux ou une configuration réseau complexes ne sont pas nécessaires.
  - Besoins simplement un toobe léger agent installé sur site.
  - Aucun frais de gestion. l’agent de Hello reçoit automatiquement des améliorations et correctifs de bogues.
- *Sécuriser*
  - Les mots de passe local ne sont jamais stockées dans le cloud hello dans n’importe quelle forme.
  - agent de Hello effectue uniquement des connexions sortantes à partir de votre réseau. Par conséquent, aucun agent de hello tooinstall exigence est dans un réseau de périmètre, également appelé un réseau de périmètre.
  - Il protège vos comptes utilisateur en toute transparence avec les [stratégies d’accès conditionnel d’Azure AD](../active-directory-conditional-access-azure-portal.md), y compris l’authentification multifacteur (MFA) et en [filtrant des attaques de mot de passe par recherche exhaustive](active-directory-aadconnect-pass-through-authentication-smart-lockout.md).
- *Hautement disponible*
  - Agents supplémentaires peuvent être installés sur plusieurs local serveurs tooprovide haute disponibilité des demandes de connexion.

## <a name="feature-highlights"></a>Présentation des fonctionnalités

- Prend en charge la connexion de l’utilisateur dans toutes les applications basées sur un navigateur web et dans les applications clientes Microsoft Office qui utilisent [l’authentification moderne](https://aka.ms/modernauthga).
- Authentification dans les noms d’utilisateur peut être un nom d’utilisateur de hello local par défaut (`userPrincipalName`) ou un autre attribut configuré dans Azure AD Connect (appelé `Alternate ID`).
- fonctionnalité de Hello fonctionne de façon transparente avec [accès conditionnel](../active-directory-conditional-access.md) fonctionnalités, telles que l’authentification multifacteur (MFA) toohelp sécuriser vos utilisateurs.
- Les environnements à plusieurs forêts sont pris en charge s’il existe des approbations de forêts entre les forêts AD et si le routage du suffixe de leurs noms est configuré correctement.
- Il s’agit d’une fonctionnalité gratuite et vous n’avez pas besoin des éditions payantes d’Azure AD toouse il.
- Elle peut être activée via [Azure AD Connect](active-directory-aadconnect.md).
- Elle utilise un agent local léger qui écoute et répond toopassword les demandes de validation.
- L’installation de plusieurs agents fournit une haute disponibilité des requêtes de connexion.
- Il [protège](active-directory-aadconnect-pass-through-authentication-smart-lockout.md) vos comptes locale contre les attaques en force les attaques de mot de passe dans le cloud de hello.

## <a name="next-steps"></a>Étapes suivantes

- [**Démarrage rapide**](active-directory-aadconnect-pass-through-authentication-quick-start.md) : soyez opérationnel avec l’authentification directe Azure AD.
- [**Limitations actuelles**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) : cette fonctionnalité est actuellement en préversion. Découvrez les scénarios pris en charge et ceux qui ne le sont pas.
- [**Immersion technique**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) : découvrez comment fonctionne cette fonctionnalité.
- [**Forum aux Questions** ](active-directory-aadconnect-pass-through-authentication-faq.md) -réponses elles sonttrop aux questions.
- [**Résoudre les problèmes** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -en savoir comment tooresolve commun problèmes avec la fonctionnalité de hello.
- [**Authentification unique transparente Azure AD**](active-directory-aadconnect-sso.md) : explorez en détail cette fonctionnalité complémentaire.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) : pour formuler des demandes de nouvelles fonctionnalités.
