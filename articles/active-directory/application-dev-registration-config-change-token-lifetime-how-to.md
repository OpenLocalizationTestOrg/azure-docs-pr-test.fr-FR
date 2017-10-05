---
title: "Modifier les valeurs par défaut de la durée de vie des jetons pour une application personnalisée | Microsoft Docs"
description: "Comment mettre à jour les stratégies de durée de vie des jetons pour l’application que vous développez sur Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: a28eacd820ed28a6470992ce86b060e886c00bcb
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-change-the-token-lifetime-defaults-for-a-custom-developed-application"></a><span data-ttu-id="3950e-103">Modifier les valeurs par défaut de la durée de vie des jetons pour une application personnalisée</span><span class="sxs-lookup"><span data-stu-id="3950e-103">How to change the token lifetime defaults for a custom-developed application</span></span>

<span data-ttu-id="3950e-104">Azure AD Premium permet aux développeurs d’applications et aux administrateurs de locataires de configurer la durée de vie des jetons émis pour les clients non confidentiels.</span><span class="sxs-lookup"><span data-stu-id="3950e-104">Azure AD Premium allows app developers and tenant admins to configure the lifetime of tokens issued for non-confidential clients.</span></span> <span data-ttu-id="3950e-105">Les stratégies de durée de vie des jetons sont définies à l’échelle d’un locataire ou en fonction des ressources accessibles.</span><span class="sxs-lookup"><span data-stu-id="3950e-105">Token lifetime policies are set on a tenant-wide basis or the resources being accessed.</span></span>

 * <span data-ttu-id="3950e-106">Pour définir une stratégie de durée de vie de jeton, vous devez télécharger le [module Azure AD PowerShell](https://www.powershellgallery.com/packages/AzureADPreview).</span><span class="sxs-lookup"><span data-stu-id="3950e-106">To set a token lifetime policy, you need to download the [Azure AD PowerShell Module](https://www.powershellgallery.com/packages/AzureADPreview).</span></span>

 * <span data-ttu-id="3950e-107">Exécutez la commande **Connect-AzureAD -Confirm**.</span><span class="sxs-lookup"><span data-stu-id="3950e-107">Run the **Connect-AzureAD -Confirm** command.</span></span>

 * <span data-ttu-id="3950e-108">Voici un exemple de stratégie qui définit le jeton d’actualisation à facteur unique d’âge maximal.</span><span class="sxs-lookup"><span data-stu-id="3950e-108">Here’s an example policy that sets the max age single factor refresh token.</span></span> <span data-ttu-id="3950e-109">Créez la stratégie : ```New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"```</span><span class="sxs-lookup"><span data-stu-id="3950e-109">Create the policy: ```New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"```</span></span>

 * <span data-ttu-id="3950e-110">Consultez l’article [Durées de vie des jetons configurables dans Azure Active Directory (version préliminaire publique)](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes) pour apprendre à créer d’autres stratégies personnalisées.</span><span class="sxs-lookup"><span data-stu-id="3950e-110">Checkout the [Configuring token lifetime](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes)   document to learn how to create other custom.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3950e-111">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3950e-111">Next steps</span></span>
[<span data-ttu-id="3950e-112">Durées de vie des jetons configurables dans Azure Active Directory (version préliminaire publique)</span><span class="sxs-lookup"><span data-stu-id="3950e-112">Configuring Token Lifetime</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes)<br>

[<span data-ttu-id="3950e-113">Référence sur les jetons Azure AD</span><span class="sxs-lookup"><span data-stu-id="3950e-113">Azure AD Token Reference</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-token-and-claims)

