---
title: 'Azure Active Directory B2C : configuration Amazon | Microsoft Docs'
description: "Fournir tooconsumers d’abonnement et connectez-vous avec des comptes d’Amazon dans vos applications sont sécurisées par Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 77c099bb-a005-4d75-87f9-f61e3de48725
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 60d7c4b76d9d3e86ed535765329abed07f1e5996
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-amazon-accounts"></a>Azure B2C Active Directory : Fournir tooconsumers d’abonnement et connectez-vous avec les comptes d’Amazon
## <a name="create-an-amazon-application"></a>Création d’une application Amazon
toouse Amazon comme fournisseur d’identité dans Azure Active Directory (Azure AD) B2C, vous devez toocreate une application Amazon et lui fournir les paramètres appropriés hello. Vous devez une toodo de compte Amazon cela. Si vous n’en avez pas, vous pouvez en obtenir un à l’adresse [http://www.amazon.com/](http://www.amazon.com/).

1. Accédez toohello [Centre pour développeurs Amazon](https://login.amazon.com/) et connectez-vous avec vos informations d’identification du compte Amazon.
2. Si vous ne le n'avez pas déjà fait, cliquez sur **s’inscrire**, suivez les étapes d’inscription de développeur hello et acceptez la politique de hello.
3. Cliquez sur **Register new application**.
   
    ![L’inscription d’une nouvelle application sur le site Web de hello Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-new-app.png)
4. Fournissez les informations relatives à l’application (**Nom**, **Description** et **Privacy Notice URL** (URL de déclaration de confidentialité), puis cliquez sur **Enregistrer**.
   
    ![Fourniture d’informations d’application pour l’inscription d’une nouvelle application sur Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-register-app.png)
5. Bonjour **paramètres Web** section, copie les valeurs hello de **ID Client** et **clé secrète Client**. (Vous devez tooclick hello **afficher le Secret** bouton toosee ce.) Vous avez besoin des deux d'entre eux tooconfigure Amazon comme fournisseur d’identité dans votre client. Cliquez sur **modifier** bas hello de section de hello. **Client Secret** est une information d’identification de sécurité importante.
   
    ![Fourniture de l’ID client et de la clé secrète client pour votre nouvelle application sur Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-client-secret.png)
6. Entrez `https://login.microsoftonline.com` Bonjour **autorisé les origines JavaScript** champ et `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` Bonjour **autorisé les URL de retour** champ. Remplacez **{tenant}** par votre nom de client (par exemple, contoso.onmicrosoft.com). Cliquez sur **Enregistrer**. Hello **{tenant}** valeur respecte la casse.
   
    ![Fourniture de JavaScript Origins et Return URLs pour votre nouvelle application sur Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-urls.png)

## <a name="configure-amazon-as-an-identity-provider-in-your-tenant"></a>Configuration d’Amazon en tant que fournisseur d’identité dans votre client
1. Suivez ces étapes trop[accédez Panneau de fonctionnalités toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) sur hello portail Azure.
2. Dans le panneau de fonctionnalités hello B2C, cliquez sur **fournisseurs d’identité**.
3. Cliquez sur **+ ajouter** haut hello du Panneau de hello.
4. Fournissez un nom convivial de **nom** pour la configuration du fournisseur d’identité hello. Par exemple, entrez « Amzn ».
5. Cliquez sur **Type de fournisseur d’identité**, sélectionnez **Amazon**, puis cliquez sur **OK**.
6. Cliquez sur **configurer ce fournisseur d’identité** et entrez hello client et ID de clé secrète client de hello application Amazon que vous avez créé précédemment.
7. Cliquez sur **OK** puis cliquez sur **créer** toosave votre configuration Amazon.

