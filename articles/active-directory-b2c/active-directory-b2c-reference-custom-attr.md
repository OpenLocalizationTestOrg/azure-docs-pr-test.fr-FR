---
title: "Azure Active Directory B2C : attributs personnalisés | Microsoft Docs"
description: "Attributs personnalisés de toouse dans Azure Active Directory B2C toocollect plus d’informations sur vos clients."
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
ms.openlocfilehash: fb1bff77ad54c246c6d2f69f39c03eafb76fe6bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-use-custom-attributes-toocollect-information-about-your-consumers"></a><span data-ttu-id="edea4-103">Azure B2C Active Directory : Utilisez des attributs personnalisés toocollect plus d’informations sur vos clients</span><span class="sxs-lookup"><span data-stu-id="edea4-103">Azure Active Directory B2C: Use custom attributes toocollect information about your consumers</span></span>
<span data-ttu-id="edea4-104">Votre annuaire Azure Active Directory (Azure AD) B2C est fourni avec un ensemble intégré d’informations (attributs) : le prénom, le nom, la ville, le code postal, et d’autres attributs.</span><span class="sxs-lookup"><span data-stu-id="edea4-104">Your Azure Active Directory (Azure AD) B2C directory comes with a built-in set of information (attributes): Given Name, Surname, City, Postal Code, and other attributes.</span></span> <span data-ttu-id="edea4-105">Toutefois, chaque application réservée aux consommateurs a des contraintes uniques sur le toogather attributs des consommateurs.</span><span class="sxs-lookup"><span data-stu-id="edea4-105">However, every consumer-facing application has unique requirements on what attributes toogather from consumers.</span></span> <span data-ttu-id="edea4-106">Avec Azure AD B2C, vous pouvez étendre le jeu hello d’attributs stockés sur chaque compte du consommateur.</span><span class="sxs-lookup"><span data-stu-id="edea4-106">With Azure AD B2C, you can extend hello set of attributes stored on each consumer account.</span></span> <span data-ttu-id="edea4-107">Vous pouvez créer des attributs personnalisés sur hello [portail Azure](https://portal.azure.com/) et l’utiliser dans vos stratégies d’inscription, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="edea4-107">You can create custom attributes on hello [Azure portal](https://portal.azure.com/) and use it in your sign-up policies, as shown below.</span></span> <span data-ttu-id="edea4-108">Vous pouvez également lire et écrire ces attributs à l’aide de hello [API Azure AD Graph](active-directory-b2c-devquickstarts-graph-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="edea4-108">You can also read and write these attributes by using hello [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).</span></span>

> [!NOTE]
> <span data-ttu-id="edea4-109">Les attributs personnalisés utilisent les [Extensions de schéma de répertoire de l’API Azure AD Graph](https://msdn.microsoft.com/library/azure/dn720459.aspx).</span><span class="sxs-lookup"><span data-stu-id="edea4-109">Custom attributes use [Azure AD Graph API Directory Schema Extensions](https://msdn.microsoft.com/library/azure/dn720459.aspx).</span></span>
> 
> 

## <a name="create-a-custom-attribute"></a><span data-ttu-id="edea4-110">Création d’un attribut personnalisé</span><span class="sxs-lookup"><span data-stu-id="edea4-110">Create a custom attribute</span></span>
1. <span data-ttu-id="edea4-111">[Suivez ces Panneau de fonctionnalités étapes toonavigate toohello B2C hello Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span><span class="sxs-lookup"><span data-stu-id="edea4-111">[Follow these steps toonavigate toohello B2C features blade on hello Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="edea4-112">Cliquez sur **Attributs utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="edea4-112">Click **User attributes**.</span></span>
3. <span data-ttu-id="edea4-113">Cliquez sur **+ ajouter** haut hello du Panneau de hello.</span><span class="sxs-lookup"><span data-stu-id="edea4-113">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="edea4-114">Fournir un **nom** pour l’attribut personnalisé de hello (par exemple, « ShoeSize ») et, éventuellement, un **Description**.</span><span class="sxs-lookup"><span data-stu-id="edea4-114">Provide a **Name** for hello custom attribute (for example, "ShoeSize") and optionally, a **Description**.</span></span> <span data-ttu-id="edea4-115">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="edea4-115">Click **Create**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="edea4-116">Uniquement hello « Chaîne » **Type de données** n’est disponible actuellement.</span><span class="sxs-lookup"><span data-stu-id="edea4-116">Only hello "String" **Data Type** is currently available.</span></span>
   > 
   > 

<span data-ttu-id="edea4-117">attribut personnalisé de Hello est désormais disponible dans la liste des hello **attributs utilisateur**et pour une utilisation dans vos stratégies d’inscription.</span><span class="sxs-lookup"><span data-stu-id="edea4-117">hello custom attribute is now available in hello list of **User attributes**, and for use in your sign-up policies.</span></span>

## <a name="use-a-custom-attribute-in-your-sign-up-policy"></a><span data-ttu-id="edea4-118">Utilisation d’un attribut personnalisé dans votre stratégie d’inscription</span><span class="sxs-lookup"><span data-stu-id="edea4-118">Use a custom attribute in your sign-up policy</span></span>
1. <span data-ttu-id="edea4-119">[Suivez ces Panneau de fonctionnalités étapes toonavigate toohello B2C hello Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span><span class="sxs-lookup"><span data-stu-id="edea4-119">[Follow these steps toonavigate toohello B2C features blade on hello Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="edea4-120">Cliquez sur **Stratégies d'inscription**.</span><span class="sxs-lookup"><span data-stu-id="edea4-120">Click **Sign-up policies**.</span></span>
3. <span data-ttu-id="edea4-121">Cliquez sur tooopen de votre stratégie d’inscription (par exemple, « B2C_1_SiUp ») il.</span><span class="sxs-lookup"><span data-stu-id="edea4-121">Click your sign-up policy (for example, "B2C_1_SiUp") tooopen it.</span></span> <span data-ttu-id="edea4-122">Cliquez sur **modifier** haut hello du Panneau de hello.</span><span class="sxs-lookup"><span data-stu-id="edea4-122">Click **Edit** at hello top of hello blade.</span></span>
4. <span data-ttu-id="edea4-123">Cliquez sur **des attributs d’abonnement** et sélectionnez hello, attribut personnalisé (par exemple, « ShoeSize »).</span><span class="sxs-lookup"><span data-stu-id="edea4-123">Click **Sign-up attributes** and select hello custom attribute (for example, "ShoeSize").</span></span> <span data-ttu-id="edea4-124">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="edea4-124">Click **OK**.</span></span>
5. <span data-ttu-id="edea4-125">Cliquez sur **revendications Application** et les attributs personnalisés sélectionnez hello.</span><span class="sxs-lookup"><span data-stu-id="edea4-125">Click **Application claims** and select hello custom attribute.</span></span> <span data-ttu-id="edea4-126">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="edea4-126">Click **OK**.</span></span>
6. <span data-ttu-id="edea4-127">Cliquez sur **enregistrer** haut hello du Panneau de hello.</span><span class="sxs-lookup"><span data-stu-id="edea4-127">Click **Save** at hello top of hello blade.</span></span>

<span data-ttu-id="edea4-128">Vous pouvez utiliser la fonctionnalité de « Exécuter maintenant » hello sur hello stratégie tooverify hello expérience des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="edea4-128">You can use hello "Run now" feature on hello policy tooverify hello consumer experience.</span></span> <span data-ttu-id="edea4-129">Vous devez maintenant voir « ShoeSize » dans la liste hello d’attributs collectées au cours de l’inscription du consommateur et apparaît dans l’application de jeton tooyour de retour envoyé hello.</span><span class="sxs-lookup"><span data-stu-id="edea4-129">You should now see "ShoeSize" in hello list of attributes collected during consumer sign-up, and see it in hello token sent back tooyour application.</span></span>

## <a name="notes"></a><span data-ttu-id="edea4-130">Remarques</span><span class="sxs-lookup"><span data-stu-id="edea4-130">Notes</span></span>
* <span data-ttu-id="edea4-131">Au-delà des stratégies d’inscription, il est également possible d’utiliser des attributs personnalisés dans les stratégies de connexion ou d’authentification ainsi que dans les stratégies de modification de profil.</span><span class="sxs-lookup"><span data-stu-id="edea4-131">Along with sign-up policies, custom attributes can also be used in sign-up or sign-in policies and profile editing policies.</span></span>
* <span data-ttu-id="edea4-132">Les attributs personnalisés présentent toutefois un inconvénient connu.</span><span class="sxs-lookup"><span data-stu-id="edea4-132">There is a known limitation of custom attributes.</span></span> <span data-ttu-id="edea4-133">Il est uniquement créé hello première fois, il est utilisé dans une stratégie, et pas lorsque vous les ajoutez toohello la liste des **attributs utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="edea4-133">It is only created hello first time it is used in any policy, and not when you add it toohello list of **User attributes**.</span></span>

