---
title: "aaaHow toochange hello durée de vie par défaut pour une application personnalisée | Documents Microsoft"
description: "Comment les stratégies de durée de vie de jeton tooupdate pour votre application que vous développez sur Azure AD"
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
ms.openlocfilehash: 6e1aa1f2a7c33c1f55c5fb619c618ad43cd96273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toochange-hello-token-lifetime-defaults-for-a-custom-developed-application"></a><span data-ttu-id="534c1-103">La durée de vie toochange hello par défaut pour une application personnalisée</span><span class="sxs-lookup"><span data-stu-id="534c1-103">How toochange hello token lifetime defaults for a custom-developed application</span></span>

<span data-ttu-id="534c1-104">Azure AD Premium permet aux développeurs d’application et client administrateurs tooconfigure hello durée de vie des jetons émis pour les clients non confidentielle.</span><span class="sxs-lookup"><span data-stu-id="534c1-104">Azure AD Premium allows app developers and tenant admins tooconfigure hello lifetime of tokens issued for non-confidential clients.</span></span> <span data-ttu-id="534c1-105">Stratégies de durée de vie de jeton sont définies sur un client à l’échelle ou ressources hello en cours d’accès.</span><span class="sxs-lookup"><span data-stu-id="534c1-105">Token lifetime policies are set on a tenant-wide basis or hello resources being accessed.</span></span>

 * <span data-ttu-id="534c1-106">tooset une stratégie de durée de vie de jeton, vous devez les hello toodownload [Module PowerShell Azure AD](https://www.powershellgallery.com/packages/AzureADPreview).</span><span class="sxs-lookup"><span data-stu-id="534c1-106">tooset a token lifetime policy, you need toodownload hello [Azure AD PowerShell Module](https://www.powershellgallery.com/packages/AzureADPreview).</span></span>

 * <span data-ttu-id="534c1-107">Exécutez hello **organisation de se connecter-confirmer** commande.</span><span class="sxs-lookup"><span data-stu-id="534c1-107">Run hello **Connect-AzureAD -Confirm** command.</span></span>

 * <span data-ttu-id="534c1-108">Voici un exemple de stratégie qui définit le jeton d’actualisation hello âge max facteur unique.</span><span class="sxs-lookup"><span data-stu-id="534c1-108">Here’s an example policy that sets hello max age single factor refresh token.</span></span> <span data-ttu-id="534c1-109">Créez la stratégie de hello :```New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"```</span><span class="sxs-lookup"><span data-stu-id="534c1-109">Create hello policy: ```New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"```</span></span>

 * <span data-ttu-id="534c1-110">Hello d’extraction [durée de vie de jeton configuration](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes) document toolearn comment toocreate autres personnalisé.</span><span class="sxs-lookup"><span data-stu-id="534c1-110">Checkout hello [Configuring token lifetime](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes)   document toolearn how toocreate other custom.</span></span>

## <a name="next-steps"></a><span data-ttu-id="534c1-111">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="534c1-111">Next steps</span></span>
[<span data-ttu-id="534c1-112">Durées de vie des jetons configurables dans Azure Active Directory (version préliminaire publique)</span><span class="sxs-lookup"><span data-stu-id="534c1-112">Configuring Token Lifetime</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes)<br>

[<span data-ttu-id="534c1-113">Référence sur les jetons Azure AD</span><span class="sxs-lookup"><span data-stu-id="534c1-113">Azure AD Token Reference</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-token-and-claims)

