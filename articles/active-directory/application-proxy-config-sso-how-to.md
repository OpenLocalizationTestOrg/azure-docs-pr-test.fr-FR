---
title: "aaaHow tooconfigure unique authentification tooan application de Proxy d’Application | Documents Microsoft"
description: "Comment configurer rapidement une application proxy tooyour de l’authentification unique"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: e1289203177c77b3a8bcc9058c5c0b8ae50f243e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-single-sign-on-tooan-application-proxy-application"></a>Comment tooconfigure single sign-on tooan application de Proxy d’Application

L’authentification unique (SSO) permet à votre tooaccess aux utilisateurs une application sans authentifier plusieurs fois. Il permet toooccur d’authentification unique de hello dans cloud hello, par rapport à Azure Active Directory et le service de hello ou connecteur tooimpersonate hello utilisateur toocomplete toutes les demandes d’authentification supplémentaires à partir de l’application hello.

## <a name="how-tooconfigure-single-sign-on"></a>Comment tooconfigure d’authentification unique
tooconfigure l’authentification unique, d’abord vous assurer que votre application est configurée pour l’authentification préalable via Azure Active Directory. toodo, accédez trop**Azure Active Directory**  - &gt; **des Applications d’entreprise**  - &gt; **toutes les Applications**  - &gt; Votre application  **- &gt; le Proxy d’Application**. Dans cette page, vous voyez hello « Pré-authentification » champ et assurez-vous qu’est défini trop « Azure Active Directory. 

Pour plus d’informations sur les méthodes de pré-authentification hello, consultez l’étape 4 de hello [document de publication d’application](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).

   ![Méthode de pré-authentification dans le Portail Azure](./media/application-proxy-config-sso-how-to/app-proxy.png)

## <a name="configuring-single-sign-on-modes-for-application-proxy-applications"></a>Configuration des modes d’authentification unique pour les applications de proxy d’application
Ensuite, nous configurons type spécifique de hello de l’authentification unique. méthodes d’authentification Hello sont classées selon le type d’application de serveur principal d’authentification hello. Les applications de proxy d’application prennent en charge trois types d’authentification :

-   **Mot de passe de session**: mot de passe de session peut servir pour toute application qui utilise les champs nom d’utilisateur et mot de passe sur toosign. Les étapes de configuration sont décrites dans notre [documentation sur la configuration de l’authentification SSO par mot de passe](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#bring-your-own-password-sso-applications).

-   **Authentification Windows intégrée** : pour les applications utilisant l’authentification Windows intégrée, l’authentification unique est activée par le biais de la délégation Kerberos contrainte (KCD, Kerberos Constrained Delegation). Cela autorise les connecteurs de Proxy d’Application dans les utilisateurs Active Directory tooimpersonate et toosend et recevoir des jetons en leur nom. Vous trouverez des détails sur la configuration de KCD Bonjour [Single Sign-On avec la documentation de KCD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd).

-   **Authentification basée sur l’en-tête** : l’authentification basée sur l’en-tête est activée par le biais d’un partenariat. Elle nécessite une configuration supplémentaire. Pour plus d’informations sur le partenariat de hello et des instructions détaillées pour la configuration d’application tooan d’authentification unique qui utilise des en-têtes pour l’authentification, consultez hello [PingAccess pour la documentation d’Azure AD](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access).

Chacune de ces options sont accessibles à partir d’applications tooyour dans « Applications d’entreprise » et ouverture hello **Single Sign-On** page sur le menu de gauche hello. Notez que si votre application a été créée dans l’ancien portail de hello, vous pouvez voir pas toutes ces options.

Cette page propose aussi l’option d’authentification « Authentification liée », également prise en charge par le proxy d’application. Toutefois, notez que cette option n’ajoute pas d’application de toohello de l’authentification unique. Ceci dit application hello peut-être déjà l’authentification unique implémentée à l’aide d’un autre service, telles que les Services de fédération Active Directory. 

Cette option permet une toocreate admin une application tooan lien que les utilisateurs se retrouver tout d’abord sur lors de l’accès d’application hello. Par exemple, s’il existe une application qui est configuré tooauthenticate les utilisateurs à l’aide d’Active Directory Federation Services 2.0, un administrateur peut utiliser hello « lié authentification » option toocreate un tooit lien sur le volet d’accès hello.

## <a name="next-steps"></a>Étapes suivantes
[Fournissent des applications de tooyour de l’authentification unique avec le Proxy d’Application](active-directory-application-proxy-sso-using-kcd.md)
