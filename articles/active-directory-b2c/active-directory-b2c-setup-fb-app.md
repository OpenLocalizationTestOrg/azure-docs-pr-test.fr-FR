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
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-facebook-accounts"></a><span data-ttu-id="7e993-103">Azure Active Directory B2C : fourniture d’inscription et de connexion à des consommateurs disposant de comptes Facebook</span><span class="sxs-lookup"><span data-stu-id="7e993-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Facebook accounts</span></span>
## <a name="create-a-facebook-application"></a><span data-ttu-id="7e993-104">Création d’une application Facebook</span><span class="sxs-lookup"><span data-stu-id="7e993-104">Create a Facebook application</span></span>
<span data-ttu-id="7e993-105">Pour utiliser Facebook en tant que fournisseur d’identité dans Azure Active Directory (Azure AD) B2C, vous devez créer une application Facebook et lui fournir les paramètres appropriés.</span><span class="sxs-lookup"><span data-stu-id="7e993-105">To use Facebook as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Facebook application and supply it with the right parameters.</span></span> <span data-ttu-id="7e993-106">Pour ce faire, vous avez besoin d’un compte Facebook.</span><span class="sxs-lookup"><span data-stu-id="7e993-106">You need a Facebook account to do this.</span></span> <span data-ttu-id="7e993-107">Si vous n’en avez pas, vous pouvez en obtenir un à l’adresse [https://www.facebook.com/](https://www.facebook.com/).</span><span class="sxs-lookup"><span data-stu-id="7e993-107">If you don’t have one, you can get it at [https://www.facebook.com/](https://www.facebook.com/).</span></span>

1. <span data-ttu-id="7e993-108">Accédez au site web [Facebook pour les développeurs](https://developers.facebook.com/) et connectez-vous à l’aide des informations d’identification de votre compte Facebook.</span><span class="sxs-lookup"><span data-stu-id="7e993-108">Go to the [Facebook for developers](https://developers.facebook.com/) website and sign in with your Facebook account credentials.</span></span>
2. <span data-ttu-id="7e993-109">Si ce n’est pas déjà fait, vous devez vous inscrire en tant que développeur Facebook.</span><span class="sxs-lookup"><span data-stu-id="7e993-109">If you have not already done so, you need to register as a Facebook developer.</span></span> <span data-ttu-id="7e993-110">Pour cela, cliquez sur **Register** (dans le coin supérieur droit de la page), acceptez les politiques de Facebook et suivez les étapes de l’inscription.</span><span class="sxs-lookup"><span data-stu-id="7e993-110">To do this, click **Register** (on the upper-right corner of the page), accept Facebook's policies, and complete the registration steps.</span></span>
3. <span data-ttu-id="7e993-111">Cliquez sur **Mes applications**, puis sur **Ajouter une nouvelle application**.</span><span class="sxs-lookup"><span data-stu-id="7e993-111">Click **My Apps** and then click **Add a New App**.</span></span> 
4. <span data-ttu-id="7e993-112">Dans le formulaire, indiquez un **nom d’affichage** et une **adresse e-mail de contact** valide.</span><span class="sxs-lookup"><span data-stu-id="7e993-112">In the form, provide a **Display Name** and a valid **Contact Email**.</span></span>
5. <span data-ttu-id="7e993-113">Cliquez sur **Créer l’ID d’application**.</span><span class="sxs-lookup"><span data-stu-id="7e993-113">Click **Create App ID**.</span></span> <span data-ttu-id="7e993-114">Vous devrez peut-être accepter les politiques de la plateforme Facebook et effectuer une vérification de sécurité en ligne.</span><span class="sxs-lookup"><span data-stu-id="7e993-114">This may require you to accept Facebook platform policies and complete an online security check.</span></span>
6. <span data-ttu-id="7e993-115">Dans la colonne de gauche, cliquez sur **Paramètres** , puis sélectionnez **De base** si cette option n’est pas déjà sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="7e993-115">In the left column, click **Settings** and then select **Basic** if not selected already.</span></span>
7. <span data-ttu-id="7e993-116">Sélectionnez une **catégorie**.</span><span class="sxs-lookup"><span data-stu-id="7e993-116">Select a **Category**.</span></span> 
8. <span data-ttu-id="7e993-117">Cliquez sur **+ Ajouter une plateforme**, puis sélectionnez **Site web**.</span><span class="sxs-lookup"><span data-stu-id="7e993-117">Click **+ Add Platform** and select **Website**.</span></span>
   
    ![Facebook - paramètres](./media/active-directory-b2c-setup-fb-app/fb-settings.png)
   
    ![Facebook - paramètres - site Web](./media/active-directory-b2c-setup-fb-app/fb-website.png)
9. <span data-ttu-id="7e993-120">Entrez `https://login.microsoftonline.com/` dans le champ **URL du site**, puis cliquez sur **Enregistrer les modifications** en bas de la page.</span><span class="sxs-lookup"><span data-stu-id="7e993-120">Enter `https://login.microsoftonline.com/` in the **Site URL** field and then click **Save Changes** at the bottom of the page.</span></span>
   
    ![Facebook - URL du site](./media/active-directory-b2c-setup-fb-app/fb-site-url.png)

10. <span data-ttu-id="7e993-122">Copiez la valeur **ID de l’application**.</span><span class="sxs-lookup"><span data-stu-id="7e993-122">Copy the value of **App ID**.</span></span> <span data-ttu-id="7e993-123">Cliquez sur **Afficher**, puis copiez la valeur **Clé secrète de l’application**.</span><span class="sxs-lookup"><span data-stu-id="7e993-123">Click **Show** and copy the value of **App Secret**.</span></span> <span data-ttu-id="7e993-124">Vous aurez besoin de ces deux valeurs pour configurer Facebook en tant que fournisseur d’identité dans votre client.</span><span class="sxs-lookup"><span data-stu-id="7e993-124">You will need both of them to configure Facebook as an identity provider in your tenant.</span></span> <span data-ttu-id="7e993-125">**App Secret** est une information d’identification de sécurité importante.</span><span class="sxs-lookup"><span data-stu-id="7e993-125">**App Secret** is an important security credential.</span></span>
   
    ![Facebook - ID et clé secrète de l’application](./media/active-directory-b2c-setup-fb-app/fb-app-id-app-secret.png)
11. <span data-ttu-id="7e993-127">Cliquez sur **+ Ajouter un produit** dans la barre de navigation gauche, puis sur le bouton **Set up** (Configurer) de **Connexion Facebook**.</span><span class="sxs-lookup"><span data-stu-id="7e993-127">Click **+ Add Product** on the left navigation and then the **Set Up** button for **Facebook Login**.</span></span>
   
    ![Facebook - Connexion Facebook](./media/active-directory-b2c-setup-fb-app/fb-login.png)
12. <span data-ttu-id="7e993-129">Cliquer sur **Paramètres** dans la barre de navigation droite sous **Connexion Facebook**</span><span class="sxs-lookup"><span data-stu-id="7e993-129">Click **Settings** on the right nav under **Facebook Login**</span></span>

    ![Facebook - Paramètres Connexion Facebook](./media/active-directory-b2c-setup-fb-app/fb-login-settings.png)
13. <span data-ttu-id="7e993-131">Entrez `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` dans le champ **URI de redirection OAuth valides** dans la section **Paramètres du client OAuth**.</span><span class="sxs-lookup"><span data-stu-id="7e993-131">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Valid OAuth redirect URIs** field in the **Client OAuth Settings** section.</span></span> <span data-ttu-id="7e993-132">Remplacez **{tenant}** par votre nom de client (par exemple, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="7e993-132">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="7e993-133">Cliquez sur **Save Changes** en bas de la page.</span><span class="sxs-lookup"><span data-stu-id="7e993-133">Click **Save Changes** at the bottom of the page.</span></span>
    
    ![Facebook - OAuth Redirect URI](./media/active-directory-b2c-setup-fb-app/fb-oauth-redirect-uri.png)
14. <span data-ttu-id="7e993-135">Pour rendre votre application Facebook utilisable par Azure AD B2C, vous devez la rendre disponible publiquement.</span><span class="sxs-lookup"><span data-stu-id="7e993-135">To make your Facebook application usable by Azure AD B2C, you need to make it publicly available.</span></span> <span data-ttu-id="7e993-136">Vous pouvez le faire en cliquant sur **Révision de l’application** dans le volet de navigation gauche, en positionnant le commutateur en haut de la page sur **OUI** et en cliquant sur **Confirmer**.</span><span class="sxs-lookup"><span data-stu-id="7e993-136">You can do this by clicking **App Review** on the left navigation and by turning the switch at the top of the page to **YES** and clicking **Confirm**.</span></span>
    
    ![Facebook - App publique](./media/active-directory-b2c-setup-fb-app/fb-app-public.png)

## <a name="configure-facebook-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="7e993-138">Configuration de Facebook en tant que fournisseur d’identité dans votre client</span><span class="sxs-lookup"><span data-stu-id="7e993-138">Configure Facebook as an identity provider in your tenant</span></span>
1. <span data-ttu-id="7e993-139">Suivez ces étapes pour [accéder au panneau de fonctionnalités B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="7e993-139">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="7e993-140">Dans le panneau de fonctionnalités B2C, cliquez sur **Fournisseurs d’identité**.</span><span class="sxs-lookup"><span data-stu-id="7e993-140">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="7e993-141">Cliquez sur **+Ajouter** dans la partie supérieure du panneau.</span><span class="sxs-lookup"><span data-stu-id="7e993-141">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="7e993-142">Fournissez un **Nom** convivial pour la configuration de fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="7e993-142">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="7e993-143">Par exemple, entrez « Facebook ».</span><span class="sxs-lookup"><span data-stu-id="7e993-143">For example, enter "Facebook".</span></span>
5. <span data-ttu-id="7e993-144">Cliquez sur **Type de fournisseur d’identité**, sélectionnez **Facebook**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="7e993-144">Click **Identity provider type**, select **Facebook**, and click **OK**.</span></span>
6. <span data-ttu-id="7e993-145">Cliquez sur **Configurer ce fournisseur d’identité**, puis entrez l’ID de l’application et la question secrète (de l’application Facebook que vous avez créée précédemment) respectivement dans les champs **ID client** et **Clé secrète client**.</span><span class="sxs-lookup"><span data-stu-id="7e993-145">Click **Set up this identity provider** and enter the app ID and app secret (of the Facebook application that you created earlier) in the **Client ID** and **Client secret** fields respectively.</span></span>
7. <span data-ttu-id="7e993-146">Cliquez sur **OK**, puis sur **Créer** pour enregistrer votre configuration Facebook.</span><span class="sxs-lookup"><span data-stu-id="7e993-146">Click **OK**, and then click **Create** to save your Facebook configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="7e993-147">L’ajout d’un **fournisseur d’identité** à votre locataire ne modifie pas vos stratégies existantes.</span><span class="sxs-lookup"><span data-stu-id="7e993-147">Adding an **Identity provider** to your tenant does not modify your existing policies.</span></span> <span data-ttu-id="7e993-148">Rappelez-vous de mettre à jour vos stratégies en incluant le fournisseur d’identité que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="7e993-148">Remember to update your policies by including the identity provider you just created.</span></span>
>