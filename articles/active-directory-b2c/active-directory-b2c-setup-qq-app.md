---
title: 'Azure Active Directory B2C : configuration QQ | Microsoft Docs'
description: "Fournir tooconsumers d’abonnement et connectez-vous avec des comptes QQ dans vos applications sont sécurisées par Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 18c2cf94-8004-4de1-81c2-e45be65ce12d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: 896d6221e01d15de1652a5717cf1f65619101e0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-qq-accounts"></a><span data-ttu-id="2ce42-103">Azure B2C Active Directory : Fournir tooconsumers d’abonnement et connectez-vous avec les comptes QQ</span><span class="sxs-lookup"><span data-stu-id="2ce42-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with QQ accounts</span></span>

> [!NOTE]
> <span data-ttu-id="2ce42-104">Cette fonctionnalité est en préversion.</span><span class="sxs-lookup"><span data-stu-id="2ce42-104">This feature is in preview.</span></span>
> 

## <a name="create-a-qq-application"></a><span data-ttu-id="2ce42-105">Créer une application QQ</span><span class="sxs-lookup"><span data-stu-id="2ce42-105">Create a QQ application</span></span>

<span data-ttu-id="2ce42-106">toouse QQ comme fournisseur d’identité dans Azure Active Directory (Azure AD) B2C, vous devez toocreate une application QQ et lui fournir les paramètres appropriés hello.</span><span class="sxs-lookup"><span data-stu-id="2ce42-106">toouse QQ as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a QQ application and supply it with hello right parameters.</span></span> <span data-ttu-id="2ce42-107">Vous devez un toodo de compte QQ cela.</span><span class="sxs-lookup"><span data-stu-id="2ce42-107">You need a QQ account toodo this.</span></span> <span data-ttu-id="2ce42-108">Si vous n’avez pas, vous pouvez en obtenir un à la page [https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033](https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033).</span><span class="sxs-lookup"><span data-stu-id="2ce42-108">If you don’t have one, you can get one at [https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033](https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033).</span></span>

### <a name="register-for-hello-qq-developer-program"></a><span data-ttu-id="2ce42-109">Inscrivez-vous au programme pour développeur QQ hello</span><span class="sxs-lookup"><span data-stu-id="2ce42-109">Register for hello QQ developer program</span></span>

