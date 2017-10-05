---
title: 'Azure Active Directory B2C : configuration Facebook | Microsoft Docs'
description: "Fourniture d’inscription et de connexion à des consommateurs disposant de comptes Facebook dans vos applications sécurisées par Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: sromeroz
manager: krassk
editor: sromeroz
ms.assetid: b875f235-a1d2-4abb-b9f0-b89beac38a32
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/7/2017
ms.author: sromeroz
ms.openlocfilehash: 8c2154fcf33537358b549395d15b4ba937371cd0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-facebook-accounts"></a>Azure Active Directory B2C : fourniture d’inscription et de connexion à des consommateurs disposant de comptes Facebook
## <a name="create-a-facebook-application"></a>Création d’une application Facebook
Pour utiliser Facebook en tant que fournisseur d’identité dans Azure Active Directory (Azure AD) B2C, vous devez créer une application Facebook et lui fournir les paramètres appropriés. Pour ce faire, vous avez besoin d’un compte Facebook. Si vous n’en avez pas, vous pouvez en obtenir un à l’adresse [https://www.facebook.com/](https://www.facebook.com/).

1. Accédez au site web [Facebook pour les développeurs](https://developers.facebook.com/) et connectez-vous à l’aide des informations d’identification de votre compte Facebook.
2. Si ce n’est pas déjà fait, vous devez vous inscrire en tant que développeur Facebook. Pour cela, cliquez sur **Register** (dans le coin supérieur droit de la page), acceptez les politiques de Facebook et suivez les étapes de l’inscription.
3. Cliquez sur **Mes applications**, puis sur **Ajouter une nouvelle application**. 
4. Dans le formulaire, indiquez un **nom d’affichage** et une **adresse e-mail de contact** valide.
5. Cliquez sur **Créer l’ID d’application**. Vous devrez peut-être accepter les politiques de la plateforme Facebook et effectuer une vérification de sécurité en ligne.
6. Dans la colonne de gauche, cliquez sur **Paramètres** , puis sélectionnez **De base** si cette option n’est pas déjà sélectionnée.
7. Sélectionnez une **catégorie**. 
8. Cliquez sur **+ Ajouter une plateforme**, puis sélectionnez **Site web**.
   
    ![Facebook - paramètres](./media/active-directory-b2c-setup-fb-app/fb-settings.png)
   
    ![Facebook - paramètres - site Web](./media/active-directory-b2c-setup-fb-app/fb-website.png)
9. Entrez `https://login.microsoftonline.com/` dans le champ **URL du site**, puis cliquez sur **Enregistrer les modifications** en bas de la page.
   
    ![Facebook - URL du site](./media/active-directory-b2c-setup-fb-app/fb-site-url.png)

10. Copiez la valeur **ID de l’application**. Cliquez sur **Afficher**, puis copiez la valeur **Clé secrète de l’application**. Vous aurez besoin de ces deux valeurs pour configurer Facebook en tant que fournisseur d’identité dans votre client. **App Secret** est une information d’identification de sécurité importante.
   
    ![Facebook - ID et clé secrète de l’application](./media/active-directory-b2c-setup-fb-app/fb-app-id-app-secret.png)
11. Cliquez sur **+ Ajouter un produit** dans la barre de navigation gauche, puis sur le bouton **Set up** (Configurer) de **Connexion Facebook**.
   
    ![Facebook - Connexion Facebook](./media/active-directory-b2c-setup-fb-app/fb-login.png)
12. Cliquer sur **Paramètres** dans la barre de navigation droite sous **Connexion Facebook**

    ![Facebook - Paramètres Connexion Facebook](./media/active-directory-b2c-setup-fb-app/fb-login-settings.png)
13. Entrez `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` dans le champ **URI de redirection OAuth valides** dans la section **Paramètres du client OAuth**. Remplacez **{tenant}** par votre nom de client (par exemple, contosob2c.onmicrosoft.com). Cliquez sur **Save Changes** en bas de la page.
    
    ![Facebook - OAuth Redirect URI](./media/active-directory-b2c-setup-fb-app/fb-oauth-redirect-uri.png)
14. Pour rendre votre application Facebook utilisable par Azure AD B2C, vous devez la rendre disponible publiquement. Vous pouvez le faire en cliquant sur **Révision de l’application** dans le volet de navigation gauche, en positionnant le commutateur en haut de la page sur **OUI** et en cliquant sur **Confirmer**.
    
    ![Facebook - App publique](./media/active-directory-b2c-setup-fb-app/fb-app-public.png)

## <a name="configure-facebook-as-an-identity-provider-in-your-tenant"></a>Configuration de Facebook en tant que fournisseur d’identité dans votre client
1. Suivez ces étapes pour [accéder au panneau de fonctionnalités B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) sur le portail Azure.
2. Dans le panneau de fonctionnalités B2C, cliquez sur **Fournisseurs d’identité**.
3. Cliquez sur **+Ajouter** dans la partie supérieure du panneau.
4. Fournissez un **Nom** convivial pour la configuration de fournisseur d’identité. Par exemple, entrez « Facebook ».
5. Cliquez sur **Type de fournisseur d’identité**, sélectionnez **Facebook**, puis cliquez sur **OK**.
6. Cliquez sur **Configurer ce fournisseur d’identité**, puis entrez l’ID de l’application et la question secrète (de l’application Facebook que vous avez créée précédemment) respectivement dans les champs **ID client** et **Clé secrète client**.
7. Cliquez sur **OK**, puis sur **Créer** pour enregistrer votre configuration Facebook.

> [!NOTE]
> L’ajout d’un **fournisseur d’identité** à votre locataire ne modifie pas vos stratégies existantes. Rappelez-vous de mettre à jour vos stratégies en incluant le fournisseur d’identité que vous venez de créer.
>