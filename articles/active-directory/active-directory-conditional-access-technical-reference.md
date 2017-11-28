---
title: "aaaAzure référence technique d’Active Directory Access conditionnel | Documents Microsoft"
description: "Avec le contrôle d’accès conditionnel, Azure Active Directory vérifie les conditions spécifiques hello que vous choisissez lors de l’authentification utilisateur de hello et avant d’autoriser l’accès toohello application. Lorsque ces conditions sont réunies, hello utilisateur authentifié et autorisé accès toohello application."
services: active-directory.
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 56a5bade-7dcc-4dcf-8092-a7d4bf5df3c1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: ee201405d1d17f130607a95bf455b60cd222dd0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-conditional-access-technical-reference"></a><span data-ttu-id="1d5b6-104">Référence technique d’Azure Active Directory Conditional Access</span><span class="sxs-lookup"><span data-stu-id="1d5b6-104">Azure Active Directory Conditional Access technical reference</span></span>

## <a name="services-enabled-with-conditional-access"></a><span data-ttu-id="1d5b6-105">Services activés avec accès conditionnel</span><span class="sxs-lookup"><span data-stu-id="1d5b6-105">Services enabled with conditional access</span></span>

<span data-ttu-id="1d5b6-106">Les règles d’accès conditionnel sont prises en charge sur différents types d’application Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1d5b6-106">Conditional Access rules are supported across various Azure AD application types.</span></span> <span data-ttu-id="1d5b6-107">Cette liste comprend les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="1d5b6-107">This list includes:</span></span>


* <span data-ttu-id="1d5b6-108">Applications inscrites avec hello Proxy d’Application Azure</span><span class="sxs-lookup"><span data-stu-id="1d5b6-108">Applications registered with hello Azure Application Proxy</span></span>
* <span data-ttu-id="1d5b6-109">Application distante Azure</span><span class="sxs-lookup"><span data-stu-id="1d5b6-109">Azure Remote App</span></span>
* <span data-ttu-id="1d5b6-110">Applications métiers et mutualisées développées inscrites auprès d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="1d5b6-110">Developed line of business and multi-tenant applications registered with Azure AD</span></span>
* <span data-ttu-id="1d5b6-111">Dynamics CRM</span><span class="sxs-lookup"><span data-stu-id="1d5b6-111">Dynamics CRM</span></span>
* <span data-ttu-id="1d5b6-112">Applications fédérées à partir de la galerie d’applications Azure AD hello</span><span class="sxs-lookup"><span data-stu-id="1d5b6-112">Federated applications from hello Azure AD application gallery</span></span>
* <span data-ttu-id="1d5b6-113">Microsoft Office 365 Yammer</span><span class="sxs-lookup"><span data-stu-id="1d5b6-113">Microsoft Office 365 Yammer</span></span>
* <span data-ttu-id="1d5b6-114">Microsoft Office 365 Exchange Online</span><span class="sxs-lookup"><span data-stu-id="1d5b6-114">Microsoft Office 365 Exchange Online</span></span>
* <span data-ttu-id="1d5b6-115">Microsoft Office 365 SharePoint Online (y compris OneDrive Entreprise)</span><span class="sxs-lookup"><span data-stu-id="1d5b6-115">Microsoft Office 365 SharePoint Online (includes OneDrive for Business)</span></span>
* <span data-ttu-id="1d5b6-116">Microsoft Power BI</span><span class="sxs-lookup"><span data-stu-id="1d5b6-116">Microsoft Power BI</span></span> 
* <span data-ttu-id="1d5b6-117">Applications de l’authentification unique de mot de passe à partir de la galerie d’applications hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="1d5b6-117">Password SSO applications from hello Azure AD application gallery</span></span>
* <span data-ttu-id="1d5b6-118">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="1d5b6-118">Visual Studio Team Services</span></span>
* <span data-ttu-id="1d5b6-119">Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="1d5b6-119">Microsoft Teams</span></span>









