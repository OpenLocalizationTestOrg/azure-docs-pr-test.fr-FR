---
title: invitations aaaDelegate pour Azure Active Directory B2B collaboration | Documents Microsoft
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
ms.openlocfilehash: c0122d6f60d494c6e251c41d947dc254ea887620
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="delegate-invitations-for-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="17244-103">Déléguer des invitations pour Azure Active Directory B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="17244-103">Delegate invitations for Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="17244-104">À la collaboration d’entreprise-entreprise (B2B) Azure Active Directory (Azure AD), il est inutile toobe un toosend les invitations administrateur global.</span><span class="sxs-lookup"><span data-stu-id="17244-104">With Azure Active Directory (Azure AD) business-to-business (B2B) collaboration, you do not have toobe a global admin toosend invitations.</span></span> <span data-ttu-id="17244-105">Au lieu de cela, vous pouvez utiliser des stratégies et déléguer toousers invitations dont les rôles et les autorisent les invitations toosend.</span><span class="sxs-lookup"><span data-stu-id="17244-105">Instead, you can use policies and delegate invitations toousers whose roles allow them toosend invitations.</span></span> <span data-ttu-id="17244-106">Un important nouvelle façon toodelegate invité utilisateur invitations est via le rôle d’invité Inviter hello.</span><span class="sxs-lookup"><span data-stu-id="17244-106">An important new way toodelegate guest user invitations is through hello Guest Inviter role.</span></span>

## <a name="guest-inviter-role"></a><span data-ttu-id="17244-107">Rôle Inviteur d’invités</span><span class="sxs-lookup"><span data-stu-id="17244-107">Guest Inviter role</span></span>
<span data-ttu-id="17244-108">Nous pouvons attribuer hello utilisateur tooGuest invitations de toosend Inviter rôle.</span><span class="sxs-lookup"><span data-stu-id="17244-108">We can assign hello user tooGuest Inviter role toosend invitations.</span></span> <span data-ttu-id="17244-109">Vous n’êtes pas membre de toobe des invitations à participer à toosend de rôle d’administrateur global hello.</span><span class="sxs-lookup"><span data-stu-id="17244-109">You don't have toobe member of hello global admin role toosend invitations.</span></span> <span data-ttu-id="17244-110">Par défaut, les utilisateurs standard peuvent également appeler hello invitation API, sauf si un administrateur global désactivé invitations pour les utilisateurs normaux.</span><span class="sxs-lookup"><span data-stu-id="17244-110">By default, regular users can also invoke hello invite API unless a global admin disabled invitations for regular users.</span></span> <span data-ttu-id="17244-111">Un utilisateur peut également appeler des API hello à l’aide de hello portail Azure ou PowerShell.</span><span class="sxs-lookup"><span data-stu-id="17244-111">A user can also invoke hello API using hello Azure portal or PowerShell.</span></span>

<span data-ttu-id="17244-112">Voici un exemple qui montre comment toouse PowerShell tooadd un rôle d’invité Inviter toohello utilisateur :</span><span class="sxs-lookup"><span data-stu-id="17244-112">Here's an example that shows how toouse PowerShell tooadd a user toohello Guest Inviter role:</span></span>

```
Add-MsolRoleMember -RoleObjectId 95e79109-95c0-4d8e-aee3-d01accf2d47b -RoleMemberEmailAddress <RoleMemberEmailAddress>
```

## <a name="control-who-can-invite"></a><span data-ttu-id="17244-113">Contrôler qui peut inviter</span><span class="sxs-lookup"><span data-stu-id="17244-113">Control who can invite</span></span>

![Contrôle comment tooinvite](media/active-directory-b2b-delegate-invitations/control-who-to-invite.png)

<span data-ttu-id="17244-115">Avec Azure AD B2B collaboration, un administrateur client peut définir hello suivant des stratégies de l’invitation :</span><span class="sxs-lookup"><span data-stu-id="17244-115">With Azure AD B2B collaboration, a tenant admin can set hello following invitation policies:</span></span>

- <span data-ttu-id="17244-116">Désactiver les invitations</span><span class="sxs-lookup"><span data-stu-id="17244-116">Turn off invitations</span></span>
- <span data-ttu-id="17244-117">Seuls les administrateurs et les utilisateurs dans le rôle d’invité Inviter hello peuvent inviter</span><span class="sxs-lookup"><span data-stu-id="17244-117">Only admins and users in hello Guest Inviter role can invite</span></span>
- <span data-ttu-id="17244-118">Administrateurs, le rôle d’invité Inviter hello et membres peuvent inviter</span><span class="sxs-lookup"><span data-stu-id="17244-118">Admins, hello Guest Inviter role, and members can invite</span></span>
- <span data-ttu-id="17244-119">Tous les utilisateurs, notamment les invités, peuvent inviter</span><span class="sxs-lookup"><span data-stu-id="17244-119">All users, including guests, can invite</span></span>

<span data-ttu-id="17244-120">Par défaut, les clients sont définis trop n° 4.</span><span class="sxs-lookup"><span data-stu-id="17244-120">By default, tenants are set too#4.</span></span> <span data-ttu-id="17244-121">Tous les utilisateurs, notamment les invités, peuvent inviter des utilisateurs B2B.</span><span class="sxs-lookup"><span data-stu-id="17244-121">(All users, including guests, can invite B2B users.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="17244-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="17244-122">Next steps</span></span>

<span data-ttu-id="17244-123">Consultez les autres articles sur la collaboration B2B d'Azure AD :</span><span class="sxs-lookup"><span data-stu-id="17244-123">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="17244-124">Qu’est-ce qu’Azure AD B2B Collaboration ?</span><span class="sxs-lookup"><span data-stu-id="17244-124">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="17244-125">Propriétés de l’utilisateur B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="17244-125">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="17244-126">Ajout d’un rôle tooa B2B collaboration</span><span class="sxs-lookup"><span data-stu-id="17244-126">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="17244-127">Groupes dynamiques et B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="17244-127">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="17244-128">Code B2B Collaboration et exemples PowerShell</span><span class="sxs-lookup"><span data-stu-id="17244-128">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="17244-129">Configurer des applications SaaS pour B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="17244-129">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="17244-130">Jetons utilisateur B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="17244-130">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="17244-131">Mappage des revendications utilisateur B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="17244-131">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="17244-132">Partage externe d’Office 365</span><span class="sxs-lookup"><span data-stu-id="17244-132">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="17244-133">Limitations actuelles de B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="17244-133">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
