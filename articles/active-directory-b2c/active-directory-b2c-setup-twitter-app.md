---
title: "Azure Active Directory B2C : configuration Twitter | Microsoft Docs"
description: "Proposez l’inscription et la connexion à des consommateurs disposant de comptes Twitter dans vos applications sécurisées par Azure Active Directory B2C."
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
ms.openlocfilehash: 82a001dd53cdddcf3b360090f3250af593c96fbb
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-twitter-accounts"></a><span data-ttu-id="bdfee-103">Azure Active Directory B2C : Proposer l’inscription et la connexion à des consommateurs disposant de comptes Twitter</span><span class="sxs-lookup"><span data-stu-id="bdfee-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Twitter accounts</span></span>

> [!NOTE]
> <span data-ttu-id="bdfee-104">Cette fonctionnalité est en préversion.</span><span class="sxs-lookup"><span data-stu-id="bdfee-104">This feature is in preview.</span></span>
> 

## <a name="create-a-twitter-application"></a><span data-ttu-id="bdfee-105">Création d'une application Twitter</span><span class="sxs-lookup"><span data-stu-id="bdfee-105">Create a Twitter application</span></span>
<span data-ttu-id="bdfee-106">Pour utiliser Twitter en tant que fournisseur d’identité dans Azure Active Directory (Azure AD) B2C, vous devez créer une application Twitter et lui fournir les paramètres appropriés.</span><span class="sxs-lookup"><span data-stu-id="bdfee-106">To use Twitter as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Twitter application and supply it with the right parameters.</span></span> <span data-ttu-id="bdfee-107">Pour ce faire, vous devez disposer d’un compte développeur Twitter.</span><span class="sxs-lookup"><span data-stu-id="bdfee-107">You need a Twitter developer account to do this.</span></span> <span data-ttu-id="bdfee-108">Si vous n’en avez pas, vous pouvez en obtenir un à l’adresse [https://dev.twitter.com/](https://dev.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="bdfee-108">If you don’t have one, you can get it at [https://dev.twitter.com/](https://dev.twitter.com/).</span></span>

1. <span data-ttu-id="bdfee-109">Accédez au [site Web des développeurs Twitter](https://dev.twitter.com/) et connectez-vous à l’aide de vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="bdfee-109">Go to the [Twitter developer's website](https://dev.twitter.com/) and sign in with your credentials.</span></span>
2. <span data-ttu-id="bdfee-110">Cliquez sur **My apps** (Mes applications sous **Tools & Support** (Outils et support), puis sur **Create New App** (Créer une application).</span><span class="sxs-lookup"><span data-stu-id="bdfee-110">Click **My apps** under **Tools & Support** and then click **Create New App**.</span></span> 
3. <span data-ttu-id="bdfee-111">Dans le formulaire, indiquez une valeur pour **Name** (Nom), **Description** (Description) et **Website** (Site Web).</span><span class="sxs-lookup"><span data-stu-id="bdfee-111">In the form, provide a value for the **Name**, **Description**, and **Website**.</span></span>
4. <span data-ttu-id="bdfee-112">Dans le champ **Callback URL** (URL de rappel), entrez `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="bdfee-112">For the **Callback URL**, enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`.</span></span> <span data-ttu-id="bdfee-113">Assurez-vous de remplacer **{tenant}** par votre nom de client (par exemple, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="bdfee-113">Make sure to replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span>
5. <span data-ttu-id="bdfee-114">Cochez la case pour accepter le **contrat pour les développeurs** et cliquez sur **Create your Twitter application** (Créer votre application Twitter).</span><span class="sxs-lookup"><span data-stu-id="bdfee-114">Check the box to agree to the **Developer Agreement** and click **Create your Twitter application**.</span></span>
6. <span data-ttu-id="bdfee-115">Une fois l’application créée, cliquez sur **Keys and Access Tokens** (Clés et jetons d’accès).</span><span class="sxs-lookup"><span data-stu-id="bdfee-115">Once the app is created, click **Keys and Access Tokens**.</span></span>
7. <span data-ttu-id="bdfee-116">Copiez les informations de **Consumer Key** (Clé du client) et de **Consumer Secret** (Secret du client).</span><span class="sxs-lookup"><span data-stu-id="bdfee-116">Copy the value of **Consumer Key** and **Consumer Secret**.</span></span> <span data-ttu-id="bdfee-117">Vous aurez besoin de ces deux valeurs pour configurer Twitter en tant que fournisseur d’identité dans votre client.</span><span class="sxs-lookup"><span data-stu-id="bdfee-117">You will need both of them to configure Twitter as an identity provider in your tenant.</span></span>

## <a name="configure-twitter-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="bdfee-118">Configurer Twitter en tant que fournisseur d’identité dans votre locataire</span><span class="sxs-lookup"><span data-stu-id="bdfee-118">Configure Twitter as an identity provider in your tenant</span></span>
1. <span data-ttu-id="bdfee-119">Suivez ces étapes pour [accéder au panneau de fonctionnalités B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="bdfee-119">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="bdfee-120">Dans le panneau de fonctionnalités B2C, cliquez sur **Fournisseurs d’identité**.</span><span class="sxs-lookup"><span data-stu-id="bdfee-120">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="bdfee-121">Cliquez sur **+Ajouter** dans la partie supérieure du panneau.</span><span class="sxs-lookup"><span data-stu-id="bdfee-121">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="bdfee-122">Fournissez un **Nom** convivial pour la configuration de fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="bdfee-122">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="bdfee-123">Par exemple, entrez « Twitter ».</span><span class="sxs-lookup"><span data-stu-id="bdfee-123">For example, enter "Twitter".</span></span>
5. <span data-ttu-id="bdfee-124">Cliquez sur **Identity provider type** (Type de fournisseur d’identité), sélectionnez **Twitter**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="bdfee-124">Click **Identity provider type**, select **Twitter**, and click **OK**.</span></span>
6. <span data-ttu-id="bdfee-125">Cliquez sur **Set up this identity provider** (Configurer ce fournisseur d’identité) et entrez la **clé du client** Twitter pour **l’ID du client** et le **secret du client** Twitter pour le **secret du client**.</span><span class="sxs-lookup"><span data-stu-id="bdfee-125">Click **Set up this identity provider** and enter the Twitter **Consumer Key** for the **Client id** and the Twitter **Consumer Secret** for the **Client secret**.</span></span>
7. <span data-ttu-id="bdfee-126">Cliquez sur **OK**, puis sur **Create** (Créer) pour enregistrer votre configuration Twitter.</span><span class="sxs-lookup"><span data-stu-id="bdfee-126">Click **OK**, and then click **Create** to save your Twitter configuration.</span></span>