## <a name="enable-access-rules"></a><span data-ttu-id="1d5b6-120">Activer les règles d’accès</span><span class="sxs-lookup"><span data-stu-id="1d5b6-120">Enable access rules</span></span>
<span data-ttu-id="1d5b6-121">Chaque règle peut être activée ou désactivée sur la base de l’application.</span><span class="sxs-lookup"><span data-stu-id="1d5b6-121">Each rule can be enabled or disabled on a per application bases.</span></span> <span data-ttu-id="1d5b6-122">Lorsque les règles sont **ON** ils seront activés et appliquées pour les utilisateurs l’accès à application hello.</span><span class="sxs-lookup"><span data-stu-id="1d5b6-122">When rules are **ON** they will be enabled and enforced for users accessing hello application.</span></span> <span data-ttu-id="1d5b6-123">Lorsqu’ils sont **OFF** ils ne doivent pas être utilisés et seront affecte pas les utilisateurs sur le hello de connexion.</span><span class="sxs-lookup"><span data-stu-id="1d5b6-123">When they are **OFF** they will not be used and will not impact hello users sign in experience.</span></span>

## <a name="applying-rules-toospecific-users"></a><span data-ttu-id="1d5b6-124">Appliquant les règles des utilisateurs toospecific</span><span class="sxs-lookup"><span data-stu-id="1d5b6-124">Applying rules toospecific users</span></span>
<span data-ttu-id="1d5b6-125">Les règles peuvent être toospecific appliqué des jeux d’utilisateurs basés sur le groupe de sécurité en définissant **s’appliquent à**.</span><span class="sxs-lookup"><span data-stu-id="1d5b6-125">Rules can be applied toospecific sets of users based on security group by setting **Apply To**.</span></span> <span data-ttu-id="1d5b6-126">**Appliquer à** peut être défini trop**tous les utilisateurs** ou **groupes**.</span><span class="sxs-lookup"><span data-stu-id="1d5b6-126">**Apply To** can be set too**All Users** or **Groups**.</span></span> <span data-ttu-id="1d5b6-127">Lorsque la valeur trop**tous les utilisateurs** règles que hello s’appliquent utilisateur tooany avec application toohello d’accès.</span><span class="sxs-lookup"><span data-stu-id="1d5b6-127">When set too**All Users** hello rules will apply tooany user with access toohello application.</span></span> <span data-ttu-id="1d5b6-128">Hello **groupes** option permet de sécurité spécifiques et toobe de groupes de distribution sélectionné, les règles sont appliquées uniquement pour ces groupes.</span><span class="sxs-lookup"><span data-stu-id="1d5b6-128">hello **Groups** option allows specific security and distribution groups toobe selected, rules will only be enforced for these groups.</span></span>

<span data-ttu-id="1d5b6-129">Lors du déploiement d’une règle, il est courant toofirst appliquer un ensemble limité d’utilisateurs, qui sont membres d’un groupe de pilotage.</span><span class="sxs-lookup"><span data-stu-id="1d5b6-129">When deploying a rule,  it is common toofirst apply it a limited set of users, that are members of a piloting groups.</span></span> <span data-ttu-id="1d5b6-130">Une fois que la règle de hello complète peut être appliquée trop**tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="1d5b6-130">Once complete hello rule can be applied too**All Users**.</span></span> <span data-ttu-id="1d5b6-131">Cela entraîne la règle hello toobe appliquée pour tous les utilisateurs de l’organisation de hello.</span><span class="sxs-lookup"><span data-stu-id="1d5b6-131">This will cause hello rule toobe enforced for all users in hello organization.</span></span>

