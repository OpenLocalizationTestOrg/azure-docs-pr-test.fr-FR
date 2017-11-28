---
title: "rôle tooa aaaAdd un B2B Active Directory de Azure collaboration | Documents Microsoft"
description: "Ajouter un rôle tooa d’utilisateur invité dans Azure Active Directory"
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
ms.openlocfilehash: ccc58a0c8ecc73f8e79a8d827efdc0ff93846a96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="grant-permissions-toousers-from-partner-organizations-in-your-azure-active-directory-tenant"></a><span data-ttu-id="98b73-103">Accorder des autorisations toousers des organisations partenaires dans votre locataire Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="98b73-103">Grant permissions toousers from partner organizations in your Azure Active Directory tenant</span></span>

<span data-ttu-id="98b73-104">Azure Active Directory (Azure AD) B2B collaboration les utilisateurs sont ajoutés en tant que répertoire de toohello les utilisateurs invités et les autorisations invité dans le répertoire de hello sont limitées par défaut.</span><span class="sxs-lookup"><span data-stu-id="98b73-104">Azure Active Directory (Azure AD) B2B collaboration users are added as guest users toohello directory, and guest permissions in hello directory are restricted by default.</span></span> <span data-ttu-id="98b73-105">Votre entreprise peut-être certains rôles invité utilisateurs toofill privilège plus élevé dans votre organisation.</span><span class="sxs-lookup"><span data-stu-id="98b73-105">Your business may need some guest users toofill higher-privilege roles in your organization.</span></span> <span data-ttu-id="98b73-106">toosupport définition des rôles de privilège plus élevé, les utilisateurs invités peuvent être des rôles tooany ajouté souhaitée, en fonction des besoins de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="98b73-106">toosupport defining higher-privilege roles, guest users can be added tooany roles you desire, based on your organization's needs.</span></span>

## <a name="default-role"></a><span data-ttu-id="98b73-107">Rôle par défaut</span><span class="sxs-lookup"><span data-stu-id="98b73-107">Default role</span></span>

![rôle par défaut](./media/active-directory-b2b-add-guest-to-role/default-role.png)

## <a name="global-administrator-role"></a><span data-ttu-id="98b73-109">Rôle Administrateur général</span><span class="sxs-lookup"><span data-stu-id="98b73-109">Global Administrator Role</span></span>

![rôle administrateur général](./media/active-directory-b2b-add-guest-to-role/global-admin-role.png)

## <a name="limited-administrator-role"></a><span data-ttu-id="98b73-111">Rôle Administrateur limité</span><span class="sxs-lookup"><span data-stu-id="98b73-111">Limited Administrator Role</span></span>

![rôle administrateur limité](./media/active-directory-b2b-add-guest-to-role/limited-admin-role.png)

## <a name="next-steps"></a><span data-ttu-id="98b73-113">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="98b73-113">Next steps</span></span>

<span data-ttu-id="98b73-114">Consultez les autres articles sur la collaboration B2B d'Azure AD :</span><span class="sxs-lookup"><span data-stu-id="98b73-114">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="98b73-115">Qu’est-ce qu’Azure AD B2B Collaboration ?</span><span class="sxs-lookup"><span data-stu-id="98b73-115">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="98b73-116">Propriétés de l’utilisateur B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="98b73-116">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="98b73-117">Déléguer des invitations B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="98b73-117">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="98b73-118">Groupes dynamiques et B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="98b73-118">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="98b73-119">Code B2B Collaboration et exemples PowerShell</span><span class="sxs-lookup"><span data-stu-id="98b73-119">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="98b73-120">Configurer des applications SaaS pour B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="98b73-120">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="98b73-121">Jetons utilisateur B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="98b73-121">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="98b73-122">Mappage des revendications utilisateur B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="98b73-122">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="98b73-123">Partage externe d’Office 365</span><span class="sxs-lookup"><span data-stu-id="98b73-123">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="98b73-124">Limitations actuelles de B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="98b73-124">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
