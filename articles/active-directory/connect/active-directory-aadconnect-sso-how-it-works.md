---
title: "Azure AD Connect : authentification unique transparente - Fonctionnement | Microsoft Docs"
description: "Cet article décrit le fonctionne de la fonctionnalité d’Azure Active Directory transparente Single Sign-On hello."
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
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: 17ce35b32832d241068ab878cf7aac42deab74ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-technical-deep-dive"></a>Authentification unique transparente Azure Active Directory : immersion technique

Cet article vous donne des détails techniques dans le fonctionne de la fonctionnalité d’Azure Active Directory transparente Single Sign-On (l’authentification unique transparente) hello.

>[!IMPORTANT]
>fonctionnalité d’authentification unique transparente Hello est actuellement en version préliminaire.

## <a name="how-does-seamless-sso-work"></a>Fonctionnement de l’authentification unique transparente (SSO)

Cette section comporte deux parties tooit :
1. programme d’installation Bonjour de fonctionnalité de l’authentification unique transparente hello.
2. Fonctionnement d’une transaction de connexion mono-utilisateur avec l’authentification unique transparente.

### <a name="how-does-set-up-work"></a>Comment la configuration s’opère-t-elle ?

L’authentification unique transparente s’active via Azure AD Connect comme indiqué [ici](active-directory-aadconnect-sso-quick-start.md). Lors de l’activation de fonctionnalité de hello, hello suit se produire :
- Un compte d’ordinateur nommé `AZUREADSSOACCT` (c’est-à-dire Azure AD) est créé dans votre instance Active Directory (AD) locale.
- clé de déchiffrement Kerberos du compte d’ordinateur Hello est partagée en toute sécurité auprès d’Azure AD.
- En outre, les deux Kerberos noms principaux de service (SPN) sont créés toorepresent deux URL sont utilisées pendant l’authentification dans Azure AD.

>[!NOTE]
> compte d’ordinateur Hello et les noms principaux de service Kerberos hello sont créés dans chaque forêt Active Directory vous synchronisez tooAzure AD (à l’aide d’Azure AD Connect) et pour les utilisateurs dont vous souhaitez l’authentification unique transparente. Déplacer hello `AZUREADSSOACCT` tooan de compte d’ordinateur unité organisation (UO) où les autres comptes d’ordinateur sont stockée tooensure qui il est géré dans hello la même façon et n’est pas supprimé.

>[!IMPORTANT]
>Il est fortement recommandé que vous [substituer la clé de déchiffrement hello Kerberos](active-directory-aadconnect-sso-faq.md#how-can-i-roll-over-the-kerberos-decryption-key-of-the-azureadssoacct-computer-account) Hello `AZUREADSSOACCT` compte d’ordinateur au moins tous les 30 jours.

### <a name="how-does-sign-in-with-seamless-sso-work"></a>Comment s’opère une connexion avec l’authentification unique transparente ?

Une fois l’installation de hello est terminée, l’authentification unique transparente fonctionne hello même façon que n’importe quel autre connectez-vous qui utilise l’authentification Windows (intégrée). flux de Hello est comme suit :

1. utilisateur de Hello tente tooaccess une application (par exemple, hello Outlook Web App - https://outlook.office365.com/owa/) à partir d’un appareil d’entreprise à un domaine à l’intérieur de votre réseau d’entreprise.
2. Si l’utilisateur de hello n’est pas déjà inscrit, utilisateur de hello est redirigé toohello Azure AD-page de connexion.

  >[!NOTE]
  >Si la demande de connexion hello Azure AD inclut un `domain_hint` (identifiant votre locataire - par exemple, contoso.onmicrosoft.com) ou `login_hint` (identifiant utilisateur hello - par exemple, user@contoso.onmicrosoft.com ou user@contoso.com) paramètre, puis l’étape 2 est ignorée.

3. types d’utilisateur Hello dans leur nom d’utilisateur dans la page de connexion hello Azure AD.
4. Azure AD à l’aide de JavaScript dans l’arrière-plan de hello, défis hello navigateur, via une réponse non autorisé 401, tooprovide un ticket Kerberos.
5. navigateur de Hello, à son tour, demande un ticket à partir d’Active Directory pour hello `AZUREADSSOACCT` compte d’ordinateur (c'est-à-dire, Azure AD).
6. Active Directory recherche de compte d’ordinateur hello et retourne un navigateur toohello de ticket Kerberos crypté avec mot de passe du compte d’ordinateur hello.
7. navigateur de Hello transfère le ticket Kerberos de hello elle acquis à partir d’Active Directory tooAzure AD (sur l’un des hello [Azure AD URL ajouté précédemment des paramètres de la zone Intranet du navigateur toohello](active-directory-aadconnect-sso-quick-start.md#step-3-roll-out-the-feature)).
8. Azure AD déchiffre hello ticket Kerberos, qui inclut l’identité hello d’utilisateur hello connecté à un appareil d’entreprise hello, à l’aide de hello précédemment de clé partagée.
9. Après l’évaluation, Azure AD retourne une application de jeton toohello précédent ou demande hello utilisateur tooperform preuves supplémentaires, telles que l’authentification multifacteur.
10. Si l’authentification utilisateur hello dans réussit, utilisateur de hello est application hello de tooaccess en mesure de.

Hello diagramme suivant illustre tous les composants de hello et étapes hello.

![Authentification unique transparente](./media/active-directory-aadconnect-sso/sso2.png)

L’authentification unique transparente est opportuniste, ce qui signifie qu’en cas d’échec, expérience de connexion hello revient comportement normal de tooits - c'est-à-dire, hello utilisateur doit tooenter toosign de leur mot de passe dans.

## <a name="next-steps"></a>Étapes suivantes

- [**Démarrage rapide**](active-directory-aadconnect-sso-quick-start.md) : découvrez l’authentification unique transparente Azure AD.
- [**Forum aux Questions** ](active-directory-aadconnect-sso-faq.md) -réponses elles sonttrop aux questions.
- [**Résoudre les problèmes** ](active-directory-aadconnect-troubleshoot-sso.md) -en savoir comment tooresolve commun problèmes avec la fonctionnalité de hello.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) : pour le dépôt de nouvelles demandes de fonctionnalités.
