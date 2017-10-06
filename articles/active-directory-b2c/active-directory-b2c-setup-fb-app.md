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
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-facebook-accounts"></a><span data-ttu-id="d20d9-103">Azure B2C Active Directory : Fournir tooconsumers d’abonnement et connectez-vous avec les comptes de Facebook</span><span class="sxs-lookup"><span data-stu-id="d20d9-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Facebook accounts</span></span>
## <a name="create-a-facebook-application"></a><span data-ttu-id="d20d9-104">Création d’une application Facebook</span><span class="sxs-lookup"><span data-stu-id="d20d9-104">Create a Facebook application</span></span>
<span data-ttu-id="d20d9-105">toouse Facebook comme fournisseur d’identité dans Azure Active Directory (Azure AD) B2C, vous devez toocreate une application Facebook et lui fournir les paramètres appropriés hello.</span><span class="sxs-lookup"><span data-stu-id="d20d9-105">toouse Facebook as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Facebook application and supply it with hello right parameters.</span></span> <span data-ttu-id="d20d9-106">Vous devez cela un toodo de compte Facebook.</span><span class="sxs-lookup"><span data-stu-id="d20d9-106">You need a Facebook account toodo this.</span></span> <span data-ttu-id="d20d9-107">Si vous n’en avez pas, vous pouvez en obtenir un à l’adresse [https://www.facebook.com/](https://www.facebook.com/).</span><span class="sxs-lookup"><span data-stu-id="d20d9-107">If you don’t have one, you can get it at [https://www.facebook.com/](https://www.facebook.com/).</span></span>

1. <span data-ttu-id="d20d9-108">Accédez toohello [Facebook pour les développeurs](https://developers.facebook.com/) site Web et connectez-vous avec votre Facebook des informations d’identification de compte.</span><span class="sxs-lookup"><span data-stu-id="d20d9-108">Go toohello [Facebook for developers](https://developers.facebook.com/) website and sign in with your Facebook account credentials.</span></span>
2. <span data-ttu-id="d20d9-109">Si vous ne le n'avez pas déjà fait, vous devez tooregister en tant qu’un développeur de Facebook.</span><span class="sxs-lookup"><span data-stu-id="d20d9-109">If you have not already done so, you need tooregister as a Facebook developer.</span></span> <span data-ttu-id="d20d9-110">toodo, cliquez sur **inscrire** (sur hello haut à droite de la page de hello), accepter les stratégies de Facebook et effectuez les étapes de l’inscription hello.</span><span class="sxs-lookup"><span data-stu-id="d20d9-110">toodo this, click **Register** (on hello upper-right corner of hello page), accept Facebook's policies, and complete hello registration steps.</span></span>
3. <span data-ttu-id="d20d9-111">Cliquez sur **Mes applications**, puis sur **Ajouter une nouvelle application**.</span><span class="sxs-lookup"><span data-stu-id="d20d9-111">Click **My Apps** and then click **Add a New App**.</span></span> 
4. <span data-ttu-id="d20d9-112">Dans le formulaire de hello, fournissez un **nom d’affichage** et valide **messagerie du Contact**.</span><span class="sxs-lookup"><span data-stu-id="d20d9-112">In hello form, provide a **Display Name** and a valid **Contact Email**.</span></span>
5. <span data-ttu-id="d20d9-113">Cliquez sur **Créer l’ID d’application**.</span><span class="sxs-lookup"><span data-stu-id="d20d9-113">Click **Create App ID**.</span></span> <span data-ttu-id="d20d9-114">Cela peut vous nécessitent des stratégies de plateforme Facebook tooaccept et effectuer une vérification de sécurité en ligne.</span><span class="sxs-lookup"><span data-stu-id="d20d9-114">This may require you tooaccept Facebook platform policies and complete an online security check.</span></span>
6. <span data-ttu-id="d20d9-115">Dans la colonne de gauche hello, cliquez sur **paramètres** , puis sélectionnez **base** si ne pas déjà sélectionné.</span><span class="sxs-lookup"><span data-stu-id="d20d9-115">In hello left column, click **Settings** and then select **Basic** if not selected already.</span></span>
7. <span data-ttu-id="d20d9-116">Sélectionnez une **catégorie**.</span><span class="sxs-lookup"><span data-stu-id="d20d9-116">Select a **Category**.</span></span> 
8. <span data-ttu-id="d20d9-117">Cliquez sur **+ Ajouter une plateforme**, puis sélectionnez **Site web**.</span><span class="sxs-lookup"><span data-stu-id="d20d9-117">Click **+ Add Platform** and select **Website**.</span></span>
   
    ![Facebook - paramètres](./media/active-directory-b2c-setup-fb-app/fb-settings.png)
   
    ![Facebook - paramètres - site Web](./media/active-directory-b2c-setup-fb-app/fb-website.png)
9. <span data-ttu-id="d20d9-120">Entrez `https://login.microsoftonline.com/` Bonjour **URL du Site** champ, puis cliquez sur **enregistrer les modifications** bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="d20d9-120">Enter `https://login.microsoftonline.com/` in hello **Site URL** field and then click **Save Changes** at hello bottom of hello page.</span></span>
   
    ![Facebook - URL du site](./media/active-directory-b2c-setup-fb-app/fb-site-url.png)

10. <span data-ttu-id="d20d9-122">Copiez la valeur hello **ID d’application**.</span><span class="sxs-lookup"><span data-stu-id="d20d9-122">Copy hello value of **App ID**.</span></span> <span data-ttu-id="d20d9-123">Cliquez sur **afficher** et copiez la valeur hello **Secret d’application**.</span><span class="sxs-lookup"><span data-stu-id="d20d9-123">Click **Show** and copy hello value of **App Secret**.</span></span> <span data-ttu-id="d20d9-124">Vous devez les deux tooconfigure Facebook comme fournisseur d’identité dans votre client.</span><span class="sxs-lookup"><span data-stu-id="d20d9-124">You will need both of them tooconfigure Facebook as an identity provider in your tenant.</span></span> <span data-ttu-id="d20d9-125">**App Secret** est une information d’identification de sécurité importante.</span><span class="sxs-lookup"><span data-stu-id="d20d9-125">**App Secret** is an important security credential.</span></span>
   
    ![Facebook - ID et clé secrète de l’application](./media/active-directory-b2c-setup-fb-app/fb-app-id-app-secret.png)
11. <span data-ttu-id="d20d9-127">Cliquez sur **+ ajouter un produit** hello de navigation de gauche et puis hello **Set Up** bouton **connexion Facebook**.</span><span class="sxs-lookup"><span data-stu-id="d20d9-127">Click **+ Add Product** on hello left navigation and then hello **Set Up** button for **Facebook Login**.</span></span>
   
    ![Facebook - Connexion Facebook](./media/active-directory-b2c-setup-fb-app/fb-login.png)
12. <span data-ttu-id="d20d9-129">Cliquez sur **paramètres** sur nav de droite hello sous **connexion Facebook**</span><span class="sxs-lookup"><span data-stu-id="d20d9-129">Click **Settings** on hello right nav under **Facebook Login**</span></span>

    ![Facebook - Paramètres Connexion Facebook](./media/active-directory-b2c-setup-fb-app/fb-login-settings.png)
13. <span data-ttu-id="d20d9-131">Entrez `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` Bonjour **URI de redirection OAuth valide** champ hello **les paramètres Client OAuth** section.</span><span class="sxs-lookup"><span data-stu-id="d20d9-131">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Valid OAuth redirect URIs** field in hello **Client OAuth Settings** section.</span></span> <span data-ttu-id="d20d9-132">Remplacez **{tenant}** par votre nom de client (par exemple, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="d20d9-132">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="d20d9-133">Cliquez sur **enregistrer les modifications** bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="d20d9-133">Click **Save Changes** at hello bottom of hello page.</span></span>
    
    ![Facebook - OAuth Redirect URI](./media/active-directory-b2c-setup-fb-app/fb-oauth-redirect-uri.png)
14. <span data-ttu-id="d20d9-135">toomake votre application Facebook utilisable par Azure AD B2C, vous devez toomake publiquement disponibles.</span><span class="sxs-lookup"><span data-stu-id="d20d9-135">toomake your Facebook application usable by Azure AD B2C, you need toomake it publicly available.</span></span> <span data-ttu-id="d20d9-136">Vous pouvez le faire en cliquant sur **révision d’application** basculer sur hello barre de navigation gauche et en activant le hello en hello haut hello trop**Oui** et en cliquant sur **confirmer**.</span><span class="sxs-lookup"><span data-stu-id="d20d9-136">You can do this by clicking **App Review** on hello left navigation and by turning hello switch at hello top of hello page too**YES** and clicking **Confirm**.</span></span>
    
    ![Facebook - App publique](./media/active-directory-b2c-setup-fb-app/fb-app-public.png)

## <a name="configure-facebook-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="d20d9-138">Configuration de Facebook en tant que fournisseur d’identité dans votre client</span><span class="sxs-lookup"><span data-stu-id="d20d9-138">Configure Facebook as an identity provider in your tenant</span></span>
1. <span data-ttu-id="d20d9-139">Suivez ces étapes trop[accédez Panneau de fonctionnalités toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) sur hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d20d9-139">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="d20d9-140">Dans le panneau de fonctionnalités hello B2C, cliquez sur **fournisseurs d’identité**.</span><span class="sxs-lookup"><span data-stu-id="d20d9-140">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="d20d9-141">Cliquez sur **+ ajouter** haut hello du Panneau de hello.</span><span class="sxs-lookup"><span data-stu-id="d20d9-141">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="d20d9-142">Fournissez un nom convivial de **nom** pour la configuration du fournisseur d’identité hello.</span><span class="sxs-lookup"><span data-stu-id="d20d9-142">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="d20d9-143">Par exemple, entrez « Facebook ».</span><span class="sxs-lookup"><span data-stu-id="d20d9-143">For example, enter "Facebook".</span></span>
5. <span data-ttu-id="d20d9-144">Cliquez sur **Type de fournisseur d’identité**, sélectionnez **Facebook**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="d20d9-144">Click **Identity provider type**, select **Facebook**, and click **OK**.</span></span>
6. <span data-ttu-id="d20d9-145">Cliquez sur **configurer ce fournisseur d’identité** et entrez hello application et le code secret d’application (de hello application Facebook que vous avez créé précédemment) Bonjour **ID Client** et **question secrète du Client**champs respectivement.</span><span class="sxs-lookup"><span data-stu-id="d20d9-145">Click **Set up this identity provider** and enter hello app ID and app secret (of hello Facebook application that you created earlier) in hello **Client ID** and **Client secret** fields respectively.</span></span>
7. <span data-ttu-id="d20d9-146">Cliquez sur **OK**, puis cliquez sur **créer** toosave votre configuration de Facebook.</span><span class="sxs-lookup"><span data-stu-id="d20d9-146">Click **OK**, and then click **Create** toosave your Facebook configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="d20d9-147">Ajout d’un **fournisseur d’identité** tooyour client ne modifie pas vos stratégies existantes.</span><span class="sxs-lookup"><span data-stu-id="d20d9-147">Adding an **Identity provider** tooyour tenant does not modify your existing policies.</span></span> <span data-ttu-id="d20d9-148">N’oubliez pas tooupdate vos stratégies en incluant le fournisseur d’identité hello que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="d20d9-148">Remember tooupdate your policies by including hello identity provider you just created.</span></span>
>