---
title: "Audit et création de rapports relatifs à un utilisateur Azure Active Directory B2B Collaboration | Microsoft Docs"
description: "Les propriétés de l’utilisateur invité sont configurables dans Azure Active Directory B2B Collaboration"
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
ms.date: 04/12/2017
ms.author: sasubram
ms.openlocfilehash: ba782270f3280e52235bc13148d232284b55762a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="auditing-and-reporting-a-b2b-collaboration-user"></a><span data-ttu-id="18f2c-103">Audit et création de rapports relatifs à un utilisateur B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="18f2c-103">Auditing and reporting a B2B collaboration user</span></span>
<span data-ttu-id="18f2c-104">Avec les utilisateurs invités, vous disposez de fonctionnalités d’audit identiques à celles des utilisateurs membres.</span><span class="sxs-lookup"><span data-stu-id="18f2c-104">With guest users, you have auditing capabilities similar to with member users.</span></span> <span data-ttu-id="18f2c-105">Voici un exemple de l’historique d’invitation et d’échange pour l’invité Sam Oogle :</span><span class="sxs-lookup"><span data-stu-id="18f2c-105">Here's an example of the invitation and redemption history of invitee Sam Oogle:</span></span>

![journal d’audit](./media/active-directory-b2b-auditing-and-reporting/audit-log.png)

<span data-ttu-id="18f2c-107">Vous pouvez explorer chacun de ces événements pour en obtenir les détails.</span><span class="sxs-lookup"><span data-stu-id="18f2c-107">You can dive into each of these events to get the details.</span></span> <span data-ttu-id="18f2c-108">Examinons, par exemple, les détails de l’acceptation.</span><span class="sxs-lookup"><span data-stu-id="18f2c-108">For example, let's look at the acceptance details.</span></span>

![détails de l’activité](./media/active-directory-b2b-auditing-and-reporting/activity-details.png)

<span data-ttu-id="18f2c-110">Vous pouvez également exporter ces journaux à partir d’Azure AD et utiliser l’outil de création de rapports de votre choix afin d’obtenir des rapports personnalisés.</span><span class="sxs-lookup"><span data-stu-id="18f2c-110">You can also export these logs from Azure AD and use the reporting tool of your choice to get customized reports.</span></span>

### <a name="next-steps"></a><span data-ttu-id="18f2c-111">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="18f2c-111">Next steps</span></span>

<span data-ttu-id="18f2c-112">Consultez les autres articles sur la collaboration B2B d'Azure AD :</span><span class="sxs-lookup"><span data-stu-id="18f2c-112">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="18f2c-113">Qu’est-ce qu’Azure AD B2B Collaboration ?</span><span class="sxs-lookup"><span data-stu-id="18f2c-113">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="18f2c-114">Propriétés de l’utilisateur B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="18f2c-114">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="18f2c-115">Ajout d’un utilisateur B2B Collaboration à un rôle</span><span class="sxs-lookup"><span data-stu-id="18f2c-115">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="18f2c-116">Déléguer des invitations B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="18f2c-116">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="18f2c-117">Groupes dynamiques et B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="18f2c-117">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="18f2c-118">Code B2B Collaboration et exemples PowerShell</span><span class="sxs-lookup"><span data-stu-id="18f2c-118">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="18f2c-119">Configurer des applications SaaS pour B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="18f2c-119">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="18f2c-120">Jetons utilisateur B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="18f2c-120">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="18f2c-121">Mappage des revendications utilisateur B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="18f2c-121">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="18f2c-122">Partage externe d’Office 365</span><span class="sxs-lookup"><span data-stu-id="18f2c-122">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="18f2c-123">Limitations actuelles de B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="18f2c-123">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
