---
title: aaaAdd B2B collaboration utilisateurs tooAzure Active Directory sans invitation | Documents Microsoft
description: "Vous pouvez permettre à un utilisateur invité d’ajouter d’autres tooyour d’utilisateurs invités Azure AD sans échange une invitation dans Azure Active Directory B2B collaboration."
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
ms.openlocfilehash: 459d99b9f856a35973d1b2cbfabdc23fe40c8f44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-b2b-collaboration-guest-users-without-an-invitation"></a><span data-ttu-id="52617-103">Ajouter des utilisateurs invités B2B Collaboration sans invitation</span><span class="sxs-lookup"><span data-stu-id="52617-103">Add B2B collaboration guest users without an invitation</span></span>

<span data-ttu-id="52617-104">Vous pouvez autoriser un utilisateur, par exemple un partenaire représentatif, tooadd les utilisateurs de hello partenaire tooyour organisation sans avoir besoin de toobe invitations échangé.</span><span class="sxs-lookup"><span data-stu-id="52617-104">You can allow a user, such as a partner representative, tooadd users from hello partner tooyour organization without needing invitations toobe redeemed.</span></span> <span data-ttu-id="52617-105">Il vous suffit est lui accorder les privilèges d’énumération dans le répertoire de hello vous utilisez pour l’organisation du partenaire hello</span><span class="sxs-lookup"><span data-stu-id="52617-105">All you must do is grant that user enumeration privileges in hello directory you're using for hello partner org.</span></span> 

<span data-ttu-id="52617-106">Accordez ces privilèges lorsque :</span><span class="sxs-lookup"><span data-stu-id="52617-106">Grant these privileges when:</span></span>

1. <span data-ttu-id="52617-107">Un utilisateur d’organisation d’hôte hello (par exemple, WoodGrove) invite un utilisateur à partir de l’organisation partenaire de hello (par exemple, Sam@litware.com) en tant qu’invité.</span><span class="sxs-lookup"><span data-stu-id="52617-107">A user in hello host organization (for example, WoodGrove) invites one user from hello partner organization (for example, Sam@litware.com) as Guest.</span></span>
2. <span data-ttu-id="52617-108">admin Hello dans l’organisation d’hôte hello définit les stratégies qui permettent de Sam tooidentify et ajouter d’autres utilisateurs de l’organisation partenaire de hello (Litware).</span><span class="sxs-lookup"><span data-stu-id="52617-108">hello admin in hello host organization sets up policies that allow Sam tooidentify and add other users from hello partner organization (Litware).</span></span>
3. <span data-ttu-id="52617-109">Maintenant Sam peut ajouter d’autres utilisateurs d’annuaire de Litware toohello WoodGrove, des groupes ou des applications sans avoir besoin de toobe des invitations à participer à échanger.</span><span class="sxs-lookup"><span data-stu-id="52617-109">Now Sam can add other users from Litware toohello WoodGrove directory, groups, or applications without needing invitations toobe redeemed.</span></span> <span data-ttu-id="52617-110">Si Sam dispose de privilèges d’énumération appropriée de hello dans Litware, il se produit automatiquement.</span><span class="sxs-lookup"><span data-stu-id="52617-110">If Sam has hello appropriate enumeration privileges in Litware, it happens automatically.</span></span>

### <a name="next-steps"></a><span data-ttu-id="52617-111">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="52617-111">Next steps</span></span>

<span data-ttu-id="52617-112">Consultez les autres articles sur la collaboration B2B d'Azure AD :</span><span class="sxs-lookup"><span data-stu-id="52617-112">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="52617-113">Qu’est-ce qu’Azure AD B2B Collaboration ?</span><span class="sxs-lookup"><span data-stu-id="52617-113">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="52617-114">Comment les administrateurs Azure Active Directory ajoutent-ils des utilisateurs B2B Collaboration ?</span><span class="sxs-lookup"><span data-stu-id="52617-114">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="52617-115">Comment les professionnels de l’information ajoutent-ils des utilisateurs B2B Collaboration ?</span><span class="sxs-lookup"><span data-stu-id="52617-115">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="52617-116">éléments Hello Hello e-mail d’invitation B2B collaboration</span><span class="sxs-lookup"><span data-stu-id="52617-116">hello elements of hello B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="52617-117">Utilisation d’une invitation B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="52617-117">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="52617-118">Attribution de licences Azure AD B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="52617-118">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="52617-119">Résolution des problèmes d’Azure Active Directory B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="52617-119">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="52617-120">Questions fréquemment posées (FAQ) sur Azure Active Directory B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="52617-120">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="52617-121">API et personnalisation d’Azure Active Directory B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="52617-121">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="52617-122">Authentification multifacteur pour les utilisateurs B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="52617-122">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="52617-123">Index d’articles pour la gestion des applications dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="52617-123">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)