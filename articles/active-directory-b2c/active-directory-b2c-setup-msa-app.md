---
title: 'Azure Active Directory B2C : configuration de compte Microsoft | Microsoft Docs'
description: "Fournir tooconsumers d’abonnement et connectez-vous avec les comptes Microsoft dans vos applications sont sécurisées par Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 06407322-142c-4cb3-9106-a8d752c4c853
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: bec4777f003c459030f68c35b24f0e4bcddf84ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-microsoft-accounts"></a>Azure B2C Active Directory : Fournir tooconsumers d’abonnement et connectez-vous avec les comptes Microsoft
## <a name="create-a-microsoft-account-application"></a>Créer une application de compte Microsoft
toouse de compte Microsoft en tant que fournisseur d’identité dans Azure Active Directory (Azure AD) B2C, vous devez toocreate une application de compte Microsoft et lui fournir les paramètres appropriés hello. Vous devez cela un toodo de compte Microsoft. Si vous n’en avez pas, vous pouvez en obtenir un à l’adresse [https://www.live.com/](https://www.live.com/).

1. Accédez toohello [portail de l’enregistrement d’Application Microsoft](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) et connectez-vous avec vos informations d’identification du compte Microsoft.
2. Cliquez sur **Ajouter une application**.
   
    ![Compte Microsoft - Ajouter une nouvelle application](./media/active-directory-b2c-setup-msa-app/msa-add-new-app.png)
3. Indiquez un **nom** pour votre application et cliquez sur **Créer une application**.
   
    ![Compte Microsoft - Nom d’application](./media/active-directory-b2c-setup-msa-app/msa-app-name.png)
4. Copiez la valeur hello **Id de l’Application**. Vous en aurez besoin tooconfigure compte Microsoft en tant que fournisseur d’identité dans votre client.
   
    ![Compte Microsoft - ID de l’application](./media/active-directory-b2c-setup-msa-app/msa-app-id.png)
5. Cliquez sur **Ajouter une plateforme** et choisissez **Web**.
   
    ![Compte Microsoft - Ajouter une plateforme](./media/active-directory-b2c-setup-msa-app/msa-add-platform.png)
   
    ![Compte Microsoft - Web](./media/active-directory-b2c-setup-msa-app/msa-web.png)
6. Entrez `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` Bonjour **URI de redirection** champ. Remplacez **{tenant}** par votre nom de client (par exemple, contosob2c.onmicrosoft.com).
   
    ![Compte Microsoft - URL de redirection](./media/active-directory-b2c-setup-msa-app/msa-redirect-url.png)
7. Cliquez sur **générer un nouveau mot de passe** sous hello **Application Secrets** section. Copiez le nouveau mot de passe hello affiché sur l’écran. Vous en aurez besoin tooconfigure compte Microsoft en tant que fournisseur d’identité dans votre client. Ce mot de passe est une information d’identification de sécurité importante.
   
    ![Compte Microsoft - générer un nouveau mot de passe](./media/active-directory-b2c-setup-msa-app/msa-generate-new-password.png)
   
    ![Compte Microsoft - Nouveau mot de passe](./media/active-directory-b2c-setup-msa-app/msa-new-password.png)
8. Case à cocher hello indiquant **prise en charge du Kit de développement logiciel Live** sous hello **Options avancées** section. Cliquez sur **Enregistrer**.
   
    ![Compte Microsoft - Support du Kit SDK Live](./media/active-directory-b2c-setup-msa-app/msa-live-sdk-support.png)

## <a name="configure-microsoft-account-as-an-identity-provider-in-your-tenant"></a>Configuration du compte Microsoft en tant que fournisseur d’identité dans votre client
1. Suivez ces étapes trop[accédez Panneau de fonctionnalités toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) sur hello portail Azure.
2. Dans le panneau de fonctionnalités hello B2C, cliquez sur **fournisseurs d’identité**.
3. Cliquez sur **+ ajouter** haut hello du Panneau de hello.
4. Fournissez un nom convivial de **nom** pour la configuration du fournisseur d’identité hello. Par exemple, saisissez « MSA ».
5. Cliquez sur **Type de fournisseur d’identité**, sélectionnez **Compte Microsoft**, puis cliquez sur **OK**.
6. Cliquez sur **configurer ce fournisseur d’identité** et entrez hello Id d’Application et mot de passe de hello application de compte Microsoft que vous avez créé précédemment.
7. Cliquez sur **OK** puis cliquez sur **créer** toosave configuration de compte Microsoft.

