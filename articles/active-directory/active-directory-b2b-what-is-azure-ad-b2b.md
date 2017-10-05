---
title: "Qu’est-ce qu’Azure Active Directory B2B Collaboration ? | Microsoft Docs"
description: "Azure Active Directory B2B Collaboration prend en charge les relations interentreprises en permettant aux partenaires commerciaux d’accéder de façon sélective à vos applications d’entreprise."
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 1464387b-ee8b-4c7c-94b3-2c5567224c27
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 06/27/2017
ms.author: curtand
ms.custom: aaddev
ms.reviewer: sasubram
ms.openlocfilehash: fbc12a52555b190d43b5e953fd4d19923a25b0ed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-azure-ad-b2b-collaboration"></a><span data-ttu-id="0be88-104">Qu’est-ce qu’Azure AD B2B Collaboration ?</span><span class="sxs-lookup"><span data-stu-id="0be88-104">What is Azure AD B2B collaboration?</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/AhwrweCBdsc" frameborder="0" allowfullscreen></iframe>

<span data-ttu-id="0be88-105">Les fonctionnalités d’Azure AD business-to-business (B2B) Collaboration permettent à n’importe quelle organisation utilisant Azure AD de travailler en toute sécurité avec des utilisateurs de n’importe quelle autre organisation, petite ou grande.</span><span class="sxs-lookup"><span data-stu-id="0be88-105">Azure AD business-to-business (B2B) collaboration capabilities enable any organization using Azure AD to work safely and securely with users from any other organization, small or large.</span></span> <span data-ttu-id="0be88-106">Ces organisations peuvent être avec ou sans Azure AD, avec ou sans service informatique.</span><span class="sxs-lookup"><span data-stu-id="0be88-106">Those organizations can be with Azure AD or without, or even with an IT organization or without.</span></span> 

<span data-ttu-id="0be88-107">Les organisations utilisant Azure AD peuvent donner accès aux documents, ressources et applications à leurs partenaires, tout en conservant un contrôle complet sur leurs propres données d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="0be88-107">Organizations using Azure AD can provide access to documents, resources, and applications to their partners, while maintaining complete control over their own corporate data.</span></span> <span data-ttu-id="0be88-108">Les développeurs peuvent utiliser les API Azure AD business-to-business pour écrire des applications qui rapprochent deux organisations de manière sécurisée.</span><span class="sxs-lookup"><span data-stu-id="0be88-108">Developers can use the Azure AD business-to-business APIs to write applications that bring two organizations together in more securely.</span></span> <span data-ttu-id="0be88-109">En outre, la navigation est assez facile pour les utilisateurs finaux.</span><span class="sxs-lookup"><span data-stu-id="0be88-109">Also, it's pretty easy for end users to navigate.</span></span>

<span data-ttu-id="0be88-110">97 % de nos clients nous ont dit qu’Azure AD B2B Collaboration était très important pour eux.</span><span class="sxs-lookup"><span data-stu-id="0be88-110">97% of our customers have told us Azure AD B2B collaboration is very important to them.</span></span>

![Graphique à secteurs](media/active-directory-b2b-what-is-azure-ad-b2b/97-percent-support.png)

<span data-ttu-id="0be88-112">Dès début avril 2017, nous avions déjà près de trois millions d’utilisateurs bénéficiant des fonctionnalités d’Azure AD B2B Collaboration.</span><span class="sxs-lookup"><span data-stu-id="0be88-112">As of early April 2017, we had about 3 million users already using Azure AD B2B collaboration capabilities.</span></span> <span data-ttu-id="0be88-113">Et plus de 23 % des organisations Azure AD comptant plus de 10 utilisateurs tirent déjà parti de ces fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="0be88-113">And more than 23% of Azure AD organizations that have more than 10 users are already benefiting from these capabilities.</span></span>

## <a name="the-key-benefits-of-azure-ad-b2b-collaboration-to-your-organization"></a><span data-ttu-id="0be88-114">Principaux avantages d’Azure AD B2B Collaboration pour votre organisation</span><span class="sxs-lookup"><span data-stu-id="0be88-114">The key benefits of Azure AD B2B collaboration to your organization</span></span>

