---
title: 'Azure Active Directory B2C : Configuration de WeChat | Microsoft Docs'
description: "Fournir tooconsumers d’abonnement et connectez-vous avec des comptes WeChat dans vos applications sont sécurisées par Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: d2424c66-ba68-4d82-847e-d137683527b0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: 92cc3579d818d2379a503ccc695138b33a34466d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-wechat-accounts"></a><span data-ttu-id="43249-103">Azure B2C Active Directory : Fournissent tooconsumers d’abonnement et connectez-vous avec les comptes WeChat</span><span class="sxs-lookup"><span data-stu-id="43249-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with WeChat accounts</span></span>

> [!NOTE]
> <span data-ttu-id="43249-104">Cette fonctionnalité est en préversion.</span><span class="sxs-lookup"><span data-stu-id="43249-104">This feature is in preview.</span></span>
> 

## <a name="create-a-wechat-application"></a><span data-ttu-id="43249-105">Créer une application WeChat</span><span class="sxs-lookup"><span data-stu-id="43249-105">Create a WeChat application</span></span>

<span data-ttu-id="43249-106">toouse WeChat comme fournisseur d’identité dans Azure Active Directory (Azure AD) B2C, vous devez toocreate une application WeChat et lui fournir les paramètres appropriés hello.</span><span class="sxs-lookup"><span data-stu-id="43249-106">toouse WeChat as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a WeChat application and supply it with hello right parameters.</span></span> <span data-ttu-id="43249-107">Vous devez un toodo de compte WeChat cela.</span><span class="sxs-lookup"><span data-stu-id="43249-107">You need a WeChat account toodo this.</span></span> <span data-ttu-id="43249-108">Si vous n’en avez pas, vous pouvez en obtenir un en vous inscrivant via une de leurs applications mobiles ou à l’aide de votre numéro QQ.</span><span class="sxs-lookup"><span data-stu-id="43249-108">If you don’t have one, you can get one by signing up through one of their mobile apps or by using your QQ number.</span></span> <span data-ttu-id="43249-109">Après cela, obtenir votre compte avec un programme pour développeur WeChat hello.</span><span class="sxs-lookup"><span data-stu-id="43249-109">After that, get your account registered with hello WeChat developer program.</span></span> <span data-ttu-id="43249-110">Pour plus d’informations, consultez la [page suivante](http://kf.qq.com/faq/161220Brem2Q161220uUjERB.html):</span><span class="sxs-lookup"><span data-stu-id="43249-110">You can find more information [here](http://kf.qq.com/faq/161220Brem2Q161220uUjERB.html).</span></span>

### <a name="register-a-wechat-application"></a><span data-ttu-id="43249-111">Inscrire une application WeChat</span><span class="sxs-lookup"><span data-stu-id="43249-111">Register a WeChat application</span></span>

1. <span data-ttu-id="43249-112">Accédez trop[https://open.weixin.qq.com/](https://open.weixin.qq.com/) et connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="43249-112">Go too[https://open.weixin.qq.com/](https://open.weixin.qq.com/) and log in.</span></span>
2. <span data-ttu-id="43249-113">Cliquez sur **管理中心** (Centre de gestion).</span><span class="sxs-lookup"><span data-stu-id="43249-113">Click on **管理中心** (management center).</span></span>
3. <span data-ttu-id="43249-114">Suivez les étapes nécessaires de hello tooregister une nouvelle application.</span><span class="sxs-lookup"><span data-stu-id="43249-114">Follow hello necessary steps tooregister a new application.</span></span>
4. <span data-ttu-id="43249-115">Pour **授权回调域** (URL de rappel), entrez `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="43249-115">For **授权回调域** (callback URL), enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span></span> <span data-ttu-id="43249-116">Par exemple, si votre `tenant_name` est contoso.onmicrosoft.com, jeu hello URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="43249-116">For example, if your `tenant_name` is contoso.onmicrosoft.com, set hello URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
5. <span data-ttu-id="43249-117">Rechercher et copie hello **ID d’application** et **clé application**.</span><span class="sxs-lookup"><span data-stu-id="43249-117">Find and copy hello **APP ID** and **APP KEY**.</span></span> <span data-ttu-id="43249-118">Vous en aurez besoin ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="43249-118">You will need these later.</span></span>

## <a name="configure-wechat-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="43249-119">Configurer WeChat en tant que fournisseur d’identité dans votre locataire</span><span class="sxs-lookup"><span data-stu-id="43249-119">Configure WeChat as an identity provider in your tenant</span></span>
1. <span data-ttu-id="43249-120">Suivez ces étapes trop[accédez Panneau de fonctionnalités toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) sur hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="43249-120">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="43249-121">Dans le panneau de fonctionnalités hello B2C, cliquez sur **fournisseurs d’identité**.</span><span class="sxs-lookup"><span data-stu-id="43249-121">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="43249-122">Cliquez sur **+ ajouter** haut hello du Panneau de hello.</span><span class="sxs-lookup"><span data-stu-id="43249-122">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="43249-123">Fournissez un nom convivial de **nom** pour la configuration du fournisseur d’identité hello.</span><span class="sxs-lookup"><span data-stu-id="43249-123">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="43249-124">Par exemple, entrez « WeChat ».</span><span class="sxs-lookup"><span data-stu-id="43249-124">For example, enter "WeChat".</span></span>
5. <span data-ttu-id="43249-125">Cliquez sur **Type de fournisseur d’identité**, sélectionnez **WeChat**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="43249-125">Click **Identity provider type**, select **WeChat**, and click **OK**.</span></span>
6. <span data-ttu-id="43249-126">Cliquez sur **Configurer ce fournisseur d’identité**.</span><span class="sxs-lookup"><span data-stu-id="43249-126">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="43249-127">Entrez hello **clé application** que vous avez copiée précédemment comme hello **ID Client**.</span><span class="sxs-lookup"><span data-stu-id="43249-127">Enter hello **App Key** that you copied earlier as hello **Client ID**.</span></span>
8. <span data-ttu-id="43249-128">Entrez hello **Secret d’application** que vous avez copiée précédemment comme hello **clé secrète Client**.</span><span class="sxs-lookup"><span data-stu-id="43249-128">Enter hello **App Secret** that you copied earlier as hello **Client Secret**.</span></span>
9. <span data-ttu-id="43249-129">Cliquez sur **OK** puis cliquez sur **créer** toosave votre configuration WeChat.</span><span class="sxs-lookup"><span data-stu-id="43249-129">Click **OK** and then click **Create** toosave your WeChat configuration.</span></span>

