---
title: "Accès conditionnel pour utilisateurs Azure Active Directory B2B Collaboration | Microsoft Docs"
description: "Azure Active Directory B2B Collaboration prend en charge l’authentification multifacteur (MFA) pour un accès sélectif à vos applications d’entreprise"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/24/2017
ms.author: sasubram
ms.openlocfilehash: d85f711d6551a68d1248ae8ec61e2ecc1ddc8ecd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="conditional-access-for-b2b-collaboration-users"></a><span data-ttu-id="516db-103">Accès conditionnel pour les utilisateurs de B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="516db-103">Conditional access for B2B collaboration users</span></span>

## <a name="multi-factor-authentication-for-b2b-users"></a><span data-ttu-id="516db-104">Authentification MFA pour utilisateurs B2B</span><span class="sxs-lookup"><span data-stu-id="516db-104">Multi-factor authentication for B2B users</span></span>
<span data-ttu-id="516db-105">Avec Azure AD B2B Collaboration, les organisations peuvent appliquer des stratégies d’authentification multifacteur (MFA) pour les utilisateurs B2B.</span><span class="sxs-lookup"><span data-stu-id="516db-105">With Azure AD B2B collaboration, organizations can enforce multi-factor authentication (MFA) policies for B2B users.</span></span> <span data-ttu-id="516db-106">Ces stratégies peuvent être appliquées au niveau locataire, application ou utilisateur individuel, de la même façon qu’elles peuvent être activées pour les employés à plein temps et les membres de l’organisation.</span><span class="sxs-lookup"><span data-stu-id="516db-106">These policies can be enforced at the tenant, app, or individual user level, the same way that they are enabled for full-time employees and members of the organization.</span></span> <span data-ttu-id="516db-107">Les stratégies MFA sont appliquées à l’organisation de ressources.</span><span class="sxs-lookup"><span data-stu-id="516db-107">MFA policies are enforced at the resource organization.</span></span>

<span data-ttu-id="516db-108">Exemple :</span><span class="sxs-lookup"><span data-stu-id="516db-108">Example:</span></span>
1. <span data-ttu-id="516db-109">L’administrateur ou le professionnel de l’information de la société A invite des utilisateurs de la société B pour l’application *Foo* dans la société A.</span><span class="sxs-lookup"><span data-stu-id="516db-109">Admin or information worker in Company A invites user from company B to an application *Foo* in company A.</span></span>
2. <span data-ttu-id="516db-110">L'application *Foo* dans la société A est configurée de manière à exiger l’authentification MFA lors de l’accès.</span><span class="sxs-lookup"><span data-stu-id="516db-110">Application *Foo* in company A is configured to require MFA on access.</span></span>
3. <span data-ttu-id="516db-111">Lorsque des utilisateurs de la société B tentent d’accéder à l’application *Foo* à partir d’un locataire de la société A, ils sont invités à effectuer une authentification MFA.</span><span class="sxs-lookup"><span data-stu-id="516db-111">When the user from company B attempts to access app *Foo* in the company A tenant, they are asked to complete an MFA challenge.</span></span>
4. <span data-ttu-id="516db-112">Les utilisateurs peuvent configurer leur authentification MFA avec la société A et choisir leur option d’authentification MFA.</span><span class="sxs-lookup"><span data-stu-id="516db-112">The user can set up their MFA with company A, and chooses their MFA option.</span></span>
5. <span data-ttu-id="516db-113">Ce scénario fonctionne pour n’importe quelle identité (Azure AD ou MSA, par exemple, si les utilisateurs dans la société B s’authentifient à l’aide de leur ID social)</span><span class="sxs-lookup"><span data-stu-id="516db-113">This scenario works for any identity (Azure AD or MSA, for example, if users in Company B authenticate using social ID)</span></span>
6. <span data-ttu-id="516db-114">La société A doit avoir suffisamment de licences Azure AD Premium qui prennent en charge l’authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="516db-114">Company A must have sufficient Premium Azure AD licenses that support MFA.</span></span> <span data-ttu-id="516db-115">L’utilisateur de la société B utilise cette licence à partir de la société A.</span><span class="sxs-lookup"><span data-stu-id="516db-115">The user from company B consumes this license from company A.</span></span>

