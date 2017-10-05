---
title: 'Azure Active Directory B2C : configuration Amazon | Microsoft Docs'
description: "Fourniture d’inscription et de connexion à des consommateurs disposant de comptes Amazon dans vos applications sécurisées par Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 77c099bb-a005-4d75-87f9-f61e3de48725
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: dcc97e1b7f6287bd7692c52bf068950065a26572
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-amazon-accounts"></a><span data-ttu-id="1c097-103">Azure Active Directory B2C : fourniture d’inscription et de connexion à des consommateurs disposant de comptes Amazon</span><span class="sxs-lookup"><span data-stu-id="1c097-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Amazon accounts</span></span>
## <a name="create-an-amazon-application"></a><span data-ttu-id="1c097-104">Création d’une application Amazon</span><span class="sxs-lookup"><span data-stu-id="1c097-104">Create an Amazon application</span></span>
<span data-ttu-id="1c097-105">Pour utiliser Amazon en tant que fournisseur d’identité dans Azure Active Directory (Azure AD) B2C, vous devez créer une application Amazon et lui fournir les paramètres appropriés.</span><span class="sxs-lookup"><span data-stu-id="1c097-105">To use Amazon as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create an Amazon application and supply it with the right parameters.</span></span> <span data-ttu-id="1c097-106">Pour ce faire, vous avez besoin d’un compte Amazon.</span><span class="sxs-lookup"><span data-stu-id="1c097-106">You need an Amazon account to do this.</span></span> <span data-ttu-id="1c097-107">Si vous n’en avez pas, vous pouvez en obtenir un à l’adresse [http://www.amazon.com/](http://www.amazon.com/).</span><span class="sxs-lookup"><span data-stu-id="1c097-107">If you don’t have one, you can get it at [http://www.amazon.com/](http://www.amazon.com/).</span></span>

1. <span data-ttu-id="1c097-108">Accédez au [centre des développeurs Amazon](https://login.amazon.com/) et connectez-vous avec les informations d’identification de votre compte Amazon.</span><span class="sxs-lookup"><span data-stu-id="1c097-108">Go to the [Amazon Developer Center](https://login.amazon.com/) and sign in with your Amazon account credentials.</span></span>
2. <span data-ttu-id="1c097-109">Si ce n’est déjà fait, cliquez sur **Sign Up**, suivez la procédure d’inscription pour développeur et acceptez la politique d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="1c097-109">If you have not already done so, click **Sign Up**, follow the developer registration steps, and accept the policy.</span></span>
3. <span data-ttu-id="1c097-110">Cliquez sur **Register new application**.</span><span class="sxs-lookup"><span data-stu-id="1c097-110">Click **Register new application**.</span></span>
   
    ![Inscription d’une nouvelle application sur le site Web d’Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-new-app.png)
4. <span data-ttu-id="1c097-112">Fournissez les informations relatives à l’application (**Nom**, **Description** et **Privacy Notice URL** (URL de déclaration de confidentialité), puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="1c097-112">Provide application information (**Name**, **Description**, and **Privacy Notice URL**) and click **Save**.</span></span>
   
    ![Fourniture d’informations d’application pour l’inscription d’une nouvelle application sur Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-register-app.png)
5. <span data-ttu-id="1c097-114">Dans la section **Paramètres web**, copiez les valeurs **ID client** et **Clé secrète client**.</span><span class="sxs-lookup"><span data-stu-id="1c097-114">In the **Web Settings** section, copy the values of **Client ID** and **Client Secret**.</span></span> <span data-ttu-id="1c097-115">(Vous devez au préalable cliquer sur le bouton **Show Secret** (Afficher la clé secrète client).) Vous avez besoin de ces deux valeurs pour configurer Amazon en tant que fournisseur d’identité dans votre client.</span><span class="sxs-lookup"><span data-stu-id="1c097-115">(You need to click the **Show Secret** button to see this.) You need both of them to configure Amazon as an identity provider in your tenant.</span></span> <span data-ttu-id="1c097-116">Cliquez sur **Modifier** au bas de la section.</span><span class="sxs-lookup"><span data-stu-id="1c097-116">Click **Edit** at the bottom of the section.</span></span> <span data-ttu-id="1c097-117">**Client Secret** est une information d’identification de sécurité importante.</span><span class="sxs-lookup"><span data-stu-id="1c097-117">**Client Secret** is an important security credential.</span></span>
   
    ![Fourniture de l’ID client et de la clé secrète client pour votre nouvelle application sur Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-client-secret.png)
6. <span data-ttu-id="1c097-119">Entrez `https://login.microsoftonline.com` dans le champ **Origines JavaScript autorisées** et `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` dans le champ **Allowed Return URLs** (URL de retour autorisées).</span><span class="sxs-lookup"><span data-stu-id="1c097-119">Enter `https://login.microsoftonline.com` in the **Allowed JavaScript Origins** field and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Allowed Return URLs** field.</span></span> <span data-ttu-id="1c097-120">Remplacez **{tenant}** par votre nom de client (par exemple, contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="1c097-120">Replace **{tenant}** with your tenant's name (for example, contoso.onmicrosoft.com).</span></span> <span data-ttu-id="1c097-121">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="1c097-121">Click **Save**.</span></span> <span data-ttu-id="1c097-122">La valeur **{tenant}** respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="1c097-122">The **{tenant}** value is case-sensitive.</span></span>
   
    ![Fourniture de JavaScript Origins et Return URLs pour votre nouvelle application sur Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-urls.png)

## <a name="configure-amazon-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="1c097-124">Configuration d’Amazon en tant que fournisseur d’identité dans votre client</span><span class="sxs-lookup"><span data-stu-id="1c097-124">Configure Amazon as an identity provider in your tenant</span></span>
1. <span data-ttu-id="1c097-125">Suivez ces étapes pour [accéder au panneau de fonctionnalités B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1c097-125">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="1c097-126">Dans le panneau de fonctionnalités B2C, cliquez sur **Fournisseurs d’identité**.</span><span class="sxs-lookup"><span data-stu-id="1c097-126">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="1c097-127">Cliquez sur **+Ajouter** dans la partie supérieure du panneau.</span><span class="sxs-lookup"><span data-stu-id="1c097-127">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="1c097-128">Fournissez un **Nom** convivial pour la configuration de fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="1c097-128">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="1c097-129">Par exemple, entrez « Amzn ».</span><span class="sxs-lookup"><span data-stu-id="1c097-129">For example, enter "Amzn".</span></span>
5. <span data-ttu-id="1c097-130">Cliquez sur **Type de fournisseur d’identité**, sélectionnez **Amazon**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="1c097-130">Click **Identity provider type**, select **Amazon**, and click **OK**.</span></span>
6. <span data-ttu-id="1c097-131">Cliquez sur **Configurer ce fournisseur d’identité** , puis entrez l’ID client et la clé secrète client de l’application Amazon que vous avez créée précédemment.</span><span class="sxs-lookup"><span data-stu-id="1c097-131">Click **Set up this identity provider** and enter the client ID and client secret of the Amazon application that you created earlier.</span></span>
7. <span data-ttu-id="1c097-132">Cliquez sur **OK**, puis sur **Créer** pour enregistrer votre configuration Amazon.</span><span class="sxs-lookup"><span data-stu-id="1c097-132">Click **OK** and then click **Create** to save your Amazon configuration.</span></span>

