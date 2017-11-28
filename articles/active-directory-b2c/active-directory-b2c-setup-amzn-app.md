---
title: 'Azure Active Directory B2C : configuration Amazon | Microsoft Docs'
description: "Fournir tooconsumers d’abonnement et connectez-vous avec des comptes d’Amazon dans vos applications sont sécurisées par Azure Active Directory B2C."
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
ms.openlocfilehash: 60d7c4b76d9d3e86ed535765329abed07f1e5996
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-amazon-accounts"></a><span data-ttu-id="727c6-103">Azure B2C Active Directory : Fournir tooconsumers d’abonnement et connectez-vous avec les comptes d’Amazon</span><span class="sxs-lookup"><span data-stu-id="727c6-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Amazon accounts</span></span>
## <a name="create-an-amazon-application"></a><span data-ttu-id="727c6-104">Création d’une application Amazon</span><span class="sxs-lookup"><span data-stu-id="727c6-104">Create an Amazon application</span></span>
<span data-ttu-id="727c6-105">toouse Amazon comme fournisseur d’identité dans Azure Active Directory (Azure AD) B2C, vous devez toocreate une application Amazon et lui fournir les paramètres appropriés hello.</span><span class="sxs-lookup"><span data-stu-id="727c6-105">toouse Amazon as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate an Amazon application and supply it with hello right parameters.</span></span> <span data-ttu-id="727c6-106">Vous devez une toodo de compte Amazon cela.</span><span class="sxs-lookup"><span data-stu-id="727c6-106">You need an Amazon account toodo this.</span></span> <span data-ttu-id="727c6-107">Si vous n’en avez pas, vous pouvez en obtenir un à l’adresse [http://www.amazon.com/](http://www.amazon.com/).</span><span class="sxs-lookup"><span data-stu-id="727c6-107">If you don’t have one, you can get it at [http://www.amazon.com/](http://www.amazon.com/).</span></span>

1. <span data-ttu-id="727c6-108">Accédez toohello [Centre pour développeurs Amazon](https://login.amazon.com/) et connectez-vous avec vos informations d’identification du compte Amazon.</span><span class="sxs-lookup"><span data-stu-id="727c6-108">Go toohello [Amazon Developer Center](https://login.amazon.com/) and sign in with your Amazon account credentials.</span></span>
2. <span data-ttu-id="727c6-109">Si vous ne le n'avez pas déjà fait, cliquez sur **s’inscrire**, suivez les étapes d’inscription de développeur hello et acceptez la politique de hello.</span><span class="sxs-lookup"><span data-stu-id="727c6-109">If you have not already done so, click **Sign Up**, follow hello developer registration steps, and accept hello policy.</span></span>
3. <span data-ttu-id="727c6-110">Cliquez sur **Register new application**.</span><span class="sxs-lookup"><span data-stu-id="727c6-110">Click **Register new application**.</span></span>
   
    ![L’inscription d’une nouvelle application sur le site Web de hello Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-new-app.png)
4. <span data-ttu-id="727c6-112">Fournissez les informations relatives à l’application (**Nom**, **Description** et **Privacy Notice URL** (URL de déclaration de confidentialité), puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="727c6-112">Provide application information (**Name**, **Description**, and **Privacy Notice URL**) and click **Save**.</span></span>
   
    ![Fourniture d’informations d’application pour l’inscription d’une nouvelle application sur Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-register-app.png)
5. <span data-ttu-id="727c6-114">Bonjour **paramètres Web** section, copie les valeurs hello de **ID Client** et **clé secrète Client**.</span><span class="sxs-lookup"><span data-stu-id="727c6-114">In hello **Web Settings** section, copy hello values of **Client ID** and **Client Secret**.</span></span> <span data-ttu-id="727c6-115">(Vous devez tooclick hello **afficher le Secret** bouton toosee ce.) Vous avez besoin des deux d'entre eux tooconfigure Amazon comme fournisseur d’identité dans votre client.</span><span class="sxs-lookup"><span data-stu-id="727c6-115">(You need tooclick hello **Show Secret** button toosee this.) You need both of them tooconfigure Amazon as an identity provider in your tenant.</span></span> <span data-ttu-id="727c6-116">Cliquez sur **modifier** bas hello de section de hello.</span><span class="sxs-lookup"><span data-stu-id="727c6-116">Click **Edit** at hello bottom of hello section.</span></span> <span data-ttu-id="727c6-117">**Client Secret** est une information d’identification de sécurité importante.</span><span class="sxs-lookup"><span data-stu-id="727c6-117">**Client Secret** is an important security credential.</span></span>
   
    ![Fourniture de l’ID client et de la clé secrète client pour votre nouvelle application sur Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-client-secret.png)
6. <span data-ttu-id="727c6-119">Entrez `https://login.microsoftonline.com` Bonjour **autorisé les origines JavaScript** champ et `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` Bonjour **autorisé les URL de retour** champ.</span><span class="sxs-lookup"><span data-stu-id="727c6-119">Enter `https://login.microsoftonline.com` in hello **Allowed JavaScript Origins** field and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Allowed Return URLs** field.</span></span> <span data-ttu-id="727c6-120">Remplacez **{tenant}** par votre nom de client (par exemple, contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="727c6-120">Replace **{tenant}** with your tenant's name (for example, contoso.onmicrosoft.com).</span></span> <span data-ttu-id="727c6-121">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="727c6-121">Click **Save**.</span></span> <span data-ttu-id="727c6-122">Hello **{tenant}** valeur respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="727c6-122">hello **{tenant}** value is case-sensitive.</span></span>
   
    ![Fourniture de JavaScript Origins et Return URLs pour votre nouvelle application sur Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-urls.png)

## <a name="configure-amazon-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="727c6-124">Configuration d’Amazon en tant que fournisseur d’identité dans votre client</span><span class="sxs-lookup"><span data-stu-id="727c6-124">Configure Amazon as an identity provider in your tenant</span></span>
1. <span data-ttu-id="727c6-125">Suivez ces étapes trop[accédez Panneau de fonctionnalités toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) sur hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="727c6-125">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="727c6-126">Dans le panneau de fonctionnalités hello B2C, cliquez sur **fournisseurs d’identité**.</span><span class="sxs-lookup"><span data-stu-id="727c6-126">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="727c6-127">Cliquez sur **+ ajouter** haut hello du Panneau de hello.</span><span class="sxs-lookup"><span data-stu-id="727c6-127">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="727c6-128">Fournissez un nom convivial de **nom** pour la configuration du fournisseur d’identité hello.</span><span class="sxs-lookup"><span data-stu-id="727c6-128">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="727c6-129">Par exemple, entrez « Amzn ».</span><span class="sxs-lookup"><span data-stu-id="727c6-129">For example, enter "Amzn".</span></span>
5. <span data-ttu-id="727c6-130">Cliquez sur **Type de fournisseur d’identité**, sélectionnez **Amazon**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="727c6-130">Click **Identity provider type**, select **Amazon**, and click **OK**.</span></span>
6. <span data-ttu-id="727c6-131">Cliquez sur **configurer ce fournisseur d’identité** et entrez hello client et ID de clé secrète client de hello application Amazon que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="727c6-131">Click **Set up this identity provider** and enter hello client ID and client secret of hello Amazon application that you created earlier.</span></span>
7. <span data-ttu-id="727c6-132">Cliquez sur **OK** puis cliquez sur **créer** toosave votre configuration Amazon.</span><span class="sxs-lookup"><span data-stu-id="727c6-132">Click **OK** and then click **Create** toosave your Amazon configuration.</span></span>

