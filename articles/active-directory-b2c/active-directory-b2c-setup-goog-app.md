---
title: 'Azure Active Directory B2C : configuration Google+ | Microsoft Docs'
description: "Fourniture d’inscription et de connexion à des consommateurs disposant de comptes Google+ dans vos applications sécurisées par Azure Active Directory B2C."
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
ms.openlocfilehash: 6ab73e5c79742ab548733f5712dee1e28461db9f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-google-accounts"></a><span data-ttu-id="65491-103">Azure Active Directory B2C : fourniture d’inscription et de connexion à des consommateurs disposant de comptes Google+</span><span class="sxs-lookup"><span data-stu-id="65491-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Google+ accounts</span></span>
## <a name="create-a-google-application"></a><span data-ttu-id="65491-104">Création d’une application Google+</span><span class="sxs-lookup"><span data-stu-id="65491-104">Create a Google+ application</span></span>
<span data-ttu-id="65491-105">Pour utiliser Google+ en tant que fournisseur d’identité dans Azure Active Directory (Azure AD) B2C, vous devez créer une application Google+ et lui fournir les paramètres appropriés.</span><span class="sxs-lookup"><span data-stu-id="65491-105">To use Google+ as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Google+ application and supply it with the right parameters.</span></span> <span data-ttu-id="65491-106">Pour ce faire, vous avez besoin d’un compte Google+.</span><span class="sxs-lookup"><span data-stu-id="65491-106">You need a Google+ account to do this.</span></span> <span data-ttu-id="65491-107">Si vous n’en avez pas, vous pouvez en obtenir un à l’adresse [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).</span><span class="sxs-lookup"><span data-stu-id="65491-107">If you don’t have one, you can get it at [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).</span></span>

