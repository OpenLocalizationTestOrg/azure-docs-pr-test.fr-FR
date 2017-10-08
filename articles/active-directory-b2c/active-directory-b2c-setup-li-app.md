---
title: 'Azure Active Directory B2C : configuration LinkedIn | Microsoft Docs'
description: "Fournir tooconsumers d’abonnement et connectez-vous avec les comptes LinkedIn dans vos applications sont sécurisées par Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: fa51a16b-9ce9-4e27-9eff-0869b4c4f0ef
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 6c5233ef48b24968fd6383f470b5d8a969a78ecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-linkedin-accounts"></a>Azure B2C Active Directory : Fournir LinkedIn comptes tooconsumers d’inscription et de connexion
## <a name="create-a-linkedin-application"></a>Création d’une application LinkedIn
toouse LinkedIn comme fournisseur d’identité dans Azure Active Directory (Azure AD) B2C, vous devez toocreate une application LinkedIn et lui fournir les paramètres appropriés hello. Vous devez cela un toodo de compte LinkedIn. Si vous n’en avez pas, vous pouvez en obtenir un à l’adresse [https://www.linkedin.com/](https://www.linkedin.com/).

1. Accédez toohello [site Web des développeurs de LinkedIn](https://www.developer.linkedin.com/) et connectez-vous avec vos informations d’identification du compte LinkedIn.
2. Cliquez sur **mes applications** dans hello barre de menus supérieure, puis cliquez sur **créer une Application**.
   
    ![LinkedIn - nouvelle application](./media/active-directory-b2c-setup-li-app/linkedin-new-app.png)
3. Bonjour **créer une nouvelle Application** forment, renseignez les informations pertinentes hello (**nom de la société**, **nom**, **Description**, **URL Logo de l’application**, **utilisation de l’Application**, **URL du site Web**, **E-mail professionnelles** et **téléphone(bureau)**).
4. Acceptez toohello **LinkedIn API conditions d’utilisation** et cliquez sur **Submit**.
   
    ![LinkedIn - inscription d’application](./media/active-directory-b2c-setup-li-app/linkedin-register-app.png)
5. Copier les valeurs hello de **ID Client** et **clé secrète Client**. (Vous les trouverez sous **Clés d’authentification**.) Vous devez les deux tooconfigure LinkedIn comme fournisseur d’identité dans votre client.
   
   > [!NOTE]
   > **Client Secret** est une information d’identification de sécurité importante.
   > 
   > 
6. Entrez `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` Bonjour **URL de redirection autorisés** champ (sous **OAuth 2.0**). Remplacez **{tenant}** par votre nom de client (par exemple, contoso.onmicrosoft.com). Cliquez sur **Ajouter**, puis sur **Mettre à jour**. Hello **{tenant}** valeur respecte la casse.
   
    ![LinkedIn - configuration d’application](./media/active-directory-b2c-setup-li-app/linkedin-setup.png)

## <a name="configure-linkedin-as-an-identity-provider-in-your-tenant"></a>Configuration de LinkedIn en tant que fournisseur d’identité dans votre client
1. Suivez ces étapes trop[accédez Panneau de fonctionnalités toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) sur hello portail Azure.
2. Dans le panneau de fonctionnalités hello B2C, cliquez sur **fournisseurs d’identité**.
3. Cliquez sur **+ ajouter** haut hello du Panneau de hello.
4. Fournissez un nom convivial de **nom** pour la configuration du fournisseur d’identité hello. Par exemple, entrez « LI ».
5. Cliquez sur **Type de fournisseur d’identité**, sélectionnez **LinkedIn**, puis cliquez sur **OK**.
6. Cliquez sur **configurer ce fournisseur d’identité** et entrez hello client et ID de clé secrète client de hello LinkedIn application que vous avez créé précédemment.
7. Cliquez sur **OK** puis cliquez sur **créer** toosave votre configuration LinkedIn.

