---
title: "Ajouter des utilisateurs B2B Collaboration à Azure Active Directory sans invitation | Microsoft Docs"
description: "Vous pouvez permettre à un utilisateur invité d’ajouter d’autres utilisateurs invités à votre Azure AD sans échanger d’invitation dans Azure Active Directory B2B Collaboration."
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
ms.date: 03/15/2017
ms.author: sasubram
ms.openlocfilehash: 91b9477cdb679851e7d8d2942c06999a05f64e46
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="add-b2b-collaboration-guest-users-without-an-invitation"></a><span data-ttu-id="37dfe-103">Ajouter des utilisateurs invités B2B Collaboration sans invitation</span><span class="sxs-lookup"><span data-stu-id="37dfe-103">Add B2B collaboration guest users without an invitation</span></span>

<span data-ttu-id="37dfe-104">Vous pouvez autoriser un utilisateur, tel qu’un représentant de partenaire, à ajouter des utilisateurs du partenaire vers votre organisation sans avoir à échanger des invitations.</span><span class="sxs-lookup"><span data-stu-id="37dfe-104">You can allow a user, such as a partner representative, to add users from the partner to your organization without needing invitations to be redeemed.</span></span> <span data-ttu-id="37dfe-105">Il vous suffit d’accorder à cet utilisateur des privilèges d’énumération dans le répertoire que vous utilisez pour l’organisation partenaire.</span><span class="sxs-lookup"><span data-stu-id="37dfe-105">All you must do is grant that user enumeration privileges in the directory you're using for the partner org.</span></span> 

<span data-ttu-id="37dfe-106">Accordez ces privilèges lorsque :</span><span class="sxs-lookup"><span data-stu-id="37dfe-106">Grant these privileges when:</span></span>

1. <span data-ttu-id="37dfe-107">Un utilisateur de l’organisation hôte (par exemple, WoodGrove) invite un utilisateur d’une organisation partenaire (par exemple, Sam@litware.com) en tant qu’invité.</span><span class="sxs-lookup"><span data-stu-id="37dfe-107">A user in the host organization (for example, WoodGrove) invites one user from the partner organization (for example, Sam@litware.com) as Guest.</span></span>
2. <span data-ttu-id="37dfe-108">L’administrateur de l’organisation hôte définit les stratégies qui permettent à Sam d’identifier et d’ajouter d’autres utilisateurs de l’organisation partenaire (Litware).</span><span class="sxs-lookup"><span data-stu-id="37dfe-108">The admin in the host organization sets up policies that allow Sam to identify and add other users from the partner organization (Litware).</span></span>
3. <span data-ttu-id="37dfe-109">Maintenant, Sam peut ajouter d’autres utilisateurs Litware au répertoire, à des groupes et à des applications WoodGrove sans avoir besoin d’utiliser des invitations.</span><span class="sxs-lookup"><span data-stu-id="37dfe-109">Now Sam can add other users from Litware to the WoodGrove directory, groups, or applications without needing invitations to be redeemed.</span></span> <span data-ttu-id="37dfe-110">Si Sam possède les privilèges d’énumération appropriés de Litware, cela se produit automatiquement.</span><span class="sxs-lookup"><span data-stu-id="37dfe-110">If Sam has the appropriate enumeration privileges in Litware, it happens automatically.</span></span>

### <a name="next-steps"></a><span data-ttu-id="37dfe-111">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="37dfe-111">Next steps</span></span>

<span data-ttu-id="37dfe-112">Consultez les autres articles sur la collaboration B2B d'Azure AD :</span><span class="sxs-lookup"><span data-stu-id="37dfe-112">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="37dfe-113">Qu’est-ce qu’Azure AD B2B Collaboration ?</span><span class="sxs-lookup"><span data-stu-id="37dfe-113">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="37dfe-114">Comment les administrateurs Azure Active Directory ajoutent-ils des utilisateurs B2B Collaboration ?</span><span class="sxs-lookup"><span data-stu-id="37dfe-114">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="37dfe-115">Comment les professionnels de l’information ajoutent-ils des utilisateurs B2B Collaboration ?</span><span class="sxs-lookup"><span data-stu-id="37dfe-115">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="37dfe-116">Éléments de l’e-mail d’invitation de B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="37dfe-116">The elements of the B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="37dfe-117">Utilisation d’une invitation B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="37dfe-117">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="37dfe-118">Attribution de licences Azure AD B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="37dfe-118">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="37dfe-119">Résolution des problèmes d’Azure Active Directory B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="37dfe-119">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="37dfe-120">Questions fréquemment posées (FAQ) sur Azure Active Directory B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="37dfe-120">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="37dfe-121">API et personnalisation d’Azure Active Directory B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="37dfe-121">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="37dfe-122">Authentification multifacteur pour les utilisateurs B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="37dfe-122">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="37dfe-123">Index d’articles pour la gestion des applications dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="37dfe-123">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)