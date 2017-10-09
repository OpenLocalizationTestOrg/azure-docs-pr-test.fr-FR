---
title: "aaaPermissions dans le centre de sécurité Azure | Documents Microsoft"
description: "Cet article explique comment le centre de sécurité Azure utilise en fonction du rôle l’accès contrôle tooassign autorisations toousers et identifie les hello autorisé des actions pour chaque rôle."
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
ms.openlocfilehash: 03e16132dc3d951ef8ad9e86b9970b9e4d15c76b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="permissions-in-azure-security-center"></a><span data-ttu-id="f9659-103">Autorisations dans Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="f9659-103">Permissions in Azure Security Center</span></span>

<span data-ttu-id="f9659-104">Centre de sécurité Azure utilise [contrôle d’accès en fonction du rôle (RBAC)](../active-directory/role-based-access-control-configure.md), qui fournit des [rôles intégrés](../active-directory/role-based-access-built-in-roles.md) qui peuvent être attribuées toousers, des groupes et des services dans Azure.</span><span class="sxs-lookup"><span data-stu-id="f9659-104">Azure Security Center uses [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md), which provides [built-in roles](../active-directory/role-based-access-built-in-roles.md) that can be assigned toousers, groups, and services in Azure.</span></span>

<span data-ttu-id="f9659-105">Centre de sécurité évalue la configuration de hello de vos problèmes de sécurité tooidentify de ressources et les vulnérabilités.</span><span class="sxs-lookup"><span data-stu-id="f9659-105">Security Center assesses hello configuration of your resources tooidentify security issues and vulnerabilities.</span></span> <span data-ttu-id="f9659-106">Dans le centre de sécurité, vous voyez uniquement les informations liées tooa ressource lorsque vous sont assignés rôle hello de propriétaire, collaborateur ou lecteur pour le groupe d’abonnement ou une ressource hello appartenant à une ressource.</span><span class="sxs-lookup"><span data-stu-id="f9659-106">In Security Center, you only see information related tooa resource when you are assigned hello role of Owner, Contributor, or Reader for hello subscription or resource group that a resource belongs to.</span></span>

<span data-ttu-id="f9659-107">Dans les rôles toothese addition, il existe deux rôles de centre de sécurité spécifiques :</span><span class="sxs-lookup"><span data-stu-id="f9659-107">In addition toothese roles, there are two specific Security Center roles:</span></span>

* <span data-ttu-id="f9659-108">**Lecteur de sécurité**: un utilisateur membre du rôle de toothis a affichage droits tooSecurity Center.</span><span class="sxs-lookup"><span data-stu-id="f9659-108">**Security Reader**: A user that belongs toothis role has viewing rights tooSecurity Center.</span></span> <span data-ttu-id="f9659-109">utilisateur de Hello peut afficher les recommandations, alertes, une stratégie de sécurité et les États de sécurité, mais il ne peut pas apporter des modifications.</span><span class="sxs-lookup"><span data-stu-id="f9659-109">hello user can view recommendations, alerts, a security policy, and security states, but cannot make changes.</span></span>
* <span data-ttu-id="f9659-110">**Administrateur de sécurité**: un utilisateur membre du rôle de toothis hello même droits comme hello du lecteur de sécurité et peut également mettre à jour de la stratégie de sécurité hello et fermer les alertes et les recommandations.</span><span class="sxs-lookup"><span data-stu-id="f9659-110">**Security Administrator**: A user that belongs toothis role has hello same rights as hello Security Reader and can also update hello security policy and dismiss alerts and recommendations.</span></span>

> [!NOTE]
> <span data-ttu-id="f9659-111">rôles de sécurité Hello, lecteur de la sécurité et l’administrateur de la sécurité, ont accès uniquement dans le centre de sécurité.</span><span class="sxs-lookup"><span data-stu-id="f9659-111">hello security roles, Security Reader and Security Administrator, have access only in Security Center.</span></span> <span data-ttu-id="f9659-112">rôles de sécurité de Hello ne doivent pas accéder aux zones de service tooother Azure telles que le stockage, Web et mobiles ou Internet des objets.</span><span class="sxs-lookup"><span data-stu-id="f9659-112">hello security roles do not have access tooother service areas of Azure such as Storage, Web & Mobile, or Internet of Things.</span></span>
>
>