<span data-ttu-id="516db-116">La location d’invitation est toujours responsable de l’authentification MFA pour les utilisateurs de l’organisation partenaire, même si l’organisation partenaire a des fonctionnalités d’authentification MFA.</span><span class="sxs-lookup"><span data-stu-id="516db-116">The inviting tenancy is always responsible for MFA for users from the partner organization, even if the partner organization has MFA capabilities.</span></span>

### <a name="setting-up-mfa-for-b2b-collaboration-users"></a><span data-ttu-id="516db-117">Configuration de MFA pour les utilisateurs de B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="516db-117">Setting up MFA for B2B collaboration users</span></span>
<span data-ttu-id="516db-118">Pour découvrir combien il est facile de configurer l’authentification MFA pour les utilisateurs de B2B Collaboration, consultez la vidéo suivante :</span><span class="sxs-lookup"><span data-stu-id="516db-118">To discover how easy it is to set up MFA for B2B collaboration users, see how in the following video:</span></span>

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/b2b-conditional-access-setup/Player]

### <a name="b2b-users-mfa-experience-for-offer-redemption"></a><span data-ttu-id="516db-119">Expérience MFA d'utilisation de l'invitation par des utilisateurs B2B</span><span class="sxs-lookup"><span data-stu-id="516db-119">B2B users MFA experience for offer redemption</span></span>
<span data-ttu-id="516db-120">Regardez l’animation suivante pour découvrir comment utiliser l’invitation :</span><span class="sxs-lookup"><span data-stu-id="516db-120">Check out the following animation to see the redemption experience:</span></span>

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/MFA-redemption/Player]

### <a name="mfa-reset-for-b2b-collaboration-users"></a><span data-ttu-id="516db-121">Réinitialisation de l'authentification MFA pour les utilisateurs de B2B de Collaboration</span><span class="sxs-lookup"><span data-stu-id="516db-121">MFA reset for B2B collaboration users</span></span>
<span data-ttu-id="516db-122">Actuellement, l’administrateur peut exiger que les utilisateurs B2B Collaboration s’authentifient à nouveau uniquement par le biais des applets de commande PowerShell suivantes :</span><span class="sxs-lookup"><span data-stu-id="516db-122">Currently, the admin can require B2B collaboration users to proof up again only by using the following PowerShell cmdlets:</span></span>

1. <span data-ttu-id="516db-123">Se connecter à Azure AD</span><span class="sxs-lookup"><span data-stu-id="516db-123">Connect to Azure AD</span></span>

  ```
  $cred = Get-Credential
  Connect-MsolService -Credential $cred
  ```
2. <span data-ttu-id="516db-124">Obtenir tous les utilisateurs avec des méthodes d'authentification</span><span class="sxs-lookup"><span data-stu-id="516db-124">Get all users with proof up methods</span></span>

  ```
  Get-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```
  <span data-ttu-id="516db-125">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="516db-125">Here is an example:</span></span>

  ```
  PS C:\Users\tjwasserGet-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```

3. <span data-ttu-id="516db-126">Réinitialisez la méthode d’authentification multifacteur pour qu’un utilisateur spécifique oblige l’utilisateur B2B Collaboration à définir de nouveau des méthodes d’authentification.</span><span class="sxs-lookup"><span data-stu-id="516db-126">Reset the MFA method for a specific user to require the B2B collaboration user to set proof-up methods again.</span></span> <span data-ttu-id="516db-127">Exemple :</span><span class="sxs-lookup"><span data-stu-id="516db-127">Example:</span></span>

  ```
  Reset-MsolStrongAuthenticationMethodByUpn -UserPrincipalName gsamoogle_gmail.com#EXT#@ WoodGroveAzureAD.onmicrosoft.com
  ```

### <a name="why-do-we-perform-mfa-at-the-resource-tenancy"></a><span data-ttu-id="516db-128">Pourquoi effectuer l’authentification MFA au niveau de la location de la ressource ?</span><span class="sxs-lookup"><span data-stu-id="516db-128">Why do we perform MFA at the resource tenancy?</span></span>

