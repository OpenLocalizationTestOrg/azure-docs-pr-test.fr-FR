---
title: "Azure Active Directory B2C : attributs personnalisés | Microsoft Docs"
description: "Utilisation d’attributs personnalisés dans Azure Active Directory B2C pour collecter des informations sur vos consommateurs"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 055ffb0a-197b-4716-8dad-1fd8a01e174f
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 356aaeff3a78fc7b682d621e8e0de9312582b2fe
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-use-custom-attributes-to-collect-information-about-your-consumers"></a><span data-ttu-id="50983-103">Azure Active Directory B2C : utilisation d’attributs personnalisés pour recueillir des informations sur vos consommateurs</span><span class="sxs-lookup"><span data-stu-id="50983-103">Azure Active Directory B2C: Use custom attributes to collect information about your consumers</span></span>
<span data-ttu-id="50983-104">Votre annuaire Azure Active Directory (Azure AD) B2C est fourni avec un ensemble intégré d’informations (attributs) : le prénom, le nom, la ville, le code postal, et d’autres attributs.</span><span class="sxs-lookup"><span data-stu-id="50983-104">Your Azure Active Directory (Azure AD) B2C directory comes with a built-in set of information (attributes): Given Name, Surname, City, Postal Code, and other attributes.</span></span> <span data-ttu-id="50983-105">Cependant, toute application accessible aux consommateurs a des exigences uniques sur les attributs à recueillir auprès des consommateurs.</span><span class="sxs-lookup"><span data-stu-id="50983-105">However, every consumer-facing application has unique requirements on what attributes to gather from consumers.</span></span> <span data-ttu-id="50983-106">Avec Azure AD B2C, vous pouvez étendre l’ensemble d’attributs stockés sur chaque compte client.</span><span class="sxs-lookup"><span data-stu-id="50983-106">With Azure AD B2C, you can extend the set of attributes stored on each consumer account.</span></span> <span data-ttu-id="50983-107">Vous pouvez créer des attributs personnalisés sur le [portail Azure](https://portal.azure.com/) et les utiliser dans vos stratégies d’abonnement, comme illustré ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="50983-107">You can create custom attributes on the [Azure portal](https://portal.azure.com/) and use it in your sign-up policies, as shown below.</span></span> <span data-ttu-id="50983-108">Vous pouvez également lire et écrire ces attributs à l’aide de [l’API Azure AD Graph](active-directory-b2c-devquickstarts-graph-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="50983-108">You can also read and write these attributes by using the [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).</span></span>

> [!NOTE]
> <span data-ttu-id="50983-109">Les attributs personnalisés utilisent les [Extensions de schéma de répertoire de l’API Azure AD Graph](https://msdn.microsoft.com/library/azure/dn720459.aspx).</span><span class="sxs-lookup"><span data-stu-id="50983-109">Custom attributes use [Azure AD Graph API Directory Schema Extensions](https://msdn.microsoft.com/library/azure/dn720459.aspx).</span></span>
> 
> 

## <a name="create-a-custom-attribute"></a><span data-ttu-id="50983-110">Création d’un attribut personnalisé</span><span class="sxs-lookup"><span data-stu-id="50983-110">Create a custom attribute</span></span>
1. <span data-ttu-id="50983-111">[Suivez ces étapes pour accéder au panneau de fonctionnalités B2C sur le portail Azure](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span><span class="sxs-lookup"><span data-stu-id="50983-111">[Follow these steps to navigate to the B2C features blade on the Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="50983-112">Cliquez sur **Attributs utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="50983-112">Click **User attributes**.</span></span>
3. <span data-ttu-id="50983-113">Cliquez sur **+Ajouter** dans la partie supérieure du panneau.</span><span class="sxs-lookup"><span data-stu-id="50983-113">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="50983-114">Fournissez un **nom** pour l’attribut personnalisé (par exemple, « ShoeSize ») et, éventuellement, une **description**.</span><span class="sxs-lookup"><span data-stu-id="50983-114">Provide a **Name** for the custom attribute (for example, "ShoeSize") and optionally, a **Description**.</span></span> <span data-ttu-id="50983-115">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="50983-115">Click **Create**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="50983-116">Actuellement, seul le **Type de données** « String » est disponible.</span><span class="sxs-lookup"><span data-stu-id="50983-116">Only the "String" **Data Type** is currently available.</span></span>
   > 
   > 

<span data-ttu-id="50983-117">L’attribut personnalisé est actuellement disponible dans la liste des **attributs utilisateur**, et pour une utilisation dans vos stratégies d’inscription.</span><span class="sxs-lookup"><span data-stu-id="50983-117">The custom attribute is now available in the list of **User attributes**, and for use in your sign-up policies.</span></span>

## <a name="use-a-custom-attribute-in-your-sign-up-policy"></a><span data-ttu-id="50983-118">Utilisation d’un attribut personnalisé dans votre stratégie d’inscription</span><span class="sxs-lookup"><span data-stu-id="50983-118">Use a custom attribute in your sign-up policy</span></span>
1. <span data-ttu-id="50983-119">[Suivez ces étapes pour accéder au panneau de fonctionnalités B2C sur le portail Azure](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span><span class="sxs-lookup"><span data-stu-id="50983-119">[Follow these steps to navigate to the B2C features blade on the Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="50983-120">Cliquez sur **Stratégies d'inscription**.</span><span class="sxs-lookup"><span data-stu-id="50983-120">Click **Sign-up policies**.</span></span>
3. <span data-ttu-id="50983-121">Ouvrez votre stratégie d’inscription (par exemple, « B2C_1_SiUp ») en cliquant dessus.</span><span class="sxs-lookup"><span data-stu-id="50983-121">Click your sign-up policy (for example, "B2C_1_SiUp") to open it.</span></span> <span data-ttu-id="50983-122">Cliquez sur **Modifier** dans la partie supérieure du panneau.</span><span class="sxs-lookup"><span data-stu-id="50983-122">Click **Edit** at the top of the blade.</span></span>
4. <span data-ttu-id="50983-123">Cliquez sur **Attributs d’inscription** , puis sélectionnez l’attribut personnalisé (par exemple, « ShoeSize »).</span><span class="sxs-lookup"><span data-stu-id="50983-123">Click **Sign-up attributes** and select the custom attribute (for example, "ShoeSize").</span></span> <span data-ttu-id="50983-124">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="50983-124">Click **OK**.</span></span>
5. <span data-ttu-id="50983-125">Cliquez sur **revendications d’applications** , puis sélectionnez l’attribut personnalisé.</span><span class="sxs-lookup"><span data-stu-id="50983-125">Click **Application claims** and select the custom attribute.</span></span> <span data-ttu-id="50983-126">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="50983-126">Click **OK**.</span></span>
6. <span data-ttu-id="50983-127">Cliquez sur **Enregistrer** dans la partie supérieure du panneau.</span><span class="sxs-lookup"><span data-stu-id="50983-127">Click **Save** at the top of the blade.</span></span>

<span data-ttu-id="50983-128">La fonctionnalité « Exécuter maintenant » de la stratégie permet de vérifier l’expérience utilisateur.</span><span class="sxs-lookup"><span data-stu-id="50983-128">You can use the "Run now" feature on the policy to verify the consumer experience.</span></span> <span data-ttu-id="50983-129">Vous devez maintenant voir « ShoeSize » dans la liste d’attributs collectés lors de l’inscription du consommateur, et le voir dans le jeton retourné à votre application.</span><span class="sxs-lookup"><span data-stu-id="50983-129">You should now see "ShoeSize" in the list of attributes collected during consumer sign-up, and see it in the token sent back to your application.</span></span>

## <a name="notes"></a><span data-ttu-id="50983-130">Remarques</span><span class="sxs-lookup"><span data-stu-id="50983-130">Notes</span></span>
* <span data-ttu-id="50983-131">Au-delà des stratégies d’inscription, il est également possible d’utiliser des attributs personnalisés dans les stratégies de connexion ou d’authentification ainsi que dans les stratégies de modification de profil.</span><span class="sxs-lookup"><span data-stu-id="50983-131">Along with sign-up policies, custom attributes can also be used in sign-up or sign-in policies and profile editing policies.</span></span>
* <span data-ttu-id="50983-132">Les attributs personnalisés présentent toutefois un inconvénient connu.</span><span class="sxs-lookup"><span data-stu-id="50983-132">There is a known limitation of custom attributes.</span></span> <span data-ttu-id="50983-133">L’attribut est créé lors de sa première utilisation dans une stratégie, et non pas lorsque vous l’ajoutez à la liste des **Attributs utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="50983-133">It is only created the first time it is used in any policy, and not when you add it to the list of **User attributes**.</span></span>

