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
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-google-accounts"></a><span data-ttu-id="6fa70-103">Azure B2C Active Directory : Fournir tooconsumers d’abonnement et connectez-vous avec des comptes Google +</span><span class="sxs-lookup"><span data-stu-id="6fa70-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Google+ accounts</span></span>
## <a name="create-a-google-application"></a><span data-ttu-id="6fa70-104">Création d’une application Google+</span><span class="sxs-lookup"><span data-stu-id="6fa70-104">Create a Google+ application</span></span>
<span data-ttu-id="6fa70-105">toouse + Google comme fournisseur d’identité dans Azure Active Directory (Azure AD) B2C, vous devez toocreate une application Google + et lui fournir les paramètres appropriés hello.</span><span class="sxs-lookup"><span data-stu-id="6fa70-105">toouse Google+ as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Google+ application and supply it with hello right parameters.</span></span> <span data-ttu-id="6fa70-106">Vous devez cela un toodo compte Google +.</span><span class="sxs-lookup"><span data-stu-id="6fa70-106">You need a Google+ account toodo this.</span></span> <span data-ttu-id="6fa70-107">Si vous n’en avez pas, vous pouvez en obtenir un à l’adresse [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).</span><span class="sxs-lookup"><span data-stu-id="6fa70-107">If you don’t have one, you can get it at [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).</span></span>