<span data-ttu-id="516db-129">Dans la version actuelle, l’authentification MFA s’effectue toujours dans la location de la ressource, pour des raisons de prévisibilité.</span><span class="sxs-lookup"><span data-stu-id="516db-129">In the current release, MFA is always in the resource tenancy, for reasons of predictability.</span></span> <span data-ttu-id="516db-130">Par exemple, un utilisateur de Contoso (Catherine) est invité à Fabrikam, et Fabrikam a activé l’authentification MFA pour les utilisateurs B2B.</span><span class="sxs-lookup"><span data-stu-id="516db-130">For example, let’s say a Contoso user (Sally) is invited to Fabrikam and Fabrikam has enabled MFA for B2B users.</span></span>

<span data-ttu-id="516db-131">Si Contoso utilise la stratégie d’authentification multifacteur sur App1 mais pas sur App2, et si nous examinons la revendication MFA Contoso dans le jeton, nous pourrions constater le problème suivant :</span><span class="sxs-lookup"><span data-stu-id="516db-131">If Contoso has MFA policy enabled for App1 but not App2, then if we look at the Contoso MFA claim in the token, we might see the following issue:</span></span>

* <span data-ttu-id="516db-132">Jour 1 : un utilisateur dispose de l’authentification multifacteur dans Contoso et accède à App1, mais aucune invite MFA supplémentaire ne s’affiche dans Fabrikam.</span><span class="sxs-lookup"><span data-stu-id="516db-132">Day 1: A user has MFA in Contoso and is accessing App1, then no additional MFA prompt is shown in Fabrikam.</span></span>

* <span data-ttu-id="516db-133">Jour 2 : l’utilisateur a accédé à App2 dans Contoso, et à présent, lorsqu’il accède à Fabrikam, il doit s’inscrire pour l’authentification multifacteur ici.</span><span class="sxs-lookup"><span data-stu-id="516db-133">Day 2: The user has accessed App 2 in Contoso, so now when accessing Fabrikam, they must register for MFA there.</span></span>

<span data-ttu-id="516db-134">Ce processus peut prêter à confusion et entraîner l’abandon de connexion.</span><span class="sxs-lookup"><span data-stu-id="516db-134">This process can be confusing and could lead to drop in sign-in completions.</span></span>

<span data-ttu-id="516db-135">En outre, même si Contoso dispose de la fonctionnalité MFA, il n’est pas toujours certain que Fabrikam approuve la stratégie MFA de Contoso.</span><span class="sxs-lookup"><span data-stu-id="516db-135">Moreover, even if Contoso has MFA capability, it is not always the case the Fabrikam would trust the Contoso MFA policy.</span></span>

<span data-ttu-id="516db-136">Enfin, l’authentification MFA du locataire de la ressource fonctionne également pour les MSA et les ID sociaux ainsi que pour les organisations partenaires au sein desquelles l’authentification MFA n’est pas configurée.</span><span class="sxs-lookup"><span data-stu-id="516db-136">Finally, resource tenant MFA also works for MSAs and social IDs and for partner orgs that do not have MFA set up.</span></span>

<span data-ttu-id="516db-137">Par conséquent, la recommandation d’authentification MFA pour les utilisateurs B2B consiste à toujours demander l’authentification MFA dans le locataire à l’origine de l’invitation.</span><span class="sxs-lookup"><span data-stu-id="516db-137">Therefore, the recommendation for MFA for B2B users is to always require MFA in the inviting tenant.</span></span> <span data-ttu-id="516db-138">Dans certains cas, cette condition requise peut entraîner une authentification MFA double, mais pour chaque accès au locataire à l’origine de l’invitation, l’expérience des utilisateurs est prévisible : Catherine doit réaliser l’authentification MFA avec le locataire à l’origine de l’invitation.</span><span class="sxs-lookup"><span data-stu-id="516db-138">This requirement could lead to double MFA in some cases, but whenever accessing the inviting tenant, the end-users experience is predictable: Sally must register for MFA with the inviting tenant.</span></span>

### <a name="device-based-location-based-and-risk-based-conditional-access-for-b2b-users"></a><span data-ttu-id="516db-139">Accès conditionnel en fonction des appareils, des emplacements et des risques pour les utilisateurs B2B</span><span class="sxs-lookup"><span data-stu-id="516db-139">Device-based, location-based, and risk-based conditional access for B2B users</span></span>

