---
title: aaaDynamic groupes et Azure Active Directory B2B collaboration | Documents Microsoft
description: "Azure Active Directory B2B Collaboration peut être utilisé avec des groupes dynamiques Azure AD"
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
ms.date: 06/27/2017
ms.author: curtand
ms.reviewer: sasubram
ms.openlocfilehash: b011298de5fd2c851c6d9caaf5c2b257807ef0a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-groups-and-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="8424c-103">Groupes dynamiques et Azure Active Directory B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="8424c-103">Dynamic groups and Azure Active Directory B2B collaboration</span></span>

## <a name="what-are-dynamic-groups"></a><span data-ttu-id="8424c-104">Qu'est-ce-que les groupes dynamiques ?</span><span class="sxs-lookup"><span data-stu-id="8424c-104">What are dynamic groups?</span></span>
<span data-ttu-id="8424c-105">Configuration dynamique de l’appartenance au groupe de sécurité pour Azure Active Directory (Azure AD) est disponible dans [hello Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8424c-105">Dynamic configuration of security group membership for Azure Active Directory (Azure AD) is available in [hello Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="8424c-106">Les administrateurs peuvent définir des règles toopopulate groupes qui sont créés dans Azure Active Directory basées sur les attributs de l’utilisateur (par exemple, userType, département ou pays).</span><span class="sxs-lookup"><span data-stu-id="8424c-106">Administrators can set rules toopopulate groups that are created in Azure Active Directory based on user attributes (such as userType, department, or country).</span></span> <span data-ttu-id="8424c-107">Les membres peuvent être ajoutées automatiquement tooor supprimé d’un groupe de sécurité en fonction de leurs attributs.</span><span class="sxs-lookup"><span data-stu-id="8424c-107">Members can be automatically added tooor removed from a security group based on their attributes.</span></span> <span data-ttu-id="8424c-108">Ces groupes peuvent fournir des accès des ressources cloud ou tooapplications (les sites SharePoint, des documents) et tooassign toomembers de licences.</span><span class="sxs-lookup"><span data-stu-id="8424c-108">These groups can provide access tooapplications or cloud resources (SharePoint sites, documents) and tooassign licenses toomembers.</span></span> <span data-ttu-id="8424c-109">En savoir plus sur les groupes dynamiques dans [Groupes dédiés dans Azure Active Directory](active-directory-accessmanagement-dedicated-groups.md).</span><span class="sxs-lookup"><span data-stu-id="8424c-109">Read more about dynamic groups in [Dedicated groups in Azure Active Directory](active-directory-accessmanagement-dedicated-groups.md).</span></span>

<span data-ttu-id="8424c-110">Hello approprié [licence Azure AD Premium P1 ou P2](https://azure.microsoft.com/pricing/details/active-directory/) est requis toocreate et l’utilisation des groupes dynamiques.</span><span class="sxs-lookup"><span data-stu-id="8424c-110">hello appropriate [Azure AD Premium P1 or P2 licensing](https://azure.microsoft.com/pricing/details/active-directory/) is required toocreate and use dynamic groups.</span></span> <span data-ttu-id="8424c-111">En savoir plus, consultez l’article de hello [créer des règles d’attribut pour l’appartenance aux groupes dynamiques dans Azure Active Directory](active-directory-groups-dynamic-membership-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8424c-111">Learn more in hello article [Create attribute-based rules for dynamic group membership in Azure Active Directory](active-directory-groups-dynamic-membership-azure-portal.md).</span></span>

## <a name="what-are-hello-built-in-dynamic-groups"></a><span data-ttu-id="8424c-112">Quelles sont les groupes dynamiques intégrés hello ?</span><span class="sxs-lookup"><span data-stu-id="8424c-112">What are hello built-in dynamic groups?</span></span>
<span data-ttu-id="8424c-113">Hello **tous les utilisateurs** permet à toocreate d’administrateurs client cliquez sur le groupe contenant tous les utilisateurs de client hello avec un seul groupe dynamique.</span><span class="sxs-lookup"><span data-stu-id="8424c-113">hello **All users** dynamic group enables tenant admins toocreate a group containing all users in hello tenant with a single click.</span></span> <span data-ttu-id="8424c-114">Par défaut, hello **tous les utilisateurs** groupe comprend tous les utilisateurs de répertoire hello, y compris les membres et invités.</span><span class="sxs-lookup"><span data-stu-id="8424c-114">By default, hello **All users** group includes all users in hello directory, including Members and Guests.</span></span>
<span data-ttu-id="8424c-115">Dans le portail d’administration hello nouveau Azure Active Directory, vous pouvez choisir tooenable hello **tous les utilisateurs** groupe hello afficher les paramètres de groupe.</span><span class="sxs-lookup"><span data-stu-id="8424c-115">Within hello new Azure Active Directory admin portal, you can choose tooenable hello **All users** group in hello Group Settings view.</span></span>

![groupes intégrés](media/active-directory-b2b-dynamic-groups/built-in-groups.png)

## <a name="hardening-hello-all-users-dynamic-group"></a><span data-ttu-id="8424c-117">Sécurisation renforcée hello groupe dynamique de tous les utilisateurs</span><span class="sxs-lookup"><span data-stu-id="8424c-117">Hardening hello All users dynamic group</span></span>
<span data-ttu-id="8424c-118">Par défaut, hello **tous les utilisateurs** groupe contient également les utilisateurs de collaboration (invité) B2B.</span><span class="sxs-lookup"><span data-stu-id="8424c-118">By default, hello **All users** group contains your B2B collaboration (guest) users as well.</span></span> <span data-ttu-id="8424c-119">Vous pouvez sécuriser davantage votre **tous les utilisateurs** groupe à l’aide d’une règle d’utilisateurs invités tooremove.</span><span class="sxs-lookup"><span data-stu-id="8424c-119">You can further secure your **All users** group by using a rule tooremove guest users.</span></span> <span data-ttu-id="8424c-120">Hello l’illustration suivante hello **tous les utilisateurs** groupe modifié tooexclude invités.</span><span class="sxs-lookup"><span data-stu-id="8424c-120">hello following illustration shows hello **All users** group modified tooexclude guests.</span></span>

![activer le groupe Tous les utilisateurs](media/active-directory-b2b-dynamic-groups/enable-all-users-group.png)

<span data-ttu-id="8424c-122">Il peut également s’avérer utile toocreate un nouveau groupe dynamique qui contient uniquement les utilisateurs invités, afin que vous pouvez appliquer des stratégies (telles que les stratégies d’accès conditionnel de Azure AD) toothem.</span><span class="sxs-lookup"><span data-stu-id="8424c-122">You might also find it useful toocreate a new dynamic group that contains only guest users, so that you can apply policies (such as Azure AD Conditional Access policies) toothem.</span></span>
<span data-ttu-id="8424c-123">Ce groupe pourrait ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="8424c-123">What such a group might look like:</span></span>

![exclure les utilisateurs invités](media/active-directory-b2b-dynamic-groups/exclude-guest-users.png)

## <a name="next-steps"></a><span data-ttu-id="8424c-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8424c-125">Next steps</span></span>

<span data-ttu-id="8424c-126">Consultez les autres articles sur la collaboration B2B d'Azure AD :</span><span class="sxs-lookup"><span data-stu-id="8424c-126">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="8424c-127">Qu’est-ce qu’Azure AD B2B Collaboration ?</span><span class="sxs-lookup"><span data-stu-id="8424c-127">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="8424c-128">Propriétés de l’utilisateur B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="8424c-128">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="8424c-129">Ajout d’un rôle tooa B2B collaboration</span><span class="sxs-lookup"><span data-stu-id="8424c-129">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="8424c-130">Déléguer des invitations B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="8424c-130">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="8424c-131">Code B2B Collaboration et exemples PowerShell</span><span class="sxs-lookup"><span data-stu-id="8424c-131">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="8424c-132">Configurer des applications SaaS pour B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="8424c-132">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="8424c-133">Jetons utilisateur B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="8424c-133">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="8424c-134">Mappage des revendications utilisateur B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="8424c-134">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="8424c-135">Partage externe d’Office 365</span><span class="sxs-lookup"><span data-stu-id="8424c-135">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="8424c-136">Limitations actuelles de B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="8424c-136">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
