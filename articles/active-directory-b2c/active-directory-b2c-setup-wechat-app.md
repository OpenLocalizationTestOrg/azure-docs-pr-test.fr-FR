---
title: 'Azure Active Directory B2C : Configuration de WeChat | Microsoft Docs'
description: "Proposez l’inscription et la connexion à des consommateurs disposant de comptes WeChat dans vos applications sécurisées par Azure Active Directory B2C."
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
ms.openlocfilehash: a54aec23d951610118246e9f70cdd27752ef39a6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-wechat-accounts"></a><span data-ttu-id="0d57b-103">Azure Active Directory B2C : Proposer l’inscription et la connexion à des consommateurs disposant de comptes WeChat</span><span class="sxs-lookup"><span data-stu-id="0d57b-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with WeChat accounts</span></span>

> [!NOTE]
> <span data-ttu-id="0d57b-104">Cette fonctionnalité est en préversion.</span><span class="sxs-lookup"><span data-stu-id="0d57b-104">This feature is in preview.</span></span>
> 

## <a name="create-a-wechat-application"></a><span data-ttu-id="0d57b-105">Créer une application WeChat</span><span class="sxs-lookup"><span data-stu-id="0d57b-105">Create a WeChat application</span></span>

<span data-ttu-id="0d57b-106">Pour utiliser WeChat en tant que fournisseur d’identité dans Azure Active Directory (Azure AD) B2C, vous devez créer une application WeChat et lui fournir les paramètres appropriés.</span><span class="sxs-lookup"><span data-stu-id="0d57b-106">To use WeChat as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a WeChat application and supply it with the right parameters.</span></span> <span data-ttu-id="0d57b-107">Pour ce faire, vous avez besoin d’un compte WeChat.</span><span class="sxs-lookup"><span data-stu-id="0d57b-107">You need a WeChat account to do this.</span></span> <span data-ttu-id="0d57b-108">Si vous n’en avez pas, vous pouvez en obtenir un en vous inscrivant via une de leurs applications mobiles ou à l’aide de votre numéro QQ.</span><span class="sxs-lookup"><span data-stu-id="0d57b-108">If you don’t have one, you can get one by signing up through one of their mobile apps or by using your QQ number.</span></span> <span data-ttu-id="0d57b-109">Après cela, ouvrez votre compte inscrit auprès du programme de développeurs WeChat.</span><span class="sxs-lookup"><span data-stu-id="0d57b-109">After that, get your account registered with the WeChat developer program.</span></span> <span data-ttu-id="0d57b-110">Pour plus d’informations, consultez la [page suivante](http://kf.qq.com/faq/161220Brem2Q161220uUjERB.html):</span><span class="sxs-lookup"><span data-stu-id="0d57b-110">You can find more information [here](http://kf.qq.com/faq/161220Brem2Q161220uUjERB.html).</span></span>

### <a name="register-a-wechat-application"></a><span data-ttu-id="0d57b-111">Inscrire une application WeChat</span><span class="sxs-lookup"><span data-stu-id="0d57b-111">Register a WeChat application</span></span>

1. <span data-ttu-id="0d57b-112">Accédez à [https://open.weixin.qq.com/](https://open.weixin.qq.com/) et connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="0d57b-112">Go to [https://open.weixin.qq.com/](https://open.weixin.qq.com/) and log in.</span></span>
2. <span data-ttu-id="0d57b-113">Cliquez sur **管理中心** (Centre de gestion).</span><span class="sxs-lookup"><span data-stu-id="0d57b-113">Click on **管理中心** (management center).</span></span>
3. <span data-ttu-id="0d57b-114">Suivez les étapes nécessaires à l’inscription d’une nouvelle application.</span><span class="sxs-lookup"><span data-stu-id="0d57b-114">Follow the necessary steps to register a new application.</span></span>
4. <span data-ttu-id="0d57b-115">Pour **授权回调域** (URL de rappel), entrez `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="0d57b-115">For **授权回调域** (callback URL), enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span></span> <span data-ttu-id="0d57b-116">Par exemple, si votre `tenant_name` est contoso.onmicrosoft.com, définissez l’URL sur `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="0d57b-116">For example, if your `tenant_name` is contoso.onmicrosoft.com, set the URL to be `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
5. <span data-ttu-id="0d57b-117">Recherchez et copiez l’**ID de l’application** et la **clé d’application**.</span><span class="sxs-lookup"><span data-stu-id="0d57b-117">Find and copy the **APP ID** and **APP KEY**.</span></span> <span data-ttu-id="0d57b-118">Vous en aurez besoin ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="0d57b-118">You will need these later.</span></span>

## <a name="configure-wechat-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="0d57b-119">Configurer WeChat en tant que fournisseur d’identité dans votre locataire</span><span class="sxs-lookup"><span data-stu-id="0d57b-119">Configure WeChat as an identity provider in your tenant</span></span>
1. <span data-ttu-id="0d57b-120">Suivez ces étapes pour [accéder au panneau de fonctionnalités B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0d57b-120">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="0d57b-121">Dans le panneau de fonctionnalités B2C, cliquez sur **Fournisseurs d’identité**.</span><span class="sxs-lookup"><span data-stu-id="0d57b-121">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="0d57b-122">Cliquez sur **+Ajouter** dans la partie supérieure du panneau.</span><span class="sxs-lookup"><span data-stu-id="0d57b-122">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="0d57b-123">Fournissez un **Nom** convivial pour la configuration de fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="0d57b-123">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="0d57b-124">Par exemple, entrez « WeChat ».</span><span class="sxs-lookup"><span data-stu-id="0d57b-124">For example, enter "WeChat".</span></span>
5. <span data-ttu-id="0d57b-125">Cliquez sur **Type de fournisseur d’identité**, sélectionnez **WeChat**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="0d57b-125">Click **Identity provider type**, select **WeChat**, and click **OK**.</span></span>
6. <span data-ttu-id="0d57b-126">Cliquez sur **Configurer ce fournisseur d’identité**.</span><span class="sxs-lookup"><span data-stu-id="0d57b-126">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="0d57b-127">Entrez la **clé d’application** que vous avez copiée précédemment dans **ID client**.</span><span class="sxs-lookup"><span data-stu-id="0d57b-127">Enter the **App Key** that you copied earlier as the **Client ID**.</span></span>
8. <span data-ttu-id="0d57b-128">Entrez le **secret d’application** que vous avez copié précédemment dans **Secret client**.</span><span class="sxs-lookup"><span data-stu-id="0d57b-128">Enter the **App Secret** that you copied earlier as the **Client Secret**.</span></span>
9. <span data-ttu-id="0d57b-129">Cliquez sur **OK**, puis sur **Créer** pour enregistrer votre configuration WeChat.</span><span class="sxs-lookup"><span data-stu-id="0d57b-129">Click **OK** and then click **Create** to save your WeChat configuration.</span></span>

