---
title: "aaaSingle authentification tooapps avec Proxy d’Application Azure AD | Documents Microsoft"
description: "Activer l’authentification unique pour vos applications publiées sur site avec le Proxy d’Application Azure AD Bonjour portail Azure."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d94ac3f4-cd33-4c51-9d19-544a528637d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 5ff288d36163b74215677d9e34c93c985ac33d54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="password-vaulting-for-single-sign-on-with-application-proxy"></a>Authentification unique avec mise au coffre des mots de passe par le biais du proxy d’application

Le service Proxy d’application Azure Active Directory vous aide à améliorer la productivité en publiant des applications locales afin que les employés travaillant à distance puissent également y accéder. Bonjour portail Azure, vous pouvez également configurer unique (SSO) toothese applications avec authentification. Vos utilisateurs doivent uniquement tooauthenticate avec Azure AD, et ils peuvent accéder à votre application d’entreprise sans avoir à nouveau les toosign.

Le proxy d’application prend en charge plusieurs [modes d’authentification unique](application-proxy-sso-overview.md). L’authentification par mot de passe est destinée aux applications qui utilisent une combinaison nom d’utilisateur/mot de passe pour l’authentification. Lorsque vous configurez le mot de passe de session pour votre application, vos utilisateurs ont toosign dans l’application locale de toohello une seule fois. Après cela, Azure Active Directory stocke les informations de connexion hello et fournit automatiquement il toohello application lorsque vos utilisateurs l’accès à distance. 

Vous devez avoir déjà publié et testé votre application avec le proxy d’application. Dans le cas contraire, suivez les étapes de hello dans [publier des applications à l’aide du Proxy d’Application Azure AD](application-proxy-publish-azure-portal.md) puis revenez ici. 

## <a name="set-up-password-vaulting-for-your-application"></a>Configurer le stockage de mots de passe pour votre application

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com) en tant qu’administrateur.
2. Sélectionnez **Azure Active Directory** > **Applications d’entreprise** > **Toutes les applications**.
3. À partir de la liste de hello, sélectionnez application hello que vous souhaitez tooset les avec l’authentification unique.  
4. Sélectionnez **Authentification unique**.

   ![Sélectionner l’authentification unique](./media/application-proxy-sso-azure-portal/select-sso.png)

5. Pour le mode d’authentification unique de hello, choisissez **mot de passe de session**.
6. Pour l’URL de connexion hello, entrez hello URL pour la page de hello où les utilisateurs entrent leur toosign nom d’utilisateur et mot de passe dans l’application tooyour en dehors du réseau d’entreprise de hello. Cela peut être hello URL externe que vous avez créé lorsque vous avez publié l’application hello via le Proxy d’Application. 

   ![Choisissez Authentification par mot de passe et entrez votre URL.](./media/application-proxy-sso-azure-portal/password-sso.png)

7. Sélectionnez **Enregistrer**.

<!-- Need toorepro?
7. hello page should tell you that a sign-in form was successfully detected at hello provided URL. If it doesn't, select **Configure [your app name] Password Single Sign-on Settings** and choose **Manually detect sign-in fields**. Follow hello instructions toopoint out where hello sign-in credentials go. 
-->

## <a name="test-your-app"></a>Test de l'application

Accédez tooexternal URL que vous avez configuré pour l’application de tooyour d’accès à distance. Connectez-vous avec vos informations d’identification pour cette application (ou hello pour un compte de test que vous avez configurée avec un accès). Une fois que vous êtes connecté avec succès, vous devez être en mesure de tooleave hello application et revenez sans entrer de nouveau vos informations d’identification. 

## <a name="next-steps"></a>Étapes suivantes

- En savoir plus sur d’autres façons tooimplement [Single sign-on avec le Proxy d’Application](application-proxy-sso-overview.md)
- En savoir plus sur les [considérations de sécurité pour l’accès aux applications à distance avec le proxy d’application Azure AD](application-proxy-security-considerations.md)