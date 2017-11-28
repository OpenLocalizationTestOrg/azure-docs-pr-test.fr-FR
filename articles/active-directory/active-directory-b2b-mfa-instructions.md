---
title: "l’accès pour les utilisateurs Azure Active Directory B2B collaboration aaaConditional | Documents Microsoft"
description: "Azure Active Directory B2B collaboration prend en charge l’authentification multifacteur (MFA) pour les applications d’entreprise un accès sélectif tooyour"
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
ms.openlocfilehash: 3a05be4393f74ff8e87f32432a222a5fbac9af62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-for-b2b-collaboration-users"></a><span data-ttu-id="009a3-103">Accès conditionnel pour les utilisateurs de B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="009a3-103">Conditional access for B2B collaboration users</span></span>

## <a name="multi-factor-authentication-for-b2b-users"></a><span data-ttu-id="009a3-104">Authentification MFA pour utilisateurs B2B</span><span class="sxs-lookup"><span data-stu-id="009a3-104">Multi-factor authentication for B2B users</span></span>
<span data-ttu-id="009a3-105">Avec Azure AD B2B Collaboration, les organisations peuvent appliquer des stratégies d’authentification multifacteur (MFA) pour les utilisateurs B2B.</span><span class="sxs-lookup"><span data-stu-id="009a3-105">With Azure AD B2B collaboration, organizations can enforce multi-factor authentication (MFA) policies for B2B users.</span></span> <span data-ttu-id="009a3-106">Ces stratégies peuvent être appliquées au client de hello, application ou au niveau utilisateur individuel, hello même façon qu’ils sont activés pour les employés à plein temps et les membres de l’organisation de hello.</span><span class="sxs-lookup"><span data-stu-id="009a3-106">These policies can be enforced at hello tenant, app, or individual user level, hello same way that they are enabled for full-time employees and members of hello organization.</span></span> <span data-ttu-id="009a3-107">Stratégies d’authentification Multifacteur sont appliquées au niveau de l’organisation de ressource hello.</span><span class="sxs-lookup"><span data-stu-id="009a3-107">MFA policies are enforced at hello resource organization.</span></span>

<span data-ttu-id="009a3-108">Exemple :</span><span class="sxs-lookup"><span data-stu-id="009a3-108">Example:</span></span>
1. <span data-ttu-id="009a3-109">Travail d’administrateur ou des informations dans la société A invite l’utilisateur à partir de l’application de la société B tooan *Foo* dans la société A.</span><span class="sxs-lookup"><span data-stu-id="009a3-109">Admin or information worker in Company A invites user from company B tooan application *Foo* in company A.</span></span>
2. <span data-ttu-id="009a3-110">Application *Foo* dans la société A est toorequire configuré l’authentification Multifacteur sur l’accès.</span><span class="sxs-lookup"><span data-stu-id="009a3-110">Application *Foo* in company A is configured toorequire MFA on access.</span></span>
3. <span data-ttu-id="009a3-111">Lorsque les utilisateur hello à partir de la société B tente de tooaccess application *Foo* entreprise hello un client, ils sont demandé toocomplete une stimulation d’authentification Multifacteur.</span><span class="sxs-lookup"><span data-stu-id="009a3-111">When hello user from company B attempts tooaccess app *Foo* in hello company A tenant, they are asked toocomplete an MFA challenge.</span></span>
4. <span data-ttu-id="009a3-112">Hello utilisateur permettre définir leur MFA avec la société A et choisit l’option de l’authentification Multifacteur.</span><span class="sxs-lookup"><span data-stu-id="009a3-112">hello user can set up their MFA with company A, and chooses their MFA option.</span></span>
5. <span data-ttu-id="009a3-113">Ce scénario fonctionne pour n’importe quelle identité (Azure AD ou MSA, par exemple, si les utilisateurs dans la société B s’authentifient à l’aide de leur ID social)</span><span class="sxs-lookup"><span data-stu-id="009a3-113">This scenario works for any identity (Azure AD or MSA, for example, if users in Company B authenticate using social ID)</span></span>
6. <span data-ttu-id="009a3-114">La société A doit avoir suffisamment de licences Azure AD Premium qui prennent en charge l’authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="009a3-114">Company A must have sufficient Premium Azure AD licenses that support MFA.</span></span> <span data-ttu-id="009a3-115">utilisateur Hello à partir de la société B utilise cette licence à partir de la société A.</span><span class="sxs-lookup"><span data-stu-id="009a3-115">hello user from company B consumes this license from company A.</span></span>

