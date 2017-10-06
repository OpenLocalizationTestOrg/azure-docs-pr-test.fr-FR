---
title: 'Azure Active Directory B2C : configuration QQ | Microsoft Docs'
description: "Fournir tooconsumers d’abonnement et connectez-vous avec des comptes QQ dans vos applications sont sécurisées par Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 18c2cf94-8004-4de1-81c2-e45be65ce12d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: 896d6221e01d15de1652a5717cf1f65619101e0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-qq-accounts"></a>Azure B2C Active Directory : Fournir tooconsumers d’abonnement et connectez-vous avec les comptes QQ

> [!NOTE]
> Cette fonctionnalité est en préversion.
> 

## <a name="create-a-qq-application"></a>Créer une application QQ

toouse QQ comme fournisseur d’identité dans Azure Active Directory (Azure AD) B2C, vous devez toocreate une application QQ et lui fournir les paramètres appropriés hello. Vous devez un toodo de compte QQ cela. Si vous n’avez pas, vous pouvez en obtenir un à la page [https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033](https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033).

### <a name="register-for-hello-qq-developer-program"></a>Inscrivez-vous au programme pour développeur QQ hello

1. Accédez toohello [portail des développeurs QQ](http://open.qq.com) et connectez-vous avec vos informations d’identification du compte QQ.
2. Une fois connecté, accédez trop[http://open.qq.com/reg](http://open.qq.com/reg) tooregister vous-même en tant que développeur.
3. Dans le menu de hello, sélectionnez**个人**(developer individuel).
4. Entrez les informations de hello requis dans le formulaire de hello et cliquez sur**下一步**(étape suivante).
5. Terminer le processus de vérification du courrier électronique hello.

> [!NOTE]
> Vous devez toowait quelques jours toobe approuvé une fois inscrit en tant que développeur. 

### <a name="register-a-qq-application"></a>Inscrire une application QQ

1. Accédez trop[https://connect.qq.com/index.html](https://connect.qq.com/index.html).
2. Cliquez sur **应用管理** (Gestion de l’application).
3. Cliquez sur **创建应用** (Création d’application).
4. Entrez les informations d’application nécessaire hello.
5. Cliquez sur **创建应用** (Création d’application).
6. Entrez les informations de hello requis.
7. Pourquoi**授权回调域**(URL de rappel), entrez `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`. Par exemple, si votre `tenant_name` est contoso.onmicrosoft.com, jeu hello URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.
8. Cliquez sur **创建应用** (Création d’application).
9. Dans la page de confirmation hello, cliquez sur**应用管理**page de gestion des applications (gestion des applications) tooreturn toohello.
10. Cliquez sur**查看**prochaine application toohello (vue), vous venez de créer.
11. Cliquez sur **修改** (Modifier).
12. À partir de hello en haut de page de hello, copiez hello **ID d’application** et **clé application**.

## <a name="configure-qq-as-an-identity-provider-in-your-tenant"></a>Configuration de QQ en tant que fournisseur d'identité dans votre client
1. Suivez ces étapes trop[accédez Panneau de fonctionnalités toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) sur hello portail Azure.
2. Dans le panneau de fonctionnalités hello B2C, cliquez sur **fournisseurs d’identité**.
3. Cliquez sur **+ ajouter** haut hello du Panneau de hello.
4. Fournissez un nom convivial de **nom** pour la configuration du fournisseur d’identité hello. Par exemple, entrez « QQ ».
5. Cliquez sur **Type de fournisseur d’identité**, sélectionnez **QQ**, puis cliquez sur **OK**.
6. Cliquez sur **Configurer ce fournisseur d’identité**.
7. Entrez hello **clé application** que vous avez copiée précédemment comme hello **ID Client**.
8. Entrez hello **Secret d’application** que vous avez copiée précédemment comme hello **clé secrète Client**.
9. Cliquez sur **OK** puis cliquez sur **créer** toosave votre configuration QQ.

