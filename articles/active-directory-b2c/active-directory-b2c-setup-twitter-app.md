---
title: "Azure Active Directory B2C : configuration Twitter | Microsoft Docs"
description: "Fournir tooconsumers d’inscription et de connexion à des comptes de Twitter dans vos applications qui sont sécurisées par Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 579a6841-9329-45b8-a351-da4315a6634e
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/06/2017
ms.author: parakhj
ms.openlocfilehash: 275c5c73fd5e8e5075e77fee942cbc1b5e1586cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-twitter-accounts"></a><span data-ttu-id="410ed-103">Azure B2C Active Directory : Fournir tooconsumers d’abonnement et connectez-vous avec des comptes de Twitter</span><span class="sxs-lookup"><span data-stu-id="410ed-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Twitter accounts</span></span>

> [!NOTE]
> <span data-ttu-id="410ed-104">Cette fonctionnalité est en préversion.</span><span class="sxs-lookup"><span data-stu-id="410ed-104">This feature is in preview.</span></span>
> 

## <a name="create-a-twitter-application"></a><span data-ttu-id="410ed-105">Création d'une application Twitter</span><span class="sxs-lookup"><span data-stu-id="410ed-105">Create a Twitter application</span></span>
<span data-ttu-id="410ed-106">toouse Twitter comme fournisseur d’identité dans Azure Active Directory (Azure AD) B2C, vous devez toocreate une application Twitter et lui fournir les paramètres appropriés hello.</span><span class="sxs-lookup"><span data-stu-id="410ed-106">toouse Twitter as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Twitter application and supply it with hello right parameters.</span></span> <span data-ttu-id="410ed-107">Vous devez cela un toodo de compte de développeur Twitter.</span><span class="sxs-lookup"><span data-stu-id="410ed-107">You need a Twitter developer account toodo this.</span></span> <span data-ttu-id="410ed-108">Si vous n’en avez pas, vous pouvez en obtenir un à l’adresse [https://dev.twitter.com/](https://dev.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="410ed-108">If you don’t have one, you can get it at [https://dev.twitter.com/](https://dev.twitter.com/).</span></span>

1. <span data-ttu-id="410ed-109">Accédez toohello [Twitter le site Web des développeurs](https://dev.twitter.com/) et connectez-vous avec vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="410ed-109">Go toohello [Twitter developer's website](https://dev.twitter.com/) and sign in with your credentials.</span></span>
2. <span data-ttu-id="410ed-110">Cliquez sur **My apps** (Mes applications sous **Tools & Support** (Outils et support), puis sur **Create New App** (Créer une application).</span><span class="sxs-lookup"><span data-stu-id="410ed-110">Click **My apps** under **Tools & Support** and then click **Create New App**.</span></span> 
3. <span data-ttu-id="410ed-111">Dans le formulaire de hello, fournissez une valeur pour hello **nom**, **Description**, et **site Web**.</span><span class="sxs-lookup"><span data-stu-id="410ed-111">In hello form, provide a value for hello **Name**, **Description**, and **Website**.</span></span>
4. <span data-ttu-id="410ed-112">Pourquoi **URL de rappel**, entrez `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="410ed-112">For hello **Callback URL**, enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`.</span></span> <span data-ttu-id="410ed-113">Assurez-vous que tooreplace **{tenant}** avec le nom de votre locataire (par exemple, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="410ed-113">Make sure tooreplace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span>
5. <span data-ttu-id="410ed-114">Vérifiez hello zone tooagree toohello **contrat du développeur** et cliquez sur **créer votre application Twitter**.</span><span class="sxs-lookup"><span data-stu-id="410ed-114">Check hello box tooagree toohello **Developer Agreement** and click **Create your Twitter application**.</span></span>
6. <span data-ttu-id="410ed-115">Une fois l’application hello est créée, cliquez sur **clés et les jetons d’accès**.</span><span class="sxs-lookup"><span data-stu-id="410ed-115">Once hello app is created, click **Keys and Access Tokens**.</span></span>
7. <span data-ttu-id="410ed-116">Copiez la valeur hello **clé de consommateur** et **Secret de consommateur**.</span><span class="sxs-lookup"><span data-stu-id="410ed-116">Copy hello value of **Consumer Key** and **Consumer Secret**.</span></span> <span data-ttu-id="410ed-117">Vous devez les deux tooconfigure Twitter comme fournisseur d’identité dans votre client.</span><span class="sxs-lookup"><span data-stu-id="410ed-117">You will need both of them tooconfigure Twitter as an identity provider in your tenant.</span></span>

## <a name="configure-twitter-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="410ed-118">Configurer Twitter en tant que fournisseur d’identité dans votre locataire</span><span class="sxs-lookup"><span data-stu-id="410ed-118">Configure Twitter as an identity provider in your tenant</span></span>
1. <span data-ttu-id="410ed-119">Suivez ces étapes trop[accédez Panneau de fonctionnalités toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) sur hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="410ed-119">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="410ed-120">Dans le panneau de fonctionnalités hello B2C, cliquez sur **fournisseurs d’identité**.</span><span class="sxs-lookup"><span data-stu-id="410ed-120">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="410ed-121">Cliquez sur **+ ajouter** haut hello du Panneau de hello.</span><span class="sxs-lookup"><span data-stu-id="410ed-121">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="410ed-122">Fournissez un nom convivial de **nom** pour la configuration du fournisseur d’identité hello.</span><span class="sxs-lookup"><span data-stu-id="410ed-122">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="410ed-123">Par exemple, entrez « Twitter ».</span><span class="sxs-lookup"><span data-stu-id="410ed-123">For example, enter "Twitter".</span></span>
5. <span data-ttu-id="410ed-124">Cliquez sur **Identity provider type** (Type de fournisseur d’identité), sélectionnez **Twitter**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="410ed-124">Click **Identity provider type**, select **Twitter**, and click **OK**.</span></span>
6. <span data-ttu-id="410ed-125">Cliquez sur **configurer ce fournisseur d’identité** et entrez hello Twitter **clé de consommateur** pour hello **id Client** et hello Twitter **Secret de consommateur**pour hello **clé secrète Client**.</span><span class="sxs-lookup"><span data-stu-id="410ed-125">Click **Set up this identity provider** and enter hello Twitter **Consumer Key** for hello **Client id** and hello Twitter **Consumer Secret** for hello **Client secret**.</span></span>
7. <span data-ttu-id="410ed-126">Cliquez sur **OK**, puis cliquez sur **créer** toosave votre configuration Twitter.</span><span class="sxs-lookup"><span data-stu-id="410ed-126">Click **OK**, and then click **Create** toosave your Twitter configuration.</span></span>