<span data-ttu-id="009a3-116">architecture mutualisée invitant à Hello est toujours chargée pour l’authentification Multifacteur pour les utilisateurs à partir de l’organisation partenaire de hello, même si l’organisation partenaire de hello possède des fonctionnalités d’authentification Multifacteur.</span><span class="sxs-lookup"><span data-stu-id="009a3-116">hello inviting tenancy is always responsible for MFA for users from hello partner organization, even if hello partner organization has MFA capabilities.</span></span>

### <a name="setting-up-mfa-for-b2b-collaboration-users"></a><span data-ttu-id="009a3-117">Configuration de MFA pour les utilisateurs de B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="009a3-117">Setting up MFA for B2B collaboration users</span></span>
<span data-ttu-id="009a3-118">toodiscover facilement se tooset de l’authentification Multifacteur pour les utilisateurs de collaboration B2B, consultez Comment procéder hello suite vidéo :</span><span class="sxs-lookup"><span data-stu-id="009a3-118">toodiscover how easy it is tooset up MFA for B2B collaboration users, see how in hello following video:</span></span>

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/b2b-conditional-access-setup/Player]

### <a name="b2b-users-mfa-experience-for-offer-redemption"></a><span data-ttu-id="009a3-119">Expérience MFA d'utilisation de l'invitation par des utilisateurs B2B</span><span class="sxs-lookup"><span data-stu-id="009a3-119">B2B users MFA experience for offer redemption</span></span>
<span data-ttu-id="009a3-120">Passez en revue hello suivant l’expérience de remboursement animation toosee hello :</span><span class="sxs-lookup"><span data-stu-id="009a3-120">Check out hello following animation toosee hello redemption experience:</span></span>

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/MFA-redemption/Player]

### <a name="mfa-reset-for-b2b-collaboration-users"></a><span data-ttu-id="009a3-121">Réinitialisation de l'authentification MFA pour les utilisateurs de B2B de Collaboration</span><span class="sxs-lookup"><span data-stu-id="009a3-121">MFA reset for B2B collaboration users</span></span>
<span data-ttu-id="009a3-122">Actuellement, hello admin peut requérir B2B collaboration utilisateurs tooproof place à nouveau uniquement à l’aide de hello suivant d’applets de commande PowerShell :</span><span class="sxs-lookup"><span data-stu-id="009a3-122">Currently, hello admin can require B2B collaboration users tooproof up again only by using hello following PowerShell cmdlets:</span></span>

1. <span data-ttu-id="009a3-123">Se connecter tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="009a3-123">Connect tooAzure AD</span></span>

  ```
  $cred = Get-Credential
  Connect-MsolService -Credential $cred
  ```
2. <span data-ttu-id="009a3-124">Obtenir tous les utilisateurs avec des méthodes d'authentification</span><span class="sxs-lookup"><span data-stu-id="009a3-124">Get all users with proof up methods</span></span>

  ```
  Get-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```
  <span data-ttu-id="009a3-125">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="009a3-125">Here is an example:</span></span>

  ```
  PS C:\Users\tjwasserGet-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```

3. <span data-ttu-id="009a3-126">Redéfinir la méthode d’authentification Multifacteur hello pour un utilisateur spécifique toorequire hello B2B collaboration utilisateur tooset preuve méthodes.</span><span class="sxs-lookup"><span data-stu-id="009a3-126">Reset hello MFA method for a specific user toorequire hello B2B collaboration user tooset proof-up methods again.</span></span> <span data-ttu-id="009a3-127">Exemple :</span><span class="sxs-lookup"><span data-stu-id="009a3-127">Example:</span></span>

  ```
  Reset-MsolStrongAuthenticationMethodByUpn -UserPrincipalName gsamoogle_gmail.com#EXT#@ WoodGroveAzureAD.onmicrosoft.com
  ```

### <a name="why-do-we-perform-mfa-at-hello-resource-tenancy"></a><span data-ttu-id="009a3-128">Pourquoi effectuer l’authentification Multifacteur à l’architecture mutualisée de ressource hello ?</span><span class="sxs-lookup"><span data-stu-id="009a3-128">Why do we perform MFA at hello resource tenancy?</span></span>

