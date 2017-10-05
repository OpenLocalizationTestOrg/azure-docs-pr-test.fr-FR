---
title: Autorisations dans Azure Security Center | Microsoft Docs
description: "Cet article explique comment Azure Security Center utilise le contrôle d’accès en fonction du rôle pour affecter des autorisations aux utilisateurs et identifie les actions autorisées pour chaque rôle."
services: security-center
cloud: na
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
ms.assetid: 
ms.service: security-center
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: terrylan
ms.openlocfilehash: 0aaa99dda44d2020afd3e841e84020eb4ff87a85
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="permissions-in-azure-security-center"></a><span data-ttu-id="69ee0-103">Autorisations dans Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="69ee0-103">Permissions in Azure Security Center</span></span>

<span data-ttu-id="69ee0-104">Azure Security Center utilise le [contrôle d’accès en fonction du rôle (RBAC)](../active-directory/role-based-access-control-configure.md) qui fournit des [rôles intégrés](../active-directory/role-based-access-built-in-roles.md) susceptibles d’être affectés à des utilisateurs, des groupes et des services dans Azure.</span><span class="sxs-lookup"><span data-stu-id="69ee0-104">Azure Security Center uses [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md), which provides [built-in roles](../active-directory/role-based-access-built-in-roles.md) that can be assigned to users, groups, and services in Azure.</span></span>

<span data-ttu-id="69ee0-105">Security Center évalue la configuration de vos ressources pour identifier les vulnérabilités et les problèmes de sécurité.</span><span class="sxs-lookup"><span data-stu-id="69ee0-105">Security Center assesses the configuration of your resources to identify security issues and vulnerabilities.</span></span> <span data-ttu-id="69ee0-106">Dans Security Center, vous ne voyez les informations relatives à une ressource que lorsque vous avez reçu le rôle de propriétaire, de collaborateur ou de lecteur pour l’abonnement ou le groupe de ressources auquel appartient la ressource.</span><span class="sxs-lookup"><span data-stu-id="69ee0-106">In Security Center, you only see information related to a resource when you are assigned the role of Owner, Contributor, or Reader for the subscription or resource group that a resource belongs to.</span></span>

<span data-ttu-id="69ee0-107">Outre ces rôles, il existe deux rôles propres à Security Center :</span><span class="sxs-lookup"><span data-stu-id="69ee0-107">In addition to these roles, there are two specific Security Center roles:</span></span>

* <span data-ttu-id="69ee0-108">**Lecteur Sécurité** : l’utilisateur ayant ce rôle dispose de droits d’affichage dans Security Center.</span><span class="sxs-lookup"><span data-stu-id="69ee0-108">**Security Reader**: A user that belongs to this role has viewing rights to Security Center.</span></span> <span data-ttu-id="69ee0-109">Il peut afficher les recommandations, les alertes, la stratégie de sécurité actuelle et les états de sécurité, mais ne peut pas apporter de modifications.</span><span class="sxs-lookup"><span data-stu-id="69ee0-109">The user can view recommendations, alerts, a security policy, and security states, but cannot make changes.</span></span>
* <span data-ttu-id="69ee0-110">**Administrateur de la sécurité** : l’utilisateur ayant ce rôle dispose des mêmes droits que le lecteur Sécurité. Il peut en outre modifier la stratégie de sécurité actuelle, ainsi qu’ignorer les alertes et les recommandations.</span><span class="sxs-lookup"><span data-stu-id="69ee0-110">**Security Administrator**: A user that belongs to this role has the same rights as the Security Reader and can also update the security policy and dismiss alerts and recommendations.</span></span>

> [!NOTE]
> <span data-ttu-id="69ee0-111">Les rôles de sécurité que sont le lecteur Sécurité et l’administrateur de la sécurité ont uniquement accès à Security Center.</span><span class="sxs-lookup"><span data-stu-id="69ee0-111">The security roles, Security Reader and Security Administrator, have access only in Security Center.</span></span> <span data-ttu-id="69ee0-112">Les rôles de sécurité n’ont pas accès aux autres services d’Azure (par exemple, Stockage, Web et mobile ou Internet des objets).</span><span class="sxs-lookup"><span data-stu-id="69ee0-112">The security roles do not have access to other service areas of Azure such as Storage, Web & Mobile, or Internet of Things.</span></span>
>
>

