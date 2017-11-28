---
title: Utilisation des portails administrateur et utilisateur dans Azure Stack | Microsoft Docs
description: "Découvrez les différences entre les portails administrateur et utilisateur dans Azure Stack."
services: azure-stack
documentationcenter: 
author: twooley
manager: byronr
editor: 
ms.assetid: 02c7ff03-874e-4951-b591-28166b7a7a79
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: twooley
ms.openlocfilehash: 066de8278d1ef4406cde837da4c7c65304854383
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="using-the-administrator-and-user-portals-in-azure-stack"></a><span data-ttu-id="727bb-103">Utilisation des portails administrateur et utilisateur dans Azure Stack</span><span class="sxs-lookup"><span data-stu-id="727bb-103">Using the administrator and user portals in Azure Stack</span></span>

<span data-ttu-id="727bb-104">Il existe deux portails dans Azure Stack : le portail administrateur et le portail utilisateur (également appelé portail du *locataire*).</span><span class="sxs-lookup"><span data-stu-id="727bb-104">There are two portals in Azure Stack; the administrator portal and the user portal (also referred to as the *tenant* portal).</span></span> <span data-ttu-id="727bb-105">Les portails sont secondés par des instances distinctes d’Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="727bb-105">The portals are backed by separate instances of Azure Resource Manager.</span></span>

<span data-ttu-id="727bb-106">Le tableau suivant montre comment se connecter aux portails et aux points de terminaison Resource Manager dans un environnement du Kit de développement Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="727bb-106">The following table shows how to connect to the portals and to Resource Manager endpoints in an Azure Stack Development Kit environment.</span></span>

|  <span data-ttu-id="727bb-107">Portail</span><span class="sxs-lookup"><span data-stu-id="727bb-107">Portal</span></span> | <span data-ttu-id="727bb-108">URL du portail</span><span class="sxs-lookup"><span data-stu-id="727bb-108">Portal URL</span></span> | <span data-ttu-id="727bb-109">URL de point de terminaison Resource Manager</span><span class="sxs-lookup"><span data-stu-id="727bb-109">Resource Manager endpoint URL</span></span> |   
| -------- | ------------- | ------- |  
| <span data-ttu-id="727bb-110">Administrateur</span><span class="sxs-lookup"><span data-stu-id="727bb-110">Administrator</span></span> | <span data-ttu-id="727bb-111">https://adminportal.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="727bb-111">https://adminportal.local.azurestack.external</span></span>  | <span data-ttu-id="727bb-112">https://adminmanagement.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="727bb-112">https://adminmanagement.local.azurestack.external</span></span>  |  
| <span data-ttu-id="727bb-113">Utilisateur</span><span class="sxs-lookup"><span data-stu-id="727bb-113">User</span></span> | <span data-ttu-id="727bb-114">https://portal.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="727bb-114">https://portal.local.azurestack.external</span></span> | <span data-ttu-id="727bb-115">https://management.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="727bb-115">https://management.local.azurestack.external</span></span>  |
| | |

## <a name="the-administrator-portal"></a><span data-ttu-id="727bb-116">Le portail administrateur</span><span class="sxs-lookup"><span data-stu-id="727bb-116">The administrator portal</span></span>

<span data-ttu-id="727bb-117">Le portail administrateur permet à un opérateur cloud effectuer des tâches d’administration et d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="727bb-117">The administrator portal enables a cloud operator to perform administrative and operational tasks.</span></span> <span data-ttu-id="727bb-118">Un opérateur cloud peut effectuer des opérations telles que :</span><span class="sxs-lookup"><span data-stu-id="727bb-118">A cloud operator can do things such as:</span></span>
* <span data-ttu-id="727bb-119">Surveiller l’intégrité et les alertes</span><span class="sxs-lookup"><span data-stu-id="727bb-119">monitor health and alerts</span></span>
* <span data-ttu-id="727bb-120">Gérer la capacité</span><span class="sxs-lookup"><span data-stu-id="727bb-120">manage capacity</span></span>
* <span data-ttu-id="727bb-121">Renseigner la Place de Marché</span><span class="sxs-lookup"><span data-stu-id="727bb-121">populate the marketplace</span></span>
* <span data-ttu-id="727bb-122">Créer des plans et des offres</span><span class="sxs-lookup"><span data-stu-id="727bb-122">create plans and offers</span></span>
* <span data-ttu-id="727bb-123">Créer des abonnements pour les locataires</span><span class="sxs-lookup"><span data-stu-id="727bb-123">create subscriptions for tenants</span></span>

<span data-ttu-id="727bb-124">Un opérateur cloud peut aussi créer des ressources telles que des machines virtuelles, des réseaux virtuels et des comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="727bb-124">A cloud operator can also create resources such as virtual machines, virtual networks, and storage accounts.</span></span>

 ![Le portail administrateur](media/azure-stack-manage-portals/image1.png)

 ## <a name="the-user-portal"></a><span data-ttu-id="727bb-126">Le portail utilisateur</span><span class="sxs-lookup"><span data-stu-id="727bb-126">The user portal</span></span>

 <span data-ttu-id="727bb-127">Le portail utilisateur ne fournit pas d’accès aux fonctionnalités d’administration ou d’exploitation du portail administrateur.</span><span class="sxs-lookup"><span data-stu-id="727bb-127">The user portal does not provide access to any of the administrative or operational capabilities of the administrator portal.</span></span> <span data-ttu-id="727bb-128">Dans ce portail, un utilisateur peut s’abonner à des offres publiques et utiliser les services qui sont mis à disposition par le biais de ces offres.</span><span class="sxs-lookup"><span data-stu-id="727bb-128">In the user portal, a user can subscribe to public offers, and use the services that are made available through those offers.</span></span>

  ![Le portail utilisateur](media/azure-stack-manage-portals/image2.png)
 
 ## <a name="subscription-behavior"></a><span data-ttu-id="727bb-130">Comportement de l’abonnement</span><span class="sxs-lookup"><span data-stu-id="727bb-130">Subscription behavior</span></span>
 
 <span data-ttu-id="727bb-131">Vous devez bien comprendre les différences suivantes entre le comportement de l’abonnement dans les deux portails.</span><span class="sxs-lookup"><span data-stu-id="727bb-131">Make sure that you understand the following differences between subscription behavior in the two portals.</span></span>

 <span data-ttu-id="727bb-132">Portail administrateur :</span><span class="sxs-lookup"><span data-stu-id="727bb-132">Administrator portal:</span></span>
