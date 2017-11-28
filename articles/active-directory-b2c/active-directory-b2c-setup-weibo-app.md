---
title: 'Azure Active Directory B2C : configuration Weibo | Microsoft Docs'
description: "Proposez l’inscription et la connexion à des consommateurs disposant de comptes Weibo dans vos applications sécurisées par Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 1860de34-94cb-4ceb-851e-102f930f7230
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: 00c5d3781455c80b33bdbb4c872ae354531baf3e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-weibo-accounts"></a><span data-ttu-id="a82f2-103">Azure Active Directory B2C : Proposer l’inscription et la connexion à des consommateurs disposant de comptes Weibo</span><span class="sxs-lookup"><span data-stu-id="a82f2-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Weibo accounts</span></span>

> [!NOTE]
> <span data-ttu-id="a82f2-104">Cette fonctionnalité est en préversion.</span><span class="sxs-lookup"><span data-stu-id="a82f2-104">This feature is in preview.</span></span> <span data-ttu-id="a82f2-105">N’utilisez pas ce fournisseur d’identité dans votre environnement de production.</span><span class="sxs-lookup"><span data-stu-id="a82f2-105">Do not use this identity provider in your production environment.</span></span>
> 

## <a name="create-a-weibo-application"></a><span data-ttu-id="a82f2-106">Créer une application Weibo</span><span class="sxs-lookup"><span data-stu-id="a82f2-106">Create a Weibo application</span></span>

