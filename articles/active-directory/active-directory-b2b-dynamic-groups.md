---
title: Groupes dynamiques et Azure Active Directory B2B Collaboration | Microsoft Docs
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
ms.openlocfilehash: 5818c41610c8c5df89abcb0dcd058bcbe9579ce7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="dynamic-groups-and-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="d5350-103">Groupes dynamiques et Azure Active Directory B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="d5350-103">Dynamic groups and Azure Active Directory B2B collaboration</span></span>

## <a name="what-are-dynamic-groups"></a><span data-ttu-id="d5350-104">Qu'est-ce-que les groupes dynamiques ?</span><span class="sxs-lookup"><span data-stu-id="d5350-104">What are dynamic groups?</span></span>
<span data-ttu-id="d5350-105">La configuration dynamique de l’appartenance au groupe de sécurité pour Azure Active Directory (Azure AD) est disponible dans le [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d5350-105">Dynamic configuration of security group membership for Azure Active Directory (Azure AD) is available in [the Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="d5350-106">Les administrateurs peuvent définir des règles pour remplir les groupes créés dans Azure Active Directory en fonction d'attributs utilisateur (par exemple, userType, département ou pays).</span><span class="sxs-lookup"><span data-stu-id="d5350-106">Administrators can set rules to populate groups that are created in Azure Active Directory based on user attributes (such as userType, department, or country).</span></span> <span data-ttu-id="d5350-107">Les membres peuvent être automatiquement ajoutés ou supprimés d’un groupe de sécurité en fonction de leurs attributs.</span><span class="sxs-lookup"><span data-stu-id="d5350-107">Members can be automatically added to or removed from a security group based on their attributes.</span></span> <span data-ttu-id="d5350-108">Ces groupes permettent d’accorder l’accès à des applications ou à des ressources cloud (sites SharePoint, documents) et d’attribuer des licences à des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="d5350-108">These groups can provide access to applications or cloud resources (SharePoint sites, documents) and to assign licenses to members.</span></span> <span data-ttu-id="d5350-109">En savoir plus sur les groupes dynamiques dans [Groupes dédiés dans Azure Active Directory](active-directory-accessmanagement-dedicated-groups.md).</span><span class="sxs-lookup"><span data-stu-id="d5350-109">Read more about dynamic groups in [Dedicated groups in Azure Active Directory](active-directory-accessmanagement-dedicated-groups.md).</span></span>

<span data-ttu-id="d5350-110">La [licence Azure AD Premium P1 ou P2](https://azure.microsoft.com/pricing/details/active-directory/) appropriée est nécessaire pour créer et utiliser des groupes dynamiques.</span><span class="sxs-lookup"><span data-stu-id="d5350-110">The appropriate [Azure AD Premium P1 or P2 licensing](https://azure.microsoft.com/pricing/details/active-directory/) is required to create and use dynamic groups.</span></span> <span data-ttu-id="d5350-111">Pour en savoir plus, consultez l’article [Créer des règles basées sur les attributs pour l’appartenance à un groupe dynamique dans Azure Active Directory](active-directory-groups-dynamic-membership-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d5350-111">Learn more in the article [Create attribute-based rules for dynamic group membership in Azure Active Directory](active-directory-groups-dynamic-membership-azure-portal.md).</span></span>

## <a name="what-are-the-built-in-dynamic-groups"></a><span data-ttu-id="d5350-112">Que sont les groupes dynamiques intégrés ?</span><span class="sxs-lookup"><span data-stu-id="d5350-112">What are the built-in dynamic groups?</span></span>
<span data-ttu-id="d5350-113">Le groupe dynamique **Tous les utilisateurs** permet à des administrateurs de locataires de créer un groupe contenant tous les utilisateurs dans le locataire en un seul clic.</span><span class="sxs-lookup"><span data-stu-id="d5350-113">The **All users** dynamic group enables tenant admins to create a group containing all users in the tenant with a single click.</span></span> <span data-ttu-id="d5350-114">Par défaut, le groupe **Tous les utilisateurs** inclut tous les utilisateurs du répertoire, dont les invités et les utilisateurs externes.</span><span class="sxs-lookup"><span data-stu-id="d5350-114">By default, the **All users** group includes all users in the directory, including Members and Guests.</span></span>
<span data-ttu-id="d5350-115">Dans le nouveau portail d’administration Azure Active Directory, vous pouvez choisir d’activer le groupe **Tous les utilisateurs** dans l’affichage des paramètres de groupe.</span><span class="sxs-lookup"><span data-stu-id="d5350-115">Within the new Azure Active Directory admin portal, you can choose to enable the **All users** group in the Group Settings view.</span></span>

![groupes intégrés](media/active-directory-b2b-dynamic-groups/built-in-groups.png)

## <a name="hardening-the-all-users-dynamic-group"></a><span data-ttu-id="d5350-117">Renforcement de la sécurité du groupe dynamique Tous les utilisateurs</span><span class="sxs-lookup"><span data-stu-id="d5350-117">Hardening the All users dynamic group</span></span>
<span data-ttu-id="d5350-118">Par défaut, le groupe **Tous les utilisateurs** contient également vos utilisateurs B2B Collaboration (invités).</span><span class="sxs-lookup"><span data-stu-id="d5350-118">By default, the **All users** group contains your B2B collaboration (guest) users as well.</span></span> <span data-ttu-id="d5350-119">Vous pouvez sécuriser davantage votre groupe **Tous les utilisateurs** en utilisant une règle pour supprimer les utilisateurs invités.</span><span class="sxs-lookup"><span data-stu-id="d5350-119">You can further secure your **All users** group by using a rule to remove guest users.</span></span> <span data-ttu-id="d5350-120">L’illustration suivante montre le groupe **Tous les utilisateurs** modifié de manière à exclure les invités.</span><span class="sxs-lookup"><span data-stu-id="d5350-120">The following illustration shows the **All users** group modified to exclude guests.</span></span>

![activer le groupe Tous les utilisateurs](media/active-directory-b2b-dynamic-groups/enable-all-users-group.png)

<span data-ttu-id="d5350-122">Vous trouverez peut-être aussi utile de créer un groupe dynamique contenant uniquement les utilisateurs invités, afin de pouvoir leur appliquer des stratégies (telles que des stratégies d’accès conditionnel Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d5350-122">You might also find it useful to create a new dynamic group that contains only guest users, so that you can apply policies (such as Azure AD Conditional Access policies) to them.</span></span>
<span data-ttu-id="d5350-123">Ce groupe pourrait ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="d5350-123">What such a group might look like:</span></span>

![exclure les utilisateurs invités](media/active-directory-b2b-dynamic-groups/exclude-guest-users.png)

## <a name="next-steps"></a><span data-ttu-id="d5350-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d5350-125">Next steps</span></span>

<span data-ttu-id="d5350-126">Consultez les autres articles sur la collaboration B2B d'Azure AD :</span><span class="sxs-lookup"><span data-stu-id="d5350-126">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="d5350-127">Qu’est-ce qu’Azure AD B2B Collaboration ?</span><span class="sxs-lookup"><span data-stu-id="d5350-127">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="d5350-128">Propriétés de l’utilisateur B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="d5350-128">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="d5350-129">Ajout d’un utilisateur B2B Collaboration à un rôle</span><span class="sxs-lookup"><span data-stu-id="d5350-129">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="d5350-130">Déléguer des invitations B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="d5350-130">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="d5350-131">Code B2B Collaboration et exemples PowerShell</span><span class="sxs-lookup"><span data-stu-id="d5350-131">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="d5350-132">Configurer des applications SaaS pour B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="d5350-132">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="d5350-133">Jetons utilisateur B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="d5350-133">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="d5350-134">Mappage des revendications utilisateur B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="d5350-134">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="d5350-135">Partage externe d’Office 365</span><span class="sxs-lookup"><span data-stu-id="d5350-135">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="d5350-136">Limitations actuelles de B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="d5350-136">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