1. <span data-ttu-id="2ce42-110">Accédez toohello [portail des développeurs QQ](http://open.qq.com) et connectez-vous avec vos informations d’identification du compte QQ.</span><span class="sxs-lookup"><span data-stu-id="2ce42-110">Go toohello [QQ developer portal](http://open.qq.com) and sign in with your QQ account credentials.</span></span>
2. <span data-ttu-id="2ce42-111">Une fois connecté, accédez trop[http://open.qq.com/reg](http://open.qq.com/reg) tooregister vous-même en tant que développeur.</span><span class="sxs-lookup"><span data-stu-id="2ce42-111">After signing in, go too[http://open.qq.com/reg](http://open.qq.com/reg) tooregister yourself as a developer.</span></span>
3. <span data-ttu-id="2ce42-112">Dans le menu de hello, sélectionnez**个人**(developer individuel).</span><span class="sxs-lookup"><span data-stu-id="2ce42-112">In hello menu, select **个人** (individual developer).</span></span>
4. <span data-ttu-id="2ce42-113">Entrez les informations de hello requis dans le formulaire de hello et cliquez sur**下一步**(étape suivante).</span><span class="sxs-lookup"><span data-stu-id="2ce42-113">Enter hello required information into hello form and click **下一步** (next step).</span></span>
5. <span data-ttu-id="2ce42-114">Terminer le processus de vérification du courrier électronique hello.</span><span class="sxs-lookup"><span data-stu-id="2ce42-114">Complete hello email verification process.</span></span>

> [!NOTE]
> <span data-ttu-id="2ce42-115">Vous devez toowait quelques jours toobe approuvé une fois inscrit en tant que développeur.</span><span class="sxs-lookup"><span data-stu-id="2ce42-115">You will need toowait a few days toobe approved after registering as a developer.</span></span> 

### <a name="register-a-qq-application"></a><span data-ttu-id="2ce42-116">Inscrire une application QQ</span><span class="sxs-lookup"><span data-stu-id="2ce42-116">Register a QQ application</span></span>

1. <span data-ttu-id="2ce42-117">Accédez trop[https://connect.qq.com/index.html](https://connect.qq.com/index.html).</span><span class="sxs-lookup"><span data-stu-id="2ce42-117">Go too[https://connect.qq.com/index.html](https://connect.qq.com/index.html).</span></span>
2. <span data-ttu-id="2ce42-118">Cliquez sur **应用管理** (Gestion de l’application).</span><span class="sxs-lookup"><span data-stu-id="2ce42-118">Click on **应用管理** (app management).</span></span>
3. <span data-ttu-id="2ce42-119">Cliquez sur **创建应用** (Création d’application).</span><span class="sxs-lookup"><span data-stu-id="2ce42-119">Click on **创建应用** (create app).</span></span>
4. <span data-ttu-id="2ce42-120">Entrez les informations d’application nécessaire hello.</span><span class="sxs-lookup"><span data-stu-id="2ce42-120">Enter hello necessary app information.</span></span>
5. <span data-ttu-id="2ce42-121">Cliquez sur **创建应用** (Création d’application).</span><span class="sxs-lookup"><span data-stu-id="2ce42-121">Click on **创建应用** (create app).</span></span>
6. <span data-ttu-id="2ce42-122">Entrez les informations de hello requis.</span><span class="sxs-lookup"><span data-stu-id="2ce42-122">Enter hello required information.</span></span>
7. <span data-ttu-id="2ce42-123">Pourquoi**授权回调域**(URL de rappel), entrez `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="2ce42-123">For hello **授权回调域** (callback URL) field, enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span></span> <span data-ttu-id="2ce42-124">Par exemple, si votre `tenant_name` est contoso.onmicrosoft.com, jeu hello URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="2ce42-124">For example, if your `tenant_name` is contoso.onmicrosoft.com, set hello URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
8. <span data-ttu-id="2ce42-125">Cliquez sur **创建应用** (Création d’application).</span><span class="sxs-lookup"><span data-stu-id="2ce42-125">Click on **创建应用** (create app).</span></span>
9. <span data-ttu-id="2ce42-126">Dans la page de confirmation hello, cliquez sur**应用管理**page de gestion des applications (gestion des applications) tooreturn toohello.</span><span class="sxs-lookup"><span data-stu-id="2ce42-126">On hello confirmation page, click on **应用管理** (app management) tooreturn toohello app management page.</span></span>
10. <span data-ttu-id="2ce42-127">Cliquez sur**查看**prochaine application toohello (vue), vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="2ce42-127">Click on **查看** (view) next toohello app you just created.</span></span>
11. <span data-ttu-id="2ce42-128">Cliquez sur **修改** (Modifier).</span><span class="sxs-lookup"><span data-stu-id="2ce42-128">Click on **修改** (edit).</span></span>
12. <span data-ttu-id="2ce42-129">À partir de hello en haut de page de hello, copiez hello **ID d’application** et **clé application**.</span><span class="sxs-lookup"><span data-stu-id="2ce42-129">From hello top of hello page, copy hello **APP ID** and **APP KEY**.</span></span>

## <a name="configure-qq-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="2ce42-130">Configuration de QQ en tant que fournisseur d'identité dans votre client</span><span class="sxs-lookup"><span data-stu-id="2ce42-130">Configure QQ as an identity provider in your tenant</span></span>
1. <span data-ttu-id="2ce42-131">Suivez ces étapes trop[accédez Panneau de fonctionnalités toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) sur hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2ce42-131">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="2ce42-132">Dans le panneau de fonctionnalités hello B2C, cliquez sur **fournisseurs d’identité**.</span><span class="sxs-lookup"><span data-stu-id="2ce42-132">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="2ce42-133">Cliquez sur **+ ajouter** haut hello du Panneau de hello.</span><span class="sxs-lookup"><span data-stu-id="2ce42-133">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="2ce42-134">Fournissez un nom convivial de **nom** pour la configuration du fournisseur d’identité hello.</span><span class="sxs-lookup"><span data-stu-id="2ce42-134">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="2ce42-135">Par exemple, entrez « QQ ».</span><span class="sxs-lookup"><span data-stu-id="2ce42-135">For example, enter "QQ".</span></span>
5. <span data-ttu-id="2ce42-136">Cliquez sur **Type de fournisseur d’identité**, sélectionnez **QQ**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="2ce42-136">Click **Identity provider type**, select **QQ**, and click **OK**.</span></span>
6. <span data-ttu-id="2ce42-137">Cliquez sur **Configurer ce fournisseur d’identité**.</span><span class="sxs-lookup"><span data-stu-id="2ce42-137">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="2ce42-138">Entrez hello **clé application** que vous avez copiée précédemment comme hello **ID Client**.</span><span class="sxs-lookup"><span data-stu-id="2ce42-138">Enter hello **App Key** that you copied earlier as hello **Client ID**.</span></span>
8. <span data-ttu-id="2ce42-139">Entrez hello **Secret d’application** que vous avez copiée précédemment comme hello **clé secrète Client**.</span><span class="sxs-lookup"><span data-stu-id="2ce42-139">Enter hello **App Secret** that you copied earlier as hello **Client Secret**.</span></span>
9. <span data-ttu-id="2ce42-140">Cliquez sur **OK** puis cliquez sur **créer** toosave votre configuration QQ.</span><span class="sxs-lookup"><span data-stu-id="2ce42-140">Click **OK** and then click **Create** toosave your QQ configuration.</span></span>

