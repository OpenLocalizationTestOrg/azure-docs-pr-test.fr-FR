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
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-microsoft-accounts"></a><span data-ttu-id="ae6d3-103">Azure B2C Active Directory : Fournir tooconsumers d’abonnement et connectez-vous avec les comptes Microsoft</span><span class="sxs-lookup"><span data-stu-id="ae6d3-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Microsoft accounts</span></span>
## <a name="create-a-microsoft-account-application"></a><span data-ttu-id="ae6d3-104">Créer une application de compte Microsoft</span><span class="sxs-lookup"><span data-stu-id="ae6d3-104">Create a Microsoft account application</span></span>
<span data-ttu-id="ae6d3-105">toouse de compte Microsoft en tant que fournisseur d’identité dans Azure Active Directory (Azure AD) B2C, vous devez toocreate une application de compte Microsoft et lui fournir les paramètres appropriés hello.</span><span class="sxs-lookup"><span data-stu-id="ae6d3-105">toouse Microsoft account as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Microsoft account application and supply it with hello right parameters.</span></span> <span data-ttu-id="ae6d3-106">Vous devez cela un toodo de compte Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ae6d3-106">You need a Microsoft account toodo this.</span></span> <span data-ttu-id="ae6d3-107">Si vous n’en avez pas, vous pouvez en obtenir un à l’adresse [https://www.live.com/](https://www.live.com/).</span><span class="sxs-lookup"><span data-stu-id="ae6d3-107">If you don’t have one, you can get it at [https://www.live.com/](https://www.live.com/).</span></span>

1. <span data-ttu-id="ae6d3-108">Accédez toohello [portail de l’enregistrement d’Application Microsoft](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) et connectez-vous avec vos informations d’identification du compte Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ae6d3-108">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) and sign in with your Microsoft account credentials.</span></span>
2. <span data-ttu-id="ae6d3-109">Cliquez sur **Ajouter une application**.</span><span class="sxs-lookup"><span data-stu-id="ae6d3-109">Click **Add an app**.</span></span>
   
    ![Compte Microsoft - Ajouter une nouvelle application](./media/active-directory-b2c-setup-msa-app/msa-add-new-app.png)
3. <span data-ttu-id="ae6d3-111">Indiquez un **nom** pour votre application et cliquez sur **Créer une application**.</span><span class="sxs-lookup"><span data-stu-id="ae6d3-111">Provide a **Name** for your application and click **Create application**.</span></span>
   
    ![Compte Microsoft - Nom d’application](./media/active-directory-b2c-setup-msa-app/msa-app-name.png)
4. <span data-ttu-id="ae6d3-113">Copiez la valeur hello **Id de l’Application**. Vous en aurez besoin tooconfigure compte Microsoft en tant que fournisseur d’identité dans votre client.</span><span class="sxs-lookup"><span data-stu-id="ae6d3-113">Copy hello value of **Application Id**. You will need it tooconfigure Microsoft account as an identity provider in your tenant.</span></span>
   
    ![Compte Microsoft - ID de l’application](./media/active-directory-b2c-setup-msa-app/msa-app-id.png)
5. <span data-ttu-id="ae6d3-115">Cliquez sur **Ajouter une plateforme** et choisissez **Web**.</span><span class="sxs-lookup"><span data-stu-id="ae6d3-115">Click on **Add platform** and choose **Web**.</span></span>
   
    ![Compte Microsoft - Ajouter une plateforme](./media/active-directory-b2c-setup-msa-app/msa-add-platform.png)
   
    ![Compte Microsoft - Web](./media/active-directory-b2c-setup-msa-app/msa-web.png)
