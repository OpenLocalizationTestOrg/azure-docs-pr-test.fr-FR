---
title: 'Azure AD Connect : authentification unique transparente | Microsoft Docs'
description: "Cette rubrique décrit l’Azure Active Directory (Azure AD) transparente l’authentification unique et comment elle permet de vous tooprovide true l’authentification unique pour les utilisateurs du bureau d’entreprise à l’intérieur de votre réseau d’entreprise."
services: active-directory
keywords: "Qu’est-ce qu’Azure AD Connect, Installation d’Active Directory, Composants requis pour Azure AD, SSO, Authentification unique"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: billmath
ms.openlocfilehash: 11c778c37ee39866dcc3a14ab648cfcd8e322e47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on"></a>Authentification unique transparente Azure Active Directory

## <a name="what-is-azure-active-directory-seamless-single-sign-on"></a>Qu’est-ce que l’authentification unique transparente Azure Active Directory ?

Azure Active Directory transparente Single Sign-On (Azure AD transparente l’authentification unique) connecte automatiquement les utilisateurs lorsqu’ils sont sur des appareils d’entreprise connectés tooyour réseau de l’entreprise. Lorsque activé, les utilisateurs ne doivent tootype dans leur toosign des mots de passe dans tooAzure AD et en règle générale, de même type dans leurs noms d’utilisateurs. Cette fonctionnalité fournit à vos utilisateurs un accès facile tooyour les applications cloud sans avoir besoin de tous les composants de site supplémentaires.

L’authentification unique transparente peut être combiné avec deux hello [synchronisation du hachage de mot de passe](active-directory-aadconnectsync-implement-password-synchronization.md) ou [authentification directe](active-directory-aadconnect-pass-through-authentication.md) méthodes de connexion.

![Authentification unique transparente](./media/active-directory-aadconnect-sso/sso1.png)

>[!IMPORTANT]
>L’authentification unique transparente est actuellement en préversion. Cette fonctionnalité est _pas_ tooActive applicable Directory Federation Services (ADFS).

## <a name="key-benefits"></a>Principaux avantages

- *Une meilleure expérience utilisateur*
  - Les utilisateurs sont automatiquement connectés aux applications cloud et locales.
  - Les utilisateurs n’aient tooenter leurs mots de passe à plusieurs reprises.
- *Toodeploy facile & administrer*
  - Aucun composant supplémentaire ne nécessaire sur site toomake ce travail.
  - Fonctionne avec n’importe quelle méthode d’authentification cloud - [Synchronisation de hachage de mot de passe](active-directory-aadconnectsync-implement-password-synchronization.md) ou [Authentification directe](active-directory-aadconnect-pass-through-authentication.md).
  - Peut être déployée toosome ou tous vos utilisateurs à l’aide de la stratégie de groupe.
  - Inscrire des appareils non Windows 10 avec Azure AD sans avoir besoin de hello de n’importe quelle infrastructure AD FS. Cette fonctionnalité doit toouse version 2.1 ou ultérieure de hello [client de jonction](https://www.microsoft.com/download/details.aspx?id=53554).

## <a name="feature-highlights"></a>Présentation des fonctionnalités

- Nom d’utilisateur de connexion peut être un nom d’utilisateur de hello local par défaut (`userPrincipalName`) ou un autre attribut configuré dans Azure AD Connect (`Alternate ID`). Les deux utilisent le travail de cas étant donné que l’authentification unique transparente utilise hello `securityIdentifier` revendication hello toolook de ticket Kerberos de l’objet utilisateur correspondant de hello dans Azure AD.
- L’authentification unique transparente est une fonctionnalité opportuniste. Si elle échoue pour une raison quelconque, expérience d’authentification de l’utilisateur du hello repasse comportement normal de tooits - c'est-à-dire, hello utilisateur doit tooenter leur mot de passe sur la page de connexion hello.
- Si une application transfère un `domain_hint` (OpenID Connect) ou `whr` paramètre (SAML) - identifier votre locataire, ou `login_hint` paramètre - identifiant utilisateur de hello, dans sa demande de connexion Azure AD, les utilisateurs sont automatiquement connectés sans les Saisie des noms d’utilisateurs ou des mots de passe.
- L’authentification unique transparente peut être activée par le biais d’Azure AD Connect.
- Il s’agit d’une fonctionnalité gratuite et vous n’avez pas besoin des éditions payantes d’Azure AD toouse il.
- L’authentification unique est prise en charge par les clients basés sur le navigateur web et les clients Office qui prennent en charge [l’authentification moderne](https://aka.ms/modernauthga) sur les plateformes et navigateurs compatibles avec l’authentification Kerberos :

| Système d’exploitation\Navigateur |Internet Explorer|Edge|Google Chrome|Mozilla Firefox|Safari|
| --- | --- |--- | --- | --- | -- 
|Windows 10|Oui|Non|Oui|Oui\*|N/A
|Windows 8.1|Oui|N/A|Oui|Oui\*|N/A
|Windows 8|Oui|N/A|Oui|Oui\*|N/A 
|Windows 7|Oui|N/A|Oui|Oui\*|N/A
|Mac OS X|N/A|N/A|Oui\*|Oui\*|Oui\*

\*Nécessite une [configuration supplémentaire](active-directory-aadconnect-sso-quick-start.md#browser-considerations)

>[!IMPORTANT]
>Nous avons récemment restaurée prise en charge de bord tooinvestigate problèmes signalés par le client.

>[!NOTE]
>Pour Windows 10, il est recommandé de hello toouse [Azure AD Join](../active-directory-azureadjoin-overview.md) pour hello optimale unique sur l’authentification auprès d’Azure AD.

## <a name="next-steps"></a>Étapes suivantes

- [**Démarrage rapide**](active-directory-aadconnect-sso-quick-start.md) : découvrez l’authentification unique transparente Azure AD.
- [**Immersion technique**](active-directory-aadconnect-sso-how-it-works.md) : découvrez comment fonctionne cette fonctionnalité.
- [**Forum aux Questions** ](active-directory-aadconnect-sso-faq.md) -réponses elles sonttrop aux questions.
- [**Résoudre les problèmes** ](active-directory-aadconnect-troubleshoot-sso.md) -en savoir comment tooresolve commun problèmes avec la fonctionnalité de hello.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) : pour le dépôt de nouvelles demandes de fonctionnalités.
