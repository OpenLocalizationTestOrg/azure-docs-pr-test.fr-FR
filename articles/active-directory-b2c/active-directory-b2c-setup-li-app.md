---
title: 'Azure Active Directory B2C : configuration LinkedIn | Microsoft Docs'
description: "Fournir tooconsumers d’abonnement et connectez-vous avec les comptes LinkedIn dans vos applications sont sécurisées par Azure Active Directory B2C"
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
ms.openlocfilehash: 6c5233ef48b24968fd6383f470b5d8a969a78ecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-linkedin-accounts"></a><span data-ttu-id="1193f-103">Azure B2C Active Directory : Fournir LinkedIn comptes tooconsumers d’inscription et de connexion</span><span class="sxs-lookup"><span data-stu-id="1193f-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with LinkedIn accounts</span></span>
## <a name="create-a-linkedin-application"></a><span data-ttu-id="1193f-104">Création d’une application LinkedIn</span><span class="sxs-lookup"><span data-stu-id="1193f-104">Create a LinkedIn application</span></span>
<span data-ttu-id="1193f-105">toouse LinkedIn comme fournisseur d’identité dans Azure Active Directory (Azure AD) B2C, vous devez toocreate une application LinkedIn et lui fournir les paramètres appropriés hello.</span><span class="sxs-lookup"><span data-stu-id="1193f-105">toouse LinkedIn as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a LinkedIn application and supply it with hello right parameters.</span></span> <span data-ttu-id="1193f-106">Vous devez cela un toodo de compte LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="1193f-106">You need a LinkedIn account toodo this.</span></span> <span data-ttu-id="1193f-107">Si vous n’en avez pas, vous pouvez en obtenir un à l’adresse [https://www.linkedin.com/](https://www.linkedin.com/).</span><span class="sxs-lookup"><span data-stu-id="1193f-107">If you don’t have one, you can get it at [https://www.linkedin.com/](https://www.linkedin.com/).</span></span>

1. <span data-ttu-id="1193f-108">Accédez toohello [site Web des développeurs de LinkedIn](https://www.developer.linkedin.com/) et connectez-vous avec vos informations d’identification du compte LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="1193f-108">Go toohello [LinkedIn Developers website](https://www.developer.linkedin.com/) and sign in with your LinkedIn account credentials.</span></span>
2. <span data-ttu-id="1193f-109">Cliquez sur **mes applications** dans hello barre de menus supérieure, puis cliquez sur **créer une Application**.</span><span class="sxs-lookup"><span data-stu-id="1193f-109">Click **My Apps** in hello top menu bar and then click **Create Application**.</span></span>
   
    ![LinkedIn - nouvelle application](./media/active-directory-b2c-setup-li-app/linkedin-new-app.png)
3. <span data-ttu-id="1193f-111">Bonjour **créer une nouvelle Application** forment, renseignez les informations pertinentes hello (**nom de la société**, **nom**, **Description**, **URL Logo de l’application**, **utilisation de l’Application**, **URL du site Web**, **E-mail professionnelles** et **téléphone(bureau)**).</span><span class="sxs-lookup"><span data-stu-id="1193f-111">In hello **Create a New Application** form, fill in hello relevant information (**Company Name**, **Name**, **Description**, **Application Logo URL**, **Application Use**, **Website URL**, **Business Email** and **Business Phone**).</span></span>
4. <span data-ttu-id="1193f-112">Acceptez toohello **LinkedIn API conditions d’utilisation** et cliquez sur **Submit**.</span><span class="sxs-lookup"><span data-stu-id="1193f-112">Agree toohello **LinkedIn API Terms of Use** and click **Submit**.</span></span>
   
    ![LinkedIn - inscription d’application](./media/active-directory-b2c-setup-li-app/linkedin-register-app.png)
5. <span data-ttu-id="1193f-114">Copier les valeurs hello de **ID Client** et **clé secrète Client**.</span><span class="sxs-lookup"><span data-stu-id="1193f-114">Copy hello values of **Client ID** and **Client Secret**.</span></span> <span data-ttu-id="1193f-115">(Vous les trouverez sous **Clés d’authentification**.) Vous devez les deux tooconfigure LinkedIn comme fournisseur d’identité dans votre client.</span><span class="sxs-lookup"><span data-stu-id="1193f-115">(You can find them under **Authentication Keys**.) You will need both of them tooconfigure LinkedIn as an identity provider in your tenant.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="1193f-116">**Client Secret** est une information d’identification de sécurité importante.</span><span class="sxs-lookup"><span data-stu-id="1193f-116">**Client Secret** is an important security credential.</span></span>
   > 
   > 
6. <span data-ttu-id="1193f-117">Entrez `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` Bonjour **URL de redirection autorisés** champ (sous **OAuth 2.0**).</span><span class="sxs-lookup"><span data-stu-id="1193f-117">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Authorized Redirect URLs** field (under **OAuth 2.0**).</span></span> <span data-ttu-id="1193f-118">Remplacez **{tenant}** par votre nom de client (par exemple, contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="1193f-118">Replace **{tenant}** with your tenant's name (for example, contoso.onmicrosoft.com).</span></span> <span data-ttu-id="1193f-119">Cliquez sur **Ajouter**, puis sur **Mettre à jour**.</span><span class="sxs-lookup"><span data-stu-id="1193f-119">Click **Add**, and then click **Update**.</span></span> <span data-ttu-id="1193f-120">Hello **{tenant}** valeur respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="1193f-120">hello **{tenant}** value is case-sensitive.</span></span>
   
    ![LinkedIn - configuration d’application](./media/active-directory-b2c-setup-li-app/linkedin-setup.png)

## <a name="configure-linkedin-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="1193f-122">Configuration de LinkedIn en tant que fournisseur d’identité dans votre client</span><span class="sxs-lookup"><span data-stu-id="1193f-122">Configure LinkedIn as an identity provider in your tenant</span></span>
1. <span data-ttu-id="1193f-123">Suivez ces étapes trop[accédez Panneau de fonctionnalités toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) sur hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1193f-123">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="1193f-124">Dans le panneau de fonctionnalités hello B2C, cliquez sur **fournisseurs d’identité**.</span><span class="sxs-lookup"><span data-stu-id="1193f-124">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="1193f-125">Cliquez sur **+ ajouter** haut hello du Panneau de hello.</span><span class="sxs-lookup"><span data-stu-id="1193f-125">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="1193f-126">Fournissez un nom convivial de **nom** pour la configuration du fournisseur d’identité hello.</span><span class="sxs-lookup"><span data-stu-id="1193f-126">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="1193f-127">Par exemple, entrez « LI ».</span><span class="sxs-lookup"><span data-stu-id="1193f-127">For example, enter "LI".</span></span>
5. <span data-ttu-id="1193f-128">Cliquez sur **Type de fournisseur d’identité**, sélectionnez **LinkedIn**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="1193f-128">Click **Identity provider type**, select **LinkedIn**, and click **OK**.</span></span>
6. <span data-ttu-id="1193f-129">Cliquez sur **configurer ce fournisseur d’identité** et entrez hello client et ID de clé secrète client de hello LinkedIn application que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="1193f-129">Click **Set up this identity provider** and enter hello client ID and client secret of hello LinkedIn application that you created earlier.</span></span>
7. <span data-ttu-id="1193f-130">Cliquez sur **OK** puis cliquez sur **créer** toosave votre configuration LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="1193f-130">Click **OK** and then click **Create** toosave your LinkedIn configuration.</span></span>