6. <span data-ttu-id="ae6d3-118">Entrez `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` Bonjour **URI de redirection** champ.</span><span class="sxs-lookup"><span data-stu-id="ae6d3-118">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Redirect URIs** field.</span></span> <span data-ttu-id="ae6d3-119">Remplacez **{tenant}** par votre nom de client (par exemple, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="ae6d3-119">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span>
   
    ![Compte Microsoft - URL de redirection](./media/active-directory-b2c-setup-msa-app/msa-redirect-url.png)
7. <span data-ttu-id="ae6d3-121">Cliquez sur **générer un nouveau mot de passe** sous hello **Application Secrets** section.</span><span class="sxs-lookup"><span data-stu-id="ae6d3-121">Click on **Generate New Password** under hello **Application Secrets** section.</span></span> <span data-ttu-id="ae6d3-122">Copiez le nouveau mot de passe hello affiché sur l’écran.</span><span class="sxs-lookup"><span data-stu-id="ae6d3-122">Copy hello new password displayed on screen.</span></span> <span data-ttu-id="ae6d3-123">Vous en aurez besoin tooconfigure compte Microsoft en tant que fournisseur d’identité dans votre client.</span><span class="sxs-lookup"><span data-stu-id="ae6d3-123">You will need it tooconfigure Microsoft account as an identity provider in your tenant.</span></span> <span data-ttu-id="ae6d3-124">Ce mot de passe est une information d’identification de sécurité importante.</span><span class="sxs-lookup"><span data-stu-id="ae6d3-124">This password is an important security credential.</span></span>
   
    ![Compte Microsoft - générer un nouveau mot de passe](./media/active-directory-b2c-setup-msa-app/msa-generate-new-password.png)
   
    ![Compte Microsoft - Nouveau mot de passe](./media/active-directory-b2c-setup-msa-app/msa-new-password.png)
8. <span data-ttu-id="ae6d3-127">Case à cocher hello indiquant **prise en charge du Kit de développement logiciel Live** sous hello **Options avancées** section.</span><span class="sxs-lookup"><span data-stu-id="ae6d3-127">Check hello box that says **Live SDK support** under hello **Advanced Options** section.</span></span> <span data-ttu-id="ae6d3-128">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="ae6d3-128">Click **Save**.</span></span>
   
    ![Compte Microsoft - Support du Kit SDK Live](./media/active-directory-b2c-setup-msa-app/msa-live-sdk-support.png)

## <a name="configure-microsoft-account-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="ae6d3-130">Configuration du compte Microsoft en tant que fournisseur d’identité dans votre client</span><span class="sxs-lookup"><span data-stu-id="ae6d3-130">Configure Microsoft account as an identity provider in your tenant</span></span>
1. <span data-ttu-id="ae6d3-131">Suivez ces étapes trop[accédez Panneau de fonctionnalités toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) sur hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ae6d3-131">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="ae6d3-132">Dans le panneau de fonctionnalités hello B2C, cliquez sur **fournisseurs d’identité**.</span><span class="sxs-lookup"><span data-stu-id="ae6d3-132">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="ae6d3-133">Cliquez sur **+ ajouter** haut hello du Panneau de hello.</span><span class="sxs-lookup"><span data-stu-id="ae6d3-133">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="ae6d3-134">Fournissez un nom convivial de **nom** pour la configuration du fournisseur d’identité hello.</span><span class="sxs-lookup"><span data-stu-id="ae6d3-134">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="ae6d3-135">Par exemple, saisissez « MSA ».</span><span class="sxs-lookup"><span data-stu-id="ae6d3-135">For example, enter "MSA".</span></span>
5. <span data-ttu-id="ae6d3-136">Cliquez sur **Type de fournisseur d’identité**, sélectionnez **Compte Microsoft**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="ae6d3-136">Click **Identity provider type**, select **Microsoft account**, and click **OK**.</span></span>
6. <span data-ttu-id="ae6d3-137">Cliquez sur **configurer ce fournisseur d’identité** et entrez hello Id d’Application et mot de passe de hello application de compte Microsoft que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="ae6d3-137">Click **Set up this identity provider** and enter hello Application Id and password of hello Microsoft account application that you created earlier.</span></span>
7. <span data-ttu-id="ae6d3-138">Cliquez sur **OK** puis cliquez sur **créer** toosave configuration de compte Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ae6d3-138">Click **OK** and then click **Create** toosave your Microsoft account configuration.</span></span>