<span data-ttu-id="009a3-129">Dans la version actuelle de hello, l’authentification Multifacteur est toujours dans l’architecture mutualisée de ressource hello, pour des raisons de prévisibilité.</span><span class="sxs-lookup"><span data-stu-id="009a3-129">In hello current release, MFA is always in hello resource tenancy, for reasons of predictability.</span></span> <span data-ttu-id="009a3-130">Par exemple, un utilisateur de Contoso (Sarah) est tooFabrikam invité et Fabrikam a activé l’authentification Multifacteur pour les utilisateurs de B2B.</span><span class="sxs-lookup"><span data-stu-id="009a3-130">For example, let’s say a Contoso user (Sally) is invited tooFabrikam and Fabrikam has enabled MFA for B2B users.</span></span>

<span data-ttu-id="009a3-131">Si Contoso utilise la stratégie d’authentification Multifacteur activée pour App1 mais pas App2, puis si nous examinons hello revendication Contoso MFA dans le jeton de hello, nous pouvons voir hello suivant le problème :</span><span class="sxs-lookup"><span data-stu-id="009a3-131">If Contoso has MFA policy enabled for App1 but not App2, then if we look at hello Contoso MFA claim in hello token, we might see hello following issue:</span></span>

* <span data-ttu-id="009a3-132">Jour 1 : un utilisateur dispose de l’authentification multifacteur dans Contoso et accède à App1, mais aucune invite MFA supplémentaire ne s’affiche dans Fabrikam.</span><span class="sxs-lookup"><span data-stu-id="009a3-132">Day 1: A user has MFA in Contoso and is accessing App1, then no additional MFA prompt is shown in Fabrikam.</span></span>

* <span data-ttu-id="009a3-133">Le jour 2 : hello accès utilisateur 2 application chez Contoso, maintenant lorsque vous accédez à Fabrikam, ils doivent s’inscrire pour l’authentification Multifacteur il.</span><span class="sxs-lookup"><span data-stu-id="009a3-133">Day 2: hello user has accessed App 2 in Contoso, so now when accessing Fabrikam, they must register for MFA there.</span></span>

<span data-ttu-id="009a3-134">Ce processus peut prêter à confusion et risque de toodrop de connexion réussies.</span><span class="sxs-lookup"><span data-stu-id="009a3-134">This process can be confusing and could lead toodrop in sign-in completions.</span></span>

<span data-ttu-id="009a3-135">En outre, même si Contoso possède la capacité de l’authentification Multifacteur, il n'est pas toujours Bonjour cas Bonjour Fabrikam serait confiance hello stratégie Contoso MFA.</span><span class="sxs-lookup"><span data-stu-id="009a3-135">Moreover, even if Contoso has MFA capability, it is not always hello case hello Fabrikam would trust hello Contoso MFA policy.</span></span>

<span data-ttu-id="009a3-136">Enfin, l’authentification MFA du locataire de la ressource fonctionne également pour les MSA et les ID sociaux ainsi que pour les organisations partenaires au sein desquelles l’authentification MFA n’est pas configurée.</span><span class="sxs-lookup"><span data-stu-id="009a3-136">Finally, resource tenant MFA also works for MSAs and social IDs and for partner orgs that do not have MFA set up.</span></span>

<span data-ttu-id="009a3-137">Par conséquent, la recommandation hello pour l’authentification Multifacteur pour les utilisateurs de B2B est tooalways exiger l’authentification Multifacteur Bonjour inviter les clients.</span><span class="sxs-lookup"><span data-stu-id="009a3-137">Therefore, hello recommendation for MFA for B2B users is tooalways require MFA in hello inviting tenant.</span></span> <span data-ttu-id="009a3-138">Cette exigence peut entraîner des toodouble l’authentification Multifacteur dans certains cas, mais chaque fois que l’accès aux locataires d’invitation hello, l’expérience des utilisateurs finaux hello est prévisible : Catherine doit inscrire pour l’authentification Multifacteur avec le client d’invitation hello.</span><span class="sxs-lookup"><span data-stu-id="009a3-138">This requirement could lead toodouble MFA in some cases, but whenever accessing hello inviting tenant, hello end-users experience is predictable: Sally must register for MFA with hello inviting tenant.</span></span>

### <a name="device-based-location-based-and-risk-based-conditional-access-for-b2b-users"></a><span data-ttu-id="009a3-139">Accès conditionnel en fonction des appareils, des emplacements et des risques pour les utilisateurs B2B</span><span class="sxs-lookup"><span data-stu-id="009a3-139">Device-based, location-based, and risk-based conditional access for B2B users</span></span>

