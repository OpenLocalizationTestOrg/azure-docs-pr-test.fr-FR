---
title: "Ajouter un utilisateur Azure Active Directory B2B Collaboration à un rôle | Microsoft Docs"
description: "Ajouter un utilisateur invité à un rôle dans Azure Active Directory"
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
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e816349ea971c997f655b4d51672dba666bc3e89
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="grant-permissions-to-users-from-partner-organizations-in-your-azure-active-directory-tenant"></a><span data-ttu-id="16efe-103">Accorder des autorisations aux utilisateurs d’organisations partenaires dans votre locataire Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="16efe-103">Grant permissions to users from partner organizations in your Azure Active Directory tenant</span></span>

<span data-ttu-id="16efe-104">Les utilisateurs Azure Active Directory (Azure AD) B2B Collaboration sont ajoutés en tant qu’utilisateurs invités au répertoire et les autorisations des invités dans le répertoire sont restreintes par défaut.</span><span class="sxs-lookup"><span data-stu-id="16efe-104">Azure Active Directory (Azure AD) B2B collaboration users are added as guest users to the directory, and guest permissions in the directory are restricted by default.</span></span> <span data-ttu-id="16efe-105">Votre entreprise a peut-être besoin que certains utilisateurs invités occupent des rôles avec davantage de privilèges dans votre organisation.</span><span class="sxs-lookup"><span data-stu-id="16efe-105">Your business may need some guest users to fill higher-privilege roles in your organization.</span></span> <span data-ttu-id="16efe-106">Pour prendre la définition de rôles avec davantage de privilèges, les utilisateurs invités peuvent être ajoutés à n’importe quel rôle souhaité, en fonction des besoins de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="16efe-106">To support defining higher-privilege roles, guest users can be added to any roles you desire, based on your organization's needs.</span></span>

## <a name="default-role"></a><span data-ttu-id="16efe-107">Rôle par défaut</span><span class="sxs-lookup"><span data-stu-id="16efe-107">Default role</span></span>

![rôle par défaut](./media/active-directory-b2b-add-guest-to-role/default-role.png)

## <a name="global-administrator-role"></a><span data-ttu-id="16efe-109">Rôle Administrateur général</span><span class="sxs-lookup"><span data-stu-id="16efe-109">Global Administrator Role</span></span>

![rôle administrateur général](./media/active-directory-b2b-add-guest-to-role/global-admin-role.png)

## <a name="limited-administrator-role"></a><span data-ttu-id="16efe-111">Rôle Administrateur limité</span><span class="sxs-lookup"><span data-stu-id="16efe-111">Limited Administrator Role</span></span>

![rôle administrateur limité](./media/active-directory-b2b-add-guest-to-role/limited-admin-role.png)

## <a name="next-steps"></a><span data-ttu-id="16efe-113">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="16efe-113">Next steps</span></span>

<span data-ttu-id="16efe-114">Consultez les autres articles sur la collaboration B2B d'Azure AD :</span><span class="sxs-lookup"><span data-stu-id="16efe-114">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="16efe-115">Qu’est-ce qu’Azure AD B2B Collaboration ?</span><span class="sxs-lookup"><span data-stu-id="16efe-115">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="16efe-116">Propriétés de l’utilisateur B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="16efe-116">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="16efe-117">Déléguer des invitations B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="16efe-117">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="16efe-118">Groupes dynamiques et B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="16efe-118">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="16efe-119">Code B2B Collaboration et exemples PowerShell</span><span class="sxs-lookup"><span data-stu-id="16efe-119">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="16efe-120">Configurer des applications SaaS pour B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="16efe-120">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="16efe-121">Jetons utilisateur B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="16efe-121">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="16efe-122">Mappage des revendications utilisateur B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="16efe-122">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="16efe-123">Partage externe d’Office 365</span><span class="sxs-lookup"><span data-stu-id="16efe-123">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="16efe-124">Limitations actuelles de B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="16efe-124">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
