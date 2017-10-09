---
title: 'Azure Active Directory B2C : configuration Weibo | Microsoft Docs'
description: "Fournir tooconsumers d’abonnement et connectez-vous avec des comptes Weibo dans vos applications sont sécurisées par Azure Active Directory B2C."
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
ms.openlocfilehash: c0648620f318046c1d9d24feb92a0c5f19c6a91a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-weibo-accounts"></a><span data-ttu-id="d5988-103">Azure B2C Active Directory : Fournissent tooconsumers d’abonnement et connectez-vous avec les comptes Weibo</span><span class="sxs-lookup"><span data-stu-id="d5988-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Weibo accounts</span></span>

> [!NOTE]
> <span data-ttu-id="d5988-104">Cette fonctionnalité est en préversion.</span><span class="sxs-lookup"><span data-stu-id="d5988-104">This feature is in preview.</span></span> <span data-ttu-id="d5988-105">N’utilisez pas ce fournisseur d’identité dans votre environnement de production.</span><span class="sxs-lookup"><span data-stu-id="d5988-105">Do not use this identity provider in your production environment.</span></span>
> 

## <a name="create-a-weibo-application"></a><span data-ttu-id="d5988-106">Créer une application Weibo</span><span class="sxs-lookup"><span data-stu-id="d5988-106">Create a Weibo application</span></span>

