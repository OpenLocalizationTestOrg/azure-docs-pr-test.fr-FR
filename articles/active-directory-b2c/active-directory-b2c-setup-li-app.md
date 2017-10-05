---
title: 'Azure Active Directory B2C : configuration LinkedIn | Microsoft Docs'
description: "Fourniture d’inscription et de connexion à des consommateurs disposant de comptes LinkedIn dans vos applications sécurisées par Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: fa51a16b-9ce9-4e27-9eff-0869b4c4f0ef
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 1a6c4b19261aa34e668554ccad2b6340cddf9bf5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-linkedin-accounts"></a><span data-ttu-id="2646a-103">Azure Active Directory B2C : fourniture d’inscription et de connexion à des consommateurs disposant de comptes LinkedIn</span><span class="sxs-lookup"><span data-stu-id="2646a-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with LinkedIn accounts</span></span>
## <a name="create-a-linkedin-application"></a><span data-ttu-id="2646a-104">Création d’une application LinkedIn</span><span class="sxs-lookup"><span data-stu-id="2646a-104">Create a LinkedIn application</span></span>
<span data-ttu-id="2646a-105">Pour utiliser LinkedIn en tant que fournisseur d’identité dans Azure Active Directory (Azure AD) B2C, vous devez créer une application LinkedIn et lui fournir les paramètres appropriés.</span><span class="sxs-lookup"><span data-stu-id="2646a-105">To use LinkedIn as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a LinkedIn application and supply it with the right parameters.</span></span> <span data-ttu-id="2646a-106">Pour ce faire, vous avez besoin d’un compte LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="2646a-106">You need a LinkedIn account to do this.</span></span> <span data-ttu-id="2646a-107">Si vous n’en avez pas, vous pouvez en obtenir un à l’adresse [https://www.linkedin.com/](https://www.linkedin.com/).</span><span class="sxs-lookup"><span data-stu-id="2646a-107">If you don’t have one, you can get it at [https://www.linkedin.com/](https://www.linkedin.com/).</span></span>

1. <span data-ttu-id="2646a-108">Accédez au site web [Développeurs LinkedIn](https://www.developer.linkedin.com/) et connectez-vous à l’aide des informations d’identification de votre compte LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="2646a-108">Go to the [LinkedIn Developers website](https://www.developer.linkedin.com/) and sign in with your LinkedIn account credentials.</span></span>
2. <span data-ttu-id="2646a-109">Cliquez sur **Mes applications** dans la barre de menu, puis sur **Créer une application**.</span><span class="sxs-lookup"><span data-stu-id="2646a-109">Click **My Apps** in the top menu bar and then click **Create Application**.</span></span>
   
    ![LinkedIn - nouvelle application](./media/active-directory-b2c-setup-li-app/linkedin-new-app.png)
3. <span data-ttu-id="2646a-111">Dans le formulaire **Créer une nouvelle application**, entrez les informations pertinentes (**Nom de l’entreprise**, **Nom**, **Description**, **Application Logo URL** (URL du logo de l’application), **Application Use** (Utilisation de l’application), **URL du site Web**, **Adresse de messagerie professionnelle** et **Numéro de téléphone professionnel**).</span><span class="sxs-lookup"><span data-stu-id="2646a-111">In the **Create a New Application** form, fill in the relevant information (**Company Name**, **Name**, **Description**, **Application Logo URL**, **Application Use**, **Website URL**, **Business Email** and **Business Phone**).</span></span>
4. <span data-ttu-id="2646a-112">Acceptez les **conditions d’utilisation de l’API LinkedIn**, puis cliquez sur **Envoyer**.</span><span class="sxs-lookup"><span data-stu-id="2646a-112">Agree to the **LinkedIn API Terms of Use** and click **Submit**.</span></span>
   
    ![LinkedIn - inscription d’application](./media/active-directory-b2c-setup-li-app/linkedin-register-app.png)
5. <span data-ttu-id="2646a-114">Copiez les valeurs de **ID client** et **Clé secrète client**.</span><span class="sxs-lookup"><span data-stu-id="2646a-114">Copy the values of **Client ID** and **Client Secret**.</span></span> <span data-ttu-id="2646a-115">(Vous les trouverez sous **Clés d’authentification**.) Vous aurez besoin de ces deux valeurs pour configurer LinkedIn en tant que fournisseur d’identité dans votre client.</span><span class="sxs-lookup"><span data-stu-id="2646a-115">(You can find them under **Authentication Keys**.) You will need both of them to configure LinkedIn as an identity provider in your tenant.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="2646a-116">**Client Secret** est une information d’identification de sécurité importante.</span><span class="sxs-lookup"><span data-stu-id="2646a-116">**Client Secret** is an important security credential.</span></span>
   > 
   > 
6. <span data-ttu-id="2646a-117">Entrez `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` dans le champ **URL de redirection autorisées** (sous **OAuth 2.0**).</span><span class="sxs-lookup"><span data-stu-id="2646a-117">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Authorized Redirect URLs** field (under **OAuth 2.0**).</span></span> <span data-ttu-id="2646a-118">Remplacez **{tenant}** par votre nom de client (par exemple, contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="2646a-118">Replace **{tenant}** with your tenant's name (for example, contoso.onmicrosoft.com).</span></span> <span data-ttu-id="2646a-119">Cliquez sur **Ajouter**, puis sur **Mettre à jour**.</span><span class="sxs-lookup"><span data-stu-id="2646a-119">Click **Add**, and then click **Update**.</span></span> <span data-ttu-id="2646a-120">La valeur **{tenant}** respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="2646a-120">The **{tenant}** value is case-sensitive.</span></span>
   
    ![LinkedIn - configuration d’application](./media/active-directory-b2c-setup-li-app/linkedin-setup.png)

## <a name="configure-linkedin-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="2646a-122">Configuration de LinkedIn en tant que fournisseur d’identité dans votre client</span><span class="sxs-lookup"><span data-stu-id="2646a-122">Configure LinkedIn as an identity provider in your tenant</span></span>
1. <span data-ttu-id="2646a-123">Suivez ces étapes pour [accéder au panneau de fonctionnalités B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2646a-123">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="2646a-124">Dans le panneau de fonctionnalités B2C, cliquez sur **Fournisseurs d’identité**.</span><span class="sxs-lookup"><span data-stu-id="2646a-124">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="2646a-125">Cliquez sur **+Ajouter** dans la partie supérieure du panneau.</span><span class="sxs-lookup"><span data-stu-id="2646a-125">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="2646a-126">Fournissez un **Nom** convivial pour la configuration de fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="2646a-126">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="2646a-127">Par exemple, entrez « LI ».</span><span class="sxs-lookup"><span data-stu-id="2646a-127">For example, enter "LI".</span></span>
5. <span data-ttu-id="2646a-128">Cliquez sur **Type de fournisseur d’identité**, sélectionnez **LinkedIn**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="2646a-128">Click **Identity provider type**, select **LinkedIn**, and click **OK**.</span></span>
6. <span data-ttu-id="2646a-129">Cliquez sur **Configurer ce fournisseur d’identité** , puis entrez l’ID client et la clé secrète client de l’application LinkedIn que vous avez créée précédemment.</span><span class="sxs-lookup"><span data-stu-id="2646a-129">Click **Set up this identity provider** and enter the client ID and client secret of the LinkedIn application that you created earlier.</span></span>
7. <span data-ttu-id="2646a-130">Cliquez sur **OK**, puis sur **Créer** pour enregistrer votre configuration LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="2646a-130">Click **OK** and then click **Create** to save your LinkedIn configuration.</span></span>