1. <span data-ttu-id="65491-108">Accédez à la [Console développeur de Google](https://console.developers.google.com/) et connectez-vous avec les informations d’identification de votre compte Google+.</span><span class="sxs-lookup"><span data-stu-id="65491-108">Go to the [Google Developers Console](https://console.developers.google.com/) and sign in with your Google+ account credentials.</span></span>
2. <span data-ttu-id="65491-109">Cliquez sur **Créer un projet**, saisissez un **nom de projet**, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="65491-109">Click **Create project**, enter a **Project name**, and then click **Create**.</span></span>
   
    ![Google+ - Prise en main](./media/active-directory-b2c-setup-goog-app/google-get-started.png)
   
    ![Google+ - Nouveau projet](./media/active-directory-b2c-setup-goog-app/google-new-project.png)
3. <span data-ttu-id="65491-112">Cliquez sur **Gestionnaire d’API**, puis sur **Informations d’identification** dans le volet de navigation de gauche.</span><span class="sxs-lookup"><span data-stu-id="65491-112">Click **API Manager** and then click **Credentials** in the left navigation.</span></span>
4. <span data-ttu-id="65491-113">Cliquez sur l’onglet **OAuth consent screen** en haut.</span><span class="sxs-lookup"><span data-stu-id="65491-113">Click the **OAuth consent screen** tab at the top.</span></span>
   
    ![Google+ - Informations d’identification](./media/active-directory-b2c-setup-goog-app/google-add-cred.png)
5. <span data-ttu-id="65491-115">Sélectionnez ou spécifiez une valeur valide pour **Adresse de messagerie**, fournissez une valeur pour **Nom de produit**, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="65491-115">Select or specify a valid **Email address**, provide a **Product name**, and click **Save**.</span></span>
   
    ![Google+ - Écran de consentement OAuth](./media/active-directory-b2c-setup-goog-app/google-consent-screen.png)
6. <span data-ttu-id="65491-117">Cliquez sur **Nouvelles informations d’identification**, puis sur **ID client OAuth**.</span><span class="sxs-lookup"><span data-stu-id="65491-117">Click **New credentials** and then choose **OAuth client ID**.</span></span>
   
    ![Google+ - Écran de consentement OAuth](./media/active-directory-b2c-setup-goog-app/google-add-oauth2-client-id.png)
7. <span data-ttu-id="65491-119">Sous **Type d’application**, sélectionnez **Application web**.</span><span class="sxs-lookup"><span data-stu-id="65491-119">Under **Application type**, select **Web application**.</span></span>
   
    ![Google+ - Écran de consentement OAuth](./media/active-directory-b2c-setup-goog-app/google-web-app.png)
8. <span data-ttu-id="65491-121">Fournissez un **nom** pour votre application, entrez `https://login.microsoftonline.com` dans le champ **Origines JavaScript autorisées**, et `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` dans le champ **URI de redirection autorisée**.</span><span class="sxs-lookup"><span data-stu-id="65491-121">Provide a **Name** for your application, enter `https://login.microsoftonline.com` in the **Authorized JavaScript origins** field, and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Authorized redirect URIs** field.</span></span> <span data-ttu-id="65491-122">Remplacez **{tenant}** par votre nom de client (par exemple, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="65491-122">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="65491-123">La valeur **{tenant}** respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="65491-123">The **{tenant}** value is case-sensitive.</span></span> <span data-ttu-id="65491-124">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="65491-124">Click **Create**.</span></span>
   
    ![Google+ - Créer un identifiant client](./media/active-directory-b2c-setup-goog-app/google-create-client-id.png)
9. <span data-ttu-id="65491-126">Copiez les valeurs de **ID client** et **Clé secrète client**.</span><span class="sxs-lookup"><span data-stu-id="65491-126">Copy the values of **Client ID** and **Client secret**.</span></span> <span data-ttu-id="65491-127">Vous aurez besoin de ces deux valeurs pour configurer Google+ en tant que fournisseur d'identité dans votre client.</span><span class="sxs-lookup"><span data-stu-id="65491-127">You will need both of them to configure Google+ as an identity provider in your tenant.</span></span> <span data-ttu-id="65491-128">**Client secret** est une information d’identification de sécurité importante.</span><span class="sxs-lookup"><span data-stu-id="65491-128">**Client secret** is an important security credential.</span></span>
   
    ![Google+ - Clé secrète client](./media/active-directory-b2c-setup-goog-app/google-client-secret.png)

## <a name="configure-google-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="65491-130">Configuration de Google+ en tant que fournisseur d'identité dans votre client</span><span class="sxs-lookup"><span data-stu-id="65491-130">Configure Google+ as an identity provider in your tenant</span></span>
1. <span data-ttu-id="65491-131">Suivez ces étapes pour [accéder au panneau de fonctionnalités B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="65491-131">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="65491-132">Dans le panneau de fonctionnalités B2C, cliquez sur **Fournisseurs d’identité**.</span><span class="sxs-lookup"><span data-stu-id="65491-132">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="65491-133">Cliquez sur **+Ajouter** dans la partie supérieure du panneau.</span><span class="sxs-lookup"><span data-stu-id="65491-133">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="65491-134">Fournissez un **Nom** convivial pour la configuration de fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="65491-134">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="65491-135">Par exemple, entrez « G+ ».</span><span class="sxs-lookup"><span data-stu-id="65491-135">For example, enter "G+".</span></span>
5. <span data-ttu-id="65491-136">Cliquez sur **Type de fournisseur d’identité**, sélectionnez **Google**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="65491-136">Click **Identity provider type**, select **Google**, and click **OK**.</span></span>
6. <span data-ttu-id="65491-137">Cliquez sur **Configurer ce fournisseur d’identité** , puis entrez l’ID client et la clé secrète client de l’application Google+ que vous avez créée précédemment.</span><span class="sxs-lookup"><span data-stu-id="65491-137">Click **Set up this identity provider** and enter the client ID and client secret of the Google+ application that you created earlier.</span></span>
7. <span data-ttu-id="65491-138">Cliquez sur **OK**, puis sur **Créer** pour enregistrer votre configuration Google+.</span><span class="sxs-lookup"><span data-stu-id="65491-138">Click **OK** and then click **Create** to save your Google+ configuration.</span></span>