<span data-ttu-id="009a3-140">Lorsque Contoso Active des stratégies d’accès conditionnel basés sur un appareil pour leurs données d’entreprise, l’accès est bloqué dans les appareils qui ne sont pas gérés par Contoso et non conformes avec les stratégies d’appareil Contoso hello.</span><span class="sxs-lookup"><span data-stu-id="009a3-140">When Contoso enables device-based conditional access policies for their corporate data, access is prevented from devices that are not managed by Contoso and not compliant with hello Contoso device policies.</span></span>

<span data-ttu-id="009a3-141">Si l’appareil de l’utilisateur hello B2B n’est pas géré par Contoso, l’accès des utilisateurs B2B des organisations partenaires de hello est bloquée dans le contexte de ces stratégies sont appliquées.</span><span class="sxs-lookup"><span data-stu-id="009a3-141">If hello B2B user’s device isn't managed by Contoso, access of B2B users from hello partner organizations is blocked in whatever context these policies are enforced.</span></span> <span data-ttu-id="009a3-142">Toutefois, Contoso peut créer d’exclusion listes contenant partenaire utilisateurs tooexclude de hello stratégie d’accès conditionnel basés sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="009a3-142">However, Contoso can create exclusion lists containing specific partner users tooexclude them from hello device-based conditional access policy.</span></span>

#### <a name="location-based-conditional-access-for-b2b"></a><span data-ttu-id="009a3-143">Accès conditionnel en fonction des emplacements pour B2B</span><span class="sxs-lookup"><span data-stu-id="009a3-143">Location-based conditional access for B2B</span></span>

<span data-ttu-id="009a3-144">Stratégies d’accès conditionnel emplacement peuvent être appliquées pour les utilisateurs de B2B si l’organisation d’invitation hello est en mesure de toocreate une plage d’adresses IP approuvée qui définit leurs organisations partenaires.</span><span class="sxs-lookup"><span data-stu-id="009a3-144">Location-based conditional access policies can be enforced for B2B users if hello inviting organization is able toocreate a trusted IP address range that defines their partner organizations.</span></span>

#### <a name="risk-based-conditional-access-for-b2b"></a><span data-ttu-id="009a3-145">Accès conditionnel en fonction des risques pour B2B</span><span class="sxs-lookup"><span data-stu-id="009a3-145">Risk-based conditional access for B2B</span></span>

<span data-ttu-id="009a3-146">Actuellement, des risques connectez-vous stratégies ne peut pas être appliqué tooB2B utilisateurs, car l’évaluation des risques hello est effectuée au niveau de l’organisation d’origine de l’utilisateur hello B2B.</span><span class="sxs-lookup"><span data-stu-id="009a3-146">Currently, risk-based sign-in policies cannot be applied tooB2B users because hello risk evaluation is performed at hello B2B user’s home organization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="009a3-147">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="009a3-147">Next steps</span></span>

<span data-ttu-id="009a3-148">Consultez les autres articles sur la collaboration B2B d'Azure AD :</span><span class="sxs-lookup"><span data-stu-id="009a3-148">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="009a3-149">Qu’est-ce qu’Azure AD B2B Collaboration ?</span><span class="sxs-lookup"><span data-stu-id="009a3-149">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="009a3-150">Comment les administrateurs Azure Active Directory ajoutent-ils des utilisateurs B2B Collaboration ?</span><span class="sxs-lookup"><span data-stu-id="009a3-150">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="009a3-151">Comment les professionnels de l’information ajoutent-ils des utilisateurs B2B Collaboration ?</span><span class="sxs-lookup"><span data-stu-id="009a3-151">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="009a3-152">éléments Hello Hello e-mail d’invitation B2B collaboration</span><span class="sxs-lookup"><span data-stu-id="009a3-152">hello elements of hello B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="009a3-153">Utilisation d’une invitation B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="009a3-153">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="009a3-154">Attribution de licences Azure AD B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="009a3-154">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="009a3-155">Résolution des problèmes d’Azure Active Directory B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="009a3-155">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="009a3-156">Questions fréquemment posées (FAQ) sur Azure Active Directory B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="009a3-156">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="009a3-157">API et personnalisation d’Azure Active Directory B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="009a3-157">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="009a3-158">Ajouter des utilisateurs B2B Collaboration sans invitation</span><span class="sxs-lookup"><span data-stu-id="009a3-158">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="009a3-159">Index d’articles pour la gestion des applications dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="009a3-159">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