<span data-ttu-id="1d5b6-132">Sélectionnez des groupes peuvent également être exemptées de stratégie à l’aide de hello **sauf** option.</span><span class="sxs-lookup"><span data-stu-id="1d5b6-132">Select groups may also be exempted from policy using hello **Except** option.</span></span> <span data-ttu-id="1d5b6-133">Tous les membres de ces groupes seront exclus et ce, même s’ils apparaissent dans un groupe inclus.</span><span class="sxs-lookup"><span data-stu-id="1d5b6-133">Any members of these groups will be exempted even if they appear in an included group.</span></span>

## <a name="at-work-networks"></a><span data-ttu-id="1d5b6-134">Réseaux Au bureau</span><span class="sxs-lookup"><span data-stu-id="1d5b6-134">“At work” networks</span></span>
<span data-ttu-id="1d5b6-135">Règles d’accès conditionnel qui utilisent un réseau « au travail », s’appuient sur les plages d’adresses IP approuvés qui ont été configurés dans Azure AD, ou l’utilisation de hello « à l’intérieur du réseau d’entreprise » de revendication d’AD FS.</span><span class="sxs-lookup"><span data-stu-id="1d5b6-135">Conditional access rules that use an “At work” network, rely on trusted IP address ranges that have been configured in Azure AD, or use of hello "inside corpnet" claim from AD FS.</span></span> <span data-ttu-id="1d5b6-136">Ces règles incluent les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="1d5b6-136">These rules include:</span></span>

* <span data-ttu-id="1d5b6-137">Exiger l’authentification multifacteur à l’extérieur de l’entreprise</span><span class="sxs-lookup"><span data-stu-id="1d5b6-137">Require multi-factor authentication when not at work</span></span>
* <span data-ttu-id="1d5b6-138">Bloquer l’accès quand l’utilisateur n’est pas au bureau</span><span class="sxs-lookup"><span data-stu-id="1d5b6-138">Block access when not at work</span></span>

<span data-ttu-id="1d5b6-139">Options pour la spécification des réseaux Au bureau</span><span class="sxs-lookup"><span data-stu-id="1d5b6-139">Options for specifiying “at work” networks</span></span>