* <span data-ttu-id="727bb-133">Un seul abonnement est disponible dans le portail administrateur.</span><span class="sxs-lookup"><span data-stu-id="727bb-133">There is only one subscription that is available in the administrator portal.</span></span> <span data-ttu-id="727bb-134">Il s’agit de l’*Abonnement Fournisseur par défaut*.</span><span class="sxs-lookup"><span data-stu-id="727bb-134">This subscription is the *Default Provider Subscription*.</span></span> <span data-ttu-id="727bb-135">Vous ne pouvez pas ajouter d’autres abonnements pour une utilisation dans le portail administrateur.</span><span class="sxs-lookup"><span data-stu-id="727bb-135">You can't add any other subscriptions for use in the administrator portal.</span></span>
* <span data-ttu-id="727bb-136">En tant qu’opérateur cloud, vous pouvez ajouter des abonnements pour vos utilisateurs (y compris vous-même) à partir du portail administrateur.</span><span class="sxs-lookup"><span data-stu-id="727bb-136">As a cloud operator, you can add subscriptions for your users (including yourself) from the administrator portal.</span></span> <span data-ttu-id="727bb-137">Les utilisateurs (y compris vous-même) peuvent accéder à ces abonnements et les utiliser à partir du portail utilisateur.</span><span class="sxs-lookup"><span data-stu-id="727bb-137">Users (including yourself) can access and use these subscriptions from the user portal.</span></span>

  >[!NOTE]
  <span data-ttu-id="727bb-138">En raison de la séparation d’Azure Resource Manager, les abonnements ne traversent pas les portails.</span><span class="sxs-lookup"><span data-stu-id="727bb-138">Because of the Azure Resource Manager separation, subscriptions do not cross portals.</span></span> <span data-ttu-id="727bb-139">Par exemple, si vous-même (en tant qu’opérateur cloud) vous connectez au portail utilisateur, vous ne pouvez pas accéder à l’Abonnement Fournisseur par défaut.</span><span class="sxs-lookup"><span data-stu-id="727bb-139">For example, if you as a cloud operator signs in to the user portal, you can't access the Default Provider Subscription.</span></span> <span data-ttu-id="727bb-140">Ainsi, vous n’avez accès à aucune fonction d’administration.</span><span class="sxs-lookup"><span data-stu-id="727bb-140">Therefore, you don't have access to any administrative functions.</span></span> <span data-ttu-id="727bb-141">Vous pouvez créer des abonnements pour vous-même à partir d’offres publiques, mais vous êtes considéré comme un utilisateur de locataire.</span><span class="sxs-lookup"><span data-stu-id="727bb-141">You can create subscriptions for yourself from public offers, but you are considered a tenant user.</span></span>

<span data-ttu-id="727bb-142">Portail utilisateur :</span><span class="sxs-lookup"><span data-stu-id="727bb-142">User portal:</span></span>
* <span data-ttu-id="727bb-143">Dans le portail utilisateur, un compte peut avoir plusieurs abonnements.</span><span class="sxs-lookup"><span data-stu-id="727bb-143">In the user portal, an account can have multiple subscriptions.</span></span>

  >[!NOTE]
  <span data-ttu-id="727bb-144">Dans l’environnement du Kit de développement, si un utilisateur du locataire appartient au même annuaire que l’opérateur cloud, rien ne l’empêche de se connecter au portail administrateur.</span><span class="sxs-lookup"><span data-stu-id="727bb-144">In the development kit environment, if a tenant user belongs to the same directory as the cloud operator, they are not blocked from signing in to the administrator portal.</span></span> <span data-ttu-id="727bb-145">Toutefois, il ne peut accéder à aucune fonction d’administration.</span><span class="sxs-lookup"><span data-stu-id="727bb-145">However, they can't access any of the administrative functions.</span></span> <span data-ttu-id="727bb-146">En outre, il ne peut pas ajouter d’abonnements ni accéder à des offres qui lui sont mises à disposition dans le portail utilisateur.</span><span class="sxs-lookup"><span data-stu-id="727bb-146">Also, they can't add subscriptions or access offers that are made available to them in the user portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="727bb-147">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="727bb-147">Next steps</span></span>

[<span data-ttu-id="727bb-148">Se connecter à Azure Stack</span><span class="sxs-lookup"><span data-stu-id="727bb-148">Connect to Azure Stack</span></span>](azure-stack-connect-azure-stack.md)

[<span data-ttu-id="727bb-149">Gestion des régions dans Azure Stack</span><span class="sxs-lookup"><span data-stu-id="727bb-149">Region management in Azure Stack</span></span>](azure-stack-region-management.md)