<span data-ttu-id="a82f2-107">Pour utiliser Weibo en tant que fournisseur d’identité dans Azure Active Directory (Azure AD) B2C, vous devez créer une application Weibo et lui fournir les paramètres appropriés.</span><span class="sxs-lookup"><span data-stu-id="a82f2-107">To use Weibo as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Weibo application and supply it with the right parameters.</span></span> <span data-ttu-id="a82f2-108">Pour ce faire, vous avez besoin d’un compte Weibo.</span><span class="sxs-lookup"><span data-stu-id="a82f2-108">You need a Weibo account to do this.</span></span> <span data-ttu-id="a82f2-109">Si vous n’en avez pas, vous pouvez en obtenir un à l’adresse [http://weibo.com/signup/signup.php?lang=en-us](http://weibo.com/signup/signup.php?lang=en-us).</span><span class="sxs-lookup"><span data-stu-id="a82f2-109">If you don’t have one, you can get one at [http://weibo.com/signup/signup.php?lang=en-us](http://weibo.com/signup/signup.php?lang=en-us).</span></span>

### <a name="register-for-the-weibo-developer-program"></a><span data-ttu-id="a82f2-110">Inscrivez-vous au programme de développement Weibo</span><span class="sxs-lookup"><span data-stu-id="a82f2-110">Register for the Weibo developer program</span></span>

1. <span data-ttu-id="a82f2-111">Accédez au [centre des développeurs Weibo](http://open.weibo.com/) et connectez-vous avec les informations d’identification de votre compte Weibo.</span><span class="sxs-lookup"><span data-stu-id="a82f2-111">Go to the [Weibo developer portal](http://open.weibo.com/) and sign in with your Weibo account credentials.</span></span>
2. <span data-ttu-id="a82f2-112">Une fois que vous êtes connecté, cliquez sur votre nom d’affichage dans le coin supérieur droit.</span><span class="sxs-lookup"><span data-stu-id="a82f2-112">After signing in, click on your display name in the top-right corner.</span></span>
3. <span data-ttu-id="a82f2-113">Dans la liste déroulante, sélectionnez **编辑开发者信息** (Modifier les informations destinées aux développeurs).</span><span class="sxs-lookup"><span data-stu-id="a82f2-113">In the dropdown, select **编辑开发者信息** (edit developer information).</span></span>
4. <span data-ttu-id="a82f2-114">Entrez les informations requises dans le formulaire, puis cliquez sur **提交** (Envoyer).</span><span class="sxs-lookup"><span data-stu-id="a82f2-114">Enter the required information into the form and click **提交** (submit).</span></span>
5. <span data-ttu-id="a82f2-115">Finalisez le processus de vérification d’e-mail.</span><span class="sxs-lookup"><span data-stu-id="a82f2-115">Complete the email verification process.</span></span>
6. <span data-ttu-id="a82f2-116">Accédez à la page de [vérification d’identité](http://open.weibo.com/developers/identity/edit).</span><span class="sxs-lookup"><span data-stu-id="a82f2-116">Go to the [identity verification page](http://open.weibo.com/developers/identity/edit).</span></span>
7. <span data-ttu-id="a82f2-117">Entrez les informations requises dans le formulaire, puis cliquez sur **提交** (Envoyer).</span><span class="sxs-lookup"><span data-stu-id="a82f2-117">Enter the required information into the form and click **提交** (submit).</span></span>

### <a name="register-a-weibo-application"></a><span data-ttu-id="a82f2-118">Inscrire une application Weibo</span><span class="sxs-lookup"><span data-stu-id="a82f2-118">Register a Weibo application</span></span>

1. <span data-ttu-id="a82f2-119">Accédez à la [Page d’inscription de l’application Weibo](http://open.weibo.com/apps/new).</span><span class="sxs-lookup"><span data-stu-id="a82f2-119">Go to the [new Weibo app registration page](http://open.weibo.com/apps/new).</span></span>
2. <span data-ttu-id="a82f2-120">Entrez les informations nécessaires relatives à l’application.</span><span class="sxs-lookup"><span data-stu-id="a82f2-120">Enter the necessary application information.</span></span>
3. <span data-ttu-id="a82f2-121">Cliquez sur **创建** (Créer).</span><span class="sxs-lookup"><span data-stu-id="a82f2-121">Click **创建** (create).</span></span>
4. <span data-ttu-id="a82f2-122">Copiez les valeurs **Clé d’application** et **Secret d’application**.</span><span class="sxs-lookup"><span data-stu-id="a82f2-122">Copy the values of **App Key** and **App Secret**.</span></span> <span data-ttu-id="a82f2-123">Vous en aurez besoin ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="a82f2-123">You will need this later.</span></span>
5. <span data-ttu-id="a82f2-124">Téléchargez les photos requises et entrez les informations nécessaires.</span><span class="sxs-lookup"><span data-stu-id="a82f2-124">Upload the required photos and enter the necessary information.</span></span>
6. <span data-ttu-id="a82f2-125">Cliquez sur **保存以上信息** (Enregistrer).</span><span class="sxs-lookup"><span data-stu-id="a82f2-125">Click **保存以上信息** (save).</span></span>
7. <span data-ttu-id="a82f2-126">Cliquez sur **高级信息** (Informations avancées).</span><span class="sxs-lookup"><span data-stu-id="a82f2-126">Click **高级信息** (advanced information).</span></span>
8. <span data-ttu-id="a82f2-127">Cliquez sur **编辑** (Modifier) en regard du champ pour OAuth2.0 **授权设置** (URL de redirection).</span><span class="sxs-lookup"><span data-stu-id="a82f2-127">Click **编辑** (edit) next to the field for OAuth2.0 **授权设置** (redirect URL).</span></span>
9. <span data-ttu-id="a82f2-128">Entrez `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp` pour OAuth2.0 **授权设置** (URL de redirection).</span><span class="sxs-lookup"><span data-stu-id="a82f2-128">Enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp` for OAuth2.0 **授权设置** (redirect URL).</span></span> <span data-ttu-id="a82f2-129">Par exemple, si votre `tenant_name` est contoso.onmicrosoft.com, définissez l’URL sur `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="a82f2-129">For example, if your `tenant_name` is contoso.onmicrosoft.com, set the URL to be `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
10. <span data-ttu-id="a82f2-130">Cliquez sur **提交** (Envoyer).</span><span class="sxs-lookup"><span data-stu-id="a82f2-130">Click **提交** (submit).</span></span>  

## <a name="configure-weibo-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="a82f2-131">Configurer Weibo en tant que fournisseur d’identité dans votre locataire</span><span class="sxs-lookup"><span data-stu-id="a82f2-131">Configure Weibo as an identity provider in your tenant</span></span>
1. <span data-ttu-id="a82f2-132">Suivez ces étapes pour [accéder au panneau de fonctionnalités B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a82f2-132">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="a82f2-133">Dans le panneau de fonctionnalités B2C, cliquez sur **Fournisseurs d’identité**.</span><span class="sxs-lookup"><span data-stu-id="a82f2-133">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="a82f2-134">Cliquez sur **+Ajouter** dans la partie supérieure du panneau.</span><span class="sxs-lookup"><span data-stu-id="a82f2-134">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="a82f2-135">Fournissez un **Nom** convivial pour la configuration de fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="a82f2-135">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="a82f2-136">Par exemple, entrez « Weibo ».</span><span class="sxs-lookup"><span data-stu-id="a82f2-136">For example, enter "Weibo".</span></span>
5. <span data-ttu-id="a82f2-137">Cliquez sur **Type de fournisseur d’identité**, sélectionnez **Weibo**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="a82f2-137">Click **Identity provider type**, select **Weibo**, and click **OK**.</span></span>
6. <span data-ttu-id="a82f2-138">Cliquez sur **Configurer ce fournisseur d’identité**.</span><span class="sxs-lookup"><span data-stu-id="a82f2-138">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="a82f2-139">Entrez la **clé d’application** que vous avez copiée précédemment dans **ID client**.</span><span class="sxs-lookup"><span data-stu-id="a82f2-139">Enter the **App Key** that you copied earlier as the **Client ID**.</span></span>
8. <span data-ttu-id="a82f2-140">Entrez le **secret d’application** que vous avez copié précédemment dans **Secret client**.</span><span class="sxs-lookup"><span data-stu-id="a82f2-140">Enter the **App Secret** that you copied earlier as the **Client Secret**.</span></span>
9. <span data-ttu-id="a82f2-141">Cliquez sur **OK**, puis sur **Créer** pour enregistrer votre configuration Weibo.</span><span class="sxs-lookup"><span data-stu-id="a82f2-141">Click **OK** and then click **Create** to save your Weibo configuration.</span></span>

