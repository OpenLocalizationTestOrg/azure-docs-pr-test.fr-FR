---
title: "Déléguer des invitations pour Azure Active Directory B2B Collaboration | Microsoft Docs"
description: "Les propriétés de l’utilisateur Azure Active Directory B2B Collaboration sont configurables"
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
ms.openlocfilehash: 78613cc978b585a98d235245194c02371f7f3849
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="delegate-invitations-for-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="7c1cf-103">Déléguer des invitations pour Azure Active Directory B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="7c1cf-103">Delegate invitations for Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="7c1cf-104">Avec Azure Active Directory (Azure AD) B2B Collaboration, il n’est pas nécessaire d’être un administrateur global pour envoyer des invitations.</span><span class="sxs-lookup"><span data-stu-id="7c1cf-104">With Azure Active Directory (Azure AD) business-to-business (B2B) collaboration, you do not have to be a global admin to send invitations.</span></span> <span data-ttu-id="7c1cf-105">Vous pouvez utiliser des stratégies et déléguer des invitations aux utilisateurs dont les rôles les autorisent à envoyer des invitations.</span><span class="sxs-lookup"><span data-stu-id="7c1cf-105">Instead, you can use policies and delegate invitations to users whose roles allow them to send invitations.</span></span> <span data-ttu-id="7c1cf-106">Le rôle Inviteur d’invités est une nouvelle façon importante de déléguer les invitations d’utilisateurs invités.</span><span class="sxs-lookup"><span data-stu-id="7c1cf-106">An important new way to delegate guest user invitations is through the Guest Inviter role.</span></span>

## <a name="guest-inviter-role"></a><span data-ttu-id="7c1cf-107">Rôle Inviteur d’invités</span><span class="sxs-lookup"><span data-stu-id="7c1cf-107">Guest Inviter role</span></span>
<span data-ttu-id="7c1cf-108">Il est possible d’affecter l’utilisateur au rôle Inviteur d’invités pour envoyer des invitations.</span><span class="sxs-lookup"><span data-stu-id="7c1cf-108">We can assign the user to Guest Inviter role to send invitations.</span></span> <span data-ttu-id="7c1cf-109">Vous n’êtes pas tenu d’être membre du rôle Administrateur général pour envoyer des invitations.</span><span class="sxs-lookup"><span data-stu-id="7c1cf-109">You don't have to be member of the global admin role to send invitations.</span></span> <span data-ttu-id="7c1cf-110">Par défaut, les utilisateurs standard peuvent également appeler l’API d’invitation, sauf si un administrateur général a désactivé les invitations à leur intention.</span><span class="sxs-lookup"><span data-stu-id="7c1cf-110">By default, regular users can also invoke the invite API unless a global admin disabled invitations for regular users.</span></span> <span data-ttu-id="7c1cf-111">Un utilisateur peut également appeler l’API à l’aide du portail Azure ou de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7c1cf-111">A user can also invoke the API using the Azure portal or PowerShell.</span></span>

<span data-ttu-id="7c1cf-112">Voici un exemple qui montre comment utiliser PowerShell pour ajouter un utilisateur au rôle Inviteur d’invités :</span><span class="sxs-lookup"><span data-stu-id="7c1cf-112">Here's an example that shows how to use PowerShell to add a user to the Guest Inviter role:</span></span>

```
Add-MsolRoleMember -RoleObjectId 95e79109-95c0-4d8e-aee3-d01accf2d47b -RoleMemberEmailAddress <RoleMemberEmailAddress>
```

## <a name="control-who-can-invite"></a><span data-ttu-id="7c1cf-113">Contrôler qui peut inviter</span><span class="sxs-lookup"><span data-stu-id="7c1cf-113">Control who can invite</span></span>

![Contrôler comment inviter](media/active-directory-b2b-delegate-invitations/control-who-to-invite.png)

<span data-ttu-id="7c1cf-115">Avec Azure AD B2B Collaboration, un administrateur de clients peut définir les stratégies d’invitation suivantes :</span><span class="sxs-lookup"><span data-stu-id="7c1cf-115">With Azure AD B2B collaboration, a tenant admin can set the following invitation policies:</span></span>

- <span data-ttu-id="7c1cf-116">Désactiver les invitations</span><span class="sxs-lookup"><span data-stu-id="7c1cf-116">Turn off invitations</span></span>
- <span data-ttu-id="7c1cf-117">Seuls les administrateurs et les utilisateurs membres du rôle Inviteur d’invités peuvent envoyer des invitations</span><span class="sxs-lookup"><span data-stu-id="7c1cf-117">Only admins and users in the Guest Inviter role can invite</span></span>
- <span data-ttu-id="7c1cf-118">Les administrateurs, le rôle Inviteur d’invités et les membres peuvent envoyer des invitations</span><span class="sxs-lookup"><span data-stu-id="7c1cf-118">Admins, the Guest Inviter role, and members can invite</span></span>
- <span data-ttu-id="7c1cf-119">Tous les utilisateurs, notamment les invités, peuvent inviter</span><span class="sxs-lookup"><span data-stu-id="7c1cf-119">All users, including guests, can invite</span></span>

<span data-ttu-id="7c1cf-120">Par défaut, les clients sont définis sur 4.</span><span class="sxs-lookup"><span data-stu-id="7c1cf-120">By default, tenants are set to #4.</span></span> <span data-ttu-id="7c1cf-121">Tous les utilisateurs, notamment les invités, peuvent inviter des utilisateurs B2B.</span><span class="sxs-lookup"><span data-stu-id="7c1cf-121">(All users, including guests, can invite B2B users.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="7c1cf-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7c1cf-122">Next steps</span></span>

<span data-ttu-id="7c1cf-123">Consultez les autres articles sur la collaboration B2B d'Azure AD :</span><span class="sxs-lookup"><span data-stu-id="7c1cf-123">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="7c1cf-124">Qu’est-ce qu’Azure AD B2B Collaboration ?</span><span class="sxs-lookup"><span data-stu-id="7c1cf-124">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="7c1cf-125">Propriétés de l’utilisateur B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="7c1cf-125">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="7c1cf-126">Ajout d’un utilisateur B2B Collaboration à un rôle</span><span class="sxs-lookup"><span data-stu-id="7c1cf-126">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="7c1cf-127">Groupes dynamiques et B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="7c1cf-127">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="7c1cf-128">Code B2B Collaboration et exemples PowerShell</span><span class="sxs-lookup"><span data-stu-id="7c1cf-128">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="7c1cf-129">Configurer des applications SaaS pour B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="7c1cf-129">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="7c1cf-130">Jetons utilisateur B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="7c1cf-130">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="7c1cf-131">Mappage des revendications utilisateur B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="7c1cf-131">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="7c1cf-132">Partage externe d’Office 365</span><span class="sxs-lookup"><span data-stu-id="7c1cf-132">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="7c1cf-133">Limitations actuelles de B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="7c1cf-133">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
