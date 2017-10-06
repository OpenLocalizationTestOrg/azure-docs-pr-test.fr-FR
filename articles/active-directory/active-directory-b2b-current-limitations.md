---
title: "aaaLimitations d’Azure Active Directory B2B collaboration | Documents Microsoft"
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
ms.openlocfilehash: 322081f32fbacfe67ee1300993c7df1870e498bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-of-azure-ad-b2b-collaboration"></a><span data-ttu-id="40b77-103">Limitations d’Azure AD B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="40b77-103">Limitations of Azure AD B2B collaboration</span></span>
<span data-ttu-id="40b77-104">Azure Active Directory (Azure AD) B2B collaboration est actuellement les limitations de toohello sujet décrites dans cet article.</span><span class="sxs-lookup"><span data-stu-id="40b77-104">Azure Active Directory (Azure AD) B2B collaboration is currently subject toohello limitations described in this article.</span></span>

## <a name="possible-double-multi-factor-authentication"></a><span data-ttu-id="40b77-105">Risque de redondance de l’authentification multifacteur</span><span class="sxs-lookup"><span data-stu-id="40b77-105">Possible double multi-factor authentication</span></span>
<span data-ttu-id="40b77-106">Avec Azure AD B2B, vous pouvez appliquer l’authentification multifacteur à l’organisation de ressource hello (hello invitation d’organisation).</span><span class="sxs-lookup"><span data-stu-id="40b77-106">With Azure AD B2B, you can enforce multi-factor authentication at hello resource organization (hello inviting organization).</span></span> <span data-ttu-id="40b77-107">raisons Hello de cette approche sont détaillées dans [accès conditionnel pour les utilisateurs de collaboration B2B](active-directory-b2b-mfa-instructions.md).</span><span class="sxs-lookup"><span data-stu-id="40b77-107">hello reasons for this approach are detailed in [Conditional access for B2B collaboration users](active-directory-b2b-mfa-instructions.md).</span></span> <span data-ttu-id="40b77-108">Si un partenaire possède déjà plusieurs facteurs d’authentification configuré et appliquée, leurs les utilisateurs peuvent avoir l’authentification hello tooperform qu’une seule fois dans leur organisation d’origine, puis à nouveau dans le vôtre.</span><span class="sxs-lookup"><span data-stu-id="40b77-108">If a partner already has multi-factor authentication set up and enforced, their users might have tooperform hello authentication once in their home organization and then again in yours.</span></span>

## <a name="instant-on"></a><span data-ttu-id="40b77-109">Activation instantanée</span><span class="sxs-lookup"><span data-stu-id="40b77-109">Instant-on</span></span>
<span data-ttu-id="40b77-110">Dans le flux de collaboration hello B2B, nous ajouter les utilisateurs toohello répertoire et les mettre à jour dynamiquement pendant l’échange d’invitation, assignation d’application et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="40b77-110">In hello B2B collaboration flows, we add users toohello directory and dynamically update them during invitation redemption, app assignment, and so on.</span></span> <span data-ttu-id="40b77-111">Hello les mises à jour et les écritures normalement se produisent dans une instance d’un répertoire et doivent être répliqués sur toutes les instances.</span><span class="sxs-lookup"><span data-stu-id="40b77-111">hello updates and writes ordinarily happen in one directory instance and must be replicated across all instances.</span></span> <span data-ttu-id="40b77-112">La réplication est terminée une fois toutes les instances mises à jour.</span><span class="sxs-lookup"><span data-stu-id="40b77-112">Replication is completed once all instances are updated.</span></span> <span data-ttu-id="40b77-113">Lorsque hello objet est écrit ou mis à jour dans une seule instance et hello appeler tooretrieve cet objet est parfois tooanother instance, des latences de réplication peuvent se produire.</span><span class="sxs-lookup"><span data-stu-id="40b77-113">Sometimes when hello object is written or updated in one instance and hello call tooretrieve this object is tooanother instance, replication latencies can occur.</span></span> <span data-ttu-id="40b77-114">Si cela se produit, actualisez ou réessayez toohelp.</span><span class="sxs-lookup"><span data-stu-id="40b77-114">If that happens, refresh or retry toohelp.</span></span> <span data-ttu-id="40b77-115">Si vous écrivez une application à l’aide de notre API, puis les nouvelles tentatives avec certains temporisation est un tooalleviate correct, la pratique ce problème.</span><span class="sxs-lookup"><span data-stu-id="40b77-115">If you are writing an app using our API, then retries with some back-off is a good, defensive practice tooalleviate this issue.</span></span>

## <a name="next-steps"></a><span data-ttu-id="40b77-116">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="40b77-116">Next steps</span></span>

<span data-ttu-id="40b77-117">Consultez les autres articles sur la collaboration B2B d'Azure AD :</span><span class="sxs-lookup"><span data-stu-id="40b77-117">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="40b77-118">Qu’est-ce qu’Azure AD B2B Collaboration ?</span><span class="sxs-lookup"><span data-stu-id="40b77-118">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="40b77-119">Propriétés de l’utilisateur B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="40b77-119">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="40b77-120">Ajout d’un rôle tooa B2B collaboration</span><span class="sxs-lookup"><span data-stu-id="40b77-120">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="40b77-121">Déléguer des invitations B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="40b77-121">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="40b77-122">Groupes dynamiques et B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="40b77-122">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="40b77-123">Code B2B Collaboration et exemples PowerShell</span><span class="sxs-lookup"><span data-stu-id="40b77-123">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="40b77-124">Configurer des applications SaaS pour B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="40b77-124">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="40b77-125">Jetons utilisateur B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="40b77-125">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="40b77-126">Mappage des revendications utilisateur B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="40b77-126">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="40b77-127">Partage externe d’Office 365</span><span class="sxs-lookup"><span data-stu-id="40b77-127">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