## <a name="roles-and-allowed-actions"></a><span data-ttu-id="69ee0-113">Rôles et actions autorisées</span><span class="sxs-lookup"><span data-stu-id="69ee0-113">Roles and allowed actions</span></span>

<span data-ttu-id="69ee0-114">Le tableau suivant affiche les rôles et les actions autorisées dans Security Center.</span><span class="sxs-lookup"><span data-stu-id="69ee0-114">The following table displays roles and allowed actions in Security Center.</span></span> <span data-ttu-id="69ee0-115">Un X indique que l’action est autorisée pour ce rôle.</span><span class="sxs-lookup"><span data-stu-id="69ee0-115">An X indicates that the action is allowed for that role.</span></span>

| <span data-ttu-id="69ee0-116">Rôle</span><span class="sxs-lookup"><span data-stu-id="69ee0-116">Role</span></span> | <span data-ttu-id="69ee0-117">Modifier une stratégie de sécurité</span><span class="sxs-lookup"><span data-stu-id="69ee0-117">Edit security policy</span></span> | <span data-ttu-id="69ee0-118">Appliquer des recommandations de sécurité à une ressource</span><span class="sxs-lookup"><span data-stu-id="69ee0-118">Apply security recommendations for a resource</span></span> | <span data-ttu-id="69ee0-119">Ignorer les alertes et les recommandations</span><span class="sxs-lookup"><span data-stu-id="69ee0-119">Dismiss alerts and recommendations</span></span> | <span data-ttu-id="69ee0-120">Afficher les alertes et les recommandations</span><span class="sxs-lookup"><span data-stu-id="69ee0-120">View alerts and recommendations</span></span> |
|:--- |:---:|:---:|:---:|:---:|
| <span data-ttu-id="69ee0-121">Propriétaire de l’abonnement</span><span class="sxs-lookup"><span data-stu-id="69ee0-121">Subscription Owner</span></span> | <span data-ttu-id="69ee0-122">X</span><span class="sxs-lookup"><span data-stu-id="69ee0-122">X</span></span> | <span data-ttu-id="69ee0-123">X</span><span class="sxs-lookup"><span data-stu-id="69ee0-123">X</span></span> | <span data-ttu-id="69ee0-124">X</span><span class="sxs-lookup"><span data-stu-id="69ee0-124">X</span></span> | <span data-ttu-id="69ee0-125">X</span><span class="sxs-lookup"><span data-stu-id="69ee0-125">X</span></span> |
| <span data-ttu-id="69ee0-126">Collaborateur de l’abonnement</span><span class="sxs-lookup"><span data-stu-id="69ee0-126">Subscription Contributor</span></span> | <span data-ttu-id="69ee0-127">X</span><span class="sxs-lookup"><span data-stu-id="69ee0-127">X</span></span> | <span data-ttu-id="69ee0-128">X</span><span class="sxs-lookup"><span data-stu-id="69ee0-128">X</span></span> | <span data-ttu-id="69ee0-129">X</span><span class="sxs-lookup"><span data-stu-id="69ee0-129">X</span></span> | <span data-ttu-id="69ee0-130">X</span><span class="sxs-lookup"><span data-stu-id="69ee0-130">X</span></span> |
| <span data-ttu-id="69ee0-131">Propriétaire du groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="69ee0-131">Resource Group Owner</span></span> | -- | <span data-ttu-id="69ee0-132">X</span><span class="sxs-lookup"><span data-stu-id="69ee0-132">X</span></span> | -- | <span data-ttu-id="69ee0-133">X</span><span class="sxs-lookup"><span data-stu-id="69ee0-133">X</span></span> |
| <span data-ttu-id="69ee0-134">Collaborateur du groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="69ee0-134">Resource Group Contributor</span></span> | -- | <span data-ttu-id="69ee0-135">X</span><span class="sxs-lookup"><span data-stu-id="69ee0-135">X</span></span> | -- | <span data-ttu-id="69ee0-136">X</span><span class="sxs-lookup"><span data-stu-id="69ee0-136">X</span></span> |
| <span data-ttu-id="69ee0-137">Lecteur</span><span class="sxs-lookup"><span data-stu-id="69ee0-137">Reader</span></span> | -- | -- | -- | <span data-ttu-id="69ee0-138">X</span><span class="sxs-lookup"><span data-stu-id="69ee0-138">X</span></span> |
| <span data-ttu-id="69ee0-139">Security Administrator</span><span class="sxs-lookup"><span data-stu-id="69ee0-139">Security Administrator</span></span> | <span data-ttu-id="69ee0-140">X</span><span class="sxs-lookup"><span data-stu-id="69ee0-140">X</span></span> | -- | <span data-ttu-id="69ee0-141">X</span><span class="sxs-lookup"><span data-stu-id="69ee0-141">X</span></span> | <span data-ttu-id="69ee0-142">X</span><span class="sxs-lookup"><span data-stu-id="69ee0-142">X</span></span> |
| <span data-ttu-id="69ee0-143">Lecteur de sécurité</span><span class="sxs-lookup"><span data-stu-id="69ee0-143">Security Reader</span></span> | -- | -- | -- | <span data-ttu-id="69ee0-144">X</span><span class="sxs-lookup"><span data-stu-id="69ee0-144">X</span></span> |