### <a name="work-with-any-user-from-any-partner"></a><span data-ttu-id="0be88-115">Travaillez avec n’importe quel utilisateur de n’importe quel partenaire</span><span class="sxs-lookup"><span data-stu-id="0be88-115">Work with any user from any partner</span></span>

* <span data-ttu-id="0be88-116">Les partenaires utilisent leurs propres informations d’identification</span><span class="sxs-lookup"><span data-stu-id="0be88-116">Partners use their own credentials</span></span>

* <span data-ttu-id="0be88-117">Aucune exigence pour les partenaires d’utiliser Azure AD</span><span class="sxs-lookup"><span data-stu-id="0be88-117">No requirement for partners to use Azure AD</span></span>

* <span data-ttu-id="0be88-118">Aucun répertoire externe ou configuration complexe requis</span><span class="sxs-lookup"><span data-stu-id="0be88-118">No external directories or complex set-up required</span></span>

### <a name="simple-and-secure-collaboration"></a><span data-ttu-id="0be88-119">Collaboration simple et sécurisée</span><span class="sxs-lookup"><span data-stu-id="0be88-119">Simple and secure collaboration</span></span>

* <span data-ttu-id="0be88-120">Permet l’accès à toutes données ou applications d’entreprise avec l’application de stratégies d’autorisation puissantes d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="0be88-120">Provide access to any corporate app or data, while applying sophisticated, Azure AD-powered authorization policies</span></span>

* <span data-ttu-id="0be88-121">Simplicité pour les utilisateurs</span><span class="sxs-lookup"><span data-stu-id="0be88-121">Easy for users</span></span>

* <span data-ttu-id="0be88-122">Sécurité d’entreprise pour les applications et les données</span><span class="sxs-lookup"><span data-stu-id="0be88-122">Enterprise-grade security for apps and data</span></span>

### <a name="no-management-overhead"></a><span data-ttu-id="0be88-123">Aucune surcharge de gestion</span><span class="sxs-lookup"><span data-stu-id="0be88-123">No management overhead</span></span>

* <span data-ttu-id="0be88-124">Aucune gestion de compte ou mot de passe externe</span><span class="sxs-lookup"><span data-stu-id="0be88-124">No external account or password management</span></span>

* <span data-ttu-id="0be88-125">Aucune gestion manuelle des synchronisations ou du cycle de vie des comptes</span><span class="sxs-lookup"><span data-stu-id="0be88-125">No sync or manual account lifecycle management</span></span>

* <span data-ttu-id="0be88-126">Aucune surcharge administrative externe</span><span class="sxs-lookup"><span data-stu-id="0be88-126">No external administrative overhead</span></span>

## <a name="you-can-easily-add-b2b-collaboration-users-to-your-organization"></a><span data-ttu-id="0be88-127">Vous pouvez facilement ajouter des utilisateurs B2B Collaboration à votre organisation</span><span class="sxs-lookup"><span data-stu-id="0be88-127">You can easily add B2B collaboration users to your organization</span></span>