## <a name="roles-and-allowed-actions"></a><span data-ttu-id="f9659-113">Rôles et actions autorisées</span><span class="sxs-lookup"><span data-stu-id="f9659-113">Roles and allowed actions</span></span>

<span data-ttu-id="f9659-114">Hello tableau suivant affiche les rôles et les actions autorisées dans le centre de sécurité.</span><span class="sxs-lookup"><span data-stu-id="f9659-114">hello following table displays roles and allowed actions in Security Center.</span></span> <span data-ttu-id="f9659-115">Un X indique que l’action de hello est autorisée pour ce rôle.</span><span class="sxs-lookup"><span data-stu-id="f9659-115">An X indicates that hello action is allowed for that role.</span></span>

| <span data-ttu-id="f9659-116">Rôle</span><span class="sxs-lookup"><span data-stu-id="f9659-116">Role</span></span> | <span data-ttu-id="f9659-117">Modifier une stratégie de sécurité</span><span class="sxs-lookup"><span data-stu-id="f9659-117">Edit security policy</span></span> | <span data-ttu-id="f9659-118">Appliquer des recommandations de sécurité à une ressource</span><span class="sxs-lookup"><span data-stu-id="f9659-118">Apply security recommendations for a resource</span></span> | <span data-ttu-id="f9659-119">Ignorer les alertes et les recommandations</span><span class="sxs-lookup"><span data-stu-id="f9659-119">Dismiss alerts and recommendations</span></span> | <span data-ttu-id="f9659-120">Afficher les alertes et les recommandations</span><span class="sxs-lookup"><span data-stu-id="f9659-120">View alerts and recommendations</span></span> |
|:--- |:---:|:---:|:---:|:---:|
| <span data-ttu-id="f9659-121">Propriétaire de l’abonnement</span><span class="sxs-lookup"><span data-stu-id="f9659-121">Subscription Owner</span></span> | <span data-ttu-id="f9659-122">X</span><span class="sxs-lookup"><span data-stu-id="f9659-122">X</span></span> | <span data-ttu-id="f9659-123">X</span><span class="sxs-lookup"><span data-stu-id="f9659-123">X</span></span> | <span data-ttu-id="f9659-124">X</span><span class="sxs-lookup"><span data-stu-id="f9659-124">X</span></span> | <span data-ttu-id="f9659-125">X</span><span class="sxs-lookup"><span data-stu-id="f9659-125">X</span></span> |
| <span data-ttu-id="f9659-126">Collaborateur de l’abonnement</span><span class="sxs-lookup"><span data-stu-id="f9659-126">Subscription Contributor</span></span> | <span data-ttu-id="f9659-127">X</span><span class="sxs-lookup"><span data-stu-id="f9659-127">X</span></span> | <span data-ttu-id="f9659-128">X</span><span class="sxs-lookup"><span data-stu-id="f9659-128">X</span></span> | <span data-ttu-id="f9659-129">X</span><span class="sxs-lookup"><span data-stu-id="f9659-129">X</span></span> | <span data-ttu-id="f9659-130">X</span><span class="sxs-lookup"><span data-stu-id="f9659-130">X</span></span> |
| <span data-ttu-id="f9659-131">Propriétaire du groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="f9659-131">Resource Group Owner</span></span> | -- | <span data-ttu-id="f9659-132">X</span><span class="sxs-lookup"><span data-stu-id="f9659-132">X</span></span> | -- | <span data-ttu-id="f9659-133">X</span><span class="sxs-lookup"><span data-stu-id="f9659-133">X</span></span> |
| <span data-ttu-id="f9659-134">Collaborateur du groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="f9659-134">Resource Group Contributor</span></span> | -- | <span data-ttu-id="f9659-135">X</span><span class="sxs-lookup"><span data-stu-id="f9659-135">X</span></span> | -- | <span data-ttu-id="f9659-136">X</span><span class="sxs-lookup"><span data-stu-id="f9659-136">X</span></span> |
| <span data-ttu-id="f9659-137">Lecteur</span><span class="sxs-lookup"><span data-stu-id="f9659-137">Reader</span></span> | -- | -- | -- | <span data-ttu-id="f9659-138">X</span><span class="sxs-lookup"><span data-stu-id="f9659-138">X</span></span> |
| <span data-ttu-id="f9659-139">Security Administrator</span><span class="sxs-lookup"><span data-stu-id="f9659-139">Security Administrator</span></span> | <span data-ttu-id="f9659-140">X</span><span class="sxs-lookup"><span data-stu-id="f9659-140">X</span></span> | -- | <span data-ttu-id="f9659-141">X</span><span class="sxs-lookup"><span data-stu-id="f9659-141">X</span></span> | <span data-ttu-id="f9659-142">X</span><span class="sxs-lookup"><span data-stu-id="f9659-142">X</span></span> |
| <span data-ttu-id="f9659-143">Lecteur de sécurité</span><span class="sxs-lookup"><span data-stu-id="f9659-143">Security Reader</span></span> | -- | -- | -- | <span data-ttu-id="f9659-144">X</span><span class="sxs-lookup"><span data-stu-id="f9659-144">X</span></span> |