<span data-ttu-id="d5988-107">toouse Weibo comme fournisseur d’identité dans Azure Active Directory (Azure AD) B2C, vous devez toocreate une application Weibo et lui fournir les paramètres appropriés hello.</span><span class="sxs-lookup"><span data-stu-id="d5988-107">toouse Weibo as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Weibo application and supply it with hello right parameters.</span></span> <span data-ttu-id="d5988-108">Vous devez un toodo de compte Weibo cela.</span><span class="sxs-lookup"><span data-stu-id="d5988-108">You need a Weibo account toodo this.</span></span> <span data-ttu-id="d5988-109">Si vous n’en avez pas, vous pouvez en obtenir un à l’adresse [http://weibo.com/signup/signup.php?lang=en-us](http://weibo.com/signup/signup.php?lang=en-us).</span><span class="sxs-lookup"><span data-stu-id="d5988-109">If you don’t have one, you can get one at [http://weibo.com/signup/signup.php?lang=en-us](http://weibo.com/signup/signup.php?lang=en-us).</span></span>

### <a name="register-for-hello-weibo-developer-program"></a><span data-ttu-id="d5988-110">Inscrivez-vous au programme pour développeur hello Weibo</span><span class="sxs-lookup"><span data-stu-id="d5988-110">Register for hello Weibo developer program</span></span>

1. <span data-ttu-id="d5988-111">Accédez toohello [portail des développeurs Weibo](http://open.weibo.com/) et connectez-vous avec vos informations d’identification du compte Weibo.</span><span class="sxs-lookup"><span data-stu-id="d5988-111">Go toohello [Weibo developer portal](http://open.weibo.com/) and sign in with your Weibo account credentials.</span></span>
2. <span data-ttu-id="d5988-112">Une fois connecté, cliquez sur votre nom d’affichage dans l’angle supérieur droit de hello.</span><span class="sxs-lookup"><span data-stu-id="d5988-112">After signing in, click on your display name in hello top-right corner.</span></span>
3. <span data-ttu-id="d5988-113">Dans la liste déroulante de hello, sélectionnez**编辑开发者信息**(informations destinées aux développeurs de modification).</span><span class="sxs-lookup"><span data-stu-id="d5988-113">In hello dropdown, select **编辑开发者信息** (edit developer information).</span></span>
4. <span data-ttu-id="d5988-114">Entrez les informations de hello requis dans le formulaire de hello et cliquez sur**提交**(envoyer).</span><span class="sxs-lookup"><span data-stu-id="d5988-114">Enter hello required information into hello form and click **提交** (submit).</span></span>
5. <span data-ttu-id="d5988-115">Terminer le processus de vérification du courrier électronique hello.</span><span class="sxs-lookup"><span data-stu-id="d5988-115">Complete hello email verification process.</span></span>
6. <span data-ttu-id="d5988-116">Accédez toohello [page de vérification d’identité](http://open.weibo.com/developers/identity/edit).</span><span class="sxs-lookup"><span data-stu-id="d5988-116">Go toohello [identity verification page](http://open.weibo.com/developers/identity/edit).</span></span>
7. <span data-ttu-id="d5988-117">Entrez les informations de hello requis dans le formulaire de hello et cliquez sur**提交**(envoyer).</span><span class="sxs-lookup"><span data-stu-id="d5988-117">Enter hello required information into hello form and click **提交** (submit).</span></span>

### <a name="register-a-weibo-application"></a><span data-ttu-id="d5988-118">Inscrire une application Weibo</span><span class="sxs-lookup"><span data-stu-id="d5988-118">Register a Weibo application</span></span>

1. <span data-ttu-id="d5988-119">Accédez toohello [nouvelle page de l’inscription d’application Weibo](http://open.weibo.com/apps/new).</span><span class="sxs-lookup"><span data-stu-id="d5988-119">Go toohello [new Weibo app registration page](http://open.weibo.com/apps/new).</span></span>
2. <span data-ttu-id="d5988-120">Entrez les informations d’application nécessaire hello.</span><span class="sxs-lookup"><span data-stu-id="d5988-120">Enter hello necessary application information.</span></span>
3. <span data-ttu-id="d5988-121">Cliquez sur **创建** (Créer).</span><span class="sxs-lookup"><span data-stu-id="d5988-121">Click **创建** (create).</span></span>
4. <span data-ttu-id="d5988-122">Copier les valeurs hello de **clé application** et **Secret d’application**.</span><span class="sxs-lookup"><span data-stu-id="d5988-122">Copy hello values of **App Key** and **App Secret**.</span></span> <span data-ttu-id="d5988-123">Vous en aurez besoin ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="d5988-123">You will need this later.</span></span>
5. <span data-ttu-id="d5988-124">Télécharger les photos de hello requis et entrez les informations nécessaires hello.</span><span class="sxs-lookup"><span data-stu-id="d5988-124">Upload hello required photos and enter hello necessary information.</span></span>
6. <span data-ttu-id="d5988-125">Cliquez sur **保存以上信息** (Enregistrer).</span><span class="sxs-lookup"><span data-stu-id="d5988-125">Click **保存以上信息** (save).</span></span>
7. <span data-ttu-id="d5988-126">Cliquez sur **高级信息** (Informations avancées).</span><span class="sxs-lookup"><span data-stu-id="d5988-126">Click **高级信息** (advanced information).</span></span>
8. <span data-ttu-id="d5988-127">Cliquez sur**编辑**(modifier) le champ toohello suivant pour OAuth2.0**授权设置**(URL de redirection).</span><span class="sxs-lookup"><span data-stu-id="d5988-127">Click **编辑** (edit) next toohello field for OAuth2.0 **授权设置** (redirect URL).</span></span>
9. <span data-ttu-id="d5988-128">Entrez `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp` pour OAuth2.0 **授权设置** (URL de redirection).</span><span class="sxs-lookup"><span data-stu-id="d5988-128">Enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp` for OAuth2.0 **授权设置** (redirect URL).</span></span> <span data-ttu-id="d5988-129">Par exemple, si votre `tenant_name` est contoso.onmicrosoft.com, jeu hello URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="d5988-129">For example, if your `tenant_name` is contoso.onmicrosoft.com, set hello URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
10. <span data-ttu-id="d5988-130">Cliquez sur **提交** (Envoyer).</span><span class="sxs-lookup"><span data-stu-id="d5988-130">Click **提交** (submit).</span></span>  

## <a name="configure-weibo-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="d5988-131">Configurer Weibo en tant que fournisseur d’identité dans votre locataire</span><span class="sxs-lookup"><span data-stu-id="d5988-131">Configure Weibo as an identity provider in your tenant</span></span>
1. <span data-ttu-id="d5988-132">Suivez ces étapes trop[accédez Panneau de fonctionnalités toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) sur hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d5988-132">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="d5988-133">Dans le panneau de fonctionnalités hello B2C, cliquez sur **fournisseurs d’identité**.</span><span class="sxs-lookup"><span data-stu-id="d5988-133">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="d5988-134">Cliquez sur **+ ajouter** haut hello du Panneau de hello.</span><span class="sxs-lookup"><span data-stu-id="d5988-134">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="d5988-135">Fournissez un nom convivial de **nom** pour la configuration du fournisseur d’identité hello.</span><span class="sxs-lookup"><span data-stu-id="d5988-135">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="d5988-136">Par exemple, entrez « Weibo ».</span><span class="sxs-lookup"><span data-stu-id="d5988-136">For example, enter "Weibo".</span></span>
5. <span data-ttu-id="d5988-137">Cliquez sur **Type de fournisseur d’identité**, sélectionnez **Weibo**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="d5988-137">Click **Identity provider type**, select **Weibo**, and click **OK**.</span></span>
6. <span data-ttu-id="d5988-138">Cliquez sur **Configurer ce fournisseur d’identité**.</span><span class="sxs-lookup"><span data-stu-id="d5988-138">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="d5988-139">Entrez hello **clé application** que vous avez copiée précédemment comme hello **ID Client**.</span><span class="sxs-lookup"><span data-stu-id="d5988-139">Enter hello **App Key** that you copied earlier as hello **Client ID**.</span></span>
8. <span data-ttu-id="d5988-140">Entrez hello **Secret d’application** que vous avez copiée précédemment comme hello **clé secrète Client**.</span><span class="sxs-lookup"><span data-stu-id="d5988-140">Enter hello **App Secret** that you copied earlier as hello **Client Secret**.</span></span>
9. <span data-ttu-id="d5988-141">Cliquez sur **OK** puis cliquez sur **créer** toosave votre configuration Weibo.</span><span class="sxs-lookup"><span data-stu-id="d5988-141">Click **OK** and then click **Create** toosave your Weibo configuration.</span></span>

