---
title: 'Azure Active Directory B2C : configuration Weibo | Microsoft Docs'
description: "Fournir tooconsumers d’abonnement et connectez-vous avec des comptes Weibo dans vos applications sont sécurisées par Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 1860de34-94cb-4ceb-851e-102f930f7230
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: c0648620f318046c1d9d24feb92a0c5f19c6a91a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-weibo-accounts"></a>Azure B2C Active Directory : Fournissent tooconsumers d’abonnement et connectez-vous avec les comptes Weibo

> [!NOTE]
> Cette fonctionnalité est en préversion. N’utilisez pas ce fournisseur d’identité dans votre environnement de production.
> 

## <a name="create-a-weibo-application"></a>Créer une application Weibo

toouse Weibo comme fournisseur d’identité dans Azure Active Directory (Azure AD) B2C, vous devez toocreate une application Weibo et lui fournir les paramètres appropriés hello. Vous devez un toodo de compte Weibo cela. Si vous n’en avez pas, vous pouvez en obtenir un à l’adresse [http://weibo.com/signup/signup.php?lang=en-us](http://weibo.com/signup/signup.php?lang=en-us).

### <a name="register-for-hello-weibo-developer-program"></a>Inscrivez-vous au programme pour développeur hello Weibo

1. Accédez toohello [portail des développeurs Weibo](http://open.weibo.com/) et connectez-vous avec vos informations d’identification du compte Weibo.
2. Une fois connecté, cliquez sur votre nom d’affichage dans l’angle supérieur droit de hello.
3. Dans la liste déroulante de hello, sélectionnez**编辑开发者信息**(informations destinées aux développeurs de modification).
4. Entrez les informations de hello requis dans le formulaire de hello et cliquez sur**提交**(envoyer).
5. Terminer le processus de vérification du courrier électronique hello.
6. Accédez toohello [page de vérification d’identité](http://open.weibo.com/developers/identity/edit).
7. Entrez les informations de hello requis dans le formulaire de hello et cliquez sur**提交**(envoyer).

### <a name="register-a-weibo-application"></a>Inscrire une application Weibo

1. Accédez toohello [nouvelle page de l’inscription d’application Weibo](http://open.weibo.com/apps/new).
2. Entrez les informations d’application nécessaire hello.
3. Cliquez sur **创建** (Créer).
4. Copier les valeurs hello de **clé application** et **Secret d’application**. Vous en aurez besoin ultérieurement.
5. Télécharger les photos de hello requis et entrez les informations nécessaires hello.
6. Cliquez sur **保存以上信息** (Enregistrer).
7. Cliquez sur **高级信息** (Informations avancées).
8. Cliquez sur**编辑**(modifier) le champ toohello suivant pour OAuth2.0**授权设置**(URL de redirection).
9. Entrez `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp` pour OAuth2.0 **授权设置** (URL de redirection). Par exemple, si votre `tenant_name` est contoso.onmicrosoft.com, jeu hello URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.
10. Cliquez sur **提交** (Envoyer).  

## <a name="configure-weibo-as-an-identity-provider-in-your-tenant"></a>Configurer Weibo en tant que fournisseur d’identité dans votre locataire
1. Suivez ces étapes trop[accédez Panneau de fonctionnalités toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) sur hello portail Azure.
2. Dans le panneau de fonctionnalités hello B2C, cliquez sur **fournisseurs d’identité**.
3. Cliquez sur **+ ajouter** haut hello du Panneau de hello.
4. Fournissez un nom convivial de **nom** pour la configuration du fournisseur d’identité hello. Par exemple, entrez « Weibo ».
5. Cliquez sur **Type de fournisseur d’identité**, sélectionnez **Weibo**, puis cliquez sur **OK**.
6. Cliquez sur **Configurer ce fournisseur d’identité**.
7. Entrez hello **clé application** que vous avez copiée précédemment comme hello **ID Client**.
8. Entrez hello **Secret d’application** que vous avez copiée précédemment comme hello **clé secrète Client**.
9. Cliquez sur **OK** puis cliquez sur **créer** toosave votre configuration Weibo.