1. <span data-ttu-id="6fa70-108">Accédez toohello [Console des développeurs Google](https://console.developers.google.com/) et connectez-vous avec vos informations d’identification compte Google +.</span><span class="sxs-lookup"><span data-stu-id="6fa70-108">Go toohello [Google Developers Console](https://console.developers.google.com/) and sign in with your Google+ account credentials.</span></span>
2. <span data-ttu-id="6fa70-109">Cliquez sur **Créer un projet**, saisissez un **nom de projet**, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="6fa70-109">Click **Create project**, enter a **Project name**, and then click **Create**.</span></span>
   
    ![Google+ - Prise en main](./media/active-directory-b2c-setup-goog-app/google-get-started.png)
   
    ![Google+ - Nouveau projet](./media/active-directory-b2c-setup-goog-app/google-new-project.png)
3. <span data-ttu-id="6fa70-112">Cliquez sur **API Manager** puis cliquez sur **informations d’identification** Bonjour barre de navigation gauche.</span><span class="sxs-lookup"><span data-stu-id="6fa70-112">Click **API Manager** and then click **Credentials** in hello left navigation.</span></span>
4. <span data-ttu-id="6fa70-113">Cliquez sur hello **écran de consentement OAuth** onglet en haut de hello.</span><span class="sxs-lookup"><span data-stu-id="6fa70-113">Click hello **OAuth consent screen** tab at hello top.</span></span>
   
    ![Google+ - Informations d’identification](./media/active-directory-b2c-setup-goog-app/google-add-cred.png)
5. <span data-ttu-id="6fa70-115">Sélectionnez ou spécifiez une valeur valide pour **Adresse de messagerie**, fournissez une valeur pour **Nom de produit**, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="6fa70-115">Select or specify a valid **Email address**, provide a **Product name**, and click **Save**.</span></span>
   
    ![Google+ - Écran de consentement OAuth](./media/active-directory-b2c-setup-goog-app/google-consent-screen.png)
6. <span data-ttu-id="6fa70-117">Cliquez sur **Nouvelles informations d’identification**, puis sur **ID client OAuth**.</span><span class="sxs-lookup"><span data-stu-id="6fa70-117">Click **New credentials** and then choose **OAuth client ID**.</span></span>
   
    ![Google+ - Écran de consentement OAuth](./media/active-directory-b2c-setup-goog-app/google-add-oauth2-client-id.png)
7. <span data-ttu-id="6fa70-119">Sous **Type d’application**, sélectionnez **Application web**.</span><span class="sxs-lookup"><span data-stu-id="6fa70-119">Under **Application type**, select **Web application**.</span></span>
   
    ![Google+ - Écran de consentement OAuth](./media/active-directory-b2c-setup-goog-app/google-web-app.png)
8. <span data-ttu-id="6fa70-121">Fournir un **nom** pour votre application, entrez `https://login.microsoftonline.com` Bonjour **autorisé de JavaScript origines** champ, et `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` Bonjour **autorisés rediriger URI**champ.</span><span class="sxs-lookup"><span data-stu-id="6fa70-121">Provide a **Name** for your application, enter `https://login.microsoftonline.com` in hello **Authorized JavaScript origins** field, and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Authorized redirect URIs** field.</span></span> <span data-ttu-id="6fa70-122">Remplacez **{tenant}** par votre nom de client (par exemple, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="6fa70-122">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="6fa70-123">Hello **{tenant}** valeur respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="6fa70-123">hello **{tenant}** value is case-sensitive.</span></span> <span data-ttu-id="6fa70-124">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="6fa70-124">Click **Create**.</span></span>
   
    ![Google+ - Créer un identifiant client](./media/active-directory-b2c-setup-goog-app/google-create-client-id.png)
9. <span data-ttu-id="6fa70-126">Copier les valeurs hello de **ID Client** et **clé secrète Client**.</span><span class="sxs-lookup"><span data-stu-id="6fa70-126">Copy hello values of **Client ID** and **Client secret**.</span></span> <span data-ttu-id="6fa70-127">Vous devez les deux tooconfigure Google + en tant que fournisseur d’identité dans votre client.</span><span class="sxs-lookup"><span data-stu-id="6fa70-127">You will need both of them tooconfigure Google+ as an identity provider in your tenant.</span></span> <span data-ttu-id="6fa70-128">**Client secret** est une information d’identification de sécurité importante.</span><span class="sxs-lookup"><span data-stu-id="6fa70-128">**Client secret** is an important security credential.</span></span>
   
    ![Google+ - Clé secrète client](./media/active-directory-b2c-setup-goog-app/google-client-secret.png)

## <a name="configure-google-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="6fa70-130">Configuration de Google+ en tant que fournisseur d'identité dans votre client</span><span class="sxs-lookup"><span data-stu-id="6fa70-130">Configure Google+ as an identity provider in your tenant</span></span>
1. <span data-ttu-id="6fa70-131">Suivez ces étapes trop[accédez Panneau de fonctionnalités toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) sur hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="6fa70-131">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="6fa70-132">Dans le panneau de fonctionnalités hello B2C, cliquez sur **fournisseurs d’identité**.</span><span class="sxs-lookup"><span data-stu-id="6fa70-132">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="6fa70-133">Cliquez sur **+ ajouter** haut hello du Panneau de hello.</span><span class="sxs-lookup"><span data-stu-id="6fa70-133">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="6fa70-134">Fournissez un nom convivial de **nom** pour la configuration du fournisseur d’identité hello.</span><span class="sxs-lookup"><span data-stu-id="6fa70-134">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="6fa70-135">Par exemple, entrez « G+ ».</span><span class="sxs-lookup"><span data-stu-id="6fa70-135">For example, enter "G+".</span></span>
5. <span data-ttu-id="6fa70-136">Cliquez sur **Type de fournisseur d’identité**, sélectionnez **Google**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="6fa70-136">Click **Identity provider type**, select **Google**, and click **OK**.</span></span>
6. <span data-ttu-id="6fa70-137">Cliquez sur **configurer ce fournisseur d’identité** et entrez hello client et ID de clé secrète client de hello application Google + que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="6fa70-137">Click **Set up this identity provider** and enter hello client ID and client secret of hello Google+ application that you created earlier.</span></span>
7. <span data-ttu-id="6fa70-138">Cliquez sur **OK** puis cliquez sur **créer** toosave votre configuration de Google +.</span><span class="sxs-lookup"><span data-stu-id="6fa70-138">Click **OK** and then click **Create** toosave your Google+ configuration.</span></span>