> [!NOTE]
> <span data-ttu-id="69ee0-145">Nous vous recommandons d’attribuer le rôle le moins permissif permettant aux utilisateurs d’effectuer leurs tâches.</span><span class="sxs-lookup"><span data-stu-id="69ee0-145">We recommend that you assign the least permissive role needed for users to complete their tasks.</span></span> <span data-ttu-id="69ee0-146">Par exemple, affectez le rôle Lecteur aux utilisateurs qui n’ont besoin que de consulter des informations sur l’intégrité de la sécurité d’une ressource sans effectuer aucune action, telles que l’application des recommandations ou la modification des stratégies.</span><span class="sxs-lookup"><span data-stu-id="69ee0-146">For example, assign the Reader role to users who only need to view information about the security health of a resource but not take action, such as applying recommendations or editing policies.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="69ee0-147">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="69ee0-147">Next steps</span></span>
<span data-ttu-id="69ee0-148">Cet article vous a expliqué comment Security Center utilise le contrôle d’accès en fonction du rôle pour affecter des autorisations aux utilisateurs et a identifié les actions autorisées pour chaque rôle.</span><span class="sxs-lookup"><span data-stu-id="69ee0-148">This article explained how Security Center uses RBAC to assign permissions to users and identified the allowed actions for each role.</span></span> <span data-ttu-id="69ee0-149">Maintenant que vous êtes familiarisé avec les affectations de rôles nécessaires pour surveiller l’état de sécurité de votre abonnement, modifier les stratégies de sécurité et appliquer les recommandations, découvrez comment :</span><span class="sxs-lookup"><span data-stu-id="69ee0-149">Now that you're familiar with the role assignments needed to monitor the security state of your subscription, edit security policies, and apply recommendations, learn how to:</span></span>

- [<span data-ttu-id="69ee0-150">Définir des stratégies de sécurité dans Security Center</span><span class="sxs-lookup"><span data-stu-id="69ee0-150">Set security policies in Security Center</span></span>](security-center-policies.md)
- [<span data-ttu-id="69ee0-151">Gérer les recommandations de sécurité dans Security Center</span><span class="sxs-lookup"><span data-stu-id="69ee0-151">Manage security recommendations in Security Center</span></span>](security-center-recommendations.md)
- [<span data-ttu-id="69ee0-152">Surveiller l’intégrité de la sécurité de vos ressources Azure</span><span class="sxs-lookup"><span data-stu-id="69ee0-152">Monitor the security health of your Azure resources</span></span>](security-center-monitoring.md)
- [<span data-ttu-id="69ee0-153">Gérer et répondre aux alertes de sécurité dans Security Center</span><span class="sxs-lookup"><span data-stu-id="69ee0-153">Manage and respond to security alerts in Security Center</span></span>](security-center-managing-and-responding-alerts.md)
- [<span data-ttu-id="69ee0-154">Surveiller les solutions de sécurité des partenaires</span><span class="sxs-lookup"><span data-stu-id="69ee0-154">Monitor partner security solutions</span></span>](security-center-partner-solutions.md)
