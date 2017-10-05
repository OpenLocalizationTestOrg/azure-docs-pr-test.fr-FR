---
title: "Limitations d’Azure Active Directory B2B Collaboration | Microsoft Docs"
description: "Limitations actuelles d’Azure Active Directory B2B Collaboration"
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
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: 581e5d1fb5fb08d0dc89ed2c85edcb5f0005650b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="limitations-of-azure-ad-b2b-collaboration"></a><span data-ttu-id="fae8a-103">Limitations d’Azure AD B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="fae8a-103">Limitations of Azure AD B2B collaboration</span></span>
<span data-ttu-id="fae8a-104">Azure Active Directory (Azure AD) B2B Collaboration subit actuellement les limitations décrites dans le présent article.</span><span class="sxs-lookup"><span data-stu-id="fae8a-104">Azure Active Directory (Azure AD) B2B collaboration is currently subject to the limitations described in this article.</span></span>

## <a name="possible-double-multi-factor-authentication"></a><span data-ttu-id="fae8a-105">Risque de redondance de l’authentification multifacteur</span><span class="sxs-lookup"><span data-stu-id="fae8a-105">Possible double multi-factor authentication</span></span>
<span data-ttu-id="fae8a-106">Avec Azure AD B2B, vous pouvez appliquer l’authentification multifacteur au niveau de l’organisation de la ressource (l’organisation à l’origine de l’invitation).</span><span class="sxs-lookup"><span data-stu-id="fae8a-106">With Azure AD B2B, you can enforce multi-factor authentication at the resource organization (the inviting organization).</span></span> <span data-ttu-id="fae8a-107">Les raisons de cette approche sont détaillées dans l’article [Conditional access for B2B collaboration users](active-directory-b2b-mfa-instructions.md) (Accès conditionnel pour les utilisateurs de B2B Collaboration).</span><span class="sxs-lookup"><span data-stu-id="fae8a-107">The reasons for this approach are detailed in [Conditional access for B2B collaboration users](active-directory-b2b-mfa-instructions.md).</span></span> <span data-ttu-id="fae8a-108">Si un partenaire a déjà configuré et appliqué l’authentification multifacteur, ses utilisateurs devront peut-être effectuer l’authentification une fois dans leur organisation d’origine, puis de nouveau dans les vôtres.</span><span class="sxs-lookup"><span data-stu-id="fae8a-108">If a partner already has multi-factor authentication set up and enforced, their users might have to perform the authentication once in their home organization and then again in yours.</span></span>

## <a name="instant-on"></a><span data-ttu-id="fae8a-109">Activation instantanée</span><span class="sxs-lookup"><span data-stu-id="fae8a-109">Instant-on</span></span>
<span data-ttu-id="fae8a-110">Dans les flux B2B Collaboration, nous ajoutons des utilisateurs au répertoire et les mettons à jour de manière dynamique pendant l’échange d’invitation, l’affectation d’application, etc.</span><span class="sxs-lookup"><span data-stu-id="fae8a-110">In the B2B collaboration flows, we add users to the directory and dynamically update them during invitation redemption, app assignment, and so on.</span></span> <span data-ttu-id="fae8a-111">Les mises à jour et les écritures se produisent d’ordinaire dans une instance de répertoire et doivent être répliquées entre toutes les instances.</span><span class="sxs-lookup"><span data-stu-id="fae8a-111">The updates and writes ordinarily happen in one directory instance and must be replicated across all instances.</span></span> <span data-ttu-id="fae8a-112">La réplication est terminée une fois toutes les instances mises à jour.</span><span class="sxs-lookup"><span data-stu-id="fae8a-112">Replication is completed once all instances are updated.</span></span> <span data-ttu-id="fae8a-113">Parfois, lorsque l’objet est écrit ou mis à jour dans une instance et quand l’appel pour récupérer cet objet se fait vers une autre instance, des latences de réplication peuvent se produire.</span><span class="sxs-lookup"><span data-stu-id="fae8a-113">Sometimes when the object is written or updated in one instance and the call to retrieve this object is to another instance, replication latencies can occur.</span></span> <span data-ttu-id="fae8a-114">Si cela se produit, actualisez ou recommencez.</span><span class="sxs-lookup"><span data-stu-id="fae8a-114">If that happens, refresh or retry to help.</span></span> <span data-ttu-id="fae8a-115">Si vous écrivez une application à l’aide de notre API, effectuer de nouvelles tentatives avec des temporisations peut être une pratique judicieuse et préventive pour atténuer ce problème.</span><span class="sxs-lookup"><span data-stu-id="fae8a-115">If you are writing an app using our API, then retries with some back-off is a good, defensive practice to alleviate this issue.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fae8a-116">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fae8a-116">Next steps</span></span>

<span data-ttu-id="fae8a-117">Consultez les autres articles sur la collaboration B2B d'Azure AD :</span><span class="sxs-lookup"><span data-stu-id="fae8a-117">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="fae8a-118">Qu’est-ce qu’Azure AD B2B Collaboration ?</span><span class="sxs-lookup"><span data-stu-id="fae8a-118">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="fae8a-119">Propriétés de l’utilisateur B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="fae8a-119">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="fae8a-120">Ajout d’un utilisateur B2B Collaboration à un rôle</span><span class="sxs-lookup"><span data-stu-id="fae8a-120">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="fae8a-121">Déléguer des invitations B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="fae8a-121">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="fae8a-122">Groupes dynamiques et B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="fae8a-122">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="fae8a-123">Code B2B Collaboration et exemples PowerShell</span><span class="sxs-lookup"><span data-stu-id="fae8a-123">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="fae8a-124">Configurer des applications SaaS pour B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="fae8a-124">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="fae8a-125">Jetons utilisateur B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="fae8a-125">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="fae8a-126">Mappage des revendications utilisateur B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="fae8a-126">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="fae8a-127">Partage externe d’Office 365</span><span class="sxs-lookup"><span data-stu-id="fae8a-127">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