<span data-ttu-id="0be88-128">Les administrateurs peuvent ajouter des utilisateurs (invités) B2B Collaboration dans le [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0be88-128">Admins can add B2B collaboration (guest) users in the [Azure portal](https://portal.azure.com).</span></span>

![ajouter des utilisateurs invités](media/active-directory-b2b-what-is-azure-ad-b2b/adding-b2b-users-admin.png)

### <a name="enable-your-collaborators-to-bring-their-own-identity"></a><span data-ttu-id="0be88-130">Permettez à vos collaborateurs d’utiliser leur propre identité</span><span class="sxs-lookup"><span data-stu-id="0be88-130">Enable your collaborators to bring their own identity</span></span>

<span data-ttu-id="0be88-131">Les collaborateurs B2B peuvent se connecter avec l’identité de leur choix.</span><span class="sxs-lookup"><span data-stu-id="0be88-131">B2B collaborators can sign in with an identity of their choice.</span></span> <span data-ttu-id="0be88-132">Si l’utilisateur n’a pas de compte Microsoft ou Azure AD, un compte est créé pour lui en toute transparence au moment de l’utilisation de l’offre.</span><span class="sxs-lookup"><span data-stu-id="0be88-132">If the user doesn’t have a Microsoft account or an Azure AD account – one is created for them seamlessly at the time for offer redemption.</span></span>

![choix de l’identité à la connexion](media/active-directory-b2b-what-is-azure-ad-b2b/sign-in-identity-choice.png)

### <a name="delegate-to-application-and-group-owners"></a><span data-ttu-id="0be88-134">Déléguez aux propriétaires d’applications et de groupes</span><span class="sxs-lookup"><span data-stu-id="0be88-134">Delegate to application and group owners</span></span> 
<span data-ttu-id="0be88-135">Les propriétaires d’applications et de groupes peuvent ajouter des utilisateurs B2B directement à n’importe quelle application qui vous intéresse, qu’il s’agisse d’une application Microsoft ou non.</span><span class="sxs-lookup"><span data-stu-id="0be88-135">Application and group owners can add B2B users directly to any application that you care about, whether it is a Microsoft application or not.</span></span> <span data-ttu-id="0be88-136">Les administrateurs peuvent déléguer l’autorisation d’ajouter des utilisateurs B2B aux utilisateurs non administrateurs.</span><span class="sxs-lookup"><span data-stu-id="0be88-136">Admins can delegate permission to add B2B users to non-admins.</span></span> <span data-ttu-id="0be88-137">Les utilisateurs non administrateurs peuvent utiliser le [volet d’accès aux applications Azure AD](https://myapps.microsoft.com) pour ajouter des utilisateurs B2B Collaboration aux applications ou aux groupes.</span><span class="sxs-lookup"><span data-stu-id="0be88-137">Non-admins can use the [Azure AD Application Access Panel](https://myapps.microsoft.com) to add B2B collaboration users to applications or groups.</span></span>

![volet d’accès](media/active-directory-b2b-what-is-azure-ad-b2b/access-panel.png)

![ajout d’un membre](media/active-directory-b2b-what-is-azure-ad-b2b/add-member.png)

### <a name="authorization-policies-protect-your-corporate-content"></a><span data-ttu-id="0be88-140">Les stratégies d’autorisation protègent votre contenu d’entreprise</span><span class="sxs-lookup"><span data-stu-id="0be88-140">Authorization policies protect your corporate content</span></span>

<span data-ttu-id="0be88-141">Les stratégies d’accès conditionnel, telles que l’authentification multifacteur, peuvent être appliquées :</span><span class="sxs-lookup"><span data-stu-id="0be88-141">Conditional access policies, such as multi-factor authentication, can be enforced:</span></span>
- <span data-ttu-id="0be88-142">Au niveau du locataire</span><span class="sxs-lookup"><span data-stu-id="0be88-142">At the tenant level</span></span>
- <span data-ttu-id="0be88-143">Au niveau de l’application</span><span class="sxs-lookup"><span data-stu-id="0be88-143">At the application level</span></span>
- <span data-ttu-id="0be88-144">Pour des utilisateurs spécifiques afin de protéger les données et les applications d’entreprise</span><span class="sxs-lookup"><span data-stu-id="0be88-144">For specific users to protect corporate apps and data</span></span>

![ajout d’un membre](media/active-directory-b2b-what-is-azure-ad-b2b/add-member.png)

### <a name="use-our-apis-and-sample-code-to-easily-build-applications-to-onboard"></a><span data-ttu-id="0be88-146">Utilisez nos API et l’exemple de code pour créer facilement des applications à intégrer</span><span class="sxs-lookup"><span data-stu-id="0be88-146">Use our APIs and sample code to easily build applications to onboard</span></span>
<span data-ttu-id="0be88-147">Intégrez vos partenaires externes de façon personnalisée en fonction des besoins de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="0be88-147">Bring your external partners on board in ways customized to your organization’s needs.</span></span>

<span data-ttu-id="0be88-148">À l’aide de nos [API d’invitation B2B Collaboration](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation), vous pouvez personnaliser votre expérience d’intégration, notamment créer des portails d’inscription libre-service.</span><span class="sxs-lookup"><span data-stu-id="0be88-148">Using the [B2B collaboration invitation APIs](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation), you can customize your onboarding experiences, including creating self-service sign-up portals.</span></span> <span data-ttu-id="0be88-149">Nous fournissons un exemple de code pour un portail libre-service [sur Github](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).</span><span class="sxs-lookup"><span data-stu-id="0be88-149">We provide sample code for a self-service portal [on Github](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).</span></span>

![portail d’inscription](media/active-directory-b2b-what-is-azure-ad-b2b/sign-up-portal.png)

<span data-ttu-id="0be88-151">Avec Azure AD B2B Collaboration, vous pouvez tirer parti de la puissance d’Azure AD pour protéger vos relations avec vos partenaires de façon simple et intuitive pour vos utilisateurs finaux.</span><span class="sxs-lookup"><span data-stu-id="0be88-151">With Azure AD B2B collaboration, you can get the full power of Azure AD to protect your partner relationships in a way that end users find easy and intuitive.</span></span> <span data-ttu-id="0be88-152">Alors n’hésitez pas, rejoignez les milliers d’organisations qui utilisent déjà Azure AD B2B pour leur collaboration externe !</span><span class="sxs-lookup"><span data-stu-id="0be88-152">So go ahead, join the thousands of organizations that are already using Azure AD B2B for their external collaboration!</span></span>

## <a name="next-steps"></a><span data-ttu-id="0be88-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0be88-153">Next steps</span></span>

* <span data-ttu-id="0be88-154">Les expériences d’administrateurs sont trouvent dans le [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0be88-154">Administrator experiences are found in the [Azure portal](https://portal.azure.com).</span></span>

* <span data-ttu-id="0be88-155">Les expériences de professionnels de l’information sont disponibles dans le [volet d’accès](https://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="0be88-155">Information worker experiences are available in the [Access Panel](https://myapps.microsoft.com).</span></span>

* <span data-ttu-id="0be88-156">Et, comme toujours, contactez l’équipe produit pour vos commentaires, discussions et suggestions par le biais de notre [Communauté technologique Microsoft](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B/bd-p/AzureAD_B2b).</span><span class="sxs-lookup"><span data-stu-id="0be88-156">And, as always, connect with the product team for any feedback, discussions, and suggestions through our [Microsoft Tech Community](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B/bd-p/AzureAD_B2b).</span></span>

<span data-ttu-id="0be88-157">Consultez les autres articles sur la collaboration B2B d'Azure AD :</span><span class="sxs-lookup"><span data-stu-id="0be88-157">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="0be88-158">Comment les administrateurs Azure Active Directory ajoutent-ils des utilisateurs B2B Collaboration ?</span><span class="sxs-lookup"><span data-stu-id="0be88-158">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="0be88-159">Comment les professionnels de l’information ajoutent-ils des utilisateurs B2B Collaboration ?</span><span class="sxs-lookup"><span data-stu-id="0be88-159">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="0be88-160">Éléments de l’e-mail d’invitation de B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="0be88-160">The elements of the B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="0be88-161">Utilisation d’une invitation B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="0be88-161">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="0be88-162">Attribution de licences Azure AD B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="0be88-162">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="0be88-163">Résolution des problèmes d’Azure Active Directory B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="0be88-163">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="0be88-164">Questions fréquemment posées (FAQ) sur Azure Active Directory B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="0be88-164">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="0be88-165">API et personnalisation d’Azure Active Directory B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="0be88-165">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="0be88-166">Authentification multifacteur pour les utilisateurs B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="0be88-166">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="0be88-167">Ajouter des utilisateurs B2B Collaboration sans invitation</span><span class="sxs-lookup"><span data-stu-id="0be88-167">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* <span data-ttu-id="0be88-168">[B2B collaboration user auditing and reporting](active-directory-b2b-auditing-and-reporting.md) (Audit et création de rapports relatifs aux utilisateurs B2B Collaboration)</span><span class="sxs-lookup"><span data-stu-id="0be88-168">[B2B collaboration user auditing and reporting](active-directory-b2b-auditing-and-reporting.md)</span></span>
* [<span data-ttu-id="0be88-169">Index d’articles pour la gestion des applications dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0be88-169">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