1. <span data-ttu-id="1d5b6-140">Configurer des plages d’adresses IP approuvées Bonjour [page de configuration de l’authentification multifacteur](../multi-factor-authentication/multi-factor-authentication-whats-next.md).</span><span class="sxs-lookup"><span data-stu-id="1d5b6-140">Configure trusted IP address ranges in hello [multi-factor authentication configuration page](../multi-factor-authentication/multi-factor-authentication-whats-next.md).</span></span> <span data-ttu-id="1d5b6-141">Stratégie d’accès conditionnel utilise les plages hello configuré sur chaque demande et le jeton d’émission tooevaluate les règles d’authentification.</span><span class="sxs-lookup"><span data-stu-id="1d5b6-141">Conditional Access policy will use hello configured ranges on each authentication request and token issuance tooevaluate rules.</span></span> 
2. <span data-ttu-id="1d5b6-142">Configurer l’utilisation de hello à l’intérieur de revendication du réseau d’entreprise, cette option peut être utilisée avec les répertoires fédérés, à l’aide d’AD FS.</span><span class="sxs-lookup"><span data-stu-id="1d5b6-142">Configure use of hello inside corpnet claim, this option can be used with federated directories, using AD FS.</span></span> <span data-ttu-id="1d5b6-143">toolearn en savoir plus sur hello à l’intérieur des revendications de réseau d’entreprise, consultez [Tusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span><span class="sxs-lookup"><span data-stu-id="1d5b6-143">toolearn more about hello inside corpnet claims, see [Tusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span></span>


## <a name="rules-based-on-application-sensitivity"></a><span data-ttu-id="1d5b6-144">Règles basées sur le critère de diffusion des applications</span><span class="sxs-lookup"><span data-stu-id="1d5b6-144">Rules based on application sensitivity</span></span>
<span data-ttu-id="1d5b6-145">Les règles sont configurées par application qui permet de toobe de services de valeur élevée hello sécurisé sans impact sur les services d’accès tooother.</span><span class="sxs-lookup"><span data-stu-id="1d5b6-145">Rules are configured per application allowing hello high value services toobe secured without impacting access tooother services.</span></span> <span data-ttu-id="1d5b6-146">Règles d’accès conditionnel peuvent être configurés sur hello **configurer** onglet de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="1d5b6-146">Conditional access rules can be configured on hello  **Configure** tab of hello application.</span></span> 

<span data-ttu-id="1d5b6-147">Règles actuellement proposées :</span><span class="sxs-lookup"><span data-stu-id="1d5b6-147">Rules currently offered:</span></span>

* <span data-ttu-id="1d5b6-148">**Imposer l’authentification multifacteur**</span><span class="sxs-lookup"><span data-stu-id="1d5b6-148">**Require multi-factor authentication**</span></span>
  
  * <span data-ttu-id="1d5b6-149">Tous les utilisateurs que cette stratégie est appliquée toowill être tooauthenticate requis via l’authentification multifacteur au moins une fois.</span><span class="sxs-lookup"><span data-stu-id="1d5b6-149">All users that this policy is applied toowill be required tooauthenticate via multi-factor authentication at least once.</span></span>
* <span data-ttu-id="1d5b6-150">**Exiger l’authentification multifacteur à l’extérieur de l’entreprise**</span><span class="sxs-lookup"><span data-stu-id="1d5b6-150">**Require multi-factor authentication when not at work**</span></span>
  
  * <span data-ttu-id="1d5b6-151">Si cette stratégie est appliquée, tous les utilisateurs seront requis toohave effectuée l’authentification multifacteur au moins une fois si elles accéder au service de hello à partir d’un emplacement distant non liés au travail.</span><span class="sxs-lookup"><span data-stu-id="1d5b6-151">If this policy is applied, all users will be required toohave performed multi-factor authentication at least once if they access hello service from a non-work remote location.</span></span> <span data-ttu-id="1d5b6-152">S’ils se déplacent à partir d’un emplacement de tooremote de travail, elles seront tooperform obligatoire l’authentification multifacteur lors de l’accès au service de hello.</span><span class="sxs-lookup"><span data-stu-id="1d5b6-152">If they move from a work tooremote location, they will be required tooperform multifactor authentication when accessing hello service.</span></span>
* <span data-ttu-id="1d5b6-153">**Bloquer l’accès quand l’utilisateur n’est pas au bureau**</span><span class="sxs-lookup"><span data-stu-id="1d5b6-153">**Block access when not at work**</span></span> 
  
  * <span data-ttu-id="1d5b6-154">Lorsque des utilisateurs changent d’emplacement de travail tooa distant, ils ne peuvent pas si hello « Bloquer l’accès à l’extérieur de travail » la stratégie est appliquée toothem.</span><span class="sxs-lookup"><span data-stu-id="1d5b6-154">When users move from work tooa remote location, they will be blocked if hello "Block access when not at work" policy is applied toothem.</span></span>  <span data-ttu-id="1d5b6-155">Ils seront de nouveau autorisés à y accéder lorsqu’ils se trouvent au bureau.</span><span class="sxs-lookup"><span data-stu-id="1d5b6-155">They will be re-allowed access when at a work location.</span></span>

## <a name="related-topics"></a><span data-ttu-id="1d5b6-156">Rubriques connexes</span><span class="sxs-lookup"><span data-stu-id="1d5b6-156">Related topics</span></span>
* [<span data-ttu-id="1d5b6-157">Sécurisation de l’accès tooOffice 365 et d’autres applications connectées tooAzure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1d5b6-157">Securing access tooOffice 365 and other apps connected tooAzure Active Directory</span></span>](active-directory-conditional-access.md)
* [<span data-ttu-id="1d5b6-158">Index d’articles pour la gestion des applications dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1d5b6-158">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)