> [!NOTE]
> <span data-ttu-id="f9659-145">Nous recommandons d’attribuer hello rôle le moins permissif nécessaire pour les utilisateurs toocomplete leurs tâches.</span><span class="sxs-lookup"><span data-stu-id="f9659-145">We recommend that you assign hello least permissive role needed for users toocomplete their tasks.</span></span> <span data-ttu-id="f9659-146">Par exemple, affecter toousers de rôle de lecteur hello qui a uniquement besoin d’informations sur l’intégrité de la sécurité hello tooview d’une ressource mais pas effectuer une action, telles que l’application des recommandations ou de la modification des stratégies.</span><span class="sxs-lookup"><span data-stu-id="f9659-146">For example, assign hello Reader role toousers who only need tooview information about hello security health of a resource but not take action, such as applying recommendations or editing policies.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="f9659-147">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f9659-147">Next steps</span></span>
<span data-ttu-id="f9659-148">Cet article explique comment le centre de sécurité utilise RBAC tooassign autorisations toousers et identifié hello autorisé des actions pour chaque rôle.</span><span class="sxs-lookup"><span data-stu-id="f9659-148">This article explained how Security Center uses RBAC tooassign permissions toousers and identified hello allowed actions for each role.</span></span> <span data-ttu-id="f9659-149">Maintenant que vous êtes familiarisé avec les attributions de rôles hello nécessaire toomonitor hello état de sécurité de votre abonnement, modifiez les stratégies de sécurité et appliquer les recommandations, découvrez comment :</span><span class="sxs-lookup"><span data-stu-id="f9659-149">Now that you're familiar with hello role assignments needed toomonitor hello security state of your subscription, edit security policies, and apply recommendations, learn how to:</span></span>

- [<span data-ttu-id="f9659-150">Définir des stratégies de sécurité dans Security Center</span><span class="sxs-lookup"><span data-stu-id="f9659-150">Set security policies in Security Center</span></span>](security-center-policies.md)
- [<span data-ttu-id="f9659-151">Gérer les recommandations de sécurité dans Security Center</span><span class="sxs-lookup"><span data-stu-id="f9659-151">Manage security recommendations in Security Center</span></span>](security-center-recommendations.md)
- [<span data-ttu-id="f9659-152">Surveiller l’intégrité de la sécurité de vos ressources Azure hello</span><span class="sxs-lookup"><span data-stu-id="f9659-152">Monitor hello security health of your Azure resources</span></span>](security-center-monitoring.md)
- [<span data-ttu-id="f9659-153">Gérer et répondre toosecurity des alertes dans le centre de sécurité</span><span class="sxs-lookup"><span data-stu-id="f9659-153">Manage and respond toosecurity alerts in Security Center</span></span>](security-center-managing-and-responding-alerts.md)
- [<span data-ttu-id="f9659-154">Surveiller les solutions de sécurité des partenaires</span><span class="sxs-lookup"><span data-stu-id="f9659-154">Monitor partner security solutions</span></span>](security-center-partner-solutions.md)
