---
title: 'Azure Active Directory B2C : Configuration de WeChat | Microsoft Docs'
description: "Fournir tooconsumers d’abonnement et connectez-vous avec des comptes WeChat dans vos applications sont sécurisées par Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: d2424c66-ba68-4d82-847e-d137683527b0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: 92cc3579d818d2379a503ccc695138b33a34466d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-wechat-accounts"></a>Azure B2C Active Directory : Fournissent tooconsumers d’abonnement et connectez-vous avec les comptes WeChat

> [!NOTE]
> Cette fonctionnalité est en préversion.
> 

## <a name="create-a-wechat-application"></a>Créer une application WeChat

toouse WeChat comme fournisseur d’identité dans Azure Active Directory (Azure AD) B2C, vous devez toocreate une application WeChat et lui fournir les paramètres appropriés hello. Vous devez un toodo de compte WeChat cela. Si vous n’en avez pas, vous pouvez en obtenir un en vous inscrivant via une de leurs applications mobiles ou à l’aide de votre numéro QQ. Après cela, obtenir votre compte avec un programme pour développeur WeChat hello. Pour plus d’informations, consultez la [page suivante](http://kf.qq.com/faq/161220Brem2Q161220uUjERB.html):

### <a name="register-a-wechat-application"></a>Inscrire une application WeChat

1. Accédez trop[https://open.weixin.qq.com/](https://open.weixin.qq.com/) et connectez-vous.
2. Cliquez sur **管理中心** (Centre de gestion).
3. Suivez les étapes nécessaires de hello tooregister une nouvelle application.
4. Pour **授权回调域** (URL de rappel), entrez `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`. Par exemple, si votre `tenant_name` est contoso.onmicrosoft.com, jeu hello URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.
5. Rechercher et copie hello **ID d’application** et **clé application**. Vous en aurez besoin ultérieurement.

## <a name="configure-wechat-as-an-identity-provider-in-your-tenant"></a>Configurer WeChat en tant que fournisseur d’identité dans votre locataire
1. Suivez ces étapes trop[accédez Panneau de fonctionnalités toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) sur hello portail Azure.
2. Dans le panneau de fonctionnalités hello B2C, cliquez sur **fournisseurs d’identité**.
3. Cliquez sur **+ ajouter** haut hello du Panneau de hello.
4. Fournissez un nom convivial de **nom** pour la configuration du fournisseur d’identité hello. Par exemple, entrez « WeChat ».
5. Cliquez sur **Type de fournisseur d’identité**, sélectionnez **WeChat**, puis cliquez sur **OK**.
6. Cliquez sur **Configurer ce fournisseur d’identité**.
7. Entrez hello **clé application** que vous avez copiée précédemment comme hello **ID Client**.
8. Entrez hello **Secret d’application** que vous avez copiée précédemment comme hello **clé secrète Client**.
9. Cliquez sur **OK** puis cliquez sur **créer** toosave votre configuration WeChat.

