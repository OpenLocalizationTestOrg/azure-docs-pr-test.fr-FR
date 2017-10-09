---
title: "aaaManage l’authentification unique pour le Proxy d’Application Azure AD | Documents Microsoft"
description: "En savoir plus sur les concepts de base hello de l’authentification unique avec le Proxy d’Application"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: a278751a5cb1bf98c970a4e5d2eb3edc3b784096
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-ad-application-proxy-provide-single-sign-on"></a>Comment le proxy d’application Azure AD fournit-il l’authentification unique ?

L’authentification unique est un élément clé du proxy d’application Azure AD.  Il fournit une expérience utilisateur optimale de hello étant donné que vos utilisateurs disposent uniquement des toosign dans tooAzure Active Directory dans le cloud de hello. Une fois qu’ils s’authentifient tooAzure Active Directory, le connecteur de Proxy d’Application hello gère application locale de hello authentification toohello. l’application Hello principale ne peut pas différencier hello un utilisateur distant, la connexion via le Proxy d’Application et une utilisation régulière sur un appareil appartenant à un domaine. 

toouse Azure Active Directory pour les applications tooyour de l’authentification unique, vous devez tooselect **Azure Active Directory** en tant que méthode de pré-authentification hello. Si vous sélectionnez **Passthrough** vos utilisateurs ne s’authentifier tooAzure Active Directory du tout, mais sont dirigées toohello droite à l’application. Vous pouvez configurer ce paramètre lorsque vous publiez une application, tout d’abord, ou qui accédez application tooyour Bonjour portail Azure et modifiez les paramètres de Proxy d’Application hello. 

toosee vos options d’authentification uniques, procédez comme suit :

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Accédez trop**Azure Active Directory** > **des applications d’entreprise** > **toutes les applications**.
3. Application hello Select dont l’authentification unique sur les options vous souhaitez toomanage.
4. Sélectionnez **Authentification unique**.

   ![Menu déroulant de l’authentification unique](./media/application-proxy-sso-overview/single-sign-on-mode.png)

menu déroulant de Hello montre cinq options pour l’application de tooyour de l’authentification unique :

* Authentification unique Azure AD désactivée
* Authentification par mot de passe
* Authentification liée
* Authentification Windows intégrée
* Authentification basée sur l’en-tête

## <a name="azure-ad-single-sign-on-disabled"></a>Authentification unique Azure AD désactivée

Si vous ne souhaitez pas toouse intégration d’Azure Active Directory pour l’application de tooyour de l’authentification unique, choisissez **AD Azure l’authentification unique sur désactivé**. Lorsque cette option est sélectionnée, vos utilisateurs pourraient devoir s’authentifier deux fois. Tout d’abord, ils s’authentifier tooAzure Active Directory et puis connectez-vous à application toohello lui-même. 

Cette option est un bon choix si votre application sur site ne nécessite pas les utilisateurs tooauthenticate, mais que vous souhaitez définir tooadd Azure Active Directory comme une couche de sécurité pour l’accès à distance. 

## <a name="password-based-sign-on"></a>Authentification par mot de passe

Si vous souhaitez toouse Azure Active Directory comme un coffre de mot de passe pour vos applications locales, choisissez **mot de passe de session**. Cette option constitue un bon choix si votre application s’authentifie à l’aide d’une combinaison nom d’utilisateur/mot de passe au lieu d’en-têtes ou de jetons d’accès. Avec le mot de passe d’authentification, vos utilisateurs doivent toosign Bonjour d’application toohello première fois qu’ils y accèdent. Après cela, Azure Active Directory fournit hello username et password pour le compte d’utilisateur de hello. 

Pour plus d’informations sur la configuration de l’authentification par mot de passe, consultez la page [Authentification unique avec le proxy d’application](application-proxy-sso-azure-portal.md).

## <a name="linked-sign-on"></a>Authentification liée

Si vous avez déjà configuré une solution d’authentification unique pour vos identités locales, choisissez **Authentification liée**. Cette option permet aux solutions de l’authentification unique Azure Active Directory tooleverage existantes, mais toujours permet à vos utilisateurs application toohello de l’accès à distance. 

Pour en savoir plus sur l’authentification liée (antérieurement appelée authentification unique existante), consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).

## <a name="integrated-windows-authentication"></a>Authentification Windows intégrée

Si vos applications locales utilisent intégré Windows Authentication(IWA) ou si vous souhaitez toouse la délégation Kerberos (KCD) pour l’authentification unique, choisissez **l’authentification Windows intégrée**. Avec cette option, vos utilisateurs doivent uniquement tooauthenticate tooAzure Active Directory, et puis connecteur de Proxy d’Application hello emprunte l’identité hello utilisateur tooget un jeton Kerberos et signe dans toohello application. 

Pour plus d’informations sur la configuration de l’authentification Windows intégrée, consultez la section [Délégation contrainte Kerberos pour l’authentification unique à vos applications avec le proxy d’application](active-directory-application-proxy-sso-using-kcd.md).

## <a name="header-based-sign-on"></a>Authentification basée sur l’en-tête 

Si vos applications utilisent des en-têtes pour l’authentification, choisissez **Authentification basée sur l’en-tête**. Avec cette option, vos utilisateurs doivent uniquement tooauthentication hello Azure Active Directory. Les partenaires Microsoft avec un service d’authentification tiers appelé PingAccess qui traduit le jeton d’accès Azure Active Directory hello dans un format d’en-tête pour une application hello. 

Pour plus d’informations sur la configuration de l’authentification basée sur l’en-tête, consultez la page [Authentification basée sur l’en-tête pour une authentification unique avec le Proxy d’application et PingAccess](application-proxy-ping-access.md).

## <a name="next-steps"></a>Étapes suivantes

- [Authentification unique avec le proxy d’application](application-proxy-sso-azure-portal.md)
- [Délégation contrainte Kerberos pour l’authentification unique à vos applications avec le proxy d’application](active-directory-application-proxy-sso-using-kcd.md)
- [Authentification basée sur l’en-tête pour une authentification unique avec le Proxy d’application et PingAccess](application-proxy-ping-access.md) 
