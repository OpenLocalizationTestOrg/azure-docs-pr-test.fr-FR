---
title: 'Azure Active Directory B2C : configuration Google+ | Microsoft Docs'
description: "Fournir tooconsumers d’abonnement et connectez-vous avec des comptes Google + dans vos applications sont sécurisées par Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 4dcca66f-29e4-4b4d-8840-50baad736bd7
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 6ef66eb17777acd95b5f4745ed6097c77e37663b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-google-accounts"></a>Azure B2C Active Directory : Fournir tooconsumers d’abonnement et connectez-vous avec des comptes Google +
## <a name="create-a-google-application"></a>Création d’une application Google+
toouse + Google comme fournisseur d’identité dans Azure Active Directory (Azure AD) B2C, vous devez toocreate une application Google + et lui fournir les paramètres appropriés hello. Vous devez cela un toodo compte Google +. Si vous n’en avez pas, vous pouvez en obtenir un à l’adresse [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).

1. Accédez toohello [Console des développeurs Google](https://console.developers.google.com/) et connectez-vous avec vos informations d’identification compte Google +.
2. Cliquez sur **Créer un projet**, saisissez un **nom de projet**, puis cliquez sur **Créer**.
   
    ![Google+ - Prise en main](./media/active-directory-b2c-setup-goog-app/google-get-started.png)
   
    ![Google+ - Nouveau projet](./media/active-directory-b2c-setup-goog-app/google-new-project.png)
3. Cliquez sur **API Manager** puis cliquez sur **informations d’identification** Bonjour barre de navigation gauche.
4. Cliquez sur hello **écran de consentement OAuth** onglet en haut de hello.
   
    ![Google+ - Informations d’identification](./media/active-directory-b2c-setup-goog-app/google-add-cred.png)
5. Sélectionnez ou spécifiez une valeur valide pour **Adresse de messagerie**, fournissez une valeur pour **Nom de produit**, puis cliquez sur **Enregistrer**.
   
    ![Google+ - Écran de consentement OAuth](./media/active-directory-b2c-setup-goog-app/google-consent-screen.png)
6. Cliquez sur **Nouvelles informations d’identification**, puis sur **ID client OAuth**.
   
    ![Google+ - Écran de consentement OAuth](./media/active-directory-b2c-setup-goog-app/google-add-oauth2-client-id.png)
7. Sous **Type d’application**, sélectionnez **Application web**.
   
    ![Google+ - Écran de consentement OAuth](./media/active-directory-b2c-setup-goog-app/google-web-app.png)
8. Fournir un **nom** pour votre application, entrez `https://login.microsoftonline.com` Bonjour **autorisé de JavaScript origines** champ, et `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` Bonjour **autorisés rediriger URI**champ. Remplacez **{tenant}** par votre nom de client (par exemple, contosob2c.onmicrosoft.com). Hello **{tenant}** valeur respecte la casse. Cliquez sur **Créer**.
   
    ![Google+ - Créer un identifiant client](./media/active-directory-b2c-setup-goog-app/google-create-client-id.png)
9. Copier les valeurs hello de **ID Client** et **clé secrète Client**. Vous devez les deux tooconfigure Google + en tant que fournisseur d’identité dans votre client. **Client secret** est une information d’identification de sécurité importante.
   
    ![Google+ - Clé secrète client](./media/active-directory-b2c-setup-goog-app/google-client-secret.png)

## <a name="configure-google-as-an-identity-provider-in-your-tenant"></a>Configuration de Google+ en tant que fournisseur d'identité dans votre client
1. Suivez ces étapes trop[accédez Panneau de fonctionnalités toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) sur hello portail Azure.
2. Dans le panneau de fonctionnalités hello B2C, cliquez sur **fournisseurs d’identité**.
3. Cliquez sur **+ ajouter** haut hello du Panneau de hello.
4. Fournissez un nom convivial de **nom** pour la configuration du fournisseur d’identité hello. Par exemple, entrez « G+ ».
5. Cliquez sur **Type de fournisseur d’identité**, sélectionnez **Google**, puis cliquez sur **OK**.
6. Cliquez sur **configurer ce fournisseur d’identité** et entrez hello client et ID de clé secrète client de hello application Google + que vous avez créé précédemment.
7. Cliquez sur **OK** puis cliquez sur **créer** toosave votre configuration de Google +.