<span data-ttu-id="516db-140">Lorsque Contoso active les stratégies d’accès conditionnel en fonction des appareils pour ses données d’entreprise, l’accès est protégé contre les appareils non gérés par Contoso et non conformes aux stratégies d’appareils de Contoso.</span><span class="sxs-lookup"><span data-stu-id="516db-140">When Contoso enables device-based conditional access policies for their corporate data, access is prevented from devices that are not managed by Contoso and not compliant with the Contoso device policies.</span></span>

<span data-ttu-id="516db-141">Si l’appareil de l’utilisateur B2B n’est pas géré par Contoso, l’accès des utilisateurs B2B des organisations partenaires est bloqué quel que soit le contexte d’application de ces stratégies.</span><span class="sxs-lookup"><span data-stu-id="516db-141">If the B2B user’s device isn't managed by Contoso, access of B2B users from the partner organizations is blocked in whatever context these policies are enforced.</span></span> <span data-ttu-id="516db-142">Cependant, Contoso peut créer des listes d’exclusion contenant des utilisateurs spécifiques du partenaire afin d’exclure ces derniers de la stratégie d’accès conditionnel en fonction des appareils.</span><span class="sxs-lookup"><span data-stu-id="516db-142">However, Contoso can create exclusion lists containing specific partner users to exclude them from the device-based conditional access policy.</span></span>

#### <a name="location-based-conditional-access-for-b2b"></a><span data-ttu-id="516db-143">Accès conditionnel en fonction des emplacements pour B2B</span><span class="sxs-lookup"><span data-stu-id="516db-143">Location-based conditional access for B2B</span></span>

<span data-ttu-id="516db-144">Les stratégies d’accès conditionnel en fonction des emplacements peuvent être appliquées pour les utilisateurs B2B si l’organisation à l’origine de l’invitation est en mesure de créer une plage d’adresses IP approuvée qui définit leurs organisations partenaires.</span><span class="sxs-lookup"><span data-stu-id="516db-144">Location-based conditional access policies can be enforced for B2B users if the inviting organization is able to create a trusted IP address range that defines their partner organizations.</span></span>

#### <a name="risk-based-conditional-access-for-b2b"></a><span data-ttu-id="516db-145">Accès conditionnel en fonction des risques pour B2B</span><span class="sxs-lookup"><span data-stu-id="516db-145">Risk-based conditional access for B2B</span></span>

<span data-ttu-id="516db-146">Actuellement, les stratégies de connexion en fonction des risques ne peuvent pas être appliquées aux utilisateurs B2B, car l’évaluation des risques s’effectue au niveau de l’organisation d’origine de l’utilisateur B2B.</span><span class="sxs-lookup"><span data-stu-id="516db-146">Currently, risk-based sign-in policies cannot be applied to B2B users because the risk evaluation is performed at the B2B user’s home organization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="516db-147">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="516db-147">Next steps</span></span>

<span data-ttu-id="516db-148">Consultez les autres articles sur la collaboration B2B d'Azure AD :</span><span class="sxs-lookup"><span data-stu-id="516db-148">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="516db-149">Qu’est-ce qu’Azure AD B2B Collaboration ?</span><span class="sxs-lookup"><span data-stu-id="516db-149">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="516db-150">Comment les administrateurs Azure Active Directory ajoutent-ils des utilisateurs B2B Collaboration ?</span><span class="sxs-lookup"><span data-stu-id="516db-150">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="516db-151">Comment les professionnels de l’information ajoutent-ils des utilisateurs B2B Collaboration ?</span><span class="sxs-lookup"><span data-stu-id="516db-151">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="516db-152">Éléments de l’e-mail d’invitation de B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="516db-152">The elements of the B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="516db-153">Utilisation d’une invitation B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="516db-153">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="516db-154">Attribution de licences Azure AD B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="516db-154">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="516db-155">Résolution des problèmes d’Azure Active Directory B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="516db-155">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="516db-156">Questions fréquemment posées (FAQ) sur Azure Active Directory B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="516db-156">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="516db-157">API et personnalisation d’Azure Active Directory B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="516db-157">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="516db-158">Ajouter des utilisateurs B2B Collaboration sans invitation</span><span class="sxs-lookup"><span data-stu-id="516db-158">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="516db-159">Index d’articles pour la gestion des applications dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="516db-159">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
