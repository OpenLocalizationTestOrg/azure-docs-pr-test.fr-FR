---
title: 'Azure Active Directory B2C : configuration Facebook | Microsoft Docs'
description: "Fournir tooconsumers d’inscription et de connexion à des comptes de Facebook dans vos applications qui sont sécurisées par Azure Active Directory B2C."
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
ms.openlocfilehash: 4c3b79c7248bd1e789bf33fc467abb27d0170edd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-facebook-accounts"></a>Azure B2C Active Directory : Fournir tooconsumers d’abonnement et connectez-vous avec les comptes de Facebook
## <a name="create-a-facebook-application"></a>Création d’une application Facebook
toouse Facebook comme fournisseur d’identité dans Azure Active Directory (Azure AD) B2C, vous devez toocreate une application Facebook et lui fournir les paramètres appropriés hello. Vous devez cela un toodo de compte Facebook. Si vous n’en avez pas, vous pouvez en obtenir un à l’adresse [https://www.facebook.com/](https://www.facebook.com/).

1. Accédez toohello [Facebook pour les développeurs](https://developers.facebook.com/) site Web et connectez-vous avec votre Facebook des informations d’identification de compte.
2. Si vous ne le n'avez pas déjà fait, vous devez tooregister en tant qu’un développeur de Facebook. toodo, cliquez sur **inscrire** (sur hello haut à droite de la page de hello), accepter les stratégies de Facebook et effectuez les étapes de l’inscription hello.
3. Cliquez sur **Mes applications**, puis sur **Ajouter une nouvelle application**. 
4. Dans le formulaire de hello, fournissez un **nom d’affichage** et valide **messagerie du Contact**.
5. Cliquez sur **Créer l’ID d’application**. Cela peut vous nécessitent des stratégies de plateforme Facebook tooaccept et effectuer une vérification de sécurité en ligne.
6. Dans la colonne de gauche hello, cliquez sur **paramètres** , puis sélectionnez **base** si ne pas déjà sélectionné.
7. Sélectionnez une **catégorie**. 
8. Cliquez sur **+ Ajouter une plateforme**, puis sélectionnez **Site web**.
   
    ![Facebook - paramètres](./media/active-directory-b2c-setup-fb-app/fb-settings.png)
   
    ![Facebook - paramètres - site Web](./media/active-directory-b2c-setup-fb-app/fb-website.png)
9. Entrez `https://login.microsoftonline.com/` Bonjour **URL du Site** champ, puis cliquez sur **enregistrer les modifications** bas hello de page de hello.
   
    ![Facebook - URL du site](./media/active-directory-b2c-setup-fb-app/fb-site-url.png)

10. Copiez la valeur hello **ID d’application**. Cliquez sur **afficher** et copiez la valeur hello **Secret d’application**. Vous devez les deux tooconfigure Facebook comme fournisseur d’identité dans votre client. **App Secret** est une information d’identification de sécurité importante.
   
    ![Facebook - ID et clé secrète de l’application](./media/active-directory-b2c-setup-fb-app/fb-app-id-app-secret.png)
11. Cliquez sur **+ ajouter un produit** hello de navigation de gauche et puis hello **Set Up** bouton **connexion Facebook**.
   
    ![Facebook - Connexion Facebook](./media/active-directory-b2c-setup-fb-app/fb-login.png)
12. Cliquez sur **paramètres** sur nav de droite hello sous **connexion Facebook**

    ![Facebook - Paramètres Connexion Facebook](./media/active-directory-b2c-setup-fb-app/fb-login-settings.png)
13. Entrez `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` Bonjour **URI de redirection OAuth valide** champ hello **les paramètres Client OAuth** section. Remplacez **{tenant}** par votre nom de client (par exemple, contosob2c.onmicrosoft.com). Cliquez sur **enregistrer les modifications** bas hello de page de hello.
    
    ![Facebook - OAuth Redirect URI](./media/active-directory-b2c-setup-fb-app/fb-oauth-redirect-uri.png)
14. toomake votre application Facebook utilisable par Azure AD B2C, vous devez toomake publiquement disponibles. Vous pouvez le faire en cliquant sur **révision d’application** basculer sur hello barre de navigation gauche et en activant le hello en hello haut hello trop**Oui** et en cliquant sur **confirmer**.
    
    ![Facebook - App publique](./media/active-directory-b2c-setup-fb-app/fb-app-public.png)

## <a name="configure-facebook-as-an-identity-provider-in-your-tenant"></a>Configuration de Facebook en tant que fournisseur d’identité dans votre client
1. Suivez ces étapes trop[accédez Panneau de fonctionnalités toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) sur hello portail Azure.
2. Dans le panneau de fonctionnalités hello B2C, cliquez sur **fournisseurs d’identité**.
3. Cliquez sur **+ ajouter** haut hello du Panneau de hello.
4. Fournissez un nom convivial de **nom** pour la configuration du fournisseur d’identité hello. Par exemple, entrez « Facebook ».
5. Cliquez sur **Type de fournisseur d’identité**, sélectionnez **Facebook**, puis cliquez sur **OK**.
6. Cliquez sur **configurer ce fournisseur d’identité** et entrez hello application et le code secret d’application (de hello application Facebook que vous avez créé précédemment) Bonjour **ID Client** et **question secrète du Client**champs respectivement.
7. Cliquez sur **OK**, puis cliquez sur **créer** toosave votre configuration de Facebook.

> [!NOTE]
> Ajout d’un **fournisseur d’identité** tooyour client ne modifie pas vos stratégies existantes. N’oubliez pas tooupdate vos stratégies en incluant le fournisseur d’identité hello que vous venez de créer.
>